## 引言
[蠕变与应力松弛](@entry_id:201309)是决定材料和结构长期性能与可靠性的基本时间依赖性力学现象，其影响无处不在，从航空发动机到生物组织。然而，尽管其重要性毋庸置疑，对这些行为的全面理解往往是碎片化的，理论原理、微观机制和实际应用常被孤立对待。本文旨在弥合这一鸿沟，通过对这些关键现象进行统一而系统的探索。

我们的学习之旅始于**“原理与机制”**一章，我们将在此奠定坚实的理论基础。从[蠕变与应力松弛](@entry_id:201309)的宏观定义出发，逐步深入到线性黏[弹性理论](@entry_id:184142)和[热力学一致性](@entry_id:138886)本构模型等严谨的框架中。我们将揭示这些现象的微观结构起源，将原子尺度的过程与宏观定律联系起来。在此理论核心之上，**“应用与跨学科连接”**一章将展示这些概念的深远影响。我们将探索它们如何决定工程部件的[结构完整性](@entry_id:165319)，驱动先进材料的设计，甚至解释[地球物理学](@entry_id:147342)和生物力学中的现象。最后，为巩固理论知识，**“动手实践”**部分提供了指导性的计算练习，让读者能够亲手实现并探索关键的黏弹性模型。通过这种结构化的方法，您将获得关于蠕变和[应力松弛](@entry_id:159905)的深刻且可应用的知识，从而有能力在广泛的科学与工程背景下分析和预测材料的[长期行为](@entry_id:192358)。

## 原理与机制

本章旨在深入探讨[蠕变与应力松弛](@entry_id:201309)现象背后的核心物理原理和数学框架。我们将从宏观现象的定义出发，逐步深入到线性与[非线性](@entry_id:637147)黏[弹性理论](@entry_id:184142)、[热力学](@entry_id:141121)基础，并最终触及控制这些行为的微观尺度机制。本章内容建立在引言章节所述的基本概念之上，旨在为读者提供一个系统而严谨的理论视角。

### 宏观现象学：[蠕变与应力松弛](@entry_id:201309)

材料的时间依赖性行为主要通过两种理想化的[力学测试](@entry_id:203797)来表征：[蠕变](@entry_id:150410)测试和[应力松弛](@entry_id:159905)测试。理解这两种测试的本质区别，是掌握黏弹性力学的起点。

**[蠕变](@entry_id:150410) (Creep)** 是指在恒定应力作用下，材料应变随时间持续增长的现象。想象一根金属杆，在某个高温环境下，我们对其施加并维持一个恒定的拉伸载荷。初始加载瞬间，材料会产生一个瞬时的弹性应变。然而，与纯弹性材料不同，即使外加载荷不再变化，这根杆的伸长（即应变）仍会随着时间的推移而不断增加。这种应变的累积过程就是[蠕变](@entry_id:150410)。从实验控制的角度看，这是一个**应力控制 (stress-controlled)** 或**牵[引力](@entry_id:175476)控制 (traction-controlled)** 的过程。实验中，需要在试样的加载端面上施加恒定的牵[引力](@entry_id:175476)，例如 $\mathbf{t} = \sigma_{0}\mathbf{n}$，同时最小化其他运动学约束以避免过约束，并确保环境温度恒定 。

**[应力松弛](@entry_id:159905) (Stress Relaxation)** 则是指在恒定应变下，材料内部应力随时间逐渐减小的现象。现在，我们对同一根金属杆施加一个瞬时的拉伸位移，并将其长度固定，使其总应变保持在一个恒定值 $\varepsilon_{0}$。初始时刻，维持这一应变需要一个[初始应力](@entry_id:750652) $\sigma(0)$。然而，随着时间的推移，材料内部的微观结构会发生重排，以适应这一固定的变形。结果是，维持该恒定应变所需的力（以及应力）会逐渐减小。这个应力自行“放松”的过程就是[应力松弛](@entry_id:159905)。这是一个**应变控制 (strain-controlled)** 或**[位移控制](@entry_id:748569) (displacement-controlled)** 的过程。实验上，这通常需要借助高刚度的测试机或[闭环控制系统](@entry_id:269635)来实现，通过记录维持恒定应变所需的载荷反力随时间的变化来测得松弛的应力 。

