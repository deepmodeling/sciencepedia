## 引言
[黎曼曲率张量](@entry_id:160189)是[微分几何](@entry_id:145818)的基石，是理解弯曲空间内在几何结构的核心工具。它精确地量化了一个黎曼流形在局部上如何偏离平坦的欧氏空间，从而捕捉了“曲率”这一直观概念的数学本质。然而，这一（1,3）-型张量的复杂性也带来了挑战：如何系统地理解其结构、对称性以及其在不同领域的深刻含义？这正是本文旨在解决的核心问题。

本文将引导读者全面掌握黎曼曲率张量的理论与应用。在第一章**“原理与机制”**中，我们将从其最根本的定义出发，推导其坐标表达式，并系统地揭示其赖以成立的代数和[微分](@entry_id:158718)对称性，例如著名的Bianchi恒等式。接着，在第二章**“应用与交叉学科联系”**中，我们将展示这些理论原理如何应用于刻画具体的几何空间（如球面和[双曲空间](@entry_id:268092)）、如何通过[Ricci分解](@entry_id:161263)揭示其物理意义，以及它如何在广义相对论、[几何分析](@entry_id:157700)等前沿领域中扮演关键角色。最后，在第三章**“动手实践”**中，我们提供了精选的练习题，旨在通过计算和证明，巩固读者对曲率[张量对称性](@entry_id:191651)和应用的理解。通过这一结构化的学习路径，读者将建立起对[黎曼曲率张量](@entry_id:160189)一个既严谨又直观的认识。

## 原理与机制

继引言之后，本章深入探讨黎曼曲率张量的核心原理与内在机制。我们将从其内在定义出发，推导其坐标表达式，并揭示其与度量张量之间的深刻联系。随后，我们将系统地阐述黎曼张量所满足的代数对称性，这些对称性不仅约束了其分量的形式，还赋予了它丰富的[代数结构](@entry_id:137052)。最后，我们将探讨[曲率张量](@entry_id:181383)的[微分性质](@entry_id:275298)，特别是第二 Bianchi 恒等式，以及它在刻画[局部对称空间](@entry_id:637873)等重要几何结构中的关键作用。我们还将讨论一些重要的约定和推广，以期为读者提供一个全面而严谨的理论框架。

### 从曲率的内在定义到坐标表示

[黎曼曲率张量](@entry_id:160189) $R$ 最根本的定义源于对协变导数不可交换性的度量。对于光滑流形 $(M, g)$ 上的任意光滑向量场 $X, Y, Z$，[曲率张量](@entry_id:181383) $R(X,Y)Z$ 定义为：
$$
R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z
$$
其中 $\nabla$ 是 Levi-Civita 联络，$[X,Y]$ 是向量场的 Lie 括号。这个定义是“内在的”，因为它不依赖于任何特定的[坐标系](@entry_id:156346)。

为了理解[曲率张量](@entry_id:181383)的具体计算，我们通常需要其在[局部坐标系](@entry_id:751394)中的表达式。设 $(x^1, \dots, x^n)$ 是一个[局部坐标](@entry_id:181200)卡，其对应的[坐标基](@entry_id:270149)向量场为 $\partial_i = \frac{\partial}{\partial x^i}$。在这一基底下，Levi-Civita 联络由 Christoffel 符号 $\Gamma^k_{ij}$ 描述，其定义为 $\nabla_{\partial_i} \partial_j = \Gamma^k_{ij} \partial_k$。

