## 引言
在[强化学习](@entry_id:141144)的广阔天地中，[行动者-评论家](@entry_id:634214)（Actor-Critic）与[策略优化](@entry_id:635350)方法代表了一类兼具强大表达能力与广泛适用性的核心算法。与传统的基于价值的方法不同，它们不试图去估计每个状态-动作对的精确价值，而是直接学习一个参数化的策略，指导智能体如何在复杂环境中做出决策。这种直接优化的方式为解决高维、连续的动作空间问题提供了优雅的框架，但也带来了其固有的挑战，其中最突出的便是[梯度估计](@entry_id:164549)的高[方差](@entry_id:200758)问题，它常常导致学习过程缓慢而不稳定。

本文旨在系统性地剖析[行动者-评论家](@entry_id:634214)与[策略优化](@entry_id:635350)方法的全貌，引领读者从基础理论走向前沿应用。我们将分三个章节展开：
*   在**“原理与机制”**中，我们将从[策略梯度定理](@entry_id:635009)的第一性原理出发，揭示其内在的挑战，并逐步引出作为解决方案的[行动者-评论家](@entry_id:634214)架构、[优势函数](@entry_id:635295)估计以及如PPO和SAC等现代算法的核心思想。
*   在**“应用与[交叉](@entry_id:147634)学科联系”**中，我们将探索这些理论如何被应用于解决机器人学、计算金融、[系统工程](@entry_id:180583)等领域的实际问题，并展示其如何与好奇心驱动探索、事后[经验回放](@entry_id:634839)（HER）、安全约束等高级概念相结合。
*   最后，在**“动手实践”**部分，我们将通过一系列精心设计的编程练习，将理论知识转化为解决具体问题的实践能力。

通过本次学习，您将不仅掌握[行动者-评论家方法](@entry_id:178939)的工作原理，更能理解其在应对真实世界复杂性时所展现出的灵活性与强大潜力。

## 原理与机制

在前一章中，我们介绍了强化学习的基本框架。现在，我们将深入探讨一类特别强大且广泛应用的算法：[策略优化](@entry_id:635350)与[行动者-评论家](@entry_id:634214)（Actor-Critic）方法。与基于价值的方法（如Q-learning）试图学习最优行动[价值函数](@entry_id:144750)不同，[策略优化](@entry_id:635350)方法直接对策略本身进行参数化，并通过梯度上升来最大化预期的累积回报。本章将从[策略梯度](@entry_id:635542)的基本定理出发，系统地阐述其核心挑战（如高[方差](@entry_id:200758)问题），并逐步引出[行动者-评论家](@entry_id:634214)架构、高级优势估计技术，最终介绍如PPO、DPG和[最大熵](@entry_id:156648)强化学习等现代前沿算法的原理与机制。

### [策略梯度](@entry_id:635542)的基本原理

[策略优化](@entry_id:635350)方法的核心思想是，将策略 $\pi$ 表示为一个由参数 $\theta$ 控制的函数 $\pi_\theta(a|s)$，该函数在给定状态 $s$ 时输出一个关于行动 $a$ 的[概率分布](@entry_id:146404)。我们的目标是找到一组参数 $\theta$，以最大化性能[目标函数](@entry_id:267263) $J(\theta)$，该函数通常定义为智能体在一个完整回合（episode）中能够获得的期望累积回报。对于一个持续时间为 $T$ 的回合，其目标函数可以写作：
$$J(\theta) = \mathbb{E}_{\tau \sim p_{\theta}(\tau)}\left[\sum_{t=0}^{T-1} r(s_t, a_t)\right]$$
其中，$\tau = (s_0, a_0, s_1, a_1, \dots)$ 代表一个由策略 $\pi_\theta$ 和环境动态共同作用产生的轨迹（trajectory），$p_{\theta}(\tau)$ 是在参数 $\theta$ 下该轨迹发生的概率。

