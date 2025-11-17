## 引言
在科学和工程的许多前沿领域，基于复杂计算机模拟的机理模型日益成为探索世界的核心工具。然而，这些模型的复杂性往往导致其似然函数难以或无法以解析形式表达，这为使用传统的[贝叶斯推断](@entry_id:146958)方法带来了根本性的挑战。当似然函数变得“难解”（intractable）时，我们如何才能将模型的预测与观测数据相结合，从而对模型参数进行推断和学习？这正是近似贝叶斯计算（Approximate Bayesian Computation, ABC）旨在解决的核心知识缺口。

本文将系统性地介绍ABC这一强大的“无[似然](@entry_id:167119)”（likelihood-free）推断框架。读者将通过三个层层递进的章节，全面掌握ABC的理论与实践。在第一章**“原理与机制”**中，我们将深入剖析ABC的基本思想，阐明其如何通过模拟和比较来近似[后验分布](@entry_id:145605)，并探讨其误差来源与收敛性质。随后，在第二章**“应用与跨学科联系”**中，我们将通过一系列来自生命科学、物理学和工程学的生动案例，展示ABC在解决真实世界问题中的巨大威力，并揭示其作为跨学科桥梁的角色。最后，在第三章**“动手实践”**中，读者将通过具体的编程练习，将理论知识转化为实际技能，学会如何实现、验证和优化[ABC算法](@entry_id:746190)。

通过本文的学习，您将不仅理解ABC的运作方式，更将洞悉其在现代计算科学中的重要地位，并掌握一种能够驾驭复杂模型的强大统计推断工具。

## 原理与机制

在贝叶斯推断的框架下，[后验分布](@entry_id:145605)通过贝叶斯定理将先验知识与数据中包含的信息（以[似然函数](@entry_id:141927)的形式）结合起来。然而，在许多科学领域，尤其是那些依赖复杂计算机模拟的领域，模型的似然函数 $p(x|\theta)$ 可能是“难解的”（intractable）。这意味着，虽然给定参数 $\theta$ 我们可以从模型中生成（模拟）数据 $x$，但我们无法写出或评估似然函数 $p(x|\theta)$ 的解析表达式。近似贝叶斯计算（Approximate Bayesian Computation, ABC）提供了一个强大的框架，专门用于处理这类“无似然”（likelihood-free）的推断问题。本章将深入探讨ABC的基本原理、理论解释及其关键机制。

### 棘手的[似然函数](@entry_id:141927)：[无似然推断](@entry_id:190479)的动机

标准的[贝叶斯推断](@entry_id:146958)围绕后验分布展开：
$$
\pi(\theta | x_{\text{obs}}) \propto \pi(\theta) p(x_{\text{obs}} | \theta)
$$
其中 $\pi(\theta)$ 是参数的先验分布，$p(x_{\text{obs}} | \theta)$ 是观测数据 $x_{\text{obs}}$ 的[似然函数](@entry_id:141927)。当模型由一个隐式生成过程定义时，例如一个复杂的计算机模拟器 $x = g(\theta, u)$（其中 $u$ 是随机输入），[似然函数](@entry_id:141927)就变得难以捉摸。从测度论的角度来看，一个显式的[似然函数](@entry_id:141927) $p(x|\theta)$ 可以被理解为由映射 $g(\theta, \cdot)$ 诱导的关于某个参考测度（如[勒贝格测度](@entry_id:139781)）的[拉东-尼科迪姆导数](@entry_id:158399)。如果模拟器的输出 $x$ 实际上位于一个比数据空间 $\mathcal{X}$ 维度更低的[数据流形](@entry_id:636422)上，那么其[分布](@entry_id:182848)测度相对于[勒贝格测度](@entry_id:139781)就是奇异的，一个有意义的似然密度函数便不存在。在这种情况下，对单个点 $x_{\text{obs}}$ 进行的精确[贝叶斯推断](@entry_id:146958)是病态的（ill-posed）。这正是ABC等[无似然方法](@entry_id:751277)发挥作用的场景 [@problem_id:3489611]。

