## 引言
在[大涡模拟](@entry_id:153702)（Large Eddy Simulation, LES）成为[计算流体力学](@entry_id:747620)和热工学领域不可或缺的高精度仿真工具的今天，对[湍流](@entry_id:151300)中未解析的小尺度运动进行精确建模，即亚格子尺度（Subgrid-Scale, SGS）建模，是决定仿真成败的核心环节。当我们将[控制流](@entry_id:273851)体运动的[Navier-Stokes](@entry_id:276387)方程进行空间滤波以分离大、小尺度时，会不可避免地产生一个未封闭的项——亚格子应力张量。这个项代表了所有小于计算网格尺度的湍[涡对](@entry_id:199153)我们能够解析的大尺度流动的集体效应。如何准确地为这一项建立模型，构成了LES理论与实践中的核心知识缺口。

本文旨在为读者提供一个关于亚格子尺度建模的全面而深入的指南。我们将系统地梳理从经典到前沿的各类[SGS模型](@entry_id:754720)，剖析其背后的物理思想与数学构造，并展示它们在解决复杂工程与科学问题时的威力与局限。

- 在“**原理与机制**”一章中，我们将从滤波操作的数学基础出发，揭示亚格子应力的起源。随后，我们将详细阐述基于[涡粘性假设](@entry_id:1124144)的[Smagorinsky模型](@entry_id:276289)和[WALE模型](@entry_id:1133933)，并深入探讨旨在捕捉[湍流](@entry_id:151300)结构的尺度相似模型，以及实现模型系数自适应的动态模型。
- 随后的“**应用与跨学科联系**”一章将理论付诸实践，探讨这些模型在航空航天、热工、地球物理等领域的具体应用。我们将分析[壁面束缚流](@entry_id:153603)、激波-[湍流](@entry_id:151300)相互作用等复杂现象对模型提出的挑战，并揭示[SGS建模](@entry_id:1131520)方法与数值方案之间深刻的相互作用。
- 最后，在“**动手实践**”部分，我们通过一系列精心设计的实践问题，引导读者亲手实现和评估[SGS模型](@entry_id:754720)，将理论知识转化为解决实际问题的能力。

通过本章的学习，您将不仅掌握各类[SGS模型](@entry_id:754720)的工作原理，更能建立起一种审慎的、基于物理问题的[模型选择](@entry_id:155601)与评估能力，为您的[计算热工学](@entry_id:1122812)研究与工程应用打下坚实的基础。

## 原理与机制

在[大涡模拟](@entry_id:153702)（Large Eddy Simulation, LES）中，核心挑战在于精确地表示已解析尺度与未解析（或亚格子）尺度之间的相互作用。由于计算资源的限制，我们无法解析[湍流](@entry_id:151300)中所有的尺度，因此必须对亚格子尺度运动对已解析尺度运动的影响进行建模。本章将系统地阐述大涡模拟中亚格子尺度（Subgrid-Scale, SGS）建模的基本原理与核心机制。我们将从滤波操作的数学基础出发，推导出亚格子应力的起源，然后详细探讨几类关键的[SGS模型](@entry_id:754720)，包括基于[涡粘性假设](@entry_id:1124144)的[Smagorinsky模型](@entry_id:276289)和[WALE模型](@entry_id:1133933)，以及基于结构相似性思想的尺度相似模型和动态模型。

### 滤波操作与亚格子应力的起源

[大涡模拟](@entry_id:153702)的出发点是对控制方程（通常是Navier-Stokes方程）进行[空间滤波](@entry_id:202429)，从而将流场变量$\phi(\mathbf{x}, t)$分解为已解析（大尺度）部分$\tilde{\phi}(\mathbf{x}, t)$和亚格子（小尺度）部分$\phi'(\mathbf{x}, t)$。

#### 滤波的定义与性质

