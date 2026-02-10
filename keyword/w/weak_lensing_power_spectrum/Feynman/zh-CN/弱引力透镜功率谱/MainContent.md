## 引言
宇宙中绝大部分物质是不可见的，仅通过其[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)效应揭示自身的存在。[弱引力透镜](@keyword=weak_lensing|lang=zh-CN|style=Feynman)是我们描绘这一隐藏的宇宙网最强大的技术，它观测遥远星系的光线在穿过团块状[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)的暗物质时如何被微弱地扭曲。但是，一个充满微弱剪切星系的天空并非一张直接的地图；我们如何将这些充满噪声的复杂数据转化为关于宇宙基本属性和起源的精确陈述？答案在于一个强大的统计工具：弱[引力透镜功率谱](@keyword=lensing_power_spectrum|lang=zh-CN|style=Feynman)。本文是对[现代宇宙学](@keyword=modern_cosmology|lang=zh-CN|style=Feynman)这一基石的全面指南。第一章，**原理与机制**，将阐释从广义相对论中物质与时空的基本联系，到我们天空中观测到的二维[汇聚图](@keyword=convergence_map|lang=zh-CN|style=Feynman)的统计描述的整个理论过程。随后，**应用与交叉学科联系**一章将探讨[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)在实践中的应用，从限制[标准宇宙学模型](@keyword=standard_cosmological_model|lang=zh-CN|style=Feynman)，到处理复杂的系统效应，再到寻找超出我们当前理解的新物理。

## 原理与机制

想象一下，你正身处平静海洋中央的一艘船上。突然，你注意到远处一座灯塔的倒影有些许扭曲、闪烁和摇晃。你看不见水下有什么，但你知道那里一定有东西——也许是水流，也许是鱼群，或者是水中密度的微小变化。通过仔细研究光线是如何被弯曲的，原则上你可以绘制出这些看不见的扰动的地图。

这正是我们在[弱引力透镜](@keyword=weak_lensing|lang=zh-CN|style=Feynman)中所玩的游戏。遥远的灯塔是古老的星系，而看不见的海洋则是广袤无垠的空间，充满了成团、不[均匀分布](@keyword=equidistribution|lang=zh-CN|style=Feynman)的物质。来自这些星系的光线穿行数十亿年，其路径被其经过的每一个星系、每一个星系团和每一根暗物质纤维的[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)所轻微扰动。我们不像在强引力透镜中那样看到巨大的弧或多个像；相反，我们看到的是背景星系形状中微弱而相干的畸变。我们的任务是解读这种畸变，并重建导致它的不可见物质的[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)图。但是，我们如何将一个充满微弱扭曲星系形状的天空，转化为关于我们宇宙基本属性的精确陈述呢？答案在于统计学的强大语言，具体来说，就是**功率谱**。

### 从物质团块到时空弯曲

首先要掌握的原理是物质与时空几何之间的联系，这是 Einstein 广义相对论的核心。对于宇宙的宏大尺度而言，[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)通常较弱，我们可以用每个点上的一个单一数值来描述时空的轻微弯曲：即**[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman)**，用希腊字母 $\Phi$ 表示。可以把它想象成一张时空的[等高线图](@keyword=contour_maps|lang=zh-CN|style=Feynman)；就像球会在丘陵地带滚下坡一样，光线也会被引力势中的“山丘”和“山谷”所偏折。

这些山丘和山谷从何而来？它们来自物质。一个区域内物质越多，意味着引力势阱越深。其精确的联系是我们在入门物理学中学到的熟悉的 Poisson 方程的一个优美的宇宙学版本。它将[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman) $\Phi$ 与**物质密度对比** $\delta$ 联系起来。[密度对比](@keyword=density_contrast|lang=zh-CN|style=Feynman)只是衡量宇宙团块程度的一个指标：$\delta = (\rho - \bar{\rho}) / \bar{\rho}$，其中 $\rho$ 是局部密度，$\bar{\rho}$ 是宇宙的平均密度。在傅立叶分析的语言中——它将一个场分解为不同大小的波——这种关系异常简洁：

