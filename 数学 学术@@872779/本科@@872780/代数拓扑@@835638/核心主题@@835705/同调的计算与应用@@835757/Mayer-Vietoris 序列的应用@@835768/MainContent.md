## 引言
在[代数拓扑学](@entry_id:138192)的广阔领域中，同调群扮演着基石的角色。它们是将拓扑空间的几何形态转化为代数[不变量](@entry_id:148850)的有力工具，揭示了空间的“洞”和连通性等深层结构。然而，对于许多复杂的空间而言，直接从定义出发计算其同调群是一项极其繁琐甚至不可能完成的任务。这一挑战催生了对更高效、更具系统性计算方法的需求，即一种能够将复杂问题分解为可管理部分的策略。

本文聚焦于解决这一核心问题的强大技术：迈尔-维托里斯序列。它提供了一种优雅的“分而治之”的代数框架，允许我们将一个难以处理的[空间分解](@entry_id:755142)为两个相对简单的[子空间](@entry_id:150286)，并通过一个精巧的长正合序列，将这些[子空间](@entry_id:150286)及其交集的同调信息联系起来，从而推导出原始空间的同调群。

在接下来的内容中，我们将踏上一段从理论到实践的探索之旅。在“原理与机制”一章中，我们将深入剖析迈尔-维托里斯序列的构造、其中各个映射的几何意义，以及它与[切除定理](@entry_id:159397)的深刻联系。随后，在“应用与交叉学科联系”一章，我们将见证该序列在实际计算中的威力，从计算球面、环面等基本空间的同调，到分析由粘合构造出的[克莱因瓶](@entry_id:149661)和[透镜空间](@entry_id:274705)，再到其在纽结理论和[微分几何](@entry_id:145818)等交叉学科中的应用。最后，“动手实践”部分将为您提供亲手应用这些知识解决具体问题的机会，从而真正巩固您的理解。通过本次学习，您将不仅掌握一个计算工具，更将获得一种洞察拓扑结构本质的代数思维方式。

## 原理与机制

在代数拓扑中，一个核心任务是计算[拓扑空间](@entry_id:155056)的同调群，这些代数[不变量](@entry_id:148850)揭示了空间的内在连通性结构。对于复杂的空间，直接从奇异[链复形](@entry_id:150246)的定义出发进行计算往往是极其困难的。迈尔-维托里斯序列（Mayer-Vietoris sequence）提供了一种强大的“分而治之”的策略，它允许我们将一个复杂的[空间分解](@entry_id:755142)为若干个更简单的、其同调群已知的[子空间](@entry_id:150286)，然后通过一个长正合序列将这些[子空间](@entry_id:150286)的同调信息重新组合，从而推导出原空间的同调群。本章将深入探讨迈尔-维托里斯序列的原理、机制及其在各种情境下的应用。

### 迈尔-维托里斯序列：表述与直观理解

迈尔-维托里斯序列是联系一个空间 $X$ 的同调群与其两个[子空间](@entry_id:150286) $A$ 和 $B$ （$X = A \cup B$）及其交集 $A \cap B$ 的同调群的代数工具。为了序列能够最直接地应用，我们通常要求 $A$ 和 $B$ 是 $X$ 的开[子集](@entry_id:261956)。更一般地，该序列也适用于 $A$ 和 $B$ 是 $X$ 的[任意子](@entry_id:143753)空间，只要它们的内部覆盖了 $X$（即 $\operatorname{int}(A) \cup \operatorname{int}(B) = X$）。

