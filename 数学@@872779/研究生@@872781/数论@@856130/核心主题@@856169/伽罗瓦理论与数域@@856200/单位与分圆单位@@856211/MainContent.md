## 引言
在[代数数论](@entry_id:148067)的宏伟版图上，对[代数整数](@entry_id:151672)环算术性质的研究占据着核心地位。正如研究有理整数环 $\mathbb{Z}$ 离不开其可逆元 $\{\pm 1\}$，对一般[代数数域](@entry_id:637592) $K$ 的[整数环](@entry_id:181003) $\mathcal{O}_K$ 的理解也深刻地依赖于其[单位群](@entry_id:184012) $\mathcal{O}_K^\times$ 的结构。然而，与 $\mathbb{Z}$ 的情况截然不同，$\mathcal{O}_K^\times$ 的结构往往极其丰富和复杂，其[有限生成](@entry_id:156447)性与秩的大小直接关系到[数域](@entry_id:155558)的诸多根本性质，例如[唯一因子分解的失效](@entry_id:155196)程度。本文旨在系统地揭示这一复杂结构，并聚焦于一类特殊而重要的单位——[分圆单位](@entry_id:184331)，阐明它们在理论与应用中的关键作用。

本文致力于解决从抽象结构到具体应用之间的鸿沟。我们不仅要回答“[单位群](@entry_id:184012)的结构是怎样的？”这个问题，更要探索“我们如何利用这些单位来解决数论中的深刻问题？”。为此，文章将分为三个章节，引领读者循序渐进地掌握这一领域的核心知识。
    
在“**原理与机制**”一章中，我们将从[代数数论](@entry_id:148067)的基石——[狄利克雷单位定理](@entry_id:155550)出发，阐明单位群的抽象结构。随后，我们将进入分圆域这一特殊的研究对象，定义并构造[分圆单位](@entry_id:184331)，并证明它们在整个[单位群](@entry_id:184012)中的重要性。
    
接下来，“**应用与跨学科联系**”一章将展示这些理论的强大威力。我们将探讨[单位群](@entry_id:184012)如何通过[解析类数公式](@entry_id:184272)与L函数建立联系，[分圆单位](@entry_id:184331)如何通过Sinnott定理和Stickelberger定理与类[群结构](@entry_id:146855)紧密交织，以及这些经典思想如何成为通往p进分析与现代[岩泽理论](@entry_id:197056)的桥梁。
    
最后，“**动手实践**”部分将提供一系列精心设计的计算问题，帮助读者将抽象的理论应用于具体的[数域](@entry_id:155558)，亲手计算[基本单位](@entry_id:148878)和验证理论预测，从而巩固和深化所学知识。

## 原理与机制

本章旨在深入探讨[代数数域](@entry_id:637592)中[单位群](@entry_id:184012)的结构，并聚焦于一类极其重要的单位——[分圆单位](@entry_id:184331)。我们将从[狄利克雷单位定理](@entry_id:155550)这一基石出发，揭示单位群的抽象代数结构，然后通过[对数嵌入](@entry_id:148678)的几何视角，赋予这一定理更直观的内涵。在此基础上，我们将进入分圆域的世界，定义并研究[分圆单位](@entry_id:184331)，最终阐明它们在连接类数与L函数特殊值等深刻问题中的核心作用。

### [单位群](@entry_id:184012)的结构：[狄利克雷单位定理](@entry_id:155550)

在任意一个[代数数域](@entry_id:637592) $K$ 中，其[整数环](@entry_id:181003) $\mathcal{O}_K$ 是一个戴德金整环。正如我们在研究有理[整数环](@entry_id:181003) $\mathbb{Z}$ 时关心其可逆元（即单位）$\{\pm 1\}$ 一样，研究 $\mathcal{O}_K$ 中的可逆元也至关重要。

