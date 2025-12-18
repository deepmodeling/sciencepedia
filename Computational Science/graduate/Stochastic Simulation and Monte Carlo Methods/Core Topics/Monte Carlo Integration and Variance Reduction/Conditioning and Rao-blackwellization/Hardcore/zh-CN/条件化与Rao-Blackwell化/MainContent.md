## 引言
在[随机模拟](@entry_id:168869)和[统计推断](@entry_id:172747)的世界中，效率和精度是永恒的追求。[蒙特卡洛方法](@entry_id:136978)虽然通用性强，但其收敛速度往往受限于[估计量的方差](@entry_id:167223)，这意味着获得高精度结果可能需要巨大的计算代价。这引出了一个核心问题：我们能否利用问题的内在结构，设计出更“聪明”的估计量，以更少的样本获得更精确的答案？

本文旨在深入探讨解决这一问题的强大武器——基于条件化的[方差缩减技术](@entry_id:141433)，特别是著名的[Rao-Blackwell化](@entry_id:138858)方法。我们将系统性地揭示这一方法如何将[随机模拟](@entry_id:168869)中的一部分“随机性”转化为确定性的解析计算，从而在不引入偏差的前提下显著降低[统计误差](@entry_id:755391)。

在接下来的章节中，您将踏上一段从理论到实践的旅程。在“原理与机制”部分，我们将从全期望和[全方差定律](@entry_id:184705)出发，推导出[Rao-Blackwell定理](@entry_id:172242)的核心思想，并阐明其在经典统计和现代模拟中的运作机制。随后，在“应用与交叉学科联系”部分，我们将穿越统计学、机器学习、金融工程等多个领域，见证条件化思想如何被巧妙地应用于改进[MCMC算法](@entry_id:751788)、稳定随机梯度、为复杂[衍生品定价](@entry_id:144008)等前沿问题。最后，“动手实践”部分将提供一系列精心设计的问题，让您亲手实现并感受[Rao-Blackwell化](@entry_id:138858)带来的效率提升。通过本文的学习，您将掌握一种优化计算效率的深刻思维框架，并能将其应用于自己的研究和实践中。

## 原理与机制

在上一章引言的基础上，本章将深入探讨一类强大的[蒙特卡洛方差缩减](@entry_id:169974)技术的核心——以条件期望为基础的方法。我们将揭示其理论基石，即著名的[Rao-Blackwell定理](@entry_id:172242)，并展示该原理如何从经典的[参数估计](@entry_id:139349)理论自然地延伸到现代[随机模拟](@entry_id:168869)的实践中。通过系统性的阐述和一系列精心设计的实例，我们将阐明如何利用问题的内在结构，通过对部分信息进行“条件化”，来[解析性](@entry_id:140716)地消除随机性，从而以更少的计算代价获得更精确的估计。

### 条件化的核心原理：[方差缩减](@entry_id:145496)的数学基础

蒙特卡洛方法的核心思想是通过模拟[随机变量](@entry_id:195330)的样本均值来估计其期望。如果我们希望估计量 $\theta = \mathbb{E}[Z]$，一个朴素的估计量是基于 $n$ 个独立同分布的样本 $Z_1, \dots, Z_n$ 的均值 $\hat{\theta} = \frac{1}{n}\sum_{i=1}^n Z_i$。该[估计量的方差](@entry_id:167223)为 $\frac{1}{n}\mathrm{Var}(Z)$，这意味着为了将误差减半，我们需要将样本量增加四倍。[方差缩减技术](@entry_id:141433)旨在通过构造一个具有更小[方差](@entry_id:200758)的新估计量来提高效率。

