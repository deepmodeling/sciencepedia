## Introduction
Computational [psychiatry](@entry_id:925836) is a burgeoning field that bridges the gap between the descriptive classifications of mental illness and the complex neural mechanisms that underlie them. By applying formal mathematical and computational tools to the brain and behavior, it aims to move beyond asking *what* the symptoms of a disorder are, to asking *why* they arise. This approach addresses a fundamental gap in modern medicine—the lack of mechanistic, testable theories for many psychiatric conditions. It provides a formal language to generate precise hypotheses about how disruptions at the level of neurons, circuits, and learning rules can manifest as the subjective experiences and maladaptive behaviors seen in clinical practice.

This article offers a comprehensive journey into this exciting field. We begin in "Principles and Mechanisms" by building a foundational toolkit of computational models, starting from the electrical dynamics of single neurons and synapses, and scaling up to theories of decision-making, learning, and Bayesian inference in the brain. Following this, "Applications and Interdisciplinary Connections" demonstrates how these formalisms are applied to deconstruct and explain a wide range of disorders, from addiction and [psychosis](@entry_id:893734) to anxiety and functional [movement disorders](@entry_id:912830). Finally, a series of "Hands-On Practices" will allow you to directly engage with these models, solidifying your understanding by simulating the very computational processes thought to go awry in mental illness.

## Principles and Mechanisms

Computational [psychiatry](@entry_id:925836) seeks to understand the mechanisms of mental disorders by applying formal mathematical models to brain function and behavior. This chapter delves into the core principles and mechanisms that form the bedrock of this field, organized by levels of analysis—from the electrical dynamics of single neurons to the collective behavior of [large-scale brain networks](@entry_id:895555) and the abstract principles of learning and inference. By grounding our discussion in these fundamental models, we can begin to formulate precise, testable hypotheses about how their dysfunction might give rise to the complex symptomatology of psychiatric illness.

### Modeling the Neuron: From Biophysical Detail to Computational Abstraction

The neuron is the fundamental information-processing unit of the brain. Modeling its behavior is the first step in constructing any biologically grounded model of neural computation. However, neurons are immensely complex biophysical entities, and a trade-off between model fidelity and [computational tractability](@entry_id:1122814) is always necessary. The choice of a neuronal model is therefore not arbitrary but is dictated by the specific scientific question being addressed.

At one end of the spectrum lies the **Hodgkin-Huxley (HH) model**, a landmark achievement in [quantitative biology](@entry_id:261097). This is a **[conductance-based model](@entry_id:1122855)** that describes the generation of an action potential through the dynamics of specific ion channels. The core of the model is a current-balance equation for a patch of [neuronal membrane](@entry_id:182072), conceptualized as an electrical circuit:

$$C_m \frac{dV}{dt} = I_{\text{ext}}(t) - \sum_k g_k (V - E_k)$$

Here, $C_m$ is the membrane capacitance, $V$ is the membrane potential, $I_{\text{ext}}(t)$ is an externally injected current, and the sum is over different types of ion channels (e.g., sodium, potassium, and a passive leak channel). The crucial insight of Hodgkin and Huxley was that the conductances $g_k$ for voltage-gated channels are not constant. Instead, they are functions of voltage and time, controlled by dimensionless **[gating variables](@entry_id:203222)** (e.g., $m$, $h$, and $n$ for sodium activation, [sodium inactivation](@entry_id:192205), and potassium activation, respectively) that each follow their own [first-order differential equations](@entry_id:173139).

Because the HH model explicitly represents the [biophysics of ion channels](@entry_id:175469), it provides unparalleled **fidelity** in reproducing the precise shape and dynamics of action potentials. Its mechanistic transparency makes it the model of choice for studying conditions like **[channelopathies](@entry_id:142187)**, where a [genetic mutation](@entry_id:166469) affects the function of a specific [ion channel](@entry_id:170762). By modifying the equations governing a particular conductance, a researcher can directly simulate the downstream effects of the mutation on [neuronal firing](@entry_id:184180) and, in a network, on circuit-level rhythms. However, this fidelity comes at a high **computational cost**, as it requires numerically integrating a system of several coupled, nonlinear ordinary differential equations for every neuron. This makes simulating large networks of HH neurons computationally prohibitive for many applications .

