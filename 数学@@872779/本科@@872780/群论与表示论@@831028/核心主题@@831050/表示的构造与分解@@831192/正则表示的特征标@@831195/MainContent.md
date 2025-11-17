## 引言
在[群表示](@entry_id:156757)理论的宏伟画卷中，**[正则表示](@entry_id:137028)（regular representation）**无疑是其中最基本且最深刻的概念之一。它并非源于外部的[几何对称性](@entry_id:189059)，而是直接从群自身的[代数结构](@entry_id:137052)中生长出来，通过[群作用](@entry_id:268812)于其自身的方式，为我们提供了一个窥探群内蕴性质的独特视角。理解[正则表示](@entry_id:137028)，特别是其特征标的性质，是掌握整个表示论体系的关键一步。

然而，[正则表示](@entry_id:137028)的简洁定义背后隐藏着巨大的威力，初学者往往难以立即洞察其全部意义。本文旨在填补这一认知鸿沟，系统性地揭示[正则表示](@entry_id:137028)特征标的奥秘。我们将看到，一个在单位元之外处处为零的[简单函数](@entry_id:137521)，如何成为解锁[群结构](@entry_id:146855)信息的万能钥匙。

在接下来的内容中，我们将分三步深入探索这一主题。首先，在“**原理与机制**”一章中，我们将严格定义[正则表示](@entry_id:137028)及其特征标，推导其关键的分解定理，并引出著名的维数公式。随后，在“**应用与[交叉](@entry_id:147634)学科联系**”一章中，我们将展示[正则表示](@entry_id:137028)如何作为工具，揭示群的忠实性、代数运算性质，并与物理学、概率论等领域产生联系。最后，通过“**动手实践**”部分，读者将有机会通过具体计算来巩固所学知识，将抽象理论付诸实践。

## 原理与机制

在[群表示](@entry_id:156757)理论中，**[正则表示](@entry_id:137028)（regular representation）**是一种核心的构造，它通过群自身结构来定义表示，从而揭示了群的内在属性。本章将深入探讨[正则表示](@entry_id:137028)，特别是其特征标的定义、关键性质、分解定理以及由此产生的深刻推论。

### [正则表示](@entry_id:137028)及其特征标

思考一个[有限群](@entry_id:139710) $G$。最自然的[群作用](@entry_id:268812)莫过于 $G$ 作用于其自身。这种作用可以通过左乘法来实现：对于任意 $g, h \in G$，定义 $g$ 对 $h$ 的作用为 $g \cdot h = gh$。这个简单的思想是[正则表示](@entry_id:137028)的出发点。

为了构建一个[线性表示](@entry_id:139970)，我们需要一个[向量空间](@entry_id:151108)。最自然的选择是**[群代数](@entry_id:145139) (group algebra)** $\mathbb{C}[G]$，这是一个以群 $G$ 的所有元素为基的[复向量空间](@entry_id:264355)。也就是说，$\mathbb{C}[G]$ 中的任意向量可以唯一地写成 $\sum_{h \in G} c_h h$ 的形式，其中 $c_h \in \mathbb{C}$。这个空间的维数等于[群的阶](@entry_id:137115) $|G|$。

[左正则表示](@entry_id:146345) $\rho_{\text{reg}}$ 就是群 $G$ 在[向量空间](@entry_id:151108) $\mathbb{C}[G]$ 上的表示，其定义如下：对于任意 $g \in G$，它在 $\mathbb{C}[G]$ 上诱导的线性变换 $\rho_{\text{reg}}(g)$ 作用在[基向量](@entry_id:199546) $h \in G$ 上，结果是它们的群内乘积 $gh$。即：
$$
\rho_{\text{reg}}(g)(h) = gh
$$
这个作用可以线性地扩张到整个 $\mathbb{C}[G]$ 空间。

我们的首要任务是计算这个表示的**特征标 (character)** $\chi_{\text{reg}}(g) = \text{Tr}(\rho_{\text{reg}}(g))$。特征标是表示矩阵的迹。为了计算迹，我们选择 $\mathbb{C}[G]$ 的自然基，即群 $G$ 的所有元素 $\{h_1, h_2, \ldots, h_{|G|}\}$。

