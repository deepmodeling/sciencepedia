## 引言
代数数论是现代数论的基石，它通过将我们熟悉的整数和有理数置于更广阔的[代数结构](@entry_id:137052)中，为解决经典的数论问题提供了强有力的工具。其核心研究对象便是代数数与[代数整数](@entry_id:151672)——它们分别是整系数多项式和首一整系数[多项式的根](@entry_id:154615)。然而，当我们将整数 $\mathbb{Z}$ 推广到[数域](@entry_id:155558)中的整数环时，一个基本而优美的性质——唯一[因子分解](@entry_id:150389)，时常会失效。如何理解并“修复”这一结构上的“缺陷”，正是代数数论所要解决的核心知识缺口之一。

本文将带领读者系统地探索代数数与[代数整数](@entry_id:151672)的世界。在第一章“原理与机制”中，我们将从基本定义出发，建立起数域、整数环、理想和范数等核心概念，并揭示整数环作为戴德金[整环](@entry_id:155321)的深刻结构。随后，在第二章“应用与跨学科联系”中，我们将展示这些抽象理论如何应用于具体计算，例如确定类数和[基本单位](@entry_id:148878)，并探讨其如何与[群表示论](@entry_id:141930)、椭圆曲线等其他数学分支产生深刻的共鸣。最后，第三章“动手实践”将通过一系列精心设计的问题，帮助读者巩固理论知识，并将其转化为解决实际问题的能力。通过这一趟旅程，读者将不仅掌握代数数论的基础，更能领会其在现代数学中的力量与美。

## 原理与机制

本章旨在系统地阐述[代数数论](@entry_id:148067)的基本构造单元——[代数数](@entry_id:150888)与[代数整数](@entry_id:151672)的原理和机制。我们将从基本定义出发，逐步建立起它们的结构性属性，并引入数域、[整数环](@entry_id:181003)、嵌入、迹、范数等核心概念。最终，我们将探讨整数环作为一个独特代数对象所具有的深刻结构，特别是作为戴德金整环（Dedekind domain）的[理想分解](@entry_id:148948)理论及其与唯一因子分解的关联。

### 基本定义：[代数数](@entry_id:150888)与[代数整数](@entry_id:151672)

在数论的研究中，我们常常需要将研究范围从有理数域 $\mathbb{Q}$ 拓展到更广阔的代数领域。这一拓展的核心是**代数数 (algebraic number)** 的概念。

一个复数 $\alpha \in \mathbb{C}$ 被称为**[代数数](@entry_id:150888)**，如果它是有理数域 $\mathbb{Q}$ 上某个非零多项式 $f(x) \in \mathbb{Q}[x]$ 的根，即 $f(\alpha)=0$ [@problem_id:3007366]。不是[代数数](@entry_id:150888)的复数被称为**超越数 (transcendental number)**。$\pi$ 和 $e$ 是两个著名的[超越数](@entry_id:154911)。

这个定义有一个等价且在实践中非常方便的表述：一个复数 $\alpha$ 是代数数，当且仅当它是某个非零整系数多项式 $g(x) \in \mathbb{Z}[x]$ 的根 [@problem_id:3007366]。这一等价性很容易证明。如果 $g(x) \in \mathbb{Z}[x]$，那么它自然也是 $\mathbb{Q}[x]$ 中的多项式。反之，如果 $\alpha$ 是 $f(x) \in \mathbb{Q}[x]$ 的根，我们可以将 $f(x)$ 的所有有理系数通分，乘以系数分母的[最小公倍数](@entry_id:140942) $L$，得到一个整系数多项式 $g(x)=L \cdot f(x)$，它显然仍以 $\alpha$ 为根。

根据这个定义，所有有理数 $r \in \mathbb{Q}$ 都是代数数。因为对于任意有理数 $r = a/b$（其中 $a,b \in \mathbb{Z}, b \neq 0$），它都是一次整系数多项式 $f(x) = bx-a$ 的根 [@problem_id:3007366]。

