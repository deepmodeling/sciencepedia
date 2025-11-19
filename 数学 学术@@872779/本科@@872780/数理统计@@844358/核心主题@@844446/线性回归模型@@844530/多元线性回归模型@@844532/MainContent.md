## 引言
[多元线性回归](@entry_id:141458)（Multiple Linear Regression, MLR）是现代数据分析的基石，它提供了一个强大而灵活的框架，用以理解和量化多个预测变量与单一响应变量之间的关系。从经济学中预测GDP增长，到生物学中探究基因表达的影响因素，再到工程学中优化系统性能，MLR的应用无处不在。然而，要真正驾驭这一工具，仅仅了解其基本方程是远远不够的。我们必须深入其核心原理，理解其赖以成立的假设，并掌握其在复杂现实世界问题中的应用技巧。

本文旨在填补理论知识与实际应用之间的鸿沟。许多学习者在初次接触MLR时，往往会遇到理解障碍，例如：[普通最小二乘法](@entry_id:137121)（OLS）背后的几何直觉是什么？为何说OLS在特定条件下是“最优”的？模型设定中的微小变化（如遗漏一个变量或错误处理一个分类特征）会如何严重影响结论？本系列文章将系统地回答这些问题，引领您从基础理论走向高级应用。

在接下来的内容中，我们将分三步构建您的知识体系。首先，在“原理与机制”一章中，我们将深入剖析模型的数学结构，从[矩阵表示法](@entry_id:190318)到OLS[参数估计](@entry_id:139349)，再到奠定其理论基石的[高斯-马尔可夫定理](@entry_id:138437)。接着，在“应用与跨学科联系”一章中，我们将展示MLR如何在经济学、社会科学、生物学等多个领域中大放异彩，通过实例学习如何使用[指示变量](@entry_id:266428)、交互项来捕捉复杂关系。最后，“动手实践”部分将提供一系列精心设计的问题，帮助您巩固所学，将理论转化为解决实际问题的能力。让我们一同开启这段探索[多元线性回归](@entry_id:141458)世界的旅程。

## 原理与机制

本章旨在深入探讨[多元线性回归](@entry_id:141458)模型的基本原理与运作机制。继引言之后，我们将从模型的数学表示法出发，系统地阐述其参数如何通过[普通最小二乘法](@entry_id:137121)（OLS）进行估计，并揭示其背后的几何直觉。随后，我们将讨论[OLS估计量](@entry_id:177304)的关键统计性质，特别是[高斯-马尔可夫定理](@entry_id:138437)（Gauss-Markov theorem）所描述的[最优性条件](@entry_id:634091)。最后，本章将涵盖模型设定中的实际问题，如处理[分类变量](@entry_id:637195)、诊断模型假设的有效性，以及因模型设定不当（如遗漏重要变量）而产生的后果。我们还将介绍如何对模型参数进行统计推断，以评估预测变量的显著性。

### [多元线性回归](@entry_id:141458)模型

[多元线性回归](@entry_id:141458)模型是简单[线性回归](@entry_id:142318)的扩展，它旨在通过一组多个预测变量（也称为自变量或解释变量）来描述一个响应变量（或因变量）的变化。假设我们有 $p$ 个预测变量 $X_1, X_2, \dots, X_p$ 和一个响应变量 $Y$。对于第 $i$ 个观测样本，其模型可以表示为：

$$Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \dots + \beta_p X_{ip} + \epsilon_i$$

其中，$i = 1, 2, \dots, n$ 表示观测样本的索引。在这个方程中：
- $Y_i$ 是第 $i$ 个观测样本的响应变量值。
- $X_{ij}$ 是第 $i$ 个观测样本的第 $j$ 个预测变量值。
- $\beta_0$ 是截距项，表示当所有预测变量都为零时 $Y$ 的[期望值](@entry_id:153208)。
- $\beta_j$（对于 $j=1, \dots, p$）是与预测变量 $X_j$ 相关联的**偏[回归系数](@entry_id:634860)**。它衡量的是在**保持所有其他预测变量不变**的情况下，$X_j$ 每增加一个单位，响应变量 $Y$ 的[期望值](@entry_id:153208)平均变化的量。
- $\epsilon_i$ 是第 $i$ 个观测样本的随机误差项，它代表了所有未被模型中的预测变量所解释的 $Y$ 的变异。

