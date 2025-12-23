## 引言
在[计算声学](@entry_id:172112)领域，[偏微分](@entry_id:194612)方程（PDEs）是描述声波传播的通用语言。然而，对于具有复杂几何、多变介质或奇异源的实际问题，直接求解这些方程的经典解（即强形式解）往往极其困难甚至不切实际，这在理论分析和数值计算之间形成了一道鸿沟。声学问题的变分公式正是为了跨越这道鸿沟而生的强大数学工具，它通过将问题重构成一种积分形式（即[弱形式](@entry_id:142897)），为设计稳健而灵活的[数值模拟](@entry_id:146043)方法奠定了坚实的基础。

本文旨在系统性地引导读者深入理解变分公式的理论与实践。通过学习本文，您将掌握从物理定律到可[计算模型](@entry_id:637456)的完整推导路径，并洞悉其在解决前沿声学挑战中的核心作用。文章将分为三个核心部分展开：在“原理与机制”一章中，我们将从第一性原理出发，推导声学[波动方程](@entry_id:139839)的弱形式，并引入[索博列夫空间](@entry_id:141995)这一关键的数学语言。接下来，“应用与跨学科交叉”一章将展示变分框架如何处理无界域、流动介质等复杂场景，并揭示其与地球物理、电磁学等领域的深刻联系。最后，“动手实践”部分将提供具体的编程练习，让您将理论知识转化为解决实际问题的能力。

## 原理与机制

在理解了声学问题的物理背景后，我们现在转向其数学表述的核心：变分公式。本章将从第一性原理出发，系统地推导出声学波动方程的弱形式，并阐明其在[计算声学](@entry_id:172112)中的关键作用。我们将建立必要的数学框架，即[索博列夫空间](@entry_id:141995)（Sobolev spaces），并探讨如何在该框架内精确地处理各种边界条件和初始条件。最后，我们将讨论几个高级主题，包括无界域问题、非均匀介质界面、混合公式以及与数值方法稳定性的深刻联系。本章的目标是为后续章节中详细的[数值离散化](@entry_id:752782)方法奠定坚实的理论基础。

### 从强形式到弱形式：声学[波动方程](@entry_id:139839)

声学现象在数学上通常由[偏微分](@entry_id:194612)方程（PDE）描述，这被称为问题的**强形式**（strong form）。强形式要求解在定义域内的每一点都满足方程，并且具有足够的[光滑性](@entry_id:634843)（例如，二阶连续可微）。然而，对于具有复杂几何形状或非均匀介质的实际问题，寻找满足这些严格要求的经典解往往是不现实的。此外，从数值计算的角度来看，直接离散化强形式也可能很困难。

变分公式或**[弱形式](@entry_id:142897)**（weak form）提供了一种更灵活且功能强大的替代方案。其核心思想是通过将PDE乘以一个任意的**[检验函数](@entry_id:166589)**（test function），然后在整个定义域上积分，从而放宽对解的光滑性要求。这个过程利用**分部积分**（integration by parts），将[高阶导数](@entry_id:140882)转移到[检验函数](@entry_id:166589)上，从而允许解在某种“平均”意义下满足方程，而非逐点满足。

#### 压力波方程的推导

让我们从[线性声学](@entry_id:1127264)的基本物理定律出发，推导标准的二阶压力波方程。考虑一个充满可压缩、[无粘性流体](@entry_id:198262)的有界区域 $\Omega \subset \mathbb{R}^3$。流体由其空间变化的质量密度 $\rho(\boldsymbol{x}) > 0$ 和声速 $c(\boldsymbol{x}) > 0$ 表征。描述小幅声扰动的线性化方程组包括：

