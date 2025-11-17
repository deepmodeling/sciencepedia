## 引言
在自然科学与数学的广阔领域中，许多系统表现出由多个相互独立的对称性共同支配的特征。例如，一个分子的总对称性可能源于其空间结构和[电子自旋](@entry_id:137016)的组合；一个物理系统的[哈密顿量](@entry_id:172864)可能同时在坐标空间和某个内部空间中保持不变。描述这种复合对称性的自然语言是群论中的**[直积](@entry_id:143046)群**。然而，一个关键的问题随之而来：我们如何理解和分类这样一个复合系统的[状态和](@entry_id:193625)行为？这在数学上转化为一个核心挑战：如何系统地构建和分解一个直积[群的表示](@entry_id:140711)？

本文旨在全面解答这一问题，为读者提供一套理解[直积](@entry_id:143046)[群表示](@entry_id:156757)的完整理论框架和实用工具。我们将证明，一个看似复杂的[直积](@entry_id:143046)[群表示](@entry_id:156757)理论，实际上可以被优雅地分解为其构成部分的表示的组合，遵循着简洁而强大的[乘法规则](@entry_id:197368)。

在接下来的内容中，我们将分三步展开：
- **“原理与机制”** 章节将深入探讨该理论的数学核心，从表示的**外张量积**构造出发，系统阐述其维度、特征标的计算方法，并揭示其与[群代数](@entry_id:145139)及子[群结构](@entry_id:146855)的深刻联系。
- **“应用与[交叉](@entry_id:147634)学科联系”** 章节将展示这些抽象原理的强大威力，通过具体案例，说明该理论如何被应用于解决[量子力学中的角动量](@entry_id:142408)耦合、化学中的[光谱选择定则](@entry_id:139860)，以及抽象代数中的结构分解等前沿问题。
- **“动手实践”** 部分则提供了一系列精心设计的问题，旨在帮助读者巩固理论知识，并将所学应用于解决实际计算。

通过本次学习，你将不仅掌握直积[群表示](@entry_id:156757)的基本构造，更能体会到它作为连接不同对称世界的桥梁所扮演的关键角色。让我们首先从构建这一理论的基石——外[张量积](@entry_id:140694)开始。

## 原理与机制

本章在前一章介绍性内容的基础上，深入探讨直积[群表示](@entry_id:156757)理论的核心原理与机制。我们将系统地构建[直积](@entry_id:143046)群的表示，阐明其维度与特征标的计算方法，并探索其与[群代数](@entry_id:145139)、[子群](@entry_id:146164)及商[群表示](@entry_id:156757)之间的深刻联系。

### 表示的外[张量积](@entry_id:140694)

构建两个或多个群的复合系统表示的基石是**外张量积（outer tensor product）**，有时也称为**外积（outer product）**。假设 $G_1$ 和 $G_2$ 是两个群，$\rho_1: G_1 \to \text{GL}(V_1)$ 和 $\rho_2: G_2 \to \text{GL}(V_2)$ 分别是它们在[复向量空间](@entry_id:264355) $V_1$ 和 $V_2$ 上的表示。它们的外张量积，记为 $\rho_1 \boxtimes \rho_2$，是[直积](@entry_id:143046)群 $G = G_1 \times G_2$ 在张量积空间 $V_1 \otimes V_2$ 上的一个表示。

对于 $G_1 \times G_2$ 中的任意元素 $(g_1, g_2)$（其中 $g_1 \in G_1, g_2 \in G_2$），它在表示 $\rho_1 \boxtimes \rho_2$ 下的作用定义为：
$$
(\rho_1 \boxtimes \rho_2)(g_1, g_2) = \rho_1(g_1) \otimes \rho_2(g_2)
$$
其中右侧是两个线性算符的[张量积](@entry_id:140694)。不难验证，这个定义确实构成了一个[群表示](@entry_id:156757)，因为它保持了群的乘法结构：
$$
\begin{align*}
(\rho_1 \boxtimes \rho_2)((g_1, g_2)(h_1, h_2))  &= (\rho_1 \boxtimes \rho_2)(g_1h_1, g_2h_2) \\
 &= \rho_1(g_1h_1) \otimes \rho_2(g_2h_2) \\
 &= (\rho_1(g_1)\rho_1(h_1)) \otimes (\rho_2(g_2)\rho_2(h_2)) \\
 &= (\rho_1(g_1) \otimes \rho_2(g_2)) (\rho_1(h_1) \otimes \rho_2(h_2)) \\
 &= (\rho_1 \boxtimes \rho_2)(g_1, g_2) (\rho_1 \boxtimes \rho_2)(h_1, h_2)
