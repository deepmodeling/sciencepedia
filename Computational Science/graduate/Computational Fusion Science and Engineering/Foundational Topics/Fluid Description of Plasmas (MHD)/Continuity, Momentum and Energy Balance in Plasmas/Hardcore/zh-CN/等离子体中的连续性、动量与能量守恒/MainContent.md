## 引言
在等离子体物理的广阔领域中，理解物质第四态的复杂行为是推动从核聚变能源到天体物理学等众多科学前沿的关键。无论是[托卡马克](@entry_id:160432)中被约束的亿度高温等离子体，还是太阳风中广袤的磁化气流，其动态演化都遵循着一组共同的基本物理原理——质量、动量和能量的守恒定律。然而，从这些抽象的守恒定律到预测和解释真实世界等离子体中观察到的具体现象，存在着一条概念上的鸿沟。本文旨在弥合这一差距，系统地阐明这些基本平衡方程如何构成我们理解等离子体世界的数学和物理框架。

通过本文的学习，读者将深入了解这些控制方程的结构及其物理内涵。在“原理与机制”一章中，我们将从微观动理学角度出发，构建连续性、动量和[能量平衡方程](@entry_id:191484)，并剖析其中如压力张量、广义欧姆定律和能量交换项等关键组成部分的物理意义。随后，在“应用与跨学科联系”一章中，我们将展示这些理论如何应用于解释聚变装置中的宏观输运、功率平衡、边界物理，以及[湍流](@entry_id:151300)和磁重联等[非线性](@entry_id:637147)现象。最后，“动手实践”部分将提供具体计算问题，帮助读者将理论知识转化为解决实际问题的能力。

现在，让我们首先进入第一章，深入探讨这些控制方程的基本原理与内在机制。

## 原理与机制

本章在前一章介绍的基础上，深入探讨描述等离子体的基本守恒定律，即连续性、动量和能量平衡方程。我们将从基本原理出发，构建描述等离子体作为导电流体的数学框架。本章的核心目标不仅是呈现这些方程，更重要的是阐明其中各个项的物理机制，并揭示这些机制如何决定从实验室聚变装置到天体物理环境中等离子体的复杂行为。我们将通过一系列思想实验和计算示例，系统地剖析这些控制方程的结构及其在[计算建模](@entry_id:144775)中的应用。

### 粒子守恒：连续性方程

任何流体描述的出发点都是质量或粒子数的守恒。对于等离子体中的特定组分 $s$（例如电子或某种离子），其数密度为 $n_s(\boldsymbol{x}, t)$，宏观流速为 $\boldsymbol{u}_s(\boldsymbol{x}, t)$。在空间中的任意一点，粒子数密度的变化率由两个因素决定：一是[粒子流](@entry_id:753205)进或流出该点的净通量，二是该点存在的粒子源或汇。这构成了**[连续性方程](@entry_id:195013) (continuity equation)** 的局部或微分形式：

$$
\frac{\partial n_s}{\partial t} + \nabla \cdot (n_s \boldsymbol{u}_s) = S_s
$$

其中，$S_s$ 是单位体积、单位时间内的净粒子源率（例如，电离减去复合）。$\nabla \cdot (n_s \boldsymbol{u}_s)$ 这一项是粒子通量 $n_s \boldsymbol{u}_s$ 的**散度 (divergence)**，它量化了从一个无穷小体积中流出的净粒子数。

虽然局部形式在理论分析中至关重要，但在计算物理和许多实验分析中，我们更关心一个有限体积内的全局守恒。考虑一个随时间变化的控制体积 $V(t)$，其边界 $\partial V(t)$ 以速度场 $\boldsymbol{w}(\boldsymbol{x}, t)$ 运动。体积内粒子总数 $N_s(t) = \int_{V(t)} n_s dV$ 的变化率是多少？要回答这个问题，我们需要一个强大的数学工具，即**雷诺输运定理 (Reynolds Transport Theorem, RTT)**。该定理将一个移动体积上积分量的时间导数与场本身的[局部时](@entry_id:194383)间导数和穿过移动边界的通量联系起来。

