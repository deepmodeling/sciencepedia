## 引言
宇宙微波背景辐射（CMB）是[早期宇宙](@entry_id:160168)的快照，其[光子](@entry_id:145192)在穿越数十亿光年到达我们探测器的旅程中，路径会被宇宙大尺度结构的[引力场](@entry_id:169425)轻微偏折。这种被称为CMB[引力透镜](@entry_id:159000)的效应，将沿途所有物质[分布](@entry_id:182848)的信息微妙地编码在CMB的温度和偏振图中。精确地提取和解码这一透镜信号，对于理解暗物质、[暗能量](@entry_id:161123)以及宇宙结构的形成与演化至关重要。然而，这一信号并非直接可观测量，而是以一种微弱的非高斯统计[特征形式](@entry_id:198300)存在，对其进行稳健的重构构成了现代宇宙学数据分析中的一个核心挑战。本文旨在系统性地阐述解决这一挑战的主流技术：二次估计量方法。

通过本文，读者将全面了解二次估计量方法的理论与实践。第一章“原理与机制”将从物理根源出发，揭示[引力透镜](@entry_id:159000)如何破坏CMB的统计各向同性，并以此为基础构建二次估计量，同时讨论如何通过最优滤波来最大化其信噪比。第二章“应用与跨学科联系”将展示这一技术的强大科学价值，从测量透镜功率谱本身，到与[星系巡天](@entry_id:749696)进行[交叉](@entry_id:147634)关联，再到其在搜寻[原初引力波](@entry_id:161080)信号中作为“污染物”去除的关键作用——即去透镜化。最后，第三章“动手实践”将通过具体的编程练习，指导读者将理论付诸实践，亲手完成一个简化的透镜重构流程。这篇文章将带领你从基本概念深入到前沿分析技术，为理解和应用CMB[引力透镜](@entry_id:159000)重构奠定坚实的基础。

## 原理与机制

本章旨在阐述宇宙微波背景辐射（CMB）[引力透镜](@entry_id:159000)重构的基本原理，并深入探讨二次估计量方法的内在机制。我们将从引力透镜效应的物理和数学描述入手，揭示其如何打破CMB的统计各向同性，进而引出二次估计量的构建思想。随后，我们将讨论如何优化这些估计量以达到最高信噪比，并最终探讨在真实数据分析中遇到的关键挑战及其缓解策略。

### CMB[引力透镜效应](@entry_id:159000)的基础

CMB[光子](@entry_id:145192)从[最后散射面](@entry_id:266191)传播至今，其路径会被宇宙中的大尺度结构（如星系团和[暗物质晕](@entry_id:147523)）的[引力场](@entry_id:169425)所偏折。这种现象被称为CMB[引力透镜效应](@entry_id:159000)。在[弱引力透镜](@entry_id:158468)情况下，这种偏折效应可以被精确地模型化。

假设一个未经透镜效应影响的CM[B场](@entry_id:144179)，例如温度场$T(\hat{n})$或E模/B模偏振场，定义在[天球](@entry_id:158268)的方向向量$\hat{n}$上。[引力透镜效应](@entry_id:159000)将这个场重新映射，我们观测到的透镜化场$\tilde{T}(\hat{n})$实际上是源于天空中的另一个方向$\hat{n}'$：$\tilde{T}(\hat{n}) = T(\hat{n}')$。偏转角$\boldsymbol{\alpha} = \hat{n}' - \hat{n}$非常小，并且可以从一个标量势——**透镜势** (lensing potential) $\phi(\hat{n})$的梯度导出。

