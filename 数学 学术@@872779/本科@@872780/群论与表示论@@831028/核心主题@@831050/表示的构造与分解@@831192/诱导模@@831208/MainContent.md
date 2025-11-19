## 引言
在[群表示论](@entry_id:141930)的宏伟画卷中，理解一个群的结构与对称性，其关键在于剖析其[不可约表示](@entry_id:263310)。然而，直接构造和分析一个复杂[群的表示](@entry_id:140711)往往极其困难。这就引出了一个核心问题：我们能否利用已知的、来自更小或更简单结构（如[子群](@entry_id:146164)）的信息，来系统地构建和理解整个[群的表示](@entry_id:140711)？

[诱导模](@entry_id:137976) (Induced Module) 正是解答这一问题的强大工具。它提供了一条代数路径，可以将子群的表示“提升”或“诱导”为整个[群的表示](@entry_id:140711)，从而成为连接简单与复杂、局部与全局的桥梁。掌握[诱导表示](@entry_id:136842)不仅是深入学习表示论的必经之路，更是理解其在现代数学和物理学中广泛应用的基石。

本文将全面而系统地介绍[诱导模](@entry_id:137976)理论。在“原理与机制”一章中，我们将从[群代数](@entry_id:145139)的角度出发，给出[诱导模](@entry_id:137976)的严格定义，并探讨其维数、[特征标公式](@entry_id:142515)以及最重要的[Frobenius互反律](@entry_id:140909)。接着，在“应用与跨学科联系”一章中，我们将展示[诱导模](@entry_id:137976)如何用于构造[置换表示](@entry_id:142960)、借助麦基理论分析不可约性，并揭示其在数论、[组合数学](@entry_id:144343)及固体物理等领域的深刻影响。最后，“实践练习”部分将提供一系列具体问题，帮助读者巩固理论知识，并将抽象概念付诸实践。

通过这三部分的学习，读者将能够深刻理解[诱导模](@entry_id:137976)的[构造原理](@entry_id:141667)，熟练运用其关键性质进行计算与分析，并领会其作为基础工具的强大威力与广泛适用性。

## 原理与机制

在上一章介绍表示论的基本概念之后，我们现在转向一个更为高级但极其强大的构造工具：**[诱导表示](@entry_id:136842) (induced representation)**。[表示论](@entry_id:137998)的一个核心任务是从已知的、更简单的表示（例如子[群的表示](@entry_id:140711)）来构建和理解更复杂的表示（例如整个[群的表示](@entry_id:140711)）。[诱导表示](@entry_id:136842)正是实现这一目标的主要途径。它允许我们将一个[子群](@entry_id:146164) $H$ 的表示“提升”为整个群 $G$ 的一个表示。本章将深入探讨[诱导表示](@entry_id:136842)的定义、基本原理、关键性质以及其在[表示分解](@entry_id:139061)中的核心作用。

### [诱导表示](@entry_id:136842)的定义与构造

假设我们有一个群 $G$ 和它的一个[子群](@entry_id:146164) $H$。如果我们已经有了一个 $H$ 的表示，即一个[向量空间](@entry_id:151108) $W$ 以及一个[群同态](@entry_id:140603) $\rho: H \to GL(W)$，我们如何利用这些信息来构造一个 $G$ 的表示呢？

最现代且最强大的方法是通过[群代数](@entry_id:145139)的语言来定义。一个群 $H$ 在域 $\mathbb{C}$ 上的表示 $W$ 等价于一个左 $\mathbb{C}[H]$-模。我们的目标是利用这个 $\mathbb{C}[H]$-模 $W$ 来构建一个左 $\mathbb{C}[G]$-模。这里的 $\mathbb{C}[G]$ 和 $\mathbb{C}[H]$ 分别是群 $G$ 和 $H$ 在[复数域](@entry_id:153768)上的**[群代数](@entry_id:145139)**。

