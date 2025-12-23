## 引言
时域有限体积法（Finite-Volume Time-Domain, FVTD）是现代[计算电磁学](@entry_id:265339)中一种功能强大且应用广泛的数值技术。它直接求解[麦克斯韦方程组](@entry_id:150940)的时域形式，能够模拟[电磁波](@entry_id:269629)在复杂几何与材料环境中的传播、散射和相互作用，在[天线设计](@entry_id:746476)、电磁兼容、雷达散射及[光子](@entry_id:145192)学等领域发挥着至关重要的作用。然而，要真正掌握并有效利用FVTD方法，不仅需要理解其基本概念，更需要深入其数值核心，洞悉其如何确保精度、稳定性与物理守恒性。本文旨在填补理论与实践之间的鸿沟，为读者提供一个关于FVTD方法的系统性、深层次的指南。

在接下来的内容中，读者将踏上一段从基础到前沿的探索之旅。第一章“原理与机制”将奠定坚实的理论基础，从麦克斯韦方程的守恒律形式出发，详细拆[解空间](@entry_id:200470)离散、[数值通量](@entry_id:752791)构造、[高阶重构](@entry_id:750332)和[时间积分](@entry_id:267413)等关键步骤。第二章“应用与交叉学科联系”将视野拓宽至实际应用，展示FVTD如何模拟复杂材料、实现[大规模并行计算](@entry_id:268183)，并与伴随方法、不确定性量化等先进分析技术相结合，彰显其跨学科的强大生命力。最后，在“动手实践”部分，通过精选的编程问题，引导读者将理论知识转化为解决实际问题的能力。这趟旅程将使您不仅“知道”FVTD是什么，更“理解”它为何如此强大。

## 原理与机制

本章深入探讨了时域[有限体积法](@entry_id:749372)（Finite-Volume Time-Domain, FVTD）的核心原理与数值机制。我们将从[麦克斯韦方程组的积分形式](@entry_id:264550)出发，构建其作为守恒律的理论基础，进而阐述空间和时间上的[离散化方法](@entry_id:272547)，并讨论如何处理数值稳定性、边界条件和源项等关键问题。

### [麦克斯韦方程组的积分形式](@entry_id:264550)：一种守恒律

时域有限体积法的理论基石是[麦克斯韦方程组的积分形式](@entry_id:264550)。与[微分形式](@entry_id:146747)描述场在空间中某一点的行为不同，积分形式描述了场量在有限大小的区域内的总体行为，这自然地导向了“守恒”的概念。考虑一个固定的、有界的[控制体积](@entry_id:143882) $V$，其边界为 $\partial V$，外法向单位矢量为 $\hat{\mathbf{n}}$。麦克斯韦的四个方程可以写成积分形式。

[法拉第感应定律](@entry_id:146175)和[安培-麦克斯韦定律](@entry_id:266368)是描述场演化的核心方程。对它们在控制体积 $V$ 上进行积分，我们得到：

$$
\int_{V} (\nabla \times \mathbf{E}) \, dV = - \int_{V} \frac{\partial \mathbf{B}}{\partial t} \, dV
$$

$$
\int_{V} (\nabla \times \mathbf{H}) \, dV = \int_{V} \left( \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t} \right) dV
$$

这里，$\mathbf{E}$ 是[电场](@entry_id:194326)强度，$\mathbf{H}$ 是[磁场强度](@entry_id:197932)，$\mathbf{B}$ 是[磁通量密度](@entry_id:194922)，$\mathbf{D}$ 是[电位移场](@entry_id:273493)，而 $\mathbf{J}$ 是电流密度。在FVTD方法中，关键一步是利用矢量微积分的[广义斯托克斯定理](@entry_id:159620)（或称为散度定理的推论），将体积内的旋度积分转化为边界上的[面积分](@entry_id:275394)。该定理指出，对于任意矢量场 $\mathbf{F}$，有 $\int_{V} (\nabla \times \mathbf{F}) dV = \oint_{\partial V} (\hat{\mathbf{n}} \times \mathbf{F}) dS$。

应用此定理，上述两个旋度定律转化为守恒律的形式：

$$
\frac{d}{dt} \int_{V} \mathbf{B} \, dV + \oint_{\partial V} \hat{\mathbf{n}} \times \mathbf{E} \, dS = \mathbf{0}
$$

$$
\frac{d}{dt} \int_{V} \mathbf{D} \, dV - \oint_{\partial V} \hat{\mathbf{n}} \times \mathbf{H} \, dS = - \int_{V} \mathbf{J} \, dV
$$

