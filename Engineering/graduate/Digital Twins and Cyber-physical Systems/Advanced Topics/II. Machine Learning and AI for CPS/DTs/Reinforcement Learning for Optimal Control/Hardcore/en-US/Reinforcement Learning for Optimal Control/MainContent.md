## Introduction
Reinforcement Learning (RL) has emerged as a powerful computational framework for solving complex [optimal control](@entry_id:138479) problems, offering a data-driven approach to decision-making under uncertainty. Its significance lies in its ability to handle nonlinear dynamics and learn optimal strategies directly from interaction, a critical capability for the design of autonomous Cyber-Physical Systems (CPS). This article bridges the gap between classical control theory and modern machine learning, demonstrating how RL provides a generalized framework for optimization. In the following chapters, you will first delve into the core theoretical foundations in "Principles and Mechanisms," exploring Markov Decision Processes and the celebrated Bellman equations. Next, "Applications and Interdisciplinary Connections" will illustrate the versatility of these methods across engineering, finance, and medicine, showing how RL extends classical techniques. Finally, "Hands-On Practices" will offer concrete exercises to solidify your understanding. We begin by establishing the fundamental principles that allow us to formally frame optimal control as a problem of reinforcement learning.

## Principles and Mechanisms

The formulation of optimal control as a [reinforcement learning](@entry_id:141144) (RL) problem rests upon a set of core principles and mechanisms that provide the mathematical language for decision-making under uncertainty and the algorithmic tools to find optimal solutions. This chapter delineates these foundational concepts, beginning with the Markov Decision Process (MDP) as the formal model for controlled [stochastic systems](@entry_id:187663). We will then explore the [principle of optimality](@entry_id:147533) through the celebrated Bellman equations, which underpin nearly all solution methods. Subsequently, we will introduce the primary families of RL algorithms—including model-free and model-based approaches, value-based and policy-based methods—and conclude with advanced mechanisms crucial for the deployment of RL in real-world Cyber-Physical Systems (CPS), such as handling partial observability and enforcing safety constraints.

### Modeling Sequential Decision Problems in Cyber-Physical Systems

At the heart of reinforcement learning for optimal control lies a formal mathematical structure that captures the interaction between a decision-making agent and its environment. This structure is the Markov Decision Process.

#### The Markov Decision Process Framework

A Cyber-Physical System operating in discrete time can often be described by a [state evolution](@entry_id:755365) equation of the form $x_{t+1} = f(x_t, a_t) + w_t$, where $x_t$ is the system's state at time $t$, $a_t$ is the control action applied, $f$ is a function describing the nominal system dynamics, and $w_t$ represents stochastic disturbances or [process noise](@entry_id:270644). To formalize the sequential decision problem faced by an RL agent, we model this interaction as a **Markov Decision Process (MDP)**. An MDP is formally defined by the tuple $(\mathcal{S}, \mathcal{A}, P, r, \gamma)$.

*   **State Space ($\mathcal{S}$):** The set of all possible states the system can be in. For the CPS described, if the state $x_t$ is fully measurable and the disturbance $w_t$ is independent of past states and actions, then the physical state is a [sufficient statistic](@entry_id:173645) for the future. This means that the history of the system provides no more information about the future than the current state does. This is the **Markov property**. Consequently, the MDP state $s_t$ can be taken to be the physical state $x_t$.

*   **Action Space ($\mathcal{A}$):** The set of all admissible control actions the agent can take.

*   **Transition Model ($P$):** The [transition probability](@entry_id:271680) kernel, $P(s' \mid s, a) = \mathbb{P}(s_{t+1}=s' \mid s_t=s, a_t=a)$, specifies the probability distribution of the next state $s'$ given the current state $s$ and action $a$. In our CPS example, for a given state-action pair $(x, a)$, the next state is $f(x, a) + w$, where $w$ is a random variable. The transition kernel $P$ is therefore determined by the distribution of the disturbance $w_t$. Specifically, the probability of landing in a set of states $B \subseteq \mathcal{S}$ is $P(B \mid x,a) = \mathbb{P}(f(x,a)+w \in B)$.