$$
k^2 \Phi(\boldsymbol{k}) \propto a^{-1} \delta(\boldsymbol{k})
$$

此处，$\boldsymbol{k}$ 是波矢，代表特定尺度或波长的涨落，而 $a$ 是宇宙的[尺度因子](@keyword=scale_factors|lang=zh-CN|style=Feynman)，用于解释[宇宙膨胀](@keyword=universe_expansion|lang=zh-CN|style=Feynman)。这个方程告诉我们，某个尺度上的[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)会产生同一尺度上的[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman)漲落。

现在，我们可以进入下一步。物质[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)是一个[随机场](@keyword=random_fields|lang=zh-CN|style=Feynman)，是一幅由超密区和欠密区构成的复杂织锦。我们无法也不想描述每一个粒子的位置。取而代之的是，我们描述其统计特性。最强大的工具是**[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman)**，$P_\delta(k)$。它告诉我们在每个空间尺度 $k$ 上[密度涨落](@keyword=density_fluctuations|lang=zh-CN|style=Feynman)的“功率”，即[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)的大小。在某个 $k$ 值上较大的 $P_\delta(k)$ 意味着宇宙在对应于 $k$ 的尺度上非常成团。

利用 Poisson 方程，我们可以直接得到引力势的[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman) $P_\Phi(k)$。如果我们知道物质涨落的“配方”，我们就能找到它们所产生的时空弯曲的“配方”。这种关系既简单又深刻 [@problem_id:3497175]：

$$
P_{\Phi}(k) \propto \frac{1}{k^4} P_{\delta}(k)
$$

