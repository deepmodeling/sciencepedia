## 引言
在物理学与工程学的广阔天地中，[偏微分方程](@entry_id:141332)（PDE）是描述从热量传导到[流体运动](@entry_id:182721)等各种现象的核心语言。然而，经典数学理论通常要求这些方程的解是光滑且连续可微的，这在面对现实世界中的许多复杂情况时显得力不从心。例如，流体中的激波、材料中的裂纹、或作用于结构上的集中力，都表现为解的间断或奇异性，在这些点上经典导数失去了意义。这种理论与现实之间的鸿沟，催生了对更广义、更强大的数学工具的需求。

本文旨在系统地介绍“[弱解](@entry_id:161732)”与“[分布导数](@entry_id:181138)”这一深刻而强大的理论框架，它正是为了解决上述难题而生。通过重新定义“解”与“导数”的概念，该理论不仅能够严谨地处理[非光滑函数](@entry_id:175189)，还为现代数值分析，特别是有限元法的蓬勃发展，提供了坚不可摧的数学基石。

在接下来的内容中，我们将开启一段从理论到应用的探索之旅。在**“原理与机制”**一章，我们将深入探讨[分布导数](@entry_id:181138)的核心定义，了解如何从光滑的[检验函数](@entry_id:166589)出发，为任何[局部可积函数](@entry_id:175678)乃至更奇异的“[分布](@entry_id:182848)”赋予导数的意义，并构建起[偏微分方程](@entry_id:141332)的弱形式。随后，在**“应用与跨学科联系”**一章，我们将见证这些抽象概念在物理建模、界面问题、[非线性](@entry_id:637147)分析和前沿计算方法中的具体应用，展示其作为连接数学与物理现实的桥梁所发挥的巨大作用。最后，通过**“动手实践”**部分，您将有机会通过具体的计算练习，亲手体验并巩固对[弱解](@entry_id:161732)和[分布导数](@entry_id:181138)理论的理解。

## 原理与机制

在[偏微分方程](@entry_id:141332)的经典理论中，解的[可微性](@entry_id:140863)是一个基本要求。然而，许[多源](@entry_id:170321)自物理和工程问题的模型所产生的解并不具备这种正则性。例如，在[流体动力学](@entry_id:136788)中，激波的形成是[双曲守恒律](@entry_id:147752)方程（如[无粘性伯格斯方程](@entry_id:168659)）的普遍特征。这些激波表现为解的间断，在间断处，经典的导数没有定义。因此，为了有意义地分析这类问题，我们必须拓宽“解”和“导数”的概念。本章旨在建立一个严谨的数学框架——弱解和[分布导数](@entry_id:181138)理论——它使我们能够处理这些[非光滑函数](@entry_id:175189)，并为[偏微分方程的数值分析](@entry_id:752774)提供坚实的基础。

### 从经典导数到[分布导数](@entry_id:181138)

解决经典[可微性](@entry_id:140863)限制的核心思想是通过一种“对偶”或“测试”的方法来重新定义导数。我们不再直接在函数本身上进行[微分](@entry_id:158718)操作，而是考察该函数与一类性质极好的“检验函数”相互作用时所产生的效果。

#### [检验函数](@entry_id:166589)与[分布](@entry_id:182848)空间

我们首先定义**[检验函数](@entry_id:166589)空间 (space of test functions)**，记为 $\mathcal{D}(\Omega)$ 或 $C_c^\infty(\Omega)$。对于 $\mathbb{R}^n$ 中的一个非空开集 $\Omega$，该空间由所有在 $\Omega$ 内具有[紧支集](@entry_id:276214)（compact support）的无限可微[复值函数](@entry_id:196054)组成。一个函数 $\varphi$ 的支集，记为 $\operatorname{supp} \varphi$，是其非零点[集的[闭](@entry_id:143367)包](@entry_id:148169)。$\varphi \in C_c^\infty(\Omega)$ 意味着 $\varphi$ 是光滑的，并且在一个远离 $\Omega$ 边界的[紧集](@entry_id:147575)之外恒为零。这些函数既光滑又局部化，是理想的“探针”。

