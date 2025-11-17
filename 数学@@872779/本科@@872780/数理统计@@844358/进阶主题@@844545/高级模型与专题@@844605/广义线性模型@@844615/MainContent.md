## 引言
在[统计建模](@entry_id:272466)领域，经典线性回归模型是一个强大的工具，但其对数据正态性和恒定[方差](@entry_id:200758)的严格假设在许多现实场景中并不成立。当我们需要分析的数据是二元的（如成功/失败）、计数的（如事件发生次数）或[偏态](@entry_id:178163)的（如索赔金额）时，我们应该如何构建一个既严谨又灵活的模型？这正是广义[线性模型](@entry_id:178302)（Generalized Linear Models, GLMs）所要解决的核心问题。GLMs 提供了一个统一而强大的框架，极大地扩展了[线性建模](@entry_id:171589)的边界，使其成为现代数据分析中不可或缺的基石。

本文将系统地引导您深入理解广义线性模型的世界。在接下来的内容中，我们将分三步展开：
*   **原理与机制**：我们将首先剖析构成 GLM 的三大核心组件——随机成分、系统成分和[连接函数](@entry_id:636388)，并深入其理论基础指数散布族，以及参数估计和模型评估的关键方法。
*   **应用与跨学科联系**：接着，我们将跨越[流行病学](@entry_id:141409)、[基因组学](@entry_id:138123)到生态学等多个领域，通过丰富的实例展示逻辑回归、泊松回归等模型如何在实践中解决真实世界的问题。
*   **动手实践**：最后，您将有机会通过一系列精心设计的问题，将理论知识应用于具体的数据分析挑战中，巩固和深化您的理解。

让我们从第一部分开始，深入探索广义[线性模型](@entry_id:178302)的内在原理与机制。

## 原理与机制

在上一章中，我们介绍了广义线性模型 (Generalized Linear Models, GLMs) 作为对传统线性回归模型的扩展，它极大地拓宽了[统计建模](@entry_id:272466)的应用范围。本章将深入探讨构成 GLM 的核心原理与机制。我们将从其基本结构入手，剖析其三大核心组件，并详细阐述其理论基础——指数散布族。随后，我们将探讨模型参数的估计方法，以及评估[模型拟合](@entry_id:265652)度的关键指标。

### 广义线性模型的构成

经典线性回归模型建立在一系列严格的假设之上，包括响应变量服从正态分布、[方差](@entry_id:200758)恒定，且其[期望值](@entry_id:153208)与预测变量之间存在线性关系。然而，在许多实际应用中，这些假设往往难以满足。例如，当我们研究每年保险索赔的次数、特定区域内某种疾病的发病数，或一项实验的成功与否时，响应变量显然不是连续且无界的[正态分布](@entry_id:154414)。广义[线性模型](@entry_id:178302)通过引入更灵活的框架，系统地解决了这些挑战。一个 GLM 由三个关键部分定义：

1.  **随机成分 (Random Component)**：指定响应变量 $Y$ 的[概率分布](@entry_id:146404)。与经典线性模型强制要求[正态分布](@entry_id:154414)不同，GLM 允许 $Y$ 服从任何属于**指数散布族**的[分布](@entry_id:182848)。这包括了正态分布、泊松分布、二项分布、伽马[分布](@entry_id:182848)和逆高斯分布等，从而能够自然地处理计数数据、比例数据以及[偏态分布](@entry_id:175811)的连续数据。

2.  **系统成分 (Systematic Component)**：这是一个[线性预测](@entry_id:180569)器 $\eta$ (eta)，由解释变量的[线性组合](@entry_id:154743)构成。对于第 $i$ 个观测，其形式为：
    $$ \eta_i = \mathbf{x}_i^T \boldsymbol{\beta} = \beta_0 + \beta_1 x_{i1} + \dots + \beta_p x_{ip} $$
    其中 $\mathbf{x}_i$ 是第 $i$ 个观测的解释变量向量，$\boldsymbol{\beta}$ 是待估计的模型参数向量。这部分保留了[线性模型](@entry_id:178302)的核心思想，即可加性和线性关系，但作用对象不再是响应变量的[期望值](@entry_id:153208)本身。

