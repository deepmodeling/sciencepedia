## 引言
[分析力学](@entry_id:166738)为我们提供了一套优雅而强大的工具，用于超越传统[牛顿力学](@entry_id:162125)的矢量方法来理解物理世界。其中，核心议题之一便是如何描述一个不受外力的“自由”粒子在不同观测视角下的运动。虽然在标准的[笛卡尔坐标系](@entry_id:169789)中，[自由粒子](@entry_id:148748)的匀速[直线运动](@entry_id:165142)定律看似简单，但当我们将视角切换到旋转的平台、加速的航天器，或使用弯曲的[坐标系](@entry_id:156346)来描述受几何约束的运动时，问题变得异常复杂。牛顿方法此时需要复杂的力分解和几何构想，而[拉格朗日形式](@entry_id:145697)体系则揭示了一条更为普适和深刻的路径。

本文旨在系统地阐述如何运用[拉格朗日力学](@entry_id:147054)来分析[自由粒子](@entry_id:148748)在各种[坐标系](@entry_id:156346)和[非惯性参考系](@entry_id:169712)中的动力学行为。读者将通过三个核心章节的学习，逐步掌握这一强大的分析方法：
- 在**“原理与机制”**一章中，我们将深入探讨拉格朗日量的坐标协变性，理解[广义坐标](@entry_id:156576)、[度规张量](@entry_id:160222)，以及对称性如何引出[守恒定律](@entry_id:269268)，并系统推导[非惯性系](@entry_id:168746)中的[惯性力](@entry_id:169104)。
- 在**“应用与跨学科联系”**一章中，我们将展示这些原理如何应用于描述[曲面上的测地线](@entry_id:190974)运动、解决工程中的约束问题，并揭示其与广义相对论、计算化学等现代科学领域的深刻联系。
- 最后，在**“动手实践”**部分，读者将通过解决具体的物理问题，将理论知识转化为实际的分析技能。

通过本文的学习，我们将从根本上理解，一个“自由”粒子的运动轨迹如何蕴含着其所在空间的几何结构以及观察者自身的运动状态。

## 原理与机制

在上一章中，我们为[分析力学](@entry_id:166738)的研究奠定了基础。现在，我们将深入探讨[自由粒子](@entry_id:148748)在各种[坐标系](@entry_id:156346)和[非惯性参考系](@entry_id:169712)中运动的描述。本章的核心在于展示[拉格朗日形式](@entry_id:145697)体系的强大威力，即其在[坐标变换](@entry_id:172727)下的[协变](@entry_id:634097)性。对于一个不受外力的**[自由粒子](@entry_id:148748)**，其[拉格朗日量](@entry_id:174593)等于其动能，$L=T$。虽然这个表述在笛卡尔坐标系下形式简单，但当我们转向更复杂的[坐标系](@entry_id:156346)或[非惯性参考系](@entry_id:169712)时，其深刻的内涵和强大的应用价值才得以真正彰显。我们将系统地探索如何选择合适的坐标来简化问题，如何从系统的对称性中发现[守恒量](@entry_id:150267)，以及如何处理在加速或转动[参考系](@entry_id:169232)中观察到的运动。

### [广义坐标](@entry_id:156576)与动能

在[笛卡尔坐标系](@entry_id:169789)中，一个质量为 $m$ 的自由粒子的动能表达式是众所周知的：$T = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2 + \dot{z}^2)$。然而，许多物理问题由于其内在的几何约束或对称性，使用非[笛卡尔坐标系](@entry_id:169789)（如极坐标、球坐标或柱坐标）会更为便捷。这些[坐标系](@entry_id:156346)以及其他任何能唯一确定系统位形的独立参数集合，统称为**[广义坐标](@entry_id:156576)**，记为 $q_1, q_2, \dots, q_n$。

