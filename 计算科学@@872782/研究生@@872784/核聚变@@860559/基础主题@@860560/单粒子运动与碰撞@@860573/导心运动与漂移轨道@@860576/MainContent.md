## 引言
在[磁约束](@entry_id:161852)核聚变等离子体这样由数万亿[带电粒子](@entry_id:160311)组成的复杂系统中，精确追踪每个粒子的运动轨迹是一项不可能完成的任务。然而，理解单个粒子的行为是掌握等离子体宏观约束与输运特性的基石。[导心运动](@entry_id:202625)理论正是为了解决这一挑战而发展的核心物理模型，它将粒子在强[磁场](@entry_id:153296)中看似杂乱无章的螺旋轨迹，巧妙地简化为一系列可分析的、更慢时间尺度上的运动分量。本文旨在为读者系统性地构建对[导心运动](@entry_id:202625)与漂移[轨道](@entry_id:137151)的深入理解。

本文内容遵循一个从基本原理到复杂应用的逻辑结构。在“原理与机制”一章中，我们将深入探讨[导心近似](@entry_id:750090)的物理基础，阐释磁矩[不变量](@entry_id:148850)的深刻含义，并推导由[电场](@entry_id:194326)、[磁场](@entry_id:153296)梯度和曲率等引起的各种关键漂移。接着，在“应用与跨学科联系”一章中，我们会将这些理论应用于分析真实[磁约束](@entry_id:161852)装置（如磁镜和[托卡马克](@entry_id:182005)）中的[粒子约束](@entry_id:148454)问题，揭示理论与工程实践的紧密联系。最后，通过“动手实践”部分，您将有机会运用所学知识解决具体的物理问题，从而巩固和深化您的理解。通过这一学习路径，您将掌握分析[磁化等离子体](@entry_id:201225)中[带电粒子](@entry_id:160311)动力学的基本工具，为进一步研究等离子体物理和受控[核聚变](@entry_id:139312)打下坚实的基础。

## 原理与机制

在[磁约束聚变](@entry_id:180408)等离子体中，单个[带电粒子](@entry_id:160311)的运动轨迹极其复杂。在强[磁场](@entry_id:153296)作用下，粒子被约束在磁力线附近，进行快速的[回旋运动](@entry_id:204632)，同时沿着磁力线运动，并缓慢地垂直于磁力线漂移。直接求解洛伦兹力方程来描述数万亿个粒子的行为是不现实的。因此，我们需要一个简化但足够精确的物理模型。本章的目标是系统地阐述[导心运动](@entry_id:202625)理论的基本原理和关键机制，将复杂的[粒子轨迹](@entry_id:204827)分解为几个更简单、更直观的运动分量：快速的[回旋运动](@entry_id:204632)、沿磁力线的平行运动，以及缓慢的[导心漂移](@entry_id:162721)。

### [导心近似](@entry_id:750090)

[导心近似](@entry_id:750090)（guiding-center approximation）是描述磁化等离子体中[带电粒子运动](@entry_id:262424)的基石。其核心思想是将粒子的瞬时位置 $\mathbf{r}$ 分解为一个快速[振荡](@entry_id:267781)的[回旋运动](@entry_id:204632)分量 $\boldsymbol{\rho}$ 和一个缓慢演化的“导向中心”（或简称“[导心](@entry_id:200181)”）位置 $\mathbf{R}$ 的叠加，即 $\mathbf{r} = \mathbf{R} + \boldsymbol{\rho}$。[导心](@entry_id:200181)实质上是粒子[回旋运动](@entry_id:204632)的平均中心，它的轨迹描绘了粒子在宏观时空尺度上的运动。

这种运动分解的有效性，依赖于对系统内不同物理过程的空间和时间尺度进行严格的排序。[@problem_id:3690493]

