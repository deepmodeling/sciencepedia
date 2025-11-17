## 引言
在研究[电场](@entry_id:194326)时，引入标量势 $V$ 使得许多静电学问题得以简化。一个自然而然的问题是：我们能否为[磁场](@entry_id:153296) $\vec{B}$ 引入一个类似的[势函数](@entry_id:176105)？[磁矢量势](@entry_id:141246) $\vec{A}$ 正是这个问题的答案，它是一个深刻而强大的概念，构成了现代[电动力学](@entry_id:158759)乃至整个物理学理论框架的基石。然而，与标量势不同，矢量势的引入带来了新的特性，例如规范自由度，这既是其理论优雅性的体现，也对实际应用提出了挑战。本文旨在系统地揭开[磁矢量势](@entry_id:141246)的神秘面纱，解决如何定义、选择和使用这一工具的知识缺口。

本文将引导读者分三步深入探索[磁矢量势](@entry_id:141246)的世界。在“原理与机制”一章中，我们将从[磁场](@entry_id:153296)的基本性质出发，引出[磁矢量势](@entry_id:141246)的定义，并详细探讨其核心性质——规范自由度，以及如何通过[库仑规范](@entry_id:273044)来简化计算。接下来的“应用与跨学科联系”一章将展示磁矢量势的强大威力，其应用范围从计算电感等经典工程问题，延伸到[分析力学](@entry_id:166738)中的[广义动量](@entry_id:165699)，直至在量子力学中通过阿哈罗诺夫-玻姆效应证明其物理实在性。最后，在“动手实践”部分，读者将有机会通过解决具体问题，将所学理论知识转化为实际的计算技能。通过这一系列的學習，读者将不仅掌握一个计算工具，更将领会到贯穿现代物理学的规范思想的深刻内涵。

## 原理与机制

在[静电学](@entry_id:140489)中，标量势 $V$ 的引入极大地简化了[电场](@entry_id:194326) $\vec{E}$ 的计算。我们不禁要问：对于[磁场](@entry_id:153296) $\vec{B}$，是否存在类似的[势函数](@entry_id:176105)，能够简化[磁场](@entry_id:153296)的分析与计算？答案是肯定的，但[磁场](@entry_id:153296)的情况更为复杂，它需要一个矢量场——即**[磁矢量势](@entry_id:141246)** (magnetic vector potential)，记作 $\vec{A}$。本章将深入探讨磁矢量势的定义、基本性质、及其在[电动力学](@entry_id:158759)中的核心作用。

### [磁矢量势](@entry_id:141246)的引入与定义

[磁场](@entry_id:153296)的一个基本实验定律是[磁场](@entry_id:153296)是无散的，即[磁场](@entry_id:153296)线总是闭合的，不存在发出或汇入[磁场](@entry_id:153296)线的“磁荷”。这一物理事实在数学上表现为[高斯磁定律](@entry_id:182942)：
$$
\nabla \cdot \vec{B} = 0
$$
这条方程是[麦克斯韦方程组](@entry_id:150940)的核心成员之一，它对[磁场](@entry_id:153296)的结构施加了根本性的约束。根据矢量分析中的[亥姆霍兹定理](@entry_id:275687)，任何无散的矢量场（即散度处处为零的矢量场）都可以表示为另一个[矢量场的旋度](@entry_id:146155)。因此，$\nabla \cdot \vec{B} = 0$ 这一条件保证了[磁场](@entry_id:153296) $\vec{B}$ 一定可以写成某个矢量场 $\vec{A}$ 的旋度形式：
$$
\vec{B} = \nabla \times \vec{A}
$$
这个矢量场 $\vec{A}$ 就是我们所定义的**[磁矢量势](@entry_id:141246)**。这个定义是磁矢量势概念的基石。从这个定义出发，我们可以立即推断出[高斯磁定律](@entry_id:182942)，因为对于任何矢量场 $\vec{A}$，其[旋度的散度](@entry_id:271562)恒为零，即 $\nabla \cdot (\nabla \times \vec{A}) \equiv 0$。这表明，只要[磁场](@entry_id:153296)可以从一个矢量势导出，[高斯磁定律](@entry_id:182942)就自动得到满足。