这种形式清晰地揭示了守恒关系：[控制体积](@entry_id:143882)内[磁通量](@entry_id:268943)（或[电位移](@entry_id:269383)通量）的时间变化率，等于通过其边界的[电场](@entry_id:194326)环流（或[磁场](@entry_id:153296)环流）的通量，再加上体积内的源项（电流）。 在这里，项 $\oint_{\partial V} \hat{\mathbf{n}} \times \mathbf{E} \, dS$ 和 $\oint_{\partial V} \hat{\mathbf{n}} \times \mathbf{H} \, dS$ 被识别为**表面通量**（surface flux），它们代表了控制体积与其邻域的相互作用。而时间导数项则代表了**体积累积**（volume accumulation），$\int_{V} \mathbf{J} \, dV$ 则是**体积源**（volume source）。

另外两个麦克斯韦方程，即[高斯电场定律](@entry_id:146732)和高斯[磁场](@entry_id:153296)定律，则作为系统的**约束**（constraints）：

$$
\oint_{\partial V} \mathbf{D} \cdot \hat{\mathbf{n}} \, dS = \int_{V} \rho \, dV
$$

$$
\oint_{\partial V} \mathbf{B} \cdot \hat{\mathbf{n}} \, dS = 0
$$

这两个定律指出，穿出任一闭合[曲面](@entry_id:267450)的[电位移](@entry_id:269383)通量等于其包裹的净[电荷](@entry_id:275494)，而穿出任一闭合[曲面](@entry_id:267450)的[磁通量](@entry_id:268943)恒为零。这些方程不直接描述场的演化，但必须在数值求解过程中得到满足，以保证解的物理真实性。

### 有限体积离散化：从连续到离散

FVTD方法通过将计算域分割成一系列不重叠的控制体积（或称为**单元**，cells）来实现[空间离散化](@entry_id:172158)。在每个单元 $i$ 内，我们不追踪场在每一点的精确值，而是追踪其**单元平均值**（cell average）。例如，[电位移场](@entry_id:273493)的单元平均值定义为：

$$
\langle \mathbf{D} \rangle_i = \frac{1}{|\mathcal{V}_i|} \int_{\mathcal{V}_i} \mathbf{D} \, dV
$$

其中 $|\mathcal{V}_i|$ 是单元 $i$ 的体积。将守恒律形式的麦克斯韦方程应用于每个单元 $\mathcal{V}_i$，我们得到一个[常微分方程组](@entry_id:266774)（ODEs），即[半离散格式](@entry_id:165671)：

$$
\frac{d}{dt} \langle \mathbf{D} \rangle_i = \frac{1}{|\mathcal{V}_i|} \oint_{\partial \mathcal{V}_i} \hat{\mathbf{n}} \times \mathbf{H} \, dS - \langle \mathbf{J} \rangle_i = -\frac{1}{|\mathcal{V}_i|} \sum_{f \in \partial \mathcal{V}_i} \int_{f} \mathbf{F}_D^* \cdot \hat{\mathbf{n}}_f \, dA - \langle \mathbf{J} \rangle_i
$$

$$
\frac{d}{dt} \langle \mathbf{B} \rangle_i = -\frac{1}{|\mathcal{V}_i|} \oint_{\partial \mathcal{V}_i} \hat{\mathbf{n}} \times \mathbf{E} \, dS = -\frac{1}{|\mathcal{V}_i|} \sum_{f \in \partial \mathcal{V}_i} \int_{f} \mathbf{F}_B^* \cdot \hat{\mathbf{n}}_f \, dA
$$

这里，$\sum_{f \in \partial \mathcal{V}_i}$ 表示对单元 $i$ 所有表面（**面**，faces）求和。关键在于，位于两个单元交界面上的场值（例如 $\mathbf{H}$ 和 $\mathbf{E}$）是未知的，因为我们只存储了单元平均值。因此，必须引入一个**数值通量**（numerical flux）函数，记为 $\mathbf{F}^*$，来近似每个面上的真实物理通量。这个[数值通量](@entry_id:752791)是FVTD方法的核心，它的构造直接决定了数值格式的精度、稳定性和耗散/[色散](@entry_id:263750)特性。

### [黎曼问题](@entry_id:171440)与数值通量

