## 引言
原始非高斯性（Primordial Non-Gaussianity, PNG）是探索极[早期宇宙物理学](@entry_id:161859)（如宇宙暴胀时期）的关键探针。虽然[标准宇宙学模型](@entry_id:159833)（ΛCDM）假设初始[密度扰动](@entry_id:159546)是近乎完美的[高斯随机场](@entry_id:749757)，但许多理论模型预测了微小的非高斯性偏离。在模拟中精确地实现这些非高斯性，对于利用未来的宇宙[大尺度结构](@entry_id:158990)巡天数据检验这些基本理论至关重要。然而，将抽象的理论模型转化为[N体模拟](@entry_id:157492)中数以十亿计粒子的精确初始位置与速度，是一项充满挑战的任务。这不仅需要深刻理解微扰场的统计物理，还要求掌握复杂的数值技术，并能辨别物理信号与数值人为效应。

本文旨在系统性地解决这一问题，为研究者提供一套完整的理论、方法与实践指南。在“**原理与机制**”一章中，我们将奠定理论基础，详细解释非高斯场的统计描述、主流的PNG模型及其生成机制。接下来的“**应用与跨学科联系**”一章将展示这些原理如何应用于分析宇宙结构形成、应对数值挑战，并探讨PNG与其他宇宙学前沿课题的[交叉](@entry_id:147634)与简并性。最后，在“**动手实践**”部分，我们通过具体的计算问题，帮助读者巩固核心概念，检验代码实现的正确性。通过这三个层层递进的章节，读者将能够全面掌握生成含PNG初始条件的核心技术，并将其应用于前沿的宇宙学研究中。

## 原理与机制

在[宇宙学模拟](@entry_id:747928)中生成具有初始非高斯性的[初始条件](@entry_id:152863)，需要对随机场理论、宇宙[微扰理论](@entry_id:138766)以及数值方法有深刻的理解。本章旨在系统地阐述这些核心原理与关键机制，从场的统计描述开始，过渡到非高斯性的具体模型，最后探讨如何将这些理论概念转化为[N体模拟](@entry_id:157492)中精确的粒子初始[分布](@entry_id:182848)，并讨论验证这些模拟结果时所面临的挑战。

### 原始场的统计基础

为了描述宇宙早期的微扰，我们通常将其建模为一个[随机场](@entry_id:177952)，例如原始曲率微扰场 $\zeta(\boldsymbol{x})$。该场的统计特性完全由其[N点相关函数](@entry_id:186634)（或等效地，其累积量）的层级结构决定。一个场的性质是高斯性的还是非高斯性的，取决于这些相关函数的结构。

#### 高斯场与非高斯场的定义

在[统计场论](@entry_id:155447)中，一个随机场 $\zeta(\boldsymbol{x})$ 被定义为**高斯场**，当且仅当其所有高阶（$N > 2$）**连通相关函数**（或称[累积量](@entry_id:152982)）为零。连通[相关函数](@entry_id:146839) $\langle \zeta(\boldsymbol{x}_1) \dots \zeta(\boldsymbol{x}_N) \rangle_c$ 是描述场内在关联的基本量。因此，对于一个高斯场，其全部统计信息都蕴含在平均值（一阶连通[相关函数](@entry_id:146839)）和两点连通[相关函数](@entry_id:146839)中。在宇宙学中，我们通常假设原始微扰的平均值为零，此时高斯场就完全由其[两点相关函数](@entry_id:185074)，或其[傅里叶对偶](@entry_id:200473)——**功率谱**（Power Spectrum）所刻画。

相反，如果至少存在一个 $N>2$ 的连通[相关函数](@entry_id:146839)不为零，那么该场就是**非高斯场**。最简单且最重要的非高斯性指标是三点连通相关函数，其[傅里叶变换](@entry_id:142120)被称为**[能谱](@entry_id:181780)**（Bispectrum）。需要强调的是，仅仅[能谱](@entry_id:181780)为零并不足以保证场是高斯性的。一个场的能谱可能因为某种对称性（例如在 $\zeta \to -\zeta$ 变换下对称）而消失，但其四点连通[相关函数](@entry_id:146839)（其[傅里叶变换](@entry_id:142120)为**三能谱**，Trispectrum）或其他更高阶的[累积量](@entry_id:152982)可能非零，这样的场仍然是非高斯的 [@problem_id:3474088]。

