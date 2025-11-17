## 引言
在代数拓扑的研究中，[链复形](@entry_id:150246)与[链映射](@entry_id:268209)为我们提供了将拓扑空间转化为代数对象的强大语言。然而，一个核心问题依然存在：[拓扑空间](@entry_id:155056)中至关重要的“连续变形”概念，即同伦，在代数层面上有何对应？如果两个连续映射是同伦的，它们所诱导的同调映射之间存在怎样的关系？本文旨在深入探讨**链同伦**——这一为解答上述问题而生的核心代数工具。通过学习本文，读者将全面掌握链同伦的理论与实践。在“原理和机制”一章中，我们将建立链同伦的严格定义，证明其在同调上的[不变性](@entry_id:140168)，并介绍[链同伦等价](@entry_id:270936)等关键概念。接着，在“应用与跨学科联系”一章，我们将探索链同伦如何成为连接几何直观与代数计算的桥梁，并展示其在[微分几何](@entry_id:145818)与[莫尔斯理论](@entry_id:151962)等领域的深刻影响。最后，“动手实践”部分将提供一系列练习，帮助读者将理论知识应用于具体问题的求解中。现在，让我们从链[同伦](@entry_id:139266)的基本原理和机制开始，揭示其[代数结构](@entry_id:137052)的奥秘。

## 原理和机制

在前一章中，我们引入了[链复形](@entry_id:150246)作为研究[拓扑空间](@entry_id:155056)[代数结构](@entry_id:137052)的核心工具。我们看到，一个连续映射 $f: X \to Y$ 如何诱导了链群之间的同态，即[链映射](@entry_id:268209) $f_\#: C_*(X) \to C_*(Y)$，并进一步在同调群上诱导了同态 $f_*: H_*(X) \to H_*(Y)$。一个自然而深刻的问题随之而来：拓扑空间之间的[同伦](@entry_id:139266)关系在代数层面上有何对应？如果两个映射 $f, g: X \to Y$ 是[同伦](@entry_id:139266)的，它们诱导的同调同态 $f_*$ 和 $g_*$ 之间有什么联系？本章将引入**链[同伦](@entry_id:139266) (chain homotopy)** 的概念，它为这个问题提供了完美的代数解答，并成为同调论中一个极其强大的工具。

### 链同伦的定义

我们寻求一种代数等价关系，它能捕捉拓扑[同伦](@entry_id:139266)的本质。直观上，如果两个[链映射](@entry_id:268209) $f$ 和 $g$ 是“代数上[同伦](@entry_id:139266)的”，我们期望它们在同调层面上是不可区分的。这启发我们去寻找一种方式来“填补”这两个[链映射](@entry_id:268209)之间的差异。

**定义 (链同伦)**：令 $(C_*, \partial^C)$ 和 $(D_*, \partial^D)$ 为两个[链复形](@entry_id:150246)，并令 $f, g: C_* \to D_*$ 为两个[链映射](@entry_id:268209)。我们称 $f$ 和 $g$ 是**链同伦的 (chain homotopic)**，记作 $f \simeq g$，如果存在一个**度数为 $+1$** 的同态族 $H = \{H_n: C_n \to D_{n+1}\}$，称为**链[同伦](@entry_id:139266)**，使得对于所有的整数 $n$，以下代数关系式成立：
$$
f_n - g_n = \partial^D_{n+1} \circ H_n + H_{n-1} \circ \partial^C_n
$$
为简洁起见，我们通常省略下标和复合符号，将此关系式写作 $f - g = \partial H + H \partial$。

这个定义的核心在于 $H$ 的作用。它是一个“升维”的映射，将 $C_*$ 中的 $n$-链映为 $D_*$ 中的 $(n+1)$-链。该公式表明，$f$ 和 $g$ 之间的差可以分解为两部分：一部分来自高一维链的边界 (项 $\partial H$)，另一部分与低一维链的边界有关 (项 $H \partial$)。

