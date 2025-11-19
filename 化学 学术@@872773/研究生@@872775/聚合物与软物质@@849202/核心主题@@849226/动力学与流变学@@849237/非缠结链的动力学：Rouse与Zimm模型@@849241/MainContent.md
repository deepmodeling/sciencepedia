## 引言
柔性聚合物链的动力学行为，即它们如何随时间运动和改变构象，是理解[高分子](@entry_id:150543)材料宏观性质（如粘弹性、[扩散](@entry_id:141445)性）和许多[生物过程](@entry_id:164026)（如[染色质组织](@entry_id:174540)）的基础。然而，从[单体](@entry_id:136559)的微观热运动到整条长链的集体行为，其间存在着巨大的时空尺度鸿沟，构成了高分子物理学中的一个核心挑战。为了跨越这一鸿沟，理论物理学家发展了一系列简化但功能强大的模型，其中，[Rouse模型](@entry_id:194732)和[Zimm模型](@entry_id:201998)是描述无缠结聚合物链动力学的两大基石。

本文旨在系统性地阐述这两种经典模型。我们将首先在“原理与机制”一章中，从基础的[珠簧模型](@entry_id:199502)出发，详细推导[Rouse模型](@entry_id:194732)（无[流体力学](@entry_id:136788)相互作用）和[Zimm模型](@entry_id:201998)（有[流体力学](@entry_id:136788)相互作用）的物理图像和数学形式，并解释浓度增加如何通过“筛选效应”导致两种动力学行为之间的过渡。接下来，在“应用与交叉学科联系”一章中，我们将展示这些模型如何应用于预测实验可观测的量（如[扩散](@entry_id:141445)系数和[弛豫谱](@entry_id:192983)），并探讨它们在[生物物理学](@entry_id:154938)、分析技术和[材料科学](@entry_id:152226)等前沿领域的深刻影响。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者通过计算和推导，巩固对这些核心概念的理解。通过这三个层次的深入学习，读者将构建起一个关于无缠结链动力学的完整理论框架。

## 原理与机制

本章旨在阐述无缠结聚合物链动力学的基本原理与核心机制。我们将从最基础的[珠簧模型](@entry_id:199502)出发，逐步建立描述[聚合物动力学](@entry_id:146985)的两大经典模型——[Rouse模型](@entry_id:194732)和[Zimm模型](@entry_id:201998)。随后，我们将探讨这些模型如何预测链的内部运动模式及其在实验中的体现。最后，我们将引入“筛选”这一关键概念，以统一的物理图像来理解聚合物如何从稀溶液过渡到[半稀溶液](@entry_id:185434)，并展示其动力学行为的深刻转变。

### 基本概念：[珠簧模型](@entry_id:199502)

为了在理论上处理柔性长链分子的复杂运动，我们采用一种**粗粒化**（coarse-graining）方法，将聚合物链简化为一个**[珠簧模型](@entry_id:199502)**（bead-spring model）。在此模型中，整条链被视为由$N$个“珠子”通过无质量的“弹簧”连接而成。每个珠子代表一个Kuhn链段，它包含了足够多的化学[单体](@entry_id:136559)，使得链段间的取向变得不相关。这些珠子在粘性溶剂中进行布朗运动，其行为受到三种基本作用力的支配：来自溶剂的[摩擦力](@entry_id:171772)、随机热涨落力以及来自相邻珠子的[熵弹簧](@entry_id:136248)力。

#### [摩擦力](@entry_id:171772)、[扩散](@entry_id:141445)与爱因斯坦关系

当一个珠子以速度$\mathbf{v}$在溶剂中运动时，它会受到与运动方向相反的阻力，即**[摩擦力](@entry_id:171772)**（frictional force）。在低雷诺数下（[聚合物动力学](@entry_id:146985)中通常满足此条件），该力与速度成正比。因此，我们可以定义一个**[单体](@entry_id:136559)摩擦系数**$\zeta$，它是在[线性响应区](@entry_id:751325)域内描述耗散的比例常数 [@problem_id:3010799]：
$$
\langle \mathbf{F}_{\mathrm{drag}} \rangle = -\zeta \mathbf{v}
$$
这个摩擦系数$\zeta$源于珠子与周围溶剂分子或其它聚合物链段在微观时间尺度上的无数次碰撞和相互作用。

