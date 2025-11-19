## 引言
材料的时间依赖性力学行为，即粘弹性和[粘塑性](@entry_id:165397)，是理解和预测从高分子材料到生物组织，再到岩土结构等众多系统响应的关键。然而，准确描述这些复杂的非弹性现象，并将其有效地应用于工程仿真，需要一个连接物理原理、数学模型与数值算法的坚实理论桥梁。本文旨在构建这样一个桥梁，系统地解决如何从根本上区分、建立和应用粘弹性与[粘塑性](@entry_id:165397)[本构模型](@entry_id:174726)这一核心问题。

在接下来的内容中，读者将踏上一段从理论到实践的深入学习之旅。“原理与机制”部分将从连续介质[热力学](@entry_id:141121)的基础出发，系统阐述这两类模型的物理机理、数学表达（如[Prony级数](@entry_id:204348)和[Perzyna模型](@entry_id:753365)）及其在有限元分析中的数值实现方法。“应用与交叉学科联系”部分将通过一系列生动的案例，展示这些理论在[生物力学](@entry_id:153973)、[软物质物理](@entry_id:145473)、结构工程和先进[材料设计](@entry_id:160450)等前沿领域的强大应用价值。最后，“动手实践”部分将提供具体的计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，本文将引导您全面掌握粘弹性与[粘塑性](@entry_id:165397)[本构模型](@entry_id:174726)的核心精髓。

## 原理与机制

本节深入探讨粘弹性与[粘塑性](@entry_id:165397)[本构模型](@entry_id:174726)的物理原理和数学机制。我们将从基本的[热力学](@entry_id:141121)框架出发，系统地阐述这两类材料行为的建模方法，从经典的[线性粘弹性](@entry_id:181219)理论，到复杂的[非线性](@entry_id:637147)[粘塑性](@entry_id:165397)理论，最终延伸至有限变形下的高级运动学和[客观性原理](@entry_id:185412)。本节旨在为读者构建一个严谨、系统且适用于[有限元分析](@entry_id:138109)的理论基础。

### 非弹性行为的基本概念：可恢[复性](@entry_id:162752)与永久性

材料在受力时发生的变形，在载荷移除后，一部分可以恢复（弹性变形），而另一部分则可能与时间相关或永久保留下来，这部分统称为**非弹性变形 (inelastic deformation)**。非弹性行为主要分为两类：**粘弹性 (viscoelasticity)** 和 **塑性 (plasticity)**。

一个核心的区别在于变形的**可恢复性 (recoverability)**。[粘弹性](@entry_id:148045)变形，有时也称为**滞弹性 (anelasticity)**，是一种完全可恢复的变形，但恢复过程需要时间。想象一下挤压一块记忆海绵：它会立即变形，松手后它会慢慢地恢复到原始形状。这个缓慢恢复的过程正是粘弹性的体现。相比之下，塑性变形是永久性的、不可恢复的。将回形针弯曲超过其[弹性极限](@entry_id:186242)，它将永久保持新的形状，即使移除所有外力。当这种永久变形的速率依赖于加载速率时，我们称之为**[粘塑性](@entry_id:165397) (viscoplasticity)**。

为了从根本上理解和区分这两种行为，我们引入一个统一的**连续介质[热力学](@entry_id:141121)框架 (continuum thermodynamics framework)**。对于[等温过程](@entry_id:143096)，[热力学第二定律](@entry_id:142732)要求材料内部的耗散 $\mathcal{D}$ 必须是非负的。这由 **Clausius–Duhem 不等式** 给出：
$$
\mathcal{D} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} \ge 0
$$
其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\varepsilon}$ 是总[应变张量](@entry_id:193332)，$\psi$ 是单位体积的 **亥姆霍兹自由能 (Helmholtz free energy)**，上方的点表示材料时间导数。[亥姆霍兹自由能](@entry_id:136442) $\psi$ 是一个[状态函数](@entry_id:137683)，代表了储存在材料中的可恢复的弹性能。

