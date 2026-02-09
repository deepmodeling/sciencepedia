## 引言
电磁-结构耦合是现代工程与科学领域中一个普遍存在且至关重要的多物理场现象，从微观的MEMS谐振器到宏伟的聚变反应堆，其影响无处不在。精确预测和控制由电磁场引起的结构响应，或反之，利用结构形变调控电磁特性，对设备性能、可靠性与创新设计至关重要。然而，要驾驭这一复杂课题，需要跨越电磁学与固体力学的传统界限，建立一个统一的理论与计算框架。本文旨在系统性地解决这一知识鸿沟，为读者提供一个从理论到实践的全面指南。

在接下来的内容中，我们将首先在“原理与机制”一章中，深入剖析耦合现象的物理根源，建立起关于力、动量、能量以及变形介质中电动力学的坚实理论基础。随后，我们将在“应用与跨学科联系”一章中，通过一系列生动的工程实例，展示这些基础理论如何应用于解决从电磁阻尼到腔光力学等前沿问题。最后，通过“动手实践”部分的计算练习，您将有机会亲手实现关键的耦合算法，将理论知识转化为解决实际问题的能力。

## 原理与机制

本章旨在深入探讨电磁-结构耦合现象背后的基本物理原理和核心作用机制。我们将从电磁力、动量和能量的产生与转换出发，建立一个坚实的理论基础。随后，我们将讨论在变形介质中描述电磁现象所需的特殊考虑，包括本构关系和运动学框架。最后，我们将通过具体的材料耦合效应（如压电和磁致伸缩）以及求解这些复杂问题的计算策略，将理论与实践联系起来。

### 力、动量与能量的基本原理

电磁-结构耦合的根源在于电磁场与物质之间的相互作用，这种作用通过力、动量和能量的交换来体现。理解这些基本量的定义和守恒定律是分析所有耦合问题的起点。

#### 宏观介质中的洛伦兹力

作用于物质上的电磁力的最基本描述是**洛伦兹力**。在宏观尺度下，我们需要考虑所有电荷和电流，包括材料内部由电极化和磁化产生的束缚电荷和束缚电流。因此，作用于单位体积介质的**洛伦兹力密度** $\mathbf{f}$ 由作用在总电荷密度 $\rho_{\text{tot}}$ 和总电流密度 $\mathbf{J}_{\text{tot}}$ 上的力构成：

$$
\mathbf{f} = \rho_{\text{tot}}\mathbf{E} + \mathbf{J}_{\text{tot}}\times\mathbf{B}
$$

其中 $\mathbf{E}$ 和 $\mathbf{B}$ 分别是宏观电场和磁感应强度。总电荷密度和总电流密度是自由源与束缚源之和：

$$
\rho_{\text{tot}} = \rho_f + \rho_b = \rho_f - \nabla\cdot\mathbf{P}
$$

$$
\mathbf{J}_{\text{tot}} = \mathbf{J}_f + \mathbf{J}_b = \mathbf{J}_f + \frac{\partial \mathbf{P}}{\partial t} + \nabla\times\mathbf{M}
$$

这里，$\rho_f$ 和 $\mathbf{J}_f$ 是自由电荷密度和自由电流密度。$\mathbf{P}$ 是电极化强度，其散度负值 $-\nabla\cdot\mathbf{P}$ 定义了**束缚电荷密度** $\rho_b$。$\mathbf{M}$ 是磁化强度，其旋度 $\nabla\times\mathbf{M}$ 定义了**束缚电流密度**（安培电流），而电极化强度的时间变化率 $\frac{\partial \mathbf{P}}{\partial t}$ 产生了**极化电流**。

对于一个没有自由电荷和自由电流的介电和磁性体（即 $\rho_f=0, \mathbf{J}_f=\mathbf{0}$），力密度完全来自束缚源。例如，在静磁情况下，力密度简化为 $\mathbf{f} = (\nabla\times\mathbf{M})\times\mathbf{B}$。这个表达式可以通过矢量恒等式和麦克斯韦方程变换为多种等效形式，这些形式虽然在局部力的分布上有所不同，但在对整个物体积分后，会得到相同的合力和合力矩。这种局部力密度的不唯一性是电动力学中一个深刻且持续被探讨的问题。

