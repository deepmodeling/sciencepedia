## 引言
在[统计推断](@entry_id:172747)的实践中，我们的兴趣点往往超越了对参数本身的估计，而更多地关注于这些参数的函数。例如，流行病学家在估计了患病率后，可能更关心其发生比；金融分析师在估计了资产的平均回报和波动率后，需要计算其[夏普比率](@entry_id:136824)。[中心极限定理](@entry_id:143108)为我们估计样本均值等统计量的[分布](@entry_id:182848)提供了坚实的基础，但并未直接回答如何确定这些统计量经过[非线性变换](@entry_id:636115)后的[分布](@entry_id:182848)。这一知识鸿沟正是[德尔塔方法](@entry_id:276272)所要解决的核心问题。

[德尔塔方法](@entry_id:276272)是一个强大而灵活的工具，它通过[泰勒级数展开](@entry_id:138468)的思想，为我们提供了一种系统性的方式来近似估计量函数的[抽样分布](@entry_id:269683)和[方差](@entry_id:200758)。本文将引导您深入理解[德尔塔方法](@entry_id:276272)。在“原理与机制”一章中，我们将从最基础的单变量一阶方法入手，逐步扩展到多变量情形，并探讨在一阶近似失效时如何运用二阶方法。随后，在“应用与跨学科联系”一章中，我们将通过物理学、生命科学、[金融工程](@entry_id:136943)等多个领域的实例，展示[德尔塔方法](@entry_id:276272)在解决实际问题中的广泛适用性。最后，“动手实践”部分将提供具体的练习，帮助您将理论知识转化为解决问题的能力。

## 原理与机制

在统计推断中，我们经常依赖于[中心极限定理](@entry_id:143108)（Central Limit Theorem）来确定样本均值或其他类似估计量的[渐近分布](@entry_id:272575)。然而，在许多实际应用中，我们感兴趣的量往往不是估计量本身，而是其某个函数。例如，我们可能通过样本比例 $\hat{p}$ 来估计一个群体的患病率，但我们更关心的是该疾病的发生比（odds），即 $\frac{\hat{p}}{1-\hat{p}}$。另一个例子是，物理学家可能测量了粒子的平均寿命 $\bar{T}$，但理论模型的核心参数是[衰变率](@entry_id:156530) $\frac{1}{\bar{T}}$。在这些情况下，我们需要一个系统性的方法来从原始估计量的[渐近分布](@entry_id:272575)推导出其函数的[渐近分布](@entry_id:272575)。[Delta方法](@entry_id:276272)正是解决这一问题的核心工具。

[Delta方法](@entry_id:276272)利用[泰勒展开](@entry_id:145057)式（Taylor expansion）来[局部线性化](@entry_id:169489)一个函数，从而将一个已知渐近[正态分布](@entry_id:154414)的估计量的性质“传递”给它的一个变换。本章将系统地阐述[Delta方法](@entry_id:276272)的原理，从最基础的一阶单变量情形，到多变量情形，最后探讨当一阶近似失效时所需的二阶方法。

### 一阶[Delta方法](@entry_id:276272)：单变量情形

[Delta方法](@entry_id:276272)的核心思想是，在一个[点的邻域](@entry_id:144055)内，一个光滑的函数可以被其[切线](@entry_id:268870)很好地近似。假设我们有一个估计量序列 $\hat{\theta}_n$，它以某种方式收敛于真实参数 $\theta$。具体来说，我们通常有如下形式的中心极限定理结果：
$$
\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} \mathcal{N}(0, \sigma^2)
$$
这里，$\xrightarrow{d}$ 表示[依分布收敛](@entry_id:275544)（convergence in distribution），$\mathcal{N}(0, \sigma^2)$ 代表一个均值为0、[方差](@entry_id:200758)为 $\sigma^2$ 的正态分布。