在一个**内变量 (internal variable)** 框架中，我们假设自由能 $\psi$ 是弹性应变 $\boldsymbol{\varepsilon}^e$ 和一组内变量 $\mathbf{q}$ 的函数，即 $\psi = \psi(\boldsymbol{\varepsilon}^e, \mathbf{q})$。这些内变量描述了材料内部微观结构的不可见状态。将总应变做加法分解为弹性部分 $\boldsymbol{\varepsilon}^e$ 和非弹性部分 $\boldsymbol{\varepsilon}^{in}$，即 $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^{in}$。通过标准的 Coleman-Noll 推导程序，可以得到应力 $\boldsymbol{\sigma} = \partial\psi / \partial\boldsymbol{\varepsilon}^e$，并且[耗散不等式](@entry_id:188634)简化为仅涉及内变量演化的形式。

这套框架清晰地揭示了滞弹性与[粘塑性](@entry_id:165397)变形的本质区别 [@problem_id:2610462]。
- 对于**滞弹性**（[粘弹性](@entry_id:148045)）变形 $\boldsymbol{\varepsilon}^{ve}$，它通常被视为或与某些内变量 $\mathbf{q}_{ve}$ 相关联，而自由能 $\psi$ 明确地依赖于这些内变量，即 $\psi = \psi(\boldsymbol{\varepsilon}^e, \mathbf{q}_{ve})$。这意味着能量可以储存在这些与滞弹性变形相关的内部构型中。当外加载荷移除后，系统会自发地朝着自由能 $\psi$ 的极小值状态演化。驱动这一过程的是[热力学力](@entry_id:161907) $\mathbf{X} = -\partial\psi / \partial\mathbf{q}_{ve}$，它会驱动内变量 $\mathbf{q}_{ve}$（以及滞弹性应变 $\boldsymbol{\varepsilon}^{ve}$）回归到它们的平衡位置（通常是零），从而实现应变的完全恢复。这个恢复过程由于内部粘性效应而是随时间发生的。
- 对于**[粘塑性](@entry_id:165397)**变形 $\boldsymbol{\varepsilon}^p$，它被定义为永久变形。这意味着自由能不能储存与 $\boldsymbol{\varepsilon}^p$ 相关的能量，即 $\psi$ 不显式依赖于 $\boldsymbol{\varepsilon}^p$（或 $\partial\psi/\partial\boldsymbol{\varepsilon}^p = \boldsymbol{0}$）。因此，一旦产生塑性应变，便没有[热力学](@entry_id:141121)恢复力能将其驱动回零。塑性应变的演化通常由一个**[屈服函数](@entry_id:167970) (yield function)** $f$ 控制，只有当应力状态达到或超过屈服面时（$f \ge 0$），塑性流动才会发生，并且这种流动是不可逆的。

一个简单的思想实验可以阐明这一点 [@problem_id:2610348]：考虑一个杆件，在一段时间内施加恒定的拉伸应力，然后卸载。如果材料是滞弹性的（如[标准线性固体模型](@entry_id:204500)），卸载后杆件的应变会随时间逐渐减小至零。如果材料是[粘塑性](@entry_id:165397)的（如 Perzyna 模型），并且加载应力超过了其屈服强度，那么卸载后杆件将保留一部分永久的残余应变，其大小等于加载过程中累积的塑性应变。

### [线性粘弹性](@entry_id:181219)：原理与模型

[线性粘弹性](@entry_id:181219)是描述那些[应力应变](@entry_id:204183)关系是线性的、但响应具有时间依赖性材料的理论。

#### [流变模型](@entry_id:193749)与 Prony 级数