为了通过梯度上升法优化 $\theta$，我们必须计算[目标函数](@entry_id:267263)关于参数的梯度 $\nabla_\theta J(\theta)$。直接对这个期望求导似乎很困难，因为轨迹的[概率分布](@entry_id:146404) $p_\theta(\tau)$ 本身就依赖于 $\theta$。然而，通过一个被称为**“log-derivative trick”**（[对数导数技巧](@entry_id:751429)）的关键数学恒等式，我们可以将梯度重写为一个期望的形式，从而允许我们使用[蒙特卡洛采样](@entry_id:752171)来估计它。这个重要的结果被称为**[策略梯度定理](@entry_id:635009)（Policy Gradient Theorem）**。

我们可以从第一性原理出发推导出该定理 [@problem_id:3094818]。首先，我们将期望写成积分（或求和）形式，然后对积分内的项求导：
$$\nabla_{\theta} J(\theta) = \nabla_{\theta} \int p_{\theta}(\tau) R(\tau) d\tau = \int (\nabla_{\theta} p_{\theta}(\tau)) R(\tau) d\tau$$
其中 $R(\tau) = \sum_{t=0}^{T-1} r(s_t, a_t)$ 是轨迹的总回报。利用恒等式 $\nabla_x f(x) = f(x) \nabla_x \log f(x)$，我们可以得到 $\nabla_{\theta} p_{\theta}(\tau) = p_{\theta}(\tau) \nabla_{\theta} \log p_{\theta}(\tau)$。代入上式，我们有：
$$\nabla_{\theta} J(\theta) = \int p_{\theta}(\tau) (\nabla_{\theta} \log p_{\theta}(\tau)) R(\tau) d\tau = \mathbb{E}_{\tau \sim p_{\theta}(\tau)}\left[ (\nabla_{\theta} \log p_{\theta}(\tau)) R(\tau) \right]$$
轨迹的概率 $p_\theta(\tau)$ 可以分解为初始状态概率和一系列策略概率与状态转移概率的乘积。由于环境的动态 $p(s_{t+1}|s_t, a_t)$ 不依赖于策略参数 $\theta$，其对数梯度 $\nabla_\theta \log p_\theta(\tau)$ 可以简化为：
$$\nabla_{\theta} \log p_{\theta}(\tau) = \nabla_{\theta} \left( \log \rho(s_0) + \sum_{t=0}^{T-1} \log \pi_{\theta}(a_t | s_t) \right) = \sum_{t=0}^{T-1} \nabla_{\theta} \log \pi_{\theta}(a_t | s_t)$$
$\nabla_{\theta} \log \pi_{\theta}(a_t | s_t)$ 通常被称为**[得分函数](@entry_id:164520)（score function）**。将此结果代入，并利用因果关系（即在时间步 $t$ 的决策只影响未来的回报），我们可以将整个轨迹的回报 $R(\tau)$ 替换为从该时间步开始的未来回报，即**行动[价值函数](@entry_id:144750)** $Q^\pi(s_t, a_t)$。最终，[策略梯度定理](@entry_id:635009)可以简洁地表达为：
$$\nabla_{\theta} J(\theta) = \mathbb{E}_{s \sim d^{\pi}, a \sim \pi_{\theta}}\left[\nabla_{\theta} \log \pi_{\theta}(a | s) Q^{\pi}(s, a)\right]$$
其中 $d^\pi$ 是策略 $\pi_\theta$ 下的状态访问[分布](@entry_id:182848)。

这个定理非常强大，因为它将一个难以处理的关于[分布](@entry_id:182848)的梯度问题，转化为了一个可以通过从环境中采样 $(s, a)$ 并估计 $Q^{\pi}(s, a)$ 来近似的期望。最简单的[策略梯度](@entry_id:635542)算法，**REINFORCE**（或称为蒙特卡洛[策略梯度](@entry_id:635542)），正是基于此。它在每个回合结束后，使用整个回合的实际观测回报 $G_t = \sum_{k=t}^{T-1} \gamma^{k-t} r_k$作为 $Q^\pi(s_t, a_t)$ 的一个无偏估计，然后更新策略参数：
$$\theta \leftarrow \theta + \alpha \sum_{t=0}^{T-1} \nabla_{\theta} \log \pi_{\theta}(a_t | s_t) G_t$$

