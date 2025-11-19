## 引言
在贝叶斯统计的宏伟蓝图中，模型选择是一个核心挑战，其关键在于量化每个模型对观测数据的解释能力。这一量化指标被称为“[边际似然](@entry_id:636856)”或“[模型证据](@entry_id:636856)”。然而，计算[边际似然](@entry_id:636856)通常需要求解一个棘手的[高维积分](@entry_id:143557)，这构成了[贝叶斯模型比较](@entry_id:637692)中的一个主要计算瓶颈。尽管[马尔可夫链蒙特卡洛](@entry_id:138779)（MCMC）方法在参数后验推断中取得了巨大成功，但它们本身并不能直接提供[边际似然](@entry_id:636856)的值。

为了填补这一空白，Siddhartha Chib (1995) 提出了一种独创性的方法，巧妙地利用 MCMC 采样器的输出，将困难的积分问题转化为一个更易于处理的[密度估计](@entry_id:634063)问题。本文旨在全面解析 Chib 方法，为读者提供从理论到实践的完整指南。

文章将分为三个核心部分展开。在“原理与机制”一章中，我们将深入剖析该方法赖以成立的基本恒等式，并阐明其在[吉布斯采样](@entry_id:139152)等框架下的实现细节。接下来，在“应用与跨学科联系”一章中，我们将探讨 Chib 方法在处理各类复杂[统计模型](@entry_id:165873)时的实际应用、高级策略及其与其他计算方法的比较与联系。最后，“动手实践”部分将提供具体的编程练习，引导读者从零开始实现 Chib 方法，解决从简单的共轭模型到复杂的[回归分析](@entry_id:165476)等真实问题。通过这一结构化的学习路径，您将不仅理解 Chib 方法的“为何”，更将掌握其“如何”应用。

## 原理与机制

在贝叶斯统计中，模型的[边际似然](@entry_id:636856)（marginal likelihood），或称为[模型证据](@entry_id:636856)（model evidence），是[模型比较](@entry_id:266577)与选择的核心。Chib (1995) 提出的方法是一种基于[吉布斯采样](@entry_id:139152)（Gibbs sampler）输出，用以估计[边际似然](@entry_id:636856)的独创性方法，后续被推广至包括 Metropolis-Hastings 在内的更一般的马尔可夫链蒙特卡洛（MCMC）算法。本章旨在深入阐述 Chib 方法的统计学原理与实现机制，从其赖以成立的基本恒等式出发，逐步探讨其在不同模型情境下的具体应用、实践中的关键考量以及针对复杂情况的扩展。

### 基本恒等式：从贝叶斯定理到[边际似然估计](@entry_id:751675)

在[贝叶斯推断](@entry_id:146958)的框架下，参数 $\theta$ 的[后验分布](@entry_id:145605)、似然函数与[先验分布](@entry_id:141376)通过[贝叶斯定理](@entry_id:151040)联系在一起：

$$ p(\theta \mid y) = \frac{p(y \mid \theta) p(\theta)}{p(y)} $$

其中，$y$ 代表观测数据，$p(y \mid \theta)$ 是[似然函数](@entry_id:141927)，$p(\theta)$ 是[先验分布](@entry_id:141376)。分母 $p(y)$ 是[边际似然](@entry_id:636856)，通过对[联合分布](@entry_id:263960) $p(y, \theta)$ 在整个参数空间上积分得到：

$$ p(y) = \int p(y \mid \theta) p(\theta) \, d\theta $$

[边际似然](@entry_id:636856) $p(y)$ 扮演着双重角色。在单一模型的[参数推断](@entry_id:753157)中，它是一个归一化常数，确保[后验分布](@entry_id:145605) $p(\theta \mid y)$ 的积分为 1。对于依赖于[后验分布](@entry_id:145605)比率的 MCMC 算法（如 Metropolis-Hastings），$p(y)$ 的具体数值无关紧要，因为它会在计算中被抵消。然而，在[模型比较](@entry_id:266577)的场景中，$p(y)$ 的角色发生了根本性转变。它不再是无足轻重的常数，而是成为了衡量模型 $\mathcal{M}$ 优劣的核心指标，即“[模型证据](@entry_id:636856)” $p(y \mid \mathcal{M})$。[@problem_id:3294562]

