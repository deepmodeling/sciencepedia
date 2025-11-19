## 引言
在自适应信号处理与[系统辨识](@entry_id:201290)领域，递归最小二乘（Recursive Least Squares, RLS）算法是一种以其卓越收敛性能而闻名的强大工具。与广泛使用的最小均方（LMS）算法相比，RLS能够在处理具有相关性（有色）的输入信号时，提供显著更快的[收敛速度](@entry_id:636873)，使其成为许多高性能应用的首选。然而，这种性能的提升伴随着更高的计算复杂度和对算法内部机制更深刻的理解要求。本文旨在全面剖析RLS[自适应滤波](@entry_id:185698)，解决从基础理论到实际应用中可能出现的各种问题。

本文将引导您完成一次对RLS的系统性学习之旅。在“原理与机制”一章中，我们将从加权[最小二乘估计](@entry_id:262764)的基础出发，一步步推导出RLS的核心递归方程，并深入探讨其收敛性、稳定性条件以及与[卡尔曼滤波器](@entry_id:145240)的内在联系，揭示其背后的数学精髓。接着，在“应用与跨学科联系”一章中，我们将展示RLS在[系统辨识](@entry_id:201290)、[自适应控制](@entry_id:262887)以及声学回声消除等多个领域的实际应用，并讨论为克服现实挑战而设计的多种实用变体。最后，“动手实践”部分将通过精心设计的练习，帮助您巩固理论知识，并将抽象的算法付诸于实践。通过本次学习，您将不仅掌握[RLS算法](@entry_id:180846)的实现，更能深刻理解其在现代[估计理论](@entry_id:268624)中的地位和价值。

## 原理与机制

本章深入探讨递归最小二乘 (RLS) [自适应滤波](@entry_id:185698)器的核心原理与工作机制。我们将从加权[最小二乘估计](@entry_id:262764)的基本原则出发，推导出 RLS 算法的核心[递推公式](@entry_id:149465)。随后，我们将探讨算法收敛与稳定性的关键条件，并揭示其与[卡尔曼滤波器](@entry_id:145240)之间深刻的内在联系。最后，我们将讨论在实际应用中遇到的挑战，如模型误差导致的偏置和有限精度运算带来的数值稳定性问题，并介绍相应的先进解决方案。

### 加权最小二乘原则

[自适应滤波](@entry_id:185698)的核心任务是根据一系列观测数据，在线地调整一组滤波器参数，以最小化某个代价函数。对于 RLS 算法，该[代价函数](@entry_id:138681)是**加权最小二乘 (Weighted Least Squares, WLS)**误差。

假设一个[线性模型](@entry_id:178302)，在时刻 $k$ 其输出 $y_k$ 与回归向量 $\boldsymbol{x}_k \in \mathbb{R}^p$ 以及未知参数向量 $\boldsymbol{\theta} \in \mathbb{R}^p$ 之间的关系为 $y_k = \boldsymbol{x}_k^\top \boldsymbol{\theta} + v_k$，其中 $v_k$ 是噪声或模型误差。在收集了 $N$ 组数据 $\{(\boldsymbol{x}_k, y_k)\}_{k=1}^N$ 后，我们的目标是找到一个参数估计值 $\hat{\boldsymbol{\theta}}$，以最小化所有历史预测误差的加权平方和。该[代价函数](@entry_id:138681) $J(\boldsymbol{\theta})$ 定义为：

$J(\boldsymbol{\theta}) = \sum_{k=1}^N w_k (y_k - \boldsymbol{x}_k^\top \boldsymbol{\theta})^2 = (\boldsymbol{y} - \boldsymbol{X}\boldsymbol{\theta})^\top \boldsymbol{W} (\boldsymbol{y} - \boldsymbol{X}\boldsymbol{\theta})$

其中，$\boldsymbol{y} = [y_1, \dots, y_N]^\top$ 是观测输出向量，$\boldsymbol{X}$ 是一个 $N \times p$ 的矩阵，其第 $k$ 行为 $\boldsymbol{x}_k^\top$，而 $\boldsymbol{W}$ 是一个 $N \times N$ 的对角加权矩阵，其对角元素为 $w_k > 0$。