#### [威克定理](@entry_id:137086)

高斯场的统计简明性通过**[威克定理](@entry_id:137086)**（Wick's Theorem）得到了最优雅的体现。该定理指出，对于一个零均值高斯场，任意[N点相关函数](@entry_id:186634) $\langle \zeta(\boldsymbol{x}_1) \dots \zeta(\boldsymbol{x}_N) \rangle$ 都可以被分解为所有可能的[两点相关函数](@entry_id:185074)对的乘积之和。例如，四点[相关函数](@entry_id:146839)可以表示为：
$$
\langle \zeta_1 \zeta_2 \zeta_3 \zeta_4 \rangle = \langle \zeta_1 \zeta_2 \rangle \langle \zeta_3 \zeta_4 \rangle + \langle \zeta_1 \zeta_3 \rangle \langle \zeta_2 \zeta_4 \rangle + \langle \zeta_1 \zeta_4 \rangle \langle \zeta_2 \zeta_3 \rangle
$$
[威克定理](@entry_id:137086)的成立与所有 $N>2$ 的连通[相关函数](@entry_id:146839)为零是数学上等价的陈述。这正是为什么功率谱足以完全定义一个高斯场的原因：一旦两点函数已知，所有更高阶的（非连通）相关函数都可以通过它计算出来，不需要任何额外的信息。这使得高斯初始条件的生成在计算上变得直接明了 [@problem_id:3474088]。

#### 对称性的作用：[均匀性与各向同性](@entry_id:158336)

[宇宙学原理](@entry_id:158425)假设宇宙在统计上是**均匀**（homogeneous）和**各向同性**（isotropic）的。这些[基本对称性](@entry_id:161256)深刻地约束了相关函数的形式，无论场是否为高斯场 [@problem_id:3474104]。

**[统计均匀性](@entry_id:136481)**意味着物理规律在空间中任意平移下不变。这一对称性导致真实空间中的[N点相关函数](@entry_id:186634)只依赖于点之间的相对位置向量，而非绝对位置。在傅里叶空间中，这一特性表现为**动量守恒**：[N点相关函数](@entry_id:186634)必须包含一个狄拉克 $\delta$ 函数，强制要求所有涉及的[波矢](@entry_id:178620)量的和为零。例如，对于功率谱和[能谱](@entry_id:181780)，我们有：
$$
\langle \zeta(\boldsymbol{k}) \zeta(\boldsymbol{k}') \rangle \propto \delta_D(\boldsymbol{k} + \boldsymbol{k}')
$$
$$
\langle \zeta(\boldsymbol{k}_1) \zeta(\boldsymbol{k}_2) \zeta(\boldsymbol{k}_3) \rangle \propto \delta_D(\boldsymbol{k}_1 + \boldsymbol{k}_2 + \boldsymbol{k}_3)
$$
这个 $\delta$ 函数确保了只有形成闭合多边形（例如，能谱对应一个闭合三角形）的波矢量组才有关联 [@problem_id:3474124]。

**统计各向同性**意味着物理规律在空间中任意旋转下不变。对于一个[标量场](@entry_id:151443)，这要求其相关函数不能依赖于波矢量的方向，只能依赖于由它们构成的标量。因此，功率谱 $P(\boldsymbol{k})$ 只能是其模长 $k = |\boldsymbol{k}|$ 的函数，即 $P(k)$。类似地，由于 $\boldsymbol{k}_1 + \boldsymbol{k}_2 + \boldsymbol{k}_3 = \boldsymbol{0}$ 的约束，能谱 $B(\boldsymbol{k}_1, \boldsymbol{k}_2, \boldsymbol{k}_3)$ 的形状完全由构成三角形的三条边长 $k_1, k_2, k_3$ 决定，而与该三角形在空间中的绝对朝向无关。因此，我们有 $B(k_1, k_2, k_3)$ [@problem_id:3474104, @problem_id:3474124]。

