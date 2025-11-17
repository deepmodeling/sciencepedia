## 引言
[分析力学](@entry_id:166738)为经典力学的研究提供了一种深刻而优雅的视角，其核心工具之一便是第二类[拉格朗日方程](@entry_id:175419)。相较于依赖于矢量力和加速度的牛顿力学，[拉格朗日方法](@entry_id:142825)将分析的[焦点](@entry_id:174388)转移到了系统的标量能量函数上，从而极大地简化了对复杂系统的动力学建模，特别是那些涉及多自由度、约束和非惯性[坐标系](@entry_id:156346)的难题。这种基于[作用量原理](@entry_id:154742)的框架不仅是理论物理的基石，也在现代工程和数据科学中展现出强大的生命力。

本文旨在全面解析第二类拉格朗-日方程的理论与实践。在“原理与机制”一章中，我们将从[广义坐标](@entry_id:156576)和拉格朗日量的构建出发，系统学习如何运用[欧拉-拉格朗日方程](@entry_id:137827)求解运动。接着，在“应用与交叉学科联系”一章中，我们将探讨该方法在处理[刚体动力学](@entry_id:142040)、耦合[振动](@entry_id:267781)、相对论及电磁学等前沿和交叉问题中的强大功能。最后，通过“动手实践”中的精选问题，您将有机会将理论知识应用于具体计算，从而真正掌握这一强大的分析工具。

## 原理与机制

在上一章中，我们介绍了[分析力学](@entry_id:166738)的基本思想，它将研究重点从[牛顿力学](@entry_id:162125)中的矢量力转移到了更为抽象但功能强大的标量函数——[拉格朗日量](@entry_id:174593)。本章将深入探讨第二类[拉格朗日方程](@entry_id:175419)的原理与机制。我们将从构建拉格朗日量（Lagrangian）的核心步骤开始，逐步展示如何运用[欧拉-拉格朗日方程](@entry_id:137827)（Euler-Lagrange Equation）求解复杂的动力学问题，包括那些涉及[非惯性系](@entry_id:168746)、约束、[振动](@entry_id:267781)以及非机械作用（如[电磁力](@entry_id:196024)）的系统。

### [广义坐标](@entry_id:156576)与拉格朗日量

[拉格朗日力学](@entry_id:147054)的出发点是选择一套能够完全描述系统位形的独立坐标，即**[广义坐标](@entry_id:156576) (generalized coordinates)**。这些坐标的数量等于系统的**自由度 (degrees of freedom)**，它们的选择往往能极大地简化问题的数学表达。

思考一个质量为 $m$、长度为 $L$ 的均匀细杆，其两端被约束在水平 $xy$ 平面的正 $x$ 轴和正 $y$ 轴上滑动 [@problem_id:2062695]。尽管杆上的每个[质点](@entry_id:186768)都有自己的[笛卡尔坐标](@entry_id:167698)，但整个系统的位形仅由一个变量即可完全确定，例如杆与 $x$ 轴的夹角 $\theta$。因此，该系统只有一个自由度，$\theta$ 便是一个合适的[广义坐标](@entry_id:156576)。一旦选定了[广义坐标](@entry_id:156576)，系统的所有[运动学](@entry_id:173318)量，如速度和位置，都应由这些坐标及其对时间的导数（[广义速度](@entry_id:178456)）来表达。

[拉格朗日量](@entry_id:174593) $L$ 定义为系统的总动能 $T$ 与总势能 $V$之差：

$L = T - V$

正确地用[广义坐标](@entry_id:156576)表达 $T$ 和 $V$ 是应用[拉格朗日方法](@entry_id:142825)的关键第一步。

#### 动能的表达

动能 $T$ 是系统所有部分运动能量的总和，必须表示为[广义坐标](@entry_id:156576)和[广义速度](@entry_id:178456)的函数。对于刚体，动能通常包含[平动动能](@entry_id:174977)和[转动动能](@entry_id:177668)两部分。

