## 引言
黏性流（Viscometric flows），特别是[简单剪切流](@entry_id:1131665)和[泊肃叶流](@entry_id:276368)，是流[体力](@entry_id:174230)学研究中两个最基础也最重要的模型。它们不仅是理论分析的理想范例，更是理解从工业管道输送、[聚合物加工](@entry_id:161528)到微流控和[生物流](@entry_id:1121604)体等众多实际应用中流体行为的基石。然而，当流体从简单的[牛顿流体](@entry_id:263796)变为复杂的黏弹性流体（如[聚合物溶液](@entry_id:145399)或熔体）时，其行为会变得异常复杂且违反直觉，经典的流[体力](@entry_id:174230)学理论难以完全解释。

本文旨在填补这一认知空白，系统性地阐明黏弹性流体在这些基本流动模式下的独特性质。我们将从最基本的运动学描述出发，逐步揭示黏弹性应力的起源，特别是[正应力差](@entry_id:199507)的产生及其物理意义。读者将通过本文的学习，理解为何黏弹性流体会“爬杆”，以及为何它们在非圆形管道中会产生复杂的二次流。

为实现这一目标，本文将分为三个核心部分。在“原理与机制”一章中，我们将建立描述黏性流的数学框架，对比牛顿流体与以Oldroyd-B等模型为代表的黏弹性流体的应力响应，并阐释关键宏观现象背后的物理机制。接着，在“应用与跨学科关联”一章中，我们将展示这些基本原理如何应用于工程、材料科学和生物医学等多个领域，解决从[管道设计](@entry_id:154419)到疾病诊断的实际问题。最后，通过“动手实践”部分提供的计算问题，读者将有机会亲手应用所学知识，巩固对理论和数值方法的理解。

## 原理与机制

本章旨在深入探讨黏弹性流体在两种典型的黏性流（viscometric flow）——[简单剪切流](@entry_id:1131665)和[泊肃叶流](@entry_id:276368)（Poiseuille flow）——中的基本运动学和应力响应。我们将从连续介质力学的第一性原理出发，系统地建立描述这些流动的数学框架，并逐步揭示黏弹性与纯黏性牛顿流体行为之间的根本差异。通过分析[应力张量](@entry_id:148973)的分量，特别是[正应力差](@entry_id:199507)，我们将阐释如杆爬（Weissenberg）效应和非圆形管道中的二次流等宏观现象的物理机制。最后，我们将引入[无量纲数](@entry_id:260863)来对流动状态进行分类，并探讨流动过程中的瞬态动力学与能量转化。

### 黏性流的运动学描述

流体在流动过程中经历的局部运动，包括变形和旋转，可以由**[速度梯度张量](@entry_id:270928)** $\nabla \boldsymbol{v}$ 精确描述。在[笛卡尔坐标系](@entry_id:169789)中，其分量为 $(\nabla \boldsymbol{v})_{ij} = \partial v_i / \partial x_j$。这个[二阶张量](@entry_id:199780)可以唯一地分解为一个对称部分和一个反对称部分之和：

$\nabla \boldsymbol{v} = \boldsymbol{D} + \boldsymbol{W}$

其中，$\boldsymbol{D}$ 是**变形率张量** (rate-of-deformation tensor)，定义为：

$\boldsymbol{D} = \frac{1}{2} \left( \nabla \boldsymbol{v} + (\nabla \boldsymbol{v})^T \right)$

它描述了流体微元的拉伸和[剪切变形](@entry_id:170920)速率。$\boldsymbol{W}$ 是**[涡量张量](@entry_id:189621)** (vorticity tensor) 或[自旋张量](@entry_id:187346) (spin tensor)，定义为：

$\boldsymbol{W} = \frac{1}{2} \left( \nabla \boldsymbol{v} - (\nabla \boldsymbol{v})^T \right)$

它描述了流体微元的刚性旋转速率。理解这两个张量是分析任何流动的基础。

#### [简单剪切流](@entry_id:1131665)

