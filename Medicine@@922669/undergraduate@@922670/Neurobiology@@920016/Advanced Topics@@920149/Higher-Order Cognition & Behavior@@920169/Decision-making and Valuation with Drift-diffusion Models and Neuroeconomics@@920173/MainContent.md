## Introduction
How does the brain weigh evidence over time to arrive at a choice? This fundamental question lies at the intersection of psychology, neuroscience, and economics. While we often experience decisions as instantaneous, they are the result of complex neural computations that gradually unfold. To bridge the gap between observable behaviors—such as the choices we make and how long it takes to make them—and the hidden workings of the brain, researchers rely on computational frameworks. Among the most powerful of these is the Drift-Diffusion Model (DDM), a mathematical model that conceptualizes decisions as a process of evidence accumulation.

This article provides a comprehensive exploration of the DDM and its profound implications for understanding valuation and choice from a neuroeconomic perspective. The first chapter, **Principles and Mechanisms**, will lay out the mathematical foundations of the model, explaining how its core parameters govern behavior and how it relates to optimal decision strategies and plausible biophysical mechanisms. Next, **Applications and Interdisciplinary Connections** will demonstrate the model's power in practice, showing how it integrates with reinforcement learning theories, explains the effects of [neuromodulation](@entry_id:148110), and offers novel insights into clinical disorders. Finally, **Hands-On Practices** will allow you to engage directly with the concepts through computational problems, solidifying your understanding of how to use the DDM as a tool for research.

## Principles and Mechanisms

### The Drift-Diffusion Model: A Formalism for Evidence Accumulation

At the heart of many models of decision-making lies the concept of evidence accumulation. When faced with a choice between two alternatives, the brain is thought to gather sensory or value-based information over time until a critical amount of evidence favoring one option has been accrued, at which point a decision is made and a motor response is initiated. The **Drift-Diffusion Model (DDM)** provides a mathematically precise and remarkably successful framework for describing this process.

The DDM conceptualizes the decision process as a single scalar **decision variable**, $X_t$, which represents the net evidence accumulated up to time $t$. This variable evolves according to a [stochastic differential equation](@entry_id:140379), describing a Wiener process with drift:

$$
dX_t = v\,dt + \sigma\,dW_t
$$

Here, the evolution of the decision variable is governed by two key components. The first, $v\,dt$, is a deterministic term representing the average rate of evidence accumulation, known as the **drift rate** ($v$). The drift rate reflects the quality or strength of the evidence; a stronger, clearer stimulus or a larger difference in subjective value between options corresponds to a higher magnitude of $v$. The second term, $\sigma\,dW_t$, is a stochastic component, where $dW_t$ represents an increment of a standard Wiener process (a model of Brownian motion) and $\sigma$ is the **diffusion coefficient** or noise standard deviation. This term captures the inherent variability and noise present in neural processing.

The accumulation process does not continue indefinitely. The model posits the existence of two **decision boundaries**. In a common formulation with symmetric boundaries, these are placed at $+A$ and $-A$. The process starts at an initial **starting point**, $z$, which is typically set to $z=0$ for an unbiased decision. The decision variable $X_t$ drifts and diffuses over time until it is absorbed by one of these boundaries. If it first hits the upper boundary $+A$, one choice is made; if it first hits the lower boundary $-A$, the alternative choice is made. The time taken to reach a boundary is the **decision time**, and the boundary that is reached determines the choice itself. The magnitude of the boundary separation, $2A$, represents the level of caution or the amount of evidence the decision-maker requires before committing to a choice.

### From Model Parameters to Behavior: Choice and Reaction Time

The power of the DDM lies in its ability to simultaneously account for two fundamental aspects of decision-making behavior: the choices made and the time taken to make them (reaction times). The model's parameters—drift rate $v$, boundary separation $A$, and starting point $z$—jointly determine the full distribution of choices and reaction times.

#### Choice Probability and the Speed-Accuracy Tradeoff