### [方差缩减](@entry_id:145496)：基[线与](@entry_id:177118)[优势函数](@entry_id:635295)

尽管REINFOR[CE算法](@entry_id:178177)在理论上是无偏的，但它在实践中面临一个严重的问题：[梯度估计](@entry_id:164549)的**高[方差](@entry_id:200758)**。因为蒙特卡洛回报 $G_t$ 的值在不同回合之间可能有巨大波动，这会导致[梯度估计](@entry_id:164549)非常不稳定，使得学习过程缓慢且难以收敛。

为了解决这个问题，我们可以引入一个**基线（baseline）**函数 $b(s)$，它只依赖于状态 $s$ 而不依赖于行动 $a$。我们将[策略梯度](@entry_id:635542)估计器修改为：
$$\nabla_{\theta} J(\theta) = \mathbb{E}\left[\nabla_{\theta} \log \pi_{\theta}(a | s) (Q^{\pi}(s, a) - b(s))\right]$$
这个修改并不会引入偏差，因为基线项的期望为零 [@problem_id:3094822]。我们可以证明这一点：
$$\mathbb{E}_{a \sim \pi_\theta(\cdot|s)}\left[\nabla_{\theta} \log \pi_{\theta}(a | s) b(s)\right] = b(s) \int \pi_{\theta}(a|s) \frac{\nabla_\theta \pi_\theta(a|s)}{\pi_\theta(a|s)} da = b(s) \nabla_\theta \int \pi_\theta(a|s) da = b(s) \nabla_\theta (1) = 0$$
既然基线不改变梯度的期望，我们可以选择一个合适的 $b(s)$ 来最小化[梯度估计](@entry_id:164549)的[方差](@entry_id:200758)。一个直观且非常有效的选择是状态价值函数 $V^\pi(s)$。$V^\pi(s)$ 定义为在状态 $s$ 之后遵循策略 $\pi$ 所能获得的期望回报。它与 $Q^\pi(s,a)$ 之间存在一个基本关系 [@problem_id:2738651]：
$$V^\pi(s) = \mathbb{E}_{a \sim \pi(\cdot|s)}[Q^\pi(s,a)] = \sum_a \pi(a|s) Q^\pi(s,a)$$
这个关系表明，一个状态的价值是在该状态下，根据策略 $\pi$ 采取所有可能行动的价值的期望。

使用 $V^\pi(s)$ 作为基线后，[策略梯度](@entry_id:635542)中的项 $Q^\pi(s,a) - V^\pi(s)$ 有了一个特殊的名称：**[优势函数](@entry_id:635295)（Advantage Function）**，记作 $A^\pi(s,a)$。
$$A^\pi(s,a) = Q^\pi(s,a) - V^\pi(s)$$
[优势函数](@entry_id:635295)直观地衡量了在状态 $s$ 下，采取特定行动 $a$ 相对于遵循当前策略 $\pi$ 的平均表现要好多少。如果 $A^\pi(s,a) > 0$，则说明行动 $a$ 比平均行动要好，我们应该增加选择它的概率。反之，如果 $A^\pi(s,a) < 0$，我们则应该减少选择它的概率。使用[优势函数](@entry_id:635295)不仅能显著降低[方差](@entry_id:200758)，还能提供更清晰的信用分配信号。一个重要的性质是，[优势函数](@entry_id:635295)在策略 $\pi$ 下的期望为零：$\mathbb{E}_{a \sim \pi(\cdot|s)}[A^\pi(s,a)] = 0$ [@problem_id:2738651]。

### [行动者-评论家方法](@entry_id:178939)

引入[优势函数](@entry_id:635295)将我们自然地引向了**[行动者-评论家](@entry_id:634214)（Actor-Critic）**方法。在这种框架下，学习过程由两个部分协同完成：

