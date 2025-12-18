## 引言
在我们的日常经验中，[牛顿运动定律](@entry_id:163846)似乎是普适的。然而，当我们试图精确描述地球大气和海洋这样的大尺度流体运动时，一个根本性的复杂性出现了：我们赖以观测和建模的参考系——地球本身——是一个在不断旋转的[非惯性系](@entry_id:168746)。直接在此参考系中应用[牛顿定律](@entry_id:163541)将导致与观测不符的错误结果。为了解决这一难题，我们必须引入一系列“虚拟”的力，即视示力，以修正我们的动力学方程。本文旨在系统地揭示这些视示力的本质，并阐明它们在塑造地球天气与气候过程中的核心作用。

本文将引导读者完成一次从理论推导到实际应用的完整学习旅程。在“原理与机制”一章中，我们将从第一性原理出发，通过严谨的数学变换，推导出科里奥利力、离心力等视示力的表达式，并剖析其物理特性。接着，在“应用与跨学科联系”一章中，我们将探索这些理论概念如何在真实世界中显现，从解释地转风和[行星波](@entry_id:195650)等宏观现象，到阐明位涡守恒这一强大工具，并最终揭示它们如何对数值模型的构建提出根本性要求。最后，“动手实践”部分将提供具体的计算和分析问题，帮助读者巩固理解，将理论知识转化为解决实际问题的能力。通过这三章的学习，你将对[旋转参考系](@entry_id:174154)下的动力学建立起一个深刻而全面的认识。

## 原理与机制

在[数值天气预报](@entry_id:191656)和气候模型中，我们描述流体运动所使用的参考系是固定在地球上的，而地球本身在不断旋转。因此，这个参考系是一个[非惯性参考系](@entry_id:169712)。为了在这样的[旋转参考系](@entry_id:174154)中正确应用[牛顿运动定律](@entry_id:163846)，我们必须引入一系列“视示力”（apparent forces）。本章将系统地阐述这些力的基本原理、数学形式及其在地球物理流体动力学中的关键作用。

### 速度与加速度的变换

为了理解视示力的起源，我们首先需要建立[惯性参考系](@entry_id:276742)（由下标 $I$ 表示）和旋转参考系（由下标 $R$ 表示）中运动学量之间的变换关系。考虑一个以恒定[角速度](@entry_id:192539) $\boldsymbol{\Omega}$ 相对于[惯性系](@entry_id:266190)旋转的参考系。

对于任意矢量 $\mathbf{A}$，其在[惯性系](@entry_id:266190)中的时间变化率 $(d\mathbf{A}/dt)_I$ 和在旋转系中的时间变化率 $(d\mathbf{A}/dt)_R$ 之间存在一个普适的变换关系，即**[输运定理](@entry_id:176504)**（transport theorem）：
$$
\left(\frac{d\mathbf{A}}{dt}\right)_I = \left(\frac{d\mathbf{A}}{dt}\right)_R + \boldsymbol{\Omega} \times \mathbf{A}
$$
该公式的第二项 $\boldsymbol{\Omega} \times \mathbf{A}$ 源于[旋转参考系](@entry_id:174154)[基矢](@entry_id:199546)量的变化率。从[惯性系](@entry_id:266190)看，旋转系的基矢量在不断改变方向，这一变化率贡献了额外的速度分量。

现在，我们将这个定理应用于流体质点的位置矢量 $\mathbf{r}$。在[惯性系](@entry_id:266190)中观测到的速度，即**绝对速度** $\mathbf{U}$，定义为 $(d\mathbf{r}/dt)_I$。在旋转系中观测到的速度，即**[相对速度](@entry_id:178060)** $\mathbf{u}$，定义为 $(d\mathbf{r}/dt)_R$。将 $\mathbf{r}$ 代入[输运定理](@entry_id:176504)，我们直接得到绝对速度和相对速度之间的关系：
$$
\mathbf{U} = \mathbf{u} + \boldsymbol{\Omega} \times \mathbf{r}
$$
这里的 $\boldsymbol{\Omega} \times \mathbf{r}$ 项具有明确的物理意义：它代表了在旋转系中与质点位置 $\mathbf{r}$ 固连的那个点的速度。换言之，这是由于参考系本身的[刚体](@entry_id:1131033)旋转所产生的牵连速度。

