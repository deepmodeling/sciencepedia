## 引言
在科学研究与工程实践中，我们常常需要从充满噪声的数据中提取有意义的模型。当数据点数量远超模型参数时，便构成了无法精确求解的超定[线性系统](@entry_id:147850)。那么，我们如何定义并找到一个“最佳”的近似解呢？这正是[线性最小二乘法](@entry_id:165427)要解决的核心问题，也是数据分析领域最基本、最强大的工具之一。本文旨在深入剖析求解线性[最小二乘问题](@entry_id:164198)的经典方法——正规方程，带领读者踏上一段从理论到实践的旅程。

在第一章“原则与机理”中，我们将从代数和几何两个角度推导正规方程，并探讨其[解的唯一性](@entry_id:143619)和[数值稳定性](@entry_id:146550)问题。接着，在第二章“应用与跨学科联系”中，我们将展示该方法如何被广泛应用于物理学、经济学、信号处理等多个领域，揭示其强大的模型构建能力。最后，在第三章“动手实践”中，你将有机会通过具体问题，亲手应用所学知识，巩固对核心概念的理解。

## 原则与机理

在本章中，我们将深入探讨线性[最小二乘问题](@entry_id:164198)的核心——[正规方程](@entry_id:142238) (The Normal Equations)。我们将从其代数推导和几何意义入手，阐明其求解“最优”近似解的内在机理。接着，我们将分析保证唯一解存在的条件，并揭示这些条件在实际建模中是如何体现的。最后，我们将讨论直接求解[正规方程](@entry_id:142238)可能面临的[数值稳定性](@entry_id:146550)问题，并介绍一种更为稳健的替代方法。

### [正规方程](@entry_id:142238)的推导

在科学与工程领域，我们常常需要用一个线性数学模型来拟合一组实验数据。假设我们有 $m$ 个数据点 $(t_k, y_k)$，并且我们的模型预测 $y$ 的值是 $n$ 个已知[基函数](@entry_id:170178) $f_j(t)$ 的[线性组合](@entry_id:154743)，其系数 $x_j$ 是未知的：

$y(t) \approx x_1 f_1(t) + x_2 f_2(t) + \dots + x_n f_n(t)$

对于每一个数据点，我们都可以写出一个方程：

$y_k \approx x_1 f_1(t_k) + x_2 f_2(t_k) + \dots + x_n f_n(t_k)$

当数据点的数量 $m$ 大于未知系数的数量 $n$ 时，这通常会构成一个**超定[线性系统](@entry_id:147850) (overdetermined linear system)**。由于测量误差和模型不精确性的存在，这个系统一般没有精确解。我们无法找到一个系数向量 $\mathbf{x} = \begin{pmatrix} x_1  \dots  x_n \end{pmatrix}^T$ 使得模型完美穿过所有数据点。

我们可以将这个系统写成矩阵形式 $A\mathbf{x} \approx \mathbf{b}$，其中：
- $A$ 是一个 $m \times n$ 的矩阵，称为**[设计矩阵](@entry_id:165826) (design matrix)**，其元素 $A_{kj} = f_j(t_k)$。每一列对应一个[基函数](@entry_id:170178)在所有测量点上的取值，每一行对应一个测量点的所有[基函数](@entry_id:170178)取值。
- $\mathbf{x}$ 是一个 $n \times 1$ 的列向量，包含待求的未知系数。
- $\mathbf{b}$ 是一个 $m \times 1$ 的列向量，包含所有测量的观测值 $y_k$。

我们的目标是找到一个“最佳”的系数向量 $\hat{\mathbf{x}}$，使得由它产生的预测值 $A\hat{\mathbf{x}}$ 与实际观测值 $\mathbf{b}$ 之间的“误差”最小。[最小二乘法](@entry_id:137100)的核心思想是定义这个误差为**[残差向量](@entry_id:165091) (residual vector)** $\mathbf{r} = \mathbf{b} - A\mathbf{x}$ 的欧几里得范数（即其长度）的平方。我们要最小化的[目标函数](@entry_id:267263)是**[残差平方和](@entry_id:174395) (sum of squared residuals)** $S(\mathbf{x})$：

$S(\mathbf{x}) = \|\mathbf{r}\|_2^2 = \|\mathbf{b} - A\mathbf{x}\|_2^2 = (\mathbf{b} - A\mathbf{x})^T(\mathbf{b} - A\mathbf{x})$