条件化的思想是寻找一个辅助[随机变量](@entry_id:195330) $Y$，使得给定 $Y$ 时 $Z$ 的条件期望 $\mathbb{E}[Z \mid Y]$ 是可计算的。然后，我们用这个[条件期望](@entry_id:159140)来构造一个新的估计量。这个新估计量，我们称之为[Rao-Blackwell化](@entry_id:138858)估计量，其形式为 $\hat{\theta}_{\mathrm{RB}} = \frac{1}{n}\sum_{i=1}^n \mathbb{E}[Z_i \mid Y_i]$。要理解这一策略为何有效，我们需要依赖两个关于[条件期望](@entry_id:159140)的基本定律。

首先是**[全期望定律](@entry_id:265946) (Law of Total Expectation)**。该定律指出，对于任意可积[随机变量](@entry_id:195330) $Z$，其期望等于其[条件期望](@entry_id:159140)的期望：
$$
\mathbb{E}[Z] = \mathbb{E}[\mathbb{E}[Z \mid Y]]
$$
这一定律保证了[Rao-Blackwell化](@entry_id:138858)估计量是无偏的。对于估计量 $\hat{\theta}_{\mathrm{RB}}$ 的期望，我们有：
$$
\mathbb{E}[\hat{\theta}_{\mathrm{RB}}] = \mathbb{E}\left[\frac{1}{n}\sum_{i=1}^n \mathbb{E}[Z_i \mid Y_i]\right] = \frac{1}{n}\sum_{i=1}^n \mathbb{E}[\mathbb{E}[Z_i \mid Y_i]] = \frac{1}{n}\sum_{i=1}^n \mathbb{E}[Z_i] = \mathbb{E}[Z] = \theta
$$
因此，只要原始的[随机变量](@entry_id:195330) $Z$ 是可积的，通过条件化得到的估计量始终能正确地估计目标量 $\theta$ 。

其次，也是更关键的，是**[全方差定律](@entry_id:184705) (Law of Total Variance)**。对于任意平方可积的[随机变量](@entry_id:195330) $Z$（即 $\mathbb{E}[Z^2]  \infty$），其[方差](@entry_id:200758)可以分解为：
$$
\mathrm{Var}(Z) = \mathbb{E}[\mathrm{Var}(Z \mid Y)] + \mathrm{Var}(\mathbb{E}[Z \mid Y])
$$
这个等式的美妙之处在于它将总[方差](@entry_id:200758) $\mathrm{Var}(Z)$ 分解为两个非负部分：
1.  $\mathrm{Var}(\mathbb{E}[Z \mid Y])$：这是条件期望 $\mathbb{E}[Z \mid Y]$ 本身的[方差](@entry_id:200758)。它代表了由于辅助信息 $Y$ 的变动而引起的 $Z$ 均值的变动。这正是我们[Rao-Blackwell化](@entry_id:138858)估计量单样本的[方差](@entry_id:200758)。
2.  $\mathbb{E}[\mathrm{Var}(Z \mid Y)]$：这是[条件方差](@entry_id:183803) $\mathrm{Var}(Z \mid Y) = \mathbb{E}[(Z - \mathbb{E}[Z \mid Y])^2 \mid Y]$ 的期望。它代表了在给定信息 $Y$ 之后，$Z$ 仍然存留的“残余”[方差](@entry_id:200758)的平均大小。

由于 $\mathbb{E}[\mathrm{Var}(Z \mid Y)] \ge 0$，[全方差定律](@entry_id:184705)直接导出了一个至关重要的不等式：
$$
\mathrm{Var}(\mathbb{E}[Z \mid Y]) \le \mathrm{Var}(Z)
$$
这就是**[Rao-Blackwell定理](@entry_id:172242)**的核心结论：对一个估计量取其关于某个辅助信息的[条件期望](@entry_id:159140)，所得到的新[估计量的方差](@entry_id:167223)不会超过原[估计量的方差](@entry_id:167223)。我们通过条件化，“平均掉”了残余[方差](@entry_id:200758)，从而实现了[方差缩减](@entry_id:145496)。

