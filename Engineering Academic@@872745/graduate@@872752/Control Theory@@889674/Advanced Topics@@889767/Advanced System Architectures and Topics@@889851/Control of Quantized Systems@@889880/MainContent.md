## Introduction
In the landscape of modern engineering, from [networked control systems](@entry_id:271631) to embedded devices, the interface between continuous physical processes and digital computation is universal. This translation is mediated by quantization, the process of mapping continuous signals to a [finite set](@entry_id:152247) of discrete values. While essential for digital implementation, quantization introduces nonlinearity and information loss, fundamentally challenging the classical assumptions of linear control theory. This creates a critical knowledge gap: how can we rigorously analyze the stability and performance of systems when the feedback loop is corrupted by this inherent imperfection?

This article provides a comprehensive exploration of the control of quantized systems, structured to build both theoretical understanding and practical skill. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, dissecting the properties of different quantizers, presenting powerful modeling techniques, and introducing fundamental stability analysis frameworks and information-theoretic limits. The second chapter, "Applications and Interdisciplinary Connections," bridges theory and practice by demonstrating how these concepts are applied in crucial domains like Networked Control Systems, digital signal processing, and advanced control methodologies, revealing deep connections to fields such as information theory and computer science. Finally, the "Hands-On Practices" chapter offers a set of curated problems, allowing you to apply and solidify your understanding of these core principles.

## Principles and Mechanisms

The introduction of a quantizer into a control loop transforms a system, which may have been linear and continuous, into one that is fundamentally nonlinear and hybrid. The discrete nature of the quantizer's output presents a host of challenges for analysis and design. This chapter lays out the foundational principles of quantization in the context of [control systems](@entry_id:155291), explores the primary mechanisms for modeling and analysis, and introduces advanced techniques for mitigating the adverse effects of information constraints.

### The Nature of Quantization: Static Mappings and Their Properties

A **quantizer** is a nonlinear mapping $Q$ that takes a continuous-valued signal and maps it to a value from a finite or countably infinite set of reproduction levels. This process is the primary source of error in a [digital control](@entry_id:275588) system. The nature of this error is critically dependent on the type of quantizer employed. We will focus on two canonical types: uniform and logarithmic.

#### Uniform Quantization

The most common type of quantizer is the **[uniform quantizer](@entry_id:192441)**. A symmetric **mid-tread** [uniform quantizer](@entry_id:192441) with step size $\Delta > 0$ is characterized by reproduction levels that are integer multiples of $\Delta$. Within a non-overload region, typically defined as $[-X_{\max}, X_{\max}]$, this mapping can be expressed as:
$Q_{\mathrm{u}}(x) = \Delta \cdot \mathrm{round}(\frac{x}{\Delta})$
where the `round` function maps a real number to the nearest integer. Outside this region, the quantizer **saturates**, mapping all inputs $x > X_{\max}$ to its largest output level and all $x  -X_{\max}$ to its smallest.

The primary characteristic of a [uniform quantizer](@entry_id:192441) is its **[absolute error](@entry_id:139354)** bound. The [quantization error](@entry_id:196306) is defined as $e(x) = x - Q_{\mathrm{u}}(x)$. For any input $x$ in the non-overload region, the magnitude of the error is bounded by half the step size:
$|e(x)| = |x - Q_{\mathrm{u}}(x)| \le \frac{\Delta}{2}$
This constant absolute error bound is the main advantage of [uniform quantization](@entry_id:276054); it treats all signal amplitudes within its range equally.

