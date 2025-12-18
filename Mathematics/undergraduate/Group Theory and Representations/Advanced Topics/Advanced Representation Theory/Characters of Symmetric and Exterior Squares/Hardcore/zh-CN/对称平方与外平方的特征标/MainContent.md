## 引言
在[群表示论](@entry_id:141930)的研究中，从已知表示构造新表示是一项核心技术，它极大地扩展了我们理解和应用对称性的能力。在众多构造方法中，源于[张量积分解](@entry_id:138873)的**对称方 (symmetric square)** 和**[外代数](@entry_id:201164)方 (exterior square)** 尤为基本且深刻。然而，如何系统地理解这两种新表示的结构，特别是如何计算它们的特征标，是学习者面临的一个关键问题。本文旨在填补这一知识空白，为读者提供一个关于对称方与[外代数](@entry_id:201164)方[特征标理论](@entry_id:144021)的全面指南。

在接下来的内容中，读者将循序渐进地掌握这一主题。第一章 **“原理与机制”** 将从[张量积表示](@entry_id:143629)出发，详细推导对称方与[外代数](@entry_id:201164)方[特征标的核](@entry_id:146159)心公式，并阐释其背后的代数原理。第二章 **“应用与交叉学科联系”** 将展示这些公式的强大威力，探讨其在分解表示、通过Frobenius-Schur指示子判断表示类型以及与物理学、组合学等领域的联系。最后，在 **“动手实践”** 部分，读者将通过解决具体问题，将理论知识转化为实践技能。通过这三章的学习，你将能够熟练运用这些工具来分析复杂的表示结构。

## 原理与机制

在研究[群表示论](@entry_id:141930)时，一个核心任务是从已知的表示构造新的表示。这种构造不仅丰富了我们对[群对称性](@entry_id:147821)的理解，也为分析复杂的物理或数学系统提供了强大的工具。在上一章介绍的基础上，本章将深入探讨两种源于[张量积表示](@entry_id:143629)的基本构造：**对称方 (symmetric square)** 和**[外代数](@entry_id:201164)方 (exterior square)**。我们将推导它们的[特征标公式](@entry_id:142515)，并探讨其背后的原理、重要性质及应用。

### 从张量积到对称与[外代数](@entry_id:201164)方

给定一个群 $G$ 在[复向量空间](@entry_id:264355) $V$ 上的表示 $\rho: G \to GL(V)$，我们可以构造其**[张量积表示](@entry_id:143629) (tensor product representation)** $V \otimes V$。群元素 $g \in G$ 在此空间上的作用由 $\rho(g) \otimes \rho(g)$ 给出，它作用于简单张量 $v \otimes w$ 的方式是：
$$
(\rho(g) \otimes \rho(g))(v \otimes w) = \rho(g)v \otimes \rho(g)w
$$
如果表示 $V$ 的特征标是 $\chi_V$，那么[张量积表示](@entry_id:143629) $V \otimes V$ 的特征标 $\chi_{V \otimes V}$ 有一个非常简洁的性质：
$$
\chi_{V \otimes V}(g) = \mathrm{Tr}(\rho(g) \otimes \rho(g)) = (\mathrm{Tr}(\rho(g)))^2 = (\chi_V(g))^2
$$
即张量积[表示的特征标](@entry_id:198072)是原特征标的逐点平方。

[张量积](@entry_id:140694)空间 $V \otimes V$ 自身包含着更精细的结构。我们可以将其分解为两个非常重要的[子空间](@entry_id:150286)。为此，我们引入**交换算子 (flip operator)** $S: V \otimes V \to V \otimes V$，其定义为 $S(v \otimes w) = w \otimes v$。容易验证，对于任意 $g \in G$，该算子与群作用可交换，即 $S \circ (\rho(g) \otimes \rho(g)) = (\rho(g) \otimes \rho(g)) \circ S$。这意味着 $S$ 的特征[子空间](@entry_id:150286)在群作用下是保持不变的，因此它们本身就是 $G$ 的[子表示](@entry_id:141094)。