[贝叶斯因子](@entry_id:143567)（Bayes factor）是比较两个竞争模型 $\mathcal{M}_1$ 和 $\mathcal{M}_2$ 的标准工具，其定义为两者[边际似然](@entry_id:636856)的比值：

$$ BF_{12} = \frac{p(y \mid \mathcal{M}_1)}{p(y \mid \mathcal{M}_2)} $$

[边际似然](@entry_id:636856) $p(y \mid \mathcal{M})$ 是一个先验预测量（prior predictive quantity），它表示在观测到数据之前，模型 $\mathcal{M}$ 对当前数据的预测能力，是在模型所有参数可能性上（由先验分布加权）的平均。一个能够以高先验概率预测出观测数据的模型将被赋予更高的证据值。这种平均化过程天然地惩罚了过于复杂的模型。一个参数空间巨大、先验弥散的模型（即过于灵活的模型）虽然可能对某些特定参数值能极好地拟合数据，但其[先验概率](@entry_id:275634)质量被分散在广阔的[参数空间](@entry_id:178581)中，其中大部分区域对应的参数值并不能很好地预测数据。积分过程会惩罚这种“浪费”的先验概率，从而体现出一种内在的奥卡姆剃刀（Occam's razor）原则，偏好那些在参数先验信念范围内能稳定给出合理解释的、更简洁的模型。因此，基于[贝叶斯因子](@entry_id:143567)的模型选择与基于[后验分布](@entry_id:145605) $p(\theta \mid y, \mathcal{M})$ 的[参数推断](@entry_id:753157)有着本质的区别。[@problem_id:3294520]

Chib 方法的巧妙之处在于，它完全避开了对[高维积分](@entry_id:143557) $p(y) = \int p(y \mid \theta) p(\theta) \, d\theta$ 的直接计算，而是通过重新整理贝叶斯定理的基本形式来求解 $p(y)$。上述贝叶斯定理恒等式对于[参数空间](@entry_id:178581)中任意一点 $\theta$ 都成立。因此，我们可以选择任意一个特定的点 $\theta^\star$，并得到：

$$ p(y) = \frac{p(y \mid \theta^\star) p(\theta^\star)}{p(\theta^\star \mid y)} $$

这就是 Chib 方法的核心恒等式，常被称为“候选者公式”（candidate's formula）。在对数尺度上，它表现为一个简单的加减法：

$$ \log p(y) = \log p(y \mid \theta^\star) + \log p(\theta^\star) - \log p(\theta^\star \mid y) $$

这个公式优雅地将一个困难的积分问题转化为了一个在特定点上进行函数求值的问题。公式右边的三项中，$\log p(y \mid \theta^\star)$（在 $\theta^\star$ 处的[对数似然](@entry_id:273783)）和 $\log p(\theta^\star)$（在 $\theta^\star$ 处的对数先验）通常是已知的，可以直接计算。唯一的挑战在于估计第三项，即在 $\theta^\star$ 处的对数后验纵坐标（log posterior ordinate）$\log p(\theta^\star \mid y)$。[@problem_id:3294572]

### 原理验证：一个共轭模型的例子

为了建立对上述恒等式的直观理解，我们考察一个简单的共轭高斯模型。假设我们有单个观测值 $y$，其[似然函数](@entry_id:141927)为正态分布 $y \mid \theta \sim \mathcal{N}(\theta, \sigma^2)$，参数 $\theta$ 的[先验分布](@entry_id:141376)也为正态分布 $\theta \sim \mathcal{N}(\mu_0, \tau_0^2)$，其中 $\sigma^2, \mu_0, \tau_0^2$ 均为已知常数。

