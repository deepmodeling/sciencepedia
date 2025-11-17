## 引言
数域，作为有理[数域](@entry_id:155558)的[有限扩张](@entry_id:152412)，是[代数数论](@entry_id:148067)的核心研究对象。然而，作为一个抽象的[代数结构](@entry_id:137052)，其内在的算术和几何性质往往难以直接探究。我们如何才能将这些抽象的域与我们更熟悉的、具有丰富几何与分析工具的复数域 $\mathbb{C}$ 联系起来呢？这个问题的答案在于“嵌入”——将[数域](@entry_id:155558)以保持其结构的方式“置入”复数之中的映射。

本文系统地探讨了数域到复数的[嵌入理论](@entry_id:203677)及其深远的应用。我们将揭示，一个数域有多少种不同的嵌入方式，以及这些方式的性质，是理解该[数域](@entry_id:155558)一切深刻属性的起点。

在“原理与机制”一章中，我们将从第一性原理出发，定义什么是嵌入，阐明为何一个 n 次数域恰有 n 个嵌入，并引入关键[不变量](@entry_id:148850)“符号”(r1, r2) 来分类这些嵌入。接着，在“应用与跨学科联系”一章中，我们将见证这一理论的威力，看它如何通过[闵可夫斯基嵌入](@entry_id:189382)将[数域](@entry_id:155558)转化为几何格，如何通过[狄利克雷单位定理](@entry_id:155550)揭示[单位群](@entry_id:184012)的结构，并如何与[解析数论](@entry_id:158402)中的深刻公式产生联系。最后，“动手实践”部分将通过具体问题，帮助读者巩固这些核心概念。通过本文的学习，读者将理解嵌入如何成为连接抽象代数、[欧几里得几何](@entry_id:634933)与[复分析](@entry_id:167282)的中心枢纽，为深入探索现代数论铺平道路。

## 原理与机制

在上一章中，我们介绍了数域作为有理[数域](@entry_id:155558) $\mathbb{Q}$ 的[有限扩张](@entry_id:152412)的概念。一个[数域](@entry_id:155558) $K$ 是一个抽象的[代数结构](@entry_id:137052)，但数论中的许多深刻问题都源于它与复数域 $\mathbb{C}$ 之间的具体联系。本章的核心任务是系统地阐述将一个抽象[数域](@entry_id:155558) $K$ “置入”或“实现”为[复数域](@entry_id:153768) $\mathbb{C}$ 的[子域](@entry_id:155812)的各种方式。这些实现方式被称为 **嵌入 (embeddings)**，它们是研究[数域](@entry_id:155558)算术和几何性质的基本工具。

### 嵌入的定义与基本性质

一个从[数域](@entry_id:155558) $K$ 到复数域 $\mathbb{C}$ 的 **嵌入 (embedding)** 是一个[域同态](@entry_id:155269) $\sigma: K \to \mathbb{C}$。由于任何非零的[域同态](@entry_id:155269)都是单射的，因此嵌入实际上是将 $K$ 同构地映射到 $\mathbb{C}$ 的一个[子域](@entry_id:155812) $\sigma(K)$ 上。根据定义，任何[域同态](@entry_id:155269)都必须将乘法单位 $1_K$ 映为 $1_{\mathbb{C}}$。由此可以推断，任何嵌入都逐点固定 $K$ 的[素域](@entry_id:634209) $\mathbb{Q}$，即对任意 $q \in \mathbb{Q}$，都有 $\sigma(q) = q$。因此，我们通常称之为 **$\mathbb{Q}$-嵌入**。

一个基础性定理指出，任何次数为 $n = [K:\mathbb{Q}]$ 的数域 $K$，都恰好有 $n$ 个不同的到 $\mathbb{C}$ 的 $\mathbb{Q}$-嵌入。这些嵌入的集合记为 $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$。

这些嵌入是如何确定的呢？根据[本原元](@entry_id:154321)素定理，任何数域 $K$ 都可以表示为 $K = \mathbb{Q}(\alpha)$ 的形式，其中 $\alpha \in K$ 是某个[代数数](@entry_id:150888)。由于嵌入 $\sigma$ 固定了 $\mathbb{Q}$，它的行为完全由它对生成元 $\alpha$ 的作用所决定。设 $\alpha$ 在 $\mathbb{Q}$ 上的极小多项式为 $m_{\alpha}(x) \in \mathbb{Q}[x]$，其次数为 $n$。对 $m_{\alpha}(\alpha)=0$ 两边作用 $\sigma$，我们得到：
$$ \sigma(m_{\alpha}(\alpha)) = m_{\alpha}(\sigma(\alpha)) = 0 $$
这里第二个等式成立是因为 $m_{\alpha}(x)$ 的系数均为有理数，而被 $\sigma$ 固定。这表明 $\sigma(\alpha)$ 必须是 $m_{\alpha}(x)$ 在 $\mathbb{C}$ 中的一个根。由于特征为零的域上的不[可约多项式](@entry_id:148759)都是可分的，$m_{\alpha}(x)$ 在 $\mathbb{C}$ 中恰有 $n$ 个不同的根。每一个根都唯一地确定了一个嵌入。