将[雷诺输运定理](@entry_id:191217)应用于密度 $n_s$，我们得到：
$$
\frac{d N_s}{dt} = \frac{d}{dt} \int_{V(t)} n_s dV = \int_{V(t)} \frac{\partial n_s}{\partial t} dV + \oint_{\partial V(t)} n_s \boldsymbol{w} \cdot \hat{\boldsymbol{n}} dA
$$
其中 $\hat{\boldsymbol{n}}$ 是边界上指向外部的[单位法向量](@entry_id:178851)。将局部连续性方程代入上式，并使用高斯散度定理，可以得到全局[粒子平衡](@entry_id:753197)方程 ：

$$
\frac{d}{dt}\int_{V(t)} n_{s} dV = \int_{V(t)} S_{s} dV - \oint_{\partial V(t)} n_{s}(\boldsymbol{u}_{s}-\boldsymbol{w}) \cdot \hat{\boldsymbol{n}} dA
$$

这个方程有深刻的物理含义。它表明，控制体积内粒子总数的变化率等于体积内的总源项减去穿过边界的净[粒子通量](@entry_id:753207)。至关重要的是，这里的通量是由流体相对于移动边界的**[相对速度](@entry_id:178060) (relative velocity)** $(\boldsymbol{u}_s - \boldsymbol{w})$ 决定的。

这个结果在[计算聚变科学](@entry_id:1122784)中尤为重要。例如，在**任意拉格朗日-欧拉 (Arbitrary Lagrangian-Eulerian, ALE)** 方法中，[计算网格](@entry_id:168560)可以独立于流体运动而移动。为了在移动的网格单元之间精确地保持粒子守恒，[数值通量](@entry_id:145174)必须基于流体相对于网格面运动的相对速度来计算 。

两个重要的极限情况值得注意：
1.  **固定（欧拉）控制体积**：此时 $\boldsymbol{w} = \boldsymbol{0}$，方程简化为对局部连续性方程的直接积分。
2.  **物质（拉格朗日）控制体积**：控制体积随流体一起运动，即 $\boldsymbol{w} = \boldsymbol{u}_s$。在这种情况下，如果没有粒子源（$S_s=0$），则相对速度为零，通量项消失，$\frac{d N_s}{dt} = 0$。这意味着跟随流体运动的体积内的粒子总数是守恒的，这符合物理直觉。

### 动量平衡：等离子体中的力

在描述了粒子数的守恒之后，我们转向描述等离子体运动状态的动量守恒。单流体或多流体等离子体模型的动量方程本质上是牛顿第二定律的体现，即单位体积内流体的动量变化率等于作用在其上的力的总和。对于等离子体中的组分 $s$，其动量方程的一般形式为：

$$
\rho_s \left( \frac{\partial \boldsymbol{u}_s}{\partial t} + \boldsymbol{u}_s \cdot \nabla \boldsymbol{u}_s \right) = n_s q_s(\boldsymbol{E} + \boldsymbol{u}_s \times \boldsymbol{B}) - \nabla \cdot \mathsf{P}_s + \mathbf{R}_s
$$

其中 $\rho_s = m_s n_s$ 是质量密度。左边是单位体积的惯性项。右边则包含了作用在流体元素上的各种力：$n_s q_s(\boldsymbol{E} + \boldsymbol{u}_s \times \boldsymbol{B})$ 是宏观**[洛伦兹力](@entry_id:145104) (Lorentz force)**；$-\nabla \cdot \mathsf{P}_s$ 是由粒子热运动产生的内力，即压力[梯度力](@entry_id:166847)的推广；$\mathbf{R}_s$ 代表与其他组分碰撞所产生的动量交换或摩擦力。

#### [压力张量](@entry_id:147910)

在[动量方程](@entry_id:197225)中，**[压力张量](@entry_id:147910) (pressure tensor)** $\mathsf{P}_s$ 扮演着核心角色。它源于[粒子速度](@entry_id:196946)相对于平均流速的随机涨落，即所谓的热运动。从动理学角度看，压力张量是粒子分布函数 $f_s$ 的二阶[中心矩](@entry_id:270177) ：

