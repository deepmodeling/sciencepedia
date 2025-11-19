## 引言
在固体力学领域，虚功原理是一个基石性概念，它为描述和分析物体的平衡状态提供了一种与牛顿定律等效但更为深刻和普适的视角。传统上，[平衡问题](@entry_id:636409)通过建立局部[力平衡](@entry_id:267186)的[微分方程](@entry_id:264184)（即“强形式”）来求解，但这种方法在面对复杂几何、边界条件或材料行为时会变得异常困难。虚功原理通过一个全局的、积分形式的能量陈述，巧妙地绕开了这些困难，为现代计算力学的发展铺平了道路。

本文旨在对[可变形体](@entry_id:201887)的[虚功原理](@entry_id:138749)进行一次全面而深入的剖析，从其理论核心到其在尖端工程问题中的应用。我们将分三个章节展开：第一章，“原理与机制”，将系统阐述[虚功原理](@entry_id:138749)的数学构造，揭示其与强形式的[等价关系](@entry_id:138275)，并介绍其在现代变分理论框架下的严谨表述。第二章，“应用与跨学科联系”，将展示该原理如何统一地应用于结构力学、动力学、[多物理场耦合](@entry_id:171389)和[非线性材料建模](@entry_id:752644)等多个领域，彰显其作为一种通用工具的强大威力。最后，在“动手实践”部分，我们将通过一系列精选的计算练习，将理论知识转化为解决实际问题的能力。通过本次学习，读者将深刻理解虚功原理为何是连接理论力学与现代工程计算的桥梁。

## 原理与机制

本章旨在系统性地阐述[可变形体](@entry_id:201887)[虚功原理](@entry_id:138749)的理论基础与核心机制。我们将从虚功原理的基本陈述出发，逐步深入其数学构造、与强形式（[微分方程](@entry_id:264184)）的[等价关系](@entry_id:138275)，并探讨其在[非线性力学](@entry_id:178303)和现代变分理论框架下的扩展。本章内容是理解和应用[有限元法](@entry_id:749389)等计算力学方法的基石。

### [虚功](@entry_id:176403)的基本概念

在静力学中，一个处于平衡状态的物体，其内部和外部的所有力必然相互抵消。虚功原理为这一朴素的物理直觉提供了另一种等效且功能强大的数学表述。它考察的是，当物体从其[平衡位置](@entry_id:272392)经历一个**[虚位移](@entry_id:168781)（virtual displacement）**时，系统中的力所做的功。

