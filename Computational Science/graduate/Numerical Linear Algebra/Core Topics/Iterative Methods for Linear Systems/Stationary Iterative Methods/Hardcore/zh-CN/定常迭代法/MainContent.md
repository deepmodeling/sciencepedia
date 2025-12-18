## 引言
在科学与工程计算的广阔领域中，求解形如 $A\boldsymbol{x}=\boldsymbol{b}$ 的大规模[线性方程组](@entry_id:148943)是一项无处不在的基础性任务。当系数矩阵 $A$ 巨大且稀疏时，传统的直接消元法因其高昂的计算和存储成本而变得不切实际。这促使我们转向迭代法，它通过从一个初始猜测出发，逐步逼近精确解，为解决这类问题提供了高效的途径。在众多迭代策略中，[定常迭代](@entry_id:755385)法（Stationary Iterative Methods）因其结构清晰、易于实现而构成了整个迭代法理论的基石。

然而，理解这些方法不仅仅是记住几个公式。其背后蕴含着深刻的数学原理：为何迭代会收敛？收敛的速度由什么决定？不同的方法之间有何内在联系？本文旨在填补理论与实践之间的鸿沟，系统性地解答这些问题。

本文将分为三个核心部分。在“原理与机制”一章中，我们将深入探索[定常迭代](@entry_id:755385)法的统一框架——矩阵分裂，并揭示其收敛性与[迭代矩阵](@entry_id:637346)谱半径之间的根本关系。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在[物理模拟](@entry_id:144318)、[网络分析](@entry_id:139553)、[图像处理](@entry_id:276975)乃至现代[高性能计算](@entry_id:169980)中发挥作用，并阐明它们作为更复杂算法基石的持久价值。最后，“动手实践”部分将提供一系列练习，帮助您将理论知识转化为解决实际问题的能力。

## 原理与机制

在上一章引言中，我们了解了求解大规模线性系统 $A\boldsymbol{x}=\boldsymbol{b}$ 的重要性，并初步接触了[迭代法](@entry_id:194857)作为直接法之外的一种有效途径。本章将深入探讨一类重要的[迭代法](@entry_id:194857)——**[定常迭代](@entry_id:755385)法 (stationary iterative methods)** 的核心原理与内在机制。我们将从一个统一的数学框架出发，揭示这些方法如何构造，并阐明其收敛性背后的深刻数学原理。

### [定常迭代](@entry_id:755385)法的一般框架：矩阵分裂

所有[定常迭代](@entry_id:755385)法的思想根源在于将原始方程 $A\boldsymbol{x}=\boldsymbol{b}$ 变形为一个等价的**[不动点方程](@entry_id:203270) (fixed-point equation)**，其形式为 $\boldsymbol{x} = T\boldsymbol{x} + \boldsymbol{c}$。一旦获得这种形式，我们就可以从一个初始猜测 $\boldsymbol{x}^{(0)}$ 开始，通过迭代公式 $\boldsymbol{x}^{(k+1)} = T\boldsymbol{x}^{(k)} + \boldsymbol{c}$ 生成一个向量序列 $\{\boldsymbol{x}^{(k)}\}$。如果这个序列收敛，其极限 $\boldsymbol{x}^*$ 必然满足 $\boldsymbol{x}^* = T\boldsymbol{x}^* + \boldsymbol{c}$，从而也是原始方程的解。

实现这种转化的关键技巧是**矩阵分裂 (matrix splitting)**。我们选择一个非奇异矩阵 $M$，将矩阵 $A$ 分解为两个矩阵的差：

$A = M - N$

将此分裂代入原方程 $A\boldsymbol{x}=\boldsymbol{b}$，得到 $(M-N)\boldsymbol{x} = \boldsymbol{b}$，即 $M\boldsymbol{x} = N\boldsymbol{x} + \boldsymbol{b}$。这个形式启发我们构造如下的迭代格式：

$M\boldsymbol{x}^{(k+1)} = N\boldsymbol{x}^{(k)} + \boldsymbol{b}$

由于 $M$ 是非奇异的，我们可以通过求解一个以 $M$ 为系数矩阵的[线性系统](@entry_id:147850)（理想情况下，$M$ 的结构应使这个求解过程非常高效，例如对角或[三角矩阵](@entry_id:636278)）来得到 $\boldsymbol{x}^{(k+1)}$。为了进行理论分析，我们通常将其写为显式形式：

