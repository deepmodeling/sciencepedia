## 引言
在现代精准宇宙学中，结合多种观测探针是最大化科学回报的关键策略。然而，单一探针的分析往往受限于其固有的系统误差、噪声特性以及宇宙[方差](@entry_id:200758)这一基本统计极限。[宇宙学探针](@entry_id:160927)间的互[相关分析](@entry_id:265289)应运而生，它通过比较来自不同实验或观测窗口的数据，不仅能够提取出被噪声淹没的微弱信号，还能有效诊断并削弱不相关的系统误差，从而成为突破单一探针瓶颈的强大武器。

本文将系统性地引导读者深入理解这一关键技术。在第一章**“原理与机制”**中，我们将奠定互[相关分析](@entry_id:265289)的数学和物理基础，从互[功率谱](@entry_id:159996)的定义、估计方法到其理论建模和统计性质。接着，在第二章**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将展示[互相关](@entry_id:143353)在真实科研场景中的广泛应用，包括测量[宇宙学参数](@entry_id:161338)、校准观测特性以及检验基础物理定律。最后，第三章**“动手实践”**将通过一系列精心设计的计算问题，帮助读者将理论知识转化为解决实际问题的能力。通过这三章的学习，读者将掌握互[相关分析](@entry_id:265289)的核心思想，并了解其在揭示宇宙奥秘的前沿研究中所扮演的重要角色。

## 原理与机制

### 互[功率谱](@entry_id:159996)：定义与估计

在宇宙学中，我们研究的大尺度结构（Large-Scale Structure, LSS）和宇宙微波背景（Cosmic Microwave Background, CMB）等可观测场，通常被建模为[天球](@entry_id:158268)上的投影场。对于任意两个这样的场，例如 $X(\hat{\boldsymbol{n}})$ 和 $Y(\hat{\boldsymbol{n}})$，它们之间的[统计关联](@entry_id:172897)性可以通过[两点相关函数](@entry_id:185074)来描述。在谐空间（harmonic space）中，这种关联性由[角功率谱](@entry_id:161125)（angular power spectrum）来量化。

当[天球](@entry_id:158268)上的两个场相同时，我们计算其**自功率谱**（auto-power spectrum），记为 $C_{\ell}^{XX}$。当两个场不同时，我们计算**互[功率谱](@entry_id:159996)**（cross-power spectrum），记为 $C_{\ell}^{XY}$。这些功率谱是多极矩 $\ell$ 的函数，反映了不同角尺度上的相关性强度。

为了从观测数据中估计这些量，我们首先将[天球](@entry_id:158268)上的场 $A(\hat{\boldsymbol{n}})$ 分解为球谐系数 $a_{\ell m}^{A}$：
$$
a_{\ell m}^{A} = \int d\hat{\boldsymbol{n}}\, A(\hat{\boldsymbol{n}})\,Y_{\ell m}^{*}(\hat{\boldsymbol{n}})
$$
其中 $Y_{\ell m}(\hat{\boldsymbol{n}})$ 是[球谐函数](@entry_id:178380)。在统计各向同性（statistical isotropy）的假设下，不同 $\ell$ 和 $m$ 的模式是[相互独立](@entry_id:273670)的，并且其系综平均满足：
$$
\langle a_{\ell m}^{A} (a_{\ell' m'}^{B})^{*} \rangle = \delta_{\ell\ell'} \delta_{mm'} C_{\ell}^{AB}
$$
其中 $\langle \cdot \rangle$ 表示系综平均，$\delta$ 是克罗内克符号，$C_{\ell}^{AB}$ 是真实的[角功率谱](@entry_id:161125)。

