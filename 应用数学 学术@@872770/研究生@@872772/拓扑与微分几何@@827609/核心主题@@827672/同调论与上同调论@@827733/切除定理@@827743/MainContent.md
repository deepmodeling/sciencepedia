## 引言
在[代数拓扑学](@entry_id:138192)中，引入[相对同调群](@entry_id:159711)为我们提供了一种研究带有[子空间](@entry_id:150286)结构的空间的强大代数[不变量](@entry_id:148850)。然而，直接从定义出发计算这些群往往非常复杂，这构成了一个显著的知识鸿沟和计算障碍。为了解决这一问题，数学家们发展了一系列强大的工具，其中切除定理 (Excision Theorem) 居于核心地位。它提供了一种看似简单却极其深刻的方法，通过“切除”空间中无关紧要的部分来简化[相对同调群](@entry_id:159711)的计算，从而揭示空间的局部[拓扑性质](@entry_id:141605)。

本文旨在全面解析切除定理。在“原理与机制”一章中，我们将深入探讨该定理的精确陈述、其假设条件的必要性，并通过反例理解其边界。接着，在“应用与跨学科联系”一章中，我们将展示该定理如何作为基石，支撑起[局部同调](@entry_id:160439)、[流形定向](@entry_id:159308)理论以及[Mayer-Vietoris序列](@entry_id:161286)等重要概念和工具。最后，通过“动手实践”一章，读者将有机会应用所学知识解决具体的拓扑问题，加深对切除定理实际操作的理解。

## 原理与机制

在引入了[相对同调](@entry_id:159348)的概念之后，我们自然会寻求强大的计算工具来处理这些新的代数[不变量](@entry_id:148850)。切除定理 (Excision Theorem) 正是这样一个核心工具，它极大地简化了[相对同调群](@entry_id:159711)的计算。该定理的本质思想是，[相对同调群](@entry_id:159711) $H_n(X, A)$ 捕捉的是空间 $X$ 在[子空间](@entry_id:150286) $A$ “附近”的拓扑性质，因此，切除掉 $A$ 内部与边界无关的部分，并不会改变这个[相对同调群](@entry_id:159711)。本章将深入探讨切除定理的精确陈述、其假设条件的必要性，以及它在[局部同调](@entry_id:160439)、[流形定向](@entry_id:159308)和证明其他基本定理（如[Mayer-Vietoris序列](@entry_id:161286)）中的深刻应用。

### 切除定理：陈述与直观理解

切除定理允许我们从一对[拓扑空间](@entry_id:155056) $(X, A)$ 中“切除”一部分 $U$，从而得到一个更小、可能更易于处理的空间偶，而其[相对同调群](@entry_id:159711)保持不变。

**切除定理**：设 $X$ 是一个[拓扑空间](@entry_id:155056)，$A$ 是其[子空间](@entry_id:150286)。令 $U$ 是 $A$ 的一个[子集](@entry_id:261956)，满足其在 $X$ 中的闭包包含于 $A$ 在 $X$ 中的内部，即 $\text{cl}(U) \subseteq \text{int}(A)$。那么，由包含映射 $i: (X \setminus U, A \setminus U) \hookrightarrow (X, A)$ 诱导的同调[群同态](@entry_id:140603)

$$ i_*: H_n(X \setminus U, A \setminus U) \to H_n(X, A) $$

对于所有维度 $n \ge 0$ 都是一个同构。

这个定理的直观意义在于，[相对同调群](@entry_id:159711) $H_n(X, A)$ 对空间 $A$ 中“深埋”的部分不敏感。条件 $\text{cl}(U) \subseteq \text{int}(A)$ 精确地描述了这种“深埋”的状态：$U$ 不仅包含在 $A$ 中，而且它的[闭包](@entry_id:148169)也完全位于 $A$ 的内部，意味着 $U$ 远离 $A$ 在 $X$ 中的边界。因此，将 $U$ 从 $X$ 和 $A$ 中同[时移](@entry_id:261541)除，不会改变 $X$ 相对于 $A$ 的拓扑结构。