在任意两个相邻单元的交界面上，存在两个不同的单元平均场值，例如左侧的 $\mathbf{U}_L$ 和右侧的 $\mathbf{U}_R$。如何根据这两个值确定一个唯一的、物理上一致的界面通量？这个问题在数学上被称为**[黎曼问题](@entry_id:171440)**（Riemann problem）。现代FVTD方法正是通过求解这个局部的、一维的[黎曼问题](@entry_id:171440)来构造[数值通量](@entry_id:752791)的。

首先，我们将无源、线性的麦克斯韦方程组写成一个一阶[双曲系统](@entry_id:260647)：

$$
\frac{\partial \mathbf{U}}{\partial t} + \nabla \cdot \mathbf{F}(\mathbf{U}) = 0
$$

其中，状态矢量 $\mathbf{U}$ 和通量张量 $\mathbf{F}$ 可以有多种定义。一个常见的选择是 $\mathbf{U} = [\mathbf{E}, \mathbf{H}]^\top$。对于沿法向 $\mathbf{n}$ 的通量，可以定义一个**通量[雅可比矩阵](@entry_id:264467)**（flux Jacobian）$A_n$，使得法向通量为 $\mathbf{F}_n(\mathbf{U}) = A_n \mathbf{U}$。从[麦克斯韦方程组](@entry_id:150940)的旋度定律出发，可以推导出 ：

$$
A_n = \begin{pmatrix} \mathbf{0}  & -\varepsilon^{-1} C(\mathbf{n}) \\ \mu^{-1} C(\mathbf{n}) & \mathbf{0} \end{pmatrix}
$$

这里 $C(\mathbf{n})\mathbf{v} = \mathbf{n} \times \mathbf{v}$ 是叉乘算子。

**[戈杜诺夫通量](@entry_id:634733)**（Godunov flux）是一种基于精确黎曼解的数值通量。它通过求解界面上的[黎曼问题](@entry_id:171440)，得到一个中间的“星状态”（star state）$\mathbf{U}^* = [\mathbf{E}^*, \mathbf{H}^*]^\top$，然后用这个星状态来计算通量 $\mathbf{F}_n^* = \mathbf{F}_n(\mathbf{U}^*)$。对于[电磁波](@entry_id:269629)，这个解依赖于界面两侧介质的**[波阻抗](@entry_id:276571)**（wave impedance）$Z = \sqrt{\mu/\varepsilon}$。

在界面上，场的切向分量 $\mathbf{E}_t$ 和 $\mathbf{H}_t$ 必须连续。通过求解基于特征分析的[黎曼不变量](@entry_id:165930)，可以得到界面上的切向场“星状态”值 $\mathbf{E}_t^*$ 和 $\mathbf{H}_t^*$。例如，对于由状态 $(\mathbf{U}_L, Z_L)$ 和 $(\mathbf{U}_R, Z_R)$ 分隔的界面，$\mathbf{E}_t^*$ 的表达式为  ：

$$
\mathbf{E}_t^* = \frac{Z_R \mathbf{E}_t^{L} + Z_L \mathbf{E}_t^{R} + Z_L Z_R (\mathbf{n} \times \mathbf{H}_t^{L} - \mathbf{n} \times \mathbf{H}_t^{R})}{Z_L + Z_R}
$$

一个类似的表达式可以用于 $\mathbf{n} \times \mathbf{H}_t^*$。这种基于特征的**上风格式**（upwind scheme）能够物理地解释波在不同介质界面上的传播、反射和透射，并自动满足物理**[跳跃条件](@entry_id:750965)**（jump conditions），即在没有表面源的情况下，$\mathbf{E}$ 和 $\mathbf{H}$ 的切向分量是连续的 。

### 实现[高阶精度](@entry_id:750325)：MUSCL重构

直接使用单元平均值来构造黎曼问题的左右状态（即假设单元内场是常数）会得到一个只有一阶空间精度的格式。为了获得更高的精度，必须在每个单元内对场进行**重构**（reconstruction）。

**MUSCL**（Monotonic Upstream-centered Schemes for Conservation Laws）方法是一种实现[高阶精度](@entry_id:750325)的流行策略。其核心思想是在每个单元 $i$ 内，用一个[分段多项式](@entry_id:634113)（通常是线性函数）来近似场的[分布](@entry_id:182848)，而不仅仅是单元平均值 $\mathbf{U}_i$。一个[分段线性](@entry_id:201467)重构具有形式 ：

$$
\mathbf{U}_i(x) = \mathbf{U}_i + \boldsymbol{\sigma}_i (x - x_i)
$$