[简单剪切流](@entry_id:1131665)，或称平面[库埃特流](@entry_id:260750) (planar Couette flow)，是最基本的黏性流之一。考虑流体被限制在两个平行板之间，其中一个板以恒定速度移动。若流动方向为 $x$ 方向，[速度梯度](@entry_id:261686)方向为 $y$ 方向，则其理想速度场可以表示为 $\boldsymbol{v} = (\dot{\gamma} y, 0, 0)$，其中 $\dot{\gamma}$ 是一个常数，称为**剪切率**。

根据定义，我们可以计算出该流动的关键运动学张量 。[速度梯度张量](@entry_id:270928) $\nabla \boldsymbol{v}$ 只有一个非零分量：

$\nabla \boldsymbol{v} = \begin{pmatrix} 0 & \dot{\gamma} & 0 \\ 0 & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$

进而，变形率张量 $\boldsymbol{D}$ 和[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 分别为：

$\boldsymbol{D} = \frac{1}{2} \left( \nabla \boldsymbol{v} + (\nabla \boldsymbol{v})^T \right) = \begin{pmatrix} 0 & \frac{\dot{\gamma}}{2} & 0 \\ \frac{\dot{\gamma}}{2} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$

$\boldsymbol{W} = \frac{1}{2} \left( \nabla \boldsymbol{v} - (\nabla \boldsymbol{v})^T \right) = \begin{pmatrix} 0 & \frac{\dot{\gamma}}{2} & 0 \\ -\frac{\dot{\gamma}}{2} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$

这些结果清晰地表明，[简单剪切流](@entry_id:1131665)是纯[剪切变形](@entry_id:170920)（由 $\boldsymbol{D}$ 的非对角元素表示）和纯旋转（由 $\boldsymbol{W}$ 表示）的等量叠加。流体微元在变形的同时，也以 $\dot{\gamma}/2$ 的[角速率](@entry_id:173628)绕 $z$ 轴旋转。

#### [泊肃叶流](@entry_id:276368)

[泊肃叶流](@entry_id:276368)是另一种典型的黏性流，通常指在管道或通道中由压力梯度驱动的流动。考虑在半径为 $R$ 的圆形管道中充分发展的层流，采用[圆柱坐标系](@entry_id:266798) $(r, \theta, z)$，其中 $z$ 为轴向。速度场是纯轴向的，且仅依赖于径向位置 $r$，即 $\boldsymbol{v} = u(r)\boldsymbol{e}_z$。

在这种情况下，我们需要使用[圆柱坐标系](@entry_id:266798)下的张量运算法则 。[速度梯度张量](@entry_id:270928) $\nabla \boldsymbol{v}$ 同样只有一个非零分量，即 $(\nabla \boldsymbol{v})_{zr} = \frac{du}{dr} = u'(r)$。由此可得变形率张量 $\boldsymbol{D}$ 和[涡量张量](@entry_id:189621) $\boldsymbol{W}$ 的非零分量为：

$D_{rz} = D_{zr} = \frac{1}{2} u'(r)$

$W_{zr} = -W_{rz} = \frac{1}{2} u'(r)$

与[简单剪切流](@entry_id:1131665)类似，管道[泊肃叶流](@entry_id:276368)在其局部也是一种剪切流，流体微元同时经历变形和旋转。然而，与剪切率恒定的[简单剪切流](@entry_id:1131665)不同，这里的剪切率 $u'(r)$ 是径向位置的函数，通常在管道中心为零，在管壁处达到最大值。

### 黏性流中的应力响应

流体的力学行为由其本构关系（constitutive relation）决定，该关系描述了应力如何响应变形或变形历史。

#### [牛顿流体](@entry_id:263796)基准

最简单的流体模型是不可压缩[牛顿流体](@entry_id:263796)，其柯西（Cauchy）[应力张量](@entry_id:148973) $\boldsymbol{\sigma}$ 与变形率张量 $\boldsymbol{D}$ 呈线性关系：

$\boldsymbol{\sigma} = -p\boldsymbol{I} + 2\eta \boldsymbol{D}$

其中 $p$ 是[热力学压力](@entry_id:1133073)，$\boldsymbol{I}$ 是单位张量，$\eta$ 是恒定的剪切黏度。项 $2\eta\boldsymbol{D}$ 被称为[偏应力](@entry_id:163323)或额外[应力张量](@entry_id:148973)，记作 $\boldsymbol{\tau}$。

将此[本构关系](@entry_id:186508)应用于[简单剪切流](@entry_id:1131665) ，并将之前计算得到的 $\boldsymbol{D}$ 代入，我们得到额外应力张量 $\boldsymbol{\tau}$：

$\boldsymbol{\tau} = 2\eta \begin{pmatrix} 0 & \frac{\dot{\gamma}}{2} & 0 \\ \frac{\dot{\gamma}}{2} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix} = \begin{pmatrix} 0 & \eta\dot{\gamma} & 0 \\ \eta\dot{\gamma} & 0 & 0 \\ 0 & 0 & 0 \end{pmatrix}$

