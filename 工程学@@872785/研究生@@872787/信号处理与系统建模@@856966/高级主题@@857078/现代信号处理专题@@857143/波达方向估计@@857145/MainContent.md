## 引言
[到达角](@entry_id:265527)（Direction of Arrival, DOA）估计是[阵列信号处理](@entry_id:197159)领域的一项基本任务，其核心目标是利用空间分布的传感器阵列来确定一个或多个入射信号源的方位。从雷达、声呐到无线通信和[射电天文学](@entry_id:153213)，精确定位信号源的能力在无数科学与工程应用中都至关重要。尽管其基本概念直观，但从理想化的理论模型过渡到充满噪声、干扰和[模型不确定性](@entry_id:265539)的现实世界，存在着巨大的知识鸿沟与技术挑战。

本文旨在系统性地跨越这一鸿沟。我们将从DOA估计的数学基石出发，逐步深入到解决实际应用难题的高级技术和前沿[范式](@entry_id:161181)。通过本文的学习，读者将不仅掌握核心算法的原理，还将理解其在复杂场景下的局限性，并探索最新的研究方向。

文章结构如下：第一章 **“原理与机制”** 将奠定坚实的理论基础，详细介绍阵列信号模型、[参数可辨识性](@entry_id:197485)条件、经典的MUSIC和ESPRIT[子空间](@entry_id:150286)算法及其性能界限。第二章 **“应用与交叉学科联系”** 将理论应用于更广泛的场景，探讨二维阵列、[近场](@entry_id:269780)/远场问题、阵列校准、宽带信号处理、[稀疏恢复](@entry_id:199430)方法，并将其与[分布式传感](@entry_id:191741)和[量子生物学](@entry_id:268396)等前沿领域联系起来。最后，**“动手实践”** 部分将通过具体问题，帮助读者巩固和应用所学知识。

## 原理与机制

本章旨在深入探讨[到达角](@entry_id:265527)（Direction of Arrival, DOA）估计的基本原理和核心机制。我们将从构建阵列信号的数学模型出发，逐步深入到[参数辨识](@entry_id:275549)的基本限制、经典的[子空间](@entry_id:150286)估计算法，并讨论在实际应用中遇到的各种挑战及其解决方案。本章的目标是为读者提供一个系统而严谨的理论框架，为后续章节中更高级的算法和应用奠定坚实的基础。

### 窄带[远场](@entry_id:269288)阵列信号模型

DOA 估计的第一步是建立一个精确的数学模型，以描述传感器阵列接收到的信号。我们考虑一个由 $M$ 个传感器组成的阵列，接收来自 $K$ 个[远场](@entry_id:269288)信源的窄带信号。

#### 几何延迟与相位关系

假设一个平面波以速度 $c$ 从方向 $\theta$ 入射到阵列上。由于[波前](@entry_id:197956)到达不同传感器的路径长度不同，各传感器接收到的信号存在时间延迟。以一个沿 $x$ 轴放置、传感器间距为 $d$ 的**均匀线性阵列（Uniform Linear Array, ULA）**为例，若角度 $\theta$ 从阵列的[法线](@entry_id:167651)方向（Broadside）算起，那么第 $m$ 个传感器相对于第一个（参考）传感器的路径差为 $(m-1)d \sin\theta$。相应的时间延迟 $\tau_m(\theta)$ 为：

$$ \tau_m(\theta) = \frac{(m-1)d \sin\theta}{c} $$

其中 $m = 1, 2, \ldots, M$。[@problem_id:2866444]

#### 窄带近似

在信号处理中，信号通常表示为其复基带（或[复包络](@entry_id:181897)）形式。一个[载波](@entry_id:261646)频率为 $f_c$ 的通带信号可以表示为 $s_c(t) = \Re\{s_b(t)\exp(j 2\pi f_c t)\}$，其中 $s_b(t)$ 是[复包络](@entry_id:181897)。在存在时间延迟 $\tau$ 的情况下，接收到的信号为 $s_c(t-\tau)$，其对应的[复包络](@entry_id:181897)为 $s_b(t-\tau)\exp(-j 2\pi f_c \tau)$。

