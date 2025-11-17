## 引言
[边界元法](@entry_id:141290)（Boundary Element Method, BEM）是一种功能强大的数值技术，它通过将[偏微分方程](@entry_id:141332)的求解从整个体积域转移到其边界上，为科学与工程计算提供了一条优雅而高效的路径。这种根本性的维度降低，使其在处理具有复杂几何、无限域或物理量主要集中在边界上的问题时，展现出相较于[有限元法](@entry_id:749389)等区域方法的独特优势。然而，从经典的[偏微分方程](@entry_id:141332)到最终的数值解，这一过程涉及深刻的数学原理和复杂的数值挑战，尤其是在如何构建[积分方程](@entry_id:138643)以及如何处理其固有的奇异性方面，存在着显著的知识鸿沟。

本文旨在系统地揭示[边界元法](@entry_id:141290)的内在机制和实践应用。我们将分为三个核心部分，引导读者完成从理论到实践的认知跨越。
- 在“**原理与机制**”一章中，我们将追溯BEM的数学源头，从[格林公式](@entry_id:173118)出发，推导核心的[边界积分方程](@entry_id:746942)。我们将深入剖析不同类型的[边界积分算子](@entry_id:173789)，并详细阐述处理弱奇异、强奇异及[超奇异积分](@entry_id:750482)这一关键挑战的数学工具和数值策略。最后，我们将讨论如何通过离散化将积分方程转化为线性代数系统，并分析不同离散方案的数值性能。
- 接着，在“**应用与跨学科连接**”一章中，我们将展示BEM的强大威力，探讨其在[固体力学](@entry_id:164042)、[声学](@entry_id:265335)、[流体动力学](@entry_id:136788)、计算化学等多个领域的具体应用。本章还将介绍FEM-BEM耦合、双互易方法等高级格式，以及[快速多极子方法](@entry_id:140932)（FMM）和[层次矩阵](@entry_id:750262)等前沿加速算法，这些技术使得BEM能够胜任大规模复杂问题的求解。
- 最后，在“**动手实践**”部分，我们将通过一系列精心设计的编程练习，让读者亲手实现并验证BEM的核心概念，从而将理论知识转化为解决实际问题的能力。

通过本次学习，您将对[边界元法](@entry_id:141290)建立一个全面而深刻的理解，掌握其背后的数学精髓，并了解其在现代科学与工程计算前沿的应用潜力。

## 原理与机制

[边界元法](@entry_id:141290)（Boundary Element Method, BEM）的理论核心是将一个在求解域 $\Omega$ 内定义的[偏微分方程](@entry_id:141332)（Partial Differential Equation, PDE）转化为一个仅在其边界 $\partial\Omega$ 上定义的[积分方程](@entry_id:138643)。这一转化过程极大地降低了问题的维度，从而成为 BEM 相比于区域方法（如[有限元法](@entry_id:749389)）的根本优势。本章将系统地阐述实现这一转化的基本原理，并深入探讨由此产生的[边界积分算子](@entry_id:173789)、[奇异积分](@entry_id:167381)处理、离散化策略及其[数值分析](@entry_id:142637)的关键机制。

### 从[格林公式](@entry_id:173118)到[边界积分方程](@entry_id:746942)

[边界元法](@entry_id:141290)的推导始于一个经典的数学工具：**[格林公式](@entry_id:173118)（Green's Identities）**。对于定义在有界域 $\Omega \subset \mathbb{R}^d$ 上的两个足够光滑的函数 $u$ 和 $v$，格林第二公式表述为：
$$
\int_{\Omega} (u \Delta v - v \Delta u) \, d\Omega = \int_{\partial\Omega} (u \frac{\partial v}{\partial n} - v \frac{\partial u}{\partial n}) \, d\Gamma
$$
其中 $\Delta$ 是[拉普拉斯算子](@entry_id:146319)，$\partial/\partial n$ 表示沿边界 $\partial\Omega$ 的外[法向导数](@entry_id:169511)。

这个公式将域内（体积）积分与边界（面积或弧长）积分联系起来。BEM 的巧妙之处在于，选择其中一个函数 $v$ 为[偏微分方程](@entry_id:141332)的**基本解（fundamental solution）**。基本解，通常记为 $G(\mathbf{x}, \mathbf{y})$，是特定微分算子 $L$ 在点源 $\mathbf{y}$ 作用下的响应，其定义为 $L_{\mathbf{x}} G(\mathbf{x}, \mathbf{y}) = -\delta(\mathbf{x}-\mathbf{y})$，其中 $\delta$ 是狄拉克-德尔塔[分布](@entry_id:182848)。