为了更好地理解这个抽象的定义，让我们通过一个具体的例子来剖析它的工作方式。

**示例：链[同伦](@entry_id:139266)的计算**
考虑两个由自由[阿贝尔群](@entry_id:150284)构成的[链复形](@entry_id:150246) $C_*$ 和 $D_*$。
[链复形](@entry_id:150246) $C_*$ 由 $C_2 = \mathbb{Z}, C_1 = \mathbb{Z}^2, C_0 = \mathbb{Z}$ 给出，其[边界映射](@entry_id:151165)在标准基下由[矩阵表示](@entry_id:146025)为：
$$
\partial^C_2 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}, \quad \partial^C_1 = \begin{pmatrix} 1  -1 \end{pmatrix}
$$
[链复形](@entry_id:150246) $D_*$ 由 $D_2 = \mathbb{Z}, D_1 = \mathbb{Z}^2, D_0 = \mathbb{Z}$ 给出，其[边界映射](@entry_id:151165)为：
$$
\partial^D_2 = \begin{pmatrix} 1 \\ -2 \end{pmatrix}, \quad \partial^D_1 = \begin{pmatrix} 2  1 \end{pmatrix}
$$
现有两个[链映射](@entry_id:268209) $f_*, g_*: C_* \to D_*$。假设我们已知 $f_*$ 和 $g_*$ 是链[同伦](@entry_id:139266)的，且其间的链同伦 $H$ 在非零维上由 $H_0: C_0 \to D_1$ 和 $H_1: C_1 \to D_2$ 组成。这些映射由矩阵给出：
$$
f_2 = \begin{pmatrix} 1 \end{pmatrix}, \quad f_1 = \begin{pmatrix} 1  0 \\ -1  -1 \end{pmatrix}, \quad f_0 = \begin{pmatrix} 1 \end{pmatrix}
$$
$$
g_2 = \begin{pmatrix} 3 \end{pmatrix}, \quad g_1 = \begin{pmatrix} 2  1 \\ -2  -4 \end{pmatrix}, \quad g_0 = \begin{pmatrix} 2 \end{pmatrix}
$$
$$
H_0 = \begin{pmatrix} 1 \\ -1 \end{pmatrix}, \quad H_1 = \begin{pmatrix} 0  h \end{pmatrix}
$$
其中 $h$ 是一个待定的整数。我们的任务是确定 $h$ 的值 [@problem_id:1638428]。

我们可以逐个维度地应用链同伦的定义式 $g_n - f_n = \partial^D_{n+1} H_n + H_{n-1} \partial^C_n$。

*   **在维度 $n=2$**：该维度的方程为 $g_2 - f_2 = \partial^D_3 H_2 + H_1 \partial^C_2$。由于 $D_3 = 0$，我们有 $\partial^D_3 = 0$，所以方程简化为 $g_2 - f_2 = H_1 \partial^C_2$。代入矩阵，我们得到：
    $$
    \begin{pmatrix} 3 \end{pmatrix} - \begin{pmatrix} 1 \end{pmatrix} = \begin{pmatrix} 0  h \end{pmatrix} \begin{pmatrix} 1 \\ 1 \end{pmatrix}
    $$
    $$
    \begin{pmatrix} 2 \end{pmatrix} = \begin{pmatrix} h \end{pmatrix}
    $$
    这直接给出 $h=2$。

