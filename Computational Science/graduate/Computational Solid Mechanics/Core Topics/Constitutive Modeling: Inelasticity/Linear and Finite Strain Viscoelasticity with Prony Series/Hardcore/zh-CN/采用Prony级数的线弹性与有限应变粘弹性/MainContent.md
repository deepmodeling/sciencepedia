## 引言
[粘弹性](@entry_id:148045)是聚合物、生物组织和岩土等众多工程材料的关键力学特性，其响应同时兼具弹性固体的储能行为和粘性流体的耗能行为。在[计算固体力学](@entry_id:169583)领域，能否精确地描述和预测这种复杂的时间依赖性与历史依赖性行为，对于结构设计的可靠性、安全性和[性能优化](@entry_id:753341)至关重要。尽管存在多种本构模型，但基于[Prony级数](@entry_id:204348)的模型因其清晰的物理背景（[广义Maxwell模型](@entry_id:169862)）、优良的数学特性和高效的计算实现，已成为现代工程仿真软件中的标准方法。然而，对于初学者和研究人员而言，在深刻理解其理论基础、掌握其在复杂工程问题中的应用，以及解决数值实现中的挑战之间，往往存在知识鸿沟。

本文旨在系统性地填补这一鸿沟，为读者提供一份关于[Prony级数](@entry_id:204348)[粘弹性模型](@entry_id:175352)的全面指南。我们将分三个章节逐步深入：
1.  **原理与机制**：本章将从[应力松弛](@entry_id:159905)与[蠕变](@entry_id:150410)等基本现象出发，构建[线性粘弹性](@entry_id:181219)理论的数学框架，阐明[Prony级数](@entry_id:204348)作为[广义Maxwell模型](@entry_id:169862)的物理内涵，探讨[热力学定律](@entry_id:202285)如何约束模型参数，并最终将理论推广至三维有限应变和非等温情境。
2.  **应用与交叉学科联系**：本章将展示理论的实践价值，内容涵盖如何从实验数据中辨识模型参数，如何在有限元软件中高效实现模型算法，以及如何应用模型解决涉及历史依赖性、[多物理场耦合](@entry_id:171389)的前沿工程问题。
3.  **动手实践**：通过一系列精心设计的计算练习，读者将有机会亲手应用所学知识，解决具体问题，从而将理论理解转化为实践能力。

通过这一结构化的学习路径，读者将能够从基本原理出发，逐步掌握[Prony级数](@entry_id:204348)[粘弹性模型](@entry_id:175352)的核心思想与应用技巧。现在，让我们首先进入第一章，深入探索其背后的原理与机制。

## 原理与机制

本章旨在深入探讨[粘弹性本构模型](@entry_id:265825)的核心原理与基本机制，重点关注在[计算固体力学](@entry_id:169583)中广泛应用的、基于[Prony级数](@entry_id:204348)的线性和[有限应变粘弹性](@entry_id:194034)理论。我们将从[线性粘弹性](@entry_id:181219)的基本概念出发，建立其数学框架，随后引入[Prony级数](@entry_id:204348)作为一种强大的物理和数学表示方法。在此基础上，我们将阐明[热力学定律](@entry_id:202285)如何约束材料参数，确保模型的物理实在性。最后，我们会将这些概念推广至三维和有限应变领域，并讨论温度对[粘弹性](@entry_id:148045)行为的影响，从而为后续章节中复杂的计算实现和应用奠定坚实的理论基础。

### [线性粘弹性](@entry_id:181219)框架：松弛与蠕变

[粘弹性材料](@entry_id:194223)同时表现出弹性固体的储能特性和粘性流体的耗能特性。这种双重性最直接地体现在两个经典的一维力学实验中：[应力松弛](@entry_id:159905)和[蠕变](@entry_id:150410)。

**[应力松弛](@entry_id:159905)**描述的是材料在瞬时施加并保持恒定应变后的应力响应。对于一个在时间 $t=0$ 时受到阶跃应变 $\epsilon_0$ 的材料，其应力 $\sigma(t)$ 会随时间逐渐减小，最终趋于一个平衡值（对于固体）或零（对于流体）。我们将这种时变行为通过**[应力松弛模量](@entry_id:181332)** $G(t)$ 来量化：
$$
\sigma(t) = G(t) \epsilon_0 \quad (\text{for } t \ge 0)
$$
$G(t)$ 本质上是材料在单位应变下的应力响应历史，是材料固有的属性。