基于此，我们可以构建一个针对全天（full-sky）观测的互功率谱的[无偏估计量](@entry_id:756290) **$\hat{C}_{\ell}^{XY}$**。这个估计量是通过对给定 $\ell$ 下所有方位模式 $m$ 的系[数乘](@entry_id:155971)积进行平均得到的 ：
$$
\hat{C}_{\ell}^{XY} \equiv \frac{1}{2\ell+1} \sum_{m=-\ell}^{\ell} a_{\ell m}^{X} a_{\ell m}^{Y*}
$$
为了验证其无偏性，我们计算它的[期望值](@entry_id:153208)。考虑到观测系数 $a_{\ell m}$ 通常是真实宇宙学信号 $s_{\ell m}$ 和不相关的噪声 $n_{\ell m}$ 之和，即 $a_{\ell m}^{X} = s_{\ell m}^{X} + n_{\ell m}^{X}$。如果两项观测中的噪声 $n_{\ell m}^X$ 和 $n_{\ell m}^Y$ 是不相关的（例如，来自不同的仪器或观测），那么 $\langle n_{\ell m}^{X} (n_{\ell m}^{Y})^* \rangle = 0$。因此，估计量的[期望值](@entry_id:153208)为：
$$
\langle \hat{C}_{\ell}^{XY} \rangle = \frac{1}{2\ell+1} \sum_{m=-\ell}^{\ell} \langle (s_{\ell m}^{X} + n_{\ell m}^{X}) (s_{\ell m}^{Y} + n_{\ell m}^{Y})^* \rangle = \frac{1}{2\ell+1} \sum_{m=-\ell}^{\ell} \langle s_{\ell m}^{X} (s_{\ell m}^{Y})^* \rangle = C_{\ell}^{XY}
$$
这表明，在噪声不相关的前提下，互[功率谱](@entry_id:159996)的估计是无偏的，即它不受各自观测中独立噪声功率的偏置影响。这是互[相关分析](@entry_id:265289)的首要优势之一。

### 互功率谱的理论建模

为了从测量的互功率谱中提取宇宙学信息，我们必须能够从理论上预测其形态和幅度。大多数[宇宙学探针](@entry_id:160927)，如星系密度或[弱引力透镜效应](@entry_id:158468)，都可以被看作是三维[物质密度](@entry_id:263043)扰动场 $\delta(\mathbf{x}, z)$ 沿着视线方向的加权积分。一个投影场 $A(\hat{\boldsymbol{n}})$ 可以表示为：
$$
A(\hat{\boldsymbol{n}}) = \int dz\, W_A(z)\, \delta(\chi(z)\hat{\boldsymbol{n}}, z)
$$
其中 $z$ 是红移，$\chi(z)$ 是到该[红移](@entry_id:159945)的同移距离，$W_A(z)$ 是探针 $A$ 的**径向[核函数](@entry_id:145324)**（radial kernel），它描述了不同[红移](@entry_id:159945)处的物质扰动对最终二维投影的贡献权重。

在 **[林伯近似](@entry_id:751282)**（Limber approximation）下，两个投影场 $A$ 和 $B$ 的角互功率谱 $C_{\ell}^{AB}$ 可以直接与三维[物质功率谱](@entry_id:161407) $P(k, z)$ 联系起来 ：
$$
C_{\ell}^{AB} = \int dz\, \frac{W_A(z) W_B(z)}{\chi^2(z)} P\left(k = \frac{\ell+1/2}{\chi(z)}, z\right)
$$
这个公式是连接理论与观测的核心桥梁。它表明，角互[功率谱](@entry_id:159996)的形状和幅度取决于两个探针核函数的乘积（即它们的重叠部分）以及[物质功率谱](@entry_id:161407)本身。