#### 麦克斯韦应力张量

计算作用在物体上的总电磁力，除了对整个体积积分洛伦兹力密度外，还有一种等效且往往更方便的方法，即使用**麦克斯韦应力张量** $\mathbf{T}_{\text{EM}}$。这个二阶张量描述了电磁场通过空间传递动量的方式。在真空中，其定义为：

$$
\mathbf{T}_{\text{vac}} = \varepsilon_0 \left( \mathbf{E}\mathbf{E} - \frac{1}{2}(\mathbf{E}\cdot\mathbf{E})\mathbf{I} \right) + \frac{1}{\mu_0} \left( \mathbf{B}\mathbf{B} - \frac{1}{2}(\mathbf{B}\cdot\mathbf{B})\mathbf{I} \right)
$$

其中 $\varepsilon_0$ 和 $\mu_0$ 分别是真空介电常数和磁导率，$\mathbf{E}\mathbf{E}$ 是并矢积，$\mathbf{I}$ 是单位张量。

通过麦克斯韦方程和矢量恒等式，可以证明洛伦兹力密度 $\mathbf{f}$ 与麦克斯韦应力张量的散度之间存在以下关系（动量守恒定律的微分形式）：

$$
\mathbf{f} = \nabla \cdot \mathbf{T}_{\text{vac}} - \frac{\partial \mathbf{g}_{\text{field}}}{\partial t}
$$

其中 $\mathbf{g}_{\text{field}} = \varepsilon_0 (\mathbf{E} \times \mathbf{B})$ 是电磁场的动量密度。对上式在一个包含物体的体积 $V$ 内积分，并应用散度定理，可得作用在物体上的总力 $\mathbf{F}$：

$$
\mathbf{F} = \int_V \mathbf{f} \, dV = \oint_S \mathbf{T}_{\text{vac}} \cdot d\mathbf{a} - \frac{d}{dt}\int_V \mathbf{g}_{\text{field}} dV
$$

这里，$S$ 是包围体积 $V$ 的封闭曲面。这个重要的结果表明，作用在物体上的总力等于通过其边界的动量通量（由麦克斯韦应力张量的面积分给出），减去物体内部场动量的时间变化率。

对于结构分析，这意味着有两种等效的方式来施加载荷：
1.  在物体内部施加体积力密度 $\mathbf{f}(\mathbf{r})$。
2.  在物体表面施加面力（牵引力），其密度由 $\mathbf{t} = \mathbf{T}_{\text{vac}} \cdot \mathbf{n}$ 给出（$\mathbf{n}$ 为外法线向量）。

在计算中同时施加体积力和表面力将导致重复计算。对于稳态时谐场，场动量项的时间平均值为零，因此周期平均的合力恰好等于在物体表面外侧计算的周期平均麦克斯韦应力张量的面积分。

#### 介质中的电磁动量：Abraham-Minkowski之争

虽然麦克斯韦应力张量提供了一种计算总力的有效方法，但关于电磁动量在介质中的局部分布，存在一个长达百年的著名争议，即 **Abraham-Minkowski 争议**。这个争议的核心在于如何唯一定义介质中的电磁动量密度。

主要有两种形式：
- **Abraham 动量密度**: $\mathbf{g}_{A} = \dfrac{1}{c^2} \mathbf{E} \times \mathbf{H} = \dfrac{1}{c^2} \mathbf{S}$，其中 $\mathbf{S}$ 是坡印亭矢量。
- **Minkowski 动量密度**: $\mathbf{g}_{M} = \mathbf{D} \times \mathbf{B}$。

对于一个在介质中传播的能量为 $U$ 的光脉冲，其群速度为 $v_g = c/n_g$（$n_g$ 为群折射率），两种形式预测的总场动量不同：
- Abraham 总动量: $p_A = \dfrac{U}{n_g c}$
- Minkowski 总动量: $p_M = \dfrac{n_p^2}{n_g} \dfrac{U}{c}$，其中 $n_p$ 是相折射率。

