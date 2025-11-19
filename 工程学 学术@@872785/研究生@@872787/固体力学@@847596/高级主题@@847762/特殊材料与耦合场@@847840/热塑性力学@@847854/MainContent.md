## 引言
热塑性力学是[固体力学](@entry_id:164042)的一个高级分支，致力于研究材料在力学载荷和热载荷联合作用下的行为。在航空航天、先进制造、能源工程等众多领域，部件往往在极端温度和应力环境下服役，这使得单纯的等温塑性理论不足以准确预测其响应。本文旨在弥合这一知识鸿沟，系统性地阐述热-力全耦合问题的理论基础与工程应用。通过学习本文，读者将首先在“原理与机制”一章中掌握基于连续介质[热力学](@entry_id:141121)的严谨理论框架，理解塑性流动的[本构模型](@entry_id:174726)以及核心的耦合机制。接着，在“应用与跨学科交叉”一章中，我们将展示这些理论如何应用于分析[增材制造](@entry_id:160323)[残余应力](@entry_id:138788)、高[应变率](@entry_id:154778)下的绝热剪切失效以及[热机械疲劳](@entry_id:192113)等前沿工程问题。最后，“动手实践”部分将引导读者将理论知识转化为解决实际问题的计算技能。这种从理论到应用再到实践的结构，将为读者构建一个完整而深入的热塑性力学知识体系。

## 原理与机制

本章旨在系统地阐述热塑性力学的核心原理与机制。我们将从连续介质[热力学](@entry_id:141121)的基本定律出发，构建一个严格的理论框架。在此基础上，我们将详细探讨小应变假设下的[运动学](@entry_id:173318)基础，并深入研究描述材料行为的本构关系，包括[屈服准则](@entry_id:193897)、流动法则和[硬化](@entry_id:177483)规律。最后，我们将重点[分析力学](@entry_id:166738)变形与热传导之间的[双向耦合](@entry_id:178809)作用，揭示热塑性问题的本质。

### [热力学](@entry_id:141121)基本框架

任何物理上合理的材料[本构模型](@entry_id:174726)都必须遵循[热力学](@entry_id:141121)基本定律。在热塑性力学中，这些定律为[本构方程](@entry_id:138559)的形式施加了严格的约束。我们将以亥姆霍兹自由能（Helmholtz free energy）为核心，通过严谨的推导，揭示这些内在约束。

我们考虑一个连续体，其状态由一组[状态变量](@entry_id:138790)描述。在热塑性中，一个最小且[热力学一致的](@entry_id:755906)状态变量集必须能够描述材料的弹性变形、塑性历史和热状态 [@problem_id:2702564]。因此，我们选择弹性应变张量 $\boldsymbol{\varepsilon}^{e}$、绝对温度 $T$ 以及一组用于描述[材料微观结构](@entry_id:198422)演化（如[硬化](@entry_id:177483)）的内变量 $\boldsymbol{\alpha}$ 作为[状态变量](@entry_id:138790)。[亥姆霍兹自由能](@entry_id:136442)密度 $\psi$ 是这些[状态变量](@entry_id:138790)的函数，即 $\psi = \psi(\boldsymbol{\varepsilon}^{e}, T, \boldsymbol{\alpha})$。

理论框架的出发点是[能量守恒](@entry_id:140514)（第一定律）和[熵增原理](@entry_id:142282)（第二定律），它们的局部形式（单位体积）分别为：

- **第一定律（[能量守恒](@entry_id:140514)）**: $\dot{u} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \nabla \cdot \mathbf{q} + r$
- **第二定律（Clausius–Duhem 不等式）**: $\rho \dot{\eta} + \nabla \cdot (\frac{\mathbf{q}}{T}) - \frac{\rho r}{T} \ge 0$

其中，$u$ 是内能密度，$\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\varepsilon}$ 是总[应变张量](@entry_id:193332)，$\mathbf{q}$ 是热流矢量，$r$ 是单位体积的内热源。$\rho$ 是质量密度，$\eta$ 是比熵。