一个具体的例子是[星系成团](@entry_id:158300)（galaxy clustering）与宇宙学剪切（cosmic shear）的[互相关](@entry_id:143353)，即所谓的“星系-星系透镜效应”。
- 对于星系密度场 $g_i$，其核函数 $W_{g_i}(z)$ 主要由该星系样本的[红移分布](@entry_id:157730) $n_i(z)$ 和星系偏袒 $b_g(z)$ 决定：$W_{g_i}(z) = b_g(z) n_i(z)$。
- 对于源星系位于红移切片 $j$ 的[弱引力透镜](@entry_id:158468)汇聚场 $\kappa_j$，其核函数 $W_{\kappa_j}(z)$ 则由广义相对论给出。它描述了位于[红移](@entry_id:159945) $z$ 的前景物质如何使来自更高红移 $z_s > z$ 的背景星系（其[分布](@entry_id:182848)为 $n_j^s(z_s)$）的[光线偏折](@entry_id:269868)。在[平坦宇宙](@entry_id:183782)中，该[核函数](@entry_id:145324)（每单位同移距离）为 ：
$$
W_{\kappa_{j}}(z) = \frac{3}{2}\,\Omega_{m}\,H_{0}^{2}\,(1+z)\,\chi(z)\,\int_{z}^{\infty}dz_{s}\,n^{s}_{j}(z_{s})\,\frac{\chi(z_{s})-\chi(z)}{\chi(z_{s})}
$$
其中 $\Omega_m$ 是当前物质密度参数，$H_0$ 是哈勃常数。将这两个核函数代入林伯公式，我们就可以为星系-汇聚互功率谱 $C_{\ell}^{g_i \kappa_j}$ 建立一个依赖于[宇宙学参数](@entry_id:161338)和星系属性的完整理论模型。

### 统计性质与[似然](@entry_id:167119)分析

精确的[宇宙学参数](@entry_id:161338)推断要求我们不仅要有一个准确的理论模型，还需要对测量的不确定性有精确的描述。这体现在[似然函数](@entry_id:141927)（likelihood function）的构建中，而[似然函数](@entry_id:141927)的核心是数据的[协方差矩阵](@entry_id:139155)。

对于[高斯随机场](@entry_id:749757)，功率谱[估计量的[方](@entry_id:167223)差](@entry_id:200758)和协[方差](@entry_id:200758)可以从理论上推导。单个互[功率谱估计](@entry_id:753656)量 $\hat{C}_{\ell}^{XY}$ 的[方差](@entry_id:200758)，即所谓的**高斯[方差](@entry_id:200758)**（Gaussian variance），可以推广到包含噪声的情况 ：
$$
\mathrm{Var}(\hat{C}_{\ell}^{XY}) = \frac{1}{(2\ell+1)f_{\mathrm{sky}}} \left[ (C_{\ell}^{XY})^2 + (C_{\ell}^{XX} + N_{\ell}^{X})(C_{\ell}^{YY} + N_{\ell}^{Y}) \right]
$$
其中 $N_{\ell}^{X}$ 和 $N_{\ell}^{Y}$ 分别是探针 $X$ 和 $Y$ 的自[功率谱](@entry_id:159996)中的噪声功率（例如，[星系巡天](@entry_id:749696)中的泊松噪声或CMB实验中的仪器噪声），$f_{\mathrm{sky}}$ 是观测天区的面积分数，用于近似修正因天空覆盖不全而减少的独立模式数量。该[方差](@entry_id:200758)由两部分组成：第一项 $(C_{\ell}^{XY})^2$ 是信号自身的样本[方差](@entry_id:200758)（sample variance），第二项则包含了两个场的总功率（信号加噪声），反映了测量过程中的不确定性。

在现代宇宙学分析中，我们通常同时分析多个功率谱，包括自谱和互谱。因此，我们需要一个完整的**[协方差矩阵](@entry_id:139155)**（covariance matrix）。对于任意四个场 $X, Y, U, V$，其[功率谱估计](@entry_id:753656)量之间的协[方差](@entry_id:200758)由一个通用的“Knox公式”给出 ：
$$
\mathrm{Cov}(\hat{C}_{\ell}^{XY}, \hat{C}_{\ell'}^{UV}) = \frac{\delta_{\ell\ell'}}{(2\ell+1)f_{\mathrm{sky}}} \left[ \tilde{C}_{\ell}^{XU}\tilde{C}_{\ell}^{YV} + \tilde{C}_{\ell}^{XV}\tilde{C}_{\ell}^{YU} \right]
$$
其中 $\tilde{C}_{\ell}^{AB} = C_{\ell}^{AB} + N_{\ell}^{AB}$ 是包含信号和噪声的总功率谱。这个公式是所有高斯协[方差](@entry_id:200758)计算的基础。