为了求得最小化 $J(\boldsymbol{\theta})$ 的 $\hat{\boldsymbol{\theta}}$，我们计算 $J(\boldsymbol{\theta})$ 关于 $\boldsymbol{\theta}$ 的梯度并令其为零。代价函数展开为：

$J(\boldsymbol{\theta}) = \boldsymbol{y}^\top\boldsymbol{W}\boldsymbol{y} - 2\boldsymbol{\theta}^\top\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{y} + \boldsymbol{\theta}^\top(\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{X})\boldsymbol{\theta}$

其梯度为：

$\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) = -2\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{y} + 2(\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{X})\boldsymbol{\theta}$

令梯度为零，我们得到**[正规方程](@entry_id:142238) (normal equations)**：

$(\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{X})\hat{\boldsymbol{\theta}}_{WLS} = \boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{y}$

如果矩阵 $\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{X}$ 可逆，则加权[最小二乘估计量](@entry_id:204276)有唯一的[闭式](@entry_id:271343)解 [@problem_id:2899730]：

$\hat{\boldsymbol{\theta}}_{WLS} = (\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{X})^{-1} (\boldsymbol{X}^\top\boldsymbol{W}\boldsymbol{y})$

在[自适应滤波](@entry_id:185698)的场景中，我们通常更关心最近的数据，因为它们更能反映系统当前的状态，尤其是在[时变系统](@entry_id:175653)中。这通过**指数加权 (exponential weighting)** 得以实现。具体而言，在时刻 $N$，赋予第 $k$ 个数据点的权重为 $w_k = \lambda^{N-k}$，其中 $\lambda \in (0, 1]$ 被称为**[遗忘因子](@entry_id:175644) (forgetting factor)**。当 $\lambda  1$ 时，历史越久远的数据 ($k$ 越小)，其权重 $\lambda^{N-k}$ 就越小，实现了对旧数据的“遗忘”。当 $\lambda = 1$ 时，所有权重均为 1，加权最小二乘退化为标准的普通最小二乘 (Ordinary Least Squares, OLS)。

在这种指数加权下，WLS 解可以写成求和形式：

$\hat{\boldsymbol{\theta}}_N = \left( \sum_{k=1}^{N} \lambda^{N-k} \boldsymbol{x}_k \boldsymbol{x}_k^\top \right)^{-1} \left( \sum_{k=1}^{N} \lambda^{N-k} y_k \boldsymbol{x}_k \right)$

[遗忘因子](@entry_id:175644) $\lambda$ 的选择是一个关键的设计权衡 [@problem_id:2899670]。$\lambda$ 的值越接近 1，算法的“记忆”就越长，对历史数据的平均效果越好，从而使得参数估计的[方差](@entry_id:200758)更小，对噪声更不敏感。然而，长记忆也意味着算法对系统参数的真实变化反应迟钝。反之，一个较小的 $\lambda$ (例如 0.95) 会赋予近期数据更大的权重，缩短算法的有效记忆长度（近似为 $1/(1-\lambda)$ 个样本），从而提高对系统变化的**跟踪能力 (tracking capability)**，但代价是估计结果对[测量噪声](@entry_id:275238)更为敏感，导致更大的估计[方差](@entry_id:200758)。当 $\lambda=1$ 时，算法拥有无限记忆，适用于参数恒定的系统。

### 递归机制：[RLS算法](@entry_id:180846)的推导

尽管上述闭式解在理论上很完美，但它在计算上是低效的。每当有新的数据点到来时，都需要重新计算包含所有历史数据的大型矩阵的乘法和求逆。RLS 算法的精妙之处在于，它提供了一种高效的递归方法，仅利用前一时刻的计算结果和当前的新数据，就能更新[参数估计](@entry_id:139349)。