与此同时，热能使得珠子永不停歇地进行随机运动，即**布朗运动**。这种运动的剧烈程度由[扩散](@entry_id:141445)系数$D_b$来量化。系统的涨落（[扩散](@entry_id:141445)）与耗散（摩擦）并非相互独立，它们通过著名的**爱因斯坦关系**（Einstein relation）联系在一起 [@problem_id:3010799]：
$$
D_b = \frac{k_{\mathrm{B}} T}{\zeta}
$$
其中$k_{\mathrm{B}}$是[玻尔兹曼常数](@entry_id:142384)，$T$是绝对温度。这个关系是**涨落-耗散定理**（fluctuation-dissipation theorem）的一个重要体现，它构成了后续动力学模型的[热力学](@entry_id:141121)基础。

值得注意的是，对于稀溶液中的一个孤立珠子，其[摩擦系数](@entry_id:150354)$\zeta$通常可以用[斯托克斯定律](@entry_id:147173)近似，即$\zeta = 6 \pi \eta_s a$，其中$\eta_s$是[溶剂粘度](@entry_id:264247)，$a$是珠子的[流体力学](@entry_id:136788)半径。然而，在浓溶液或熔体中，情况变得更为复杂。长程的[流体力学](@entry_id:136788)效应被周围的链段所“筛选”，导致[斯托克斯定律](@entry_id:147173)失效。此时，$\zeta$应被视为一个由局部微环境决定的有效参数 [@problem_id:3010799]。

#### 随机力与涨落-耗散定理

驱动珠子进行布朗运动的**随机力**（random force）$\boldsymbol{\eta}(t)$来源于溶剂分子的无规则热碰撞。这个力在时间上是高度不相关的（可视为[白噪音](@entry_id:145248)），且其平均值为零。涨落-耗散定理给出了随机力涨落的强度。对于一个孤立的珠子，其随机力在不同笛卡尔分量（以$i, j$表示）和不同时间点上的关联函数为 [@problem_id:3010799]：
$$
\langle \eta_i(t) \eta_j(t') \rangle = 2 k_{\mathrm{B}} T \zeta \delta_{ij} \delta(t-t')
$$
这个公式精确地表明，系统的耗散越大（$\zeta$越大），驱动其平衡涨落的随机力也越强。

#### [熵弹簧](@entry_id:136248)

连接珠子的“弹簧”并非机械弹簧，而是一种**[熵弹簧](@entry_id:136248)**（entropic spring）。它的恢复力源于[热力学第二定律](@entry_id:142732)：当两个相邻珠子被拉开或推近，偏离其平均距离时，它们之间链段构象的数量减少，导致熵降低。系统为抵抗这种熵的降低而产生一个有效的恢复力。

对于满足高斯统计的[理想链](@entry_id:196640)，两个相邻珠子（例如第$n$和$n-1$个）之间的有效弹性势能可以表示为 [@problem_id:3010812]：
$$
U_{n-1, n} = \frac{3 k_{\mathrm{B}} T}{2 b^2} (\mathbf{R}_n - \mathbf{R}_{n-1})^2
$$
其中$\mathbf{R}_n$是第$n$个珠子的位置矢量，$b$是Kuhn长度。由此，我们可以定义[熵弹簧](@entry_id:136248)的**[弹簧常数](@entry_id:167197)**$k_s$为：
$$
k_s = \frac{3 k_{\mathrm{B}} T}{b^2}
$$
这个[弹簧常数](@entry_id:167197)与温度成正比，体现了其熵的本质：温度越高，熵效应越强，链段抵抗形变的能力也越强。

### [Rouse模型](@entry_id:194732)：无[流体力学](@entry_id:136788)相互作用的动力学

**[Rouse模型](@entry_id:194732)**是描述[聚合物动力学](@entry_id:146985)最简单的模型，其核心假设是完全忽略珠子之间的**[流体力学](@entry_id:136788)相互作用**（hydrodynamic interaction, HI）。这被称为**自由排干**（free-draining）极限，即溶剂可以无阻碍地流过聚合物线团。此外，[Rouse模型](@entry_id:194732)也忽略了**排斥体积效应**，将链视为可以自由相互穿越的“幻影链”（phantom chain）。

