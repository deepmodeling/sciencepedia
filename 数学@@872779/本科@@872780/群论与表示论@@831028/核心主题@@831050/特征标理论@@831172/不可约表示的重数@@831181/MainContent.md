## 引言
在[群表示论](@entry_id:141930)中，一个基本而深刻的结论是：任何有限群的[复表示](@entry_id:144331)都可以唯一地分解为[不可约表示](@entry_id:263310)的直和。这一结构性的事实自然引出了一个核心问题：在这个分解中，每一个特定的不可约表示究竟出现了多少次？这个计数被称为“重数”，是理解和量化表示内部结构的关键。直接通过寻找[不变子空间](@entry_id:152829)来分解一个表示往往极其困难，这构成了理论应用中的一个巨大障碍。幸运的是，[特征标理论](@entry_id:144021)提供了一条优雅的捷径，将这一复杂的代数问题转化为简单的数值计算。

本文旨在系统阐述[不可约表示](@entry_id:263310)[重数](@entry_id:136466)的概念、计算方法及其广泛应用。在接下来的章节中，我们将首先在 **“原理与机制”** 中深入探讨[重数](@entry_id:136466)的定义，并详细介绍如何利用[特征标内积](@entry_id:137125)这一强大工具来精确计算重数，同时揭示其背后的代数内涵。随后，我们将在 **“应用与跨学科联系”** 一章中，展示重数概念如何在物理、化学、[组合数学](@entry_id:144343)等领域中发挥作用，用以解决从粒子系统对称性到[分子振动](@entry_id:140827)模式分析等实际问题。最后，通过 **“动手实践”** 部分提供的一系列练习，读者将有机会亲手应用所学知识，巩固对这一核心工具的掌握。

## 原理与机制

在上一章中，我们已经了解到[有限群](@entry_id:139710)的任何[复表示](@entry_id:144331)都可以分解为一系列[不可约表示](@entry_id:263310)（irreducible representations, or irreps）的[直和](@entry_id:156782)。一个深刻而优美的结果是，对于任何给定的表示，这种分解在同构和求和顺序的意义下是唯一的。这一结论自然引出了一个核心问题：在给定的表示中，每个特定的[不可约表示](@entry_id:263310)“出现”了多少次？这个计数就是我们本章将要深入探讨的核心概念——**[重数](@entry_id:136466)（multiplicity）**。理解和计算重数是表示论的基石，它使得我们能够仅通过考察[表示的特征标](@entry_id:198072)就完全确定其内部结构。

### [重数](@entry_id:136466)的定义与直观理解

从最直观的层面理解，一个[不可约表示](@entry_id:263310) $U_i$ 在一个表示 $V$ 中的**重数**，记作 $n_i$，就是当我们将 $V$ 分解为[不可约表示](@entry_id:263310)的[直和](@entry_id:156782)时，$U_i$（或其同构表示）作为[直和项](@entry_id:150541)出现的次数。如果一个表示 $V$ 的分解式为：

$$
V \cong n_1 U_1 \oplus n_2 U_2 \oplus \dots \oplus n_k U_k
$$

其中 $\{U_1, \dots, U_k\}$ 是该群所有不等价的[不可约表示](@entry_id:263310)的完备集，那么整数 $n_i \ge 0$ 就是 $U_i$ 在 $V$ 中的重数。

例如，假设 $U$ 和 $W$ 是群 $G$ 的两个不等价的不可约表示。我们构造一个新的表示，其[向量空间](@entry_id:151108)为 $V = U \oplus W \oplus U \oplus W \oplus U$。通过检视这个直和的结构，我们可以直接数出每个不可约分量的数量。表示 $U$ 在此出现了三次，而 $W$ 出现了两次。因此，我们说 $U$ 在 $V$ 中的重数是 3，而 $W$ 的[重数](@entry_id:136466)是 2 [@problem_id:1630980]。

这个定义虽然清晰，但在实践中却有局限。我们通常不是以一个显式的[直和](@entry_id:156782)形式得到一个表示，而是通过矩阵、[置换](@entry_id:136432)或作用在某个函数空间上的变换来定义它。在这些情况下，直接分解表示以寻找[不变子空间](@entry_id:152829)并识别其类型是一项极其繁琐乃至不可能完成的任务。幸运的是，[特征标理论](@entry_id:144021)为我们提供了一个优雅而强大的计算工具。