与此对偶的概念是**蠕变**，它描述的是材料在瞬时施加并保持恒定应力下的应变响应。对于一个在时间 $t=0$ 时受到阶跃应力 $\sigma_0$ 的材料，其应变 $\epsilon(t)$ 会随时间逐渐增大。这种行为通过**[蠕变柔量](@entry_id:182488)** $J(t)$ 来定义：
$$
\epsilon(t) = J(t) \sigma_0 \quad (\text{for } t \ge 0)
$$
$J(t)$ 是材料在单位应力下的应变响应历史。

对于更一般的加载历史，我们可以借助**[Boltzmann叠加原理](@entry_id:185170)**来构建本构关系。该原理假设总的响应是所有过去加载增量所引起响应的线性叠加。对于一个从静止状态（即在 $t  0$ 时，$\sigma(t)=0, \epsilon(t)=0$）开始的加载过程，[应力-应变关系](@entry_id:274093)可以写成以下两种等价的[遗传积分](@entry_id:186265)（hereditary integral）形式：
$$
\sigma(t) = \int_{0}^{t} G(t-s) \frac{d\epsilon(s)}{ds} ds
$$
$$
\epsilon(t) = \int_{0}^{t} J(t-s) \frac{d\sigma(s)}{ds} ds
$$
这里的积分核 $G(t-s)$ 和 $J(t-s)$ 体现了材料的“记忆”效应：当前时刻的响应取决于整个加载历史，且过去事件的影响会随着时间的流逝而衰减。

松弛模量 $G(t)$ 和[蠕变柔量](@entry_id:182488) $J(t)$ 并非[相互独立](@entry_id:273670)，它们通过材料的统一[本构关系](@entry_id:186508)联系在一起。在[拉普拉斯变换](@entry_id:159339)（Laplace transform）域中，上述卷积分关系可以转化为简单的代数关系。记 $\tilde{f}(s)$ 为函数 $f(t)$ 的[拉普拉斯变换](@entry_id:159339)，上述两个[积分方程](@entry_id:138643)变换后得到：
$$
\tilde{\sigma}(s) = s \tilde{G}(s) \tilde{\epsilon}(s)
$$
$$
\tilde{\epsilon}(s) = s \tilde{J}(s) \tilde{\sigma}(s)
$$
将两者结合，我们得到一个关于松弛模量和[蠕变柔量](@entry_id:182488)[拉普拉斯变换](@entry_id:159339)的基本关系式 ：
$$
s^2 \tilde{G}(s) \tilde{J}(s) = 1
$$
这个关系式表明，如果我们知道了其中一个函数，原则上就可以确定另一个。在时域中，这种相互关系表现为一组[Volterra积分方程](@entry_id:146652)，例如 $\int_{0}^{t} G(t-s)\,\dot{J}(s)\\,ds=u(t)$，其中 $u(t)$ 是亥维赛德阶跃函数 。

### [Prony级数](@entry_id:204348)表示法：[广义Maxwell模型](@entry_id:169862)

虽然 $G(t)$ 和 $J(t)$ 可以通过实验测量，但在计算模型中，我们需要一个方便、高效的数学表达式来表示它们。**[Prony级数](@entry_id:204348)**（或称Dirichlet级数）是一种极其有效的表示方法，它将松弛模量表示为一系列衰减指数项的和：
$$
G(t) = G_{\infty} + \sum_{i=1}^{N} G_{i}e^{-t/\tau_{i}}
$$
这种形式不仅具有优良的数学特性，便于数值计算，而且有着深刻的物理背景，可以直接与**[广义Maxwell模型](@entry_id:169862)**（或称Wiechert模型）对应 。

[广义Maxwell模型](@entry_id:169862)是一个由多个简单力学元件并联组成的网络。它包含：
1.  一个单独的弹性弹簧，其剪切模量为 $G_\infty$。
2.  $N$ 个Maxwell单元，每个单元由一个模量为 $G_i$ 的弹簧和一个粘度为 $\eta_i$ 的粘壶[串联](@entry_id:141009)而成。

当对该模型施加一个阶跃剪切应变 $\gamma_0$ 时，总应力是所有并联支路应力之和。单独的弹簧支路产生一个恒定的平衡应力 $s_\infty = G_\infty \gamma_0$。对于第 $i$ 个Maxwell单元，在应变施加的瞬间（$t=0$），粘壶来不及流动，如同刚性连接，因此弹簧瞬间产生应力 $s_i(0^+) = G_i \gamma_0$。随后的恒定应变过程中（$t > 0$），粘壶开始流动，导致该支路的应力按指数规律衰减，其特征时间——即**松弛时间** $\tau_i$——由该单元的粘度和模量之比决定：$\tau_i = \eta_i / G_i$。该支路的应力历史为 $s_i(t) = G_i \gamma_0 e^{-t/\tau_i}$。