\end{align*}
$$

直积[群表示](@entry_id:156757)理论的一个基本定理指出，这种构造方法涵盖了所有的不可约表示。

**定理：** 若 $\{\rho_i^{(1)}\}_{i \in I}$ 和 $\{\rho_j^{(2)}\}_{j \in J}$ 分别是群 $G_1$ 和 $G_2$ 的完备非同构不可约表示集，则集合 $\{\rho_i^{(1)} \boxtimes \rho_j^{(2)}\}_{(i,j) \in I \times J}$ 构成了[直积](@entry_id:143046)群 $G_1 \times G_2$ 的一个完备非同构不可约表示集。

这个定理意味着，要理解 $G_1 \times G_2$ 的表示，我们只需理解其[构成因子](@entry_id:141517) $G_1$ 和 $G_2$ 的表示，并将它们通过张量积组合起来。

### 基本性质：维度与特征标

基于外张量积的定义，我们可以立即推导出直积[群表示](@entry_id:156757)的两个最基本也是最重要的性质：维度和特征标。

#### 维度

[张量积](@entry_id:140694)空间的维度是其构成空间维度的乘积。因此，表示 $\rho_1 \boxtimes \rho_2$ 的**维度（dimension）**是：
$$
\dim(\rho_1 \boxtimes \rho_2) = \dim(V_1 \otimes V_2) = (\dim V_1) \cdot (\dim V_2) = \dim(\rho_1) \cdot \dim(\rho_2)
$$
这个简单的乘法关系是解决许多问题的关键。例如，考虑确定直积群 $G = S_3 \times D_6$ 所有4维[不可约表示的数量](@entry_id:147329)。我们首先需要知道[因子群](@entry_id:146225) $S_3$（6阶对称群）和 $D_6$（12阶二面体群）的[不可约表示](@entry_id:263310)的维度。
- $S_3$ 有三个[不可约表示](@entry_id:263310)，维度分别为 $1, 1, 2$。
- $D_6$ 有六个[不可约表示](@entry_id:263310)，维度分别为 $1, 1, 1, 1, 2, 2$。

我们寻找所有维度对 $(d_1, d_2)$，其中 $d_1$ 来自 $S_3$ 的维度集， $d_2$ 来自 $D_6$ 的维度集，使得它们的乘积 $d_1 \cdot d_2 = 4$。通过检验，唯一满足条件的组合是 $2 \times 2 = 4$。$S_3$ 有一个2维[不可约表示](@entry_id:263310)，$D_6$ 有两个2维[不可约表示](@entry_id:263310)。因此，$S_3 \times D_6$ 的4维[不可约表示](@entry_id:263310)的总数就是这些可能组合的数量，即 $1 \times 2 = 2$ 个 [@problem_id:755483]。

#### 特征标

表示的**特征标（character）**是[矩阵的迹](@entry_id:139694)。对于外[张量积表示](@entry_id:143629)，其特征标同样具有简洁的乘法形式。利用迹的性质 $\text{Tr}(A \otimes B) = \text{Tr}(A) \text{Tr}(B)$，我们得到：
$$
\chi_{\rho_1 \boxtimes \rho_2}(g_1, g_2) = \text{Tr}((\rho_1 \boxtimes \rho_2)(g_1, g_2)) = \text{Tr}(\rho_1(g_1) \otimes \rho_2(g_2)) = \text{Tr}(\rho_1(g_1)) \cdot \text{Tr}(\rho_2(g_2))
$$
即
$$
\chi_{\rho_1 \boxtimes \rho_2}(g_1, g_2) = \chi_{\rho_1}(g_1) \cdot \chi_{\rho_2}(g_2)
$$
[直积](@entry_id:143046)[群的表示](@entry_id:140711)特征标是在特定元素上各分量特征标的乘积。