交换算子 $S$ 的平方是[恒等变换](@entry_id:264671) ($S^2 = I$)，所以它的[特征值](@entry_id:154894)只能是 $+1$ 和 $-1$。
+ 对应的[特征值](@entry_id:154894)为 $+1$ 的[子空间](@entry_id:150286)称为**对称方 (symmetric square)**，记作 $Sym^2(V)$。它由形如 $v \otimes w + w \otimes v$ 的**对称张量 (symmetric tensors)** 张成。
+ 对应的[特征值](@entry_id:154894)为 $-1$ 的[子空间](@entry_id:150286)称为**[外代数](@entry_id:201164)方 (exterior square)** 或**交错方 (alternating square)**，记作 $\Lambda^2(V)$。它由形如 $v \otimes w - w \otimes v$ 的**交错张量 (alternating tensors)** 张成。

由于这两个[子空间](@entry_id:150286)是群作用下的[不变子空间](@entry_id:152829)，并且它们的直和构成了整个张量积空间，我们得到了 $V \otimes V$ 的一个基本分解：
$$
V \otimes V \cong Sym^2(V) \oplus \Lambda^2(V)
$$
这个分解在[表示论](@entry_id:137998)和物理学中都有着深刻的应用。例如，在量子力学中，对于一个由两个[全同粒子](@entry_id:142755)组成的系统，如果粒子是[玻色子](@entry_id:138266)，其状态空间就是单粒子[希尔伯特空间](@entry_id:261193) $V$ 的对称方 $Sym^2(V)$；如果粒子是[费米子](@entry_id:146235)，其[状态空间](@entry_id:177074)则是[外代数](@entry_id:201164)方 $\Lambda^2(V)$。

### 对称方与[外代数](@entry_id:201164)方的维数

表示的维数是其最基本的属性。我们可以通过组合学的方法确定 $Sym^2(V)$ 和 $\Lambda^2(V)$ 的维数。设 $\dim(V) = n$，并取 $V$ 的一组基 $\{e_1, e_2, \dots, e_n\}$。

$Sym^2(V)$ 的一组基可以由形如 $e_i \otimes e_j + e_j \otimes e_i$ 的向量构成。为了避免重复，我们要求 $1 \le i \le j \le n$。这相当于从 $n$ 个元素中可重复地选取两个元素。这样的组[合数](@entry_id:263553)等于：
$$
\dim(Sym^2(V)) = \binom{n+2-1}{2} = \binom{n+1}{2} = \frac{n(n+1)}{2}
$$

$\Lambda^2(V)$ 的一组基可以由形如 $e_i \otimes e_j - e_j \otimes e_i$ 的向量构成。由于当 $i=j$ 时该向量为零，且交换 $i,j$ 只改变符号，我们要求 $1 \le i  j \le n$。这相当于从 $n$ 个元素中不重复地选取两个元素。这样的组[合数](@entry_id:263553)等于：
$$
\dim(\Lambda^2(V)) = \binom{n}{2} = \frac{n(n-1)}{2}
$$

注意到，这两个维数之和为 $\frac{n(n+1)}{2} + \frac{n(n-1)}{2} = \frac{n^2+n+n^2-n}{2} = n^2$，这恰好是 $\dim(V \otimes V) = (\dim V)^2 = n^2$，与我们的分解 $V \otimes V \cong Sym^2(V) \oplus \Lambda^2(V)$ 相符。

### 核心公式：对称方与[外代数](@entry_id:201164)方特征标

虽然维数的计算很直观，但要完整地理解这两个表示，我们需要计算它们在任意群元素 $g \in G$ 上的特征标。

由于特征标在[直和](@entry_id:156782)下是可加的，我们有：
$$
\chi_{V \otimes V}(g) = \chi_{Sym^2(V)}(g) + \chi_{\Lambda^2(V)}(g)
$$
结合 $\chi_{V \otimes V}(g) = (\chi_V(g))^2$，我们得到：
$$
(\chi_V(g))^2 = \chi_{Sym^2(V)}(g) + \chi_{\Lambda^2(V)}(g)
$$
这是一个重要的关系式，它表明如果我们能独立求出对称方或[外代数](@entry_id:201164)方的特征标，另一个也就随之确定。