**窄带近似（Narrowband Approximation）**是DOA估计中的一个核心假设。它指出，如果信号的带宽 $B$ 远小于其载波频率 $f_c$（即 $B \ll f_c$），并且由阵列孔径引起的最大时间延迟扩展 $\tau_{\max}$ 满足 $B \cdot \tau_{\max} \ll 1$，那么可以认为在延迟时间段内[复包络](@entry_id:181897) $s_b(t)$ 的变化可以忽略不计，即 $s_b(t - \tau_m(\theta)) \approx s_b(t)$。然而，由载波引起相移项 $\exp(-j 2\pi f_c \tau)$ 不能被忽略，因为它对一个很小的时间延迟 $\tau$ 也可能非常敏感。因此，时间延迟主要体现为一个纯粹的相位旋转。[@problem_id:2866503]

#### 导向矢量与阵列信号模型

基于窄带近似，第 $m$ 个传感器接收到的来自第 $k$ 个信源的复基带信号可以表示为：

$$ x_{m,k}[n] \approx s_k[n] \exp\left(-j 2\pi f_c \tau_m(\theta_k)\right) = s_k[n] \exp\left(-j 2\pi \frac{(m-1)d \sin\theta_k}{\lambda}\right) $$

其中 $s_k[n]$ 是第 $k$ 个信源在参考点的离散时间[复包络](@entry_id:181897)样本，$\lambda = c/f_c$ 是信号波长。

我们将所有传感器的相位关系收集到一个向量中，这个向量被称为**导向矢量（Steering Vector）**，记为 $\mathbf{a}(\theta)$。对于上述的ULA，其导向矢量为：

$$ \mathbf{a}(\theta) = \begin{pmatrix} 1 \\ \exp\left(-j 2\pi \frac{d}{\lambda} \sin\theta\right) \\ \vdots \\ \exp\left(-j 2\pi \frac{(M-1)d}{\lambda} \sin\theta\right) \end{pmatrix} $$

当阵列同时接收 $K$ 个信源的信号，并叠加[加性噪声](@entry_id:194447)时，第 $n$ 个采样时刻的 $M \times 1$ 维阵列接收数据向量 $\mathbf{x}[n]$ 可以建模为：

$$ \mathbf{x}[n] = \sum_{k=1}^{K} \mathbf{a}(\theta_k) s_k[n] + \mathbf{w}[n] $$

该模型可以进一步写成紧凑的矩阵形式：

$$ \mathbf{x}[n] = \mathbf{A}(\boldsymbol{\theta}) \mathbf{s}[n] + \mathbf{w}[n] $$

其中 $\mathbf{A}(\boldsymbol{\theta}) = [\mathbf{a}(\theta_1), \mathbf{a}(\theta_2), \ldots, \mathbf{a}(\theta_K)]$ 是 $M \times K$ 维的**阵列[流形](@entry_id:153038)矩阵（Array Manifold Matrix）**，$\mathbf{s}[n] = [s_1[n], \ldots, s_K[n]]^T$ 是 $K \times 1$ 维的信源信号向量，$\mathbf{w}[n]$ 是 $M \times 1$ 维的噪声向量。通常，我们假设噪声是时空均为白色的复[高斯噪声](@entry_id:260752)，即 $\mathbf{w}[n] \sim \mathcal{CN}(\mathbf{0}, \sigma_w^2 \mathbf{I}_M)$。

阵列的**[协方差矩阵](@entry_id:139155)** $\mathbf{R}_x$ 是大多数DOA估计算法的基础，其定义为：

$$ \mathbf{R}_x = \mathbb{E}\left\{\mathbf{x}[n]\mathbf{x}[n]^H\right\} = \mathbf{A}(\boldsymbol{\theta})\mathbf{R}_s\mathbf{A}(\boldsymbol{\theta})^H + \mathbf{R}_w $$

其中 $\mathbf{R}_s = \mathbb{E}\left\{\mathbf{s}[n]\mathbf{s}[n]^H\right\}$ 是信源[协方差矩阵](@entry_id:139155)，$\mathbf{R}_w = \mathbb{E}\left\{\mathbf{w}[n]\mathbf{w}[n]^H\right\}$ 是噪声[协方差矩阵](@entry_id:139155)。这个模型是后续所有分析的基石。[@problem_id:2866444]

### [参数可辨识性](@entry_id:197485)、模糊性与阵列[流形](@entry_id:153038)

