## 引言
在[电动力学](@entry_id:158759)的宏伟画卷中，理解由单个[运动点电荷](@entry_id:273707)产生的[电磁场](@entry_id:265881)无疑是核心议题之一。与[静电学](@entry_id:140489)中瞬时作用的[库仑力](@entry_id:174598)不同，电[磁相](@entry_id:161372)互作用以有限的光速传播，这意味着我们在某一时刻观测到的场，是由[电荷](@entry_id:275494)在过去某个时刻的运动状态决定的。如何精确描述这种“推迟”效应，并将[电荷](@entry_id:275494)的运动轨迹与其在时空中激发的场联系起来，构成了一个基础而深刻的物理问题。[李纳-维谢尔势](@entry_id:262307)（Liénard-Wiechert potentials）正是解答这一问题的关键钥匙，它为[经典电动力学](@entry_id:270496)提供了一个与狭义相对论完全兼容的坚实基础。

本文将系统地引导读者深入[李纳-维谢尔势](@entry_id:262307)的理论世界。在“原理与机制”一章中，我们将从更普适的[推迟势](@entry_id:204770)积分出发，通过精巧的数学处理，一步步推导出适用于[点电荷](@entry_id:263616)的优雅公式，并着重剖析其核心——[推迟时间](@entry_id:274033)——以及势表达式中看似复杂的分母项所蕴含的深刻物理内涵。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将理论付诸实践，探讨该势在分析匀速运动、加速运动、[电磁辐射](@entry_id:152916)乃至[切伦科夫辐射](@entry_id:275457)等多种物理情景中的强大威力，并揭示其如何将电磁学与[狭义相对论](@entry_id:275552)、粒子物理等领域紧密联系起来。最后，“动手实践”部分将提供一系列精心设计的问题，帮助读者巩固理解并掌握计算技巧。通过这一系列的探索，读者将构建起关于运动[电荷](@entry_id:275494)电磁现象的完整而深刻的物理图像。

## 原理与机制

在上一章中，我们介绍了由[运动点电荷](@entry_id:273707)产生的[电磁场](@entry_id:265881)这一电动力学的核心问题。我们认识到，由于电[磁相](@entry_id:161372)互作用的传播速度是有限的（即光速 $c$），在某个特定时刻和特定位置观测到的场，是由[电荷](@entry_id:275494)在更早时刻的运动状态决定的。本章将深入探讨描述这一现象的数学框架——[李纳-维谢尔势](@entry_id:262307)（Liénard-Wiechert potentials）。我们将从[一般性](@entry_id:161765)的[推迟势](@entry_id:204770)积分表达式出发，系统地推导出适用于点电荷的精确公式，并详细阐释其中每一个组成部分的深刻物理意义。

### 从连续分布到[点电荷](@entry_id:263616)：[推迟势](@entry_id:204770)的特殊化

我们从适用于一般[连续电荷分布](@entry_id:270971) $\rho(\vec{r}', t')$ 和[电流密度](@entry_id:190690)[分布](@entry_id:182848) $\vec{J}(\vec{r}', t')$ 的[推迟势](@entry_id:204770)（retarded potential）公式出发。在给定时刻 $t$ 和观测点 $\vec{r}$，标势 $\Phi(\vec{r}, t)$ 和[矢势](@entry_id:153642) $\vec{A}(\vec{r}, t)$ 分别由以下积分给出：

