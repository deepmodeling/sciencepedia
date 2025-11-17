## 引言
[代数数](@entry_id:150888)域是数论研究的核心对象，它将我们所熟悉的有理数域扩展到一个更广阔、更丰富的算术世界。通过研究[代数方程](@entry_id:272665)的根所生成的[数域](@entry_id:155558)，数学家们得以用全新的代数工具来审视古老的数论问题。然而，这个新世界也带来了挑战：整数最宝贵的性质之一——唯一[因子分解定理](@entry_id:749213)，在代数数域的“整数”中往往不再成立。这一根本性的困境促使19世纪的数学家发展出了一套深刻而优美的理论，不仅解决了问题，还揭示了数之间前所未见的深层联系。

本文将带领读者系统地探索[代数数](@entry_id:150888)域的宏伟结构。我们的旅程将分为三个部分：

首先，在“原理与机制”一章中，我们将从第一性原理出发，构建[代数数](@entry_id:150888)域的理论基石。我们将定义[代数数](@entry_id:150888)、域扩张，并引入数域的“[整数环](@entry_id:181003)”这一核心概念。随后，我们将探讨为何元[素分解](@entry_id:198620)会失效，并见证Richard Dedekind的革命性思想——[理想理论](@entry_id:184127)——如何挽救了[唯一分解](@entry_id:152313)性。我们还将学习衡量算术复杂度的关键工具：判别式、类群和[单位群](@entry_id:184012)。

接下来，在“应用与[交叉](@entry_id:147634)学科联系”一章中，我们将见证这些抽象理论的强大威力。我们将学习如何利用[代数数](@entry_id:150888)域的结构来预测素数的分解行为，以及如何系统性地求解[佩尔方程](@entry_id:136532)等经典的[丢番图方程](@entry_id:148433)。更令人惊奇的是，我们将跨出数论的边界，探索这些思想如何解决了古希腊的几何作图难题，并与[现代密码学](@entry_id:274529)乃至前沿的[拓扑量子计算](@entry_id:138660)产生了意想不到的联系。

最后，通过“动手实践”部分，读者将有机会亲手应用所学知识解决具体问题，从而将理论概念内化为真正的技能，巩固对这一迷人领域的理解。

## 原理与机制

本章旨在深入探讨[代数数](@entry_id:150888)域的核心结构与内在机制。在前一章对[代数数](@entry_id:150888)域进行了初步介绍之后，我们将系统性地剖析其基本属性、关键[不变量](@entry_id:148850)，以及作为代数数论基石的整数环的深刻性质。我们将从最基本的第一性原理出发，逐步揭示数域中元素与[理想分解](@entry_id:148948)的奥秘，并最终阐述其[单位群](@entry_id:184012)的精密结构。

### [代数数](@entry_id:150888)域的基本属性

#### 代数数与极小多项式

我们研究的出发点是有理数域 $\mathbb{Q}$。一个复数 $\alpha$ 如果是某个以有理数为系数的非零多项式 $f(x) \in \mathbb{Q}[x]$ 的根，即 $f(\alpha)=0$，则称 $\alpha$ 为**[代数数](@entry_id:150888)**。例如，$\sqrt{2}$ 是一个代数数，因为它是多项式 $x^2 - 2$ 的根。

对于每一个代数数 $\alpha$，都存在一个唯一的、首一的（即最高次项系数为 $1$）、在 $\mathbb{Q}[x]$ 中次数最小的多项式，它以 $\alpha$ 为根。这个多项式被称为 $\alpha$ 在 $\mathbb{Q}$ 上的**极小多项式** (minimal polynomial)，记作 $m_{\alpha}(x)$。极小多项式具有两个至关重要的性质：它在 $\mathbb{Q}[x]$ 中是**不可约的** (irreducible)，并且任何其他以 $\alpha$ 为根的有理系数多项式 $h(x)$ 都必然能被 $m_{\alpha}(x)$ 整除 [@problem_id:3080456]。

这两个性质的证明是理解代数数结构的关键。唯一性可以通过构造两个次数最小的[首一多项式](@entry_id:152311)之差来证明，该差式多项式的次数更小，从而导出矛盾。不可约性则通过反证法，假设 $m_{\alpha}(x)$ 可以分解为两个次数更低的多项式 $g(x)h(x)$，那么 $g(\alpha)h(\alpha)=0$ 意味着 $g(\alpha)=0$ 或 $h(\alpha)=0$，这与 $m_{\alpha}(x)$ 的次数最小性相矛盾。

