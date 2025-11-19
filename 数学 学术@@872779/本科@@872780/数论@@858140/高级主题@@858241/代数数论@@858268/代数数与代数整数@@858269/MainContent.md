## 引言
在整数的世界里，[算术基本定理](@entry_id:146420)——即每个整数都能唯一分解为素数的乘积——是我们理解数系结构的基石。然而，当我们试图将这一优美的性质推广到更广阔的数系中时，会遇到一个根本性的挑战：唯一因子分解并不总是成立。本文旨在系统地介绍[代数数论](@entry_id:148067)的核心工具——[代数数](@entry_id:150888)与[代数整数](@entry_id:151672)，正是为了应对这一挑战并建立一套更普适的算术理论。

通过本文的学习，你将深入理解这些概念如何将我们熟悉的整数进行推广，并揭示其背后深刻的[代数结构](@entry_id:137052)。我们将首先在“原理与机制”一章中，从基本定义出发，建立[代数数](@entry_id:150888)、[代数整数](@entry_id:151672)、整数环以及[理想分解](@entry_id:148948)的理论框架，并引入理想类群来精确衡量[唯一分解](@entry_id:152313)的“失效程度”。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何应用于解决[佩尔方程](@entry_id:136532)等具体问题，并探索其与几何作图、[抽象代数](@entry_id:145216)等领域的惊人联系。最后，“动手实践”部分将通过一系列精心设计的问题，帮助你巩固所学知识，将理论付诸实践。

## 原理与机制

在本章中，我们将深入探讨代数数论的核心概念：[代数数](@entry_id:150888)与[代数整数](@entry_id:151672)。这些概念将我们熟悉的整数和有理数推广到一个更广阔的[代数结构](@entry_id:137052)中。我们将从基本定义出发，系统地建立它们的性质，并最终揭示这些新对象如何拥有自己独特的算术规律，即使经典的唯一因子分解可能失效。

### [代数数](@entry_id:150888)：连接代数与数的桥梁

我们从一个基本问题开始：哪些数可以被视为“代数的”？直观上，这些数应该能通过[代数方程](@entry_id:272665)与有理数联系起来。这引出了我们的第一个正式定义。

一个复数 $\alpha \in \mathbb{C}$ 被称为**[代数数](@entry_id:150888)**（algebraic number），如果它是某个非零有理系数多项式 $f(x) \in \mathbb{Q}[x]$ 的根。也就是说，存在不全为零的有理数 $r_0, r_1, \dots, r_n$ 使得：
$$
r_n \alpha^n + r_{n-1} \alpha^{n-1} + \dots + r_1 \alpha + r_0 = 0
$$

例如，$\sqrt[3]{2}$ 是一个代数数，因为它是多项式 $x^3 - 2 = 0$ 的根。类似地，三次[单位根](@entry_id:143302) $\zeta_3 = \exp(2\pi i/3)$ 也是代数数，因为它满足 $x^3 - 1 = 0$。由于 $\zeta_3 \neq 1$，它必然是 $x^3-1=(x-1)(x^2+x+1)$ 的另一个因子 $x^2+x+1=0$ 的根。[代数数](@entry_id:150888)的和与积也是代数数，例如 $\sqrt{2}+\sqrt{3}$ 也是一个代数数，因为它满足 $x^4 - 10x^2 + 1 = 0$。事实上，所有[代数数](@entry_id:150888)的集合构成一个域，通常记为 $\overline{\mathbb{Q}}$。[@problem_id:3080537]

不满足任何有理系数多项式的复数被称为**[超越数](@entry_id:154911)**（transcendental number）。著名的例子包括圆周率 $\pi$ 和自然对数的底 $e$。它们的超越性是数论中深刻的结果。第一个被证明是[超越数](@entry_id:154911)的数是刘维尔常数 $L = \sum_{k=1}^{\infty} 10^{-k!}$，这一证明依赖于刘维尔定理，该定理刻画了[代数数](@entry_id:150888)被有理数逼近的“速度”有多快。[@problem_id:3080537]

