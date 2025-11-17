## 引言
李代数的[最高权表示](@entry_id:184031)理论是现代数学与理论物理学的基石之一，它为理解对称性的深刻结构提供了一套极其优美和强大的语言。尤其对于物理学中无处不在的[半单李代数](@entry_id:190073)，其表示（即对称性的具体实现方式）的行为似乎纷繁复杂。如何系统地分类并理解这些表示，构成了[表示论](@entry_id:137998)中的一个核心问题，也是本文章旨在解决的知识鸿沟。

通过本文的学习，读者将全面掌握这一理论的精髓。我们将从第一章“原理与机制”开始，深入[李代数](@entry_id:137954)的心脏，揭示其[根空间分解](@entry_id:185263)和三角分解等内部结构，并在此基础上精确定义最高权、[最高权向量](@entry_id:199275)以及[最高权表示](@entry_id:184031)，最终通向辉煌的[最高权](@entry_id:202808)分类定理。接着，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将走出纯粹的代数领域，探索该理论如何在粒子物理的[对称性破缺](@entry_id:158994)、[共形场论](@entry_id:145449)的动力学结构以及代数组合学的计数问题中发挥关键作用，展示其作为通用工具的强大生命力。最后，第三章“动手实践”将通过具体的计算问题，帮助读者将抽象的理论转化为可操作的技能。让我们一同开始这段探索之旅，揭开[最高权表示](@entry_id:184031)理论的神秘面纱。

## 原理与机制

在上一章对[李代数表示论](@entry_id:190569)的背景进行初步介绍之后，本章将深入探讨其核心——[最高权表示](@entry_id:184031)理论的原理与机制。对于复[半单李代数](@entry_id:190073)，其有限维不可约表示有一个极其优美和完整的[分类理论](@entry_id:153976)，这一理论完全建立在最高权的概念之上。我们将系统地构建这一理论框架，从基本的[代数结构](@entry_id:137052)出发，定义[最高权表示](@entry_id:184031)，阐述其分类定理，并介绍一系列用于刻画这些表示的关键工具和计算公式。

### 李代数的结构基础

在讨论表示之前，我们必须首先明确复[半单李代数](@entry_id:190073) $\mathfrak{g}$ 自身的精细结构。这个结构是[表示论](@entry_id:137998)得以建立的基石。

#### [嘉当子代数](@entry_id:191259)与[根空间分解](@entry_id:185263)

理论的核心始于**[嘉当子代数](@entry_id:191259) (Cartan subalgebra)** $\mathfrak{h}$ 的选取。这是一个最大[交换子代数](@entry_id:143966)，其所有元素在 $\mathfrak{g}$ 的伴随作用下都是半单的。一旦选定 $\mathfrak{h}$，整个[李代数](@entry_id:137954) $\mathfrak{g}$ 可以被分解为相对于 $\mathfrak{h}$ 的共同特征[子空间之和](@entry_id:180324)。具体而言，我们有**[根空间分解](@entry_id:185263) (root space decomposition)**：
$$
\mathfrak{g} = \mathfrak{h} \oplus \bigoplus_{\alpha \in \Phi} \mathfrak{g}_{\alpha}
$$
这里，$\Phi$ 是 $\mathfrak{h}$ 的对偶空间 $\mathfrak{h}^*$ 中的一个非[零向量](@entry_id:156189)集合，称为**根 (roots)**。每一个根 $\alpha \in \Phi$ 都定义了一个一维的**根空间 (root space)** $\mathfrak{g}_{\alpha}$，其定义为：
$$
\mathfrak{g}_{\alpha} = \{ X \in \mathfrak{g} \mid [H, X] = \alpha(H)X \text{ for all } H \in \mathfrak{h} \}
$$
其中 $[H, X]$ 是 $\mathfrak{g}$ 中的李括号。换言之，$\mathfrak{h}$ 中的元素同时对所有根空间 $\mathfrak{g}_{\alpha}$ 起[对角化](@entry_id:147016)作用，其[特征值](@entry_id:154894)即为根 $\alpha$。

#### 序的引入：波莱尔子代数与三角分解

