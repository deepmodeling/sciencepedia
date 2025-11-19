## 引言
在[代数数论](@entry_id:148067)的宏伟蓝图中，当我们从熟悉的有理[数域](@entry_id:155558) $\mathbb{Q}$ 迈向更广阔的[数域](@entry_id:155558) $K$ 时，一个根本性的问题随之浮现：什么是这些新世界中的“整数”？正如[整数环](@entry_id:181003) $\mathbb{Z}$ 是研究有理数算术的基石，寻找并理解其在数域中的对应物——[整数环](@entry_id:181003) $\mathcal{O}_K$——构成了代数数论的核心任务。这篇文章旨在系统地解答这一问题，不仅定义何为[代数整数](@entry_id:151672)，更要揭示如何具体地构造和运用它们。

本文将带领读者踏上一段从理论到实践的旅程。在第一章“原理与机制”中，我们将从“整性”的基本概念出发，严格定义整数环，并证明其作为一个自由 $\mathbb{Z}$-模的优美结构，引出[整基](@entry_id:190217)、[判别式](@entry_id:174614)与单源性的关键概念。第二章“应用与跨学科联系”将展示这些理论的威力，通过显式构造二次、三次及更高次域的整数环，并利用它们分析素理想的分歧行为，进而揭示其与伽罗瓦理论、[类域论](@entry_id:155687)及丢番图方程的深刻联系。最后，在第三章“动手实践”中，我们将通过一系列精心设计的问题，将抽象理论转化为可操作的计算技能。

通过这三章的学习，读者将不仅掌握整数环与[整基](@entry_id:190217)的基础理论，还将学会如何将其应用于解决具体的数论问题，为进一步探索[理想类群](@entry_id:153974)、单位群等更高等的[代数数论](@entry_id:148067)主题奠定坚实的基础。

## 原理与机制

在[代数数论](@entry_id:148067)的研究中，数域的[整数环](@entry_id:181003)扮演着核心角色，其地位类似于有理数域 $\mathbb{Q}$ 中的[整数环](@entry_id:181003) $\mathbb{Z}$。本章旨在深入探讨整数环的根本原理与结构机制。我们将从“整性”这一基本概念出发，建立整数环的定义，揭示其作为 $\mathbb{Z}$-模的深刻结构，并阐明判别式、指标与单源性等关键概念之间的联系。最后，我们将展望从局部信息构建整体[整基](@entry_id:190217)的现代计算方法。

### 整数环：定义与基本性质

#### 整元

我们首先从一个更广泛的代数概念——**整元 (integral element)** 开始。给定一个[交换环](@entry_id:148261) $A$ 及其扩环 $B$，如果元素 $\alpha \in B$ 是一个首一（monic）且系数在 $A$ 中的多项式 $f(x) \in A[x]$ 的根，即 $f(\alpha)=0$，我们就称 $\alpha$ 在 $A$ 上是整的。

这个定义对于理解[数域](@entry_id:155558)中的“整数”至关重要。让我们考虑最简单的情形：$A = \mathbb{Z}$ 和 $B = \mathbb{Q}$。哪些有理数在 $\mathbb{Z}$ 上是整的？一个有理数 $\alpha = p/q$（其中 $p, q \in \mathbb{Z}$，$q \neq 0$ 且 $\gcd(p, q) = 1$）若在 $\mathbb{Z}$ 上是整的，则它必须满足一个形如 $f(x) = x^n + c_{n-1}x^{n-1} + \dots + c_0 = 0$ 的方程，其中所有系数 $c_i$ 均为整数。将 $\alpha = p/q$ 代入并乘以 $q^n$ 可得：
$$
p^n + c_{n-1}p^{n-1}q + \dots + c_0q^n = 0
$$
整理后得到 $p^n = -q(c_{n-1}p^{n-1} + \dots + c_0q^{n-1})$。这表明 $q$ 整除 $p^n$。然而，我们已假设 $p$ 和 $q$ 互素，这意味着 $q$ 的任何素因子都不会出现在 $p$ 的素[因子分解](@entry_id:150389)中，因此也不会出现在 $p^n$ 中。这迫使 $q$ 只能是 $\pm 1$。于是，任何在 $\mathbb{Z}$ 上整的有理数都必须是整数。例如，$\alpha = 3/5$ 就不可能是整元，因为它不是整数 [@problem_id:1804515]。它虽然是多项式 $5x-3=0$ 的根，但该多项式不是首一的；它也是[首一多项式](@entry_id:152311) $x^2 - 9/25=0$ 的根，但该多项式的系数不全是整数。这个结论——即 $\mathbb{Q}$ 中在 $\mathbb{Z}$ 上整的元素恰好就是 $\mathbb{Z}$ 本身——是我们将要推广的一般理论的基石。

