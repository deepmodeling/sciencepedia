## 引言
[霍奇分解定理](@entry_id:199343)是现代几何分析的基石，它在[黎曼流形](@entry_id:261160)的分析学（由度量决定的[微分算子](@entry_id:140145)）与拓扑学（由[上同调群](@entry_id:142450)捕捉的全局[不变量](@entry_id:148850)）之间建立了一座深刻而优美的桥梁。这一定理不仅是微分几何的核心成果，其思想和应用更渗透到[复几何](@entry_id:159080)、代数几何、理论物理乃至新兴的数据科学等多个领域。从根本上说，它解决了一个核心问题：我们如何在一个看似连续和柔性的几何空间中，精确地分离出其刚性的、不变的拓扑结构？[霍奇理论](@entry_id:161814)通过引入调和形式这一分析对象，给出了一个出人意料的解答。

本文旨在为读者提供一个关于[霍奇分解定理](@entry_id:199343)的全面而深入的理解。我们将分三个章节展开：
- **第一章：原理与机制**，我们将从构建[微分形式](@entry_id:146747)的希尔伯特空间开始，系统介绍[霍奇理论](@entry_id:161814)的分析基础，陈述并证明经典定理，并探讨其向[完备流形](@entry_id:190409)和凯勒流形的推广。
- **第二章：应用与跨学科联系**，我们将展示该定理如何作为强大的工具，应用于解决[偏微分方程](@entry_id:141332)、分解矢量场、连接几何与拓扑，并成为[复几何](@entry_id:159080)、[谱几何](@entry_id:186460)乃至离散数据分析的理论核心。
- **第三章：动手实践**，我们将通过具体的计算问题，引导读者亲手推导[内积](@entry_id:158127)表达式、[分析算子](@entry_id:746429)性质以及应用[格林恒等式](@entry_id:176369)，从而将抽象的理论转化为切实的分析技能。

通过这一结构化的学习路径，读者将不仅掌握[霍奇分解定理](@entry_id:199343)的数学精髓，更能领会其在不同学科中展现出的统一性和强大威力。

## 原理与机制

[霍奇分解定理](@entry_id:199343)是[微分几何](@entry_id:145818)中的一块基石，它在微分形式的空间上建立了一个深刻的结构性结果。该定理不仅揭示了[黎曼流形](@entry_id:261160)上分析学（由度量诱导的微分算子）与拓扑学（由[上同调群](@entry_id:142450)捕捉的全局[不变量](@entry_id:148850)）之间的惊人联系，还在[凯勒几何](@entry_id:160314)等领域发挥着核心作用。在本章中，我们将系统地探讨支撑[霍奇理论](@entry_id:161814)的基本原理及其分析机制。我们将从构建分析框架开始，然后陈述并证明[紧致流形](@entry_id:158804)上的经典定理，接着探索其背后的[泛函分析](@entry_id:146220)基础，并将其推广到更一般的[完备流形](@entry_id:190409)上，最后展示其在[复几何](@entry_id:159080)中的强大应用。

### 分析基础：微分形式的[希尔伯特空间](@entry_id:261193)

[霍奇理论](@entry_id:161814)的舞台是微分形式的空间，但我们需要为其配备一个由黎曼度量诱导的[内积](@entry_id:158127)结构。

#### $L^2$ [内积](@entry_id:158127)与前希尔伯特空间

令 $(M, g)$ 是一个 $n$ 维的有向黎曼流形。[黎曼度量](@entry_id:754359) $g$ 在每一点 $x \in M$ 的[余切空间](@entry_id:270516) $T_x^*M$ 上诱导了一个[内积](@entry_id:158127)，并可以自然地推广到任意阶的[外代数](@entry_id:201164)上，从而在 $k$-形式丛 $\Lambda^k T^*M$ 的每个纤维上定义了一个逐点[内积](@entry_id:158127) $\langle\cdot, \cdot\rangle_{g,x}$。

为了定义一个全局[内积](@entry_id:158127)，我们需要一个[体积元](@entry_id:267802)。[流形的定向](@entry_id:160954)与[黎曼度量](@entry_id:754359) $g$ 一起，唯一地确定了一个无处为零的 $n$-形式，称为**[黎曼体积形式](@entry_id:275973)** $\mathrm{vol}_g$。其定义特征是，对于任何正定向的 $g$-[标准正交标架](@entry_id:189702) $(e_1, \dots, e_n)$，都有 $\mathrm{vol}_g(e_1, \dots, e_n) = 1$。如果反转[流形的定向](@entry_id:160954)，体积形式会变为 $-\mathrm{vol}_g$ [@problem_id:3035677]。

