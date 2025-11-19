## 引言
在代数数论的宏伟画卷中，[数域](@entry_id:155558)构成了研究的核心对象。作为有理[数域](@entry_id:155558) $\mathbb{Q}$ 的[有限扩张](@entry_id:152412)，数域展现了远比我们熟悉的整数更为丰富和复杂的算术规律。然而，如何量化和理解这些抽象域的结构与复杂性呢？答案始于一个看似简单的概念：[数域](@entry_id:155558)的 **次数 (degree)**。这个[数值不变量](@entry_id:752800)不仅衡量了域相对于 $\mathbb{Q}$ 的“大小”，更深刻地支配着其内部的代数与算术行为。本文旨在系统地揭示[数域](@entry_id:155558)次数的中心地位，解决的核心问题是：这个基本的[不变量](@entry_id:148850)是如何定义、计算，并最终决定一个数域的内在结构的？

为了全面解答这一问题，我们将分三个章节展开探讨。在“**原理与机制**”中，我们将从第一性原理出发，精确定义数域及其次数，介绍计算次数的强大工具——塔律，并揭示次数与域嵌入、符号差、判别式等关键[不变量](@entry_id:148850)之间的紧密联系。接下来，在“**应用与跨学科联系**”中，我们将见证这些理论原理的威力，探索次数如何在伽罗瓦理论、[素理想分解](@entry_id:197179)、[单位群](@entry_id:184012)结构乃至经典几何问题中扮演着决定性角色。最后，在“**动手实践**”部分，读者将通过解决一系列精心设计的问题，将理论知识转化为具体的计算和分析能力。通过这一趟旅程，你将深刻理解为何域扩张次数是通往现代数论殿堂的基石。

## 原理与机制

继前一章对数域这一研究对象的初步介绍之后，本章将深入探讨其内在的结构性原理与机制。代数数论的核心目标之一是理解有理[数域](@entry_id:155558) $\mathbb{Q}$ 的[有限扩张](@entry_id:152412)（即[数域](@entry_id:155558)）中的算术规律。我们将看到，一个[数域](@entry_id:155558)最基本的[数值不变量](@entry_id:752800)——它的**次数 (degree)**——扮演了核心的支配角色。本章将系统地阐述数域的次数是如何定义的，它如何通过塔律（Tower Law）来刻画域的层次结构，以及它如何与域的嵌入（embeddings）、符号差（signature）和[判别式](@entry_id:174614)（discriminant）等关键[不变量](@entry_id:148850)紧密相连。最终，我们将揭示这些[不变量](@entry_id:148850)如何共同决定了[数域](@entry_id:155558)中素数的分解行为和单位群的结构，这些都是[数域](@entry_id:155558)算术研究的基石。

### 数域及其次数的定义

根据定义，一个**[数域](@entry_id:155558) (number field)** $K$ 是有理数域 $\mathbb{Q}$ 的一个[有限域](@entry_id:142106)扩张。这意味着 $K$ 本身是一个包含 $\mathbb{Q}$ 的域，并且当将 $K$ 视为一个在 $\mathbb{Q}$ 上的[向量空间](@entry_id:151108)时，它的维数是有限的。这个维数被称为扩张的**次数 (degree)**，记作 $[K:\mathbb{Q}]$。因此，一个域 $K \supseteq \mathbb{Q}$ 是数域，当且仅当 $[K:\mathbb{Q}] < \infty$ [@problem_id:3019989]。

在[数域](@entry_id:155558) $K$ 中的每一个元素 $\alpha$ 都是**[代数数](@entry_id:150888) (algebraic number)**，即它是某个以有理数为系数的非零多项式的根。在所有以 $\alpha$ 为根的有理系数多项式中，存在唯一一个首一（monic，即最高次项系数为1）且次数最小的多项式，我们称之为 $\alpha$ 在 $\mathbb{Q}$ 上的**极小多项式 (minimal polynomial)**，记作 $m_{\alpha}(x)$。这个多项式在 $\mathbb{Q}[x]$（即有理系数[多项式环](@entry_id:152854)）中是不可约的。