1.  **动量守恒方程**（冲量方程）：$\rho(\boldsymbol{x}) \partial_t \boldsymbol{v}(\boldsymbol{x}, t) = -\nabla p(\boldsymbol{x}, t)$，其中 $p$ 是声压，$\boldsymbol{v}$ 是质点速度。
2.  **[质量守恒](@entry_id:204015)方程**（[连续性方程](@entry_id:195013)）：$\partial_t \rho'(\boldsymbol{x}, t) + \rho(\boldsymbol{x}) \nabla \cdot \boldsymbol{v}(\boldsymbol{x}, t) = s_m(\boldsymbol{x}, t)$，其中 $\rho'$ 是密度扰动，$s_m$ 是单位体积的质量注入率。
3.  **[本构关系](@entry_id:186508)**：$\rho'(\boldsymbol{x}, t) = p(\boldsymbol{x}, t) / c^2(\boldsymbol{x})$，它将[密度扰动](@entry_id:159546)与声压联系起来。

我们的目标是消去辅助变量 $\boldsymbol{v}$ 和 $\rho'$，得到一个只关于声压 $p$ 的方程。首先，对质量守恒方程关于时间 $t$ 求导，并注意到 $\rho(\boldsymbol{x})$ 不随时间变化：
$$
\partial_{tt} \rho' + \rho \nabla \cdot (\partial_t \boldsymbol{v}) = \partial_t s_m
$$
接下来，利用动量守恒方程将 $\partial_t \boldsymbol{v}$ 替换为 $-\rho^{-1} \nabla p$：
$$
\partial_{tt} \rho' - \rho \nabla \cdot (\rho^{-1} \nabla p) = \partial_t s_m
$$
最后，使用[本构关系](@entry_id:186508)消去 $\rho'$，即 $\partial_{tt} \rho' = c^{-2} \partial_{tt} p$（因为 $c(\boldsymbol{x})$ 也不随时间变化），我们得到二阶声学[波动方程](@entry_id:139839)：
$$
c^{-2}(\boldsymbol{x}) \partial_{tt} p - \nabla \cdot (\rho^{-1}(\boldsymbol{x}) \nabla p) = s(\boldsymbol{x}, t)
$$
其中，体积声源项 $s = \partial_t s_m$ 代表了有效**[单极子](@entry_id:1128137)源**（monopole source）的密度。

方程中的各项具有明确的物理意义：
- 系数 $c^{-2}$ 是流体[可压缩性](@entry_id:144559) $\kappa_s$ 与质量密度 $\rho$ 的乘积 ($c^2 = 1/(\rho \kappa_s)$)。它衡量了压[力场](@entry_id:147325)的时间变化（加速度）与介质[体积应变率](@entry_id:272471)之间的比例关系，在弱形式中扮演着类似于质量的角色。
- 项 $\rho^{-1} \nabla p$ 根据[动量守恒](@entry_id:149964)方程等于负的质点加速度 $(-\partial_t \boldsymbol{v})$。因此，$\nabla \cdot (\rho^{-1} \nabla p)$ 描述了由压力梯度驱动的流体运动所引起的压缩或稀疏效应。

#### 变分法的推导过程

现在，我们将上述强形式PDE转化为弱形式。我们将方程乘以一个[检验函数](@entry_id:166589) $q$，并在定义域 $\Omega$ 上积分：
$$
\int_{\Omega} \left( c^{-2} \partial_{tt} p \right) q \, \mathrm{d}\boldsymbol{x} - \int_{\Omega} \left( \nabla \cdot (\rho^{-1} \nabla p) \right) q \, \mathrm{d}\boldsymbol{x} = \int_{\Omega} s q \, \mathrm{d}\boldsymbol{x}
$$
这个方程仍然包含对 $p$ 的二阶空间导数。为了降低对 $p$ 的[光滑性](@entry_id:634843)要求，我们对第二项应用**[格林第一恒等式](@entry_id:170345)**（Green's first identity），也就是多维空间的分部积分：
$$
- \int_{\Omega} (\nabla \cdot (\rho^{-1} \nabla p)) q \, \mathrm{d}\boldsymbol{x} = \int_{\Omega} (\rho^{-1} \nabla p) \cdot \nabla q \, \mathrm{d}\boldsymbol{x} - \int_{\partial\Omega} q (\rho^{-1} \nabla p) \cdot \boldsymbol{n} \, \mathrm{d}S
$$
其中 $\partial\Omega$ 是定义域的边界，$\boldsymbol{n}$ 是指向外部的[单位法向量](@entry_id:178851)。将此式代回原积分方程，得到：
$$
\int_{\Omega} c^{-2} \partial_{tt} p \, q \, \mathrm{d}\boldsymbol{x} + \int_{\Omega} \rho^{-1} \nabla p \cdot \nabla q \, \mathrm{d}\boldsymbol{x} = \int_{\Omega} s q \, \mathrm{d}\boldsymbol{x} + \int_{\partial\Omega} q (\rho^{-1} \nabla p) \cdot \boldsymbol{n} \, \mathrm{d}S
$$
这个方程就是**变分形式**。它寻找一个解 $p$，使得对于所有“可允许的”[检验函数](@entry_id:166589) $q$，该积分恒等式都成立。值得注意的是，解 $p$ 的最高空间导数阶数从二阶降至一阶。作为代价，我们现在要求检验函数 $q$ 也具有[一阶导数](@entry_id:749425)。这引出了一个核心问题：函数 $p$ 和 $q$ 应该属于什么样的函数空间？

