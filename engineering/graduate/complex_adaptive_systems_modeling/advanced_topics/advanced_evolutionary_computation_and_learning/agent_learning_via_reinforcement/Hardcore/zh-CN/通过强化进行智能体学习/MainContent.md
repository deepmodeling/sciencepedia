## 引言
智能体如何在一个不确定的环境中，通过与环境的反复试错交互，自主地学习以实现特定目标？这是人工智能和认知科学领域的一个根本问题。[强化学习](@entry_id:141144)（Reinforcement Learning, RL）为解答这一问题提供了一个强大而普适的计算框架。它研究智能体（agent）如何基于环境反馈的奖励或惩罚信号，逐步优化其行为策略（policy），最终目的是最大化长期累积奖励。这种学习范式不仅是构建智能机器人的关键技术，也为我们理解生物乃至人类的学习机制提供了深刻的见解。

本文旨在系统性地介绍智能体强化学习的理论、应用与实践。我们将从最基本的数学原理出发，逐步深入到前沿的算法和跨学科应用。读者将通过本文的学习，构建一个关于强化学习的完整知识体系。

在“原理与机制”一章中，我们将奠定理论基础，详细阐述将决策问题形式化为马尔可夫决策过程（MDP）的方法，并探讨[贝尔曼方程](@entry_id:1121499)以及求解它的核心算法，包括[动态规划](@entry_id:141107)、无模型学习和[策略梯度](@entry_id:635542)等。

接着，在“应用与交叉学科联系”一章中，我们将展示[强化学习](@entry_id:141144)如何跨越学科界限，在[工程控制](@entry_id:177543)、[计算金融](@entry_id:145856)、神经科学乃至AI安[全等](@entry_id:273198)多个领域提供解决方案和洞见，揭示其作为一种通用适应性理论的广泛影响力。

最后，在“动手实践”部分，我们提供了一系列精心设计的编程练习，引导读者将理论知识付诸实践，通过解决具体问题来深化对核心概念（如奖励塑形和[离策略评估](@entry_id:181976)）的理解。

让我们从核心问题——智能体如何学习最大化未来奖励——开始，深入探索[强化学习](@entry_id:141144)的原理与机制。

## 原理与机制

本章旨在阐述[强化学习](@entry_id:141144)中[智能体学习](@entry_id:1120882)的核心原理与机制。我们将从最大化未来奖励这一根本目标出发，逐步建立马尔可夫决策过程的数学框架，并深入探讨求解最优策略的各种算法。内容将涵盖[动态规划](@entry_id:141107)、无模型学习、[函数近似](@entry_id:141329)以及[策略梯度方法](@entry_id:634727)，最终延伸至[多智能体系统](@entry_id:170312)的复杂情境。

### 核心问题：最大化未来奖励

强化学习的中心思想是，一个**智能体 (agent)** 通过与**环境 (environment)** 的交互来学习一个**策略 (policy)**，以最大化其在未来收到的累积**奖励 (reward)** 信号。智能体在每个时间步 $t$ 观察到一个状态 $S_t$，选择一个动作 $A_t$，然后收到一个标量奖励 $R_{t+1}$ 并转移到一个新的状态 $S_{t+1}$。我们如何量化“累积未来奖励”这一概念呢？这个量被称为**回报 (return)**，记为 $G_t$。

一个通用的回报形式可以写成未来奖励的加权和：
$$G_t = \mathbb{E}\left[\sum_{k=0}^{\infty} w_k R_{t+k+1}\right]$$
其中 $w_k$ 是仅取决于延迟 $k$ 的权重。为了使这一评价标准在理论上稳健且实用，我们要求它满足一些基本公理 。例如，**平稳性 (stationarity)** 要求偏好不随时间改变，这已体现在权重 $w_k$ 仅依赖于 $k$。**动态一致性 (dynamic consistency)** 是一个更强的要求，它规定从任何时间点开始对策略的排序，与从初始时间点对相应尾部奖励序列的排序应保持一致。这一公理意味着权重序列必须是成比例的，即存在一个常数 $\gamma > 0$ 使得 $w_{k+1} = \gamma \cdot w_k$ 对所有 $k \ge 0$ 成立。结合 $w_0=1$ 的归一化假设，我们得到权重必须是[几何级数](@entry_id:158490)形式：$w_k = \gamma^k$。

