## Introduction
Reinforcement learning (RL) provides a powerful computational framework for understanding how intelligent agents, including humans and other animals, learn to make adaptive decisions by interacting with their environment. Its principles of value, prediction, and error-driven learning offer a compelling explanation for a wide range of behaviors, from simple choices to complex planning. A central challenge in modern neuroscience, however, is to bridge the conceptual gap between these algorithmic theories and their biological implementation: how do the brain's circuits and synapses actually compute prediction errors and update strategies to maximize future rewards? This article tackles this question by providing a comprehensive theoretical and applied overview of reinforcement learning in the brain.

This exploration is structured to build a deep, layered understanding. The journey begins in the **Principles and Mechanisms** chapter, where we will formalize the core mathematical concepts of RL, such as Markov Decision Processes and [temporal difference learning](@entry_id:138242), and map them directly onto their neural substrates, including the dopaminergic system and the basal ganglia. Next, the **Applications and Interdisciplinary Connections** chapter expands this view, demonstrating how the RL framework illuminates complex cognitive functions like memory consolidation, planning, and cognitive control, and even provides mechanistic insights into neuropsychiatric disorders. Finally, the **Hands-On Practices** section offers a chance to engage directly with these concepts through a series of computational problems, solidifying theoretical knowledge through practical application.

## Principles and Mechanisms

This chapter delineates the core principles and mechanisms that form the foundation of reinforcement learning (RL) theory as it is applied to the brain. We will begin by formalizing the problem of decision-making in a structured environment and then proceed to explore the computational solutions and their neurobiological substrates, moving from circuit-level architectures down to synaptic-level plasticity.

### Formalizing Sequential Decision-Making: The Markov Decision Process

The fundamental abstraction for modeling an agent interacting with an environment to achieve a goal is the **Markov Decision Process (MDP)**. An MDP provides a mathematical language to describe the essential elements of this interaction. It is formally defined as a quintuple $(\mathcal{S}, \mathcal{A}, P, R, \gamma)$.

-   **State Space ($\mathcal{S}$):** A set of states that describe the configuration of the agent and its environment. A state $s \in \mathcal{S}$ is a complete description of the world at a particular moment.
-   **Action Space ($\mathcal{A}$):** A set of actions $a \in \mathcal{A}$ available to the agent.
-   **Transition Function ($P$):** A function $P(s' \mid s, a) = \Pr(S_{t+1}=s' \mid S_t=s, A_t=a)$ that specifies the probability of transitioning to state $s'$ from state $s$ after taking action $a$.
-   **Reward Function ($R$):** A function $R(s,a)$ that defines the expected immediate scalar reward, $r_t$, received after taking action $a$ in state $s$.
-   **Discount Factor ($\gamma$):** A scalar $\gamma \in [0, 1)$ that determines the present value of future rewards. A reward received $k$ steps in the future is discounted by a factor of $\gamma^k$.

The entire framework rests on a critical assumption: the **Markov Property**. This property asserts that the future is independent of the past given the present. In formal terms, the state $S_t$ is a [sufficient statistic](@entry_id:173645) for the history of all preceding states and actions, such that the distribution of the next state and reward depends only on the current state and action.

Applying this abstract framework to a real biological system presents a significant challenge: defining the state $s_t$. Consider a common neuroscience experiment where an animal performs a two-alternative forced choice (2AFC) task . We might record the population activity vector $x_t$ from various cortical areas. It is tempting to equate this raw neural activity with the state, but this is generally incorrect. The high-dimensional vector $x_t$ is an *observation*, which may be noisy or incomplete. To satisfy the Markov property, the [state representation](@entry_id:141201) $s_t$ must be a [sufficient statistic](@entry_id:173645) for predicting the future. This often requires constructing the state from the history of observations or by applying a fixed transformation $\phi$ to the current observation, $s_t = \phi(x_t)$, that extracts task-relevant information, such as a belief over the latent state of the task (e.g., "stimulus A is present"). The action $a_t$ corresponds to the discrete choice made by the animal, which is the result of computation in circuits like the Basal Ganglia, rather than the continuous [neural dynamics](@entry_id:1128578) that produce it. The transition and reward functions, $P$ and $R$, are assumed to be **time-homogeneous** or stationary within a stable experimental session, meaning the rules of the task do not change.

This standard MDP model, while powerful, makes strong assumptions of full state [observability](@entry_id:152062) and fixed-duration actions. Later in this chapter, we will explore more complex frameworks that relax these assumptions, such as **Partially Observable Markov Decision Processes (POMDPs)**, which handle noisy observations, and **Semi-Markov Decision Processes (SMDPs)**, which accommodate temporally extended actions .

### Evaluating Policies: Value Functions and Reward Prediction