一个[数域](@entry_id:155558)最简单的构造方式是通过添加单个[代数数](@entry_id:150888) $\alpha$ 到 $\mathbb{Q}$ 中生成的域，记作 $\mathbb{Q}(\alpha)$。这样的域被称为**[单扩张](@entry_id:152948) (simple extension)**。对于[单扩张](@entry_id:152948)，其次数由生成元 $\alpha$ 的极小多项式的次数唯一确定，即 $[ \mathbb{Q}(\alpha) : \mathbb{Q} ] = \deg(m_{\alpha}(x))$。$\mathbb{Q}(\alpha)$ 作为 $\mathbb{Q}$-[向量空间](@entry_id:151108)的一组**基 (basis)** 可以由 $\alpha$ 的幂次给出：$\{1, \alpha, \alpha^2, \dots, \alpha^{n-1}\}$，其中 $n = \deg(m_{\alpha}(x))$。

值得注意的是，一个[数域](@entry_id:155558)可以由不同的元素生成，但其次数是唯一确定的。考虑一个例子 [@problem_id:3019977]，令 $\theta = \sqrt[3]{2}$，我们知道它的极小多项式是 $x^3-2$，因此 $[\mathbb{Q}(\theta):\mathbb{Q}]=3$。现在考虑元素 $\alpha = \sqrt[3]{2} + \sqrt[3]{4} = \theta + \theta^2$。显然，由于 $\theta$ 和 $\theta^2$ 都在 $\mathbb{Q}(\theta)$ 中，它们的和 $\alpha$ 也必然在 $\mathbb{Q}(\theta)$ 中，这意味着 $\mathbb{Q}(\alpha) \subseteq \mathbb{Q}(\theta)$。反过来，我们能否用 $\alpha$ 表示 $\theta$ 呢？通过计算：
$\alpha^2 = (\theta + \theta^2)^2 = \theta^2 + 2\theta^3 + \theta^4 = \theta^2 + 2(2) + 2\theta = 4 + 2\theta + \theta^2$。
于是我们得到一个关于 $\theta$ 的[线性方程](@entry_id:151487)：
$\alpha^2 - \alpha = (4 + 2\theta + \theta^2) - (\theta + \theta^2) = 4 + \theta$。
由此解出 $\theta = \alpha^2 - \alpha - 4$。这表明 $\theta \in \mathbb{Q}(\alpha)$，因此 $\mathbb{Q}(\theta) \subseteq \mathbb{Q}(\alpha)$。结合两个方向的包含关系，我们得出结论 $\mathbb{Q}(\alpha) = \mathbb{Q}(\theta)$。因此，$[\mathbb{Q}(\alpha):\mathbb{Q}]=[\mathbb{Q}(\theta):\mathbb{Q}]=3$。通过进一步的计算，可以发现 $\alpha$ 的极小多项式是 $m_{\alpha}(x) = x^3 - 6x - 6$。这个例子说明，域的次数是域本身的内在属性，不依赖于其特定的生成元。

### [域扩张](@entry_id:153187)的结构：基与塔律

域的次数作为[向量空间](@entry_id:151108)的维度，其核心意义在于它等于域的任何一组基的元素个数。正如线性代数中一样，一个[向量空间的基](@entry_id:191509)不是唯一的，但所有基的基数（元素个数）是相同的。这个原理在[域扩张](@entry_id:153187)中同样适用。

让我们通过一个具体的例子来理解这一点 [@problem_id:3020015]。考虑域 $K = \mathbb{Q}(\sqrt{2})$ 和 $L = \mathbb{Q}(\sqrt{2}, \sqrt{3})$。我们可以将 $L$ 视为 $K$ 的扩张，记作 $L = K(\sqrt{3})$。首先，我们需要证明 $\sqrt{3} \notin K$。若 $\sqrt{3} \in K$，则存在有理数 $a, b \in \mathbb{Q}$ 使得 $\sqrt{3} = a + b\sqrt{2}$。两边平方得到 $3 = (a^2 + 2b^2) + 2ab\sqrt{2}$。由于 $\sqrt{2}$ 是无理数，这要求 $2ab=0$ 且 $a^2+2b^2=3$。若 $a=0$，则 $2b^2=3$， $b^2=3/2$， $b$ 不是有理数；若 $b=0$，则 $a^2=3$，$a$ 不是有理数。两种情况都产生矛盾，因此 $\sqrt{3} \notin K$。