将所有支路的应力相加，得到的总应力为 $\sigma(t) = \gamma_0 \left( G_{\infty} + \sum_{i=1}^{N} G_{i}e^{-t/\tau_{i}} \right)$。根据松弛模量的定义，我们立即得到[Prony级数](@entry_id:204348)形式。由此，各项参数的物理意义变得清晰 ：
*   $G_{\infty}$ 是**长期平衡模量**，代表材料在所有松弛过程完成后剩余的弹性刚度。对于固体，$G_{\infty} > 0$；对于（粘）流体，$G_{\infty} = 0$。
*   $G_{i}$ 是第 $i$ 个非平衡Maxwell支路的**分模量**，它决定了该松弛模式对总模量的贡献大小。
*   $\tau_{i}$ 是第 $i$ 个松弛模式的**松弛时间**，表征了该模式下应力衰减的速率。

### [热力学约束](@entry_id:755911)与[材料稳定性](@entry_id:183933)

任何物理上合理的[本构模型](@entry_id:174726)都必须遵循[热力学](@entry_id:141121)基本定律。对于[粘弹性材料](@entry_id:194223)，这主要体现为以下几个基本假设和推论 ：
1.  **因果性 (Causality)**：响应不能先于激励。这要求松弛模量和[蠕变柔量](@entry_id:182488)对于负时间参数必须为零，即 $G(t)=0, J(t)=0$ 对于 $t0$。
2.  **衰减记忆 (Fading Memory)**：遥远过去的事件对当前响应的影响可以忽略不计。这要求松弛模量的瞬态部分必须随时间衰减至零，即 $\lim_{t\to\infty} (G(t) - G_\infty) = 0$。
3.  **非负耗散 (Non-negative Dissipation)**：根据热力学第二定律，在任何等温加载过程中，材料的能量耗散率必须非负。

为了深入理解第三个条件如何约束[Prony级数](@entry_id:204348)的参数，我们可以构造一个[亥姆霍兹自由能](@entry_id:136442)函数 $\psi$，并应用[Clausius-Duhem不等式](@entry_id:193424) 。通过严谨的推导，可以证明耗散率 $\mathcal{D}$（即[应力功率](@entry_id:182907)超出自由能储存速率的部分）等于所有粘壶[耗散功率](@entry_id:177328)之和。对于第 $i$ 个Maxwell单元，其非平衡应力为 $\sigma_i$，粘度为 $\eta_i = G_i \tau_i$。因此，总耗散率为：
$$
\mathcal{D}(t) = \sum_{i=1}^{N} \frac{\sigma_i(t)^2}{\eta_i} = \sum_{i=1}^{N} \frac{\sigma_i(t)^2}{G_i \tau_i} \ge 0
$$
为了保证在任何可能的变形历史中（即对于任意可能的 $\sigma_i(t)$ 值）$\mathcal{D}(t)$ 都非负，上式中的每一项都必须非负。考虑到松弛时间 $\tau_i$ 必须为正值（代表有物理意义的耗散过程），这必然要求每个分模量 $G_i$ 也必须是非负的，即 $G_i \ge 0$。同时，为保证材料在长期加载下的稳定性，平衡模量也必须非负，$G_\infty \ge 0$。

综上，[热力学一致性](@entry_id:138886)为[Prony级数](@entry_id:204348)提供了严格的约束：
$$
G_{\infty} \ge 0, \quad G_{i} \ge 0, \quad \tau_{i} > 0 \quad (\text{for all } i)
$$
满足这些条件的松弛模量 $G(t)$ 是一个**完全单调函数 (completely monotone function)**，这意味着它本身及其各阶导数交替变号，即 $G(t) \ge 0, G'(t) \le 0, G''(t) \ge 0, \dots$。这是一个比简单的“非增”更强的条件，是源自物理模型的耗散函数的一个关键数学特征 。相应地，[蠕变柔量](@entry_id:182488) $J(t)$ 必须是一个**伯恩斯坦函数 (Bernstein function)**，即函数非负且其[一阶导数](@entry_id:749425)是完全单调的，这意味着 $J(t)$ 是非减且凹的 。