这个构造的核心工具是**[张量积](@entry_id:140694) (tensor product)**。我们将 $\mathbb{C}[G]$ 视为一个 $(\mathbb{C}[G], \mathbb{C}[H])$-双模，其中左乘来自 $\mathbb{C}[G]$，右乘来自 $\mathbb{C}[H]$。

**定义 ([诱导表示](@entry_id:136842))**：设 $H$ 是 $G$ 的一个[子群](@entry_id:146164)，$W$ 是一个 $\mathbb{C}[H]$-模（即 $H$ 的一个表示空间）。从 $H$ 到 $G$ 的**[诱导模](@entry_id:137976) (induced module)**，记作 $\operatorname{Ind}_H^G W$，定义为如下的张量积：
$$ \operatorname{Ind}_H^G W = \mathbb{C}[G] \otimes_{\mathbb{C}[H]} W $$
这个构造的结果是一个左 $\mathbb{C}[G]$-模，因为 $\mathbb{C}[G]$ 本身是一个左 $\mathbb{C}[G]$-模，这个作用自然地传递给了张量积。因此，$\operatorname{Ind}_H^G W$ 构成了一个 $G$ 的表示。

这个定义虽然抽象，但它引出了一个至关重要的具体结果——[诱导表示](@entry_id:136842)的维数。

**定理 ([诱导表示](@entry_id:136842)的维数)**：[诱导表示](@entry_id:136842) $\operatorname{Ind}_H^G W$ 的维数等于 $H$ 在 $G$ 中的指数乘以 $W$ 的维数。
$$ \dim(\operatorname{Ind}_H^G W) = [G:H] \cdot \dim(W) $$
其中 $[G:H] = |G|/|H|$ 是[子群](@entry_id:146164) $H$ 在 $G$ 中的指数。

为了理解这个公式，我们可以考虑 $G$ 关于 $H$ 的[左陪集](@entry_id:143879)分解 $G = \bigcup_{i=1}^n g_i H$，其中 $g_1, \dots, g_n$ 是一组[陪集](@entry_id:147145)代表元，且 $n = [G:H]$。作为右 $\mathbb{C}[H]$-模，[群代数](@entry_id:145139) $\mathbb{C}[G]$ 可以分解为自由[模的[直](@entry_id:156308)和](@entry_id:156782)：
$$ \mathbb{C}[G] \cong \bigoplus_{i=1}^n g_i \mathbb{C}[H] $$
当我们在这个同构的两边与 $W$ 在 $\mathbb{C}[H]$ 上作[张量积](@entry_id:140694)时，张量积的分配律告诉我们：
$$ \operatorname{Ind}_H^G W = \mathbb{C}[G] \otimes_{\mathbb{C}[H]} W \cong \left(\bigoplus_{i=1}^n g_i \mathbb{C}[H]\right) \otimes_{\mathbb{C}[H]} W \cong \bigoplus_{i=1}^n (g_i \mathbb{C}[H] \otimes_{\mathbb{C}[H]} W) $$
由于 $g_i$ 是[陪集](@entry_id:147145)代表元，每个 $g_i \mathbb{C}[H]$ 在结构上与 $\mathbb{C}[H]$ 同构，因此 $g_i \mathbb{C}[H] \otimes_{\mathbb{C}[H]} W$ 与 $W$ 同构。最终我们得到：
$$ \operatorname{Ind}_H^G W \cong \bigoplus_{i=1}^n W $$
这是一个由 $n$ 个 $W$ 的拷贝构成的直和空间。因此，其维数自然是 $n \cdot \dim(W)$。

例如，假设 $H$ 是群 $G$ 的一个[子群](@entry_id:146164)，其指数 $[G:H]=3$。如果我们有一个 $H$ 的 2 维表示 $W$，那么诱导到 $G$ 的表示 $\operatorname{Ind}_H^G W$ 的维数就是 $[G:H] \cdot \dim(W) = 3 \cdot 2 = 6$ [@problem_id:1650423]。这个简单的公式是我们在处理[诱导表示](@entry_id:136842)时首先要掌握的工具。

### 诱导的基本性质

