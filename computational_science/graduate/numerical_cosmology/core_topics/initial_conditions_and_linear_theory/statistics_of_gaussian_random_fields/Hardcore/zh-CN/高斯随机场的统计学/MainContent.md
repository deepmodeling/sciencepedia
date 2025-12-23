## 引言
[高斯随机场](@entry_id:749757)（Gaussian Random Fields, GRFs）是现代物理学和应用数学中的一个基石概念，尤其在宇宙学中扮演着无可替代的角色。从早期宇宙的量子涨落到我们今天观测到的宇宙微波背景辐射和宏大的星系网，[高斯随机场](@entry_id:749757)为描述这些复杂现象的统计起源提供了简洁而强大的理论框架。然而，从抽象的数学定义到具体的数值模拟和数据分析，存在一个知识鸿沟：我们如何精确地利用这一工具来构建虚拟宇宙、预测可观测量，并理解其在其他科学领域中的普适性？

本文旨在系统性地跨越这一鸿沟。我们将从[高斯随机场](@entry_id:749757)的统计学基础出发，为您构建一个坚实的理论与实践知识体系。在**“原理与机制”**一章中，我们将深入探讨[高斯随机场](@entry_id:749757)的数学定义、平稳性和各向同性等核心性质，并建立起连接实空间相关函数与傅里叶空间功率谱的关键桥梁。随后的**“应用与交叉学科联系”**一章将展示这些原理的强大应用，不仅阐明其如何作为[标准宇宙学模型](@entry_id:159833)的基石，用于生成和演化宇宙，还将探索其在波动物理、数据科学和不确定性量化等领域的惊人普适性。最后，在**“动手实践”**一章中，您将通过一系列精心设计的编程练习，将理论知识转化为实际的计算技能。

通过本次学习，您将不仅掌握[高斯随机场](@entry_id:749757)的[统计力](@entry_id:194984)学，更能深刻体会到它作为一种通用语言，在理解和模拟众多复杂系统中的核心价值。让我们一同开启这段探索之旅，揭示隐藏在随机性背后的深刻秩序。

## 原理与机制

在上一章中，我们介绍了[高斯随机场](@entry_id:749757)在宇宙学中作为[初始条件](@entry_id:152863)和可观测场（如宇宙微波背景）统计模型的核心作用。本章将深入探讨这些场的数学原理和统计机制。我们将从基本定义出发，建立描述这些场的统计语言，并推导它们在平坦空间和球面上的关键性质。这些原理构成了[数值宇宙学](@entry_id:752779)中生成和分析[高斯随机场](@entry_id:749757)的基础。

### [高斯随机场](@entry_id:749757)的定义

一个**[随机场](@entry_id:177952)**（random field）$f(\boldsymbol{x})$ 是定义在某个空间（例如三维[欧氏空间](@entry_id:138052) $\mathbb{R}^3$）上的[随机变量](@entry_id:195330)的集合，其中每个点 $\boldsymbol{x}$ 都对应一个[随机变量](@entry_id:195330) $f(\boldsymbol{x})$。一个场的完整统计特性由其所有[有限维分布](@entry_id:197042)（finite-dimensional distributions）决定，即对于任意一组有限的点 $\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$，随机向量 $(f(\boldsymbol{x}_1), \dots, f(\boldsymbol{x}_n))$ 的[联合概率分布](@entry_id:171550)。

在众多随机场中，**[高斯随机场](@entry_id:749757)**（Gaussian random field）因其简洁性和物理上的合理性而尤为重要。一个随机场被称为[高斯随机场](@entry_id:749757)，如果其所有[有限维分布](@entry_id:197042)都是多元正态（或高斯）[分布](@entry_id:182848) 。这一定义有一个等价的表述：一个随机场是高斯的，当且仅当其值的任意有限线性组合 $\sum_{i=1}^n a_i f(\boldsymbol{x}_i)$ 是一个一元高斯[随机变量](@entry_id:195330) 。