### 推广至三维与有限应变

#### 三维[线性粘弹性](@entry_id:181219)

将上述概念推广到三维情况，首先需要定义合适的[应变张量](@entry_id:193332)。在线性理论中，我们采用**[小应变张量](@entry_id:754968)**（或称[无穷小应变张量](@entry_id:167211)） $\boldsymbol{\epsilon}$：
$$
\boldsymbol{\epsilon} = \frac{1}{2} (\nabla \boldsymbol{u} + (\nabla \boldsymbol{u})^{\top})
$$
其中 $\boldsymbol{u}$ 是位移场。该定义是通过对精确的[非线性](@entry_id:637147)[应变度量](@entry_id:755495)进行线性化得到的，它成立的前提是[位移梯度](@entry_id:165352) $\nabla \boldsymbol{u}$ 的范数远小于1，即应变和转动都必须是微小的 。在此假设下，[几何非线性](@entry_id:169896)可以忽略，也无需区分不同的[应力张量](@entry_id:148973)（如Cauchy应力、[Piola-Kirchhoff应力](@entry_id:173629)等），且[本构关系](@entry_id:186508)无需引入[客观应力率](@entry_id:199282)来保证框架无关性。

对于各向同性材料，其响应可以方便地分解为**体积响应**（与形状改变无关）和**偏响应**（与体积改变无关）。应力张量 $\boldsymbol{\sigma}$ 和[应变张量](@entry_id:193332) $\boldsymbol{\epsilon}$ 分别分解为球量部分和偏量部分：
*   **应力**：$\boldsymbol{\sigma} = \boldsymbol{s} + p\boldsymbol{I}$，其中 $\boldsymbol{s}$ 是[偏应力张量](@entry_id:267642) ($\mathrm{tr}(\boldsymbol{s}) = 0$)，$p = \frac{1}{3}\mathrm{tr}(\boldsymbol{\sigma})$ 是[静水压力](@entry_id:275365)。
*   **应变**：$\boldsymbol{\epsilon} = \boldsymbol{e} + \frac{1}{3}\epsilon_v\boldsymbol{I}$，其中 $\boldsymbol{e}$ 是偏[应变张量](@entry_id:193332) ($\mathrm{tr}(\boldsymbol{e}) = 0$)，$\epsilon_v = \mathrm{tr}(\boldsymbol{\epsilon})$ 是[体积应变](@entry_id:267252)。

对于各向同性[线性粘弹性](@entry_id:181219)材料，偏响应和体积响应是解耦的，分别由**剪切松弛模量** $G(t)$ 和**体积松弛模量** $K(t)$ 控制。它们各自都可以用[Prony级数](@entry_id:204348)表示。三维的[遗传积分](@entry_id:186265)[本构关系](@entry_id:186508)为 ：
$$
\boldsymbol{s}(t) = 2 \int_{0}^{t} G(t-s) \frac{d\boldsymbol{e}(s)}{ds} ds
$$
$$
p(t) = \int_{0}^{t} K(t-s) \frac{d\epsilon_v(s)}{ds} ds
$$

#### [有限应变粘弹性](@entry_id:194034)的基本原理

当变形不再微小时，线性理论失效。[有限应变理论](@entry_id:176941)必须处理[几何非线性](@entry_id:169896)（[大应变](@entry_id:751152)、大转动）和[材料非线性](@entry_id:162855)。建立一个物理上合理的[有限应变粘弹性](@entry_id:194034)模型，必须满足以下几个关键要求。

首先，我们需要区分不同的**应力张量**及其**功率共轭**的率度量 。在当前构型中，单位体积的[应力功率](@entry_id:182907)是柯西应力 $\boldsymbol{\sigma}$ 与**变形率张量** $\boldsymbol{d}$ 的[双点积](@entry_id:748648)，即 $p = \boldsymbol{\sigma} : \boldsymbol{d}$。变形率张量 $\boldsymbol{d}$ 是[速度梯度](@entry_id:261686) $\boldsymbol{L}=\nabla\boldsymbol{v}$ 的对称部分，$\boldsymbol{d} = \frac{1}{2}(\boldsymbol{L} + \boldsymbol{L}^{\top})$。在参考构型中，等效的单位体积功率可以表示为第一[Piola-Kirchhoff应力](@entry_id:173629) $\boldsymbol{P}$ 与变形梯度率 $\dot{\boldsymbol{F}}$ 的[点积](@entry_id:149019) ($p_R = \boldsymbol{P}:\dot{\boldsymbol{F}}$)，或[第二Piola-Kirchhoff应力](@entry_id:173163) $\boldsymbol{S}$ 与[格林-拉格朗日应变](@entry_id:170427)率 $\dot{\boldsymbol{E}}$ 的[点积](@entry_id:149019) ($p_R = \boldsymbol{S}:\dot{\boldsymbol{E}}$)。这些共轭对应关系是建立[热力学](@entry_id:141121)一致模型的基础。