对于这个模型，[边际似然](@entry_id:636856) $p(y)$ 可以通过直接积分解析求出。$y$ 可以看作是 $\theta$ 和一个独立噪声 $\epsilon \sim \mathcal{N}(0, \sigma^2)$ 的和，即 $y = \theta + \epsilon$。由于 $\theta$ 和 $\epsilon$ 是两个独立的正态[随机变量](@entry_id:195330)，它们的和 $y$ 也服从[正态分布](@entry_id:154414)，其均值为 $\mathbb{E}[y] = \mathbb{E}[\theta] + \mathbb{E}[\epsilon] = \mu_0 + 0 = \mu_0$，[方差](@entry_id:200758)为 $\text{Var}(y) = \text{Var}(\theta) + \text{Var}(\epsilon) = \tau_0^2 + \sigma^2$。因此，[边际似然](@entry_id:636856)的 closed-form 解为：

$$ p(y) = \frac{1}{\sqrt{2\pi(\sigma^2 + \tau_0^2)}} \exp\left(-\frac{(y - \mu_0)^2}{2(\sigma^2 + \tau_0^2)}\right) $$

这是一个 $\mathcal{N}(\mu_0, \sigma^2 + \tau_0^2)$ [分布](@entry_id:182848)的[概率密度函数](@entry_id:140610)。

现在，我们来验证 Chib 方法的恒等式。在这个共轭模型中，后验分布 $p(\theta \mid y)$ 也是[正态分布](@entry_id:154414)，其形式为 $\mathcal{N}(\mu_1, \tau_1^2)$，其中[后验均值](@entry_id:173826)和[方差](@entry_id:200758)分别为：
$$ \mu_1 = \frac{y\tau_0^2 + \mu_0\sigma^2}{\sigma^2 + \tau_0^2}, \quad \tau_1^2 = \frac{\sigma^2 \tau_0^2}{\sigma^2 + \tau_0^2} $$

根据恒等式 $p(y) = \frac{p(y \mid \theta) p(\theta)}{p(\theta \mid y)}$，无论我们选择哪个 $\theta$ 值，这个等式都应该成立。我们可以代入似然、先验和后验的正[态密度](@entry_id:147894)函数，并通过代数运算验证该比值确实等于我们通过积分得到的 $p(y)$，并且与所选的 $\theta$ 无关。

这个解析可解的例子为 Chib 方法提供了原理上的完美证明。它表明，[边际似然](@entry_id:636856) $p(y)$ 确实是连接联合密度 $p(y, \theta)$ 与后验密度 $p(\theta \mid y)$ 的那个唯一的归一化常数。对于那些无法解析积分的非共轭模型，Chib 方法提供了一种通过 MCMC 模拟来数值上求解这个常数的途径。[@problem_id:3294504]

### 实现机制：估计后验纵坐标

Chib 方法的实际可行性取决于我们能否利用 MCMC 的输出样本来可靠地估计后验纵坐标 $p(\theta^\star \mid y)$。MCMC 算法（如[吉布斯采样](@entry_id:139152)或 Metropolis-Hastings）的遍历性（ergodicity）保证了从 MCMC 链中抽取的样本可以用来一致地估计关于后验分布的各种量，其中就包括在某一点的密度值。[@problem_id:3294572]

#### [吉布斯采样](@entry_id:139152)下的实现

Chib (1995) 的原始论文详细阐述了如何在[吉布斯采样](@entry_id:139152)的框架下估计后验纵坐标。假设参数向量 $\theta$ 被划分为 $B$ 个区块，$\theta = (\theta_1, \theta_2, \dots, \theta_B)$，[吉布斯采样器](@entry_id:265671)通过依次从全条件[后验分布](@entry_id:145605)（full conditional posteriors）$p(\theta_i \mid \theta_{-i}, y)$ 中抽样来更新参数。

利用概率论中的链式法则，我们可以将后验纵坐标分解为一系列条件密度的乘积。为了简化说明，我们考虑最常见的两区块情况 $\theta = (\theta_1, \theta_2)$。此时，在点 $\theta^\star = (\theta_1^\star, \theta_2^\star)$ 处的后验纵坐标可以分解为：

