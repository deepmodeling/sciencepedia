## 引言
在现代大气科学和气候研究领域，[原始方程](@entry_id:1130162)组（Primitive Equations）扮演着基石般的角色，它们是描述地球大气大尺度运动的物理定律的数学体现。然而，这些方程的复杂性要求我们必须选择一个巧妙的坐标系统来简化其形式并提高求解效率。压强坐标系，正是这样一个因其理论优雅性和计算便利性而被广泛采用的框架。本文旨在系统性地剖析以压强为垂直坐标的原始方程组，揭示其为何成为[数值天气预报](@entry_id:191656)和气候模拟的行业标准。

本文致力于解决一个核心问题：为何以及如何将基于几何高度的[复杂流体](@entry_id:198415)动力学方程，转换为一个在压强坐标下更为简洁且物理意义更为清晰的理论体系。我们将带领读者穿越这一理论构建的全过程，从最基本的物理近似出发，直至其在复杂现实问题中的高级应用。

在接下来的内容中，读者将首先在“原理与机制”一章中，学习[静力平衡近似](@entry_id:1126281)的本质，理解压强坐标系的建立基础，并逐一推导动量、连续性和[热力学](@entry_id:172368)方程在这一新坐标下的形式。随后，“应用与跨学科联系”一章将展示这套理论的强大威力，探讨如何利用它来诊断风场、分析大气波动、构建[准地转理论](@entry_id:1130437)，并将其与[气候动力学](@entry_id:192646)中的全球能量循环和环流模式联系起来。最后，“实践练习”部分将提供具体的计算问题，帮助读者将理论知识转化为解决实际问题的技能。通过这一结构化的学习路径，本文将为您构建一个关于大气动力学核心方程的完整知识图谱。

## 原理与机制

本章旨在深入探讨以压强为垂直坐标的[原始方程](@entry_id:1130162)组的物理原理和数学机制。我们将从采用压强坐标的根本原因出发，逐步构建整个方程体系，并阐明其在描述大尺度大气运动中的核心作用与固有属性。

### 压强坐标系的理论基础

在地球物理流体力学中，选择合适的坐标系对于简化控制方程和提高数值求解效率至关重要。尽管几何高度（$z$ 坐标）在直观上最为自然，但在模拟大尺度[大气环流](@entry_id:1125564)时，采用压强（$p$）作为垂直坐标具有显著的理论优势。这一转换的基石是 **[静力平衡近似](@entry_id:1126281) (hydrostatic balance approximation)**。

#### [静力平衡近似](@entry_id:1126281)

让我们从垂直方向的[动量方程](@entry_id:197225)（牛顿第二定律）出发：

$$
\frac{Dw}{Dt} = -\frac{1}{\rho}\frac{\partial p}{\partial z} - g + (\text{Coriolis})_z + \mathcal{F}_z
$$

其中，$w$ 是几何垂直速度，$D/Dt$ 是物质导数，$\rho$ 是密度，$p$ 是压强，$z$ 是几何高度，$g$ 是重力加速度，$(\text{Coriolis})_z$ 是科里奥利力的垂直分量，$\mathcal{F}_z$ 代表摩擦和[粘性力](@entry_id:263294)。

对于天气尺度（synoptic scale）的大尺度运动，其水平尺度（$L \sim 10^6$ m）远大于垂直尺度（$H \sim 10^4$ m）。通过[尺度分析](@entry_id:1131264)可以发现，方程左侧的垂直加速度项（$Dw/Dt$）和科里奥利力垂直分量远小于[垂直气压梯度](@entry_id:1133794)力（$-\frac{1}{\rho}\frac{\partial p}{\partial z}$）和重力（$-g$）。具体而言，[垂直气压梯度](@entry_id:1133794)力和重力的大小均在 $10$ m/s² 量级，而垂直加速度和科里奥利力的量级则要小上好几个数量级。因此，在极高的精度下，我们可以忽略较小的项，得到主导的力学平衡关系：

$$
\frac{\partial p}{\partial z} = -\rho g
$$