我们需要精确地定义**[虚位移](@entry_id:168781)** $\delta\boldsymbol{u}$。它并非物体在真实时间过程中的实际位移增量，而是一个概念上的、无穷小的、满足所有运动学约束的任意位移场。可以将它想象成对平衡构型的一次“虚拟扰动”。它是一个用于“探测”系统是否平衡的数学工具。与此相对，在求解[非线性](@entry_id:637147)问题时出现的位移**增量** $\Delta\boldsymbol{u}$ 是一个真实的、待求解的量，它将物体的构型从一个迭代步更新到下一个迭代步。[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 是一个任意的检验函数，而位移增量 $\Delta\boldsymbol{u}$ 则是线性化平衡方程的特定解。[@problem_id:2676355]

**[虚功原理](@entry_id:138749) (Principle of Virtual Work, PVW)** 的核心论断是：一个[可变形体](@entry_id:201887)处于平衡状态的充分必要条件是，对于任何满足[运动学](@entry_id:173318)约束的[虚位移](@entry_id:168781)，所有外力所做的**[虚功](@entry_id:176403)**与所有内力所做的**[虚功](@entry_id:176403)**之和为零。通常，我们将[内力](@entry_id:167605)功以负号计入，从而得到一个更常用的表述：

$$
\delta W_{\text{int}} = \delta W_{\text{ext}}
$$

即，对于任意容许的[虚位移](@entry_id:168781)，**内力[虚功](@entry_id:176403)等于外力[虚功](@entry_id:176403)**。

### [虚功](@entry_id:176403)的量化表达

为了应用虚功原理，我们必须为内力[虚功](@entry_id:176403)和外力[虚功](@entry_id:176403)建立精确的数学表达式。

#### 外力[虚功](@entry_id:176403)

外力通常分为两类：作用于整个体积的**体力（body forces）**和作用于物体表面的**面力（surface forces 或 tractions）**。

假设物体占据的区域为 $\Omega$，其边界为 $\partial\Omega$。体力密度为 $\boldsymbol{b}(\boldsymbol{x})$（单位体积的力），施加在边界一部分 $\Gamma_t$ 上的面力密度为 $\bar{\boldsymbol{t}}(\boldsymbol{x})$（单位面积的力）。功的基本定义是力与位移的[点积](@entry_id:149019)。因此，在一个[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}(\boldsymbol{x})$ 下，外力所做的总[虚功](@entry_id:176403) $\delta W_{\text{ext}}$ 就是这些力在各自作用域上的积分 [@problem_id:2676312]：

$$
\delta W_{\text{ext}} = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta\boldsymbol{u} \, \mathrm{d}A
$$

这里有两点需要注意：
1.  上式中的积分是在当前构型下进行的。在小应变理论中，当前构型与参考构型可以不加区分。
2.  面力积分**仅在边界的 $\Gamma_t$ 部分执行**。边界的另一部分，我们称之为 $\Gamma_u$，是位移被指定的部分（[位移边界条件](@entry_id:203261)）。在 $\Gamma_u$ 上也存在面力，即维持指定位移所需的**支反力**。然而，我们稍后将看到，[虚功原理](@entry_id:138749)的巧妙之处在于，通过对[虚位移](@entry_id:168781)场的恰当选择，这些未知的支反力并不会出现在[虚功](@entry_id:176403)方程中。

#### 内力[虚功](@entry_id:176403)

内力[虚功](@entry_id:176403) $\delta W_{\text{int}}$ 是物体内部的应[力场](@entry_id:147325) $\boldsymbol{\sigma}$ 在虚变形过程中所做的功。在连续介质力学中，与应力张量 $\boldsymbol{\sigma}$ **[功共轭](@entry_id:194957)（work-conjugate）**的运动学量是[应变率张量](@entry_id:266108)。对于[虚位移](@entry_id:168781)，这个量就是**虚[应变张量](@entry_id:193332)（virtual strain tensor）** $\delta\boldsymbol{\varepsilon}$。因此，[内力](@entry_id:167605)[虚功](@entry_id:176403)可以直观地定义为：

$$
\delta W_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} \, \mathrm{d}V
$$

其中“$:$”表示张量的[双点积](@entry_id:748648)。在小应变理论中，虚应变张量 $\delta\boldsymbol{\varepsilon}$ 是虚[位移梯度](@entry_id:165352) $\nabla\delta\boldsymbol{u}$ 的对称部分：

$$
\delta\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla\delta\boldsymbol{u} + (\nabla\delta\boldsymbol{u})^{\mathsf{T}} \right)
$$

一个关键的问题是：为什么内力[虚功](@entry_id:176403)的表达式中是虚应变 $\delta\boldsymbol{\varepsilon}$，而不是完整的虚[位移梯度](@entry_id:165352) $\nabla\delta\boldsymbol{u}$？答案在于经典连续介质（或称Cauchy连续介质）的一个基本假设。在没有体力偶和面力偶的情况下，动量矩平衡定律要求Cauchy应力张量 $\boldsymbol{\sigma}$ 必须是**对称**的，即 $\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}}$。

任何二阶张量（如 $\nabla\delta\boldsymbol{u}$）都可以分解为一个对称部分和一个反对称部分。虚[位移梯度](@entry_id:165352)的反对称部分，$\delta\boldsymbol{\omega} = \frac{1}{2} ( \nabla\delta\boldsymbol{u} - (\nabla\delta\boldsymbol{u})^{\mathsf{T}} )$，代表了物质微元的**虚[刚体转动](@entry_id:191086)（virtual rigid-body rotation）**。根据[张量代数](@entry_id:161671)的基本性质，一个对称张量与一个[反对称张量](@entry_id:199349)的[双点积](@entry_id:748648)恒为零。因此：

$$
\boldsymbol{\sigma} : \delta\boldsymbol{\omega} = 0
$$