综上，任意一个满足[宇宙学原理](@entry_id:158425)的微扰场的二阶和三阶统计量可以由以下形式的[多谱](@entry_id:200847)（polyspectra）定义：
$$
\langle \zeta(\boldsymbol{k}_1) \zeta(\boldsymbol{k}_2) \rangle = (2\pi)^3 \delta_D(\boldsymbol{k}_1 + \boldsymbol{k}_2) P_{\zeta}(k_1)
$$
$$
\langle \zeta(\boldsymbol{k}_1) \zeta(\boldsymbol{k}_2) \zeta(\boldsymbol{k}_3) \rangle = (2\pi)^3 \delta_D(\boldsymbol{k}_1 + \boldsymbol{k}_2 + \boldsymbol{k}_3) B_{\zeta}(k_1, k_2, k_3)
$$
这些形式是普适的，由对称性决定，与场是否为高斯场无关。对于高斯场，我们只是额外要求 $B_{\zeta} \equiv 0$ 以及所有更高阶的连通[多谱](@entry_id:200847)也为零。

### 非高斯性的模型与生成

虽然高斯场是理论分析的基石，但许多[暴胀模型](@entry_id:161366)预测了微小的原始非高斯性。在数值模拟中研究这些模型需要具体的非高斯场生成方法。

#### 局域型非高斯性模型

最常用和研究最广泛的非高斯模型是**局域型**（local-type）模型。它假设非高斯势场 $\Phi(\boldsymbol{x})$ 与一个潜在的高斯场 $\phi_G(\boldsymbol{x})$ 在**真实空间**中通过一个简单的局域非线性关系相联系：
$$
\Phi(\boldsymbol{x}) = \phi_G(\boldsymbol{x}) + f_{\mathrm{NL}} \left[ \phi_G^2(\boldsymbol{x}) - \langle \phi_G^2(\boldsymbol{x}) \rangle \right]
$$
其中 $f_{\mathrm{NL}}$ 是一个[无量纲参数](@entry_id:169335)，用于描述非高斯性的强度。减去[期望值](@entry_id:153208) $\langle \phi_G^2 \rangle$ 是为了确保 $\langle \Phi \rangle = \langle \phi_G \rangle = 0$。

这个二次项 $\phi_G^2$ 是产生非高斯性的根源。我们可以通过计算三点相关函数来看到这一点。使用[威克定理](@entry_id:137086)展开 $\langle \Phi_1 \Phi_2 \Phi_3 \rangle$，在 $f_{\mathrm{NL}}$ 的[一阶近似](@entry_id:147559)下，我们发现非零的贡献来自于形如 $\langle f_{\mathrm{NL}}\phi_{G1}^2 \phi_{G2} \phi_{G3} \rangle$ 的项。这会产生一个非零的[能谱](@entry_id:181780)。对于局域模型，在[树图](@entry_id:276372)水平（tree level）上，其能谱具有非常特定的形式 [@problem_id:3473795]：
$$
B_{\Phi}(k_1, k_2, k_3) = 2 f_{\mathrm{NL}} \left[ P_{\phi}(k_1)P_{\phi}(k_2) + P_{\phi}(k_2)P_{\phi}(k_3) + P_{\phi}(k_3)P_{\phi}(k_1) \right]
$$
其中 $P_{\phi}(k)$ 是高斯场 $\phi_G$ 的[功率谱](@entry_id:159996)。值得注意的是，这个模型中所有 $N>2$ 的连通[相关函数](@entry_id:146839)都非零，其幅度大致与 $f_{\mathrm{NL}}^{N-2}$ 成正比 [@problem_id:3474088]。

#### 局域型非高斯场的生成算法

局域型模型的真实空间定义使其在数值上易于实现。在周期性立方体（体积 $V=L^3$，网格数 $N^3$）中生成一个局域型非高斯场的典型算法如下 [@problem_id:3473795]：

1.  **生成高斯傅里叶模式**：在傅里叶空间的离散网格上，为每个独立的[波矢](@entry_id:178620)量 $\boldsymbol{k}$ 生成一个复数高斯[随机变量](@entry_id:195330) $\phi_G(\boldsymbol{k})$。根据高斯场的统计特性，$\phi_G(\boldsymbol{k})$ 的实部和虚部分别是独立的、均值为零的高斯随机数，其[方差](@entry_id:200758)由功率谱 $P_{\phi}(k)$ 决定：$\langle |\phi_G(\boldsymbol{k})|^2 \rangle = V P_{\phi}(k)$。必须强制满足实数场条件 $\phi_G(-\boldsymbol{k}) = \phi_G(\boldsymbol{k})^*$。