其中 $x_i$ 是单元中心，$ \boldsymbol{\sigma}_i$ 是单元内的场斜率。这个斜率需要仔细选择。一个简单的选择，如[中心差分](@entry_id:173198)，虽然在光滑区域是[二阶精度](@entry_id:137876)的，但在不连续点或陡峭梯度附近会引发非物理的[振荡](@entry_id:267781)（[吉布斯现象](@entry_id:138701)）。

为了抑制这些[振荡](@entry_id:267781)，MUSCL引入了**[斜率限制器](@entry_id:638003)**（slope limiter）的概念。限制器的作用是“限制”或“修正”计算出的斜率，以确保重构后的场满足**[单调性](@entry_id:143760)**（monotonicity）或**总变差不增**（Total Variation Diminishing, TVD）的性质。这意味着重构过程不会产生新的局部最大值或最小值。

[斜率限制器](@entry_id:638003)通常被构造为一个函数 $\boldsymbol{\phi}(r)$，它作用于连续梯度之比 $r_i = (\mathbf{U}_{i+1} - \mathbf{U}_i) / (\mathbf{U}_i - \mathbf{U}_{i-1})$。这个比率 $r_i$ 衡量了场的局部光滑度。限制器函数 $\boldsymbol{\phi}(r)$ 被设计为 ：
1.  在场的[极值](@entry_id:145933)点附近（$r \le 0$），将斜率设为零（$\phi(r)=0$），局部退化为[一阶精度](@entry_id:749410)以保证稳定性。
2.  在场的光滑区域（$r \approx 1$），$\phi(1)=1$，使得限制后的斜率逼近二阶精度的[中心差分](@entry_id:173198)斜率，从而保证了光滑解的**二阶精度**。
3.  在所有情况下，满足TVD条件，如 $0 \le \phi(r) \le \min(2, 2r)$，以确保重构后的界面值不会超出相邻单元平均值的范围。

通过这种方式，MUSCL方法巧妙地在保持[高阶精度](@entry_id:750325)和抑制[数值振荡](@entry_id:163720)之间取得了平衡。

### [时间积分](@entry_id:267413)与稳定性

通过[空间离散化](@entry_id:172158)，我们得到了一个大型的[常微分方程组](@entry_id:266774)（ODEs），形式为 $\frac{d\mathbf{U}}{dt} = \mathcal{L}(\mathbf{U})$，其中 $\mathcal{L}$ 代表了整个有限体[积空间](@entry_id:151693)算子（包括重构和[数值通量](@entry_id:752791)计算）。下一步是进行时间积分。

#### 显式格式的稳定性：CFL条件

对于[显式时间积分](@entry_id:165797)格式，时间步长 $\Delta t$ 受到稳定性条件的限制。**[Courant-Friedrichs-Lewy (CFL) 条件](@entry_id:747986)**指出，在一步[时间积分](@entry_id:267413)内，数值信息的传播速度必须快于物理信息的传播速度。换言之，数值计算的[依赖域](@entry_id:160270)必须包含物理波的[依赖域](@entry_id:160270)。对于麦克斯韦方程组，物理波速为 $c = 1/\sqrt{\mu\varepsilon}$。对于在 $d$ 维均匀笛卡尔网格（单元尺寸为 $\Delta$）上采用[中心通量](@entry_id:747204)和[蛙跳格式](@entry_id:163462)的FVTD/[FDTD方法](@entry_id:263763)，最严格的[CFL稳定性条件](@entry_id:747253)为 ：

$$
c \Delta t \le \frac{\Delta}{\sqrt{d}}
$$

这个 $1/\sqrt{d}$ 因子源于多维耦合。在多维空间中，最不稳定的数值模式是沿网格对角线传播的[平面波](@entry_id:189798)，其数值[波速](@entry_id:186208)高于沿坐标轴传播的波。这种效应体现在离散[旋度算子](@entry_id:184984)谱半径的增大上，它要求比一维情况（$d=1$）更小的时间步长。

#### [高阶时间积分](@entry_id:750308)：SSP-RK方法

为了匹配MUSCL等高阶空间格式，[时间积分](@entry_id:267413)也需要是高阶的。然而，许多[高阶时间积分](@entry_id:750308)方法（如标准[龙格-库塔法](@entry_id:140014)）可能会破坏由[斜率限制器](@entry_id:638003)保证的TVD性质。**强稳定性保持（Strong-Stability-Preserving, SSP）龙格-库塔**方法被设计用来解决这个问题。