诱导作为一个操作，具有几个非常优美的代数性质，这些性质极大地简化了计算和理论推导。

#### 可加性

诱导操作对于[表示的直和](@entry_id:138310)是可分配的。这意味着如果 $H$ 的一个表示 $W$ 可以分解为两个子[表示的直和](@entry_id:138310) $W = W_1 \oplus W_2$，那么诱导到 $G$ 的表示也遵循同样的分解。

**定理 (可加性)**：设 $W_1$ 和 $W_2$ 是 $H$ 的两个表示，则存在一个 $G$-表示的同构：
$$ \operatorname{Ind}_H^G(W_1 \oplus W_2) \cong (\operatorname{Ind}_H^G W_1) \oplus (\operatorname{Ind}_H^G W_2) $$
这个性质源于张量积对直和的[分配律](@entry_id:144084)。它告诉我们，要理解一个复杂表示的诱导，我们可以先将其分解为[不可约表示](@entry_id:263310)，然后分别诱导每一个部分，最后再将结果合成为直和。

例如，考虑[对称群](@entry_id:146083) $G=S_3$ 和其[子群](@entry_id:146164) $H=\{e, (12)\}$。$H$ 是一个二阶循环群，它有两个一维不可约表示：[平凡表示](@entry_id:141357) $W_1$（特征标为 $\chi_1(e)=1, \chi_1(12)=1$）和符号表示 $W_2$（特征标为 $\chi_2(e)=1, \chi_2(12)=-1$）。如果我们想分析 $H$ 的正规表示 $W = \mathbb{C}[H] = W_1 \oplus W_2$ 的[诱导表示](@entry_id:136842) $V = \operatorname{Ind}_H^G W$，我们可以利用可加性，分别计算 $\operatorname{Ind}_H^G W_1$ 和 $\operatorname{Ind}_H^G W_2$，然后将它们的结果相加 [@problem_id:1650388]。

#### [诱导的传递性](@entry_id:139747)

如果存在一个[子群](@entry_id:146164)链 $K \subset H \subset G$，我们可以从 $K$ 直接诱导到 $G$，也可以分两步：先从 $K$ 诱导到 $H$，再从 $H$ 诱导到 $G$。一个深刻的结果是，这两种方式得到的是同一个表示。

**定理 ([诱导的传递性](@entry_id:139747))**：对于[子群](@entry_id:146164)链 $K \subset H \subset G$ 和 $K$ 的一个表示 $V$，存在一个 $G$-表示的同构：
$$ \operatorname{Ind}_K^G V \cong \operatorname{Ind}_H^G(\operatorname{Ind}_K^H V) $$
这个性质可以用张量积的[结合律](@entry_id:151180)来优雅地证明 [@problem_id:1650415]。根据定义，两步诱导过程的结果是：
$$ \operatorname{Ind}_H^G(\operatorname{Ind}_K^H V) = \mathbb{C}[G] \otimes_{\mathbb{C}[H]} (\mathbb{C}[H] \otimes_{\mathbb{C}[K]} V) $$
由于张量积的结合律，上式同构于：
$$ (\mathbb{C}[G] \otimes_{\mathbb{C}[H]} \mathbb{C}[H]) \otimes_{\mathbb{C}[K]} V $$
而 $\mathbb{C}[G] \otimes_{\mathbb{C}[H]} \mathbb{C}[H]$ 自然同构于 $\mathbb{C}[G]$，因此整个表达式简化为 $\mathbb{C}[G] \otimes_{\mathbb{C}[K]} V$，这正是 $\operatorname{Ind}_K^G V$ 的定义。这个“分步诱导”的性质在理论推导中非常有用。

#### 正规表示的诱导

一个特别重要且具有启发性的例子是诱导[子群](@entry_id:146164) $H$ 的正规表示 $\mathbb{C}[H]$。结果是，我们得到了整个群 $G$ 的正规表示 $\mathbb{C}[G]$。