现在，假设我们对 $g(\hat{\theta}_n)$ 的[分布](@entry_id:182848)感兴趣，其中 $g$ 是一个在 $\theta$ 点可微的函数，并且其导数 $g'(\theta)$ 不为零。我们可以对 $g(\hat{\theta}_n)$ 在 $\theta$ 点进行一阶[泰勒展开](@entry_id:145057)：
$$
g(\hat{\theta}_n) \approx g(\theta) + g'(\theta)(\hat{\theta}_n - \theta)
$$
这个近似在 $\hat{\theta}_n$ 接近 $\theta$ 时（即样本量 $n$ 很大时）非常精确。通过简单的代数变换，我们得到：
$$
g(\hat{\theta}_n) - g(\theta) \approx g'(\theta)(\hat{\theta}_n - \theta)
$$
将两边同时乘以 $\sqrt{n}$：
$$
\sqrt{n}(g(\hat{\theta}_n) - g(\theta)) \approx g'(\theta) \left( \sqrt{n}(\hat{\theta}_n - \theta) \right)
$$
由于我们已知 $\sqrt{n}(\hat{\theta}_n - \theta)$ 渐近服从一个均值为0、[方差](@entry_id:200758)为 $\sigma^2$ 的[正态分布](@entry_id:154414)，而上式右边是这个渐近正态[随机变量](@entry_id:195330)乘以一个常数 $g'(\theta)$，因此，左边的项也将渐近服从一个[正态分布](@entry_id:154414)。一个正态变量 $X \sim \mathcal{N}(0, \sigma^2)$ 乘以常数 $c$ 后，得到的新变量 $cX$ 服从 $\mathcal{N}(0, c^2 \sigma^2)$。因此，我们可以得出**一阶[Delta方法](@entry_id:276272)**的结论：
$$
\sqrt{n}(g(\hat{\theta}_n) - g(\theta)) \xrightarrow{d} \mathcal{N}(0, [g'(\theta)]^2 \sigma^2)
$$

这意味着，对于大的样本量 $n$，$g(\hat{\theta}_n)$ 近似服从一个正态分布，其均值为 $g(\theta)$，[方差](@entry_id:200758)为 $\frac{[g'(\theta)]^2 \sigma^2}{n}$。

让我们通过几个例子来具体理解这个强大的工具。

- **估计量的[函数变换](@entry_id:141095)**：在[材料科学](@entry_id:152226)中，假设我们测量了 $n$ 个纳米晶体的边长，得到样本均值 $\bar{X}_n$。我们知道 $\bar{X}_n$ 是真实平均边长 $\mu$ 的一个良好估计。如果我们对一个边长等于 $\bar{X}_n$ 的立方体的体积感兴趣，即 $V_n = \bar{X}_n^3$，我们可以使用[Delta方法](@entry_id:276272)。这里，$\hat{\theta}_n = \bar{X}_n$，$\theta = \mu$，而变换函数是 $g(x) = x^3$。其导数为 $g'(x) = 3x^2$。根据[中心极限定理](@entry_id:143108)，$\sqrt{n}(\bar{X}_n - \mu) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$，其中 $\sigma^2$ 是单个晶体边长的[方差](@entry_id:200758)。应用[Delta方法](@entry_id:276272)， $V_n$ 的[渐近方差](@entry_id:269933)为 $\operatorname{Var}(V_n) \approx \frac{[g'(\mu)]^2 \sigma^2}{n} = \frac{(3\mu^2)^2 \sigma^2}{n} = \frac{9\mu^4\sigma^2}{n}$ [@problem_id:1959853]。

- **倒数变换**：在粒子物理学中，[衰变率](@entry_id:156530)是[平均寿命](@entry_id:195236)的倒数。如果测得的[平均寿命](@entry_id:195236)为 $\bar{T}$，那么[衰变率](@entry_id:156530)的估计量就是 $R = 1/\bar{T}$。这里，$g(t) = 1/t$，其导数为 $g'(t) = -1/t^2$。如果真实平均寿命为 $\mu_T$，单个寿命测量的[方差](@entry_id:200758)为 $\sigma_T^2$，则 $\operatorname{Var}(\bar{T}) = \sigma_T^2/n$。因此，衰变率估计量 $R$ 的近似[方差](@entry_id:200758)为 $\operatorname{Var}(R) \approx [g'(\mu_T)]^2 \operatorname{Var}(\bar{T}) = (-1/\mu_T^2)^2 (\sigma_T^2/n) = \frac{\sigma_T^2}{n\mu_T^4}$ [@problem_id:1959804]。

- **[对数变换](@entry_id:267035)**：[对数变换](@entry_id:267035)在统计学中非常普遍，常用于处理具有[正偏态分布](@entry_id:275398)的数据或稳定[方差](@entry_id:200758)。假设气候学家对平均降雨量的对数 $\ln(\bar{X}_n)$ 感兴趣。这里 $g(x) = \ln(x)$，导数为 $g'(x) = 1/x$。如果真实均值为 $\mu$，[方差](@entry_id:200758)为 $\sigma^2$，则 $\operatorname{Var}(\ln(\bar{X}_n)) \approx \frac{[g'(\mu)]^2 \sigma^2}{n} = \frac{(1/\mu)^2 \sigma^2}{n} = \frac{\sigma^2}{n\mu^2}$。这个结果本身很有趣：对数均值的[渐近方差](@entry_id:269933)等于样本均值的相对[变异系数](@entry_id:272423)（[方差](@entry_id:200758)除以均值的平方）除以 $n$。在某些特定[分布](@entry_id:182848)下，这个表达式可以进一步简化。例如，对于均值为 $\mu = \alpha/\beta$、[方差](@entry_id:200758)为 $\sigma^2 = \alpha/\beta^2$ 的伽玛[分布](@entry_id:182848)，$\operatorname{Var}(\ln(\bar{X}_n))$ 的近似值为 $\frac{\alpha/\beta^2}{n(\alpha/\beta)^2} = \frac{1}{\alpha n}$ [@problem_id:1959841]。