SSP-RK方法的核心思想是将其表示为一系列**前向欧拉步**的**[凸组合](@entry_id:635830)**（convex combination）。由于[前向欧拉法](@entry_id:141238)在满足[CFL条件](@entry_id:178032)下是保持单调性的，那么由其[凸组合](@entry_id:635830)构成的[高阶方法](@entry_id:165413)也能在相同的（或略微缩减的）[时间步长限制](@entry_id:756010)下保持这一良好性质。常用的二阶和三阶SSP-RK格式（SSP-RK2 和 SSP-RK3）的SSP系数均为1，意味着它们与[前向欧拉法](@entry_id:141238)享有相同的稳定性区域，即 $\Delta t \le \Delta t_{\mathrm{FE}}$。

例如，一个二阶SSP-RK格式（Heun法）的阶段形式可以写成：
$$
\mathbf{U}^{(1)} = \mathbf{U}^n + \Delta t\,\mathcal{L}(\mathbf{U}^n)
$$
$$
\mathbf{U}^{n+1} = \frac{1}{2}\,\mathbf{U}^n + \frac{1}{2}\left(\mathbf{U}^{(1)} + \Delta t\,\mathcal{L}(\mathbf{U}^{(1)})\right)
$$
这个形式清楚地显示了它是由多个前向欧拉步和凸组合构成的。

#### 刚性[源项](@entry_id:269111)的处理

当介质具有[导电性](@entry_id:137481)（$\sigma > 0$）时，安培定律中会出现一个欧姆电流项 $\mathbf{J} = \sigma \mathbf{E}$。这在[半离散格式](@entry_id:165671)中表现为一个衰减[源项](@entry_id:269111)：
$$
\epsilon \frac{d \bar{\mathbf{E}}}{d t} = \dots - \sigma \bar{\mathbf{E}}
$$
这个项引入了一个物理[弛豫时间](@entry_id:191572)尺度 $\tau = \epsilon/\sigma$。如果完全采用[显式时间积分](@entry_id:165797)（如[前向欧拉法](@entry_id:141238)），该项会引入一个独立的稳定性约束 ：
$$
\Delta t \le 2\frac{\epsilon}{\sigma} = 2\tau
$$
当介质导电性很强或[介电常数](@entry_id:146714)很低时，$\tau$ 可能远小于[CFL条件](@entry_id:178032)决定的时间步长（$\tau \ll \Delta/c$），导致整个系统变得**刚性**（stiff）。这会迫使我们采用极小的时间步长，严重影响[计算效率](@entry_id:270255)。

为了克服刚性问题，可以采用**半隐式**（semi-implicit）处理。具体来说，只对刚性的[源项](@entry_id:269111) $\sigma\mathbf{E}$ 采用[隐式格式](@entry_id:166484)（如[后向欧拉法](@entry_id:139674)或梯形法则），而空间耦合的通量项仍然显式处理。例如，使用[后向欧拉法](@entry_id:139674)的更新格式为：
$$
\epsilon \frac{\bar{\mathbf{E}}^{n+1} - \bar{\mathbf{E}}^n}{\Delta t} = \mathbf{R}_E(\bar{\mathbf{H}}^n) - \sigma \bar{\mathbf{E}}^{n+1}
$$
这个方程可以方便地对每个单元内的 $\bar{\mathbf{E}}^{n+1}$ 进行局部求解，而无需全局耦合。这种处理方式对于刚性项是无条件稳定的，从而消除了由[电导率](@entry_id:137481)带来的[时间步长限制](@entry_id:756010)，使得全局时间步长仅由[CFL条件](@entry_id:178032)决定。

### 约束与边界条件的应用

一个成功的FVTD模拟器必须精确地施加物理约束和边界条件。

#### 散度约束的保持

[麦克斯韦方程组](@entry_id:150940)包含两个散度约束：$\nabla \cdot \mathbf{B} = 0$ 和 $\nabla \cdot \mathbf{D} = \rho$。[数值误差](@entry_id:635587)可能导致这些约束被违反，产生非物理的“[磁单极子](@entry_id:142817)”或[电荷](@entry_id:275494)。主要有两种策略来处理这个问题。