根集 $\Phi$ 本身不具有内在的序结构。为了定义“最高”或“最低”的概念，我们必须在[权空间](@entry_id:195741) $\mathfrak{h}^*$ 中引入一个序。这通过选取一个**波莱尔子代数 (Borel subalgebra)** $\mathfrak{b}$ 来实现。波莱尔子代数是 $\mathfrak{g}$ 的一个极大可解子代数。对于我们的目的，我们总是选取包含我们已选定的[嘉当子代数](@entry_id:191259) $\mathfrak{h}$ 的波莱尔子代数。

这个选择等价于将根集 $\Phi$ 分裂为两个不相交的[子集](@entry_id:261956)：**[正根](@entry_id:199264) (positive roots)** $\Phi^+$ 和**负根 (negative roots)** $\Phi^-$，满足 $\Phi^- = -\Phi^+$。一旦确定了[正根](@entry_id:199264)集 $\Phi^+$，我们就可以定义两个重要的幂零子代数：
$$
\mathfrak{n}_{+} = \bigoplus_{\alpha \in \Phi^{+}} \mathfrak{g}_{\alpha} \quad \text{和} \quad \mathfrak{n}_{-} = \bigoplus_{\alpha \in \Phi^{-}} \mathfrak{g}_{\alpha}
$$
$\mathfrak{n}_{+}$ 是波莱尔子代数 $\mathfrak{b}$ 的[幂零根](@entry_id:155268)基，且 $\mathfrak{b} = \mathfrak{h} \oplus \mathfrak{n}_{+}$。这一系列定义最终引出了[李代数](@entry_id:137954)的**三角分解 (triangular decomposition)**：
$$
\mathfrak{g} = \mathfrak{n}_{-} \oplus \mathfrak{h} \oplus \mathfrak{n}_{+}
$$
这个分解是[最高权理论](@entry_id:191912)的代数基础，因为它将代数分解为“下降算子”($\mathfrak{n}_{-}$)、“[对角算子](@entry_id:262993)”($\mathfrak{h}$)和“上升算子”($\mathfrak{n}_{+}$)三部分。因此，[最高权表示](@entry_id:184031)的概念总是相对于一个给定的波莱尔子代数（或等价地，一个[正根](@entry_id:199264)系的选择）来定义的 [@problem_id:3031876]。

#### [根系](@entry_id:198970)、单根与[嘉当矩阵](@entry_id:185184)

在[正根](@entry_id:199264)集 $\Phi^+$ 中，存在一个特殊的[子集](@entry_id:261956)，称为**单根 (simple roots)**，记为 $\Delta = \{\alpha_1, \dots, \alpha_r\}$，其中 $r$ 是 $\mathfrak{g}$ 的**秩 (rank)**（即 $\mathfrak{h}$ 的维数）。单根集的关键性质是，每一个[正根](@entry_id:199264)都可以唯一地表示为单根的非负整系数[线性组合](@entry_id:154743)。

根系的几何结构由单根之间的[内积](@entry_id:158127)关系完全决定。这些信息被编码在一个称为**[嘉当矩阵](@entry_id:185184) (Cartan matrix)** $A$ 的 $r \times r$ 矩阵中，其元素定义为：
$$
A_{ij} = \frac{2 \langle \alpha_i, \alpha_j \rangle}{\langle \alpha_j, \alpha_j \rangle}
$$
其中 $\langle \cdot, \cdot \rangle$ 是由[基灵型](@entry_id:161046)诱导的[内积](@entry_id:158127)。[嘉当矩阵](@entry_id:185184)的整数元和特定结构（例如 $A_{ii}=2$，$A_{ij} \le 0$ for $i \ne j$）极大地限制了可能的[根系](@entry_id:198970)类型，并最终导向了单李代数的分类。