首先，在**空间尺度**上，我们要求粒子的**[拉莫尔半径](@entry_id:197083)**（Larmor radius） $\rho$ 远小于[磁场](@entry_id:153296)发生显著变化的特征长度 $L$。[拉莫尔半径](@entry_id:197083)是粒子回旋[轨道](@entry_id:137151)的半径，定义为 $\rho = v_{\perp}/\Omega$，其中 $v_{\perp}$ 是粒子垂直于[磁场](@entry_id:153296)的速度分量，$\Omega = |q|B/m$ 是粒子的**[回旋频率](@entry_id:156231)**（cyclotron frequency），$q$ 和 $m$ 分别是粒子的[电荷](@entry_id:275494)和质量，$B$ 是磁场强度。[磁场](@entry_id:153296)的特征变化尺度 $L$ 通常由 $L \sim B/|\nabla B|$ 定义。因此，[导心近似](@entry_id:750090)成立的首要条件是存在一个小参数 $\epsilon = \rho/L \ll 1$。这个条件确保了粒子在一次[回旋运动](@entry_id:204632)中经历的[磁场](@entry_id:153296)近似是均匀的，从而使得回旋运动可以被清晰地定义并从总运动中分离出来。

其次，在**时间尺度**上，我们要求回旋周期（$\sim \Omega^{-1}$）远小于[磁场](@entry_id:153296)本身或其他外部作用发生显著变化的时间尺度 $\tau_{\mathrm{var}}$。$\tau_{\mathrm{var}}$ 的定义为 $|\partial \mathbf{B}/\partial t|/B \sim 1/\tau_{\mathrm{var}}$。这一要求，即 $\Omega^{-1} \ll \tau_{\mathrm{var}}$，保证了在单个回旋周期内，[磁场](@entry_id:153296)是准静态的，使得[回旋运动](@entry_id:204632)的参数（如[拉莫尔半径](@entry_id:197083)和回旋频率）保持近似恒定，从而可以在一个回旋周期上进行有效的平均。此外，[导心](@entry_id:200181)自身的运动（如在[磁镜](@entry_id:204158)中的弹跳运动或在[环形装置](@entry_id:188972)中的漂移[轨道](@entry_id:137151)）也具有一个更慢的[轨道](@entry_id:137151)时间尺度 $T_{\mathrm{orbit}}$。一个清晰的[尺度分离](@entry_id:270204)层次应该是：

$ \Omega^{-1} \ll \tau_{\mathrm{var}} \ll T_{\mathrm{orbit}} $

这个完整的时空尺度排序构成了[导心近似](@entry_id:750090)的物理基础。在这种排序下，由[磁场](@entry_id:153296)不均匀性引起的[导心漂移](@entry_id:162721)速度 $v_{\mathrm{drift}}$ 通常远小于粒子的总速度 $v$，其量级关系为 $v_{\mathrm{drift}}/v \sim \epsilon = \rho/L$。

### 运动的基本分量

在[导心近似](@entry_id:750090)的框架下，粒子的复杂运动可以被分解为三个基本组成部分：[回旋运动](@entry_id:204632)、平行运动和垂直于[磁场](@entry_id:153296)的漂移运动。

#### [回旋运动](@entry_id:204632)与磁矩[不变量](@entry_id:148850)

最快的运动是粒子围绕磁力线的**回旋运动**（gyromotion）。在一个近似均匀的[磁场](@entry_id:153296)中，这是一个频率为 $\Omega$、半径为 $\rho$ 的圆周运动。这个快速[振荡](@entry_id:267781)的运动本身并不导致粒子的宏观输运，但它与[磁场](@entry_id:153296)不[均匀性](@entry_id:152612)的相互作用是产生漂移的关键。

在[导心近似](@entry_id:750090)成立的条件下，存在一个近似守恒的物理量，即**[第一绝热不变量](@entry_id:184749)**（first adiabatic invariant），也称为**磁矩**（magnetic moment） $\mu$。其定义为：