最简单的例子是二次域 $K = \mathbb{Q}(\sqrt{d})$，其中 $d$ 是一个非零的无平方因子整数。这里 $[K:\mathbb{Q}]=2$，生成元 $\sqrt{d}$ 的极小多项式是 $x^2-d=0$。它在 $\mathbb{C}$ 中的两个根是 $\sqrt{d}$ 和 $-\sqrt{d}$。因此，存在两个嵌入：
1.  恒等嵌入 $\sigma_1$，定义为 $\sigma_1(a+b\sqrt{d}) = a+b\sqrt{d}$。
2.  共轭嵌入 $\sigma_2$，定义为 $\sigma_2(a+b\sqrt{d}) = a-b\sqrt{d}$。

### [数域](@entry_id:155558)的符号

尽管所有嵌入都以 $\mathbb{C}$ 为靶域，但它们的像域 $\sigma(K)$ 的性质可能有所不同。这种差异引出了数域的一个关键[不变量](@entry_id:148850)——**符号 (signature)**。

一个嵌入 $\sigma: K \to \mathbb{C}$ 如果其像域完全包含于[实数域](@entry_id:151347) $\mathbb{R}$ 中，即 $\sigma(K) \subseteq \mathbb{R}$，则被称为 **实嵌入 (real embedding)**。否则，它被称为 **[复嵌入](@entry_id:189961) (complex embedding)**。

[复嵌入](@entry_id:189961)具有一个重要的对称性。令 $c: \mathbb{C} \to \mathbb{C}$ 为[复共轭](@entry_id:174690)映射 $z \mapsto \bar{z}$。如果 $\sigma$ 是一个[复嵌入](@entry_id:189961)，那么复合映射 $\bar{\sigma} := c \circ \sigma$ 也是一个从 $K$ 到 $\mathbb{C}$ 的嵌入。由于 $\sigma$ 是[复嵌入](@entry_id:189961)，存在某个 $\alpha \in K$ 使得 $\sigma(\alpha) \notin \mathbb{R}$，这意味着 $\sigma(\alpha) \neq \overline{\sigma(\alpha)}$。因此 $\sigma \neq \bar{\sigma}$。这意味着[复嵌入](@entry_id:189961)总是成对出现的，每一对 $(\sigma, \bar{\sigma})$ 称为一个 **共轭[复嵌入](@entry_id:189961)对**。

[数域](@entry_id:155558) $K$ 的 **符号 (signature)** 是一个[有序对](@entry_id:269702) $(r_1, r_2)$，其中：
-   $r_1$ 是实嵌入的数量。
-   $r_2$ 是共轭[复嵌入](@entry_id:189961)对的数量。

由于总嵌入数是 $n=[K:\mathbb{Q}]$，并且[复嵌入](@entry_id:189961)成对出现（总数为 $2r_2$），我们得到了基本的关系式：
$$ n = [K:\mathbb{Q}] = r_1 + 2r_2 $$
这个关系式是代数数论中的基本恒等式，它将数域的抽象次数与其在复数域中的[几何实现](@entry_id:265700)联系起来。