例如，对于秩为3的[辛李代数](@entry_id:190736) $\mathfrak{sp}(6, \mathbb{C})$（类型 $C_3$），其龙金图 (Dynkin diagram) 为 $\alpha_1 - \alpha_2 \Leftarrow \alpha_3$。根据图的规则，我们可以构建其[嘉当矩阵](@entry_id:185184)。节点 $i$ 和 $j$ 之间由 $N$ 条线连接意味着 $A_{ij}A_{ji}=N$。箭头从较长的根指向较短的根，且 $|A_{ij}|$ 等于连接数（如果箭头从 $i$ 指向 $j$）。由此可得：
$$
A=\begin{pmatrix} 2   -1   0 \\ -1   2  -1 \\ 0   -2   2 \end{pmatrix}
$$
这个[矩阵的行列式](@entry_id:148198)是一个重要的[不变量](@entry_id:148850)。通过沿第一行展开，我们计算得：
$$
\det A = 2 \det\begin{pmatrix} 2   -1 \\ -2   2 \end{pmatrix} - (-1) \det\begin{pmatrix} -1  -1 \\ 0    2 \end{pmatrix} = 2(4-2) + (-2) = 4 - 2 = 2
$$
这个简单的计算展示了如何从[根系](@entry_id:198970)的组合数据中提取出代数的深刻属性 [@problem_id:703566]。

### [最高权表示](@entry_id:184031)的核心理论

有了[李代数](@entry_id:137954)的结构基础，我们现在可以精确定义[最高权表示](@entry_id:184031)。

#### [最高权表示](@entry_id:184031)的定义

令 $V$ 是一个 $\mathfrak{g}$-模。如果 $V$ 中存在一个非[零向量](@entry_id:156189) $v_0$，称为**[最高权向量](@entry_id:199275) (highest weight vector)**，满足以下三个条件，则称 $V$ 是一个**[最高权表示](@entry_id:184031) (highest weight representation)**：
1.  $v_0$ 是 $\mathfrak{h}$ 的共同[特征向量](@entry_id:151813)。即存在一个线性泛函 $\lambda \in \mathfrak{h}^*$，称为**最高权 (highest weight)**，使得对于所有 $H \in \mathfrak{h}$，都有 $H \cdot v_0 = \lambda(H) v_0$。
2.  $v_0$ 被所有[正根](@entry_id:199264)空间构成的子代数 $\mathfrak{n}_{+}$ 湮灭。即对于所有 $X \in \mathfrak{n}_{+}$，都有 $X \cdot v_0 = 0$。
3.  整个表示空间 $V$ 是由 $v_0$ 在 $\mathfrak{g}$ 的作用下生成的。即 $V = U(\mathfrak{g}) \cdot v_0$，其中 $U(\mathfrak{g})$ 是 $\mathfrak{g}$ 的普适包络代数。

这个定义是[最高权理论](@entry_id:191912)的基石。[最高权向量](@entry_id:199275)在某种意义上是表示中的“最顶层”向量，它被所有“上升算子”$\mathfrak{g}_\alpha, \alpha \in \Phi^+$ 送到零，而整个表示空间则通过向它施加“下降算子”$\mathfrak{g}_\alpha, \alpha \in \Phi^-$ 来构建 [@problem_id:3031876]。

#### 有限维不可约表示的分类

[最高权理论](@entry_id:191912)最辉煌的成就是它对复[半单李代数](@entry_id:190073)的有限维[不可约表示](@entry_id:263310)给出了一个完全的分类。**最高权定理 (Theorem of the Highest Weight)** 指出：
1.  任何一个有限维不可约 $\mathfrak{g}$-模都是一个[最高权](@entry_id:202808)模。
2.  其最高权 $\lambda$ 必定是**主整权 (dominant integral weight)**。**整性 (integrality)** 意味着 $\lambda$ 在所有单根对应的[余根](@entry_id:193338) $h_i$ 上的取值都是整数，即 $\lambda(h_i) \in \mathbb{Z}$。**主性 (dominance)** 意味着这些整数都是非负的，即 $\lambda(h_i) \ge 0$ for all $i=1, \dots, r$。
3.  两个有限维不可约表示是同构的，当且仅当它们的[最高权](@entry_id:202808)相同。
4.  对于每一个主整权 $\lambda$，都存在一个唯一的（在同构意义下）有限维不可约表示 $L(\lambda)$，其最高权为 $\lambda$。

这个定理建立了一一对应关系：有限维[不可约表示](@entry_id:263310)的[同构类](@entry_id:147854) $\longleftrightarrow$ 主整权 [@problem_id:3031876]。