However, this strength becomes a weakness when considering **relative error**, defined as $|e(x)|/|x|$ for $x \neq 0$. The bound on relative error is given by:
$\frac{|e(x)|}{|x|} \le \frac{\Delta}{2|x|}$
This bound is inversely proportional to the signal's magnitude, $|x|$. Consequently, for small signals (as $|x| \to 0$), the [relative error](@entry_id:147538) can become arbitrarily large. This implies that uniform quantizers have poor fidelity for signals with a wide dynamic range, as they cannot simultaneously provide high precision for both large and small amplitudes with a single fixed step size $\Delta$ [@problem_id:2696305]. To achieve a specific worst-case [relative error](@entry_id:147538) bound $\gamma$ at a target magnitude $|x^\star|$, the step size must be chosen as $\Delta = 2\gamma|x^\star|$, highlighting the impossibility of maintaining a constant relative error bound over a range of magnitudes with a fixed $\Delta$ [@problem_id:2696305].

#### Logarithmic Quantization

To address the shortcomings of [uniform quantization](@entry_id:276054) for wide-dynamic-range signals, the **logarithmic quantizer** provides a constant bound on relative error. A logarithmic quantizer partitions the signal space geometrically rather than arithmetically. For positive signals, the decision thresholds are defined by a [geometric progression](@entry_id:270470) $t_k = X_{\min} r^{k}$ for $k=0, 1, \dots, K$, where $r > 1$ is the density ratio, $X_{\min}$ is the smallest quantizable magnitude, and $t_K = X_{\max}$ is the saturation level. A symmetric quantizer is constructed for negative signals.

The key property of a logarithmic quantizer is that by choosing the reproduction levels appropriately, the worst-case relative error can be made constant across all quantization bins. For an input $x$ in a bin $[t_k, t_{k+1})$, the optimal choice of reproduction level $m_k$ that minimizes the maximum relative error is not the geometric or arithmetic mean of the thresholds. Instead, the optimal level is given by [@problem_id:2696305]:
$m_k = \frac{2r}{r+1} t_k$
With this choice, the [relative error](@entry_id:147538) $e_r(x) = (x - m_k)/x$ is bounded. At the lower endpoint of the bin, $x=t_k$, the error is $e_r(t_k) = 1 - \frac{2r}{r+1} = -\frac{r-1}{r+1}$. At the upper endpoint, $x=t_{k+1}=rt_k$, the error is $e_r(t_{k+1}) = 1 - \frac{m_k}{rt_k} = 1 - \frac{2}{r+1} = \frac{r-1}{r+1}$.
Thus, for any input $|x| \in [X_{\min}, X_{\max}]$, the [relative error](@entry_id:147538) is uniformly bounded by:
$\frac{|x - Q_{\log}(x)|}{|x|} \le \gamma, \quad \text{where} \quad \gamma = \frac{r-1}{r+1}$
This constant relative error bound makes logarithmic quantizers ideal for applications where percentage accuracy is critical over many orders of magnitude. The trade-off is that the [absolute error](@entry_id:139354), $|x - Q_{\log}(x)| \le \gamma |x|$, is no longer constant but grows in proportion to the signal magnitude. The maximum [absolute error](@entry_id:139354) in the bin $[t_k, t_{k+1})$ is approximately $\gamma t_{k+1}$, demonstrating that larger signals are quantized with less absolute precision [@problem_id:2696305].

### Modeling Quantizers for System Analysis

The discontinuous and nonlinear nature of quantizers complicates the analysis of feedback systems. To make analysis tractable, we often replace the exact quantizer mapping with a simpler, more analytically convenient model. The choice of model depends on the specific properties of the system and the analysis tools to be used.

#### The High-Resolution Additive Noise Model

A widely used heuristic, particularly in signal processing and [stochastic control](@entry_id:170804), is to model the quantizer as an [additive noise](@entry_id:194447) source. That is, the output of the quantizer is written as $q(x) = x + e_q$, where the quantization error $e_q$ is treated as a random noise signal. For this model to be useful, the "noise" $e_q$ is typically assumed to be:
1.  Uniformly distributed over its range (e.g., $[-\Delta/2, \Delta/2]$ for a [uniform quantizer](@entry_id:192441)).
2.  Independent of the input signal $x$.
3.  White, meaning uncorrelated in time.