根据**[柯尼希定理](@entry_id:268028) (König's theorem)**，刚体的总动能等于其质心[平动动能](@entry_id:174977)与绕[质心](@entry_id:265015)转动的动能之和：$T = \frac{1}{2} M v_{cm}^2 + \frac{1}{2} I_{cm} \omega^2$。

让我们再次考虑前述在轴上滑动的细杆 [@problem_id:2062695]。其两端坐标分别为 $(L\cos\theta, 0)$ 和 $(0, L\sin\theta)$，因此质心坐标为 $(x_{cm}, y_{cm}) = (\frac{1}{2} L \cos\theta, \frac{1}{2} L \sin\theta)$。[质心速度](@entry_id:175479)的平方为 $v_{cm}^2 = \dot{x}_{cm}^2 + \dot{y}_{cm}^2 = \frac{1}{4} L^2 \dot{\theta}^2$。杆绕[质心](@entry_id:265015)的转动[角速度](@entry_id:192539)为 $\dot{\theta}$，其绕质心的[转动惯量](@entry_id:174608)为 $I_{cm} = \frac{1}{12} m L^2$。因此，总动能为：
$$ T = \frac{1}{2} m \left(\frac{1}{4} L^2 \dot{\theta}^2\right) + \frac{1}{2} \left(\frac{1}{12} m L^2\right) \dot{\theta}^2 = \frac{1}{6} m L^2 \dot{\theta}^2 $$

另一个例子是悠悠球 [@problem_id:2062692]，它是一个质量为 $M$、半径为 $R$ 的圆柱体，绕半径为 $r$ 的轴转动下落。设其质心下落的垂直坐标为 $y$，转动角度为 $\phi$。系统的运动受到一个**约束条件**：绳子无滑动地展开，即 $y = r\phi$。这意味着 $\dot{y} = r\dot{\phi}$。我们可以选择 $y$ 作为[广义坐标](@entry_id:156576)。系统的动能包含平动和转动两部分，[质心](@entry_id:265015)的[转动惯量](@entry_id:174608)为 $I = \frac{1}{2}MR^2$。
$$ T = \frac{1}{2} M \dot{y}^2 + \frac{1}{2} I \dot{\phi}^2 = \frac{1}{2} M \dot{y}^2 + \frac{1}{2} \left(\frac{1}{2}MR^2\right) \left(\frac{\dot{y}}{r}\right)^2 = \frac{1}{2} M \left(1 + \frac{R^2}{2r^2}\right) \dot{y}^2 $$
可见，通过[广义坐标](@entry_id:156576)和约束条件，我们将一个复杂的复合运动的动能表示成了一个只含[广义速度](@entry_id:178456) $\dot{y}$ 的简单二次式。

#### 势能的表达

对于保守系统，势能 $V$ 仅是[广义坐标](@entry_id:156576)的函数。常见的势能来源包括重力势和弹性势。

在一个位于斜面上、绕竖直轴旋转的系统中，一个质量为 $m$ 的滑块沿斜面上的直线运动。设斜面与水平面夹角为 $\theta$，旋转[角速度](@entry_id:192539)为 $\omega$。我们选择滑块到[旋转轴](@entry_id:187094)与斜面交点（枢轴）的距离 $r$ 作为[广义坐标](@entry_id:156576)。滑块的重力[势能](@entry_id:748988)（以枢轴为零[势能](@entry_id:748988)点）为 $V_g = mgz = mgr\sin\theta$。如果滑块还连接到一个弹簧，例如一个自然长度为 $L_0$、[劲度系数](@entry_id:167197)为 $k$ 的弹簧，其一端固定在离枢轴距离为 $d$ 的点上，则弹簧的弹性势能为 $V_s = \frac{1}{2}k(r - d - L_0)^2$。系统的总势能就是这两者之和 [@problem_id:2062656]：
$$ V(r) = mgr\sin\theta + \frac{1}{2}k(r-d-L_0)^2 $$

一旦将 $T$ 和 $V$ 都用[广义坐标](@entry_id:156576)及其导数表示出来，我们就可以构建[拉格朗日量](@entry_id:174593) $L = T - V$，为下一步求解[运动方程](@entry_id:170720)做好准备。

### 欧拉-拉格朗日方程

对于一个由[广义坐标](@entry_id:156576) $q_i$ 描述的[保守系统](@entry_id:167760)，其运动轨迹遵循**[哈密顿原理](@entry_id:175601) (Hamilton's Principle)**，即作用量 $S = \int L(q_i, \dot{q}_i, t) dt$ 取极值。这一原理的直接数学结果就是**欧拉-拉格朗日方程**：
$$ \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q_i}}\right) - \frac{\partial L}{\partial q_i} = 0 $$
对于系统的每一个自由度（即每一个 $q_i$），都有一个对应的方程。这组[二阶常微分方程](@entry_id:204212)构成了系统的**运动方程 (equations of motion)**。