3.  **[连接函数](@entry_id:636388) (Link Function)**：这是一个可微的单调函数 $g$，它将随机成分的[期望值](@entry_id:153208) $\mu_i = E[Y_i]$ 与系统成分（[线性预测](@entry_id:180569)器）$\eta_i$ 联系起来。其关系式为：
    $$ g(\mu_i) = \eta_i $$
    [连接函数](@entry_id:636388)的引入是 GLM 的一项核心创新。它允许模型的线性部分 ($\eta_i$) 的取值范围（通常是 $(-\infty, \infty)$）与响应变量[期望值](@entry_id:153208) $\mu_i$ 的取值范围（例如，对于计数数据 $\mu_i > 0$）不一致。

为了具体理解这三个组件如何协同工作，我们考虑一个保险公司的分析场景 [@problem_id:1919872]。假设一个数据科学家希望研究驾驶员年龄 ($x$) 与其每年提交的保险索赔次数 ($Y$) 之间的关系。这里的响应变量 $Y$ 是一个非负整数（计数）。一个合适的 GLM 构建如下：

*   **随机成分**：由于 $Y$ 是计数数据，选择**[泊松分布](@entry_id:147769)**是自然的选择，即 $Y \sim \text{Poisson}(\mu)$。
*   **系统成分**：[线性预测](@entry_id:180569)器被设定为 $\eta = \beta_0 + \beta_1 x$。
*   **[连接函数](@entry_id:636388)**：为了确保期望索赔数 $\mu = E[Y]$ 始终为正，我们不能直接令 $\mu = \eta$。一个常用的选择是**[对数连接函数](@entry_id:163146) (log link)**，即 $g(\mu) = \ln(\mu)$。这样，模型就变为 $\ln(\mu) = \beta_0 + \beta_1 x$。

通过这种设定，即使[线性预测](@entry_id:180569)器 $\eta$ 取任何实数值，期望索赔数 $\mu = \exp(\eta) = \exp(\beta_0 + \beta_1 x)$ 也将永远是正数，这与响应变量的内在属性完全吻合。

反过来，为了从计算出的[线性预测](@entry_id:180569)器 $\eta_i$ 得到对应的[期望值](@entry_id:153208) $\mu_i$，我们需要使用[连接函数](@entry_id:636388)的逆函数 $g^{-1}$ [@problem_id:1919829]。这个**逆[连接函数](@entry_id:636388) (inverse link function)** 的作用是将[线性预测](@entry_id:180569)器的值映射回响应变量的[期望值](@entry_id:153208)尺度上：
$$ \mu_i = g^{-1}(\eta_i) $$
在上述保险索赔的例子中，逆[连接函数](@entry_id:636388)是[指数函数](@entry_id:161417)，$\mu_i = \exp(\eta_i)$。因此，逆[连接函数](@entry_id:636388)在模型解释和预测中扮演着至关重要的角色，它将模型的线性结构转换回我们感兴趣的、具有实际意义的响应均值。

### 指数散布族：随机成分的基石

GLM 的广泛适用性在很大程度上归功于其随机成分可以源自一个庞大的[概率分布](@entry_id:146404)家族——**指数散布族 (Exponential Dispersion Family)**。一个[分布](@entry_id:182848)若属于该族，其[概率密度函数](@entry_id:140610) (PDF) 或[概率质量函数](@entry_id:265484) (PMF) 可以写成如下的**正则形式 (canonical form)**：

$$ f(y; \theta, \phi) = \exp\left(\frac{y\theta - b(\theta)}{\phi} + c(y, \phi)\right) $$

