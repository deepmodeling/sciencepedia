## 引言
单[李代数](@entry_id:137954)与[半单李代数](@entry_id:190073)是数学和理论物理学中最为优美和强大的[代数结构](@entry_id:137052)之一。它们以其高度的对称性和规整性著称，为描述自然界的基本规律提供了精确的语言。从基本粒子的分类方案到时空的几何结构，这些代数的印记无处不在。然而，要从[李代数](@entry_id:137954)的一般定义跨越到对其精细内部构造的深刻理解，需要一套系统而强大的理论工具。本文旨在填补这一知识鸿沟，引领读者深入探索这一迷人的数学领域。

在接下来的内容中，我们将分三个章节展开这场智力之旅。首先，在“原则与机制”一章中，我们将奠定理论基石，介绍用于判别半单性的关键工具——[基灵型](@entry_id:161046)，并详细阐述如何通过根[系统分解](@entry_id:274870)和[最高权理论](@entry_id:191912)来完全刻画这些代数的结构与表示。接着，在“应用与跨学科联系”一章中，我们将把这些抽象的理论与具体实践联系起来，展示它们如何作为核心工具应用于粒子物理学的大统一理论、[微分几何](@entry_id:145818)以及[量子计算](@entry_id:142712)等前沿领域。最后，通过“动手实践”部分，读者将有机会通过解决具体问题来巩固和深化所学知识。现在，让我们从这些[代数结构](@entry_id:137052)的基本原则与内在机制开始。

## 原则与机制

在上一章对李代数的基本概念进行介绍之后，本章将深入探讨一类在数学和物理学中占据核心地位的[代数结构](@entry_id:137052)：单[李代数](@entry_id:137954)与[半单李代数](@entry_id:190073)。这些代数具有高度的对称性和规整性，其内部结构可以通过一套强大而优美的理论进行完全分类和理解。我们将从定义这些代数的基本判据出发，逐步揭示其由根系统所决定的精细构造，并最终探讨其表示理论以及与李群拓扑性质的深刻联系。

### 定义半单性：可解根与[基灵型](@entry_id:161046)

为了精确地定义何为“半单”，我们首先需要引入与之相对的概念：**可解性 (solvability)**。一个李代数 $\mathfrak{g}$ 的 **[导序列](@entry_id:140607) (derived series)** 是通过[递归定义](@entry_id:266613)的子代数序列：$\mathcal{D}^0(\mathfrak{g}) = \mathfrak{g}$ 以及 $\mathcal{D}^{k+1}(\mathfrak{g}) = [\mathcal{D}^k(\mathfrak{g}), \mathcal{D}^k(\mathfrak{g})]$。如果这个序列在有限步后达到零理想 $\{0\}$，即存在某个整数 $n$ 使得 $\mathcal{D}^n(\mathfrak{g}) = \{0\}$，那么我们称 $\mathfrak{g}$ 是一个 **[可解李代数](@entry_id:180318)**。直观上，[可解李代数](@entry_id:180318)是一种可以被“交换化”的[代数结构](@entry_id:137052)，其换[位运算](@entry_id:172125)在反复进行后会最终消失。

在任意一个李代数 $\mathfrak{g}$ 中，所有可解理想的和构成一个唯一的、最大的可解理想，我们称之为 $\mathfrak{g}$ 的 **可解根 (solvable radical)**，记作 $\text{rad}(\mathfrak{g})$。可解根衡量了一个[李代数](@entry_id:137954)“偏离”完全非交换性的程度。

基于此，我们可以给出核心定义：
- 一个[李代数](@entry_id:137954) $\mathfrak{g}$ 如果其可解根为零，即 $\text{rad}(\mathfrak{g}) = \{0\}$，则称其为 **[半单李代数](@entry_id:190073) (semi-simple Lie algebra)**。
- 一个[非交换](@entry_id:136599)的[半单李代数](@entry_id:190073)如果没有任何非平庸的理想（即除了 $\{0\}$ 和其自身外没有其他理想），则称其为 **单[李代数](@entry_id:137954) (simple Lie algebra)**。

一个基本而重要的结构定理指出，任何[半单李代数](@entry_id:190073)都可以分解为其单理想的[直和](@entry_id:156782)。因此，对单李代数的分类是理解所有[半单李代数](@entry_id:190073)的关键。