当光脉冲进出介质块时，这两种不同的场动量预测会导致不同的界面力。根据动量守恒，施加在介质块上的力应等于场动量变化率的负值。
- 根据 **Abraham 形式**，由于在典型介质中 $n_g > 1$，场动量 $p_A$ 小于其在真空中的值 $U/c$。为守恒总动量，介质块在脉冲进入时必须获得一个**向前**的冲量，即受到一个**向前**的推力。
- 根据 **Minkowski 形式**，在正常色散介质中通常有 $n_p^2/n_g > 1$，场动量 $p_M$ 大于其在真空中的值。因此，介质块在脉冲进入时会受到一个**向后**的拉力（反冲力）。

尽管在入口和出口的瞬时力不同，但对于一个无损、无反射的介质块，当光脉冲完全穿过后，两种理论都预测净冲量为零。然而，由于入口和出口的力作用时间不同（由光在介质中的传播延迟决定），介质块会产生一个净位移。这个净位移可以通过能量-动量守恒推导得出，其大小为 $\Delta x = \dfrac{U L}{M c^2} (n_g - 1)$，其中 $L$ 是块的长度，$M$ 是其质量。这个结果不依赖于动量形式的选择，并已在实验中得到验证，从而巧妙地回避了直接判定哪种动量形式“正确”的问题。这个争议提醒我们，将总动量在“场”和“物质”之间进行划分可能不是唯一的，但总系统的守恒律必须得到满足。

#### 能量守恒与耦合功率流

除了力和动量，能量守恒是分析耦合系统的另一个基石。描述电磁能流和转换的定律是**坡印亭定理**。在包含变形介质的广义情况下，能量守恒方程必须包含电磁子系统与机械子系统之间的功率交换项。

对于一个一般性的电磁活跃的连续体，局域电磁能量[平衡方程](@entry_id:172166)可以写作：
$$
\frac{\partial u}{\partial t} + \nabla\cdot\mathbf{S} = - W_{\text{sink}}
$$
其中，$u = \frac{1}{2}(\mathbf{E}\cdot\mathbf{D} + \mathbf{B}\cdot\mathbf{H})$ 是电磁能量密度，$\mathbf{S} = \mathbf{E}\times\mathbf{H}$ 是坡印亭矢量，代表电磁能流密度。右侧的 $W_{\text{sink}}$ 代表从电磁场转移到其他形式能量的功率密度。

在耦合问题中，$W_{\text{sink}}$ 至少包含两部分：
1.  **焦耳热和对自由电荷做的功**: $\mathbf{J}\cdot\mathbf{E}$，这部分功率一部分转化为热量，另一部分通过洛伦兹力做功转化为机械能。
2.  **与变形相关的功率**: 这部分代表了由于材料变形（如压电、磁致伸缩）引起的极化和磁化状态改变所伴随的能量转换。

在一些先进的计算模型中，为了在数值上解耦电磁和结构求解器，会采用一种特定的能量划分方案。例如，可以将总的机械应力功率 $\boldsymbol{\sigma}:\nabla\mathbf{v}$（其中 $\boldsymbol{\sigma}$ 是柯西应力张量，$\nabla\mathbf{v}$ 是速度梯度）视为电磁子系统的一个能量汇。在这种情况下，电磁能量[平衡方程](@entry_id:172166)写作：
$$
\frac{\partial u}{\partial t}+\nabla\cdot\mathbf{S}=-\mathbf{J}\cdot\mathbf{E}-\boldsymbol{\sigma}:\nabla\mathbf{v}
$$
这个方程的右侧两项代表了从电磁场流向外部（焦耳热、机械功）的总功率。这个方程为构建分步求解算法提供了能量守恒的基础。

### 变形介质中的电动力学

当介质本身在运动和变形时，描述电磁现象的方程需要进行修正和恰当的诠释。这涉及到运动介质中的本构关系，以及在不同参考系（如随材料运动的拉格朗日参考系和固定的欧拉参考系）之间转换场量的数学框架。