*   **在维度 $n=1$**：该维度的方程为 $g_1 - f_1 = \partial^D_2 H_1 + H_0 \partial^C_1$。我们分别计算每一项：
    $$
    g_1 - f_1 = \begin{pmatrix} 2  1 \\ -2  -4 \end{pmatrix} - \begin{pmatrix} 1  0 \\ -1  -1 \end{pmatrix} = \begin{pmatrix} 1  1 \\ -1  -3 \end{pmatrix}
    $$
    $$
    \partial^D_2 H_1 = \begin{pmatrix} 1 \\ -2 \end{pmatrix} \begin{pmatrix} 0  h \end{pmatrix} = \begin{pmatrix} 0  h \\ 0  -2h \end{pmatrix}
    $$
    $$
    H_0 \partial^C_1 = \begin{pmatrix} 1 \\ -1 \end{pmatrix} \begin{pmatrix} 1  -1 \end{pmatrix} = \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix}
    $$
    将它们相加得到：
    $$
    \partial^D_2 H_1 + H_0 \partial^C_1 = \begin{pmatrix} 0  h \\ 0  -2h \end{pmatrix} + \begin{pmatrix} 1  -1 \\ -1  1 \end{pmatrix} = \begin{pmatrix} 1  h-1 \\ -1  1-2h \end{pmatrix}
    $$
    将此结果与 $g_1 - f_1$ 的矩阵相等，我们得到两个方程：$h-1=1$ 和 $1-2h=-3$。这两个方程都给出了唯一解 $h=2$，这与我们在维度 $n=2$ 得到的结论一致。

这个例子清晰地表明，链[同伦](@entry_id:139266)的定义是一个在所有维度上都必须同时满足的严格的代数约束。

### 基本性质：同调不变性

链[同伦](@entry_id:139266)的定义之所以如此重要，是因为它引出了同调论中的一个基石性定理。这个定理正是我们将拓扑[同伦](@entry_id:139266)与同调联系起来的桥梁。

**定理：** 如果两个[链映射](@entry_id:268209) $f, g: C_* \to D_*$ 是链同伦的，那么它们在同调群上诱导的同态是相同的。也就是说，对于所有的 $n$，有：
$$
f_* = g_*: H_n(C) \to H_n(D)
$$

**证明：**
证明这个定理的过程非常直接，并且深刻地揭示了链同伦定义的威力。
1.  取任意一个同调类 $[z] \in H_n(C)$。这个同调类由一个**闭链 (cycle)** $z \in C_n$ 代表，根据定义，这意味着 $z$ 属于[边界算子](@entry_id:160216) $\partial^C_n$ 的核，即 $\partial^C_n(z) = 0$。

2.  根据[诱导同态](@entry_id:266478)的定义，$f_*([z]) = [f_n(z)]$ 以及 $g_*([z]) = [g_n(z)]$。要证明 $f_*([z]) = g_*([z])$，我们只需证明这两个同调类相等，即 $[f_n(z)] = [g_n(z)]$。这等价于证明它们的差 $f_n(z) - g_n(z)$ 在 $D_n$ 中是一个**恰当链 (boundary)**。

3.  现在，我们将链[同伦](@entry_id:139266)的定义式 $f_n - g_n = \partial^D_{n+1} H_n + H_{n-1} \partial^C_n$ 应用到闭链 $z$ 上：
    $$
    f_n(z) - g_n(z) = (\partial^D_{n+1} \circ H_n)(z) + (H_{n-1} \circ \partial^C_n)(z)
    $$

4.  因为 $z$ 是一个闭链，所以 $\partial^C_n(z) = 0$。因此，上式右边的第二项为 $H_{n-1}(0) = 0$。方程简化为：
    $$
    f_n(z) - g_n(z) = \partial^D_{n+1}(H_n(z))
    $$

5.  这个结果至关重要。它明确指出，$f_n(z) - g_n(z)$ 这个链，正是 $D_{n+1}$ 中某个链 $H_n(z)$ 的边界 [@problem_id:1638400]。按照定义，这意味着 $f_n(z) - g_n(z)$ 是 $D_n$ 中的一个恰当链。

6.  因此， $f_n(z) - g_n(z)$ 在同调群 $H_n(D)$ 中代表零元素，即 $[f_n(z) - g_n(z)] = 0$。通过[同态的性质](@entry_id:147906)，这意味着 $[f_n(z)] = [g_n(z)]$。