这两种现象的内在联系可以通过一个简单的本构模型来理解。考虑一个由线性弹簧（代表弹性响应）和[非线性](@entry_id:637147)黏壶（代表黏性流动）[串联](@entry_id:141009)而成的模型。总应变 $\varepsilon$ 是[弹性应变](@entry_id:189634) $\varepsilon^e$ 和[蠕变](@entry_id:150410)应变 $\varepsilon^c$ 之和，即 $\varepsilon = \varepsilon^e + \varepsilon^c$。弹性部分服从胡克定律 $\sigma = E\varepsilon^e$，而蠕变流动部分可能服从诺顿型定律 $\dot{\varepsilon}^c = A\sigma^n$。

- 在[蠕变](@entry_id:150410)测试中，$\sigma(t) = \sigma_0$ 是常数。因此，弹性应变 $\varepsilon^e = \sigma_0/E$ 也是常数。[蠕变应变率](@entry_id:187109) $\dot{\varepsilon}^c = A\sigma_0^n$ 是一个正的常数，导致[蠕变](@entry_id:150410)应变 $\varepsilon^c(t)$ 随时间线性增长（对于次级蠕变）。总应变 $\varepsilon(t) = \varepsilon^e + \varepsilon^c(t)$ 随之增加。
- 在[应力松弛](@entry_id:159905)测试中，$\varepsilon(t) = \varepsilon_0$ 是常数，因此 $\dot{\varepsilon} = \dot{\varepsilon}^e + \dot{\varepsilon}^c = 0$。这意味着 $\dot{\varepsilon}^e = -\dot{\varepsilon}^c$。将[本构关系](@entry_id:186508)代入，我们得到 $\frac{\dot{\sigma}}{E} = -A\sigma^n$。这是一个[微分方程](@entry_id:264184)，其解表明只要 $\sigma>0$，$\dot{\sigma}$ 就为负值，即应力随时间单调递减。在这个过程中，[蠕变](@entry_id:150410)应变 $\varepsilon^c$ 的增长恰好被弹性应变 $\varepsilon^e$ 的减少所抵消，从而保持总应变不变 。

### 线性黏弹性框架

当应力和应变足够小时，许多材料的响应可以近似为线性。线性黏弹性理论的核心是 **Boltzmann 叠加原理 (Boltzmann superposition principle)**。该原理指出，材料对一系列载荷的响应等于其对每个单独载荷响应的简单叠加。这一原理假定材料响应是**因果的 (causal)**（即响应不先于激励）和**时移不变的 (time-translation-invariant)**（即[材料性质](@entry_id:146723)不随[绝对时间](@entry_id:265046)改变）。

基于这些基本假设，[应力-应变关系](@entry_id:274093)可以通过[遗传积分](@entry_id:186265)（或称记忆积分）来表示。对于一个初始静止的材料，其在任意应力历史 $\sigma(t)$ 下的应变响应为：
$$
\varepsilon(t) = \int_{0}^{t} J(t-\tau)\,\mathrm{d}\sigma(\tau)
$$
反之，在任意应变历史 $\varepsilon(t)$ 下的应力响应为：
$$
\sigma(t) = \int_{0}^{t} G(t-\tau)\,\mathrm{d}\varepsilon(\tau)
$$
这里的积分是 Riemann–[Stieltjes 积分](@entry_id:157841)形式，它能严谨地处理包含阶跃变化的输入历史 。

这两个方程中的核心是两个材料函数：

- **[蠕变柔量](@entry_id:182488) (Creep Compliance)** $J(t)$：定义为材料对一个在 $t=0$ 时施加的单位阶跃应力（即 $\sigma(t) = H(t)$）所产生的应变响应。物理上，$J(t)$ 描述了材料在单位恒定应力下随时间“变软”或“变形”的程度。
- **松弛模量 (Relaxation Modulus)** $G(t)$：定义为材料对一个在 $t=0$ 时施加的单位阶跃应变（即 $\varepsilon(t) = H(t)$）所产生的应力响应。物理上，$G(t)$ 描述了材料在单位恒定应变下其内部应力随时间“放松”的程度。