理解[线性粘弹性](@entry_id:181219)的一个直观方法是通过**[流变模型](@entry_id:193749) (rheological models)**，即弹簧和粘壶的组合。弹簧代表理想弹性行为（[应力与应变](@entry_id:137374)成正比，$\sigma = E\varepsilon$），粘壶代表理想粘性行为（[应力与应变率](@entry_id:263123)成正比，$\sigma = \eta\dot{\varepsilon}$）。

- **Maxwell 模型**：一个弹簧和一个粘壶[串联](@entry_id:141009)。它能描述[应力松弛](@entry_id:159905)，但不能描述长期平衡模量。
- **Kelvin-Voigt 模型**：一个弹簧和一个粘壶并联。它能描述[蠕变](@entry_id:150410)，但不能瞬时产生应变。

为了更真实地模拟高分子材料等复杂材料的行为，通常使用多个 Maxwell 单元与一个单独的弹簧并联，构成**广义 Maxwell 模型 (Generalized Maxwell Model)** [@problem_id:2610272]。在这种模型中，总应力是所有并联支路应力的总和，而所有支路的应变均相等。

对广义 Maxwell 模型施加一个阶跃应变 $\gamma(t) = \gamma_0 H(t)$ 进行[应力松弛](@entry_id:159905)实验，可以推导出其松弛模量 $G(t) = \sigma(t)/\gamma_0$。每个 Maxwell 支路 $i$（由模量为 $G_i$ 的弹簧和粘度为 $\eta_i$ 的粘壶[串联](@entry_id:141009)而成）的应力会随时间指数衰减，其特征时间称为**松弛时间 (relaxation time)** $\tau_i = \eta_i / G_i$。总的松弛模量是所有支路贡献的总和，包括一个代表长期平衡响应的并联弹簧 $G_\infty$。最终得到的松弛模量具有以下形式：
$$
G(t) = G_{\infty} + \sum_{i=1}^{N} G_{i} \exp\left(-\frac{t}{\tau_{i}}\right)
$$
这个表达式被称为 **Prony 级数 (Prony series)**。它是一个极其强大的数学工具，可以通过拟合实验数据来表征几乎任何[线性粘弹性](@entry_id:181219)材料的松弛行为。Prony 级数中的参数 $\{G_\infty, G_i, \tau_i\}$ 直接对应于广义 Maxwell 模型中弹簧和粘壶的物理参数 [@problem_id:2610272]。

#### 积分形式与内变量形式

基于[线性响应理论](@entry_id:145737)和 **Boltzmann [叠加原理](@entry_id:144649) (Boltzmann superposition principle)**，一般加载历史下的应力可以通过**[遗传积分](@entry_id:186265) (hereditary integral)** 计算得到：
$$
\boldsymbol{\sigma}(t) = \int_{0}^{t} \mathbf{C}(t-s) : \dot{\boldsymbol{\varepsilon}}(s) ds
$$
其中 $\mathbf{C}(t)$ 是四阶松弛模量张量，其分量形式即为 Prony 级数。这个积分体现了材料的“**衰退记忆 (fading memory)**”特性：当前时刻的应力是过去所有应变率历史的加权总和，而时间久远的事件权重会随 $t-s$ 的增大而衰减 [@problem_id:2610338]。

虽然[遗传积分](@entry_id:186265)为理论分析提供了深刻的见解，但它对于数值计算（尤其是有限元分析）而言效率低下，因为它需要存储整个加载历史。为了克服这一点，我们可以将 Prony 级数模型转化为等效的**[状态变量](@entry_id:138790) (state-variable)** 或内变量[微分方程](@entry_id:264184)形式。对于一维情况，总应力 $\sigma(t)$ 可以写成平衡部分和非平衡部分之和：
$$
\sigma(t) = E_{\infty}\varepsilon(t) + \sum_{k=1}^{N} q_k(t)
$$
其中，$q_k(t) = \int_{0}^{t} E_k \exp(-(t-s)/\tau_k) \dot{\varepsilon}(s) ds$ 是第 $k$ 个 Maxwell 支路的非平衡应力。可以证明，每个 $q_k$ 都满足一个[一阶常微分方程](@entry_id:264241)：
$$
\dot{q}_k(t) + \frac{1}{\tau_k} q_k(t) = E_k \dot{\varepsilon}(t)
$$
这种微分形式的优点在于，它将历史依赖性完全编码在了当前时刻的内变量 $\{q_k(t)\}$ 中。在数值计算中，我们只需存储和更新这些内变量的值，而无需存储完整的加载历史。