ABC的核心思想是绕过对似然函数的直接评估，转而利用模型的模拟能力。最简单的ABC形式是**拒绝抽样算法**：
1. 从先验分布 $\pi(\theta)$ 中抽取一个参数提议 $\theta^*$。
2. 使用 $\theta^*$ 从模型中模拟一个合成数据集 $x^*$。
3. 如果模拟数据 $x^*$ 与观测数据 $x_{\text{obs}}$ “足够接近”，则接受 $\theta^*$ 作为后验分布的一个样本。

这个过程重复多次，收集到的接受样本就构成了对后验分布 $\pi(\theta | x_{\text{obs}})$ 的近似。

为了使“足够接近”这一概念具有可操作性，我们通常引入三个要素：
- **摘要统计量 (Summary Statistic)** $s(\cdot)$: 一个将[高维数据](@entry_id:138874) $x$ 映射到低维（通常是信息更集中）向量的函数。我们比较的是摘要统计量 $s(x^*)$ 和 $s(x_{\text{obs}})$。
- **[距离度量](@entry_id:636073) (Distance Metric)** $\rho(\cdot, \cdot)$: 用于量化两个摘要统计量向量之间差异的函数，例如欧氏距离。
- **容忍度 (Tolerance)** $\epsilon$: 一个小的正数，定义了可接受的距离阈值。

于是，接受准则变为 $\rho(s(x^*), s(x_{\text{obs}})) \le \epsilon$。

### ABC后验分布的正式定义

拒绝抽样算法实际上是从一个近似的[后验分布](@entry_id:145605)中进行抽样。我们可以更正式地定义这个目标分布。ABC通过一个基于核函数 $K_\epsilon$ 的加权方案来替代棘手的[似然函数](@entry_id:141927)，该方案根据模拟摘要与观测摘要的差异来衡量权重。这个替代品被称为 **ABC似然函数**：
$$
L_{\epsilon}(s_{\text{obs}} | \theta) = \int K_{\epsilon}(\rho(s(x), s_{\text{obs}})) p(x | \theta) dx
$$
这里，$K_\epsilon$ 是一个由容忍度 $\epsilon$ 参数化的非负[核函数](@entry_id:145324)，它在零点附近集中大部分质量。例如，对应于基本拒绝算法的均匀核（或称盒形核）可以写为 $K_\epsilon(u) \propto \mathbb{I}\{u \le \epsilon\}$，其中 $\mathbb{I}\{\cdot\}$ 是指示函数。在这种情况下，ABC似然函数就简化为模拟摘要落在观测摘要 $\epsilon$-邻域内的概率 [@problem_id:3288743]。

将这个ABC[似然函数](@entry_id:141927)代入[贝叶斯定理](@entry_id:151040)，我们便得到了 **ABC后验分布** 的正式表达式 [@problem_id:3288743]：
$$
\pi_{\epsilon}(\theta | s_{\text{obs}}) \propto \pi(\theta) L_{\epsilon}(s_{\text{obs}} | \theta) = \pi(\theta) \int K_{\epsilon}(\rho(s(x), s_{\text{obs}})) p(x | \theta) dx
$$
所有基于ABC的算法，无论是简单的拒绝抽样还是更高级的变体，其目标都是从这个 $\pi_{\epsilon}(\theta | s_{\text{obs}})$ [分布](@entry_id:182848)中抽样。

### 对ABC近似的解释

ABC后验是一种近似，理解这种近似的性质至关重要。我们可以从两个互补的角度来解释ABC在做什么。

#### 卷积与平滑解释

