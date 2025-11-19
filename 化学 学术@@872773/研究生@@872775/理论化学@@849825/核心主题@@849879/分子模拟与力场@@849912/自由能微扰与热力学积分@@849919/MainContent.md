## 引言
自由能是化学和生物学中的核心[热力学](@entry_id:141121)量，它决定了反应的自发方向、分子的结合亲和力以及[相变](@entry_id:147324)的平衡条件。分子模拟，特别是[分子动力学](@entry_id:147283)（MD）和[蒙特卡洛](@entry_id:144354)（MC）方法，为我们提供了一个从原子尺度理解宏观现象的强大窗口。然而，一个根本性的挑战在于，直接从模拟中计算绝对自由能几乎是不可能的。幸运的是，在科学研究中，我们更关心的往往是状态之间的**自由能差**，例如，一个分子的化学修饰如何影响其与靶蛋白的结合强度。

[自由能微扰](@entry_id:165589) (Free Energy Perturbation, FEP) 和[热力学积分](@entry_id:156321) (Thermodynamic Integration, TI) 正是为解决这一问题而发展的两种基石性计算方法。它们通过巧妙的[统计力](@entry_id:194984)学构建，允许我们沿着一条计算上可行的非物理（“炼金术”）路径，精确地计算两个明确定义的物理状态之间的自由能差，从而架起了微观模拟与宏观实验测量之间的桥梁。

本文将系统性地引导您深入理解这两种强大的技术。在第一部分“原理与机制”中，我们将回顾自由能的[统计力](@entry_id:194984)学基础，推导FEP和TI的核心方程，并剖析它们在实践中面临的统计挑战，如相空间重叠问题和收敛性偏差。接下来，在“应用与跨学科连接”部分，我们将通过一系列来自[药物设计](@entry_id:140420)、免疫学、[材料科学](@entry_id:152226)等领域的真实案例，展示这些方法如何被用于解决复杂的科学问题。最后，“动手实践”部分将提供一系列精心设计的练习，帮助您将理论知识转化为解决实际问题的计算技能。

## Principles and Mechanisms

### 自由能的[统计力](@entry_id:194984)学基础 (Statistical Mechanical Foundations of Free Energy)

在[统计力](@entry_id:194984)学中，系统的宏观热力学性质源于其微观状态的集合行为。对于一个处于恒定粒子数 $N$、体积 $V$ 和温度 $T$ 的正则系综 (canonical ensemble) 中的经典系统，其核心的热力学势是亥姆霍兹自由能 (Helmholtz free energy)，通常表示为 $F$ (或 $A$)。它通过以下基本关系与系统的[配分函数](@entry_id:193625) $Z$ 相联系：

$F = -k_B T \ln Z$

其中，$k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是绝对温度。[正则配分函数](@entry_id:154330) $Z$ 是对系统所有可能微观状态的[玻尔兹曼因子](@entry_id:141054)进行积分或求和，它囊括了系统在[热平衡](@entry_id:141693)时的所有统计信息。对于一个由位置坐标 $\mathbf{q}$ 和动量坐标 $\mathbf{p}$ 描述的经典系统，其[配分函数](@entry_id:193625)定义为：

$Z = \frac{1}{N! h^{3N}} \int d^{3N}\mathbf{p} \int d^{3N}\mathbf{q} \, \exp\left(-\frac{H(\mathbf{p}, \mathbf{q})}{k_B T}\right)$

在这里，$H(\mathbf{p}, \mathbf{q})$ 是系统的[哈密顿量](@entry_id:172864)，即总能量。因子 $N!$ 用于修正粒子的不可区分性，$h$ 是具有作用量纲的常数（通常取[普朗克常数](@entry_id:139373)），用于使相空间体积无量纲化。

