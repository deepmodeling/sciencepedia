## 引言
在抽象代数中，域扩张是研究域结构的核心工具，它使我们能够从一个已知的域（基域）出发，构建出更广阔、更复杂的代数世界。在所有类型的扩张中，**[单扩张](@entry_id:152948)**（Simple Extension）是最为基本和直观的一种，它通过向基域中添加仅仅一个新元素来生成一个更大的域。理解[单扩张](@entry_id:152948)的内在机制，是掌握更高级理论（如伽罗瓦理论）的必经之路。本文旨在系统性地揭示[单扩张](@entry_id:152948)的结构、运算规则及其在数学各分支中的广泛应用。

本文将带领读者深入[单扩张](@entry_id:152948)的世界，分为三个主要部分。在“**原则与机制**”中，我们将建立[单扩张](@entry_id:152948)的理论基础，阐明其如何根据添加元素的性质（[代数元](@entry_id:153893)或[超越元](@entry_id:150504)）呈现为截然不同的结构，并将其描述为一个[向量空间](@entry_id:151108)，从而简化其内部的算术运算。接着，在“**应用与交叉学科联系**”中，我们将展示这一抽象理论的强大生命力，探讨其如何应用于数论、几何学、编码理论和现代密码学等领域，揭示代数对称性与数字世界构造之间的深刻联系。最后，通过“**动手实践**”部分，读者将有机会通过解决具体问题来巩固所学知识，将理论应用于实践。

## 原则与机制

在介绍完[域扩张](@entry_id:153187)的基本概念之后，本章将深入探讨一类最基本且最重要的扩张：**[单扩张](@entry_id:152948)** (simple extension)。[单扩张](@entry_id:152948)是由基域 $F$ 添加单个元素 $\alpha$ 生成的最小域，记作 $F(\alpha)$。对[单扩张](@entry_id:152948)的结构和性质的理解，是通往更高级的抽象代数理论（如伽罗瓦理论）的基石。我们将系统地阐述其核心原理与内在机制。

### [单扩张](@entry_id:152948)的结构：从多项式到[向量空间](@entry_id:151108)

一个[单扩张](@entry_id:152948) $F(\alpha)$ 的结构，根本上取决于元素 $\alpha$ 与基域 $F$ 之间的关系。存在两种截然不同的情况：$\alpha$ 是 $F$ 上的**[代数元](@entry_id:153893)** (algebraic element)，或者 $\alpha$ 是 $F$ 上的**[超越元](@entry_id:150504)** (transcendental element)。

如果 $\alpha$ 是[超越元](@entry_id:150504)，意味着它不是任何一个系数在 $F$ 中的非零多项式的根。在这种情况下，域 $F(\alpha)$ 同构于 $F$ 上的[有理函数](@entry_id:154279)域 $F(x)$。这意味着 $F(\alpha)$ 中的元素是形如 $\frac{f(\alpha)}{g(\alpha)}$ 的“分数”，其中 $f(x)$ 和 $g(x)$ 是系数在 $F$ 中的多项式，且 $g(\alpha) \neq 0$。

然而，本章的重点是当 $\alpha$ 为[代数元](@entry_id:153893)时的情形。一个元素 $\alpha$ 被称为 $F$ 上的[代数元](@entry_id:153893)，如果存在一个以 $F$ 中元素为系数的非零多项式 $p(x)$，使得 $p(\alpha) = 0$。在所有满足该条件的多项式中，存在一个唯一的首一（即最高次项系数为1）且次数最低的多项式，我们称之为 $\alpha$ 在 $F$ 上的**[最小多项式](@entry_id:153598)** (minimal polynomial)，记作 $m_{\alpha, F}(x)$。最小多项式在 $F[x]$（系数在 $F$ 中的[多项式环](@entry_id:152854)）中总是不可约的。