#### 运动介质中的本构关系与动生电动势

在处理速度远小于光速（$\lVert \mathbf{v} \rVert \ll c$）的运动导体时，一个关键的修正是欧姆定律。在相对于导体静止的参考系（材料参考系）中，欧姆定律通常具有简单的形式 $\mathbf{J}'=\sigma\mathbf{E}'$，其中 $\sigma$ 是电导率。然而，在实验室参考系中观察时，我们需要使用洛伦兹变换来关联两个参考系中的场量。

在一阶近似下（$\lVert \mathbf{v} \rVert / c$），从实验室参考系 $(S)$ 到材料参考系 $(S')$ 的电场变换为：
$$
\mathbf{E}' \approx \mathbf{E} + \mathbf{v} \times \mathbf{B}
$$
这个关系表明，即使在实验室参考系中没有电场，运动的导体也会在其自身参考系中感受到一个有效电场 $\mathbf{E}_{\text{motional}} = \mathbf{v}\times\mathbf{B}$。这被称为**动生电动势** (motional EMF)。

将此变换后的电场代入材料本构关系 $\mathbf{J}' = \sigma \mathbf{E}'$，我们得到在材料参考系中的传导电流。接着，我们需要将这个电流变换回实验室参考系。四维电流密度的洛伦兹变换在一阶近似下给出：
$$
\mathbf{J} \approx \mathbf{J}' + \rho_e' \mathbf{v}
$$
其中 $\rho_e' \approx \rho_e$ 是材料参考系中的净电荷密度。

综合这些关系，我们得到实验室参考系中的总电流密度 $\mathbf{J}$：
$$
\mathbf{J} \approx \sigma(\mathbf{E} + \mathbf{v} \times \mathbf{B}) + \rho_e \mathbf{v}
$$
这个**广义欧姆定律**包含两个截然不同的部分：
1.  **传导电流** $\mathbf{J}_{\text{cond}} = \sigma(\mathbf{E} + \mathbf{v} \times \mathbf{B})$：由导体内部电荷载流子在外加场和动生电动势共同驱动下产生的电流。
2.  **对流电流** $\mathbf{J}_{\text{conv}} = \rho_e \mathbf{v}$：如果导体本身携带净电荷 $\rho_e$，其整体运动也会形成电流。

在大多数金属导体中，材料是准电中性的（$\rho_e \approx 0$），因此对流电流可以忽略。然而，动生电动势项 $\mathbf{v}\times\mathbf{B}$ 在电磁-结构耦合中至关重要，它是许多发电机、电动机和电磁阻尼现象的物理基础。

#### 变形体的运动学描述：Lagrange、Euler与ALE方法

在对变形体进行数值模拟时，我们需要一个精确的数学框架来描述其运动和相关的物理场。主要有三种描述方法：

1.  **物质描述（拉格朗日，Lagrangian）**: 跟踪每个物质点。坐标 $\mathbf{X}$ 标记一个固定的物质点，其在时刻 $t$ 的空间位置为 $\mathbf{x} = \boldsymbol{\chi}(\mathbf{X}, t)$。该点的物理量（如温度、应力）被看作是 $(\mathbf{X}, t)$ 的函数。物质时间导数 $\frac{D a}{D t} = \frac{\partial a}{\partial t} \big|_{\mathbf{X}}$ 描述了跟随一个特定物质点的物理量的变化率。这种方法非常适合描述固体结构，因为网格随材料一起运动，材料边界和界面被精确捕捉。

2.  **空间描述（欧拉，Eulerian）**: 观察空间中的固定点。坐标 $\mathbf{x}$ 标记一个固定的空间位置，物理量被看作是 $(\mathbf{x}, t)$ 的函数。空间时间导数 $\frac{\partial a}{\partial t} \big|_{\mathbf{x}}$ 描述了在固定空间点上物理量的变化率。这种方法常用于流体力学，因为它可以处理大变形和流体流动，但描述移动边界比较复杂。

3.  **任意拉格朗日-欧拉（ALE）描述**: 这是一种混合方法，试图结合上述两种方法的优点。它引入一个独立的计算网格，该网格的运动既不完全跟随物质（Lagrangian），也不完全固定在空间（Eulerian）。网格点由计算坐标 $\hat{\mathbf{X}}$ 标记，其空间位置为 $\mathbf{x} = \hat{\boldsymbol{\chi}}(\hat{\mathbf{X}}, t)$。网格自身的运动速度为**网格速度** $\mathbf{w}$，而物质的物理速度为**材料速度** $\mathbf{v}$。

在ALE框架中，一个空间场量 $a(\mathbf{x},t)$ 的三种时间导数通过以下链式法则联系起来：
- 物质导数: $\dfrac{D a}{D t} = \dfrac{\partial a}{\partial t} \big|_{\mathbf{x}} + (\mathbf{v} \cdot \nabla) a$
- ALE 导数: $\dfrac{\partial a}{\partial t} \big|_{\hat{\mathbf{X}}} = \dfrac{\partial a}{\partial t} \big|_{\mathbf{x}} + (\mathbf{w} \cdot \nabla) a$

为了在移动的计算网格上求解麦克斯韦方程，需要将标准的欧拉形式（空间导数形式）转换为ALE形式。通过上述关系，我们可以替换空间时间导数 $\frac{\partial a}{\partial t} \big|_{\mathbf{x}}$：
$$
\frac{\partial a}{\partial t} \big|_{\mathbf{x}} = \frac{\partial a}{\partial t} \big|_{\hat{\mathbf{X}}} - (\mathbf{w} \cdot \nabla) a
$$
将此变换应用于法拉第定律和安培-麦克斯韦定律的微分形式，需要从积分形式出发以保证正确性，其最终结果为：
$$
\nabla \times \mathbf{E} = - \frac{\partial \mathbf{B}}{\partial t} \bigg|_{\hat{\mathbf{X}}} - \nabla \times (\mathbf{w} \times \mathbf{B})
$$
$$
\nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t} \bigg|_{\hat{\mathbf{X}}} + \nabla \times (\mathbf{w} \times \mathbf{D})
$$
这些方程中的时间导数是在固定的计算网格点上计算的，而新增的对流项则精确地解释了由于网格运动所带来的影响。至关重要的是，物理本构关系（如广义欧姆定律）必须始终使用物理的材料速度 $\mathbf{v}$，而不是非物理的网格速度 $\mathbf{w}$。