[方差](@entry_id:200758)的缩减量恰好是 $\mathbb{E}[\mathrm{Var}(Z \mid Y)]$。这意味着，[方差缩减](@entry_id:145496)是严格的（即不等式严格成立），除非 $\mathbb{E}[\mathrm{Var}(Z \mid Y)] = 0$。这种情况仅当 $\mathrm{Var}(Z \mid Y)$ 几乎处处为零时发生，这等价于 $Z$ 本身是 $Y$ 的一个函数，即 $Z$ 是 $\sigma(Y)$-可测的。换言之，只要 $Y$ 不能完全确定 $Z$，条件化就能严格地降低[方差](@entry_id:200758) 。

### 在[统计估计](@entry_id:270031)中的应用：[UMVUE](@entry_id:169429)

[Rao-Blackwell定理](@entry_id:172242)在[数理统计](@entry_id:170687)的参数估计理论中扮演着基础性角色，尤其是在寻找**[一致最小方差无偏估计量](@entry_id:166888) (Uniformly Minimum-Variance Unbiased Estimator, [UMVUE](@entry_id:169429))** 的过程中。

在[统计模型](@entry_id:165873)中，**充分统计量 (sufficient statistic)** $T(\mathbf{X})$ 是一个函数，它包含了样本 $\mathbf{X}$ 中关于未知参数 $\theta$ 的所有信息。根据Fisher-Neyman[因子分解定理](@entry_id:749213)，这意味着样本的联合概率密度（或质量）函数可以分解为两部分，一部分仅依赖于 $T(\mathbf{X})$ 和 $\theta$，另一部分不依赖于 $\theta$。直观上，一旦我们知道了充分统计量 $T$ 的值，原始样本 $\mathbf{X}$ 的其余信息对于推断 $\theta$ 而言是多余的。

这为[Rao-Blackwell化](@entry_id:138858)提供了一个天然的途径。如果我们有一个对目标函数 $\tau(\theta)$ 的任意[无偏估计量](@entry_id:756290) $\delta(\mathbf{X})$，但它不是 $T$ 的函数，那么我们可以通过条件化来改进它。构造新的估计量 $\delta^*(T) = \mathbb{E}[\delta(\mathbf{X}) \mid T(\mathbf{X})]$。根据[Rao-Blackwell定理](@entry_id:172242)，$\delta^*(T)$ 仍然是无偏的，且其[方差](@entry_id:200758)不大于 $\delta(\mathbf{X})$。由于 $\delta^*$ 仅依赖于充分统计量 $T$，它通常是一个更优的估计量。

更进一步，如果一个充分统计量 $T$ 是**完备的 (complete)**，这意味着唯一一个期望为零的 $T$ 的函数是零函数本身。**[Lehmann-Scheffé定理](@entry_id:163798)**指出，如果 $T$ 是一个完备充分统计量，那么任何基于 $T$ 的[无偏估计量](@entry_id:756290)都是唯一的[UMVUE](@entry_id:169429)。

这套理论提供了一个寻找[最优估计量](@entry_id:176428)的系统性方法：
1.  找到参数的完备充分统计量 $T$。
2.  找到[目标函数](@entry_id:267263) $\tau(\theta)$ 的任何一个简单的[无偏估计量](@entry_id:756290) $\delta(\mathbf{X})$。
3.  计算条件期望 $\delta^*(T) = \mathbb{E}[\delta(\mathbf{X}) \mid T]$。这个结果就是[UMVUE](@entry_id:169429)。