在计算化学中，我们通常更关心的是状态之间的**自由能差**，而非绝对自由能。例如，考虑两个由不同[势能函数](@entry_id:200753) $U_A$ 和 $U_B$ 描述的炼金术终态 (alchemical end states) A 和 B。它们之间的亥姆霍兹自由能差 $\Delta F_{B \leftarrow A}$ 定义为：

$\Delta F_{B \leftarrow A} = F_B - F_A = -k_B T \ln\left(\frac{Z_B}{Z_A}\right)$

在实践中，我们几乎总是计算自由能差，因为对于[经典力场](@entry_id:747367)描述的凝聚相系统，计算绝对自由能是不可行且无物理意义的。这主要有两个根本原因 [@problem_id:2774301]。首先，[经典势能函数](@entry_id:747368) $U(\mathbf{q})$ 总是可以加上一个任意的常数 $C$ 而不改变其物理性质，因为力（势能的负梯度）保持不变。然而，这个常数 $C$ 会使绝对自由能 $F$ 平移相同的量（$F' = F+C$）。在计算自由能差时，这个任意的常数会被抵消，使得差值成为一个物理上[可观测量](@entry_id:267133)。其次，[配分函数](@entry_id:193625)定义中的常数 $h$ 在纯经典力学中没有唯一的理论依据，其选择是约定俗成的。改变 $h$ 的值会改变绝对自由能，但同样不会影响自由能差。因此，计算方法如[自由能微扰](@entry_id:165589) (FEP) 和[热力学积分](@entry_id:156321) (TI) 的目标始终是计算这种不变的自由能差。

### 从系综到轨迹：[遍历性假设](@entry_id:147104) (From Ensembles to Trajectories: The Ergodic Hypothesis)

上述[统计力](@entry_id:194984)学公式涉及对整个相空间（系综）的积分，这在计算上是无法实现的。实际的[分子模拟](@entry_id:182701)，无论是[分子动力学](@entry_id:147283) (MD) 还是蒙特卡洛 (MC)，都是通过生成系统随[时间演化](@entry_id:153943)的一系列构象（一条轨迹）来探索相空间。因此，为了使模拟具有实际意义，我们需要一个理论桥梁，将基于轨迹的时间平均值与理论上的系综平均值联系起来。这个桥梁就是**[遍历性假设](@entry_id:147104)** (ergodic hypothesis) [@problem_id:2774311]。

将系综平均值 $\langle f \rangle_A = \int f(x) \rho_A(x) dx$（其中 $\rho_A(x)$ 是状态A的[平衡概率](@entry_id:187870)密度）替换为[时间平均](@entry_id:267915)值 $\frac{1}{\mathcal{T}} \int_0^{\mathcal{T}} f(X_t) dt$（其中 $X_t$ 是 $t$ 时刻的构象，$\mathcal{T}$ 是总模拟时间）的合法性，依赖于几个关键的数学假设：

1.  **不变性 (Invariance) 和[平稳性](@entry_id:143776) (Stationarity)**：用于采样的动力学过程（如[朗之万动力学](@entry_id:142305)或Nose-Hoover恒温动力学）必须以目标[平衡分布](@entry_id:263943) $\rho_A$ 作为其[不变测度](@entry_id:202044)。这意味着一旦系统达到平衡，其统计性质将不随[时间演化](@entry_id:153943)。在实践中，我们通过舍弃模拟初始阶段的“弛豫”或“平衡”过程来实现这一点，使得后续的轨迹是平稳的。

2.  **遍历性 (Ergodicity)**：[平稳过程](@entry_id:196130)必须是遍历的。这意味着系统在足够长的时间内，将以正确的概率访问所有可及的微观状态。从形式上讲，任何在动力学演化下保持不变的相空间[子集](@entry_id:261956)，其测度（概率）必须为0或1。遍历性保证了单条轨迹能够充分代表整个系综，从而使得时间平均值在 $\mathcal{T} \to \infty$ 的极限下[几乎必然收敛](@entry_id:265812)于系综平均值。