我们的首要任务，是将在[笛卡尔坐标系](@entry_id:169789)下定义的动能，用[广义坐标](@entry_id:156576)及其时间导数（即**[广义速度](@entry_id:178456)** $\dot{q}_i$）来表示。这可以通过[坐标变换](@entry_id:172727)关系 $x_i = x_i(q_1, \dots, q_n, t)$ 实现。利用链式法则对时间求导，我们得到笛卡尔速度分量与[广义速度](@entry_id:178456)之间的关系：
$$
\dot{x}_i = \sum_{j=1}^{n} \frac{\partial x_i}{\partial q_j} \dot{q}_j + \frac{\partial x_i}{\partial t}
$$
将此表达式代入动能公式 $T = \frac{1}{2}m \sum_i \dot{x}_i^2$，经过展开后，动能通常可以写成[广义速度](@entry_id:178456)的二次型、线性项和常数项之和：$T = T_2 + T_1 + T_0$。其中 $T_2$ 是关于 $\dot{q}_j$ 的二次齐次式，$T_1$ 是线性项，$T_0$ 是不含[广义速度](@entry_id:178456)的项。如果[坐标变换](@entry_id:172727)不显含时间（即 $\frac{\partial x_i}{\partial t} = 0$），则动能简化为仅包含二次项的齐次二次式。

为了具体说明这个过程，让我们考虑一个在二维平面内运动的粒子 [@problem_id:2033471]。其位置由笛卡尔坐标 $(x, y)$ 或一组非标准的[广义坐标](@entry_id:156576) $(u, v)$ 描述，变换关系为：
$$
x = uv, \quad y = \frac{1}{2}(v^2 - u^2)
$$
假设粒子的运动轨迹由 $u(t) = u_0$ 和 $v(t) = \alpha t$ 给出，其中 $u_0$ 和 $\alpha$ 是常数。为了计算动能 $T = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)$，我们首先需要计算 $\dot{x}$ 和 $\dot{y}$。应用[链式法则](@entry_id:190743)：
$$
\dot{x} = \frac{\partial x}{\partial u}\dot{u} + \frac{\partial x}{\partial v}\dot{v} = v\dot{u} + u\dot{v}
$$
$$
\dot{y} = \frac{\partial y}{\partial u}\dot{u} + \frac{\partial y}{\partial v}\dot{v} = -u\dot{u} + v\dot{v}
$$
根据给定的[运动学](@entry_id:173318)关系，$u(t)=u_0$ 意味着 $\dot{u}=0$，$v(t)=\alpha t$ 意味着 $\dot{v}=\alpha$。代入上述表达式，我们得到：
$$
\dot{x} = (\alpha t)(0) + (u_0)(\alpha) = \alpha u_0
$$
$$
\dot{y} = (-u_0)(0) + (\alpha t)(\alpha) = \alpha^2 t
$$
于是，粒子的动能随时间变化的函数为：
$$
T(t) = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) = \frac{1}{2}m\left((\alpha u_0)^2 + (\alpha^2 t)^2\right) = \frac{m}{2}(\alpha^2 u_0^2 + \alpha^4 t^2)
$$
这个例子清晰地展示了，即便在不熟悉的[坐标系](@entry_id:156346)中，只要坐标变换关系已知，我们总能通过系统性的计算，得到以[广义坐标](@entry_id:156576)表示的动能表达式。

### [度规张量](@entry_id:160222)与运动的几何

上一节的推导揭示了一个更深层次的结构。对于不显含时间的[坐标变换](@entry_id:172727)，动能可以普遍地写成：
$$
T = \frac{1}{2}m \sum_{i,j} \left( \sum_k \frac{\partial x_k}{\partial q_i} \frac{\partial x_k}{\partial q_j} \right) \dot{q}_i \dot{q}_j
$$
括号中的项定义了一个重要的对象，称为**度规张量** (metric tensor)，其分量记为 $g_{ij}(q)$：
$$
g_{ij}(q) = \sum_k \frac{\partial x_k}{\partial q_i} \frac{\partial x_k}{\partial q_j}
$$
于是，动能的表达式变得异常简洁：
$$
T = \frac{1}{2}m \sum_{i,j} g_{ij} \dot{q}_i \dot{q}_j
$$
度规张量 $g_{ij}$ 编码了[广义坐标](@entry_id:156576)系下空间的局部几何性质。它直接关联到空间中两邻近点间距离的平方，即弧元平方 $ds^2$：
$$
ds^2 = \sum_k dx_k^2 = \sum_k \left(\sum_i \frac{\partial x_k}{\partial q_i} dq_i\right) \left(\sum_j \frac{\partial x_k}{\partial q_j} dq_j\right) = \sum_{i,j} g_{ij} dq_i dq_j
$$
这个关系说明，粒子的动能本质上是由其运动空间的几何结构决定的。[拉格朗日力学](@entry_id:147054)的优越性在于，我们只需知道度规张量 $g_{ij}$，就可以写出[拉格朗日量](@entry_id:174593)，而无需退回到最初的笛卡尔坐标系。