通过引入亥姆霍兹自由能的定义 $\psi = u - T s$（其中 $s=\rho \eta$ 为单位体积的熵），并结合第一定律，Clausius–Duhem 不等式可以被转化为一个更为直接的[耗散不等式](@entry_id:188634)：
$$
\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}} - \dot{\psi} - s\dot{T} - \frac{1}{T}\mathbf{q} \cdot \nabla T \ge 0
$$

根据[小应变运动学](@entry_id:192140)假设，总应变率可以分解为弹性部分和塑性部分，$\dot{\boldsymbol{\varepsilon}} = \dot{\boldsymbol{\varepsilon}}^{e} + \dot{\boldsymbol{\varepsilon}}^{p}$。将自由能 $\psi$ 对时间的[全导数](@entry_id:137587)展开，并代入上述不等式，经过整理可得：
$$
\left( \boldsymbol{\sigma} - \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^e} \right) : \dot{\boldsymbol{\varepsilon}}^e - \left( s + \frac{\partial \psi}{\partial T} \right)\dot{T} + \left(\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^{p} - \frac{\partial \psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}\right) - \frac{1}{T}\mathbf{q} \cdot \nabla T \ge 0
$$

根据 Coleman-Noll 方法，对于任意可能的[热力学过程](@entry_id:141636)，该不等式必须恒成立。由于我们可以任意选择弹性应变率 $\dot{\boldsymbol{\varepsilon}}^{e}$ 和温度变化率 $\dot{T}$，为保证不等式不被违反，它们的系数必须为零。由此，我们得到了一组与耗散无关的状态方程 [@problem_id:2702564]：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{e}}
$$
$$
s = - \frac{\partial \psi}{\partial T}
$$

第一个方程表明，应力是[弹性应变](@entry_id:189634)、温度和内变量的函数，它完全由[亥姆霍兹自由能](@entry_id:136442)的形式确定。第二个方程定义了熵与自由能的关系。这些关系是[热力学](@entry_id:141121)一致[本构模型](@entry_id:174726)的基础。

在满足上述状态方程后，[耗散不等式](@entry_id:188634)简化为：
$$
\mathcal{D}_{\text{int}} + \mathcal{D}_{\text{th}} \ge 0
$$
其中，**内在耗散** $\mathcal{D}_{\text{int}} = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^{p} - \frac{\partial \psi}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}}$ 和 **热耗散** $\mathcal{D}_{\text{th}} = -\frac{1}{T}\mathbf{q} \cdot \nabla T$。通常假设这两种耗散机制是[解耦](@entry_id:637294)的，即要求它们各自非负：
$$
\mathcal{D}_{\text{int}} \ge 0
$$
$$
\mathcal{D}_{\text{th}} \ge 0
$$
热耗散非负的要求通过[傅里叶热传导定律](@entry_id:138911) $\mathbf{q} = -\mathbf{k} \nabla T$（其中热导率张量 $\mathbf{k}$ 是正定的）来满足。而内在耗散非负则对塑性流动和内变量的演化施加了根本性的约束，它表明塑性变形是一个不可逆的、产热的过程 [@problem_id:2702505]。

### [运动学](@entry_id:173318)基础

为了具体化[自由能函数](@entry_id:749582) $\psi(\boldsymbol{\varepsilon}^{e}, T, \boldsymbol{\alpha})$ 中的[弹性应变](@entry_id:189634) $\boldsymbol{\varepsilon}^{e}$，我们必须首先建立描述变形的[运动学](@entry_id:173318)框架。

#### 小应变加法分解

在大多数工程应用中，材料的变形远小于其自身尺寸，此时可以采用小应变理论。该理论的核心运动学假设是**应变加法分解** [@problem_id:2702549]。总的[无穷小应变张量](@entry_id:167211) $\boldsymbol{\varepsilon}$ 可以分解为三个物理上可区分的部分之和：
$$
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^{e} + \boldsymbol{\varepsilon}^{p} + \boldsymbol{\varepsilon}^{th}
$$