这里的各个组成部分具有明确的统计意义：
*   $y$ 是观测值。
*   $\theta$ 是**自然参数 (natural parameter)** 或**典范参数 (canonical parameter)**，它直接与[分布](@entry_id:182848)的均值相关。
*   $\phi$ 是**散布参数 (dispersion parameter)**，它与[分布](@entry_id:182848)的[方差](@entry_id:200758)有关。对于某些[分布](@entry_id:182848)（如[泊松分布](@entry_id:147769)和二项分布），$\phi$ 是一个已知的常数（通常为 1）。
*   $b(\theta)$ 是**[累积量生成函数](@entry_id:748109) (cumulant function)**，它完全由 $\theta$ 决定。这个函数极为重要，因为它的各阶导数可以生成[分布](@entry_id:182848)的[累积量](@entry_id:152982)（如均值和[方差](@entry_id:200758)）。
*   $c(y, \phi)$ 是一个归一化项，确保函数积分为 1。

为了更好地理解这个抽象的定义，让我们通过实例来展示如何将常见[分布](@entry_id:182848)转换为正则形式。

**示例 1：[伯努利分布](@entry_id:266933)** [@problem_id:1919842]
一个伯努利[随机变量](@entry_id:195330) $Y \in \{0, 1\}$，其成功概率为 $p$，其 PMF 为 $P(Y=y) = p^y(1-p)^{1-y}$。我们可以通过对数和指数运算将其改写：
$$
\begin{align}
p^y (1-p)^{1-y}  = \exp\left( \ln(p^y (1-p)^{1-y}) \right) \\
 = \exp\left( y\ln(p) + (1-y)\ln(1-p) \right) \\
 = \exp\left( y\ln(p) - y\ln(1-p) + \ln(1-p) \right) \\
 = \exp\left( y \ln\left(\frac{p}{1-p}\right) - \left[-\ln(1-p)\right] \right)
\end{align}
$$
令 $\theta = \ln\left(\frac{p}{1-p}\right)$，这是我们熟悉的 logit 函数。从这个关系可以反解出 $p = \frac{\exp(\theta)}{1+\exp(\theta)}$。将其代入 $-\ln(1-p)$ 中，得到：
$$ -\ln(1-p) = -\ln\left(1 - \frac{\exp(\theta)}{1+\exp(\theta)}\right) = -\ln\left(\frac{1}{1+\exp(\theta)}\right) = \ln(1+\exp(\theta)) $$
因此，[伯努利分布](@entry_id:266933)的 PMF 可以写为：
$$ f(y; \theta) = \exp\left( y\theta - \ln(1+\exp(\theta)) \right) $$
与正则形式对比，我们发现对于[伯努利分布](@entry_id:266933)：
*   自然参数 $\theta = \ln\left(\frac{p}{1-p}\right)$。
*   [累积量生成函数](@entry_id:748109) $b(\theta) = \ln(1+\exp(\theta))$。
*   散布参数 $\phi=1$，且 $c(y, \phi)=0$。

指数散布族的优美之处在于其[累积量生成函数](@entry_id:748109) $b(\theta)$ 的性质。可以证明，对于服从该族的任何[分布](@entry_id:182848)，其均值和[方差](@entry_id:200758)与 $b(\theta)$ 的导数直接相关：

1.  **均值**: $E(Y) = \mu = b'(\theta)$
2.  **[方差](@entry_id:200758)**: $\text{Var}(Y) = \phi \cdot b''(\theta)$

让我们以泊松分布为例来验证第一个性质 [@problem_id:1919861]。[泊松分布](@entry_id:147769)的 PMF 为 $P(Y=y) = \frac{\lambda^y \exp(-\lambda)}{y!}$。将其改写为正则形式：
$$ P(Y=y) = \frac{1}{y!} \exp(y \ln(\lambda) - \lambda) $$
对比正则形式，我们得到：
*   $\theta = \ln(\lambda)$
*   $b(\theta) = \lambda$
*   $\phi = 1$ 和 $h(y) = 1/y!$ (这里使用了 $h(y)\exp(...)$ 的形式，等价于 $c(y, \phi)=-\ln(y!)$)

