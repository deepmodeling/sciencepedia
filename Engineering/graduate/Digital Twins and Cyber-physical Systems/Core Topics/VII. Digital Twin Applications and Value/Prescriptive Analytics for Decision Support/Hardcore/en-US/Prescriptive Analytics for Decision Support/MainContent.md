## Introduction
In the era of Digital Twins (DTs) and Cyber-Physical Systems (CPS), the ability to generate vast amounts of data and create high-fidelity predictive models is well-established. However, prediction alone is not enough. The ultimate goal is to leverage this insight to make better, faster, and more reliable decisions. This brings us to the domain of [prescriptive analytics](@entry_id:1130131), the crucial final step that translates "what will happen" into "what should we do." It serves as the intelligent core that empowers autonomous systems to act optimally in complex, dynamic, and uncertain environments. This article bridges the gap between [predictive modeling](@entry_id:166398) and actionable intelligence, providing a comprehensive guide to the theories and practices of [prescriptive analytics](@entry_id:1130131) for decision support.

The journey begins in the **Principles and Mechanisms** chapter, where we lay the mathematical groundwork. We will explore how to formulate decision problems using [statistical decision theory](@entry_id:174152), understand the power of convexity in optimization, and handle conflicting goals with multi-objective methods. We will also delve into frameworks for dynamic decision-making, including Model Predictive Control (MPC) and Markov Decision Processes (MDPs). Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates how these principles are applied in real-world domains like energy systems and manufacturing. It highlights the critical links between [prescriptive analytics](@entry_id:1130131) and adjacent fields such as state estimation, [safety verification](@entry_id:1131179), and cybersecurity. Finally, the **Hands-On Practices** chapter offers practical exercises that challenge you to apply these concepts to problems involving resource allocation, trade-off analysis, and robust scheduling. Through this structured exploration, you will gain the expertise to design and implement sophisticated decision support systems.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that underpin [prescriptive analytics](@entry_id:1130131) for decision support in the context of cyber-physical systems (CPS) and their digital twins (DTs). We move from the foundational formulation of a decision problem to advanced methods for handling dynamics, uncertainty, multiple objectives, and multi-agent interactions. The emphasis is on the mathematical structures that enable tractable and reliable decision-making.

### The Fundamental Formulation of Prescriptive Analytics

At its heart, [prescriptive analytics](@entry_id:1130131) seeks to answer the question: "What should we do?" This distinguishes it from its counterpart, [predictive analytics](@entry_id:902445), which addresses the question: "What will happen?" To formalize this, we draw upon the language of [statistical decision theory](@entry_id:174152). A decision problem is characterized by several key components:

1.  An **action space** $\mathcal{A}$, which is the set of all possible decisions $a$ that can be made.
2.  A space of **states of nature** $\Theta$, representing all possible realities or configurations of the uncertain environment, denoted by a state vector $\theta$.
3.  A **loss function** $L(a, \theta)$, a scalar function that quantifies the cost, risk, or undesirability of having chosen action $a$ if the true state of nature turns out to be $\theta$.
4.  An **uncertainty model**, typically a probability distribution $P$ over the states of nature $\theta$, which encapsulates our knowledge or beliefs about which state will be realized.

Within this framework, the roles of predictive and [prescriptive analytics](@entry_id:1130131) become clear. **Predictive analytics** is the task of learning the uncertainty model, $P(\theta)$, from data. For instance, a digital twin might ingest sensor data and historical logs from a CPS to construct a probabilistic model of future demands or component failures. This predictive model is an essential input, but it does not, by itself, recommend an action.

**Prescriptive analytics** takes the output of the predictive model and uses it to recommend an optimal action. Since the decision $a$ must often be chosen *before* the true state $\theta$ is realized, we cannot simply minimize $L(a, \theta)$ directly. Instead, the central principle is to choose an action that performs best on average, across all possibilities. This is achieved by minimizing the **expected loss**, also known as the Bayes risk. The prescriptive task is thus formulated as the following optimization problem:

$$ a^* = \arg\min_{a \in \mathcal{A}} \mathbb{E}_{\theta \sim P}[L(a, \theta)] = \arg\min_{a \in \mathcal{A}} \int L(a, \theta) \, dP(\theta) $$

