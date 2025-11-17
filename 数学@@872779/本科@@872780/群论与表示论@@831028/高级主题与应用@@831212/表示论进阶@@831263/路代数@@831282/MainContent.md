## 引言
路代数（Path Algebra）是现代表数学中一个迷人而强大的概念，它在[图论](@entry_id:140799)的直观性与[代数表示](@entry_id:143783)论的抽象性之间架起了一座坚实的桥梁。在研究复杂的[代数结构](@entry_id:137052)时，我们常常希望能有一种更具体、更具[组合性](@entry_id:637804)的方法来理解和构造它们。路代数正是为了解决这一需求而生，它允许我们从一个简单的有向图——称为“[箭图](@entry_id:143940)”（quiver）——出发，系统地生成具有丰富结构的代数，并研究其上的表示。这种方法不仅简化了许多代数的描述，还揭示了代数性质与其底层组合结构之间深刻而优美的联系。

本文将带领读者深入路代数的世界。我们将分为三个核心章节，逐步揭开其神秘面纱：
*   在**原则与机理**一章中，我们将学习如何从一个[箭图](@entry_id:143940)出发，定义路径并构造路代数，掌握其[乘法规则](@entry_id:197368)和基本的代数性质，并最终理解其与[箭图表示](@entry_id:146286)之间至关重要的[等价关系](@entry_id:138275)。
*   在**应用与交叉学科联系**一章中，我们将探索路代数的强大应用，看它如何描述[上三角矩阵](@entry_id:150931)等经典代数，并揭示其在同调代数、[Auslander-Reiten理论](@entry_id:146542)、[代数几何](@entry_id:156300)乃至[弦论](@entry_id:145688)等前沿领域的惊人联系。
*   最后，在**动手实践**部分，您将通过一系列精心设计的问题，将理论知识应用于具体计算，从而巩固对路代数构造、乘法和表示同构的理解。

通过本次学习，您将掌握一种从组合视角理解和构建[代数表示](@entry_id:143783)的全新工具，为探索更广阔的数学领域打下坚实的基础。让我们从最基本的定义开始，踏上这段激动人心的旅程。

## 原则与机理

在本章中，我们将深入探讨路代数的核心原理与内在机制。路代数是连接[图论](@entry_id:140799)与[代数表示](@entry_id:143783)论的桥梁，它通过一种直观的方式，从称为“[箭图](@entry_id:143940)”的有向图出发，构建出丰富的[代数结构](@entry_id:137052)。我们将从基本定义开始，系统地建立路代数的框架，探索其代数性质，并最终揭示它与[箭图表示](@entry_id:146286)之间的深刻联系。

### 从图到代数：路代数的构造

路代数的起点是一个纯粹的组合对象：一个[有向图](@entry_id:272310)。我们将展示如何从这个简单的图形结构中，生发出一个具有完备运算规则的代数系统。

#### [箭图](@entry_id:143940)与路

在[表示论](@entry_id:137998)中，我们使用的有向图有一个专门的名称：**[箭图](@entry_id:143940) (quiver)**。一个[箭图](@entry_id:143940) $Q$ 由两个集合定义：一个顶点集 $Q_0$ 和一个箭矢集 $Q_1$。每个箭矢 $\alpha \in Q_1$ 都有一个源顶点 $s(\alpha) \in Q_0$ 和一个目标顶点 $t(\alpha) \in Q_0$。

有了顶点和连接它们的箭矢，我们自然可以考虑将箭矢首尾相连形成的“路”。在[箭图](@entry_id:143940) $Q$ 中，一条长度为 $k \ge 1$ 的**路 (path)** 是一个箭矢序列 $p = \alpha_k \dots \alpha_2 \alpha_1$，其连接规则是前一个箭矢的目标顶点必须是后一个箭矢的源顶点，即对所有的 $i=1, \dots, k-1$，都有 $t(\alpha_i) = s(\alpha_{i+1})$。这条路的源点是第一个箭矢的源点 $s(p) = s(\alpha_1)$，目标是最后一个箭矢的目标 $t(p) = t(\alpha_k)$。