1.  **行动者（Actor）**：负责学习和更新策略 $\pi_\theta(a|s)$。它根据评论家提供的信息来调整其参数 $\theta$，目标是做出能带来更高回报的决策。
2.  **评论家（Critic）**：负责学习和评估[价值函数](@entry_id:144750)，通常是状态[价值函数](@entry_id:144750) $V_\phi(s)$ 或行动价值函数 $Q_\phi(s,a)$，由参数 $\phi$ 控制。它通过观察环境的反馈（奖励）来评估当前策略的好坏，并为行动者提供指导信号（例如，[优势函数](@entry_id:635295)）。

最简单的[行动者-评论家](@entry_id:634214)算法使用单步时序差分（TD）误差作为[优势函数](@entry_id:635295)的估计。[TD误差](@entry_id:634080) $\delta_t$ 定义为：
$$\delta_t = r_t + \gamma V_\phi(s_{t+1}) - V_\phi(s_t)$$
$\delta_t$ 是一个有偏但[方差](@entry_id:200758)较低的对 $A^\pi(s_t, a_t)$ 的估计。行动者使用这个信号来更新策略，而评论家则使用这个[TD误差](@entry_id:634080)来更新自身的价值函数估计，通常是通过最小化[TD误差](@entry_id:634080)的平方。

行动者和评论家是相互依存的。行动者的策略决定了评论家观察到的数据，而评论家的评估则直接指导行动者的更新。然而，这种相互依赖也带来了挑战。如果评论家由于学习不足而产生了一个**有偏（biased）**的价值估计，它可能会误导行动者，使其收敛到一个次优的策略。一个精心设计的简单场景就可以揭示这种风险 [@problem_id:3094900]：在一个两状态MDP中，如果评论家因为初始探索不足和TD学习的步长限制，对一个高回报的远端状态的价值产生了严重低估（即存在巨大的**自举偏差（bootstrapping bias）**），行动者可能会错误地认为通往该状态的路径是不值得的，从而永久地选择了一个局部最优但在全局看来是次优的策略。这突显了评论家估计的准确性对于整个算法成功的重要性。

### 高级优势估计

正如我们所见，[优势函数](@entry_id:635295)的估计是[行动者-评论家方法](@entry_id:178939)的核心。简单的单步[TD误差](@entry_id:634080)（如 $\delta_t$）[方差](@entry_id:200758)小但偏差大，而完整的[蒙特卡洛](@entry_id:144354)回报 $G_t$ 偏差小但[方差](@entry_id:200758)大。这构成了强化学习中一个经典的**偏差-方差权衡（bias-variance tradeoff）**。

为了更好地平衡这一点，我们可以使用**n步回报（n-step returns）**来构造优势估计。一个n步回报目标 $G_t^{(n)}$ 是通过观察未来 $n$ 步的实际奖励，并用第 $n+1$ 步的[价值函数](@entry_id:144750)估计进行自举（bootstrap）来构建的：
$$G_t^{(n)} = \sum_{k=0}^{n-1} \gamma^k r_{t+k} + \gamma^n V_\phi(s_{t+n})$$
当 $n=1$ 时，这就是单步TD目标。当 $n \to \infty$ 时，它就变成了蒙特卡洛回报。通过调整 $n$，我们可以在[偏差和方差](@entry_id:170697)之间进行权衡 [@problem_id:3094906]。选择一个中等的 $n$ 值通常能在实践中取得比纯TD或纯蒙特卡洛更好的效果。