**示例 1：二次域**
对于二次域 $K = \mathbb{Q}(\sqrt{d})$ [@problem_id:3013296]，其符号取决于 $d$ 的正负。
-   若 $d > 0$，$\sqrt{d}$ 是实数，因此 $K = \mathbb{Q}(\sqrt{d})$ 是 $\mathbb{R}$ 的一个[子域](@entry_id:155812)。两个嵌入 $\sigma_1$ 和 $\sigma_2$ 的像域都是 $K$ 本身，因此都是实嵌入。此时 $r_1=2, r_2=0$，符号为 $(2,0)$。
-   若 $d  0$，$\sqrt{d}$ 是纯虚数，例如 $\sqrt{-3} = i\sqrt{3}$。此时 $K$ 不是 $\mathbb{R}$ 的[子域](@entry_id:155812)。两个嵌入 $\sigma_1(a+b\sqrt{d}) = a+b\sqrt{d}$ 和 $\sigma_2(a+b\sqrt{d}) = a-b\sqrt{d} = \overline{\sigma_1(a+b\sqrt{d})}$ 都是[复嵌入](@entry_id:189961)，且互为共轭。此时 $r_1=0, r_2=1$，符号为 $(0,1)$。
我们可以用[符号函数](@entry_id:167507) $\mathrm{sgn}(d)$ 将此统一表示：$r_1 = 1 + \mathrm{sgn}(d)$ 以及 $r_2 = (1 - \mathrm{sgn}(d))/2$（对于 $d0$ 的情况，$\mathrm{sgn}(d)$ 取值为-1）。

**示例 2：通过实[根计数](@entry_id:137502)确定符号**
对于由更高次的不[可约多项式](@entry_id:148759) $f(x)$ 生成的[数域](@entry_id:155558) $K = \mathbb{Q}[x]/(f(x))$，实嵌入的数量 $r_1$ 正好等于 $f(x)$ 的实根个数。我们可以利用微积分中的方法来确定实根的数量 [@problem_id:3013292]。考虑多项式 $f(x) = x^5 - 10x + 5$。它的导数是 $f'(x) = 5x^4 - 10$，令 $f'(x)=0$ 得到实数[临界点](@entry_id:144653) $x = \pm \sqrt[4]{2}$。通过分析 $f(x)$ 在这些[临界点](@entry_id:144653)的值以及在无穷远处的行为：
-   $f(-\sqrt[4]{2}) = 8\sqrt[4]{2} + 5 > 0$ ([局部极大值](@entry_id:137813))。
-   $f(\sqrt[4]{2}) = 5 - 8\sqrt[4]{2}  0$ (局部极小值)。
-   当 $x \to -\infty$ 时，$f(x) \to -\infty$；当 $x \to \infty$ 时，$f(x) \to \infty$。

根据介值定理， $f(x)$ 在 $(-\infty, -\sqrt[4]{2})$、$(-\sqrt[4]{2}, \sqrt[4]{2})$ 和 $(\sqrt[4]{2}, \infty)$ 三个区间内各有且仅有一个实根。因此，$f(x)$ 共有 3 个实根，$r_1=3$。由于域的次数是 $n=5$，根据 $5 = r_1 + 2r_2 = 3 + 2r_2$，我们得到 $r_2=1$。所以[数域](@entry_id:155558) $K=\mathbb{Q}[x]/(x^5-10x+5)$ 的符号是 $(3,1)$。

### 嵌入、自同构与[正规扩张](@entry_id:156398)

我们需要仔细区分两种重要的同态：一般的嵌入 $\sigma: K \to \mathbb{C}$ 和 **[自同构](@entry_id:155390) (automorphism)** $\tau: K \to K$。自同构是一种特殊的嵌入，其像域恰好是 $K$ 本身。一个数域 $K$ 的所有 $\mathbb{Q}$-[自同构](@entry_id:155390)构成一个群，记为 $\operatorname{Aut}_{\mathbb{Q}}(K)$。

一个自然的问题是：在何种条件下，一个[数域](@entry_id:155558) $K$ 的所有嵌入都是[自同构](@entry_id:155390)？这个问题的答案引出了代数数论的核心概念之一：**[正规扩张](@entry_id:156398) (normal extension)**。一个[数域](@entry_id:155558) $K$ 被称为 $\mathbb{Q}$ 的[正规扩张](@entry_id:156398)，如果对于任何在 $\mathbb{Q}[x]$ 中的不[可约多项式](@entry_id:148759)，只要它在 $K$ 中有一个根，那么它的所有根都必须在 $K$ 中。

以下三个命题是等价的，它们构成了 Galois 理论的基石 [@problem_id:3013302]：
1.  $K/\mathbb{Q}$ 是一个[正规扩张](@entry_id:156398)。
2.  对于 $K$ 的任意嵌入 $\sigma: K \to \mathbb{C}$，都有 $\sigma(K) = K$（这里我们将 $K$ 视为通过某个固定的嵌入包含于 $\mathbb{C}$）。
3.  $K$ 的嵌入集合 $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ 与其[自同构群](@entry_id:139672) $\operatorname{Aut}_{\mathbb{Q}}(K)$ 是同一集合。

