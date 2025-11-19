## 引言
在固体力学领域，理解物体如何在外力、温度变化或其他激励下发生变形，是进行工程设计与科学研究的基石。[位移矢量场](@entry_id:196067)是描述和量化这一变形过程的核心数学工具，它精确地追踪了物体内部每一个物质点的运动轨迹，从而构成了连接运动学与动力学的桥梁。然而，从宏观的位移到微观的应变与应力，其间涉及一系列深刻的物理与数学概念，包括如何区分真实变形与刚体运动，以及如何处理不同变形尺度下的复杂性。

本文旨在系统性地剖析[位移矢量场](@entry_id:196067)这一关键概念。在“原理与机制”一章中，我们将从其基本定义出发，深入探讨[位移梯度](@entry_id:165352)、应变张量和转动张量，并详细辨析小变形与[大变形](@entry_id:167243)运动学的区别与联系。接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示[位移场](@entry_id:141476)如何在[结构分析](@entry_id:153861)、[材料科学](@entry_id:152226)、断裂力学乃至计算方法等多个领域发挥关键作用，揭示其广泛的实践价值。最后，通过“动手实践”部分提供的具体问题，读者将有机会亲手应用所学知识，将抽象的理论转化为解决实际问题的能力。

## 原理与机制

在[连续介质力学](@entry_id:155125)中，理解物体的变形始于精确描述其各点的运动。**[位移矢量场](@entry_id:196067)**（Displacement Vector Field）是描述这种运动并连接[运动学](@entry_id:173318)与变形分析的核心工具。本章将从其基本定义出发，系统地阐述位移场的性质、其在推导应变和[平衡方程](@entry_id:172166)中的作用，以及在理论和计算分析中引出的重要概念。

### 位移场的[拉格朗日描述](@entry_id:264498)

为了追踪连续体中物质点的运动，我们首先需要一种标记这些点的方法。最自然的方式是在一个固定的、未变形的**参考构型**（Reference Configuration） $\mathcal{B}_0$ 中，用物[质点](@entry_id:186768)的位置矢量 $\boldsymbol{X}$ 来唯一标记它。物体的**运动**（Motion）则被描述为一个映射 $\boldsymbol{\chi}(\boldsymbol{X}, t)$，它给出了物[质点](@entry_id:186768) $\boldsymbol{X}$ 在时刻 $t$ 的**当前构型**（Current Configuration） $\mathcal{B}_t$ 中的空间位置 $\boldsymbol{x}$。因此，我们有关系式 $\boldsymbol{x} = \boldsymbol{\chi}(\boldsymbol{X}, t)$。

**[位移矢量](@entry_id:262782)**（Displacement Vector）$\boldsymbol{u}$ 的定义是连接一个物[质点](@entry_id:186768)从其[参考位](@entry_id:754187)置到其当前位置的矢量。对于由 $\boldsymbol{X}$ 标记的物质点，其位移为：
$$
\boldsymbol{u} = \boldsymbol{x} - \boldsymbol{X}
$$
由于 $\boldsymbol{x}$ 是 $\boldsymbol{X}$ 和 $t$ 的函数，[位移矢量场](@entry_id:196067)也自然地被定义为参考构型上的一个矢量场，即 $\boldsymbol{u}(\boldsymbol{X}, t)$:
$$
\boldsymbol{u}(\boldsymbol{X}, t) = \boldsymbol{\chi}(\boldsymbol{X}, t) - \boldsymbol{X}
$$
这种将物理量表达为物[质点](@entry_id:186768)（即参考坐标 $\boldsymbol{X}$）和时间 $t$ 的函数的描述方法，被称为**[拉格朗日描述](@entry_id:264498)**（Lagrangian Description）或**物质描述**（Material Description）。

一个自然的问题是：为什么不将[位移场](@entry_id:141476)定义为当前构型 $\mathcal{B}_t$ 上的函数，即 $\boldsymbol{d}(\boldsymbol{x}, t)$？这种描述被称为**[欧拉描述](@entry_id:264722)**（Eulerian Description）或**空间描述**（Spatial Description）。要定义这样一个场，我们必须首先确定在时刻 $t$ 占据空间位置 $\boldsymbol{x}$ 的是哪个物[质点](@entry_id:186768) $\boldsymbol{X}$，这需要反转运动映射：$\boldsymbol{X} = \boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)$。于是，空间位移场可以定义为 $\boldsymbol{d}(\boldsymbol{x}, t) = \boldsymbol{x} - \boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)$。

