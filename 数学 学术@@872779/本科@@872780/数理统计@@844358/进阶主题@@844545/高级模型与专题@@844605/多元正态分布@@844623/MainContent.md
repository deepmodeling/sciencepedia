## 引言
[多元正态分布](@entry_id:175229)，作为单变量[正态分布](@entry_id:154414)向多维空间的自然延伸，是统计学和数据科学中描述多个连续变量联合行为的基石。在现实世界中，数据点很少是孤立的；股票收益、生物指标、或传感器读数往往相互关联。理解并建模这些变量间的复杂依赖关系，是进行准确预测和[科学推断](@entry_id:155119)的关键。然而，如何用一个统一的数学框架来捕捉这种多维度的相关结构，正是许多定量分析面临的核心挑战。

本文旨在系统地揭开[多元正态分布](@entry_id:175229)的面纱，带领读者深入其核心。通过学习，你将不仅掌握其数学定义，更将领会其背后深刻的几何直觉和强大的分析能力。文章分为三个核心部分：
在 **原理与机制** 章节中，我们将从定义出发，详细拆解其概率密度函数，并探讨其核心性质，如线性变换、[边际分布](@entry_id:264862)、[条件分布](@entry_id:138367)以及独立性的深刻含义。
接着，在 **应用与[交叉](@entry_id:147634)学科联系** 章节，我们将走出纯粹的数学理论，探索[多元正态分布](@entry_id:175229)如何在金融建模、机器学习、信号处理等前沿领域中扮演关键角色，连接起看似无关的学科。
最后，在 **动手实践** 部分，你将有机会通过具体的计算练习，将理论知识转化为解决实际问题的技能。

让我们首先进入第一章，深入探索[多元正态分布](@entry_id:175229)的基本原理与机制。

## 原理与机制

在统计学领域，[多元正态分布](@entry_id:175229)（Multivariate Normal Distribution），或称多元[高斯分布](@entry_id:154414)，是描述多个[连续随机变量](@entry_id:166541)联合行为的最重要的[概率分布](@entry_id:146404)之一。它作为单变量[正态分布](@entry_id:154414)的自然推广，在金融、工程、生物科学和机器学习等众多领域中扮演着核心角色。本章将深入探讨[多元正态分布](@entry_id:175229)的基本原理、核心性质及其背后的数学机制。

### 定义与概率密度函数

一个 $p$ 维随机向量 $\mathbf{X} = (X_1, X_2, \dots, X_p)^T$ 如果服从[多元正态分布](@entry_id:175229)，我们记为 $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$。该[分布](@entry_id:182848)完全由两个参数确定：

1.  **[均值向量](@entry_id:266544) (Mean Vector)** $\boldsymbol{\mu}$：一个 $p \times 1$ 的向量，其中第 $i$ 个元素 $\mu_i = \mathbb{E}[X_i]$ 是随机向量 $\mathbf{X}$ 中第 $i$ 个分量的[期望值](@entry_id:153208)。从几何上看，$\boldsymbol{\mu}$ 定义了[分布](@entry_id:182848)的中心或位置。

2.  **协方差矩阵 (Covariance Matrix)** $\boldsymbol{\Sigma}$：一个 $p \times p$ 的[对称半正定矩阵](@entry_id:163376)。其对角[线元](@entry_id:196833)素 $\Sigma_{ii} = \operatorname{Var}(X_i)$ 是各个分量的[方差](@entry_id:200758)，而非对角[线元](@entry_id:196833)素 $\Sigma_{ij} = \operatorname{Cov}(X_i, X_j)$ 则是不同分量之间的协[方差](@entry_id:200758)。协方差矩阵描述了随机向量各分量的离散程度以及它们之间的线性相关性。

当协方差矩阵 $\boldsymbol{\Sigma}$ 是严格正定（即非奇异，[行列式](@entry_id:142978) $|\boldsymbol{\Sigma}| > 0$）时，[多元正态分布](@entry_id:175229)存在一个[概率密度函数](@entry_id:140610) (PDF)。对于一个具体的观测值向量 $\mathbf{x} = (x_1, x_2, \dots, x_p)^T$，其[概率密度](@entry_id:175496)由以下公式给出：

$$
f(\mathbf{x}; \boldsymbol{\mu}, \boldsymbol{\Sigma}) = \frac{1}{(2\pi)^{p/2} |\boldsymbol{\Sigma}|^{1/2}} \exp\left( -\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}) \right)
$$