These assumptions, known as the **high-resolution [additive noise model](@entry_id:197111)**, are justified under specific conditions formalized by Widrow's quantization theorem [@problem_id:2696243]. For a quantizer without saturation, the error's probability density function $p_e(\epsilon)$ is given by the sum $\sum_i p_x(i\Delta - \epsilon)$, where $p_x$ is the input signal's PDF. For $p_e(\epsilon)$ to be approximately constant (i.e., uniform), the input PDF $p_x(y)$ must be nearly constant over any interval of width $\Delta$. This is the essence of the **high-resolution assumption**: the quantization step $\Delta$ must be small compared to the scale over which the input signal's amplitude distribution changes. Similarly, for the error to be uncorrelated with the input and white over time, the input signal must be sufficiently "random" or "busy," such that its position within a quantization bin is effectively randomized from one sample to the next.

When these conditions are not met (e.g., for coarse quantization or slowly varying signals), the model is invalid. However, its properties can be enforced through the use of **[dither](@entry_id:262829)**, an external random signal added to the input before quantization. With **subtractive [dither](@entry_id:262829)**, a [dither signal](@entry_id:177752) $d[k]$, typically from a [uniform distribution](@entry_id:261734) $\mathcal{U}(-\Delta/2, \Delta/2)$, is added to the input $x[k]$ before quantization and then subtracted from the output. The effective error $e_{eff}[k] = Q(x[k]+d[k]) - (x[k]+d[k])$ can be shown to be statistically independent of the input $x[k]$, white, and uniformly distributed on $[-\Delta/2, \Delta/2]$, making the [additive noise model](@entry_id:197111) exact [@problem_id:2696243].

#### The Sector-Bounded Nonlinearity Model

An alternative and more rigorous approach, especially for deterministic stability analysis, is to model the quantizer as a static nonlinearity belonging to a specific **sector**. A function $\varphi(y)$ is said to lie in the sector $[\alpha, \beta]$ if the inequality $(\varphi(y)-\alpha y)(\beta y-\varphi(y)) \ge 0$ holds for all $y$. This is equivalent to stating that the graph of $\varphi(y)$ lies between the lines $y' = \alpha y$ and $y' = \beta y$.

For instance, a uniform mid-tread quantizer without saturation satisfies $q(y) \approx y$ for large $y$ and has $q(0)=0$. The graph of $q(y)$ versus $y$ is a [staircase function](@entry_id:183518) that always remains in the first and third quadrants, and its local slope (where defined) is either 0 or infinite. It is straightforward to show that for any $y$, $q(y)y \ge 0$. Furthermore, for a quantizer with step $\Delta$, one can establish a bound of the form $q(y)y \le k y^2$ for some $k \ge 1$. This means the quantizer lies within the sector $[0, k]$ [@problem_id:2696252]. Additionally, the non-decreasing nature of the quantizer implies it has an **incremental sector** bound (or slope restriction) in $[0, \infty)$. For many standard quantizers, this can be tightened to an incremental sector $[0, 1]$ if we neglect the points of discontinuity [@problem_id:2696270]. This [sector-bound model](@entry_id:176619) allows the powerful tools of [absolute stability](@entry_id:165194) theory, such as the Circle Criterion and LMI-based methods, to be applied.

#### The Bounded Disturbance Model

In many modern control frameworks, particularly those based on Lyapunov methods, it is convenient to model the quantization effect as a bounded disturbance. The control law is designed for a continuous input $u_c(t)$, but the implemented control is the quantized version $u_q(t) = Q(u_c(t))$. We can write the quantized input as the intended input plus an error term: $u_q(t) = u_c(t) + e_q(t)$, where $e_q(t) = Q(u_c(t)) - u_c(t)$.