$$ p(\theta_1^\star, \theta_2^\star \mid y) = p(\theta_1^\star \mid y) \, p(\theta_2^\star \mid \theta_1^\star, y) $$

这个分解将估计一个联合密度的问题转化为了估计两个（边际和条件）密度的问题。

1.  **估计 $p(\theta_2^\star \mid \theta_1^\star, y)$**：这一项是 $\theta_2$ 的全条件后验密度在 $\theta_2^\star$ 处的值，其条件是 $\theta_1$ 固定在 $\theta_1^\star$。在[吉布斯采样](@entry_id:139152)中，全条件后验的函数形式是已知的。因此，这一项可以直接计算出来，无需估计。

2.  **估计 $p(\theta_1^\star \mid y)$**：这一项是 $\theta_1$ 的边际后验密度在 $\theta_1^\star$ 处的值。这个密度通常没有 closed-form 表达式，但我们可以通过一个巧妙的积分恒等式来估计它：
    $$ p(\theta_1^\star \mid y) = \int p(\theta_1^\star, \theta_2 \mid y) \, d\theta_2 = \int p(\theta_1^\star \mid \theta_2, y) p(\theta_2 \mid y) \, d\theta_2 $$
    这个积分可以看作是全条件密度 $p(\theta_1^\star \mid \theta_2, y)$ 在 $\theta_2$ 的边际后验分布 $p(\theta_2 \mid y)$下的[期望值](@entry_id:153208)。根据[大数定律](@entry_id:140915)，我们可以用 MCMC 样本来近似这个期望。假设我们已经通过[吉布斯采样](@entry_id:139152)得到了 $M$ 个来自后验分布 $p(\theta_1, \theta_2 \mid y)$ 的样本 $\{(\theta_1^{(m)}, \theta_2^{(m)})\}_{m=1}^M$。那么，我们可以用这些样本中的 $\theta_2$ 部分来估计 $p(\theta_1^\star \mid y)$：
    $$ \hat{p}(\theta_1^\star \mid y) = \frac{1}{M} \sum_{m=1}^{M} p(\theta_1^\star \mid \theta_2^{(m)}, y) $$
    这里的 $p(\theta_1^\star \mid \theta_2^{(m)}, y)$ 是 $\theta_1$ 的全条件后验密度函数，其形式已知，我们只需将 MCMC 迭代得到的 $\theta_2^{(m)}$ 和我们选定的点 $\theta_1^\star$ 代入即可。这种利用已知条件密度函数来降低[蒙特卡洛估计](@entry_id:637986)[方差](@entry_id:200758)的方法，是一种 Rao-Blackwellization。

将这两部分结合起来，后验纵坐标的估计值为：

$$ \hat{p}(\theta^\star \mid y) = \left( \frac{1}{M} \sum_{m=1}^{M} p(\theta_1^\star \mid \theta_2^{(m)}, y) \right) \cdot p(\theta_2^\star \mid \theta_1^\star, y) $$

这个过程可以推广到任意 $B$ 个区块的情况。后验纵坐标被分解为 $B$ 个条件密度的乘积，其中一个可以直接计算，另外 $B-1$ 个需要通过对 MCMC 输出进行 Rao-Blackwellized 平均来估计。

**示例：[贝叶斯线性回归](@entry_id:634286)**

让我们通过一个[贝叶斯线性回归](@entry_id:634286)模型来具体说明。模型设定如下：
- 似然: $y \mid \beta, \sigma^2 \sim \mathcal{N}(X\beta, \sigma^2 I_n)$
- 先验: $\beta \mid \sigma^2 \sim \mathcal{N}(m_0, \sigma^2 S_0)$ and $\sigma^2 \sim \text{Inverse-Gamma}(a_0, b_0)$

这是一个典型的两区块 $(\beta, \sigma^2)$ [吉布斯采样](@entry_id:139152)问题。其全条件后验分布分别为：
- $p(\beta \mid \sigma^2, y) \sim \mathcal{N}(m_n, \sigma^2 S_n)$
- $p(\sigma^2 \mid \beta, y) \sim \text{Inverse-Gamma}(a_n, b_n)$
其中 $m_n, S_n, a_n, b_n$ 是由数据和先验超参数决定的已知量。

