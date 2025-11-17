## 引言
在经典力学的宏伟殿堂中，[拉格朗日形式](@entry_id:145697)体系以其简洁和优雅独树一帜，它通过能量而非矢量力来描述物理系统的演化。然而，标准的[拉格朗日量](@entry_id:174593) $L = T - V$ 主要适用于[保守系统](@entry_id:167760)，这在现实世界中是一个巨大的局限，因为摩擦、空气阻力、外加驱动等[非保守力](@entry_id:163431)无处不在。那么，我们如何才能在保持[拉格朗日框架](@entry_id:751113)优雅性的同时，系统地处理这些复杂的力呢？答案便是**广义力**（Generalized Force）这一核心概念。广义力是连接理想化力学世界与复杂现实的桥梁，它为所有无法被纳入势能的力提供了一个统一的入口。

本文旨在全面而深入地剖析广义力。我们将从其最基本的定义出发，逐步揭示其在不同物理情境下的多样面貌和深刻内涵。
*   在**第一章“原理与机制”**中，我们将从虚功原理出发，严格定义广义力，并系统学习如何计算源于保守场、点作用力、耗散效应乃至[电磁场](@entry_id:265881)的各类广义力。
*   在**第二章“应用与跨学科联系”**中，我们将拓宽视野，探索广义力如何在[工程控制](@entry_id:177543)、机器人学、电磁学、[热力学](@entry_id:141121)和凝聚态物理等前沿领域中发挥关键作用，展示其强大的跨学科整合能力。
*   最后，在**第三章“动手实践”**部分，读者将通过解决具体的物理问题，将理论知识转化为实际的分析和计算技能。

通过本次学习，您将掌握一个强大的分析工具，它不仅能解决复杂的力学问题，更能让您领会到[分析力学](@entry_id:166738)作为一个统一理论框架的深刻魅力。

## 原理与机制

在[分析力学](@entry_id:166738)中，[拉格朗日形式](@entry_id:145697)体系通过[广义坐标](@entry_id:156576)和能量函数，为描述和预测物理系统的运动提供了一个优雅而强大的框架。[拉格朗日方程](@entry_id:175419)的核心思想是将系统受到的力分为两类：一类是**保守力**，它们可以通过一个标量[势能函数](@entry_id:200753) $V$ 来描述，并被内建于拉格朗日量 $L = T - V$ 之中；另一类则包含所有其余的力，例如[摩擦力](@entry_id:171772)、外加的驱动力或[非保守场](@entry_id:265048)力。这些力通过**广义力**（**generalized force**）$Q_j$ 的概念被引入[运动方程](@entry_id:170720)。本章旨在深入探讨广义力的基本原理和计算机制，揭示其在不同物理情境下的多样表现形式和深刻内涵。

### 广义力的定义

广义力的概念源于**[虚功原理](@entry_id:138749)**（**principle of virtual work**）。考虑一个由 $N$ 个[质点](@entry_id:186768)组成的系统，其位形由一组[广义坐标](@entry_id:156576) $\{q_1, q_2, \dots, q_n\}$ 完全描述。若系统发生一个无穷小的[虚位移](@entry_id:168781) $\{\delta q_1, \delta q_2, \dots, \delta q_n\}$，则第 $i$ 个[质点](@entry_id:186768)的位置矢量 $\mathbf{r}_i$ 将产生相应的[虚位移](@entry_id:168781) $\delta \mathbf{r}_i$。

$$
\delta \mathbf{r}_i = \sum_{j=1}^{n} \frac{\partial \mathbf{r}_i}{\partial q_j} \delta q_j
$$

假设有一组**主动力**（**active forces**）$\mathbf{F}_i$ 作用在各个[质点](@entry_id:186768)上（这些力不包括维持约束的内力），它们在[虚位移](@entry_id:168781)过程中所做的总[虚功](@entry_id:176403) $\delta W$ 为：