**迈尔-维托[里斯定理](@entry_id:147851)**：设 $X$ 是一个拓扑空间，且 $X=A \cup B$ 是两个[子空间](@entry_id:150286) $A, B$ 的并。存在一个关于同调群（以某个[阿贝尔群](@entry_id:150284) $G$ 为系数，通常为 $\mathbb{Z}$）的[长正合序列](@entry_id:153438)：
$$
\cdots \to H_n(A \cap B) \xrightarrow{j_*} H_n(A) \oplus H_n(B) \xrightarrow{k_*} H_n(X) \xrightarrow{\partial_*} H_{n-1}(A \cap B) \to \cdots
$$
$$
\cdots \to H_1(X) \xrightarrow{\partial_*} H_0(A \cap B) \xrightarrow{j_*} H_0(A) \oplus H_0(B) \xrightarrow{k_*} H_0(X) \to 0
$$

这个序列中的映射具有清晰的几何意义：

1.  **映射 $j_*$**：这个映射由包含映射 $i_A: A \cap B \hookrightarrow A$ 和 $i_B: A \cap B \hookrightarrow B$ 导出。具体而言，$j_*$ 定义为 $j_*(\alpha) = (i_{A*}(\alpha), -i_{B*}(\alpha))$。这是代数拓扑中的一个标准约定，尽管存在其他符号约定。对于一个在交集 $A \cap B$ 中的 $n$-闭链 $\alpha$， $j_*$ 将其同调类 $[\alpha]$ 映射到由它在 $A$ 中和在 $B$ 中所代表的两个同调类组成的对，其中第二个分量带负号。

2.  **映射 $k_*$**：这个映射由包含映射 $j_A: A \hookrightarrow X$ 和 $j_B: B \hookrightarrow X$ 导出，定义为 $k_*([\alpha], [\beta]) = j_{A*}([\alpha]) + j_{B*}([\beta])$。它将来自 $A$ 和 $B$ 的同调类相加，得到 $X$ 中的一个同调类。直观上，这是将 $A$ 和 $B$ 中的“洞”合并到 $X$ 中。

3.  **[连接同态](@entry_id:160713) $\partial_*$**：这是序列中最关键也最不平凡的部分。一个 $X$ 中的 $n$-闭链 $c$ 的同调类 $[c]$ 被 $k_*$ 映射为零当且仅当 $[c]$ 是一个来自 $A$ 的类和一个来自 $B$ 的类的和。而[连接同态](@entry_id:160713) $\partial_*$ 则处理那些不能被简单地看作 $A$ 中或 $B$ 中闭链之和的 $X$ 的闭链。一个 $X$ 中的 $n$-闭链 $c$ 可以被写成 $a+b$，其中 $a$ 是 $A$ 中的链， $b$ 是 $B$ 中的链。由于 $\partial(c) = \partial a + \partial b = 0$，我们有 $\partial a = -\partial b$。这个链 $\partial a$ 的支撑集必然位于 $A \cap B$ 内，并且它本身是一个 $(n-1)$-闭链。[连接同态](@entry_id:160713) $\partial_*$ 就将 $X$ 中的同调类 $[c]$ 映射到这个在“接缝” $A \cap B$ 上定义的 $(n-1)$-同调类 $[\partial a]$。

迈尔-维托里斯序列的构建在根本上依赖于 **[切除定理](@entry_id:159397) (Excision Theorem)**。在推导过程中，一个关键步骤是证明[相对同调群](@entry_id:159711)之间的同构 $H_n(X, B) \cong H_n(A, A \cap B)$。这个同构正是通过切除 $X$ 中的一个[子集](@entry_id:261956) $U = X \setminus A$ 来实现的。根据[切除定理](@entry_id:159397)，若 $\overline{U} \subset \operatorname{int}(B)$，则包含映射 $(A, A \cap B) = (X \setminus U, B \setminus U) \hookrightarrow (X, B)$ 将诱导同调群的同构 [@problem_id:1681009]。这个步骤是连接代数（[链复形](@entry_id:150246)的代数性质）与几何（空间的分解）的桥梁，构成了迈尔-维托里斯序列的核心机制。

### 最简单的情形：可缩的交集