现在，我们可以在光滑 $k$-形式的空间 $\Omega^k(M)$ 上定义 **$L^2$ [内积](@entry_id:158127)**：
$$
\langle \alpha, \beta \rangle_{L^2} \coloneqq \int_M \langle \alpha(x), \beta(x) \rangle_{g,x} \, \mathrm{vol}_g
$$
对于任意 $\alpha, \beta \in \Omega^k(M)$。这个[内积](@entry_id:158127)是双线性的、对称的且正定的。[正定性](@entry_id:149643)源于，如果 $\langle \alpha, \alpha \rangle_{L^2} = \int_M \|\alpha(x)\|_g^2 \, \mathrm{vol}_g = 0$，由于被积函数是连续且非负的，它必须恒等于零。因此，$\alpha(x)$ 在每一点都为零。

于是，$(\Omega^k(M), \langle\cdot, \cdot\rangle_{L^2})$ 构成了一个**前希尔伯特空间**（即一个[内积空间](@entry_id:271570)）。然而，这个空间通常不是完备的。也就是说，存在一个由光滑形式组成的柯西序列，其极限在一个更广阔的空间中，这个极限形式可能不是光滑的，甚至不是连续的，而仅仅是可测的。通过标准的完备化程序（即添加所有柯西序列的极限），我们得到一个[希尔伯特空间](@entry_id:261193)，记为 $L^2\Omega^k(M)$。这个空间由所有在 $M$ 上平方可积的可测 $k$-形式（在[几乎处处相等](@entry_id:267606)的意义下）组成。根据[索博列夫空间](@entry_id:141995)的惯例，这个空间也记为 $H^0\Omega^k(M)$ [@problem_id:3035655]。

#### 核心算子：$d$, $*$, $\delta$, 和 $\Delta$

在装备了 $L^2$ [内积](@entry_id:158127)的空间 $\Omega^k(M)$ 上，我们可以定义[霍奇理论](@entry_id:161814)的核心算子：

1.  **外[微分算子](@entry_id:140145) ($d$)**：$d: \Omega^k(M) \to \Omega^{k+1}(M)$ 是一个基本的[微分算子](@entry_id:140145)，它只依赖于[流形](@entry_id:153038)的[光滑结构](@entry_id:159394)，并满足关键的**对合性** $d^2 = d \circ d = 0$。

2.  **[霍奇星算子](@entry_id:197539) ($*$)**：$*: \Omega^k(M) \to \Omega^{n-k}(M)$ 是一个由度量 $g$ 和定向共同决定的[线性同构](@entry_id:270529)。它的定义由以下关系唯一确定：对于任意 $\alpha, \beta \in \Omega^k(M)$，
    $$
    \alpha \wedge *\beta = \langle \alpha, \beta \rangle_g \, \mathrm{vol}_g
    $$
    从这个定义可以看出，如果反转[流形的定向](@entry_id:160954)，$\mathrm{vol}_g$ 会变号，而 $\langle \alpha, \beta \rangle_g$ 不变，这意味着 $*$ 算子也会变号，即 $*' = -*$。有趣的是，尽管 $*$ 算子本身依赖于定向，但 $L^2$ [内积](@entry_id:158127)的另一种等价定义 $\langle \alpha, \beta \rangle_{L^2} = \int_M \alpha \wedge *\beta$ 却不依赖于定向。这是因为反转定向时，积分 $\int_M$ 和 $*$ 算子同时变号，两个负号相互抵消 [@problem_id:3035677]。

3.  **[余微分算子](@entry_id:191334) ($\delta$)**：$\delta: \Omega^k(M) \to \Omega^{k-1}(M)$ 被定义为外微分 $d$ 在 $L^2$ [内积](@entry_id:158127)下的**形式伴随算子**。这意味着对于任何定义域内的 $\alpha \in \Omega^{k-1}(M)$ 和 $\beta \in \Omega^k(M)$，我们有：
    $$
    \langle d\alpha, \beta \rangle_{L^2} = \langle \alpha, \delta\beta \rangle_{L^2}
    $$
    使用[霍奇星算子](@entry_id:197539)，可以给出 $\delta$ 的一个具体表达式：$\delta = (-1)^{n(k+1)+1} *d* $。从这个表达式和 $d^2=0$ 可以推断出 $\delta^2=0$。