$$
\delta W = \sum_{i=1}^{N} \mathbf{F}_i \cdot \delta \mathbf{r}_i = \sum_{i=1}^{N} \mathbf{F}_i \cdot \left( \sum_{j=1}^{n} \frac{\partial \mathbf{r}_i}{\partial q_j} \delta q_j \right)
$$

通过交换求和顺序，我们可以将[虚功](@entry_id:176403)表示为[广义坐标](@entry_id:156576)[虚位移](@entry_id:168781)的[线性组合](@entry_id:154743)：

$$
\delta W = \sum_{j=1}^{n} \left( \sum_{i=1}^{N} \mathbf{F}_i \cdot \frac{\partial \mathbf{r}_i}{\partial q_j} \right) \delta q_j
$$

由此，我们定义与[广义坐标](@entry_id:156576) $q_j$ 共轭的**广义力** $Q_j$ 为：

$$
Q_j \equiv \sum_{i=1}^{N} \mathbf{F}_i \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}
$$

这个定义揭示了广义力的本质：它是主动力在由[广义坐标](@entry_id:156576) $q_j$ 的单位变化所引导的位移方向上的投影的加权和。值得注意的是，$Q_j$ 的量纲不一定是力。如果 $q_j$ 是长度，则 $Q_j$ 的量纲是力；如果 $q_j$ 是角度，则 $Q_j$ 的量纲是力矩。在任何情况下，乘积 $Q_j \delta q_j$ 的量纲始终是功或能量。

在[拉格朗日力学](@entry_id:147054)中，我们将所有不能由一个简单标量势能函数 $V$ 描述的力都归入广义力 $Q_j$ 的范畴。因此，完整的**[拉格朗日方程](@entry_id:175419)**写作：

$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_j}\right) - \frac{\partial L}{\partial q_j} = Q_j
$$

这里的 $Q_j$ 特指那些未包含在[拉格朗日量](@entry_id:174593) $L = T - V$ 中的**非保守广义力**或**外加广义力**。

### 源于[保守场](@entry_id:137555)的广义力

为了更好地理解广义力的概念，我们首先考察一个特例：当主动力 $\mathbf{F}_i$ 本身是保守的，即可以从一个总势能函数 $V(\mathbf{r}_1, \dots, \mathbf{r}_N)$ 导出，$\mathbf{F}_i = -\nabla_{\mathbf{r}_i} V$。在这种情况下，广义力 $Q_j$ 可以表示为：

$$
Q_j = \sum_{i=1}^{N} (-\nabla_{\mathbf{r}_i} V) \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}
$$

根据[多元函数](@entry_id:145643)求导的链式法则，上式右侧恰好是[势能](@entry_id:748988) $V$ 对[广义坐标](@entry_id:156576) $q_j$ 的偏导数的负值：

$$
Q_j = -\frac{\partial V}{\partial q_j}
$$

这表明，对于[保守力](@entry_id:170586)，我们有两种等效的处理方式：既可以将其势能 $V$ 包含在拉格朗日量中（$L=T-V$），此时方程右侧为零；也可以不将 $V$ 放入 $L$ 中（即 $L=T$），而是在方程右侧计入相应的广义力 $Q_j = -\frac{\partial V}{\partial q_j}$。这两种方法在数学上是完[全等](@entry_id:273198)价的，从而验证了广义力定义的自洽性。

我们通过一个具体的力学系统来阐明这一点。考虑一个质量为 $m$ 的质点，被约束在竖直平面内一根无摩擦的抛物线形金属丝上运动，其形状由方程 $z = ax^2$ 描述，其中 $z$ 轴竖直向上。系统仅受重力作用。如果我们选取质点的水平位置 $x$ 作为[广义坐标](@entry_id:156576)，那么其位置矢量可以写为 $\mathbf{r} = x\hat{i} + ax^2\hat{k}$。重力 $\mathbf{F}_g = -mg\hat{k}$ 是保守力，其势能为 $V = mgz = mgax^2$。

根据[势能](@entry_id:748988)求导的方法，与坐标 $x$ 共轭的广义力为 [@problem_id:2053512]：