为了更好地理解半单性的缺失，我们可以考察一个由半单[部分和](@entry_id:162077)可解部分通过 **[半直积](@entry_id:147230) (semidirect product)** 构成的例子。假设 $\mathfrak{h}$ 是一个李代数，$V$ 是一个[向量空间](@entry_id:151108)，同时也是 $\mathfrak{h}$ 的一个表示。[李代数](@entry_id:137954)的[半直积](@entry_id:147230) $\mathfrak{g} = \mathfrak{h} \ltimes V$ 是在[向量空间](@entry_id:151108) $\mathfrak{h} \oplus V$ 上定义的，其李括号为：
$$[(h_1, v_1), (h_2, v_2)] = ([h_1, h_2]_{\mathfrak{h}}, \rho(h_1)v_2 - \rho(h_2)v_1)$$
这里 $V$ 被视为一个交换[李代数](@entry_id:137954)（即 $[v_1, v_2]_V = 0$）。在这种构造中，$V$ 成为了 $\mathfrak{g}$ 的一个交换理想，因此它本身是可解的。如果 $\mathfrak{h}$ 是半单的，那么它不包含任何非零可解理想。可以证明，在这种情况下，$\mathfrak{g}$ 的可解根恰好就是 $V$。例如，考虑[半单李代数](@entry_id:190073) $\mathfrak{h} = \mathfrak{sl}(2, \mathbb{C}) \oplus \mathfrak{sl}(2, \mathbb{C})$，并令 $V = V_1 \otimes V_2$ 是其两个标准二维[表示的张量积](@entry_id:137150)。构造出的李代数 $\mathfrak{g} = \mathfrak{h} \ltimes V$ 就不是半单的，其可解根正是 $V$。由于 $V_1$ 和 $V_2$ 都是二维的，$\text{rad}(\mathfrak{g})$ 的维数是 $\dim(V) = \dim(V_1) \times \dim(V_2) = 2 \times 2 = 4$ [@problem_id:632485]。

虽然可解根的定义在理论上是清晰的，但在实践中验证一个理想是否为最大可解理想却很困难。幸运的是，有一个更为直接和强大的工具——**[基灵型](@entry_id:161046) (Killing form)**。对于[李代数](@entry_id:137954) $\mathfrak{g}$ 中的任意元素 $X$，其 **伴随表示 (adjoint representation)** 是一个线性映射 $\text{ad}_X: \mathfrak{g} \to \mathfrak{g}$，定义为 $\text{ad}_X(Y) = [X, Y]$。[基灵型](@entry_id:161046)是 $\mathfrak{g}$ 上的一个[对称双线性形式](@entry_id:148281)，定义为：
$$
\kappa(X, Y) = \text{tr}(\text{ad}_X \circ \text{ad}_Y)
$$
其中 $\text{tr}$ 表示[线性变换](@entry_id:149133)的迹。