3.  **可积性 (Integrability)**：被平均的观测量 $f(x)$ 必须是可积的，即 $\int |f(x)| \rho_A(x) dx \lt \infty$。对于FEP中的指数项或TI中的[能量导数](@entry_id:170468)，这通常在物理系统中是满足的，但当遇到奇异行为（如下文的“端点灾难”）时，这一条件可能会被破坏。

在满足这些条件下，[Birkhoff遍历定理](@entry_id:276508)保证了时间平均值会收敛到系综平均值。因此，分子模拟的全部实践都隐含地依赖于所用算法的遍历性，它构成了连接理论公式与计算实践的基石。

### 计算自由能的核心方程：微扰与积分

基于上述[统计力](@entry_id:194984)学框架，发展出了两种计算自由能差的主流方法：[自由能微扰](@entry_id:165589) (FEP) 和[热力学积分](@entry_id:156321) (TI)。它们都始于相同的基本原理，但通过不同的数学路径来实现目标 [@problem_id:2453017]。

#### [自由能微扰](@entry_id:165589) (Free Energy Perturbation, FEP)

FEP源于Robert Zwanzig在1954年推导出的一个惊人地简洁而精确的关系。我们从自由能差的定义出发：

$\Delta F = F_B - F_A = -k_B T \ln\left(\frac{Z_B}{Z_A}\right)$

通过一个简单的代数技巧，我们可以将[配分函数](@entry_id:193625)之比表示为在状态A系综下的平均值：

$\frac{Z_B}{Z_A} = \frac{\int e^{-\beta U_B} d\mathbf{q}}{\int e^{-\beta U_A} d\mathbf{q}} = \frac{\int e^{-\beta (U_A + U_B - U_A)} d\mathbf{q}}{Z_A} = \int e^{-\beta (U_B - U_A)} \frac{e^{-\beta U_A}}{Z_A} d\mathbf{q}$

右侧的积分正是[玻尔兹曼因子](@entry_id:141054) $e^{-\beta \Delta U}$ 在状态A系综下的平均值，其中 $\Delta U = U_B - U_A$。因此，我们得到了**[Zwanzig方程](@entry_id:176184)**，也即FEP的核心公式 [@problem_id:2642310] [@problem_id:2774315]：

$\Delta F = -k_B T \ln \left\langle e^{-\beta (U_B - U_A)} \right\rangle_A$

这个方程意味着，原则上我们只需在一个状态（例如初始态A）进行模拟采样，然后计算两个状态之间势能差的指数的平均值，就可以直接得到它们之间的自由能差。这种方法被称为“前向”FEP。类似地，我们也可以从状态B采样来计算自由能差，这被称为“后向”FEP：

$-\Delta F = F_A - F_B = -k_B T \ln \left\langle e^{-\beta (U_A - U_B)} \right\rangle_B = -k_B T \ln \left\langle e^{\beta \Delta U} \right\rangle_B$

FEP的优雅之处在于其形式上的直接性，但其成功与否极度依赖于两个状态在相空间中的重叠程度。

#### [热力学积分](@entry_id:156321) (Thermodynamic Integration, TI)

与FEP的“一步跳跃”不同，TI采用了一种更为循序渐进的策略。它引入了一个[耦合参数](@entry_id:747983) $\lambda$，将系统的势能函数 $U(\lambda)$ 定义为初始态 $U_A$ 和终末态 $U_B$ 之间的平滑过渡，其中 $\lambda$ 从0变化到1。一个常见的选择是线性插值：$U(\lambda) = (1-\lambda)U_A + \lambda U_B$。

自由能 $F(\lambda)$ 现在是 $\lambda$ 的函数。总的自由能差可以通过对 $F(\lambda)$ 的导数进行积分得到：

$\Delta F = F(1) - F(0) = \int_{0}^{1} \frac{dF(\lambda)}{d\lambda} d\lambda$