至关重要的是理解在 $\mathcal{D}(\Omega)$ 中[序列的收敛](@entry_id:140648)性。一个序列 $\{\varphi_k\}$ 在 $\mathcal{D}(\Omega)$ 中收敛到 $0$（记为 $\varphi_k \to 0$），其条件比逐点收敛或[一致收敛](@entry_id:146084)更为严格。它要求同时满足两个条件：
1.  存在一个固定的紧集 $K \subset \Omega$，使得所有 $\varphi_k$ 的支集都被包含在 $K$ 内。
2.  对于任意多重指标 $\alpha$，导数序列 $\partial^\alpha \varphi_k$ 在 $K$ 上[一致收敛](@entry_id:146084)到 $0$。

这个定义确保了[微分算子](@entry_id:140145) $\partial^\alpha: \mathcal{D}(\Omega) \to \mathcal{D}(\Omega)$ 是连续的，这是后续理论的关键。从拓扑学上讲，$\mathcal{D}(\Omega)$ 的拓扑结构是作为一系列Fréchet空间 $C_K^\infty(\Omega)$ 的严格归纳极限来定义的，它是使得所有嵌入映射 $i_K : C_K^\infty(\Omega) \hookrightarrow \mathcal{D}(\Omega)$ 连续的最精细的局部凸拓扑 。

有了[检验函数](@entry_id:166589)空间，我们便可以定义**[分布](@entry_id:182848) (distribution)**。一个[分布](@entry_id:182848) $T$ 是定义在 $\mathcal{D}(\Omega)$ 上的一个[连续线性泛函](@entry_id:262913)，即一个映射 $T: \mathcal{D}(\Omega) \to \mathbb{C}$。[分布](@entry_id:182848)的空间 $\mathcal{D}'(\Omega)$ 是 $\mathcal{D}(\Omega)$ 的**连续[对偶空间](@entry_id:146945)**。连续性要求至关重要，它将[分布](@entry_id:182848)与纯粹的代数对偶空间区分开来。一个线性泛函 $T$ 是连续的（即为一个[分布](@entry_id:182848)），当且仅当对于任意[紧集](@entry_id:147575) $K \subset \Omega$，存在常数 $C_K$ 和一个整数 $m \in \mathbb{N}$，使得对于所有支集在 $K$ 内的检验函数 $\varphi$，下式成立 ：
$$
|T(\varphi)| \le C_K \sum_{|\alpha| \le m} \sup_{x \in K} |\partial^\alpha \varphi(x)|
$$
这本质上意味着，一个[分布](@entry_id:182848)在每个[子空间](@entry_id:150286) $C_K^\infty(\Omega)$ 上的行为都是有界的。

任何[局部可积函数](@entry_id:175678) $f \in L^1_{\mathrm{loc}}(\Omega)$ 都可以通过积分定义一个**正则[分布](@entry_id:182848) (regular distribution)** $T_f$：
$$
\langle T_f, \varphi \rangle = \int_{\Omega} f(x) \varphi(x) \,dx
$$
其中 $\langle T, \varphi \rangle$ 表示[分布](@entry_id:182848) $T$ 作用于[检验函数](@entry_id:166589) $\varphi$。然而，并非所有[分布](@entry_id:182848)都是正则的。一个典型的例子是 **狄拉克 (Dirac) [分布](@entry_id:182848)** $\delta_{x_0}$，其作用是取检验函数在点 $x_0$ 处的值：
$$
\langle \delta_{x_0}, \varphi \rangle = \varphi(x_0)
$$
这个[分布](@entry_id:182848)描述了一个集中在单点 $x_0$ 的理想化[点源](@entry_id:196698)或[冲量](@entry_id:178343)，它无法由任何[局部可积函数](@entry_id:175678)通[过积分](@entry_id:753033)生成。