这两个函数是材料的内在属性，并且受到热力学第二定律的制约。对于一个**被动 (passive)** 材料（即不能自发产生能量的材料），其在任何准静态加载过程中吸收的净功 $W(t)=\int_{0}^{t}\sigma(\tau)\,\mathrm{d}\varepsilon(\tau)$ 必须是非负的。这一基本物理要求导致了对 $J(t)$ 和 $G(t)$ 形状的严格约束。可以证明，为了保证在任意加载历史下系统的[被动性](@entry_id:171773)，[蠕变柔量](@entry_id:182488) $J(t)$ 必须是一个时间的**非减函数**（即 $\dot{J}(t) \ge 0$），而松弛模量 $G(t)$ 必须是一个时间的**非增函数**（即 $\dot{G}(t) \le 0$）。如果违反这些条件，理论上就可以构造一个特定的加载-卸载循环，从材料中净提取能量，这违背了[热力学](@entry_id:141121)基本定律 。因此，$J(t)$ 的单调非减和 $G(t)$ 的单调非增是线性黏弹性[材料稳定性](@entry_id:183933)的基本标志。

### 统一的[热力学](@entry_id:141121)表述：广义标准材料

弹簧-黏壶等模型为黏弹性行为提供了直观的物理图像，但一个更严谨和普适的框架是基于不可逆过程[热力学](@entry_id:141121)的**广义标准材料 (Generalized Standard Materials, GSM)** 模型。该框架将材料的本构行为与[热力学状态函数](@entry_id:204381)联系起来，自动保证了[热力学第二定律](@entry_id:142732)的满足。

在 GSM 框架下，材料的状态由[可观测量](@entry_id:267133)（如总应变 $\varepsilon$）和一组**[内状态变量](@entry_id:750754) (internal state variables)**（如黏性应变 $\varepsilon^v$）共同描述。材料的本构行为由两个[势函数](@entry_id:176105)完全定义：

1.  **[亥姆霍兹自由能](@entry_id:136442)密度 (Helmholtz free energy density)** $\psi$：一个描述系统儲存能量的状态函数，依赖于状态变量，例如 $\psi(\varepsilon, \varepsilon^v)$。
2.  **耗散势 (dissipation potential)** $\phi$：一个描述[能量耗散](@entry_id:147406)速率的函数，依赖于[内状态变量](@entry_id:750754)的变化率，例如 $\phi(\dot{\varepsilon}^v)$。

应力 $\sigma$ 和内变量的[演化方程](@entry_id:268137)可以通过 Clausius-Duhem 不等式（即[热力学第二定律](@entry_id:142732)的局部形式 $\mathcal{D} = \sigma : \dot{\varepsilon} - \dot{\psi} \ge 0$）导出。

让我们以一个具体的例子——三维 Maxwell 模型——来说明这个过程 。假设自由能和耗散势具有以下形式：
$$
\psi(\varepsilon, \varepsilon^{v}) = \frac{1}{2}(\varepsilon-\varepsilon^{v}) : \mathbb{C} : (\varepsilon-\varepsilon^{v})
$$
$$
\phi(\dot{\varepsilon}^{v}) = \frac{\eta}{2}\dot{\varepsilon}^{v} : \dot{\varepsilon}^{v}
$$
其中 $\mathbb{C}$ 是[四阶弹性张量](@entry_id:188318)，$\eta$ 是黏度系数。$\psi$ 的形式表明能量储存在弹性应变 $\varepsilon^e = \varepsilon - \varepsilon^v$ 中。