[最小多项式](@entry_id:153598)的次数 $n = \deg(m_{\alpha, F}(x))$ 扮演着至关重要的角色。它定义了扩张的**次数** (degree) 或**维数** (dimension)，记作 $[F(\alpha):F] = n$。这个次数的深刻含义是，域 $F(\alpha)$ 可以被看作是基域 $F$ 上的一个 $n$ 维**[向量空间](@entry_id:151108)**。这个[向量空间](@entry_id:151108)的一组**基** (basis) 是 $\{1, \alpha, \alpha^2, \dots, \alpha^{n-1}\}$。这意味着 $F(\alpha)$ 中的任何一个元素 $\beta$ 都可以被唯一地表示为这些[基向量](@entry_id:199546)的[线性组合](@entry_id:154743)：
$$ \beta = c_0 + c_1\alpha + c_2\alpha^2 + \dots + c_{n-1}\alpha^{n-1} $$
其中系数 $c_0, c_1, \dots, c_{n-1}$ 都是基域 $F$ 中的元素。

从形式上讲，单[代数扩张](@entry_id:156472) $F(\alpha)$ 同构于商环 $F[x]/\langle m_{\alpha, F}(x) \rangle$，其中 $\langle m_{\alpha, F}(x) \rangle$ 是由最小多项式生成的理想。这个同构关系为我们将[多项式环](@entry_id:152854)中的算术规则转化为新域 $F(\alpha)$ 中的运算提供了理论基础。

**例1：确定扩张次数** [@problem_id:1821122]
要确定[单扩张](@entry_id:152948) $\mathbb{Q}(\alpha)$ 的次数，我们需要找到 $\alpha$ 在 $\mathbb{Q}$ 上的[最小多项式](@entry_id:153598)的次数。假设 $\alpha$ 是多项式 $p(x) = x^5 - 6x^4 + 3x^2 - 12x + 9 = 0$ 的一个根。如果我们能够证明 $p(x)$ 在 $\mathbb{Q}$ 上是不可约的，那么它就是 $\alpha$ 的[最小多项式](@entry_id:153598)。一种强大的证明不可约性的方法是模素数约化。将 $p(x)$ 的系数模 $2$ 得到 $x^5 + x^2 + 1 \in \mathbb{F}_2[x]$。可以验证这个多项式在 $\mathbb{F}_2$ 上没有根，也不是 $\mathbb{F}_2$ 上唯一的不可约二次多项式 $x^2+x+1$ 的倍数，因此它在 $\mathbb{F}_2$ 上是不可约的。一个整系数多项式如果在模某个素数后得到的低次多项式是不可约的，那么原多项式在 $\mathbb{Q}$ 上也是不可约的。因此，$p(x)$ 是不可约的，其次数为 $5$。所以，扩张次数 $[\mathbb{Q}(\alpha):\mathbb{Q}] = 5$。

这个[向量空间](@entry_id:151108)的视角也清晰地揭示了[代数元](@entry_id:153893)与[超越元](@entry_id:150504)之间的本质区别 [@problem_id:1821166]。对于[代数元](@entry_id:153893) $\alpha$（例如，$\alpha = \sqrt[3]{7}$，其[最小多项式](@entry_id:153598)为 $x^3-7=0$），它的幂次序列 $\{1, \alpha, \alpha^2, \alpha^3, \dots\}$ 在基域 $\mathbb{Q}$ 上是**[线性相关](@entry_id:185830)**的。最小的[线性相关](@entry_id:185830)关系恰好由最小多项式给出：$1 \cdot \alpha^3 + 0 \cdot \alpha^2 + 0 \cdot \alpha - 7 \cdot 1 = 0$。使得集合 $\{1, \alpha, \dots, \alpha^{n_1}\}$ 首次[线性相关](@entry_id:185830)的最小正整数 $n_1$ 就是最小多项式的次数，即扩张次数。在此例中，$n_1=3$。

相反，如果一个元素 $\beta$ 是[超越元](@entry_id:150504)，根据定义，它的任何非平凡多项式都不会为零。这意味着它的幂次序列 $\{1, \beta, \beta^2, \dots, \beta^m\}$ 对于任何正整数 $m$ 都是**线性无关**的。因此，不存在一个有限的基，$\mathbb{Q}(\beta)$ 作为 $\mathbb{Q}$ 上的[向量空间](@entry_id:151108)是无限维的。例如，如果 $\beta$ 是超越的，那么 $\beta^2$ 也是超越的。因此，集合 $\{1, \beta^2, (\beta^2)^2, \dots, (\beta^2)^m\}$ 对所有 $m$ 都是线性无关的，不存在满足线性相关性的最小正整数 $n_2$。