#### [分布导数](@entry_id:181138)的定义与实例

[分布理论](@entry_id:186499)的真正威力在于它为任何[分布](@entry_id:182848)（包括[非光滑函数](@entry_id:175189)）定义了导数。其定义源于对[光滑函数](@entry_id:267124)进行分部积分。若 $f \in C^1(\Omega)$，对于任意 $\varphi \in C_c^\infty(\Omega)$，[分部积分](@entry_id:136350)给出：
$$
\int_{\Omega} \frac{\partial f}{\partial x_i}(x) \varphi(x) \,dx = - \int_{\Omega} f(x) \frac{\partial \varphi}{\partial x_i}(x) \,dx
$$
在[分布](@entry_id:182848)的语言中，这可以写作 $\langle \partial_i T_f, \varphi \rangle = \langle T_f, -\partial_i \varphi \rangle$。我们把这个关系提升为定义。对于任意[分布](@entry_id:182848) $T \in \mathcal{D}'(\Omega)$ 和任意多重指标 $\alpha$，其**[分布导数](@entry_id:181138) (distributional derivative)** $\partial^\alpha T$ 定义为：
$$
\langle \partial^\alpha T, \varphi \rangle := (-1)^{|\alpha|} \langle T, \partial^\alpha \varphi \rangle
$$
由于 $\partial^\alpha: \mathcal{D}(\Omega) \to \mathcal{D}(\Omega)$ 是连续映射，而 $T$ 也是连续泛函，它们的复合 $\varphi \mapsto \langle T, \partial^\alpha \varphi \rangle$ 仍然是 $\mathcal{D}(\Omega)$ 上的一个[连续线性泛函](@entry_id:262913)。因此，$\partial^\alpha T$ 是一个良定义的[分布](@entry_id:182848)。这个定义成功地将[微分](@entry_id:158718)操作从可能“病态”的[分布](@entry_id:182848) $T$ 转移到了无限光滑的[检验函数](@entry_id:166589) $\varphi$ 上。

让我们来看几个关键例子：
1.  **亥维赛德 (Heaviside) 函数的导数**：考虑一维亥维赛德函数 $H(x)$，当 $x > 0$ 时为 $1$，当 $x \le 0$ 时为 $0$。它在 $x=0$ 处有一个[跳跃间断](@entry_id:139886)。它的[分布导数](@entry_id:181138) $D(H)$ 通过定义计算：
    $$
    \langle D(H), \varphi \rangle = - \langle H, \varphi' \rangle = - \int_{-\infty}^\infty H(x) \varphi'(x) \,dx = - \int_0^\infty \varphi'(x) \,dx = -[\varphi(x)]_0^\infty = - (0 - \varphi(0)) = \varphi(0)
    $$
    我们发现 $\langle D(H), \varphi \rangle = \langle \delta_0, \varphi \rangle$。因此，亥维赛德函数的[分布导数](@entry_id:181138)正是狄拉克[分布](@entry_id:182848) $D(H) = \delta_0$ 。这从数学上精确地捕捉了“一个[阶跃函数](@entry_id:159192)的导数是一个无穷大的尖峰”这一直观概念。

