## 引言
在代数拓扑的宏伟殿堂中，[奇异上同调](@entry_id:271229)是衡量和区分拓扑空间的核心[不变量](@entry_id:148850)。然而，这一经典理论在处理某些基础但重要的拓扑构造时，其表述会略显繁琐，例如，单点空间的0阶[上同调](@entry_id:160558)并非[平凡群](@entry_id:151996)，这为悬挂同构等重要定理的表述带来了不便。为了克服这些障碍，并构建一个在处理带基点空间时更为简洁、优雅的理论框架，[代数拓扑学](@entry_id:138192)家们引入了**约化上同调 (Reduced Cohomology)** 的概念。

本文旨在为读者系统地介绍约化[上同调](@entry_id:160558)。在**第一章：原理和机制**中，我们将从[增广链复形](@entry_id:274443)出发，详细阐述约化上同调的定义，并揭示其与普通上同调之间的精确代数关系，同时探讨其在[可缩空间](@entry_id:153541)上的重要性质。接下来的**第二章：应用与跨学科联系**，将展示约化[上同调](@entry_id:160558)的强大威力，探讨它如何简化[楔和](@entry_id:270607)、悬置等拓扑构造的计算，并通过[亚历山大对偶](@entry_id:161895)性、纤维丛理论等高级主题，展现其在现代几何与物理中的应用。最后，在**第三章：动手实践**中，我们提供了一系列精选的计算问题，旨在帮助读者巩固理论知识，并将抽象概念应用于具体拓扑空间的分析中。

通过这三章的学习，您将不仅掌握约化上同调的计算方法，更能深刻理解它为何是代数拓扑工具箱中不可或缺的一部分。让我们首先深入其核心，从定义和基本原理开始探索。

## 原理和机制

在前一章中，我们介绍了[奇异上同调](@entry_id:271229)作为一种从拓扑空间中提取代数[不变量](@entry_id:148850)的强大工具。然而，标准的[上同调理论](@entry_id:270863)在处理某些基本对象和构造时，其表述会显得有些累赘。例如，单点空间的 $0$ 阶[上同调群](@entry_id:142450)不是[平凡群](@entry_id:151996)，这使得某些定理的表述（如悬挂同构）需要特殊处理。为了简化理论并使其在特定情况下更加优雅和有力，我们引入了**约化[上同调](@entry_id:160558) (reduced cohomology)** 的概念。本章将详细阐述约化[上同调](@entry_id:160558)的定义、基本性质及其在关键定理中的应用。

### 定义约化[上同调](@entry_id:160558)：一种必要的精炼

我们首先要回答一个问题：为什么我们需要另一个版本的[上同调](@entry_id:160558)？答案在于我们希望有一个“表现更好”的理论，特别是对于[带基点的空间](@entry_id:273706)。在这样的理论中，我们期望最简单的非空空间——单点空间——在所有维度上都具有平凡的上同调群。普通[上同调](@entry_id:160558)不满足这一点，因为一个单点空间的 $0$ 阶上同调群与系数[群同构](@entry_id:147371)。约化上同调正是为了修正这一点而设计的。

其构造始于对奇异[链复形](@entry_id:150246)的一个小小修改。对于一个[拓扑空间](@entry_id:155056) $X$，其奇异[链复形](@entry_id:150246) $C_\bullet(X)$ 形如：
$$ \dots \xrightarrow{\partial_3} C_2(X) \xrightarrow{\partial_2} C_1(X) \xrightarrow{\partial_1} C_0(X) \to 0 $$
其中 $C_n(X)$ 是 $n$-[奇异单纯形](@entry_id:265569)的自由[阿贝尔群](@entry_id:150284)，$\partial_n$ 是[边界映射](@entry_id:151165)。我们通过引入一个**[增广映射](@entry_id:272732) (augmentation map)** $\varepsilon: C_0(X) \to \mathbb{Z}$ 来扩展这个复形。这个映射作用于 $C_0(X)$ 的一个基元素（一个 $0$-单纯形，即 $X$ 中的一个点）时取值为 $1$，然后线性扩展到整个 $C_0(X)$。直观地说，$\varepsilon$ 计算了一个 $0$-链中所有系数的总和。由于任何 $1$-单纯形的边界都由两个点组成，其形式为 $\sigma_1 - \sigma_0$，[增广映射](@entry_id:272732)作用于其上结果为 $1-1=0$，因此我们有 $\varepsilon \circ \partial_1 = 0$。这使得我们可以构造**[增广链复形](@entry_id:274443) (augmented chain complex)**：
$$ \dots \xrightarrow{\partial_2} C_1(X) \xrightarrow{\partial_1} C_0(X) \xrightarrow{\varepsilon} \mathbb{Z} \to 0 $$
这个复形在所有非负维度的同调群（称为[约化同调](@entry_id:274187)群 $\tilde{H}_n(X)$）与普通同调群 $H_n(X)$ 几乎相同，除了在 $0$ 维。

