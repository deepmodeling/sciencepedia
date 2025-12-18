## 引言
贝叶斯推断为在不确定性下进行推理提供了一个严谨而强大的理论框架，但在实践中，其应用常常受限于一个核心的计算挑战：后验分布的解析形式通常是未知的或难以处理的。当模型变得复杂、参数维度增高时，直接计算[后验分布](@entry_id:145605)变得不可行。这一挑战催生了统计学和机器学习领域一个充满活力的研究方向——后验分布的近似。

本文旨在系统性地解决这一知识鸿沟，即在无法获得精确解时，我们如何进行可靠的贝叶斯推断。我们将深入探讨为何精确推断如此困难，其根源在于一个棘手的、高维的归一化积分，并展示现代贝叶斯实践如何围绕着绕过或近似这个积分而构建。

为了全面掌握这些技术，本文将引导您学习三个循序渐进的部分。首先，在“原理与机制”一章中，我们将剖析[近似推断](@entry_id:746496)的根本挑战，并系统阐述各类主流方法，包括[渐近近似](@entry_id:275870)（如[拉普拉斯近似](@entry_id:636859)）、[随机近似](@entry_id:270652)（如MCMC和重要性抽样）和确定性近似（如[变分推断](@entry_id:634275)）的内在逻辑与数学基础。接着，在“应用与跨学科联系”一章中，我们将展示这些理论如何在计算物理学、生态学、文本分析等真实科学问题中发挥作用，将抽象的原理与具体的实践应用联系起来。最后，“动手实践”部分将提供一系列精心设计的练习，让您通过实际操作来加深对采样器偏差、多峰性挑战等关键概念的理解。

通过本篇文章的学习，您将能够理解并区分不同的[后验近似](@entry_id:753628)策略，为在您自己的研究中选择和评估合适的近似方法打下坚实的基础。让我们首先深入探讨这些方法的原理与机制。

## 原理与机制

在贝叶斯推断的实践中，我们很少能够获得后验分布的精确解析解。因此，理解何时以及为何需要近似，并掌握各种近似方法的原理，对于现代统计学家和数据科学家来说至关重要。本章将系统地阐述[后验分布近似](@entry_id:753632)的核心挑战，并深入探讨各类主要近似方法的内在原理和机制。

### 根本挑战：棘手的[归一化常数](@entry_id:752675)

根据贝叶斯定理，给定数据 $y$ 后，参数 $\theta$ 的[后验分布](@entry_id:145605) $p(\theta \mid y)$ 可以表示为：

$$
p(\theta \mid y) = \frac{p(y \mid \theta) p(\theta)}{p(y)}
$$

其中，$p(y \mid \theta)$ 是似然函数，$p(\theta)$ 是先验分布。分母 $p(y)$ 被称为**[边际似然](@entry_id:636856)**（marginal likelihood）或**证据**（evidence）。它通过对参数空间中所有可能的 $\theta$ 值进行积分（或求和）得到：

$$
p(y) = \int p(y \mid \theta) p(\theta) \, d\theta
$$

$p(y)$ 的作用是作为[归一化常数](@entry_id:752675)，确保后验分布 $p(\theta \mid y)$ 的总积分为1，使其成为一个合法的[概率分布](@entry_id:146404)。然而，正是这个积分构成了贝叶斯推断中最主要的计算瓶颈 。在大多数实际模型中，参数 $\theta$ 的维度 $d$ 可能很高，导致上述积分成为一个[高维积分](@entry_id:143557)。这种积分通常没有解析解，并且使用传统的[数值积分方法](@entry_id:141406)（如网格法或求积法）进行计算的成本会随着维度 $d$ 的增加呈指数级增长，很快变得不可行。

$p(y)$ 对于给定的数据 $y$ 而言是一个常数，它不依赖于 $\theta$。一些错误的观点认为在类似Metropolis-Hastings的算法中需要为每个提议的 $\theta$ 值重新计算 $p(y)$，但这是一种误解；$p(y)$ 在这些算法的接受率计算中恰好被消去了。真正的挑战在于，如果我们想要直接计算[后验概率](@entry_id:153467)密度 $p(\theta \mid y)$ 的值，或者比较不同模型的证据 $p(y)$，我们就无法回避这个棘手的积分。