[拉格朗日方法](@entry_id:142825)的一大优势在于它能自动处理约束。只要我们选择了正确的独立[广义坐标](@entry_id:156576)，约束条件就已经被内嵌于动能和[势能](@entry_id:748988)的表达式中，我们无需像在牛顿力学中那样明确地处理[约束力](@entry_id:170052)。

然而，有时我们确实需要知道约束力的大小。[拉格朗日方法](@entry_id:142825)提供了一条间接的途径：首先利用[拉格朗日方程](@entry_id:175419)求解出系统的加速度，然后应用牛顿第二定律 $\vec{F}_{net} = m\vec{a}$，将[约束力](@entry_id:170052)作为未知力与其他已知力（如重力）一起代入，从而解出约束力。

让我们来看一个例子：一个质量为 $m$ 的珠子被约束在固定的螺旋线上滑动，该螺旋线由[参数方程](@entry_id:172360) $x = R\cos\phi$, $y = R\sin\phi$, $z = -b\phi$ 描述，并处在均匀重[力场](@entry_id:147325) $\vec{g}=-g\hat{k}$ 中 [@problem_id:2062687]。
系统的自由度为1，我们选择 $\phi$ 作为[广义坐标](@entry_id:156576)。
动能 $T = \frac{1}{2}m(\dot{x}^2+\dot{y}^2+\dot{z}^2) = \frac{1}{2}m(R^2+b^2)\dot{\phi}^2$。
[势能](@entry_id:748988) $V = mgz = -mgb\phi$。
[拉格朗日量](@entry_id:174593) $L = T - V = \frac{1}{2}m(R^2+b^2)\dot{\phi}^2 + mgb\phi$。
应用欧拉-拉格朗日方程：
$\frac{\partial L}{\partial \dot{\phi}} = m(R^2+b^2)\dot{\phi}$
$\frac{\partial L}{\partial \phi} = mgb$
方程为：$\frac{d}{dt}(m(R^2+b^2)\dot{\phi}) - mgb = 0$，解得角加速度 $\ddot{\phi} = \frac{gb}{R^2+b^2}$，这是一个常数。

有了加速度，我们就可以计算[约束力](@entry_id:170052)（法向力 $\vec{N}$）。珠子所受合力为重力 $\vec{F}_g$ 和法向力 $\vec{N}$，根据牛顿第二定律，$\vec{F}_g + \vec{N} = m\vec{a}$。因此，$\vec{N} = m\vec{a} - \vec{F}_g$。通过对位置矢量求[二阶导数](@entry_id:144508)得到加[速度矢量](@entry_id:269648) $\vec{a}$，代入上式即可求得法向力。这个过程清晰地展示了[拉格朗日力学](@entry_id:147054)在求解运动和约束力问题中的[分工](@entry_id:190326)与合作。

### 在[非惯性系](@entry_id:168746)中的应用

[拉格朗日形式](@entry_id:145697)在[非惯性系](@entry_id:168746)中依然有效，这是它相较于牛顿力学的另一个巨大优势。我们只需在[惯性系](@entry_id:266190)中写出动能和势能，然后通过[坐标变换](@entry_id:172727)将其用[非惯性系](@entry_id:168746)中的[广义坐标](@entry_id:156576)来表示即可。

#### 平动[加速参考系](@entry_id:168026)

考虑一个在以[恒定加速度](@entry_id:268979) $a_0$ 向上加速的火箭中的单摆 [@problem_id:2062638]。在火箭这个[非惯性系](@entry_id:168746)中，除了重力 $mg$ 外，摆锤还受到一个向下的惯性力 $ma_0$。这等效于摆锤处在一个**有效重[力场](@entry_id:147325) (effective gravitational field)** 中，其加速度为 $g_{\text{eff}} = g+a_0$。