以一个包含两个场 $X$ 和 $Y$ 的分析为例，我们通常会测量数据向量 $\hat{\mathbf{C}}_{\ell} = (\hat{C}_{\ell}^{XX}, \hat{C}_{\ell}^{YY}, \hat{C}_{\ell}^{XY})^{\mathsf{T}}$。利用上述Knox公式，我们可以构建出 $3 \times 3$ 的[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}_{\ell}$ 。其对角[线元](@entry_id:196833)素为[方差](@entry_id:200758)，非对角线元素为协[方差](@entry_id:200758)，例如：
$$
\mathrm{Cov}(\hat{C}_{\ell}^{XX}, \hat{C}_{\ell}^{YY}) = \frac{2}{(2\ell+1)f_{\mathrm{sky}}} (C_{\ell}^{XY})^2
$$
$$
\mathrm{Cov}(\hat{C}_{\ell}^{XX}, \hat{C}_{\ell}^{XY}) = \frac{2}{(2\ell+1)f_{\mathrm{sky}}} \tilde{C}_{\ell}^{XX} C_{\ell}^{XY}
$$
这些协[方差](@entry_id:200758)项的存在意味着不同的功率谱测量并非[相互独立](@entry_id:273670)，必须在似然分析中予以考虑。

在 **高斯[似然](@entry_id:167119)近似**（Gaussian likelihood approximation）下，我们假设数据向量 $\hat{\mathbf{C}}_{\ell}$ 服从多元[高斯分布](@entry_id:154414)。如果不同 $\ell$ 之间的协[方差](@entry_id:200758)可以忽略（即块[对角近似](@entry_id:270948)），则总的[对数似然函数](@entry_id:168593) $\ln \mathcal{L}$ 是各个 $\ell$ 的对数似然之和：
$$
\ln \mathcal{L} = \sum_{\ell} \ln \mathcal{L}_{\ell} = -\frac{1}{2} \sum_{\ell} \left[ (\hat{\mathbf{C}}_{\ell} - \mathbf{m}_{\ell})^{\mathsf{T}} \boldsymbol{\Sigma}_{\ell}^{-1} (\hat{\mathbf{C}}_{\ell} - \mathbf{m}_{\ell}) + \ln \det \boldsymbol{\Sigma}_{\ell} + \text{const.} \right]
$$
其中 $\mathbf{m}_{\ell} = \langle \hat{\mathbf{C}}_{\ell} \rangle$ 是理论模型预测的[均值向量](@entry_id:266544)。通过最大化这个[似然函数](@entry_id:141927)（或在[贝叶斯分析](@entry_id:271788)中探索其[后验概率](@entry_id:153467)），我们便可以对[宇宙学参数](@entry_id:161338)进行约束。

### [互相关](@entry_id:143353)的威力：削弱系统误差与宇宙[方差](@entry_id:200758)

进行互[相关分析](@entry_id:265289)的主要动机在于其能够有效地应对自[相关分析](@entry_id:265289)中难以处理的某些挑战，特别是系统误差和[统计不确定性](@entry_id:267672)。

#### 系统误差削弱

