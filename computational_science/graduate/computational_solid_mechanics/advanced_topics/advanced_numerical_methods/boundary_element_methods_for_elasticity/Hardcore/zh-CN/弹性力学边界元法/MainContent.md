## 引言
在[计算固体力学](@entry_id:169583)领域，[有限元法](@entry_id:749389)（FEM）以其普适性占据主导地位。然而，对于特定类型的问题，例如涉及无限域、裂纹扩展或高[应力集中](@entry_id:160987)的场景，对整个求解域进行网格剖分可能变得异常繁琐甚至不可行。正是在这些领域，[边界元法](@entry_id:141290)（Boundary Element Method, BEM）作为一种强大而优雅的替代方案脱颖而出。BEM的核心思想是将问题的维度降低一维，仅在物体的边界上进行离散和求解，从而根本性地简化了建模过程并能获得极高的精度。

本文旨在为读者提供一份关于弹性力学[边界元法](@entry_id:141290)的全面指南，弥合理论推导与工程应用之间的鸿沟。我们将系统地揭示BEM如何从弹性力学的基本公理出发，演化为一种精密的数值工具。通过本文的学习，读者将不仅理解“如何”使用BEM，更将深刻领会其“为何”在特定问题上表现卓越。

文章将分为三个核心部分展开：
-   **原理与机制**：我们将深入探讨BEM的理论基石，从[Betti互易定理](@entry_id:184528)出发，推导关键的[Somigliana恒等式](@entry_id:755063)和[边界积分方程](@entry_id:746942)，并阐明离散化、[奇异积分](@entry_id:167381)处理等数值实现的核心机制。
-   **应用与跨学科联系**：我们将展示BEM在[断裂力学](@entry_id:141480)、[接触力学](@entry_id:177379)、[复合材料](@entry_id:139856)及[波动力学](@entry_id:166256)等前沿领域的强大应用，并探讨其与计算科学的交叉，如快速多极子等加速算法。
-   **动手实践**：通过一系列精心设计的编程练习，您将亲手处理面力计算、自由项推导和[奇异积分](@entry_id:167381)求值等BEM编程中的关键环节。

让我们首先进入第一章，探索[边界元法](@entry_id:141290)的基本原理与核心机制。

## 原理与机制

[边界元法](@entry_id:141290) (Boundary Element Method, BEM) 的核心思想，是将弹性力学中由[偏微分方程](@entry_id:141332)定义的体域 (volume domain) 问题，转化为仅在物体边界上定义的积分方程问题。相较于需要对整个求解域进行网格剖分的有限元法 (Finite Element Method, FEM)，BEM 仅需离散化问题的边界，从而显著降低了问题的维度。这在处理具有高应力梯度（如断裂力学）或无限域（如岩土工程）的问题时，展现出独特的优势。本章旨在系统阐述弹性力学[边界元法](@entry_id:141290)的基本原理与核心机制，从其理论基石出发，逐步深入到数值实现的关键环节。

### [边界积分方程](@entry_id:746942)的理论基础

[边界积分方程](@entry_id:746942)并非凭空产生，它根植于弹性力学坚实的理论体系。其推导过程巧妙地融合了弹性力学[互易定理](@entry_id:267731)与一个特殊的解析解——基本解。

#### [弹性静力学边值问题](@entry_id:199165)

首先，我们必须精确地定义我们旨在解决的问题。考虑一个由均质、各向同性、线性弹性材料构成的物体，占据了三维空间中的有界域 $\Omega$，其边界为 $\Gamma$。在没有体力的情况下，物体的平衡状态由一组方程和边界条件所描述。[位移场](@entry_id:141476) $\boldsymbol{u}(\boldsymbol{x})$ 必须满足控制方程，即 **Navier-Cauchy 方程**：

$$
\mu \nabla^2 u_i(\boldsymbol{x}) + (\lambda + \mu) \partial_i (\partial_k u_k(\boldsymbol{x})) = 0 \quad \text{in } \Omega
$$

其中，$u_i$ 是位移分量，$\lambda$ 和 $\mu$ 是材料的 **拉梅参数 (Lamé parameters)**，$\nabla^2$ 是[拉普拉斯算子](@entry_id:146319)，$\partial_i$ 表示对坐标 $x_i$ 的偏导数。