**定理**：$\operatorname{Ind}_H^G(\mathbb{C}[H]) \cong \mathbb{C}[G]$。
这个同构可以通过映射 $m: \mathbb{C}[G] \otimes_{\mathbb{C}[H]} \mathbb{C}[H] \to \mathbb{C}[G]$，$m(x \otimes y) = xy$ 来建立 [@problem_id:1650404]。

这个结果意义非凡。我们知道，任何一个有限群 $G$ 的正规表示 $\mathbb{C}[G]$ 的分解包含了 $G$ 的所有[不可约表示](@entry_id:263310)，并且每个不可约表示 $V_\rho$ 的[重数](@entry_id:136466)等于它的维数 $\dim(V_\rho)$。因此，通过诱导 $H$ 的正规表示，我们实际上构造了一个包含 $G$ 所有不可约信息的大表示。例如，对于 $G=S_3$，其不可约表示为一维的[平凡表示](@entry_id:141357) $V_{triv}$、一维的符号表示 $V_{sign}$ 和二维的标准表示 $V_{std}$。$S_3$ 的正规[表示分解](@entry_id:139061)为 $V_{triv} \oplus V_{sign} \oplus 2V_{std}$。因此，通过诱导 $S_3$ 的任意子群 $H$ 的正规表示，我们都会得到这个包含所有 $S_3$ [不可约表示](@entry_id:263310)的 6 维表示 [@problem_id:1650404]。

### [诱导表示的特征标](@entry_id:145122)

尽管[诱导表示](@entry_id:136842)的定义较为抽象，但其特征标有一个具体的计算公式，这使得它成为一个强大的计算工具。

**定理 ([诱导特征标](@entry_id:143636)公式)**：设 $\psi$ 是[子群](@entry_id:146164) $H$ 的一个[表示的特征标](@entry_id:198072)。那么[诱导表示](@entry_id:136842) $\operatorname{Ind}_H^G \psi$ 的特征标 $\chi$ 在元素 $g \in G$ 上的取值为：
$$ \chi(g) = \frac{1}{|H|} \sum_{\substack{x \in G \\ x^{-1}gx \in H}} \psi(x^{-1}gx) $$
这个公式直观上可以理解为：对于一个给定的 $g \in G$，我们考察它在 $G$ 中的所有共轭元素 $x^{-1}gx$。我们只对那些恰好落在[子群](@entry_id:146164) $H$ 中的共轭元素感兴趣。然后，我们将 $H$ 的特征标 $\psi$ 应用于这些元素，并求和，最后进行归一化。

这个公式的一个直接推论是：如果元素 $g$ 的任何共轭都不在[子群](@entry_id:146164) $H$ 中，那么上述求和的[指标集](@entry_id:268489)为空集，特征标的值为 0 [@problem_id:1650355]。这是一个非常有用的快速判断法则。

让我们通过一个例子来演示这个公式的应用。考虑 $G=S_3$ 和[子群](@entry_id:146164) $H = \{e, (13)\}$。令 $\psi$ 是 $H$ 的一个非平凡一维特征标，即 $\psi(e)=1, \psi((13))=-1$。我们来计算[诱导特征标](@entry_id:143636) $\chi = \operatorname{Ind}_H^G \psi$ [@problem_id:1650418]。
$S_3$ 的[共轭类](@entry_id:143916)代表元为 $e$, $(12)$, $(123)$。
- **对于 $g=e$**：任何 $x \in G$ 都满足 $x^{-1}ex = e \in H$。因此，求和中有 $|G|=6$ 项，每一项都是 $\psi(e)=1$。
  $$ \chi(e) = \frac{1}{2} \sum_{x \in S_3} \psi(e) = \frac{1}{2} \cdot 6 \cdot 1 = 3 $$
  这与维数公式 $[G:H]\dim(W) = (6/2) \cdot 1 = 3$ 的结果一致。

