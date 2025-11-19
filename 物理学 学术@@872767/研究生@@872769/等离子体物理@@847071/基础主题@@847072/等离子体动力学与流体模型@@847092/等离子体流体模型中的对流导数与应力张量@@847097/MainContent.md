## 引言
动量守恒方程是等离子体物理学的基石，它描述了各种力如何决定[等离子体流体](@entry_id:187430)的运动。在该方程中，两个概念具有至关重要的物理意义：[对流导数](@entry_id:262900)与应力张量。[对流导数](@entry_id:262900)捕捉了流体自身的惯性，这是一个微妙而强大的效应；而[应力张量](@entry_id:148973)则为所有内力（从简单的压力到复杂的粘性和[湍流](@entry_id:151300)效应）提供了一种系统的描述语言。尽管这些术语是[流体动力学](@entry_id:136788)的标准内容，但它们在等离子体所处的各种极端环境——从磁化实验室装置到[湍流](@entry_id:151300)天体物理[吸积盘](@entry_id:159973)——中的全部内涵并非总是显而易见。本文旨在弥合这一差距，为研究生水平的读者提供一次深入的探索，将这些概念的基本原理与其在真实世界中的应用联系起来。

在“原理与机制”一章中，我们将剖析[对流导数](@entry_id:262900)和各种应力张量模型的数学形式与物理意义。随后，“应用与[交叉](@entry_id:147634)学科联系”一章将展示如何运用这些概念来解决[磁流体动力学稳定性](@entry_id:204501)、[粘性加热](@entry_id:161646)、[湍流输运](@entry_id:150198)甚至相对论背景下的问题。最后，“动手实践”部分将提供具体的练习，以巩固您对这些关键理论工具的理解。

## 原理与机制

在等离子体的流体描述中，[动量守恒](@entry_id:149964)方程是核心。它刻画了作用在等离子体微元上的各种力如何改变其运动状态。本章旨在深入剖析该方程中的两个关键概念：[对流导数](@entry_id:262900)和[应力张量](@entry_id:148973)。[对流导数](@entry_id:262900)描述了流体自身的惯性效应，而[应力张量](@entry_id:148973)则系统地概括了流体内部的[接触力](@entry_id:165079)，包括[各向同性压力](@entry_id:269937)和更复杂的粘性力。理解这些原理与机制对于掌握从实验室等离子体中的[动量输运](@entry_id:139628)到天体物理现象（如[恒星风](@entry_id:161386)和吸积盘）中的[湍流](@entry_id:151300)与不稳定性等众多课题至关重要。

### [对流导数](@entry_id:262900)：流体惯性的表述

在[流体动力学](@entry_id:136788)中，我们通常采用两种视角来描述物理量的变化：[拉格朗日视角](@entry_id:265471)和[欧拉视角](@entry_id:265288)。[拉格朗日视角](@entry_id:265471)跟随一个特定的流体微元，观察其物理量随时间的变化，记为 $\frac{D}{Dt}$。[欧拉视角](@entry_id:265288)则是在空间中的一个[固定点](@entry_id:156394)上，观察流过该点的不同流体微元的物理量变化，记为 $\frac{\partial}{\partial t}$。

