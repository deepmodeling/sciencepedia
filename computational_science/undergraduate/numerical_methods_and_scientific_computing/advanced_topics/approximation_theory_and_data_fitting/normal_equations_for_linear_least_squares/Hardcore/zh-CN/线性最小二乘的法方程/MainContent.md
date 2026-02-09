## 引言
在科学探索与工程实践中，我们经常需要从充满噪声的实验数据中构建数学模型。这些问题通常可以简化为求解一个线性方程组 $A\mathbf{x} = \mathbf{b}$。然而，由于测量误差，数据点往往过多且不完全一致，导致方程组成为一个无精确解的超定系统。此时，我们追求的不再是精确解，而是一个能最好地“拟合”数据的“最优”近似解。线性最小二乘法为此提供了一个强大而直观的框架，而正规方程（Normal Equations）正是求解该问题的核心工具。

本文旨在系统性地阐述线性最小二乘问题的正规方程法。我们不仅会揭示其数学推导和几何本质，还会探讨其在广泛的跨学科领域中的实际应用，并指出其在数值计算中的关键考量。

在接下来的内容中，我们将分三步深入学习：首先，在“原理与机制”一章中，我们将从微积分和线性代数的角度推导正规方程，探讨解的存在性与唯一性，并分析其数值稳定性问题。接着，在“应用与跨学科联系”一章中，我们将通过物理参数估计、模型线性化和信号处理等丰富案例，展示如何将现实世界的问题转化为最小二乘框架并加以解决。最后，“动手实践”部分将提供一系列精心设计的问题，引导您亲手应用正规方程进行数据拟合与分析，从而将理论知识内化为实践能力。

## 原理与机制

在处理许多科学和工程问题时，我们常常需要从一组实验数据中拟合出一个数学模型。这些问题通常可以被表述为一个线性方程组 $A\mathbf{x} = \mathbf{b}$。然而，由于测量误差的存在，数据点（构成 $\mathbf{b}$ 和可能的 $A$）往往带有噪声，导致方程组超定（即方程数量 $m$ 大于未知数数量 $n$）且不相容（即无精确解）。在这种情况下，我们的目标不再是寻找一个精确满足所有方程的解 $\mathbf{x}$，而是寻找一个“最佳”的近似解。最小二乘法为此提供了一个强大而直观的框架：它定义“最佳”解 $\hat{\mathbf{x}}$ 为那个能够最小化残差向量 $\mathbf{r} = A\mathbf{x} - \mathbf{b}$ 的欧几里得范数（长度）的平方的解。本章将深入探讨导出该解的核心工具——正规方程（Normal Equations）的原理与机制。

### 最小二乘原理与正规方程的推导

线性最小二乘问题的核心目标是找到一个向量 $\hat{\mathbf{x}} \in \mathbb{R}^n$，使得误差的平方和 $S(\mathbf{x})$ 最小。这个误差平方和就是残差向量 $A\mathbf{x} - \mathbf{b}$ 的欧几里得范数的平方：

$$ S(\mathbf{x}) = \|A\mathbf{x} - \mathbf{b}\|_2^2 $$

为了找到使 $S(\mathbf{x})$ 最小的 $\mathbf{x}$，我们可以利用多元微积分的知识。首先，我们将范数的平方展开为向量的转置与其自身的乘积：

$$ S(\mathbf{x}) = (A\mathbf{x} - \mathbf{b})^T (A\mathbf{x} - \mathbf{b}) $$

展开这个表达式，我们得到：

$$ S(\mathbf{x}) = (\mathbf{x}^T A^T - \mathbf{b}^T)(A\mathbf{x} - \mathbf{b}) = \mathbf{x}^T A^T A \mathbf{x} - \mathbf{x}^T A^T \mathbf{b} - \mathbf{b}^T A \mathbf{x} + \mathbf{b}^T \mathbf{b} $$

注意到 $\mathbf{x}^T A^T \mathbf{b}$ 是一个标量，因此它等于其自身的转置 $(\mathbf{x}^T A^T \mathbf{b})^T = \mathbf{b}^T A \mathbf{x}$。所以，上述表达式可以简化为：

$$ S(\mathbf{x}) = \mathbf{x}^T (A^T A) \mathbf{x} - 2 \mathbf{x}^T (A^T \mathbf{b}) + \mathbf{b}^T \mathbf{b} $$

这是一个关于 $\mathbf{x}$ 的二次型。为了找到其最小值，我们计算 $S(\mathbf{x})$ 相对于向量 $\mathbf{x}$ 的梯度 $\nabla_{\mathbf{x}} S(\mathbf{x})$，并令其为零向量。利用矩阵微积分的法则，我们得到：

$$ \nabla_{\mathbf{x}} S(\mathbf{x}) = 2 (A^T A) \mathbf{x} - 2 A^T \mathbf{b} $$

