## 引言
在现代工程与[科学计算](@entry_id:143987)中，有限元法（FEM）是分析[固体力学](@entry_id:164042)问题不可或缺的工具。然而，任何成功的[数值模拟](@entry_id:137087)都始于对所求解的物理问题有精确的数学描述。对于固体结构而言，这一描述的核心便是源于连续介质力学的平衡方程与边界条件。它们共同构成了描述结构如何在载荷作用下响应的数学模型。本文旨在填补抽象理论与计算实践之间的知识鸿沟，系统性地阐明这些基础方程的由来、内涵及其在有限元框架下的转化。

本文将引导读者深入探索从基本力学公理到高级数值应用的完整路径。我们将从以下三个方面展开：
- **原理与机制**：本章将追本溯源，从柯西[应力张量](@entry_id:148973)和牵[引力](@entry_id:175476)的概念出发，推导出描述物体受力的[局部平衡](@entry_id:156295)方程（强形式）。随后，我们将重点剖析两类关键的边界条件——[位移边界条件](@entry_id:203261)和[牵引边界条件](@entry_id:167112)，并展示如何通过虚功原理将强形式问题转化为更适合数值求解的弱形式，同时阐明“本质”与“自然”边界条件的深刻含义。
- **应用与[交叉](@entry_id:147634)学科联系**：理论的生命力在于应用。本章将展示这些核心原理在经典弹性力学、[结构分析](@entry_id:153861)、[非线性](@entry_id:637147)[大变形](@entry_id:167243)问题以及动力学分析中的具体应用。我们将探讨它们如何在有限元方法中被离散化和实现，以及它们如何与[材料科学](@entry_id:152226)、流固耦合和[科学机器学习](@entry_id:145555)等前沿领域交叉融合。
- **动手实践**：为了将理论知识转化为实践能力，本章提供了一系列精心设计的编程练习。这些练习将引导你通过[代码验证](@entry_id:146541)、[数值积分](@entry_id:136578)和“制造解方法”等手段，加深对牵[引力](@entry_id:175476)加载、代码正确性验证和[收敛性分析](@entry_id:151547)的理解。

通过学习本文，你将为掌握和应用高级[有限元分析](@entry_id:138109)打下坚实的理论基础，并能更深刻地理解数值模拟背后的物理与数学原理。

## 原理与机制

在对有限元法进行系统性学习之前，我们必须首先掌握其所求解的物理问题的数学描述。对于[固体力学](@entry_id:164042)问题，这些描述建立在[连续介质力学](@entry_id:155125)的基本原理之上。本章旨在深入阐述这些核心原理，重点关注[平衡方程](@entry_id:172166)和[牵引边界条件](@entry_id:167112)，它们共同构成了[有限元分析](@entry_id:138109)的强形式（strong form）和[弱形式](@entry_id:142897)（weak form）的基础。我们将从基本概念出发，推导出控制方程，并阐明在变分框架下如何处理不同类型的边界条件，为后续的[数值离散化](@entry_id:752782)奠定坚实的理论基础。

### 柯西应力与边界牵[引力](@entry_id:175476)

考虑一个占据三维空间中某个区域 $\Omega$ 的连续体。当这个物体受到外部载荷或约束时，其内部会产生相互作用力。为了描述这种内部作用力，我们引入**牵[引力](@entry_id:175476)矢量（traction vector）** $\mathbf{t}$ 的概念。想象在物体内部任取一点 $\mathbf{x}$，并切出一个具有单位法向矢量 $\mathbf{n}$ 的无限小虚拟表面。物体在 $\mathbf{n}$ 所指向的一侧对另一侧施加的力，除以该微小面积 $A$，在其面积趋近于零时的极限，就定义为在该点、该方向上的牵[引力](@entry_id:175476)矢量 [@problem_id:2556124]：

$$
\mathbf{t}(\mathbf{x}, \mathbf{n}) = \lim_{A \to 0} \frac{\Delta\mathbf{F}}{A}
$$