利用 $F(\lambda) = -k_B T \ln Z(\lambda)$ 和[链式法则](@entry_id:190743)，我们可以推导出导数 $\frac{dF}{d\lambda}$ 的表达式 [@problem_id:2642310]：

$\frac{dF(\lambda)}{d\lambda} = -k_B T \frac{1}{Z(\lambda)} \frac{dZ(\lambda)}{d\lambda} = -k_B T \frac{1}{Z(\lambda)} \int \left(-\beta \frac{\partial U(\lambda)}{\partial \lambda}\right) e^{-\beta U(\lambda)} d\mathbf{q} = \left\langle \frac{\partial U(\lambda)}{\partial \lambda} \right\rangle_\lambda$

这个优美的结果表明，自由能对 $\lambda$ 的导数恰好等于势能对 $\lambda$ 的导数在对应 $\lambda$ 系综下的平均值。这个平均值 $\langle \frac{\partial U}{\partial \lambda} \rangle_\lambda$ 在物理上可以被解释为维持系统状态不变时，抵抗 $\lambda$ 变化的“[广义力](@entry_id:169699)”。

将此结果代入积分，我们得到**[热力学积分](@entry_id:156321) (TI) 公式**：

$\Delta F = \int_{0}^{1} \left\langle \frac{\partial U(\lambda)}{\partial \lambda} \right\rangle_\lambda d\lambda$

在实践中，TI的计算过程包括：(1) 选择一系列离散的 $\lambda$ 值（例如 $\lambda_1, \lambda_2, \dots, \lambda_m$）；(2) 在每个 $\lambda_i$ 值下运行一次独立的模拟，以计算平均[广义力](@entry_id:169699) $\langle \frac{\partial U}{\partial \lambda} \rangle_{\lambda_i}$；(3) 使用[数值积分方法](@entry_id:141406)（如梯形法则或高斯求积）根据这些离散点估算整个积分的值。

### 统计挑战与收敛性问题

尽管FEP和TI的公式在理论上是精确的，但它们的实际应用充满了统计上的挑战。这些挑战的核心在于有限的模拟时间所带来的采样不充分问题。

#### 相空间重叠的重要性

FEP和TI的收敛效率都与不同状态（或相邻 $\lambda$ 窗口）之间**[相空间分布](@entry_id:151304)的重叠度**密切相关 [@problem_id:2642327]。我们可以用一个量化的指标来定义两个[概率分布](@entry_id:146404) $\pi_0(x)$ 和 $\pi_1(x)$ 之间的重叠 $O$：

$O \equiv \int \min\big(\pi_0(x), \pi_1(x)\big) dx$

这个值的范围在0（完全无重叠）和1（[分布](@entry_id:182848)相同）之间。

对于FEP，如果状态A和B的重叠度很低，意味着在状态A的模拟中，那些对状态B很重要的构象（即 $\pi_B$ 很大的区域）出现的概率极低（即 $\pi_A$ 很小）。根据FEP公式，这些罕见构象的[玻尔兹曼权重](@entry_id:137515) $e^{-\beta \Delta U}$ 会变得异常巨大。因此，FEP的平均值将被极少数的罕见事件所主导，导致其统计[方差](@entry_id:200758)极大，收敛极其缓慢。在最坏的情况下，如果状态B的重要区域在状态A中采样的概率为零，FEP的估计将是有偏的，永远无法收敛到正确结果。

对于TI，相空间重叠问题表现为**滞后效应 (hysteresis)**。当沿 $\lambda$ 路径从0到1（正向）和从1到0（反向）进行积[分时](@entry_id:274419)，如果相邻 $\lambda_i$ 和 $\lambda_{i+1}$ 窗口之间的重叠很小，那么在从 $\lambda_i$ 切换到 $\lambda_{i+1}$ 后，系统需要很长的模拟时间才能从旧的平衡态弛豫到新的[平衡态](@entry_id:168134)。在有限的模拟时间内，系统会“滞后”于其[平衡态](@entry_id:168134)，导致计算出的 $\langle \frac{\partial U}{\partial \lambda} \rangle$ 存在系统性误差。这种误差在正向和反向积分中通常方向相反，从而导致 $\Delta F_{\text{forward}} \neq -\Delta F_{\text{reverse}}$。滞后的大小是衡量TI模拟收敛性的一个重要指标。

