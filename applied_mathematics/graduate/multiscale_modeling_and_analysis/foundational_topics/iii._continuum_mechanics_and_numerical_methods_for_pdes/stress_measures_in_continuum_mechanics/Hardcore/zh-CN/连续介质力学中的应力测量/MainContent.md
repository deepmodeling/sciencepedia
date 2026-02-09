## 引言
在连续介质力学中，应力是描述和量化物体内部相互作用力的基本概念。当物体受到外力作用或发生非均匀变形时，其内部会产生抵抗形变的内力。然而，随着物体从初始的参考构型运动到当前的变形构型，单一的应力定义变得捉襟见肘。例如，描述材料固有属性的本构关系通常在参考构型中建立更为自然，而描述力学平衡的方程则必须在当前构型中书写。这一理论上的需求催生了多种相互关联但应用场景各异的应力度量体系。

本文旨在系统地梳理这些关键的应力度量。读者将学习到不同应力张量（如柯西应力、第一和第二皮奥拉-基尔霍夫应力）的精确定义、它们之间的数学转换关系，以及选择特定度量的物理依据。我们将首先在“原理与机制”一章中，奠定这些概念的理论基础，包括变形运动学、能量共轭以及至关重要的客观性原理。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何在工程力学、材料科学、生物力学乃至多尺度建模等前沿领域中解决实际问题。最后，“动手实践”部分将提供具体的计算练习，以巩固和深化读者对这些抽象概念的理解。

## 原理与机制

在连续介质力学中，应力是描述物体内部各部分之间相互作用力的核心概念。当一个物体受到外部载荷或经历非均匀变形时，其内部会产生力，以抵抗形状和体积的改变。为了将这一物理直觉转化为严谨的数学框架，我们需要建立能够量化这些内力的场量。然而，由于物体在变形过程中会改变其几何构型，单一的应力定义不足以应对所有情况。例如，在材料本构关系的研究中，我们通常希望在材料的初始、未变形构型中描述其行为；而在求解平衡方程时，则必须在物体当前的、已变形的构型中进行。因此，连续介质力学发展了一套不同但相互关联的应力张量体系，每一种都有其特定的物理意义和应用领域。本章将系统地阐述这些关键应力度量的基本原理、它们之间的数学联系，以及在不同力学框架下（如能量共轭和客观性原理）使用它们的理论必要性。

### 应力的基本概念：柯西应力张量

我们分析的出发点是**柯西应力原理**。想象在变形后的物体内部任意取一点 $\mathbf{x}$，并通过该点做一个假想的切割面。这个面的方向可以用其单位法向量 $\mathbf{n}$ 来描述。根据牛顿第三定律，切面一侧的材料会对另一侧的材料施加一个分布力。在点 $\mathbf{x}$ 处，这个分布力的密度被称为**牵引力矢量** (traction vector)，记为 $\mathbf{t}(\mathbf{x}, \mathbf{n})$。它的单位是力每单位面积。

柯西假设，对于一个给定的点 $\mathbf{x}$，牵引力矢量 $\mathbf{t}$ 仅依赖于该点的局部状态和切面的法向 $\mathbf{n}$，而与切面的具体形状或曲率无关。这是一个极其深刻的局部化假设。更有力的是，通过考虑一个以点 $\mathbf{x}$ 为顶点的无限小四面体上的线性动量平衡（柯西四面体论证），可以证明牵引力 $\mathbf{t}$ 与法向量 $\mathbf{n}$ 之间存在线性关系。[@problem_id:3810217]

这个线性关系是连续介质力学的一块基石，它保证了存在一个二阶张量场 $\boldsymbol{\sigma}(\mathbf{x}, t)$，使得对于任意单位法向量 $\mathbf{n}$，牵引力矢量都可以通过该张量与法向量的乘积得到。这个张量就是**柯西应力张量** (Cauchy stress tensor)，也称为真实应力张量。

$$ \mathbf{t}(\mathbf{x}, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x}, t) \mathbf{n} $$