我们可以通过[拉格朗日量](@entry_id:174593)来形式化地得到这个结果。设摆角为 $\theta$（与竖直方向的夹角），摆长为 $L$。在地面（惯性）系中，摆锤的坐标为 $(x, y) = (L\sin\theta, y_0(t) - L\cos\theta)$，其中 $y_0(t) = \frac{1}{2}a_0 t^2$ 是枢轴的坐标。
动能 $T = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)$，势能 $V = mgy$。将坐标表达式代入并化简，会得到一个相当复杂的拉格朗日量。然而，一个更简洁的方法是在[非惯性系](@entry_id:168746)中直接引入一个与加速度相关的[势能](@entry_id:748988)项。[有效势能](@entry_id:171609)为 $V_{\text{eff}} = -mgL\cos\theta - ma_0L\cos\theta = -m(g+a_0)L\cos\theta$。动能则是在该[参考系](@entry_id:169232)中观察到的动能 $T = \frac{1}{2}mL^2\dot{\theta}^2$。
[拉格朗日量](@entry_id:174593)为 $L = T - V_{\text{eff}} = \frac{1}{2}mL^2\dot{\theta}^2 + m(g+a_0)L\cos\theta$。
对应的[运动方程](@entry_id:170720)为 $mL^2\ddot{\theta} + m(g+a_0)L\sin\theta = 0$。对于小角度[振荡](@entry_id:267781)，$\sin\theta \approx \theta$，方程变为 $\ddot{\theta} + \frac{g+a_0}{L}\theta=0$。这是一个简谐[振动](@entry_id:267781)方程，其[角频率](@entry_id:261565)为 $\omega = \sqrt{\frac{g+a_0}{L}}$。

#### 转动[参考系](@entry_id:169232)

