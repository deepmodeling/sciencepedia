## 引言
在[群表示论](@entry_id:141930)的宏伟框架中，从已有的表示出发构造新表示是一项核心技术。[对称平方](@entry_id:137676)（Symmetric Square）正是其中最基本且功能强大的构造之一。它为我们提供了一种数学语言，用以精确描述由成对的、不可区分的实体组成的系统，或由二次关系支配的现象。无论是分析两个[全同粒子](@entry_id:142755)的[量子态](@entry_id:146142)，还是研究物理量中的对称张量，[对称平方](@entry_id:137676)都自然而然地成为首选的分析工具。

本文旨在系统地揭示表示的[对称平方](@entry_id:137676)的奥秘。我们面临的核心问题是：如何利用[群的对称性](@entry_id:136707)来理解一个表示空间中元素两两组合所形成的结构？[对称平方](@entry_id:137676)的理论为这一问题提供了完整的解答。

在接下来的内容中，读者将踏上一段从基础到应用的探索之旅。在“原理与机制”一章，我们将深入其形式化定义，从张量积出发，推导出它的维度和关键的[特征标公式](@entry_id:142515)。随后的“应用与跨学科联系”一章将展示[对称平方](@entry_id:137676)如何在物理学、化学、组合学甚至数论等不同领域中发挥其威力，彰显[表示论](@entry_id:137998)的统一之美。最后，“动手实践”部分将通过精心设计的习题，帮助读者巩固理论知识并提升解决实际问题的能力。让我们首先进入第一章，探究其背后的基本原理。

## 原理与机制

继引言之后，本章将深入探讨表示的[对称平方](@entry_id:137676)的构造、性质及其在[群表示论](@entry_id:141930)中的核心作用。我们将从最基本的定义出发，逐步建立起一个坚实的理论框架，并通过具体的例子来阐明抽象的概念。

### [对称平方](@entry_id:137676)空间的构造

在表示论中，我们经常通过在现有[向量空间](@entry_id:151108)上进行代数构造来生成新的、更复杂的表示。其中一种最重要的构造便是[张量积](@entry_id:140694)。给定一个域 $\mathbb{F}$ 上的[向量空间](@entry_id:151108) $V$，我们可以构造其**张量平方 (tensor square)** $V \otimes V$。这个新的[向量空间](@entry_id:151108)由形如 $v \otimes w$（其中 $v, w \in V$）的“纯张量”线性张成。

在张量平方空间 $V \otimes V$ 中，存在一个非常自然的[线性算子](@entry_id:149003)，称为**交换算子 (swap operator)** 或**翻转算子 (flip operator)**，我们记作 $\tau$。对于任意 $v, w \in V$，该算子的定义为：
$$
\tau(v \otimes w) = w \otimes v
$$
这个定义可以线性地延拓到 $V \otimes V$ 中的所有元素。交换算子 $\tau$ 的一个显著性质是其对合性，即 $\tau^2 = \text{id}$，其中 $\text{id}$ 是[恒等算子](@entry_id:204623)。这意味着 $\tau$ 的[特征值](@entry_id:154894)只能是 $+1$ 或 $-1$。据此，只要域 $\mathbb{F}$ 的特征不为 2，[向量空间](@entry_id:151108) $V \otimes V$ 就可以分解为 $\tau$ 的两个特征[子空间](@entry_id:150286)的[直和](@entry_id:156782)。

这两个特征[子空间](@entry_id:150286)在[表示论](@entry_id:137998)中具有特殊的名称和重要性：

1.  **[对称平方](@entry_id:137676) (Symmetric Square)**：记作 $S^2(V)$ 或 $\text{Sym}^2(V)$，它是 $\tau$ 对应于[特征值](@entry_id:154894) $+1$ 的特征[子空间](@entry_id:150286)。换言之，它由在交换两个因子时保持不变的张量组成：
    $$
    S^2(V) = \{x \in V \otimes V \mid \tau(x) = x\}
    $$
    这个空间中的元素称为**对称张量 (symmetric tensors)**。典型的对称张量形如 $v \otimes w + w \otimes v$。