在处理代数数时，使用有理系数多项式和整系数多项式在很多情况下是等价的。如果一个数 $\alpha$ 是有理系数多项式 $f(x) = \sum_{i=0}^n \frac{a_i}{b_i} x^i$ 的根，其中 $a_i, b_i \in \mathbb{Z}$，我们可以通过乘以所有分母 $b_i$ 的最小公倍数 $D = \mathrm{lcm}(b_0, \dots, b_n)$ 来“清除分母”。这样就得到了一个新的非零多项式 $g(x) = D \cdot f(x)$，它的系数都是整数，并且 $g(\alpha) = D \cdot f(\alpha) = 0$。因此，一个数是[代数数](@entry_id:150888)的定义可以等价地表述为：它是某个非零整系数多项式的根。[@problem_id:3080519]

### [代数整数](@entry_id:151672)：一个特殊的类别

在[代数数](@entry_id:150888)的海洋中，有一类特殊的数表现出与我们熟悉的整数 $\mathbb{Z}$ 更为相似的性质。这就是[代数整数](@entry_id:151672)。

一个复数 $\alpha \in \mathbb{C}$ 被称为**[代数整数](@entry_id:151672)**（algebraic integer），如果它是某个首一（monic）整系数多项式 $f(x) \in \mathbb{Z}[x]$ 的根。[首一多项式](@entry_id:152311)是指其最高次项系数为 $1$ 的多项式。[@problem_id:3080541]
$$
\alpha^n + c_{n-1} \alpha^{n-1} + \dots + c_1 \alpha + c_0 = 0, \quad c_i \in \mathbb{Z}
$$

这个定义非常关键。所有普通的整数 $n \in \mathbb{Z}$ 都是[代数整数](@entry_id:151672)，因为每个整数 $n$ 都是[首一多项式](@entry_id:152311) $x - n = 0$ 的根。[@problem_id:3080541]

然而，并非所有代数数都是[代数整数](@entry_id:151672)。考虑有理数 $\alpha = \frac{1}{2}$。它是 $2x-1=0$ 的根，所以它是一个[代数数](@entry_id:150888)。但它是不是一个[代数整数](@entry_id:151672)呢？为了回答这个问题，我们建立一个至关重要的判据：

**一个有理数是[代数整数](@entry_id:151672)，当且仅当它是一个整数。**

**证明**: 一方面，我们已经知道每个整数都是[代数整数](@entry_id:151672)。另一方面，假设一个有理数 $r = \frac{a}{b}$ 是一个[代数整数](@entry_id:151672)，其中 $a,b \in \mathbb{Z}$，$b>0$ 且 $\gcd(a,b)=1$（即分数已化至最简）。根据定义，存在整数 $c_0, \dots, c_{n-1}$ 使得：
$$
\left(\frac{a}{b}\right)^n + c_{n-1}\left(\frac{a}{b}\right)^{n-1} + \dots + c_1\left(\frac{a}{b}\right) + c_0 = 0
$$
将等式两边同乘以 $b^n$：
$$
a^n + c_{n-1}a^{n-1}b + \dots + c_1ab^{n-1} + c_0b^n = 0
$$
移项可得：
$$
a^n = -b(c_{n-1}a^{n-1} + \dots + c_1ab^{n-1} + c_0b^{n-1})
$$
这表明 $b$ 整除 $a^n$。但我们假设 $\gcd(a,b)=1$，这意味着 $a$ 和 $b$ 没有共同的素因子。因此，$b$ 也不可能与 $a^n$ 有共同的素因子，除非 $b=1$。如果 $b=1$，那么 $r=a$ 就是一个整数。这就完成了证明。[@problem_id:1805222]

这个结论为我们提供了一个清晰的界限。像 $\frac{1}{2}$ 这样的非整数有理数是[代数数](@entry_id:150888)，但不是[代数整数](@entry_id:151672)。[代数整数](@entry_id:151672)的集合是代数数集合的一个[真子集](@entry_id:152276)。[@problem_id:3080541]

