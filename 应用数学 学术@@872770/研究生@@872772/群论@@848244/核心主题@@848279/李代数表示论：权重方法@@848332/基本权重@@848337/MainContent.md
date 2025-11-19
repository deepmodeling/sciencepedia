## 引言
在[半单李代数](@entry_id:190073)的宏伟结构中，基本权（fundamental weights）扮演着基石般的角色，尤其是在其[表示论](@entry_id:137998)的研究中。与作为代数“原子”的单根（simple roots）相比，基本权为我们提供了一套更强大、更自然的语言来构造、分类和理解不可约表示的复杂世界。基本权不仅是抽象的代数对象，更是描绘对称性内在几何的坐标，其深刻意义贯穿了纯数学和理论物理的诸多领域。

本文旨在系统性地阐明基本权的理论及其应用。我们首先将解决一个核心问题：为何在已有单根的基础上，仍需引入基本权这一对偶概念？答案在于它们为表示论提供无与伦比的便利性。通过本文，读者将全面学习基本权的核心知识。第一章“原理和机制”将深入探讨基本权的定义，揭示其与单根通过[嘉当矩阵](@entry_id:185184)建立的对偶关系，并阐明它们所生成的[权格](@entry_id:195778)与根格的几何与拓扑内涵。第二章“应用与跨学科联系”将展示这些理论工具的威力，从计算表示维度和[张量积分解](@entry_id:138873)，到解释物理学中[大统一理论](@entry_id:150304)的对称性破缺。最后，“动手实践”部分将提供具体问题，帮助读者巩固所学，将抽象理论转化为解决实际问题的能力。

## 原理和机制

在研究[半单李代数](@entry_id:190073)及其表示的结构时，有两个基础向量集合至关重要：单根（simple roots）和基本权（fundamental weights）。单根构成了根系的基石，通过它们可以生成整个根系并构建代数的生成元和关系。然而，在构造和分类[不可约表示](@entry_id:263310)时，基本权提供了一个更自然、更强大的框架。本章将深入探讨基本权的定义、它们与单根的对偶关系、它们所生成的几何结构，以及它们在表示论中的核心作用。

### 定义与对偶性

我们从一个秩为 $r$ 的[半单李代数](@entry_id:190073) $\mathfrak{g}$ 开始。其[根系](@entry_id:198970)位于[嘉当子代数](@entry_id:191259)（Cartan subalgebra）$\mathfrak{h}$ 的对偶空间 $\mathfrak{h}^*$ 中。这个空间配备了一个由[基灵型](@entry_id:161046)（Killing form）诱导的非退化[内积](@entry_id:158127) $(\cdot, \cdot)$。一个关键的构造是**单根**（simple roots）的集合 $\{\alpha_1, \dots, \alpha_r\}$，它们是 $\mathfrak{h}^*$ 的一个基。

为了引入基本权，我们首先定义**单[余根](@entry_id:193338)**（simple coroots）。对于每一个单根 $\alpha_j$，对应的单[余根](@entry_id:193338) $\alpha_j^\vee$ 定义为：
$$
\alpha_j^\vee = \frac{2\alpha_j}{(\alpha_j, \alpha_j)}
$$
这些单[余根](@entry_id:193338)构成了 $\mathfrak{h}$ 的一个基，与 $\mathfrak{h}^*$ 中的单根基 $\{\alpha_i\}$ 密切相关。

现在，我们可以定义**基本权**（fundamental weights）。基本权集合 $\{\omega_1, \dots, \omega_r\}$ 是 $\mathfrak{h}^*$ 中的一个基，其定义方式是与单[余根](@entry_id:193338)基形成对偶关系。具体来说，第 $i$ 个基本权 $\omega_i$ 由以下关系唯一确定：
$$
(\omega_i, \alpha_j^\vee) = \delta_{ij}
$$
其中 $\delta_{ij}$ 是克罗内克（Kronecker）符号。将单[余根](@entry_id:193338)的定义代入，这个对偶关系可以更直接地用单根和[内积](@entry_id:158127)来表示：
$$
\frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}
$$
这个定义是整个理论的基石。它表明，在由[内积](@entry_id:158127)定义的几何结构中，每个基本权 $\omega_i$ 在与 $\alpha_i$ 相关的“方向”上具有单位长度（经过适当归一化），同时与所有其他的单根 $\alpha_j$ ($j \neq i$)“正交”。这种对偶性使得基本权成为描述表示的“自然[坐标系](@entry_id:156346)”。