$$
\mathsf{P}_s \equiv m_s \int \mathbf{c}\mathbf{c} f_s d^3v
$$

其中 $\mathbf{c} = \mathbf{v} - \boldsymbol{u}_s$ 是粒子的**奇特速度 (peculiar velocity)**，$\mathbf{c}\mathbf{c}$ 是[并矢积](@entry_id:748716)。$\mathsf{P}_s$ 的物理意义是随机热运动所携带的动量在空间中的通量。由于 $c_i c_j = c_j c_i$，压力张量是一个**[对称张量](@entry_id:148092)**。此外，由于它是基于相对速度 $\mathbf{c}$ 定义的，它在伽利略变换下保持不变，即**伽利略不变性 (Galilean invariance)**。

在流体模型中，将压力张量分解为其各向同性部分和各向异性部分是标准做法。任何二阶[对称张量](@entry_id:148092)都可以唯一地分解为一个标量（迹）[部分和](@entry_id:162077)一个迹为零的偏部分。对于压力张量，这对应于：

$$
\mathsf{P}_s = p_s \mathsf{I} + \boldsymbol{\pi}_s
$$

其中 $p_s = \frac{1}{3} \mathrm{Tr}(\mathsf{P}_s)$ 是我们熟悉的**标量压力 (scalar pressure)**，它代表三个方向上正应力的平均值。$\mathsf{I}$ 是单位张量。$\boldsymbol{\pi}_s$ 是**[偏应力张量](@entry_id:267642) (deviatoric stress tensor)**，它描述了压力的各向异性部分，且其迹为零 ($\mathrm{Tr}(\boldsymbol{\pi}_s)=0$)。对于完全[热平衡](@entry_id:157986)的麦克斯韦分布，压力是各向同性的，$\boldsymbol{\pi}_s = \mathbf{0}$ 。

在强磁场中，等离子体的性质沿磁场方向和垂直磁场方向有显著差异。这导致压力也常常是各向异性的。一个重要的模型是**回旋各向异性 (gyrotropic)** [压力张量](@entry_id:147910)，其形式为：

$$
\mathsf{P}_{\text{gyro}} = p_{\perp} \mathsf{I} + (p_{\parallel} - p_{\perp}) \mathbf{b} \mathbf{b}
$$

其中 $p_\parallel$ 和 $p_\perp$ 分别是平行和垂直于磁场方向 $\mathbf{b} = \mathbf{B}/|\mathbf{B}|$ 的压力。这种形式的[压力张量](@entry_id:147910)可以分解为标量压力 $p_s = \frac{1}{3}(p_\parallel + 2p_\perp)$ 和[偏应力](@entry_id:163323) $\boldsymbol{\pi}_s = (p_\parallel - p_\perp)(\mathbf{b}\mathbf{b} - \frac{1}{3}\mathsf{I})$ 。这种分解对于理解能量平衡中的各向异性效应至关重要。

#### [磁流体动力学平衡](@entry_id:1127852)

在许多聚变和天体物理应用中，等离子体处于近似静态平衡状态，此时惯性项可以忽略。单流体动量方程简化为力平衡方程。在最简单的情况下，即[各向同性压力](@entry_id:269937)，平衡条件是压力[梯度力](@entry_id:166847)与[洛伦兹力](@entry_id:145104)相抗衡：

$$
\nabla p = \mathbf{J} \times \mathbf{B}
$$

这个方程是**磁流体动力学 (Magnetohydrodynamics, MHD)** 的基石，它描述了磁场如何约束高温等离子体 。为了更深入地理解[磁约束](@entry_id:161852)的物理机制，可以将洛伦兹力分解为两个部分：

$$
\mathbf{J} \times \mathbf{B} = -\nabla\left(\frac{B^2}{2\mu_0}\right) + \frac{(\mathbf{B} \cdot \nabla)\mathbf{B}}{\mu_0}
$$