在边界 $\Gamma$ 上，我们必须指定边界条件。边界 $\Gamma$ 可以划分为两个不相交的部分，$\Gamma_u$ 和 $\Gamma_t$。在 $\Gamma_u$ 上，位移是已知的（**狄利克雷 (Dirichlet) 条件** 或[位移边界条件](@entry_id:203261)）；在 $\Gamma_t$ 上，面力是已知的（**诺伊曼 (Neumann) 条件** 或[面力边界条件](@entry_id:167112)）。面力向量 $t_i$ 通过柯西公式定义为 $t_i = \sigma_{ij} n_j$，其中 $\sigma_{ij}$ 是应力张量，$n_j$ 是边界外法线向量的分量。

问题的[适定性](@entry_id:148590)（解的[存在性与唯一性](@entry_id:263101)）取决于边界条件的施加方式。如果位移在一个测度大于零的边界部分 ($\text{meas}(\Gamma_u) > 0$) 上被指定，则解是唯一的。然而，对于纯[诺伊曼问题](@entry_id:176713)（即 $\Gamma_u = \emptyset$），解只在刚体位移的意义上是唯一的，并且仅当施加的面力满足整体平衡条件时才存在解 。这些条件是：

$$
\int_{\Gamma} \overline{\boldsymbol{t}} \, \mathrm{d}\Gamma = \boldsymbol{0} \quad \text{and} \quad \int_{\Gamma} \boldsymbol{y} \times \overline{\boldsymbol{t}} \, \mathrm{d}\Gamma = \boldsymbol{0}
$$

这表明总[合力](@entry_id:163825)和总[合力矩](@entry_id:166772)必须为零。

#### Betti [互易定理](@entry_id:267731)：理论基石

推导[边界积分方程](@entry_id:746942)的关键工具是 **Betti [互易定理](@entry_id:267731) (Betti's reciprocal theorem)**。该定理揭示了[线性弹性](@entry_id:166983)系统中不同载荷与位移状态之间的深刻联系。考虑同一个弹性体 $\Omega$ 上的两个独立的平衡状态，状态 (1) 和状态 (2)。每个状态都包含一组相容的[位移场](@entry_id:141476)、应[力场](@entry_id:147325)、[体力](@entry_id:174230)场和边[界面力](@entry_id:184024)场，即 $(\boldsymbol{u}^{(1)}, \boldsymbol{\sigma}^{(1)}, \boldsymbol{b}^{(1)}, \boldsymbol{t}^{(1)})$ 和 $(\boldsymbol{u}^{(2)}, \boldsymbol{\sigma}^{(2)}, \boldsymbol{b}^{(2)}, \boldsymbol{t}^{(2)})$。Betti [互易定理](@entry_id:267731)指出，状态 (1) 的外力（[体力](@entry_id:174230)与面力）在状态 (2) 的[位移场](@entry_id:141476)上所做的功，等于状态 (2) 的外力在状态 (1) 的[位移场](@entry_id:141476)上所做的功。其数学表达式为 ：

$$
\int_{\Gamma} t_i^{(1)}(\boldsymbol{y}) u_i^{(2)}(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y}) + \int_{\Omega} b_i^{(1)}(\boldsymbol{x}) u_i^{(2)}(\boldsymbol{x}) \, \mathrm{d}\Omega(\boldsymbol{x}) = \int_{\Gamma} t_i^{(2)}(\boldsymbol{y}) u_i^{(1)}(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y}) + \int_{\Omega} b_i^{(2)}(\boldsymbol{x}) u_i^{(1)}(\boldsymbol{x}) \, \mathrm{d}\Omega(\boldsymbol{x})
$$

这个定理的成立依赖于[弹性张量](@entry_id:170728) $C_{ijkl}$ 的主对称性，即 $C_{ijkl} = C_{klij}$，它保证了[应变能密度函数](@entry_id:755490)的存在。该定理为我们将[体积分](@entry_id:171119)转化为面积分提供了理论桥梁。