#### 准静态近似：磁准静态模型

求解完整的麦克斯韦方程组在计算上可能非常昂贵，尤其是在电磁波长远大于系统尺寸或某些物理效应占主导地位时。**准静态近似**通过忽略某些项来简化方程组，从而在保持关键物理特性的同时降低计算复杂性。

对于电磁-结构耦合问题，特别是涉及良导体和低频场的应用（如电机、变压器、电磁成形），**磁准静态 (MQS)** 近似非常普遍。MQS模型的核心是假设磁场效应远比电场效应重要。这建立在以下两个关键物理假设之上：

1.  **系统电尺寸小**: 系统的特征长度 $L$ 远小于电磁波在介质中的波长 $\lambda$。即 $L \ll \lambda = 2\pi c_m / \omega$，其中 $\omega$ 是场的工作角频率，$c_m = 1/\sqrt{\mu\epsilon}$ 是介质中的光速。这个假设意味着电磁波传播的延迟可以忽略不计，整个系统中的场可以看作是瞬时响应源的变化。

2.  **传导电流占主导**: 在安培-麦克斯韦定律 $\nabla \times \mathbf{H} = \mathbf{J} + \frac{\partial \mathbf{D}}{\partial t}$ 中，传导电流密度 $\mathbf{J}$ 的幅值远大于位移电流密度 $\frac{\partial \mathbf{D}}{\partial t}$ 的幅值。对于时谐场，这意味着 $|\mathbf{J}| \sim \sigma|\mathbf{E}|$ 远大于 $|\frac{\partial \mathbf{D}}{\partial t}| \sim \omega\epsilon|\mathbf{E}|$。这给出了一个无量纲判据：
    $$
    \frac{\omega\epsilon}{\sigma} \ll 1
    $$
    这个比值衡量了位移电流与传导电流的相对重要性。对于良导体（$\sigma$ 很大）和低频（$\omega$ 较小）情况，这个条件通常成立。