这个关系被称为**柯西应力定理**。柯西应力张量 $\boldsymbol{\sigma}$ 是一个定义在当前构型（即变形后的构型）上的物理量。它的分量 $\sigma_{ij}$ 代表了作用在法向为第 $j$ 个坐标轴方向的微小面元上、沿第 $i$ 个坐标轴方向的力分量。值得注意的是，柯西应力描述的是通过表面的接触力，它与作用于整个体积的**体力** (body force) $\mathbf{b}$（如重力）是截然不同的概念。体力直接进入动量平衡方程的体积积分项，而柯西应力则通过其散度（在应用高斯散度定理后）贡献于平衡方程。[@problem_id:3810196]

对于经典（非极性）连续介质，角动量守恒定律进一步要求柯西应力张量必须是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathrm{T}}$。这意味着描述一个点的应力状态只需要六个独立分量，而不是九个。

### 变形运动学：连接构型的桥梁

为了定义与材料初始状态相关的应力，我们必须首先建立描述变形的数学语言。一个连续体在运动过程中会占据一系列空间区域。我们选择一个特定的时刻（通常是初始时刻 $t=0$）的构型作为**参考构型**（或物质构型），并用物质坐标 $\mathbf{X}$ 来标记材料点。在任意时刻 $t$，物体占据**当前构型**（或空间构型），该材料点的空间位置由空间坐标 $\mathbf{x}$ 给出。运动可以描述为一个映射 $\mathbf{x} = \boldsymbol{\varphi}(\mathbf{X}, t)$。

**变形梯度张量** (deformation gradient tensor) $\mathbf{F}$ 是描述局部变形的核心工具，它定义为空间坐标对物质坐标的梯度：

$$ \mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \nabla_{\mathbf{X}} \boldsymbol{\varphi} $$

$\mathbf{F}$ 将参考构型中的一个无限小线元 $d\mathbf{X}$ 映射到当前构型中的对应线元 $d\mathbf{x}$，即 $d\mathbf{x} = \mathbf{F} d\mathbf{X}$。

变形的局部体积变化由 $\mathbf{F}$ 的行列式，即**雅可比行列式** (Jacobian) $J$ 描述：

$$ J = \det(\mathbf{F}) $$

物理上，物质不可穿透，因此我们要求 $J > 0$。$J$ 给出了局部体积的变化率，即当前构型中的一个无限小体积元 $dv$ 与其在参考构型中的原像 $dV$ 之间的关系是 $dv = J dV$。对于不可压缩材料，任何变形都必须保持体积不变，因此 $J=1$。[@problem_id:3810193]