这个公式的结构值得我们仔细分析。常数项 $\frac{1}{(2\pi)^{p/2} |\boldsymbol{\Sigma}|^{1/2}}$ 是归一化因子，确保整个概率密度函数在 $\mathbb{R}^p$ 空间上的积分为1。指数部分的核心是一个二次型 $(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu})$，这个量被称为 $\mathbf{x}$ 相对于均值 $\boldsymbol{\mu}$ 的**[马氏距离](@entry_id:269828)的平方 (squared Mahalanobis distance)**。它度量了一个点 $\mathbf{x}$ 到[分布](@entry_id:182848)中心 $\boldsymbol{\mu}$ 的“[统计距离](@entry_id:270491)”，并考虑了各分量之间的相关性。

为了更具体地理解这个公式，让我们来看一个二维（即二元）正态分布的例子 [@problem_id:1939216]。假设一个二维随机向量 $\mathbf{X} = (X_1, X_2)^T$ 的[均值向量](@entry_id:266544)为 $\boldsymbol{\mu} = \begin{pmatrix} -1 \\ 3 \end{pmatrix}$，[协方差矩阵](@entry_id:139155)为 $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & -2 \\ -2 & 5 \end{pmatrix}$。

首先，我们需要计算 $\boldsymbol{\Sigma}$ 的[行列式](@entry_id:142978)和[逆矩阵](@entry_id:140380)：
$|\boldsymbol{\Sigma}| = (4)(5) - (-2)(-2) = 20 - 4 = 16$。
$\boldsymbol{\Sigma}^{-1} = \frac{1}{|\boldsymbol{\Sigma}|} \begin{pmatrix} 5 & 2 \\ 2 & 4 \end{pmatrix} = \frac{1}{16} \begin{pmatrix} 5 & 2 \\ 2 & 4 \end{pmatrix}$。

接下来，我们计算指数中的二次型。令 $\mathbf{x} - \boldsymbol{\mu} = \begin{pmatrix} x_1 - (-1) \\ x_2 - 3 \end{pmatrix} = \begin{pmatrix} x_1 + 1 \\ x_2 - 3 \end{pmatrix}$。
$$
(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}) = \begin{pmatrix} x_1+1 & x_2-3 \end{pmatrix} \left(\frac{1}{16} \begin{pmatrix} 5 & 2 \\ 2 & 4 \end{pmatrix}\right) \begin{pmatrix} x_1+1 \\ x_2-3 \end{pmatrix} = \frac{1}{16} \left( 5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2 \right)
$$

将这些部分代入PDF公式 ($p=2$)，我们得到该[二元正态分布](@entry_id:165129)的显式概率密度函数：
$$
f(x_1, x_2) = \frac{1}{(2\pi)^{2/2} (16)^{1/2}} \exp\left( -\frac{1}{2} \cdot \frac{1}{16} \left(5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2\right) \right)
$$
$$
f(x_1, x_2) = \frac{1}{8\pi} \exp\left( -\frac{1}{32}\left(5(x_1+1)^2 + 4(x_1+1)(x_2-3) + 4(x_2-3)^2\right) \right)
$$
这个例子清晰地展示了[均值向量](@entry_id:266544)和协方差矩阵如何直接塑造概率密度的具体形式。

### 几何解释：等高线与协方差矩阵

[多元正态分布](@entry_id:175229)的[概率密度函数](@entry_id:140610)具有优美的几何结构。PDF中 $f(\mathbf{x})$ 为常数的点集构成了等[概率密度](@entry_id:175496)轮廓，我们称之为**等高线 (contours)**。这些[等高线](@entry_id:268504)由方程 $(\mathbf{x}-\boldsymbol{\mu})^T \boldsymbol{\Sigma}^{-1} (\mathbf{x}-\boldsymbol{\mu}) = c$（其中 $c$ 是一个正常数）定义。这个方程描述了 $\mathbb{R}^p$ 空间中的一个椭球（在二维情况下是椭圆）。