- **弹性应变** $\boldsymbol{\varepsilon}^{e}$：这部分应变是可逆的，与应力直接相关（通过 $\boldsymbol{\sigma} = \partial\psi/\partial\boldsymbol{\varepsilon}^e$）。它代表了[晶格](@entry_id:196752)的弹性畸变。卸载后，[弹性应变](@entry_id:189634)将完全恢复。

- **塑性应变** $\boldsymbol{\varepsilon}^{p}$：这部分应变是不可逆的，代表了材料内部微观结构（如[位错滑移](@entry_id:275474)）的永久性重排。塑性应变是路径依赖的，其演化由流动法则和[硬化](@entry_id:177483)规律决定。对于大多数金属，在塑性变形过程中体积变化很小，因此常假设[塑性流动](@entry_id:201346)是不可压缩的，即 $\text{tr}(\boldsymbol{\varepsilon}^{p}) = 0$。

- **[热应变](@entry_id:187744)** $\boldsymbol{\varepsilon}^{th}$：这部分应变由温度变化引起，即使在没有外力的情况下也会发生。对于宏观[各向同性材料](@entry_id:170678)，温度从参考温度 $T_0$ 均匀变化到 $T$ 时，[热应变](@entry_id:187744)是一个纯球形张量，其形式为 [@problem_id:2702549]：
  $$
  \boldsymbol{\varepsilon}^{th} = \alpha(T - T_0)\mathbf{I}
  $$
  其中 $\alpha$ 是线性热膨胀系数，$\mathbf{I}$ 是二阶单位张量。[热应变](@entry_id:187744)本身不产生应力，但如果材料的[自由膨胀](@entry_id:139216)受到约束，就会因 $\boldsymbol{\varepsilon}^{e} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{p} - \boldsymbol{\varepsilon}^{th}$ 的关系而产生热应力。

#### 与[有限应变理论](@entry_id:176941)的联系

虽然小应变理论应用广泛，但理解其与更普适的[有限应变理论](@entry_id:176941)的关系至关重要。在[有限应变理论](@entry_id:176941)中，[运动学](@entry_id:173318)由变形梯度 $\mathbf{F}$ 的**[乘法分解](@entry_id:199514)**描述 [@problem_id:2702510] [@problem_id:2702551]：
$$
\mathbf{F} = \mathbf{F}^{e} \mathbf{F}^{p} \mathbf{F}^{\theta}
$$
其中 $\mathbf{F}^{e}$、$\mathbf{F}^{p}$ 和 $\mathbf{F}^{\theta}$ 分别代表弹性、塑性和热变形梯度。小应变加法分解实际上是当[位移梯度](@entry_id:165352)、塑性变形和[热膨胀](@entry_id:137427)都很小时，对上述[乘法分解](@entry_id:199514)进行一阶线性化的结果。这一推导为小应变理论的有效性提供了坚实的理论基础 [@problem_id:2702510]。

在有限应变框架下，为了保证客观性（即[本构关系](@entry_id:186508)在[刚体转动](@entry_id:191086)下不变），自由能通常被定义为弹性[右柯西-格林张量](@entry_id:174156) $\mathbf{C}^{e} = \mathbf{F}^{e\top}\mathbf{F}^{e}$ 的函数。此时，与变形率张量 $\mathbf{d}$ 功率共轭的应力是[基尔霍夫应力](@entry_id:751039) $\boldsymbol{\tau} = J\boldsymbol{\sigma}$，而塑性变形梯度 $\mathbf{F}^{p}$ 则成为一个核心的内变量 [@problem_id:2702551]。

### [塑性流动](@entry_id:201346)的[本构模型](@entry_id:174726)