为了计算 $b'(\theta)$，我们首先需要将 $b(\theta)$ 表示为 $\theta$ 的函数。由 $\theta = \ln(\lambda)$ 可知 $\lambda = \exp(\theta)$。因此，$b(\theta) = \exp(\theta)$。对其求导：
$$ b'(\theta) = \frac{d}{d\theta}\exp(\theta) = \exp(\theta) $$
因为 $\lambda = \exp(\theta)$，所以 $b'(\theta) = \lambda$。这恰好是泊松分布的[期望值](@entry_id:153208) $E[Y]$。这个结果具有普遍性，是 GLM 理论的基石。

[方差的性质](@entry_id:185416)同样重要。[方差](@entry_id:200758)函数 $V(\mu) = b''(\theta)$ 描述了[方差](@entry_id:200758)如何随均值的变化而变化，这是区分不同[分布](@entry_id:182848)的关键特征。例如，对于[泊松分布](@entry_id:147769)，$b''(\theta) = \frac{d}{d\theta}\exp(\theta) = \exp(\theta) = \lambda = \mu$，因此其[方差](@entry_id:200758)函数为 $V(\mu) = \mu$，这与我们熟知的泊松分布“均值等于[方差](@entry_id:200758)”的特性一致（在 $\phi=1$ 的情况下）。

散布参数 $\phi$ 的作用是缩放[方差](@entry_id:200758) [@problem_id:1919873]。
*   对于[泊松分布](@entry_id:147769)和[二项分布](@entry_id:141181)，理论上 $\phi=1$。在实际数据分析中，如果估计出的 $\phi$ 显著大于 1，则表明数据存在**过度散布 (overdispersion)**，即数据的实际[方差](@entry_id:200758)大于理论模型所假设的[方差](@entry_id:200758)。
*   对于[正态分布](@entry_id:154414) $N(\mu, \sigma^2)$，其[方差](@entry_id:200758)函数 $V(\mu)=1$ 是一个常数，而散布参数 $\phi = \sigma^2$。这表明，在 GLM 的框架下，经典[线性模型](@entry_id:178302)可以被看作是随机成分为[正态分布](@entry_id:154414)、[连接函数](@entry_id:636388)为[恒等函数](@entry_id:152136) ($g(\mu)=\mu$) 且[方差](@entry_id:200758)函数为常数的特例 [@problem_id:1919873]。

通过一个具体的计算示例，我们可以看到 $b(\theta)$ 如何决定[方差](@entry_id:200758)结构 [@problem_id:1919825]。假设一个模型的 $b(\theta) = -\frac{1}{2}\ln(1-2\theta)$。其一阶和[二阶导数](@entry_id:144508)分别为：
$$ b'(\theta) = \frac{1}{1-2\theta} $$
$$ b''(\theta) = \frac{2}{(1-2\theta)^2} $$
因此，该模型的[方差](@entry_id:200758)为 $\text{Var}(Y) = \phi \cdot b''(\theta) = \frac{2\phi}{(1-2\theta)^2}$。

### 正则连接与非正则[连接函数](@entry_id:636388)

[连接函数](@entry_id:636388)的选择对模型有重要影响。在所有可能的[连接函数](@entry_id:636388)中，有一类特别重要，称为**正则[连接函数](@entry_id:636388) (canonical link function)**。当一个模型的[连接函数](@entry_id:636388)使得自然参数 $\theta$ 等于[线性预测](@entry_id:180569)器 $\eta$ 时，即 $\theta = \eta$，该[连接函数](@entry_id:636388)就是正则连接。

*   对于**[伯努利分布](@entry_id:266933)**，$\theta = \ln(p/(1-p))$，因此其正则连接是**logit 函数**。
*   对于**[泊松分布](@entry_id:147769)**，$\theta = \ln(\lambda)$，因此其正则连接是**对数函数 (log link)**。
*   对于**伽马[分布](@entry_id:182848)**，$\theta = -1/\mu$，因此其正则连接是**倒数函数 (inverse link)**。