请注意这里的记法约定：我们像[函数复合](@entry_id:144881)一样，从右向左读取路径的构成。$p = \alpha_k \dots \alpha_1$ 表示首先走过 $\alpha_1$，然后是 $\alpha_2$，依此类推，最后走过 $\alpha_k$。

除了由箭矢组成的路，我们还为每个顶点 $v \in Q_0$ 定义一条长度为 0 的**平凡路 (trivial path)**，记作 $e_v$。这条路可以想象成“停在原地不动”，它的源点和目标点都是 $v$。

让我们通过一个例子来具体化这些概念。考虑一个[箭图](@entry_id:143940) $Q$，其顶点集为 $Q_0 = \{1, 2, 3\}$，箭矢集为 $Q_1 = \{\alpha, \beta\}$，其中 $\alpha$ 从顶点 1 指向 2（记作 $\alpha: 1 \to 2$），$\beta$ 从顶点 2 指向 3（记作 $\beta: 2 \to 3$）。这个[箭图](@entry_id:143940)可以直观地表示为 $1 \xrightarrow{\alpha} 2 \xrightarrow{\beta} 3$。

现在我们来列出这个[箭图](@entry_id:143940)中的所有路 [@problem_id:1634486]：
*   **长度为 0 的路**：每个顶点对应一条平凡路，所以我们有 $e_1, e_2, e_3$。
*   **长度为 1 的路**：就是[箭图](@entry_id:143940)中的所有箭矢，即 $\alpha$ 和 $\beta$。
*   **长度为 2 的路**：我们需要寻找一个箭矢序列 $\alpha_2\alpha_1$ 满足 $t(\alpha_1) = s(\alpha_2)$。在我们的例子中，$t(\alpha)=2$ 且 $s(\beta)=2$，因此 $t(\alpha)=s(\beta)$。这构成了一条从 1 到 3 的有效路径 $\beta\alpha$。
*   **更长的路**：由于没有从顶点 3 出发的箭矢，我们无法在 $\beta\alpha$ 之后再连接任何箭矢。因此，不存在长度大于 2 的路。

值得注意的是，$\alpha\beta$ 并不是一条有效的路，因为根据我们的记法，它要求先走 $\beta$ 再走 $\alpha$。但 $t(\beta) = 3$ 而 $s(\alpha) = 1$，它们不匹配，所以无法连接。

#### 定义路代数 $kQ$

有了[箭图](@entry_id:143940)中的所有路，我们就可以定义**路代数 (path algebra)** $kQ$。给定一个域 $k$（例如实数域 $\mathbb{R}$ 或[复数域](@entry_id:153768) $\mathbb{C}$），路代数 $kQ$ 是一个以 $k$ 为系数的[向量空间](@entry_id:151108)，其**基 (basis)** 由[箭图](@entry_id:143940) $Q$ 中的所有路构成。这意味着 $kQ$ 中的任何一个元素都是这些路的有限[线性组合](@entry_id:154743)，形式为 $\sum c_i p_i$，其中 $c_i \in k$ 且 $p_i$是 $Q$ 中的路。

因此，路代数 $kQ$ 的维度等于 $Q$ 中所有路的数量。例如，对于[箭图](@entry_id:143940) $Q$ 为 $1 \to 2 \leftarrow 3$ [@problem_id:1625895]，其路径包括长度为0的 $e_1, e_2, e_3$ 和长度为1的 $\alpha: 1 \to 2, \beta: 3 \to 2$。由于 $t(\alpha)=2, s(\alpha)=1, t(\beta)=2, s(\beta)=3$，我们无法构造长度更长的路。所以，这个[箭图](@entry_id:143940)的所有路集合为 $\{e_1, e_2, e_3, \alpha, \beta\}$，路代数 $kQ$ 的维度为 5。

路代数的精髓在于其乘法运算。对于任意两条路 $p$ 和 $q$，它们的乘积 $pq$ 定义如下：
*   如果 $p$ 的终点与 $q$ 的源点匹配，即 $t(p) = s(q)$，则乘积 $pq$ 是将 $q$ 连接在 $p$ 之后形成的新路。
*   如果 $t(p) \neq s(q)$，则乘积 $pq$ 定义为零元素 $0$。