在建立[热力学](@entry_id:141121)和运动学框架之后，我们需要具体的[本构方程](@entry_id:138559)来描述塑性行为，这通常包括[屈服准则](@entry_id:193897)、[流动法则](@entry_id:177163)和[硬化](@entry_id:177483)规律。

#### 屈服准则

屈服准则定义了材料从弹性变形转入塑性变形的临界应力状态。它通常表示为一个[屈服函数](@entry_id:167970) $f(\boldsymbol{\sigma}, \boldsymbol{\alpha}, T) \le 0$。当 $f  0$ 时，材料处于弹性状态；当 $f=0$ 时，材料可能发生[塑性流动](@entry_id:201346)。

- **von Mises 准则**: 该准则广泛用于金属材料，假设屈服仅取决于[偏应力张量](@entry_id:267642)的第二[不变量](@entry_id:148850) $J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s}$，其中 $\boldsymbol{s}$ 是偏应力。其形式为：
  $$
  f = \sqrt{3J_2} - \sigma_y(T) = 0
  $$
  其中 $\sigma_y(T)$ 是随温度变化的单轴[屈服应力](@entry_id:274513)。该准则与静水压力无关，其在[主应力空间](@entry_id:184388)的屈服面是一个以静水压力线为轴的圆柱体，在偏平面（$\pi$-plane）上的[截面](@entry_id:154995)是一个圆形 [@problem_id:2702477]。

- **Tresca 准则**: 该准则假设当[最大剪应力](@entry_id:181794)达到临界值时材料发生屈服。它也与静水压力无关，但在偏平面上的[截面](@entry_id:154995)是一个正六边形。

- **Drucker-Prager 准则**: 该准则常用于岩土等摩擦性材料，它同时考虑了偏[应力[不变](@entry_id:170526)量](@entry_id:148850) $J_2$ 和静水压力（应力第一[不变量](@entry_id:148850) $I_1 = \text{tr}(\boldsymbol{\sigma})$）。其形式为：
  $$
  f = \sqrt{J_2} + \alpha(T) I_1 - k(T) = 0
  $$
  其中，材料参数 $\alpha(T)$ 和 $k(T)$ 分别与材料的[内摩擦角](@entry_id:197521) $\phi(T)$ 和粘聚力 $c(T)$ 相关，并且这些参数都可能随温度变化。由于对 $I_1$ 的依赖，该准则描述了压力敏感性行为 [@problem_id:2702477]。

在热塑性模型中，一个关键特征是材料参数的温度依赖性。例如，金属的[屈服强度](@entry_id:162154) $\sigma_y(T)$ 通常随温度升高而降低。将这些参数表达为温度的函数，是实现热-力耦合的第一步。

#### [流动法则](@entry_id:177163)

流动法则描述了当[材料屈服](@entry_id:751736)后，塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 的方向和大小。一个被广泛接受的假设是**关联流动法则** (associative flow rule)，它源于[最大塑性耗散](@entry_id:184825)原理。该法则指出，塑性[应变率](@entry_id:154778)的方向垂直于屈服面 [@problem_id:2702526]：
$$
\dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial f}{\partial \boldsymbol{\sigma}}
$$
其中，$\dot{\lambda}$ 是一个非负的标量，称为塑性乘子。其演化遵循 [Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)：$\dot{\lambda} \ge 0$, $f \le 0$, $\dot{\lambda}f = 0$。这意味着只有当应力状态位于[屈服面](@entry_id:175331)上 ($f=0$) 时，才可能发生[塑性流动](@entry_id:201346) ($\dot{\lambda} > 0$)。

对于 von Mises 这类仅依赖于偏应力的 $J_2$ 屈服准则，其对全应力 $\boldsymbol{\sigma}$ 的梯度 $\partial f / \partial \boldsymbol{\sigma}$ 是一个偏量张量。因此，关联[流动法则](@entry_id:177163)自然地预测了[塑性流动](@entry_id:201346)是不可压缩的，即 $\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$ [@problem_id:2702526]。相反，对于 Drucker-Prager 这类压力敏感的准则，$\partial f / \partial \boldsymbol{\sigma}$ 包含体积部分，关联流动将导致塑性体积膨胀（[剪胀性](@entry_id:201001)）。

