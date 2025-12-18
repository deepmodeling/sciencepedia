## 引言
在科学研究和工程实践中，我们常常需要用数学模型来描述和预测复杂的现象。当这些模型与待求参数之间呈现非线性关系时，经典的线性方法便[无能](@entry_id:201612)为力。非[线性最小二乘法](@entry_id:165427)（NLS）应运而生，它提供了一套强大的框架，通[过拟合](@entry_id:139093)观测数据来精确估计[非线性模型](@entry_id:276864)中的未知参数，已成为数据分析和[参数估计](@entry_id:139349)领域不可或缺的基石。然而，从线性到[非线性](@entry_id:637147)的转变带来了本质的挑战：解不再能一步求得，而必须依赖于复杂的迭代优化过程。本文旨在系统性地揭示非[线性最小二乘法](@entry_id:165427)的内在逻辑和实践应用。在第一章“原理与机制”中，我们将深入探讨问题的数学构建，剖析核心算法——[高斯-牛顿法](@entry_id:173233)与列文伯格-马夸特法——的工作原理、优势与局限性。随后，在第二章“应用与[交叉](@entry_id:147634)学科联系”中，我们将跨越学科界限，展示NLS如何在物理、生物、工程乃至机器学习等前沿领域中解决真实世界的问题。最后，通过第三章“动手实践”，你将有机会亲手实现并应用这些算法，将理论知识转化为解决问题的实用技能。

## 原理与机制

在[数值优化](@entry_id:138060)领域，非[线性[最小二乘](@entry_id:165427)法](@entry_id:137100)（Nonlinear Least Squares, NLS）是[数据拟合](@entry_id:149007)和[参数估计](@entry_id:139349)中一个极其重要和广泛应用的分支。它处理的是将一个参数化的[非线性模型](@entry_id:276864)函数与一组观测数据进行拟合的问题。本章将深入探讨非[线性最小二乘法](@entry_id:165427)的基本原理、核心算法机制及其在实践中遇到的关键问题。我们将从问题的定义出发，逐步剖析[高斯-牛顿法](@entry_id:173233)（Gauss-Newton method）及其稳健的改进版——列文伯格-马夸特法（Levenberg-Marquardt algorithm）。

### [非线性](@entry_id:637147)[最小二乘问题](@entry_id:164198)的构建

[非线性](@entry_id:637147)最小二乘问题的核心目标是调整模型中的参数，使得模型预测值与实际观测数据之间的差异（即**残差**）的平方和达到最小。

假设我们有一组包含 $N$ 个数据点的实验数据 $(t_i, y_i)$，其中 $i = 1, \dots, N$。我们希望用一个[非线性模型](@entry_id:276864) $y = \phi(t; \boldsymbol{\beta})$ 来描述这些数据，其中 $\boldsymbol{\beta} = (\beta_1, \beta_2, \dots, \beta_p)$ 是一个包含 $p$ 个待定参数的向量。对于每个数据点 $i$，模型预测值与观测值之间的残差定义为：

$r_i(\boldsymbol{\beta}) = y_i - \phi(t_i; \boldsymbol{\beta})$

非[线性最小二乘法](@entry_id:165427)旨在找到一组最优参数 $\boldsymbol{\beta}^*$，以最小化所有残差的平方和。这个[目标函数](@entry_id:267263)通常表示为 $S(\boldsymbol{\beta})$：

$S(\boldsymbol{\beta}) = \sum_{i=1}^{N} [r_i(\boldsymbol{\beta})]^2 = \sum_{i=1}^{N} (y_i - \phi(t_i; \boldsymbol{\beta}))^2$

例如，在[材料科学](@entry_id:152226)中，研究新合金的冷却过程时，样品温度 $T$ 随时间 $t$ 的变化可以用[牛顿冷却定律](@entry_id:142531)的变体来建模：$T_{\text{model}}(t; \beta_1, \beta_2) = A + \beta_1 \exp(-\beta_2 t)$。这里，$A$ 是已知的环境温度，而 $\beta_1$（初始温差）和 $\beta_2$（冷却速率常数）是需要从实验数据 $(t_i, T_i)$ 中估计的参数。在这种情况下，最小化的目标函数就是：

