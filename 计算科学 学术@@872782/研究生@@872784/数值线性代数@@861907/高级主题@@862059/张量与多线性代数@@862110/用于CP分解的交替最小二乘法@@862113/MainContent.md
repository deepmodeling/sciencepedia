## 引言
张量，作为向量和矩阵在高维度的推广，已成为表示和分析多方面数据的标准工具。从神经科学中的脑电信号到[推荐系统](@entry_id:172804)中的用户-商品-评分数据，揭示这些[多维数据](@entry_id:189051)集背后的潜在结构对于科学发现和技术创新至关重要。[正则分解](@entry_id:634116)/[平行因子分析](@entry_id:753095)（[CP分解](@entry_id:203488)）是其中最基本且最富解释性的模型之一，它将一个[高阶张量](@entry_id:200122)近似为若干个秩-1张量的和。然而，寻找最佳[CP分解](@entry_id:203488)是一个具有挑战性的[非凸优化](@entry_id:634396)问题，缺乏直接的闭式解。

为了解决这一难题，交替最小二乘（ALS）算法应运而生，并成为最广泛使用的求解方法之一。ALS以其概念上的简洁性和实现的相对容易性而著称，它通过将复杂的联合[优化问题](@entry_id:266749)分解为一系列更简单的线性最小二乘子问题来迭代求解。尽管其基本思想简单，但深入理解其数学机制、计算特性以及在实际应用中的细微差别，对于有效地利用这一强大工具至关重要。本文旨在为读者提供一个关于CP-ALS的全面指南，弥合理论推导与实践应用之间的鸿沟。

在接下来的内容中，我们将分三个核心章节展开探讨。首先，在“原理与机制”中，我们将深入CP模型的核心，推导ALS的更新规则，并剖析其计算瓶颈、[数值稳定性](@entry_id:146550)以及收敛中可能遇到的陷阱。其次，在“应用与交叉学科联系”中，我们将展示如何扩展和调[整基](@entry_id:190217)础ALS框架，通过引入约束和正则化来处理真实世界的复杂数据，并探讨其在信号处理、机器学习等多个领域的交叉应用。最后，在“动手实践”部分，我们提供了一系列精心设计的计算问题，旨在通过实践加深您对算法实现和性能分析的理解，将理论知识转化为实际技能。

## 原理与机制

本章深入探讨了用于[正则分解](@entry_id:634116)/[平行因子分析](@entry_id:753095)（CP）分解的交替最小二乘（ALS）算法的数学原理和计算机制。我们将从CP模型的基本属性（包括其固有的不确定性和唯一的秩概念）开始，然后系统地推导ALS更新规则。最后，我们将分析算法的计算、数值和收敛特性，包括其主要计算瓶颈和潜在的陷阱，如退化解。

### CP模型及其基本性质

[CP分解](@entry_id:203488)将一个[高阶张量](@entry_id:200122)表示为若干个秩-1张量的和。对于一个三阶张量 $\mathcal{X} \in \mathbb{R}^{I \times J \times K}$，其秩为 $R$ 的[CP分解](@entry_id:203488)形式为：
$$
\mathcal{X} \approx \sum_{r=1}^{R} a_r \circ b_r \circ c_r
$$
其中 $a_r \in \mathbb{R}^{I}$, $b_r \in \mathbb{R}^{J}$ 和 $c_r \in \mathbb{R}^{K}$ 是因子向量，$\circ$ 表示向量外积。这些因子向量通常被组织成因子矩阵 $A = [a_1, \dots, a_R] \in \mathbb{R}^{I \times R}$, $B = [b_1, \dots, b_R] \in \mathbb{R}^{J \times R}$ 和 $C = [c_1, \dots, c_R] \in \mathbb{R}^{K \times R}$。该模型有时也用 Kruskal 算[子表示](@entry_id:141094)为 $\mathcal{X} \approx \llbracket A, B, C \rrbracket$。

#### 固有的不确定性

与矩阵分解不同，[CP分解](@entry_id:203488)的因子矩阵并非唯一确定。即使对于一个给定的张量，也存在多种因子矩阵组合可以重构出完全相同的张量。理解这些不确定性对于正确解释模型和设计算法至关重要。主要的不确定性包括两种：

