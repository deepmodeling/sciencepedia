## 引言
在代数拓扑学的宏伟蓝图中，[纤维化的长正合序列](@entry_id:161359)是连接空间几何形态与代数[不变量](@entry_id:148850)的核心桥梁之一。这一强大的工具使我们能够系统地研究和计算空间的[同伦群](@entry_id:159885)——一种捕捉空间高维“洞”的[代数结构](@entry_id:137052)。许多复杂的[拓扑空间](@entry_id:155056)虽然难以直接分析，但可以被分解为一个更简单的底空间和一个纤维，而[长正合序列](@entry_id:153438)恰恰揭示了这三者同伦群之间深刻而精确的代数关系。它解决了计算看似遥不可及的同伦群这一核心难题，为拓扑学研究提供了强有力的计算引擎。

本文将引导你深入探索这一基本工具。在“原理与机制”一章中，我们将详细阐述[长正合序列](@entry_id:153438)的构成、正合性的含义以及[连接同态](@entry_id:160713)的关键作用。接着，在“应用与跨学科联系”一章中，我们将通过Hopf[纤维化](@entry_id:203334)、[李群的拓扑](@entry_id:191016)结构以及[环路空间](@entry_id:160867)等一系列经典例子，展示该序列在几何学、物理学等领域的广泛应用。最后，通过“动手实践”部分，你将有机会亲自运用长正合序列解决具体问题，从而巩固和深化你的理解。

## 原理与机制

继上一章介绍纤维化的基本概念之后，本章将深入探讨其核心工具——同伦[长正合序列](@entry_id:153438)。我们将系统地阐述该序列的原理，揭示其内在机制，并通过一系列精心设计的例子展示它在计算同伦群和理解空间拓扑结构方面的强大威力。

### 基本工具：[同伦](@entry_id:139266)[长正合序列](@entry_id:153438)

对于任何一个以点为基的纤维化 $F \xrightarrow{i} E \xrightarrow{p} B$，其中 $F$ 是纤维， $E$ 是总空间， $B$ 是底空间，拓扑学中一个至关重要的定理断言，存在一个关联这些空间[同伦群](@entry_id:159885)的**[长正合序列](@entry_id:153438) (long exact sequence)**。这个序列构成了我们研究纤维化的代[数基](@entry_id:634389)石。

该序列的形式如下：
$$
\cdots \to \pi_n(F) \xrightarrow{i_*} \pi_n(E) \xrightarrow{p_*} \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(F) \to \cdots \to \pi_1(B) \xrightarrow{\partial_1} \pi_0(F)
$$
这里的映射定义如下：
*   $i_*: \pi_n(F) \to \pi_n(E)$ 是由纤维包含映射 $i: F \to E$ 诱导的[群同态](@entry_id:140603)。
*   $p_*: \pi_n(E) \to \pi_n(B)$ 是由[投影映射](@entry_id:153398) $p: E \to B$ 诱导的[群同态](@entry_id:140603)。
*   $\partial_n: \pi_n(B) \to \pi_{n-1}(F)$ 是一个新出现的、称为**[连接同态](@entry_id:160713) (connecting homomorphism)** 的映射。它以一种深刻的方式将底空间的[同伦](@entry_id:139266)与纤维的同伦联系起来，其构造依赖于纤维化所满足的[同伦提升性质](@entry_id:149641)。

“正合” (exact) 的概念是此序列的核心性质。一个序列在一个群（例如 $\pi_n(E)$）处是正合的，意味着从左侧进入该群的映射（$i_*$）的**像 (image)** 恰好等于从该群向右侧出去的映射（$p_*$）的**核 (kernel)**。即，在序列的每一步都满足 $\operatorname{im}(\text{in-map}) = \operatorname{ker}(\text{out-map})$。

