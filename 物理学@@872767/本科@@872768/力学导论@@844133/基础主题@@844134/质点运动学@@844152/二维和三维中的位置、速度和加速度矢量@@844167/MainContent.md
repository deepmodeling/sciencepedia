## 引言
在物理世界中，从行星的宏伟[轨道](@entry_id:137151)到微观粒子的瞬息轨迹，运动无处不在。要精确地描述和预测这些运动，尤其是在超越简单一维[直线运动](@entry_id:165142)的复杂二维和三维空间中，我们需要一套强大而普适的数学语言。这套语言的核心便是矢量[运动学](@entry_id:173318)，它利用位置、速度和加速度矢量来捕捉物体运动的完整信息，包括其路径、快慢和方向变化。然而，许多初学者往往将这些概念割裂开来，未能深刻理解它们之间基于微积分的内在联系，也难以将这些抽象的矢量工具应用于解决真实世界中的复杂问题。本文旨在弥合这一知识鸿沟。

本文将分为三个部分，带领读者系统地掌握二维和三维运动学。首先，在“原理与机制”一章中，我们将建立矢量运动学的基础，阐明如何通过[微分](@entry_id:158718)和积分来关联位置、速度和加速度，并深入探讨加速度的几何分解及其在分析曲线运动中的关键作用。接着，在“应用与跨学科联系”一章中，我们将展示这些原理如何在机器人学、[天体动力学](@entry_id:176169)、[流体力学](@entry_id:136788)乃至广义相对论等前沿领域中大放异彩，揭示运动学在现代科技中的核心地位。最后，通过“动手实践”部分提供的一系列精心设计的计算问题，您将有机会亲手应用所学知识，巩固并深化对这些核心概念的理解。

## 原理与机制

在导论中，我们建立了描述物体运动需要一个[参考系](@entry_id:169232)的概念。本章将深入探讨运动学的核心矢量：位置、速度和加速度。我们将超越一维[直线运动](@entry_id:165142)的范畴，进入更普适的二维和三维空间。这里的关键在于将这些物理量理解为矢量，并运用矢量微积分的强大工具来揭示它们之间深刻的内在联系。本章将系统地阐述这些基本原理，并展示它们如何解释从天体运行到[机器人导航](@entry_id:263774)等各种复杂现象。

### 运动学的矢量基础：位置、速度与加速度

为了精确描述一个质点在三维空间中的运动轨迹，我们首先需要定义其**位置矢量 (position vector)**。在一个固定的[笛卡尔坐标系](@entry_id:169789)中，[质点](@entry_id:186768)在任意时刻 $t$ 的位置可以用一个从坐标原点指向该[质点](@entry_id:186768)的矢量 $\vec{r}(t)$ 来表示。该矢量可以分解为沿三个[正交基](@entry_id:264024)矢量 $\hat{i}$、$\hat{j}$ 和 $\hat{k}$ 的分量：
$$ \vec{r}(t) = x(t)\hat{i} + y(t)\hat{j} + z(t)\hat{k} $$
其中，$x(t)$、$y(t)$ 和 $z(t)$ 是质点位置坐标随时间变化的函数。

有了位置的瞬时描述，我们自然会问：物体运动得有多快，方向又是指向哪里？这由**[速度矢量](@entry_id:269648) (velocity vector)** $\vec{v}(t)$ 描述，它被严格定义为位置矢量对时间的一阶导数：
$$ \vec{v}(t) = \frac{d\vec{r}}{dt} = \frac{dx}{dt}\hat{i} + \frac{dy}{dt}\hat{j} + \frac{dz}{dt}\hat{k} = v_x(t)\hat{i} + v_y(t)\hat{j} + v_z(t)\hat{k} $$
从这个定义可以看出，速度矢量在任意时刻都与[质点](@entry_id:186768)轨迹的[切线](@entry_id:268870)方向相同。速度矢量的**大小 (magnitude)**，$v = |\vec{v}| = \sqrt{v_x^2 + v_y^2 + v_z^2}$，是我们通常所说的**速率 (speed)**，它是一个标量。