第一项 $-\nabla(B^2/2\mu_0)$ 类似于一个压力[梯度力](@entry_id:166847)，被称为**磁压力 (magnetic pressure)**。它描述了磁场如同气体一样，倾向于从强场区向弱场区膨胀。第二项 $(\mathbf{B} \cdot \nabla)\mathbf{B}/\mu_0$ 被称为**[磁张力](@entry_id:192593) (magnetic tension)**，它类似于拉伸的橡皮筋，描述了弯曲磁力线试图变直的趋势。磁约束的本质就是利用[磁压力](@entry_id:272413)和磁张力的[合力](@entry_id:163825)来平衡等离子体的[热压力](@entry_id:202761)。

通过比较[热压力](@entry_id:202761) $p$ 与[磁压力](@entry_id:272413) $B^2/2\mu_0$，我们可以定义一个关键的无量纲参数——**等离子体 Beta (plasma beta)**：

$$
\beta \equiv \frac{p}{B^2 / (2\mu_0)} = \frac{2\mu_0 p}{B^2}
$$

$\beta$ 值衡量了等离子体压力相对于磁场压力的重要性。在[环形装置](@entry_id:188972)（如[托卡马克](@entry_id:160432)）中，高压等离子体不仅被磁场约束，其自身压力也会显著改变磁场位形。通过量级分析可以发现，压力效应的显著性取决于一个组合参数。在主半径为 $R$、小半径（梯度标长）为 $a$ 的环中，压力[梯度力](@entry_id:166847)尺度约为 $p/a$，而抵抗其向外膨胀的主要磁力来自磁张力，其尺度约为 $B^2/(\mu_0 R)$。当这两个力量相当时，平衡位形会发生显著改变（例如，磁轴向外移动，即 **Shafranov 位移 (Shafranov shift)**）。该判据为 ：

$$
\frac{p}{a} \gtrsim \frac{B^2}{\mu_0 R} \quad \implies \quad \left(\frac{\beta}{2}\right) \left(\frac{R}{a}\right) \gtrsim 1
$$

这个关系表明，对于给定的 $\beta$ 值，环径比 $R/a$ 越大（即越“细长”的环），压力对平衡的扭曲效应越强。

#### 广义欧姆定律