**[正规扩张](@entry_id:156398)示例**：任何二次域 $K=\mathbb{Q}(\sqrt{d})$ 都是[正规扩张](@entry_id:156398)。如前所述，其两个嵌入的像域都是 $K$ 本身，因此它们都是自同构。

**非[正规扩张](@entry_id:156398)示例**：$K = \mathbb{Q}(\sqrt[3]{2})$ 是一个典型的非[正规扩张](@entry_id:156398) [@problem_id:3013297]。其次数为 $3$，由不[可约多项式](@entry_id:148759) $x^3-2=0$ 定义。该多项式在 $\mathbb{C}$ 中的三个根是 $\alpha_1 = \sqrt[3]{2}$, $\alpha_2 = \sqrt[3]{2}\omega$, $\alpha_3 = \sqrt[3]{2}\omega^2$，其中 $\omega = \exp(2\pi i/3)$。$K$ 可以被视为 $\mathbb{R}$ 的[子域](@entry_id:155812)，因为它是由实数 $\sqrt[3]{2}$ 生成的。然而，它只有三个嵌入中的一个是实嵌入（恒等嵌入），另外两个是[复嵌入](@entry_id:189961)，分别将 $\sqrt[3]{2}$ 映到 $\alpha_2$ 和 $\alpha_3$。这两个[复嵌入](@entry_id:189961)的像域，例如 $\sigma_2(K) = \mathbb{Q}(\sqrt[3]{2}\omega)$，包含了非实数，因此显然不等于 $K$。这表明 $K/\mathbb{Q}$ 不是[正规扩张](@entry_id:156398)。

对于非[正规扩张](@entry_id:156398)，嵌入的行为可能更加复杂。例如，对于上述的嵌入 $\sigma_2: K \to \mathbb{C}$，其像域是 $\sigma_2(K) = \mathbb{Q}(\sqrt[3]{2}\omega)$。其共轭嵌入 $\bar{\sigma_2}$ 的像域是 $\overline{\sigma_2(K)} = \mathbb{Q}(\overline{\sqrt[3]{2}\omega}) = \mathbb{Q}(\sqrt[3]{2}\omega^2)$。由于 $2$ 不是 $3$ 的倍数，$\mathbb{Q}(\sqrt[3]{2}\omega)$ 和 $\mathbb{Q}(\sqrt[3]{2}\omega^2)$ 是 $\mathbb{C}$ 中两个不同的[子域](@entry_id:155812)。这意味着 $\sigma_2(K)$ 本身并非在[复共轭](@entry_id:174690)下保持不变 [@problem_id:3013304]。这是非[正规扩张](@entry_id:156398)的一个深刻特征：嵌入的像域不一定具有我们期望的对称性。

### 嵌入集的结构

我们可以从[群作用](@entry_id:268812)的视角来理解数域的符号。复共轭映射 $c: z \mapsto \bar{z}$ 是 $\mathbb{C}$ 的一个[自同构](@entry_id:155390)，它可以后作用于嵌入集 $\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ 上。对于任意嵌入 $\sigma$，我们定义 $c \cdot \sigma = c \circ \sigma = \bar{\sigma}$。这个作用将嵌入集划分为若干个[轨道](@entry_id:137151) [@problem_id:3013303]。

-   **[不动点](@entry_id:156394)**：一个嵌入 $\sigma$ 是该作用下的[不动点](@entry_id:156394)，当且仅当 $\bar{\sigma} = \sigma$。这意味着对所有 $\alpha \in K$，$\overline{\sigma(\alpha)} = \sigma(\alpha)$，这等价于 $\sigma(K) \subseteq \mathbb{R}$。因此，**该作用的[不动点](@entry_id:156394)恰好是所有的实嵌入**。[不动点](@entry_id:156394)的数量就是 $r_1$。

-   **[轨道](@entry_id:137151)**：如果 $\sigma$ 不是[不动点](@entry_id:156394)（即它是一个[复嵌入](@entry_id:189961)），那么它的[稳定子群](@entry_id:137216)是平凡的，根据[轨道](@entry_id:137151)-稳定子定理，它的[轨道](@entry_id:137151)大小为 $2$。这个[轨道](@entry_id:137151)就是共轭对 $\{\sigma, \bar{\sigma}\}$。**所有的[复嵌入](@entry_id:189961)被划分为 $r_2$ 个大小为 2 的[轨道](@entry_id:137151)**。