总应力张量为 $\boldsymbol{\sigma} = \begin{pmatrix} -p & \eta\dot{\gamma} & 0 \\ \eta\dot{\gamma} & -p & 0 \\ 0 & 0 & -p \end{pmatrix}$。由此可见，剪切应力 $\sigma_{xy} = \eta\dot{\gamma}$，这正是牛顿黏度定律。

至关重要的是，我们引入两个关键的物理量：**第一正应力差** ($N_1$) 和**第二[正应力差](@entry_id:199507)** ($N_2$)，定义为：

$N_1 = \sigma_{xx} - \sigma_{yy}$
$N_2 = \sigma_{yy} - \sigma_{zz}$

对于牛顿流体，由于 $\sigma_{xx} = \sigma_{yy} = \sigma_{zz} = -p$，我们得到一个标志性的结果：

$N_1 = 0 \quad \text{and} \quad N_2 = 0$

这个结果表明，牛顿流体在[剪切流](@entry_id:266817)动中不会在流动方向、速度梯度方向或[涡量](@entry_id:142747)方向上产生额外的拉伸或压缩应力。这是区别黏弹性流体的一个根本特征  。

#### 黏弹性的出现：Oldroyd-B 模型

[聚合物溶液](@entry_id:145399)和熔体等[复杂流体](@entry_id:198415)在流动中同时表现出黏性和弹性，即黏弹性。Oldroyd-B 模型是描述这类流体的经典模型之一。它将总应力视为牛顿溶剂贡献和聚合物贡献之和：$\boldsymbol{\sigma} = -p\boldsymbol{I} + \boldsymbol{\tau}_s + \boldsymbol{\tau}_p$。其中溶剂应力 $\boldsymbol{\tau}_s = 2\eta_s\boldsymbol{D}$，而聚合物应力 $\boldsymbol{\tau}_p$ 由一个[演化方程](@entry_id:268137)描述，该方程考虑了聚合物链的松弛和被流场对流拉伸的历史：

$\boldsymbol{\tau}_p + \lambda \stackrel{\nabla}{\boldsymbol{\tau}}_p = 2\eta_p\boldsymbol{D}$

其中 $\lambda$ 是松弛时间，$\eta_p$ 是聚合物黏度贡献，$\stackrel{\nabla}{\boldsymbol{\tau}}_p$ 是[上随体导数](@entry_id:756365)，它描述了应力张量如何随流体微元一起变形和旋转。

在[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)中，我们可以求解该方程得到聚合物的应力分量 。总的剪切应力为 $\sigma_{xy} = (\eta_s + \eta_p)\dot{\gamma}$，总黏度为 $\eta_s + \eta_p$。然而，正应力差的行为发生了质变：

$N_1 = 2\eta_p\lambda\dot{\gamma}^2$
$N_2 = 0$

与[牛顿流体](@entry_id:263796)不同，Oldroyd-B 流体在剪切中产生了**正的第一[正应力差](@entry_id:199507)** ($N_1>0$)。$N_1$ 的大小与剪切率的平方成正比，并且依赖于流体的弹性（由 $\lambda$ 和 $\eta_p$ 体现）。这表明流体在流动方向（$x$ 方向）上产生了额外的拉伸应力，就好像[流线](@entry_id:266815)是绷紧的橡皮筋一样。

#### 超越简单模型：各向异性与[非线性](@entry_id:637147)效应