为了更简洁、更普遍地处理这个问题，我们通常使用[矩阵表示法](@entry_id:190318)。将所有 $n$ 个观测样本整合起来，模型可以写成：

$$\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$$

在这个表达式中：
- $\mathbf{y}$ 是一个 $n \times 1$ 的响应向量：$\mathbf{y} = \begin{pmatrix} Y_1 \\ Y_2 \\ \vdots \\ Y_n \end{pmatrix}$。
- $\mathbf{X}$ 是一个 $n \times (p+1)$ 的**[设计矩阵](@entry_id:165826)**。它的第一列通常全是1（对应截距项 $\beta_0$），其余各列是每个预测变量的观测值：
$$ \mathbf{X} = \begin{pmatrix} 1 & X_{11} & X_{12} & \dots & X_{1p} \\ 1 & X_{21} & X_{22} & \dots & X_{2p} \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & X_{n1} & X_{n2} & \dots & X_{np} \end{pmatrix} $$
- $\boldsymbol{\beta}$ 是一个 $(p+1) \times 1$ 的未知参数向量：$\boldsymbol{\beta} = \begin{pmatrix} \beta_0 \\ \beta_1 \\ \vdots \\ \beta_p \end{pmatrix}$。
- $\boldsymbol{\epsilon}$ 是一个 $n \times 1$ 的误差向量：$\boldsymbol{\epsilon} = \begin{pmatrix} \epsilon_1 \\ \epsilon_2 \\ \vdots \\ \epsilon_n \end{pmatrix}$。

### [参数估计](@entry_id:139349)：[普通最小二乘法](@entry_id:137121)

我们的目标是利用观测数据 $(\mathbf{y}, \mathbf{X})$ 来找到对未知参数向量 $\boldsymbol{\beta}$ 的最佳估计，记为 $\hat{\boldsymbol{\beta}}$。最广泛使用的方法是**[普通最小二乘法](@entry_id:137121) (Ordinary Least Squares, OLS)**。

#### OLS原理与[正规方程](@entry_id:142238)

OLS的指导原则是选择能使观测值 $Y_i$ 与[模型拟合](@entry_id:265652)值 $\hat{Y}_i$ 之间差异的平方和最小的系数。这个差异被称为**残差** ($e_i = Y_i - \hat{Y}_i$)。因此，OLS旨在最小化**[残差平方和](@entry_id:174395) (Sum of Squared Residuals, SSR)**，也记为 $S(\boldsymbol{\beta})$。

$$S(\boldsymbol{\beta}) = \sum_{i=1}^{n} e_i^2 = \sum_{i=1}^{n} (Y_i - \hat{Y}_i)^2 = \sum_{i=1}^{n} (Y_i - (\beta_0 + \beta_1 X_{i1} + \dots + \beta_p X_{ip}))^2$$

为了找到最小化 $S(\boldsymbol{\beta})$ 的 $\boldsymbol{\beta}$ 值，我们使用微积分的方法，即计算 $S(\boldsymbol{\beta})$ 对每个系数 $\beta_j$ 的[偏导数](@entry_id:146280)，并令其等于零。这个过程会产生一个由 $(p+1)$ 个线性方程组成的[方程组](@entry_id:193238)，称为**[正规方程](@entry_id:142238) (normal equations)**。

例如，考虑一个有两个预测变量的模型（$p=2$）[@problem_id:1938940]：
$S(\beta_0, \beta_1, \beta_2) = \sum_{i=1}^{n} (Y_i - \beta_0 - \beta_1 X_{i1} - \beta_2 X_{i2})^2$。
对 $\beta_1$ 求偏导并令其为零：
$$\frac{\partial S}{\partial \beta_1} = -2 \sum_{i=1}^{n} X_{i1}(Y_i - \beta_0 - \beta_1 X_{i1} - \beta_2 X_{i2}) = 0$$
整理后得到第二个[正规方程](@entry_id:142238)：
$$\beta_0 \sum X_{i1} + \beta_1 \sum X_{i1}^2 + \beta_2 \sum X_{i1}X_{i2} = \sum X_{i1}Y_i$$
在这个方程中，$\hat{\beta}_2$ 的系数是 $\sum_{i=1}^{n}X_{i1}X_{i2}$。对所有参数（$\beta_0, \beta_1, \dots, \beta_p$）执行此操作，便得到完整的正规方程组。