在MQS近似下，安培定律简化为 $\nabla \times \mathbf{H} \approx \mathbf{J}$，完全忽略了位移电流。然而，法拉第感应定律 $\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$ 被完整保留，因为它正是感应涡流的根源。这些简化的方程与广义欧姆定律 $\mathbf{J} \approx \sigma(\mathbf{E} + \mathbf{v} \times \mathbf{B})$ 共同构成了描述变形导体中涡流和相关洛伦兹力的MQS模型。

### 耦合现象的本构模型

宏观的电磁-结构耦合效应最终体现在材料的本构关系上。本构模型将微观物理机制（如晶格畸变、电偶极子[排列](@entry_id:136432)）与宏观可观测的物理量（如应力、应变、电场、磁场）联系起来。下面我们介绍两种重要的耦合效应。

#### 压电效应：机电耦合的谐振器模型

**压电效应**是指某些电介质晶体在受到机械应力时表面产生电荷（正压电效应），以及在受到外加电场时产生机械形变（逆压电效应）的现象。这种双向耦合是许多传感器、执行器和高频滤波器的核心工作原理。

线性压电效应的本构关系（应力-电荷形式）可以写成张量形式：
$$
\boldsymbol{\sigma} = \mathbf{C} : \boldsymbol{\epsilon}_{\text{mech}} - \mathbf{e}^\top \mathbf{E}
$$
$$
\mathbf{D} = \mathbf{e} : \boldsymbol{\epsilon}_{\text{mech}} + \boldsymbol{\epsilon} \mathbf{E}
$$
其中，$\boldsymbol{\sigma}$ 是柯西应力张量，$\boldsymbol{\epsilon}_{\text{mech}}$ 是机械应变张量，$\mathbf{E}$ 是电场强度，$\mathbf{D}$ 是电位移矢量。材料参数包括四阶弹性张量 $\mathbf{C}$、二阶介电张量 $\boldsymbol{\epsilon}$ 和三阶压电耦合张量 $\mathbf{e}$。

为了直观理解这种耦合如何影响系统动力学，我们可以考察一个一维压电板谐振器模型。考虑一个厚度为 $t$ 的压电板，其上下表面被电极覆盖，并外接一个电感 $L$。我们可以建立一个集总参数的两自由度模型，用广义坐标 $u(t)$（代表厚度方向的平均位移）和 $q(t)$（代表电极上的电荷）来描述系统。

通过能量方法（拉格朗日力学），可以推导出系统的耦合运动方程。系统的总动能是机械动能和电感储能之和，总势能是弹性储能和电容静电储能之和，其中包含了压电耦合项。最终得到的运动方程可以写成矩阵形式 $\mathbf{M}\ddot{\mathbf{x}} + \mathbf{K}\mathbf{x} = \mathbf{0}$，其中 $\mathbf{x} = [u, q]^\top$。求解这个系统的广义特征值问题 $\mathbf{K}\mathbf{X} = \omega^2 \mathbf{M}\mathbf{X}$，可以得到系统的两个固有谐振频率。

分析表明，当压电耦合系数 $\mathbf{e}$ 不为零时，系统的两个固有频率会发生改变。如果将无耦合时的纯机械谐振频率 $\omega_m$ 和纯电气谐振频率 $\omega_e = 1/\sqrt{LC_0}$（$C_0$为压电板的钳定电容）调谐到彼此接近时，耦合效应最为显著。它会导致两个新的混合模式频率一个比原来的高，一个比原来的低，这种现象称为**模式劈裂**（mode splitting）。两个新频率之间的差值直接反映了机电耦合的强度。这种现象是耦合系统动力学的一个普遍特征，表明能量在两个子系统之间发生了有效的交换。

#### 磁致伸缩效应：基于自由能的应变推导