考虑一个二维平面上的通用线性坐标变换 [@problem_id:2033472]：
$$
q_1 = ax + by, \quad q_2 = cx + dy
$$
其中 $a,b,c,d$ 是常数且 $ad-bc \neq 0$ 以保证变换可逆。为了求出 $(q_1, q_2)$ [坐标系](@entry_id:156346)下的度规张量，我们需要反向表示 $x, y$：
$$
\begin{pmatrix} x \\ y \end{pmatrix} = \frac{1}{ad-bc} \begin{pmatrix} d & -b \\ -c & a \end{pmatrix} \begin{pmatrix} q_1 \\ q_2 \end{pmatrix}
$$
由此可得 $x = \frac{d q_1 - b q_2}{ad-bc}$ 和 $y = \frac{-c q_1 + a q_2}{ad-bc}$。现在我们可以计算[偏导数](@entry_id:146280)，例如 $\frac{\partial x}{\partial q_1} = \frac{d}{ad-bc}$，$\frac{\partial y}{\partial q_1} = \frac{-c}{ad-bc}$，等等。代入[度规张量](@entry_id:160222)的定义 $g_{ij} = \frac{\partial x}{\partial q_i}\frac{\partial x}{\partial q_j} + \frac{\partial y}{\partial q_i}\frac{\partial y}{\partial q_j}$，经过计算可得：
$$
g = \frac{1}{(ad-bc)^2} \begin{pmatrix} d^2+c^2 & -(ac+bd) \\ -(ac+bd) & a^2+b^2 \end{pmatrix}
$$
这个结果表明，即便是简单的[线性变换](@entry_id:149133)，也可能引入非对角项 ($g_{12} \neq 0$)，意味着新坐标轴不是正交的。

[拉格朗日形式](@entry_id:145697)体系的普适性甚至允许我们处理[非欧几里得几何](@entry_id:198138)。例如，在一个具有[恒定曲率](@entry_id:162122)的空间中，弧元可以用特定形式的度规来描述。考虑一个由度规 $ds^2 = \frac{dr^2}{1-kr^2} + r^2 d\theta^2$ 定义的二维[曲面](@entry_id:267450) [@problem_id:2033482]。自由粒子在该[曲面](@entry_id:267450)上的[拉格朗日量](@entry_id:174593)就是：
$$
L = T = \frac{1}{2}m\left(\frac{\dot{r}^2}{1-kr^2} + r^2\dot{\theta}^2\right)
$$
尽管这个空间不是我们熟悉的[平直空间](@entry_id:204618)，[拉格朗日力学](@entry_id:147054)的套路依然完全适用，我们可以直接从此出发分析其动力学，这正是该方法的强大之处。

### [对称性与守恒](@entry_id:154858)定律

[分析力学](@entry_id:166738)最深刻、最有力的结果之一，是它揭示了系统的**对称性** (symmetry) 与**[守恒定律](@entry_id:269268)** (conservation law) 之间的内在联系。这个联系通过[拉格朗日方程](@entry_id:175419)得以清晰地展现：
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_i}\right) - \frac{\partial L}{\partial q_i} = 0
$$
如果拉格朗日量 $L$ 不显式地依赖于某个[广义坐标](@entry_id:156576) $q_k$（即 $\frac{\partial L}{\partial q_k} = 0$），那么该坐标就被称为**[循环坐标](@entry_id:166220)** (cyclic coordinate)。对于[循环坐标](@entry_id:166220)，[拉格朗日方程](@entry_id:175419)简化为：
$$
\frac{d}{dt}\left(\frac{\partial L}{\partial \dot{q}_k}\right) = 0
$$
这表明，与[循环坐标](@entry_id:166220) $q_k$ 共轭的**[广义动量](@entry_id:165699)** (generalized momentum) $p_k = \frac{\partial L}{\partial \dot{q}_k}$ 是一个不随时间变化的[守恒量](@entry_id:150267)。