### 利用[特征标计算](@entry_id:139604)重数

[特征标理论](@entry_id:144021)的巨大成功之一在于它将计算重数这一复杂的代数问题，转化为了一个简单的数值计算。其核心工具是**[特征标内积](@entry_id:137125)（character inner product）**。对于定义在群 $G$ 上的两个[类函数](@entry_id:146970) $\alpha$ 和 $\beta$（例如两个特征标），它们的[内积](@entry_id:158127)定义为：

$$
\langle \alpha, \beta \rangle = \frac{1}{|G|} \sum_{g \in G} \alpha(g) \overline{\beta(g)}
$$

其中 $|G|$ 是群 $G$ 的阶，$\overline{\beta(g)}$ 表示 $\beta(g)$ 的[复共轭](@entry_id:174690)。由于特征标在共轭类上取值恒定，此公式可以更高效地通过对[共轭类](@entry_id:143916)求和来计算：

$$
\langle \alpha, \beta \rangle = \frac{1}{|G|} \sum_{C} |C| \cdot \alpha(g_C) \overline{\beta(g_C)}
$$

其中求和遍历 $G$ 的所有[共轭类](@entry_id:143916) $C$，$|C|$ 是类 $C$ 中元素的数量，$g_C$ 是类 $C$ 中的任意一个代表元。

不可约[表示的特征标](@entry_id:198072)构成一组关于此[内积](@entry_id:158127)的正交规范基，即若 $\chi_i$ 和 $\chi_j$ 是两个不可约特征标，则 $\langle \chi_i, \chi_j \rangle = \delta_{ij}$（当 $i=j$ 时为 1，否则为 0）。

现在，回到我们的表示 $V$。其特征标 $\chi_V$ 是其不可约分量特征标的线性组合，系数正是[重数](@entry_id:136466)：

$$
\chi_V = \sum_{i=1}^{k} n_i \chi_i
$$

利用[特征标的正交性](@entry_id:140971)，我们可以像在[向量空间](@entry_id:151108)中提取分量一样，轻松地分离出每一个重数 $n_j$。只需将上式与 $\chi_j$ 做[内积](@entry_id:158127)：

$$
\langle \chi_V, \chi_j \rangle = \left\langle \sum_{i=1}^{k} n_i \chi_i, \chi_j \right\rangle = \sum_{i=1}^{k} n_i \langle \chi_i, \chi_j \rangle = \sum_{i=1}^{k} n_i \delta_{ij} = n_j
$$

于是，我们得到了计算[重数](@entry_id:136466)的黄金法则：

**[不可约表示](@entry_id:263310) $U_j$ 在表示 $V$ 中的[重数](@entry_id:136466) $n_j$，等于它们的特征标 $\chi_V$ 和 $\chi_j$ 的[内积](@entry_id:158127)。**

$$
n_j = \langle \chi_V, \chi_j \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_V(g) \overline{\chi_j(g)}
$$

这个公式是[表示论](@entry_id:137998)中最为实用的结果之一。它意味着只要我们知道一个[表示的特征标](@entry_id:198072)（即每个群元素对应[线性变换](@entry_id:149133)的迹），以及群的所有不可约特征标（通常以[特征标表](@entry_id:146676)的形式给出），我们就可以完全确定该表示的内部结构，而无需进行任何矩阵分解或寻找[不变子空间](@entry_id:152829)。

### 应用与实例

#### 基本计算

让我们通过一个具体的例子来演示这个公式的威力。考虑3阶[循环群](@entry_id:138668) $G = C_3 = \{e, a, a^2\}$，并设 $\omega = \exp(2\pi i / 3)$。一个4维表示 $\rho$ 由其在生成元 $a$ 上的作用定义为 $\rho(a) = \operatorname{diag}(\omega, \omega, \omega, \omega^2)$。我们要计算一个特定的不可约表示 $\Gamma_1$ 在 $\rho$ 中的重数，已知 $\Gamma_1$ 的特征标 $\chi_1$ 满足 $\chi_1(a) = \omega$。