因为 $\sqrt{3}$ 是 $K$ 上二次多项式 $x^2-3=0$ 的根，且 $\sqrt{3} \notin K$，所以 $\sqrt{3}$ 在 $K$ 上的极小多项式就是 $x^2-3$。因此，扩张 $L/K$ 的次数为 $[L:K]=2$。这意味着 $L$ 作为 $K$-[向量空间](@entry_id:151108)的一个基是 $\{1, \sqrt{3}\}$。

现在，我们考虑另一个元素 $\sqrt{6}$。由于 $\sqrt{6} = \sqrt{2}\sqrt{3}$，且 $\sqrt{2} \in L, \sqrt{3} \in L$，所以 $\sqrt{6} \in L$。我们可以证明 $L = K(\sqrt{6})$。一方面 $K(\sqrt{6}) \subseteq L$ 是显然的。另一方面，$\sqrt{3} = \sqrt{6}/\sqrt{2} \in K(\sqrt{6})$，所以 $\mathbb{Q}(\sqrt{2}, \sqrt{3}) \subseteq K(\sqrt{6})$。因此 $L = K(\sqrt{6})$。同样可以证明 $\sqrt{6} \notin K$，其在 $K$ 上的极小多项式是 $x^2-6$。因此，$\{1, \sqrt{6}\}$ 也是 $L$ 在 $K$ 上的一组基。这个例子清晰地表明，扩张的基不是唯一的，但所有基的元素个数都是2，这个不变的数就是[扩张的次数](@entry_id:151271)。

这种层次结构可以用**塔律 (Tower Law)** 来精确描述。对于一个[域塔](@entry_id:153606) $F \subseteq K \subseteq L$，其中每次扩张都是有限的，则从 $F$ 到 $L$ 的总次数等于各步扩张次数的乘积：
$$[L:F] = [L:K] \cdot [K:F]$$

我们可以通过构造基来直观地理解这个定律 [@problem_id:3020027]。设 $F=\mathbb{Q}$，$\alpha = \sqrt[4]{2}$，$K = \mathbb{Q}(\alpha)$，以及 $L=K(\mathrm{i})$，其中 $\mathrm{i}^2=-1$。
1.  首先，多项式 $x^4-2$ 在 $\mathbb{Q}$ 上根据艾森斯坦判别法（对于素数 $p=2$）是不可约的。因此 $[K:\mathbb{Q}] = 4$，$K$ 的一组 $\mathbb{Q}$-基是 $\mathcal{B}_{K/\mathbb{Q}} = \{1, \alpha, \alpha^2, \alpha^3\}$。
2.  其次，由于 $K=\mathbb{Q}(\sqrt[4]{2})$ 是 $\mathbb{R}$ 的一个子域，它不包含虚数单位 $\mathrm{i}$。因此多项式 $x^2+1$ 在 $K$ 上是不可约的。所以 $[L:K]=2$，$L$ 的一组 $K$-基是 $\mathcal{B}_{L/K} = \{1, \mathrm{i}\}$。

塔律预测 $[L:\mathbb{Q}] = [L:K] \cdot [K:\mathbb{Q}] = 2 \cdot 4 = 8$。为了验证这一点，我们可以构造 $L$ 的一组 $\mathbb{Q}$-基。这组基可以通过将 $\mathcal{B}_{L/K}$ 的每个元素与 $\mathcal{B}_{K/\mathbb{Q}}$ 的每个元素相乘得到：
$$ \mathcal{B}_{L/\mathbb{Q}} = \{b_k \cdot b_l \mid b_k \in \mathcal{B}_{K/\mathbb{Q}}, b_l \in \mathcal{B}_{L/K} \} = \{1, \alpha, \alpha^2, \alpha^3, \mathrm{i}, \mathrm{i}\alpha, \mathrm{i}\alpha^2, \mathrm{i}\alpha^3 \} $$
这个集合包含 $4 \times 2 = 8$ 个元素。可以证明这个集合在 $\mathbb{Q}$ 上是[线性无关](@entry_id:148207)的。任何 $L$ 中的元素都可以唯一地写成 $u + v\mathrm{i}$ 的形式，其中 $u, v \in K$。而 $u$ 和 $v$ 又可以唯一地写成 $\mathcal{B}_{K/\mathbb{Q}}$ 的 $\mathbb{Q}$-[线性组合](@entry_id:154743)。将这些表达式代入并展开，就证明了 $\mathcal{B}_{L/\mathbb{Q}}$ 确实是 $L$ 的一组 $\mathbb{Q}$-基。因此，$L$ 作为 $\mathbb{Q}$-[向量空间](@entry_id:151108)的维数是8，这与塔律的预测完全一致。