转动[参考系](@entry_id:169232)是[拉格朗日方法](@entry_id:142825)大放异彩的领域。考虑一个以恒定角速度 $\omega$ 绕竖直轴旋转的水平转盘。一个质量为 $m$ 的[质点](@entry_id:186768)在盘上运动 [@problem_id:2062669]。在实验室（惯性）系中，若[质点](@entry_id:186768)在转盘上的极坐标为 $(r, \phi')$，则其在实验室的极坐标为 $(r, \phi = \phi' + \omega t)$。
[质点](@entry_id:186768)在实验室系中的速度平方为 $v^2 = \dot{r}^2 + r^2\dot{\phi}^2 = \dot{r}^2 + r^2(\dot{\phi}' + \omega)^2 = (\dot{r}^2 + r^2\dot{\phi}'^2) + 2\omega r^2 \dot{\phi}' + \omega^2 r^2$。
动能 $T = \frac{1}{2}mv^2$。如果系统中还存在[势能](@entry_id:748988) $V(r, \phi')$，则拉格朗日量为 $L = T - V$。
代入欧拉-拉格朗日方程后，我们会发现方程中自然地出现了对应于**[科里奥利力](@entry_id:160096) (Coriolis force)** 和**[离心力](@entry_id:173726) (centrifugal force)** 的项。

对于许多只关心平衡状态的问题，我们可以引入**[有效势能](@entry_id:171609) (effective potential)** 的概念。对于一个在转动[参考系](@entry_id:169232)中径向位置为 $r_{\perp}$（到转轴的垂直距离）、[势能](@entry_id:748988)为 $V$ 的粒子，其有效势能定义为：
$$ V_{\text{eff}} = V - \frac{1}{2}m\omega^2 r_{\perp}^2 $$
其中第二项被称为**[离心势](@entry_id:172447)能**。系统的[平衡位置](@entry_id:272392)对应于[有效势能](@entry_id:171609) $V_{\text{eff}}$ 的[极值](@entry_id:145933)点。

例如，一个质量为 $m$ 的珠子套在半径为 $R$ 的光滑[圆环](@entry_id:163678)上，[圆环](@entry_id:163678)以角速度 $\omega$ 绕其竖直直径旋转 [@problem_id:2062641]。设珠子位置与向下竖直方向的夹角为 $\theta$。其重力势能为 $V_g = -mgR\cos\theta$，到转轴的距离为 $r_{\perp} = R\sin\theta$。
有效势能为：
$$ V_{\text{eff}}(\theta) = -mgR\cos\theta - \frac{1}{2}m\omega^2(R\sin\theta)^2 $$
平衡条件是 $\frac{dV_{\text{eff}}}{d\theta} = 0$：
$$ \frac{dV_{\text{eff}}}{d\theta} = mgR\sin\theta - m\omega^2R^2\sin\theta\cos\theta = mR\sin\theta(g - \omega^2R\cos\theta) = 0 $$
该方程的解为 $\sin\theta = 0$（即 $\theta=0$ 或 $\theta=\pi$，在环的底部和顶部）或 $\cos\theta = \frac{g}{\omega^2R}$。后者是非平凡的[平衡位置](@entry_id:272392)，只有当 $\omega^2 \ge g/R$ 时才存在。

### 平衡与微[振动](@entry_id:267781)

[拉格朗日方法](@entry_id:142825)是研究系统在[平衡点](@entry_id:272705)附近行为的强大工具。

#### 寻找[平衡点](@entry_id:272705)与[稳定性分析](@entry_id:144077)

如前所述，系统的[平衡点](@entry_id:272705) $q_{i0}$ 是有效势能的[极值](@entry_id:145933)点，即 $\frac{\partial V_{\text{eff}}}{\partial q_i}|_{q_{i0}} = 0$。

[平衡点的稳定性](@entry_id:177203)由[有效势能](@entry_id:171609)的[二阶导数](@entry_id:144508)决定。如果在一个单自由度系统中，在[平衡点](@entry_id:272705) $\theta_0$ 处，$\frac{d^2 V_{\text{eff}}}{d\theta^2}|_{\theta_0} > 0$，则该点是[势能](@entry_id:748988)的极小值点，对应**稳定平衡 (stable equilibrium)**。反之，若[二阶导数](@entry_id:144508)小于零，则为**不稳定平衡 (unstable equilibrium)**。

在前面滑杆的例子中 [@problem_id:2062695]，假设两端分别与劲度系数为 $k_x$ 和 $k_y$ 的弹簧相连，弹簧原长为零。势能为 $U(\theta) = \frac{1}{2}k_x(L\cos\theta)^2 + \frac{1}{2}k_y(L\sin\theta)^2$。
其[一阶导数](@entry_id:749425)为 $\frac{dU}{d\theta} = \frac{1}{2}L^2(k_y - k_x)\sin(2\theta)$。[平衡点](@entry_id:272705)为 $\theta_0=0$ 和 $\theta_0=\pi/2$。
[二阶导数](@entry_id:144508)为 $\frac{d^2U}{d\theta^2} = L^2(k_y-k_x)\cos(2\theta)$。
若 $k_x > k_y$，在 $\theta_0=0$ 处，$U''  0$ (不稳定)；在 $\theta_0=\pi/2$ 处，$U'' > 0$ (稳定)。

#### 微[振动频率](@entry_id:199185)

对于在稳定[平衡点](@entry_id:272705) $q_0$ 附近的微小[振动](@entry_id:267781)，我们可以将系统坐标写为 $q(t) = q_0 + \eta(t)$，其中 $\eta(t)$ 是小位移。将此代入[拉格朗日量](@entry_id:174593)，并展开到 $\eta$ 和 $\dot{\eta}$ 的二阶项，可以得到一个近似的[拉格朗日量](@entry_id:174593)：
$$ L \approx \frac{1}{2}M_{\text{eff}}\dot{\eta}^2 - \frac{1}{2}K_{\text{eff}}\eta^2 + \text{常量} $$
其中 $M_{\text{eff}} = \left(\frac{\partial^2 T}{\partial \dot{q}^2}\right)_{q_0}$ 是有效惯量，$K_{\text{eff}} = \left(\frac{\partial^2 V}{\partial q^2}\right)_{q_0}$ 是有效[弹性系数](@entry_id:192914)。
对应的运动方程为 $M_{\text{eff}}\ddot{\eta} + K_{\text{eff}}\eta = 0$，这是一个简谐[振动](@entry_id:267781)方程，其角频率为：
$$ \Omega = \sqrt{\frac{K_{\text{eff}}}{M_{\text{eff}}}} = \sqrt{\frac{V''(q_0)}{T''(\dot{q}_0)}} $$
其中 $T''$ 表示对[广义速度](@entry_id:178456)求二阶导。

对于前面提到的稳定[平衡点](@entry_id:272705)在 $\theta_0=\pi/2$ 的滑杆系统 [@problem_id:2062695]，我们有 $K_{\text{eff}} = U''(\pi/2) = L^2(k_x-k_y)$，以及从 $T = \frac{1}{6}mL^2\dot{\theta}^2$ 得到的有效惯量（即 $\dot{\theta}^2$ 前系数的两倍）$M_{\text{eff}} = \frac{1}{3}mL^2$。因此，微[振动](@entry_id:267781)[角频率](@entry_id:261565)为：
$$ \Omega = \sqrt{\frac{L^2(k_x-k_y)}{\frac{1}{3}mL^2}} = \sqrt{\frac{3(k_x-k_y)}{m}} $$
这个方法具有普适性，可应用于各种系统，例如分析在旋转圆锥体上运动的粒子的径向微[振动](@entry_id:267781) [@problem_id:2062686] 或在旋转转盘上由弹簧连接的两个物体的[振动](@entry_id:267781)模式 [@problem_id:2062675]。

### [守恒定律](@entry_id:269268)与[广义势](@entry_id:175268)

[拉格朗日形式](@entry_id:145697)与物理学的基本[守恒定律](@entry_id:269268)有着深刻的联系。

#### [循环坐标](@entry_id:166220)与守恒动量

如果拉格朗日量 $L$ 不显含某个[广义坐标](@entry_id:156576) $q_k$（即 $\frac{\partial L}{\partial q_k} = 0$），则称 $q_k$ 为**[循环坐标](@entry_id:166220) (cyclic coordinate)** 或**[可忽略坐标](@entry_id:166220) (ignorable coordinate)**。
在这种情况下，[欧拉-拉格朗日方程](@entry_id:137827)简化为 $\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q_k}}\right) = 0$。
这意味着物理量 $p_k = \frac{\partial L}{\partial \dot{q_k}}$ 是一个守恒量。这个量被称为 $q_k$ 的**广义[共轭动量](@entry_id:172203) (generalized conjugate momentum)**。
例如，对于在重[力场](@entry_id:147325)中绕竖直轴旋转的圆锥体上运动的粒子 [@problem_id:2062686]，如果我们使用柱坐标 $(r, \phi, z)$ 并利用约束，[拉格朗日量](@entry_id:174593)中将不包含[方位角](@entry_id:164011) $\phi$，只包含 $\dot{\phi}$。因此 $\phi$ 是一个[循环坐标](@entry_id:166220)，其[共轭动量](@entry_id:172203) $p_\phi = \frac{\partial L}{\partial \dot{\phi}}$ (角动量的某个分量) 是守恒的。这个守恒律是解决该问题的关键。