At the other end of the spectrum are highly simplified models designed for computational efficiency. The quintessential example is the **[leaky integrate-and-fire](@entry_id:261896) (LIF) model**. The LIF neuron is modeled as a simple resistor-capacitor (RC) circuit, whose subthreshold membrane potential is governed by a single, [linear differential equation](@entry_id:169062):

$$\tau_m \frac{dV}{dt} = -(V - E_L) + R_m I_{\text{ext}}(t)$$

where $\tau_m$ is the [membrane time constant](@entry_id:168069). Instead of modeling the biophysical machinery of [spike generation](@entry_id:1132149), the LIF model uses an algorithmic rule: if $V$ reaches a threshold $V_{\text{th}}$, a "spike" is registered, and $V$ is reset to a value $V_{\text{reset}}$. The LIF model is exceptionally fast to simulate, making it a workhorse for studying the dynamics of very large [spiking neural networks](@entry_id:1132168). Its primary limitation is its low biophysical fidelity; it cannot intrinsically reproduce the rich repertoire of firing patterns observed in real neurons, such as bursting or [spike-frequency adaptation](@entry_id:274157), because it lacks the necessary dynamic [state variables](@entry_id:138790) .

Bridging this gap are intermediate models like the **Izhikevich model**. It is a two-dimensional nonlinear dynamical system that, with a simple reset rule, can reproduce a wide variety of biologically observed firing patterns (e.g., regular spiking, bursting, chattering) with remarkable computational efficiency. While powerful for generating realistic spike patterns in large networks, its variables are phenomenological and do not map directly onto specific ion channels. This makes it less suitable than the HH model for investigating questions about specific [channelopathies](@entry_id:142187) or the effects of drugs that target particular channels .

### Modeling Neural Dynamics and Variability

Beyond the generation of individual spikes, a central challenge is to model the continuous, fluctuating dynamics of neural activity, be it the subthreshold membrane potential of a single neuron or the aggregate activity of a neural population. A cornerstone model for this purpose is the **Ornstein-Uhlenbeck (OU) process**, a [stochastic differential equation](@entry_id:140379) that describes the behavior of a variable returning to a mean value in the presence of noise:

$$dx_t = \theta(\mu - x_t)dt + \sigma dW_t$$

Here, $x_t$ is the latent neural state, $\mu$ is the mean to which it reverts, $\theta > 0$ is the rate of [mean reversion](@entry_id:146598), and $\sigma dW_t$ represents stochastic input from a Wiener process with amplitude $\sigma$. This simple model elegantly captures two fundamental properties of [neural dynamics](@entry_id:1128578).

First, the term $\theta(\mu - x_t)dt$ represents a deterministic "pull" or relaxation toward the mean $\mu$. The rate of this pull is governed by $\theta$. The [characteristic time scale](@entry_id:274321) of the process is the **[correlation time](@entry_id:176698)**, $\tau_c = 1/\theta$, which describes how long fluctuations persist. A large $\theta$ implies a short memory and rapid fluctuations, while a small $\theta$ implies a long memory and slow, persistent fluctuations. In a biophysical context, for a neuron's membrane potential, $\theta$ is directly related to the leak conductance; higher leak leads to faster reversion to the resting potential (larger $\theta$, shorter correlation time) .

Second, the term $\sigma dW_t$ represents a stochastic drive, modeling the barrage of noisy synaptic inputs a neuron constantly receives. The parameter $\sigma$ directly controls the amplitude of this noise.