对于任何一个[代数数](@entry_id:150888) $\alpha$，在所有以 $\alpha$ 为根的、首项系数为 $1$ 的有理系数多项式中，存在一个次数最小的，我们称之为 $\alpha$ 在 $\mathbb{Q}$ 上的**最小多项式 (minimal polynomial)**，记作 $m_{\alpha}(x)$。最小多项式在 $\mathbb{Q}[x]$ 上是不可约的，并且是唯一的。[代数数](@entry_id:150888) $\alpha$ 的**次数 (degree)** 定义为其[最小多项式](@entry_id:153598)的次数。

例如，$\alpha = \sqrt{7}$ 是多项式 $x^2 - 7 = 0$ 的根。根据艾森斯坦判别法（Eisenstein's Criterion），取素数 $p=7$，由于 $7$ 整除常数项 $-7$ 但不整除首项系数 $1$，且 $7^2=49$ 不整除 $-7$，因此 $x^2-7$ 在 $\mathbb{Q}$ 上不可约。所以，$m_{\sqrt{7}}(x) = x^2-7$，$\sqrt{7}$ 是一个二次代数数 [@problem_id:3007346]。同理，$\beta = \sqrt[3]{19}$ 是 $x^3-19=0$ 的根，同样利用艾森斯坦判别法（取 $p=19$），可知其[最小多项式](@entry_id:153598)为 $m_{\sqrt[3]{19}}(x) = x^3-19$，它是一个三次代数数 [@problem_id:3007346]。

在代数数的集合中，有一类特殊的数，它们的性质与整数 $\mathbb{Z}$ 更为接近，这就是**[代数整数](@entry_id:151672) (algebraic integer)**。

一个复数 $\alpha \in \mathbb{C}$ 被称为**[代数整数](@entry_id:151672)**，如果它是某个首一（monic）整系数多项式 $h(x) \in \mathbb{Z}[x]$ 的根 [@problem_id:3007366]。[首一多项式](@entry_id:152311)是指其最高次项系数为 $1$。

显然，所有[代数整数](@entry_id:151672)都是代数数，但反之不成立。例如，我们已经知道有理数 $1/2$ 是[代数数](@entry_id:150888)，但它不是[代数整数](@entry_id:151672)。假如 $1/2$ 是某个首一整系数多项式 $x^n + c_{n-1}x^{n-1} + \dots + c_0 = 0$ 的根，根据[有理根定理](@entry_id:150684)，任何有理根 $p/q$（最简形式）必须满足分母 $q$ 整除首项系数 $1$。对于 $1/2$，$q=2$，但 $2$ 并不整除 $1$，因此 $1/2$ 不可能是任何首一整系数[多项式的根](@entry_id:154615)。

这个例子揭示了一个基本而重要的事实：一个有理数是[代数整数](@entry_id:151672)当且仅当它是一个普通的整数 [@problem_id:1805222] [@problem_id:3007378]。换言之，[代数整数](@entry_id:151672)的概念是对整数 $\mathbb{Z}$ 在[代数数域](@entry_id:637592)中的自然推广，而 $\mathbb{Q}$ 与[代数整数](@entry_id:151672)的交集恰好就是 $\mathbb{Z}$。

### [代数数](@entry_id:150888)与[代数整数](@entry_id:151672)的集合结构

[代数数](@entry_id:150888)和[代数整数](@entry_id:151672)并非散乱的个体，它们各自构成了具有良好[代数结构](@entry_id:137052)的集合。