因此，现代贝叶斯方法论的核心，在很大程度上是围绕如何绕过或近似计算这个棘手的[归一化常数](@entry_id:752675)而建立的。许多[近似推断](@entry_id:746496)方法，例如马尔可夫链蒙特卡洛（MCMC）和重要性抽样，都巧妙地设计为仅依赖于**未归一化的后验分布**，即[后验分布](@entry_id:145605)与[似然](@entry_id:167119)和先验的乘积成正比的关系：

$$
p(\theta \mid y) \propto p(y \mid \theta) p(\theta)
$$

这种方法使我们能够在不知道归一化常数的情况下，对[后验分布](@entry_id:145605)进行采样或计算其[期望值](@entry_id:153208)。

### 理想情况：[共轭先验](@entry_id:262304)

在深入探讨近似方法之前，我们有必要了解一种理想情况，即后验分布可以被精确解析地计算出来。这种情况出现在似然函数和[先验分布](@entry_id:141376)形成一个**共轭对**（conjugate pair）时。

如果一个先验分布族中的某个[先验分布](@entry_id:141376)与某个[似然函数](@entry_id:141927)结合后，得到的后验分布仍然属于这个[分布](@entry_id:182848)族，那么这个先验分布族就被称为该似然函数的**[共轭先验](@entry_id:262304)**（conjugate prior）。这意味着，数据更新过程仅仅是将[先验分布](@entry_id:141376)的超参数（hyperparameters）更新为后验分布的超参数，而[分布](@entry_id:182848)的函数形式保持不变。

[指数族](@entry_id:263444)[分布](@entry_id:182848)为共轭性提供了一个经典的框架 。假设我们有一系列独立同分布的观测值 $\{x_{i}\}_{i=1}^{n}$，其[似然函数](@entry_id:141927)属于[指数族](@entry_id:263444)：

$$
p(x \mid \theta) = h(x)\,\exp\!\{ \eta(\theta)^{\top} T(x) - A(\theta) \}
$$

其中 $T(x)$ 是充分统计量向量，$\eta(\theta)$ 是自然参数，而 $A(\theta)$ 是[对数配分函数](@entry_id:165248)。对于该似然，存在一个[共轭先验](@entry_id:262304)，其形式通常为：

$$
\pi(\theta \mid \chi, \nu) \propto m(\theta)\,\exp\!\{ \eta(\theta)^{\top} \chi - \nu A(\theta) \}
$$

其中 $(\chi, \nu)$ 是超参数。通过贝叶斯定理，[后验分布](@entry_id:145605)正比于[似然](@entry_id:167119)与先验的乘积：

$$
\begin{aligned}
\pi(\theta \mid \{x_i\}, \chi, \nu)  \propto p(\{x_i\} \mid \theta) \pi(\theta \mid \chi, \nu) \\
 \propto \left( \prod_{i=1}^n \exp\!\{ \eta(\theta)^{\top} T(x_i) - A(\theta) \} \right) \exp\!\{ \eta(\theta)^{\top} \chi - \nu A(\theta) \} \\
 \propto \exp\! \left\{ \eta(\theta)^{\top} \sum_{i=1}^n T(x_i) - n A(\theta) + \eta(\theta)^{\top} \chi - \nu A(\theta) \right\} \\
 \propto \exp\! \left\{ \eta(\theta)^{\top} \left(\chi + \sum_{i=1}^n T(x_i)\right) - (\nu + n) A(\theta) \right\}
\end{aligned}
$$

我们可以观察到，后验分布与[先验分布](@entry_id:141376)具有完全相同的函数形式。数据[更新过程](@entry_id:273573)仅仅是通过一个简单的加法规则来更新超参数：

$$
\begin{pmatrix} \chi_{\text{post}} \\ \nu_{\text{post}} \end{pmatrix} = \begin{pmatrix} \chi + \sum_{i=1}^{n} T(x_{i}) \\ \nu + n \end{pmatrix}
$$