这意味着，对于一个Cauchy连续体，应[力场](@entry_id:147325)在材料的纯[刚体转动](@entry_id:191086)部分不做功。内力[虚功](@entry_id:176403)的完整表达式本应是 $\int_{\Omega} \boldsymbol{\sigma} : \nabla\delta\boldsymbol{u} \, \mathrm{d}V$，但由于 $\boldsymbol{\sigma}$ 的对称性，我们可以将其写为：

$$
\boldsymbol{\sigma} : \nabla\delta\boldsymbol{u} = \boldsymbol{\sigma} : (\delta\boldsymbol{\varepsilon} + \delta\boldsymbol{\omega}) = \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon} + \boldsymbol{\sigma} : \delta\boldsymbol{\omega} = \boldsymbol{\sigma} : \delta\boldsymbol{\varepsilon}
$$

所以，内力[虚功](@entry_id:176403)只与虚应变（变形部分）有关，而与虚转动（刚体运动部分）无关。这个结论是建立在Cauchy[应力对称性](@entry_id:181689)之上的。在一些更广义的连续介质理论中，如[Cosserat介质](@entry_id:747932)或偶应力理论，应力张量不必是对称的，其反对称部分会与材料的微观转动梯度发生[能量耦合](@entry_id:137595)。但在经典力学范畴内，[应力的对称性](@entry_id:181684)是基本假设。[@problem_id:2676278]

### 容许位移空间：运动学约束的数学诠释

[虚功原理](@entry_id:138749)的表述中包含一个至关重要的条件：[虚位移](@entry_id:168781)必须是“运动学容许的”（kinematically admissible）。这一要求的精确化是构建严谨变分理论的核心。

一个真实的[位移场](@entry_id:141476) $\boldsymbol{u}$ 必须满足问题的**[本质边界条件](@entry_id:173524)（essential boundary conditions）**，即在边界 $\Gamma_u$ 上位移被指定为 $\bar{\boldsymbol{u}}$。我们可以将所有满足此条件的位移场集合视为一个“约束[流形](@entry_id:153038)”。[虚位移](@entry_id:168781) $\delta\boldsymbol{u}$ 代表了这个[流形](@entry_id:153038)上真实解 $\boldsymbol{u}$ 处的一个“[切线](@entry_id:268870)方向”。这意味着，如果 $\boldsymbol{u}$ 是一个容许的[位移场](@entry_id:141476)（即 $\boldsymbol{u}|_{\Gamma_u} = \bar{\boldsymbol{u}}$），那么一个被扰动后的场 $\boldsymbol{u} + \delta\boldsymbol{u}$ 也必须（在[一阶近似](@entry_id:147559)下）是一个容许的[位移场](@entry_id:141476)。这要求：

$$
(\boldsymbol{u} + \delta\boldsymbol{u})|_{\Gamma_u} = \bar{\boldsymbol{u}}
$$

由于 $\boldsymbol{u}|_{\Gamma_u} = \bar{\boldsymbol{u}}$，上述条件直接导出对[虚位移](@entry_id:168781)的约束：

$$
\delta\boldsymbol{u}|_{\Gamma_u} = \boldsymbol{0}
$$

这就是对[虚位移](@entry_id:168781)场最关键的运动学要求：**在指定位移的边界上，[虚位移](@entry_id:168781)必须为零**。[@problem_id:2676379] 这个简单的要求具有深远的意义：
1.  它使得外力[虚功](@entry_id:176403)表达式中未知的支反力（作用在 $\Gamma_u$ 上）所做的功为零，从而将它们从方程中消除。
2.  它为选择合适的[函数空间](@entry_id:143478)提供了依据。

除了边界条件，[虚功](@entry_id:176403)方程中的积分（特别是包含导数的内力[虚功](@entry_id:176403)）必须是有意义的。这要求位移场及其导数具有一定的“正则性”。在数学上，仅仅要求函数连续可导（$C^1$空间）过于严格，会排除许多物理上有意义的解（例如有限元法中的分片多项式解）。能够确保[能量积分](@entry_id:166228)有限的“最弱”条件是函数本身及其一阶[弱导数](@entry_id:189356)都属于[平方可积函数](@entry_id:200316)空间 $L^2$。满足此条件的函数构成了**[索博列夫空间](@entry_id:141995)（Sobolev space）** $H^1(\Omega)$。

综合以上两点，运动学容许的[虚位移](@entry_id:168781)场 $\delta\boldsymbol{u}$ 构成的**检验函数空间（test function space）** $\mathcal{V}$，在数学上被精确地定义为：