Consider a CPS that coordinates a fleet of autonomous mobile robots, supported by a DT . The decision $a$ could be a task assignment and charging schedule for the fleet. The uncertain state $\theta$ might include parameters for task arrival intensities and battery degradation rates. The DT, acting as a predictive engine, analyzes historical data to produce a distribution $P$ over these parameters. The loss function $L(a, \theta)$ would capture the total operational cost, including energy consumption and penalties for delayed tasks, under a given schedule $a$ and environmental reality $\theta$. The [prescriptive analytics](@entry_id:1130131) module then solves for the schedule $a^*$ that minimizes the expected cost, where the expectation is taken over the distribution $P$ supplied by the DT. The DT's ability to simulate the system is crucial here, as it allows for the evaluation of $L(a, \theta)$ for various $\theta$, which is necessary to estimate the expectation, often via Monte Carlo methods.

### Decision Criteria Under Uncertainty

The principle of minimizing expected loss is powerful, but it hinges on having a trusted probability distribution $P(\theta)$. In many real-world scenarios, this distribution may be unknown, unreliable, or impossible to construct. In such cases of deep uncertainty, alternative decision criteria are needed. These criteria reflect different attitudes toward [risk and uncertainty](@entry_id:261484).

Let's consider a simplified decision problem with a finite set of actions $\{a_1, a_2, \dots\}$ and a [finite set](@entry_id:152247) of states $\{s_1, s_2, \dots\}$. The outcomes are captured in a **loss matrix** $L(a_i, s_j)$. Suppose a DT provides the following loss matrix for three control actions under two possible disturbance regimes :

| Action | Loss in State $s_1$ | Loss in State $s_2$ |
| :--- | :---: | :---: |
| $a_1$ | $2$ | $6$ |
| $a_2$ | $4$ | $5$ |
| $a_3$ | $5$ | $7$ |

Given this matrix but no probabilities for $s_1$ and $s_2$, which action is best? The answer depends on the chosen criterion.

*   **Minimax Criterion:** This profoundly conservative criterion guards against the worst possible outcome. For each action, we identify the maximum possible loss, and then we choose the action that minimizes this maximum loss. It is a "min-max" strategy: $\min_a \max_s L(a, s)$.
    For our example, the maximum losses are:
    -   $a_1: \max\{2, 6\} = 6$
    -   $a_2: \max\{4, 5\} = 5$
    -   $a_3: \max\{5, 7\} = 7$
    The minimum of these maximums is $5$, corresponding to action $a_2$. The minimax criterion thus prescribes $a_2$.

*   **Minimax-Regret Criterion:** This criterion seeks to minimize the maximum "opportunity cost" or "regret." Regret is the difference between the loss you incurred and the loss you *would* have incurred had you known the state in advance and chosen the best action for it. The regret is $R(a,s) = L(a,s) - \min_{a'} L(a',s)$.
    First, we compute the regret matrix. The best possible loss in $s_1$ is $2$ (from $a_1$), and in $s_2$ is $5$ (from $a_2$).
    The regret matrix $R(a_i, s_j)$ is:
    | Action | Regret in State $s_1$ | Regret in State $s_2$ | Max Regret |
    | :--- | :---: | :---: | :---: |
    | $a_1$ | $2-2=0$ | $6-5=1$ | $1$ |
    | $a_2$ | $4-2=2$ | $5-5=0$ | $2$ |
    | $a_3$ | $5-2=3$ | $7-5=2$ | $3$ |
    The minimax-regret criterion chooses the action that minimizes the maximum regret. The minimum value in the "Max Regret" column is $1$, corresponding to action $a_1$. This criterion prescribes $a_1$, demonstrating that different rationales can lead to different prescriptions.

The connection between the Bayes and minimax criteria is a deep result in [decision theory](@entry_id:265982). For any decision problem, there exists a **least favorable prior**—a probability distribution over states that maximizes the Bayes risk. A central theorem states that the Bayes risk under this prior is equal to the [minimax risk](@entry_id:751993). In our example, one can show that for the prior $p(s_1)=0, p(s_2)=1$, the Bayes action is $a_2$ and the expected loss is $5$, which equals the [minimax risk](@entry_id:751993). This establishes a prior for which the Bayesian and minimax philosophies coincide .

Finally, it is worth noting that if an action $a^*$ exists that is superior to all other actions in every single state of nature (a so-called **dominant action**), i.e., $L(a^*,s) \leq L(a,s)$ for all $a$ and $s$, then all reasonable decision criteria—Bayes (for any prior), minimax, and minimax-regret—will select $a^*$ .

