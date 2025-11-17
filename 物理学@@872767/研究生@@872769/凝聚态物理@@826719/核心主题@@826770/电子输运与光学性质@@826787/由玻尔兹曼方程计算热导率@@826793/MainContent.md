## 引言
[热导率](@entry_id:147276)是描述物质传热能力的核心物理量，对于[材料科学](@entry_id:152226)、电子工程乃至天体物理学都至关重要。宏观上，[傅里叶定律](@entry_id:136311)为我们提供了现象学的描述，但一个根本性的问题依然存在：宏观的[热导](@entry_id:189019)系数是如何由微观世界中载流子（如电子和[声子](@entry_id:140728)）的动力学行为和相互作用所决定的？填补这一宏观与微观之间鸿沟的关键理论工具，正是[玻尔兹曼输运方程](@entry_id:140472)（BTE）。

本文将带领读者系统地掌握如何利用[玻尔兹曼方程](@entry_id:141554)来计算和理解热导率。在“原理与机制”一章中，我们将从半经典框架出发，建立[玻尔兹曼输运方程](@entry_id:140472)，并引入[弛豫时间近似](@entry_id:138429)等关键概念。随后的“应用与跨学科联系”一章将展示这一理论框架的强大威力，通过分析其在晶体、纳米结构、[拓扑材料](@entry_id:142123)乃至[中子星](@entry_id:147259)等前沿和[交叉](@entry_id:147634)学科领域的具体应用。最后，在“动手实践”一章中，读者将有机会通过解决具体问题来巩固所学知识。

现在，让我们从构建理论的基石开始，深入探讨玻尔兹曼方程的基本原理与内在机制。

## 原理与机制

本章旨在深入探讨热导率的微观理论，其核心是[玻尔兹曼输运方程](@entry_id:140472)（Boltzmann Transport Equation, BTE）。我们将从半经典框架的基础出发，严格区分[能量流](@entry_id:142770)与热流，并阐明定义热导率的物理条件。随后，我们将详细介绍[弛豫时间近似](@entry_id:138429)（Relaxation Time Approximation, RTA）这一关键的简化方法，并探讨其[适用范围](@entry_id:636189)与局限性。最后，我们将该理论框架应用于具体的物理系统——[声子](@entry_id:140728)和电子的[热输运](@entry_id:198424)，并介绍一种更高级、更严谨的处理方法——[变分原理](@entry_id:198028)。

### 半经典框架：[玻尔兹曼输运方程](@entry_id:140472)

在微观尺度上，固体中的热量由[准粒子](@entry_id:136584)（如电子和[声子](@entry_id:140728)）携带。为了描述这些[准粒子](@entry_id:136584)在温度梯度驱动下的非平衡行为，我们采用[半经典方法](@entry_id:181818)。该方法将[准粒子](@entry_id:136584)视为具有确定能量 $\epsilon(\boldsymbol{k})$ 和[群速度](@entry_id:147686) $\boldsymbol{v}_{\boldsymbol{k}} = \frac{1}{\hbar}\nabla_{\boldsymbol{k}}\epsilon(\boldsymbol{k})$ 的[波包](@entry_id:154698)，其在相空间 $(\boldsymbol{r}, \boldsymbol{k})$ 中的演化由分布函数 $f(\boldsymbol{r}, \boldsymbol{k}, t)$ 描述。这个[分布函数](@entry_id:145626)给出了在时间 $t$、位置 $\boldsymbol{r}$ 附近，找到一个[晶体动量](@entry_id:136369)为 $\boldsymbol{k}$ 的[准粒子](@entry_id:136584)的概率。[分布函数](@entry_id:145626)的演化遵循[玻尔兹曼输运方程](@entry_id:140472)：

$$
\frac{\partial f}{\partial t} + \dot{\boldsymbol{r}}\cdot\nabla_{\boldsymbol{r}} f + \dot{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{k}} f = \left(\frac{\partial f}{\partial t}\right)_{\text{coll}}
$$