[线性变换](@entry_id:149133) $\rho_{\text{reg}}(g)$ 的矩阵表示 $M(g)$ 在这个基下的[矩阵元](@entry_id:186505) $[M(g)]_{ij}$ 是什么呢？根据定义，$\rho_{\text{reg}}(g)$ 将[基向量](@entry_id:199546) $h_j$ 映到 $gh_j$。如果 $gh_j = h_i$，那么 $[M(g)]_{ij} = 1$；否则为 $0$。因此，$M(g)$ 是一个[置换矩阵](@entry_id:136841)。

[矩阵的迹](@entry_id:139694)是其对角元素之和。对角元素 $[M(g)]_{jj}$ 只有在 $\rho_{\text{reg}}(g)$ 将[基向量](@entry_id:199546) $h_j$ 映到自身时才为 $1$，否则为 $0$。换言之，$[M(g)]_{jj} = 1$ 当且仅当 $gh_j = h_j$。因此，特征标 $\chi_{\text{reg}}(g)$ 就是被 $g$ 的[左乘作用](@entry_id:140679)固定的[基向量](@entry_id:199546)的数目 [@problem_id:1646199]。
$$
\chi_{\text{reg}}(g) = \sum_{h \in G} [M(g)]_{h,h} = |\{h \in G \mid gh = h\}|
$$
现在我们来求解方程 $gh=h$。在群中，我们可以右乘 $h^{-1}$，得到 $g=e$，其中 $e$ 是单位元。

这个简单的推[导带](@entry_id:159736)来了一个极为重要的结果：

*   如果 $g = e$，那么对于所有 $h \in G$，都有 $eh=h$。这意味着所有 $|G|$ 个[基向量](@entry_id:199546)都是[不动点](@entry_id:156394)。因此，
    $$
    \chi_{\text{reg}}(e) = |G|
    $$
    这个结果也符合一般表示理论的结论：表示在单位元处的特征标值等于表示空间的维数 [@problem_id:1646230]。

*   如果 $g \neq e$，那么方程 $gh=h$ 没有解，即不存在任何[不动点](@entry_id:156394)。因此，
    $$
    \chi_{\text{reg}}(g) = 0
    $$

综上所述，[正则表示的特征标](@entry_id:137278)具有一个非常简洁和独特的结构 [@problem_id:1646229] [@problem_id:1646192]：
$$
\chi_{\text{reg}}(g) = \begin{cases} |G|,  &\text{若 } g = e \\ 0,  &\text{若 } g \neq e \end{cases}
$$
例如，对于8阶[二面体群](@entry_id:143875) $D_4$，其[正则表示的特征标](@entry_id:137278)在单位元处为8，在所有其他7个非单位元（以及它们所在的共轭类）处均为0 [@problem_id:1646199]。

### 正则特征标的分解

我们已经确定了 $\chi_{\text{reg}}$ 的值。下一个关键问题是：[正则表示](@entry_id:137028)是可约的还是不可约的？

判断一个表示是否可约的有力工具是[特征标的内积](@entry_id:137615)。对于群 $G$ 上的两个特征标 $\chi$ 和 $\psi$，它们的[内积](@entry_id:158127)定义为：
$$
\langle \chi, \psi \rangle = \frac{1}{|G|} \sum_{g \in G} \chi(g) \overline{\psi(g)}
$$
一个表示是不可约的当且仅当其特征标的自身[内积](@entry_id:158127)为1。现在我们计算 $\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle$ [@problem_id:1646200]：
$$
\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{\text{reg}}(g) \overline{\chi_{\text{reg}}(g)}
$$
由于 $\chi_{\text{reg}}(g)$ 的值都是实数，复共轭等于其自身。当 $g \neq e$ 时，求和项为0，所以我们只需要考虑 $g=e$ 的情况：
$$
\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle = \frac{1}{|G|} \left( \chi_{\text{reg}}(e)^2 + \sum_{g \neq e} 0^2 \right) = \frac{1}{|G|} (|G|^2) = |G|
$$
这个结果 $\langle \chi_{\text{reg}}, \chi_{\text{reg}} \rangle = |G|$ 意味着，当群 $G$ 不是平凡群（即 $|G| > 1$）时，该[内积](@entry_id:158127)值大于1。因此，对于任何非平凡有限群，其[正则表示](@entry_id:137028)总是**可约的（reducible）** [@problem_id:1646205]。