一个流体微元的速度 $\mathbf{v}$ 是其空间位置 $\mathbf{r}$ 和时间 $t$ 的函数，即 $\mathbf{v}(\mathbf{r}, t)$。根据链式法则，一个跟随[流体运动](@entry_id:182721)的微元，其速度随时间的[全导数](@entry_id:137587)（或称物质导数、[随体导数](@entry_id:204621)）为：
$$
\frac{D\mathbf{v}}{Dt} = \frac{\partial \mathbf{v}}{\partial t} + \frac{dx}{dt}\frac{\partial \mathbf{v}}{\partial x} + \frac{dy}{dt}\frac{\partial \mathbf{v}}{\partial y} + \frac{dz}{dt}\frac{\partial \mathbf{v}}{\partial z}
$$
由于流体微元的速度就是 $\mathbf{v} = (\frac{dx}{dt}, \frac{dy}{dt}, \frac{dz}{dt})$，上式可以紧凑地写成：
$$
\frac{D\mathbf{v}}{Dt} = \frac{\partial \mathbf{v}}{\partial t} + (\mathbf{v} \cdot \nabla)\mathbf{v}
$$
这就是流体加速度的完整表达式。其中，$\frac{\partial \mathbf{v}}{\partial t}$ 是[局部加速度](@entry_id:272847)，表示在空间[固定点](@entry_id:156394)上[速度场](@entry_id:271461)随时间的变化。而第二项，**[对流导数](@entry_id:262900)** $(\mathbf{v} \cdot \nabla)\mathbf{v}$，则描述了由于流体微元从一个位置移动到另一个具有不同速度的位置而产生的加速度。即使流场是定常的（即 $\frac{\partial \mathbf{v}}{\partial t} = 0$），只要速度在空间上不均匀，流体微元依然会经历加速或减速。因此，$\rho(\mathbf{v} \cdot \nabla)\mathbf{v}$ 项在动量方程中代表了单位体积的**惯性力**。

[对流导数](@entry_id:262900)的物理意义在[曲线坐标系](@entry_id:172561)中尤为明显。例如，在[托卡马克](@entry_id:182005)等离子体的环向旋转中，我们可以使用[柱坐标系](@entry_id:266798) $(R, \phi, z)$ 来近似描述。考虑一个纯环向的定常[旋转流](@entry_id:276737)，其速度剖面为 $\mathbf{v} = v_\phi(R) \mathbf{\hat{e}}_\phi$。在这种情况下，[对流导数](@entry_id:262900) $(\mathbf{v} \cdot \nabla)\mathbf{v}$ 的径向分量变为：
$$
((\mathbf{v} \cdot \nabla)\mathbf{v})_R = -\frac{v_\phi^2(R)}{R}
$$
这恰恰是向心加速度。因此，维持这种[旋转流](@entry_id:276737)所需的径向力平衡中，必须有一个向内的力来平衡这个由[对流](@entry_id:141806)产生的离心惯性力 $\rho \frac{v_\phi^2}{R}$。例如，一个具有[高斯剖面](@entry_id:166151)的环向急流 $\mathbf{v} = v_0 \exp\left( - \frac{(R-R_0)^2}{w^2} \right) \mathbf{\hat{e}}_\phi$ 将产生一个径向惯性力密度 $(\rho(\mathbf{v} \cdot \nabla)\mathbf{v})_R = -\rho \frac{v_0^2}{R} \exp\left( - \frac{2(R-R_0)^2}{w^2} \right)$ [@problem_id:336463]。这个力必须由径向的压力梯度或洛伦兹力来平衡，否则等离子体环将会膨胀。

### 应力张量：内部作用力的语言

流体内部的力可分为两类：作用于整个体积的彻[体力](@entry_id:174230)（如重力、电磁力）和作用于微元表面的接触力。**[应力张量](@entry_id:148973)** $\mathbf{P}$ 是描述内部[接触力](@entry_id:165079)的数学工具。它是一个二阶张量，其分量 $P_{ij}$ 表示在 $i$ 方向上通过一个法向为 $j$ 的单位面积的动量通量。作用在单位体积流体上的总[接触力](@entry_id:165079)由应力张量的负散度给出：$\mathbf{F}_{contact} = -\nabla \cdot \mathbf{P}$。

