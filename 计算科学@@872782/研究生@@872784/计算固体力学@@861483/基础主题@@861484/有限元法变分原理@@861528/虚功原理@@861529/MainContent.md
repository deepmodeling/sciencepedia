## 引言
[虚功](@entry_id:176403)原理是连接经典力学理论与现代计算方法的关键桥梁，在[计算固体力学](@entry_id:169583)领域占据着核心地位。工程师和研究人员在面对复杂结构时，往往难以直接求解描述其物理行为的[偏微分方程](@entry_id:141332)（即“强形式”）。[虚功](@entry_id:176403)原理通过将这些方程转化为等效的积分形式（“弱形式”），不仅极大地简化了数学上的求解难度，更为[有限元法](@entry_id:749389)等强大的数值技术奠定了坚实的理论基础。本文旨在系统性地阐述[虚功](@entry_id:176403)原理的内涵与外延。在“原理与机制”一章中，我们将从[虚位移](@entry_id:168781)等基本概念出发，深入推导其在不同力学情境下的数学表述。接着，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将展示该原理如何被应用于构建有限元模型、分析[非线性](@entry_id:637147)行为，并与[材料科学](@entry_id:152226)、[多物理场耦合](@entry_id:171389)等领域产生深刻联系。最后，通过“动手实践”部分，读者将有机会亲手推导与[虚功](@entry_id:176403)原理相关的关键方程，从而将理论知识转化为解决实际问题的能力。让我们首先进入第一章，探索[虚功](@entry_id:176403)原理的理论核心。

## 原理与机制

本章旨在深入探讨[虚功](@entry_id:176403)原理的理论基础与核心机制。作为连接固体力学中平衡方程的“强形式”与计算方法中积分“[弱形式](@entry_id:142897)”的关键桥梁，[虚功](@entry_id:176403)原理不仅是一种强大的理论工具，更是[有限元法](@entry_id:749389)等数值技术赖以建立的基石。我们将从[虚功](@entry_id:176403)原理的基本定义出发，系统地推导其在小应变和有限变形下的数学表述，阐明其与变分原理的关系，并最终探讨其在现代计算力学高级理论中的扩展。

### 基本概念：[虚位移](@entry_id:168781)与[运动学](@entry_id:173318)许可

在固体力学中，一个物体的平衡状态通常由一组[偏微分方程](@entry_id:141332)（即[平衡方程](@entry_id:172166)）及其边界条件来描述。这种表述形式被称为“强形式”，因为它要求在物体内的每一点上，这些方程都必须精确满足。然而，直接求解强形式在数学上可能非常困难，尤其对于复杂的几何形状和材料行为。[虚功](@entry_id:176403)原理提供了一种等效的、基于积分的“[弱形式](@entry_id:142897)”表述，它放宽了对解的连续性要求，并为[数值离散化](@entry_id:752782)铺平了道路。

弱形式的核心思想在于，不再要求平衡方程在每一点都为零，而是要求其在与一个任意的、满足特定条件的“权函数”相乘并在整个求解域上积分后结果为零。在力学中，这个权函数具有明确的物理意义，即 **[虚位移](@entry_id:168781)**。

#### [虚位移](@entry_id:168781)与真实位移的辨析

理解[虚功](@entry_id:176403)原理的第一步，是精确区分 **真实位移** $u$ 与 **[虚位移](@entry_id:168781)** $\delta u$。

-   **真实位移** $u(\boldsymbol{x})$ 是物体在外载荷和边界约束下产生的物理响应。它是一个待求解的未知场，其最终形式由材料的[本构关系](@entry_id:186508)、[平衡方程](@entry_id:172166)和所有边界条件唯一确定（在[适定问题](@entry_id:176268)中）。真实位移是物理世界中实际发生的变形。