2.  **[逆傅里叶变换](@entry_id:178300)**：对整个傅里叶空间网格上的 $\phi_G(\boldsymbol{k})$ 场执行一次[快速傅里叶逆变换](@entry_id:749305)（iFFT），得到真[实空间](@entry_id:754128)中的高斯场 $\phi_G(\boldsymbol{x})$。

3.  **计算[方差](@entry_id:200758)**：根据给定的功率谱 $P_{\phi}(k)$，通过在傅里叶网格上求和来计算场的理论[方差](@entry_id:200758) $\sigma^2 = \langle \phi_G^2 \rangle = \frac{1}{V} \sum_{\boldsymbol{k}} P_{\phi}(k)$。

4.  **应用[非线性变换](@entry_id:636115)**：在真实空间的每个网格点 $\boldsymbol{x}$ 上，逐点应用局域模型的二次变换，从而得到最终的非高斯场 $\Phi(\boldsymbol{x})$：
    $$
    \Phi(\boldsymbol{x}) = \phi_G(\boldsymbol{x}) + f_{\mathrm{NL}} \left[ \phi_G^2(\boldsymbol{x}) - \sigma^2 \right]
    $$

这个过程高效且精确，因为它将复杂的非高斯统计生成问题简化为一次标准的高斯场生成和一次简单的逐点[实空间](@entry_id:754128)运算。

### 非高斯性的物理特征与多样性

局域模型只是[暴胀](@entry_id:161204)理论预测的多种非高斯性中的一种。不同的物理机制会产生具有不同“形状”的能谱，这些形状在特定的[波矢](@entry_id:178620)构型下有不同的表现。

#### 等边型与正交型非高斯性

除了局域型，另外两种重要的能谱形状是**等边型**（equilateral）和**正交型**（orthogonal）。这些形状通常源于单场[暴胀模型](@entry_id:161366)中包含[高阶导数](@entry_id:140882)项的有效场论。

-   **局域型** [能谱](@entry_id:181780)在**挤压极限**（squeezed limit）下达到峰值，即当一个波长远大于另外两个波长时（$k_L \ll k_S$）。这对应于长波模式与短波模式之间的强耦合。
-   **等边型** 能谱在等边三角形构型（$k_1 \approx k_2 \approx k_3$）下达到峰值。它在挤压极限下被压制，通常其幅度与 $(k_L/k_S)^2$ 成正比。这表明非高斯性主要源于相同尺度模式之间的相互作用。
-   **正交型** 能谱被构造为在数学上与局域型和等边型都正交。它同样在挤压极限下被压制，表现出与等边型类似的弱长短[波耦合](@entry_id:198588) [@problem_id:3474131]。

这些不同的形状可以通过可分离的模板（separable templates）来精确描述。例如，对于近似标度不变的[功率谱](@entry_id:159996)（$P_{\phi}(k) \propto k^{-3}$），这些能谱模板可以表示为三个基本对称单项式 $S_1, S_2, S_3$ 的[线性组合](@entry_id:154743)。等边型和正交型模板的一个关键特征是，它们在挤压极限下的[主导项](@entry_id:167418)会因为单场暴胀的[一致性关系](@entry_id:157858)而抵消，导致信号被压制 [@problem_id:3474098]。这些模板可以通过在傅里叶空间中作用于高斯场的非局域二次算符来生成，这与局域模型的实空间局域算符形成对比。

### 从原始场到[N体模拟](@entry_id:157492)[初始条件](@entry_id:152863)

生成非高斯初始条件的最终目标是为[N体模拟](@entry_id:157492)设定粒子的初始位置和速度。这个过程涉及几个关键的理论转换步骤。

#### $f_{\mathrm{NL}}$ 的约定与转换

在比较观测数据和理论预测时，必须注意不同研究领域（如宇宙微波背景CMB和宇宙大尺度结构LSS）对 $f_{\mathrm{NL}}$ 的定义可能不同。CMB界通常在原始曲率微扰 $\mathcal{R}$ 的层面定义非高斯性，而LSS界则习惯于在晚期（例如 $z=0$）的[引力势](@entry_id:160378) $\Phi$ 层面定义。