$$
\mathcal{V} = \{ \boldsymbol{v} \in [H^1(\Omega)]^d \mid \boldsymbol{v} = \boldsymbol{0} \text{ on } \Gamma_u \}
$$

这里，边界条件是在迹的意义下（in the sense of traces）满足的，这是索博列夫空间理论中的一个标准概念。相应地，待求解的真实[位移场](@entry_id:141476) $\boldsymbol{u}$ 属于一个[仿射空间](@entry_id:152906)，即某个满足[非齐次边界条件](@entry_id:750645) $\boldsymbol{u}|_{\Gamma_u} = \bar{\boldsymbol{u}}$ 的特定函数 $\boldsymbol{u}_g$ 与上述[向量空间](@entry_id:151108) $\mathcal{V}$ 的和集。[@problem_id:2676267]

### 弱形式及其与强形式的关系

综合以上所有要素，我们可以写出[虚功原理](@entry_id:138749)的完整数学形式，这被称为问题的**[弱形式](@entry_id:142897)（weak form）**或**[变分形式](@entry_id:166033)（variational form）**：

寻找位移场 $\boldsymbol{u}$（满足 $\boldsymbol{u}|_{\Gamma_u} = \bar{\boldsymbol{u}}$），使得对于**所有**容许的[虚位移](@entry_id:168781) $\delta\boldsymbol{u} \in \mathcal{V}$，下式成立：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\delta\boldsymbol{u}) \, \mathrm{d}V = \int_{\Omega} \boldsymbol{b} \cdot \delta\boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta\boldsymbol{u} \, \mathrm{d}A
$$

这个积分方程与我们最初用[微分方程](@entry_id:264184)和边界条件描述的**强形式（strong form）**问题是等价的（在一定正则性假设下）。这种等价性是变分方法的基石。

#### 从强形式到[弱形式](@entry_id:142897)
我们实际上已经完成了这个推导。从平衡[微分方程](@entry_id:264184) $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$ 出发，乘以[检验函数](@entry_id:166589) $\delta\boldsymbol{u}$ 并分部积分，利用边界条件 $\boldsymbol{\sigma}\cdot\boldsymbol{n}|_{\Gamma_t} = \bar{\boldsymbol{t}}$ 和 $\delta\boldsymbol{u}|_{\Gamma_u} = \boldsymbol{0}$，即可得到上述弱形式。

#### 从[弱形式](@entry_id:142897)到强形式
反向的推导更能体现弱形式的威力。假设我们有一个满足[弱形式](@entry_id:142897)的解 $\boldsymbol{u}$，我们可以通过巧妙地[选择检验](@entry_id:182706)函数 $\delta\boldsymbol{u}$ 来恢复强形式。

首先，对弱形式的左侧进行[分部积分](@entry_id:136350)（利用[高斯散度定理](@entry_id:188065)）：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\delta\boldsymbol{u}) \, \mathrm{d}V = - \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}(\boldsymbol{u})) \cdot \delta\boldsymbol{u} \, \mathrm{d}V + \int_{\partial\Omega} (\boldsymbol{\sigma}(\boldsymbol{u})\cdot\boldsymbol{n}) \cdot \delta\boldsymbol{u} \, \mathrm{d}A
$$
代入弱形式方程并整理，可得：
$$
-\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b}) \cdot \delta\boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} (\boldsymbol{\sigma}\cdot\boldsymbol{n} - \bar{\boldsymbol{t}}) \cdot \delta\boldsymbol{u} \, \mathrm{d}A = 0
$$
这个方程必须对所有容许的 $\delta\boldsymbol{u}$ 成立。

1.  **恢复[平衡方程](@entry_id:172166)**：我们首先选择一类特殊的检验函数，它们在区域 $\Omega$ 内部是任意的，但在整个边界 $\partial\Omega$ 上都为零（即具有[紧支集](@entry_id:276214)）。对于这[类函数](@entry_id:146970)，边界积分项自动消失，方程简化为：
    $$
    \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b}) \cdot \delta\boldsymbol{u} \, \mathrm{d}V = 0
    $$
    根据**[变分法](@entry_id:163656)基本引理（Fundamental Lemma of Calculus of Variations）**，如果这个积分对在 $\Omega$ 内部任意选择的 $\delta\boldsymbol{u}$ 都成立，那么括号内的被积函数本身必须处处为零。这就恢复了平衡[微分方程](@entry_id:264184)：$\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$。[@problem_id:2676305]