让我们通过一个经典的例子来说明这个过程。假设 $X_1, \dots, X_n$ 是来自参数为 $\lambda$ 的泊松分布的[独立同分布](@entry_id:169067)样本。我们的目标是估计 $\tau(\lambda) = \exp(-c\lambda)$，其中 $c$ 是一个 $1 \le c \le n$ 的整数。
首先，样本的和 $T = \sum_{i=1}^n X_i$ 是 $\lambda$ 的完备充分统计量。
接下来，我们需要一个简单的[无偏估计量](@entry_id:756290)。注意到 $P(X_i=0) = \exp(-\lambda)$，我们可以构造一个[无偏估计量](@entry_id:756290) $\delta(\mathbf{X}) = \mathbf{1}\{X_1=0, \dots, X_c=0\}$，其期望为 $\mathbb{E}[\delta(\mathbf{X})] = (\exp(-\lambda))^c = \tau(\lambda)$。
最后，我们应用[Rao-Blackwell化](@entry_id:138858)，计算 $\mathbb{E}[\delta(\mathbf{X}) \mid T=t]$:
$$
\mathbb{E}[\mathbf{1}\{X_1=0, \dots, X_c=0\} \mid \sum_{i=1}^n X_i = t] = P(X_1=0, \dots, X_c=0 \mid \sum_{i=1}^n X_i = t)
$$
通过计算[条件概率](@entry_id:151013)，可以得到一个看似神奇但完全由第一性原理导出的结果  ：
$$
\hat{\tau}_{\mathrm{UMVUE}}(T) = \left(1 - \frac{c}{n}\right)^T
$$
这个估计量是 $T$ 的函数，无偏，并且根据[Lehmann-Scheffé定理](@entry_id:163798)，它在所有[无偏估计量](@entry_id:756290)中具有最小[方差](@entry_id:200758)。这个例子有力地展示了条件化如何将一个粗糙的、依赖于特定样本[排列](@entry_id:136432)的估计量（指示函数）提炼成一个光滑的、仅依赖于充分信息的、最优的估计量。

同样的方法可以应用于其他[分布](@entry_id:182848)族。例如，对于均值为 $\theta$ 的指数分布，其[UMVUE](@entry_id:169429)是样本均值 $\bar{X}$ 。对于在 $[\theta, \theta+1]$ 上的[均匀分布](@entry_id:194597)，其参数 $\theta$ 的[UMVUE](@entry_id:169429)可以被推导为 $\frac{X_{(1)}+X_{(n)}}{2}-\frac{1}{2}$，其中 $X_{(1)}$ 和 $X_{(n)}$ 分别是样本的最小值和最大值 。这些例子都体现了通过对充分统计量进行条件化来达到最优估计的思想。

### 在[蒙特卡洛模拟](@entry_id:193493)中的应用

虽然[Rao-Blackwell化](@entry_id:138858)植根于[经典统计学](@entry_id:150683)，但它在现代[蒙特卡洛模拟](@entry_id:193493)中作为一种[方差缩减技术](@entry_id:141433)同样大放异彩。其应用逻辑非常直接：在模拟过程中，如果我们能将目标函数 $g(X)$ 的一部分期望解析地计算出来，就应当这么做。

具体而言，我们寻找一个可以在模拟中轻易生成的辅助变量 $Y$，并且[条件期望](@entry_id:159140) $\mathbb{E}[g(X) \mid Y]$ 具有已知的解析表达式或易于计算。我们的模拟策略便从“生成 $X$，计算 $g(X)$”转变为“生成 $Y$，计算 $h(Y) = \mathbb{E}[g(X) \mid Y]$”。由于 $\mathrm{Var}(h(Y)) \le \mathrm{Var}(g(X))$，新策略下的估计量将具有更小的[方差](@entry_id:200758)。

考虑一个分层模型 ：首先从 $X \sim \mathrm{Gamma}(k, \theta)$ 中抽取样本，然后给定 $X$，从 $Y \mid X \sim \mathrm{Poisson}(\lambda X)$ 中抽取样本。我们要估计 $\mu = \mathbb{E}[Y + aX]$。
-   **朴素估计量**: 模拟 $n$ 对 $(X_i, Y_i)$，计算 $\hat{\mu}_{\mathrm{naive}} = \frac{1}{n} \sum (Y_i + aX_i)$。
-   **[Rao-Blackwell化](@entry_id:138858)估计量**: 仅模拟 $n$ 个 $X_i$，然后计算条件期望 $\mathbb{E}[Y_i + aX_i \mid X_i]$。由于 $\mathbb{E}[Y_i \mid X_i] = \lambda X_i$，这个[条件期望](@entry_id:159140)是 $(\lambda+a)X_i$。新估计量为 $\hat{\mu}_{\mathrm{RB}} = \frac{1}{n} \sum (\lambda+a)X_i$。