这种定义的根本问题在于，运动映射 $\boldsymbol{\chi}(\cdot, t)$ 不一定是[单射](@entry_id:183792)的（injective）。例如，在物体自接触的情况下，两个不同的物质点 $\boldsymbol{X}_1 \neq \boldsymbol{X}_2$ 可能在同一时刻占据同一个空间位置 $\boldsymbol{x}$。此时，$\boldsymbol{\chi}^{-1}(\boldsymbol{x}, t)$ 的值是模糊的，导致位移的定义不明确。因为位移的本质是比较*同一个物质点*的两个位置，所以它必须与物质点的唯一标签 $\boldsymbol{X}$ 绑定。因此，[拉格朗日描述](@entry_id:264498) $\boldsymbol{u}(\boldsymbol{X}, t)$ 是更基本、更普适的定义，即使在运动映射可逆的情况下，空间位移场 $\boldsymbol{d}(\boldsymbol{x}, t)$ 也是一个派生量，其计算依赖于运动的逆映射 [@problem_id:2695470]。

### 变形的局部度量：[位移梯度](@entry_id:165352)

[位移场](@entry_id:141476)本身只告诉我们每个点移动了多远，但要理解变形——即物体内部相对位置的改变——我们需要考察[位移场](@entry_id:141476)的空间变化率。**[位移梯度张量](@entry_id:748571)**（Displacement Gradient Tensor），记为 $\boldsymbol{H}$ 或 $\nabla_{\boldsymbol{X}} \boldsymbol{u}$，是描述这种局部变化的关键。其分量形式为 $H_{ij} = \frac{\partial u_i}{\partial X_j}$。

与[位移梯度](@entry_id:165352)密切相关的是**变形梯度张量**（Deformation Gradient Tensor） $\boldsymbol{F}$。它被定义为当前位置矢量 $\boldsymbol{x}$ 对[参考位](@entry_id:754187)置矢量 $\boldsymbol{X}$ 的梯度：
$$
\boldsymbol{F} = \nabla_{\boldsymbol{X}} \boldsymbol{x} = \nabla_{\boldsymbol{X}} (\boldsymbol{X} + \boldsymbol{u}) = \boldsymbol{I} + \nabla_{\boldsymbol{X}} \boldsymbol{u} = \boldsymbol{I} + \boldsymbol{H}
$$
其中 $\boldsymbol{I}$ 是二阶单位张量。变形梯度 $\boldsymbol{F}$ 具有清晰的几何意义：它将参考构型中的一个无穷小矢量 $d\boldsymbol{X}$ 映射到当前构型中对应的矢量 $d\boldsymbol{x}$，即 $d\boldsymbol{x} = \boldsymbol{F} d\boldsymbol{X}$。因此，$\boldsymbol{F}$ 包含了关于局部拉伸、剪切和旋转的全部信息。

### 变形的分解：应变与转动

变形梯度 $\boldsymbol{F}$ 描述了刚体运动（平移和转动）和纯变形（拉伸和剪切）的组合效应。为了发展本构关系，我们必须将这两种效应分离开来。分离的方式取决于变形的幅度。

#### 小变形运动学