$ \mu = \frac{m v_{\perp}^2}{2B} $

$\mu$ 的守恒意味着，当一个粒子移动到[磁场强度](@entry_id:197932)不同的区域时，它的垂直动能 $K_{\perp} = \frac{1}{2}mv_{\perp}^2$ 会随磁场强度 $B$ 成比例地变化，以保持 $\mu$ 不变。这是[粒子物理学](@entry_id:145253)中最重要和最有用的概念之一。

#### 平行运动与[磁镜效应](@entry_id:171262)

粒子的第二个运动分量是沿着磁力线的**平行运动**（parallel motion）。由于[磁场](@entry_id:153296)对平行于其方向的运动不施加洛伦兹力，因此在没有[电场](@entry_id:194326)或其他力的情况下，粒子会以速度 $v_{\parallel}$ 沿磁力线自由运动。

然而，当磁场强度沿磁力线变化时，情况变得有趣起来。根据[能量守恒](@entry_id:140514) $E = \frac{1}{2}m(v_{\parallel}^2 + v_{\perp}^2) = \text{const}$ 和磁矩守恒 $mv_{\perp}^2 / (2B) = \mu = \text{const}$，我们可以推导出平行运动的有效[一维运动](@entry_id:190890)方程。将 $v_{\perp}^2 = 2\mu B/m$ 代入[能量守恒方程](@entry_id:748978)，我们得到：

$ E = \frac{1}{2}mv_{\parallel}^2 + \mu B(s) $

其中 $s$ 是沿磁力线的[弧长](@entry_id:191173)坐标。这个方程形式上等同于一个质量为 $m$ 的粒子在[有效势能](@entry_id:171609) $U(s) = \mu B(s)$ 中的[一维运动](@entry_id:190890)。

作用在[导心](@entry_id:200181)上的平行力，即**[磁镜](@entry_id:204158)力**（mirror force），是该有效势能的负梯度：

$ F_{\parallel} = -\nabla_{\parallel} U(s) = -\mu \frac{dB}{ds} $

这个力总是将粒子推向[磁场](@entry_id:153296)较弱的区域。因此，如果一个粒子朝着[磁场](@entry_id:153296)增强的方向运动，它的平行速度 $v_{\parallel}$ 会减小（因为 $v_{\perp}$ 必须增大以保持 $\mu$ 不变）。如果[磁场](@entry_id:153296)足够强，粒子的平行速度可以减小到零，此时粒子将被“反射”，向着[磁场](@entry_id:153296)减弱的方向运动。这种现象被称为**[磁镜效应](@entry_id:171262)**（magnetic mirroring），是[磁约束](@entry_id:161852)装置（如磁镜和托卡马克）中[粒子约束](@entry_id:148454)的基本机制。

我们可以通过一个具体的例子来量化这种沿磁力线的往复运动，即**弹跳运动**（bounce motion）。考虑一个粒子在[磁场](@entry_id:153296)极小值 $B_0$ 附近运动，[磁场](@entry_id:153296)[分布](@entry_id:182848)近似为抛物线形：$B(s) = B_0(1 + s^2/L^2)$，其中 $L$ 是[磁场](@entry_id:153296)变化的特征长度。[@problem_id:3701424] [@problem_id:3701420] 粒子在 $s=0$ 处具有总能量 $E$ 和速度与[磁场](@entry_id:153296)方向的夹角（**[螺距](@entry_id:188083)角**，pitch angle） $\vartheta_0$。