**1. 不相关的加性系统误差 (Additive Systematics)**
许多观测会受到与宇宙学信号不相关的加性污染，例如未被减除的仪器噪声或前景残留。如果我们将观测模型写为 $X_{\mathrm{obs}}(\hat{\boldsymbol{n}}) = X_{\mathrm{true}}(\hat{\boldsymbol{n}}) + a_X(\hat{\boldsymbol{n}})$，其中 $a_X$ 是加性系统误差，那么自功率谱的[期望值](@entry_id:153208)会包含一个偏置项：$\langle \hat{C}_{\ell}^{XX} \rangle = C_{\ell, \mathrm{true}}^{XX} + C_{\ell}^{aa,X}$。然而，在互[功率谱](@entry_id:159996)中，如果两个探针 $X$ 和 $Y$ 的加性系统误差 $a_X$ 和 $a_Y$ 是不相关的（$\langle a_X a_Y \rangle = 0$），它们的贡献项在[期望值](@entry_id:153208)中会消失 ：
$$
\langle \hat{C}_{\ell}^{XY} \rangle = \langle (X_{\mathrm{true}}+a_X)(Y_{\mathrm{true}}+a_Y)^* \rangle = C_{\ell, \mathrm{true}}^{XY}
$$
这种“自动清洁”的特性使得[互相关](@entry_id:143353)成为一种强大的诊断工具，能够揭示在[自相关](@entry_id:138991)中被污染淹没的真实宇宙学信号。即便加性前景 $F$ 与其中一个探针 $X$ 相关，其在互谱中的表现形式也十分简单，即一个偏置项 $\Delta C_{\ell}^{XY} = \epsilon C_{\ell}^{XF}$，其中 $\epsilon$ 是泄漏幅度 。这种简单的形式为建模和移除[前景污染](@entry_id:749514)提供了可能。

**2. 乘性定标偏差与自定标 (Multiplicative Bias and Self-Calibration)**
仪器的定标不准或模型中的某些参数误差会导致信号被乘上一个未知的因子，即 $X_{\mathrm{obs}} = (1+m_X) X_{\mathrm{true}}$。在互相关中，这种偏差会以乘积形式出现：$C_{\ell, \mathrm{obs}}^{XY} = (1+m_X)(1+m_Y) C_{\ell, \mathrm{true}}^{XY}$。它们并不会相互抵消。然而，互相关提供了一种强大的**自定标**（self-calibration）方法。

假设我们有第三个探针 $Z$，其定标是准确的（$m_Z=0$），例如来自CMB实验的透镜场。通过测量 $X$ 和 $Y$ 与 $Z$ 的[互相关](@entry_id:143353) $C_{\ell, \mathrm{obs}}^{XZ}$ 和 $C_{\ell, \mathrm{obs}}^{YZ}$，我们可以分离出各自的定标因子。由于 $C_{\ell, \mathrm{obs}}^{XZ} = (1+m_X) C_{\ell}^{XZ}$，我们可以通过将观测数据与一个理论模板 $T_{\ell}^{XZ}$ 进行拟合，来求解定标因子 $(1+m_X)$ 。一个统计上最优的估计量是：
$$
\widehat{(1+m_{X})} = \frac{\sum_{\ell} w_{\ell}^{XZ}\,C_{\ell,\mathrm{obs}}^{XZ}\,T_{\ell}^{XZ}}{\sum_{\ell} w_{\ell}^{XZ}\,(T_{\ell}^{XZ})^{2}}
$$
其中 $w_\ell$ 是逆[方差](@entry_id:200758)权重。通过这种方式，我们可以独立地确定 $m_X$ 和 $m_Y$，然后用它们来校正我们真正感兴趣的 $C_{\ell}^{XY}$ 测量，从而打破定标参数与[宇宙学参数](@entry_id:161338)之间的简并性。

#### 宇宙[方差](@entry_id:200758)削弱

**宇宙[方差](@entry_id:200758)**（cosmic variance）是指由于我们只能观测我们宇宙中的一个实现，而不是所有可能实现的系综平均，而产生的基本[统计不确定性](@entry_id:267672)。对于一个密度场，这种不确定性表现为特定模式的随机相位。

**[多示踪剂技术](@entry_id:752263)**（multi-tracer technique）利用互相关来削弱宇宙[方差](@entry_id:200758)的影响。其原理是，如果我们用两个或更多具有不同偏袒（bias）的示踪剂（例如，两种不同类型的星系 $g_1$ 和 $g_2$）来追踪同一个潜在的物质密度场，那么它们在观测上的差异就主要源于各自的泊松噪声，而不是共同的宇宙[方差](@entry_id:200758)。