在许多情况下，将应力张量分解为两部分是十分有用的：
$$
\mathbf{P} = p\mathbf{I} + \boldsymbol{\pi}
$$
其中 $p$ 是**标量压力**，$\mathbf{I}$ 是单位张量，而 $\boldsymbol{\pi}$ 是**[粘性应力](@entry_id:261328)张量**。标量压力代表流体的各向同性部分，它在所有方向上施加相同的力，其作用力为 $-\nabla p$。[粘性应力](@entry_id:261328)张量 $\boldsymbol{\pi}$ 则代表了由流体内部[速度梯度](@entry_id:261686)引起的[动量输运](@entry_id:139628)，它描述了流体的剪切和拉伸/压缩效应。通常定义 $\boldsymbol{\pi}$ 为无迹的（$\text{Tr}(\boldsymbol{\pi}) = 0$），这意味着它的贡献已经从标量压力中分离出来。

### 牛顿流体中的[粘性应力](@entry_id:261328)

粘性是流体抵抗形变的性质，其根源在于[速度梯度](@entry_id:261686)的存在。为了理解[粘性应力](@entry_id:261328)，我们首先需要量化流体的形变。这可以通过考察[速度梯度张量](@entry_id:270928) $\nabla \mathbf{v}$ 来实现，其分量为 $(\nabla \mathbf{v})_{ij} = \frac{\partial v_i}{\partial x_j}$。这个张量可以分解为一个对称部分和一个反对称部分：
$$
\frac{\partial v_i}{\partial x_j} = \frac{1}{2}\left(\frac{\partial v_i}{\partial x_j} + \frac{\partial v_j}{\partial x_i}\right) + \frac{1}{2}\left(\frac{\partial v_i}{\partial x_j} - \frac{\partial v_j}{\partial x_i}\right)
$$
对称部分，即**[应变率张量](@entry_id:266108)** $\mathbf{W}$，其分量为 $W_{ij} = \frac{1}{2}(\partial_j v_i + \partial_i v_j)$，描述了流体微元的形变速率（拉伸和剪切）。反对称部分则与流体的旋转（涡度 $\boldsymbol{\omega} = \nabla \times \mathbf{v}$）有关。

流体微元的形变可以通过考察连接两个相邻流体质点的无限小物质[线元](@entry_id:196833) $\delta\mathbf{l}$ 的演化来直观理解。该[线元](@entry_id:196833)长度平方的变化率与[应变率张量](@entry_id:266108)直接相关 [@problem_id:336535]：
$$
\frac{1}{\delta l^2} \frac{d(\delta l^2)}{dt} = 2 n_i n_j \frac{\partial v_i}{\partial x_j} = 2 n_i n_j W_{ij}
$$
其中 $\mathbf{n} = \delta\mathbf{l} / \delta l$ 是线元的单位[方向向量](@entry_id:169562)。这个关系表明，流体微元的拉伸或压缩完全由[应变率张量](@entry_id:266108)决定。

对于**牛顿流体**，[粘性应力](@entry_id:261328)被假定为与[应变率张量](@entry_id:266108)成[线性关系](@entry_id:267880)。对于[不可压缩流体](@entry_id:181066)（$\nabla \cdot \mathbf{v} = 0$），[粘性应力](@entry_id:261328)张量的表达式为：
$$
\boldsymbol{\pi} = \eta (\nabla \mathbf{v} + (\nabla \mathbf{v})^T) = 2\eta \mathbf{W}
$$
其中 $\eta$ 是**[动力粘度](@entry_id:268228)**，它是一个依赖于[流体性质](@entry_id:200256)（如温度和密度）的输运系数。作用在流体上的[粘性力](@entry_id:263294)密度为 $\mathbf{F}_{visc} = \nabla \cdot \boldsymbol{\pi}$。