### 变分公式的语言：[索博列夫空间](@entry_id:141995)

为了严格地定义弱形式，我们需要引入[索博列夫空间](@entry_id:141995)的概念，它为处理具有[弱导数](@entry_id:189356)的函数提供了数学框架。

对于一个有界Lipschitz定义域 $\Omega \subset \mathbb{R}^d$，[复值函数](@entry_id:196054)的**$L^2$空间**，记作 $L^2(\Omega; \mathbb{C})$，包含了所有在 $\Omega$ 上平方可积的函数，即满足 $\int_{\Omega} |u|^2 \, dx  \infty$ 的函数。这是一个希尔伯特空间。

**[索博列夫空间](@entry_id:141995) $H^1(\Omega; \mathbb{C})$** 是 $L^2$ 空间的一个子集，它包含了自身及其所有一阶**[弱导数](@entry_id:189356)**（weak derivatives）都属于 $L^2$ 的函数。具体来说：
$$
H^1(\Omega; \mathbb{C}) = \left\{ u \in L^2(\Omega; \mathbb{C}) : \frac{\partial u}{\partial x_j} \in L^2(\Omega; \mathbb{C}) \text{ for } j=1,\dots,d \right\}
$$
这里的导数是在分布意义下定义的。$H^1$ 空间是一个希尔伯特空间，其标[准范数](@entry_id:753960)定义为：
$$
\|u\|_{H^1(\Omega)}^2 = \int_{\Omega} \left(|u|^2 + |\nabla u|^2\right)\, dx
$$
其中 $|\nabla u|^2 = \sum_{j=1}^d |\partial_{x_j} u|^2$。

对于 $H^1$ 空间中的函数，其在边界 $\partial\Omega$ 上的值（称为**迹**，trace）并非总是经典意义下明确定义的。然而，**[迹定理](@entry_id:203967)**（Trace Theorem）保证了存在一个唯一的[连续线性算子](@entry_id:154042) $\gamma_0: H^1(\Omega) \to H^{1/2}(\partial\Omega)$，可以将 $H^1$ 函数映射到边界上。这个[迹算子](@entry_id:183665)的[像空间](@entry_id:918062)是**分数阶[索博列夫空间](@entry_id:141995) $H^{1/2}(\partial\Omega)$**，而不是更简单的 $L^2(\partial\Omega)$。这意味着，要在边界上规定一个狄利克雷（Dirichlet）数据 $g$，从数学上讲，$g$ 必须属于 $H^{1/2}(\partial\Omega)$ 才能保证存在一个 $H^1(\Omega)$ 内的解其迹为 $g$。

### 在[弱形式](@entry_id:142897)中施加边界条件

变分公式的一个巨大优势在于它处理边界条件的方式。边界条件分为两类：**[本质边界条件](@entry_id:173524)**（essential boundary conditions）和**自然边界条件**（natural boundary conditions）。

