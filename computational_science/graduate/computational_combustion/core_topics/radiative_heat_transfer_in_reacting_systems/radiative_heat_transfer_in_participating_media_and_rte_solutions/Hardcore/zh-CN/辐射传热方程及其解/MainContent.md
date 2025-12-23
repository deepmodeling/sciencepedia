## 引言
辐射换热，作为与导热、对流并列的三种基本热量传递方式之一，在高温工程系统中扮演着至关重要的角色。当热量通过气体、烟尘颗粒或多孔材料等“参与性介质”传递时，辐射不再仅仅是表面间的现象，而是变成了复杂的体积效应，涉及吸收、发射和散射等多种物理过程。准确地预测和控制这种体积辐射，对于优化燃烧效率、设计先进热防护系统以及开发高性能隔热材料等前沿科技领域至关重要。然而，描述[辐射场](@entry_id:164265)行为的数学模型——辐射传输方程（RTE）——是一个高维度的积分-[微分](@entry_id:158422)方程，其求解极具挑战性，构成了[计算传热学](@entry_id:148412)中的一个核心难题。

本文旨在为读者构建一个关于参与性介质中辐射换热的全面知识体系。我们将从第一性原理出发，系统地梳理该领域的理论基础、关键应用和前沿计算方法。
- 在 **“原理与机制”** 章节中，我们将详细推导辐射传输方程，阐明吸收、发射、散射等基本过程的物理意义，并深入探讨[局部热力学平衡](@entry_id:147993)（LTE）、非[灰体辐射](@entry_id:142501)物性模型（如普朗克平均和罗斯兰平均系数）等核心建模概念。
- 接下来，在 **“应用与跨学科连接”** 章节中，我们将展示这些理论在真实世界问题中的强大威力，重点分析辐射在燃烧[火焰结构](@entry_id:1125069)、[湍流-辐射相互作用](@entry_id:1133488)（TRI）、[高超声速飞行](@entry_id:272087)器热管理以及[多孔材料](@entry_id:152752)传热中的关键作用。
- 最后，在 **“动手实践”** 章节中，我们将引导读者通过具体的编程练习，亲手实现并评估先进的光谱模型和RTE求解器，从而将理论知识转化为解决实际问题的计算能力。

通过这三个章节的逐层深入，本文将带领读者跨越从理论到实践的鸿沟，全面掌握参与性介质中辐射换[热分析](@entry_id:150264)的核心技能。

## 原理与机制

在“引言”章节之后，我们深入探讨参与性介质中辐射换热的物理原理和数学描述。本章的目标是构建一个坚实的理论框架，从辐射能守恒的基本假设出发，推导出描述[辐射强度](@entry_id:150179)场的核心方程，定义关键的物性参数，并阐明在计算燃烧学中至关重要的建模假设和简化方法。

### 辐射传输方程（RTE）

辐射换[热分析](@entry_id:150264)的核心是理解 **光[谱辐射强度](@entry_id:148916)** $I_\lambda(\mathbf{r}, \hat{\mathbf{s}})$ 的时空演化。该物理量描述了在位置 $\mathbf{r}$，沿方向单位矢量 $\hat{\mathbf{s}}$ 传播的，单位波长、单位立体角、单位投影面积上的[辐射功率](@entry_id:267187)。在一个 **参与性介质**（participating medium）中，例如火焰中的气体和烟尘颗粒混合物，辐射在穿行过程中会与介质发生相互作用，导致其强度发生改变。

为了推导控制 $I_\lambda$ 演化的方程，我们考察一束沿 $\hat{\mathbf{s}}$ 方向传播的辐射，在穿过一个无穷小控制体积 $dV$ 时其能量的变化。该变化由四种基本物理过程共同决定：吸收、发射、出射散射和入射散射。

1.  **吸收（Absorption）**：介质从辐射束中吸收能量，使其强度减弱。这种能量损失正比于入射强度 $I_\lambda$。我们定义比例系数为 **光谱吸收系数**（spectral absorption coefficient）$k_\lambda$ (单位: $m^{-1}$)，则强度变化为 $-k_\lambda I_\lambda ds$，其中 $ds$ 是路径微元。