该方程的左侧描述了在没有碰撞的情况下，由于[准粒子](@entry_id:136584)在相空间中连续运动（“漂流”）而导致的[分布函数](@entry_id:145626)变化。右侧的[碰撞积分](@entry_id:152100)项则描述了由散射过程引起的 $f$ 的瞬时变化。让我们逐一解析这些项的物理意义 [@problem_id:3021067]：

1.  **漂移项 (Drift Term) $\dot{\boldsymbol{r}}\cdot\nabla_{\boldsymbol{r}} f$**：此项写作 $\boldsymbol{v}_{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{r}} f$，描述了由于空间不[均匀性](@entry_id:152612)引起的[分布函数](@entry_id:145626)变化。当系统存在空间梯度（如温度梯度 $\nabla T$）时，从邻近区域（例如，温度为 $T+\delta T$ 的区域）流入的粒子会携带不同的[分布](@entry_id:182848)特征。因此，$\boldsymbol{v}_{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{r}} f$ 代表了在 $\boldsymbol{r}$ 点，由于速度为 $\boldsymbol{v}_{\boldsymbol{k}}$ 的粒子流入和流出该无限小体积元而引起的净变化率。正是这一项驱动了由空间不均匀性（如[温度梯度](@entry_id:136845)）引起的[扩散输运](@entry_id:150792)现象，是热流的根源。

2.  **力项 (Force Term) $\dot{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{k}} f$**：此项描述了在外力作用下，[准粒子](@entry_id:136584)[动量空间](@entry_id:148936)[分布](@entry_id:182848)的变化。根据[半经典运动方程](@entry_id:138500)，$\hbar \dot{\boldsymbol{k}} = \boldsymbol{F}_{\text{ext}}$，其中 $\boldsymbol{F}_{\text{ext}}$ 是作用在[准粒子](@entry_id:136584)上的外力（如[电场](@entry_id:194326)或[磁场](@entry_id:153296)产生的[洛伦兹力](@entry_id:145104)）。在纯热导问题中，我们通常考虑没有外加[电场](@entry_id:194326)或[磁场](@entry_id:153296)的情况。在一个理想的周期性晶体中，[晶格](@entry_id:196752)的周期性势已经包含在能带结构 $\epsilon(\boldsymbol{k})$ 中，不会产生额外的力。因此，在两次碰撞之间，[准粒子](@entry_id:136584)的晶体动量是守恒的，即 $\dot{\boldsymbol{k}} = \mathbf{0}$。在这种情况下，力项为零，可以被忽略。

3.  **[碰撞积分](@entry_id:152100) (Collision Integral) $(\frac{\partial f}{\partial t})_{\text{coll}}$**：此项描述了各种[散射机制](@entry_id:136443)（如[杂质散射](@entry_id:267814)、[声子散射](@entry_id:140674)、[电子-电子散射](@entry_id:152847)等）如何使[分布函数](@entry_id:145626)趋向于平衡。它是[输运理论](@entry_id:143989)中最为复杂的部分，因为它包含了系统内相互作用的全部细节。

在[稳态](@entry_id:182458) (steady state) 且无外场的情况下，BTE 简化为：
$$
\boldsymbol{v}_{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{r}} f = \left(\frac{\partial f}{\partial t}\right)_{\text{coll}}
$$
这个方程的物理图像非常清晰：由[温度梯度](@entry_id:136845)驱动的漂移效应，恰好被使系统恢[复平衡](@entry_id:204586)的碰撞效应所平衡。