这个[乘法规则](@entry_id:197368)通过[双线性性](@entry_id:146819)（即满足分配律和数乘结合律）扩展到路代数 $kQ$ 中的所有元素。

让我们以一个循环[箭图](@entry_id:143940) $C_3$ 为例来说明这个[乘法规则](@entry_id:197368) [@problem_id:1634521]。设 $Q_0 = \{1, 2, 3\}$，箭矢为 $\alpha: 1 \to 2$, $\beta: 2 \to 3$, $\gamma: 3 \to 1$。
*   考虑乘积 $\alpha\beta$：这里 $p=\alpha, q=\beta$。因为 $t(\alpha) = 2$ 且 $s(\beta) = 2$，满足 $t(p)=s(q)$，所以 $\alpha\beta$ 是一个从 1 到 3 的非零路径。
*   考虑乘积 $\beta\alpha$：这里 $p=\beta, q=\alpha$。因为 $t(\beta) = 3$ 但 $s(\alpha) = 1$，不满足 $t(p)=s(q)$，所以 $\beta\alpha = 0$。

### 路代数的代数性质

路代数不仅仅是一个[向量空间](@entry_id:151108)，它拥有丰富的[代数结构](@entry_id:137052)，如结合律、单位元以及通常的非交换性。

#### [结合律](@entry_id:151180)与单位元

路代数的乘法是**结合的 (associative)**，即 $(pq)r = p(qr)$。这源于路径拼接本身的[结合性](@entry_id:147258)：无论先拼接 $q$ 和 $r$ 再接上 $p$，还是先拼接 $p$ 和 $q$ 再与 $r$ 组合，只要连接条件满足，最终得到的箭矢序列是完全相同的。

路代数还拥有一个乘法**单位元 (multiplicative identity)**。这个单位元是所有平凡路之和：$1_{kQ} = \sum_{i \in Q_0} e_i$。我们可以验证它对于任何路 $p: i \to j$ 都满足 $1_{kQ} \cdot p = p \cdot 1_{kQ} = p$。

#### 平凡路的角色：[幂等元](@entry_id:153117)

平凡路 $e_i$ 在路代数中扮演着至关重要的角色。它们是一族**正交[幂等元](@entry_id:153117) (orthogonal idempotents)**。
*   **[幂等性](@entry_id:190768) (Idempotent)**: $e_i^2 = e_i e_i = e_i$。这是因为 $t(e_i)=s(e_i)=i$，所以乘积是 $e_i$ 本身。
*   **正交性 (Orthogonal)**: 若 $i \neq j$，则 $e_i e_j = 0$。这是因为 $t(e_i)=i \neq j=s(e_j)$。

这些性质使得平凡路如同“投影算子”。对于任意一条从顶点 $i$ 到顶点 $j$ 的路 $p$ (即 $s(p)=i, t(p)=j$)，我们有：
$e_i p = p$ 且 $p e_j = p$
而对于任何不匹配的顶点 $k$，则有 $e_k p = 0$ ($k \neq i$) 和 $p e_k = 0$ ($k \neq j$)。

这些规则是进行代数计算的基础。例如，在循环[箭图](@entry_id:143940) $C_3$ 中，考虑两个元素 $x = e_1 + \gamma$ 和 $y = e_3 + \beta\alpha$ [@problem_id:1634495]。它们的乘积 $xy$ 可以通过展开并逐项应用[乘法规则](@entry_id:197368)来计算：
$xy = (e_1 + \gamma)(e_3 + \beta\alpha) = e_1 e_3 + e_1(\beta\alpha) + \gamma e_3 + \gamma(\beta\alpha)$
我们逐项分析：
*   $e_1 e_3 = 0$ (因为 $t(e_1)=1 \neq s(e_3)=3$)
*   $e_1 (\beta\alpha) = 0$ (因为 $t(e_1)=1 \neq s(\beta\alpha)=1$)。等一下，这里的 $s(\beta\alpha)=s(\alpha)=1$。所以 $t(e_1)=s(\beta\alpha)=1$。因此 $e_1(\beta\alpha)=\beta\alpha$。
*   $\gamma e_3 = 0$ (因为 $t(\gamma)=1 \neq s(e_3)=3$)
*   $\gamma(\beta\alpha) = \gamma\beta\alpha$ (因为 $t(\gamma)=1 = s(\beta\alpha)=1$)
将它们相加，得到 $xy = \beta\alpha + \gamma\beta\alpha$。