根据之前的推导，平行[运动方程](@entry_id:170720)为 $m \frac{d^2s}{dt^2} = F_{\parallel} = -\mu \frac{dB}{ds}$。
首先，我们用初始条件确定磁矩 $\mu$：
$ \mu = \frac{m v_{\perp,0}^2}{2B_0} = \frac{m (v_0 \sin\vartheta_0)^2}{2B_0} = \frac{E \sin^2\vartheta_0}{B_0} $
其中 $E = \frac{1}{2}mv_0^2$。
然后，计算[磁场](@entry_id:153296)梯度：
$ \frac{dB}{ds} = \frac{2B_0 s}{L^2} $
代入[运动方程](@entry_id:170720)：
$ m \frac{d^2s}{dt^2} = - \left( \frac{E \sin^2\vartheta_0}{B_0} \right) \left( \frac{2B_0 s}{L^2} \right) = - \left( \frac{2E \sin^2\vartheta_0}{L^2} \right) s $
这是一个标准的简谐[振动](@entry_id:267781)方程 $\frac{d^2s}{dt^2} + \omega_b^2 s = 0$。通过比较，我们得到**弹跳角频率**（bounce angular frequency） $\omega_b$ 的平方：
$ \omega_b^2 = \frac{2E \sin^2\vartheta_0}{mL^2} $
因此，弹跳角频率为：
$ \omega_b = \frac{\sin\vartheta_0}{L} \sqrt{\frac{2E}{m}} $
这个频率描述了被[捕获粒子](@entry_id:756145)在磁镜[势阱](@entry_id:151413)中来回[振荡](@entry_id:267781)的快慢。例如，对于一个能量为 $E=73\,\mathrm{keV}$、质量为 $m_d = 3.343583719 \times 10^{-27}\,\mathrm{kg}$ 的[氘核](@entry_id:161402)，在一个特征长度为 $L=0.27\,\mathrm{m}$ 的[磁镜](@entry_id:204158)中，如果其初始螺距角为 $\vartheta_0 = 68^\circ$，它的弹跳角频率约为 $\omega_b \approx 9.083 \times 10^6\,\mathrm{rad/s}$。[@problem_id:3701420]

### [导心漂移](@entry_id:162721)

除了沿磁力线的运动，[导心](@entry_id:200181)还会缓慢地垂直于[磁场](@entry_id:153296)方向漂移。这种**漂移运动**（drift motion）是由于[洛伦兹力](@entry_id:145104)在一个回旋周期内不完全为零的净效应造成的。任何作用在[带电粒子](@entry_id:160311)上的垂直于 $\mathbf{B}$ 的力 $\mathbf{F}_{\perp}$ 都会导致一个漂移。通过对洛伦兹力方程进行周期平均，可以得到一个普遍的漂移速度公式：

$ \mathbf{v}_F = \frac{\mathbf{F}_{\perp} \times \mathbf{B}}{q B^2} $

下面我们将讨论几种最重要的漂移机制。

#### $\mathbf{E} \times \mathbf{B}$ 漂移

当存在一个垂直于[磁场](@entry_id:153296)的[电场](@entry_id:194326) $\mathbf{E}_{\perp}$ 时，粒子会经历一个 $\mathbf{E} \times \mathbf{B}$ 漂移。此时 $\mathbf{F}_{\perp} = q\mathbf{E}_{\perp}$，代入通用公式得到：

$ \mathbf{v}_E = \frac{(q\mathbf{E}_{\perp}) \times \mathbf{B}}{q B^2} = \frac{\mathbf{E} \times \mathbf{B}}{B^2} $

这个[漂移速度](@entry_id:262489)非常特殊，因为它与粒子的[电荷](@entry_id:275494) $q$、质量 $m$ 和能量 $E$ 均无关。这意味着在给定的[电磁场](@entry_id:265881)中，所有的粒子，无论其种类和能量，都以相同的速度和方向漂移。因此，$\mathbf{E} \times \mathbf{B}$ 漂移代表了等离子体作为一个整体的宏观流动，可以看作是磁力线自身的运动。

#### [磁场](@entry_id:153296)不[均匀性](@entry_id:152612)引起的漂移

在一个不均匀的[磁场](@entry_id:153296)中，即使没有外加[电场](@entry_id:194326)，粒子也会发生漂移。主要有两种相关的机制：梯度漂移和[曲率漂移](@entry_id:189511)。

