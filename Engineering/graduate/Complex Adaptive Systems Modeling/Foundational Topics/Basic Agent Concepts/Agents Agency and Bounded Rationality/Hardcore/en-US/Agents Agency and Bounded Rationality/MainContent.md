## Introduction
In the study of complex adaptive systems, the concept of the "agent"—an entity capable of goal-directed action—is fundamental. However, traditional models often rely on an idealized notion of perfect rationality, assuming agents possess unlimited computational power and information. This assumption creates a significant gap between theory and the observable behavior of humans, organizations, and even artificial systems, which are invariably constrained by real-world limitations. This article bridges that gap by providing a comprehensive exploration of agency through the more realistic lens of [bounded rationality](@entry_id:139029). We will begin by establishing the foundational "Principles and Mechanisms", moving from a formal definition of agency to the specific models—such as satisficing and [rational inattention](@entry_id:1130592)—that describe decision-making under constraints. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the broad utility of these concepts in explaining phenomena across economics, cognitive science, and AI safety. Finally, the "Hands-On Practices" section will offer the opportunity to engage directly with these ideas through guided quantitative problems, solidifying the theoretical knowledge.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms that define an entity as an agent within a [complex adaptive system](@entry_id:893720). We will move from a formal, causal definition of agency to the spectrum of rational decision-making, contrasting the ideal of perfect rationality with the more realistic framework of bounded rationality. Through a series of formal models, we will explore specific mechanisms—such as [satisficing](@entry_id:1131222), computational trade-offs, and information-processing constraints—that govern the behavior of boundedly rational agents. Finally, we will broaden our perspective to include intrinsic motivations and rationality under ambiguity, providing a comprehensive toolkit for modeling intelligent behavior in complex environments.

### Defining Agency: A Causal and Teleological Perspective

At its core, agency is distinguished from passive dynamics by the concept of goal-directed action. An agent is not merely a component of a system that reacts to stimuli; it is a subsystem that possesses goals and acts to influence the environment in service of those goals. To formalize this, we can employ the language of Structural Causal Models (SCMs) and Markov Decision Processes (MDPs).

Consider a system where an entity's action $a_t$ can influence the subsequent state of the environment $x_{t+1}$. A purely mechanical description might specify a fixed feedback rule. However, to qualify as an agent, this entity's action-selection process, or **policy**, must be contingent on an internal **goal parameter**, which we can denote by $g$. This goal parameter determines the agent's preferences, often via a utility function $U$. The full causal chain of agency is therefore teleological: a change in goals propagates to a change in actions, which in turn propagates to a change in environmental outcomes.

A rigorous, operational definition of an agent requires three conditions :
1.  **Goal-Contingent Action Selection**: The agent's policy, $\Pi$, which generates action $a_t$, must be a function of the goal parameter $g$. In an SCM, this is represented by a causal link $g \to a_t$.
2.  **Causal Influence on the Environment**: The agent's action $a_t$ must have a causal effect on the future state of the environment $x_{t+1}$. In an SCM, this is a link $a_t \to x_{t+1}$.
3.  **Optimization Under Constraints**: The policy is not arbitrary but is the result of an optimization process that seeks to maximize [expected utility](@entry_id:147484), subject to constraints on available resources (e.g., computational budget, information). This acknowledges that real-world agents operate under limitations, a concept we will explore as **bounded rationality**.

The definitive test for agency is counterfactual. If we could perform a causal intervention on the agent's goal, setting it from $g$ to a new value $g'$ using the $do$-operator, $do(g=g')$, we would observe a change in the probability distribution of the agent's actions, and consequently, a change in the distribution of future environmental states. That is, for an agent, there must exist some $g, g'$ such that $P(x_{t+1} | do(g=g')) \neq P(x_{t+1} | do(g=g))$. A passive dynamical subsystem, in contrast, would fail this test: either its actions have no effect on the environment, or its actions are invariant to its goals . This distinction is crucial: it separates systems that merely exhibit regularities from those that are genuinely goal-seeking .