其次，本构模型必须满足**物质框架无关性（客观性）**原理，即材料响应不应依赖于观察者的[刚体运动](@entry_id:193355)。速度梯度 $\boldsymbol{L}$ 本身不是客观的，在叠加一个刚体旋转时会额外增加一个[旋转张量](@entry_id:191990)。然而，其对称部分，即变形率张量 $\boldsymbol{d}$，却是客观的。在叠加刚体运动 $\boldsymbol{x}^* = \boldsymbol{Q}(t)\boldsymbol{x} + \boldsymbol{c}(t)$ 后，它遵循[张量变换法则](@entry_id:185176) $\boldsymbol{d}^* = \boldsymbol{Q}\boldsymbol{d}\boldsymbol{Q}^{\top}$。此外，由于柯西应力 $\boldsymbol{\sigma}$ 是对称的，[应力功率](@entry_id:182907)仅取决于 $\boldsymbol{d}$（$\boldsymbol{\sigma}:\boldsymbol{L} = \boldsymbol{\sigma}:\boldsymbol{d}$），而与[速度梯度](@entry_id:261686)的反对称部分（[自旋张量](@entry_id:187346) $\boldsymbol{w}$）无关。因此，$\boldsymbol{d}$ 是驱动粘性（耗散）效应的、物理上和数学上都正确的[运动学](@entry_id:173318)度量 。

#### [有限应变粘弹性](@entry_id:194034)本构模型

现代[有限应变粘弹性](@entry_id:194034)模型常采用一种强大的方法，即对变形进行**[乘法分解](@entry_id:199514)**，将响应分离为体积和等容（形状改变）部分 。变形梯度 $\boldsymbol{F}$ 可以唯一地分解为一个纯体积变形部分 $\boldsymbol{F}_{\text{vol}}$ 和一个纯[等容变形](@entry_id:196451)部分 $\boldsymbol{F}_{\text{iso}}$ 的乘积：
$$
\boldsymbol{F} = \boldsymbol{F}_{\text{iso}} \boldsymbol{F}_{\text{vol}}
$$
其中，$\boldsymbol{F}_{\text{vol}} = J^{1/3}\boldsymbol{I}$ 代表一个均匀的球形膨胀（$J=\det \boldsymbol{F}$ 是体积变化率），而 $\boldsymbol{F}_{\text{iso}} = J^{-1/3}\boldsymbol{F}$ 则是一个保体积的变形（$\det\boldsymbol{F}_{\text{iso}}=1$）。

这个[运动学分解](@entry_id:751020)允许我们将[亥姆霍兹自由能](@entry_id:136442)函数 $\Psi$ 假设为等容和体积两部分贡献的**加和**：
$$
\Psi(\boldsymbol{C}) \rightarrow \Psi(\bar{\boldsymbol{C}}, J) = \Psi_{\text{iso}}(\bar{\boldsymbol{C}}) + \Psi_{\text{vol}}(J)
$$
其中 $\bar{\boldsymbol{C}} = J^{-2/3}\boldsymbol{C}$ 是等容[右柯西-格林张量](@entry_id:174156)。这种能量形式的[解耦](@entry_id:637294)，直接导致了应力响应的解耦。[Kirchhoff应力](@entry_id:751039) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$ 可以分解为一个完全由 $\Psi_{\text{iso}}$ 决定的无迹偏应力部分，和一个完全由 $\Psi_{\text{vol}}$ 决定的球量（静水压力）部分。