迈尔-维托里斯序列最富有成效的应用场景之一是当交集 $A \cap B$ 在同调上是平凡的时候。具体来说，如果 $A \cap B$ 是道路连通的 ($H_0(A \cap B) \cong \mathbb{Z}$) 并且对于所有 $n \ge 1$ 都有 $H_n(A \cap B) = 0$（例如，如果 $A \cap B$ 是可缩的），那么长正合序列会大大简化。

在这种情况下，对于 $n \ge 2$，序列的一部分变为：
$$
\cdots \to H_n(A \cap B) \to H_n(A) \oplus H_n(B) \to H_n(X) \to H_{n-1}(A \cap B) \to \cdots
$$
$$
\cdots \to 0 \to H_n(A) \oplus H_n(B) \xrightarrow{k_*} H_n(X) \xrightarrow{\partial_*} 0 \to \cdots
$$
根据[正合序列](@entry_id:151503)的性质，这意味着映射 $k_*: H_n(A) \oplus H_n(B) \to H_n(X)$ 是一个同构。对于 $n=1$ 的情形，我们得到短[正合序列](@entry_id:151503)：
$$
0 \to H_1(A) \oplus H_1(B) \to H_1(X) \to H_0(A \cap B) \to H_0(A) \oplus H_0(B) \to H_0(X) \to 0
$$
如果 $A$ 和 $B$ 都是道路连通的，那么 $H_0(A) \cong \mathbb{Z}$, $H_0(B) \cong \mathbb{Z}$，并且 $H_0(X) \cong \mathbb{Z}$。此时 $H_0(A \cap B) \to H_0(A) \oplus H_0(B)$ 是单射，因此 $H_1(X)$ 到 $H_0(A \cap B)$ 的映射是零映射。这同样导出了 $H_1(X) \cong H_1(A) \oplus H_1(B)$。

这个原理在计算[楔和](@entry_id:270607) (wedge sum) 的同调群时特别有用。对于两个带基点的“行为良好”的空间 $(A, a_0)$ 和 $(B, b_0)$，它们的[楔和](@entry_id:270607) $X = A \vee B$ 可以通过选择合适的开集 $U$ 和 $V$ 来进行分析，使得它们的交集是可缩的。一个标准的构造是取 $U$ 为 $A$ 在 $X$ 中的一个[开邻域](@entry_id:268496)，它可以[形变收缩](@entry_id:148036)到 $A$，取 $V$ 为 $B$ 的一个类似[开邻域](@entry_id:268496)，并使得 $U \cap V$ 是基点的一个可缩开邻域 [@problem_id:1687807]。在这种情况下，通过[同伦不变性](@entry_id:150428)，$H_*(U) \cong H_*(A)$，$H_*(V) \cong H_*(B)$，且对于 $n \ge 1$，$H_n(U \cap V) = 0$。于是，对于[约化同调](@entry_id:274187)群 $\tilde{H}_n$，我们得到一个非常简洁的结果：
$$
\tilde{H}_n(A \vee B) \cong \tilde{H}_n(A) \oplus \tilde{H}_n(B) \quad \text{for all } n \ge 0.
$$

让我们用一个具体的例子来说明这一点：计算两个圆的[楔和](@entry_id:270607) $X = S^1 \vee S^1$ 的同调群 [@problem_id:1680233]。我们可以将 $X$ 想象为在原点处相切的两个圆。为了应用迈尔-维托里斯序列，我们需要明智地选择开集 $U$ 和 $V$。最佳策略是让 $U$ 成为其中一个圆（比如 $C_1$）的[开邻域](@entry_id:268496)，它包含 $C_1$ 以及 $C_2$ 在[切点](@entry_id:172885)附近的一小段开弧。类似地，让 $V$ 成为 $C_2$ 的一个开邻域。通过这种方式， $U$ 可以[形变收缩](@entry_id:148036)到 $C_1$，$V$ 可以[形变收缩](@entry_id:148036)到 $C_2$，而它们的交集 $U \cap V$ 是围绕[切点](@entry_id:172885)的一个小的“X”形区域，它是可缩的。