以[拉普拉斯方程](@entry_id:143689) $\Delta u = 0$ 为例，其在二维和三维空间中的[基本解](@entry_id:184782)具有不同的形式。通过求解 $\Delta G = -\delta$，可以推导出 [@problem_id:2560788] [@problem_id:2560748]：
- 在三维空间 ($d=3$) 中, $G(\mathbf{x}, \mathbf{y}) = \frac{1}{4\pi r}$，其中 $r = \|\mathbf{x}-\mathbf{y}\|$。
- 在二维空间 ($d=2$) 中, $G(\mathbf{x}, \mathbf{y}) = -\frac{1}{2\pi} \ln(r)$。

注意到三维[基本解](@entry_id:184782)具有 $r^{-1}$ 型的代数奇性，而二维[基本解](@entry_id:184782)具有较弱的 $\ln(r)$ 型对数奇性。这一差异对[数值积分](@entry_id:136578)和算法性能有深远影响，我们将在后续讨论。

现在，我们将格林第二公式应用于函数 $u$（PDE的待求未知解）和基本解 $G(\mathbf{x}, \mathbf{y})$（其中 $\mathbf{x}$ 是一个固定的“源点”或“观察点”）。由于 $G$ 在 $\mathbf{y} = \mathbf{x}$ 处是奇异的，我们不能直接在整个域 $\Omega$ 上应用[格林公式](@entry_id:173118)。标准做法是先将点 $\mathbf{x}$ 用一个半径为 $\varepsilon$ 的小球（或圆）$B_{\varepsilon}(\mathbf{x})$ 挖去，在余下的正则域 $\Omega \setminus B_{\varepsilon}(\mathbf{x})$ 上应用公式，然后取极限 $\varepsilon \to 0$。

假设 $u$ 在 $\Omega$ 内满足 $\Delta u = 0$，并且 $\Delta_{\mathbf{y}} G(\mathbf{x}, \mathbf{y}) = 0$ 对于 $\mathbf{y} \neq \mathbf{x}$ 成立，[格林公式](@entry_id:173118)左端的[体积分](@entry_id:171119)项消失。经过这个极限过程，源点 $\mathbf{x}$ 处的奇异性会产生一个额外的项，最终我们得到**[边界积分方程](@entry_id:746942)（Boundary Integral Equation, BIE）** [@problem_id:2560780]：
$$
c(\mathbf{x}) u(\mathbf{x}) + \int_{\partial\Omega} u(\mathbf{y}) \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{y}}} \, d\Gamma_{\mathbf{y}} = \int_{\partial\Omega} \frac{\partial u(\mathbf{y})}{\partial n_{\mathbf{y}}} G(\mathbf{x}, \mathbf{y}) \, d\Gamma_{\mathbf{y}}
$$
这个方程是 BEM 的基石。它表明，只要我们知道边界上 $u$ 和其[法向导数](@entry_id:169511) $\partial u / \partial n$ 的值，就可以求出域内任意点 $\mathbf{x}$ 处的解 $u(\mathbf{x})$。

方程中的系数 $c(\mathbf{x})$ 被称为**自由项（free term）**，它取决于点 $\mathbf{x}$ 处的局部几何。
- 如果 $\mathbf{x}$ 在域 $\Omega$ 内部，则 $c(\mathbf{x}) = 1$。
- 如果 $\mathbf{x}$ 在域 $\Omega$ 外部，则 $c(\mathbf{x}) = 0$。
- 如果 $\mathbf{x}$ 位于边界 $\partial\Omega$ 上，则 $c(\mathbf{x})$ 等于点 $\mathbf{x}$ 处的内[立体角](@entry_id:154756)（三维）或内角（二维）与总[立体角](@entry_id:154756)（$4\pi$）或总角（$2\pi$）之比。例如，在边界光滑处，域占据一[半空间](@entry_id:634770)，因此 $c(\mathbf{x}) = 1/2$。这对于二维、三维乃至[轴对称](@entry_id:173333)问题都是成立的，因为光滑性意味着局部边界可由一个平面近似 [@problem_id:2560780]。