- **对于 $g=(12)$ (一个二轮换)**：我们需要找到所有 $x \in S_3$，使得 $x^{-1}(12)x \in H=\{e, (13)\}$。由于[元素的阶](@entry_id:145276)在共轭下不变，所以 $x^{-1}(12)x$ 只能是 $(13)$。满足 $x^{-1}(12)x = (13)$ 的元素 $x$ 的数量等于 $g=(12)$ 的[中心化子的大小](@entry_id:137596) $|C_G(g)|$。在 $S_3$ 中，$|C_G((12))| = 2$。因此，求和中有 2 项，每一项的值都是 $\psi((13))=-1$。
  $$ \chi((12)) = \frac{1}{2} \cdot 2 \cdot (-1) = -1 $$

- **对于 $g=(123)$ (一个三轮换)**：它的所有共轭都是三轮换。[子群](@entry_id:146164) $H$ 中没有三轮换。因此，求和为[空集](@entry_id:261946)。
  $$ \chi((123)) = 0 $$
综上，[诱导特征标](@entry_id:143636)在三个共轭类上的值分别为 $(3, -1, 0)$。

通过另一个例子，考虑八阶[二面体群](@entry_id:143875) $D_8 = \langle r, s \mid r^4 = s^2 = 1, sr = r^3s \rangle$ 及其[子群](@entry_id:146164) $H = \{1, s\}$。令 $\chi$ 为 $H$ 的非平凡一维特征标，$\chi(1)=1, \chi(s)=-1$。[诱导特征标](@entry_id:143636) $\psi = \operatorname{Ind}_H^{D_8}\chi$ 在 $D_8$ 的五个[共轭类](@entry_id:143916)代表元 $1, r^2, r, s, sr$ 上的值可以按同样方法计算 [@problem_id:1650376]：
- $\psi(1) = [D_8:H] = 4$。
- $r^2$ 和 $r$ 的[共轭类](@entry_id:143916)均不与 $H$ 相交，因此 $\psi(r^2) = 0, \psi(r) = 0$。
- $s$ 的共轭需要落在 $H$ 中，只能是 $s$ 本身。满足 $x^{-1}sx=s$ 的元素 $x$ 构成 $s$ 的[中心化子](@entry_id:146604) $C_{D_8}(s)$，其大小为 4。因此 $\psi(s) = \frac{1}{2} |C_{D_8}(s)| \chi(s) = \frac{1}{2} \cdot 4 \cdot (-1) = -2$。
- $sr$ 的[共轭类](@entry_id:143916)不与 $H$ 相交，因此 $\psi(sr) = 0$。
最终得到的特征标向量为 $(4, 0, 0, -2, 0)$。

### [Frobenius互反律](@entry_id:140909)：[诱导与限制](@entry_id:182341)的对偶性

[诱导表示](@entry_id:136842)最深刻和最有用的性质是 **Frobenius [互反律](@entry_id:188215) (Frobenius Reciprocity)**。这个定理在诱导 ($\operatorname{Ind}$) 和我们之前可能已经熟悉的限制 (Restriction, $\operatorname{Res}$) 操作之间建立了一个优美的对偶关系。限制操作是将一个 $G$ 的表示 $V$ 看作其[子群](@entry_id:146164) $H$ 的表示，记作 $\operatorname{Res}_H^G V$。

**定理 (Frobenius [互反律](@entry_id:188215))**：设 $H$ 是 $G$ 的[子群](@entry_id:146164)，$W$ 是 $H$ 的表示， $V$ 是 $G$ 的表示。则存在一个[典范同构](@entry_id:202335)：
$$ \operatorname{Hom}_G(\operatorname{Ind}_H^G W, V) \cong \operatorname{Hom}_H(W, \operatorname{Res}_H^G V) $$
在特征标的语言中，这个定理表述为一个[内积](@entry_id:158127)的等式。设 $\psi$ 是 $W$ 的特征标，$\chi$ 是 $V$ 的特征标。
$$ \langle \operatorname{Ind}_H^G \psi, \chi \rangle_G = \langle \psi, \operatorname{Res}_H^G \chi \rangle_H $$
这里 $\langle \cdot, \cdot \rangle_G$ 和 $\langle \cdot, \cdot \rangle_H$ 分别是 $G$ 和 $H$ 上的[特征标内积](@entry_id:137125)。