这些椭球的共同中心是[均值向量](@entry_id:266544) $\boldsymbol{\mu}$。而椭球的形状、大小和方向则完全由[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}$ 决定。具体来说，椭球的主轴方向由 $\boldsymbol{\Sigma}$ 的**[特征向量](@entry_id:151813) (eigenvectors)** 给出，而主轴的长度与 $\boldsymbol{\Sigma}$ 的**[特征值](@entry_id:154894) (eigenvalues)** 的平方根成正比。

让我们通过一个例子来阐明这一点 [@problem_id:1320466]。考虑一个[二元正态分布](@entry_id:165129)，其协方差矩阵为 $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & 2 \\ 2 & 9 \end{pmatrix}$。[等高线](@entry_id:268504)是椭圆，其[主轴](@entry_id:172691)方向由 $\boldsymbol{\Sigma}$ 的[特征向量](@entry_id:151813)决定。为了找到这些方向，我们求解[特征值方程](@entry_id:192306) $\det(\boldsymbol{\Sigma} - \lambda \mathbf{I}) = 0$：
$$
\det \begin{pmatrix} 4-\lambda & 2 \\ 2 & 9-\lambda \end{pmatrix} = (4-\lambda)(9-\lambda) - 4 = \lambda^2 - 13\lambda + 32 = 0
$$
[特征值](@entry_id:154894)为 $\lambda = \frac{13 \pm \sqrt{13^2 - 4(32)}}{2} = \frac{13 \pm \sqrt{41}}{2}$。

较长的**主长轴 (major axis)** 对应于较大的[特征值](@entry_id:154894) $\lambda_1 = \frac{13 + \sqrt{41}}{2}$。该轴的方向由对应的[特征向量](@entry_id:151813) $\mathbf{v}_1 = (v_1, v_2)^T$ 给出，满足 $(\boldsymbol{\Sigma} - \lambda_1 \mathbf{I})\mathbf{v}_1 = \mathbf{0}$。即：
$$
(4 - \lambda_1)v_1 + 2v_2 = 0
$$
主长轴的斜率 $m = v_2/v_1 = \frac{\lambda_1 - 4}{2} = \frac{(13+\sqrt{41})/2 - 4}{2} = \frac{5+\sqrt{41}}{4}$。
因此，该轴[线与](@entry_id:177118)正x轴的夹角 $\theta$ 为 $\arctan(m) = \arctan\left(\frac{5+\sqrt{41}}{4}\right) \approx 70.7^\circ$。这说明椭圆是“倾斜”的，其方向由变量之间的协[方差](@entry_id:200758)（此处为 $\Sigma_{12}=2$）决定。如果协[方差](@entry_id:200758)为零，则 $\boldsymbol{\Sigma}$ 为对角矩阵，[特征向量](@entry_id:151813)将与坐标轴平行，椭圆的轴线也会与坐标轴对齐。

### 核心性质

[多元正态分布](@entry_id:175229)之所以在理论和应用中如此普遍，很大程度上归功于其优雅的数学性质。

#### [线性变换](@entry_id:149133)的不变性

[多元正态分布](@entry_id:175229)的一个最基本且强大的性质是它在**线性变换**下是封闭的。这意味着，一个多元正态随机向量的任何线性变换（或[仿射变换](@entry_id:144885)）的结果仍然是一个多元正态随机向量。

形式上，如果 $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$，并且我们定义一个新的随机向量 $\mathbf{Y} = A\mathbf{X} + \mathbf{b}$，其中 $A$ 是一个 $q \times p$ 的常数矩阵，$\mathbf{b}$ 是一个 $q \times 1$ 的常数向量，那么 $\mathbf{Y}$ 的[分布](@entry_id:182848)是：
$$
\mathbf{Y} \sim \mathcal{N}_q(A\boldsymbol{\mu} + \mathbf{b}, A\boldsymbol{\Sigma}A^T)
$$
这个性质非常有用，因为它允许我们从已知的正态向量导出其他相关正态向量的[分布](@entry_id:182848)，而无需重新进行复杂的推导。例如，在质量控制中，我们可能测量一组原始数据 $\mathbf{X}$，然后计算一些性能指标 $\mathbf{Y}$，这些指标是原始数据的线性组合 [@problem_id:1939221]。