For a [uniform quantizer](@entry_id:192441) with step size $\Delta$, this error is bounded: $\|e_q\|_{\infty} \le \Delta/2$. For a logarithmic quantizer, the error is bounded relative to the input, $|e_q(t)| \le \eta |u_c(t)|$. If the intended control signal $u_c(t)$ is itself bounded, then the quantization error $e_q(t)$ is also guaranteed to be bounded. The system dynamics can then be written as a nominal system driven by the continuous control $u_c(t)$, perturbed by an additive, bounded, state-dependent disturbance term. This model is the foundation for the Input-to-State Stability framework [@problem_id:2696269].

### Stability Analysis of Quantized Feedback Systems

Armed with these models, we can now analyze the stability of [feedback systems](@entry_id:268816) containing quantizers.

#### Absolute Stability via Sector Bounds

By modeling the quantizer as a sector-bounded nonlinearity, we cast the [quantized control](@entry_id:168852) problem into the canonical **Lur'e problem** framework. This framework concerns the [feedback interconnection](@entry_id:270694) of a linear time-invariant (LTI) system $G(s)$ and a memoryless nonlinearity $\varphi(\cdot)$ belonging to a known sector $[\alpha, \beta]$. **Absolute stability** refers to the property that the closed-loop system is globally asymptotically stable for *any* nonlinearity within the specified sector.

A cornerstone result is the **Circle Criterion**, which provides a graphical frequency-domain test for [absolute stability](@entry_id:165194). For a stable plant $G(s)$ in [negative feedback](@entry_id:138619) with a nonlinearity in the sector $[\alpha, \beta]$, the system is absolutely stable if the Nyquist plot of $G(j\omega)$ does not enter or encircle the critical disk in the complex plane defined by the diameter with endpoints $-1/\alpha$ and $-1/\beta$. For the important sector $[0, 1]$ (which can model a quantizer with slope restriction), the [critical region](@entry_id:172793) is the half-plane $\text{Re}\{z\} \le -1$. Stability is guaranteed if $\text{Re}\{G(j\omega)\} > -1$ for all $\omega$ [@problem_id:2696270].

While the Circle Criterion is intuitive, passivity-based approaches and the **Kalman-Yakubovich-Popov (KYP) Lemma** yield more computationally tractable conditions in the form of **Linear Matrix Inequalities (LMIs)**. To certify stability for a plant $G(s)$ with [state-space realization](@entry_id:166670) $(A,B,C,D)$ in negative feedback with a quantizer in the sector $[0, k]$, one can test for the Strict Positive Realness (SPR) of the transformed transfer function $H(s) = 1+kG(s)$. The KYP lemma states that $H(s)$ is SPR if and only if there exists a [symmetric positive definite matrix](@entry_id:142181) $P$ ($P=P^{\top} \succ 0$) satisfying the LMI [@problem_id:2696252]:
$$
\begin{pmatrix}
A^{\top}P+PA   PB-kC^{\top} \\
B^{\top}P-kC   -2(1+kD)
\end{pmatrix} \prec 0
$$
This LMI is linear in the variables $P$ and $k$. For a given plant, one can use this condition to solve for the largest sector bound $k$ for which stability can be guaranteed. For example, for the plant $G(s) = \frac{s-1}{s+1}$ with realization $A=-1, B=1, C=-2, D=1$, this LMI can be solved to find that [absolute stability](@entry_id:165194) is guaranteed for any quantizer in the sector $[0, k)$ as long as $k  1$. The largest such sector bound is therefore $k=1$ [@problem_id:2696252].

#### The Input-to-State Stability Framework

A more modern and nuanced approach to stability in the presence of disturbances is the framework of **Input-to-State Stability (ISS)**. Consider a [nonlinear system](@entry_id:162704) $\dot{x} = F(x, w)$ with state $x$ and external input $w$. The system is ISS if its state is bounded by a function of the initial state that decays to zero, plus a term proportional to the magnitude of the input:
$\|x(t)\| \le \beta(\|x(0)\|, t) + \gamma(\|w\|_{\infty})$
Here, $\beta$ is a class $\mathcal{KL}$ function (describing transient decay) and $\gamma$ is a class $\mathcal{K}$ function (describing the asymptotic gain from the input).

