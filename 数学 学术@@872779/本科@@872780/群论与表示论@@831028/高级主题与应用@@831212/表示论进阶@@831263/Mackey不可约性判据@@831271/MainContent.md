## 引言
在[群表示论](@entry_id:141930)中，[诱导表示](@entry_id:136842)是一种从子群的表示“构建”出整个[群表示](@entry_id:156757)的基础性方法。然而，一个根本问题随之而来：从一个不可约的子[群表示](@entry_id:156757)出发，我们得到的[诱导表示](@entry_id:136842)是否依然是不可约的？简单地进行诱导并不能保证我们获得[表示论](@entry_id:137998)的基本构件——[不可约表示](@entry_id:263310)。这篇文章旨在填补这一认知空白，系统地介绍 George Mackey 提出的一个强大解决方案——Mackey 不可约判据。

本文将引导读者深入探索这一核心理论。在第一章“原理与机制”中，我们将通过具体例子揭示[诱导表示](@entry_id:136842)的可约性问题，并详细阐述 Mackey [内积](@entry_id:158127)公式以及由此推导出的不可约判据，同时分析其在[正规子群](@entry_id:147397)、中心[子群](@entry_id:146164)等特殊结构下的简化形式。接下来，在“应用与跨学科联系”一章，我们将展示该判据如何在构建具体群的表示、李型[有限群表示论](@entry_id:143275)、甚至在伽罗瓦理论和数论等领域中发挥关键作用，彰显其深刻的结构性意义。最后，“动手实践”部分将提供一系列练习，帮助读者将理论知识转化为解决实际问题的能力。通过这一系列的学习，你将掌握判断[诱导表示](@entry_id:136842)不可约性的关键工具，并领会其在现代数学中的广泛影响。

## 原理与机制

在上一章中，我们介绍了从[子群](@entry_id:146164) $H$ 的表示来构造群 $G$ 的表示的一种核心技术——[诱导表示](@entry_id:136842)。一个自然而深刻的问题随之而来：如果从一个[不可约表示](@entry_id:263310)出发，诱导出的表示是否也一定是不可约的？答案是否定的。本章将深入探讨这一问题，并引入一个强大的工具——**Mackey 不可约判据 (Mackey Irreducibility Criterion)**，它为我们判断[诱导表示](@entry_id:136842)是否可约提供了精确的条件。

### 从一个例子看[诱导表示](@entry_id:136842)的可约性

判断一个特征标 $\chi$ 是否不可约的最直接方法是计算其[内积](@entry_id:158127) $\langle \chi, \chi \rangle_G$。根据表示理论的基本原理，一个特征标是不可约的，当且仅当其与自身的[内积](@entry_id:158127)为 1。如果[内积](@entry_id:158127)大于 1，则表示是可约的，且[内积](@entry_id:158127)的值等于其不可约分量重数的平方和。

让我们通过一个具体的例子来感受这一过程，并发现其局限性。

考虑 3 次对称群 $G = S_3$，其阶为 6。取[子群](@entry_id:146164) $H = \{e, (12)\}$，其中 $e$ 是单位元。$H$ 的阶为 2。令 $\psi$ 为 $H$ 的非平凡一维特征标，定义为 $\psi(e) = 1$ 和 $\psi((12)) = -1$。现在我们来考察从 $\psi$ 诱导到 $G$ 的特征标 $\chi = \text{Ind}_H^G \psi$。

[诱导特征标](@entry_id:143636) $\chi(g)$ 的值可以通过以下公式计算：
$$ \chi(g) = \frac{1}{|H|} \sum_{x \in G, x^{-1}gx \in H} \psi(x^{-1}gx) $$
我们需要计算 $\chi$ 在 $S_3$ 的三个共轭类 $C_1 = \{e\}$, $C_2 = \{(12), (13), (23)\}$, $C_3 = \{(123), (132)\}$ 上的值。