1.  **[置换](@entry_id:136432)不确定性 (Permutation Indeterminacy)**：由于[向量加法](@entry_id:155045)满足[交换律](@entry_id:141214)，秩-1分量的求和顺序不影响最终结果。因此，如果我们将因子矩阵 $A, B, C$ 的列以相同的[置换](@entry_id:136432)方式重新[排列](@entry_id:136432)，重构出的张量保持不变。具体来说，对于任何一个 $R \times R$ 的[置换矩阵](@entry_id:136841) $P$，因子组 $(AP, BP, CP)$ 与 $(A, B, C)$ 生成的张量是完全相同的 [@problem_id:3533191]。

2.  **缩放不确定性 (Scaling Indeterminacy)**：外积是[多重线性](@entry_id:151506)的，这意味着我们可以对构成单个秩-1分量的因子向量进行缩放，只要它们的乘积保持不变。对于任意一组非零标量 $\alpha_r, \beta_r, \gamma_r$ 满足 $\alpha_r \beta_r \gamma_r = 1$，用 $(\alpha_r a_r, \beta_r b_r, \gamma_r c_r)$ 替换 $(a_r, b_r, c_r)$ 不会改变第 $r$ 个秩-1分量。这对应于对因子矩阵的列进行缩放。例如，对于任意满足 $D_A D_B D_C = I_R$ 的[对角矩阵](@entry_id:637782) $D_A, D_B, D_C$，因子组 $(A D_A, B D_B, C D_C)$ 与 $(A, B, C)$ 表示同一个张量 [@problem_id:3533191]。在实践中，为了消除这种不确定性并改善算法的数值表现，通常会将因子矩阵的列归一化（例如，使每列的范数为1），并将吸收的缩放因子存放在一个单独的权重向量 $\lambda \in \mathbb{R}^R$ 中。例如，模型可以写成 $\mathcal{X} \approx \sum_{r=1}^{R} \lambda_r (\tilde{a}_r \circ \tilde{b}_r \circ \tilde{c}_r)$，其中 $\tilde{a}_r, \tilde{b}_r, \tilde{c}_r$ 是归一化后的向量。

#### [张量秩](@entry_id:266558)的概念

[张量秩](@entry_id:266558)的概念比[矩阵秩](@entry_id:153017)更为复杂。

**[CP秩](@entry_id:748030) (CP rank)**，记为 $\operatorname{rank}_{CP}(\mathcal{X})$，是指能够精确表示张量 $\mathcal{X}$ 所需的最少秩-1分量的数量 $R$。确定一个通用张量的[CP秩](@entry_id:748030)是一个NP-hard问题。

[CP秩](@entry_id:748030)不同于**多线性秩 (multilinear rank)** 或 **[Tucker秩](@entry_id:756214)**，后者由张量沿各模式展开（matricization）后得到的矩阵的秩定义。对于一个三阶张量 $\mathcal{X}$，其[Tucker秩](@entry_id:756214)是一个元组 $(r_1, r_2, r_3)$，其中 $r_n = \operatorname{rank}(X_{(n)})$，$X_{(n)}$ 是 $\mathcal{X}$ 的模式-$n$ 展开矩阵。一个基本的不等式是 $\operatorname{rank}_{CP}(\mathcal{X}) \ge \max(r_1, r_2, r_3)$。然而，[CP秩](@entry_id:748030)可以远大于任何一个模式展开[矩阵的秩](@entry_id:155507)。例如，一个 $3 \times 2 \times 2$ 的张量，其[CP秩](@entry_id:748030)可以是 $R=3$，而其[Tucker秩](@entry_id:756214)为 $(3, 2, 2)$，这表明[CP秩](@entry_id:748030)可能等于但不必小于最大维度 [@problem_id:3533194]。同样，一个 $2 \times 2 \times 2$ 的张量，其[CP秩](@entry_id:748030)可以是 $R=2$，而其[Tucker秩](@entry_id:756214)为 $(2, 2, 1)$ [@problem_id:3533194]。这些例子说明，仅仅通过检查展开[矩阵的秩](@entry_id:155507)来确定[CP秩](@entry_id:748030)是不可行的。

#### CP分[解的唯一性](@entry_id:143619)

尽管存在[置换](@entry_id:136432)和缩放不确定性，但在某些条件下，[CP分解](@entry_id:203488)可以是**本质唯一 (essentially unique)** 的，即分解在上述不确定性之外是唯一的。这是[CP分解](@entry_id:203488)在数据分析中备受青睐的一个关键原因，因为唯一性意味着因子是可解释的。

Joseph Kruskal 证明了一个关于三阶张量[CP分解](@entry_id:203488)唯一性的充分条件，即著名的**Kruskal条件**。该条件与因子矩阵的**Kruskal秩**有关。一个矩阵 $M$ 的Kruskal秩，记为 $k_M$，是使得 $M$ 的任意 $k_M$ 列都[线性无关](@entry_id:148207)的最大整数 $k_M$。

