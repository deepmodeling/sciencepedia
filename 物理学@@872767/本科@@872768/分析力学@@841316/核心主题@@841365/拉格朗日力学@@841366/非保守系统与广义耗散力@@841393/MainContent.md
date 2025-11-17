## 引言
在[分析力学](@entry_id:166738)中，[拉格朗日形式主义](@entry_id:158185)为描述保守系统提供了一个优雅而强大的框架，其中系统的[总机械能](@entry_id:167353)保持守恒。然而，真实世界充满了摩擦、空气阻力等[非保守力](@entry_id:163431)，它们导致[能量耗散](@entry_id:147406)，使得理想化的保守模型在许多实际应用中显得力不从心。如何将这些普遍存在的耗散效应系统地纳入[拉格朗日框架](@entry_id:751113)，是理论力学面临的一个核心问题。

本文旨在填补这一空白，系统阐述处理[非保守系统](@entry_id:166237)与广义[耗散力](@entry_id:166970)的理论和方法。通过学习本文，您将能够超越理想化模型的限制，分析更为现实和复杂的物理情景。在接下来的内容中，读者将首先在“原理与机制”一章中，深入理解[广义力](@entry_id:169699)和[瑞利耗散函数](@entry_id:165938)的定义、计算及其对系统能量的影响；随后，通过“应用与跨学科联系”一章，探索这些原理在经典力学、电磁学、天体物理学等多个领域中的实际应用；最后，通过一系列精心设计的“动手实践”问题，巩固和深化对这些概念的理解与运用。

## 原理与机制

在[拉格朗日力学](@entry_id:147054)的基础框架中，我们通常处理的是**保守系统**。在这些系统中，所有力都可以从一个标量势能函数 $U$ 中导出，并且系统的[总机械能](@entry_id:167353) $E = T + U$ 是守恒的。然而，现实世界中的物理系统很少是完全保守的。[摩擦力](@entry_id:171772)、空气阻力以及各种驱动力等**[非保守力](@entry_id:163431)**普遍存在，它们会导致机械能不守恒。本章旨在将[拉格朗日形式主义](@entry_id:158185)扩展到[非保守系统](@entry_id:166237)，重点阐述处理这些相互作用的原理和机制。

### [广义力](@entry_id:169699)：非保守相互作用的语言

扩展[拉格朗日力学](@entry_id:147054)的最直接方法是在[拉格朗日方程](@entry_id:175419)中引入一个附加项，以描述[非保守力](@entry_id:163431)的效应。对于一个由[广义坐标](@entry_id:156576) $q_j$ 描述的系统，包含[非保守力](@entry_id:163431)的[拉格朗日方程](@entry_id:175419)形式如下：

$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \frac{\partial L}{\partial q_j} = Q_j
$$

这里的 $L = T - V$ 仍然是系统的拉格朗日量，其中 $V$ 只包含所有**保守力**对应的[势能](@entry_id:748988)。右侧的项 $Q_j$ 被称为**[广义力](@entry_id:169699)**，它代表了所有作用于系统的**[非保守力](@entry_id:163431)**的总效应。

[广义力](@entry_id:169699) $Q_j$ 是通过[虚功原理](@entry_id:138749)定义的。由[非保守力](@entry_id:163431) $\mathbf{F}_i^{\text{nc}}$ 在[虚位移](@entry_id:168781) $\delta \mathbf{r}_i$ 中所做的[虚功](@entry_id:176403)为 $\delta W_{\text{nc}} = \sum_i \mathbf{F}_i^{\text{nc}} \cdot \delta \mathbf{r}_i$。将[虚位移](@entry_id:168781)用[广义坐标](@entry_id:156576)表示 $\delta \mathbf{r}_i = \sum_j \frac{\partial \mathbf{r}_i}{\partial q_j} \delta q_j$，我们得到：

$$
\delta W_{\text{nc}} = \sum_i \mathbf{F}_i^{\text{nc}} \cdot \left(\sum_j \frac{\partial \mathbf{r}_i}{\partial q_j} \delta q_j\right) = \sum_j \left(\sum_i \mathbf{F}_i^{\text{nc}} \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}\right) \delta q_j
$$

通过将此表达式与[虚功](@entry_id:176403)的定义 $\delta W_{\text{nc}} = \sum_j Q_j \delta q_j$ 进行比较，我们获得了计算[广义力](@entry_id:169699)的实用公式：