### The Role of Convexity in Optimization

Most [prescriptive analytics](@entry_id:1130131) problems, regardless of the criterion used, are ultimately formulated as optimization problems: minimizing a cost function over a set of feasible decisions. The difficulty of solving such a problem is profoundly influenced by its mathematical structure. Among the most important and desirable structures is **[convexity](@entry_id:138568)**.

A set $\mathcal{X} \subseteq \mathbb{R}^n$ is **convex** if for any two points $x,y \in \mathcal{X}$, the entire line segment connecting them, $\{\lambda x + (1-\lambda) y \mid \lambda \in [0,1]\}$, is also contained within $\mathcal{X}$ . Geometrically, a [convex set](@entry_id:268368) has no "dents" or "holes."

A function $f : \mathbb{R}^n \to \mathbb{R}$ is **convex** if its domain is a [convex set](@entry_id:268368) and for any two points $x,y$ in its domain, the following inequality holds for all $\lambda \in [0,1]$:
$$ f(\lambda x + (1-\lambda) y) \le \lambda f(x) + (1-\lambda) f(y) $$
Geometrically, this means the line segment connecting any two points on the function's graph lies on or above the graph itself .

A **[convex optimization](@entry_id:137441) problem** is the task of minimizing a convex function over a convex feasible set. Such problems are of immense practical importance because they possess a remarkable property: **any local minimizer is also a global minimizer**. This means that if an algorithm finds a point from which no small step can further decrease the objective function, we can be confident that we have found the true best possible solution over the entire feasible set. This eliminates the pervasive problem in [non-convex optimization](@entry_id:634987) of getting stuck in suboptimal local minima.

Furthermore, if the objective function $f$ is **strictly convex** (meaning the inequality above is strict for $x \neq y$ and $\lambda \in (0,1)$), then the global minimizer, if it exists, is guaranteed to be **unique** .

