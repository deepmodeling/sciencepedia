## 引言
在代数拓扑的研究中，[奇异同调](@entry_id:158380)通常以整数环 $\mathbb{Z}$ 作为其默认的系数群。虽然整数同调是理解拓扑空间[不变量](@entry_id:148850)的基石，但它并非总是最有效或最具洞察力的工具。某些拓扑特征，特别是与挠扑（torsion）相关的[精细结构](@entry_id:140861)，可能在整数系数下难以计算或被掩盖。为了克服这些局限性并解锁更深层次的拓扑信息，代数拓扑学引入了使用任意[阿贝尔群](@entry_id:150284) $G$ 作为系数的同调论。

本文旨在系统地介绍带任意系数的同调群这一核心概念。我们将从其基本原理出发，探索这一理论推广如何成为解决复杂拓扑问题的强大分析工具。读者将通过本文学习到：

- 在第一章“原理与机制”中，我们将学习如何通过张量积定义带任意系数的同调群，并深入探讨连接不同系数群的核心工具——泛系数定理（Universal Coefficient Theorem）。
- 在第二章“应用与跨学科联系”中，我们将展示如何选择合适的系数群（如域系数 $\mathbb{Q}$ 或 $\mathbb{Z}_p$）来简化计算、探测空间的挠扑结构，并揭示其在几何与群论中的应用。
- 在第三章“动手实践”中，您将通过具体的计算问题，巩固理论知识，并亲身体验改变系数带来的深刻影响。

通过这三个章节的层层深入，我们将揭示为何改变系数不仅是一种技术上的推广，更是一种能够让我们以不同视角审视[拓扑空间](@entry_id:155056)，从而获得更丰富理解的强大思想。

## 原理与机制

在上一章中，我们介绍了[奇异同调](@entry_id:158380)的概念，其系数群默认为[整数环](@entry_id:181003) $\mathbb{Z}$。虽然整数同调功能强大，但代数拓扑学的一个深刻见解是，通过改变系数群，我们可以探测到[拓扑空间](@entry_id:155056)的不同方面。将系数群从 $\mathbb{Z}$ 推广到任意[阿贝尔群](@entry_id:150284) $G$，不仅可以简化计算，有时还能揭示整数同调无法捕捉的[精细结构](@entry_id:140861)。本章将深入探讨带任意系数的同调论的原理与机制，重点介绍其定义、计算方法以及连接不同系数群的核心工具——泛系数定理。

### 带任意系数的同调群的定义与计算

从代数角度看，[奇异同调](@entry_id:158380)建立在奇异[链复形](@entry_id:150246)之上。对于一个拓扑空间 $X$，其 $n$ 维奇异链群 $C_n(X; \mathbb{Z})$ 是由所有奇异 $n$-单纯形（即从标准 $n$-单纯形 $\Delta^n$ 到 $X$ 的[连续映射](@entry_id:153855)）生成的自由[阿贝尔群](@entry_id:150284)。这些链群与[边界映射](@entry_id:151165) $\partial_n$ 共同构成了一个[链复形](@entry_id:150246) $(C_*(X; \mathbb{Z}), \partial)$。

将系数推广到任意[阿贝尔群](@entry_id:150284) $G$ 的想法在代数上非常自然。我们通过张量积来“更换”系数。具体而言，**带系数 $G$ 的奇异[链复形](@entry_id:150246)** $(C_*(X; G), d)$ 定义为整数[链复形](@entry_id:150246)与群 $G$ 在 $\mathbb{Z}$ 上的张量积：
$$
C_n(X; G) := C_n(X; \mathbb{Z}) \otimes_{\mathbb{Z}} G
$$
其[边界映射](@entry_id:151165) $d_n: C_n(X; G) \to C_{n-1}(X; G)$ 由 $d_n := \partial_n \otimes \text{id}_G$ 给出。由于 $\partial_{n-1} \circ \partial_n = 0$，我们有 $d_{n-1} \circ d_n = (\partial_{n-1} \otimes \text{id}_G) \circ (\partial_n \otimes \text{id}_G) = (\partial_{n-1} \circ \partial_n) \otimes \text{id}_G = 0 \otimes \text{id}_G = 0$，因此 $(C_*(X; G), d)$ 确实是一个[链复形](@entry_id:150246)。