$$
Q_x = -\frac{\partial V}{\partial x} = -\frac{\partial}{\partial x}(mgax^2) = -2mgax
$$

我们也可以通过[虚功原理](@entry_id:138749)来验证这个结果。质点的[虚位移](@entry_id:168781)为 $\delta\mathbf{r} = \frac{\partial \mathbf{r}}{\partial x}\delta x = (\hat{i} + 2ax\hat{k})\delta x$。重力所做的[虚功](@entry_id:176403)为 $\delta W = \mathbf{F}_g \cdot \delta\mathbf{r} = (-mg\hat{k}) \cdot (\hat{i} + 2ax\hat{k})\delta x = -2mgax \delta x$。根据定义 $\delta W = Q_x \delta x$，我们得到完全相同的结果 $Q_x = -2mgax$。这个结果直观地反映了在抛物线[轨道](@entry_id:137151)的不同位置，重力驱动质点运动的“有效分量”是如何随 $x$ 变化的。

这个思想同样适用于刚体。考虑一根质量为 $M$、长度为 $L$ 的均匀刚性板，其一端靠在光滑的竖直墙壁上，另一端置于光滑的水平地面上。我们可以用板与地面之间的夹角 $\theta$ 作为[广义坐标](@entry_id:156576)。对于均匀刚体，重力的作用点可以等效为其质心。板的[质心](@entry_id:265015)高度为 $y_{\text{cm}} = \frac{L}{2}\sin\theta$。因此，系统的引力势能为 $V(\theta) = Mgy_{\text{cm}} = \frac{MgL}{2}\sin\theta$。由此产生的广义力（在此例中是广义力矩）为 [@problem_id:2095415]：

$$
Q_{\theta} = -\frac{\partial V}{\partial \theta} = -\frac{MgL}{2}\cos\theta
$$

当 $\theta$ 趋近于 $\pi/2$ 时（板接近竖直），$Q_{\theta}$ 趋近于零，符合直觉；当 $\theta$ 趋近于零时（板接近水平），$Q_{\theta}$ 的[绝对值](@entry_id:147688)最大，表明此时重力产生使其转动的效果最强。

### 点作用力与纯力矩

在更复杂的系统中，力可能以多种形式施加。广义力的定义 $Q_j = \sum_i \mathbf{F}_i \cdot \frac{\partial \mathbf{r}_i}{\partial q_j}$ 对于作用在特定点上的力尤其重要。然而，当系统受到一个直接与某个[广义坐标](@entry_id:156576)（通常是角度）共轭的**纯力矩**（**pure torque**）时，情况会大大简化。如果一个力矩 $\tau$ 的作用是直接改变角度坐标 $\theta$，那么它对广义力 $Q_{\theta}$ 的贡献就是 $\tau$ 本身（如果力矩方向与 $\theta$ 增大的方向一致）或 $-\tau$（如果方向相反）。

一个双连杆机器人臂的例子能够清晰地展示这两种情况的区别。设想一个在水平面内运动的机器人臂，由两个长度分别为 $L_1$ 和 $L_2$ 的连杆组成。其位形由两个[广义坐标](@entry_id:156576)描述：$\theta_1$ 是第一个连杆与 $x$ 轴的夹角，$\theta_2$ 是第二个连杆相对于第一个连杆延长线的夹角。假设在肘关节处有一个电机，施加一个大小为 $\tau_0$ 的恒定力矩，试图增大 $\theta_2$。同时，在第二个连杆的中点处，有一个小型推进器，提供一个大小为 $F_0$ 的恒定推力，其方向始终平行于第一个连杆。