使用正则[连接函数](@entry_id:636388)在数学上特别方便，因为它能极大地简化参数估计算法中的数学表达式。然而，在实践中，我们也可以选择**非正则[连接函数](@entry_id:636388) (non-canonical link)**。选择非正则连接通常是出于对模型解释性的考虑。例如，对于服从伽马[分布](@entry_id:182848)的响应变量（如保险索赔金额），虽然其正则连接是倒数函数，但分析师们常常使用对数连接 ($\ln(\mu) = \eta$) [@problem_id:1919879]。这是因为对数连接模型 ($\mu = \exp(\mathbf{x}^T \boldsymbol{\beta})$) 意味着协变量对均值有乘性效应，这种解释方式通常比倒数连接下的可加效应（在 $1/\mu$ 尺度上）更为直观。选择不同的[连接函数](@entry_id:636388)会影响到模型拟合算法的细节，我们将在下一节看到这一点。

### [参数估计](@entry_id:139349)：最大似然与[迭代重加权最小二乘法](@entry_id:175255)

与大多数现代统计模型一样，GLM 的参数 $\boldsymbol{\beta}$ 是通过**[最大似然估计](@entry_id:142509) (Maximum Likelihood Estimation, MLE)** 来确定的。其基本思想是找到一组参数 $\hat{\boldsymbol{\beta}}$，使得观测到当前数据集的概率（即似然函数）最大化。

对于 $n$ 个独立观测 $y_1, \dots, y_n$，总的[对数似然函数](@entry_id:168593)是各项[对数似然](@entry_id:273783)之和：
$$ l(\boldsymbol{\beta}; \mathbf{y}) = \sum_{i=1}^n l_i(\boldsymbol{\beta}; y_i) = \sum_{i=1}^n \left( \frac{y_i\theta_i - b(\theta_i)}{\phi} + c(y_i, \phi) \right) $$
为了最大化 $l(\boldsymbol{\beta}; \mathbf{y})$，我们需求其关于每个参数 $\beta_j$ 的[偏导数](@entry_id:146280)，并令其为零。这些[偏导数](@entry_id:146280)构成了**得分向量 (score vector)** $\mathbf{U}(\boldsymbol{\beta}) = \nabla_{\boldsymbol{\beta}} l(\boldsymbol{\beta}; \mathbf{y})$。通过应用链式法则，可以推导出得分向量的一般表达式 [@problem_id:1919869]。
$$ \frac{\partial l_i}{\partial \beta_j} = \frac{\partial l_i}{\partial \theta_i} \frac{d\theta_i}{d\mu_i} \frac{d\mu_i}{d\eta_i} \frac{\partial \eta_i}{\partial \beta_j} $$
将各部分代入（例如，$\frac{\partial l_i}{\partial \theta_i} = \frac{y_i-\mu_i}{\phi}$，$\frac{d\mu_i}{d\theta_i} = b''(\theta_i) = V(\mu_i)$，$\frac{\partial \eta_i}{\partial \beta_j} = x_{ij}$），经过整理，整个得分向量可以写成非常紧凑的矩阵形式：
$$ \mathbf{U}(\boldsymbol{\beta}) = \mathbf{X}^{T}\mathbf{\Delta}\mathbf{V}_{\text{var}}^{-1}(\mathbf{y}-\boldsymbol{\mu}) $$
其中：
*   $\mathbf{X}$ 是 $n \times p$ 的[设计矩阵](@entry_id:165826)。
*   $\mathbf{y}$ 和 $\boldsymbol{\mu}$ 分别是观测值和[期望值](@entry_id:153208)的 $n \times 1$ 向量。
*   $\mathbf{V}_{\text{var}}$ 是一个 $n \times n$ 的[对角矩阵](@entry_id:637782)，其对角线元素为 $\text{Var}(Y_i) = \phi V(\mu_i)$。
*   $\mathbf{\Delta}$ 是一个 $n \times n$ 的对角矩阵，其对角线元素为 $\frac{d\mu_i}{d\eta_i}$。