As a concrete illustration, consider a simple linear-Gaussian SCM where goal attainment $G$ is a linear function of the next state $S'$, $G = \theta S'$, and the [system dynamics](@entry_id:136288) are $S' = \alpha S + \gamma A$. An agent's policy is $A = bS + \epsilon_A$. We can quantify the "causal leverage" of different interventions. An external intervention on the action channel, $do(A=a)$, yields an expected goal attainment that changes with $a$ at a rate of $\frac{d}{da} E[G | do(A=a)] = \theta\gamma$. An intervention on the state channel, $do(S=s)$, allows the agent to react, and the expected goal attainment changes with $s$ at a rate of $\frac{d}{ds} E[G | do(S=s)] = \theta\alpha + \theta\gamma b$. A statistic that compares these causal pathways can reveal the structure of the agent's policy encoded in the parameter $b$. For instance, the difference in these two [marginal effects](@entry_id:634982), $\theta(\gamma - \alpha - \gamma b)$, provides a quantitative signature of the agent's embedded policy .

### The Ideal of Perfect Rationality in Sequential Decisions

Before examining the "bounds" on rationality, we must first define the ideal. In the context of [sequential decision-making](@entry_id:145234) under uncertainty, such as a Partially Observable Markov Decision Process (POMDP), perfect rationality can be decomposed into two aligned components: instrumental and epistemic rationality .

**Instrumental rationality** is the principle of choosing actions to best achieve one's objectives. For a sequential problem with a [utility function](@entry_id:137807) $u(s, a)$ and a discount factor $\beta$, this means selecting a policy $\pi$ that maximizes the total expected discounted utility over the planning horizon:
$$
\pi^* \in \arg\max_{\pi} \mathbb{E}_{\pi} \left[ \sum_{t=0}^{T} \beta^t u(s_t, a_t) \right]
$$
This is the "what to do" aspect of rationality.

**Epistemic rationality** concerns the agent's beliefs about the world. It is the principle of maintaining a coherent set of beliefs and updating them in response to new evidence according to the laws of probability. This means beliefs must conform to the Kolmogorov axioms and be updated from a prior to a posterior distribution via Bayes' rule upon receiving new information (e.g., an observation $o_t$). This is the "what to believe" aspect of rationality.

In a perfectly rational agent, these two components are seamlessly aligned. This alignment is guaranteed by the principle of **dynamic consistency**: a plan of action deemed optimal today remains optimal at every future decision point, given the information available at that time. The mathematical mechanism ensuring this consistency is the **Bellman optimality equation**. For a POMDP, where an agent's knowledge is captured by the history of observations and actions $h_t$, the optimal value function $V_t(h_t)$ satisfies:
$$
V_t(h_t) = \max_{a \in \mathcal{A}} \mathbb{E} \big[ u(s_t, a) + \beta V_{t+1}(h_{t+1}) \mid h_t, a \big]
$$
This recursive equation breaks a complex, long-term optimization problem into a series of smaller, stage-wise decisions. The law of [iterated expectations](@entry_id:169521) guarantees that solving this equation at each step is equivalent to solving the global, ex-ante optimization problem. Thus, for a perfect Bayesian expected-utility maximizer, planning and acting are perfectly aligned .

### Mechanisms of Bounded Rationality

The ideal of perfect rationality assumes unlimited computational power and costless information. Real-world agents, from humans to organizations to AI systems, are subject to constraints. **Bounded rationality**, a concept pioneered by Herbert Simon, is not irrationality but rather the study of how agents make rational decisions given these constraints. It is a framework of optimization under constraints. We now explore several key mechanisms.

#### Satisficing: Search with Aspiration Levels

One of the earliest and most influential models of [bounded rationality](@entry_id:139029) is **satisficing**. Instead of seeking the single best, globally optimal option, a satisficing agent searches for an option that is "good enough." This is formalized by an **aspiration level**, $\alpha$. The agent's goal is not to maximize utility, but to find any option whose utility meets or exceeds this threshold.