为了定义约化[上同调](@entry_id:160558)，我们将 $\text{Hom}(-, G)$ 函子应用于这个[增广链复形](@entry_id:274443)，其中 $G$ 是系数[阿贝尔群](@entry_id:150284)。这产生了一个**约化上[链复形](@entry_id:150246) (reduced cochain complex)**：
$$ 0 \to \text{Hom}(\mathbb{Z}, G) \xrightarrow{\varepsilon^*} \text{Hom}(C_0(X), G) \xrightarrow{\delta^0} \text{Hom}(C_1(X), G) \xrightarrow{\delta^1} \dots $$
其中 $\delta^n$ 是上边缘算子。我们定义空间 $X$ 的第 $n$ 个**约化[上同调群](@entry_id:142450) (reduced cohomology group)**，记作 $\tilde{H}^n(X; G)$，就是这个约化上[链复形](@entry_id:150246)的[上同调群](@entry_id:142450)。

### 与普通上同调的基本关系

约化上同调和普通[上同调](@entry_id:160558)之间存在一个直接而基本的关系。这个关系源于[链复形](@entry_id:150246)层面的一个短[正合序列](@entry_id:151503)。对于任何非空空间 $X$，[增广链复形](@entry_id:274443)可以分解为一个短[正合序列](@entry_id:151503)：
$$ 0 \to \tilde{C}_\bullet(X) \to C_\bullet(X) \xrightarrow{\varepsilon} \mathbb{Z} \to 0 $$
这里，$\tilde{C}_n(X) = C_n(X)$ 对于 $n \ge 1$，而 $\tilde{C}_0(X) = \ker(\varepsilon)$。由于 $X$ 非空，我们可以选择一个基点，并通过将 $\mathbb{Z}$ 中的 $1$ 映到该基点处的 $0$-单纯形来定义一个分裂映射 $\mathbb{Z} \to C_0(X)$。这个分裂使得上述序列在[链复形](@entry_id:150246)层面是可分裂的。

将 $\text{Hom}(-, \mathbb{Z})$ 函子应用于这个分裂的短[正合序列](@entry_id:151503)，我们得到一个上[链复形](@entry_id:150246)的[分裂短正合序列](@entry_id:159775)：
$$ 0 \to \text{Hom}(\mathbb{Z}, \mathbb{Z}) \to C^*(X; \mathbb{Z}) \to \tilde{C}^*(X; \mathbb{Z}) \to 0 $$
这个序列诱导了一个上同调的长正合序列。注意到复形 $\text{Hom}(\mathbb{Z}, \mathbb{Z})$ 仅在 $0$ 维非零，其值为 $\mathbb{Z}$，并且其[微分](@entry_id:158718)均为零。因此，它的[上同调群](@entry_id:142450)为 $H^0(\text{Hom}(\mathbb{Z}, \mathbb{Z})) \cong \mathbb{Z}$ 和 $H^n(\text{Hom}(\mathbb{Z}, \mathbb{Z})) = 0$ 对于 $n \ge 1$。

[长正合序列](@entry_id:153438)的形式如下：
$$ \dots \to H^n(\text{Hom}(\mathbb{Z}, \mathbb{Z})) \to H^n(X; \mathbb{Z}) \to \tilde{H}^n(X; \mathbb{Z}) \to H^{n+1}(\text{Hom}(\mathbb{Z}, \mathbb{Z})) \to \dots $$