### 基的相互作用：根与权

由于单根 $\{\alpha_i\}$ 和基本权 $\{\omega_i\}$ 都是 $\mathfrak{h}^*$ 的基，它们之间必然可以通过线性变换相互表示。这些变换的[系数矩阵](@entry_id:151473)不是任意的，而是由代数的核心结构——[嘉当矩阵](@entry_id:185184)（Cartan matrix）$A$——精确确定。

#### 在权基中表示根

要将在基本权基中表示任意一个根（或权）$\lambda = \sum_i c_i \omega_i$，我们可以利用对偶关系。将表达式与 $\alpha_j^\vee$ 作[内积](@entry_id:158127)，我们得到：
$$
(\lambda, \alpha_j^\vee) = \sum_{i=1}^r c_i (\omega_i, \alpha_j^\vee) = \sum_{i=1}^r c_i \delta_{ij} = c_j
$$
因此，系数 $c_j$ 就是 $\lambda$ 与第 $j$ 个单[余根](@entry_id:193338)的[内积](@entry_id:158127)。

现在，让我们将这个结果应用于单根本身。若取 $\lambda = \alpha_k$，则其在基本权基下的第 $j$ 个分量为：
$$
c_j = (\alpha_k, \alpha_j^\vee) = \frac{2(\alpha_k, \alpha_j)}{(\alpha_j, \alpha_j)} = A_{kj}
$$
这里的 $A_{kj}$ 正是[嘉当矩阵](@entry_id:185184)的第 $(k, j)$ 个元素。因此，我们得到了一个至关重要的关系式，它将单根表示为基本权的线性组合：
$$
\alpha_k = \sum_{j=1}^r A_{kj} \omega_j
$$
这意味着，[嘉当矩阵](@entry_id:185184)的第 $k$ 行的元素，恰好是单根 $\alpha_k$ 在基本权基下的坐标。

例如，考虑 $C_3$ 型[李代数](@entry_id:137954)（即 $\mathfrak{sp}(6)$），其[嘉当矩阵](@entry_id:185184)为：
$$
A = \begin{pmatrix} 2  -1  0 \\ -1  2  -2 \\ 0  -1  2 \end{pmatrix}
$$
根据上述公式，我们可以直接读出单根 $\alpha_2$ 的表达式。取 $k=2$，我们查看矩阵的第二行 $(-1, 2, -2)$，得到：
$$
\alpha_2 = A_{21}\omega_1 + A_{22}\omega_2 + A_{23}\omega_3 = -\omega_1 + 2\omega_2 - 2\omega_3
$$
这个结果展示了[嘉当矩阵](@entry_id:185184)作为[基变换矩阵](@entry_id:184480)的直接应用 [@problem_id:683131]。同样的方法也适用于任何根，而不仅仅是单根。例如，对于 $A_3$ 代数中的根 $\beta = \alpha_1 + \alpha_2$，其在基本权基下的系数 $c_j$ 可以通过 $\beta$ 的单根展开式 $(n_1, n_2, n_3) = (1, 1, 0)$ 和 $A_3$ 的[嘉当矩阵](@entry_id:185184)计算得出：$c_j = \sum_i n_i A_{ij}$ [@problem_id:682946]。

#### 在根基中表示权

反过来，我们也可以将基本权在单根基中展开。关系式 $\alpha_k = \sum_j A_{kj} \omega_j$ 可以写作矩阵方程 $\vec{\alpha} = A^T \vec{\omega}$。求解 $\vec{\omega}$ 可得 $\vec{\omega} = (A^T)^{-1} \vec{\alpha}$。展开这个[矩阵方程](@entry_id:203695)的第 $i$ 个分量，我们得到：
$$
\omega_i = \sum_{j=1}^r ((A^T)^{-1})_{ij} \alpha_j = \sum_{j=1}^r (A^{-1})_{ji} \alpha_j
$$
这表明，**基本权 $\omega_i$ 在单根基下的坐标由逆[嘉当矩阵](@entry_id:185184) $A^{-1}$ 的第 $i$ 列给出**。这一关系表明，计算基本权在根基下的展开，本质上是一个矩阵求逆问题。