将 $\dot{\psi} = \frac{\partial\psi}{\partial\varepsilon} : \dot{\varepsilon} + \frac{\partial\psi}{\partial\varepsilon^{v}} : \dot{\varepsilon}^{v}$ 代入 Clausius-Duhem 不等式，得到：
$$
\left(\sigma - \frac{\partial\psi}{\partial\varepsilon}\right) : \dot{\varepsilon} - \frac{\partial\psi}{\partial\varepsilon^{v}} : \dot{\varepsilon}^{v} \ge 0
$$
为了使该不等式对任意 $\dot{\varepsilon}$ 过程都成立，$\dot{\varepsilon}$ 的系数必须为零。这给出了应力的[本构方程](@entry_id:138559)：
$$
\sigma = \frac{\partial\psi}{\partial\varepsilon} = \mathbb{C} : (\varepsilon - \varepsilon^v)
$$
不等式简化为耗散率 $\mathcal{D} = -\frac{\partial\psi}{\partial\varepsilon^{v}} : \dot{\varepsilon}^{v} \ge 0$。这里的 $-\frac{\partial\psi}{\partial\varepsilon^{v}} = \mathbb{C} : (\varepsilon - \varepsilon^v) = \sigma$ 是与 $\dot{\varepsilon}^v$ 共轭的[热力学力](@entry_id:161907)。

接下来，我们利用耗散势 $\phi$ 导出内变量的演化律（也称[流动法则](@entry_id:177163)）。对于这类简单的二次型耗散势，流动法则服从正交[流动法则](@entry_id:177163)：
$$
\sigma = \frac{\partial\phi}{\partial\dot{\varepsilon}^v} = \eta \dot{\varepsilon}^v \quad \implies \quad \dot{\varepsilon}^v = \frac{1}{\eta}\sigma
$$
这组方程 $\sigma = \mathbb{C}:(\varepsilon - \varepsilon^v)$ 和 $\dot{\varepsilon}^v = \sigma/\eta$ 完整地定义了三维 Maxwell 模型。我们可以验证其[耗散率](@entry_id:748577) $\mathcal{D} = \sigma : \dot{\varepsilon}^v = (\eta \dot{\varepsilon}^v) : \dot{\varepsilon}^v = \eta (\dot{\varepsilon}^v : \dot{\varepsilon}^v) \ge 0$，由于 $\eta > 0$ 且张量的[双点积](@entry_id:748648)为其 Frobenius 范数的平方，所以耗散恒为非负，模型[热力学](@entry_id:141121)自洽 。

作为一个应用，考虑一维[应力松弛](@entry_id:159905)问题，$\varepsilon(t) = \varepsilon_0 H(t)$。上述模型可化为[微分方程](@entry_id:264184) $\dot{\sigma} + \frac{E}{\eta}\sigma = E\dot{\varepsilon}$。在 $t > 0$ 时，$\dot{\varepsilon}=0$，方程变为 $\dot{\sigma} + \frac{E}{\eta}\sigma = 0$。结合初始条件 $\sigma(0^+) = E\varepsilon_0$（瞬时弹性响应），解得[应力松弛](@entry_id:159905)历史为：
$$
\sigma(t) = E \varepsilon_{0} \exp\left(-\frac{E}{\eta} t\right)
$$
这表明应力从初始弹性值呈指数衰减，衰减的时间常数为 $\tau = \eta/E$ 。

### 蠕变曲线及其微观结构起源

在较高温度下（通常指绝对温度 $T$ 超过[熔点](@entry_id:195793) $T_m$ 的一半，即 $T/T_m \gtrsim 0.5$），金属和陶瓷材料的[蠕变行为](@entry_id:199994)通常呈现出一条特征性的蠕变曲线，即[蠕变](@entry_id:150410)应变 $\varepsilon$ 对时间 $t$ 的曲线。这条曲线一般可分为三个阶段：

1.  **[初始蠕变](@entry_id:204710) (Primary Creep, Stage I)**：在此阶段，[蠕变](@entry_id:150410)速率 $\dot{\varepsilon}$ 随时间减小。这是一个[加工硬化](@entry_id:160669)起主导作用的瞬态过程。
2.  **[稳态蠕变](@entry_id:161740) (Secondary or Steady-State Creep, Stage II)**：[蠕变](@entry_id:150410)速率达到一个近似的最小值并保持恒定。这是工程设计中最为关注的阶段。
3.  **三次蠕变 (Tertiary Creep, Stage III)**：蠕变速率随时间加速增长，最终导致材料断裂。