首先，我们需要表示 $\rho$ 的特征标 $\chi_\rho$。
$\chi_\rho(e) = \operatorname{tr}(I_4) = 4$
$\chi_\rho(a) = \operatorname{tr}(\rho(a)) = 3\omega + \omega^2$
$\chi_\rho(a^2) = \operatorname{tr}(\rho(a^2)) = \operatorname{tr}(\rho(a)^2) = 3\omega^2 + \omega$

[不可约表示](@entry_id:263310) $\Gamma_1$ 是一维的，其特征标为 $\chi_1(e)=1, \chi_1(a)=\omega, \chi_1(a^2)=\omega^2$。其复共轭为 $\overline{\chi_1(e)}=1, \overline{\chi_1(a)}=\omega^2, \overline{\chi_1(a^2)}=\omega$。

现在，我们可以应用[内积](@entry_id:158127)公式计算 $\Gamma_1$ 的重数 $m_{\Gamma_1}$ [@problem_id:1630943]：

$$
m_{\Gamma_1} = \langle \chi_\rho, \chi_1 \rangle = \frac{1}{3} \sum_{g \in C_3} \chi_\rho(g) \overline{\chi_1(g)}
$$
$$
m_{\Gamma_1} = \frac{1}{3} \left( \chi_\rho(e)\overline{\chi_1(e)} + \chi_\rho(a)\overline{\chi_1(a)} + \chi_\rho(a^2)\overline{\chi_1(a^2)} \right)
$$
$$
m_{\Gamma_1} = \frac{1}{3} \left( 4 \cdot 1 + (3\omega + \omega^2)\omega^2 + (3\omega^2 + \omega)\omega \right)
$$
利用 $\omega^3 = 1$ 和 $\omega^4 = \omega$，我们得到：
$$
m_{\Gamma_1} = \frac{1}{3} \left( 4 + (3\omega^3 + \omega^4) + (3\omega^3 + \omega^2) \right) = \frac{1}{3} \left( 4 + (3+\omega) + (3+\omega^2) \right)
$$
再利用 $1 + \omega + \omega^2 = 0$，上式化为：
$$
m_{\Gamma_1} = \frac{1}{3} (10 + \omega + \omega^2) = \frac{1}{3} (10 - 1) = \frac{9}{3} = 3
$$
因此，不可约表示 $\Gamma_1$ 在表示 $\rho$ 中出现了3次。

#### 平凡[表示的重数](@entry_id:138441)

一个特别重要的[不可约表示](@entry_id:263310)是**[平凡表示](@entry_id:141357)（trivial representation）**，它将所有群元素都映射到1。其特征标 $\chi_T$ 因此恒为1，即 $\chi_T(g) = 1$ 对所有 $g \in G$ 成立。计算其在任意表示 $V$ 中的[重数](@entry_id:136466) $m_T$ 时，公式变得异常简洁：
$$
m_T = \langle \chi_V, \chi_T \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_V(g) \overline{1} = \frac{1}{|G|} \sum_{g \in G} \chi_V(g)
$$
这意味着，平凡[表示的[重](@entry_id:138441)数](@entry_id:136466)就是表示 $V$ 的特征标在整个群上的平均值。在物理和几何中，这通常对应于系统中在群 $G$ 的所有对称变换下保持不变的维度或状态数。

例如，考虑对称群 $S_4$（阶为24）的一个16维表示 $V$，其在五个[共轭类](@entry_id:143916)上的特征标值已知。我们要计算[平凡表示](@entry_id:141357)在 $V$ 中的[重数](@entry_id:136466) [@problem_id:1630960]。
- 恒等元类 (1个元素): $\chi_V = 16$
- 对换类 (6个元素): $\chi_V = 4$
- 3-轮换类 (8个元素): $\chi_V = 1$
- 4-轮换类 (6个元素): $\chi_V = 0$
- 双对换类 (3个元素): $\chi_V = 0$