2.  **出射散射（Out-scattering）**：介质中的颗粒或分子将能量从 $\hat{\mathbf{s}}$ 方向散射到其他方向，同样导致该方向上的强度减弱。这种损失也正比于 $I_\lambda$。我们定义比例系数为 **光谱[散射系数](@entry_id:1131287)**（spectral scattering coefficient）$\sigma_{s,\lambda}$ (单位: $m^{-1}$)，强度变化为 $-\sigma_{s,\lambda} I_\lambda ds$。

3.  **发射（Emission）**：处于一定温度 $T$ 的介质自身会向各个方向发射热辐射，从而增强辐射场的强度。我们用 **光谱发射系数**（spectral emission coefficient）$j_\lambda$ 来描述单位体积、单位[立体角](@entry_id:154756)、单位波长内发射的能量。发射导致的强度增加为 $j_\lambda ds$。

4.  **入射散射（In-scattering）**：从所有其他方向 $\hat{\mathbf{s}}'$ 传来的辐射，被介质散射进入我们所关心的 $\hat{\mathbf{s}}$ 方向。这是一个增益项，其大小取决于来自所有方向的强度以及散射的角向分布特性。

综合以上四项，我们得到辐射能沿路径的[守恒方程](@entry_id:1122898)，即 **辐射传输方程**（Radiative Transfer Equation, RTE）：
$$
\frac{dI_\lambda}{ds} = \hat{\mathbf{s}} \cdot \nabla I_\lambda = -k_\lambda I_\lambda - \sigma_{s,\lambda} I_\lambda + j_\lambda + S_{\lambda, \text{is}}
$$
其中 $S_{\lambda, \text{is}}$ 代表入射散射源项。通常，我们将吸收和出射散射的衰减效应合并，定义 **光谱消光系数**（spectral extinction coefficient）$\beta_\lambda = k_\lambda + \sigma_{s,\lambda}$。于是，RTE可写为：
$$
\frac{dI_\lambda}{ds} = -\beta_\lambda I_\lambda + j_\lambda + S_{\lambda, \text{is}}
$$
这个方程是辐射换[热分析](@entry_id:150264)的基石。对于不与辐射发生体积相互作用的 **非参与性介质**（non-participating medium），其吸收和[散射系数](@entry_id:1131287)均为零 ($k_\lambda = 0, \sigma_{s,\lambda} = 0$)，RTE简化为 $dI_\lambda/ds=0$，意味着强度沿直线路径保持不变。在这种情况下，辐射换热完全由封闭体表面之间的几何关系和表面性质决定，通常使用 **[角系数](@entry_id:149598)**（view factor）方法进行分析 。

### 介质的辐射物性

RTE中的系数 $k_\lambda$、$\sigma_{s,\lambda}$ 和 $j_\lambda$ 是描述介质与辐射相互作用强弱的物性参数。准确获取这些参数是求解RTE的前提。

#### 吸收、散射与[消光系数](@entry_id:270201)

从RTE的[量纲一致性](@entry_id:271193)可知，$k_\lambda$, $\sigma_{s,\lambda}$ 和 $\beta_\lambda$ 的单位均为逆长度（$m^{-1}$），它们分别代表辐射光子在单位路径长度上被吸收、被散射或被消光（吸收或散射）的概率 。

在典型的燃烧环境中，这些系数的物理来源和特性有显著差异：

-   **燃烧气体**（如 $\text{H}_2\text{O}, \text{CO}_2$）：气体的吸收和发射主要源于分子振转能级的跃迁。其[吸收光谱](@entry_id:144611)呈现为由数千条分立谱线构成的复杂带状结构，因此 $k_\lambda$ 对波长 $\lambda$ 极为敏感。此外，能级上的布居数和[谱线宽度](@entry_id:168313)（受多普勒和碰撞展宽影响）都强烈依赖于温度，导致[气体辐射](@entry_id:150797)物性具有很强的 **温度依赖性** 。在没有颗粒物的情况下，气体分子的散射（瑞利散射）通常可以忽略不计。