-   $H_n(U) \cong H_n(S^1)$，所以 $H_1(U) \cong \mathbb{Z}$，$H_0(U) \cong \mathbb{Z}$。
-   $H_n(V) \cong H_n(S^1)$，所以 $H_1(V) \cong \mathbb{Z}$，$H_0(V) \cong \mathbb{Z}$。
-   $U \cap V$ 是可缩的，所以 $H_n(U \cap V)=0$ 对所有 $n \ge 1$ 成立，$H_0(U \cap V) \cong \mathbb{Z}$。

将这些代入迈尔-维托里斯序列中关于 $H_1$ 的部分：
$$
H_1(U \cap V) \to H_1(U) \oplus H_1(V) \to H_1(X) \to H_0(U \cap V) \to \cdots
$$
即
$$
0 \to \mathbb{Z} \oplus \mathbb{Z} \to H_1(X) \to \mathbb{Z} \to \cdots
$$
如前所述，由于 $U,V,X$ 都是道路连通的，从 $H_1(X)$ 到 $H_0(U \cap V)$ 的映射是零映射。因此，我们立即得到 $H_1(S^1 \vee S^1) \cong \mathbb{Z} \oplus \mathbb{Z}$。这个结果直观地告诉我们，$S^1 \vee S^1$ 有两个独立的一维“洞”。

### 非平凡交集的应用

当交集 $A \cap B$ 本身具有非平凡的拓扑结构时，迈尔-维托里斯序列的威力就更加凸显出来。此时，长正合序列不会断裂成简单的直和，我们需要分析其中各个映射来提取信息。

#### 道路连通的交集

一个经典的例子是[克莱因瓶](@entry_id:149661) $K$ 的同调计算。[克莱因瓶](@entry_id:149661)可以看作是由两个[莫比乌斯带](@entry_id:152389) $M_A$ 和 $M_B$ 沿着它们共同的边界圆粘合而成。我们可以构造开集 $A$ 和 $B$ 分别[形变收缩](@entry_id:148036)到 $M_A$ 和 $M_B$，它们的交集 $A \cap B$ 则[形变收缩](@entry_id:148036)到这个边界圆，因此 $A \cap B \simeq S^1$。

我们知道莫比乌斯带的中心圆是其一阶同调群 $\mathbb{Z}$ 的生成元。设 $\alpha$ 和 $\beta$ 分别是 $H_1(A)$ 和 $H_1(B)$ 的生成元（对应于两个莫比乌斯带的中心圆），$\gamma$ 是 $H_1(A \cap B)$ 的生成元（对应于边界圆）。关键在于理解映射 $j_*: H_1(A \cap B) \to H_1(A) \oplus H_1(B)$ [@problem_id:1632636]。在[莫比乌斯带](@entry_id:152389)中，边界圆会环绕中心圆两周。因此，边界圆的同调类是中心圆同调类的2倍（或-2倍，取决于定向）。设 $i_{A*}: H_1(A \cap B) \to H_1(A)$ 和 $i_{B*}: H_1(A \cap B) \to H_1(B)$ 是由包含映射诱导的同态。假设我们选择的定向使得 $i_{A*}(\gamma) = 2\alpha$ 且 $i_{B*}(\gamma) = 2\beta$。根据我们选定的 $j_*$ 定义，$j_*(\gamma) = (i_{A*}(\gamma), -i_{B*}(\gamma)) = (2\alpha, -2\beta)$。用矩阵表示，这个映射由 $\begin{pmatrix} 2 \\ -2 \end{pmatrix}$ 给出。