同样，面元在变形过程中也会发生变化。参考构型中一个有向面元 $d\mathbf{A} = \mathbf{N} dA$（其中 $\mathbf{N}$ 是单位法向量，$dA$ 是面积）与当前构型中对应的有向面元 $d\mathbf{a} = \mathbf{n} da$ 之间的关系由**南森公式** (Nanson's formula) 给出：

$$ \mathbf{n} da = J \mathbf{F}^{-\mathrm{T}} \mathbf{N} dA $$

其中 $\mathbf{F}^{-\mathrm{T}}$ 是 $\mathbf{F}$ 的逆转置。这个公式至关重要，因为它直接联系了两个构型中的力与面积，从而构成了定义其他应力度量的基础。南森公式本身可以从 $\mathbf{F}$ 的**余子式张量** (cofactor tensor) $\text{cof}(\mathbf{F})$ 导出，其关系为 $d\mathbf{a} = \text{cof}(\mathbf{F}) d\mathbf{A}$，并且 $\text{cof}(\mathbf{F}) = J \mathbf{F}^{-\mathrm{T}}$。[@problem_id:3810193]

### 替代应力度量：拉格朗日观点

柯西应力 $\boldsymbol{\sigma}$ 定义在当前构型上，非常适合用于空间描述的平衡方程。然而，在材料科学中，本构关系（即应力与应变的关系）通常是材料的固有属性，更自然的做法是在不随时间改变的参考构型中进行描述。这就催生了拉格朗日描述下的应力度量。

#### 第一皮奥拉-基尔霍夫应力张量 (P)

我们定义**名义牵引力** (nominal traction) $\mathbf{T}$ 为作用在变形体上的力除以其在**参考构型**中的初始面积 $dA$，即 $\mathbf{T} = d\mathbf{f} / dA$。而柯西牵引力是 $\mathbf{t} = d\mathbf{f} / da$。因此，力元是守恒的：$\mathbf{T} dA = \mathbf{t} da$。

结合柯西定理 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$ 和南森公式，我们得到：

$$ \mathbf{T} dA = (\boldsymbol{\sigma}\mathbf{n}) da = \boldsymbol{\sigma} (\mathbf{n} da) = \boldsymbol{\sigma} (J \mathbf{F}^{-\mathrm{T}} \mathbf{N} dA) $$

由于上式对任意 $\mathbf{N}$ 和 $dA$ 均成立，我们得到 $\mathbf{T} = (J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}}) \mathbf{N}$。这启发我们定义一个二阶张量 $\mathbf{P}$，使得 $\mathbf{T} = \mathbf{P} \mathbf{N}$。这个张量就是**第一皮奥拉-基尔霍夫应力张量** (First Piola-Kirchhoff stress tensor)，其定义为：

$$ \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}} $$

$\mathbf{P}$ 张量是一个**两点张量** (two-point tensor)，因为它将参考构型中的一个向量（法向量 $\mathbf{N}$）映射到当前构型中的一个向量（力 $\mathbf{T}$）。一个重要的特性是，即使柯西应力 $\boldsymbol{\sigma}$ 是对称的，$\mathbf{P}$ 通常也**不是对称的**。角动量守恒施加的约束是 $\mathbf{P}\mathbf{F}^{\mathrm{T}} = (\mathbf{P}\mathbf{F}^{\mathrm{T}})^{\mathrm{T}}$，但这并不意味着 $\mathbf{P}$ 本身是对称的。[@problem_id:3810204]

#### 第二皮奥拉-基尔霍夫应力张量 (S)

为了得到一个完全定义在参考构型上且对称的应力张量，我们对 $\mathbf{P}$ 进行一次“拉回”操作。定义**第二皮奥拉-基尔霍夫应力张量** (Second Piola-Kirchhoff stress tensor) $\mathbf{S}$，使得它通过变形梯度 $\mathbf{F}$ 与 $\mathbf{P}$ 相关联：

$$ \mathbf{P} = \mathbf{F} \mathbf{S} $$

将此定义与 $\mathbf{P}$ 和 $\boldsymbol{\sigma}$ 的关系式结合，我们得到 $\mathbf{S}$ 的直接转换公式：

$$ \mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = \mathbf{F}^{-1} (J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}}) = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}} $$

$\mathbf{S}$ 张量是一个纯粹的物质张量，因为它将参考构型中的向量映射到参考构型中的向量（尽管其物理意义源于当前构型中的力）。通过计算其转置可以证明，$\mathbf{S}$ 是对称的**当且仅当**柯西应力 $\boldsymbol{\sigma}$ 是对称的。[@problem_id:3810222] 这个对称性使得 $\mathbf{S}$ 成为固体力学本构建模中极为重要的一个量，特别是在超弹性理论中。

为了加深理解，我们来看一个具体的计算示例。假设一个材料点经历了变形，其变形梯度和柯西应力分别为：[@problem_id:3810213]
$$ \mathbf{F}=\begin{pmatrix} 2  & 0 & 0 \\ 0 & 1 & 1 \\ 0 & 0 & 1 \end{pmatrix}, \qquad \boldsymbol{\sigma}=\begin{pmatrix} 3 & 1 & 0 \\ 1 & 2 & -1 \\ 0 & -1 & 1 \end{pmatrix} $$
其中 $\boldsymbol{\sigma}$ 是对称的。