例如，考虑球面 $S^2$ 和其上的一个[闭圆盘](@entry_id:148403) $A$（比如北半球）。我们可以通过切除 $A$ 的内部的一个稍小的开圆盘 $U$ 来简化计算。此时， $(S^2 \setminus U, A \setminus U)$ 近似于 $(S^2 \setminus A, \partial A)$，而通过一点[紧化](@entry_id:150518)，$S^2 \setminus A$ 同胚于一个开圆盘，其边界是 $\partial A \cong S^1$。这启发我们 $H_n(S^2, A)$ 可能与 $H_n(D^2, S^1)$ 同构，事实也的确如此[@problem_id:1670788]。

在许多应用中，该定理的另一种形式也十分有用，它通常用于处理由两个[子空间](@entry_id:150286)并集构成的空间。如果空间 $X$ 是两个[子空间](@entry_id:150286) $A$ 和 $B$ 的并集，且 $X$ 被 $A$ 和 $B$ 的内部所覆盖（即 $X = \text{int}(A) \cup \text{int}(B)$），那么切除定理保证了包含映射 $(B, A \cap B) \hookrightarrow (A \cup B, A)$ 诱导的同构 $H_n(B, A \cap B) \cong H_n(X, A)$。

### 假设条件的至关重要性

切除定理的威力蕴含在其严格的假设条件中。如果条件 $\text{cl}(U) \subseteq \text{int}(A)$ 不成立，同构关系通常就会失效。这是因为，如果 $U$ 的[闭包](@entry_id:148169)接触到了 $A$ 的边界，那么切除 $U$ 就可能会改变 $X$ 与 $A$ 之间的根本拓扑关系。

为了清晰地说明这一点，让我们构造一个反例[@problem_id:1681027]。令 $X = \mathbb{R}^2$ 为欧几里得平面，$A = [0, 1] \times \{0\}$ 为 $x$ 轴上的闭线段。我们想要切除 $A$ 的“内部”部分，即开线段 $U = (0, 1) \times \{0\}$。首先，我们必须在 $X = \mathbb{R}^2$ 的拓扑中考察定理的假设。$A$ 作为 $\mathbb{R}^2$ 中的一个线段，其内部 $\text{int}(A)$ 是[空集](@entry_id:261946) $\emptyset$。因此，对于非空的 $U$，其闭包 $\text{cl}(U) = A$ 显然不包含于 $\text{int}(A) = \emptyset$。假设条件被严重违反了。

现在我们来计算相关的同调群。
对于空间偶 $(X, A) = (\mathbb{R}^2, [0,1]\times\{0\})$，由于 $A$ 是 $\mathbb{R}^2$ 中的一个可缩[子空间](@entry_id:150286)，空间偶 $(X, A)$ 是一个好对，其[相对同调群](@entry_id:159711)同构于商空间 $X/A$ 的[约化同调](@entry_id:274187)群。由于 $X$ [形变收缩](@entry_id:148036)到 $A$ 上，商空间 $X/A$ 是可缩的，因此其[约化同调](@entry_id:274187)群为零。特别地，$H_1(\mathbb{R}^2, A) = 0$。