**广义优势估计（Generalized Advantage Estimation, GAE）** [@problem_id:3094793] 将这一思想推广到了极致。GAE通过引入一个额外的参数 $\lambda \in [0,1]$，对所有不同步数 $n$ 的优势估计进行指数加权平均：
$$A_t^{\text{GAE}(\gamma, \lambda)} = \sum_{l=0}^{\infty} (\gamma \lambda)^l \delta_{t+l}$$
其中 $\delta_{t+l} = r_{t+l} + \gamma V_\phi(s_{t+l+1}) - V_\phi(s_{t+l})$ 是在未来时间步 $t+l$ 的[TD误差](@entry_id:634080)。这个公式看起来很复杂，但它有两个直观的特例：
-   当 $\lambda=0$ 时，GAE估计退化为单步[TD误差](@entry_id:634080)：$A_t^{\text{GAE}(\gamma, 0)} = \delta_t$。这是一个高偏差、低[方差](@entry_id:200758)的估计。
-   当 $\lambda=1$ 时，GAE估计等价于[蒙特卡洛](@entry_id:144354)回报减去一个基线：$A_t^{\text{GAE}(\gamma, 1)} = \sum_{l=0}^{\infty} \gamma^l r_{t+l} - V_\phi(s_t)$。这是一个低偏差（如果 $V_\phi$ 是准确的，甚至是无偏的）、高[方差](@entry_id:200758)的估计。

通过调整 $\lambda$ 在0和1之间，GAE为我们提供了一个平滑控制[偏差-方差权衡](@entry_id:138822)的旋钮。在实践中，使用GAE的[行动者-评论家](@entry_id:634214)算法（如A2C）通常比使用简单[TD误差](@entry_id:634080)的算法表现更稳定、更高效。这在数值实验中可以被清晰地观察到，通过比较不同算法[梯度估计](@entry_id:164549)的[信噪比](@entry_id:185071)，我们发现使用更高级优势估计的A2C和PPO通常优于原始的REINFORCE [@problem_id:3094823]。

### 现代[策略优化](@entry_id:635350)算法

基于上述原理，研究者们开发了多种先进的[策略优化](@entry_id:635350)算法，这些算法在各种复杂任务中取得了巨大成功。

#### 信任区域与近端[策略优化](@entry_id:635350)

一个朴素的[策略梯度](@entry_id:635542)更新可能会因为单次更新步长过大而彻底破坏当前策略，导致性能的灾难性下降。**信任区域[策略优化](@entry_id:635350)（Trust Region Policy Optimization, TRPO）** [@problem_id:3094827] 通过在每次更新时施加一个约束来解决这个问题，该约束要求新旧策略之间的差异（通常用**KL散度**衡量）不能超过一个小的阈值 $\delta$：
$$\max_{\theta} \ \mathbb{E}\left[ \frac{\pi_\theta(a|s)}{\pi_{\theta_{\text{old}}}(a|s)} A_t \right] \quad \text{subject to} \quad \mathbb{E}_s\left[ D_{\mathrm{KL}}(\pi_{\theta_{\text{old}}}(\cdot|s) \| \pi_{\theta}(\cdot|s)) \right] \le \delta$$
TRPO使用**自然梯度（natural gradient）**来求解这个约束优化问题，这涉及到计算和求逆**[费雪信息矩阵](@entry_id:750640)（Fisher Information Matrix）**，计算开销巨大。

**近端[策略优化](@entry_id:635350)（Proximal Policy Optimization, PPO）** 是一种更简单、但效果同样出色的算法。PPO旨在实现TRPO的稳定更新，但只使用一阶优化。PPO最常见的变体是使用一个**裁剪的替代[目标函数](@entry_id:267263)（clipped surrogate objective）**：
$$L^{\text{CLIP}}(\theta) = \mathbb{E}_t\left[ \min\left( r_t(\theta) A_t, \ \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) A_t \right) \right]$$
其中 $r_t(\theta) = \frac{\pi_\theta(a_t|s_t)}{\pi_{\theta_{\text{old}}}(a_t|s_t)}$ 是新旧策略的概率比，$\epsilon$ 是一个小的超参数（如0.2）。这个目标函数通过裁剪概率比来惩罚过大的策略更新。如果优势 $A_t$ 是正的，目标函数在 $r_t(\theta)$ 增长到 $1+\epsilon$ 后就被限制住；如果 $A_t$ 是负的，目标函数在 $r_t(\theta)$ 减小到 $1-\epsilon$ 后被限制。这种机制有效地将策略更新限制在一个“信任区域”内，从而实现了稳定而高效的学习。