对于 $n \ge 1$，序列中的 $H^n(\text{Hom}(\mathbb{Z}, \mathbb{Z}))$ 和 $H^{n+1}(\text{Hom}(\mathbb{Z}, \mathbb{Z}))$ 均为零。正合性立即告诉我们中间的映射是一个同构：
$$ H^n(X; \mathbb{Z}) \cong \tilde{H}^n(X; \mathbb{Z}) \quad \text{for } n \ge 1 $$

对于 $n=0$，长正合序列的一部分变为：
$$ 0 \to H^0(\text{Hom}(\mathbb{Z}, \mathbb{Z})) \to H^0(X; \mathbb{Z}) \to \tilde{H}^0(X; \mathbb{Z}) \to H^1(\text{Hom}(\mathbb{Z}, \mathbb{Z})) \to \dots $$
代入已知的上同调群，我们得到短[正合序列](@entry_id:151503)：
$$ 0 \to \mathbb{Z} \to H^0(X; \mathbb{Z}) \to \tilde{H}^0(X; \mathbb{Z}) \to 0 $$
由于这个序列是可分裂的（继承自[链复形](@entry_id:150246)的分裂），我们得到一个[直和分解](@entry_id:263004)：
$$ H^0(X; \mathbb{Z}) \cong \tilde{H}^0(X; \mathbb{Z}) \oplus \mathbb{Z} $$

总结一下，对于任何非空拓扑空间 $X$ 和整数系数，约化与非约化[上同调群](@entry_id:142450)的关系如下 [@problem_id:1668504]：
*   $H^n(X; \mathbb{Z}) \cong \tilde{H}^n(X; \mathbb{Z})$ for $n \ge 1$
*   $H^0(X; \mathbb{Z}) \cong \tilde{H}^0(X; \mathbb{Z}) \oplus \mathbb{Z}$

这个关系揭示了约化[上同调](@entry_id:160558)的本质：它仅仅在 $0$ 维对普通上同调进行了一次“约化”。

### $\tilde{H}^0$ 的几何意义

$0$ 维[上同调群](@entry_id:142450) $H^0(X; G)$ 有一个非常直观的几何解释：它与空间的[连通分支](@entry_id:141881)数密切相关。具体来说，$H^0(X; G)$ 同构于所有从 $X$ 到 $G$ 的局部常值函数的群。如果 $X$ 有 $k$ 个[路径连通分支](@entry_id:275432)，那么在每个分支上函数必须是常数，因此 $H^0(X; G)$ 同构于 $k$ 个 $G$ 的[直积](@entry_id:143046)，即 $G^k$。

利用我们刚刚建立的关系 $H^0(X; \mathbb{Z}) \cong \tilde{H}^0(X; \mathbb{Z}) \oplus \mathbb{Z}$，我们可以推导出 $\tilde{H}^0$ 的几何意义。如果 $X$ 有 $k$ 个[路径连通分支](@entry_id:275432)，则 $H^0(X; \mathbb{Z}) \cong \mathbb{Z}^k$。代入关系式，我们得到：
$$ \mathbb{Z}^k \cong \tilde{H}^0(X; \mathbb{Z}) \oplus \mathbb{Z} $$
这表明 $\tilde{H}^0(X; \mathbb{Z}) \cong \mathbb{Z}^{k-1}$ [@problem_id:1668483]。

这个结果有一个至关重要的推论：如果一个空间 $X$ 是[路径连通](@entry_id:148704)的（即 $k=1$），那么它的 $0$ 阶约化[上同调群](@entry_id:142450)是[平凡群](@entry_id:151996)，$\tilde{H}^0(X; G) = 0$，对于任何系数群 $G$ [@problem_id:1668514]。这正是我们引入约化上同调所期望的性质。单点空间是路径连通的，所以 $\tilde{H}^0(\ast; G)=0$。由于高维[上同调群](@entry_id:142450)在约化和非约化情况下是一致的，我们知道对于 $n \ge 1$，$H^n(\ast; G)=0$，因此 $\tilde{H}^n(\ast; G)=0$。这样，对于单点空间，所有的约化上同调群都是平凡的。