因此，$\operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})$ 在复[共轭作用](@entry_id:143328)下分解为 $r_1$ 个大小为 1 的[轨道](@entry_id:137151)（[不动点](@entry_id:156394)）和 $r_2$ 个大小为 2 的[轨道](@entry_id:137151)。总[轨道](@entry_id:137151)数就是 $r_1+r_2$。这一视角为符号 $(r_1, r_2)$ 提供了一个优雅的组合解释。

### 域扩张的嵌入

当[数域](@entry_id:155558)之间存在包含关系 $\mathbb{Q} \subset F \subset K$ 时，它们的嵌入集之间也存在着深刻的结构性关联。任何 $K$ 的嵌入 $\sigma: K \to \mathbb{C}$，当其限制在子域 $F$ 上时，自然给出了一个 $F$ 的嵌入 $\sigma|_F: F \to \mathbb{C}$。这定义了一个 **限制映射 (restriction map)**：
$$ \operatorname{res}: \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C}) \to \operatorname{Hom}_{\mathbb{Q}}(F, \mathbb{C}), \quad \sigma \mapsto \sigma|_F $$
这个映射的纤维 (fiber) 包含了所有扩展了 $F$ 的同一个嵌入的 $K$ 的嵌入。一个关键的结果是，这个映射的每个纤维的大小都是相同的，其值恰好是扩张次数 $[K:F]$ [@problem_id:3013305]。

**定理**：对于任意给定的 $F$ 的嵌入 $\tau: F \to \mathbb{C}$，能够扩展 $\tau$ 的 $K$ 的嵌入 $\sigma$（即满足 $\sigma|_F = \tau$）的数量恰好为 $[K:F]$。

这个定理对于计算[复合域](@entry_id:151036)的符号非常有用。考虑域 $K = \mathbb{Q}(\sqrt[3]{2}, \sqrt{5})$ [@problem_id:3024688]。这是一个次数为 $[K:\mathbb{Q}] = [\mathbb{Q}(\sqrt[3]{2}):\mathbb{Q}] \cdot [\mathbb{Q}(\sqrt{5}):\mathbb{Q}] = 3 \cdot 2 = 6$ 的域。$K$ 的一个嵌入 $\sigma$ 由它对 $\alpha = \sqrt[3]{2}$ 和 $\beta = \sqrt{5}$ 的作用唯一确定。

-   $\sigma(\alpha)$ 必须是 $x^3-2=0$ 的根之一：$\{\sqrt[3]{2}, \sqrt[3]{2}\omega, \sqrt[3]{2}\omega^2\}$。其中有 1 个实根和 2 个[复根](@entry_id:172941)。
-   $\sigma(\beta)$ 必须是 $x^2-5=0$ 的根之一：$\{\sqrt{5}, -\sqrt{5}\}$。两者都是实根。

一个嵌入 $\sigma$是实嵌入，当且仅当它将所有生成元映为实数。
-   要使 $\sigma(\alpha)$ 为实数，只有 1 种选择：$\sigma(\alpha) = \sqrt[3]{2}$。
-   要使 $\sigma(\beta)$ 为实数，有 2 种选择：$\sigma(\beta) = \pm\sqrt{5}$。

因此，实嵌入的总数是 $r_1 = 1 \times 2 = 2$。根据 $n = r_1+2r_2$，我们有 $6 = 2 + 2r_2$，解得 $r_2=2$。故 $K$ 的符号为 $(2,2)$。

### 几类重要的域

根据符号的特点，我们可以对[数域](@entry_id:155558)进行分类。

-   **全实域 (Totally Real Field)**：如果一个数域的所有嵌入都是实嵌入，即 $r_2=0$（或等价地 $r_1=n$），则称之为全实域。例如 $\mathbb{Q}(\sqrt{d})$ 当 $d>0$ 时。

-   **全虚域 (Totally Imaginary Field)**：如果一个数域没有任何实嵌入，即 $r_1=0$（或等价地 $n=2r_2$），则称之为全虚域。例如 $\mathbb{Q}(\sqrt{d})$ 当 $d0$ 时。

-   **CM 域 (Complex Multiplication Field)**：这是一类特别重要的全虚域。一个数域 $K$ 被称为 **CM 域**，如果它是一个全实域 $F$ 的二次扩张（即 $[K:F]=2$），并且 $K$ 本身是全虚的。CM 域在[代数几何](@entry_id:156300)和[类域论](@entry_id:155687)中扮演着核心角色。