在[物质主导时期](@entry_id:272362)，这两个量在[超视界尺度](@entry_id:158063)上通过线性关系 $\Phi = \frac{3}{5}\mathcal{R}$ 相关联。考虑到从[物质主导时期](@entry_id:272362)到今天，[引力势](@entry_id:160378)的线性增长会受到暗能量的抑制（由增长抑制因子 $g(z)$ 描述，其中在 $z=0$ 时 $g(0)1$），我们可以推导出两个约定之间的转换关系。从CMB定义的 $\mathcal{R}$ 出发，最终可以得到以今天引力势 $\Phi(\boldsymbol{x}, z=0)$ 表示的非高斯关系，其[非线性](@entry_id:637147)参数为 $f_{\mathrm{NL}}^{\mathrm{LSS}}$。比较系数可得 [@problem_id:3474141]：
$$
f_{\mathrm{NL}}^{\mathrm{LSS}} = \frac{1}{g(0)} f_{\mathrm{NL}}^{\mathrm{CMB}}
$$
例如，若 $g(0) \approx 0.76$，则 $f_{\mathrm{NL}}^{\mathrm{LSS}} \approx 1.316 f_{\mathrm{NL}}^{\mathrm{CMB}}$。这个[转换因子](@entry_id:142644)对于在模拟中使用正确的非高斯性幅度至关重要。

#### 规范问题：选择正确的密度场

从爱因斯坦-玻尔兹曼求解器（如CAMB或CLASS）获得的线性微扰量（如密度和速度）是在特定规范（gauge）下计算的，通常是**[牛顿规范](@entry_id:160348)**（Newtonian gauge）。然而，[N体模拟](@entry_id:157492)中的粒子代表的是物质流体，它们的运动定义了一个**同步共动规范**（synchronous-comoving gauge），在该规范中物质流体的整体速度为零。

这两个规范下的密度微扰 $\delta_m^{\mathrm{N}}$ 和 $\delta_m^{\mathrm{S}}$ 并不相同。通过一阶[规范变换](@entry_id:176521)理论，可以推导出它们之间的关系 [@problem_id:3474161]：
$$
\delta_m^{\mathrm{S}}(\boldsymbol{k}, \tau) = \delta_m^{\mathrm{N}}(\boldsymbol{k}, \tau) - 3\mathcal{H}(\tau) v_m^{\mathrm{N}}(\boldsymbol{k}, \tau)
$$
其中 $\mathcal{H}$ 是共形哈勃参数，$v_m^{\mathrm{N}}$ 是[牛顿规范](@entry_id:160348)下的物质[速度势](@entry_id:262992)。在存在局域型非高斯性的情况下，[牛顿规范](@entry_id:160348)的密度场 $\delta_m^{\mathrm{N}}$ 在大尺度上存在一个与 $f_{\mathrm{NL}}/k^2$ 成正比的非物理“[规范模式](@entry_id:161405)”。直接使用它来设置[初始条件](@entry_id:152863)会引入巨大的、错误的初始位移。而共动规范密度 $\delta_m^{\mathrm{S}}$ 则没有这个问题，它直接与原始曲率微扰相关，行为良好。因此，为了保证大尺度上的物理一致性，**必须使用共动规范密度 $\delta_m^{\mathrm{S}}$ 来生成[N体模拟](@entry_id:157492)的[初始条件](@entry_id:152863)** [@problem_id:3474161]。

#### [拉格朗日微扰理论](@entry_id:751116)中的非高斯性

[N体模拟](@entry_id:157492)的初始条件通常使用**[拉格朗日微扰理论](@entry_id:751116)**（LPT）来设置，它通过[位移场](@entry_id:141476) $\boldsymbol{\psi}$ 将粒子从初始的拉格朗日格点位置 $\boldsymbol{q}$ 移动到欧拉位置 $\boldsymbol{x}(\boldsymbol{q}, a) = \boldsymbol{q} + \boldsymbol{\psi}(\boldsymbol{q}, a)$。[位移场](@entry_id:141476)可以展开为 $\boldsymbol{\psi} = \boldsymbol{\psi}^{(1)} + \boldsymbol{\psi}^{(2)} + \dots$。

