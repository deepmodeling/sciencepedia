## 引言
[雷达散射截面](@entry_id:754001)（RCS）是衡量物体在[电磁波](@entry_id:269629)照射下反射能量能力的物理量，是雷达探测、[目标识别](@entry_id:184883)和[隐身技术](@entry_id:264201)领域的核心概念。理解RCS不仅需要掌握其物理本质，还要求能将其应用于解决复杂的工程问题。然而，将深奥的电磁理论与多样化的实际应用场景无缝对接，往往是学习和研究过程中的一个挑战。

本文旨在系统性地构建从理论到实践的知识桥梁。在接下来的内容中，我们将首先在**“原理与机制”**一章中，从麦克斯韦方程出发，深入剖析RCS的数学定义、极化散射特性、[高频近似](@entry_id:750288)方法以及[非互易性](@entry_id:168607)等基本物理原理。随后，**“应用与跨学科[交叉](@entry_id:147634)”**一章将这些理论应用于现实世界，探索RCS在雷达工程、[隐身技术](@entry_id:264201)、地球[遥感](@entry_id:149993)和[目标识别](@entry_id:184883)等领域的具体实践。最后，通过**“动手实践”**部分提供的一系列计算问题，读者将有机会亲手实现关键算法，巩固所学知识，并将其转化为解决实际问题的能力。

## 原理与机制

本章在前一章介绍性概述的基础上，深入探讨[雷达散射截面 (RCS)](@entry_id:754001) 的基本物理原理和核心机制。我们将从其严格的数学定义出发，逐步扩展到描述散射过程复杂性的高级概念，包括极化效应、材料影响、[高频近似](@entry_id:750288)、互易性及其破坏，最后将探讨计算方法中的关键问题以及由非相干过程引起的散射现象。

### [雷达散射截面](@entry_id:754001)的基本定义与公式

从概念上讲，[雷达散射截面 (RCS)](@entry_id:754001) 是衡量目标在被雷达波照射时反射[电磁波](@entry_id:269629)能力的物理量。它被定义为一个等效面积，该面积能够将入射到其上的功率无方向性地（即各向同性地）辐射出去，并在接收机处产生与目标实际散射场相同的[功率密度](@entry_id:194407)。尽管这个定义直观，但一个更严谨的数学表述对于精确分析至关重要。

RCS，记为 $\sigma$，被严格定义为在[远场区](@entry_id:185115)，目标的单位[立体角](@entry_id:154756)散射功率与入射到目标处的[功率密度](@entry_id:194407)之比的 $4\pi$ 倍。用数学语言表达，即：
$$
\sigma = \lim_{R \to \infty} 4\pi R^2 \frac{S_s}{S_i}
$$
其中 $R$ 是目标与观测点之间的距离，$S_i$ 是入射到目标位置的[功率密度](@entry_id:194407)，$S_s$ 是在观测点处测得的散射[功率密度](@entry_id:194407)。

为将此定义转化为一个更实用的公式，我们需分析涉及的[功率密度](@entry_id:194407) 。考虑一个频率为 $\omega$ 的时谐[电磁场](@entry_id:265881)，其时间依赖性为 $e^{-j\omega t}$。

首先，考虑入射场。一个典型的雷达场景涉及一个远离目标的源，因此入射波可以近似为平面波。其[电场](@entry_id:194326)相量形式为 $\mathbf{E}_i(\mathbf{r}) = \mathbf{E}_0 e^{j k \hat{\mathbf{r}}_i \cdot \mathbf{r}}$，其中 $\mathbf{E}_0$ 是恒定的[复振幅](@entry_id:164138)矢量，$\hat{\mathbf{r}}_i$ 是传播方向的单位矢量，$k$ 是[波数](@entry_id:172452)。在无损耗的均匀介质中，相应的[磁场](@entry_id:153296)为 $\mathbf{H}_i = \frac{1}{\eta} \hat{\mathbf{r}}_i \times \mathbf{E}_i$，其中 $\eta$ 是介质的[波阻抗](@entry_id:276571)。入射波的时间平均[功率密度](@entry_id:194407)（坡印亭矢量的大小）为：
$$
S_i = \frac{1}{2} \text{Re} \{ \mathbf{E}_i \times \mathbf{H}_i^* \} = \frac{|\mathbf{E}_0|^2}{2\eta}
$$
这个[功率密度](@entry_id:194407)在空间中是均匀的。