值得注意的是，整个半经典BTE框架的有效性依赖于一系列基本假设 [@problem_id:3021058]。首先，**[准粒子](@entry_id:136584)必须是良定义的**，这意味着其寿命 $\tau$ 必须足够长，使得能量的不确定性 $\Gamma = \hbar/\tau$ 远小于其特征激发能（对于[热输运](@entry_id:198424)，该[能量尺度](@entry_id:196201)为 $k_B T$），即 $\hbar/\tau \ll k_B T$。其次，**[半经典动力学](@entry_id:140913)必须成立**，这要求[准粒子](@entry_id:136584)的[平均自由程](@entry_id:139563) $\ell = v_F \tau$ 远大于其[德布罗意波长](@entry_id:139033)，即 $k_F \ell \gg 1$（Ioffe-Regel 判据）。最后，**[局域平衡假设](@entry_id:182180)必须有效**，即宏观物理量（如温度）在[平均自由程](@entry_id:139563) $\ell$ 的尺度上变化缓慢 ($L_{\nabla T} = T/|\nabla T| \gg \ell$)，这样[准粒子](@entry_id:136584)才能在局部区域内与环境充分[热化](@entry_id:142388)，使得局域温度 $T(\boldsymbol{r})$ 的概念有意义。对于金属中的电子，我们还需假设系统处于[简并费米气体](@entry_id:139445)状态，即 $k_B T \ll E_F$。

### 热流的定义与热导率

在从微观模型计算[热导率](@entry_id:147276)之前，我们必须精确定义“热流”。这并非一个微不足道的问题，尤其是在有[电荷](@entry_id:275494)载流子存在的系统中。

考虑一个输运系统，我们可以定义几个基本的流密度：
- **粒子数流密度 (Particle-number current)**: $\boldsymbol{J}_{N} = \int \frac{d^d k}{(2\pi)^d} \boldsymbol{v}_{\boldsymbol{k}} f$
- **[能量流](@entry_id:142770)密度 (Energy current)**: $\boldsymbol{J}_{E} = \int \frac{d^d k}{(2\pi)^d} \epsilon_{\boldsymbol{k}} \boldsymbol{v}_{\boldsymbol{k}} f$

[能量流](@entry_id:142770) $\boldsymbol{J}_E$ 描述了单位时间通过单位面积的总能量。然而，这部分能量不仅包括以热的形式传递的能量，还包括随粒子宏观流动而[对流](@entry_id:141806)的能量。在开放系统中，将一个粒子加入系统所需的能量是电化学势 $\bar{\mu}$。因此，一个粒子流 $\boldsymbol{J}_N$ 会携带一部分[能量流](@entry_id:142770)，其大小为 $\bar{\mu}\boldsymbol{J}_N$。这部分能量与粒子的整体运动相关联，而非热量本身。

**热流密度 (Heat current)** $\boldsymbol{J}_Q$ 被定义为总[能量流](@entry_id:142770)中扣除这部分[对流](@entry_id:141806)能量之后的部分 [@problem_id:3021065]：

$$
\boldsymbol{J}_Q = \boldsymbol{J}_E - \bar{\mu}\boldsymbol{J}_N
$$

其中 $\bar{\mu} = \mu + q\phi$ 是电化学势，它包括化学势 $\mu$ 和[静电势能](@entry_id:204009) $q\phi$。将流密度的积分形式代入，我们得到：

$$
\boldsymbol{J}_Q = \int \frac{d^d k}{(2\pi)^d} (\epsilon_{\boldsymbol{k}} - \bar{\mu}) \boldsymbol{v}_{\boldsymbol{k}} f
$$

这表明，热流是相对于电化学势测量的[能量流](@entry_id:142770)动。

热导率 $\kappa$ 是通过[傅里叶热传导定律](@entry_id:138911)定义的，该定律将热流与[温度梯度](@entry_id:136845)联系起来：$\boldsymbol{J}_Q = -\kappa \nabla T$。在一个导体中，温度梯度不仅会引起热流，还会通过塞贝克效应（Seebeck effect）驱动[电荷](@entry_id:275494)载流子[扩散](@entry_id:141445)，从而可能产生电流。为了纯粹地测量由[热传导](@entry_id:147831)引起的[能量输运](@entry_id:183081)，我们必须消除由净[电荷](@entry_id:275494)流动所携带的[对流](@entry_id:141806)能量的贡献。这要求我们在**零[电荷](@entry_id:275494)电流**的条件下定义和测量[热导率](@entry_id:147276)，即 $\boldsymbol{J}_c = q\boldsymbol{J}_N = \mathbf{0}$。这被称为**开路 (open-circuit) 条件** [@problem_id:3021013]。