2.  **交错平方 (Alternating Square)** 或 **[外平方](@entry_id:141620) (Exterior Square)**：记作 $\Lambda^2(V)$ 或 $\text{Alt}^2(V)$，它是 $\tau$ 对应于[特征值](@entry_id:154894) $-1$ 的特征[子空间](@entry_id:150286)。它由在交换两个因子时符号反转的张量组成：
    $$
    \Lambda^2(V) = \{x \in V \otimes V \mid \tau(x) = -x\}
    $$
    这个空间中的元素称为**[反对称张量](@entry_id:199349) (alternating/anti-symmetric tensors)**。典型的[反对称张量](@entry_id:199349)形如 $v \otimes w - w \otimes v$。

因此，当[域的特征](@entry_id:154386)不为 2 时，我们有如下的[向量空间](@entry_id:151108)[直和分解](@entry_id:263004)：
$$
V \otimes V = S^2(V) \oplus \Lambda^2(V)
$$

一个基本的问题是确定这些空间的维度。假设 $V$ 是一个 $n$ 维[向量空间](@entry_id:151108)，并令 $\{e_1, e_2, \dots, e_n\}$ 是 $V$ 的一组基。那么，集合 $\{e_i \otimes e_j \mid 1 \le i, j \le n\}$ 构成了 $V \otimes V$ 的一组基，因此 $\dim(V \otimes V) = n^2$。

我们可以构造出 $S^2(V)$ 的一组基。对于基底 $\{e_i \otimes e_j\}$，我们有 $\tau(e_i \otimes e_j) = e_j \otimes e_i$。
- 当 $i = j$ 时，$\tau(e_i \otimes e_i) = e_i \otimes e_i$，所以 $e_i \otimes e_i$ 是对称张量。这为我们提供了 $n$ 个线性无关的[对称张量](@entry_id:148092)。
- 当 $i \neq j$ 时，$e_i \otimes e_j$ 和 $e_j \otimes e_i$ 张成一个二维[子空间](@entry_id:150286)。在这个[子空间](@entry_id:150286)中，向量 $e_i \otimes e_j + e_j \otimes e_i$ 满足 $\tau$ 的作用后不变，属于 $S^2(V)$；而向量 $e_i \otimes e_j - e_j \otimes e_i$ 在 $\tau$ 作用下变为其[相反数](@entry_id:151709)，属于 $\Lambda^2(V)$。
因此，对于每一对不等的下标 $\{i, j\}$（为了避免重复，我们可假定 $i  j$），我们都可以得到一个对称[基向量](@entry_id:199546) $e_i \otimes e_j + e_j \otimes e_i$。这样的组合共有 $\binom{n}{2}$ 个。

综上所述，$S^2(V)$ 的维度是对角项和非对角项贡献的总和 [@problem_id:1643920]：
$$
\dim(S^2(V)) = n + \binom{n}{2} = n + \frac{n(n-1)}{2} = \frac{2n + n^2 - n}{2} = \frac{n(n+1)}{2}
$$
相应地，$\dim(\Lambda^2(V)) = \dim(V \otimes V) - \dim(S^2(V)) = n^2 - \frac{n(n+1)}{2} = \frac{n(n-1)}{2}$。

例如，如果一个[复向量空间](@entry_id:264355) $V$ 的维数是 $\dim(V) = 21$，那么其[对称平方](@entry_id:137676)的维数是 $\dim(S^2(V)) = \frac{21 \times (21+1)}{2} = \frac{21 \times 22}{2} = 231$ [@problem_id:1643920]。

### [对称平方](@entry_id:137676)作为一种表示