在得到信号模型后，一个自然的问题是：我们能否从接收到的信号中唯一地确定信源的DOA？这个问题的答案与阵列的几何结构密切相关，可以通过**阵列[流形](@entry_id:153038)（Array Manifold）**的概念来阐述。阵列[流形](@entry_id:153038) $\mathcal{A}$ 是所有可能方向对应的导向矢量的集合，即 $\mathcal{A} = \{\mathbf{a}(\theta) : \theta \in [-\pi/2, \pi/2]\}$。[@problem_id:2866449]

#### 全局[可辨识性](@entry_id:194150)与空间模糊

**全局可辨识性（Global Identifiability）**要求对于任意两个不同的方向 $\theta_1 \neq \theta_2$，其对应的导向矢量是线性无关的。如果存在 $\theta_1 \neq \theta_2$ 使得 $\mathbf{a}(\theta_1)$ 和 $\mathbf{a}(\theta_2)$ 共线，那么我们就无法区分这两个方向，这种情况称为**模糊（Ambiguity）**。

对于一个ULA，模糊产生的条件是 $\mathbf{a}(\theta_1) = \mathbf{a}(\theta_2)$（由于导向矢量的第一个元素为1，共线即等价于相等）。这等价于对所有 $m$ 都满足 $\exp(-j(m-1)\frac{2\pi d}{\lambda}\sin\theta_1) = \exp(-j(m-1)\frac{2\pi d}{\lambda}\sin\theta_2)$。这要求：

$$ \frac{d}{\lambda}(\sin\theta_1 - \sin\theta_2) = q $$

其中 $q$ 为某个非零整数。这种由阵列周期性结构引起的模糊被称为**[空间混叠](@entry_id:275674)（Spatial Aliasing）**或**栅瓣（Grating Lobe）**。为了避免这种模糊，必须使得上述等式对于任意 $\theta_1 \neq \theta_2$ 都不存在非零整数解 $q$。由于 $\sin\theta_1 - \sin\theta_2$ 的取值范围为 $(-2, 2)$，只要我们保证 $|\frac{d}{\lambda}(\sin\theta_1 - \sin\theta_2)| \lt 1$，就可以确保 $q$ 只能为0。这引出了著名的**半波长准则**：当传感器间距 $d  \lambda/2$ 时，ULA不会产生空间模糊。当 $d=\lambda/2$ 时，仅在端射方向（$\theta = \pm \pi/2$）出现模糊。而当 $d > \lambda/2$ 时，必然会在某些方向上出现模糊，导致全局[可辨识性](@entry_id:194150)丧失。[@problem_id:2866449]

对于二维平面阵列，避免模糊的条件更为严格。除了要求所有传感器对之间的距离小于 $\lambda/2$ 外，还要求阵列是**非共线（Non-collinear）**的，即所有传感器不位于同一直线上。如果阵列是共线的，那么它总会存在关于阵列轴线的镜像模糊。只有当阵列的基线向量（baseline vectors）能够张成整个二维平面时，结合半波长间距条件，才能保证在整个角度空间 $[0, 2\pi)$ 内的唯一[可辨识性](@entry_id:194150)。[@problem_id:2866465]

#### 局部[可辨识性](@entry_id:194150)

**局部可辨识性（Local Identifiability）**关心的是能否区分两个无限接近的方向。这与阵列[流形](@entry_id:153038)在某一点的[切线](@entry_id:268870)方向有关。在单信源模型中，信号为 $s \cdot \mathbf{a}(\theta)$，其中 $s$ 是未知的[复振幅](@entry_id:164138)。当 $\theta$ 发生微小变化 $\delta\theta$ 时，信号的变化量近似为 $s \cdot \frac{\partial \mathbf{a}(\theta)}{\partial \theta} \delta\theta$。如果这个变化方向与原信号方向 $\mathbf{a}(\theta)$ 共线，那么这个变化就可以被误认为是[复振幅](@entry_id:164138) $s$ 的变化，从而导致 $\theta$ 无法被识别。因此，局部[可辨识性](@entry_id:194150)要求导向矢量的导数 $\dot{\mathbf{a}}(\theta) = \frac{\partial \mathbf{a}(\theta)}{\partial \theta}$ 与 $\mathbf{a}(\theta)$ 本身是[线性无关](@entry_id:148207)的。换言之，$\dot{\mathbf{a}}(\theta)$ 在 $\mathbf{a}(\theta)$ 的[正交补](@entry_id:149922)空间上的投影必须非零。对于ULA，只有在端射方向（$\theta = \pm \pi/2$）时，这个条件才会失效。[@problem_id:2866449]