我们定义在时刻 $k$ 的加权自[相关矩阵](@entry_id:262631)（或称[信息矩阵](@entry_id:750640)）$\boldsymbol{R}_k$ 和加权[互相关](@entry_id:143353)向量 $\boldsymbol{r}_k$：

$\boldsymbol{R}_k \triangleq \sum_{i=1}^{k} \lambda^{k-i} \boldsymbol{x}_i \boldsymbol{x}_i^\top$

$\boldsymbol{r}_k \triangleq \sum_{i=1}^{k} \lambda^{k-i} y_i \boldsymbol{x}_i$

于是，$\hat{\boldsymbol{\theta}}_k = \boldsymbol{R}_k^{-1} \boldsymbol{r}_k$。通过观察它们的定义，可以发现 $\boldsymbol{R}_k$ 和 $\boldsymbol{r}_k$ 自身也满足简单的递归关系：

$\boldsymbol{R}_k = \lambda \boldsymbol{R}_{k-1} + \boldsymbol{x}_k \boldsymbol{x}_k^\top$

$\boldsymbol{r}_k = \lambda \boldsymbol{r}_{k-1} + y_k \boldsymbol{x}_k$

一种直接的递归策略是：在每一步，根据上述公式更新 $\boldsymbol{R}_k$ 和 $\boldsymbol{r}_k$，然后通过求解线性方程组 $\boldsymbol{R}_k \hat{\boldsymbol{\theta}}_k = \boldsymbol{r}_k$ 来得到 $\hat{\boldsymbol{\theta}}_k$ [@problem_id:2899718]。然而，这个方法的主要瓶颈在于求解该[线性方程组](@entry_id:148943)，特别是如果通过显式计算矩阵逆 $\boldsymbol{R}_k^{-1}$，其计算复杂度为 $\mathcal{O}(p^3)$，其中 $p$ 是参数数量。这对于实时应用来说通常是不可接受的。

RLS 算法通过直接递推 $\boldsymbol{P}_k \triangleq \boldsymbol{R}_k^{-1}$ 来规避了矩阵求逆的巨大计算量。这里的关键工具是**[矩阵求逆](@entry_id:636005)引理 (Matrix Inversion Lemma)**，也称为 Woodbury 恒等式。对于 $\boldsymbol{R}_k = \lambda \boldsymbol{R}_{k-1} + \boldsymbol{x}_k \boldsymbol{x}_k^\top$ 这种“矩阵 + 秩-1 更新”的形式，引理提供了一个高效计算其逆的方法。

具体地，我们将 $\boldsymbol{R}_k$ 的递推关系与[矩阵求逆](@entry_id:636005)引理的一般形式 $\left(\boldsymbol{A} + \boldsymbol{U}\boldsymbol{C}\boldsymbol{V}\right)^{-1}$ 进行匹配 [@problem_id:2899694]。通过选择 $\boldsymbol{A} = \lambda \boldsymbol{R}_{k-1}$, $\boldsymbol{U} = \boldsymbol{x}_k$, $\boldsymbol{C}=1$, 以及 $\boldsymbol{V} = \boldsymbol{x}_k^\top$，我们可以推导出 $\boldsymbol{P}_k$ 的[递推公式](@entry_id:149465)：

$\boldsymbol{P}_k = \frac{1}{\lambda} \left( \boldsymbol{P}_{k-1} - \frac{\boldsymbol{P}_{k-1} \boldsymbol{x}_k \boldsymbol{x}_k^\top \boldsymbol{P}_{k-1}}{\lambda + \boldsymbol{x}_k^\top \boldsymbol{P}_{k-1} \boldsymbol{x}_k} \right)$

利用这个 $\boldsymbol{P}_k$ 的更新，并结合 $\boldsymbol{r}_k$ 的递推，经过一系列代数推导，可以得到 $\hat{\boldsymbol{\theta}}_k$ 的最终更新法则：

$\hat{\boldsymbol{\theta}}_k = \hat{\boldsymbol{\theta}}_{k-1} + \boldsymbol{K}_k (y_k - \boldsymbol{x}_k^\top \hat{\boldsymbol{\theta}}_{k-1})$

