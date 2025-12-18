## 引言
在固体力学中，分析诸如长梁、管道或地质构造等柱状体的力学行为是一项基本而又普遍的任务。完全采用三维实体模型进行分析虽然精确，但往往计算成本高昂且不必要。因此，力学家们发展了多种二维简化模型。然而，经典的[平面应力与平面应变](@entry_id:172357)模型虽大大简化了问题，却也因其过于严格的假设（分别为零轴向应力或零[轴向应变](@entry_id:160811)）而无法捕捉结构在轴向上的整体伸缩，这一效应在许多工程实践中至关重要。

广义[平面应变](@entry_id:167046)（Generalized Plane Strain, GPS）理论的提出，正是为了填补这一空白。它是一种更为精致的二维理想化模型，通过允许一个均匀但未知的[轴向应变](@entry_id:160811)存在，巧妙地将三维效应融入二维分析框架中，从而在[计算效率](@entry_id:270255)和物理真实性之间取得了理想的平衡。本文旨在系统性地阐述广义平面应变理论的核心思想、应用范围及其在现代力学分析中的重要地位。

在接下来的章节中，我们将首先在“原理与机制”中深入探讨广义[平面应变](@entry_id:167046)的运动学基础、本构关系，并阐明圣文南原理如何为其有效性提供坚实的物理依据。随后，在“应用与[交叉](@entry_id:147634)学科联系”一章，我们将通过一系列来自工程结构、[断裂力学](@entry_id:141480)、[热力学](@entry_id:141121)乃至[地球物理学](@entry_id:147342)的实例，展示该理论解决实际问题的强大能力。最后，通过“动手实践”部分的引导性问题，您将有机会将理论知识应用于具体计算，从而巩固和深化对这一重要概念的理解。

## 原理与机制

在连续介质力学中，为了分析在某个方向上尺寸远大于[横截面](@entry_id:154995)尺寸的柱状体（如梁、杆、长筒）的行为，我们常常采用降维的简化方法。广义[平面应变](@entry_id:167046)（Generalized Plane Strain, GPS）便是一种关键的二维理想化模型。它在保持问题二维性的同时，能够捕捉到物体沿轴向发生的均匀伸长、收缩或弯曲等三维效应。本章将深入探讨广义平面应变的基本原理、[本构关系](@entry_id:186508)、问题的[适定性](@entry_id:148590)及其物理依据。

### 二维理想化的运动学基础

我们首先从运动学角度出发，考察三维物体变形的二维简化。考虑一个沿 $z$ 轴方向延伸的柱状体，其[位移场](@entry_id:141476)在笛卡尔坐标系 $(x, y, z)$ 下表示为 $\mathbf{u} = (u_x, u_y, u_z)$。根据小应变理论，应变分量由[位移梯度](@entry_id:165352)确定。

#### 严格平面应变

最严格的二维简化是**严格[平面应变](@entry_id:167046)**（Strict Plane Strain）。该模型的核心[运动学](@entry_id:173318)假设是，物体的变形完全被限制在 $x$-$y$ 平面内，且这种变形在沿 $z$ 轴的任何[横截面](@entry_id:154995)上都是相同的。这等价于以下位移场形式：

$u_x = u_x(x, y)$
$u_y = u_y(x, y)$
$u_z = 0$

在此假设下，所有与 $z$ 坐标相关的应变分量均为零。具体而言，轴向[正应变](@entry_id:204633) $\varepsilon_{zz} = \frac{\partial u_z}{\partial z} = 0$，横向剪切应变 $\gamma_{xz} = \frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x} = 0$ 和 $\gamma_{yz} = \frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y} = 0$。因此，严格平面应变状态下，只有面内应变分量 $\varepsilon_{xx}$、$\varepsilon_{yy}$ 和 $\gamma_{xy}$ 可能非零，并且它们仅是 $x$ 和 $y$ 的函数。

#### 广义[平面应变](@entry_id:167046)

严格平面应变模型虽然简洁，但其 $u_z=0$ 的假设过于严苛，无法描述长柱体在轴向力或温度变化下发生的整体伸缩。**广义平面应变**（Generalized Plane Strain, GPS）通过放宽这一限制，提供了更灵活且贴近实际的模型。