让我们通过一个具体的例子来理解这个公式的应用。考虑群 $G = D_6 \times Q_8$，其中 $D_6$ 是12阶二面体群，$Q_8$ 是8阶[四元数群](@entry_id:147721)。假设 $\rho_{D_6}$ 是 $D_6$ 的一个2维[不可约表示](@entry_id:263310)，$\rho_{Q_8}$ 是 $Q_8$ 的一个2维[不可约表示](@entry_id:263310)。我们想计算它们的[张量积表示](@entry_id:143629) $\rho = \rho_{D_6} \boxtimes \rho_{Q_8}$ 在元素 $(r^2, j) \in D_6 \times Q_8$ 上的特征标值。根据公式，我们有：
$$
\chi_{\rho}(r^2, j) = \chi_{\rho_{D_6}}(r^2) \cdot \chi_{\rho_{Q_8}}(j)
$$
首先，计算 $\chi_{\rho_{D_6}}(r^2)$。在 $D_6$ 的几何表示中，$r$ 是一个旋转 $\frac{2\pi}{6} = \frac{\pi}{3}$ 的操作，所以 $r^2$ 是一个旋转 $\frac{2\pi}{3}$ 的操作。一个[二维旋转矩阵](@entry_id:154975) $\begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$ 的迹是 $2\cos\theta$。因此，$\chi_{\rho_{D_6}}(r^2) = 2\cos(\frac{2\pi}{3}) = 2(-\frac{1}{2}) = -1$。

接下来，计算 $\chi_{\rho_{Q_8}}(j)$。在 $Q_8$ 的标准2维表示中，$j$ 由矩阵 $\begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$ 表示。该矩阵的迹为 $0+0=0$。

最后，我们将这两个值相乘，得到 $\chi_{\rho}(r^2, j) = (-1) \cdot 0 = 0$ [@problem_id:755459]。这个例子清晰地展示了如何利用各部分的特征标来计算整个系统的特征标。

### 与[群结构](@entry_id:146855)的联系

直积[群的表示](@entry_id:140711)理论与其[代数结构](@entry_id:137052)密切相关，特别是共轭类和[群代数](@entry_id:145139)的结构。

#### 共轭类与[不可约表示的数量](@entry_id:147329)

一个群的非同构[不可约表示的数量](@entry_id:147329)等于其**共轭类（conjugacy classes）**的数量。对于直积群 $G = G_1 \times G_2$，其共轭类具有非常简单的形式。如果 $C_i \subseteq G_1$ 和 $K_j \subseteq G_2$ 分别是 $G_1$ 和 $G_2$ 的共轭类，那么笛卡尔积 $C_i \times K_j$ 就是 $G_1 \times G_2$ 的一个[共轭类](@entry_id:143916)。因此，$G_1 \times G_2$ 的[共轭类](@entry_id:143916)总数是 $G_1$ 和 $G_2$ [共轭类](@entry_id:143916)数量的乘积。
$$
k(G_1 \times G_2) = k(G_1) \cdot k(G_2)
$$
这与我们之前关于不可约表示数量的定理是自洽的：
$$
|Irr(G_1 \times G_2)| = |Irr(G_1)| \cdot |Irr(G_2)|
$$
这个关系可以与[群代数](@entry_id:145139)联系起来。一个[有限群](@entry_id:139710) $G$ 的[群代数](@entry_id:145139) $\mathbb{C}[G]$ 的**中心 $Z(\mathbb{C}[G])$** 的维度等于 $G$ 的[共轭类](@entry_id:143916)数。因此，我们可以推断出：
$$
\dim_{\mathbb{C}} Z(\mathbb{C}[G_1 \times G_2]) = k(G_1 \times G_2) = k(G_1) \cdot k(G_2) = (\dim_{\mathbb{C}} Z(\mathbb{C}[G_1])) \cdot (\dim_{\mathbb{C}} Z(\mathbb{C}[G_2]))
$$
例如，要计算[群代数](@entry_id:145139) $\mathbb{C}[SL(2,3) \times S_4]$ 中心的维度，我们只需知道 $SL(2,3)$ 和 $S_4$ 各自的共轭类数。已知 $SL(2,3)$ 有7个共轭类，$S_4$（4元素[置换群](@entry_id:142907)）有5个[共轭类](@entry_id:143916)（由整数4的划分决定）。因此，$\dim_{\mathbb{C}}Z(\mathbb{C}[SL(2,3) \times S_4]) = 7 \times 5 = 35$ [@problem_id:755572]。