$S(\beta_1, \beta_2) = \sum_{i=1}^{N} (T_i - (A + \beta_1 \exp(-\beta_2 t_i)))^2$ 

这个问题被称为“[非线性](@entry_id:637147)”的，是因为模型函数 $\phi(t; \boldsymbol{\beta})$ 相对于至少一个参数 $\beta_j$ 是[非线性](@entry_id:637147)的。

### 关键区别：线性与[非线性](@entry_id:637147)最小二乘

理解线性和[非线性](@entry_id:637147)最小二乘之间的区别至关重要，因为它决定了求解问题的根本方法。一个最小二乘问题是**线性的**，当且仅当模型函数 $\phi(x; \mathbf{c})$ 是其参数 $\mathbf{c} = (c_1, \dots, c_p)$ 的线性组合。这意味着模型可以写成 $\phi(x; \mathbf{c}) = \sum_{j=1}^p c_j g_j(x)$ 的形式，其中[基函数](@entry_id:170178) $g_j(x)$ 不依赖于任何参数 $c_k$。

让我们通过一个例子来阐明这一点 。考虑两个模型：
1.  **模型一**: $y = c_1 x + c_2 x^2$
2.  **模型二**: $y = c_1 (x - c_2)^2$

**模型一**是一个线性最小二乘问题。尽[管模型](@entry_id:140303)中包含[自变量](@entry_id:267118) $x$ 的[非线性](@entry_id:637147)项 $x^2$，但模型本身是参数 $c_1$ 和 $c_2$ 的线性组合。我们可以将其写作 $\phi(x; c_1, c_2) = c_1 g_1(x) + c_2 g_2(x)$，其中[基函数](@entry_id:170178)为 $g_1(x)=x$ 和 $g_2(x)=x^2$。对于这类问题，[目标函数](@entry_id:267263) $S(c_1, c_2)$ 是一个关于参数的二次函数。其最小值可以通过求解一个称为**[正规方程](@entry_id:142238)**（normal equations）的[线性方程组](@entry_id:148943)一步得到，并且在[基函数](@entry_id:170178)线性无关的条件下，解是唯一的[全局最优解](@entry_id:175747)。

**模型二**则是一个[非线性](@entry_id:637147)最小二乘问题。如果我们展开模型函数，会得到 $y = c_1(x^2 - 2c_2x + c_2^2) = c_1x^2 - 2c_1c_2x + c_1c_2^2$。在这个表达式中，我们看到了参数的乘积项（$c_1c_2$）和参数的平方项（$c_2^2$），这表明模型不是参数 $c_1$ 和 $c_2$ 的线性函数。因此，目标函数 $S(c_1, c_2)$ 是一个复杂的四次多项式，而非二次型。这类问题的求解不能一步完成，必须依赖于迭代优化算法，如[高斯-牛顿法](@entry_id:173233)或列文伯格-马夸特法。

值得注意的是，试图通过引入新参数（例如 $d_1 = c_1$, $d_2 = -2c_1c_2$, $d_3 = c_1c_2^2$）将模型二改写为[线性形式](@entry_id:276136) $y = d_1x^2 + d_2x + d_3$ 的做法是具有误导性的。虽然可以对新参数 $(d_1, d_2, d_3)$ 进行线性[最小二乘拟合](@entry_id:751226)，但这忽略了这些新参数之间存在的非[线性约束](@entry_id:636966)关系，即 $d_2^2 - 4d_1d_3 = 0$。无约束的线性拟合得到的解 $(d_1^*, d_2^*, d_3^*)$ 通常不满足这个约束，因此无法还原回原始的 $(c_1, c_2)$ 参数。这说明模型二的[非线性](@entry_id:637147)是其內禀属性 。

### [高斯-牛顿法](@entry_id:173233)：一种基于线性化的迭代策略

由于[非线性](@entry_id:637147)[最小二乘问题](@entry_id:164198)的目标函数通常很复杂，我们采用迭代方法，从一个初始猜测 $\boldsymbol{\beta}_0$ 开始，逐步逼近最优解。[高斯-牛顿法](@entry_id:173233)是其中最基本和最直观的一种。