$\boldsymbol{x}^{(k+1)} = M^{-1}N\boldsymbol{x}^{(k)} + M^{-1}\boldsymbol{b}$

这正是我们所寻求的[不动点迭代](@entry_id:749443)形式。我们定义：

- **[迭代矩阵](@entry_id:637346) (iteration matrix)**: $T = M^{-1}N$
- **常数向量 (constant vector)**: $\boldsymbol{c} = M^{-1}\boldsymbol{b}$

因此，任何基于矩阵分裂的[定常迭代](@entry_id:755385)法都可以统一表达为 $\boldsymbol{x}^{(k+1)} = T\boldsymbol{x}^{(k)} + \boldsymbol{c}$。

一个重要的问题是：这个迭代过程的[不动点](@entry_id:156394)是否就是我们想要的解？假设 $\boldsymbol{x}^*$ 是迭代的一个[不动点](@entry_id:156394)，那么 $\boldsymbol{x}^* = T\boldsymbol{x}^* + \boldsymbol{c}$。代入 $T$ 和 $\boldsymbol{c}$ 的定义，我们有 $\boldsymbol{x}^* = (M^{-1}N)\boldsymbol{x}^* + M^{-1}\boldsymbol{b}$。用 $M$ 左乘等式两边，得到 $M\boldsymbol{x}^* = N\boldsymbol{x}^* + \boldsymbol{b}$，整理后即 $(M-N)\boldsymbol{x}^* = \boldsymbol{b}$。由于 $A=M-N$，这等价于 $A\boldsymbol{x}^*=\boldsymbol{b}$。反之，如果 $A\boldsymbol{x}^*=\boldsymbol{b}$，通过相同的步骤可以推导出 $\boldsymbol{x}^* = T\boldsymbol{x}^* + \boldsymbol{c}$。这证明了迭代过程的[不动点](@entry_id:156394)集合与原[线性系统](@entry_id:147850)的[解集](@entry_id:154326)是完全相同的。如果 $A$ 是非奇异的，那么系统存在唯一解 $\boldsymbol{x}^*=A^{-1}\boldsymbol{b}$，这个解也就是迭代过程的唯一[不动点](@entry_id:156394) 。

[迭代矩阵](@entry_id:637346) $T$ 也可以用 $A$ 和 $M$ 表示。由 $N=M-A$ 可得，$T = M^{-1}(M-A) = I - M^{-1}A$。这个形式在某些理论推导中更为方便 。

### 收敛性原理：[误差分析](@entry_id:142477)与[谱半径](@entry_id:138984)

确定了迭代法的构造框架后，下一个核心问题是：迭代序列 $\{\boldsymbol{x}^{(k)}\}$ 是否收敛于真解 $\boldsymbol{x}^*$？如果收敛，其收敛速度如何？

为了回答这个问题，我们引入**误差向量 (error vector)**，定义为 $\boldsymbol{e}^{(k)} = \boldsymbol{x}^* - \boldsymbol{x}^{(k)}$。我们来考察误差是如何从一步迭代传递到下一步的。我们有两个方程：
1. 真解满足的[不动点方程](@entry_id:203270): $\boldsymbol{x}^* = T\boldsymbol{x}^* + \boldsymbol{c}$
2. 第 $k$ 步的迭代公式: $\boldsymbol{x}^{(k+1)} = T\boldsymbol{x}^{(k)} + \boldsymbol{c}$

将两式相减，得到：
$\boldsymbol{x}^* - \boldsymbol{x}^{(k+1)} = (T\boldsymbol{x}^* + \boldsymbol{c}) - (T\boldsymbol{x}^{(k)} + \boldsymbol{c}) = T(\boldsymbol{x}^* - \boldsymbol{x}^{(k)})$

根据误差的定义，上式可以写成一个简洁而深刻的关系：

$\boldsymbol{e}^{(k+1)} = T \boldsymbol{e}^{(k)}$

这个公式被称为**[误差传播](@entry_id:147381)方程 (error propagation equation)** 。它表明，在每次迭代中，误差向量完全按照[迭代矩阵](@entry_id:637346) $T$ 的[线性变换](@entry_id:149133)进行演化。通过递推，我们可以得到 $\boldsymbol{e}^{(k)} = T^k \boldsymbol{e}^{(0)}$。