在实验上，这意味着将样品置于温度梯度中，但不连接任何外部电路。样品内部会自动建立一个[静电场](@entry_id:268546)（塞贝克[电场](@entry_id:194326)），该[电场](@entry_id:194326)产生的电力恰好抵消了由[温度梯度](@entry_id:136845)引起的载流子[扩散](@entry_id:141445)，从而使净电流为零。

我们可以用[线性响应理论](@entry_id:145737)更形式化地描述这一点。[电荷](@entry_id:275494)流 $\boldsymbol{J}$ 和热流 $\boldsymbol{J}_Q$ 可以表示为[热力学](@entry_id:141121)驱动力（电[化学势梯度](@entry_id:142294)和温度梯度）的线性组合：
$$
\boldsymbol{J} = L_{11} (\boldsymbol{E} - \frac{\nabla\mu}{e}) + L_{12} (-\frac{\nabla T}{T})
$$
$$
\boldsymbol{J}_Q = L_{21} (\boldsymbol{E} - \frac{\nabla\mu}{e}) + L_{22} (-\frac{\nabla T}{T})
$$
其中 $L_{ij}$ 是[输运系数](@entry_id:136790)。根据定义，热导率是在 $\boldsymbol{J}=\mathbf{0}$ 的条件下测量的。从第一个方程解出 $(\boldsymbol{E} - \frac{\nabla\mu}{e}) = -\frac{L_{12}}{L_{11}}(-\frac{\nabla T}{T})$，并代入第二个方程，我们得到：
$$
\boldsymbol{J}_Q = \left( L_{22} - \frac{L_{21}L_{12}}{L_{11}} \right) \left(-\frac{\nabla T}{T}\right)
$$
与 $\boldsymbol{J}_Q = -\kappa \nabla T$ 比较，我们得到开路条件下的热导率 [@problem_id:3021013]：
$$
\kappa = \frac{1}{T} \left( L_{22} - \frac{L_{12}L_{21}}{L_{11}} \right)
$$
这个表达式明确显示，热导率不仅与直接的热输运系数 $L_{22}$ 有关，还受到热电耦合效应（由 $L_{12}$ 和 $L_{21}$ 描述，根据昂萨格倒易关系 $L_{12}=L_{21}$）的修正。

### [碰撞积分](@entry_id:152100)与[弛豫时间近似](@entry_id:138429)

求解BTE的关键和难点在于处理复杂的[碰撞积分](@entry_id:152100)项 $\mathcal{I}[f]$。一个极其有效且广泛应用的简化是**[弛豫时间近似](@entry_id:138429) (Relaxation Time Approximation, RTA)**。其核心思想是，任何对[局域平衡](@entry_id:156295)[分布](@entry_id:182848) $f_0$ 的偏离 $\delta f = f - f_0$ 都会以一个特征时间尺度 $\tau$ 指数衰减回平衡状态。数学上，这表示为：

$$
\left(\frac{\partial f}{\partial t}\right)_{\text{coll}} \approx -\frac{f - f_0}{\tau} = -\frac{\delta f}{\tau}
$$

其中 $\tau$ 被称为**弛豫时间**，它通常依赖于[准粒子](@entry_id:136584)的能量 $\epsilon$ 和其他[量子数](@entry_id:145558)。

RTA的有效性基于几个关键假设 [@problem_id:3021051]：
1.  **[线性响应](@entry_id:146180)**：系统对驱动力（如 $\nabla T$）的响应是线性的，这意味着偏离平衡的 $\delta f$ 足够小，可以对[碰撞积分](@entry_id:152100)进行线性化。
2.  **详细平衡**：在完全平衡状态下（即 $\nabla T = \mathbf{0}$），碰撞必须使系统保持不变，即 $\mathcal{I}[f_0] = 0$。这源于[微观可逆性原理](@entry_id:137392)。
3.  **[弹性散射](@entry_id:152152)**：RTA最适用于[弹性散射](@entry_id:152152)过程，即散射前后[准粒子](@entry_id:136584)的能量不变。这使得能量壳层之间[解耦](@entry_id:637294)，每个能量 $\epsilon$ 都可以被赋予一个独立的弛豫时间 $\tau(\epsilon)$。
4.  **局域化与非关联性**：碰撞被假定为瞬时发生的、在空间上局域的、且彼此统计独立的（[马尔可夫过程](@entry_id:160396)）。