#### [基本权](@entry_id:200855)与[权格](@entry_id:195778)

为了方便地描述所有主整权，我们引入**[基本权](@entry_id:200855) (fundamental weights)** $\{\omega_1, \dots, \omega_r\}$。它们构成了[权空间](@entry_id:195741)的一组基，其定义与单根对偶：
$$
\frac{2\langle \omega_i, \alpha_j \rangle}{\langle \alpha_j, \alpha_j \rangle} = \omega_i(h_j) = \delta_{ij}
$$
其中 $\delta_{ij}$ 是克罗内克符号。根据这个定义，一个权 $\Lambda = \sum_{i=1}^r c_i \omega_i$ 是主整权，当且仅当所有系数 $c_i$ 都是非负整数。

#### 一个重要的例子：伴随表示

[李代数](@entry_id:137954) $\mathfrak{g}$ 本身可以看作一个表示空间，其作用由李括号定义，即 $X \cdot Y = [X, Y]$。这称为**伴随表示 (adjoint representation)**。它的非零权恰好是根集 $\Phi$。伴随表示的[最高权](@entry_id:202808)是[根系](@entry_id:198970)中的**[最高根](@entry_id:183719) (highest root)** $\theta$，即在由[正根](@entry_id:199264)定义的偏序下的[最大元](@entry_id:276547)。

作为一个具体的例子，我们来确定 $\mathfrak{g} = \mathfrak{sp}(6, \mathbb{C})$ (类型 $C_3$) 的伴随表示的最高权。其单根为 $\alpha_1 = e_1 - e_2, \alpha_2 = e_2 - e_3, \alpha_3 = 2e_3$，[最高根](@entry_id:183719)为 $\theta = 2e_1$。我们需要将 $\theta$ 表示为[基本权](@entry_id:200855)的线性组合。首先，通过对偶关系计算出基本权：
$\omega_1 = e_1$
$\omega_2 = e_1 + e_2$
$\omega_3 = e_1 + e_2 + e_3$
现在，我们求解方程 $\theta = c_1 \omega_1 + c_2 \omega_2 + c_3 \omega_3$：
$2e_1 = c_1 e_1 + c_2 (e_1+e_2) + c_3 (e_1+e_2+e_3)$
比较 $e_1, e_2, e_3$ 的系数，得到[方程组](@entry_id:193238) $c_1+c_2+c_3=2, c_2+c_3=0, c_3=0$，解得 $c_1=2, c_2=0, c_3=0$。因此，伴随表示的[最高权](@entry_id:202808)为 $\lambda_{adj} = \theta = 2\omega_1$ [@problem_id:703531]。

### 普适构造：维尔马模

对于任意给定的权 $\lambda \in \mathfrak{h}^*$（不一定是主整权），是否存在一个“最大”的、以 $\lambda$ 为[最高权](@entry_id:202808)的模？答案是肯定的，这就是**维尔马模 (Verma module)**。

#### 定义与普适性质

维尔马模 $M(\lambda)$ 可以通过[诱导表示](@entry_id:136842)来构造。令 $\mathbb{C}_\lambda$ 是一个一维的波莱尔子代数 $\mathfrak{b}$-模，其中 $\mathfrak{h}$ 按权 $\lambda$ 作用，而 $\mathfrak{n}_+ = [\mathfrak{b}, \mathfrak{b}]$ 作用为零。则维尔马模定义为：
$$
M(\lambda) = U(\mathfrak{g}) \otimes_{U(\mathfrak{b})} \mathbb{C}_{\lambda}
$$
维尔马模具有重要的**普适性质**：任何一个[最高权](@entry_id:202808)为 $\lambda$ 的 $\mathfrak{g}$-模，都是 $M(\lambda)$ 的一个[商模](@entry_id:155903)。这意味着 $M(\lambda)$ 包含了所有关于最高权为 $\lambda$ 的表示的全部信息。特别地，不可约模 $L(\lambda)$ 是 $M(\lambda)$ 对其唯一的极大真[子模](@entry_id:148922)的商 [@problem_id:3031876]。

#### 维尔马模的结构与可约性