通过[全方差定律](@entry_id:184705)，我们可以精确计算两种[估计量的方差](@entry_id:167223)。$\mathrm{Var}(Y+aX) = \mathbb{E}[\mathrm{Var}(Y+aX|X)] + \mathrm{Var}(\mathbb{E}[Y+aX|X])$。其中，$\mathrm{Var}(\mathbb{E}[Y+aX|X])$ 是[Rao-Blackwell化](@entry_id:138858)[估计量的方差](@entry_id:167223)，而 $\mathbb{E}[\mathrm{Var}(Y+aX|X)]$ 是[方差缩减](@entry_id:145496)量。经过计算，我们发现[方差比](@entry_id:162608)率为：
$$
\frac{\mathrm{Var}(\hat{\mu}_{\mathrm{naive}})}{\mathrm{Var}(\hat{\mu}_{\mathrm{RB}})} = 1 + \frac{\lambda}{(\lambda + a)^2 \theta}
$$
这个表达式定量地显示了[方差缩减](@entry_id:145496)的效果，并且表明效果依赖于模型参数。当 $a = -\lambda$ 时，[Rao-Blackwell化](@entry_id:138858)[估计量的方差](@entry_id:167223)为零，实现了无穷大的[方差缩减](@entry_id:145496)，因为此时估计的目标变成了 $\mathbb{E}[Y-\lambda X]=0$。

这种技术在金融衍生品定价等领域尤为重要。例如，在为连续监控的[障碍期权](@entry_id:264959)定价时，我们需要判断标的资产价格的路径是否在离散的时间步之间触及了障碍。一种朴素的方法是模拟路径上的多个中间点来检查穿越。一个更优的[Rao-Blackwell化](@entry_id:138858)方法是，只模拟时间步的两个端点，然后利用已知的[布朗桥](@entry_id:265208)（Brownian bridge）在给定端点条件下穿越某个水平线的解析概率公式。用这个解析概率代替随机的指示函数，可以在保持无偏性的同时，极大地降低[方差](@entry_id:200758) 。

值得注意的是，[Rao-Blackwell化](@entry_id:138858)并非总是“免费的午餐”。计算条件期望 $\mathbb{E}[g(X) \mid Y]$ 的成本可能高于直接计算 $g(X)$。在某些情况下，这个[条件期望](@entry_id:159140)可能没有[闭式](@entry_id:271343)解，需要通过数值积分甚至嵌套的蒙特卡洛模拟来估计，这可能会显著增加每次迭代的计算成本。因此，该技术的有效性取决于[方差缩减](@entry_id:145496)带来的收益是否能超过可能增加的单次样本计算成本。一个成功的应用通常意味着[方差缩减](@entry_id:145496)的幅度足以弥补（甚至超越）计算成本的增加 。

此外，我们不必对所有可用的信息进行条件化。有时，“部分[Rao-Blackwell化](@entry_id:138858)”是一种实用策略。例如，在一个分层混合模型中，我们可能只对层[指示变量](@entry_id:266428) $S$ 进行条件化，而不是对整个[随机变量](@entry_id:195330) $X$。即使只利用了部分信息，只要条件期望是可计算的，我们仍然可以获得[方差缩减](@entry_id:145496) 。

### 与其他统计概念的联系

Rao-Blackwell原理的美妙之处在于它与其他核心统计思想的深刻联系，这进一步揭示了其普遍性。