计算特定流场中的[粘性应力](@entry_id:261328)分量是理解其作用的关键一步。例如，在一个球坐标系 $(r, \theta, \phi)$ 下，考虑一个不可压缩的轴对称极向流，其速度分量为 $v_r = \frac{2K_0 \cos{\theta}}{r^3}$ 和 $v_\theta = \frac{K_0 \sin{\theta}}{r^3}$。我们可以利用球坐标系下[速度梯度张量](@entry_id:270928)的表达式来计算非对角[粘性应力](@entry_id:261328)分量 $\pi_{r\theta}$。根据定义 $\pi_{r\theta} = \eta((\nabla \mathbf{v})_{r\theta} + (\nabla \mathbf{v})_{\theta r})$，通过细致的计算，可以得到 $\pi_{r\theta} = -\frac{6\eta K_0\sin\theta}{r^4}$ [@problem_id:336396]。这个结果表明，在赤道平面（$\theta = \pi/2$）附近，存在显著的径向动量的极向输运，这种输运是由流场的剪切造成的。

粘性力的另一个重要作用是耗散涡旋。涡度 $\boldsymbol{\omega} = \nabla \times \mathbf{v}$ 描述了流体的局部旋转。通过对[粘性力](@entry_id:263294) $\mathbf{F}_{visc}$ 取旋度，可以得到其对涡度[演化方程](@entry_id:268137)的贡献。对于一个具有恒定粘度 $\eta$ 的不可压缩[牛顿流体](@entry_id:263796)，我们有 $\mathbf{F}_{visc} = \eta \nabla^2 \mathbf{v}$。因此，粘性力对涡度演化的贡献是：
$$
\nabla \times \mathbf{F}_{visc} = \nabla \times (\eta \nabla^2 \mathbf{v}) = \eta \nabla^2 (\nabla \times \mathbf{v}) = \eta \nabla^2 \boldsymbol{\omega}
$$
[@problem_id:336470]。这个结果表明[粘性力](@entry_id:263294)倾向于使涡度场变得平滑，即它扮演了一个**[扩散](@entry_id:141445)项**的角色，将涡度从高浓度区域输运到低浓度区域，最终导致涡旋能量的耗散。

### [动量平衡](@entry_id:193575)：惯性、压力与粘性的相互作用

在许[多物理场](@entry_id:164478)景中，等离子体的[稳态](@entry_id:182458)行为是由[惯性力](@entry_id:169104)、[压力梯度力](@entry_id:262279)和粘性力之间的精细平衡决定的。完整的[稳态](@entry_id:182458)动量方程（忽略彻[体力](@entry_id:174230)）为：
$$
\rho (\mathbf{v} \cdot \nabla)\mathbf{v} = -\nabla p + \nabla \cdot \boldsymbol{\pi}
$$
这个方程揭示了流体内部力的复杂相互作用。

考虑一个特殊的[势流](@entry_id:159985)，其[速度场](@entry_id:271461)由[势函数](@entry_id:176105) $\phi(x, y) = A x y + B(x^2 - y^2)$ 给出。该流场是不可压缩的。如果假设压力梯度为零，那么流体的惯性必须完全由[粘性力](@entry_id:263294)来平衡 [@problem_id:336369]。通过计算[对流导数](@entry_id:262900)项，我们发现 $\rho(\mathbf{v} \cdot \nabla)\mathbf{v} = \rho(A^2+4B^2)(x\hat{\mathbf{x}} + y\hat{\mathbf{y}})$。这意味着要维持这样一个向外辐射的惯性流，必须有一个向内的粘性力 $\mathbf{F}_{visc} = \nabla \cdot \boldsymbol{\pi} = -\rho(A^2+4B^2)(x\hat{\mathbf{x}} + y\hat{\mathbf{y}})$。这直观地展示了粘性力如何作为一种“拉力”来维持特定的流场结构。

