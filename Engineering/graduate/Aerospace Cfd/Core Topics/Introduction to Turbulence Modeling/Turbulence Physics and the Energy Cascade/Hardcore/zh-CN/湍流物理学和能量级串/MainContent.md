## 引言
[湍流](@entry_id:151300)，作为自然界与工程领域中无处不在的现象，从飞机掠过天际到星系间的气体运动，其复杂性与混沌特性长久以来都是物理学与工程学面临的巨大挑战。理解[湍流](@entry_id:151300)的关键在于破解其内在的能量传递机制。[能量串级](@entry_id:153717)（energy cascade）概念的提出，为我们提供了一个优雅而强大的框架，它描绘了一幅能量如何从被注入的宏观大尺度，通过一系列涡的破碎与变形，最终在微观小尺度上耗散为热量的壮丽图景。然而，这一跨越多个数量级的过程，其背后的物理原理、数学描述以及在不同学科中的具体表现，构成了理解[湍流](@entry_id:151300)的核心知识缺口。

本文旨在系统性地梳理[湍流](@entry_id:151300)物理与能量串级的核心知识。我们将带领读者穿越理论的殿堂与应用的广阔天地，构建一个完整而深入的知识体系。在“**原理与机制**”一章中，我们将从流体运动的控制方程出发，揭示[湍流](@entry_id:151300)的起源，并深入剖析能量串级的物理机制——涡拉伸，以及奠定其统计规律的柯尔莫哥洛夫理论。随后，在“**应用与跨学科联系**”一章中，我们将展示[能量串级](@entry_id:153717)理论如何成为现代[计算流体动力学](@entry_id:142614)（CFD）仿真的基石，并探讨其在化学、[地球物理学](@entry_id:147342)乃至天体物理学等领域的惊人普适性。最后，通过“**动手实践**”部分，读者将有机会运用所学知识解决实际问题，从理论推导到计算分析，加深对能量串级这一核心概念的理解。

## 原理与机制

本章旨在深入探讨[湍流物理学](@entry_id:756228)的核心原理与关键机制。我们将从流体运动的控制方程出发，揭示[湍流](@entry_id:151300)现象的数学根源，并引入统计方法来描述其看似随机的行为。随后，我们将系统地阐述[湍流物理学](@entry_id:756228)中最核心的概念——**[能量串级](@entry_id:153717) (energy cascade)**，解释能量如何在不同尺度的涡旋之间传递。我们将剖析驱动这一过程的关键物理机制，即**涡拉伸 (vortex stretching)**，并比较其在三维与[二维湍流](@entry_id:198015)中的根本差异。最后，我们将介绍[安德雷·柯尔莫哥洛夫](@entry_id:272558) (Andrey Kolmogorov) 的相似性假设，它为[湍流](@entry_id:151300)的[标度律](@entry_id:266186)提供了理论基石，并探讨超越经典理论的**间歇性 (intermittency)** 现象。

### 控制方程与[湍流](@entry_id:151300)的起源

流体运动由一组[偏微分](@entry_id:194612)方程——**[纳维-斯托克斯](@entry_id:276387) ([Navier-Stokes](@entry_id:276387)) 方程**——所支配，它们是[质量守恒](@entry_id:204015)和[牛顿第二定律](@entry_id:274217)在流体介质中的数学体现。对于密度 $\rho$、速度场 $\boldsymbol{u}(\boldsymbol{x},t)$ 和压[力场](@entry_id:147325) $p(\boldsymbol{x},t)$ 的[牛顿流体](@entry_id:263796)，其动量守恒方程为：
$$
\frac{\partial (\rho \boldsymbol{u})}{\partial t} + \nabla\cdot(\rho\boldsymbol{u}\boldsymbol{u})=-\nabla p+\nabla\cdot\boldsymbol{\tau}
$$
其中 $\boldsymbol{\tau}$ 是粘性应力张量。质量守恒由连续性方程描述：
$$
\frac{\partial \rho}{\partial t} + \nabla\cdot(\rho\boldsymbol{u})=0
$$
这些方程的**[非线性平流](@entry_id:1128854)项 (nonlinear advection term)** $\nabla\cdot(\rho\boldsymbol{u}\boldsymbol{u})$ 是[湍流](@entry_id:151300)复杂性的根源。当流动的**雷诺数 (Reynolds number)**——代表[惯性力](@entry_id:169104)与粘性力之比——足够高时，该项的主导作用会使得任何微小的扰动被放大和扭曲，导致流动从平滑的层流状态转变为时空上极不规则、看似混乱的[湍流](@entry_id:151300)状态。