看这个 $k^{-4}$ 因子！由于大的 $k$ 对应小的空间尺度，这个因子极大地抑制了小尺度上的[引力势](@keyword=gravitational_potential|lang=zh-CN|style=Feynman)功率。即使物质[分布](@keyword=generalized_function|lang=zh-CN|style=Feynman)在小尺度上非常成团，它所产生的引力势也极其平滑。这是[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的一个普遍特征：其效应是长程的，并倾向于使事物平滑化。

### 宏伟的投影

我们拥有了宇宙[三维引力](@keyword=3d_gravity|lang=zh-CN|style=Feynman)景观的统计描述。但我们生活在地球上向外看，看到的是一个二维[天球](@keyword=celestial_sphere|lang=zh-CN|style=Feynman)。我们测量的畸变是一束光线在到达我们之前的旅程中穿过的所有[势阱](@keyword=potential_energy_well|lang=zh-CN|style=Feynman)和势丘的累积效应。[弱引力透镜](@keyword=weak_lensing|lang=zh-CN|style=Feynman)中的关键可观测量是**汇聚度** $\kappa$，它实际上是沿视线方向物质密度的加权总和。

我们如何从底层的三维[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman)得到这个二维投影图的功率谱？这涉及到数学意义上的“投影”。汇聚度的[角功率谱](@keyword=angular_power_spectrum|lang=zh-CN|style=Feynman) $C_\ell^{\kappa\kappa}$ 通过沿视线方向的积分与三维[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman) $P_\delta(k)$ 相关联。这里，$\ell$ 是角多极矩，是三维[波数](@keyword=wavenumber|lang=zh-CN|style=Feynman) $k$ 的二维模拟；大的 $\ell$ 意味着天空中小的角尺度。

完整的表达式有点吓人，但一个被称为**Limber 近似**的绝妙简化给了我们巨大的直观洞察。它在小角尺度（大 $\ell$）上有效，并且本质上说明，在尺度 $\ell$ 上的[角功率谱](@keyword=angular_power_spectrum|lang=zh-CN|style=Feynman)的主要贡献来自于[波数](@keyword=wavenumber|lang=zh-CN|style=Feynman)为 $k \approx \ell/\chi$ 的三维涨落，其中 $\chi$ 是到涨落处的[共动距离](@keyword=comoving_distance|lang=zh-CN|style=Feynman)。公式如下：

$$
C_\ell^{\kappa\kappa} \approx \int_0^{\chi_s} d\chi \, \frac{W(\chi)^2}{\chi^2} P_{\delta}\left(k = \frac{\ell}{\chi}, \chi\right)
$$

这个方程是[弱引力透镜](@keyword=weak_lensing|lang=zh-CN|style=Feynman)的罗塞塔石碑。它告诉我们，我们观测到的二维[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)（$C_\ell^{\kappa\kappa}$）是三维[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman)（$P_\delta$）沿视线方向（$\int d\chi$）的总和。项 $W(\chi)$ 是“透镜效率”核。它是一个几何因子，对于非常靠近我们或非常靠近源星系的结构来说很小，而在大约中间位置最大，这完全合乎情理——当透镜位于观测者和源之间时，其效率最高 [@problem_id:960703] [@problem_id:826770]。通过测量不同源星系距离（不同的 $\chi_s$）下的 $C_\ell^{\kappa\kappa}$，我们可以进行一种宇宙学层析成像，逐层剥离积分，以重建[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman)随宇宙时间的演化。

事实上，汇聚度功率谱只是看待统计数据的一种方式。我们可以转而测量星系对的形状与其分离角 $\theta$ 之间的相关性。这就是**[两点相关函数](@keyword=two_point_correlation_function|lang=zh-CN|style=Feynman)** $\xi(\theta)$，它是功率谱的傅立叶变换对 [@problem_id:960646]。它们包含完全相同的信息，只是呈現在不同的空間中——一個是用角度的語言（實空間），另一個是用角頻率的語言（傅立葉空間）。[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)，或者说透镜信号的整体“强度”，就是[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)在所有尺度上的积分 [@problem_id:960498]。

### 解读宇宙乐谱

所以我们测量 $C_\ell^{\kappa\kappa}$。它看起来是什么样子，又告诉了我们什么？它不仅仅是一条没有特征的曲线。其特定形状深刻反映了我们宇宙的历史和组成。

[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman) $P_\delta(k)$ 并非一个简单的[幂律](@keyword=power_law|lang=zh-CN|style=Feynman)。它是由[引力坍缩](@keyword=gravitational_collapse|lang=zh-CN|style=Feynman)与宇宙膨胀之间长达138亿年的竞争所塑造的。它通常被写作：

$$
P_{\delta}(k) \propto k^{n_s} T^2(k)
$$

这里，$k^{n_s}$ 代表了[原初涨落](@keyword=primordial_fluctuations|lang=zh-CN|style=Feynman)谱，很可能是在宇宙暴胀时期形成的。[谱指数](@keyword=spectral_index|lang=zh-CN|style=Feynman) $n_s$ 是我们想要测量的一个基本参数；$n_s=1$ 的值对应于“尺度不变”的[原初涨落](@keyword=primordial_fluctuations|lang=zh-CN|style=Feynman)。神奇之处在于**[转移函数](@keyword=transfer_function|lang=zh-CN|style=Feynman)** $T(k)$。它描述了这些原初涟漪如何成长为我们今天看到的结构。

对于非常大的尺度（小 $k$），这些尺度在[早期宇宙](@keyword=early_universe|lang=zh-CN|style=Feynman)总是比可观测宇宙的[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)要大，扰动得以无阻碍地增长。因此，$T(k) \approx 1$。然而，对于较小的尺度（大 $k$），情况就不同了。这些尺度在宇宙由辐射主导时进入了[视界](@keyword=apparent_horizon|lang=zh-CN|style=Feynman)。在这种炽热致密的等离子体中，光子的压力阻止了正常物质的坍缩。不与光发生相互作用的暗物质仍然可以开始成团，但其增长受到了严重抑制。这种停滞发展的结果是，这些尺度上的[转移函数](@keyword=transfer_function|lang=zh-CN|style=Feynman)表现为 $T(k) \propto \ln(k)/k^2$ [@problem_id:892783]。

这给[物质功率谱](@keyword=matter_power_spectrum|lang=zh-CN|style=Feynman)烙上了一个特征形状：它在大尺度上几乎是平坦的，然后在小尺度上“翻转”并下降。当这个三维[谱投影](@keyword=spectral_projection|lang=zh-CN|style=Feynman)到二维透镜[功率谱](@keyword=power_spectrum|lang=zh-CN|style=Feynman)时，这个形状也被继承下来。通过测量小尺度（高 $\ell$）上 $C_\ell^{\kappa\kappa}$ 的斜率，我们可以[直接探测](@keyword=direct_detection|lang=zh-CN|style=Feynman)原初指数 $n_s$。通过定位翻转的位置，我们可以测量物质-辐射相等时的尺度，这告诉我们宇宙中物质和辐射的[相对丰度](@keyword=relative_abundance|lang=zh-CN|style=Feynman)。这是一个惊人的联系：遥远星系形状的微小扭曲，告诉了我们宇宙仅有几千年历史时的物理学。

### 一个更复杂而美丽的现实

当然，真实世界从来不像我们的玩具模型那样简单。[现代宇宙学](@keyword=modern_cosmology|lang=zh-CN|style=Feynman)的美妙之处在于理解其中的复杂性，因为它们常常隐藏着新的物理学，或让我们对已知事物有更深入的把握。

首先，我们钟爱的 Limber 近似毕竟只是一个近似。它在小角尺度上表现出色，但对于天空的大片区域（低 $\ell$），它就开始失效。精确计算表明，涨落沿视线方向的关联方式是 Limber 近似所忽略的。通过仔细计算修正项，我们可以确保我们的分析在所有尺度上都是准确的，将一个潜在的系统误差转化为验证我们模型的工具 [@problem_id:897189]。

其次，当我们从有限的巡天项目中测量功率谱时，我们的测量本身就具有不确定性。其中一部分是简单的统计噪声。但还有更微妙、更有趣的误差来源，它们产生的原因是宇宙并非一个完美的[高斯随机场](@keyword=gaussian_random_fields|lang=zh-CN|style=Feynman)。它在[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)作用下的演化是[非线性](@keyword=non_linearity|lang=zh-CN|style=Feynman)的，产生了致密的星系团和空旷的宇宙空洞。这种非高斯性意味着我们在不同尺度上对功率的测量不是独立的。理解我们测量的**[协方差矩阵](@keyword=covariance_matrix|lang=zh-CN|style=Feynman)**至关重要。有两个有趣的效应促成了这一点：

-   **超样本协[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)（SSC）：** 我们的巡天，无论多大，都只是宇宙的一小块。这一小块可能恰好位于一个在更大尺度上略微超密或欠密的区域。超密的背景就像一个[物质密度](@keyword=matter_density|lang=zh-CN|style=Feynman)稍高的迷你宇宙，导致我们巡天范围内的[结构增长](@keyword=structure_growth|lang=zh-CN|style=Feynman)得快一些。这会提升我们在所有尺度上测量的功率谱。这种“超样本”模式将我们巡天内的所有尺度耦合在一起，引入了强大的协[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman) [@problem_id:894834]。将其考虑在内对于获得正确的[宇宙学参数](@keyword=cosmological_parameters|lang=zh-CN|style=Feynman)[误差棒](@keyword=error_bars|lang=zh-CN|style=Feynman)至关重要。

-   **晕模型：** 在小尺度上，宇宙中几乎所有的物质都被锁定在分立的暗物质**晕**中。这个简单的物理图像为理解[非线性引力](@keyword=non_linear_gravity|lang=zh-CN|style=Feynman)坍缩提供了一个强有力的方法。它还告诉我们关于宇宙场的高阶统计信息。例如，小尺度上非高斯协[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)的主要来源来自于恰好位于同一个大质量[暗物质晕](@keyword=dark_matter_halos|lang=zh-CN|style=Feynman)内的四个点之间的相关性（即“单晕”项）。这为计算和理解我们数据的复杂协[方差](@keyword=second_central_moment|lang=zh-CN|style=Feynman)结构提供了一个物理框架 [@problem_id:897139]。

从物质与[引力](@keyword=gravitational_force|lang=zh-CN|style=Feynman)的简单联系，到宇宙的统计描述，再到该结构在我们天空上的投影，弱[引力透镜功率谱](@keyword=lensing_power_spectrum|lang=zh-CN|style=Feynman)是一首物理学的交响曲。通过学习解读它的乐谱——包括其真实世界测量中的复杂和声——我们得以了解宇宙自身的故事。