物理上，一个坐标成为[循环坐标](@entry_id:166220)，意味着系统在该坐标对应的变换下具有[不变性](@entry_id:140168)或对称性。例如，如果拉格朗日量与坐标 $x$ 无关，则系统在沿 $x$ 方向的平移下保持不变，其结果是 $x$ 方向的动量 $p_x$ 守恒。如果[拉格朗日量](@entry_id:174593)与角度 $\phi$ 无关，则系统在绕某轴的转动下保持不变，其结果是角动量的相应分量 $p_\phi$ 守恒。

让我们考察一个在二维平面上运动的自由粒子 [@problem_id:2033439]。其拉格朗日量为 $L = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)$。显然，$x$ 和 $y$ 都是[循环坐标](@entry_id:166220)，对应动量 $p_x = m\dot{x}$ 和 $p_y = m\dot{y}$ 守恒。现在，我们换用一个旋转了 $\theta$ 角的[坐标系](@entry_id:156346) $(q_1, q_2)$：
$$
q_1 = x\cos\theta + y\sin\theta, \quad q_2 = -x\sin\theta + y\cos\theta
$$
由于动能（即[拉格朗日量](@entry_id:174593)）在[坐标旋转](@entry_id:164444)下是不变的，我们可以将其写为 $L = \frac{1}{2}m(\dot{q}_1^2 + \dot{q}_2^2)$。在这个新[坐标系](@entry_id:156346)中，$q_1$ 和 $q_2$ 显然也是[循环坐标](@entry_id:166220)。与 $q_1$ 共轭的动量为：
$$
p_1 = \frac{\partial L}{\partial \dot{q}_1} = m\dot{q}_1
$$
将 $\dot{q}_1 = \dot{x}\cos\theta + \dot{y}\sin\theta$ 代入，我们得到 $p_1 = m(\dot{x}\cos\theta + \dot{y}\sin\theta)$。这是一个守恒量。这个表达式恰好是原笛卡尔动量矢量 $\vec{p} = (p_x, p_y)$ 在新的 $q_1$ 轴上的投影。

这个原理在处理受约束的系统时同样强大。考虑一个珠子被限制在绕 $z$ 轴旋转的[抛物面](@entry_id:264713) $z=a\rho^2$ 上运动 [@problem_id:2033415]。在[柱坐标](@entry_id:271645) $(\rho, \phi, z)$ 中，由于约束，$z$ 和 $\rho$ 是关联的，我们可以用 $\rho$ 和 $\phi$ 作为[广义坐标](@entry_id:156576)。系统的动能和[势能](@entry_id:748988)分别为：
$$
T = \frac{m}{2}(\dot{\rho}^2 + \rho^2\dot{\phi}^2 + \dot{z}^2) = \frac{m}{2}((1+4a^2\rho^2)\dot{\rho}^2 + \rho^2\dot{\phi}^2)
$$
$$
V = mgz = mga\rho^2
$$
[拉格朗日量](@entry_id:174593) $L=T-V$ 显式地依赖于 $\rho$ 和 $\dot{\rho}$，但不依赖于 $\phi$。因此，$\phi$ 是一个[循环坐标](@entry_id:166220)。对应的守恒的[广义动量](@entry_id:165699)为：
$$
p_\phi = \frac{\partial L}{\partial \dot{\phi}} = m\rho^2\dot{\phi}
$$
这个守恒量正是粒子绕 $z$ 轴的角动量。利用给定的[初始条件](@entry_id:152863) $m=1.50\,\text{kg}$, $\rho(0)=2.00\,\text{m}$, $\dot{\phi}(0)=2.00\,\text{rad/s}$，我们可以计算出该[守恒量](@entry_id:150267)的值为 $p_\phi = 1.50 \times (2.00)^2 \times 2.00 = 12.0\,\text{kg}\cdot\text{m}^2/\text{s}$。