其核心思想是在每次迭代中，用一个线性函数来近似[非线性](@entry_id:637147)的残差函数。在当前迭代点 $\boldsymbol{\beta}_k$ 附近，对残差向量 $\mathbf{r}(\boldsymbol{\beta})$ 进行一阶泰勒展开：
$\mathbf{r}(\boldsymbol{\beta}_k + \mathbf{p}) \approx \mathbf{r}(\boldsymbol{\beta}_k) + \mathbf{J}(\boldsymbol{\beta}_k) \mathbf{p}$

这里，$\mathbf{p}$ 是我们希望找到的更新步长，而 $\mathbf{J}(\boldsymbol{\beta}_k)$ 是残差向量 $\mathbf{r}$ 在 $\boldsymbol{\beta}_k$ 处的**雅可比矩阵**（Jacobian matrix）。[雅可比矩阵](@entry_id:264467)的第 $(i, j)$ 个元素定义为 $J_{ij} = \frac{\partial r_i}{\partial \beta_j}$。

将这个线性近似代入[目标函数](@entry_id:267263)，原问题就转化为在每一步求解一个关于步长 $\mathbf{p}$ 的线性[最小二乘问题](@entry_id:164198)：
$\min_{\mathbf{p}} S(\mathbf{p}) = \sum_{i=1}^N \left( r_i(\boldsymbol{\beta}_k) + (\mathbf{J}(\boldsymbol{\beta}_k)\mathbf{p})_i \right)^2 = \|\mathbf{r}(\boldsymbol{\beta}_k) + \mathbf{J}(\boldsymbol{\beta}_k)\mathbf{p}\|_2^2$

这个问题可以通过求解其[正规方程](@entry_id:142238)来解决：
$(\mathbf{J}_k^T \mathbf{J}_k) \mathbf{p} = -\mathbf{J}_k^T \mathbf{r}_k$

其中 $\mathbf{J}_k = \mathbf{J}(\boldsymbol{\beta}_k)$ 且 $\mathbf{r}_k = \mathbf{r}(\boldsymbol{\beta}_k)$。解出步长 $\mathbf{p}$ 后，更新参数：$\boldsymbol{\beta}_{k+1} = \boldsymbol{\beta}_k + \mathbf{p}$。重复此过程直至收敛。

#### 与[牛顿法](@entry_id:140116)的关系

[高斯-牛顿法](@entry_id:173233)可以看作是牛顿法的一种近似。[牛顿法](@entry_id:140116)通过求解 $\mathbf{H}_k \mathbf{p} = -\mathbf{g}_k$ 来确定步长，其中 $\mathbf{g}_k$ 是目标函数 $S(\boldsymbol{\beta})$ 的梯度，$\mathbf{H}_k$ 是其**[海森矩阵](@entry_id:139140)**（Hessian matrix）。

对于 NLS 目标函数 $S(\boldsymbol{\beta}) = \frac{1}{2} \mathbf{r}(\boldsymbol{\beta})^T \mathbf{r}(\boldsymbol{\beta})$，其梯度和[海森矩阵](@entry_id:139140)可以精确计算得出 ：
$\mathbf{g}(\boldsymbol{\beta}) = \nabla S(\boldsymbol{\beta}) = \mathbf{J}(\boldsymbol{\beta})^T \mathbf{r}(\boldsymbol{\beta})$
$\mathbf{H}(\boldsymbol{\beta}) = \nabla^2 S(\boldsymbol{\beta}) = \mathbf{J}(\boldsymbol{\beta})^T \mathbf{J}(\boldsymbol{\beta}) + \sum_{i=1}^N r_i(\boldsymbol{\beta}) \nabla^2 r_i(\boldsymbol{\beta})$

对比之下，[高斯-牛顿法](@entry_id:173233)使用的矩阵 $\mathbf{J}^T \mathbf{J}$ 正是海森矩阵的第一部分。它忽略了包含残差[二阶导数](@entry_id:144508)（即曲率）的第二部分 $\sum r_i \nabla^2 r_i$。