#### [整数环](@entry_id:181003) $\mathcal{O}_K$

现在，我们将视线投向更广阔的领域。一个**数域 (number field)** $K$ 被定义为有理数域 $\mathbb{Q}$ 的一个有限次域扩张，即 $K$ 作为 $\mathbb{Q}$ 上的[向量空间](@entry_id:151108)，其维数 $[K:\mathbb{Q}]$ 是有限的。

对于任意[数域](@entry_id:155558) $K$，其**[整数环](@entry_id:181003) (ring of integers)**，记作 $\mathcal{O}_K$，被定义为 $K$ 中所有在 $\mathbb{Z}$ 上整的元素的集合 [@problem_id:3022890]：
$$
\mathcal{O}_K = \{ \alpha \in K \mid \exists f(x) \in \mathbb{Z}[x], f(x) \text{ is monic and } f(\alpha) = 0 \}
$$
这个集合有时也被称为 $K$ 中的**[代数整数](@entry_id:151672) (algebraic integers)**。根据[交换代数](@entry_id:149047)中的标准术语，一个环 $A$ 在其扩环 $B$ 中的**[整闭](@entry_id:149392)包 (integral closure)** 是指 $B$ 中所有在 $A$ 上整的元素的集合。因此，$\mathcal{O}_K$ 按其定义正是 $\mathbb{Z}$ 在 $K$ 中的[整闭](@entry_id:149392)包。

#### $\mathcal{O}_K$ 的环结构

“[整数环](@entry_id:181003)”这一名称并非虚设，$\mathcal{O}_K$ 的确是 $K$ 的一个[子环](@entry_id:154194)。证明这一点需要一个关于整元的等价刻画：元素 $\alpha$ 在 $A$ 上整，当且仅当环 $A[\alpha]$（由 $A$ 和 $\alpha$ 生成的环）是 $A$ 上的一个[有限生成模](@entry_id:148410)。

基于此，若 $\alpha, \beta \in \mathcal{O}_K$，则 $\mathbb{Z}[\alpha]$ 是一个有限生成的 $\mathbb{Z}$-模。由于 $\beta$ 在 $\mathbb{Z}$ 上整，它必然也在更大的环 $\mathbb{Z}[\alpha]$ 上整。因此，环 $(\mathbb{Z}[\alpha])[\beta] = \mathbb{Z}[\alpha, \beta]$ 是一个有限生成的 $\mathbb{Z}[\alpha]$-模。模理论的一个标准结论是，如果 $M$ 是有限生成的 $B$-模，而 $B$ 是有限生成的 $A$-模，那么 $M$ 也是[有限生成](@entry_id:156447)的 $A$-模。应用此结论，可知 $\mathbb{Z}[\alpha, \beta]$ 是一个有限生成的 $\mathbb{Z}$-模。

由于 $\alpha+\beta$ 和 $\alpha\beta$ 均属于 $\mathbb{Z}[\alpha, \beta]$，它们所在的子环 $\mathbb{Z}[\alpha+\beta]$ 和 $\mathbb{Z}[\alpha\beta]$ 也是 $\mathbb{Z}[\alpha, \beta]$ 的子模。因为 $\mathbb{Z}$ 是一个[诺特环](@entry_id:153961)（Noetherian ring），[有限生成模](@entry_id:148410)的任何[子模](@entry_id:148922)也是[有限生成](@entry_id:156447)的。因此，$\mathbb{Z}[\alpha+\beta]$ 和 $\mathbb{Z}[\alpha\beta]$ 都是有限生成的 $\mathbb{Z}$-模，这意味着 $\alpha+\beta$ 和 $\alpha\beta$ 在 $\mathbb{Z}$ 上是整的，故它们属于 $\mathcal{O}_K$。这证明了 $\mathcal{O}_K$ 对加法和乘法封闭，因此它是一个环 [@problem_id:3022890]。