### 数域的整数环

现在我们将注意力集中在一个固定的代[数环](@entry_id:636822)境中。一个**数域**（number field）$K$ 是有理数域 $\mathbb{Q}$ 的一个有限次扩张，即 $K$ 是一个包含 $\mathbb{Q}$ 的域，并且可以看作是 $\mathbb{Q}$ 上的一个[有限维向量空间](@entry_id:265491)。

对于一个[数域](@entry_id:155558) $K$，我们定义其**[整数环](@entry_id:181003)**（ring of integers） $\mathcal{O}_K$ 为 $K$ 中所有[代数整数](@entry_id:151672)的集合。形式上：
$$
\mathcal{O}_K = \{\alpha \in K \mid \alpha \text{ 是代数整数}\}
$$
这是一个极其重要的结论：$\mathcal{O}_K$ 确实构成一个环。也就是说，两个[代数整数](@entry_id:151672)的和与积仍然是[代数整数](@entry_id:151672)。这个结论的证明较为深入，但它确保了我们可以像研究 $\mathbb{Z}$ 一样研究 $\mathcal{O}_K$ 的算术性质。从更抽象的角度看，$\mathcal{O}_K$ 是 $\mathbb{Z}$ 在 $K$ 中的**[整闭](@entry_id:149392)包**（integral closure）。此外，$\mathcal{O}_K$ 本身也是[整闭](@entry_id:149392)的，即任何在 $K$ 中且整于 $\mathcal{O}_K$ 的元素都已经属于 $\mathcal{O}_K$。[@problem_id:3007367]

为了具体地操作和识别[代数整数](@entry_id:151672)，**域范数**（field norm）和**域迹**（field trace）是两个强大的工具。对于 $K$ 中的任意元素 $\alpha$，我们可以将其视为一个 $\mathbb{Q}$-[线性映射](@entry_id:185132) $m_\alpha: K \to K$，定义为 $m_\alpha(x) = \alpha x$。
- **范数** $N_{K/\mathbb{Q}}(\alpha)$ 定义为该线性映射的[行列式](@entry_id:142978) $\det(m_\alpha)$。
- **迹** $T_{K/\mathbb{Q}}(\alpha)$ 定义为该线性映射的迹 $\mathrm{Tr}(m_\alpha)$。

这些定义与 $K$ 到[复数域](@entry_id:153768) $\mathbb{C}$ 的所有 $n=[K:\mathbb{Q}]$ 个嵌入（embeddings）$\sigma_j$ 有着深刻的联系：
$$
N_{K/\mathbb{Q}}(\alpha) = \prod_{j=1}^n \sigma_j(\alpha)
$$
$$
T_{K/\mathbb{Q}}(\alpha) = \sum_{j=1}^n \sigma_j(\alpha)
$$
如果 $\alpha$ 是一个[代数整数](@entry_id:151672)，那么它的范数 $N_{K/\mathbb{Q}}(\alpha)$ 和迹 $T_{K/\mathbb{Q}}(\alpha)$ 都是整数。这个性质为我们判断一个元素是否为[代数整数](@entry_id:151672)提供了必要条件。[@problem_id:3080540]