### 基于[子空间](@entry_id:150286)的估计算法：MUSIC

[子空间方法](@entry_id:200957)是现代DOA估计技术的核心，其中**多重信号分类（Multiple Signal Classification, MUSIC）**算法是最具代表性的一个。

#### [信号子空间](@entry_id:185227)与噪声[子空间](@entry_id:150286)

在前面定义的阵列[协方差矩阵](@entry_id:139155)模型 $\mathbf{R}_x = \mathbf{A}\mathbf{R}_s\mathbf{A}^H + \sigma^2 \mathbf{I}$ 中，假设信源是不相关的（$\mathbf{R}_s$ 为对角满秩），噪声是空间[白噪声](@entry_id:145248)（$\mathbf{R}_w = \sigma^2 \mathbf{I}$）。对 $\mathbf{R}_x$ 进行[特征值分解](@entry_id:272091)，可以得到 $M$ 个[特征值](@entry_id:154894)和对应的[特征向量](@entry_id:151813)。

由于信号协[方差](@entry_id:200758)部分 $\mathbf{A}\mathbf{R}_s\mathbf{A}^H$ 的秩为 $K$，而噪声协[方差](@entry_id:200758)部分 $\sigma^2 \mathbf{I}$ 是对所有方向的能量的均匀提升，$\mathbf{R}_x$ 的[特征值](@entry_id:154894)将呈现出如下结构：
- $K$ 个较大的[特征值](@entry_id:154894)（信号[特征值](@entry_id:154894)），其对应的[特征向量](@entry_id:151813)张成**[信号子空间](@entry_id:185227)（Signal Subspace）**。这个[子空间](@entry_id:150286)与阵列[流形](@entry_id:153038)矩阵 $\mathbf{A}$ 的[列空间](@entry_id:156444)相同，即 $\text{span}\{\mathbf{A}\}$。
- $M-K$ 个较小且相等的[特征值](@entry_id:154894)（均为 $\sigma^2$），其对应的[特征向量](@entry_id:151813)张成**噪声[子空间](@entry_id:150286)（Noise Subspace）**。

最重要的性质是，[信号子空间](@entry_id:185227)与噪声[子空间](@entry_id:150286)是**正交**的。[@problem_id:2866491]

#### MUSIC 算法原理

MUSIC 算法的核心思想正是利用了这种正交性：任何一个真实信源方向 $\theta_k$ 对应的导向矢量 $\mathbf{a}(\theta_k)$ 都位于[信号子空间](@entry_id:185227)中，因此它必然与噪声[子空间](@entry_id:150286)中的任意向量正交。

在实践中，我们使用 $N$ 个快拍数据计算样本协方差矩阵 $\widehat{\mathbf{R}}_x = \frac{1}{N}\sum_{n=1}^N \mathbf{x}[n]\mathbf{x}[n]^H$，并对其进行[特征分解](@entry_id:181333)，得到估计的噪声[子空间](@entry_id:150286)，其由对应的[特征向量](@entry_id:151813)矩阵 $\widehat{\mathbf{U}}_N$ 表示。MUSIC 算法通过构造一个**伪谱（pseudo-spectrum）**函数来搜索DOA：

$$ P_{\text{MUSIC}}(\theta) = \frac{1}{\mathbf{a}(\theta)^H \widehat{\mathbf{U}}_N \widehat{\mathbf{U}}_N^H \mathbf{a}(\theta)} $$

当搜索角 $\theta$ 与某个真实DOA $\theta_k$ 一致时，$\mathbf{a}(\theta_k)$ 与噪声[子空间](@entry_id:150286)近似正交，分母趋近于零，从而在[伪谱](@entry_id:138878)上形成一个尖锐的峰值。通过寻找该函数的峰值，我们就能估计出所有信源的DOA。

#### 性能与局限

MUSIC 算法是一种**超分辨率（Super-resolution）**算法。与传统波束形成（Classical Beamforming, CBF）方法相比，它的分辨能力不受瑞利限的限制。CBF的分辨极限 $\Delta u_{\text{CBF}}$ (其中 $u=\sin\theta$) 主要由阵列[孔径](@entry_id:172936)决定，与传感器数量 $M$ 成反比，即 $\Delta u_{\text{CBF}} \asymp 1/M$，且与[信噪比](@entry_id:185071)（SNR）和快拍数 $N$ 无关。而[MUSIC算法](@entry_id:182406)在较高[信噪比](@entry_id:185071)和足够多的快拍数下，其分辨极限 $\Delta u_{\text{MUSIC}}$ 可远超瑞利限，其缩放规律近似为：