由于上述论证对任意同调类 $[z]$ 都成立，我们得出结论 $f_* = g_*$。**证毕**。

这个定理的一个直接推论是：如果一个[链映射](@entry_id:268209) $f$ 与零映射 $0$ (即在每个维度上都是零同态) 链[同伦](@entry_id:139266)，那么 $f$ 在同调上诱导的也是零映射。这意味着对于任何闭链 $z$，其像 $f_n(z)$ 必定是一个恰当链 [@problem_id:1638399]。

我们可以通过一个计算来验证这个定理的应用 [@problem_id:1638397]。假设对于一个 2-闭链 $z \in C_2$，我们有 $f_2(z) = 10d$。又假设连接 $f$ 和 $g$ 的[同伦](@entry_id:139266) $h$ 满足 $h_2(z) = 2e$，且[边界算子](@entry_id:160216) $\partial_3^D(e)=6d$。根据上述证明中的关键步骤，我们有 $f_2(z) - g_2(z) = \partial_3^D(h_2(z))$。代入已知条件：
$$
10d - g_2(z) = \partial_3^D(2e) = 2 \cdot \partial_3^D(e) = 2 \cdot (6d) = 12d
$$
解得 $g_2(z) = 10d - 12d = -2d$。这表明，一旦链同伦关系确定，不同映射下闭链的像之间的关系也随之确定，且这种关系与同调的定义完美契合。

### 推论与应用

链[同伦](@entry_id:139266)的概念及其在同调上的不变性引出了一系列重要的[代数结构](@entry_id:137052)和结论。

#### 链[同伦](@entry_id:139266)作为等价关系

在从 $C_*$ 到 $D_*$ 的所有[链映射](@entry_id:268209)的集合上，链[同伦](@entry_id:139266)是一种**等价关系**。
*   **自反性 (Reflexivity):** 任何[链映射](@entry_id:268209) $f$ 都与自身链同伦 ($f \simeq f$)。取 $H=0$ (零同伦)，则 $f-f = 0 = \partial 0 + 0 \partial$。
*   **对称性 (Symmetry):** 如果 $f \simeq g$，那么 $g \simeq f$。如果 $f-g = \partial H + H \partial$，那么 $g-f = \partial(-H) + (-H)\partial$。因此，$g$ 与 $f$ 通过同伦 $-H$ 相联系。
*   **传递性 (Transitivity):** 如果 $f \simeq g$ 且 $g \simeq h$，那么 $f \simeq h$。设 $S^{(1)}$ 是 $f$ 与 $g$ 之间的同伦， $S^{(2)}$ 是 $g$ 与 $h$ 之间的同伦。我们有：
    $$
    f - g = \partial S^{(1)} + S^{(1)} \partial
    $$
    $$
    g - h = \partial S^{(2)} + S^{(2)} \partial
    $$
    将这两个方程相加，得到：
    $$
    (f - g) + (g - h) = (\partial S^{(1)} + S^{(1)} \partial) + (\partial S^{(2)} + S^{(2)} \partial)
    $$
    $$
    f - h = \partial (S^{(1)} + S^{(2)}) + (S^{(1)} + S^{(2)}) \partial
    $$
    这表明 $f$ 和 $h$ 是链同伦的，其间的同伦为 $S^{(1)} + S^{(2)}$ [@problem_id:1638430]。

#### [链同伦等价](@entry_id:270936)

等价关系的存在使我们能够定义更高层次的“等价”概念。