在这些假设下，第$n$个珠子的运动仅受其自身与溶剂的相互作用（[摩擦力](@entry_id:171772)和随机力）以及来自直接相邻珠子的[熵弹簧](@entry_id:136248)力的影响。其运动方程（Langevin方程）在[过阻尼极限](@entry_id:161869)下（忽略惯性项）由力的平衡给出 [@problem_id:3010812]：
$$
\mathbf{F}_{\mathrm{friction}, n} + \mathbf{F}_{\mathrm{spring}, n} + \boldsymbol{\eta}_n(t) = \mathbf{0}
$$
将前一节定义的各项力代入，我们得到[Rouse模型](@entry_id:194732)的完整数学表述。对于一个内部珠子（$n=2, \dots, N-1$）：
$$
\zeta \frac{d\mathbf{R}_n(t)}{dt} = k_s (\mathbf{R}_{n+1} - 2\mathbf{R}_n + \mathbf{R}_{n-1}) + \boldsymbol{\eta}_n(t)
$$
对于两个末端珠子（$n=1$和$n=N$），由于它们各自只与一个珠子相连，其方程为：
$$
\zeta \frac{d\mathbf{R}_1(t)}{dt} = k_s (\mathbf{R}_2 - \mathbf{R}_1) + \boldsymbol{\eta}_1(t)
$$
$$
\zeta \frac{d\mathbf{R}_N(t)}{dt} = k_s (\mathbf{R}_{N-1} - \mathbf{R}_N) + \boldsymbol{\eta}_N(t)
$$
其中弹簧常数$k_s = 3k_{\mathrm{B}}T/b^2$。由于忽略了HI，不同珠子上的随机力是互不相关的：
$$
\langle \eta_{n\alpha}(t) \eta_{m\beta}(t') \rangle = 2k_{\mathrm{B}}T \zeta \delta_{nm} \delta_{\alpha\beta} \delta(t-t')
$$
其中$\alpha, \beta$是笛卡尔分量。

[Rouse模型](@entry_id:194732)的一个重要推论是，整条链的总[摩擦力](@entry_id:171772)是所有[单体](@entry_id:136559)[摩擦力](@entry_id:171772)的简单加和，即$\zeta_{\mathrm{chain}}^{\mathrm{Rouse}} = N\zeta$ [@problem_id:3010799]。这导致其质心[扩散](@entry_id:141445)系数$D_{\mathrm{CM}}$和最长[弛豫时间](@entry_id:191572)$\tau_{\mathrm{Rouse}}$的标度关系为 [@problem_id:2909878] [@problem_id:2909040]：
$$
D_{\mathrm{CM}} = \frac{k_{\mathrm{B}} T}{N\zeta} \sim N^{-1}
$$
$$
\tau_{\mathrm{Rouse}} \sim \frac{R^2}{D_{\mathrm{CM}}} \sim \frac{(b N^{1/2})^2}{N^{-1}} \sim N^2 \quad (\text{对于理想链, } \nu=1/2)
$$
尽管[Rouse模型](@entry_id:194732)忽略HI的做法对于稀溶液来说是不现实的，但它完美地描述了**无缠结浓溶液和熔体**的动力学。在这些体系中，周围密集的聚合物链段会有效地“筛选”掉长程的[流体力学](@entry_id:136788)相互作用，使得每个珠子的摩擦主要来自于局部环境，其动力学行为回归到自由排干的图像 [@problem_id:2909040]。

### [Zimm模型](@entry_id:201998)：包含[流体力学](@entry_id:136788)相互作用的动力学

在稀溶液中，聚合物链的运动会扰动周围的溶剂，产生一个流场，这个流场又会影响链上其他珠子的运动。这种通过溶剂传递的间接耦合就是**[流体力学](@entry_id:136788)相互作用**（HI）。**[Zimm模型](@entry_id:201998)**正是将这种相互作用纳入考量的动力学模型。

在低雷诺数的[斯托克斯流](@entry_id:138636)中，由一个施加在原点的点力$\mathbf{F}$所产生的[流体速度](@entry_id:267320)场$\mathbf{u}(\mathbf{r})$由**Oseen张量**$\mathbf{T}(\mathbf{r})$描述 [@problem_id:3010749]：
$$
\mathbf{u}(\mathbf{r}) = \mathbf{T}(\mathbf{r}) \cdot \mathbf{F}, \quad \text{其中} \quad \mathbf{T}(\mathbf{r}) = \frac{1}{8\pi \eta_s r} \left(\mathbf{I} + \hat{\mathbf{r}}\hat{\mathbf{r}}\right)
$$
其中$r=|\mathbf{r}|$，$\hat{\mathbf{r}}=\mathbf{r}/r$。Oseen张量$1/r$的长程衰减特性是HI长程本质的体现。