4.  **[霍奇-拉普拉斯算子](@entry_id:261049) ($\Delta$)**：$\Delta: \Omega^k(M) \to \Omega^k(M)$ 是一个二阶[椭圆微分算子](@entry_id:635792)，定义为：
    $$
    \Delta = d\delta + \delta d
    $$
    一个 $k$-形式 $\omega$ 如果满足 $\Delta\omega = 0$，则被称为**[调和形式](@entry_id:193378)**。所有调和 $k$-形式构成的空间记为 $\mathcal{H}^k(M)$。

### 紧致流形上的[霍奇分解定理](@entry_id:199343)

有了以上的准备，我们现在可以陈述经典[霍奇分解定理](@entry_id:199343)。

**[霍奇分解定理](@entry_id:199343)**：令 $(M,g)$ 是一个紧致、有向、无边的[黎曼流形](@entry_id:261160)。那么，对于每个 $k \in \{0, 1, \dots, n\}$，光滑 $k$-形式的空间 $\Omega^k(M)$ 可以分解为三个相互 $L^2$-正交的[子空间](@entry_id:150286)的直和：
$$
\Omega^k(M) = \mathcal{H}^k(M) \oplus \mathrm{im}(d) \oplus \mathrm{im}(\delta)
$$
这里，$\mathrm{im}(d) = \{d\alpha \mid \alpha \in \Omega^{k-1}(M)\}$ 是**恰当形式**（exact forms）的空间，而 $\mathrm{im}(\delta) = \{\delta\beta \mid \beta \in \Omega^{k+1}(M)\}$ 是**余恰当形式**（co-exact forms）的空间。

#### 分解的正交性

这个分解的美妙之处在于其正交性，这一点可以直接从算子的定义中推导出来 [@problem_id:2978686] [@problem_id:3035651]。

首先，我们需要一个关于调和形式的关键性质。在紧致无边[流形](@entry_id:153038)上，一个形式是调和的当且仅当它既是**闭的**（closed, $d\omega=0$）又是**余闭的**（co-closed, $\delta\omega=0$）。这可以通过计算 $\langle \Delta\omega, \omega \rangle_{L^2}$ 来证明：
$$
\langle \Delta\omega, \omega \rangle_{L^2} = \langle (d\delta + \delta d)\omega, \omega \rangle_{L^2} = \langle d\delta\omega, \omega \rangle_{L^2} + \langle \delta d\omega, \omega \rangle_{L^2}
$$
利用 $\delta$ 是 $d$ 的伴随算子这一性质，我们得到：
$$
\langle \Delta\omega, \omega \rangle_{L^2} = \langle \delta\omega, \delta\omega \rangle_{L^2} + \langle d\omega, d\omega \rangle_{L^2} = \|\delta\omega\|_{L^2}^2 + \|d\omega\|_{L^2}^2
$$
如果 $\omega$ 是调和的，即 $\Delta\omega = 0$，那么左边为零。由于[内积](@entry_id:158127)的[正定性](@entry_id:149643)，这意味着 $\|d\omega\|_{L^2}^2 = 0$ 和 $\|\delta\omega\|_{L^2}^2 = 0$，从而 $d\omega = 0$ 且 $\delta\omega = 0$。

现在，我们可以证明三个[子空间](@entry_id:150286)是两两正交的：

1.  **$\mathcal{H}^k(M) \perp \mathrm{im}(d)$**：令 $h \in \mathcal{H}^k(M)$ 且 $\alpha \in \Omega^{k-1}(M)$。
    $$
    \langle h, d\alpha \rangle_{L^2} = \langle \delta h, \alpha \rangle_{L^2} = \langle 0, \alpha \rangle_{L^2} = 0
    $$

2.  **$\mathcal{H}^k(M) \perp \mathrm{im}(\delta)$**：令 $h \in \mathcal{H}^k(M)$ 且 $\beta \in \Omega^{k+1}(M)$。
    $$
    \langle h, \delta\beta \rangle_{L^2} = \langle dh, \beta \rangle_{L^2} = \langle 0, \beta \rangle_{L^2} = 0
    $$

3.  **$\mathrm{im}(d) \perp \mathrm{im}(\delta)$**：令 $\alpha \in \Omega^{k-1}(M)$ 且 $\beta \in \Omega^{k+1}(M)$。
    $$
    \langle d\alpha, \delta\beta \rangle_{L^2} = \langle d(d\alpha), \beta \rangle_{L^2} = \langle d^2\alpha, \beta \rangle_{L^2} = \langle 0, \beta \rangle_{L^2} = 0
    $$