When analyzing a quantized system, we use the bounded disturbance model. A continuous feedback law $u_c(t)=k(x(t))$ is designed to make the nominal system $\dot{x} = f(x) + g(x)k(x)$ asymptotically stable. The full dynamics are then $\dot{x} = (f(x) + g(x)k(x)) + g(x)e_q(t)$, where the [quantization error](@entry_id:196306) $e_q$ is the external input.

However, standard ISS is often too strong a property for quantized systems. Due to the quantizer's "dead-zone" around the origin, a small control signal $u_c(t)$ might be quantized to zero, i.e., $u_q(t)=0$. If the open-loop dynamics $\dot{x}=f(x)$ are not stable, the state may not converge to the origin but to a small [residual set](@entry_id:153458) around it. This behavior is captured by the notion of **Input-to-State Practical Stability (ISpS)**. A system is ISpS if its state satisfies [@problem_id:2696269]:
$$
\|x(t)\| \le \beta(\|x(0)\|, t) + \gamma(\|e_q\|_{\infty}) + b
$$
The additional constant $b \ge 0$ accounts for the size of the ultimate bound or [residual set](@entry_id:153458), even in the absence of a persistent input. This framework provides a rigorous way to characterize that the state will converge not necessarily to zero, but to a small neighborhood whose size depends on the quantization parameters (which determine $\|e_q\|_{\infty}$) and the system properties (which determine $b$).

### Information-Theoretic Limitations: The Data-Rate Theorem

Beyond stability analysis for a given scheme, a fundamental question is: what is the minimum amount of information required to control a system at all? The **[data-rate theorem](@entry_id:165781)** provides a profound answer for stabilizing an unstable LTI system over a noiseless digital channel with a limited data rate.

Consider the discrete-time LTI plant $x_{k+1} = A x_k + B u_k$. If the matrix $A$ has unstable eigenvalues (magnitude greater than 1), the state will grow exponentially without control. The role of the controller, which receives information about the state via a channel with an average rate of $R$ bits per sample, is to counteract this growth.

An intuitive way to understand the limitation is to consider the volume of an [uncertainty set](@entry_id:634564) in the state space. The dynamics of the system, when restricted to the unstable subspace, expand the volume of any set of [initial conditions](@entry_id:152863) by a factor equal to the product of the magnitudes of the unstable eigenvalues, $\prod_{|\lambda_i(A)| > 1} |\lambda_i(A)|$, at each time step. To counteract this "uncertainty expansion," the controller must receive enough information to re-localize the state within a smaller region. A channel with rate $R$ can transmit one of $2^R$ distinct messages on average, allowing the expanded uncertainty volume to be partitioned into $2^R$ sub-regions. For stability, the new uncertainty volume must be no larger than the original one. This leads to the inequality:
$2^R \ge \prod_{|\lambda_i(A)| > 1} |\lambda_i(A)|$

Taking the base-2 logarithm of both sides yields the celebrated [data-rate theorem](@entry_id:165781): the minimum average data rate $R_{min}$ required for stabilization is [@problem_id:2696293]:
$$
R_{min} = \sum_{|\lambda_i(A)| > 1} \log_2(|\lambda_i(A)|) \quad (\text{bits/sample})
$$
This remarkable result shows that the minimum information rate is determined solely by the unstable part of the plant dynamics. For instance, a plant with eigenvalues $\{2, 0.5, -3\}$ has two [unstable modes](@entry_id:263056) with magnitudes 2 and 3. The minimum data rate for stabilization is $\log_2(2) + \log_2(3) = 1 + \log_2(3) \approx 2.585$ bits/sample [@problem_id:2696293]. This is a fundamental limit that no control or quantization scheme can overcome.