**定义 ([链同伦等价](@entry_id:270936)):** 一个[链映射](@entry_id:268209) $f: C_* \to D_*$ 被称为一个**[链同伦等价](@entry_id:270936) (chain homotopy equivalence)**，如果存在一个反向的[链映射](@entry_id:268209) $g: D_* \to C_*$，称为 $f$ 的**同伦逆 (homotopy inverse)**，使得复合映射 $g \circ f$ 与 $C_*$ 上的恒等映射 $\mathrm{id}_C$ 链同伦 ($g \circ f \simeq \mathrm{id}_C$)，并且 $f \circ g$ 与 $D_*$ 上的[恒等映射](@entry_id:634191) $\mathrm{id}_D$ 链同伦 ($f \circ g \simeq \mathrm{id}_D$)。

这个定义是代数拓扑中最重要的概念之一。它完美地翻译了[拓扑空间](@entry_id:155056)中的同伦等价。其在同调上的推论是直接而强大的。

**定理：** 如果一个[链映射](@entry_id:268209) $f: C_* \to D_*$ 是一个[链同伦等价](@entry_id:270936)，那么它诱导的同调同态 $f_*: H_*(C) \to H_*(D)$ 是一个同构。

**证明：**
设 $g$ 是 $f$ 的同伦逆。我们有 $g \circ f \simeq \mathrm{id}_C$ 和 $f \circ g \simeq \mathrm{id}_D$。
根据同调[不变性定理](@entry_id:264626)，链同伦的映射在同调上诱导相同的同态。因此：
*   从 $g \circ f \simeq \mathrm{id}_C$，我们得到 $(g \circ f)_* = (\mathrm{id}_C)_*$。映射复合的[诱导同态](@entry_id:266478)等于[诱导同态](@entry_id:266478)的复合，即 $g_* \circ f_* = (\mathrm{id}_C)_*$。而恒等映射诱导的显然是同调群上的恒等同态，所以 $g_* \circ f_* = \mathrm{id}_{H_*(C)}$。
*   同理，从 $f \circ g \simeq \mathrm{id}_D$，我们得到 $f_* \circ g_* = \mathrm{id}_{H_*(D)}$。

这两个条件表明，$f_*: H_*(C) \to H_*(D)$ 是一个[群同构](@entry_id:147371)，其逆同构正是 $g_*: H_*(D) \to H_*(C)$ [@problem_id:1638432]。

一个特殊情况是，如果一个[链映射](@entry_id:268209) $f: C \to C$ 与恒等映射 $\mathrm{id}_C$ 链[同伦](@entry_id:139266)，那么它诱导的同调映射 $f_*$ 就是同调群上的恒等映射 $\mathrm{id}_{H_*(C)}$ [@problem_id:1638414]。

#### 可缩[链复形](@entry_id:150246)

[链同伦等价](@entry_id:270936)的一个极端但重要的例子是**可缩[链复形](@entry_id:150246) (contractible chain complex)**。

**定义 (可缩[链复形](@entry_id:150246)):** 一个[链复形](@entry_id:150246) $C_*$ 如果其恒等映射 $\mathrm{id}_C$ 与零映射 $0$ 链同伦，则称其为可缩的。满足 $\mathrm{id}_C - 0 = \partial H + H \partial$ 的[同伦](@entry_id:139266) $H$ 被称为**[收缩同伦](@entry_id:264916) (contracting homotopy)**。

可缩[链复形](@entry_id:150246)的同调性质是平凡的。由于 $\mathrm{id}_C \simeq 0$，它们诱导的同调映射必须相等：$(\mathrm{id}_C)_* = 0_*$。这意味着对所有 $n$，同调群上的恒等映射 $\mathrm{id}_{H_n(C)}$ 等于零映射。一个群上的恒等映射是零映射的唯一可能性是这个群本身是平凡群 $\{0\}$。

因此，**一个可缩[链复形](@entry_id:150246)是无闭链的 (acyclic)，即其所有同调群均为平凡群** ($H_n(C) = 0$ for all $n$)。实际上，[收缩同伦](@entry_id:264916)的存在性给出了一个更强的结论：对于任何闭链 $z \in C_n$，我们有 $z = \mathrm{id}_C(z) - 0(z) = \partial(H_n(z)) + H_{n-1}(\partial(z)) = \partial(H_n(z))$。这表明**在可缩[链复形](@entry_id:150246)中，每一个闭链都是恰当链** [@problem_id:1638695]。