GPS模型保留了“平面”的核心特征，即所有场量（位移、应变、应力）的面内[分布](@entry_id:182848)不随轴向坐标 $z$ 变化。为了满足这一要求，同时允许[轴向变形](@entry_id:180213)，[位移场](@entry_id:141476)必须具有特定的函数形式。如果所有应变分量都与 $z$ 无关，那么位移场最普遍的形式为：

$u_x = u_{x0}(x, y)$
$u_y = u_{y0}(x, y)$
$u_z = \varepsilon_0 z + g(x, y)$

其中 $\varepsilon_0$ 是一个常数，代表了均匀的轴向拉伸或压缩，而 $g(x,y)$ 是[横截面](@entry_id:154995)上的一个任意函数，被称为**[翘曲函数](@entry_id:187475)**（warping function）。

最常用且基础的GPS模型进一步假设横向剪切应变为零，即 $\gamma_{xz} = \gamma_{yz} = 0$。将上述位移场代入剪切应变的定义，我们得到：

$\gamma_{xz} = \frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x} = 0 + \frac{\partial g}{\partial x} = 0$
$\gamma_{yz} = \frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y} = 0 + \frac{\partial g}{\partial y} = 0$

这两个条件意味着函数 $g(x,y)$ 的梯度为零，因此 $g(x,y)$ 必定是一个常数。这个常数仅代表沿 $z$ 轴的刚体平移，对变形和应力没有影响，故可以忽略。因此，这种标准GPS模型的位移场简化为：

$u_x = u_{0}(x, y)$
$u_y = v_{0}(x, y)$
$u_z = \varepsilon_{0} z$

其中 $\varepsilon_0$ 是一个待定的常数。根据[应变-位移关系](@entry_id:173321)，我们可以直接计算出该[位移场](@entry_id:141476)对应的应变状态 ：
- **面内应变**：$\varepsilon_{xx} = \frac{\partial u_0}{\partial x}$, $\varepsilon_{yy} = \frac{\partial v_0}{\partial y}$, $\gamma_{xy} = \frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x}$。它们仅是 $x, y$ 的函数。
- **轴向[正应变](@entry_id:204633)**：$\varepsilon_{zz} = \frac{\partial u_z}{\partial z} = \varepsilon_0$，这是一个空间上均匀的常数。
- **横向剪切应变**：$\gamma_{xz} = 0$, $\gamma_{yz} = 0$。

总结来说，标准GPS模型的[运动学](@entry_id:173318)核心是：允许存在一个未知的、均匀的[轴向应变](@entry_id:160811) $\varepsilon_{zz}$，同时保持横向剪切应变为零，且所有场量在面内的[分布](@entry_id:182848)与轴向坐标 $z$ 无关。

### 广义平面应变的本构关系

建立了运动学框架后，我们接下来考察GPS状态下的[应力-应变关系](@entry_id:274093)。对于一个线弹性[各向同性材料](@entry_id:170678)，其三维[本构关系](@entry_id:186508)（胡克定律）可以用拉梅参数 $\lambda$ 和 $\mu$ 表示为：

$\sigma_{ij} = \lambda \delta_{ij} \varepsilon_{kk} + 2\mu \varepsilon_{ij}$

其中，$\varepsilon_{kk} = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}$ 是体积应变。

在GPS条件下，$\varepsilon_{xz} = \varepsilon_{yz} = 0$，因此对应的横向[剪切应力](@entry_id:137139)也为零：$\sigma_{xz} = 2\mu\varepsilon_{xz} = 0$，$\sigma_{yz} = 2\mu\varepsilon_{yz} = 0$。对于其他非零分量，我们将GPS的应变形式代入[本构方程](@entry_id:138559)：

$\sigma_{xx} = \lambda(\varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}) + 2\mu\varepsilon_{xx}$
$\sigma_{yy} = \lambda(\varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}) + 2\mu\varepsilon_{yy}$
$\sigma_{zz} = \lambda(\varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz}) + 2\mu\varepsilon_{zz}$
$\sigma_{xy} = 2\mu\varepsilon_{xy} = \mu\gamma_{xy}$

