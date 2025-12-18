## 引言
[湍流](@entry_id:151300)动态能量（TKE）收支是理解地球物理流体中[湍流生成](@entry_id:189980)、维持和衰亡的核心理论框架。从微尺度的空气运动到全球尺度的气候系统，能量在平均流动和[湍流](@entry_id:151300)脉动之间的转换无处不在，而准确量化这一过程对于发展可靠的[数值天气预报](@entry_id:191656)和气候模型至关重要。本文旨在系统性地解决一个根本问题：[湍流](@entry_id:151300)的能量从何而来，又去往何处？通过建立并剖析TKE收支方程，我们得以揭示驱动[湍流](@entry_id:151300)的复杂物理机制。

在接下来的内容中，我们将踏上一段从理论到实践的探索之旅。在“原理与机制”一章，我们将从基本定义出发，推导TKE收支方程，并深入分析切变、[浮力](@entry_id:154088)、输运和耗散等关键过程的物理意义。随后，在“应用与交叉学科联系”一章，我们将展示TKE收支原理如何被应用于诊断不同的[大气边界层](@entry_id:1121182)状态、分析天气现象以及连接大气与海洋科学。最后，“实践练习”部分将通过具体问题，帮助您巩固所学知识，并将其应用于实际分析中。通过本次学习，您将能够掌握分析和[参数化](@entry_id:265163)[湍流](@entry_id:151300)能量学的基本工具。

## 原理与机制

在本章中，我们将深入探讨[湍流理论](@entry_id:264896)的核心概念之一：**[湍流](@entry_id:151300)动态能量（Turbulent Kinetic Energy, TKE）收支**。理解TKE的来源、去向和输运机制，对于在[数值天气预报](@entry_id:191656)和气候模型中准确地[参数化](@entry_id:265163)行星边界层（PBL）及其他[湍流](@entry_id:151300)现象至关重要。我们将从基本定义出发，系统地构建TKE收支方程，并逐一剖析其中每一项的物理意义和行为特征。

### 动能的基本分解

在研究[湍流](@entry_id:151300)时，我们通常将瞬时物理量分解为平均[部分和](@entry_id:162077)脉动部分。对于速度场 $\boldsymbol{u}$，**[雷诺分解](@entry_id:267756)（Reynolds decomposition）**将其表示为：
$$
u_i = \overline{U_i} + u_i'
$$
其中 $\overline{U_i}$ 是[平均速度](@entry_id:267649)，而 $u_i'$ 是围绕平均值的脉动速度。根据定义，脉动量的平均值为零，即 $\overline{u_i'} = 0$。