#### 本质边界条件：狄利克雷条件

[狄利克雷条件](@entry_id:137096)，如 $p=g$ 在部分边界 $\Gamma_D$ 上，是一种[本质边界条件](@entry_id:173524)。它必须由解所在的**[试探空间](@entry_id:756166)**（trial space）直接满足。

对于**齐次狄利克雷条件** ($p=0$ on $\Gamma_D$)，解 $p$ 必须属于一个其迹在 $\Gamma_D$ 上为零的函数空间。这个空间通常记为 $V_0 = \{ v \in H^1(\Omega) : \gamma_0(v) = 0 \text{ on } \Gamma_D \}$。特别地，如果狄利克雷条件施加在整个边界 $\partial\Omega$ 上，这个空间就是 $H^1_0(\Omega)$。$H^1_0(\Omega)$ 可以被严谨地定义为光滑且在 $\Omega$ 内具有[紧支集](@entry_id:276214)函数空间 $C_c^\infty(\Omega)$ 在 $H^1$ 范数下的[闭包](@entry_id:148169)。对于[Lipschitz域](@entry_id:751354)，这等价于 $H^1(\Omega)$ 中迹为零的函数构成的子空间。

当我们在[弱形式](@entry_id:142897)的推导中[选择检验](@entry_id:182706)函数 $q$ 也来自这个空间 $V_0$ 时，边界积分项 $\int_{\Gamma_D} q (\rho^{-1} \nabla p) \cdot \boldsymbol{n} \, \mathrm{d}S$ 会自动消失，因为在 $\Gamma_D$ 上 $q=0$。这巧妙地移除了我们不了解的法向通量项，使得公式封闭。

对于**非齐次狄利克雷条件** ($p=g$ on $\Gamma_D$，$g \neq 0$)，一个标准做法是使用**提升**（lifting）技术。我们寻找一个已知的“[提升函数](@entry_id:175709)” $\tilde{g} \in H^1(\Omega)$，它满足边界条件，即 $\gamma_0(\tilde{g})=g$ on $\Gamma_D$。然后，我们将未知解 $p$ 分解为 $p = u + \tilde{g}$。代入原问题后，我们发现新的未知函数 $u$ 满足一个具有修正源项的方程以及**齐次**[狄利克雷条件](@entry_id:137096) $u=0$ on $\Gamma_D$。因此，我们可以在空间 $V_0$ 中求解 $u$，这大大简化了问题。

#### 自然边界条件：诺伊曼与[罗宾条件](@entry_id:153384)

诺伊曼（Neumann）条件和罗宾（Robin）条件规定了法向导数或其与函数值的组合，它们是自然边界条件。这类条件通过弱形式中的边界积分项**自然地**被满足，而不需要对[函数空间](@entry_id:143478)施加额外约束。

以一个声学刚性壁为例，其物理条件是法向质点速度为零，即 $\boldsymbol{v} \cdot \boldsymbol{n} = 0$。根据[动量方程](@entry_id:197225)，$\nabla p \cdot \boldsymbol{n} = -\rho (\partial_t \boldsymbol{v}) \cdot \boldsymbol{n} = 0$。这是一个**齐次诺伊曼条件** $\partial_n p = 0$。 在弱形式的边界项 $\int_{\partial\Omega} q (\rho^{-1} \nabla p) \cdot \boldsymbol{n} \, \mathrm{d}S$ 中，我们直接将 $\nabla p \cdot \boldsymbol{n} = 0$ 代入，使得该积分为零。在这种情况下，[试探函数](@entry_id:756165) $p$ 和检验函数 $q$ 都来自整个 $H^1(\Omega)$ 空间，因为没有迹的约束。