首先计算所需量：
$J = \det(\mathbf{F}) = 2$
$\mathbf{F}^{-1} = \begin{pmatrix} 1/2 & 0 & 0 \\ 0 & 1 & -1 \\ 0 & 0 & 1 \end{pmatrix}$
$\mathbf{F}^{-\mathrm{T}} = (\mathbf{F}^{-1})^{\mathrm{T}} = \begin{pmatrix} 1/2 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & -1 & 1 \end{pmatrix}$

根据定义，第一皮奥拉-基尔霍夫应力为：
$$ \mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}} = 2 \begin{pmatrix} 3 & 1 & 0 \\ 1 & 2 & -1 \\ 0 & -1 & 1 \end{pmatrix} \begin{pmatrix} 1/2 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & -1 & 1 \end{pmatrix} = 2 \begin{pmatrix} 3/2 & 1 & 0 \\ 1/2 & 3 & -1 \\ 0 & -2 & 1 \end{pmatrix} = \begin{pmatrix} 3 & 2 & 0 \\ 1 & 6 & -2 \\ 0 & -4 & 2 \end{pmatrix} $$
我们可以观察到 $\mathbf{P}$ 是非对称的，这在有限变形中是常见情况。

接下来，计算第二皮奥拉-基尔霍夫应力：
$$ \mathbf{S} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-\mathrm{T}} = \mathbf{F}^{-1} \mathbf{P} = \begin{pmatrix} 1/2 & 0 & 0 \\ 0 & 1 & -1 \\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 3 & 2 & 0 \\ 1 & 6 & -2 \\ 0 & -4 & 2 \end{pmatrix} = \begin{pmatrix} 3/2 & 1 & 0 \\ 1 & 10 & -4 \\ 0 & -4 & 2 \end{pmatrix} $$
通过检查，可以看到 $S_{12}=S_{21}=1$，$S_{13}=S_{31}=0$，$S_{23}=S_{32}=-4$。因此，计算出的 $\mathbf{S}$ 张量是对称的，这与理论预测（对称的 $\boldsymbol{\sigma}$ 导致对称的 $\mathbf{S}$）完全一致。

### 能量共轭与功率

选择何种应力度量的一个关键物理依据是**能量共轭** (energetic conjugacy) 原则。它要求应力功率（单位时间、单位体积内应力所做的功）必须能表示为某个应力度量与对应应变率度量的双点积形式。

单位**当前**体积的应力功（也称应力功率）为：
$w_v = \boldsymbol{\sigma} : \mathbf{d}$
其中 $\mathbf{d} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{\mathrm{T}})$ 是**变形率张量**，而 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$ 是空间速度梯度。由于 $\boldsymbol{\sigma}$ 是对称的，它与 $\mathbf{L}$ 的反对称部分（自旋张量 $\mathbf{W}$）的双点积为零。

单位**参考**体积的应力功等于 $w_V = J w_v = J (\boldsymbol{\sigma} : \mathbf{d})$。这启发了**基尔霍夫应力张量** (Kirchhoff stress tensor) $\boldsymbol{\tau}$ 的定义：
$\boldsymbol{\tau} = J\boldsymbol{\sigma}$
于是，参考体积的应力功可以简洁地写为 $w_V = \boldsymbol{\tau} : \mathbf{d}$。这表明 $(\boldsymbol{\tau}, \mathbf{d})$ 是一对能量共轭量。[@problem_id:3810174]