理解一个物理量的第一步是明确其单位。我们可以从几个关键的物理关系中推导出 $\vec{A}$ 的[国际单位制](@entry_id:172547)（SI）单位 [@problem_id:1833437]。
1.  从定义式 $\vec{B} = \nabla \times \vec{A}$ 出发，在量纲上，[旋度算子](@entry_id:184984) $\nabla \times$ 的量纲是长度的倒数（$1/\text{length}$）。因此，$\vec{A}$ 的单位应为 $\vec{B}$ 的单位乘以长度单位。由于[磁场](@entry_id:153296) $\vec{B}$ 的单位是特斯拉（T），所以 $\vec{A}$ 的一个有效单位是**特斯拉·米**（$\text{T} \cdot \text{m}$）。

2.  磁通量 $\Phi_B$ 定义为[磁场](@entry_id:153296)通过一个[曲面](@entry_id:267450)的积分，其单位是韦伯（Wb），并且 $1 \ \text{Wb} = 1 \ \text{T} \cdot \text{m}^2$。由此，$\text{T} \cdot \text{m}$ 可以表示为 $\text{Wb}/\text{m}$。因此，**韦伯/米**（$\text{Wb}/\text{m}$）也是 $\vec{A}$ 的一个有效单位。

3.  在完整的[电动力学](@entry_id:158759)中，含时的[电场](@entry_id:194326)由[法拉第感应定律](@entry_id:146175)给出：$\vec{E} = -\nabla V - \frac{\partial \vec{A}}{\partial t}$。从这个表达式可以看出，$\frac{\partial \vec{A}}{\partial t}$ 的单位必须与[电场](@entry_id:194326) $\vec{E}$ 的单位（$\text{V}/\text{m}$）相同。因此，$\vec{A}$ 的单位可以表示为 $(\text{V}/\text{m}) \cdot \text{s} = \text{V} \cdot \text{s} / \text{m}$。考虑到 $1 \ \text{V} = 1 \ \text{N} \cdot \text{m} / \text{C}$（伏特等于牛顿·米/库仑），我们可以进一步推导：$[A] = \frac{(\text{N} \cdot \text{m} / \text{C}) \cdot \text{s}}{\text{m}} = \text{N} \cdot \text{s} / \text{C}$。所以，**牛顿·秒/库仑**（$\text{N} \cdot s / \text{C}$）也是 $\vec{A}$ 的一个有效单位。

这几种不同的单位表示方式从不同侧面反映了磁矢量势与[磁场](@entry_id:153296)、[磁通量](@entry_id:268943)和[电场](@entry_id:194326)之间的深刻联系。

### [规范自由度](@entry_id:160491)：矢量势的不唯一性

定义了 $\vec{A}$ 之后，一个至关重要的问题随之而来：对于一个给定的[磁场](@entry_id:153296) $\vec{B}$，它所对应的[磁矢量势](@entry_id:141246) $\vec{A}$ 是否是唯一的？答案是否定的。

让我们考虑一个任意的、可微的标量函数 $\lambda(\vec{r}, t)$。根据矢量恒等式，任意标量函数的梯度（gradient）的旋度（curl）恒为零：
$$
\nabla \times (\nabla \lambda) \equiv 0
$$
这一数学事实具有深远的物理意义 [@problem_id:1621739]。假设我们找到了一个矢量势 $\vec{A}$，它能产生[磁场](@entry_id:153296) $\vec{B}$。现在，我们构造一个新的矢量势 $\vec{A}'$，定义为：
$$
\vec{A}' = \vec{A} + \nabla \lambda
$$
这个从 $\vec{A}$到 $\vec{A}'$ 的变换被称为**[规范变换](@entry_id:176521)**（gauge transformation），$\lambda$ 被称为[规范函数](@entry_id:749731)。让我们计算一下由 $\vec{A}'$ 产生的新[磁场](@entry_id:153296) $\vec{B}'$：
$$
\vec{B}' = \nabla \times \vec{A}' = \nabla \times (\vec{A} + \nabla \lambda) = \nabla \times \vec{A} + \nabla \times (\nabla \lambda)
$$
由于 $\nabla \times (\nabla \lambda) = 0$，我们得到：
$$
\vec{B}' = \nabla \times \vec{A} = \vec{B}
$$
这个结果表明，$\vec{A}'$ 和 $\vec{A}$ 虽然是不同的矢量场，但它们描述的是完全相同的[磁场](@entry_id:153296) $\vec{B}$ [@problem_id:1833418]。这种可以选择不同的势函数来描述同一物理场（[磁场](@entry_id:153296)）的自由度，被称为**规范自由度**（gauge freedom）。这意味着对于任何给定的[磁场](@entry_id:153296)，都存在无穷多个与之对应的磁矢量势，它们之间通过一个标量函数的梯度相联系 [@problem_id:1621694]。