为了找到使 $S(\mathbf{x})$ 最小的 $\mathbf{x}$，我们可以运用多元微积分的方法。我们将 $S(\mathbf{x})$ 展开：

$S(\mathbf{x}) = \mathbf{b}^T\mathbf{b} - \mathbf{b}^T(A\mathbf{x}) - (A\mathbf{x})^T\mathbf{b} + (A\mathbf{x})^T(A\mathbf{x})$
$S(\mathbf{x}) = \mathbf{b}^T\mathbf{b} - 2\mathbf{x}^T A^T \mathbf{b} + \mathbf{x}^T A^T A \mathbf{x}$

这是一个关于 $\mathbf{x}$ 的二次函数。其[最小值点](@entry_id:634980)出现在梯度 $\nabla_{\mathbf{x}}S(\mathbf{x})$ 为[零向量](@entry_id:156189)的位置。利用矩阵[求导法则](@entry_id:145443)，我们得到：

$\nabla_{\mathbf{x}}S(\mathbf{x}) = -2 A^T \mathbf{b} + 2 A^T A \mathbf{x}$

令梯度为零：

$2 A^T A \mathbf{x} - 2 A^T \mathbf{b} = \mathbf{0}$

简化后，我们便得到了著名的**正规方程**：

$A^T A \mathbf{x} = A^T \mathbf{b}$

任何[最小二乘解](@entry_id:152054) $\hat{\mathbf{x}}$ 都必须满足这个方程。这是一个包含 $n$ 个方程和 $n$ 个未知数的方阵[线性系统](@entry_id:147850)。矩阵 $A^T A$ 是一个 $n \times n$ 的对称矩阵，而 $A^T \mathbf{b}$ 是一个 $n \times 1$ 的向量。

让我们通过一个具体的例子来理解 $A^T A$ 和 $A^T \mathbf{b}$ 的结构。考虑最常见的**简单[线性回归](@entry_id:142318)**模型 $y \approx \beta_0 + \beta_1 x$ 。对于 $n$ 个数据点 $(x_i, y_i)$，[设计矩阵](@entry_id:165826) $A$ 和系数向量 $\boldsymbol{\beta}$ 分别是：

$A = \begin{pmatrix} 1  x_1 \\ 1  x_2 \\ \vdots  \vdots \\ 1  x_n \end{pmatrix}, \quad \boldsymbol{\beta} = \begin{pmatrix} \beta_0 \\ \beta_1 \end{pmatrix}$

矩阵 $A^T A$ 的计算如下：

$A^T A = \begin{pmatrix} 1  1  \dots  1 \\ x_1  x_2  \dots  x_n \end{pmatrix} \begin{pmatrix} 1  x_1 \\ 1  x_2 \\ \vdots  \vdots \\ 1  x_n \end{pmatrix} = \begin{pmatrix} n  \sum_{i=1}^n x_i \\ \sum_{i=1}^n x_i  \sum_{i=1}^n x_i^2 \end{pmatrix}$

向量 $A^T \mathbf{y}$ 的计算如下：

$A^T \mathbf{y} = \begin{pmatrix} 1  1  \dots  1 \\ x_1  x_2  \dots  x_n \end{pmatrix} \begin{pmatrix} y_1 \\ y_2 \\ \vdots \\ y_n \end{pmatrix} = \begin{pmatrix} \sum_{i=1}^n y_i \\ \sum_{i=1}^n x_i y_i \end{pmatrix}$

因此，简单[线性回归](@entry_id:142318)的正规方程具体形式为：
$\begin{pmatrix} n  \sum x_i \\ \sum x_i  \sum x_i^2 \end{pmatrix} \begin{pmatrix} \beta_0 \\ \beta_1 \end{pmatrix} = \begin{pmatrix} \sum y_i \\ \sum x_i y_i \end{pmatrix}$

这个结果表明，正规方程的系数完全由数据的各种汇总统计量（如样本量、和、平方和、乘积和）决定。