我们可以通过一个包含**硬化 (hardening)** 和**损伤 (damage)** 的[内状态变量](@entry_id:750754)模型来理解这三个阶段的演变 。设蠕变速率 $\dot{\varepsilon}$ 是应力 $\sigma_0$、温度 $T$、[硬化](@entry_id:177483)变量 $\alpha$ 和[损伤变量](@entry_id:197066) $D$ 的函数：$\dot{\varepsilon}(t) = f(\sigma_0, \alpha(t), D(t), T)$。根据物理观察：
- [硬化](@entry_id:177483)（如位错密度的增加）会阻碍形变，因此 $\frac{\partial f}{\partial \alpha}  0$。
- 损伤（如微裂纹、孔洞的形成）会削弱材料，加速形变，因此 $\frac{\partial f}{\partial D}  0$。
- 在[蠕变](@entry_id:150410)过程中，硬化和损伤都在累积，即 $\dot{\alpha}(t) \ge 0$ 和 $\dot{D}(t) \ge 0$。

蠕变加速度 $\ddot{\varepsilon}$ 可通过链式法则求得：
$$
\ddot{\varepsilon}(t) = \frac{d\dot{\varepsilon}}{dt} = \frac{\partial f}{\partial \alpha}\dot{\alpha}(t) + \frac{\partial f}{\partial D}\dot{D}(t)
$$
这个表达式清晰地揭示了蠕变加速度是[硬化](@entry_id:177483)引起的减速效应和损伤引起的加速效应之间竞争的结果。

- **初始阶段**：材料初始位错密度较低，变形导致[位错](@entry_id:157482)迅速增殖和缠结，即 $\dot{\alpha}(t)$ 很大。此时损伤尚未显著发展，$\dot{D}(t) \approx 0$。因此，硬化项占主导，导致 $\ddot{\varepsilon}(t)  0$，[蠕变](@entry_id:150410)速率随时间降低。
- **[稳态](@entry_id:182458)阶段**：硬化速率与**动态回复 (dynamic recovery)** 速率（如[位错](@entry_id:157482)通过攀移和[交滑移](@entry_id:195437)发生的湮灭和重排）之间达到一种动态平衡。同时，损伤累积速率可能还很小，或者其加速效应恰好被持续的硬化/回复平衡所抵消。其净效应是 $\ddot{\varepsilon}(t) \approx 0$，蠕变速率保持近似恒定。
- **三次阶段**：损伤机制变得显著，如孔洞形核、长大和汇合。$\dot{D}(t)$ 迅速增加。此时，材料的硬化能力可能已经耗尽（$\dot{\alpha}(t) \to 0$），或者损伤的加速效应完全压倒了[硬化](@entry_id:177483)效应。结果是 $\ddot{\varepsilon}(t)  0$，蠕变速率加速，直至断裂 。

### [稳态蠕变](@entry_id:161740)：机制与模型

工程应用中最关键的参数是[稳态蠕变](@entry_id:161740)速率 $\dot{\varepsilon}_{min}$（或 $\dot{\varepsilon}_{ss}$）。对于多晶金属在高温下的蠕变，[稳态蠕变](@entry_id:161740)速率与应力和温度的关系通常由一个经验和理论支持的半经验公式——**[诺顿幂律蠕变](@entry_id:203393) (Norton Power-Law Creep)** 或 Dorn 方程描述 ：
$$
\dot{\varepsilon}_{\min} = A \sigma^{n} \exp\left(-\frac{Q}{RT}\right)
$$
其中：
- $A$ 是一个与[材料微观结构](@entry_id:198422)（如晶粒尺寸、[晶体结构](@entry_id:140373)）和[物理常数](@entry_id:274598)相关的**蠕变常数**。
- $\sigma$ 是外加应力。
- $n$ 是**[应力指数](@entry_id:183429) (stress exponent)**，其数值是判断蠕变主导机制的重要依据。例如，$n \approx 3-8$ 通常对应[位错攀移](@entry_id:199426)控制的[位错蠕变](@entry_id:159638)；$n=1$ 则常与[扩散蠕变](@entry_id:159646)相关。
- $Q$ 是**[蠕变](@entry_id:150410)激活能 (activation energy for creep)**，代表了控制蠕变速率的原子尺度过程（如[原子扩散](@entry_id:159939)）所需克服的能垒。$Q$ 的值常常与材料的[自扩散](@entry_id:754665)激活能相近。
- $R$ 是[普适气体常数](@entry_id:136843)，$T$ 是[绝对温度](@entry_id:144687)。Arrhenius 项 $\exp(-Q/RT)$ 体现了[蠕变](@entry_id:150410)作为[热激活过程](@entry_id:274558)的强烈[温度依赖性](@entry_id:147684)。