在持续的塑性加载过程中，应力点必须保持在[屈服面](@entry_id:175331)上，这要求[屈服函数](@entry_id:167970)的时间导数为零，即**[一致性条件](@entry_id:637057)** $\dot{f}=0$。展开后为：
$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \boldsymbol{\alpha}} \cdot \dot{\boldsymbol{\alpha}} + \frac{\partial f}{\partial T} \dot{T} = 0
$$
该方程用于在给定的应力率和温度变化率下确定塑性乘子 $\dot{\lambda}$ 的大小。

#### 硬化规律

硬化描述了材料在塑性变形过程中[屈服应力](@entry_id:274513)增大的现象。它通过内变量 $\boldsymbol{\alpha}$ 的演化来建模，反映了微观结构的变化。

- **[各向同性硬化](@entry_id:164486) (Isotropic Hardening)**: 描述[屈服面](@entry_id:175331)在应力空间中均匀膨胀，而不改变其中心位置。这通常通过一个标量内变量（如等效塑性应变 $p$ 或其相关的变量 $R$）来描述。[屈服函数](@entry_id:167970)写为 $f(\boldsymbol{\sigma}, R, T)$。其演化规律通常与等效塑性[应变率](@entry_id:154778) $\dot{p}$ 相关，例如 $\dot{R} = H(T)\dot{p}$，其中 $H(T)$ 是随温度变化的硬化模量 [@problem_id:2702555]。

- **[随动硬化](@entry_id:172077) (Kinematic Hardening)**: 描述屈服面在应力空间中的平移，而不改变其尺寸。这对于模拟[循环加载](@entry_id:181502)下的 Bauschinger 效应至关重要。平移由一个称为**背应力** (backstress) 的张量内变量 $\boldsymbol{\alpha}$ 描述。[屈服函数](@entry_id:167970)写为 $f(\boldsymbol{\sigma} - \boldsymbol{\alpha}, T)$。一个常见的[随动硬化](@entry_id:172077)模型是 Armstrong-Frederick 模型，它包含一个线性[硬化](@entry_id:177483)项和一个[非线性](@entry_id:637147)的动态恢复项：
  $$
  \dot{\boldsymbol{\alpha}} = \frac{2}{3}C(T)\dot{\boldsymbol{\varepsilon}}^p - \gamma(T)\boldsymbol{\alpha}\dot{p}
  $$
  其中 $C(T)$ 是[随动硬化](@entry_id:172077)模量，$\gamma(T)$ 是[恢复系数](@entry_id:170710)。

- **混合硬化 (Combined Hardening)**: 结合了[各向同性硬化和随动硬化](@entry_id:195752)，能够更全面地描述复杂的材料行为。

在热塑性中，[硬化](@entry_id:177483)行为强烈依赖于温度。通常，随着温度升高，[位错](@entry_id:157482)的储存能力下降，而动态恢复（如[位错攀移](@entry_id:199426)和[交滑移](@entry_id:195437)）机制增强。这导致硬化模量 $H(T)$ 和 $C(T)$ 减小，而[恢复系数](@entry_id:170710) $\gamma(T)$ 增大 [@problem_id:2702555]。

### 热-力耦合机制

热塑性力学的核心在于热场和力学场之间的[双向耦合](@entry_id:178809)。

#### 力学到热的耦合：[塑性耗散](@entry_id:201273)热

塑性变形是一个高度耗散的过程。如[热力学](@entry_id:141121)框架部分所述，塑性功率 $w_p = \boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p$ 的绝大部分会转化为热量，成为一个内热源。只有一小部分能量以[位错](@entry_id:157482)、空位等[晶体缺陷](@entry_id:267016)的形式被储存在材料中，称为冷作硬化能。