### 深入探讨：微妙之处与反例

尽管链[同伦](@entry_id:139266)与同调之间的关系非常紧密，但我们必须小心，不要做出超出定理范畴的推断。

#### 定理的逆命题不成立

我们已经证明，如果两个[链映射](@entry_id:268209)链同伦，则它们诱导相同的同调映射。那么反过来是否成立呢？即：**如果 $f_* = g_*$，是否一定有 $f \simeq g$？**

答案是否定的。这是一个非常重要的微妙之处，它告诉我们同调虽然是一个强大的[不变量](@entry_id:148850)，但它并没有捕捉到[链映射](@entry_id:268209)的全部链[同伦](@entry_id:139266)信息。

**反例 [@problem_id:1638216]：**
考虑一个基于 $\mathbb{Z}_4$-模的[链复形](@entry_id:150246) $C_*$，其中 $C_1 = \mathbb{Z}_4 a$，$C_0 = \mathbb{Z}_4 b$，其余 $C_n=0$。[边界映射](@entry_id:151165) $d_1: C_1 \to C_0$ 定义为 $d_1(a) = 2b$。（我们可验证 $\partial_0 \circ d_1 = 0$，因为 $d_0=0$）。

定义两个[链映射](@entry_id:268209) $f, g: C_* \to C_*$：
*   $f$ 是零映射：$f_1=0, f_0=0$。
*   $g$ 定义为：$g_1(a) = 2a$, $g_0(b) = 0$。（可验证 $g$ 是一个[链映射](@entry_id:268209)：$d_1(g_1(a)) = d_1(2a) = 2(2b) = 4b = 0$，而 $g_0(d_1(a)) = g_0(2b) = 2g_0(b) = 0$）。

首先，我们[计算同调](@entry_id:161051)群并检验 $f_*$ 和 $g_*$。
$H_1(C) = \ker(d_1) / \mathrm{im}(d_2) = \ker(d_1) / 0$。$\ker(d_1)$ 由满足 $k \cdot d_1(a) = k(2b)=0$ 的 $ka$ 组成。在 $\mathbb{Z}_4$ 中，这要求 $2k \equiv 0 \pmod 4$，即 $k$ 是偶数。所以 $\ker(d_1) = \{0, 2a\} \cong \mathbb{Z}_2$。
$H_0(C) = \ker(d_0) / \mathrm{im}(d_1) = C_0 / \{0, 2b\} \cong \mathbb{Z}_4 / 2\mathbb{Z}_4 \cong \mathbb{Z}_2$。

$f_*$ 显然是零映射。对于 $g_*$，在 $H_1(C)$ 上，生成元是 $[2a]$，$g_1(2a) = 2(2a) = 4a = 0$，所以 $g_{1*}$ 是零映射。在 $H_0(C)$ 上，$g_0$ 本身就是零映射，所以 $g_{0*}$ 也是零映射。因此，$f_*=g_*=0$。

现在我们检查 $f$ 和 $g$ 是否链[同伦](@entry_id:139266)。如果它们是链[同伦](@entry_id:139266)的，则存在一个映射 $h_0: C_0 \to C_1$ (因为 $C_2=0$，所以 $h_1=0$) 满足 $g-f = dh+hd$。设 $h_0(b) = m a$ for $m \in \{0,1,2,3\}$。
*   在维度 $n=1$，$g_1 - f_1 = d_2 h_1 + h_0 d_1 \implies g_1 = h_0 d_1$。作用在 $a$ 上：
    $g_1(a) = h_0(d_1(a)) \implies 2a = h_0(2b) = 2 h_0(b) = 2(ma) = (2m)a$。
    在 $\mathbb{Z}_4$ 中，$2 \equiv 2m \pmod 4$，这意味着 $2(m-1) \equiv 0 \pmod 4$，所以 $m-1$ 必须是偶数，即 $m \in \{1, 3\}$。