现在来看迈尔-维托里斯序列：
$$
\cdots \to H_1(A \cap B) \xrightarrow{j_*} H_1(A) \oplus H_1(B) \xrightarrow{k_*} H_1(K) \to H_0(A \cap B) \to \cdots
$$
$$
\cdots \to \mathbb{Z} \xrightarrow{\begin{pmatrix} 2 \\ -2 \end{pmatrix}} \mathbb{Z} \oplus \mathbb{Z} \to H_1(K) \to \mathbb{Z} \to \cdots
$$
根据正合性，$H_1(K)$ 同构于 $k_*$ 的像，而 $\operatorname{Im}(k_*) = \ker(H_1(K) \to H_0(A \cap B))$。同时，$\operatorname{Im}(k_*) \cong (H_1(A) \oplus H_1(B)) / \operatorname{Im}(j_*)$。[商群](@entry_id:145113) $(\mathbb{Z} \oplus \mathbb{Z}) / \operatorname{Im}(j_*)$ 是 $(\mathbb{Z} \oplus \mathbb{Z}) / \langle(2,-2)\rangle \cong \mathbb{Z} \oplus \mathbb{Z}_2$。因此，$H_1(K) \cong \mathbb{Z} \oplus \mathbb{Z}_2$。

[正合序列](@entry_id:151503)的刚性结构意味着，如果我们知道序列中一个映射的性质，就能推断出其他部分的信息。例如，在一个假设的分解 $X=A \cup B$ 中，若 $A \simeq S^1$, $B \simeq S^1$, $A \cap B \simeq T^2$（2-维环面），且已知映射 $j_*: H_1(A \cap B) \to H_1(A) \oplus H_1(B)$ 是一个同构，我们可以利用序列来计算 $H_2(X)$ [@problem_id:1632664]。序列的相关部分为：
$$
H_2(A) \oplus H_2(B) \to H_2(X) \xrightarrow{\partial_*} H_1(A \cap B) \xrightarrow{j_*} H_1(A) \oplus H_1(B)
$$
由于 $A, B \simeq S^1$, $H_2(A)=H_2(B)=0$。序列变为 $0 \to H_2(X) \xrightarrow{\partial_*} H_1(A \cap B) \xrightarrow{j_*} \cdots$。正合性要求 $\operatorname{Im}(\partial_*) = \ker(j_*)$。既然 $j_*$ 是同构，它的核是平凡的，即 $\ker(j_*) = 0$。因此 $\operatorname{Im}(\partial_*) = 0$。同时，从 $0 \to H_2(X)$ 可知 $\partial_*$ 是单射。一个既是单射又具有平凡像的映射，其定义域必然是零群。因此，$H_2(X)=0$。

#### 非道路连通的交集

当交集 $A \cap B$ 不是道路连通时，迈尔-维托里斯序列在低维处会展现出有趣的现象。考虑一个空间 $X = A \cup B$，其中 $A$ 和 $B$ 都是可缩的（例如开圆盘），但它们的交集 $A \cap B$ 由两个不相交的可缩区域 $C_1$ 和 $C_2$ 组成 [@problem_id:1669771]。

在这种情况下：
-   $H_n(A)=0$ 和 $H_n(B)=0$ 对所有 $n \ge 1$ 成立。$H_0(A) \cong \mathbb{Z}, H_0(B) \cong \mathbb{Z}$。
-   $A \cap B = C_1 \sqcup C_2$，所以 $H_0(A \cap B) \cong \mathbb{Z} \oplus \mathbb{Z}$，且 $H_n(A \cap B) = 0$ 对所有 $n \ge 1$ 成立。