#### [电磁场](@entry_id:265881)中的[拉格朗日量](@entry_id:174593)

[拉格朗日方法](@entry_id:142825)的应用可以超越经典力学[势能](@entry_id:748988)的范畴。对于一个在[电磁场](@entry_id:265881)中运动的[带电粒子](@entry_id:160311)，其受到的[洛伦兹力](@entry_id:145104) $\vec{F} = q(\vec{E} + \vec{v}\times\vec{B})$ 是速度相关的，因此不能简单地用一个标量势能 $V$ 来描述。然而，我们可以定义一个**[广义势](@entry_id:175268) (generalized potential)**：
$$ U = q\Phi - q\vec{v}\cdot\vec{A} $$
其中 $\Phi$ 是[电势](@entry_id:267554)，$\vec{A}$ 是[磁矢量势](@entry_id:141246) ($\vec{E}=-\nabla\Phi - \frac{\partial\vec{A}}{\partial t}$, $\vec{B}=\nabla\times\vec{A}$)。
此时，拉格朗日量写为 $L = T - U = \frac{1}{2}m\vec{v}^2 - q\Phi + q\vec{v}\cdot\vec{A}$。将这个拉格朗日量代入[欧拉-拉格朗日方程](@entry_id:137827)，就能正确地推导出[洛伦兹力定律](@entry_id:270735)。