这里的 $\varepsilon_{zz}$ 是一个常数。这些方程可以整理成一个矩阵形式，清晰地展示应力向量 $(\sigma_{xx}, \sigma_{yy}, \sigma_{xy}, \sigma_{zz})^T$ 与应变向量 $(\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}, \varepsilon_{zz})^T$ 之间的[线性关系](@entry_id:267880)。将[本构关系](@entry_id:186508)用[杨氏模量](@entry_id:140430) $E$ 和[泊松比](@entry_id:158876) $\nu$ 表示，可以得到GPS状态下的有效二维[本构矩阵](@entry_id:164908) ：

$$
\begin{pmatrix}
\sigma_{xx} \\
\sigma_{yy} \\
\sigma_{xy} \\
\sigma_{zz}
\end{pmatrix}
=
\frac{E}{(1+\nu)(1-2\nu)}
\begin{pmatrix}
1-\nu  & \nu  & 0  & \nu \\
\nu  & 1-\nu  & 0  & \nu \\
0  & 0  & \frac{1-2\nu}{2}  & 0 \\
\nu  & \nu  & 0  & 1-\nu
\end{pmatrix}
\begin{pmatrix}
\varepsilon_{xx} \\
\varepsilon_{yy} \\
\gamma_{xy} \\
\varepsilon_{zz}
\end{pmatrix}
$$

这个关系是GPS分析的核心。它表明，面内应力不仅依赖于面内应变，还受到均匀[轴向应变](@entry_id:160811) $\varepsilon_{zz}$ 的影响。$\varepsilon_{zz}$ 相当于在面[内应力](@entry_id:193721)中引入了一个[静水压力](@entry_id:275365)项。

#### 与[平面应变](@entry_id:167046)及[平面应力](@entry_id:172193)的关系

GPS框架优雅地统一了经典的平面应变和平面应力模型。 

1.  **平面应变 (Plane Strain)**：其定义就是 $\varepsilon_{zz}=0$。将此条件代入GPS的 $\sigma_{zz}$ 表达式，我们得到在平面应变状态下，为维持 $\varepsilon_{zz}=0$ 所需的轴向应力：
    $\sigma_{zz}^{\text{(plane strain)}} = \lambda(\varepsilon_{xx} + \varepsilon_{yy})$
    这表明，除非面内应变之和处处为零，否则维持平面应变状态需要一个非零的、随 $(x,y)$ 变化的轴向应力。

2.  **[平面应力](@entry_id:172193) (Plane Stress)**：其定义是 $\sigma_{zz}=0$（以及 $\sigma_{xz}=\sigma_{yz}=0$，这在GPS中已满足）。将 $\sigma_{zz}=0$ 代入GPS的 $\sigma_{zz}$ 表达式，我们可以反解出维持平面应力状态所必需的[轴向应变](@entry_id:160811)：
    $\varepsilon_{zz}^{\text{(plane stress)}} = -\frac{\lambda}{\lambda + 2\mu}(\varepsilon_{xx} + \varepsilon_{yy}) = -\frac{\nu}{1-\nu}(\varepsilon_{xx} + \varepsilon_{yy})$
    这揭示了一个深刻的联系：平面应力状态本质上是一种特殊的广义[平面应变](@entry_id:167046)状态，其[轴向应变](@entry_id:160811) $\varepsilon_{zz}$ 并非为零，而是通过[泊松效应](@entry_id:158876)自动调整，以精确地使轴向应力 $\sigma_{zz}$ 保持为零。

### 广义平面应变边值问题

GPS模型的引入，将一个三维弹性力学问题转化为了一个二维问题，但这个二维问题带有一个额外的未知常数 $\varepsilon_{zz}$。为了使问题适定，我们必须补充一个额外的方程来求解 $\varepsilon_{zz}$。

首先，考察[平衡方程](@entry_id:172166) $\sigma_{ij,j} = 0$（假设[体力](@entry_id:174230)为零）。在GPS条件下，由于所有场量都与 $z$ 无关，且 $\sigma_{xz}=\sigma_{yz}=0$，三维平衡方程简化为：

$\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} = 0$
$\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} = 0$
$\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} = 0 \implies 0=0$

前两个方程正是经典的二维平面平衡方程。第三个方程（$z$ 方向的平衡）自动满足。这意味着，对于任意给定的常数 $\varepsilon_{zz}$，只要我们求解关于 $(u_x(x,y), u_y(x,y))$ 的二维边值问题，平衡方程总是被满足的。 