为了求出这两个特征标，我们需要一个与 $\chi_V(g^2)$ 相关的关键恒等式。我们可以通过[投影算子](@entry_id:154142)的方法来推导。如前所述，$Sym^2(V)$ 和 $\Lambda^2(V)$ 分别是交换算子 $S$ 的 $+1$ 和 $-1$ 特征[子空间](@entry_id:150286)。到这两个[子空间](@entry_id:150286)的[投影算子](@entry_id:154142)分别是 $P_{sym} = \frac{1}{2}(I+S)$ 和 $P_{alt} = \frac{1}{2}(I-S)$。

$Sym^2(V)$ 上的特征标 $\chi_{Sym^2(V)}(g)$ 是[群作用](@entry_id:268812) $\rho(g) \otimes \rho(g)$ 在[子空间](@entry_id:150286) $Sym^2(V)$ 上的迹。利用投影算子，这个迹可以表示为在整个空间 $V \otimes V$ 上的迹：
$$
\chi_{Sym^2(V)}(g) = \mathrm{Tr}\left( P_{sym} \circ (\rho(g) \otimes \rho(g)) \right) = \frac{1}{2} \mathrm{Tr}\left( (I+S) \circ (\rho(g) \otimes \rho(g)) \right)
$$
展开后得到：
$$
\chi_{Sym^2(V)}(g) = \frac{1}{2} \left[ \mathrm{Tr}(\rho(g) \otimes \rho(g)) + \mathrm{Tr}(S \circ (\rho(g) \otimes \rho(g))) \right]
$$
第一项我们已经知道是 $\mathrm{Tr}(\rho(g) \otimes \rho(g)) = (\mathrm{Tr}(\rho(g)))^2 = (\chi_V(g))^2$。对于第二项，有一个标准的[迹恒等式](@entry_id:188149)：$\mathrm{Tr}(S \circ (A \otimes B)) = \mathrm{Tr}(AB)$。在本例中，$A=B=\rho(g)$，所以：
$$
\mathrm{Tr}(S \circ (\rho(g) \otimes \rho(g))) = \mathrm{Tr}(\rho(g)^2) = \mathrm{Tr}(\rho(g^2)) = \chi_V(g^2)
$$
将这两个结果代入，我们便得到了**对称方[特征标公式](@entry_id:142515)**：
$$
\chi_{Sym^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 + \chi_V(g^2) \right]
$$
同理，对于[外代数](@entry_id:201164)方，我们有：
$$
\chi_{\Lambda^2(V)}(g) = \mathrm{Tr}\left( P_{alt} \circ (\rho(g) \otimes \rho(g)) \right) = \frac{1}{2} \left[ \mathrm{Tr}(\rho(g) \otimes \rho(g)) - \mathrm{Tr}(S \circ (\rho(g) \otimes \rho(g))) \right]
$$
这便给出了**[外代数](@entry_id:201164)方[特征标公式](@entry_id:142515)**：
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} \left[ (\chi_V(g))^2 - \chi_V(g^2) \right]
$$
这两个公式是本章的核心，它们将一个表示的对称方和[外代数](@entry_id:201164)方的特征标，完全通过原[表示的特征标](@entry_id:198072) $\chi_V$ 在 $g$ 和 $g^2$ 上的取值来表达。

### 公式的应用与实例分析

这些公式为我们分析表示提供了强大的计算工具。