**磁致伸缩效应**是指铁磁性材料在外加磁场中会发生尺寸变化的现象。与压电效应类似，它也是一种双向耦合，机械应力同样可以改变材料的磁特性（Villari效应）。

分析磁致伸缩这类热力学耦合现象的一个强有力的方法是基于材料的**亥姆霍兹自由能密度** $\psi$。自由能是一个状态函数，它包含了弹性储能、磁场储能以及它们之间的耦合能。对于一个各向同性的磁致伸缩材料，在小应变假设下，其自由能密度可以写成如下形式：
$$
\psi(\boldsymbol{\varepsilon},\mathbf{B}) = \underbrace{\tfrac{1}{2}\lambda (\operatorname{tr}\boldsymbol{\varepsilon})^{2} + \mu\, \boldsymbol{\varepsilon}:\boldsymbol{\varepsilon}}_{\text{弹性储能}} + \underbrace{\tfrac{1}{2}\alpha\, \mathbf{B}\cdot\mathbf{B}}_{\text{磁场储能}} \underbrace{- \beta\, \mathbf{B}\cdot\boldsymbol{\varepsilon}\cdot\mathbf{B}}_{\text{磁弹耦合能}}
$$
其中，$\boldsymbol{\varepsilon}$ 是小应变张量，$\mathbf{B}$ 是磁感应强度，$\lambda$ 和 $\mu$ 是拉梅弹性常数，$\alpha$ 是磁化相关参数，$\beta$ 是磁弹耦合系数。

根据热力学共轭关系，应力张量 $\boldsymbol{\sigma}$ 可以通过自由能对应变张量 $\boldsymbol{\varepsilon}$ 求偏导数得到：
$$
\boldsymbol{\sigma} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}} = \lambda (\operatorname{tr}\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon} - \beta (\mathbf{B} \otimes \mathbf{B})
$$
这个本构关系清晰地显示了磁场如何产生应力（或等效地，产生应变）。最后一项 $-\beta(\mathbf{B}\otimes\mathbf{B})$ 就是**磁致应力**。

考虑一个细长的磁致伸缩杆，沿轴向施加一个均匀磁场 $\mathbf{B}=B\mathbf{n}$，并且杆体不受任何外部机械载荷（即 $\boldsymbol{\sigma}=\mathbf{0}$）。通过求解 $\boldsymbol{\sigma}=\mathbf{0}$ 这个方程，我们可以得到平衡状态下的应变张量 $\boldsymbol{\varepsilon}$。最终可以计算出沿杆轴向的法向应变，即**磁致伸缩应变** $\varepsilon_{\parallel}$：
$$
\varepsilon_{\parallel} = \frac{\beta B^{2} (\lambda + \mu)}{\mu (3\lambda + 2\mu)}
$$
这个结果表明，应变与磁场强度的平方成正比，其符号和大小由材料的弹性常数和磁弹耦合系数决定。这种基于热力学势函数的方法是推导和建立复杂多物理场本构模型的标准范式。

### 耦合问题的计算策略

求解电磁-结构耦合问题通常需要借助数值方法，如有限元法（FEM）或有限差分法（FDTD）。对于瞬态问题，时间积分算法的选择对求解的稳定性、精度和效率至关重要。

#### 求解方案：整体式与分裂式算法

对于一个由多个子系统（如电磁和结构）组成的耦合问题，瞬态求解算法大致可以分为两类：

1.  **整体式（Monolithic）算法**: 在每个时间步内，将所有子系统的未知量（如位移、速度、电流、场强）作为一个大的向量，联立求解一个庞大的代数方程组。
    -   **优点**: 如果采用隐式时间积分格式（如后向欧拉法或隐式Newmark法），整体式算法通常是**无条件稳定**的。这意味着时间步长 $\Delta t$ 的选择仅受精度要求的限制，而不受稳定性条件的约束。这对于刚性问题（包含非常快的时间尺度）尤其有利。
    -   **缺点**: 需要开发和维护一个庞大而复杂的多物理场求解器。求解大型联立方程组的计算成本和内存需求可能非常高。