正合性的一个直接且极为重要的推论是，序列中任意两个[连续映射](@entry_id:153855)的复合是平凡同态（即把所有元素都映到单位元）。例如，对于映射链 $\pi_n(F) \xrightarrow{i_*} \pi_n(E) \xrightarrow{p_*} \pi_n(B)$，我们有 $\operatorname{im}(i_*) \subseteq \operatorname{ker}(p_*)$。这直接导致了复合映射 $p_* \circ i_*$ 是平凡映射。我们可以从几何上直观地理解这一点：
*   **$p_* \circ i_* = 0$**: 该复合映射由几何上的复合 $p \circ i: F \to B$ 诱导。根据定义，纤维 $F$ 被包含映射 $i$ 映入总空间 $E$，而投影 $p$ 恰好将 $i(F)$ 中的所有点都映射到底空间的同一个基点 $b_0$ 上。因此，$p \circ i$ 是一个常值映射，它诱导的[同伦群](@entry_id:159885)同态必然是平凡的。
*   **$\partial_n \circ p_* = 0$**: 给定 $\pi_n(E)$ 中的一个元素，它由某个映射 $\alpha: S^n \to E$ 代表。$p_*$ 将其变为由 $p \circ \alpha$ 代表的 $\pi_n(B)$ 中的元素。[连接同态](@entry_id:160713) $\partial_n$ 的构造本质上是尝试将底空间中的球面“提升”回总空间。如果底空间中的球面本身就是从总空间投影下去的（如 $p \circ \alpha$），那么它已经有了一个自然的提升（即 $\alpha$ 本身）。在这种情况下，构造出的[边界映射](@entry_id:151165)（即 $\partial_n$ 的结果）是可缩的，即为 $\pi_{n-1}(F)$ 中的单位元。
*   **$i_* \circ \partial_n = 0$**: $\partial_n$ 的像是由提升过程产生的、位于纤维 $F$ 中的一个 $(n-1)$-球面。这个 $(n-1)$-球面在 $E$ 中是可缩的，因为它是在构造过程中作为一个 $n$-维圆盘在 $E$ 中的像的边界出现的。因此，当通过 $i_*$ 将其视为 $\pi_{n-1}(E)$ 的元素时，它代表的是单位元。

这些关系构成了利用[长正合序列](@entry_id:153438)进行代数推演的基础。

### 解读序列：性质与基本推论

#### 平凡[纤维化](@entry_id:203334)与[连接同态](@entry_id:160713)的角色

理解[连接同态](@entry_id:160713) $\partial$ 最好的方式，莫过于考察它在最简单情形下的行为。考虑一个**平凡纤维化 (trivial fibration)**，其总空间 $E$ 就是纤维 $F$ 和底空间 $B$ 的笛卡尔积 $F \times B$，投影 $p: F \times B \to B$ 就是到第二个分量的投影。

在这种情况下，存在一个**[截面](@entry_id:154995) (section)**，即一个[连续映射](@entry_id:153855) $s: B \to F \times B$，使得 $p \circ s = \operatorname{id}_B$（例如，可以取 $s(b) = (f_0, b)$，其中 $f_0$ 是纤维的基点）。这个[截面](@entry_id:154995)的存在对[长正合序列](@entry_id:153438)有决定性的影响。由[函子性](@entry_id:150069)，$p_* \circ s_* = (p \circ s)_* = (\operatorname{id}_B)_* = \operatorname{id}_{\pi_n(B)}$。这意味着 $p_*: \pi_n(F \times B) \to \pi_n(B)$ 对所有 $n \ge 1$ 都是满同态。

根据在 $\pi_n(B)$ 处的正合性，我们有 $\operatorname{ker}(\partial_n) = \operatorname{im}(p_*) = \pi_n(B)$。一个映射的核是其整个定义域，当且仅当这个映射是零映射。因此，对于平凡纤维化，所有[连接同态](@entry_id:160713) $\partial_n$ 都是零映射。