此外，**有限估值 (finite valuation)** 公理要求对于任何有界的奖励序列，回报的[期望值](@entry_id:150961)都应是有限的。这要求权重级数 $\sum_{k=0}^{\infty} w_k = \sum_{k=0}^{\infty} \gamma^k$ 收敛。[几何级数](@entry_id:158490)收敛的条件是 $|\gamma| < 1$。结合 $\gamma > 0$（因为我们假设所有权重 $w_k$ 均为正，以保持奖励的偏好顺序），我们得出结论：折扣因子 $\gamma$ 必须满足 $0  \gamma  1$。

因此，这些基本公理共同指向了[强化学习](@entry_id:141144)中最标准的回报形式——**[折扣](@entry_id:139170)回报 (discounted return)**：
$$G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$$
其中 $\gamma \in [0, 1)$ 被称为**折扣因子 (discount factor)**。它衡量了未来奖励相对于即时奖励的重要性。当 $\gamma$ 接近 0 时，智能体更关注即时奖励（“短视”）；当 $\gamma$ 接近 1 时，智能体更关注长远未来的奖励（“[远视](@entry_id:178735)”）。

### 交互的规范化：[马尔可夫决策过程](@entry_id:140981)

为了严谨地分析智能体的决策问题，我们通常将其环境建模为**[马尔可夫决策过程](@entry_id:140981) (Markov Decision Process, MDP)**。一个 MDP 由一个元组 $(\mathcal{S}, \mathcal{A}, P, R, \gamma)$ 定义：
- $\mathcal{S}$ 是一个有限的**状态 (state)** 集合。
- $\mathcal{A}$ 是一个有限的**动作 (action)** 集合。
- $P(s' \mid s, a) = \Pr(S_{t+1}=s' \mid S_t=s, A_t=a)$ 是**状态转移概率**，描述了在状态 $s$ 采取动作 $a$ 后转移到状态 $s'$ 的概率。它满足**[马尔可夫性质](@entry_id:139474)**，即未来只依赖于当前的状态和动作，而与过去无关。
- $R(s, a) = \mathbb{E}[R_{t+1} \mid S_t=s, A_t=a]$ 是**奖励函数**，表示在状态 $s$ 采取动作 $a$ [后期](@entry_id:165003)望获得的即时奖励。
- $\gamma \in [0, 1)$ 是之前讨论过的折扣因子。

智能体的行为由其**策略 (policy)** $\pi(a \mid s) = \Pr(A_t=a \mid S_t=s)$ 定义，即在每个状态下选择动作的概率分布。强化学习的目标是找到一个**[最优策略](@entry_id:138495)** $\pi^*$，使得从任何初始状态出发，期望的[折扣](@entry_id:139170)回报都最大化。

为了评估一个策略的好坏，我们定义了**价值函数 (value function)**。**状态[价值函数](@entry_id:144750) (state-value function)** $V^\pi(s)$ 是从状态 $s$ 开始，遵循策略 $\pi$ 所能获得的期望回报：
$$V^\pi(s) = \mathbb{E}_\pi\left[G_t \mid S_t=s\right] = \mathbb{E}_\pi\left[\sum_{k=0}^{\infty} \gamma^k R_{t+k+1} \mid S_t=s\right]$$
类似地，**动作价值函数 (action-value function)** $Q^\pi(s, a)$ 是从状态 $s$ 开始，采取动作 $a$，然后遵循策略 $\pi$ 所能获得的期望回报：
$$Q^\pi(s, a) = \mathbb{E}_\pi\left[G_t \mid S_t=s, A_t=a\right] = \mathbb{E}_\pi\left[\sum_{k=0}^{\infty} \gamma^k R_{t+k+1} \mid S_t=s, A_t=a\right]$$