我们可以通过将[基向量](@entry_id:199546)场代入曲率的内在定义来推导其分量 $R^l{}_{ijk}$。令 $X = \partial_i, Y = \partial_j, Z = \partial_k$。[坐标基](@entry_id:270149)向量场的一个关键性质是它们的 [Lie 括号](@entry_id:636461)为零，即 $[\partial_i, \partial_j] = 0$。这使得定义简化为：
$$
R(\partial_i, \partial_j)\partial_k = \nabla_{\partial_i} \nabla_{\partial_j} \partial_k - \nabla_{\partial_j} \nabla_{\partial_i} \partial_k
$$
根据 $R(\partial_i, \partial_j)\partial_k = R^l{}_{ijk} \partial_l$ 的定义，我们需要计算右侧表达式中 $\partial_l$ 的系数。我们首先计算第一项 $\nabla_{\partial_i} \nabla_{\partial_j} \partial_k$：
$$
\begin{align}
\nabla_{\partial_i} (\nabla_{\partial_j} \partial_k)  &= \nabla_{\partial_i} (\Gamma^m_{jk} \partial_m) \\
 &= (\partial_i \Gamma^m_{jk}) \partial_m + \Gamma^m_{jk} (\nabla_{\partial_i} \partial_m) \\
 &= (\partial_i \Gamma^m_{jk}) \partial_m + \Gamma^m_{jk} \Gamma^l_{im} \partial_l
\end{align}
$$
为了将所有项都表示为 $\partial_l$ 的系数，我们重命名[哑指标](@entry_id:188070)。第一项中的 $m$ 可重命名为 $l$，第二项中的 $m$ 可重命名为 $p$，得到：
$$
\nabla_{\partial_i} (\nabla_{\partial_j} \partial_k) = (\partial_i \Gamma^l_{jk} + \Gamma^p_{jk} \Gamma^l_{ip}) \partial_l
$$
通过交换 $i$ 和 $j$，我们可以类似地得到第二项的表达式：
$$
\nabla_{\partial_j} (\nabla_{\partial_i} \partial_k) = (\partial_j \Gamma^l_{ik} + \Gamma^p_{ik} \Gamma^l_{jp}) \partial_l
$$
将两者相减，我们便得到了 $R^l{}_{ijk}$ 的坐标表达式：
$$
R^l{}_{ijk} = \partial_i \Gamma^l_{jk} - \partial_j \Gamma^l_{ik} + \Gamma^l_{ip} \Gamma^p_{jk} - \Gamma^l_{jp} \Gamma^p_{ik}
$$

一个至关重要的问题是：为什么这个由[非张量对象](@entry_id:201374) Christoffel 符号及其导数构成的组合，其本身是一个张量？ Christoffel 符号在坐标变换下表现出一种非齐次的、仿射的变换法则，这使它不是一个张量。然而，[黎曼曲率张量](@entry_id:160189)的内在定义 $R(X,Y)Z$ 保证了其对于 $X, Y, Z$ 的输入是 $\mathcal{C}^\infty(M)$-线性的，这正是张量的定义。例如，对于任意光滑函数 $f$，可以验证 $R(fX, Y)Z = f R(X,Y)Z$。这一性质确保了 $R$ 是一个 $(1,3)$-型张量。因此，其分量 $R^l{}_{ijk}$ 必然遵循 $(1,3)$-型张量的坐标变换法则。上述坐标表达式的巧妙之处在于，当进行坐标变换时，$\Gamma^l_{jk}$ 变换法则中的所有非齐次项（即涉及[坐标变换](@entry_id:172727)[二阶导数](@entry_id:144508)的项）在这个特定的组合中精确地相互抵消，最终只留下齐次的[张量变换](@entry_id:183453)项。[@problem_id:3002447]

### 曲率张量与度量

我们已经看到[曲率张量](@entry_id:181383)是由 Levi-Civita 联络及其[一阶导数](@entry_id:749425)决定的。而 Levi-Civita 联络本身是由度量张量 $g$ 唯一决定的。具体来说，其 Christoffel 符号可以通过度量张量的分量 $g_{ij}$ 及其一阶偏导数明确计算得出：
$$
\Gamma^k_{ij} = \frac{1}{2} g^{kl} \left( \frac{\partial g_{jl}}{\partial x^i} + \frac{\partial g_{il}}{\partial x^j} - \frac{\partial g_{ij}}{\partial x^l} \right)
$$
这个公式的唯一性源于 Levi-Civita 联络的两个基本特性：无挠性（torsion-free）和[度量兼容性](@entry_id:265910)（metric-compatible）。

