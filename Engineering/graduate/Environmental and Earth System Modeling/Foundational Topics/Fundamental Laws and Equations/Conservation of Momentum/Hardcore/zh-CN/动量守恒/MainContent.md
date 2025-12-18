## 引言
[动量守恒](@entry_id:149964)是物理学中最基本的守恒定律之一，对于理解和预测从行星尺度环流到局部环境流动的各类运动至关重要。它不仅支配着大气和海洋的宏观运动，也决定了雪崩、地下水流和污染物扩散等关键地球过程的动态行为。

然而，将这一普适原理应用于复杂多变的地球系统——一个充满旋转、分层、[湍流](@entry_id:151300)和多相相互作用的领域——构成了一个巨大的挑战。这不仅需要深刻的理论理解，还需要掌握将其转化为可靠数值模型的复杂技术。本文旨在系统性地跨越这一知识鸿沟，为读者构建一个从第一性原理到前沿应用的完整知识体系。

本文将分为三个核心章节。首先，在“原理与机制”一章中，我们将从连续介质力学的基础出发，逐步构建[动量守恒](@entry_id:149964)的数学框架，并探讨旋转、分层和[湍流](@entry_id:151300)等关键因素的影响。接着，在“应用与跨学科联系”一章中，我们将展示这些原理如何解释和模拟从[海洋环流](@entry_id:195237)到海冰漂移等广泛的地球物理现象，并揭示其与生态学、工程学等领域的深刻联系。最后，“动手实践”部分将提供具体的计算问题，帮助读者将理论知识应用于解决实际的建模挑战。我们的探索将从[动量守恒](@entry_id:149964)最核心的表述开始，深入其基本原理与机制。

## 原理与机制

本章深入探讨[动量守恒](@entry_id:149964)的基本原理及其在环境与地球系统建模中的具体机制。我们将从[连续介质力学](@entry_id:155125)的第一性原理出发，建立动量守恒的数学表述，并逐步引入旋转、分层、[湍流](@entry_id:151300)和[数值离散化](@entry_id:752782)等复杂情境，这些都是在真实[地球系统模型](@entry_id:1124096)中必须考虑的因素。

### 动量守恒的基本表述

[动量守恒](@entry_id:149964)是[牛顿第二定律](@entry_id:274217)在连续介质中的直接体现，它指出一个物质系统的总动量变化率等于作用在该系统上的外力之和。为了在环境流动建模中应用这一定律，我们首先需要精确定义动量及其在空间中的分布。

#### [动量密度](@entry_id:271360)与[总动量](@entry_id:173071)

在[连续介质力学](@entry_id:155125)中，我们将流体视为一个连续的场，而不是离散的粒子集合。因此，我们引入 **[动量密度](@entry_id:271360)（momentum density）** 的概念，它是一个在空间和时间上逐点定义的矢量场。对于一个密度为 $\rho(\mathbf{x}, t)$、速度为 $\mathbf{u}(\mathbf{x}, t)$ 的流体，其在点 $\mathbf{x}$ 和时间 $t$ 的线性[动量密度](@entry_id:271360)被定义为 $\rho\mathbf{u}$。这是一个 **[强度性质](@entry_id:181209)（intensive property）** 的场，意味着其在某一点的值不依赖于我们所考虑的区域大小。

与之相对，一个有限控制体积 $\Omega$ 内的 **[总动量](@entry_id:173071)（total momentum）** 是一个 **[广延性质](@entry_id:145410)（extensive property）**，它通过对[动量密度](@entry_id:271360)在该体积内进行积分得到：
$$
\mathbf{P}(t) = \int_{\Omega} \rho \mathbf{u} \, dV
$$
[总动量](@entry_id:173071) $\mathbf{P}(t)$ 的值显然依赖于控制体积 $\Omega$ 的大小和形状，以及时间 $t$。这两个概念——逐点定义的场量和积分得到的总量——之间的区别是理解[动量平衡](@entry_id:1128118)的关键。