考虑一个质量为 $m$、[电荷](@entry_id:275494)为 $q$ 的粒子，在均匀重[力场](@entry_id:147325) $\vec{g}=-g\hat{k}$ 和均匀[磁场](@entry_id:153296) $\vec{B}=B\hat{j}$ 中从静止开始运动 [@problem_id:2062666]。我们可以将重力视为来自一个等效的“[电场](@entry_id:194326)” $\vec{E}_{eff} = \frac{m}{q}\vec{g}$。
[拉格朗日量](@entry_id:174593)为 $L = \frac{1}{2}m(\dot{x}^2+\dot{y}^2+\dot{z}^2) - mgz - qBx\dot{z}$，其中我们选择了[磁矢量势](@entry_id:141246) $\vec{A}=-Bx\hat{k}$。
通过求解 $x, y, z$ 三个坐标的[拉格朗日方程](@entry_id:175419)，可以得到粒子的运动轨迹。其解描述了一种在 $xz$ 平面内的[摆线](@entry_id:172297)运动，同时伴随着一个沿 $x$ 轴方向的恒定**[漂移速度](@entry_id:262489) (drift velocity)**。这个平均速度可以通过对一个振荡周期积分求得，结果为：
$$ \langle\vec{v}\rangle = \frac{mg}{qB}\hat{i} $$
这个结果就是著名的 $\vec{E} \times \vec{B}$ 漂移（在此例中为有效[电场](@entry_id:194326)）。这个例子完美地展示了[拉格朗日形式](@entry_id:145697)在统一描述力学和电磁学相互作用时的优美与力量。

### [非保守系统](@entry_id:166237)

当系统中存在摩擦或阻力等[非保守力](@entry_id:163431)时，标准的欧拉-拉格朗日方程不再适用。我们需要对其进行推广，引入**[广义力](@entry_id:169699) (generalized force)** $Q_i$：
$$ \frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q_i}}\right) - \frac{\partial L}{\partial q_i} = Q_i $$
[广义力](@entry_id:169699) $Q_i$ 是[非保守力](@entry_id:163431)在[广义坐标](@entry_id:156576) $q_i$ 方向上所做的[虚功](@entry_id:176403) $\delta W_{nc}$ 的系数，即 $\delta W_{nc} = \sum_i Q_i \delta q_i$。

对于与速度成正比的阻力，可以方便地通过**[瑞利耗散函数](@entry_id:165938) (Rayleigh dissipation function)** $\mathcal{F}$ 来描述。例如，对于阻力 $\vec{f} = -\beta\vec{v}$，耗散函数为 $\mathcal{F} = \frac{1}{2}\beta v^2 = \frac{1}{2}\beta \sum_{j} \dot{x}_j^2$。
此时，[广义力](@entry_id:169699)可以由耗散函数导出：
$$ Q_i = -\frac{\partial\mathcal{F}}{\partial\dot{q_i}} $$
例如，在一个有空气阻力的球摆系统中 [@problem_id:2062707]，耗散函数为 $\mathcal{F} = \frac{1}{2}\beta(l^2\dot{\theta}^2 + l^2\sin^2\theta\dot{\phi}^2)$。系统的[总机械能](@entry_id:167353) $E=T+V$ 的变化率等于[耗散功率](@entry_id:177328) $P_{diss} = -2\mathcal{F}$。通过分析能量随时间的变化 $\frac{dE}{dt} = \frac{dE}{d\theta}\dot{\theta} = P_{diss}$，我们可以求解出系统由于能量耗散而缓慢变化的动力学行为，例如摆的极角 $\theta$ 随时间的变化率 $\dot{\theta}$。这为处理[耗散系统](@entry_id:151564)提供了一个系统性的框架。

综上所述，[拉格朗日方程](@entry_id:175419)提供了一套强大而优雅的工具，它不仅统一了对保守和非保守、惯性系和[非惯性系](@entry_id:168746)下各种力学系统的描述，还能自然地扩展到电磁学等其他物理领域，深刻地揭示了物理世界的[对称性与守恒律](@entry_id:160300)。