一个更普遍的例子是[一维可压缩流](@entry_id:276373)动 [@problem_id:336392]。考虑一个沿x轴的[稳态流](@entry_id:275664)，其速度 $v_x(x)$、密度 $\rho(x)$ 和压力 $p(x)$ 都在变化。此时，一维[动量方程](@entry_id:197225)为：
$$
\rho v_x \frac{d v_x}{d x} = -\frac{d p}{d x} + \frac{d \pi_{xx}}{d x}
$$
左边是[惯性力](@entry_id:169104)，右边是[压力梯度力](@entry_id:262279)和[粘性力](@entry_id:263294)。如果给定速度剖面（例如，指数增长 $v_x(x) = v_0 \exp(x/L)$）和压力剖面（例如，指数衰减 $p(x) = p_0 \exp(-x/L_p)$），并利用[连续性方程](@entry_id:195013) $\rho v_x = \text{const}$，我们就可以精确地求解出维持这种流动所必需的[粘性应力](@entry_id:261328)梯度 $\frac{d \pi_{xx}}{d x}$。这个例子清晰地表明，粘性力是动量方程中一个独立的“旋钮”，它可以被调整以平衡其他力，从而实现各种复杂的[稳态流](@entry_id:275664)动剖面。

### 粘性的动力学起源

流体模型中的粘度是一个唯象参数。要理解其物理根源，我们必须深入到描述[粒子分布函数](@entry_id:753202) $f(\mathbf{r}, \mathbf{v}, t)$ 的[动力学理论](@entry_id:136901)。粘性本质上是粒子通过无规热运动和碰撞，在流体不同层之间传递动量的宏观表现。

我们可以使用简化的**Vlasov-BGK方程**来阐明这一点 [@problem_id:336375]。该方程描述了分布函数 $f$ 在外力、空间梯度以及与一个局部麦克斯韦[分布](@entry_id:182848) $f_M$ 的[碰撞弛豫](@entry_id:160961)（频率为 $\nu$）下的演化：
$$
\frac{Df}{Dt} = -\nu (f - f_M)
$$
考虑一个具有线性剪切流 $\mathbf{u} = A y \hat{\mathbf{x}}$ 的均匀等离子体。在这个流场中，不同 $y$ 位置的流体具有不同的 $x$ 方向平均速度。由于粒子的热运动，一个从 $y$ 处移动到 $y+\delta y$ 处的粒子会携带其在 $y$ 处的平均 $x$ 方向动量。同样，从 $y+\delta y$ 移动到 $y$ 处的粒子也会携带其源位置的动量。这种动量交换导致了 $x$ 方向动量在 $y$ 方向上的净输运。

在[稳态](@entry_id:182458)下，分布函数 $f$ 会偏离局部麦克斯韦[分布](@entry_id:182848) $f_M$。这个偏差 $\delta f = f - f_M$ 可以通过Vlasov-BGK方程近似求得，结果为 $\delta f \approx -\frac{1}{\nu} (\mathbf{v} \cdot \nabla) f_M$。对于剪切流，这导致 $\delta f$ 与[速度梯度](@entry_id:261686) $A$ 成正比。

[粘性应力](@entry_id:261328)张量的非对角分量 $\pi_{xy}$ 正是 $x$ 方向动量在 $y$ 方向的通量，定义为 $P_{xy} = m \int (v_x - u_x)(v_y - u_y) f \, d^3v$。通过将 $\delta f$ 代入积分，经过细致的计算可以得到：
$$
\pi_{xy} = - \frac{n k_B T}{\nu} A
$$
这里 $p=nk_BT$ 是标量压力。这个结果与[牛顿流体](@entry_id:263796)的唯象关系 $\pi_{xy} = \eta (\partial_y v_x + \partial_x v_y) = \eta A$ 相比较，我们得到了粘度系数的动力学表达式：
$$
\eta \approx \frac{p}{\nu}
$$
这个重要的关系式将宏观输运系数（粘度 $\eta$）与等离子体的微观参数（压力 $p$ 和碰撞频率 $\nu$）联系起来，深刻揭示了粘性来源于碰撞过程对动量各向异性的弛豫。

### 等离子体中的高级应力张量模型

对于处于强[磁场](@entry_id:153296)、高温或[湍流](@entry_id:151300)状态的等离子体，简单的各向同性牛顿粘性模型已不再适用。需要更复杂的应力张量模型来描述其独特的物理行为。