1.  **单位元 $g=e$**: 对所有 $x \in G$，都有 $x^{-1}ex = e \in H$，因此：
    $$ \chi(e) = \frac{1}{2} \sum_{x \in G} \psi(e) = \frac{1}{2} |G| = \frac{6}{2} = 3 $$
    这也等于 $[G:H] \cdot \dim(\psi) = 3 \cdot 1 = 3$。

2.  **对换 $g \in C_2$**: 以 $g=(13)$ 为例。我们需要找到所有 $x \in G$ 使得 $x^{-1}(13)x \in H = \{e, (12)\}$。由于共轭不改变元素的轮换结构，$x^{-1}(13)x$ 必须是一个[对换](@entry_id:142115)，因此它只能是 $(12)$。满足 $x^{-1}(13)x = (12)$ 的 $x$ 的数量等于 $g$ 的[中心化子的大小](@entry_id:137596)，即 $|C_G((13))| = |\{e, (13)\}| = 2$。对每一个这样的 $x$，我们有 $\psi(x^{-1}(13)x) = \psi((12)) = -1$。因此：
    $$ \chi((13)) = \frac{1}{2} (2 \cdot (-1)) = -1 $$
    由于特征标在共轭类上取值相同，所有[对换](@entry_id:142115)上的值都是 $-1$。

3.  **3-轮换 $g \in C_3$**: 3-轮换的任何共轭都不是 $H$ 中的元素，所以求和为[空集](@entry_id:261946)：
    $$ \chi((123)) = 0 $$

我们得到了[诱导特征标](@entry_id:143636) $\chi$ 的值：$\chi(e)=3, \chi(C_2)=-1, \chi(C_3)=0$。现在我们可以计算其[内积](@entry_id:158127)：
$$ \langle \chi, \chi \rangle_G = \frac{1}{|G|} \sum_{g \in G} |\chi(g)|^2 = \frac{1}{6} \left( 1 \cdot \chi(e)^2 + 3 \cdot \chi(C_2)^2 + 2 \cdot \chi(C_3)^2 \right) $$
$$ \langle \chi, \chi \rangle_G = \frac{1}{6} \left( 1 \cdot 3^2 + 3 \cdot (-1)^2 + 2 \cdot 0^2 \right) = \frac{1}{6}(9+3+0) = 2 $$

[内积](@entry_id:158127)为 2 表明，尽管我们从一个不可约特征标 $\psi$ 出发，但诱导出的特征标 $\chi = \text{Ind}_H^G \psi$ 却是可约的 [@problem_id:1628770]。它分解为了两个不可约特征标之和（事实上，是 $S_3$ 的[符号特征标](@entry_id:137578)和二维标准特征标之和）。

这个计算过程虽然有效，但较为繁琐。它需要我们计算出[诱导特征标](@entry_id:143636)在所有共轭类上的值。这引出一个重要问题：是否存在一个更深刻、更直接的判据，能够不经过完整的[特征标计算](@entry_id:139604)，就预言[诱导表示](@entry_id:136842)的可约性？George Mackey 的工作为我们提供了有力的解答。

### Mackey [内积](@entry_id:158127)公式与不可约判据

Mackey 理论的核心成果之一是一个计算两个[诱导表示](@entry_id:136842)[特征标内积](@entry_id:137125)的普适公式。设 $\psi$ 和 $\phi$ 分别是[子群](@entry_id:146164) $H$ 和 $K$ 的特征标，则 $\langle \text{Ind}_H^G \psi, \text{Ind}_K^G \phi \rangle_G$ 可以通过一个涉及 **[双陪集](@entry_id:145342) (double cosets)** 的和来计算。我们在此关注最重要的一种情况，即两个[诱导表示](@entry_id:136842)来自同一个[子群](@entry_id:146164) $H$。