将这个结果与上一节得到的 $R^l{}_{ijk}$ 的坐标表达式相结合，我们可以得出一个核心结论：**[黎曼曲率张量](@entry_id:160189)在任何一点的数值完全由度量张量 $g$ 在该点的数值及其一阶和[二阶偏导数](@entry_id:635213)唯一确定。**[@problem_id:3002442] 具体来说，$R^l{}_{ijk}$ 表达式中的 $\Gamma \Gamma$ 项依赖于 $g$ 的[一阶导数](@entry_id:749425)的乘积，而 $\partial \Gamma$ 项则依赖于 $g$ 的[二阶导数](@entry_id:144508)。

这一结论揭示了曲率的几何本质。它是一个内蕴于度量结构的量。我们可以通过选取一种特殊的[坐标系](@entry_id:156346)——黎曼[法坐标](@entry_id:143194)系（或称正规[坐标系](@entry_id:156346)），来更清晰地看到这一点。在一个点 $p$ 的邻域内建立[法坐标](@entry_id:143194)系，在该点 $p$ 处，度量张量的所有一阶导数均为零，且 Christoffel 符号也为零，即 $\Gamma^k_{ij}(p) = 0$。在这种特殊情况下，$R^l{}_{ijk}$ 的表达式在点 $p$ 简化为：
$$
R^l{}_{ijk}(p) = \partial_i \Gamma^l_{jk}(p) - \partial_j \Gamma^l_{ik}(p)
$$
这清楚地表明，即使联络本身在某点为零，曲率（作为联络的[一阶导数](@entry_id:749425)）通常不为零。曲率正是度量结构在二阶水平上偏离平直欧氏空间的度量。如果曲率也为零，那么[流形](@entry_id:153038)在局部上就是平直的。

### [曲率张量](@entry_id:181383)的代数对称性

为了更深入地研究曲率的结构，我们通常将其指标降低，定义一个 $(0,4)$-型的[协变张量](@entry_id:634493)，记作 $R_{ijkl}$：
$$
R_{ijkl} = g_{lm} R^m{}_{ijk} = g(R(\partial_i, \partial_j)\partial_k, \partial_l)
$$
这个形式的曲率张量展现出一套优雅而强大的代数对称性，这些对称性源于 Levi-Civita 联络的无挠性和[度量兼容性](@entry_id:265910)。

1.  **前两个指标反对称（Antisymmetry in the first pair）**:
    $$
    R_{ijkl} = -R_{jikl}
    $$
    这直接源于 $R(X,Y)Z = -R(Y,X)Z$。

2.  **后两个指标反对称（Antisymmetry in the last pair）**:
    $$
    R_{ijkl} = -R_{ijlk}
    $$
    此性质是[度量兼容性](@entry_id:265910) ($\nabla g = 0$) 的直接推论。

3.  **块[交换对称性](@entry_id:151892)（Pair interchange symmetry）**:
    $$
    R_{ijkl} = R_{klij}
    $$
    这个性质将前后两对指标联系起来，表明交换这两对指标时张量的值不变。

4.  **[第一 Bianchi 恒等式](@entry_id:200081)（First Bianchi Identity）**:
    $$
    R_{ijkl} + R_{iklj} + R_{iljk} = 0
    $$
    这个恒等式是对最后三个指标进行循环求和。它源于 Levi-Civita 联络的无挠性以及向量场 [Lie 括号](@entry_id:636461)所满足的 Jacobi 恒等式。