For differentiable convex problems that satisfy certain regularity conditions (such as Slater's condition), the **Karush-Kuhn-Tucker (KKT) conditions** provide a set of equations and inequalities that are both necessary and sufficient for optimality. A point satisfying the KKT conditions is certified to be a global optimum, providing a rigorous foundation for algorithmic solutions . The tractability and reliability afforded by convexity make it a central goal in the formulation of prescriptive models.

### Handling Multiple Objectives: Pareto Optimality

In many engineering applications, a single loss function is insufficient. A decision often involves inherent trade-offs between multiple, conflicting objectives. For instance, in a manufacturing process, we might want to simultaneously minimize energy consumption ($E$), production delay ($D$), and component wear ($W$). Improving one objective often requires sacrificing performance in another. Prescriptive analytics must provide a way to reason about these trade-offs systematically.

This is the domain of **multi-objective optimization**. Instead of a scalar objective $f(x)$, we have a vector-valued objective function $f(x) = (f_1(x), f_2(x), \dots, f_k(x))$. Since there is no natural ordering for vectors, we cannot simply find a "minimum." Instead, we use the concept of Pareto efficiency.

*   **Pareto Domination:** A solution $x_A$ is said to **Pareto-dominate** another solution $x_B$ if $x_A$ is at least as good as $x_B$ in all objectives and strictly better in at least one objective. For a minimization problem, this means $f_i(x_A) \le f_i(x_B)$ for all $i=1,\dots,k$, and there exists at least one index $j$ such that $f_j(x_A)  f_j(x_B)$.

*   **Pareto Efficiency:** A solution $x^*$ is **Pareto-efficient** (or **Pareto-optimal**) if it is not dominated by any other [feasible solution](@entry_id:634783). A rational decision-maker should never choose a dominated solution, because there is an alternative that is strictly better in at least one way and no worse in any other.

The set of all Pareto-efficient solutions is called the **Pareto-optimal set**, and its image in the [objective space](@entry_id:1129023) is the **Pareto front**. This front represents the menu of all best possible trade-offs.

Consider five feasible control policies for a CPS, with their outcomes for Energy, Delay, and Wear ($E, D, W$) forecast by a DT :
*   $x_1: f(x_1) = (10, 5, 7)$
*   $x_2: f(x_2) = (8, 6, 9)$
*   $x_3: f(x_3) = (12, 4, 6)$
*   $x_4: f(x_4) = (9, 5, 8)$
*   $x_5: f(x_5) = (11, 7, 9)$

By performing [pairwise comparisons](@entry_id:173821), we can identify dominated solutions. For example, compare $x_1$ and $x_5$. We see that $10  11$ (better energy), $5  7$ (better delay), and $7  9$ (better wear). Therefore, policy $x_1$ dominates $x_5$, and $x_5$ is not a rational choice. After checking all pairs, we find that the set of non-dominated, Pareto-efficient policies is $\{x_1, x_2, x_3, x_4\}$. Within this set, no policy dominates another. For example, to get the low energy of $x_2$ ($E=8$), one must accept higher delay and wear compared to $x_1$. To get the excellent delay and wear of $x_3$ ($D=4, W=6$), one must accept a much higher energy cost ($E=12$).

The role of [prescriptive analytics](@entry_id:1130131) is to compute and present this Pareto front to the human decision-maker. The final choice of a single solution from the front then depends on the decision-maker's subjective preferences (e.g., "delay is twice as important as energy cost").

### Prescriptive Analytics in Dynamic Systems

Many CPS problems involve not a single decision, but a sequence of decisions over time. Prescriptive analytics provides powerful frameworks for these dynamic problems, which can be broadly categorized based on whether the system's evolution is modeled as deterministic or stochastic.

#### Deterministic Dynamics and Model Predictive Control

When a system's evolution can be predicted with reasonable accuracy, **Model Predictive Control (MPC)** is a preeminent prescriptive methodology. MPC operates on a **[receding horizon](@entry_id:181425)** principle: at each point in time, it solves an optimization problem to find an optimal sequence of control actions over a finite future horizon, but it only implements the *first* action in that sequence. At the next time step, it obtains a new system state measurement (or estimate), and repeats the entire process.

The optimization problem solved at each time $t$ is a prescriptive task that synthesizes information from a digital twin to make a decision. Its structure is typically as follows :

$$
\begin{aligned}
\min_{\{x_k, u_k\}_{k=t}^{t+N-1}, x_{t+N}} \quad  \sum_{k=t}^{t+N-1} \ell(x_k, u_k, \hat{\theta}_k) + V_f(x_{t+N}) \\
\text{s.t.} \quad  x_t = \hat{x}_t, \\
 x_{k+1} = f(x_k, u_k, \hat{\theta}_k), \quad k = t, \dots, t+N-1, \\
 x_k \in \mathcal{X}_{\mathrm{safe}}, \quad u_k \in \mathcal{U}, \quad k = t, \dots, t+N-1, \\
 x_{t+N} \in \mathcal{X}_f.
\end{aligned}
$$

Here:
*   The **objective function** minimizes the sum of **stage costs** $\ell(\cdot)$ over a horizon of length $N$, plus a **terminal cost** $V_f(\cdot)$ that approximates the cost-to-go beyond the horizon.
*   The optimization is constrained by the **initial state** $\hat{x}_t$, which is the best estimate of the current system state provided by the DT.
*   The **[system dynamics](@entry_id:136288)** $x_{k+1} = f(x_k, u_k, \hat{\theta}_k)$ describe how the state evolves, using the DT's predictive model and forecasts of exogenous inputs $\hat{\theta}_k$.
*   **State and input constraints**, $\mathcal{X}_{\mathrm{safe}}$ and $\mathcal{U}$, enforce safety and operational limits.
*   A **[terminal constraint](@entry_id:176488)** $x_{t+N} \in \mathcal{X}_f$ is often included to guarantee stability and [recursive feasibility](@entry_id:167169) of the controller.

If the dynamics are linear and the costs and constraints are convex, this is a convex optimization problem, which can be solved efficiently and reliably at each time step.

#### Stochastic Dynamics and Markov Decision Processes

When the system's evolution is subject to significant random uncertainty, the **Markov Decision Process (MDP)** provides the standard modeling framework. An MDP is formally defined by the tuple $(\mathcal{S}, \mathcal{A}, P, r, \gamma)$, where :

*   $\mathcal{S}$ is the set of possible states.
*   $\mathcal{A}$ is the set of possible actions.
*   $P(s' \mid s, a)$ is the **[transition probability](@entry_id:271680) function**, giving the probability of transitioning to state $s'$ after taking action $a$ in state $s$.
*   $r(s, a)$ is the **reward function**, giving the immediate reward (or negative cost) received after taking action $a$ in state $s$.
*   $\gamma \in [0, 1)$ is the **discount factor**, which prioritizes immediate rewards over future ones.

The goal in an MDP is to find a **policy** $\pi: \mathcal{S} \to \mathcal{A}$, a mapping from states to actions, that maximizes the expected discounted sum of future rewards. In **model-based reinforcement learning**, the digital twin serves as the "model," providing the [transition probabilities](@entry_id:158294) $P$ and rewards $r$. With this model, one can perform planning to find the [optimal policy](@entry_id:138495).

A classic planning algorithm is **Value Iteration**. It computes the optimal state-[value function](@entry_id:144750), $V^*(s)$, which represents the maximum expected future reward starting from state $s$. This is done by iteratively applying the **Bellman optimality operator**:
$$ V^{(k+1)}(s) = \max_{a \in \mathcal{A}} \left( r(s, a) + \gamma \sum_{s' \in \mathcal{S}} P(s' \mid s, a) V^{(k)}(s') \right) $$
Starting with an arbitrary initial [value function](@entry_id:144750) $V^{(0)}$, this process is repeated until $V^{(k)}$ converges to $V^*$. The [optimal policy](@entry_id:138495) is then the one that greedily chooses the action that achieves the maximum in the Bellman equation at each state. For example, in a machine maintenance problem where the state is "healthy" or "degraded" and actions are "produce" or "maintain," a DT can provide the model parameters, and [value iteration](@entry_id:146512) can compute whether it is optimal to perform preventative maintenance or continue production based on the machine's current health state and the long-term expected rewards .

### Advanced Topics in Prescriptive Analytics

Building upon these foundations, we can explore several advanced topics that address more complex challenges in real-world decision support.

#### Robustness to Model Error: Surrogate Models and Robust Optimization

The models used by a digital twin, whether physics-based simulators or learned functions, are never perfect. High-fidelity simulators may be too computationally expensive to use directly within an optimization loop. A common solution is to create a computationally cheap **surrogate model**, $\hat{f}(u)$, that approximates the true high-fidelity model, $f(u)$.

This introduces a new source of uncertainty: the [approximation error](@entry_id:138265) of the surrogate. If we can bound this error, for example, with a uniform guarantee of the form $|f(u) - \hat{f}(u)| \le \epsilon$ for all decisions $u$ in a feasible set $\mathcal{U}$, we can use **robust optimization** to make decisions that are resilient to this error .

Robust optimization replaces the original problem with its **[robust counterpart](@entry_id:637308)**, which seeks a solution that is optimal under the worst-case realization of the uncertainty. For an objective $J(x) = c(x) + h(f(u(x)))$, the [robust counterpart](@entry_id:637308) is:
$$ \min_{x \in X} \sup_{f : |f(u(x)) - \hat{f}(u(x))| \le \epsilon} \left( c(x) + h(f(u(x))) \right) $$
The inner [supremum](@entry_id:140512) finds the worst-case cost for a given decision $x$. If the [penalty function](@entry_id:638029) $h(\cdot)$ is non-decreasing (a common property), the worst case occurs when its argument is maximized. The true value $f(u(x))$ is at most $\hat{f}(u(x)) + \epsilon$. Therefore, the [robust counterpart](@entry_id:637308) simplifies to the following tractable problem:
$$ \min_{x \in X} \left( c(x) + h(\hat{f}(u(x)) + \epsilon) \right) $$
By solving this modified problem, we find a decision $x$ whose performance is guaranteed to be no worse than the calculated optimal value, providing a conservative but reliable prescription in the face of model error.

#### Handling Risk with Chance Constraints

In safety-critical systems, we often need to limit the probability of an undesirable event. Instead of optimizing for expected performance, we may need to enforce constraints on risk. **Chance-constrained programming** provides a framework for this.

A **chance constraint** takes the form:
$$ P(g(x, \xi) \le 0) \ge 1 - \alpha $$
where $g(x, \xi) \le 0$ represents a desired safe condition, $x$ is the decision, $\xi$ is a random variable, and $\alpha \in (0,1)$ is a small, user-specified risk level (e.g., $0.01$). The constraint requires that the decision $x$ be chosen such that the probability of staying in the safe region is at least $1-\alpha$ .

A major challenge with [chance constraints](@entry_id:166268) is that the feasible set they define, $\mathcal{X} = \{x \mid P(g(x, \xi) \le 0) \ge 1 - \alpha\}$, is often non-convex, making the optimization problem computationally intractable. However, there are important special cases where [convexity](@entry_id:138568) is preserved. A key result from stochastic programming states that if:
1.  The probability density of the random vector $\xi$ is **log-concave** (a broad class of distributions including Gaussian, exponential, and uniform), and
2.  The set $\{(x, \xi) \mid g(x, \xi) \le 0\}$ is convex in the joint space of decisions $x$ and uncertainties $\xi$,

then the feasible set $\mathcal{X}$ is convex . The second condition holds, for example, if $g(x, \xi)$ is a jointly [convex function](@entry_id:143191) in $(x, \xi)$. This theoretical result is critical, as it identifies classes of risk-aware prescriptive problems that can be solved efficiently.

#### Active Learning and Dual Control

In some problems, our actions affect not only the physical state of the system but also our knowledge about it. For example, applying a large control input might excite [system dynamics](@entry_id:136288) in a way that allows for more accurate estimation of an unknown model parameter. This leads to the fundamental **[exploration-exploitation trade-off](@entry_id:1124776)**. Should we take an action that is optimal according to our current beliefs (exploitation), or should we take an action that is more informative but potentially suboptimal in the short term, in the hope that it will improve our model and lead to better decisions later (exploration)?

**Dual control** refers to control strategies that explicitly balance these two objectives. The [value of information](@entry_id:185629) is incorporated directly into the prescriptive objective function. Consider a simple system $x_{t+1} = a x_t + b u_t + w_t$, where the input gain $b$ is unknown and believed to be Gaussian, $b \sim \mathcal{N}(\mu_t, \sigma_t^2)$ . A [dual control](@entry_id:1124025) objective for choosing the input $u_t$ could be:

$$ J(u_t) = \underbrace{\mathbb{E}[(x_{t+1} - r)^2]}_{\text{Exploitation}} + \underbrace{\rho u_t^2}_{\text{Control Effort}} + \underbrace{\lambda \, \text{Var}(b \mid \text{data up to } t+1)}_{\text{Exploration}} $$

The first term penalizes deviation from a reference $r$, encouraging exploitation of the current model. The third term, weighted by $\lambda > 0$, explicitly rewards actions that lead to a reduction in the posterior variance of the unknown parameter $b$. Since the posterior variance after an observation is a function of the control input $u_t$—specifically, it decreases more for larger values of $|u_t|$—this term provides a quantitative incentive for exploration. The optimal control input $u_t^*$ balances the myopic goal of tracking the reference with the strategic goal of learning the system model more accurately.

#### Multi-Agent Systems and Game Theory

Finally, many modern CPS are not monolithic entities but collections of interacting, autonomous agents, each with its own objectives. Examples include competing firms in a power market or different climate control zones within a building sharing a central HVAC unit. In such [multi-agent systems](@entry_id:170312), the optimal decision for one agent depends on the decisions of others.

**Game theory** provides the mathematical language for analyzing these interactions. In a **noncooperative game**, each agent seeks to minimize its own cost function, $J_i(x_i, x_{-i})$, where $x_i$ is the agent's own decision and $x_{-i}$ represents the decisions of all other agents. The stable solution concept in such games is the **Nash Equilibrium**. A profile of decisions $(x_1^*, x_2^*, \dots, x_N^*)$ is a Nash equilibrium if no single agent can improve its outcome by unilaterally changing its decision, assuming all other agents' decisions remain fixed .

For games with continuous action spaces and convex cost functions, a Nash equilibrium can often be computed by finding a fixed point of the agents' **best-response functions**. The [best response](@entry_id:272739) of agent $i$, $BR_i(x_{-i})$, is the solution to its individual optimization problem, holding the other agents' actions $x_{-i}$ fixed. A Nash equilibrium is a point $x^*$ where $x_i^* = BR_i(x_{-i}^*)$ for all agents $i$.

A more general and powerful framework for capturing such equilibria is that of **Variational Inequalities (VIs)**. For a game with $N$ agents, we can define a mapping $F(x) = (\nabla_{x_1} J_1, \dots, \nabla_{x_N} J_N)^T$. An equilibrium $x^*$ is a point in the feasible set $K$ that solves the VI:
$$ F(x^*)^T (y - x^*) \ge 0, \quad \text{for all } y \in K $$
This formulation unifies equilibrium problems with optimization and has a rich theory. For instance, if the mapping $F$ is strongly monotone—a condition related to how strongly the agents' costs are coupled—the Nash equilibrium is guaranteed to be unique .