### Advanced Mechanisms and Challenges

Building upon the fundamental principles, several advanced mechanisms have been developed to enhance the performance of [quantized control](@entry_id:168852) systems and address inherent challenges.

#### Dynamic Quantization and Zooming

Static quantizers force a fixed trade-off between dynamic range and resolution. A large range implies a large step size $\Delta$ (for uniform quantizers) or a large [relative error](@entry_id:147538) $\gamma$ (for logarithmic quantizers), leading to poor precision. A small step size provides high precision but is prone to saturation. **Dynamic quantization** overcomes this limitation by allowing the quantizer's parameters to be adjusted in real-time.

A dynamic quantizer is defined by a time-varying [scale parameter](@entry_id:268705) $s_k > 0$, with the mapping given by $q_{s_k}(x) = s_k \cdot q(x/s_k)$, where $q(\cdot)$ is a static base quantizer [@problem_id:2696240]. Scaling the input by $1/s_k$ and the output by $s_k$ effectively scales the quantizer's step size and saturation limits by $s_k$. This enables a **zooming** strategy:
-   **Zooming-out:** When the state is large or its location is unknown, $s_k$ is increased to expand the quantizer's range and avoid saturation.
-   **Zooming-in:** Once the state is known to be within a certain bound and is converging towards the origin, $s_k$ is decreased to shrink the quantizer's step size, thereby increasing its resolution and allowing for finer control.

For a system designed to be stable (e.g., a deadbeat controller), a simple update rule like $s_{k+1} = \rho s_k$ with $\rho \in (0,1)$ can guarantee stability. Under certain conditions relating the [system gain](@entry_id:171911), the base quantizer's parameters, and the contraction factor $\rho$, one can prove that if the state starts within the non-saturating region of the scaled quantizer, it will remain there for all future times, and both the state $x_k$ and the scale parameter $s_k$ will converge geometrically to zero [@problem_id:2696240].

#### Hysteretic Quantizers for Chattering Reduction

When a signal oscillates around a quantizer's decision threshold, the output can switch rapidly back and forth, a phenomenon known as **chattering**. This is undesirable as it can excite high-frequency dynamics and cause wear on actuators. Hysteresis is a common mechanism to prevent this.

A **hysteretic quantizer** introduces memory into the quantization process. Instead of a single decision threshold $t_k$, each nominal threshold is replaced by a pair of switching thresholds, $t_k-h$ and $t_k+h$, where $h>0$ is the [hysteresis](@entry_id:268538) half-width. A transition from a lower output level to a higher one occurs only when the input exceeds the upper threshold $t_k+h$. Conversely, a transition from a higher level to a lower one occurs only when the input drops below the lower threshold $t_{k-1}-h$. In the "[hysteresis](@entry_id:268538) band" between these switching points, the output remains constant.

This path-dependent behavior is naturally modeled as a **deterministic [finite-state machine](@entry_id:174162)**, specifically a Moore machine where the output is a function of the state alone [@problem_id:2696255]. The state $s \in \mathbb{Z}$ corresponds to the index of the current output level, $q_s$. The state transitions are governed by the input $x$ and the switching thresholds. A transition from state $s$ to $s+1$ happens if $x \ge t_s+h$, and from $s$ to $s-1$ if $x \le t_{s-1}-h$. Otherwise, the state remains $s$. This structure explicitly captures the memory of the quantizer and provides a formal model for analysis and simulation.

#### State Estimation with Quantized Outputs and the Failure of Separation

When designing an [observer-based controller](@entry_id:188214), a critical challenge arises if the measurements are quantized. Consider a system where the available measurement is $y_k = q(C x_k + v_k)$, where $v_k$ is [measurement noise](@entry_id:275238). The optimal [state estimator](@entry_id:272846) in this setting is a recursive **Bayesian filter** that propagates the probability density function (PDF) of the state given the measurements.