当共轭性存在时，我们可以得到[后验分布](@entry_id:145605)的精确解析表达式，从而避免了任何近似。这种情况虽然在实践中不常见（因为模型和先验的选择常常受到实际问题的驱动，而非为了数学上的便利），但它提供了一个至关重要的“基准真相”。当我们在一个非共轭的模型中使用近似方法时，可以通过将其与一个相似的、但具有共轭性的模型所得出的精确后验进行比较，来评估近似方法的误差 。

### 近似策略的分类

当共轭性不适用时，我们就必须依赖近似方法。这些方法大致可以分为三类：

1.  **[渐近近似](@entry_id:275870) (Asymptotic Approximations)**：依赖于大数据样本 ($n \to \infty$) 的极限理论，将[后验分布近似](@entry_id:753632)为[高斯分布](@entry_id:154414)。
2.  **确定性近似 (Deterministic Approximations)**：将推断问题转化为一个[优化问题](@entry_id:266749)，寻找一个 tractable 的[分布](@entry_id:182848)来近似真实的后验分布。
3.  **[随机近似](@entry_id:270652) (Stochastic Approximations)**：使用从（或与...相关的）后验分布中生成的随机样本来近似其性质。

接下来，我们将详细探讨这些策略中的关键方法。

### [渐近近似](@entry_id:275870)：高斯[范式](@entry_id:161181)

在大数据背景下，后验分布通常会呈现出一种钟形，即高斯形态。两种关键的理论——[拉普拉斯近似](@entry_id:636859)和[伯恩斯坦-冯·米塞斯定理](@entry_id:635022)——为这种近似提供了形式化的基础。

#### [拉普拉斯近似](@entry_id:636859)

**[拉普拉斯近似](@entry_id:636859)**（Laplace Approximation）是一种基于对数[后验分布](@entry_id:145605)在其峰值（即[后验众数](@entry_id:174279)）附近的二阶泰勒展开，从而构建一个局部[高斯近似](@entry_id:636047)的方法 。

假设后验分布 $p(\theta \mid y)$ 是单峰的，其众数为 $\hat{\theta}$。我们将对数后验 $\log p(\theta \mid y)$ 在 $\hat{\theta}$ 处进行[泰勒展开](@entry_id:145057)：

$$
\log p(\theta \mid y) \approx \log p(\hat{\theta} \mid y) + (\theta - \hat{\theta})^T \nabla \log p(\theta \mid y)\big|_{\theta=\hat{\theta}} + \frac{1}{2}(\theta - \hat{\theta})^T \nabla^2 \log p(\theta \mid y)\big|_{\theta=\hat{\theta}} (\theta - \hat{\theta})
$$

由于 $\hat{\theta}$ 是众数，梯度项 $\nabla \log p(\theta \mid y)\big|_{\theta=\hat{\theta}}$ 为零。定义**观测后验曲率**（observed posterior curvature）为在众数处的负Hessian矩阵：$\mathcal{H}(\hat{\theta}) = -\nabla^2 \log p(\theta \mid y)\big|_{\theta=\hat{\theta}}$。于是，对数[后验近似](@entry_id:753628)为：

$$
\log p(\theta \mid y) \approx C - \frac{1}{2}(\theta - \hat{\theta})^T \mathcal{H}(\hat{\theta}) (\theta - \hat{\theta})
$$

对上式取指数，我们得到[后验分布](@entry_id:145605) $p(\theta \mid y)$ 的近似形式，它正比于一个多元高斯分布的核：

$$
p(\theta \mid y) \approx \mathcal{N}(\theta \mid \hat{\theta}, \mathcal{H}(\hat{\theta})^{-1})
$$

这个高斯分布以**[后验众数](@entry_id:174279)** $\hat{\theta}$ 为中心，其协方差矩阵是**观测后验曲率的逆**。值得注意的是，由于 $\log p(\theta \mid y) = \log p(y \mid \theta) + \log p(\theta) - \log p(y)$，[先验分布](@entry_id:141376)的曲率 $(\nabla^2 \log p(\theta))$ 会对 $\mathcal{H}(\hat{\theta})$ 产生贡献，从而影响近似协[方差](@entry_id:200758) 。

#### [伯恩斯坦-冯·米塞斯定理](@entry_id:635022)