-   **[虚位移](@entry_id:168781)** $\delta u(\boldsymbol{x})$ 则是一个纯粹的数学和概念工具。它并不代表任何物理上实际发生的运动，也与时间或载荷的增量无关。它是一个想象中的、无穷小的、施加于物体已平衡构型上的任意扰动。在数学上，它扮演着一个 **检验函数 (test function)** 的角色，用以“检验”真实应[力场](@entry_id:147325)是否满足平衡状态。[@problem_id:3591306]

[虚位移](@entry_id:168781)的关键特性是它的 **任意性** 和 **[运动学](@entry_id:173318)许可** 性。

#### [运动学](@entry_id:173318)许可条件

**[运动学](@entry_id:173318)许可 (Kinematically Admissible)** 是对[虚位移](@entry_id:168781)场的关键约束。它要求[虚位移](@entry_id:168781)必须与系统的几何约束相容。在固体力学中，最常见的几何约束是[位移边界条件](@entry_id:203261)，也称为 **本质边界条件 (Essential Boundary Conditions)** 或狄利克雷 (Dirichlet) 边界条件。

考虑一个物体，其边界 $\partial \Omega$ 的一部分 $\Gamma_u$ 上被施加了已知的位移 $\bar{\boldsymbol{u}}$。真实[位移场](@entry_id:141476) $u$ 必须在 $\Gamma_u$ 上满足 $u = \bar{\boldsymbol{u}}$。现在，我们考虑一个与真实解 $u$ “邻近”的[运动学](@entry_id:173318)许可位移场 $u + \delta u$。为了使这个新的位移场仍然是运动学许可的，它也必须满足相同的本质边界条件，即在 $\Gamma_u$ 上有 $u + \delta u = \bar{\boldsymbol{u}}$。由于 $u$ 本身已经满足 $u = \bar{\boldsymbol{u}}$，上述条件立即简化为：
$$
\delta u = \boldsymbol{0} \quad \text{在 } \Gamma_u \text{ 上}
$$
这个结论至关重要：**任何[运动学](@entry_id:173318)许可的[虚位移](@entry_id:168781)场，在施加了本质边界条件（位移约束）的边界部分必须为零。**[@problem_id:3591331]

从[变分学](@entry_id:197464)的角度看，所有满足本质边界条件的真实[位移场](@entry_id:141476)构成了一个[仿射空间](@entry_id:152906)（或[流形](@entry_id:153038)）。[虚位移](@entry_id:168781)场则属于该空间在真实解 $u$ 处的 **[切空间](@entry_id:199137) (tangent space)**。由于[本质边界条件](@entry_id:173524)的值 $\bar{\boldsymbol{u}}$ 是固定的，其变分为零，因此[切空间](@entry_id:199137)中的任何向量（即[虚位移](@entry_id:168781)）在 $\Gamma_u$ 上都必须为零。[@problem_id:3591331]

### 小应变弹性力学的[虚功](@entry_id:176403)原理

掌握了[虚位移](@entry_id:168781)的概念后，我们可以从[平衡方程](@entry_id:172166)的强形式出发，推导小应变弹性力学中的[虚功](@entry_id:176403)原理。

#### 从强形式到弱形式的推导

对于一个处于准静态平衡状态的物体，其内部任意点的[平衡方程](@entry_id:172166)为：
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0} \quad \text{在 } \Omega \text{ 内}
$$
其中 $\boldsymbol{\sigma}$ 是柯西 (Cauchy) 应力张量，$\boldsymbol{b}$ 是单位体积的[体力](@entry_id:174230)。