**Mackey [内积](@entry_id:158127)公式** 指出，对于[子群](@entry_id:146164) $H \le G$ 的两个特征标 $\psi$ 和 $\phi$，我们有：
$$ \langle \text{Ind}_H^G \psi, \text{Ind}_H^G \phi \rangle_G = \sum_{s \in H \backslash G / H} \langle \text{Res}_{H \cap sHs^{-1}}^H \psi, \text{Res}_{H \cap sHs^{-1}}^{sHs^{-1}} \phi^s \rangle_{H \cap sHs^{-1}} $$
让我们仔细解读这个公式的构成：
-   **$H \backslash G / H$**: 这是 $G$ 中 $(H,H)$-[双陪集](@entry_id:145342)的代表元集合。一个[双陪集](@entry_id:145342) $HsH$ 是形如 $\{h_1sh_2 \mid h_1, h_2 \in H\}$ 的集合。整个群 $G$ 可以被分解为不相交的[双陪集](@entry_id:145342)之并。
-   **$sHs^{-1}$**: 这是 $H$ 经由元素 $s$ 共轭后得到的[子群](@entry_id:146164)，记为 $H^s$。
-   **$\phi^s$**: 这是定义在[共轭子群](@entry_id:140560) $H^s$ 上的一个新特征标，称为 $\phi$ 的**共轭特征标 (conjugate character)**，其定义为 $\phi^s(shs^{-1}) = \phi(h)$ 对于所有 $h \in H$。
-   **$\text{Res}_{K}^{H} \psi$**: 这表示将 $H$ 上的特征标 $\psi$ **限制 (restriction)** 到[子群](@entry_id:146164) $K \subseteq H$ 上。
-   $\langle \cdot, \cdot \rangle_{H \cap sHs^{-1}}$: 这是在交[子群](@entry_id:146164) $H \cap sHs^{-1}$ 上的标准[特征标内积](@entry_id:137125)。

现在，我们将这个公式应用于我们关心的核心问题：判断 $\text{Ind}_H^G \psi$ 的不可约性。我们令 $\phi = \psi$，并假设 $\psi$ 本身是 $H$ 的一个不可约特征标。公式变为：
$$ \langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G = \sum_{s \in H \backslash G / H} \langle \text{Res}_{H \cap sHs^{-1}}^H \psi, (\psi^s)|_{H \cap sHs^{-1}} \rangle_{H \cap sHs^{-1}} $$
其中 $(\psi^s)|_{H \cap sHs^{-1}}$ 表示将 $H^s$ 上的特征标 $\psi^s$ 限制在[子群](@entry_id:146164) $H \cap sHs^{-1}$ 上。

[双陪集](@entry_id:145342)的求和中，总有一个代表元可以取为单位元 $e$（对应[双陪集](@entry_id:145342) $HeH = H$）。对于 $s=e$ 这一项，我们有 $H \cap eHe^{-1} = H$，且 $\psi^e = \psi$。因此，该项的贡献是 $\langle \psi, \psi \rangle_H$。因为我们假设 $\psi$ 是不可约的，所以 $\langle \psi, \psi \rangle_H = 1$。

于是，$\langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G$ 的值等于 $1$ 加上所有其他[双陪集](@entry_id:145342)代表元 $s \notin H$ 的项的贡献。[诱导表示](@entry_id:136842) $\text{Ind}_H^G \psi$ 是不可约的，当且仅当这个[内积](@entry_id:158127)为 1。这要求对于所有 $s \in G \setminus H$（技术上是所有不在 $H$ 中的[双陪集](@entry_id:145342)代表元 $s$），对应的求和项必须为 0。

这便引出了 **Mackey 不可约判据**:
假设 $\psi$ 是 $H$ 的一个不可约特征标。则[诱导表示](@entry_id:136842) $\text{Ind}_H^G \psi$ 是不可约的，当且仅当对于所有 $s \in G \setminus H$，以下两个在[子群](@entry_id:146164) $K_s = H \cap sHs^{-1}$ 上的表示是**不交的 (disjoint)**，即它们的[特征标内积](@entry_id:137125)为 0：
1.  $\psi$ 限制到 $K_s$ 上的表示，其特征标为 $\text{Res}_{K_s}^H \psi$。
2.  $\psi^s$ 限制到 $K_s$ 上的表示，其特征标为 $\text{Res}_{K_s}^{sHs^{-1}} \psi^s$。