[多元正态分布](@entry_id:175229)完全由其[均值向量](@entry_id:266544)和[协方差矩阵](@entry_id:139155)确定。因此，一个[高斯随机场](@entry_id:749757)的全部统计信息被完全编码在其**[均值函数](@entry_id:264860)**（mean function）$\mu(\boldsymbol{x}) = \langle f(\boldsymbol{x}) \rangle$ 和**[协方差函数](@entry_id:265031)**（covariance function）$\xi(\boldsymbol{x}, \boldsymbol{y}) = \langle (f(\boldsymbol{x}) - \mu(\boldsymbol{x}))(f(\boldsymbol{y}) - \mu(\boldsymbol{y})) \rangle$ 中。在宇宙学中，我们通常处理零均值场，例如物质密度扰动 $\delta(\boldsymbol{x})$，因此 $\mu(\boldsymbol{x}) = 0$。在这种情况下，[协方差函数](@entry_id:265031)，也称为**[两点相关函数](@entry_id:185074)**（two-point correlation function），$\xi(\boldsymbol{x}, \boldsymbol{y}) = \langle f(\boldsymbol{x}) f(\boldsymbol{y}) \rangle$，就包含了该场的所有统计信息。

一个自然的问题是：什么样的函数可以作为[高斯随机场](@entry_id:749757)的[协方差函数](@entry_id:265031)？答案是，一个函数 $\xi(\boldsymbol{x}, \boldsymbol{y})$ 是一个有效的[协方差函数](@entry_id:265031)，必须满足两个条件：对称性（$\xi(\boldsymbol{x}, \boldsymbol{y}) = \xi(\boldsymbol{y}, \boldsymbol{x})$）和**[正定性](@entry_id:149643)**（positive definiteness）。[正定性](@entry_id:149643)要求对于任意一组点 $\boldsymbol{x}_1, \dots, \boldsymbol{x}_n$ 和任意实系数 $a_1, \dots, a_n$，[协方差矩阵](@entry_id:139155)都是半正定的，即 $\sum_{i,j=1}^n a_i a_j \xi(\boldsymbol{x}_i, \boldsymbol{x}_j) \ge 0$。这一条件源于任何线性组合的[方差](@entry_id:200758)都必须是非负的 。

**[科尔莫戈罗夫扩展定理](@entry_id:267158)**（Kolmogorov extension theorem）为[高斯随机场](@entry_id:749757)的存在性提供了严格的数学基础。该定理指出，只要给定一个对称且正定的[协方差函数](@entry_id:265031) $C(\boldsymbol{x}, \boldsymbol{y})$ 和一个[均值函数](@entry_id:264860) $m(\boldsymbol{x})$，就必然存在一个[高斯随机场](@entry_id:749757)，其[有限维分布](@entry_id:197042)恰好是由这对函数所确定的[多元正态分布](@entry_id:175229) 。这一定理的强大之处在于，它保证了只要我们能构造一个数学上合法的[协方差函数](@entry_id:265031)，一个与之对应的、统计上完整的随机场就一定存在。

### [平稳性](@entry_id:143776)、各向同性及其在傅里叶空间的体现

[宇宙学原理](@entry_id:158425)假设宇宙在大尺度上是统计均匀和各向同性的。这些对称性极大地简化了随机场的统计描述。

**[统计均匀性](@entry_id:136481)**（statistical homogeneity），或称**平稳性**（stationarity），指的是统计性质在空间平移下保持不变。对于[两点相关函数](@entry_id:185074)，这意味着 $\xi(\boldsymbol{x}, \boldsymbol{y})$ 只依赖于两点间的**分离向量**（separation vector）$\boldsymbol{r} = \boldsymbol{x} - \boldsymbol{y}$，而与绝对位置无关。我们可以通过平移 $\boldsymbol{t} = -\boldsymbol{y}$ 来证明这一点：$\xi(\boldsymbol{x}, \boldsymbol{y}) = \xi(\boldsymbol{x}+\boldsymbol{t}, \boldsymbol{y}+\boldsymbol{t}) = \xi(\boldsymbol{x}-\boldsymbol{y}, \boldsymbol{0})$。因此，对于一个平稳场，我们可以将相关函数写作 $\xi(\boldsymbol{r})$ 。需要注意的是，相关性依赖于坐标的差 $\boldsymbol{x} - \boldsymbol{y}$，而非和 $\boldsymbol{x} + \boldsymbol{y}$ 。