$$
Q_j = \sum_i \mathbf{F}_i^{\text{nc}} \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}
$$

这个公式是[广义力](@entry_id:169699)的核心定义，它将笛卡尔坐标系下的[非保守力](@entry_id:163431)矢量映射到系统的[广义坐标](@entry_id:156576)上。值得注意的是，$Q_j$ 的量纲不一定是力；例如，如果 $q_j$ 是一个角度，那么 $Q_j$ 的量纲就是力矩。

#### [广义力](@entry_id:169699)的计算实例

为了更好地理解[广义力](@entry_id:169699)的计算，我们来看几个例子。

考虑一个[改进的阿特伍德机](@entry_id:178147)，其中物块 $m_2$ 在一个水平面上滑动，该平面的[动摩擦系数](@entry_id:162794)依赖于位置 $x$，即 $\mu_k(x) = \alpha + \beta x$ [@problem_id:2067487]。系统的唯一[非保守力](@entry_id:163431)是作用在 $m_2$ 上的[摩擦力](@entry_id:171772)。当 $m_2$向右滑动时，[摩擦力](@entry_id:171772)方向向左，大小为 $F_f = \mu_k(x) N = (\alpha + \beta x)m_2 g$。因此，[摩擦力](@entry_id:171772)的矢量形式为 $\mathbf{F}_f = -(\alpha + \beta x)m_2 g \hat{\mathbf{i}}$。物块 $m_2$ 的位置矢量是 $\mathbf{r}_2 = x \hat{\mathbf{i}}$。使用[广义力](@entry_id:169699)的定义，我们可以计算与[广义坐标](@entry_id:156576) $x$ 相关联的[广义力](@entry_id:169699) $Q_x$：

$$
Q_x = \mathbf{F}_f \cdot \frac{\partial \mathbf{r}_2}{\partial x} = \left(-(\alpha + \beta x)m_2 g \hat{\mathbf{i}}\right) \cdot (\hat{\mathbf{i}}) = -m_2 g (\alpha + \beta x)
$$

这个负号清晰地表明，[摩擦力](@entry_id:171772)阻碍了坐标 $x$ 的增加，这与我们的物理直觉相符。

[广义力](@entry_id:169699)方法在处理复杂几何约束和非笛卡尔坐标系时尤其显示出其威力。考虑一个质量为 $m$ 的粒子在一个由 $z=a\rho^2$ 定义的[抛物面](@entry_id:264713)碗内运动，并受到[线性阻力](@entry_id:265409) $\mathbf{F}_d = -k\mathbf{v}$ 的作用 [@problem_id:2067513]。我们使用柱坐标 $(\rho, \phi)$ 作为[广义坐标](@entry_id:156576)。粒子的位置矢量可以写为 $\mathbf{r} = \rho \mathbf{e}_\rho + z \mathbf{e}_z = \rho \mathbf{e}_\rho + a\rho^2 \mathbf{e}_z$。速度为 $\mathbf{v} = \dot{\rho} \mathbf{e}_\rho + \rho\dot{\phi} \mathbf{e}_\phi + 2a\rho\dot{\rho} \mathbf{e}_z$。

要计算与[径向坐标](@entry_id:165186) $\rho$ 相关联的广义阻力 $Q_\rho$，我们需要计算 $\frac{\partial \mathbf{r}}{\partial \rho}$：

$$
\frac{\partial \mathbf{r}}{\partial \rho} = \mathbf{e}_\rho + 2a\rho \mathbf{e}_z
$$

然后，应用[广义力](@entry_id:169699)的定义：

$$
Q_\rho = \mathbf{F}_d \cdot \frac{\partial \mathbf{r}}{\partial \rho} = (-k\mathbf{v}) \cdot (\mathbf{e}_\rho + 2a\rho \mathbf{e}_z)
$$

将速度表达式代入，并利用柱坐标[基矢](@entry_id:199546)量的正交性（$\mathbf{e}_i \cdot \mathbf{e}_j = \delta_{ij}$），我们得到：

