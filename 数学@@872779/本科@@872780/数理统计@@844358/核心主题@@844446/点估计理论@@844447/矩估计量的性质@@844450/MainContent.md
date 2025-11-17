## 引言
[矩估计法](@entry_id:270941)（Method of Moments, MOME）是[统计推断](@entry_id:172747)中最古老也最直观的参数估计技术之一。其核心思想——用样本的特征去估计总体的特征——简单而深刻，为更复杂的统计方法奠定了概念基础。尽管现代统计学发展出了效率更高的估计方法，如最大似然估计，但[矩估计法](@entry_id:270941)因其构造简便和广泛的适用性，至今仍在理论研究和实际应用中占据着重要地位。然而，初学者往往只停留在其基本计算层面，对其背后的统计性质、优缺点以及在跨学科领域中的应用缺乏深入理解。

本文旨在填补这一知识鸿沟，为读者提供一个关于矩估计量性质的全面视角。我们将超越基础定义，深入剖析这一经典方法的内在机制与外在价值。

*   在第一章“原理与机制”中，我们将系统梳理[矩估计法](@entry_id:270941)的基本步骤，并通过实例展示其操作流程。更重要的是，本章将深入探讨估计量的有限样本性质（如偏差和[均方误差](@entry_id:175403)）与大样本性质（如相合性和[渐近正态性](@entry_id:168464)），并介绍[Delta方法](@entry_id:276272)等关键分析工具。
*   第二章“应用与跨学科联系”将视野扩展到实际问题中，展示[矩估计法](@entry_id:270941)如何在计量经济学、[生物统计学](@entry_id:266136)、[极值理论](@entry_id:140083)乃至机器学习等不同领域中发挥作用，并探讨其与[方差分析](@entry_id:275547)（[ANOVA](@entry_id:275547)）、[广义矩估计](@entry_id:140147)（GMM）等高级方法的深刻联系。
*   最后，在“动手实践”部分，读者将通过解决一系列精心设计的问题，亲手推导和评估矩估计量，将理论知识转化为实践技能。

通过本次学习，你将不仅掌握[矩估计法](@entry_id:270941)的计算，更能深刻理解其统计特性，并学会在多样化的应用场景中对其进行评估和使用。

## 原理与机制

[矩估计法](@entry_id:270941)（Method of Moments Estimator, MOME）是最早被提出的参数[点估计](@entry_id:174544)方法之一，其核心思想极为直观：**用样本矩来估计相应的[总体矩](@entry_id:170482)**。这一原理基于大数定律所揭示的一个基本事实，即随着样本容量的增大，样本矩会[依概率收敛](@entry_id:145927)于其所对应的[总体矩](@entry_id:170482)。通过建立[总体矩](@entry_id:170482)与未知参数之间的函数关系，并用样本矩取而代之，我们便可以求解出参数的估计量。本章将深入探讨[矩估计法](@entry_id:270941)的核心原理、基本性质及其在实践中应用的具体机制。

### [矩估计法](@entry_id:270941)的原理

[矩估计法](@entry_id:270941)的实施过程系统而直接。首先，我们需要识别待估计参数与[分布](@entry_id:182848)的[总体矩](@entry_id:170482)之间的关系。对于一个由参数 $\theta$ 决定的[随机变量](@entry_id:195330) $X$，其 $k$ 阶[原点矩](@entry_id:165197)定义为 $\mu'_k = \mathbb{E}[X^k]$。相应地，基于一个[独立同分布](@entry_id:169067)的随机样本 $X_1, X_2, \dots, X_n$，其 $k$ 阶样本[原点矩](@entry_id:165197)定义为 $m'_k = \frac{1}{n} \sum_{i=1}^n X_i^k$。

[矩估计法](@entry_id:270941)的基本步骤如下：