让我们看一个重要的例子：二次域 $K = \mathbb{Q}(\sqrt{d})$，其中 $d$ 是一个无平方因子的整数。$K$ 中的任意元素都可以写成 $\alpha = x + y\sqrt{d}$ 的形式，其中 $x, y \in \mathbb{Q}$。它的[迹和范数](@entry_id:155207)分别为 $T_{K/\mathbb{Q}}(\alpha) = 2x$ 和 $N_{K/\mathbb{Q}}(\alpha) = x^2 - dy^2$。如果 $\alpha$ 是[代数整数](@entry_id:151672)，那么 $2x$ 和 $x^2 - dy^2$ 必须是整数。通过对这两个条件进行细致分析，可以得出 $\mathcal{O}_K$ 的完整结构，它取决于 $d$ 模 $4$ 的余数：
- 如果 $d \equiv 2$ 或 $d \equiv 3 \pmod 4$，那么整数环就是 $\mathcal{O}_K = \mathbb{Z}[\sqrt{d}] = \{m + n\sqrt{d} \mid m,n \in \mathbb{Z}\}$。例如，在 $\mathbb{Q}(\sqrt{2})$ 中，[整数环](@entry_id:181003)是 $\mathbb{Z}[\sqrt{2}]$。
- 如果 $d \equiv 1 \pmod 4$，情况则有所不同。整数环是 $\mathcal{O}_K = \mathbb{Z}\left[\frac{1+\sqrt{d}}{2}\right] = \{m + n\frac{1+\sqrt{d}}{2} \mid m,n \in \mathbb{Z}\}$。例如，在 $\mathbb{Q}(\sqrt{5})$ 中，元素 $\frac{1+\sqrt{5}}{2}$（[黄金比例](@entry_id:139097)）是一个[代数整数](@entry_id:151672)（它是 $x^2-x-1=0$ 的根），其整数环为 $\mathbb{Z}[\frac{1+\sqrt{5}}{2}]$。同理，在 $\mathbb{Q}(\sqrt{-3})$ 中（$d=-3 \equiv 1 \pmod 4$），整数环是 $\mathbb{Z}[\frac{1+\sqrt{-3}}{2}]$。[@problem_id:3080556]

### [整数环](@entry_id:181003)中的分解

我们研究 $\mathcal{O}_K$ 的主要动机之一是推广 $\mathbb{Z}$ 中的算术基本定理（唯一[因子分解](@entry_id:150389)）。然而，在一般的整数环 $\mathcal{O}_K$ 中，元素的唯一[因子分解](@entry_id:150389)性质可能不再成立。例如，在 $\mathcal{O}_{\mathbb{Q}(\sqrt{-5})} = \mathbb{Z}[\sqrt{-5}]$ 中，我们有 $6 = 2 \cdot 3 = (1+\sqrt{-5})(1-\sqrt{-5})$。这里的 $2, 3, 1+\sqrt{-5}, 1-\sqrt{-5}$ 都是不可约元素，这表明 $6$ 有两种本质上不同的分解方式。

尽管元[素分解](@entry_id:198620)失败了，但数学家们发现了一个替代的、同样强大的[唯一分解](@entry_id:152313)理论，即**理想的唯一[因子分解](@entry_id:150389)**。在任何数域的整数环 $\mathcal{O}_K$（它是一个**戴德金[整环](@entry_id:155321)**）中，任何非零理想都可以唯一地分解为[素理想](@entry_id:154026)的乘积。[@problem_id:3007356]

这个理论的核心是研究有理素数 $p \in \mathbb{Z}$ 在 $\mathcal{O}_K$ 中如何分解。当我们把 $p$ 看作 $\mathcal{O}_K$ 中的一个理想 $(p) = p\mathcal{O}_K$ 时，它可以分解为 $\mathcal{O}_K$ 中一系列素理想 $\mathfrak{p}_i$ 的幂次乘积：
$$
p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_g^{e_g}
$$
这里的 $e_i$ 被称为**[分歧指数](@entry_id:186386)**（ramification index），它度量了[素理想](@entry_id:154026) $\mathfrak{p}_i$ 在分解中的“[重数](@entry_id:136466)”。$f_i$ 被称为**惯性指数**（inertia degree），定义为商环的域扩张次数 $f_i = [\mathcal{O}_K/\mathfrak{p}_i : \mathbb{Z}/p\mathbb{Z}]$。它描述了每个素[理想因子](@entry_id:137944)“大小”的度量，因为 $\mathcal{O}_K/\mathfrak{p}_i$ 是一个包含 $p^{f_i}$ 个元素的[有限域](@entry_id:142106)。[@problem_id:3007355]