将得分向量设为零 $\mathbf{U}(\boldsymbol{\beta}) = \mathbf{0}$ 就得到了一组**[似然方程](@entry_id:164995)**。除了极少数特殊情况（如正态线性模型），这组方程通常是[非线性](@entry_id:637147)的，无法求得解析解。因此，必须使用[数值优化](@entry_id:138060)算法进行求解。

在 GLM 中，最常用的算法是 **Fisher scoring**，它在形式上等价于一个被称为**[迭代重加权最小二乘法](@entry_id:175255) (Iteratively Reweighted Least Squares, IRLS)** 的过程。IRLS 的核心思想是将复杂的[非线性优化](@entry_id:143978)问题转化为一系列加权[最小二乘回归](@entry_id:262382)问题来迭代求解 [@problem_id:1919865]。

在 IRLS 的每次迭代中，算法会构造一个临时的“响应”变量，称为**工作响应 (working response)** 或调整因变量 $z_i$，其定义为：
$$ z_i = \eta_i^{(t)} + (y_i - \mu_i^{(t)}) g'(\mu_i^{(t)}) $$
其中上标 $(t)$ 表示当前迭代的估计值，$g'(\mu)$ 是[连接函数](@entry_id:636388)的一阶导数。这个 $z_i$ 可以被看作是基于当前模型估计，对[线性预测](@entry_id:180569)器 $\eta_i$ 的一个线性化近似。它将观测残差 $(y_i - \mu_i^{(t)})$ 通过 $g'(\mu_i^{(t)})$ 投影到[线性预测](@entry_id:180569)器的尺度上，并加到当前的 $\eta_i^{(t)}$ 上作为修正。