1.  确定需要估计的未知参数个数，设为 $p$。
2.  写出该[分布](@entry_id:182848)的前 $p$ 个总体[原点矩](@entry_id:165197)，这些矩通常是未知参数 $\theta_1, \theta_2, \dots, \theta_p$ 的函数。
3.  令前 $p$ 个总体[原点矩](@entry_id:165197)等于对应阶数的样本[原点矩](@entry_id:165197)，从而建立一个包含 $p$ 个方程的[方程组](@entry_id:193238)：
    $$
    \begin{cases}
        \mu'_1(\theta_1, \dots, \theta_p)  = m'_1 \\
        \mu'_2(\theta_1, \dots, \theta_p)  = m'_2 \\
         \vdots \\
        \mu'_p(\theta_1, \dots, \theta_p)  = m'_p
    \end{cases}
    $$
4.  求解这个[方程组](@entry_id:193238)，得到的解 $(\hat{\theta}_1, \dots, \hat{\theta}_p)$ 即为参数的矩估计量。

在最简单的情况下，当只有一个未知参数 $\theta$ 时，我们通常只需使用一阶矩。例如，考虑一个来自[移位](@entry_id:145848)几何分布（shifted Geometric distribution）的样本，其[概率质量函数](@entry_id:265484)为 $P(X=k) = (1-p)^{k-1}p$，其中 $k=1, 2, 3, \dots$。该[分布](@entry_id:182848)的[总体均值](@entry_id:175446)（一阶[原点矩](@entry_id:165197)）为 $\mathbb{E}[X] = 1/p$。根据[矩估计法](@entry_id:270941)，我们令[总体均值](@entry_id:175446)等于样本均值 $\bar{X} = m'_1$，即 $\bar{X} = 1/p$。解出 $p$，便得到其矩估计量 $\hat{p}_{\text{MOME}} = 1/\bar{X}$ [@problem_id:1948436]。同样地，对于 $\text{Beta}(\alpha, 1)$ [分布](@entry_id:182848)，其[概率密度函数](@entry_id:140610)为 $f(x; \alpha) = \alpha x^{\alpha-1}$，[总体均值](@entry_id:175446)为 $\mathbb{E}[X] = \frac{\alpha}{\alpha+1}$。令其等于样本均值 $\bar{X}$，通过简单的代数运算 $\bar{X}(\alpha+1) = \alpha$，可解得 $\alpha$ 的矩估计量为 $\hat{\alpha} = \frac{\bar{X}}{1-\bar{X}}$ [@problem_id:1948439]。

当[分布](@entry_id:182848)涉及多个参数时，则需要建立并求解一个[方程组](@entry_id:193238)。一个经典的例子是[均匀分布](@entry_id:194597) $\text{U}(\theta_1, \theta_2)$，它有两个未知参数。我们需要使用前两个矩来估计它们。该[分布](@entry_id:182848)的前两阶总体[原点矩](@entry_id:165197)为：
$$
\mu'_1 = \mathbb{E}[X] = \frac{\theta_1 + \theta_2}{2}
$$
$$
\mu'_2 = \mathbb{E}[X^2] = \frac{\theta_1^2 + \theta_1\theta_2 + \theta_2^2}{3}
$$
根据[矩估计法](@entry_id:270941)，我们建立[方程组](@entry_id:193238)：
$$
\begin{cases}
    \frac{\theta_1 + \theta_2}{2}  = \bar{X} \\
    \frac{\theta_1^2 + \theta_1\theta_2 + \theta_2^2}{3}  = m'_2 = \frac{1}{n}\sum_{i=1}^n X_i^2
\end{cases}
$$
通过求解这个关于 $\theta_1$ 和 $\theta_2$ 的非线性方程组，可以得到它们的矩估计量为 $\hat{\theta}_1 = \bar{X} - \sqrt{3(m'_2 - \bar{X}^2)}$ 和 $\hat{\theta}_2 = \bar{X} + \sqrt{3(m'_2 - \bar{X}^2)}$ [@problem_id:1948457]。值得注意的是，表达式 $m'_2 - \bar{X}^2$ 正是样本[方差](@entry_id:200758)（分母为 $n$ 的形式）。