这里，$\Delta\mathbf{F}$ 是通过面积为 $A$ 的微小表面传递的[接触力](@entry_id:165079)。牵[引力](@entry_id:175476)是一个矢量，其物理单位是力每单位面积（例如，帕斯卡 Pa 或 N/m²）。值得注意的是，牵[引力](@entry_id:175476)的定义与当前构型（current configuration）下的面积相关。

牵[引力](@entry_id:175476) $\mathbf{t}$ 依赖于其作用点 $\mathbf{x}$ 和作用面的法向 $\mathbf{n}$。一个核心的力学原理，即**柯西应力定理（Cauchy's Stress Theorem）**，揭示了这两者之间的[线性关系](@entry_id:267880)。该定理指出，在任意一点 $\mathbf{x}$，存在一个[二阶张量](@entry_id:199780) $\boldsymbol{\sigma}(\mathbf{x})$，称为**柯西应力张量（Cauchy stress tensor）**，使得对于任何方向的单位法向 $\mathbf{n}$，其上的牵[引力](@entry_id:175476)矢量 $\mathbf{t}$ 都可以通过下式计算得出 [@problem_id:2556124, 2556063]：

$$
\mathbf{t}(\mathbf{x}, \mathbf{n}) = \boldsymbol{\sigma}(\mathbf{x})\mathbf{n}
$$

柯西应力张量 $\boldsymbol{\sigma}$ 完全描述了物体内一点的应力状态。它不依赖于作用面的方向 $\mathbf{n}$，而是该点固有的物理属性。在三维空间中，$\boldsymbol{\sigma}$ 是一个 $3 \times 3$ 的矩阵。此外，基于动量矩平衡原理（balance of angular momentum），在没有体力矩（body couple）的经典连续介质模型中，柯西[应力张量](@entry_id:148973)被证明是对称的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^T$。这一对称性在后续的变分推导中至关重要。

### [动量平衡](@entry_id:193575)：控制[微分方程](@entry_id:264184)

所有力学问题的核心是[牛顿运动定律](@entry_id:163846)。对于连续体，我们可以将其应用于任意一个子区域（[控制体](@entry_id:143882)）$\omega \subset \Omega$。线[动量平衡原理](@entry_id:196256)（balance of linear momentum）指出，[控制体](@entry_id:143882)内[线动量](@entry_id:174467)的变化率等于作用在该[控制体](@entry_id:143882)上的所有外力之和。这些外力包括作用在[控制体](@entry_id:143882)表面 $\partial\omega$ 上的[表面力](@entry_id:188034)（通过牵[引力](@entry_id:175476) $\mathbf{t}$ 描述）和作用在[控制体](@entry_id:143882)内部的体力（body force）$\mathbf{b}$（单位质量的力，如重力）。对于动态问题，这一平衡关系可以写作 [@problem_id:2556096]：

$$
\frac{d}{dt}\int_{\omega} \rho \dot{\mathbf{u}} \, d\Omega = \int_{\omega} \rho \mathbf{b} \, d\Omega + \int_{\partial\omega} \mathbf{t} \, d\Gamma
$$

其中，$\rho$ 是质量密度，$\mathbf{u}$ 是[位移场](@entry_id:141476)，$\dot{\mathbf{u}}$ 是速度。

利用柯西应力定理 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$，并将[高斯散度定理](@entry_id:188065)（divergence theorem）应用于表[面积分](@entry_id:275394)项，我们可以将其转化为[体积分](@entry_id:171119)：

$$
\int_{\partial\omega} \mathbf{t} \, d\Gamma = \int_{\partial\omega} \boldsymbol{\sigma}\mathbf{n} \, d\Gamma = \int_{\omega} \nabla \cdot \boldsymbol{\sigma} \, d\Omega
$$

这里，$\nabla \cdot \boldsymbol{\sigma}$ 是应力[张量的散度](@entry_id:191736)。将此结果代回[动量平衡](@entry_id:193575)方程，并将时间导数移入积分号内（假设足够光滑），我们得到：

$$
\int_{\omega} \rho \ddot{\mathbf{u}} \, d\Omega = \int_{\omega} \rho \mathbf{b} \, d\Omega + \int_{\omega} \nabla \cdot \boldsymbol{\sigma} \, d\Omega
$$