*   **Reward Function ($r$):** A function $r: \mathcal{S} \times \mathcal{A} \to \mathbb{R}$ (or sometimes $r: \mathcal{S} \times \mathcal{A} \times \mathcal{S} \to \mathbb{R}$) that provides a scalar feedback signal at each step. The agent's objective is to maximize the cumulative sum of these rewards. In [optimal control](@entry_id:138479), problems are often framed as minimizing a cost function. The reward is simply the negative of the one-step cost; for instance, for a quadratic cost $x_t^\top Q x_t + a_t^\top R a_t$, the reward would be $r(x_t, a_t) = -(x_t^\top Q x_t + a_t^\top R a_t)$.

*   **Discount Factor ($\gamma$):** A scalar $\gamma \in [0, 1)$ that balances the importance of immediate versus future rewards. The agent seeks to maximize the **return**, which is the discounted sum of future rewards, $G_t = \sum_{k=0}^{\infty} \gamma^k r_{t+k+1}$.

The primary distinction between this stochastic MDP formulation and classical deterministic [optimal control](@entry_id:138479) arises from the transition model. In a deterministic system with known dynamics $f$ and no disturbance ($w_t=0$), the transition model collapses to a Dirac delta function: given $s$ and $a$, the next state $s' = f(s,a)$ is known with certainty. The [dynamic programming](@entry_id:141107) equations, as we will see, then involve deterministic lookaheads rather than expectations over a probability distribution.

#### Policies and Induced System Dynamics

An agent's strategy for selecting actions is called a **policy**. A policy, denoted $\pi$, is a mapping from states to actions. We distinguish between two types of policies:

1.  **Deterministic Policy:** A deterministic policy is a function $\mu: \mathcal{S} \to \mathcal{A}$ that specifies a single action for each state. It can be viewed as a degenerate [conditional probability distribution](@entry_id:163069) $\pi(a \mid s) = \delta(a - \mu(s))$, where $\delta$ is the Dirac [delta function](@entry_id:273429).

2.  **Stochastic Policy:** A stochastic policy $\pi(a \mid s)$ specifies a probability distribution over the action space $\mathcal{A}$ for each state $s \in \mathcal{S}$. The agent samples an action from this distribution, $a_t \sim \pi(\cdot \mid s_t)$.