这个近似的合理性基于两个假设：
1.  **小残差假设**：如果模型能很好地拟[合数](@entry_id:263553)据，那么在解附近，残差 $r_i$ 会非常小，使得第二项可以忽略不计。
2.  **低曲率假设**：如果模型相对于参数“接近线性”，那么残差的[二阶导数](@entry_id:144508) $\nabla^2 r_i$ 本身就很小。对于一个纯粹的[线性模型](@entry_id:178302)，$\nabla^2 r_i = \mathbf{0}$，此时[高斯-牛顿法](@entry_id:173233)的[海森近似](@entry_id:171462)是精确的。

当这些假设成立时（例如，对于一个[线性模型](@entry_id:178302)，或者一个接近解且残差很小的[非线性模型](@entry_id:276864)），[高斯-牛顿法](@entry_id:173233)的表现接近[牛顿法](@entry_id:140116)。然而，当远离解、残差很大或模型曲率很高时，被忽略的第二项可能变得非常重要，导致[高斯-牛顿法](@entry_id:173233)的步长方向和大小不佳 。

### [高斯-牛顿法](@entry_id:173233)的性能与缺陷

[高斯-牛顿法](@entry_id:173233)的性能和稳定性高度依赖于问题的结构。

#### [收敛速度](@entry_id:636873)

该方法的收敛速度与问题的残差大小密切相关 。
-   对于**零残差问题**（即存在一个参数 $\boldsymbol{\beta}^*$ 使得 $\mathbf{r}(\boldsymbol{\beta}^*) = \mathbf{0}$），[高斯-牛顿法](@entry_id:173233)在解附近通常表现出**二次收敛**（quadratic convergence）或更快的速度。这是因为在解处，$r_i = 0$，其[海森近似](@entry_id:171462) $\mathbf{J}^T \mathbf{J}$ 与真实[海森矩阵](@entry_id:139140)完全一致。
-   对于**非零残差问题**（即最优解处的残差不为零），被忽略的[海森矩阵](@entry_id:139140)项在解附近不为零，这使得[高斯-牛顿法](@entry_id:173233)通常退化为**[线性收敛](@entry_id:163614)**（linear convergence），[收敛速度](@entry_id:636873)会显著变慢。

#### 稳定性问题：[雅可比矩阵](@entry_id:264467)的[秩亏](@entry_id:754065)

[高斯-牛顿法](@entry_id:173233)一个更严重的缺陷是其稳定性。该方法依赖于求解正规方程 $(\mathbf{J}^T \mathbf{J}) \mathbf{p} = -\mathbf{J}^T \mathbf{r}$。如果雅可比矩阵 $\mathbf{J}$ 的列是线性相关的（即**[秩亏](@entry_id:754065)**），那么矩阵 $\mathbf{J}^T \mathbf{J}$ 将是奇异的（不可逆），导致正规方程没有唯一解或解不稳定（步长 $\mathbf{p}$ 可能变得极大）。

[雅可比矩阵](@entry_id:264467)的[秩亏](@entry_id:754065)通常与**参数不可辨识性**（non-identifiability）有关。当模型的结构或实验的设计使得多个参数（或参数组合）对模型输出产生相同或相似的影响时，就会出现这种情况。

例如，考虑一个模型 $y = \exp(x(\theta_1 + \theta_2))$ 。其[雅可比矩阵](@entry_id:264467)的两个列（分别对应于 $\theta_1$ 和 $\theta_2$ 的[偏导数](@entry_id:146280)）是完全相同的。这意味着我们只能辨识参数的和 $\theta_1 + \theta_2$，而无法独立确定 $\theta_1$ 和 $\theta_2$ 各自的值。在这种情况下，$\mathbf{J}$ 是[秩亏](@entry_id:754065)的，$\mathbf{J}^T \mathbf{J}$ 是奇异的，纯粹的[高斯-牛顿法](@entry_id:173233)会立即失效。