Oldroyd-B 模型虽然抓住了黏弹性的核心特征（即 $N_1 > 0$），但其预测 $N_2=0$ 与许多真实聚合物体系的实验观察不符。更先进的模型通过引入更复杂的物理机制来改进预测。

- **[Giesekus 模型](@entry_id:1125643)**：此模型引入了“各向异性拖曳”的概念，即聚合物链在不同方向上受到的流体阻力不同。其[本构方程](@entry_id:138559)中增加了一个[非线性](@entry_id:637147)的 $\boldsymbol{\tau}\cdot\boldsymbol{\tau}$ 项。在[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)中，[Giesekus 模型](@entry_id:1125643)不仅预测 $N_1 > 0$，还预测了一个**非零的、负的第二正应力差**，即 $N_2 < 0$ 。在低剪切率下，其[渐近行为](@entry_id:160836)为 $N_2 \approx -\alpha\eta_p\lambda\dot{\gamma}^2$，其中 $\alpha$ 是各向异性参数。

- **FENE-P 模型**：此模型考虑了聚合物链的[有限可延展性](@entry_id:1124989)（Finitely Extensible Nonlinear Elastic）。虽然它引入了[非线性弹性](@entry_id:185743)，但在[稳态](@entry_id:139253)[简单剪切流](@entry_id:1131665)中，它仍然预测 $N_2 = 0$，与 Oldroyd-B 模型相同 。

对比这些模型可以看出，不同的物理假设（如各向异性拖曳）会导致宏观[流变性](@entry_id:152243)质（如 $N_2$ 的符号和大小）的显著差异。实验上，大多数[聚合物溶液](@entry_id:145399)确实表现出负的 $N_2$，其量值通常小于 $N_1$。

### 黏弹性应力的宏观表现

抽象的[正应力差](@entry_id:199507)是导致一系列奇特且反直觉宏观现象的根本原因。

#### Weissenberg 效应（爬杆效应）

当一根旋转的杆部分[浸入](@entry_id:161534)黏弹性流体中时，流体倾向于沿着杆向上爬升，形成一个凸起的液面，这便是 Weissenberg 效应。其物理机制正是正的第一正应力差 $N_1 > 0$ 。在杆周围的环形[剪切流](@entry_id:266817)中，[流线](@entry_id:266815)是圆形的。正的 $N_1$ 表现为沿流线的拉伸应力，即“环向应力”（hoop stress）。这种[环向应力](@entry_id:190931)像箍一样向内挤压流体，导致杆附近的压力升高。为了平衡这种压力，流体只能沿杆向上运动，对抗重力，直到其自由表面处的压力与大气压相等。纯黏性的[牛顿流体](@entry_id:263796)由于 $N_1=0$，则不会产生这种效应，反而可能因为离心力而在杆附近形成凹陷的液面。

#### 非圆形管道中的[二次流](@entry_id:754609)

在压力驱动的[泊肃叶流](@entry_id:276368)中，黏弹性也会导致惊人的效应。在具有高度对称性的几何结构中，如圆形管道或无限宽的平面通道，流场通常是单向的。尽管黏弹性会产生变化的法向应力梯度（例如，$\partial \tau_{yy}/\partial y \neq 0$），但这些梯度可以被一个相应的压力梯度所平衡，而不会破坏[单向流](@entry_id:262401)动的结构 。

然而，当流道[截面](@entry_id:154995)为非圆形（如正方形或矩形）时，对称性被破坏。主流动（沿管道轴向）产生的[正应力](@entry_id:260622)场在[横截面](@entry_id:154995)上分布不均。特别是，当 $N_2 \neq 0$ 时，应力散度 $\nabla \cdot \boldsymbol{\tau}$ 在[横截面](@entry_id:154995)（cross-stream plane）上的分量通常不再是一个[保守场](@entry_id:137555)（其旋度不为零）。这意味着这个由黏弹性产生的[力场](@entry_id:147325)无法仅由一个压力梯度来平衡（因为[梯度的旋度](@entry_id:274168)恒为零）。为了满足[动量守恒](@entry_id:149964)，流体必须在[横截面](@entry_id:154995)上产生一个**[二次流](@entry_id:754609)**（secondary flow），形成典型的向角落流动的涡旋结构 。这种二次流是纯黏弹性效应，在低雷诺数的牛顿流体中不会出现。