这就是 **[静力平衡](@entry_id:163498)方程**。它表明，在垂直方向上，向上的气压[梯度力](@entry_id:166847)与向下的重力几乎完全抵消。这个诊断关系取代了完整的、具有预报性的[垂直动量方程](@entry_id:1133792)。由于密度 $\rho$ 和[重力加速度](@entry_id:173411) $g$ 均为正值，该关系确保了压强 $p$ 随高度 $z$ 单调递减。这一[单调性](@entry_id:143760)是压强能够作为有效垂直坐标的根本前提 。

然而，[静力平衡](@entry_id:163498)是一个近似。在垂直加速度不可忽略的情况下，该近似会失效。这通常发生在水平尺度和垂直尺度相当的系统中（即运动的“深宽比”接近1），例如强烈的[深对流](@entry_id:1123472)（雷暴）、山地[背风波](@entry_id:274386)以及短波长的重力内波 。在这些 **非静力 (non-hydrostatic)** 过程中，必须使用完整的[垂直动量方程](@entry_id:1133792)。

[静力平衡近似](@entry_id:1126281)的一个重要后果是它过滤掉了垂直传播的声波。声波的传播依赖于压强扰动与垂直加速度之间的动态耦合。通过用一个诊断关系取代预报垂直加速度的方程，[静力平衡](@entry_id:163498)模型从根本上切断了这种耦合机制，从而无法支持垂直声波的存在 。

### 压强坐标系中的变量与变换

从 $z$ [坐标系转换](@entry_id:263003)到 $p$ 坐标系，我们需要重新定义垂直速度，并推导关键变量之间的关系。

#### 压强垂直速度 ($\omega$)

在 $p$ 坐标系中，垂直速度被定义为流体[质点](@entry_id:186768)随时间经历的压强变化率，记为 $\omega$（omega）：

$$
\omega \equiv \frac{Dp}{Dt}
$$

$\omega$ 的物理意义是质点穿越等压面的速率。根据[静力平衡](@entry_id:163498)，压强随高度增加而减小。因此，一个上升的空气[质点](@entry_id:186768)（$w = Dz/Dt > 0$）会移动到压强更低的区域，导致其 $\omega$ 值为负。反之，下沉的质点（$w  0$）会进入高压区，其 $\omega$ 值为正。所以，**上升运动对应 $\omega  0$，下沉运动对应 $\omega > 0$** 。

#### 位势与 $p$ 坐标系下的静力方程

为了处理重力势能，我们引入 **位势 (geopotential)**，定义为 $\Phi = g z$。位势是在重[力场](@entry_id:147325)中将单位质量的物体从海平面（$z=0$）提升到高度 $z$ 所需的功。

在 $p$ 坐标系下，[静力平衡](@entry_id:163498)方程可以被转换成一个关于位势的优雅形式。从定义出发，对 $\Phi$ 求 $p$ 的[偏导数](@entry_id:146280)（保持水平位置和时间不变）：

$$
\frac{\partial \Phi}{\partial p} = \frac{\partial (gz)}{\partial p} = g \frac{\partial z}{\partial p}
$$

利用[静力平衡](@entry_id:163498)方程 $\frac{\partial p}{\partial z} = -\rho g$ 的倒数关系 $\frac{\partial z}{\partial p} = - \frac{1}{\rho g}$，我们得到：

$$
\frac{\partial \Phi}{\partial p} = g \left( -\frac{1}{\rho g} \right) = -\frac{1}{\rho}
$$

定义 **比容 (specific volume)** 为密度的倒数 $\alpha = 1/\rho$，最终得到 $p$ 坐标系下的静力方程 ：

$$
\frac{\partial \Phi}{\partial p} = -\alpha
$$

这个方程揭示了一个深刻的物理联系：两个等压面之间的位势厚度（即几何厚度）与比容成正比。由于理想气体定律（$p\alpha = RT$），比容与温度 $T$ 成正比。因此，暖空气层（$\alpha$ 较大）中等压面之间的[垂直距离](@entry_id:176279)比冷空气层（$\alpha$ 较小）中的更远。

