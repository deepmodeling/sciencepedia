## 引言
模拟含激波等间断现象的[非线性](@entry_id:637147)[双曲守恒律](@entry_id:147752)是计算科学中的一大挑战。虽然连续理论中的[熵条件](@entry_id:166346)可以筛选出物理上唯一正确的解，但标准的数值格式往往无法自动满足这一条件，从而可能导致非物理[振荡](@entry_id:267781)和不稳定性。因此，一个核心的知识缺口在于：如何设计出能够在离散层面严格遵循熵耗散原理，从而保证鲁棒性的[高阶数值方法](@entry_id:142601)？

本文旨在系统性地解答这一问题，全面介绍[非线性系统](@entry_id:168347)的离散熵分析理论。通过学习本文，读者将能够掌握构建[熵稳定格式](@entry_id:749017)的数学框架和关键技术。文章将分为三个章节，引导读者逐步深入：

在“原理与机制”一章中，我们将从连续熵分析出发，详细拆解离散[熵稳定性](@entry_id:749023)的核心要素，包括[分部求和](@entry_id:185335)（SBP）算子、[熵守恒](@entry_id:749018)与[熵稳定数值通量](@entry_id:749026)，以及如何处理[源项](@entry_id:269111)和实现全离散稳定性。

接着，“应用与交叉学科联系”一章将展示这些理论在计算流体动力学、气候建模和[不确定性量化](@entry_id:138597)等领域的具体应用，揭示熵分析作为统一设计原则的强大能力。

最后，在“动手实践”部分，我们提供了一系列精心设计的问题，让读者通过实际操作，加深对[熵稳定格式](@entry_id:749017)、平衡律以及正性保持等关键概念的理解。

让我们首先进入第一章，深入探索保证[数值格式](@entry_id:752822)[非线性](@entry_id:637147)稳定性的基本原理与核心机制。

## 原理与机制

在引言章节中，我们已经了解了[非线性](@entry_id:637147)[双曲守恒律](@entry_id:147752)数值模拟所面临的挑战，特别是解可能出现的间断（如激波）以及由此产生的非唯一性问题。[熵条件](@entry_id:166346)是从物理[上筛](@entry_id:637064)选出正确解的关键数学工具。然而，仅仅在理论上拥有[熵条件](@entry_id:166346)是不够的；我们的数值格式本身必须能够尊重这一条件，以确保其稳定性和收敛到物理相关解。本章将深入探讨确保数值格式满足离散[熵条件](@entry_id:166346)的原理和机制，这一领域通常被称为**离散熵分析 (discrete entropy analysis)**。我们将从连续理论出发，逐步构建离散框架，并阐明现代高阶方法（如谱方法和间断伽辽金方法）中实现[非线性](@entry_id:637147)稳定性的核心思想。

### 连续熵分析回顾

我们首先回顾一下连续统层面上的熵分析。考虑一个一维[标量守恒律](@entry_id:754532)：
$$
\partial_t u + \partial_x f(u) = 0
$$
其中 $u(x,t)$ 是[守恒量](@entry_id:150267)，$f(u)$ 是其通量。对于光滑解，该方程等价于 $\partial_t u + f'(u) \partial_x u = 0$。然而，[非线性](@entry_id:637147)通量可能导致光滑初值在有限时间内发展为间断，此时上述[偏微分方程](@entry_id:141332)的经典解不复存在，我们必须在弱解的框架下进行讨论。[弱解](@entry_id:161732)的不幸之处在于其不唯一性，因此需要一个额外的判据来筛选出物理上有意义的解。