### [单扩张](@entry_id:152948)中的算术运算

将 $F(\alpha)$ 视为[向量空间](@entry_id:151108)极大地简化了其中的算术。加法和减法就是对应系数的加减，与向量运算完全相同。乘法和除法是体现域结构的关键。

**乘法**

要计算 $F(\alpha)$ 中两个元素 $\beta_1$ 和 $\beta_2$ 的乘积，我们首先像普通多项式一样将它们相乘。结果会得到一个关于 $\alpha$ 的多项式，其次数可能大于或等于 $n$。此时，我们需要利用关系式 $m_{\alpha, F}(\alpha) = 0$ 来“降次”，将所有次数不小于 $n$ 的 $\alpha$ 的幂都替换为次数小于 $n$ 的幂的[线性组合](@entry_id:154743)，直到最终结果是次数小于 $n$ 的多项式。

**例2：元素相乘** [@problem_id:1821150]
设 $\alpha = \sqrt[3]{5}$，则其在 $\mathbb{Q}$ 上的[最小多项式](@entry_id:153598)为 $x^3-5=0$，即 $\alpha^3=5$。我们来计算域 $\mathbb{Q}(\alpha)$ 中两个元素 $x = 2 - 3\alpha + \frac{1}{2}\alpha^2$ 和 $y = 1 + \alpha - 2\alpha^2$ 的乘积 $z = xy$。
首先展开乘积：
$$ z = (2 - 3\alpha + \frac{1}{2}\alpha^2)(1 + \alpha - 2\alpha^2) = 2 - \alpha - \frac{13}{2}\alpha^2 + \frac{13}{2}\alpha^3 - \alpha^4 $$
接下来，使用 $\alpha^3=5$ 进行降次。我们有 $\alpha^4 = \alpha \cdot \alpha^3 = 5\alpha$。代入上式：
$$ z = 2 - \alpha - \frac{13}{2}\alpha^2 + \frac{13}{2}(5) - 5\alpha = (2 + \frac{65}{2}) + (-1 - 5)\alpha - \frac{13}{2}\alpha^2 = \frac{69}{2} - 6\alpha - \frac{13}{2}\alpha^2 $$
这就得到了乘积在基 $\{1, \alpha, \alpha^2\}$ 下的标准表示。这个过程 [@problem_id:1821120] 也同样适用，例如，若 $\alpha^3 - 3\alpha + 4 = 0$，则 $\alpha^3 = 3\alpha-4$，于是 $\alpha^4 = \alpha \cdot \alpha^3 = \alpha(3\alpha-4) = 3\alpha^2 - 4\alpha$。

**除法（求[逆元](@entry_id:140790)）**

证明 $F(\alpha)$ 是一个域的关键在于证明每个非零元素都存在乘法逆元，并且该[逆元](@entry_id:140790)仍在 $F(\alpha)$ 中。对于非零元素 $\beta = g(\alpha) \in F(\alpha)$，求其[逆元](@entry_id:140790) $\beta^{-1}$ 有两种主要方法。

第一种方法是利用**[扩展欧几里得算法](@entry_id:153449)**。由于 $m_{\alpha, F}(x)$ 是不可约的，且 $g(x)$ 的次数小于 $m_{\alpha, F}(x)$，所以它们[互素](@entry_id:143119)。根据[扩展欧几里得算法](@entry_id:153449)，存在多项式 $s(x), t(x) \in F[x]$ 使得：
$$ s(x)g(x) + t(x)m_{\alpha, F}(x) = 1 $$
将 $\alpha$ 代入上式，由于 $m_{\alpha, F}(\alpha) = 0$，我们得到 $s(\alpha)g(\alpha) = 1$。因此，逆元就是 $g(\alpha)^{-1} = s(\alpha)$，它显然是 $F(\alpha)$ 中的元素。