这个定理的威力在于，它将一个在 $G$ 中计算的、可能很复杂的[内积](@entry_id:158127)（左边）转换为了一个在[子群](@entry_id:146164) $H$ 中计算的、通常简单得多的[内积](@entry_id:158127)（右边）。如果 $V$ 是 $G$ 的一个不可约表示，那么左边的[内积](@entry_id:158127) $\langle \operatorname{Ind}_H^G \psi, \chi \rangle_G$ 正是 $V$ 在[诱导表示](@entry_id:136842) $\operatorname{Ind}_H^G W$ 分解式中出现的**[重数](@entry_id:136466)**。这意味着我们可以通过在[子群](@entry_id:146164) $H$ 中做计算，来精确地确定一个[诱导表示](@entry_id:136842)如何分解为 $G$ 的不可约表示之和。

让我们看一个应用。设 $G=S_4$，$H$ 是由四轮换 $(1234)$ 生成的四阶[循环子群](@entry_id:138079)。设 $W$ 是 $H$ 的一个[一维表示](@entry_id:136509)，其生成元 $(1234)$ 的作用为乘以 $i = \sqrt{-1}$。我们想知道 $S_4$ 的一个 3 维不可约表示 $V$（其特征标为 $\chi_4=(3, 1, 0, -1, -1)$）在[诱导表示](@entry_id:136842) $\operatorname{Ind}_H^G W$ 中出现了多少次？[@problem_id:1650400]

根据 Frobenius [互反律](@entry_id:188215)，这个[重数](@entry_id:136466) $m$ 等于：
$$ m = \langle \operatorname{Ind}_H^G \psi, \chi_4 \rangle_G = \langle \psi, \operatorname{Res}_H^G \chi_4 \rangle_H $$
我们只需计算右边的[内积](@entry_id:158127)。[子群](@entry_id:146164) $H=\{e, (1234), (13)(24), (1432)\}$。$H$ 的特征标 $\psi$ 在这些元素上的值分别为 $1, i, -1, -i$。$G$ 的特征标 $\chi_4$ 限制在 $H$ 上的值，可以从 $S_4$ 的[特征标表](@entry_id:146676)中查到，分别为 $\chi_4(e)=3, \chi_4((1234))=-1, \chi_4((13)(24))=-1, \chi_4((1432))=-1$。
于是，
$$ m = \frac{1}{|H|} \sum_{h \in H} \psi(h) \overline{\chi_4(h)} = \frac{1}{4} [ \psi(e)\overline{\chi_4(e)} + \psi(\sigma)\overline{\chi_4(\sigma)} + \psi(\sigma^2)\overline{\chi_4(\sigma^2)} + \psi(\sigma^3)\overline{\chi_4(\sigma^3)} ] $$
$$ m = \frac{1}{4} [ 1 \cdot 3 + i \cdot \overline{(-1)} + (-1) \cdot \overline{(-1)} + (-i) \cdot \overline{(-1)} ] = \frac{1}{4} [3 - i + 1 + i] = \frac{4}{4} = 1 $$
计算结果表明，这个 3 维[不可约表示](@entry_id:263310) $V$ 在[诱导表示](@entry_id:136842)中恰好出现一次。

当[子群](@entry_id:146164) $H$ 是 $G$ 的[正规子群](@entry_id:147397)时，Frobenius [互反律](@entry_id:188215)与 Clifford 理论结合，可以系统地分析诱导[表示的分解](@entry_id:147581)结构。例如，对于 $G=S_4$ 及其正规子群 Klein 四元群 $H=V_4$，我们可以用[互反律](@entry_id:188215)来确定从 $H$ 的任何一个[一维表示](@entry_id:136509) $W$ 诱导得到的 6 维[表示的分解](@entry_id:147581)方式。计算表明，对于 $H$ 的某个非平凡[一维表示](@entry_id:136509) $W$，$\operatorname{Ind}_H^G W$ 会分解为两个不同的 3 维[不可约表示](@entry_id:263310)的直和 [@problem_id:1650399]。