#### 维数验证
表示的维数等于其特征标在单位元 $e$ 处的取值。将 $g=e$ 代入上述公式，我们可以重新推导出维数公式。注意到 $\chi_V(e) = \dim V = n$ 且 $e^2=e$，因此 $\chi_V(e^2) = \chi_V(e) = n$。
对于对称方：
$$
\dim(Sym^2(V)) = \chi_{Sym^2(V)}(e) = \frac{1}{2} \left[ (\chi_V(e))^2 + \chi_V(e^2) \right] = \frac{1}{2} (n^2 + n) = \frac{n(n+1)}{2}
$$
对于[外代数](@entry_id:201164)方：
$$
\dim(\Lambda^2(V)) = \chi_{\Lambda^2(V)}(e) = \frac{1}{2} \left[ (\chi_V(e))^2 - \chi_V(e^2) \right] = \frac{1}{2} (n^2 - n) = \frac{n(n-1)}{2}
$$
结果与我们通过组合方法得到的维数完全一致，展示了[特征标理论](@entry_id:144021)的内在一致性。

#### 特殊情况：一维与二维表示
- **[一维表示](@entry_id:136509)**：如果 $V$ 是一个[一维表示](@entry_id:136509)，其特征标为 $\psi: G \to \mathbb{C}^*$。此时 $n=1$，$\dim(\Lambda^2(V))=0$，说明[外代数](@entry_id:201164)方是零表示。对于对称方，$\dim(Sym^2(V))=1$。其特征标为：
$$
\chi_{Sym^2(\psi)}(g) = \frac{1}{2} [ (\psi(g))^2 + \psi(g^2) ]
$$
由于 $\psi$ 是一个[群同态](@entry_id:140603)（[一维表示](@entry_id:136509)的矩阵就是数），我们有 $\psi(g^2) = (\psi(g))^2$。因此：
$$
\chi_{Sym^2(\psi)}(g) = \frac{1}{2} [ (\psi(g))^2 + (\psi(g))^2 ] = (\psi(g))^2
$$
这意味着[一维表示](@entry_id:136509) $\psi$ 的对称方就是其平方表示 $\psi^2$。

- **二维表示**：如果 $\dim V = 2$，那么 $\dim(\Lambda^2(V)) = \frac{2(1)}{2} = 1$。这意味着[外代数](@entry_id:201164)方是一个[一维表示](@entry_id:136509)。其特征标 $\chi_{\Lambda^2(V)}(g)$ 是一个标量。这个标量有一个特别的意义：它等于表示[矩阵的行列式](@entry_id:148198) $\det(\rho_V(g))$。我们可以通过[特征值](@entry_id:154894)来验证。设 $\rho_V(g)$ 的两个[特征值](@entry_id:154894)为 $\lambda_1, \lambda_2$。那么：
$$
\chi_V(g) = \lambda_1 + \lambda_2
$$
$$
\chi_V(g^2) = \lambda_1^2 + \lambda_2^2
$$
根据[外代数](@entry_id:201164)方的[特征标公式](@entry_id:142515)：
$$
\chi_{\Lambda^2(V)}(g) = \frac{1}{2} [ (\lambda_1 + \lambda_2)^2 - (\lambda_1^2 + \lambda_2^2) ] = \frac{1}{2} [ (\lambda_1^2 + 2\lambda_1\lambda_2 + \lambda_2^2) - (\lambda_1^2 + \lambda_2^2) ] = \lambda_1\lambda_2
$$
而 $\lambda_1\lambda_2$ 正是 $\rho_V(g)$ 的[行列式](@entry_id:142978)。因此，对于任意二维表示 $V$，我们有 $\chi_{\Lambda^2(V)} = \det(\rho_V)$。

#### 实例：$S_3$ 的[表示分解](@entry_id:139061)
让我们通过一个具体的例子来演示如何运用这些公式来分解表示。考虑对称群 $S_3$，它有三个[共轭类](@entry_id:143916)：单位元 $C_{id}=\{e\}$，换位 $C_{trans}=\{(12),(13),(23)\}$，以及三轮换 $C_{3-cycle}=\{(123),(132)\}$。$S_3$ 有一个二维不可约表示 $V$（标准表示），其特征标在三个类上的值分别为 $\chi_V(e)=2$, $\chi_V((12))=0$, $\chi_V((123))=-1$。