#### [域扩张的次数](@entry_id:149430)

将一个或多个代数数添加到有理数域 $\mathbb{Q}$ 中，我们便构造出一个更大的域，称为**[代数数](@entry_id:150888)域** (algebraic number field)。[代数数](@entry_id:150888)域被严格定义为 $\mathbb{Q}$ 的一个**[有限域](@entry_id:142106)扩张** (finite field extension)。这意味着，如果我们将一个数域 $K$ 视为一个以 $\mathbb{Q}$ 为标量域的[向量空间](@entry_id:151108)，那么它的维数是有限的。这个维度被称为扩张的**次数** (degree)，记作 $[K:\mathbb{Q}]$ [@problem_id:3080395]。

例如，考虑域 $K = \mathbb{Q}(\sqrt{2})$，它由所有形如 $a+b\sqrt{2}$（其中 $a,b \in \mathbb{Q}$）的数构成。这个集合构成一个二维的 $\mathbb{Q}$-[向量空间](@entry_id:151108)，其一组基可以是 $\{1, \sqrt{2}\}$。因此，$[K:\mathbb{Q}] = 2$。

如果一个[数域](@entry_id:155558) $K$ 可以由单个[代数数](@entry_id:150888) $\theta$ 生成，即 $K = \mathbb{Q}(\theta)$，这样的 $\theta$ 被称为 $K$ 的一个**[本原元](@entry_id:154321)** (primitive element)。在这种情况下，[扩张的次数](@entry_id:151271)恰好等于 $\theta$ 的极小多项式的次数，即 $[K:\mathbb{Q}] = \deg(m_{\theta}(x))$。一个更复杂的例子是 $L = \mathbb{Q}(\sqrt{2}, \sqrt{3})$。我们可以通过“[域塔](@entry_id:153606)”法则 (tower law) 计算其次数：
$$[\mathbb{Q}(\sqrt{2},\sqrt{3}):\mathbb{Q}] = [\mathbb{Q}(\sqrt{2},\sqrt{3}):\mathbb{Q}(\sqrt{2})] \cdot [\mathbb{Q}(\sqrt{2}):\mathbb{Q}]$$
由于 $\sqrt{2}$ 的极小多项式是 $x^2-2$，所以 $[\mathbb{Q}(\sqrt{2}):\mathbb{Q}]=2$。可以证明 $\sqrt{3}$ 不在 $\mathbb{Q}(\sqrt{2})$ 中，它在 $\mathbb{Q}(\sqrt{2})$ 上的极小多项式仍然是 $x^2-3$，次数为 $2$。因此，$[\mathbb{Q}(\sqrt{2},\sqrt{3}):\mathbb{Q}(\sqrt{2})]=2$。最终得到 $[L:\mathbb{Q}]=2 \cdot 2 = 4$ [@problem_id:3080395]。这个域的一组 $\mathbb{Q}$-基是 $\{1, \sqrt{2}, \sqrt{3}, \sqrt{6}\}$。

#### [有限扩张](@entry_id:152412)与[代数扩张](@entry_id:156472)

一个深刻而基本的结论是：$\mathbb{Q}$ 的任何[有限扩张](@entry_id:152412)都是**[代数扩张](@entry_id:156472)** (algebraic extension)，这意味着扩张中的每一个元素都是代数数。这个结论将[域扩张](@entry_id:153187)的“有限维”这一线性代数概念与“每个元素都满足一个多项式方程”这一代数概念联系起来。

其证明巧妙地运用了[向量空间的基](@entry_id:191509)本原理。设 $K$ 是 $\mathbb{Q}$ 的一个[有限扩张](@entry_id:152412)，且 $[K:\mathbb{Q}]=n$。对 $K$ 中的任意一个元素 $\alpha$，考虑集合 $\{1, \alpha, \alpha^2, \ldots, \alpha^n\}$。这个集合包含 $n+1$ 个元素，而它们都属于一个 $n$ 维的 $\mathbb{Q}$-[向量空间](@entry_id:151108) $K$。根据线性代数的基本定理，一个 $n$ 维空间中任何 $n+1$ 个向量的集合必然是[线性相关](@entry_id:185830)的。因此，存在不全为零的有理数 $q_0, q_1, \ldots, q_n$ 使得：
$$ q_0 \cdot 1 + q_1 \alpha + q_2 \alpha^2 + \cdots + q_n \alpha^n = 0 $$
这恰恰表明 $\alpha$ 是非零多项式 $f(x) = q_0 + q_1 x + \cdots + q_n x^n \in \mathbb{Q}[x]$ 的一个根。因此，$\alpha$ 是一个[代数数](@entry_id:150888) [@problem_id:3080418]。这个证明完美地体现了将[数域](@entry_id:155558)视为[向量空间](@entry_id:151108)的威力。

