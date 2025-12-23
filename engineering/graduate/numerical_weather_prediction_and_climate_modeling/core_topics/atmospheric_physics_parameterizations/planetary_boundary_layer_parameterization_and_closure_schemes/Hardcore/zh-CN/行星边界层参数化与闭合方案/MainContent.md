## 引言
[行星边界层](@entry_id:187799)（PBL）是地球大气与地表直接相互作用的区域，其内部复杂的[湍流](@entry_id:151300)过程对天气和气候系统的能量、动量和物质交换起着决定性作用。然而，由于计算资源的限制，现代数值天气预报和气候模型无法直接解析这些微小而关键的[湍流](@entry_id:151300)涡旋，这便引出了大气科学中的一个核心挑战——“[湍流](@entry_id:151300)闭合问题”。如何准确地描述这些次网格[湍流](@entry_id:151300)对大尺度气流的集体效应，即PBL[参数化](@entry_id:265163)，已成为决定模型性能的关键环节。本文旨在为研究生和科研人员提供一个关于PBL[参数化](@entry_id:265163)方案的全面而深入的指南。

在接下来的章节中，我们将系统地探索这一领域。首先，在“原理与机制”一章，我们将深入研究[参数化](@entry_id:265163)背后的核心物理原理，从[雷诺平均](@entry_id:754341)引出[湍流](@entry_id:151300)闭合问题，并详细阐述从一阶局地闭合到更高级非局地方案的演进。随后，在“应用与跨学科连接”一章，我们将把理论应用于实践，探讨PBL方案如何在数值模型中诊断边界层结构、如何与陆面和海洋等其他[地球系统圈层](@entry_id:1124102)耦合，并讨论其在空气质量和复杂地形等前沿问题中的作用。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者将理论知识转化为解决实际问题的能力。通过本系列的学习，您将掌握PBL[参数化](@entry_id:265163)方案的设计精髓及其在地球系统科学中的核心地位。

## 原理与机制

本章旨在深入探讨[行星边界层](@entry_id:187799)（Planetary Boundary Layer, PBL）[参数化](@entry_id:265163)方案背后的核心物理原理与数学机制。在数值天气预报与气候模型中，由于计算网格无法解析PBL内部复杂的[湍流](@entry_id:151300)运动，我们必须通过[参数化](@entry_id:265163)的方法来描述其对大尺度气流的集体效应。本章将从PBL的基本物理特性出发，系统地阐述[湍流](@entry_id:151300)闭合问题的起源，介绍从一阶局地闭合到更高级方案的发展脉络，并揭示这些方案如何将复杂的[湍流](@entry_id:151300)过程与模型可解的平均场变量联系起来。

### 行星边界层的物理特性与[参数化](@entry_id:265163)的必要性

[行星边界层](@entry_id:187799)是直接受地球表面影响的对流层最底层，其典型厚度从百米到几千米不等。它的根本特征在于对地表强迫（如摩擦、加热、冷却）的快速响应。这种快速响应是通过[湍流混合](@entry_id:202591)实现的，其调整时间尺度远小于天气系统演变的时间尺度。

我们可以通过尺度分析来量化这一点。在一个典型的PBL中，[湍流](@entry_id:151300)涡旋将整个PBL混合均匀所需的时间，即“涡旋翻转时间”，可以通过[特征速度](@entry_id:165394)和PBL高度$h$来估算。在由风切变驱动的PBL中，特征速度为**摩擦速度** $u_*$，其[湍流](@entry_id:151300)调整时间尺度为 $T_{\mathrm{shear}} \sim h/u_*$。在由地表加热驱动的对流边界层中，特征速度为**对流速度尺度** $w_*$，其时间尺度为 $T_{\mathrm{buoy}} \sim h/w_*$。例如，在一个典型的白昼对流边界层中，当 $h \approx 800\,\mathrm{m}$，$u_* = 0.50\,\mathrm{m\,s^{-1}}$，$w_* = 1.20\,\mathrm{m\,s^{-1}}$ 时，我们得到的调整时间尺度 $T_{\mathrm{shear}} \approx 1600\,\mathrm{s}$ (约27分钟) 和 $T_{\mathrm{buoy}} \approx 670\,\mathrm{s}$ (约11分钟)。这些时间远小于一天（约$8.6 \times 10^4\,\mathrm{s}$）的日变化周期和天气系统的演变周期（数天）。这表明PBL能够在其内部迅速重新分配地表输入的动量、热量和水汽，从而与上方的**自由大气**（Free Troposphere, FT）形成鲜明对比 。