要确定总的广义力 $Q_{\theta_1}$ 和 $Q_{\theta_2}$，我们需要分别考虑电机和推进器的贡献 [@problem_id:2053539]。
1.  **电机的贡献**：电机力矩 $\tau_0$ 直接作用于改变 $\theta_2$，因此它对 $Q_{\theta_2}$ 的贡献为 $+\tau_0$，而对 $Q_{\theta_1}$ 没有直接贡献。
2.  **推进器的贡献**：推进力 $\mathbf{F}$ 作用在第二个连杆的中点 $P$ 上。我们需要计算出点 $P$ 的位置矢量 $\mathbf{r}_P$ 关于 $\theta_1$ 和 $\theta_2$ 的偏导数。经过详细的矢量运算可以发现，这个力对两个广义力都有贡献：
    $$
    Q_{\theta_1}^{(F)} = \mathbf{F} \cdot \frac{\partial \mathbf{r}_P}{\partial \theta_1} = -\frac{F_0 L_2}{2}\sin\theta_2
    $$
    $$
    Q_{\theta_2}^{(F)} = \mathbf{F} \cdot \frac{\partial \mathbf{r}_P}{\partial \theta_2} = -\frac{F_0 L_2}{2}\sin\theta_2
    $$
    这个结果颇具启发性：一个方向仅依赖于 $\theta_1$ 的力，由于其作用点同时依赖于 $\theta_1$ 和 $\theta_2$，最终对两个广义力都产生了影响。

将两部分贡献相加，我们得到总的广义力：

$$
\begin{pmatrix} Q_{\theta_1} & Q_{\theta_2} \end{pmatrix} = \begin{pmatrix} -\frac{F_0 L_2}{2}\sin\theta_2 & \tau_0 - \frac{F_0 L_2}{2}\sin\theta_2 \end{pmatrix}
$$

这个例子凸显了在处理多自由度系统时，严格应用广义力定义的重要性。

### [非保守力](@entry_id:163431)与速度依赖力

广义力概念真正的威力体现在处理那些无法用[势能函数](@entry_id:200753)描述的力，例如[摩擦力](@entry_id:171772)、阻力以及某些[电磁力](@entry_id:196024)。

#### [耗散力](@entry_id:166970)

**[耗散力](@entry_id:166970)**（**dissipative forces**）如[流体阻力](@entry_id:262242)或[摩擦力](@entry_id:171772)，通常依赖于物体的速度，并将机械能转化为热能。一个典型的例子是浸在[粘性流](@entry_id:136330)体中的单摆。假设一个质量为 $m$、长度为 $L$ 的单摆，在运动时受到与速度成正比的阻力 $\mathbf{F}_d = -b\mathbf{v}$，其中 $b$ 是阻尼系数。

我们使用摆角 $\theta$（与竖直向下的稳定[平衡位置](@entry_id:272392)的夹角）作为[广义坐标](@entry_id:156576)。[质点](@entry_id:186768)的位置矢量为 $\mathbf{r}(\theta) = L(\sin\theta\hat{i} - \cos\theta\hat{j})$。其速度为 $\mathbf{v} = \frac{d\mathbf{r}}{dt} = \frac{\partial \mathbf{r}}{\partial \theta}\dot{\theta}$。阻力产生的广义力 $Q_{\theta}$ 为 [@problem_id:2053730]：

$$
Q_{\theta} = \mathbf{F}_d \cdot \frac{\partial \mathbf{r}}{\partial \theta} = (-b\mathbf{v}) \cdot \frac{\partial \mathbf{r}}{\partial \theta} = -b\left(\frac{\partial \mathbf{r}}{\partial \theta}\dot{\theta}\right) \cdot \frac{\partial \mathbf{r}}{\partial \theta} = -b \left|\frac{\partial \mathbf{r}}{\partial \theta}\right|^2 \dot{\theta}
$$

对于单摆，$\left|\frac{\partial \mathbf{r}}{\partial \theta}\right| = L$，因此我们得到：

$$
Q_{\theta} = -bL^2\dot{\theta}
$$

这个结果表明，线性的速度阻力 $\mathbf{F}_d \propto \mathbf{v}$ 转化为了线性的[广义速度](@entry_id:178456)阻力 $Q_{\theta} \propto \dot{\theta}$。这是一个普遍的结论，对于许多常见的[耗散力](@entry_id:166970)形式都成立。

#### 速度依赖力：[洛伦兹力](@entry_id:145104)