在LES中，滤波操作通常定义为一个空间[卷积积分](@entry_id:155865)：
$$
\tilde{\phi}(\mathbf{x}, t) = \int_{\mathcal{D}} G(\mathbf{x}-\mathbf{r}; \Delta) \phi(\mathbf{r}, t) \, d\mathbf{r}
$$
其中，$G$是**滤波[核函数](@entry_id:145324)**，$\Delta$是**滤波宽度**，它与计算网格的尺寸相关。为了使该操作成为一个合理的[空间平均](@entry_id:203499)，滤波[核函数](@entry_id:145324)$G$必须满足几个基本性质：
1.  **归一化**: $\int_{\mathcal{D}} G(\mathbf{r}; \Delta) \, d\mathbf{r} = 1$。这个性质保证了对一个常数场进行滤波后，结果仍然是该常数。
2.  **线性**: 滤波是一个线性算子，即$\widetilde{a\phi + b\psi} = a\tilde{\phi} + b\tilde{\psi}$。
3.  **[平移不变性](@entry_id:195885)**: 核函数仅依赖于相对位置$\mathbf{x}-\mathbf{r}$，而与绝对位置无关。

与[雷诺平均](@entry_id:754341)（Reynolds Averaging）相比，[LES滤波](@entry_id:1127170)在概念和数学性质上都有着本质区别。雷诺平均是系综平均，具有**[幂等性](@entry_id:190768)**（即$\overline{\overline{\phi}} = \overline{\phi}$），且脉动量的平均为零（$\overline{\phi'} = 0$）。而[LES滤波](@entry_id:1127170)是对单一样本的局部空间平均，通常不满足[幂等性](@entry_id:190768)（即$\widetilde{\tilde{\phi}} \neq \tilde{\phi}$），并且对亚格子脉动$\phi' = \phi - \tilde{\phi}$再次滤波通常不为零（$\widetilde{\phi'} = \tilde{\phi} - \widetilde{\tilde{\phi}} \neq 0$）。这一非零项是动态模型（将在后文讨论）的理论基础。

#### 滤波方程与亚格子[应力张量](@entry_id:148973)

为了推导已解析尺度的控制方程，我们需要将滤波操作应用于原始的[Navier-Stokes](@entry_id:276387)方程。一个关键问题是滤波与求导运算是否可以交换。当滤波宽度$\Delta$在空间上为常数，且在周期性边界或无限大域中（或当核函数具有[紧支集](@entry_id:276214)时），滤波与空间求导可以交换，即$\widetilde{\nabla\phi} = \nabla\tilde{\phi}$。在时间上，若$\Delta$不随时间变化，则$\widetilde{\partial_t\phi} = \partial_t\tilde{\phi}$。

考虑不可压缩流动的[动量方程](@entry_id:197225)：
$$
\frac{\partial u_i}{\partial t} + \frac{\partial (u_i u_j)}{\partial x_j} = -\frac{1}{\rho}\frac{\partial p}{\partial x_i} + \nu \frac{\partial^2 u_i}{\partial x_j \partial x_j}
$$
对其进行滤波，并假设滤波与求导可交换，我们得到：
$$
\frac{\partial \tilde{u}_i}{\partial t} + \frac{\partial \widetilde{u_i u_j}}{\partial x_j} = -\frac{1}{\rho}\frac{\partial \tilde{p}}{\partial x_i} + \nu \frac{\partial^2 \tilde{u}_i}{\partial x_j \partial x_j}
$$
方程中的[非线性](@entry_id:637147)对流项$\widetilde{u_i u_j}$是未封闭的，因为一般来说，滤波后的乘积不等于乘积的滤波，即$\widetilde{u_i u_j} \neq \tilde{u}_i \tilde{u}_j$。为了封闭方程，我们定义**亚格子应力（SGS）张量**$\tau_{ij}$来表示这一差异：
$$
\tau_{ij} = \widetilde{u_i u_j} - \tilde{u}_i \tilde{u}_j
$$
通过这个定义，我们可以将$\widetilde{u_i u_j}$替换为$\tilde{u}_i \tilde{u}_j + \tau_{ij}$，并将滤波后的动量方程重写为：
$$
\frac{\partial \tilde{u}_i}{\partial t} + \frac{\partial (\tilde{u}_i \tilde{u}_j)}{\partial x_j} = -\frac{1}{\rho}\frac{\partial \tilde{p}}{\partial x_i} - \frac{\partial \tau_{ij}}{\partial x_j} + \nu \frac{\partial^2 \tilde{u}_i}{\partial x_j \partial x_j}
$$
这个方程形式上与原始的Navier-Stokes方程非常相似，但增加了一个新的项：$-\frac{\partial \tau_{ij}}{\partial x_j}$。这一项代表了亚格子尺度运动对已解析尺度[动量方程](@entry_id:197225)的力的作用，是[SGS建模](@entry_id:1131520)的核心目标。

### [Boussinesq假设](@entry_id:272519)与[涡粘性模型](@entry_id:1124145)

[SGS应力张量](@entry_id:1131522)$\tau_{ij}$是一个[对称张量](@entry_id:148092)，可以分解为其各向同性部分和偏（无迹）部分：
$$
\tau_{ij} = \tau'_{ij} + \frac{1}{3}\tau_{kk}\delta_{ij}
$$
其中，$\tau'_{ij}$是[偏应力张量](@entry_id:267642)，$\delta_{ij}$是Kronecker delta符号。各向同性部分的散度$\frac{\partial}{\partial x_j}(\frac{1}{3}\tau_{kk}\delta_{ij}) = \frac{1}{3}\frac{\partial \tau_{kk}}{\partial x_i}$是一个标量的梯度，因此可以被吸收到压力项中，形成一个修正的压力$\tilde{p}^* = \tilde{p} + \frac{1}{3}\rho\tau_{kk}$。因此，建模的重点就落在了[偏应力张量](@entry_id:267642)$\tau'_{ij}$上。值得注意的是，在不可压缩流中$\tau_{kk} = \widetilde{u_k u_k} - \tilde{u}_k \tilde{u}_k$并不为零，它代表了亚格子尺度的动能的两倍。

最广泛应用的[SGS建模](@entry_id:1131520)方法是**[Boussinesq假设](@entry_id:272519)**，它借鉴了分子粘性的思想，假设亚格子应力与已解析尺度的应变率张量成正比：
$$
\tau'_{ij} = -2\nu_t \tilde{S}_{ij}
$$
这里，$\nu_t$被称为**涡粘性系数**或亚格子粘性系数，它不是流体的物理属性，而是反映了亚格子尺度[湍流](@entry_id:151300)运动引起的[动量输运](@entry_id:139628)的等效粘性。$\tilde{S}_{ij}$是**已解析尺度应变率张量**，定义为已解析[速度梯度](@entry_id:261686)$\partial_j \tilde{u}_i$的对称部分：
$$
\tilde{S}_{ij} = \frac{1}{2}\left(\frac{\partial \tilde{u}_i}{\partial x_j} + \frac{\partial \tilde{u}_j}{\partial x_i}\right)
$$
这个[涡粘性假设](@entry_id:1124144)的合理性基于几个基本物理约束：
- **对称性**：$\tilde{S}_{ij}$是对称的，保证了模型化的$\tau'_{ij}$也是对称的。
- **客观性（伽利略不变性）**：模型必须与观察者的[惯性参考系](@entry_id:276742)无关。这要求模型只能依赖于[速度梯度](@entry_id:261686)的对称部分（应变率张量$\tilde{S}_{ij}$），而不能依赖于其反对称部分，即**旋转率张量** $\tilde{\Omega}_{ij} = \frac{1}{2}(\partial_j \tilde{u}_i - \partial_i \tilde{u}_j)$。
- **[能量耗散](@entry_id:147406)**：SGS模型的核心物理作用是模拟能量从已解析尺度向亚格子尺度的传递（即能量级串）。这个能量[传递率](@entry_id:756124)（SGS耗散）为$\Pi = -\tau_{ij}\tilde{S}_{ij}$。对于[涡粘性模型](@entry_id:1124145)，$\Pi = -(-2\nu_t\tilde{S}_{ij})\tilde{S}_{ij} = 2\nu_t \tilde{S}_{ij}\tilde{S}_{ij} = 2\nu_t |\tilde{S}|^2$。由于$|\tilde{S}|^2 \ge 0$，只要$\nu_t \ge 0$，该模型就能保证能量从大尺度向小尺度净输运，符合[湍流](@entry_id:151300)物理并保证[数值稳定性](@entry_id:175146)。

不同的[涡粘性模型](@entry_id:1124145)，其区别就在于如何构造标量涡粘性系数$\nu_t$。

### 基础[涡粘性模型](@entry_id:1124145)

#### [Smagorinsky模型](@entry_id:276289)

最经典、最简单的[涡粘性模型](@entry_id:1124145)是**[Smagorinsky模型](@entry_id:276289)**。该模型通过量纲分析和物理假设来构造$\nu_t$。其核心思想基于**[局部平衡假设](@entry_id:182180)**，即在亚格子尺度上，能量的产生率$\Pi$与[湍流](@entry_id:151300)的耗散率$\epsilon$[相平衡](@entry_id:136822)。

根据Kolmogorov的[惯性区](@entry_id:1126481)理论，$\nu_t$应该只依赖于滤波宽度$\Delta$和耗散率$\epsilon$。量纲分析表明，$\nu_t$的量纲为$[L]^2[T]^{-1}$，而$\epsilon$的量纲为$[L]^2[T]^{-3}$，$\Delta$的量纲为$[L]$。由此可得，$\nu_t \sim \epsilon^{1/3}\Delta^{4/3}$。同时，[惯性区](@entry_id:1126481)中的应变率大小尺度关系为$|\tilde{S}| \sim \epsilon^{1/3}\Delta^{-2/3}$。将这两个关系式结合，可以消去未知的$\epsilon$，得到$\nu_t \propto \Delta^2 |\tilde{S}|$。[Smagorinsky模型](@entry_id:276289)正是基于此，其表达式为：
$$
\nu_t = (C_s \Delta)^2 |\tilde{S}|
$$
其中，$|\tilde{S}| = \sqrt{2\tilde{S}_{ij}\tilde{S}_{ij}}$是[应变率张量](@entry_id:266108)大小的模，$C_s$是一个无量纲的模型常数（Smagorinsky常数）。

尽管[Smagorinsky模型](@entry_id:276289)具有坚实的物理基础，但它存在明显缺陷：
1.  模型常数$C_s$并非普适，对于不同类型的流动需要调整。
2.  在壁面附近，即使流动趋于层流，模型仍然会预测出非零的涡粘性，这是不符合物理的。因此，需要引入额外的壁面阻尼函数。
3.  模型是纯耗散的，无法描述能量从亚格子尺度到已解析尺度的“逆向散射”（backscatter）现象。

#### [WALE模型](@entry_id:1133933) (Wall-Adapting Local Eddy-viscosity)

为了解决[Smagorinsky模型](@entry_id:276289)在壁面附近的缺陷，**[WALE模型](@entry_id:1133933)**被提出来。它的核心思想是构造一个对[速度梯度](@entry_id:261686)的不同不变量更敏感的涡粘性系数，使其能够在壁面附近自动趋于零，而无需引入任何经验性的阻尼函数。

[WALE模型](@entry_id:1133933)利用了速度梯度[张量的对称部分](@entry_id:182434)（应变率$\tilde{S}_{ij}$）和反对称部分（旋转率$\tilde{\Omega}_{ij}$）的信息。其涡粘性系数$\nu_t$的构造依赖于一个特殊的张量算子，该算子由[速度梯度张量](@entry_id:270928)的平方$\tilde{g}_{ik}\tilde{g}_{kj} = (\tilde{S}_{ik}+\tilde{\Omega}_{ik})(\tilde{S}_{kj}+\tilde{\Omega}_{kj})$导出，从而同时包含了应变和旋转的信息。

[WALE模型](@entry_id:1133933)的一个重要特性是它能够正确地区分纯应变流动和纯旋转流动。例如，在一个二维[刚体](@entry_id:1131033)[旋转流](@entry_id:276737)$\mathbf{u} = (-\Omega y, \Omega x)$中，流场只存在旋转（$\tilde{\Omega}_{ij} \neq 0$）而没有应变（$\tilde{S}_{ij} = 0$）。在这种情况下，[湍流](@entry_id:151300)涡粘性应该为零。[Smagorinsky模型](@entry_id:276289)由于直接依赖于$|\tilde{S}|$，自然满足这个条件。通过详细的代数推导可以证明，[WALE模型](@entry_id:1133933)在该流场中计算出的涡粘性系数也精确为零。更重要的是，在壁面附近的[剪切流](@entry_id:266817)中，[WALE模型](@entry_id:1133933)能够正确地给出$\nu_t \propto y^3$的[渐近行为](@entry_id:160836)（$y$是到壁面的距离），从而实现了模型的“壁面自适应”能力。

### 高级建模概念：结构与动态方法

#### 尺度相似模型

[涡粘性模型](@entry_id:1124145)本质上是“功能性”模型，它们旨在模仿亚格子应力的主要功能——[能量耗散](@entry_id:147406)。另一类模型，称为**结构性模型**，则试图直接模拟亚格子[应力张量](@entry_id:148973)本身的结构。其中最著名的是**Bardina尺度相似模型**。

其核心假设是，亚格子应力$\tau_{ij} = \widetilde{u_i u_j} - \tilde{u}_i \tilde{u}_j$的结构与由已解析速度场$\tilde{u}_i$在更大尺度上定义的应力相似。具体而言，通过对已解析场再进行一次滤波（称为**测试滤波**，通常使用相同的滤波核），我们可以构造一个“可解尺度应力”：
$$
L_{ij} = \widetilde{\tilde{u}_i \tilde{u}_j} - \tilde{\tilde{u}}_i \tilde{\tilde{u}}_j
$$
尺度相似模型假设$\tau_{ij}$与$L_{ij}$成正比，最简单的形式即$\tau_{ij} \approx L_{ij}$。

尺度相似模型的主要优点是它与真实的[SGS应力](@entry_id:1131521)有很高的相关性，并且能够自然地描述能量的逆向散射。然而，它的主要缺点是耗散性不足，如果单独使用，通常会导致数值不稳定。因此，它常常与一个[涡粘性模型](@entry_id:1124145)（如[Smagorinsky模型](@entry_id:276289)）结合，形成所谓的**混合模型**，以兼顾结构相似性和足够的能量耗散。

#### 动态模型

[Smagorinsky模型](@entry_id:276289)等传统[涡粘性模型](@entry_id:1124145)的一个主要问题是模型系数（如$C_s$）的非普适性。**动态模型**（或动态过程）提供了一种在模拟过程中根据流场局部信息自动[计算模型](@entry_id:637456)系数的方法。

动态模型同样基于测试滤波的思想。它引入一个比网格滤波$\Delta$更宽的测试滤波$\hat{\Delta}$（通常取$\hat{\Delta}=2\Delta$）。在实践中，离散的测试滤波器需要精心构造以满足归一化、对称性和一定的精度要求。例如，一个在均匀一维网格上常用的二阶精度三点[对称滤波](@entry_id:182791)器，其权重为$\{\frac{1}{6}, \frac{2}{3}, \frac{1}{6}\}$ 。

动态模型的核心是**[Germano恒等式](@entry_id:749887)**，这是一个在不同滤波尺度之间建立联系的精确关系：
$$
T_{ij} = \widehat{\tau_{ij}} + L_{ij}
$$
其中，$T_{ij} = \widehat{\widetilde{u_i u_j}} - \hat{\tilde{u}}_i \hat{\tilde{u}}_j$是在测试滤波尺度$\hat{\Delta}$上的亚格子应力，$\widehat{\tau_{ij}}$是网格尺度$\Delta$上的[SGS应力](@entry_id:1131521)经过测试滤波后的结果，而$L_{ij} = \widehat{\tilde{u}_i \tilde{u}_j} - \hat{\tilde{u}}_i \hat{\tilde{u}}_j$正是前面提到的可解尺度应力。

现在，如果我们假设在两个尺度上[SGS应力](@entry_id:1131521)都遵循相同的模型形式（例如[Smagorinsky模型](@entry_id:276289)），即：
$$
\tau_{ij} - \frac{1}{3}\tau_{kk}\delta_{ij} = -2(C_s\Delta)^2|\tilde{S}|\tilde{S}_{ij}
$$
$$
T_{ij} - \frac{1}{3}T_{kk}\delta_{ij} = -2(C_s\hat{\Delta})^2|\hat{\tilde{S}}|\hat{\tilde{S}}_{ij}
$$
将这两个模型代入[Germano恒等式](@entry_id:749887)，就可以得到一个关于$C_s$的代数方程。通过求解这个方程，就可以在每个时间步、每个空间位置动态地确定$C_s$的值，从而使模型能够自适应于不同的流动区域（例如，在近壁区自动减小，在[湍流](@entry_id:151300)核心区增大）。

### 亚格子尺度[标量输运](@entry_id:150360)建模

在[计算热工学](@entry_id:1122812)等领域，除了动量输运，对温度等标量场的输运建模也至关重要。通过对温度[输运方程](@entry_id:174281)进行滤波，会产生一个未封闭的**亚格子[标量通量](@entry_id:1131249)**项：
$$
q_i^{\text{sgs}} = \widetilde{u_i T} - \tilde{u}_i \tilde{T}
$$
类似于[SGS应力](@entry_id:1131521)，这个项代表了未解析的[湍流](@entry_id:151300)运动对[标量输运](@entry_id:150360)的贡献。

对此最常用的封闭方法是**梯度扩散假设**，它假设亚格子通量与已解析[标量场的梯度](@entry_id:270765)成反比，方向沿着梯度的反方向（即“顺梯度”输运）：
$$
q_i^{\text{sgs}} = -\alpha_t \frac{\partial \tilde{T}}{\partial x_i}
$$
这里的$\alpha_t$是**涡扩散系数**，负号保证了湍流混合的宏观效果是平滑标量梯度，符合[热力学](@entry_id:172368)第二定律。

为了确定$\alpha_t$，通常利用**雷诺比拟**的思想，即[湍流](@entry_id:151300)对动量和标量的输运机制是相似的。这种相似性通过**湍流普朗特数**$\text{Pr}_t$来量化：
$$
\text{Pr}_t = \frac{\nu_t}{\alpha_t}
$$
对于许多气体流动，$\text{Pr}_t$可以近似为一个常数（通常在0.7到0.9之间）。这样，一旦通过SGS动量模型（如Smagorinsky或WALE）计算出涡粘性$\nu_t$，就可以很容易地得到涡扩散系数$\alpha_t = \nu_t / \text{Pr}_t$。最终的SGS标量通量模型为 ：
$$
q_i^{\text{sgs}} = -\frac{\nu_t}{\text{Pr}_t} \frac{\partial \tilde{T}}{\partial x_i}
$$
这个模型形式与Kolmogorov[惯性区](@entry_id:1126481)[标度律](@entry_id:266186)是相容的，为模拟[湍流传热](@entry_id:189092)提供了坚实的理论基础。

### 关于非均匀网格的注记

我们之前假设滤波与求导运算可以交换，这通常要求滤波宽度$\Delta$是[空间常数](@entry_id:193491)。然而，在实际的CFD计算中，网格往往是非均匀的，这意味着隐式的滤波宽度$\Delta(x)$是随空间变化的。在这种情况下，滤波与求导运算不再能交换，会产生一个**交换误差项**。

例如，对于一个宽度可变的盒式滤波器，可以精确推导出其交换误差为：
$$
C(x) = \frac{d\tilde{u}}{dx} - \widetilde{\frac{du}{dx}} = \frac{\Delta'(x)}{2\Delta(x)} \left( u\left(x + \frac{\Delta}{2}\right) + u\left(x - \frac{\Delta}{2}\right) \right) - \frac{\Delta'(x)}{\Delta(x)^2} \int_{x-\Delta/2}^{x+\Delta/2} u(\xi) d\xi
$$
这个误差项正比于滤波宽度的梯度$\Delta'(x)$，它在滤波后的[Navier-Stokes](@entry_id:276387)方程中会产生额外的、与[SGS应力](@entry_id:1131521)$\tau_{ij}$在数学上截然不同的源项。在许多实际应用中，这些项被忽略或被认为包含在数值离散误差中。然而，从严格的理论角度看，它们是LES方程在[非均匀网格](@entry_id:752607)上的一个确定部分，其处理方式是LES理论与实践之间的一个重要差异点。