- **发生比（Odds）的估计**：在流行病学中，发生比 $\theta = p/(1-p)$ 是一个比概率 $p$ 更常用的度量。样本发生比为 $\hat{\theta} = \hat{p}/(1-\hat{p})$，其中 $\hat{p}$ 是样本比例。这里，$g(p) = p/(1-p)$，$g'(p) = 1/(1-p)^2$。我们知道 $\hat{p}$ 的[渐近方差](@entry_id:269933)是 $p(1-p)/n$。因此，样本发生比 $\hat{\theta}$ 的[渐近方差](@entry_id:269933)为 $\operatorname{Var}(\hat{\theta}) \approx \frac{[g'(p)]^2 p(1-p)}{n} = \frac{1}{(1-p)^4} \frac{p(1-p)}{n} = \frac{p}{n(1-p)^3}$ [@problem_id:1959818]。

### 应用：[方差稳定变换](@entry_id:273381)

在上述例子中，我们看到 $g(\hat{\theta}_n)$ 的[渐近方差](@entry_id:269933)通常依赖于未知参数 $\theta$。例如，$\operatorname{Var}(\hat{p}/(1-\hat{p}))$ 依赖于 $p$。这在构建[置信区间](@entry_id:142297)或进行假设检验时会带来不便，因为我们需要在[方差](@entry_id:200758)公式中再插入一个对 $\theta$ 的估计。

一个自然的问题是：我们能否找到一个变换 $g$，使得 $g(\hat{\theta}_n)$ 的[渐近方差](@entry_id:269933)是一个**常数**，不依赖于 $\theta$？这样的变换被称为**[方差稳定变换](@entry_id:273381)**（variance-stabilizing transformation）。