为了使上述推导在数学上严谨，特别是在处理非光滑边界（如带尖角的多边形或多面体）时，我们需要更现代的泛函分析工具。[格林公式](@entry_id:173118)的[弱形式](@entry_id:142897)要求函数属于**索博列夫空间（Sobolev spaces）**，如 $H^1(\Omega)$。为了确保边界积分有意义，我们需要**[迹定理](@entry_id:203967)（trace theorems）**，它保证了 $H^1(\Omega)$ 中的函数在边界 $\partial\Omega$ 上存在一个“迹”，这个迹位于分数阶索博列夫空间 $H^{1/2}(\partial\Omega)$ 中。同样，[法向导数](@entry_id:169511)也需要被推广为 $H^{-1/2}(\partial\Omega)$ 中的一个[分布](@entry_id:182848)。这些理论成立的最小边界[正则性条件](@entry_id:166962)是**利普希茨连续（Lipschitz continuous）**。一个多边形或[多面体](@entry_id:637910)域就是典型的[利普希茨域](@entry_id:751354)，因此 BEM 的数学框架在其上是完全成立的 [@problem_id:2560749]。

### [边界积分算子](@entry_id:173789)与[奇异积分](@entry_id:167381)

上述[边界积分方程](@entry_id:746942)可以更紧凑地写作算子形式。为此，我们定义几个核心的**[边界积分算子](@entry_id:173789)**：
- **单层势算子（Single-layer potential operator）** $V$：
$$ (V\phi)(\mathbf{x}) = \int_{\Gamma} G(\mathbf{x}, \mathbf{y}) \phi(\mathbf{y}) \, d\Gamma_{\mathbf{y}} $$
- **双层势算子（Double-layer potential operator）** $K$：
$$ (K\phi)(\mathbf{x}) = \int_{\Gamma} \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{y}}} \phi(\mathbf{y}) \, d\Gamma_{\mathbf{y}} $$
- **伴随双层势算子（Adjoint double-layer operator）** $K'$：
$$ (K'\phi)(\mathbf{x}) = \int_{\Gamma} \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{x}}} \phi(\mathbf{y}) \, d\Gamma_{\mathbf{y}} $$
- **超奇异算子（Hypersingular operator）** $W$：
$$ (W\phi)(\mathbf{x}) = -\frac{\partial}{\partial n_{\mathbf{x}}} \int_{\Gamma} \frac{\partial G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{y}}} \phi(\mathbf{y}) \, d\Gamma_{\mathbf{y}} = \int_{\Gamma} \left(-\frac{\partial^2 G(\mathbf{x}, \mathbf{y})}{\partial n_{\mathbf{x}}\partial n_{\mathbf{y}}}\right) \phi(\mathbf{y}) \, d\Gamma_{\mathbf{y}} $$

当源点 $\mathbf{x}$ 也位于边界上时，这些积分的核函数在 $\mathbf{y} \to \mathbf{x}$ 时会表现出不同程度的奇异性。正确理解和处理这些[奇异积分](@entry_id:167381)是 BEM 的核心挑战之一。积分的奇异性可以分为三类 [@problem_id:2560788]：

1.  **弱[奇异积分](@entry_id:167381)（Weakly Singular Integrals）**：
    这类积分的[核函数](@entry_id:145324)虽然在 $\mathbf{y} = \mathbf{x}$ 处趋于无穷，但其积分在勒贝格（Lebesgue）意义下是收敛的。单层势算子 $V$ 就属于此类。
    - 在 3D 中，核 $G \sim r^{-1}$，在一个二维[曲面](@entry_id:267450)上的积分类似于 $\int r^{-1} \cdot r \,dr \,d\theta$，是可积的。
    - 在 2D 中，核 $G \sim \ln r$，在一个一维曲线上的积分类似于 $\int \ln r \, dr$，也是可积的。
    对于弱[奇异积分](@entry_id:167381)，无需特殊的积分定义。即使采用对称挖去小邻域再取极限的方式（即[柯西主值](@entry_id:192761)的定义方式），其结果也与常规的[勒贝格积分](@entry_id:140189)值相同，且该值不依赖于挖去区域的形状 [@problem_id:2560731]。