令梯度为零，$\nabla_{\mathbf{x}} S(\mathbf{x}) = \mathbf{0}$，我们得到：

$$ 2 (A^T A) \hat{\mathbf{x}} - 2 A^T \mathbf{b} = \mathbf{0} $$

简化后，便得到了著名的**正规方程**（Normal Equations）：

$$ A^T A \hat{\mathbf{x}} = A^T \mathbf{b} $$

任何满足最小二乘准则的解 $\hat{\mathbf{x}}$ 都必须满足这个方程组 [@problem_id:2218999]。这是一个包含 $n$ 个未知数和 $n$ 个方程的线性方程组，其系数矩阵 $A^T A$ 是一个 $n \times n$ 的方阵。

### 正规方程的构建实践

正规方程的应用始于根据给定的模型和数据构建矩阵 $A$ 和向量 $\mathbf{b}$。对于一个一般的线性模型，其形式为 $y \approx c_1 f_1(\mathbf{z}) + c_2 f_2(\mathbf{z}) + \dots + c_n f_n(\mathbf{z})$，其中 $f_j$ 是已知的基函数，$\mathbf{z}$ 是自变量，而 $c_j$ 是待求的系数。对于第 $i$ 个数据点 $(\mathbf{z}_i, y_i)$，我们有方程 $y_i \approx \sum_{j=1}^n c_j f_j(\mathbf{z}_i)$。

将所有 $m$ 个数据点写成矩阵形式 $A\mathbf{x} \approx \mathbf{b}$，其中 $\mathbf{x} = [c_1, c_2, \dots, c_n]^T$ 是未知系数向量，$\mathbf{b} = [y_1, y_2, \dots, y_m]^T$ 是观测值向量。设计矩阵 $A$ 的每一行对应一个数据点，每一列对应一个基函数。具体来说，$A$ 的第 $i$ 行、第 $j$ 列的元素是 $A_{ij} = f_j(\mathbf{z}_i)$。

**示例 1：简单线性回归**
一个最常见的例子是拟合一条直线 $y \approx \beta_0 + \beta_1 x$。这里有两个基函数：$f_1(x) = 1$ 和 $f_2(x) = x$。未知系数向量是 $\boldsymbol{\beta} = [\beta_0, \beta_1]^T$。对于 $m$ 个数据点 $(x_i, y_i)$，设计矩阵 $A$ 和向量 $\mathbf{y}$ 分别为：
$$
A = \begin{pmatrix}
1 & x_1 \\
1 & x_2 \\
\vdots & \vdots \\
1 & x_m
\end{pmatrix}, \quad
\mathbf{y} = \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_m \end{pmatrix}
$$
正规方程的系数矩阵 $A^T A$ 和右侧向量 $A^T \mathbf{y}$ 可以通过矩阵乘法直接计算 [@problem_id:2217991]：
$$
A^T A = \begin{pmatrix} \sum_{i=1}^m 1 & \sum_{i=1}^m x_i \\ \sum_{i=1}^m x_i & \sum_{i=1}^m x_i^2 \end{pmatrix} = \begin{pmatrix} m & \sum x_i \\ \sum x_i & \sum x_i^2 \end{pmatrix}
$$
$$
A^T \mathbf{y} = \begin{pmatrix} \sum_{i=1}^m y_i \\ \sum_{i=1}^m x_i y_i \end{pmatrix}
$$
求解这个 $2 \times 2$ 的线性方程组即可得到最佳的截距 $\beta_0$ 和斜率 $\beta_1$。

**示例 2：更复杂的线性模型**
考虑一个物理系统，其位移模型为 $y(t) = c_1 \sin(\omega t) + c_2 \cos(\omega t) + c_3 t$ [@problem_id:2218999]。这里的基函数是 $f_1(t) = \sin(\omega t)$，$f_2(t) = \cos(\omega t)$ 和 $f_3(t) = t$。设计矩阵 $A$ 的第 $k$ 行就是 $[\sin(\omega t_k), \cos(\omega t_k), t_k]$。
正规方程的系数矩阵 $M = A^T A$ 的元素 $M_{ij}$ 是 $A$ 的第 $i$ 列和第 $j$ 列的内积（点积）。例如，要计算 $M$ 的第一行第三列元素 $M_{13}$，我们需要计算 $A$ 的第一列（对应 $c_1$ 的基函数 $\sin(\omega t)$）和第三列（对应 $c_3$ 的基函数 $t$）的内积：
$$
M_{13} = \sum_{k=1}^{m} A_{k1} A_{k3} = \sum_{k=1}^{m} \sin(\omega t_k) \cdot t_k
$$
通过这种方式，我们可以为任何线性模型系统地构建正规方程。

### 正规方程的几何解释