然而，对于切除后的空间偶 $(X \setminus U, A \setminus U)$，情况截然不同。这里 $X \setminus U = \mathbb{R}^2 \setminus ((0,1)\times\{0\})$ 是移除了一个开线段的平面，而 $A \setminus U = \{(0,0), (1,0)\}$ 是两个端点。空间 $X \setminus U$ 并非单连通的，它同伦等价于一个圆 $S^1$（例如，通过将平面[形变收缩](@entry_id:148036)到环绕被移除线段的一个圆周上）。因此，$H_1(X \setminus U) \cong \mathbb{Z}$。
我们可以利用长正合序列来计算 $H_1(X \setminus U, A \setminus U)$。[长正合序列](@entry_id:153438)的相关部分是：
$$ \cdots \to H_1(A \setminus U) \to H_1(X \setminus U) \to H_1(X \setminus U, A \setminus U) \to H_0(A \setminus U) \to H_0(X \setminus U) \to \cdots $$
我们有 $H_1(A \setminus U)=0$（因为 $A \setminus U$ 是两个点），$H_1(X \setminus U) \cong \mathbb{Z}$，$H_0(A \setminus U) \cong \mathbb{Z} \oplus \mathbb{Z}$（由两个点生成），以及 $H_0(X \setminus U) \cong \mathbb{Z}$（因为 $X \setminus U$ 是道路连通的）。包含映射 $i_*: H_0(A \setminus U) \to H_0(X \setminus U)$ 将两个生成元都映到同一个生成元上，因此其核 $\ker(i_*)$ 同构于 $\mathbb{Z}$。
序列变为：
$$ \cdots \to \mathbb{Z} \xrightarrow{j_*} H_1(X \setminus U, A \setminus U) \xrightarrow{\partial_*} \mathbb{Z} \oplus \mathbb{Z} \xrightarrow{i_*} \mathbb{Z} \to \cdots $$
由正合性，我们有一个短[正合序列](@entry_id:151503)：
$$ 0 \to \text{coker}(j_*) \to H_1(X \setminus U, A \setminus U) \to \ker(i_*) \to 0 $$
即 $0 \to \text{coker}(j_*) \to H_1(X \setminus U, A \setminus U) \to \mathbb{Z} \to 0$。可以证明，从 $H_1(X \setminus U)$ 到 $H_1(X \setminus U, A \setminus U)$ 的映射 $j_*$ 是[单射](@entry_id:183792)，因此 coker($j_*) \cong \mathbb{Z}$。故该短[正合序列](@entry_id:151503)分裂，我们得到 $H_1(X \setminus U, A \setminus U) \cong \mathbb{Z} \oplus \mathbb{Z}$。

我们得到了 $H_1(X, A) = 0$ 而 $H_1(X \setminus U, A \setminus U) \cong \mathbb{Z} \oplus \mathbb{Z}$。切除同构不成立。失败的根源在于我们切除的集合 $U$ 在背景空间 $X$ 的意义下是“无内部的”，它紧贴着自己的边界。

另一个更微妙的例子是[拓扑学家的正弦曲线](@entry_id:142923)[@problem_id:1681029]，它由图像 $G = \{(x, \sin(1/x)) \mid x \in (0, 1]\}$ 和极限段 $L = \{0\} \times [-1, 1]$ 构成。这个集合 $A = G \cup L$ 在 $\mathbb{R}^2$ 中是[闭集](@entry_id:136446)，但其内部为空集。这意味着，我们无法使用切除定理来切除 $A$ 的任何非空开[子集](@entry_id:261956) $U \subset A$，因为条件 $\text{cl}(U) \subseteq \text{int}(A) = \emptyset$ 永远无法满足。

### 关键应用一：[局部同调](@entry_id:160439)与[流形](@entry_id:153038)的结构

切除定理最重要和最深刻的应用之一是它使“局部”拓扑性质的研究成为可能。我们可以定义一个空间 $X$ 在点 $x$ 处的**[局部同调群](@entry_id:272269) (local homology groups)** 为[相对同调群](@entry_id:159711) $H_n(X, X \setminus \{x\})$。

直观上，这个群应该只依赖于 $X$ 在 $x$ 点任意小的邻域内的结构。切除定理为这个直观想法提供了严格的证明。令 $V$ 是 $x$ 的任意一个[开邻域](@entry_id:268496)。我们考虑空间偶 $(X, X \setminus \{x\})$，并希望切除掉 $V$ 以外的所有部分。令 $U = X \setminus V$。那么 $U$ 是一个[闭集](@entry_id:136446)，所以 $\text{cl}(U) = U = X \setminus V$。而 $A = X \setminus \{x\}$ 的内部是其自身，因为 $\{x\}$ 是[闭集](@entry_id:136446)。切除定理的条件是 $\text{cl}(U) \subseteq \text{int}(A)$，即 $X \setminus V \subseteq X \setminus \{x\}$。这等价于 $\{x\} \subseteq V$，根据 $V$是$x$的邻域，这个条件成立。

