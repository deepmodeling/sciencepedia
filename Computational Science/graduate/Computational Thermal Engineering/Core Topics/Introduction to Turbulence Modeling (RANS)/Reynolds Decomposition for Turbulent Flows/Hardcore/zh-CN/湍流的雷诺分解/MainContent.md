## 引言
[湍流](@entry_id:151300)，作为一种本质上混乱且不规则的流动现象，为科学研究与工程实践带来了巨大的挑战。直接求解描述其瞬时运动的[纳维-斯托克斯方程](@entry_id:142275)在计算上极为昂贵，对于大多数应用而言不切实际。因此，我们迫切需要一个系统性的方法，来从复杂的脉动中提取出具有统计意义的平均流动特性，并理解这些平均量所遵循的物理规律。[雷诺分解](@entry_id:267756)正是为解决这一核心问题而生的奠基性理论框架，它为我们分析、建模和预测[湍流](@entry_id:151300)提供了第一把钥匙。

本文旨在全面而深入地探讨[雷诺分解](@entry_id:267756)。在接下来的内容中，我们将分三步展开：首先，在“原理与机制”一章中，我们将深入[雷诺分解](@entry_id:267756)的数学基础，理解[雷诺应力](@entry_id:263788)的由来以及它所引出的著名的“[湍流封闭问题](@entry_id:268973)”，并探讨[湍流](@entry_id:151300)能量传递的关键物理过程。接着，在“应用与跨学科连接”一章中，我们将展示这一理论如何在[计算流体动力学](@entry_id:142614)（CFD）、[环境科学](@entry_id:187998)乃至等离子体物理等不同领域中发挥关键作用，连接起理论与现实世界的复杂现象。最后，“动手实践”部分将提供具体的练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一结构化的学习路径，读者将能够系统地掌握[雷诺分解](@entry_id:267756)的精髓，从基本概念到前沿应用。

## 原理与机制

在对[湍流](@entry_id:151300)这一本质上混乱且不规则的现象进行数学描述时，我们面临一个核心挑战：瞬时场变量（如速度和压力）在空间和时间上都表现出随机、多尺度的波动，直接求解这些变量的控制方程（即[纳维-斯托克斯方程](@entry_id:142275)）在计算上极其昂贵，对于大多数工程应用而言不切实际。因此，我们需要一种系统性的方法来提取出我们更感兴趣的统计平均量，并推导出这些平均量所遵循的控制方程。[雷诺分解](@entry_id:267756)与平均正是实现这一目标奠基性的理论框架。本章将深入探讨[雷诺分解](@entry_id:267756)的基本原理、其在流体动量和[标量输运方程](@entry_id:1131253)中的应用，以及由此产生的关键物理机制和核心建模挑战。

### 基础：[雷诺分解](@entry_id:267756)与平均

分析[湍流](@entry_id:151300)的第一步是将任何瞬时流动变量 $f(\mathbf{x}, t)$ 分解为一个**平均部分**（mean part）和一个**脉动部分**（fluctuating part）。这种方法被称为**[雷诺分解](@entry_id:267756)**（Reynolds decomposition），其数学表达式为：

$f(\mathbf{x}, t) = \overline{f}(\mathbf{x}) + f'(\mathbf{x}, t)$

在这里，$\overline{f}(\mathbf{x})$ 是在空间点 $\mathbf{x}$ 处的平均值，对于统计[定常流](@entry_id:191654)（statistically stationary flow），该平均值不随时间变化。脉动部分 $f'(\mathbf{x}, t)$ 则是瞬时值与平均值的偏差。

为了使这种分解有效，我们必须明确定义**平均算符**（averaging operator）$\overline{(\cdot)}$ 的性质。在理论分析中，这个算符通常指**系综平均**（ensemble average），即对大量相同宏观条件下流动实验（或实现）的集合进行平均。对于满足**遍历性**（ergodicity）的统计[定常流](@entry_id:191654)，系综平均等价于**[时间平均](@entry_id:267915)**（time average），后者在实验测量和计算中更为常用。无论采用哪种定义，该平均算符都必须满足以下几个基本运算法则 ：

1.  **线性**（Linearity）：对于任意两个场 $a$ 和 $b$ 以及常数 $c$，有 $\overline{a+b} = \overline{a} + \overline{b}$ 和 $\overline{ca} = c\overline{a}$。
2.  **[幂等性](@entry_id:190768)**（Idempotency）：对一个已经平均过的量再次平均，其值不变，即 $\overline{\overline{f}} = \overline{f}$。这也适用于常数，$\overline{c} = c$。