为了更具体地理解这一点，让我们考虑一个由两个离散点 $p$ 和 $q$ 组成的空间 $X = \{p, q\}$ [@problem_id:1668516]。这个空间有两个[路径连通分支](@entry_id:275432) ($k=2$)。它的 $0$ 阶普通[上同调群](@entry_id:142450)是 $H^0(X; \mathbb{Z}) \cong \mathbb{Z} \oplus \mathbb{Z}$。一个 $0$-上链 $\phi$ 由它在 $0$-单纯形 $\sigma_p$ 和 $\sigma_q$ 上的取值 $(\phi(\sigma_p), \phi(\sigma_q))$ 决定。由于空间是离散的，任何 $0$-上链都是一个 $0$-上循环。从 $H^0(X; \mathbb{Z})$ 到 $\tilde{H}^0(X; \mathbb{Z})$ 的[商映射](@entry_id:140877)，其本质是模掉了常值上链构成的[子群](@entry_id:146164)，即形如 $(m, m)$ 的元素。商群 $\frac{\mathbb{Z} \oplus \mathbb{Z}}{\{(m, m) \mid m \in \mathbb{Z}\}}$ 同构于 $\mathbb{Z}$。这个同构由映射 $(a, b) \mapsto a-b$ 给出。一个生成元是任何满足 $a-b = \pm 1$ 的[等价类](@entry_id:156032)。例如，由上链 $\phi$ 定义的配对 $(1, 0)$ 就是这样一个生成元。这个上链在点 $p$ 取值 $1$，在点 $q$ 取值 $0$，它不是常值的，因此在约化上同调群中代表一个非平凡的元素。

### [同伦不变性](@entry_id:150428)与[可缩空间](@entry_id:153541)

与普通[上同调](@entry_id:160558)一样，约化上同调也是一种**[同伦不变量](@entry_id:151920) (homotopy invariant)**。这意味着如果两个空间 $X$ 和 $Y$ 具有相同的[同伦型](@entry_id:148015)（即存在映射 $f: X \to Y$ 和 $g: Y \to X$ 使得 $g \circ f$ 和 $f \circ g$ 分别同伦于[恒等映射](@entry_id:634191)），那么它们的约化上同调群是同构的：$\tilde{H}^n(X; G) \cong \tilde{H}^n(Y; G)$ 对所有 $n \ge 0$ 成立。

这个性质有一个直接而强大的推论：对于任何非空**[可缩空间](@entry_id:153541) (contractible space)** $X$，其所有的约化上同调群都是平凡的。[可缩空间](@entry_id:153541)是指一个可以连续地“收缩”到一个点的空间，也就是说，它与单点空间具有相同的[同伦型](@entry_id:148015)。由于我们已经确立单点空间的所有约化[上同调群](@entry_id:142450)均为零，根据[同伦不变性](@entry_id:150428)，任何[可缩空间](@entry_id:153541)的约化[上同调群](@entry_id:142450)也必须全部为零。

$$ \tilde{H}^n(X; G) = 0 \quad \text{for all } n \ge 0 \text{ if } X \text{ is contractible.} $$

许多在拓扑学中常见的空间都是可缩的。例如，[欧几里得空间](@entry_id:138052) $\mathbb{R}^k$ 对于任何 $k \ge 1$ 都是可缩的 [@problem_id:1668473]。另一个重要的例子是任意空间 $X$ 上的**锥 (cone)**，记作 $CX$。它是通过取乘积 $X \times [0,1]$ 并将顶端 $X \times \{1\}$ 的所有点捏合成一个点而得到的空间。对于任何非空空间 $X$，其锥 $CX$ 总是可缩的 [@problem_id:1668510]。因此，我们立即可以断定，对于任何 $n \ge 0$ 和任何系数群 $G$，$\tilde{H}^n(CX; G) = 0$。这个看似简单的结果在建立[上同调理论](@entry_id:270863)中的一些核心定理时起着关键作用。

### 约化上同调在长正合序列中的威力

约化[上同调](@entry_id:160558)的真正优势在于它能够极大地简化某些重要定理的表述和应用，特别是那些涉及长正合序列的定理。

#### 悬挂同构

悬挂是拓扑学中一个基本的构造。一个[带基点的空间](@entry_id:273706) $X$ 的**悬挂 (suspension)** $SX$（有时也记作 $\Sigma X$）是通过取锥 $CX$ 并将其底部的 $X$（即 $X \times \{0\}$）也捏合成一个点得到的商空间，即 $SX = CX/X$。悬挂操作直观上将空间的维度提升了一。悬挂[同构定理](@entry_id:145702)精确地描述了这一过程在上同调层面的代数后果。