以 $C_3$ 代数（$\mathfrak{sp}(6)$）为例，为了找到 $\omega_2$ 的展开式，我们首先需要计算其[嘉当矩阵](@entry_id:185184)的逆 [@problem_id:683082]。
$$
A = \begin{pmatrix} 2  -1  0 \\ -1  2  -2 \\ 0  -1  2 \end{pmatrix} \quad \implies \quad A^{-1} = \begin{pmatrix} 1  1  1 \\ 1  2  2 \\ 1/2  1  3/2 \end{pmatrix}
$$
根据 $A^{-1}$ 的第二列 $(1, 2, 1)^T$，我们立即得到：
$$
\omega_2 = 1 \cdot \alpha_1 + 2 \cdot \alpha_2 + 1 \cdot \alpha_3 = \alpha_1 + 2\alpha_2 + \alpha_3
$$

### [权空间](@entry_id:195741)的几何学

基本权不仅是一个代数工具，它们还在[权空间](@entry_id:195741) $\mathfrak{h}^*$ 中定义了丰富的几何结构。它们的长度和相互之间的角度，蕴含了[代数表示](@entry_id:143783)的重要信息。

#### 通过逆[嘉当矩阵](@entry_id:185184)计算[内积](@entry_id:158127)

我们可以计算任意两个基本权之间的[内积](@entry_id:158127) $(\omega_i, \omega_j)$。利用关系式 $\omega_i = \sum_k (A^{-1})_{ki} \alpha_k$，我们有：
$$
(\omega_i, \omega_j) = \left( \sum_k (A^{-1})_{ki} \alpha_k, \omega_j \right) = \sum_k (A^{-1})_{ki} (\alpha_k, \omega_j)
$$
再利用对偶性的定义 $(\omega_j, \alpha_k) = \delta_{jk} \frac{(\alpha_k, \alpha_k)}{2}$，上式变为：
$$
(\omega_i, \omega_j) = \sum_k (A^{-1})_{ki} \delta_{jk} \frac{(\alpha_k, \alpha_k)}{2} = (A^{-1})_{ji} \frac{(\alpha_j, \alpha_j)}{2}
$$
对于**单边（simply-laced）**代数（A、D、E系列），所有根的长度都相同。通过归一化，我们可以设 $(\alpha_i, \alpha_i) = 2$ 对所有 $i$ 成立。在这种情况下，公式急剧简化：
$$
(\omega_i, \omega_j) = (A^{-1})_{ji}
$$
由于单边代数的[嘉当矩阵](@entry_id:185184)是对称的，其[逆矩阵](@entry_id:140380)也是对称的，因此 $(A^{-1})_{ji} = (A^{-1})_{ij}$。所以，我们得到一个非常优美的结果：
$$
(\omega_i, \omega_j) = (A^{-1})_{ij} \quad (\text{对于单边代数})
$$
这意味着，对于单边代数，基本权之间的[内积](@entry_id:158127)矩阵就是逆[嘉当矩阵](@entry_id:185184)。这包括了它们的模方 $(\omega_i, \omega_i) = (A^{-1})_{ii}$ 和它们之间的[内积](@entry_id:158127)。

以 $D_4$ 代数（$\mathfrak{so}(8)$）为例，这是一个具有“三位一体”（triality）对称性的单边代数。其[嘉当矩阵](@entry_id:185184)和[逆矩阵](@entry_id:140380)为 [@problem_id:683000]：
$$
A = \begin{pmatrix} 2  -1  0  0 \\ -1  2  -1  -1 \\ 0  -1  2  0 \\ 0  -1  0  2 \end{pmatrix}, \quad A^{-1} = \frac{1}{2} \begin{pmatrix} 2  2  1  1 \\ 2  4  2  2 \\ 1  2  2  1 \\ 1  2  1  2 \end{pmatrix}
$$
（在此约定下，根长平方为 2，故 $(A^{-1})_{ij} = (\omega_i, \omega_j)$）。我们可以直接从 $A^{-1}$ 中读取[旋量](@entry_id:158054)权 $\omega_3$ 和 $\omega_4$ 的[内积](@entry_id:158127)信息：
$$
(\omega_3, \omega_3) = (A^{-1})_{33} = \frac{2}{2} = 1
$$
$$
(\omega_4, \omega_4) = (A^{-1})_{44} = \frac{2}{2} = 1
$$
$$
(\omega_3, \omega_4) = (A^{-1})_{34} = \frac{1}{2}
$$
因此，它们之间夹角的余弦值为 $\cos(\theta_{34}) = \frac{(\omega_3, \omega_4)}{\sqrt{(\omega_3, \omega_3)(\omega_4, \omega_4)}} = \frac{1/2}{1} = \frac{1}{2}$。

#### 在标准正交基中直接计算