这个[幂律](@entry_id:143404)关系并非纯粹经验性的，它可以从[晶体塑性](@entry_id:141273)变形的基本机制推导出来  。塑性应变率可由 **Orowan 方程** 给出：
$$
\dot{\varepsilon} = b \rho v
$$
其中 $b$ 是柏氏矢量的大小，$\rho$ 是可动[位错密度](@entry_id:161592)，$v$ 是[位错](@entry_id:157482)的平均运动速度。在[高温蠕变](@entry_id:189747)中，[位错](@entry_id:157482)的滑移运动常常被[晶格](@entry_id:196752)中的障碍物（如其他[位错](@entry_id:157482)、析出相）所阻碍。[位错](@entry_id:157482)克服这些障碍物的过程，如**[位错攀移](@entry_id:199426) (dislocation climb)**，需要[原子扩散](@entry_id:159939)的辅助，因此成为整个变形过程的速率控制步骤。

- **[位错](@entry_id:157482)速度 ($v$)**：[位错攀移](@entry_id:199426)速度依赖于指向[位错核心](@entry_id:201451)的[空位通量](@entry_id:203720)，而这个通量又受应力驱动。理论分析表明，速度 $v$ 与应力 $\sigma$ 之间存在[幂律](@entry_id:143404)关系，即 $v \propto \sigma^p$。
- **位错密度 ($\rho$)**：在[稳态蠕变](@entry_id:161740)中，[位错](@entry_id:157482)的增殖（硬化）与湮灭（回复）达到动态平衡，使得[位错密度](@entry_id:161592) $\rho$ 达到一个不随时间变化但依赖于应力水平的[稳态](@entry_id:182458)值。实验和理论均表明，[稳态](@entry_id:182458)位错密度也与应力呈[幂律](@entry_id:143404)关系，通常为 $\rho \propto \sigma^q$ (例如，基于 Taylor 关系 $\sigma \propto \sqrt{\rho}$，可得 $q=2$)。

将这两个关系代入 Orowan 方程：
$$
\dot{\varepsilon} \propto (\sigma^q)(b)(\sigma^p) = b\sigma^{p+q}
$$
通过取对数并对应力求导，我们可以直接得到[应力指数](@entry_id:183429) $n$ 与[位错](@entry_id:157482)速度和密度的应力依赖指数之间的关系 ：
$$
n \equiv \frac{\partial \ln\dot{\varepsilon}}{\partial \ln\sigma} = p + q
$$
例如，在一个简单的模型中，若攀移速度 $v \propto \sigma^1$ ($p=1$) 且[位错密度](@entry_id:161592)由 Taylor 关系给出 $\rho \propto \sigma^2$ ($q=2$)，则可以预测[应力指数](@entry_id:183429) $n=3$ 。更复杂的模型可以解释为何 $n$ 的观测值常在 3 到 8 之间。同时，由于[位错攀移](@entry_id:199426)由原子扩散控制，而[扩散](@entry_id:141445)系数具有 Arrhenius 型[温度依赖性](@entry_id:147684) $D \propto \exp(-Q/RT)$，这就自然地解释了蠕变速率中的指数温度项。

### 外部变量的影响与[非线性](@entry_id:637147)行为

除了应力与温度，材料的黏弹性行为还受到其他因素的复杂影响，并常常表现出显著的[非线性](@entry_id:637147)。

#### 时间-温度[叠加原理](@entry_id:144649) (Time-Temperature Superposition, TTS)

对于许多高分子材料，改变温度对松弛模量或[蠕变柔量](@entry_id:182488)的影响，仅仅是将其曲线沿着[对数时间](@entry_id:636778)轴进行平移，而曲线的形状保持不变。这种材料被称为**热流变简单 (thermorheologically simple)** 材料。这一现象被称为**时间-温度叠加原理 (TTS)** 。