**梯度-B 漂移 (Grad-B Drift)**

当磁场强度存在梯度时（$\nabla B \neq 0$），粒子的[拉莫尔半径](@entry_id:197083)在其回旋[轨道](@entry_id:137151)的不同位置是不同的。例如，在一个垂直于纸面向里的[磁场](@entry_id:153296)中，如果磁场强度向上增强，那么正离子（逆时针回旋）在其[轨道](@entry_id:137151)的上半部分（[磁场](@entry_id:153296)更强）的[回旋半径](@entry_id:261534)会更小，而在下半部分（[磁场](@entry_id:153296)更弱）的[回旋半径](@entry_id:261534)会更大。这种不对称的[轨道](@entry_id:137151)导致粒子在每个回旋周期后都有一个净的横向位移。这个漂移的有效力可以看作是磁矩与[磁场](@entry_id:153296)梯度相互作用的结果，$\mathbf{F}_{\nabla B} = -\mu \nabla B$。代入通用漂移公式，得到**梯度-B漂移**速度：

$ \mathbf{v}_{\nabla B} = \frac{(-\mu \nabla_{\perp} B) \times \mathbf{B}}{q B^2} = \frac{\mu}{q} \frac{\mathbf{B} \times \nabla B}{B^2} $

梯度-B漂移的速度与粒子的垂直能量（通过 $\mu$）成正比，并且依赖于[电荷](@entry_id:275494)的符号。

**[曲率漂移](@entry_id:189511) (Curvature Drift)**

当磁力线是弯曲的时，沿着磁力线运动的粒子会感受到一个[离心力](@entry_id:173726)。[@problem_id:3701430] 我们可以将此[离心力](@entry_id:173726)视为一个作用在[导心](@entry_id:200181)上的有效力 $\mathbf{F}_{\kappa}$。对于一个以平行速度 $v_{\parallel}$ 运动的粒子，这个力为 $\mathbf{F}_{\kappa} = m v_{\parallel}^2 \boldsymbol{\kappa}$，其中 $\boldsymbol{\kappa} = (\mathbf{b} \cdot \nabla)\mathbf{b}$ 是磁力线的曲率矢量，$\mathbf{b} = \mathbf{B}/B$。将这个力代入通用漂移公式，得到**[曲率漂移](@entry_id:189511)**速度：

$ \mathbf{v}_{\kappa} = \frac{(m v_{\parallel}^2 \boldsymbol{\kappa}) \times \mathbf{B}}{q B^2} = \frac{m v_{\parallel}^2}{q B^2} (\boldsymbol{\kappa} \times \mathbf{B}) $

[曲率漂移](@entry_id:189511)与粒子的平行能量成正比，并且也依赖于[电荷](@entry_id:275494)的符号。在典型的[托卡马克](@entry_id:182005)几何中，梯度-B漂移和[曲率漂移](@entry_id:189511)的方向通常是相同的（例如，都沿竖直方向），并且它们的效应会叠加。

#### [托卡马克](@entry_id:182005)几何中的组合漂移

让我们考虑一个更实际的例子，将多种漂移结合起来。在一个简化的托卡马克模型中，[磁场](@entry_id:153296)主要是环向的，其强度随大半径 $R$ 的变化而变化，即 $B \approx B_0 R_0/R$。同时，可能存在一个竖直方向的[电场](@entry_id:194326) $\mathbf{E} = E_0 \mathbf{e}_z$。[@problem_id:3701422]

在这种情况下，一个离子的总漂移由 $\mathbf{E} \times \mathbf{B}$ 漂移和梯度-B漂移（假设 $v_{\parallel} \approx 0$ 以简化讨论）组成：
$\mathbf{v}_D = \mathbf{v}_E + \mathbf{v}_{\nabla B}$。

