## 引言
声音在介质中的传播是物理学中的一个经典课题，但当介质本身处于运动状态时——例如在大气中的风、海洋中的[洋流](@entry_id:185590)或飞机发动机的喷流中——声波的行为会变得异常复杂和有趣。经典声学理论大多基于静止介质的假设，这在许多重要工程和自然现象面前显得力不从心。本文旨在填补这一知识空白，系统地建立一个理解声波在运动流体中传播行为的理论框架。

本文将引导读者踏上一段从基础到前沿的探索之旅。在“原理与机制”一章中，我们将从[流体动力学](@entry_id:136788)的基本方程出发，推导出核心的[对流波动方程](@entry_id:181114)，并探讨流动如何影响[波的色散](@entry_id:275520)、速度和对称性，最终引出深刻的[声学](@entry_id:265335)时空类比。接下来，“应用与跨学科联系”一章将展示这些理论在航空[声学](@entry_id:265335)、天体物理学和地球物理学等领域的实际应用，揭示其强大的解释力和实用价值。最后，“动手实践”部分提供了一系列计算练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将全面掌握运动介质[声学](@entry_id:265335)的核心概念与分析方法。

## 原理与机制

本章旨在深入探讨声波在运动介质中传播的基本原理与核心机制。继前一章对该主题的背景介绍之后，我们将从基本控制方程出发，系统地推导和分析描述声传播的数学模型，并逐步揭示背景流场如何深刻地改变声[波的运动学](@entry_id:756646)、动力学及其对称性。内容将涵盖从基本的[对流波动方程](@entry_id:181114)到[高频近似](@entry_id:750288)下的[几何声学](@entry_id:188385)，再到[非线性](@entry_id:637147)效应和深刻的几何类比，为读者构建一个关于运动介质中[声学](@entry_id:265335)现象的坚实理论框架。

### 控制方程：[对流波动方程](@entry_id:181114)

我们研究的出发点是在均匀流动背景下，描述声扰动的基本[偏微分方程](@entry_id:141332)。考虑一个无粘、等熵的[理想流体](@entry_id:161909)。其运动由[连续性方程](@entry_id:195013)和[动量方程](@entry_id:197225)（[欧拉方程](@entry_id:177914)）支配：
$$ \frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{u}) = 0 $$
$$ \rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla) \mathbf{u} \right) = -\nabla p $$
其中 $\rho$ 是流体密度，$p$ 是压力，$\mathbf{u}$ 是[流体速度](@entry_id:267320)矢量。

我们假设总流场由一个均匀、稳定的背景流和一个小的声扰动叠加而成。背景流具有恒定的速度 $\mathbf{U}_0 = (U_0, 0, 0)$、密度 $\rho_0$ 和压力 $p_0$。声扰动由微小的速度 $\mathbf{u}'$、密度 $\rho'$ 和压力 $p'$ 表征。因此，总场为 $\mathbf{u} = \mathbf{U}_0 + \mathbf{u}'$, $\rho = \rho_0 + \rho'$, $p = p_0 + p'$。对于[等熵流](@entry_id:267193)动，压力扰动和[密度扰动](@entry_id:159546)通过静止介质中的声速 $c_0$ 相关联，即 $p' = c_0^2 \rho'$。进一步假设声扰动场是无旋的，因此速度扰动可以表示为一个[速度势](@entry_id:262992) $\phi$ 的梯度：$\mathbf{u}' = \nabla \phi$。