根据[弱形式](@entry_id:142897)的思想，我们将此方程与一个任意的运动学许可[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 做[点积](@entry_id:149019)，并在整个体积 $\Omega$ 上积分：
$$
\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V = 0
$$
$$
\int_{\Omega} (\nabla \cdot \boldsymbol{\sigma}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V = 0
$$
这里的关键一步是利用 **分部积分**（即[高斯散度定理](@entry_id:188065)）来处理第一项，目的是将微分算子从应[力场](@entry_id:147325) $\boldsymbol{\sigma}$（其连续性可能较低）转移到更光滑的[虚位移](@entry_id:168781)场 $\delta \boldsymbol{u}$ 上。利用张量恒等式 $(\nabla \cdot \boldsymbol{\sigma}) \cdot \delta \boldsymbol{u} = \nabla \cdot (\boldsymbol{\sigma}^T \delta \boldsymbol{u}) - \boldsymbol{\sigma} : \nabla(\delta \boldsymbol{u})$，并应用[散度定理](@entry_id:143110)，我们得到：
$$
\int_{\partial \Omega} (\boldsymbol{\sigma} \boldsymbol{n}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A - \int_{\Omega} \boldsymbol{\sigma} : \nabla(\delta \boldsymbol{u}) \, \mathrm{d}V + \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V = 0
$$
其中 $\boldsymbol{n}$ 是边界 $\partial \Omega$ 的外法向[单位向量](@entry_id:165907)。

#### [内虚功](@entry_id:172278)与外[虚功](@entry_id:176403)

上式可以整理为一种更具物理意义的形式。首先，我们定义在边界上的 **牵[引力](@entry_id:175476) (traction)** 向量为 $\boldsymbol{t} = \boldsymbol{\sigma} \boldsymbol{n}$。其次，对于小应变问题，我们假设[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 是对称的。因此，它与虚[位移梯度](@entry_id:165352) $\nabla(\delta \boldsymbol{u})$ 的[双点积](@entry_id:748648)可以简化。任何一个[二阶张量](@entry_id:199780)都可以分解为其对称[部分和](@entry_id:162077)反对称部分。虚应变张量 $\delta \boldsymbol{\varepsilon}$ 定义为虚[位移梯度](@entry_id:165352)的对称部分：$\delta \boldsymbol{\varepsilon} = \frac{1}{2}(\nabla(\delta \boldsymbol{u}) + (\nabla(\delta \boldsymbol{u}))^T)$。由于[对称张量与反对称张量](@entry_id:194720)的[双点积](@entry_id:748648)为零，我们有：
$$
\boldsymbol{\sigma} : \nabla(\delta \boldsymbol{u}) = \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon}
$$
将这些关系代入并重新整理，得到：
$$
\underbrace{\int_{\Omega} \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon} \, \mathrm{d}V}_{\delta W_{\text{int}}} = \underbrace{\int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\partial \Omega} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A}_{\delta W_{\text{ext}}}
$$
这就是 **[虚功](@entry_id:176403)原理** 的经典表述：对于任意[运动学](@entry_id:173318)许可的[虚位移](@entry_id:168781)，**[内虚功](@entry_id:172278)** 等于 **外[虚功](@entry_id:176403)**。

-   **[内虚功](@entry_id:172278)** $\delta W_{\text{int}}$ 是内部应力 $\boldsymbol{\sigma}$ 在虚应变 $\delta \boldsymbol{\varepsilon}$ 上所做的功。
-   **外[虚功](@entry_id:176403)** $\delta W_{\text{ext}}$ 是外部载荷（体力 $\boldsymbol{b}$ 和边界牵[引力](@entry_id:175476) $\boldsymbol{t}$）在[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 上所做的功。

这个等式揭示了力与位移之间的 **[功共轭](@entry_id:194957) (work-conjugate)** 关系。柯西应力 $\boldsymbol{\sigma}$ 与小应变 $\boldsymbol{\varepsilon}$ 是一对[功共轭](@entry_id:194957)量。类似地，体力 $\boldsymbol{b}$ 和牵[引力](@entry_id:175476) $\boldsymbol{t}$ 都与位移 $\boldsymbol{u}$ [功共轭](@entry_id:194957)。[@problem_id:3591313]

#### [本质边界条件与自然边界条件](@entry_id:146051)

现在我们来考察边界积分项 $\int_{\partial \Omega} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A$。物体的边界 $\partial \Omega$ 通常被划分为两部分：施加位移约束的本质边界 $\Gamma_u$ 和施加力约束的 **自然边界 (Natural Boundary Conditions)** $\Gamma_t$。
$$
\int_{\partial \Omega} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A = \int_{\Gamma_u} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A + \int_{\Gamma_t} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$
-   在本质边界 $\Gamma_u$ 上，根据运动学许可条件，我们强制要求 $\delta \boldsymbol{u} = \boldsymbol{0}$。这使得第一项积分恒为零：$\int_{\Gamma_u} \boldsymbol{t} \cdot \delta \boldsymbol{u} \, \mathrm{d}A = 0$。这意味着，我们通过限制[虚位移](@entry_id:168781)的函数空间，“强行”满足了本质边界条件。这部分边界上的未知反力 $\boldsymbol{t}$ 也因此不做[虚功](@entry_id:176403)，从而被消除了。
-   在自然边界 $\Gamma_t$ 上，[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$ 是任意的，而牵[引力](@entry_id:175476) $\boldsymbol{t}$ 是已知的 prescribed traction $\bar{\boldsymbol{t}}$。因此，这部分积分成为外[虚功](@entry_id:176403)的一部分：$\int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A$。

最终，[虚功](@entry_id:176403)原理的完整形式为：寻找满足 $u = \bar{\boldsymbol{u}}$ on $\Gamma_u$ 的位移场 $u$，使得对于所有满足 $\delta \boldsymbol{u} = \boldsymbol{0}$ on $\Gamma_u$ 的[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$，下式成立：
$$
\int_{\Omega} \boldsymbol{\sigma}(\boldsymbol{u}) : \boldsymbol{\varepsilon}(\delta \boldsymbol{u}) \, \mathrm{d}V = \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$
这个过程清晰地解释了为何两类边界条件在[弱形式](@entry_id:142897)中有如此不同的处理方式。[本质边界条件](@entry_id:173524)通过对[试探函数](@entry_id:756165)空间和检验函数空间的约束来满足；而自然边界条件则“自然地”出现在[变分方程](@entry_id:635018)的边界积分项中，并通过方程本身得到满足。[@problem_id:3591310]

### 数学基础与推广

#### 函数空间与正则性要求

[虚功](@entry_id:176403)原理的数学严谨性要求我们明确解和[虚位移](@entry_id:168781)所属的[函数空间](@entry_id:143478)。为了使[内虚功](@entry_id:172278)积分 $\int_{\Omega} \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon} \, \mathrm{d}V$ 有意义，我们需要[应变能](@entry_id:162699)是有限的。对于线性弹性材料，$\boldsymbol{\sigma} = \mathsf{C} : \boldsymbol{\varepsilon}$，[应变能密度](@entry_id:200085)与应变的平方成正比。因此，积分 $\int_{\Omega} (\boldsymbol{\varepsilon}(\boldsymbol{u}))^2 \, \mathrm{d}V$ 必须是有限的。这要求位移场的[一阶导数](@entry_id:749425)是平方可积的。满足这一条件的函数空间正是 **索伯列夫空间 (Sobolev space)** $H^1(\Omega)$。

因此，真实位移 $u$ 的求[解空间](@entry_id:200470)（[试探空间](@entry_id:756166)）和[虚位移](@entry_id:168781) $\delta u$ 的[函数空间](@entry_id:143478)（检验空间）都必须是 $[H^1(\Omega)]^d$ 的[子空间](@entry_id:150286)。具体而言：
-   [试探空间](@entry_id:756166) $\mathcal{S} = \{ \boldsymbol{w} \in [H^1(\Omega)]^d \mid \boldsymbol{w} = \bar{\boldsymbol{u}} \text{ 在 } \Gamma_u \text{ 上} \}$
-   检验空间 $\mathcal{V} = \{ \boldsymbol{w} \in [H^1(\Omega)]^d \mid \boldsymbol{w} = \boldsymbol{0} \text{ 在 } \Gamma_u \text{ 上} \}$

选择 $H^1$ 空间既保证了[应变能](@entry_id:162699)积分的良定义性，也通过[迹定理](@entry_id:203967) (Trace Theorem) 保证了位移在边界上的值（以及边界积分项）是良定义的。[@problem_id:3591273]

为了更直观地理解[虚功](@entry_id:176403)原理的普适性，我们可以考虑一个简单的标量模型，如泊松 (Poisson) 方程 $-\Delta u = f$。通过乘以检验函数 $v$ 并分部积分，我们得到其[弱形式](@entry_id:142897)：$\int_{\Omega} \nabla u \cdot \nabla v \, \mathrm{d}\Omega = \int_{\Omega} f v \, \mathrm{d}\Omega$ (假设[齐次边界条件](@entry_id:750371))。这个方程可以类比于[虚功](@entry_id:176403)原理：左侧的 $\int \nabla u \cdot \nabla v$ 如同“[内虚功](@entry_id:172278)”（内部通量与虚梯度的作用），右侧的 $\int fv$ 如同“外[虚功](@entry_id:176403)”（源项与[虚位移](@entry_id:168781)的作用）。这种类比有助于我们将[虚功](@entry_id:176403)原理看作是更广泛的[加权余量法](@entry_id:165159) (Weighted Residual Method) 在力学中的具体体现。[@problem_id:3223744]

#### 动力学扩展：[达朗贝尔原理](@entry_id:166612)

[虚功](@entry_id:176403)原理可以很容易地推广到动力学问题。根据[牛顿第二定律](@entry_id:274217)，平衡方程变为：
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \rho \ddot{\boldsymbol{u}}
$$
其中 $\rho$ 是密度，$\ddot{\boldsymbol{u}}$ 是加速度。

**达朗贝尔 (D'Alembert) 原理** 提供了一个巧妙的视角：将动力学问题转化为“动态平衡”问题。它将惯性项 $\rho \ddot{\boldsymbol{u}}$ 移到方程左边，并视其为一种“[惯性力](@entry_id:169104)”密度 $-\rho \ddot{\boldsymbol{u}}$。
$$
\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} - \rho \ddot{\boldsymbol{u}} = \boldsymbol{0}
$$
现在，这个方程的形式与静态[平衡方程](@entry_id:172166)完全相同，只是多了一个“[体力](@entry_id:174230)”项。应用与静态情况完全相同的[虚功](@entry_id:176403)推导过程，我们只需在原来的外[虚功](@entry_id:176403)中增加惯性力所做的功：
$$
\delta W_{\text{int}} = \delta W_{\text{ext}} + \delta W_{\text{inertia}}
$$
$$
\int_{\Omega} \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon} \, \mathrm{d}V = \int_{\Omega} \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A - \int_{\Omega} \rho \ddot{\boldsymbol{u}} \cdot \delta \boldsymbol{u} \, \mathrm{d}V
$$
惯性项的负号源于它在[平衡方程](@entry_id:172166)中的形式。这个方程是动力学分析中，特别是瞬态动力学有限元分析的出发点。[@problem_id:2676317]

### 与变分原理的关系

对于由保守力系统（即存在势能函数）构成的弹性体，[虚功](@entry_id:176403)原理与 **[最小势能原理](@entry_id:173340) (Principle of Minimum Potential Energy, MPE)** 密切相关。

#### 势能泛函的驻值

一个弹性系统的 **总[势能](@entry_id:748988)** $\Pi$ 定义为内能（应变能）$U$ 与外力[势能](@entry_id:748988) $W_{\text{pot}}$之和，通常写作 $U$ 减去外力所做的功 $W_{\text{ext}}$：
$$
\Pi[\boldsymbol{u}] = U[\boldsymbol{u}] - W_{\text{ext}}[\boldsymbol{u}] = \int_{\Omega} \psi(\boldsymbol{\varepsilon}(\boldsymbol{u})) \, \mathrm{d}V - \left( \int_{\Omega} \boldsymbol{b} \cdot \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} \bar{\boldsymbol{t}} \cdot \boldsymbol{u} \, \mathrm{d}A \right)
$$
其中 $\psi$ 是[应变能密度函数](@entry_id:755490)。

变分原理指出，在所有[运动学](@entry_id:173318)许可的位移场中，真实的平衡位移场 $u$ 使得总[势能](@entry_id:748988)泛函 $\Pi$ 取 **驻值 (stationary value)**。驻值条件意味着 $\Pi$ 的一阶变分 $\delta \Pi$ 为零：
$$
\delta \Pi = \delta U - \delta W_{\text{ext}} = 0
$$
通过计算，可以证明 $\delta U = \int \boldsymbol{\sigma} : \delta \boldsymbol{\varepsilon} \, \mathrm{d}V = \delta W_{\text{int}}$，且 $\delta W_{\text{ext}} = \int \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A$。因此，驻值条件 $\delta \Pi = 0$ 与[虚功](@entry_id:176403)原理 $\delta W_{\text{int}} = \delta W_{\text{ext}}$ 是完[全等](@entry_id:273198)价的。[@problem_id:3223744]

#### [平衡与稳定性](@entry_id:175068)：[虚功](@entry_id:176403)原理 vs. [最小势能原理](@entry_id:173340)

尽管数学上等价，[虚功](@entry_id:176403)原理和[最小势能原理](@entry_id:173340)在物理概念上存在细微但重要的差别。
-   **[虚功](@entry_id:176403)原理 (PVW)** 是平衡的陈述。它寻找的是势能泛函的所有[驻点](@entry_id:136617)（包括极小值点、极大值点和[鞍点](@entry_id:142576)）。
-   **[最小势能原理](@entry_id:173340) (MPE)** 是稳定性的陈述。它指出，只有当平衡构型对应于势能的 **局部最小值** 时，该平衡才是稳定的。

这意味着MPE是一个比PVW更强的条件。稳定性不仅要求一阶变分 $\delta \Pi = 0$，还要求二阶变分 $\delta^2 \Pi$ 是正定的。在某些情况下，一个系统可以处于平衡状态（满足PVW），但该平衡是不稳定的。

一个典型的例子是具有非凸[应变能函数](@entry_id:178435) $\psi(\varepsilon)$ 的材料。例如，考虑一个一维杆，其[应变能密度](@entry_id:200085)为 $\psi(\varepsilon) = \frac{1}{2} E \varepsilon^{2} - \frac{1}{4} \beta \varepsilon^{4}$（其中 $E, \beta > 0$）。其[切线](@entry_id:268870)模量为 $C_t(\varepsilon) = \frac{d^2\psi}{d\varepsilon^2} = E - 3\beta\varepsilon^2$。当应变 $\bar{\varepsilon}$ 足够大，使得 $E - 3\beta\bar{\varepsilon}^2  0$ 时，尽管该状态可能是一个[平衡点](@entry_id:272705)（满足 $\delta \Pi = 0$），但其二阶变分 $\delta^2 \Pi$ 将为负，表明这是一个不稳定的[平衡点](@entry_id:272705)（势能的极大值或[鞍点](@entry_id:142576)）。这种现象称为 **材料失稳**。因此，PVW找到了所有可能的[平衡解](@entry_id:174651)，而[稳定性分析](@entry_id:144077)（基于MPE）则用于判断哪个解是物理上可实现的。[@problem_id:3591282]

### 有限变形下的[虚功](@entry_id:176403)原理

当变形较大时，必须考虑[几何非线性](@entry_id:169896)。这要求我们在描述运动和力时，区分 **参考构型 (Reference Configuration)** $\Omega_0$ 和 **当前构型 (Current Configuration)** $\Omega_t$。由此产生了两种主要的分析框架：总拉格朗日 (Total Lagrangian, TL) 和更新拉格朗日 (Updated Lagrangian, UL) 构型。

#### 总拉格朗日 (TL) 构型

TL构型将所有物理量都映射回初始的、未变形的参考构型 $\Omega_0$ 上进行描述。推导从当前构型下的PVW出发，通过一系列[坐标变换](@entry_id:172727)和变量代换完成。

关键的运动学量是 **变形梯度 (Deformation Gradient)** $\boldsymbol{F} = \nabla_0 \boldsymbol{x}$，它将参考构型中的向量映射到当前构型。与之相关的[应变度量](@entry_id:755495)是 **格林-拉格朗日 (Green-Lagrange) [应变张量](@entry_id:193332)** $\boldsymbol{E} = \frac{1}{2}(\boldsymbol{F}^T \boldsymbol{F} - \boldsymbol{I})$。与 $\boldsymbol{E}$ [功共轭](@entry_id:194957)的应力度量是 **第二类皮奥拉-基尔霍夫 (Second Piola-Kirchhoff, PK2) [应力张量](@entry_id:148973)** $\boldsymbol{S}$。

通过复杂的推导，可以证明当前构型中的[内虚功](@entry_id:172278) $\int_{\Omega_t} \boldsymbol{\sigma} : \delta\boldsymbol{d} \, \mathrm{d}V$ 等价于参考构型中的：
$$
\delta W_{\text{int}} = \int_{\Omega_0} \boldsymbol{S} : \delta \boldsymbol{E} \, \mathrm{d}\Omega_0
$$
其中 $\delta \boldsymbol{E} = \text{sym}(\boldsymbol{F}^T \nabla_0 \delta \boldsymbol{U})$ 是[格林-拉格朗日应变](@entry_id:170427)的变分。外部载荷也需要转换到参考构型，包括参考构型下的[体力](@entry_id:174230) $\boldsymbol{B}_0$ 和 **名义牵[引力](@entry_id:175476) (Nominal Traction)** $\boldsymbol{T}_0$。最终，TL形式的[虚功](@entry_id:176403)原理写作：
$$
\int_{\Omega_0} \boldsymbol{S} : \delta \boldsymbol{E} \, \mathrm{d}\Omega_0 = \int_{\Omega_0} \boldsymbol{B}_0 \cdot \delta \boldsymbol{U} \, \mathrm{d}\Omega_0 + \int_{\Gamma_{0t}} \boldsymbol{T}_0 \cdot \delta \boldsymbol{U} \, \mathrm{d}\Gamma_0
$$
这种形式的优点是积分域始终是固定的初始构型 $\Omega_0$，从而简化了数值实现。[@problem_id:3591287]

#### 更新拉格朗日 (UL) 构型

UL构型则选择在每个时间（或载荷）步结束时的当前构型 $\Omega_t$ 作为计算的参考。因此，其形式与小应变理论中的PVW非常相似，但所有量都是在当前构型下定义的。
$$
\int_{\Omega_t} \boldsymbol{\sigma} : \delta \boldsymbol{d} \, \mathrm{d}V = \int_{\Omega_t} \rho \boldsymbol{b} \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\partial \Omega_t^t} \bar{\boldsymbol{t}} \cdot \delta \boldsymbol{u} \, \mathrm{d}A
$$
这里的 $\boldsymbol{\sigma}$ 是柯西应力（真实应力），$\delta \boldsymbol{u}$ 是空间[虚位移](@entry_id:168781)，而 $\delta \boldsymbol{d}$ 是[虚位移](@entry_id:168781)在当前构型下的对称梯度，即 **虚变形率张量** $\delta \boldsymbol{d} = \frac{1}{2}(\nabla_{\boldsymbol{x}} \delta \boldsymbol{u} + (\nabla_{\boldsymbol{x}} \delta \boldsymbol{u})^T)$。[功共轭](@entry_id:194957)对应力-应变率对是 $(\boldsymbol{\sigma}, \boldsymbol{d})$。UL方法的挑战在于积分域 $\Omega_t$ 随变形而改变，需要在计算中不断更新。[@problem_id:2609717]