#### [磁化等离子体](@entry_id:201225)中的各向异性粘性

在强[磁场](@entry_id:153296)中，[带电粒子](@entry_id:160311)围绕磁力线做快速的[回旋运动](@entry_id:204632)，但在垂直于[磁场](@entry_id:153296)的方向上运动受限。这导致[动量输运](@entry_id:139628)具有强烈的各向异性。S.I. Braginskii 通过求解动力学方程，系统地导出了强磁化、高[碰撞频率](@entry_id:138992)等离子体的粘性张量。这个张量非常复杂，但其核心思想是，平行于[磁场](@entry_id:153296)的[动量输运](@entry_id:139628)与垂直于[磁场](@entry_id:153296)的[动量输运](@entry_id:139628)由不同的粘度系数描述。

以一个沿 $\hat{\mathbf{z}}$ 方向的强[磁场](@entry_id:153296) $\mathbf{B}$ 和一个[剪切流](@entry_id:266817) $\mathbf{u} = u_x(y) \hat{\mathbf{x}}$ 为例，我们来探讨垂直粘性的起源 [@problem_id:336412]。通过在小[碰撞频率](@entry_id:138992)与[回旋频率](@entry_id:156231)之比 $\nu_{ii}/\Omega_i$ 的量级上对[动力学方程](@entry_id:751029)进行[微扰展开](@entry_id:159275)，可以求解出[分布函数](@entry_id:145626)的修正项。零阶修正（忽略碰撞）给出了无耗散的**回旋粘性**（gyroviscosity），它与流体的加速有关，而不是能量耗散。[一阶修正](@entry_id:155896)项则包含了碰撞效应，给出了耗散粘性。

通过这个过程，可以导出剪切[粘性应力](@entry_id:261328) $\pi_{xy}$，并由此得到所谓的**Braginskii粘度系数** $\eta_1$：
$$
\eta_1 \approx \frac{n_i k_B T_i \nu_{ii}}{\Omega_i^2}
$$
其中 $\Omega_i = eB/m_i$ 是离子[回旋频率](@entry_id:156231)。这个结果的物理意义非常清晰：垂直于[磁场](@entry_id:153296)的粘性正比于[碰撞频率](@entry_id:138992) $\nu_{ii}$（因为碰撞是动量跨磁力线输运的媒介），并且反比于[磁场强度](@entry_id:197932)的平方（$\propto 1/B^2$），因为强[磁场](@entry_id:153296)极大地抑制了跨场输运。

#### [无碰撞等离子体](@entry_id:191924)中的CGL[压力张量](@entry_id:147910)

在许多天体物理和聚变等离子体中，碰撞非常稀少，以至于在感兴趣的时间尺度上，平行和垂直于[磁场](@entry_id:153296)方向的粒子能量[分布](@entry_id:182848)可以独立演化。这导致了**压力各向异性**，即平行压力 $p_\|$ 不等于垂直压力 $p_\perp$。

在这种情况下，Chew, Goldberger, 和 Low (CGL) 提出了一个适用于无碰撞[磁化等离子体](@entry_id:201225)的[压力张量](@entry_id:147910)模型：
$$
\mathbf{P}_{CGL} = p_\perp \mathbf{I} + (p_\| - p_\perp) \hat{\mathbf{b}}\hat{\mathbf{b}}
$$
其中 $\hat{\mathbf{b}} = \mathbf{B}/|\mathbf{B}|$ 是沿[磁场](@entry_id:153296)方向的[单位向量](@entry_id:165907)。这一项 $(p_\| - p_\perp) \hat{\mathbf{b}}\hat{\mathbf{b}}$ 描述了沿磁力线方向的额外压力（或张力）。