值得注意的是，[第一 Bianchi 恒等式](@entry_id:200081)的循环和形式与对最后三指标进行完全反对称化 $R_{i[jkl]}$ 密切相关。反对称化的定义为：
$$
T_{i[jkl]} = \frac{1}{3!}\sum_{\sigma\in S_3} \mathrm{sgn}(\sigma) T_{i\sigma(j)\sigma(k)\sigma(l)}
$$
展开后，我们发现 $6 R_{i[jkl]} = (R_{ijkl} + R_{iklj} + R_{iljk}) - (R_{ijlk} + R_{ikjl} + R_{ilkj})$。利用后两指标的[反对称性](@entry_id:261893)（$R_{ijlk} = -R_{ijkl}$ 等），上式可以简化为 $6 R_{i[jkl]} = 2 (R_{ijkl} + R_{iklj} + R_{iljk})$。因此，对于任何满足后两指标[反对称性](@entry_id:261893)的张量，条件 $R_{i[jkl]}=0$ 与循环和 $R_{ijkl}+R_{iklj}+R_{iljk}=0$ 是等价的。[@problem_id:3002439]

### 曲率的[代数结构](@entry_id:137052)

黎曼曲率张量的代数对称性极大地限制了其独立分量的数量，并揭示了其深刻的[代数结构](@entry_id:137052)。

首先，前两个和后两个指标的[反对称性](@entry_id:261893)（$R_{ijkl} = -R_{jikl}$ 和 $R_{ijkl} = -R_{ijlk}$）意味着 $R$ 可以被看作是作用于 [2-形式](@entry_id:188008)空间 $\Lambda^2 T_p M$ 的一个[双线性形式](@entry_id:746794)。我们可以定义一个映射 $B_R: \Lambda^2 T_p M \times \Lambda^2 T_p M \to \mathbb{R}$，对于简单的 2-形式 $u \wedge v$ 和 $w \wedge z$，其定义为：
$$
B_R(u \wedge v, w \wedge z) := R(u,v,w,z)
$$
这个定义是良性的，因为它尊重了[外积](@entry_id:147029)的[反对称性](@entry_id:261893)。

接下来，块[交换对称性](@entry_id:151892) $R_{ijkl} = R_{klij}$ 翻译到这个[双线性形式](@entry_id:746794)上，即 $B_R(u \wedge v, w \wedge z) = B_R(w \wedge z, u \wedge v)$。这表明 $B_R$ 是一个**对称**双线性形式。

因此，$(0,4)$-型黎曼曲率张量本质上是在每一点 $p$ 的 [2-形式](@entry_id:188008)空间 $\Lambda^2 T_p M$ 上的一个[对称双线性形式](@entry_id:148281)。从代数上看，这意味着 $R$ 可以被视为 $S^2((\Lambda^2 T_p M)^*)$ 的一个元素，其中 $V^*$ 表示对偶空间，$S^2$ 表示二阶[对称张量](@entry_id:148092)积。通过自然同构，这等价于 $R \in S^2(\Lambda^2 T_p^* M)$。[@problem_id:3002445]

基于此，我们可以定义**[曲率算子](@entry_id:198006)** $\mathcal{R}: \Lambda^2 T_p M \to \Lambda^2 T_p M$，它是一个[自伴算子](@entry_id:152188)，由下式定义：
$$
\langle \mathcal{R}(u \wedge v), x \wedge y \rangle = R(u,v,x,y)
$$
其中 $\langle \cdot, \cdot \rangle$ 是由度量 $g$ 在 $\Lambda^2 T_p M$ 上诱导的[内积](@entry_id:158127)。

所有这些对称性（包括[第一 Bianchi 恒等式](@entry_id:200081)）合在一起，严格地限制了在 $n$ 维空间中一个代数曲率张量（即满足所有这些对称性的张量）的独立分量数。通过详细的代数计算，可以证明这个空间的维数是：
$$
\dim \mathcal{A} = \frac{n^2(n^2-1)}{12}
$$
其中 $\mathcal{A}$ 代表所有代数曲率张量构成的空间。例如，在二维情况下（$n=2$），维数为 1，对应于高斯曲率。在三维情况下（$n=3$），维数为 6。在四维情况下（$n=4$），维数为 20。[@problem_id:3002435]

### Ricci 分解

