## 引言
在工程与科学领域，准确预测材料在载荷下的行为是结构设计与安全评估的基石。当材料受力超出其[弹性极限](@entry_id:186242)时，便会进入塑性变形阶段，而精确描述这一转变的[临界点](@entry_id:144653)正是**[屈服准则](@entry_id:193897)**的核心任务。然而，从延性金属到压力敏感的土壤，不同材料的屈服机制千差万别，这催生了多种理论模型。对于研究生和工程师而言，理解这些模型的内在原理、[适用范围](@entry_id:636189)及数值实现方法，是弥合理论与实践之间差距的关键。

本文旨在系统性地剖析四种在[弹塑性力学](@entry_id:193198)中具有里程碑意义的屈服准则。我们将在第一章**“原理与机制”**中，首先建立各向同性塑性理论的通用框架，包括[应力不变量](@entry_id:170526)、流动法则和[硬化](@entry_id:177483)机制，随后深入辨析用于金属的Tresca与[von Mises准则](@entry_id:164472)，以及用于岩土材料的Drucker-Prager与Cam-Clay模型。接下来，在第二章**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将展示这些理论模型如何应用于岩土工程和[计算固体力学](@entry_id:169583)等领域，解决从地基稳定到有限元算法收敛性等实际问题。最后，通过第三章**“动手实践”**提供的一系列计算练习，读者将有机会亲手实现和应用这些模型，从而将理论知识转化为扎实的工程技能。

## 原理与机制

本章旨在深入探讨[弹塑性力学](@entry_id:193198)中若干关键[屈服准则](@entry_id:193897)的数学原理与物理机制。我们将从适用于各类材料模型的普适性理论框架出发，系统地阐述各向同性塑性力学的核心概念，包括[应力不变量](@entry_id:170526)、流动法则、[硬化](@entry_id:177483)机制以及[一致性条件](@entry_id:637057)。在此基础上，本章将详细剖析四种具有里程碑意义的屈服准则：两种主要用于描述金属等延性材料、与[静水压力](@entry_id:275365)无关的[Tresca准则](@entry_id:167002)和[von Mises准则](@entry_id:164472)；以及两种主要用于模拟岩土等压力敏感性材料的[Drucker-Prager准则](@entry_id:174815)和Cam-Clay模型。

### 塑性理论的基本概念

在深入研究具体的屈服模型之前，我们必须首先建立一个描述材料从弹性向塑性状态转变的通用理论框架。这一框架基于一系列严谨的数学定义和物理原理，为所有各向同性塑性模型提供了共同的基础。

#### 应力、应变与弹性域

材料的力学行为可以通过其内部的应力状态与变形（应变）之间的关系来描述。对于[弹塑性](@entry_id:193198)材料，其响应可以划分为两个截然不同的区域：弹性区和塑性区。只要材料的应力状态维持在某个特定区域内，其变形就是完全可逆的，这个区域被称为**弹性域**。定义弹性域边界的数学函数，即为**[屈服函数](@entry_id:167970)** (yield function)，通常记为 $f$。屈服准则 $f \le 0$ 明确了所有允许的弹性应力状态。当应力状态达到并试图超越该边界（即 $f=0$ 且有加载趋势）时，材料便开始产生不可恢复的塑性变形。

#### 各向同性塑性中[应力不变量](@entry_id:170526)的角色

对于[各向同性材料](@entry_id:170678)，其材料响应与[坐标系](@entry_id:156346)的选取无关。这意味着屈服准则必须通过不随[坐标系](@entry_id:156346)旋转而改变的量来表达。这些量就是**[应力不变量](@entry_id:170526)** (stress invariants)。在连续介质力学中，任意一点的应力状态由二阶**柯西应力张量** (Cauchy stress tensor) $\boldsymbol{\sigma}$ 描述。为了构建客观的[本构模型](@entry_id:174726)，将 $\boldsymbol{\sigma}$ 分解为其球量部分和偏量部分是至关重要的。

应力张量的球量部分与材料的体积变化相关，通常由**静水压力** (hydrostatic pressure) $p$ 或应力第一[不变量](@entry_id:148850) $I_1$ 来度量：
$$
I_1 = \mathrm{tr}(\boldsymbol{\sigma}) = \sigma_{11} + \sigma_{22} + \sigma_{33}
$$
其中 $\mathrm{tr}(\cdot)$ 表示[张量的迹](@entry_id:190669)。[平均应力](@entry_id:751819)定义为 $p = \frac{1}{3}I_1$。