[磁场](@entry_id:153296)对运动[电荷](@entry_id:275494)施加的**[洛伦兹力](@entry_id:145104)**（**Lorentz force**）$\mathbf{F}_m = q(\mathbf{v} \times \mathbf{B})$ 是另一种重要的速度依赖力。一个显著的特点是，洛伦兹力始终垂直于粒子的速度，因此它**不做功**（$\mathbf{F}_m \cdot \mathbf{v} = 0$）。然而，它所对应的广义力 $Q_j = \mathbf{F}_m \cdot \frac{\partial \mathbf{r}}{\partial q_j}$ 通常不为零。这是因为[虚位移](@entry_id:168781) $\delta \mathbf{r}_j = \frac{\partial \mathbf{r}}{\partial q_j}\delta q_j$ 的方向一般与实际的速度矢量 $\mathbf{v}$ 不同。

考虑一个[电荷](@entry_id:275494)为 $q$ 的粒子在沿 $z$ 轴的均匀[磁场](@entry_id:153296) $\mathbf{B} = B_0\hat{k}$ 中运动。我们采用球坐标 $(r, \theta, \phi)$ 来描述其位置。我们想求出与方位角 $\phi$ 共轭的广义力 $Q_{\phi}$。

首先，我们需要用球坐标[基矢](@entry_id:199546)表达速度 $\mathbf{v}$ 和[磁场](@entry_id:153296) $\mathbf{B}$，然后计算叉乘积 $\mathbf{v} \times \mathbf{B}$ 得到洛伦兹力 $\mathbf{F}_m$。接着，我们计算位置矢量对 $\phi$ 的偏导数 $\frac{\partial \mathbf{r}}{\partial \phi} = r\sin\theta\hat{e}_{\phi}$。最后，将二者做[点积](@entry_id:149019)。经过一系列的[矢量代数](@entry_id:152340)运算，我们得到 [@problem_id:2053769]：

$$
Q_{\phi} = \mathbf{F}_m \cdot \frac{\partial \mathbf{r}}{\partial \phi} = -qB_0 (r\dot{r}\sin^2\theta + r^2\dot{\theta}\sin\theta\cos\theta)
$$

这个广义力依赖于坐标 $r, \theta$ 和[广义速度](@entry_id:178456) $\dot{r}, \dot{\theta}$，但有趣的是它不依赖于与它共轭的速度 $\dot{\phi}$。洛伦兹力虽然不做功，但它通过改变动量的方向，其效应在[拉格朗日方程](@entry_id:175419)中通过这样一个复杂的广义力形式体现出来。

### 更广阔背景下的广义力

广义力的概念远不止局限于经典力学中的[非保守力](@entry_id:163431)，它可以被推广到更广泛的物理领域，如[变质量系统](@entry_id:177386)、电磁学和统计物理学。

#### 开放系统：变质量问题

标准的[拉格朗日力学](@entry_id:147054)是为质量守恒的封闭系统建立的。对于像火箭这样通过喷射工质来获得推力的**[变质量系统](@entry_id:177386)**，我们可以巧妙地利用广义力来处理。我们将火箭主体视为一个质量为 $m(t)$ 的[质点](@entry_id:186768)，其拉格朗日量为 $L = \frac{1}{2}m(t)\dot{z}^2 - m(t)gz$。然后，我们将由于质量变化引起的[动量通量](@entry_id:199796)效应全部归入一个广义力 $Q_z$ 中。

通过计算[拉格朗日方程](@entry_id:175419)的左侧 $\frac{d}{dt}(\frac{\partial L}{\partial \dot{z}}) - \frac{\partial L}{\partial z} = m\ddot{z} + \dot{m}\dot{z} + mg$，并将其与由牛顿第二定律导出的[火箭方程](@entry_id:274435) $m\ddot{z} = F_{\text{thrust}} - mg = -u_{\text{ex}}\dot{m} - mg$ 相比较（其中 $u_{\text{ex}}$ 是相对于火箭的恒定排气速率，$\dot{m}0$），我们可以反解出广义力 $Q_z$ [@problem_id:2053515]：