2.  **狄拉克[分布](@entry_id:182848)的导数**：我们可以对狄拉克[分布](@entry_id:182848)本身求导。利用定义 ：
    $$
    \langle \partial^\alpha \delta_{x_0}, \varphi \rangle = (-1)^{|\alpha|} \langle \delta_{x_0}, \partial^\alpha \varphi \rangle = (-1)^{|\alpha|} (\partial^\alpha \varphi)(x_0)
    $$
    这表明 $\delta_{x_0}$ 的 $\alpha$ 阶导数作用于一个[检验函数](@entry_id:166589)，会得到该检验函数在 $x_0$ 点的 $\alpha$ 阶导数值（再乘以一个符号因子）。例如，在 $\mathbb{R}^2$ 中，对于给定的点 $x_0=(1, -2)$ 和检验函数 $\varphi(x,y)$，计算 $(\partial_{x}^{2}\delta_{x_{0}} - 3\partial_{x}\partial_{y}\delta_{x_{0}} + 5\delta_{x_{0}})(\varphi)$ 就转化为计算 $\varphi$ 及其导数在 $(1, -2)$ 点的线性组合：
    $$
    \frac{\partial^2 \varphi}{\partial x^2}(1,-2) - 3 \frac{\partial^2 \varphi}{\partial x \partial y}(1,-2) + 5 \varphi(1,-2)
    $$

#### [分布](@entry_id:182848)运算的微妙之处

尽管[分布导数](@entry_id:181138)威力强大，但我们必须谨慎。并非所有在经典函数上成立的规则都能直接推广到[分布](@entry_id:182848)。一个核心问题是**[分布](@entry_id:182848)的乘积**。一般而言，两个任意[分布](@entry_id:182848)的乘积是未定义的。例如，考虑 $D(H^2)$。由于 $H(x)^2 = H(x)$（几乎处处成立），我们有 $D(H^2) = D(H) = \delta_0$。然而，如果天真地套用莱布尼兹法则，会得到 $D(H^2) = 2H \cdot D(H) = 2H \cdot \delta_0$。这导出了一个矛盾的等式 $\delta_0 = 2H \cdot \delta_0$。问题的根源在于，乘积 $H \cdot \delta_0$ 是一个[非光滑函数](@entry_id:175189)与一个[分布](@entry_id:182848)的乘积，这在标准[分布理论](@entry_id:186499)中是没有定义的。只有当乘子是一个[光滑函数](@entry_id:267124)（$C^\infty$ 函数）时，[分布](@entry_id:182848)的乘法才有明确的定义 。这一限制凸显了[分布](@entry_id:182848)框架的[代数结构](@entry_id:137052)的微妙性。

### [偏微分方程](@entry_id:141332)的弱解

[分布理论](@entry_id:186499)为重新阐述[偏微分方程](@entry_id:141332)的解提供了语言。这个新的表述，即**弱形式 (weak formulation)**，是数值方法（如有限元法）的理论基石。

基本思想是将方程乘以一个[检验函数](@entry_id:166589)，然后在整个定义域上积分，并通过[分部积分](@entry_id:136350)（或其高维推广——[格林公式](@entry_id:173118)）将导数从待求的解函数 $u$ 转移到检验函数 $v$ 上。

#### [泊松方程](@entry_id:143763)的弱形式

以狄利克雷边界条件的**[泊松方程](@entry_id:143763) (Poisson equation)** 为例：
$$
-\Delta u = f \quad \text{in } \Omega, \qquad u = 0 \quad \text{on } \partial\Omega
$$
经典解 $u$ 需要是二次连续可微的。为了推导弱形式，我们用一个在边界上为零的光滑检验函数 $v$ 乘以方程两边并积分：
$$
-\int_\Omega (\Delta u) v \,dx = \int_\Omega f v \,dx
$$
利用格林第一公式，$\int_\Omega (\Delta u) v \,dx = -\int_\Omega \nabla u \cdot \nabla v \,dx + \int_{\partial\Omega} (\nabla u \cdot n) v \,dS$。由于[检验函数](@entry_id:166589) $v$ 在边界 $\partial\Omega$ 上为零，边界积分项消失。于是我们得到：
$$
\int_\Omega \nabla u \cdot \nabla v \,dx = \int_\Omega f v \,dx
$$
这个[积分方程](@entry_id:138643)不再要求 $u$ 是二次可微的。它只需要 $u$ 和 $v$ 的[一阶导数](@entry_id:749425)是平方可积的，这样积分才有意义。这就引出了**索博列夫空间 (Sobolev spaces)**。$H^1(\Omega)$ 空间包含所有其本身及一阶[弱导数](@entry_id:189356)均在 $L^2(\Omega)$ 中的函数。$H^1_0(\Omega)$ 是 $H^1(\Omega)$ 中在边界上（以迹的意义下）为零的函数构成的[子空间](@entry_id:150286)。