TTS 的核心思想是，温度的变化统一地改变了材料中所有分子运动模式的速率。这种变化可以通过一个**水平[移位因子](@entry_id:158260) (horizontal shift factor)** $a_T(T)$ 来量化。$a_T$ 定义为在温度 $T$ 下的特征松弛时间与在参考温度 $T_{\text{ref}}$ 下的特征松弛时间之比。通过将实验时间 $t$ 乘以 $1/a_T$，我们可以得到**简约时间 (reduced time)** $\xi = t/a_T(T)$。在简约时间[坐标系](@entry_id:156346)下，不同温度下的响应曲线可以叠加成一条单一的**[主曲线](@entry_id:161549) (master curve)**。

[移位因子](@entry_id:158260) $a_T(T)$ 的温度依赖性本身也蕴含着物理信息：
- 在[玻璃化转变温度](@entry_id:152253) $T_g$ 附近，其行为通常由经验性的 **WLF (Williams-Landel-Ferry) 方程**描述。
- 在远离 $T_g$ 的区域，其行为常常遵循 **Arrhenius 方程**，表明[分子运动](@entry_id:140498)是由简单的[热激活过程](@entry_id:274558)控制的。

对于那些具有多种弛豫机制且这些机制的激活能不同的材料，TTS 原理不成立，这类材料被称为**热流变复杂 (thermorheologically complex)** 材料 。

此外，TTS 原理可以推广到非[等温过程](@entry_id:143096)。对于一个温度随时间变化的历程 $T(t)$，简约时间通过积分定义：$\xi(t) = \int_0^t \frac{d\tau}{a_T(T(\tau))}$。这使得我们能够利用等温实验数据来预测非等温条件下的材料响应 。

#### [非线性](@entry_id:637147)黏弹性

当应力水平较高时，线性黏[弹性理论](@entry_id:184142)不再适用。Boltzmann 叠加原理失效，[应力与应变](@entry_id:137374)之间的关系变为[非线性](@entry_id:637147)。一个重要的[非线性](@entry_id:637147)现象是**时间-应力叠加 (time-stress superposition)**，即应力水平本身也会像温度一样，改变材料的内在时间尺度。

为了描述这种[非线性](@entry_id:637147)行为，发展了多种理论模型，其中 **Schapery 单积分模型** 是一个广泛应用且基于[热力学](@entry_id:141121)理论的框架 。Schapery 模型通过引入几个依赖于应力的[非线性](@entry_id:637147)函数，对线性黏[弹性理论](@entry_id:184142)进行推广。对于单轴[蠕变](@entry_id:150410)，其应变响应可以表示为一个[遗传积分](@entry_id:186265)，其核心要素包括：

- **[非线性](@entry_id:637147)函数 $g_0, g_1, g_2$**：这些函数直接乘以应力或柔量，以描述响应幅度的[非线性](@entry_id:637147)。例如，$g_0$ 可能调整瞬时弹性响应，$g_1$ 和 $g_2$ 则调整瞬态和平衡[蠕变](@entry_id:150410)响应的幅度。
- **应力依赖的[移位因子](@entry_id:158260) $a_{\sigma}(\sigma)$**：这个函数捕捉了时间-应力叠加效应。类似于 $a_T$，它通过定义一个应力依赖的简约时间 $\xi(t) = \int_0^t \frac{d\theta}{a_{\sigma}(\sigma(\theta))}$ 来伸缩材料的内在时间尺度。如果 $a_\sigma  1$，高应力会[加速蠕变](@entry_id:184032)过程；反之则减速。

Schapery 模型的通用形式允许通过实验确定这些[非线性](@entry_id:637147)函数，从而为特定材料构建一个预测能力强的[非线性](@entry_id:637147)[本构模型](@entry_id:174726)。这个框架优雅地将线性理论的积分形式与对幅度和时间尺度的[非线性](@entry_id:637147)修正结合在一起，为理解和预测复杂加载条件下的材料行为提供了强大工具 。