通过一系列张量运算，我们还可以将 $w_V$ 表示为其他形式，从而揭示更多的能量共轭对：
- $w_V = \mathbf{P} : \dot{\mathbf{F}}$。这表明第一皮奥拉-基尔霍夫应力 $\mathbf{P}$ 与变形梯度率 $\dot{\mathbf{F}}$ 共轭。[@problem_id:3810204]
- $w_V = \mathbf{S} : \dot{\mathbf{E}}$。其中 $\mathbf{E} = \frac{1}{2}(\mathbf{C} - \mathbf{I})$ 是**格林-拉格朗日应变张量** (Green-Lagrange strain tensor)，而 $\mathbf{C} = \mathbf{F}^{\mathrm{T}} \mathbf{F}$ 是**右柯西-格林变形张量** (Right Cauchy-Green deformation tensor)。这表明第二皮奥拉-基尔霍夫应力 $\mathbf{S}$ 与格林-拉格朗日应变率 $\dot{\mathbf{E}}$ 共轭。[@problem_id:3810223]

总结一下，我们有以下几对重要的能量共轭量：
- $(\boldsymbol{\sigma}, \mathbf{d})$：柯西应力与变形率（对应当前体积功率）
- $(\boldsymbol{\tau}, \mathbf{d})$：基尔霍夫应力与变形率（对应参考体积功率）
- $(\mathbf{P}, \dot{\mathbf{F}})$：第一PK应力与变形梯度率
- $(\mathbf{S}, \dot{\mathbf{E}})$：第二PK应力与格林-拉格朗日应变率

这些共轭关系是建立热力学一致的本构模型的基础。例如，在多尺度模型中，宏观和微观功率的等价性（Hill-Mandel条件）就依赖于这些共轭对的正确识别。[@problem_id:3810204]

### 本构模型中的客观性原理

一个物理上合理的本构关系（连接应力与应变的方程）必须满足**物质客观性原理** (principle of material objectivity)，或称**标架无关性** (frame-indifference)。这意味着材料的响应不应依赖于观察者。不同的观察者之间通过刚体运动（平移和旋转）相联系。

考虑一个叠加在当前运动之上的刚体旋转 $\mathbf{Q}(t)$。对于一个叠加了该旋转的观察者来说，测得的各个物理量（用星号表示）与原始观察者测得的量之间有如下关系：[@problem_id:3810206]
- 变形梯度: $\mathbf{F}^* = \mathbf{Q}\mathbf{F}$
- 右柯西-格林张量: $\mathbf{C}^* = (\mathbf{F}^*)^{\mathrm{T}} \mathbf{F}^* = \mathbf{F}^{\mathrm{T}} \mathbf{Q}^{\mathrm{T}} \mathbf{Q} \mathbf{F} = \mathbf{C}$
- 柯西应力: $\boldsymbol{\sigma}^* = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{\mathrm{T}}$
- 第一PK应力: $\mathbf{P}^* = \mathbf{Q}\mathbf{P}$
- 第二PK应力: $\mathbf{S}^* = (\mathbf{F}^*)^{-1} \mathbf{P}^* = (\mathbf{F}^{-1}\mathbf{Q}^{\mathrm{T}})(\mathbf{Q}\mathbf{P}) = \mathbf{F}^{-1}\mathbf{P} = \mathbf{S}$

这些变换规则揭示了一个深刻的结论：$\mathbf{C}$ 和 $\mathbf{S}$ 在刚体旋转下是**不变的**（客观的物质张量），而 $\boldsymbol{\sigma}$ 和 $\mathbf{P}$ 则随观察者旋转而改变（客观的空间张量或两点张量）。

这一结论对本构建模具有决定性影响：
- **超弹性模型 (Hyperelasticity)**：如果本构关系写作 $\mathbf{S} = \mathcal{G}(\mathbf{C})$，例如源于一个应变能密度函数 $\Psi(\mathbf{C})$ 的形式 $\mathbf{S} = 2 \frac{\partial \Psi}{\partial \mathbf{C}}$，那么这个本构关系**自动满足**客观性原理。因为在变换后的坐标系中，$\mathbf{S}^* = \mathbf{S}$ 和 $\mathbf{C}^* = \mathbf{C}$，所以本构方程 $\mathbf{S}^* = \mathcal{G}(\mathbf{C}^*)$ 自动成立。这是在参考构型中用 $(\mathbf{S}, \mathbf{C})$ 建立本构模型的巨大优势。然后，可以通过“推前”运算 $\boldsymbol{\sigma} = J^{-1} \mathbf{F} \mathbf{S} \mathbf{F}^{\mathrm{T}}$ 得到在当前构型中同样满足客观性的柯西应力。[@problem_id:3810206] [@problem_id:3810186]