其中，$\boldsymbol{K}_k$ 是**增益向量 (gain vector)**，定义为：

$\boldsymbol{K}_k = \frac{\boldsymbol{P}_{k-1} \boldsymbol{x}_k}{\lambda + \boldsymbol{x}_k^\top \boldsymbol{P}_{k-1} \boldsymbol{x}_k}$

完整的标准 RLS 算法总结如下（初始化 $\hat{\boldsymbol{\theta}}_0$ 和 $\boldsymbol{P}_0$）：
1.  计算增益向量: $\boldsymbol{K}_k = \boldsymbol{P}_{k-1} \boldsymbol{x}_k / (\lambda + \boldsymbol{x}_k^\top \boldsymbol{P}_{k-1} \boldsymbol{x}_k)$
2.  计算先验[预测误差](@entry_id:753692): $e_k = y_k - \boldsymbol{x}_k^\top \hat{\boldsymbol{\theta}}_{k-1}$
3.  更新参数估计: $\hat{\boldsymbol{\theta}}_k = \hat{\boldsymbol{\theta}}_{k-1} + \boldsymbol{K}_k e_k$
4.  更新[逆协方差矩阵](@entry_id:138450): $\boldsymbol{P}_k = \frac{1}{\lambda}(\boldsymbol{I} - \boldsymbol{K}_k \boldsymbol{x}_k^\top) \boldsymbol{P}_{k-1}$

该算法的每一步计算复杂度约为 $\mathcal{O}(p^2)$，远低于直接求逆的 $\mathcal{O}(p^3)$，这使其在实际中变得可行 [@problem_id:2899718]。

### 算法的[收敛性与稳定性](@entry_id:636533)

RLS 算法的良好性能并非无条件的。其核心要求是输入信号必须具有足够的“丰富性”，以确保能够唯一地确定所有待估参数。

在批处理模式下，[最小二乘解](@entry_id:152054) $\hat{\boldsymbol{\theta}} = (\boldsymbol{X}^\top\boldsymbol{X})^{-1}\boldsymbol{X}^\top\boldsymbol{y}$ 存在且唯一的条件是信息矩阵 $\boldsymbol{X}^\top\boldsymbol{X}$ 可逆。这等价于数据矩阵 $\boldsymbol{X}$ 的列是线性无关的，即 $\text{rank}(\boldsymbol{X}) = p$ [@problem_id:2899742]。如果这个条件不满足，意味着存在无穷多组参数可以同样好地拟合数据，参数是**不可辨识的 (non-identifiable)**。

在递归的 RLS 算法中，相应地，我们需要信息矩阵 $\boldsymbol{R}_k = \sum_{i=1}^k \lambda^{k-i} \boldsymbol{x}_i \boldsymbol{x}_i^\top$ 在所有时刻 $k$ 都保持可逆（即正定）。对于 $\lambda=1$ 的情况，只要输入序列 $\{ \boldsymbol{x}_k \}$ 随着时间的推移最终能张成整个 $p$ 维空间，$\boldsymbol{R}_k$ 最终会变得可逆。然而，当[遗忘因子](@entry_id:175644) $\lambda  1$ 时，情况变得更为严苛。因为旧的信息被不断遗忘，算法需要持续不断地从新数据中获取关于参数空间所有维度的信息。这个对输入信号的持续丰富性要求，被称为**[持续激励](@entry_id:263834) (Persistent Excitation, PE)** 条件。一个信号被称为[持续激励](@entry_id:263834)的，如果存在常数 $\alpha > 0$ 和整数 $M$，使得在任意长度为 $M$ 的时间窗口内，信息矩阵的累加都满足 $\sum_{i=k}^{k+M-1} \boldsymbol{x}_i \boldsymbol{x}_i^\top \ge \alpha \boldsymbol{I}$。PE 条件保证了[信息矩阵](@entry_id:750640) $\boldsymbol{R}_k$ 的[最小特征值](@entry_id:177333)有正的下界，从而保证了算法的稳定性。