同时，算法会为每个观测计算一个**权重 (weight)** $w_i$：
$$ w_i = \frac{1}{\text{Var}(Y_i)} \left( \frac{d\mu_i}{d\eta_i} \right)^2 = \frac{1}{\phi V(\mu_i) [g'(\mu_i)]^2} $$
这个权重反映了每个观测在其当前估计值附近的[信息量](@entry_id:272315)。[方差](@entry_id:200758)越小、或者[连接函数](@entry_id:636388)在该点附近越陡峭（即 $\mu_i$ 对 $\eta_i$ 的变化越敏感），该观测获得的权重就越大。

有了工作响应 $z_i$ 和权重 $w_i$ 之后，下一次迭代的参数估计 $\boldsymbol{\beta}^{(t+1)}$ 就是通过求解一个**加权最小二乘 (Weighted Least Squares, WLS)** 问题得到的：即找到 $\boldsymbol{\beta}$ 来最小化 $\sum_{i=1}^n w_i (z_i - \mathbf{x}_i^T \boldsymbol{\beta})^2$。

这个过程不断重复——计算 $\boldsymbol{\eta}^{(t)}, \boldsymbol{\mu}^{(t)}$，更新工作响应 $\mathbf{z}^{(t)}$ 和权重 $\mathbf{W}^{(t)}$，然后求解 WLS 问题得到 $\boldsymbol{\beta}^{(t+1)}$——直到参数估计值收敛。

值得一提的是，当使用**正则[连接函数](@entry_id:636388)**时，$\frac{d\mu_i}{d\eta_i} = V(\mu_i)$，这使得权重公式简化为 $w_i = V(\mu_i) / \phi$ (在 $\phi=1$ 时，$w_i=V(\mu_i)$)，并且得分方程也简化为 $\mathbf{X}^T(\mathbf{y}-\boldsymbol{\mu}) = \mathbf{0}$。这种简化是正则连接在计算上具有吸[引力](@entry_id:175476)的根本原因 [@problem_id:1919879]。

### [拟合优度](@entry_id:637026)评估：偏差

在拟合了一个 GLM 之后，我们需要评估它对数据的拟合程度。在经典线性回归中，我们使用[残差平方和](@entry_id:174395) (RSS) 来度量模型的[拟合优度](@entry_id:637026)。在 GLM 中，一个类似但更具普适性的概念是**偏差 (Deviance)**。

偏差的核心思想是比较我们当前拟合的模型与一个“完美”模型之间的差距。这个完美的模型被称为**[饱和模型](@entry_id:150782) (saturated model)** [@problem_id:1919828]。[饱和模型](@entry_id:150782)为每个观测点都分配了一个独立的参数，因此它能够完美地拟合数据，即对每个观测 $i$，其拟合值 $\hat{\mu}_i$ 都恰好等于观测值 $y_i$。[饱和模型](@entry_id:150782)代表了任何模型所能达到的拟合上限。

**偏差**被定义为拟合模型的[对数似然](@entry_id:273783)与[饱和模型](@entry_id:150782)的[对数似然](@entry_id:273783)之差的特定倍数：
$$ D(\mathbf{y}, \hat{\boldsymbol{\mu}}) = 2\phi \left( \ell(\mathbf{y}; \mathbf{y}) - \ell(\hat{\boldsymbol{\mu}}; \mathbf{y}) \right) $$
其中 $\ell(\hat{\boldsymbol{\mu}}; \mathbf{y})$ 是我们拟合模型的最大对数似然值，而 $\ell(\mathbf{y}; \mathbf{y})$ 是[饱和模型](@entry_id:150782)的最大[对数似然](@entry_id:273783)值。对于许多常见的 GLM（如泊松和[二项模型](@entry_id:275034)，其中 $\phi=1$），公式简化为 $D = 2(\ell_{\text{sat}} - \ell_{\text{fit}})$ [@problem_id:1919828]。一个模型的偏差值越小，说明它与[饱和模型](@entry_id:150782)的差距越小，即模型对数据的拟合越好。

例如，如果一个环境科学家的泊松[回归模型](@entry_id:163386)拟合后的最大[对数似然](@entry_id:273783)为 $-127.8$，而该数据集的[饱和模型](@entry_id:150782)的最大[对数似然](@entry_id:273783)为 $-109.3$，那么该模型的偏差就是 $D = 2 \times (-109.3 - (-127.8)) = 2 \times 18.5 = 37.0$。

与偏差相关的一个重要概念是**零偏差 (null deviance)** [@problem_id:1919876]。它特指**[零模型](@entry_id:181842) (null model)** 的偏差。[零模型](@entry_id:181842)是最简单的模型，只包含一个截距项，即假设所有观测的均值都相同 ($\mu_i = \mu$)。零偏差代表了仅用一个全局平均值来预测所有数据点所产生的“总误差”，在概念上类似于[线性回归](@entry_id:142318)中的总平方和 (Total Sum of Squares)。

例如，对于一组泊松观测数据 $y = (5, 7, 6, 10, 12)$，零模型的拟合值是所有观测的样本均值，即 $\hat{\mu} = (5+7+6+10+12)/5 = 8$。该模型的偏差（即零偏差）可以根据泊松偏差的特定公式计算：
$$ D(\mathbf{y}, \hat{\boldsymbol{\mu}}) = 2 \sum_{i=1}^{n} \left[ y_i \ln\left(\frac{y_i}{\hat{\mu}_i}\right) - (y_i - \hat{\mu}_i) \right] $$
在这个例子中，由于 $\sum (y_i - \hat{\mu}_i) = 0$，公式简化为 $2 \sum y_i \ln(y_i/\hat{\mu}_i)$，计算结果约为 $4.172$ [@problem_id:1919876]。

偏差不仅是衡量单个模型拟合度的指标，它在比较[嵌套模型](@entry_id:635829)时也极为有用。两个[嵌套模型](@entry_id:635829)偏差的差异近似服从[卡方分布](@entry_id:165213)，这为进行[似然比检验](@entry_id:268070)、评估新加入的预测变量是否显著改善[模型拟合](@entry_id:265652)提供了理论依据。