#### 特殊性质：忠实性与[实值特征标](@entry_id:143937)

表示的某些定性性质在[张量积](@entry_id:140694)下也表现出简单的行为。

一个表示 $\rho$ 被称为是**忠实的（faithful）**，如果它的核 $\ker(\rho)$ 是[平凡子群](@entry_id:141709) $\{e\}$。对于由不可约表示构成的外[张量积](@entry_id:140694) $\rho = \rho_1 \boxtimes \rho_2$，其核的结构如下。一个元素 $(g_1, g_2)$ 属于核，当且仅当 $\rho_1(g_1) \otimes \rho_2(g_2) = I \otimes I$。根据[舒尔引理](@entry_id:136779)，这意味着 $\rho_1(g_1)$ 和 $\rho_2(g_2)$ 都必须是标量矩阵，即 $\rho_1(g_1) = \lambda I$ 且 $\rho_2(g_2) = \mu I$，并且它们的乘积 $\lambda\mu=1$。因此，$\ker(\rho_1 \boxtimes \rho_2)$ 由所有满足 $\rho_1(g_1) = \lambda I$ 和 $\rho_2(g_2) = \lambda^{-1} I$ 的元素对 $(g_1, g_2)$ 组成。表示 $\rho_1 \boxtimes \rho_2$ 是忠实的，当且仅当除了 $(e_1, e_2)$ 之外，不存在满足此条件的元素对。这**不**等同于要求 $\rho_1$ 和 $\rho_2$ 都是忠实的。然而，如果 $\rho_1$ 或 $\rho_2$ 中有一个不是忠实的（例如 $\ker(\rho_1) \neq \{e_1\}$），那么对于任意 $g_1 \in \ker(\rho_1)$ 且 $g_1 \neq e_1$，元素 $(g_1, e_2)$ 就在 $\ker(\rho_1 \boxtimes \rho_2)$ 中，因此[张量积表示](@entry_id:143629)也不是忠实的。所以，**因[子表示](@entry_id:141094)的忠实性是[张量积表示](@entry_id:143629)忠实的必要条件，但非充分条件**。

以 $G = D_4 \times S_3$ 为例，要找到其忠实的[不可约表示](@entry_id:263310)，我们必须找到 $D_4$ 和 $S_3$ 各自的[不可约表示](@entry_id:263310) $\rho_1, \rho_2$，并检查张量积 $\rho_1 \boxtimes \rho_2$ 的核是否平凡。首先，如果 $\rho_1$ 或 $\rho_2$ 不忠实，则 $\rho_1 \boxtimes \rho_2$ 也不忠实。
- 对于 $D_4$（8阶），它有四个1维表示和一个2维表示。所有1维表示都通过其[交换化](@entry_id:140523)子 $D_4/[D_4,D_4] \cong \mathbb{Z}_2 \times \mathbb{Z}_2$ 分解，因此它们的核都非平凡。只有那个2维的“几何”表示是忠实的。
- 对于 $S_3$（6阶），它有两个1维表示（[平凡表示](@entry_id:141357)和符号表示）和一个2维标准表示。两个1维[表示的核](@entry_id:202190)分别是 $S_3$ 和 $A_3$，都是非平凡的。只有2维标准表示是忠实的。
因此，我们只需考虑忠实[表示的张量积](@entry_id:137150)：即 $D_4$ 的2维表示 $\rho_{D_4}$ 与 $S_3$ 的2维表示 $\rho_{S_3}$ 的张量积。我们需要检查是否存在 $(g_1, g_2) \neq (e, e)$ 使得 $\rho_{D_4}(g_1) = \lambda I$ 且 $\rho_{S_3}(g_2) = \lambda^{-1} I$。
- 在 $S_3$ 中，由于其中心是平凡的，只有单位元 $e$ 在[不可约表示](@entry_id:263310)下的像是标量矩阵 $I$ (即 $\lambda=1$)。
- 因此，我们必须有 $\lambda^{-1}=1$，即 $\lambda=1$。这意味着 $\rho_{S_3}(g_2) = I$。由于 $\rho_{S_3}$ 是忠实的，这迫使 $g_2 = e$。
- 相应的，我们必须有 $\rho_{D_4}(g_1) = 1 \cdot I = I$。由于 $\rho_{D_4}$ 也是忠实的，这迫使 $g_1 = e$。
- 唯一的解是 $(g_1, g_2) = (e, e)$，因此核是平凡的。
所以，$D_4$ 有1个忠实不可约表示，$S_3$ 也有1个，而它们的[张量积](@entry_id:140694)是 $D_4 \times S_3$ 的一个忠实不可约表示。因此，$D_4 \times S_3$ 的忠实不可约表示数量是 $1 \times 1 = 1$ 个 [@problem_id:755493]。