$$
Q_\rho = -k \left( (\dot{\rho}\mathbf{e}_\rho + \rho\dot{\phi}\mathbf{e}_\phi + 2a\rho\dot{\rho}\mathbf{e}_z) \cdot (\mathbf{e}_\rho + 2a\rho \mathbf{e}_z) \right) = -k(\dot{\rho} + 4a^2\rho^2\dot{\rho}) = -k\dot{\rho}(1 + 4a^2\rho^2)
$$

这个结果展示了[广义力](@entry_id:169699)如何将一个简单的笛卡尔力定律（$\mathbf{F}_d = -k\mathbf{v}$）转化为一个在[广义坐标](@entry_id:156576)中依赖于坐标和速度的复杂表达式。

### [非保守系统](@entry_id:166237)中的能量与功率

[广义力](@entry_id:169699)的引入直接影响系统的[能量守恒](@entry_id:140514)。一个系统的[总机械能](@entry_id:167353)定义为 $E = T+V$。其随时间的变化率可以通过[拉格朗日方程](@entry_id:175419)推导得出。对于一个由[广义坐标](@entry_id:156576) $q_j$ 描述的系统，能量的时间导数为：

$$
\frac{dE}{dt} = \frac{d}{dt} \left( \sum_j \dot{q}_j \frac{\partial L}{\partial \dot{q}_j} - L \right) = \sum_j \dot{q}_j \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \sum_j \frac{\partial L}{\partial q_j}\dot{q}_j - \frac{\partial L}{\partial t}
$$

将[拉格朗日方程](@entry_id:175419) $\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) = \frac{\partial L}{\partial q_j} + Q_j$ 代入上式，并假设拉格朗日量不显含时间（$\frac{\partial L}{\partial t} = 0$），我们得到一个极为重要的关系：

$$
\frac{dE}{dt} = \sum_j \dot{q}_j \left( \frac{\partial L}{\partial q_j} + Q_j \right) - \sum_j \frac{\partial L}{\partial q_j}\dot{q}_j = \sum_j Q_j \dot{q}_j
$$

这个方程表明，**机械能的变化率等于非保守[广义力](@entry_id:169699)所做的[瞬时功率](@entry_id:174754)**。如果 $Q_j$ 是[耗散力](@entry_id:166970)（如[摩擦力](@entry_id:171772)或阻力），它通常与 $\dot{q}_j$ 方向相反，导致 $Q_j \dot{q}_j  0$，系统能量减少。此时，[能量耗散](@entry_id:147406)的速率为 $P_{\text{diss}} = -\frac{dE}{dt} = -\sum_j Q_j \dot{q}_j$。

例如，对于一个在垂直圆环上运动并受到二次阻力 $F_d = cv^2$ 的珠子 [@problem_id:2053754]，我们可以计算其[能量耗散](@entry_id:147406)率。珠子的速度为 $v=R|\dot{\theta}| = R|\omega|$。在这里，$Q_\theta$ 是与[广义坐标](@entry_id:156576) $\theta$ 相关的[广义力](@entry_id:169699)，即力矩。阻力大小为 $F_d = cv^2 = c(R\omega)^2$，方向与运动相反。因此，它产生的力矩与角速度 $\omega$ 方向相反，大小为 $R F_d$。所以：

$$
Q_\theta = -R F_d \mathrm{sgn}(\omega) = -R(c(R\omega)^2)\mathrm{sgn}(\omega) = -cR^3\omega^2\mathrm{sgn}(\omega) = -cR^3\omega|\omega|
$$

因此，[能量耗散](@entry_id:147406)率为：

$$
P_{\text{diss}} = -Q_\theta \omega = -(-cR^3\omega|\omega|)\omega = cR^3\omega^2|\omega| = cR^3|\omega|^3
$$

这个结果也可以通过更直接的物理方法得到：[耗散功率](@entry_id:177328)就是 $\mathbf{F}_d \cdot \mathbf{v}$ 的大小。由于 $\mathbf{F}_d$ 与 $\mathbf{v}$ 反向，$\mathbf{F}_d \cdot \mathbf{v} = -F_d v = - (cv^2)v = -cv^3$。耗散率是其[绝对值](@entry_id:147688)，即 $P_{\text{diss}} = cv^3 = c(R|\omega|)^3 = cR^3|\omega|^3$，与通过[广义力](@entry_id:169699)得到的结果一致。