2.  **强[奇异积分](@entry_id:167381)（Strongly Singular Integrals）**：
    这类积分的核函数奇异性更强，以至于积分发散，但可以通过对称抵消来定义一个有限值。这需要**[柯西主值](@entry_id:192761)（Cauchy Principal Value, CPV）**积分。双层势算子 $K$ 和其伴随算子 $K'$ 属于此类。
    - 在 3D 中，核 $\partial G/\partial n \sim r^{-2}$，在[曲面积分](@entry_id:144805)中行为如 $\int r^{-2} \cdot r \,dr \,d\theta = \int r^{-1} \,dr$，导致对数发散。
    - 在 2D 中，核 $\partial G/\partial n \sim r^{-1}$，在线积分中行为如 $\int r^{-1} \,dr$，也导致对数发散。
    [柯西主值](@entry_id:192761)的思想是，通过对称地挖去[奇异点](@entry_id:199525)周围的邻域（例如，一个球或圆盘）进行积分，然后取邻域半径趋于零的极限。由于核函数通常具有奇对称性，正负部分的贡献会相互抵消，从而得到一个有限的结果。

3.  **[超奇异积分](@entry_id:750482)（Hypersingular Integrals）**：
    这类积分的奇异性最强，即使在[柯西主值](@entry_id:192761)意义下也发散。超奇异算子 $W$ 属于此类，其核函数 $\partial^2 G/\partial n_{\mathbf{x}} \partial n_{\mathbf{y}}$ 的行为如 $r^{-(d+1)}$（在 $d$ 维空间中）。要处理这类积分，需要更高级的[正则化技术](@entry_id:261393)，即**哈达玛有限部分（Hadamard Finite-Part）**积分。
    其核心思想是，在积分前，从密度函数 $\phi(\mathbf{y})$ 中减去其在[奇异点](@entry_id:199525) $\mathbf{x}$ 附近的[泰勒展开](@entry_id:145057)的前几项。例如，对于超奇异算子，我们需要减去零阶和一阶项：
    $$
    (W\phi)(\mathbf{x}) := \lim_{\varepsilon\to 0^+} \int_{\Gamma\setminus B_{\varepsilon}(\mathbf{x})} \frac{\partial^2 G(\mathbf{x},\mathbf{y})}{\partial n_{\mathbf{x}}\partial n_{\mathbf{y}}}\,\Big(\phi(\mathbf{y}) - \phi(\mathbf{x}) - \nabla_{\Gamma}\phi(\mathbf{x})\cdot (\mathbf{y}-\mathbf{x})\Big)\, d\Gamma_{\mathbf{y}}
    $$
    其中 $\nabla_{\Gamma}\phi$ 是 $\phi$ 的[曲面梯度](@entry_id:261146)。由于被积函数 $\phi(\mathbf{y}) - \phi(\mathbf{x}) - \dots$ 在 $\mathbf{y} \to \mathbf{x}$ 时以 $\mathcal{O}(r^2)$ 的速度趋于零，它恰好能够“抵消”核函数 $r^{-(d+1)}$ 的过强奇异性（在 $d-1$ 维[曲面积分](@entry_id:144805)后为 $r^{-2}$），使得积分的极限存在且有限 [@problem_id:2560792]。

### 离散化：从 BIE 到[线性系统](@entry_id:147850)

为了数值求解[边界积分方程](@entry_id:746942)，我们需要将其离散化，转换成一个线性[代数方程](@entry_id:272665)组 $A\boldsymbol{\phi} = \boldsymbol{b}$。这个过程被称为[边界元法](@entry_id:141290)。

首先，我们将边界 $\Gamma$ 剖分成一系列小的**边界单元（boundary elements）** $\Gamma_e$。然后，在每个单元上，我们用一组**形函数（shape functions）** $N_i$ 和相应的节点值来近似表示边界的几何形状和未知的边界函数（例如 $\phi$）。

**等参元（Isoparametric element）**概念在 BEM 中被广泛使用，它指的是使用同一组形函数来表示几何和未知量 [@problem_id:2560776]。例如，对于一个由多个节点 $\mathbf{x}_i$ 定义的[曲边单元](@entry_id:748117)，其上任意一点的坐标可以表示为：
$$ \mathbf{x}(\boldsymbol{\xi}) = \sum_{i} N_i(\boldsymbol{\xi}) \mathbf{x}_i $$
同样，该单元上的未知函数 $\phi$ 也被近似为：
$$ \phi(\boldsymbol{\xi}) = \sum_{i} N_i(\boldsymbol{\xi}) \phi_i $$
其中 $\boldsymbol{\xi}$ 是定义在标准“参考单元”（如 $[-1, 1]$ 线段或单位三角形）上的[局部坐标](@entry_id:181200)，$\phi_i$ 是待求的节点值。