于是，泊松方程的**[弱解](@entry_id:161732) (weak solution)** 定义为：寻找一个函数 $u \in H^1_0(\Omega)$，使得对于所有检验函数 $v \in H^1_0(\Omega)$，上述积分方程都成立 。对于给定的 $f \in L^2(\Omega)$，Lax-Milgram 定理保证了这样的[弱解](@entry_id:161732)存在且唯一。

#### 自然边界条件：[诺伊曼问题](@entry_id:176713)

对于**诺伊曼 (Neumann) 边界条件**，如 $A \nabla u \cdot n = g$ on $\partial\Omega$，[弱形式](@entry_id:142897)的推导过程揭示了其“自然”属性。对于方程 $-\nabla \cdot (A \nabla u) = f$，推导过程类似：
$$
\int_\Omega (A \nabla u) \cdot \nabla v \,dx - \int_{\partial\Omega} (A \nabla u \cdot n) v \,dS = \int_\Omega f v \,dx
$$
与[狄利克雷问题](@entry_id:274408)不同，我们不能假设检验函数 $v$ 在边界上为零。相反，我们将[诺伊曼边界条件](@entry_id:142124) $A \nabla u \cdot n = g$ 代入边界积分项，得到[弱形式](@entry_id:142897) ：
$$
\int_\Omega (A \nabla u) \cdot \nabla v \,dx = \int_\Omega f v \,dx + \int_{\partial\Omega} g v \,dS
$$
这里的[检验函数](@entry_id:166589)空间是整个 $H^1(\Omega)$。边界积分项 $\int_{\partial\Omega} gv \,dS$ 需要仔细解释。函数在边界上的取值通过**[迹算子](@entry_id:183665) (trace operator)** $\gamma: H^1(\Omega) \to H^{1/2}(\partial\Omega)$ 定义，它将一个 $H^1$ 函数映射到边界上的一个 $H^{1/2}$ 函数。为了使边界项成为 $H^1(\Omega)$ 上的[连续线性泛函](@entry_id:262913)，边界数据 $g$ 必须属于 $H^{1/2}(\partial\Omega)$ 的[对偶空间](@entry_id:146945)，即 $H^{-1/2}(\partial\Omega)$。因此，边界项被严谨地理解为对偶作用 $\langle g, \gamma v \rangle$ 。

#### 源项的[索博列夫空间](@entry_id:141995)解释

在泊松问题的[弱形式](@entry_id:142897)中，右端项是 $\int_\Omega f v \,dx$。这定义了一个关于 $v$ 的线性泛函 $L(v) = \langle f, v \rangle$。为了使[Lax-Milgram定理](@entry_id:137966)适用，这个泛函必须是 $H^1_0(\Omega)$ 上的有界（连续）泛函。这意味着 $f$ 必须属于 $H^1_0(\Omega)$ 的[对偶空间](@entry_id:146945)，我们将其记为 $H^{-1}(\Omega)$。

$H^{-1}(\Omega)$ 空间有着丰富的结构。任何 $L^2(\Omega)$ 中的函数 $g$ 都可以通过 $L^2$ [内积](@entry_id:158127)定义 $H^{-1}(\Omega)$ 中的一个元素，这构成了一个连续嵌入 $L^2(\Omega) \hookrightarrow H^{-1}(\Omega)$。更有趣的是，$L^2(\Omega)^d$ 中任何向量场 $G$ 的散度 $\operatorname{div} G$（在[分布](@entry_id:182848)意义下定义为 $\langle \operatorname{div} G, v \rangle := - \int_\Omega G \cdot \nabla v \,dx$）也定义了 $H^{-1}(\Omega)$ 中的一个元素。一个深刻的结果是，任何 $f \in H^{-1}(\Omega)$ 都可以表示为 $f = g - \operatorname{div} G$ 的形式，其中 $g \in L^2(\Omega)$ 且 $G \in L^2(\Omega)^d$ 。这为理解和逼近广义[源项](@entry_id:269111)提供了强大的工具。