速度的变化则由**加速度矢量 (acceleration vector)** $\vec{a}(t)$ 描述，它被定义为[速度矢量](@entry_id:269648)对时间的一阶导数，也就是位置矢量对时间的[二阶导数](@entry_id:144508)：
$$ \vec{a}(t) = \frac{d\vec{v}}{dt} = \frac{d^2\vec{r}}{dt^2} = \frac{dv_x}{dt}\hat{i} + \frac{dv_y}{dt}\hat{j} + \frac{dv_z}{dt}\hat{k} = a_x(t)\hat{i} + a_y(t)\hat{j} + a_z(t)\hat{k} $$
重要的是要认识到，只要[速度矢量](@entry_id:269648)发生变化——无论是大小还是方向——就一定存在加速度。一个以恒定速率做曲线运动的物体，其速度方向在不断改变，因此它仍然具有加速度。

微积分的对称性告诉我们，正如[微分](@entry_id:158718)联系着位置、速度和加速度，积分则扮演着相反的角色。如果我们知道一个物体从时刻 $t=0$ 到 $t=T$ 的速度函数 $\vec{v}(t)$，我们就可以通过积分来计算其**[位移矢量](@entry_id:262782) (displacement vector)** $\Delta\vec{r}$，即位置矢量的变化量：
$$ \Delta\vec{r} = \vec{r}(T) - \vec{r}(0) = \int_{0}^{T} \vec{v}(t) dt $$
由于[积分的线性](@entry_id:189393)性质，这个矢量积分可以分解为对每个分量的[标量积](@entry_id:138996)分：
$$ \Delta\vec{r} = \left(\int_{0}^{T} v_x(t) dt\right)\hat{i} + \left(\int_{0}^{T} v_y(t) dt\right)\hat{j} + \left(\int_{0}^{T} v_z(t) dt\right)\hat{k} $$

例如，考虑一个在二维平面上测试的自主探测车 [@problem_id:2208699]。假设其速度由 $\vec{v}(t) = (3\alpha t^2 - \beta) \hat{i} + \gamma \cos(\omega t) \hat{j}$ 给出，其中 $\alpha, \beta, \gamma, \omega$ 是常数。为了求出从 $t=0$ 到任意时刻 $T$ 的位移，我们分别对 $x$ 和 $y$ 分量进行积分：
$$ \Delta x = \int_{0}^{T} (3\alpha t^2 - \beta) dt = [\alpha t^3 - \beta t]_{0}^{T} = \alpha T^3 - \beta T $$
$$ \Delta y = \int_{0}^{T} \gamma \cos(\omega t) dt = \left[\frac{\gamma}{\omega} \sin(\omega t)\right]_{0}^{T} = \frac{\gamma}{\omega} \sin(\omega T) $$
因此，总[位移矢量](@entry_id:262782)为 $\Delta\vec{r} = (\alpha T^3 - \beta T)\hat{i} + \frac{\gamma}{\omega} \sin(\omega T) \hat{j}$。

一个特别重要且常见的情形是**[匀加速](@entry_id:268628)运动**，即加[速度矢量](@entry_id:269648) $\vec{a}$ 是一个不随时间变化的常矢量。在这种情况下，通过对常数加速度积分两次，我们可以得到速度和位置的矢量[运动学方程](@entry_id:173032)：
$$ \vec{v}(t) = \vec{v}_0 + \vec{a}t $$
$$ \vec{r}(t) = \vec{r}_0 + \vec{v}_0 t + \frac{1}{2}\vec{a}t^2 $$
其中 $\vec{r}_0$ 和 $\vec{v}_0$ 分别是[质点](@entry_id:186768)在 $t=0$ 时的初始位置和初始速度。这些方程是解决所有[抛体运动](@entry_id:174344)问题的基础。通过这些方程，我们可以探索一些有趣的几何条件，例如在何时质点的位置矢量会与其[速度矢量](@entry_id:269648)垂直 [@problem_id:2208706]。要解决这类问题，只需将上述 $\vec{r}(t)$ 和 $\vec{v}(t)$ 的表达式代入垂直条件 $\vec{r}(t) \cdot \vec{v}(t) = 0$ 中，然后求解关于时间 $t$ 的方程即可。