与适用于固定数据集的局部[拉普拉斯近似](@entry_id:636859)不同，**[伯恩斯坦-冯·米塞斯定理](@entry_id:635022)**（Bernstein-von Mises theorem, BvM）是一个关于大样本 ($n \to \infty$) 的渐近结果 。它在数学上严谨地建立了贝叶斯[后验分布](@entry_id:145605)与频率学派的[最大似然估计](@entry_id:142509)之间的联系。

在一定的[正则性条件](@entry_id:166962)下（例如，模型可识别、[参数空间](@entry_id:178581)为开集、先验在[真值](@entry_id:636547)附近为正且连续、[费雪信息矩阵](@entry_id:750640)正定等），BvM定理指出，[后验分布](@entry_id:145605) $\Pi(\cdot \mid y_1, \dots, y_n)$ 在总变差距离（total variation distance）下，[依概率收敛](@entry_id:145927)于一个[高斯分布](@entry_id:154414)：

$$
\big\|\Pi\big(\cdot\mid y^n\big) - \mathcal{N}\! \big(\hat{\theta}_{n}, [n I(\theta_{0})]^{-1}\big)\big\|_{\mathrm{TV}} \xrightarrow{P_{\theta_{0}}} 0
$$

其中 $\hat{\theta}_{n}$ 是**最大似然估计** (MLE)，$\theta_0$ 是参数的真实值，$I(\theta_0)$ 是单个观测的**费雪信息**（Fisher information） 。

BvM定理与[拉普拉斯近似](@entry_id:636859)有本质区别 ：
- **[适用范围](@entry_id:636189)**：[拉普拉斯近似](@entry_id:636859)是针对固定样本量 $n$ 的一种数值方法；BvM是关于 $n \to \infty$ 的理论极限。
- **中心**：[拉普拉斯近似](@entry_id:636859)以**[后验众数](@entry_id:174279)** $\hat{\theta}$ 为中心；BvM近似以**[最大似然估计](@entry_id:142509)** $\hat{\theta}_{n}$ 为中心（渐近地，两者都收敛到真值 $\theta_0$）。
- **先验的角色**：在[拉普拉斯近似](@entry_id:636859)中，先验的曲率影响协[方差](@entry_id:200758)；而在BvM定理的条件下，随着数据量的增长，似然函数的作用占主导地位，先验分布的局部形状影响会消失。

### [随机近似](@entry_id:270652)（蒙特卡洛方法）

[随机近似](@entry_id:270652)方法不寻求后验分布的解析形式，而是通过生成服从该[分布](@entry_id:182848)（或与其相关）的样本，并利用这些样本来估计后验的性质，如期望、分位数等。

#### [马尔可夫链蒙特卡洛 (MCMC)](@entry_id:137985)

