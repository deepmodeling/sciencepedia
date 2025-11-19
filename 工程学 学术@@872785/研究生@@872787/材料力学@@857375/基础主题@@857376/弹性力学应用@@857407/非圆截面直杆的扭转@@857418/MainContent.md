## 引言
在工程实践中，从传动轴到飞机机翼的梁结构，许多承力构件都会承受扭转载荷。初等[材料力学](@entry_id:201885)为圆形[截面](@entry_id:154995)杆的扭转提供了简洁而精确的分析方法，其核心是“平面假定”——即[横截面](@entry_id:154995)在扭转过程中保持为平面。然而，对于形状更为普遍的非圆形[截面](@entry_id:154995)杆，这一基本假设不再成立，导致初等理论的应用范围受到极大限制。当扭矩作用于非圆形[截面](@entry_id:154995)杆时，其[横截面](@entry_id:154995)不仅会绕轴线转动，还会发生平面外的位移，即“翘曲”。这一现象从根本上改变了[截面](@entry_id:154995)上的应力[分布](@entry_id:182848)和杆件的[扭转刚度](@entry_id:182139)，对其力学行为产生决定性影响。

本文旨在系统地解决这一知识鸿沟，深入探讨非圆形[截面](@entry_id:154995)[棱柱杆](@entry_id:190143)扭转的力学原理和工程应用。我们将超越初等理论的局限，基于更为普适的[圣维南扭转](@entry_id:194475)理论，为读者构建一个完整而严谨的分析框架。

本文将分为三个核心部分。在“原理与机制”一章中，我们将详细阐述[圣维南扭转](@entry_id:194475)问题的数学描述，引入[翘曲函数](@entry_id:187475)的概念来量化平面外位移，并介绍功能强大的[普朗特应力函数](@entry_id:187068)法，它将复杂的三维问题简化为二维问题。接着，在“应用与跨学科联系”一章中，我们将展示该理论如何在结构设计、[失效分析](@entry_id:266723)以及计算力学和[材料科学](@entry_id:152226)等多个领域中发挥关键作用，特别关注薄壁结构和[应力集中](@entry_id:160987)等重要工程问题。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固所学理论，加深对核心概念的理解。通过本次学习，你将掌握分析和设计承受扭转作用的非圆形[截面](@entry_id:154995)构件所需的关键理论工具。

## 原理与机制

在对非圆形[截面](@entry_id:154995)[棱柱杆](@entry_id:190143)的扭转行为进行分析时，我们必须超越初等[梁理论](@entry_id:176426)中“平面假定”的限制。当扭矩作用于非圆形[截面](@entry_id:154995)杆时，[横截面](@entry_id:154995)不仅会绕杆轴线转动，还会发生翘曲，即沿杆轴线方向产生平面外位移。本章将从基本原理出发，系统阐述[圣维南扭转](@entry_id:194475)理论（Saint-Venant torsion theory），介绍描述这一现象的两种核心数学方法——位移法（[翘曲函数](@entry_id:187475)）和应力法（[普朗特应力函数](@entry_id:187068)），并探讨这些理论在分析和设计中的应用。

### [圣维南扭转](@entry_id:194475)问题：运动学与翘曲

我们考虑一根沿 $z$ 轴放置的均匀[棱柱杆](@entry_id:190143)，其在 $z=0$ 处固定，并在另一端受到一个纯扭矩作用。根据圣维南半逆法（semi-inverse method），我们首先对位移场做出一个合理的假设。我们假定每个[横截面](@entry_id:154995)都绕 $z$ 轴作刚性转动，且转动角 $\theta$ 仅是轴向坐标 $z$ 的函数。此外，我们允许[横截面](@entry_id:154995)发生平面外位移，即翘曲，该位移是[截面](@entry_id:154995)[内坐标](@entry_id:169764) $(x, y)$ 的函数。对于单位长度扭转角 $\theta' = \frac{d\theta}{dz}$ 为常数的纯扭转情况，位移分量可以表示为：

$u_x = -\theta' z y$
$u_y = \theta' z x$
$u_z = w(x, y)$

这里，$u_x$ 和 $u_y$ 描述了[截面](@entry_id:154995)的刚性转动，而 $u_z = w(x, y)$ 代表了不随 $z$ 变化的翘曲位移。为方便起见，我们将翘曲位移写成与扭转角 $\theta'$ 成正比的形式，定义**[翘曲函数](@entry_id:187475)** $\psi(x, y)$：