### 矩估计量的有限样本性质

在样本量 $n$ 固定的情况下，我们需要关心估计量的几个关键性质，其中最主要的是偏差和[均方误差](@entry_id:175403)。

#### 偏差 (Bias)

一个估计量 $\hat{\theta}$ 的**偏差**定义为 $\text{Bias}(\hat{\theta}) = \mathbb{E}[\hat{\theta}] - \theta$。如果偏差为零，即 $\mathbb{E}[\hat{\theta}] = \theta$，我们称该估计量为**[无偏估计量](@entry_id:756290)**。矩估计量的一个显著特点是它们**通常是有偏的**。

一个重要的例子是[正态分布](@entry_id:154414) $\text{N}(\mu, \sigma^2)$ 的[方差估计](@entry_id:268607)。其前两阶矩为 $\mathbb{E}[X]=\mu$ 和 $\mathbb{E}[X^2]=\mu^2+\sigma^2$。[矩估计法](@entry_id:270941)给出 $\hat{\mu} = \bar{X}$ 和 $m'_2 = \hat{\mu}^2 + \hat{\sigma}^2$。因此，$\sigma^2$ 的矩估计量为 $\hat{\sigma}^2_{\text{MOME}} = m'_2 - \bar{X}^2 = \frac{1}{n}\sum_{i=1}^n X_i^2 - (\frac{1}{n}\sum_{i=1}^n X_i)^2 = \frac{1}{n}\sum_{i=1}^n (X_i - \bar{X})^2$。利用 $\frac{n\hat{\sigma}^2_{\text{MOME}}}{\sigma^2} \sim \chi^2_{n-1}$ 的性质，我们可以计算其期望：
$$
\mathbb{E}[\hat{\sigma}^2_{\text{MOME}}] = \mathbb{E}\left[\frac{\sigma^2}{n} \cdot \frac{n\hat{\sigma}^2_{\text{MOME}}}{\sigma^2}\right] = \frac{\sigma^2}{n}\mathbb{E}[\chi^2_{n-1}] = \frac{\sigma^2}{n}(n-1) = \frac{n-1}{n}\sigma^2
$$
因此，该[估计量的偏差](@entry_id:168594)为 $\text{Bias}(\hat{\sigma}^2_{\text{MOME}}) = \frac{n-1}{n}\sigma^2 - \sigma^2 = -\frac{\sigma^2}{n}$ [@problem_id:1948450]。这是一个负偏差，意味着该估计量倾向于低估真实的[方差](@entry_id:200758)。