这个思想可以推广到任何绕 $z$ 轴的[旋转曲面](@entry_id:261378)。对于一个被约束在[轴对称](@entry_id:173333)[曲面](@entry_id:267450) $\rho=\rho(z)$ 上运动的粒子，只要作用于其上的外力（如重力）也具有轴对称性，角坐标 $\phi$ 就总是[循环坐标](@entry_id:166220)，导致角动量的 $z$ 分量 $p_\phi = m\rho^2\dot{\phi}$ 守恒 [@problem_id:2033429]。这个守恒律可以写成一个更具几何意义的形式，即**[克莱罗关系](@entry_id:159248)** (Clairaut's relation)。粒子的速度矢量 $\vec{v}$ 可以分解为沿着子午线（$\phi$ 不变）方向的分量 $v_m$ 和沿着[方位角](@entry_id:164011)（纬线）方向的分量 $v_\phi = \rho\dot{\phi}$。设 $\psi$ 为[速度矢量](@entry_id:269648)与子午线方向的夹角，则 $\sin\psi = v_\phi/v$，其中 $v$ 是总速率。因此，[角动量守恒](@entry_id:156798)可以写成：
$$
m\rho v_\phi = m\rho (v \sin\psi) = \text{常数}
$$
这个优雅的关系式 $\rho \sin\psi = \text{常数}$ 刻画了粒子在任意[旋转曲面](@entry_id:261378)上的运动轨迹特性。例如，在双曲面上，它决定了粒子在接近最窄处（“颈部”）时其轨迹与子午线的夹角。

### [非惯性系](@entry_id:168746)中的运动

牛顿定律的简洁形式只在[惯性参考系](@entry_id:276742)中成立。然而，我们常常需要在[非惯性参考系](@entry_id:169712)（即相对于[惯性系](@entry_id:266190)在做加速运动的[参考系](@entry_id:169232)）中分析问题，例如在地球上或航天器内。在[非惯性系](@entry_id:168746)中观察一个“自由”的粒子，会发现它似乎受到了力的作用。这些力并非来自与其他物体的相互作用，而是观察者自身加速运动的体现，因此被称为**惯性力** (inertial forces) 或**[虚拟力](@entry_id:165088)** (fictitious forces)。

[拉格朗日方法](@entry_id:142825)为处理[非惯性系](@entry_id:168746)提供了一个统一而强大的框架。基本策略是：首先在惯性系中写下粒子的[拉格朗日量](@entry_id:174593)（对于[自由粒子](@entry_id:148748)就是动能），然后通过[坐标变换](@entry_id:172727)，将[拉格朗日量](@entry_id:174593)用[非惯性系](@entry_id:168746)的坐标和速度来表示。最后，在[非惯性系](@entry_id:168746)坐标下应用[拉格朗日方程](@entry_id:175419)，方程中自然会涌现出描述惯性力的项。

#### 线性[加速参考系](@entry_id:168026)

最简单的[非惯性系](@entry_id:168746)是纯平动的[参考系](@entry_id:169232)。设惯性系为 $S$，[非惯性系](@entry_id:168746)为 $S'$。$S'$ 的原点相对于 $S$ 的原点的位置矢量为 $\vec{R}(t)$，$S'$ 的坐标轴与 $S$ 的坐标轴始终保持平行。那么，一个粒子在两个[参考系](@entry_id:169232)中的位置矢量 $\vec{r}$ 和 $\vec{r}'$ 满足关系 $\vec{r}(t) = \vec{R}(t) + \vec{r}'(t)$。

对时间求导，得到速度关系 $\dot{\vec{r}} = \dot{\vec{R}} + \dot{\vec{r}}'$。自由粒子在[惯性系](@entry_id:266190) $S$ 中的[拉格朗日量](@entry_id:174593)为：
$$
L = T = \frac{1}{2}m\dot{\vec{r}}^2 = \frac{1}{2}m(\dot{\vec{R}} + \dot{\vec{r}}')^2 = \frac{1}{2}m(\dot{\vec{R}}^2 + 2\dot{\vec{R}}\cdot\dot{\vec{r}}' + \dot{\vec{r}}'^2)
$$
在 $S'$ 系中，[广义坐标](@entry_id:156576)是 $\vec{r}'$ 的分量。[拉格朗日方程](@entry_id:175419)为 $m\ddot{\vec{r}}' = \vec{F}_{\text{eff}}$。其中有效力 $\vec{F}_{\text{eff}}$ 由[拉格朗日量](@entry_id:174593)中与 $\vec{r}'$ 相关的项导出。直接对加速度关系 $\ddot{\vec{r}} = \ddot{\vec{R}} + \ddot{\vec{r}}'$ 应用[牛顿第二定律](@entry_id:274217) $m\ddot{\vec{r}}=0$ 更为直接，我们得到 $S'$ 系中的[运动方程](@entry_id:170720)：
$$
m\ddot{\vec{r}}' = -m\ddot{\vec{R}}(t)
$$
这表明，在 $S'$ 系中的观察者看来，粒子受到了一个有效力 $\vec{F}_{\text{eff}} = -m\ddot{\vec{R}}$，其中 $\ddot{\vec{R}}$ 是 $S'$ 系相对于惯性系的加速度。

一个典型的例子是处于深空中、以[恒定加速度](@entry_id:268979) $\vec{a}$ 运动的航天器 [@problem_id:2033436]。对于航天器内的观察者，一个被释放的自由物体所受到的有效力为 $\vec{F}_{\text{eff}} = -m\vec{a}$。这个均匀的[惯性力](@entry_id:169104)场与一个方向为 $-\vec{a}$、强度为 $g_{\text{eff}}=|\vec{a}|$ 的均匀[引力场](@entry_id:169425)是无法区分的，这是广义相对论中**[等效原理](@entry_id:157518)**的一个简[单体](@entry_id:136559)现。

如果[参考系](@entry_id:169232)的加速度是随时间变化的，例如其原点做正弦[振荡](@entry_id:267781) $\vec{R}(t) = \vec{C}\cos(\omega t)$ [@problem_id:2033426]，那么惯性力也将随时间变化：
$$
\vec{F}_{\text{eff}} = -m\ddot{\vec{R}} = -m(-\omega^2 \vec{C}\cos(\omega t)) = m\omega^2\vec{C}\cos(\omega t)
$$
粒子的运动方程为 $\ddot{\vec{r}}'(t) = \omega^2\vec{C}\cos(\omega t)$。如果粒子在 $t=0$ 时在 $S'$ 系原点处相对静止，通过两次积分可以解得其在[非惯性系](@entry_id:168746)中的轨迹：
$$
\vec{r}'(t) = \vec{C}(1-\cos(\omega t))
$$
这表明，尽管在[惯性系](@entry_id:266190)看来粒子是静止或匀速[直线运动](@entry_id:165142)，但在[振荡](@entry_id:267781)的[参考系](@entry_id:169232)中，它会以与[参考系](@entry_id:169232)相反的相位进行[振荡](@entry_id:267781)。

#### 转动[参考系](@entry_id:169232)

当[非惯性系](@entry_id:168746)在转动时，情况变得更加复杂，会涌现出多种惯性力。设 $S'$ 系相对于惯性系 $S$ 以角速度矢量 $\vec{\Omega}$ 转动（共享原点）。一个在 $S'$ 系中位置为 $\vec{r}'$、速度为 $\vec{v}'$ 的粒子，其在 $S$ 系中的速度为：
$$
\vec{v} = \vec{v}' + \vec{\Omega} \times \vec{r}'
$$
[自由粒子](@entry_id:148748)的[拉格朗日量](@entry_id:174593)为 $L = \frac{1}{2}m|\vec{v}' + \vec{\Omega} \times \vec{r}'|^2$。从这个[拉格朗日量](@entry_id:174593)出发推导[运动方程](@entry_id:170720)，虽然可行但过程繁琐。一个更直接的方法是使用加[速度变换](@entry_id:265594)公式。粒子在 $S$ 系中的加速度 $\vec{a}$ 和在 $S'$ 系中的加速度 $\vec{a}'$ 之间的关系是：
$$
\vec{a} = \vec{a}' + 2(\vec{\Omega} \times \vec{v}') + \vec{\Omega} \times (\vec{\Omega} \times \vec{r}') + \dot{\vec{\Omega}} \times \vec{r}'
$$
对于[自由粒子](@entry_id:148748)，$m\vec{a} = 0$，因此 $S'$ 系中的运动方程为 $m\vec{a}' = \vec{F}_{\text{fict}}$，其中总的[惯性力](@entry_id:169104)为：
$$
\vec{F}_{\text{fict}} = -2m(\vec{\Omega} \times \vec{v}') - m\vec{\Omega} \times (\vec{\Omega} \times \vec{r}') - m(\dot{\vec{\Omega}} \times \vec{r}')
$$
这三个项分别对应三种著名的[惯性力](@entry_id:169104)：
1.  **科里奥利力** (Coriolis force): $\vec{F}_{\text{Cor}} = -2m(\vec{\Omega} \times \vec{v}')$，它只作用于在转动系中有相对运动的物体，方向垂直于 $\vec{\Omega}$ 和 $\vec{v}'$。
2.  **离心力** (Centrifugal force): $\vec{F}_{\text{Cen}} = -m\vec{\Omega} \times (\vec{\Omega} \times \vec{r}')$，它总是指向远离[转轴](@entry_id:187094)的方向，大小为 $m\Omega^2 r_\perp$，其中 $r_\perp$ 是粒子到[转轴](@entry_id:187094)的垂直距离。
3.  **[欧拉力](@entry_id:173795)** (Euler force) 或横向力: $\vec{F}_{\text{Euler}} = -m(\dot{\vec{\Omega}} \times \vec{r}')$，它仅在角速度 $\vec{\Omega}$ 发生变化时出现。

考虑一个以恒定角速度 $\omega$ 转动的平台上的自由粒子 [@problem_id:2033465]。此时 $\dot{\vec{\Omega}}=0$，[欧拉力](@entry_id:173795)为零。在平台的极[坐标系](@entry_id:156346) $(r, \phi)$ 中，$\vec{\Omega} = \omega\hat{z}$，$\vec{r}'=r\hat{r}$，$\vec{v}' = \dot{r}\hat{r} + r\dot{\phi}\hat{\phi}$。[科里奥利力](@entry_id:160096)和[离心力](@entry_id:173726)的径向分量分别为 $2m\omega r \dot{\phi}$ 和 $m\omega^2 r$。在转动系中，径向[运动方程](@entry_id:170720)的形式为 $m(\ddot{r}-r\dot{\phi}^2) = F_{r, \text{fict}}$。因此，总的有效径向力 $F_r$（使得 $m\ddot{r}=F_r$）为：
$$
F_r = m r\dot{\phi}^2 + F_{r, \text{fict}} = m r\dot{\phi}^2 + 2m\omega r \dot{\phi} + m\omega^2 r = mr(\omega + \dot{\phi})^2
$$
这个结果可以被解释为：转动系中的观察者看到的总角速度是平台的角速度与粒子相对平台的角速度之和，即 $\omega_{\text{total}} = \omega + \dot{\phi}$，而有效径向力就是对应于这个总角速度的“离心力”。

如果转动是不均匀的，例如角速度随时间线性增加 $\omega(t) = \beta t$ [@problem_id:2033428]，那么[欧拉力](@entry_id:173795)就不可忽略。此时 $\vec{\Omega}=(0,0,\beta t)$，$\dot{\vec{\Omega}}=(0,0,\beta)$。在转动系的[笛卡尔坐标](@entry_id:167698) $(x', y')$ 中，三种[惯性力](@entry_id:169104)共同作用。通过分别计算科里奥利力、[离心力](@entry_id:173726)和[欧拉力](@entry_id:173795)的 $x'$ 和 $y'$ 分量并相加，我们可以得到总的[惯性力](@entry_id:169104)分量：
$$
F_{\text{fict}, x'} = 2m\beta t \dot{y}' + m\beta^2 t^2 x' + m\beta y'
$$
$$
F_{\text{fict}, y'} = -2m\beta t \dot{x}' + m\beta^2 t^2 y' - m\beta x'
$$
这些表达式虽然复杂，但它们是遵循严格的变换法则得到的必然结果，系统地描述了在这样一个复杂[非惯性系](@entry_id:168746)中自由粒子所呈现出的表观运动。

综上所述，[拉格朗日形式](@entry_id:145697)体系为我们提供了一套系统性的方法，用于在任意[坐标系](@entry_id:156346)下描述粒子的运动。无论是通过[度规张量](@entry_id:160222)来理解运动的几何本质，还是通过寻找[循环坐标](@entry_id:166220)来发现守恒律，亦或是通过坐标变换来揭示[非惯性系](@entry_id:168746)中的虚拟力，该方法都展示了其深刻的理论洞察力和强大的实际应用能力。