#### 坐标变换与[体积元](@entry_id:267802)

从数学角度看，从 $(x, y, z)$ 坐标到 $(x, y, p)$ 坐标的转换，其雅可比行列式 $J$ 为：

$$
J = \det\left(\frac{\partial(x,y,p)}{\partial(x,y,z)}\right) = \det\begin{pmatrix} 1  0  0 \\ 0  1  0 \\ \frac{\partial p}{\partial x}  \frac{\partial p}{\partial y}  \frac{\partial p}{\partial z} \end{pmatrix} = \frac{\partial p}{\partial z}
$$

利用[静力平衡](@entry_id:163498)关系，我们得到 $J = -\rho g$。根据[多重积分](@entry_id:146170)的变量代换法则，两个坐标系下的体积元 $dV_z = dx\,dy\,dz$ 和 $dV_p = dx\,dy\,dp$ 之间的关系由[雅可比行列式](@entry_id:137120)的绝对值决定：

$$
dx\,dy\,dp = |J| \, dx\,dy\,dz \implies dx\,dy\,dp = \rho g \, dx\,dy\,dz
$$

因此，我们有重要的[体积元](@entry_id:267802)转换关系 ：

$$
dx\,dy\,dz = \frac{1}{\rho g} dx\,dy\,dp
$$

这个关系是进行[积分变换](@entry_id:186209)（如质量积分）的关键。

### 压强坐标系下的原始方程组

现在，我们可以利用上述原理，将流[体力](@entry_id:174230)学和[热力学](@entry_id:172368)的基本定律系统地转换到压强坐标系中，从而得到一套自洽的 **[原始方程](@entry_id:1130162)组 (primitive equations)** 。

#### 水平[动量方程](@entry_id:197225)

在 $z$ 坐标系中，水平动量方程中的气压[梯度力](@entry_id:166847)项为 $(-\frac{1}{\rho} \nabla_z p)$。在 $p$ 坐标系中，该项被优雅地替换为位[势的梯度](@entry_id:268447) $(-\nabla_p \Phi)$。这一变换的本质在于：

$$
\left(\frac{\partial p}{\partial x}\right)_z = \rho g \left(\frac{\partial z}{\partial x}\right)_p = \rho \left(\frac{\partial \Phi}{\partial x}\right)_p
$$

因此，$-\frac{1}{\rho}(\frac{\partial p}{\partial x})_z = -(\frac{\partial \Phi}{\partial x})_p$。[物质导数](@entry_id:262900) $D/Dt$ 在坐标变换下保持形式不变，但在 $p$ 坐标系下展开为 $D/Dt = \partial/\partial t + u \partial/\partial x + v \partial/\partial y + \omega \partial/\partial p$。最终，水平动量方程为：

$$
\frac{Du}{Dt} - fv = -\frac{\partial \Phi}{\partial x} + F_u
$$
$$
\frac{Dv}{Dt} + fu = -\frac{\partial \Phi}{\partial y} + F_v
$$

其中 $f$ 是[科里奥利参数](@entry_id:1123077)，$F_u$ 和 $F_v$ 是摩擦力项。

#### 连续性方程

[连续性方程](@entry_id:195013)（质量守恒定律）在 $p$ 坐标系下的形式是该坐标系最显著的优点之一。从 $z$ 坐标系下的连续性方程 $\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0$ 出发，利用[体积元](@entry_id:267802)变换关系可以推导出 $p$ 坐标系的形式。一个更直观的方法是考虑单位水平面积内，压强层 $dp$ 所含的质量 $dM$。根据[静力平衡](@entry_id:163498)，$dM = \rho |dz| = \rho (\frac{dp}{\rho g}) = \frac{dp}{g}$。这表明，在压强坐标系中，单位坐标体积 $(dx\,dy\,dp)$ 内的质量“密度”为 $1/g$。由于 $g$ 通常假定为常数，这个“密度”在时空中也是恒定的。这使得质量守-恒定律简化为一个类似于不可压缩流体的无散度条件 ：