假设三项电压测量值 $\mathbf{X}=(X_1, X_2, X_3)^T \sim \mathcal{N}_3(\boldsymbol{\mu}, \boldsymbol{\Sigma})$，其中 $\boldsymbol{\mu} = \begin{pmatrix} 5 \\ 8 \\ 4 \end{pmatrix}$，$\boldsymbol{\Sigma} = \begin{pmatrix} 3 & -1 & 1 \\ -1 & 5 & 0 \\ 1 & 0 & 2 \end{pmatrix}$。我们关心两个性能指标 $Y_1 = X_1 - X_2$ 和 $Y_2 = X_2 - X_3$。我们可以将这个变换写成矩阵形式 $\mathbf{Y} = A\mathbf{X}$，其中 $\mathbf{Y} = \begin{pmatrix} Y_1 \\ Y_2 \end{pmatrix}$ 且 $A = \begin{pmatrix} 1 & -1 & 0 \\ 0 & 1 & -1 \end{pmatrix}$。
$\mathbf{Y}$ 的[均值向量](@entry_id:266544)为 $E[\mathbf{Y}] = A\boldsymbol{\mu} = \begin{pmatrix} 5-8 \\ 8-4 \end{pmatrix} = \begin{pmatrix} -3 \\ 4 \end{pmatrix}$。
$\mathbf{Y}$ 的协方差矩阵为 $\operatorname{Cov}(\mathbf{Y}) = A\boldsymbol{\Sigma}A^T$。
$$
A\boldsymbol{\Sigma}A^T = \begin{pmatrix} 1 & -1 & 0 \\ 0 & 1 & -1 \end{pmatrix} \begin{pmatrix} 3 & -1 & 1 \\ -1 & 5 & 0 \\ 1 & 0 & 2 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ -1 & 1 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 4 & -6 & 1 \\ -2 & 5 & -2 \end{pmatrix} \begin{pmatrix} 1 & 0 \\ -1 & 1 \\ 0 & -1 \end{pmatrix} = \begin{pmatrix} 10 & -7 \\ -7 & 7 \end{pmatrix}
$$
因此，性能指标向量 $\mathbf{Y}$ 服从[二元正态分布](@entry_id:165129) $\mathcal{N}_2\left(\begin{pmatrix} -3 \\ 4 \end{pmatrix}, \begin{pmatrix} 10 & -7 \\ -7 & 7 \end{pmatrix}\right)$。

#### [边际分布](@entry_id:264862)

[线性变换](@entry_id:149133)性质的一个直接推论是，多元正态向量的任何子向量（即其**[边际分布](@entry_id:264862) (marginal distributions)**）也服从正态分布。要找到一个子向量的[分布](@entry_id:182848)，我们只需从原始的[均值向量](@entry_id:266544)和协方差矩阵中“提取”出相应的行和列即可。

例如，如果 $\mathbf{X} = \begin{pmatrix} \mathbf{X}_1 \\ \mathbf{X}_2 \end{pmatrix} \sim \mathcal{N}_p\left(\begin{pmatrix} \boldsymbol{\mu}_1 \\ \boldsymbol{\mu}_2 \end{pmatrix}, \begin{pmatrix} \boldsymbol{\Sigma}_{11} & \boldsymbol{\Sigma}_{12} \\ \boldsymbol{\Sigma}_{21} & \boldsymbol{\Sigma}_{22} \end{pmatrix}\right)$，那么 $\mathbf{X}_1$ 的[边际分布](@entry_id:264862)就是 $\mathbf{X}_1 \sim \mathcal{N}(\boldsymbol{\mu}_1, \boldsymbol{\Sigma}_{11})$。

这个规则非常直观。考虑一个机器人部件的长、宽、高 $X_1, X_2, X_3$ 服从三元正态分布，其参数为 $\boldsymbol{\mu} = \begin{pmatrix} 20.0 \\ 8.0 \\ 5.0 \end{pmatrix}$ 和 $\boldsymbol{\Sigma} = \begin{pmatrix} 0.36 & 0.12 & 0.08 \\ 0.12 & 0.25 & 0.10 \\ 0.08 & 0.10 & 0.16 \end{pmatrix}$ [@problem_id:1939262]。如果我们只关心其长度 $X_1$ 的[分布](@entry_id:182848)，我们只需查看 $\boldsymbol{\mu}$ 的第一个元素和 $\boldsymbol{\Sigma}$ 的 $(1,1)$ 元素。因此，$X_1$ 的[边际分布](@entry_id:264862)是单变量正态分布 $\mathcal{N}(\mu_1, \Sigma_{11}) = \mathcal{N}(20.0, 0.36)$。