当 $\partial_n$ 为零时，[长正合序列](@entry_id:153438)在每一处都断裂开来，形成一系列短[正合序列](@entry_id:151503)：
$$
0 \to \pi_n(F) \xrightarrow{i_*} \pi_n(F \times B) \xrightarrow{p_*} \pi_n(B) \to 0
$$
[截面](@entry_id:154995) $s$ 诱导的映射 $s_*$ 提供了 $p_*$ 的一个[右逆](@entry_id:161498)，这意味着上述短[正合序列](@entry_id:151503)是**可裂的 (split)**。因此，我们得到了一个众所周知的结果：
$$
\pi_n(F \times B) \cong \pi_n(F) \oplus \pi_n(B)
$$
这个例子揭示了[连接同态](@entry_id:160713) $\partial$ 的本质：它衡量了纤维化相对于平凡积的“扭曲”程度。如果[纤维化](@entry_id:203334)是“直的”（平凡的），则 $\partial$ 为零；如果纤维是“扭着”安放在底空间之上的，$\partial$ 就会捕捉到这种扭曲的拓扑信息。

#### 同态之间的相互作用

正合性 $\operatorname{im}(i_*) = \operatorname{ker}(p_*)$ 如同一座桥梁，连接着关于 $i_*$ 和 $p_*$ 的信息。例如，假设在某个维度 $k$，我们知道 $p_*: \pi_k(E) \to \pi_k(B)$ 是[单射](@entry_id:183792)。根据[单射](@entry_id:183792)的定义，这意味着 $\operatorname{ker}(p_*) = \{0\}$，即其核只包含单位元。

将此信息代入正合性条件，我们得到 $\operatorname{im}(i_*) = \{0\}$。这意味着 $i_*: \pi_k(F) \to \pi_k(E)$ 的像空间是平凡的，换言之，$i_*$ 将 $\pi_k(F)$ 中的所有元素都映射到 $\pi_k(E)$ 的单位元。这正是平凡映射的定义。这个简单的推论展示了长正合序列如何将一个映射的性质转化为另一个映射的性质。

#### 低维末端与[单值性作用](@entry_id:154516)

[长正合序列](@entry_id:153438)在低维部分呈现出独特的几何意义。序列的末端通常写作：
$$
\cdots \to \pi_1(E) \xrightarrow{p_*} \pi_1(B) \xrightarrow{\partial_1} \pi_0(F) \to \pi_0(E) \to \pi_0(B) \to 0
$$
这里 $\pi_0(X)$ 表示空间 $X$ 的[路径连通分支](@entry_id:275432)的集合（这是一个带基点的集合，而非群）。[连接同态](@entry_id:160713) $\partial_1: \pi_1(B) \to \pi_0(F)$ 有一个优美的几何解释，称为**[单值性作用](@entry_id:154516) ([monodromy](@entry_id:174849) action)**。取 $\pi_1(B)$ 中一个由环路 $\gamma: [0,1] \to B$ 代表的元素。根据[同伦提升性质](@entry_id:149641)，我们可以将这个环路提升为总空间 $E$ 中的一条路径 $\tilde{\gamma}: [0,1] \to E$，其起点 $\tilde{\gamma}(0)$ 位于基点纤维 $F$ 中。由于 $\gamma$ 是一个环路（$\gamma(0)=\gamma(1)$），其提升路径的终点 $\tilde{\gamma}(1)$ 也必定位于纤维 $F$ 中。$\partial_1([\gamma])$ 的值就是终点 $\tilde{\gamma}(1)$ 所在的 $F$ 的[路径连通分支](@entry_id:275432)。

如果总空间 $E$ 和底空间 $B$ 都是[路径连通](@entry_id:148704)的（这在多数应用中都成立），那么 $\pi_0(E)$ 和 $\pi_0(B)$ 都只有一个元素。此时，序列在 $\pi_0(F)$ 处的正合性意味着 $\operatorname{im}(\partial_1) = \operatorname{ker}(\pi_0(F) \to \pi_0(E))$。由于 $\pi_0(E)$ 是单点集，从 $\pi_0(F)$ 出发的映射的核就是整个 $\pi_0(F)$。因此，$\operatorname{im}(\partial_1) = \pi_0(F)$，即 $\partial_1$ 是一个满射。这在直观上很有意义：如果纤维有多个[连通分支](@entry_id:141881)，我们应该能找到底空间中的某个环路，沿着它走一圈回到起点后，发现我们从纤维的一个分支“滑”到了另一个分支。