为了更具体地理解这一概念，让我们考虑一个在空间中[均匀分布](@entry_id:194597)的静[磁场](@entry_id:153296) $\vec{B} = B_0 \hat{z}$，其中 $B_0$ 是一个常数 [@problem_id:1833420]。我们可以提出至少两种不同的矢量势来产生这个场。
第一个势函数是 $\vec{A}_1 = \frac{B_0}{2}(-y\hat{x} + x\hat{y})$。通过计算其旋度：
$$
\nabla \times \vec{A}_1 = \left(\frac{\partial A_{1z}}{\partial y} - \frac{\partial A_{1y}}{\partial z}\right)\hat{x} + \left(\frac{\partial A_{1x}}{\partial z} - \frac{\partial A_{1z}}{\partial x}\right)\hat{y} + \left(\frac{\partial A_{1y}}{\partial x} - \frac{\partial A_{1x}}{\partial y}\right)\hat{z}
$$
$$
\nabla \times \vec{A}_1 = (0-0)\hat{x} + (0-0)\hat{y} + \left(\frac{\partial}{\partial x}\left(\frac{B_0}{2}x\right) - \frac{\partial}{\partial y}\left(-\frac{B_0}{2}y\right)\right)\hat{z} = \left(\frac{B_0}{2} + \frac{B_0}{2}\right)\hat{z} = B_0 \hat{z}
$$
它确实产生了正确的[磁场](@entry_id:153296)。
第二个势函数是 $\vec{A}_2 = B_0 x \hat{y}$。计算其旋度：
$$
\nabla \times \vec{A}_2 = \left(\frac{\partial}{\partial x}(B_0 x) - \frac{\partial}{\partial y}(0)\right)\hat{z} = B_0 \hat{z}
$$
它也产生了完全相同的[磁场](@entry_id:153296)。这两个势显然不同，但它们在物理上是等效的。它们之间必然通过一个规范变换相联系。我们可以找到这个[规范函数](@entry_id:749731) $\lambda$：
$$
\nabla \lambda = \vec{A}_2 - \vec{A}_1 = B_0 x \hat{y} - \frac{B_0}{2}(-y\hat{x} + x\hat{y}) = \frac{B_0}{2}y\hat{x} + \frac{B_0}{2}x\hat{y}
$$
通过积分，我们可以得到 $\lambda(x, y) = \frac{B_0}{2}xy$（假设在原点处 $\lambda=0$）。这个例子清晰地展示了[规范自由度](@entry_id:160491)的实际体现。

### [库仑规范](@entry_id:273044)：一种方便的规范选择

[规范自由度](@entry_id:160491)虽然在理论上优雅，但在实际计算中，我们需要一个确定的、唯一的[势函数](@entry_id:176105)。为了做到这一点，我们可以对 $\vec{A}$ 施加一个额外的数学条件，这个过程称为“选择一个规范”或“[规范固定](@entry_id:142821)”。

在[静磁学](@entry_id:140120)中，最常用和最方便的规范选择是**[库仑规范](@entry_id:273044)**（Coulomb gauge），也称为横向规范（transverse gauge）。该[规范条件](@entry_id:749730)要求[磁矢量势](@entry_id:141246)的散度为零：
$$
\nabla \cdot \vec{A} = 0
$$
我们总能找到一个[规范函数](@entry_id:749731) $\lambda$ 来满足这个条件。假设我们有一个初始的矢量势 $\vec{A}_0$，其散度不为零（$\nabla \cdot \vec{A}_0 \neq 0$）。我们可以进行一次规范变换 $\vec{A} = \vec{A}_0 + \nabla \lambda$，并要求新的势 $\vec{A}$ 满足[库仑规范](@entry_id:273044)条件：
$$
\nabla \cdot \vec{A} = \nabla \cdot (\vec{A}_0 + \nabla \lambda) = \nabla \cdot \vec{A}_0 + \nabla^2 \lambda = 0
$$
这导致了一个关于 $\lambda$ 的[泊松方程](@entry_id:143763)：$\nabla^2 \lambda = -\nabla \cdot \vec{A}_0$。对于给定的 $\vec{A}_0$，这个方程总是有解的，从而证明我们总能将矢量势调整到满足[库仑规范](@entry_id:273044)。