$$
Q_z = m\ddot{z} + \dot{m}\dot{z} + mg = (-u_{\text{ex}}\dot{m} - mg) + \dot{m}\dot{z} + mg = \dot{m}(\dot{z} - u_{\text{ex}})
$$

这个广义力代表了因物质流出系统而产生的等效作用力，它与质量变化率 $\dot{m}$ 以及排出的气体在[惯性系](@entry_id:266190)中的速度 $(\dot{z} - u_{\text{ex}})$ 有关。

#### 源于[热力学](@entry_id:141121)和[电磁势](@entry_id:266145)的力

广义力的思想可以自然地推广到非机械系统。力可以被看作是能量对某个[广义坐标](@entry_id:156576)的导数。

一个经典的电磁学例子是插入平行板电容器中的[电介质](@entry_id:147163)板。考虑一个极板面积为 $w \times L$、间距为 $d$ 的[电容器](@entry_id:267364)，连接到恒定电压为 $V_0$ 的电源上。一块[介电常数](@entry_id:146714)为 $\kappa$ 的[电介质](@entry_id:147163)板被插入了距离 $x$。系统总希望通过吸引[电介质](@entry_id:147163)来降低其总能量。然而，在恒定电压下，当[电介质](@entry_id:147163)板移动时，电池会做功来维持电压，因此不能简单地使用储存的[电场](@entry_id:194326)能 $U_E = \frac{1}{2}CV^2$ 来计算力。

正确的做法是考虑包含电池在内的整个系统的[能量守恒](@entry_id:140514)。当[电介质](@entry_id:147163)板移动 $dx$ 时，电容 $C(x)$ 改变 $dC$。电池做的功为 $dW_{\text{batt}} = V_0 dQ = V_0^2 dC$。[电场](@entry_id:194326)储能的变化为 $dU_E = \frac{1}{2}V_0^2 dC$。根据[能量守恒](@entry_id:140514)，电池做的功等于系统[储能](@entry_id:264866)的增加和对外（拉动[电介质](@entry_id:147163)板的力）所做的机械功之和：$dW_{\text{batt}} = dU_E + dW_{\text{mech}}$。因此，外力做的功为 $dW_{\text{mech}} = F_x dx = \frac{1}{2}V_0^2 dC$。由此得到吸[引力](@entry_id:175476)的大小为 [@problem_id:2053523]：

$$
F_x = \frac{1}{2}V_0^2 \frac{dC}{dx}
$$

通过计算电容 $C(x) = \frac{\epsilon_0 w}{d}(L + (\kappa-1)x)$，我们发现吸[引力](@entry_id:175476) $F_x = \frac{\epsilon_0 w V_0^2}{2d}(\kappa-1)$ 是一个不依赖于插入距离 $x$ 的恒力。这展示了如何通过[广义坐标](@entry_id:156576)下的能量变化来定义和计算非机械来源的力。

另一个更深刻的例子来自[统计力](@entry_id:194984)学。一些力，如[高分子](@entry_id:150543)聚合物的弹性，其本质并非来自原子间的[势能](@entry_id:748988)变化，而是源于熵。考虑一个理想化的橡皮筋，其熵 $S$ 与其端到端长度 $L$ 的关系为 $S(L) = C - \frac{3 k_B L^2}{2 N b^2}$，其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$T$ 是绝对温度，$N$ 和 $b$ 是聚合物链的微观参数。在恒定温度下，系统倾向于最大化熵，这表现为一种宏观上的收缩趋势，即“**[熵力](@entry_id:137746)**”（**entropic force**）。

在[热力学](@entry_id:141121)中，与可逆功相关联的能量函数是[亥姆霍兹自由能](@entry_id:136442) $F = U - TS$。对于这种理想橡皮筋，其内能 $U$ 与长度无关，因此其有效势能可以视为 $V_{\text{eff}}(L) = F(L) = \text{const} + \frac{3k_B T}{2Nb^2}L^2$。这等价于一个劲度系数 $k = \frac{3k_B T}{Nb^2}$ 的胡克定律弹簧，其弹性与[绝对温度](@entry_id:144687)成正比！