在维度 $n \ge 4$ 时，代数曲率张量的空间 $\mathcal{R}$ 在[正交群](@entry_id:152531) $O(n)$ 的作用下可以进一步分解为三个不可约的[子表示](@entry_id:141094)，这被称为 **Ricci 分解**。这个分解将[曲率张量](@entry_id:181383)分为与[标量曲率](@entry_id:157547)、无迹 Ricci 曲率和 Weyl 曲率相关的三个部分。

首先，我们通过对黎曼张量进行迹运算来定义 **Ricci 张量** $\operatorname{Ric}$ 和 **标量曲率** $s$：
$$
\operatorname{Ric}_{jl} = g^{ik}R_{ijkl}, \quad s = g^{jl}\operatorname{Ric}_{jl}
$$
Ricci 张量是一个对称的 $(0,2)$-型张量。我们可以从中分离出无迹部分，定义**无迹 Ricci 张量** $S$：
$$
S = \operatorname{Ric} - \frac{s}{n} g
$$
Ricci 分解指出，任何代数曲率张量 $R$ 都可以唯一地、正交地分解为：
$$
R = W + \frac{1}{n-2} S \owedge g + \frac{s}{2n(n-1)} g \owedge g
$$
这里的 $\owedge$ 是 **[Kulkarni-Nomizu 积](@entry_id:204232)**，它由两个对称 $(0,2)$-型张量 $A,B$ 生成一个代数曲率张量：
$$
(A \owedge B)_{ijkl} = A_{ik}B_{jl} + A_{jl}B_{ik} - A_{il}B_{jk} - A_{jk}B_{il}
$$
分解中的三个部分各自具有明确的几何意义：
1.  **标量部分**: $\frac{s}{2n(n-1)} g \owedge g$ 完全由[标量曲率](@entry_id:157547) $s$ 决定，捕捉了体积变化的趋势。它构成了 $\mathcal{R}$ 中一个 1 维的[子空间](@entry_id:150286)。
2.  **无迹 Ricci 部分**: $\frac{1}{n-2} S \owedge g$ 完全由无迹 Ricci 张量 $S$ 决定。它构成的[子空间](@entry_id:150286)维数为 $\frac{n(n+1)}{2}-1$。
3.  **Weyl 部分**: $W$ 是 **Weyl 张量**，其定义为 $R$ 减去另外两个部分。它的一个关键特性是“完全无迹”，即其任何形式的迹（特别是 Ricci 张量）都为零。Weyl 张量度量了[流形](@entry_id:153038)在保持体积不变的情况下的形状畸变，与[共形几何](@entry_id:186351)密切相关。其构成的[子空间](@entry_id:150286)维数为 $\frac{n(n+1)(n+2)(n-3)}{12}$。

这个分解在广义相对论和[共形几何](@entry_id:186351)中至关重要，因为它将复杂的曲率张量分解为具有不同几何和物理含义的独立部分。[@problem_id:3036586]

### 曲率条件及其谱性质

曲率的正负性对[流形的拓扑](@entry_id:267834)和几何有着深刻的影响。这些性质通常通过[曲率算子](@entry_id:198006) $\mathcal{R}$ 的谱（即[特征值](@entry_id:154894)）来表述。

最经典的曲率概念是**截面曲率** $K(\sigma)$，它度量了沿二维平面 $\sigma$ 的弯曲程度。对于由标准正交基 $\{u,v\}$ 张成的平面 $\sigma$，[截面曲率](@entry_id:159738)由下式给出：
$$
K(\sigma) = R(u,v,v,u) = \langle \mathcal{R}(u \wedge v), u \wedge v \rangle
$$
[流形](@entry_id:153038)被称为具有**[正截面曲率](@entry_id:193532)**，如果对所有二维平面 $\sigma$ 都有 $K(\sigma)>0$。这等价于说，[曲率算子](@entry_id:198006) $\mathcal{R}$ 在所有可分解的单位 [2-形式](@entry_id:188008)（形如 $u \wedge v$）上的二次型取正值。然而，当维数 $n \ge 4$ 时，[2-形式](@entry_id:188008)空间 $\Lambda^2 T_p M$ 中存在不可分解的 2-形式（例如 $e_1 \wedge e_2 + e_3 \wedge e_4$）。因此，[正截面曲率](@entry_id:193532)并不意味着[曲率算子](@entry_id:198006) $\mathcal{R}$ 是正定的。事实上，存在具有严格[正截面曲率](@entry_id:193532)的[流形](@entry_id:153038)（如[复射影空间](@entry_id:268402) $\mathbb{CP}^k, k \ge 2$），其[曲率算子](@entry_id:198006)却有负[特征值](@entry_id:154894)。[@problem_id:3036579]