由[雷诺分解](@entry_id:267756)的定义和平均算符的性质，我们可以立即推导出一个至关重要的结论：**任何脉动量的平均值为零**  。我们可以通过对分解式 $f = \overline{f} + f'$ 两边取平均来证明：

$\overline{f} = \overline{(\overline{f} + f')} = \overline{\overline{f}} + \overline{f'}$

根据[幂等性](@entry_id:190768)，$\overline{\overline{f}} = \overline{f}$，因此上式简化为：

$\overline{f} = \overline{f} + \overline{f'}$

这意味着 $\overline{f'} = 0$。

然而，当涉及到乘积的平均时，情况就变得复杂了。对两个场 $a$ 和 $b$ 的乘积 $ab$ 取平均，结果并**不等于**它们各自平均值的乘积。让我们代入[雷诺分解](@entry_id:267756) $a = \overline{a} + a'$ 和 $b = \overline{b} + b'$：

$\overline{ab} = \overline{(\overline{a} + a')(\overline{b} + b')} = \overline{\overline{a}\overline{b} + \overline{a}b' + a'\overline{b} + a'b'}$

利用线性和 $\overline{f'} = 0$ 的性质，上式变为：

$\overline{ab} = \overline{a}\overline{b} + \overline{a'b'}$

这个结果是湍流理论的核心。它表明，一个乘积项的平均值等于平均值之积，外加一个**脉动量相关项**（correlation term）$\overline{a'b'}$。在[湍流](@entry_id:151300)中，不同物理量（甚至同一物理量的不同分量）的脉动通常是相关的，因此 $\overline{a'b'}$ 一般不为零。正是这一项的出现，导致了湍流建模中著名的“封闭问题”，我们将在后续章节中详细探讨。例如，当我们考虑总对流热通量 $\overline{u_i T}$ 时，它会分解为由平均运动引起的输运 $\overline{u_i}\overline{T}$ 和由[湍流](@entry_id:151300)脉动引起的输运 $\overline{u_i'T'}$ 。后者被称为**[湍流热通量](@entry_id:151024)**（turbulent heat flux），是[湍流](@entry_id:151300)增强热量混合的关键机制。

### 平均算符的[交换性](@entry_id:140240)质

在推导平均流控制方程时，一个关键步骤是将平均算符应用于包含导数的项。这要求我们审视平均算符与[微分](@entry_id:158422)算符是否可以交换顺序。这个问题的答案取决于平均算符的具体定义和流动的物理特性 。

对于**系综平均** $\langle \cdot \rangle$，由于平均操作是在所有可能的流动“实现”构成的[样本空间](@entry_id:275301)上进行的，而[微分](@entry_id:158422)操作是在时空坐标上进行的，两者作用于独立的变量。因此，在满足足够[光滑性](@entry_id:634843)的条件下，系综平均与时间和空间[微分](@entry_id:158422)算符总是可以交换的 。例如：

$\langle \nabla \cdot \mathbf{u} \rangle = \nabla \cdot \langle \mathbf{u} \rangle$ 和 $\langle \nabla^2 \phi \rangle = \nabla^2 \langle \phi \rangle$

对于在统计[定常流](@entry_id:191654)中定义的**[时间平均](@entry_id:267915)**，情况稍有不同。[时间平均](@entry_id:267915)算符与**空间导数**可以交换，因为积分变量（时间）和[微分](@entry_id:158422)变量（空间）是独立的 。即：

$\overline{\frac{\partial f}{\partial x_i}} = \frac{\partial \overline{f}}{\partial x_i}$

然而，[时间平均](@entry_id:267915)与**时间导数**的交换则需要特别注意。在统计[定常流](@entry_id:191654)中，任何物理量的平均值 $\overline{f}$ 根据定义不随时间变化，因此 $\frac{\partial \overline{f}}{\partial t} = 0$。另一方面，对时间导数取平均：

$\overline{\frac{\partial f}{\partial t}} = \lim_{\mathcal{T}\to\infty} \frac{1}{\mathcal{T}} \int_{0}^{\mathcal{T}} \frac{\partial f}{\partial t} dt = \lim_{\mathcal{T}\to\infty} \frac{f(\mathcal{T}) - f(0)}{\mathcal{T}}$

由于在有物理意义的[湍流](@entry_id:151300)中，物理量 $f$ 的值是有界的（不会随时间无限增长），上述极限为零。因此，在统计[定常流](@entry_id:191654)中，[时间平均](@entry_id:267915)算符与时间导数确实可以交换，因为等式两边都等于零 。

类似的[交换律](@entry_id:141214)也适用于**[空间平均](@entry_id:203499)**。例如，在一个沿 $x$ 方向具有周期性的通道流中，对 $x$ 方向的[空间平均](@entry_id:203499)与对 $x$ 的偏导数也可以交换，因为在周期性边界条件下，积分后的结果同样为零 。

需要强调的是，并非所有类型的平均或滤波算符都具有这种良好的[交换性](@entry_id:140240)质。例如，在[大涡模拟](@entry_id:153702)（Large-Eddy Simulation, LES）中使用的[空间滤波器](@entry_id:1132038)，如果其滤波核函数依赖于空间位置（例如在[近壁区](@entry_id:1128462)变化的滤波宽度），则滤波操作与[微分](@entry_id:158422)操作通常不可交换，其差值会产生一个必须处理的“交换误差项” 。

### 未封闭项的出现：封闭问题

现在，我们将[雷诺分解](@entry_id:267756)应用于不可压缩流体的[纳维-斯托克斯方程](@entry_id:142275)，以揭示[湍流建模](@entry_id:151192)的核心困难。动量方程中的**[非线性](@entry_id:637147)对流项** $(\mathbf{u} \cdot \nabla)\mathbf{u}$ 或其等价的[散度形式](@entry_id:748608) $\nabla \cdot (\mathbf{u}\mathbf{u})$ 是问题的根源 。

让我们对 $\nabla \cdot (\mathbf{u}\mathbf{u})$ 应用雷诺平均。以[张量表示法](@entry_id:272140)，我们关注 $u_i u_j$ 这一项：

$\overline{u_i u_j} = \overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{\overline{u_i}\overline{u_j} + \overline{u_i}u_j' + u_i'\overline{u_j} + u_i'u_j'}$

应用平均法则后，我们得到：

$\overline{u_i u_j} = \overline{u_i}\overline{u_j} + \overline{u_i'u_j'}$

将此结果代入经过平均的[动量方程](@entry_id:197225)，我们得到**雷诺平均纳维-斯托克斯（RANS）方程**（Reynolds-Averaged Navier-Stokes equations）：

$\frac{\partial \overline{u_i}}{\partial t} + \overline{u_j} \frac{\partial \overline{u_i}}{\partial x_j} = -\frac{1}{\rho}\frac{\partial \overline{p}}{\partial x_i} + \nu \frac{\partial^2 \overline{u_i}}{\partial x_j \partial x_j} - \frac{\partial (\overline{u_i'u_j'})}{\partial x_j}$

与瞬时[纳维-斯托克斯方程](@entry_id:142275)相比，RANS 方程在形式上非常相似，但出现了一个新的项：$-\frac{\partial (\overline{u_i'u_j'})}{\partial x_j}$。这个新项源于对[非线性](@entry_id:637147)对流项的平均，而非源于黏性项或压力项 。

该项中的[二阶相关](@entry_id:190427)张量 $\overline{u_i'u_j'}$ 是一个核心量。当乘以密度 $\rho$ 后，$\tau_{ij}^{(R)} = -\rho\overline{u_i'u_j'}$ 被称为**[雷诺应力张量](@entry_id:270803)**（Reynolds stress tensor）。从方程结构上看，它如同一个附加的应力作用于平均流场，代表了由速度脉动引起的平均动量输运 。

这里的关键问题是，张量 $\overline{u_i'u_j'}$ 是一个未知量。我们试图求解的 RANS 方程是关于[平均速度](@entry_id:267649) $\overline{u_i}$ 和平均压力 $\overline{p}$ 的方程，但方程本身却引入了新的未知数——[雷诺应力](@entry_id:263788)。在三维流动中，由于对称性，[雷诺应力张量](@entry_id:270803)有6个独立的未知分量。这使得方程组中的未知数数量超过了方程数量，系统因此是“不封闭的”。这个问题被称为**[湍流封闭问题](@entry_id:268973)**（turbulence closure problem），它是[湍流建模](@entry_id:151192)领域的中心任务：即如何通过建立雷诺应力与平均流场之间的关系（即“[湍流模型](@entry_id:190404)”）来封闭 RANS 方程组。

### [雷诺应力张量](@entry_id:270803)的性质与物理

[雷诺应力张量](@entry_id:270803)（为方便起见，我们常指其运动学形式 $R_{ij} = \overline{u_i'u_j'}$）不仅是数学上的未知数，更蕴含了[湍流](@entry_id:151300)脉动的丰富物理信息。它具有以下重要的数学和物理性质：

1.  **对称性**（Symmetry）：根据其定义 $R_{ij} = \overline{u_i'u_j'}$，由于[标量乘法](@entry_id:155971)是可交换的（$u_i'u_j' = u_j'u_i'$），显然有 $R_{ij} = R_{ji}$。因此，[雷诺应力张量](@entry_id:270803)是一个对称[二阶张量](@entry_id:199780) 。

2.  **正定性**（Positive-definiteness）：更准确地说是[半正定性](@entry_id:147720)。对于任意非零实向量 $\mathbf{a}$，二次型 $a_i R_{ij} a_j$ 总是非负的。证明如下 ：
    $a_i R_{ij} a_j = a_i \overline{u_i'u_j'} a_j = \overline{(a_i u_i')(a_j u_j')}$
    令 $s = a_i u_i' = \mathbf{a} \cdot \mathbf{u}'$ 是一个标量，则上式变为 $\overline{s^2}$。由于 $s$ 是实数，其平方 $s^2$ 必然非负，一个非负量的平均值也必然非负。因此 $a_i R_{ij} a_j \ge 0$。该性质的物理意义是，沿任意方向的速度脉动方差（即 $R_{ij}$ 的对角元）都是非负的。

3.  **坐标系无关性（客观性）**（Frame-Invariance/Objectivity）：雷诺应力张量是一个客观的物理量，其性质不应依赖于观察者的参考系。在**伽利略变换**（即叠加一个恒定的平移速度）下，速度脉动本身不变，因此 $R_{ij}$ 也不变。在**刚性旋转**下，$R_{ij}$ 遵循标准的二阶[张量变换法则](@entry_id:185176)。这意味着由 $R_{ij}$ 构成的[标量不变量](@entry_id:193787)（如迹、行列式等）是独立于参考系的，具有普适的物理意义 。

最重要的一个不变量是 $R_{ij}$ 的迹。**[湍动能](@entry_id:262712)**（Turbulent Kinetic Energy, TKE），用 $k$ 表示，定义为单位质量流体所具有的脉动动能，即：

$k \equiv \frac{1}{2} \overline{u_l' u_l'} = \frac{1}{2} (\overline{u_1'^2} + \overline{u_2'^2} + \overline{u_3'^2})$

而雷诺应力张量的迹为 $R_{ii} = \overline{u_i' u_i'} = \overline{u_1'^2} + \overline{u_2'^2} + \overline{u_3'^2}$。因此，我们得到了一个直接的联系  ：

$R_{ii} = 2k$

$k$ 是衡量湍流强度的核心指标，它概括了所有方向上速度脉动的总体能量。

### 能量级串：湍能的产生与耗散

[湍流](@entry_id:151300)的一个核心特征是能量从大尺度向小尺度的连续传递，最终在小尺度上因黏性作用而耗散，这一过程被称为**能量级串**（energy cascade）。雷诺平均方法为我们提供了洞察这一过程的数学工具。通过分别推导[平均动能](@entry_id:146353)（MKE）和湍动能（TKE）的[输运方程](@entry_id:174281)，我们可以清晰地看到能量在平均流和[脉动流](@entry_id:191445)之间的转换机制。

在 TKE 的[输运方程](@entry_id:174281)中，一个关键的源项是**[湍动能](@entry_id:262712)产生项**（production term），记为 $\mathcal{P}$：

$\mathcal{P} = - \overline{u_i'u_j'} \frac{\partial \overline{u_i}}{\partial x_j}$

这个项在[平均动能](@entry_id:146353)方程中以 $-\mathcal{P}$ 的形式出现，正好说明了它代表了平均流与[脉动流](@entry_id:191445)之间的能量交换 。其物理意义是，[雷诺应力](@entry_id:263788)在平均流的变形过程中所做的功。

为了更深入地理解 $\mathcal{P}$，我们可以将平均[速度梯度张量](@entry_id:270928) $\frac{\partial \overline{u_i}}{\partial x_j}$ 分解为一个对称部分（平均[应变率张量](@entry_id:266108) $S_{ij} = \frac{1}{2}(\frac{\partial \overline{u_i}}{\partial x_j} + \frac{\partial \overline{u_j}}{\partial x_i})$）和一个反对称部分（平均[旋转张量](@entry_id:191990)或[涡量张量](@entry_id:189621) $\Omega_{ij}$）。由于雷诺应力张量 $\overline{u_i'u_j'}$ 是对称的，而[对称张量与反对称张量](@entry_id:194720)的缩并结果恒为零，因此产生项可以被精确地写为 ：

$\mathcal{P} = - \overline{u_i'u_j'} S_{ij}$

这个重要的结果表明，**[湍动能](@entry_id:262712)的产生仅与平均流的应变（变形）有关，而与平均流的刚性旋转无关**。当流体微团在平均剪切作用下拉伸时，能量从平均流中被“抽取”出来，注入到[湍流](@entry_id:151300)脉动中，此时 $\mathcal{P} > 0$。

在某些特殊情况下，$\mathcal{P}$ 可以为零，例如在无平均应变的流动中（如[刚体](@entry_id:1131033)旋转）。在更复杂的流动中，例如急剧加速或具有稳定曲率的流动，雷诺应力与平均应变率的相对取向可能导致 $\mathcal{P} < 0$，这种现象称为**能量[逆散射](@entry_id:182338)**（backscatter），即能量从[湍流](@entry_id:151300)脉动反向传递给平均流 。值得注意的是，许多简单的[湍流模型](@entry_id:190404)（如基于 Boussinesq 假设的模型）假设[雷诺应力张量](@entry_id:270803)的[主轴](@entry_id:172691)与平均应变率张量的主轴对齐，但这只是一个模型假设，而非普遍的物理事实 。

### 向[标量输运](@entry_id:150360)的拓展：湍流热通量

[雷诺分解](@entry_id:267756)与平均的方法具有很好的普适性，它可以直接应用于任何由对流-扩散方程描述的[标量输运](@entry_id:150360)过程，例如热量或物质组分的输运。

考虑不可压缩流体中的[热能守恒](@entry_id:166461)方程。对其应用[雷诺分解](@entry_id:267756)（$T = \overline{T} + T'$, $u_j = \overline{u_j} + u_j'$）和平均算符，与动量方程完全类似，[非线性](@entry_id:637147)的对流项 $u_j \frac{\partial T}{\partial x_j}$ 在平均后会产生一个未封闭的相关项  。经过平均的[热能方程](@entry_id:1132993)如下：

$\frac{\partial \overline{T}}{\partial t} + \overline{u_j} \frac{\partial \overline{T}}{\partial x_j} = \alpha \frac{\partial^2 \overline{T}}{\partial x_j \partial x_j} - \frac{\partial (\overline{u_j'T'})}{\partial x_j}$

这里，$\alpha$ 是热扩散系数。方程中出现的新项是 $\overline{u_j'T'}$ 的散度。矢量 $\overline{\mathbf{u}'T'}$ 被称为**[湍流热通量](@entry_id:151024)**（kinematic turbulent heat flux），它代表了由速度和温度的协同脉动所引起的额外热量输运。与雷诺应力类似，这也是一个必须通过模型来封闭的未知量。这一类比深刻地揭示了[湍流](@entry_id:151300)的核心机制：脉动场通过[非线性](@entry_id:637147)相互作用，极大地增强了动量、热量和质量的宏观输运效率。

### 处理可变密度：法夫尔（质量加权）平均

标准的[雷诺平均](@entry_id:754341)在处理**密度可变**的流动时会遇到困难。这类流动在航空航天（高速[可压缩流](@entry_id:747589)）和能源工程（如燃烧，即使在[低马赫数](@entry_id:1127478)下，剧烈的温差也会导致显著的密度变化）中非常普遍 。

当密度 $\rho$ 也是一个波动的量（$\rho = \overline{\rho} + \rho'$）时，对[守恒形式](@entry_id:1122899)的动量方程中的 $\rho u_i u_j$ 项进行[雷诺平均](@entry_id:754341)，会产生极其复杂的[湍流](@entry_id:151300)相关项，例如 $\overline{\rho'u_i'u_j'}$ 和 $\overline{\rho'u_i'}$ 等，这使得封闭问题变得异常棘手 。

为了简化方程形式，Augustin-Louis Cauchy 和后来的 Anatol Roshko 与 Paul A. Libby 发展了**[法夫尔平均](@entry_id:198824)**（Favre averaging），或称**质量加权平均**（mass-weighted averaging）。对于任意场 $\phi$，其[法夫尔平均](@entry_id:198824)值 $\tilde{\phi}$ 定义为：

$\tilde{\phi} = \frac{\overline{\rho \phi}}{\overline{\rho}}$

相应的法夫尔脉动量定义为 $\phi'' = \phi - \tilde{\phi}$。这种定义的精妙之处在于，它使得质量加权的脉动平均为零：$\overline{\rho \phi''} = 0$ 。

使用[法夫尔平均](@entry_id:198824)的主要优势在于，它极大地简化了平均后的守恒方程。例如，平均[连续性方程](@entry_id:195013)可以精确地写为：

$\frac{\partial \overline{\rho}}{\partial t} + \nabla \cdot (\overline{\rho} \tilde{\mathbf{u}}) = 0$

这个方程在形式上与瞬时方程完全相同，并且不包含任何未封闭的[湍流](@entry_id:151300)项。类似地，[法夫尔平均](@entry_id:198824)后的动量和能量方程中的对流项也变得更为简洁，所有未封闭的[湍流](@entry_id:151300)相关项都以类似于不可压缩流动中[雷诺应力](@entry_id:263788)和[湍流通量](@entry_id:1133513)的形式出现（例如，法夫尔雷诺应力 $\overline{\rho u_i'' u_j''}$）。这使得为[不可压缩流](@entry_id:140301)发展的[湍流模型](@entry_id:190404)可以更容易地推广到[可压缩流](@entry_id:747589)中。

需要明确的是，当流体密度恒定时，[法夫尔平均](@entry_id:198824)与[雷诺平均](@entry_id:754341)是完[全等](@entry_id:273198)价的（$\tilde{\phi} = \overline{\phi}$） 。因此，[法夫尔平均](@entry_id:198824)可以被看作是[雷诺平均](@entry_id:754341)在[可变密度流](@entry_id:756427)中的一种自然推广。

### 更深的洞察：压力脉动的作用

在[湍流](@entry_id:151300)的动力学中，压力脉动 $p'$ 扮演着一个独特而关键的角色。要理解它的作用，我们需要考察[雷诺应力](@entry_id:263788) $R_{ij}$ 的精确[输运方程](@entry_id:174281)。在该方程中，存在一个与压力脉动相关的项，被称为**压力-应变相关项**（pressure-strain correlation），通常记为 $\phi_{ij}$ 或 $\Pi_{ij}$ ：

$\phi_{ij} = \frac{1}{\rho}\overline{p' \left( \frac{\partial u_i'}{\partial x_j} + \frac{\partial u_j'}{\partial x_i} \right)}$

对于不可压缩流动，这个张量具有两个至关重要的性质 ：
1.  它是**对称的**（$\phi_{ij} = \phi_{ji}$）。
2.  它的**迹为零**（$\phi_{ii} = 0$）。迹为零的性质源于脉动速度场的无散性（$\frac{\partial u_k'}{\partial x_k} = 0$）。

由于其迹为零，压力-应变项对总[湍动能](@entry_id:262712) $k$ 的收支没有贡献（其在 TKE 方程中的贡献为 $\frac{1}{2}\phi_{ii}=0$）。那么它的作用是什么呢？它的作用在于**重新分配**湍动能。具体来说，$\phi_{ij}$ 将能量在不同的法向[雷诺应力](@entry_id:263788)分量（$R_{11} = \overline{u_1'^2}$, $R_{22} = \overline{u_2'^2}$, $R_{33} = \overline{u_3'^2}$）之间进行传递，但保持它们的总和（即 $2k$）不变  。

这种能量的重新分配倾向于使[湍流](@entry_id:151300)变得更**各向同性**（isotropic）。如果某个方向的脉动能量过高（例如，在[剪切流](@entry_id:266817)中，主流方向的脉动通常最强），压力-应变项就会将该方向的能量转移到其他方向，这种机制被称为“**向各向同性的回归**”（return-to-isotropy） 。理解和模拟压力-应变项是高级[湍流模型](@entry_id:190404)（如[雷诺应力模型](@entry_id:198103)，RSM）的核心挑战之一，因为它与[湍流](@entry_id:151300)的非局部性（压[力场](@entry_id:147325)由泊松方程决定）和各向异性动力学直接相关 。