$$ \Delta u_{\text{MUSIC}} \asymp \frac{1}{M^{3/2}\sqrt{N \cdot \rho}} $$

其中 $\rho$ 为[信噪比](@entry_id:185071)。这表明MUSIC的分辨能力随 $M$, $N$, $\rho$ 的增加而显著提升。

然而，MUSIC的超分辨率特性并非无条件的。它存在一个**门限效应（Threshold Effect）**。当信噪比或快拍数过低时，估计的[子空间](@entry_id:150286)与真实[子空间](@entry_id:150286)偏差过大，正交性被严重破坏，算法性能会急剧下降，其分辨能力将退化到与传统波束形成相当的水平。[@problem_id:2866459]

### 实际挑战与高级方法

标准[MUSIC算法](@entry_id:182406)的推导依赖于几个理想化假设。在实际应用中，这些假设往往不成立，导致算法性能下降甚至失效。

#### 相干信源问题

当两个或多个信源信号是**相干（Coherent）**的，例如在多径传播环境中，一个信源的信号通过不同路径到达阵列，它们的信号波形是[线性相关](@entry_id:185830)的。这导致信源[协方差矩阵](@entry_id:139155) $\mathbf{R}_s$ 发生**[秩亏](@entry_id:754065)损（Rank-Deficient）**。具体而言，一个包含 $G$ 个完全相干信源的群组，其源信号子向量为 $\mathbf{s}_c(t) = \mathbf{b} u(t)$，对应的协[方差](@entry_id:200758)子矩阵将变为一个秩为1的矩阵 $\mathbf{S}_c = \sigma_u^2 \mathbf{b}\mathbf{b}^H$。[@problem_id:2866422]

这种[秩亏](@entry_id:754065)损使得信号协方差矩阵 $\mathbf{A}\mathbf{R}_s\mathbf{A}^H$ 的秩小于信源数 $K$。[信号子空间](@entry_id:185227)的维度随之“坍缩”，不再包含所有真实信源的导向矢量。因此，[MUSIC算法](@entry_id:182406)的基本正交性假设被破坏，导致无法分辨出所有的相干信源。[@problem_id:2866422] [@problem_id:2866459]

一种常见的解决方法是**前向-后向平均（Forward-Backward Averaging）**。对于**[中心对称](@entry_id:144242)（Centro-symmetric）**的阵列（如中心位于原点的ULA），可以通过构建一个新的协方差矩阵 $\widehat{\mathbf{R}}_{FB}=\frac{1}{2}(\widehat{\mathbf{R}}+\mathbf{J}\widehat{\mathbf{R}}^T\mathbf{J})$（其中 $\mathbf{J}$ 是交换矩阵）来恢复信号协方差矩阵的秩。这个过程可以被理解为将数据与其“时间反转共轭”版本结合，有效地对相干信源进行解相干。然而，这种解相干并非在所有情况下都完全有效。[@problem_id:2866416]

#### 空间[有色噪声](@entry_id:265434)

标准MUSIC假设噪声是**空间白噪声**，即 $\mathbf{R}_w = \sigma^2 \mathbf{I}$。但在实际中，由于其他未建模的远场干擾或传感器本身的不一致性，噪声可能呈现**空间有色（Spatially Colored）**特性，其[协方差矩阵](@entry_id:139155) $\mathbf{R}_w$ 为一个非对角或非标量的矩阵。

在这种情况下，阵列协方差矩阵变为 $\mathbf{R}_x = \mathbf{A}\mathbf{R}_s\mathbf{A}^H + \mathbf{R}_w$。由于 $\mathbf{R}_w$ 的非标量结构，$\mathbf{R}_x$ 的噪声[子空间](@entry_id:150286)不再与[信号子空间](@entry_id:185227)（$\text{span}\{\mathbf{A}\}$）正交。直接应用[MUSIC算法](@entry_id:182406)将导致错误的DOA估计。