另一个实际例子是带有仪器增益因子 $s$ 的[米氏方程](@entry_id:146495)模型 $y = s \frac{V_{\max}x}{K_m+x}$ 。对参数 $s$ 和 $V_{\max}$ 的[偏导数](@entry_id:146280)分别为 $\frac{V_{\max}x}{K_m+x}$ 和 $\frac{sx}{K_m+x}$。这两列总是成比例的，比例常数为 $\frac{s}{V_{\max}}$。因此，仅凭这种形式的实验数据，我们无法将 $s$ 和 $V_{\max}$ 分开，只能确定它们的乘积 $s \cdot V_{\max}$。这种不可辨识性是实验设计本身的缺陷，仅仅增加更多相同类型的测量点无法解决问题。要打破这种对称性，必须引入一种新的、能独立约束其中一个参数的实验，例如一次校准测量，其响应只依赖于 $s$ 而不依赖于 $V_{\max}$ 和 $K_m$。

### 列文伯格-马夸特算法：稳健的[混合策略](@entry_id:145261)

为了解决[高斯-牛顿法](@entry_id:173233)在雅可比矩阵[秩亏](@entry_id:754065)或近似海森矩阵非正定时的不稳定性，**列文伯格-马夸特算法**（Levenberg-Marquardt, LM）被提出来。LM算法通过引入一个**阻尼项**（damping term）来修正正规方程：

$(\mathbf{J}^T \mathbf{J} + \lambda \mathbf{I}) \mathbf{p} = -\mathbf{J}^T \mathbf{r}$

其中 $\mathbf{I}$ 是[单位矩阵](@entry_id:156724)，$\lambda \ge 0$ 是**阻尼参数**。这个简单的修改带来了深刻的影响：
-   **保证可解性**：由于 $\mathbf{J}^T \mathbf{J}$ 是半正定的，对于任何 $\lambda > 0$，矩阵 $(\mathbf{J}^T \mathbf{J} + \lambda \mathbf{I})$ 都将是正定的，从而保证了[方程组](@entry_id:193238)总是有唯一的、稳定的解。
-   **[混合算法](@entry_id:171959)特性**：阻尼参数 $\lambda$ 在两种不同的优化策略之间扮演了“开关”的角色 。
    -   当 $\lambda$ 很小（接近 0）时，LM 方程近似于高斯-牛顿方程，算法表现出[高斯-牛顿法](@entry_id:173233)的快速收敛特性。
    -   当 $\lambda$ 很大时，对角项 $\lambda \mathbf{I}$ 在方程中占主导地位，步长 $\mathbf{p} \approx -\frac{1}{\lambda} \mathbf{J}^T \mathbf{r}$。由于 $\mathbf{J}^T \mathbf{r}$ 是[目标函数](@entry_id:267263)的梯度，这相当于一个步长很小的**最速下降**（steepest descent）步。[最速下降法](@entry_id:140448)虽然收敛慢，但保证了每一步都会使目标函数值下降（只要步长足够小）。

#### 自适应阻尼策略

LM 算法的精髓在于其**自适应调整**阻尼参数 $\lambda$ 的策略 。在每次迭代中，算法计算出一个试探步长 $\mathbf{p}$，然后评估这个步长的“质量”。质量的评估通过一个称为**增益比**（gain ratio）$\rho$ 的指标来完成：

$\rho = \frac{\text{实际下降量}}{\text{预测下降量}} = \frac{S(\boldsymbol{\beta}_k) - S(\boldsymbol{\beta}_k + \mathbf{p})}{L(\mathbf{0}) - L(\mathbf{p})}$

其中，$S(\boldsymbol{\beta}_k) - S(\boldsymbol{\beta}_k + \mathbf{p})$ 是目标函数的真实减少量，而分母是线性模型预测的减少量。
-   如果 $\rho$ 是正的且接近 1，说明线性近似效果很好，步长是“好”的。算法会接受这个步长，并减小 $\lambda$（例如除以 10），以便在下一次迭代中更接近[高斯-牛顿法](@entry_id:173233)。
-   如果 $\rho$ 很小甚至是负的，说明线性近似很差，步长是“坏”的。算法会拒绝这个步长，并增大 $\lambda$（例如乘以 10），使得下一步更保守，更像[最速下降法](@entry_id:140448)。然后使用新的 $\lambda$ 重新计算步长。