-   **烟尘（Soot）**：烟尘是由纳米级的碳质颗粒组成的。其辐射物性在整个红外波段通常是连续变化的，不像气体那样呈线状光谱。烟尘的吸收和[散射系数](@entry_id:1131287)主要取决于其颗粒的尺寸分布、形状（形态）、数密度以及[复折射率](@entry_id:268061)。虽然烟尘的生成和氧化过程与温度密切相关，但对于一个给定的烟尘场，其辐射物性对气体温度的 **显式依赖性较弱** 。

#### 单次散射反照率

为了量化散射相对于总消光的重要性，我们定义一个无量纲参数——**单次散射反照率**（single scattering albedo）$\omega_\lambda$：
$$
\omega_\lambda = \frac{\sigma_{s,\lambda}}{\beta_\lambda} = \frac{\sigma_{s,\lambda}}{k_\lambda + \sigma_{s,\lambda}}
$$
由于 $k_\lambda$ 和 $\sigma_{s,\lambda}$ 均为非负值，$\omega_\lambda$ 的取值范围为 $0 \le \omega_\lambda \le 1$。它代表了一次消光事件（光子与介质发生相互作用）中，该事件是散射而非吸收的概率 。

-   当 $\omega_\lambda = 0$ 时，介质为纯吸收-发射介质，没有散射。
-   当 $\omega_\lambda = 1$ 时，介质为纯散射介质（也称 **保守散射**，conservative scattering），辐射能量在介质中只改变传播方向而不被转化为内能。
-   在燃烧应用中，烟尘的散射作用不可忽略，因此 $\omega_\lambda$ 是一个描述其辐射特性的重要参数。

### RTE源项的建模

RTE是一个包含未知源项（发射和入射散射）的积分-[微分](@entry_id:158422)方程。为了求解它，必须为这些源项提供封闭模型。

#### 发射项与局部热力学平衡（LTE）

发射项 $j_\lambda$ 的建模是核心挑战之一。一个在计算燃烧学中被广泛采用的关键假设是 **[局部热力学平衡](@entry_id:147993)**（Local Thermodynamic Equilibrium, LTE）。

LTE假设指的是，在介质的局部微元内，分子的平动、转动、振动等能级的布居数主要由粒子间的 **碰撞过程** 主导，并遵循对应于局部[气体动理学](@entry_id:140543)温度 $T$ 的[玻尔兹曼分布](@entry_id:142765)。这种情况通常发生在压力和温度足够高的环境中（如大多数燃烧系统），此时碰撞频率远高于[自发辐射](@entry_id:140032)等辐射过程的频率 。

在LTE条件下，根据[微观可逆性原理](@entry_id:137392)，可以推导出宏观发射系数 $j_\lambda$ 和[吸收系数](@entry_id:156541) $k_\lambda$ 之间的关系，这本质上是[基尔霍夫定律](@entry_id:180785)（Kirchhoff's Law）在体积辐射上的体现 。该关系为：
$$
j_\lambda = k_\lambda B_\lambda(T)
$$
其中 $B_\lambda(T)$ 是著名的 **普朗克黑体辐射函数**，它仅是波长和局部温度的函数。

这一关系至关重要，因为它用一个已知的普适函数 $B_\lambda(T)$ 和介质的[吸收系数](@entry_id:156541) $k_\lambda$ 来封闭发射项。需要强调的是：
-   该关系成立的条件是 **介质本身** 处于LTE，而与穿过它的 **[辐射场](@entry_id:164265)的状态无关**。即使局部辐射强度 $I_\lambda$ 远不等于 $B_\lambda(T)$，只要气体[分子能级](@entry_id:158418)布居由碰撞决定，该关系依然有效 。
-   该关系的有效性与介质的 **[光学厚度](@entry_id:150612)无关**。无论介质是光学薄还是光学厚，只要满足LTE条件，就可以使用此公式 。

然而，在某些燃烧场景中，LTE假设会失效。例如，在 **[化学发光](@entry_id:153756)**（chemiluminescence）过程中，化学反应直接生成处于特定激发态的[自由基](@entry_id:188302)，其[能级布居](@entry_id:197877)由[化学动力学](@entry_id:144961)而非热碰撞决定。此外，在极低压力下，分子的[辐射衰变](@entry_id:159878)速率可能超过[碰撞弛豫](@entry_id:160961)速率，导致高能级粒子数低于玻尔兹曼分布的预测值。在这些[非LTE](@entry_id:152428)情况下，使用 $k_\lambda B_\lambda(T)$ 会高估或低估真实的辐射发射，必须通过求解粒子数布居的速率方程来计算 $j_\lambda$ [@problem_id:4056027, @problem_id:4056049]。