当位移和[位移梯度](@entry_id:165352)都足够小（$||\nabla \boldsymbol{u}|| \ll 1$）时，我们可以采用线性化的[运动学](@entry_id:173318)理论。在这种情况下，[位移梯度张量](@entry_id:748571) $\boldsymbol{H}$ 可以被唯一地**加法分解**为一个对称[部分和](@entry_id:162077)一个反对称部分：
$$
\boldsymbol{H} = \boldsymbol{\varepsilon} + \boldsymbol{\omega}
$$
其中，对称部分被称为**[无穷小应变张量](@entry_id:167211)**（Infinitesimal Strain Tensor）：
$$
\boldsymbol{\varepsilon} = \frac{1}{2}(\boldsymbol{H} + \boldsymbol{H}^{\mathrm{T}}) = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\mathrm{T}})
$$
反对称部分被称为**无穷小转动张量**（Infinitesimal Rotation Tensor）：
$$
\boldsymbol{\omega} = \frac{1}{2}(\boldsymbol{H} - \boldsymbol{H}^{\mathrm{T}}) = \frac{1}{2}(\nabla \boldsymbol{u} - (\nabla \boldsymbol{u})^{\mathrm{T}})
$$
$\boldsymbol{\varepsilon}$ 的分量直接度量了物质微元的长度和角度变化。其对角分量 $\varepsilon_{ii}$ 表示沿 $X_i$ 轴的**[正应变](@entry_id:204633)**（Normal Strain），而非对角分量 $\varepsilon_{ij}$ ($i \neq j$) 则与 $X_i$ 和 $X_j$ 轴之间的角度变化有关，称为**[剪应变](@entry_id:175241)**（Shear Strain）。在[各向同性线弹性](@entry_id:185899)材料中，只有应变张量 $\boldsymbol{\varepsilon}$ 会产生应力并储存弹性能，而转动张量 $\boldsymbol{\omega}$ 代表了物质微元的局部[刚体转动](@entry_id:191086)，不引起能量变化 [@problem_id:2695506]。

应变张量的迹 $\mathrm{tr}(\boldsymbol{\varepsilon})$ 有一个特别重要的物理意义。通过计算可以发现：
$$
\mathrm{tr}(\boldsymbol{\varepsilon}) = \mathrm{tr}(\nabla \boldsymbol{u}) = \nabla \cdot \boldsymbol{u}
$$
这个量被称为**体积应变**（Volumetric Strain），它表示了在小变形假设下，单位体积的相对变化量。例如，一个初始体积为 $V_0$ 的微元，变形后的体积 $V$ 近似为 $V \approx V_0 (1 + \nabla \cdot \boldsymbol{u})$ [@problem_id:2695497]。

#### [大变形](@entry_id:167243)运动学