为了在点 $\theta^\star = (\beta^\star, \sigma^{2\star})$ 处估计后验纵坐标 $p(\beta^\star, \sigma^{2\star} \mid y)$，我们使用分解：
$$ p(\beta^\star, \sigma^{2\star} \mid y) = p(\sigma^{2\star} \mid y) \, p(\beta^\star \mid \sigma^{2\star}, y) $$
注意这里的分解顺序与之前的泛型例子不同，但原理相同。
1.  $p(\beta^\star \mid \sigma^{2\star}, y)$ 是 $\beta$ 的全条件后验，给定 $\sigma^2 = \sigma^{2\star}$，可以直接计算其在 $\beta^\star$ 处的密度值。
2.  $p(\sigma^{2\star} \mid y)$ 是 $\sigma^2$ 的边际后验，需要通过对[吉布斯采样](@entry_id:139152)输出的 $\beta$ 样本进行 Rao-Blackwellized 平均来估计：
    $$ \hat{p}(\sigma^{2\star} \mid y) = \frac{1}{M} \sum_{m=1}^{M} p(\sigma^{2\star} \mid \beta^{(m)}, y) $$
    其中 $p(\sigma^{2\star} \mid \beta^{(m)}, y)$ 是 $\sigma^2$ 的全条件后验（一个逆伽玛[分布](@entry_id:182848)）在 $\sigma^{2\star}$ 处的值，其参数依赖于第 $m$ 次迭代的 $\beta^{(m)}$。
    
通过这种方式，我们可以得到对 $\log p(\theta^\star|y)$ 的估计，并最终计算出 $\log \hat{p}(y)$。[@problem_id:3294515]

### 实践考量与方法细节

虽然 Chib 方法原理清晰，但其在实践中的成功应用依赖于对几个关键细节的审慎处理。

#### $\theta^\star$ 的选择

理论上，Chib 方法的恒等式对任意 $\theta^\star$ 都成立。然而在实践中，$\theta^\star$ 的选择对估计的[数值稳定性](@entry_id:146550)至关重要。一个好的选择是[后验分布](@entry_id:145605)中具有高密度的点，例如 MCMC 样本的[后验均值](@entry_id:173826)或众数。选择这样的点有两个主要好处：

1.  **减小估计的[方差](@entry_id:200758)**：最终我们关心的是 $\log \hat{p}(y)$ 的稳定性，其主要误差来源是 $\log \hat{p}(\theta^\star \mid y)$。使用 Delta 方法近似，$\log \hat{p}(\theta^\star \mid y)$ 的[方差近似](@entry_id:268585)为 $\text{Var}(\log \hat{p}(\theta^\star \mid y)) \approx \frac{\text{Var}(\hat{p}(\theta^\star \mid y))}{\{p(\theta^\star \mid y)\}^2}$。选择一个高密度点会使得分母 $p(\theta^\star \mid y)^2$ 变大，从而显著降低对数尺度上的估计[方差](@entry_id:200758)。此外，当 $\theta^\star$ 位于后验样本集中的区域时，用于 Rao-Blackwellization 平均的各项 $p(\theta^\star|\dots, y)$ 的值也趋向于更为齐整，这会减小分子 $\text{Var}(\hat{p}(\theta^\star \mid y))$ 本身。[@problem_id:3294555]

2.  **减小有限样本偏倚**：MCMC 在有限次迭代中可能无法充分探索整个后验空间，尤其是在多模态或[长尾分布](@entry_id:142737)的情况下。如果选择的 $\theta^\star$ 位于 MCMC 链很少访问甚至从未访问过的区域（例如一个未被发现的远端模式），那么基于现有样本的估计将会产生严重的偏倚。选择一个链已充分混合和探索的区域内的点，可以确保估计是基于[代表性样本](@entry_id:201715)进行的，从而减小有限样本偏倚。[@problem_id:3294555]