如果[向量空间](@entry_id:151108) $V$ 是一个群 $G$ 的表示空间，其对应的表示为 $(\rho, V)$，那么我们自然可以将其上的代数构造提升为新的表示。对于 $g \in G$，它在 $V$ 上的作用由线性算子 $\rho(g)$ 给出。它在张量平方 $V \otimes V$ 上的作用则通过**[张量积表示](@entry_id:143629) (tensor product representation)** $\rho \otimes \rho$ 定义：
$$
(\rho \otimes \rho)(g) (v \otimes w) = (\rho(g)v) \otimes (\rho(g)w)
$$
一个关键的事实是，这个诱导的作用与交换算子 $\tau$ 是可交换的：
$$
\tau((\rho \otimes \rho)(g) (v \otimes w)) = \tau((\rho(g)v) \otimes (\rho(g)w)) = (\rho(g)w) \otimes (\rho(g)v) = (\rho \otimes \rho)(g) (w \otimes v) = (\rho \otimes \rho)(g) (\tau(v \otimes w))
$$
这意味着 $(\rho \otimes \rho)(g)$ 保持了 $S^2(V)$ 和 $\Lambda^2(V)$ 这两个[子空间](@entry_id:150286)的不变性。换句话说，$S^2(V)$ 和 $\Lambda^2(V)$ 都是 $V \otimes V$ 的**[子表示](@entry_id:141094) (subrepresentations)**。因此，我们得到了两个新的表示：
- **[对称平方](@entry_id:137676)表示 (symmetric square representation)**，记作 $\rho_{S^2(V)}$ 或 $Sym^2(\rho)$。
- **交错平方表示 (alternating square representation)**，记作 $\rho_{\Lambda^2(V)}$ 或 $\Lambda^2(\rho)$。

为了更具体地理解[对称平方](@entry_id:137676)表示是如何运作的，我们可以考察一个实例。考虑二维实[向量空间](@entry_id:151108) $V = \mathbb{R}^2$ 上的二维旋转群 $SO(2)$。群元 $g(\theta)$ 对应于逆时针旋转 $\theta$ 角，其在标准基下的矩阵表示为：
$$
\rho(g(\theta)) = \begin{pmatrix} \cos\theta  -\sin\theta \\ \sin\theta  \cos\theta \end{pmatrix}
$$
$V$ 的维数 $n=2$，所以 $S^2(V)$ 的维数是 $\frac{2(2+1)}{2}=3$。为了找到表示 $\rho_{S^2(V)}(g(\theta))$ 的矩阵，我们计算 $\rho(g(\theta))$ 作用在 $S^2(V)$ 的[基向量](@entry_id:199546)上。令 $\{e_1, e_2\}$ 为 $V$ 的标准基，则 $S^2(V)$ 的一组自然基是 $B = \{b_1, b_2, b_3\}$，其中 $b_1 = e_1 \otimes e_1$, $b_2 = e_1 \otimes e_2 + e_2 \otimes e_1$, $b_3 = e_2 \otimes e_2$。令 $c = \cos\theta, s = \sin\theta$，我们有：
$\rho(g(\theta))e_1 = c e_1 + s e_2$
$\rho(g(\theta))e_2 = -s e_1 + c e_2$

现在我们计算表示矩阵的列向量，即[基向量](@entry_id:199546)的像在基 $B$ 下的坐标 [@problem_id:1643937]：
1.  对 $b_1$ 的作用：
    $(\rho(g)e_1) \otimes (\rho(g)e_1) = (c e_1 + s e_2) \otimes (c e_1 + s e_2) = c^2 (e_1 \otimes e_1) + cs (e_1 \otimes e_2 + e_2 \otimes e_1) + s^2 (e_2 \otimes e_2) = c^2 b_1 + cs b_2 + s^2 b_3$.
2.  对 $b_2$ 的作用：
    $(\rho(g)e_1) \otimes (\rho(g)e_2) + (\rho(g)e_2) \otimes (\rho(g)e_1) = (c e_1 + s e_2) \otimes (-s e_1 + c e_2) + (-s e_1 + c e_2) \otimes (c e_1 + s e_2) = -2sc(e_1 \otimes e_1) + (c^2-s^2)(e_1 \otimes e_2 + e_2 \otimes e_1) + 2sc(e_2 \otimes e_2) = -2sc b_1 + (c^2-s^2) b_2 + 2sc b_3$.
3.  对 $b_3$ 的作用：
    $(\rho(g)e_2) \otimes (\rho(g)e_2) = (-s e_1 + c e_2) \otimes (-s e_1 + c e_2) = s^2(e_1 \otimes e_1) - sc(e_1 \otimes e_2 + e_2 \otimes e_1) + c^2(e_2 \otimes e_2) = s^2 b_1 - sc b_2 + c^2 b_3$.