当转动或拉伸不是无穷小时，加法分解不再适用。特别是，即使是纯[刚体转动](@entry_id:191086)，[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 也会产生非零的、虚假的“应变”分量，这使得它不适合描述大转动问题。

为了正确处理[大变形](@entry_id:167243)，我们需要回到变形梯度 $\boldsymbol{F}$ 并采用**[乘法分解](@entry_id:199514)**。根据**极分解定理**（Polar Decomposition Theorem），任何可逆的变形梯度张量 $\boldsymbol{F}$ 都可以被唯一地分解为：
$$
\boldsymbol{F} = \boldsymbol{R}\boldsymbol{U} \quad \text{(右极分解)}
$$
或者
$$
\boldsymbol{F} = \boldsymbol{V}\boldsymbol{R} \quad \text{(左极分解)}
$$
其中：
- $\boldsymbol{R}$ 是一个**转动张量**（Rotation Tensor），它是一个正常交阵（$\boldsymbol{R}^{\mathrm{T}}\boldsymbol{R}=\boldsymbol{I}$ 且 $\det \boldsymbol{R} = 1$），描述了物质微元的局部[刚体转动](@entry_id:191086)。
- $\boldsymbol{U}$ 是**右[拉伸张量](@entry_id:193200)**（Right Stretch Tensor），它是一个[对称正定](@entry_id:145886)张量，作用在参考构型上，描述了在转动*之前*的纯拉伸。
- $\boldsymbol{V}$ 是**左[拉伸张量](@entry_id:193200)**（Left Stretch Tensor），它也是一个[对称正定](@entry_id:145886)张量，作用在当前构型上，描述了在转动*之后*的纯拉伸。

这两个[拉伸张量](@entry_id:193200)可以通过**柯西-格林变形张量**（Cauchy-Green Deformation Tensors）计算得到。**[右柯西-格林张量](@entry_id:174156)** $\boldsymbol{C} = \boldsymbol{F}^{\mathrm{T}}\boldsymbol{F}$，于是 $\boldsymbol{U} = \sqrt{\boldsymbol{C}}$。**[左柯西-格林张量](@entry_id:186163)** $\boldsymbol{B} = \boldsymbol{F}\boldsymbol{F}^{\mathrm{T}}$，于是 $\boldsymbol{V} = \sqrt{\boldsymbol{B}}$。例如，对于一个位移场 $\boldsymbol{u}(\boldsymbol{X}) = \begin{pmatrix} -X_{1} - X_{2} \\ 2 X_{1} - X_{2} \end{pmatrix}$，我们可以计算出变形梯度为 $\boldsymbol{F} = \begin{pmatrix} 0  -1 \\ 2  0 \end{pmatrix}$。通过计算 $\boldsymbol{C}=\boldsymbol{F}^{\mathrm{T}}\boldsymbol{F}$ 和 $\boldsymbol{B}=\boldsymbol{F}\boldsymbol{F}^{\mathrm{T}}$，可以得到右[拉伸张量](@entry_id:193200) $\boldsymbol{U} = \begin{pmatrix} 2  0 \\ 0  1 \end{pmatrix}$ 和左[拉伸张量](@entry_id:193200) $\boldsymbol{V} = \begin{pmatrix} 1  0 \\ 0  2 \end{pmatrix}$，以及转动张量 $\boldsymbol{R} = \begin{pmatrix} 0  -1 \\ 1  0 \end{pmatrix}$，它代表了逆时针旋转 $90^\circ$ [@problem_id:2695476]。

在[大变形理论](@entry_id:188422)中，一个客观（即与[刚体转动](@entry_id:191086)无关）的[应变度量](@entry_id:755495)是**[格林-拉格朗日应变张量](@entry_id:187745)**（Green-Lagrange Strain Tensor） $\boldsymbol{E}$：
$$
\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^{\mathrm{T}}\boldsymbol{F} - \boldsymbol{I}) = \frac{1}{2}(\boldsymbol{C} - \boldsymbol{I})
$$
通过代入 $\boldsymbol{F} = \boldsymbol{I} + \nabla \boldsymbol{u}$，可以得到 $\boldsymbol{E} = \boldsymbol{\varepsilon} + \frac{1}{2}((\nabla \boldsymbol{u})^{\mathrm{T}} \nabla \boldsymbol{u})$。这表明 $\boldsymbol{E}$ 包含了 $\boldsymbol{\varepsilon}$ 中没有的、关于[位移梯度](@entry_id:165352)的二次项。正是这些二次项，即所谓的**[几何非线性](@entry_id:169896)**（Geometric Nonlinearity），使得 $\boldsymbol{E}$ 能够在有限转动下保持客观性。例如，对于一个纯[刚体转动](@entry_id:191086)（$\boldsymbol{F}=\boldsymbol{R}, \boldsymbol{U}=\boldsymbol{I}$），我们有 $\boldsymbol{C} = \boldsymbol{R}^{\mathrm{T}}\boldsymbol{R} = \boldsymbol{I}$，因此 $\boldsymbol{E}=\boldsymbol{0}$，正确地反映了没有发生变形。然而，[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 在这种情况下通常不为零，从而给出了错误的结果 [@problem_id:2695496]。

在大变形下，体积变化的[精确度](@entry_id:143382)量是变形梯度的[行列式](@entry_id:142978)，即**[雅可比行列式](@entry_id:137120)**（Jacobian） $J = \det \boldsymbol{F}$。它表示了局部体积的变化率，$J = dV/dV_0$。在小变形的极限下，对 $J = \det(\boldsymbol{I} + \nabla \boldsymbol{u})$ 进行一阶[泰勒展开](@entry_id:145057)，我们得到 $J \approx 1 + \mathrm{tr}(\nabla \boldsymbol{u}) = 1 + \nabla \cdot \boldsymbol{u}$，这与之前[体积应变](@entry_id:267252)的结论完全一致 [@problem_id:2695497]。

### 弹性力学中的[位移场](@entry_id:141476)：[边值问题](@entry_id:193901)

在弹性力学中，[位移场](@entry_id:141476)通常是求解的核心未知量。一个完整的静力学问题由三个基本部分组成：
1.  **[平衡方程](@entry_id:172166)**（静力学）：$\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$，其中 $\boldsymbol{\sigma}$ 是柯西[应力张量](@entry_id:148973)，$\boldsymbol{b}$ 是单位体积的[体力](@entry_id:174230)。
2.  **[几何方程](@entry_id:173321)**（[运动学](@entry_id:173318)）：$\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\mathrm{T}})$。
3.  **[本构方程](@entry_id:138559)**（材料定律）：$\boldsymbol{\sigma} = \boldsymbol{\sigma}(\boldsymbol{\varepsilon})$，例如对于[各向同性线弹性](@entry_id:185899)材料，$\boldsymbol{\sigma} = \lambda \mathrm{tr}(\boldsymbol{\varepsilon})\boldsymbol{I} + 2\mu\boldsymbol{\varepsilon}$，其中 $\lambda$ 和 $\mu$ 是拉梅参数。