The probability of choosing one option over another is determined by the probability that the [diffusion process](@entry_id:268015) reaches one boundary before the other. For a process starting at $x(0) = x$ with boundaries at $\pm A$, the probability of hitting the upper boundary, $P(x)$, can be found by solving the Kolmogorov backward equation, which for this process is:

$$
\frac{1}{2}\sigma^2 \frac{d^2P}{dx^2} + v \frac{dP}{dx} = 0
$$

This second-order [ordinary differential equation](@entry_id:168621) is solved with the boundary conditions $P(A) = 1$ (starting at the boundary means hitting it with probability 1) and $P(-A) = 0$. For an unbiased start at $x=0$, the solution yields a simple and elegant expression for the probability of making a correct choice (assuming $v>0$ directs the process toward the correct boundary $+A$):

$$
P(\text{correct}) = P(0) = \frac{1}{1 + \exp\left(-\frac{2vA}{\sigma^2}\right)}
$$

This equation, a [logistic function](@entry_id:634233) of the term $\frac{2vA}{\sigma^2}$, elegantly captures one of the most robust findings in decision psychology: the **speed-accuracy tradeoff**. To increase accuracy, a subject must adopt a more cautious strategy, which in the DDM framework corresponds to increasing the boundary separation $A$. As is clear from the formula, a larger $A$ increases $P(\text{correct})$. However, wider boundaries mean that the diffusion process will, on average, take longer to terminate, leading to slower responses. Conversely, emphasizing speed encourages a subject to lower their decision boundaries, resulting in faster but more error-prone choices. This principle allows us to predict the level of caution required to achieve a specific performance goal. For instance, if a decision-maker aims for a target accuracy of $p^{\star} = 0.82$ with an evidence quality yielding $v = 0.75$ and noise $\sigma = 1.10$, we can rearrange the formula to solve for the necessary boundary height $A$:

$$
A = \frac{\sigma^2}{2v} \ln\left(\frac{p^{\star}}{1 - p^{\star}}\right) = \frac{1.10^2}{2 \times 0.75} \ln\left(\frac{0.82}{0.18}\right) \approx 1.223 \text{ evidence units}
$$

This calculation demonstrates how the abstract parameter of boundary separation can be directly and quantitatively linked to an observable behavioral policy. [@problem_id:5011105]

#### Reaction Time Decomposition

The time predicted by the DDM, from the start of the accumulation process to boundary crossing, is the **decision time ($T_D$)**. However, the observed reaction time ($RT$) measured in an experiment includes additional latencies. These are captured by a **non-decision time ($T_{nd}$)**, which lumps together all perceptual and motor delays that are not part of the deliberative decision process itself. Thus, the full model for reaction time is:

$$
RT = T_D + T_{nd}
$$

The non-decision time can be further decomposed into components such as **sensory encoding time ($T_{enc}$)** and **motor execution time ($T_{mot}$)**. A powerful experimental technique, known as the **method of additive factors**, allows for the empirical isolation of these components. The logic assumes that certain experimental manipulations will selectively influence one component of processing without affecting others. [@problem_id:5011112]

For example, consider a task where participants make either a manual (button-press) or saccadic (eye-movement) response. Switching the response modality is hypothesized to selectively change the motor execution time $T_{mot}$ but leave sensory and decision processes untouched. Similarly, degrading the stimulus (e.g., using a backward mask) might selectively prolong the sensory encoding time $T_{enc}$. If the effects of these manipulations on mean reaction time are additive, it provides strong support for the model's architecture. If a stimulus mask adds a delay of $\Delta T_{enc}$ and switching to a saccade changes motor time by $\Delta T_{mot}$, the total change in RT for both manipulations combined should be $\Delta T_{enc} + \Delta T_{mot}$. In a hypothetical experiment where a backward mask was found to increase manual reaction times from $0.517$ s to $0.5653$ s and saccadic reaction times from $0.4661$ s to $0.5144$ s, the inferred sensory encoding delay is identical in both cases ($0.5653 - 0.517 = 0.0483$ s and $0.5144 - 0.4661 = 0.0483$ s), perfectly illustrating this [principle of additivity](@entry_id:189700). [@problem_id:5011112]