PBL与自由大气的另一个关键区别在于[湍流](@entry_id:151300)的强度。我们可以用**[湍流](@entry_id:151300)雷诺数** $Re_t$ 来衡量[湍流](@entry_id:151300)惯性输送相对于分子黏性扩散的主导地位。该[无量纲数](@entry_id:260863)可由[湍流](@entry_id:151300)动能（Turbulent Kinetic Energy, TKE）$k$ 和其耗散率 $\epsilon$ 构建：$Re_t = k^2/(\nu \epsilon)$，其中 $\nu$ 是空气的运动学分子黏度。在PBL内部，$k$ 和 $\epsilon$ 的值通常很大，导致 $Re_t$ 可高达 $10^7$ 或更高；而在自由大气中，[湍流](@entry_id:151300)活动微弱，使得 $Re_t$ 的值骤降数个数量级。这种 $Re_t$ 的巨大差异，为在模型中区分PBL和自由大气提供了物理上稳健且可操作的依据 。

为了进一步凸显[湍流参数化](@entry_id:1133496)的必要性，我们可以比较不同垂直输送过程的[特征时间尺度](@entry_id:276738)。考虑一个高度为 $H$ 的PBL，[湍流混合](@entry_id:202591)的时间尺度 $\tau_{\mathrm{mix}} = H^2/K$，其中 $K$ 是**涡动扩散系数**。而[分子扩散](@entry_id:154595)的时间尺度为 $\tau_{\nu} = H^2/\nu$。以 $H=1000\,\mathrm{m}$，$K \sim 50\,\mathrm{m}^2\,\mathrm{s}^{-1}$ 和 $\nu \sim 1.5 \times 10^{-5}\,\mathrm{m}^2\,\mathrm{s}^{-1}$ 为例，我们得到 $\tau_{\mathrm{mix}} \sim 2 \times 10^4\,\mathrm{s}$（约5.6小时），而 $\tau_{\nu} \sim 7 \times 10^{10}\,\mathrm{s}$（超过2000年）。这表明，如果没有[湍流](@entry_id:151300)，仅靠[分子运动](@entry_id:140498)，地表的信息需要数千年才能传递到PBL顶部。与此同时，大尺度平均垂直运动的输送时间尺度 $\tau_w = H/W$ （$W$为平均垂直速度）通常与湍流混合时间尺度相当或更长。因此，在一天的时间尺度内，[湍流](@entry_id:151300)是PBL中实现动量、热量和物质垂直快速输送的唯一有效机制。这正是为何我们必须在无法直接解析[湍流](@entry_id:151300)的数值模型中，对其效应进行[参数化](@entry_id:265163)的根本原因 。

### 闭合问题：从[雷诺平均](@entry_id:754341)到[湍流](@entry_id:151300)脉动通量

[参数化](@entry_id:265163)方案的数学基础源于对控制大气运动的[Navier-Stokes方程组](@entry_id:142275)进行平均化处理。最常用的方法是**[雷诺平均](@entry_id:754341)**。该方法将任何瞬时物理量 $a(\boldsymbol{x},t)$ 分解为一个系综平均（或时间/空间平均）量 $\overline{a}$ 和一个脉动量 $a'$ 的和：

$a(\boldsymbol{x},t) = \overline{a}(\boldsymbol{x},t) + a'(\boldsymbol{x},t)$