将这些坐标作为列向量，我们得到 $\rho_{S^2(V)}(g(\theta))$ 在基 $B$ 下的矩阵：
$$
\rho_{S^2(V)}(g(\theta)) = \begin{pmatrix} c^2  -2sc  s^2 \\ cs  c^2-s^2  -sc \\ s^2  2sc  c^2 \end{pmatrix}
$$
这个例子清晰地展示了从原表示的矩阵到一个新表示（[对称平方](@entry_id:137676)表示）矩阵的具体构造过程。

一个重要的普适性质是，如果两个表示 $\rho_1$ 和 $\rho_2$ 是同构的，那么它们的[对称平方](@entry_id:137676)表示 $Sym^2(\rho_1)$ 和 $Sym^2(\rho_2)$ 也是同构的。这是因为同构意味着存在一个可逆的[线性映射](@entry_id:185132) $T$ 使得 $T \rho_1(g) = \rho_2(g) T$ 对所有 $g \in G$ 成立。这个映射可以自然地提升为 $T \otimes T$，它将建立起 $Sym^2(\rho_1)$ 和 $Sym^2(\rho_2)$ 之间的同构关系。在实践中，验证表示是否同构最有效的方法是比较它们的特征标，我们将在下一节讨论这一点 [@problem_id:1643954]。

### [对称平方](@entry_id:137676)的特征标

特征标是表示论中一个极其强大的工具。一个表示 $(\rho, V)$ 的**特征标 (character)** 是一个函数 $\chi_V: G \to \mathbb{C}$，定义为 $\chi_V(g) = \text{Tr}(\rho(g))$。特征标是类函数，即在群的每个共轭类上取值恒定。两个有限维[复表示](@entry_id:144331)是同构的，当且仅当它们的特征标完全相同。

我们可以推导[对称平方](@entry_id:137676)[表示的特征标](@entry_id:198072)公式。首先，[张量积表示](@entry_id:143629) $(\rho \otimes \rho, V \otimes V)$ 的特征标为：
$$
\chi_{V \otimes V}(g) = \text{Tr}((\rho \otimes \rho)(g)) = \text{Tr}(\rho(g) \otimes \rho(g))
$$
利用迹的一个标准性质 $\text{Tr}(A \otimes B) = \text{Tr}(A)\text{Tr}(B)$，我们得到：
$$
\chi_{V \otimes V}(g) = (\text{Tr}(\rho(g)))^2 = (\chi_V(g))^2
$$

为了得到 $S^2(V)$ 的特征标，我们利用投影算子。将 $V \otimes V$ 投影到[子空间](@entry_id:150286) $S^2(V)$ 上的投影算子是 $P_+ = \frac{1}{2}(\text{id} + \tau)$。因此，$\rho_{S^2(V)}(g)$ 的迹等于 $(\rho \otimes \rho)(g)$ 在 $S^2(V)$ [子空间](@entry_id:150286)上的迹，这可以通过先应用 $(\rho \otimes \rho)(g)$ 再投影到 $S^2(V)$ 来计算，即 $\text{Tr}(P_+ (\rho \otimes \rho)(g))$。
$$
\chi_{S^2(V)}(g) = \text{Tr}(P_+ (\rho \otimes \rho)(g)) = \text{Tr}\left(\frac{1}{2}(\text{id} + \tau)(\rho \otimes \rho)(g)\right) = \frac{1}{2} \left[ \text{Tr}((\rho \otimes \rho)(g)) + \text{Tr}(\tau (\rho \otimes \rho)(g)) \right]
$$
我们已经知道第一项是 $(\chi_V(g))^2$。对于第二项，我们需要计算 $\text{Tr}(\tau (\rho(g) \otimes \rho(g)))$。这里有一个关键的[迹恒等式](@entry_id:188149)：对于任意两个 $V$ 上的线性算子 $A, B$，有 $\text{Tr}(\tau(A \otimes B)) = \text{Tr}(AB)$。