考虑测量两个星系样本 $g_1$ 和 $g_2$ 与CMB透镜场 $\kappa$ 的[互相关](@entry_id:143353) 。数据向量是 $(\hat{C}_\ell^{\kappa g_1}, \hat{C}_\ell^{\kappa g_2})$。由于两个测量共享同一个 $\kappa$ 场，它们的[测量误差](@entry_id:270998)是相关的，其协[方差](@entry_id:200758)中会包含一个由 $C_\ell^{\kappa\kappa}$ 主导的项。如果星系偏袒 $b_1 \neq b_2$，那么宇宙学信号（例如对 $\sigma_8$ 的响应）在二维数据空间中的方向与主要的[方差](@entry_id:200758)方向是不同的。通过对这两个观测量进行一个最优的[线性组合](@entry_id:154743)，可以构建一个新的观测量，其对共同的 $\kappa$ 场涨落不敏感，从而有效地“消除”了部分宇宙[方差](@entry_id:200758)，最终获得比任何单一示踪剂所能达到的更强的[宇宙学参数](@entry_id:161338)约束。当 $b_1 = b_2$ 时，两个示踪剂变得简并，这种方法便会失效。

### 互[相关分析](@entry_id:265289)中的挑战与前沿课题

尽管互[相关分析](@entry_id:265289)非常强大，但在实际应用中也面临着一系列挑战，这些挑战是当前宇宙学研究的前沿领域。

#### 观测效应：不完整的巡天与[模式耦合](@entry_id:752088)

实际的观测总是在有限的天区上进行的，并且会受到明亮恒星或仪器故障等因素的影响，需要用**掩模**（mask）来剔除部分区域。这导致我们测量的不再是真实的球谐系数，而是被掩模场 $M(\hat{\boldsymbol{n}})$ 调制过的场的系数。直接从掩模后的场计算出的[功率谱](@entry_id:159996)被称为**[伪谱](@entry_id:138878)**（pseudo-spectrum）$\tilde{C}_\ell$。

