## 引言
在[逆问题](@entry_id:143129)和数据同化等众多科学领域，我们常常需要从远少于未知数的测量数据中恢复一个高维信号。这在数学上是一个[欠定线性系统](@entry_id:756304)，若无额外信息则有无穷多解。然而，当信号本身是“稀疏”的——即其大部分分量为零时，问题就变得可以解决。但直接寻找最[稀疏解](@entry_id:187463)是一个计算上不可行的[NP难问题](@entry_id:146946)，这构成了[稀疏恢复](@entry_id:199430)领域的核心挑战。

本文聚焦于解决这一挑战的一种高效贪婪算法——[正交匹配追踪](@entry_id:202036)（Orthogonal Matching Pursuit, OMP）。通过阅读本文，您将系统地掌握OMP的理论与实践。第一章“原理与机制”将深入剖析OMP的迭代步骤、其成功恢复信号的数学保证（如[互相关性](@entry_id:188177)与受限等距性质），以及处理[数值稳定性](@entry_id:146550)和噪声时的关键策略。第二章“应用与交叉学科联系”将展示OMP如何在地球物理、图像处理、信号处理乃至机器学习等不同领域中解决实际问题。最后，第三章“动手实践”将提供一系列练习，帮助您巩固理论知识，将算法付诸实践。

让我们首先从OMP的核心工作原理开始，揭示它如何巧妙地逐步构建稀疏解。

## 原理与机制

本章深入探讨[正交匹配追踪](@entry_id:202036)（Orthogonal Matching Pursuit, OMP）算法的内部工作原理及其理论基础。在“引言”章节的基础上，我们将不再赘述[稀疏恢复](@entry_id:199430)的背景，而是直接进入其核心机制的解析。我们将阐明OMP如何通过一种贪婪的迭代策略来应对[稀疏恢复](@entry_id:199430)问题固有的组合复杂性，并剖析保证其成功恢复信号的数学条件。此外，我们还将讨论算法在实际应用中的关键考量，包括数值稳定性与含噪数据下的终止策略。

### [稀疏恢复](@entry_id:199430)问题：一个组合挑战

在许多逆问题和数据同化应用中，我们面临这样一个问题：从一个欠定的线性测量系统 $\boldsymbol{y} = \boldsymbol{A}\boldsymbol{x}$ 中恢复未知[状态向量](@entry_id:154607) $\boldsymbol{x} \in \mathbb{R}^n$。其中，$\boldsymbol{y} \in \mathbb{R}^m$ 是测量向量，$\boldsymbol{A} \in \mathbb{R}^{m \times n}$ 是已知的[观测算子](@entry_id:752875)或字典矩阵，且通常 $m \ll n$。这样一个系统拥有无穷多解，因为矩阵 $\boldsymbol{A}$ 存在一个非平凡的[零空间](@entry_id:171336)。然而，如果我们引入一个强有力的[先验信息](@entry_id:753750)——即 $\boldsymbol{x}$ 是**稀疏的 (sparse)**——问题的性质将发生根本改变。

一个向量 $\boldsymbol{x}$ 被认为是 **$k$-稀疏** 的，如果它最多只有 $k$ 个非零元素。我们使用所谓的 $\ell_0$“范数”，$\|\boldsymbol{x}\|_0$，来表示 $\boldsymbol{x}$ 中非零元素的个数。因此，$k$-稀疏意味着 $\|\boldsymbol{x}\|_0 \le k$。稀疏性假设极大地缩小了解的搜索空间。