**Kruskal条件**：如果因子矩阵 $A, B, C$ 的Kruskal秩满足以下不等式：
$$
k_A + k_B + k_C \ge 2R + 2
$$
那么张量的[CP分解](@entry_id:203488)是本质唯一的。

例如，考虑一个由 $R=4$ 的因子矩阵 $A \in \mathbb{R}^{4 \times 4}, B \in \mathbb{R}^{3 \times 4}, C \in \mathbb{R}^{3 \times 4}$ 定义的CP模型。如果 $A$ 是单位矩阵，其任意4列都线性无关，因此 $k_A=4$。如果 $B$ 和 $C$ 的任意3列都是线性无关的，那么 $k_B=3$ 且 $k_C=3$。在这种情况下，我们有 $k_A + k_B + k_C = 4 + 3 + 3 = 10$。对于 $R=4$，$2R+2 = 2(4)+2 = 10$。由于 $10 \ge 10$，Kruskal条件得到满足，该分解是本质唯一的 [@problem_id:3533252]。

### 交替最小二乘 (ALS) 算法

ALS算法是拟合CP模型最常用的方法之一。其目标是找到因子矩阵 $A, B, C$ 以最小化模型残差的平方[Frobenius范数](@entry_id:143384)：
$$
\min_{A, B, C} \left\| \mathcal{X} - \sum_{r=1}^{R} a_r \circ b_r \circ c_r \right\|_F^2
$$
这是一个关于所有因子矩阵的[非凸优化](@entry_id:634396)问题。ALS采用**块[坐标下降](@entry_id:137565) (block coordinate descent)** 的策略，通过循环地固定其他因子矩阵，只对一个因子矩阵求解一个线性最小二乘子问题。

#### ALS更新规则的推导

下面我们推导更新因子矩阵 $A$ 的规则，更新 $B$ 和 $C$ 的规则可由对称性得到。

**1. 子问题的矩阵形式**

当固定 $B$ 和 $C$ 时，[优化问题](@entry_id:266749)变为一个关于 $A$ 的线性[最小二乘问题](@entry_id:164198)。为了利用线性代数的工具，我们将张量问题转化为矩阵形式。CP模型的模式-1展开矩阵可以表示为：
$$
\left(\llbracket A, B, C \rrbracket\right)_{(1)} = A (C \odot B)^{\top}
$$
这里，$X_{(1)} \in \mathbb{R}^{I \times JK}$ 是张量 $\mathcal{X}$ 的模式-1展开矩阵，而 $\odot$ 表示**[Khatri-Rao积](@entry_id:751014) (Khatri-Rao product)**。两个具有相同列数的矩阵 $B \in \mathbb{R}^{J \times R}$ 和 $C \in \mathbb{R}^{K \times R}$ 的[Khatri-Rao积](@entry_id:751014) $C \odot B$ 是一个 $JK \times R$ 的矩阵，其第 $r$ 列是 $C$ 和 $B$ 的第 $r$ 列的Kronecker积：$(C \odot B)_{:,r} = c_r \otimes b_r$ [@problem_id:3533199]。

因此，关于 $A$ 的子问题可以写成标准的矩阵最小二乘形式：
$$
\min_{A} \left\| X_{(1)} - A (C \odot B)^{\top} \right\|_F^2
$$

**2. 正规方程**

该[最小二乘问题](@entry_id:164198)的解可以通过**正规方程 (normal equations)** 找到。对目标函数关于 $A$ 求导并令其为零，我们得到：
$$
A (C \odot B)^{\top}(C \odot B) = X_{(1)} (C \odot B)
$$
这个方程是求解 $A$ 的核心 [@problem_id:3485665] [@problem_id:3533225]。

**3. [Gram矩阵](@entry_id:148915)的简化**