#### 有限元实现

在有限元分析中，时间被离散为一系列时间步 $[t_n, t_{n+1}]$。在每个时间步内，我们可以对内变量的[演化方程](@entry_id:268137)进行积分。假设在一个时间步内应变率恒定（即应变呈线性变化），我们可以对上述[微分方程](@entry_id:264184)进行精确积分 [@problem_id:2610359]。这会得到一个递推的[应力更新算法](@entry_id:181937)。在 $t_{n+1}$ 时刻的应力 $\sigma_{n+1}$ 可以由 $t_n$ 时刻的状态（$\varepsilon_n$ 和 $q_k^n$）以及当前时间步的应变增量 $\Delta\varepsilon = \varepsilon_{n+1} - \varepsilon_n$ 来确定：
$$
\sigma_{n+1} = E_{\infty}\varepsilon_{n+1} + \sum_{k=1}^{N}\left[e^{-\beta_{k}} q_{k}^{n} + E_{k} \frac{1-e^{-\beta_{k}}}{\beta_{k}} \Delta\varepsilon \right]
$$
其中 $\beta_k = \Delta t / \tau_k$ 是无量纲化的时间步长。

对于隐式有限元求解器（通常基于 [Newton-Raphson](@entry_id:177436) 方法），除了应力更新之外，还需要计算**[一致切线模量](@entry_id:168075) (consistent algorithmic tangent)**，定义为 $C^{\text{alg}} = \partial \sigma_{n+1} / \partial \varepsilon_{n+1}$。这个量是[应力更新算法](@entry_id:181937)的精确线性化，对于保证 [Newton-Raphson](@entry_id:177436) 迭代的二次收敛速率至关重要。对于上述[粘弹性模型](@entry_id:175352)，[一致切线模量](@entry_id:168075)为 [@problem_id:2610359]：
$$
C^{\text{alg}} = E_{\infty} + \sum_{k=1}^{N} E_{k} \frac{1-e^{-\beta_{k}}}{\beta_{k}}
$$
最后，该数值格式必须满足[热力学一致性](@entry_id:138886)。可以证明，对于一个由 $\psi(\varepsilon, \{q_k\}) = \frac{1}{2}E_{\infty}\varepsilon^{2} + \sum_{k=1}^{N}\frac{q_{k}^{2}}{2E_{k}}$ 定义的[自由能函数](@entry_id:749582)，上述更新算法在任何时间步长下都是无条件耗散的，满足 $\mathcal{D}_{n\to n+1} \ge 0$，这保证了数值解的稳定性 [@problem_id:2610359] [@problem_id:2610462]。

### [粘塑性](@entry_id:165397)：率相关的永久变形

[粘塑性](@entry_id:165397)理论描述的是材料发生不可恢复变形且变形速率与应力水平相关的现象。与依赖整个加载历史的[粘弹性](@entry_id:148045)不同，[粘塑性](@entry_id:165397)的[路径依赖性](@entry_id:186326)源于其[非线性](@entry_id:637147)和存在一个明确的弹性域。

#### 屈服准则与硬化模型

[粘塑性](@entry_id:165397)理论的核心是**[屈服面](@entry_id:175331) (yield surface)** 的概念，它是在应力空间中定义的一个边界，用于区分纯弹性行为和[弹塑性](@entry_id:193198)/[粘塑性](@entry_id:165397)行为。当应力状态位于[屈服面](@entry_id:175331)内部时，材料行为是弹性的；当应力状态达到或超过[屈服面](@entry_id:175331)时，则发生塑性变形。