那么，如何确定 $\varepsilon_{zz}$ 呢？答案来自于沿 $z$ 轴的**全局约束或平衡条件**。一个适定的GPS问题，其边界条件通常如下设定 ：
- **侧面边界** ($\partial\Omega \times [0,L]$)：施加不依赖于 $z$ 的面内位移或面[内力](@entry_id:167605)边界条件。对于标准的GPS模型，还需假设侧面上的轴向剪切力为零 ($t_z=0$)。
- **端面边界** ($\Omega \times \{0, L\}$)：必须提供一个关于轴向行为的标量条件。这通常是以下两种情况之一：
    1.  **指定[轴向应变](@entry_id:160811)**：直接给定 $\varepsilon_{zz}$ 的值。例如，如果柱体的两端被固定且相对位移为 $\Delta$，则 $\varepsilon_{zz} = \Delta / L$。
    2.  **指定轴向[合力](@entry_id:163825)**：给定作用在[横截面](@entry_id:154995)上的总轴向力 $N_z = \int_{\Omega} \sigma_{zz} dA$。将 $\sigma_{zz}$ 的本构表达式代入此积分，即可得到一个包含 $\varepsilon_{zz}$ 和面内应变积分的代数方程，从而可以求解 $\varepsilon_{zz}$。

因此，一个完整的GPS求解过程通常是：将 $\varepsilon_{zz}$ 作为未知参数，求解一个[参数化](@entry_id:272587)的二维[边值问题](@entry_id:193901)，得到依赖于 $\varepsilon_{zz}$ 的解；然后利用全局轴向条件建立关于 $\varepsilon_{zz}$ 的方程，最终确定其值。

### 物理依据：圣文南原理

迄今为止，GPS一直被当作一种数学上的理想化模型。其作为一种有效物理近似的合理性，根植于弹性力学中的**圣文南原理**（Saint-Venant's Principle）。

圣文南原理的现代诠释是：对于一个弹性体，如果将作用于其上一小块区域的载荷替换为另一套静力等效（即具有相同合力和[合力矩](@entry_id:166772)）的载荷，那么这两套载荷引起的应[力场](@entry_id:147325)差异将是局部的，并会随着远离该区域而迅速衰减。

对于一个细长柱状体（$L \gg D$，其中 $L$ 是长度，$D$ 是[横截面](@entry_id:154995)特征尺寸），圣文南原理意味着：
1.  **端部效应的局部性**：作用在端部的具体载荷[分布](@entry_id:182848)所产生的应[力场](@entry_id:147325)，其[影响范围](@entry_id:166501)仅限于距端部约几个[横截面](@entry_id:154995)尺寸 $D$ 的区域内。在远离端部的“内部”区域，应[力场](@entry_id:147325)几乎不受端部载荷具体[分布](@entry_id:182848)形式的影响，而只依赖于其静力[合力](@entry_id:163825)。
2.  **内部解的 $z$ 无关性**：如果柱体侧面承受的载荷不沿 $z$ 轴变化，那么在远离两端的内部区域，其精确三维解将趋近于一个不依赖于 $z$ 的状态。这个渐近的内部解，正是广义平面应变状态。

数学上可以证明，端部效应（即精确三维解与GPS解的差异）会以指数形式衰减，其衰减形式为 $\exp(-\alpha z/D)$，其中 $z$ 是到端部的距离，$\alpha$ 是一个取决于[横截面](@entry_id:154995)形状和材料性质的正实数。 这为在长梁或长轴的工程分析中，忽略端部区域而直接使用GPS解提供了坚实的理论基础。

值得注意的是，即使作用在端部的轴向合力为零 ($N_z=0$)，内部解的[轴向应变](@entry_id:160811) $\varepsilon_{zz}$ 通常也不为零。这是因为侧面载荷会通过泊松效应引起面内变形，而为了保持轴向合力为零，物体必须产生一个补偿性的[轴向应变](@entry_id:160811)。因此，零轴向力并不意味着是严格平面应变状态。

### 扩展与局限性

#### 各向异性材料