由于这个积分等式对任意控制体 $\omega$ 都成立，因此被积函数必须处处相等。这便得到了[动量平衡](@entry_id:193575)的**局部（local）**或**[微分形式](@entry_id:146747)**：

$$
\nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b} = \rho \ddot{\mathbf{u}}
$$

这个方程是[弹性动力学](@entry_id:175818)问题的**强形式（strong form）**控制方程。我们来分析方程中每一项的物理意义 [@problem_id:2556148]：
*   $\nabla \cdot \boldsymbol{\sigma}$：应力[张量的散度](@entry_id:191736)，代表由应力在空间上的不[均匀分布](@entry_id:194597)引起的单位体积的净内部[接触力](@entry_id:165079)，其量纲为力/体积。
*   $\rho \mathbf{b}$：单位体积的[体力](@entry_id:174230)，例如重力密度。其量纲也为力/体积。
*   $\rho \ddot{\mathbf{u}}$：单位体积的惯性力，其中 $\ddot{\mathbf{u}}$ 是加速度。根据[牛顿第二定律](@entry_id:274217)，这一项是质量密度与加速度的乘积，量纲同样为力/体积。

在许多工程问题中，我们关心的是静态或准静态（quasi-static）情况，此时物体的运动非常缓慢，惯性效应可以忽略不计 ($\ddot{\mathbf{u}} = \mathbf{0}$)。在这种情况下，平衡方程简化为：

$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}
$$

这个方程是在区域 $\Omega$ 内部必须满足的平衡条件。对于一个完整的**[边值问题](@entry_id:193901)（Boundary Value Problem, BVP）**，我们还需要在物体的边界 $\partial\Omega$ 上施加合适的条件。

### 边界条件：本质与自然之分

控制[微分方程](@entry_id:264184)的解通常不是唯一的，除非在边界上指定了足够的约束。在[固体力学](@entry_id:164042)中，边界条件通常分为两类。我们将物体的总边界 $\partial\Omega$ 分割为两个互不相交的部分，$\Gamma_u$ 和 $\Gamma_t$，使得 $\partial\Omega = \Gamma_u \cup \Gamma_t$ 且 $\Gamma_u \cap \Gamma_t = \emptyset$。

1.  **[位移边界条件](@entry_id:203261) (Displacement Boundary Conditions)**：在边界部分 $\Gamma_u$ 上，我们直接规定物体的位移。这种条件通常被称为**本质边界条件（essential boundary conditions）**或**[狄利克雷条件](@entry_id:137096)（Dirichlet conditions）**。其数学表达式为：
    $$
    \mathbf{u} = \bar{\mathbf{u}} \quad \text{on } \Gamma_u
    $$
    其中 $\bar{\mathbf{u}}$ 是已知的位移函数。

2.  **[牵引边界条件](@entry_id:167112) (Traction Boundary Conditions)**：在边界部分 $\Gamma_t$ 上，我们规定作用在物体表面的力。利用柯西应力定理，这等价于规定[应力张量](@entry_id:148973)与边界外法向 $\mathbf{n}$ 的乘积。这种条件被称为**自然边界条件（natural boundary conditions）**或**[诺伊曼条件](@entry_id:165471)（Neumann conditions）** [@problem_id:2556063]。其数学表达式为：
    $$
    \boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}} \quad \text{on } \Gamma_t
    $$
    其中 $\bar{\mathbf{t}}$ 是已知的牵[引力](@entry_id:175476)矢量。

综上所述，一个完整的线[弹性静力学](@entry_id:198298)问题的**强形式表述**包括：在区域 $\Omega$ 内满足平衡方程、[本构关系](@entry_id:186508)（如 $\boldsymbol{\sigma} = \mathbb{C}:\boldsymbol{\varepsilon}$）和几何关系（如 $\boldsymbol{\varepsilon} = \nabla^s \mathbf{u}$），同时在边界 $\Gamma_u$ 上满足位移条件，在边界 $\Gamma_t$ 上满足牵[引力](@entry_id:175476)条件 [@problem_id:2556147]。

### [弱形式](@entry_id:142897)：通往有限元法的桥梁