应用切除定理，我们得到同构：
$$ H_n(X \setminus (X \setminus V), (X \setminus \{x\}) \setminus (X \setminus V)) \cong H_n(X, X \setminus \{x\}) $$
这可以简化为：
$$ H_n(V, V \setminus \{x\}) \cong H_n(X, X \setminus \{x\}) $$
这个同构关系意义非凡：它表明，要计算 $X$ 在 $x$ 点的[局部同调](@entry_id:160439)，我们不需要整个空间 $X$，只需要 $x$ 的任意一个邻域 $V$ 就足够了。

这一结论在研究[流形](@entry_id:153038)时威力尽显。一个 $n$ 维[拓扑流形](@entry_id:271368) $M$ 的定义是，其上每一点 $x$ 都有一个[开邻域](@entry_id:268496) $V$[同胚](@entry_id:146933)于欧几里得空间 $\mathbb{R}^n$。结合上述结论，我们可以计算任何 $n$ 维[流形](@entry_id:153038)在任意点 $x$ 的[局部同调](@entry_id:160439)[@problem_id:1661090] [@problem_id:1661147]：
$$ H_k(M, M \setminus \{x\}) \cong H_k(V, V \setminus \{x\}) \cong H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\}) $$
为了计算 $H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\})$，我们可以再次使用切除，切除掉单位[闭球](@entry_id:157850) $D^n$ 外面的部分。这给出 $H_k(\mathbb{R}^n, \mathbb{R}^n \setminus \{0\}) \cong H_k(D^n, D^n \setminus \{0\})$。注意到 $D^n \setminus \{0\}$ 同伦等价于球面 $S^{n-1}$，因此 $H_k(D^n, D^n \setminus \{0\}) \cong H_k(D^n, S^{n-1})$。

利用空间偶 $(D^n, S^{n-1})$ 的长正合序列：
$$ \cdots \to H_k(D^n) \to H_k(D^n, S^{n-1}) \to H_{k-1}(S^{n-1}) \to H_{k-1}(D^n) \to \cdots $$
由于 $D^n$ 是可缩的，对于 $k \ge 1$，$H_k(D^n)=0$ 和 $H_{k-1}(D^n)=0$。因此，对于 $k \ge 2$，序列变为 $0 \to H_k(D^n, S^{n-1}) \to H_{k-1}(S^{n-1}) \to 0$，这意味着 $H_k(D^n, S^{n-1}) \cong H_{k-1}(S^{n-1})$。

特别地，在最高维度 $k=n$ ($n \ge 1$)，我们得到：
$$ H_n(M, M \setminus \{x\}) \cong H_{n-1}(S^{n-1}) \cong \mathbb{Z} $$
而在其他维度 $k \neq n$，$H_k(M, M \setminus \{x\}) \cong \tilde{H}_{k-1}(S^{n-1}) = 0$（对于$k \geq 1$）。

这个惊人的结果表明，所有 $n$ 维[流形](@entry_id:153038)在任何一点都具有相同的[局部同调](@entry_id:160439)结构：在维度 $n$ 有一个 $\mathbb{Z}$ 群，其他维度则为[平凡群](@entry_id:151996)。例如，[二维环面](@entry_id:265991) $T^2$ 在任意一点 $p$ 的二阶[局部同调群](@entry_id:272269) $H_2(T^2, T^2 \setminus \{p\})$ 都同构于 $\mathbb{Z}$[@problem_id:1661147]。

### 关键应用二：从局部到全局——定向与[基本类](@entry_id:158335)

[局部同调](@entry_id:160439)的概念为[流形的定向](@entry_id:160954)理论提供了代[数基](@entry_id:634389)础。我们已经知道，对于一个连通的 $n$ 维[流形](@entry_id:153038) $M$，每个[局部同调群](@entry_id:272269) $H_n(M, M \setminus \{x\})$ 都同构于 $\mathbb{Z}$。这意味着该群有两个生成元，一个可记为 $1$，另一个是 $-1$。