当估计量是样本均值的[非线性](@entry_id:637147)函数时，我们可以使用**琴生不等式 (Jensen's Inequality)** 来判断偏差的方向。如果 $g(x)$ 是一个[凸函数](@entry_id:143075)，那么 $\mathbb{E}[g(Y)] \ge g(\mathbb{E}[Y])$。对于前述的移位几何分布，其矩估计量为 $\hat{p} = 1/\bar{X}$。函数 $g(x) = 1/x$ 在其定义域 $(0, \infty)$ 上是[凸函数](@entry_id:143075)。因此，根据琴生不等式：
$$
\mathbb{E}[\hat{p}] = \mathbb{E}\left[\frac{1}{\bar{X}}\right] \ge \frac{1}{\mathbb{E}[\bar{X}]}
$$
由于样本均值是[总体均值](@entry_id:175446)的[无偏估计](@entry_id:756289)，$\mathbb{E}[\bar{X}] = \mathbb{E}[X] = 1/p$。代入上式，我们得到 $\mathbb{E}[\hat{p}] \ge p$。由于在有限样本下 $\bar{X}$ 是一个[随机变量](@entry_id:195330)而非定值，不等式是严格的，即 $\mathbb{E}[\hat{p}] > p$。这表明该估计量是**正偏**的，或称向上偏的 [@problem_id:1948436]。类似地，对于 $\text{Beta}(\alpha, 1)$ [分布](@entry_id:182848)的估计量 $\hat{\alpha} = \frac{\bar{X}}{1-\bar{X}}$，由于函数 $g(x) = \frac{x}{1-x}$ 在 $(0,1)$ 上是[凸函数](@entry_id:143075)，同样可以利用琴生不等式证明其具有正偏差 [@problem_id:1948439]。

#### [均方误差](@entry_id:175403) (Mean Squared Error)

评估一个估计量优劣的综合性指标是**[均方误差 (MSE)](@entry_id:165831)**，其定义为 $\text{MSE}(\hat{\theta}) = \mathbb{E}[(\hat{\theta} - \theta)^2]$。MSE 可以被分解为[估计量方差](@entry_id:263211)和偏差平方的和：
$$
\text{MSE}(\hat{\theta}) = \text{Var}(\hat{\theta}) + (\text{Bias}(\hat{\theta}))^2
$$
这个分解揭示了[偏差和方差](@entry_id:170697)之间的权衡。一个估计量可能有较小的偏差但[方差](@entry_id:200758)很大，或者反之。理想的估计量是两者都很小。

我们再次以正态分布[方差](@entry_id:200758)的MOME $\hat{\sigma}^2_{\text{MOME}} = \frac{1}{n}\sum(X_i-\bar{X})^2$ 为例。我们已经计算出其偏差为 $-\sigma^2/n$。其[方差](@entry_id:200758)可以利用 $\chi^2$ [分布](@entry_id:182848)的[方差](@entry_id:200758) $\text{Var}(\chi^2_k) = 2k$ 来计算：
$$
\text{Var}(\hat{\sigma}^2_{\text{MOME}}) = \text{Var}\left(\frac{\sigma^2}{n}\chi^2_{n-1}\right) = \left(\frac{\sigma^2}{n}\right)^2 \text{Var}(\chi^2_{n-1}) = \frac{\sigma^4}{n^2} \cdot 2(n-1) = \frac{2(n-1)}{n^2}\sigma^4
$$
因此，该估计量的[均方误差](@entry_id:175403)为：
$$
\text{MSE}(\hat{\sigma}^2_{\text{MOME}}) = \frac{2(n-1)}{n^2}\sigma^4 + \left(-\frac{\sigma^2}{n}\right)^2 = \frac{2n-2+1}{n^2}\sigma^4 = \frac{2n-1}{n^2}\sigma^4
$$
这个结果精确地量化了该估计量在有限样本下的表现 [@problem_id:1948450]。

#### 潜在问题

尽管[矩估计法](@entry_id:270941)简单直观，但它也存在一些固有的问题。一个主要问题是，矩估计量的值**可能落在参数空间的有效范围之外**。例如，假设一个参数 $\theta$ 的有效范围是 $(0, 1)$，且其矩估计量恰好是样本均值 $\hat{\theta} = \bar{X}$。如果观测到的一个样本为 $\{-0.4, 0.1, 0.3, 0.6\}$，则 $\bar{X} = 0.15$，这是一个有效的估计。但如果样本是 $\{0.8, 0.9, 1.0, 1.5\}$，则 $\bar{X}=1.05$，这个估计值就超出了 $(0,1)$ 的范围，这在理论上是不合理的 [@problem_id:1948391]。

另一个特点是矩估计量**可能不唯一**。[矩估计法](@entry_id:270941)的定义并未规定必须使用哪几个矩。对于一个单参数问题，我们可以使用一阶矩，也可以使用二阶矩。不同的选择可能导致不同的估计量。例如，对于[拉普拉斯分布](@entry_id:266437) $f(x; b) = \frac{1}{2b} \exp(-|x|/b)$，我们可以通过一阶绝对矩 $\mathbb{E}[|X|]=b$ 得到估计量 $\hat{b}_1 = \frac{1}{n}\sum|X_i|$，也可以通过二阶[原点矩](@entry_id:165197) $\mathbb{E}[X^2] = 2b^2$ 得到估计量 $\hat{b}_2 = \sqrt{\frac{1}{2n}\sum X_i^2}$ [@problem_id:1948428]。这就引出了一个问题：当存在多个可能的矩估计量时，我们应该如何选择？这需要我们考察它们的大样本性质，特别是效率。

### 矩估计量的大样本（渐近）性质

当样本量 $n$ 趋于无穷时，估计量的性质称为[渐近性质](@entry_id:177569)。对于矩估计量而言，其[渐近性质](@entry_id:177569)通常非常良好，这也是该方法虽古老但仍具价值的重要原因。

#### 相合性 (Consistency)

一个估计量序列 $\hat{\theta}_n$ 如果随着 $n \to \infty$ **[依概率收敛](@entry_id:145927)**于真值 $\theta$（记作 $\hat{\theta}_n \xrightarrow{P} \theta$），则称其为**[相合估计量](@entry_id:266642)**。相合性是评价估计量的一个基本要求，它意味着只要有足够多的数据，我们就能得到任意接近真实参数的估计。

矩估计量通常是相合的。其理论基础在于**大数定律 (Law of Large Numbers, LLN)** 和**[连续映射定理](@entry_id:269346) (Continuous Mapping Theorem, CMT)**。[大数定律](@entry_id:140915)保证了样本矩[依概率收敛](@entry_id:145927)于[总体矩](@entry_id:170482)，即 $m'_k \xrightarrow{P} \mu'_k$。由于矩估计量是通过[求解方程组](@entry_id:152624)得到的，它通常是样本矩的[连续函数](@entry_id:137361)，记为 $\hat{\theta}_n = g(m'_1, m'_2, \dots)$。[连续映射定理](@entry_id:269346)则保证了，如果矩估计量是样本矩的[连续函数](@entry_id:137361)，那么估计量本身也将收敛到以[总体矩](@entry_id:170482)为输入的同一函数的值，即 $\hat{\theta}_n \xrightarrow{P} g(\mu'_1, \mu'_2, \dots) = \theta$。

让我们以[几何分布](@entry_id:154371)的参数估计为例来正式说明这一点。估计量 $\hat{p}_n = \frac{n-1}{n\bar{X}_n}$ 是对标准MOME的一个微小修正。根据[弱大数定律](@entry_id:159016)，样本均值 $\bar{X}_n$ [依概率收敛](@entry_id:145927)于[总体均值](@entry_id:175446) $\mathbb{E}[X] = 1/p$。由于函数 $g(x) = 1/x$ 在 $1/p$ 处是连续的，根据[连续映射定理](@entry_id:269346)，$1/\bar{X}_n \xrightarrow{P} p$。同时，因子 $(n-1)/n$ 确定性地收敛于 1。根据[斯卢茨基定理](@entry_id:181685)（Slutsky's Theorem），整个表达式收敛于 $1 \cdot p = p$。因此，这个估计量是相合的 [@problem_id:1948414]。

相合性的一个实际意义是，我们可以通过增加样本量来控制估计误差的概率。例如，对于泊松分布，其参数 $\lambda$ 的MOME是 $\hat{\lambda}=\bar{X}$。该[估计量的方差](@entry_id:167223)为 $\text{Var}(\hat{\lambda}) = \lambda/n$。根据[切比雪夫不等式](@entry_id:269182) (Chebyshev's inequality)，$P(|\hat{\lambda} - \lambda| \ge \delta) \le \frac{\text{Var}(\hat{\lambda})}{\delta^2} = \frac{\lambda}{n\delta^2}$。为了使[估计误差](@entry_id:263890)大于给定值 $\delta$ 的概率不超过 $p_{max}$，我们只需保证 $\frac{\lambda}{n\delta^2} \le p_{max}$，从而解出所需的最小样本量 $n \ge \frac{\lambda}{p_{max}\delta^2}$。这表明，随着 $n$ 的增大，任意大小的误差范围的概率都可以被控制得任意小 [@problem_id:1948461]。

#### [渐近正态性](@entry_id:168464) (Asymptotic Normality)

除了收敛到真值外，[相合估计量](@entry_id:266642)在真值附近的波动行为也至关重要。在很普遍的条件下，矩估计量服从**渐近正态分布**。这一性质主要源于**中心极限定理 (Central Limit Theorem, CLT)**。

对于最简单的情况，如[伯努利分布](@entry_id:266933) $\text{Bernoulli}(p)$，其MOME为 $\hat{p} = \bar{X}$。中心极限定理直接表明，$\sqrt{n}(\hat{p} - p)$ 在[分布](@entry_id:182848)上收敛于一个正态分布 $N(0, \text{Var}(X))$，其中 $\text{Var}(X) = p(1-p)$。这意味着对于大的 $n$，$\hat{p}$ 的[抽样分布](@entry_id:269683)可以近似为 $\text{N}(p, \frac{p(1-p)}{n})$ [@problem_id:1948390]。这个性质是构建关于参数 $p$ 的置信区间和进行[假设检验](@entry_id:142556)的理论基础。

#### [Delta方法](@entry_id:276272)与[渐近效率](@entry_id:168529)

当矩估计量是样本矩的[非线性](@entry_id:637147)函数时，我们不能直接应用CLT。这时，**[Delta方法](@entry_id:276272)**就成为了推导其[渐近分布](@entry_id:272575)的强大工具。[Delta方法](@entry_id:276272)指出，如果一个[随机变量](@entry_id:195330)序列经过适当标准化后渐近于正态分布，那么该序列的光滑函数的[渐近分布](@entry_id:272575)也是正态的，其[方差](@entry_id:200758)可以通过原序列的[方差](@entry_id:200758)和该函数的[一阶导数](@entry_id:749425)来确定。

具体来说，如果 $\sqrt{n}(m'_k - \mu'_k) \xrightarrow{D} N(0, \sigma^2_k)$，且 $\hat{\theta} = g(m'_k)$，其中 $g$ 可微，则：
$$
\sqrt{n}(\hat{\theta}_n - \theta) \xrightarrow{D} N(0, [g'(\mu'_k)]^2 \sigma^2_k)
$$
$\hat{\theta}_n$ 的[渐近方差](@entry_id:269933)为 $\text{Asym.Var}(\hat{\theta}_n) = \frac{[g'(\mu'_k)]^2 \sigma^2_k}{n}$。

这使我们能够比较不同估计量的性能。之前提到的[拉普拉斯分布](@entry_id:266437)例子 [@problem_id:1948428] 提供了一个绝佳的平台。我们有两个估计量：$\hat{b}_1 = \bar{Y}$（其中 $Y_i=|X_i|$）和 $\hat{b}_2 = \sqrt{\bar{Z}/2}$（其中 $Z_i=X_i^2$）。
-   对于 $\hat{b}_1$，其[渐近方差](@entry_id:269933)可以直接由CLT得到，为 $\text{Asym.Var}(\hat{b}_1) = \frac{\text{Var}(|X|)}{n} = \frac{\mathbb{E}[X^2]-(\mathbb{E}[|X|])^2}{n} = \frac{2b^2 - b^2}{n} = \frac{b^2}{n}$。
-   对于 $\hat{b}_2 = g(\bar{Z}) = \sqrt{\bar{Z}/2}$，我们应用[Delta方法](@entry_id:276272)。首先 $\mathbb{E}[Z]=\mathbb{E}[X^2]=2b^2$，$\text{Var}(Z)=\mathbb{E}[X^4]-(\mathbb{E}[X^2])^2 = 24b^4 - (2b^2)^2 = 20b^4$。导数 $g'(z) = \frac{1}{2\sqrt{2z}}$ 在 $\mathbb{E}[Z]=2b^2$ 处的值为 $g'(2b^2) = \frac{1}{4b}$。因此，$\hat{b}_2$ 的[渐近方差](@entry_id:269933)为：
    $$
    \text{Asym.Var}(\hat{b}_2) = \frac{[g'(2b^2)]^2 \text{Var}(Z)}{n} = \frac{(\frac{1}{4b})^2 \cdot 20b^4}{n} = \frac{20b^4}{16b^2 n} = \frac{1.25 b^2}{n}
    $$
通过比较两个估计量的[渐近方差](@entry_id:269933)，我们可以定义它们的**[渐近相对效率](@entry_id:171033) (Asymptotic Relative Efficiency, ARE)**。$\text{ARE}(\hat{b}_2, \hat{b}_1) = \frac{\text{Asym.Var}(\hat{b}_1)}{\text{Asym.Var}(\hat{b}_2)} = \frac{b^2/n}{1.25b^2/n} = \frac{1}{1.25} = 0.8$。由于此值小于1，我们说 $\hat{b}_1$ 比 $\hat{b}_2$ 更有效率，因为它在大样本下具有更小的[方差](@entry_id:200758)。因此，在可选择的情况下，我们应优先使用 $\hat{b}_1$。

### 稳健性与实际考量

矩估计量的性质是在假定数据完全来[自指](@entry_id:153268)定[概率模型](@entry_id:265150)的前提下推导的。然而在现实世界中，数据可能受到[测量误差](@entry_id:270998)、记录错误或模型本身不完全准确等问题的影响。

考察估计量在这些非理想条件下的表现至关重要。例如，考虑一个估计[伯努利分布](@entry_id:266933)成功概率 $p$ 的场景，但[数据采集](@entry_id:273490)过程存在一个系统性错误：如果真实样本中存在至少一个“失败”（0），那么恰好有一个“失败”会被错误地记录为“成功”（1）[@problem_id:1948401]。

一个不知情的统计学家会使用观测到的数据均值 $\bar{Y}$ 作为 $p$ 的估计量。为了分析其偏差，我们需要计算 $\mathbb{E}[\bar{Y}]$。设真实样本的总和为 $S_X = \sum X_i$，观测样本的总和为 $S_Y = \sum Y_i$。根据错误规则，$S_Y = S_X + 1$ 当且仅当真实样本不全是成功时（即 $S_X \lt n$）；如果全是成功（$S_X=n$），则 $S_Y=S_X$。这可以表示为 $S_Y = S_X + I\{S_X \le n-1\} = S_X + 1 - I\{S_X=n\}$。由于 $S_X \sim \text{Binomial}(n, p)$，我们有 $\mathbb{E}[S_X] = np$ 且 $P(S_X=n)=p^n$。于是：
$$
\mathbb{E}[S_Y] = \mathbb{E}[S_X] + 1 - P(S_X=n) = np + 1 - p^n
$$
因此，估计量的期望为 $\mathbb{E}[\bar{Y}] = p + \frac{1-p^n}{n}$。其偏差为：
$$
\text{Bias}(\hat{p}_{\text{MOM}}) = \mathbb{E}[\bar{Y}] - p = \frac{1-p^n}{n}
$$
这个结果表明，即使是一个看似微小的[数据损坏](@entry_id:269966)，也会给矩估计量带来系统性的偏差。这个偏差依赖于样本量 $n$ 和真实参数 $p$。当 $n \to \infty$ 时，该偏差趋于零，说明估计量仍然是相合的。然而，在有限样本下，这种偏差可能相当显著，这警示我们在应用任何统计方法之前，都必须审慎地考虑数据的生成过程和质量。