令 $A = B = \rho(g)$，我们得到：
$$
\text{Tr}(\tau (\rho(g) \otimes \rho(g))) = \text{Tr}(\rho(g)^2) = \text{Tr}(\rho(g^2)) = \chi_V(g^2)
$$
将这两部分合并，我们得到了[对称平方](@entry_id:137676)特征标的中心公式 [@problem_id:1643903] [@problem_id:1643956]：
$$
\chi_{S^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 + \chi_V(g^2) \right]
$$
通过类似的推导（使用[投影算子](@entry_id:154142) $P_- = \frac{1}{2}(\text{id} - \tau)$），我们也可以得到交错平方的[特征标公式](@entry_id:142515)：
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 - \chi_V(g^2) \right]
$$
注意，这两个特征标之和恰好是 $(\chi_V(g))^2$，这与 $V \otimes V = S^2(V) \oplus \Lambda^2(V)$ 的[表示分解](@entry_id:139061)是一致的。

除了[特征标公式](@entry_id:142515)，还有一种理解[对称平方](@entry_id:137676)表示作用的方式，即通过分析其谱（[特征值](@entry_id:154894)）。如果算子 $\rho(g)$ 在 $V$ 上是可对角化的，其[特征值](@entry_id:154894)为 $\{\lambda_1, \dots, \lambda_n\}$，那么算子 $(\rho \otimes \rho)(g)$ 在 $V \otimes V$ 上的[特征值](@entry_id:154894)就是所有的两两乘积 $\{\lambda_i \lambda_j\}_{1 \le i,j \le n}$。[对称平方](@entry_id:137676)表示 $\rho_{S^2(V)}(g)$ 作用在 $S^2(V)$ 上，其[特征值](@entry_id:154894)集合正是这些乘积中的对称部分，即 $\{\lambda_i \lambda_j\}_{1 \le i \le j}$。这个集合包含 $n$ 个平方项 $\lambda_i^2$ 和 $\binom{n}{2}$ 个混合项 $\lambda_i \lambda_j$ ($i  j$)，总数为 $\frac{n(n+1)}{2}$，与 $S^2(V)$ 的维数相符。

例如，考虑一个算子 $A$，其[特征值](@entry_id:154894)为 $\{1, \omega, \omega^2\}$，其中 $\omega = \exp(2\pi i/3)$ 是三次[单位根](@entry_id:143302) [@problem_id:1643943]。那么，诱导在 $S^2(V)$ 上的算子 $A_{Sym^2}$ 的[特征值](@entry_id:154894)由所有成对的乘积 $\lambda_i \lambda_j$ (其中 $i \le j$) 给出：
- 平方项: $1^2=1$, $\omega^2$, $(\omega^2)^2=\omega^4=\omega$。
- 混合项: $1 \cdot \omega = \omega$, $1 \cdot \omega^2 = \omega^2$, $\omega \cdot \omega^2 = \omega^3=1$。
因此，$A_{Sym^2}$ 的[特征值](@entry_id:154894)多重集为 $\{1, 1, \omega, \omega, \omega^2, \omega^2\}$。这些[特征值](@entry_id:154894)的和就是 $\chi_{S^2(V)}(g) = 2(1+\omega+\omega^2) = 0$。我们也可以用[特征标公式](@entry_id:142515)验证这一点：$\chi_V(g) = 1+\omega+\omega^2 = 0$，而 $g^2$ 的[特征值](@entry_id:154894)为 $\{1^2, \omega^2, (\omega^2)^2\} = \{1, \omega^2, \omega\}$，所以 $\chi_V(g^2)=0$。代入公式得 $\chi_{S^2(V)}(g) = \frac{1}{2}[0^2+0]=0$，结果一致。

### 关键性质与应用

[对称平方](@entry_id:137676)构造不仅在理论上十分优美，在实际应用中也扮演着重要角色。

#### 对偶性

一个表示 $(\rho, V)$ 的**[对偶表示](@entry_id:146263) (dual representation)** $(\rho^*, V^*)$ 定义在[对偶空间](@entry_id:146945) $V^*$ 上，其特征标为原特征标的复共轭：$\chi_{V^*}(g) = \overline{\chi_V(g)}$。一个自然的问题是，对一个表示先作[对称平方](@entry_id:137676)再取对偶，与先取对偶再作[对称平方](@entry_id:137676)，得到的结果是否相同？即，$(S^2 V)^*$ 和 $S^2(V^*)$ 是否同构？