### [诱导表示](@entry_id:136842)的进阶恒等式

最后，我们介绍一个涉及[张量积](@entry_id:140694)的更高级的恒等式，它有时被称为**[投影公式](@entry_id:152164) (Projection Formula)** 或张量恒等式。

**定理 (张量恒等式)**：设 $V$ 是[子群](@entry_id:146164) $H$ 的表示，$W$ 是群 $G$ 的表示。则存在一个 $G$-表示的同构：
$$ (\operatorname{Ind}_H^G V) \otimes W \cong \operatorname{Ind}_H^G (V \otimes \operatorname{Res}_H^G W) $$
这个恒等式将一个在 $G$ 中计算的张量积（左侧）与一个先在[子群](@entry_id:146164) $H$ 中计算张量积再进行诱导的过程（右侧）联系起来。在特征标层面，这意味着：
$$ \chi_{\operatorname{Ind} V} \cdot \chi_W = \chi_{\operatorname{Ind}(V \otimes \operatorname{Res} W)} $$
在实际计算中，我们常常只需要一个更简单的事实：两个表示的[张量积的特征标](@entry_id:143383)是它们各自特征标的逐点乘积，即 $\chi_{A \otimes B} = \chi_A \cdot \chi_B$。

让我们考虑一个计算问题：设 $G=S_4$，$H$ 是其一个 8 阶二面体[子群](@entry_id:146164)。令 $U$ 是 $H$ 的一个特定的[一维表示](@entry_id:136509)，$W_{std}$ 是 $S_4$ 的 3 维标准表示。我们想计算表示 $V = (\operatorname{Ind}_H^G U) \otimes W_{std}$ 在元素 $g=(12)(34)$ 处的特征标值 [@problem_id:1650417]。

利用特征标的乘法性质，我们有：
$$ \chi_V(g) = \chi_{\operatorname{Ind}_H^G U}(g) \cdot \chi_{W_{std}}(g) $$
我们需要分别计算右侧的两个因子。
1.  对于 $\chi_{W_{std}}(g)$：标准[表示的特征标](@entry_id:198072) $\chi_{W_{std}}(g)$ 等于[置换](@entry_id:136432) $g$ 的[不动点](@entry_id:156394)数目减 1。$g=(12)(34)$ 在 $\{1,2,3,4\}$上没有[不动点](@entry_id:156394)，所以 $\chi_{W_{std}}(g) = 0 - 1 = -1$。
2.  对于 $\chi_{\operatorname{Ind}_H^G U}(g)$：我们可以使用[诱导特征标](@entry_id:143636)公式的一个变体，它按[共轭类](@entry_id:143916)进行求和：
    $$ \chi_{\operatorname{Ind}_H^G U}(g) = \frac{|C_G(g)|}{|H|} \sum_{h \in \operatorname{Cl}_G(g) \cap H} \chi_U(h) $$
    对于 $g=(12)(34)$，其[中心化子](@entry_id:146604)大小 $|C_G(g)|=8$，$|H|=8$。$g$ 所在的共轭类与 $H$ 的交集包含三个元素，经过计算可知 $\chi_U$ 在这三个元素上的值之和为 3。因此，$\chi_{\operatorname{Ind}_H^G U}(g) = \frac{8}{8} \cdot 3 = 3$。

最后，将两部分相乘得到 $\chi_V(g) = 3 \cdot (-1) = -3$。

总而言之，[诱导表示](@entry_id:136842)是表示论中一个核心的构造工具。它不仅提供了一种从子[群表示](@entry_id:156757)构建全[群表示](@entry_id:156757)的系统方法，其优美的代数性质，尤其是 Frobenius [互反律](@entry_id:188215)，更为我们深入理解[群表示](@entry_id:156757)的结构和分解提供了无与伦比的视角和计算能力。