一个经典的例子是2-球面 $S^2$ 到实射影平面 $\mathbb{RP}^2$ 的万有覆叠映射 $p: S^2 \to \mathbb{RP}^2$。这是一个[纤维化](@entry_id:203334)，其纤维 $F$ 是离散的两点集（对径点）。$\pi_1(\mathbb{RP}^2) \cong \mathbb{Z}_2$ 的非平凡元代表了 $\mathbb{RP}^2$ 中一条不可缩的环路。将此环路从 $S^2$ 的一个点开始提升，最终会到达其对径点。这表明 $\partial_1$ 将 $\pi_1(\mathbb{RP}^2)$ 的非平凡元映到纤维的非基点分支，完美地诠释了[单值性作用](@entry_id:154516)。

### 连通性与同构

长正合序列最深刻的应用之一，是揭示当纤维或底空间具有较高连通性时，纤维化中空间的同伦群之间的同构关系。

#### 高连通纤维的影响

假设纤维 $F$ 是**$(k-1)$-连通的**（对于 $k \ge 1$），并且是[路径连通](@entry_id:148704)的。这意味着 $\pi_i(F) = 0$ 对所有 $1 \le i \le k-1$ 成立。考察[长正合序列](@entry_id:153438)的片段：
$$
\cdots \to \pi_i(F) \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to \pi_{i-1}(F) \to \cdots
$$
*   当 $1 \le i \le k-1$ 时，我们有 $\pi_i(F)=0$ 和 $\pi_{i-1}(F)=0$。序列变为 $0 \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to 0$。根据正合性，这意味着 $p_*$ 既是单射又是满射，即为一个同构。
*   当 $i=k$ 时，我们有 $\pi_{k-1}(F)=0$，但 $\pi_k(F)$ 不一定为零。序列变为 $\cdots \to \pi_k(E) \xrightarrow{p_*} \pi_k(B) \to 0$。正合性保证了 $p_*$ 是一个满射。

综上，我们得到一个重要的定理：
**定理**：若在一个[纤维化](@entry_id:203334) $F \to E \to B$ 中，纤维 $F$ 是[路径连通](@entry_id:148704)且 $(k-1)$-连通的，则投影诱导的同态 $p_*: \pi_i(E) \to \pi_i(B)$ 对于 $i \le k-1$ 是同构，对于 $i=k$ 是满射。

此定理的一个关键应用是计算空间的同伦群。例如，对于一个连通的[CW复形](@entry_id:150589) $X$，其万有覆叠空间 $\tilde{X}$ 构成了纤维化 $\tilde{X} \to X$，纤维是离散群 $\pi_1(X, x_0)$。对于 $i \ge 2$，纤维的同伦群 $\pi_{i-1}(F)$ 均为零。应用上述定理的变体（对于非连通纤维需直接分析序列），我们得到 $p_*: \pi_i(\tilde{X}) \to \pi_i(X)$ 对所有 $i \ge 2$ 都是同构。这说明一个空间的[高阶同伦群](@entry_id:159688)与其万有[覆叠空间](@entry_id:152318)相同，这是一个深刻的结果。

#### 高连通底空间的影响

与上述情况对偶，我们也可以考察底空间高度连通时的情形。假设底空间 $B$ 是 $k$-连通的，即 $\pi_i(B)=0$ 对所有 $1 \le i \le k$ 成立。考察序列片段：
$$
\cdots \to \pi_i(B) \to \pi_{i-1}(F) \xrightarrow{i_*} \pi_{i-1}(E) \to \pi_{i-1}(B) \to \cdots
$$
通过类似的分析，我们可以得到如下的[对偶定理](@entry_id:137804)：
**定理**：若在一个[纤维化](@entry_id:203334) $F \to E \to B$ 中，底空间 $B$ 是[路径连通](@entry_id:148704)且 $k$-连通的，则包含映射诱导的同态 $i_*: \pi_i(F) \to \pi_i(E)$ 对于 $i \le k-1$ 是同构，对于 $i=k$ 是满射。