利用对共轭类的求和公式：
$$
m_T = \frac{1}{24} \left( 1 \cdot 16 + 6 \cdot 4 + 8 \cdot 1 + 6 \cdot 0 + 3 \cdot 0 \right)
$$
$$
m_T = \frac{1}{24} (16 + 24 + 8) = \frac{48}{24} = 2
$$
所以，在这个16维表示中，[平凡表示](@entry_id:141357)（即在所有 $S_4$ [置换](@entry_id:136432)下不变的[子空间](@entry_id:150286)）的维度为2。

#### 可约性判据

[特征标内积](@entry_id:137125)不仅能计算重数，还能提供一个简单的**可约性判据**。一个非零表示 $V$ 是不可约的，当且仅当其自身是唯一的不可约分量，即 $n_i = 1$ 对应于 $V$ 自身，而所有其他 $n_j=0$。这意味着：

$$
\langle \chi_V, \chi_V \rangle = \left\langle \sum_i n_i \chi_i, \sum_j n_j \chi_j \right\rangle = \sum_{i,j} n_i n_j \langle \chi_i, \chi_j \rangle = \sum_i n_i^2 = 1
$$

因此，我们有结论：**一个表示 $V$ 是不可约的，当且仅当 $\langle \chi_V, \chi_V \rangle = 1$**。如果 $\langle \chi_V, \chi_V \rangle > 1$，则表示 $V$ 是可约的，并且这个[内积](@entry_id:158127)的值 $\sum_i n_i^2$ 衡量了其分解的“复杂性”。例如，如果 $\langle \chi_V, \chi_V \rangle = 4$，那么分解可能是 $V \cong 2U_1$ 或 $V \cong U_1 \oplus U_2 \oplus U_3 \oplus U_4$ (假设 $n_i$ 只能是 0 或 1)。通过计算与各个不可约[特征标的内积](@entry_id:137615)，我们可以精确确定每种情况 [@problem_id:1607779]。

### [重数](@entry_id:136466)的代数内涵：[阿贝尔群](@entry_id:150284)的情形

对于[阿贝尔群](@entry_id:150284)，所有不可约表示都是一维的。这为[重数](@entry_id:136466)提供了一个非常清晰的代数解释。在一个[阿贝尔群](@entry_id:150284) $G$ 的表示 $(\rho, V)$ 中，由于所有群元素的作用 $\rho(g)$ 相互交换，它们构成了一个可交换的[线性算子](@entry_id:149003)族。根据线性代数的基本定理，这个算子族可以被[同时对角化](@entry_id:196036)。这意味着存在一个 $V$ 的基，使得在该基下，每个 $\rho(g)$ 都是一个[对角矩阵](@entry_id:637782)。

基中的每个向量 $v$ 都是所有 $\rho(g)$ 的共同[特征向量](@entry_id:151813)。对于这样一个向量 $v$，对任意 $g \in G$，有 $\rho(g)v = \lambda_g v$。不难验证，映射 $g \mapsto \lambda_g$ 本身构成了一个从 $G$ 到 $\mathbb{C}^\times$ 的[群同态](@entry_id:140603)，即 $G$ 的一个一维特征标。

因此，整个表示空间 $V$ 可以分解为一系列的同时特征[子空间](@entry_id:150286) $V_{\chi_j}$ 的直和：
$$
V = \bigoplus_j V_{\chi_j} \quad \text{其中} \quad V_{\chi_j} = \{v \in V \mid \rho(g)v = \chi_j(g)v \text{ for all } g \in G\}
$$
这里的 $\chi_j$ 是 $G$ 的一个不可约特征标（一个[一维表示](@entry_id:136509)）。

在这个框架下，[不可约表示](@entry_id:263310) $\chi_j$ 在 $V$ 中的**[重数](@entry_id:136466) $n_j$**，精确地等于**对应于特征标 $\chi_j$ 的同时特征[子空间](@entry_id:150286) $V_{\chi_j}$ 的维度** [@problem_id:1630974]。换言之，$n_j = \dim(V_{\chi_j})$。在量子力学中，这对应于具有相同对称性[量子数](@entry_id:145558)（由特征标 $\chi_j$ 定义）的[简并态](@entry_id:274678)的数量。

### 特殊表示中的[重数](@entry_id:136466)

#### [正则表示](@entry_id:137028)