第一个解释是，ABC[似然函数](@entry_id:141927)可以看作是真实摘要统计量[似然函数](@entry_id:141927) $p_s(s|\theta)$ 的一个平滑版本。通过在摘要统计量空间上进行积分，ABC似然函数可以重写为：
$$
L_{\epsilon}(s_{\text{obs}} | \theta) = \int K_{\epsilon}(\rho(s, s_{\text{obs}})) p_s(s | \theta) ds
$$
如果距离 $\rho$ 是由范数诱导的（例如，$\rho(s, s_{\text{obs}}) = \|s - s_{\text{obs}}\|$），并且[核函数](@entry_id:145324)是对称的，那么这个积分就是一个 **卷积**。ABC本质上是用一个[平滑核](@entry_id:195877)去卷积真实的（但难解的）摘要似然函数。这种平滑操作引入了偏差，但使得计算成为可能 [@problem_id:3288759]。

#### 扰动[模型解释](@entry_id:637866)

卷积解释直接引出了一个更深刻的观点：ABC可以被视为在一个**扰动模型**（perturbed model）上进行**精确的贝叶斯推断** [@problem_id:3288759]。想象一个两步的生成过程：
1. 真实摘要 $s$ 是根据模型 $s \sim p_s(\cdot|\theta)$ 生成的。
2. 观测到的摘要 $s_{\text{obs}}$ 是由真实摘要 $s$ 加上一个误差项 $\eta$ 得到的，即 $s_{\text{obs}} = s + \eta$。

如果误差项 $\eta$ 的[分布](@entry_id:182848)恰好由ABC的[核函数](@entry_id:145324)和[距离度量](@entry_id:636073)定义，那么在这个“摘要加噪”的辅助模型下，$s_{\text{obs}}$ 的[边际似然](@entry_id:636856)函数恰好就是ABC似然函数 $L_{\epsilon}(s_{\text{obs}} | \theta)$。因此，[ABC算法](@entry_id:746190)得到的后验 $\pi_\epsilon(\theta|s_{\text{obs}})$ 是关于这个加入了人造噪声的模型的精确后验。

我们可以通过一个具体的例子来阐明这一点。假设我们有来自正态分布 $y_i \sim \mathcal{N}(\theta, \sigma^2)$ 的数据（$\sigma^2$ 已知），我们使用样本均值 $\bar{y}$ 作为摘要统计量。[样本均值的抽样分布](@entry_id:173957)是 $\bar{y} \sim \mathcal{N}(\theta, \sigma^2/n)$。如果我们选择一个高斯核 $K_\epsilon(u) \propto \exp(-u^2 / 2\epsilon^2)$，其中 $u = s - s_{\text{obs}}$ 是摘要的差值，那么经过直接计算，可以推导出ABC似然函数为 [@problem_id:3288811]：
$$
L_{\epsilon}(\bar{y} | \theta) = \frac{1}{\sqrt{2\pi\left(\frac{\sigma^{2}}{n} + \epsilon^{2}\right)}} \exp\left(-\frac{(\bar{y} - \theta)^{2}}{2\left(\frac{\sigma^{2}}{n} + \epsilon^{2}\right)}\right)
$$
这正是一个均值为 $\theta$、[方差](@entry_id:200758)为 $(\sigma^2/n + \epsilon^2)$ 的正态分布密度。这清晰地表明，使用高斯核进行ABC，等价于在原摘要统计量的[方差](@entry_id:200758)之上，额外增加了一个由[核函数](@entry_id:145324)宽度决定的[方差](@entry_id:200758) $\epsilon^2$。

### ABC中的误差来源与收敛性

ABC的“近似”性质来源于两个方面：非零的容忍度 $\epsilon > 0$ 和摘要统计量 $s(\cdot)$ 可能造成的信息损失。

#### 容忍度误差与充分性

当容忍度 $\epsilon \to 0$ 时，ABC后验 $\pi_\epsilon(\theta|s_{\text{obs}})$ 收敛到以摘要统计量为条件的[后验分布](@entry_id:145605) $\pi(\theta|s_{\text{obs}})$ [@problem_id:3288743]。这个[极限分布](@entry_id:174797)是否与我们真正想要的、基于完整数据的后验分布 $\pi(\theta|x_{\text{obs}})$ 一致，取决于摘要统计量的选择。