其次，考虑散射场。根据惠更斯原理，散射体可以被看作是二次辐射源。在远离散射体的**[远场区](@entry_id:185115)** (far-field zone)，散射场局部表现为向外传播的[球面波](@entry_id:200471)。其[电场](@entry_id:194326)具有以下渐近形式：
$$
\mathbf{E}_s(\mathbf{r}) \approx \frac{e^{j k R}}{R} \mathbf{F}(\hat{\mathbf{r}})
$$
其中 $\mathbf{r} = R\hat{\mathbf{r}}$ 是观测点的位置矢量，$\mathbf{F}(\hat{\mathbf{r}})$ 是与距离无关的矢量远场方向图。在[远场](@entry_id:269288)，散射[电场](@entry_id:194326) $\mathbf{E}_s$ 和[磁场](@entry_id:153296) $\mathbf{H}_s$ 几乎是横向的，且关系为 $\mathbf{H}_s \approx \frac{1}{\eta} \hat{\mathbf{r}} \times \mathbf{E}_s$。因此，散射[功率密度](@entry_id:194407)为：
$$
S_s \approx \frac{1}{2\eta} |\mathbf{E}_s(\mathbf{r})|^2 = \frac{1}{2\eta R^2} |\mathbf{F}(\hat{\mathbf{r}})|^2
$$

将 $S_i$ 和 $S_s$ 的表达式代入 $\sigma$ 的定义中，我们得到：
$$
\sigma(\hat{\mathbf{r}}, \hat{\mathbf{r}}_i) = \lim_{R \to \infty} 4\pi R^2 \frac{|\mathbf{F}(\hat{\mathbf{r}})|^2 / (2\eta R^2)}{|\mathbf{E}_0|^2 / (2\eta)} = 4\pi \frac{|\mathbf{F}(\hat{\mathbf{r}})|^2}{|\mathbf{E}_0|^2}
$$
这个公式是RCS计算的基石。它将目标的散射特性与[远场](@entry_id:269288)方向图的模平方直接联系起来，并且与观测距离 $R$ 无关。

RCS的定义取决于发射机和接收机的位置。
*   **双基地RCS** (Bistatic RCS)：发射机和接收机位于不同位置，对应于一般的入射方向 $\hat{\mathbf{r}}_i$ 和散射方向 $\hat{\mathbf{r}}$。
*   **单基地RCS** (Monostatic RCS)：发射机和接收机位于同一位置，此时观测方向是入射方向的相反方向，即 $\hat{\mathbf{r}} = -\hat{\mathbf{r}}_i$。这在大多数雷达应用中是标准配置，通常称为**后向散射** (backscattering) RCS。

在数值计算中，例如使用[矩量法](@entry_id:752140) (Method of Moments, MoM) 等技术，我们通常首先计算包围散射体的某个闭合[曲面](@entry_id:267450)上的等效电磁流，然后通过辐射积分计算远场。这个过程称为**近远[场变换](@entry_id:265108)** (Near-to-Far-Field Transformation, NTFF)。数值程序通常输出在有限距离 $R$ 处的[电场](@entry_id:194326) $\mathbf{E}_s(\mathbf{r})$。为了得到与距离无关的RCS，必须对输出进行归一化。从远场表达式可知，[远场](@entry_id:269288)方向图 $\mathbf{F}(\hat{\mathbf{r}})$ 可由数值计算得到的场恢复：$|\mathbf{F}(\hat{\mathbf{r}})| = R |\mathbf{E}_s(\mathbf{r})|$。因此，RCS的计算需要将数值结果乘以 $R$ 来抵消[球面波](@entry_id:200471)的 $1/R$ 幅度衰减 。