在航空航天领域的许多应用中，例如亚音速翼型绕流，流动马赫数 $M$ 通常远小于1。在这种情况下，流体密度变化可以忽略，从而引出**[不可压缩流](@entry_id:140301) (incompressible flow)** 的重要简化模型 。不可压缩假设包含两个关键约束：密度为常数（$\rho = \text{const}$），以及速度场满足**[无散约束](@entry_id:755035) (solenoidal constraint)** $\nabla\cdot \boldsymbol{u}=0$。在此模型下，连续性方程简化为[无散约束](@entry_id:755035)本身，而[动量方程](@entry_id:197225)则变为：
$$
\frac{\partial \boldsymbol{u}}{\partial t} + \boldsymbol{u}\cdot\nabla \boldsymbol{u} = -\frac{1}{\rho}\nabla p + \nu \nabla^2 \boldsymbol{u}
$$
其中 $\nu = \mu/\rho$ 是[运动粘度](@entry_id:275614)。

值得注意的是，在不可压缩模型中，压力的角色发生了根本性转变。它不再是与密度和温度相关的[热力学状态](@entry_id:755916)量，而是一个**[拉格朗日乘子](@entry_id:142696) (Lagrange multiplier)** 。其作用是通过瞬时调整自身，来确保速度场在任何时刻都满足 $\nabla\cdot \boldsymbol{u}=0$ 的约束。对动量方程两边取散度，并利用 $\nabla\cdot \boldsymbol{u}=0$，我们可以得到一个关于压力的**泊松方程 (Poisson equation)**：
$$
\nabla^2 p = -\rho \nabla \cdot (\boldsymbol{u} \cdot \nabla \boldsymbol{u})
$$
这是一个椭圆型方程，意味着边界上任何一点的扰动会瞬时（以无限速度）传播到整个流场。这与可压缩流中压力波（声波）以有限速度传播的物理特性形成鲜明对比，后者的控制方程具有双曲性。因此，不可压缩假设有效地滤除了声学现象。在动能预算中，压力项 $\boldsymbol{u} \cdot \nabla p$ 可以写成一个纯散度项 $\nabla \cdot (p\boldsymbol{u})$，它在全域积分后为零，表明压力在[不可压缩流](@entry_id:140301)中仅重新分布能量，而不产生或消耗净动能 。与之相对，在[可压缩流](@entry_id:747589)中，动能方程会出现一个**压力-膨胀项 (pressure–dilatation term)** $p\nabla\cdot\boldsymbol{u}$，它使得动能和内能之间可以相互转化，为能量串级提供了额外的通道。

### [湍流](@entry_id:151300)的统计描述

由于[湍流](@entry_id:151300)的混沌特性，精确预测每一个时空点的[瞬时速度](@entry_id:167797)变得不切实际。因此，我们采用统计方法来描述[湍流](@entry_id:151300)。奥斯鲍恩·雷诺 (Osborne Reynolds) 提出的**[雷诺分解](@entry_id:267756) (Reynolds decomposition)** 是这一方法的核心。我们将[瞬时速度](@entry_id:167797) $u_i$ 分解为系综平均（或在统计定常态下的时间平均）的**[平均速度](@entry_id:267649) (mean velocity)** $U_i$ 和**脉动速度 (fluctuating velocity)** $u_i'$ 的和 ：
$$
u_i(\boldsymbol{x},t) = U_i(\boldsymbol{x},t) + u_i'(\boldsymbol{x},t)
$$
其中，[平均算子](@entry_id:746605) $\langle \cdot \rangle$ 具有线性、对确定量不变等性质。根据定义，脉动量的平均值为零，即 $\langle u_i' \rangle = 0$。