这就引出了**充分统计量**（sufficient statistic）的概念。一个统计量 $s(x)$ 如果包含了数据 $x$ 中关于参数 $\theta$ 的所有信息，那么它就是充分的。根据**内曼-费雪[因子分解定理](@entry_id:749213)**（Neyman-Fisher factorization theorem），当且仅当[似然函数](@entry_id:141927)可以分解为 $p(x|\theta) = g(s(x), \theta)h(x)$ 的形式时，$s(x)$ 是充分的 [@problem_id:3288740]。

- 如果 $s(\cdot)$ 是**充分**的，那么 $\pi(\theta|s_{\text{obs}}) = \pi(\theta|x_{\text{obs}})$。在这种理想情况下，只要 $\epsilon \to 0$，ABC就能收敛到真实的[后验分布](@entry_id:145605)。例如，对于已知[方差](@entry_id:200758)的正态分布，样本均值 $\bar{X}$ 就是均值参数 $\theta$ 的充分统计量。因此，使用 $\bar{X}$ 作为摘要的ABC，在 $\epsilon \to 0$ 时会收敛到精确的共轭后验 [@problem_id:3288740]。

- 如果 $s(\cdot)$ 是**不充分**的，那么 $\pi(\theta|s_{\text{obs}})$ 通常不等于 $\pi(\theta|x_{\text{obs}})$，因为从 $x$ 到 $s(x)$ 的[降维](@entry_id:142982)过程丢失了关于 $\theta$ 的信息。在这种情况下，即使 $\epsilon \to 0$，ABC也只会收敛到一个有偏差的后验分布。例如，对于正态分布，样本[中位数](@entry_id:264877)通常不是均值参数的充分统计量。使用样本[中位数](@entry_id:264877)进行ABC，其极限后验会比使用样本均值的精确后验更加分散（即不确定性更大），因为它没有利用数据中的全部信息 [@problem_id:3288740]。

#### 量化信息损失

摘要统计量造成的信息损失可以通过经典统计理论中的**费雪信息**（Fisher Information）来量化。费雪信息 $I_\theta(Z)$ 衡量了[随机变量](@entry_id:195330) $Z$ 中包含的关于参数 $\theta$ 的[信息量](@entry_id:272315)。通过比较完整数据 $X$ 的费雪信息 $I_\theta(X)$ 和摘要统计量 $s(X)$ 的费雪信息 $I_\theta(s(X))$，我们可以评估信息损失的程度。根据[数据处理不等式](@entry_id:142686)，总有 $I_\theta(s(X)) \le I_\theta(X)$。

例如，对于单次观测来自指数[分布](@entry_id:182848) $X \sim \text{Exp}(\theta)$ 的情况，其[似然函数](@entry_id:141927)为 $f(x|\theta) = \theta e^{-\theta x}$。完整数据的费雪信息为 $I_\theta(X) = 1/\theta^2$。如果我们使用一个不充分的二元摘要统计量 $s(X) = \mathbf{1}\{X \le c\}$（即数据是否超过某个阈值 $c$），可以计算出该摘要的费雪信息为 $I_\theta(s(X)) = (c^2 \theta^2) / (\exp(\theta c) - 1)$。信息保留的比率 $R(\theta, c) = I_\theta(s(X)) / I_\theta(X)$ 就明确地量化了由于使用这个不充分摘要而造成的信息损失 [@problem_id:3288754]。选择能最大化费雪信息的摘要统计量是ABC实践中的一个重要目标。

### ABC[误差分析](@entry_id:142477)与控制

理解了误差的来源后，我们需要发展理论来分析和控制这些误差。

#### 偏差-方差权衡