维尔马模并非总是不可约的。它的可约性由一个深刻的准则判定。定义**[移位](@entry_id:145848)作用 (dot action)** 为 $w \cdot \lambda = w(\lambda + \rho) - \rho$，其中 $\rho$ 是外尔向量（见后文），$w$ 是外尔群中的元素。一个关键结果是，如果对于某个[正根](@entry_id:199264) $\beta \in \Phi^+$，$(\lambda + \rho)(h_\beta)$ 是一个正整数，那么 $M(\lambda)$ 是可约的，并且它包含一个最高权为 $s_\beta \cdot \lambda$ 的[子模](@entry_id:148922)，其中 $s_\beta$ 是对应于根 $\beta$ 的反射。

我们以 $\mathfrak{g} = \mathfrak{sl}(3, \mathbb{C})$ (类型 $A_2$) 为例，考察最高权为 $\lambda = -\alpha_1$ 的维尔马模 $M(-\alpha_1)$ 的结构。首先，计算移位的权 $\lambda+\rho$。对于 $A_2$，$\rho = \alpha_1+\alpha_2$，所以 $\lambda+\rho = -\alpha_1 + (\alpha_1+\alpha_2) = \alpha_2$。
我们对所有[正根](@entry_id:199264) $\beta \in \Phi^+ = \{\alpha_1, \alpha_2, \alpha_1+\alpha_2\}$ 检查条件：
*   对于 $\beta=\alpha_1$：$(\lambda+\rho)(h_1) = \alpha_2(h_1) = A_{12} = -1$，不是正整数。
*   对于 $\beta=\alpha_2$：$(\lambda+\rho)(h_2) = \alpha_2(h_2) = A_{22} = 2$，是正整数。因此存在一个最高权为 $s_2 \cdot \lambda$ 的[子模](@entry_id:148922)。
*   对于 $\beta=\alpha_1+\alpha_2$：$(\lambda+\rho)(h_1+h_2) = \alpha_2(h_1)+\alpha_2(h_2) = -1+2=1$，是正整数。存在另一个子模。

根据维尔马模的理论，其子模结构与外尔群的布吕阿序(Bruhat order)密切相关。在本例中，由于$(\lambda+\rho)$对于[正根](@entry_id:199264)$\alpha_2$和$\alpha_1+\alpha_2$在对应[余根](@entry_id:193338)上的取值为正整数，这预示着一个复杂的子模结构。然而，其唯一的极大真[子模](@entry_id:148922)是由对应于单根$\alpha_2$的反射$s_2$所确定的，其[最高权](@entry_id:202808)为：
$$
\lambda' = s_2 \cdot \lambda = s_2(\lambda+\rho) - \rho = s_2(\alpha_2) - \rho = -\alpha_2 - (\alpha_1+\alpha_2) = -\alpha_1 - 2\alpha_2
$$
这个例子揭示了维尔马模复杂的内部结构，它与外尔群的组合学密切相关 [@problem_id:703537]。

### 表示的定量描述

分类定理告诉我们存在哪些表示，但我们还想知道它们的具体属性，如维数、[权重复度](@entry_id:184204)等。一系列强大的公式为此提供了计算工具。

#### 外尔向量

所有这些公式中都出现一个核心对象——**外尔向量 (Weyl vector)** $\rho$，它被定义为所有[正根](@entry_id:199264)和的一半，或者等价地，所有[基本权](@entry_id:200855)之和：
$$
\rho = \frac{1}{2} \sum_{\alpha \in \Phi^+} \alpha = \sum_{i=1}^r \omega_i
$$
例如，对于 $\mathfrak{sp}(6, \mathbb{C})$ (类型 $C_3$)，我们已经知道其基本权为 $\omega_1=e_1, \omega_2=e_1+e_2, \omega_3=e_1+e_2+e_3$。因此，其外尔向量为 $\rho = \omega_1+\omega_2+\omega_3 = 3e_1+2e_2+e_3$。我们可以计算其范数的平方：$(\rho, \rho) = 3^2+2^2+1^2 = 14$ [@problem_id:703679]。

#### 外尔维数公式