对于非单边代数（B、C、F、G 系列），或在处理具体问题时，另一种强大的方法是在一个合适的[标准正交基](@entry_id:147779) $\{e_i\}$ 中直接写出根和权的表达式，然后利用欧几里得[内积](@entry_id:158127)进行计算。

以 $B_n = \mathfrak{so}(2n+1)$ 代数系列为例。在一个 $n$ 维欧几里得空间中，其单根可以表示为 [@problem_id:682982]：
$$
\alpha_i = e_i - e_{i+1} \quad (i=1, \dots, n-1), \quad \alpha_n = e_n
$$
这里，$\alpha_1, \dots, \alpha_{n-1}$ 是长根（模方为 2），$\alpha_n$ 是短根（模方为 1）。我们可以通过求解定义方程 $\frac{2(\omega_i, \alpha_j)}{(\alpha_j, \alpha_j)} = \delta_{ij}$ 来确定基本权的表达式。例如，对于 $B_3 = \mathfrak{so}(7)$ [@problem_id:682974]，[求解方程组](@entry_id:152624)可以得到：
$$
\omega_1 = e_1
$$
$$
\omega_2 = e_1 + e_2
$$
$$
\omega_3 = \frac{1}{2}(e_1 + e_2 + e_3)
$$
一旦有了这些显式表达式，计算它们的[内积](@entry_id:158127)就变得非常简单。例如：
$$
(\omega_1, \omega_2) = (e_1, e_1 + e_2) = (e_1, e_1) + (e_1, e_2) = 1 + 0 = 1
$$
同样，对于一般的 $B_n$ 代数，可以推导出 $\omega_1 = e_1$ 和 $\omega_n = \frac{1}{2}\sum_{i=1}^n e_i$。因此它们的模方为：
$$
(\omega_1, \omega_1) = (e_1, e_1) = 1
$$
$$
(\omega_n, \omega_n) = \frac{1}{4} \left( \sum_{i=1}^n e_i, \sum_{j=1}^n e_j \right) = \frac{1}{4} \sum_{i=1}^n (e_i, e_i) = \frac{n}{4}
$$
这两种方法——抽象的[矩阵求逆](@entry_id:636005)和具体的坐标表示——为理解和计算权的几何性质提供了互补的视角。

### 格子与群中心

单根和基本权各自生成了 $\mathfrak{h}^*$ 中的离散加法[子群](@entry_id:146164)，称为格（lattice）。这两个格之间的关系揭示了代数背后对应李群的深刻结构。

- **根格 (Root Lattice)** $Q$：由单根的所有整系数[线性组合](@entry_id:154743)构成。
  $$ Q = \Lambda_R = \left\{ \sum_{i=1}^r n_i \alpha_i \mid n_i \in \mathbb{Z} \right\} $$
- **[权格](@entry_id:195778) (Weight Lattice)** $P$：由基本权的所有整系数线性组合构成。
  $$ P = \Lambda_W = \left\{ \sum_{i=1}^r m_i \omega_i \mid m_i \in \mathbb{Z} \right\} $$
  [权格](@entry_id:195778)中的元素称为**整权 (integral weights)**。

由于基本权在单根基下的展开系数 $(A^{-1})_{ji}$ 可能是分数，所以[权格](@entry_id:195778)通常比根格更“密集”，即 $Q \subseteq P$。这两个格的[商群](@entry_id:145113) $P/Q$ 是一个[有限阿贝尔群](@entry_id:136632)，它具有重要的拓扑和代数意义：它同构于与李代数 $\mathfrak{g}$ 对应的单连通[紧李群](@entry_id:146703) $G$ 的**中心 (center)** $Z(G)$。
$$
P/Q \cong Z(G)
$$
$P/Q$ 中一个元素 $[\lambda] = \lambda + Q$ 的**阶 (order)** 是指最小的正整数 $k$，使得 $k\lambda \in Q$。换言之，需要将权 $\lambda$ 乘以 $k$ 才能使其成为根的整线性组合。

要计算一个基本权 $\omega_i$ 在 $P/Q$ 中的阶，我们需要找到它在根基下的展开式 $\omega_i = \sum_j b_j \alpha_j$。这些系数 $b_j = (A^{-1})_{ji}$。这个权 $k\omega_i$ 属于根格 $Q$ 的条件是，它的所有展开系数 $kb_j$ 都是整数。因此，$\omega_i$ 的阶就是将所有系数 $b_j$ 变为整数所需的最小正整数 $k$，即这些分数系数分母的最小公倍数。

