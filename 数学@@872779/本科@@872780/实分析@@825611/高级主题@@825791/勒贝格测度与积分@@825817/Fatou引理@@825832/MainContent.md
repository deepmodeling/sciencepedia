## 引言
在分析学中，极限与积分运算的交换是核心问题。虽然[单调收敛定理](@entry_id:147772)和[控制收敛定理](@entry_id:137784)为等式成立提供了强大的保证，但当函数序列不满足其严格条件时，我们该如何描述极限与积分的关系？这一知识缺口正是[法图引理](@entry_id:147006)（Fatou's Lemma）所要解决的核心问题。[法图引理](@entry_id:147006)并非提供一个等式，而是给出了一个深刻而普适的不等式，为函数序列极限行为的分析提供了重要的下界估计。它在测度论、[泛函分析](@entry_id:146220)和概率论等领域扮演着基石性的角色。

本文将引导您全面掌握[法图引理](@entry_id:147006)。在“原理与机制”一章中，我们将深入其数学表述，探讨不等式严格成立的内在机制，并分析其关键条件。接着，在“应用与跨学科联系”一章中，我们将展示该引理如何成为构建$L^p$空间理论、推导概率论核心结论以及解决[变分问题](@entry_id:756445)的关键工具。最后，通过“动手实践”部分的精选习题，您将有机会亲自运用[法图引理](@entry_id:147006)，巩固所学知识。

## 原理与机制