这个结果在拓扑学的构造性方法（如Postnikov塔和Eilenberg-MacLane空间理论）中扮演着核心角色，它允许我们通过[纤维化](@entry_id:203334)将一个空间的同伦群“拼接”到另一个空间上。

### 典型应用与计算

现在，我们将展示[长正合序列](@entry_id:153438)作为一个强大的计算引擎，如何被用于解决具体问题。

#### [路径空间纤维化](@entry_id:161224)与[环路空间](@entry_id:160867)

对任何带基点的[路径连通空间](@entry_id:152443) $(B, b_0)$，我们可以构造一个称为**[路径空间纤维化](@entry_id:161224) (path space fibration)** 的重要例子。其总空间 $PB$ 是 $B$ 中所有始于 $b_0$ 的路径构成的空间。投影 $p: PB \to B$ 将每条路径映射到其终点 $p(\gamma) = \gamma(1)$。这个映射是一个[纤维化](@entry_id:203334)，其在基点 $b_0$ 上的纤维恰好是所有始于并终于 $b_0$ 的路径，即**[环路空间](@entry_id:160867) (loop space)** $\Omega B$。

这个[纤维化](@entry_id:203334)有一个神奇的性质：总空间 $PB$ 是**可缩的 (contractible)**，这意味着它的所有[同伦群](@entry_id:159885)均为零，即 $\pi_n(PB) = 0$ 对所有 $n \ge 0$ 成立。将此信息代入[长正合序列](@entry_id:153438)：
$$
\cdots \to \pi_n(PB) \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to \pi_{n-1}(PB) \to \cdots
$$
由于 $\pi_n(PB)$ 和 $\pi_{n-1}(PB)$ 都是零群，序列简化为：
$$
0 \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to 0
$$
正合性立即告诉我们，[连接同态](@entry_id:160713) $\partial_n$ 是一个同构：
$$
\pi_n(B) \cong \pi_{n-1}(\Omega B) \quad (\text{for } n \ge 1)
$$
这个同构关系是代数拓扑中的基石之一。它将计算一个空间的[高阶同伦群](@entry_id:159688)问题，转化为计算其[环路空间](@entry_id:160867)的低一阶同伦群问题。更深一步的分析表明，这个同构非常自然：代表 $\pi_n(B)$ 中元素的映射 $\alpha: I^n \to B$ 与代表 $\pi_{n-1}(\Omega B)$ 中对应元素的映射 $\beta: I^{n-1} \to \Omega B$ 之间，通过伴随关系 $\alpha(v,s) = (\beta(v))(s)$ 直接关联。

通过迭代此关系，我们能进行奇妙的计算。例如，$\pi_k(\Omega^2 B) = \pi_k(\Omega(\Omega B)) \cong \pi_{k+1}(\Omega B) \cong \pi_{k+2}(B)$。如果我们想知道3-球面的二次[环路空间](@entry_id:160867)的一阶同伦群，$\pi_1(\Omega^2 S^3)$，我们可以立即得到 $\pi_1(\Omega^2 S^3) \cong \pi_3(S^3)$。由于已知 $\pi_3(S^3) \cong \mathbb{Z}$，我们便算出了一个看似复杂的空间的同伦群。

#### 计算同伦群：[扩张问题](@entry_id:150521)