原始非高斯性并不改变[引力](@entry_id:175476)演化的方程，因此，LPT的演化核（kernel），例如二阶[位移场](@entry_id:141476)的核 $L^{(2)}(\boldsymbol{k}_1, \boldsymbol{k}_2)$，其形式是**独立于原始非高斯性**的。例如，在爱因斯坦-[德西特宇宙](@entry_id:159695)中，该核的形式为 [@problem_id:3474126]：
$$
L^{(2)}(\boldsymbol{k}_1, \boldsymbol{k}_2) = \frac{3}{7} \frac{\boldsymbol{k}_1+\boldsymbol{k}_2}{|\boldsymbol{k}_1+\boldsymbol{k}_2|^2} \left(1 - \frac{(\boldsymbol{k}_1 \cdot \boldsymbol{k}_2)^2}{k_1^2 k_2^2}\right)
$$
非高斯性的影响体现在作为LPT源项的**初始线性密度场 $\delta_0$ 的统计性质发生了改变**。由于 $\delta_0$ 具有非零的[能谱](@entry_id:181780)，在计算二阶[位移场](@entry_id:141476) $\boldsymbol{\psi}^{(2)}$（它涉及 $\delta_0$ 的二次卷积）时，会产生与高斯情况不同的结果。特别是对于局域型非高斯性，其长短波[模式耦合](@entry_id:752088)特性会导致二阶[位移场](@entry_id:141476)在长波模式存在的条件下产生一个非零的条件期望值 $\langle \boldsymbol{\psi}^{(2)}(\boldsymbol{k}_S) | \Phi(\boldsymbol{k}_L) \rangle \neq 0$，从而改变粒子在大尺度环境下的运动轨迹 [@problem_id:3474126]。

### 数值挑战与诊断方法

在有限的起始[红移](@entry_id:159945) $z_{\mathrm{start}}$ 和离散化的模拟中，测量的非高斯信号可能被数值效应污染。区分真实的原始信号、[引力](@entry_id:175476)演化产生的信号和数值暂现模（transient modes）是至关重要的。

以下是一些有效的诊断技术 [@problem_id:3474127]：

1.  **演化历史检验**：不同来源的非高斯性具有不同的[时间演化](@entry_id:153943)标度。原始信号在物质为主导时期近似与[线性增长因子](@entry_id:751309) $D(a)$ 的三次方成比例 ($B_{\delta}^{\mathrm{prim}} \propto D^3(a)$)；[引力](@entry_id:175476)自发产生的信号与四次方成比例 ($B_{\delta}^{\mathrm{grav}} \propto D^4(a)$)；而数值暂现模则会更快地衰减。通过测量不同早期时刻的能谱并检验其是否符合 $D^3(a)$ 标度，可以分离出原始信号。

2.  **相位随机化**：原始非高斯性本质上是傅里叶模式之间特定的**相位关联**。一个强大的诊断方法是创建一对初始条件：一个具有真实的非高斯相位，另一个则在保持功率谱完全相同的情况下将其相位完全[随机化](@entry_id:198186)（“高斯化”）。对两者进行相同的数值演化后，其[高阶统计量](@entry_id:193349)（如能谱）的差异就精确地对应于原始相位关联所产生的信号。任何在两个模拟中都存在的非高斯信号则源于[引力](@entry_id:175476)演化或数值效应。

3.  **互相关技术**：将模拟演化出的密度场 $\delta(\boldsymbol{k}, a)$ 与已知的、无噪声的**原始势场 $\Phi(\boldsymbol{k})$** 进行[互相关](@entry_id:143353)，例如计算混合能谱 $B_{\delta\delta\Phi}$。数值暂现模通常与原始场不相关或相关性很弱，因此在这种[互相关](@entry_id:143353)中会被压制。这种方法可以有效地过滤掉数值噪声，分离出与原始场直接相关的信号，例如挤压极限下 $B_{\delta\delta\Phi} \propto P_{\delta}(k_S) P_{\Phi}(k_L)$ 的特征标度。

4.  **各向同性检验**：[宇宙学原理](@entry_id:158425)保证原始信号是统计各向同性的。然而，[数值模拟](@entry_id:137087)中的离散化效应（如初始粒子格点）可能会引入虚假的各向异性。通过旋转[位移场](@entry_id:141476)相对于粒子格点的方向，或者比较使用不同初始格点类型（如[晶格](@entry_id:196752) vs. 玻璃态）的模拟结果，可以检验测量到的[能谱](@entry_id:181780)是否存在对方向的依赖。任何显著的各向异性都标志着数值系统误差的存在。

通过综合运用这些原理和诊断方法，研究人员能够可靠地生成具有原始非高斯性的[宇宙学初始条件](@entry_id:747919)，并对其进行精确的演化和科学解释。