如果我们将能量变化率对[时间积分](@entry_id:267413)，就可以得到总能量变化与[非保守力](@entry_id:163431)做功之间的关系。对于一个初始能量为 $E_i$ 的系统，在运动后达到末态能量 $E_f$，其间的能量变化等于[非保守力](@entry_id:163431)做的总功 $W_{\text{nc}}$：

$$
\Delta E = E_f - E_i = \int_{t_i}^{t_f} \frac{dE}{dt} dt = \int_{t_i}^{t_f} \left(\sum_j Q_j \dot{q}_j\right) dt = W_{\text{nc}}
$$

一个经典的例子是弹簧[振子](@entry_id:271549)在恒定[动摩擦](@entry_id:177897)力作用下的运动 [@problem_id:2067554]。如果一个质量为 $m$ 的物块连接到劲度系数为 $k$ 的弹簧，在有[动摩擦系数](@entry_id:162794)为 $\mu_k$ 的平面上[振荡](@entry_id:267781)。若物块从振幅 $A_0$ 处静止释放，并最终停在平衡位置 $x=0$ 处，我们可以通过[能量守恒](@entry_id:140514)来计算总路程 $S$。初始机械能为 $E_i = \frac{1}{2} k A_0^2$，末态[机械能](@entry_id:162989)为 $E_f = 0$。在此过程中，[非保守力](@entry_id:163431)（[摩擦力](@entry_id:171772)）做的总功为 $W_f = -F_f S = -\mu_k m g S$。根据功-能定理：

$$
E_f - E_i = W_f \implies 0 - \frac{1}{2} k A_0^2 = -\mu_k m g S
$$

解得总路程为 $S = \frac{k A_0^2}{2 \mu_k m g}$。

### [瑞利耗散函数](@entry_id:165938)

对于一类常见且重要的[耗散力](@entry_id:166970)——与速度成正比的[线性阻力](@entry_id:265409)——我们可以引入一个更为优雅的工具来系统地处理它们，即**[瑞利耗散函数](@entry_id:165938) (Rayleigh dissipation function)**，记作 $\mathcal{F}$。这个函数被定义为使得广义[耗散力](@entry_id:166970)可以通过以下方式导出：

$$
Q_j^{\text{diss}} = -\frac{\partial \mathcal{F}}{\partial \dot{q}_j}
$$

对于一个在三维空间中运动的粒子，如果它受到的[线性阻力](@entry_id:265409)为 $\mathbf{F}_d = -k\mathbf{v} = -k(\dot{x}\hat{\mathbf{i}} + \dot{y}\hat{\mathbf{j}} + \dot{z}\hat{\mathbf{k}})$，那么[瑞利耗散函数](@entry_id:165938)的形式为：

$$
\mathcal{F} = \frac{1}{2} k v^2 = \frac{1}{2} k (\dot{x}^2 + \dot{y}^2 + \dot{z}^2)
$$

不难验证，$\frac{\partial \mathcal{F}}{\partial \dot{x}} = k\dot{x}$，因此[广义力](@entry_id:169699) $Q_x = -k\dot{x}$，这正是阻力在 $x$ 方向的分量。

引入[瑞利耗散函数](@entry_id:165938)后，包含[线性阻力](@entry_id:265409)的[拉格朗日方程](@entry_id:175419)可以写成一个更加紧凑和对称的形式：

$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \frac{\partial L}{\partial q_j} + \frac{\partial \mathcal{F}}{\partial \dot{q}_j} = 0
$$

这个方程形式优美，因为它将[耗散力](@entry_id:166970)以类似于拉格朗日量 $L$ 的方式纳入了[动力学方程](@entry_id:751029)中。

一个典型的应用是计算在[粘性流](@entry_id:136330)体中下落的小球的**[终端速度](@entry_id:147799)** [@problem_id:2067512]。设小球质量为 $m$，向下为 $y$ 轴正方向。其拉格朗日量为 $L = T - U = \frac{1}{2} m \dot{y}^2 - (-mgy) = \frac{1}{2} m \dot{y}^2 + mgy$。[线性阻力](@entry_id:265409)对应的[瑞利耗散函数](@entry_id:165938)为 $\mathcal{F} = \frac{1}{2} k \dot{y}^2$。代入修正后的[拉格朗日方程](@entry_id:175419)：