[稀疏恢复](@entry_id:199430)的核心任务是识别出 $\boldsymbol{x}$ 的非零元素所在的位置，这个位置的索引集合被称为向量的**支撑集 (support)**，定义为 $\operatorname{supp}(\boldsymbol{x}) = \{ j \in \{1, \dots, n\} \mid x_j \neq 0 \}$。 一旦我们成功地确定了真实的支撑集 $S = \operatorname{supp}(\boldsymbol{x})$，恢复问题就从一个欠定的问题转化为了一个可能超定的良态问题。我们只需在由 $S$ 索引的 $\boldsymbol{A}$ 的列（记为子矩阵 $\boldsymbol{A}_S$）上求解一个标准最小二乘问题，即可确定非零系数的值：
$$
\min_{\boldsymbol{w}} \|\boldsymbol{y} - \boldsymbol{A}_S \boldsymbol{w}\|_2^2
$$
然而，寻找这个正确的支撑集 $S$ 本身就是一个巨大的挑战。在 $n$ 个可能的位置中选择 $k$ 个非零元素，存在 $\binom{n}{k}$ 种可能性。遍历所有这些[子集](@entry_id:261956)以找到给出最佳数据拟合的那个，即求解所谓的 $\ell_0$ 最小化问题：
$$
\min_{\boldsymbol{x}} \|\boldsymbol{x}\|_0 \quad \text{subject to} \quad \boldsymbol{A}\boldsymbol{x} = \boldsymbol{y}
$$
在计算上是不可行的。这个问题是[NP难](@entry_id:264825)的，这意味着对于实际规模的问题，穷举搜索的计算成本高到无法接受。 这就催生了各种旨在以可计算的成本逼近最优解的高效算法，其中，贪婪算法（如OMP）和[凸松弛](@entry_id:636024)方法（如[基追踪](@entry_id:200728)）是最为重要的两类。

### [正交匹配追踪 (OMP)](@entry_id:753008) 算法

[正交匹配追踪](@entry_id:202036)（OMP）是一种迭代的贪婪算法，它试图通过一系列局部最优选择来逐步构建出真实的支撑集。其核心思想是，在每一步中，选择与当前数据残差最“匹配”的原子（即字典矩阵 $\boldsymbol{A}$ 的列），并将其添加到支撑集中。

算法的具体流程如下 ：

1.  **初始化**: 设迭代次数 $t=1$，初始支撑集为空 $S^{(0)} = \emptyset$，初始解为零向量 $\boldsymbol{\hat{x}}^{(0)} = \boldsymbol{0}$，初始残差等于测量向量 $\boldsymbol{r}^{(0)} = \boldsymbol{y} - \boldsymbol{A}\boldsymbol{\hat{x}}^{(0)} = \boldsymbol{y}$。

2.  **迭代步骤 (对 $t=1, 2, \dots$)**:
    a.  **识别 (Identification)**: 在字典中寻找与当前残差 $\boldsymbol{r}^{(t-1)}$ 最相关的原子。这通过计算所有原子与残差的[内积](@entry_id:158127)，并选取[绝对值](@entry_id:147688)最大的那个来实现：
        $$
        j^{(t)} = \operatorname{argmax}_{j \in \{1, \dots, n\}} |\langle \boldsymbol{a}_j, \boldsymbol{r}^{(t-1)} \rangle|
        $$
    b.  **支撑集更新 (Support Update)**: 将新选出的原子索引加入支撑集：
        $$
        S^{(t)} = S^{(t-1)} \cup \{j^{(t)}\}
        $$
    c.  **[系数估计](@entry_id:175952) (Coefficient Estimation)**: 基于更新后的支撑集 $S^{(t)}$，重新计算信号的最佳估计。这是通过求解一个最小二乘问题完成的，该问题将测量向量 $\boldsymbol{y}$ 正交投影到由 $S^{(t)}$ 中原子张成的[子空间](@entry_id:150286)上：
        $$
        \boldsymbol{\hat{x}}^{(t)} = \operatorname{argmin}_{\boldsymbol{x} \text{ s.t. } \operatorname{supp}(\boldsymbol{x})=S^{(t)}} \|\boldsymbol{y} - \boldsymbol{A}\boldsymbol{x}\|_2
        $$
        这等价于求解 $\min_{\boldsymbol{w}} \|\boldsymbol{y} - \boldsymbol{A}_{S^{(t)}} \boldsymbol{w}\|_2$，其中 $\boldsymbol{A}_{S^{(t)}}$ 是由 $S^{(t)}$ 索引的列构成的子矩阵。
    d.  **残差更新 (Residual Update)**: 用新的估计值更新残差：
        $$
        \boldsymbol{r}^{(t)} = \boldsymbol{y} - \boldsymbol{A}\boldsymbol{\hat{x}}^{(t)} = \boldsymbol{y} - \boldsymbol{A}_{S^{(t)}}\boldsymbol{\hat{x}}_{S^{(t)}}^{(t)}
        $$
        由于[最小二乘解](@entry_id:152054)的性质，新的残差 $\boldsymbol{r}^{(t)}$ 与 $\boldsymbol{A}_{S^{(t)}}$ 张成的[子空间](@entry_id:150286)正交，即对于所有 $j \in S^{(t)}$，都有 $\langle \boldsymbol{a}_j, \boldsymbol{r}^{(t)} \rangle = 0$。这个“正交”特性正是算法名称的由来，它确保了每个原子只被选择一次。