如果 PE 条件不满足，且 $\lambda  1$，RLS 算法可能会表现出灾难性的行为。一个典型的例子是当输入信号 $\boldsymbol{x}_k$ 在一段时间内变为零或接近零时 [@problem_id:2899724]。在此期间，由于没有新的信息输入，$\boldsymbol{P}_k$ 的更新公式近似为 $\boldsymbol{P}_k \approx \frac{1}{\lambda} \boldsymbol{P}_{k-1}$。由于 $\lambda  1$，$\boldsymbol{P}_k$ 矩阵会指数级增长，这种现象被称为**[协方差膨胀](@entry_id:635604) (covariance blow-up)**。当一个微弱的非零输入 $\boldsymbol{x}_k$ 最终出现时，巨大的 $\boldsymbol{P}_{k-1}$ 会导致增益向量 $\boldsymbol{K}_k$ 变得极大。这个巨大的增益会将测量噪声不成比例地放大，并加到[参数估计](@entry_id:139349)中，导致 $\hat{\boldsymbol{\theta}}_k$ 发生剧烈的、不稳定的跳变，最终可能导致估计发散。

### 贝叶斯视角：与卡尔曼滤波器的联系

RLS 算法不仅可以从最小二乘优化角度理解，还可以从一个更深刻的贝叶斯或概率视角来审视。事实上，RLS 算法是**卡尔曼滤波器 (Kalman Filter)** 在一个特定[状态空间模型](@entry_id:137993)下的精确实现。这种联系不仅为 RLS 提供了优美的统计解释，也为 $\boldsymbol{P}_k$ 矩阵赋予了清晰的物理意义。

考虑如下的线性状态空间模型，其中待估参数 $\boldsymbol{\theta}_k$ 被视为系统的状态：

- **[状态方程](@entry_id:274378)**: $\boldsymbol{\theta}_k = \boldsymbol{\theta}_{k-1} + \boldsymbol{w}_{k-1}$
- **观测方程**: $y_k = \boldsymbol{x}_k^\top \boldsymbol{\theta}_k + v_k$

这里，$\boldsymbol{w}_{k-1}$ 是[过程噪声](@entry_id:270644)，代表参数随时间的[随机游走](@entry_id:142620)；$v_k$ 是观测噪声。[卡尔曼滤波器](@entry_id:145240)为这一模型提供了最优的（在[均方误差](@entry_id:175403)意义下）线性[递归估计](@entry_id:169954)。

惊人的是，标准 RLS 算法与应用于以下特定模型的卡尔曼滤波器在数学上是完全等价的 [@problem_id:2899731] [@problem_id:2899699]：
1.  [状态转移矩阵](@entry_id:269075)为单位阵，即 $\boldsymbol{A}=\boldsymbol{I}$。
2.  观测矩阵为时变的回归向量，即 $\boldsymbol{H}_k = \boldsymbol{x}_k^\top$。
3.  观测噪声[方差](@entry_id:200758)为 $\lambda$，即 $R_k = \lambda$ (或者等价地，观测噪声[方差](@entry_id:200758)为 1，但整个代价函数被缩放)。
4.  [过程噪声协方差](@entry_id:186358)是时变的，并且与上一时刻的估计[误差协[方](@entry_id:194780)差](@entry_id:200758)成正比：$\boldsymbol{Q}_{k-1} = (\frac{1}{\lambda} - 1)\boldsymbol{P}_{k-1}$。