这些简单的计算优雅地证明了分解的正交性。然而，分解的**存在性**——即任何一个光滑形式都可以被这样分解——是一个更深刻的结果，其根源在于[泛函分析](@entry_id:146220)和[椭圆算子](@entry_id:181616)理论。

#### 存在性背后的机制

[霍奇分解定理](@entry_id:199343)的存在性部分，是**[椭圆算子](@entry_id:181616)理论**在紧致流形上应用的辉煌成果 [@problem_id:2978682]。其核心逻辑如下：

1.  **拉普拉斯算子的椭圆性**：[霍奇-拉普拉斯算子](@entry_id:261049) $\Delta$ 是一个二阶**椭圆型偏[微分算子](@entry_id:140145)**。椭圆性是一个技术性条件，大致意味着算子在所有方向上都表现得像拉普拉斯算子，这使得它具有非常好的正则性性质。

2.  **紧致性与Fredholm性质**：在紧致流形上，[椭圆算子](@entry_id:181616)具有卓越的谱性质。关键的分析工具是 **[Rellich-Kondrachov](@entry_id:140267) 紧[嵌入定理](@entry_id:150872)**，它指出[索博列夫空间](@entry_id:141995) $H^s(M)$ 到 $H^t(M)$（当 $s>t$ 时）的嵌入是紧算子。由于 $\Delta$ 是椭圆的，它的逆（在与核正交的空间上）是一个光滑化算子。具体来说，解算子 $(\Delta+I)^{-1}: L^2\Omega^k(M) \to H^2\Omega^k(M)$ 是有界的。与[紧嵌入](@entry_id:263276) $H^2 \hookrightarrow L^2$ 复合后，我们发现**解算子** $(\Delta+I)^{-1}: L^2\Omega^k(M) \to L^2\Omega^k(M)$ 是一个**紧算子**。

3.  **谱理论与有限维调和形式**：根据希尔伯特空间上[紧自伴算子](@entry_id:147701)的[谱理论](@entry_id:275351)，一个具有紧解算子的[自伴算子](@entry_id:152188)（如 $\Delta$）具有[离散谱](@entry_id:150970)，且每个[特征空间](@entry_id:638014)的维数是有限的。特别是，$\Delta$ 的核，即[调和形式](@entry_id:193378)空间 $\mathcal{H}^k(M)$，是有限维的。这便是连接分析（[调和形式](@entry_id:193378)）与拓扑（[贝蒂数](@entry_id:153109)）的桥梁，因为霍奇[同构定理](@entry_id:145702)将断言 $\dim \mathcal{H}^k(M)$ 等于第 $k$ 个贝蒂数 $b_k$。

4.  **闭值域与分解**：椭圆估计还保证了算子 $d$ 和 $\delta$ 的值域在 $L^2$ 空间中是闭的。这确保了 $L^2\Omega^k(M)$ 可以被分解为 $\ker(\Delta) \oplus \overline{\mathrm{im}(\Delta)}$，并且 $\overline{\mathrm{im}(\Delta)}$ 可以进一步分解为 $\overline{\mathrm{im}(d)} \oplus \overline{\mathrm{im}(\delta)}$。由于值域是闭的，我们不需要[闭包](@entry_id:148169)符号。最后，**[椭圆正则性](@entry_id:177548)**确保了如果一个 $L^2$ 形式被分解为三个 $L^2$ 分量，且原始形式是光滑的，那么它的每个分量也都可以被选择为光滑的。这使得分解从 $L^2$ 空间回到了光滑形式空间 $\Omega^k(M)$。

为了更精确地描述这些分析工具，我们需要引入**索博列夫空间** $H^s\Omega^k(M)$。这些空间是通过[局部坐标](@entry_id:181200)卡和单位分解来定义的，它们由直到 $s$ 阶[弱导数](@entry_id:189356)都属于 $L^2$ 的形式组成。在这个框架下，像 $d$ 和 $\delta$ 这样的一阶微分算子，可以被看作是从 $H^s\Omega^k(M)$ 到 $H^{s-1}\Omega^{k \pm 1}(M)$ 的有界[线性映射](@entry_id:185132)，这对于所有实数 $s$ 都成立 [@problem_id:3035663]。

### 推广到[完备非紧流形](@entry_id:634266)