### [弱解](@entry_id:161732)的性质与存在性

[弱解](@entry_id:161732)理论不仅扩展了解的概念，还引入了新的分析工具和微妙之处。

#### 弱收敛与[变分法](@entry_id:163656)

在索博列夫空间中，**[弱收敛](@entry_id:146650) (weak convergence)** 是一个核心概念。一个序列 $u_h$ 在[希尔伯特空间](@entry_id:261193)（如 $H^1_0(\Omega)$）中[弱收敛](@entry_id:146650)于 $u$（记为 $u_h \rightharpoonup u$），是指对于空间中任意元素 $v$，[内积](@entry_id:158127) $(u_h, v)$ 收敛于 $(u, v)$。强收敛（即[范数收敛](@entry_id:261322)）蕴含[弱收敛](@entry_id:146650)，但反之不然。

一个典型的例子是高频[振荡](@entry_id:267781)序列，如在 $\Omega=(0,1)$ 上的 $u_h(x) = \frac{1}{2\pi h} \sin(2\pi h x) x(1-x)$。可以证明，当 $h \to \infty$ 时，$u_h \to 0$ 于 $L^2(\Omega)$（强收敛），且 $u_h \rightharpoonup 0$ 于 $H^1_0(\Omega)$（弱收敛）。然而，其梯度的 $L^2$ 范数的平方的极限却非零：$\liminf_{h\to\infty} \|\nabla u_h\|_{L^2}^2 > 0 = \|\nabla 0\|_{L^2}^2$ 。

这个严格的不等式展示了范数的一个关键性质：**[弱下半连续性](@entry_id:198224) (weak lower semicontinuity)**。即若 $u_h \rightharpoonup u$，则 $\|u\| \le \liminf_{h\to\infty} \|u_h\|$。这意味着在[弱收敛](@entry_id:146650)极限下，范数（或能量）可能会“丢失”一部分，但绝不会增加。这个性质是**[变分法](@entry_id:163656)直接法 (direct method of the calculus of variations)** 的基石。该方法通过构造一个能量泛函的极小化序列，利用弱收敛找到一个弱极限点，然后借助[弱下半连续性](@entry_id:198224)证明该[极限点](@entry_id:177089)就是能量泛函的[极小元](@entry_id:266349)，从而证明了[弱解](@entry_id:161732)的存在性 。

#### 守恒律的非唯一性与熵解

对于[双曲守恒律](@entry_id:147752)，如 $u_t + f(u)_x = 0$，[弱形式](@entry_id:142897)虽然允许间断解，但也带来了新的问题：解的非唯一性。考虑一个具有凸通量 $f$ 和初始条件 $u_L  u_R$ 的[黎曼问题](@entry_id:171440)。此时，存在至少两个不同的[弱解](@entry_id:161732)：一个是通过特征线散开形成的连续**[稀疏波](@entry_id:168428) (rarefaction wave)**，另一个是满足**兰金-雨果尼奥 (Rankine-Hugoniot) [跳跃条件](@entry_id:750965)** $s = \frac{f(u_R)-f(u_L)}{u_R-u_L}$ 的非物理**激波 (shock wave)**  。