$$
\frac{\partial u}{\partial x} + \frac{\partial v}{\partial y} + \frac{\partial \omega}{\partial p} = 0 \quad \text{或} \quad \nabla_p \cdot \mathbf{v} + \frac{\partial \omega}{\partial p} = 0
$$

注意，这个简洁形式的方程描述的是一个完全可压缩的大气，其简化完全归功于坐标系的选择和[静力平衡](@entry_id:163498)假设，而非任何关于流体[可压缩性](@entry_id:144559)的近似。密度 $\rho$ 在方程中被完全消除，这是一个巨大的简化。

#### [热力学](@entry_id:172368)能量方程

[热力学第一定律](@entry_id:146485)通常写作 $c_p \frac{DT}{Dt} - \alpha \frac{Dp}{Dt} = Q$，其中 $Q$ 是单位质量的[非绝热加热](@entry_id:1123650)率。在 $p$ 坐标系中，由于 $\omega \equiv Dp/Dt$，并且利用[理想气体定律](@entry_id:146757) $\alpha = RT/p$，方程可直接写为：

$$
c_p \frac{DT}{Dt} - \frac{RT}{p} \omega = Q
$$

两边同除以 $c_p$ 并定义 $\kappa = R/c_p$，得到：

$$
\frac{DT}{Dt} - \frac{\kappa T}{p} \omega = \frac{Q}{c_p}
$$

这个方程描述了随质点运动的温度变化，它受到水平和垂直热量平流、[非绝热加热](@entry_id:1123650)（$Q$）以及因垂直运动引起的[绝热压缩](@entry_id:142708)或膨胀（$\omega$ 项）的控制。

#### 完整的干空气原始方程组

综上所述，描述干空气的静力[原始方程](@entry_id:1130162)组在压强坐标系 $(x,y,p,t)$ 下由以下五个方程组成 ：

1.  **$x$ 方向动量方程:** $\dfrac{Du}{Dt} - fv = -\dfrac{\partial \Phi}{\partial x} + F_u$
2.  **$y$ 方向动量方程:** $\dfrac{Dv}{Dt} + fu = -\dfrac{\partial \Phi}{\partial y} + F_v$
3.  **[静力平衡](@entry_id:163498)方程 (诊断方程):** $\dfrac{\partial \Phi}{\partial p} = -\alpha = -\dfrac{RT}{p}$
4.  **[连续性方程](@entry_id:195013):** $\dfrac{\partial u}{\partial x} + \dfrac{\partial v}{\partial y} + \dfrac{\partial \omega}{\partial p} = 0$
5.  **[热力学](@entry_id:172368)能量方程:** $\dfrac{DT}{Dt} - \dfrac{\kappa T}{p} \omega = \dfrac{Q}{c_p}$

其中[物质导数](@entry_id:262900) $\dfrac{D}{Dt} = \dfrac{\partial}{\partial t} + u\dfrac{\partial}{\partial x} + v\dfrac{\partial}{\partial y} + \omega\dfrac{\partial}{\partial p}$。这套方程组是现代[数值天气预报](@entry_id:191656)和气候模型的核心。

### 系统的关键物理属性

#### 质量守恒与地面气压倾向

$p$ 坐标系下的[连续性方程](@entry_id:195013)提供了一个强大的工具来诊断地面气压的变化。将[连续性方程](@entry_id:195013)从大气层顶（$p=p_t$，通常取 $p_t=0$）到地面（$p=p_s(x,y,t)$）进行垂[直积](@entry_id:143046)分：

$$
\int_{p_t}^{p_s} (\nabla_p \cdot \mathbf{v}) \, dp + \int_{p_t}^{p_s} \frac{\partial \omega}{\partial p} \, dp = 0
$$

第二个积分等于 $[\omega]_{p_t}^{p_s} = \omega(p_s) - \omega(p_t)$。根据边界条件，$\omega(p_t)=0$，而 $\omega(p_s) = Dp_s/Dt$。因此，我们得到地面气压的[预报方程](@entry_id:1130221) ：