$u_z(x, y) = \theta' \psi(x, y)$

这个定义是合理的，因为如果没有扭转（$\theta'=0$），就不会有翘曲。[@problem_id:2927234] [@problem_id:2704686]

根据小应变假设，我们可以计算应变分量。[法向应变](@entry_id:204633) $\varepsilon_{xx}$、$\varepsilon_{yy}$ 和面内[剪应变](@entry_id:175241) $\gamma_{xy}$ 均为零。一个关键的结果是，由于纯扭转假设，杆件上任意[横截面](@entry_id:154995)的轴向[合力](@entry_id:163825)为零，这可以证明[轴向应变](@entry_id:160811) $\varepsilon_{zz}$ 也必须为零。[@problem_id:2927234] 因此，在[圣维南扭转](@entry_id:194475)理论中，唯一可能非零的应变分量是横向[剪应变](@entry_id:175241) $\gamma_{xz}$ 和 $\gamma_{yz}$：

$\gamma_{xz} = \frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x} = -\theta' y + \theta' \frac{\partial \psi}{\partial x} = \theta' \left( \frac{\partial \psi}{\partial x} - y \right)$

$\gamma_{yz} = \frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y} = \theta' x + \theta' \frac{\partial \psi}{\partial y} = \theta' \left( \frac{\partial \psi}{\partial y} + x \right)$

这些表达式清晰地表明，[剪应变](@entry_id:175241)由两部分组成：一部分源于[截面](@entry_id:154995)的刚性转动（$-\theta'y$ 和 $\theta'x$），另一部分源于翘曲的贡献（$\theta'\frac{\partial \psi}{\partial x}$ 和 $\theta'\frac{\partial \psi}{\partial y}$）。[@problem_id:2927234]

#### 翘曲的必然性

为什么非圆形[截面](@entry_id:154995)必须发生翘曲？我们可以通过一个思想实验来理解。[@problem_id:2704684] 假设[截面](@entry_id:154995)不发生翘曲，即 $\psi(x, y) = 0$。此时，应[力场](@entry_id:147325)（对于线弹性[各向同性材料](@entry_id:170678)，$\tau_{xz} = G\gamma_{xz}$，$\tau_{yz} = G\gamma_{yz}$）将简化为：

$\tau_{xz} = -G\theta'y$
$\tau_{yz} = G\theta'x$

这个应[力场](@entry_id:147325)在杆的内部满足平衡方程。然而，在杆的侧表面上，必须满足无[面力边界条件](@entry_id:167112)。侧表面的法向矢量为 $\mathbf{n}=(n_x, n_y, 0)$，轴向面力分量 $t_z$ 为：

$t_z = \tau_{xz}n_x + \tau_{yz}n_y = (-G\theta'y)n_x + (G\theta'x)n_y = G\theta'(xn_y - yn_x)$

为了使侧表面无面力，必须有 $t_z = 0$，即 $xn_y - yn_x = 0$。这个条件意味着在边界上的任意一点，其位置矢量 $(x, y)$ 必须平行于其法向矢量 $(n_x, n_y)$。这正是圆的几何定义。对于任何非圆形[截面](@entry_id:154995)，这个条件通常不成立。因此，“平面保持平面”的假设对于非圆形[截面](@entry_id:154995)会导致在侧表面上出现虚假的轴向剪应力，这与物理实际相悖。为了消除这些虚假面力，[截面](@entry_id:154995)必须发生翘曲。翘曲位移 $\psi(x,y)$ 的引入，正是为了调整应[力场](@entry_id:147325)，以满足侧表面无面力的边界条件。

#### [翘曲函数](@entry_id:187475)的控制方程

[翘曲函数](@entry_id:187475) $\psi(x, y)$ 并非任意的，它由材料内部的平衡和边界条件唯一确定。在没有体力的情况下，应力[平衡方程](@entry_id:172166)为 $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$。对于扭转问题，非平凡的[平衡方程](@entry_id:172166)是：

$\frac{\partial \tau_{xz}}{\partial x} + \frac{\partial \tau_{yz}}{\partial y} = 0$