我们的目标是找到一个 $g$，使得 $[g'(\theta)]^2 \sigma^2(\theta) = c$（常数）。这意味着 $g'(\theta)$ 必须正比于 $1/\sigma(\theta)$。通过对 $1/\sigma(\theta)$ 积分，我们就可以找到所需的变换函数 $g$。

一个经典例子是伯努利试验中的样本比例 $\hat{p}_n$。其[渐近方差](@entry_id:269933)为 $\sigma^2(p) = p(1-p)$。为了稳定[方差](@entry_id:200758)，我们需要找到一个函数 $g(p)$，其导数 $g'(p)$ 满足：
$$
[g'(p)]^2 p(1-p) = c
$$
这意味着 $g'(p) \propto \frac{1}{\sqrt{p(1-p)}}$。这个[微分方程](@entry_id:264184)的解是反正弦函数。具体来说，如果我们选择变换 $g(p) = \arcsin(\sqrt{p})$，我们可以计算其导数：
$$
g'(p) = \frac{1}{\sqrt{1-(\sqrt{p})^2}} \cdot \frac{d}{dp}(\sqrt{p}) = \frac{1}{\sqrt{1-p}} \cdot \frac{1}{2\sqrt{p}} = \frac{1}{2\sqrt{p(1-p)}}
$$
现在，我们应用[Delta方法](@entry_id:276272)来计算 $Y_n = \arcsin(\sqrt{\hat{p}_n})$ 的[渐近方差](@entry_id:269933)。这个[方差](@entry_id:200758)是 $[g'(p)]^2 \sigma^2(p) = \left( \frac{1}{2\sqrt{p(1-p)}} \right)^2 \cdot p(1-p) = \frac{1}{4p(1-p)} \cdot p(1-p) = \frac{1}{4}$ [@problem_id:1959833]。

这是一个非常漂亮的结果：经过反正弦平方根变换后，样本比例的[渐近方差](@entry_id:269933)稳定为常数 $1/4$，完全独立于真实的成功概率 $p$。这使得基于 $Y_n$ 的[统计推断](@entry_id:172747)在某些情况下更为简洁和稳健。

### 一阶[Delta方法](@entry_id:276272)：多变量情形

[Delta方法](@entry_id:276272)可以自然地推广到处理多个估计量的函数。假设我们有一个 $k$ 维的估计量向量 $\hat{\boldsymbol{\theta}}_n = (\hat{\theta}_{1,n}, \dots, \hat{\theta}_{k,n})$，它收敛于参数向量 $\boldsymbol{\theta} = (\theta_1, \dots, \theta_k)$。多变量中心极限定理告诉我们：
$$
\sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta}) \xrightarrow{d} \mathcal{N}_k(\mathbf{0}, \boldsymbol{\Sigma})
$$
其中 $\mathbf{0}$ 是 $k$ 维[零向量](@entry_id:156189)，$\boldsymbol{\Sigma}$ 是一个 $k \times k$ 的[协方差矩阵](@entry_id:139155)。

现在，我们考虑一个从 $\mathbb{R}^k$ 到 $\mathbb{R}$ 的函数 $g(\boldsymbol{\theta})$，并希望找到 $g(\hat{\boldsymbol{\theta}}_n)$ 的[渐近分布](@entry_id:272575)。同样，我们使用[泰勒展开](@entry_id:145057)，这次是多变量形式：
$$
g(\hat{\boldsymbol{\theta}}_n) \approx g(\boldsymbol{\theta}) + (\nabla g(\boldsymbol{\theta}))^T (\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta})
$$
其中 $\nabla g(\boldsymbol{\theta})$ 是 $g$ 在 $\boldsymbol{\theta}$ 点的[梯度向量](@entry_id:141180)，即由偏导数组成的列向量：
$$
\nabla g(\boldsymbol{\theta}) = \begin{pmatrix} \frac{\partial g}{\partial \theta_1} \\ \vdots \\ \frac{\partial g}{\partial \theta_k} \end{pmatrix}
$$
与单变量情况类似，我们得到：
$$
\sqrt{n}(g(\hat{\boldsymbol{\theta}}_n) - g(\boldsymbol{\theta})) \approx (\nabla g(\boldsymbol{\theta}))^T \left( \sqrt{n}(\hat{\boldsymbol{\theta}}_n - \boldsymbol{\theta}) \right)
$$
右侧是一个向量的[线性组合](@entry_id:154743)，其中该向量服从多维[正态分布](@entry_id:154414)。结果仍然是一个正态分布，其[方差](@entry_id:200758)是一个二次型（quadratic form）。**多变量[Delta方法](@entry_id:276272)**的结论是：
$$
\sqrt{n}(g(\hat{\boldsymbol{\theta}}_n) - g(\boldsymbol{\theta})) \xrightarrow{d} \mathcal{N}(0, (\nabla g(\boldsymbol{\theta}))^T \boldsymbol{\Sigma} (\nabla g(\boldsymbol{\theta})))
$$
当估计量 $\hat{\theta}_{i,n}$ 之间相互独立时，协方差矩阵 $\boldsymbol{\Sigma}$ 是一个对角矩阵，对角线上的元素为 $\sigma_i^2 = \operatorname{Var}(\sqrt{n}(\hat{\theta}_{i,n}-\theta_i))$。在这种常见情况下，[渐近方差](@entry_id:269933)的二次型表达式简化为：
$$
(\nabla g(\boldsymbol{\theta}))^T \boldsymbol{\Sigma} (\nabla g(\boldsymbol{\theta})) = \sum_{i=1}^k \left(\frac{\partial g}{\partial \theta_i}\right)^2 \sigma_i^2
$$

让我们看两个基于[独立样本](@entry_id:177139)均值的例子。