如果我们把这样一个橡皮筋连接在力学系统上，例如连接在竖直旋转[圆环](@entry_id:163678)顶端和环上一个质量为 $m$ 的珠子之间，我们就可以计算它产生的广义力。设珠子位置由其从顶端算起的角度 $\theta$ 描述，橡皮筋的长度 $L(\theta) = 2R\sin(\theta/2)$。那么，[熵力](@entry_id:137746)产生的广义力为 [@problem_id:2053536]：

$$
Q_{\theta} = -\frac{\partial V_{\text{eff}}}{\partial \theta} = -\frac{\partial V_{\text{eff}}}{\partial L}\frac{dL}{d\theta} = -\left(\frac{3k_B T L}{Nb^2}\right) \left(R\cos\frac{\theta}{2}\right) = -\frac{3 k_B T R^2}{N b^2}\sin\theta
$$

这个例子完美地展示了[拉格朗日力学](@entry_id:147054)的普适性，它能够将源于微观统计行为的宏观效应无缝地整合到力学方程中。

### 作为未知量的广义力

最后，广义力还提供了一种强大的分析工具：当一个系统的运动轨迹被预先指定时，我们可以利用[拉格朗日方程](@entry_id:175419)来求解维持该运动所**必需**的外加广义力。在这种情况下，$Q_j$ 成为了方程中的未知量。

设想一个粒子在半角为 $\alpha$ 的无摩擦圆锥内表面运动。除了重力和一条连接顶点与粒子的弹簧力外，还有一个外部作用源施加额外的力，迫使粒子以恒定的[径向速度](@entry_id:159824) $v_0$（沿锥面远离顶点的速度）和恒定的角速度 $\omega_0$ 运动。我们想知道为了维持这种特定的螺旋运动，外部作用源必须提供多大的方位角方向的广义力 $Q_{\phi}$。

我们采用沿锥面的距离 $r$ 和[方位角](@entry_id:164011) $\phi$ 作为[广义坐标](@entry_id:156576)。由于保守力（重力和弹簧力）的势能都与 $\phi$ 无关，它们对 $Q_{\phi}$ 没有贡献，$\frac{\partial L}{\partial \phi} = 0$。因此，[拉格朗日方程](@entry_id:175419)的 $\phi$ 分量简化为：

$$
Q_{\phi} = \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{\phi}}\right) = \frac{d}{dt}\left(\frac{\partial T}{\partial \dot{\phi}}\right)
$$

系统的动能为 $T = \frac{1}{2}m(\dot{r}^2 + (r\sin\alpha)^2\dot{\phi}^2)$。计算可得 $\frac{\partial T}{\partial \dot{\phi}} = m r^2 \sin^2\alpha \dot{\phi}$。将其对时间求导，并代入指定的运动条件 $\dot{r}=v_0$ 和 $\dot{\phi}=\omega_0$（这意味着 $\ddot{\phi}=0$），我们得到 [@problem_id:2053513]：

$$
Q_{\phi} = \frac{d}{dt}(m r^2 \sin^2\alpha \, \omega_0) = m \sin^2\alpha \, \omega_0 (2r\dot{r}) = 2mrv_0\omega_0\sin^2\alpha
$$

这个结果就是外部作用源必须提供的广义力矩，用以抵消因半径 $r$ 增加而导致的转动惯量增加，从而维持角速度 $\omega_0$ 不变。这一应用在控制理论和机器人学中至关重要，它允许工程师计算驱动复杂系统按预定轨迹运动所需的控制力或力矩。

综上所述，广义力是[拉格朗日力学](@entry_id:147054)中的一个核心概念。它不仅为处理[非保守力](@entry_id:163431)和速度依赖力提供了系统性的方法，而且作为一个高度灵活的工具，将力学与电磁学、[热力学](@entry_id:141121)和控制理论等领域紧密联系起来，展现了[分析力学](@entry_id:166738)框架的强大威力与深远影响。