#### [拉格朗日观点](@entry_id:1127015)：物质体积的[动量方程](@entry_id:197225)

描述物理定律最直接的方式是采用 **拉格朗日（Lagrangian）** 观点，即跟踪一个固定的流体团（称为 **物质体积**，material volume），它在运动过程中始终由相同的流体[质点](@entry_id:186768)组成。对于这样一个随流体运动和变形的物质体积 $\Omega(t)$，[牛顿第二定律](@entry_id:274217)可以直接应用。其[总动量](@entry_id:173071)的[物质导数](@entry_id:262900)（[随体导数](@entry_id:204621)）等于作用在该物质体积上的所有外力之和：
$$
\frac{D}{Dt} \int_{\Omega(t)} \rho \mathbf{u} \, dV = \sum \mathbf{F}_{\text{ext}}
$$
其中，$\frac{D}{Dt}$ 表示物质导数，$\sum \mathbf{F}_{\text{ext}}$ 包括作用于整个体积的 **彻体力（body forces）**（如重力）和作用于其表面的 **[表面力](@entry_id:188034)（surface forces）**（如压力和[粘性应力](@entry_id:261328)）。这个积分形式的方程是连续介质动量守恒最根本的陈述，它明确了 $\rho\mathbf{u}$ 作为[动量密度](@entry_id:271360)在积分中的核心地位。 

### [欧拉框架](@entry_id:749109)：输运与局部平衡

尽管拉格朗日观点在理论上很直观，但在[地球系统模型](@entry_id:1124096)中，我们通常在固定的空间网格上求解方程，这要求我们采用 **欧拉（Eulerian）** 观点。**[Reynolds输运定理](@entry_id:191217)（Reynolds Transport Theorem）** 是连接这两种观点的数学桥梁。

#### [Reynolds输运定理](@entry_id:191217)

[Reynolds输运定理](@entry_id:191217)描述了一个积分量的[物质导数](@entry_id:262900)如何与在一个可能移动和变形的控制体积内的量的变化率以及通过该控制体积边界的通量联系起来。对于动量这一矢量，其最广义的积分形式为：
$$
\frac{D}{Dt} \int_{\Omega_m(t)} \rho \mathbf{u} \, dV = \frac{d}{dt} \int_{\Omega_c(t)} \rho \mathbf{u} \, dV + \oint_{\partial \Omega_c(t)} \rho \mathbf{u} \left[ (\mathbf{u} - \mathbf{u}_{\text{CS}}) \cdot \mathbf{n} \right] \, dA
$$
这里，左侧是物质体积 $\Omega_m(t)$（即流体团）的总动量变化率。右侧则是从一个任意选定的、其边界面速度为 $\mathbf{u}_{\text{CS}}$ 的控制体积 $\Omega_c(t)$ 观察到的变化。第一项是控制体积内总动量的[瞬时变化率](@entry_id:141382)；第二项是穿过控制体积边界 $\partial \Omega_c(t)$ 的动量净通量，其中 $\mathbf{n}$ 是边界面的外[法线](@entry_id:167651)单位矢量。

这个通量项至关重要，它量化了由于流体相对于控制边界的运动而产生的动量交换。例如，在[海洋混合层](@entry_id:1129065)模型中，[混合层](@entry_id:926526)的底部界面 $z = -h(x, y, t)$ 是一个移动的边界。如果流体的垂向速度 $w$ 与界面本身的垂向速度 $w_i$ 不同，就会发生流体的 **卷入（entrainment）** 或 **卷出（detrainment）**。这种跨越[移动界面](@entry_id:141467)的质量交换会带来动量的输运，表现为通量项中依赖于相对速度 $(w - w_i)$ 的部分。而风应力或界面应力等[表面力](@entry_id:188034)则作为外力项 $\sum \mathbf{F}_{\text{ext}}$ 的一部分，它们是施加在边界上的力，与穿越边界的质量通量在物理上是截然不同的。