ABC估计（例如[后验均值](@entry_id:173826)的估计）的误差可以分解为偏差（bias）和[方差](@entry_id:200758)（variance）。考虑ABC的[核密度估计](@entry_id:167724)形式，其[均方误差](@entry_id:175403)（Mean Squared Error, MSE）可以进行[渐近分析](@entry_id:160416)。对于后验期望 $\mathbb{E}[\varphi(\theta)|s_{obs}]$ 的ABC估计量 $\widehat{\mu}_{ABC}$，其MSE主要由两部分构成 [@problem_id:3288819]：
- **平方偏差项**: $ (\text{Bias})^2 \propto \epsilon^4 $。这个误差来自于 $\epsilon>0$ 导致的系统性近似，它随着 $\epsilon$ 的增大而增大。
- **[方差](@entry_id:200758)项**: $\text{Var} \propto (M\epsilon^d)^{-1}$。这个误差来自于用有限的 $M$ 次模拟来估计ABC[似然](@entry_id:167119)，它随着模拟次数 $M$ 和容忍度 $\epsilon$ 的增大而减小（$d$是摘要统计量的维度）。

这个结果揭示了ABC中一个核心的**偏差-方差权衡**。选择非常小的 $\epsilon$ 会减小偏差，但会导致[方差](@entry_id:200758)增大（因为接受的样本变得稀少），需要更多的模拟次数 $M$ 来补偿。

#### 后验分布的收敛性

除了分析[点估计](@entry_id:174544)的误差，我们还可以分析整个后验分布的收敛性。使用**[瓦瑟斯坦距离](@entry_id:147338)**（Wasserstein distance）等度量，可以为ABC后验 $\pi_\epsilon$ 与真实摘要后验 $\pi(\cdot|s_{obs})$ 之间的距离提供上界。在一定的[正则性条件](@entry_id:166962)下，可以证明它们之间的2-[瓦瑟斯坦距离](@entry_id:147338) $W_2(\pi_\epsilon, \pi(\cdot|s_{obs}))$ 以 $\epsilon$ 的速率收敛，即 $W_2 = O(\epsilon)$ [@problem_id:3288750]。

#### 最佳容忍度设置

这些[误差分析](@entry_id:142477)不仅具有理论价值，还能指导实践。通过平衡[偏差和方差](@entry_id:170697)，我们可以推导出**最佳容忍度设置策略**。例如，要最小化总误差，我们需要平衡系统性近似误差（如 $O(\epsilon)$）和[蒙特卡洛](@entry_id:144354)[抽样误差](@entry_id:182646)（如 $O(N^{-1/2})$，其中 $N$ 是接受的样本数）。由于接受样本数 $N$ 本身与 $\epsilon$ 相关（$N \propto n \epsilon^{d_s}$，其中 $n$ 是总模拟次数），我们可以求解得到一个关于 $n$ 的最优容忍度衰减方案。一个典型的结果是 $\epsilon_n \propto n^{-1/(d_s+2)}$ [@problem_id:3288750]。这表明，摘要统计量的维度 $d_s$ 越高，为了控制误差，容忍度 $\epsilon$ 就需要以更慢的速度减小，这反映了所谓的“[维度灾难](@entry_id:143920)”。

### 高级机制：提升ABC效率

简单的拒绝抽样算法在处理小容忍度 $\epsilon$ 时效率极低，因为绝大多数模拟都会被拒绝。为了使ABC成为一种实用工具，研究者们开发了更高效的算法。

#### [序贯蒙特卡洛ABC](@entry_id:754703) (SMC-ABC)