为了恢复唯一性并选出物理上相关的解，需要引入一个附加的**[熵条件](@entry_id:166346) (entropy condition)**。Kruzhkov [熵条件](@entry_id:166346)是一个普遍适用的判据。它要求对于任意常数 $k \in \mathbb{R}$ 和任意非负[检验函数](@entry_id:166589) $\varphi \in C_c^\infty(\mathbb{R}\times[0,\infty))$，一个**熵解 (entropy solution)** $u$ 必须满足以下[积分不等式](@entry_id:139182) ：
$$
\int_0^\infty \int_{\mathbb{R}} \Big( |u-k|\varphi_t + \operatorname{sgn}(u-k)(f(u)-f(k))\varphi_x \Big) \,dx\,dt + \int_{\mathbb{R}} |u_0(x)-k|\varphi(x,0) \,dx \ge 0
$$
这个条件本质上要求信息沿特征线向前传播，并排除了那些特征线会从间断处产生的非物理解。

### 从[弱解](@entry_id:161732)回到经典解

最后，一个自然的问题是：在何种条件下，一个弱解也同时是一个（更光滑的）经典解？

#### [椭圆正则性](@entry_id:177548)

对于[椭圆方程](@entry_id:169190)，答案由**[椭圆正则性](@entry_id:177548) (elliptic regularity)** 理论给出。该理论指出，如果方程的系数、定义域的边界和右端项（源项）足够光滑，那么[弱解](@entry_id:161732)也将是光滑的。对于[泊松方程](@entry_id:143763) $-\Delta u = f$，若 $f \in L^2(\Omega)$，为了保证弱解 $u \in H^1_0(\Omega)$ 同样属于 $H^2(\Omega)$（即其二阶[弱导数](@entry_id:189356)平方可积），从而使得方程 $-\Delta u = f$ 几乎处处成立，通常需要边界 $\partial\Omega$ 足够光滑。例如， $C^{1,1}$ 正则的边界就足够了。对于多边形定义域，情况则更为微妙：在二维情况下，当且仅当多边形是**凸**的，才能保证对于任意 $f \in L^2(\Omega)$ 都有 $u \in H^2(\Omega)$。非凸角点（所谓的“凹角”）会导致解的奇性，使得 $u$ 不在 $H^2(\Omega)$ 中，即使 $f$ 非常光滑 。

#### 格林函数与[分布](@entry_id:182848)

[椭圆正则性理论](@entry_id:203755)与**[格林函数](@entry_id:147802) (Green's function)** 的概念密切相关。对于泊松算子，[格林函数](@entry_id:147802) $G(x,y)$ 可以被理解为方程在右端项为狄拉克[分布](@entry_id:182848) $\delta_y$ 时的解，即它在[分布](@entry_id:182848)意义下满足：
$$
-\Delta_x G(\cdot,y) = \delta_y \quad \text{in } \mathcal{D}'(\Omega)
$$
这意味着对于所有 $\varphi \in C_c^\infty(\Omega)$，$\int_\Omega G(x,y)(-\Delta \varphi(x))\,dx = \varphi(y)$ 。
格林函数为求解泊松方程提供了积分表示 $u(x) = \int_\Omega G(x,y)f(y)\,dy$。对于[自伴算子](@entry_id:152188)（如[狄利克雷拉普拉斯算子](@entry_id:266386)），[格林函数](@entry_id:147802)具有对称性 $G(x,y) = G(y,x)$。然而，值得注意的是，即使在光滑域上，由于其在 $x=y$ 处的奇性，格林函数 $G(\cdot, y)$ 本身通常不属于 $H^1(\Omega)$ 。这再次说明了[分布](@entry_id:182848)框架在精确描述点源及其响应中的核心作用。

总之，从[分布导数](@entry_id:181138)的抽象定义到守恒律的熵解，再到[椭圆方程](@entry_id:169190)的[正则性理论](@entry_id:194071)，弱解的框架不仅为处理非光滑现象提供了严谨的工具，也深化了我们对[偏微分方程解](@entry_id:166250)的结构和性质的理解，为现代[数值分析](@entry_id:142637)的发展奠定了不可或缺的理论基础。