将[雷诺分解](@entry_id:267756)代入[纳维-斯托克斯方程](@entry_id:142275)并取平均，我们得到**雷诺平均纳维-斯托克斯 (Reynolds-Averaged [Navier-Stokes](@entry_id:276387), RANS) 方程**。在这个过程中，[非线性平流](@entry_id:1128854)项 $\langle u_i u_j \rangle$ 产生了一个关键项：
$$
\langle u_i u_j \rangle = \langle (U_i + u_i')(U_j + u_j') \rangle = U_i U_j + \langle u_i' u_j' \rangle
$$
这里的 $\langle u_i' u_j' \rangle$ 项被称为**雷诺应力张量 (Reynolds stress tensor)**（通常乘以 $-\rho$）。它代表了速度脉动对平均[动量输运](@entry_id:139628)的贡献。由于 $\langle u_i' u_j' \rangle$ 是一个新的未知量，这导致了著名的**[湍流封闭问题](@entry_id:268973) (turbulence closure problem)**。

为了建立普适的[湍流理论](@entry_id:264896)，我们常常引入理想化的[统计对称性](@entry_id:272586)假设 ：
*   **[统计均匀性](@entry_id:136481) (Statistical homogeneity)**：指所有 $n$ 点联合统计量在空间平移下保持不变。这意味着单点统计量（如[平均速度](@entry_id:267649)、[湍动能](@entry_id:262712)）在空间中是常数，而[两点相关函数](@entry_id:185074) $R_{ij}(\boldsymbol{x}, \boldsymbol{r}, t) = \langle u_i(\boldsymbol{x}, t) u_j(\boldsymbol{x} + \boldsymbol{r}, t)\rangle$ 仅依赖于[分离矢量](@entry_id:268468) $\boldsymbol{r}$，而与绝对位置 $\boldsymbol{x}$ 无关。
*   **统计各向同性 (Statistical isotropy)**：指所有 $n$ 点统计量在坐标系任意旋转下保持不变。对于均匀[湍流](@entry_id:151300)，这意味着两点相关性仅依赖于分离距离 $r=|\boldsymbol{r}|$，而与方向无关。
*   **统计定常性 (Statistical stationarity)**：指所有 $n$ 点统计量在时间平移下保持不变。

需要强调的是，这些[统计对称性](@entry_id:272586)是关于**统计系综 (statistical ensemble)** 的性质，与单个流场实现的确定性对称（如[管道流](@entry_id:189531)的[轴对称](@entry_id:1130776)）有着本质区别 。虽然真实世界的流动（如翼型边界层）通常既不均匀也非各向同性，但这些理想化概念在局部小尺度上仍具有近似的有效性，为构建理论模型提供了坚实的基础。

### [能量串级](@entry_id:153717)：理查森的洞见与柯尔莫哥洛夫理论

[湍流](@entry_id:151300)的维持需要持续的能量供应。在许多工程流动中，例如均匀剪切流或边界层中，能量通过平均速度梯度做功的方式从平均流注入到[湍流](@entry_id:151300)脉动中。描述[湍动能](@entry_id:262712) $k = \frac{1}{2}\langle u_i' u_i' \rangle$ 演化的[输运方程](@entry_id:174281)中，这一能量注入过程由**[湍流生成](@entry_id:189980)项 (turbulence production term)** $\mathcal{P} = -\langle u_i' u_j' \rangle \frac{\partial U_i}{\partial x_j}$ 来描述 。例如，在[平均速度](@entry_id:267649)为 $U_1 = S x_2$ 的剪切流中，生成项为 $\mathcal{P} = - \langle u_1' u_2' \rangle S$。要维持[湍流](@entry_id:151300)，$\mathcal{P}$ 必须为正，这意味着[雷诺切应力](@entry_id:148861) $\langle u_1' u_2' \rangle$ 和平均剪切率 $S$ 的符号必须相反。