第二种方法是**[解线性方程组](@entry_id:136676)**，这是一种更具构造性的方法 [@problem_id:1821116]。设[逆元](@entry_id:140790)为 $\beta^{-1} = d_0 + d_1\alpha + \dots + d_{n-1}\alpha^{n-1}$。我们要求解满足 $\beta \cdot \beta^{-1} = 1$ 的系数 $d_i$。我们将乘积展开，并利用 $m_{\alpha, F}(\alpha) = 0$ 进行降次，最终得到一个关于 $\alpha$ 的次数小于 $n$ 的多项式。令该多项式等于 $1$（即 $1 + 0\alpha + 0\alpha^2 + \dots$），通过比较基 $\{1, \alpha, \dots, \alpha^{n-1}\}$ 的系数，我们可以建立一个关于未知数 $d_0, \dots, d_{n-1}$ 的 $n \times n$ [线性方程组](@entry_id:148943)。因为 $\beta \neq 0$，这个[方程组](@entry_id:193238)总有唯一解。虽然对于一般的系数 $a, b, c$ 求解会很繁琐，但这个过程从原理上保证了逆元的存在性和[可计算性](@entry_id:276011)。

此外，值得一提的是，当我们从[整数环](@entry_id:181003) $\mathbb{Z}$ 出发，考虑一个**[代数整数](@entry_id:151672)** $\alpha$（即它是某个首一整系数[多项式的根](@entry_id:154615)）时，我们可以构造环 $\mathbb{Z}[\alpha]$。这个环的[分式域](@entry_id:154960) $\text{Frac}(\mathbb{Z}[\alpha])$，与直接在有理[数域](@entry_id:155558) $\mathbb{Q}$ 上添加 $\alpha$ 得到的域 $\mathbb{Q}(\alpha)$，实际上是同一个域 [@problem_id:1821138]。这表明，无论是先将系数扩展到有理数再添加 $\alpha$，还是先用整数和 $\alpha$ 构造环再取分式，最终都殊途同归，得到了同一个[单扩张](@entry_id:152948)域。

### [单扩张](@entry_id:152948)的进阶性质

掌握了[单扩张](@entry_id:152948)的基本结构和运算后，我们可以探讨一些更深刻的性质，这些性质将[单扩张](@entry_id:152948)与更广阔的代数理论联系起来。

#### [本原元定理](@entry_id:156597)

我们经常会遇到由多个元素生成的域，例如 $\mathbb{Q}(\sqrt{2}, i)$，它是包含 $\mathbb{Q}$、$\sqrt{2}$ 和 $i$ 的最小域。一个自然的问题是：这种多次扩张能否被一个单次扩张所取代？也就是说，是否存在一个“[本原元](@entry_id:154321)” $\gamma$ 使得 $\mathbb{Q}(\sqrt{2}, i) = \mathbb{Q}(\gamma)$？

**[本原元定理](@entry_id:156597)** (Primitive Element Theorem) 给出了一个强有力的肯定回答：任何特征为零的域（如 $\mathbb{Q}$）上的有限次扩张都是一个[单扩张](@entry_id:152948)。对于 $\mathbb{Q}(\sqrt{2}, i)$，其扩张次数为 $[\mathbb{Q}(\sqrt{2}, i):\mathbb{Q}] = [\mathbb{Q}(\sqrt{2}, i):\mathbb{Q}(\sqrt{2})] \cdot [\mathbb{Q}(\sqrt{2}):\mathbb{Q}] = 2 \cdot 2 = 4$。根据[本原元定理](@entry_id:156597)，必定存在一个 $\gamma$ 使得 $\mathbb{Q}(\sqrt{2}, i) = \mathbb{Q}(\gamma)$ 且 $[\mathbb{Q}(\gamma):\mathbb{Q}]=4$。