#### 基本解：点力的响应

Betti 定理为我们提供了一个通用的框架。为了得到针对特定问题的具体积分方程，我们需要引入一个特殊的辅助弹性状态。这个状态就是弹性力学中的**基本解 (fundamental solution)**，也称为 **Kelvin 解**。

基本解描述了无限大弹性体在某一点 $\boldsymbol{y}$ 受到一个单位集中力作用时，在另一点 $\boldsymbol{x}$ 产生的位移和应[力场](@entry_id:147325)。它相当于[弹性静力学](@entry_id:198298)控制方程的[格林函数](@entry_id:147802)。对于三维各向同性介质，位移[基本解](@entry_id:184782)张量 $U_{ij}(\boldsymbol{x}, \boldsymbol{y})$ 表示在源点 $\boldsymbol{y}$ 施加 $j$ 方向的单位力时，在场点 $\boldsymbol{x}$ 引起的 $i$ 方向的位移。其表达式为 ：

$$
U_{ij}(\boldsymbol{x}, \boldsymbol{y}) = \frac{1}{16\pi\mu(1-\nu)} \left( \frac{(3-4\nu)\delta_{ij}}{r} + \frac{r_i r_j}{r^3} \right)
$$

其中，$r = \lVert\boldsymbol{x}-\boldsymbol{y}\rVert$ 是源点和场点之间的距离，$r_i = x_i - y_i$，$\mu$ 是剪切模量，$\nu$ 是泊松比，$\delta_{ij}$ 是克罗内克符号。

$U_{ij}(\boldsymbol{x}, \boldsymbol{y})$ 具有以下关键特性：
1.  **对称性**: $U_{ij}(\boldsymbol{x}, \boldsymbol{y}) = U_{ji}(\boldsymbol{x}, \boldsymbol{y})$ 且 $U_{ij}(\boldsymbol{x}, \boldsymbol{y}) = U_{ij}(\boldsymbol{y}, \boldsymbol{x})$。
2.  **奇异性**: 当场点趋近于源点 ($r \to 0$) 时，位移基本解具有 $\mathcal{O}(1/r)$ 的奇异性。
3.  **远场衰减**: 当场点远离源点 ($r \to \infty$) 时，位移以 $\mathcal{O}(1/r)$ 的速度衰减至零。

与位移[基本解](@entry_id:184782) $U_{ij}$ 相对应，我们还可以推导出面力[基本解](@entry_id:184782) $T_{ij}(\boldsymbol{x}, \boldsymbol{y})$，它表示在源点 $\boldsymbol{y}$ 施加 $j$ 方向单位力时，在场点 $\boldsymbol{x}$ 处法线为 $\boldsymbol{n}(\boldsymbol{x})$ 的[截面](@entry_id:154995)上产生的 $i$ 方向面力。它由 $U_{ij}$ 对场点坐标求导并通过[本构关系](@entry_id:186508)得到，其奇异[性比](@entry_id:172643) $U_{ij}$ 更强，为 $\mathcal O(1/r^2)$。

#### Somigliana 恒等式与[边界积分方程](@entry_id:746942)

现在，我们可以将 Betti 定理与[基本解](@entry_id:184782)结合起来。我们在 Betti 定理中选择：
- 状态 (1) 为我们要求解的物理状态 $(\boldsymbol{u}, \boldsymbol{t})$。为简化讨论，我们假设[体力](@entry_id:174230)为零。
- 状态 (2) 为由源点 $\boldsymbol{x}$ 处 $j$ 方向的单位点力所引起的 Kelvin 解 $(\boldsymbol{U}_j, \boldsymbol{T}_j)$。

由于 Kelvin 解在源点 $\boldsymbol{x}$ 处是奇异的，我们不能直接在整个域 $\Omega$ 上应用 Betti 定理。标准的处理方法是先将包含[奇异点](@entry_id:199525) $\boldsymbol{x}$ 的一个小球（或二维情况下的圆）$B_\epsilon$ 从 $\Omega$ 中挖去，然后在剩下的正则域 $\Omega \setminus B_\epsilon$ 上应用 Betti 定理。接着，通过一个极限过程，让小球的半径 $\epsilon \to 0$。经过严谨的推导，我们最终得到 **Somigliana 位移恒等式**，它给出了域内任意一点 $\boldsymbol{x}$ 的位移表达式：