一个 $M$ 上的**定向 (orientation)** 就是为每一点 $x \in M$ 一致地选择一个 $H_n(M, M \setminus \{x\})$ 的生成元 $\mu_x$[@problem_id:1682089]。所谓“一致地”，粗略地说，是指当点 $x$ 在[流形](@entry_id:153038)上连续移动时，其对应的生成元 $\mu_x$ 也“连续”变化，不会突然从 $1$ 跳到 $-1$。

一旦一个紧致、连通的[流形](@entry_id:153038)被赋予了一个定向 $\{\mu_x\}_{x \in M}$，我们就可以定义一个全局的同调类，称为**[基本类](@entry_id:158335) (fundamental class)**，记作 $[M]$。这是一个属于 $H_n(M)$ 的特定同调类，它与所有[局部定向](@entry_id:264384) $\mu_x$ 通过如下方式联系起来：
对于每一点 $x \in M$，存在一个由包含映射 $(M, \emptyset) \hookrightarrow (M, M \setminus \{x\})$ 诱导的自然同态 $j_x: H_n(M) \to H_n(M, M \setminus \{x\})$。[基本类](@entry_id:158335) $[M]$ 就是 $H_n(M)$ 中那个唯一的、满足以下条件的生成元：
$$ j_x([M]) = \mu_x \quad \text{对于所有 } x \in M $$
这个定义是合理的，因为对于一个连通的 $n$ 维[可定向流形](@entry_id:276936)，$H_n(M)$ 也同构于 $\mathbb{Z}$，因此存在两个生成元。[基本类](@entry_id:158335) $[M]$ 就是与所选定向相容的那一个。这个等式完美地体现了局部与全局的联系：一个全局的同调类 $[M]$ 的性质，可以通过它在每一点的“局部化”或“投影” $j_x([M])$ 来刻画。切除定理正是建立这一切的基石，因为它保证了[局部同调群](@entry_id:272269)的良定义性和一致性。

### 关键应用三：同调论中的基础工具

除了在[流形理论](@entry_id:263722)中的核心地位，切除定理也是证明其他许多同调论基本定理的关键步骤。

**1. [Mayer-Vietoris序列](@entry_id:161286)的推导**

[Mayer-Vietoris序列](@entry_id:161286)是另一个强大的同调计算工具，它关联了一个空间 $X=A \cup B$ 的同调群与[子空间](@entry_id:150286) $A$、$B$ 以及它们的交集 $A \cap B$ 的同调群。在它的标准代数推导中，一个关键步骤是证明同构 $H_n(X, B) \cong H_n(A, A \cap B)$[@problem_id:1681009]。

这个同构正是切除定理的直接推论。我们考虑空间偶 $(X, B)$，并切除[子集](@entry_id:261956) $U = X \setminus A$。为了应用切除定理，我们需要验证 $\text{cl}(U) \subseteq \text{int}(B)$，即 $\text{cl}(X \setminus A) \subseteq \text{int}(B)$。这正是推导[Mayer-Vietoris序列](@entry_id:161286)所需要的标准“切除友好”条件（即 $(A,B)$ 构成一个excisive couple）。在该条件下，切除定理给出：
$$ H_n(X \setminus (X \setminus A), B \setminus (X \setminus A)) \cong H_n(X, B) $$
左边化简后即为 $H_n(A, B \cap A)$。这样，我们就利用切除定理建立了证明[Mayer-Vietoris序列](@entry_id:161286)所需的核心代数联系。

**2. 商空间的同调**

另一个重要的应用是在计算[商空间](@entry_id:274314)的同调群时。对于所谓的“好对” $(X, A)$（即 $A$ 是 $X$ 的一个[闭子集](@entry_id:155133)，且在 $X$ 中存在一个邻域 $V$ 使得 $A$ 是 $V$ 的[形变收缩](@entry_id:148036)核），有一个基本结论：$H_n(X, A) \cong \tilde{H}_n(X/A)$，其中 $\tilde{H}$ 表示简约同调。