于是，空间 $X$ 的**第 $n$ 阶带系数 $G$ 的[奇异同调](@entry_id:158380)群** $H_n(X; G)$ 被定义为这个新[链复形](@entry_id:150246)的同调群：
$$
H_n(X; G) := \frac{\ker(d_n)}{\text{Im}(d_{n+1})}
$$
这个定义同样适用于[胞腔同调](@entry_id:264549)等其他同调论。

为了理解这个定义的直接后果，让我们从最简单的空间开始。考虑一个单点空间 $X = \{\text{pt}\}$。对于每个维度 $n \geq 0$，存在唯一的奇异 $n$-单纯形，即映到该点的常数映射。因此，整数链群 $C_n(\text{pt}; \mathbb{Z})$ 是由这个唯一的单纯形生成的秩为1的自由[阿贝尔群](@entry_id:150284)，即 $C_n(\text{pt}; \mathbb{Z}) \cong \mathbb{Z}$。[边界映射](@entry_id:151165) $\partial_n$ 将 $n$-单纯形的生成元映为它的交错面之和。由于所有面都是同一个 $(n-1)$-单纯形，当 $n>0$ 时，$\partial_n$ 的作用是乘以 $\sum_{i=0}^n (-1)^i$。这个和在 $n$ 为偶数时为 1，在 $n$ 为奇数时为 0。因此，整数[链复形](@entry_id:150246)是：
$$
\dots \xrightarrow{\times 1} \mathbb{Z} \xrightarrow{\times 0} \mathbb{Z} \xrightarrow{\times 1} \mathbb{Z} \xrightarrow{\times 0} \mathbb{Z} \to 0
$$
现在，我们将此[链复形](@entry_id:150246)与任意[阿贝尔群](@entry_id:150284) $G$ 作张量积。由于 $\mathbb{Z} \otimes_{\mathbb{Z}} G \cong G$，并且 $(\times k) \otimes \text{id}_G$ 对应于映射 $g \mapsto kg$，我们得到[链复形](@entry_id:150246) $C_*(\text{pt}; G)$ [@problem_id:1655547]：
$$
\dots \xrightarrow{\text{id}_G} G \xrightarrow{0} G \xrightarrow{\text{id}_G} G \xrightarrow{0} G \to 0
$$
其中，从右到左，第一个非零群是 $C_0(\text{pt}; G)$。我们来计算其同调群：
- $H_0(\text{pt}; G) = \ker(d_0) / \text{Im}(d_1) = \ker(0) / \text{Im}(0) = G / \{0\} \cong G$。
- 对于 $n>0$ 且为奇数，$H_n(\text{pt}; G) = \ker(d_n) / \text{Im}(d_{n+1}) = \ker(0) / \text{Im}(\text{id}_G) = G / G \cong \{0\}$。
- 对于 $n>0$ 且为偶数，$H_n(\text{pt}; G) = \ker(d_n) / \text{Im}(d_{n+1}) = \ker(\text{id}_G) / \text{Im}(0) = \{0\} / \{0\} \cong \{0\}$。
综上所述，单点空间的同调群为 $H_0(\text{pt}; G) \cong G$，且对于所有 $n>0$， $H_n(\text{pt}; G) \cong \{0\}$。这与我们对 $H_0$ 作为[路径连通分支](@entry_id:275432)的衡量这一直觉是相符的。

让我们再看一个例子，圆周 $S^1$。使用胞腔分解，它有一个0-胞腔和一个1-胞腔。其[胞腔链复形](@entry_id:160435)为：
$$
\dots \to 0 \to C_1(S^1; \mathbb{Z}) \xrightarrow{\partial_1} C_0(S^1; \mathbb{Z}) \to 0 \to \dots
$$
即 $\dots \to 0 \to \mathbb{Z} \xrightarrow{\partial_1} \mathbb{Z} \to 0 \to \dots$。由于1-胞腔的边界映到同一点上，其度为 $1-1=0$，所以[边界映射](@entry_id:151165) $\partial_1=0$。现在考虑系数群 $G = \mathbb{Z}_4$ [@problem_id:1655543]。我们对上述[链复形](@entry_id:150246)张量 $\mathbb{Z}_4$：
$$
\dots \to 0 \to \mathbb{Z} \otimes \mathbb{Z}_4 \xrightarrow{0 \otimes \text{id}} \mathbb{Z} \otimes \mathbb{Z}_4 \to 0 \to \dots
$$
这变成了 $\dots \to 0 \to \mathbb{Z}_4 \xrightarrow{0} \mathbb{Z}_4 \to 0 \to \dots$。由于所有[边界映射](@entry_id:151165)都是零，同调群就是链群本身。因此，我们得到 $H_1(S^1; \mathbb{Z}_4) \cong \mathbb{Z}_4$，$H_0(S^1; \mathbb{Z}_4) \cong \mathbb{Z}_4$，而其他阶的同调群为零。这与整数同调 $H_1(S^1; \mathbb{Z}) \cong \mathbb{Z}$ 和 $H_0(S^1; \mathbb{Z}) \cong \mathbb{Z}$ 形成了有趣的对比。