### 极化散射与散射矩阵

上述标量定义忽略了一个关键方面：[电磁波](@entry_id:269629)的极化。目标的散射特性不仅取决于其形状和材料，还强烈依赖于入射波的极化状态以及接收天线所选择的极化。为了完整描述目标的散射行为，我们需要引入一个矢量-矩阵框架。

一个线性、无源目标的极化散射特性可以通过一个 $2 \times 2$ 的复数矩阵来描述，称为**极化[散射矩阵](@entry_id:137017)** (Polarization Scattering Matrix) 或**辛克莱矩阵** (Sinclair Matrix)，记为 $\boldsymbol{S}$。该矩阵将入射波的横向[电场](@entry_id:194326)矢量（用[琼斯矢量](@entry_id:176164) $\mathbf{e}_t$ 表示）[线性映射](@entry_id:185132)到散射波的横向[电场](@entry_id:194326)矢量（[琼斯矢量](@entry_id:176164) $\mathbf{e}_s$）：
$$
\mathbf{e}_s = \frac{e^{j k R}}{R} \boldsymbol{S} \mathbf{e}_t
$$
矩阵 $\boldsymbol{S}$ 的元素是在一个正交极化基（例如，水平/垂直基 $\{ \hat{\mathbf{e}}_H, \hat{\mathbf{e}}_V \}$）中定义的：
$$
\boldsymbol{S} = \begin{pmatrix} S_{HH} & S_{HV} \\ S_{VH} & S_{VV} \end{pmatrix}
$$
其中 $S_{HV}$ 表示入射场为[垂直极化](@entry_id:261458) (V-pol) 时，散射场中的水平极化 (H-pol) 分量的[复振幅](@entry_id:164138)。$S_{HH}$ 和 $S_{VV}$ 称为同极化 (co-polarized) 分量，而 $S_{HV}$ 和 $S_{VH}$ 称为[交叉极化](@entry_id:187254) (cross-polarized) 分量。

当考虑极化时，RCS的定义被推广为包含发射和接收天线极化特性的形式。若发射天线的单位[琼斯矢量](@entry_id:176164)为 $\mathbf{e}_t$，接收天线的单位[琼斯矢量](@entry_id:176164)为 $\mathbf{e}_r$，则极化RCS由以下公式给出 ：
$$
\sigma = 4\pi |\mathbf{e}_r^\dagger \boldsymbol{S} \mathbf{e}_t|^2
$$
其中 $\dagger$ 表示[共轭转置](@entry_id:147909)。这个表达式量化了目标将入射极化 $\mathbf{e}_t$ 的[能量转换](@entry_id:165656)并散射到接收极化 $\mathbf{e}_r$ 的能力。

例如，假设一个目标在某后向散射方向上的散射矩阵 $\boldsymbol{S}$ 已知。如果雷达发射右旋圆极化波（$\mathbf{e}_t = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ -j \end{pmatrix}$），并使用一个设计用于接收 $+45^\circ$ 线极化波的天线（$\mathbf{e}_r = \frac{1}{\sqrt{2}} \begin{pmatrix} 1 \\ 1 \end{pmatrix}$），则测得的RCS将通过计算[复标量](@entry_id:272141) $\mathbf{e}_r^\dagger \boldsymbol{S} \mathbf{e}_t$ 并代入上述公式得到。通过改变 $\mathbf{e}_t$ 和 $\mathbf{e}_r$，我们可以全面探测目标的极化响应，这在[目标识别](@entry_id:184883)和分类中至关重要。

### [高频近似](@entry_id:750288)：[物理光学](@entry_id:178058)法

对于电大尺寸物体 (electrically large objects) (尺寸远大于波长的物体)，精确求解麦克斯韦方程的数值方法（如[矩量法](@entry_id:752140)）可能需要巨大的计算资源。在这种情况下，[高频近似](@entry_id:750288)方法提供了一种高效且足够精确的替代方案。**[物理光学](@entry_id:178058)法** (Physical Optics, PO) 是其中最常用的一种。