这个结论的证明过程巧妙地运用了切除定理[@problem_id:1681031]。证明的大致思路如下：
首先，利用 $A$ 是 $V$ 的[形变收缩](@entry_id:148036)核这一事实，可以从三元组 $(X, V, A)$ 的长正合序列中推出 $H_n(X, A) \cong H_n(X, V)$。
接下来是关键的切除步骤。我们对空间偶 $(X, V)$ 切除[子集](@entry_id:261956) $A$。由于 $A$ 是[闭集](@entry_id:136446)且包含在 $V$ 的内部（因为 $V$ 是 $A$ 的邻域），我们有 $\text{cl}(A) = A \subseteq \text{int}(V)$。切除定理的条件得到满足。因此，我们有同构：
$$ H_n(X, V) \cong H_n(X \setminus A, V \setminus A) $$
结合第一步，我们得到 $H_n(X, A) \cong H_n(X \setminus A, V \setminus A)$。证明的后续步骤会将右侧的群与商空间 $X/A$ 的同调群联系起来，最终得到所需的结果。这个例子再次展示了切除定理如何通过巧妙地选择切除对象来连接看似不同的拓扑构造。

### 证明一瞥：拓扑与代数的交汇

切除定理的证明本身是[奇异同调](@entry_id:158380)理论的一大成就，它深刻地揭示了代数构造（[链复形](@entry_id:150246)）与点集拓扑性质之间的联系。其核心思想是证明，对于任何一个链 $c \in C_n(X)$，它都同一个“小”链 $c'$ 同调，其中 $c'$ 是由许多小的单纯形之和构成，每个小单纯形的像都完全落在 $A$ 的内部或者 $X \setminus U$ 的内部。

这一论证通常被称为“[重心](@entry_id:273519)重分引理”或“小单纯形引理”。它断言，对于 $X$ 的任意[开覆盖](@entry_id:140020) $\mathcal{V}$，包含映射 $C_n^{\mathcal{V}}(X) \hookrightarrow C_n(X)$（其中前者是由其像含于某个[开覆盖](@entry_id:140020)成员中的单纯形生成的[子复形](@entry_id:264130)）是一个[链同伦等价](@entry_id:270936)。对于切除定理，我们使用的开覆盖是 $\{\text{int}(A), X \setminus \text{cl}(U)\}$。

值得注意的是，这个引理的某些证明方法对空间 $X$ 的点集拓扑性质提出了要求[@problem_id:1672427]。一种经典的证明策略是为开覆盖构造一个[单位分解](@entry_id:150115)。例如，对于由两个开集 $\{\mathcal{O}_1, \mathcal{O}_2\}$ 构成的覆盖，我们需要找到[连续函数](@entry_id:137361) $\lambda_1, \lambda_2: X \to [0,1]$，使得 $\lambda_1(x) + \lambda_2(x) = 1$，且 $\lambda_1$ 的支集在 $\mathcal{O}_1$ 内，$\lambda_2$ 的支集在 $\mathcal{O}_2$ 内。[Urysohn引理](@entry_id:150431)保证了在**[正规空间](@entry_id:152381)** ($T_4$) 中，这样的单位分解总是存在的。然而，如果空间 $X$ 仅仅是正则的 ($T_3$) 而非正规的，[Urysohn引理](@entry_id:150431)不成立，这种基于单位分解的证明策略就会在第一步——断言[单位分解](@entry_id:150115)的存在性——上失败。

这揭示了一个深刻的事实：虽然[奇异同调](@entry_id:158380)对于许多“行为良好”的空间（如[CW复形](@entry_id:150589)）表现出强大的威力，但它的理论基础与空间的底层点集拓扑性质紧密相连。切除定理的成立，最终依赖于能够将拓扑问题（链的分解）转化为代数操作（[链同伦](@entry_id:158964)）的精妙论证，而这些论证在最深层次上，需要空间的拓扑结构足够“好”。