#### [热力学积分](@entry_id:156321)中的“端点灾难”

相空间重叠问题在[炼金术计算](@entry_id:176497)中有一个臭名昭著的实例，即“端点灾难” (end-point catastrophe)，它在使用简单的线性插值势进行原子凭空“创生”或“湮灭”时尤为突出 [@problem_id:2774304]。

考虑一个场景：我们通过[线性缩放](@entry_id:197235)一个溶质与溶剂之间的Lennard-Jones (LJ) 相互作用来计算其[水合自由能](@entry_id:178818)，即 $U(\lambda) = \lambda U_{\text{LJ}}$。这里的 $U_A = U(\lambda=0)$ 是一个完全不相互作用的“幽灵”粒子，而 $U_B = U(\lambda=1)$ 是一个具有完整LJ相互作用的真实粒子。TI的积分为 $\langle \frac{\partial U}{\partial \lambda} \rangle_\lambda = \langle U_{\text{LJ}} \rangle_\lambda$。

当 $\lambda \to 0$ 时，溶[质粒](@entry_id:263777)子与溶剂分子的排斥作用变得极弱。在 $\lambda$ 系综的模拟中，溶剂分子可以以不可忽略的概率运动到与溶[质粒](@entry_id:263777)子核心非常接近的位置（$r \to 0$）。在这些构象下，$U_{\text{LJ}}(r)$ 由于其 $r^{-12}$ 的排斥项而趋于正无穷。尽管这些构象在有限但非零的 $\lambda$ 下的[玻尔兹曼权重](@entry_id:137515) $e^{-\beta \lambda U_{\text{LJ}}}$ 会受到抑制，但积分 $\langle U_{\text{LJ}} \rangle_\lambda$ 仍然会发散。

通过更严谨的[数学分析](@entry_id:139664)可以证明 [@problem_id:2774290]，对于三维空间中的LJ势，当 $\lambda \to 0^+$ 时，TI的积分项会以 $\lambda^{-3/4}$ 的形式发散。这种在路径端点的奇异行为使得数值积分极为困难，需要极密集的 $\lambda$ 窗口来捕捉这种急剧变化，这正是“端点灾难”的由来。

#### [自由能微扰](@entry_id:165589)中的系统性偏差

除了[方差](@entry_id:200758)巨大之外，有限采样的FEP估计还存在固有的**系统性偏差** [@problem_id:2774315]。这一偏差可以通过[Jensen不等式](@entry_id:144269)来揭示。对于一个[凸函数](@entry_id:143075) $\phi(x)$，我们有 $\langle \phi(X) \rangle \ge \phi(\langle X \rangle)$。

对于前向FEP估计 $\widehat{\Delta F}_{F} = -k_B T \ln \left( \frac{1}{n_0} \sum_i e^{-\beta \Delta U_i} \right)$，由于函数 $f(x) = -\ln(x)$ 是一个凸函数，应用[Jensen不等式](@entry_id:144269)于样本均值上可得：

$\mathbb{E}[\widehat{\Delta F}_{F}] = -k_B T \mathbb{E}\left[ \ln\left( \frac{1}{n_0}\sum_i e^{-\beta \Delta U_i} \right) \right] \ge -k_B T \ln\left( \mathbb{E}\left[ \frac{1}{n_0}\sum_i e^{-\beta \Delta U_i} \right] \right) = -k_B T \ln\left( \langle e^{-\beta \Delta U} \rangle_A \right) = \Delta F$