在一个空间平坦的Friedmann–Lemaître–Robertson–Walker (FLRW)宇宙中，并采用[牛顿规范](@entry_id:160348)下的[标量微扰](@entry_id:160338)，透镜势$\phi$可以表示为沿视线路径对[引力势](@entry_id:160378)$\Psi$的加权积分。在**[玻恩近似](@entry_id:138141)** (Born approximation)下，该积分沿着未受扰动的[光子](@entry_id:145192)路径进行。此时，透镜势、**偏转场** (deflection field) $\boldsymbol{d}(\hat{n})$以及场$X$（代表$T$或由偏振导出的标量场）的重映射关系可以精确地写为 [@problem_id:3467510]：

$$
\phi(\hat n) = -2\int_{0}^{\chi_*} \mathrm d\chi\,\frac{\chi_*-\chi}{\chi_* \chi}\,\Psi\big(\chi\,\hat n,\eta_0-\chi\big)
$$

$$
\boldsymbol{d}(\hat{n}) = \boldsymbol{\nabla}_{\hat{n}}\phi(\hat{n})
$$

$$
\tilde{X}(\hat{n}) = X\big(\hat{n} + \boldsymbol{d}(\hat{n})\big)
$$

这里，$\chi$是共形距离，$\chi_*$是到[最后散射面](@entry_id:266191)的共形距离，$\eta_0$是当前的[共形时间](@entry_id:263727)。$\boldsymbol{\nabla}_{\hat{n}}$是[天球](@entry_id:158268)上的角向[协变](@entry_id:634097)梯度。这个定义依赖于一系列关键假设：几何光学近似、弱透镜效应、线性[标量微扰](@entry_id:160338)、以及忽略[各向异性应力](@entry_id:161403)（使得两个标量[引力势](@entry_id:160378)相等，$\Psi = \Phi$）。[玻恩近似](@entry_id:138141)意味着我们忽略了[透镜-透镜耦合](@entry_id:751241)等高阶效应。

除了透镜势$\phi$，另一个密切相关的量是**透镜汇聚** (lensing convergence) $\kappa$，它描述了透镜效应引起的图像局部放大或缩小。在平坦天空近似下，它与偏转场的关系为$\kappa = -\frac{1}{2}\boldsymbol{\nabla} \cdot \boldsymbol{d}$。在傅里叶空间中，$\kappa(\boldsymbol{L}) = \frac{L^2}{2} \phi(\boldsymbol{L})$，其中$\boldsymbol{L}$是二维傅里叶波数。这意味着，对$\phi$的估计也直接给出了对$\kappa$的估计，它们的估计噪声[功率谱](@entry_id:159996)之间存在简单的代数关系$N_L^\kappa = \frac{L^4}{4}N_L^\phi$ [@problem_id:3467589]。

### 引力透镜作为统计各向同性的破坏者

原始CM[B场](@entry_id:144179)的一个基本属性是其**统计各向同性** (statistical isotropy)。这意味着其统计性质在天空的任何方向上都是相同的，并且不随[坐标系](@entry_id:156346)旋转而改变。在傅里叶（或球谐）空间中，这表现为不同模式之间的不相关性。对于两个任意的无透镜场$X$和$Y$，其傅里叶模式的[两点相关函数](@entry_id:185074)是对角的：

$$
\langle X_{\boldsymbol{\ell}}\, Y_{\boldsymbol{\ell}'} \rangle = (2\pi)^{2}\,\delta^{(2)}(\boldsymbol{\ell}+\boldsymbol{\ell}')\, C_{\ell}^{XY}
$$

其中$C_{\ell}^{XY}$是功率谱，仅依赖于[波数](@entry_id:172452)的模长$\ell=|\boldsymbol{\ell}|$，而$\delta^{(2)}$是二维狄拉克$\delta$函数。

然而，引力透镜效应打破了这种完美的统计各向同性。一个特定的透镜势$\phi$在天空中具有固定的结构，它不是各向同性的。当CMB[光子](@entry_id:145192)穿过这个结构时，这种各向异性便被“印”在了我们观测到的CM[B场](@entry_id:144179)上。