我们可以通过比较它们的特征标来回答这个问题 [@problem_id:1643926]。
$$
\chi_{(S^2 V)^*}(g) = \overline{\chi_{S^2 V}(g)} = \overline{\frac{1}{2}[(\chi_V(g))^2 + \chi_V(g^2)]} = \frac{1}{2}[\overline{(\chi_V(g))^2} + \overline{\chi_V(g^2)}]
$$
对于[复表示](@entry_id:144331)，有 $\overline{\chi_V(g^2)} = \chi_{V^*}(g^2)$ 和 $\overline{(\chi_V(g))^2} = (\overline{\chi_V(g)})^2 = (\chi_{V^*}(g))^2$。因此：
$$
\chi_{(S^2 V)^*}(g) = \frac{1}{2}[(\chi_{V^*}(g))^2 + \chi_{V^*}(g^2)]
$$
这正是 $S^2(V^*)$ 的[特征标公式](@entry_id:142515) $\chi_{S^2(V^*)}(g)$。由于它们的特征标相同，所以我们得出结论：对于任意有限维[复表示](@entry_id:144331) $V$，我们有表示的同构关系：
$$
(S^2 V)^* \cong S^2(V^*)
$$

#### 不变[对称双线性形式](@entry_id:148281)

[对称平方](@entry_id:137676)的一个深刻应用在于它与**双线性形式 (bilinear forms)** 的联系。一个定义在 $V$ 上的双线性形式是一个映射 $B: V \times V \to \mathbb{F}$，它在每个变量上都是线性的。如果 $B(v, w) = B(w, v)$，则称其为**对称的**。所有 $V$ 上的[对称双线性形式](@entry_id:148281)构成的空间，与[对偶空间](@entry_id:146945)的[对称平方](@entry_id:137676) $S^2(V^*)$ 是同构的。

如果 $V$ 是一个群 $G$ 的表示空间，一个双线性形式 $B$ 被称为 **$G$-不变的**，如果对于所有 $g \in G$ 和 $v, w \in V$ 都满足：
$$
B(\rho(g)v, \rho(g)w) = B(v, w)
$$
$G$-不变的[对称双线性形式](@entry_id:148281)构成的空间，其维数等于 $S^2(V^*)$ 中**[平凡表示](@entry_id:141357) (trivial representation)** 的重数。[平凡表示](@entry_id:141357)是指所有群元都作用为[恒等变换](@entry_id:264671)的[一维表示](@entry_id:136509)，其特征标恒为 1。

对于[复数域](@entry_id:153768)上的[有限群](@entry_id:139710)表示，一个表示与其[对偶表示](@entry_id:146263)同构当且仅当其特征标是实值的。在这种常见情况下，$S^2(V^*) \cong S^2(V)$，因此不变[对称双线性形式](@entry_id:148281)空间的维数就等于[平凡表示](@entry_id:141357)在 $S^2(V)$ 中的[重数](@entry_id:136466)。这个重数可以通过[特征标内积](@entry_id:137125)公式计算：
$$
m_1 = \langle \chi_{S^2(V)}, \chi_{1_G} \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_{S^2(V)}(g)
$$