### 域的[不变量](@entry_id:148850)：迹、范数与[判别式](@entry_id:174614)

为了更深入地研究数域的结构，我们需要引入一些不随特定基的选择而改变的内在量，即[不变量](@entry_id:148850)。

#### 嵌入、迹与范数

设 $K$ 是一个次数为 $n$ 的[数域](@entry_id:155558)。存在 $n$ 个不同的[域同态](@entry_id:155269)（保持域运算的映射），它们将 $K$ 嵌入到复数域 $\mathbb{C}$ 中，记为 $\sigma_1, \sigma_2, \ldots, \sigma_n$。这些**嵌入** (embeddings) 的作用方式是由 $K$ 的[本原元](@entry_id:154321) $\theta$ 的 $n$ 个[复共轭](@entry_id:174690)根决定的。

对于 $K$ 中的任意元素 $\alpha$，它的 $n$ 个**共轭** (conjugates) 就是它在这些嵌入下的像 $\sigma_1(\alpha), \ldots, \sigma_n(\alpha)$。基于这些共轭，我们定义两个核心[不变量](@entry_id:148850)：
- **迹** (Trace): $\mathrm{Tr}_{K/\mathbb{Q}}(\alpha) = \sum_{i=1}^{n} \sigma_i(\alpha)$
- **范数** (Norm): $N_{K/\mathbb{Q}}(\alpha) = \prod_{i=1}^{n} \sigma_i(\alpha)$

迹是线性的，而范数是乘性的。它们的结果总是有理数。例如，在 $K = \mathbb{Q}(\sqrt{2})$ 中，两个嵌入是 $\sigma_1(\sqrt{2})=\sqrt{2}$ 和 $\sigma_2(\sqrt{2})=-\sqrt{2}$。对于元素 $\sqrt{2}$ 本身，我们计算其[迹和范数](@entry_id:155207)如下 [@problem_id:3080393]：
$$ \mathrm{Tr}_{K/\mathbb{Q}}(\sqrt{2}) = \sigma_1(\sqrt{2}) + \sigma_2(\sqrt{2}) = \sqrt{2} + (-\sqrt{2}) = 0 $$
$$ N_{K/\mathbb{Q}}(\sqrt{2}) = \sigma_1(\sqrt{2}) \cdot \sigma_2(\sqrt{2}) = \sqrt{2} \cdot (-\sqrt{2}) = -2 $$

#### [判别式](@entry_id:174614)的定义

判别式是另一个更为精细的[不变量](@entry_id:148850)，它深刻地揭示了[数域](@entry_id:155558)的算术特性。给定 $K$ 的一组 $\mathbb{Q}$-基 $\{\alpha_1, \ldots, \alpha_n\}$，其**判别式** (discriminant) 定义为：
$$ \operatorname{disc}(\alpha_1, \ldots, \alpha_n) = \det\left( \big(\mathrm{Tr}_{K/\mathbb{Q}}(\alpha_i \alpha_j)\big)_{1 \le i,j \le n} \right) $$
这是一个由迹构成的 $n \times n$ 矩阵的行列式。[判别式](@entry_id:174614)还有一个等价且更具启发性的定义，即通过嵌入来表达 [@problem_id:3080435]：
$$ \operatorname{disc}(\alpha_1, \ldots, \alpha_n) = \left( \det\left( \big(\sigma_j(\alpha_i)\big)_{1 \le i,j \le n} \right) \right)^2 $$
这个定义表明，[判别式](@entry_id:174614)是嵌入[矩阵行列式](@entry_id:194066)的平方。这立即揭示了判别式的一个重要性质：它总是一个有理数，并且对于[代数整数](@entry_id:151672)构成的基，它是一个整数。

### [代数整数](@entry_id:151672)环

#### [整数环](@entry_id:181003)与[整基](@entry_id:190217)