1.  **$\mathbf{E} \times \mathbf{B}$ 漂移**：在 $R=R_0$ 处，$\mathbf{B} = B_0 \mathbf{e}_{\phi}$，$\mathbf{E} = E_0 \mathbf{e}_z$。漂移速度为 $\mathbf{v}_E = (\mathbf{E} \times \mathbf{B})/B^2 = (E_0 \mathbf{e}_z \times B_0 \mathbf{e}_{\phi}) / B_0^2 = -(E_0/B_0)\mathbf{e}_R$。这是一个径向向内的漂移。

2.  **梯度-B 漂移**：[磁场](@entry_id:153296)梯度为 $\nabla B = \frac{\partial}{\partial R}(B_0 R_0/R) \mathbf{e}_R = -B_0 R_0/R^2 \mathbf{e}_R$。在 $R=R_0$ 处，$\nabla B = -(B_0/R_0)\mathbf{e}_R$。漂移速度为 $\mathbf{v}_{\nabla B} = \frac{\mu}{q} \frac{\mathbf{B} \times \nabla B}{B^2} = \frac{W_{\perp}/B_0}{e} \frac{B_0 \mathbf{e}_{\phi} \times (-B_0/R_0 \mathbf{e}_R)}{B_0^2} = \frac{W_{\perp}}{eB_0 R_0} \mathbf{e}_z$。这是一个竖直向上的漂移。

总漂移速度为 $\mathbf{v}_D = -(E_0/B_0)\mathbf{e}_R + (W_{\perp}/eB_0 R_0)\mathbf{e}_z$。对于典型的聚变参数，如 $B_0 = 5\,\mathrm{T}$, $R_0 = 3\,\mathrm{m}$, $E_0=100\,\mathrm{V/m}$, $W_{\perp} = 50\,\mathrm{keV}$ 的氘离子，$\mathbf{E} \times \mathbf{B}$ 漂移速度约为 $20\,\mathrm{m/s}$，而梯度-B漂移速度约为 $3333\,\mathrm{m/s}$。这表明在没有强[径向电场](@entry_id:194700)的情况下，由[磁场](@entry_id:153296)不均匀性引起的漂移通常是主导的。

在[托卡马克](@entry_id:182005)中，梯度-B漂移和[曲率漂移](@entry_id:189511)共同导致了正离子和电子向相反的竖直方向漂移。例如，在标准配置下，离子向上漂移，电子向下漂移。这种[电荷](@entry_id:275494)分离会在等离子体的顶部和底部积累[电荷](@entry_id:275494)，从而产生一个竖直[电场](@entry_id:194326)。这个[电场](@entry_id:194326)反过来又会引起一个径向向外的 $\mathbf{E} \times \mathbf{B}$ 漂移，这对[粒子约束](@entry_id:148454)是不利的。

### [有限拉莫尔半径效应](@entry_id:204257)与回旋平均

标准的[导心漂移](@entry_id:162721)理论假设作用力是在[导心](@entry_id:200181)位置处评估的。然而，粒子实际上是在其整个拉莫尔[轨道](@entry_id:137151)上感受场的作用。当[电场](@entry_id:194326)或[磁场](@entry_id:153296)的空间变化尺度可与[拉莫尔半径](@entry_id:197083) $\rho$ 相比拟时，我们就必须考虑这种“有限[拉莫尔半径](@entry_id:197083)”（Finite Larmor Radius, FLR）效应。这通过对物理量在回旋[轨道](@entry_id:137151)上进行平均来处理，这个过程称为**回旋平均**（gyroaveraging）。

考虑一个在均匀[磁场](@entry_id:153296) $\mathbf{B}=B\hat{\mathbf{z}}$ 中的离子，但它受到一个空间变化的[静电势](@entry_id:188370) $\phi(x) = \phi_0 \sin(kx)$ 的影响。[@problem_id:3701429] 其产生的[电场](@entry_id:194326)为 $\mathbf{E}(x) = -k\phi_0 \cos(kx) \hat{\mathbf{x}}$。这会导致一个瞬时的 $\mathbf{E} \times \mathbf{B}$ 漂移，方向在 $\hat{\mathbf{y}}$ 方向。