对于在固定欧拉网格上的模型，控制体积是固定的，因此 $\mathbf{u}_{\text{CS}} = \mathbf{0}$。此时，[动量方程的积分形式](@entry_id:750703)简化为：
$$
\sum \mathbf{F}_{\text{ext}} = \frac{d}{dt} \int_{\Omega} \rho \mathbf{u} \, dV + \oint_{\partial \Omega} \rho \mathbf{u} (\mathbf{u} \cdot \mathbf{n}) \, dA
$$
这个方程表明，[固定控制体](@entry_id:272149)积内动量的变化，不仅源于作用在体积上的外力，还源于通过其边界的动量 **平流（advection）**。

#### [通量形式](@entry_id:273811)与平流形式

通过应用高斯散度定理并将积分体积缩小至无穷小，我们可以从上述积分方程得到[动量守恒](@entry_id:149964)的微分形式。惯性项（即动量自身的变化）可以写成两种数学上等价但物理解释不同的形式。

第一种是 **[通量形式](@entry_id:273811)（flux form）** 或 **守恒形式（conservative form）**:
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \mathbf{u})
$$
这里，$\mathbf{u} \mathbf{u}$ 表示[速度矢量](@entry_id:269648)的[张量积](@entry_id:140694)（dyadic product），$\rho \mathbf{u} \mathbf{u}$ 是[动量通量](@entry_id:199796)张量。这种形式将[动量密度](@entry_id:271360)的[局部时](@entry_id:194383)间变化率与[动量通量](@entry_id:199796)的散度联系起来，清晰地表达了在一个固定点上的动量收支平衡。

第二种是 **平流形式（advective form）**:
$$
\rho \frac{D\mathbf{u}}{Dt} = \rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right)
$$
这种形式表示单位体积流体的质量乘以其加速度（即[物质导数](@entry_id:262900) $\frac{D\mathbf{u}}{Dt}$），直接对应于牛顿第二定律“质量乘以加速度”。

这两种形式的等价性，依赖于 **质量守恒定律（continuity equation）**，即 $\partial_t \rho + \nabla \cdot (\rho \mathbf{u}) = 0$。通过简单的[向量代数](@entry_id:152340)运算可以证明：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \mathbf{u}) = \rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) + \mathbf{u} \left( \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) \right) = \rho \frac{D\mathbf{u}}{Dt}
$$
在建模实践中，[通量形式](@entry_id:273811)是[有限体积法](@entry_id:141374)（Finite Volume Method）的首选，因为它能够自然地保证离散动量的守恒。而平流形式则更便于进行拉格朗日式的[轨迹分析](@entry_id:756092)和流体[质点](@entry_id:186768)受力分析。

### [动量方程](@entry_id:197225)中的力与能量

将惯性项与作用力项结合，我们就得到了完整的动量方程。

#### [Cauchy动量方程](@entry_id:187010)

在一个可压缩的[粘性流](@entry_id:136330)体中，作用于流体单元的力主要包括压力[梯度力](@entry_id:166847)、[粘性力](@entry_id:263294)以及像重力这样的彻[体力](@entry_id:174230)。总的[表面力](@entry_id:188034)可以通过 **Cauchy[应力张量](@entry_id:148973)（Cauchy stress tensor）** $\boldsymbol{\sigma}$ 来描述，它通常被分解为各向同性的压力[部分和](@entry_id:162077)[偏应力](@entry_id:163323)部分：$\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$，其中 $p$ 是压力，$I$ 是单位张量，$\boldsymbol{\tau}$ 是 **偏粘性应力张量（deviatoric viscous stress tensor）**。