在有理数 $\mathbb{Q}$ 中，我们可以区分出子环——整数 $\mathbb{Z}$。类似地，在任意一个[代数数](@entry_id:150888)域 $K$ 中，也存在一个扮演“整数”角色的特殊[子环](@entry_id:154194)。一个[代数数](@entry_id:150888) $\alpha \in K$ 如果是某个首一整系数[多项式的根](@entry_id:154615)，则称其为**[代数整数](@entry_id:151672)** (algebraic integer)。$K$ 中所有[代数整数](@entry_id:151672)的集合构成一个环，称为 $K$ 的**整数环** (ring of integers)，记作 $\mathcal{O}_K$。

整数环 $\mathcal{O}_K$ 是一个秩为 $n=[K:\mathbb{Q}]$ 的自由 $\mathbb{Z}$-模。这意味着存在一组基 $\{\omega_1, \ldots, \omega_n\}$，使得 $\mathcal{O}_K$ 中的任何元素 $\gamma$ 都可以唯一地表示为这些基元素的整系数线性组合：
$$ \gamma = c_1 \omega_1 + c_2 \omega_2 + \cdots + c_n \omega_n, \quad c_i \in \mathbb{Z} $$
这样的一组基被称为 $\mathcal{O}_K$ 的一组**[整基](@entry_id:190217)** (integral basis)。

#### [域判别式](@entry_id:198568)

[整基](@entry_id:190217)的[判别式](@entry_id:174614)是一个不依赖于具体[整基](@entry_id:190217)选择的域[不变量](@entry_id:148850)。如果 $\{\omega_1, \ldots, \omega_n\}$ 和 $\{\omega'_1, \ldots, \omega'_n\}$ 是 $\mathcal{O}_K$ 的两组不同的[整基](@entry_id:190217)，它们之间通过一个[行列式](@entry_id:142978)为 $\pm 1$ 的整[系数矩阵](@entry_id:151473)（属于 $\mathrm{GL}_n(\mathbb{Z})$）进行转换。根据判别式的变换法则，$\operatorname{disc}(\omega'_1, \ldots, \omega'_n) = (\det(C))^2 \operatorname{disc}(\omega_1, \ldots, \omega_n)$, 由于 $(\det(C))^2 = 1$，两组基的[判别式](@entry_id:174614)相等。这个不依赖于[整基](@entry_id:190217)选择的整数值，被称为 $K$ 的**[域判别式](@entry_id:198568)** (field discriminant)，记作 $\Delta_K$ [@problem_id:3080435]。[域判别式](@entry_id:198568)是[数域](@entry_id:155558)最重要的[不变量](@entry_id:148850)之一，它编码了[数域](@entry_id:155558)的算术信息。

#### $\mathcal{O}_K$ 与 $\mathbb{Z}[\alpha]$ 的关系

寻找一个[数域](@entry_id:155558)的[整数环](@entry_id:181003) $\mathcal{O}_K$ 及其[整基](@entry_id:190217)是一项核心任务。对于由单个[代数整数](@entry_id:151672) $\alpha$ 生成的[数域](@entry_id:155558) $K=\mathbb{Q}(\alpha)$，一个自然的问题是：$\mathcal{O}_K$ 是否就是由 $\alpha$ 生成的更简单的环 $\mathbb{Z}[\alpha]$（即所有 $g(\alpha)$ 形式的元素，其中 $g(x) \in \mathbb{Z}[x]$）？

答案是：不一定，但它们之间有密切的联系。由于 $\alpha$ 是[代数整数](@entry_id:151672)，并且 $\mathbb{Z}$ 中的元素也是[代数整数](@entry_id:151672)，而[代数整数](@entry_id:151672)集合成环，所以 $\mathbb{Z}[\alpha]$ 必然是 $\mathcal{O}_K$ 的一个[子环](@entry_id:154194)，即 $\mathbb{Z}[\alpha] \subseteq \mathcal{O}_K$ [@problem_id:3080452]。

这两个环之间的“距离”可以通过它们的[判别式](@entry_id:174614)来衡量。$\mathbb{Z}[\alpha]$ 作为自由 $\mathbb{Z}$-模，其基为 $\{1, \alpha, \ldots, \alpha^{n-1}\}$，其[判别式](@entry_id:174614)恰好等于 $\alpha$ 的极小多项式 $f(x)$ 的判别式 $\operatorname{Disc}(f)$。这两个判别式通过一个重要公式联系在一起：
$$ \operatorname{Disc}(f) = [\mathcal{O}_K : \mathbb{Z}[\alpha]]^2 \cdot \Delta_K $$
其中 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 是[加法群](@entry_id:151801) $\mathbb{Z}[\alpha]$ 在 $\mathcal{O}_K$ 中的指标。