MCMC的核心思想是构建一个**马尔可夫链**，使其**[平稳分布](@entry_id:194199)**（stationary distribution）恰好是我们的目标后验分布 $\pi(\theta \mid y)$ 。如果马尔可夫链的转移核 $K(\theta, \theta')$ 满足[平稳性条件](@entry_id:191085)：

$$
\int_{\Theta} \pi(\theta) K(\theta, \theta') \, d\theta = \pi(\theta') \quad \text{for all } \theta' \in \Theta
$$

那么，只要链是遍历的（ergodic），从任意初始点开始运行足够长时间后，链上的样本就可以被看作是从目标[后验分布](@entry_id:145605) $\pi(\theta \mid y)$ 中抽取的（近似）样本。

一个确保[平稳性](@entry_id:143776)的更强的、但更容易构造的条件是**[细致平衡条件](@entry_id:265158)**（detailed balance condition），也称为**[可逆性](@entry_id:143146)**（reversibility）：

$$
\pi(\theta) K(\theta, \theta') = \pi(\theta') K(\theta', \theta) \quad \text{for all } \theta, \theta' \in \Theta
$$

满足[细致平衡条件](@entry_id:265158)的[马尔可夫链](@entry_id:150828)是可逆的。**Metropolis-Hastings (MH) 算法**就是通过精心设计[接受概率](@entry_id:138494)来强制满足[细致平衡](@entry_id:145988)的典型例子 。在其接受率的计算中，目标分布 $\pi$ 以比率形式出现，使得[归一化常数](@entry_id:752675) $p(y)$ 被完美抵消，从而解决了 intractable normalizing constant 的问题 。

然而，[可逆性](@entry_id:143146)并[非平稳性](@entry_id:180513)的必要条件。可逆链常表现出类似[随机游走](@entry_id:142620)的[扩散](@entry_id:141445)行为，探索效率可能不高。现代MCMC研究的一个重要方向是设计**非可逆**（non-reversible）马尔可夫链，例如[哈密顿蒙特卡洛](@entry_id:144208)（HMC）及其变体。这些算法引入了类似“动量”的机制，使得链能够以更持久和系统的轨迹探索[参数空间](@entry_id:178581)，从而可以显著提高混合效率（mixing efficiency），减少样本的[自相关](@entry_id:138991)性 。

#### 重要性抽样

**重要性抽样**（Importance Sampling, IS）是另一种强大的[蒙特卡洛](@entry_id:144354)技术，尤其适用于修正一个已有近似[分布](@entry_id:182848)的场景。其基本思想是，通过从一个易于抽样的**提议分布**（proposal distribution）$g(\theta)$ 中抽取样本，然后对每个样本赋予一个**重要性权重**，来估计在目标后验分布 $\pi(\theta \mid y)$下的期望。

在[贝叶斯推断](@entry_id:146958)中，由于[归一化常数](@entry_id:752675)未知，我们通常使用**[自归一化](@entry_id:636594)重要性抽样**（Self-Normalized Importance Sampling, SNIS）。对于目标期望 $\mu = \mathbb{E}_{\pi}[h(\theta)]$，其[SNIS估计量](@entry_id:754991)为：

$$
\hat{\mu} = \frac{\sum_{i=1}^N w_i \, h(\theta_i)}{\sum_{i=1}^N w_i}
$$

其中，样本 $\theta_1, \dots, \theta_N$ 是从 $g(\theta)$ 中独立抽取的，权重 $w_i = \frac{\pi(\theta_i \mid y)}{g(\theta_i)} \propto \frac{p(y \mid \theta_i) p(\theta_i)}{g(\theta_i)}$ 。同样，归一化常数在权重的比率中被消去。

[SNIS估计量](@entry_id:754991)具有以下关键性质 ：
1.  **有限样本偏差**：由于分母是随机的，[SNIS估计量](@entry_id:754991)对于有限样本量 $N$ 是有偏的，其偏差通常为 $O(1/N)$。但它是渐近无偏的。
2.  **[方差](@entry_id:200758)敏感性**：SNIS的成败极度依赖于提议分布 $g(\theta)$ 的选择。如果 $g(\theta)$ 的尾部比 $\pi(\theta \mid y)$ 更“轻”（即在后验概率高的区域，$g(\theta)$ 的值很小），那么重要性权重 $w_i$ 的[方差](@entry_id:200758)会非常大，甚至无穷大。这会导致估计量 $\hat{\mu}$ 的[方差](@entry_id:200758)极大，估计结果极其不稳定。这种现象被称为**权重退化**（weight degeneracy）。理想的[提议分布](@entry_id:144814)是目标后验本身，而一个常见的、但往往效率很差的选择是使用先验分布 $p(\theta)$ 作为[提议分布](@entry_id:144814)。

#### [近似贝叶斯计算](@entry_id:746494) (ABC)

在某些情况下，[似然函数](@entry_id:141927) $p(y \mid \theta)$ 本身就难以评估，但从模型 $p(x \mid \theta)$ 中生成模拟数据 $x$ 是可行的。**[近似贝叶斯计算](@entry_id:746494)**（Approximate Bayesian Computation, ABC）就是为这类“似然函数未知”问题设计的 。

ABC的核心思想是用一个更宽松的条件替代严格的 $p(y \mid \theta)$ 评估：它接受参数 $\theta$ 的条件是，根据 $\theta$ 生成的模拟数据 $x$ 与观测数据 $y$ “足够接近”。通常，这种“接近”是通过比较低维的**摘要统计量**（summary statistics）$S(\cdot)$ 来度量的。ABC的后验分布定义为：

$$
p_{\epsilon}(\theta\mid y) \propto p(\theta)\int \mathbb{I}\{d(S(x),S(y)) \le \epsilon\}\,p(x\mid \theta)\,dx
$$

其中 $d(\cdot, \cdot)$ 是一个[距离度量](@entry_id:636073)，$\epsilon$ 是一个容忍度阈值。这个过程可以被看作是对条件 $S(x) \in B_{\epsilon}(S(y))$ （即模拟摘要统计量落在观测摘要统计量的一个 $\epsilon$-球内）进行贝叶斯推断。

ABC的近似质量由几个关键因素决定 ：
- **摘要统计量 $S$**：如果 $S$ 是 $\theta$ 的**充分统计量**，那么当 $\epsilon \to 0$ 时，ABC后验 $p_{\epsilon}(\theta \mid y)$ 会收敛到真实的后验 $p(\theta \mid y)$。如果 $S$ 不充分，信息就会丢失，即使 $\epsilon \to 0$，ABC后验也只会收敛到 $p(\theta \mid S(y))$，这与真实后验之间存在一个不可约减的偏差。
- **容忍度 $\epsilon$**：$\epsilon$ 控制着一个关键的[偏差-方差权衡](@entry_id:138822)。当 $\epsilon \to \infty$ 时，所有模拟都被接受，后验退化为先验。当 $\epsilon \to 0$ 时，偏差减小，但接受率急剧下降，导致蒙特卡洛[方差](@entry_id:200758)急剧增加。
- **摘要统计量的维度 $d_S$**：接受率与 $\epsilon^{d_S}$ 成正比。这意味着摘要统计量的维度越高，接受率下降得越快。这就是ABC中的**维度灾难**，它限制了我们使用高维摘要统计量的能力。

### 确定性近似：[变分推断](@entry_id:634275)

**[变分推断](@entry_id:634275)**（Variational Inference, VI）将贝叶斯推断问题重新构建为一个[优化问题](@entry_id:266749) 。其目标是在一个指定的、易于处理的[分布](@entry_id:182848)族 $\mathcal{Q}$（例如，全分解的高斯分布，即**平均场**（mean-field）近似）中，寻找一个成员 $q(\theta)$ 来最好地近似真实的[后验分布](@entry_id:145605) $p(\theta \mid y)$。

“最好”的衡量标准通常是最小化 $q(\theta)$ 与 $p(\theta \mid y)$ 之间的**Kullback-Leibler (KL) 散度**，即 $\text{KL}(q \,\|\, p(\theta \mid y))$。通过简单的代数推导，我们可以得到一个至关重要的恒等式：

$$
\log p(y) = \underbrace{\mathbb{E}_{q}[\log p(y,\theta)] - \mathbb{E}_{q}[\log q(\theta)]}_{\text{ELBO}(q)} + \underbrace{\text{KL}(q \,\|\, p(\theta \mid y))}_{\ge 0}
$$

上式中，$\text{ELBO}(q)$ 被称为**[证据下界](@entry_id:634110)**（Evidence Lower Bound）。由于KL散度总是非负的，ELBO是[模型证据](@entry_id:636856) $\log p(y)$ 的一个下界。因为 $\log p(y)$ 对于 $q$ 是一个常数，所以最小化[KL散度](@entry_id:140001) $\text{KL}(q \,\|\, p(\theta \mid y))$ 等价于最大化ELBO 。

ELBO的巨大优势在于它的计算不依赖于棘手的证据 $p(y)$。通过最大化ELBO，VI将推断问题转化为了一个（通常是高维的）[优化问题](@entry_id:266749)，可以使用梯度上升等方法来求解。

#### 正则化流：一种强大的变分族

传统VI（如平均场近似）的主要局限在于其选择的变分族 $\mathcal{Q}$ 可能过于简单，无法捕捉真实后验分布的复杂依赖结构。**正则化流**（Normalizing Flows）提供了一种构建极其灵活和富有表现力的变分族的方法 。

其核心思想是通过一个可逆的、可微的变换 $T_\phi$ 将一个简单基础[分布](@entry_id:182848)（如标准正态分布）的[随机变量](@entry_id:195330) $z$ 映射到目标空间，生成 $\theta = T_\phi(z)$。根据[变量替换公式](@entry_id:139692)，变换后的变量 $\theta$ 的概率密度 $q_\phi(\theta)$ 为：

$$
q_\phi(\theta) = r(T_\phi^{-1}(\theta)) \left| \det \nabla T_\phi^{-1}(\theta) \right|
$$

其中 $r(\cdot)$ 是基础[分布](@entry_id:182848)的密度。通过将多个简单的可逆变换（其[雅可比行列式](@entry_id:137120)易于计算，例如那些[雅可比矩阵](@entry_id:264467)是三角形的变换）组合起来，可以构建出非常复杂的变换 $T_\phi$。然后，我们可以将ELBO（或等价的[KL散度](@entry_id:140001)）表示为对简单基础[分布](@entry_id:182848) $z$ 的期望，并使用梯度下降法优化变换的参数 $\phi$ 。

### 误差预算与方法综合

在实践中，我们常常结合使用这些方法。例如，我们可能首先使用[变分推断](@entry_id:634275)得到一个近似后验 $q_\lambda(\theta)$，然后从 $q_\lambda$ 中抽样来计算期望。理解这种多阶段近似过程中的总误差至关重要 。

考虑我们使用从VI近似 $q_\lambda$ 中抽取的 $n$ 个样本来估计 $\mu = \mathbb{E}_{\pi}[h(\theta)]$。一个简单的估计量是 $\hat{\mu}_{n} = \frac{1}{n}\sum_{i=1}^{n} h(\theta_{i})$。其[均方误差 (MSE)](@entry_id:165831) 可以分解为两个部分：

$$
\mathrm{MSE}(\hat{\mu}_{n}) = \underbrace{(\mathbb{E}_{q_{\lambda}}[h(\theta)] - \mu)^2}_{\text{平方算法偏差}} + \underbrace{\frac{1}{n}\mathrm{Var}_{q_{\lambda}}(h(\theta))}_{\text{蒙特卡洛方差}}
$$

- **算法偏差**：源于近似[分布](@entry_id:182848) $q_\lambda$ 与真实后验 $\pi$ 之间的系统性差异。例如，VI最小化 $\text{KL}(q\|\pi)$ 的倾向会导致 $q_\lambda$ 比 $\pi$ 更“紧凑”（即[方差](@entry_id:200758)偏低，尾部更轻），这种**[方差](@entry_id:200758)偏低**（underdispersion）会直接导致对某些函数 $h(\theta)$ 的期望估计产生偏差。
- **蒙特卡洛[方差](@entry_id:200758)**：源于我们只使用了有限数量的样本 $n$。

为了消除算法偏差，我们可以使用**重要性抽样修正**。通过使用 $q_\lambda$ 作为提议分布，我们可以构建[SNIS估计量](@entry_id:754991) $\tilde{\mu}_{n}$。这个估计量是渐近无偏的，它有效地用权重“校正”了样本，使其表现得像是从真实后验 $\pi$ 中抽取的一样。

然而，这种修正并非没有代价。如果 $q_\lambda$ 对 $\pi$ 的近似很差（例如，VI的[方差](@entry_id:200758)偏低问题很严重），那么重要性权重的[方差](@entry_id:200758)会非常大，导致 $\tilde{\mu}_{n}$ 的[方差](@entry_id:200758)爆炸，使其变得不可靠。

因此，现代贝叶斯工作流强调以下几点 ：
- **控制算法偏差**：使用更灵活的变分族（如正则化流）来减少 $q_\lambda$ 和 $\pi$ 之间的差距。
- **控制蒙特卡洛[方差](@entry_id:200758)**：增加样本量 $n$，或在MCMC的背景下，通过改进采样器（如使用HMC）来提高**[有效样本量](@entry_id:271661)**（Effective Sample Size, ESS）。
- **诊断**：使用诸如**帕累托平滑重要性抽样**（Pareto Smoothed Importance Sampling, PSIS）之类的诊断工具来评估重要性权重是否稳定。PSIS的形状参数 $\hat{k}$ 可以告诉我们IS修正是否可靠。

通过结合确定性近似（如VI）的速度和[随机近似](@entry_id:270652)（如IS或MCMC）的渐近精确性，并辅以严格的诊断，我们可以在复杂的贝叶斯模型中实现既高效又可靠的推断。