所有[代数数](@entry_id:150888)的集合，通常记为 $\overline{\mathbb{Q}}$，构成一个**域 (field)**。这意味着任意两个[代数数](@entry_id:150888)的和、差、积、商（除数非零）仍然是[代数数](@entry_id:150888) [@problem_id:3007378]。虽然证明这一事实需要更高等的[域论](@entry_id:155241)工具，但其核心思想是，如果 $\alpha$ 和 $\beta$ 是[代数数](@entry_id:150888)，则[域扩张](@entry_id:153187) $\mathbb{Q}(\alpha, \beta)$ 是 $\mathbb{Q}$ 的一个有限次扩张，而有限次扩张中的任何元素都是代数数。由于 $\alpha+\beta$ 和 $\alpha\beta$ 都属于 $\mathbb{Q}(\alpha, \beta)$，因此它们也都是代数数。特别地，如果 $\alpha \neq 0$ 是一个[代数数](@entry_id:150888)，其最小多项式为 $c_n x^n + \dots + c_1 x + c_0 = 0$（其中 $c_0 \neq 0$），那么它的倒数 $\alpha^{-1}$ 是多项式 $c_0 y^n + c_1 y^{n-1} + \dots + c_n = 0$ 的根，因此 $\alpha^{-1}$ 也是代数数 [@problem_id:3007366]。

所有[代数整数](@entry_id:151672)的集合则构成一个**环 (ring)**，但不构成域。这意味着任意两个[代数整数](@entry_id:151672)的和、差、积仍然是[代数整数](@entry_id:151672)。例如，$1/2$ 是代数数但非[代数整数](@entry_id:151672)，这说明[代数整数](@entry_id:151672)环不是一个域，因为它不包含所有元素的乘法[逆元](@entry_id:140790)。

从集合论的角度看，代数数的集合是**可数 (countable)** 的。我们可以通过计算所有整系数多项式的数量来证明这一点。对于任意给定的次数 $n$，次数为 $n$ 的整系数多项式可以由其 $n+1$ 个整数系数唯一确定，因此这样的多项式集合是可数的（如同 $\mathbb{Z}^{n+1}$）。所有整系数多项式的集合是这些可数集的、可数个并集，因此它本身也是可数的。由于每个多项式只有有限个根，所有[代数数](@entry_id:150888)的集合是可数个有限集的并集，故而是可数的 [@problem_id:3007366]。这也意味着，虽然[超越数](@entry_id:154911)看起来很稀有，但它们实际上比代数数“多得多”，因为复数集 $\mathbb{C}$ 是不可数的。

### 数域及其[整数环](@entry_id:181003)

在实践中，我们通常不是在整个 $\overline{\mathbb{Q}}$ 中工作，而是在其子域中进行研究。一个**[数域](@entry_id:155558) (number field)** $K$ 是 $\mathbb{Q}$ 的一个有限次[域扩张](@entry_id:153187)。根据定义，数域中的每个元素都是代数数。

对于一个[数域](@entry_id:155558) $K$，我们最关心的是其中表现得像“整数”的元素。这引出了**[整数环](@entry_id:181003) (ring of integers)** 的概念。数域 $K$ 的整数环，记作 $\mathcal{O}_K$，定义为 $K$ 中所有[代数整数](@entry_id:151672)的集合。即，$\mathcal{O}_K = K \cap \{\text{所有代数整数}\}$。

例如，对于高斯有理[数域](@entry_id:155558) $K = \mathbb{Q}(i)$，其[整数环](@entry_id:181003)是[高斯整数环](@entry_id:149594) $\mathcal{O}_K = \mathbb{Z}[i] = \{a+bi \mid a,b \in \mathbb{Z}\}$。

[整数环](@entry_id:181003) $\mathcal{O}_K$ 在 $K$ 中的地位，等同于 $\mathbb{Z}$ 在 $\mathbb{Q}$ 中的地位。这个类比可以通过**整性 (integrality)** 的概念精确化。给定环的扩张 $A \subseteq B$，一个元素 $b \in B$ 被称为在 $A$ 上是**整的 (integral over A)**，如果它是某个以 $A$ 中元素为系数的[首一多项式](@entry_id:152311)的根。在 $A$ 上整的所有 $B$ 中元素的集合称为 $A$ 在 $B$ 中的**[整闭](@entry_id:149392)包 (integral closure)**。