#### [独立性与不相关性](@entry_id:268517)

对于一般的[随机变量](@entry_id:195330)，不相关（即协[方差](@entry_id:200758)为零）并不一定意味着统计独立。然而，对于联合呈正态分布的[随机变量](@entry_id:195330)，这两个概念是等价的。这是[多元正态分布](@entry_id:175229)一个非常特殊的性质。

如果 $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$，那么其任意两个分量 $X_i$ 和 $X_j$（$i \neq j$）是独立的，当且仅当它们的协[方差](@entry_id:200758) $\Sigma_{ij} = 0$。更一般地，子向量 $\mathbf{X}_1$ 和 $\mathbf{X}_2$ 是独立的，当且仅当它们之间的[协方差矩阵](@entry_id:139155)块 $\boldsymbol{\Sigma}_{12}$（以及其转置 $\boldsymbol{\Sigma}_{21}$）是零矩阵。

我们可以通过考察[二元正态分布](@entry_id:165129)的PDF来直观地理解这一点 [@problem_id:1939205]。二元PDF的一般形式包含一个交叉项 $-2\rho(\frac{x-\mu_X}{\sigma_X})(\frac{y-\mu_Y}{\sigma_Y})$，其中 $\rho$ 是相关系数。如果 $X$ 和 $Y$ 不相关，即 $\rho=0$，则此交叉项消失。PDF简化为：
$$
f(x, y) = \frac{1}{2 \pi \sigma_X \sigma_Y} \exp\left( -\frac{1}{2} \left[ \left(\frac{x - \mu_X}{\sigma_X}\right)^2 + \left(\frac{y - \mu_Y}{\sigma_Y}\right)^2 \right] \right)
$$
这个表达式可以分解为两个独立函数的乘积：
$$
f(x, y) = \left[ \frac{1}{\sigma_X\sqrt{2\pi}} \exp\left(-\frac{(x-\mu_X)^2}{2\sigma_X^2}\right) \right] \left[ \frac{1}{\sigma_Y\sqrt{2\pi}} \exp\left(-\frac{(y-\mu_Y)^2}{2\sigma_Y^2}\right) \right] = f_X(x) f_Y(y)
$$
由于联合密度是[边际密度](@entry_id:276750)的乘积，因此 $X$ 和 $Y$ 是独立的。在卫星通信系统中，如果两个独立放大器的噪声电压 $(X, Y)$ 服从均值为零的[二元正态分布](@entry_id:165129)且不相关 ($\rho=0$)，那么它们是独立的。因此，计算 $P(X > 0 \text{ and } Y > 0)$ 的概率就简化为 $P(X > 0) \times P(Y > 0)$。由于正态分布关于其均值对称，对于均值为零的情况，$P(X > 0) = 0.5$ 和 $P(Y > 0) = 0.5$，所以联合概率为 $0.5 \times 0.5 = 0.25$ [@problem_id:1939205]。

这个性质也为我们提供了一个强大的设计工具。例如，在[通信系统](@entry_id:265921)中，我们可能希望构造两个统计独立的性能指标 $Y_1$ 和 $Y_2$，它们是原始正态测量值 $X_1, X_2$ 的[线性组合](@entry_id:154743) [@problem_id:1939250]。如果 $Y_1 = X_1 + X_2$ 和 $Y_2 = X_1 + kX_2$，由于 $(Y_1, Y_2)$ 是联合正态的，要使它们独立，我们只需使其协[方差](@entry_id:200758)为零。
$\operatorname{Cov}(Y_1, Y_2) = \operatorname{Cov}(X_1+X_2, X_1+kX_2) = \operatorname{Var}(X_1) + (k+1)\operatorname{Cov}(X_1, X_2) + k\operatorname{Var}(X_2)$。
给定 $\operatorname{Var}(X_1)=4$, $\operatorname{Var}(X_2)=9$, 和 $\operatorname{Cov}(X_1,X_2)=-2$，我们有：
$\operatorname{Cov}(Y_1, Y_2) = 4 + (k+1)(-2) + 9k = 4 - 2k - 2 + 9k = 2 + 7k$。
令协[方差](@entry_id:200758)为零，得到 $2 + 7k = 0$，解出 $k = -2/7$。通过选择这个特定的 $k$ 值，我们就能确保两个性能指标是统计独立的。