让我们用这个判据重新审视 $G=S_3, H=\{e, (12)\}$ 的例子 [@problem_id:1628770]。$G$ 关于 $H$ 的[双陪集](@entry_id:145342)分解为 $G = H \cup H(13)H$。我们可以选取代表元集合为 $\{e, (13)\}$。
-   **$s=e$**: 贡献为 $\langle \psi, \psi \rangle_H = 1$。
-   **$s=(13)$**: 我们需要计算交[子群](@entry_id:146164)上的[内积](@entry_id:158127)。
    -   [共轭子群](@entry_id:140560) $H^s = (13)H(13)^{-1} = \{e, (13)(12)(13)^{-1}\} = \{e, (23)\}$。
    -   交[子群](@entry_id:146164) $K_s = H \cap H^s = \{e, (12)\} \cap \{e, (23)\} = \{e\}$。
    -   在[平凡子群](@entry_id:141709) $\{e\}$ 上，任何特征标的限制都是平凡特征标（值为 1）。$\text{Res}_{\{e\}}^H \psi$ 和 $\text{Res}_{\{e\}}^{H^s} \psi^s$ 都是平凡特征标。
    -   因此，它们在 $\{e\}$ 上的[内积](@entry_id:158127)是 $\langle 1_{\{e\}}, 1_{\{e\}} \rangle_{\{e\}} = 1$。
总的[内积](@entry_id:158127)为 $\langle \chi, \chi \rangle_G = 1 + 1 = 2$。这与我们之前的直接计算结果完全一致，但它揭示了可约性的来源：存在一个 $s \notin H$ 使得限制在交[子群](@entry_id:146164)上的两个特征标并不正交（这里是因为交[子群](@entry_id:146164)过于平凡）。

### 判据的应用：特殊情形分析

[Mackey 判据](@entry_id:142003)的真正威力在于它能根据 $H$ 和 $G$ 的结构关系，推导出关于可约性的通用结论。

#### [正规子群](@entry_id:147397)与[惯性群](@entry_id:200010)

当 $H$ 是 $G$ 的一个**正规子群** ($H \trianglelefteq G$) 时，情况大大简化。对于任何 $s \in G$，我们有 $sHs^{-1} = H$。因此，[双陪集](@entry_id:145342) $HsH$ 就是[陪集](@entry_id:147145) $sH$。这意味着[双陪集](@entry_id:145342)分解就是陪集分解 $G/H$。[Mackey 公式](@entry_id:142235)中的交[子群](@entry_id:146164) $H \cap sHs^{-1}$ 恒为 $H$。公式变为：
$$ \langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G = \sum_{s \in G/H} \langle \psi, \psi^s \rangle_H $$
由于 $\psi$ 和 $\psi^s$ 都是 $H$ 的不可约特征标，根据[正交关系](@entry_id:145540)，$\langle \psi, \psi^s \rangle_H$ 的值要么是 1（如果 $\psi = \psi^s$），要么是 0（如果 $\psi \neq \psi^s$）。
因此，[内积](@entry_id:158127)的值恰好等于满足 $\psi^s = \psi$ 的[陪集](@entry_id:147145) $sH \in G/H$ 的数量。

这个条件引导我们定义**[惯性群](@entry_id:200010) (inertia group)** $I_G(\psi) = \{ g \in G \mid gHg^{-1}=H \text{ 且 } \psi^g = \psi \}$。当 $H$ 正规时，它简化为 $I_G(\psi) = \{ g \in G \mid \psi^g = \psi \}$。$I_G(\psi)$ 本身是 $G$ 的一个[子群](@entry_id:146164)，并且包含 $H$。[内积](@entry_id:158127)的值就是指数 $|I_G(\psi)/H|$。