[基灵型](@entry_id:161046)的重要性在于 **Cartan 半单性判据 (Cartan's Criterion for Semi-simplicity)**：一个[李代数](@entry_id:137954) $\mathfrak{g}$ 是半单的当且仅当它的[基灵型](@entry_id:161046)是 **非退化 (non-degenerate)** 的。非退化意味着如果对于所有的 $Y \in \mathfrak{g}$ 都有 $\kappa(X, Y) = 0$，那么必然有 $X=0$。这为我们提供了一个具体的计算方法来判断半单性。

计算[基灵型](@entry_id:161046)的值需要选取一个基。例如，考虑 $\mathfrak{g} = \mathfrak{sl}(3, \mathbb{C})$，其由所有 $3 \times 3$ 的无迹[复矩阵](@entry_id:190650)构成。对角子代数（即 **Cartan 子代数**）中的一个元素 $H = E_{11} - E_{22}$，其[基灵型](@entry_id:161046)范数 $\kappa(H, H)$ 可以通过计算 $\text{ad}_H \circ \text{ad}_H$ 的迹得到。算子 $\text{ad}_H$ 在 $\mathfrak{g}$ 的基上是对角的，其[特征值](@entry_id:154894)是 $\alpha(H)$，其中 $\alpha$ 是[李代数的根](@entry_id:190590)。具体而言，$\text{ad}_H$ 在根向量 $E_{ij}$ ($i \neq j$) 上的作用是 $[H, E_{ij}] = (H_{ii} - H_{jj}) E_{ij}$。因此，$\text{ad}_H$ 在 $E_{ij}$ 上的[特征值](@entry_id:154894)为 $\lambda_{ij} = H_{ii} - H_{jj}$。$\kappa(H, H)$ 就是这些[特征值](@entry_id:154894)的平方和：
$$
\kappa(H, H) = \text{tr}(\text{ad}_H^2) = \sum_{\alpha \in \Phi} \alpha(H)^2
$$
对于 $H = E_{11} - E_{22}$，其在 $\mathfrak{sl}(3, \mathbb{C})$ 的根向量上的[特征值](@entry_id:154894)为 $\pm 2, \pm 1, \pm 1$。在 Cartan 子代数本身上，$\text{ad}_H$ 的作用为零。因此，$\kappa(H, H) = 2^2 + (-2)^2 + 1^2 + (-1)^2 + 1^2 + (-1)^2 = 12$ [@problem_id:773748]。

对于实[李代数](@entry_id:137954)，[基灵型](@entry_id:161046)的 **符号差 (signature)** 提供了更精细的结构信息。任何实[半单李代数](@entry_id:190073) $\mathfrak{g}$ 都有一个 **Cartan 分解** $\mathfrak{g} = \mathfrak{k} \oplus \mathfrak{p}$，其中 $\mathfrak{k}$ 是一个紧致子代数，$\mathfrak{p}$ 是一个[向量空间](@entry_id:151108)。[基灵型](@entry_id:161046)在 $\mathfrak{k}$ 上是负定的，在 $\mathfrak{p}$ 上是正定的。因此，[基灵型](@entry_id:161046)正[特征值](@entry_id:154894)的数量 $n_+$ 等于 $\dim(\mathfrak{p})$，负[特征值](@entry_id:154894)的数量 $n_-$ 等于 $\dim(\mathfrak{k})$。例如，对于 $B_2$ 型复单[李代数](@entry_id:137954)的[分裂实形式](@entry_id:181390) $\mathfrak{g} = \mathfrak{so}(3,2)$，其 Cartan 分解对应于 $\mathfrak{k} = \mathfrak{so}(3) \oplus \mathfrak{so}(2)$ 和 $\mathfrak{p}$，维度分别为 $\dim(\mathfrak{k}) = 3+1=4$ 和 $\dim(\mathfrak{p}) = 6$。因此，[基灵型](@entry_id:161046)的符号差为 $n_+ - n_- = 6 - 4 = 2$ [@problem_id:773943]。

### 根系统：[半单代数](@entry_id:139931)的分解

[基灵型](@entry_id:161046)的非退化性是解锁[半单李代数](@entry_id:190073)详细结构的钥匙。它保证了 **Cartan 子代数 (Cartan subalgebra)** $\mathfrak{h}$ 的存在，这是一个极大[交换子代数](@entry_id:143966)，且其中所有元素的伴随表示都是半单的（可对角化）。

由于 $\mathfrak{h}$ 中所有元素的伴随表示 $\text{ad}_H$ 相互交换，它们可以被[同时对角化](@entry_id:196036)。这意味着整个[李代数](@entry_id:137954) $\mathfrak{g}$ 可以被分解为这些算子的共同特征[子空间之和](@entry_id:180324)。这个分解称为 **[根空间分解](@entry_id:185263) (root space decomposition)**：
$$
\mathfrak{g} = \mathfrak{h} \oplus \bigoplus_{\alpha \in \Phi} \mathfrak{g}_\alpha
$$
这里，$\Phi$ 是 $\mathfrak{h}$ 的对偶空间 $\mathfrak{h}^*$ 中的一个非零向量集合，称为 **[根系](@entry_id:198970)统 (root system)**。每个 **根 (root)** $\alpha \in \Phi$ 都是一个线性泛函 $\alpha: \mathfrak{h} \to \mathbb{C}$。对应的 **根空间 (root space)** $\mathfrak{g}_\alpha$ 定义为：
$$
\mathfrak{g}_\alpha = \{X \in \mathfrak{g} \mid [H, X] = \alpha(H)X \text{ for all } H \in \mathfrak{h}\}
$$
对于复[半单李代数](@entry_id:190073)，所有根空间 $\mathfrak{g}_\alpha$ 都是一维的。根系统 $\Phi$ 并不依赖于 Cartan 子代数的具体选择，它完全由李代数本身决定，并编码了代数的所有结构信息。

根系统具有高度的几何对称性。我们可以选择一个超平面，将 $\Phi$ 分为两部分：**[正根](@entry_id:199264) (positive roots)** $\Phi^+$ 和 **负根 (negative roots)** $\Phi^-$。[正根](@entry_id:199264)中不能表示为另外两个[正根](@entry_id:199264)之和的根，构成了 **单根 (simple roots)** 的集合 $\Pi = \{\alpha_1, \dots, \alpha_n\}$，其中 $n$ 是代数的 **秩 (rank)**，即 $\dim(\mathfrak{h})$。所有根都可以表示为单根的整系数[线性组合](@entry_id:154743)，且对于[正根](@entry_id:199264)，系数均为非负整数。

例如，对于 $D_5 \cong \mathfrak{so}(10, \mathbb{C})$，其秩为 5。根可以用 $\mathfrak{h}^*$ 的一个[标准正交基](@entry_id:147779) $\{L_i\}_{i=1}^5$ 来表示，形式为 $\pm L_i \pm L_j$ 其中 $1 \le i  j \le 5$。如果我们定义一个根为[正根](@entry_id:199264)，当其在基 $\{L_i\}$ 下展开的第一个非零系数为正，那么[正根](@entry_id:199264)集就是 $\{L_i \pm L_j \mid 1 \le i  j \le 5\}$。组合的选择数是 $\binom{5}{2} = 10$，每对组合有两种符号选择（$L_i+L_j$ 和 $L_i-L_j$），所以[正根](@entry_id:199264)的总数是 $2 \times 10 = 20$ [@problem_id:773918]。

[根系](@entry_id:198970)统的几何结构（根之间的夹角和相对长度）可以通过 **Cartan 矩阵** $A$ 来代数化。这是一个 $n \times n$ 矩阵，其元素由单根之间的[内积](@entry_id:158127)（由[基灵型](@entry_id:161046)诱导）定义：
$$
A_{ij} = \frac{2 \langle \alpha_i, \alpha_j \rangle}{\langle \alpha_j, \alpha_j \rangle}
$$
Cartan 矩阵的元素都是整数，并且完全决定了李代数的类型（如 $A_n, B_n, C_n, D_n$ 或例外类型）。例如，如果我们已知一个秩为 3 的单[李代数](@entry_id:137954)的单根[内积](@entry_id:158127)，就可以构建其 Cartan 矩阵。假设单根为 $\{\alpha_1, \alpha_2, \alpha_3\}$，[内积](@entry_id:158127)为 $(\alpha_1, \alpha_1) = 2, (\alpha_2, \alpha_2) = 2, (\alpha_3, \alpha_3) = 4$ 以及 $(\alpha_1, \alpha_2) = -1, (\alpha_1, \alpha_3) = 0, (\alpha_2, \alpha_3) = -2$。根据定义，我们可以计算出 Cartan 矩阵为：
$$
A = \begin{pmatrix} 2   -1  0 \\ -1  2  -1 \\ 0  -2  2 \end{pmatrix}
$$
这个矩阵对应于 $C_3$ 型[李代数](@entry_id:137954) [@problem_id:773734]。

### 从结构到表示

[半单李代数](@entry_id:190073)的优美结构为其表示理论提供了坚实的基础。一个[李代数](@entry_id:137954) $\mathfrak{g}$ 在[向量空间](@entry_id:151108) $V$ 上的 **表示 (representation)** 是一个[李代数](@entry_id:137954)同态 $\rho: \mathfrak{g} \to \mathfrak{gl}(V)$。与[根空间分解](@entry_id:185263)类似，对于一个表示 $V$，我们也可以根据 Cartan 子代数 $\mathfrak{h}$ 的作用将其分解：
$$
V = \bigoplus_{\lambda \in P(V)} V_\lambda
$$
其中 $V_\lambda = \{v \in V \mid H \cdot v = \lambda(H) v \text{ for all } H \in \mathfrak{h}\}$ 是对应于 **权 (weight)** $\lambda \in \mathfrak{h}^*$ 的 **[权空间](@entry_id:195741) (weight space)**。$P(V)$ 是该表示的所有权的集合。

对于有限维不可约表示，存在一个唯一的“最高”的权，称为 **[最高权](@entry_id:202808) (highest weight)** $\Lambda$。这个表示完全由其最高权确定，记为 $V(\Lambda)$。一个权 $\Lambda$ 能成为某个有限维不可约表示的[最高权](@entry_id:202808)，当且仅当它是一个 **支配整权 (dominant integral weight)**，这意味着它在所有单根的对偶基（即 **基本权 (fundamental weights)**）下的展开系数都是非负整数。

[基本权](@entry_id:200855) $\{\omega_i\}_{i=1}^n$ 是[权空间](@entry_id:195741)中的一个特殊基，它与单根构成的 **单[余根](@entry_id:193338) (simple coroots)** $\alpha_j^\vee = \frac{2\alpha_j}{\langle \alpha_j, \alpha_j \rangle}$ 是对偶的，满足关系 $\langle \omega_i, \alpha_j^\vee \rangle = \delta_{ij}$。

一个核心的工具是 **Weyl 维数公式 (Weyl dimension formula)**，它给出了具有[最高权](@entry_id:202808) $\Lambda$ 的不可约表示 $V(\Lambda)$ 的维数：
$$
\dim V(\Lambda) = \prod_{\alpha \in \Phi^+} \frac{\langle \Lambda + \rho, \alpha \rangle}{\langle \rho, \alpha \rangle}
$$
其中 $\Phi^+$ 是[正根](@entry_id:199264)集，而 **Weyl 向量** $\rho$ 定义为所有[正根](@entry_id:199264)之和的一半，它也等于所有[基本权](@entry_id:200855)之和，即 $\rho = \frac{1}{2} \sum_{\alpha \in \Phi^+} \alpha = \sum_{i=1}^n \omega_i$。

为了应用此公式，我们需要知道根与权之间的[内积](@entry_id:158127)。例如，对于 $B_2$ 型[李代数](@entry_id:137954)，其[正根](@entry_id:199264)为 $\{\alpha_1, \alpha_2, \alpha_1+\alpha_2, \alpha_1+2\alpha_2\}$。设我们要计算最高权为 $\Lambda = 2\omega_2$ 的表示的维数。首先，我们计算 $\Lambda + \rho = \omega_1 + 3\omega_2$。然后，利用对偶关系 $2\frac{\langle \omega_i, \alpha_j \rangle}{\langle \alpha_j, \alpha_j \rangle} = \delta_{ij}$，我们可以计算出 $\langle \Lambda + \rho, \alpha \rangle$ 和 $\langle \rho, \alpha \rangle$ 对每个[正根](@entry_id:199264) $\alpha$ 的值。将这些值代入 Weyl 维数公式，经过计算可得 $\dim V(2\omega_2) = 10$ [@problem_id:773774]。

伴随表示本身就是一个重要的不可约表示，其权就是根系统的根（以及零权）。伴随表示的最高权正是李代数的 **[最高根](@entry_id:183719) (highest root)** $\theta$，即在单根基下系数之和最大的[正根](@entry_id:199264)。例如，对于 $A_3 \cong \mathfrak{sl}(4, \mathbb{C})$，其[最高根](@entry_id:183719)是 $\theta = \alpha_1+\alpha_2+\alpha_3$。我们可以通过 Cartan 矩阵将其表示为[基本权](@entry_id:200855)的线性组合。利用 $A_3$ 和 $D_3$ 之间的例外同构 $\mathfrak{sl}(4, \mathbb{C}) \cong \mathfrak{so}(6, \mathbb{C})$，我们可以推断出 $\mathfrak{so}(6, \mathbb{C})$ 的伴随表示对应于 $\mathfrak{sl}(4, \mathbb{C})$ 中[最高权](@entry_id:202808)为 $\theta = \omega_1 + \omega_3$ 的表示 [@problem_id:773848]。

### 重要的子结构与分解

[半单李代数](@entry_id:190073)的内部结构不仅体现在[根系](@entry_id:198970)统上，也体现在其丰富的子[代数结构](@entry_id:137052)中。

首先，如前所述，[半单李代数](@entry_id:190073)的核心分解性质是它可以写成单理想的[直和](@entry_id:156782)：$\mathfrak{g} = \mathfrak{g}_1 \oplus \dots \oplus \mathfrak{g}_k$。这意味着代数的操作可以分别在每个单分量上进行。这个性质直接反映在表示理论上：$\mathfrak{g}$ 的一个不可约表示是其各单分量不可约[表示的[张量](@entry_id:137150)积](@entry_id:140694)，$V \cong V_1 \otimes \dots \otimes V_k$。一个经典的例子是 $\mathfrak{so}(4, \mathbb{C}) \cong \mathfrak{sl}(2, \mathbb{C}) \oplus \mathfrak{sl}(2, \mathbb{C})$。$\mathfrak{so}(4, \mathbb{C})$ 的不可约表示由一对半整数 $(j_1, j_2)$ 标记，对应于两个 $\mathfrak{sl}(2, \mathbb{C})$ 分量的自旋 $j_1$ 和 $j_2$ [表示的张量积](@entry_id:137150)。该代数的 **二次 Casimir 算子** $C_2$ 的总[特征值](@entry_id:154894)也是两个分量 Casimir [特征值](@entry_id:154894)之和：$c_{j_1, j_2} = j_1(j_1+1) + j_2(j_2+1)$ [@problem_id:773824]。

对于更一般的李代数，**Levi-Mal'cev 定理** 表明，任何有限维[李代数](@entry_id:137954) $\mathfrak{g}$ 都可以分解为其可解根 $\text{rad}(\mathfrak{g})$ 和一个半单子代数 $\mathfrak{l}$（称为 **Levi 因子**）的[半直积](@entry_id:147230)：$\mathfrak{g} = \mathfrak{l} \ltimes \text{rad}(\mathfrak{g})$。这为研究一般李代数提供了一个清晰的路径：将其分解为半单[部分和](@entry_id:162077)可解部分。

在[半单李代数](@entry_id:190073)内部，还存在一类重要的子代数，称为 **[抛物子代数](@entry_id:189305) (parabolic subalgebras)**。它们是包含 **Borel 子代数**（极大可解子代数）的子代数。每个[抛物子代数](@entry_id:189305) $\mathfrak{p}$ 也承认一个 **Levi 分解** $\mathfrak{p} = \mathfrak{l} \ltimes \mathfrak{n}$，其中 $\mathfrak{l}$ 是一个（通常是半单的）**Levi 子代数**，而 $\mathfrak{n}$ 是一个[幂零理想](@entry_id:155673)，称为 **[幂零根](@entry_id:155268) (nilradical)**。在矩阵表示中，这种分解通常具有直观的[块矩阵](@entry_id:148435)形式。例如，在 $\mathfrak{sl}(4, \mathbb{C})$ 中，与选择单根[子集](@entry_id:261956) $J = \{\alpha_1, \alpha_3\}$ 相关联的[抛物子代数](@entry_id:189305)，其 Levi 因子 $\mathfrak{l}_J$ 由[块对角矩阵](@entry_id:145530)构成，而[幂零根](@entry_id:155268) $\mathfrak{n}$ 则由严格的块[上三角矩阵](@entry_id:150931)构成。对于一个给定的矩阵，我们可以通过将其投影到这些块上，唯一地分解为 Levi [部分和](@entry_id:162077)幂零部分 [@problem_id:773743]。

### 格、群与中心

[李代数的根](@entry_id:190590)和权不仅仅是[向量空间](@entry_id:151108)中的向量，它们还形成了离散的格结构。由单根的所有整系数线性组合构成的格称为 **根格 (root lattice)** $Q$，而由[基本权](@entry_id:200855)的所有整系数线性组合构成的格称为 **[权格](@entry_id:195778) (weight lattice)** $P$。

显然，每个单根都可以写成基本权的整系数线性组合，因此根格总是[权格](@entry_id:195778)的一个子格，$Q \subseteq P$。这两个格之间的关系蕴含了深刻的拓扑信息。[商群](@entry_id:145113) $P/Q$ 是一个有限[交换群](@entry_id:145145)，它同构于与[李代数](@entry_id:137954) $\mathfrak{g}$ 相关联的单连通[紧李群](@entry_id:146703) $G$ 的 **中心 (center)** $Z(G)$。这个群也被称为代数的 **基本群 (fundamental group)**。

这个[有限群](@entry_id:139710)的阶可以通过一个纯代数的方法计算：它等于 Cartan 矩阵 $A$ 的[行列式](@entry_id:142978)的[绝对值](@entry_id:147688)，即 $|P/Q| = |\det(A)|$。例如，对于 $B_3$ 型李代数（对应于李群 $SO(7)$），其 Cartan 矩阵为：
$$
A = \begin{pmatrix} 2  -1  0 \\ -1  2  -2 \\ 0  -1  2 \end{pmatrix}
$$
通过直接计算，我们得到 $\det(A) = 2$。因此，与 $B_3$ 关联的单连通[群的中心](@entry_id:141952)是一个二阶循环群 $\mathbb{Z}_2$ [@problem_id:773787]。这一结果完美地展示了[李代数](@entry_id:137954)的内在[代数结构](@entry_id:137052)（由 Cartan 矩阵编码）如何决定了相应李群的全局[拓扑性质](@entry_id:141605)。

综上所述，[半单李代数](@entry_id:190073)的理论通过 Cartan 判据、[根系](@entry_id:198970)统、[最高权表示](@entry_id:184031)和各种结构分解，构建了一个完整而自洽的框架。这个框架不仅使得对这些代数进行完全分类成为可能，而且为它们在现代物理学和几何学中的广泛应用奠定了坚实的数学基础。