$$
u_j(\boldsymbol{x}) = \int_{\Gamma} U_{ij}(\boldsymbol{x}, \boldsymbol{y}) t_i(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y}) - \int_{\Gamma} T_{ij}(\boldsymbol{x}, \boldsymbol{y}) u_i(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y})
$$

这个恒等式意义非凡：它表明域内任意一点的位移完全由边界上的位移和面力决定。这正是将问题从“体”降至“界”的关键一步。

然而，Somigliana 恒等式还不是最终的求解方程，因为它牵涉到我们尚不知道的边界量。为了求解这些未知的边界量，我们需要将源点 $\boldsymbol{x}$ 移动到边界 $\Gamma$ 上。这个极限过程需要特别小心处理，因为此时积分核 $T_{ij}(\boldsymbol{x}, \boldsymbol{y})$ 在 $\boldsymbol{y} \to \boldsymbol{x}$ 时呈现强奇异性。

当源点 $\boldsymbol{x}$ 位于边界 $\Gamma$ 上时，极限过程会产生一个额外的项，称为**自由项 (free-term)**。最终的**[边界积分方程](@entry_id:746942) (Boundary Integral Equation, BIE)** 形式如下 ：

$$
c_{ij}(\boldsymbol{x}) u_j(\boldsymbol{x}) + \int_{\Gamma} T_{ij}(\boldsymbol{x}, \boldsymbol{y}) u_j(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y}) = \int_{\Gamma} U_{ij}(\boldsymbol{x}, \boldsymbol{y}) t_j(\boldsymbol{y}) \, \mathrm{d}\Gamma(\boldsymbol{y})
$$

这里的积分 $\int_{\Gamma} T_{ij}...$ 是在 **[柯西主值](@entry_id:192761) (Cauchy Principal Value)** 意义下定义的。

系数 $c_{ij}(\boldsymbol{x})$ 是一个与源点 $\boldsymbol{x}$ 处边界局部几何形状相关的张量。对于[各向同性材料](@entry_id:170678)，它可以简化为 $c_{ij}(\boldsymbol{x}) = c(\boldsymbol{x}) \delta_{ij}$。这个标量系数 $c(\boldsymbol{x})$ 有着明确的几何意义：它代表了从点 $\boldsymbol{x}$ 看过去，弹性体所占空间立体角与全空间立体角 ($4\pi$) 的比值（对于二维问题，则是平面角与 $2\pi$ 的比值）。
-   对于**光滑边界**点，弹性体占据一[半空间](@entry_id:634770)，所以[立体角](@entry_id:154756)为 $2\pi$，因此 $c(\boldsymbol{x}) = \frac{2\pi}{4\pi} = \frac{1}{2}$。
-   对于**角点或棱边**，该值取决于弹性体在该点的内角。例如，在一个二维问题中，如果一个外角点（相对于弹性体是凹角）的内角为 $\alpha(\boldsymbol{x})$，则 $c(\boldsymbol{x}) = \frac{\alpha(\boldsymbol{x})}{2\pi}$。对于一个外边界为正方形的无限大平面中的孔洞问题，在孔洞的凸角处（相对于求解域是凹角），内角为 $\frac{3\pi}{2}$，因此 $c = \frac{3\pi/2}{2\pi} = \frac{3}{4}$ 。而在一个光滑的[共线点](@entry_id:174222)上，内角为 $\pi$，因此 $c=1/2$ [@problem_id:3547822, @problem_id:3547846]。

### 数值实现的关键概念

我们已经获得了[边界积分方程](@entry_id:746942)，这是一个关于边界未知量的连续方程。为了进行数值求解，必须将其离散化为代数方程组。

#### 离散化：等参元

离散化的第一步是将边界 $\Gamma$ 剖分成一系列小的**边界单元 (boundary elements)**。然后，在每个单元内部，我们用一组节点值和形函数来近似表示几何形状以及未知的边界场量（位移和面力）。