对于金属等延性材料，广泛采用的是 **von Mises [屈服准则](@entry_id:193897)**。该准则假设材料的屈服行为与静水压力无关，仅取决于[偏应力张量](@entry_id:267642) $\mathbf{s} = \operatorname{dev}(\boldsymbol{\sigma})$ 的第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2}\mathbf{s}:\mathbf{s}$。

材料在经历塑性变形后，其屈服应力通常会发生变化，这种现象称为**[硬化](@entry_id:177483) (hardening)**。主要有两种理想化的[硬化](@entry_id:177483)模型 [@problem_id:2610306]：
1.  **[各向同性硬化](@entry_id:164486) (Isotropic Hardening)**：[屈服面](@entry_id:175331)在应力空间中均匀扩大，尺寸增加。这由一个标量硬化变量 $R$ 描述。
2.  **[随动硬化](@entry_id:172077) (Kinematic Hardening)**：[屈服面](@entry_id:175331)在应力空间中发生平移，而其尺寸保持不变。这用于描述 **Bauschinger 效应**（即在反向加载时屈服应力降低的现象），由一个称为**[背应力](@entry_id:198105) (backstress)** 的张量 $\boldsymbol{\alpha}$ 描述。

将这两种效应结合起来，带[组合硬化](@entry_id:186067)的 von Mises [屈服函数](@entry_id:167970) $f$ 可以写为 [@problem_id:2610306]：
$$
f = \sqrt{\frac{3}{2}}\|\operatorname{dev}\,\boldsymbol{\sigma}-\boldsymbol{\alpha}\| - (\sigma_{y}+R)
$$
其中 $\sigma_y$ 是初始[屈服应力](@entry_id:274513)。屈服条件为 $f=0$（对于率无关塑性）或 $f>0$（对于过应力型[粘塑性](@entry_id:165397)）。

#### [流动法则](@entry_id:177163)与演化方程