方程左侧的矩阵 $(C \odot B)^{\top}(C \odot B)$ 是一个 $R \times R$ 的[Gram矩阵](@entry_id:148915)。它可以被极大地简化。该矩阵的 $(r,s)$ 元素是[Khatri-Rao积](@entry_id:751014)矩阵的第 $r$ 列和第 $s$ 列的[内积](@entry_id:158127)：
$$
\left[ (C \odot B)^{\top}(C \odot B) \right]_{rs} = (c_r \otimes b_r)^{\top} (c_s \otimes b_s)
$$
利用Kronecker积的一个重要性质 $(u \otimes v)^{\top}(x \otimes y) = (u^{\top}x)(v^{\top}y)$，上式变为：
$$
(c_r^{\top}c_s)(b_r^{\top}b_s) = [C^{\top}C]_{rs} [B^{\top}B]_{rs}
$$
这正是[Gram矩阵](@entry_id:148915) $C^{\top}C$ 和 $B^{\top}B$ 的**[Hadamard积](@entry_id:180744) (Hadamard product)**（即逐元素乘积，用 $*$ 表示）的 $(r,s)$ 元素。因此，我们得到了一个关键的恒等式 [@problem_id:3485665]：
$$
(C \odot B)^{\top}(C \odot B) = (C^{\top}C) * (B^{\top}B)
$$
由于[Hadamard积](@entry_id:180744)是可交换的，这也等于 $(B^{\top}B) * (C^{\top}C)$ [@problem_id:3485665]。

**4. 闭式更新规则**

将上述恒等式代入正规方程，我们得到：
$$
A \left( (C^{\top}C) * (B^{\top}B) \right) = X_{(1)} (C \odot B)
$$
假设矩阵 $(C^{\top}C) * (B^{\top}B)$ 可逆，我们可以解出 $A$ 的更新规则：
$$
A \leftarrow X_{(1)} (C \odot B) \left( (C^{\top}C) * (B^{\top}B) \right)^{-1}
$$
通过[循环置换](@entry_id:272913)索引 $(1,2,3)$ 和因子矩阵 $(A,B,C)$，我们可以得到更新 $B$ 和 $C$ 的对称规则 [@problem_id:3533203] [@problem_id:3485665]：
$$
B \leftarrow X_{(2)} (C \odot A) \left( (C^{\top}C) * (A^{\top}A) \right)^{-1}
$$
$$
C \leftarrow X_{(3)} (B \odot A) \left( (B^{\top}B) * (A^{\top}A) \right)^{-1}
$$
这些方程构成了CP-ALS算法的核心迭代步骤。

### 计算与数值考量

#### MTTKRP计算瓶颈

在每个ALS子步骤中，计算量最大的部分是计算形如 $X_{(n)} (\dots)$ 的项。以更新 $A$ 为例，该项是 $X_{(1)} (C \odot B)$。这个操作被称为**[矩阵化](@entry_id:751739)张量乘以[Khatri-Rao积](@entry_id:751014) (Matricized-Tensor Times Khatri-Rao Product, MTTKRP)**。

让我们分析一下计算成本。计算[Gram矩阵](@entry_id:148915) $C^{\top}C$ 和 $B^{\top}B$ 的成本分别为 $O(KR^2)$ 和 $O(JR^2)$。它们的[Hadamard积](@entry_id:180744)成本为 $O(R^2)$。求解一个 $R \times R$ 线性系统的成本大约是 $O(IR^2 + R^3)$。然而，MTTKRP的计算涉及与大尺寸数据张量 $\mathcal{X}$ 的收缩。对于一个稠密张量，其成本为 $O(IJKR)$。在典型应用中，张量的维度 $I, J, K$ 远大于秩 $R$，因此 $IJKR$ 远远超过其他项的成本。正因为如此，MTTKRP被认为是ALS算法的主要计算瓶颈 [@problem_id:3533225]。高效的实现通常会避免显式地构建展开矩阵和[Khatri-Rao积](@entry_id:751014)矩阵，而是通过专门的例程直接计算收缩。

#### [条件数](@entry_id:145150)与稳定性

ALS更新的数值稳定性取决于需要求逆的[Gram矩阵](@entry_id:148915)的[条件数](@entry_id:145150)。对于 $A$ 的更新，这个矩阵是 $G = (C^{\top}C) * (B^{\top}B)$。其谱[条件数](@entry_id:145150) $\kappa_2(G)$ 直接决定了 $A$ 的解对右侧MTTKRP项中扰动的敏感度 [@problem_id:3533260]。

因子矩阵的**共线性 (collinearity)** 对这个[条件数](@entry_id:145150)有显著影响。如果因子矩阵 $B$ 和 $C$ 的某些列几乎是线性相关的（即几乎共线），例如 $b_r \approx \alpha b_s$，那么它们的[Gram矩阵](@entry_id:148915)的对应非对角元素 $(B^{\top}B)_{rs}$ 将接近其对角元素。当两个[Gram矩阵](@entry_id:148915)的这些大非对角元素通过[Hadamard积](@entry_id:180744)相乘时，效应会被放大。例如，如果 $b_r$ 和 $b_s$ 以及 $c_r$ 和 $c_s$ 都是[单位向量](@entry_id:165907)，且它们之间的[内积](@entry_id:158127)（即夹角的余弦）都是 $0.99$，那么 $G$ 的 $(r,s)$ 非对角元素将是 $0.99 \times 0.99 = 0.9801$ [@problem_id:3533260]。这使得矩阵 $G$ 接近奇异，导致其[条件数](@entry_id:145150)非常大，从而使ALS更新不稳定且收敛缓慢。