#### [非交换性](@entry_id:153545)与中心

路代数通常是**非交换的 (non-commutative)**，即一般情况下 $xy \neq yx$。我们可以通过计算**[交换子](@entry_id:158878) (commutator)** $[x, y] = xy - yx$ 来检验交换性。如果[交换子](@entry_id:158878)不为零，则代数是[非交换](@entry_id:136599)的。

考虑线性[箭图](@entry_id:143940) $A_3$：$1 \xrightarrow{\alpha} 2 \xrightarrow{\beta} 3$ [@problem_id:1634512]。设 $x = e_1 + \alpha$ 和 $y = 2e_2 + \beta$。
$xy = (e_1 + \alpha)(2e_2 + \beta) = 2e_1e_2 + e_1\beta + 2\alpha e_2 + \alpha\beta$。根据[乘法规则](@entry_id:197368)：
* $e_1e_2=0$ ($t(e_1)=1 \ne s(e_2)=2$)
* $e_1\beta=0$ ($t(e_1)=1 \ne s(\beta)=2$)
* $\alpha e_2 = \alpha$ ($t(\alpha)=2 = s(e_2)=2$)
* $\alpha\beta$ 是有效路径。
所以 $xy = 2\alpha + \alpha\beta$。
$yx = (2e_2 + \beta)(e_1 + \alpha) = 2e_2e_1 + 2e_2\alpha + \beta e_1 + \beta\alpha$。根据[乘法规则](@entry_id:197368)：
* $e_2e_1=0$ ($t(e_2)=2 \ne s(e_1)=1$)
* $e_2\alpha=0$ ($t(e_2)=2 \ne s(\alpha)=1$)
* $\beta e_1=0$ ($t(\beta)=3 \ne s(e_1)=1$)
* $\beta\alpha=0$ ($t(\beta)=3 \ne s(\alpha)=1$)
所以 $yx = 0$。
因此，[交换子](@entry_id:158878) $[x, y] = xy - yx = 2\alpha + \alpha\beta \neq 0$。这表明该路代数是非交换的。

代数的**中心 (center)** $Z(kQ)$ 是所有与代数中任何元素都交换的元素的集合。一个有趣的问题是：平凡[幂等元](@entry_id:153117) $e_i$ 何时位于中心？
对于任意箭矢 $\alpha: k \to l$，我们有 $e_i \alpha$ (非零仅当 $i=k$) 和 $\alpha e_i$ (非零仅当 $l=i$)。
要使 $e_i \alpha = \alpha e_i$ 对所有 $\alpha$ 成立：
*   若 $\alpha$ 从 $i$ 出发但不指向 $i$（即 $\alpha: i \to j, j \neq i$），则 $e_i \alpha = \alpha$ 但 $\alpha e_i = 0$。它们不交换。
*   若 $\alpha$ 指向 $i$ 但不从 $i$ 出发（即 $\alpha: j \to i, j \neq i$），则 $e_i \alpha = 0$ 但 $\alpha e_i = \alpha$。它们不交换。
*   若 $\alpha$ 与 $i$ 无关，则两者皆为零。
*   若 $\alpha$ 是在 $i$ 上的环（$\alpha: i \to i$），则 $e_i \alpha = \alpha$ 且 $\alpha e_i = \alpha$。它们交换。
因此，一个[幂等元](@entry_id:153117) $e_i$ 属于中心的充要条件是，所有与顶点 $i$ 相连的箭矢都是以 $i$ 为顶点的环 [@problem_id:1634501]。若要*所有*的 $e_i$ 都位于中心，那么[箭图](@entry_id:143940)中的*所有*箭矢都必须是环。