在计算边界积分时，我们需要将物理单元上的积分转换到[参考单元](@entry_id:168425)上。这涉及到**雅可比行列式（Jacobian）**的计算，它描述了微元长度或面积的变换关系。
- 对于一维曲线单元（参数为 $\xi$），$d\Gamma = J(\xi) d\xi$，其中[雅可比](@entry_id:264467)为 $J(\xi) = \|\frac{d\mathbf{x}}{d\xi}\|_2$。
- 对于二维[曲面](@entry_id:267450)单元（参数为 $(\xi, \eta)$），$d\Gamma = J(\xi, \eta) d\xi d\eta$，其中[雅可比](@entry_id:264467)为 $J(\xi, \eta) = \|\frac{\partial\mathbf{x}}{\partial\xi} \times \frac{\partial\mathbf{x}}{\partial\eta}\|_2$。

例如，对于一个由两节点 $\mathbf{x}_1, \mathbf{x}_2$ 定义的直线元，使用 $[-1, 1]$ 上的线性形函数，其[雅可比](@entry_id:264467)是一个常数 $J = \|\mathbf{x}_2 - \mathbf{x}_1\| / 2$ [@problem_id:2560776]。

将这些离散表示代入[边界积分方程](@entry_id:746942)后，我们需要一种方法来强制该方程成立，从而得到一个封闭的线性系统。最常用的两种方法是**[配置法](@entry_id:142690)（Collocation Method）**和**[伽辽金法](@entry_id:749698)（Galerkin Method）**。

- **[配置法](@entry_id:142690)**：选取一系列离散的[配置点](@entry_id:169000)（通常是单元节点），并要求离散后的[边界积分方程](@entry_id:746942)在这些点上精确成立。这相当于用狄拉克-[德尔塔函数](@entry_id:273429)作为权函数。
- **[伽辽金法](@entry_id:749698)**：要求离散方程的残差与近似空间中的所有[基函数](@entry_id:170178)（或权函数）正交。这导致了一个[变分形式](@entry_id:166033)的方程，例如 $\langle V\phi_h, \psi_h \rangle = \langle g, \psi_h \rangle$ 对所有测试函数 $\psi_h$ 成立。

### [数值分析](@entry_id:142637)与性能

不同的离散方法和[积分方程](@entry_id:138643)形式导致了不同的数值特性，理解这些特性对于选择和实现高效的 BEM 至关重要。

#### [伽辽金法](@entry_id:749698) vs. [配置法](@entry_id:142690)

[伽辽金法](@entry_id:749698)通常具有更优的数学性质。对于像单层势算子 $V$ 这样的**强制（coercive）**算子，[伽辽金法](@entry_id:749698)保证是稳定且准最优的。这意味着离散系统的解是唯一存在的，且误差以最优速率收敛 [@problem_id:2560773]。相比之下，[配置法](@entry_id:142690)的稳定性没有普适的理论保证，它依赖于一个离散的 [inf-sup 条件](@entry_id:174538)，这个条件是否满足与[基函数](@entry_id:170178)的选取和[配置点](@entry_id:169000)的位置密切相关。在某些情况下，例如[配置点](@entry_id:169000)聚集时，[配置法](@entry_id:142690)可能会变得不稳定。此外，伽辽-金法的变分（积分平均）性质使其对[数值积分误差](@entry_id:137490)的容忍度更高，而[配置法](@entry_id:142690)的点态性质使其对奇异或[近奇异积分](@entry_id:752383)的计算精度更为敏感 [@problem_id:2560773]。

#### 一类方程 vs. 二[类方程](@entry_id:144428)