另一个性质是特征标的**实值性（real-valuedness）**。如果一个表示 $\rho$ 的特征标 $\chi_\rho(g)$ 对所有 $g \in G$ 都是实数，我们称其为实值表示。由于实数的乘积仍然是实数，如果 $\chi_1$ 和 $\chi_2$ 都是[实值特征标](@entry_id:143937)，那么它们的乘积 $\chi_1 \chi_2$ 也是实值的。因此，两个实值[表示的张量积](@entry_id:137150)仍然是实值的。

一个群的所有不可约特征标都是实值的充分必要条件是该群的每个元素都与其逆共轭（这种群称为**含糊群（ambivalent group）**）。[对称群](@entry_id:146083) $S_n$ 和二面体群 $D_{n}$ 都是含糊群的例子。如果 $G_1$ 和 $G_2$ 都是含糊群，那么它们的所有不可约特征标都是实值的。因此，$G_1 \times G_2$ 的所有不可约特征标（作为乘积）也都是实值的。例如，$S_4$ 和 $D_5$ 都是含糊群，所以它们各自的所有不可约表示（分别为5个和4个）都是实值的。因此，[直积](@entry_id:143046)群 $S_4 \times D_5$ 的所有 $5 \times 4 = 20$ 个[不可约表示](@entry_id:263310)也都是实值的 [@problem_id:755639]。

### 高级应用与相关构造

[直积](@entry_id:143046)群的表示理论是更复杂结构的基础，例如[子群](@entry_id:146164)限制、[诱导表示](@entry_id:136842)和[中心积](@entry_id:199155)。

#### 对角[子群](@entry_id:146164)的限制与[Clebsch-Gordan分解](@entry_id:139084)

在物理学和化学中，一个常见的问题是考虑两个对称性相同的系统如何耦合。在数学上，这对应于研究直积群 $G \times G$ 的表示如何在其**对角[子群](@entry_id:146164)（diagonal subgroup）** $\Delta(G) = \{(g, g) \in G \times G \mid g \in G\}$ 上表现。注意 $\Delta(G)$ 与 $G$ 本身是同构的。

当我们把 $G \times G$ 的一个[不可约表示](@entry_id:263310) $\rho_\lambda \boxtimes \rho_\mu$ 限制到对角[子群](@entry_id:146164) $\Delta(G)$ 上时，我们得到一个 $\Delta(G) \cong G$ 的表示。对于 $(g,g) \in \Delta(G)$：
$$
(\rho_\lambda \boxtimes \rho_\mu)(g, g) = \rho_\lambda(g) \otimes \rho_\mu(g)
$$
这正是 $G$ 的两个表示 $\rho_\lambda$ 和 $\rho_\mu$ 的**内张量积（internal tensor product）** $\rho_\lambda \otimes \rho_\mu$。这个表示通常是可约的，即使 $\rho_\lambda$ 和 $\rho_\mu$ 是不可约的。将其分解为 $G$ 的[不可约表示](@entry_id:263310)之和的过程，在物理学中被称为**[Clebsch-Gordan分解](@entry_id:139084)**。
$$
\text{Res}^{G \times G}_{\Delta(G)}(\rho_\lambda \boxtimes \rho_\mu) \cong \rho_\lambda \otimes \rho_\mu = \bigoplus_{\nu} a_{\nu} \rho_{\nu}
$$
其中 $\rho_\nu$ 是 $G$ 的[不可约表示](@entry_id:263310)，系数 $a_\nu$ 称为 Clebsch-Gordan 系数或重数。