2.  **分裂式（Partitioned）或交错式（Staggered）算法**: 在每个时间步内，依次求解每个子系统。例如，先求解电磁方程得到电磁力，然后将此力作为载荷施加到结构上，求解结构的响应。
    -   **优点**: 模块化程度高，可以复用现有的、经过充分验证的单物理场求解器。实现相对简单，便于软件开发和维护。
    -   **缺点**: 稳定性是一个主要挑战。在**松耦合**（loosely coupled）或**显式耦合**（explicit coupling）方案中（即在一个时间步内，子系统之间只交换一次信息，不进行迭代），耦合项的显式处理（例如，用前一时刻的结构速度计算当前时刻的电磁力）会引入数值不稳定性。这种不稳定性在强耦合问题中尤为严重，通常导致非常小的时间步长限制，其严苛程度随耦合强度 $k_c$ 的增加而急剧恶化（例如，$\Delta t \lesssim C/k_{c}^{2}$）。此外，这种时间上的滞后还会引入**分裂误差**，将方法的整体精度限制在一阶，即使每个子求解器本身是二阶的。

为了克服分裂式算法的稳定性问题，可以采用**强耦合**（strongly coupled）或**迭代耦合**（iterative coupling）策略。即在每个时间步内，在子系统之间进行多次迭代，直到界面上的耦合变量（如力和速度）收敛。收敛后，其结果与整体式算法在同一时间步的结果在数学上是等价的，因此可以恢复无条件稳定性和更高的精度。然而，这种迭代会增加每个时间步的计算成本。

#### 先进技术：多速率时间积分

在许多电磁-结构耦合问题中，两个子系统具有截然不同的特征时间尺度。例如，电磁波的传播速度极快，要求非常小的时间步长（$\Delta t_{\text{em}}$）来满足CFL稳定性条件或捕捉高频现象；而机械结构的响应通常慢得多，用较大的时间步长（$\Delta t_{\text{mech}}$）就足以保证精度。在这种情况下，对整个系统使用统一的最小时间步长 $\Delta t_{\text{em}}$ 会极大地浪费计算资源。

**多速率时间积分**是一种高效的策略。其思想是：让每个子系统使用各自合适的步长时间。例如，在每个结构宏观步 $\Delta t_{\text{mech}}$ 内，对电磁子系统进行 $N$ 次子循环（subcycling），其微观步长为 $\Delta t_{\text{em}} = \Delta t_{\text{mech}}/N$。

关键问题在于如何在不同速率的子系统之间传递耦合信息。例如，在每个宏观步内计算出的 $N$ 个瞬时电磁力值，应如何施加到结构求解器上？
- **采样保持 (Sample-and-hold)**: 直接使用宏观步结束时的最后一个电磁力值。这种方法简单，但它等同于用一个瞬时值来近似一个时间段内的平均力，会引入一阶精度误差 $\mathcal{O}(\Delta t_{\text{mech}})$。
- **时间平均耦合 (Time-averaged coupling)**: 将宏观步内所有子循环计算出的电磁力进行时间平均，然后将这个平均力施加到结构上。这在物理上更合理，因为它更好地代表了在一个结构时间步内冲量的累积效应。使用梯形法则等数值积分方法计算这个平均值，其积分误差为 $\mathcal{O}((\Delta t_{\text{em}})^2)$。

为了在固定计算成本下达到最高精度，需要明智地选择子循环因子 $N$。一个常用的原则是**误差均衡**（equidistribution of errors）。即调整 $N$ 使得来自不同来源的误差贡献（如电磁子循环的离散化误差和宏观步长上的分裂误差）量级相当。例如，如果总误差可以表示为 $\mathcal{E} \approx C_{1}(\Delta t_{\text{em}})^{2} + C_{2}(\Delta t_{\text{mech}})^{2}$，为了平衡两个误差项，我们令 $C_{1}(\Delta t_{\text{mech}}/N^{\star})^{2} = C_{2}(\Delta t_{\text{mech}})^{2}$，从而得到最优子循环因子 $N^{\star} = \sqrt{C_1/C_2}$。这使得我们能够在不同时间尺度之间实现计算资源的优化分配。