根据这个定义，$\mathcal{O}_K$ 正是 $\mathbb{Z}$ 在 $K$ 中的[整闭](@entry_id:149392)包 [@problem_id:3007367]。这是一个基本而深刻的性质，它表明 $\mathcal{O}_K$ 是从 $\mathbb{Z}$ 到 $K$ 的最自然的“整数”延伸。需要注意的是，$\mathcal{O}_K$ 不是 $\mathbb{Q}$ 在 $K$ 中的[整闭](@entry_id:149392)包；由于 $K$ 中的每个元素都以其在 $\mathbb{Q}$ 上的[最小多项式](@entry_id:153598)为根（该多项式是首一的），所以 $\mathbb{Q}$ 在 $K$ 中的[整闭](@entry_id:149392)包就是 $K$ 本身 [@problem_id:3007367]。

$\mathcal{O}_K$ 自身也具有一个重要的[闭包性质](@entry_id:136899)：它是**[整闭](@entry_id:149392)的 (integrally closed)**。这意味着，如果 $K$ 中某个元素在 $\mathcal{O}_K$ 上是整的，那么它必然已经属于 $\mathcal{O}_K$ [@problem_id:3007367]。这个性质源于整性的传递性：$\mathbb{Z} \subseteq \mathcal{O}_K \subseteq K$，如果 $x$ 在 $\mathcal{O}_K$ 上整，而 $\mathcal{O}_K$ 的所有元素在 $\mathbb{Z}$ 上整，那么 $x$ 也在 $\mathbb{Z}$ 上整。

判断一个代数数 $\alpha$ 是否为[代数整数](@entry_id:151672)，有几个等价的判别方法，它们在理论和计算中都极为重要：
1.  **定义法**：$\alpha$ 是某个首一整系数[多项式的根](@entry_id:154615)。
2.  **[最小多项式](@entry_id:153598)法**：$\alpha$ 的[最小多项式](@entry_id:153598) $m_\alpha(x)$ 的所有系数都是整数，即 $m_\alpha(x) \in \mathbb{Z}[x]$ [@problem_id:3007378]。这是最实用的判别法之一。其正确性源于[高斯引理](@entry_id:149771)（Gauss's Lemma），它保证了如果一个首一整系数多项式在 $\mathbb{Q}[x]$ 中分解，那么其因子（调整为首一后）也都在 $\mathbb{Z}[x]$ 中。
3.  **[模论](@entry_id:139410)法**：包含 $\alpha$ 的环 $\mathbb{Z}[\alpha]$ 是一个[有限生成](@entry_id:156447)的 $\mathbb{Z}$-模（finitely generated $\mathbb{Z}$-module） [@problem_id:3007378]。这个更抽象的判别法在证明[代数整数](@entry_id:151672)环的[闭包性质](@entry_id:136899)时非常强大。

### 数域及其元素的[不变量](@entry_id:148850)

为了更深入地理解数域的结构，我们需要一些“测量”它的工具，这些工具在域的自同构下保持不变，故称为[不变量](@entry_id:148850)。

对于一个次数为 $n=[K:\mathbb{Q}]$ 的[数域](@entry_id:155558) $K$，存在恰好 $n$ 个不同的**域嵌入 (field embedding)** $\sigma: K \hookrightarrow \mathbb{C}$。这些嵌入是保持 $\mathbb{Q}$ 中元素不变的[域同态](@entry_id:155269)。每个嵌入 $\sigma$ 由它如何映射 $K$ 的生成元唯一确定。如果 $\alpha \in K$ 是多项式 $f(x) \in \mathbb{Q}[x]$ 的一个根，那么 $\sigma(\alpha)$ 必定是 $f(x)$ 的另一个根。