将应力表达式 $\tau_{xz} = G\theta'(\psi_{,x}-y)$ 和 $\tau_{yz} = G\theta'(\psi_{,y}+x)$ 代入上式，我们得到：

$G\theta' \left( \frac{\partial^2 \psi}{\partial x^2} \right) + G\theta' \left( \frac{\partial^2 \psi}{\partial y^2} \right) = 0$

这表明[翘曲函数](@entry_id:187475) $\psi(x, y)$ 必须是一个**调和函数**，即它满足拉普拉斯方程：

$\nabla^2 \psi = 0$

同时，在侧边界 $\partial A$ 上，无面力条件 $t_z = \tau_{xz}n_x + \tau_{yz}n_y = 0$ 给出了 $\psi$ 必须满足的**[诺伊曼边界条件](@entry_id:142124)** (Neumann boundary condition)：

$G\theta'(\psi_{,x}-y)n_x + G\theta'(\psi_{,y}+x)n_y = 0 \implies \frac{\partial \psi}{\partial x}n_x + \frac{\partial \psi}{\partial y}n_y = yn_x - xn_y$

即[法向导数](@entry_id:169511) $\frac{\partial \psi}{\partial n} = yn_x - xn_y$。[@problem_id:2927234] [@problem_id:2704686] 这个边值问题完整地定义了给定[截面](@entry_id:154995)形状的[翘曲函数](@entry_id:187475)。

### 圆形[截面](@entry_id:154995)的特殊情况

[圣维南理论](@entry_id:195321)的优雅之处在于，它统一了解释了圆形[截面](@entry_id:154995)和非圆形[截面](@entry_id:154995)的行为。对于一个半径为 $R$、圆心在原点的圆形[截面](@entry_id:154995)，其边界上的任意一点 $(x, y)$ 满足 $x^2 + y^2 = R^2$。该点的外法向矢量为 $\mathbf{n} = (x/R, y/R)$，即 $n_x = x/R$ 和 $n_y = y/R$。我们将此代入[翘曲函数](@entry_id:187475)的边界条件中：

$\frac{\partial \psi}{\partial n} = y n_x - x n_y = y \left(\frac{x}{R}\right) - x \left(\frac{y}{R}\right) = \frac{xy - xy}{R} = 0$

因此，对于圆形[截面](@entry_id:154995)，[翘曲函数](@entry_id:187475)的边界条件退化为齐次的[诺伊曼条件](@entry_id:165471) $\frac{\partial \psi}{\partial n} = 0$。[@problem_id:2926965] 对于拉普拉斯方程 $\nabla^2 \psi = 0$，在单连通域上，这个[齐次边界条件](@entry_id:750371)意味着其解 $\psi$ 只能是一个常数。常数翘曲对应于整个[截面](@entry_id:154995)的刚体平移，不产生应变或应力，因此在物理上没有意义。我们可以不失[一般性](@entry_id:161765)地取 $\psi = 0$。

这个结果表明，对于圆形[截面](@entry_id:154995)，[翘曲函数](@entry_id:187475)为零，即**圆形[截面](@entry_id:154995)在扭转时不会发生翘曲**，“平面保持平面”的假设是成立的。这解释了为什么初等扭转理论对圆形杆是精确的，而对非圆形杆则是不精确的。只有当[截面](@entry_id:154995)几何形状导致翘曲边界条件非齐次时，才会出现非平凡的翘曲位移。

### [普朗特应力函数](@entry_id:187068)法

除了直接求解[翘曲函数](@entry_id:187475)的位移法，还有一种等效且在很多情况下更强大的方法，即[普朗特应力函数](@entry_id:187068)法。此方法从满足平衡方程出发。如前所述，[平衡方程](@entry_id:172166)为 $\frac{\partial \tau_{xz}}{\partial x} + \frac{\partial \tau_{yz}}{\partial y} = 0$。

这个方程的形式表明，应力矢量场 $(\tau_{xz}, \tau_{yz})$ 是无散的。因此，我们可以引入一个[标量势](@entry_id:276177)函数，即**[普朗特应力函数](@entry_id:187068)** $\varphi(x, y)$，来自动满足平衡方程：

$\tau_{xz} = \frac{\partial \varphi}{\partial y}$
$\tau_{yz} = -\frac{\partial \varphi}{\partial x}$