3.  **终止**: 算法持续迭代，直到满足某个预设的**[终止准则](@entry_id:136282)**。常见的准则包括：達到已知的稀疏度 $k$，或者残差的能量降低到某个与噪声水平相关的阈值以下。

在上述识别步骤中，一个至关重要的细节是**列归一化 (column normalization)**。为了使基于相关性的选择有意义，通常要求字典的所有列（原子）都具有单位 $\ell_2$ 范数，即 $\|\boldsymbol{a}_j\|_2 = 1$。如果不进行归一化，选择过程会产生偏差。根据[内积](@entry_id:158127)的几何定义 $\langle \boldsymbol{u}, \boldsymbol{v} \rangle = \|\boldsymbol{u}\|_2 \|\boldsymbol{v}\|_2 \cos(\theta)$，OMP的选择准则实际上是在最大化 $|\langle \boldsymbol{a}_j, \boldsymbol{r}^{(t-1)} \rangle| = \|\boldsymbol{a}_j\|_2 \|\boldsymbol{r}^{(t-1)}\|_2 |\cos(\theta_j)|$。如果 $\|\boldsymbol{a}_j\|_2$ 各不相同，一个与残差方向并不对齐（$|\cos(\theta_j)|$ 较小）但自身范数很大的原子，可能会胜过一个方向更一致但范数较小的原子。归一化消除了 $\|\boldsymbol{a}_j\|_2$ 的影响，使得选择纯粹基于方向的对齐程度（即最大化 $|\cos(\theta_j)|$）。

### 精确恢复的理论保证

OMP作为一个贪婪算法，其成功并非无条件的。理论分析旨在回答两个核心问题：首先，一个稀疏解在何时是唯一的？其次，OMP在何时能够成功找到这个唯一解？

#### 稀疏[解的唯一性](@entry_id:143619)

即便系统是欠定的（$m \lt n$），[稀疏性](@entry_id:136793)假设也能保证[解的唯一性](@entry_id:143619)。假设存在两个不同的 $k$-稀疏解 $\boldsymbol{x}$ 和 $\boldsymbol{x}'$。那么它们的差 $\boldsymbol{h} = \boldsymbol{x} - \boldsymbol{x}'$ 是一个非[零向量](@entry_id:156189)，且 $\|\boldsymbol{h}\|_0 \le \|\boldsymbol{x}\|_0 + \|\boldsymbol{x}'\|_0 \le 2k$。同时，$\boldsymbol{A}\boldsymbol{h} = \boldsymbol{A}\boldsymbol{x} - \boldsymbol{A}\boldsymbol{x}' = \boldsymbol{y} - \boldsymbol{y} = \boldsymbol{0}$，这意味着 $\boldsymbol{h}$ 位于 $\boldsymbol{A}$ 的零空间中。因此，$k$-稀疏[解的唯一性](@entry_id:143619)等价于要求 $\boldsymbol{A}$ 的[零空间](@entry_id:171336)中不包含任何 $2k$-稀疏或更稀疏的非零向量。

这个条件可以用字典 $\boldsymbol{A}$ 的一个重要属性——**spark**——来表述。$\operatorname{spark}(\boldsymbol{A})$ 定义为矩阵 $\boldsymbol{A}$ 中线性相关的列的最小数目。一个 $k$-[稀疏解](@entry_id:187463)是唯一的，当且仅当 $\operatorname{spark}(\boldsymbol{A}) > 2k$。 这个条件保证了任何 $2k$ 个或更少的列都是[线性无关](@entry_id:148207)的，从而排除了零空间中存在 $2k$-稀疏向量的可能性。

#### OMP的成功条件

[解的唯一性](@entry_id:143619)并不自动保证OMP能够找到它。算法的成功依赖于字典 $\boldsymbol{A}$ 更精细的几何结构，这些结构确保了贪婪选择的正确性。

##### [互相关性](@entry_id:188177) (Mutual Coherence)