#### 入射散射项与相函数

入射散射源项 $S_{\lambda, \text{is}}$ 描述了来自所有方向 $\hat{\mathbf{s}}'$ 的辐射被散射到方向 $\hat{\mathbf{s}}$ 的贡献。其通用表达式为：
$$
S_{\lambda, \text{is}}(\hat{\mathbf{s}}) = \sigma_{s,\lambda} \int_{4\pi} I_\lambda(\hat{\mathbf{s}}') \Phi_\lambda(\hat{\mathbf{s}}', \hat{\mathbf{s}}) d\Omega'
$$
这里的 $\Phi_\lambda(\hat{\mathbf{s}}', \hat{\mathbf{s}})$ 被称为 **[散射相函数](@entry_id:1131288)**（scattering phase function），它描述了辐射从 $\hat{\mathbf{s}}'$ 方向散射到 $\hat{\mathbf{s}}$ 方向的[概率密度](@entry_id:175496)分布，通常归一化为 $\frac{1}{4\pi}\int_{4\pi} \Phi_\lambda d\Omega = 1$。

-   **各向同性散射（Isotropic Scattering）**：这是最简单的散射模型，假设辐射被均匀地散射到所有方向，与入射方向无关。此时，[相函数](@entry_id:1129581)为常数 $\Phi_\lambda = 1$。在这种情况下，入射散射源项可以被极大简化 ：
    $$
    S_{\lambda, \text{is}} = \sigma_{s,\lambda} \frac{1}{4\pi} \int_{4\pi} I_\lambda(\hat{\mathbf{s}}') d\Omega' = \sigma_{s,\lambda} J_\lambda
    $$
    其中 $J_\lambda = \frac{1}{4\pi} \int_{4\pi} I_\lambda d\Omega'$ 定义为 **平均光[谱辐射强度](@entry_id:148916)**。可见，对于各向同性散射，入射散射源项只与局部的平均强度有关。

-   **[各向异性散射](@entry_id:148372)（Anisotropic Scattering）**：对于烟尘等实际颗粒物，散射通常具有方[向性](@entry_id:144651)，即前向散射（与原方向夹角小）的概率远大于后向散射。此时必须使用非均匀的相函数模型。一个广泛应用的简单模型是 **[Henyey-Greenstein](@entry_id:750228) (HG) [相函数](@entry_id:1129581)** ：
    $$
    \Phi_{\text{HG}}(\mu; g) = \frac{1-g^2}{(1+g^2-2g\mu)^{3/2}}
    $$
    其中 $\mu = \hat{\mathbf{s}} \cdot \hat{\mathbf{s}}'$ 是散射前后[方向余弦](@entry_id:170591)。该函数由一个参数——**不[对称因子](@entry_id:274828)**（asymmetry parameter）$g$ 控制。$g$ 的定义为散射角余弦的平均值，$g = \langle \cos\theta \rangle$，其取值范围为 $[-1, 1]$。
    -   $g > 0$ 表示 **[前向散射](@entry_id:191808)** 占主导。
    -   $g  0$ 表示 **后向散射** 占主导。
    -   $g = 0$ 对应 **各向同性散射**。
    烟尘颗粒的散射通常是强前向的，其 $g$ 值一般为正且接近1。

### 辐射传输的特征：[无量纲参数](@entry_id:169335)与渐近区域

为了更好地理解和简化辐射传输问题，我们引入一些关键的[无量纲参数](@entry_id:169335)和极限情况。

#### 光学厚度与特征区域

辐射在介质中的衰减程度，不仅取决于[消光系数](@entry_id:270201) $\beta_\lambda$，还取决于其穿过的物理距离 $L$。我们将这两者结合，定义一个无量纲的路径长度——**光学坐标**（optical coordinate）$\tau_\lambda(s) = \int_0^s \beta_\lambda(s') ds'$。整个介质的 **[光学厚度](@entry_id:150612)**（optical thickness）为 $\tau_{\lambda,L} = \int_0^L \beta_\lambda(s) ds$ 。

光学厚度的物理意义是辐射光子在穿过介质时所经历的平均自由程的个数。当RTE用光学坐标 $\tau_\lambda$ 作为[自变量](@entry_id:267118)时，其衰减项的系数变为1，表明 $\tau_\lambda$ 是描述辐射衰减的自然尺度。

根据光学厚度的大小，我们可以将辐射传输问题划分为三个典型区域：
1.  **光学薄区域（Optically Thin, $\tau_\lambda \ll 1$）**：介质对辐射几乎是透明的。内部发射的辐射可以几乎无衰减地逃逸出去，吸收和散射作用微弱。
2.  **光学厚区域（Optically Thick, $\tau_\lambda \gg 1$）**：介质对辐射高度不透明。辐射在介质内部经历多次吸收、发射和散射，与物质达到高度耦合，其传输行为类似于[扩散过程](@entry_id:268015)。
3.  **光学中间区域（Optically Intermediate, $\tau_\lambda \sim 1$）**：这是最复杂的情况，吸收、发射和散射同等重要，[辐射场](@entry_id:164265)既不透明也不完全扩散，表现出强烈的方向性。

例如，在一个厚度为 $L=0.5$ m，吸收系数为 $\kappa_\lambda(s) = 2.0(1 + 0.6s/L)$ $\text{m}^{-1}$，散射系数为 $\sigma_\lambda(s) = 1.0\exp(-s/L)$ $\text{m}^{-1}$ 的燃烧气体层中，其总光学厚度可计算为 $\tau_\lambda \approx 1.62$ 。这个值属于典型的光学中间区域，意味着任何基于光学薄或光学厚假设的简化模型（如[扩散近似](@entry_id:147930)）都将产生较大误差，必须采用能精确求解完整RTE的角度离散方法（如[离散纵标法](@entry_id:1123828) $S_N$ 或蒙特卡洛法）才能获得准确结果。

#### 渐近区域的灰体模型

为了避免求解复杂的谱线依赖的RTE，工程上常在光学薄或光学厚的极限情况下使用 **灰体模型**（gray-gas model），即用一个在光谱上平均的[吸收系数](@entry_id:156541)来代替 $k_\lambda$。然而，正确的平均方式在不同极限下是不同的。

-   **[光学薄极限](@entry_id:1129155)与普朗克平均吸收系数**：在[光学薄极限](@entry_id:1129155)下，介质的净辐射损失主要由体积发射决定。总的体积发射功率为 $\int_0^\infty 4\pi k_\lambda B_\lambda(T) d\lambda$。为了用一个灰体系数 $\bar{k}$ 来等效表示这个积分，即 $4\pi \bar{k} \int_0^\infty B_\lambda(T) d\lambda$，我们必须定义：
    $$
    \bar{k}_P = \frac{\int_0^\infty k_\lambda B_\lambda(T) d\lambda}{\int_0^\infty B_\lambda(T) d\lambda}
    $$
    这个系数被称为 **普朗克平均吸收系数**（Planck mean absorption coefficient）。其物理意义是：它是一个以黑体发射谱 $B_\lambda(T)$ 为权重函数的 $k_\lambda$ 的加权平均，因为在发射主导的区域，光谱中[黑体辐射](@entry_id:137223)强的部分对总发射的贡献更大 。

-   **光学厚极限与[罗斯兰平均吸收系数](@entry_id:754423)**：在光学厚极限下，辐射传输类似于[热传导](@entry_id:143509)，辐射热流可以近似表示为傅里叶定律的形式 $\mathbf{q}_r \approx -K_r \nabla T$，其中 $K_r$ 是辐射热导率。通过对RTE进行[渐近分析](@entry_id:1121160)可以证明，辐射[热导](@entry_id:189019)率与一个平均[吸收系数](@entry_id:156541)的倒数成正比。这个平均系数被称为 **[罗斯兰平均吸收系数](@entry_id:754423)**（Rosseland mean absorption coefficient），其倒数定义为：
    $$
    \frac{1}{\bar{k}_R} = \frac{\int_0^\infty \frac{1}{k_\lambda} \frac{\partial B_\lambda(T)}{\partial T} d\lambda}{\int_0^\infty \frac{\partial B_\lambda(T)}{\partial T} d\lambda}
    $$
    这种平均方式的物理意义是：在[扩散过程](@entry_id:268015)中，能量主要通过介质最“透明”的光谱“窗口”（即 $k_\lambda$ 值最小的波段）进行传输。因此，平均过程是通过对“[光子平均自由程](@entry_id:753417)” $1/k_\lambda$ 进行加权平均来实现的。权重函数 $\partial B_\lambda / \partial T$ 的出现，是因为热流是由温度梯度驱动的，该函数表征了[黑体谱](@entry_id:158574)的哪个部分对温度变化最敏感，因而对热量输运最有效 。

### 辐射与流动的耦合：辐射源项

最后，也是在[计算流体力学](@entry_id:747620)（CFD）中至关重要的一步，是将辐射场与流体的能量方程耦合起来。在包含化学反应、导热和辐射的流体中，温度场的能量守恒方程（忽略粘性耗散等次要项）可写为：
$$
\rho c_p \frac{DT}{Dt} = \nabla \cdot (k \nabla T) - \nabla \cdot \mathbf{q}_r + S_{\text{chem}}
$$
其中，$\rho$ 是密度，$c_p$ 是定[压比](@entry_id:137698)热，$k$ 是[热导](@entry_id:189019)率，$S_{\text{chem}}$ 是化学[反应热](@entry_id:140993)释放率。$-\nabla \cdot \mathbf{q}_r$ 即为 **辐射源项**，代表[辐射场](@entry_id:164265)向单位体积介质传递的净能量。

为了得到辐射源项的表达式，我们将RTE在所有 $4\pi$ [立体角](@entry_id:154756)上进行积分 。RTE的左侧 $\int_{4\pi} (\hat{\mathbf{s}} \cdot \nabla I_\lambda) d\Omega$ 变为光谱辐射热流的散度 $\nabla \cdot \mathbf{q}_{r,\lambda}$。RTE的右侧各项积分后，一个关键的结果是，对于 **[弹性散射](@entry_id:152152)**（即散射过程中[光子能量](@entry_id:139314)不变），出射散射项和入射散射项的积分恰好相互抵消。这反映了一个深刻的物理事实：散射只改变辐射能的分布，而不能在辐射场和介质内能之间产生净的能量交换。

因此，角度积分后的RTE简化为仅包含吸收和发射项的平衡：
$$
\nabla \cdot \mathbf{q}_{r,\lambda} = 4\pi k_\lambda B_\lambda(T) - 4\pi k_\lambda J_\lambda = 4\pi k_\lambda (B_\lambda(T) - J_\lambda)
$$
这个量代表在波长 $\lambda$ 处，介质因辐射而产生的净功率损失（发射减去吸收）。为了得到总的辐射源项，我们再对所有波长进行积分：
$$
\nabla \cdot \mathbf{q}_r = \int_0^\infty \nabla \cdot \mathbf{q}_{r,\lambda} d\lambda = \int_0^\infty 4\pi k_\lambda (B_\lambda(T) - J_\lambda) d\lambda
$$
于是，代入能量方程的辐射源项（能量增益）为：
$$
-\nabla \cdot \mathbf{q}_r = \int_0^\infty 4\pi k_\lambda (J_\lambda - B_\lambda(T)) d\lambda
$$
这个简洁而深刻的公式构成了辐射与流体[能量耦合](@entry_id:137595)的核心。它表明，介质从[辐射场](@entry_id:164265)中获得的净能量，等于它所吸收的总辐射能（与平均强度 $J_\lambda$ 成正比）减去它自身发射的总辐射能（与黑体函数 $B_\lambda(T)$ 成正比）。在[数值模拟](@entry_id:146043)中，[CFD求解器](@entry_id:747244)负责求解温度场 $T$，而RTE求解器则提供[辐射强度](@entry_id:150179)场（用以计算 $J_\lambda$）。两者通过辐射源项迭代耦合，直至达到收敛解。