由此我们得到一个重要推论：对于[正规子群](@entry_id:147397) $H$，$\text{Ind}_H^G \psi$ 是不可约的当且仅当 $I_G(\psi) = H$，即不存在 $H$ 之外的元素可以“稳定”$\psi$。反之，只要我们能找到一个元素 $g \in G \setminus H$ 使得 $gHg^{-1}=H$ 并且 $\psi^g = \psi$，那么 $\text{Ind}_H^G \psi$ 必定是可约的 [@problem_id:1628752]。

例如，考虑 $G=S_4$ 和 Klein [四元数群](@entry_id:147721) $H = V_4 = \{e, (12)(34), (13)(24), (14)(23)\}$。$H$ 是 $S_4$ 的正规子群。令 $\psi$ 是 $H$ 的一个非平凡特征标，例如 $\psi((12)(34))=1, \psi((13)(24))=-1, \psi((14)(23))=-1$。取元素 $s=(12) \in G \setminus H$。通过计算可以发现，[共轭作用](@entry_id:143328) $h \mapsto s^{-1}hs$ 保持 $(12)(34)$ 不变，并交换 $(13)(24)$ 和 $(14)(23)$。对于我们选择的 $\psi$，可以发现 $\psi^s = \psi$。因此，$s \in I_G(\psi)$。这意味着[惯性群](@entry_id:200010) $I_G(\psi)$ 严格大于 $H$。根据我们的推导，$\langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G = |I_G(\psi)/H| \ge 2$。事实上，可以计算出这个值为 2，因此表示是可约的 [@problem_id:1628737]。

#### 平凡的失效：阿贝尔群与中心[子群](@entry_id:146164)

[Mackey 判据](@entry_id:142003)在某些结构下会立即“失效”，从而直接断定表示是可约的。

考虑 $G$ 是一个有限**[阿贝尔群](@entry_id:150284) (abelian group)**，$H$ 是其任意一个[真子群](@entry_id:141915) ($H \neq G$) [@problem_id:1628745]。由于 $G$ 是阿贝尔群，对于任何 $s \in G \setminus H$：
-   $sHs^{-1} = H$，因为所有元素都可交换。
-   $\psi^s(h) = \psi(s^{-1}hs) = \psi(h)$，因此 $\psi^s = \psi$。

这意味着 [Mackey 判据](@entry_id:142003)的第二个条件对于任何 $s \notin H$ 都无法满足。限制在交[子群](@entry_id:146164) $H$ 上的两个特征标 $\psi$ 和 $\psi^s$ 完全相同，因此它们的[内积](@entry_id:158127)为 1。所以，$\text{Ind}_H^G \psi$ 总是可约的。

这个结论可以推广到更一般的情形。如果 $H$ 是 $G$ 的**中心 $Z(G)$** 的一个[真子群](@entry_id:141915) (或者就是 $Z(G)$ 本身，只要它不等于 $G$)，那么对于任何 $s \in G$ 和 $h \in H$，我们有 $s^{-1}hs = h$。因此，和阿贝尔群的情形一样，$\psi^s = \psi$ 总是成立。[Mackey 公式](@entry_id:142235)给出 $\langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G = [G:H]$ [@problem_id:1628762]。由于 $H$ 是[真子群](@entry_id:141915)，$[G:H] > 1$，所以[诱导表示](@entry_id:136842)总是可约的。

#### 一个关键的[二分法](@entry_id:140816)：指数为 2 的[子群](@entry_id:146164)

当 $H$ 在 $G$ 中的指数为 2 时，这是一个非常特殊且重要的正规子群情形。商群 $G/H$ 只有两个元素，可以表示为 $\{H, sH\}$，其中 $s$ 是任何一个不在 $H$ 中的元素。