如何找到这样的 $\gamma$ 呢？通常，生成元的[线性组合](@entry_id:154743)是一个很好的候选。例如，取 $\gamma = \sqrt{2} + i$ [@problem_id:1821097]。我们可以通过计算证明它是我们寻找的[本原元](@entry_id:154321)。通过一系列代数运算，可以发现 $\gamma$ 满足整系数多项式 $x^4 - 2x^2 + 9 = 0$。可以证明此多项式在 $\mathbb{Q}$ 上不可约，因此它是 $\gamma$ 的[最小多项式](@entry_id:153598)。这意味着 $[\mathbb{Q}(\gamma):\mathbb{Q}] = 4$。由于 $\mathbb{Q}(\gamma)$ 是 $\mathbb{Q}(\sqrt{2}, i)$ 的一个子域，且它们的扩张次数相同，因此这两个域必然相等：$\mathbb{Q}(\sqrt{2}, i) = \mathbb{Q}(\sqrt{2}+i)$。

#### [正规扩张](@entry_id:156398)与[分裂域](@entry_id:151552)

当我们通过添加一个不[可约多项式](@entry_id:148759) $p(x)$ 的根 $\alpha$ 构造了[单扩张](@entry_id:152948) $\mathbb{Q}(\alpha)$ 后，一个非常深刻的问题随之而来：$p(x)$ 的其他根是否也“自动”地包含在这个新域中？[@problem_id:1821141]

如果一个扩张 $K/F$ 具有这样的性质，即任何一个在 $F$ 上不可约、但在 $K$ 中有一个根的多项式，其所有根都在 $K$ 中，则称该扩张为**[正规扩张](@entry_id:156398)** (normal extension)。对于由不[可约多项式](@entry_id:148759) $p(x)$ 的根 $\alpha$ 生成的[单扩张](@entry_id:152948) $\mathbb{Q}(\alpha)$，它是否为[正规扩张](@entry_id:156398)，等价于 $p(x)$ 的所有根是否都在 $\mathbb{Q}(\alpha)$ 中。如果一个域包含了某个多项式的所有根，则称该域为该多项式的**[分裂域](@entry_id:151552)** (splitting field)。

*   **是[正规扩张](@entry_id:156398)的情况**：
    *   $p(x) = x^2 + 5$。其根为 $\alpha = i\sqrt{5}$ 和 $-\alpha = -i\sqrt{5}$。显然，$\mathbb{Q}(\alpha)$ 包含了它的[相反数](@entry_id:151709) $-\alpha$。事实上，所有二次扩张都是[正规扩张](@entry_id:156398)。
    *   $p(x) = x^4 + x^3 + x^2 + x + 1$。这是5次单位根的[最小多项式](@entry_id:153598)（即5次[分圆多项式](@entry_id:155668) $\Phi_5(x)$）。如果 $\alpha$ 是一个根，那么其他根是 $\alpha^2, \alpha^3, \alpha^4$。这些根显然都是 $\alpha$ 的幂，因此它们都在 $\mathbb{Q}(\alpha)$ 中。

*   **不是[正规扩张](@entry_id:156398)的情况**：
    *   $p(x) = x^3 - 2$。它的三个根是 $\sqrt[3]{2}$, $\sqrt[3]{2}\omega$, $\sqrt[3]{2}\omega^2$，其中 $\omega = e^{i2\pi/3}$ 是一个复立方[单位根](@entry_id:143302)。如果我们令 $\alpha = \sqrt[3]{2}$，则 $\mathbb{Q}(\alpha)$ 完全包含在实数域 $\mathbb{R}$ 中。然而，另外两个根是复数，它们显然不在 $\mathbb{Q}(\alpha)$ 中。要包含所有根，我们需要同时添加 $\alpha$ 和 $\omega$，生成的[分裂域](@entry_id:151552)是 $\mathbb{Q}(\alpha, \omega)$，其次数为6，大于 $\mathbb{Q}(\alpha)$ 的次数3。
    *   $p(x) = x^4 - 2$。其根为 $\sqrt[4]{2}, -\sqrt[4]{2}, i\sqrt[4]{2}, -i\sqrt[4]{2}$。同样，如果我们取实根 $\alpha = \sqrt[4]{2}$，则 $\mathbb{Q}(\alpha)$ 是 $\mathbb{R}$ 的[子域](@entry_id:155812)，无法包含复数根 $i\alpha$。其[分裂域](@entry_id:151552)是 $\mathbb{Q}(\alpha, i)$，次数为8，大于 $\mathbb{Q}(\alpha)$ 的次数4。