The interplay between these two forces results in a [stationary process](@entry_id:147592) whose probability distribution is Gaussian, with a mean of $\mathbb{E}[x_t] = \mu$ and a variance of $\text{Var}(x_t) = \frac{\sigma^2}{2\theta}$. This relationship is highly instructive: the variability of the neural state increases with the amplitude of the noise ($\sigma$) but decreases with the rate of [mean reversion](@entry_id:146598) ($\theta$). The autocovariance function, which describes the correlation of the process with itself over a time lag $\tau$, decays exponentially: $C(\tau) = \frac{\sigma^2}{2\theta} \exp(-\theta|\tau|)$.

In [computational psychiatry](@entry_id:187590), the OU process provides a powerful tool for formalizing hypotheses about altered [neural variability](@entry_id:1128630). For example, conditions characterized by "noisy" processing, such as Attention-Deficit/Hyperactivity Disorder (ADHD), could be modeled as an increase in the noise amplitude $\sigma$. Conversely, disorders hypothesized to involve cortical disinhibition or a reduction in stabilizing feedback could be modeled by a reduced mean-reversion rate $\theta$. This would lengthen the correlation time ($1/\theta$) and increase variance, leading to more persistent and amplified low-frequency fluctuations in neural activity .

### Learning at the Synapse: Spike-Timing Dependent Plasticity

The connections between neurons are not fixed; they are dynamically modified by experience. A key mechanism for this plasticity is **Spike-Timing Dependent Plasticity (STDP)**, a form of Hebbian learning where the sign and magnitude of a synaptic weight change depend on the precise relative timing of presynaptic and postsynaptic spikes.

The [canonical form](@entry_id:140237) of STDP observed at many excitatory synapses is causal: if a presynaptic neuron fires just before a postsynaptic neuron (a "pre-before-post" pairing), the synapse is strengthened. This is known as **Long-Term Potentiation (LTP)**. Conversely, if the presynaptic neuron fires just after the postsynaptic neuron ("post-before-pre"), the synapse is weakened, a process called **Long-Term Depression (LTD)**. This temporal dependency is often modeled by an asymmetric exponential window. For a single pair of spikes separated by time $\Delta t = t_{\text{post}} - t_{\text{pre}}$, the change in synaptic weight $\Delta w$ can be expressed as:

$$ \Delta w(\Delta t) = \begin{cases} A_+ \exp(-\Delta t/\tau_+) & \text{if } \Delta t > 0 \\ -A_- \exp(\Delta t/\tau_-) & \text{if } \Delta t  0 \end{cases} $$

Here, $A_+$ and $A_-$ are the maximum amplitudes of potentiation and depression, and $\tau_+$ and $\tau_-$ are the time constants of the respective temporal windows .

This simple rule has profound computational consequences. Consider a synapse bombarded by independent, uncorrelated presynaptic and postsynaptic spike trains, modeled as homogeneous Poisson processes with rates $r_{\text{pre}}$ and $r_{\text{post}}$. Even with no correlation, random spike coincidences will drive synaptic changes. The expected rate of change of the synaptic weight, or mean drift, can be calculated by integrating the effect of all possible pairings. This yields:

$$ \left\langle \frac{dw}{dt} \right\rangle = r_{\text{pre}} r_{\text{post}} (A_+ \tau_+ - A_- \tau_-) $$

This equation reveals a crucial insight: the stability of the synapse depends on the balance between the total areas under the LTP and LTD curves. If the area of the LTP window ($A_+ \tau_+$) is greater than the area of the LTD window ($A_- \tau_-$), the synapse will, on average, potentiate even in response to uncorrelated activity. This provides a powerful mechanism for neuromodulators like dopamine to influence learning. A neuromodulatory signal that transiently increases $A_+$ relative to $A_-$ could tip the balance toward net potentiation. In a psychiatric context, a pathologically sustained bias towards potentiation could cause the brain to reinforce spurious, coincidental associations. This forms the basis of the **[aberrant salience](@entry_id:924030)** hypothesis of [psychosis](@entry_id:893734), where meaningless events acquire undue significance, potentially leading to the formation of [delusions](@entry_id:908752) .