考察序列的末端：
$$
H_1(A) \oplus H_1(B) \to H_1(X) \xrightarrow{\partial_*} H_0(A \cap B) \xrightarrow{j_*} H_0(A) \oplus H_0(B) \to H_0(X) \to 0
$$
代入已知的同调群：
$$
0 \oplus 0 \to H_1(X) \xrightarrow{\partial_*} \mathbb{Z} \oplus \mathbb{Z} \xrightarrow{j_*} \mathbb{Z} \oplus \mathbb{Z} \to \mathbb{Z} \to 0
$$
正合性告诉我们 $\partial_*$ 是一个[单射](@entry_id:183792)，且其像等于 $j_*$ 的核。$j_*$ 映射 $H_0(A \cap B)$ 的两个生成元（分别对应 $C_1$ 和 $C_2$）到它们在 $A$ 和 $B$ 中的同调类。由于 $A$ 和 $B$ 都是道路连通的， $j_*$ 将 $(1,0)$ 映为 $(1,-1)$，将 $(0,1)$ 也映为 $(1,-1)$（在某个基底下，取决于$C_1,C_2$如何嵌入）。一个更标准的处理方式是：设 $H_0(C_1)$ 的生成元是 $g_1$, $H_0(C_2)$ 的生成元是 $g_2$。$j_*(g_1) = (i_{A*}(g_1), -i_{B*}(g_1))$. 在$H_0(A)\oplus H_0(B)$中，这对应于 $(1,-1)$。同理$j_*(g_2)$也对应于$(1,-1)$。所以 $j_*(m,n)=(m+n, -(m+n))$。这个映射的核是所有满足 $m+n=0$ 的整数组 $(m,n)$，即形如 $(m, -m)$ 的元素。这个核同构于 $\mathbb{Z}$，由 $(1,-1)$ 生成。
因此，我们得到 $H_1(X) \cong \operatorname{Im}(\partial_*) = \ker(j_*) \cong \mathbb{Z}$。

这个结果有一个漂亮的几何解释：虽然 $A$ 和 $B$ 都没有洞，但它们的组合方式创造了一个洞。$H_1(X)$ 的生成元可以由这样一条路径代表：从交集的一个分量 $C_1$ 出发，通过 $A$ 内部的一条路径到达另一个分量 $C_2$，然后再通过 $B$ 内部的一条路径返回到 $C_1$。这条闭合路径无法在 $X$ 中收缩为一点，因为它环绕了由 $A$ 和 $B$ 的“非相交”部分所形成的“洞”。这个例子有力地说明了同调群不仅依赖于空间的局部性质，还深刻地依赖于各个部分是如何粘合在一起的。

### 系数域的角色

同调群的定义可以推广到使用任意[阿贝尔群](@entry_id:150284) $G$作为系数，记为 $H_n(X; G)$。迈尔-维托里斯序列对于任何系数群都成立。改变系数群有时能极大地简化计算，特别是当使用有理数 $\mathbb{Q}$ 这样的域作为系数时。

当系数群 $G$ 是一个域（如 $\mathbb{Q}$ 或 $\mathbb{Z}_p$），$H_n(X; G)$ 成为 $G$ 上的一个[向量空间](@entry_id:151108)。一个重要的推论是，如果使用特征为零的域（如 $\mathbb{Q}$）作为系数，所有关于整数同调群 $H_n(X; \mathbb{Z})$ 的挠扑信息都会丢失。例如，如果 $H_n(X; \mathbb{Z}) \cong \mathbb{Z}_2$，那么 $H_n(X; \mathbb{Q})=0$，因为在 $\mathbb{Q}$-[向量空间](@entry_id:151108)中不存在2-[挠元](@entry_id:148301)。

让我们通过计算实射影三维空间 $\mathbb{R}P^3$ 的[有理同调](@entry_id:263114)群 $H_n(\mathbb{R}P^3; \mathbb{Q})$ 来看看这一点 [@problem_id:1632635]。$\mathbb{R}P^3$ 的整数同调群是已知的：$H_0 \cong \mathbb{Z}$, $H_1 \cong \mathbb{Z}_2$, $H_2=0$, $H_3 \cong \mathbb{Z}$。其中 $H_1$ 是一个挠扑群。

我们可以将 $\mathbb{R}P^3$ 分解为 $A \cup B$，其中 $B$ 是一个[开球](@entry_id:143668)（因此可缩），而 $A = \mathbb{R}P^3 \setminus \{p\}$ (其中 $p \in B$)。这个 $A$ 同伦等价于 $\mathbb{R}P^2$，交集 $A \cap B$ 则同伦等价于球面 $S^2$。