#### 条件分布

另一个关键性质是，[多元正态分布](@entry_id:175229)的**条件分布 (conditional distributions)** 也是正态的。给定一个多元正态向量 $\mathbf{X}$ 被划分为两个子向量 $\mathbf{X}_1$ 和 $\mathbf{X}_2$，如果我们观测到 $\mathbf{X}_2$ 的值为 $\mathbf{a}$，那么在这一条件下 $\mathbf{X}_1$ 的[分布](@entry_id:182848)仍然是[多元正态分布](@entry_id:175229)。

形式上，如果 $\mathbf{X} = \begin{pmatrix} \mathbf{X}_1 \\ \mathbf{X}_2 \end{pmatrix} \sim \mathcal{N}_p\left(\begin{pmatrix} \boldsymbol{\mu}_1 \\ \boldsymbol{\mu}_2 \end{pmatrix}, \begin{pmatrix} \boldsymbol{\Sigma}_{11} & \boldsymbol{\Sigma}_{12} \\ \boldsymbol{\Sigma}_{21} & \boldsymbol{\Sigma}_{22} \end{pmatrix}\right)$，则给定 $\mathbf{X}_2 = \mathbf{a}$ 时 $\mathbf{X}_1$ 的[条件分布](@entry_id:138367)为：
$$
\mathbf{X}_1 | (\mathbf{X}_2 = \mathbf{a}) \sim \mathcal{N}(\boldsymbol{\mu}_{1|2}, \boldsymbol{\Sigma}_{1|2})
$$
其中，条件均值和条件协方差矩阵为：
$$
\boldsymbol{\mu}_{1|2} = \boldsymbol{\mu}_1 + \boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}(\mathbf{a} - \boldsymbol{\mu}_2)
$$
$$
\boldsymbol{\Sigma}_{1|2} = \boldsymbol{\Sigma}_{11} - \boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}\boldsymbol{\Sigma}_{21}
$$

这个结果在[贝叶斯推断](@entry_id:146958)和预测中至关重要。条件均值 $\boldsymbol{\mu}_{1|2}$ 可以被看作是对 $\boldsymbol{\mu}_1$ 的一个更新或修正。修正项 $\boldsymbol{\Sigma}_{12}\boldsymbol{\Sigma}_{22}^{-1}(\mathbf{a} - \boldsymbol{\mu}_2)$ 根据观测值 $\mathbf{a}$ 与其期望 $\boldsymbol{\mu}_2$ 的偏差，并结合 $\mathbf{X}_1$ 和 $\mathbf{X}_2$ 之间的协[方差](@entry_id:200758)结构，来调整对 $\mathbf{X}_1$ 的最佳猜测。条件协[方差](@entry_id:200758) $\boldsymbol{\Sigma}_{1|2}$ 则表示在知道了 $\mathbf{X}_2$ 的信息后，$\mathbf{X}_1$ 剩余的不确定性。注意到 $\boldsymbol{\Sigma}_{1|2}$ 不依赖于具体的观测值 $\mathbf{a}$，并且由于减去的项是半正定的，[条件方差](@entry_id:183803)总是小于或等于边际[方差](@entry_id:200758)，这反映了信息增加导致不确定性降低的直觉。

例如，在金融模型中，三支股票的回报率 $\mathbf{X} = (X_1, X_2, X_3)^T$ 服从 $\mathcal{N}_3(\boldsymbol{\mu}, \boldsymbol{\Sigma})$。如果我们观测到第三支股票的回报率 $X_3 = 0.5$，我们可以更新对前两支股票回报率 $(X_1, X_2)^T$ 的预测 [@problem_id:1939195]。利用上述公式，通过划分 $\boldsymbol{\mu}$ 和 $\boldsymbol{\Sigma}$，我们可以精确计算出在 $X_3=0.5$ 条件下，$(X_1, X_2)$ 的新[均值向量](@entry_id:266544)和[协方差矩阵](@entry_id:139155)。

### 相关[分布](@entry_id:182848)与特殊情况

#### 二次型的[分布](@entry_id:182848)