应力张量的偏量部分，即**[偏应力张量](@entry_id:267642)** (deviatoric stress tensor) $\boldsymbol{s}$，则与材料的形状改变（剪切变形）相关，其定义为：
$$
\boldsymbol{s} = \boldsymbol{\sigma} - \frac{1}{3}I_1\boldsymbol{I}
$$
其中 $\boldsymbol{I}$ 是二阶单位张量。根据定义，[偏应力张量](@entry_id:267642)的迹恒为零，即 $\mathrm{tr}(\boldsymbol{s}) = 0$。

对于各向同性塑性，三个最基本的[应力不变量](@entry_id:170526)是：
1.  **应力第一[不变量](@entry_id:148850)** $I_1$，它正比于[平均应力](@entry_id:751819)。
2.  **[偏应力](@entry_id:163323)第二[不变量](@entry_id:148850)** $J_2$，它度量了偏应力的大小，与剪切应变能相关：
    $$
    J_2 = \frac{1}{2}\boldsymbol{s}:\boldsymbol{s} = \frac{1}{2}\mathrm{tr}(\boldsymbol{s}^2)
    $$
    这里的“$:$”表示张量的[双点积](@entry_id:748648)。
3.  **[偏应力](@entry_id:163323)第三[不变量](@entry_id:148850)** $J_3$，它与[偏应力](@entry_id:163323)的[主应力方向](@entry_id:753737)有关，其定义为 $\boldsymbol{s}$ 的[行列式](@entry_id:142978)：
    $$
    J_3 = \det(\boldsymbol{s})
    $$

这些量之所以被称为“[不变量](@entry_id:148850)”，是因为在任意[正交坐标](@entry_id:166074)变换下（由正交张量 $\boldsymbol{Q}$ 定义，满足 $\boldsymbol{Q}\boldsymbol{Q}^{\mathsf{T}} = \boldsymbol{I}$），应力张量变换为 $\boldsymbol{\sigma}' = \boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}$，但 $I_1$, $J_2$, 和 $J_3$ 的值保持不变。例如，由于迹的循环特性，我们有 $I_1' = \mathrm{tr}(\boldsymbol{Q}\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}) = \mathrm{tr}(\boldsymbol{\sigma}\boldsymbol{Q}^{\mathsf{T}}\boldsymbol{Q}) = \mathrm{tr}(\boldsymbol{\sigma}) = I_1$。类似地，可以证明[偏应力张量](@entry_id:267642)变换为 $\boldsymbol{s}' = \boldsymbol{Q}\boldsymbol{s}\boldsymbol{Q}^{\mathsf{T}}$，从而保证了 $J_2$ 和 $J_3$ 的不变性 [@problem_id:2612486]。因此，任何依赖于这些[不变量](@entry_id:148850)的[屈服函数](@entry_id:167970)都自然地满足了材料的各向同性要求。

#### 通用框架：流动法则、硬化与[一致性条件](@entry_id:637057)

塑性理论的数学结构由一组控制塑性变形演化的基本方程和不等式构成，这通常被称为[Karush-Kuhn-Tucker (KKT) 条件](@entry_id:176491)。这些条件源于[最大塑性耗散](@entry_id:184825)原理，构成了[计算塑性力学](@entry_id:171377)的基石 [@problem_id:2612497]。

1.  **屈服条件**：应力状态必须始终满足 $f(\boldsymbol{\sigma}, \boldsymbol{\kappa}) \le 0$，其中 $\boldsymbol{\kappa}$ 代表一组描述材料历史状态的**内变量** (internal variables)，如塑性应变。