**统计各向同性**（statistical isotropy）指的是统计性质在空间旋转下保持不变。当这个性质应用于平稳场的[两点相关函数](@entry_id:185074) $\xi(\boldsymbol{r})$ 时，它要求 $\xi(\boldsymbol{r})$ 在其[自变量](@entry_id:267118) $\boldsymbol{r}$ 绕原点旋转时保持不变。任何对向量方向不敏感的函数必然只依赖于该向量的模。因此，对于一个平稳且各向同性的[随机场](@entry_id:177952)，其[两点相关函数](@entry_id:185074)只依赖于两点间的距离 $r = |\boldsymbol{r}| = |\boldsymbol{x}-\boldsymbol{y}|$，即 $\xi(\boldsymbol{x}, \boldsymbol{y}) = \xi(r)$ 。值得强调的是，统计各向同性是指场的[统计系综](@entry_id:149738)具有[旋转不变性](@entry_id:137644)，而非每个单独的场实现自身是球对称的。一个具体的宇宙实现（比如我们观测到的宇宙）会充满各种结构，但这些结构的统计规律在所有方向上都是相同的 。

对于平稳[随机场](@entry_id:177952)，[傅里叶分析](@entry_id:137640)是一个极其强大的工具。场的[傅里叶变换](@entry_id:142120) $\tilde{f}(\boldsymbol{k})$ 和原场 $f(\boldsymbol{x})$ 构成一个[傅里叶变换](@entry_id:142120)对。在宇宙学中，一个常见的约定是：
$$
f(\boldsymbol{x}) = \int \frac{d^3 k}{(2\pi)^3} e^{i \boldsymbol{k} \cdot \boldsymbol{x}} \tilde{f}(\boldsymbol{k}) \quad , \quad \tilde{f}(\boldsymbol{k}) = \int d^3 x \, e^{-i \boldsymbol{k} \cdot \boldsymbol{x}} f(\boldsymbol{x})
$$
平稳性在傅里叶空间中有一个简洁的表述：不同波矢 $\boldsymbol{k}$ 的傅里叶模式是互不相关的。具体而言，傅里叶系数的协[方差](@entry_id:200758)满足：
$$
\langle \tilde{f}(\boldsymbol{k}) \tilde{f}^*(\boldsymbol{k}') \rangle = (2\pi)^3 \delta_D^{(3)}(\boldsymbol{k} - \boldsymbol{k}') P(\boldsymbol{k})
$$
其中 $\delta_D^{(3)}$ 是[三维狄拉克δ函数](@entry_id:274703)，而 $P(\boldsymbol{k})$ 被定义为**[功率谱](@entry_id:159996)**（power spectrum）。功率谱描述了场在不同尺度（由波矢 $k = |\boldsymbol{k}|$ 的大小决定）上的波动的“强度”。

**[维纳-辛钦定理](@entry_id:188017)**（Wiener-Khinchin theorem）指出，对于一个平稳随机场，其[两点相关函数](@entry_id:185074) $\xi(\boldsymbol{r})$ 和[功率谱](@entry_id:159996) $P(\boldsymbol{k})$ 恰好是一个[傅里叶变换](@entry_id:142120)对 。使用上述傅里叶约定，其关系为：
$$
\xi(\boldsymbol{r}) = \int \frac{d^3 k}{(2\pi)^3} P(\boldsymbol{k}) e^{i \boldsymbol{k} \cdot \boldsymbol{r}}
$$
如果场同时是各向同性的，那么[功率谱](@entry_id:159996) $P(\boldsymbol{k})$ 也必然是各向同性的，即只依赖于 $k=|\boldsymbol{k}|$，写作 $P(k)$。在这种情况下，上述积分可以在[球坐标](@entry_id:146054)中进行，得到一个只与 $r$ 有关的结果：
$$
\xi(r) = \int_0^\infty \frac{k^2 dk}{2\pi^2} P(k) j_0(kr)
$$
其中 $j_0(x) = \sin(x)/x$ 是零阶[球贝塞尔函数](@entry_id:153247) 。

这个傅里叶关系为[协方差函数](@entry_id:265031)的[正定性](@entry_id:149643)提供了一个极其有力的判据。**[博赫纳定理](@entry_id:183496)**（Bochner's theorem）指出，一个[连续函数](@entry_id:137361)是正定的，当且仅当它是某个非负测度的[傅里叶变换](@entry_id:142120)。在我们的语境下，这意味着相关函数 $\xi(r)$ 是一个有效的[协方差函数](@entry_id:265031)，当且仅当其对应的功率谱 $P(k)$ 处处非负，即 $P(k) \ge 0$ 。这提供了一个清晰的物理图像：场的总功率是各个独立傅里叶模式功率的叠加，而每个模式的功率（[方差](@entry_id:200758)）不能是负的。需要注意的是，虽然 $P(k)$ 必须非负，但[相关函数](@entry_id:146839) $\xi(r)$ 本身在某些 $r$ 值上可以是负的，例如在某些宇宙学模型中，物质相关函数在大尺度上会因重子声波[振荡](@entry_id:267781)而呈现负值 。