注入的能量并不会停留在其被注入的大尺度涡结构中。相反，它会经历一个被称为**[能量串级](@entry_id:153717) (energy cascade)** 的过程。这是由刘易斯·弗莱·理查森 (Lewis Fry Richardson) 在一首著名的诗中首次生动描绘的：
> "Big whorls have little whorls that feed on their velocity, and little whorls have lesser whorls and so on to viscosity."

这个过程的核心驱动力正是[纳维-斯托克斯方程](@entry_id:142275)中的[非线性平流](@entry_id:1128854)项。虽然该项在全局上是能量守恒的——即它不改变整个流场的总动能——但它在不同尺度之间扮演着能量搬运工的角色 。它将能量从被注入的**大尺度**（[能量尺度](@entry_id:196201)，特征长度为**积分尺度 (integral scale)** $L$）涡结构，通过一系列连续的、越来越小的涡，传递到**小尺度**。

这个传递过程并非没有尽头。当尺度变得足够小时，[速度梯度](@entry_id:261686)会变得非常剧烈，此时粘性效应开始变得重要。[粘性力](@entry_id:263294)通过**粘性耗散 (viscous dissipation)** 将动能不可逆地转化为内能（热量）。发生显著耗散的尺度被称为**柯尔莫哥洛夫尺度 (Kolmogorov scale)**，用 $\eta$ 表示 。在极高雷诺数下，能量注入的积分尺度 $L$ 与耗散发生的柯尔莫哥洛夫尺度 $\eta$ 之间存在巨大的[尺度分离](@entry_id:270204)，其关系为 $L/\eta \sim Re^{3/4}$。

在这两个极限尺度之间，存在一个广阔的中间尺度范围，被称为**[惯性子区](@entry_id:273327) (inertial subrange)**。柯尔莫哥洛夫假设，在这个区域内，涡的动力学既不受大尺度能量注入的具体方式影响，也几乎不受小尺度粘性耗散的影响。它们唯一的任务就是将能量以一个恒定的通量从大尺度传递到小尺度。在统计定常态下，这个**能量通量 (energy flux)** $\Pi$ 必须等于单位质量的平均能量[耗散率](@entry_id:748577) $\varepsilon$ [@problem_id:4001702, @problem_id:4001709]。因此，[惯性子区](@entry_id:273327)的核心特征就是一个近似恒定的、从大尺度流向小尺度的能量通量 $\Pi(k) \approx \varepsilon$，其中 $k$ 是波数。这个清晰的图像——能量在大尺度注入，在[惯性区](@entry_id:1126481)传递，在小尺度耗散——构成了我们理解[湍流](@entry_id:151300)能量动力学的基础 。

### 串级的物理机制：涡拉伸

[能量串级](@entry_id:153717)从大尺度到小尺度的传递过程，其背后的核心物理机制是三维流体运动中独有的**涡拉伸 (vortex stretching)** 现象。为了理解这一点，我们需要考察**[涡量](@entry_id:142747) (vorticity)** $\boldsymbol{\omega} = \nabla \times \boldsymbol{u}$ 的演化。对[不可压缩纳维-斯托克斯](@entry_id:750595)方程两边取旋度，可以得到[涡量输运方程](@entry_id:139098) ：
$$
\frac{D\boldsymbol{\omega}}{Dt} = \frac{\partial \boldsymbol{\omega}}{\partial t} + (\boldsymbol{u} \cdot \nabla)\boldsymbol{\omega} = (\boldsymbol{\omega} \cdot \nabla)\boldsymbol{u} + \nu \nabla^2 \boldsymbol{\omega}
$$
其中 $D/Dt$ 是[物质导数](@entry_id:262900)。右侧第一项 $(\boldsymbol{\omega} \cdot \nabla)\boldsymbol{u}$ 就是涡拉伸项。它描述了速度场沿[涡量](@entry_id:142747)方向的变化率如何改变[涡量矢量](@entry_id:187667)。