让我们看一个例子 [@problem_id:1643919]。考虑置换群 $S_3$ 在三维空间 $W=\mathbb{C}^3$ 上的[置换表示](@entry_id:142960)，$\rho(\sigma)e_i = e_{\sigma(i)}$。$S_3$ 有三个共轭类：单位元 $e$，[对换](@entry_id:142115)（如 $(12)$），三轮换（如 $(123)$）。该[表示的特征标](@entry_id:198072) $\chi_W$ 在这三个类上的取值分别为 $(3, 1, 0)$（一个[置换](@entry_id:136432)的迹等于它固定的[基向量](@entry_id:199546)的数目）。由于特征标是实值的，我们可以直接计算 $S^2(W)$ 中平凡[表示的[重](@entry_id:138441)数](@entry_id:136466)。
首先计算 $\chi_{S^2(W)}$：
- $g=e$: $\chi_{S^2(W)}(e) = \frac{1}{2}[(\chi_W(e))^2 + \chi_W(e^2)] = \frac{1}{2}[3^2 + 3] = 6$。
- $g=(12)$: $g^2=e$。$\chi_{S^2(W)}((12)) = \frac{1}{2}[(\chi_W((12)))^2 + \chi_W(e)] = \frac{1}{2}[1^2 + 3] = 2$。
- $g=(123)$: $g^2=(132)$，与 $g$ 在同一[共轭类](@entry_id:143916)。$\chi_{S^2(W)}((123)) = \frac{1}{2}[(\chi_W((123)))^2 + \chi_W((132))] = \frac{1}{2}[0^2 + 0] = 0$。

$S_3$ 中三个共轭类的大小分别为 1, 3, 2。因此，不变[对称双线性形式](@entry_id:148281)空间的维数是：
$$
m_1 = \frac{1}{6} [1 \cdot \chi_{S^2(W)}(e) + 3 \cdot \chi_{S^2(W)}((12)) + 2 \cdot \chi_{S^2(W)}((123))] = \frac{1}{6}[1 \cdot 6 + 3 \cdot 2 + 2 \cdot 0] = \frac{12}{6} = 2
$$
这意味着在 $W$ 上存在一个二维的 $S_3$-不变[对称双线性形式](@entry_id:148281)空间。

#### Frobenius-Schur 指标

上述讨论引出了一个更深层的概念——**Frobenius-Schur 指标 (Frobenius-Schur indicator)**。对于一个不可约[复表示](@entry_id:144331) $V$，其指标定义为：
$$
\nu(V) = \frac{1}{|G|} \sum_{g \in G} \chi_V(g^2)
$$
这个指标的值只能是 $1, 0, -1$ 中的一个，并揭示了表示 $V$ 的“实数”性质：
- $\nu(V) = 1$：$V$ 是**[实表示](@entry_id:146117)**（可以在实数域上实现）。
- $\nu(V) = 0$：$V$ 是**[复表示](@entry_id:144331)**（非[实表示](@entry_id:146117)，且 $V \not\cong V^*$）。
- $\nu(V) = -1$：$V$ 是**[四元数表示](@entry_id:146458)**（非[实表示](@entry_id:146117)，但 $V \cong V^*$）。

$S^2(V)$ 中平凡[表示的[重](@entry_id:138441)数](@entry_id:136466)与这个指标紧密相关。对于一个[不可约表示](@entry_id:263310) $V$，这个[重数](@entry_id:136466)是：
$$
\langle \chi_{S^2(V)}, \chi_{1_G} \rangle = \frac{1}{|G|} \sum_{g \in G} \frac{1}{2} [(\chi_V(g))^2 + \chi_V(g^2)] = \frac{1}{2} \left( \frac{1}{|G|} \sum_{g \in G} (\chi_V(g))^2 + \frac{1}{|G|} \sum_{g \in G} \chi_V(g^2) \right)
$$
由于 $V$ 不可约，$\frac{1}{|G|} \sum_{g \in G} (\chi_V(g))^2 = \langle \chi_V, \overline{\chi_V} \rangle$。如果 $V \cong V^*$（实或[四元数](@entry_id:147023)类型），则 $\overline{\chi_V}=\chi_V$，此[内积](@entry_id:158127)为 1。如果 $V$ 是复类型，则 $\overline{\chi_V}$ 是另一个不同构的不可约[表示的特征标](@entry_id:198072)，[内积](@entry_id:158127)为 0。结合 Frobenius-Schur 指标的定义，我们有：
- 如果 $\nu(V)=1$ (实类型)，[重数](@entry_id:136466)为 $\frac{1}{2}(1+1)=1$。
- 如果 $\nu(V)=0$ (复类型)，重数为 $\frac{1}{2}(0+0)=0$。
- 如果 $\nu(V)=-1$ ([四元数](@entry_id:147023)类型)，重数为 $\frac{1}{2}(1-1)=0$。