在RTA下，[稳态](@entry_id:182458)BTE变为一个简单的[代数方程](@entry_id:272665)：$\boldsymbol{v}_{\boldsymbol{k}}\cdot\nabla_{\boldsymbol{r}} f_0 = -\frac{\delta f}{\tau_{\boldsymbol{k}}}$。由此可以解出非[平衡分布](@entry_id:263943)的偏离项 $\delta f$，进而计算各种[输运系数](@entry_id:136790)。

然而，我们必须认识到 $\tau$ 的深刻含义及其局限性。当散射概率 $W_{\boldsymbol{k}\boldsymbol{k}'}$ 依赖于散射前后动量方向的夹角 $\theta$ 时，一个简单的标量弛豫时间就不再足够。特别是，小角度[前向散射](@entry_id:191808)虽然能有效地改变粒子的动量方向，但对弛豫一个净电流（无论是[电荷](@entry_id:275494)流还是热流）的贡献很小。为了正确描述电流的衰减，我们需要引入**输运弛豫时间 (transport relaxation time)** $\tau_{\text{tr}}$ [@problem_id:3021047]。对于[各向异性能](@entry_id:200263)带上的弹性散射，输运[弛豫率](@entry_id:150136)定义为：

$$
\frac{1}{\tau_{\text{tr}}(\boldsymbol{k})} = \sum_{\boldsymbol{k}'} W_{\boldsymbol{k}\boldsymbol{k}'} \left( 1 - \frac{\boldsymbol{v}_{\boldsymbol{k}'} \cdot \hat{\boldsymbol{e}}}{\boldsymbol{v}_{\boldsymbol{k}} \cdot \hat{\boldsymbol{e}}} \right) \delta(\epsilon_{\boldsymbol{k}'} - \epsilon_{\boldsymbol{k}})
$$

其中 $\hat{\boldsymbol{e}}$ 是电流方向。对于各向同性的抛物线能带，该表达式简化为我们更熟悉的形式：

$$
\frac{1}{\tau_{\text{tr}}(\epsilon)} = \sum_{\boldsymbol{k}'} W_{\boldsymbol{k}\boldsymbol{k}'} (1 - \cos\theta_{\boldsymbol{k}\boldsymbol{k}'}) \delta(\epsilon_{\boldsymbol{k}'} - \epsilon_{\boldsymbol{k}})
$$

这里的 $(1 - \cos\theta)$ 因子给大角度散射（$\theta \approx \pi$）赋予了最大的权重，而对[前向散射](@entry_id:191808)（$\theta \approx 0$）的权重则趋于零。这正确地反映了不同角度散射对电流弛豫效率的贡献。因此，输运弛豫时间 $\tau_{\text{tr}}$ 通常不等于从单粒子谱函数虚部得到的单[粒子寿命](@entry_id:151134) $\tau_{sp}$，后者计算的是总[散射率](@entry_id:143589)，不区分散射角度。

此外，RTA在某些情况下会完全失效。一个重要的例子是涉及**[非弹性散射](@entry_id:138624)**的[热导率](@entry_id:147276)计算。例如，在低温下金属中的[电子-[声子散](@entry_id:138098)射](@entry_id:140674)（Bloch-Grüneisen 区），电子在散射过程中吸收或发射一个[声子](@entry_id:140728)，其能量 $\hbar\omega_{\boldsymbol{q}}$ 与电子的[热激发](@entry_id:275697)能 $k_B T$ 相当。这种散射对于[热输运](@entry_id:198424)而言是显著非弹性的。在这种情况下，[碰撞算符](@entry_id:189499)会耦合不同能量的电子态，无法用一个简单的、仅依赖于初始能量的 $\tau(\epsilon)$ 来描述。此时，完整的线性化[碰撞积分](@entry_id:152100)必须被保留 [@problem_id:3021042]：

$$
I_{\text{e-ph}}^{\text{lin}}[\psi](\boldsymbol{k}) \propto \sum_{\boldsymbol{q}} |M_{\boldsymbol{q}}|^2 \left\{ \dots [\psi(\boldsymbol{k}) - \psi(\boldsymbol{k}+\boldsymbol{q})] + \dots [\psi(\boldsymbol{k}) - \psi(\boldsymbol{k}-\boldsymbol{q})] \right\}
$$

其中 $\psi$ 是与 $\delta f$ 相关的非平衡函数。这种能量上的非对角性是导致维德曼-弗朗兹定律（Wiedemann-Franz law）在低温下失效的根本原因。

### 应用与机制

#### [声子](@entry_id:140728)[热导率](@entry_id:147276)

在绝缘体中，热量主要由晶格振动量子——[声子](@entry_id:140728)——来输运。利用BTE和RTA，我们可以推导出[声子](@entry_id:140728)[热导率](@entry_id:147276)的动力学理论表达式：

$$
\kappa = \frac{1}{3} \int_0^{\omega_{\text{max}}} C_{\text{mode}}(\omega) v_g^2(\omega) \tau(\omega) D(\omega) d\omega
$$

其中 $C_{\text{mode}}$ 是单模[热容](@entry_id:137594)， $v_g$ 是[群速度](@entry_id:147686)， $\tau$ 是[弛豫时间](@entry_id:191572)， $D(\omega)$ 是[声子态密度](@entry_id:199476)。

让我们考虑一个具体的例子：在高温 ($T \gg \Theta_D$, $\Theta_D$为[德拜温度](@entry_id:140328)) 下，[声子](@entry_id:140728)-[声子](@entry_id:140728)间的**乌姆克拉普（Umklapp, U）过程**成为限制[热导率](@entry_id:147276)的主要[散射机制](@entry_id:136443)。[乌姆克拉普过程](@entry_id:145784)是一种涉及三个或更多[声子](@entry_id:140728)的散射，其总晶体动量不守恒（相差一个[倒格矢](@entry_id:263351)）。这种动量非守恒的过程是产[生热](@entry_id:167810)阻的必要条件。在高温极限下，每个[声子模式](@entry_id:201212)的[热容](@entry_id:137594)趋于经典值 $k_B$（[杜隆-珀蒂定律](@entry_id:191078)），且所有[声子模式](@entry_id:201212)都被充分激发。三[声子散射](@entry_id:140674)率主要由[声子](@entry_id:140728)数量决定，后者正比于温度$T$。因此，[乌姆克拉普散射](@entry_id:136879)率近似为 $\tau_U^{-1} \propto T$。代入动力学公式，我们得到高温下的热导率行为：$\kappa(T) \propto 1/T$。这表明，随着温度升高，[声子](@entry_id:140728)间散射愈发频繁，导致热导率下降，这是绝缘体在高温下的典型行为。相反，在低温下 ($T \ll \Theta_D$)，能参与U过程的大动量[声子](@entry_id:140728)数量呈指数抑制，其数量正比于 $\exp(-\Theta_U/T)$（其中 $\Theta_U$ 是一个与U过程激活能相关的特征温度），这导致[热导率](@entry_id:147276)随温度降低而指数增长 [@problem_id:3021053]。

一个更精细的问题是**正常（Normal, N）过程**的作用。N过程是同样是[声子](@entry_id:140728)间的散射，但它们守恒总[晶体动量](@entry_id:136369)。根据简单的RTA，如果将N过程和U过程的散射率通过[马西森定则](@entry_id:141203) ($1/\tau = 1/\tau_N + 1/\tau_R$) 相加，我们会错误地将N过程也视为产生热阻的机制。然而，在纯粹的[德拜模型](@entry_id:141712)中，热流正比于总动量，因此守恒动量的N过程本身不能弛豫热流。在N过程远快于U过程的**[流体动力学](@entry_id:136788)区 (hydrodynamic regime)** ($\tau_N \ll \tau_R$)，频繁的N过程会使[声子](@entry_id:140728)系统达到一个漂移的[局域平衡](@entry_id:156295)态，形成一种称为**[声子泊肃叶流](@entry_id:137131) (phonon Poiseuille flow)** 的[集体运动](@entry_id:747472)。此时，[热导率](@entry_id:147276)由缓慢的动量弛豫过程（U过程）决定，$\kappa \propto \tau_R$，远大于简单RTA给出的 $\kappa_{\text{RTA}} \propto \tau_N$ 的结果。这揭示了[马西森定则](@entry_id:141203)在处理不同类型散射过程时的局限性 [@problem_id:3021035]。

#### [电子热导率](@entry_id:262860)

在金属中，热量主要由导电电子携带。一个著名的结果是维德曼-弗朗兹定律，它指出在许多金属中，[热导率](@entry_id:147276) $\kappa$ 与电导率 $\sigma$ 的比值正比于温度 $T$，即 $\kappa/\sigma = LT$，其中 $L$ 是洛伦兹数。该定律的微观基础是，对于弹性[杂质散射](@entry_id:267814)，弛豫[电荷](@entry_id:275494)流和热流的机制是相同的。然而，正如我们前面提到的，当电子-[声子](@entry_id:140728)非弹性散射变得重要时，该定律会失效。这是因为[电导率](@entry_id:137481)主要关心动量弛豫，而[热导率](@entry_id:147276)对[能量弛豫](@entry_id:136820)更为敏感 [@problem_id:3021042]。

### 高级形式：变分原理

当RTA失效或我们寻求更精确的解时，变分原理提供了一个强大而严谨的途径来求解线性化的玻尔兹曼方程 [@problem_id:3021054]。该方法源于热力学第二定律，其核心思想是：在[非平衡稳态](@entry_id:141783)下，系统会选择一个能以[最小熵产生](@entry_id:183433)率来维持给定热流的[分布函数](@entry_id:145626)。

形式上，这可以表述为一个约束极值问题。熵产生率与[碰撞算符](@entry_id:189499)的[期望值](@entry_id:153208) $\langle \psi | \hat{C} | \psi \rangle$ 成正比，其中 $\hat{C}$ 是（正半定的）线性化[碰撞算符](@entry_id:189499)，$\psi$ 是描述偏离平衡的函数，而[内积](@entry_id:158127) $\langle \cdot | \cdot \rangle$ 是一个适当加权的积分。热流可以表示为 $\langle Y | \psi \rangle$，其中 $Y$ 是一个与热流算符相关的已知函数。我们的目标是在保持热流 $\langle Y | \psi \rangle = J_Q$ 为常数的约束下，最小化熵产生 $\langle \psi | \hat{C} | \psi \rangle$。

使用[拉格朗日乘子法](@entry_id:176596)，我们构建如下泛函并求其极值：

$$
F[\psi, \lambda] = \langle \psi | \hat{C} | \psi \rangle - 2\lambda (\langle Y | \psi \rangle - J_Q)
$$

对该泛函求变分，可以得到线性化的[玻尔兹曼方程](@entry_id:141554) $\hat{C}\psi = \lambda Y$。这个方法的强大之处在于，即使我们无法精确求解该方程，也可以通过代入一个物理上合理的[试探函数](@entry_id:756165) $\psi_{\text{trial}}$ 来获得[热导率](@entry_id:147276)的良好近似。例如，选择一个与热流算符形式相同的[试探函数](@entry_id:756165)，我们就可以得到输运弛豫时间的变分表达式，该表达式在形式上推广了我们之前讨论的加权散射率 [@problem_id:3021047]。变分原理为超越简单的RTA、系统地处理复杂[散射机制](@entry_id:136443)提供了坚实的理论基础。