涡拉伸项的物理意义可以类比于[角动量守恒](@entry_id:156798)。想象一个流体微元，如果它沿着[涡量矢量](@entry_id:187667) $\boldsymbol{\omega}$ 的方向被拉伸，它的“半径”就会减小。为了保持角动量，它的旋转速度（即[涡量](@entry_id:142747)）就必须增加。反之，如果它被压缩，[涡量](@entry_id:142747)就会减弱。更精确地，[涡量](@entry_id:142747)大小 $|\boldsymbol{\omega}|$ 的平方（即**拟能 (enstrophy)** 的两倍）的变化率由下式决定：
$$
\frac{D |\boldsymbol{\omega}|^2}{Dt} = 2 \boldsymbol{\omega} \cdot [(\boldsymbol{\omega} \cdot \nabla)\boldsymbol{u}] + \dots = 2 \omega_i S_{ij} \omega_j + \dots
$$
其中 $S_{ij} = \frac{1}{2}(\partial_j u_i + \partial_i u_j)$ 是**[应变率张量](@entry_id:266108) (rate-of-strain tensor)** 。这表明，[涡量](@entry_id:142747)的增长或衰减取决于[涡量矢量](@entry_id:187667) $\boldsymbol{\omega}$ 与局部应变场[主轴](@entry_id:172691)的相对取向。当[涡量矢量](@entry_id:187667)与[应变率张量](@entry_id:266108)的拉伸方向（正特征值对应的[特征向量](@entry_id:151813)方向）对齐时，涡量被放大；当它与压缩方向对齐时，涡量被减弱。在三维[湍流](@entry_id:151300)中，[涡量](@entry_id:142747)倾向于与拉伸方向对齐，导致净的拟能产生。

涡拉伸正是连接大尺度和小尺度的桥梁。一个大涡被周围的速度场不均匀地拉伸，其涡量得到加强，同时其特征尺度变小，从而分裂成更小的、旋转更快的涡。这个过程不断重复，就构成了从大到小的[能量串级](@entry_id:153717)。

### 二维与三维[湍流](@entry_id:151300)中的双重串级

涡拉伸机制的存在与否，是区分三维[湍流](@entry_id:151300)和[二维湍流](@entry_id:198015)动力学的关键。在严格的[二维流](@entry_id:266853)中，速度场为 $\boldsymbol{u} = (u_x(x,y,t), u_y(x,y,t), 0)$，[涡量矢量](@entry_id:187667)只有z分量 $\boldsymbol{\omega} = (0, 0, \omega_z(x,y,t))$，处处垂直于流动平面。因此，涡拉伸项 $(\boldsymbol{\omega} \cdot \nabla)\boldsymbol{u} = \omega_z \frac{\partial \boldsymbol{u}}{\partial z}$ 恒等于零，因为速度场不依赖于 $z$ [@problem_id:4001731, @problem_id:4001654]。

涡拉伸的缺失导致了根本性的动力学差异。在三维[湍流](@entry_id:151300)中，能量是唯一的二次不变量（在无粘、无外力极限下），而拟能不守恒。这使得能量可以无障碍地通过涡拉伸向小尺度串级，形成**正向[能量串级](@entry_id:153717) (forward energy cascade)** 。