### The Role of the Starting Point in Modeling Bias

The DDM's starting point, $z$, provides a natural mechanism for incorporating bias into the decision process. An unbiased decision-maker starts accumulation from the midpoint of the boundaries ($z=0$ for boundaries $\pm A$). Any deviation from this midpoint reflects a pre-existing bias toward one of the choices, as the process begins closer to one boundary and is therefore more likely to terminate there, all else being equal.

#### Priors and Starting Point Bias

In a Bayesian framework, prior knowledge should rationally influence decisions. If one option is a priori more likely than another, a decision-maker should require less evidence to choose it. The DDM can implement this normative principle by setting the starting point according to the prior [log-odds](@entry_id:141427) of the alternatives. If the decision variable represents the **[log-likelihood ratio](@entry_id:274622) (LLR)** of the evidence, and the prior probabilities for options $\mathcal{A}$ and $\mathcal{B}$ are $\pi_{\mathcal{A}}$ and $\pi_{\mathcal{B}}$, the optimal starting point is $Y_0 = \ln(\pi_{\mathcal{A}}/\pi_{\mathcal{B}})$. [@problem_id:5011103]

The general formula for choice probability, starting from an arbitrary point $y$ between boundaries $-B$ and $+B$, can be derived from the same Kolmogorov equation used before, but with the more general initial condition. The resulting probability of hitting the upper boundary is:

$$
P(\text{choose } \mathcal{A}) = \frac{1 - \exp\left(-\frac{2v(y+B)}{\sigma^2}\right)}{1 - \exp\left(-\frac{4vB}{\sigma^2}\right)}
$$

This formula shows how the starting point $y$ and the drift $v$ interact to determine the final choice probability. A positive starting point (bias towards $\mathcal{A}$) and a positive drift (evidence for $\mathcal{A}$) both increase the probability of choosing $\mathcal{A}$.

#### Sequential Dependencies and History Bias

Biases can also arise from the recent history of choices and outcomes, a phenomenon known as **sequential dependency**. For example, subjects often show a tendency to repeat a previous choice (a "stay" bias) or to alternate between choices (a "switch" bias). Such history biases can be modeled as a trial-by-trial shift in the starting point. For instance, the starting point $z$ on trial $n$ can be made dependent on the previous choice $c_{n-1} \in \{+1, -1\}$:

$$
z_n = \frac{a}{2} + b\,c_{n-1}
$$

In this formulation (for boundaries at $0$ and $a$), the starting point is shifted from the midpoint $a/2$ by an amount $b$. A positive bias parameter $b$ pushes the starting point toward the boundary corresponding to the previous choice, increasing the probability of a repeat. A negative $b$ pushes it away, increasing the probability of a switch. This simple mechanism allows the DDM to capture complex, dynamic patterns in choice sequences that go beyond the evidence presented on the current trial. [@problem_id:5011115]

### Normative Foundations: The DDM as an Optimal Decision Procedure

A key reason for the DDM's prominence is that it is not merely a descriptive model that happens to fit data well; it has deep normative roots. The DDM can be shown to be a continuous-time implementation of the **Sequential Probability Ratio Test (SPRT)**, which is the optimal statistical procedure for making a decision between two hypotheses. "Optimal" here means that for a given level of accuracy (i.e., a fixed error rate), the SPRT minimizes the average number of samples—and thus the time—required to make a decision.

In the context of the SPRT, the decision variable is the **[log-likelihood ratio](@entry_id:274622) (LLR)** of the evidence collected so far. For a DDM where the momentary evidence under two hypotheses ($\mathcal{H}_{+}$ and $\mathcal{H}_{-}$) is Gaussian with mean $\pm \kappa$ and variance $\sigma^2$, the accumulated LLR, $L_t$, is directly proportional to the accumulated evidence, $S_t$:

$$
L_t = \frac{2\kappa}{\sigma^2} S_t
$$

The SPRT operates by accumulating this LLR until it crosses one of two pre-defined thresholds. These thresholds are determined by the acceptable error rate, $\epsilon$. To achieve a symmetric error rate of $\epsilon$, the LLR boundaries must be set at $\pm B$, where $B = \ln((1-\epsilon)/\epsilon)$. This provides a normative prescription for setting the decision boundaries of the DDM to achieve a desired level of accuracy. [@problem_id:5011106]

Furthermore, this framework allows for the derivation of the expected decision time. For a process with drift $\kappa$ and symmetric evidence boundaries $\pm Z$ (corresponding to the LLR boundaries), the mean decision time $\langle T \rangle$ starting from an unbiased point $S_0=0$ is given by:

$$
\langle T \rangle = \frac{Z}{\kappa} \tanh\left(\frac{\kappa Z}{\sigma^2}\right)
$$

This expression formalizes the speed-accuracy tradeoff within a normative context, showing precisely how the decision time depends on the boundary height $Z$ (which sets accuracy) and the evidence quality $\kappa$. For example, for an error constraint of $\epsilon=0.1$ and evidence parameters $\kappa=0.2$ and $\sigma=1$, the expected decision time can be calculated to be approximately $21.97$ seconds. [@problem_id:5011106]

### Biophysical Mechanisms: Neural Implementation of Accumulation

While the DDM is an abstract model, a central goal of neuroeconomics is to understand how its computations might be implemented by [neural circuits](@entry_id:163225). A prevailing hypothesis is that evidence accumulation is carried out by recurrently connected populations of neurons in associative cortical areas, such as the lateral intraparietal area (LIP) or frontal eye fields (FEF).

A more biophysically detailed model of a single neuron or a population's mean firing rate is the **[leaky integrator](@entry_id:261862)**. Unlike the "perfect" integrator of the standard DDM, a [leaky integrator](@entry_id:261862) has a tendency to "forget" or let evidence decay over time. Its dynamics can be described by an equation analogous to that of a simple RC electrical circuit:

$$
C \frac{dx}{dt} = -g_{L} x + I + \xi(t)
$$

Here, $x(t)$ is the decision variable (e.g., membrane voltage or population firing rate), $C$ is capacitance, $I$ is the input current representing evidence, and $\xi(t)$ is noise. The crucial new term is $-g_L x$, the **leak current**, where $g_L$ is the leak conductance. This term causes the variable $x(t)$ to decay toward a resting potential (here, zero) with a time constant $\tau = C/g_L$. In the presence of a constant input $I$, the variable does not grow indefinitely but instead approaches a steady-state value $\mu = I/g_L$.

Under strong evidence where noise is negligible, the trajectory of the [leaky integrator](@entry_id:261862) starting from $x(0)=0$ is deterministic:

$$
x(t) = \mu (1 - \exp(-\kappa t))
$$

where $\kappa = 1/\tau$ is the inverse time constant. A decision is made when $x(t)$ crosses a threshold $\theta$. The time $T$ to reach this threshold can be found by solving for $T$ in $\theta = x(T)$:

$$
T = -\frac{1}{\kappa} \ln\left(1 - \frac{\theta}{\mu}\right)
$$

This model makes distinct predictions from the perfect DDM. For instance, a decision is only possible if the steady-state value is greater than the threshold ($\mu > \theta$). This leaky integration mechanism is considered more biologically plausible, as it can be implemented by simple recurrent circuits and prevents the runaway excitation that would occur in a perfect integrator. The standard DDM can be viewed as a special case or a useful approximation of this leaky process, particularly when decisions are fast relative to the integrator's time constant. [@problem_id:5011116]