[伪谱](@entry_id:138878)与真实谱的关系通过一个**[模式耦合](@entry_id:752088)矩阵**（mode-coupling matrix）$M_{\ell\ell'}$ 来描述 ：
$$
\langle \tilde{C}_{\ell}^{XY} \rangle = \sum_{\ell'} M_{\ell \ell'}^{XY} C_{\ell'}^{XY}
$$
这个矩阵将不同 $\ell'$ 的真实功率“泄漏”到我们测量的 $\ell$ 模式中。该矩阵本身由掩模的功率谱 $W_L^{XY}$ 决定：
$$
M_{\ell \ell'}^{XY} = \sum_{L} \frac{(2\ell'+1)(2L+1)}{4\pi} W_{L}^{XY} \begin{pmatrix} \ell  \ell'  L \\ 0  0  0 \end{pmatrix}^2
$$
其中 $\begin{pmatrix} \cdot  \cdot  \cdot \\ \cdot  \cdot  \cdot \end{pmatrix}$ 是[Wigner 3j符号](@entry_id:163869)。处理[模式耦合](@entry_id:752088)是所有实际[功率谱分析](@entry_id:158761)的关键一步，通常需要通过解一个大型[线性方程组](@entry_id:148943)（即“去耦合”）或在理论模型端进行正向卷积来完成。这种耦合也导致了不同 $\ell$ 模式测量值之间的协[方差](@entry_id:200758)，破坏了前面提到的协方差矩阵的[块对角结构](@entry_id:746869)。

#### 天体物理与分析系统误差

与不相关的加性误差不同，某些系统误差本身就是相关的，或者与宇宙学信号物理相关，因此无法在[互相关](@entry_id:143353)中简单地消除。

**1. [内禀排列](@entry_id:162059) (Intrinsic Alignments, IA)**
星系的形状和方向并不仅仅由[引力透镜效应](@entry_id:159000)决定，它们自身的形成和演化也会受到周围大尺度结构[引力](@entry_id:175476)[潮汐](@entry_id:194316)场的影响，这种效应被称为**[内禀排列](@entry_id:162059)**。在星系密度-剪切互相关中，前景星系的位置与背景星系（被用作剪切测量的源）的内禀形状相关，因为它们都受到相同[大尺度结构](@entry_id:158990)的影响。这导致了一个额外的、非宇宙学透镜效应的信号项 $C_{\ell}^{gI}$，它会污染并偏置从 $C_{\ell}^{g\gamma}$ 中提取的宇宙学信息 。IA是当前[弱引力透镜](@entry_id:158468)宇宙学分析中最主要的物理系统误差之一。

**2. 重子反馈 (Baryonic Feedback)**
[活动星系核](@entry_id:158029)（AGN）反馈和[恒星形成](@entry_id:159940)过程会重新[分布](@entry_id:182848)[星系团](@entry_id:160919)和星系内部的物质，这种**重子反馈**效应会改变中小尺度上的[物质功率谱](@entry_id:161407) $P(k,z)$。由于所有基于物质[分布](@entry_id:182848)的探针（如星系密度、透镜效应）都会受到这种改变的影响，它是一个“共同模式”的物理效应。它不会在[互相关](@entry_id:143353)中抵消，而是会同样地改变自谱和互谱的理论预测 。精确地为这些效应建模是未来高精度宇宙学分析的重大挑战。

**3. [红移分布](@entry_id:157730)不确定性 (Redshift Distribution Uncertainty)**
林伯积分表明，[功率谱](@entry_id:159996)的预测值对径向核函数 $W(z)$ 非常敏感，而核函数又依赖于我们对星系样本[红移分布](@entry_id:157730) $n(z)$ 的了解。对于通过测光数据选择的星系样本，其[红移](@entry_id:159945)（光度红移，$z_{\mathrm{ph}}$）存在不确定性。这种不确定性通常被建模为一个[条件概率分布](@entry_id:163069) $p(z_{\mathrm{ph}}|z)$，包含一个偏差 $b_z$ 和一个散射 $\sigma_p$。这些误差会导致观测到的有效核函数 $W_{\mathrm{eff}}(z)$ 与真实的核函数不同。例如，在一个简化的模型中，这种误差会导致对互相关信号幅度的[乘性](@entry_id:187940)偏差 $m$，其大小不仅依赖于 $b_z$ 和 $\sigma_p$，还依赖于两个互相关探针的核函数的相对位置和宽度 。精确校准 $n(z)$ 是所有大尺度结构分析的基石。

#### [统计模型](@entry_id:165873)的局限性

我们之前构建的高斯[似然](@entry_id:167119)是许多分析的出发点，但其有效性有其边界。
- **非高斯性 (Non-Gaussianity)**：在小尺度上，[引力](@entry_id:175476)演化是[非线性](@entry_id:637147)的，导致物质密度场呈现显著的**非高斯性**。这会产生一个非零的连通四点[相关函数](@entry_id:146839)，即**三谱**（trispectrum），它为功率谱协方差矩阵贡献了额外的项。此外，长波模式对短波模式的调制，即**超样本协[方差](@entry_id:200758)**（super-sample covariance, SSC），也会引入非对角的协[方差](@entry_id:200758)。这些非高斯项会增加测量的不确定性，并使不同 $\ell$ 模式之间产生关联。
- **低 $\ell$ 统计**：[功率谱估计](@entry_id:753656)量 $\hat{C}_\ell$ 的[分布](@entry_id:182848)实际上是[Wishart分布](@entry_id:172059)。只有在模式数 $2\ell+1$ 很大时，根据中心极限定理，它才趋近于高斯分布。在低 $\ell$ 区间，估计量的[分布](@entry_id:182848)是高度非[高斯和](@entry_id:196588)偏斜的，此时采用高斯[似然](@entry_id:167119)会产生不准确的参数约束。

综上所述，高斯、块对角的似然近似在[非线性](@entry_id:637147)尺度、小天区覆盖或低 $\ell$ 分析中会失效 。精确的宇宙学分析必须通过[数值模拟](@entry_id:137087)或解析模型来仔细地构建更复杂的协方差矩阵，有时甚至需要超越高斯似然的框架。