[迭代法](@entry_id:194857)收敛，意味着对于任意的初始误差 $\boldsymbol{e}^{(0)}$（即对于任意的初始猜测 $\boldsymbol{x}^{(0)}$），当 $k \to \infty$ 时，误差向量 $\boldsymbol{e}^{(k)}$ 都趋向于零向量。这等价于要求矩阵的幂 $T^k$ 随着 $k$ 的增大而趋向于零矩阵。

线性代数中的一个基本定理给出了这一极限行为的精确判断标准。矩阵序列 $\{T^k\}$ 当且仅当 $T$ 的所有[特征值](@entry_id:154894)的模长都严格小于 $1$ 时，才收敛于[零矩阵](@entry_id:155836)。我们将一个矩阵 $T$ 的所有[特征值](@entry_id:154894) $\{\lambda_i\}$ 模长的最大值，定义为其**[谱半径](@entry_id:138984) (spectral radius)**，记作 $\rho(T)$。

$\rho(T) = \max_i \{|\lambda_i|\}$

至此，我们得到了[定常迭代](@entry_id:755385)法收敛的根本判据：

**[定常迭代](@entry_id:755385)法 $\boldsymbol{x}^{(k+1)} = T\boldsymbol{x}^{(k)} + \boldsymbol{c}$ 对任意初始向量 $\boldsymbol{x}^{(0)}$ 收敛的充分必要条件是，其[迭代矩阵](@entry_id:637346)的[谱半径](@entry_id:138984)严格小于 $1$，即 $\rho(T)  1$。**  

这个条件是[定常迭代](@entry_id:755385)法理论的基石。如果 $\rho(T) \ge 1$，则至少存在一个特征方向，使得误差在该方向上的分量不会衰减，导致迭代无法保证对所有初始猜测都收敛。例如，即使 $\rho(T)=1$，也无法保证收敛 。

让我们通过一个具体的例子来应用这个原理。假设一个迭代过程的[迭代矩阵](@entry_id:637346)为：
$T = \begin{pmatrix} 0   2 \\ 0   0.4 \end{pmatrix}$
这是一个[上三角矩阵](@entry_id:150931)，其[特征值](@entry_id:154894)就是对角线上的元素，即 $\lambda_1 = 0$ 和 $\lambda_2 = 0.4$。该矩阵的谱半径为 $\rho(T) = \max\{|0|, |0.4|\} = 0.4$。由于 $\rho(T) = 0.4  1$，我们可以断定，与该[迭代矩阵](@entry_id:637346)对应的任何[定常迭代](@entry_id:755385)法都将收敛 。

### 经典[迭代法](@entry_id:194857)：分裂思想的应用

矩阵分裂 $A=M-N$ 的选择不是唯一的。不同的[分裂选择](@entry_id:139946)定义了不同的迭代法，它们的[迭代矩阵](@entry_id:637346) $T=M^{-1}N$ 也不同，因此收敛特性也可能截然不同。下面我们介绍几种基于特定分裂方式的经典方法。为此，我们首先将矩阵 $A$ 分解为其对角部分 $D$、严格下三角部分 $-L$ 和严格上三角部分 $-U$ 的和，即 $A = D - L - U$。这里，$D$ 是一个[对角矩阵](@entry_id:637782)，$L$ 是一个严格下三角矩阵，$U$ 是一个严格[上三角矩阵](@entry_id:150931)。

#### 雅可比 (Jacobi) 方法

[雅可比方法](@entry_id:270947)是最直观的[迭代法](@entry_id:194857)之一。它的思想是在求解第 $i$ 个分量 $x_i$ 时，将方程 $A\boldsymbol{x}=\boldsymbol{b}$ 的第 $i$ 行中所有其他分量 $x_j (j \ne i)$ 都暂时使用上一步的迭代值 $\boldsymbol{x}^{(k)}$。写成方程形式为：
$a_{ii}x_i^{(k+1)} = b_i - \sum_{j \ne i} a_{ij}x_j^{(k)}$

将所有 $n$ 个这样的方程写成矩阵形式，等式左边对应于 $D\boldsymbol{x}^{(k+1)}$，右边对应于 $(L+U)\boldsymbol{x}^{(k)} + \boldsymbol{b}$。因此，[雅可比方法](@entry_id:270947)的迭代格式为：
$D\boldsymbol{x}^{(k+1)} = (L+U)\boldsymbol{x}^{(k)} + \boldsymbol{b}$

这对应于一种矩阵分裂，其中 $M=D$，$N=L+U$。由此，[雅可比方法](@entry_id:270947)的[迭代矩阵](@entry_id:637346)和常数向量为：
$T_J = D^{-1}(L+U) = I - D^{-1}A$
$\boldsymbol{c}_J = D^{-1}\boldsymbol{b}$