这些空间的[有理同调](@entry_id:263114)群为：
-   $H_k(B; \mathbb{Q})$：因为 $B$ 可缩，所以 $H_0(B; \mathbb{Q}) \cong \mathbb{Q}$，$H_k(B; \mathbb{Q})=0$ for $k>0$。
-   $H_k(A; \mathbb{Q}) \cong H_k(\mathbb{R}P^2; \mathbb{Q})$：$\mathbb{R}P^2$ 的整数同调群是 $H_0 \cong \mathbb{Z}, H_1 \cong \mathbb{Z}_2$。因此，它的[有理同调](@entry_id:263114)群是 $H_0(\mathbb{R}P^2; \mathbb{Q}) \cong \mathbb{Q}$，$H_k(\mathbb{R}P^2; \mathbb{Q})=0$ for $k>0$。
-   $H_k(A \cap B; \mathbb{Q}) \cong H_k(S^2; \mathbb{Q})$：$H_0(S^2; \mathbb{Q}) \cong \mathbb{Q}$, $H_2(S^2; \mathbb{Q}) \cong \mathbb{Q}$，其他阶为0。

将这些代入迈尔-维托里斯序列。
对于 $n=3$:
$$
0 = H_3(A;\mathbb{Q}) \oplus H_3(B;\mathbb{Q}) \to H_3(\mathbb{R}P^3;\mathbb{Q}) \xrightarrow{\partial_*} H_2(A \cap B;\mathbb{Q}) \cong \mathbb{Q} \to H_2(A;\mathbb{Q}) \oplus H_2(B;\mathbb{Q}) = 0
$$
正合性迫使 $\partial_*$ 是一个同构，因此 $H_3(\mathbb{R}P^3; \mathbb{Q}) \cong \mathbb{Q}$。

对于 $n=2$:
$$
\mathbb{Q} \cong H_2(A \cap B;\mathbb{Q}) \to 0 = H_2(A;\mathbb{Q}) \oplus H_2(B;\mathbb{Q}) \to H_2(\mathbb{R}P^3;\mathbb{Q}) \to H_1(A \cap B;\mathbb{Q}) = 0
$$
正合性意味着 $H_2(\mathbb{R}P^3; \mathbb{Q}) = 0$。

对于 $n=1$:
$$
0 \to H_1(\mathbb{R}P^3; \mathbb{Q}) \to H_0(A \cap B; \mathbb{Q}) \cong \mathbb{Q} \to H_0(A; \mathbb{Q}) \oplus H_0(B; \mathbb{Q}) \cong \mathbb{Q} \oplus \mathbb{Q}
$$
由于 $A \cap B$ 在 $A$ 和 $B$ 中都是非空的，从 $\mathbb{Q}$ 到 $\mathbb{Q} \oplus \mathbb{Q}$ 的映射是单射。因此 $H_1(\mathbb{R}P^3; \mathbb{Q})$ 的像是0，故 $H_1(\mathbb{R}P^3; \mathbb{Q})=0$。

综上所述，$H_n(\mathbb{R}P^3; \mathbb{Q})$ 在 $n=0, 3$ 时为 $\mathbb{Q}$，其他情况为0。与整数同调群相比，我们看到 $H_1(\mathbb{R}P^3; \mathbb{Z}) \cong \mathbb{Z}_2$ 的挠扑部分在有理系数下“消失”了。这表明，通过选择不同的系数群，迈尔-维托里斯序列可以用来探测空间不同方面的代数拓扑特性。

总之，迈尔-维托里斯序列是一个极其灵活和强大的工具。通过巧妙地分[解空间](@entry_id:200470)，并细致地分析交集的[拓扑性质](@entry_id:141605)以及序列中的诱导映射，我们可以计算出许多复杂空间的同调群，从而深刻地理解它们的几何结构。