更一般地，矩阵 $A^T A$ 的第 $(i, j)$ 个元素是矩阵 $A$ 的第 $i$ 列和第 $j$ 列的[点积](@entry_id:149019)。同样，$A^T \mathbf{b}$ 的第 $i$ 个元素是 $A$ 的第 $i$ 列和向量 $\mathbf{b}$ 的[点积](@entry_id:149019)。例如，对于一个更复杂的物理模型 $y(t) = c_1 \sin(\omega t) + c_2 \cos(\omega t) + c_3 t$ ，[设计矩阵](@entry_id:165826) $A$ 的三列分别是对应于所有测量时间 $t_k$ 的 $\sin(\omega t_k)$、$\cos(\omega t_k)$ 和 $t_k$ 的向量。正规方程矩阵 $M = A^T A$ 的第一行第三列元素 $M_{13}$ 就是 $A$ 的第一列（$\sin(\omega t)$ [基函数](@entry_id:170178)）与第三列（$t$ [基函数](@entry_id:170178)）的[点积](@entry_id:149019)，即 $\sum_{k=1}^{m} t_k \sin(\omega t_k)$。

### 几何诠释

[正规方程](@entry_id:142238)不仅可以通过微积分推导，它还有一个非常直观和深刻的几何意义。让我们回到问题 $A\mathbf{x} \approx \mathbf{b}$。向量 $A\mathbf{x}$ 是矩阵 $A$ 的列向量的[线性组合](@entry_id:154743)，其系数由向量 $\mathbf{x}$ 给出。因此，当 $\mathbf{x}$ 取遍所有可能的 $n$ 维向量时，$A\mathbf{x}$ 的所有可能结果构成了 $A$ 的**列空间 (column space)**，记为 $\text{Col}(A)$。

从几何上看，[最小二乘问题](@entry_id:164198)等价于：在 $A$ 的[列空间](@entry_id:156444) $\text{Col}(A)$ 中，寻找一个向量 $\mathbf{p}$，使其与给定的观测向量 $\mathbf{b}$ 的距离最近。这个向量 $\mathbf{p}$ 就是我们对 $\mathbf{b}$ 的最佳逼近，并且它可以表示为 $A\hat{\mathbf{x}}$ 的形式，其中 $\hat{\mathbf{x}}$ 就是我们要求的[最小二乘解](@entry_id:152054)。

在[欧几里得空间](@entry_id:138052)中，一个点到一个[子空间](@entry_id:150286)的最短距离是通过作垂线得到的。这意味着，从 $\mathbf{b}$ 指向其在[子空间](@entry_id:150286) $\text{Col}(A)$ 上的最近点 $\mathbf{p}$ 的向量，必须与该[子空间](@entry_id:150286)**正交 (orthogonal)**。这个向量正是我们的残差向量 $\mathbf{r} = \mathbf{b} - \mathbf{p} = \mathbf{b} - A\hat{\mathbf{x}}$。

“[残差向量](@entry_id:165091) $\mathbf{r}$ 与[子空间](@entry_id:150286) $\text{Col}(A)$ 正交”意味着 $\mathbf{r}$ 与 $\text{Col}(A)$ 中的**任何**向量都正交。由于 $\text{Col}(A)$ 是由 $A$ 的列向量 $\mathbf{a}_1, \dots, \mathbf{a}_n$ 张成的，这个条件等价于 $\mathbf{r}$ 与每一个列向量都正交：

$\mathbf{a}_1^T \mathbf{r} = 0, \quad \mathbf{a}_2^T \mathbf{r} = 0, \quad \dots, \quad \mathbf{a}_n^T \mathbf{r} = 0$

将这 $n$ 个标量[方程组](@entry_id:193238)合成一个矩阵方程，就是：

$\begin{pmatrix} \rule[2pt]{1.5em}{0.4pt}  \mathbf{a}_1^T  \rule[2pt]{1.5em}{0.4pt} \\ \rule[2pt]{1.5em}{0.4pt}  \mathbf{a}_2^T  \rule[2pt]{1.5em}{0.4pt} \\  \vdots  \\ \rule[2pt]{1.5em}{0.4pt}  \mathbf{a}_n^T  \rule[2pt]{1.5em}{0.4pt} \end{pmatrix} \mathbf{r} = \mathbf{0} \quad \implies \quad A^T \mathbf{r} = \mathbf{0}$

将 $\mathbf{r} = \mathbf{b} - A\hat{\mathbf{x}}$ 代入，我们得到 $A^T (\mathbf{b} - A\hat{\mathbf{x}}) = \mathbf{0}$，整理后即为 $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$。这正是正规方程 。因此，正规方程的几何本质是**[残差向量](@entry_id:165091)与[列空间](@entry_id:156444)的[正交性条件](@entry_id:168905)**。这个正交性保证了 $A\hat{\mathbf{x}}$ 是 $\mathbf{b}$ 在 $\text{Col}(A)$ 上的**正交投影 (orthogonal projection)**。