### 高级论题：[混合变分原理](@entry_id:165106)

标准的、基于位移的[虚功](@entry_id:176403)原理在某些情况下会遇到困难，例如在模拟不可压缩或[近不可压缩材料](@entry_id:752388)时，会出现所谓的 **[体积锁定](@entry_id:172606) (Volumetric Locking)** 现象，导致数值解严重偏离真实解。

为了克服这些问题，发展出了 **[混合变分原理](@entry_id:165106) (Mixed Variational Principles)**。其核心思想是，除了位移场，还将其他场（如应力或压力）也作为独立的未知量引入到变分泛函中。

以 **Hellinger-Reissner (HR) 原理** 为例，它将位移 $\boldsymbol{u}$ 和应力 $\boldsymbol{\sigma}$ 都视为[独立变量](@entry_id:267118)。其变分叙述可以表达为寻找驻点 $(\boldsymbol{\sigma}, \boldsymbol{u})$，使得对于任意的虚应力 $\delta \boldsymbol{\sigma}$ 和[虚位移](@entry_id:168781) $\delta \boldsymbol{u}$，下式成立：
$$
\int_{\Omega} \delta \boldsymbol{\sigma} : (\mathsf{C}^{-1} : \boldsymbol{\sigma} - \boldsymbol{\varepsilon}(\boldsymbol{u})) \, \mathrm{d}V - \int_{\Omega} (\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b}) \cdot \delta \boldsymbol{u} \, \mathrm{d}V + \int_{\Gamma_t} (\boldsymbol{\sigma}\boldsymbol{n} - \bar{\boldsymbol{t}}) \cdot \delta \boldsymbol{u} \, \mathrm{d}A = 0
$$
这个混合形式的[弱解](@entry_id:161732)同时包含了[本构关系](@entry_id:186508) $\boldsymbol{\varepsilon} = \mathsf{C}^{-1} : \boldsymbol{\sigma}$ 和平衡方程 $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$ 的[弱形式](@entry_id:142897)。[@problem_id:3591325]