而在[二维湍流](@entry_id:198015)中，由于涡拉伸项为零，不仅能量 $E$ 守恒，拟能 $Z = \frac{1}{2}\int |\boldsymbol{\omega}|^2 dV$ 也成为第二个二次[守恒量](@entry_id:161475)。这种**双重守恒 (dual conservation)** 约束对能量传递施加了强大的限制。罗伯特·克莱奇南 (Robert Kraichnan) 指出，系统无法同时将能量和拟能都向小尺度传递。其结果是，[二维湍流](@entry_id:198015)展现出一种奇特的**双重串级 (dual cascade)** 现象：能量被注入后，大部分会向大尺度（低波数）传递，形成更大的涡结构，这被称为**逆向[能量串级](@entry_id:153717) (inverse energy cascade)**；而拟能则向小尺度（高波数）传递，并最终被粘性耗散，这被称为**正向拟能串级 (forward enstrophy cascade)** 。这一差异在地球物理流体（如大气和海洋的大尺度运动）中具有至关重要的意义。

### 柯尔莫哥洛夫相似性假设（K41理论）

1941年，柯尔莫哥洛夫提出了两个革命性的相似性假设，为[湍流](@entry_id:151300)的统计规律奠定了定量基础。这些假设主要针对高雷诺数下、尺度远小于积分尺度的[湍流](@entry_id:151300)运动。

**第一相似性假设** 关注的是最小的、受粘性影响的尺度，即所谓的**耗散区 (dissipation range)**。该假设指出：在足够高的雷诺数下，[湍流](@entry_id:151300)足够小尺度的统计特性具有普适性，并且仅由[平均能量](@entry_id:145892)耗散率 $\varepsilon$ 和运动粘度 $\nu$ 决定 。这里的普适性是基于**局部各向同性 (local isotropy)** 的思想，即尽管大尺度流动可能因边界条件而是各向异性的（如飞机尾迹），但经过多次涡破碎和拉伸后，小尺度的涡会“忘记”大尺度的方向信息，变得统计上各向同性。

基于这个假设，通过[量纲分析](@entry_id:140259)，我们可以构建出一套只依赖于 $\varepsilon$ 和 $\nu$ 的特征尺度，即**柯尔莫哥洛夫尺度**：
*   长度尺度: $\eta = (\nu^3 / \varepsilon)^{1/4}$
*   时间尺度: $\tau_\eta = (\nu / \varepsilon)^{1/2}$
*   速度尺度: $u_\eta = (\nu \varepsilon)^{1/4}$

第一假设预言，如果我们用这些柯尔莫哥洛夫尺度来[无量纲化](@entry_id:136704)任何小尺度统计量（如能谱、[结构函数](@entry_id:161908)），那么得到的无量纲函数将是普适的，不依赖于具体流动的大尺度细节 。

**第二相似性假设** 针对的是**[惯性子区](@entry_id:273327)**，即尺度 $r$ 满足 $\eta \ll r \ll L$ 的范围。该假设指出：在尺度 $r$ 属于[惯性子区](@entry_id:273327)时，[湍流](@entry_id:151300)的统计特性仅由平均能量[耗散率](@entry_id:748577) $\varepsilon$ 和尺度 $r$ 本身决定，而与粘度 $\nu$ 无关 。其物理基础是，在这个尺度范围内，能量传递起主导作用，而[粘性耗散](@entry_id:143708)可以忽略不计。

同样运用量纲分析，我们可以从该假设中推导出[湍流理论](@entry_id:264896)中最著名的一些结果。例如，对于二阶纵向**[结构函数](@entry_id:161908) (structure function)** $S_2(r) = \langle (\delta u_L(r))^2 \rangle$，其中 $\delta u_L(r)$ 是沿分离方向 $r$ 的[速度增量](@entry_id:176263)，我们有：
$$
S_2(r) = C_2 (\varepsilon r)^{2/3}
$$
对于三维[能量谱密度](@entry_id:270564) $E(k)$，其中 $k$ 是波数，我们得到：
$$
E(k) = C_K \varepsilon^{2/3} k^{-5/3}
$$
这就是著名的**柯尔莫哥洛夫-5/3定律**。其中 $C_2$ 和 $C_K$ 是普适的无量纲常数。这些[标度律](@entry_id:266186)在无数的实验和[计算流体动力学](@entry_id:142614)（CFD）模拟中得到了验证，是分析和建模[湍流](@entry_id:151300)的基本工具 。