2.  **恢复自然边界条件**：既然[平衡方程](@entry_id:172166)在区域内部必须成立，那么对于任意的 $\delta\boldsymbol{u}$，体积积分项就恒为零了。剩下的方程是：
    $$
    \int_{\Gamma_t} (\boldsymbol{\sigma}\cdot\boldsymbol{n} - \bar{\boldsymbol{t}}) \cdot \delta\boldsymbol{u} \, \mathrm{d}A = 0
    $$
    现在，这个方程必须对在 $\Gamma_t$ 上任意取值的检验函数 $\delta\boldsymbol{u}$ 成立。再次应用变分法基本引理（这次是在[曲面](@entry_id:267450) $\Gamma_t$ 上），我们得到括号内的项必须在 $\Gamma_t$ 上处处为零。这就恢复了**自然边界条件（natural boundary condition）**：$\boldsymbol{\sigma}\cdot\boldsymbol{n} = \bar{\boldsymbol{t}}$。[@problem_id:2676331]

这个推导过程完美地揭示了两种边界条件在变分框架下的本质区别：
- **[本质边界条件](@entry_id:173524)**（[位移边界条件](@entry_id:203261)）：必须预先施加于求解空间和检验函数空间，是[变分问题](@entry_id:756445)的“输入”。
- **自然边界条件**（力边界条件）：作为[变分方程](@entry_id:635018)求解的结果而“自然”满足，是[变分问题](@entry_id:756445)的“输出”。

### 高级主题与扩展

虚功原理的框架具有极强的普适性，可以自然地扩展到更复杂的物理情境。

#### [非线性力学](@entry_id:178303)中的应用

当处理[大变形](@entry_id:167243)问题时，必须区分参考构型和当前构型。虚功原理依然适用，但其表达式需要推广。此时，通常使用**[虚功](@entry_id:176403)率原理（Principle of Virtual Power）**，它与[虚功原理](@entry_id:138749)本质相同，只是将[虚位移](@entry_id:168781)替换为虚速度。

在[大变形](@entry_id:167243)框架下，存在多种[应力张量和应变张量](@entry_id:755512)的定义，它们与不同的构型相关联。重要的[功共轭](@entry_id:194957)对包括 [@problem_id:2676350]：
1.  **Cauchy应力** $\boldsymbol{\sigma}$ 与 **变形率张量** $\boldsymbol{d}$：这是在**当前构型**下最自然的能量率表达。[内力](@entry_id:167605)[虚功](@entry_id:176403)率为 $\delta P_{\text{int}} = \int_{\Omega} \boldsymbol{\sigma} : \delta\boldsymbol{d} \, dv$。
2.  **第一Piola-Kirchhoff (PK1)应力** $\boldsymbol{P}$ 与 **变形梯度率** $\dot{\boldsymbol{F}}$：这是混合度量，将参考构型上的力与变形梯度的变化率联系起来。[内力](@entry_id:167605)[虚功](@entry_id:176403)率为 $\delta P_{\text{int}} = \int_{\Omega_0} \boldsymbol{P} : \delta\dot{\boldsymbol{F}} \, dV$。
3.  **第二Piola-Kirchhoff (PK2)应力** $\boldsymbol{S}$ 与 **[Green-Lagrange应变](@entry_id:170427)率** $\dot{\boldsymbol{E}}$：这完全是在**参考构型**下描述能量率。[内力](@entry_id:167605)[虚功](@entry_id:176403)率为 $\delta P_{\text{int}} = \int_{\Omega_0} \boldsymbol{S} : \delta\dot{\boldsymbol{E}} \, dV$。

这三种表达方式通过运动学和应力度量之间的转换关系是完全等价的。它们在理论分析和数值计算中各有优势。

#### 载荷类型与势能