#### 贝叶斯推断中的应用

在[贝叶斯分析](@entry_id:271788)中，我们常常关心[后验预测分布](@entry_id:167931)的性质。例如，给定数据 $y_{1:n}$，一个新观测值 $Y_{\mathrm{new}}$ 的后验预测[方差](@entry_id:200758) $\mathbb{V}(Y_{\mathrm{new}} \mid y_{1:n})$ 是一个关键量。[全方差定律](@entry_id:184705)提供了一个优雅的分解 ：
$$
\mathbb{V}(Y_{\mathrm{new}} \mid y_{1:n}) = \mathbb{E}_{\theta|y_{1:n}}[\mathbb{V}(Y_{\mathrm{new}} \mid \theta)] + \mathbb{V}_{\theta|y_{1:n}}[\mathbb{E}(Y_{\mathrm{new}} \mid \theta)]
$$
这个分解极具启发性。第一项 $\mathbb{E}_{\theta|y_{1:n}}[\mathbb{V}(Y_{\mathrm{new}} \mid \theta)]$ 是给定参数 $\theta$ 时观测噪声[方差](@entry_id:200758)的后验期望，代表了模型固有的、不可约的**[偶然不确定性](@entry_id:154011) (aleatoric uncertainty)**。第二项 $\mathbb{V}_{\theta|y_{1:n}}[\mathbb{E}(Y_{\mathrm{new}} \mid \theta)]$ 是模型均值（由 $\theta$ 决定）的后验[方差](@entry_id:200758)，代表了由于我们对参数 $\theta$ 不完全了解而产生的**认知不确定性 (epistemic uncertainty)**。

在贝叶斯蒙特卡洛（例如MCMC）中，如果我们想估计后验预测[方差](@entry_id:200758)，朴素的方法是：(1) 从[后验分布](@entry_id:145605) $p(\theta|y_{1:n})$ 中抽取样本 $\theta^{(j)}$；(2) 对每个 $\theta^{(j)}$，从 $p(y_{\mathrm{new}}|\theta^{(j)})$ 中抽取样本 $y_{\mathrm{new}}^{(j)}$；(3) 计算 $\{y_{\mathrm{new}}^{(j)}\}$ 的样本[方差](@entry_id:200758)。这个过程引入了两个层面的随机性。

[Rao-Blackwell化](@entry_id:138858)在此处的应用是，如果 $\mathbb{V}(Y_{\mathrm{new}} \mid \theta)$ 和 $\mathbb{E}(Y_{\mathrm{new}} \mid \theta)$ 有解析形式（在共轭模型中通常如此），我们就不需要模拟 $Y_{\mathrm{new}}$。我们可以只从后验中抽取 $\theta^{(j)}$，然后用这些样本来估计分解式中的两项。例如，在[正态-正态模型](@entry_id:267798)中，$\mathbb{V}(Y_{\mathrm{new}} \mid \theta) = \sigma^2$ 是一个常数，而 $\mathbb{E}(Y_{\mathrm{new}} \mid \theta) = \theta$。因此，$\mathbb{V}(Y_{\mathrm{new}} \mid y_{1:n}) = \sigma^2 + \mathbb{V}(\theta \mid y_{1:n})$。我们可以用 $\theta$ 的后验样本[方差](@entry_id:200758)来估计第二项，从而消除了模拟 $Y_{\mathrm{new}}$ 所带来的额外变异。

#### 与控制变量法的关系

[Rao-Blackwell化](@entry_id:138858)可以被看作是**[控制变量](@entry_id:137239)法 (control variates)** 的一种特殊且理想化的形式。[控制变量](@entry_id:137239)法的思想是，为了估计 $\mathbb{E}[X]$，我们找到一个均值为零的[随机变量](@entry_id:195330) $C$（[控制变量](@entry_id:137239)），它与 $X$ 相关。然后我们估计 $\mathbb{E}[X - \beta C] = \mathbb{E}[X]$，通过选择最优的系数 $\beta$ 来最小化 $\mathrm{Var}(X - \beta C)$。