我们之前遇到的[马氏距离](@entry_id:269828)平方，作为一个[随机变量](@entry_id:195330)，其自身也具有明确的[分布](@entry_id:182848)。这是一个非常重要的结论：如果 $\mathbf{X} \sim \mathcal{N}_p(\boldsymbol{\mu}, \boldsymbol{\Sigma})$ 且 $\boldsymbol{\Sigma}$ 是正定的，那么二次型
$$
S = (\mathbf{X}-\boldsymbol{\mu})^T\boldsymbol{\Sigma}^{-1}(\mathbf{X}-\boldsymbol{\mu})
$$
服从自由度为 $p$ 的**[卡方分布](@entry_id:165213) (chi-squared distribution)**，记为 $\chi^2(p)$。

这个结果的推导思路是先对 $\mathbf{X}$ 进行[标准化](@entry_id:637219)。令 $\mathbf{Z} = \boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu})$，其中 $\boldsymbol{\Sigma}^{-1/2}$ 是 $\boldsymbol{\Sigma}^{-1}$ 的对称正定平方根。根据[线性变换](@entry_id:149133)性质，$\mathbf{Z}$ 也是[正态分布](@entry_id:154414)的，其均值为 $\mathbb{E}[\mathbf{Z}] = \boldsymbol{\Sigma}^{-1/2}(\mathbb{E}[\mathbf{X}] - \boldsymbol{\mu}) = \mathbf{0}$，[协方差矩阵](@entry_id:139155)为 $\operatorname{Cov}(\mathbf{Z}) = \boldsymbol{\Sigma}^{-1/2}\operatorname{Cov}(\mathbf{X})\boldsymbol{\Sigma}^{-1/2} = \boldsymbol{\Sigma}^{-1/2}\boldsymbol{\Sigma}\boldsymbol{\Sigma}^{-1/2} = \mathbf{I}_p$。因此，$\mathbf{Z}$ 是一个包含 $p$ 个[相互独立](@entry_id:273670)的标准正态[随机变量](@entry_id:195330)的向量，即 $Z_i \sim \mathcal{N}(0,1)$。
那么，二次型 $S$ 可以被重写为：
$$
S = (\mathbf{X}-\boldsymbol{\mu})^T (\boldsymbol{\Sigma}^{-1/2})^T \boldsymbol{\Sigma}^{-1/2} (\mathbf{X}-\boldsymbol{\mu}) = (\boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu}))^T (\boldsymbol{\Sigma}^{-1/2}(\mathbf{X}-\boldsymbol{\mu})) = \mathbf{Z}^T\mathbf{Z} = \sum_{i=1}^p Z_i^2
$$
根据定义，$p$ 个独立标准正态[随机变量](@entry_id:195330)的平方和服从自由度为 $p$ 的[卡方分布](@entry_id:165213)。

这个结论在统计推断中有广泛应用，例如构建置信椭球和进行假设检验。在自主车辆的传感器数据分析中，这个二次型可以作为一个“异常分数”，如果该分数超过了 $\chi^2(p)$ [分布](@entry_id:182848)某个高分位数（如95%分位数），系统就可以判定出现了异常情况 [@problem_id:1939245]。

#### 退化[多元正态分布](@entry_id:175229)

到目前为止，我们都假设协方差矩阵 $\boldsymbol{\Sigma}$ 是可逆的。但当 $\boldsymbol{\Sigma}$ 是奇异的（即[行列式](@entry_id:142978)为零，$\operatorname{rank}(\boldsymbol{\Sigma}) < p$）时，会发生什么？这种情况对应于**退化[多元正态分布](@entry_id:175229) (degenerate multivariate normal distribution)**。

当 $\boldsymbol{\Sigma}$ 奇异时，随机向量的分量之间存在精确的[线性关系](@entry_id:267880)。因此，整个概率质量并非[分布](@entry_id:182848)在整个 $\mathbb{R}^p$ 空间，而是集中在一个维度低于 $p$ 的仿射[子空间](@entry_id:150286)上（例如，二维空间中的一条直线，三维空间中的一个平面）。因此，它在 $\mathbb{R}^p$ 空间中没有[概率密度函数](@entry_id:140610)。