在这种对应关系下：
-   RLS 的参数估计 $\hat{\boldsymbol{\theta}}_k$ 就是卡尔曼滤波器的后验状态估计 $\hat{\boldsymbol{\theta}}_{k|k}$。
-   RLS 的 $\boldsymbol{P}_k$ 矩阵就是[卡尔曼滤波器](@entry_id:145240)的后验**估计[误差协方差矩阵](@entry_id:749077)** $\boldsymbol{P}_{k|k} = E[(\boldsymbol{\theta}_k - \hat{\boldsymbol{\theta}}_k)(\boldsymbol{\theta}_k - \hat{\boldsymbol{\theta}}_k)^\top | y_{1:k}]$。它量化了我们对当前参数估计的不确定性程度。
-   RLS 的先验误差 $e_k = y_k - \boldsymbol{x}_k^\top \hat{\boldsymbol{\theta}}_{k-1}$ 是[卡尔曼滤波](@entry_id:145240)中的**新息 (innovation)**，即基于旧知识对新息观的预测与实际观测之差。它代表了新测量值中包含的“意外”信息。
-   增益向量 $\boldsymbol{K}_k$ 的作用是根据新息的大小以及我们对[先验估计](@entry_id:186098)和新观测的信任程度（由 $\boldsymbol{P}_{k-1}$ 和噪声[方差](@entry_id:200758)决定）来修正[先验估计](@entry_id:186098)。我们可以将增益向量写作 $K_k = P_{k-1} \boldsymbol{x}_k / \sigma_k^2$，其中 $\sigma_k^2 = \lambda + \boldsymbol{x}_k^\top P_{k-1} \boldsymbol{x}_k$ 可以被解释为**新息[方差](@entry_id:200758)**的标度版本 [@problem_id:2899699]。

[遗忘因子](@entry_id:175644) $\lambda$ 的作用在贝叶斯视角下得到了清晰的解释：它通过引入一个非零的[过程噪声](@entry_id:270644) $\boldsymbol{Q}_{k-1}$ 来对先验协[方差](@entry_id:200758)进行膨胀 ($P_{k|k-1} = P_{k-1|k-1} + Q_{k-1} = \frac{1}{\lambda}P_{k-1|k-1}$)。这相当于在每个时间步，我们主动增加对参数的不确定性，声明参数可能已经发生了变化。这种“不确定性的注入”使得滤波器能够不断地接纳新的数据来跟踪参数的变化。

### 实际应用中的挑战与扩展

标准的 RLS 算法在理想条件下表现优异，但在实际应用中，我们必须面对两个主要挑战：输入与噪声相关导致的有偏估计，以及有限精度计算带来的[数值稳定性](@entry_id:146550)问题。

#### 有偏估计与[工具变量法](@entry_id:204495)

[最小二乘估计](@entry_id:262764)的一个基本假设是，回归向量 $\boldsymbol{x}_k$ 与真实的方程误差是统计不相关的。然而，在许多实际问题中，这个假设不成立。一个典型的例子是带有[测量噪声](@entry_id:275238)的[自回归 (AR) 模型](@entry_id:265459)辨识 [@problem_id:2899692]。

假设真实系统为 $y_k = -\sum a_i y_{k-i} + e_k$，但我们只能观测到被[噪声污染](@entry_id:188797)的信号 $d_k = y_k + v_k$。如果我们用过去的观测值构造回归向量 $\boldsymbol{\phi}_k = -[d_{k-1}, \dots, d_{k-p}]^\top$ 来估计参数 $\boldsymbol{\theta}_0 = [a_1, \dots, a_p]^\top$，那么回归向量 $\boldsymbol{\phi}_k$ 中包含了噪声项 $v_{k-1}, \dots, v_{k-p}$。同时，真实的方程误差 $\varepsilon_k = d_k - \boldsymbol{\phi}_k^\top \boldsymbol{\theta}_0$ 也包含了这些噪声项。因此，$E[\boldsymbol{\phi}_k \varepsilon_k] \neq \mathbf{0}$，[最小二乘估计](@entry_id:262764)的基本[正交性原理](@entry_id:153755)被打破，导致 RLS 算法收敛到一个有偏的估计。

为了解决这个问题，可以采用**工具变量 (Instrumental Variable, IV)** 方法。IV 方法引入一个辅助的**工具向量 (instrument vector)** $\boldsymbol{z}_k$，它需要满足两个条件：
1.  与真实的方程误差不相关，即 $E[\boldsymbol{z}_k \varepsilon_k] = \mathbf{0}$。
2.  与回归向量充分相关，即矩阵 $E[\boldsymbol{z}_k \boldsymbol{\phi}_k^\top]$ 是非奇异的。