[雅可比法](@entry_id:147508)的优点是所有分量 $x_i^{(k+1)}$ 可以[并行计算](@entry_id:139241)，因为它只依赖于旧的向量 $\boldsymbol{x}^{(k)}$。

#### 高斯-赛德尔 (Gauss-Seidel) 方法

高斯-赛德尔方法是对[雅可比方法](@entry_id:270947)的一个自然改进。在计算第 $i$ 个分量 $x_i^{(k+1)}$ 时，对于那些已经计算出来的、属于当前迭代步的新分量 $x_j^{(k+1)} (j  i)$，我们立即使用它们，而不是继续使用旧值。其分量形式为：
$a_{ii}x_i^{(k+1)} = b_i - \sum_{j=1}^{i-1} a_{ij}x_j^{(k+1)} - \sum_{j=i+1}^{n} a_{ij}x_j^{(k)}$

将这个更新规则写成矩阵形式，等式左边涉及到了 $\boldsymbol{x}^{(k+1)}$ 的下三角部分，对应于 $D\boldsymbol{x}^{(k+1)} - L\boldsymbol{x}^{(k+1)} = (D-L)\boldsymbol{x}^{(k+1)}$。等式右边则对应于 $U\boldsymbol{x}^{(k)} + \boldsymbol{b}$。于是，高斯-赛德尔方法的迭代格式是：
$(D-L)\boldsymbol{x}^{(k+1)} = U\boldsymbol{x}^{(k)} + \boldsymbol{b}$

这定义了另一种矩阵分裂，其中 $M = D-L$，$N=U$。因此，高斯-赛德尔方法的[迭代矩阵](@entry_id:637346)为：
$T_{GS} = (D-L)^{-1}U$


由于[高斯-赛德尔法](@entry_id:145727)总是利用最新的信息，人们直观上会感觉它比[雅可比法](@entry_id:147508)收敛得更快。在很多情况下确实如此，但并非总是。

#### 逐次超松弛 (SOR) 方法与分裂的多样性

SOR 方法可以看作是高斯-赛德尔方法的一种推广，它引入了一个**松弛因子 (relaxation parameter)** $\omega > 0$ 来加速收敛。其思想是在计算出高斯-赛德尔的增量后，对其进行缩放。SOR 方法的分裂定义相对复杂一些：
$M = \frac{1}{\omega}(D - \omega L)$
$N = \frac{1}{\omega}((1-\omega)D + \omega U)$

对应的[迭代矩阵](@entry_id:637346)为 $T_{SOR}(\omega) = (D-\omega L)^{-1}((1-\omega)D + \omega U)$。当 $\omega=1$ 时，SOR 方法就退化为高斯-赛德尔方法。

SOR 方法的存在清晰地表明，对于同一个矩阵 $A$，我们可以有无穷多种分裂方式（通过改变 $\omega$）。不同的分裂会导致不同的[迭代矩阵](@entry_id:637346)和收敛行为。一个迭代法收敛与否，并不完全取决于矩阵 $A$ 本身，而是强烈地依赖于我们选择的**分裂方式**。

例如，对于矩阵 $A = \begin{pmatrix} 2  -1 \\ -1  2 \end{pmatrix}$，当选择 $\omega=1$（即[高斯-赛德尔法](@entry_id:145727)）时，[迭代矩阵](@entry_id:637346)的[谱半径](@entry_id:138984)为 $\rho(T_{GS})=0.25  1$，方法收敛。然而，如果选择 $\omega=2.5$，计算可得[迭代矩阵](@entry_id:637346)的[谱半径](@entry_id:138984)为 $\rho(T_{SOR}(2.5))=1.5 > 1$，此时方法发散。这有力地说明了选择合适的分裂（或参数）对于保证收敛至关重要 。

### 收敛性的充分条件

[谱半径](@entry_id:138984)是判断收敛的最终标准，但计算[谱半径](@entry_id:138984)通常需要求解特征值问题，这本身可能就很困难。因此，在实践中，能够直接通过矩阵 $A$ 的性质来判断收敛性的**充分条件**非常有价值。