2.  **[流动法则](@entry_id:177163)** (Flow Rule)：当塑性变形发生时，塑性[应变率](@entry_id:154778) $\dot{\boldsymbol{\varepsilon}}^p$ 的方向由**塑性势函数** (plastic potential function) $g(\boldsymbol{\sigma}, \boldsymbol{\kappa})$ 的梯度确定：
    $$
    \dot{\boldsymbol{\varepsilon}}^p = \dot{\lambda} \frac{\partial g}{\partial \boldsymbol{\sigma}}
    $$
    其中 $\dot{\lambda} \ge 0$ 是一个称为**塑性乘子** (plastic multiplier) 的标量，它度量了塑性流动的速率。如果塑性势函数与[屈服函数](@entry_id:167970)相同（$g=f$），则称[流动法则](@entry_id:177163)是**相关的** (associative)。如果 $g \neq f$，则为**不相关** (non-associative) [流动法则](@entry_id:177163)。

3.  **硬化法则** (Hardening Law)：内变量的演化也由塑性乘子驱动，其通用形式为 $\dot{\boldsymbol{\kappa}} = \dot{\lambda} \boldsymbol{H}(\boldsymbol{\sigma}, \boldsymbol{\kappa})$，其中 $\boldsymbol{H}$ 是[硬化](@entry_id:177483)函数。

4.  **加载/卸载[一致性条件](@entry_id:637057)** (Loading/Unloading Consistency Conditions)：这组[互补条件](@entry_id:747558)将塑性流动与[屈服函数](@entry_id:167970)联系起来：
    $$
    \dot{\lambda} \ge 0, \quad f \le 0, \quad \dot{\lambda} f = 0
    $$
    这些条件精炼地描述了塑性行为：只有当应力状态位于[屈服面](@entry_id:175331)上（$f=0$）时，才可能发生塑性流动（$\dot{\lambda} > 0$）；如果应力状态严格处于弹性域内（$f0$），则必无塑性流动（$\dot{\lambda}=0$）。在塑性加载期间，应力点必须维持在[屈服面](@entry_id:175331)上，这要求[屈服函数](@entry_id:167970)的时间变化率 $\dot{f}=0$，这被称为**[一致性条件](@entry_id:637057)** (consistency condition)。

在数值计算（如有限元法）中，这些连续的率形式方程通过**[返回映射算法](@entry_id:168456)** (return-mapping algorithm) 在离散的时间增量步内得以执行。算法的核心思想是“[弹性预测-塑性修正](@entry_id:748860)”：首先假设整个增量步是纯弹性的，计算出一个“试探”应力状态。如果该试探应力点位于[屈服面](@entry_id:175331)之外（$f_{\text{trial}}  0$），则必须进行塑性修正，通过求解一个[非线性方程组](@entry_id:178110)，将应力点“[拉回](@entry_id:160816)”到更新后的屈服面上，同时满足离散化的流动法则和[硬化](@entry_id:177483)法则 [@problem_id:2612497]。

### 压力无关的[金属屈服](@entry_id:195134)准则

许多金属材料在屈服时表现出对静水压力的不敏感性，这意味着它们的屈服行为主要由[偏应力](@entry_id:163323)决定。Von Mises和[Tresca准则](@entry_id:167002)是描述此类行为最经典的两个模型。

#### [von Mises屈服准则](@entry_id:174339)（$J_2$ 塑性）

[von Mises准则](@entry_id:164472)，也称为 $J_2$ 流动理论，假设当偏应力第二[不变量](@entry_id:148850) $J_2$ 达到临界值时材料发生屈服。该准则可以方便地写成**[等效应力](@entry_id:749064)** (equivalent stress) $\sigma_{eq}$ 的形式：
$$
f(\boldsymbol{\sigma}, \kappa) = \sigma_{eq} - \sigma_y(\kappa) = \sqrt{3J_2} - \sigma_y(\kappa) = 0
$$
其中 $\sigma_y(\kappa)$ 是材料当前的单轴屈服强度，它依赖于一个标量[硬化](@entry_id:177483)内变量 $\kappa$（通常是等效塑性应变）。由于该函数仅依赖于 $J_2$，它天然地与静水压力无关 [@problem_id:2612486]。

对于**[各向同性硬化](@entry_id:164486)** (isotropic hardening)，随着塑性变形的累积（$\kappa$ 增加），屈服强度 $\sigma_y(\kappa)$ 单调增长。在[应力空间](@entry_id:199156)中，这表现为[屈服面](@entry_id:175331)以原点为中心、保持形状不变地均匀扩张。这与**[运动硬化](@entry_id:172077)** (kinematic hardening) 形成对比，后者表现为屈服面在[应力空间](@entry_id:199156)中的平移，能够描述[包辛格效应](@entry_id:173790) (Bauschinger effect)，而[各向同性硬化](@entry_id:164486)则不能 [@problem_id:2612510]。