### 泛系数定理

尽管直接计算在某些情况下可行，但它往往很繁琐，并且不能清晰地揭示 $H_n(X; G)$ 与我们已经熟知的 $H_n(X; \mathbb{Z})$ 之间的系统性关系。幸运的是，代数上存在一个深刻的定理，它精确地描述了这种关系，这就是**泛系数定理 (Universal Coefficient Theorem, UCT)**。

泛系数定理指出，对于任何拓扑空间 $X$ 和任意阿贝尔群 $G$，对每个维度 $n \ge 0$，都存在一个自然的短[正合序列](@entry_id:151503)：
$$
0 \to \left(H_n(X; \mathbb{Z}) \otimes G\right) \to H_n(X; G) \to \text{Tor}_1^{\mathbb{Z}}\left(H_{n-1}(X; \mathbb{Z}), G\right) \to 0
$$
[@problem_id:1648713]。这里，$\text{Tor}_1^{\mathbb{Z}}(A, B)$ 是阿贝尔群 $A$ 和 $B$ 的**挠积 (Torsion Product)** 函子。它衡量了张量积函子 $-\otimes B$ 在应用于短[正合序列](@entry_id:151503)时偏离正合性的程度。例如，对于循环群，我们有 $\text{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_m, G) \cong \ker(G \xrightarrow{\times m} G)$。

更重要的是，这个短[正合序列](@entry_id:151503)是**分裂的 (split)**。这意味着中间的[群同构](@entry_id:147371)于两端群的[直和](@entry_id:156782)：
$$
H_n(X; G) \cong \left(H_n(X; \mathbb{Z}) \otimes G\right) \oplus \text{Tor}_1^{\mathbb{Z}}\left(H_{n-1}(X; \mathbb{Z}), G\right)
$$
这个分裂虽然存在，但通常不是自然的，这意味着映射 $H_n(X; G) \to H_n(Y; G)$ 一般不保持这种[直和分解](@entry_id:263004)。尽管如此，这个同构关系本身就是一个极其强大的计算工具。它告诉我们，带系数 $G$ 的同调群完全由整数同调[群代数](@entry_id:145139)地确定。具体来说，$H_n(X; G)$ 由两部分贡献：
1.  来自第 $n$ 阶整数同调 $H_n(X; \mathbb{Z})$ 的贡献，通过张量积体现。
2.  来自第 $n-1$ 阶整数同调 $H_{n-1}(X; \mathbb{Z})$ 的挠曲部分的贡献，通过[Tor函子](@entry_id:151730)体现。

### 泛系数定理的应用与推论

泛系数定理不仅是一个计算公式，更是一个深刻的结构性定理，它揭示了不同系数下同调论的内在联系。

#### 特殊系数群：域

当系数群 $G$ 是一个域（例如有理[数域](@entry_id:155558) $\mathbb{Q}$ 或[有限域](@entry_id:142106) $\mathbb{Z}_p$）时，情况会大大简化。