The agent's behavior is described by a **policy**, $\pi(a \mid s)$, which is a mapping from states to a probability distribution over actions. The goal of the agent is to find a policy that maximizes the expected discounted sum of future rewards, known as the **return**, $G_t = \sum_{k=0}^{\infty} \gamma^k R_{t+k+1}$.

To achieve this, the agent must be able to evaluate how good a given policy is. This is accomplished through **value functions**. There are two primary types of value functions:

1.  The **state-value function**, $V^\pi(s)$, is the expected return when starting in state $s$ and subsequently following policy $\pi$:
    $$V^\pi(s) = \mathbb{E}_{\pi}[G_t \mid S_t = s]$$
    It represents the long-term value of being in a particular state under a given policy.

2.  The **action-value function**, $Q^\pi(s,a)$, is the expected return when starting in state $s$, taking action $a$, and thereafter following policy $\pi$:
    $$Q^\pi(s,a) = \mathbb{E}_{\pi}[G_t \mid S_t = s, A_t = a]$$
    It represents the long-term value of taking a specific action in a specific state.

These value functions are not merely abstract mathematical tools; they are hypothesized to be concrete computational quantities represented in the brain. In frameworks like **[predictive coding](@entry_id:150716)**, the brain is seen as a generative model that constantly makes predictions about the world. Within this view, value functions can be interpreted as top-down predictions of cumulative future rewards . The brain learns by comparing these predictions to actual outcomes and using the mismatch, or error, to update its internal models and improve future predictions.

### Learning from Errors: Temporal Difference Learning and Dopamine

How can an agent learn value functions directly from experience, without a full model of the environment's dynamics ($P$ and $R$)? The most influential class of algorithms for this task is **Temporal Difference (TD) learning**. TD learning updates value estimates based on the difference between successive predictions over time.

The core of TD learning is the **TD error**, denoted by $\delta_t$. For state-value learning, it is calculated after transitioning from state $S_t$ to $S_{t+1}$ and receiving reward $R_{t+1}$:
$$ \delta_t = R_{t+1} + \gamma V(S_{t+1}) - V(S_t) $$
The term $R_{t+1} + \gamma V(S_{t+1})$ is the **TD target**, which is a more accurate, one-step-updated estimate of the value of $S_t$. The TD error is the difference between this new target and the old estimate, $V(S_t)$. This error signal drives learning, updating the value estimate for the previous state:
$$ V(S_t) \leftarrow V(S_t) + \alpha \delta_t $$
where $\alpha$ is a learning rate.

A cornerstone of modern computational neuroscience is the **[reward prediction error](@entry_id:164919) (RPE) hypothesis**, which posits that the phasic activity of midbrain **dopamine neurons** in the Ventral Tegmental Area (VTA) and Substantia Nigra pars compacta (SNc) encodes a signal analogous to the TD error $\delta_t$. Experimental evidence robustly shows that these neurons exhibit a baseline tonic firing rate. An outcome that is better than expected ($\delta_t > 0$) elicits a phasic burst of firing, an outcome worse than expected ($\delta_t  0$) causes a pause in firing below baseline, and a perfectly predicted outcome ($\delta_t = 0$) results in no change.

This relationship can be formalized under the assumption of a linear encoding scheme . If $f_{\mathrm{base}}$ is the baseline firing rate and $\Delta f_t$ is the transient change in firing rate, then the phasic modulation is directly proportional to the TD error:
$$ \Delta f_t = k \cdot \delta_t $$
where $k > 0$ is a gain constant. The existence of a non-zero baseline is crucial, as it allows for [bidirectional signaling](@entry_id:177893)—increases for positive errors and decreases for negative errors—a key feature of the dopaminergic RPE signal.

### Learning to Act: Actor-Critic Architectures and the Basal Ganglia

Learning value functions (prediction) is a stepping stone to improving behavior (control). The **Actor-Critic architecture** provides a neurally plausible framework that separates the policy from the value function. It consists of two distinct components:

-   **The Critic:** This component learns and represents the state-[value function](@entry_id:144750), $V_w(s)$, where $w$ are the critic's parameters. It evaluates the current policy by calculating the TD error, $\delta_t = R_{t+1} + \gamma V_w(S_{t+1}) - V_w(S_t)$. Its parameters are updated using this error:
    $$ w \leftarrow w + \beta \cdot \delta_t \cdot \nabla_{w} V_{w}(S_t) $$

-   **The Actor:** This component represents the policy, $\pi_\theta(a \mid s)$, parameterized by $\theta$. It is responsible for selecting actions. The actor updates its policy based on the feedback from the critic. If the TD error $\delta_t$ is positive, the action taken was good and should be made more likely in the future. If $\delta_t$ is negative, the action was bad and should be made less likely. This is achieved via a [policy gradient](@entry_id:635542) update:
    $$ \theta \leftarrow \theta + \alpha \cdot \delta_t \cdot \nabla_{\theta} \log \pi_{\theta}(A_t \mid S_t) $$