采用相关的[流动法则](@entry_id:177163)（$g=f$），塑性应变率的方向由[屈服函数](@entry_id:167970)的梯度决定。通过链式法则可以推导出：
$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial \sqrt{3J_2}}{\partial \boldsymbol{\sigma}} = \frac{\partial \sqrt{3J_2}}{\partial J_2}\frac{\partial J_2}{\partial \boldsymbol{\sigma}} = \frac{\sqrt{3}}{2\sqrt{J_2}} \boldsymbol{s} = \frac{3}{2\sigma_{eq}}\boldsymbol{s}
$$
这个结果 [@problem_id:2612467] 表明，塑性流动的方向与[偏应力张量](@entry_id:267642) $\boldsymbol{s}$ 共线。由于 $\mathrm{tr}(\boldsymbol{s})=0$，塑性[应变率](@entry_id:154778)的迹也为零：
$$
\mathrm{tr}(\dot{\boldsymbol{\varepsilon}}^p) = \mathrm{tr}\left(\dot{\lambda} \frac{3}{2\sigma_{eq}}\boldsymbol{s}\right) = \dot{\lambda}\frac{3}{2\sigma_{eq}}\mathrm{tr}(\boldsymbol{s}) = 0
$$
这证明了 von Mises 塑性流动是**[体积守恒](@entry_id:276587)**的（即等容流动），这与实验观察到的[金属塑性](@entry_id:176585)变形行为高度吻合 [@problem_id:2612510]。

#### [Tresca屈服准则](@entry_id:190718)（[最大剪应力](@entry_id:181794)）

[Tresca准则](@entry_id:167002)提出了一个更直接的物理图像：当材料内任意平面上的[最大剪应力](@entry_id:181794)达到一个临界值 $k$（称为剪切[屈服强度](@entry_id:162154)）时，材料开始屈服。通过[应力分析](@entry_id:168804)可以证明，[最大剪应力](@entry_id:181794)总是出现在与[主应力方向](@entry_id:753737)成45度角的平面上，其大小等于最大主应力 $\sigma_1$ 和最小[主应力](@entry_id:176761) $\sigma_3$ 之差的一半（假设 $\sigma_1 \ge \sigma_2 \ge \sigma_3$）。因此，[Tresca屈服准则](@entry_id:190718)可写作 [@problem_id:2612537]：
$$
f(\boldsymbol{\sigma}) = \frac{\sigma_1 - \sigma_3}{2} - k = 0
$$
通过分析[单轴拉伸试验](@entry_id:195375)的应力状态（$\sigma_1 = \sigma_y, \sigma_2 = \sigma_3 = 0$），我们可以建立材料参数 $k$ 与单轴[屈服强度](@entry_id:162154) $\sigma_y$ 之间的关系：
$$
\frac{\sigma_y - 0}{2} = k \quad \implies \quad k = \frac{\sigma_y}{2}
$$
这意味着材料的纯剪切屈服强度是其拉伸[屈服强度](@entry_id:162154)的一半 [@problem_id:2612537]。与 von Mises 准则不同，Tresca 准则的数学形式依赖于主应力的排序，这意味着它不仅依赖于 $J_2$，还隐含地依赖于 $J_3$（通过所谓的[Lode角](@entry_id:191590)）[@problem_id:2612486]。

#### 在偏平面上的比较

为了直观地比较这两种准则，我们可以考察它们在**偏平面**（$\pi$-plane）上的几何形状。偏平面是在[主应力空间](@entry_id:184388)中满足 $s_1+s_2+s_3=0$ 的一个平面。

-   **von Mises 准则**在偏平面上是一个**圆形**。其半径 $R = \sqrt{s_1^2+s_2^2+s_3^2} = \sqrt{2J_2}$。当屈服时，$\sqrt{3J_2}=\sigma_y$，所以圆的半径为 $R = \sqrt{2/3}\sigma_y$ [@problem_id:2612460]。