经典[霍奇理论](@entry_id:161814)依赖于[流形](@entry_id:153038)的紧致性。当[流形](@entry_id:153038)非紧时，[Rellich-Kondrachov](@entry_id:140267) 紧[嵌入定理](@entry_id:150872)不再成立，$\Delta$ 的解算子不再是紧的，其谱可以是连续的，调和形式空间 $\mathcal{H}^k_{(2)}(M)$ 也可能是无限维的。此外，$d$ 和 $\delta$ 的值域也未必是闭的。

然而，如果我们将紧致性条件放宽为**完备性**，仍然可以得到一个有意义的 $L^2$ 版本的[霍奇分解](@entry_id:160332)。完备的[黎曼流形](@entry_id:261160)是指其上的[测地线](@entry_id:269969)可以无限延伸。

#### Gaffney 定理与[本质自伴性](@entry_id:264279)

在[非紧流形](@entry_id:185981)上，一个关键的技术问题是微分[算子的定义域](@entry_id:152686)。对于定义在光滑[紧支撑](@entry_id:276214)形式 $C_c^\infty(\Lambda^k T^*M)$ 上的[拉普拉斯算子](@entry_id:146319) $\Delta_0$，它只是一个[对称算子](@entry_id:272489)。为了应用[谱理论](@entry_id:275351)，我们需要一个自伴的延拓。**Gaffney 定理**断言，如果 $(M,g)$ 是完备的，那么 $\Delta_0$ 是**本质自伴的**，即它有唯一的自伴延拓 $\Delta$ [@problem_id:3035660]。

这个定理的证明依赖于[完备流形](@entry_id:190409)上存在一族特殊的截断函数，这些函数可以用来控制积分中的“边界项”，确保在取极限时边界项消失。这[实质](@entry_id:149406)上保证了 $d$ 的最小延拓和最大延拓是一致的，从而其[伴随算子](@entry_id:140236) $\delta$ 也是良定义的 [@problem_id:3035660] [@problem_id:3035650]。

#### $L^2$ [霍奇分解](@entry_id:160332)

有了良定义的自伴拉普拉斯算子 $\Delta$，我们可以在[希尔伯特空间](@entry_id:261193) $L^2\Omega^k(M)$ 上应用谱理论。这给出了如下的**$L^2$ [霍奇分解定理](@entry_id:199343)**：

令 $(M,g)$ 是一个完备、有向的黎曼流形。那么，平方可积 $k$-形式的希尔伯特空间 $L^2\Omega^k(M)$ 可以分解为三个相互正交的[闭子空间](@entry_id:267213)的直和：
$$
L^2\Omega^k(M) = \mathcal{H}_{(2)}^k(M) \oplus \overline{\mathrm{im}(d)} \oplus \overline{\mathrm{im}(\delta)}
$$
这里，$\mathcal{H}_{(2)}^k(M)$ 是 $L^2$-调和形式空间（即 $\Delta$ 在 $L^2\Omega^k(M)$ 中的核），$\overline{\mathrm{im}(d)}$ 和 $\overline{\mathrm{im}(\delta)}$ 分别是恰当形式和余恰当形式在 $L^2$ 范数下的[闭包](@entry_id:148169)。与紧致情况不同，这里的[闭包](@entry_id:148169)是必不可少的 [@problem_id:3035650]。

### [凯勒流形](@entry_id:161192)上的[霍奇理论](@entry_id:161814)

[霍奇理论](@entry_id:161814)在[复几何](@entry_id:159080)，特别是**[凯勒几何](@entry_id:160314)**中，展现了其最深刻和最富有成果的一面。

#### $(p,q)$ 型分解与[凯勒条件](@entry_id:637291)

在复维数为 $n$ 的[复流形](@entry_id:159076) $(M,J)$ 上，复值微分形式的空间 $\Omega^k(M, \mathbb{C})$ 有一个典范的分解。[复结构](@entry_id:269128) $J$ (满足 $J^2 = -\mathrm{Id}$) 将[复化](@entry_id:260775)的[切空间](@entry_id:199137)分裂为 $TM \otimes \mathbb{C} = T^{(1,0)}M \oplus T^{(0,1)}M$，分别是 $J$ 的 $+i$ 和 $-i$ 特征[子空间](@entry_id:150286)。对偶地，[复化](@entry_id:260775)的[余切空间](@entry_id:270516)也分裂。这导致了 $k$-形式空间可以被细分为**$(p,q)$-形式**的空间 $\Omega^{p,q}(M)$，其中 $p+q=k$：
$$
\Omega^k(M, \mathbb{C}) = \bigoplus_{p+q=k} \Omega^{p,q}(M)
$$
外[微分算子](@entry_id:140145) $d$ 也相应地分裂为 $d = \partial + \bar{\partial}$，其中 $\partial: \Omega^{p,q}(M) \to \Omega^{p+1,q}(M)$ 且 $\bar{\partial}: \Omega^{p,q}(M) \to \Omega^{p,q+1}(M)$。