**[流动法则](@entry_id:177163) (flow rule)** 决定了塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向和大小。它通常表示为：
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\gamma} \frac{\partial g}{\partial \boldsymbol{\sigma}}
$$
其中 $g$ 是塑性势函数，$\dot{\gamma}$ 是塑性乘子（一个标量，表示塑性流动的速率）。当 $g=f$ 时，称为**关联流动法则 (associative flow rule)**，此时塑性应变率的方向垂直于屈服面。对于 von Mises 模型，这意味着[塑性流动](@entry_id:201346)是保体积的（$\operatorname{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$）。

对于[粘塑性](@entry_id:165397)，塑性乘子 $\dot{\gamma}$ 是应力状态的函数。一个经典的[粘塑性](@entry_id:165397)模型是 **Perzyna 过应力模型 (overstress model)**。在该模型中，塑性流动的速率取决于应力状态超出静态屈服面的程度，即**过应力 (overstress)** $f$。一维 Perzyna 模型的流动法则可以写为 [@problem_id:2610371]：
$$
\dot{\varepsilon}^{p} = \gamma \left\langle \frac{f}{\sigma_{0}} \right\rangle^{m} \text{sgn}(\sigma)
$$
其中 $\langle x \rangle = \max(x, 0)$ 是 Macaulay 括号，$\gamma$ 是**粘度参数 (viscosity parameter)**，控制材料的流动性（$\gamma$ 越大，流动越快），$m$ 是**率敏感性指数 (rate-sensitivity exponent)**，描述塑性[应变率](@entry_id:154778)与过应力的非线性关系，$\sigma_0$ 是一个参考应力。

#### [热力学](@entry_id:141121)框架与数值实现

将[粘塑性](@entry_id:165397)模型置于[热力学](@entry_id:141121)框架下，可以确保其物理上的合理性。考虑一个包含线弹性、塑性应变和[各向同性硬化](@entry_id:164486)的模型，其自由能可以写为 $\psi(\epsilon, \epsilon_p, \alpha) = \frac{1}{2} E (\epsilon - \epsilon_p)^2 + \frac{1}{2} H \alpha^2$，其中 $\alpha$ 是累积塑性应变，$\dot{\alpha} = |\dot{\epsilon}_p|$ [@problem_id:2610334]。根据 Clausius-Duhem 不等式，可以推导出应力 $\sigma = E(\epsilon - \epsilon_p)$ 以及耗散 $\mathcal{D} = (\sigma - H\alpha)\dot{\epsilon}_p \ge 0$。将[屈服函数](@entry_id:167970) $f = \sigma - (\sigma_y + H\alpha)$ 代入，耗散可以表示为 $\mathcal{D} = (f + \sigma_y)\dot{\epsilon}_p$。由于在激活状态下 $f>0, \sigma_y>0, \dot{\epsilon}_p>0$，耗散非负性得到保证。

在有限元中，[粘塑性](@entry_id:165397)[本构方程](@entry_id:138559)通常采用**[返回映射算法](@entry_id:168456) (return mapping algorithm)** 进行[数值积分](@entry_id:136578)，最常用的是隐式的**[后向欧拉法](@entry_id:139674) (backward Euler)**。算法分为两步：
1.  **弹性预测 (Elastic Predictor)**：假设整个时间步内行为是纯弹性的，计算一个“试探”应力状态。
2.  **塑性修正 (Plastic Corrector)**：检查试探应力是否超出了[屈服面](@entry_id:175331)。如果超出，则需要求解一个非线性方程组来同时满足离散化的[流动法则](@entry_id:177163)和[硬化](@entry_id:177483)法则，将应力状态“[拉回](@entry_id:160816)”到一个满足[本构关系](@entry_id:186508)的位置。

对于带线性[硬化](@entry_id:177483)的 Perzyna 模型，使用[后向欧拉法](@entry_id:139674)可以推导出更新后的应力 $\sigma_{n+1}$ 的闭式解。更重要的是，可以导出其**[一致切线模量](@entry_id:168075)** [@problem_id:2610334]：
$$
K_{\text{alg}} = \frac{d\sigma_{n+1}}{d\epsilon_{n+1}} = E \frac{1 + \Delta t \gamma H}{1 + \Delta t \gamma (E+H)}
$$
这个模量依赖于时间步长 $\Delta t$ 和材料粘度 $\gamma$，并且与简单的[弹性模量](@entry_id:198862) $E$ 或率无关塑性[切线](@entry_id:268870)模量 $EH/(E+H)$ 都不同。使用这个精确的[切线](@entry_id:268870)模量对于保证有限元全局迭代的收敛性至关重要 [@problem_id:2610338]。

[粘塑性](@entry_id:165397)的**[路径依赖性](@entry_id:186326) (path dependence)** 与[线性粘弹性](@entry_id:181219)有本质区别。它的响应取决于加载路径是否以及何时穿过屈服面，这是一个高度[非线性](@entry_id:637147)的条件。因此，与可以用线性[遗传积分](@entry_id:186265)描述的[粘弹性](@entry_id:148045)不同，[粘塑性](@entry_id:165397)行为无法通过任何具有衰退记忆核的[线性卷积](@entry_id:190500)来表示 [@problem_id:2610338]。

### 高级运动学与客观性

以上讨论主要基于小应变假设。当变形和转动较大时，必须采用更严谨的运动学描述，并确保[本构关系](@entry_id:186508)满足物理客观性。

#### [有限应变运动学](@entry_id:168563)：[乘法分解](@entry_id:199514)

在**有限应变 (finite strain)** 理论中，描述变形的主要是**变形梯度张量 (deformation gradient)** $\mathbf{F}$。对于[弹粘塑性](@entry_id:748867)材料，通常采用**[乘法分解](@entry_id:199514) (multiplicative decomposition)** 的思想，将总变形梯度分解为弹性部分 $\mathbf{F}_e$ 和非弹性部分 $\mathbf{F}_{in}$（例如粘性部分 $\mathbf{F}_v$）的乘积：
$$
\mathbf{F} = \mathbf{F}_e \mathbf{F}_v
$$
小应变理论中的**加法分解** $\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}_e + \boldsymbol{\varepsilon}_{in}$ 可以看作是[乘法分解](@entry_id:199514)在单位张量 $\mathbf{I}$ 附近的一阶线性化近似 [@problem_id:2610276]。例如，令 $\mathbf{F} = \mathbf{I} + \nabla\mathbf{u}$，$\mathbf{F}_e = \mathbf{I} + \nabla\mathbf{u}_e$，$\mathbf{F}_v = \mathbf{I} + \nabla\mathbf{u}_v$，代入[乘法分解](@entry_id:199514)并忽略高阶项，可得 $\nabla\mathbf{u} \approx \nabla\mathbf{u}_e + \nabla\mathbf{u}_v$。取其对称部分，就回到了[小应变张量](@entry_id:754968)的加法分解。然而，当应变较大时，这种线性化不再成立，使用[乘法分解](@entry_id:199514)计算出的应力会与[小应变近似](@entry_id:754971)值产生显著差异 [@problem_id:2610276]。