我们的目标是计算 $Sym^2(V)$ 和 $\Lambda^2(V)$ 的特征标，并将它们分解为 $S_3$ 的不可约表示的直和。$S_3$ 的不可约特征标表如下：

|            | $e$  | $(12)$ | $(123)$ |
|------------|------|--------|---------|
| $\chi_1$ (平凡) | 1    | 1      | 1       |
| $\chi_2$ (符号) | 1    | -1     | 1       |
| $\chi_3$ (标准) | 2    | 0      | -1      |

首先，我们需要计算 $\chi_V(g^2)$ 的值：
- 若 $g \in C_{id}$ ($g=e$)，则 $g^2=e$。$\chi_V(g^2) = \chi_V(e) = 2$。
- 若 $g \in C_{trans}$ (如 $g=(12)$)，则 $g^2=e$。$\chi_V(g^2) = \chi_V(e) = 2$。
- 若 $g \in C_{3-cycle}$ (如 $g=(123)$)，则 $g^2=(132)$，仍在 $C_{3-cycle}$ [共轭类](@entry_id:143916)中。$\chi_V(g^2) = \chi_V((132)) = -1$。

现在我们可以计算 $Sym^2(V)$ 的特征标：
- $\chi_{Sym^2(V)}(e) = \frac{1}{2}[(\chi_V(e))^2 + \chi_V(e^2)] = \frac{1}{2}[2^2 + 2] = 3$。
- $\chi_{Sym^2(V)}((12)) = \frac{1}{2}[(\chi_V((12)))^2 + \chi_V((12)^2)] = \frac{1}{2}[0^2 + 2] = 1$。
- $\chi_{Sym^2(V)}((123)) = \frac{1}{2}[(\chi_V((123)))^2 + \chi_V((123)^2)] = \frac{1}{2}[(-1)^2 + (-1)] = 0$。

所以 $\chi_{Sym^2(V)}$ 在三个类上的值是 $(3, 1, 0)$。为了分解它，我们计算它与每个不可约[特征标的内积](@entry_id:137615) $\langle \chi, \psi \rangle = \frac{1}{|G|} \sum_{g \in G} \chi(g)\overline{\psi(g)}$：
- $\langle \chi_{Sym^2(V)}, \chi_1 \rangle = \frac{1}{6}[1 \cdot 3 \cdot 1 + 3 \cdot 1 \cdot 1 + 2 \cdot 0 \cdot 1] = \frac{6}{6} = 1$。
- $\langle \chi_{Sym^2(V)}, \chi_2 \rangle = \frac{1}{6}[1 \cdot 3 \cdot 1 + 3 \cdot 1 \cdot (-1) + 2 \cdot 0 \cdot 1] = \frac{0}{6} = 0$。
- $\langle \chi_{Sym^2(V)}, \chi_3 \rangle = \frac{1}{6}[1 \cdot 3 \cdot 2 + 3 \cdot 1 \cdot 0 + 2 \cdot 0 \cdot (-1)] = \frac{6}{6} = 1$。

因此，我们得到分解：$Sym^2(V) \cong V_1 \oplus V_3$。

类似地，我们计算 $\Lambda^2(V)$ 的特征标：
- $\chi_{\Lambda^2(V)}(e) = \frac{1}{2}[2^2 - 2] = 1$。
- $\chi_{\Lambda^2(V)}((12)) = \frac{1}{2}[0^2 - 2] = -1$。
- $\chi_{\Lambda^2(V)}((123)) = \frac{1}{2}[(-1)^2 - (-1)] = 1$。

$\chi_{\Lambda^2(V)}$ 在三个类上的值是 $(1, -1, 1)$。通过查阅特征标表，我们立刻发现这正是符号[表示的特征标](@entry_id:198072) $\chi_2$。因此，$ \Lambda^2(V) \cong V_2$。这也符合我们之前的结论，即二维表示的[外代数](@entry_id:201164)方是其[行列式](@entry_id:142978)表示，对于 $S_3$ 的标准表示，其[行列式](@entry_id:142978)正是符号表示。