**[单位群](@entry_id:184012) (Group of Units)** $\mathcal{O}_K^\times$ 被定义为环 $\mathcal{O}_K$ 中所有乘法可[逆元](@entry_id:140790)的集合。具体来说，一个元素 $\alpha \in \mathcal{O}_K$ 是一个单位，当且仅当存在另一个元素 $\beta \in \mathcal{O}_K$ 使得 $\alpha\beta = 1$。可以证明，这等价于[代数整数](@entry_id:151672) $\alpha$ 的域范数 $N_{K/\mathbb{Q}}(\alpha)$ 为 $\pm 1$。$\mathcal{O}_K^\times$ 在环乘法下构成一个[阿贝尔群](@entry_id:150284)。

数域的[单位群](@entry_id:184012)结构远比 $\mathbb{Z}^\times = \{\pm 1\}$ 复杂。例如，在[实二次域](@entry_id:636720) $\mathbb{Q}(\sqrt{2})$ 中，整数环为 $\mathbb{Z}[\sqrt{2}]$，其单位群为 $\{\pm(1+\sqrt{2})^n \mid n \in \mathbb{Z}\}$，这是一个[无限群](@entry_id:147005)。深刻地描述任意数域 $K$ 的[单位群](@entry_id:184012)结构的，正是**[狄利克雷单位定理](@entry_id:155550) (Dirichlet's Unit Theorem)**。

该定理指出，$\mathcal{O}_K^\times$ 是一个[有限生成阿贝尔群](@entry_id:156372)。根据[有限生成阿贝尔群](@entry_id:156372)的基本定理，它可以分解为其[扭子群](@entry_id:139454)和一个自由[阿贝尔群](@entry_id:150284)的直积。

1.  **[扭子群](@entry_id:139454) (Torsion Subgroup)**：$\mathcal{O}_K^\times$ 的[扭子群](@entry_id:139454)由其中所有有限阶元素构成。一个单位 $\zeta \in \mathcal{O}_K^\times$ 具有有限阶，当且仅当它是单位根。因此，[扭子群](@entry_id:139454)就是 $K$ 中包含的所有单位根构成的群，记作 $\mu(K)$。对于任意[数域](@entry_id:155558) $K$，$\mu(K)$ 都是一个[有限循环群](@entry_id:147298)。

2.  **自由部分 (Free Part)**：$\mathcal{O}_K^\times$ 的自由部分的秩，记为 $r$，由[数域](@entry_id:155558) $K$ 的“嵌入”方式完全确定。令 $r_1$ 表示 $K$ 的实嵌入（$K \hookrightarrow \mathbb{R}$）的个数，$r_2$ 表示 $K$ 的共轭[复嵌入](@entry_id:189961)对（$K \hookrightarrow \mathbb{C}$ 且像不落在 $\mathbb{R}$ 中）的个数。[数域](@entry_id:155558)的次数 $n=[K:\mathbb{Q}]$ 满足 $n=r_1+2r_2$。[狄利克雷单位定理](@entry_id:155550)断言，[单位群的秩](@entry_id:150706)为 $r = r_1+r_2-1$。

综合这两点，我们可以精确地写出[单位群](@entry_id:184012)的结构 [@problem_id:3030596]：
$$ \mathcal{O}_K^\times \cong \mu(K) \times \mathbb{Z}^{r_1+r_2-1} $$
这个优美的公式是[代数数论](@entry_id:148067)的基石之一。它告诉我们，要完全理解 $\mathcal{O}_K^\times$，我们需要确定其[扭子群](@entry_id:139454) $\mu(K)$（这通常不难）以及一个秩为 $r_1+r_2-1$ 的自由部分的生成元。这些生成元被称为一组**基本单位 (fundamental units)**。例如，对于 $K=\mathbb{Q}$，$r_1=1, r_2=0$，秩为 $1+0-1=0$，所以 $\mathbb{Z}^\times \cong \mu(\mathbb{Q}) \times \mathbb{Z}^0 \cong \{\pm 1\}$。对于[虚二次域](@entry_id:197298)，如 $\mathbb{Q}(i)$，$r_1=0, r_2=1$，秩为 $0+1-1=0$，其单位群也是有限的，$\mathbb{Z}[i]^\times = \{\pm 1, \pm i\}$。而对于[实二次域](@entry_id:636720)，如 $\mathbb{Q}(\sqrt{2})$，$r_1=2, r_2=0$，秩为 $2+0-1=1$，这与我们前面观察到的 $\mathbb{Z}[\sqrt{2}]^\times \cong \{\pm 1\} \times \mathbb{Z}$ 相符。

### 几何解释：[对数嵌入](@entry_id:148678)与调整子

[狄利克雷单位定理](@entry_id:155550)的证明及其内涵，可以通过一个巧妙的几何构造——**[对数嵌入](@entry_id:148678) (logarithmic embedding)**——来深刻理解。这个工具将[单位群](@entry_id:184012)的乘法结构转化为[欧氏空间](@entry_id:138052)中的加法结构，从而允许我们使用格 (lattice) 的几何理论。

令 $K$ 的 $r_1$ 个实嵌入为 $\sigma_1, \dots, \sigma_{r_1}$，并从 $r_2$ 对共轭[复嵌入](@entry_id:189961)中每对各选一个代表，记为 $\tau_1, \dots, \tau_{r_2}$。我们可以定义一个**[对数映射](@entry_id:637227)** $L$:
$$ L: \mathcal{O}_K^\times \longrightarrow \mathbb{R}^{r_1+r_2} $$
$$ L(u) = \bigl(\log|\sigma_1(u)|, \dots, \log|\sigma_{r_1}(u)|, 2\log|\tau_1(u)|, \dots, 2\log|\tau_{r_2}(u)|\bigr) $$
这个映射是一个[群同态](@entry_id:140603)，它将左边的乘法群映到右边的加性[向量空间](@entry_id:151108)。系数 $2$ 的出现是为了后续公式的简洁性，因为它对应于共轭对的贡献 ($|\tau(u)|^2 = \tau(u)\overline{\tau(u)}$)。

[对数映射](@entry_id:637227) $L$ 的性质完美地解释了[狄利克雷单位定理](@entry_id:155550)的各个部分 [@problem_id:3030626] [@problem_id:3030597]：

1.  **$L$ 的核 (Kernel)**：一个单位 $u$ 属于 $L$ 的核，当且仅当 $L(u)=0$。这意味着 $|\sigma_i(u)|=1$ 对所有 $i$ 成立，且 $|\tau_j(u)|=1$ 对所有 $j$ 成立。也就是说，$u$ 的所有伽罗瓦共轭（即它在所有嵌入下的像）的[绝对值](@entry_id:147688)都为 $1$。根据克罗内克 (Kronecker) 的一个定理，满足此条件的[代数整数](@entry_id:151672)必须是单位根。反之，任何单位根 $\zeta \in \mu(K)$ 在任何嵌入下的[绝对值](@entry_id:147688)都为 $1$，因此 $L(\zeta)=0$。所以，我们有：
    $$ \ker(L) = \mu(K) $$
    这从几何上解释了单位群的[扭子群](@entry_id:139454)。

2.  **$L$ 的像 (Image)**：对于任何单位 $u \in \mathcal{O}_K^\times$，我们知道其范数 $N_{K/\mathbb{Q}}(u) = \pm 1$，因此 $|N_{K/\mathbb{Q}}(u)|=1$。范数可以表示为所有共轭的乘积：
    $$ |N_{K/\mathbb{Q}}(u)| = \left(\prod_{i=1}^{r_1} |\sigma_i(u)|\right) \left(\prod_{j=1}^{r_2} |\tau_j(u)|^2\right) = 1 $$
    对上式取对数，我们得到：
    $$ \sum_{i=1}^{r_1} \log|\sigma_i(u)| + \sum_{j=1}^{r_2} 2\log|\tau_j(u)| = 0 $$
    这恰好意味着 $L(u)$ 的所有分量之和为零。因此，$L$ 的像落在 $\mathbb{R}^{r_1+r_2}$ 的一个[余维](@entry_id:273141)为 $1$ 的[超平面](@entry_id:268044) $H$ 中，其定义为 $H = \{ (x_1, \dots, x_{r_1+r_2}) \in \mathbb{R}^{r_1+r_2} \mid \sum_{k=1}^{r_1+r_2} x_k = 0 \}$。这个[超平面](@entry_id:268044)的维数是 $r_1+r_2-1$。

[狄利克雷单位定理](@entry_id:155550)的核心内容是，$L$ 的像 $L(\mathcal{O}_K^\times)$ 是超平面 $H$ 中的一个**满秩格 (full-rank lattice)**。这意味着 $L(\mathcal{O}_K^\times)$ 是 $H$ 的一个离散[子群](@entry_id:146164)，并且它在实数意义下张成了整个 $H$。一个 $d$ 维空间中的满秩[格同构](@entry_id:137015)于 $\mathbb{Z}^d$。由于 $H$ 的维数是 $r_1+r_2-1$，这就证明了 $\mathcal{O}_K^\times / \mu(K)$ 同构于 $\mathbb{Z}^{r_1+r_2-1}$。

这个几何图像引出了一个重要的[不变量](@entry_id:148850)。格 $L(\mathcal{O}_K^\times)$ 在超平面 $H$ 中有一个[基本域](@entry_id:201756)（fundamental domain），这个[基本域](@entry_id:201756)的体积被称为[数域](@entry_id:155558) $K$ 的**调整子 (Regulator)**，记作 $R_K$ [@problem_id:3030610]。$R_K$ 是一个正实数，度量了[单位群](@entry_id:184012)“大小”或“密度”的对数尺度。

调整子 $R_K$ 的一个关键性质是它的**不变性**。$R_K$ 是[数域](@entry_id:155558) $K$ 的内蕴[不变量](@entry_id:148850)，不依赖于我们如何选取基本单位。这是因为任意两组基本单位 $\{\varepsilon_1, \dots, \varepsilon_r\}$ 和 $\{\varepsilon'_1, \dots, \varepsilon'_r\}$ 作为 $\mathcal{O}_K^\times/\mu(K)$ 的 $\mathbb{Z}$-基，它们之间通过一个整系数的[可逆线性变换](@entry_id:149915)联系。这个变换的矩阵 $U$ 属于 $\mathrm{GL}_r(\mathbb{Z})$，其[行列式](@entry_id:142978)为 $\det(U) = \pm 1$。在对数空间中，这个基变换对应于对格的[基向量](@entry_id:199546)做了一个线性变换，[变换矩阵](@entry_id:151616)就是 $U$。一个线性变换对体积的影响是通过其[行列式](@entry_id:142978)的[绝对值](@entry_id:147688)来度量的。由于 $| \det(U) | = 1$，格的[基本域](@entry_id:201756)[体积保持](@entry_id:141001)不变。因此，$R_K$ 的定义是良定的 [@problem_id:3030610]。

### 一类特殊的单位：[分圆单位](@entry_id:184331)

现在我们将目光从一般数域转向一类特别重要且结构丰富的数域——**[分圆域](@entry_id:153828) (cyclotomic fields)**。令 $n \ge 3$ 为整数，$\zeta_n = \exp(2\pi i / n)$ 为一个本原 $n$ 次单位根。第 $n$ 个[分圆域](@entry_id:153828)定义为 $K=\mathbb{Q}(\zeta_n)$。

[分圆域](@entry_id:153828)的基本性质对于理解其单位至关重要 [@problem_id:3030583] [@problem_id:3030623]：
- **次数与伽罗瓦群**：$K/\mathbb{Q}$ 的扩张次数为 $[\mathbb{Q}(\zeta_n):\mathbb{Q}] = \varphi(n)$，其中 $\varphi$ 是[欧拉函数](@entry_id:634684)。这是一个伽罗瓦扩张，其伽罗瓦群 $\mathrm{Gal}(K/\mathbb{Q})$ 同构于模 $n$ 的整数[乘法群](@entry_id:155975) $(\mathbb{Z}/n\mathbb{Z})^\times$。这个同构由映射 $a \mapsto \sigma_a$ 给出，其中自同构 $\sigma_a$ 由其在生成元上的作用 $\sigma_a(\zeta_n) = \zeta_n^a$ 唯一确定。由于 $(\mathbb{Z}/n\mathbb{Z})^\times$ 是[阿贝尔群](@entry_id:150284)，[分圆域](@entry_id:153828)是[阿贝尔扩张](@entry_id:152984)。
- **[整数环](@entry_id:181003)**：$\mathbb{Q}(\zeta_n)$ 的整数环是 $\mathcal{O}_K = \mathbb{Z}[\zeta_n]$。

在[分圆域](@entry_id:153828)中，我们可以明确地构造出一大批单位，它们被称为**[分圆单位](@entry_id:184331) (cyclotomic units)**。最基本的一类[分圆单位](@entry_id:184331)形如 [@problem_id:3030599]：
$$ u_a = \frac{1-\zeta_n^a}{1-\zeta_n} \quad \text{其中} \gcd(a, n)=1 $$
要证明 $u_a$ 确实是 $\mathcal{O}_K$ 中的单位，我们需要做两步验证：
1.  **$u_a$ 是[代数整数](@entry_id:151672)**：我们可以将 $u_a$ 写成一个几何级数求和的形式：
    $$ u_a = 1 + \zeta_n + \zeta_n^2 + \dots + \zeta_n^{a-1} $$
    由于 $\zeta_n$ 是[代数整数](@entry_id:151672)（它是 $x^n-1=0$ 的根），而[代数整数](@entry_id:151672)环是封闭的，所以这个和也是一个[代数整数](@entry_id:151672)。即 $u_a \in \mathcal{O}_K$。

2.  **$u_a$ 是可逆的**：我们计算其范数 $N_{K/\mathbb{Q}}(u_a)$。利用范数的乘法性质和伽罗瓦群的作用，我们有：
    $$ N_{K/\mathbb{Q}}(u_a) = \frac{N_{K/\mathbb{Q}}(1-\zeta_n^a)}{N_{K/\mathbb{Q}}(1-\zeta_n)} $$
    分子 $N_{K/\mathbb{Q}}(1-\zeta_n^a)$ 是 $1-\zeta_n^a$ 的所有伽罗瓦共轭的乘积。$1-\zeta_n^a$ 的共轭是 $\sigma_c(1-\zeta_n^a) = 1-\zeta_n^{ac}$，其中 $c$ 跑遍 $(\mathbb{Z}/n\mathbb{Z})^\times$。由于 $\gcd(a,n)=1$，当 $c$ 跑遍 $(\mathbb{Z}/n\mathbb{Z})^\times$ 时，$ac$ 也跑遍这个群。这意味着 $\{1-\zeta_n^{ac}\}$ 这个集合与 $\{1-\zeta_n^c\}$ 只是次序不同。因此，分子等于分母，故 $N_{K/\mathbb{Q}}(u_a) = 1$。
    一个范数为 $1$ (或 $-1$) 的[代数整数](@entry_id:151672)一定是单位。因此 $u_a$ 是一个单位 [@problem_id:3030583]。

值得注意的是，定义中的分母 $1-\zeta_n$ 自身并不总是单位。它的范数是 $N_{K/\mathbb{Q}}(1-\zeta_n) = \Phi_n(1)$，其中 $\Phi_n(x)$ 是第 $n$ 个[分圆多项式](@entry_id:155668)。可以证明：
$$ \Phi_n(1) = \begin{cases} p  \text{ if } n=p^k \text{ (素数幂)} \\ 1  \text{if } n \text{ 有至少两个不同的素因子} \end{cases} $$
因此，$1-\zeta_n$ 是单位当且仅当 $n$ 不是素数的幂 [@problem_id:3030583] [@problem_id:3030623]。

### [分圆单位](@entry_id:184331)的重要性：[类数公式](@entry_id:202401)与[岩泽理论](@entry_id:197056)的先声

由形如 $u_a$ 的元素以及 $-1$ 和 $\zeta_n$ 生成的单位群[子群](@entry_id:146164)，被称为**[分圆单位](@entry_id:184331)群**，记作 $C(K)$。一个驚人的事实是，这个我们可以明确构造出的[子群](@entry_id:146164)，在整个单位群 $\mathcal{O}_K^\times$ 中只占一个“很小”的部分，但却抓住了其本质。

更准确地说， $C(K)$ 在 $\mathcal{O}_K^\times$ 中是一个**有限指数**的[子群](@entry_id:146164)。这意味着从秩的角度看，它们是一样大的。两个群的秩都是 $r_1+r_2-1 = 0 + \varphi(n)/2 - 1 = \varphi(n)/2 - 1$。这意味着[分圆单位](@entry_id:184331)足以生成一个与整个[单位群](@entry_id:184012)的自由部分“共度”的格。

这一现象的深刻意义在 $K$ 的**最大实子域 (maximal real subfield)** $K^+ = \mathbb{Q}(\zeta_n+\zeta_n^{-1})$ 中表现得最为清晰。$K^+$ 的[单位群](@entry_id:184012)记作 $E^+ = \mathcal{O}_{K^+}^\times$。可以证明 $\mathcal{O}_K^\times$ 中大部分单位“来自”$E^+$，更精确地，$E^+$ 在 $\mathcal{O}_K^\times$ 中的指数 $Q = [\mathcal{O}_K^\times : \mu(K)E^+]$ 是 $1$ 或 $2$。

令 $C^+ = C(K) \cap E^+$ 为 $K^+$ 中的实[分圆单位](@entry_id:184331)群。关于 $C^+$ 在 $E^+$ 中的指数，有一个著名的定理，它将代数对象（单位群和[类数](@entry_id:156164)）与分析对象（L函数）联系起来，是**[解析类数公式](@entry_id:184272)**的一个体现 [@problem_id:3030598]：

**[分圆单位](@entry_id:184331)指数定理**：令 $h^+$ 为最大实子域 $K^+$ 的[类数](@entry_id:156164)。则指数 $[E^+ : C^+]$ 与 $h^+$ 密切相关。在特定条件下，它们完全相等。
- 如果 $n$ 是一个素数的幂（$n=p^k$）或一个奇[素数幂](@entry_id:636094)的两倍（$n=2p^k$），则有优美的等式：
  $$ [E^+ : C^+] = h^+ $$
- 对于一般的 $n$，公式稍微变为 $[E^+ : C^+] = 2^a h^+$，其中 $a$ 是一个非负整数，仅当 $n$ 满足上述条件时 $a=0$。

这个公式意义非凡。它表明，我们可以通过计算代数上明确定义的[分圆单位](@entry_id:184331)[群的指数](@entry_id:145655)来得到关于类数 $h^+$ 的信息。类数是衡量唯一[因子分解](@entry_id:150389)失败程度的指标，通常极难计算。而[分圆单位](@entry_id:184331)是具体可构造的。这个联系是代数数论中最深刻和最有用的结果之一，并且它为后来的[岩泽理论](@entry_id:197056) (Iwasawa theory) 铺平了道路，后者研究类数和单位群在p-进[域塔](@entry_id:153606)中的变化规律。

### 高等视角：伽罗瓦模结构与[S-单位](@entry_id:194670)

我们可以从表示论的视角来审视单位群，这能揭示其更深层次的[代数结构](@entry_id:137052)。单位群 $\mathcal{O}_K^\times$ 自然地成为一个 $\mathbb{Z}[G]$-模，其中 $G = \mathrm{Gal}(K/\mathbb{Q})$。为了得到一个[向量空间](@entry_id:151108)，我们作张量积 $V = \mathcal{O}_K^\times \otimes_\mathbb{Z} \mathbb{Q}$，这是一个 $\mathbb{Q}[G]$-模。这个空间只保留了[单位群](@entry_id:184012)的自由部分的信息，其维度为[单位群的秩](@entry_id:150706) $r=\varphi(n)/2 - 1$。

对于[分圆域](@entry_id:153828) $K = \mathbb{Q}(\zeta_n)$，其伽罗瓦群 $G$ 是[阿贝尔群](@entry_id:150284)，因此其在 $\mathbb{C}$ 上的不可约表示都是一维的，由模 $n$ 的[狄利克雷特征](@entry_id:151586) $\chi: G \to \mathbb{C}^\times$ 给出。我们可以将模 $V$ [复化](@entry_id:260775)为 $V_\mathbb{C} = V \otimes_\mathbb{Q} \mathbb{C}$，并根据这些特征将其分解为特征[子空间](@entry_id:150286)。

一个重要的结果是，空间 $V_\mathbb{C}$ 分解为与**非平凡偶特征**相对应的特征[子空间](@entry_id:150286)的[直和](@entry_id:156782) [@problem_id:3030616]。一个特征 $\chi$ 被称为偶特征，如果它在对应于复共轭的伽罗瓦元素 $\sigma_{-1}$ 上的取值为 $\chi(-1)=1$。
$$ V_\mathbb{C} = \bigoplus_{\substack{\chi \neq \mathbf{1} \\ \chi(-1)=1}} V_\chi $$
其中 $\mathbf{1}$ 是平凡特征，每个 $V_\chi$ 都是一维的。这个分解表明，单位群的结构被伽罗瓦群的偶表示精确地编码。例如，这也解释了为何[单位群的秩](@entry_id:150706)是 $\varphi(n)/2 - 1$，因为这正是非平凡偶特征的数量。这个视角在L函数的p-adic理论和[岩泽理论](@entry_id:197056)中是基础性的。

最后，值得一提的是单位概念的一个重要推广——**[S-单位](@entry_id:194670) (S-units)**。给定一个[数域](@entry_id:155558) $K$，我们可以选取一个包含所有阿基米德place（即由 $r_1$ 个实嵌入和 $r_2$ 个[复嵌入](@entry_id:189961)诱导的范数）的有限place集合 $S$。一个**S-整数**是指那些在 $S$ 之外的所有非阿基米德place（即[素理想](@entry_id:154026)）上都是整数的域中元素。相应地，**[S-单位](@entry_id:194670)群** $\mathcal{O}_{K,S}^\times$ 就是S-整数环中的可[逆元](@entry_id:140790)。

从赋值的角度看，$\mathcal{O}_{K,S}^\times$ 定义为 $K^\times$ 中那些在 $S$ 之外的所有[素理想](@entry_id:154026) $\mathfrak{p}$ 处赋值 $v_\mathfrak{p}(x)$ 为 $0$ 的元素 $x$ [@problem_id:3030606]。这实质上是允许单位在 $S$ 中指定的有限个素理想处有“分母”。

[狄利克雷单位定理](@entry_id:155550)可以推广为**[S-单位](@entry_id:194670)定理**，它声明 $\mathcal{O}_{K,S}^\times$ 也是一个[有限生成阿贝尔群](@entry_id:156372)，其秩为：
$$ \text{rank}(\mathcal{O}_{K,S}^\times) = |S| - 1 $$
其中 $|S|$ 是集合 $S$ 中place的个数。若 $S_f$ 是 $S$ 中有限place的集合，则 $|S| = r_1+r_2+|S_f|$，因此秩为 $r_1+r_2+|S_f|-1$。经典单位群是 $S$ 只包含阿基米德place（即 $|S_f|=0$）时的特例。[S-单位](@entry_id:194670)在[类域论](@entry_id:155687)和伽罗瓦[上同调](@entry_id:160558)等领域扮演着关键角色。