这意味着，对于有限的样本量，前向FEP估计值的[期望值](@entry_id:153208)总是大于或等于真实的自由能差 $\Delta F$，即它具有正向偏差（或向上偏差）。

同理，对于反向FEP估计 $\widehat{\Delta F}_{R} = k_B T \ln \left( \frac{1}{n_1} \sum_j e^{\beta \Delta U_j} \right)$，由于函数 $g(x) = \ln(x)$ 是一个[凹函数](@entry_id:274100)，应用[Jensen不等式](@entry_id:144269)可得 $\mathbb{E}[\widehat{\Delta F}_{R}] \le \Delta F$。这意味着反向FEP估计具有负向偏差（或向下偏差）。

这两种方向相反的偏差再次反映了采样问题 [@problem_id:2774303]。例如，在[前向计算](@entry_id:193086)中，有限的采样总是会低估那些能量差 $\Delta U$ 很小的罕见事件的贡献，从而低估[指数平均](@entry_id:749182)值 $\langle e^{-\beta \Delta U} \rangle_A$，最终导致对 $\Delta F$ 的高估。

### 高级方法与实用解决方案

为了克服上述挑战，研究人员开发了多种更为先进和稳健的计算策略。

#### 双向方法：[Bennett接受率](@entry_id:175184)方法

既然前向和后向FEP具有方向相反的偏差，一个自然的想法是结合两个方向的采样信息来获得一个更好的估计。**[Bennett接受率](@entry_id:175184)方法 (Bennett Acceptance Ratio, BAR)** 就是这类双向方法中最著名和最高效的一种 [@problem_id:2774303]。

BAR通过求解一个[自洽方程](@entry_id:155949)来得到自由能差 $\Delta F$，这个方程巧妙地结合了来自状态A和状态B的采样数据。其核心思想是找到一种最优的方式来组合两个方向的信息，从而最小化最终估计的[方差](@entry_id:200758)。BAR的方程可以写作：

$\Delta F = k_B T \ln \frac{\left\langle f(\Delta U - \Delta F) \right\rangle_B}{\left\langle f(-\Delta U + \Delta F) \right\rangle_A} + \Delta F$

其中 $f(x) = (1+e^{\beta x})^{-1}$ 是[费米-狄拉克分布](@entry_id:138909)函数。这个方程需要迭代求解 $\Delta F$。

BAR的优越性在于，它对来自两个系综的样本进行对称的、最优的加权。它有效地利用了相空间重叠区域的信息，而不是像单向FEP那样只依赖于一个[分布](@entry_id:182848)的“尾巴”去探索另一个[分布](@entry_id:182848)的核心区域。因此，BAR不仅[方差](@entry_id:200758)远小于FEP，其系统性偏差也显著减小，成为目前最为精准和高效的[自由能计算](@entry_id:164492)方法之一 [@problem_id:2642327]。

#### [软核势](@entry_id:191962)：解决端点灾难

为了解决TI中的端点灾难问题，标准做法是修改炼金路径，使用所谓的**[软核势](@entry_id:191962) (soft-core potentials)** [@problem_id:2642331]。其核心思想是在 $\lambda$ 较小时，[对相互作用势](@entry_id:140875)的短程部分进行“软化”，使其在 $r \to 0$ 时保持有限，从而避免积分发散。

一种常见的[软核势](@entry_id:191962)形式如下：

$U_{\text{LJ}}^{\text{sc}}(r;\lambda) = 4\epsilon\left[ \left(\frac{\sigma^6}{\alpha(1-\lambda) + r^6}\right)^2 - \left(\frac{\sigma^6}{\alpha(1-\lambda) + r^6}\right) \right]$

这里的 $\alpha$ 是一个正常数。让我们分析这个势函数如何工作：