**[正则表示](@entry_id:137028)（regular representation）** $R$ 是一个在群论中具有基础地位的表示。它的表示空间以群 $G$ 自身元素为基，群元素通过[左乘作用](@entry_id:140679)于这些[基向量](@entry_id:199546)。[正则表示的特征标](@entry_id:137278) $\chi_R$ 有一个非常独特的性质：
$$
\chi_R(g) = \begin{cases} |G|  \text{if } g = e \\ 0  \text{if } g \neq e \end{cases}
$$
利用这个性质，我们可以计算任意[不可约表示](@entry_id:263310) $U_i$（维度为 $d_i = \chi_i(e)$）在[正则表示](@entry_id:137028)中的[重数](@entry_id:136466) $m_i$ [@problem_id:1630986]：
$$
m_i = \langle \chi_R, \chi_i \rangle = \frac{1}{|G|} \sum_{g \in G} \chi_R(g) \overline{\chi_i(g)} = \frac{1}{|G|} \left( \chi_R(e) \overline{\chi_i(e)} + \sum_{g \neq e} 0 \cdot \overline{\chi_i(g)} \right)
$$
$$
m_i = \frac{1}{|G|} (|G| \cdot \overline{d_i}) = d_i
$$
因为维度 $d_i$ 是一个正整数，所以 $\overline{d_i}=d_i$。这个惊人的结果表明：**每个不可约表示 $U_i$ 在[正则表示](@entry_id:137028)中出现的次数，恰好等于它自身的维度 $d_i$**。

这个结论有一个重要的推论。[正则表示](@entry_id:137028)的维度等于[群的阶](@entry_id:137115) $|G|$。根据其分解，我们有：
$$
\dim(R) = \sum_i m_i \dim(U_i) = \sum_i d_i \cdot d_i = \sum_i d_i^2
$$
于是我们得到了著名的**平方和公式**：$|G| = \sum_i d_i^2$，即群的阶等于其所有不可约表示维度的平方和。

#### [张量积表示](@entry_id:143629)

从现有表示构造新表示的一个重要方法是**张量积（tensor product）**。如果 $V$ 和 $W$ 是群 $G$ 的两个表示，它们的[张量积](@entry_id:140694) $V \otimes W$ 也是 $G$ 的一个表示。其特征标由一个简单的逐点[乘法规则](@entry_id:197368)给出：
$$
\chi_{V \otimes W}(g) = \chi_V(g) \chi_W(g)
$$
知道了张量积[表示的特征标](@entry_id:198072)，我们就可以用标准[内积](@entry_id:158127)公式计算任何[不可约表示](@entry_id:263310) $U$ 在其中的[重数](@entry_id:136466)：
$$
m_U(V \otimes W) = \langle \chi_{V \otimes W}, \chi_U \rangle = \langle \chi_V \chi_W, \chi_U \rangle
$$
例如，对于8阶二面体群 $D_4$，给定两个表示 $V$ 和 $W$ 的特征标，我们可以计算其[张量积](@entry_id:140694) $V \otimes W$ 中某个二维[不可约表示](@entry_id:263310) $E$ 的[重数](@entry_id:136466) [@problem_id:1604301]。首先，我们通过逐点相乘得到 $\chi_{V \otimes W}$ 的值，然后将其与 $\chi_E$ 的值代入[内积](@entry_id:158127)公式，并考虑每个[共轭类](@entry_id:143916)的大小，最终得到重数。这个过程在处理物理系统中角动量耦合等问题时至关重要。

### 高阶性质与应用

#### 实特征标与[共轭表示](@entry_id:139136)

在许多物理应用中，[表示的特征标](@entry_id:198072)都是实数，即 $\chi_V(g) \in \mathbb{R}$ 对所有 $g \in G$ 成立。这对此表示的结构施加了有趣的约束。考虑一个“复”不可约表示 $U$，即它与其复[共轭表示](@entry_id:139136) $\bar{U}$ 不等价。我们知道 $\bar{U}$ 的特征标是 $\chi_{\bar{U}}(g) = \overline{\chi_U(g)}$。