### 运动的几何学：加速度的分解

加速度的核心作用是改变速度矢量。然而，速度矢量的改变有两种方式：改变其大小（速率）或改变其方向。为了更精细地理解加速度的作用机制，我们通常将其分解为两个相互正交的分量：**[切向加速度](@entry_id:173884) (tangential acceleration)** $\vec{a}_T$ 和**[法向加速度](@entry_id:170071) (normal acceleration)** $\vec{a}_N$。

**[切向加速度](@entry_id:173884)** $\vec{a}_T$ 与速度矢量 $\vec{v}$ 平行（或反平行），它唯一的作用是改变速度的大小，即速率。
**[法向加速度](@entry_id:170071)** $\vec{a}_N$ 与[速度矢量](@entry_id:269648) $\vec{v}$ 垂直，它唯一的作用是改变速度的方向，使物体的轨迹弯曲。

总加速度是这两个分量的矢量和：$\vec{a} = \vec{a}_T + \vec{a}_N$。

如何从给定的 $\vec{v}$ 和 $\vec{a}$ 中求出这两个分量呢？我们可以利用矢量投影的思想 [@problem_id:2208705]。[切向加速度](@entry_id:173884) $\vec{a}_T$ 本质上就是总加速度 $\vec{a}$ 在速度方向上的投影。速度方向的单位矢量是 $\hat{u}_T = \vec{v}/|\vec{v}|$。因此，$\vec{a}_T$ 可以表示为：
$$ \vec{a}_T = (\vec{a} \cdot \hat{u}_T) \hat{u}_T = \frac{\vec{a} \cdot \vec{v}}{|\vec{v}|^2} \vec{v} $$
这个表达式优雅地捕捉了[切向加速度](@entry_id:173884)的本质。其大小 $a_T = |\vec{a} \cdot \hat{u}_T| = \frac{|\vec{a} \cdot \vec{v}|}{|\vec{v}|}$。

一旦求出了切向分量，法向分量就可以通过矢量减法轻易得到：
$$ \vec{a}_N = \vec{a} - \vec{a}_T = \vec{a} - \frac{\vec{a} \cdot \vec{v}}{|\vec{v}|^2} \vec{v} $$
我们可以验证 $\vec{a}_N \cdot \vec{v} = 0$，证明其确实与速度方向垂直。

[切向加速度](@entry_id:173884)的大小与速率的变化率直接相关。让我们对速率的平方 $v^2 = \vec{v} \cdot \vec{v}$ 求时间导数：
$$ \frac{d}{dt}(v^2) = \frac{d}{dt}(\vec{v} \cdot \vec{v}) = \frac{d\vec{v}}{dt} \cdot \vec{v} + \vec{v} \cdot \frac{d\vec{v}}{dt} = 2(\vec{a} \cdot \vec{v}) $$
同时，$\frac{d}{dt}(v^2) = 2v \frac{dv}{dt}$。比较两式可得：
$$ \frac{dv}{dt} = \frac{\vec{a} \cdot \vec{v}}{v} = \vec{a} \cdot \frac{\vec{v}}{v} = \vec{a} \cdot \hat{u}_T $$
这正是[切向加速度](@entry_id:173884) $\vec{a}_T$ 在 $\vec{v}$ 方向上的分量值。因此，$\frac{dv}{dt} = a_T$（若 $\vec{a}_T$ 与 $\vec{v}$ 同向）或 $\frac{dv}{dt} = -a_T$（若反向）。这清晰地表明，只有[切向加速度](@entry_id:173884)才能改变物体的速率。