**1. [约束输运](@entry_id:747775)（Constrained Transport, CT）**：这种方法通过特殊设计的[离散化格式](@entry_id:153074)，从根本上保证散度约束被精确保持（达到机器精度）。对于 $\nabla \cdot \mathbf{B} = 0$，CT方法利用了**交错网格**（staggered grid）的拓扑结构。[磁通量](@entry_id:268943) $\mathbf{B}$ 的分量被存储在单元的面上，而[电场](@entry_id:194326) $\mathbf{E}$ 的分量被存储在单元的边上。法拉第定律的离散形式 $\frac{d\Phi_f^B}{dt} = -\oint_{\partial S_f} \mathbf{E} \cdot d\mathbf{l}$ 意味着面的[磁通量](@entry_id:268943)更新依赖于其边界上边的[环路积分](@entry_id:164828)。当我们计算一个单元所有面流出磁通量的总和（即离散散度）的时间导数时，每个边上的 $\mathbf{E}$ 场贡献会因为方向相反而被精确抵消。因此，如果初始[磁场](@entry_id:153296)的离散散度为零，它将在所有后续时间步中保持为零。 对于 $\nabla \cdot \mathbf{D} = \rho$，要保持此约束，需要确保电流 $\mathbf{J}$ 的离散化与[电荷](@entry_id:275494) $\rho$ 的更新满足离散的[电荷守恒](@entry_id:264158)方程。

**2. [散度清理](@entry_id:748607)（Divergence Cleaning）**：与CT方法不同，[散度清理](@entry_id:748607)方法允许散度误差产生，然后通过附加的步骤来主动地减小或消除这些误差。例如，**[双曲散度清理](@entry_id:750471)**（或GLM方法）会引入一个辅助标量场 $\psi$，并将麦克斯韦方程组修正为包含 $\nabla \psi$ 这样的项。这些新项使得散度误差会像波一样从源头传播出去并被耗散掉。这种方法避免了全局求解（如[泊松方程](@entry_id:143763)），但不能保证散度约束被精确保持。

#### 物理边界条件

在计算域的边界上，必须施加物理边界条件。一种常见且强大的方法是使用**虚拟单元**（ghost cells）。对于一个边界上的单元，我们在其外部虚构一个或多个虚拟单元，并根据边界条件填充这些虚拟单元中的场值。然后，边界上的通量就可以像内部界面一样，通过求解一个包含内部真实单元和外部虚拟单元的黎曼问题来计算。

例如，对于**[理想电导体](@entry_id:753331)（PEC）**边界，物理条件是[切向电场](@entry_id:267195)为零（$\mathbf{n}\times \mathbf{E}=\mathbf{0}$）。为了在数值上实现这一点，我们可以设置虚拟单元中的场，使其模拟一个反射波：[切向电场](@entry_id:267195)分量反向（$\mathbf{E}_t^g = -\mathbf{E}_t^\\ell$），而切向[磁场](@entry_id:153296)分量同向（$\mathbf{H}_t^g = \mathbf{H}_t^\\ell$）。将这些值代入[黎曼求解器](@entry_id:754362)，将自然得到界面上的[切向电场](@entry_id:267195)星状态 $\mathbf{E}_t^* = \mathbf{0}$，从而精确地施加了[PEC边界条件](@entry_id:753304)。 **[理想磁导体](@entry_id:753334)（PMC）**边界（$\mathbf{n}\times \mathbf{H}=\mathbf{0}$）则采用对偶的设置。

#### 自适应网格加密（AMR）

为了高效地模拟包含多尺度特征的问题，可以使用**自适应网格加密（[AMR](@entry_id:204220)）**。在AMR中，计算域的不同部分采用不同分辨率的网格。一个关键的挑战是在粗网格和细网格的交界面上保持物理量的守恒。

由于粗、细网格在交界面上计算的通量不一致，直接耦合会导致守恒律被违反。**通量修正**（flux correction）或**回流**（refluxing）技术被用来解决此问题。其基本步骤如下：
1.  在一个粗网格时间步 $\Delta t_c$ 内，粗网格和细网格（通常需要多个细网格时间步 $\Delta t_f$）都向前演化。
2.  记录下在粗细网格交界面上，粗网格计算出的总积分通量 $\mathcal{F}_c$，以及细网格计算出的总积分通量 $\sum \mathcal{F}_f$。
3.  由于[离散化误差](@entry_id:748522)，这两个通量通常不相等。它们的差值 $\Delta \mathcal{F} = \mathcal{F}_c - \sum \mathcal{F}_f$ 代表了未被守恒的物理量。
4.  将这个差值 $\Delta \mathcal{F}$ 加回到交界面旁的粗网格单元中，从而修正其状态，保证跨越不同网格层级的总通量是守恒的。

通过这种方式，FVTD方法可以在AMR框架下保持其严格的守恒性，这是该方法的一个主要优势。