在此框架下，[粘弹性](@entry_id:148045)可以非常自然地被引入。通常，我们假设材料的体积响应是纯弹性的（即 $\Psi_{\text{vol}}$ 是率无关的），而剪切（等容）响应是[粘弹性](@entry_id:148045)的。这意味着 $\Psi_{\text{iso}}$ 将依赖于一组描述非平衡状态的内部变量，这些内部变量的[演化方程](@entry_id:268137)（通常为[一阶微分方程](@entry_id:173139)）引入了率相关性和耗散。每个[Prony级数](@entry_id:204348)项都对应于一个内部变量的演化，其形式保证了客观性和[热力学一致性](@entry_id:138886)。例如，一种称为“[准线性粘弹性](@entry_id:753957)”的模型通过在客观的[超弹性](@entry_id:159356)应力度量上应用[遗传积分](@entry_id:186265)来实现这一点 。当应变趋于无穷小时，这种复杂的有限应变模型能够自然地退化为我们之前讨论过的[线性粘弹性](@entry_id:181219)模型，即具有粘弹性[剪切模量](@entry_id:167228) $G(t)$ 和弹性[体积模量](@entry_id:160069) $K$ 的模型 。

### 温度效应：[时温等效原理](@entry_id:141843)

温度对[粘弹性材料](@entry_id:194223)（尤其是聚合物）的行为有显著影响。通常，升高温度会加速分子链的运动，从而加快松弛过程。对于一类被称为**热流变简单 (thermorheologically simple)** 的材料，温度变化的影响可以通过对时间轴的伸缩变换来等效。这就是**[时温等效原理](@entry_id:141843) (Time-Temperature Superposition, TTS)**。

该原理的核心思想是，温度变化对材料响应速率的影响，可以通过对时间轴进行伸缩来等效地描述。我们引入一个**位移因子 (shift factor)** $a_T(T)$，它是一个仅与温度相关的无量纲函数。这个因子将参考温度 $T_{\text{ref}}$ 下测得的参考松弛时间 $\tau_i^{\text{ref}}$ 映射到任意温度 $T$ 下的有效松弛时间 $\tau_i(T)$ ：
$$
\tau_i(T) = a_T(T) \cdot \tau_i^{\text{ref}}
$$
对于聚合物等材料，升高温度会加速松弛过程，因此有效松弛时间变短。这要求当 $T > T_{\text{ref}}$ 时，$a_T  1$；当 $T  T_{\text{ref}}$ 时，$a_T > 1$。在此约定下，[Prony级数](@entry_id:204348)形式的松弛模量在任意等温温度 $T$ 下变为：
$$
G(t; T) = G_{\infty} + \sum_{i=1}^{N} G_{i}e^{-t/\tau_{i}(T)}
$$
对于非等温情况，我们引入**折算时间 (reduced time)** $\xi(t)$，其定义为：
$$
\xi(t) = \int_{0}^{t} \frac{ds}{a_T(T(s))}
$$
这样，非等温本构关系可以统一写成与参考温度下形式相同的[遗传积分](@entry_id:186265)：
$$
\sigma(t) = \int_{0}^{t} G_{\text{ref}}(\xi(t) - \xi(s)) \frac{d\epsilon(s)}{ds} ds
$$
其中 $G_{\text{ref}}$ 是在参考温度下测得的松弛模量。

位移因子 $a_T(T)$ 的具体形式是一个材料属性。在玻璃化转变温度附近及以上，**Williams-Landel-Ferry (WLF) 方程**被广泛用于描述其温度依赖性 ：
$$
\log_{10} a_T(T) = -\frac{C_1(T-T_{\text{ref}})}{C_2+(T-T_{\text{ref}})}
$$
其中 $C_1$ 和 $C_2$ 是材料常数。这个方程与我们的约定一致：当 $T > T_{\text{ref}}$ 时，$a_T  1$；当 $T  T_{\text{ref}}$ 时，$a_T > 1$。例如，当温度从 $T_{\text{ref}} = 20^{\circ}\mathrm{C}$ 降至 $T=0^{\circ}\mathrm{C}$ 时，使用典型的WLF常数计算出的 $a_T$ 值将大于1，导致有效松弛时间 $\tau_i(T)$ 变长，松弛过程显著减慢，这与物理直觉相符 。

[TTS原理](@entry_id:192943)同样可以无缝地集成到有限应变模型中。位移因子 $a_T$ 直接用于调整内部变量演化方程中的动力学速率，而不改变[自由能函数](@entry_id:749582)本身。这相当于在物理时间域内，将[Prony级数](@entry_id:204348)中的参考松弛时间 $\tau_i^{\text{ref}}$ 替换为温度依赖的有效松弛时间 $\tau_i(T)$ 。这种方法使得在复杂的非等温、[大变形分析](@entry_id:163435)中，能够以一种[热力学](@entry_id:141121)一致且物理上合理的方式来考虑温度的影响。