- **两个均值的比率**：生物学家可能想要比较两个独立种群的某个特征，例如甲虫的平均体长。假设从种群 $X$ 和 $Y$ 中分别抽取了 $n$ 和 $m$ 个样本，得到样本均值 $\bar{X}_n$ 和 $\bar{Y}_m$。我们对它们的比率 $R = \bar{X}_n / \bar{Y}_m$ 感兴趣。这里，函数是 $g(x, y) = x/y$，参数是 $(\mu_X, \mu_Y)$。梯度向量为 $\nabla g = (1/y, -x/y^2)^T$。由于样本是独立的，$\bar{X}_n$ 和 $\bar{Y}_m$ 也是独立的，所以它们的协[方差](@entry_id:200758)为零。因此，$R$ 的近似[方差](@entry_id:200758)为：
$$
\operatorname{Var}(R) \approx \left(\frac{\partial g}{\partial \mu_X}\right)^2 \operatorname{Var}(\bar{X}_n) + \left(\frac{\partial g}{\partial \mu_Y}\right)^2 \operatorname{Var}(\bar{Y}_m) = \left(\frac{1}{\mu_Y}\right)^2 \frac{\sigma_X^2}{n} + \left(-\frac{\mu_X}{\mu_Y^2}\right)^2 \frac{\sigma_Y^2}{m} = \frac{\sigma_X^2}{n\mu_Y^2} + \frac{\mu_X^2 \sigma_Y^2}{m\mu_Y^4}
$$
[@problem_id:1959801]。

- **两个均值的乘积**：一个在线零售商可能想通过估计平均购买商品数量（$\mu_X$）和商品的平均价格（$\mu_Y$）来估计每位顾客的平均收入。估计量为 $T = \bar{X}_n \bar{Y}_m$。这里，函数是 $g(x,y)=x \cdot y$，梯度为 $\nabla g = (y, x)^T$。同样，在独立性的假设下，估计量 $T$ 的近似[方差](@entry_id:200758)为：
$$
\operatorname{Var}(T) \approx \left(\frac{\partial g}{\partial \mu_X}\right)^2 \operatorname{Var}(\bar{X}_n) + \left(\frac{\partial g}{\partial \mu_Y}\right)^2 \operatorname{Var}(\bar{Y}_m) = \mu_Y^2 \frac{\sigma_X^2}{n} + \mu_X^2 \frac{\sigma_Y^2}{m}
$$
[@problem_id:1959837]。

### 二阶[Delta方法](@entry_id:276272)：当一阶近似失效时

一阶[Delta方法](@entry_id:276272)依赖于一个关键假设：$g'(\theta) \neq 0$。如果 $g'(\theta) = 0$，那么一阶泰勒近似项 $g'(\theta)(\hat{\theta}_n - \theta)$ 就消失了。在这种情况下，一阶[Delta方法](@entry_id:276272)会错误地预测[渐近方差](@entry_id:269933)为0。这并不意味着 $g(\hat{\theta}_n)$ 没有变异性，而是意味着它的[收敛速度](@entry_id:636873)比 $\hat{\theta}_n$ 更快，并且其[极限分布](@entry_id:174797)不再是正态分布。

为了处理这种情况，我们需要将[泰勒展开](@entry_id:145057)推进到二阶：
$$
g(\hat{\theta}_n) \approx g(\theta) + g'(\theta)(\hat{\theta}_n - \theta) + \frac{1}{2}g''(\theta)(\hat{\theta}_n - \theta)^2
$$
当 $g'(\theta) = 0$ 且 $g''(\theta) \neq 0$ 时，上式变为：
$$
g(\hat{\theta}_n) - g(\theta) \approx \frac{1}{2}g''(\theta)(\hat{\theta}_n - \theta)^2
$$
这次，我们两边同时乘以 $n$（而不是 $\sqrt{n}$）：
$$
n(g(\hat{\theta}_n) - g(\theta)) \approx \frac{1}{2}g''(\theta) \left( \sqrt{n}(\hat{\theta}_n - \theta) \right)^2
$$
我们知道 $\sqrt{n}(\hat{\theta}_n - \theta)$ [依分布收敛](@entry_id:275544)于一个正态[随机变量](@entry_id:195330) $Z \sim \mathcal{N}(0, \sigma^2)$。根据[连续映射定理](@entry_id:269346)（Continuous Mapping Theorem），它的平方会收敛于 $Z^2$ 的[分布](@entry_id:182848)。标准正态变量的平方服从自由度为1的[卡方分布](@entry_id:165213)（$\chi^2_1$）。因此，$Z^2 = (\sigma \cdot \frac{Z}{\sigma})^2 = \sigma^2 \cdot (\frac{Z}{\sigma})^2$，其中 $\frac{Z}{\sigma} \sim \mathcal{N}(0,1)$，所以 $Z^2$ 的[分布](@entry_id:182848)是 $\sigma^2 \cdot \chi^2_1$。