这些重数可以通过[特征标理论](@entry_id:144021)计算。由于限制后的表示特征标为 $\chi_{\text{res}}(g) = \chi_\lambda(g) \chi_\mu(g)$，[重数](@entry_id:136466) $a_\nu$ 由[内积](@entry_id:158127)公式给出：
$$
a_\nu = \langle \chi_{\text{res}}, \chi_\nu \rangle_G = \frac{1}{|G|} \sum_{g \in G} \chi_\lambda(g) \chi_\mu(g) \overline{\chi_\nu(g)}
$$
以 $G = S_4$ 为例，考虑 $S_4 \times S_4$ 的表示 $\Pi = \rho_{(3,1)} \boxtimes \rho_{(2,1,1)}$。限制到对角[子群](@entry_id:146164) $H \cong S_4$ 上，我们得到 $S_4$ 的一个表示，其特征标是 $\chi_{(3,1)}$ 和 $\chi_{(2,1,1)}$ 的逐点乘积。利用 $S_4$ 的特征标表，我们可以计算这个乘积特征标，然后用[内积](@entry_id:158127)公式计算出它包含各个不可约表示 $\rho_\lambda$ 的重数 $a_\lambda$ [@problem_id:755507]。这一过程不仅在理论上重要，在处理角动量耦合等量子力学问题时也至关重要。

这一思想也与[中心化子代数](@entry_id:141029)有关。在代数 $\mathbb{C}[G \times G]$ 中，对角子[群代数](@entry_id:145139) $\mathbb{C}[\Delta(G)]$ 的[中心化子](@entry_id:146604) $Z_{\mathbb{C}[G \times G]}(\mathbb{C}[\Delta(G)])$ 的维度，可以通过将 $\mathbb{C}[G \times G]$ 分解为[矩阵代数](@entry_id:153824)的[直和](@entry_id:156782)，并对每一块应用[舒尔引理](@entry_id:136779)来计算。其维度最终等于 $\sum_{\lambda, \mu} \langle \chi_\lambda \otimes \chi_\mu, \chi_\lambda \otimes \chi_\mu \rangle_G = \sum_{\lambda, \mu, \nu} a_{\nu}(\lambda,\mu)^2$，其中 $a_\nu(\lambda, \mu)$ 是 $\rho_\lambda \otimes \rho_\mu$ 分解式中 $\rho_\nu$ 的重数 [@problem_id:755443]。

#### [诱导表示](@entry_id:136842)与[Frobenius互反律](@entry_id:140909)

表示论的另一个强大工具是**[诱导表示](@entry_id:136842)（induced representation）**。[Frobenius互反律](@entry_id:140909)将[诱导与限制](@entry_id:182341)联系起来。这个定律在直积群的背景下同样适用，并能产生有趣的结果。

考虑 $G=S_4 \times S_3$ 及其[子群](@entry_id:146164) $H = A_4 \times \{e\}$。我们可以从 $H$ 的[平凡表示](@entry_id:141357) $\psi=1$ 出发，诱导得到 $G$ 的一个表示 $V = \text{Ind}_H^G(\psi)$。要将 $V$ 分解为 $G$ 的不可约表示 $\rho_i \otimes \sigma_j$ 的直和，我们需计算重数 $a_{ij}$。根据[Frobenius互反律](@entry_id:140909)：
$$
a_{ij} = \langle \text{Ind}_H^G(\psi), \rho_i \otimes \sigma_j \rangle_G = \langle \psi, \text{Res}^G_H(\rho_i \otimes \sigma_j) \rangle_H
$$
限制到 $H = A_4 \times \{e\}$，表示 $\rho_i \otimes \sigma_j$ 变为 $\text{Res}_{A_4}(\rho_i) \otimes \text{Res}_{\{e\}}(\sigma_j)$。在[平凡子群](@entry_id:141709) $\{e\}$ 上，$\sigma_j$ 成为 $\dim(\sigma_j)$ 个平凡[表示的[直](@entry_id:138310)和](@entry_id:156782)。因此，[内积](@entry_id:158127)可以分解为：
$$
a_{ij} = \langle 1_{A_4}, \text{Res}_{A_4}(\rho_i) \rangle_{A_4} \cdot \langle 1_{\{e\}}, \text{Res}_{\{e\}}(\sigma_j) \rangle_{\{e\}}
$$
第一个因子是 $\rho_i$ 限制到 $A_4$ 后包含平凡[表示的[重](@entry_id:138441)数](@entry_id:136466)，可以通过在 $A_4$ 的元素上对 $\chi_{\rho_i}$求和来计算。第二个因子就是 $\sigma_j$ 的维度。这个例子 [@problem_id:755466] 巧妙地结合了直积、诱导、限制和[Frobenius互反律](@entry_id:140909)，展示了这些概念如何协同工作。