在某些特殊情况下，[条件数](@entry_id:145150)可以得到很好的控制。例如，如果因子矩阵 $C$ 的列是标准正交的，那么 $C^{\top}C=I$。此时，[Gram矩阵](@entry_id:148915) $G = I * (B^{\top}B) = \operatorname{diag}(\|b_1\|_2^2, \dots, \|b_R\|_2^2)$ 变成一个[对角矩阵](@entry_id:637782)。其[条件数](@entry_id:145150)仅取决于 $B$ 的列范数的平方之比，而与 $B$ 中列之间的任何共[线性无关](@entry_id:148207) [@problem_id:3533260]。

### 收敛特性与陷阱

#### 收敛保证

ALS算法的每次迭代都能保证目标函数值非增。然而，它是否收敛到一个理想的点（如[驻点](@entry_id:136617)，即梯度为零的点）则需要满足特定条件。由于[CP分解](@entry_id:203488)的非凸性，ALS不保证收敛到[全局最小值](@entry_id:165977)。

对于ALS迭代序列的任何一个聚点（accumulation point），要保证它是一个[驻点](@entry_id:136617)，通常需要满足两个关键条件 [@problem_id:3533231]：
1.  **有界性 (Boundedness)**：迭代序列必须位于一个紧集中。由于CP模型固有的缩放不确定性，原始因子矩阵的范数可能在迭代中趋于无穷大。通过在每一步进行归一化，可以确保迭代序列保持有界。
2.  **子问题的唯一解 (Unique Subproblem Solution)**：在每个块[坐标下降](@entry_id:137565)步骤中，最小二乘子问题必须有唯一解。对于 $A$ 的更新，这要求矩阵 $(C \odot B)$ 具有[满列秩](@entry_id:749628) $R$，这等价于其[Gram矩阵](@entry_id:148915) $(C^{\top}C) * (B^{\top}B)$ 是可逆的。

如果这些条件在迭代的[后期](@entry_id:165003)阶段得到满足，那么可以保证ALS的任何聚点都是[目标函数](@entry_id:267263)的一个[驻点](@entry_id:136617)。

#### “沼泽”现象与退化

在实践中，ALS有时会表现出极度缓慢的收敛，目标函数值在很长一段时间内几乎没有变化，这种现象被称为**“沼泽” (swamp)**。这通常与CP模型的**退化 (degeneracy)** 有关。

这种退化的根源在于，秩最多为 $R$ 的张量集合在[Frobenius范数](@entry_id:143384)拓扑下不是一个[闭集](@entry_id:136446)。这意味着一个秩大于 $R$ 的张量可以是一个秩为 $R$ 的张量[序列的极限](@entry_id:159239)。在这样的序列中，为了逼近目标张量，两个或多个秩-1分量可能变得几乎[线性相关](@entry_id:185830)，而它们的权重则同时发散到正负无穷大，通过巨大的、几乎相互抵消的项来精确拟合目标。

一个典型的例子是，一个秩为3的张量 $T$ 可以被一个秩为2的张量序列 $X(t)$ 逼近，其中当 $t \to 0$ 时，$X(t) \to T$ [@problem_id:3485668]。在这个序列中，$X(t)$ 由两个秩-1项构成，它们的因子向量随着 $t \to 0$ 变得几乎共线，而它们的权重（尺度）则像 $1/t$ 一样发散到无穷大。尽管残差 $\|T - X(t)\|_F^2$ 像 $O(t^2)$ 一样趋于零，但因子范数却在爆炸。

这种退化行为直接影响ALS的性能。当因子向量变得几乎共线时，如前一节所述，正规方程中的[Gram矩阵](@entry_id:148915) $G = (C^{\top}C) * (B^{\top}B)$ 变得严重病态（ill-conditioned），其条件数会爆炸。这使得ALS的每一步更新都非常微小，导致算法在目标函数景观的平坦区域（“沼泽”）中停滞不前 [@problem_id:3485668]。因此，因子[共线性](@entry_id:270224)和因子范数发散是导致ALS收敛缓慢的根本原因。