#### 通过极小多项式刻画

还有一个极其有用的判别方法。对于 $K$ 中的任意元素 $\alpha$，它在 $\mathbb{Q}$ 上都有一个唯一的首一不[可约多项式](@entry_id:148759)，称为**极小多项式 (minimal polynomial)**，记作 $m_{\alpha, \mathbb{Q}}(x)$。一个深刻的结论是：
**元素 $\alpha \in K$ 是[代数整数](@entry_id:151672)（即 $\alpha \in \mathcal{O}_K$），当且仅当其在 $\mathbb{Q}$ 上的极小多项式 $m_{\alpha, \mathbb{Q}}(x)$ 的系数全部为整数，即 $m_{\alpha, \mathbb{Q}}(x) \in \mathbb{Z}[x]$。**

这个结论的证明巧妙地运用了[高斯引理](@entry_id:149771) (Gauss's Lemma)。如果 $\alpha \in \mathcal{O}_K$，它满足某个首一整系数多项式 $f(x) \in \mathbb{Z}[x]$。由于 $m_{\alpha, \mathbb{Q}}(x)$ 是 $\alpha$ 在 $\mathbb{Q}[x]$ 中的极小多项式，它必然在 $\mathbb{Q}[x]$ 中整除 $f(x)$。[高斯引理](@entry_id:149771)的一个推论是，如果一个整系数多项式能被一个首一有理系数多项式整除，那么商多项式也必须是整系数的。这意味着 $m_{\alpha, \mathbb{Q}}(x)$ 本身必须拥有整数系数。反方向的证明是显然的，因为 $m_{\alpha, \mathbb{Q}}(x)$ 本身就是一个满足条件的、$\alpha$ 为根的首一整系数多项式 [@problem_id:3022890]。

### $\mathcal{O}_K$ 作为 $\mathbb{Z}$-模的结构

整数环 $\mathcal{O}_K$ 不仅是一个环，它还具有优美的模结构，这对于理解其算术性质至关重要。

#### 有限生成性与秩

[代数数论](@entry_id:148067)的一个基石性定理断言：**对于任意[数域](@entry_id:155558) $K$，其[整数环](@entry_id:181003) $\mathcal{O}_K$ 是一个[有限生成](@entry_id:156447)的 $\mathbb{Z}$-模。**

证明这一点的标准思路是，将 $\mathcal{O}_K$ “夹在”两个结构已知的 $\mathbb{Z}$-模之间 [@problem_id:3022904]。根据[本原元定理](@entry_id:156597) (Primitive Element Theorem)，任何[数域](@entry_id:155558) $K$ 都可以由单个元素生成，即 $K = \mathbb{Q}(\theta)$。我们可以选择一个[代数整数](@entry_id:151672) $\theta \in \mathcal{O}_K$ 作为生成元。那么，集合 $\{1, \theta, \dots, \theta^{n-1}\}$ （其中 $n=[K:\mathbb{Q}]$）构成了 $K$ 的一组 $\mathbb{Q}$-基。

考虑由 $\theta$ 生成的子环 $\mathbb{Z}[\theta]$，它显然是 $\mathcal{O}_K$ 的一个[子集](@entry_id:261956)，并且是一个秩为 $n$ 的自由 $\mathbb{Z}$-模。通过运用[迹映射](@entry_id:194370) $\text{Tr}_{K/\mathbb{Q}}$ 和判别式理论，可以证明存在一个非零整数 $D$（实际上可以是 $\theta$ 的极小[多项式的判别式](@entry_id:148721)），使得 $D \cdot \mathcal{O}_K \subseteq \mathbb{Z}[\theta]$。

这样，我们就得到了一个包含关系：
$$
\mathbb{Z}[\theta] \subseteq \mathcal{O}_K \subseteq \frac{1}{D}\mathbb{Z}[\theta]
$$
$\mathbb{Z}[\theta]$ 是一个秩为 $n$ 的自由 $\mathbb{Z}$-模，而 $\frac{1}{D}\mathbb{Z}[\theta]$ 同样如此。由于 $\mathcal{O}_K$ 被夹在两个[有限生成](@entry_id:156447)的 $\mathbb{Z}$-模之间，且 $\mathbb{Z}$ 是[主理想整环](@entry_id:152359)，我们可以断定 $\mathcal{O}_K$ 本身也是一个有限生成的 $\mathbb{Z}$-模。

进一步，$\mathcal{O}_K$ 包含 $n$ 个在 $\mathbb{Q}$ 上[线性无关](@entry_id:148207)的元素（例如 $\mathbb{Z}[\theta]$ 的基），所以其秩至少为 $n$。同时，$\mathcal{O}_K$ 是 $n$ 维 $\mathbb{Q}$-[向量空间](@entry_id:151108) $K$ 的一个[子集](@entry_id:261956)，所以其秩至多为 $n$。综合可知，**$\mathcal{O}_K$ 作为 $\mathbb{Z}$-模的秩恰好等于数域的次数 $n=[K:\mathbb{Q}]$** [@problem_id:3022904]。值得注意的是，这个秩 $n = r_1 + 2r_2$（其中 $r_1$ 是实嵌入的数目，$r_2$ 是共轭[复嵌入](@entry_id:189961)的对数），不要与[狄利克雷单位定理](@entry_id:155550)中的单位秩 $r_1+r_2-1$ 相混淆。

#### [整基](@entry_id:190217)

一个[有限生成](@entry_id:156447)且[无挠的](@entry_id:161664) $\mathbb{Z}$-模必然是一个自由 $\mathbb{Z}$-模。由于 $\mathcal{O}_K$ 的[加法群](@entry_id:151801)没有[挠元](@entry_id:148301)（任何非零元的整数倍都不会是零），我们得出结论：**$\mathcal{O}_K$ 是一个秩为 $n=[K:\mathbb{Q}]$ 的自由 $\mathbb{Z}$-模。**

这意味着存在一组基 $\omega_1, \dots, \omega_n \in \mathcal{O}_K$，使得 $\mathcal{O}_K$ 中的每一个元素 $\alpha$ 都可以唯一地表示为这些基元的整线性组合：
$$
\alpha = c_1 \omega_1 + c_2 \omega_2 + \dots + c_n \omega_n, \quad c_i \in \mathbb{Z}
$$
这样的一组基 $\{\omega_1, \dots, \omega_n\}$ 被称为 $K$ 的一个**[整基](@entry_id:190217) (integral basis)**。[整基](@entry_id:190217)的存在是代数数论中进行具体计算的基石。

### 判别式、指标与单源性

有了[整基](@entry_id:190217)的概念，我们便可以引入判别式和指标，这两个工具深刻地揭示了[整数环](@entry_id:181003)的内部结构。

#### [判别式](@entry_id:174614)

对于数域 $K$ 中的任意 $n$ 个元素 $\beta_1, \dots, \beta_n$，我们可以定义它们的**[判别式](@entry_id:174614) (discriminant)** 为：
$$
\text{disc}(\beta_1, \dots, \beta_n) = \det\left( (\text{Tr}_{K/\mathbb{Q}}(\beta_i \beta_j))_{i,j=1}^n \right)
$$
其中 $\text{Tr}_{K/\mathbb{Q}}$ 是从 $K$ 到 $\mathbb{Q}$ 的[迹映射](@entry_id:194370)。一个重要的性质是，这 $n$ 个元素构成 $K$ 的一组 $\mathbb{Q}$-基当且仅当它们的[判别式](@entry_id:174614)非零。

如果取一组[整基](@entry_id:190217) $\{\omega_1, \dots, \omega_n\}$，其判别式 $\text{disc}(\omega_1, \dots, \omega_n)$ 是一个不依赖于具体[整基](@entry_id:190217)选择的整数（只可能相差一个平方因子 $(\pm 1)^2=1$）。这个[不变量](@entry_id:148850)被称为**[数域](@entry_id:155558) $K$ 的[判别式](@entry_id:174614)**，记为 $\text{disc}(K)$ 或 $d_K$ [@problem_id:3023000]。

#### 序与指标

在[整数环](@entry_id:181003) $\mathcal{O}_K$ 中，任何一个既是子环又是满秩自由 $\mathbb{Z}$-模的[子集](@entry_id:261956)，被称为一个**序 (order)**。对于任意一个能生成整个[数域](@entry_id:155558) $K = \mathbb{Q}(\alpha)$ 的[代数整数](@entry_id:151672) $\alpha$，由它生成的多项式环 $\mathbb{Z}[\alpha]$ 就是一个序。

由于 $\mathbb{Z}[\alpha] \subseteq \mathcal{O}_K$ 且二者都是秩为 $n$ 的自由 $\mathbb{Z}$-模，商群 $\mathcal{O}_K / \mathbb{Z}[\alpha]$ 是一个[有限阿贝尔群](@entry_id:136632)。这个群的大小被称为序 $\mathbb{Z}[\alpha]$ 在 $\mathcal{O}_K$ 中的**指标 (index)**，记作 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ [@problem_id:3022885]。

#### [指标-判别式公式](@entry_id:201303)

指标与判别式之间存在一个至关重要的关系。对于生成元 $\alpha \in \mathcal{O}_K$，其幂基 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 的[判别式](@entry_id:174614)与[域判别式](@entry_id:198568)通过指标联系起来：
$$
\text{disc}(1, \alpha, \dots, \alpha^{n-1}) = [\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 \cdot \text{disc}(K)
$$
这个公式非常强大 [@problem_id:3023000] [@problem_id:3022885]。左边的判别式，$\text{disc}(1, \alpha, \dots, \alpha^{n-1})$，可以被证明恰好等于 $\alpha$ 的极小多项式 $m_{\alpha, \mathbb{Q}}(x)$ 的判别式 $\text{disc}(m_{\alpha, \mathbb{Q}})$。[多项式的判别式](@entry_id:148721)可以直接通过其系数计算，因此这是一个相对容易获得的值。

#### 单源域与[幂整基](@entry_id:181090)

从[指标-判别式公式](@entry_id:201303)可以看出，$\text{disc}(m_{\alpha, \mathbb{Q}}) = \text{disc}(K)$ 当且仅当 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 = 1$，即指标为 $1$。指标为 $1$ 意味着 $\mathcal{O}_K = \mathbb{Z}[\alpha]$ [@problem_id:3017535]。

如果存在这样一个 $\alpha \in \mathcal{O}_K$ 使得 $\mathcal{O}_K = \mathbb{Z}[\alpha]$，我们就称[数域](@entry_id:155558) $K$ 是**单源的 (monogenic)**，并且 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 构成一个**[幂整基](@entry_id:181090) (power integral basis)** [@problem_id:3022885]。

一个直接的应用是，如果 $\alpha$ 的极小[多项式的判别式](@entry_id:148721) $\text{disc}(m_{\alpha, \mathbb{Q}})$ 是一个**无平方因子整数 (square-free integer)**，那么从公式中我们可以立即推断出 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]^2$ 必须等于 $1$，从而指标为 $1$。例如，考虑由 $f(x) = x^3 - x - 1$ 的根 $\alpha$ 生成的数域 $K = \mathbb{Q}(\alpha)$。该[多项式的判别式](@entry_id:148721)是 $-23$，这是一个无平方因子的素数。因此，我们必定有 $[\mathcal{O}_K : \mathbb{Z}[\alpha]] = 1$，即 $\mathcal{O}_K = \mathbb{Z}[\alpha]$ [@problem_id:3022901]。

另一个重要的例子是[分圆域](@entry_id:153828)。对于任意 $m$，分圆域 $K = \mathbb{Q}(\zeta_m)$（其中 $\zeta_m$ 是本原 $m$ 次单位根）都是单源的，其[整数环](@entry_id:181003)恰好是 $\mathcal{O}_K = \mathbb{Z}[\zeta_m]$ [@problem_id:3023000]。

#### 非单源域与[指标形式](@entry_id:183467)

然而，并非所有数域都是单源的 [@problem_id:3023000]。第一个反例由 Richard Dedekind 发现。一个更常见的情形是，一个序 $\mathbb{Z}[\alpha]$ 并不等于 $\mathcal{O}_K$。例如，对于 $K = \mathbb{Q}(\sqrt{5})$，我们知道其整数环是 $\mathcal{O}_K = \mathbb{Z}[\frac{1+\sqrt{5}}{2}]$，[域判别式](@entry_id:198568)为 $d_K = 5$。如果我们取 $\alpha = \sqrt{5}$，它的极小多项式是 $x^2-5$，[判别式](@entry_id:174614)为 $20$。根据公式，$20 = [\mathcal{O}_K : \mathbb{Z}[\sqrt{5}]]^2 \cdot 5$，解得指标为 $2$。这表明 $\mathbb{Z}[\sqrt{5}]$ 只是 $\mathcal{O}_K$ 的一个子环，而非其本身 [@problem_id:3017535]。

为了系统地研究一个域是否单源，可以引入**[指标形式](@entry_id:183467) (index form)**。固定一组[整基](@entry_id:190217) $\{\omega_1, \dots, \omega_n\}$，对于任意[代数整数](@entry_id:151672) $\alpha = \sum_{i=1}^n x_i \omega_i$（其中 $x_i \in \mathbb{Z}$），其指标 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 的值可以表示为一个关于系数 $x_1, \dots, x_n$ 的整系数[齐次多项式](@entry_id:178156) $I(x_1, \dots, x_n)$ 的[绝对值](@entry_id:147688)，即 $[\mathcal{O}_K : \mathbb{Z}[\alpha]] = |I(x_1, \dots, x_n)|$ [@problem_id:3022885]。这个多项式的次数为 $\binom{n}{2}$。

因此，一个[数域](@entry_id:155558) $K$ 是单源的，当且仅当[丢番图方程](@entry_id:148433) $|I(x_1, \dots, x_n)| = 1$ 存在整数解 $(x_1, \dots, x_n) \in \mathbb{Z}^n$ [@problem_id:3022885]。

### 计算[整基](@entry_id:190217)的机制：从局部到整体

尽管我们证明了[整基](@entry_id:190217)的存在性，但在实践中如何计算它是一个重要且非平凡的问题。现代方法通常采用一种“从局部到整体”的策略。

#### $\mathcal{O}_K$ 的局部结构

[代数数论](@entry_id:148067)的一个核心思想是通过“局部化”来简化问题。对于一个给定的有理素数 $p$，我们可以通过[张量积](@entry_id:140694)来研究 $\mathcal{O}_K$ 在 $p$ 处的结构，即考虑环 $\mathcal{O}_K \otimes_{\mathbb{Z}} \mathbb{Z}_p$，其中 $\mathbb{Z}_p$ 是 $p$-adic [整数环](@entry_id:181003)。

这个[环的结构](@entry_id:150907)与素数 $p$ 在 $\mathcal{O}_K$ 中的分解行为密切相关。设 $p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \cdots \mathfrak{p}_g^{e_g}$ 是 $p$ 在 $\mathcal{O}_K$ 中的[素理想分解](@entry_id:197179)。一个基本定理指出，存在一个典范的[环同构](@entry_id:147982) [@problem_id:3022879]：
$$
\mathcal{O}_K \otimes_{\mathbb{Z}} \mathbb{Z}_p \cong \prod_{i=1}^{g} \mathcal{O}_{K_{\mathfrak{p}_i}}
$$
其中 $\mathcal{O}_{K_{\mathfrak{p}_i}}$ 是 $K$ 在 $\mathfrak{p}_i$-adic 范数下的完备化所得到的[局部域](@entry_id:195717) $K_{\mathfrak{p}_i}$ 的整数环。此外，$\mathcal{O}_K \otimes_{\mathbb{Z}} \mathbb{Z}_p$ 是一个秩为 $n=[K:\mathbb{Q}]$ 的自由 $\mathbb{Z}_p$-模 [@problem_id:3022879]。例如，当 $p$ 在 $K$ 中完全分裂时（即 $g=n, e_i=f_i=1$），这个同构就简化为 $\mathcal{O}_K \otimes_{\mathbb{Z}} \mathbb{Z}_p \cong \mathbb{Z}_p^n$ [@problem_id:3022879]。

#### 识别“问题素数”

从计算的角度看，局部化思想的巨大威力在于，它将一个全局[问题分解](@entry_id:272624)为在每个素数处的局部问题。给定一个[本原元](@entry_id:154321) $\theta \in \mathcal{O}_K$ 及相应的序 $\mathbb{Z}[\theta]$，我们想知道在哪些素数 $p$ 处，这个序“不够好”，即 $\mathbb{Z}[\theta]$ 在 $p$ 处的局部化 $\mathbb{Z}[\theta] \otimes_{\mathbb{Z}} \mathbb{Z}_p$ 不等于 $\mathcal{O}_K \otimes_{\mathbb{Z}} \mathbb{Z}_p$。

[指标-判别式公式](@entry_id:201303) $ \text{disc}(\mathbb{Z}[\theta]) = [\mathcal{O}_K : \mathbb{Z}[\theta]]^2 \cdot \text{disc}(K)$ 提供了答案。这个公式表明，任何整除指标 $[\mathcal{O}_K : \mathbb{Z}[\theta]]$ 的素数 $p$，也必须整除[多项式判别式](@entry_id:154854) $\text{disc}(\mathbb{Z}[\theta])$。这意味着，我们只需要关注那些整除 $\text{disc}(m_{\theta, \mathbb{Q}})$ 的**有限个素数**。对于所有不整除该[判别式](@entry_id:174614)的素数 $p$，序 $\mathbb{Z}[\theta]$ 已经是“$p$-极大”的，其幂基 $\{1, \theta, \dots, \theta^{n-1}\}$ 已经构成了 $\mathcal{O}_K$ 在 $p$ 处的局部[整基](@entry_id:190217) [@problem_id:3022905]。

#### 计算的[局部-整体原则](@entry_id:183320)

这引导我们得出计算全局[整基](@entry_id:190217)的总体策略 [@problem_id:3022905]：
1.  从一个方便的序 $\mathbb{Z}[\theta]$ 开始，计算其[判别式](@entry_id:174614) $\Delta = \text{disc}(m_{\theta, \mathbb{Q}})$。
2.  对于每一个整除 $\Delta$ 的“问题素数”$p$，运用特定算法（如 Round-2, Round-4, 或 Montes 算法）计算出 $\mathcal{O}_K$ 在 $p$ 处的局部[整基](@entry_id:190217)的一个修正。这个修正通常表现为对原有基 $\{1, \theta, \dots, \theta^{n-1}\}$ 的某些线性组合除以 $p$ 的幂次。这相当于找到一组元素，它们满足在 $p$ 处的整性条件。
3.  一个元素 $\alpha \in K$ 属于全局整数环 $\mathcal{O}_K$，当且仅当它在所有素数 $p$ 处都是局部整的。由于我们只在有限个素数处有非平凡的整性条件，我们可以利用**[中国剩余定理](@entry_id:144030) (Chinese Remainder Theorem)** 将这些在不同素数下的局部整性条件（表现为对系数的[同余](@entry_id:143700)要求）“拼接”起来，从而构造出满足所有条件的全局元素。
4.  通过系统地应用此方法，我们可以对初始基 $\mathbb{Z}[\theta]$进行逐步“放大”，直到它在所有问题素数处都达到极大，最终得到 $\mathcal{O}_K$ 的一组全局[整基](@entry_id:190217)。

#### 高等算法展望：Montes算法

在上述框架中，步骤2——计算局部[整基](@entry_id:190217)和相关算术[不变量](@entry_id:148850)——是技术核心。**Montes算法**是解决这一问题的现代强力工具 [@problem_id:3022889]。该算法可以被看作是[亨泽尔引理](@entry_id:137105) (Hensel's Lemma) 的一种深刻推广，它通过构造一系列更高阶的[牛顿多边形](@entry_id:182301) (Newton polygons) 和剩余多项式，来彻底分析给定的多项式 $f(x)$ 在 $p$-adic 意义下的分解。

算法的输出，即所谓的“类型”(types)，不仅给出了 $p\mathcal{O}_K$ 的完整[素理想分解](@entry_id:197179)（包括每个[素理想](@entry_id:154026)的[分歧指数](@entry_id:186386) $e_i$ 和剩余次数 $f_i$），还直接给出了 $p$-指标 $\nu_p([\mathcal{O}_K : \mathbb{Z}[\theta]])$ 的值，并提供了一个明确的配方来构造一个局部的 $p$-[整基](@entry_id:190217)。当应用于经典 Dedekind 判别法的情形，即 $f(x) \pmod p$ 无平方因子时，Montes 算法会在第一步就终止，确认 $p$-指标为零，幂基已经是 $p$-[整基](@entry_id:190217)，从而与经典理论完美衔接 [@problem_id:3022889]。这一算法体现了代数数论从理论构造到高效计算的深刻转变。