接下来，我们对速度关系式再次求导，以获得加速度之间的变换。[惯性系](@entry_id:266190)中的加速度 $\mathbf{a}_I$ 是绝对速度 $\mathbf{U}$ 在[惯性系](@entry_id:266190)中的时间导数。我们将[输运定理](@entry_id:176504)应用于绝对速度 $\mathbf{U}$：
$$
\mathbf{a}_I = \left(\frac{d\mathbf{U}}{dt}\right)_I = \left(\frac{d(\mathbf{u} + \boldsymbol{\Omega} \times \mathbf{r})}{dt}\right)_I
$$
为了在旋转系中表达这个加速度，我们再次使用[输运定理](@entry_id:176504)：
$$
\mathbf{a}_I = \left(\frac{d(\mathbf{u} + \boldsymbol{\Omega} \times \mathbf{r})}{dt}\right)_R + \boldsymbol{\Omega} \times (\mathbf{u} + \boldsymbol{\Omega} \times \mathbf{r})
$$
在地球系统建模中，地球自转速率的变化极其缓慢，因此我们通常假设 $\boldsymbol{\Omega}$ 是一个常矢量。在这种情况下，对括号内的项求导得到：
$$
\left(\frac{d\mathbf{u}}{dt}\right)_R + \boldsymbol{\Omega} \times \left(\frac{d\mathbf{r}}{dt}\right)_R = \mathbf{a}_R + \boldsymbol{\Omega} \times \mathbf{u}
$$
其中 $\mathbf{a}_R = (d\mathbf{u}/dt)_R$ 是相对加速度。将此结果代回并展开，最终得到[绝对加速度](@entry_id:263735)和相对加速度之间的完整关系：
$$
\mathbf{a}_I = \mathbf{a}_R + 2(\boldsymbol{\Omega} \times \mathbf{u}) + \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})
$$
这个关系式是连接[惯性系](@entry_id:266190)与旋转系动力学的桥梁。右边的后两项并非真实的加速度，而是由于参考系旋转而产生的视示加速度。

### [运动方程](@entry_id:264286)中的视示力

牛顿第二定律必须在[惯性系](@entry_id:266190)中表述：$m\mathbf{a}_I = \sum \mathbf{F}_{\text{real}}$，其中 $\sum \mathbf{F}_{\text{real}}$ 是作用在质量为 $m$ 的流体[质点](@entry_id:186768)上的所有**真实力**（real forces）之和，例如[引力](@entry_id:189550)、压力[梯度力](@entry_id:166847)、粘性力等。这些真实力不依赖于观测者所在的参考系。

为了得到在旋转系中的[运动方程](@entry_id:264286)，我们将加[速度变换](@entry_id:265594)关系代入牛顿第二定律，并整理得到相对加速度 $\mathbf{a}_R$ 的表达式：
$$
m\mathbf{a}_R = \sum \mathbf{F}_{\text{real}} - 2m(\boldsymbol{\Omega} \times \mathbf{u}) - m[\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})]
$$
方程右边的后两项被称为**视示力**（apparent forces）。它们不是真实存在的相互作用，而是为了使[牛顿定律](@entry_id:163541)在[非惯性系](@entry_id:168746)中保持形式上的有效性而引入的修正项。与在所有[惯性系](@entry_id:266190)之间形式不变（协变）的真实力不同，视示力仅在[加速参考系](@entry_id:168026)中出现，它们是坐标系本身运动的体现。

我们逐一检视这些视示力：

*   **科里奥利力（Coriolis force）**：$\mathbf{F}_{\text{Coriolis}} = -2m(\boldsymbol{\Omega} \times \mathbf{u})$。这是最重要的视示力之一，具有以下关键特性：
    *   它只作用于在旋转系中运动的物体（即 $\mathbf{u} \neq \mathbf{0}$）。
    *   它的方向始终垂直于物体的相对速度 $\mathbf{u}$ 和旋转矢量 $\boldsymbol{\Omega}$。
    *   由于力与速度垂直，科里奥利力对物体**不做功**（$\mathbf{F}_{\text{Coriolis}} \cdot \mathbf{u} = 0$），因此它只改变物体运动的方向，而不改变其动能。在北半球，它使运动物体向右偏转；在南半球，向左偏转。

*   **[离心力](@entry_id:173726)（Centrifugal force）**：$\mathbf{F}_{\text{centrifugal}} = -m[\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})]$。该力具有以下特性：
    *   它仅取决于物体在旋转系中的位置 $\mathbf{r}$，而与物体的运动状态无关。
    *   它的方向总是垂直于[并指](@entry_id:276731)向远离旋转轴的方向。

在某些极特殊的情况下，地球的自转速率 $\boldsymbol{\Omega}$ 可能会随时间变化，例如由于天文力矩或地球内部质量的重新分布。在这种情况下，加[速度变换](@entry_id:265594)会多出一项，从而引入第三个视示力：