例如，对于 $D_5$ 代数，我们可以通过[求解线性方程组](@entry_id:169069) $A^T \mathbf{b} = e_1$ 来找到 $\omega_1$ 在根基下的系数 $\mathbf{b}$。计算表明 [@problem_id:682947]：
$$
\omega_1 = \alpha_1 + \alpha_2 + \alpha_3 + \frac{1}{2}\alpha_4 + \frac{1}{2}\alpha_5
$$
由于系数中出现了 $1/2$，为了使 $k\omega_1$ 的所有系数都成为整数， $k$ 必须是 2 的倍数。最小的正整数 $k$ 是 2。因此，$\omega_1$ 在 $P/Q$ 中的阶是 2。

该原理也适用于其他权。例如，对于 $D_5$ 代数中的旋量权 $\omega_5 = \frac{1}{2}(\epsilon_1+\epsilon_2+\epsilon_3+\epsilon_4+\epsilon_5)$ [@problem_id:682977]，我们可以通过检查其倍数是否属于根格来确定其阶。[求解丢番图方程](@entry_id:149511)组可以发现，需要将 $\omega_5$ 乘以 4 才能使其表示为根的整数[线性组合](@entry_id:154743)，因此其阶为 4。

### 对称性与表示

基本权在表示论中的核心地位源于它们作为**最高权 (highest weights)** 的基本构件。一个有限维[不可约表示](@entry_id:263310) $V(\lambda)$ 由其最高权 $\lambda$ 唯一确定。一个权 $\lambda$ 能成为最高权的条件是它必须是**占优整权 (dominant integral weight)**，即它可以写成基本权的非负整系数[线性组合](@entry_id:154743)：
$$
\lambda = \sum_{i=1}^r k_i \omega_i, \quad k_i \in \mathbb{Z}_{\ge 0}
$$
这些系数 $k_i$ 通常被称为**丹金标签 (Dynkin labels)**。

外尔群 (Weyl group) $W$ 是由单根的反射生成的对称性群，它在[权空间](@entry_id:195741)上起作用。外尔群中存在一个唯一的**最长元 (longest element)** $w_0$，它将所有[正根](@entry_id:199264)映射到负根。$w_0$ 对基本权的作用有一个简洁的公式：
$$
w_0(\omega_i) = -\omega_{\sigma(i)}
$$
其中 $\sigma$ 是丹金图的一个[自同构](@entry_id:155390)。对于 $A_n (n > 1)$，$\sigma(i) = n+1-i$；对于 $D_n (n > 4)$，$\sigma$ 交换两个旋量节点；对于 $D_4$，$\sigma$ 是 $S_3$ 群的[置换](@entry_id:136432)（三位一体）；对于 $E_6$，$\sigma$ 是一个对合。对于没有丹金[图对称性](@entry_id:272377)的代数（B、C、F、G系列），$\sigma$ 是恒等映射。

这个性质在研究表示的**[对偶表示](@entry_id:146263) (contragredient representation)** 时至关重要。一个[最高权](@entry_id:202808)为 $\lambda$ 的不可约表示 $V(\lambda)$，其最低权是 $w_0(\lambda)$。其[对偶表示](@entry_id:146263) $V(\lambda)^*$ 也是不可约的，其最高权 $\lambda^*$ 由下式给出：
$$
\lambda^* = -w_0(\lambda)
$$
利用 $w_0$ 作用的线性和它对基本权的作用规则，我们可以轻易地计算出任何表示的[对偶表示](@entry_id:146263)的[最高权](@entry_id:202808)。

考虑 $A_4$ 代数中的一个表示，其最高权为 $\lambda = \omega_1 + 2\omega_3$ [@problem_id:682937]。其[对偶表示](@entry_id:146263)的最高权 $\lambda^*$ 计算如下：
$$
\lambda^* = -w_0(\omega_1 + 2\omega_3) = -w_0(\omega_1) - 2w_0(\omega_3)
$$
对于 $A_4$ ($n=4$)，我们有 $w_0(\omega_i) = -\omega_{5-i}$。因此，$w_0(\omega_1) = -\omega_4$ 且 $w_0(\omega_3) = -\omega_2$。代入得：
$$
\lambda^* = -(-\omega_4) - 2(-\omega_2) = 2\omega_2 + \omega_4
$$
这个例子 [@problem_id:683036] 完美地展示了基本权、外尔[群对称性](@entry_id:147821)以及表示论的对偶性之间深刻而实用的联系。通过基本权的语言，复杂的表示论问题可以被转化为优雅的代数组合学计算。