一个简单而直观的度量是**[互相关性](@entry_id:188177)**，它衡量字典中任意两个不同原子之间的最大“重叠”程度。对于一个列已归一化的字典 $\boldsymbol{A}$，其[互相关性](@entry_id:188177)定义为：
$$
\mu(\boldsymbol{A}) = \max_{i \neq j} |\langle \boldsymbol{a}_i, \boldsymbol{a}_j \rangle|
$$
$\mu(\boldsymbol{A})$ 的值越小，字典的原子就越接近正交，OMP的选择就越不容易出错。

我们可以通过分析OMP的第一步来理解其作用。假设真实信号是 $\boldsymbol{x}^\star$，其支撑集为 $S$。测量向量为 $\boldsymbol{y} = \boldsymbol{A}\boldsymbol{x}^\star = \sum_{i \in S} \boldsymbol{a}_i x_i^\star$。
- 对于一个“不正确”的原子 $j \notin S$，其与 $\boldsymbol{y}$ 的相关性有[上界](@entry_id:274738)：
  $|\langle \boldsymbol{a}_j, \boldsymbol{y} \rangle| = |\sum_{i \in S} x_i^\star \langle \boldsymbol{a}_j, \boldsymbol{a}_i \rangle| \le \sum_{i \in S} |x_i^\star| |\langle \boldsymbol{a}_j, \boldsymbol{a}_i \rangle| \le \mu(\boldsymbol{A}) \|\boldsymbol{x}^\star_S\|_1$。
- 对于一个“正确”的原子 $i \in S$，其相关性有下界：
  $|\langle \boldsymbol{a}_i, \boldsymbol{y} \rangle| = |x_i^\star + \sum_{l \in S, l \neq i} x_l^\star \langle \boldsymbol{a}_i, \boldsymbol{a}_l \rangle| \ge |x_i^\star| - \mu(\boldsymbol{A}) (\|\boldsymbol{x}^\star_S\|_1 - |x_i^\star|)$。

OMP要做出正确的选择，就需要至少有一个正确原子的相关性大于所有不正确原子的相关性。上述不等式表明，如果 $\mu(\boldsymbol{A})$ 足够小，那么真实信号系数 $|x_i^\star|$ 的贡献将主导相关性计算，使得OMP能够正确识别出支撑集中的元素。一个经典的充分条件是，如果 $k  \frac{1}{2}(1 + \mu(\boldsymbol{A})^{-1})$，OMP保证能够在 $k$ 步内精确恢复任何 $k$-[稀疏信号](@entry_id:755125)。 另一个更严格但更简洁的条件是，当 $\mu(\boldsymbol{A})  \frac{1}{2k-1}$ 时，OMP和[基追踪](@entry_id:200728)都能成功。

需要注意的是，即使唯一解存在（例如，$\operatorname{spark}(\boldsymbol{A})  2k$），如果字典的相关性结构比较“恶劣”，OMP仍有可能在早期选择了错误的原子而导致失败。

##### 受限等距性质 (Restricted Isometry Property, RIP)

[互相关性](@entry_id:188177)是一个强大但有时过于严苛的准则。一个更通用、更强大的分析工具是**受限等距性质 (RIP)**。一个矩阵 $\boldsymbol{A}$ 满足 $k$ 阶RIP，如果存在一个常数 $\delta_k \in [0, 1)$，使得对于所有 $k$-稀疏向量 $\boldsymbol{v}$，以下不等式成立：
$$
(1 - \delta_k) \|\boldsymbol{v}\|_2^2 \le \|\boldsymbol{A}\boldsymbol{v}\|_2^2 \le (1 + \delta_k) \|\boldsymbol{v}\|_2^2
$$
**受限等距常数 $\delta_k$** 被定义为满足此式的最小 $\delta_k$。

RIP的几何意义是，任何由 $\boldsymbol{A}$ 中不超过 $k$ 个列组成的子矩阵 $\boldsymbol{A}_S$都近似于一个**[等距同构](@entry_id:273188) (isometry)**，即它近似地保持了向量的欧几里得长度和任意两个向量之间的角度。当 $\delta_k$ 很小时，这些子矩阵的行为就非常像一个[正交基](@entry_id:264024)，它们所张成的[子空间](@entry_id:150286)之间的“纠缠”很小。