这个判据就是[熵不等式](@entry_id:184404)。我们寻找一个所谓的**熵对 (entropy pair)** $(U, F)$，其中 $U(u)$ 是一个**凸函数 (convex function)**，称为熵函数，而 $F(u)$ 是相应的熵通量。对于光滑解，熵对必须满足一个由原守恒律导出的附加守恒律。通过将原方程乘以 $U'(u)$，我们得到：
$$
U'(u) \partial_t u + U'(u) f'(u) \partial_x u = 0
$$
利用链式法则，第一项是 $\partial_t U(u)$。为了使整个表达式也成为一个守恒律，即 $\partial_t U(u) + \partial_x F(u) = 0$，第二项必须能够写成某个函数 $F(u)$ 的空间导数 $\partial_x F(u) = F'(u) \partial_x u$。比较可知，熵通量 $F(u)$ 必须满足如下的**相容性条件 (compatibility condition)**：
$$
F'(u) = U'(u) f'(u)
$$
这个关系式定义了（在相差一个常数的情况下）与熵函数 $U(u)$ 和物理通量 $f(u)$ 相容的熵通量 $F(u)$ [@problem_id:3380656]。对于弱解，这个等式推广为[熵不等式](@entry_id:184404)：
$$
\partial_t U(u) + \partial_x F(u) \le 0
$$
这个不等式表明，在存在激波等间断时，总熵 $\int U(u) dx$ 必须是随时间不增的（或耗散的）。[凸性](@entry_id:138568) $U''(u) \ge 0$ 是确保这一性质在数学上成立的关键。值得注意的是，一个函数要成为特定守恒律的熵函数，光是凸的还不够，还必须存在一个满足相容性条件的熵通量。例如，虽然 $L^2$ 能量 $\frac{1}{2}u^2$ 是凸的，但它只有在与物理通量 $f(u)$ 相容时才能作为熵函数 [@problem_id:3380656]。