更一般地，考虑一个**[阻抗边界条件](@entry_id:750536)**，如 $(\rho^{-1} \nabla p) \cdot \boldsymbol{n} + Z c^{-2} \partial_t p = g_R$ on $\Gamma_R$。 我们可以解出 $(\rho^{-1} \nabla p) \cdot \boldsymbol{n} = g_R - Z c^{-2} \partial_t p$，并将其代入边界积分：
$$
\int_{\Gamma_R} q (\rho^{-1} \nabla p) \cdot \boldsymbol{n} \, \mathrm{d}S = \int_{\Gamma_R} q (g_R - Z c^{-2} \partial_t p) \, \mathrm{d}S
$$
将这个表达式移到弱形式方程的两边，阻抗条件就自然地融入了变分公式中。其中，包含未知解 $\partial_t p$ 的部分 $\int_{\Gamma_R} Z c^{-2} (\partial_t p) q \, \mathrm{d}S$ 成为[双线性形式](@entry_id:746794)的一部分，而给定的数据项 $\int_{\Gamma_R} g_R q \, \mathrm{d}S$ 则成为[线性泛函](@entry_id:276136)的一部分。

### [时域与频域](@entry_id:268132)公式

变分框架同样适用于时域和[频域声学](@entry_id:1125317)问题。

#### 时域：[初边值问题](@entry_id:1126514)

对于时域波动方程，我们需要考虑时间演化，这构成一个**[初边值问题](@entry_id:1126514)**（Initial-Boundary Value Problem, IBVP）。除了边界条件，我们还必须指定**初始条件**：
$$
p(\cdot,0) = p_0, \qquad \partial_t p(\cdot,0) = v_0 \quad \text{in } \Omega
$$
[弱形式](@entry_id:142897)的推导需要对时空域 $\Omega \times (0,T)$ 进行积分。通过在时间上进行分部积分，初始条件 $v_0$ 会作为一个时间边界项出现在变分公式中。而初始条件 $p_0$ 则作为一个本质条件，要求解在 $t=0$ 时刻的迹等于 $p_0$。

为了保证问题的适定性（存在唯一且稳定的解），初始数据和源项必须属于特定的函数空间。对于标准的[波动方程](@entry_id:139839)，有限能量的初始状态要求初始压力 $p_0 \in H^1(\Omega)$ (如果含狄利克雷边界，则为 $H_0^1(\Omega)$)，初始压力时间导数 $v_0 \in L^2(\Omega)$。在这些条件下，可以证明存在唯一的[弱解](@entry_id:161732) $p$，其具有如下正则性：
$$
p \in C([0,T]; H_0^1(\Omega)) \quad \text{and} \quad \partial_t p \in C([0,T]; L^2(\Omega))
$$
这种时间上的连续性保证了初始条件可以被严格满足。

对于无源($s=0$)且边界无耗散（如刚性壁或声-软边界）的系统，声能是守恒的。总声能 $E(t)$ 的表达式为：
$$
E(t) = \frac{1}{2} \int_{\Omega} \left( \frac{1}{\rho c^2} (\partial_t p)^2 + \frac{1}{\rho} |\nabla p|^2 \right) \mathrm{d}\boldsymbol{x}
$$
通过在[弱形式](@entry_id:142897)中[选择检验](@entry_id:182706)函数 $q = \partial_t p$，可以证明 $\frac{dE(t)}{dt}=0$，即能量守恒。

#### 频域：亥姆霍兹方程

许多声学问题，特别是那些涉及单一频率激励或散射的问题，在频域中分析更为方便。通过假设所有场量都具有时间谐波依赖性，例如 $p(\boldsymbol{x},t) = \Re\{P(\boldsymbol{x})e^{-i\omega t}\}$，其中 $\omega$ 是角频率，$P(\boldsymbol{x})$ 是复值压力幅值，时间导数 $\partial_t$ 被替换为 $-i\omega$。