一种高效且广泛使用的方法是**等参元 (isoparametric element)** 方法。其核心思想是，用同一套形函数 $N_a$ 及其对应的节点值来插值描述单元的几何坐标 $\boldsymbol{x}$ 和单元上的场函数（如位移 $u$ 和面力 $t$）。

例如，对于一个由节点 $\boldsymbol{x}_1, \boldsymbol{x}_2, \boldsymbol{x}_3$ 定义的二维二次曲线单元，其几何和场量可以表示为：
$$
\boldsymbol{x}(\xi) = \sum_{a=1}^{3} N_a(\xi) \boldsymbol{x}_a, \quad u(\xi) = \sum_{a=1}^{3} N_a(\xi) u_a, \quad t(\xi) = \sum_{a=1}^{3} N_a(\xi) t_a
$$
其中 $\xi \in [-1, 1]$ 是单元上的[局部坐标](@entry_id:181200)，$N_a(\xi)$ 是拉格朗日二次形函数。常见的形函数包括用于直线段的线性函数、用于曲线段的二次函数，以及用于[曲面](@entry_id:267450)的[双线性](@entry_id:146819)或双二次函数 。

在进行积[分时](@entry_id:274419)，需要将物理坐标下的积分转换到局部参考[坐标系](@entry_id:156346)下。这需要引入一个 **[雅可比](@entry_id:264467) (Jacobian)** [行列式](@entry_id:142978) $J(\xi)$。例如，对于线单元，$ds = \lVert \frac{\partial \boldsymbol{x}}{\partial \xi} \rVert d\xi = J(\xi) d\xi$。

#### [奇异积分](@entry_id:167381)的处理

[边界元法](@entry_id:141290)的数值实现中最具挑战性的部分是如何精确计算 BIE 中的积分，特别是当源点 $\boldsymbol{x}$ 和积分点 $\boldsymbol{y}$ 位于同一个单元上时，积分核会呈现奇异性。根据奇异性的强度，我们可以将这些积分分类 ：

1.  **正则积分 (Regular Integrals)**: 当源点和积分单元相距较远时，被积函数是光滑的，可以使用标准的[数值求积](@entry_id:136578)方法（如高斯求积）精确计算。

2.  **弱[奇异积分](@entry_id:167381) (Weakly Singular Integrals)**: 这发生在对 $U_{ij}$ 核（奇异性为 $\mathcal{O}(1/r)$）进行积[分时](@entry_id:274419)。虽然被积函数在 $r=0$ 处无界，但积分本身是收敛的。这类积分可以通过特殊的[坐标变换](@entry_id:172727)（如 Duffy 变换）将奇异性消除，然后使用标准求积。

3.  **强[奇异积分](@entry_id:167381) (Strongly Singular Integrals)**: 这发生在对 $T_{ij}$ 核（奇异性为 $\mathcal{O}(1/r^2)$）进行积[分时](@entry_id:274419)。积分在常规意义下是发散的，必须在[柯西主值](@entry_id:192761)意义下进行计算。数值上，这通常通过“刚体位移法”间接计算，或者使用解析/半解析方法处理奇异部分。

4.  **[超奇异积分](@entry_id:750482) (Hypersingular Integrals)**: 当对面力方程（即对位移 BIE 进行[微分](@entry_id:158718)）进行积[分时](@entry_id:274419)，会出现更高阶的 $\mathcal{O}(1/r^3)$ 奇异性。这类积分需要在 Hadamard 有限部分意义下进行解释，其数值处理更为复杂，通常需要借助格林第二公式进行正则化或采用伽辽金等弱形式方法。

#### 直接法与间接法

我们以上推导的 BIE 称为**直接[边界元法](@entry_id:141290) (Direct BEM)**，因为方程中的未知量是物理上真实的边界位移和面力。这是目前最主流的 BEM 形式。

与之相对的是**间接[边界元法](@entry_id:141290) (Indirect BEM)**。间接法不直接求解物理量，而是假设解可以由[分布](@entry_id:182848)在边界上的虚拟源（如单层势和双层势）的密度函数 $\boldsymbol{\phi}$ 和 $\boldsymbol{\psi}$ 来表示。通过施加边界条件，建立关于这些非物理密度函数的[积分方程](@entry_id:138643)。解出密度函数后，再通过积分计算域内或边界上的物理量。