[Zimm模型](@entry_id:201998)将这种耦合引入[Langevin方程](@entry_id:144277)，通过一个依赖于构象的**迁移率张量**$\mathbf{H}_{ij}$来实现。珠子$i$的速度现在不仅与作用在它身上的力$\mathbf{F}_i$有关，还与作用在所有其他珠子$j$上的力$\mathbf{F}_j$有关：
$$
\frac{d\mathbf{R}_i}{dt} = \sum_{j=1}^N \mathbf{H}_{ij}(\{\mathbf{R}\}) \cdot \mathbf{F}_j + \boldsymbol{\xi}_i(t)
$$
其中，$\mathbf{F}_j$是[熵弹簧](@entry_id:136248)力，$\mathbf{H}_{ii} = \mu_0 \mathbf{I} = (6\pi\eta_s a)^{-1} \mathbf{I}$是珠子自身的迁移率，而$\mathbf{H}_{ij} = \mathbf{T}(\mathbf{R}_i - \mathbf{R}_j)$（对于$i \neq j$）正是Oseen张量。相应地，涨落-耗散定理也需要推广，随机力$\boldsymbol{\xi}_i(t)$的关联函数现在与迁移率张量耦合 [@problem_id:3010749]：
$$
\langle \xi_{i\alpha}(t) \xi_{j\beta}(t') \rangle = 2k_{\mathrm{B}}T (\mathbf{H}_{ij})_{\alpha\beta} \delta(t-t')
$$
由于$\mathbf{H}_{ij}$依赖于不断变化的珠子间距离，上述方程极难求解。[Zimm模型](@entry_id:201998)采用了一个关键的近似——**预平均近似**（pre-averaging approximation），即用$\mathbf{H}_{ij}$在平衡构象下的平均值$\langle \mathbf{H}_{ij} \rangle$来代替其瞬时值。

HI的引入极大地改变了链的动力学行为。由于溶剂被链“拖拽”着一起运动，整条[链表](@entry_id:635687)现得像一个不完全透水的球体，其有效[摩擦力](@entry_id:171772)不再是$N$个[单体](@entry_id:136559)[摩擦力](@entry_id:171772)的总和，而是与整个线团的尺寸$R$成正比 [@problem_id:2909878]：
$$
\zeta_{\mathrm{chain}}^{\mathrm{Zimm}} \sim \eta_s R \sim \eta_s b N^\nu
$$
其中$\nu$是[Flory指数](@entry_id:142030)（良溶剂中$\nu \approx 0.588$，$\theta$溶剂中$\nu = 1/2$）。由于$\nu  1$，Zimm[摩擦力](@entry_id:171772)远小于Rouse[摩擦力](@entry_id:171772)（$\zeta \sim N$），表明HI显著降低了链运动的耗散。这导致了与[Rouse模型](@entry_id:194732)截然不同的标度行为 [@problem_id:2909040]：
$$
D_{\mathrm{CM}} \sim \frac{1}{\zeta_{\mathrm{chain}}^{\mathrm{Zimm}}} \sim N^{-\nu}
$$
$$
\tau_{\mathrm{Zimm}} \sim \zeta_{\mathrm{chain}}^{\mathrm{Zimm}} R^2 \sim N^{\nu} (N^{\nu})^2 = N^{3\nu}
$$
对于$\theta$溶剂（$\nu = 1/2$），$\tau_{\mathrm{Zimm}} \sim N^{3/2}$；对于良溶剂（$\nu \approx 3/5$），$\tau_{\mathrm{Zimm}} \sim N^{9/5}$。这都比[Rouse模型](@entry_id:194732)的$\tau \sim N^2$要弱，说明HI的存在加速了链的整体弛豫过程。[Zimm模型](@entry_id:201998)是描述**稀溶液**中无缠结聚合物链动力学的标准模型 [@problem_id:2909040]。

### 内部动力学：正常模式与实验信号

为了分析聚合物链复杂的内部运动，我们引入**正常模式**（normal modes）的概念。这些模式是链上所有珠子运动的集体坐标，它们相互解耦，各自独立地以指数形式弛豫。模式序号$p$（$p=1, 2, \dots, N-1$）代表了运动的空间尺度，$p=1$对应整个链的运动，而大的$p$值对应链上短片段的局域运动。