RIP为OMP的成功提供了更精细的保证。一个重要的结果是，如果矩阵 $\boldsymbol{A}$ 满足
$$
\delta_{k+1}  \frac{1}{\sqrt{k} + 1}
$$
那么[OMP算法](@entry_id:752901)保证能从无噪声的测量 $\boldsymbol{y} = \boldsymbol{A}\boldsymbol{x}^\star$ 中精确恢复任何 $k$-稀疏信号 $\boldsymbol{x}^\star$。这里的阶数为 $k+1$ 是因为[算法分析](@entry_id:264228)在每一步都需要考虑当前支撑集（最多 $k$ 个正确原子）与一个潜在的错误原子之间的关系。

### 更广阔的视角：OMP的定位与扩展

#### 与其他方法的比较

OMP作为一种贪婪算法，在[稀疏恢复](@entry_id:199430)的方法论版图中占据着一个特定位置 ：
- **$l_0$-最小化**: 这是“黄金标准”，旨在直接找到最稀疏的解。它能给出所有 $k$-项模型中最佳的预测，但因其[NP难](@entry_id:264825)的组合复杂性而在计算上不可行。
- **[基追踪](@entry_id:200728) (Basis Pursuit, BP) / $l_1$-最小化**: 这是一种**[凸松弛](@entry_id:636024) (convex relaxation)**方法。它用 $\ell_1$ 范数 $\|\boldsymbol{x}\|_1 = \sum_i |x_i|$ 替代难以处理的 $\ell_0$ “范数”，将问题转化为一个可以高效求解的凸[优化问题](@entry_id:266749)（通常是[线性规划](@entry_id:138188)）。BP寻求的是全局最优的 $\ell_1$ 范数解。
- **OMP**: 它既不像 $l_0$ 最小化那样寻求全局最优，也不像BP那样进行[凸松弛](@entry_id:636024)。它是一种前向选择的贪婪启发式算法，通过一系列局部最优决策来逼近 $l_0$ 问题。OMP的计算成本通常低于BP，尤其适用于稀疏度 $k$ 较小的情况。

#### 超越稀疏性：[可压缩信号](@entry_id:747592)

在许多实际应用中，信号并非严格稀疏，而是**可压缩的 (compressible)**。这意味着将其系数按大小排序后，数值会迅速衰减。对于这类信号，我们的目标不再是精确恢复，而是找到一个好的[稀疏近似](@entry_id:755090)。

OMP的机制天然地适应于处理[可压缩信号](@entry_id:747592)。因为其选择准则 $\arg\max_j |\langle \boldsymbol{a}_j, \boldsymbol{r}^{(t-1)} \rangle|$ 在低相关性字典中倾向于选择具有最大幅值系数的原子，OMP会自然地优先拾取信号中最重要的分量。理论表明，在一定条件下，OMP在 $k$ 步后得到的解 $\boldsymbol{\hat{x}}_k$ 是一个近乎最优的 $k$-项近似，其误差与最佳 $k$-项近似误差在同一个[数量级](@entry_id:264888)。

### 实际应用中的考量

#### [数值稳定性](@entry_id:146550)

OMP的核心计算步骤之一是求解[最小二乘问题](@entry_id:164198) $\min_{\boldsymbol{w}} \|\boldsymbol{y} - \boldsymbol{A}_S \boldsymbol{w}\|_2$。标准的教科书解法是构造并求解**[正规方程](@entry_id:142238) (normal equations)**：
$$
(\boldsymbol{A}_S^\top \boldsymbol{A}_S) \boldsymbol{w} = \boldsymbol{A}_S^\top \boldsymbol{y}
$$
然而，在有限精度计算中，这种方法可能存在严重的**数值不稳定性**。问题在于，当子矩阵 $\boldsymbol{A}_S$ 的列变得接近线性相关时（即 $\boldsymbol{A}_S$ 是病态的），矩阵 $\boldsymbol{A}_S^\top \boldsymbol{A}_S$ 的[条件数](@entry_id:145150)会急剧恶化。具体而言，其[条件数](@entry_id:145150)是原[矩阵条件数](@entry_id:142689)的平方：$\kappa_2(\boldsymbol{A}_S^\top \boldsymbol{A}_S) = (\kappa_2(\boldsymbol{A}_S))^2$。条件数的平方效应会放大舍入误差，导致计算出的系数 $\boldsymbol{w}$ 极其不准确。