一个重要的代数事实是，如果一个阿贝尔群 $A$ 是[无挠的](@entry_id:161664)（torsion-free），那么 $\text{Tor}_1^{\mathbb{Z}}(A, G) = \{0\}$ 对任何 $G$ 成立。因此，如果一个空间 $X$ 的所有整数同调群 $H_n(X; \mathbb{Z})$ 都是[无挠的](@entry_id:161664)，则UCT中的Tor项总是为零 [@problem_id:1655531]。在这种情况下，我们有：
$$
H_n(X; G) \cong H_n(X; \mathbb{Z}) \otimes G
$$
一个更普遍的简化发生在系数群 $G$ 是一个**平坦的 $\mathbb{Z}$-模**时。这意味着函子 $-\otimes G$ 是正合的，从而 $\text{Tor}_1^{\mathbb{Z}}(A, G) = \{0\}$ 对所有 $A$ 成立。有理[数域](@entry_id:155558) $\mathbb{Q}$ 就是一个平坦的 $\mathbb{Z}$-模。因此，对于任何空间 $X$，我们总是有 $\text{Tor}_1^{\mathbb{Z}}(H_{n-1}(X; \mathbb{Z}), \mathbb{Q}) = \{0\}$。UCT因此简化为：
$$
H_n(X; \mathbb{Q}) \cong H_n(X; \mathbb{Z}) \otimes \mathbb{Q}
$$
[@problem_id:1655541]。如果 $H_n(X; \mathbb{Z}) \cong \mathbb{Z}^{\beta_n} \oplus T_n$，其中 $\beta_n$ 是[贝蒂数](@entry_id:153109)（Betti number），$T_n$ 是[挠子群](@entry_id:139454)，那么由于[挠子群](@entry_id:139454)与 $\mathbb{Q}$ 的张量积为零（$T_n \otimes \mathbb{Q} = 0$），我们得到：
$$
H_n(X; \mathbb{Q}) \cong (\mathbb{Z}^{\beta_n} \otimes \mathbb{Q}) \oplus (T_n \otimes \mathbb{Q}) \cong \mathbb{Q}^{\beta_n}
$$
这意味着 $H_n(X; \mathbb{Q})$ 是一个维度为 $\beta_n$ 的 $\mathbb{Q}$-[向量空间](@entry_id:151108)。换言之，**有理系数同调只探测空间的贝蒂数，而完全忽略了挠曲信息**。例如，如果一个空间的整数同调群为 $H_1(Y; \mathbb{Z}) \cong \mathbb{Z}^{4} \oplus \mathbb{Z}_{2} \oplus \mathbb{Z}_{6}$ 和 $H_2(Y; \mathbb{Z}) \cong \mathbb{Z}^{3} \oplus \mathbb{Z}_{3}$ [@problem_id:1655541]，其[有理同调](@entry_id:263114)群的维度将分别为 $d_1 = \dim_{\mathbb{Q}} H_1(Y; \mathbb{Q}) = 4$ 和 $d_2 = \dim_{\mathbb{Q}} H_2(Y; \mathbb{Q}) = 3$。

与此相反，当系数群是有限域 $\mathbb{Z}_p$ 时，Tor项通常非零。事实上，$\text{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_m, \mathbb{Z}_p)$ 在 $p$ 整除 $m$ 时非零（此时它同构于 $\mathbb{Z}_p$）。这意味着 $\mathbb{Z}_p$ 系数同调不仅能探测[贝蒂数](@entry_id:153109)，还能探测整数同调中的 $p$-挠曲（即阶为 $p$ 的幂次的挠曲元素）。

利用UCT，我们可以推导出 $H_k(X; \mathbb{Z}_p)$ 作为 $\mathbb{Z}_p$-[向量空间](@entry_id:151108)的维数公式 [@problem_id:1655562]。设 $H_n(X; \mathbb{Z}) \cong \mathbb{Z}^{\beta_n} \oplus T_n$，其中 $T_n$ 是[挠子群](@entry_id:139454)。$T_n$ 可以分解为其 $q$-素元部分 $T_n(q)$ 的[直和](@entry_id:156782)。令 $c_n(p)$ 为 $T_n$ 的 $p$-素元部分分解成的[循环群](@entry_id:138668)的个数。
- $H_k(X; \mathbb{Z}) \otimes \mathbb{Z}_p$ 的维数是 $\beta_k + c_k(p)$。
- $\text{Tor}_1^{\mathbb{Z}}(H_{k-1}(X; \mathbb{Z}), \mathbb{Z}_p)$ 的维数是 $c_{k-1}(p)$。
因此，总维度为：
$$
\dim_{\mathbb{Z}_p} H_k(X; \mathbb{Z}_p) = \beta_k + c_k(p) + c_{k-1}(p)
$$
例如，若 $H_1(X; \mathbb{Z}) \cong \mathbb{Z}^2 \oplus \mathbb{Z}_6 \oplus \mathbb{Z}_{15}$ 且 $H_2(X; \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}_{18} \oplus \mathbb{Z}_{20}$，我们可以计算 $H_2(X; \mathbb{Z}_3)$ 的维数。首先分解整数同调群：$\beta_2 = 1$。$H_2$ 的挠曲部分 $T_2 = \mathbb{Z}_{18} \oplus \mathbb{Z}_{20} \cong \mathbb{Z}_2 \oplus \mathbb{Z}_9 \oplus \mathbb{Z}_4 \oplus \mathbb{Z}_5$，其3-素元部分是 $\mathbb{Z}_9$，故 $c_2(3)=1$。$H_1$ 的挠曲部分 $T_1 = \mathbb{Z}_6 \oplus \mathbb{Z}_{15} \cong \mathbb{Z}_2 \oplus \mathbb{Z}_3 \oplus \mathbb{Z}_3 \oplus \mathbb{Z}_5$，其3-素元部分是 $\mathbb{Z}_3 \oplus \mathbb{Z}_3$，故 $c_1(3)=2$。代入公式得：
$$
\dim_{\mathbb{Z}_3} H_2(X; \mathbb{Z}_3) = \beta_2 + c_2(3) + c_{1}(3) = 1 + 1 + 2 = 4
$$
这个公式清晰地展示了 $\mathbb{Z}_p$ 系数同调是如何从 $k$ 阶和 $k-1$ 阶整数同调中提取信息的。