这个结论在能量方面有直接的体现。质点的动能为 $K = \frac{1}{2}mv^2$。其对时间的变化率为：
$$ \frac{dK}{dt} = m v \frac{dv}{dt} = m v a_T = m \vec{a}_T \cdot \vec{v} $$
因为 $\vec{a}_N$ 与 $\vec{v}$ 垂直，所以 $\vec{a}_N \cdot \vec{v} = 0$。因此，我们有 $\frac{dK}{dt} = m (\vec{a}_T + \vec{a}_N) \cdot \vec{v} = m \vec{a} \cdot \vec{v}$。这表明，动能的变化率（即功率）只取决于加速度在速度方向上的分量。[法向加速度](@entry_id:170071)不对物体做功，不改变其动能 [@problem_id:2208708]。例如，在[磁场](@entry_id:153296)中运动的[带电粒子](@entry_id:160311)所受的洛伦兹力总是垂直于其速度，因此[磁场](@entry_id:153296)只能改变粒子的运动方向而不能改变其动能。

### 典型运动分析：从[匀速圆周运动](@entry_id:178264)到一般曲线运动

加速度分解的概念在分析曲线运动时尤其有用。

最简单的曲线运动是**[匀速圆周运动](@entry_id:178264)**。考虑一个传感器附着在半径为 $R$ 的飞轮边缘，[飞轮](@entry_id:195849)以恒定角速度 $\omega$ 转动 [@problem_id:2208677]。若 $t=0$ 时传感器在 $(R, 0)$，其位置矢量可以表示为：
$$ \vec{r}(t) = R\cos(\omega t)\hat{i} + R\sin(\omega t)\hat{j} $$
对其求导得到[速度矢量](@entry_id:269648)：
$$ \vec{v}(t) = -R\omega\sin(\omega t)\hat{i} + R\omega\cos(\omega t)\hat{j} $$
其速率为 $|\vec{v}| = \sqrt{(-R\omega\sin(\omega t))^2 + (R\omega\cos(\omega t))^2} = R\omega$，是一个常数，这正是“匀速”的含义。

再次求导得到加[速度矢量](@entry_id:269648)：
$$ \vec{a}(t) = -R\omega^2\cos(\omega t)\hat{i} - R\omega^2\sin(\omega t)\hat{j} = -\omega^2 \vec{r}(t) $$
这个结果非常重要。它表明，在[匀速圆周运动](@entry_id:178264)中，加速度矢量的大小恒为 $a = \omega^2 R = v^2/R$，并且其方向始终指向圆心（与位置矢量 $\vec{r}$ 方向相反）。这种加速度被称为**[向心加速度](@entry_id:190458)**。由于加速度始终存在且不为零，即使速率恒定，[速度矢量](@entry_id:269648)也绝非恒定。

在这个例子中，我们可以计算 $\vec{a} \cdot \vec{v}$：
$$ \vec{a} \cdot \vec{v} = (-\omega^2 \vec{r}) \cdot \vec{v} = (-R\omega^2\cos(\omega t))(-R\omega\sin(\omega t)) + (-R\omega^2\sin(\omega t))(R\omega\cos(\omega t)) = 0 $$
由于 $\vec{a} \cdot \vec{v} = 0$，根据我们之前的推导，[切向加速度](@entry_id:173884) $a_T = 0$。这意味着总加速度完全是[法向加速度](@entry_id:170071)，即 $\vec{a} = \vec{a}_N$。这与我们的预期完全一致：[匀速圆周运动](@entry_id:178264)的加速度只负责改变方向，而不改变速率。