这个问题——[单扩张](@entry_id:152948)何时包含其生成元[最小多项式](@entry_id:153598)的所有根——是通向伽罗瓦理论的核心入口，它将域的结构与群论联系起来。

### [单扩张](@entry_id:152948)的边界

最后，我们探讨[单扩张](@entry_id:152948)概念的适用范围和局限性，这将帮助我们更全面地理解[域扩张](@entry_id:153187)理论。

首先，基域的性质对扩张有决定性影响。考虑[复数域](@entry_id:153768) $\mathbb{C}$，它是**[代数闭域](@entry_id:151836)** (algebraically closed field)，这意味着任何系数在 $\mathbb{C}$ 中的非常数多项式在 $\mathbb{C}$ 中都有根。根据[代数基本定理](@entry_id:152321)，$\mathbb{C}$ 上唯一的不[可约多项式](@entry_id:148759)是一次多项式。因此，如果一个元素 $\alpha$ 在 $\mathbb{C}$ 上是代数的，其[最小多项式](@entry_id:153598)必然是形如 $x-\alpha$ 的一次多项式。这意味着扩张次数 $[\mathbb{C}(\alpha):\mathbb{C}] = 1$，从而 $\mathbb{C}(\alpha) = \mathbb{C}$ [@problem_id:1821167]。换言之，在[代数闭域](@entry_id:151836)上进行任何单**代数**扩张，都无法得到比原域更大的域。

其次，是否存在不能被表示为[单扩张](@entry_id:152948)的[代数扩张](@entry_id:156472)？考虑所有有理数域 $\mathbb{Q}$ 上的[代数元](@entry_id:153893)的集合，记为 $\overline{\mathbb{Q}}$。这个集合自身构成一个域，是 $\mathbb{Q}$ 的一个扩张。$\overline{\mathbb{Q}}$ 能否被写成 $\mathbb{Q}(\gamma)$ 的形式呢？答案是否定的 [@problem_id:1821142]。

其根本原因在于扩张次数。一个单[代数扩张](@entry_id:156472) $\mathbb{Q}(\gamma)$ 的次数 $[\mathbb{Q}(\gamma):\mathbb{Q}]$ 是有限的，等于 $\gamma$ 的最小多项式的次数 $d$。然而，$\overline{\mathbb{Q}}$ 这个域包含了**所有**的代数数。我们可以构造任意高次数的不[可约多项式](@entry_id:148759)，例如，根据爱森斯坦判别法，多项式 $p_n(x) = x^n - 2$ 对任意正整数 $n$ 在 $\mathbb{Q}$ 上都是不可约的。它的根 $\sqrt[n]{2}$ 是一个 $n$ 次[代数数](@entry_id:150888)，因此 $\sqrt[n]{2} \in \overline{\mathbb{Q}}$。这意味着 $\overline{\mathbb{Q}}$ 包含一个次数为 $n$ 的[子域](@entry_id:155812) $\mathbb{Q}(\sqrt[n]{2})$。根据[域扩张](@entry_id:153187)的乘法塔定理（Tower Law），子域的次数必须能整除整个[扩张的次数](@entry_id:151271)，即 $[ \mathbb{Q}(\sqrt[n]{2}) : \mathbb{Q} ]$ 必须整除 $[\overline{\mathbb{Q}}:\mathbb{Q}]$。这意味着 $n$ 必须整除 $[\overline{\mathbb{Q}}:\mathbb{Q}]$。但由于 $n$ 可以是任意大的正整数，没有任何一个有限的整数可以被所有正整数整除。唯一的可能性是 $[\overline{\mathbb{Q}}:\mathbb{Q}]$ 是无限的。

因为任何单代数[扩张的次数](@entry_id:151271)都是有限的，而 $[\overline{\mathbb{Q}}:\mathbb{Q}]$ 是无限的，所以 $\overline{\mathbb{Q}}$ 不可能是一个[单扩张](@entry_id:152948)。这揭示了[单扩张](@entry_id:152948)虽然强大，但并不能描述所有类型的[代数扩张](@entry_id:156472)，尤其像 $\overline{\mathbb{Q}}$ 这样的无限次[代数扩张](@entry_id:156472)。