PO近似的核心思想是，在电大尺寸物体的光滑、被照亮表面上，感应电流可以近似为该点处无限大平坦切面上会产生的电流。对于[理想电导体](@entry_id:753331) (Perfect Electric Conductor, PEC)，这意味着感应[表面电流](@entry_id:261791) $\mathbf{J}_s$ 可以近似为：
$$
\mathbf{J}_{PO}(\mathbf{r}') = 2 \hat{\mathbf{n}} \times \mathbf{H}_{inc}(\mathbf{r}')
$$
其中 $\hat{\mathbf{n}}$ 是表面外法向单位矢量，$\mathbf{H}_{inc}$ 是入射[磁场](@entry_id:153296)。在物体的阴影区域，PO假定感应电流为零。这个近似忽略了边缘绕射和[爬行波](@entry_id:748046)等更复杂的现象，但对于预测主散射瓣的RCS非常有效。

一旦获得了PO电流，就可以通过辐射积分计算[远场](@entry_id:269288)散射场，进而得到RCS。对于一个大的平坦PEC板，这个积分特别容易计算。考虑一个面积为 $A$ 的平坦PEC板，在法向入射（$\theta_i = 0$）情况下，PO电流在整个板上是均匀的。[远场](@entry_id:269288)方向图是板形状的[傅里叶变换](@entry_id:142120)，在后向散射方向上达到峰值。其单基地RCS为 ：
$$
\sigma = \frac{4\pi A^2}{\lambda^2}
$$
其中 $\lambda$ 是波长。这个著名的公式表明，对于法向入射，大平面的RCS与面积的平方成正比，与波长的平方成反比，可以产生非常强的回波。

当入射波以倾斜角度 $\theta_i$照射时，PO积分中会出现一个相位项，导致RCS随角度变化而产生[振荡](@entry_id:267781)。对于一个位于 $z=0$ 平面、$L_x \times L_y$ 的矩形板，其单基地RCS可以表示为 ：
$$
\sigma(\theta_i, \phi_i) = \frac{4\pi A^2}{\lambda^2} \left| \text{sinc} \left( \frac{k L_x}{2} \sin\theta_i \cos\phi_i \right) \text{sinc} \left( \frac{k L_y}{2} \sin\theta_i \sin\phi_i \right) \right|^2 \cos^2\theta_i
$$
其中 [sinc函数](@entry_id:274746)（$\text{sinc}(x) = \sin(x)/x$）的出现是矩形[孔径](@entry_id:172936)[傅里叶变换](@entry_id:142120)的直接结果。这个结果精确地描述了RCS的主瓣和[旁瓣](@entry_id:270334)结构，是[天线理论](@entry_id:266250)和雷达散射分析中的一个经典模型。

### RCS缩减技术：材料与涂层

[物理光学](@entry_id:178058)法不仅为计算RCS提供了工具，也为理解和设计RCS缩减技术（即**[隐身技术](@entry_id:264201)**）奠定了基础。从法向入射的大平面RCS公式 $\sigma \propto A^2/\lambda^2$ 可以看出，缩减RCS的两个基本策略是**整形** (shaping) 和**材料** (materials)。整形旨在避免大的平坦表面正对威胁雷达方向，而是将散射能量反射到其他方向。而材料技术则旨在吸收而非反射入射的[电磁能](@entry_id:264720)量。

**雷达吸波材料** (Radar Absorbent Material, RAM) 的设计是一个核心课题。一个典型的例子是，在PEC表面涂覆一层特殊设计的[电介质](@entry_id:147163)或磁介质材料 。我们可以使用传输线模型来分析这种情况。对于法向入射的平面波，自由空间可被视为一个[特性阻抗](@entry_id:182353)为 $\eta_0$ 的半无限长传输线。厚度为 $d$、[波阻抗](@entry_id:276571)为 $\eta_1$ 的涂层则像一段长度为 $d$ 的传输线，而PEC背衬相当于一个短路端（负载阻抗 $Z_L=0$）。