我们可以通过一个具体的数值例子来验证这个正交性 。考虑系统 $A = \begin{pmatrix} 1  0 \\ 1  1 \\ 1  2 \end{pmatrix}$, $\mathbf{b} = \begin{pmatrix} 1 \\ 2 \\ 4 \end{pmatrix}$。
通过求解[正规方程](@entry_id:142238)可以得到[最小二乘解](@entry_id:152054) $\hat{\mathbf{x}} = \begin{pmatrix} 5/6 \\ 3/2 \end{pmatrix}$。
由此计算出投影向量 $\mathbf{p} = A\hat{\mathbf{x}} = \begin{pmatrix} 5/6 \\ 7/3 \\ 23/6 \end{pmatrix}$。
残差向量为 $\mathbf{r} = \mathbf{b} - \mathbf{p} = \begin{pmatrix} 1/6 \\ -1/3 \\ 1/6 \end{pmatrix}$。
现在我们来检验其与 $A$ 的列向量 $\mathbf{a}_1 = \begin{pmatrix} 1 \\ 1 \\ 1 \end{pmatrix}$ 和 $\mathbf{a}_2 = \begin{pmatrix} 0 \\ 1 \\ 2 \end{pmatrix}$ 的正交性：
$\mathbf{r} \cdot \mathbf{a}_1 = (1/6)(1) + (-1/3)(1) + (1/6)(1) = 0$
$\mathbf{r} \cdot \mathbf{a}_2 = (1/6)(0) + (-1/3)(1) + (1/6)(2) = 0$
结果确实为零，证实了[残差向量](@entry_id:165091)与 $A$ 的所有列向量正交。

这个[正交性条件](@entry_id:168905)是如此根本，以至于它可以用来识别一个给定的向量是否可能是一个[最小二乘问题](@entry_id:164198)的[残差向量](@entry_id:165091) 。一个向量 $\mathbf{r}$ 若要成为由矩阵 $A$ 定义的某个最小二乘问题的残差，它必须满足 $A^T \mathbf{r} = \mathbf{0}$，即 $\mathbf{r}$ 必须属于 $A^T$ 的**[零空间](@entry_id:171336) (null space)**，也就是 $A$ 的[列空间](@entry_id:156444)的[正交补](@entry_id:149922)空间 $\text{Col}(A)^\perp$。

### 唯一解的条件

正规方程 $A^T A \hat{\mathbf{x}} = A^T \mathbf{b}$ 是一个 $n \times n$ 的线性方程组。它的解 $\hat{\mathbf{x}}$ 是否存在且唯一，取决于方阵 $A^T A$ 的性质。一个方阵[线性系统](@entry_id:147850)有唯一解的充分必要条件是该方阵是**可逆的 (invertible)**。

那么，在什么条件下 $A^T A$ 是可逆的呢？我们可以证明一个至关重要的结论：**矩阵 $A^T A$ 是可逆的，当且仅当矩阵 $A$ 的列向量是线性无关的 (linearly independent)。**

- **证明**:
    1.  首先，我们证明如果 $A$ 的列线性无关，则 $A^T A$ 可逆。要证明 $A^T A$ 可逆，只需证明方程 $A^T A \mathbf{x} = \mathbf{0}$ 只有唯一解 $\mathbf{x} = \mathbf{0}$。
        假设 $A^T A \mathbf{x} = \mathbf{0}$。用 $\mathbf{x}^T$ 左乘该方程，得到 $\mathbf{x}^T A^T A \mathbf{x} = 0$。
        这可以写成 $(A\mathbf{x})^T(A\mathbf{x}) = 0$，即 $\|A\mathbf{x}\|_2^2 = 0$。
        一个[向量的范数](@entry_id:154882)为零，当且仅当该向量为零向量，因此 $A\mathbf{x} = \mathbf{0}$。
        根据假设，$A$ 的列是[线性无关](@entry_id:148207)的，这意味着 $A\mathbf{x} = \mathbf{0}$ 的唯一解就是 $\mathbf{x} = \mathbf{0}$。
        因此，$A^T A \mathbf{x} = \mathbf{0}$ 仅有零解，故 $A^T A$ 可逆。

    2.  反之，如果 $A$ 的列是[线性相关](@entry_id:185830)的，那么存在一个非[零向量](@entry_id:156189) $\mathbf{c}$ 使得 $A\mathbf{c} = \mathbf{0}$。
        那么，$A^T A \mathbf{c} = A^T (\mathbf{0}) = \mathbf{0}$。
        这意味着方程 $A^T A \mathbf{x} = \mathbf{0}$ 存在非零解 $\mathbf{c}$，所以 $A^T A$ 的[零空间](@entry_id:171336)非平凡，因此 $A^T A$ 是**奇异的 (singular)**，即不可逆。