一个重要且易于验证的条件是**对角占优 (diagonal dominance)**。
- 如果一个矩阵 $A$ 对于每一行 $i$，其对角元 $a_{ii}$ 的[绝对值](@entry_id:147688)都**严格大于**该行所有非对角元[绝对值](@entry_id:147688)之和，即 $|a_{ii}| > \sum_{j \neq i} |a_{ij}|$，则称 $A$ 是**[严格对角占优](@entry_id:154277) (strictly diagonally dominant)** 的。
- 如果上述条件中的“>”替换为“≥”，且至少对于一个 $i$ 不等式严格成立，并且 $A$ 是**不可约 (irreducible)** 的（即无法通过行和列的重新[排列](@entry_id:136432)变成块上三角形式），则称 $A$ 是**不可约[对角占优](@entry_id:748380) (irreducibly diagonally dominant)** 的。

一个重要的定理（Taussky 定理）指出：
**如果矩阵 $A$ 是[严格对角占优](@entry_id:154277)或不可约[对角占优](@entry_id:748380)的，那么[雅可比方法](@entry_id:270947)和高斯-赛德尔方法都收敛。**

例如，矩阵 $A = \begin{pmatrix} 2  -1  -1 \\ -1  3  -1 \\ -1  -1  3 \end{pmatrix}$ 是不可约[对角占优](@entry_id:748380)的（第1行是等号，但第2、3行是严格不等，且矩阵不可约），可以验证其[雅可比迭代](@entry_id:139235)矩阵的[谱半径](@entry_id:138984) $\rho(T_J) = \frac{1+\sqrt{13}}{6} \approx 0.767  1$，因此[雅可比方法](@entry_id:270947)收敛。这个例子证实了该定理的应用 。需要注意的是，如果矩阵只是弱[对角占优](@entry_id:748380)（即所有行都是“≥”且无严格大于）并且是可约的，收敛性则无法保证。

### 深入探讨：收敛过程的动态与细微之处

谱半径 $\rho(T)1$ 保证了误差最终会趋于零，即**渐近收敛 (asymptotic convergence)**。然而，在迭代的初始阶段，误差的行为可能更为复杂。

#### 残差动态及其与误差的关系

误差向量 $\boldsymbol{e}^{(k)} = \boldsymbol{x}^* - \boldsymbol{x}^{(k)}$ 是一个理论分析工具，但在实际计算中我们无法得到它，因为真解 $\boldsymbol{x}^*$ 是未知的。一个可以计算的、用于监控收敛过程的量是**残差向量 (residual vector)**：

$\boldsymbol{r}^{(k)} = \boldsymbol{b} - A\boldsymbol{x}^{(k)}$

残差衡量了当前近似解 $\boldsymbol{x}^{(k)}$ 在多大程度上满足原方程。误差和残差之间存在一个直接的[线性关系](@entry_id:267880)。因为 $\boldsymbol{b}=A\boldsymbol{x}^*$，所以：

$\boldsymbol{r}^{(k)} = A\boldsymbol{x}^* - A\boldsymbol{x}^{(k)} = A(\boldsymbol{x}^* - \boldsymbol{x}^{(k)}) = A\boldsymbol{e}^{(k)}$

由于 $A$ 是非奇异的，我们也有 $\boldsymbol{e}^{(k)} = A^{-1}\boldsymbol{r}^{(k)}$ 。这个关系表明，误差和残差的范数是等价的，即一个趋于零当且仅当另一个也趋于零。

我们还可以推导残差的传播规律。
$\boldsymbol{r}^{(k+1)} = A\boldsymbol{e}^{(k+1)} = A(T\boldsymbol{e}^{(k)}) = A T (A^{-1}\boldsymbol{r}^{(k)}) = (ATA^{-1})\boldsymbol{r}^{(k)}$

这说明残差以矩阵 $S = ATA^{-1}$ 的方式传播。矩阵 $S$ 与[迭代矩阵](@entry_id:637346) $T$ 是**相似 (similar)** 的。[相似矩阵](@entry_id:155833)有相同的[特征值](@entry_id:154894)，因此也有相同的谱半径。这意味着，分析误差的收敛性与分析残差的收敛性是等价的，$\rho(S)=\rho(T)1$ 同为收敛的充要条件。

#### 瞬态增长与[非正规矩阵](@entry_id:752668)

即使 $\rho(T)  1$，[误差范数](@entry_id:176398) $\|\boldsymbol{e}^{(k)}\|$ 并非总是单调递减的。在迭代的初期，[误差范数](@entry_id:176398)可能会出现短暂的增长，这种现象称为**瞬态增长 (transient growth)**。