为了理解这一点，我们可以将透镜重映射关系$\tilde{X}(\boldsymbol{n}) = X(\boldsymbol{n} + \boldsymbol{d}(\boldsymbol{n}))$在一阶泰勒展开：

$$
\tilde{X}(\boldsymbol{n}) \approx X(\boldsymbol{n}) + \boldsymbol{d}(\boldsymbol{n}) \cdot \boldsymbol{\nabla} X(\boldsymbol{n}) = X(\boldsymbol{n}) + (\boldsymbol{\nabla}\phi(\boldsymbol{n})) \cdot (\boldsymbol{\nabla}X(\boldsymbol{n}))
$$

这个表达式清楚地显示，透镜化场包含一个原始场与透镜[势梯度](@entry_id:261486)和原始场梯度的乘积项。在傅里叶空间中，乘积变为卷积，这导致原本不相关的傅里叶模式之间产生耦合。给定一个固定的透镜势$\phi$的实现，我们可以计算透镜化场的[两点相关函数](@entry_id:185074)。其结果是，除了原始的对角项之外，还出现了一个与$\phi$成正比的**非对角** (off-diagonal)项 [@problem_id:3467538]：

$$
\langle \tilde{X}_{\boldsymbol{\ell}} \tilde{Y}_{\boldsymbol{\ell}'} \rangle_{\text{CMB}\,|\,\phi} \approx (2\pi)^{2}\,\delta^{(2)}(\boldsymbol{\ell}+\boldsymbol{\ell}')\, C_{\ell}^{XY} + \phi_{\boldsymbol{\ell}+\boldsymbol{\ell}'}\left[ (\boldsymbol{\ell}+\boldsymbol{\ell}')\cdot \boldsymbol{\ell}\, C_{\ell}^{XY} + (\boldsymbol{\ell}+\boldsymbol{\ell}')\cdot \boldsymbol{\ell}'\, C_{\ell'}^{XY} \right]
$$

这个表达式是[CMB透镜重构](@entry_id:747410)的理论基石。它表明，[波数](@entry_id:172452)为$\boldsymbol{\ell}$和$\boldsymbol{\ell}'$的CM[B模](@entry_id:161767)式之间的相关性，正比于波数为$\boldsymbol{L} = \boldsymbol{\ell}+\boldsymbol{\ell}'$的透镜势模式$\phi_{\boldsymbol{L}}$。因此，通过测量CM[B场](@entry_id:144179)中这些由透镜效应诱导的特定[模式耦合](@entry_id:752088)，我们原则上可以反演出透镜势$\phi$本身。

### 二次估计量的构建

上述的非对角相关性启发了一种重构$\phi$的方法。既然$\phi_{\boldsymbol{L}}$导致了$\tilde{X}_{\boldsymbol{\ell}}$和$\tilde{X}_{\boldsymbol{L}-\boldsymbol{\ell}}$之间的耦合，我们可以通过将观测到的CM[B场](@entry_id:144179)中的这些模式对相乘并求和，来构造一个对$\phi_{\boldsymbol{L}}$的估计量。由于该估计量是观测场$\tilde{X}$的二次方，因此被称为**二次估计量** (quadratic estimator)。

一个通用的二次估计量可以写成如下形式：

$$
\hat{\phi}(\boldsymbol{L}) = A_{L} \int \frac{d^{2}\boldsymbol{\ell}}{(2\pi)^{2}}\,\, g(\boldsymbol{\ell}, \boldsymbol{L}-\boldsymbol{\ell})\, \tilde{X}_{\boldsymbol{\ell}}\, \tilde{Y}_{\boldsymbol{L}-\boldsymbol{\ell}}
$$

其中$\tilde{X}$和$\tilde{Y}$是两个（可能相同的）观测到的CM[B场](@entry_id:144179)（如$T, E, B$），$g(\boldsymbol{\ell}, \boldsymbol{L}-\boldsymbol{\ell})$是一个权重函数，用于优化估计的信噪比，$A_L$是归一化因子，用于确保$\langle \hat{\phi}(\boldsymbol{L}) \rangle = \phi(\boldsymbol{L})$，即估计量是无偏的。

虽然在傅里叶空间中定义最为简洁，二次估计量也可以在[实空间](@entry_id:754128)中理解。傅里叶空间中的卷积对应于[实空间](@entry_id:754128)中的乘积。我们可以定义两个经过不同滤波器$K_a, K_b$滤波的CMB图$T_a = K_a * \tilde{T}$ 和 $T_b = K_b * \tilde{T}$。那么，一个实空间估计量可以由这些滤波图的局域乘积及其导数构成。例如，一个对透镜汇聚$\kappa$的估计量可以从$\nabla \cdot (T_a \nabla T_b)$构建，并通过一个归一化核函数进行[反卷积](@entry_id:141233)得到[无偏估计](@entry_id:756289) [@problem_id:3467584]。这提供了一个更直观的图像：透镜效应在CMB图中引入的畸变，可以通过比较经过不同滤波的场的局域梯度和强度信息来探测。

### 优化估计量：滤波与多描图组合

为了获得最精确的透镜势图，我们需要精心设计估计量。这主要涉及两个方面：为单个估计量选择最优的滤波器，以及组合来自不同CM[B场](@entry_id:144179)（$T, E, B$）的信息。

#### 最优滤波

二次估计量中的权重函数$g$（或等价地，[实空间](@entry_id:754128)中的滤波器$K$）并非任意选择。其目的是在满足无偏性约束的同时，最小化估计量$\hat{\phi}$的[方差](@entry_id:200758)（即重构噪声）。

在一个简化的框架下，假设我们使用一个预滤波器$F_\ell$作用于观测到的CMB图，那么估计量的噪声$N_L^{(0)}$将与滤波后场的[方差](@entry_id:200758)成正比，即$\int d^2\boldsymbol{\ell} \, F_\ell^2 C_\ell^{\text{tot}}$，其中$C_\ell^{\text{tot}} = C_\ell^{\text{CMB}} + N_\ell^{\text{noise}}$是信号和仪器噪声的总功率谱。同时，为了保证估计量无偏，滤波器需要满足一个[归一化条件](@entry_id:156486)，形式为$\int d^2\boldsymbol{\ell} \, F_\ell S_\ell = 1$，其中$S_\ell$是一个给定的响应核函数。

利用柯西-施瓦茨不等式，可以证明最小化[方差](@entry_id:200758)的[最优滤波器](@entry_id:262061)$F_\ell$具有如下形式 [@problem_id:3467521]：

$$
F_\ell \propto \frac{S_\ell}{C_\ell^{\text{tot}}} = \frac{S_\ell}{C_\ell^{\text{CMB}} + N_\ell^{\text{noise}}}
$$

这个结果的物理意义是，[最优滤波器](@entry_id:262061)在“模板”形状（由$S_\ell$决定）和[噪声抑制](@entry_id:276557)（通过对总功率$C_\ell^{\text{tot}}$大的模式赋予低权重）之间取得了平衡。

*   **[维纳滤波器](@entry_id:264227) (Wiener-type filter):** 如果我们[选择响应](@entry_id:267049)核$S_\ell$与CMB信号功率谱$C_\ell^{\text{CMB}}$成正比，这对应于使用信号自身的谱形状作为模板。此时[最优滤波器](@entry_id:262061)为$F_\ell \propto C_\ell^{\text{CMB}} / C_\ell^{\text{tot}}$。这种滤波器被称为[维纳滤波器](@entry_id:264227)，它优先考虑[信噪比](@entry_id:185071)高的模式。
*   **反[方差](@entry_id:200758)权重 (Inverse-variance weighting):** 如果我们对信号的谱形状不可知或选择忽略它，可以取$S_\ell=1$。此时[最优滤波器](@entry_id:262061)为$F_\ell \propto 1/C_\ell^{\text{tot}}$。这是一种纯粹的反[方差](@entry_id:200758)加权方案。

通常，[维纳滤波器](@entry_id:264227)利用了更多关于信号的先验知识，因此在信号谱形状已知且具有显著特征（如CMB[声学峰](@entry_id:746227)）时，性能更优。

#### 组合不同示踪剂

CMB的温度和偏振场都受到[引力透镜](@entry_id:159000)的影响，因此我们可以构建多个二次估计量，例如TT, EE, EB, TE等。每种估计量都有其自身的[信噪比](@entry_id:185071)特性。为了获得最精确的全局估计，我们将这些独立的估计量进行**最小[方差](@entry_id:200758) (minimum-variance, MV)**组合。这本质上是一种反噪声[方差](@entry_id:200758)加权平均：

$$
\hat{\phi}_{\text{MV}} = \frac{\sum_X N_L^{-1, X} \hat{\phi}_X}{\sum_X N_L^{-1, X}}
$$

其中$X$遍历所有估计量（TT, EE, EB, ...），$\hat{\phi}_X$是来自$X$渠道的估计量，$N_L^{-1, X}$是其对应的反噪声[功率谱](@entry_id:159996)（也称为[信息量](@entry_id:272315)）。

不同估计量的相对重要性取决于[CMB功率谱](@entry_id:158529)的形状和仪器噪声的水平。例如，在重构小尺度（高$L$）透镜模式时，我们需要依赖高$\ell$的CM[B模](@entry_id:161767)式。
*   温度功率谱$C_\ell^{TT}$在高$\ell$处由于Silk阻尼效应而呈指数衰减，其梯度$dC_\ell^{TT}/d\ell$变得很小。由于估计量的响应正比于此梯度，TT估计量在高$\ell$处的效率会降低。
*   相比之下，$E$模偏振[功率谱](@entry_id:159996)$C_\ell^{EE}$在高$\ell$处仍然保留着显著的[声学振荡](@entry_id:161154)结构，具有陡峭的梯度。这为EE和EB估计量提供了强大的响应信号 [@problem_id:3G7516]。

因此，即使偏振探测器的噪声水平通常高于温度探测器，对于高分辨率、低噪声的下一代CMB实验，偏振（特别是EB和EE）估计量在重构小尺度透镜模式时也可能超越温度估计量。一个更定量的分析，例如在仪器噪声主导的高$\ell$极限下，可以推导出EB和TT估计量对总[信息量](@entry_id:272315)的相对贡献$R(L) = N_L^{-1, EB} / N_L^{-1, TT}$，它明确依赖于CMB谱的振幅、仪器噪声水平和[望远镜分辨率](@entry_id:170098) [@problem_id:3467552]。

### 实际应用中的挑战与缓解策略

将二次估计量方法应用于真实的CMB观测数据时，会遇到一系列系统性挑战。其中最主要的两个是[前景污染](@entry_id:749514)和不完整的巡天覆盖。

#### 非高斯[前景污染](@entry_id:749514)

CMB观测图包含了来自我们银河系和河外星系的前景辐射。其中一些前景，如热Sunyaev-Zeldovich (tSZ)效应和宇宙红外背景 (CIB)，其本身是非高斯的。这意味着它们具有非零的内禀连通四点[相关函数](@entry_id:146839)，即**三谱** (trispectrum)。

二次估计量本质上是测量CM[B场](@entry_id:144179)的四点相关函数。当应用于包含非高斯前景的[总温](@entry_id:143265)度图时，前景的内禀三谱会给估计量的自相关功率谱引入一个额外的贡献。这个贡献与透镜信号无关，但形式上与透镜功率谱无法区分，从而产生一个**加性偏置** (additive bias) $\Delta C_L^{\phi\phi}$ [@problem_id:3467514]。在一个简化的“白色三谱”模型下，即前景三谱$T_0$为常数，这个偏置可以被解析地计算出来，其大小正比于$T_0$和估计量权重函数的积分的平方。在实际分析中，这个前景偏置必须通过多频段[数据清洗](@entry_id:748218)或专门的模板扣除技术来精确移除，否则会严重污染[宇宙学参数](@entry_id:161338)的推断。

#### 不完整的巡天覆盖与掩模效应

由于银河系银道面等区域的强[前景污染](@entry_id:749514)或巡天策略的限制，我们永远无法获得完美的全天CMB图。分析时必须使用一个**掩模** (mask)或**窗口函数** (window function) $W(\boldsymbol{x})$来排除污染区域。将二次估计量应用于[加窗](@entry_id:145465)后的场$T_W(\boldsymbol{x}) = W(\boldsymbol{x}) T(\boldsymbol{x})$会引入两个主要的系统误差。

1.  **平均场偏置 (Mean-field bias):** 即使在没有透镜效应的天图上，掩模的尖锐边界也会打破[统计均匀性](@entry_id:136481)，并与CMB的内禀相关性相互作用，为二次估计量产生一个非零的[期望值](@entry_id:153208)$\langle \hat{\phi}(\boldsymbol{L}) \rangle \neq 0$。这个虚假的平均信号被称为**平均场**。可以证明，平均场的主要来源是窗口函数梯度的平方$|\nabla W|^2$ [@problem_id:3467536]。为了抑制这种效应，需要对掩模的边界进行平滑处理，即**[切趾](@entry_id:147798)平滑**。

2.  **归一化修正 (Normalization correction):** 窗口函数减少了有效的巡天面积，从而改变了估计量的响应和[方差](@entry_id:200758)。这导致估计量的归一化因子$A_L$需要修正。在一定近似下，这个修正因子正比于窗口函数平方的全图平均值 $\int W^2(\boldsymbol{x}) d^2\boldsymbol{x}$ [@problem_id:3467536]。

一个理想的窗口函数应该在最小化平均场偏置的同时，保持估计量的归一化不变。这构成了一个变分[优化问题](@entry_id:266749)：在归一化约束$\frac{1}{A} \int W^2 d^2\boldsymbol{x} = 1$下，最小化[Dirichlet能量](@entry_id:276589)$\int |\nabla W|^2 d^2\boldsymbol{x}$。对于一个方形观测区域，这个问题的解是正弦函数构成的[基模](@entry_id:165201) [@problem_id:3467536]。

对于形状复杂的掩模和空间变化的噪声，解析计算平均场变得不可行。此时，必须采用**[蒙特卡洛模拟](@entry_id:193493)** (Monte Carlo simulation)的方法来估计和扣除平均场。具体做法是生成大量无透镜但包含同样掩模和噪声特性的模拟CMB图，对它们应用二次估计量，然后取平均得到平均场的估计$\widehat{\text{MF}}$。

这个模拟估计本身也存在[统计误差](@entry_id:755391)。根据[中心极限定理](@entry_id:143108)，使用$N_{\text{sim}}$个模拟得到的平均场估计的残余标准差$\sigma_{\text{resid}}$，与单次估计的统计标准差$\sigma_{\hat{\phi}}$之间满足关系 [@problem_id:3467586]：

$$
\sigma_{\text{resid}} = \frac{\sigma_{\hat{\phi}}}{\sqrt{N_{\text{sim}}}}
$$

为了将平均场扣除引入的额外[误差控制](@entry_id:169753)在可接受范围内（例如，小于[统计误差](@entry_id:755391)的某个比例$r$），所需的模拟数量为$N_{\text{sim,min}} = \lceil 1/r^2 \rceil$。这个简单的关系凸显了在现代高精度CMB分析中，进行大量[数值模拟](@entry_id:137087)以控制系统误差的极端重要性。