### Modeling Decision-Making and Action Selection

Computational [psychiatry](@entry_id:925836) aims to deconstruct complex behaviors like decision-making into underlying computational components. Two dominant frameworks for this are [evidence accumulation](@entry_id:926289) models and reinforcement learning.

#### Evidence Accumulation Models

For simple perceptual decisions between two alternatives, the **Drift-Diffusion Model (DDM)** is a powerful and widely used framework. The DDM proposes that the brain makes a decision by accumulating the difference in sensory evidence for the two options over time. This process is modeled as a single latent decision variable, $x(t)$, that evolves according to a simple [stochastic differential equation](@entry_id:140379):

$$ dx(t) = v dt + \sigma dW_t $$

The process starts at an initial point $x(0) = z$ and terminates when it reaches one of two [absorbing boundaries](@entry_id:746195), typically set at $0$ and $a$. Each parameter of this simple model maps onto a distinct latent cognitive construct :
- **Drift Rate ($v$)**: The average slope of the accumulation process. It represents the quality or strength of the sensory evidence. A larger $|v|$ means clearer evidence and faster, more accurate decisions.
- **Boundary Separation ($a$)**: The distance between the two decision thresholds. It represents the amount of evidence required to commit to a choice and is interpreted as **response caution**. A wider boundary leads to slower, more accurate responses, directly capturing the [speed-accuracy trade-off](@entry_id:174037).
- **Starting Point ($z$)**: The initial value of the decision variable. An unbiased starting point is $z = a/2$. If $z$ is closer to one boundary, it reflects a pre-existing **bias** toward that choice.
- **Noise ($\sigma$)**: The amplitude of the Wiener process, representing moment-to-moment fluctuations in the [evidence accumulation](@entry_id:926289) process.

By fitting the DDM to distributions of reaction times and choices, researchers can obtain quantitative estimates of these latent psychological processes, allowing them to dissociate, for example, whether a patient's poor performance is due to weak evidence processing (low $v$), impulsivity (low $a$), or a response bias (biased $z$). The DDM should be distinguished from **Race Models**, which propose a separate, parallel accumulator for each choice alternative. The DDM is fundamentally a differencing model, reducing the problem to one dimension, while race models are multi-dimensional .

#### Reinforcement Learning Frameworks