### 维度与结构

路代数的维度和结构由其底层[箭图](@entry_id:143940)的拓扑性质直接决定，特别是环路的存在与否。

#### 有限维与无限维

路代数 $kQ$ 的维度是 $Q$ 中路径的数量。这个数量可能是有限的，也可能是无限的。
*   如果一个[箭图](@entry_id:143940)不包含**有向环路 (oriented cycle)**（即一条起点和终点相同的非平凡路），则称该[箭图](@entry_id:143940)是**无环的 (acyclic)**。在无环[箭图](@entry_id:143940)中，任何路的长度都不能超过顶点的数量，因此路径的总数是有限的。这样的路代数是**有限维的**。我们之前分析的 $1 \to 2 \leftarrow 3$ 就是一个例子。
*   如果一个[箭图](@entry_id:143940)包含一个有向环路 $c$，比如一个从顶点 $v$ 出发又回到 $v$ 的路，那么我们可以反复遍历这个环路，构造出一系列无限多的、不同长度的路径：$c, c^2, c^3, \dots$。由于不同长度的路径在路代数中是线性无关的基元，这意味着路代数的基是无限集，因此路代数是**无限维的** [@problem_id:1634493]。

#### 带关系的路代数

在代数和[表示论](@entry_id:137998)中，许多重要的代数不仅由[箭图](@entry_id:143940)定义，还受到一些附加的“关系”约束。这些代数被称为**带关系的路代数 (path algebras with relations)** 或**商代数 (quotient algebras)**。

一个**关系 (relation)** 是路代数 $kQ$ 中的一个元素，通常是路径的线性组合。给定一组关系 $R = \{\rho_1, \dots, \rho_m\}$，我们可以生成一个由这些关系张成的**[双边理想](@entry_id:272452) (two-sided ideal)** $I = (\rho_1, \dots, \rho_m)$。这个理想包含所有形如 $\sum_j a_j \rho_{i_j} b_j$ 的元素，其中 $a_j, b_j$ 是 $kQ$ 中的任意元素。

直观地讲，生成一个理想并构造商代数 $A = kQ/I$，相当于在路代数中“强行令所有关系等于零”。

例如，考虑[箭图](@entry_id:143940) $1 \xrightarrow{\alpha} 2 \xrightarrow{\beta} 3$。其路代数 $kQ$ 的基是 $\{e_1, e_2, e_3, \alpha, \beta, \beta\alpha\}$，维度为 6。如果我们施加关系 $\beta\alpha = 0$，我们实际上是在研究商代数 $A = kQ/(\beta\alpha)$ [@problem_id:1634468]。理想 $I = (\beta\alpha)$ 在这个例子中非常简单，它就是由路径 $\beta\alpha$ 本身张成的空间（因为没有箭矢可以接在 $\beta\alpha$ 之后或 $\beta\alpha$ 之前）。在商代数 $A$ 中，基元 $\beta\alpha$ 被视为零。因此，$A$ 的一组基是 $\{e_1, e_2, e_3, \alpha, \beta\}$，其维度为 5。

理想的结构可能更复杂。考虑[箭图](@entry_id:143940) $1 \xrightarrow{\alpha} 2 \xrightarrow{\beta} 3 \xrightarrow{\gamma} 4$，并考察由路径 $g = \beta\alpha$ 生成的理想 $I = (g)$ [@problem_id:1634473]。理想 $I$ 中的元素是形如 $pgq$ 的路径的线性组合，其中 $p,q$ 是 $Q$ 中的路径。为了使 $p(\beta\alpha)q$ 非零，路径 $p$ 的终点必须是 $s(\beta\alpha)=1$，路径 $q$ 的源点必须是 $t(\beta\alpha)=3$。在 $Q$ 中，唯一终点为 1 的路径是平凡路 $e_1$，所以 $p=e_1$ 是唯一选择。源点为 3 的路径是 $q=e_3$ 和 $q=\gamma$。因此，由 $g$ 生成的路径基元是 $e_1(\beta\alpha)e_3 = \beta\alpha$ 和 $e_1(\beta\alpha)\gamma = \beta\alpha\gamma$。所以，路径 $\beta\alpha\gamma$ 属于理想 $I$。