$$
\frac{d}{dt}(m\dot{y}) - mg + k\dot{y} = 0 \implies m\ddot{y} = mg - k\dot{y}
$$

当小球达到终端速度 $v_t$ 时，其加速度为零，即 $\ddot{y}=0$。此时，重力与阻力平衡：$mg - k v_t = 0$，解得 $v_t = \frac{mg}{k}$。

[瑞利耗散函数](@entry_id:165938)的概念可以推广到更一般的情况，例如各向异性的线性阻尼。在这种情况下，阻力可以表示为 $\vec{F}_d = -\mathbf{B}\vec{v}$，其中 $\mathbf{B}$ 是一个对称的阻尼张量。相应的[瑞利耗散函数](@entry_id:165938)是一个关于[广义速度](@entry_id:178456)的二次型 [@problem_id:2067551]：

$$
\mathcal{F} = \frac{1}{2} \sum_{i,k} b_{ik} \dot{q}_i \dot{q}_k = \frac{1}{2} \dot{\mathbf{q}}^T \mathbf{B} \dot{\mathbf{q}}
$$

在这种情况下，瞬时[耗散功率](@entry_id:177328)与[瑞利耗散函数](@entry_id:165938)之间有一个非常简洁的关系。由于 $\mathcal{F}$ 是[广义速度](@entry_id:178456)的二次齐次函数，根据[欧拉齐次函数定理](@entry_id:186434)，我们有 $\sum_j \dot{q}_j \frac{\partial \mathcal{F}}{\partial \dot{q}_j} = 2\mathcal{F}$。因此，能量耗散率为：

$$
P_{\text{diss}} = -\sum_j Q_j^{\text{diss}} \dot{q}_j = -\sum_j \left(-\frac{\partial \mathcal{F}}{\partial \dot{q}_j}\right) \dot{q}_j = \sum_j \frac{\partial \mathcal{F}}{\partial \dot{q}_j} \dot{q}_j = 2\mathcal{F}
$$

这意味着能量耗散的速率是[瑞利耗散函数](@entry_id:165938)的两倍。这个关系对于一个拉格朗日量不显含时间的系统，也直接关联到[哈密顿量](@entry_id:172864) $H$ 的变化率 [@problem_id:2058074]。[哈密顿量](@entry_id:172864)在这种情况下等于总能量 $E$。因此：

$$
\frac{dH}{dt} = \frac{dE}{dt} = \sum_j Q_j^{\text{diss}} \dot{q}_j = -2\mathcal{F}
$$

由于耗散函数 $\mathcal{F}$（作为速度的二次型）通常是正定的，这意味着 $\frac{dH}{dt} \le 0$。[哈密顿量](@entry_id:172864)（能量）在[耗散力](@entry_id:166970)的作用下单调递减，直到系统达到一个速度为零或耗散为零的状态。

### [稳态](@entry_id:182458)运动与稳定性

在许多包含耗散和驱动的[非保守系统](@entry_id:166237)中，系统并不会简单地停止运动，而是会演化到一个**[稳态](@entry_id:182458) (steady-state)**。在[稳态](@entry_id:182458)下，由驱动力（如重力、外加策动力）提供的能量输入与[耗散力](@entry_id:166970)（如[摩擦力](@entry_id:171772)、阻力）消耗的能量输出[达到平衡](@entry_id:170346)。

#### 驱动力与[耗散力](@entry_id:166970)的平衡

一个清晰的例子是同时存在驱动力和[耗散力](@entry_id:166970)的系统，例如一个由“追随力”驱动的质点 [@problem_id:2067493]。考虑一个质量为 $m$ 的[质点](@entry_id:186768)被限制在长度为 $L$ 的杆上，在水平面内绕原点转动。它受到一个大小恒为 $P$ 的追随力，其方向与杆的夹角 $\alpha$ 恒定，同时受到线性空气阻力 $\mathbf{F}_d = -b\mathbf{v}$。追随力的切向分量 $P\sin\alpha$ 提供了一个驱动力矩 $\tau_P = L P \sin\alpha$。阻力产生的[耗散力](@entry_id:166970)矩为 $\tau_d = -L (b v_\theta) = -bL^2\omega$。系统的[转动动力学](@entry_id:267911)方程为 $I\dot{\omega} = \tau_{net}$，即：