通过将[几何方程](@entry_id:173321)和[本构方程](@entry_id:138559)代入平衡方程，我们可以消去应变和应力，得到一个只包含[位移场](@entry_id:141476) $\boldsymbol{u}$ 的[偏微分方程](@entry_id:141332)。对于均匀[各向同性线弹性](@entry_id:185899)体，这个方程被称为**[纳维-柯西方程](@entry_id:189211)**（Navier-Cauchy Equation）：
$$
\mu \nabla^2 \boldsymbol{u} + (\lambda + \mu) \nabla(\nabla \cdot \boldsymbol{u}) + \boldsymbol{b} = \boldsymbol{0}
$$
这个方程的推导清晰地表明，位移场是求解弹性问题的核心变量 [@problem_id:2695495]。

为了得到一个适定的（well-posed）问题，我们还必须在物体的边界 $\partial\Omega$ 上规定**边界条件**（Boundary Conditions）。边界条件通常分为两类：
- **[本质边界条件](@entry_id:173524)**（Essential Boundary Conditions），也称**狄利克雷（Dirichlet）条件**：在边界的一部分 $\Gamma_u$ 上直接指定位移的值，例如 $\boldsymbol{u} = \bar{\boldsymbol{u}}$。它们之所以是“本质的”，是因为在基于变分原理（如虚功原理）的弱形式中，解函数必须在指定的[函数空间](@entry_id:143478)中满足这些条件。
- **自然边界条件**（Natural Boundary Conditions），也称**诺伊曼（Neumann）条件**：在边界的另一部分 $\Gamma_t$ 上指定**面力**（Traction）的值，$\boldsymbol{t} = \boldsymbol{\sigma}\boldsymbol{n} = \bar{\boldsymbol{t}}$，其中 $\boldsymbol{n}$ 是边界外[法线](@entry_id:167651)矢量。它们之所以是“自然的”，是因为它们在推导弱形式时通过[分部积分](@entry_id:136350)自然地出现，作为边界积分项，而不是作为对函数空间的硬性约束 [@problem_id:2695499]。

#### [解的唯一性](@entry_id:143619)与刚体位移

[纳维-柯西方程](@entry_id:189211)是一个[线性偏微分方程](@entry_id:172517)。它的[解的唯一性](@entry_id:143619)与一个重要概念——**刚体位移**（Rigid Body Motion）——密切相关。一个刚体位移 $\boldsymbol{u}_{rb}$ 是指不产生任何应变的[位移场](@entry_id:141476)，即 $\boldsymbol{\varepsilon}(\boldsymbol{u}_{rb}) = \boldsymbol{0}$。在二维空间中，任何刚体位移都可以表示为平移和一个[绕轴转动](@entry_id:185161)的组合：$\boldsymbol{u}_{rb}(\boldsymbol{x}) = \boldsymbol{c} + \omega \begin{pmatrix} -x_2 \\ x_1 \end{pmatrix}$，其中 $\boldsymbol{c}$ 是常数平移矢量，$\omega$ 是转动角。这个刚体[位移场](@entry_id:141476)构成的[线性空间](@entry_id:151108)维度为3（两个平移分量，一个转动分量）。

由于刚体位移不产生应变，它自然也不产生应力，$\boldsymbol{\sigma}(\boldsymbol{u}_{rb}) = \boldsymbol{0}$。因此，它自动满足无[体力](@entry_id:174230)时的[平衡方程](@entry_id:172166)，$\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u}_{rb}) = \boldsymbol{0}$。这意味着刚体[位移场](@entry_id:141476)是纳维-柯西算子的**核**（kernel），即 $\mathcal{L}[\boldsymbol{u}_{rb}] = \boldsymbol{0}$。