直接求解强形式的[偏微分方程组](@entry_id:172573)通常非常困难，尤其是对于具有复杂几何形状和边界条件的实际问题。有限元法正是通过求解其等价的**[弱形式](@entry_id:142897)（weak form）**或**[变分形式](@entry_id:166033)（variational form）**来克服这一困难。弱形式的推导基于**虚功原理（Principle of Virtual Work）**。

我们从静态平衡方程出发：
$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}
$$
我们将该方程与一个任意的、满足特定条件的矢量函数 $\mathbf{w}$（称为**[虚位移](@entry_id:168781)**或**检验函数 (test function)**）做[点积](@entry_id:149019)，然后在整个区域 $\Omega$ 上进行积分：
$$
\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \mathbf{b}) \cdot \mathbf{w} \, d\Omega = 0
$$
这个积分形式的方程之所以被称为“弱”形式，是因为它不要求[平衡方程](@entry_id:172166)在每个点上都严格成立，而是在积分平均的意义上成立。

接下来是关键一步：**[分部积分](@entry_id:136350)（integration by parts）**，在多维情况下通过[散度定理](@entry_id:143110)实现。我们对包含最[高阶导数](@entry_id:140882)的项 $\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{w} \, d\Omega$ 进行处理 [@problem_id:2556123]。利用张量恒等式和散度定理，可以得到：
$$
\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{w} \, d\Omega = \int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma - \int_{\Omega} \boldsymbol{\sigma} : \nabla\mathbf{w} \, d\Omega
$$
这里，冒号“:”代表张量的[双点积](@entry_id:748648)。将此式代回原[积分方程](@entry_id:138643)，并利用[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 的对称性（$\boldsymbol{\sigma} : \nabla\mathbf{w} = \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{w})$，其中 $\boldsymbol{\varepsilon}(\mathbf{w})$ 是虚应变张量），我们得到[虚功原理](@entry_id:138749)的数学表达式：
$$
\int_{\Omega} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}(\mathbf{w}) \, d\Omega = \int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, d\Omega + \int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma
$$
等式左边代表**[内虚功](@entry_id:172278)**（internal virtual work），右边是体力与[表面力](@entry_id:188034)所做的**外[虚功](@entry_id:176403)**（external virtual work）。

现在，我们来考察边界积分项 $\int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma$ 如何帮助我们处理边界条件。我们将边界积分分解到 $\Gamma_u$ 和 $\Gamma_t$ 上：
$$
\int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma = \int_{\Gamma_u} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma + \int_{\Gamma_t} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma
$$

在推导[弱形式](@entry_id:142897)的过程中，我们对检验函数 $\mathbf{w}$ 的选择施加了一个关键约束：它必须在[本质边界条件](@entry_id:173524)（位移边界）$\Gamma_u$ 上为零，即 $\mathbf{w} = \mathbf{0}$ on $\Gamma_u$ [@problem_id:2556162, 2556061]。这一要求的动机是，在 $\Gamma_u$ 上，真实的边界牵[引力](@entry_id:175476) $(\boldsymbol{\sigma}\mathbf{n})$ 是未知的反力。通过令 $\mathbf{w}=\mathbf{0}$ on $\Gamma_u$，我们巧妙地使得包含这个未知反力的积分项自动消失，从而避免了在方程中引入新的未知量。

而在边界 $\Gamma_t$ 上，牵[引力](@entry_id:175476)是已知的，$\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$。我们可以直接将这个已知量代入积分中。因此，边界积分项最终简化为：
$$
\int_{\partial\Omega} (\boldsymbol{\sigma}\mathbf{n}) \cdot \mathbf{w} \, d\Gamma = \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{w} \, d\Gamma
$$
至此，[弱形式](@entry_id:142897)的最终形式为：寻找一个位移场 $\mathbf{u}$（它必须满足本质边界条件 $\mathbf{u}=\bar{\mathbf{u}}$ on $\Gamma_u$），使得对于所有满足 $\mathbf{w}=\mathbf{0}$ on $\Gamma_u$ 的[检验函数](@entry_id:166589) $\mathbf{w}$，以下方程均成立：