这些嵌入分为两类：如果一个嵌入 $\sigma$ 的像 $\sigma(K)$ 完全落在实数轴 $\mathbb{R}$ 内，则称其为**实嵌入 (real embedding)**；否则称为**[复嵌入](@entry_id:189961) (complex embedding)**。[复嵌入](@entry_id:189961)总是成对出现：如果 $\sigma$ 是一个[复嵌入](@entry_id:189961)，那么它的复共轭 $\overline{\sigma}$（定义为 $\overline{\sigma}(x) = \overline{\sigma(x)}$）是另一个不同的[复嵌入](@entry_id:189961)。数域 $K$ 的**符号差 (signature)** 是一个数对 $(r_1, r_2)$，其中 $r_1$ 是实嵌入的数量，$r_2$ 是共轭[复嵌入](@entry_id:189961)的对数。它们满足基本关系 $n = r_1 + 2r_2$ [@problem_id:3007357]。

例如，考虑[数域](@entry_id:155558) $K=\mathbb{Q}(\sqrt{5}, \sqrt[3]{2})$。其次数为 $[\mathbb{Q}(\sqrt{5}):\mathbb{Q}] \cdot [\mathbb{Q}(\sqrt[3]{2}):\mathbb{Q}]=2 \cdot 3=6$。一个嵌入 $\sigma$ 由 $\sigma(\sqrt{5})$ 和 $\sigma(\sqrt[3]{2})$ 的值决定。$\sigma(\sqrt{5})$ 必须是 $x^2-5=0$ 的根，即 $\pm\sqrt{5}$（两个实数）。$\sigma(\sqrt[3]{2})$ 必须是 $x^3-2=0$ 的根，即 $\sqrt[3]{2}$（一个实数）和 $\sqrt[3]{2}\omega, \sqrt[3]{2}\omega^2$（两个共轭复数，其中 $\omega=e^{i2\pi/3}$）。一个嵌入是实的，当且仅当它将所有生成元映射到实数。因此，$\sigma(\sqrt{5})$ 有 2 个实数选择，而 $\sigma(\sqrt[3]{2})$ 只有 1 个实数选择。故实嵌入的数量 $r_1 = 2 \times 1 = 2$。根据 $6 = 2 + 2r_2$，我们得到 $r_2=2$。所以 $K$ 的符号差是 $(2,2)$ [@problem_id:3007357]。

利用嵌入，我们可以为数域中的每个元素定义两个重要的[不变量](@entry_id:148850)：**迹 (trace)** 和**范数 (norm)**。对于 $\alpha \in K$，其[迹和范数](@entry_id:155207)定义为：
$$ \mathrm{Tr}_{K/\mathbb{Q}}(\alpha) = \sum_{i=1}^n \sigma_i(\alpha) \quad \text{和} \quad \mathrm{N}_{K/\mathbb{Q}}(\alpha) = \prod_{i=1}^n \sigma_i(\alpha) $$
例如，在二次域 $K=\mathbb{Q}(\sqrt{d})$（$d$ 为无平方因子的整数）中，存在两个嵌入：恒等嵌入 $\sigma_1(\sqrt{d}) = \sqrt{d}$ 和共轭嵌入 $\sigma_2(\sqrt{d}) = -\sqrt{d}$。对于元素 $\alpha = a+b\sqrt{d}$（$a,b \in \mathbb{Q}$），其[迹和范数](@entry_id:155207)为：
$$ \mathrm{Tr}_{K/\mathbb{Q}}(\alpha) = (a+b\sqrt{d}) + (a-b\sqrt{d}) = 2a $$
$$ \mathrm{N}_{K/\mathbb{Q}}(\alpha) = (a+b\sqrt{d})(a-b\sqrt{d}) = a^2 - b^2d $$
[@problem_id:3007391]