将这些关系代入[流体动力学](@entry_id:136788)方程并进行线性化（即忽略所有扰动量的二次及以上高阶项），我们可以推导出关于[速度势](@entry_id:262992) $\phi$ 的单一控制方程。线性化的连续性方程给出：
$$ \frac{\partial \rho'}{\partial t} + \mathbf{U}_0 \cdot \nabla \rho' + \rho_0 \nabla^2 \phi = 0 $$
线性化的动量方程，通过对 $\phi$ 的积分并忽略一个无关紧要的空间函数，可以得到：
$$ \frac{\partial \phi}{\partial t} + \mathbf{U}_0 \cdot \nabla \phi + \frac{p'}{\rho_0} = 0 $$
结合 $p' = c_0^2 \rho'$，我们可以用 $\phi$ 来表示 $\rho'$：
$$ \rho' = -\frac{\rho_0}{c_0^2}\left(\frac{\partial \phi}{\partial t} + U_0 \frac{\partial \phi}{\partial x}\right) $$
将此表达式代回线性化的连续性方程，我们便得到了描述声势在均匀流中传播的**[对流波动方程](@entry_id:181114)** ([@problem_id:627390])：
$$ \frac{1}{c_0^2}\left(\frac{\partial}{\partial t} + U_0 \frac{\partial}{\partial x}\right)^2 \phi - \nabla^2 \phi = 0 $$
展开后，方程写作：
$$ \frac{\partial^2 \phi}{\partial t^2} + 2U_0 \frac{\partial^2 \phi}{\partial t \partial x} + U_0^2 \frac{\partial^2 \phi}{\partial x^2} - c_0^2 \nabla^2 \phi = 0 $$
这个方程的核心特征是混合时空导数项 $\frac{\partial^2 \phi}{\partial t \partial x}$ 的出现，它明确地体现了背景流对声波的“拖曳”或“[对流](@entry_id:141806)”效应。这一项使得方程不再具有[洛伦兹不变性](@entry_id:155152)，声波的上游和下游传播行为将不再对称。

### [波的运动学](@entry_id:756646)：频散、[相速度与群速度](@entry_id:162723)

为了理解波在运动介质中的传播特性，我们考察[平面波解](@entry_id:195230) $\phi \propto \exp(i(\mathbf{k} \cdot \mathbf{r} - \omega t))$。将其代入[对流波动方程](@entry_id:181114)，可以得到连接角频率 $\omega$ 和波矢量 $\mathbf{k}$ 的**频散关系**：
$$ \omega - \mathbf{k} \cdot \mathbf{U}_0 = \pm c_0 |\mathbf{k}| $$
这个关系具有深刻的物理意义：在随流体运动的[参考系](@entry_id:169232)中，观察到的频率（即内在频率）$\omega' = \omega - \mathbf{k} \cdot \mathbf{U}_0$ 与波数 $k=|\mathbf{k}|$ 遵循经典关系 $\omega' = \pm c_0 k$。正负号代表了相对于流体向前和向后传播的波。这里的多普勒频移项 $\mathbf{k} \cdot \mathbf{U}_0$ 是理解运动介质声学的关键。

在运动介质中，波的[能量传播](@entry_id:202589)方向（由**群速度** $\mathbf{v}_g = \nabla_{\mathbf{k}} \omega$ 给出）通常与[波阵面](@entry_id:197956)[法线](@entry_id:167651)方向（由**相速度** $\mathbf{v}_p = (\omega/k^2)\mathbf{k}$ 给出）不同。利用上述频散关系，我们可以计算出[群速度](@entry_id:147686) ([@problem_id:586452])：
$$ \mathbf{v}_g = \nabla_{\mathbf{k}} (c_0 |\mathbf{k}| + \mathbf{k} \cdot \mathbf{U}_0) = c_0 \frac{\mathbf{k}}{|\mathbf{k}|} + \mathbf{U}_0 $$
这个结果非常直观：声能以声速 $c_0$ 相对于流体传播（方向沿波矢量 $\mathbf{k}$），同时被背景流以速度 $\mathbf{U}_0$ 整体平移。

这种[相速度与群速度](@entry_id:162723)方向上的差异导致了**声畸变**（acoustic aberration）现象。考虑一个位于均匀流中的静止声源，它发出的声波。设波法线方向 $\mathbf{k}$ 与流速方向 $\mathbf{U}_0$（设为 $x$ 轴）的夹角为 $\theta$，而声能传播方向（声线）$\mathbf{v}_g$ 与 $x$ 轴的夹角为 $\phi$。那么，这两个角度之间的关系可以通过群速度的分量来确定：
$$ \tan\phi = \frac{v_{g,y}}{v_{g,x}} = \frac{c_0 \sin\theta}{U_0 + c_0 \cos\theta} = \frac{\sin\theta}{M + \cos\theta} $$
其中 $M = U_0/c_0$ 是背景流的马赫数 ([@problem_id:586452])。这个公式表明，除非波沿上游或下游传播（$\theta=0$ 或 $\pi$），否则声线方向总是偏向下游。

### 界面处的波传播：广义[斯涅尔定律](@entry_id:162003)

当声波传播到一个介质界面时，例如两种不同流体之间的[剪切层](@entry_id:274623)，会发生反射和折射。在运动介质中，这些现象遵循一个广义的斯涅尔定律。考虑一个位于 $z=0$ 的平面，分隔着两种以不同速度 $V_1$ 和 $V_2$ 平行于 $x$ 轴运动的流体（声速分别为 $c_1, c_2$）。

波在界面上匹配的基本物理原则是：在界面两侧，观察到的频率 $\omega$ 以及平行于界面的[波矢](@entry_id:178620)量分量 $k_x$ 必须是连续的。这确保了在所有时间和界面上的所有点，[波的相位](@entry_id:171303)是匹配的。

利用这一连续性条件以及各向异性的频散关系 $(\omega - V k_x)^2 = c^2 (k_x^2 + k_z^2)$，我们可以推导出来自介质1的入射角 $\theta_i$ 与进入介质2的折射角 $\theta_t$ 之间的关系 ([@problem_id:592712])。经过推导，我们得到广义的[斯涅尔定律](@entry_id:162003)：
$$ \frac{\sin\theta_t}{\sin\theta_i} = \frac{c_2 / (1 - M_{2t})}{c_1 / (1 - M_{1t})} $$
其中 $M_{1t} = (V_1/c_1)\sin\theta_i$ 和 $M_{2t} = (V_2/c_2)\sin\theta_t$ 分别是流速在波[法线](@entry_id:167651)方向上的投影马赫数。一个更有用的形式是直接求解 $\sin\theta_t$：
$$ \sin\theta_t = \frac{c_2 \sin\theta_i}{c_1 + (V_1 - V_2)\sin\theta_i} $$
这个结果表明，折射角不仅取决于两种介质的声速比（如静态情况），还直接依赖于界面上的流速差（剪切）$V_1 - V_2$。这为控制声波传播路径提供了新的可能性。

### 高频极限：[几何声学](@entry_id:188385)与射线追踪

当波长远小于背景流场变化的特征尺度时，我们可以采用**[几何声学](@entry_id:188385)**（或 WKB）近似。在这种近似下，声能被认为沿着**声线**（rays）传播。这些声线的轨迹可以通过一个强大的[哈密顿力学](@entry_id:146202)框架来描述。

频散关系 $H(\mathbf{r}, \mathbf{k}) = \omega$ 被视为系统的[哈密顿量](@entry_id:172864)，其中 $\omega$ 在定常介质中是一个[守恒量](@entry_id:150267)（类似于能量）。声线的位置 $\mathbf{r}(t)$ 和波矢量 $\mathbf{k}(t)$ 的演化由[哈密顿方程](@entry_id:156213)给出 ([@problem_id:547706], [@problem_id:586512])：
$$ \frac{d\mathbf{r}}{dt} = \frac{\partial H}{\partial \mathbf{k}}, \quad \frac{d\mathbf{k}}{dt} = -\frac{\partial H}{\partial \mathbf{r}} $$
第一个方程定义了声线的速度，即[群速度](@entry_id:147686) $\mathbf{v}_g$。第二个方程描述了波矢量 $\mathbf{k}$ 如何因介质在空间上的不[均匀性](@entry_id:152612)（即 $c(\mathbf{r})$ 或 $\mathbf{v}(\mathbf{r})$ 的变化）而发生“[折射](@entry_id:163428)”。

作为一个重要的例子，考虑在声速 $c_0$ 恒定的流体中进行刚体旋转，其[速度场](@entry_id:271461)为 $\mathbf{v}(\mathbf{r}) = \mathbf{\Omega} \times \mathbf{r}$，其中 $\mathbf{\Omega}$ 是恒定的角速度矢量。此时的[哈密顿量](@entry_id:172864)为：
$$ H(\mathbf{r}, \mathbf{k}) = c_0 |\mathbf{k}| + (\mathbf{\Omega} \times \mathbf{r}) \cdot \mathbf{k} $$
应用哈密顿方程，我们可以得到波矢量的演化规律：
$$ \frac{d\mathbf{k}}{dt} = -\nabla_{\mathbf{r}} H = -\nabla_{\mathbf{r}} [(\mathbf{\Omega} \times \mathbf{r}) \cdot \mathbf{k}] = -(\mathbf{k} \times \mathbf{\Omega}) = \mathbf{\Omega} \times \mathbf{k} $$
这个方程表明，波矢量 $\mathbf{k}$ 会围绕角[速度矢量](@entry_id:269648) $\mathbf{\Omega}$ 发生进动。一个直接的推论是，$\mathbf{k}$ 的模长是守恒的，因为 $\frac{d|\mathbf{k}|}{dt} \propto \mathbf{k} \cdot \frac{d\mathbf{k}}{dt} = \mathbf{k} \cdot (\mathbf{\Omega} \times \mathbf{k}) = 0$ ([@problem_id:547706])。这意味着在均匀旋转的流体中，声波的波长沿着声线保持不变。我们可以利用这些守恒律和[哈密顿方程](@entry_id:156213)来精确追踪声线的轨迹 ([@problem_id:586512])。

### 守恒律与对称性

除了射线追踪，更一般的守恒律和对称性原理为我们理解[波的传播](@entry_id:144063)提供了深刻的见解。

#### 波作用量守恒
在随时间变化或不均匀的运动介质中，波的能量通常不守恒。然而，一个更为基本的量——**波作用量**（wave action）——在缓变介质中是守恒的。根据Whitham的平均拉格朗日理论，对于一个波包，波作用量密度 $N$ 和波作用量流 $\mathbf{F}_N$ 满足一个守恒方程：
$$ \frac{\partial N}{\partial t} + \nabla \cdot \mathbf{F}_N = 0 $$
波作用量密度定义为平均[拉格朗日量](@entry_id:174593) $\bar{\mathcal{L}}$ 对频率 $\omega$ 的偏导数, $N = \partial \bar{\mathcal{L}} / \partial \omega$。对于在背景流 $\mathbf{v}_0(\mathbf{x})$、密度 $\rho_0(\mathbf{x})$ 和声速 $c(\mathbf{x})$ 中传播的声波，其波作用量密度与波的振幅 $A$ 和内在频率 $\omega_0 = \omega - \mathbf{k} \cdot \mathbf{v}_0$ 直接相关 ([@problem_id:586431])：
$$ N \propto \frac{\rho_0 A^2 \omega_0}{c^2} $$
波作用量守恒是[声学](@entry_id:265335)和其他波物理学中的一个基本原理，它将波的振幅演化与背景介质的变化联系起来。

#### 互易原理
在[声学](@entry_id:265335)中，**互易原理**是一个强大的对称性原理。在静止介质中，它指出交换声源和接收器的位置不会改变测得的声场。然而，在运动介质中，由于流动的方向破坏了空间对称性，这种简单的互易性不再成立。

取而代之的是一个修正的**[空气动力学](@entry_id:193011)互易原理**。考虑一个任意的、定常、无旋的[亚音速流](@entry_id:192984)场 $\mathbf{v}_0(\mathbf{x})$。如果在位置 $\mathbf{x}_1$ 放置一个点源，在 $\mathbf{x}_2$ 处测得的声势为 $\phi_1(\mathbf{x}_2)$。现在，如果在**反向流场** $-\mathbf{v}_0(\mathbf{x})$ 中的 $\mathbf{x}_2$ 处放置同样类型的[点源](@entry_id:196698)，在 $\mathbf{x}_1$ 处测得的声势为 $\phi_2(\mathbf{x}_1)$。那么，互易原理表明 ([@problem_id:586442])：
$$ \frac{\phi_1(\mathbf{x}_2)}{q_1} = \frac{\phi_2(\mathbf{x}_1)}{q_2} $$
其中 $q_1, q_2$ 是源的强度。这个原理的证明依赖于[对流波动方程](@entry_id:181114)算子的伴随性质和[格林第二恒等式](@entry_id:169499)。它在声学测量、[源定位](@entry_id:755075)和[逆问题](@entry_id:143129)中有重要的应用。

### 高级主题与诠释

#### [非线性](@entry_id:637147)效应：[对流](@entry_id:141806)[伯格斯方程](@entry_id:177995)
当声波的振幅不再是微小量时，[非线性](@entry_id:637147)效应变得显著，可能导致波形变陡并最终形成激波。对于在均匀流中[单向传播](@entry_id:174820)的弱[非线性](@entry_id:637147)声波，其演化可以用**[对流](@entry_id:141806)[伯格斯方程](@entry_id:177995)**来描述 ([@problem_id:586461])。在一个随波移动的[坐标系](@entry_id:156346) $\xi = x - (v_0+c_0)t$ 中，速度扰动 $u'$ 的[演化方程](@entry_id:268137)为：
$$ \frac{\partial u'}{\partial \tau} + A u' \frac{\partial u'}{\partial \xi} - B \frac{\partial^2 u'}{\partial \xi^2} = 0 $$
其中 $\tau$ 是一个慢时间变量。这里的三个项分别代表了波形在慢时间尺度上的演化、[非线性](@entry_id:637147)陡峭化和[粘性耗散](@entry_id:143708)。对于理想气体，[非线性](@entry_id:637147)系数 $A = (\gamma+1)/2$，其中 $\gamma$ 是[比热容比](@entry_id:140850)。值得注意的是，这个系数与静止介质中的值完全相同。这表明，在主导阶上，背景流只是“搭载”着[非线性波](@entry_id:273091)一起传播，而基本的[非线性](@entry_id:637147)物理机制并未改变。

#### [非惯性系](@entry_id:168746)中的声学
在旋转等[非惯性参考系](@entry_id:169712)中分析声学问题时，必须在[动量方程](@entry_id:197225)中引入惯性力，如[科里奥利力](@entry_id:160096)和[离心力](@entry_id:173726)。考虑一个在惯性系中静止的流体，在一个以恒定角速度 $\mathbf{\Omega}$ 旋转的[参考系](@entry_id:169232)中观察它。在这个旋转系里，流体具有一个非平凡的背景速度场 $\mathbf{u}_0 = -\mathbf{\Omega} \times \mathbf{r}$。线性化的欧拉方程变为：
$$ \frac{\partial \mathbf{u}'}{\partial t} + 2\mathbf{\Omega} \times \mathbf{u}' + (\mathbf{u}_0 \cdot \nabla)\mathbf{u}' + (\mathbf{u}' \cdot \nabla)\mathbf{u}_0 = -\frac{1}{\rho_0} \nabla p' $$
科里奥利项 $2\mathbf{\Omega} \times \mathbf{u}'$ 会像[磁场](@entry_id:153296)作用于[电荷](@entry_id:275494)一样使声波路径弯曲，并引入新的波模态。即使在一个看似简单的[初始条件](@entry_id:152863)下，声压的演化也会因为这些惯性效应而变得相当复杂 ([@problem_id:586497])。

#### 几何类比：[声学](@entry_id:265335)时空
本章最深刻的观点之一是，[理想流体](@entry_id:161909)中的声波传播可以被精确地描述为在一个等效的弯曲时空中的[标量场](@entry_id:151443)传播。这个惊人的类比是**[模拟引力](@entry_id:144870)**（analogue gravity）领域的核心思想。

让我们从无粘、正压、无[旋流](@entry_id:153202)体的基本方程出发。通过对背景流 $(\rho_0, \mathbf{v}_0)$ 上的小扰动进行线性化，我们可以推导出[声学](@entry_id:265335)[速度势](@entry_id:262992) $\Psi_1$ 满足的[波动方程](@entry_id:139839) ([@problem_id:1865749])。经过一系列代数运算，这个方程可以被重写成一个优美的、具有协变形式的广义[波动方程](@entry_id:139839)：
$$ \frac{1}{\sqrt{-g}} \partial_\mu \left( \sqrt{-g} g^{\mu\nu} \partial_\nu \Psi_1 \right) = 0 $$
这个方程在形式上与广义相对论中无质量标量场在[弯曲时空](@entry_id:159822)中的传播方程完全相同。这里的 $g^{\mu\nu}$ 是所谓的**[声学度规](@entry_id:199206)**（acoustic metric）的逆。通过将[流体方程](@entry_id:195729)的推导结果与此形式对比，我们可以确定[声学度规](@entry_id:199206)的各个分量。它依赖于背景流体的性质：
$$ g^{\mu\nu}_{\text{acoustic}} \propto \begin{pmatrix} -1  -v_0^x  -v_0^y  -v_0^z \\ -v_0^x  c_s^2 - (v_0^x)^2  -v_0^x v_0^y  -v_0^x v_0^z \\ -v_0^y  -v_0^y v_0^x  c_s^2 - (v_0^y)^2  -v_0^y v_0^z \\ -v_0^z  -v_0^z v_0^x  -v_0^z v_0^y  c_s^2 - (v_0^z)^2 \end{pmatrix} $$
其中 $c_s$ 是当地声速，$\mathbf{v}_0 = (v_0^x, v_0^y, v_0^z)$ 是背景流速。这个度规的结构揭示了流场如何“塑造”声波所感受到的时空几何：流速 $\mathbf{v}_0$ 引入了时空[交叉](@entry_id:147634)项（$g^{0i} \neq 0$），这类似于[旋转黑洞](@entry_id:157805)引起的“[惯性系](@entry_id:266190)拖曳”效应；而流速和声速共同决定了空间部分的几何结构。

这个类比不仅仅是数学上的巧合。它开启了一扇窗，允许我们在流体实验中模拟和研究通常只在天体物理背景下出现的[引力](@entry_id:175476)现象，例如[黑洞](@entry_id:158571)的事件视界（当流速超过声速时，即 $v_0 > c_s$，形成[声学黑洞](@entry_id:157885)）和霍金辐射。因此，对运动介质中声传播的研究，最终将我们引向了现代物理学最前沿的交叉领域。