如果噪声协方差矩阵 $\mathbf{R}_w$ 已知或可以被独立地估计，可以通过**[预白化](@entry_id:185911)（Pre-whitening）**来解决这个问题。通过对接收数据进行线性变换 $\mathbf{y}[n] = \mathbf{R}_w^{-1/2}\mathbf{x}[n]$，变换后的[数据协方差](@entry_id:748192)矩阵将恢复标准MUSIC模型所要求的结构。在数学上，这等价于求解**[广义特征值问题](@entry_id:151614)** $(\mathbf{R}_x, \mathbf{R}_w)$。[@problem_id:2866491]

#### ESPRIT：一种免[搜索算法](@entry_id:272182)

[MUSIC算法](@entry_id:182406)虽然性能优越，但其需要在整个角度空间进行一维或多维的谱峰搜索，计算复杂度高。**基于旋转不变技术的信号[参数估计](@entry_id:139349)（Estimation of Signal Parameters via Rotational Invariance Techniques, ESPRIT）**算法提供了一种高效的免搜索替代方案。

ESPRIT的核心要求是阵列具有**[平移不变性](@entry_id:195885)（Shift-Invariance）**，即阵列可以被看作是两个完全相同但有位移的子阵列。一个标准的ULA就满足这个特性。ESPRIT利用了这两个子阵列接收到的信号之间的相位关系，这种关系直接编码了DOA信息。

算法流程大致如下：
1.  与MUSIC类似，首先进行子[空间分解](@entry_id:755142)，得到[信号子空间](@entry_id:185227)的一个基底。
2.  利用两个子阵列的选择矩阵，构建两个基于[信号子空间](@entry_id:185227)的矩阵。
3.  通过求解一个[最小二乘问题](@entry_id:164198)，得到一个与DOA相关的旋转算子 $\boldsymbol{\Psi}$。
4.  对 $\boldsymbol{\Psi}$ 进行[特征值分解](@entry_id:272091)，其[特征值](@entry_id:154894)直接包含了所有信源的相位因子，从中可以直接计算出DOA，无需任何搜索。

**ESPRIT与MUSIC的比较**：
- **计算复杂度**：在子[空间分解](@entry_id:755142)之后，ESPRIT仅需处理一个 $K \times K$ 的小矩阵，而MUSIC需要进行密集的谱搜索。当搜索网格很大或维度很高时（如二维DOA），ESPRIT的计算优势极其显著。[@problem_id:2866482]
- **通用性**：MUSIC适用于任何已知阵列[流形](@entry_id:153038)的阵列，而ESPRIT严格要求阵列具有平移不变性。因此，MUSIC在阵列几何方面更具通用性。
- **精度**：在满足各自条件的理想情况下，当快拍数趋于无穷时，两种算法的精度相当，都能逼近理论性能极限。

**酉ESPRIT（Unitary ESPRIT）**是ESPRIT的一个重要变种。它结合了前向-后向平均技术，通过一个固定的[酉变换](@entry_id:152599)将复数域的估计[问题转换](@entry_id:274273)到实数域进行，这不仅提高了[数值稳定性](@entry_id:146550)，也常常带来更好的估计精度。[@problem_id:2866416]

### 基本性能界：克拉默-拉奥界

**克拉默-拉奥界（Cramér-Rao Bound, CRB）**为任何无偏[估计量的[方](@entry_id:167223)差](@entry_id:200758)提供了一个理论下限。它描述了在给定信号模型和统计假设下，我们可能达到的最佳估计精度。

对于DOA估计，一个有趣且重要的结论是：在单信源、[确定性信号](@entry_id:272873)模型和[加性高斯白噪声](@entry_id:269320)的条件下，无论噪声[方差](@entry_id:200758) $\sigma^2$ 是已知还是未知，DOA参数 $\theta$ 的CRB是**相同**的。

这个结论的根本原因在于**[费雪信息矩阵](@entry_id:750640)（Fisher Information Matrix, FIM）**的结构。对于这个模型，FIM在与均值相关的参数（包括 $\theta$ 和信源幅度 $s_t$）和与[方差](@entry_id:200758)相关的参数（$\sigma^2$）之间是**块对角**的。这意味着，从估计 $\sigma^2$ 中获取的信息对于改善 $\theta$ 的估计没有任何帮助。因此，在渐近意义上，对噪声功率的无知并不会降低我们对信号方向的最终估计精度。这个比值为1的结果，揭示了该模型下一个深刻的统计特性。[@problem_id:2866454]