This architecture maps elegantly onto the anatomy of the **cortico-basal ganglia-thalamic loops** . The **striatum**, the main input nucleus of the basal ganglia, is considered the locus of the **actor**. It receives massive convergent input from the cortex, representing the state $S_t$. The synaptic weights of these cortico-striatal connections are thought to encode the policy parameters $\theta$.

The dopaminergic projection from the VTA/SNc provides the globally broadcast TD [error signal](@entry_id:271594) $\delta_t$ that modulates plasticity at these cortico-striatal synapses. This modulation acts differently on two distinct populations of striatal Medium Spiny Neurons (MSNs):
-   **Direct Pathway ('Go'):** MSNs expressing D1 [dopamine receptors](@entry_id:173643) facilitate action execution. A positive RPE ($\delta_t > 0$, dopamine burst) potentiates active cortico-striatal synapses onto D1 neurons, strengthening the 'Go' signal for the chosen action.
-   **Indirect Pathway ('No-Go'):** MSNs expressing D2 [dopamine receptors](@entry_id:173643) inhibit action execution. A positive RPE weakens synapses onto active D2 neurons. Conversely, a negative RPE ($\delta_t  0$, dopamine dip) weakens D1 synapses and strengthens D2 synapses, making the chosen action less likely in the future.

This oppositional arrangement provides a powerful mechanism for the actor to refine its policy based on the critic's evaluations.

### Synaptic Mechanisms: Three-Factor Rules and Eligibility Traces

How does the dopaminergic signal, arriving after an action has been taken, modify the specific synapses responsible for that action? This is the **distal reward problem**, or the challenge of [temporal credit assignment](@entry_id:1132917). The solution is thought to lie in **three-factor synaptic plasticity rules**.

Unlike simpler two-factor Hebbian rules (e.g., Spike-Timing-Dependent Plasticity or STDP), which depend only on local presynaptic and postsynaptic activity, a three-factor rule incorporates a third, neuromodulatory signal. The weight change $\Delta w_{ij}$ at a synapse from neuron $i$ to neuron $j$ depends on:
1.  Presynaptic activity.
2.  Postsynaptic activity.
3.  A third modulatory signal, such as dopamine, carrying the RPE.

The mechanism works as follows: the conjunction of presynaptic and postsynaptic activity creates a short-lived **[eligibility trace](@entry_id:1124370)**, $e_{ij}(t)$, at the synapse. This trace acts as a "[synaptic tag](@entry_id:897900)," marking the synapse as having been recently active and thus potentially causally involved in the current behavior. The actual weight change only occurs when the third factor—the global RPE signal $m(t)$—arrives. The update is a multiplicative interaction:
$$ \Delta w_{ij}(t) = \eta \cdot m(t) \cdot e_{ij}(t) $$
where $\eta$ is a learning rate. This elegant mechanism bridges the temporal gap between an action and its delayed consequence, as the [eligibility trace](@entry_id:1124370) keeps a memory of recent synaptic activity until the outcome is known .

This concept can be formalized through the **TD($\lambda$) algorithm**, which uses eligibility traces to efficiently assign credit over multiple time steps . For a parametric [value function](@entry_id:144750) $V_\theta(S_t)$, the parameter update is $\Delta \theta_t = \alpha \delta_t e_t$. The eligibility trace vector $e_t$ is updated at each step according to:
$$ e_t = \gamma\lambda e_{t-1} + \nabla_\theta V_\theta(S_t) $$
Here, $\nabla_\theta V_\theta(S_t)$ is the gradient of the [value function](@entry_id:144750) with respect to the parameters, representing the sensitivity of the value estimate to each parameter (synaptic weight). This term corresponds to the formation of the [synaptic tag](@entry_id:897900). The parameter $\lambda \in [0,1]$ controls the decay rate of the trace, in conjunction with the discount factor $\gamma$. This recursive update creates a decaying memory of which synapses were recently influential, allowing a single TD error signal at time $t$ to update the parameters responsible for states visited many steps in the past.

### Advanced Concepts and Model Extensions

The basic RL framework can be extended to capture more complex and realistic aspects of cognition and behavior.

#### The Exploration-Exploitation Trade-off

An agent must balance **exploitation** (choosing actions known to yield high rewards) with **exploration** (trying new actions to discover potentially better ones). An overly greedy agent may get stuck in a suboptimal routine, while an overly explorative agent may fail to capitalize on its knowledge. This trade-off can be formalized by augmenting the standard reward-maximization objective with a term that encourages policy entropy . The objective becomes:
$$ J(\theta) = \mathbb{E}[G_t] + \beta \mathbb{E}[H(\pi_\theta(\cdot \mid S_t))] $$
where $H(\pi)$ is the Shannon entropy of the policy and $\beta > 0$ is a temperature parameter controlling the emphasis on exploration. Maximizing entropy promotes more stochastic policies.

