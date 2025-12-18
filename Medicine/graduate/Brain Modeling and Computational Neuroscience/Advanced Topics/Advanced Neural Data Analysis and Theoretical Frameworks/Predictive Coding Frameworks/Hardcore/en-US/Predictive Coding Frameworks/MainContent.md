## Introduction
In the quest to understand the brain, few ideas have been as encompassing as the theory of predictive coding. This framework repositions the brain not as a passive receiver of sensory information, but as a proactive, prediction-generating machine. Its central tenet—that the brain's primary function is to infer the causes of its sensations by continuously minimizing the error between its predictions and reality—offers a powerful, unifying principle for brain function. For decades, neuroscience has grappled with the problem of how the brain's intricate biological hardware could implement the sophisticated computations required for perception and cognition. Predictive coding addresses this gap by providing a neurally plausible and mathematically rigorous account of how the brain might approximate optimal Bayesian inference.

This article will guide you through the core tenets and expansive reach of the predictive coding framework. We will begin in the first chapter, **"Principles and Mechanisms"**, by deconstructing the framework's mathematical foundations in [variational free energy](@entry_id:1133721) and exploring how the simple imperative of minimizing prediction error gives rise to complex neural dynamics. We will then see how these abstract principles map onto the canonical microcircuitry of the cortex. In the second chapter, **"Applications and Interdisciplinary Connections"**, we will survey the framework's remarkable explanatory power, showing how it provides a unified understanding of perception, action, attention, and learning, while also offering profound insights into mental illness and inspiring next-generation artificial intelligence. Finally, in the third chapter, **"Hands-On Practices"**, you will have the opportunity to engage directly with the core computations through a series of guided exercises, solidifying your understanding of how the brain turns prediction into perception.

## Principles and Mechanisms

The [predictive coding](@entry_id:150716) framework provides a comprehensive and neurally plausible theory of how the brain might implement Bayesian inference. At its core, the framework posits that the brain continuously generates predictions about the causes of its sensory inputs and uses the discrepancy between these predictions and the actual sensory signals—the prediction error—to update its internal model of the world. This chapter will deconstruct the fundamental principles and mechanisms that govern this process, beginning with its formulation as a problem of approximate Bayesian inference and culminating in its mapping onto the canonical microcircuitry of the cerebral cortex.

### Predictive Coding as Approximate Bayesian Inference

The central problem for the brain, from a Bayesian perspective, is to infer the hidden **latent causes** ($s$) in the world that give rise to its sensory observations ($y$). This requires an internal **generative model**, a probabilistic model $p(y, s)$ that specifies the [joint probability](@entry_id:266356) of causes and their sensory consequences. According to Bayes' rule, the desired [posterior probability](@entry_id:153467) of the causes given the sensory data is:

$p(s | y) = \frac{p(y | s) p(s)}{p(y)}$