Consider an agent who can inspect a stream of options, with utilities drawn independently from a distribution with CDF $F$. Each inspection incurs a cost $c > 0$. The [optimal stopping](@entry_id:144118) rule for a [satisficing](@entry_id:1131222) agent is simple: inspect options sequentially and stop at the first one, say at time $t$, for which the utility $U_t \ge \alpha$. Because any option meeting the aspiration is equally good, there is no reason to pay another cost $c$ to continue searching. The agent's problem reduces to minimizing the expected total search cost. The probability of any given option being satisfactory is $p = 1 - F(\alpha)$. The search is a sequence of Bernoulli trials, and the number of inspections follows a [geometric distribution](@entry_id:154371). The minimal expected total inspection cost is therefore :
$$
\mathbb{E}[\text{Total Cost}] = \frac{c}{1 - F(\alpha)}
$$
This elegant result shows how the agent's behavior (expected search duration and cost) is a direct function of its internal aspiration level ($\alpha$), the cost of thinking ($c$), and the statistical structure of the environment ($F$).

The trade-off between satisficing and optimizing can be made precise using the concept of **expected regret**. Regret measures the [expected shortfall](@entry_id:136521) of a strategy relative to an omniscient chooser who knows all outcomes at no cost. If we consider a finite set of $n$ options, an optimizing strategy would inspect all $n$ options at a total cost of $cn$ and select the maximum. A satisficing strategy would inspect options until its threshold $\tau$ is met, potentially saving on search costs but risking a lower payoff. The difference in expected regret between these two strategies, $\Delta R = R_{\mathrm{opt}} - R_{\mathrm{sat}}$, explicitly quantifies the trade-off. For options drawn from a $\mathrm{Uniform}([0,1])$ distribution, this difference can be derived analytically, revealing a complex interplay between the search cost $c$, the number of options $n$, and the aspiration level $\tau$ .

#### Computational Rationality: The Economics of Deliberation

A more general approach is to model the agent's internal deliberation process as an economic choice. Thinking, simulating, or planning takes time and energy. **Computational rationality** (or resource rationality) frames decision-making as a meta-level optimization problem: the agent must decide how much computational effort to expend to improve its decision quality.

Imagine an agent whose probability of success, $p(d)$, increases with the depth of its computation or lookahead, $d$, but with [diminishing returns](@entry_id:175447), e.g., $p(d) = 1 - \exp(-kd)$. This computation incurs a cost, $C(d) = cd$. The agent's problem is to choose the optimal depth $d^*$ that maximizes its expected utility *net of the cost of computation*. This can be formulated as an [unconstrained optimization](@entry_id:137083) problem using a Lagrange multiplier $\lambda$, which represents the shadow price of the computational resource:
$$
\max_{d} \left( \mathbb{E}[U \mid d] - \lambda C(d) \right) = \max_{d} \left( U_{\max}(1 - \exp(-kd)) - \lambda c d \right)
$$
By taking the derivative with respect to $d$ and setting it to zero, we find the [first-order optimality condition](@entry_id:634945), which equates the marginal benefit of computation with its marginal cost. Solving for $d$ gives the resource-rational computation intensity :
$$
d^* = \frac{1}{k} \ln\left(\frac{k U_{\max}}{\lambda c}\right)
$$
This result formalizes the intuition that an agent should think more about decisions that are high-stakes ($U_{\max}$) and where thinking is effective ($k$), and think less when computation is costly ($c$, $\lambda$).

#### Rational Inattention: Constraints on Information Processing

A particularly powerful framework for bounded rationality is **[rational inattention](@entry_id:1130592)**, developed by economist Christopher Sims. Here, the constraint is not on abstract "computation," but on the agent's capacity to process information, quantified by information theory. The agent is assumed to have a finite budget for the amount of information (measured in nats or bits) it can extract about the state of the world.

Consider an agent who needs to estimate an uncertain state $s$, which has a Gaussian [prior distribution](@entry_id:141376) $s \sim \mathcal{N}(0, \sigma_s^2)$. The agent's loss is quadratic, $\mathbb{E}[(s-a)^2]$, meaning the best action $a$ is the [posterior mean](@entry_id:173826) estimate $\mathbb{E}[s|x]$ based on some signal $x$. The agent chooses a signal channel $p(x|s)$ subject to an information budget: the mutual information between the state and the signal cannot exceed a capacity $\kappa$, i.e., $I(s;x) \le \kappa$. The agent's problem is to design the optimal channel that minimizes the expected posterior variance of its estimate.