For a given action-[value function](@entry_id:144750) $Q(s,a)$, the policy that optimizes this objective is the **Boltzmann** or **[softmax](@entry_id:636766)** policy:
$$ \pi^*(a \mid s) = \frac{\exp(Q(s,a)/\beta)}{\sum_{a'} \exp(Q(s,a')/\beta)} $$
As $\beta \to 0$, the policy becomes deterministic and purely exploitative (greedy). As $\beta \to \infty$, the policy approaches a uniform random distribution, maximizing exploration. This framework also gives rise to a "soft" version of the Bellman backup, where the hard maximum operator is replaced by a smooth `[log-sum-exp](@entry_id:1127427)` operator: $V(s) = \beta \log \sum_a \exp(Q(s,a)/\beta)$, which converges to $\max_a Q(s,a)$ as $\beta \to 0$.

#### Temporal Abstraction: Hierarchy and Predictive Maps

Real-world behavior is hierarchical. We choose high-level goals (e.g., "make coffee") which are composed of lower-level actions. The **options framework** formalizes such temporally extended actions. An option is a triple $(\mathcal{I}, \pi, \beta)$ consisting of an initiation set of states $\mathcal{I}$, an intra-option policy $\pi$, and a termination condition $\beta$ . When an option is chosen, its policy $\pi$ is followed until the termination condition is met. This transforms the decision problem into a **Semi-Markov Decision Process (SMDP)**, where decisions are made between options, not just primitive actions. The duration of these "macro-actions" is variable, which requires adjusting the [value function](@entry_id:144750) updates to account for the compounded discount factor $\gamma^\tau$ over the option's duration $\tau$ . This hierarchical structure is thought to be implemented by the nested architecture of cortico-striatal loops, with prefrontal loops selecting abstract options and sensorimotor loops implementing their constituent actions.

Another powerful approach to temporal abstraction is the **Successor Representation (SR)**. The SR, denoted $M_\pi(s, s')$, encodes the expected discounted future occupancy of state $s'$ when starting in state $s$ and following policy $\pi$:
$$ M_\pi(s,s') = \mathbb{E}_\pi\left[\sum_{t=0}^{\infty} \gamma^t \mathbf{1}\{S_t=s'\} \mid S_0=s\right] $$
where $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167). The SR satisfies its own Bellman equation and can be expressed in matrix form as $M_\pi = (I - \gamma P_\pi)^{-1}$, where $P_\pi$ is the [state-transition matrix](@entry_id:269075) under policy $\pi$.

The key utility of the SR lies in its factorization of the [value function](@entry_id:144750) when rewards depend only on states, $r(s')$ :
$$ V_\pi(s) = \sum_{s' \in \mathcal{S}} M_\pi(s, s') r(s') $$
This equation decomposes value into two components: a predictive map of the environment's transition structure under the current policy ($M_\pi$) and the reward values associated with each state ($r$). This has profound implications for [cognitive flexibility](@entry_id:894038). If the rewards in an environment change but the layout remains the same, an agent with an SR representation only needs to re-learn the simple reward vector $r$; it does not need to re-compute the entire value function from scratch. The hippocampus is a leading candidate for encoding such a predictive map, with [place cells](@entry_id:902022) potentially representing rows of the SR matrix. The discount factor $\gamma$ controls the predictive horizon of this map; a larger $\gamma$ leads to more prospective representations, corresponding to larger place fields.

#### State Uncertainty and Partial Observability

Finally, we must address the fact that the brain rarely has access to the true, latent state of the world. Instead, it receives noisy and incomplete **observations**, $o_t$. This scenario is modeled by a **Partially Observable Markov Decision Process (POMDP)**. In a POMDP, an observation $o_t$ is not a [sufficient statistic](@entry_id:173645) of the past, and a simple reactive policy $\pi(a \mid o_t)$ is suboptimal.

The optimal solution to a POMDP involves maintaining a **belief state**, $b_t(s) = P(S_t=s \mid o_t, a_{t-1}, o_{t-1}, \ldots)$, which is a probability distribution over the latent states given the entire history of actions and observations. This belief state is updated at each step using Bayes' rule and becomes the new [sufficient statistic](@entry_id:173645). By transforming the problem into a search for a policy over belief states, $\pi(a \mid b)$, the POMDP becomes a fully observable (though continuous-state) MDP. This belief-[state representation](@entry_id:141201) provides a formal account of how the brain can integrate evidence over time to infer the [hidden state](@entry_id:634361) of its environment and make optimal decisions under uncertainty .