CGL[压力张量](@entry_id:147910)可以导致独特的宏观不稳定性。一个经典的例子是**[软管不稳定性](@entry_id:275138)**（firehose instability）[@problem_id:336416]。当平行压力远大于垂直压力时（$p_\| \gg p_\perp$），磁力线就如同被过度加压的消防软管一样，会变得不稳定而发生弯折。动量方程中与[磁场](@entry_id:153296)弯曲相关的恢复力是[磁张力](@entry_id:192593) $\frac{B^2}{\mu_0}$。然而，CGL[压力张量](@entry_id:147910)的各向异性项提供了与[磁张力](@entry_id:192593)相反的效应。[线性稳定性分析](@entry_id:154985)表明，当满足以下条件时，系统变得不稳定：
$$
p_\| - p_\perp > \frac{B^2}{\mu_0}
$$
这个判据说明，如果压力各向异性产生的“反张力”超过了[磁场](@entry_id:153296)自身的张力，磁力线就会失稳。这个例子生动地说明了应力张量的具体形式如何决定等离子体的[宏观稳定性](@entry_id:273181)和动力学行为。

#### [湍流](@entry_id:151300)应力：[雷诺应力](@entry_id:263788)与[麦克斯韦应力](@entry_id:199347)

在[湍流](@entry_id:151300)等离子体中，物理量（如速度 $\mathbf{v}$ 和[磁场](@entry_id:153296) $\mathbf{B}$）可以分解为平均部分 $\langle \cdot \rangle$ 和脉动部分 $\tilde{\cdot}$。将这个分解代入[非线性](@entry_id:637147)的动量方程并取平均，会出现源于脉动量二次相关的项。这些项表现为作用在平均流上的有效力，可以被形式化地写成一个**[湍流](@entry_id:151300)[应力张量](@entry_id:148973)**的散度。

这个总的[湍流](@entry_id:151300)应力 $\mathbf{T}_{turb}$ 包括两部分：
1.  **[雷诺应力](@entry_id:263788)** $\mathbf{R}$，源于速度脉动的[非线性](@entry_id:637147)[对流](@entry_id:141806)项：$R_{ij} = -\rho \langle \tilde{v}_i \tilde{v}_j \rangle$。
2.  **[湍流](@entry_id:151300)[麦克斯韦应力](@entry_id:199347)** $\mathbf{M}$，源于[磁场](@entry_id:153296)脉动的洛伦兹力项：$M_{ij} = \frac{1}{\mu_0} \left( \langle \tilde{B}_i \tilde{B}_j \rangle - \frac{1}{2} \langle |\tilde{\mathbf{B}}|^2 \rangle \delta_{ij} \right)$。

因此，作用在平均流上的[湍流](@entry_id:151300)力密度为 $\mathbf{F}_{turb} = \nabla \cdot (\mathbf{R} + \mathbf{M})$。这表明[湍流](@entry_id:151300)脉动可以通过其空间梯度的形式对平均流施加净力，驱动平均流的加速或减速。

考虑一个由两列[反向传播](@entry_id:199535)的阿尔芬波组成的[湍流](@entry_id:151300)场 [@problem_id:336391]。即使平均流为零，如果波的振幅在空间上不均匀（例如，振幅呈[高斯分布](@entry_id:154414) $A(z) = B_S \exp(-z^2 / L^2)$），[湍流](@entry_id:151300)[应力张量](@entry_id:148973)也会随之变化。具体来说，总的[湍流](@entry_id:151300)[应力张量](@entry_id:148973)的 $zz$ 分量 $T_{zz}$ 等于波的磁压 $-\frac{1}{2\mu_0}\langle|\tilde{\mathbf B}|^2\rangle$。因此，[湍流](@entry_id:151300)力在 $z$ 方向上的分量为 $F_{turb, z} = \frac{\partial T_{zz}}{\partial z}$，这对应于波压梯度的负值。这个力可以驱动等离子体产生平均流，这种现象被称为“[声流](@entry_id:187348)”或“波驱动流”，在[等离子体加热](@entry_id:158813)和[动量输运](@entry_id:139628)中扮演着重要角色。