现在考虑Rao-Blackwell估计量 $\mathbb{E}[X \mid Z]$。我们可以将原始估计量 $X$ 写成：
$$
X = \mathbb{E}[X \mid Z] + (X - \mathbb{E}[X \mid Z])
$$
令 $C = X - \mathbb{E}[X \mid Z]$。显然 $\mathbb{E}[C] = 0$，所以 $C$ 是一个有效的控制变量。Rao-Blackwell估计量 $\mathbb{E}[X \mid Z]$ 等价于用 $X$ 减去这个“完美”的[控制变量](@entry_id:137239)。这里的“完美”体现在它移除了所有在给定 $Z$ 后仍然存在的[方差](@entry_id:200758)。

在一个具体的例子中，比如估计 $\mathbb{E}[\exp(aZ+bW)]$，其中 $Z, W$ 是独立标准正态变量，我们可以比较两种方法 ：
1.  [Rao-Blackwell化](@entry_id:138858)：条件化于 $Z$，使用估计量 $\mathbb{E}[\exp(aZ+bW) \mid Z] = \exp(aZ + b^2/2)$。
2.  [控制变量](@entry_id:137239)法：使用 $Y=Z$ 作为[控制变量](@entry_id:137239)（$\mathbb{E}[Y]=0$），找到最优的 $\beta^*$ 来最小化 $\mathrm{Var}(\exp(aZ+bW) - \beta Z)$。

通过计算可以发现，这两种方法得到的[方差](@entry_id:200758)是不同的。[Rao-Blackwell化](@entry_id:138858)通常更有效，因为它利用了模型结构的更多信息。然而，当 $\mathbb{E}[X \mid Z]$ 难以计算时，使用一个简单的、相关的[控制变量](@entry_id:137239)（如 $Z$ 本身）可能是一个更实际的选择。

#### 总结：没有万能的方法

最后，必须强调[Rao-Blackwell化](@entry_id:138858)是[方差缩减](@entry_id:145496)工具箱中的一种强大工具，但并非总是最优选择。其他方法，如对偶变量法 (antithetic variates) 或[重要性采样](@entry_id:145704)，可能在特定问题上表现更佳。

考虑一个估计 $\mathbb{E}[\exp(aX+bY)]$ 的例子，其中 $(X,Y)$ 是相关的标准正态变量。我们可以比较三种方法的预算[标准化](@entry_id:637219)[方差](@entry_id:200758) ：
-   **朴素法**: $\mathbb{V}_N = \exp(2S) - \exp(S)$
-   **Rao-Blackwell法** (条件化于 $X$): $\mathbb{V}_{RB} = \exp(2a^2+b^2+4ab\rho+b^2\rho^2) - \exp(S)$
-   **对偶变量法** (使用 $(-X,-Y)$): $\mathbb{V}_{AV} = \exp(2S) - 2\exp(S) + 1$
其中 $S = a^2+b^2+2ab\rho$。

哪种方法最优取决于参数 $a, b, \rho$ 的具体值。例如，如果 $b=0$，[Rao-Blackwell化](@entry_id:138858)估计量就变成了 $\exp(aX)$，其[方差](@entry_id:200758)为 $\exp(2a^2) - \exp(a^2)$，这与朴素[估计量的方差](@entry_id:167223)完全相同，因为此时 $Y$ 无关，条件化没有带来任何信息。对偶变量法在函数关于原点近似对称时表现良好。因此，方法的选择需要对问题的结构有深刻的理解。[Rao-Blackwell化](@entry_id:138858)的威力在于，当一个问题可以分解为一个解析可解的[部分和](@entry_id:162077)一个随机部分时，它提供了一种系统性地消除部分随机性的方法，从而通向更高效的模拟。