[导心](@entry_id:200181)感受到的有效漂移是这个瞬时漂移在整个回旋[轨道](@entry_id:137151)上的平均值。假设[导心](@entry_id:200181)位于 $x_{\mathrm{gc}}=0$，粒子的瞬时x坐标为 $x = \rho \cos\theta$，其中 $\theta$ 是回旋相位角。回旋平均的y方向[漂移速度](@entry_id:262489)为：
$ \langle v_{E,y} \rangle = \frac{1}{2\pi} \int_0^{2\pi} v_{E,y}(x(\theta)) d\theta = \frac{1}{2\pi} \int_0^{2\pi} \frac{k\phi_0}{B} \cos(k\rho\cos\theta) d\theta $
这个积分是零阶[第一类贝塞尔函数](@entry_id:166421) $J_0(k\rho)$ 的积分表示。而在[导心](@entry_id:200181)位置处的漂移速度为 $v_{E0} = (k\phi_0/B)\cos(0) = k\phi_0/B$。因此，我们得到：
$ \langle v_{E,y} \rangle = J_0(k\rho) v_{E0} $
贝塞尔函数 $J_0(z)$ 在 $z=0$ 时为1，并随着 $z$ 的增加而[振荡](@entry_id:267781)衰减。这个结果表明，FLR效应会减小[导心](@entry_id:200181)感受到的平均[电场](@entry_id:194326)，当波长 $1/k$ 变得与[拉莫尔半径](@entry_id:197083) $\rho$ 相当时，这种削弱效应变得非常显著。

对于长波极限（$k\rho \ll 1$），我们可以对结果进行[泰勒展开](@entry_id:145057)。[@problem_id:3701435] 例如，对于一个[电势](@entry_id:267554) $\Phi(y) = \Phi_1 \cos(ky)$，回旋平均的x方向漂移速度在保留到 $(k\rho)^2$ 阶时为：
$ \langle v_x \rangle \approx \frac{k\Phi_1}{B_0}\sin(kY) \left( 1 - \frac{(k\rho)^2}{4} \right) $
这清晰地展示了FLR效应引入的对“零阶”漂移（即在[导心](@entry_id:200181)位置评估的漂移）的修正。

FLR效应还引入了一种新的漂移机制，即**[极化漂移](@entry_id:187655)**（polarization drift）。它源于粒子回旋运动的惯性。当[电场](@entry_id:194326)随时间变化时，粒子[轨道](@entry_id:137151)需要时间来调整，这种延迟导致了一个净漂移。在低频（$\omega \ll \Omega$）和小 $k\rho$ 的 gyrokinetic 极限下，可以从粒子数守恒和[导心运动](@entry_id:202625)方程出发，推导出由[静电波](@entry_id:196551)扰动 $\phi$ 引起的线性化的离子密度响应。[@problem_id:3701433]

结果表明，离子[密度扰动](@entry_id:159546)振幅 $\delta n_i$ 与[电势](@entry_id:267554)振幅 $\phi_0$ 的关系（在等温、无背景梯度的简化情况下）为：
$ \frac{\delta n_i}{\phi_0} = -n_0 \frac{q_i}{T_i} k^2 \rho_i^2 $
这里的 $\rho_i$ 是热离子[拉莫尔半径](@entry_id:197083)。这个响应被称为**[离子极化](@entry_id:145365)密度**（ion polarization density）。它完全是一个FLR效应，因为当 $\rho_i \to 0$ 时，该响应消失。这个结果是[线性波理论](@entry_id:193657)和微观不稳定性分析的基石，它展示了FLR效应如何将粒子动力学与等离子体的集体行为联系起来。