因此，一个不可约表示 $V$ 容许一个非零的 $G$-不变[对称双线性形式](@entry_id:148281)，当且仅当它是[实表示](@entry_id:146117)。

让我们考察[四元数群](@entry_id:147721) $Q_8 = \{\pm 1, \pm i, \pm j, \pm k\}$ 的唯一二维[不可约表示](@entry_id:263310) $V$ [@problem_id:1643965]。其特征标为 $\chi_V(1)=2, \chi_V(-1)=-2$，在其他元素上为 0。我们来计算 $S^2(V)$ 中平凡[表示的[重](@entry_id:138441)数](@entry_id:136466)。
首先计算 $\chi_{S^2(V)}$ 在各元素上的值：
- $g=1, g^2=1$: $\chi_{S^2(V)}(1) = \frac{1}{2}[2^2 + \chi_V(1)] = \frac{1}{2}[4+2] = 3$。
- $g=-1, g^2=1$: $\chi_{S^2(V)}(-1) = \frac{1}{2}[(-2)^2 + \chi_V(1)] = \frac{1}{2}[4+2] = 3$。
- 对于 $g \in \{\pm i, \pm j, \pm k\}$，$g^2=-1$: $\chi_{S^2(V)}(g) = \frac{1}{2}[0^2 + \chi_V(-1)] = \frac{1}{2}[-2] = -1$。

$S^2(V)$ 中平凡[表示的重数](@entry_id:138441)为：
$$
m_1 = \frac{1}{8} [ \chi_{S^2(V)}(1) + \chi_{S^2(V)}(-1) + \sum_{g \in \{\pm i, \pm j, \pm k\}} \chi_{S^2(V)}(g) ] = \frac{1}{8} [3 + 3 + 6 \cdot (-1)] = \frac{1}{8}[6 - 6] = 0
$$
结果为 0，这与我们的理论预测一致，因为这个二维表示是四元数类型的 ($\nu(V)=-1$)。

### 关于特征2域的注记

我们之前的所有讨论都隐含地假设[域的特征](@entry_id:154386)不为 2。当域 $F$ 的特征为 2 时，情况变得复杂得多。主要问题在于 $2=0$，这导致分解 $V \otimes V = S^2(V) \oplus \Lambda^2(V)$ 失效，因为投影算子 $\frac{1}{2}(\text{id} \pm \tau)$ 没有定义。

在这种情况下，我们仍然可以定义**[对称张量](@entry_id:148092)[子空间](@entry_id:150286)** $U$ 和**[对称张量](@entry_id:148092)[商空间](@entry_id:274314)** $W$：
1.  $U = \{x \in V \otimes V \mid \tau(x)=x\} = \ker(\text{id}+\tau)$（因为 $x= \tau(x) \iff x+\tau(x)=0$）
2.  $W = (V \otimes V) / K$，其中 $K = \text{span}\{y-\tau(y) \mid y \in V \otimes V\} = \text{im}(\text{id}+\tau)$

在特征为 2 的情况下，$U$ 和 $W$ 通常是**不同构**的 $G$-表示。它们之间的关系更为微妙 [@problem_id:1643947]。注意到算子 $\phi = \text{id}+\tau$ 满足 $\phi^2 = (\text{id}+\tau)^2 = \text{id}^2 + 2\tau + \tau^2 = \text{id} + 0 + \text{id} = 0$。这意味着 $\text{im}(\phi) \subseteq \ker(\phi)$，即 $K \subseteq U$。

这个包含关系 $K \subseteq U$ 意味着我们可以定义商表示 $U/K$。可以证明，$W$ 包含一个同构于 $U/K$ 的[子表示](@entry_id:141094)，并且相应的商表示同构于 $K$。这可以用一个短[正合序列](@entry_id:151503)来描述：
$$
0 \to U/K \to W \to K \to 0
$$
这个结果揭示了在特征为 2 的域上，对称性的[代数结构](@entry_id:137052)比在特征为 0 的域上要复杂得多，它为[模表示论](@entry_id:147491)（modular representation theory）的研究提供了有趣的例子。