对于一般的**曲线运动**，在任意一点的轨迹都可以用一个“瞬时”圆来近似，这个圆被称为**[密切圆](@entry_id:169863) (osculating circle)**。[密切圆](@entry_id:169863)的半径被称为**[曲率半径](@entry_id:274690) (radius of curvature)** $\rho$。[法向加速度](@entry_id:170071)的大小与速率和曲率半径的关系，与[匀速圆周运动](@entry_id:178264)完全相同：
$$ a_N = \frac{v^2}{\rho} $$
这个关系式极其有用，它将运动的动力学量（[法向加速度](@entry_id:170071)）与轨迹的纯几何量（[曲率半径](@entry_id:274690)）联系起来。因此，如果我们能计算出 $a_N$ 和 $v$，就能确定质点轨迹在该点的弯曲程度：
$$ \rho = \frac{v^2}{a_N} = \frac{|\vec{v}|^2}{|\vec{a}_N|} = \frac{|\vec{v}|^2}{|\vec{a} - \vec{a}_T|} = \frac{|\vec{v}|^2}{\sqrt{|\vec{a}|^2 - a_T^2}} $$

在某些特殊情况下，计算会变得更简单。例如，在一个假想的探测器导航问题中 [@problem_id:2208707]，我们需要在加速度矢量恰好与[速度矢量](@entry_id:269648)垂直的瞬间计算曲率半径。在这个特殊时刻 $t_*$，我们有 $\vec{a}(t_*) \cdot \vec{v}(t_*) = 0$。这意味着该时刻的[切向加速度](@entry_id:173884) $a_T$ 为零，总加速度就是[法向加速度](@entry_id:170071)，即 $\vec{a}(t_*) = \vec{a}_N(t_*)$。因此，曲率半径的计算公式简化为：
$$ \rho = \frac{|\vec{v}(t_*)|^2}{|\vec{a}(t_*)|} $$
这使得我们只需计算在该特定时刻的速度和加速度的大小，即可求得曲率半径。

### [运动约束](@entry_id:168736)与守恒律

在许多物理问题中，质点的运动受到几何形状的约束，或者受到的作用力具有特殊的对称性。这些情况往往会导致一些简洁而深刻的[运动学](@entry_id:173318)关系或守恒律。

一个典型的例子是**中心力场中的运动**，即[质点](@entry_id:186768)所受的加速度始终指向或背离一个固定的[中心点](@entry_id:636820)（例如行星绕太阳运动）。在这种情况下，加速度矢量 $\vec{a}(t)$ 始终与位置矢量 $\vec{r}(t)$ 共线 [@problem_id:2208694]。让我们来考察一个重要的物理量 $\vec{\Omega}(t) = \vec{r}(t) \times \vec{v}(t)$，它与质点的角动量成正比。我们来计算它对时间的导数，利用矢量叉乘的[求导法则](@entry_id:145443)：
$$ \frac{d\vec{\Omega}}{dt} = \frac{d}{dt}(\vec{r} \times \vec{v}) = \left(\frac{d\vec{r}}{dt} \times \vec{v}\right) + \left(\vec{r} \times \frac{d\vec{v}}{dt}\right) $$
根据定义，$\frac{d\vec{r}}{dt} = \vec{v}$ 且 $\frac{d\vec{v}}{dt} = \vec{a}$。因此：
$$ \frac{d\vec{\Omega}}{dt} = (\vec{v} \times \vec{v}) + (\vec{r} \times \vec{a}) $$
任何矢量与自身的叉乘都为零，所以 $\vec{v} \times \vec{v} = \vec{0}$。又因为 $\vec{a}$ 与 $\vec{r}$ 共线，它们之间的叉乘也为零，即 $\vec{r} \times \vec{a} = \vec{0}$。最终我们得到一个非凡的结论：
$$ \frac{d\vec{\Omega}}{dt} = \vec{0} $$
这意味着矢量 $\vec{\Omega} = \vec{r} \times \vec{v}$ 是一个不随时间改变的**[守恒量](@entry_id:150267)**。这个守恒律蕴含着丰富的物理意义：首先，由于 $\vec{r}$ 和 $\vec{v}$ 始终垂直于常矢量 $\vec{\Omega}$，[质点](@entry_id:186768)的运动被限制在一个固定的平面内。其次，它直接导出了[开普勒第二定律](@entry_id:178684)，即行星与太阳的连线在相等的时间内扫过相等的面积。