直接法和间接法在处理不同类型的边界问题时，会导出不同性质的积分方程。例如，对于纯位移边界问题（[Dirichlet 问题](@entry_id:274408)），直接法导出一个关于未知面力的**第一类 Fredholm [积分方程](@entry_id:138643)**，而间接法（采用双层势）则导出一个关于密度函数的**第二类 Fredholm 积分方程**。第二[类方程](@entry_id:144428)由于含有[恒等算子](@entry_id:204623)项，通常具有更好的数学性质和[数值稳定性](@entry_id:146550) 。

### 高级主题与应用

#### 无限域问题

BEM 的一个突出优点是它能自然地处理**无限域问题**（或称外部问题），例如计算地下洞室周围的应力或流体中障碍物的绕流。对于此类问题，除了内部边界条件外，解还必须满足**无穷远处的[衰减条件](@entry_id:157952) (decay conditions at infinity)**。

-   在三维问题中，位移场 $\boldsymbol{u}(\boldsymbol{x})$ 和应力/面[力场](@entry_id:147325) $\boldsymbol{t}(\boldsymbol{x})$ 必须分别满足 $\mathcal{O}(r^{-1})$ 和 $\mathcal{O}(r^{-2})$ 的衰减率。
-   在二维问题中，情况更为复杂，衰减行为与边界上的载荷是否自平衡有关。若载荷自平衡，则衰减率与三维情况类似；若不平衡，位移场可能呈现对数增长 。

BEM 之所以能优雅地处理这类问题，是因为其所使用的 Kelvin [基本解](@entry_id:184782)本身就在无限域中定义，并自动满足了相应的[衰减条件](@entry_id:157952)。在推导 BIE 时，沿无穷远处边界的积分项会自然消失（在载荷平衡的情况下），因此无需像有限元法那样设置一个巨大的人工截断边界 。

#### 纯[诺伊曼问题](@entry_id:176713)与[刚体模态](@entry_id:754366)

当整个边界都施加面力条件时（纯[诺伊曼问题](@entry_id:176713)），BEM 会遇到一个特殊的挑战。从物理上看，如果一个物体不受任何位移约束，那么在给定一组平衡力系的作用下，它的任何**刚体位移 (rigid body motion)**（平动和转动）都不会产生应变和应力。因此，问题的解不是唯一的，它可以在任意一个刚体位移的基础上叠加。

这种物理上的不确定性反映在 BEM 的离散代数方程组 $[H]\{u\} = [G]\{t\}$ 上，就是系数矩阵 $[H]$ 是**奇异的 (singular)** 或称**[秩亏](@entry_id:754065)的 (rank-deficient)** 。其[零空间](@entry_id:171336)恰好对应于离散的刚体位移模态。在三维空间中，有3个平动模态和3个转动模态，因此矩阵 $[H]$ 的[秩亏](@entry_id:754065)数为6；在二维空间中则为3。

要获得唯一解，必须采取措施消除这种不确定性：
1.  **存在性条件**：首先，施加的面力必须是自平衡的，即[合力](@entry_id:163825)与[合力矩](@entry_id:166772)为零。若不满足，则[方程组](@entry_id:193238)无解，这对应于物体会做刚体加速运动，不存在[静力平衡](@entry_id:163498)解 。
2.  **唯一性约束**：其次，必须施加额外的约束来固定物体的刚体位移。常见的方法有：
    -   **固定位移**：在边界上选择足够多的点（3D 中至少3个非[共线点](@entry_id:174222)，共6个位移分量）并将其位移值设为零。
    -   **约束方程**：通过[拉格朗日乘子法](@entry_id:176596)等方式，在代数方程组中加入关于整体位移的[约束方程](@entry_id:138140)，例如要求边界位移的均值为零 。

通过这些原理和机制，[边界元法](@entry_id:141290)为弹性力学问题提供了一套强大而优雅的求解框架，尤其是在处理特定类型的问题时，其优势无可替代。