#### 确定性[策略梯度](@entry_id:635542)与探索问题

到目前为止，我们讨论的都是**随机策略（stochastic policies）**。在拥有连续动作空间的环境中，另一种选择是学习一个**确定性策略（deterministic policy）** $a = \mu_\theta(s)$。**确定性[策略梯度](@entry_id:635542)（Deterministic Policy Gradient, DPG）**定理 [@problem_id:3094787] 表明，其梯度可以直接通过[链式法则](@entry_id:190743)得到，而无需对动作空间进行积分：
$$\nabla_{\theta} J(\theta) = \mathbb{E}_{s \sim d^\mu}\left[ \nabla_{\theta} \mu_{\theta}(s) \nabla_a Q^{\mu}(s,a)|_{a=\mu_\theta(s)} \right]$$
DPG算法通常比随机[策略梯度](@entry_id:635542)算法有更高的数据效率，因为它不需要在动作空间上进行采样。然而，DPG也面临一个严重的问题：**探索不足**。由于策略是确定性的，它不会主动尝试当前策略认为不是最优的动作。如果智能体在一个局部最优点附近，其梯度可能为零，导致它被困住，而无法发现远处可能存在更高回报的区域。相比之下，随机策略由于其内在的随机性，总是有机会探索到新的动作。在一个[奖励函数](@entry_id:138436)具有平坦区域或稀疏奖励的场景中，DPG的这一弱点尤为明显，而随机[策略梯度](@entry_id:635542)（SPG）则可能凭借其探索能力成功找到优化方向 [@problem_id:3094787]。为了解决这个问题，基于DPG的算法（如DDPG）通常会引入[离策略学习](@entry_id:634676)（off-policy learning）和在训练时向确定性动作中注入噪声来保证充分的探索。

#### [熵正则化](@entry_id:749012)与[最大熵](@entry_id:156648)[强化学习](@entry_id:141144)

另一种鼓励探索的强大机制是**[熵正则化](@entry_id:749012)（entropy regularization）**。其核心思想是在最大化累积回报的同时，也最大化策略的**熵（entropy）**。策略的熵衡量了其随机性或不确定性；一个高熵的策略会以更均匀的概率选择所有动作，从而进行更广泛的探索。

正则化后的[目标函数](@entry_id:267263)变为：
$$J(\pi) = \mathbb{E}_{\tau \sim \pi}\left[ \sum_t r(s_t, a_t) + \alpha H(\pi(\cdot|s_t)) \right]$$
其中 $H(\pi(\cdot|s_t))$ 是策略在状态 $s_t$ 的熵，$\alpha > 0$ 是一个控制[熵正则化](@entry_id:749012)强度的温度参数。

可以证明，对于一个单步决策问题，最大化这个正则化目标将得到一个**softmax策略** [@problem_id:3094842]：
$$\pi_\alpha(a|s) = \frac{\exp(r(a)/\alpha)}{\sum_{b} \exp(r(b)/\alpha)}$$
这里的回报 $r(a)$ 可以被泛化为[Q值](@entry_id:265045) $Q(s,a)$。这个结果揭示了温度参数 $\alpha$ 的作用：
-   当 $\alpha \to 0$ 时，策略变得贪婪，几乎所有概率都集中在拥有最高回报的动作上，趋近于标准的最优策略。
-   当 $\alpha \to \infty$ 时，策略变得完全均匀，对所有动作一视同仁，进行最大程度的探索。

通过在训练过程中调整 $\alpha$（或将其作为可学习的参数），智能体可以在学习初期进行广泛探索，而在学习后期逐渐收敛到更优的策略。这一原理是**软[行动者-评论家](@entry_id:634214)（Soft Actor-Critic, SAC）**等现代算法的基石，这些算法在许多具有挑战性的连续控制任务中取得了顶尖的性能。