将这些力代入并使用动量方程的通量形式，我们得到[守恒形式](@entry_id:1122899)的 **[Cauchy动量方程](@entry_id:187010)**：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \mathbf{u}) = -\nabla p + \nabla \cdot \boldsymbol{\tau} + \rho \mathbf{g}
$$
或者写成更紧凑的[通量形式](@entry_id:273811)，这在[可压缩流](@entry_id:747589)模型中非常常见：
$$
\frac{\partial (\rho \mathbf{u})}{\partial t} + \nabla \cdot (\rho \mathbf{u} \mathbf{u} + p\mathbf{I} - \boldsymbol{\tau}) = \rho \mathbf{g}
$$
这个方程是现代[地球系统模型](@entry_id:1124096)中流体动力学核心的基础。

#### 压力功在动能收支中的作用

压力在[动量方程](@entry_id:197225)中以[梯度力](@entry_id:166847) $(-\nabla p)$ 的形式出现，它驱动流动并重新分配动量。为了理解其在能量转化中的作用，我们可以通过将动量方程与速度场 $\mathbf{u}$ 做点积来推导动能方程。

经过一系列基于质量连续性方程的推导，压力梯度项的贡献 $\mathbf{u} \cdot (-\nabla p)$ 可以被分解为两部分：
$$
-\mathbf{u} \cdot \nabla p = -\nabla \cdot (p\mathbf{u}) + p(\nabla \cdot \mathbf{u})
$$
这揭示了压力的双重角色：
1.  **[能量通量](@entry_id:266056)输运（Energy Flux Transport）**：第一项 $-\nabla \cdot (p\mathbf{u})$ 是一个散度项，它代表了由压[力场](@entry_id:147325)做的机械功所引起的能量通量。这一项并不在局部产生或消耗动能，而是在空间上重新分配动能。
2.  **动能与内能的转换（Kinetic-Internal Energy Conversion）**：第二项 $p(\nabla \cdot \mathbf{u})$ 代表了体积变化所做的功。当流[体膨胀](@entry_id:144241)时（$\nabla \cdot \mathbf{u} > 0$），这一项为正，意味着内能被消耗并转化为动能；当流体被压缩时（$\nabla \cdot \mathbf{u}  0$），动能被消耗并转化为内能。这个过程是可逆的。

对于不可压缩流（如[Boussinesq近似](@entry_id:147239)下的海洋模型），运动学约束 $\nabla \cdot \mathbf{u} = 0$ 使得动能-内能转换项消失。在这种情况下，压力的作用简化为通过 $-\nabla \cdot (p\mathbf{u})$ 项在空间中瞬时地重新分配能量，以确保流场始终满足[无散度](@entry_id:190991)条件。

### 地球物理系统中的动量：旋转与分层

地球系统中的[大尺度流动](@entry_id:263652)受到行星旋转和稳定分层的强烈影响，这催生了独特的动力学机制。

#### 旋转参考系：视示力

由于地球的自转，[地球系统模型](@entry_id:1124096)通常建立在一个随行星旋转的[非惯性参考系](@entry_id:169712)中。从[惯性系](@entry_id:266190)转换到角速度为 $\boldsymbol{\Omega}$ 的旋转系，[牛顿第二定律](@entry_id:274217)中的[绝对加速度](@entry_id:263735) $\mathbf{a}_I$ 会转变为包含额外项的表达式。对任意矢量的时间导数在[惯性系](@entry_id:266190) $(d/dt)_I$ 和旋转系 $(d/dt)_R$ 之间有如下关系：$(d/dt)_I = (d/dt)_R + \boldsymbol{\Omega} \times$。