分圆域 $K = \mathbb{Q}(\zeta_m)$（其中 $\zeta_m = \exp(2\pi i/m)$）是 CM 域的典型例子 [@problem_id:3013294]。考虑 $K=\mathbb{Q}(\zeta_9)$，其次数为 $\phi(9)=6$。
-   它的嵌入由 $\sigma_k(\zeta_9) = \zeta_9^k$ 给出，其中 $k \in (\mathbb{Z}/9\mathbb{Z})^\times = \{1,2,4,5,7,8\}$。由于 $\zeta_9^k$ 均不是实数，所以 $K$ 是全虚域，$r_1=0, r_2=3$。
-   $K$ 中有一个重要的子域，即它的 **极大实子域 (maximal real subfield)** $K^+ = K \cap \mathbb{R}$。这个[子域](@entry_id:155812)由复[共轭作用](@entry_id:143328)所固定，可以证明 $K^+ = \mathbb{Q}(\zeta_9 + \bar{\zeta}_9) = \mathbb{Q}(\cos(2\pi/9))$。
-   $K^+$ 是一个全实域，且 $[K:K^+]=2$。
因此，$K=\mathbb{Q}(\zeta_9)$ 满足 CM 域的定义。对于 CM 域，[复共轭](@entry_id:174690)在每个嵌入中都表现为 $K/K^+$ 扩张的非平凡[自同构](@entry_id:155390) [@problem_id:3013303]。

### 应用：域的[范数与迹](@entry_id:637837)

嵌入的概念不仅是结构性的，它还为我们提供了计算数域中元素[不变量](@entry_id:148850)的强大工具。对于数域 $K$ 中的任意元素 $\alpha$，其 **范数 (norm)** 和 **迹 (trace)** 定义为它在所有 $n=[K:\mathbb{Q}]$ 个嵌入下的像的乘积和总和：
$$ N_{K/\mathbb{Q}}(\alpha) = \prod_{\sigma \in \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})} \sigma(\alpha) $$
$$ \operatorname{Tr}_{K/\mathbb{Q}}(\alpha) = \sum_{\sigma \in \operatorname{Hom}_{\mathbb{Q}}(K, \mathbb{C})} \sigma(\alpha) $$
尽管每个 $\sigma(\alpha)$ 可能是复数，但可以证明 $N_{K/\mathbb{Q}}(\alpha)$ 和 $\operatorname{Tr}_{K/\mathbb{Q}}(\alpha)$ 的值总是**有理数**。

**示例 1：[代数整数](@entry_id:151672)的范数**
让我们计算 $K = \mathbb{Q}(\alpha)$（其中 $\alpha=\sqrt[3]{2}$）中元素 $\beta = 1+\alpha+\alpha^2$ 的范数 [@problem_id:3013297]。$K$ 的三个嵌入是 $\sigma_1(\alpha)=\alpha$, $\sigma_2(\alpha)=\alpha\omega$, $\sigma_3(\alpha)=\alpha\omega^2$。
$$ N_{K/\mathbb{Q}}(\beta) = \sigma_1(\beta) \sigma_2(\beta) \sigma_3(\beta) $$
$$ = (1+\alpha+\alpha^2)(1+\alpha\omega+\alpha^2\omega^2)(1+\alpha\omega^2+\alpha^2\omega) $$
通过代数运算，可以发现后两个因子的乘积是 $\alpha-1$。因此，
$$ N_{K/\mathbb{Q}}(\beta) = (1+\alpha+\alpha^2)(\alpha-1) = \alpha^3 - 1 = 2-1 = 1 $$

**示例 2：[分圆域](@entry_id:153828)中的范数**
让我们计算 $K = \mathbb{Q}(\zeta_9)$ 中元素 $1-\zeta_9$ 的范数 [@problem_id:3013294]。$K$ 的 6 个嵌入是 $\sigma_k(\zeta_9) = \zeta_9^k$ for $k \in \{1,2,4,5,7,8\}$。
$$ N_{K/\mathbb{Q}}(1-\zeta_9) = \prod_{k \in \{1,2,4,5,7,8\}} \sigma_k(1-\zeta_9) = \prod_{k \in \{1,2,4,5,7,8\}} (1-\zeta_9^k) $$
这个乘积正是第 9 个[分圆多项式](@entry_id:155668) $\Phi_9(x)$ 在 $x=1$ 处的值。我们知道 $\Phi_9(x) = \frac{x^9-1}{x^3-1} = x^6+x^3+1$。因此，
$$ N_{K/\mathbb{Q}}(1-\zeta_9) = \Phi_9(1) = 1^6+1^3+1 = 3 $$
这个结果揭示了嵌入、范数与[分圆多项式](@entry_id:155668)之间深刻而优美的联系。