### 超越K41：间歇性现象

尽管柯尔莫哥洛夫的K41理论取得了巨大成功，但后续更精确的测量揭示了与理论预测的系统性偏差，尤其是在[高阶统计量](@entry_id:193349)上。这种偏差的根源被称为**[间歇性](@entry_id:275330) (intermittency)** 。

K41理论隐含地假设了[能量耗散](@entry_id:147406)在空间中是均匀分布的，或者说能量串级是“空间填充”的。然而，实验和[数值模拟](@entry_id:146043)表明，真实的能量耗散 $\epsilon(\boldsymbol{x},t)$ 具有高度不均匀的、**[阵发性](@entry_id:275330) (bursty)** 的时空分布。耗散主要集中在一些非常小的、呈片状或线状的区域内，而广阔的流体区域内耗散则非常微弱。

这种间歇性在统计上有清晰的体现 ：
1.  **[速度增量](@entry_id:176263)的[非高斯性](@entry_id:158327)**：随着尺度 $r$ 的减小，[速度增量](@entry_id:176263) $\delta u_r$ 的[概率密度函数](@entry_id:140610)（PDF）会变得越来越偏离高斯分布。其特征是出现“[重尾](@entry_id:274276)”，意味着极端事件（非常大的速度差）的发生概率远高于高斯分布的预测。
2.  **标度无关性的破坏**：归一化的统计矩不再是常数。例如，**平坦度 (flatness)** $F(r) = S_4(r)/[S_2(r)]^2$ 会随着 $r$ 的减小而显著增大，偏离高斯值的3。这直接反映了小尺度下极端事件的日益重要。
3.  **反常[标度律](@entry_id:266186) (Anomalous scaling)**：[结构函数](@entry_id:161908)的[标度指数](@entry_id:188212) $\zeta_p$（定义为 $S_p(r) \sim r^{\zeta_p}$）不再满足K41的预测 $\zeta_p = p/3$，而是 $p$ 的一个[非线性](@entry_id:637147)[凹函数](@entry_id:274100)。

一个有趣且深刻的事实是，即使存在[间歇性](@entry_id:275330)，三阶[结构函数](@entry_id:161908)的[标度律](@entry_id:266186) $S_3(r) = -\frac{4}{5}\varepsilon r$ （即 $\zeta_3 = 1$）被认为是精确成立的。这是因为它直接与守恒的[平均能量](@entry_id:145892)通量相关，而间歇性主要影响的是[能量通量](@entry_id:266056)的涨落 。

为了解释[间歇性](@entry_id:275330)，人们发展了**乘法串级 (multiplicative cascade)** 等模型。这些模型认为，在能量从大涡传递到小涡的每一步中，[能量通量](@entry_id:266056)不是均匀分配的，而是乘以一个随机因子。经过多级串联，这种[乘法过程](@entry_id:173623)自然会导致[能量耗散](@entry_id:147406)的高度集中和不均匀分布，从而再现了观测到的反常[标度律](@entry_id:266186)。

总之，[湍流](@entry_id:151300)的物理图像是分层的：在大尺度上，能量通过平均流剪切等机制注入；在[惯性子区](@entry_id:273327)，能量通过三维涡拉伸机制，以近似恒定的通量向小尺度传递，并遵循柯尔莫哥洛夫的[标度律](@entry_id:266186)；在耗散区，能量最终被粘性转化为热。而贯穿整个过程的间歇性现象，则为这一经典图像增添了更为丰富和复杂的细节。