将此**ansatz**代入声学波动方程，我们得到**亥姆霍兹方程**（Helmholtz equation）：
$$
\nabla^2 P + k^2 P = 0
$$
其中 $k = \omega/c$ 是**波数**（wavenumber），它是一个核心参数，描述了单位长度内的相位变化。波数与波长 $\lambda$ 的关系为 $k=2\pi/\lambda$。波数越大（或频率越高），波长越短，声压场的空间振荡越剧烈。这对于数值求解提出了挑战：为了准确捕捉这些振荡，数值网格的尺寸 $h$ 必须远小于波长，通常要求每个波长至少有8到10个网格节点或自由度。对于高阶有限元方法，这个要求可以放宽，关键的[无量纲参数](@entry_id:169335)是 $kh/p$，其中 $p$ 是多项式次数。

[亥姆霍兹方程的弱形式](@entry_id:756664)为：寻找 $P \in V$ 使得对于所有 $Q \in V_0$：
$$
\int_{\Omega} \nabla P \cdot \nabla \overline{Q} \, \mathrm{d}\boldsymbol{x} - k^2 \int_{\Omega} P \overline{Q} \, \mathrm{d}\boldsymbol{x} - \text{boundary terms} = \int_{\Omega} F \overline{Q} \, \mathrm{d}\boldsymbol{x}
$$
其中 $V$ 和 $V_0$ 是合适的[复值函数](@entry_id:196054)空间（如 $H^1(\Omega;\mathbb{C})$ 及其子空间），$\overline{Q}$ 是[检验函数](@entry_id:166589)的[复共轭](@entry_id:174690)。

### 高级主题与应用

变分框架的强大之处在于其处理更复杂问题的能力。

#### 外部问题与[索末菲辐射条件](@entry_id:168772)

当处理散射或辐射问题时，计算域是无界的（例如，$\Omega_{\infty} = \mathbb{R}^3 \setminus \overline{\mathcal{O}}$，其中 $\mathcal{O}$ 是一个障碍物）。在这种情况下，仅有[亥姆霍兹方程](@entry_id:149977)和障碍物表面的边界条件不足以保证[解的唯一性](@entry_id:143619)。物理上，我们需要一个条件来排除从无穷远处传入的、非物理的波，并确保所有由障碍物产生的波都向外传播并消失。

这个条件就是**[索末菲辐射条件](@entry_id:168772)**（Sommerfeld radiation condition）。在三维空间中，对于时间因子 $e^{-i\omega t}$，它写作：
$$
\lim_{r \to \infty} r \left( \frac{\partial u}{\partial r} - i k u \right) = 0
$$
其中 $r = |\boldsymbol{x}|$。这个条件保证了解在无穷远处表现为衰减的 outgoing [球面波](@entry_id:200471)。从数学上讲，它是确保外部亥姆霍兹问题[适定性](@entry_id:148590)的关键。通过结合[格林公式](@entry_id:173118)和Rellich引理，可以证明任何满足[齐次边界条件](@entry_id:750371)和[索末菲辐射条件](@entry_id:168772)的解必定为零，从而保证了[解的唯一性](@entry_id:143619)。

#### [非均匀介质](@entry_id:750241)与界面

当声波穿过不同介质的界面时（例如，$\rho$ 和 $c$ 发生跳变），物理上要求压力和法向质点速度在界面 $\Gamma$ 上连续。这翻译成如下**传输条件**：
1.  压力连续：$[p]_{\Gamma} := p_1|_{\Gamma} - p_2|_{\Gamma} = 0$
2.  法向通量连续：$[a \nabla p \cdot \boldsymbol{n}]_{\Gamma} := a_1 \nabla p_1 \cdot \boldsymbol{n}_1 + a_2 \nabla p_2 \cdot \boldsymbol{n}_2 = 0$，其中 $a=1/\rho$。

在标准（连续）有限元方法中，压力连续性被强加，但法向通量的连续性仅被弱满足。当介质参数（如密度 $\rho$）的对比度（contrast）很大时，标准方法的精度会严重恶化。