一个**[凯勒流形](@entry_id:161192)**是一个[复流形](@entry_id:159076)，其上带有一个与复结构 $J$ 相容的[黎曼度量](@entry_id:754359) $g$（即 $g(JX, JY) = g(X,Y)$），并且由 $g$ 和 $J$ 定义的[基本2-形式](@entry_id:183276) $\omega(X,Y) = g(JX,Y)$ 是一个闭形式，即满足**[凯勒条件](@entry_id:637291)** $d\omega = 0$ [@problem_id:3035648]。

#### [霍奇分解](@entry_id:160332)与[上同调](@entry_id:160558)

在紧致凯勒流形上，[凯勒条件](@entry_id:637291) $d\omega=0$ 导致了这些算子 $d, \delta, \partial, \bar{\partial}$ 及其伴随算子之间一系列惊人的**凯勒恒等式**。其中最核心的一个是[拉普拉斯算子](@entry_id:146319)之间的关系：
$$
\Delta_d = 2\Delta_{\partial} = 2\Delta_{\bar{\partial}}
$$
其中 $\Delta_{\partial} = \partial\partial^* + \partial^*\partial$ 和 $\Delta_{\bar{\partial}} = \bar{\partial}\bar{\partial}^* + \bar{\partial}^*\bar{\partial}$。

这个恒等式意味着一个形式是 $d$-调和的，当且仅当它是 $\partial$-调和的，也当且仅当它是 $\bar{\partial}$-调和的。由于这些拉普拉斯算子都保持 $(p,q)$ 类型，[调和形式](@entry_id:193378)空间也相应地分解：
$$
\mathcal{H}^k(M, \mathbb{C}) = \bigoplus_{p+q=k} \mathcal{H}^{p,q}(M)
$$
其中 $\mathcal{H}^{p,q}(M)$ 是调和 $(p,q)$-形式的空间。

根据[霍奇定理](@entry_id:196610)，[德拉姆上同调](@entry_id:158673)群 $H^k(M, \mathbb{C})$ 同构于 $\mathcal{H}^k(M, \mathbb{C})$。而根据多尔博（Dolbeault）定理，$H^{p,q}(M) \cong \mathcal{H}^{p,q}(M)$。因此，上同调群本身也分裂为[直和](@entry_id:156782)：
$$
H^k(M, \mathbb{C}) \cong \bigoplus_{p+q=k} H^{p,q}(M)
$$
这就是[凯勒流形](@entry_id:161192)上的**[霍奇分解](@entry_id:160332)**。它将一个[拓扑不变量](@entry_id:138526)（[德拉姆上同调](@entry_id:158673)）分解为更精细的、蕴含了[复结构](@entry_id:269128)信息的片段（[多尔博上同调](@entry_id:203257)）[@problem_id:3035649]。

#### [霍奇数](@entry_id:161605)与霍奇菱形

这个分解的维数关系为我们提供了**[霍奇数](@entry_id:161605)** $h^{p,q} = \dim H^{p,q}(M)$ 和**[贝蒂数](@entry_id:153109)** $b_k = \dim H^k(M, \mathbb{C})$ 之间的关系：
$$
b_k = \sum_{p+q=k} h^{p,q}
$$
此外，[霍奇数](@entry_id:161605)还满足一些重要的对称性。复共轭运算将一个 $(p,q)$-形式映为一个 $(q,p)$-形式，并且与拉普拉斯算子 $\Delta_d$ 可交换。因此，它诱导了 $\mathcal{H}^{p,q}(M)$ 和 $\mathcal{H}^{q,p}(M)$ 之间的一个反[线性同构](@entry_id:270529)，这意味着它们的维数相等：
$$
h^{p,q} = h^{q,p}
$$
另一个对称性 $h^{p,q} = h^{n-p, n-q}$ 来自于[霍奇星算子](@entry_id:197539)诱导的[庞加莱对偶](@entry_id:161676)。这些对称性使得我们可以将[霍奇数](@entry_id:161605)[排列](@entry_id:136432)成一个菱形图案，称为**霍奇菱形**，它优雅地展示了紧致凯勒流形[上同调](@entry_id:160558)结构的丰富对称性 [@problem_id:3035649]。