-   **Tresca 准则**在偏平面上是一个**正六边形**。这个六边形的六条边分别对应于六种可能的[主应力](@entry_id:176761)排序下的屈服条件，例如 $s_1-s_3 = 2k$。[@problem_id:2612460]。

这两个几何形状的关系取决于校准方式。如果两种模型被校准为在[单轴拉伸](@entry_id:188287)时给出相同的[屈服应力](@entry_id:274513)，那么von Mises圆将外接于Tresca六边形。这意味着在除单轴应力状态外的所有应力状态下，[Tresca准则](@entry_id:167002)都比[von Mises准则](@entry_id:164472)更为保守（预测的[屈服应力](@entry_id:274513)更低）。Tresca六边形的[外接圆](@entry_id:165300)半径与[内切圆半径](@entry_id:168802)之比恒为 $2/\sqrt{3}$，这反映了其固有的几何特性 [@problem_id:2612460]。由于其数学上的[光滑性](@entry_id:634843)，[von Mises准则](@entry_id:164472)在数值计算中通常更受欢迎，尽管Tresca六边形因其角点和棱的存在，更准确地捕捉了某些晶体滑移行为。

### 压力相关的岩土[材料屈服](@entry_id:751736)准则

与金属不同，土壤、岩石、混凝土等**岩土材料** (geomaterials) 的屈服行为显著依赖于静水压力：压力越大，材料抵抗剪切破坏的能力越强。Drucker-Prager和Cam-Clay模型是描述此类压力敏感性行为的代表。

#### [Drucker-Prager准则](@entry_id:174815)：Mohr-Coulomb的光滑近似

Drucker-Prager (DP) 准则可以看作是经典Mohr-Coulomb (MC) 准则的一个光滑、连续的近似。其[屈服函数](@entry_id:167970)线性地组合了应力第一[不变量](@entry_id:148850) $I_1$ 和偏应力第二[不变量](@entry_id:148850) $J_2$ 的平方根：
$$
f(\boldsymbol{\sigma}) = \alpha I_1 + \sqrt{J_2} - k = 0
$$
其中 $\alpha$ 和 $k$ 是材料常数。$\alpha$ 控制了屈服面对[静水压力](@entry_id:275365)的**敏感性**（类似于摩擦角），而 $k$ 代表了材料在零[静水压力](@entry_id:275365)下的**内聚力**强度 [@problem_id:2612468]。当 $\alpha=0$ 时，DP准则退化为与压力无关的[von Mises准则](@entry_id:164472)。

为了便于与岩[土力学](@entry_id:180264)中的常用变量对接，我们引入平均压应力 $p = -I_1/3$（压应力为正）和等效剪应力 $q=\sqrt{3J_2}$。DP屈服面在 $p-q$ 平面上是一条直线 [@problem_id:2612468]：
$$
q = 3\sqrt{3}\alpha p + \sqrt{3}k
$$
DP模型的参数 $\alpha$ 和 $k$ 可以通过使其直线在特定应力路径（如三轴压缩或三轴拉伸）上与MC准则的[非线性](@entry_id:637147)[包络线](@entry_id:174062)相切或相交来进行标定 [@problem_id:2612468]。

一个关键特性是**[剪胀性](@entry_id:201001)** (dilatancy)，即材料在剪切作用下发生体积膨胀的现象。如果采用相关流动法则，塑性[体积应变率](@entry_id:272471) $\dot{\varepsilon}_v^p$ 与参数 $\alpha$ 直接相关。这导致一个问题：与实验数据相比，相关联的DP模型往往会过度预测剪胀。为了解决这个问题，可以采用**不相关流动法则**，引入一个与[屈服函数](@entry_id:167970) $f$ 不同的塑性[势函数](@entry_id:176105) $g$：
$$
g(\boldsymbol{\sigma}) = \alpha_g I_1 + \sqrt{J_2}
$$
其中，**剪胀参数** $\alpha_g$ 可以独立于摩擦参数 $\alpha$ 进行标定。在这种情况下，塑性[体积应变](@entry_id:267252)仅由 $\alpha_g$ 控制，从而可以更灵活地匹配实验数据 [@problem_id:2612502]。然而，采用不相关[流动法则](@entry_id:177163)的代价是，在[有限元分析](@entry_id:138109)中，算法的**一致性[切线刚度矩阵](@entry_id:170852)**通常会变得非对称，增加了求解的计算成本 [@problem_id:2612502]。