为了捕捉更强的曲率性质，引入了其他概念：
- **2-正[曲率算子](@entry_id:198006) (2-positive curvature operator)**: 指[曲率算子](@entry_id:198006) $\mathcal{R}$ 的最小两个[特征值](@entry_id:154894)之和为正，即 $\lambda_1 + \lambda_2 > 0$。这个条件直接蕴含了 $\lambda_2 > 0$，因此除了可能的一个负[特征值](@entry_id:154894)外，其余所有[特征值](@entry_id:154894)都为正。这是一个比[正截面曲率](@entry_id:193532)更强的条件。[@problem_id:3036579]
- **正迷向曲率 (Positive isotropic curvature, PIC)**: 这个条件要求对于任意标准正交 4-标架 $\{e_1, e_2, e_3, e_4\}$，都有 $R_{1313} + R_{1414} + R_{2323} + R_{2424} - 2 R_{1234} > 0$。这等价于对所有形如 $\omega = (e_1 + i e_2) \wedge (e_3 + i e_4)$ 的复迷向 2-形式，Hermitian 二次型 $\langle \mathcal{R}\omega, \overline{\omega} \rangle$ 为正。同样，PIC 也不足以保证[曲率算子](@entry_id:198006)是正定的。[@problem_id:3036579]

这些不同的曲率条件构成了[比较几何](@entry_id:180578)中的一个层次结构，为研究[流形](@entry_id:153038)拓扑提供了强大的工具。

### [微分](@entry_id:158718) Bianchi 恒等式与[局部对称空间](@entry_id:637873)

除了代数对称性，黎曼曲率张量还满足一个关键的[微分](@entry_id:158718)恒等式，称为**第二 Bianchi 恒等式**：
$$
(\nabla_X R)(Y,Z) + (\nabla_Y R)(Z,X) + (\nabla_Z R)(X,Y) = 0
$$
或者用[指标形式](@entry_id:183467)写作：
$$
\nabla_k R_{ijlm} + \nabla_i R_{jklm} + \nabla_j R_{kilm} = 0
$$
这里，指标 $i,j,k$ 进行了循环求和。这个恒等式直接从曲率的内在定义和 Lie 括号的 Jacobi 恒等式推导而来，它对任何联络都成立（当存在挠率时会包含挠率项）。

第二 Bianchi 恒等式的一个深刻几何应用是刻画**[局部对称空间](@entry_id:637873)**。一个黎曼流形被称为[局部对称空间](@entry_id:637873)，如果其曲率张量是平行的，即 $\nabla R = 0$。这意味着曲率在沿任何方向的平行移动下都保持不变。