#### 不同系数揭示不同信息

一个引人注目的现象是，一个在整数同调中不可见的特征，可能会在改变系数后“显现”出来。考虑一个[CW复形](@entry_id:150589)，其整数[链复形](@entry_id:150246)在某维度 $n$ 附近形如 $\dots \to \mathbb{Z} \xrightarrow{\times p} \mathbb{Z} \to \dots$，其中 $p$ 是一个素数 [@problem_id:1655548]。例如，若 $d_2(c_2) = 7c_1$ 且 $d_1(c_1)=0$，则 $H_2(X; \mathbb{Z}) = \ker(d_2)/\text{Im}(d_3) = \ker(\times 7)/0 = 0$。这个2阶循环在整数同调中是平凡的。
然而，当我们把系数换成 $\mathbb{Z}_7$ 时，[链复形](@entry_id:150246)变为 $\dots \to \mathbb{Z}_7 \xrightarrow{\times 7} \mathbb{Z}_7 \to \dots$。由于在 $\mathbb{Z}_7$ 中乘以7是零映射，所以 $d_2 \otimes \text{id}_{\mathbb{Z}_7} = 0$。因此 $H_2(X; \mathbb{Z}_7) = \ker(0)/\text{Im}(0) \cong \mathbb{Z}_7$。这个在整数同调中消失的循环，在 $\mathbb{Z}_7$ 系数下变得可见。

我们也可以用UCT来解释这个现象。对于这个空间，可以算出 $H_1(X; \mathbb{Z}) \cong \mathbb{Z}_7$。应用UCT计算 $H_2(X; \mathbb{Z}_7)$：
$$
H_2(X; \mathbb{Z}_7) \cong (H_2(X; \mathbb{Z}) \otimes \mathbb{Z}_7) \oplus \text{Tor}_1^{\mathbb{Z}}(H_1(X; \mathbb{Z}), \mathbb{Z}_7)
$$
$$
\cong (\{0\} \otimes \mathbb{Z}_7) \oplus \text{Tor}_1^{\mathbb{Z}}(\mathbb{Z}_7, \mathbb{Z}_7) \cong \{0\} \oplus \mathbb{Z}_7 \cong \mathbb{Z}_7
$$
这个例子完美地展示了UCT中的Tor项如何捕捉到由 $(n-1)$ 阶挠曲产生的 $n$ 阶同调。

综合来看，通过使用 $\mathbb{Q}$ 和所有素[数域](@entry_id:155558) $\mathbb{Z}_p$ 作为系数，我们可以完全重构一个具有[有限生成](@entry_id:156447)同调群的空间的整数同调群。
- $H_n(X; \mathbb{Q})$ 的维数给出了 $H_n(X; \mathbb{Z})$ 的秩（即[贝蒂数](@entry_id:153109) $\beta_n$）。
- $H_*(X; \mathbb{Z}_p)$ 的维数信息，通过UCT公式，可以用来确定 $H_*(X; \mathbb{Z})$ 中 $p$-挠曲部分的结构。例如，$\dim_{\mathbb{Z}_p} \text{Tor}(H_{n-1}(X), \mathbb{Z}_p) = \dim_{\mathbb{Z}_p} H_n(X; \mathbb{Z}_p) - (\beta_n + \dim_{\mathbb{Z}_p}(T_n \otimes \mathbb{Z}_p))$，这可以帮助我们递归地确定各阶挠曲[子群](@entry_id:146164)的信息 [@problem_id:1655542]。