这就引出了**二阶[Delta方法](@entry_id:276272)**的结论：如果 $\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{d} \mathcal{N}(0, \sigma^2)$，且 $g'(\theta)=0, g''(\theta) \neq 0$，则：
$$
n(g(\hat{\theta}_n) - g(\theta)) \xrightarrow{d} \frac{1}{2}g''(\theta)\sigma^2 \cdot \chi^2_1
$$
这个结果揭示了两个关键点：(1) 标准化因子从 $\sqrt{n}$ 变为 $n$。(2) [极限分布](@entry_id:174797)不再是正态分布，而是一个经过缩放的[卡方分布](@entry_id:165213) [@problem_id:1959813]。

让我们来看几个重要的例子。

- **零均值过程的能量**：在信号处理中，我们可能对一个均值为零的噪声信号的能量感兴趣，这与样本均值的平方有关。假设我们有来自均值为 $\mu=0$、[方差](@entry_id:200758)为 $\sigma^2$ 的[分布](@entry_id:182848)的样本。我们想知道 $n\bar{X}_n^2$ 的[极限分布](@entry_id:174797)。这里，$\hat{\theta}_n = \bar{X}_n$，$\theta = \mu = 0$。我们考察的函数是 $g(x) = x^2$。其导数为 $g'(x) = 2x$，所以在 $\mu=0$ 处，$g'(0)=0$。[二阶导数](@entry_id:144508) $g''(x)=2$。这正是一个需要二阶[Delta方法](@entry_id:276272)的情形。将 $\theta=0, g''(0)=2$ 和中心极限定理的[方差](@entry_id:200758) $\sigma^2$ 代入二阶公式，我们发现 $n(g(\bar{X}_n) - g(0)) = n\bar{X}_n^2$ 的[极限分布](@entry_id:174797)是 $\frac{1}{2} g''(0) \sigma^2 \cdot \chi^2_1 = \frac{1}{2} (2) \sigma^2 \cdot \chi^2_1 = \sigma^2 \cdot \chi^2_1$ [@problem_id:1396660]。

- **公平硬币的样本[方差](@entry_id:200758)**：考虑一个成功概率为 $p=1/2$ 的伯努利过程（例如，抛掷一枚公平的硬币）。样本[方差](@entry_id:200758)的估计量是 $\hat{S}_n^2 = \hat{p}_n(1-\hat{p}_n)$，真实[方差](@entry_id:200758)是 $\sigma^2 = p(1-p)=1/4$。我们想知道 $n(\hat{S}_n^2 - 1/4)$ 的[极限分布](@entry_id:174797)。这里的变换函数是 $g(p)=p(1-p)$，我们在点 $p=1/2$ 处进行分析。导数 $g'(p)=1-2p$，因此 $g'(1/2)=0$。[二阶导数](@entry_id:144508) $g''(p)=-2$。这是一个典型的二阶[Delta方法](@entry_id:276272)应用场景。[中心极限定理](@entry_id:143108)告诉我们，对于 $\hat{p}_n$，其[渐近方差](@entry_id:269933)参数是 $\sigma^2_{\hat{p}} = p(1-p)=1/4$。应用二阶公式，[极限分布](@entry_id:174797)为：
$$
\frac{1}{2}g''(1/2) \sigma^2_{\hat{p}} \cdot \chi^2_1 = \frac{1}{2}(-2)\left(\frac{1}{4}\right) \cdot \chi^2_1 = -\frac{1}{4}\chi^2_1
$$
这个结果表明，当真实概率为 $1/2$ 时，样本[方差](@entry_id:200758)的波动性呈现出一种特定的、非正态的缩放[卡方分布](@entry_id:165213)形态 [@problem_id:1959855]。

总而言之，[Delta方法](@entry_id:276272)是一个极其有用的统计工具，它将[中心极限定理](@entry_id:143108)的[适用范围](@entry_id:636189)从简单的估计量本身扩展到了这些估计量的任意[光滑函数](@entry_id:267124)。无论是进行简单的一阶线性近似，还是在特殊情况下进行更精细的二阶二次近似，[Delta方法](@entry_id:276272)都为理解和量化变换后统计量的渐近行为提供了坚实的理论基础。