对于一个以主整权 $\Lambda$ 为最高权的不可约表示 $L(\Lambda)$，其维数由**外尔维数公式 (Weyl dimension formula)** 给出：
$$
\dim L(\Lambda) = \prod_{\alpha \in \Phi^+} \frac{\langle \Lambda + \rho, \alpha \rangle}{\langle \rho, \alpha \rangle}
$$
我们以 $\mathfrak{sl}(3, \mathbb{C})$ (类型 $A_2$) 的表示 $L(2\omega_1 + 3\omega_2)$ 为例来应用此公式。这里，$\Lambda = 2\omega_1 + 3\omega_2$，而 $\rho = \omega_1+\omega_2$。所以 $\Lambda+\rho = 3\omega_1+4\omega_2$。[正根](@entry_id:199264)集为 $\Phi^+ = \{\alpha_1, \alpha_2, \alpha_1+\alpha_2\}$。利用对偶关系 $\langle \omega_i, \alpha_j \rangle = \delta_{ij}$ (在 $\langle \alpha_k, \alpha_k \rangle=2$ 的归一化下)，我们计算[内积](@entry_id:158127)：
*   $\langle \Lambda+\rho, \alpha_1 \rangle = 3\langle \omega_1, \alpha_1 \rangle + 4\langle \omega_2, \alpha_1 \rangle = 3(1) + 4(0) = 3$
*   $\langle \Lambda+\rho, \alpha_2 \rangle = 3\langle \omega_1, \alpha_2 \rangle + 4\langle \omega_2, \alpha_2 \rangle = 3(0) + 4(1) = 4$
*   $\langle \Lambda+\rho, \alpha_1+\alpha_2 \rangle = 3+4=7$

同样地，$\langle \rho, \alpha_1 \rangle=1$, $\langle \rho, \alpha_2 \rangle=1$, $\langle \rho, \alpha_1+\alpha_2 \rangle=2$。代入公式：
$$
\dim L(2\omega_1 + 3\omega_2) = \frac{3}{1} \cdot \frac{4}{1} \cdot \frac{7}{2} = 42
$$
这个强大的公式将复杂的表示维数计算简化为简单的算术 [@problem_id:703621]。

#### 外尔[特征标公式](@entry_id:142515)

一个表示的**特征标 (character)** 是一个函数，它记录了该表示所有权的重复度信息。对于 $L(\Lambda)$，其特征标 $\chi_\Lambda$ 由**外尔[特征标公式](@entry_id:142515) (Weyl character formula)** 给出：
$$
\chi_\Lambda = \frac{\sum_{w \in W} \det(w) e^{w(\Lambda+\rho)}}{\sum_{w \in W} \det(w) e^{w(\rho)}}
$$
其中 $W$ 是外尔群，$e^\mu$ 是权 $\mu$ 对应的形式指数。这是一个优雅但计算复杂的公式。在某些情况下，例如对于 $\mathfrak{sp}(4, \mathbb{C})$ (类型 $C_2$) 的4维标准表示（[最高权](@entry_id:202808)为 $\Lambda=\omega_1=\epsilon_1$），我们知道其权集为 $\{\pm\epsilon_1, \pm\epsilon_2\}$。因此，其特征标是一个简单的洛朗多项式：
$$
\chi_{\omega_1}(x_1, x_2) = x_1 + x_1^{-1} + x_2 + x_2^{-1}
$$
其中 $x_i = e^{\epsilon_i}$。可以验证，这个简单的多项式确实满足外尔[特征标公式](@entry_id:142515)的商形式 [@problem_id:703685]。

#### [权重复度](@entry_id:184204)

[特征标公式](@entry_id:142515)在理论上很完美，但要从中提取单个权的重复度可能很困难。为此，有更直接的计算工具。