[迹和范数](@entry_id:155207)都是从 $K$ 到 $\mathbb{Q}$ 的映射。一个关键性质是，如果 $\alpha \in \mathcal{O}_K$ 是一个[代数整数](@entry_id:151672)，那么它的迹 $\mathrm{Tr}_{K/\mathbb{Q}}(\alpha)$ 和范数 $\mathrm{N}_{K/\mathbb{Q}}(\alpha)$ 都是普通的整数 $\mathbb{Z}$。这是因为它们（除去一个符号）分别是 $\alpha$ 的特征多项式的次高项系数和常数项，而对于[代数整数](@entry_id:151672)，[特征多项式](@entry_id:150909)是整系数的。然而，反之不成立：[迹和范数](@entry_id:155207)都是整数的元素不一定是[代数整数](@entry_id:151672) [@problem_id:3007378]。

范数具有重要的**乘法性质**：$\mathrm{N}_{K/\mathbb{Q}}(\alpha\beta) = \mathrm{N}_{K/\mathbb{Q}}(\alpha) \mathrm{N}_{K/\mathbb{Q}}(\beta)$。这可以直接从定义和嵌入的乘法性质推导出来 [@problem_id:3007391]。范数还与最小多项式密切相关。如果 $\alpha$ 的[最小多项式](@entry_id:153598)是 $m_\alpha(x) = x^k + \dots + a_0$，那么 $\mathrm{N}_{\mathbb{Q}(\alpha)/\mathbb{Q}}(\alpha) = (-1)^k a_0$。这为计算范数提供了另一条途径 [@problem_id:3007346]。

### 整数[环的结构](@entry_id:150907)

[整数环](@entry_id:181003) $\mathcal{O}_K$ 是[代数数论](@entry_id:148067)的核心研究对象。它的结构远比 $\mathbb{Z}$ 复杂。

作为一个[加法群](@entry_id:151801)，$\mathcal{O}_K$ 总是一个秩为 $n=[K:\mathbb{Q}]$ 的自由 $\mathbb{Z}$-模。这意味着存在一个由 $n$ 个元素组成的**[整基](@entry_id:190217) (integral basis)** $\{\omega_1, \dots, \omega_n\}$，使得 $\mathcal{O}_K$ 中的每个元素都可以唯一地表示为它们的整线性组合。

对于二次域 $K=\mathbb{Q}(\sqrt{d})$（$d$ 为无平方因子的整数），整数环 $\mathcal{O}_K$ 的结构取决于 $d$ 模 $4$ 的余数 [@problem_id:3007381]：
- 如果 $d \equiv 2$ 或 $3 \pmod{4}$，则 $\mathcal{O}_K = \mathbb{Z}[\sqrt{d}] = \{a+b\sqrt{d} \mid a,b \in \mathbb{Z}\}$。[整基](@entry_id:190217)是 $\{1, \sqrt{d}\}$。
- 如果 $d \equiv 1 \pmod{4}$，则 $\mathcal{O}_K = \mathbb{Z}\left[\frac{1+\sqrt{d}}{2}\right] = \left\{a+b\frac{1+\sqrt{d}}{2} \mid a,b \in \mathbb{Z}\right\}$。[整基](@entry_id:190217)是 $\{1, \frac{1+\sqrt{d}}{2}\}$。

这表明，像 $\mathbb{Z}[\sqrt{d}]$ 这样的环，虽然总是 $\mathcal{O}_K$ 的一个[子环](@entry_id:154194)（称为一个**序 (order)**），但并不总是等于 $\mathcal{O}_K$。例如，在 $K=\mathbb{Q}(\sqrt{5})$ 中，$d=5 \equiv 1 \pmod 4$，所以 $\mathcal{O}_K = \mathbb{Z}[\frac{1+\sqrt{5}}{2}]$，而 $\mathbb{Z}[\sqrt{5}]$ 只是它的一个[子环](@entry_id:154194)。[子环](@entry_id:154194) $\mathbb{Z}[\sqrt{d}]$ 在 $\mathcal{O}_K$ 中的**指数 (index)** $[\mathcal{O}_K : \mathbb{Z}[\sqrt{d}]]$ 要么是 $1$（当 $d \equiv 2,3 \pmod 4$），要么是 $2$（当 $d \equiv 1 \pmod 4$）[@problem_id:3007381]。