#### [压力驱动流](@entry_id:148814)动的动力学

为了更好地理解驱动力与流动之间的关系，我们回顾[牛顿流体](@entry_id:263796)在两块间距为 $2H$ 的[平行板](@entry_id:269827)间的平面[泊肃叶流](@entry_id:276368) 。从 [Navier-Stokes](@entry_id:276387) 方程出发，在[稳态](@entry_id:139253)、充分发展和忽略惯性的条件下，动量方程简化为压力梯度与剪切应力梯度的平衡：

$\eta \frac{d^2 u}{dy^2} = \frac{dp}{dx}$

其中 $\frac{dp}{dx}$ 是恒定的轴向压力梯度。结合壁面上的[无滑移边界条件](@entry_id:186229) $u(\pm H) = 0$，可以解得抛物线形的速度分布：

$u(y) = \frac{1}{2\eta} \left( \frac{dp}{dx} \right) (y^2 - H^2)$

施加在壁面上的剪切应力 $\tau_w$ 可以通过计算壁面处的[速度梯度](@entry_id:261686)得到：

$\tau_w = \eta \left. \frac{du}{dy} \right|_{y=H} = H \frac{dp}{dx}$

这个经典结果清晰地展示了宏观驱动力（压力梯度）如何通过流体黏性转化为内部应[力场](@entry_id:147325)和速度场。对于黏弹性流体，类似的力平衡依然成立，但应力与[速度梯度](@entry_id:261686)的关系更为复杂，导致非抛物线形的速度分布。

### [无量纲分析](@entry_id:188181)与流动状态

为了对不同流动状态下[惯性力](@entry_id:169104)、黏性力和弹性力的相对重要性进行分类，我们引入一系列[无量纲数](@entry_id:260863)。

- **雷诺数 (Reynolds number, $Re$)**: $Re = \frac{\rho U L}{\eta}$，其中 $\rho$ 是密度，$U$ 和 $L$ 分别是[特征速度](@entry_id:165394)和特征长度。$Re$ 量化了惯性力与黏性力的比值。当 $Re \ll 1$ 时，流动由黏性主导（[斯托克斯流](@entry_id:138636)或蠕动流）；当 $Re \gg 1$ 时，惯性效应显著 。

- **魏森贝格数 (Weissenberg number, $Wi$)**: $Wi = \lambda \dot{\gamma} \sim \frac{\lambda U}{L}$。它比较了流体的松弛时间 $\lambda$ 和流场变形的特征时间 $1/\dot{\gamma}$。$Wi$ 衡量了聚合物链在流动中被拉伸和取向的程度，从而量化了[稳态](@entry_id:139253)[剪切流](@entry_id:266817)中弹性效应的强度。当 $Wi \ll 1$ 时，流体行为接近[牛顿流体](@entry_id:263796)；当 $Wi \ge 1$ 时，[非线性](@entry_id:637147)黏弹性效应（如[正应力差](@entry_id:199507)）变得显著  。

- **[德博拉数](@entry_id:158162) (Deborah number, $De$)**: $De = \frac{\lambda}{T}$，其中 $T$ 是一个外部过程或观察的特征时间。它衡量了流体响应外部变化的“固态”或“液态”程度。如果 $De \gg 1$（松弛时间远长于观察时间），流体表现为弹性固体；如果 $De \ll 1$，流体表现为黏性液体 。在振荡[剪切流](@entry_id:266817)中，若[振荡频率](@entry_id:269468)为 $\omega$，则特征时间 $T=1/\omega$，此时 $De=\lambda\omega$。黏性主导和弹性主导响应的转变就发生在 $De \sim 1$ 附近 。

$Wi$ 和 $De$ 的关系值得注意。在稳态流动中，$T \to \infty$，因此 $De=0$，但 $Wi$ 可以是任意值。在[非稳态流](@entry_id:269993)动中，例如一个启动过程，如果过程时间由运动学本身决定，即 $T \sim L/U$，那么 $De \sim Wi$。此时，两个数描述的是同一物理本质 。