#### 同调群的代数确定性

UCT公式 $H_n(X; G) \cong (H_n(X; \mathbb{Z}) \otimes G) \oplus \text{Tor}(H_{n-1}(X; \mathbb{Z}), G)$ 表明，$H_n(X; G)$ 的[同构类](@entry_id:147854)完全由 $H_n(X; \mathbb{Z})$ 和 $H_{n-1}(X; \mathbb{Z})$ 的[同构类](@entry_id:147854)确定。这意味着，如果两个空间 $X$ 和 $Y$ 在所有维度上都有同构的整数同调群，即 $H_k(X; \mathbb{Z}) \cong H_k(Y; \mathbb{Z})$ 对所有 $k$ 成立，那么对于任意系数群 $G$，它们的带系数 $G$ 的同调群也必定同构，即 $H_k(X; G) \cong H_k(Y; G)$ 对所有 $k$ 成立 [@problem_id:1655527]。

这个结论初看起来可能与UCT分裂的“非自然性”相矛盾，但实际上不然。非自然性指的是，一个从 $X$到$Y$的映射 $f$ 所诱导的同调映射 $f_*: H_n(X; G) \to H_n(Y; G)$ 一般不会将 $H_n(X; G)$ 的[直和分解](@entry_id:263004)映到 $H_n(Y; G)$ 的[直和分解](@entry_id:263004)中。然而，对于单个空间而言，其同调群的[同构类](@entry_id:147854)型是确定的。因此，“具有同构的整数同调”是一个非常强的条件，它保证了在任何系数下同调群的同构。

#### 同调公理的代数推广

UCT的另一个强大之处在于，它使得许多为整数同调证明的定理能够几乎 purely algebraically 地推广到任意系数群。许多重要的同调理论性质，如长正合序列、[Mayer-Vietoris序列](@entry_id:161286)和[切除定理](@entry_id:159397)，其证明的核心是[链复形](@entry_id:150246)层面上的代数构造。一旦这些性质对整数同调成立，UCT就能作为一座桥梁，将结论延伸到任意系数。

以**[切除定理](@entry_id:159397) (Excision Theorem)** 为例。对于整数同调，该定理断言，在适当条件下，从 $(X \setminus Z, A \setminus Z)$到$(X, A)$ 的包含映射诱导了同调群的同构。为了证明它对任意系数群 $G$ 也成立，我们无需重复复杂的几何论证。取而代之，我们利用UCT的自然性 [@problem_id:1655536]。

包含映射 $i$ 诱导了UCT短[正合序列](@entry_id:151503)之间的一个[交换图](@entry_id:747516)：
$$
\begin{array}{ccccccccc}
0  \to  H_n(X \!\setminus\! Z, A \!\setminus\! Z) \!\otimes\! G  \to  H_n(X \!\setminus\! Z, A \!\setminus\! Z; G)  \to  \text{Tor}(H_{n-1}(X \!\setminus\! Z, A \!\setminus\! Z),G)  \to  0 \\
    \downarrow i_* \otimes \text{id}   \downarrow i_*   \downarrow \text{Tor}(i_*, \text{id})   \\
0  \to  H_n(X, A) \!\otimes\! G  \to  H_n(X, A;G)  \to  \text{Tor}(H_{n-1}(X, A),G)  \to  0
\end{array}
$$
我们已知整数[切除定理](@entry_id:159397)成立，即垂直映射 $i_*: H_k(X \setminus Z, A \setminus Z; \mathbb{Z}) \to H_k(X, A; \mathbb{Z})$ 对所有 $k$ 都是同构。由于 $\otimes G$ 和 $\text{Tor}(-, G)$ 都是函子，它们将同构映为同构。因此，图中最左边和最右边的垂直箭头都是同构。根据代数中的**[五引理](@entry_id:263766) (Five Lemma)**，我们立即得出结论：中间的垂直箭头 $i_*: H_n(X \setminus Z, A \setminus Z; G) \to H_n(X, A; G)$ 也必须是同构。

这个论证思路体现了泛系数定理的核心作用：它将关于同调群的几何问题（如切除）转化为一个纯粹的代数问题，从而使整个理论体系更具系统性和威力。通过改变系数群 $G$，我们实际上是在用不同的代数“探针”来审视同一个底层的拓扑结构，而UCT则精确地告诉我们这些不同探针所获得的信息之间的关系。