另一个例子是**受几何约束的运动**。考虑一个探测器被限制在一个以原点为中心的球形容器表面上运动 [@problem_id:2208690]。这个约束的数学表达是，其位置矢量的模长始终为常数 $R$，即 $|\vec{r}(t)| = R$。我们可以利用这个约束来推导运动学关系。将约束写为 $\vec{r} \cdot \vec{r} = R^2$，然后对时间求导：
$$ \frac{d}{dt}(\vec{r} \cdot \vec{r}) = \vec{v} \cdot \vec{r} + \vec{r} \cdot \vec{v} = 2(\vec{r} \cdot \vec{v}) = \frac{d}{dt}(R^2) = 0 $$
由此得到 $\vec{r} \cdot \vec{v} = 0$。这个结果在几何上是显然的：在球面上运动的物体的速度矢量必须时刻与从球心指向它的位置矢量相切（即垂直）。

现在，让我们再次对 $\vec{r} \cdot \vec{v} = 0$ 求导：
$$ \frac{d}{dt}(\vec{r} \cdot \vec{v}) = \frac{d\vec{r}}{dt} \cdot \vec{v} + \vec{r} \cdot \frac{d\vec{v}}{dt} = \vec{v} \cdot \vec{v} + \vec{r} \cdot \vec{a} = 0 $$
这给出了一个非常强大的关系式：
$$ v^2 = -\vec{r} \cdot \vec{a} $$
这个等式允许我们在只知道位置和加速度的情况下，直接计算出物体的速率平方，而无需知道速度矢量的具体分量。例如，在问题 [@problem_id:2208690] 中，通过测量探测器在某瞬间的 $\vec{r}$ 和 $\vec{a}$，就可以利用这个公式计算其 $v^2$，进而求出其动能 $K = \frac{1}{2} m v^2 = -\frac{1}{2} m (\vec{r} \cdot \vec{a})$。这完美地展示了如何从几何约束中提炼出实用的动力学信息。

### 高级主题：场中的加速度与旋转参考系

矢量[运动学](@entry_id:173318)的原理还可以扩展到更复杂的场景，例如在流体场中的运动或在[非惯性参考系](@entry_id:169712)中的观察。

**场中的加速度**

考虑一个微小粒子在稳定的流体中运动，其速度在任意时刻都等于其所在位置的[流体速度](@entry_id:267320) [@problem_id:2208681]。这意味着粒子的速度不仅仅是时间的函数，它还依赖于其空间位置 $\vec{r}$，即 $\vec{v} = \vec{v}(\vec{r}(t))$。在这种情况下，粒子的加速度是什么？我们必须使用[链式法则](@entry_id:190743)来求导：
$$ \vec{a}(t) = \frac{d\vec{v}}{dt}(\vec{r}(t)) $$
对于 $\vec{v}(x, y, z)$，其[全微分](@entry_id:171747)是 $d\vec{v} = \frac{\partial\vec{v}}{\partial x}dx + \frac{\partial\vec{v}}{\partial y}dy + \frac{\partial\vec{v}}{\partial z}dz$。除以 $dt$ 得到：
$$ \vec{a} = \frac{d\vec{v}}{dt} = \frac{\partial\vec{v}}{\partial x}\frac{dx}{dt} + \frac{\partial\vec{v}}{\partial y}\frac{dy}{dt} + \frac{\partial\vec{v}}{\partial z}\frac{dz}{dt} $$
注意到 $\frac{dx}{dt} = v_x$, $\frac{dy}{dt} = v_y$, $\frac{dz}{dt} = v_z$，所以上式可以写成一个紧凑的矢量形式：
$$ \vec{a} = (v_x \frac{\partial}{\partial x} + v_y \frac{\partial}{\partial y} + v_z \frac{\partial}{\partial z})\vec{v} = (\vec{v} \cdot \nabla)\vec{v} $$
这个加速度被称为**[对流加速度](@entry_id:263153) (convective acceleration)**。它揭示了一个深刻的概念：即使速度场 $\vec{v}(\vec{r})$ 本身不随时间变化（即 $\frac{\partial\vec{v}}{\partial t} = 0$），在场中穿行的粒子仍然可以经历加速度，因为它从一个速度较低的区域移动到了一个速度较高的区域（或速度方向不同的区域）。这是[流体力学](@entry_id:136788)中[拉格朗日描述](@entry_id:264498)（跟随粒子）和[欧拉描述](@entry_id:264722)（观察定点）之间的关键区别。