既然是可约的，那么[正则表示](@entry_id:137028)可以分解为[不可约表示](@entry_id:263310)的直和。相应地，其特征标 $\chi_{\text{reg}}$ 可以写成不可约特征标 $\chi_i$ 的[线性组合](@entry_id:154743)：
$$
\chi_{\text{reg}} = \sum_{i=1}^k n_i \chi_i
$$
其中 $\{ \chi_1, \ldots, \chi_k \}$ 是 $G$ 的所有互不等价的不可约特征标的集合，$n_i$ 是非负整数，表示第 $i$ 个不可约表示在[正则表示](@entry_id:137028)中出现的**重数（multiplicity）**。

利用不可约特征标之间的[正交关系](@entry_id:145540)（$\langle \chi_i, \chi_j \rangle = \delta_{ij}$），我们可以确定系数 $n_j$：
$$
n_j = \langle \chi_{\text{reg}}, \chi_j \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{\text{reg}}(g) \overline{\chi_j(g)}
$$
再次利用 $\chi_{\text{reg}}$ 的特殊性质，这个求和中只有 $g=e$ 一项非零：
$$
n_j = \frac{1}{|G|} \left( \chi_{\text{reg}}(e) \overline{\chi_j(e)} \right) = \frac{1}{|G|} \left( |G| \overline{\chi_j(e)} \right) = \overline{\chi_j(e)}
$$
由于 $\chi_j(e)$ 是第 $j$ 个不可约表示的维数 $d_j$，它是一个正整数，因此是实数。所以 $\overline{\chi_j(e)} = \chi_j(e) = d_j$。

我们得到了[表示论](@entry_id:137998)中一个里程碑式的定理 [@problem_id:1646218] [@problem_id:1646201]：
$$
n_j = d_j = \chi_j(e)
$$
这意味着，每个不可约表示在[正则表示](@entry_id:137028)中出现的次数，恰好等于其自身的维数！

因此，正则特征标的分解公式为：
$$
\chi_{\text{reg}} = \sum_{i=1}^k d_i \chi_i
$$
例如，对于对称群 $S_3$，它有三个不可约表示，维数分别为 $d_1=1$（[平凡表示](@entry_id:141357)），$d_2=1$（符号表示）和 $d_3=2$。其[正则表示的特征标](@entry_id:137278)分解为 $\chi_{\text{reg}} = 1 \cdot \chi_1 + 1 \cdot \chi_2 + 2 \cdot \chi_3$ [@problem_id:1646218]。

### 分解的基本推论

[正则表示的分解](@entry_id:146409)公式 $\chi_{\text{reg}} = \sum_i d_i \chi_i$ 不仅仅是一个漂亮的数学表达式，它还蕴含着关于[群结构](@entry_id:146855)的深刻信息。

一个最直接且重要的推论是通过在单位元 $e$ 处取值得到的。我们将 $g=e$ 代入分解公式两侧：
左边是 $\chi_{\text{reg}}(e) = |G|$。
右边是 $\sum_{i=1}^k d_i \chi_i(e) = \sum_{i=1}^k d_i \cdot d_i = \sum_{i=1}^k d_i^2$。

于是，我们得到了著名的**维数公式（或称平方和公式）**：
$$
|G| = \sum_{i=1}^k d_i^2
$$
这个公式表明，群的阶等于其所有[不可约表示](@entry_id:263310)维数的平方和。这是一个非常强大的约束条件，极大地帮助了我们寻找和分类一个给定群的不可约表示。例如，任何一个阶为8的群，其[不可约表示](@entry_id:263310)维数的平方和必须等于8。

此外，正则特征标的分解也揭示了群的另一个基本结构属性。分解式 $\chi_{\text{reg}} = \sum_{i=1}^{k} d_i \chi_i$ 中的求和项数 $k$，即群 $G$ 的互不等价的不可约表示的总数，本身就是一个重要的群[不变量](@entry_id:148850)。表示理论的一个基本定理告诉我们，这个数 $k$ 恰好等于群 $G$ 中**共轭类（conjugacy classes）**的数量 [@problem_id:1646244]。[正则表示](@entry_id:137028)包含了所有的不可约表示，从而将群的[代数结构](@entry_id:137052)（通过共轭类）和其[线性表示](@entry_id:139970)行为（通过[不可约表示](@entry_id:263310)）联系在一起。