在[虚功原理](@entry_id:138749)的框架下，外力的性质对问题的数学结构有重要影响。我们可以区分以下几类载荷 [@problem_id:2676327]：
- **固载（Dead loads）**：载荷的大小和方向在空间中是固定的，不随物体的变形而改变。例如，重力。
- **活载（Live loads）**：载荷的大小或[分布](@entry_id:182848)可能随时间等外部参数变化，但在任一瞬间，其性质类似于固载。
- **随动载荷（Follower loads）**：载荷的大小或方向依赖于物体的当前构型。例如，始终垂直于变形后表面的压力。

如果一个载荷系统所做的[虚功](@entry_id:176403)可以表示为某个标量函数（载荷势 $\Lambda(\boldsymbol{u})$）的变分，即 $\delta W_{\text{ext}} = \delta \Lambda$，那么该载荷系统是**保守的（conservative）**。对于固载和活载，总可以找到这样的载荷势。对于保守载荷系统，[虚功原理](@entry_id:138749) $\delta W_{\text{int}} = \delta W_{\text{ext}}$ 可以与材料的[应变能势](@entry_id:755493) $\mathcal{U}$（对于[超弹性材料](@entry_id:190241)）结合，写成**总势能最小原理**：$\delta \Pi = \delta(\mathcal{U} - \Lambda) = 0$。

随动载荷通常是非保守的。一个重要的后果是，当对[非线性](@entry_id:637147)问题进行线性化以获得[切线刚度](@entry_id:166213)算子时，保守载荷贡献的[几何刚度](@entry_id:172820)部分是对称的，而**非保守随动载荷通常会导致非对称的[切线刚度矩阵](@entry_id:170852)**。这对于结构的[稳定性分析](@entry_id:144077)至关重要，因为它可能导致动态失稳（如颤振），而非静态[屈曲](@entry_id:162815)。一个重要的例外是**[静水压力](@entry_id:275365)**，尽管它是一种随动载荷（始终垂直于当前表面），但它恰好是保守的，其载荷势与物体体积的变化成正比。

### 严谨的数学表述

最后，我们可以将[线性弹性](@entry_id:166983)问题的虚功原理表述为抽象的[变分问题](@entry_id:756445)，这正是现代[偏微分方程理论](@entry_id:189232)和有限元分析的出发点 [@problem_id:2676354]。

令 $\mathcal{V} = H^1_{\Gamma_u}(\Omega)^n$ 为[检验函数](@entry_id:166589)空间，解 $\boldsymbol{u}$ 属于[仿射空间](@entry_id:152906) $\boldsymbol{u}_g + \mathcal{V}$。我们定义：
- **[双线性形式](@entry_id:746794)** $a(\cdot, \cdot)$，代表[内力](@entry_id:167605)[虚功](@entry_id:176403)：
  $$
  a(\boldsymbol{u}, \boldsymbol{v}) = \int_{\Omega} \boldsymbol{\varepsilon}(\boldsymbol{u}) : \mathbb{C} : \boldsymbol{\varepsilon}(\boldsymbol{v}) \, \mathrm{d}x
  $$
- **线性泛函** $\ell(\cdot)$，代表外力[虚功](@entry_id:176403)：
  $$
  \ell(\boldsymbol{v}) = \int_{\Omega} \boldsymbol{f} \cdot \boldsymbol{v} \, \mathrm{d}x + \langle \bar{\boldsymbol{t}}, \boldsymbol{v} \rangle_{\Gamma_t}
  $$
  其中 $\langle \cdot, \cdot \rangle_{\Gamma_t}$ 表示在边界 $\Gamma_t$ 上的对偶作用，以处理正则性较低的力边界数据。

那么，整个弹性力学问题可以简洁地表述为：寻找 $\boldsymbol{u} \in \boldsymbol{u}_g + \mathcal{V}$，使得对于所有 $\boldsymbol{v} \in \mathcal{V}$，有：

$$
a(\boldsymbol{u}, \boldsymbol{v}) = \ell(\boldsymbol{v})
$$

这个抽象形式不仅优雅，而且功能强大。利用泛函分析中的[Lax-Milgram定理](@entry_id:137966)，可以基于双线性形式 $a(\cdot, \cdot)$ 的性质（如连续性和强制性/椭圆性）来证明解的存在性和唯一性。此外，这个形式直接导出了[有限元法](@entry_id:749389)的离散化方案，即将无限维的函数空间 $\mathcal{V}$ 近似为有限维的[子空间](@entry_id:150286)。