### 连接表示论：路代数上的模

路代数理论的真正威力在于它与[箭图表示](@entry_id:146286)论的深刻联系。实际上，两者是同一枚硬币的两个面。

#### 从表示到模

首先，我们定义[箭图](@entry_id:143940) $Q$ 的一个**表示 (representation)**。一个表示 $V$ 为 $Q$ 的每个顶点 $i \in Q_0$ 赋予一个 $k$-[向量空间](@entry_id:151108) $V_i$，并为每个箭矢 $\alpha: i \to j$ 赋予一个[线性映射](@entry_id:185132) $V_\alpha: V_i \to V_j$。

[表示论](@entry_id:137998)中一个 foundational 的结果是：[箭图](@entry_id:143940) $Q$ 的表示范畴等价于左 $kQ$-**模 (module)** 的范畴。这意味着我们可以将关于表示的（通常是图形化和线性代数的）问题，转化为关于模的（纯代数的）问题，反之亦然。

这个转化的具体构造如下：给定一个 $Q$ 的表示 $V = (V_i, V_\alpha)$，我们可以构造一个对应的左 $kQ$-模 $M$。这个模的底层[向量空间](@entry_id:151108)是所有顶点空间的**[直和](@entry_id:156782) (direct sum)**：
$M = \bigoplus_{i \in Q_0} V_i$
一个 $M$ 中的元素 $m$ 可以看作是一个元组 $(m_1, m_2, \dots)$，其中每个分量 $m_i \in V_i$。

#### 路在模上的作用

要使 $M$ 成为一个左 $kQ$-模，我们需要定义路代数 $kQ$ 中的元素如何作用于 $M$ 中的向量。这个作用由路径的作用通过线性性扩展而来。

一个路径 $p: i \to j$ 在 $M$ 上的作用定义如下：它接收 $M$ 中的第 $i$ 个分量，通过与 $p$ 对应的复合[线性映射](@entry_id:185132)进行变换，然后将结果放入输出向量的第 $j$ 个分量中。
*   **平凡路 $e_i$ 的作用**：$e_i$ 作用在向量 $m = (m_j)_{j \in Q_0}$ 上，其结果是将除第 $i$ 个分量外的所有分量置零的向量，即 $e_i \cdot m = (0, \dots, m_i, \dots, 0)$。它起到了投影到[子空间](@entry_id:150286) $V_i$ 的作用。
*   **箭矢 $\alpha: i \to j$ 的作用**：$\alpha$ 作用在 $m$ 上，它取出分量 $m_i \in V_i$，应用[线性映射](@entry_id:185132) $V_\alpha$ 得到 $V_\alpha(m_i) \in V_j$，然后将此结果作为新向量的第 $j$ 个分量。所有其他分量为零。
*   **一般路径 $p=\alpha_k \dots \alpha_1$ 的作用**：它对应于[线性映射的复合](@entry_id:154187) $V_p = V_{\alpha_k} \circ \dots \circ V_{\alpha_1}$。它将源顶点 $s(p)$ 对应的分量通过 $V_p$ 映射到目标顶点 $t(p)$ 对应的空间。

让我们通过一个具体的计算来阐明这一点 [@problem_id:1787560]。考虑[箭图](@entry_id:143940) $Q$ 及其在 $\mathbb{R}$ 上的表示：
*   $Q_0 = \{1, 2, 3\}$, $Q_1 = \{\alpha: 1 \to 2, \beta: 2 \to 3, \gamma: 1 \to 3\}$
*   $V_1 = \mathbb{R}^2, V_2 = \mathbb{R}^3, V_3 = \mathbb{R}^2$
*   $V_\alpha = \begin{pmatrix} 1  0 \\ 2  -1 \\ 0  3 \end{pmatrix}, V_\beta = \begin{pmatrix} 1  1  0 \\ -2  0  1 \end{pmatrix}, V_\gamma = \begin{pmatrix} 0  1 \\ -1  1 \end{pmatrix}$