#### 先验分布的角色

[边际似然](@entry_id:636856)的值对先验分布的选择高度敏感，这是其作为[模型复杂度惩罚](@entry_id:752069)机制的内在属性。

1.  **正派先验 (Proper Priors) 的必要性**：使用 Chib 方法（以及任何其他方法）计算[贝叶斯因子](@entry_id:143567)时，一个绝对的要求是所有模型都必须使用正派先验（即积分为 1 的先验）。如果使用不正派先验（improper prior），例如常用的 [Jeffreys 先验](@entry_id:164583) $p(\beta, \sigma^2) \propto \sigma^{-2}$，先验密度 $p(\theta)$ 本身只被定义到一个任意的乘法常数。这意味着 $\log p(\theta^\star)$ 是未定义的（或包含一个任意常数），导致计算出的 $\log p(y)$ 也是任意的。这样的“证据”在模型间不具有可比性，因为它们各自依赖于一个独立的、无法确定的常数。因此，不正派先验使得[贝叶斯因子](@entry_id:143567)失去意义。为了进行有效的[模型选择](@entry_id:155601)，必须为所有参数指定正派先验。例如，在[线性回归](@entry_id:142318)[模型选择](@entry_id:155601)中，可以使用 Zellner's g-prior 这类在不同模型间保持一致性和可比性的客观信息先验。[@problem_id:3294571]

2.  **弱信息先验的尾部行为**：即使先验是正派的，其具体形式（特别是尾部行为）也会影响估计的稳定性。当似然函数对某些参数（例如， nuisance parameters $\eta$）提供的信息很弱时，后验 $p(\eta \mid y)$ 将在很大程度上由先验 $p(\eta)$决定。如果此时为 $\eta$选择了一个弱信息的[重尾](@entry_id:274276)先验（如[柯西分布](@entry_id:266469)），那么其后验也会非常弥散。这会导致 Rao-Blackwellized 估计 $\hat{p}(\theta^\star \mid y) = \frac{1}{M}\sum p(\theta^\star \mid \eta^{(m)}, y)$ 中的各项 $p(\theta^\star \mid \eta^{(m)}, y)$ 随 $\eta^{(m)}$ 的剧烈变化而大幅波动，从而增大了估计的蒙特卡洛[方差](@entry_id:200758)。此外，[重尾](@entry_id:274276)的[后验分布](@entry_id:145605)往往会使 MCMC 采样器的混合速度变慢，增加链的自相关性，进一步降低[有效样本量](@entry_id:271661)，恶化估计精度。不过值得注意的是，随着样本量 $n \to \infty$，[后验分布](@entry_id:145605)会越来越集中于[最大似然估计](@entry_id:142509)附近，此时先验的影响会逐渐消失，估计的稳定性也会随之提高。[@problem_id:3294535]

#### [蒙特卡洛](@entry_id:144354)误差的量化

Chib 方法的输出是一个估计值，而非精确值，因此报告其不确定性至关重要。MCMC 链的自相关性是[估计误差](@entry_id:263890)的主要来源。正自相关意味着样本并非独立，[有效样本量](@entry_id:271661)小于 MCMC 迭代次数。Markov Chain Central Limit Theorem (CLT) 指出，估计量 $\hat{p}(\theta^\star \mid y)$ 的[方差](@entry_id:200758)为 $\sigma_g^2/N_{eff}$，其中 $N_{eff}$ 是[有效样本量](@entry_id:271661)，$\sigma_g^2$ 是[平稳分布](@entry_id:194199)下的[方差](@entry_id:200758)。$\sigma_g^2$ 本身等于 $\gamma_0 + 2\sum_{k=1}^\infty \gamma_k$，其中 $\gamma_k$ 是滞后 $k$ 阶的[自协方差](@entry_id:270483)。强正[自相关](@entry_id:138991)会使 $\sigma_g^2$ 远大于[独立样本](@entry_id:177139)的[方差](@entry_id:200758)。