这些指数之间存在一个基本的、优美的关系式，它将分解行为与数域的次数 $n=[K:\mathbb{Q}]$联系在一起：
$$
\sum_{i=1}^g e_i f_i = n
$$
这个恒等式可以通过计算[商环](@entry_id:148632) $\mathcal{O}_K/p\mathcal{O}_K$ 作为 $\mathbb{F}_p=\mathbb{Z}/p\mathbb{Z}$ 上[向量空间](@entry_id:151108)的维数来证明。一方面，由于 $\mathcal{O}_K \cong \mathbb{Z}^n$，我们有 $\dim_{\mathbb{F}_p}(\mathcal{O}_K/p\mathcal{O}_K) = n$。另一方面，通过[中国剩余定理](@entry_id:144030)，$\mathcal{O}_K/p\mathcal{O}_K \cong \bigoplus_i \mathcal{O}_K/\mathfrak{p}_i^{e_i}$，而每一部分的维数是 $e_i f_i$。[@problem_id:3080558] 如果 $K/\mathbb{Q}$ 是一个伽罗瓦扩张，情况会变得更简单：所有的 $e_i$ 都相等（记为 $e$），所有的 $f_i$ 也都相等（记为 $f$），此时关系式简化为 $efg=n$。[@problem_id:3007355]

### 衡量唯一因子分解失败的尺度：[类群](@entry_id:182524)

既然[理想的唯一分解](@entry_id:154997)总是成立，那么是什么决定了元素的唯一分解是否成立呢？答案在于主理想（由单个元素生成的理想）与其他理想之间的关系。

为了量化这种关系，我们引入**[理想类群](@entry_id:153974)**（ideal class group）的概念。首先，我们将理想的概念推广到**分式理想**（fractional ideal），它们是 $K$ 的 $\mathcal{O}_K$-子模。所有非零分式理想的集合在理想乘法下构成一个[交换群](@entry_id:145145)，记为 $\mathcal{I}_K$。其中，由单个元素 $x \in K^\times$ 生成的主分式理想 $x\mathcal{O}_K$ 构成一个[子群](@entry_id:146164) $\mathcal{P}_K$。[@problem_id:3007356]

**[理想类群](@entry_id:153974)** $\mathrm{Cl}_K$ 定义为[商群](@entry_id:145113)：
$$
\mathrm{Cl}_K = \mathcal{I}_K / \mathcal{P}_K
$$
两个理想 $\mathfrak{a}$ 和 $\mathfrak{b}$ 属于同一个理想类，当且仅当存在一个元素 $x \in K^\times$ 使得 $\mathfrak{a} = x\mathfrak{b}$。[理想类群](@entry_id:153974)的阶，记为 $h_K = |\mathrm{Cl}_K|$，被称为**[类数](@entry_id:156164)**（class number）。数论中的一个深刻结果表明，任何[数域](@entry_id:155558)的类数都是有限的。[@problem_id:3080549] [@problem_id:3007356]

[类群](@entry_id:182524)的结构完美地捕捉了元素唯一分解的失败程度。
- 如果类群是平凡的，即 $h_K=1$，这意味着 $\mathcal{I}_K = \mathcal{P}_K$。换言之，$\mathcal{O}_K$ 中的每一个理想都是[主理想](@entry_id:152760)。这样的环被称为[主理想整环](@entry_id:152359)（PID）。对于戴德金[整环](@entry_id:155321)（如 $\mathcal{O}_K$），[主理想整环](@entry_id:152359)等价于唯一因子分解整环（UFD）。
- 因此，我们得到了一个根本性的结论：**$\mathcal{O}_K$ 中元素的唯一[因子分解](@entry_id:150389)成立，当且仅当其[类数](@entry_id:156164) $h_K=1$**。[@problem_id:3080549]

当 $h_K > 1$ 时，存在[非主理想](@entry_id:201831)，这正是导致元素唯一分解失败的根源。类数 $h_K$ 就像一个“度量尺”，精确地衡量了 $\mathcal{O}_K$ 偏离唯一因子分解[整环](@entry_id:155321)的程度。尽管元素的算术变得复杂，但通过理想和类群的视角，我们恢复了一种更深层次的、完美的算术结构。