作为一个具体的例子，考虑无粘**[伯格斯方程](@entry_id:177995) (Burgers' equation)**，$f(u) = \frac{1}{2}u^2$。如果我们选择二次函数 $U(u) = \frac{1}{2}u^2$ 作为熵函数（它显然是凸的），那么 $U'(u) = u$ 且 $f'(u) = u$。根据[相容性条件](@entry_id:637057)，熵通量的导数应为 $F'(u) = u \cdot u = u^2$。对其积分并设 $F(0)=0$ 可得熵通量为 $F(u) = \frac{1}{3}u^3$ [@problem_id:3380704]。

对于[守恒律方程组](@entry_id:755768) $\partial_t \boldsymbol{u} + \nabla \cdot \boldsymbol{f}(\boldsymbol{u}) = 0$，其中 $\boldsymbol{u} \in \mathbb{R}^m$，上述概念可以自然推广。熵函数 $U(\boldsymbol{u})$ 是一个从 $\mathbb{R}^m$ 到 $\mathbb{R}$ 的标量凸函数。一个极其重要的概念是**熵变量 (entropy variables)**，定义为熵函数关于[守恒变量](@entry_id:747720)的梯度：
$$
\boldsymbol{v}(\boldsymbol{u}) = \frac{\partial U}{\partial \boldsymbol{u}}
$$
[熵变](@entry_id:138294)量的一个关键作用是它们可以“对称化”[非线性](@entry_id:637147)的[双曲系统](@entry_id:260647)。相容性条件也推广到多维和[方程组](@entry_id:193238)的情况。

让我们以一维**[可压缩欧拉方程](@entry_id:747588) (compressible Euler equations)** 为例。其[守恒变量](@entry_id:747720)为 $\boldsymbol{q} = (\rho, \rho u, \rho E)^T$，代表密度、动量和总能量。对于[理想气体](@entry_id:200096)，物理熵（在忽略常数因子的情况下）可以写成 $s = \ln(p) - \gamma \ln(\rho)$。一个标准的数学熵函数是 $\eta(\boldsymbol{q}) = -\frac{\rho s}{\gamma-1}$。这个函数在其物理容许的状态空间上是严格凸的。通过[链式法则](@entry_id:190743)，我们可以计算出相应的[熵变](@entry_id:138294)量 $\boldsymbol{v} = \partial \eta / \partial \boldsymbol{q}$。以原始变量 $(\rho, u, p)$ 表示，[熵变](@entry_id:138294)量为 [@problem_id:3380713]：
$$
\boldsymbol{v} = \begin{pmatrix} \frac{\gamma - \ln(p) + \gamma\ln(\rho)}{\gamma-1} - \frac{\rho u^2}{2p} & \frac{\rho u}{p} & -\frac{\rho}{p} \end{pmatrix}^T
$$
这个例子清楚地揭示了一个根本性的要求：由于熵函数表达式中包含 $\ln(\rho)$ 和 $\ln(p)$，熵函数和熵变量只在**密度和压力严格为正** ($\rho > 0, p > 0$) 的物理[状态空间](@entry_id:177074)内有定义。如果数值解在任何点违反了这个**正性要求 (positivity requirement)**，熵分析的整个数学框架就会崩溃，因为熵变量本身变得无定义 [@problem_id:3380707]。

### 离散熵分析的目标与核心机制

离散熵分析的目标是在离散层面模拟连续熵分析，从而构建一个保证[非线性](@entry_id:637147)稳定的[数值格式](@entry_id:752822)。具体来说，我们希望构造一个[半离散格式](@entry_id:165671) $\frac{d}{dt}\boldsymbol{u}_h = \mathcal{L}(\boldsymbol{u}_h)$，使得其解 $\boldsymbol{u}_h$ 满足一个半[离散熵不等式](@entry_id:748505)：
$$
\frac{d}{dt} \mathcal{U}_h \le 0
$$
其中 $\mathcal{U}_h$ 是总离散熵，对于一个使用求积规则的节点式方法，它被定义为所有节点上熵值的加权和：
$$
\mathcal{U}_h = \sum_j w_j U(\boldsymbol{u}_j)
$$
其中 $w_j$ 是与节点 $j$ 相关的正[求积权重](@entry_id:753910)。这个不等式保证了一个范数类的量（总熵）不会随时间增长，从而有效地抑制了[非线性不稳定性](@entry_id:752642)的发展。

实现这一目标的核心机制是**在离散层面精确地模仿连续分析中的关键数学操作**，即“乘以熵变量”和“[分部积分](@entry_id:136350)”。

#### [分部求和算子](@entry_id:754520) (Summation-By-Parts Operators)

**[分部求和](@entry_id:185335) (Summation-By-Parts, SBP)** 算子是离散世界中分部积分的[完美模拟](@entry_id:753337)。对于一个节点式离散，一个一阶 SBP 算子由一个对角范数矩阵（或质量矩阵）$M$ 和一个[微分矩阵](@entry_id:149870) $D$ 构成，它们满足代数关系 $M D + D^T M = B$，其中 $B$ 是一个只在区域边界上非零的[边界算子](@entry_id:160216)。这个属性使得我们能够像在连续情况下一样，将一个导数从一个函数“移动”到另一个函数上，代价是在边界上产生一些项。这是在[高阶格式](@entry_id:150564)中处理[非线性](@entry_id:637147)项以实现稳定性的基石 [@problem_id:3380656, @problem_id:3380683]。

#### 求积规则的角色与通量差分

一个常见误解是，为了准确计算总熵 $\mathcal{U}_h$，我们需要一个对高度[非线性](@entry_id:637147)的函数 $U(\boldsymbol{u}_h)$ 都能精确积分的求积规则。然而，基于 SBP 的现代熵稳定方法巧妙地绕开了这个问题。稳定性证明并不依赖于对 $U(\boldsymbol{u}_h)$ 的精确积分，而是依赖于离散算子的[代数结构](@entry_id:137052)（即 SBP 属性）和[数值通量](@entry_id:752791)的特殊构造。因此，对求积规则的最低要求是它能够支持一个 SBP 算子，而不是要求它对任意[非线性](@entry_id:637147)函数都具有很高的积分精度 [@problem_id:3380663]。

此外，对通量散度项 $\partial_x f(u)$ 的简单离散（例如，对多项式 $f(u_h)$ 进行[微分](@entry_id:158718)）通常无法保证[熵稳定性](@entry_id:749023)。取而代之的是，我们使用一种所谓的**分裂形式 (split form)** 或**通量差分 (flux differencing)** 的方法。这种方法将单元内部的通量贡献重新构造为一系列两点[数值通量](@entry_id:752791)的相互作用。通过 SBP 属性，这种构造可以确保单元内部（体积积分）的贡献在熵平衡中能够精确地转化为单元边界上的项，从而将所有可能的熵产生或耗散都**局部化到单元的交界面上** [@problem_id:3380683]。

### 在界面处控制熵：[数值通量](@entry_id:752791)

通过 SBP 和通量差分处理了单元内部的贡献后，整个系统的离散熵演化完全取决于我们在单元交界面上如何定义**数值通量 (numerical flux)**。

#### [熵守恒通量](@entry_id:749013) (Entropy-Conservative Flux)

熵分析的第一步是构建一个在界面上不产生任何数值熵的通量，即**[熵守恒](@entry_id:749018) (entropy-conservative, EC)** 通量。为此，我们引入**熵势 (entropy potential)** 的概念，定义为 $\psi(\boldsymbol{u}) = \boldsymbol{v}(\boldsymbol{u})^T \boldsymbol{f}(\boldsymbol{u}) - F(\boldsymbol{u})$。一个两点[数值通量](@entry_id:752791) $\boldsymbol{f}^{ec}(\boldsymbol{u}_L, \boldsymbol{u}_R)$ 若要实现[熵守恒](@entry_id:749018)，必须满足由 Tadmor 提出的以下关键条件 [@problem_id:3380653, @problem_id:3380664]：
$$
(\boldsymbol{v}_R - \boldsymbol{v}_L)^T \boldsymbol{f}^{ec}(\boldsymbol{u}_L, \boldsymbol{u}_R) = \psi(\boldsymbol{u}_R) - \psi(\boldsymbol{u}_L)
$$
其中 $\boldsymbol{u}_L, \boldsymbol{u}_R$ 是界面左右两侧的状态，$\boldsymbol{v}_L, \boldsymbol{v}_R$ 是对应的熵变量。这个条件保证了数值熵通量在界面上是连续的。当在整个计算域上对所有界面的熵贡献求和时，这些项会形成一个伸缩求和 (telescoping sum)，在[周期性边界条件](@entry_id:147809)下其总和为零。这样，整个格式就实现了离散熵的精确守恒。值得注意的是，为[欧拉方程](@entry_id:177914)等复杂系统构造[熵守恒通量](@entry_id:749013)通常需要用到对数平均等[特殊函数](@entry_id:143234)，这些函数也只在状态量（如密度、压力）为正时才有定义，这再次强调了正性要求的重要性 [@problem_id:3380707]。

#### [熵稳定通量](@entry_id:749015) (Entropy-Stable Flux)

对于包含激波的真实物理问题，我们需要的不仅仅是[熵守恒](@entry_id:749018)，还需要在激波处耗散熵以确保[解的唯一性](@entry_id:143619)。这可以通过在[熵守恒通量](@entry_id:749013)的基础上添加[人工耗散](@entry_id:746522)项来实现，从而构造出**熵稳定 (entropy-stable, ES)** 通量。其一般形式为 [@problem_id:3380653]：
$$
\boldsymbol{f}^{es}(\boldsymbol{u}_L, \boldsymbol{u}_R) = \boldsymbol{f}^{ec}(\boldsymbol{u}_L, \boldsymbol{u}_R) - \frac{1}{2} \boldsymbol{D}(\boldsymbol{u}_L, \boldsymbol{u}_R) (\boldsymbol{v}_R - \boldsymbol{v}_L)
$$
这里的 $\boldsymbol{D}$ 是一个对称半正定 (symmetric positive semidefinite) 的耗散矩阵。当我们将这个通量代入界面的熵产生项时，熵[守恒部分](@entry_id:747718)与熵势的跳跃精确抵消，剩下的耗散项贡献为 $-\frac{1}{2}(\boldsymbol{v}_R - \boldsymbol{v}_L)^T \boldsymbol{D} (\boldsymbol{v}_R - \boldsymbol{v}_L)$。由于 $\boldsymbol{D}$ 是半正定的，这一项永远非正。因此，总熵的变化率 $\frac{d}{dt}\mathcal{U}_h$ 必然小于等于零，从而实现了[离散熵不等式](@entry_id:748505) [@problem_id:3380683]。

最后，必须强调，要获得一个全局稳定的格式，不仅内部界面的通量需要精心设计，计算域**边界上的通量**选择也至关重要。例如，一个允许[能量流](@entry_id:142770)入的边界条件自然会增加区域内的总熵 [@problem_id:3380656]。

### 扩展至更复杂的系统：源项的处理

许多实际问题，如带有地形变化的浅水波方程，都包含源项。考虑如下带[源项](@entry_id:269111)的守恒律：
$$
\partial_t \boldsymbol{q} + \partial_x \boldsymbol{f}(\boldsymbol{q}) = \boldsymbol{s}(\boldsymbol{q},x)
$$
对于这类问题，一个理想的[数值格式](@entry_id:752822)不仅要熵稳定，还应能精确保持某些有物理意义的定常解，例如“湖泊静止”状态（即流速为零，水面为平坦的平衡态）。这种性质被称为**保平衡 (well-balanced)**。

对源项的简单、逐点的离散化通常会破坏格式的保平衡性和[熵稳定性](@entry_id:749023)。为了维持稳定性，[源项](@entry_id:269111)的离散化必须与通量散度的离散化相容。这引出了**熵相容[源项](@entry_id:269111)离散 (entropy-compatible source term discretization)** 的概念。其核心思想是，源项的离散形式必须被精心构造，以便其在熵平衡分析中产生的项能够与通量散度项中由非齐次部分（如地形）产生的项精确抵消。这通常涉及到复杂的、非局部的离散格式，它利用 SBP 属性，并将源项的离散化与[熵守恒通量](@entry_id:749013)中使用的两点平均状态耦合起来 [@problem_id:3380668]。

### 从半离散到全离散稳定性

以上步骤为我们提供了一个[半离散格式](@entry_id:165671)，它满足[熵稳定性](@entry_id:749023)的要求。最后一步是选择一个[时间积分方法](@entry_id:136323)来求解这个[常微分方程组](@entry_id:266774) $\frac{d}{dt} \boldsymbol{u}_h = \mathcal{L}(\boldsymbol{u}_h)$，同时保持已建立的稳定性。

并非所有的[时间积分方法](@entry_id:136323)都能保持[熵稳定性](@entry_id:749023)。一类特别适合此任务的方法是**强稳定保持[龙格-库塔](@entry_id:140452) (Strong-Stability-Preserving [Runge-Kutta](@entry_id:140452), SSP-RK)** 方法。这类方法的关键特性是，它们的每一步都可以被分解为一系列前向欧拉步的**[凸组合](@entry_id:635830) (convex combination)**。

这个特性与[熵稳定性](@entry_id:749023)的联系如下：假设我们的空间离散算子 $\mathcal{L}$ 满足一个**前向欧拉[熵条件](@entry_id:166346)**，即对于足够小的时间步长 $\tau \le \Delta t_{\mathrm{FE}}$，一步前向欧拉更新是熵不增的：
$$
H(\boldsymbol{u}_h + \tau \mathcal{L}(\boldsymbol{u}_h)) \le H(\boldsymbol{u}_h)
$$
由于总离散熵 $H(\boldsymbol{u}_h)$ 是[守恒变量](@entry_id:747720) $\boldsymbol{u}_h$ 的一个[凸函数](@entry_id:143075)，根据**延森不等式 (Jensen's inequality)**，一个凸函数的[凸组合](@entry_id:635830)小于等于其值的凸组合。由于 SSP-RK 的每一步都是前向欧拉步（熵不增）的凸组合，通过对[龙格-库塔](@entry_id:140452)的各个阶段进行归纳，可以证明整个 SSP-RK 步也是熵不增的。这个结论成立的条件是，时间步长 $\Delta t$ 必须满足一个与 SSP 方法的特定系数 $\mathcal{C}_{\mathrm{SSP}}$ 相关的 CFL-类条件：
$$
\Delta t \le \mathcal{C}_{\mathrm{SSP}} \Delta t_{\mathrm{FE}}
$$
这样，我们就将半离散的[熵稳定性](@entry_id:749023)成功地继承到了全离散格式中，从而获得了一个在时间和空间上都具有[非线性](@entry_id:637147)鲁棒性的数值方案 [@problem_id:3380679]。

综上所述，离散熵分析为设计和验证用于[非线性](@entry_id:637147)[双曲系统](@entry_id:260647)的鲁棒[高阶数值方法](@entry_id:142601)提供了一套强大而严谨的理论框架。其核心在于通过 SBP 算子和特殊构造的[数值通量](@entry_id:752791)在离散层面精确模仿连续的熵分析，并将这一稳定性通过 SSP-RK 等[时间积分方法](@entry_id:136323)延伸到全离散层面。