**[科斯坦特配分函数](@entry_id:189947) (Kostant's Partition Function)** $K(\nu)$ 定义为将权 $\nu$ 写成[正根](@entry_id:199264)之和的方式数。这是一个纯组合问题。例如，对于 $G_2$ 型李代数，其[正根](@entry_id:199264)为 $\{\alpha_1, \alpha_2, \alpha_1+\alpha_2, 2\alpha_1+\alpha_2, 3\alpha_1+\alpha_2, 3\alpha_1+2\alpha_2\}$。要计算 $K(3\alpha_1+2\alpha_2)$，我们需要找到方程 $\sum_{\beta \in \Phi^+} n_\beta \beta = 3\alpha_1+2\alpha_2$ 的非负整数解 $\{n_\beta\}$ 的个数。通过枚举所有可能性，可以发现共有7组解 [@problem_id:703623]。这个函数出现在科斯坦特重复度公式中。

**弗洛伊登塔尔公式 (Freudenthal's Formula)** 提供了一个计算[权重复度](@entry_id:184204) $m_\Lambda(\mu)$ 的递归方法：
$$
\left( \langle \Lambda+\rho, \Lambda+\rho \rangle - \langle \mu+\rho, \mu+\rho \rangle \right) m_\Lambda(\mu) = 2 \sum_{\alpha \in \Phi^+} \sum_{k=1}^\infty m_\Lambda(\mu+k\alpha) \langle \mu+k\alpha, \alpha \rangle
$$
该公式从已知的最高[权重复度](@entry_id:184204) $m_\Lambda(\Lambda)=1$ 开始，递归地计算比 $\mu$ 更高的权的重复度，从而求出 $m_\Lambda(\mu)$。例如，使用此公式可以计算出在 $\mathfrak{sl}(3, \mathbb{C})$ 的 $L(2\omega_1 + \omega_2)$ 表示中，权 $\mu = \omega_1$ 的重复度为2 [@problem_id:703533]。

### [不变量](@entry_id:148850)：[卡西米尔算子](@entry_id:144193)

在表示中，有些算子具有特别简单的行为。**二次[卡西米尔算子](@entry_id:144193) (Quadratic Casimir operator)** $C_2$ 是 $U(\mathfrak{g})$ 中心的一个元素。根据[舒尔引理](@entry_id:136779)，它在任何[不可约表示](@entry_id:263310) $L(\Lambda)$ 上都作为一个标量算子作用。其[本征值](@entry_id:154894)由一个简洁的公式给出：
$$
C_2(\Lambda) = \langle \Lambda, \Lambda + 2\rho \rangle
$$
我们以一个更高级的例子来说明其计算：$\mathfrak{g} = \mathfrak{so}(10, \mathbb{C})$ (类型 $D_5$) 的伴随表示。对于 $D_n$ 型代数，伴随表示的[最高权](@entry_id:202808)是 $\Lambda_{adj} = \omega_2$。因此，[本征值](@entry_id:154894)为 $C_2(\omega_2) = \langle \omega_2, \omega_2 + 2\rho \rangle$。
利用 $\rho = \sum_i \omega_i$ 和 $\langle \omega_i, \omega_j \rangle = (A^{-1})_{ij}$，我们有：
$$
C_2(\omega_2) = \langle \omega_2, \omega_2 \rangle + 2\sum_{i=1}^5 \langle \omega_2, \omega_i \rangle = (A^{-1})_{22} + 2\sum_{i=1}^5 (A^{-1})_{2i}
$$
这需要计算 $D_5$ 的[嘉当矩阵](@entry_id:185184)的逆。通过[解线性方程组](@entry_id:136676) $Ax=e_2$，可以求得 $A^{-1}$ 的第二行是 $(1, 2, 2, 1, 1)$。于是，$(A^{-1})_{22}=2$，且该行元素之和为 $1+2+2+1+1=7$。代入公式得到：
$$
C_2(\omega_2) = 2 + 2(7) = 16
$$
这个计算完美地融合了[最高权](@entry_id:202808)、外尔向量、[嘉当矩阵](@entry_id:185184)和基本权等多个核心概念，展示了理论的内在一致性和强大威力 [@problem_id:703591]。

本章系统地介绍了[最高权表示](@entry_id:184031)的理论框架和相关计算机制。从李代数的结构分解开始，到[最高权表示](@entry_id:184031)的定义、分类，再到维尔马模的普适构造，最后到一系列强大的定量公式，我们勾勒出了一幅完整而精密的数学图景。这些原理和机制不仅是纯粹数学的核心内容，也为理论物理等领域提供了不可或缺的工具。