*   **[欧拉力](@entry_id:173795)（Euler force）**：$\mathbf{F}_{\text{Euler}} = -m(\dot{\boldsymbol{\Omega}} \times \mathbf{r})$，其中 $\dot{\boldsymbol{\Omega}} = d\boldsymbol{\Omega}/dt$。此力与参考系[角速度](@entry_id:192539)的时间变化率成正比。

### 地球物理流体动力学中的简化与应用

在模拟地球大气和海洋时，上述普适原理会被进一步简化和应用，以适应地球系统的特定条件。

#### 有效重力与位势

对于地球而言，离心力是一个不随时间变化、仅与地理位置（即 $\mathbf{r}$）相关的[力场](@entry_id:147325)。因此，将离心力与万有引力（一个真实的力）合并处理会非常方便。我们定义**有效重力**（effective gravity）$\mathbf{g}_{\text{eff}}$ 为真实[引力](@entry_id:189550) $\mathbf{g}_{\text{true}}$ 和单位质量离心力的矢量和：
$$
\mathbf{g}_{\text{eff}} = \mathbf{g}_{\text{true}} - \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})
$$
由于真实[引力](@entry_id:189550)和离心力都是[保守力场](@entry_id:164320)（其旋度为零），它们的和——有效重力——也是一个[保守场](@entry_id:137555)。因此，我们可以定义一个标量场，称为**位势**（geopotential）$\Phi$，使其梯度等于负的有效重力：
$$
\mathbf{g}_{\text{eff}} = -\nabla\Phi
$$
位势 $\Phi$ 是单位质量的势能，它包括了[引力势能](@entry_id:269038)和[离心势](@entry_id:172447)能。地球的平均海平面被定义为一个等位势面，称为**大地水准面**（geoid）。引入位势后，单位质量的水平动量方程可以写得更简洁：
$$
\frac{D\mathbf{u}_h}{Dt} = -2(\boldsymbol{\Omega} \times \mathbf{u})_h - \frac{1}{\rho}\nabla_h p
$$
其中下标 $h$ 表示水平分量。在静止的、无粘性的大气中（$\mathbf{u}=\mathbf{0}$），该方程简化为 $\nabla p = \rho \mathbf{g}_{\text{eff}}$，这意味着压力梯度与有效重力方向相反，等压面与等位势面重合。对于大尺度运动，垂直方向的[动量方程](@entry_id:197225)通常简化为**[静力平衡](@entry_id:163498)**（hydrostatic balance），即[垂直压力梯度](@entry_id:1133794)力与有效重[力平衡](@entry_id:267186)：
$$
\frac{\partial p}{\partial z} = -\rho g_{\text{eff}}
$$
其中 $g_{\text{eff}} = |\mathbf{g}_{\text{eff}}|$。结合位势的定义 $\partial\Phi/\partial z = g_{\text{eff}}$，我们可以推导出在以气压 $p$ 为垂直坐标的坐标系中，[静力平衡](@entry_id:163498)方程有一个极其简洁的形式：
$$
\frac{\partial\Phi}{\partial p} = -\frac{1}{\rho} = -\alpha
$$
其中 $\alpha$ 是比容。这个关系式是[大气动力学](@entry_id:746558)和数值模型中的基石，它优雅地将旋转效应隐含在了位[势场](@entry_id:143025) $\Phi$ 的定义中。

#### 科里奥利力在局地坐标系下的形式与[传统近似](@entry_id:1133287)

为了在模型中使用科里奥利力，需要将其在局地坐标系（如东、北、上方向）中分解。在地理纬度为 $\phi$ 的位置，地球自转矢量 $\boldsymbol{\Omega}$ 可以分解为沿当地垂直方向（向上）的分量 $\Omega_v = \Omega\sin\phi$ 和沿当地水平方向（向北）的分量 $\Omega_h = \Omega\cos\phi$。