-   当 $\lambda=1$ 时，$\alpha(1-\lambda)=0$，该[势函数](@entry_id:176105)精确地还原为标准的LJ势，保证了路径的终点是物理真实的。
-   当 $\lambda  1$ 时，即使 $r \to 0$，分母 $\alpha(1-\lambda) + r^6$ 也会趋向于一个正的常数 $\alpha(1-\lambda)$，而不是零。这使得[势能](@entry_id:748988)及其对 $\lambda$ 的导数在 $r=0$ 处保持有限。
-   在长程 $r \to \infty$ 时，常数项 $\alpha(1-\lambda)$ 可以忽略不计，[势函数](@entry_id:176105)行为与标准LJ势一致。

通过引入这种依赖于 $\lambda$ 的软化项，我们构建了一条从“软核”粒子到“硬核”LJ粒子的平滑路径。这有效地消除了端点灾难，使得TI的积分在整个 $\lambda$ 区间内都表现良好，大大提高了计算的稳定性和效率。

### 选择合适的工具：系综与[热力学势](@entry_id:140516)

最后，一个关键的实践问题是：我们应该计算[亥姆霍兹自由能](@entry_id:136442)差 $\Delta A$ 还是吉布斯自由能差 $\Delta G$？这取决于我们模拟的系综以及我们希望与何种实验条件进行比较 [@problem_id:2642321]。

-   **正则系综 ($NVT$)**：在恒定粒子数、体积和温度下进行模拟，其自然的热力学势是亥姆霍兹自由能 $A$。因此，在 $NVT$ 系综中进行FEP或TI计算，直接得到的是 $\Delta A$。
-   **[等温等压系综](@entry_id:143530) ($NpT$)**：在恒定粒子数、压强和温度下进行模拟，其自然的热力学势是[吉布斯自由能](@entry_id:146774) $G$。在 $NpT$ 系综中进行计算，直接得到的是 $\Delta G$。

两者的关系是 $G = A + pV$。因此，$\Delta G = \Delta A + \Delta(pV)$。

大多数化学和[生物过程](@entry_id:164026)，如[配体](@entry_id:146449)与蛋白质的结合、分子的[溶剂化](@entry_id:146105)或[相变](@entry_id:147324)，都是在恒定的温度和压强下发生的。因此，实验上可测量的自由能通常是[吉布斯自由能](@entry_id:146774)差 $\Delta G$。

-   **溶剂化与结合过程**：计算[溶剂化自由能](@entry_id:174814)或配体[结合自由能](@entry_id:166006)时，最直接的方法是在 $NpT$ 系综中进行模拟，直接计算 $\Delta G$。如果由于技术原因（例如，为了维持稳定的模拟盒子）在 $NVT$ 系综中进行计算，那么得到的 $\Delta A$ 必须经过修正（例如，加上 $p\Delta V$ 项和其它[有限尺寸效应](@entry_id:155681)的修正）才能与实验的 $\Delta G$ 值进行比较。

-   **相平衡**：确定两种物相（如固相和液相）在给定压强下的共存温度，其[热力学](@entry_id:141121)判据是两相的摩尔吉布斯自由能（即化学势 $\mu$）相等：$\mu_{\alpha}(T, p) = \mu_{\beta}(T, p)$。因此，最自然的方法是在 $NpT$ 系综中分别计算两相的 $\Delta G$，并找到它们的交点。虽然也可以在 $NVT$ 系综中通过计算 $\Delta A$ 并使用麦克斯韦[公切线构造](@entry_id:187353)来确定共存条件，但这会确定一个内蕴的共存压强，而不是我们预先设定的压强，使得与实验比较更为间接。

综上所述，虽然 $NVT$ 模拟在技术上可能更简单，但对于大多数与真实世界实验对比的应用场景，$NpT$ 系综和吉布斯自由能 $G$ 是更基本、更直接的目标物理量。理解不同系综与其对应的热力学势之间的关系，对于正确设计和解读[自由能计算](@entry_id:164492)至关重要 [@problem_id:2642310]。