在实际应用中，$A$ 的列[线性相关](@entry_id:185830)通常源于实验设计不当或[模型选择](@entry_id:155601)不佳。

- **实验设计不当**：考虑用二次多项式 $y(x) = c_0 + c_1 x + c_2 x^2$ 拟合数据 。如果我们在三个不同的 $x$ 坐标 $(x_1, x_2, x_3)$ 处进行测量，[设计矩阵](@entry_id:165826) $A$ 是一个 $3 \times 3$ 的[范德蒙矩阵](@entry_id:147747)。只要 $x_1, x_2, x_3$ 互不相同，该矩阵的列就是线性无关的，其[行列式](@entry_id:142978)非零，从而 $A$ 和 $A^T A$ 都是可逆的，系数 $\mathbf{c}$ 有唯一解。但是，如果我们选择的测量点有重复，例如 $x_3 = x_1$，那么 $A$ 的第一行和第三行将完全相同，导致其列线性相关，$\det(A) = 0$，$A^T A$ 奇异，系数 $\mathbf{c}$ 无法被唯一确定。

- **模型[基函数](@entry_id:170178)选择不佳**：如果模型中的[基函数](@entry_id:170178)本身就是线性相关的，那么无论在哪些点进行测量，$A$ 的列都将是线性相关的。例如，一个模型使用两个[基函数](@entry_id:170178) $f_1(t) = t$ 和 $f_2(t) = -2t$ 。显然，$f_2(t) = -2f_1(t)$。因此，[设计矩阵](@entry_id:165826) $A$ 的第二列将永远是第一列的 $-2$ 倍。这导致 $\text{rank}(A) = 1  2$，$A^T A$ 是一个奇异的 $2 \times 2$ 矩阵。在这种情况下，[正规方程](@entry_id:142238)系统虽然仍然是相容的（解总是存在），但它有无穷多个解，无法得到唯一的系数向量。

- **共线性问题**：在某些实验中，两个或多个自变量可能高度相关，甚至是完全相关的。例如，一个实验中湿度 $H$ 总是被控制为温度 $T$ 的某个倍数，$H_i = \alpha T_i$ 。如果模型是 $V = c_1 T + c_2 P + c_3 H$，那么[设计矩阵](@entry_id:165826) $A$ 的第三列将是第一列的 $\alpha$ 倍。这些列是[线性相关](@entry_id:185830)的，导致 $A^T A$ 矩阵是奇异的，其[行列式](@entry_id:142978)为零。这意味着我们无法同时唯一地确定 $c_1$ 和 $c_3$。

综上所述，[最小二乘问题](@entry_id:164198)有唯一解的充要条件是[设计矩阵](@entry_id:165826) $A$ 的列线性无关。

### 数值稳定性与更稳健的方法

理论上，只要 $A$ 的列[线性无关](@entry_id:148207)，$A^T A$ 就是可逆的，我们可以通过求解正规方程得到唯一的[最小二乘解](@entry_id:152054)。然而，在实际的数值计算中，我们还必须关心**数值稳定性 (numerical stability)**。

当 $A$ 的列虽然[线性无关](@entry_id:148207)但“几乎”[线性相关](@entry_id:185830)时，问题就出现了。这种情况称为**[共线性](@entry_id:270224) (collinearity)** 或**病态 (ill-conditioning)**。例如，对一个[线性模型](@entry_id:178302) $y(t) = c_0 + c_1 t$ 进行拟合，如果测量时间点非常接近，如 $t_1=100.0, t_2=101.0, t_3=102.0$ ，那么[设计矩阵](@entry_id:165826) $A = \begin{pmatrix} 1  100.0 \\ 1  101.0 \\ 1  102.0 \end{pmatrix}$ 的两列向量虽然线性无关，但它们的方向非常接近。