### [高斯随机场](@entry_id:749757)的核心性质

[高斯随机场](@entry_id:749757)最核心、最强大的性质在于，其所有统计信息都完全由其均值和[两点相关函数](@entry_id:185074)（或等价地，[功率谱](@entry_id:159996)）所决定。所有更高阶的[相关函数](@entry_id:146839)（N点函数）都可以通过两点函数表示出来。

这一性质的数学表述是**[威克定理](@entry_id:137086)**（Wick's theorem）。对于一个零均值[高斯随机场](@entry_id:749757)，其任意偶数个点的 N 点相关函数等于将这 N 个点两两配对，然后将每对点的[两点相关函数](@entry_id:185074)相乘，最后将所有可能的配对方式加起来。所有奇数个点的 N 点相关函数都为零。

以四点相关函数为例，$\langle f_1 f_2 f_3 f_4 \rangle$（其中 $f_i = f(\boldsymbol{x}_i)$），有三种配对方式：$(1,2)(3,4)$、$(1,3)(2,4)$ 和 $(1,4)(2,3)$。根据[威克定理](@entry_id:137086)，我们有：
$$
\langle f_1 f_2 f_3 f_4 \rangle = \langle f_1 f_2 \rangle \langle f_3 f_4 \rangle + \langle f_1 f_3 \rangle \langle f_2 f_4 \rangle + \langle f_1 f_4 \rangle \langle f_2 f_3 \rangle
$$
若用 $\xi_{ij} = \langle f_i f_j \rangle$ 表示，则上式为 $\xi_{12}\xi_{34} + \xi_{13}\xi_{24} + \xi_{14}\xi_{23}$ 。[威克定理](@entry_id:137086)的本质是高斯分布的[矩母函数](@entry_id:154347)是一个指数为二次型的函数，这意味着所有高于二阶的**[累积量](@entry_id:152982)**（cumulants）或**连通[相关函数](@entry_id:146839)**（connected correlation functions）都为零。