For the Gaussian case, the solution is particularly elegant. The minimum achievable posterior variance under an information constraint $\kappa$ is :
$$
\mathrm{Var}(s \mid x) = \sigma_s^2 \exp(-2\kappa)
$$
This equation beautifully connects a core statistical quantity (posterior variance, which measures uncertainty) to an information-theoretic one ([channel capacity](@entry_id:143699)). It shows that the reduction in uncertainty is an exponential function of the information-processing capacity. An agent with zero capacity ($\kappa=0$) has a posterior variance equal to the prior variance $\sigma_s^2$; it learns nothing. An agent with infinite capacity can, in principle, reduce its uncertainty to zero. This model provides a rigorous and flexible way to analyze how agents allocate their limited attention in complex environments.

### Intrinsic Motivation and Extended Rationality

Our discussion so far has assumed that agents are driven by extrinsic rewards or utility functions. However, agents can also be guided by intrinsic objectives. Furthermore, rationality can be extended to handle deeper forms of uncertainty than mere risk.

#### Empowerment: The Drive for Control

What should an agent do in the absence of any specific task or reward? One compelling answer is that it should act to keep its options open and maintain its ability to influence the future. This intrinsic motivation is formalized by the concept of **empowerment**. Empowerment is defined as the [channel capacity](@entry_id:143699) of the agent's action-to-state channel. It is the maximum mutual information the agent can "inject" into its future states by choosing its actions optimally. Formally, at a given state $s$:
$$
\text{Empowerment}(s) = C(s) = \max_{p(a)} I(A; S')
$$
where $S'$ is the successor state. Empowerment measures the agent's potential for control. It is high in states from which actions lead to a wide and distinguishable variety of possible futures. It is low in states where all actions lead to the same outcome, or where the outcomes are random and uncontrollable.

An empowerment-maximizing agent will prefer states with higher empowerment, as these states offer more future control. For example, consider a state $s_0$ where three actions lead to three very different probability distributions over successor states, and a state $s_1$ where all three actions lead to the exact same successor distribution. The empowerment at $s_1$ is zero, because the action $A$ and the successor state $S'$ are statistically independent. The empowerment at $s_0$, however, will be positive. An agent guided by this intrinsic objective would therefore navigate towards $s_0$, demonstrating purposeful behavior without any external reward signal .

#### Rationality Under Ambiguity

Standard [expected utility theory](@entry_id:140626) assumes agents face **risk**, where probabilities are known. Many real-world situations, however, involve **ambiguity** (or Knightian uncertainty), where the probabilities themselves are unknown. The famous Ellsberg paradox shows that people often have a preference for risk over ambiguity, a behavior that violates standard [expected utility theory](@entry_id:140626).

Modern decision theories, such as the **smooth ambiguity model**, extend the concept of rationality to accommodate such preferences. This model proposes a two-stage evaluation process. An agent has a second-order belief $\mu$ over a set of possible first-order probability models $P$. The value of an act $f$ is given by:
$$
V(f) = \int \phi\left(\int u(f) dP\right) d\mu(P)
$$
Here, $\phi$ is an increasing function whose [concavity](@entry_id:139843) measures ambiguity aversion. If $\phi$ is concave, the agent dislikes the "mean-preserving spread" of possible expected utilities and is ambiguity-averse. If $\phi$ is linear, the model reduces to standard subjective [expected utility](@entry_id:147484).

By observing an agent's choices—for instance, the known probability $q$ that makes them indifferent between a risky act and an ambiguous one—we can use this framework to identify their ambiguity preferences. Given a functional form for $\phi$, such as $\phi(t) = t^{1-\alpha}$, we can solve for the ambiguity aversion parameter $\alpha$, providing a quantitative measure of this aspect of the agent's rationality . This demonstrates that even behaviors that seem "irrational" under a narrow definition can be understood as coherent and principled under a richer model of decision-making.