根据定义，脉动量的平均值为零，即 $\overline{a'} = 0$。对于一个与时空坐标无关的线性[平均算子](@entry_id:746605)，它与[微分](@entry_id:158422)运算可以交换次序，例如 $\overline{\partial a / \partial t} = \partial \overline{a} / \partial t$ 。

当我们将此分解应用于流体守恒方程中的[非线性平流](@entry_id:1128854)项时，问题便出现了。以一个[守恒标量](@entry_id:1122921) $\phi$（如位温或水汽[混合比](@entry_id:1127970)）的输送方程为例，其平流项为 $\nabla \cdot (\boldsymbol{u}\phi)$，其中 $\boldsymbol{u}$ 是速度矢量。对其进行[雷诺平均](@entry_id:754341)：

$\overline{\nabla \cdot (\boldsymbol{u}\phi)} = \nabla \cdot \overline{(\overline{\boldsymbol{u}} + \boldsymbol{u}')(\overline{\phi} + \phi')}$

展开并利用[平均算子](@entry_id:746605)的线性和 $\overline{a'}=0$ 的性质，我们得到：

$\overline{\boldsymbol{u}\phi} = \overline{\overline{\boldsymbol{u}}\overline{\phi} + \overline{\boldsymbol{u}}\phi' + \boldsymbol{u}'\overline{\phi} + \boldsymbol{u}'\phi'} = \overline{\boldsymbol{u}}\overline{\phi} + \overline{\boldsymbol{u}'\phi'}$

因此，平均后的平流项散度变为 $\nabla \cdot (\overline{\boldsymbol{u}}\overline{\phi}) + \nabla \cdot (\overline{\boldsymbol{u}'\phi'})$。这意味着，描述平均场 $\overline{\phi}$ 演变的方程中，出现了一个新的未知项 $\overline{\boldsymbol{u}'\phi'}$。这个项被称为**湍流通量**或**雷诺通量**，它代表了由速度脉动和标量脉动之间的相关性所产生的净输送效应。由于这个新项无法仅由平均场变量 $\overline{\boldsymbol{u}}$ 和 $\overline{\phi}$ 直接确定，使得平均后的方程组不封闭——未知量的数目超过了方程的数目。这就是著名的**[湍流](@entry_id:151300)闭合问题** (closure problem) 。[湍流参数化](@entry_id:1133496)方案的核心任务，正是为这个未知的湍流通量（如垂直通量 $\overline{w'\phi'}$）提供一个合理的、基于平均场量的表达式。

值得注意的是，在可压缩流中，由于密度 $\rho$ 也会脉动，直接使用雷诺平均会产生更复杂的项。在这种情况下，**密度加权的[法夫尔平均](@entry_id:198824)**（Favre averaging）提供了一个更简洁的框架。它定义了[法夫尔平均](@entry_id:198824)量 $\tilde{a} = \overline{\rho a}/\overline{\rho}$ 和法夫尔脉动量 $a''$，其关键性质是 $\overline{\rho a''} = 0$。在此框架下，平均后的方程形式更为简洁，但同样会产生需要闭合的[湍流通量](@entry_id:1133513)项，如 $\overline{\rho}\widetilde{w''\phi''}$ 。

### 一阶闭合：[梯度扩散假说](@entry_id:1125716)

解决闭合问题最简单的方法是**一阶闭合**方案，也称为**[K理论](@entry_id:160831)**或**[梯度扩散假说](@entry_id:1125716)** (gradient-diffusion hypothesis)。该假说类比分子扩散过程（如[傅里叶热传导定律](@entry_id:138911)），假设[湍流通量](@entry_id:1133513)与平均场量的梯度成正比，并且方向相反（即“顺梯度”输送）。对于垂直[湍流通量](@entry_id:1133513) $\overline{w'\phi'}$，其数学表达式为：

$\overline{w'\phi'} = -K_\phi \frac{\partial\overline{\phi}}{\partial z}$

其中，$K_\phi$ 被称为**[涡动扩散系数](@entry_id:196515)** (eddy diffusivity)，它是一个正值，量化了湍流混合的效率。与作为流体固有属性的[分子扩散系数](@entry_id:752110)不同，$K_\phi$ 是[湍流](@entry_id:151300)流场自身的一个属性，其大小取决于[湍流](@entry_id:151300)的强度和尺度 。

[梯度扩散假说](@entry_id:1125716)基于“局地性”假设，即[湍流混合](@entry_id:202591)主要由远小于平均场梯度变化尺度的涡旋完成。因此，该假说在某些特定条件下是物理合理的，例如在水平均匀、准[稳态](@entry_id:139253)、由风切变主导且层结为中性或弱稳定的[大气边界层](@entry_id:1121182)中。在这些情况下，[湍流](@entry_id:151300)涡旋的尺度相对较小，其混合效应确实可以近似为局地的梯度依赖过程 。

### 涡动扩散系数的[参数化](@entry_id:265163)：稳定性与相似性理论

一阶闭合方案的成功与否，关键在于如何准确地[参数化](@entry_id:265163)[涡动扩散系数](@entry_id:196515) $K_\phi$。$K_\phi$ 并非一个[普适常数](@entry_id:165600)，它强烈地依赖于流动的不稳定性和局地几何特征。

#### 稳定性参数：理查森数

大气层结的静力稳定性对[湍流](@entry_id:151300)的生成与抑制起着决定性作用。这一效应可以通过无量纲的**理查森数** (Richardson number) 来量化。

**[梯度理查森数](@entry_id:276161)** ($Ri_g$) 定义为浮力频率 $N^2$ 与平均风切变平方 $S^2$ 的比值：

$Ri_g = \frac{N^2}{S^2} = \frac{(g/\overline{\theta})\partial\overline{\theta}/\partial z}{(\partial\overline{u}/\partial z)^2+(\partial\overline{v}/\partial z)^2}$

$Ri_g$ 直接比较了层结稳定（或不稳定）对垂直运动的抑制（或促进）作用与风切变产生[湍流](@entry_id:151300)的倾向。当 $Ri_g  0$ 时，层结不稳定，[浮力](@entry_id:154088)产生[湍流](@entry_id:151300)；当 $Ri_g > 0$ 时，层结稳定，[浮力](@entry_id:154088)抑制[湍流](@entry_id:151300)；当 $Ri_g \approx 0$ 时，为中性层结。

另一个相关的参数是**通量理查森数** ($Ri_f$)，它直接从[湍流](@entry_id:151300)动能（TKE）收支方程中定义，为[浮力](@entry_id:154088)产生项 $B = (g/\overline{\theta})\overline{w'\theta'}$ 与切变产生项 $P = -(\overline{u'w'}\partial\overline{u}/\partial z + \overline{v'w'}\partial\overline{v}/\partial z)$ 的比值（通常带负号）：$Ri_f = -B/P$。$Ri_f$ 度量了[湍流](@entry_id:151300)能量在[浮力](@entry_id:154088)作用下被消耗（稳定情况）或产生（不稳定情况）的[相对效率](@entry_id:165851)。

利用一阶闭合假说，可以推导出这两个理查森数之间的关系：$Ri_f = Ri_g / Pr_t$，其中 $Pr_t = K_m/K_h$ 是**[湍流普朗特数](@entry_id:153739)**，即动量的涡动黏性系数与热量的[涡动扩散系数](@entry_id:196515)之比。理论和观测均表明，当 $Ri_g$ 增加到某个**临界理查森数**（通常约为0.25）时，[湍流](@entry_id:151300)会完全被抑制。许多[参数化](@entry_id:265163)方案正是通过引入依赖于 $Ri_g$ 的稳定度函数来调整 $K_\phi$ 的大小，以体现这种稳定性效应  。在稳定条件下，$Pr_t$ 通常随 $Ri_g$ 增加而增加，这意味着[湍流](@entry_id:151300)对动量的混合比对热量的混合更有效率  。

#### [地表层](@entry_id:1132680)与[莫宁-奥布霍夫相似性理论](@entry_id:1128126)

在PBL最底层的10%（称为**地表层**或**常通量层**），[湍流通量](@entry_id:1133513)随高度的变化很小，可近似为常数。对于这一特殊区域，**[莫宁-奥布霍夫相似性理论](@entry_id:1128126)** (Monin-Obukhov Similarity Theory, MOST) 提供了一个强大的理论框架 。

MOST的核心思想是：在水平均匀、准[稳态](@entry_id:139253)的[地表层](@entry_id:1132680)中，任何[无量纲化](@entry_id:136704)的[湍流统计](@entry_id:200093)量（如无量纲风切变或温度梯度）都应是无量纲高度 $\zeta = z/L$ 的普适函数。这里的关键[尺度参数](@entry_id:268705)包括：
- **摩擦速度** $u_* = (-\overline{u'w'}_s)^{1/2}$，代表由地表摩擦产生的[湍流](@entry_id:151300)速度尺度。
- **[奥布霍夫长度](@entry_id:1129033)** (Obukhov length) $L$，这是一个至关重要的长度尺度，其定义为：

$L = -\frac{u_*^3 \overline{\theta}}{k g \overline{w'\theta'}_s}$

其中 $k$ 是[冯·卡门常数](@entry_id:261117)（约0.4），$g$ 是重力加速度，$\overline{w'\theta'}_s$ 是地表运动学热通量。[奥布霍夫长度](@entry_id:1129033)的物理意义是：在高度 $z \approx |L|$ 处，由风切变产生的[湍流](@entry_id:151300)动能与由[浮力](@entry_id:154088)产生（或消耗）的[湍流](@entry_id:151300)动能大小相当。因此，$|z/L|$ 这个比值直接衡量了[浮力](@entry_id:154088)相对于切变的相对重要性 。
- 当层结不稳定时（$\overline{w'\theta'}_s > 0$），$L  0$。
- 当层结稳定时（$\overline{w'\theta'}_s  0$），$L > 0$。
- 当层结中性时（$\overline{w'\theta'}_s = 0$），$|L| \to \infty$。

在MOST框架下，$K_\phi$ 可以表示为 $K_\phi = \kappa u_* z / \phi_h(\zeta)$，其中 $\phi_h(\zeta)$ 是一个通过实验确定的普适稳定度函数。这为在[地表层](@entry_id:1132680)中[参数化](@entry_id:265163)[涡动扩散系数](@entry_id:196515)提供了坚实的理论基础。

#### 混合长模型

为了将涡动扩散系数的[参数化](@entry_id:265163)推广到整个PBL，**混合长** ($l$) 的概念被引入。混合长被设想为一个流体微团在失去其原有特性之前能够移动的特征距离。在一阶闭合中，涡动黏性系数通常被建模为 $K_m \sim l^2 S$。而在包含TKE[预报方程](@entry_id:1130221)的闭合方案中，则常采用 $K_m \sim c_\mu l \sqrt{e}$ 的形式，其中 $e$ 是TKE，$c_\mu$ 是经验常数。这两种形式在TKE产生与耗散达到局地平衡的条件下是相容的 。

混合长的具体形式有多种模型：
- **Prandtl模型**：在中性[地表层](@entry_id:1132680)，$l = \kappa z$，即混合长与离地高度成正比 。
- **Blackadar公式**：这是一个插值公式 $l = \frac{\kappa z}{1 + \kappa z / l_\infty}$，它保证了近地表 $l \approx \kappa z$ 的行为，并在高处渐近于一个由PBL外部尺度决定的上限 $l_\infty$ 。
- **Bougeault–Lacarrère (B-L) 公式**：这是一种基于能量的诊断方法，尤其适用于稳定层结。它将混合长定义为一个TKE为 $e$ 的气块在克服[浮力](@entry_id:154088)做功时所能上升的最大高度。在具有恒定[浮力频率](@entry_id:1121933) $N$ 的层结中，这导致 $l \sim \sqrt{2e}/N$。这个公式物理意义清晰，但在中性或不稳定条件下需要与其他模型混合使用 。

### 超越一阶与局地闭合

#### 高阶闭合与[湍流](@entry_id:151300)动能方程

一阶闭合方案将所有[湍流](@entry_id:151300)信息都压缩到一个涡动扩散系数中，这在许多情况下过于简化。**高阶闭合**方案通过为[湍流通量](@entry_id:1133513)（二阶矩）本身或更高阶的矩（如TKE，即二阶矩的迹）建立[预报方程](@entry_id:1130221)来提高模型的物理真实性。

最常见的“升阶”方法是采用**1.5阶闭合**，即引入一个关于[湍流](@entry_id:151300)动能 $e$ 的[预报方程](@entry_id:1130221)。对于水平[均匀流](@entry_id:272775)，该方程可写作：

$\frac{\partial e}{\partial t} = \underbrace{-\overline{u'w'}\frac{\partial \overline{u}}{\partial z}}_{P_s} + \underbrace{\frac{g}{\overline{\theta}}\overline{w'\theta'}}_{P_b} - \underbrace{\frac{\partial}{\partial z}\left[ \frac{1}{2}\overline{w' u_i' u_i'} + \frac{1}{\rho_0}\overline{w' p'} - \nu\frac{\partial e}{\partial z} \right]}_{\text{输运}} - \underbrace{\epsilon}_{\text{耗散}}$

等号右边各项依次为：由平均风切变产生的**切变产生项** ($P_s$)、由[浮力](@entry_id:154088)作用产生的**[浮力](@entry_id:154088)产生/破坏项** ($P_b$)、由[湍流](@entry_id:151300)自身、压力脉动和分子黏性共同作用的**输运项**，以及将TKE转化为内能的**分子耗散项** ($\epsilon$) 。通过预报 $e$ 的时空演变，模型可以更动态地描述[湍流](@entry_id:151300)的生命周期（生成、输运、耗散），并利用 $e$ 来构建[涡动扩散系数](@entry_id:196515)（如 $K_m \sim l\sqrt{e}$），从而避免了一阶闭合中对TKE局地平衡的隐含假设。

#### 非局地输运与对流边界层中的[逆梯度通量](@entry_id:1123121)

一阶局地闭合方案最显著的失败发生在白天的**对流边界层** (Convective Boundary Layer, CBL)。在这种由地表强烈加热驱动的边界层中，大尺度的、贯穿整个PBL的上升热泡和补偿性下沉气流主导了垂直输送。这种输送是**非局地**的，因为一个从地表附近升起的气块可以携带其高温特性，长距离地穿越PBL，其产生的通量取决于整个PBL的结构和边界强迫，而不仅仅是其所在位置的局地平均梯度。

在充分发展的CBL中，中上部区域通常是“充分混合”的，即平均位温 $\overline{\theta}$ 随高度基本不变（$\partial\overline{\theta}/\partial z \approx 0$）。然而，观测和[大涡模拟（LES）](@entry_id:273295)都显示，即使在梯度为零的区域，仍然存在显著的向上的热通量（$\overline{w'\theta'} > 0$）。对于这种情况，局地的梯度扩散公式 $\overline{w'\theta'} = -K_\theta \partial\overline{\theta}/\partial z$ 会错误地预测通量为零。这种在零梯度或甚至微弱顺梯度（$\partial\overline{\theta}/\partial z > 0$）区域出现的向上（负梯度方向）的热通量，被称为**逆梯度输运** (counter-gradient transport) 。

为了修正这一根本缺陷，[参数化](@entry_id:265163)方案需要引入一个**逆梯度订正项** $\gamma_\theta$：

$\overline{w'\theta'} = -K_\theta \left(\frac{\partial\overline{\theta}}{\partial z} - \gamma_\theta\right)$

这个订正项 $\gamma_\theta$ 代表了由大型[相干结构](@entry_id:182915)驱动的非局地输送贡献，它不依赖于局地梯度，而是与PBL整体的对流强度（如通过对流速度尺度 $w_*$）和边界层高度 $z_i$ 相关。这体现了从[地表层](@entry_id:1132680)（由 $u_*, L, z$ 标度）到对流混合层（由 $w_*, z_i$ 标度）的物理图像的转变，后者强调的是整体对流而非局地剪切与稳定度的平衡 。引入逆梯度项或采用更复杂的质量通量方案，是准确模拟对流边界层结构和演变的关键。