### 嵌入、符号差与[判别式](@entry_id:174614)：关键[不变量](@entry_id:148850)

除了次数，还有其他一些从不同角度刻画[数域](@entry_id:155558)结构的[不变量](@entry_id:148850)，它们都与次数密切相关。

#### 域嵌入与符号差

**原始元素定理 (Primitive Element Theorem)** 保证了任何数域 $K$ 都是一个[单扩张](@entry_id:152948)，即存在某个[代数数](@entry_id:150888) $\alpha$ 使得 $K=\mathbb{Q}(\alpha)$。这意味着我们可以通过研究 $\alpha$ 的性质来理解 $K$。一个关键的视角是考察如何将 $K$ **嵌入 (embed)** 到[复数域](@entry_id:153768) $\mathbb{C}$ 中。

一个从 $K$到 $\mathbb{C}$ 的**域嵌入**是一个[域同态](@entry_id:155269) $\sigma: K \hookrightarrow \mathbb{C}$，它逐点固定 $\mathbb{Q}$（即对所有 $q \in \mathbb{Q}$，有 $\sigma(q)=q$）。这样的嵌入 $\sigma$ 由它对生成元 $\alpha$ 的作用完全决定。设 $m_\alpha(x)$ 是 $\alpha$ 的极小多项式，次数为 $n=[K:\mathbb{Q}]$。对等式 $m_\alpha(\alpha)=0$ 应用 $\sigma$，我们得到 $m_\alpha(\sigma(\alpha)) = \sigma(m_\alpha(\alpha)) = \sigma(0) = 0$。这表明 $\sigma(\alpha)$ 必须是 $m_\alpha(x)$ 在 $\mathbb{C}$ 中的一个根。由于 $\mathbb{Q}$ 的特征为0，其[有限扩张](@entry_id:152412)都是可分的，这意味着 $m_\alpha(x)$ 在 $\mathbb{C}$ 中恰好有 $n$个不同的根。每一个根 $\beta_i$ 都唯一地确定了一个嵌入 $\sigma_i: K \to \mathbb{C}$，该嵌入将 $\alpha$ 映到 $\beta_i$。因此，一个次数为 $n$ 的数域 $K$ 恰好有 $n$ 个不同的到 $\mathbb{C}$ 的嵌入 [@problem_id:3019989]。

这些嵌入的像 $\sigma(K)$ 提供了关于 $K$ 结构的重要信息。如果一个嵌入的像完全落在实数域 $\mathbb{R}$ 中，我们称之为一个**实嵌入 (real embedding)**。否则，称之为**[复嵌入](@entry_id:189961) (complex embedding)**。[复嵌入](@entry_id:189961)总是成对出现：如果 $\sigma$ 是一个[复嵌入](@entry_id:189961)，那么它的复共轭 $\overline{\sigma}$（定义为 $\overline{\sigma}(x) = \overline{\sigma(x)}$）是另一个不同的[复嵌入](@entry_id:189961)。

数域 $K$ 的**符号差 (signature)** 是一个数对 $(r_1, r_2)$，其中 $r_1$ 是实嵌入的数量，$r_2$ 是共轭[复嵌入](@entry_id:189961)的对数。总的嵌入数 $n$ 与符号差之间存在一个基本关系：
$$ n = [K:\mathbb{Q}] = r_1 + 2r_2 $$
符号差由生成元极小[多项式的根](@entry_id:154615)的性质决定。以二次域 $K=\mathbb{Q}(\sqrt{d})$ 为例，其中 $d$ 是一个非1的无平方因子整数 [@problem_id:3019969]。其次数为2，极小多项式为 $x^2-d=0$。两个嵌入由 $\sqrt{d}$ 的两个根 $\pm\sqrt{d}$ 决定。
-   如果 $d > 0$，两个根 $\pm\sqrt{d}$ 都是实数。因此，我们有两个实嵌入，没有[复嵌入](@entry_id:189961)。符号差为 $(r_1, r_2) = (2, 0)$。这样的域称为**全实域 (totally real field)**。
-   如果 $d  0$，两个根 $\pm\sqrt{d} = \pm i\sqrt{|d|}$ 都是纯虚数。因此，我们没有实嵌入，只有一对共轭的[复嵌入](@entry_id:189961)。符号差为 $(r_1, r_2) = (0, 1)$。这样的域称为**全虚域 (totally imaginary field)**。