这个公式告诉我们，当且仅当指标为 $1$ 时，$\mathcal{O}_K = \mathbb{Z}[\alpha]$。这给出了判断何时 $\mathcal{O}_K = \mathbb{Z}[\alpha]$ 的实用判据 [@problem_id:3080452]：
1.  如果 $\operatorname{Disc}(f) = \Delta_K$，则 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]=1$，因此 $\mathcal{O}_K = \mathbb{Z}[\alpha]$。
2.  一个更强的条件是：如果[多项式判别式](@entry_id:154854) $\operatorname{Disc}(f)$ 是一个**无平方因子** (square-free) 的整数，那么由于 $\Delta_K$ 是整数，$[\mathcal{O}_K : \mathbb{Z}[\alpha]]^2$ 必须是 $1$，从而 $\mathcal{O}_K = \mathbb{Z}[\alpha]$。

然而，存在许多情况使得 $\mathbb{Z}[\alpha]$ 只是 $\mathcal{O}_K$ 的一个真子环。例如，在 $K=\mathbb{Q}(\sqrt{-7})$ 中，取 $\alpha = \sqrt{-7}$，其整数环是 $\mathcal{O}_K = \mathbb{Z}[\frac{1+\sqrt{-7}}{2}]$，而 $\mathbb{Z}[\sqrt{-7}]$ 并不包含 $\frac{1+\sqrt{-7}}{2}$。

### 分解的困境与出路：从元素到理想

#### 元素分解唯一性的失效

我们从小就熟悉整数的唯一[因子分解定理](@entry_id:749213)（算术基本定理）。一个很自然的想法是，这种美好的性质是否也能推广到代数数域的整数环 $\mathcal{O}_K$ 中？答案是否定的。在许多[整数环](@entry_id:181003)中，将一个元素分解为不可约元素（无法再分解为两个非单位元素的乘积）的方式并不唯一。

一个经典的例子发生在 $K=\mathbb{Q}(\sqrt{-5})$ 的整数环 $\mathcal{O}_K=\mathbb{Z}[\sqrt{-5}]$ 中。考虑元素 $6$ 的分解 [@problem_id:3080417]：
$$ 6 = 2 \cdot 3 = (1+\sqrt{-5})(1-\sqrt{-5}) $$
我们可以通过范数 $N(a+b\sqrt{-5}) = a^2+5b^2$ 来验证，这里的四个因子 $2, 3, 1+\sqrt{-5}, 1-\sqrt{-5}$ 都是不可约的。例如，要分解 $2$，需要找到范数为 $2$ 的因子，但方程 $a^2+5b^2=2$ 无整数解。同样的方法可以证明其他三个因子也是不可约的。由于这些因子的范数各不相同，它们之间也不是互为伴随元（即相差一个单位元素）。因此，我们为 $6$ 找到了两种本质上不同的不可约[因子分解](@entry_id:150389)。这表明 $\mathbb{Z}[\sqrt{-5}]$ 不是一个**唯一[因子分解](@entry_id:150389)整环** (Unique Factorization Domain, UFD)。

#### Dedekind 的解决方案：[理想的唯一分解](@entry_id:154997)

19世纪的数学家 Ernst Kummer 和 Richard Dedekind 在研究[费马大定理](@entry_id:204421)的过程中遇到了这一障碍。Dedekind 提出了一个革命性的思想：虽然元素的唯一分解失败了，但可以通过引入“理想数”或更现代的**理想** (ideals) 概念来挽救[唯一分解](@entry_id:152313)性。

他证明了，任何[数域](@entry_id:155558)的[整数环](@entry_id:181003) $\mathcal{O}_K$ 都是一类特殊的环，称为**戴德金[整环](@entry_id:155321)** (Dedekind domain)。戴德金整环最重要的性质是：环中的任何非零真理想都可以唯一地（不计顺序）分解为**素理想** (prime ideals) 的乘积 [@problem_id:3080417]。