#### [临界状态土力学](@entry_id:748062)：Cam-Clay模型

Cam-Clay模型及其修正形式（Modified Cam-Clay, MCC）是基于**[临界状态土力学](@entry_id:748062)** (Critical State Soil Mechanics, CSSM) 理论发展起来的，专门用于描述饱和土在复杂应力路径下的行为。这些模型统一了土体的剪切和压缩行为，并自然地包含了硬化机制。

MCC模型的[屈服面](@entry_id:175331)在 $p'-q$ 平面上是一个**椭圆**（此处 $p'$ 为有效[平均应力](@entry_id:751819)），其方程为 [@problem_id:2612488]：
$$
f(p', q, p'_c) = \frac{q^2}{M^2} + p'(p' - p'_c) = 0
$$
这里的 $M$ 是[临界状态线](@entry_id:748061)的斜率，一个与土的[内摩擦角](@entry_id:197521)相关的常数。$p'_c$ 是**[前期](@entry_id:170157)固结压力**，它是一个硬化内变量，表征了土体所经历过的最大历史压力，并决定了当前屈服椭圆的大小。

MCC模型的[硬化](@entry_id:177483)机制是其核心特征之一。[硬化](@entry_id:177483)（即屈服面的扩张，$\mathrm{d}p'_c > 0$）是由不可逆的**塑性体积压缩**（$\mathrm{d}\varepsilon_v^p > 0$）驱动的。[硬化](@entry_id:177483)法则将 $p'_c$ 的增量与塑性[体积应变](@entry_id:267252)增量联系起来 [@problem_id:2612534]：
$$
\frac{\mathrm{d}p'_c}{p'_c} = \frac{\mathrm{d}\varepsilon_v^p}{\lambda - \kappa}
$$
其中 $\lambda$ 和 $\kappa$ 分别是土体在 $e-\ln p'$ 平面中正常固结线和回弹线的斜率。几何上， $p'_c$ 的增加会导致整个屈服椭圆以坐标原点为中心进行**相似（或称均匀）扩张**，这是一种典型的[各向同性硬化](@entry_id:164486) [@problem_id:2612534]。

MCC模型的关联[流动法则](@entry_id:177163)预测了非常丰富的行为。屈服椭圆上不同点的法线方向不同，导致[塑性流动](@entry_id:201346)的方向也随应力状态而变：
-   在椭圆的“湿侧”（$p'  p'_c/2$），剪切将伴随着塑性体积压缩（[硬化](@entry_id:177483)）。
-   在椭圆的“干侧”（$p' > p'_c/2$），剪切将伴随着塑性体积膨胀（剪胀），并导致软化（$p'_c$ 减小）。
-   在[椭圆的顶点](@entry_id:167190)（$p' = p'_c/2$），法线方向垂直于 $p'$ 轴。在此特殊点，[塑性流动](@entry_id:201346)是纯剪切的，不产生塑性体积应变（$\mathrm{d}\varepsilon_v^p = 0$）。因此，根据硬化法则，也不会有硬化或软化发生（$\mathrm{d}p'_c=0$），材料表现出[理想塑性](@entry_id:753335)行为 [@problem_id:2612488]。

在数值实现中，虽然MCC的[屈服函数](@entry_id:167970)是光滑可微的，但在椭圆与 $q$ 轴的交点（$p'=0$）处，[屈服面](@entry_id:175331)的曲率无限大，[切线斜率](@entry_id:137445)垂直。这种强烈的[非线性](@entry_id:637147)给[返回映射算法](@entry_id:168456)的收敛带来了挑战，而非函数本身的不[可微性](@entry_id:140863) [@problem_id:2612544]。值得注意的是，[屈服函数](@entry_id:167970)的不同数学表达式，如 $f_1 = q^2 + M^2 p'(p' - p'_c)$ 和 $f_2 = \frac{q^2}{M^2} + p'(p' - p'_c)$，虽然代数形式不同（$f_1=M^2 f_2$），但它们定义了完全相同的屈服轨迹，并且由于其梯度向量共线，它们在关联塑性框架下描述的是完全相同的物理模型 [@problem_id:2612544]。