另一个重要性质是场的**光滑性**或**可微性**。一个场的导数的统计性质与原场的[相关函数](@entry_id:146839)或[功率谱](@entry_id:159996)密切相关。例如，场的梯度 $\nabla f(\boldsymbol{x})$ 的协[方差](@entry_id:200758)张量可以通过对[两点相关函数](@entry_id:185074) $\xi(r)$ 求导得到 。对于一个平稳各向同性场，其梯度的协[方差](@entry_id:200758)为：
$$
\langle \partial_i f(\boldsymbol{x}) \partial_j f(\boldsymbol{y}) \rangle = - \frac{\partial^2}{\partial r_i \partial r_j} \xi(r) = \left(\frac{\xi'(r)}{r} - \xi''(r)\right)\frac{r_i r_j}{r^2} - \frac{\xi'(r)}{r}\delta_{ij}
$$
其中 $\boldsymbol{r} = \boldsymbol{x} - \boldsymbol{y}$，$r_i$ 是其分量，$\xi'$ 和 $\xi''$ 是 $\xi(r)$ 对 $r$ 的一阶和[二阶导数](@entry_id:144508)。

场的**均方可微性**（mean-square differentiability）则由[功率谱](@entry_id:159996)在高波数（大 $k$）下的行为决定。一个场是 $n$ 次均方可微的，意味着其 $n$ 阶导数的[方差](@entry_id:200758)是有限的。$n$ 阶导数的[方差](@entry_id:200758)涉及对 $k^{2n} P(k)$ 的积分。具体来说，我们定义**谱矩**（spectral moments）为：
$$
\sigma_n^2 \equiv \int \frac{d^3 k}{(2\pi)^3} k^{2n} P(k)
$$
场的[方差](@entry_id:200758)是 $\sigma_0^2$，其一阶导数[方差](@entry_id:200758)与 $\sigma_1^2$ 成正比，[二阶导数](@entry_id:144508)[方差](@entry_id:200758)与 $\sigma_2^2$ 成正比。如果功率谱在高[波数](@entry_id:172452)下呈现[幂律衰减](@entry_id:262227) $P(k) \sim k^{-\alpha}$，那么在三维空间中，谱矩 $\sigma_n^2$ 收敛的条件是积分核 $k^{2n+2} P(k) \sim k^{2n+2-\alpha}$ 的指数小于 $-1$，即 $\alpha > 2n+3$ 。因此：
- 场的[方差](@entry_id:200758)有限（$\sigma_0^2  \infty$），需要 $\alpha > 3$。
- 场是一次均方可微的（$\sigma_1^2  \infty$），需要 $\alpha > 5$。
- 场是二次均方可微的（$\sigma_2^2  \infty$），需要 $\alpha > 7$。
这表明，功率谱在高 $k$ 处衰减得越快，场在实空间中就越光滑。

### 宇宙学中的应用：从天空到立方体

[高斯随机场](@entry_id:749757)的理论在宇宙学的两个主要领域——观测宇宙微波背景（CMB）和数值模拟宇宙结构形成——中得到了广泛应用。

#### 球面上的随机场

CMB 温度和偏振的各向异性可以被建模为定义在[天球](@entry_id:158268) $S^2$ 上的[高斯随机场](@entry_id:749757)。在这种几何结构下，**[球谐函数](@entry_id:178380)**（spherical harmonics）$Y_{\ell m}(\hat{\boldsymbol{n}})$ 扮演了[傅里叶基](@entry_id:201167)函数的角色。场 $T(\hat{\boldsymbol{n}})$ 可以展开为：
$$
T(\hat{\boldsymbol{n}}) = \sum_{\ell=0}^{\infty} \sum_{m=-\ell}^{\ell} a_{\ell m} Y_{\ell m}(\hat{\boldsymbol{n}})
$$
其中 $a_{\ell m}$ 是球谐系数。

对于一个统计各向同性的零均值高斯场，其球谐系数具有非常简洁的统计性质 ：
1.  **不相关性**：不同模式的系数是不相关的，其协[方差](@entry_id:200758)为对角阵：
    $$
    \langle a_{\ell m} a_{\ell' m'}^* \rangle = C_\ell \delta_{\ell\ell'} \delta_{mm'}
    $$
    这里的 $C_\ell$ 被称为**[角功率谱](@entry_id:161125)**（angular power spectrum），它描述了在角尺度 $\sim \pi/\ell$ 上的波动功率。
2.  **高斯性和独立性**：由于 $a_{\ell m}$ 是高斯场 $T(\hat{\boldsymbol{n}})$ 的线性泛函（通过积分得到），它们本身也服从高斯分布。因为它们不相关，所以它们也是[相互独立](@entry_id:273670)的。
3.  **实在性**：由于天空中的温度场 $T(\hat{\boldsymbol{n}})$ 是一个实数场，其球谐系数必须满足**实在性条件**（reality condition）：$a_{\ell, -m} = (-1)^m a_{\ell m}^*$。这意味着 $m$ 和 $-m$ 的系数是相关的（互为复共轭关系，并有一个相位因子）。因此，只有 $m \ge 0$ 的系数是独立的。具体来说：
    -   对于 $m=0$， $a_{\ell 0}$ 是实数，服从均值为零、[方差](@entry_id:200758)为 $C_\ell$ 的[正态分布](@entry_id:154414)，即 $a_{\ell 0} \sim \mathcal{N}(0, C_\ell)$。
    -   对于 $m0$， $a_{\ell m}$ 是复数，其实部和虚部是独立的、均值为零、[方差](@entry_id:200758)为 $C_\ell/2$ 的高斯[随机变量](@entry_id:195330) 。

在实际观测中，我们通过测量 $a_{\ell m}$ 来估计真实的[角功率谱](@entry_id:161125) $C_\ell$。一个无偏的估计量是：
$$
\hat{C}_\ell = \frac{1}{2\ell+1} \sum_{m=-\ell}^{\ell} |a_{\ell m}|^2
$$
由于我们只有一个宇宙可以观测，这个估计量本身就是一个[随机变量](@entry_id:195330)，其固有的不确定性被称为**宇宙[方差](@entry_id:200758)**（cosmic variance）。对于全天区的无噪声观测，这个[方差](@entry_id:200758)为 ：
$$
\mathrm{Var}(\hat{C}_\ell) = \frac{2 C_\ell^2}{2\ell+1}
$$
这个结果可以通过对 $\hat{C}_\ell$ 的[方差](@entry_id:200758)进行直接计算得出，其中利用了[高斯变量](@entry_id:276673)四阶矩的性质。它也可以从以下事实推导：经过归一化的估计量 $(2\ell+1)\hat{C}_\ell / C_\ell$ 服从自由度为 $2\ell+1$ 的卡方分布（$\chi^2_{2\ell+1}$）。宇宙[方差](@entry_id:200758)表明，即使观测完美，我们对 $C_\ell$ 的[测量精度](@entry_id:271560)也受到有限的统计样本（每个 $\ell$ 只有 $2\ell+1$ 个模式）的限制。

实际观测还会受到仪器效应的影响，主要是**波束平滑**（beam smoothing）和**仪器噪声**（instrumental noise）。如果仪器的角响应函数（波束）由[传递函数](@entry_id:273897) $B_\ell$ 描述，而噪声的[角功率谱](@entry_id:161125)为 $N_\ell$，那么观测到的球谐系数为 $a_{\ell m}^{\mathrm{obs}} = B_\ell a_{\ell m} + n_{\ell m}$。观测到的功率谱[期望值](@entry_id:153208)为 $\langle \tilde{C}_\ell^{\mathrm{obs}} \rangle = B_\ell^2 C_\ell + N_\ell$。因此，为了恢复真实的宇宙信号功率谱 $C_\ell$，我们需要构建一个[无偏估计量](@entry_id:756290)，它首先减去已知的噪声功率贡献，然后除以波束[传递函数](@entry_id:273897)的平方来进行反卷积 ：
$$
\hat{C}_\ell = \frac{1}{B_\ell^2} \left( \frac{\sum_{m=-\ell}^\ell |a_{\ell m}^{\mathrm{obs}}|^2}{2\ell+1} - N_\ell \right)
$$

#### 有限体积中的[随机场](@entry_id:177952)

在进行宇宙学 N 体模拟等数值计算时，我们通常在一个具有周期性边界条件的有限立方体（边长为 $L$）内生成[高斯随机场](@entry_id:749757)作为[初始条件](@entry_id:152863)。周期性边界条件 $\delta(\boldsymbol{x} + L\boldsymbol{e}_i) = \delta(\boldsymbol{x})$ 使得场只能由特定波长的平面波叠加而成。这导致傅里叶空间中的波矢 $\boldsymbol{k}$ 被离散化，形成一个[晶格](@entry_id:196752)，其分量为：
$$
k_i = \frac{2\pi}{L} n_i, \quad n_i \in \mathbb{Z}
$$
每个允许的 $\boldsymbol{k}$ 模式占据了傅里叶空间中体积为 $(2\pi/L)^3 = (2\pi)^3/V$ 的一个基本单元，其中 $V=L^3$ 是模拟盒的体积 。

在生成随机场时，我们需要知道在某个尺度范围内有多少独立的傅里叶模式。在 $L$ 足够大的连续近似下，一个半径为 $k$、厚度为 $\Delta k$ 的薄球壳内的模式总数，可以通过该球壳的体积 $4\pi k^2 \Delta k$ 乘以模式的数密度 $V/(2\pi)^3$ 来估计，得到 $\frac{V k^2 \Delta k}{2\pi^2}$。

然而，与球面情况类似，由于场 $\delta(\boldsymbol{x})$ 是实数，其傅里叶系数必须满足实在性条件 $\delta(-\boldsymbol{k}) = \delta(\boldsymbol{k})^*$。这意味着 $\boldsymbol{k}$ 和 $-\boldsymbol{k}$ 模式不是独立的。因此，为了计算独立的自由度数量，我们必须将总模式数除以 2（忽略少数如 $\boldsymbol{k}=0$ 的自[共轭点](@entry_id:160335)）。所以，在 $k$ 到 $k+\Delta k$ 范围内的独立傅里叶模式数量为 ：
$$
N_{\mathrm{ind}}(k, \Delta k) \approx \frac{V k^2 \Delta k}{4\pi^2}
$$
在实际生成[高斯随机场](@entry_id:749757)时，我们为这些独立的模式（例如，半个傅里叶空间中的所有模式）赋予随机的、服从[高斯分布](@entry_id:154414)的振幅和相位，然后利用实在性条件确定另一[半空间](@entry_id:634770)中的模式，最后通过傅里叶逆变换得到[实空间](@entry_id:754128)中的随机场。