**[旋转参考系](@entry_id:174154)中的加速度**

另一个高级主题是在**[非惯性参考系](@entry_id:169712)**中描述运动，特别是**旋转参考系**。假设一个[参考系](@entry_id:169232) S' 以恒定角速度 $\vec{\omega}$ 相对于一个[惯性系](@entry_id:266190) S 旋转。对于任意一个矢量 $\vec{Q}$，它在两个[参考系](@entry_id:169232)中的时间导数满足如下关系：
$$ \left(\frac{d\vec{Q}}{dt}\right)_{S} = \left(\frac{d\vec{Q}}{dt}\right)_{S'} + \vec{\omega} \times \vec{Q} $$
这个公式是联系两个[参考系](@entry_id:169232)的关键。将此规则应用于位置矢量 $\vec{r}$，我们可以得到两个[参考系](@entry_id:169232)中[速度矢量](@entry_id:269648)的关系：
$$ \vec{v}_S = \vec{v}_{S'} + \vec{\omega} \times \vec{r} $$
其中 $\vec{v}_S$ 是在[惯性系](@entry_id:266190)中测得的“真实”速度，$\vec{v}_{S'}$ 是在旋转系中测得的速度。

为了得到加速度的关系，我们必须再次应用这个[求导法则](@entry_id:145443)，这次是对[速度矢量](@entry_id:269648) $\vec{v}_S$ 进行操作：
$$ \vec{a}_S = \left(\frac{d\vec{v}_S}{dt}\right)_{S} = \left(\frac{d}{dt}(\vec{v}_{S'} + \vec{\omega} \times \vec{r})\right)_{S'} + \vec{\omega} \times (\vec{v}_{S'} + \vec{\omega} \times \vec{r}) $$
展开并整理后，我们得到最终的加[速度变换](@entry_id:265594)公式：
$$ \vec{a}_S = \vec{a}_{S'} + 2(\vec{\omega} \times \vec{v}_{S'}) + \vec{\omega} \times (\vec{\omega} \times \vec{r}) $$
这个公式极为重要。它表明，在[惯性系](@entry_id:266190)中测得的真实加速度 $\vec{a}_S$ 是由三部分组成的：
1.  $\vec{a}_{S'}$：在旋转系中观察到的加速度。
2.  $2(\vec{\omega} \times \vec{v}_{S'})$：**[科里奥利加速度](@entry_id:171639) (Coriolis acceleration)**，它只在物体相对于旋转系运动时（$\vec{v}_{S'} \neq 0$）才存在。
3.  $\vec{\omega} \times (\vec{\omega} \times \vec{r})$：**向心加速度 (centripetal acceleration)**，它取决于物体在旋转系中的位置，即使物体在旋转系中静止，它也存在。

在处理地球自转、陀螺仪或如问题 [@problem_id:2208698] 中描述的在旋转平台上运动的珠子等问题时，这个公式是必不可少的。通过仔细计算这三个矢量项，我们可以将在[非惯性系](@entry_id:168746)中观察到的看似复杂的运动，还原为其在[惯性系](@entry_id:266190)中遵循牛顿定律的真实动力学过程。