#### [判别式](@entry_id:174614)

**判别式 (discriminant)** 是另一个与次数和嵌入密切相关的[不变量](@entry_id:148850)，它衡量了[数域](@entry_id:155558)中整数环的“密度”。对于[数域](@entry_id:155558) $K$ 的整数环 $\mathcal{O}_K$ 的任意一组 $\mathbb{Z}$-基 $\{b_1, \dots, b_n\}$，其[判别式](@entry_id:174614)定义为：
$$ \operatorname{disc}(b_1, \dots, b_n) = \left(\det\left(\sigma_i(b_j)\right)\right)^2 $$
其中 $\sigma_1, \dots, \sigma_n$ 是 $K$ 的 $n$ 个嵌入。可以证明，这个值不依赖于基的选择，因此是[数域](@entry_id:155558) $K$ 的一个[不变量](@entry_id:148850)，称为**[域判别式](@entry_id:198568) (field discriminant)**，记作 $d_K$ 或 $\operatorname{Disc}(K)$。

在实际计算中，直接找到整数环 $\mathcal{O}_K$ 的一组基并计算判别式可能很困难。一个更易于计算的量是与生成元 $\alpha$ 及其极小多项式 $m_\alpha(x)$ 相关联的**[多项式判别式](@entry_id:154854)** $\operatorname{Disc}(m_\alpha)$。这两个判别式之间存在一个非常重要的关系 [@problem_id:3020018]：
$$ \operatorname{Disc}(m_\alpha) = [\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 \cdot \operatorname{Disc}(K) $$
这里，$\mathbb{Z}[\alpha]$ 是由 $\alpha$ 生成的环，它是 $\mathcal{O}_K$ 的一个[子环](@entry_id:154194)（称为一个**序 (order)**）。$[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 是子环 $\mathbb{Z}[\alpha]$ 在 $\mathcal{O}_K$ 中的**指标 (index)**，它是一个正整数。

这个公式揭示了几个关键点：
1.  [域判别式](@entry_id:198568) $d_K$ 整除任何由整代数数 $\alpha$ 生成的序 $\mathbb{Z}[\alpha]$ 的判别式。
2.  当且仅当 $\mathbb{Z}[\alpha]$ 恰好就是 $K$ 的[整数环](@entry_id:181003) $\mathcal{O}_K$（即指标为1）时，[多项式判别式](@entry_id:154854)才等于[域判别式](@entry_id:198568)。这种情况被称为 $\mathcal{O}_K$ 是**单生成的 (monogenic)**。
3.  由于[判别式](@entry_id:174614)都是整数，这个公式提供了一个强大的工具，可以通过计算[多项式判别式](@entry_id:154854)来获得关于[域判别式](@entry_id:198568)的信息，特别是它的素因子。

### 度与[不变量](@entry_id:148850)在域算术中的作用

我们已经定义了数域的次数、符号差和判别式。这些抽象的[不变量](@entry_id:148850)之所以重要，是因为它们深刻地支配着数域内部的算术行为，例如素数的分解和[单位群](@entry_id:184012)的结构。

#### [素理想分解](@entry_id:197179)

当我们将一个有理素数 $p$ 视为[数域](@entry_id:155558) $K$ 的整数环 $\mathcal{O}_K$ 中的元素时，由它生成的理想 $p\mathcal{O}_K$ 通常不再是[素理想](@entry_id:154026)。它会分解成 $\mathcal{O}_K$ 中一系列[素理想](@entry_id:154026)的乘积：
$$ p\mathcal{O}_K = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_g^{e_g} $$
其中 $\mathfrak{p}_i$ 是 $\mathcal{O}_K$ 中不同的[素理想](@entry_id:154026)，它们都“位于” $p$ 之上（即 $\mathfrak{p}_i \cap \mathbb{Z} = (p)$）。
-   $e_i$ 称为**[分歧指数](@entry_id:186386) (ramification index)**。如果某个 $e_i  1$，我们说素数 $p$ 在 $K$ 中是**分歧的 (ramified)**。
-   每个商环 $\mathcal{O}_K / \mathfrak{p}_i$ 都是一个有限域，它是 $\mathbb{Z}/p\mathbb{Z} \cong \mathbb{F}_p$ 的一个扩张。这个[扩张的次数](@entry_id:151271) $f_i = [\mathcal{O}_K/\mathfrak{p}_i : \mathbb{F}_p]$ 称为**惯性指数 (inertia degree)**。

这些指数与域的次数之间存在一个基本的恒等式 [@problem_id:3020021]：
$$ \sum_{i=1}^g e_i f_i = [K:\mathbb{Q}] $$
这个公式是[代数数论](@entry_id:148067)的基石之一。它表明，一个次数为 $n$ 的[数域](@entry_id:155558)，其内部任何一个有理素数的分解方式都受到 $n$ 的严格制约。分解出的[素理想](@entry_id:154026)的个数 $g$、它们的[分歧指数](@entry_id:186386) $e_i$ 和惯性指数 $f_i$ 必须满足这个和为 $n$ 的关系。由此可以立即推断出 $g \le [K:\mathbb{Q}]$。

那么，我们如何具体确定一个给定的素数 $p$ 是如何分解的呢？**[Kummer-Dedekind 定理](@entry_id:196910)**提供了一个强大的计算工具 [@problem_id:3020017]。该定理指出，如果数域 $K = \mathbb{Q}(\alpha)$（其中 $\alpha$ 是一个整[代数数](@entry_id:150888)），并且素数 $p$ 不整除指标 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$，那么 $p\mathcal{O}_K$ 的分解方式与 $\alpha$ 的极小多项式 $m_\alpha(x)$ 在模 $p$ 的[有限域](@entry_id:142106) $\mathbb{F}_p$ 上的因式分解方式完全一致。
具体来说，如果 $m_\alpha(x) \pmod{p}$ 在 $\mathbb{F}_p[x]$ 中分解为：
$$ \overline{m_\alpha}(x) = g_1(x)^{e_1} g_2(x)^{e_2} \cdots g_t(x)^{e_t} $$
其中 $g_i(x)$ 是 $\mathbb{F}_p[x]$ 中互不相同的首一不[可约多项式](@entry_id:148759)，那么 $p\mathcal{O}_K$ 的分解为：
$$ p\mathcal{O}_K = \mathfrak{P}_1^{e_1} \mathfrak{P}_2^{e_2} \cdots \mathfrak{P}_t^{e_t} $$
其中 $\mathfrak{P}_i$ 是由 $(p, \tilde{g}_i(\alpha))$ 生成的素理想（$\tilde{g}_i(x)$ 是 $g_i(x)$ 在 $\mathbb{Z}[x]$ 中的任意一个首一提法）。对于每个 $i$，其[分歧指数](@entry_id:186386)就是 $e_i$，惯性指数 $f_i$ 就是不可约因子 $g_i(x)$ 的次数 $\deg(g_i)$。特别地，如果 $\overline{m_\alpha}(x)$ 在 $\mathbb{F}_p[x]$ 中是无平方因子的（即所有 $e_i=1$），则 $p$ 在 $K$ 中是非[分歧](@entry_id:193119)的。

#### 单位群的结构

[数域](@entry_id:155558)的乘法结构由其**单位群 (group of units)** $\mathcal{O}_K^\times$ 掌控。**[Dirichlet 单位定理](@entry_id:153844)** [@problem_id:3020008] 揭示了这个群的结构，并再次展现了次数和符号差的核心作用。该定理指出，[数域](@entry_id:155558) $K$ 的单位群 $\mathcal{O}_K^\times$ 是一个[有限生成阿贝尔群](@entry_id:156372)，其结构如下：
$$ \mathcal{O}_K^\times \cong \mu_K \times \mathbb{Z}^{r_1 + r_2 - 1} $$
这里，$\mu_K$ 是 $K$ 中所有[单位根](@entry_id:143302)构成的[有限循环群](@entry_id:147298)（ torsion subgroup），$r_1$ 和 $r_2$ 是 $K$ 的符号差。这个公式的精髓在于，单位群的**秩 (rank)**，即其“自由”部分的维度，完全由符号差决定，为 $r_1+r_2-1$。
-   对于二次域 $\mathbb{Q}(\sqrt{d})$ 且 $d0$，符号差为 $(2,0)$，[单位群的秩](@entry_id:150706)为 $2+0-1=1$。
-   对于二次域 $\mathbb{Q}(\sqrt{d})$ 且 $d0$，符号差为 $(0,1)$，[单位群的秩](@entry_id:150706)为 $0+1-1=0$。这意味着单位群是有限的，仅由[单位根](@entry_id:143302)构成。

这个定理的证明依赖于将单位嵌入到一个对数[向量空间](@entry_id:151108)中，并利用几何论证（如闵可夫斯基的[凸体](@entry_id:183909)定理）。它深刻地表明，数域的加法结构（通过整数环 $\mathcal{O}_K$）和乘法结构（通过[单位群](@entry_id:184012) $\mathcal{O}_K^\times$）的复杂度，都最终可以追溯到域的次数和符号差这两个基本[不变量](@entry_id:148850)。

### [不变量](@entry_id:148850)的局限性：同构问题

我们已经看到次数、符号差和判别式是多么强大的[不变量](@entry_id:148850)。一个自然的问题是：这些[不变量](@entry_id:148850)是否能完全确定一个[数域](@entry_id:155558)？换言之，如果两个数域 $K$ 和 $K'$ 具有相同的次数和相同的[判别式](@entry_id:174614)，它们是否必然同构（$K \cong K'$）？

答案出人意料地是否定的。存在着具有相同次数和相同[判别式](@entry_id:174614)的非同构数域。这样的[数域](@entry_id:155558)被称为**算术等价的 (arithmetically equivalent)**，因为它们在许多算术性质上表现得无法区分，例如它们拥有相同的 Dedekind zeta 函数 $\zeta_K(s) = \zeta_{K'}(s)$。

构造这类例子的一个系统性方法来自群论，特别是 **Gassmann 等价**的概念 [@problem_id:3019960]。如果一个[有限群](@entry_id:139710) $G$ 包含两个[子群](@entry_id:146164) $H$ 和 $H'$，它们在 $G$ 中不共轭，但对于 $G$ 的任何一个[共轭类](@entry_id:143916) $C$，都有 $|C \cap H| = |C \cap H'|$，则称 $H$ 和 $H'$ 是 Gassmann 等价的。
如果能找到一个伽罗瓦扩张 $L/\mathbb{Q}$，其伽罗瓦群 $\operatorname{Gal}(L/\mathbb{Q}) \cong G$，那么根据伽罗瓦理论：
-   由于 $H$ 和 $H'$ 不共轭，它们的[不动域](@entry_id:155430) $K=L^H$ 和 $K'=L^{H'}$ 是非同构的。
-   [扩张的次数](@entry_id:151271) $[K:\mathbb{Q}] = [G:H]$ 和 $[K':\mathbb{Q}] = [G:H']$ 是相等的。
-   Gassmann 等价的群论条件保证了域 $K$ 和 $K'$ 是算术等价的，这意味着它们有相同的次数和[判别式](@entry_id:174614)。

具体的例子存在于：
-   群 $G=\mathrm{PSL}_2(\mathbb{F}_7)$（阶为168）中存在两个非共轭但 Gassmann 等价的[子群](@entry_id:146164) $H, H' \cong S_4$（指数为7）。取 $\operatorname{Gal}(L/\mathbb{Q}) \cong G$ 的扩张 $L$，则 $L^H$ 和 $L^{H'}$ 是一对非同构的7次域，但具有相同的[判别式](@entry_id:174614)。
-   群 $G=S_6$ 中存在两个通过[外自同构](@entry_id:198918)相关联的非[共轭子群](@entry_id:140560) $H, H' \cong S_5$（指数为6）。它们也是 Gassmann 等价的。取 $\operatorname{Gal}(L/\mathbb{Q}) \cong S_6$ 的扩张 $L$，则得到一对非同构的6次域，它们具有相同的判别式。

这些例子深刻地表明，尽管次数和判别式是数域的基本[不变量](@entry_id:148850)，它们并不能完全捕捉到[数域](@entry_id:155558)的全部同构信息。数域的分类是一个远比其基本[不变量](@entry_id:148850)所能描述的更为精细和复杂的问题，这也为代数数论的进一步研究开辟了广阔的空间。