将此关系两次应用于位置矢量 $\mathbf{r}$，可以推导出[绝对加速度](@entry_id:263735) $\mathbf{a}_I$ 与旋转系中的相对加速度 $\mathbf{a}_R = D\mathbf{u}/Dt$ 之间的关系：
$$
\mathbf{a}_I = \frac{D\mathbf{u}}{Dt} + 2\boldsymbol{\Omega} \times \mathbf{u} + \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})
$$
（这里假设 $\boldsymbol{\Omega}$ 恒定）。因此，在旋转系中的[动量方程](@entry_id:197225)必须引入两个 **视示力（apparent forces）**：
1.  **科里奥利力（Coriolis Force）**：每单位质量为 $-2\boldsymbol{\Omega} \times \mathbf{u}$。这个力源于参考系的旋转，它只取决于流体在旋转系中的[相对速度](@entry_id:178060) $\mathbf{u}$。由于它总是与速度 $\mathbf{u}$ 垂直，所以科里奥利力对流体 **不做功**，不会改变其动能，仅改变其运动方向。
2.  **离心力（Centrifugal Force）**：每单位质量为 $-\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r})$。它指向外侧且垂直于旋转轴。在[地球系统模型](@entry_id:1124096)中，[离心力](@entry_id:173726)通常与[万有引力](@entry_id:157534)合并，定义为一个有效的重[力场](@entry_id:147325) $\mathbf{g}$。

最终，旋转系中的[动量方程](@entry_id:197225)（平流形式）为：
$$
\frac{D\mathbf{u}}{Dt} + 2\boldsymbol{\Omega} \times \mathbf{u} = -\frac{1}{\rho}\nabla p + \mathbf{g} + \text{粘性力}
$$
科里奥利力的出现是理解大尺度大气和[海洋环流](@entry_id:195237)（如气旋和反[气旋](@entry_id:262310)）的关键。

#### 大尺度流动的近似：地转平衡

对于地球上的天气尺度（synoptic-scale）等[大尺度流动](@entry_id:263652)，其特征是水平尺度 $L$ 远大于垂直尺度 $H$，且流速 $U$ 相对较慢。我们可以通过[尺度分析](@entry_id:1131264)来比较动量方程中各项的量级。描述惯性力与科里奥利力量级之比的[无量纲数](@entry_id:260863)是 **Rossby数（Rossby number）**，$Ro = U/(fL)$，其中 $f = 2\Omega \sin\phi$ 是局地科里奥利参数（$\phi$ 为纬度）。

在中纬度地区，对于 $L \sim 1000 \text{ km}$，$U \sim 10 \text{ m/s}$ 的流动，$Ro \approx 0.1 \ll 1$。这意味着加速度项 $\frac{D\mathbf{u}}{Dt}$ 比[科里奥利项](@entry_id:1123078) $f\hat{\mathbf{k}} \times \mathbf{u}_h$ 小一个数量级。在远离边界层的自由大气或海洋内部，粘性力也可以忽略。因此，水平方向的[动量方程](@entry_id:197225)在零阶近似下简化为一个简单的平衡关系：
$$
f \hat{\mathbf{k}} \times \mathbf{u}_g = -\frac{1}{\rho_0} \nabla_h p
$$
这被称为 **地转平衡（geostrophic balance）**，其中 $\mathbf{u}_g$ 是 **地转流（geostrophic flow）**，$\rho_0$ 是参考密度。地转平衡表明，在旋转效应占主导的[大尺度流动](@entry_id:263652)中，科里奥利力与水平压力[梯度力](@entry_id:166847)达到平衡。[地转流](@entry_id:1125618)的方向平行于等压线，而不是从高压流向低压。

地转平衡是地球物理流体动力学中最基本也是最有用的概念之一。它与垂直方向的 **[静力平衡](@entry_id:163498)（hydrostatic balance）** ($\partial p / \partial z = -\rho g$) 共同构成了 **[原始方程](@entry_id:1130162)（primitive equations）** 的基础。这两个平衡关系结合起来，可以导出 **[热成风关系](@entry_id:192206)（thermal wind relation）**，它将地转流的[垂直切变](@entry_id:1133795)与流体的水平密度（或温度）梯度联系起来。