此时，Mackey [内积](@entry_id:158127)公式简化为：
$$ \langle \text{Ind}_H^G \psi, \text{Ind}_H^G \psi \rangle_G = \langle \psi, \psi^e \rangle_H + \langle \psi, \psi^s \rangle_H = 1 + \langle \psi, \psi^s \rangle_H $$
由于 $\psi$ 和 $\psi^s$ 都是不可约的，$\langle \psi, \psi^s \rangle_H$ 的值只能是 1（若 $\psi = \psi^s$）或 0（若 $\psi \neq \psi^s$）。

因此，我们得到了一个异常简洁的判据 [@problem_id:1628710]：
设 $H$ 是 $G$ 的指数为 2 的[子群](@entry_id:146164)，$\psi$ 是 $H$ 的不可约特征标。则 $\text{Ind}_H^G \psi$ 是不可约的，当且仅当 $\psi \neq \psi^s$ 对于任何（等价于所有）$s \in G \setminus H$。
-   如果 $\psi \neq \psi^s$，则[内积](@entry_id:158127)为 $1+0=1$，表示不可约。
-   如果 $\psi = \psi^s$，则[内积](@entry_id:158127)为 $1+1=2$，表示可约，且分解为两个不等价的[不可约表示](@entry_id:263310)之和。

例如，在 $G=S_3$ 中，[正规子群](@entry_id:147397) $H=A_3$ 的指数为 2。$A_3$ 是 3 阶[循环群](@entry_id:138668)，有三个一维特征标。取一个非平凡特征标 $\pi$，例如 $\pi((123)) = \exp(2\pi i/3) = \omega$。取 $s=(12) \in S_3 \setminus A_3$。我们需要比较 $\pi$ 和 $\pi^s$。对于生成元 $(123) \in A_3$：
$$ \pi^s((123)) = \pi(s^{-1}(123)s) = \pi((12)(123)(12)) = \pi((132)) = \pi((123)^2) = \omega^2 $$
因为 $\omega^2 \neq \omega$，所以 $\pi^s \neq \pi$。根据判据，$\text{Ind}_{A_3}^{S_3} \pi$ 是不可约的 [@problem_id:1628743]。事实上，这是一个二维表示，它就是 $S_3$ 的标准表示。

#### 更广泛的视角：[置换表示](@entry_id:142960)

当诱导的特征标是[子群](@entry_id:146164) $H$ 的平凡特征标 $\psi = 1_H$ 时，[诱导表示](@entry_id:136842) $\text{Ind}_H^G 1_H$ 对应于 $G$ 在[陪集空间](@entry_id:180459) $G/H$ 上的[置换表示](@entry_id:142960)。[Mackey 判据](@entry_id:142003)此时也给出了一个优美的组合解释。

将 $\psi=1_H$ 代入 [Mackey 公式](@entry_id:142235)：
$$ \langle \text{Ind}_H^G 1_H, \text{Ind}_H^G 1_H \rangle_G = \sum_{s \in H \backslash G / H} \langle \text{Res}_{H \cap sHs^{-1}}^H 1_H, (1_H^s)|_{H \cap sHs^{-1}} \rangle_{H \cap sHs^{-1}} $$
注意到 $1_H$ 在任何[子群](@entry_id:146164)上的限制仍然是平凡特征标，且其共轭 $1_H^s$ 也是相应[共轭子群](@entry_id:140560)上的平凡特征标。因此，每一项都变成了在交[子群](@entry_id:146164)上两个平凡[特征标的内积](@entry_id:137615)，这个值恒为 1。
$$ \langle \text{Ind}_H^G 1_H, \text{Ind}_H^G 1_H \rangle_G = \sum_{s \in H \backslash G / H} 1 = |H \backslash G / H| $$
这意味着，[置换表示](@entry_id:142960) $\text{Ind}_H^G 1_H$ 的不可约分量的[重数](@entry_id:136466)平方和，恰好等于 $(H,H)$-[双陪集](@entry_id:145342)的数量。因此，[置换表示](@entry_id:142960)是不可约的当且仅当只有 1 个[双陪集](@entry_id:145342)（即 $G=H$，这是平凡情况）或 2 个[双陪集](@entry_id:145342)。