最后，由于不可约特征标构成了所有**[类函数](@entry_id:146970)（class functions）**（即在共轭类上取常值的函数）所组成[向量空间](@entry_id:151108)的一组标准正交基，任何类函数都可以唯一地表示为它们的[线性组合](@entry_id:154743)。正则特征标的定义 $\chi_{\text{reg}}(g) = |G|\delta_{g,e}$ 是如此特殊，以至于任何满足此条件的类函数都必然是正则特征标，因为它们会有完全相同的分解系数 [@problem_id:1646201]。

### 正则特征标与[子群](@entry_id:146164)

[正则表示](@entry_id:137028)的优美性质也延伸到了群与[子群](@entry_id:146164)的关系中。设 $H$ 是 $G$ 的一个[子群](@entry_id:146164)，我们可以分别考虑 $G$ 和 $H$ 的[正则表示](@entry_id:137028)，记其特征标为 $\chi_{\text{reg},G}$ 和 $\chi_{\text{reg},H}$。

我们可以研究 $\chi_{\text{reg},G}$ **限制（restriction）**到[子群](@entry_id:146164) $H$ 上的行为。一个 $G$ 的特征标 $\chi$ 限制到 $H$ 上，记为 $\chi\downarrow_H$，其定义就是简单地将函数定义域缩小到 $H$。对于 $\chi_{\text{reg},G}$：
$$
(\chi_{\text{reg},G}\downarrow_H)(h) = \chi_{\text{reg},G}(h) \quad \text{for } h \in H
$$
根据 $\chi_{\text{reg},G}$ 的定义，当 $h=e$ 时，其值为 $|G|$；当 $h \in H$ 且 $h \neq e$ 时，其值为 $0$。
另一方面， $H$ 自身的正则特征标为 $\chi_{\text{reg},H}(h) = |H|\delta_{h,e}$。
比较两者，我们发现一个简洁的关系：
$$
(\chi_{\text{reg},G}\downarrow_H)(h) = \frac{|G|}{|H|} \chi_{\text{reg},H}(h) = [G:H] \cdot \chi_{\text{reg},H}(h)
$$
其中 $[G:H] = |G|/|H|$ 是[子群](@entry_id:146164) $H$ 在 $G$ 中的**指数（index）**。这个关系表明，$G$ 的正则[特征标限制](@entry_id:139251)到 $H$ 上，等于 $H$ 的正则特征标乘以指数 $[G:H]$。

这个关系也可以从更高等的视角来理解，例如通过**[诱导表示](@entry_id:136842)（induced representation）**和**[弗罗贝尼乌斯互反律](@entry_id:140909)（Frobenius Reciprocity）**。[弗罗贝尼乌斯互反律](@entry_id:140909)指出，对于 $H$ 的特征标 $\psi$ 和 $G$ 的特征标 $\phi$，有 $\langle \text{Ind}_H^G(\psi), \phi \rangle_G = \langle \psi, \phi\downarrow_H \rangle_H$。

让我们考虑一个从 $H$ 的正则[特征标诱导](@entry_id:140107)到 $G$ 的特征标 $\Psi = \text{Ind}_H^G(\chi_{\text{reg},H})$。如果我们计算它与 $G$ 的正则[特征标的内积](@entry_id:137615) $\langle \Psi, \chi_{\text{reg},G} \rangle_G$，一方面可以直接计算得到 $\Psi(e) = [G:H]\chi_{\text{reg},H}(e) = [G:H]|H|=|G|$，从而[内积](@entry_id:158127)为 $|G|$ [@problem_id:1646208]。另一方面，利用[互反律](@entry_id:188215)和我们刚刚导出的限制关系：
$$
\langle \Psi, \chi_{\text{reg},G} \rangle_G = \langle \chi_{\text{reg},H}, \chi_{\text{reg},G}\downarrow_H \rangle_H = \langle \chi_{\text{reg},H}, [G:H]\chi_{\text{reg},H} \rangle_H = [G:H] \langle \chi_{\text{reg},H}, \chi_{\text{reg},H} \rangle_H
$$
我们已知 $\langle \chi_{\text{reg},H}, \chi_{\text{reg},H} \rangle_H = |H|$，因此整个表达式等于 $[G:H]|H| = |G|$。两种方法得到相同的结果，这不仅验证了我们的结论，也展示了表示理论内部概念的和谐统一。