When a policy is applied to an MDP, it "closes the loop," creating a new stochastic process exclusively over the state space. If the policy $\pi$ and the underlying MDP dynamics $P$ are **stationary** (time-invariant), the resulting state process $\{s_t\}_{t \ge 0}$ is a time-homogeneous **Markov chain**. Its transition kernel, $P^\pi(s' \mid s)$, is found by averaging the original transition kernel over the actions prescribed by the policy:
$$
P^\pi(s' \mid s) = \int_{\mathcal{A}} P(s' \mid s, a) \pi(\mathrm{d}a \mid s)
$$
For a [discrete action space](@entry_id:142399), this becomes a sum: $P^\pi(s' \mid s) = \sum_{a \in \mathcal{A}} \pi(a \mid s) P(s' \mid s, a)$. If the policy is deterministic, $\pi(a|s) = \delta(a-\mu(s))$, this simplifies further to $P^\mu(s' \mid s) = P(s' \mid s, \mu(s))$. If the policy itself is time-varying, $\pi_t(a \mid s)$, the resulting state process is a time-inhomogeneous Markov chain with a time-dependent transition kernel $P^{\pi_t}(s' \mid s)$.

### The Principle of Optimality and Bellman Equations

The central aim of RL is to find a policy $\pi^*$ that maximizes the expected discounted return from every state. This concept of optimality is formalized by the [principle of optimality](@entry_id:147533), which states that an optimal policy has the property that whatever the initial state and initial decision are, the remaining decisions must constitute an optimal policy with regard to the state resulting from the first decision. This principle is mathematically expressed through the Bellman equations.

#### Value Functions and the Bellman Expectation Equation

To evaluate how "good" a state or a state-action pair is, we define **value functions**.

*   The **state-value function** $V^\pi(s)$ of a policy $\pi$ is the expected return starting from state $s$ and thereafter following policy $\pi$:
    $$V^\pi(s) \triangleq \mathbb{E}_\pi [G_t \mid s_t=s] = \mathbb{E}_\pi \left[ \sum_{k=0}^\infty \gamma^k r_{t+k+1} \mid s_t=s \right]$$

*   The **action-[value function](@entry_id:144750)** $Q^\pi(s,a)$ is the expected return starting from state $s$, taking action $a$, and thereafter following policy $\pi$:
    $$Q^\pi(s,a) \triangleq \mathbb{E}_\pi [G_t \mid s_t=s, a_t=a] = \mathbb{E}_\pi \left[ \sum_{k=0}^\infty \gamma^k r_{t+k+1} \mid s_t=s, a_t=a \right]$$

These two functions are related: $V^\pi(s) = \mathbb{E}_{a \sim \pi(\cdot|s)} [Q^\pi(s,a)]$.

The return can be written recursively: $G_t = r_{t+1} + \gamma G_{t+1}$. By taking the expectation of this identity, we derive the **Bellman expectation equation**, which provides a recursive relationship for the value function of a fixed policy $\pi$:
$$
V^\pi(s) = \mathbb{E}_\pi[r_{t+1} + \gamma V^\pi(s_{t+1}) \mid s_t=s]
$$
Expanding this expectation over the policy's actions and the environment's dynamics for a finite MDP gives:
$$
V^\pi(s) = \sum_{a \in \mathcal{A}} \pi(a \mid s) \sum_{s' \in \mathcal{S}} P(s' \mid s, a) \left[ r(s,a,s') + \gamma V^\pi(s') \right]
$$
This equation asserts that the value of a state $s$ under policy $\pi$ is the expected immediate reward plus the discounted expected value of the next state. It forms the basis for [policy evaluation](@entry_id:136637) algorithms.

#### The Bellman Optimality Equation

The ultimate goal is to find the **optimal value functions**, $V^*(s) = \sup_\pi V^\pi(s)$ and $Q^*(s,a) = \sup_\pi Q^\pi(s,a)$. These functions obey a special Bellman equation that is independent of any specific policy. The **Bellman optimality equation** expresses the value of a state under an optimal policy as the expected return from taking the *best* action and then proceeding optimally thereafter:
$$
V^*(s) = \max_{a \in \mathcal{A}} \mathbb{E}[r_{t+1} + \gamma V^*(s_{t+1}) \mid s_t=s, a_t=a] = \max_{a \in \mathcal{A}} Q^*(s,a)
$$
For a finite MDP, this expands to:
$$
V^*(s) = \max_{a \in \mathcal{A}} \sum_{s' \in \mathcal{S}} P(s' \mid s, a) \left[ r(s,a,s') + \gamma V^*(s') \right]
$$
The key difference between the expectation and optimality equations is the replacement of the policy-weighted average ($\sum_a \pi(a|s) \dots$) with a maximization operator ($\max_a \dots$). Solving this non-linear system of equations yields the optimal [value function](@entry_id:144750), from which an optimal policy can be extracted by choosing the action that achieves the maximum at each state (acting greedily with respect to $V^*$).

#### Existence and Uniqueness of the Value Function: A Contraction Mapping Approach

A crucial theoretical question is whether the Bellman expectation equation for $V^\pi$ always has a solution, and if so, whether it is unique. This can be answered elegantly using the Banach [fixed-point theorem](@entry_id:143811).

We can define a **Bellman [policy evaluation](@entry_id:136637) operator**, $T^\pi$, that maps a [value function](@entry_id:144750) $V$ to a new value function $(T^\pi V)$:
$$
(T^\pi V)(s) \triangleq \mathbb{E}_\pi [r_{t+1} + \gamma V(s_{t+1}) \mid s_t=s]
$$
The Bellman expectation equation is then simply the [fixed-point equation](@entry_id:203270) $V^\pi = T^\pi V^\pi$. One can show that for any two value functions $V_1$ and $V_2$, the following inequality holds:
$$
\| T^\pi V_1 - T^\pi V_2 \|_\infty \le \gamma \| V_1 - V_2 \|_\infty
$$
where $\| \cdot \|_\infty$ is the [supremum norm](@entry_id:145717), $\|V\|_\infty = \max_{s \in \mathcal{S}} |V(s)|$. This means that the operator $T^\pi$ is a **$\gamma$-contraction mapping**. The Banach [fixed-point theorem](@entry_id:143811) states that any contraction mapping on a complete [metric space](@entry_id:145912) (such as the space of bounded functions over $\mathcal{S}$) has a unique fixed point. Therefore, for any stationary policy $\pi$ and any discount factor $\gamma \in [0, 1)$, a unique [value function](@entry_id:144750) $V^\pi$ exists and is the unique solution to the Bellman expectation equation.

For a finite state space with $|\mathcal{S}|=n$, we can represent $V^\pi$ as a vector in $\mathbb{R}^n$. The Bellman equation becomes a linear system. Let $r^\pi$ be the vector of expected one-step rewards from each state under policy $\pi$, and let $P^\pi$ be the $n \times n$ [state transition matrix](@entry_id:267928) induced by $\pi$. The Bellman equation in vector form is:
$$
V^\pi = r^\pi + \gamma P^\pi V^\pi
$$
Rearranging gives the linear system $(I - \gamma P^\pi)V^\pi = r^\pi$. Since $P^\pi$ is a [stochastic matrix](@entry_id:269622), its spectral radius is $\rho(P^\pi) \le 1$. For $\gamma \lt 1$, the spectral radius of $\gamma P^\pi$ is strictly less than 1, which guarantees that the matrix $(I - \gamma P^\pi)$ is invertible. The [value function](@entry_id:144750) can thus be found analytically via [matrix inversion](@entry_id:636005), providing a direct solution in the model-based setting:
$$
V^\pi = (I - \gamma P^\pi)^{-1} r^\pi
$$

### Reinforcement Learning Algorithms

The Bellman equations provide a theoretical foundation. Reinforcement learning provides the algorithmic machinery to solve these equations and find optimal policies, especially when the model ($P$ and $r$) is unknown.

#### Model-Based versus Model-Free Reinforcement Learning

RL algorithms can be broadly categorized based on whether they use an explicit model of the environment.

*   **Model-Based RL:** These methods first learn an approximate model of the environment, $(\hat{P}, \hat{r})$, from experience. Then, they use this learned model to find a policy through planning. This planning can involve solving the Bellman equations directly (as in the [matrix inversion](@entry_id:636005) above), or using methods like [value iteration](@entry_id:146512), policy iteration, or tree search. Classical optimal control methods such as the Linear Quadratic Regulator (LQR) and Model Predictive Control (MPC) are inherently model-based, as they rely on an explicit system model (e.g., the matrices $A, B$ in $x_{t+1} = Ax_t + Bu_t$) to compute the control law. An adaptive MPC controller that learns its model online is a prime example of model-based RL.

*   **Model-Free RL:** These methods do not learn an explicit model of the transition dynamics or reward function. Instead, they learn a [value function](@entry_id:144750) or a policy directly from sampled experience tuples $(s_t, a_t, r_{t+1}, s_{t+1})$. Model-free methods are often more straightforward to implement but can be less sample-efficient than model-based approaches. They can be further subdivided into value-based methods (like Q-learning) and policy-based methods (like policy gradients).

It is noteworthy that even for problems with known analytical solutions like LQR, model-free methods can be applied. For instance, a model-free [policy gradient](@entry_id:635542) algorithm that searches over the space of linear feedback policies, $u_t = Kx_t$, can converge to the optimal LQR gain matrix $K^*$ under appropriate technical conditions, demonstrating the power and generality of the RL framework.

#### Model-Free Policy Evaluation: Monte Carlo and Temporal Difference Methods

In model-free RL, a central task is [policy evaluation](@entry_id:136637): estimating $V^\pi$ from trajectories generated by following $\pi$. Two canonical approaches are Monte Carlo (MC) and Temporal Difference (TD) learning.

**Monte Carlo (MC) evaluation** uses the empirical mean of returns to estimate the value function. After generating a trajectory starting from state $s_t$, we observe the full return $G_t = r_{t+1} + \gamma r_{t+2} + \dots$. This observed return is an unbiased sample of the true value $V^\pi(s_t)$. The estimate $\hat{V}(s_t)$ is updated to move it closer to this sample:
$$
\hat{V}(s_t) \leftarrow \hat{V}(s_t) + \alpha \left[ G_t - \hat{V}(s_t) \right]
$$
where $\alpha$ is a learning rate. While the MC target $G_t$ is unbiased, it suffers from high variance because it is a sum of many random variables (rewards over the rest of the episode).

**Temporal Difference (TD) learning**, specifically TD(0), updates the value estimate after only one time step. It uses the observed reward $r_{t+1}$ and the current estimate of the next state's value, $\hat{V}(s_{t+1})$, to form a TD target. This process of using an estimate to update another estimate is called **bootstrapping**. The update rule is:
$$
\hat{V}(s_t) \leftarrow \hat{V}(s_t) + \alpha \left[ r_{t+1} + \gamma \hat{V}(s_{t+1}) - \hat{V}(s_t) \right]
$$
The term $\delta_t = r_{t+1} + \gamma \hat{V}(s_{t+1}) - \hat{V}(s_t)$ is the **TD error**. The TD target, $r_{t+1} + \gamma \hat{V}(s_{t+1})$, is a biased estimate of $V^\pi(s_t)$ because it depends on the current (and likely incorrect) estimate $\hat{V}$. However, because it only depends on one step of random transitions, its variance is much lower than the MC target. This illustrates a fundamental **[bias-variance trade-off](@entry_id:141977)** in [reinforcement learning](@entry_id:141144). Despite the bias, TD(0) is guaranteed to converge to the true [value function](@entry_id:144750) in the tabular case with appropriate learning rates.

When using a Digital Twin (DT) as a simulator, if the DT perfectly matches the real plant, using it to generate transitions for TD learning introduces no additional bias. However, if the DT has model error, the algorithm will converge to the value function of the DT's dynamics, introducing a [model bias](@entry_id:184783) relative to the true system's value function.

#### Actor-Critic Methods: Combining Policy and Value Learning

Actor-critic methods are a sophisticated family of algorithms that explicitly maintain and learn both a policy and a value function.

*   The **Actor** is the policy, $\pi_\theta(a|s)$, parameterized by $\theta$. It controls how the agent behaves.
*   The **Critic** is the value function, $V_w(s)$ (or $Q_w(s,a)$), parameterized by $w$. It evaluates the policy's actions.

The actor is typically updated using a [policy gradient](@entry_id:635542) method. The [policy gradient theorem](@entry_id:635009) states that the gradient of the performance objective $J(\theta)$ is given by $\nabla_\theta J(\theta) = \mathbb{E}_{\pi_\theta} [\nabla_\theta \log \pi_\theta(a|s) Q^{\pi_\theta}(s,a)]$. A crucial technique for variance reduction in this estimate is to subtract a state-dependent baseline from the Q-value. The optimal baseline is the state-[value function](@entry_id:144750) $V^{\pi_\theta}(s)$. The resulting term, $A^{\pi_\theta}(s,a) = Q^{\pi_\theta}(s,a) - V^{\pi_\theta}(s)$, is known as the **[advantage function](@entry_id:635295)**. The [advantage function](@entry_id:635295) quantifies how much better taking action $a$ is compared to the average action from state $s$ under policy $\pi_\theta$. By definition, its expectation under the policy is zero: $\mathbb{E}_{a \sim \pi_\theta(\cdot|s)} [A^{\pi_\theta}(s,a)] = 0$. Using the [advantage function](@entry_id:635295) does not bias the [policy gradient](@entry_id:635542) but significantly reduces its variance, leading to more stable learning.

In a practical actor-critic algorithm, we use the critic's estimate $V_w(s)$ as the baseline. Furthermore, we approximate the Q-value using the TD target. This leads to the TD error $\delta_t = r_{t+1} + \gamma V_w(s_{t+1}) - V_w(s_t)$ serving as a single-sample estimate of the [advantage function](@entry_id:635295). The update rules are then:

1.  **Critic Update:** The critic's parameters $w$ are updated to minimize the TD error, typically via [gradient descent](@entry_id:145942) on $(\delta_t)^2$. For a linear critic $V_w(s) = w^T \phi(s)$, the update is $\Delta w_t = \alpha_w \delta_t \nabla_w V_w(s_t) = \alpha_w \delta_t \phi(s_t)$.

2.  **Actor Update:** The actor's parameters $\theta$ are updated via stochastic gradient ascent, using the TD error as the advantage estimate:
    $$
    \Delta \theta_t = \alpha_\theta \nabla_\theta \log \pi_\theta(a_t|s_t) \delta_t
    $$
    For example, if the policy is Gaussian with mean $\mu_\theta(s) = \theta s$ and fixed variance $\sigma^2$, the score function is $\nabla_\theta \log \pi_\theta(a|s) = \frac{s(a - \theta s)}{\sigma^2}$. The update pushes the probability of taking action $a_t$ up if $\delta_t$ is positive (the action was better than expected) and down if $\delta_t$ is negative.

### Advanced Mechanisms for Control in Cyber-Physical Systems

Deploying RL in real-world CPS often requires addressing complexities beyond the basic MDP framework. These include learning from pre-existing data, handling sensor limitations, and guaranteeing safety.

#### Off-Policy Evaluation with Importance Sampling

In many CPS applications, executing a new, exploratory policy on the physical plant can be risky or expensive. A common scenario involves evaluating a new **target policy** $\pi$ using data logged from a different, often safer, **behavior policy** $\mu$. This is the problem of **[off-policy evaluation](@entry_id:181976)**.

A key model-free technique for this is **importance sampling (IS)**. The core idea is to re-weight the returns observed under the behavior policy $\mu$ to correct for the distribution mismatch. The expected return under $\pi$ can be expressed as an expectation under $\mu$ using a [likelihood ratio](@entry_id:170863):
$$
J(\pi) = \mathbb{E}_{\tau \sim \pi}[R(\tau)] = \mathbb{E}_{\tau \sim \mu} \left[ \frac{P(\tau \mid \pi)}{P(\tau \mid \mu)} R(\tau) \right]
$$
Assuming the [system dynamics](@entry_id:136288) are the same, the trajectory probability ratio simplifies to a product of policy ratios:
$$
\frac{P(\tau \mid \pi)}{P(\tau \mid \mu)} = \prod_{t=0}^{T-1} \frac{\pi(a_t \mid s_t)}{\mu(a_t \mid s_t)} = \prod_{t=0}^{T-1} \rho_t
$$
where $\rho_t$ is the importance sampling ratio at time $t$. This correction allows us to estimate the performance of $\pi$ without a model of the environment, using only data from $\mu$. A critical requirement for this to be valid is the **coverage assumption**: $\mu(a|s) > 0$ whenever $\pi(a|s) > 0$.

The simplest estimator, ordinary [importance sampling](@entry_id:145704), weights the entire return of each trajectory by the product of ratios for that trajectory. This estimator is unbiased but can have extremely high variance, especially for long episodes, as the product of ratios can explode. A more stable, lower-variance (though biased in finite samples) alternative is **per-decision [importance sampling](@entry_id:145704) (PDIS)**, which applies weights to rewards at each step individually.

#### Control under Partial Observability: The POMDP Framework

In many real-world systems, the agent cannot directly measure the true underlying state $s_t$. Instead, it receives an **observation** $o_t$ which is a noisy or incomplete projection of the state. This setting is modeled as a **Partially Observable Markov Decision Process (POMDP)**. A POMDP extends the MDP tuple with an observation space $\Omega$ and an observation model $O(o' \mid s', a) = \mathbb{P}(o_{t+1}=o' \mid s_{t+1}=s', a_t=a)$.

Since the state is not known, the agent cannot condition its policy directly on $s_t$. Instead, it maintains a **belief state**, $b(s)$, which is a probability distribution over the latent states $S$. The belief $b(s)$ is a [sufficient statistic](@entry_id:173645) for the history of observations and actions. After taking action $a$ from belief $b$ and receiving observation $o'$, the agent updates its belief to a new posterior belief $b'(s')$ using a two-step Bayesian filter:

1.  **Prediction:** The agent first computes a predictive belief $\bar{b}(s')$ over the next state by propagating the current belief through the transition model:
    $$
    \bar{b}(s') = P(s' \mid a, b) = \sum_{s \in S} P(s' \mid s, a) b(s)
    $$

2.  **Correction:** The agent then uses the new observation $o'$ to correct this predictive belief via Bayes' rule:
    $$
    b'(s') = P(s' \mid o', a, b) = \frac{P(o' \mid s', a, b) \bar{b}(s')}{P(o' \mid a, b)} = \eta \cdot O(o' \mid s', a) \cdot \bar{b}(s')
    $$
    where $\eta$ is a [normalization constant](@entry_id:190182). This update rule allows the agent to track its uncertainty over the true state, for example, inferring the likelihood of a system being in a "degraded" or "faulty" mode based on an "alarm" observation. Planning in POMDPs is then performed in the continuous space of beliefs, which is significantly more challenging than planning in the original state space.

#### Safe Reinforcement Learning via Constrained MDPs

For safety-critical CPS, such as an autonomous mobile manipulator in a factory, it is often not enough to simply maximize a [reward function](@entry_id:138436). We must also explicitly enforce safety constraints. The **Constrained Markov Decision Process (CMDP)** framework provides a principled way to do this.

A CMDP augments the standard MDP with one or more cost functions, $c_i: \mathcal{S} \times \mathcal{A} \to \mathbb{R}_{\ge 0}$, and corresponding budget constraints, $d_i$. The optimization problem becomes:
$$
\max_{\pi} J(\pi) \quad \text{subject to} \quad C_i(\pi) \le d_i \quad \text{for all } i
$$
where $J(\pi)$ is the expected discounted reward and $C_i(\pi) = \mathbb{E}_\pi [\sum_{t=0}^\infty \gamma^t c_i(s_t, a_t)]$ is the expected discounted safety cost. The cost function $c_i$ can be designed to encode risk, such as proximity to obstacles, thermal limit violations, or excessive energy consumption. The constraint $C_i(\pi) \le d_i$ then enforces a budget on the total [expected risk](@entry_id:634700) the agent is allowed to incur.

A powerful method for solving CMDPs is the primal-dual approach using Lagrange multipliers. We form the Lagrangian $L(\pi, \lambda) = J(\pi) - \sum_i \lambda_i (C_i(\pi) - d_i)$, where $\lambda_i \ge 0$ are [dual variables](@entry_id:151022). The learning process then involves alternating between:
1.  A **primal update** (policy update) to improve the policy $\pi$ with respect to the Lagrangian, which is equivalent to solving an unconstrained RL problem with a modified reward $r(s,a) - \sum_i \lambda_i c_i(s,a)$.
2.  A **dual update** to adjust the multipliers $\lambda_i$ via projected gradient ascent: $\lambda_{i, k+1} = [\lambda_{i, k} + \alpha_k (C_i(\pi_{\theta_k}) - d_i)]_+$.

This dual update automatically increases the penalty $\lambda_i$ if the $i$-th constraint is violated and decreases it when satisfied, actively steering the policy towards the feasible region. A Digital Twin is an invaluable tool in this context, providing a safe environment to generate the trajectories needed to estimate the policy's performance $J(\pi)$ and safety costs $C_i(\pi)$ and their gradients, enabling principled and safe policy synthesis before deployment.