将此定义代入平衡方程，会得到 $\frac{\partial^2\varphi}{\partial x \partial y} - \frac{\partial^2\varphi}{\partial y \partial x} = 0$，这是一个恒等式。[@problem_id:2704689]

接下来，我们必须满足应变协调条件。通过将应力函数定义代入[应力-应变关系](@entry_id:274093)，再利用[应变-位移关系](@entry_id:173321)并消除[翘曲函数](@entry_id:187475) $\psi$，可以得到应力函数 $\varphi$ 必须满足的控制方程。这个过程最终导出一个**[泊松方程](@entry_id:143763)** (Poisson's equation)：

$\nabla^2 \varphi = \frac{\partial^2 \varphi}{\partial x^2} + \frac{\partial^2 \varphi}{\partial y^2} = -2G\theta'$

现在考虑边界条件。在无面力的侧边界 $\partial A$ 上，$\tau_{xz}n_x + \tau_{yz}n_y = 0$。代入 $\varphi$ 的定义：

$\frac{\partial \varphi}{\partial y}n_x - \frac{\partial \varphi}{\partial x}n_y = 0$

这个表达式恰好是 $\varphi$ 沿边界的切向导数 $\frac{d\varphi}{ds}$。因此，$\frac{d\varphi}{ds} = 0$，这意味着**应力函数 $\varphi$ 在每个连通的边界上都必须是一个常数**。[@problem_id:2704689] 对于实心杆这样的单连通[截面](@entry_id:154995)，只有一个边界，我们可以任意设定这个常数的值。通常，我们取 $\varphi = 0$。

为了方便分析和比较，我们常常引入一个**归一化应力函数** $\psi_p = \frac{\varphi}{G\theta'}$。将此代入[泊松方程](@entry_id:143763)和边界条件，得到一个与材料属性和扭转角无关的纯几何问题：

$\nabla^2 \psi_p = -2 \quad \text{在 } A \text{ 内}$
$\psi_p = 0 \quad \text{在 } \partial A \text{ 上}$

这个优美的公式是解决扭转问题的核心。[@problem_id:2704730]

### [扭转刚度](@entry_id:182139)与[薄膜比拟](@entry_id:203748)

杆件抵抗扭转变形的能力由其**[扭转刚度](@entry_id:182139)**（torsional rigidity）来衡量，它通常表示为 $GJ$，其中 $G$ 是[剪切模量](@entry_id:167228)，$J$ 是**[扭转常数](@entry_id:168130)**，一个纯粹依赖于[截面](@entry_id:154995)几何形状的量。扭矩 $T$ 与单位长度扭转角 $\theta'$ 之间的关系定义了[扭转刚度](@entry_id:182139)：

$T = GJ\theta'$

利用[普朗特应力函数](@entry_id:187068)，我们可以推导出扭矩与应力函数的直接关系。扭矩的定义为 $T = \iint_A (x\tau_{yz} - y\tau_{xz}) dA$。代入 $\varphi$ 的定义并使用[格林公式](@entry_id:173118)，可以证明：

$T = 2 \iint_A \varphi \, dA$

这个重要的结果表明，扭矩等于应力函数在整个[截面](@entry_id:154995)上积分的两倍。[@problem_id:2704729] 结合[扭转刚度](@entry_id:182139)的定义，我们得到[扭转常数](@entry_id:168130) $J$ 的表达式：

$J = \frac{T}{G\theta'} = \frac{2}{G\theta'} \iint_A \varphi \, dA = 2 \iint_A \psi_p \, dA$

这提供了一种计算[扭转常数](@entry_id:168130)的方法：求解归一化的泊松方程，然后将其解在[截面](@entry_id:154995)面积上积分并乘以2。

[路德维希·普朗特](@entry_id:268561)（[Ludwig Prandtl](@entry_id:268561)）提出了一个巧妙的物理类比，称为**[薄膜比拟](@entry_id:203748)**（membrane analogy），它为扭转问题提供了强大的直观理解。考虑一个绷紧在与[截面](@entry_id:154995)形状相同的框架上的薄膜，对其施加均匀的压力 $p$。薄膜的微小横向位移 $u(x, y)$ 满足的方程为 $\nabla^2 u = -p/S$，其中 $S$ 是薄膜的张力。这个方程与应力函数的方程 $\nabla^2 \varphi = -2G\theta'$ 在形式上完全相同。

这种类比关系如下：[@problem_id:2704731]
1.  薄膜的**位移** $u(x,y)$ 正比于应力函数 $\varphi(x,y)$。
2.  薄膜下方的**体积** $V = \iint u \, dA$ 正比于扭矩 $T$。
3.  薄膜在某点的**斜率** $|\nabla u|$ 正比于该点的剪应力大小 $|\boldsymbol{\tau}| = \sqrt{\tau_{xz}^2 + \tau_{yz}^2}$。
4.  薄膜的**等高线**对应于应力[流线](@entry_id:266815)。

[薄膜比拟](@entry_id:203748)告诉我们，对于给定面积的[截面](@entry_id:154995)，其[扭转常数](@entry_id:168130) $J$ 正比于相应形状的薄膜在单位压力下所能围出的体积。什么样的形状能围出最大的体积呢？答案是**最“紧凑”的形状**。在所有等面积的形状中，圆的[周长](@entry_id:263239)最短，最接近于一个点。因此，圆形框架上的薄膜可以鼓得最高，围出的体积最大。这直观地解释了为什么**在所有等面积的[截面](@entry_id:154995)中，圆形[截面](@entry_id:154995)具有最大的[扭转刚度](@entry_id:182139)**。

对于其他形状，我们可以定性地排序。一个正方形比一个等边三角形更“紧凑”，因此[扭转刚度](@entry_id:182139)更大。而一个非常细长的矩形，由于其大部分区域都非常靠近边界（薄膜位移为零），薄膜几乎无法鼓起，所以其围出的体积非常小，[扭转刚度](@entry_id:182139)也极低。因此，对于面积相同的四个[截面](@entry_id:154995)：圆、正方形、等边三角形和细长矩形，其[扭转常数](@entry_id:168130) $J$ 的排序为：[@problem_id:2704731]

$J_{\text{圆}} > J_{\text{正方形}} > J_{\text{等边三角形}} > J_{\text{细长矩形}}$

#### [扭转常数](@entry_id:168130) $J$ 与[极惯性矩](@entry_id:196420) $I_p$ 的关系

对于圆形[截面](@entry_id:154995)，[扭转常数](@entry_id:168130) $J$ 恰好等于其[截面](@entry_id:154995)[极惯性矩](@entry_id:196420) $I_p = \iint_A (x^2+y^2) dA$。但对于任何非圆形[截面](@entry_id:154995)，我们有严格的不等式 $J  I_p$。

我们可以利用[最小势能原理](@entry_id:173340)来严格证明这一点。[@problem_id:2704720] 杆的总应变能可以表示为 $U = \frac{1}{2}GJ(\theta')^2 L$。势能原理指出，在所有满足运动学条件的位移场中，真实的[位移场](@entry_id:141476)（即同时满足[平衡方程](@entry_id:172166)和边界条件的场）使总应变能最小。

我们可以构造一个不允许翘曲的假想位移场（即 $\psi=0$）。这个场的[应变能](@entry_id:162699)经计算为 $U_{\text{trial}} = \frac{1}{2}GI_p(\theta')^2 L$。由于真实解的能量不会超过任何试验场的能量，我们有 $U_{\text{real}} \le U_{\text{trial}}$，即 $J \le I_p$。

等号仅在试验场就是真实解时成立。我们已经知道，无翘曲场仅在圆形[截面](@entry_id:154995)上才满足无[面力边界条件](@entry_id:167112)。因此，对于任何非圆形[截面](@entry_id:154995)，真实解必须包含翘曲，这使得杆件能够“松弛”到一个能量更低的状态。这种“松弛”意味着杆件变得更“柔”，即其抵抗扭转的能力下降。因此，对于非圆形[截面](@entry_id:154995)，不等式是严格的：$J  I_p$。翘曲是降低[非圆形截面扭转](@entry_id:200449)刚度的根本物理机制。

### 高级主题

#### 多连通[截面](@entry_id:154995)的扭转

当[截面](@entry_id:154995)包含孔洞时（例如空心管），我们称之为多连通[截面](@entry_id:154995)。[普朗特应力函数](@entry_id:187068)法依然适用，但有一些重要修正。[@problem_id:2704664]

1.  **边界条件**：应力函数 $\varphi$ 在每个边界（包括外边界 $\Gamma_0$ 和每个内孔边界 $\Gamma_k$）上都必须为常数。我们可以设定外边界上的值为 $\varphi|_{\Gamma_0} = 0$，但内孔边界上的常数值 $C_k = \varphi|_{\Gamma_k}$ 是未知的。

2.  **附加约束**：为了确定这 $m$ 个未知的常数 $C_k$，我们需要 $m$ 个附加条件。这些条件来自于物理要求：翘曲位移 $w(x, y)$ 必须是单值的。这意味着绕任何一个内孔边界积分一周，翘曲位移的变化量必须为零。这个要求可以转化为对应力函数[法向导数](@entry_id:169511)的积分约束：

    $\oint_{\Gamma_k} \frac{\partial \varphi}{\partial n} ds = 2G\theta'A_k$

    其中 $A_k$ 是第 $k$ 个孔洞的面积，法向 $\mathbf{n}$ 指向材料区域之外（即指向孔洞内部）。

3.  **扭矩公式**：对于多连通[截面](@entry_id:154995)，扭矩的表达式也需要修正，以包含内边界上的常数 $C_k$ 的贡献：

    $T = 2 \iint_A \varphi \, dA + 2 \sum_{k=1}^{m} C_k A_k$

#### [非均匀扭转](@entry_id:187890)与翘曲约束

[圣维南理论](@entry_id:195321)假设单位长度扭转角 $\theta'$ 是常数，这被称为均匀扭转。然而，在某些情况下，例如当扭矩沿杆长变化，或者杆端部的翘曲受到约束时，$\theta'$ 将不再是常数，这种情况称为**[非均匀扭转](@entry_id:187890)**。

这在薄壁开口[截面](@entry_id:154995)（如工字钢、槽钢）中尤其重要。当这样的杆件一端被焊接到一个刚性平板上时，该端的翘曲会受到完全约束 ($u_z=0$)。[@problem_id:2704717] 这将引发一系列新的力学行为：

1.  **轴向正应力**：由于翘曲位移 $u_z = \theta'(z)\omega(x,y)$，当 $\theta'$ 随 $z$ 变化时，会产生[轴向应变](@entry_id:160811) $\varepsilon_z = \frac{\partial u_z}{\partial z} = \theta''(z)\omega(x,y)$。这进而导致轴向正应力 $\sigma_z = E\varepsilon_z = E\theta''(z)\omega(x,y)$。这些应力在[截面](@entry_id:154995)上的[分布](@entry_id:182848)与[翘曲函数](@entry_id:187475) $\omega(x,y)$ 的形状成正比。

2.  **[双力矩](@entry_id:184817) (Bimoment)**：这些自相平衡的轴向正应力形成一个高阶的[应力合力](@entry_id:180269)，称为**[双力矩](@entry_id:184817)** $B(z)$。其定义为 $B(z) = \int_A \sigma_z \omega \, dA = EI_\omega \theta''(z)$，其中 $I_\omega = \int_A \omega^2 dA$ 是[截面](@entry_id:154995)的**翘曲惯性矩**。

3.  **总扭矩**：在[非均匀扭转](@entry_id:187890)中，总扭矩由两部分组成：圣维南扭矩 $T_{SV} = GJ\theta'$ 和翘曲扭矩 $T_\omega = -EI_\omega \theta'''$。总扭矩为：

    $T(z) = T_{SV} + T_\omega = GJ\theta'(z) - EI_\omega \theta'''(z)$

4.  **端部效应**：翘曲约束的影响主要局限在杆的端部附近。这些由 $\sigma_z$ 和 $B$ 构成的附加应[力场](@entry_id:147325)会随着离约束端的距离呈指数衰减。这种衰减的特征长度为 $l_c = \sqrt{\frac{EI_\omega}{GJ}}$。在远离端部（距离大于几倍 $l_c$）的区域，杆的行为将回归到圣维南纯扭转状态。这正是[圣维南原理](@entry_id:165302)的一个具体体现。[@problem_id:2704717]
*Note: Some literature uses a convention where $u_z = -\theta'(z)\omega(x,y)$, leading to $\sigma_z = -E\theta''(z)\omega(x,y)$ and $B(z) = -EI_\omega\theta''(z)$. The final governing equation for $T(z)$ remains the same. The text was edited to follow one consistent convention ($u_z = \theta'(z)\omega(x,y)$) for clarity.*