$$
\underbrace{\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{w}) \, d\Omega}_{a(\mathbf{u}, \mathbf{w})} = \underbrace{\int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, d\Omega + \int_{\Gamma_t} \bar{\mathbf{t}} \cdot \mathbf{w} \, d\Gamma}_{L(\mathbf{w})}
$$

这个推导过程清晰地揭示了为何两类边界条件有“本质”与“自然”之分 [@problem_id:2556146, 2556162]：
*   **本质边界条件 (Essential BCs)**：[位移边界条件](@entry_id:203261) $\mathbf{u} = \bar{\mathbf{u}}$ 必须被施加在解的函数空间（称为**[试探空间](@entry_id:756166) trial space**）上，它定义了“运动学上可容许”的位移。同时，[检验函数](@entry_id:166589)必须在这些边界上取零值。这些条件是求解框架的先决条件，必须被“本质地”或“强行地”满足。
*   **自然边界条件 (Natural BCs)**：牵[引力](@entry_id:175476)边界条件 $\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$ 无需对函数空间施加约束。它们通过[分部积分](@entry_id:136350)**自然地**出现在弱形式的[线性泛函](@entry_id:276136) $L(\mathbf{w})$（载荷项）中，成为外力功的一部分。只要弱形式方程得到满足，这些边界条件就会在积分意义上被自动满足。

从更深入的[泛函分析](@entry_id:146220)角度看，这种处理方式保证了问题的良定性。将非齐次的[本质边界条件](@entry_id:173524)强加于[试探空间](@entry_id:756166)，可以确保在求解时[双线性](@entry_id:146819)形 $a(\cdot, \cdot)$ 在相应的齐次函数空间上是矫顽的（coercive），而线性泛函 $L(\cdot)$ 是有界的，这正是[Lax-Milgram定理](@entry_id:137966)保证解存在且唯一的关键条件 [@problem_id:2556162]。

### 边界条件的深入探讨

#### 示例计算