当用有限元方法离散时，标准位移法通常产生一个[对称正定](@entry_id:145886) (SPD) 的线性系统 $\boldsymbol{K}\boldsymbol{d}=\boldsymbol{f}$。相比之下，HR混合法则产生一个更大、但结构为 **[鞍点](@entry_id:142576) (saddle-point)** 的系统。这种系统是还对称但非正定（或称不定）的，需要特殊的数值求解器。[@problem_id:3591325]

此外，[混合有限元](@entry_id:178533)的成功与否，关键在于为独立场（如应力和位移）选择的离散[函数空间](@entry_id:143478)必须满足一定的[相容性条件](@entry_id:637057)，即著名的 **LBB (Ladyzhenskaya–Babuška–Brezzi) 稳定条件** 或 [inf-sup 条件](@entry_id:174538)。不满足[LBB条件](@entry_id:746626)的单元组合会导致解的失稳和伪影。满足[LBB条件](@entry_id:746626)的混合单元则可以有效避免[体积锁定](@entry_id:172606)，在处理[近不可压缩](@entry_id:752387)问题时表现出优异的鲁棒性。[@problem_id:3591325]

总之，[虚功](@entry_id:176403)原理是[计算固体力学](@entry_id:169583)的一块基石。从其基本概念出发，通过一系列严谨的数学推导和物理诠释，它不仅统一了静力学、动力学、小应变和有限变形问题，还为发展更先进和鲁棒的数值方法（如混合法）提供了坚实的理论基础。