例如，考虑 $G=S_4$ 和 $H=S_3$（稳定元素 4 的[子群](@entry_id:146164)）。[置换表示](@entry_id:142960) $\text{Ind}_H^G 1_H$ 的维数为 $[G:H]=4$。[双陪集](@entry_id:145342)的数量等于 $H$ 作用在[陪集空间](@entry_id:180459) $G/H$ 上的[轨道](@entry_id:137151)数。$G/H$ 可以等同于集合 $\{1,2,3,4\}$，$H$ 的作用是[置换](@entry_id:136432) $\{1,2,3\}$ 并保持 4 不动。因此，有两个[轨道](@entry_id:137151)：$\{1,2,3\}$ 和 $\{4\}$。这意味着 $|H \backslash G / H|=2$。所以 $\langle \text{Ind}_H^G 1_H, \text{Ind}_H^G 1_H \rangle_G = 2$ [@problem_id:1628769]。这个 4 维表示是可约的，它分解为[平凡表示](@entry_id:141357)和 $S_4$ 的 3 维标准表示。

#### 综合案例分析

让我们以二面体群 $D_{16} = \langle r, f \mid r^8=f^2=e, frf=r^{-1} \rangle$ 为例，综合运用上述原理 [@problem_id:1628768]。
-   **情形 A**: $H_A = \langle r^4 \rangle$ 是中心[子群](@entry_id:146164)。根据我们的分析，从一个真中心[子群诱导](@entry_id:140843)的表示总是可约的。
-   **情形 B**: $H_B = \langle f \rangle$ 是一个非正规子群。取 $s=r \notin H_B$。[共轭子群](@entry_id:140560) $H_B^s = \langle rfr^{-1} \rangle = \langle fr^{-2} \rangle$。交[子群](@entry_id:146164) $H_B \cap H_B^s = \{e\}$。在[平凡子群](@entry_id:141709)上，任何特征标的限制都是平凡的，它们的[内积](@entry_id:158127)为 1。因此，[Mackey 判据](@entry_id:142003)的条件不满足，[诱导表示](@entry_id:136842)是可约的。
-   **情形 C**: $H_C = \langle r \rangle$ 是指数为 2 的[正规子群](@entry_id:147397)。取 $\psi_C(r)=i$。取 $s=f \notin H_C$。共轭特征标 $\psi_C^s(r) = \psi_C(f^{-1}rf) = \psi_C(r^{-1}) = \psi_C(r)^{-1} = -i$。由于 $\psi_C^s \neq \psi_C$，根据指数为 2 [子群](@entry_id:146164)的判据，[诱导表示](@entry_id:136842)是不可约的。
-   **情形 D**: $H_D = \langle r^2 \rangle$ 是[正规子群](@entry_id:147397)，但不是中心[子群](@entry_id:146164)。取 $\psi_D(r^2)=i$。考虑元素 $s=r \in G \setminus H_D$。$r$ 与 $H_D$ 的生成元 $r^2$ 可交换，所以[共轭作用](@entry_id:143328)是平凡的：$\psi_D^s = \psi_D$。因为存在 $H_D$ 之外的元素稳定 $\psi_D$，[诱导表示](@entry_id:136842)是可约的。

综上所述，Mackey 不可约判据不仅提供了一个计算工具，更重要的是，它揭示了[诱导表示](@entry_id:136842)的结构与群的代数性质（如正规性、中心、[双陪集](@entry_id:145342)分解）之间深刻的内在联系。通过分析判据在不同情境下的表现，我们能够对表示论中这一核心构造方法的行为做出精确的预测。