为了将上述理论具体化，让我们考虑一个二维平面应变问题 [@problem_id:2556147]。假设一个弹性体，其[位移场](@entry_id:141476)由 $\mathbf{u}(x,y) = \begin{pmatrix} axy \\ cx^2 \end{pmatrix}$ 给出，其中 $a$ 和 $c$ 是常数。
首先，我们计算应变张量 $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$：
$$
\nabla\mathbf{u} = \begin{pmatrix} ay & ax \\ 2cx & 0 \end{pmatrix} \quad \implies \quad \boldsymbol{\varepsilon} = \begin{pmatrix} ay & \frac{1}{2}(ax+2cx) \\ \frac{1}{2}(ax+2cx) & 0 \end{pmatrix}
$$
对于 isotropic linear elastic material ([各向同性线弹性](@entry_id:185899)材料)，应力张量由 Lamé 参数 $\lambda$ 和 $\mu$ 给出：$\boldsymbol{\sigma} = \lambda \operatorname{tr}(\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}$。在[平面应变](@entry_id:167046)条件下，$\operatorname{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{xx} + \varepsilon_{yy} = ay$。因此，应力分量为：
$$
\sigma_{xx} = \lambda(ay) + 2\mu(ay) = (\lambda+2\mu)ay
$$
$$
\sigma_{yy} = \lambda(ay) + 2\mu(0) = \lambda ay
$$
$$
\sigma_{xy} = 2\mu \varepsilon_{xy} = \mu(a+2c)x
$$
现在，假设我们要计算在 $x=L$ 的右边界上的牵[引力](@entry_id:175476) $\mathbf{t}_R$。该边界的外法线是 $\mathbf{n} = \begin{pmatrix} 1 \\ 0 \end{pmatrix}$。根据柯西公式 $\mathbf{t} = \boldsymbol{\sigma}\mathbf{n}$：
$$
\mathbf{t}_R(y) = \boldsymbol{\sigma}(L, y)\mathbf{n} = \begin{pmatrix} (\lambda+2\mu)ay & \mu(a+2c)L \\ \mu(a+2c)L & \lambda ay \end{pmatrix} \begin{pmatrix} 1 \\ 0 \end{pmatrix} = \begin{pmatrix} (\lambda+2\mu)ay \\ \mu(a+2c)L \end{pmatrix}
$$
这个计算过程清晰地展示了如何从[位移场](@entry_id:141476)出发，通过几何关系和[本构关系](@entry_id:186508)得到应[力场](@entry_id:147325)，并最终利用柯西公式计算出任意边界上的牵[引力](@entry_id:175476)。

#### 问题的良定性与边界条件的设定

正确设定边界条件是确保问题有唯一解（或在特定情况下，解在某个[子空间](@entry_id:150286)内唯一）的关键。在边界的任何一点，每个方向上只能指定位移或牵[引力](@entry_id:175476)中的一个，不能同时指定两者 [@problem_id:2556071]。

以一个长度为 $L$、杨氏模量为 $E$ 的一维杆为例。其平衡方程为 $\frac{d\sigma}{dx}=0$，意味着应力 $\sigma$ 是一个常数 $C_1$。位移解为 $u(x) = \frac{C_1}{E}x + C_2$。如果我们固定左端 $u(0)=0$，则 $C_2=0$。此时，如果在右端 $x=L$ 同时规定位移 $u(L)=\Delta$ 和牵[引力](@entry_id:175476) $t(L)=t_0$，会发生什么？
*   位移条件给出：$u(L) = \frac{C_1}{E}L = \Delta \implies C_1 = \frac{E\Delta}{L}$。
*   牵[引力](@entry_id:175476)条件给出：$t(L) = \sigma(L)n(L) = C_1 \cdot 1 = t_0 \implies C_1 = t_0$。
显然，这两个条件只有在 $t_0 = E\Delta/L$ 这个**相容性条件（compatibility condition）**满足时才能共存。否则，问题是**超定（over-specified）**的，无解。

这说明，在一个边界点，我们不能同时规定共轭的物理量（如同一个方向上的位移和力）。然而，这并不意味着我们不能在同一点上混合指定不同方向的边界条件。例如，对于一个二维问题，在一个边界上规定法向位移和切向牵[引力](@entry_id:175476)是完全合理的，这被称为**[混合边界条件](@entry_id:176456)（mixed boundary conditions）**。一个典型的例子是无[摩擦接触](@entry_id:749595)问题，其中法向位移被限制（例如，不能穿透墙壁），而切向牵[引力](@entry_id:175476)为零 [@problem_id:2556071]。

另一类重要的边界条件是**[罗宾边界条件](@entry_id:163914)（Robin boundary conditions）**，它将位移和牵[引力](@entry_id:175476)联系起来，例如 $\mathbf{t} = k\mathbf{u}$（其中 $k>0$ 是常数）。这可以模拟物体放置在[弹性地基](@entry_id:186539)上的情况，地基提供的支撑力（牵[引力](@entry_id:175476)）与物体的位移成正比。这种条件也没有超定问题，因为它为每个方向提供了一个位移和牵[引力](@entry_id:175476)之间的约束关系，而不是直接规定它们的值 [@problem_id:2556071]。

最后，对于纯[诺伊曼问题](@entry_id:176713)（即整个边界都施加牵[引力](@entry_id:175476)，$\Gamma_u = \emptyset$），物体会存在刚体运动（[平动](@entry_id:187700)和转动）的自由度，因为[刚体运动](@entry_id:193355)不产生应变，从而不产生内力。这导致有限元法中的[刚度矩阵](@entry_id:178659)是奇异的。为了使问题有解，所施加的外力（包括[体力](@entry_id:174230)和牵[引力](@entry_id:175476)）必须自身平衡，即[合力](@entry_id:163825)与[合力矩](@entry_id:166772)均为零。这是纯[诺伊曼问题](@entry_id:176713)的**可解性条件（solvability condition）** [@problem_id:2556063]。

本章系统地阐述了从连续介质力学的基本公理到适用于[有限元法](@entry_id:749389)的[变分形式](@entry_id:166033)的推导过程，并深入探讨了边界条件的核心作用和正确设定方式。掌握这些原理和机制，是后续学习和应用有限元方法不可或缺的一步。