$$
\frac{Dp_s}{Dt} = -\int_{p_t}^{p_s} (\nabla_p \cdot \mathbf{v}) \, dp
$$

此式表明，地面气压的物质变化率（即随近地面空气运动的变化）等于整层大气质量的水平辐散的负值。当整层大气表现为质量辐散时（积分项为正），地面气压下降；当整层大气为质量辐合时，地面气压上升。

#### 静力稳定度

大气的 **静力稳定度 (static stability)** 决定了它对垂直运动的抑制或促进程度。稳定度的基本判据是位温 $\theta$ 随高度的变化。在 $p$ 坐标系中，稳定条件 $\partial\theta/\partial z > 0$ 对应于 $\partial\theta/\partial p  0$。

为了量化稳定度，我们定义 **静力稳定度参数 $\sigma$** ：

$$
\sigma = -\alpha \frac{\partial \ln \theta}{\partial p} = -\frac{RT}{p} \frac{\partial \ln \theta}{\partial p}
$$

根据这个定义，在稳定大气中（$\partial\theta/\partial p  0$），$\sigma > 0$。$\sigma$ 值越大，大气越稳定。

静力稳定度参数 $\sigma$ 与更基本的物理量 **[布伦特-维萨拉频率](@entry_id:1121902) (Brunt–Väisälä frequency)** $N$密切相关，后者的平方 $N^2 = \frac{g}{\theta}\frac{\partial\theta}{\partial z}$ 是[浮力](@entry_id:154088)恢复力的度量。通过变换可以证明 ：

$$
N^2 = \frac{g^2 \sigma}{RT}
$$

这个关系清楚地表明，$\sigma$ 在 $p$ 坐标系中扮演着与 $N^2$ 在 $z$ 坐标系中同样的角色。在[准地转理论](@entry_id:1130437)等大尺度动力学框架中，$\sigma$ 直接出现在描述垂直运动的方程中，它代表了大气对垂直位移的“刚性”或“弹性”。一个大的 $\sigma$ 值意味着强大的[浮力](@entry_id:154088)恢复力，对由动力强迫引起的垂直运动有强烈的抑制作用 。

#### [原始方程](@entry_id:1130162)组中的波动

如前所述，[静力平衡近似](@entry_id:1126281)有效地滤除了[垂直传播](@entry_id:204688)的声波。然而，该系统仍然支持对[数值模拟](@entry_id:146043)至关重要的其他快速波动 ：

-   **惯性-重力波 (Inertia-Gravity Waves):** 这些是高频波，其恢复力来自[浮力](@entry_id:154088)（重力）和科里奥利力（惯性）。它们分为两种：
    1.  **外重力波 (External Gravity Waves):** 这种波的垂直结构为正压模式，即整个大气柱同相运动。它们的行为类似于浅水波，水平传播速度非常快，约为 $c \approx \sqrt{gH}$，其中 $H$ 是大气的等效厚度（约 $10$ km）。这导致其速度可达 $300$ m/s 左右，与声速相当。这是静力模型中速度最快的波。
    2.  **[内重力波](@entry_id:185206) (Internal Gravity Waves):** 这种波具有随高度变化的垂直结构（[斜压模](@entry_id:1121346)式），其频率上限为[布伦特-维萨拉频率](@entry_id:1121902) $N$。

这些快速重力波的存在，尤其是高速的外重力波，给数值模型的稳定性带来了严峻挑战。根据 Courant-Friedrichs-Lewy (CFL) 条件，[显式时间积分](@entry_id:165797)方案的时间步长必须足够小，以至于最快的波在一个时间步内传播的距离不超过一个网格距。对于全[球模型](@entry_id:161388)而言，这意味着时间步长可能只有几分钟，这在计算上是难以承受的。因此，现代模型普遍采用 **半隐式 (semi-implicit)** 或 **分裂-显式 (split-explicit)** 等时间积分方案来有效处理这些快速波，从而允许使用更长的时间步长。