设 $U$ 和 $\bar{U}$ 在 $V$ 中的重数分别为 $m_U$ 和 $m_{\bar{U}}$。我们有：
$$
m_U = \langle \chi_V, \chi_U \rangle \quad \text{和} \quad m_{\bar{U}} = \langle \chi_V, \chi_{\bar{U}} \rangle = \langle \chi_V, \overline{\chi_U} \rangle
$$
现在，对 $m_U$ 取复共轭：
$$
\overline{m_U} = \overline{\langle \chi_V, \chi_U \rangle} = \overline{\frac{1}{|G|} \sum_g \chi_V(g) \overline{\chi_U(g)}} = \frac{1}{|G|} \sum_g \overline{\chi_V(g)} \chi_U(g)
$$
因为 $\chi_V$ 是实特征标，$\overline{\chi_V(g)} = \chi_V(g)$。所以，
$$
\overline{m_U} = \frac{1}{|G|} \sum_g \chi_V(g) \chi_U(g)
$$
我们发现，这个表达式恰好是 $\langle \chi_V, \overline{\chi_U} \rangle$，也就是 $m_{\bar{U}}$。因此，$\overline{m_U} = m_{\bar{U}}$。但[重数](@entry_id:136466)必须是非负整数，所以它们本身就是实数，这意味着 $m_U = \overline{m_U}$。结论是：
$$
m_U = m_{\bar{U}}
$$
这个结果 [@problem_id:1630962] 表明，**在一个实特征标的表示中，任何复不可约表示和它的[共轭表示](@entry_id:139136)必须以相同的重数成对出现**。

#### 张量幂与不可约表示的生成

[特征标理论](@entry_id:144021)的一个深刻结果（与Burnside和Brauer的工作相关）是，对于一个[有限单群](@entry_id:143576) $G$，其任何一个**[忠实表示](@entry_id:144577)**（faithful representation） $V$（即[群同态](@entry_id:140603) $\rho: G \to GL(V)$ 是[单射](@entry_id:183792)），通过重复取张量积，最终可以“生成”出 $G$ 的所有[不可约表示](@entry_id:263310)。更精确地说，对任意不可约表示 $U$，都存在一个正整数 $k$，使得 $U$ 在张量幂表示 $V^{\otimes k} = V \otimes \dots \otimes V$ ($k$ 次)的分解中具有非零[重数](@entry_id:136466)。

我们可以用一个具体的例子来感受这个定理的力量。考虑最小的非阿贝尔[单群](@entry_id:140851) $A_5$（阶为60），它有两个[不可约表示](@entry_id:263310) $V$ (3维) 和 $U$ (4维)。$V$ 是一个[忠实表示](@entry_id:144577)。我们要寻找最小的正整数 $k$，使得 $U$ 在 $V^{\otimes k}$ 中的[重数](@entry_id:136466) $m_k = \langle (\chi_V)^k, \chi_U \rangle$ 不为零。

通过系统地计算 $k=1, 2, 3, \dots$ 时的[内积](@entry_id:158127) [@problem_id:1630998]：
- 对于 $k=1$，计算 $\langle \chi_V, \chi_U \rangle$，结果为 0。
- 对于 $k=2$，计算 $\langle (\chi_V)^2, \chi_U \rangle$，结果仍为 0。
- 对于 $k=3$，计算 $\langle (\chi_V)^3, \chi_U \rangle$，结果为 1。

因此，最小的 $k$ 是 3。这具体地展示了，即使一个不可约表示 $U$ 没有出现在 $V$ 或 $V \otimes V$ 中，它也可能在更高阶的张量积中“浮现”出来。这个原理在粒子物理的模型构建等前沿领域具有重要意义。

有时，我们甚至不需要完整的[特征标表](@entry_id:146676)就能确定[重数](@entry_id:136466)。通过将关系式 $\chi_V = \sum n_i \chi_i$ 在少数几个关键的群元素或[共轭类](@entry_id:143916)上求值，我们可以得到一个关于未知[重数](@entry_id:136466) $n_i$ 的线性方程组。如果已知信息足够，解这个[方程组](@entry_id:193238)就能得到所需的[重数](@entry_id:136466) [@problem_id:1630972]。这再次凸显了[特征标理论](@entry_id:144021)作为一种灵活而强大的分析工具的价值。