#### 材料框架无关性原理

**材料框架无关性原理 (principle of material frame indifference)**，或称**客观性 (objectivity)**，要求本构关系不能依赖于观察者的[刚体运动](@entry_id:193355)。这意味着，如果对材料施加一个纯[刚体转动](@entry_id:191086)，不应引起任何内部应力状态的真实变化。

对于率型本构模型（即以应力率形式给出的模型），简单的材料时间导数 $\dot{\boldsymbol{\sigma}}$ 并非客观的，因为它包含了由[刚体转动](@entry_id:191086)引起的应力分量的变化。为了构建客观的本构关系，必须使用**[客观应力率](@entry_id:199282) (objective stress rate)**。有多种[客观率](@entry_id:198692)的定义，其中常用的一种是 **[Jaumann 率](@entry_id:185572)**：
$$
\overset{\triangledown}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} - \mathbf{W}\boldsymbol{\sigma} + \boldsymbol{\sigma}\mathbf{W}
$$
其中 $\mathbf{W}$ 是[自旋张量](@entry_id:187346)（[速度梯度](@entry_id:261686)的反对称部分），它描述了材料的瞬时转动速率。

[客观性原理](@entry_id:185412)的直接推论是：在一个纯[刚体转动](@entry_id:191086)过程中，由于没有任何真实变形（变形率张量 $\mathbf{D} = \mathbf{0}$），[客观应力率](@entry_id:199282)必须为零。例如，对于一个仅经历[刚体转动](@entry_id:191086)的物体，$\overset{\triangledown}{\boldsymbol{\sigma}}=\mathbf{0}$。这给出了[应力张量](@entry_id:148973)随[时间演化](@entry_id:153943)的方程 $\dot{\boldsymbol{\sigma}} = \mathbf{W}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{W}$ [@problem_id:2610412]。该方程的解表明，柯西应力张量 $\boldsymbol{\sigma}(t)$ 仅仅是[初始应力](@entry_id:750652)张量 $\boldsymbol{\sigma}(0)$ 随材料一起转动的结果，即 $\boldsymbol{\sigma}(t) = \mathbf{R}(t) \boldsymbol{\sigma}(0) \mathbf{R}^T(t)$，其中 $\mathbf{R}(t)$ 是描述[刚体转动](@entry_id:191086)的[旋转张量](@entry_id:191990)。这确保了本构响应独立于观察者，是构建可靠的有限变形[本构模型](@entry_id:174726)的基石。