将 $\boldsymbol{\Omega} = \Omega_h \hat{\mathbf{j}} + \Omega_v \hat{\mathbf{k}}$（其中 $\hat{\mathbf{j}}$ 指向北，$\hat{\mathbf{k}}$ 指向上）和速度矢量 $\mathbf{u} = u\hat{\mathbf{i}} + v\hat{\mathbf{j}} + w\hat{\mathbf{k}}$ 代入[科里奥利加速度](@entry_id:171639) $-2(\boldsymbol{\Omega} \times \mathbf{u})$ 的表达式，我们得到其在东（$x$）、北（$y$）、上（$z$）三个方向上的完整分量：
$$
\begin{align}
a_x & = 2\Omega(v\sin\phi - w\cos\phi) \\
a_y & = -2\Omega u\sin\phi \\
a_z & = 2\Omega u\cos\phi
\end{align}
$$
其中，包含 $\cos\phi$ 的项（即 $-2\Omega w\cos\phi$ 和 $2\Omega u\cos\phi$）源于 $\boldsymbol{\Omega}$ 的水平分量，它们被称为**[非传统科里奥利项](@entry_id:1128830)**。

对于大尺度天气系统，其水平尺度 $L$ 远大于垂直尺度 $H$（即 $H/L \ll 1$），并且垂直速度 $w$ 通常远小于水平速度 $U$。基于标度分析，我们可以做出**[传统近似](@entry_id:1133287)**（traditional approximation），即在计算科里奥利力时忽略地球自转矢量的水平分量（$\Omega_h$）。这相当于令 $\boldsymbol{\Omega} \approx \Omega\sin\phi \hat{\mathbf{k}}$。在此近似下，[科里奥利加速度](@entry_id:171639)的分量简化为：
$$
\begin{align}
a_x & \approx 2\Omega v\sin\phi = fv \\
a_y & \approx -2\Omega u\sin\phi = -fu \\
a_z & \approx 0
\end{align}
$$
这里 $f = 2\Omega\sin\phi$ 是著名的**[科里奥利参数](@entry_id:1123077)**。这种简化是否合理，取决于被忽略的非传统项与保留的传统项的相对大小。例如，在水平动量方程中，我们需要比较 $|-2\Omega w \cos\phi|$ 和 $|2\Omega v \sin\phi|$。对于特征速度为 $W$ 和 $U$ 的运动，该条件简化为 $W/U \ll |\tan\phi|$。利用[连续性方程](@entry_id:195013) $W/U \sim H/L$，最终的判据为 $(H/L)\cot\phi \ll 1$。对于中纬度的天气尺度运动（$H/L \sim 10^{-2}, \cot\phi \sim 1$），此条件很好地满足。然而，在赤道附近（$\phi \to 0, \cot\phi \to \infty$）或在垂直运动强烈的深对流系统（$W \sim U$）中，[传统近似](@entry_id:1133287)会失效。在最简单的教学模型中，有时会假设 $\boldsymbol{\Omega}$ 完全垂直于局地水平面，此时[科里奥利加速度](@entry_id:171639)的垂直分量为零，不直接影响[静力平衡](@entry_id:163498)。

#### [欧拉力](@entry_id:173795)的可忽略性

现在我们回到[欧拉力](@entry_id:173795) $\mathbf{F}_{\text{Euler}} = -m(\dot{\boldsymbol{\Omega}} \times \mathbf{r})$。地球的自转速率 $\boldsymbol{\Omega}$ 确实存在微小的变化，例如由于潮汐摩擦导致的日长变化、钱德勒摆动等。然而，这些变化的速率 $\dot{\boldsymbol{\Omega}}$ 极其微小。根据观测，$\boldsymbol{\Omega}$ 的相对变化 $\epsilon$ 在 $10^{-8}$ 到 $10^{-6}$ 的量级，而发生这些变化的时间尺度 $T$ 至少是天到年的量级（$10^5$ 至 $10^7$ 秒）。通过[标度分析](@entry_id:153681)可以估算出，在地球系统条件下，欧拉加速度的大小（$|\dot{\boldsymbol{\Omega}}||\mathbf{r}|$）比[科里奥利加速度](@entry_id:171639)（$2|\boldsymbol{\Omega}||\mathbf{u}|$）和离心加速度（$|\boldsymbol{\Omega}|^2|\mathbf{r}|$）要小好几个数量级。因此，在几乎所有的[数值天气预报](@entry_id:191656)和气候模型中，[欧拉力](@entry_id:173795)都可以被安全地忽略。

### 旋转效应在大气与[海洋动力学](@entry_id:1129055)中的体现

理论上的视示力在真实的大气和海洋中表现为一系列丰富而关键的动力学现象。

#### 平衡流

对于大尺度运动，[罗斯贝数](@entry_id:143106)（Rossby number）$\mathrm{Ro} = U/(fL)$ 通常很小（$\ll 1$），这意味着流体的加速度远小于科里奥利力和压力[梯度力](@entry_id:166847)。在这种情况下，流动趋向于一种平衡状态。