每个模式$p$都有一个特征**[弛豫时间](@entry_id:191572)**$\tau_p$。该时间由与该模式相关的有效[摩擦力](@entry_id:171772)$\zeta_p$和[有效弹簧常数](@entry_id:171743)$k_p$之比决定，$\tau_p \sim \zeta_p / k_p$。弹簧常数$k_p$反映了长度为$N/p$的链段的[熵弹性](@entry_id:151071)，其标度关系为$k_p \sim (N/p)^{-2\nu}$，这与[流体力学](@entry_id:136788)无关。[摩擦力](@entry_id:171772)$\zeta_p$则深刻地反映了动力学模型的差异 [@problem_id:2912514]。
*   在**[Rouse模型](@entry_id:194732)**中，[摩擦力](@entry_id:171772)是加和的，$\zeta_p \sim N/p$，因此$\tau_p^{\mathrm{Rouse}} \sim \frac{N/p}{(N/p)^{-2\nu}} \sim N^{1+2\nu}p^{-(1+2\nu)}$。对于[理想链](@entry_id:196640)，这简化为$\tau_p \sim N^2 p^{-2}$。
*   在**[Zimm模型](@entry_id:201998)**中，由于HI，尺度为$N/p$的链段的[摩擦力](@entry_id:171772)与其尺寸成正比，$\zeta_p \sim (N/p)^\nu$。因此，弛豫时间标度变为：
    $$
    \tau_p^{\mathrm{Zimm}} \sim \frac{(N/p)^{\nu}}{(N/p)^{-2\nu}} = (N/p)^{3\nu} = N^{3\nu} p^{-3\nu}
    $$

这种内部模式的[弛豫谱](@entry_id:192983)可以在**[动态光散射](@entry_id:199448)**（Dynamic Light Scattering, DLS）等实验中被探测到。DLS测量的是散射[光强度](@entry_id:177094)的[自相关函数](@entry_id:138327)，它与聚合物的[动态结构因子](@entry_id:143433)$g_1(q,t)$直接相关。当散射[波矢](@entry_id:178620)$q$处于$1/R_g \ll q \ll 1/a$范围时（$R_g$为[回转半径](@entry_id:154974)），DLS主要探测链的内部动力学。此时，$g_1(q,t)$的衰减由所有内部模式的弛豫叠加而成 [@problem_id:2912514]。

对于[Zimm模型](@entry_id:201998)，由于其[弛豫谱](@entry_id:192983)$\tau_p \sim p^{-3\nu}$的特殊形式，理论计算表明，在中间时间尺度上，$g_1(q,t)$的内部运动部分表现为一个**拉伸指数**（stretched-exponential）衰减函数：
$$
G_{\mathrm{int}}(q,t) \approx \exp\left[ -(\Gamma t)^{\beta} \right]
$$
其特征**拉伸指数**$\beta = 2/3$。这个非单指数的衰减形式是稀溶液中聚合物内部动力学受HI支配的一个标志性特征。类似地，在流变学实验中，Zimm和[Rouse模型](@entry_id:194732)分别预测[储能模量](@entry_id:201147)$G'(\omega)$和[损耗模量](@entry_id:180221)$G''(\omega)$在高频区域有不同的[幂律](@entry_id:143404)行为：[Zimm模型](@entry_id:201998)为$G', G'' \sim \omega^{2/3}$，而[Rouse模型](@entry_id:194732)为$G', G'' \sim \omega^{1/2}$ [@problem_id:2934622]。

### 从稀到半稀：筛选的角色

当聚合物浓度$c$增加，线团开始相互重叠时，体系进入**[半稀溶液](@entry_id:185434)**（semi-dilute solution）状态。这个转变的[临界点](@entry_id:144653)是**[重叠浓度](@entry_id:186591)**$c^*$，定义为单位体积内平均只有一个线团时的浓度。根据[标度理论](@entry_id:146424)，其与链长$N$的关系为 [@problem_id:3010803]：
$$
c^* \sim \frac{N}{R^3} \sim \frac{N}{(b N^\nu)^3} \sim N^{1-3\nu}
$$
在[半稀溶液](@entry_id:185434)中（$c>c^*$），聚合物链形成一个瞬态的网络，其网眼尺寸由一个仅依赖于浓度的**关联长度**$\xi$描述。这个长度$\xi$是理解[半稀溶液](@entry_id:185434)物理的关键。