GPS框架可以自然地推广到各向异性材料。以[正交各向异性材料](@entry_id:190111)为例，其[柔度矩阵](@entry_id:185679) $S_{ij}$ 包含更多独立的弹性常数。假设材料主轴与坐标轴重合，其本构关系为：
$\boldsymbol{\epsilon} = \boldsymbol{S} \boldsymbol{\sigma}$
在GPS条件下（$\gamma_{xz}=\gamma_{yz}=0$, $\sigma_{xz}=\sigma_{yz}=0$），我们可以从第三行方程 $\epsilon_{zz} = S_{13}\sigma_{xx} + S_{23}\sigma_{yy} + S_{33}\sigma_{zz}$ 中解出 $\sigma_{zz}$，并将其代回前两行方程。经过整理，可以得到一个类似各向同性情况的、联系面内应变、面内应力以及[轴向应变](@entry_id:160811) $\epsilon_{zz}$ 的有效二维本构关系 ：
$$
\begin{pmatrix}
\epsilon_{xx} \\
\epsilon_{yy} \\
\gamma_{xy}
\end{pmatrix}
=
\boldsymbol{S}^{\mathrm{gps}}
\begin{pmatrix}
\sigma_{xx} \\
\sigma_{yy} \\
\sigma_{xy}
\end{pmatrix}
+
\boldsymbol{s}\,\epsilon_{zz}
$$
其中，有效[柔度矩阵](@entry_id:185679) $\boldsymbol{S}^{\mathrm{gps}}$ 和耦合向量 $\boldsymbol{s}$ 由原始三维柔度系数 $S_{ij}$ 决定。例如，$\boldsymbol{s}$ 的分量为 $-S_{13}/S_{33}$ 和 $-S_{23}/S_{33}$，这表示[轴向应变](@entry_id:160811) $\epsilon_{zz}$ 会通过材料的泊松效应直接诱导面内[正应变](@entry_id:204633)。更一般地，对于具有更低对称性（如单斜）的材料，通过类似的[降维](@entry_id:142982)过程，可以推导出相应的二维本构律，但可能会出现更复杂的耦合形式（如剪切-拉伸耦合）。

#### 模型的局限性

标准GPS模型的核心假设是 $\gamma_{xz}=\gamma_{yz}=0$。然而，在某些重要问题中，这个假设并不成立。最典型的例子就是**扭转**（Torsion）。一个受扭的非圆[截面](@entry_id:154995)杆件，其[横截面](@entry_id:154995)会发生翘曲，导致 $u_z$ 是 $x, y$ 的[非线性](@entry_id:637147)函数，从而产生非零的横向剪切应变。

我们可以通过一个简单的例子来量化标准GPS模型的局限性。考虑一个半径为 $a$ 的圆柱，同时承受均匀[轴向应变](@entry_id:160811) $\epsilon_0$ 和单位长度扭转角 $\kappa$。其精确的三维解包含由拉伸引起的[正应变](@entry_id:204633)和由扭转引起的剪切应变 $\gamma_{xz}=-\kappa y$ 和 $\gamma_{yz}=\kappa x$。而一个强制要求 $\gamma_{xz}=\gamma_{yz}=0$ 的GPS模型，则会完全忽略与扭转相关的变形和应变能。

定义相对应变能误差 $\eta$ 为GPS模型丢失的应变能占总应变能的比例。通过计算精确解的[应变能](@entry_id:162699)（拉伸部分+扭转部分）和GPS解的应变能（仅拉伸部分），可以导出该误差为 ：
$$
\eta = \frac{ \mathcal{U}_{\text{3D}} - \mathcal{U}_{\text{GPS}} }{ \mathcal{U}_{\text{3D}} } = \frac{a^2 \kappa^2}{a^2 \kappa^2 + 4(1+\nu)\epsilon_0^2}
$$
这个结果清晰地表明：
- 当扭转效应远大于拉伸效应时（$\kappa \gg \epsilon_0$），误差 $\eta$ 趋近于1，说明GPS模型完全失效。
- 当拉伸效应远大于扭转效应时（$\epsilon_0 \gg \kappa$），误差 $\eta$ 趋近于0，说明GPS模型是很好的近似。

这提醒我们，广义[平面应变](@entry_id:167046)是一个强大的工具，但其应用必须基于对其核心假设和物理背景的深刻理解。对于涉及显著扭转或弯曲翘曲的问题，需要采用更高级的、允许横向剪切和翘曲的[梁理论](@entry_id:176426)或三维模型。