*   **地转平衡（Geostrophic Balance）**：这是最基本和最重要的[平衡态](@entry_id:270364)，即水平压力[梯度力](@entry_id:166847)与科里奥利力达到平衡：
    $$
    - \frac{1}{\rho}\nabla_h p = f\hat{\mathbf{k}} \times \mathbf{u}_g
    $$
    其中 $\mathbf{u}_g$ 是**地转风**。地转风沿等压线吹（与压力梯度垂直），在北半球，低压位于其前进方向的左侧（这被称为白贝罗定律，Buys Ballot's law）。

*   **[梯度风平衡](@entry_id:1125721)（Gradient Wind Balance）**：当气流存在曲率时（例如在[气旋](@entry_id:262310)或反气旋中），需要考虑[向心加速度](@entry_id:190458)。[梯度风平衡](@entry_id:1125721)是压力[梯度力](@entry_id:166847)、科里奥利力和[向心力](@entry_id:166628)三者之间的平衡。它解释了为什么在北半球，[气旋](@entry_id:262310)性（绕低压）曲率中的风速通常小于[地转风](@entry_id:271692)（亚地转），而反[气旋](@entry_id:262310)性（绕高压）曲率中的风速可以大于[地转风](@entry_id:271692)（超地转）。对于曲率过大的强反气旋，可能不存在稳定的[梯度风平衡](@entry_id:1125721)解。

*   **准地转平衡（Quasigeostrophic Balance）**：这是一个更高阶的平衡理论，描述了流动如何围绕地转[平衡态](@entry_id:270364)缓慢演变。它考虑了由地转风平流自身（即加速度）产生的微小非地转分量，这些分量对于驱动垂直运动和天气系统的发展至关重要。

#### 惯性振荡

如果一个流体质点受到的压力[梯度力](@entry_id:166847)突然消失（例如，在海洋中，一次强风事件过后，风应力驱动的海水[表面压](@entry_id:152856)力梯度迅速减弱），在没有摩擦的情况下，它将在科里奥利力的唯一作用下运动。此时的水平动量方程为：
$$
\frac{du}{dt} = fv, \quad \frac{dv}{dt} = -fu
$$
这个方程组的解描述了一种[匀速圆周运动](@entry_id:178264)，其[角频率](@entry_id:261565)为 $|f|$，周期为 $T = 2\pi/|f|$，被称为**惯性周期**。这种运动称为**惯性振荡**（inertial oscillations）。其运动半径为 $R=U_0/|f|$，其中 $U_0$ 是初始速度。在海洋上层，由风暴激发的近惯性流是一种非常普遍的现象，可以通过卫星跟踪的漂流浮标观测到清晰的环状轨迹。在分层海洋中，这些振荡的能量还可以作为近惯性内波向下传播。在北半球，惯性振荡的旋转方向是顺时针的。

#### [行星波](@entry_id:195650)（[罗斯贝波](@entry_id:195650)）

到目前为止，我们大多假设科里奥利参数 $f$ 是常数（$f$ 平面近似）。然而，$f=2\Omega\sin\phi$ 随纬度 $\phi$ 变化。为了研究这种变化的首要影响，我们采用 $\beta$ 平面近似，即令 $f = f_0 + \beta y$，其中 $\beta = \partial f / \partial y$ 在中纬度是一个正的常数。

对于无辐散的二维流动，一个关键的[守恒量](@entry_id:161475)是**绝对涡度** $\eta = \zeta + f$，其中 $\zeta$ 是相对涡度（气流自身的旋转），$f$ 是行星涡度（由地球自转产生）。[绝对涡度](@entry_id:262794)守恒（$D\eta/Dt=0$）意味着，如果一个流体[质点](@entry_id:186768)向北移动（$y$ 增加），它的行星涡度 $f$ 会增加，为了保持 $\eta$ 不变，它的相对涡度 $\zeta$ 必须减小（在北半球产生反[气旋](@entry_id:262310)式涡度）。反之亦然。

这种“涡度管”的拉伸和压缩提供了一种恢复机制，从而产生了**[行星波](@entry_id:195650)**或**[罗斯贝波](@entry_id:195650)**（Rossby waves）。这些波的一个显著特征是，相对于背景气流，它们的位相**本质上传播方向是向西的**。这个向西的传播速度由 $\beta$ 和波的尺度决定。当然，如果存在一个足够强的东风背景气流，观测到的波（例如天气图上的槽和脊）在地球参考系中仍然可能向东移动。[罗斯贝波](@entry_id:195650)是地球大气和海洋中大尺度环流和天气变化的最重要组成部分。