为了推导这个定理，我们考虑空间对 $(CX, X)$ 的约化[上同调长正合序列](@entry_id:266961) [@problem_id:1661656]：
$$ \dots \to \tilde{H}^k(CX) \to \tilde{H}^k(X) \xrightarrow{\delta} \tilde{H}^{k+1}(CX, X) \to \tilde{H}^{k+1}(CX) \to \dots $$
我们已经知道 $CX$ 是可缩的，所以对所有 $k$，$\tilde{H}^k(CX) = 0$。将这个信息代入长正合序列，我们发现序列中的许多项都消失了：
$$ \dots \to 0 \to \tilde{H}^k(X) \xrightarrow{\delta} \tilde{H}^{k+1}(CX, X) \to 0 \to \dots $$
正合性意味着[连接同态](@entry_id:160713) $\delta$ 是一个同构：
$$ \tilde{H}^k(X; G) \cong \tilde{H}^{k+1}(CX, X; G) $$
接下来，一个关于商空间上同调的基本结果（有时作为[切除定理](@entry_id:159397)的推论）告诉我们，对于“好的”空间对，$\tilde{H}^{k+1}(CX, X; G) \cong \tilde{H}^{k+1}(CX/X; G)$。结合 $SX = CX/X$ 的定义，我们得到了著名的**悬挂同构 (Suspension Isomorphism)**：
$$ \tilde{H}^k(X; G) \cong \tilde{H}^{k+1}(SX; G) \quad \text{for all } k \ge 0 $$
这个同构非常简洁明了，它直接关联了 $X$ 和其悬挂 $SX$ 的上同调群。如果使用普通上同调，这个定理的表述会因为 $0$ 维的特殊情况而变得复杂。

悬挂同构是一个强大的计算工具。例如，我们知道球面可以看作是低维球面的悬挂：$S^{n+1} \cong SS^n$。利用这一点和悬挂同构，我们可以归纳地计算出所有[球面的上同调](@entry_id:636700)群。另外，我们也可以将悬挂看作与 $S^1$ 的压扁积，即 $\Sigma X \cong X \wedge S^1$。假设我们知道 $S^2$ 的约化[上同调群](@entry_id:142450)为 $\tilde{H}^2(S^2; \mathbb{Z}) \cong \mathbb{Z}$ 且在其他维度为零。我们想计算 $S^2 \wedge S^1$ 的[上同调](@entry_id:160558)。根据悬挂同构 [@problem_id:1668460]：
$$ \tilde{H}^n(S^2 \wedge S^1; \mathbb{Z}) \cong \tilde{H}^{n-1}(S^2; \mathbb{Z}) $$
由于 $\tilde{H}^{n-1}(S^2; \mathbb{Z})$ 仅在 $n-1=2$（即 $n=3$）时非零且为 $\mathbb{Z}$，我们立即得出 $\tilde{H}^3(S^2 \wedge S^1; \mathbb{Z}) \cong \mathbb{Z}$，而其他维度的约化上同调群均为零。事实上，$S^2 \wedge S^1$ 同胚于 $S^3$，这个计算结果与 $S^3$ 的已知[上同调](@entry_id:160558)相符。

#### 商掉可缩[子空间](@entry_id:150286)

另一个展示约化上同调威力的例子是处理[商空间](@entry_id:274314)。假设在一个豪斯多夫空间 $X$ 中有一个非空、闭的可缩[子空间](@entry_id:150286) $A$。我们考虑[商映射](@entry_id:140877) $q: X \to X/A$，它将 $A$ 捏合成一个点。这个映射在约化上同调层面上会诱导怎样的变化呢？