这个性质对[解的唯一性](@entry_id:143619)有直接影响。如果一个问题的边界条件全部是自然边界条件（纯面力问题），那么如果 $\boldsymbol{u}$ 是一个解，$\boldsymbol{u} + \boldsymbol{u}_{rb}$ 也必然是一个解，因为加上一个刚体位移既不改变控制方程，也不改变面力（因为应力为零）。因此，对于纯[诺伊曼问题](@entry_id:176713)，解最多只能在相差一个刚体位移的意义下是唯一的。为了获得唯一解，必须施加足够的[本质边界条件](@entry_id:173524)来约束物体的[刚体运动](@entry_id:193355) [@problem_id:2695525]。

### 高级课题：[可积性](@entry_id:142415)与计算问题

#### [应变协调性](@entry_id:199659)

我们已经知道位移场可以导出应变场。一个反向的问题是：给定一个对称的[应变张量](@entry_id:193332)场 $\boldsymbol{\varepsilon}(\boldsymbol{x})$，是否总能找到一个单值的位移场 $\boldsymbol{u}(\boldsymbol{x})$ 与之对应？答案是否定的。为了保证可以从应变场通过积分得到一个单值的[位移场](@entry_id:141476)，应变场的分量必须满足一定的可积性条件，即**[圣维南协调方程](@entry_id:754487)**（Saint-Venant Compatibility Conditions）。在三维情况下，这组方程可以写作：
$$
\nabla \times (\nabla \times \boldsymbol{\varepsilon})^{\mathrm{T}} = \boldsymbol{0}
$$
这本质上是要求应变的[二阶导数](@entry_id:144508)之间满足特定的关系。如果一个应变场不满足这些条件，它就是一个“不协调”的场，不可能来自任何连续的、单值的位移场。例如，对于一个给定的应变场，其中包含一个未知参数 $\alpha$，我们可以通过将该场代入协调方程来确定使该场协调的 $\alpha$ 值 [@problem_id:2695508]。

#### 计算挑战：[体积锁定](@entry_id:172606)

在将连续介质力学问题离散化以进行数值计算（如[有限元法](@entry_id:749389)）时，[位移场](@entry_id:141476)的理论会遇到新的挑战。一个典型的例子是处理**[近不可压缩材料](@entry_id:752388)**（Nearly Incompressible Materials）时出现的**[体积锁定](@entry_id:172606)**（Volumetric Locking）现象。

对于[近不可压缩材料](@entry_id:752388)，其拉梅参数满足 $\lambda \gg \mu$。从本构关系可知，这意味着一个很小的[体积应变](@entry_id:267252) $\nabla \cdot \boldsymbol{u}$ 会导致巨大的静水压力。在不可压缩极限下（$\lambda \to \infty$），[运动学](@entry_id:173318)上必须严格满足约束 $\nabla \cdot \boldsymbol{u} = 0$。

当使用标准的、基于位移的低阶有限元方法时，离散的位移[函数空间](@entry_id:143478)可能过于“贫乏”，无法很好地近似满足 $\nabla \cdot \boldsymbol{u} = 0$ 这个约束。例如，由线性函数构成的离散空间，其散度是常数，这使得在单元级别上精确满足[零散度](@entry_id:190991)变得非常困难。为了在能量最小化过程中惩罚非零的体积应变，巨大的 $\lambda$ 项会迫使整个离散位移解趋于零，除非它恰好位于离散的[无散度](@entry_id:190991)[子空间](@entry_id:150286)内。如果真实的物理变形（如弯曲）无法被这个贫乏的无散度[子空间](@entry_id:150286)很好地表示，那么数值解就会表现出被人为夸大的刚度，位移结果远小于真实值——这就是锁定。

这个问题的根源在于离散位移空间和其隐含的压力空间不满足LBB（Ladyzhenskaya-Babuška-Brezzi）稳定性条件。为了克服锁定，研究人员发展了多种技术，如使用满足[LBB条件](@entry_id:746626)的混合单元、对体积能项采用[减缩积分](@entry_id:167949)或选择性积分等，这些方法的本质都是为了在离散层面“放松”不可压缩约束 [@problem_id:2695462]。这提醒我们，即使是概念上清晰的位移场，在转化到计算实践时也需要深刻的数学洞察力。