在更一般的情况下，长正合序列将一个空间的[同伦群](@entry_id:159885)的计算问题，转化为一个代数上的**[群扩张问题](@entry_id:145893) (group extension problem)**。对于序列的每一部分，我们都可以抽取出一个短[正合序列](@entry_id:151503)。具体来说，对于 $\pi_n(E)$，我们有短[正合序列](@entry_id:151503)：
$$
0 \to \operatorname{Coker}(\partial_{n+1}) \to \pi_n(E) \to \operatorname{ker}(\partial_n) \to 0
$$
这里 $\operatorname{Coker}(\partial_{n+1}) = \pi_n(F) / \operatorname{im}(\partial_{n+1})$ 是 $\partial_{n+1}$ 的余核，而 $\operatorname{ker}(\partial_n)$ 是 $\partial_n$ 的核。由正合性，$\operatorname{Coker}(\partial_{n+1}) \cong \operatorname{im}(i_*)$，$\operatorname{ker}(\partial_n) = \operatorname{im}(p_*)$。这个短[正合序列](@entry_id:151503)告诉我们，$\pi_n(E)$ 是由 $\pi_n(B)$ 的一个[子群](@entry_id:146164)（$\operatorname{im}(p_*)$）通过 $\pi_n(F)$ 的一个[商群](@entry_id:145113)（$\operatorname{im}(i_*)$）扩张而成的。

让我们通过一个具体的例子来看这个机制如何运作。考虑Stiefel[流形](@entry_id:153038) $V_2(\mathbb{R}^5)$（$\mathbb{R}^5$ 中的标准正交2-标架空间），它构成一个[纤维化](@entry_id:203334) $S^3 \to V_2(\mathbb{R}^5) \to S^4$。我们希望计算 $\pi_3(V_2(\mathbb{R}^5))$。相关的[长正合序列](@entry_id:153438)片段是：
$$
\pi_4(S^4) \xrightarrow{\partial_4} \pi_3(S^3) \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \xrightarrow{p_*} \pi_3(S^4)
$$
我们知道 $\pi_4(S^4) \cong \mathbb{Z}$，$\pi_3(S^3) \cong \mathbb{Z}$，$\pi_3(S^4) = 0$。此外，可以证明[连接同态](@entry_id:160713) $\partial_4: \mathbb{Z} \to \mathbb{Z}$ 是乘以2的映射。代入这些信息：
$$
\mathbb{Z} \xrightarrow{\times 2} \mathbb{Z} \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \to 0
$$
*   在 $\pi_3(V_2(\mathbb{R}^5))$ 处正合，意味着 $\operatorname{im}(i_*) = \operatorname{ker}(p_*)$。由于 $p_*$ 的目标是零群，它的核就是整个定义域，即 $\operatorname{im}(i_*) = \pi_3(V_2(\mathbb{R}^5))$。因此 $i_*$ 是满射。
*   在 $\pi_3(S^3)$ 处正合，意味着 $\operatorname{ker}(i_*) = \operatorname{im}(\partial_4)$。我们已知 $\partial_4$ 是乘以2，所以其像是 $2\mathbb{Z}$。
*   根据[第一同构定理](@entry_id:146795)，$\operatorname{im}(i_*) \cong \pi_3(S^3) / \operatorname{ker}(i_*)$。

结合以上三点，我们得到：
$$
\pi_3(V_2(\mathbb{R}^5)) \cong \mathbb{Z} / 2\mathbb{Z} \cong \mathbb{Z}_2
$$
我们就这样精确地计算出了一个非平凡的同伦群。

在某些情况下，外部信息（例如，[连接同态](@entry_id:160713)被证明是零映射）可以极大地简化计算。例如，在纤维化 $S^3 \to V_2(\mathbb{C}^3) \to S^5$ 中，如果我们知道 $\partial_5: \pi_5(S^5) \to \pi_4(S^3)$ 是零映射，那么在 $\pi_4(S^3)$ 处的正合性 $\operatorname{ker}(i_*) = \operatorname{im}(\partial_5) = 0$ 就意味着 $i_*: \pi_4(S^3) \to \pi_4(V_2(\mathbb{C}^3))$ 是[单射](@entry_id:183792)。结合其他信息，这可以帮助我们确定 $\pi_4(V_2(\mathbb{C}^3))$。

本章通过阐述同伦[长正合序列](@entry_id:153438)的原理、性质和一系列应用，展示了它作为联系空间拓扑与[代数结构](@entry_id:137052)的核心桥梁所扮演的关键角色。掌握[长正合序列](@entry_id:153438)是深入学习代数拓扑的必经之路。