让我们回到 $\mathbb{Z}[\sqrt{-5}]$ 中 $6$ 的分解问题。元[素分解](@entry_id:198620)的模糊性在理想层面得到了澄清。相关元素的[理想分解](@entry_id:148948)为：
- $(2) = (2, 1+\sqrt{-5})^2 = \mathfrak{p}_2^2$
- $(3) = (3, 1+\sqrt{-5})(3, 1-\sqrt{-5}) = \mathfrak{p}_3 \mathfrak{p}'_3$
- $(1+\sqrt{-5}) = (2, 1+\sqrt{-5})(3, 1+\sqrt{-5}) = \mathfrak{p}_2 \mathfrak{p}_3$
- $(1-\sqrt{-5}) = (2, 1+\sqrt{-5})(3, 1-\sqrt{-5}) = \mathfrak{p}_2 \mathfrak{p}'_3$

其中 $\mathfrak{p}_2, \mathfrak{p}_3, \mathfrak{p}'_3$ 是[素理想](@entry_id:154026)。现在，主理想 $(6)$ 的分解可以从两种元[素分解](@entry_id:198620)的任何一种出发，得到相同的结果：
$$ (6) = (2)(3) = \mathfrak{p}_2^2 \cdot (\mathfrak{p}_3 \mathfrak{p}'_3) = \mathfrak{p}_2^2 \mathfrak{p}_3 \mathfrak{p}'_3 $$
$$ (6) = (1+\sqrt{-5})(1-\sqrt{-5}) = (\mathfrak{p}_2 \mathfrak{p}_3) \cdot (\mathfrak{p}_2 \mathfrak{p}'_3) = \mathfrak{p}_2^2 \mathfrak{p}_3 \mathfrak{p}'_3 $$
[唯一分解](@entry_id:152313)性在理想的层面上得到了恢复！这个例子也揭示了，在非UFD中，不可约元素（如 $2$）不一定生成[素理想](@entry_id:154026)（因为 $(2)=\mathfrak{p}_2^2$ 不是素理想）。

### 度量分解失效的工具：类群

#### [理想类群](@entry_id:153974)与[类数](@entry_id:156164)

既然唯一[因子分解](@entry_id:150389)的失败与[非主理想](@entry_id:201831)的存在有关，我们自然希望有一个工具来“度量”这种失败的程度。这个工具就是**[理想类群](@entry_id:153974)** (ideal class group) $\mathrm{Cl}(K)$。

理想类群的元素是 $\mathcal{O}_K$ 的（非零）分式理想等价类，其运算是理想的乘法。两个理想 $I, J$ 被认为是等价的，如果存在一个主理想 $(\alpha)$ 使得 $I = (\alpha)J$。所有[主理想](@entry_id:152760)构成了这个群的单位元。因此，[理想类群](@entry_id:153974)衡量了环中有多少“本质上不同”的[非主理想](@entry_id:201831)。

[理想类群](@entry_id:153974)的大小，即其中元素的个数，被称为**类数** (class number)，记为 $h_K$。一个惊人的结果是，任何[数域](@entry_id:155558)的类数都是有限的。

#### 类数与唯一因子分解性

[类数](@entry_id:156164)与[整数环](@entry_id:181003)的[因子分解](@entry_id:150389)性质之间有着直接而深刻的联系：
**一个戴德金[整环](@entry_id:155321) $\mathcal{O}_K$ 是唯一因子分解[整环](@entry_id:155321) (UFD) 当且仅当它是一个[主理想整环](@entry_id:152359) (PID)，这又等价于它的[类数](@entry_id:156164) $h_K=1$** [@problem_id:3080438]。

换言之，[类数](@entry_id:156164) $h_K$ 精确地度量了 $\mathcal{O}_K$ 离唯一因子分解整环“有多远”。
- 如果 $h_K=1$，则所有理想都是主理想，$\mathcal{O}_K$ 就是一个UFD。
- 如果 $h_K > 1$，则存在[非主理想](@entry_id:201831)，$\mathcal{O}_K$ 就不是UFD。

例如，对于我们之前讨论的 $\mathbb{Q}(\sqrt{-5})$，其类数是 $h_K=2$，这解释了为什么它不是UFD。另一个例子是 $K=\mathbb{Q}(\sqrt{-6})$，其整数环是 $\mathcal{O}_K=\mathbb{Z}[\sqrt{-6}]$，类数也是 $h_K=2$。在其中，我们有分解 $10 = 2 \cdot 5 = (2+\sqrt{-6})(2-\sqrt{-6})$，这是元素[唯一分解](@entry_id:152313)失效的又一个例证 [@problem_id:3080438]。

### [素理想分解](@entry_id:197179)的机制

既然我们知道 $\mathcal{O}_K$ 中的理想可以[唯一分解](@entry_id:152313)为素理想的乘积，下一个关键问题是：给定一个有理素数 $p$，它在 $\mathcal{O}_K$ 中对应的主理想 $(p)$ 是如何分解的？

#### Dedekind 判别法

Dedekind 判别法为这个问题提供了一个强大的计算工具。假设[数域](@entry_id:155558) $K$ 由[代数整数](@entry_id:151672) $\alpha$ 生成，即 $K=\mathbb{Q}(\alpha)$，且 $\alpha$ 的极小多项式为 $f(x) \in \mathbb{Z}[x]$。该判别法指出，在 $p$ 不整除指标 $[\mathcal{O}_K : \mathbb{Z}[\alpha]]$ 的“好”情况下，$(p)$ 在 $\mathcal{O}_K$ 中的分解方式与 $f(x)$ 在[有限域](@entry_id:142106) $\mathbb{F}_p = \mathbb{Z}/p\mathbb{Z}$ 上的分解方式完全平行 [@problem_id:3080451]。

具体来说，如果 $f(x)$ 在 $\mathbb{F}_p[x]$ 中分解为：
$$ \overline{f}(x) = \overline{g_1}(x)^{e_1} \overline{g_2}(x)^{e_2} \cdots \overline{g_r}(x)^{e_r} $$
其中 $\overline{g_i}(x)$ 是 $\mathbb{F}_p[x]$ 中互不相同的首一不[可约多项式](@entry_id:148759)。那么，[主理想](@entry_id:152760) $(p)$ 在 $\mathcal{O}_K$ 中就分解为：
$$ (p) = \mathfrak{p}_1^{e_1} \mathfrak{p}_2^{e_2} \cdots \mathfrak{p}_r^{e_r} $$
这里的 $\mathfrak{p}_i$ 是 $\mathcal{O}_K$ 中不同的[素理想](@entry_id:154026)。每个[素理想](@entry_id:154026) $\mathfrak{p}_i$ 都与一个多项式因子 $\overline{g_i}(x)$ 对应，并且可以具体地表示为 $\mathfrak{p}_i = (p, g_i(\alpha))$，其中 $g_i(x)$ 是 $\overline{g_i}(x)$ 在 $\mathbb{Z}[x]$ 中的任意一个首一提升。

此外，分解中的两个重要参数也由多项式分解决定：
- **[分歧指数](@entry_id:186386)** (Ramification Index) $e_i$：就是多项式因子 $\overline{g_i}(x)$ 的指数。
- **惯性指数** (Inertia Degree) $f_i$：就是多项式因子 $\overline{g_i}(x)$ 的次数，即 $f_i = \deg(\overline{g_i}(x))$。它也等于[剩余类](@entry_id:185226)[域扩张的次数](@entry_id:149430) $[\mathcal{O}_K/\mathfrak{p}_i : \mathbb{F}_p]$。

这些指数满足基本恒等式 $\sum_{i=1}^{r} e_i f_i = [K:\mathbb{Q}]$。

#### 分歧与判别式

当[素理想分解](@entry_id:197179)中至少有一个[分歧指数](@entry_id:186386) $e_i > 1$ 时，我们称素数 $p$ 在 $K$ 中是**[分歧](@entry_id:193119)的** (ramified)。[分歧](@entry_id:193119)是一个核心概念，它标志着算术行为的某种“退化”。

哪个素数会分歧？答案与我们之前定义的[域判别式](@entry_id:198568) $\Delta_K$ 有着惊人的联系。**戴德金判别式定理** (Dedekind's Discriminant Theorem) 断言：
**一个有理素数 $p$ 在数域 $K$ 中[分歧](@entry_id:193119)，当且仅当 $p$ 整除[域判别式](@entry_id:198568) $\Delta_K$ 的[绝对值](@entry_id:147688)** [@problem_id:3080455]。

这赋予了判别式深刻的算术意义：它恰好编码了[数域](@entry_id:155558)中哪些素数会发生[分歧](@entry_id:193119)。

在**伽罗瓦扩张** (Galois extension) $K/\mathbb{Q}$ 中，[素理想](@entry_id:154026)的分解表现出更强的对称性。对于任何一个素数 $p$，它在 $\mathcal{O}_K$ 中分解得到的所有素理想 $\mathfrak{p}_i$ 都具有相同的[分歧指数](@entry_id:186386) $e$ 和惯性指数 $f$。此时，基本恒等式简化为 $n = efg$，其中 $g$ 是 $p$ 上方素理想的个数 [@problem_id:3080455]。

对于被[驯顺分歧](@entry_id:186468)（tamely ramified，即 $p \nmid e$）的素数 $p$，我们甚至可以精确计算 $\Delta_K$ 中 $p$ 的幂次：$p$ 在 $\Delta_K$ 中的幂次（$p$-adic valuation）等于 $\sum_{\mathfrak{p}|p} (e-1)f = g(e-1)f$ [@problem_id:3080455]。

### [单位群](@entry_id:184012)的结构

最后，我们来探讨[整数环](@entry_id:181003) $\mathcal{O}_K$ 中可逆元素的结构。这些元素称为**单位** (units)，它们构成一个[乘法群](@entry_id:155975)，即**单位群** (unit group) $\mathcal{O}_K^\times$。一个元素 $u \in \mathcal{O}_K$ 是单位，当且仅当它的范数 $N_{K/\mathbb{Q}}(u) = \pm 1$。

**[狄利克雷单位定理](@entry_id:155550)** (Dirichlet's Unit Theorem) 是描述单位群结构的奠基性成果。该定理指出，$\mathcal{O}_K^\times$ 的结构如下 [@problem_id:3080406]：
$$ \mathcal{O}_K^\times \cong \mu_K \times \mathbb{Z}^{r_1+r_2-1} $$
这里：
- $\mu_K$ 是 $K$ 中所有**[单位根](@entry_id:143302)** (roots of unity) 构成的[有限循环群](@entry_id:147298)，即[单位群](@entry_id:184012)的挠部分。
- $\mathbb{Z}^{r_1+r_2-1}$ 是一个自由[阿贝尔群](@entry_id:150284)，其秩为 $r = r_1+r_2-1$。
- $r_1$ 是 $K$ 的实嵌入（$\sigma(K) \subseteq \mathbb{R}$）的个数。
- $r_2$ 是 $K$ 的共轭[复嵌入](@entry_id:189961)（$\sigma(K) \not\subseteq \mathbb{R}$）的对数。总嵌入数 $n = r_1+2r_2$。

这个定理揭示了单位群由两部分构成：一个有限的[循环群](@entry_id:138668)（单位根）和一个具有 $r_1+r_2-1$ 个[基本单位](@entry_id:148878)生成的无限部分。

秩 $r_1+r_2-1$ 的来源非常巧妙，它与[对数嵌入](@entry_id:148678)有关。我们构造一个**[对数映射](@entry_id:637227)** $L: \mathcal{O}_K^\times \to \mathbb{R}^{r_1+r_2}$，定义为：
$$ L(u) = (\log|\sigma_1(u)|, \ldots, \log|\sigma_{r_1}(u)|, 2\log|\tau_1(u)|, \ldots, 2\log|\tau_{r_2}(u)|) $$
其中 $\sigma_i$ 是实嵌入，$\tau_j$ 代表成对的[复嵌入](@entry_id:189961)。

对于任何单位 $u$，其范数为 $\pm 1$，取对数后可以推导出其在对数空间中的像满足一个线性方程：
$$ \sum_{i=1}^{r_1} \log|\sigma_i(u)| + \sum_{j=1}^{r_2} 2\log|\tau_j(u)| = \log|N(u)| = \log(1) = 0 $$
这意味着所有单位的像都落在一个维度为 $(r_1+r_2)-1$ 的超平面上。狄利克雷证明了，单位群在这个[超平面](@entry_id:268044)中的像构成一个满秩的**格** (lattice)，其秩正好是超平面的维数 $r_1+r_2-1$。这个格的秩正是[单位群](@entry_id:184012)的[自由秩](@entry_id:139914)，从而解释了定理中指数的来源 [@problem_id:3080406]。

通过本章的探讨，我们从最基本的定义出发，逐步构建了代数数域的理论框架。我们看到，看似抽象的概念如判别式、[类群](@entry_id:182524)和[单位群](@entry_id:184012)，实际上是理解[数域](@entry_id:155558)算术行为、解决因子分解等具体问题的关键工具。这些原理与机制共同构成了[代数数论](@entry_id:148067)的宏伟图景。