虽然单流体[MHD模型](@entry_id:1127854)在许多情况下很有用，但它掩盖了不同组分（特别是电子和离子）之间的[相对运动](@entry_id:169798)。这些相对运动是产生电流和许多重要物理效应的根源。**广义欧姆定律 (generalized Ohm's law)** 并非一个基本定律，而是电子[动量方程](@entry_id:197225)的重写形式，它显式地给出了维持[等离子体电流](@entry_id:182365)所需的电场 。

从电子[动量方程](@entry_id:197225)出发，并将电子速度 $\mathbf{u}_e$ 用宏观流速 $\mathbf{u}$ 和电流密度 $\mathbf{J} \approx en(\mathbf{u}_i - \mathbf{u}_e)$ 来表示（$\mathbf{u}_e \approx \mathbf{u} - \mathbf{J}/(ne)$），我们可以推导出：

$$
\mathbf{E} + \mathbf{u} \times \mathbf{B} = \eta \mathbf{J} + \frac{\mathbf{J} \times \mathbf{B}}{ne} - \frac{\nabla p_e}{ne} - \frac{m_e}{e} \frac{D_e \mathbf{u}_e}{Dt}
$$

这个方程的每一项都有明确的物理意义：
-   $\mathbf{E} + \mathbf{u} \times \mathbf{B}$：这是随流体运动的坐标系中所感受到的电场。在理想MHD中，这一项为零，意味着磁力线被“冻结”在流体中。
-   $\eta \mathbf{J}$：**电阻项 (resistive term)**，源于电子与离子的碰撞，导致[能量耗散](@entry_id:147406)。$\eta$ 是[电阻率](@entry_id:143840)。
-   $\frac{\mathbf{J} \times \mathbf{B}}{ne}$：**霍尔项 (Hall term)**。它源于承载电流的电子受到的洛伦兹力。这个力导致电子漂移，产生一个垂直于 $\mathbf{J}$ 和 $\mathbf{B}$ 的电场。它代表了电子和离子运动在磁场中的[解耦](@entry_id:160890)。
-   $-\frac{\nabla p_e}{ne}$：**电子压力梯度项**，有时被称为“电池效应”，可以驱动电流。
-   $-\frac{m_e}{e} \frac{D_e \mathbf{u}_e}{Dt}$：**电子惯性项**，在高频现象中变得重要。

霍尔项的保留与否，决定了我们是使用标准[MHD模型](@entry_id:1127854)还是**霍尔-MHD (Hall-MHD)** 模型。通过[量纲分析](@entry_id:140259)可知，霍尔项与理想MHD项 $(\mathbf{u} \times \mathbf{B})$ 的比值尺度约为 $k d_i$，其中 $k$ 是现象的特征波数，$d_i = \sqrt{m_i/(\mu_0 n e^2)}$ 是**[离子趋肤深度](@entry_id:1126728) (ion skin depth)** 。因此，当研究的物理现象的尺度与[离子趋肤深度](@entry_id:1126728)相当时 ($k d_i \sim 1$)，[霍尔效应](@entry_id:136243)变得不可忽略，必须使用包含霍尔项的更精确模型。

### 能量平衡：加热、冷却与输运

能量守恒是描述等离子体[热力学状态](@entry_id:755916)演化的第三个关键支柱。等离子体的总能量包括流体的宏观动能、内能（热能）以及电磁场的能量。本节我们主要关注等离子体内能的演化，即温度的变化。

#### 能量传递机制：压力功项

在能量方程中，一个核心的项描述了宏观流动动能与内能之间的转换。这个能量转换的功率密度由压力张量和[速度梯度](@entry_id:261686)的[双点积](@entry_id:748648)给出：$\mathsf{P}:\nabla\mathbf{u}$。这个**压力功项 (pressure work term)** 的物理起源可以从动量方程推导动能方程的过程中看出 。动能密度的变化包含一个源项 $-\mathbf{u}\cdot(\nabla\cdot\mathsf{P})$，利用张量恒等式，该项可以分解为[能量通量](@entry_id:266056)的散度 $\nabla\cdot(\mathsf{P}\cdot\mathbf{u})$ 和一个局域交换项 $-\mathsf{P}:\nabla\mathbf{u}$。根据总能量守恒，这个交换项在内能方程中以相反的符号 $(+\mathsf{P}:\nabla\mathbf{u})$ 出现，代表了压[力场](@entry_id:147325)对流体做功，从而将宏观动能转化为内能。

这个项的具体形式取决于压力的性质：
-   **[各向同性压力](@entry_id:269937)**：当 $\mathsf{P} = p\mathsf{I}$ 时，$\mathsf{P}:\nabla\mathbf{u} = p\mathsf{I}:\nabla\mathbf{u} = p\nabla\cdot\mathbf{u}$。功仅在流体发生体积压缩 ($\nabla\cdot\mathbf{u}  0$) 或膨胀 ($\nabla\cdot\mathbf{u} > 0$) 时才发生。这是可逆的**[压缩功](@entry_id:265787) (compressional work)**。
-   **[各向异性压力](@entry_id:746456)**：对于前面介绍的回旋[各向异性压力](@entry_id:746456)，功项变为 ：
    $$
    \mathsf{P}_{\text{gyro}}:\nabla\mathbf{u} = p_\perp \nabla\cdot\mathbf{u} + (p_\parallel - p_\perp)\mathbf{b}\mathbf{b}:\nabla\mathbf{u}
    $$
    除了[压缩功](@entry_id:265787)，还出现了第二项，它与沿磁场方向的拉伸或压缩 $(\mathbf{b}\mathbf{b}:\nabla\mathbf{u})$ 有关。这意味着，即使在[不可压缩流](@entry_id:140301) ($\nabla\cdot\mathbf{u}=0$) 中，只要存在沿场方向的速度剪切，[各向异性压力](@entry_id:746456)仍然可以与流体交换能量。
-   **粘滞应力**：当包含[偏应力张量](@entry_id:267642) $\boldsymbol{\pi}_s$ 时（例如由碰撞引起的[粘滞](@entry_id:201265)），功项包含 $\boldsymbol{\pi}_s:\nabla\mathbf{u}$。这一项通常与流体的形变速率有关，代表了由于内部摩擦而产生的**不可逆[粘滞](@entry_id:201265)加热 (irreversible viscous heating)**  。

#### 不可逆加热：电阻的贡献

除了可逆的[压缩功](@entry_id:265787)和[粘滞](@entry_id:201265)加热外，等离子体中一个主要的不可逆加热源是电阻耗散。电磁场[对等离子体](@entry_id:1129298)做功的功率密度为 $\mathbf{J}\cdot\mathbf{E}$。利用广义欧姆定律，我们可以分解这个项的物理成分 ：

$$
\mathbf{J}\cdot\mathbf{E} = \mathbf{J} \cdot (\eta\mathbf{J} - \mathbf{u}\times\mathbf{B} + \dots) = \eta J^2 + \mathbf{u}\cdot(\mathbf{J}\times\mathbf{B}) + \dots
$$

分解后的各项意义清晰：
-   $\eta J^2$：这一项被称为**[欧姆加热](@entry_id:190028) (Ohmic heating)** 或 **焦耳加热 ([Joule heating](@entry_id:150496))**。由于[电阻率](@entry_id:143840) $\eta$ 和电流密度的平方 $J^2$ 均为非负值，该项总是正的，代表了电磁能通过碰撞不可逆地转化为等离子体内能（热量）的过程。
-   $\mathbf{u}\cdot(\mathbf{J}\times\mathbf{B})$：这一项代表了[洛伦兹力](@entry_id:145104)对宏观流体做的机械功，它改变的是流体的宏观动能，是一个可逆的能量交换过程。

因此，$\eta J^2$ 是等离子体中一个基本的熵产生项，直接导致等离子体温度的升高。我们可以通过对该功率密度在整个等离子体体积上积分，来计算总的欧姆加热功率，例如，在一个具有特定电流和[电阻率](@entry_id:143840)分布的柱形等离子体中 。

#### [破缺对称性](@entry_id:1121893)的后果：磁能与[磁螺度](@entry_id:751625)的电阻衰减

在理想MHD模型中（$\eta=0$），存在几个重要的[守恒量](@entry_id:161475)，其中最著名的是磁通量和[磁螺度](@entry_id:751625)。[电阻率](@entry_id:143840)的存在打破了这些理想守恒律。

**[磁螺度](@entry_id:751625) (Magnetic helicity)**，$K = \int_V \mathbf{A}\cdot\mathbf{B} dV$（其中 $\mathbf{B}=\nabla\times\mathbf{A}$），是衡量磁场拓扑复杂性（如缠绕、链接程度）的物理量。在理想MHD中，它是严格守恒的。然而，当存在电阻时，[磁螺度](@entry_id:751625)会发生衰减。通过推导可以证明，其衰减率正比于[电阻率](@entry_id:143840) ：

$$
\frac{dK}{dt} = -2\int_V \eta \mathbf{J}\cdot\mathbf{B} dV
$$

同样，总[磁场能量](@entry_id:267501) $U_B = \int_V \frac{B^2}{2\mu_0} dV$ 也因电阻而耗散。[能量耗散](@entry_id:147406)率正是总的[欧姆加热](@entry_id:190028)功率 ：

$$
\frac{dU_B}{dt} = -\int_V \eta J^2 dV
$$

这表明[磁场能量](@entry_id:267501)通过电阻效应被不可逆地转化为了等离子体的热能。这两个方程定量地描述了电阻是如何导致磁场重联、[磁结构](@entry_id:201216)松弛和[能量耗散](@entry_id:147406)的。

#### 聚变装置中的全局功率平衡

将上述能量来源、损失和转换机制整合起来，我们可以为聚变装置（如[托卡马克](@entry_id:160432)）构建一个全局功率[平衡模型](@entry_id:636099) 。考虑一个以最后闭合磁面为边界的[固定控制体](@entry_id:272149)积 $V$，其总热能为 $W(t) = \int_V \sum_s \frac{3}{2}n_s T_s dV$。能量[守恒原理](@entry_id:1122907)表明，输入功率必须等于输出功率加上存储能量的变化率：

$$
P_{\alpha} + P_{\text{aux}} = P_{\text{rad}} + P_{\text{cond}} + P_{\text{conv}} + \frac{dW}{dt}
$$

其中各项的定义如下：
-   **输入功率**：$P_\alpha$ 是由聚变反应产生的阿尔法粒子减速加热的功率；$P_{\text{aux}}$ 是由[中性束注入](@entry_id:204293)或[射频波](@entry_id:195520)等外部系统提供的辅助加热功率。[欧姆加热](@entry_id:190028)也是一种输入功率，但在现代大型[托卡马克](@entry_id:160432)中通常不是[主导项](@entry_id:167418)。
-   **存储能量变化**：$dW/dt$ 是等离子体总热能的时间变化率。
-   **输出（损失）功率**：
    -   $P_{\text{rad}}$：由[韧致辐射](@entry_id:270512)和杂质[线辐射](@entry_id:751334)等过程以光子形式损失的功率。
    -   $P_{\text{cond}}$：通过**[热传导](@entry_id:143509) (conduction)** 损失的功率，由热流密度 $\mathbf{q}_{\text{cond}} = -\kappa \nabla T$ 决定，其中 $\kappa$ 是热导率。总传导功率为跨越边界的净热流通量。
    -   $P_{\text{conv}}$：通过**对流 (convection)** 损失的功率。当等离子体流出控制体积时，它不仅带走了自身的内能，还对外界做了流动功。因此，对流的[能量通量](@entry_id:266056)是**焓流 (enthalpy flux)** $h_s \mathbf{v}_s$，其中焓密度 $h_s = u_s + p_s = \frac{5}{2}n_s T_s$（对于理想气体）。这是全局能量平衡中的一个关键点 。

这个[全局平衡方程](@entry_id:272290)是评估和设计[聚变反应](@entry_id:749665)堆性能的基本工具。

### 闭合问题：从动理学到流体模型

到目前为止，我们已经介绍了描述等离子体的流体方程，但留下了一个悬而未决的根本问题：这些方程是如何构成一个自洽的、可解的系统的？这引出了流体理论中的核心挑战——**闭合问题 (closure problem)**。

#### 矩方程等级链与闭合问题

[流体方程](@entry_id:195729)可以通过对底层的[动理学方程](@entry_id:751029)（如[Vlasov-Fokker-Planck方程](@entry_id:1133853)）取[速度矩](@entry_id:1133763)来系统地导出。
-   对[动理学方程](@entry_id:751029)积分（零阶矩）得到连续性方程。
-   乘以 $\mathbf{v}$ 再积分（一阶矩）得到动量方程。
-   乘以 $\mathbf{v}\mathbf{v}$ 再积分（二阶矩）得到压力张量或能量的[演化方程](@entry_id:268137)。

问题在于，这个过程会产生一个无限的“等级链”。具体来说，第 $N$ 阶矩的[演化方程](@entry_id:268137)总是会包含第 $N+1$ 阶矩的项。

我们可以通过考察[压力张量](@entry_id:147910) $\mathsf{P}_s$ 的[演化方程](@entry_id:268137)来明确地看到这一点 。通过对动理学方程乘以 $m_s \mathbf{c}\mathbf{c}$ 并积分，可以得到 $\mathsf{P}_s$ 的精确演化方程，其一般形式为：

$$
\partial_t \mathsf{P}_s + \nabla\cdot\big(\mathbf{u}_s\mathsf{P}_s + \mathsf{Q}_s\big) + \mathsf{P}_s\cdot\nabla \mathbf{u}_s + \big(\mathsf{P}_s\cdot\nabla \mathbf{u}_s\big)^{\mathsf{T}} = \frac{q_s}{m_s}\Big[\mathsf{P}_s\times\mathbf{B} + \big(\mathsf{P}_s\times\mathbf{B}\big)^{\mathsf{T}}\Big] + \mathsf{C}_{P_s}
$$

在这个方程中，除了已知的低阶矩（$n_s, \mathbf{u}_s, \mathsf{P}_s$）外，还出现了一个新的、更高阶的量：$\mathsf{Q}_s \equiv m_s \int \mathbf{c}\mathbf{c}\mathbf{c} f_s d^3\mathbf{v}$，即三阶的**热流张量 (heat flux tensor)**。$\nabla \cdot \mathsf{Q}_s$ 这一项描述了由热流引起的压力变化。为了求解 $\mathsf{P}_s$，我们必须知道 $\mathsf{Q}_s$。然而，如果我们再去推导 $\mathsf{Q}_s$ 的[演化方程](@entry_id:268137)，又会发现它依赖于四阶矩。这个无限的链条就是闭合问题的本质。

为了得到一个可解的流体模型，我们必须在某个阶次上截断这个等级链，并通过一个**闭合关系 (closure relation)** 来近似地表达最高阶的矩。这个闭合关系将未知的最[高阶矩](@entry_id:266936)表示为已知低阶矩的函数。例如，一个简单的闭合是绝热假设 $p \propto n^\gamma$，它隐式地忽略了热流。

#### 闭合关系示例：各向异性热流

更复杂的闭合关系可以从动理学理论中推导出来。例如，我们可以通过求解[动理学方程](@entry_id:751029)的微扰来为热流寻找一个表达式。在磁化碰撞等离子体中，**Chapman-Enskog 展开**方法是一种强大的技术，它利用[碰撞时间](@entry_id:261390)远小于宏观演化时间的假设，系统地推导输运系数 。

当这个方法应用于热流的计算时，它给出了一个依赖于温度梯度的闭合关系，即著名的**Braginskii 热流 (Braginskii heat flux)**：

$$
\mathbf{q}_s = -\kappa_{\parallel s}\nabla_{\parallel}T_s - \kappa_{\perp s}\nabla_{\perp}T_s - \kappa_{\wedge s}\hat{\mathbf{b}}\times\nabla T_s
$$

其中 $\mathbf{q}_s$ 是热流矢量（热流张量 $\mathsf{Q}_s$ 的迹缩并形式）。这个表达式表明，热流不仅与温度梯度平行，还包含垂直于磁场和温度梯度的分量。三个[输运系数](@entry_id:136790)的物理意义如下：
-   $\kappa_\parallel$：**[平行热导率](@entry_id:1129319)**，描述沿磁[场线](@entry_id:172226)的[热传导](@entry_id:143509)。由于粒子可以沿磁场自由运动，这个系数通常很大。
-   $\kappa_\perp$：**垂直热导率**，描述垂直于磁场线的[热传导](@entry_id:143509)。由于粒子被限制在围绕磁力线的回旋轨道上，跨越磁力线的输运需要通过碰撞来完成，因此这个系数被强磁场大大抑制。
-   $\kappa_\wedge$：**Righi-Leduc 热导率**，描述一个既垂直于磁场又垂直于温度梯度的热流。

这些系数的尺度依赖于**磁化参数 (magnetization parameter)** $\Omega_s \tau_s$，即[回旋频率](@entry_id:156231)与[碰撞时间](@entry_id:261390)的比值。对于强磁化等离子体 ($\Omega_s \tau_s \gg 1$)，我们有如下尺度关系 ：
$$
\kappa_{\perp s} \sim \frac{\kappa_{\parallel s}}{(\Omega_s \tau_s)^2}, \qquad \kappa_{\wedge s} \sim \frac{\kappa_{\parallel s}}{\Omega_s \tau_s}
$$
这清晰地展示了宏观流体模型的输运系数是如何由底层的微观动理学过程决定的。选择或推导合适的闭合关系，是构建准确、可靠的等离子体[计算模型](@entry_id:637456)的关键所在。