更进一步，基于地转平衡的 **准地转（Quasi-Geostrophic, QG）理论**，考虑了由 Rossby 数 $Ro$ 所表征的微小非地转效应。正是这些微小的非地转辐合辐散驱动了天气系统的发展和演化。

#### 高阶守恒律：位涡

除了动量本身，由动量、质量和[热力学](@entry_id:172368)方程组合可以导出更强大的[守恒量](@entry_id:161475)。其中最重要的是 **位涡（Potential Vorticity, PV）**。对于一个无粘、绝热的理想流体，**[Ertel位涡](@entry_id:1124655)** 定义为：
$$
q = \frac{\boldsymbol{\omega}_a \cdot \nabla \theta}{\rho}
$$
其中 $\boldsymbol{\omega}_a = \nabla \times \mathbf{u} + 2\boldsymbol{\Omega}$ 是绝对涡度，$\theta$ 是位温（或其他物质[守恒量](@entry_id:161475)）。在无摩擦、无热量交换（即绝热）的条件下，位涡是一个物质[守恒量](@entry_id:161475)：
$$
\frac{Dq}{Dt} = 0
$$
这意味着每个流体[质点](@entry_id:186768)在运动过程中都携带着其初始的位涡值。PV守恒极大地约束了流体的运动方式。例如，当一个空气柱在南北方向移动时，由于背景行星涡度（[科里奥利参数](@entry_id:1123077) $f$）的变化，它的相对涡度和（或）分层厚度必须相应调整以保持其PV不变。这一定律是理解大规模波动（如Rossby波）、[锋生](@entry_id:189043)、[气旋](@entry_id:262310)发展等众多天气和气候现象的核心。PV守恒的推导不依赖于静力或地转等强近似，是一个非常普适和深刻的原理。

### [湍流](@entry_id:151300)与动量建模的闭合问题

真实环境流动几乎都是[湍流](@entry_id:151300)。在模型中，我们只能解析网格尺度以上的运动，而网格尺度以下的[湍流](@entry_id:151300)涡旋运动必须被[参数化](@entry_id:265163)。

#### [Reynolds平均](@entry_id:754341)与Reynolds应力

为了处理[湍流](@entry_id:151300)，我们采用 **[Reynolds分解](@entry_id:267756)（Reynolds decomposition）**，将[瞬时速度](@entry_id:167797) $u_i$ 分解为时间平均（或系综平均）的平均流 $\overline{u_i}$ 和脉动部分 $u_i'$，即 $u_i = \overline{u_i} + u_i'$。将此分解代入[非线性](@entry_id:637147)的动量方程并进行平均，会产生一个新的项：
$$
-\frac{\partial}{\partial x_j}(\rho \overline{u_i' u_j'})
$$
这个张量 $\boldsymbol{\tau}^R_{ij} = -\rho \overline{u_i' u_j'}$ 被称为 **Reynolds[应力张量](@entry_id:148973)（Reynolds stress tensor）**。它在物理上代表了由[湍流](@entry_id:151300)脉动引起的[动量通量](@entry_id:199796)。例如，$-\rho \overline{u_1' u_3'}$ 表示由垂直速度脉动 $u_3'$ 引起的水[平动](@entry_id:187700)量 $u_1'$ 的平均垂直输运。这个新出现的项使得平均后的方程组不闭合，因为我们为平均流引入了新的未知量（Reynolds应力）。这就是经典的 **[湍流](@entry_id:151300)闭合问题（turbulence closure problem）**。

#### [涡粘性假设](@entry_id:1124144)