- **[弹性数](@entry_id:263810) (Elasticity number, $El$)**: $El = \frac{Wi}{Re} = \frac{\lambda\eta}{\rho L^2}$。它只依赖于流体物性和几何尺寸，而与流速无关，用于比较流体的弹性趋势与惯性趋势 。

### 瞬态现象：应力过冲与能量储存

黏弹性流体的复杂性在[瞬态流](@entry_id:756109)动中表现得尤为突出。

#### 应力增长与[过冲](@entry_id:147201)

考虑从静止开始的[简单剪切流](@entry_id:1131665)启动过程。当施加一个恒定的剪切率 $\dot{\gamma}_0$ 时，流体中的应力会随时间增长。对于[牛顿流体](@entry_id:263796)，剪切应力会瞬间达到其[稳态](@entry_id:139253)值 $\eta\dot{\gamma}_0$。然而，对于黏弹性流体，在较高的[魏森贝格数](@entry_id:262025)下（$Wi = \lambda\dot{\gamma}_0 \gg 1$），剪切应力（和第一[正应力差](@entry_id:199507)）在达到[稳态](@entry_id:139253)值之前，会经历一个显著的**[过冲](@entry_id:147201)**（overshoot），即瞬态峰值远高于最终的[稳态](@entry_id:139253)值 。

这种[过冲](@entry_id:147201)现象的根源在于弹性能的储存与释放。在流动初期，[聚合物网络](@entry_id:191902)像弹簧一样被拉伸，迅速储存弹性能，导致应力快速上升。随着应变的累积，聚合物链变得高度取向和拉伸，此时流场的对流效应开始起主导作用，促使链发生翻滚或构象重排，从而导致部分[应力松弛](@entry_id:159905)，最终达到一个[动态平衡](@entry_id:136767)的[稳态](@entry_id:139253)。实验和理论均表明，应力峰值通常出现在一个应变（$\gamma = \dot{\gamma}_0 t$）为常数（通常为 2-5）的时刻，而不是一个固定的时间 。

#### 黏弹性流中的能量平衡

我们可以通过能量守恒的视角来更严格地理解弹性效应。[聚合物构象](@entry_id:180389)的改变伴随着弹性能的储存。对于一个由[聚合物构象](@entry_id:180389)张量 $\boldsymbol{C}$ 描述的体系，其单位体积的弹性能密度可以定义为 $W_p(\boldsymbol{C})$。例如，对于 Oldroyd-B 模型底层的 Hookean 哑铃模型，其自由能密度为 $W_p = \frac{G}{2}(\mathrm{tr}\,\boldsymbol{C} - \ln(\det\boldsymbol{C}) - 3)$，其中 $G$ 是[弹性模量](@entry_id:198862) 。

通过对本构方程和自由能表达式的分析，可以推导出聚合物应力所做的功率（单位时间单位体积做的功）$\boldsymbol{\tau}_p : \boldsymbol{D}$ 的分配关系 ：

$\boldsymbol{\tau}_p : \boldsymbol{D} = \frac{dW_p}{dt} + \mathcal{D}_p$

这个[能量平衡方程](@entry_id:191484)表明，外界对[聚合物网络](@entry_id:191902)做的功，一部分以弹性能的形式储存起来（速率为 $\frac{dW_p}{dt}$），另一部分则通过聚合物链在溶剂中的运[动摩擦](@entry_id:177897)而耗散掉（耗散速率为 $\mathcal{D}_p$）。耗散项 $\mathcal{D}_p$ 可以被证明是恒为正的，符合[热力学](@entry_id:172368)第二定律。

在[剪切流](@entry_id:266817)启动过程中，$\frac{dW_p}{dt}$ 在初期为正，表示能量正在被储存，这与应力的快速增长相对应。随着流动趋于[稳态](@entry_id:139253)，$\frac{dW_p}{dt} \to 0$，所有输入的能量都将转化为耗散。这个能量框架为理解应力[过冲](@entry_id:147201)等瞬态现象提供了坚实的[热力学](@entry_id:172368)基础，并揭示了黏弹性流体中变形、应力与能量之间深刻的内在联系。