可以证明，一个黎曼流形是局部对称的，当且仅当 $\nabla R = 0$。这个等价性分为两个方向的证明：
1.  **局部对称 $\implies \nabla R = 0$**: 若[流形](@entry_id:153038)是局部对称的，则每一点 $p$ 都存在一个[局部等距](@entry_id:158618)同构 $s_p$（测地对称），它固定 $p$ 并且其在 $p$ 点的[微分](@entry_id:158718)为 $-\mathrm{Id}$。由于[等距同构](@entry_id:273188)保持曲率张量及其协变导数，我们有 $s_p^*(\nabla R) = \nabla R$。另一方面，在点 $p$，$s_p^*$ 的作用会给 $(0,5)$-型张量 $\nabla R$ 带来一个 $(-1)^5 = -1$ 的因子。因此，在点 $p$ 处必然有 $(\nabla R)_p = -(\nabla R)_p$，这迫使 $(\nabla R)_p = 0$。由于 $p$ 是任意的，所以 $\nabla R = 0$。[@problem_id:3036571]
2.  **$\nabla R = 0 \implies$ 局部对称**: 如果 $\nabla R = 0$，这意味着[曲率张量](@entry_id:181383)在平行移动下不变。根据 Cartan-Ambrose-Hicks 定理，这个条件足以保证在每一点 $p$ 都能构造出一个具有期望性质的[局部等距](@entry_id:158618)同构 $s_p$，从而证明[流形](@entry_id:153038)是局部对称的。[@problem_id:3036571]

### 重要约定与推广

在学习和应用黎曼几何时，有必要了解一些常见的约定差异以及如何将理论推广到更一般的情形。

#### 符号约定

黎曼曲率张量的定义存在两种主流的符号约定。我们在本章中采用的定义是：
$$
R^{(+)}(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]} Z
$$
另一种常见的约定是取其[相反数](@entry_id:151709)：
$$
R^{(-)}(X,Y)Z = -R^{(+)}(X,Y)Z = \nabla_Y \nabla_X Z - \nabla_X \nabla_Y Z + \nabla_{[X,Y]} Z
$$
这个符号上的差异会影响到一系列相关的几何量。具体来说，从 $(+)$-约定切换到 $(-)$-约定时：
- $(1,3)$-型张量 $R(X,Y)Z$ 和 $(0,4)$-型张量 $R(X,Y,Z,W)$ 都反号。
- 截面曲率 $K(\sigma)$ 反号。
- Ricci 张量 $\operatorname{Ric}$ 和标量曲率 $s$ 都反号。
- Weyl 张量 $W$ 也反号。

然而，重要的是，[黎曼张量](@entry_id:160847)的所有**代数对称性**（如 $R_{ijkl} = -R_{jikl}$ 和 $R_{ijkl} = R_{klij}$）以及**[微分](@entry_id:158718) Bianchi 恒等式**（第一和第二）都保持形式不变。这是因为这些恒等式都是关于 $R$ 的[齐次线性方程](@entry_id:153751)，当 $R$ 变为 $-R$ 时，方程 $-P(R)=0$ 与 $P(R)=0$ 是等价的。[@problem_id:3036576] 因此，例如，球面在一种约定下有正的截面曲率，在另一种约定下则有负的截面曲率，但这只是一个约定的问题，其内在几何性质并未改变。

#### 带挠联络

本章始终假设联络是 Levi-Civita 联络，特别是[无挠的](@entry_id:161664)（torsion-free）。如果联络 $\nabla$ 具有非零的[挠率张量](@entry_id:204137) $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$，那么曲率张量和 Bianchi 恒等式的形式会发生改变。

例如，在一个具有常数挠率的 [Lie 群](@entry_id:137659)上，我们可以定义一个联络 $\nabla_{e_i}e_j = 0$。此时，[曲率张量](@entry_id:181383) $R$ 可能为零，而挠率 $T$ 非零。在这种情况下，[第一 Bianchi 恒等式](@entry_id:200081)不再是简单的循环和为零，而是包含挠率项的更复杂形式。具体来说，一般的[第一 Bianchi 恒等式](@entry_id:200081)为：
$$
\sum_{\text{cyc}(X,Y,Z)} \left( R(X,Y)Z - T(T(X,Y),Z) - (\nabla_X T)(Y,Z) \right) = 0
$$
当 $T=0$ 时，该恒等式就退化为我们熟悉的形式 $\sum_{\text{cyc}} R(X,Y)Z = 0$。研究带挠联络的情形对于理解[自旋几何](@entry_id:181531)、[超引力](@entry_id:148689)理论等领域至关重要。[@problem_id:3002429]