[边界积分方程](@entry_id:746942)可以根据其算子结构分为**第一类（first-kind）**和**第二类（second-kind）** Fredholm 积分方程。
- **第一[类方程](@entry_id:144428)**：形式为 $A\phi=f$，其中 $A$ 是一个[紧算子](@entry_id:139189)或平滑算子。例如，用单层势求解狄氏问题的方程 $V\phi=g$。
- **第二类方程**：形式为 $(\lambda I + A)\phi=f$，其中 $A$ 是紧算子，$I$ 是[恒等算子](@entry_id:204623)。例如，用双层势求解[诺伊曼问题](@entry_id:176713)的方程 $(\frac{1}{2}I + K)\phi=f$。

从[伪微分算子](@entry_id:192996)的角度看，这些算子具有不同的阶数。例如，对于拉普拉斯问题，$V$ 是 -1 阶算子（平滑），$W$ 是 +1 阶算子（[微分](@entry_id:158718)），而 $K, K'$ 是 0 阶算子。算子的阶数 $\alpha$ 直接决定了伽辽金离散矩阵 $A_h$ 的条件数 $\kappa(A_h)$ 如何随网格尺寸 $h$ 变化 [@problem_id:2560758]：
$$ \kappa(A_h) \sim \mathcal{O}(h^{-|\alpha|}) $$
- 对于第一类方程（如 $V\phi=g$, $\alpha=-1$），条件数随[网格加密](@entry_id:168565)而恶化，$\kappa(A_h) \sim \mathcal{O}(h^{-1})$。
- 对于第二[类方程](@entry_id:144428)（如 $(\frac{1}{2}I + K)\phi=f$, $\alpha=0$），条件数在[网格加密](@entry_id:168565)时保持有界，$\kappa(A_h) \sim \mathcal{O}(1)$。

因此，第二类[积分方程](@entry_id:138643)通常具有更好的[数值条件](@entry_id:136760)，这使得它们在迭代求解时收敛更快，结果更鲁棒。

#### 二维外问题与额外约束

在二维外问题中，拉普拉斯方程的基本解 $\ln(r)$ 在无穷远处是对数增长的。这导致一个特殊的挑战：由单层势表示的解 $u = V\phi$ 在无穷远处也会对数增长，除非其总“[电荷](@entry_id:275494)”为零，即 $\int_{\Gamma} \phi \,d\Gamma = 0$。为了获得物理上有意义的（即在无穷远处有界的）解，必须施加这个零均值约束。在离散系统中，若不施加此约束，单层势算子矩阵将变得近乎奇异（有一个对应于常数密度函数的近零[特征值](@entry_id:154894)），导致严重的病态问题 [@problem_id:2560748]。

### 计算复杂度与快速算法

传统 BEM 的一个主要瓶颈是其计算成本。由于[边界积分算子](@entry_id:173789)的**非局部性（non-local）**——即边界上每一点都与所有其他点相互作用——离散化后得到的矩阵 $A$ 是一个**稠密（dense）**矩阵。对于一个有 $N$ 个自由度的问题 [@problem_id:2560743]：
- **矩阵组装**：需要计算 $N \times N$ 个[矩阵元](@entry_id:186505)，时间复杂度为 $\mathcal{O}(N^2)$。
- **内存消耗**：需要存储整个稠密矩阵，[空间复杂度](@entry_id:136795)为 $\mathcal{O}(N^2)$。
- **求解**：
    - 使用直接法（如高斯消元），[时间复杂度](@entry_id:145062)为 $\mathcal{O}(N^3)$。
    - 使用迭代法（如 GMRES），每次迭代需要一次矩阵-向量乘法，其时间复杂度为 $\mathcal{O}(N^2)$。

这些二次或三次的复杂度使得传统 BEM 在处理大规模问题（例如 $N > 10^5$）时变得不切实际。这催生了**快速[边界元法](@entry_id:141290)（Fast BEM）**的发展，如**[快速多极子方法](@entry_id:140932)（Fast Multipole Method, FMM）**和**[分层矩阵](@entry_id:750110)（Hierarchical Matrices, $\mathcal{H}$-Matrices）**技术。这些先进算法通过对远场相互作用进行近似，避免了显式地存储和计算整个稠密矩阵，能够将矩阵-向量乘法的复杂度降低到近线性的 $\mathcal{O}(N \log^p N)$ 甚至 $\mathcal{O}(N)$，从而使得用 BEM 求解数百万乃至数亿自由度的问题成为可能。这标志着[边界元法](@entry_id:141290)从一个理论工具向大规模科学与工程计算的强大引擎的转变。