### 深入探讨与性质

#### 同构条件
我们可能会问，在什么条件下 $Sym^2(V)$ 和 $\Lambda^2(V)$ 会是同构的表示？两个[复表示](@entry_id:144331)同构当且仅当它们的特征标完全相同。因此，我们需要：
$$
\chi_{Sym^2(V)}(g) = \chi_{\Lambda^2(V)}(g) \quad \text{for all } g \in G
$$
代入我们的公式：
$$
\frac{1}{2} \left[ (\chi_V(g))^2 + \chi_V(g^2) \right] = \frac{1}{2} \left[ (\chi_V(g))^2 - \chi_V(g^2) \right]
$$
这个等式简化为 $2\chi_V(g^2) = 0$，即 $\chi_V(g^2) = 0$ 对所有 $g \in G$ 成立。
这是一个非常强的条件。特别地，当 $g=e$ 时，$g^2=e$，该条件要求 $\chi_V(e) = 0$。由于 $\chi_V(e) = \dim V$，这意味着表示 $V$ 的维数必须为零。因此，$Sym^2(V)$ 和 $\Lambda^2(V)$ 同构的唯一情况是当 $V$ 是零维表示时，此时两者也都是零维表示。

#### 实特征标
如果一个表示 $V$ 的特征标 $\chi_V$ 是实值的（即对所有 $g \in G$，$\chi_V(g) \in \mathbb{R}$），那么其对称方和[外代数](@entry_id:201164)方的特征标也必然是实值的。这是因为 $(\chi_V(g))^2$ 是实数，而 $\chi_V(g^2)$ 根据假设也是实数，所以它们的线性和 $\chi_{Sym^2(V)}(g)$ 与 $\chi_{\Lambda^2(V)}(g)$ 也都是实数。

#### 阿贝尔群的分解
对于[阿贝尔群](@entry_id:150284)，所有不可约[复表示](@entry_id:144331)都是一维的。任何表示 $V$ 都可以分解为一维[表示的[直](@entry_id:138310)和](@entry_id:156782)。这一结构可以用来分析其对称方和[外代数](@entry_id:201164)方。例如，如果 $V \cong \bigoplus_{i=1}^k L_i$，其中 $L_i$ 是[一维表示](@entry_id:136509)，那么利用[外代数](@entry_id:201164)积的性质 $\Lambda^2(A \oplus B) \cong \Lambda^2(A) \oplus \Lambda^2(B) \oplus (A \otimes B)$，我们可以得到：
$$
\Lambda^2(V) \cong \bigoplus_{1 \le i  j \le k} (L_i \otimes L_j)
$$
(这里我们假设 $L_i$ 各不相同。若有重复，例如 $V \cong U \oplus U$，则根据[外代数](@entry_id:201164)积与直和的性质，分解变为 $\Lambda^2(V) \cong \Lambda^2(U) \oplus \Lambda^2(U) \oplus (U \otimes U)$)。
如果 $L_i$ 对应的特征标是 $\psi_i$，那么 $L_i \otimes L_j$ 对应的特征标就是 $\psi_i \psi_j$。因此，$\Lambda^2(V)$ 的特征标就是 $\sum_{1 \le i  j \le k} \psi_i \psi_j$。这种方法为计算[阿贝尔群表示](@entry_id:140513)的对称方和[外代数](@entry_id:201164)方提供了一个组合式的视角。

总而言之，对称方和[外代数](@entry_id:201164)方是表示论中自然而基本的构造。它们的[特征标公式](@entry_id:142515)不仅形式优美，而且是连接[表示论](@entry_id:137998)中不同概念（如[张量积](@entry_id:140694)、[行列式](@entry_id:142978)、[表示分解](@entry_id:139061)）的桥梁，为我们理解和应用[群对称性](@entry_id:147821)提供了不可或缺的数学语言和工具。