流体的比动能（单位质量的动能）定义为 $E = \frac{1}{2} u_i u_i$。为了理解[湍流](@entry_id:151300)如何影响系统的总能量，我们对 $E$ 进行平均，得到平均比动能 $\overline{E}$：
$$
\overline{E} = \overline{\frac{1}{2} u_i u_i} = \frac{1}{2} \overline{(\overline{U_i} + u_i')(\overline{U_i} + u_i')}
$$
展开并利用[平均算子](@entry_id:746605)的线性性质，我们得到：
$$
\overline{E} = \frac{1}{2} \left( \overline{\overline{U_i}\overline{U_i}} + 2\overline{\overline{U_i}u_i'} + \overline{u_i'u_i'} \right)
$$
根据雷诺平均的性质，平均量的平均是其自身，且 $\overline{u_i'}=0$，因此中间的交叉项 $\overline{\overline{U_i}u_i'} = \overline{U_i}\overline{u_i'} = 0$。这样，平均比动能被清晰地分解为两个部分 ：
$$
\overline{E} = \frac{1}{2}\overline{U_i}\overline{U_i} + \frac{1}{2}\overline{u_i'u_i'}
$$
这个表达式揭示了一个基本事实：流体的总平均动能由两部分构成。第一部分是**[平均动能](@entry_id:146353)（Mean Kinetic Energy, MKE）**，定义为 $K = \frac{1}{2}\overline{U_i}\overline{U_i}$，它代表了平均流动的能量。第二部分是**[湍流](@entry_id:151300)动态能量（Turbulent Kinetic Energy, TKE）**，定义为 $k = \frac{1}{2}\overline{u_i'u_i'}$，它代表了[湍流](@entry_id:151300)脉动自身的平均能量。因此，我们有 $\overline{E} = K + k$。TKE是衡量[湍流强度](@entry_id:1133493)的核心指标，我们的目标就是建立一个描述 $k$ 如何随时间演变的收支方程。

### [湍流](@entry_id:151300)动态[能量收支](@entry_id:201027)方程

TKE收支方程是通过对[动量方程](@entry_id:197225)进行一系列数学操作（特别是乘以脉动速度并求平均）推导出来的。对于一个考虑了密度变化（如垂直分层）和湿度的可压缩大气流，一个常用且形式简洁的TKE收支方程是在**[非弹性近似](@entry_id:1121006)（anelastic approximation）**下得到的。对于单位体积的TKE，即 $\rho_0 k$（其中 $\rho_0(z)$ 是背景密度），其完整的收支方程可以写为 ：
$$
\frac{\partial(\rho_0 k)}{\partial t} + \frac{\partial(\rho_0 \overline{u_j} k)}{\partial x_j} = P_s + P_b + T - \rho_0 \epsilon
$$
该方程表明，TKE的局地变化（左侧第一项）和被平均流平流输运的变化（左侧第二项）之和，由以下几个物理过程共同决定：
- **$P_s$：切变产生项 (Shear Production)**，代表TKE通过平均风速切变产生的过程。
- **$P_b$：[浮力](@entry_id:154088)产生项 (Buoyancy Production)**，代表TKE由于[浮力](@entry_id:154088)作用产生或耗散的过程。
- **$T$：输运项 (Transport)**，描述TKE在空间上的重新分布，包括[湍流](@entry_id:151300)自身输运和压力输运。
- **$\rho_0 \epsilon$：耗散项 (Dissipation)**，代表TKE由于分子粘性作用转化为内能的不可逆过程。

下面，我们将详细探讨每一个项的物理机制。

### TKE的产生与耗散机制

#### 切变产生项 ($P_s$)：[湍流](@entry_id:151300)的力学引擎

**切变产生项**是TKE最主要的力学来源，它描述了平均流的动能如何通过[湍流](@entry_id:151300)应力的作用转化为[湍流](@entry_id:151300)动态能量。其数学表达式为：
$$
P_s = -\rho_0 \overline{u_i' u_j'} \frac{\partial \overline{U_i}}{\partial x_j}
$$
这里的 $\overline{u_i' u_j'}$ 是**[雷诺应力张量](@entry_id:270803)**，它代表了[湍流](@entry_id:151300)脉动引起的动量输运。$P_s$ 的物理意义是[雷诺应力](@entry_id:263788)对平均速度梯度所做的功。

为了更深入地理解这一过程，我们可以将平均[速度梯度张量](@entry_id:270928) $\frac{\partial \overline{U_i}}{\partial x_j}$ 分解为一个对称[部分和](@entry_id:162077)一个反对称部分 ：
- **平均[应变率张量](@entry_id:266108) (Mean Strain-Rate Tensor)**: $S_{ij} = \frac{1}{2}\left(\frac{\partial \overline{U_i}}{\partial x_j} + \frac{\partial \overline{U_j}}{\partial x_i}\right)$，描述了流体微团的变形。
- **平均旋转率张量 (Mean Rotation-Rate Tensor)**: $R_{ij} = \frac{1}{2}\left(\frac{\partial \overline{U_i}}{\partial x_j} - \frac{\partial \overline{U_j}}{\partial x_i}\right)$，描述了流体微团的刚性旋转。

由于雷诺应力张量 $\overline{u_i' u_j'}$ 是对称的（因为 $u_i'u_j' = u_j'u_i'$），它与反对称的旋转率张量 $R_{ij}$ 的缩并（contraction）恒为零，即 $\overline{u_i' u_j'} R_{ij} = 0$。这意味着，平均流的刚性旋转并不能产生TKE。TKE的产生完全来自于[雷诺应力](@entry_id:263788)与平均[应变率](@entry_id:154778)的相互作用：
$$
P_s = -\rho_0 \overline{u_i' u_j'} S_{ij}
$$
在大气边界层中，最常见的[湍流](@entry_id:151300)产生源是垂直风切变。例如，在一个水平均匀的边界层中，平均风速 $\overline{U}$ 随高度 $z$ 增加（$\frac{\partial \overline{U}}{\partial z} > 0$），$P_s$ 的主要贡献来自于 $-\rho_0 \overline{u'w'} \frac{\partial \overline{U}}{\partial z}$。通常，[湍流](@entry_id:151300)会将高处的快速气流向下输运，将低处的慢速气流向上输运，这导致了向下的[动量通量](@entry_id:199796)，即 $\overline{u'w'}  0$。这种**顺梯度输运（downgradient transport）**使得 $P_s > 0$，[湍流](@entry_id:151300)得以从平均风切变中汲取能量 。

然而，$P_s$ 并非总是正的。在某些非平衡的大气流动中，[湍流](@entry_id:151300)应力可能与局地平均切变反向，即发生**逆梯度输运（counter-gradient transport）**。例如，在夜间低空急流[急流核](@entry_id:1126824)的上方，风速随高度减小（$\frac{\partial \overline{U}}{\partial z}  0$），但由于下方[湍流](@entry_id:151300)的非局地输运效应，[动量通量](@entry_id:199796) $\overline{u'w'}$ 可能仍然为负。在这种情况下，$P_s \approx -\overline{u'w'} \frac{\partial \overline{U}}{\partial z}$ 就会变为负值。这意味着[湍流](@entry_id:151300)正在消耗自身能量来加速平均流，对平均流做功。类似的情况也可能出现在风向随高度剧烈变化的埃克曼（Ekman）层中 。

#### [浮力](@entry_id:154088)产生项 ($P_b$)：层结状态的角色

**[浮力](@entry_id:154088)产生项**描述了[浮力](@entry_id:154088)对TKE的贡献，其作用方向取决于大气的热力层结状态。在考虑湿空气时，我们必须使用[虚位温](@entry_id:1133825) $\theta_v$ 来恰当地表示空气包裹的[浮力](@entry_id:154088)。该项的表达式为 ：
$$
P_b = \rho_0 \frac{g}{\overline{\theta_v}} \overline{w'\theta_v'}
$$
其中 $g$ 是重力加速度，$\overline{w'\theta_v'}$ 是[湍流](@entry_id:151300)虚热通量。

[浮力](@entry_id:154088)项的符号直接与大气稳定度相关 ：
- **不稳定层结 ($\partial \overline{\theta_v}/\partial z  0$)**: 在这种情况下，暖湿空气位于冷干空气下方。[湍流](@entry_id:151300)运动（例如热泡上升，$w' > 0, \theta_v' > 0$）会产生向上的热通量，即 $\overline{w'\theta_v'} > 0$。这导致 $P_b > 0$，[浮力](@entry_id:154088)做正功，将位能转化为TKE，从而增强[湍流](@entry_id:151300)。
- **稳定层结 ($\partial \overline{\theta_v}/\partial z > 0$)**: 在这种情况下，暖湿空气位于上方。一个被向上抬升的气块（$w' > 0$）会比周围环境更冷（$\theta_v'  0$），受到向下的恢复力。这导致向下的热通量，$\overline{w'\theta_v'}  0$。因此，$P_b  0$，[湍流](@entry_id:151300)需要消耗能量来克服负[浮力](@entry_id:154088)，TKE被转化为位能，[湍流](@entry_id:151300)受到抑制。
- **中性层结 ($\partial \overline{\theta_v}/\partial z = 0$)**: [浮力](@entry_id:154088)不起作用，$\overline{w'\theta_v'} = 0$，因此 $P_b = 0$。

为了量化[浮力](@entry_id:154088)和切变的相对重要性，我们引入一个[无量纲参数](@entry_id:169335)——**通量[理查森数](@entry_id:151448)（Flux Richardson Number, $Ri_f$）**：
$$
Ri_f = -\frac{P_b}{P_s}
$$
$Ri_f$ 的符号反映了层结状态：不稳定时为负，稳定时为正，中性时为零。在稳定层结中，当 $Ri_f$ 超过一个临界值（通常在 $0.2-0.25$ 左右）时，[浮力](@entry_id:154088)耗散TKE的速率超过了切变产生的速率，[湍流](@entry_id:151300)将无法维持并最终衰亡 。

#### 粘性耗散项 ($\epsilon$)：能量的最终归宿

无论TKE如何产生和输运，其最终的命运都是通过分子粘性作用转化为分子的无序热运动，即内能。这个不可逆的过程由**粘性耗散率** $\epsilon$ 来描述。从[Navier-Stokes](@entry_id:276387)方程出发，可以严格推导出 $\epsilon$ 的表达式 ：
$$
\epsilon = \nu \overline{\left(\frac{\partial u_i'}{\partial x_j}\right)\left(\frac{\partial u_i'}{\partial x_j}\right)}
$$
其中 $\nu$ 是运动粘性系数。由于 $\nu$ 是正的，且括号内的项是速度梯度脉动平方和的平均，它必然是非负的。因此，$\epsilon \ge 0$。在TKE收支方程中，它以 $-\rho_0 \epsilon$ 的形式出现，表明它永远是TKE的一个**汇**。

这一过程与著名的**[湍流能量级串](@entry_id:194234)（energy cascade）**理论紧密相关。TKE通常在与平均流尺度相当的大尺度涡旋上由切变和[浮力](@entry_id:154088)产生。然后，通过[非线性](@entry_id:637147)的涡旋-涡旋相互作用，能量被逐级传递到越来越小的尺度，而总能量在这一传递过程（[惯性子区](@entry_id:273327)）中几乎是守恒的。最终，当能量到达一个足够小的尺度——**柯尔莫哥洛夫微尺度（Kolmogorov microscale）**——时，[速度梯度](@entry_id:261686)变得非常大，粘性力变得足够强，从而有效地将[动能耗散](@entry_id:751026)为热能。

### TKE的输运与平衡

#### [湍流](@entry_id:151300)输运项 ($T$)：TKE的空间再分配

TKE收支方程中的**输运项** $T$ 本身并不产生或消灭TKE，而是将其从一个地方输运到另一个地方。它通常以[散度形式](@entry_id:748608)出现，其表达式为  ：
$$
T = -\frac{\partial}{\partial x_j} \left( \rho_0 \overline{k' u_j'} + \overline{p' u_j'} \right)
$$
括号内的第一项 $\rho_0 \overline{k' u_j'}$ 是由速度脉动自身引起的三阶相关项，称为**湍流通量**。第二项 $\overline{p' u_j'}$ 是压力脉动与速度脉动相关引起的**压力通量**。

在许多大气边界层的情境中，输运项非常重要。例如，在对流边界层中，TKE在近地面由切变产生，并通过强烈的上升气流向上输运，在边界层顶部则通过夹带过程消耗TKE。因此，在这些区域，输运项的散度不可忽略。

然而，在某些理想化条件下，我们可以忽略输运项，从而大大简化TKE收支方程。这一简化的关键假设是**局地平衡（local equilibrium）**。该假设在以下条件下近似成立 ：
1.  流动是**准[稳态](@entry_id:139253)**的，即TKE不随时间显著变化（$\frac{\partial k}{\partial t} \approx 0$）。
2.  流动是**水平均匀**的。
3.  我们关注的是远离地表和边界层顶夹带区的**边界层内部**区域。

在这些区域，TKE的垂直廓线 $k(z)$ 往往是近似均匀的，即 $\frac{\partial k}{\partial z} \approx 0$。由于[湍流通量](@entry_id:1133513)通常可以被模型化为与TKE梯度成正比（梯度扩散假设），平坦的TKE廓线意味着[湍流通量](@entry_id:1133513)本身很小，其散度（即输运项）也就可以忽略不计了。

#### 平衡假设与大气边界层[标度律](@entry_id:266186)

局地平衡假设是一个非常有用的工具。在中性、水平均匀的近地面层中，[浮力](@entry_id:154088)项为零，输运项可忽略，TKE收支方程简化为一个简单的平衡关系 ：
$$
P_s \approx \rho_0 \epsilon
$$
即，切变产生的TKE速率约等于粘性耗散的速率。

利用这一关系，我们可以推导出[耗散率](@entry_id:748577)的重要[标度律](@entry_id:266186)。在中性近地面层，**莫宁-奥布霍夫[相似理论](@entry_id:262184)（Monin-Obukhov Similarity Theory, MOST）**告诉我们风切变为 $\frac{\partial \overline{U}}{\partial z} = \frac{u_*}{\kappa z}$，其中 $u_*$ 是[摩擦速度](@entry_id:267882)（定义为 $u_*^2 = -\overline{u'w'}$），$\kappa$ 是[冯·卡门常数](@entry_id:261117)。将这些关系代入切变产生项的表达式：
$$
P_s = -\rho_0 \overline{u'w'} \frac{\partial \overline{U}}{\partial z} = \rho_0 u_*^2 \left(\frac{u_*}{\kappa z}\right) = \frac{\rho_0 u_*^3}{\kappa z}
$$
根据局地平衡，$P_s \approx \rho_0 \epsilon$，我们得到耗散率的[标度律](@entry_id:266186)：
$$
\epsilon \approx \frac{u_*^3}{\kappa z}
$$
这个结果意义非凡，因为它将宏观、可测量的平均流参数（如摩擦速度 $u_*$ 和离地高度 $z$）与微观、难以直接测量的[耗散率](@entry_id:748577) $\epsilon$ 联系起来，为边界层[参数化](@entry_id:265163)方案提供了坚实的理论基础 。

### 针对可压缩流的扩展

#### 法弗平均 (Favre Averaging)

当处理密度变化显著的[可压缩流](@entry_id:747589)动（如[深对流](@entry_id:1123472)或含有强重力波的流动）时，标准的雷诺平均会带来麻烦。例如，在动量方程的平流项 $\rho u_i u_j$ 中，雷诺平均会产生大量复杂的、包含密度脉动 $\rho'$ 的高阶相关项（如 $\overline{\rho'u_i'u_j'}$），使得[湍流](@entry_id:151300)闭合问题异常困难 。

为了解决这个问题，我们引入**法弗平均（Favre averaging）**或**质量加权平均（mass-weighted averaging）**。对于任意变量 $\phi$，其法弗平均 $\tilde{\phi}$ 定义为：
$$
\tilde{\phi} = \frac{\overline{\rho \phi}}{\overline{\rho}}
$$
相应的脉动量定义为 $\phi'' = \phi - \tilde{\phi}$。法弗平均的一个关键性质是 $\overline{\rho \phi''} = 0$。通过使用法弗平均，[守恒方程](@entry_id:1122898)（如质量和动量守恒）的平均形式变得异常简洁，其形式与不可压缩方程更为相似。例如，平均后的[连续性方程](@entry_id:195013)就是 $\partial_t \overline{\rho} + \partial_j(\overline{\rho}\tilde{u_j}) = 0$，没有显式的[湍流](@entry_id:151300)质量通量项。这极大地简化了[湍流](@entry_id:151300)模式的构建，因此在现代可压缩大气模型中被广泛采用 。

#### 压力-膨胀项与科里奥利力

在[可压缩流](@entry_id:747589)的TKE收支方程中，会出现一些在[不可压缩流](@entry_id:140301)中不存在的项。其中最重要的是**压力-膨胀项（pressure-dilatation term）**，写作 $-\overline{p' \nabla \cdot \boldsymbol{u}'}$。它代表了压力脉动对流体微团体积变化所做的功，是TKE与内能之间的一种**可逆**交换渠道 。在[湍流马赫数](@entry_id:756236)很低且流动主要由内重力波主导的稳定层结大气中，压力脉动 $p'$ 与[速度散度](@entry_id:264117)脉动 $\nabla \cdot \boldsymbol{u}'$ 之间存在近乎 $90^\circ$ 的相位差（[正交关系](@entry_id:145540)）。这导致它们的平均乘积 $\overline{p' \nabla \cdot \boldsymbol{u}'}$ 接近于零，因此该项的贡献通常很小 。

最后，值得重申的是，**科里奥利力**对流动（无论是平均流还是[脉动流](@entry_id:191445)）不做功。这是因为科里奥利力始终垂直于速度矢量。因此，它不会直接作为源或汇出现在平均动能或[湍流](@entry_id:151300)动态能量的收支方程中。然而，它通过改变流动的轨迹和影响[雷诺应力张量](@entry_id:270803)的分量，间接地影响TKE的产生和分布 。