[库仑规范](@entry_id:273044)的优越性在于它能极大地简化描述[磁场源](@entry_id:267241)的方程。在[静磁学](@entry_id:140120)中，安培定律为 $\nabla \times \vec{B} = \mu_0 \vec{J}$。将 $\vec{B} = \nabla \times \vec{A}$ 代入，我们得到：
$$
\nabla \times (\nabla \times \vec{A}) = \mu_0 \vec{J}
$$
使用矢量恒等式 $\nabla \times (\nabla \times \vec{A}) = \nabla(\nabla \cdot \vec{A}) - \nabla^2 \vec{A}$，上式变为：
$$
\nabla(\nabla \cdot \vec{A}) - \nabla^2 \vec{A} = \mu_0 \vec{J}
$$
在[库仑规范](@entry_id:273044)下，$\nabla \cdot \vec{A} = 0$，于是方程简化为：
$$
\nabla^2 \vec{A} = -\mu_0 \vec{J}
$$
这是一个矢量形式的**[泊松方程](@entry_id:143763)**。它在形式上与[静电学](@entry_id:140489)中[标量势](@entry_id:276177) $V$ 所满足的[泊松方程](@entry_id:143763) $\nabla^2 V = -\rho / \epsilon_0$ 非常相似。

例如，前面我们用于描述均匀[磁场](@entry_id:153296)的势 $\vec{A}_1 = \frac{B_0}{2}(-y\hat{x} + x\hat{y})$，其散度为 $\nabla \cdot \vec{A}_1 = \frac{\partial}{\partial x}(-\frac{B_0}{2}y) + \frac{\partial}{\partial y}(\frac{B_0}{2}x) = 0$。因此，$\vec{A}_1$ 满足[库仑规范](@entry_id:273044) [@problem_id:1833442]。而势 $\vec{A}_2 = B_0 x \hat{y}$ 的散度为 $\nabla \cdot \vec{A}_2 = 0$，也满足[库仑规范](@entry_id:273044)。请注意，之前例子中的 $\vec{A}_B = c((y+3x^2)\hat{i} - x\hat{j})$ [@problem_id:1621694] 并不满足[库仑规范](@entry_id:273044)，因为其散度 $\nabla \cdot \vec{A}_B = 6cx \neq 0$。然而，这并不意味着 $\vec{A}_B$ 是错误的，它只是一个处于不同规范下的、完全合法的矢量势。这再次强调了[规范条件](@entry_id:749730)是数学上的选择，而非物理上的强制要求。

### 从源计算矢量势