价值函数满足一种递归关系，称为**贝尔曼期望方程 (Bellman expectation equation)**：
$$V^\pi(s) = \sum_{a \in \mathcal{A}} \pi(a \mid s) \left( R(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) V^\pi(s') \right)$$
$$Q^\pi(s, a) = R(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) \sum_{a' \in \mathcal{A}} \pi(a' \mid s') Q^\pi(s', a')$$
这些方程将一个状态（或状态-动作对）的价值与其后继状态的价值联系起来。对于一个给定的策略 $\pi$，价值函数是该线性方程组的唯一解。

我们的最终目标是找到一个[最优策略](@entry_id:138495) $\pi^*$，其对应的[价值函数](@entry_id:144750) $V^*(s) = \max_\pi V^\pi(s)$ 和 $Q^*(s, a) = \max_\pi Q^\pi(s, a)$ 是所有策略中最大的。最优[价值函数](@entry_id:144750)满足**贝尔曼最优方程 (Bellman optimality equation)**：
$$V^*(s) = \max_{a \in \mathcal{A}} \left( R(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) V^*(s') \right)$$
$$Q^*(s, a) = R(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) \max_{a' \in \mathcal{A}} Q^*(s', a')$$
与贝尔曼期望方程不同，最优方程由于 `max` 算子的存在而是[非线性](@entry_id:637147)的。一旦我们求得了 $V^*$ 或 $Q^*$，最优策略就可以通过贪心选择得到：
$$\pi^*(s) \in \arg\max_{a \in \mathcal{A}} \left( R(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) V^*(s') \right)$$

为了具体理解这些方程，我们来看一个例子 。考虑一个包含状态 $\mathcal{S} = \{s_0, s_1, s_2, s_{\mathrm{T}}\}$ 的 MDP，其中 $s_{\mathrm{T}}$ 是一个终止状态，$V^*(s_{\mathrm{T}})=0$，折扣因子 $\gamma = \frac{1}{2}$。动态和奖励如下：
- $s_0$: 动作 $a$ 得到奖励 1，转移到 $s_1$；动作 $b$ 得到奖励 0，转移到 $s_{\mathrm{T}}$。
- $s_1$: 动作 $c$ 得到奖励 3，以概率 $\frac{1}{2}$ 回到 $s_1$，$\frac{1}{2}$ 到 $s_2$；动作 $d$ 得到奖励 5，转移到 $s_{\mathrm{T}}$。
- $s_2$: 动作 $e$ 得到奖励 2，转移到 $s_0$。

我们可以为 $V^*(s_0)$、$V^*(s_1)$ 和 $V^*(s_2)$ 写出贝尔曼最优方程：
$V^*(s_2) = 2 + \frac{1}{2} V^*(s_0)$ （因为只有一个动作）
$V^*(s_1) = \max \left\{ 3 + \frac{1}{2} (\frac{1}{2} V^*(s_1) + \frac{1}{2} V^*(s_2)), 5 + \frac{1}{2} V^*(s_{\mathrm{T}}) \right\}$
$V^*(s_0) = \max \left\{ 1 + \frac{1}{2} V^*(s_1), 0 + \frac{1}{2} V^*(s_{\mathrm{T}}) \right\}$

假设 $V^*(s_1) \ge 0$，则 $V^*(s_0)$ 的方程简化为 $V^*(s_0) = 1 + \frac{1}{2} V^*(s_1)$。将此代入 $V^*(s_2)$ 的方程，得到 $V^*(s_2) = 2 + \frac{1}{2}(1 + \frac{1}{2}V^*(s_1)) = \frac{5}{2} + \frac{1}{4}V^*(s_1)$。再将 $V^*(s_2)$ 的表达式代入 $V^*(s_1)$ 的方程中：
$V^*(s_1) = \max \left\{ 3 + \frac{1}{4} V^*(s_1) + \frac{1}{4} (\frac{5}{2} + \frac{1}{4}V^*(s_1)), 5 \right\} = \max \left\{ \frac{29}{8} + \frac{5}{16} V^*(s_1), 5 \right\}$
这是一个关于 $V^*(s_1)$ 的方程。通过求解，我们发现 $V^*(s_1) = \frac{58}{11}$。这个解是通过假设 $\frac{29}{8} + \frac{5}{16} V^*(s_1)  5$ 并验证其一致性得到的。最后，我们可以计算出我们关心的值：
$V^*(s_0) = 1 + \frac{1}{2} V^*(s_1) = 1 + \frac{1}{2} \left( \frac{58}{11} \right) = \frac{40}{11}$
这个例子展示了如何利用贝尔曼最优方程，将一个[序贯决策问题](@entry_id:136955)转化为一个可以求解的方程组。

### 寻找最优策略：[动态规划](@entry_id:141107)及其他

如果 MDP 的模型（即 $P$ 和 $R$）是已知的，我们可以使用**动态规划 (Dynamic Programming, DP)** 方法来求解贝尔曼最优方程。主要算法有两种：
- **[价值迭代](@entry_id:146512) (Value Iteration)**：通过迭代更新价值函数 $V_{k+1}(s) = \max_a \left( R(s, a) + \gamma \sum_{s'} P(s' \mid s, a) V_k(s') \right)$，可以证明 $V_k$ 会收敛到 $V^*$。
- **策略迭代 (Policy Iteration)**：在“[策略评估](@entry_id:136637)”和“[策略改进](@entry_id:139587)”两个步骤之间交替进行。首先为当前策略 $\pi_k$ 计算 $V^{\pi_k}$，然后根据 $V^{\pi_k}$ 贪心地改进策略得到 $\pi_{k+1}$。

然而，对于没有明确结束的持续性任务，折扣回报可能不适用。在这种情况下，我们通常最大化**平均回报 (average reward)**：
$$g_\pi(s) = \lim_{n \to \infty} \frac{1}{n} \mathbb{E}_{\pi}\left[\sum_{t=0}^{n-1} r(S_t, A_t) \mid S_0=s\right]$$
在某些结构性假设下（例如，MDP 是连通的，并且任何平稳策略都诱导一个单链马尔可夫链），这个长期平均回报对于所有初始状态 $s$ 都是一个常数 $g_\pi$ 。

平均回报框架下的贝尔曼最优方程变为：
$$g^* + h^*(s) = \max_{a \in \mathcal{A}} \left\{ R(s,a) + \sum_{s' \in \mathcal{S}} P(s' \mid s,a) h^*(s') \right\}$$
这里的 $g^*$ 是最优平均回报，也称为**增益 (gain)**，而 $h^*(s)$ 是**偏差 (bias)** 或[微分](@entry_id:158422)价值函数。与[折扣](@entry_id:139170)情况不同，偏差函数 $h^*$ 并非唯一，它只在相差一个常数的意义下是唯一的。此外，相应的贝尔曼算子在通常的[无穷范数](@entry_id:637586)下不再是[压缩映射](@entry_id:139989)，这使得标准[价值迭代](@entry_id:146512)算法会发散。

为了解决这个问题，需要使用一种称为**相对[价值迭代](@entry_id:146512) (Relative Value Iteration, RVI)** 的算法。该算法在每次迭代后都将[价值函数](@entry_id:144750)进行归一化，例如减去某个参考状态 $s_0$ 的价值：
$h_{k+1}(s) = \max_a \left\{ R(s,a) + \sum_{s'} P(s' \mid s,a) h_k(s') \right\} - c_k$
其中 $c_k = \max_a \left\{ R(s_0,a) + \sum_{s'} P(s' \mid s_0,a) h_k(s') \right\}$。在适当的条件下，RVI 能够保证偏差[函数序列](@entry_id:145607) $h_k$ 收敛到一个最优偏差函数 $h^*$，而被减去的标量序列 $c_k$ 则收敛到最优增益 $g^*$ 。

### 从经验中学习：无模型方法

动态规划算法要求我们完全了解环境的模型，这在许多现实问题中是不现实的。**无模型 (model-free)** 强化学习方法则直接从智能体与环境交互的经验中学习价值函数和策略，而无需显式地估计转移概率和奖励函数。

最简单的无模型学习问题是**多臂老虎机 (Multi-Armed Bandit, MAB)**。智能体面临 K 个选项（“臂”），每次选择一个臂可以获得一个随机奖励。目标是在 T 轮交互中最大化累积奖励。这个问题是[探索与利用](@entry_id:174107)困境 (exploration-exploitation dilemma) 的一个纯粹形式：智能体应该利用当前看起来最好的臂，还是探索其他可能更好的臂？

为了量化算法的性能，我们引入**累积遗憾 (cumulative regret)** $R_T$ 的概念，它是在 T 轮中，始终选择最优臂所能获得的期望奖励与智能体实际获得的期望奖励之间的差值。一个好的算法应该有次线性增长的遗憾。一个关键的理论结果是，对于任何足够好的算法，其累积遗憾存在一个对数增长的下界 。
$$R_T \ge \left( \sum_{i: \mu_i  \mu^*} \frac{\mu^* - \mu_i}{D_{KL}(\mathcal{B}(\mu_i) || \mathcal{B}(\mu^*))} \right) \ln T + o(\ln T)$$
这里的 $\mu_i$ 是臂 $i$ 的平均奖励，$\mu^*$ 是最优臂的平均奖励，$D_{KL}(\mathcal{B}(p) || \mathcal{B}(q))$ 是两个均值分别为 $p$ 和 $q$ 的[伯努利分布](@entry_id:266933)之间的**Kullback-Leibler (KL) 散度**。这个下界告诉我们，为了可靠地识别出最优臂，智能体必须为每个次优臂 $i$ 至少拉动 $\frac{\ln T}{D_{KL}}$ 次。区分两个臂的难度由它们的奖励分布之间的 KL 散度来衡量。

回到完整的 MDP 问题，**时序差分 (Temporal-Difference, TD) 学习**是无模型方法的核心。TD 学习通过使用当前价值函数的估计来更新自身，即所谓的**自举 (bootstrapping)**。最简单的 TD 算法是 TD(0)，用于评估一个给定的策略 $\pi$。其更新规则是：
$$V(S_t) \leftarrow V(S_t) + \alpha \left( R_{t+1} + \gamma V(S_{t+1}) - V(S_t) \right)$$
其中 $\alpha$ 是**学习率 (step size)**，$R_{t+1} + \gamma V(S_{t+1})$ 是**TD 目标**，$R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ 被称为**TD 误差 ($\delta_t$)**。TD 学习在每一步之后都进行更新，而不是像蒙特卡洛 (Monte Carlo, MC) 方法那样需要等待一个完整的回合结束。

TD 算法的收敛性可以通过**[随机近似](@entry_id:270652) (stochastic approximation)** 理论来分析。考虑一个最简单的情形：一个单状态的 MDP，其奖励的[条件期望](@entry_id:159140)为 $\mu$ 。TD(0) 的更新可以写成一个[随机近似](@entry_id:270652)的标准形式：
$$V_{t+1} = V_t + \alpha_t \left( (\mu - (1 - \gamma) V_t) + (r_t - \mu) \right)$$
其中 $r_t - \mu$ 是一个均值为零的噪声项。ODE 方法指出，在满足 Robbins-Monro 条件的步长（$\sum \alpha_t = \infty, \sum \alpha_t^2  \infty$）下，这个离散的[随机过程](@entry_id:268487)的渐进行为会追踪一个常微分方程 (ODE) 的轨迹：
$$\frac{dv(\tau)}{d\tau} = \mu - (1 - \gamma) v(\tau)$$
这个 ODE 有一个唯一的全局稳定不动点，即 $v^* = \frac{\mu}{1 - \gamma}$。这正是该 MDP 的真实价值。这个分析为我们提供了坚实的理论基础，解释了为什么 TD 学习能够收敛到正确的[价值函数](@entry_id:144750)。

### 从评估到控制：[同策略与异策略](@entry_id:635848)学习

将 TD 学习的思想从[策略评估](@entry_id:136637)扩展到策略控制，我们得到了两种主要的算法：SARSA 和 Q-learning。

**SARSA** 是一种**同策略 (on-policy)** 算法，它学习的是智能体当前正在执行的策略（即行为策略）的动作价值函数 $Q^\pi$。它的名字来源于其更新所依赖的五元组 $(S_t, A_t, R_{t+1}, S_{t+1}, A_{t+1})$。更新规则为：
$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left( R_{t+1} + \gamma Q(S_{t+1}, A_{t+1}) - Q(S_t, A_t) \right)$$
这里的 $A_{t+1}$ 是行为策略在状态 $S_{t+1}$ 实际选择的动作。

**Q-learning** 是一种**异策略 (off-policy)** 算法，它直接学习最优动作价值函数 $Q^*$，而不管智能体实际遵循的行为策略是什么。其更新规则为：
$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left( R_{t+1} + \gamma \max_{a'} Q(S_{t+1}, a') - Q(S_t, A_t) \right)$$
Q-learning 的 TD 目标中包含了一个 `max` 算子，这使得它总是在估计最优策略（贪心策略）的价值，即使行为策略为了探索而采取了非贪心动作。

这两种算法的收敛性质有所不同 。
- 在表格型（tabular）表示下，只要所有状态-动作对被无限次访问，并且步长满足 Robbins-Monro 条件，Q-learning 就能保证收敛到最优动作价值函数 $Q^*$。
- 对于 SARSA，为了收敛到 $Q^*$，其行为策略必须满足**无限探索下的贪心 (Greedy in the Limit with Infinite Exploration, GLIE)** 的条件。例如，一个 $\epsilon$-greedy 策略，其中探索率 $\epsilon_t$ 随着时间趋于 0。
- 如果 SARSA 使用一个固定的探索率 $\epsilon  0$，它将不会收敛到最优[价值函数](@entry_id:144750) $Q^*$，而是会收敛到这个 $\epsilon$-greedy 探索性策略本身的价值函数 $Q^{\pi_\epsilon}$。智能体将准确地学会其“边探索边利用”的行为到底有多好，但这通常不是最优的。

### 使用[函数近似](@entry_id:141329)进行扩展

对于具有巨大或[连续状态空间](@entry_id:276130)的问题，使用表格来存储每个状态（或状态-动作对）的价值是不可行的。我们需要使用**[函数近似](@entry_id:141329) (function approximation)** 来将[价值函数](@entry_id:144750)泛化到未见过的状态。一种常见的方法是**线性[函数近似](@entry_id:141329)**，其中价值被表示为一组特征 $\phi(s)$ 的线性组合：
$$\hat{v}(s, w) = \phi(s)^\top w$$
其中 $w$ 是需要学习的权重向量。

在这种情况下，学习的目标是什么？由于近似价值函数 $\hat{v}(w)$ 被限制在由特征构成的子空间中，它可能无法精确表示真实的[价值函数](@entry_id:144750) $v^\pi$。一个合理的目标是找到一个在某种意义下最接近的解。TD(0) 算法的解对应于**贝尔曼投影方程 (Projected Bellman Equation)** 的不动点 ：
$$\hat{v}_w = \Pi (r + \gamma P \hat{v}_w)$$
其中 $\Pi$ 是一个将任意价值函数投影到特征所张成的子空间的[投影算子](@entry_id:154142)。如果这个投影是根据[马尔可夫链](@entry_id:150828)的[平稳分布](@entry_id:194199) $d$ 加权的，那么该不动点的权重 $w^*$ 满足一个[线性方程组](@entry_id:148943)：
$$(\Phi^\top D \Phi - \gamma \Phi^\top D P \Phi) w^* = \Phi^\top D r$$
其中 $\Phi$ 是特征矩阵，$D$ 是包含[平稳分布](@entry_id:194199) $d$ 的[对角矩阵](@entry_id:637782)。这表明，在线性近似下，TD 学习找到的不是对真实[价值函数](@entry_id:144750)的最佳拟合，而是对贝尔曼算子的不动点的一个投影近似。

与 TD 不同，使用线性[函数近似](@entry_id:141329)的蒙特卡洛 (MC) 方法的目标是最小化均方值误差 $\mathbb{E}_{S \sim d}[(v^\pi(S) - \hat{v}(S, w))^2]$。这导致 MC 的解是真实[价值函数](@entry_id:144750) $v^\pi$ 在特征空间上的一个直接投影。TD 和 MC 的这种目标差异是理解[函数近似](@entry_id:141329)下各种算法行为的关键。例如，在一个具体的双状态马尔可夫奖励过程 (MRP) 中，可以精确推导出 TD 和 MC 解之间的差异 ，这个差异依赖于[折扣](@entry_id:139170)因子 $\gamma$、奖励 $r_1, r_2$ 以及特征的定义 $\alpha$。这个差异表明 TD 的自举引入了一种固有的偏差。

当[函数近似](@entry_id:141329)与[异策略学习](@entry_id:634676)和自举结合时，可能会出现不稳定的情况，这被称为**“致命三元组 (deadly triad)”**。例如，带有线性[函数近似](@entry_id:141329)的 Q-learning 算法可能会发散，其权重会增长到无穷大，即使在非常简单的环境中也是如此 。这促使研究人员开发更稳定的异策略算法。

### 另一种途径：[策略梯度方法](@entry_id:634727)

到目前为止，我们讨论的主要是**价值基方法 (value-based methods)**，它们通过学习价值函数来间接得到策略。另一大类方法是**策略基方法 (policy-based methods)**，它们直接对策略进行[参数化](@entry_id:265163) $\pi_\theta(a|s)$，并试[图优化](@entry_id:261938)一个性能目标 $J(\theta)$（例如，起始状态的价值）。

这类方法的核心是计算性能目标相对于策略参数的梯度 $\nabla_\theta J(\theta)$，然后使用梯度上升来更新参数：$\theta \leftarrow \theta + \alpha \nabla_\theta J(\theta)$。**[策略梯度定理](@entry_id:635009) (Policy Gradient Theorem)** 提供了一个优美的表达式来计算这个梯度：
$$\nabla_\theta J(\theta) \propto \sum_s d^\pi(s) \sum_a \nabla_\theta \pi_\theta(a|s) Q^\pi(s,a)$$
其中 $d^\pi(s)$ 是在策略 $\pi$ 下状态 $s$ 的[平稳分布](@entry_id:194199)。这个定理的美妙之处在于，梯度的表达式不依赖于状态分布对策略参数的导数，这使得梯度的估计变得可行。使用恒等式 $\nabla_\theta \pi_\theta = \pi_\theta \nabla_\theta \ln \pi_\theta$，我们可以得到一个适合采样的形式：
$$\nabla_\theta J(\theta) = \mathbb{E}_{\pi_\theta} \left[ \nabla_\theta \ln \pi_\theta(A_t|S_t) Q^{\pi_\theta}(S_t, A_t) \right]$$

**[行动者-评论家](@entry_id:634214) (Actor-Critic)** 方法是实现[策略梯度](@entry_id:635542)的一种流行框架。
- **行动者 (Actor)** 负责[参数化](@entry_id:265163)的策略 $\pi_\theta$，并根据梯度更新。
- **评论家 (Critic)** 负责学习一个[价值函数](@entry_id:144750)（例如 $Q^\pi$ 或 $V^\pi$），用于评估行动者所采取的动作。

为了降低[梯度估计](@entry_id:164549)的方差，我们可以从 $Q^{\pi_\theta}(s,a)$ 中减去一个不依赖于动作 $a$ 的基线 (baseline)，例如状态价值 $V^{\pi_\theta}(s)$。这不会改变梯度的[期望值](@entry_id:150961)，因为 $\sum_a \nabla_\theta \pi_\theta(a|s) V^{\pi_\theta}(s) = V^{\pi_\theta}(s) \nabla_\theta \sum_a \pi_\theta(a|s) = 0$。得到的 $A^\pi(s,a) = Q^\pi(s,a) - V^\pi(s)$ 被称为**[优势函数](@entry_id:635295) (advantage function)**。

在实践中，[优势函数](@entry_id:635295)可以通过 TD 误差 $\delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t)$ 来近似，因为 $\mathbb{E}[\delta_t | S_t, A_t] = A^\pi(S_t, A_t)$。因此，一个常见的 Actor-Critic 更新的期望方向为：
$$g(\theta) = \mathbb{E}_{\pi_{\theta}}\!\left[\sum_{t=0}^{\infty} \gamma^{t} \, \nabla_{\theta} \ln \pi_{\theta}(A_{t} \mid S_{t}) \, \delta_{t} \right]$$
可以严格证明，当评论家是完美的时候（即它给出了真实的 $V^{\pi_\theta}$），这个期望更新方向精确等于真实的[策略梯度](@entry_id:635542) $\nabla_\theta J(\theta)$ 。通过在一个具体的双状态 MDP 上从[贝尔曼方程](@entry_id:1121499)出发直接对价值函数求导，我们可以验证这一结论，并计算出在 $\theta=0$ 处的精确[策略梯度](@entry_id:635542)值为 $-\frac{26}{5}$ 。

### 扩展至[多智能体系统](@entry_id:170312)

当我们将单个智能体的学习框架扩展到**[多智能体系统](@entry_id:170312) (Multi-Agent Systems, MAS)** 时，问题变得更加复杂。从任何一个智能体的角度来看，其他智能体的学习和适应行为使得环境变得非平稳，这违反了标准 MDP 的假设。

然而，在某些特殊类型的博弈中，我们可以做出有力的分析。一个例子是**[势博弈](@entry_id:636960) (potential games)**，特别是**相同利益博弈 (identical-interest games)**，其中所有智能体的回报都与一个全局的**势函数 (potential function)** $\Phi$ 的变化完全一致。

在这种情况下，如果智能体使用带有**[熵正则化](@entry_id:749012) (entropy regularization)** 的学习算法，整个系统的动态会趋向于一个可预测的均衡 。智能体的目标函数被修改为最大化期望回报与策略熵的加权和：
$$\mathcal{J}(\pi)=\sum_{x}\pi(x)\,\Phi(x) - \tau\sum_{x}\pi(x)\ln \pi(x)$$
其中 $x$ 是联合动作，$\pi(x)$ 是联合动作的概率分布，$\tau$ 是控制探索程度的“温度”参数。

通过使用[拉格朗日乘子法](@entry_id:176596)对这个目标函数进行优化，我们可以推导出最大化该目标的平稳[联合分布](@entry_id:263960) $\pi^*$ 具有**吉布斯-[玻尔兹曼分布](@entry_id:142765) (Gibbs-Boltzmann distribution)** 的形式：
$$ \pi^{\star}(x) = \frac{\exp\left(\Phi(x)/\tau\right)}{\sum_{y} \exp\left(\Phi(y)/\tau\right)} $$
这个分布在统计力学中非常基础，它表明具有更高势（或更低“能量”）的联合动作被选择的概率呈指数级增长。例如，在一个具有势函数 $\Phi(a,a)=\ln 5, \Phi(a,b)=\ln 3, \Phi(b,a)=\ln 2, \Phi(b,b)=0$ 且 $\tau=1$ 的双智能体博弈中，系统达到均衡时选择最优联合动作 $(a,a)$ 的概率为 $\frac{5}{5+3+2+1} = \frac{5}{11}$ 。这一结果优雅地将多[智能体学习](@entry_id:1120882)、博弈论和统计物理联系起来，为理解[复杂适应系统](@entry_id:893720)中的集体行为提供了有力的分析工具。