通过用工具向量 $\boldsymbol{z}_k$ 替代回归向量 $\boldsymbol{\phi}_k$ 在[正规方程](@entry_id:142238)中的一个位置，IV 方法旨在满足 $E[\boldsymbol{z}_k (d_k - \boldsymbol{\phi}_k^\top\boldsymbol{\theta})] = 0$，从而获得一致的估计。其递归形式，即**递归[工具变量](@entry_id:142324) (Recursive Instrumental Variable, RIV)** 算法，与 RLS 非常相似，但其增益和协[方差](@entry_id:200758)更新中非对称地使用了 $\boldsymbol{z}_k$ 和 $\boldsymbol{\phi}_k$ [@problem_id:2899692]：

$\boldsymbol{K}_k = \frac{\boldsymbol{P}_{k-1} \boldsymbol{z}_k}{\lambda + \boldsymbol{\phi}_k^\top \boldsymbol{P}_{k-1} \boldsymbol{z}_k}, \quad \boldsymbol{P}_k = \frac{1}{\lambda}(\boldsymbol{P}_{k-1} - \boldsymbol{K}_k \boldsymbol{\phi}_k^\top \boldsymbol{P}_{k-1})$

选择合适的工具变量是 IV 方法的关键，这通常需要利用问题的特定结构。

#### 数值稳定性与平方根滤波

标准 RLS 算法中的协方差矩阵更新 $P_k = \frac{1}{\lambda}(\boldsymbol{I} - \boldsymbol{K}_k \boldsymbol{x}_k^\top)\boldsymbol{P}_{k-1}$ 包含一个减法操作。在有限精度的[浮点运算](@entry_id:749454)中，当数据病态（例如，回归向量在一段时间内接近共线）时，这个减法可能会导致**灾难性抵消 (catastrophic cancellation)** [@problem_id:2899705]。

这种数值误差的累积可能导致计算出的 $\boldsymbol{P}_k$ 矩阵失去其理论上应有的对称性和[正定性](@entry_id:149643)。一旦 $\boldsymbol{P}_k$ 变为非正定，算法可能会变得不稳定并最终发散。

为了克服这一严重的数值问题，**平方根滤波 (square-root filtering)** 技术应运而生。其核心思想是避免直接更新协方差矩阵 $\boldsymbol{P}_k$ 或[信息矩阵](@entry_id:750640) $\boldsymbol{S}_k = \boldsymbol{P}_k^{-1}$，而是对它们的一个[矩阵平方根](@entry_id:158930)（例如 Cholesky 分解因子）进行递推。例如，如果我们维护 $\boldsymbol{S}_k$ 的 Cholesky 因子 $\boldsymbol{R}_k$（一个上三角矩阵，满足 $\boldsymbol{S}_k = \boldsymbol{R}_k^\top \boldsymbol{R}_k$），那么信息矩阵的更新 $\boldsymbol{S}_k = \lambda \boldsymbol{S}_{k-1} + \boldsymbol{x}_k \boldsymbol{x}_k^\top$ 就转化为一个寻找新的 Cholesky 因子 $\boldsymbol{R}_k$ 的问题。

这个问题可以通过数值上非常稳定的**[正交变换](@entry_id:155650) (orthogonal transformations)**（如 Givens 旋转或 Householder 反射）来解决 [@problem_id:2899705]。这些变换被用来对一个[增广矩阵](@entry_id:150523)进行三角化，从而得到更新后的 Cholesky 因子。因为[正交变换](@entry_id:155650)保持了矩阵的范数，并且不涉及大规模的减法操作，所以它们在数值上是向后稳定的。通过递推平方根因子，可以保证隐含的协[方差](@entry_id:200758)/[信息矩阵](@entry_id:750640)始终是正定和对称的，从而极大地增强了 RLS 算法在严苛条件下的鲁棒性。虽然计算上更复杂一些，但对于高精度和高可靠性要求的应用，平方根 RLS 算法是首选。