这种现象的根源在于[迭代矩阵](@entry_id:637346) $T$ 的**[非正规性](@entry_id:752585) (non-normality)**。
- 一个矩阵 $T$ 如果满足 $T T^* = T^* T$（其中 $T^*$ 是 $T$ 的[共轭转置](@entry_id:147909)），则被称为**[正规矩阵](@entry_id:185943) (normal matrix)**。
- 否则，称为**[非正规矩阵](@entry_id:752668) (non-normal matrix)**。

对于[正规矩阵](@entry_id:185943)，其[谱范数](@entry_id:143091)（[2-范数](@entry_id:636114)）等于其[谱半径](@entry_id:138984)，即 $\|T\|_2 = \rho(T)$。因此，[误差范数](@entry_id:176398)的演化满足：
$\|\boldsymbol{e}^{(k+1)}\|_2 = \|T\boldsymbol{e}^{(k)}\|_2 \le \|T\|_2 \|\boldsymbol{e}^{(k)}\|_2 = \rho(T)\|\boldsymbol{e}^{(k)}\|_2$
如果 $\rho(T)1$，则[误差范数](@entry_id:176398)序列 $\|\boldsymbol{e}^{(k)}\|_2$ 是严格单调递减的，不会发生瞬态增长 。

然而，对于[非正规矩阵](@entry_id:752668)，[谱范数](@entry_id:143091)可能远大于谱半径，即 $\|T\|_2 > \rho(T)$。在这种情况下，尽管 $\rho(T)1$ 保证了长期来看 $\|\boldsymbol{e}^{(k)}\|_2 \to 0$，但在短期内，由于 $\|T\|_2 > 1$，可能会出现 $\|\boldsymbol{e}^{(k+1)}\|_2 > \|\boldsymbol{e}^{(k)}\|_2$ 的情况。

一个典型的例子是 $2 \times 2$ 的若尔当块 ([Jordan block](@entry_id:148136)):
$T = \begin{pmatrix} \alpha  1 \\ 0  \alpha \end{pmatrix}$, 其中 $0  \alpha  1$

这个矩阵是高度非正规的，其[谱半径](@entry_id:138984) $\rho(T) = \alpha  1$。它的幂次为 $T^k = \begin{pmatrix} \alpha^k  k\alpha^{k-1} \\ 0  \alpha^k \end{pmatrix}$。虽然当 $k \to \infty$ 时 $T^k \to 0$，但由于非对角线上的项 $k\alpha^{k-1}$ 的存在，当 $\alpha$ 接近 $1$ 时，这一项在 $k$ 较小时会先增大后减小。这种行为导致了[矩阵范数](@entry_id:139520) $\|T^k\|_2$ 的瞬态增长，从而可能导致某些初始误差[向量的范数](@entry_id:154882)在迭代初期增大 。例如，取 $\alpha=0.7$，初始误差为 $\boldsymbol{e}^{(0)} = \begin{pmatrix} 0 \\ 1 \end{pmatrix}$，那么 $\|\boldsymbol{e}^{(0)}\|_2=1$，而 $\boldsymbol{e}^{(1)} = T\boldsymbol{e}^{(0)} = \begin{pmatrix} 1 \\ 0.7 \end{pmatrix}$，其范数 $\|\boldsymbol{e}^{(1)}\|_2 = \sqrt{1.49} > 1$。

一个可[对角化](@entry_id:147016)的[非正规矩阵](@entry_id:752668)的瞬态增长潜力，可以通过其[特征向量](@entry_id:151813)矩阵 $V$ 的**[条件数](@entry_id:145150) (condition number)** $\kappa(V) = \|V\|_2 \|V^{-1}\|_2$ 来衡量。[误差范数](@entry_id:176398)满足不等式 $\|\boldsymbol{e}^{(k)}\|_2 \le \kappa_2(V) \rho(T)^k \|\boldsymbol{e}^{(0)}\|_2$。当 $\kappa_2(V)$ 很大时（这是[非正规性](@entry_id:752585)的一个标志），即使 $\rho(T)$ 很小，初始的放大因子 $\kappa_2(V)$ 也可能导致[误差范数](@entry_id:176398)在开始时出现显著增长 。

理解瞬态增长现象对于在[有限精度算术](@entry_id:142321)中解释[迭代法](@entry_id:194857)的行为，以及在误差容限要求严格的应用中设置[停止准则](@entry_id:136282)，都具有重要的实践意义。