**[序贯蒙特卡洛ABC](@entry_id:754703)**（Sequential Monte Carlo ABC, SMC-ABC）是一种自适应的重要性[抽样方法](@entry_id:141232)。它维护一个由带权重的参数“粒子”组成的群体 $\{\theta_i, w_i\}$，并在一系列逐渐缩小的容忍度阈值 $\epsilon_1 > \epsilon_2 > \dots > \epsilon_T$ 下迭代地演化这个群体 [@problem_id:3536601]。在每个阶段 $t$，算法大致执行以下步骤：
1. **重采样 (Resampling)**: 根据上一阶段的权重 $w_i^{(t-1)}$ 对粒[子群](@entry_id:146164)体进行[重采样](@entry_id:142583)，倾向于选择权重大的粒子。
2. **扰动 (Perturbation)**: 对[重采样](@entry_id:142583)后的粒子施加一个小的随机扰动（通过一个马尔可夫核 $K_t$），生成新的提议粒子。
3. **模拟与接受**: 对于每个新的提议粒子，进行模拟并检查其是否满足更严格的容忍度标准 $\rho(s(x^*), s_{\text{obs}}) \le \epsilon_t$。
4. **加权 (Weighting)**: 为被接受的粒子计算新的权重。权重 $w_i^{(t)}$ 正比于先验与提议分布的比值，即 $w_i^{(t)} \propto \pi(\theta_i^{(t)}) / q_t(\theta_i^{(t)})$，其中 $q_t$ 是由重采样和扰动步骤构成的有效提议分布 [@problem_id:3536601]。

通过这种方式，SMC-ABC将计算资源集中在[参数空间](@entry_id:178581)中与观测数据更匹配的“有希望”的区域。与从整个先验中盲目抽样的拒绝ABC相比，SMC-ABC在后续阶段的接受率要高得多。对于给定的目标 $\epsilon$，SMC-ABC通常能用少得多的模拟次数达到相似的[有效样本量](@entry_id:271661)，从而极大地提升了效率 [@problem_id:3536601]。

#### [马尔可夫链蒙特卡洛](@entry_id:138779)ABC ([ABC-MCMC](@entry_id:746188))

另一种提升效率的策略是将ABC嵌入到**马尔可夫链蒙特卡洛**（Markov Chain Monte Carlo, MCMC）框架中。[ABC-MCMC](@entry_id:746188)算法构建一个[马尔可夫链](@entry_id:150828)，使其平稳分布为ABC后验 $\pi_\epsilon(\theta|s_{\text{obs}})$。

**伪边际方法**（Pseudo-Marginal approach）是实现[ABC-MCMC](@entry_id:746188)的一种强大技术 [@problem_id:3288820]。其核心思想是在[Metropolis-Hastings算法](@entry_id:146870)的接受率计算中，使用ABC似然函数 $L_\epsilon(\theta)$ 的一个**[无偏估计量](@entry_id:756290)** $\widehat{L}_{\epsilon,R}(\theta)$。这个估计量可以通过在每个参数 $\theta$ 处进行 $R$ 次独立的内部模拟并取其核函数权重的平均值来获得：
$$
\widehat{L}_{\epsilon,R}(\theta) = \frac{1}{R} \sum_{r=1}^{R} K_{\epsilon}(s(x^{(r)}), s_{\text{obs}})
$$
令人惊讶的是，尽管在每一步都引入了随机性，但只要似然估计量是无偏的，所得到的MCMC链的边际[平稳分布](@entry_id:194199)**恰好**是目标ABC后验 $\pi_\epsilon(\theta|s_{\text{obs}})$。

然而，这种方法的效率对[似然](@entry_id:167119)[估计量的方差](@entry_id:167223)极为敏感。
- 如果 $\text{Var}(\log \widehat{L}_{\epsilon,R}(\theta))$ 太大，MCMC链可能会偶然生成一个极大的似然估计值，然后“卡”在这个状态很长时间，因为它很难再接受任何移动。这会导致极差的混合（mixing）和高自相关。
- 如果 $\text{Var}(\log \widehat{L}_{\epsilon,R}(\theta))$ 太小（通过使用非常大的 $R$ 实现），则每次MCMC迭代的计算成本会非常高。

因此，这里存在一个计算成本与[统计效率](@entry_id:164796)的权衡。理论和实践表明，为了达到最优效率，内部模拟次数 $R$ 的选择应使得对数似然[估计量的方差](@entry_id:167223)大约为1 [@problem_id:3288820]。这为在伪边际[ABC-MCMC](@entry_id:746188)中调整参数提供了重要的实践指导。