正规方程背后蕴含着深刻的几何意义。向量 $\mathbf{b}$ 通常不在矩阵 $A$ 的列空间 $\text{Col}(A)$ 中，这就是方程组不相容的原因。$\text{Col}(A)$ 是由 $A$ 的列向量所有可能的线性组合构成的子空间。任何形如 $A\mathbf{x}$ 的向量都必定位于 $\text{Col}(A)$ 内。

最小二乘法寻找的向量 $\hat{\mathbf{x}}$，使得 $A\hat{\mathbf{x}}$ 成为 $\text{Col}(A)$ 中距离 $\mathbf{b}$ 最近的向量。在欧几里得空间中，“最近”意味着连接这两个点的向量（即残差向量 $\mathbf{r} = \mathbf{b} - A\hat{\mathbf{x}}$）必须与目标子空间（即 $\text{Col}(A)$）正交。

一个向量若要与一个子空间正交，它必须与该子空间的任意基向量都正交。$A$ 的列向量 $\mathbf{a}_1, \mathbf{a}_2, \dots, \mathbf{a}_n$ 构成了 $\text{Col}(A)$ 的一组基。因此，残差向量 $\mathbf{r}$ 必须与每一个 $\mathbf{a}_j$ 都正交 [@problem_id:2217998]。用内积表示，即：
$$ \mathbf{a}_j^T \mathbf{r} = 0 \quad \text{for } j=1, 2, \dots, n $$
我们可以将这 $n$ 个正交条件写成一个紧凑的矩阵形式。将 $A$ 的列向量的转置作为行向量堆叠起来，就得到了 $A^T$：
$$
A^T \mathbf{r} = \begin{pmatrix} \mathbf{a}_1^T \\ \mathbf{a}_2^T \\ \vdots \\ \mathbf{a}_n^T \end{pmatrix} \mathbf{r} = \begin{pmatrix} \mathbf{a}_1^T \mathbf{r} \\ \mathbf{a}_2^T \mathbf{r} \\ \vdots \\ \mathbf{a}_n^T \mathbf{r} \end{pmatrix} = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ 0 \end{pmatrix} = \mathbf{0}
$$
于是我们得到了正交性条件 $A^T \mathbf{r} = \mathbf{0}$。将残差的定义 $\mathbf{r} = \mathbf{b} - A\hat{\mathbf{x}}$ 代入，便得到：
$$ A^T(\mathbf{b} - A\hat{\mathbf{x}}) = \mathbf{0} $$
这与我们通过微积分方法推导出的正规方程 $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$ 完全等价。因此，正规方程的本质就是强制残差向量与 $A$ 的列空间正交。

这个正交性是最小二乘解的一个基本性质，我们可以通过一个具体的例子来验证它 [@problem_id:2218002]。残差向量 $\mathbf{r}$ 既然与 $\text{Col}(A)$ 中的所有向量都正交，那么它一定属于 $\text{Col}(A)$ 的正交补空间，即 $\text{Col}(A)^\perp$。根据线性代数基本定理，这个空间恰好是 $A$ 的转置的零空间，即 $\mathcal{N}(A^T)$。因此，一个向量 $\mathbf{v}$ 可能成为某个最小二乘问题的残差向量的充要条件是 $\mathbf{v} \in \mathcal{N}(A^T)$，也就是 $A^T \mathbf{v} = \mathbf{0}$ [@problem_id:2218028]。

### 解的存在性与唯一性

在建立正规方程后，我们自然会问：这个方程组是否总是有解？如果存在解，它是否是唯一的？

**存在性**
答案是肯定的：正规方程 $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$ 对于任意的矩阵 $A$ 和向量 $\mathbf{b}$ **总是相容的**，即总存在至少一个解。
一个线性系统 $M\mathbf{x} = \mathbf{v}$ 有解的充要条件是 $\mathbf{v}$ 位于 $M$ 的列空间中，即 $\mathbf{v} \in \text{range}(M)$。对于正规方程，这意味着我们需要验证 $A^T\mathbf{b}$ 是否总在 $A^T A$ 的列空间中。一个关键的线性代数结论是，对于任何矩阵 $A$，其转置的列空间与 $A^T A$ 的列空间是相同的，即 $\text{range}(A^T) = \text{range}(A^T A)$。因为向量 $A^T \mathbf{b}$ 根据其定义显然属于 $\text{range}(A^T)$，所以它也必然属于 $\text{range}(A^T A)$。这就保证了正规方程总是有解的 [@problem_id:2217999]。

**唯一性**
正规方程的解是否唯一，取决于系数矩阵 $A^T A$ 是否可逆。如果 $A^T A$ 可逆，那么存在唯一的解 $\hat{\mathbf{x}} = (A^T A)^{-1} A^T \mathbf{b}$。如果 $A^T A$ 不可逆（奇异），则存在无穷多个解。

