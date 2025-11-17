## 引言
[牛顿运动定律](@entry_id:163846)是经典力学的基石，但在其严格成立的[惯性参考系](@entry_id:276742)之外，我们如何描述运动？我们日常所处的地球本身就是一个旋转的[非惯性系](@entry_id:168746)，在加速的交通工具中，物体的行为也似乎偏离了[牛顿定律](@entry_id:163541)的预测。为了解决这一矛盾，物理学引入了“虚拟力”（或称[惯性力](@entry_id:169104)）这一强大概念。这些力并非源于真实的物理相互作用，而是观察者所处[参考系](@entry_id:169232)加速或旋转的直接体现。本文将系统地引导读者深入虚拟力的世界。在“原理与机制”一章中，我们将从运动学转换出发，精确推导离心力、[科里奥利力](@entry_id:160096)等各种虚拟力的数学形式和物理意义。接着，在“应用与跨学科联系”一章，我们将探索这些看似抽象的力如何在地球物理、天体力学乃至广义相对论中扮演着塑造我们世界的关键角色。最后，通过“动手实践”环节，读者将有机会运用所学知识解决具体的物理问题，从而真正掌握虚拟力的分析方法。让我们首先进入第一章，揭开虚拟力背后的数学与物理原理。

## 原理与机制

在上一章中，我们确立了[牛顿运动定律](@entry_id:163846)在惯性参考系中的核心地位。然而，在实际的物理世界中，我们常常处于[非惯性参考系](@entry_id:169712)——即相对于[惯性系](@entry_id:266190)存在加速或旋转的[参考系](@entry_id:169232)。在这样的[参考系](@entry_id:169232)中，为了维持牛顿第二定律的形式，我们必须引入一些额外的“力”，这些力并非源于真实的物理相互作用（如[引力](@entry_id:175476)或电磁力），而是源于[参考系](@entry_id:169232)本身的运动状态。这些力被称为 **[惯性力](@entry_id:169104) (inertial forces)** 或 **虚拟力 (fictitious forces)**。本章将深入探讨这些力的起源、数学表述及其在各种物理情景中的具体表现。

### [非惯性参考系](@entry_id:169712)中的运动学

理解虚拟力的关键在于掌握不同[参考系](@entry_id:169232)之间运动学量的转换关系。考虑一个固定的惯性参考系 $S$ 和一个相对于 $S$ 运动的[非惯性参考系](@entry_id:169712) $S'$。设 $S'$ 的原点相对于 $S$ 的原点的位置矢量为 $\mathbf{R}_0$，且 $S'$ 相对于 $S$ 以角速度 $\boldsymbol{\Omega}$ 旋转。