从空气-涂层界面看进去的输入阻抗 $Z_{in}$ 为：
$$
Z_{in} = j \eta_1 \tan(k_1 d)
$$
其中 $k_1$ 是涂层内的[复波数](@entry_id:274896)。该界面处的反射系数 $\Gamma$ 为：
$$
\Gamma = \frac{Z_{in} - \eta_0}{Z_{in} + \eta_0}
$$
由于平坦表面的RCS正比于 $|\Gamma|^2$，即 $\sigma = \frac{4\pi A^2}{\lambda^2}|\Gamma|^2$，最小化RCS的目标就转化为最小化[反射系数](@entry_id:194350) $\Gamma$。当输入阻抗 $Z_{in}$ 与自由空间[波阻抗](@entry_id:276571) $\eta_0$ 相匹配时，即 $Z_{in} \approx \eta_0$，反射几乎为零。通过精心选择涂层的[复介电常数](@entry_id:160910) $\epsilon_r$、复磁导率 $\mu_r$ 和厚度 $d$，可以在特定频率下实现[阻抗匹配](@entry_id:151450)，使入射波能量最大限度地进入涂层并被其内部损耗（由 $\epsilon_r$ 和 $\mu_r$ 的虚部表示）所吸收，从而显著降低RCS。

### 互易性及其破坏

**[洛伦兹互易定理](@entry_id:187647)** (Lorentz reciprocity theorem) 是电磁学中的一个基本原理。它指出，在由线性、时不变、各向同性的材料组成的系统中，交换源和观测点的位置（并进行适当的方向和极化反转）不会改变测量的传输函数。在散射问题中，这意味着：
1.  对于单基地散射，极化散射矩阵是对称的，即 $S_{HV} = S_{VH}$ 。在数值计算中，这意味着[矩量法](@entry_id:752140)中的[阻抗矩阵](@entry_id:274892)是对称的，即 $Z_{ij} = Z_{ji}$ 。
2.  对于双基地散射，源于方向 $\hat{\mathbf{s}}_i$、散射到方向 $\hat{\mathbf{s}}_s$ 的RCS，等于源于方向 $-\hat{\mathbf{s}}_s$、散射到方向 $-\hat{\mathbf{s}}_i$ 的RCS（假设极化匹配）。

然而，当介质不满足线性、时不变和各向同性（或更准确地说，构成张量是对称的）这些条件时，互易性可能被破坏。

#### 材料引起的[非互易性](@entry_id:168607)

当散射体由**非互易** (non-reciprocal) 材料构成时，互易性会失效。一个典型的例子是处于[静态磁场](@entry_id:195560)偏置下的等离子体或[铁氧体](@entry_id:271668)材料 。在这种**旋磁介质** (gyrotropic media) 中，[带电粒子](@entry_id:160311)的[回旋运动](@entry_id:204632)导致[介电常数](@entry_id:146714) $\overline{\overline{\epsilon}}$ 或磁导率 $\overline{\overline{\mu}}$ 变为张量，并且该张量不是对称的，即 $\overline{\overline{\epsilon}} \neq \overline{\overline{\epsilon}}^T$。这种非对称性直接违反了[洛伦兹互易定理](@entry_id:187647)的前提条件。

其后果是可测量的。例如，[交叉极化](@entry_id:187254)RCS可能不再对称，即 $\sigma_{HV} \neq \sigma_{VH}$。此外，相对于偏置[磁场](@entry_id:153296) $\mathbf{B}_0$ 的方向，散射可能会表现出[前后不对称性](@entry_id:159567)，例如 $\sigma(\theta) \neq \sigma(\pi-\theta)$。对不[同手性](@entry_id:171537)的圆极化波（左旋与右旋）的响应也会不同，尤其是在电子[回旋共振](@entry_id:139685)频率附近。