The update step of this filter, which incorporates the new measurement $y_k$, involves multiplying the prior PDF by a [likelihood function](@entry_id:141927). This likelihood, $\mathbb{P}(y_k | x_k)$, is the probability of observing the quantized value $y_k$ given the state $x_k$. For instance, if $y_k=i$ corresponds to the measurement falling in an interval $(\alpha_{i-1}, \alpha_i]$, the likelihood is $\mathbb{P}(\alpha_{i-1}  Cx_k+v_k \le \alpha_i)$. Even if the noise $v_k$ and the prior state distribution are Gaussian, this [likelihood function](@entry_id:141927) is non-Gaussian (it is a "slab" of a Gaussian PDF). As a result, the posterior PDF of the state is also non-Gaussian [@problem_id:2696288]. This means the celebrated **Kalman filter**, which is optimal only for linear-Gaussian systems, is no longer optimal.

This non-Gaussian nature of the [belief state](@entry_id:195111) leads to a more profound consequence: the **failure of the separation principle**. In classical LQG control, the [optimal control](@entry_id:138479) problem separates into an [optimal estimation](@entry_id:165466) problem (the Kalman filter) and a deterministic control problem (the LQR). This works because the [estimation error](@entry_id:263890) covariance is independent of the control inputs. With quantized measurements, this is no longer true. The control input $u_k$ influences the future state $x_{k+1}$, which in turn affects the probability distribution of the next measurement $y_{k+1}$. An aggressive control action might steer the state well but push it into a region where the quantizer is less informative, thus degrading future state estimates. This coupling between control and estimation, often called the **dual effect**, means the problems cannot be solved separately. The [optimal control](@entry_id:138479) law depends on the full [belief state](@entry_id:195111) (the entire PDF), not just its mean, making the problem significantly more complex [@problem_id:2696288].

#### Event-Triggered Control and Zeno Behavior

**Event-triggered control (ETC)** is a strategy to reduce communication and computation by updating the control signal only when "needed." A common triggering rule is to transmit a new measurement when the error between the current plant output $y(t)$ and the last transmitted value held at the controller, $\hat{y}(t)$, exceeds a threshold, for instance, a relative threshold: $\|y(t) - \hat{y}(t)\| \ge \sigma \|y(t)\|$.

A critical issue in ETC is **Zeno behavior**: the occurrence of an infinite number of events in a finite time interval, which is physically impossible to implement. It is crucial to design triggering mechanisms that preclude this phenomenon. Several strategies exist:
-   **Forced Dwell Time:** The simplest method is to enforce a minimum time $\tau_d > 0$ between any two events. This trivially rules out Zeno behavior by design [@problem_id:2696242].
-   **Hysteresis:** A hysteretic trigger can be used, where an event is triggered when the error exceeds an upper threshold $\sigma_{\uparrow}$, and further triggers are inhibited until the error drops below a lower threshold $\sigma_{\downarrow}$. This ensures the error must evolve over a non-zero range, which takes a non-zero amount of time.
-   **System-Based Analysis:** One can prove the absence of Zeno by showing that the time between events has a strictly positive lower bound. This often involves analyzing the growth rate of the [error signal](@entry_id:271594) between events. When combined with a logarithmic quantizer, whose initial error after an update is bounded *relatively* ($\|y - Q(y)\| \le \eta\|y\|$), a [relative error](@entry_id:147538) trigger naturally avoids Zeno. The error ratio starts at a value less than $\eta$ and must grow to $\sigma > \eta$, which takes a minimum amount of time that depends on the system's dynamics. In contrast, a [uniform quantizer](@entry_id:192441) with its [absolute error](@entry_id:139354) bound does not provide such a guarantee when used with a relative error trigger, as the initial error ratio can be arbitrarily large if $\|y\|$ is small [@problem_id:2696242].