$$
mL^2 \dot{\omega} = L P \sin\alpha - bL^2\omega
$$

当系统达到终端角速度 $\omega_{\text{terminal}}$ 时，角加速度 $\dot{\omega}=0$。此时，驱动力矩与[耗散力](@entry_id:166970)矩精确平衡：

$$
L P \sin\alpha - bL^2\omega_{\text{terminal}} = 0 \implies \omega_{\text{terminal}} = \frac{P\sin\alpha}{bL}
$$

这个[稳态](@entry_id:182458)[角速度](@entry_id:192539)是由驱动力（通过 $P\sin\alpha$）和耗散（通过 $b$）共同决定的。

在更复杂的系统中，例如受外力驱动的[阻尼振子](@entry_id:173004) [@problem_id:1265995]，[稳态](@entry_id:182458)表现为系统以驱动频率[振动](@entry_id:267781)，但其振幅和相位由系统的固有属性（质量、[弹簧常数](@entry_id:167197)）以及阻尼和驱动参数共同决定。在[稳态](@entry_id:182458)下，每个周期内驱动力对系统做的功恰好等于阻尼器耗散掉的能量。因此，[时间平均](@entry_id:267915)的[耗散功率](@entry_id:177328) $\langle P_{\text{diss}} \rangle$ 等于时间平均的输入功率 $\langle P_{\text{in}} \rangle$。

#### [稳态](@entry_id:182458)的稳定性

一个系统可能存在多个力或力矩为零的[平衡点](@entry_id:272705)，但并非所有[平衡点](@entry_id:272705)都是稳定的。一个**稳定**的[平衡点](@entry_id:272705)意味着，如果系统受到微小扰动偏离此状态，它会自发地返回该状态。反之，如果微小扰动导致系统进一步偏离，则该[平衡点](@entry_id:272705)是**不稳定**的。

考虑一个物体在具有复杂速度依赖性的[摩擦力](@entry_id:171772)作用下运动的情况，例如Stribeck摩擦，其[摩擦力](@entry_id:171772)可以模型化为 $F_f(v) = \beta v^2 - \alpha v + F_0$ [@problem_id:2067488]。当施加一个恒定的外力 $F_{app}$ 时，[牛顿第二定律](@entry_id:274217)为：

$$
m\frac{dv}{dt} = F_{app} - F_f(v) = F_{app} - (\beta v^2 - \alpha v + F_0)
$$

终端速度 $v_t$ 出现在加速度为零时，即 $F_{app} - F_f(v_t) = 0$，这导致一个关于 $v_t$ 的二次方程：

$$
\beta v_t^2 - \alpha v_t + (F_0 - F_{app}) = 0
$$

在给定条件 $\alpha^2 > 4\beta(F_0 - F_{app})$ 下，这个方程有两个正实数解，我们称之为 $v_1$ 和 $v_2$。哪一个才是物理上可观测到的稳定[终端速度](@entry_id:147799)呢？

我们可以通过[线性稳定性分析](@entry_id:154985)来判断。令[运动方程](@entry_id:170720)为 $m\dot{v} = g(v)$，其中 $g(v) = -\beta v^2 + \alpha v + (F_{app} - F_0)$。一个平衡速度 $v_t$ 是稳定的，条件是如果速度有微小偏离 $v = v_t + \epsilon$，[回复力](@entry_id:269582)会使 $\epsilon$ 减小。这等价于 $g'(v_t)  0$。计算导数：

$$
g'(v) = -2\beta v + \alpha
$$

因此，稳定条件是 $-2\beta v_t + \alpha  0$，即 $v_t > \frac{\alpha}{2\beta}$。二次方程的两个解为 $v_{1,2} = \frac{\alpha \pm \sqrt{\dots}}{2\beta}$。其中，较大的根 $v_t = \frac{\alpha + \sqrt{\alpha^2 - 4\beta(F_0 - F_{app})}}{2\beta}$ 满足 $v_t > \frac{\alpha}{2\beta}$，因此它是稳定的终端速度。而较小的根则是不稳定的[平衡点](@entry_id:272705)。这说明，即使在简单的[一维运动](@entry_id:190890)中，[非保守力](@entry_id:163431)也可能导致丰富的动力学行为，需要通过[稳定性分析](@entry_id:144077)来预测系统的最终状态。