在测度论与积分理论中，极限运算与积分运算的交换是一个核心问题。[单调收敛定理](@entry_id:147772)和[控制收敛定理](@entry_id:137784)为此交换提供了充分条件。然而，在更一般的情形下，当函数序列不满足这些特定条件时，我们无法保证等式成立。[法图引理](@entry_id:147006) (Fatou's Lemma) 恰好处理了这种情况，它为积分与极限之间的关系提供了一个深刻而普适的不等式。本章将深入探讨[法图引理](@entry_id:147006)的原理、其成立的关键条件、等号成立的特例，以及它的一些重要推广和应用。

### [法图引理](@entry_id:147006)的表述与核心思想

我们首先陈述[法图引理](@entry_id:147006)的正式形式。

**[法图引理](@entry_id:147006)**：令 $(X, \mathcal{M}, \mu)$ 为一个[测度空间](@entry_id:191702)。如果 $\{f_n\}_{n=1}^{\infty}$ 是定义在 $X$ 上的一个[非负可测函数](@entry_id:192146)序列，那么下述不等式成立：
$$
\int_X \left( \liminf_{n \to \infty} f_n \right) \,d\mu \le \liminf_{n \to \infty} \left( \int_X f_n \,d\mu \right)
$$

这个不等式直观地告诉我们，**[极限函数](@entry_id:157601)的积分不超[过积分](@entry_id:753033)的极限**。更准确地说，[函数序列](@entry_id:145607)的逐点[下极限](@entry_id:145282)的积分，小于或等于该[函数序列](@entry_id:145607)积分值的[下极限](@entry_id:145282)。不等式的出现暗示，在取极限的过程中，函数序列所携带的“质量”（即积分值）可能会“丢失”或“泄露”。这种质量的丢失通常通过两种主要机制发生：质量“逃逸”到无穷远处，或者[质量集中](@entry_id:175432)在[测度为零](@entry_id:137864)的集合上。

为了理解这种严格不等的可能性，我们考察几个典型的例子。

**机制一：质量逃逸至无穷**

想象一个“移动的凸起”函数，其形状保持不变，但其位置不断向无穷远处移动。考虑定义在[实数轴](@entry_id:147286) $\mathbb{R}$（带有标准勒贝格测度）上的函数序列 $\{f_n\}$：
$$
f_n(x) = c \cdot \chi_{[n, n+a]}(x)
$$
其中 $c, a$ 是正常数，$\chi_S$ 是集合 $S$ 的[特征函数](@entry_id:186820)。对于任意固定的 $x \in \mathbb{R}$，当 $n$ 足够大以至于 $n > x$ 时，我们总有 $f_n(x) = 0$。这意味着该函数序列逐点收敛于 $0$，因此 $\liminf_{n\to\infty} f_n(x) = 0$ 对所有 $x$ 成立。于是，不等式的左边为：
$$
\int_{\mathbb{R}} \left( \liminf_{n \to \infty} f_n \right) \,d\lambda = \int_{\mathbb{R}} 0 \,d\lambda = 0
$$
然而，对于每一个 $n$，函数 $f_n$ 的积分是这个凸起的“面积”：
$$
\int_{\mathbb{R}} f_n \,d\lambda = \int_{\mathbb{R}} c \cdot \chi_{[n, n+a]} \,d\lambda = c \cdot \lambda([n, n+a]) = ca
$$
这是一个不依赖于 $n$ 的正常数。因此，积分序列的[下极限](@entry_id:145282)是：
$$
\liminf_{n \to \infty} \left( \int_{\mathbb{R}} f_n \,d\lambda \right) = \liminf_{n \to \infty} (ca) = ca
$$
综合来看，我们得到 $0 \le ca$，当 $c, a > 0$ 时这是一个严格不等式。例如，在问题 [@problem_id:1299441] 中，具体函数为 $f_n(x) = 7 \cdot \chi_{[n, n+2]}(x)$，我们计算出左边为 $0$，右边为 $14$，清晰地展示了 $0  14$ 的严格不等关系。这里的“质量”并没有消失，而是随着 $n \to \infty$ 逃逸到了无穷远处，因此在任何有限区域的积分中都无法再捕捉到它。

**机制二：[质量集中](@entry_id:175432)于零测集**

另一种导致严格不等的情形是，[函数序列](@entry_id:145607)的“质量”逐渐集中到一个[测度为零](@entry_id:137864)的集合上。考虑定义在 $[0, 1]$ 上的函数序列 $f_n(x) = (n+1)x^n$ [@problem_id:2298804]。
对于任何 $x \in [0, 1)$，当 $n \to \infty$ 时，$x^n$ 的指数衰减速度快于 $n+1$ 的[多项式增长](@entry_id:177086)速度，因此 $\lim_{n\to\infty} (n+1)x^n = 0$。在 $x=1$ 这一个点上，$f_n(1) = n+1 \to \infty$。由于[勒贝格测度](@entry_id:139781)中单点的[测度为零](@entry_id:137864)，该函数序列[几乎处处收敛](@entry_id:142008)于 $0$。因此，$\liminf_{n\to\infty} f_n(x) = 0$ [几乎处处](@entry_id:146631)成立。不等式的左边是：
$$
\int_0^1 \left( \liminf_{n \to \infty} f_n(x) \right) \,d\lambda = \int_0^1 0 \,d\lambda = 0
$$
接下来计算不等式的右边。对每个 $f_n$ 积分：
$$
\int_0^1 f_n(x) \,d\lambda = \int_0^1 (n+1)x^n \,dx = (n+1) \left[ \frac{x^{n+1}}{n+1} \right]_0^1 = 1
$$
积分序列是一个常数序列 $\{1, 1, 1, \dots\}$，其[下极限](@entry_id:145282)显然是 $1$。因此，我们得到了 $0 \le 1$ 的结果，同样是严格不等。在这个例子中，函数图像表现为一个在 $x=1$ 附近越来越高、越来越窄的“尖峰”。随着 $n$ 的增大，整个积分值（质量）$1$ 被不断地“挤压”到点 $x=1$ 的邻域内，而点 $x=1$ 本身的测度为零。极限函数在这一点的值是无穷大，但在积分意义下，这个[零测集](@entry_id:157694)上的无穷大值对积分结果没有贡献。其他类似构造，如逐渐变窄变高的“帐篷函数”序列，也能展示相同的原理 [@problem_id:1299487] [@problem_id:1418794]。

为了量化这种“质量损失”，我们可以定义 **法图差 (Fatou Discrepancy)** 为不等式两端的差值：
$$
\Delta = \left( \liminf_{n \to \infty} \int_X f_n \,d\mu \right) - \left( \int_X \liminf_{n \to \infty} f_n \,d\mu \right)
$$
根据[法图引理](@entry_id:147006)，对于非负函数序列，$\Delta \ge 0$。通过构造具体的[函数序列](@entry_id:145607)，我们可以计算出这个差值，从而更深入地理解[极限与积分交换](@entry_id:141243)的过程 [@problem_id:1299464]。

### 关键条件：非负性

[法图引理](@entry_id:147006)中的 **非负性** ($f_n \ge 0$) 是一个不可或缺的关键条件。如果允许函数取负值，那么不等式的方向可能被逆转，引理的结论将不再成立。

我们可以构造一个简单的反例来说明这一点 [@problem_id:2298800]。考虑在 $\mathbb{R}$ 上的函数序列：
$$
f_n(x) = -\chi_{[n, n+1]}(x)
$$
这是一个不满足非负性条件的函数序列。我们来计算不等式的两边。

首先，对于任意固定的 $x \in \mathbb{R}$，当 $n > x$ 时，就有 $x \notin [n, n+1]$，因此 $f_n(x) = 0$。这意味着序列 $\{f_n(x)\}$ 最终为常数 $0$，所以 $\liminf_{n\to\infty} f_n(x) = 0$。不等式左边的积分为：
$$
\int_{\mathbb{R}} \left( \liminf_{n \to \infty} f_n \right) \,d\lambda = \int_{\mathbb{R}} 0 \,d\lambda = 0
$$
然后，我们计算每个 $f_n$ 的积分：
$$
\int_{\mathbb{R}} f_n \,d\lambda = \int_{\mathbb{R}} (-\chi_{[n, n+1]}) \,d\lambda = - \lambda([n, n+1]) = -1
$$
这是一个常数序列，其[下极限](@entry_id:145282)为 $-1$。因此，不等式的右边为：
$$
\liminf_{n \to \infty} \left( \int_{\mathbb{R}} f_n \,d\lambda \right) = -1
$$
比较两边的结果，我们发现 $0 > -1$。这与[法图引理](@entry_id:147006)的 $\le$ 方向恰好相反。这个反例清楚地表明，如果没有非负性条件的约束，负值的“质量”可能在极限过程中“凭空出现”，从而破坏原有的不等关系。

[法图引理](@entry_id:147006)的标准证明也依赖于非负性。其证明思路是构造一个辅助[函数序列](@entry_id:145607) $g_n(x) = \inf_{k \ge n} f_k(x)$。由于 $f_k \ge 0$，我们有 $g_n \ge 0$。同时，$\{g_n\}$ 是一个单调递增的序列（因为取下确界的集合越来越小），并且 $\lim_{n\to\infty} g_n(x) = \liminf_{n\to\infty} f_n(x)$。对非负递增序列 $\{g_n\}$ 应用[单调收敛定理](@entry_id:147772)，我们得到：
$$
\int_X \left(\liminf_{n\to\infty} f_n\right) \,d\mu = \int_X \left(\lim_{n\to\infty} g_n\right) \,d\mu = \lim_{n\to\infty} \int_X g_n \,d\mu
$$
由于 $g_n \le f_n$，它们的积分也满足 $\int_X g_n \,d\mu \le \int_X f_n \,d\mu$。对不等式两边取[下极限](@entry_id:145282)，并注意到左边极限存在，我们有：
$$
\lim_{n\to\infty} \int_X g_n \,d\mu = \liminf_{n\to\infty} \int_X g_n \,d\mu \le \liminf_{n\to\infty} \int_X f_n \,d\mu
$$
组合以上结果，便证明了[法图引理](@entry_id:147006)。这个证明过程清晰地揭示了非负性是如何通过构造[单调序列](@entry_id:145193)和应用[单调收敛定理](@entry_id:147772)来发挥作用的。

### 等号成立的条件与[单调收敛定理](@entry_id:147772)

尽管[法图引理](@entry_id:147006)通常表现为严格不等式，但在某些重要情况下，等号是成立的。理解这些情况有助于我们把握[法图引理](@entry_id:147006)与勒贝格积分理论中其他核心定理（如[单调收敛定理](@entry_id:147772)和[控制收敛定理](@entry_id:137784)）之间的联系。

最直接的等号成立条件是当[函数序列](@entry_id:145607)本身满足 **[单调收敛定理](@entry_id:147772) (Monotone Convergence Theorem, MCT)** 的前提时。MCT指出，如果 $\{f_n\}$ 是一个[非负可测函数](@entry_id:192146)的单调递增序列，且[逐点收敛](@entry_id:145914)于 $f$，那么 $\lim_{n\to\infty} \int_X f_n \,d\mu = \int_X f \,d\mu$。

对于一个单调递增序列，其极限和[下极限](@entry_id:145282)是相等的，即 $\lim_{n\to\infty} f_n = \liminf_{n\to\infty} f_n = f$。同样，其积分序列 $\{ \int_X f_n \,d\mu \}$ 也是一个单调递增的[实数序列](@entry_id:141090)，因此其极限与[下极限](@entry_id:145282)也相等。将这些代入[法图引理](@entry_id:147006)的不等式：
$$
\int_X \left( \lim_{n \to \infty} f_n \right) \,d\mu \le \lim_{n \to \infty} \left( \int_X f_n \,d\mu \right)
$$
这正是MCT的结论，说明MCT可以被看作是[法图引理](@entry_id:147006)等号成立的一种特殊情况。

我们可以通过一个具体的递增序列来验证这一点。考虑在 $[0, 1/2]$ 上的[函数序列](@entry_id:145607) $f_n(x) = \sum_{k=0}^{n} x^k$ [@problem_id:2298831]。这是一个非负函数的[部分和序列](@entry_id:161258)，因此对任意固定的 $x$，$\{f_n(x)\}$ 是单调递增的。其[逐点极限](@entry_id:193549)为几何级数的和 $f(x) = \frac{1}{1-x}$。计算[法图引理](@entry_id:147006)的两边：
$$
A = \int_0^{1/2} f(x) \,dx = \int_0^{1/2} \frac{1}{1-x} \,dx = [-\ln(1-x)]_0^{1/2} = \ln 2
$$
$$
B = \liminf_{n\to\infty} \int_0^{1/2} \sum_{k=0}^{n} x^k \,dx = \liminf_{n\to\infty} \sum_{k=0}^{n} \frac{(1/2)^{k+1}}{k+1} = \sum_{k=1}^{\infty} \frac{(1/2)^k}{k} = \ln 2
$$
在这个例子中，我们得到 $A=B=\ln 2$，[法图引理](@entry_id:147006)的等号成立，与MCT的预测完全一致。

除了[单调序列](@entry_id:145193)，如果一个非负[函数序列](@entry_id:145607) $\{f_n\}$ 被一个[可积函数](@entry_id:191199) $g$ 所控制（即 $f_n \le g$ 对所有 $n$ 成立），并且 $\{f_n\}$ 逐点收敛于 $f$，那么由[控制收敛定理](@entry_id:137784)（Dominated Convergence Theorem, DCT）可知 $\lim_{n\to\infty} \int f_n = \int f$。在这种情况下，[法图引理](@entry_id:147006)的等号也成立。例如，序列 $g_n(x) = e^2 + x^n$ 在 $[0, 1]$ 上就属于这种情况，可以验证其法图差为零 [@problem_id:1418794]。

### [法图引理](@entry_id:147006)的推广与变体

[法图引理](@entry_id:147006)的强大之处不仅在于其自身，还在于它可以作为工具推导出其他有用的不等式和结论。

#### 反向[法图引理](@entry_id:147006) (Reverse Fatou's Lemma)

通过一个巧妙的代换，我们可以从标准的[法图引理](@entry_id:147006)推导出一个关于[上极限](@entry_id:144243)的“反向”版本。

**反向[法图引理](@entry_id:147006)**：令 $\{f_n\}$ 是一个[可测函数序列](@entry_id:194460)，如果存在一个 **可积** 函数 $g$ 使得对所有 $n$ 都有 $f_n(x) \le g(x)$，那么：
$$
\limsup_{n \to \infty} \left( \int_X f_n \,d\mu \right) \le \int_X \left( \limsup_{n \to \infty} f_n \right) \,d\mu
$$

注意这个不等式的方向与标准[法图引理](@entry_id:147006)相反，并且涉及的是[上极限](@entry_id:144243)。其证明思路是应用标准[法图引理](@entry_id:147006)到新的非负[函数序列](@entry_id:145607) $h_n = g - f_n$ 上 [@problem_id:2298821]。
由于 $f_n \le g$，序列 $\{h_n\}$ 是非负的。应用[法图引理](@entry_id:147006)于 $\{h_n\}$：
$$
\int_X \liminf_{n\to\infty} (g - f_n) \,d\mu \le \liminf_{n\to\infty} \int_X (g - f_n) \,d\mu
$$
利用[下极限](@entry_id:145282)和上极限的关系 $\liminf(a-b) = a - \limsup(b)$ 和 $\liminf(-b) = -\limsup(b)$，并利用[积分的线性](@entry_id:189393)性质（由于 $g$ 可积，其积分是有限实数，可以从极限中提出）：
$$
\int_X (g - \limsup_{n\to\infty} f_n) \,d\mu \le \int_X g \,d\mu - \limsup_{n\to\infty} \int_X f_n \,d\mu
$$
$$
\int_X g \,d\mu - \int_X \limsup_{n\to\infty} f_n \,d\mu \le \int_X g \,d\mu - \limsup_{n\to\infty} \int_X f_n \,d\mu
$$
消去 $\int_X g \,d\mu$ 并两边乘以 $-1$，我们便得到了反向[法图引理](@entry_id:147006)。这个定理在处理有[上界](@entry_id:274738)的[函数序列](@entry_id:145607)时非常有用。

#### 对[集合序列](@entry_id:184571)的应用

[法图引理](@entry_id:147006)有一个非常直观且重要的应用，即将其应用于[集合序列](@entry_id:184571)的[特征函数](@entry_id:186820)上，从而得到关于集合测度的不等式。

令 $\{A_n\}$ 是一个可测集序列。考虑其特征函数序列 $f_n = \chi_{A_n}$。这是一个[非负可测函数](@entry_id:192146)序列，因此可以应用[法图引理](@entry_id:147006)。我们需要确定 $\liminf f_n$ 对应的集合。根据定义，点 $x$ 属于集合的[下极限](@entry_id:145282) $\liminf A_n$，当且仅当 $x$ 从某一时刻起属于所有的 $A_n$。这等价于序列 $\{\chi_{A_n}(x)\}$ 从某一时刻起恒为 $1$，即 $\liminf_{n\to\infty} \chi_{A_n}(x) = 1$。如果 $x \notin \liminf A_n$，那么 $\{\chi_{A_n}(x)\}$ 中有无穷多个 $0$，其[下极限](@entry_id:145282)为 $0$。因此，我们有恒等式：
$$
\chi_{\liminf A_n} = \liminf_{n \to \infty} \chi_{A_n}
$$
将此代入[法图引理](@entry_id:147006)，并利用测度的定义 $\mu(A) = \int \chi_A \,d\mu$，我们得到：
$$
\mu(\liminf_{n\to\infty} A_n) = \int_X \chi_{\liminf A_n} \,d\mu = \int_X (\liminf_{n\to\infty} \chi_{A_n}) \,d\mu \le \liminf_{n\to\infty} \int_X \chi_{A_n} \,d\mu = \liminf_{n\to\infty} \mu(A_n)
$$
这就得到了关于集合测度的重要不等式 [@problem_id:1299422]：
$$
\mu(\liminf_{n\to\infty} A_n) \le \liminf_{n\to\infty} \mu(A_n)
$$
类似地，若[测度空间](@entry_id:191702) $(X, \mathcal{M}, \mu)$ 的总测度 $\mu(X)$ 有限，我们可以对 $f_n = \chi_{A_n}$ 应用反向[法图引理](@entry_id:147006)（此时 $f_n \le 1$，而常数函数 $g=1$ 在[有限测度空间](@entry_id:198109)上是可积的），得到关于上极限的对应不等式：$\mu(\limsup_{n\to\infty} A_n) \ge \limsup_{n\to\infty} \mu(A_n)$。

#### 对级数的应用

[法图引理](@entry_id:147006)的原理是普适的，不仅限于[勒贝格积分](@entry_id:140189)。级数求和可以看作是在自然数集 $\mathbb{N}$ 上关于 **[计数测度](@entry_id:188748)** 的积分。因此，[法图引理](@entry_id:147006)有一个离散版本，即关于级数的[法图引理](@entry_id:147006)。

**级数的[法图引理](@entry_id:147006)**：令 $\{a_{n,k}\}_{n,k=0}^{\infty}$ 是一个非负双重序列。那么：
$$
\sum_{k=0}^{\infty} \left( \liminf_{n\to\infty} a_{n,k} \right) \le \liminf_{n\to\infty} \left( \sum_{k=0}^{\infty} a_{n,k} \right)
$$
这个不等式关系是极限与求和这两个运算不可随意交换的又一个体现。同样，严格不等也可能发生。例如，考虑双重序列 $a_{n,k} = \frac{1}{2^k} + \delta_{n,k}$，其中 $\delta_{n,k}$ 是克罗内克符号 [@problem_id:2298803]。
对于固定的 $k$，当 $n \to \infty$ 时，$a_{n,k}$ 最终等于 $\frac{1}{2^k}$，所以 $\liminf_{n\to\infty} a_{n,k} = \frac{1}{2^k}$。不等式左边是：
$$
L = \sum_{k=0}^{\infty} \frac{1}{2^k} = 2
$$
对于固定的 $n$，级数 $\sum_{k=0}^{\infty} a_{n,k}$ 的和为 $\sum_{k=0}^{\infty} \frac{1}{2^k} + \sum_{k=0}^{\infty} \delta_{n,k} = 2 + 1 = 3$。因此，不等式右边是：
$$
R = \liminf_{n\to\infty} (3) = 3
$$
我们得到了 $2  3$，再次看到了[法图引理](@entry_id:147006)中的严格不等。这个例子中的“质量损失”可以看作是，对于每一个 $n$，都有一个额外的“质量”$1$（在 $k=n$ 的位置），但在逐点取[下极限](@entry_id:145282)时，这个移动的“质量”消失了。

综上所述，[法图引理](@entry_id:147006)及其变体为处理分析学中的极限问题提供了强有力的工具，深刻地揭示了积分与极限运算交换时的复杂性和微妙之处。