#### 从直积到[中心积](@entry_id:199155)

[直积](@entry_id:143046)是群构造的一种方式，**[中心积](@entry_id:199155)（central product）**则是其一种重要的推广。设 $G_1, G_2$ 是两个群，它们分别有中心[子群](@entry_id:146164) $Z_1 \le Z(G_1)$ 和 $Z_2 \le Z(G_2)$，并且存在一个同构 $\phi: Z_1 \to Z_2$。[中心积](@entry_id:199155) $G_1 \circ_{Z_1} G_2$ 定义为商群 $(G_1 \times G_2)/N$，其中 $N = \{(z, \phi(z)^{-1}) \mid z \in Z_1\}$ 是一个[正规子群](@entry_id:147397)。

[中心积](@entry_id:199155)的不可约表示与直积的不可约表示密切相关。具体来说，[中心积](@entry_id:199155) $G_1 \circ_{Z_1} G_2$ 的[不可约表示](@entry_id:263310)与那些在核 $N$ 上平凡的 $G_1 \times G_2$ 的不可约表示一一对应。

一个表示 $\rho_1 \boxtimes \rho_2$ 在 $N$ 上平凡，意味着对于所有 $z \in Z_1$，有 $(\rho_1 \boxtimes \rho_2)(z, \phi(z)^{-1}) = I$。由于 $\rho_1$ 和 $\rho_2$ 是不可约表示，中心元素 $z \in Z_1$ 和 $\phi(z) \in Z_2$ 在其上的作用是标量矩阵，即 $\rho_1(z) = \omega_1(z)I_1$ 和 $\rho_2(\phi(z)) = \omega_2(\phi(z))I_2$。这里的 $\omega_1, \omega_2$ 称为**中心特征标（central characters）**。因此，平凡性条件变为：
$$
\omega_1(z) \cdot \omega_2(\phi(z)^{-1}) \cdot (I_1 \otimes I_2) = I_1 \otimes I_2
$$
这等价于一个**[兼容性条件](@entry_id:201103)**：
$$
\omega_1(z) = \omega_2(\phi(z)) \quad \text{对所有 } z \in Z_1
$$
这意味着，只有那些中心特征标通过同构 $\phi$ 匹配的不可约表示对 $(\rho_1, \rho_2)$ 才能“存活”下来，成为[中心积](@entry_id:199155)的[不可约表示](@entry_id:263310)。

例如，考虑[中心积](@entry_id:199155) $G = SL(2,3) \circ_{\mathbb{Z}_2} Q_8$。$SL(2,3)$ 和 $Q_8$ 都有一个唯一的2阶中心，我们将其等同。要寻找 $G$ 的4维[不可约表示](@entry_id:263310)，我们首先寻找 $SL(2,3)$ 和 $Q_8$ 的不可约表示 $\rho_1, \rho_2$，使得 $\dim(\rho_1) \cdot \dim(\rho_2) = 4$。唯一的可能性是 $\dim(\rho_1)=2$ 和 $\dim(\rho_2)=2$。接下来，我们检查它们的中心特征标是否匹配。
- $SL(2,3)$ 的3个2维表示，其[非平凡中心](@entry_id:145503)元素都作用为 $-I$（中心特征标为-1）。
- $Q_8$ 的1个2维表示，其[非平凡中心](@entry_id:145503)元素也作用为 $-I$（中心特征标为-1）。
中心特征标匹配（-1 = -1）。因此，$SL(2,3)$ 的每个2维表示都可以与 $Q_8$ 的2维表示配对，形成一个4维表示。所以，总共有 $3 \times 1 = 3$ 个4维不可约表示 [@problem_id:755449] [@problem_id:755583]。

综上所述，直积[群的表示](@entry_id:140711)论通过[张量积](@entry_id:140694)这一核心机制，将复杂系统的[表示分解](@entry_id:139061)为更简单组成部分的表示的组合。其维度、特征标和各种性质都遵循着清晰的[乘法规则](@entry_id:197368)。此外，这一理论还为理解如对角[子群](@entry_id:146164)限制、[Clebsch-Gordan分解](@entry_id:139084)和[中心积](@entry_id:199155)等更高级的构造提供了坚实的基础。