**间断伽辽金（Discontinuous Galerkin, DG）方法**或**尼奇（Nitsche）方法**为处理此类问题提供了更稳健的框架。这些方法允许解在界面上不连续，并通过在[弱形式](@entry_id:142897)中添加界[面积分](@entry_id:275394)项来弱施加传输条件。这些项通常包含**[罚函数](@entry_id:638029)**（penalty term）来惩罚压力的跳变 $[p]$，以及精心设计的**[数值通量](@entry_id:145174)**（numerical flux）来近似物理通量。为了确保方法在系数对比度很大时仍然稳定和准确（即**鲁棒性**），数值通量中的加权平均和罚参数的尺度至关重要。研究表明，使用系数的**[调和平均](@entry_id:750175)**（harmonic mean）进行加权，例如罚参数 $\sigma \sim \frac{2 a_1 a_2}{a_1+a_2}$，是实现鲁棒性的关键。

#### 混合变分公式

到目前为止，我们只讨论了基于压力 $p$ 的二阶方程。另一种方法是直接处理一阶方程组，同时求解压力 $p$ 和[质点](@entry_id:186768)速度 $\boldsymbol{v}$。这被称为**混合公式**（mixed formulation）。

对于频域问题，[一阶系统](@entry_id:147467)为：
$$
-i\omega\rho\boldsymbol{v} + \nabla p = \boldsymbol{f}, \qquad -i\omega K^{-1}p + \nabla \cdot \boldsymbol{v} = g
$$
在建立混合[弱形式](@entry_id:142897)时，我们需要为 $\boldsymbol{v}$ 和 $p$ 选择合适的函数空间。由于方程中出现了 $\nabla \cdot \boldsymbol{v}$，速度场 $\boldsymbol{v}$ 必须具有平方可积的散度。这自然地引出了**$H(\mathrm{div}, \Omega)$ 空间**：
$$
H(\mathrm{div}, \Omega) = \{\boldsymbol{w} \in (L^2(\Omega))^d : \nabla \cdot \boldsymbol{w} \in L^2(\Omega)\}
$$
这个空间对于向量场来说，比 $H^1$ 空间的要求更弱（它不要求梯度的每个分量都平方可积），但比 $L^2$ 空间更强。至关重要的是，$H(\mathrm{div}, \Omega)$ 中的函数具有良定义的法向迹 $\boldsymbol{w} \cdot \boldsymbol{n}$，其属于边界空间 $H^{-1/2}(\partial\Omega)$。这使得我们能够严格处理涉及法向速度的边界条件，并确保跨越单元边界的法向通量是连续的，这在[数值离散化](@entry_id:752782)中至关重要。

#### 与[数值稳定性](@entry_id:175146)的联系：污染效应

虽然变分公式为[求解PDE](@entry_id:138485)提供了强大的理论框架，但其离散化（如有限元方法）并非总能保证准确。对于[亥姆霍兹方程](@entry_id:149977)，一个臭名昭著的问题是**污染效应**（pollution effect）或**[数值色散](@entry_id:145368)**（numerical dispersion）。

[亥姆霍兹方程的弱形式](@entry_id:756664)不是强制的（coercive），这意味着其稳定性（inf-sup常数）依赖于波数 $k$。在离散层面，当波数 $k$ 很大时，即使网格尺寸 $h$ 满足基本的波长解析度要求（即 $kh$ 保持为一个小的常数），离散系统的稳定性常数 $\gamma_h(k)$ 也会随着 $k$ 的增大而严重恶化。

这种恶化源于[离散空间](@entry_id:155685)（如分片线性函数）无法精确表示正弦波。数值解的相位[传播速度](@entry_id:189384)与真实解不同，导致相位误差沿传播路径累积。这种累积的[相位误差](@entry_id:162993)就是污染效应。其后果是，为了在固定精度下求解高频问题，必须满足比 $kh \ll C$ 更严格的网格要求，例如 $k^2h \sim C$ 或 $k(kh)^p \sim C$，这使得高频声学计算的成本急剧增加。 

总之，变分公式不仅为声学问题的数学分析提供了严谨的语言，也揭示了其数值求解所面临的深刻挑战。理解弱形式、[函数空间](@entry_id:143478)、边界条件处理以及其稳定性属性，是设计和分析可靠的[计算声学](@entry_id:172112)方法的先决条件。