For more complex scenarios where actions are chosen to maximize rewards over time, the framework of **Reinforcement Learning (RL)** is indispensable. A critical distinction within RL is between **model-based** and **model-free** control .
- **Model-free (MF) RL** is habitual and reactive. The agent learns the long-term values of actions in particular states (e.g., an action-[value function](@entry_id:144750), $Q(s,a)$) directly from trial-and-error experience, without building an explicit map of the environment.
- **Model-based (MB) RL** is deliberative and prospective. The agent first learns a model of the environment (the transition function $T(s'|s,a)$ and [reward function](@entry_id:138436) $R(s,a)$). It can then use this model to simulate potential future outcomes and plan the best course of action.

This dichotomy is thought to be instantiated in distinct neural circuits and is highly relevant to [psychiatry](@entry_id:925836). For example, compulsive behaviors seen in obsessive-compulsive disorder or addiction can be conceptualized as an imbalance, with an over-reliance on the inflexible model-free system at the expense of the goal-directed model-based system.

The foundation of many RL algorithms is the **Bellman optimality equation**, which defines the value of an [optimal policy](@entry_id:138495) in a recursive manner. For the action-value function $Q^*(s,a)$, it states:

$$ Q^*(s,a) = \mathbb{E}[r + \gamma \max_{a'} Q^*(s', a')] $$

This equation asserts that the value of taking action $a$ in state $s$ is the immediate expected reward $r$ plus the discounted value ($\gamma$) of the best possible action from the next state $s'$. Its validity rests on crucial assumptions, namely that the environment's dynamics are **stationary** (do not change over time) and satisfy the **Markov property** (the future depends only on the current state and action, not the history) .

The neurobiological substrate of RL is closely tied to the neuromodulator dopamine. The **[dopamine reward prediction error](@entry_id:926855) (RPE) hypothesis** posits that the transient, or **phasic**, firing of midbrain [dopamine neurons](@entry_id:924924) does not signal reward itself, but rather the error in the prediction of reward. This corresponds directly to the **temporal-difference (TD) error** from RL theory:

$$ \delta_t = r_{t+1} + \gamma V(s_{t+1}) - V(s_t) $$

where $V(s)$ is the value (expected future reward) of being in state $s$. A positive $\delta_t$ (a better-than-expected outcome) elicits a burst of dopamine, while a negative $\delta_t$ (worse-than-expected) causes a pause in firing. This dopamine signal acts as a global teaching signal, gating synaptic plasticity (as in the STDP rule discussed earlier) to update value estimates throughout the brain . The baseline, or **tonic**, level of dopamine, in contrast, is thought to track the [long-run average reward](@entry_id:276116) rate, providing a reference point for the phasic error signals and potentially modulating motivational vigor .

### The Brain as an Inference Engine: The Bayesian Perspective

An influential and unifying framework in modern computational neuroscience is the **Bayesian Brain Hypothesis**. This theory posits that the brain's fundamental function is to perform [probabilistic inference](@entry_id:1130186). It maintains a generative model of how sensory data are caused by hidden states of the world. Perception is the process of "inverting" this model using Bayes' rule to infer the [posterior probability](@entry_id:153467) of the hidden causes given the sensory evidence.

#### The Bayesian Brain Hypothesis and Predictive Coding

Formally, given a generative model $p(y,x)$ over sensory data $y$ and latent causes $x$, the brain's goal is to compute the posterior $p(x|y)$. As this is often intractable, the brain is thought to perform **approximate Bayesian inference**. **Predictive coding (PC)** is a prominent theory of how the brain might implement this approximation in a neurally plausible manner .

In a [hierarchical predictive coding](@entry_id:1126047) scheme, higher cortical areas send **predictions** of activity down to lower areas. Lower areas, in turn, compare these top-down predictions with their own activity and send the discrepancy—the **prediction error**—back up the hierarchy. Each population of neurons adjusts its representation of the latent variables to minimize the prediction error it receives from the level below. This simple, local message-passing scheme can be shown to perform a sophisticated computation: it minimizes a quantity called **[variational free energy](@entry_id:1133721)**, $F[q]$:

$$ F[q] = \mathbb{E}_{q(x)}[\ln q(x) - \ln p(y,x)] $$

where $q(x)$ is the brain's approximate posterior belief about the latent causes. Minimizing free energy makes the brain's belief $q(x)$ as close as possible to the true posterior $p(x|y)$, thereby optimizing perception [@problem_id:4039899, @problem_id:4039904].

#### A Concrete Example: The Kalman Filter as Predictive Coding

The relationship between Bayesian inference and predictive coding is made concrete by the **Kalman filter**, the optimal algorithm for tracking the state of a linear system with Gaussian noise . The filter's state update equation has precisely the form of a predictive coding update:

$$ \hat{x}_{t|t} = \hat{x}_{t|t-1} + K_t (y_t - C \hat{x}_{t|t-1}) $$

Here, the updated belief about the state, $\hat{x}_{t|t}$, equals the prior prediction, $\hat{x}_{t|t-1}$, plus a correction term. This correction is the [sensory prediction error](@entry_id:1131481) ($y_t - C \hat{x}_{t|t-1}$) weighted by the **Kalman gain**, $K_t$. The gain matrix is computed to optimally balance the uncertainty of the prior prediction with the uncertainty of the sensory data. A key component of the gain is the **precision** (inverse covariance) of the sensory input. If sensory data is noisy and unreliable (low precision, e.g., high observation noise variance $R$), the gain $K_t$ will be low, causing the agent to down-weight the [sensory prediction error](@entry_id:1131481) and rely more heavily on its prior beliefs.

This "[precision-weighting](@entry_id:1130103)" mechanism is a powerful concept in computational psychiatry. For instance, in [schizophrenia](@entry_id:164474), it is hypothesized that a miscalibration of precision—specifically, an under-weighting of sensory evidence precision—could lead the brain to over-rely on its internal priors, potentially giving rise to hallucinations and [delusions](@entry_id:908752) that are not corrected by sensory input [@problem_id:4039877, @problem_id:4039899]. While the Kalman filter provides a perfect illustration of the principle, its computation of the gain $K_t$ is non-local, requiring access to the full covariance matrix. This makes it less biologically plausible as a general cortical algorithm than [predictive coding](@entry_id:150716), which relies only on local message passing .

#### From Perception to Action: Active Inference

The [free energy principle](@entry_id:1125309) can be extended from perception to action, yielding the framework of **Active Inference**. Here, agents act to minimize their expected future free energy. This single objective compellingly unifies two imperatives for action :
1.  **Pragmatic Value**: Agents act to make their preferred outcomes a reality. In this framework, preferences are not specified by an external [reward function](@entry_id:138436) (as in RL), but are an intrinsic part of the agent's generative model in the form of prior beliefs about desired future states.
2.  **Epistemic Value**: Agents act to reduce their uncertainty about the world. This corresponds to an intrinsic drive for exploration and information-seeking, resolving ambiguity about the hidden causes of their sensations.

Active inference thus provides a first-principles account of the [exploration-exploitation dilemma](@entry_id:171683), contrasting with standard RL where exploration is often handled with separate, heuristic mechanisms .

### Large-Scale Brain Networks and Dysconnectivity

Finally, we can zoom out to examine the brain's organization at the macroscopic level. Brain function is supported by a complex network of anatomically and functionally connected regions. Graph theory provides a mathematical language to characterize the topology of these networks. Two key metrics are the **average clustering coefficient ($C$)**, which quantifies the cliquishness of local neighborhoods (a measure of **segregation**), and the **[characteristic path length](@entry_id:914984) ($L$)**, the average shortest distance between all pairs of nodes (a measure of **integration**).

Healthy [brain networks](@entry_id:912843) exhibit a **small-world** architecture, a topology that is simultaneously highly segregated and highly integrated. This is a highly efficient organization, allowing for specialized processing within dense local modules while also supporting rapid communication across the entire network. To formally assess this, one compares the network's $C$ and $L$ to those of equivalent [random graphs](@entry_id:270323) ($C_{\text{rand}}$, $L_{\text{rand}}$), which have poor segregation ($C \approx C_{\text{rand}}$) but excellent integration ($L \approx L_{\text{rand}}$). The **small-worldness index**, $\sigma$, is defined as:

$$ \sigma = \frac{C / C_{\text{rand}}}{L / L_{\text{rand}}} $$

A network is considered small-world if $\sigma > 1$, indicating that its clustering is substantially higher than a random graph's, while its path length remains almost as short .

In computational psychiatry, this network perspective has given rise to the **dysconnectivity hypothesis**, which posits that the symptoms of many disorders arise from aberrant brain network topology. In [schizophrenia](@entry_id:164474), for instance, a common finding is that functional [brain networks](@entry_id:912843) show reduced clustering ($C$) and increased path length ($L$) compared to healthy controls. This results in a lower small-worldness index $\sigma$, indicating a shift away from an optimal small-world organization towards a more random, less efficient topology. This disruption of the balance between segregation and integration provides a macroscopic signature of the widespread synaptic and circuit-level dysfunctions that may underlie the disorder .

By integrating insights across these multiple scales—from ion channels and [synaptic plasticity](@entry_id:137631), to [decision-making circuits](@entry_id:897178) and Bayesian inference, to whole-brain network topology—[computational psychiatry](@entry_id:187590) provides a rich and rigorous framework for understanding the mechanisms of the mind in health and disease.