#### 运动引起的[非互易性](@entry_id:168607)

即使散射体本身是互易的，它的运动也会导致在[实验室坐标系](@entry_id:166991)中观察到非互易散射现象 。这是[狭义相对论](@entry_id:275552)的一个有趣推论。考虑一个在自身静止[坐标系](@entry_id:156346)中是互易的物体，正以恒定速度 $\mathbf{v}$ 运动。

根据电磁学的[洛伦兹协变性](@entry_id:161987)，[实验室坐标系](@entry_id:166991)中测得的RCS $\sigma$与物体静止[坐标系](@entry_id:156346)中的RCS $\sigma_0$ 之间的关系可以通过相对论[多普勒因子](@entry_id:272525)来联系。其变换关系为：
$$
\sigma(\hat{\mathbf{s}}_s, \hat{\mathbf{s}}_i, \omega) = \left( \frac{D(\hat{\mathbf{s}}_s)}{D(\hat{\mathbf{s}}_i)} \right)^2 \sigma_0(\hat{\mathbf{s}}_s', \hat{\mathbf{s}}_i', \omega')
$$
其中 $D(\hat{\mathbf{n}}) = \gamma(1 - \boldsymbol{\beta} \cdot \hat{\mathbf{n}})$ 是[多普勒因子](@entry_id:272525)，$\gamma = 1/\sqrt{1-\beta^2}$，$\boldsymbol{\beta} = \mathbf{v}/c$。带撇的量（$\hat{\mathbf{s}}_s', \hat{\mathbf{s}}_i', \omega'$）是在物体静止[坐标系](@entry_id:156346)中经过[相对论光行差](@entry_id:161160)和[多普勒频移](@entry_id:158041)效应修正后的对应量。

由于[多普勒因子](@entry_id:272525) $D(\hat{\mathbf{n}})$ 的存在，以及频率和角度的变换，交换源和接收器的角色会导致一个完全不同的变换因子。因此，即使 $\sigma_0$ 是互易的，实验室坐标系中的 $\sigma$ 通常也是非互易的。这种效应在分析高速目标（如卫星或导弹）的雷达特征时必须加以考虑。

### RCS计算与现象学中的高级专题

#### [计算电磁学](@entry_id:265339)中的[内共振](@entry_id:750753)问题

表面[积分方程](@entry_id:138643) (Surface Integral Equations, SIE) 结合[矩量法 (MoM)](@entry_id:277025) 是计算RCS的黄金标准。两种最常见的SIE是**[电场积分方程](@entry_id:748872)** (Electric Field Integral Equation, EFIE) 和**[磁场积分方程](@entry_id:751614)** (Magnetic Field Integral Equation, MFIE)。然而，在处理闭合PEC物体时，这两种方程都存在一个严重的缺陷：**[内共振](@entry_id:750753)问题** (internal resonance problem) 。

当计算频率恰好与该物体作为空腔谐振器的某个内部模式的[谐振频率](@entry_id:265742)相匹配时，EFIE（对应于[Dirichlet边界条件](@entry_id:142800)）或MFIE（对应于[Neumann边界条件](@entry_id:142124)）的算子会变得奇[异或](@entry_id:172120)接近奇异。这会导致MoM矩阵的条件数急剧恶化，从而使计算出的[表面电流](@entry_id:261791)和RCS结果产生巨大误差，尽管外部散射问题本身在该频率下是良态的。

幸运的是，理论表明，对于一个闭合腔体，其Dirichlet和Neumann模式的[谐振频率](@entry_id:265742)是[互斥](@entry_id:752349)的。利用这一点，**[组合场积分方程](@entry_id:747497)** (Combined Field Integral Equation, CFIE) 被提出来解决这个问题。CFIE通过将EFIE和MFIE进行线性组合来构建一个新的积分方程：
$$
\alpha \cdot (\text{EFIE}) + (1-\alpha) \cdot j\eta \cdot (\text{MFIE})
$$
其中 $\alpha \in (0,1)$ 是一个组合系数。由于EFIE和MFIE的[零空间](@entry_id:171336)是互斥的，CFIE在所有频率下都保证唯一解，从而消除了[内共振](@entry_id:750753)问题，保证了在整个[频谱](@entry_id:265125)范围内计算结果的稳定性和准确性。

#### [非相干散射](@entry_id:190180)I：热辐射贡献

传统的RCS描述的是目标对入射波的**[相干散射](@entry_id:267724)** (coherent scattering)。然而，任何有物理温度（$T > 0$ K）且有损耗的物体都会由于内部[电荷](@entry_id:275494)的随机热运动而发射[电磁辐射](@entry_id:152916)。这种**热辐射** (thermal radiation) 是非相干的，并构成了一个噪声背景，可以被雷达接收机探测到 。

根据涨落-耗散定理和[基尔霍夫热辐射定律](@entry_id:144588)，一个物体的发射能力与其吸收能力直接相关。在无线电频率和通常温度下（即瑞利-金斯极限，$h\nu \ll k_B T$），一个损耗物体发射的总功率与其[吸收截面](@entry_id:172609) $C_{abs}$ 和[绝对温度](@entry_id:144687) $T$ 成正比。

我们可以定义一个“等效”热RCS，记为 $\sigma_T$，它代表一个能够产生与目标热辐射相同接收功率的假想[相干散射](@entry_id:267724)体。推导表明：
$$
\sigma_T = \frac{(4\pi)^2 R^2 k_B T B C_{abs}}{P_t G \lambda^2}
$$
其中 $k_B$ 是[玻尔兹曼常数](@entry_id:142384)，$B$ 是接收机带宽，$P_t$ 是发射功率，$G$ 是[天线增益](@entry_id:270737)。与描述目标固有散射特性的常规RCS不同，$\sigma_T$ 依赖于观测距离 $R$ 和雷达系统参数 ($P_t, G, B$)。它并不是一个目标的内禀属性，而是一个有用的度量，用于量化在雷达链路预算中，目标的热噪声在多大程度上与相干回波信号竞争。

#### [非相干散射](@entry_id:190180)II：部分相干波照明

散射现象的复杂性不仅源于目标本身，也可能源于照明场。经典的RCS理论假设入射波是完全相干的（如理想[平面波](@entry_id:189798)）。然而，在现实世界中，例如当信号穿过[湍流](@entry_id:151300)介质（如大气或[电离层](@entry_id:262069)）后，照明场可能会变成**部分相干** (partially coherent) 的 。

这种场的统计特性由其二阶矩，即**[交叉](@entry_id:147634)谱密度函数** (cross-spectral density) $W(\mathbf{r}_1, \mathbf{r}_2)$ 来描述。它可以分解为由平均场产生的相干[部分和](@entry_id:162077)由场涨落产生的非相干部分。

当一个部分相干场照射目标时，总的散射功率也相应地分为两部分：
1.  **[相干散射](@entry_id:267724)**：由入射场的平均（相干）分量散射产生，其行为类似于传统RCS。
2.  **[非相干散射](@entry_id:190180)**：由入射场的涨落（非相干）分量散射产生。

总的平均RCS是这两部分贡献之和。其表达式涉及对目标[响应函数](@entry_id:142629)与场的相干核（描述涨落的[空间相关性](@entry_id:203497)）进行卷积。最终的RCS不仅是目标几何和材料的函数，还是入射场统计特性（如相干分数 $c$ 和相干长度 $\delta$）的函数。例如，一个完全非相干的入射场 ($c=0$) 产生的散射完全是非相干的，其[角分布](@entry_id:193827)将比[相干散射](@entry_id:267724)更平滑，因为它是由目标上每个点独立散射的贡献叠加而成。这一领域的研究将经典雷达理论与统计光学联系起来，对于通过[复杂介质](@entry_id:164088)进行[遥感](@entry_id:149993)和成像至关重要。