- **弹塑性与率形式模型 (Hypoelasticity)**：在许多计算力学应用中，尤其是在塑性理论中，本构关系通常以率形式给出，直接关联应力率和变形率，例如 $\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C} : \mathbf{d}$。这里的问题在于，应该使用哪种“应力率” $\overset{\circ}{\boldsymbol{\sigma}}$？我们不能简单地使用柯西应力的物质时间导数 $\dot{\boldsymbol{\sigma}}$，因为可以证明 $\dot{\boldsymbol{\sigma}}$ 不是一个客观的张量率。在纯刚体旋转下（此时 $\mathbf{d}=\mathbf{0}$），$\dot{\boldsymbol{\sigma}}$ 并不为零，这意味着一个天真的本构律 $\dot{\boldsymbol{\sigma}} = \mathbb{C} : \mathbf{d}$ 会错误地预测在没有变形的情况下应力保持不变，而实际上应力张量的分量在空间固定坐标系中正在改变。

为了解决这个问题，必须使用一种**客观应力率**。这类应力率通过从物质导数中减去由刚体旋转引起的部分来构造。一个著名的例子是**Jaumann率** (Jaumann rate) 或余旋率 (corotational rate)：
$$ \overset{\triangle}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W} $$
其中 $\mathbf{W} = \frac{1}{2}(\mathbf{L} - \mathbf{L}^{\mathrm{T}})$ 是自旋张量。可以证明，在纯刚体旋转下，$\overset{\triangle}{\boldsymbol{\sigma}} = \mathbf{0}$。因此，一个客观的率形式本构律应写为 $\overset{\triangle}{\boldsymbol{\sigma}} = \mathbb{C} : \mathbf{d}$。这样，在纯刚体旋转（$\mathbf{d}=\mathbf{0}$）时，模型就能正确预测内在应力不发生改变。[@problem_id:3810199] [@problem_id:3810186]

### 基尔霍夫应力在本构模型中的应用

最后，我们回到基尔霍夫应力 $\boldsymbol{\tau} = J\boldsymbol{\sigma}$。除了其在功率表达式中的简洁性外，$\boldsymbol{\tau}$ 在处理近不可压缩材料时尤其有用。对于这类材料，通常将应变能函数 $\Psi$ 分解为体积部分 $\Psi_{\text{vol}}(J)$ 和等容部分 $\Psi_{\text{iso}}(\bar{\mathbf{F}})$，其中 $\bar{\mathbf{F}} = J^{-1/3}\mathbf{F}$ 是保持体积不变的变形梯度部分。

在这种分解下，可以证明基尔霍夫应力 $\boldsymbol{\tau}$ 也相应地分解为一个由体积变化引起的球形（静水压）部分和一个由形状变化引起的偏部分：
$$ \boldsymbol{\tau} = \boldsymbol{\tau}_{\text{iso}}(\bar{\mathbf{F}}) + p(J) \mathbf{I} $$
其中 $p(J) = J \frac{d\Psi_{\text{vol}}}{dJ}$ 是压力，$\mathbf{I}$ 是单位张量。这种加法分解的形式使得在数值计算中处理不可压缩性约束变得更加方便，是有限元分析中混合单元法等技术的理论基础。[@problem_id:3810174]

总之，从最基本的柯西应力出发，连续介质力学根据不同的理论和应用需求，构建了一系列相互关联的应力度量。第一和第二皮奥拉-基尔霍夫应力是拉格朗日描述和材料本构建模的核心。基尔霍夫应力则在能量分析和不可压缩材料模型中扮演重要角色。理解它们各自的定义、物理意义、相互关系以及在客观性原理下的变换特性，是进行高级非线性固体力学分析和计算的关键。