#### OLS的矩阵解与几何解释

在矩阵形式下，正规方程组可以优雅地表示为：
$$(\mathbf{X}^T\mathbf{X})\hat{\boldsymbol{\beta}} = \mathbf{X}^T\mathbf{y}$$
如果矩阵 $\mathbf{X}^T\mathbf{X}$ 是可逆的（这要求[设计矩阵](@entry_id:165826) $\mathbf{X}$ 的列是线性无关的，即没有完全多重共线性），我们可以解出 OLS 估计量 $\hat{\boldsymbol{\beta}}$：
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}$$
这个公式是[线性回归分析](@entry_id:166896)的核心。一旦我们计算出 $\hat{\boldsymbol{\beta}}$，我们就可以得到**拟合值向量** $\hat{\mathbf{y}}$：
$$\hat{\mathbf{y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$$

OLS估计过程有一个深刻的几何解释。我们可以将观测向量 $\mathbf{y}$ 和[设计矩阵](@entry_id:165826) $\mathbf{X}$ 的各列都看作是 $n$ 维空间中的向量。$\mathbf{X}$ 的列向量张成了一个[子空间](@entry_id:150286)，称为**列空间 (column space)**，记为 $C(\mathbf{X})$。OLS所做的，正是找到[列空间](@entry_id:156444)中离 $\mathbf{y}$ 最近的一个向量，这个向量就是拟合值向量 $\hat{\mathbf{y}}$。几何上，“最近”意味着 $\hat{\mathbf{y}}$ 是 $\mathbf{y}$ 在 $C(\mathbf{X})$ 上的**正交投影 (orthogonal projection)**。残差向量 $\mathbf{e} = \mathbf{y} - \hat{\mathbf{y}}$ 则与 $C(\mathbf{X})$ 中的任何向量都正交。

这个投影操作可以通过一个特殊的矩阵——**[帽子矩阵](@entry_id:174084) (hat matrix)** $\mathbf{H}$ 来实现 [@problem_id:1938932]。将 $\hat{\boldsymbol{\beta}}$ 的表达式代入 $\hat{\mathbf{y}}$ 的定义中：
$$\hat{\mathbf{y}} = \mathbf{X}\left((\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y}\right) = \left(\mathbf{X}(\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\right)\mathbf{y}$$
我们定义[帽子矩阵](@entry_id:174084)为：
$$\mathbf{H} = \mathbf{X}(\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T$$
于是，拟合值向量可以简洁地写成：
$$\hat{\mathbf{y}} = \mathbf{H}\mathbf{y}$$
这个名字的由来很直观：矩阵 $\mathbf{H}$ 作用于观测值向量 $\mathbf{y}$，就给它“戴上了帽子”，得到了拟合值向量 $\hat{\mathbf{y}}$。

让我们通过一个具体的计算来理解这个过程 [@problem_id:1938929]。假设有4个数据点，响应向量 $\mathbf{y}$ 和[设计矩阵](@entry_id:165826) $\mathbf{X}$ 分别为：
$$ \mathbf{y} = \begin{pmatrix} 1 \\ 2 \\ 4 \\ 5 \end{pmatrix}, \quad \mathbf{X} = \begin{pmatrix} 1 & -3 & -1 \\ 1 & -1 & 1 \\ 1 & 1 & 1 \\ 1 & 3 & -1 \end{pmatrix} $$
首先，计算 $\mathbf{X}^T\mathbf{X}$。由于 $\mathbf{X}$ 的列是正交的（它们的[点积](@entry_id:149019)为零），$\mathbf{X}^T\mathbf{X}$ 是一个对角矩阵，这极大地简化了计算：
$$ \mathbf{X}^T\mathbf{X} = \begin{pmatrix} 4 & 0 & 0 \\ 0 & 20 & 0 \\ 0 & 0 & 4 \end{pmatrix} $$
其[逆矩阵](@entry_id:140380)为：
$$ (\mathbf{X}^T\mathbf{X})^{-1} = \begin{pmatrix} 1/4 & 0 & 0 \\ 0 & 1/20 & 0 \\ 0 & 0 & 1/4 \end{pmatrix} $$
接着，计算 $\mathbf{X}^T\mathbf{y}$：
$$ \mathbf{X}^T\mathbf{y} = \begin{pmatrix} 12 \\ 14 \\ 0 \end{pmatrix} $$
现在可以求得[系数估计](@entry_id:175952)向量 $\hat{\boldsymbol{\beta}}$：
$$ \hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y} = \begin{pmatrix} 1/4 & 0 & 0 \\ 0 & 1/20 & 0 \\ 0 & 0 & 1/4 \end{pmatrix} \begin{pmatrix} 12 \\ 14 \\ 0 \end{pmatrix} = \begin{pmatrix} 3 \\ 7/10 \\ 0 \end{pmatrix} $$
因此，估计的回归方程是 $\hat{Y} = 3 + 0.7 X_1 + 0 X_2$。最后，计算拟合值向量 $\hat{\mathbf{y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$：
$$ \hat{\mathbf{y}} = \begin{pmatrix} 1 & -3 & -1 \\ 1 & -1 & 1 \\ 1 & 1 & 1 \\ 1 & 3 & -1 \end{pmatrix} \begin{pmatrix} 3 \\ 7/10 \\ 0 \end{pmatrix} = \begin{pmatrix} 3 - 2.1 \\ 3 - 0.7 \\ 3 + 0.7 \\ 3 + 2.1 \end{pmatrix} = \begin{pmatrix} 0.9 \\ 2.3 \\ 3.7 \\ 5.1 \end{pmatrix} $$
这就是观测向量 $\mathbf{y}$ 在 $\mathbf{X}$ 列空间上的[正交投影](@entry_id:144168)。

### 模型应用：进行预测

一旦[回归模型](@entry_id:163386)被成功拟合，即得到[系数估计](@entry_id:175952)值 $\hat{\beta}_0, \hat{\beta}_1, \dots, \hat{\beta}_p$，其最直接的应用之一就是进行预测。给定一组新的预测变量值 $x_1, x_2, \dots, x_p$，我们可以通过将这些值代入拟合的回归方程来预测响应变量的[期望值](@entry_id:153208) $\hat{y}$。

例如，假设一个环境机构建立了一个模型来预测空气[质量指数](@entry_id:190779)（AQI），其拟合方程为 [@problem_id:1938948]：
$$\hat{y} = 22.5 + 1.85 x_1 + 0.62 x_2 - 3.10 x_3$$
其中 $x_1$ 是交通流量（千辆/天），$x_2$ 是工业产出指数，$x_3$ 是平均风速（km/h）。如果某天的[交通流](@entry_id:165354)量预计为45千辆（$x_1=45$），工业产出指数为30（$x_2=30$），平均风速为12 km/h（$x_3=12$），那么预测的AQI为：
$$\hat{y} = 22.5 + 1.85(45) + 0.62(30) - 3.10(12) = 22.5 + 83.25 + 18.6 - 37.2 = 87.15$$
因此，该模型预测当天的AQI大约为87.2。

### [OLS估计量](@entry_id:177304)的统计性质

除了提供[参数估计](@entry_id:139349)值之外，我们还关心这些估计量的统计性质。一个好的估计量应该“平均而言”是正确的（无偏性），并且在所有同类估计量中具有最小的[方差](@entry_id:200758)（有效性）。

#### [高斯-马尔可夫定理](@entry_id:138437)及其假设

**[高斯-马尔可夫定理](@entry_id:138437)**是线性模型理论的基石。它指出，在一系列特定假设下，[OLS估计量](@entry_id:177304)是**[最佳线性无偏估计量](@entry_id:137602) (Best Linear Unbiased Estimator, BLUE)**。“最佳”意味着在所有线性和无偏的估计量中，[OLS估计量](@entry_id:177304)的[方差](@entry_id:200758)最小。这些假设（通常称为[高斯-马尔可夫假设](@entry_id:165534)）如下 [@problem_id:1938990]：

1.  **参数线性 (Linearity in parameters)**：模型必须是参数 $\boldsymbol{\beta}$ 的线性函数，即 $\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$。
2.  **误差项的零条件均值 (Zero conditional mean of errors)**：给定任意预测变量的值，误差项的[期望值](@entry_id:153208)为零，即 $E[\boldsymbol{\epsilon} | \mathbf{X}] = \mathbf{0}$。这意味着预测变量不包含关于误差项均值的任何信息。
3.  **同[方差](@entry_id:200758)与无[自相关](@entry_id:138991) (Homoscedasticity and no autocorrelation)**：所有误差项具有相同的[方差](@entry_id:200758)（$\text{Var}(\epsilon_i) = \sigma^2$），并且彼此不相关（对于 $i \neq j$，$\text{Cov}(\epsilon_i, \epsilon_j) = 0$）。在矩阵形式下，这表示为 $\text{Var}(\boldsymbol{\epsilon} | \mathbf{X}) = \sigma^2 \mathbf{I}_n$，其中 $\mathbf{I}_n$ 是 $n \times n$ 的[单位矩阵](@entry_id:156724)。
4.  **无完全多重共线性 (No perfect multicollinearity)**：[设计矩阵](@entry_id:165826) $\mathbf{X}$ 的列是[线性无关](@entry_id:148207)的，即 $\mathbf{X}$ 具有[满列秩](@entry_id:749628)。这意味着没有任何一个预测变量可以被其他预测变量的[线性组合](@entry_id:154743)完美地预测。

值得注意的是，[高斯-马尔可夫定理](@entry_id:138437)并不要求误差项服从正态分布。[正态性假设](@entry_id:170614)是进行精确的小样本推断（如t检验和[F检验](@entry_id:274297)）时才需要的额外条件。

#### OLS的无偏性

我们可以证明，只要满足误差项零均值的假设 ($E[\boldsymbol{\epsilon}]=\mathbf{0}$)，[OLS估计量](@entry_id:177304)就是无偏的，即 $E[\hat{\boldsymbol{\beta}}] = \boldsymbol{\beta}$ [@problem_id:1938946]。证明过程如下：

我们从 $\hat{\boldsymbol{\beta}}$ 的表达式开始，并代入真实模型 $\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon}$：
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{y} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T(\mathbf{X}\boldsymbol{\beta} + \boldsymbol{\epsilon})$$
利用[分配律](@entry_id:144084)展开：
$$\hat{\boldsymbol{\beta}} = (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{X}\boldsymbol{\beta} + (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\boldsymbol{\epsilon}$$
由于 $(\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\mathbf{X} = \mathbf{I}$（单位矩阵），上式简化为：
$$\hat{\boldsymbol{\beta}} = \boldsymbol{\beta} + (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\boldsymbol{\epsilon}$$
现在，我们对 $\hat{\boldsymbol{\beta}}$ 取期望。由于 $\boldsymbol{\beta}$ 是常数向量，$\mathbf{X}$ 被视为固定的，而 $E[\boldsymbol{\epsilon}] = \mathbf{0}$：
$$E[\hat{\boldsymbol{\beta}}] = E[\boldsymbol{\beta} + (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^T\boldsymbol{\epsilon}] = \boldsymbol{\beta} + (\mathbf{X}^T\mathbf{X})^{-1}\mathbf{X}^TE[\boldsymbol{\epsilon}] = \boldsymbol{\beta} + \mathbf{0} = \boldsymbol{\beta}$$
这证明了 $\hat{\boldsymbol{\beta}}$ 是 $\boldsymbol{\beta}$ 的[无偏估计量](@entry_id:756290)。这意味着，如果我们反复从同一总体中抽样并拟合模型，估计出的系数向量的平均值将收敛于真实的系数向量。

### 模型设定与诊断

建立一个可靠的[回归模型](@entry_id:163386)不仅仅是运行OLS那么简单。我们需要仔细考虑模型的设定，并对拟合后的模型进行诊断，以检验其基本假设是否成立。

#### 处理[分类预测变量](@entry_id:636655)

[线性回归](@entry_id:142318)要求输入是数值。但现实世界的数据经常包含[分类变量](@entry_id:637195)，如地区（“东部”、“西部”）、产品类型（“A”、“B”、“C”）等。直接将这些类别编码为1, 2, 3...并放入模型是错误的做法，因为这会强加一种不存在的[序数](@entry_id:150084)关系和等距关系。

正确的处理方法是创建**[虚拟变量](@entry_id:138900) (dummy variables)** 或称[指示变量](@entry_id:266428)。对于一个有 $L$ 个水平（类别）的[分类变量](@entry_id:637195)，我们需要创建 $L-1$ 个[虚拟变量](@entry_id:138900)。其中一个水平被选为**基准类别 (baseline category)**，它由所有[虚拟变量](@entry_id:138900)都取值为0来表示。其他每个[虚拟变量](@entry_id:138900)对应一个非基准类别，当观测样本属于该类别时取值为1，否则为0。

例如，一个模型需要包含有四个水平（'Seattle', 'Denver', 'Austin', 'Boston'）的工厂位置变量 [@problem_id:1938978]。如果我们选择 'Seattle' 作为基准，我们需要创建3个[虚拟变量](@entry_id:138900)：
- $D_1 = 1$ 如果位置是 'Denver'，否则为0。
- $D_2 = 1$ 如果位置是 'Austin'，否则为0。
- $D_3 = 1$ 如果位置是 'Boston'，否则为0。

这样，四个位置的编码如下：
- Seattle: $(D_1, D_2, D_3) = (0,0,0)$
- Denver: $(D_1, D_2, D_3) = (1,0,0)$
- Austin: $(D_1, D_2, D_3) = (0,1,0)$
- Boston: $(D_1, D_2, D_3) = (0,0,1)$

包含这些[虚拟变量](@entry_id:138900)的[回归模型](@entry_id:163386)可能是：$Y = \beta_0 + \beta_1 X_1 + \gamma_1 D_1 + \gamma_2 D_2 + \gamma_3 D_3 + \epsilon$。在这里，$\gamma_1$ 衡量的是，在控制了连续变量 $X_1$ 后，'Denver' 工厂相对于 'Seattle' 工厂（基准）在 $Y$ 上的平[均差](@entry_id:138238)异。

只使用 $L-1$ 个[虚拟变量](@entry_id:138900)是为了避免**[虚拟变量陷阱](@entry_id:635707) (dummy variable trap)**，这是一种完美的共[线性形式](@entry_id:276136)。如果创建了 $L$ 个[虚拟变量](@entry_id:138900)，它们的和将永远等于1，这与模型中已经存在的截距项（其对应的预测变量是一个恒为1的向量）是[线性相关](@entry_id:185830)的，导致 $\mathbf{X}^T\mathbf{X}$ 不可逆。

#### 模型设定误差：遗漏变量偏误

[高斯-马尔可夫假设](@entry_id:165534)之一是模型的设定是正确的。如果我们的模型遗漏了一个或多个与响应变量相关且与其他预测变量也相关的变量，那么[OLS估计量](@entry_id:177304)将不再是无偏的。这种现象称为**遗漏变量偏误 (Omitted Variable Bias)**。

假设真实模型是 $\mathbf{y} = \mathbf{X}_1\boldsymbol{\beta}_1 + \mathbf{X}_2\boldsymbol{\beta}_2 + \boldsymbol{\epsilon}$，其中 $\boldsymbol{\beta}_2 \neq \mathbf{0}$。但我们错误地拟合了一个更简单的模型：$\mathbf{y} = \mathbf{X}_1\boldsymbol{\beta}_1 + \boldsymbol{\nu}$。基于这个错误模型计算出的估计量是 $\hat{\boldsymbol{\beta}}_1 = (\mathbf{X}_1^T\mathbf{X}_1)^{-1}\mathbf{X}_1^T\mathbf{y}$。我们可以推导出它的[期望值](@entry_id:153208) [@problem_id:1938960]：
$$E[\hat{\boldsymbol{\beta}}_1] = E[(\mathbf{X}_1^T\mathbf{X}_1)^{-1}\mathbf{X}_1^T(\mathbf{X}_1\boldsymbol{\beta}_1 + \mathbf{X}_2\boldsymbol{\beta}_2 + \boldsymbol{\epsilon})] = \boldsymbol{\beta}_1 + (\mathbf{X}_1^T\mathbf{X}_1)^{-1}\mathbf{X}_1^T\mathbf{X}_2\boldsymbol{\beta}_2$$
因此，$\hat{\boldsymbol{\beta}}_1$ 的偏误为：
$$\text{Bias}(\hat{\boldsymbol{\beta}}_1) = E[\hat{\boldsymbol{\beta}}_1] - \boldsymbol{\beta}_1 = (\mathbf{X}_1^T\mathbf{X}_1)^{-1}\mathbf{X}_1^T\mathbf{X}_2\boldsymbol{\beta}_2$$
这个偏误只有在两种情况下才为零：
1.  $\boldsymbol{\beta}_2 = \mathbf{0}$：即被遗漏的变量实际上与响应变量无关。
2.  $\mathbf{X}_1^T\mathbf{X}_2 = \mathbf{0}$：即被遗漏的变量与模型中包含的变量完全不相关（正交）。
在大多数现实情况中，这两个条件都难以满足，因此遗漏重要变量通常会导致有偏的估计。

#### 检验模型假设：[残差分析](@entry_id:191495)

为了检验[高斯-马尔可夫假设](@entry_id:165534)（特别是[同方差性](@entry_id:634679)）是否成立，一个关键的诊断工具是**[残差图](@entry_id:169585)**，最常见的是**残差 vs. 拟合值图**。该图以拟合值 $\hat{y}_i$ 为横轴，以残差 $e_i = y_i - \hat{y}_i$ 为纵轴。

-   **理想情况**：如果模型假设成立，[残差图](@entry_id:169585)应该呈现为一团围绕水平线 $y=0$ 随机散布的点，且点的垂直散布范围（即[方差](@entry_id:200758)）不随拟合值的变化而系统性地改变。这表明[误差方差](@entry_id:636041)是恒定的（**[同方差性](@entry_id:634679), homoscedasticity**）。
-   **[异方差性](@entry_id:136378) (Heteroscedasticity)**：如果[误差方差](@entry_id:636041)不是常数，[残差图](@entry_id:169585)中通常会出现模式。一个典型的模式是**扇形或锥形** [@problem_id:1938938]。例如，如果残差的散布范围随着拟合值的增加而扩大，这表明误差的[方差](@entry_id:200758)随着响应变量的[期望值](@entry_id:153208)增加而增加。这种情况在经济数据中很常见（如高收入人群的消费行为差异更大）。[异方差性](@entry_id:136378)违反了[高斯-马尔可夫假设](@entry_id:165534)，虽然[OLS估计量](@entry_id:177304)仍然是无偏的，但它不再是BLUE，且其标准误的计算会不准确，影响[假设检验](@entry_id:142556)的有效性。
-   **[非线性](@entry_id:637147)**：如果[残差图](@entry_id:169585)呈现出明显的曲线模式（如U形或倒U形），这通常表明模型未能捕捉到预测变量和响应变量之间的非线性关系，即模型均值设定有误。

### [多元回归](@entry_id:144007)中的推断

在确定模型设定合理且其假设基本满足后，我们可以进行[统计推断](@entry_id:172747)，以评估每个预测变量对响应变量的影响是否**统计显著**。

对于单个[回归系数](@entry_id:634860) $\beta_j$，我们通常想检验它是否等于零。这对应于检验在控制了模型中所有其他变量后，$X_j$ 是否与 $Y$ 存在[线性关系](@entry_id:267880)。检验的[原假设](@entry_id:265441)和[备择假设](@entry_id:167270)通常设置为 [@problem_id:1938949]：
-   **[原假设](@entry_id:265441) ($H_0$)**: $\beta_j = 0$ （$X_j$ 对 $Y$ 没有线性影响）
-   **备择假设 ($H_a$)**: $\beta_j \neq 0$ （$X_j$ 对 $Y$ 有线性影响）

这个检验通常使用 **[t检验](@entry_id:272234)** 来完成。[t统计量](@entry_id:177481)的计算公式为：
$$t = \frac{\hat{\beta}_j - 0}{\text{SE}(\hat{\beta}_j)}$$
其中 $\hat{\beta}_j$ 是 $\beta_j$ 的OLS估计值，$\text{SE}(\hat{\beta}_j)$ 是其标准误。如果计算出的[t统计量](@entry_id:177481)的[绝对值](@entry_id:147688)足够大（超过了在特定[显著性水平](@entry_id:170793)下[t分布](@entry_id:267063)的临界值），我们就可以拒绝[原假设](@entry_id:265441)，断定 $X_j$ 是一个统计上显著的预测变量。

例如，在预测数据中心能耗的模型 $Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 + \varepsilon$ 中，要检验CPU平均负载（$X_3$）是否是能耗的显著预测因子，就需要对系数 $\beta_3$ 进行[t检验](@entry_id:272234)，其假设为 $H_0: \beta_3 = 0$ vs. $H_a: \beta_3 \neq 0$。