在[库仑规范](@entry_id:273044)下，$\nabla^2 \vec{A} = -\mu_0 \vec{J}$ 这个方程的解与[静电学](@entry_id:140489)中泊松方程的解具有完全相同的积分形式。对于一个给定的电流密度[分布](@entry_id:182848) $\vec{J}(\vec{r}')$，在空间中某点 $\vec{r}$ 的[磁矢量势](@entry_id:141246)为：
$$
\vec{A}(\vec{r}) = \frac{\mu_0}{4\pi} \int \frac{\vec{J}(\vec{r}')}{|\vec{r} - \vec{r}'|} d^3r'
$$
这个积分遍及所有电流源存在的空间。这个公式是计算磁矢量势的强大工具。

作为一个重要的应用，我们可以计算一个以恒定非相对论速度 $\vec{v}$ 运动的点电荷 $q$ 所产生的[磁矢量势](@entry_id:141246) [@problem_id:1621764]。这样一个运动的点电荷可以被模型化为一个瞬时电流密度 $\vec{J}(\vec{r}') = q\vec{v}\delta^{(3)}(\vec{r}' - \vec{r}_q(t))$，其中 $\vec{r}_q(t)$ 是[电荷](@entry_id:275494)在时刻 $t$ 的位置，$\delta^{(3)}$ 是[三维狄拉克δ函数](@entry_id:274703)。假设在某一时刻，[电荷](@entry_id:275494)恰好位于坐标原点，即 $\vec{r}_q = \vec{0}$。将其代入积分公式：
$$
\vec{A}(\vec{r}) = \frac{\mu_0}{4\pi} \int \frac{q\vec{v}\delta^{(3)}(\vec{r}')}{|\vec{r} - \vec{r}'|} d^3r'
$$
利用δ函数的[筛选性质](@entry_id:265662)，积分的结果是：
$$
\vec{A}(\vec{r}) = \frac{\mu_0}{4\pi} \frac{q\vec{v}}{|\vec{r}|}
$$
这个简洁的结果表明，一个[运动点电荷](@entry_id:273707)产生的磁矢量势的方向与[电荷](@entry_id:275494)的运动方向相同，其大小与速度成正比，并随距离的倒数减小。这个结果是[李纳-维谢尔势](@entry_id:262307)在低速极限下的特例。

我们也可以从已知的矢量势反向求解产生它的电流源 [@problem_id:1833422]。利用 $\vec{J} = \frac{1}{\mu_0}\nabla \times \vec{B}$ 和 $\vec{B} = \nabla \times \vec{A}$，我们得到 $\vec{J} = \frac{1}{\mu_0}\nabla \times (\nabla \times \vec{A})$。例如，给定一个矢量势 $\vec{A} = C(y^2 \hat{x} - x^2 \hat{y})$，首先计算[磁场](@entry_id:153296) $\vec{B} = \nabla \times \vec{A} = -2C(x+y)\hat{z}$。然后计算[磁场的旋度](@entry_id:261797) $\nabla \times \vec{B} = -2C\hat{x} + 2C\hat{y}$。最后得到电流密度 $\vec{J} = \frac{1}{\mu_0}\nabla \times \vec{B} = \frac{2C}{\mu_0}(-\hat{x} + \hat{y})$。这是一个均匀但方向固定的[电流密度](@entry_id:190690)。

### 矢量势的物理应用：[磁通量](@entry_id:268943)

磁矢量势不仅是一个数学工具，它还与一个重要的物理量——**磁通量**（magnetic flux）有着直接而优美的联系。通过一个开[曲面](@entry_id:267450) $S$ 的[磁通量](@entry_id:268943) $\Phi_B$ 定义为：
$$
\Phi_B = \iint_S \vec{B} \cdot d\vec{S}
$$
将 $\vec{B} = \nabla \times \vec{A}$ 代入，我们得到：
$$
\Phi_B = \iint_S (\nabla \times \vec{A}) \cdot d\vec{S}
$$
根据斯托克斯定理（Stokes' theorem），一个矢量场旋度的面积分等于该矢量场沿该面积边界的[环路积分](@entry_id:164828)。设 $C$ 为[曲面](@entry_id:267450) $S$ 的闭合边界线，则：
$$
\Phi_B = \oint_C \vec{A} \cdot d\vec{l}
$$
这个关系极为重要。它意味着要计算穿过一个[曲面](@entry_id:267450)的总[磁通量](@entry_id:268943)，我们无需知道每一点的[磁场](@entry_id:153296) $\vec{B}$，只需知道该[曲面](@entry_id:267450)边界线上的磁矢量势 $\vec{A}$ 并计算其[线积分](@entry_id:141417)即可。在许多情况下，这使得计算大大简化 [@problem_id:1833402]。

例如，考虑一个由矢量势 $\vec{A} = C(x^2 + y^2)(-y\hat{i} + x\hat{j})$ 描述的[磁场](@entry_id:153296)。我们希望计算穿过位于 $xy$ 平面、半径为 $R$ 的圆盘的[磁通量](@entry_id:268943)。直接计算 $\vec{B}$ 再进行面积分会很复杂。但使用上述关系，我们只需在半径为 $R$ 的圆周上对 $\vec{A}$ 进行线积分。在极坐标下，该圆周上的 $x^2+y^2=R^2$，[线元](@entry_id:196833) $d\vec{l}$ 在 $\hat{\theta}$ 方向，且 $-y\hat{i} + x\hat{j} = r\hat{\theta}$。因此，在边界圆周上 $\vec{A} = C R^2 (R\hat{\theta}) = C R^3 \hat{\theta}$。线积分变为：
$$
\Phi_B = \oint_C \vec{A} \cdot d\vec{l} = \int_0^{2\pi} (C R^3 \hat{\theta}) \cdot (R d\theta \hat{\theta}) = \int_0^{2\pi} C R^4 d\theta = 2\pi C R^4
$$
这个计算过程比先求旋度再求[面积分](@entry_id:275394)要简洁得多。

更深层次地，磁矢量势的物理实在性在量子力学中得到了惊人的证实。在著名的阿哈罗诺夫-玻姆效应（Aharonov-Bohm effect）中，即使在[磁场](@entry_id:153296) $\vec{B}$ 为零的区域，只要[磁矢量势](@entry_id:141246) $\vec{A}$ 不为零，运动的[带电粒子](@entry_id:160311)（如电子）的量子行为（如[干涉条纹](@entry_id:176719)）仍然会受到影响。这表明 $\vec{A}$ 不仅仅是计算 $\vec{B}$ 的辅助工具，它本身就携带了[物理信息](@entry_id:152556)，是一个比 $\vec{B}$ 更为基本的物理量。

### 矢量势的存在条件

我们从 $\nabla \cdot \vec{B} = 0$ 出发引入了 $\vec{A}$。那么，是否任何满足 $\nabla \cdot \vec{B} = 0$ 的矢量场都一定能写成某个 $\vec{A}$ 的旋度呢？答案是肯定的，但需要满足一定的拓扑条件。

如果一个[磁场](@entry_id:153296) $\vec{B}$ 能够由一个在全域（或在一个单连通区域内）良好定义的矢量势 $\vec{A}$ 导出，即 $\vec{B} = \nabla \times \vec{A}$，那么根据散度定理（Divergence Theorem），通过任何闭合[曲面](@entry_id:267450) $S$ 的总磁通量必然为零：
$$
\oint_S \vec{B} \cdot d\vec{S} = \oint_S (\nabla \times \vec{A}) \cdot d\vec{S} = \int_V \nabla \cdot (\nabla \times \vec{A}) dV = 0
$$
其中 $V$ 是由 $S$ 包围的体积。这个结论——通过任何闭合[曲面](@entry_id:267450)的磁通量恒为零——是[高斯磁定律](@entry_id:182942)的积分形式，它等价于“不存在磁单极子”的论断。

现在，让我们考虑一个假设性的情况 [@problem_id:1621746]。假设存在一种粒子，它在原点产生一个径向向外的[磁场](@entry_id:153296) $\vec{B} = \frac{C}{r^2} \hat{r}$，其中 $C$ 是常数。这个场在 $r>0$ 的任何点都满足 $\nabla \cdot \vec{B} = 0$。然而，如果我们计算穿过一个以原点为球心、半径为 $R$ 的球面 $S_R$ 的[磁通量](@entry_id:268943)，会得到：
$$
\Phi_B = \oint_{S_R} \vec{B} \cdot d\vec{S} = \int_0^{2\pi}\int_0^\pi \left(\frac{C}{R^2}\hat{r}\right) \cdot (\hat{r} R^2 \sin\theta d\theta d\phi) = C \int_0^{2\pi}d\phi \int_0^\pi \sin\theta d\theta = 4\pi C
$$
由于 $C \neq 0$，这个通量不为零。这与我们从 $\vec{B}=\nabla \times \vec{A}$ 推导出的结论相矛盾。因此，我们得出结论：尽管这个假设的[磁场](@entry_id:153296)在 $r>0$ 的区域内是无散的，但它不可能由一个在整个 $r>0$ 区域内都良好定义的矢量势 $\vec{A}$ 导出。这个例子说明，$\nabla \cdot \vec{B} = 0$ 是 $\vec{B}$ 可以表示为 $\nabla \times \vec{A}$ 的必要条件，但要保证 $\vec{A}$ 在整个区域内都是良好定义的，还需要更强的全局条件，即通过任意闭合[曲面](@entry_id:267450)的磁通量为零。迄今为止，所有实验都证实了自然界中的[磁场](@entry_id:153296)满足这一更强的条件。

综上所述，[磁矢量势](@entry_id:141246)是电动力学中一个强大而深刻的概念。它源于[磁场](@entry_id:153296)的无散特性，因[规范自由度](@entry_id:160491)而具有数学上的灵活性，通过[库仑规范](@entry_id:273044)等选择可以极大简化计算，并通过与[磁通量](@entry_id:268943)的直接联系及在量子力学中的核心作用，展现了其深刻的物理实在性。