[整数环](@entry_id:181003) $\mathcal{O}_K$ 最重要的性质之一是，它总是一个**戴德金整环 (Dedekind domain)**。戴德金整环的一个核心特征是，虽然其中元素的唯一[因子分解](@entry_id:150389)可能不成立（即 $\mathcal{O}_K$ 可能不是一个[唯一分解整环](@entry_id:155710) UFD），但它的**理想 (ideals)** 总能唯一地分解为**素理想 (prime ideals)** 的乘积 [@problem_id:3007356]。

这一[理想的唯一分解](@entry_id:154997)性质在很大程度上弥补了元素[唯一分解](@entry_id:152313)的缺失。例如，在 $\mathbb{Z}[\sqrt{-5}]$ 中，$6$ 有两种不同的元素分解：$6 = 2 \cdot 3 = (1+\sqrt{-5})(1-\sqrt{-5})$。但作为理想，$(6)$ 的分解是唯一的：$(6) = (2, 1+\sqrt{-5})^2 (3, 1+\sqrt{-5})(3, 1-\sqrt{-5})$。

为了“测量” $\mathcal{O}_K$ 离一个 UFD 有多远，我们引入了**理想类群 (ideal class group)** $\mathrm{Cl}_K$。它由 $\mathcal{O}_K$ 的**分式理想 (fractional ideals)** 构成。非零分式理想群 $I_K$ 对其[子群](@entry_id:146164)——**主分式理想 (principal fractional ideals)** $P_K$ 的[商群](@entry_id:145113)，就是理想类群 $\mathrm{Cl}_K = I_K/P_K$ [@problem_id:3007356]。[理想类群](@entry_id:153974)中的每个元素代表一类在某种意义上“等价”的理想。

理想类群是平凡群（只包含单位元）当且仅当所有理想都是[主理想](@entry_id:152760)。对于戴德金[整环](@entry_id:155321)，这个条件等价于它是 UFD。因此，$\mathcal{O}_K$ 是[唯一分解整环](@entry_id:155710)当且仅当其理想类群 $\mathrm{Cl}_K$ 是平凡的 [@problem_id:3007356]。[理想类群](@entry_id:153974)的大小（称为**[类数](@entry_id:156164) (class number)**）量化了元素唯一分解失败的程度。一个深刻的结果是，任何[数域](@entry_id:155558)的理想类群都是有限群。

最后，[理想的唯一分解](@entry_id:154997)理论也让我们能够精确描述有理素数 $p \in \mathbb{Z}$ 在 $\mathcal{O}_K$ 中的行为。当我们将 $p$ 视为 $\mathcal{O}_K$ 中的理想 $p\mathcal{O}_K$ 时，它会分解为素理想的乘积：$p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_g^{e_g}$。这里的指数 $e_i$ 称为**[分歧指数](@entry_id:186386) (ramification index)**，而[商环](@entry_id:148632) $\mathcal{O}_K/\mathfrak{p}_i$ 作为 $\mathbb{Z}/p\mathbb{Z}$ 的扩张次数 $f_i = [\mathcal{O}_K/\mathfrak{p}_i : \mathbb{Z}/p\mathbb{Z}]$ 称为**惯性指数 (inertia degree)**。这些[不变量](@entry_id:148850)满足一个基本恒等式 $\sum_{i=1}^g e_i f_i = [K:\mathbb{Q}]$，它将[数域](@entry_id:155558)的全局次数与素数在其中的局部行为联系起来 [@problem_id:3007355]。这一分解理论是现代数论的基石之一。