模空间为 $M = V_1 \oplus V_2 \oplus V_3 \cong \mathbb{R}^7$。设模中有一个向量 $m = (m_1, m_2, m_3)$，其中 $m_1 = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$, $m_2 = \begin{pmatrix} 1 \\ 0 \\ -1 \end{pmatrix}$, $m_3 = \begin{pmatrix} 4 \\ 5 \end{pmatrix}$。
我们计算路[代数元](@entry_id:153893)素 $r = 5e_1 + 2\gamma - \beta\alpha$ 作用在 $m$ 上的结果 $r \cdot m$。
$r \cdot m = (5e_1 + 2\gamma - \beta\alpha) \cdot (m_1 + m_2 + m_3)$

根据线性性，我们分别计算每一项的作用：
1.  **$5e_1 \cdot m$**：路径 $e_1$ 的源点和终点都是 1。它只对 $m_1$ 分量有非零作用，作用方式是恒等映射。结果向量在 $V_1$ 分量上是 $5 \cdot \text{Id}(m_1) = 5m_1$，其他分量为零。
2.  **$2\gamma \cdot m$**：路径 $\gamma$ 从 1 到 3。它只对 $m_1$ 有非零作用。结果向量在 $V_3$ 分量上是 $2V_\gamma(m_1)$，其他分量为零。
3.  **$-\beta\alpha \cdot m$**：路径 $\beta\alpha$ 从 1 到 3。它也只对 $m_1$ 有非零作用。结果向量在 $V_3$ 分量上是 $-V_\beta(V_\alpha(m_1))$，其他分量为零。

最终结果 $w = r \cdot m$ 是一个在 $M$ 中的新向量 $w=(w_1, w_2, w_3)$。
*   $w_1$ (在 $V_1$ 中) 只由终点为 1 的路径贡献，即 $5e_1$。所以 $w_1 = 5m_1 = 5 \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 5 \\ 10 \end{pmatrix}$。
*   $w_2$ (在 $V_2$ 中) 由终点为 2 的路径贡献。$r$ 中的路径没有终点为 2 的，所以 $w_2 = \begin{pmatrix} 0 \\ 0 \\ 0 \end{pmatrix}$。
*   $w_3$ (在 $V_3$ 中) 由终点为 3 的路径贡献，即 $2\gamma$ 和 $-\beta\alpha$。
    $w_3 = 2V_\gamma(m_1) - V_{\beta\alpha}(m_1)$
    $V_\gamma(m_1) = \begin{pmatrix} 0  1 \\ -1  1 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 2 \\ 1 \end{pmatrix}$
    $V_{\beta\alpha}(m_1) = V_\beta V_\alpha m_1 = \begin{pmatrix} 1  1  0 \\ -2  0  1 \end{pmatrix} \begin{pmatrix} 1  0 \\ 2  -1 \\ 0  3 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 3  -1 \\ -2  3 \end{pmatrix} \begin{pmatrix} 1 \\ 2 \end{pmatrix} = \begin{pmatrix} 1 \\ 4 \end{pmatrix}$
    所以 $w_3 = 2\begin{pmatrix} 2 \\ 1 \end{pmatrix} - \begin{pmatrix} 1 \\ 4 \end{pmatrix} = \begin{pmatrix} 3 \\ -2 \end{pmatrix}$。

将各分量组合起来，得到最终结果在 $\mathbb{R}^7$ 中的表示：
$r \cdot m = \begin{pmatrix} w_1 \\ w_2 \\ w_3 \end{pmatrix} = \begin{pmatrix} 5 \\ 10 \\ 0 \\ 0 \\ 0 \\ 3 \\ -2 \end{pmatrix}$。

这个例子完美地展示了路代数的抽象代数运算是如何转化为对[向量空间](@entry_id:151108)的具体[线性变换](@entry_id:149133)的，从而为研究[表示论](@entry_id:137998)提供了强大而系统的代数工具。