这种[能量分配](@entry_id:748987)由 **Taylor-Quinney 系数** $\beta$ 描述 [@problem_id:2702507]：
$$
h_p = \beta w_p = \beta (\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p)
$$
其中 $h_p$ 是单位体积的[塑性耗散](@entry_id:201273)热源。[储能](@entry_id:264866)率则为 $\dot{E}_s = (1-\beta)w_p$。[热力学第二定律](@entry_id:142732)仅约束了 $0 \le \beta \le 1$（假设[储能](@entry_id:264866)率为非负），而 $\beta$ 的具体数值（通常在 $0.9$ 左右）是一个需要通过实验确定的材料本构参数，它可能依赖于应变、应变率和温度。

将此热源项代入[能量守恒方程](@entry_id:748978)，我们得到描述温度场演化的热传导方程 [@problem_id:2702531]：
$$
\rho c \dot{T} = \nabla \cdot (k \nabla T) + \beta (\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p) + r
$$
其中 $c$ 是比热容，$k$ 是热导率。该方程明确地显示了塑性应变率 $\dot{\boldsymbol{\varepsilon}}^p$ 如何作为热源驱动温度场 $\dot{T}$ 的变化。为了完整地定义热问题，还需要相应的边界条件，例如描述与周围环境的[对流](@entry_id:141806)和辐射换热 [@problem_id:2702531]：
$$
-\mathbf{n} \cdot (k \nabla T) = h(T - T_\infty) + \varepsilon_{\text{rad}}\sigma_{\text{SB}}(T^4 - T_{\text{sur}}^4)
$$
其中左侧为传导出的热流，右侧为[对流](@entry_id:141806)和[辐射带](@entry_id:265357)走的热流。

#### 热到力学的耦合：[材料属性的温度依赖性](@entry_id:755834)

温度的变化反过来深刻影响材料的力学行为。这种影响体现在[本构模型](@entry_id:174726)的各个方面：

1.  **[弹性模量](@entry_id:198862)**: [杨氏模量](@entry_id:140430)、剪切模量等[弹性常数](@entry_id:146207)通常随温度升高而降低。
2.  **[热膨胀](@entry_id:137427)**: 温度变化引起[热应变](@entry_id:187744)，在约束条件下产生[热应力](@entry_id:180613)。
3.  **[屈服强度](@entry_id:162154)**: 材料的屈服强度通常对温度敏感，高温下显著降低。
4.  **[硬化](@entry_id:177483)行为**: 如前所述，[硬化](@entry_id:177483)模量和[恢复系数](@entry_id:170710)都表现出强烈的[温度依赖性](@entry_id:147684)。

### 耦合问题的本质

综上所述，热塑性问题是一个完全耦合的[多物理场](@entry_id:164478)问题。力学平衡方程（或[动量守恒](@entry_id:149964)）和[热传导方程](@entry_id:194763)（或[能量守恒](@entry_id:140514)）必须被联立求解 [@problem_id:2702505]。

- **力学场影响热场**: 通过[塑性耗散](@entry_id:201273)热 $\beta (\boldsymbol{\sigma} : \dot{\boldsymbol{\varepsilon}}^p)$，力学变形在能量方程中充当了热源。
- **热场影响力学场**: 通过材料属性（弹性模量、[屈服强度](@entry_id:162154)、[硬化](@entry_id:177483)参数等）的[温度依赖性](@entry_id:147684)以及[热应变](@entry_id:187744)的存在，温度场直接影响力学平衡方程中的本构关系。

与之相对，**[热弹性](@entry_id:158447) (thermoelasticity)** 问题中不存在塑性变形，因此没有[塑性耗散](@entry_id:201273)热源。而**等温塑性 (isothermal plasticity)** 则假设温度场是已知的或恒定的，从而将热传导方程与力学问题解耦。热塑性理论则是对这两种简化情况的推广，能够描述更广泛、更真实的工程场景，如高速成形、热疲劳和[剪切带](@entry_id:183352)的形成。