我们可以利用与空间对 $(X,A)$ 相关的[上同调长正合序列](@entry_id:266961)，或者更直接地，考虑由包含 $A \hookrightarrow X$ 和[商映射](@entry_id:140877) $X \to X/A$ 构成的“上纤维序列”所诱导的长正合序列 [@problem_id:1668499]：
$$ \dots \to \tilde{H}^n(X/A; G) \xrightarrow{q^*} \tilde{H}^n(X; G) \to \tilde{H}^n(A; G) \to \tilde{H}^{n+1}(X/A; G) \to \dots $$
由于 $A$ 是可缩的，我们有 $\tilde{H}^k(A; G)=0$ 对于所有 $k$。将此代入序列，我们得到：
$$ \dots \to \tilde{H}^n(X/A; G) \xrightarrow{q^*} \tilde{H}^n(X; G) \to 0 \to \tilde{H}^{n+1}(X/A; G) \to \dots $$
正合性意味着映射 $q^*$ 的核和余核都为零，因此 $q^*$ 是一个同构。
$$ q^*: \tilde{H}^n(X/A; G) \cong \tilde{H}^n(X; G) \quad \text{for all } n \ge 0 $$
这个结论非常有用：在一个空间中“压掉”一个可缩的子部分，并不会改变其约化[上同调](@entry_id:160558)。这为我们提供了一种简化空间而不改变其核心代数[拓扑不变量](@entry_id:138526)的方法。

#### 长正合序列的计算应用

即使在不涉及[可缩空间](@entry_id:153541)的一般情况下，约化[上同调](@entry_id:160558)的[长正合序列](@entry_id:153438)也是一个精密的计算工具。通过它，我们可以揭示空间之间的映射所诱导的[代数结构](@entry_id:137052)。

考虑一个假设性的场景 [@problem_id:1668501]：我们有一个 CW-对 $(X, A)$，其中[子空间](@entry_id:150286) $A$ 同胚于圆周 $S^1$，而商空间 $X/A$ 同胚于球面 $S^2$。此外，我们知道空间 $X$ 的某些约化上同调群，例如 $\tilde{H}^1(X; \mathbb{Z}) = 0$ 和 $\tilde{H}^2(X; \mathbb{Z}) \cong \mathbb{Z}_7$。

我们可以写出上纤维序列 $A \to X \to X/A$ 对应的约化[上同调长正合序列](@entry_id:266961)的一部分：
$$ \dots \to \tilde{H}^1(X; \mathbb{Z}) \to \tilde{H}^1(A; \mathbb{Z}) \xrightarrow{\delta} \tilde{H}^2(X/A; \mathbb{Z}) \to \tilde{H}^2(X; \mathbb{Z}) \to \tilde{H}^2(A; \mathbb{Z}) \to \dots $$
现在我们代入已知的信息。我们知道 $\tilde{H}^1(S^1; \mathbb{Z}) \cong \mathbb{Z}$，$\tilde{H}^2(S^2; \mathbb{Z}) \cong \mathbb{Z}$，$\tilde{H}^2(S^1; \mathbb{Z}) = 0$。同时，题目给出了 $\tilde{H}^1(X; \mathbb{Z}) = 0$ 和 $\tilde{H}^2(X; \mathbb{Z}) \cong \mathbb{Z}_7$。代入序列得到：
$$ \dots \to 0 \to \mathbb{Z} \xrightarrow{\delta} \mathbb{Z} \to \mathbb{Z}_7 \to 0 \to \dots $$
现在我们可以利用正合性来分析这个序列。从 $\mathbb{Z} \to \mathbb{Z}_7$ 是满射，我们可以推断出其核是 $7\mathbb{Z}$。又因为序列在 $\mathbb{Z}$ (即 $\tilde{H}^2(X/A; \mathbb{Z})$) 处是正合的，所以[连接同态](@entry_id:160713) $\delta$ 的像必须等于后面映射的核。也就是说，$\text{im}(\delta) = \ker(\mathbb{Z} \to \mathbb{Z}_7) \cong 7\mathbb{Z}$。由于 $\delta$ 是一个从 $\mathbb{Z}$ 到 $\mathbb{Z}$ 的同态，它必然是乘以某个整数 $k$ 的形式。其像为 $k\mathbb{Z}$。因此，我们有 $k\mathbb{Z} = 7\mathbb{Z}$，这意味着 $|k|=7$。通过适当地选择生成元，我们可以假定 $k$ 是非负的，从而得到 $k=7$。

这个例子完美地展示了约化[上同调](@entry_id:160558)和长正合序列如何协同工作，将空间的拓扑信息（如一个空间如何“粘合”在另一个空间上）转化为关于[上同调群](@entry_id:142450)之间映射的精确代数信息。这正是代数拓扑学的核心思想和机制所在。