最常用的闭合方法之一是 **[涡粘性假设](@entry_id:1124144)（eddy viscosity hypothesis）**，由Boussinesq提出。该假设认为，[湍流](@entry_id:151300)对平均流的作用类似于分子粘性对流动的作用，即[湍流](@entry_id:151300)引起的[动量输运](@entry_id:139628)倾向于抹平平均流的[速度梯度](@entry_id:261686)。据此，Reynolds应力被[参数化](@entry_id:265163)为与平均[应变率张量](@entry_id:266108) $S_{ij} = \frac{1}{2}(\partial_j \overline{u_i} + \partial_i \overline{u_j})$ 成正比：
$$
-\rho \overline{u_i' u_j'} \approx 2 \rho \nu_t S_{ij} - \frac{2}{3}\rho k \delta_{ij}
$$
其中，$\nu_t$ 就是 **涡粘性系数（eddy viscosity coefficient）**。与作为流体固有属性的分子粘性系数 $\nu$ 不同，涡粘性系数 $\nu_t$ 是[湍流](@entry_id:151300)流动的属性，它通常在空间和时间上变化，并且远大于分子粘性系数。它代表了未解析的[湍流](@entry_id:151300)涡旋对平均动量的“扩散”效应，倾向于将能量从解析尺度耗散到未解析的[湍流](@entry_id:151300)尺度。这个[参数化](@entry_id:265163)的应力项以[散度形式](@entry_id:748608)进入动量方程，因此它在模型内部重新分配动量，而不凭空创造或销毁[总动量](@entry_id:173071)。 

#### [多孔介质](@entry_id:154591)中的动量

在模拟地下水流或 canopy flow 等[多孔介质流动](@entry_id:146440)时，[动量守恒](@entry_id:149964)方程需要通过体积平均进行修正。引入孔隙度 $\phi(\mathbf{x})$（代表流体所占体积的比例），流体相的[动量密度](@entry_id:271360)应表示为单位 **整体体积（bulk volume）** 内的动量。若 $\mathbf{u}$ 是孔隙内的平均流速（intrinsic velocity），则整体体积内的流体质量密度为 $\phi\rho$。因此，单位整体体积的[动量密度](@entry_id:271360)为 $\phi\rho\mathbf{u}$。在一个大的控制体积 $\Omega$ 内，总的流体动量就是对这个量进行积分：$\int_{\Omega} \phi\rho\mathbf{u} \, dV$。

### 动量的[数值守恒](@entry_id:175179)

在计算机模型中，精确地保持离散形式的守恒律是至关重要的，以避免长[时间积分](@entry_id:267413)后产生非物理的漂移。

#### [有限体积法](@entry_id:141374)与[离散守恒](@entry_id:1123819)

**[有限体积法](@entry_id:141374)（Finite Volume Method, FVM）** 是保证[离散守恒](@entry_id:1123819)的天然框架。它直接对积分形式的守恒定律进行离散化。对于[动量方程](@entry_id:197225)的通量形式：
$$
\frac{d}{dt} \int_{C_i} \rho\mathbf{u} \, dV + \sum_{f \in \partial C_i} \int_f (\rho \mathbf{u} \mathbf{u} + p\mathbf{I} - \boldsymbol{\tau}) \cdot \mathbf{n}_f \, dA = \int_{C_i} \rho \mathbf{g} \, dV
$$
FVM的核心思想是，对于任意一个内部交界面 $f$（分隔单元 $C_L$ 和 $C_R$），从 $C_L$ 流出的[数值通量](@entry_id:145174)必须精确等于流入 $C_R$ 的数值通量。这要求在界面 $f$ 上的动量通量被计算为一个 **单值（single-valued）**。即，无论从哪一侧的单元信息来重构界面通量，得到的结果必须是唯一的。

当这个条件满足时，将所有单元的方程加总，所有内部界面的通量项都会两两抵消。最终，整个计算域的[总动量](@entry_id:173071)变化率就只取决于通过外部边界的通量和作用于全域的彻[体力](@entry_id:174230)之和。这就实现了离散意义下的 **全局[动量守恒](@entry_id:149964)（global momentum conservation）**。这个原则的实现与网格是否正交无关，尽管[非正交网格](@entry_id:752592)可能会降低通量计算的精度，但只要保证了界面通量的[单值性](@entry_id:174849)，守恒性就能得到保障。