Here, $p(y|s)$ is the **likelihood** (the probability of observing $y$ given cause $s$), $p(s)$ is the **prior** (the brain's initial belief about the cause), and $p(y) = \int p(y|s)p(s)ds$ is the **[model evidence](@entry_id:636856)** (or [marginal likelihood](@entry_id:191889)). Computing the posterior directly is often intractable, primarily because calculating the evidence $p(y)$ requires integrating over all possible causes, a high-dimensional and complex operation.

Predictive coding resolves this by recasting inference as an optimization problem. Instead of computing the true posterior $p(s|y)$ directly, the brain seeks to find an approximate posterior distribution, $q(s)$, that is as close as possible to the true posterior. The "closeness" between these distributions is measured by the **Kullback-Leibler (KL) divergence**, $\mathrm{KL}[q(s) \| p(s|y)]$. The optimization is performed by minimizing an objective function known as **Variational Free Energy (VFE)**, denoted as $F(q)$.

The VFE is defined in several equivalent ways, but a particularly insightful formulation links it directly to the model evidence and the KL divergence :

$F(q) = \mathbb{E}_{q}[\ln q(s) - \ln p(y, s)] = \mathrm{KL}[q(s) \| p(s|y)] - \ln p(y)$

Since the KL divergence is always non-negative ($\mathrm{KL}[\cdot \| \cdot] \ge 0$), this identity reveals that $-\ln p(y)$, the negative log model evidence (also known as **[surprisal](@entry_id:269349)**), is an upper bound for the VFE. A more common rearrangement in machine learning defines the Evidence Lower Bound (ELBO) as $\mathcal{L}(q) = -F(q) = \ln p(y) - \mathrm{KL}[q(s) \| p(s|y)]$. Because the log evidence $\ln p(y)$ is constant with respect to $q$, minimizing the VFE $F(q)$ is equivalent to minimizing the KL divergence, thereby making the approximate posterior $q(s)$ a better and better proxy for the true posterior $p(s|y)$. In this view, perception is the process of minimizing [variational free energy](@entry_id:1133721).

### The Energetics of Perception: Minimizing Prediction Error

The abstract principle of minimizing VFE acquires a more concrete and intuitive form when we specify the structure of the generative model. The [predictive coding](@entry_id:150716) framework typically assumes a hierarchical structure where causes at one level generate predictions for the level below. Furthermore, it is often assumed that the relationship between levels and the associated noise are Gaussian. These assumptions are not merely for mathematical convenience; they lead to an elegant formulation where [free energy minimization](@entry_id:183270) becomes equivalent to minimizing the sum of precision-weighted prediction errors.

Let us consider a simple generative model with a single latent cause $x$ and a sensory observation $y$. The [prior belief](@entry_id:264565) about the cause is $p(x) = \mathcal{N}(x; \mu_p, \sigma_p^2)$, and the likelihood of the observation is $p(y|x) = \mathcal{N}(y; x, \sigma_s^2)$. The brain's estimate (or belief) about the latent cause is the mean of the recognition density, $\mu$. Under a common simplification known as the **Laplace approximation**, the VFE (ignoring the entropy of the recognition density, which does not affect the optimization of its mean) becomes proportional to the negative log [joint probability](@entry_id:266356) evaluated at the mean of the belief:

$F(\mu) \approx -\ln p(y|\mu) - \ln p(\mu)$

Substituting the Gaussian forms, we get:

$F(\mu) = \frac{1}{2\sigma_s^2}(y - \mu)^2 + \frac{1}{2\sigma_p^2}(\mu - \mu_p)^2 + \text{constants}$

It is useful to define **precision** as the inverse of variance, so $\Pi_s = \sigma_s^{-2}$ and $\Pi_p = \sigma_p^{-2}$. Precision quantifies the confidence in a belief or signal; high precision implies low uncertainty. We can also define the **[sensory prediction error](@entry_id:1131481)**, $\epsilon_s = y - \mu$, and the **prior prediction error**, $\epsilon_p = \mu - \mu_p$. With these definitions, the free energy becomes a sum of precision-weighted squared prediction errors :

$F(\mu) = \frac{1}{2}\Pi_s \epsilon_s^2 + \frac{1}{2}\Pi_p \epsilon_p^2 + \text{constants}$

This formulation reveals the essence of the predictive coding objective: the brain adjusts its internal estimate $\mu$ to find a balance between [explaining away](@entry_id:203703) the sensory data (minimizing $\epsilon_s$) and adhering to its prior beliefs (minimizing $\epsilon_p$). The balance between these two objectives is mediated by their respective precisions. If sensory precision $\Pi_s$ is high (i.e., the sensory signal is reliable), the estimate $\mu$ will be pulled closer to the observation $y$. Conversely, if prior precision $\Pi_p$ is high (i.e., the [prior belief](@entry_id:264565) is strong), the estimate will be pulled closer to the prior mean $\mu_p$.

### Neural Dynamics as Gradient Descent on Free Energy

If perception is the process of minimizing free energy, how might the brain implement this minimization? Predictive coding proposes a simple and neurally plausible mechanism: neural activity, representing the brain's beliefs, evolves over time according to **gradient descent** on the free energy landscape. The estimate of the latent cause, $\mu$, changes in the direction opposite to the gradient of the free energy:

$\dot{\mu} \propto -\frac{\partial F}{\partial \mu}$

For our simple model, the gradient is:

$\frac{\partial F}{\partial \mu} = \frac{\partial}{\partial \mu} \left( \frac{1}{2}\Pi_s (y - \mu)^2 + \frac{1}{2}\Pi_p (\mu - \mu_p)^2 \right) = -\Pi_s(y - \mu) + \Pi_p(\mu - \mu_p)$

The update dynamics for the belief $\mu$ are therefore:

$\dot{\mu} \propto \Pi_s(y - \mu) - \Pi_p(\mu - \mu_p)$

This simple equation is the cornerstone of predictive coding dynamics. It states that the belief $\mu$ is driven by two forces: a bottom-up term proportional to the precision-weighted [sensory prediction error](@entry_id:1131481), $\Pi_s \epsilon_s$, which pushes the belief towards the sensory data, and a top-down term proportional to the precision-weighted prior prediction error, $-\Pi_p \epsilon_p$, which pushes the belief towards the prior mean. The system reaches a stable state, or **fixed point**, when $\dot{\mu} = 0$. At this point, the opposing forces are balanced:

$\Pi_s(y - \mu) = \Pi_p(\mu - \mu_p) \implies \mu = \frac{\Pi_s y + \Pi_p \mu_p}{\Pi_s + \Pi_p}$

This fixed point is precisely the mean of the true Bayesian posterior, which for this simple conjugate model is $\mathcal{N}(\mu; \frac{\Pi_s y + \Pi_p \mu_p}{\Pi_s + \Pi_p}, (\Pi_s + \Pi_p)^{-1})$. Thus, the process of gradient descent on free energy allows the [neural circuit](@entry_id:169301) to dynamically converge on the optimal Bayesian estimate of the hidden cause  .

The precise formulation of the update dynamics depends on the sign conventions used for the prediction errors. The definitions $\epsilon_y = y - g(\mu)$ for sensory error (where $g(\cdot)$ is the generative function) and $\epsilon_s = \mu - f(\mu)$ for state prediction error (where $f(\cdot)$ is the prior mean function) are chosen specifically so that the [gradient descent](@entry_id:145942) dynamic $\dot{\mu} \propto -\nabla_\mu F$ naturally takes the form of a corrective process, reducing both error terms .

This mechanism generalizes elegantly to deep, non-linear hierarchies. For any intermediate level $i$ in the hierarchy, the belief $\mu_i$ is influenced by two sources: the precision-weighted [error signal](@entry_id:271594) coming up from the level below, $\epsilon_{i-1}$, and the constraining prediction coming down from the level above, encoded in the error term $\epsilon_i$. The update for $\mu_i$ can be written schematically as :

$\dot{\mu}_i \propto \big[\partial_{\mu_i} g_i(\mu_i)\big]^{\top} \Pi_{i-1} \epsilon_{i-1} - \Pi_i \epsilon_i$

Here, $g_i(\mu_i)$ is the prediction of level $i-1$ generated from $\mu_i$, and the Jacobian term $\partial_{\mu_i} g_i$ projects the error from the lower level's space into the appropriate direction for updating $\mu_i$. This equation elegantly captures the [message-passing](@entry_id:751915) scheme central to predictive coding: **bottom-up feedforward connections convey precision-weighted prediction errors, while top-down feedback connections convey predictions**. Crucially, the update for any given level only requires messages from its immediate neighbors, ensuring that the computation is local and scalable. These minimal assumptions—a hierarchical generative model with conditionally independent Gaussian noise and differentiable mappings, combined with a Laplace approximation for inference via gradient descent on VFE—are sufficient for the entire [predictive coding](@entry_id:150716) scheme to emerge .

### Hierarchical Models and Empirical Priors

In a simple Bayesian model, the prior $p(s)$ is fixed. A powerful feature of [hierarchical models](@entry_id:274952) is that they furnish **empirical priors**. In a deep hierarchy, the prior for a given level is not static; instead, it is dynamically supplied by the top-down prediction from the level above.

Consider a two-level model where a high-level cause $x_1$ generates a low-level cause $x_0$, which in turn generates the sensory data $y$. The generative model factorizes as $p(y, x_0, x_1) = p(y|x_0) p(x_0|x_1) p(x_1)$. Here, the distribution $p(x_0|x_1) = \mathcal{N}(x_0; g(x_1), \Sigma_{p0})$ serves as the prior for $x_0$. However, its mean, $g(x_1)$, is not a fixed value but a function of the higher-level cause $x_1$.

During inference, the brain's posterior estimate for the high-level cause is $\mu_1$. This top-down belief provides the prior expectation for the lower level, $g(\mu_1)$. This makes the prior "empirical" because its parameters are themselves inferred from the data via the higher levels of the model. The prior prediction error at the lower level, which drives the update of its belief $\mu_0$, is therefore the discrepancy between its current state and this top-down empirical prediction: $\epsilon_0^{\text{prior}} = \mu_0 - g(\mu_1)$ . This mechanism allows the brain to flexibly adapt its priors based on context, which is encoded in the activity of higher cortical areas.

### Extending the Framework: Dynamics and Learning

The principles described thus far apply to inferring static causes. However, the world is dynamic. Predictive coding can be extended to handle temporal sequences by incorporating dynamics into the generative model. A **dynamic generative model** includes predictions about how latent states evolve over time, for example, through a state-transition function $s_{t+1} = f(s_t) + \omega_t$, where $\omega_t$ is [process noise](@entry_id:270644).

In this setting, inference at time $t$ involves minimizing prediction errors of two kinds:
1.  A **[sensory prediction error](@entry_id:1131481)**, $y_t - g(\mu_t)$, which is the mismatch between the current observation and the prediction generated from the current belief.
2.  A **[dynamic prediction](@entry_id:899830) error**, $\mu_t - f(\mu_{t-1})$, which is the mismatch between the current belief and the belief predicted based on the previous moment in time.

The update for the belief $\mu_t$ is thus driven by both sensory evidence and the need for temporal consistency, coupling the inference process across time . It is important to note that in a standard filtering scheme, the update for $\mu_t$ only depends on past ($\mu_{t-1}$) and present ($y_t$) information; terms involving future states ($\mu_{t+1}$) only arise in more complex "smoothing" algorithms that revise past beliefs in light of new evidence.

A final, crucial distinction must be made between **inference** and **learning**.
-   **Inference (Perception)** is the fast process of updating neural activity (the beliefs, or parameters of $q(s)$) to find the latent causes of a specific, incoming sensory signal. This occurs on the timescale of perception, while the model parameters $\theta$ are held constant.
-   **Learning (Plasticity)** is the slow process of updating the model parameters $\theta$ themselves (e.g., synaptic weights) to improve the generative model's ability to predict sensory data in the long run.

Both inference and learning are driven by the same objective of minimizing free energy. However, they operate on different arguments of the free energy function and on different timescales. Learning corresponds to a slow [gradient descent](@entry_id:145942) on $F$ with respect to the parameters $\theta$, which typically involves accumulating statistics (such as the average correlation between prediction errors and neural activity) over many observations. This formal separation of optimizing beliefs versus optimizing model parameters provides a principled explanation for the different timescales of perception and synaptic plasticity .

### A Neurobiological Implementation

A compelling aspect of the [predictive coding](@entry_id:150716) framework is its plausible mapping onto the laminar structure of the neocortex. A canonical microcircuit has been proposed where different neural populations, segregated by [cortical layers](@entry_id:904259), perform the distinct computations of prediction and error calculation .

-   **Prediction Units**, which encode the expectations or beliefs about latent causes ($\mu_i$), are thought to be instantiated by large [pyramidal neurons](@entry_id:922580) in the **deep layers** of the cortex (e.g., Layers 5 and 6). These neurons are the principal source of top-down feedback projections, sending predictions to lower-level cortical areas or to superficial layers within the same cortical column.

-   **Error Units**, which compute the mismatch between predictions and observations ($\epsilon_i$), are thought to be instantiated by [pyramidal neurons](@entry_id:922580) in the **superficial layers** (e.g., Layers 2 and 3). These neurons receive bottom-up sensory or transthalamic input, as well as top-down predictions from the deep layers. Their activity represents the residual "unexplained" part of the input, which is then passed forward to the deep layers of the same column and up to higher cortical areas.

This architecture naturally implements the required [message-passing](@entry_id:751915). A top-down prediction from a deep-layer cell ($\hat{y}$) arrives at the superficial layers, where it is compared with the bottom-up input ($y$). The subtraction required for error computation, $\varepsilon = y - \hat{y}$, is likely mediated by [inhibitory interneurons](@entry_id:1126509) that are driven by the deep-layer prediction cells. The resulting error signal, encoded by superficial-layer cells, then projects excitatorily to the deep-layer prediction cells, driving them to update their activity in a way that minimizes the error. This recurrent loop of top-down prediction and bottom-up [error correction](@entry_id:273762) continues until the free energy is minimized and a stable percept is formed. The synaptic weights mediating these interactions are slowly updated via Hebbian-like plasticity rules, driven by the correlations between the activity of prediction and error units, thereby implementing the learning component of the framework.