$$
\Phi(\vec{r}, t) = \frac{1}{4\pi\epsilon_0} \int \frac{\rho(\vec{r}', t_r)}{|\vec{r} - \vec{r}'|} d^3r'
$$

$$
\vec{A}(\vec{r}, t) = \frac{\mu_0}{4\pi} \int \frac{\vec{J}(\vec{r}', t_r)}{|\vec{r} - \vec{r}'|} d^3r'
$$

这两个公式的核心在于被积函数中的时间变量——**[推迟时间](@entry_id:274033) (retarded time)** $t_r$。它定义为 $t_r = t - \frac{|\vec{r} - \vec{r}'|}{c}$。这个条件体现了**因果律 (causality)**：在时刻 $t$ 到达观测点 $\vec{r}$ 的电磁“消息”，必须是在更早的时刻 $t_r$ 从源点 $\vec{r}'$ 发出的，而消息传播的时间恰好是源点与观测点之间的距离除以光速。

现在，我们的目标是处理一个沿着特定轨迹 $\vec{w}(t')$ 运动的点电荷 $q$。为了将[点电荷](@entry_id:263616)纳入上述积分框架，我们必须将其表示为一种电荷密度[分布](@entry_id:182848)。这可以通过三维狄拉克 $\delta$ 函数来实现：

$$
\rho(\vec{r}', t') = q \delta^{(3)}(\vec{r}' - \vec{w}(t'))
$$

其中 $\delta^{(3)}$ 是三维 $\delta$ 函数，它的性质是在[电荷](@entry_id:275494)所在的位置 $\vec{w}(t')$ 以外处处为零，而在全空间积分时给出总[电荷](@entry_id:275494) $q$。类似地，电流密度可以表示为 $\vec{J}(\vec{r}', t') = \rho(\vec{r}', t') \vec{v}(t') = q \vec{v}(t') \delta^{(3)}(\vec{r}' - \vec{w}(t'))$，其中 $\vec{v}(t') = \frac{d\vec{w}(t')}{dt'}$ 是[电荷](@entry_id:275494)在时刻 $t'$ 的速度。

为了严谨地导出[李纳-维谢尔势](@entry_id:262307)，一个更清晰的方法是先将推迟条件本身也用一个 $\delta$ 函数表示，从而将[标势](@entry_id:276177)写成一个四维时空积分 [@problem_id:1803879]：

$$
\Phi(\vec{r}, t) = \frac{1}{4\pi\epsilon_0} \int_{-\infty}^{\infty} \int_{V} \frac{\rho(\vec{r}', t')}{|\vec{r} - \vec{r}'|} \delta\left(t' - \left(t - \frac{|\vec{r} - \vec{r}'|}{c}\right)\right) d^3r' dt'
$$

现在，我们将[点电荷](@entry_id:263616)的电荷密度表达式代入，并利用三维 $\delta$ 函数的[筛选性质](@entry_id:265662)（sifting property）来执行对空间坐标 $d^3r'$ 的积分：

$$
\int f(\vec{r}') \delta^{(3)}(\vec{r}' - \vec{a}) d^3r' = f(\vec{a})
$$

这会消去对 $\vec{r}'$ 的积分，并将所有出现的 $\vec{r}'$ 替换为[电荷](@entry_id:275494)的轨迹位置 $\vec{w}(t')$：

$$
\Phi(\vec{r}, t) = \frac{q}{4\pi\epsilon_0} \int_{-\infty}^{\infty} \frac{1}{|\vec{r} - \vec{w}(t')|} \delta\left(t' - \left(t - \frac{|\vec{r} - \vec{w}(t')|}{c}\right)\right) dt'
$$

这个表达式告诉我们，虽然[电荷](@entry_id:275494)在历史上经过了无数个时空点，但对特定观测事件 $(\vec{r}, t)$ 有贡献的，只有那些满足 $\delta$ 函数宗量为零的时刻 $t'$。

### [推迟时间](@entry_id:274033)：连接过去与现在的桥梁

上述积分中的 $\delta$ 函数引出了整个问题的核心概念：**[推迟时间](@entry_id:274033)**。对于一个给定的观测事件 $(\vec{r}, t)$，[推迟时间](@entry_id:274033) $t_r$ 不再是一个简单的表达式，而是满足下面这个[隐式方程](@entry_id:177636)的解：

$$
t - t_r = \frac{|\vec{r} - \vec{w}(t_r)|}{c}
$$

这个方程有深刻的物理和几何意义。在四维时空中，一个观测事件 $(\vec{r}, t)$ 有一个**过去[光锥](@entry_id:158105)（past light cone）**，它是由所有能够通过光速传播影响到该事件的时空点构成的。同时，运动[电荷](@entry_id:275494)的轨迹 $\vec{w}(t')$ 是一条**[世界线](@entry_id:199036)（world line）**。[推迟时间](@entry_id:274033) $t_r$ 的解，正是在几何上对应着[电荷](@entry_id:275494)的[世界线](@entry_id:199036)与观测事件的过去[光锥](@entry_id:158105)的交点。

求解这个方程是计算任何[运动点电荷](@entry_id:273707)问题的首要步骤。例如，考虑一个沿 x 轴做相对论性双曲线运动的[电荷](@entry_id:275494)，其轨迹为 $\mathbf{w}(t) = (\sqrt{x_0^2 + (ct)^2}, 0, 0)$。对于位于 $\mathbf{r} = (0, y_0, 0)$ 并在时刻 $T$ 进行观测的观察者，[推迟时间](@entry_id:274033) $t_r$ 由以下方程决定 [@problem_id:1620079]：

$$
c^2 (T - t_r)^2 = |\vec{r} - \vec{w}(t_r)|^2 = \left(0 - \sqrt{x_0^2 + (ct_r)^2}\right)^2 + y_0^2 = x_0^2 + c^2t_r^2 + y_0^2
$$

展开并求解 $t_r$，我们得到唯一的解 $t_r = \frac{c^{2} T^{2} - x_{0}^{2} - y_{0}^{2}}{2 c^{2} T}$。对于大多数复杂的运动，这个方程可能是[超越方程](@entry_id:276279)，可能有一个、多个甚至没有解。

理解[推迟时间](@entry_id:274033)的关键在于区分[电荷](@entry_id:275494)的**推迟位置 (retarded position)** $\vec{w}(t_r)$ 和它的**当前位置 (present position)** $\vec{w}(t)$。观测到的场和势是由[电荷](@entry_id:275494)在推迟位置时的状态（位置、速度等）决定的，而不是它在观测时刻 $t$ 的当前位置。

让我们通过一个简单的例子来阐明这一点 [@problem_id:1620119]。一个[电荷](@entry_id:275494)以恒定速度 $\vec{v}$ 沿 z 轴运动，其轨迹为 $\vec{r}'(t') = v t' \hat{\mathbf{z}}$。一个观察者位于 $\mathbf{r} = b \hat{\mathbf{x}}$，并在 $t=0$ 时刻进行测量。在这一时刻，[电荷](@entry_id:275494)的“当前位置”是原点 $\vec{r}'(0) = \vec{0}$。然而，观察者接收到的信号并非来自原点。信号来自某个更早的时刻 $t_r  0$ 和某个推迟位置 $\vec{r}'(t_r) = v t_r \hat{\mathbf{z}}$。从推迟位置指向观察者的矢量 $\vec{\mathcal{R}} = \vec{r} - \vec{r}'(t_r)$ 与从当前位置指向观察者的矢量 $\vec{\mathcal{P}} = \vec{r} - \vec{r}'(0)$ 是不同的。由于信号传播的因果关系，[电磁场](@entry_id:265881)似乎来自一个“视位置”，即推迟位置，而非[电荷](@entry_id:275494)的真实当前位置。这种错位是相对论效应的直接体现，当 $v \to 0$ 时， $t_r \to t$，这种区别消失。

因果律的重要性在一个思想实验中表现得淋漓尽致 [@problem_id:1803864]。想象一个静止在原点的[电荷](@entry_id:275494) $-q$ 和一个沿 z 轴运动并恰好在 $t=0$ 时刻通过原点的[电荷](@entry_id:275494) $+q$。一个幼稚的分析可能会认为，在 $t=0$ 时刻，由于正负[电荷](@entry_id:275494)在原点重合，总势应该处处为零。然而，正确的计算表明，在任意观测点 $P(x_P, 0, z_P)$，总势并不为零。这是因为静止[电荷](@entry_id:275494) $-q$ 的势是瞬时建立的[库仑势](@entry_id:154276)，而运动[电荷](@entry_id:275494) $+q$ 的势则取决于它在推迟时刻 $t_r  0$ 时的位置。因此，在 $t=0$ 时刻，两个[电荷](@entry_id:275494)对总势的贡献来自空间中的不同点，导致总势非零。

### [李纳-维谢尔势](@entry_id:262307)的完整形式

回到我们的积分表达式：
$$
\Phi(\vec{r}, t) = \frac{q}{4\pi\epsilon_0} \int_{-\infty}^{\infty} \frac{1}{|\vec{r} - \vec{w}(t')|} \delta\left(f(t')\right) dt'
$$
其中 $f(t') = t' - t + \frac{|\vec{r} - \vec{w}(t')|}{c}$。为了计算这个积分，我们需要使用关于 $\delta$ 函数的一个重要性质：
$$
\int g(x) \delta(f(x)) dx = \sum_i \frac{g(x_i)}{|f'(x_i)|}
$$
其中 $x_i$ 是使 $f(x_i)=0$ 的根。

在我们的例子中，变量是 $t'$，函数 $g(t')$ 是 $\frac{1}{|\vec{r} - \vec{w}(t')|}$，而 $f(t')$ 的根就是[推迟时间](@entry_id:274033) $t_r$。我们需要计算 $f'(t_r) = \frac{df}{dt'}\Big|_{t'=t_r}$。
令 $\vec{\mathcal{R}} = \vec{r} - \vec{w}(t')$ 且 $\mathcal{R} = |\vec{\mathcal{R}}|$。那么 $f(t') = t' - t + \mathcal{R}/c$。对 $t'$ 求导：
$$
\frac{df}{dt'} = 1 + \frac{1}{c}\frac{d\mathcal{R}}{dt'}
$$
利用链式法则，$\frac{d\mathcal{R}}{dt'} = \frac{d}{dt'} \sqrt{\vec{\mathcal{R}} \cdot \vec{\mathcal{R}}} = \frac{1}{2\mathcal{R}} (2\vec{\mathcal{R}} \cdot \frac{d\vec{\mathcal{R}}}{dt'})$。由于 $\vec{r}$ 是固定的观测点，$\frac{d\vec{\mathcal{R}}}{dt'} = - \frac{d\vec{w}(t')}{dt'} = -\vec{v}(t')$。于是：
$$
\frac{d\mathcal{R}}{dt'} = \frac{\vec{\mathcal{R}}}{\mathcal{R}} \cdot (-\vec{v}) = -\hat{\mathcal{R}} \cdot \vec{v}
$$
其中 $\hat{\mathcal{R}}$ 是从推迟位置指向观测点的单位矢量。

将此结果代回，我们得到：
$$
\frac{df}{dt'}\Big|_{t_r} = 1 - \frac{\hat{\mathcal{R}} \cdot \vec{v}}{c} = \frac{1}{\mathcal{R}} \left( \mathcal{R} - \frac{\vec{\mathcal{R}} \cdot \vec{v}}{c} \right)
$$
假设在给定观测事件 $(\vec{r}, t)$ 只有一个[推迟时间](@entry_id:274033)解 $t_r$，积分的结果就是：
$$
\Phi(\vec{r}, t) = \frac{q}{4\pi\epsilon_0} \frac{1/\mathcal{R}}{|1 - \hat{\mathcal{R}} \cdot \vec{v}/c|} = \frac{1}{4\pi\epsilon_0} \left[ \frac{q}{\mathcal{R} - \vec{\mathcal{R}} \cdot \vec{v}/c} \right]_{t_r}
$$
方括号和下标 $t_r$ 强调了内部的所有量——距离 $\mathcal{R}$、[位移矢量](@entry_id:262782) $\vec{\mathcal{R}}$ 和[电荷](@entry_id:275494)速度 $\vec{v}$——都必须在推迟时刻 $t_r$进行计算。

通过完全相同的步骤，我们可以得到[矢势](@entry_id:153642)的表达式：
$$
\vec{A}(\vec{r}, t) = \frac{\mu_0}{4\pi} \left[ \frac{q\vec{v}}{\mathcal{R} - \vec{\mathcal{R}} \cdot \vec{v}/c} \right]_{t_r}
$$
这就是著名的**[李纳-维谢尔势](@entry_id:262307)**。

通过比较[标势](@entry_id:276177)和[矢势](@entry_id:153642)的表达式，我们可以发现一个非常简洁而深刻的关系 [@problem_id:1620087]。利用[真空介电常数](@entry_id:204253) $\epsilon_0$、磁导率 $\mu_0$ 和光速 $c$ 之间的关系 $c^2 = 1/(\epsilon_0 \mu_0)$，我们可以将 $\mu_0$ 替换为 $1/(\epsilon_0 c^2)$。于是[矢势](@entry_id:153642)可以写为：
$$
\vec{A}(\vec{r}, t) = \frac{1}{4\pi\epsilon_0 c^2} \left[ \frac{q\vec{v}}{\mathcal{R} - \vec{\mathcal{R}} \cdot \vec{v}/c} \right]_{t_r} = \frac{\vec{v}(t_r)}{c^2} \left( \frac{1}{4\pi\epsilon_0} \left[ \frac{q}{\mathcal{R} - \vec{\mathcal{R}} \cdot \vec{v}/c} \right]_{t_r} \right)
$$
我们发现，括号内的表达式正是[标势](@entry_id:276177) $\Phi(\vec{r}, t)$。因此，我们得到：
$$
\vec{A}(\vec{r}, t) = \frac{\vec{v}(t_r)}{c^2} \Phi(\vec{r}, t)
$$
这个关系表明，对于一个运动的点电荷，其[标势](@entry_id:276177)和[矢势](@entry_id:153642)并非[相互独立](@entry_id:273670)，[矢势](@entry_id:153642)可以简单地通过[标势](@entry_id:276177)乘以其推迟速度与 $c^2$ 的比值得到。

### 分母的物理内涵：[多普勒效应](@entry_id:160624)与视在体积

[李纳-维谢尔势](@entry_id:262307)公式中最不直观的部分无疑是其分母 $\mathcal{R} - \vec{\mathcal{R}} \cdot \vec{v}/c$。它并非简单的距离 $\mathcal{R}$。这个修正项 $1 - \hat{\mathcal{R}} \cdot \vec{\beta}$ (其中 $\vec{\beta} = \vec{v}/c$) 具有深刻的物理起源，可以从两个互补的角度来理解。

#### 1. 时间间隔的“压缩”效应
想象一个以速度 $\vec{v}$ 运动的[电荷](@entry_id:275494)，在极短的时间间隔 $dt_r$ 内，它相继发出了两个光脉冲 [@problem_id:1803890]。第一个脉冲在时刻 $t_1$ 从位置 $\vec{r}_1$ 发出，第二个在时刻 $t_2 = t_1 + dt_r$ 从位置 $\vec{r}_2 = \vec{r}_1 + \vec{v}dt_r$ 发出。一个位于遥远固定位置 $\vec{d}$ 的观察者将分别在时刻 $t'_1$ 和 $t'_2$ 接收到这两个脉冲。
第一个脉冲的到达时间为 $t'_1 = t_1 + |\vec{d}-\vec{r}_1|/c$。
第二个脉冲的到达时间为 $t'_2 = t_2 + |\vec{d}-\vec{r}_2|/c$。

观察者测量到的时间间隔是 $dt_{obs} = t'_2 - t'_1 = (t_2 - t_1) + \frac{1}{c} (|\vec{d}-\vec{r}_2| - |\vec{d}-\vec{r}_1|)$。在[远场近似](@entry_id:275937)下，$|\vec{d}-\vec{r}_2| \approx |\vec{d}-\vec{r}_1| - \hat{d} \cdot (\vec{r}_2 - \vec{r}_1)$，其中 $\hat{d}$ 是指向观察者的单位矢量。代入后我们得到：
$$
dt_{obs} \approx dt_r + \frac{1}{c}(-\hat{d} \cdot \vec{v} dt_r) = (1 - \hat{d} \cdot \vec{\beta}) dt_r
$$
这个结果表明，从源头发出的时间间隔 $dt_r$ 和观察者接收到的时间间隔 $dt_{obs}$ 并不相等。它们之间的[比例因子](@entry_id:266678)正是 $1 - \hat{\mathcal{R}} \cdot \vec{\beta}$ (这里用 $\hat{\mathcal{R}}$ 代替 $\hat{d}$ 表示从推迟位置指向观察者的方向)。这正是光源移动引起的光学**[多普勒效应](@entry_id:160624)**。当[电荷](@entry_id:275494)朝向观察者运动时 $(\hat{\mathcal{R}} \cdot \vec{\beta} > 0)$，$dt_{obs}  dt_r$，信号到达的时间被“压缩”了；当[电荷](@entry_id:275494)远离观察者运动时 $(\hat{\mathcal{R}} \cdot \vec{\beta}  0)$，$dt_{obs} > dt_r$，信号被“拉伸”了。

这个因子也与观察者时间 $t$ 和[推迟时间](@entry_id:274033) $t_r$ 之间的[微分](@entry_id:158718)关系有关。通过对[推迟时间](@entry_id:274033)方程 $t - t_r = \mathcal{R}(t_r)/c$ 两边对 $t$求导（保持 $\vec{r}$ 不变），可以证明 [@problem_id:1620146]：
$$
\frac{dt_r}{dt} = \frac{1}{1 - \hat{\mathcal{R}} \cdot \vec{\beta}}
$$
这再次说明了分母的物理意义：它描述了[推迟时间](@entry_id:274033)流逝的速率相对于观察者时间流逝速率的改变。

#### 2. 视在[电荷密度](@entry_id:144672)的改变
由于上述的时间压缩/拉伸效应，观察者“看到”的电荷分布的[有效长度](@entry_id:184361)也会发生改变。考虑一段长度为 $L_0 = v dt_r$ 的[电荷](@entry_id:275494)轨迹。观察者接收到来自这段轨迹两端信号的时间差是 $dt_{obs}$。因此，在观察者看来，这段[电荷](@entry_id:275494)的“视在长度”是 $L_{obs} = v dt_{obs} = v(1 - \hat{\mathcal{R}} \cdot \vec{\beta}) dt_r$。[电荷](@entry_id:275494) $q$ 似乎被“挤压”到了一个更小或更大的空间区域内。势的大小正比于单位长度的[电荷密度](@entry_id:144672)。相比于静态情况下的 $q/\mathcal{R}$，运动[电荷](@entry_id:275494)的势被因子 $dt_r/dt_{obs} = 1/(1 - \hat{\mathcal{R}} \cdot \vec{\beta})$ 修正了。这解释了为什么分母中会出现这个[多普勒因子](@entry_id:272525)。

一个至关重要的结论是，对于任何有质量的、物理上真实的粒子，其速度必须小于光速 $c$，即 $|\vec{v}|  c$ 或 $|\vec{\beta}|  1$。这意味着 $\hat{\mathcal{R}} \cdot \vec{\beta}$ 的值总是在 $-1$ 和 $+1$ 之间。因此，分母因子 $1 - \hat{\mathcal{R}} \cdot \vec{\beta}$ **永远为正** [@problem_id:1803869]。这意味着，一个正[电荷](@entry_id:275494) $q>0$ 产生的[标势](@entry_id:276177) $\Phi$ 永远是正的，而一个负[电荷](@entry_id:275494)产生的标势永远是负的。[电荷](@entry_id:275494)的运动会改变势的大小，但不会改变其符号。

反之，如果我们考虑一个假设的[超光速粒子](@entry_id:159813) ($v > c$) [@problem_id:1620144]，当它径直冲向观察者时，$\hat{\mathcal{R}} \cdot \vec{\beta} = v/c > 1$。此时，分母 $1 - \hat{\mathcal{R}} \cdot \vec{\beta}$ 会变为负数。更奇特的是，[推迟时间](@entry_id:274033)方程可能会出现多个解，导致观察者在同一时刻“看到”来自该粒子不同历史位置的多个“鬼影”，其中一些贡献的势可能是负的（即使[电荷](@entry_id:275494)为正）甚至是发散的。这揭示了[光速极限](@entry_id:263015) $c$ 在维持物理定律良好行为中的根本作用。

### [李纳-维谢尔势](@entry_id:262307)的相对论起源

[李纳-维谢尔势](@entry_id:262307)不仅仅是对[库仑定律](@entry_id:139360)的修正，它是狭义相对论框架下电磁理论的必然结果。我们可以通过[洛伦兹变换](@entry_id:176827)直接从静电势推导出它。

考虑一个在S'系中静止于原点的[电荷](@entry_id:275494) $q$。在该[参考系](@entry_id:169232)中，[矢势](@entry_id:153642)为零，[标势](@entry_id:276177)为简单的[库仑势](@entry_id:154276) $\Phi'(\vec{r}') = \frac{q}{4\pi\epsilon_0 r'}$。[标势](@entry_id:276177)和[矢势](@entry_id:153642)共同构成一个[四维矢量](@entry_id:275085)——[四维势](@entry_id:188407) $A'^\mu = (\Phi'/c, \vec{0})$。现在，让S'系相对于实验室S系以恒定速度 $\vec{v} = v\hat{x}$ 运动 [@problem_id:1803918]。

[四维势](@entry_id:188407)的变换法则与时空四维矢量 $x^\mu = (ct, \vec{r})$ 相同。通过应用[洛伦兹变换](@entry_id:176827)：
$$
\Phi = \gamma (\Phi' + v A'_x)
$$
$$
A_x = \gamma (A'_x + \frac{v}{c^2} \Phi')
$$
由于在S'系中 $A'_x=0$，我们得到 S 系中的势为 $\Phi = \gamma \Phi'$ 和 $\vec{A} = \frac{\gamma v}{c^2} \Phi' \hat{x} = \frac{\vec{v}}{c^2}\Phi$。
为了得到 $\Phi$ 作为 S 系坐标 $(t, x, y, z)$ 的函数，我们还需要将 $\Phi'$ 中的坐标 $r' = \sqrt{x'^2+y'^2+z'^2}$ 用 S 系坐标表示。利用逆洛伦兹变换 $x' = \gamma(x-vt)$，$y'=y$，$z'=z$，我们得到：
$$
\Phi(t, x, y, z) = \gamma \frac{q}{4\pi\epsilon_0 \sqrt{\gamma^2(x-vt)^2 + y^2 + z^2}} = \frac{1}{4\pi\epsilon_0} \frac{q}{\sqrt{(x-vt)^2 + (1-v^2/c^2)(y^2+z^2)}}
$$
这个结果正是[李纳-维谢尔势](@entry_id:262307)在匀速直线运动下的特殊形式。它表明，运动[电荷](@entry_id:275494)的[势场](@entry_id:143025)是静电场在[洛伦兹变换](@entry_id:176827)下的自然呈现，其著名的“椭球形”等势面是时空收缩效应的直接后果。

最后，值得一提的是，[李纳-维谢尔势](@entry_id:262307)是满足**[洛伦兹规范](@entry_id:153650)条件 (Lorenz gauge condition)** $\nabla \cdot \vec{A} + \frac{1}{c^2}\frac{\partial \Phi}{\partial t} = 0$ 的一个解。这个条件保证了从势计算出的场满足[麦克斯韦方程组](@entry_id:150940)。对[李纳-维谢尔势](@entry_id:262307)进行[微分](@entry_id:158718)运算需要非常小心，因为对观测坐标 $(\vec{r}, t)$ 的[偏导数](@entry_id:146280)会通过[推迟时间](@entry_id:274033) $t_r(\vec{r}, t)$ 传递给所有依赖于 $t_r$ 的量，这涉及到复杂的[链式法则](@entry_id:190743)。验证[洛伦兹规范](@entry_id:153650)条件是一个很好的练习，它能加深对这些势的数学结构的理解 [@problem_id:1620134]。

总结而言，[李纳-维谢尔势](@entry_id:262307)是描述[运动点电荷](@entry_id:273707)电磁现象的基石。它完美地融合了麦克斯韦方程组和狭义相对论的原理，其核心是因果律决定的[推迟时间](@entry_id:274033)概念，以及由运动产生的多普勒效应修正。理解了这些原理和机制，我们就能进一步去计算由这些势产生的[电场和磁场](@entry_id:261347)，并探索诸如[电磁辐射](@entry_id:152916)等更高级的课题。