对于任意一个矢量 $\mathbf{Q}$，其在[惯性系](@entry_id:266190) $S$ 中的时间导数 $(\frac{d\mathbf{Q}}{dt})_S$ 和在[非惯性系](@entry_id:168746) $S'$ 中的时间导数 $(\frac{d\mathbf{Q}}{dt})_{S'}$ 之间存在一个基本关系，称为** transport theorem**：
$$
\left(\frac{d\mathbf{Q}}{dt}\right)_S = \left(\frac{d\mathbf{Q}}{dt}\right)_{S'} + \boldsymbol{\Omega} \times \mathbf{Q}
$$
这个公式的直观意义是，一个矢量在[惯性系](@entry_id:266190)中的总变化率，等于它在旋转系中自身的变化率，加上由于旋转系转动而引起的变化率。

现在，我们应用这个定理来分析一个质点的位置矢量 $\mathbf{r}_S$。在 $S$ 系和 $S'$ 系中，该质点的位置可以表示为 $\mathbf{r}_S = \mathbf{R}_0 + \mathbf{r}'$。对其求一次时间导数以得到速度关系：
$$
\mathbf{v}_S = \left(\frac{d\mathbf{r}_S}{dt}\right)_S = \left(\frac{d\mathbf{R}_0}{dt}\right)_S + \left(\frac{d\mathbf{r}'}{dt}\right)_S
$$
应用 transport theorem 于 $\mathbf{r}'$，我们得到：
$$
\mathbf{v}_S = \mathbf{V}_0 + \left(\frac{d\mathbf{r}'}{dt}\right)_{S'} + \boldsymbol{\Omega} \times \mathbf{r}' = \mathbf{V}_0 + \mathbf{v}' + \boldsymbol{\Omega} \times \mathbf{r}'
$$
其中 $\mathbf{V}_0$ 是 $S'$ 原点在 $S$ 系中的速度，$\mathbf{v}'$ 是质点在 $S'$ 系中的速度。

再次对 $\mathbf{v}_S$ 求导以获得加速度关系，过程较为繁琐但至关重要。最终，质点在惯性系中的加速度 $\mathbf{a}_S$ 可以表示为：
$$
\mathbf{a}_S = \mathbf{A}_0 + \mathbf{a}' + \frac{d\boldsymbol{\Omega}}{dt} \times \mathbf{r}' + 2(\boldsymbol{\Omega} \times \mathbf{v}') + \boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r}')
$$
其中 $\mathbf{A}_0$ 是 $S'$ 原点的加速度，$\mathbf{a}'$ 是[质点](@entry_id:186768)在 $S'$ 系中的加速度。

根据牛顿第二定律，在[惯性系](@entry_id:266190) $S$ 中，$\mathbf{F}_{\text{real}} = m\mathbf{a}_S$，其中 $\mathbf{F}_{\text{real}}$ 是所有真实物理力的矢量和。将上述加速度表达式代入并整理，我们可以得到在[非惯性系](@entry_id:168746) $S'$ 中“看起来”的[牛顿第二定律](@entry_id:274217)：
$$
m\mathbf{a}' = \mathbf{F}_{\text{real}} - m\mathbf{A}_0 - 2m(\boldsymbol{\Omega} \times \mathbf{v}') - m[\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r}')] - m\left(\frac{d\boldsymbol{\Omega}}{dt} \times \mathbf{r}'\right)
$$
右边的附加项就是我们所说的虚拟力。下面我们将逐一剖析这些力。

### 平动[加速参考系](@entry_id:168026)：惯性力

最简单的一类[非惯性系](@entry_id:168746)是只存在[平动](@entry_id:187700)加速而没有旋转的[参考系](@entry_id:169232)。在这种情况下，$\boldsymbol{\Omega} = \mathbf{0}$，上述复杂的方程简化为：
$$
m\mathbf{a}' = \mathbf{F}_{\text{real}} - m\mathbf{A}_0
$$
这里的 $-m\mathbf{A}_0$ 就是平动**惯性力**。它与[参考系](@entry_id:169232)的加速度 $\mathbf{A}_0$ 方向相反，大小与质量 $m$ 和加速度大小 $A_0$ 的乘积成正比。

一个经典的例子是电梯中的物体 [@problem_id:2049603]。考虑一个质量为 $m$ 的物体放在电梯内的弹簧秤上。弹簧秤读出的“[视重](@entry_id:173983)”是物体施加给它的正压力 $N$。在地面[惯性系](@entry_id:266190)看来，物体受到向下的重力 $mg$ 和向上的[支持力](@entry_id:174233) $N$，其合力提供了与电梯共同的加速度 $a_y$ (设向上为正)：$N - mg = ma_y$。因此，$N = m(g + a_y)$。

从电梯这个[非惯性参考系](@entry_id:169712)的角度看，物体是静止的 ($\mathbf{a}' = \mathbf{0}$)，它受到真实力——重力 $mg$ 和支持力 $N$，以及一个[惯性力](@entry_id:169104) $\mathbf{F}_{\text{inertial}} = -m\mathbf{A}_0 = -ma_y$。根据虚拟力方程，力的平衡条件是 $N - mg - ma_y = 0$，这同样给出了 $N = m(g + a_y)$。当电梯向下加速时 ($a_y  0$)，[视重](@entry_id:173983)减小，出现“失重”现象；当电梯向上加速时 ($a_y > 0$)，[视重](@entry_id:173983)增加，出现“超重”现象。如果电梯的运动轨迹由平滑函数描述，例如 $y(t) = \frac{H}{2} [ 1 + \cos(\frac{\pi t}{T}) ]$，我们可以精确计算出其加速度 $\ddot{y}(t) = -\frac{H\pi^{2}}{2T^{2}}\cos(\frac{\pi t}{T})$，并由此确定整个过程中[视重](@entry_id:173983)的最大值和最小值 [@problem_id:2049603]。

这个概念也体现了**等效原理**的一个侧面，即在局部范围内，[引力](@entry_id:175476)与[加速参考系](@entry_id:168026)中引入的惯性力是不可区分的。一个在远离[引力源](@entry_id:271552)的深空中以[恒定加速度](@entry_id:268979) $\mathbf{a}_{sc} = a_0 \hat{k}$ 飞行的飞船，其内部的宇航员会感受到一个均匀的、与加速度方向相反的“[引力场](@entry_id:169425)” $\mathbf{g}_{\text{fict}} = -a_0 \hat{k}$。如果宇航员以水平速度抛出一个球，他会观察到球的轨迹是一条抛物线，这与在地球表面[引力场](@entry_id:169425)中的情况完全相同 [@problem_id:2049583]。

### 离心力：旋转的代价

现在我们转向旋转参考系。首先考虑最简单的情况：一个以恒定角速度 $\boldsymbol{\Omega}$ 绕固定轴旋转的[参考系](@entry_id:169232)（如旋转木马或离心机）。在这种情况下，$d\boldsymbol{\Omega}/dt = \mathbf{0}$，并且我们暂时忽略[参考系](@entry_id:169232)原点的[平动](@entry_id:187700)（$\mathbf{A}_0 = \mathbf{0}$）。虚拟力方程中的一项是：
$$
\mathbf{F}_{\text{cf}} = -m[\boldsymbol{\Omega} \times (\boldsymbol{\Omega} \times \mathbf{r}')]
$$
这便是**[离心力](@entry_id:173726) (centrifugal force)**。利用矢量[三重积](@entry_id:162942)的性质 $\mathbf{A} \times (\mathbf{B} \times \mathbf{C}) = \mathbf{B}(\mathbf{A} \cdot \mathbf{C}) - \mathbf{C}(\mathbf{A} \cdot \mathbf{B})$，我们可以更好地理解它的方向和大小。离心力总是沿着垂直于转轴的径向向外，其大小为 $m\Omega^2 r_{\perp}$，其中 $r_{\perp}$ 是质点到[转轴](@entry_id:187094)的垂直距离。它源于物体在惯性系中维持直线运动的趋势，但在旋转系看来，物体似乎被一股力量向外推。

在[人造重力](@entry_id:176788)的空间站设计中，[离心力](@entry_id:173726)扮演了核心角色 [@problem_id:2049569]。通过使圆柱形空间站以适当的[角速度](@entry_id:192539) $\omega$ 旋转，内壁上的居民会体验到一个指向“地面”（即圆柱内表面）的力，这个力就是离心力。如果站内宇航员释放一个物体，离心力会使其“下落”。

考虑一个在光滑旋转圆盘上的物体 [@problem_id:2049565]。如果物体在旋转系中相对于圆盘静止在位置 $\mathbf{r}'$，那么它的相对速度 $\mathbf{v}'=0$，此时它在旋转系中感受到的唯一虚拟力就是离心力 $\mathbf{F}_{\text{cf}}$，方向沿径向向外。为了让物体保持在该位置，必须有一个向内的真实力（如绳子的拉力或[静摩擦力](@entry_id:163518)）来平衡它。

### 科里奥利力：运动的幻影

当物体在旋转参考系中运动时（$\mathbf{v}' \neq \mathbf{0}$），一个更为奇特的虚拟力便会出现：
$$
\mathbf{F}_{\text{cor}} = -2m(\boldsymbol{\Omega} \times \mathbf{v}')
$$
这就是**科里奥利力 (Coriolis force)**。它的方向既垂直于转轴 $\boldsymbol{\Omega}$，也垂直于物体在旋转系中的[相对速度](@entry_id:178060) $\mathbf{v}'$。[科里奥利力](@entry_id:160096)的出现是[守恒定律](@entry_id:269268)在旋转系中表现的结果。例如，一个在旋转圆盘上沿径向向外移动的物体，其到[转轴](@entry_id:187094)的距离在增加。为了保持[角动量守恒](@entry_id:156798)（在无外力矩的惯性系中），它的角速度必须减小。但在旋转系看来，圆盘的角速度是恒定的，因此物体看起来在旋转方向上“落后”了，仿佛有一股侧向的力在作用于它——这就是科里奥利力。

科里奥利力的大小为 $2m\Omega v'_{\perp}$，其中 $v'_{\perp}$ 是相对速度在垂直于 $\boldsymbol{\Omega}$ 的平面上的分量。一个非常重要的特性是，科里奥利力从不做功。因为 $\mathbf{F}_{\text{cor}}$ 总是垂直于 $\mathbf{v}'$，所以功率 $P = \mathbf{F}_{\text{cor}} \cdot \mathbf{v}' = 0$。这意味着[科里奥利力](@entry_id:160096)可以改变物体运动的方向，但不能改变其在旋转系中的动能大小 [@problem_id:2049571]。这与[磁场](@entry_id:153296)中[洛伦兹力](@entry_id:145104)对[带电粒子](@entry_id:160311)的作用非常相似。

在旋转圆盘问题中，科里奥利力的效应非常显著。若一个冰球从圆盘中心以初速度 $\mathbf{v}_0$ 射出 [@problem_id:2049590]，在地面惯性系看来，它做的是匀速直线运动。然而，在圆盘上的观察者看来，冰球的轨迹是一条曲线。这是因为冰球在前进的同时，它下方的圆盘也在转动。这个偏转的轨迹，在旋转系中被归因于科里奥利力的作用。通过坐标变换，我们可以精确计算出冰球飞离圆盘时在旋转坐标系中的位置，例如，其 $y'$ 坐标为 $-R \sin(\frac{\Omega R}{v_0})$ [@problem_id:2049590]。

当一个物体同时具有径向位置和[相对速度](@entry_id:178060)时，离心力和科里奥利力会同时作用。例如，一个在旋转圆盘上从点 $(R, 0)$ 爬向点 $(0, R)$ 的昆虫 [@problem_id:2049548]，在其路径中点，它的位置矢量和速度矢量都非零。此时，它会同时受到一个向外的[离心力](@entry_id:173726)和一个侧向的科里奥利力，这两个力的矢量和构成了作用于它的总虚拟力。

### [欧拉力](@entry_id:173795)：变速旋转的效应

最后一种虚拟力只在角速度 $\boldsymbol{\Omega}$ 随时间变化时出现：
$$
\mathbf{F}_{\text{Eu}} = -m\left(\frac{d\boldsymbol{\Omega}}{dt} \times \mathbf{r}'\right)
$$
这被称为**[欧拉力](@entry_id:173795) (Euler force)** 或方位力 (azimuthal force)。它与[角加速度](@entry_id:177192) $\dot{\boldsymbol{\Omega}}$、质量 $m$ 和位置矢量 $\mathbf{r}'$ 有关。它的方向垂直于 $\dot{\boldsymbol{\Omega}}$ 和 $\mathbf{r}'$。

一个简单的例子是正在减速的旋转木马 [@problem_id:2049554]。设旋转木马绕着竖直的 $\hat{k}$ 轴转动，[角速度](@entry_id:192539)为 $\boldsymbol{\Omega} = \Omega(t) \hat{k}$。当施加制动时，[角加速度](@entry_id:177192) $\dot{\Omega}  0$，所以 $\dot{\boldsymbol{\Omega}}$ 指向 $-\hat{k}$ 方向。对于一个位于 $\mathbf{r}' = r \hat{r}$ 的乘客，他所受到的[欧拉力](@entry_id:173795)为 $\mathbf{F}_{\text{Eu}} = -m (\dot{\Omega}\hat{k}) \times (r\hat{r}) = -mr\dot{\Omega}(\hat{k} \times \hat{r}) = -mr\dot{\Omega} \hat{\theta}$。因为 $\dot{\Omega}  0$，所以[欧拉力](@entry_id:173795)的方向是沿着旋转的切向 $(\hat{\theta})$，与旋转方向相同。这解释了为什么在刹车时，乘客会感到一股将他们向[前推](@entry_id:158718)的力。

### 综合效应与[轨迹分析](@entry_id:756092)

在许多实际和理论问题中，多种虚拟力会同时出现，共同决定了物体在[非惯性系](@entry_id:168746)中的运动轨迹。

考虑一个从旋转圆盘上方一定高度 $h$ 处静止释放的冰球（相对于圆盘静止）[@problem_id:2049610]。在释放的瞬间，它在惯性系中具有一个切向速度 $\mathbf{v}_0 = \boldsymbol{\Omega} \times \mathbf{r}_0$。此后，它在[惯性系](@entry_id:266190)中做平抛运动。然而，在圆盘[参考系](@entry_id:169232)中，它的运动轨迹就复杂得多。当它下落时，[科里奥利力](@entry_id:160096)会使其水平轨迹发生偏转。同时，随着它的水平位置变化，离心力的大小和方向也在改变。最终的落点将既有径向的偏移，也有角向的偏移。通过在惯性系中解出运动轨迹，再转换回旋转系，我们可以得到其最终落点坐标 $(r_f, \theta_f)$，这个结果包含了所有虚拟力效应的累积结果 [@problem_id:2049610]。

虚拟力的概念甚至可以推广到更复杂的嵌套旋转系统中 [@problem_id:2049597]。如果一个[参考系](@entry_id:169232) $S'$ 以角速度 $\boldsymbol{\omega}_1$ 相对于另一个[参考系](@entry_id:169232) $S''$ 旋转，而 $S''$ 又以[角速度](@entry_id:192539) $\boldsymbol{\omega}_2$ 相对于[惯性系](@entry_id:266190) $S$ 旋转，那么在 $S''$ 中的观察者分析 $S'$ 中的静止物体时，也需要使用[科里奥利力](@entry_id:160096)。这是因为尽管物体在 $S'$ 中静止，但它相对于 $S''$ 是在运动的，其相对速度为 $\mathbf{v}_{S''} = \boldsymbol{\omega}_1 \times \mathbf{r}$。将这个速度代入 $S''$ 系的科里奥利力公式 $\mathbf{F}_{Cor} = -2m (\boldsymbol{\omega}_2 \times \mathbf{v}_{S''})$，就可以计算出 $S''$ 中的观察者测得的[科里奥利力](@entry_id:160096)。

总之，虚拟力是分析[非惯性系](@entry_id:168746)动力学不可或缺的工具。它们虽然“虚拟”，但其物理效应却是真实可测的，从地球上的[气旋](@entry_id:262310)形成到太空探测器的[轨道](@entry_id:137151)设计，都离不开对这些力的深刻理解。