在这种情况下，矩阵 $A^T A$ 会变得**病态的 (ill-conditioned)**，意味着它对输入的微小扰动非常敏感。[病态矩阵](@entry_id:147408)的特征是其**条件数 (condition number)** 非常大。对于对称正定矩阵 $M=A^T A$，其谱[条件数](@entry_id:145150)定义为其最大[特征值](@entry_id:154894)与[最小特征值](@entry_id:177333)之比：$\kappa_2(M) = \frac{\lambda_{\max}}{\lambda_{\min}}$。

一个关键的事实是，$\kappa_2(A^T A) = (\kappa_2(A))^2$。这意味着，通过构建正规方程，我们将原问题矩阵 $A$ 的[条件数](@entry_id:145150)平方了。如果 $A$ 本身就是中等程度病态的（例如 $\kappa_2(A) \approx 10^4$），那么 $A^T A$ 将会是严重病态的（$\kappa_2(A^T A) \approx 10^8$）。在有限精度的计算机上求解由这样一个[病态矩阵](@entry_id:147408)定义的线性系统，会导致解的精度严重损失。在前面提到的时间点例子  中，$A^T A$ 的条件数高达约 $1.561 \times 10^8$，这预示着数值上的巨大困难。

为了避免这种[数值不稳定性](@entry_id:137058)，推荐使用不直接形成 $A^T A$ 的方法。其中最可靠和最广泛使用的方法是基于**[奇异值分解](@entry_id:138057) (Singular Value Decomposition, SVD)**。任何 $m \times n$ 矩阵 $A$ 都可以分解为 $A = U\Sigma V^T$，其中：
- $U$ 是一个 $m \times m$ 的正交矩阵，其列为 $A$ 的**[左奇异向量](@entry_id:751233)**。
- $V$ 是一个 $n \times n$ 的正交矩阵，其列为 $A$ 的**[右奇异向量](@entry_id:754365)**。
- $\Sigma$ 是一个 $m \times n$ 的对角矩阵，其对角线上的元素 $\sigma_1 \ge \sigma_2 \ge \dots \ge 0$ 是 $A$ 的**奇异值**。

利用 SVD，[最小二乘解](@entry_id:152054) $\hat{\mathbf{x}}$ 可以表示为：

$\hat{\mathbf{x}} = A^+ \mathbf{b}$

其中 $A^+ = V\Sigma^+ U^T$ 是 $A$ 的**[穆尔-彭罗斯伪逆](@entry_id:147255) (Moore-Penrose pseudoinverse)**。$\Sigma^+$ 是通过将 $\Sigma$ 中所有非零的[奇异值](@entry_id:152907)取倒数然后[转置](@entry_id:142115)得到的。

使用 SVD 求解最小二乘问题有几个关键优势：
1.  **数值稳定性**：它直接在 $A$ 上操作，避免了计算 $A^T A$ 从而避免了条件数的平方，因此数值上更为稳健。
2.  **诊断能力**：奇异值的大小直接反映了 $A$ 的列的近线性相关性。非常小的奇异值（相对于最大的[奇异值](@entry_id:152907)）是病态的明确信号。
3.  **通用性**：即使当 $A$ 的列是[线性相关](@entry_id:185830)的（即 $A^T A$ 不可逆），SVD 方法仍然能给出一个解。在这种情况下，存在无穷多个[最小二乘解](@entry_id:152054)，而 SVD 给出的解 $\hat{\mathbf{x}} = A^+ \mathbf{b}$ 是其中[欧几里得范数](@entry_id:172687) $\|\mathbf{x}\|_2$ 最小的那个，这通常是物理上最合理的解。

例如，在一个具有一个大奇异值（如 $10$）和一个非常小的[奇异值](@entry_id:152907)（如 $10^{-4}$）的系统中 ，$\kappa_2(A) = 10^5$，而 $\kappa_2(A^T A) = 10^{10}$。直接求解正规方程会非常不稳定，而使用 SVD 和[伪逆](@entry_id:140762) $\hat{\mathbf{x}} = V\Sigma^+ U^T \mathbf{b}$ 则能稳健地计算出[最小范数解](@entry_id:751996)。

总之，虽然正规方程为我们理解最小二乘问题提供了基础的代数和几何框架，但在进行严肃的数值计算时，尤其是在可能遇到[病态问题](@entry_id:137067)的情况下，基于 SVD 等[正交分解](@entry_id:148020)的方法是更可取、更稳健的选择。