一种数值上更稳健的方法是避免直接构造 $\boldsymbol{A}_S^\top \boldsymbol{A}_S$，而是使用**[QR分解](@entry_id:139154)**。通过对 $\boldsymbol{A}_S$ 进行QR分解得到 $\boldsymbol{A}_S = \boldsymbol{Q}\boldsymbol{R}$（其中 $\boldsymbol{Q}$ 是列[正交矩阵](@entry_id:169220)，$\boldsymbol{R}$ 是[上三角矩阵](@entry_id:150931)），最小二乘问题转化为求解一个良态的[上三角系统](@entry_id:635483)：
$$
\boldsymbol{R}\boldsymbol{w} = \boldsymbol{Q}^\top \boldsymbol{y}
$$
这个系统可以通过简单的[回代法](@entry_id:168868)稳定地求解。该方法的[数值稳定性](@entry_id:146550)来源于它操作的矩阵（如 $\boldsymbol{R}$）的[条件数](@entry_id:145150)与 $\boldsymbol{A}_S$ 相同，而非其平方。使用如[Householder变换](@entry_id:168808)等稳定算法计算[QR分解](@entry_id:139154)，可以保证整个求解过程的向后稳定性。对于高度病态的子问题，带[列主元选择](@entry_id:636812)的[QR分解](@entry_id:139154)提供了更强的鲁棒性。

#### 噪声环境下的[终止准则](@entry_id:136282)

在处理真实世界数据时，测量模型通常包含噪声：$\boldsymbol{y} = \boldsymbol{A}\boldsymbol{x}^\star + \boldsymbol{\varepsilon}$。在这种情况下，[OMP算法](@entry_id:752901)如果迭代次数过多，就会开始拟合噪声，导致过拟合。因此，选择一个合适的[终止准则](@entry_id:136282)至关重要。

以下是三种基于不同原理的标准终止策略：

1.  **已知稀疏度**: 最简单的情况是如果我们有关于真实信号稀疏度 $k$ 的先验知识。此时，我们只需运行[OMP算法](@entry_id:752901)恰好 $k$ 步即可。

2.  **[残差范数](@entry_id:754273)阈值**: 此策略基于**差异原则 (discrepancy principle)**。其思想是，一旦OMP找到了所有真实的信号分量，剩余的残差就应该只包含噪声的成分。如果我们知道噪声的统计特性（例如，$\boldsymbol{\varepsilon} \sim \mathcal{N}(\boldsymbol{0}, \sigma^2 \boldsymbol{I})$），我们就可以估计出这部分“纯噪声”残差的能量。具体来说，当支撑集 $S$ 被正确识别后，残差的平方范数 $\|\boldsymbol{r}^{(t)}\|_2^2$ 服从一个尺度化的 $\chi^2$ [分布](@entry_id:182848)，其期望约为 $(m-k)\sigma^2$。因此，我们可以设定一个阈值 $\tau$，当 $\|\boldsymbol{r}^{(t)}\|_2 \le \tau$ 时停止迭代，其中 $\tau$ 是根据 $\sigma$, $m$, $k$ 校准的。这可以有效防止算法对噪声进行[过拟合](@entry_id:139093)。

3.  **相关性显著性阈值**: 这种方法直接作用于OMP的选择步骤。在每一步，我们都要检验找到的最大相关性 $\gamma^{(t)} = \max_j |\langle \boldsymbol{a}_j, \boldsymbol{r}^{(t-1)} \rangle|$ 是否“统计显著”。我们建立一个[零假设](@entry_id:265441)：当前残差 $\boldsymbol{r}^{(t-1)}$ 中已不包含任何信号成分，完全是噪声。在该假设下，$\gamma^{(t)}$ 是多个（近似）高斯[随机变量](@entry_id:195330)[绝对值](@entry_id:147688)的最大值。我们可以从统计学上推断出这个最大值的[分布](@entry_id:182848)，并设定一个高[置信度](@entry_id:267904)的阈值 $\lambda$（例如，使用[Bonferroni校正](@entry_id:261239)或[极值理论](@entry_id:140083)）。如果观测到的 $\gamma^{(t)}$ 未能超过这个阈值，我们就有理由相信残差中不再有值得拾取的信号，从而终止算法。这种方法能够有效控制[错误发现率](@entry_id:270240)（即错误地将噪声相关的原子加入支撑集）。

这三种策略为在不同信息条件下应用OMP提供了灵活的框架，使其能够在拟合信号和避免过拟合之间取得合理的平衡。