要找到这个[子空间](@entry_id:150286)，我们可以寻找[协方差矩阵](@entry_id:139155) $\boldsymbol{\Sigma}$ 的零空间 (null space) 中的任意非[零向量](@entry_id:156189) $\mathbf{a}$。对于这样的向量，我们有 $\boldsymbol{\Sigma}\mathbf{a} = \mathbf{0}$。考虑[随机变量](@entry_id:195330) $Y = \mathbf{a}^T\mathbf{X}$，它的[方差](@entry_id:200758)为：
$$
\operatorname{Var}(Y) = \operatorname{Var}(\mathbf{a}^T\mathbf{X}) = \mathbf{a}^T \operatorname{Cov}(\mathbf{X}) \mathbf{a} = \mathbf{a}^T \boldsymbol{\Sigma} \mathbf{a} = \mathbf{a}^T \mathbf{0} = 0
$$
[方差](@entry_id:200758)为零意味着 $Y$ 是一个常数，其值为其期望 $\mathbb{E}[Y] = \mathbf{a}^T\boldsymbol{\mu}$。因此，随机向量 $\mathbf{X}$ 必须以概率1满足线性约束：
$$
\mathbf{a}^T\mathbf{x} = \mathbf{a}^T\boldsymbol{\mu} \quad \text{或等价地} \quad \mathbf{a}^T(\mathbf{x}-\boldsymbol{\mu}) = 0
$$
这个方程定义了 $\mathbf{X}$ 所在的仿射[子空间](@entry_id:150286)。

例如，考虑一个[二元正态分布](@entry_id:165129)，其[协方差矩阵](@entry_id:139155)为 $\boldsymbol{\Sigma} = \begin{pmatrix} 4 & 6 \\ 6 & 9 \end{pmatrix}$ [@problem_id:1939203]。易见其[行列式](@entry_id:142978)为 $4 \times 9 - 6 \times 6 = 0$，所以是退化的。$\boldsymbol{\Sigma}$ 的[零空间](@entry_id:171336)由方程 $4a_1+6a_2=0$（即 $2a_1+3a_2=0$）给出。我们可以选择一个非零解，如 $\mathbf{a} = (3, -2)^T$。那么，如果[均值向量](@entry_id:266544)是 $\boldsymbol{\mu} = (2, -3)^T$，则[分布](@entry_id:182848)的支撑集是一条直线，其方程为：
$$
3(x_1 - 2) - 2(x_2 - (-3)) = 0 \implies 3x_1 - 6 - 2x_2 - 6 = 0 \implies 3x_1 - 2x_2 = 12
$$
所有概率质量都集中在这条直线上。

#### 边际正态不意味着联合正态

最后，必须强调一个常见的误区。虽然[多元正态分布](@entry_id:175229)的任何[边际分布](@entry_id:264862)都是正态的，但反过来不成立。也就是说，即使一组[随机变量](@entry_id:195330)中的每一个都服从[正态分布](@entry_id:154414)，它们的[联合分布](@entry_id:263960)也**不一定**是[多元正态分布](@entry_id:175229)。

我们可以通过一个构造性的例子来说明这一点 [@problem_id:1939267]。令 $X \sim \mathcal{N}(0,1)$。我们定义另一个[随机变量](@entry_id:195330) $Y$ 如下：
$$
Y = \begin{cases} X & \text{if } |X| \le 1 \\ -X & \text{if } |X| > 1 \end{cases}
$$
由于[标准正态分布](@entry_id:184509)的PDF是偶函数（即 $f_X(x) = f_X(-x)$），可以证明 $Y$ 的[边际分布](@entry_id:264862)也是[标准正态分布](@entry_id:184509) $Y \sim \mathcal{N}(0,1)$。然而，$(X, Y)$ 的[联合分布](@entry_id:263960)却不是二元正态的。一个简单的判断方法是，如果它们是联合正态的，那么 $Y$ 必须是 $X$ 的线性函数，即 $Y=aX+b$。但这里的 $Y$ 和 $X$ 的关系显然是[非线性](@entry_id:637147)的。

此外，它们的和 $X+Y$ 也不是正态分布的。当 $|X|>1$ 时，$X+Y=X+(-X)=0$。由于 $P(|X|>1) > 0$，这意味着 $X+Y$ 在0点有一个正的点质量，这与任何[连续分布](@entry_id:264735)（包括正态分布）的性质相矛盾。这个例子有力地提醒我们，在应用[多元正态分布](@entry_id:175229)的强[大性](@entry_id:268856)质（如[独立性与不相关性](@entry_id:268517)等价）之前，必须首先确认**[联合分布](@entry_id:263960)**确实是多元正态的。