*   在维度 $n=0$，$g_0 - f_0 = d_1 h_0 + h_{-1} d_0 \implies 0 = d_1 h_0$。作用在 $b$ 上：
    $0 = d_1(h_0(b)) = d_1(ma) = m d_1(a) = m(2b) = (2m)b$。
    在 $\mathbb{Z}_4$ 中，$2m \equiv 0 \pmod 4$，这意味着 $m$ 必须是偶数，即 $m \in \{0, 2\}$。

维度 $1$ 的条件要求 $m \in \{1, 3\}$，而维度 $0$ 的条件要求 $m \in \{0, 2\}$。这两个集合没有交集，因此不存在满足条件的[同伦](@entry_id:139266) $h_0$。我们得出结论：$f$ 和 $g$ 虽然诱导了相同的同调映射，但它们不是链[同伦](@entry_id:139266)的。

#### 定义的合理性

最后，我们来思考链[同伦](@entry_id:139266)定义的细节。为什么是 $f - g = \partial H + H \partial$ 而不是其他形式，比如 $f - g = \partial H - H \partial$？

这个问题触及了定义的深刻代数根源 [@problem_id:1638415]。让我们假设存在一个“另类”同伦关系 $f - g = \partial H - H \partial$。我们来检验这个关系是否在[链映射](@entry_id:268209)的集合中保持良好性质。
假设 $f$ 是一个[链映射](@entry_id:268209)，即 $\partial f = f \partial$。并设 $g$ 由此关系定义：$g = f - (\partial H - H \partial)$。我们来检验 $g$ 是否也是一个[链映射](@entry_id:268209)。计算 $\partial g - g \partial$：
$$
\begin{align*}
\partial g - g \partial  &= \partial (f - \partial H + H \partial) - (f - \partial H + H \partial) \partial \\
 &= (\partial f - f \partial) - \partial(\partial H) + \partial(H \partial) + (\partial H)\partial - (H \partial)\partial \\
 &= 0 - 0 + \partial H \partial + \partial H \partial - 0 \\
 &= 2 \partial H \partial
\end{align*}
$$
（这里我们使用了 $\partial^2=0$ 和 $f$ 是[链映射](@entry_id:268209)的性质。）

结果表明，$\partial g - g \partial = 2 \partial H \partial$。为了使 $g$ 成为一个[链映射](@entry_id:268209)，这个表达式必须为零。然而，在一般的[阿贝尔群](@entry_id:150284)或模的[链复形](@entry_id:150246)中，没有理由保证 $2 \partial H \partial = 0$。例如，如果我们的系数域是整数 $\mathbb{Z}$ 或实数 $\mathbb{R}$，这个表达式通常不为零。

这意味着，这个“另类”的同伦定义通常不会将一个[链映射](@entry_id:268209)关联到另一个[链映射](@entry_id:268209)。它没有在[链映射](@entry_id:268209)的集合上定义一个等价关系。相反，我们标准的定义 $f-g = \partial H + H \partial$ (其[代数结构](@entry_id:137052)是一个**分次交换子 (graded commutator)**) 具有保持[链映射](@entry_id:268209)性质的优良特性。这个看似微小的符号差异，实际上保证了整个理论框架的代数一致性和和谐性。

通过本章的学习，我们建立了链同伦这一核心概念，证明了其在同调上的[不变性](@entry_id:140168)，并探讨了它作为[链同伦等价](@entry_id:270936)和[可缩性](@entry_id:154431)等重要思想的基石作用。我们还通过反例和对定义的剖析，加深了对其背后深刻[代数结构](@entry_id:137052)的理解。在接下来的章节中，我们将看到链同伦如何成为连接拓扑与代数的关键纽带。