在[半稀溶液](@entry_id:185434)中，[长程相互作用](@entry_id:140725)会被周围的[聚合物网络](@entry_id:191902)所**筛选**（screened）。
1.  **排斥体积筛选**：在大于$\xi$的尺度上，一个链段与来自许多不同链的链段发生相互作用，导致其周围的[单体](@entry_id:136559)密度变得均匀。这使得链上远距离两点间的排斥体积相互作用被有效中和。因此，在大于$\xi$的尺度上，链的构象恢复为[理想链](@entry_id:196640)（高斯统计）的行为 [@problem_id:3010803]。
2.  **[流体力学](@entry_id:136788)筛选**：同样，在大于$\xi$的尺度上，一个珠子运动产生的流场会被周围的网络链段迅速耗散掉。这种效应可以通过**Brinkman方程**来描述，它在[斯托克斯方程](@entry_id:196346)中加入了一个正比于$\xi^{-2}$的阻尼项。其结果是，[流体力学](@entry_id:136788)相互作用从长程的$1/r$衰减变为指数衰减的$\exp(-r/\xi)/r$形式 [@problem_id:2914942]。

这种筛选效应导致了动力学行为在空间尺度上的 crossover：
*   在小于$\xi$的尺度上（**blob内部**），链段行为类似于稀溶液中的孤立链，HI未被筛选，动力学是**Zimm-like**的。
*   在大于$\xi$的尺度上（**blob之间**），HI被完全筛选，链的运动退化为局部摩擦和链连通性主导，动力学是**Rouse-like**的 [@problem_id:3010803] [@problem_id:2914942]。

这个物理图像直接影响了体系的宏观动力学。例如，在[流变学](@entry_id:138671)测量中，存在一个与blob[弛豫时间](@entry_id:191572)$\tau_\xi \sim \eta_s \xi^3 / k_B T$相关的[交叉](@entry_id:147634)频率$\omega_c \sim 1/\tau_\xi$。当探测频率$\omega \gg \omega_c$时，我们探测的是blob内部的Zimm动力学，因此$G', G'' \sim \omega^{2/3}$。当$\omega \ll \omega_c$时，我们探测的是由blob组成的更长链段的Rouse动力学，因此$G', G'' \sim \omega^{1/2}$。在$\theta$溶剂中，可以推导出$\xi \sim c^{-1}$，进而得到$\omega_c \sim c^3$，这为通过实验验证blob图像和筛选理论提供了可能 [@problem_id:2934622]。

### 总结：动力学模型的[适用范围](@entry_id:636189)

综上所述，[Rouse模型](@entry_id:194732)和[Zimm模型](@entry_id:201998)并非相互竞争，而是描述了聚合物在不同物理情境下的动力学行为。它们的适用性主要由两个因素决定：**[流体力学](@entry_id:136788)相互作用**是否被筛选，以及**拓扑缠结**是否重要。对于我们所关注的无缠结链，其动力学模型可以总结如下 [@problem_id:2909040]：

*   **稀溶液（Dilute, $c \ll c^*$）**: 聚合物链孤立，HI未被筛选，长程起主导作用。适用**[Zimm模型](@entry_id:201998)**。最长[弛豫时间](@entry_id:191572)$\tau \sim N^{3\nu}$，[扩散](@entry_id:141445)系数$D \sim N^{-\nu}$。

*   **[半稀溶液](@entry_id:185434)（Semi-dilute, $c > c^*$）**: 聚合物链重叠，HI在大于关联长度$\xi$的尺度上被筛选。大尺度、长时程的动力学由blob组成的链的Rouse行为主导。适用**[Rouse模型](@entry_id:194732)**（作为链-of-blobs的描述）。最长弛豫时间$\tau \sim N^2$，[扩散](@entry_id:141445)系数$D \sim N^{-1}$（此处的$D$指的是受约束链的[扩散](@entry_id:141445)，与稀溶液情况不同）。

*   **熔体（Melt）**: 体系极其稠密，HI被完全筛选到[单体](@entry_id:136559)尺度。动力学由局部摩擦主导。适用**[Rouse模型](@entry_id:194732)**。最长[弛豫时间](@entry_id:191572)$\tau \sim N^2$，[扩散](@entry_id:141445)系数$D \sim N^{-1}$。

当链长$N$远大于缠结长度$N_e$时，拓扑缠结变得不可忽略，链的运动被限制在由周围链形成的“管道”中，动力学行为转变为**[蠕动](@entry_id:181056)模型**（Reptation model）主导，其弛豫时间和[扩散](@entry_id:141445)的标度行为（如$\tau \sim N^3$）将发生根本性改变，但这超出了本章的范围。