那么，$A^T A$ 何时可逆呢？这引出了另一个基本结论：$n \times n$ 矩阵 $A^T A$ 是可逆的，当且仅当 $m \times n$ 矩阵 $A$ 的**列是线性无关的** [@problem_id:2218027]。
证明的思路是，矩阵可逆等价于其零空间只包含零向量。我们可以证明 $A^T A$ 和 $A$ 有着完全相同的零空间，即 $\mathcal{N}(A^T A) = \mathcal{N}(A)$。因此，$A^T A$ 可逆 $\iff \mathcal{N}(A^T A) = \{\mathbf{0}\} \iff \mathcal{N}(A) = \{\mathbf{0}\}$。而 $\mathcal{N}(A) = \{\mathbf{0}\}$ 正是“$A$ 的列线性无关”的定义。

在实际数据拟合中，如果 $A$ 的列是线性相关的，通常意味着模型设计存在冗余，或者数据点的选择不当。例如，在用二次多项式 $y(x) = c_0 + c_1 x + c_2 x^2$ 拟合数据时，设计矩阵 $A$ 是一个范德蒙矩阵。如果测量点 $x_i$ 中有重复值，比如 $x_1 = x_3$，那么 $A$ 的第一行和第三行将完全相同，导致 $A$ 的列线性相关（此时 $A$ 为方阵且行列式为零），$A^T A$ 也将是奇异的，无法唯一确定系数 $c_0, c_1, c_2$ [@problem_id:2217984]。

### 数值特性与计算考量

尽管正规方程在理论上非常优雅，但在实际的数值计算中，它可能存在严重的问题，主要源于数值不稳定性。这种不稳定性与矩阵的**条件数**（Condition Number）密切相关。一个矩阵的条件数 $\kappa(M)$ 衡量了其解对输入（矩阵 $M$ 或右端向量 $\mathbf{v}$）中的微小扰动的敏感程度。一个巨大的条件数意味着矩阵是**病态的**（ill-conditioned），求解相关线性系统时，舍入误差会被严重放大。

对于正规方程，最关键的问题在于，从矩阵 $A$ 构建 $A^T A$ 的过程会使条件数平方：
$$ \kappa_2(A^T A) = (\kappa_2(A))^2 $$
这里 $\kappa_2$ 表示基于欧几里得范数的条件数。这意味着，如果原始矩阵 $A$ 本身就是轻度病态的（例如 $\kappa_2(A) \approx 10^4$），那么 $A^T A$ 将会是高度病态的（$\kappa_2(A^T A) \approx 10^8$）。用浮点数运算求解一个条件数如此之大的系统，其结果的精度可能会非常低。

当矩阵 $A$ 的列向量近似线性相关时，它往往是病态的。一个典型的例子是，当使用多项式拟合一个在很小区间内采集的数据时。例如，假设我们在时间点 $t_1=100.0, t_2=101.0, t_3=102.0$ 拟合线性模型 $y(t) = c_0 + c_1 t$。对应的设计矩阵 $A$ 的两列分别是 $\begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$ 和 $\begin{pmatrix} 100.0 \\ 101.0 \\ 102.0 \end{pmatrix}$。这两列几乎是共线的，导致 $\kappa_2(A)$ 很大。计算表明，在这种情况下，$\kappa_2(A^T A)$ 可高达 $1.561 \times 10^8$，预示着严重的数值问题 [@problem_id:2218032]。

另一个经典的病态矩阵是**希尔伯特矩阵**（Hilbert Matrix），其元素为 $H_{ij} = 1/(i+j-1)$。随着维度的增加，希尔伯特矩阵的条件数会爆炸式增长。如果一个最小二乘问题中的设计矩阵 $A$ 是希尔伯特矩阵，使用正规方程求解会得到与真实解相去甚远的结果 [@problem_id:3257364]。

为了规避这种数值不稳定性，现代数值计算软件通常采用更稳健的方法来求解最小二乘问题，例如基于 **QR 分解**的方法。QR 方法通过正交变换将 $A$ 分解为 $A=QR$，其中 $Q$ 是一个具有标准正交列的矩阵，$R$ 是一个上三角矩阵。然后，最小二乘问题转化为求解一个条件数更小的上三角系统 $R\hat{\mathbf{x}} = Q^T\mathbf{b}$。这种方法的优越性在于它直接对 $A$ 进行操作，避免了形成 $A^T A$ 的过程，从而避免了条件数的平方。其求解系统的条件数 $\kappa_2(R)$ 与原始矩阵的条件数 $\kappa_2(A)$ 相同，因此在面对病态问题时表现得更为可靠。

总之，正规方程为理解最小二乘问题提供了坚实的理论和几何基础，但在高精度计算中，它的数值局限性促使我们采用更为先进和稳定的算法。