为了量化最终 $\log \hat{p}(y)$ 的不确定性，需要估计出 $\sigma_g^2$。常见的方法包括：
- **批次均值法 (Batch Means)**：将 MCMC 长链分割成若干个批次，计算每个批次的均值，然后计算这些批次均值间的[方差](@entry_id:200758)。在批次足够大的条件下，批次均值近似独立，它们的[方差](@entry_id:200758)可以一致地估计 $\sigma_g^2/(\text{batch size})$。
- **[谱方差估计](@entry_id:755189) (Spectral Variance Estimators)**：直接利用[时间序列分析](@entry_id:178930)技术，通过对[自协方差函数](@entry_id:262114)进行加权求和（例如使用 Bartlett 窗）来估计在频率为零处的谱密度，该谱密度正比于 $\sigma_g^2$。

得到 $\text{Var}(\hat{p}(\theta^\star \mid y))$ 的估计后，可再次使用 Delta 方法来得到 $\text{Var}(\log \hat{p}(\theta^\star \mid y))$，并最终得到 $\log \hat{p}(y)$ 的[标准误](@entry_id:635378)。[@problem_id:3294548]

### 高级主题：处理多模态

当后验分布 $p(\theta \mid y)$ 存在多个模式（modes）时，标准的 Chib 方法会面临严峻挑战。如果 MCMC 链在模式间混合不充分（例如，被困于单个模式），那么基于这个链的任何估计都将只反映该模式的信息，导致对 $p(\theta^\star \mid y)$ 的估计产生严重偏倚，特别是当 $\theta^\star$ 位于另一个模式时。

一个更稳健的、适用于多模态情形的扩展方法如下：
1.  **识别和分离模式**：首先，将后验分布看作是 $M$ 个模式的混合体：$p(\theta \mid y) = \sum_{m=1}^M \pi_m p_m(\theta \mid y)$。其中，$\pi_m$ 是模式 $m$ 的[后验概率](@entry_id:153467)（权重），$p_m(\theta \mid y)$ 是在模式 $m$ 内部的条件后验密度。

2.  **修正恒等式**：对于一个位于模式 $m_k$ 中的特定点 $\theta_k$，其全局后验纵坐标为 $p(\theta_k \mid y) = \pi_{m_k} p_{m_k}(\theta_k \mid y)$。将此代入 Chib 恒等式，得到：
    $$ p(y) = \frac{p(y \mid \theta_k) p(\theta_k)}{\pi_{m_k} p_{m_k}(\theta_k \mid y)} $$

3.  **分步估计**：这个修正后的恒等式指明了 principled 的估计路径：
    a.  运行多个 MCMC 模拟，每个模拟通过限制参数范围或使用特定初始值等方式，使其专门探索一个模式 $m$。
    b.  对于每个模式 $m$ 内的点 $\theta_k$，使用该模式专属的 MCMC 输出来估计其**条件**后验纵坐标 $\hat{p}_{m_k}(\theta_k \mid y)$。
    c.  使用专门的方法（如[桥式采样](@entry_id:746983)或可逆跳 MCMC）来估计各个模式的权重 $\hat{\pi}_m$。这是一个独立的、非平凡的统计问题。
    d.  将这些估计值代入修正后的恒等式，得到一个对 $p(y)$ 的估计 $\hat{p}_k(y)$。

4.  **聚合**：由于这个恒等式对任何点都成立，我们可以选择多个点 $\theta_k$ (可以来自不同模式)，得到一系列估计值 $\{\hat{p}_k(y)\}_{k=1}^K$。每一个都是对 $p(y)$ 的一致估计。通过对它们进行加权平均（[凸组合](@entry_id:635830)），例如 $\hat{p}(y) = \sum_k w_k \hat{p}_k(y)$，可以得到一个更稳健、对[方差](@entry_id:200758)不那么敏感的最终估计。

这个多点聚合策略是处理多模态问题的 principled 方法，它要求我们显式地处理后验分布的混合结构，而不是忽略它。[@problem_id:3294544]