通过这种方式，LM 算法能够自动地在快速但可能不稳定的[高斯-牛顿法](@entry_id:173233)和缓慢但稳健的[最速下降法](@entry_id:140448)之间切换。在远离解的区域（线性近似差），它表现得像[最速下降法](@entry_id:140448)，稳步向最小值靠近；在接近解的区域（线性近似好），它切换到高斯-牛顿模式，实现快速收敛 。

### 扩展与应用

#### 加权[非线性](@entry_id:637147)最小二乘

在许多实际应用中，不同数据点的测量精度可能不同。例如，某些测量的噪声[方差](@entry_id:200758) $\sigma_i^2$ 较大。为了得到更精确的参数估计，我们应该给予精度高（噪声小）的数据点更大的权重。这就引出了**加权非[线性最小二乘法](@entry_id:165427)**（Weighted Nonlinear Least Squares, WNLS）。

其目标函数被修改为：
$S_W(\boldsymbol{\beta}) = \sum_{i=1}^N w_i [r_i(\boldsymbol{\beta})]^2 = \mathbf{r}(\boldsymbol{\beta})^T \mathbf{W} \mathbf{r}(\boldsymbol{\beta})$

其中 $\mathbf{W}$ 是一个对角权重矩阵，对角元素 $w_i > 0$。在统计学上，最优的权重选择是 $w_i = 1/\sigma_i^2$。这样，噪声大的数据点（$\sigma_i^2$ 大）获得的权重 $w_i$ 就小，其对目标函数的贡献也相应减小。

这个加权问题可以通过对高斯-牛顿（或LM）方程进行简单修改来求解 。加权后的正规方程变为：
$(\mathbf{J}^T \mathbf{W} \mathbf{J}) \mathbf{p} = -\mathbf{J}^T \mathbf{W} \mathbf{r}$

从几何上看，权重矩阵 $\mathbf{W}$ 在残差空间中引入了一个新的度量，它有效地预处理了梯度映射，使得算法更加关注那些我们更有把握的数据点。

#### [求解非线性方程](@entry_id:177343)组

非[线性最小二乘法](@entry_id:165427)的一个重要应用是[求解非线性方程](@entry_id:177343)组 $\mathbf{f}(\mathbf{x}) = \mathbf{0}$，其中 $\mathbf{f}: \mathbb{R}^n \to \mathbb{R}^m$。这个问题可以被转化为一个最小二乘问题，即寻找 $\mathbf{x}$ 来最小化 $\|\mathbf{f}(\mathbf{x})\|_2^2$。如果能找到一个 $\mathbf{x}^*$ 使得 $\|\mathbf{f}(\mathbf{x}^*)\|_2^2 = 0$，那么这个 $\mathbf{x}^*$ 就是原[方程组](@entry_id:193238)的一个解。

然而，这种方法有一个重要的陷阱 。最小二乘算法（如LM）寻找的是[目标函数](@entry_id:267263) $\Phi(\mathbf{x}) = \|\mathbf{f}(\mathbf{x})\|_2^2$ 的**局部最小值**。如果原[方程组](@entry_id:193238) $\mathbf{f}(\mathbf{x}) = \mathbf{0}$ 无解，或者目标函数 $\Phi(\mathbf{x})$ 是非凸的，那么算法可能会收敛到一个梯度为零、但目标函数值大于零的局部极小点。这个点是最小二乘问题的“解”，但它并不是原始非[线性方程组的解](@entry_id:150455)。因此，在使用 NLS 方法[求解方程组](@entry_id:152624)时，必须检查最终得到的[残差范数](@entry_id:754273)是否足够接近于零。

总之，非[线性[最小二乘](@entry_id:165427)法](@entry_id:137100)是一个强大而灵活的工具。理解其核心算法（如高斯-[牛顿和](@entry_id:153339)列文伯格-马夸特）的原理、优势和局限性，对于在科学和工程实践中成功地进行[数据建模](@entry_id:141456)和参数估计至关重要。