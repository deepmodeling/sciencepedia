## Introduction
In the design of any control system, achieving stability is merely the first step; the true measure of success lies in its performance. How quickly does a system respond to a command? Does it overshoot its target? How long does it take to settle? Answering these questions requires moving beyond qualitative descriptions to a rigorous, quantitative framework. This is the role of time-domain specifications, which provide a universal language for characterizing and comparing the transient behavior of dynamic systems. This article bridges the gap between the abstract concept of 'good performance' and the concrete metrics used by engineers to design and validate systems.

First, in **Principles and Mechanisms**, we will establish the formal definitions for core specifications like [rise time](@entry_id:263755), [percent overshoot](@entry_id:261908), and [settling time](@entry_id:273984), and derive their analytical expressions for prototypical first and [second-order systems](@entry_id:276555). We will also explore advanced extensions to discrete-time and multi-input, multi-output (MIMO) systems. Next, **Applications and Interdisciplinary Connections** will demonstrate how these specifications are used in practice, translating performance requirements into system parameters and linking the time domain to frequency-domain design tools across fields like aerospace, robotics, and signal processing. Finally, the **Hands-On Practices** section will offer a series of problems to solidify your understanding and apply these analytical techniques to complex scenarios.

## Principles and Mechanisms

In the analysis and design of control systems, performance is paramount. While stability is a necessary prerequisite, it is the transient behavior of a system that often determines its suitability for a given application. To move beyond qualitative descriptions such as "fast" or "well-behaved," we must establish a set of quantitative metrics known as **time-domain specifications**. These specifications characterize a system's response to a standard input, most commonly a step function, providing a universal language for evaluating and comparing system performance. This chapter elucidates the fundamental principles behind these specifications, their formal definitions, their analytical derivation for prototypical systems, and their extension to more complex scenarios including discrete-time and multi-input, multi-output (MIMO) systems.

### Formal Definitions of Core Specifications

The seemingly simple task of defining performance metrics is fraught with subtleties. A robust definition must be unambiguous, applicable to a wide range of system behaviors—from monotonic to oscillatory responses—and possess properties like invariance to input scaling that ensure it measures an intrinsic characteristic of the system itself.

Let us consider a stable, causal, linear time-invariant (LTI) system whose output $y(t)$ in response to a step input converges to a finite, non-zero steady-state value $y_{\infty}$.

**Rise Time ($t_r$)**

The **[rise time](@entry_id:263755)** is a measure of the speed of the response. A common convention is the "10%–90% [rise time](@entry_id:263755)," but defining this for an oscillatory response that may cross these thresholds multiple times requires precision. To avoid ambiguity, the standard convention relies on **first-passage times**. For a given percentage level $p$, the [first-passage time](@entry_id:268196) $t_p$ is defined as the earliest time at which the response reaches or exceeds that level of its final value:
$$
t_p = \inf\{ t \ge 0 : y(t) \ge p \cdot y_{\infty} \}
$$
The 10%–90% [rise time](@entry_id:263755) is then defined as the difference $t_r = t_{0.9} - t_{0.1}$. This definition remains unambiguous for oscillatory responses and correctly reduces to the classical interval for monotonic responses. Alternative definitions, such as those based on the *last* time a level is crossed, can lead to nonsensical results like negative rise times for certain underdamped responses and are therefore not used [@problem_id:2754662]. Another common metric, particularly for [underdamped second-order systems](@entry_id:275912), is the time taken to first reach the final value, i.e., $t_{1.0}$.

**Peak Time ($t_p$)**

For responses that overshoot their final value, the **[peak time](@entry_id:262671)** is the time at which the first and largest peak occurs. Mathematically, it is the smallest time $t > 0$ at which the output's derivative is zero and its second derivative is negative:
$$
t_p = \min \{ t > 0 \mid \dot{y}(t) = 0 \text{ and } \ddot{y}(t)  0 \}
$$

**Percent Overshoot ($M_p$)**

The **[percent overshoot](@entry_id:261908)** quantifies the maximum amount by which the response exceeds its final value, expressed as a percentage of that final value. It is a critical measure of [relative stability](@entry_id:262615). A robust definition must handle both positive and negative final values and clearly distinguish overshoot from undershoot. The standard definition is:
$$
M_p = \frac{y_{\max} - y_{\infty}}{|y_{\infty}|}
$$
where $y_{\max} = \sup_{t \ge 0} y(t)$. If $y_{\max} \le y_{\infty}$, the overshoot is zero. The normalization by the absolute value, $|y_{\infty}|$, ensures the metric is a meaningful non-negative ratio regardless of the sign of the output. A separate metric, **percent undershoot** ($M_u$), can be defined as $M_u = (y_{\infty} - y_{\min}) / |y_{\infty}|$, where $y_{\min} = \inf_{t \ge 0} y(t)$, to capture excursions below the final value. It is crucial to recognize that these specifications are meaningful only for systems that reach a finite steady-state. For unstable or marginally stable systems, $y_{\infty}$ may not exist or may be infinite, and these specifications are consequently undefined [@problem_id:2754698].

**Settling Time ($t_s$)**

The **settling time** is the time required for the response to enter and remain within a specified tolerance band around its final value. This "enter-and-stay" condition is crucial. For a given relative tolerance $\delta$ (e.g., $0.02$ for a 2% band), the settling time is formally defined as:
$$
t_s = \inf\{ t \ge 0 : |y(\tau) - y_{\infty}| \le \delta |y_{\infty}| \text{ for all } \tau \ge t \}
$$
This definition, based on a **relative tolerance band**, has the desirable property of being invariant to the amplitude of the step input. If the input is scaled by a factor $\lambda$, both the error signal $e(t) = y(t) - y_{\infty}$ and the final value $y_{\infty}$ are scaled by $\lambda$, leaving the inequality $| \lambda e(\tau) | \le \delta |\lambda y_{\infty}|$ equivalent to the original. In contrast, an **absolute-band** [settling time](@entry_id:273984), defined by $|y(\tau) - y_{\infty}| \le \delta_{\text{abs}}$, is not invariant to input scaling and is therefore less useful as an intrinsic system metric [@problem_id:2754709].

### Analysis of Prototypical Continuous-Time Systems

With rigorous definitions in place, we can derive analytical expressions for these specifications for fundamental system models. This provides invaluable insight into the relationship between system parameters (poles and zeros) and transient performance.

#### First-Order Systems

Consider a stable first-order system with the transfer function $G(s) = \frac{k}{s+a}$, where $a > 0$. For a unit step input ($U(s) = 1/s$), the output in the Laplace domain is $Y(s) = \frac{k}{s(s+a)}$. A [partial fraction expansion](@entry_id:265121) yields $Y(s) = \frac{k}{a}(\frac{1}{s} - \frac{1}{s+a})$. The inverse Laplace transform gives the time response:
$$
y(t) = \frac{k}{a} (1 - \exp(-at)), \quad t \ge 0
$$
The final value is $y_{\infty} = k/a$. The system's response is a monotonic exponential approach to this value, characterized by the **time constant** $\tau = 1/a$.

Let's compute the rise time. The time $t_{\beta}$ to reach a fraction $\beta$ of the final value is found by solving $y(t_{\beta}) = \beta y_{\infty}$:
$$
\frac{k}{a} (1 - \exp(-at_{\beta})) = \beta \frac{k}{a} \implies \exp(-at_{\beta}) = 1-\beta \implies t_{\beta} = -\frac{\ln(1-\beta)}{a}
$$
The 10%–90% [rise time](@entry_id:263755) is then:
$$
t_{r}^{10-90} = t_{0.9} - t_{0.1} = -\frac{\ln(0.1)}{a} - \left(-\frac{\ln(0.9)}{a}\right) = \frac{\ln(0.9) - \ln(0.1)}{a} = \frac{\ln(9)}{a}
$$
This shows that for any first-order system, the 10%–90% rise time is precisely $\ln(9) \approx 2.2$ times its time constant $\tau$. What about the 0%–100% [rise time](@entry_id:263755)? The response starts at $y(0)=0$. To reach 100% of the final value, we require $\exp(-at) = 0$, which is only true in the limit as $t \to \infty$. Therefore, the 0%–100% rise time is infinite. This is a key theoretical point: a system with an [exponential response](@entry_id:269644) component approaches its final value asymptotically but never reaches it in finite time [@problem_id:2754678].

#### Second-Order Underdamped Systems

The canonical underdamped [second-order system](@entry_id:262182), with transfer function $T(s) = \frac{\omega_n^2}{s^2 + 2\zeta\omega_n s + \omega_n^2}$ where $0  \zeta  1$, is arguably the most important prototype in control theory. Its unit [step response](@entry_id:148543) is given by:
$$
y(t) = 1 - \frac{\exp(-\zeta\omega_n t)}{\sqrt{1-\zeta^2}} \sin(\omega_d t + \phi)
$$
where $\omega_d = \omega_n\sqrt{1-\zeta^2}$ is the [damped natural frequency](@entry_id:273436) and $\phi = \arccos(\zeta)$ is a phase angle. The response consists of a decaying exponential envelope modulating a sinusoidal oscillation.

*   **Rise Time:** If we define rise time as the time to first reach the final value of 1, we set $y(t_r)=1$. This implies $\sin(\omega_d t_r + \phi) = 0$. The smallest positive time $t_r$ corresponds to the argument being $\pi$, yielding the exact expression [@problem_id:2754688]:
    $$
    t_r = \frac{\pi - \arccos(\zeta)}{\omega_n \sqrt{1-\zeta^2}}
    $$
    A common approximation, especially for small damping, is to neglect the phase offset $\phi$, leading to the simpler formula $t_{r,\text{app}} = \frac{\pi}{\omega_d}$. While convenient, this approximation can be highly inaccurate, with the relative error approaching 100% as the damping ratio $\zeta$ approaches zero [@problem_id:2754688].

*   **Peak Time and Overshoot:** The [peak time](@entry_id:262671) $t_p$ corresponds to the first peak of the sinusoid after $t=0$, which occurs when $\omega_d t = \pi$. This gives the exact formula $t_p = \frac{\pi}{\omega_d}$. Substituting this into the response $y(t)$ yields the peak value $y_{\max} = y(t_p) = 1 + \exp(-\zeta\pi/\sqrt{1-\zeta^2})$. The [percent overshoot](@entry_id:261908) $M_p$ is then:
    $$
    M_p = \frac{y_{\max} - 1}{1} = \exp\left(-\frac{\pi\zeta}{\sqrt{1-\zeta^2}}\right)
    $$
    This fundamental result shows that the [percent overshoot](@entry_id:261908) of a [canonical second-order system](@entry_id:266318) is a function of the [damping ratio](@entry_id:262264) $\zeta$ only.

*   **Settling Time:** The [settling time](@entry_id:273984) is determined by the decay of the response envelope. The error signal is $e(t) = 1-y(t)$, and its envelope is $E_{\text{env}}(t) = \frac{\exp(-\zeta\omega_n t)}{\sqrt{1-\zeta^2}}$. To find the envelope-based [settling time](@entry_id:273984) $t_s(\epsilon)$ for a tolerance $\epsilon$, we solve for the time when the envelope decays to $\epsilon$:
    $$
    \frac{\exp(-\zeta\omega_n t_s)}{\sqrt{1-\zeta^2}} = \epsilon \implies t_s(\epsilon) = \frac{1}{\zeta\omega_n} \ln\left(\frac{1}{\epsilon\sqrt{1-\zeta^2}}\right)
    $$
    This is an exact expression for settling time based on the envelope [@problem_id:2754681]. For the common 2% criterion ($\epsilon=0.02$), and for small $\zeta$ where $\sqrt{1-\zeta^2} \approx 1$, the formula gives the widely used "rule of thumb" $t_s \approx \frac{\ln(50)}{\zeta\omega_n} \approx \frac{3.91}{\zeta\omega_n}$, often rounded to $t_s \approx \frac{4}{\zeta\omega_n}$.

### Advanced Topics and Extensions

While prototype systems offer foundational insights, real-world systems often feature additional complexities. We now extend our analysis to consider the effects of zeros and to systems operating in discrete-time or with multiple inputs and outputs.

#### The Influence of Zeros on Transient Response

Adding a zero to a system's transfer function can significantly alter its transient response. Consider adding a stable, real zero at $s=-z$ to our second-order prototype, while preserving the DC gain of unity:
$$
G_z(s) = \left(1 + \frac{s}{z}\right) G_0(s)
$$
where $G_0(s)$ is the original prototype. The [step response](@entry_id:148543) of this new system is $y_z(t) = y_0(t) + \frac{1}{z}\dot{y}_0(t)$, where $y_0(t)$ is the prototype's response. The additional term $\frac{1}{z}\dot{y}_0(t)$ introduces a velocity feedforward component. For a left-half-plane zero ($z>0$), this term initially acts in the same direction as the main response, often increasing the overshoot and potentially affecting rise and settling times.

The effect on [settling time](@entry_id:273984) can be analyzed by examining the new error envelope. Using complex residue calculations, it can be shown that the envelope of the transient for the system with the zero is larger than the original envelope by a specific factor that depends on the zero location $z$, the natural frequency $\omega_n$, and the [damping ratio](@entry_id:262264) $\zeta$. For a system with $\omega_n=5$, $\zeta=0.3$, adding a zero at $z=2$ substantially modifies the transient envelope, leading to a demonstrable increase in the [2% settling time](@entry_id:261963). This illustrates a critical design trade-off: while zeros can be used to shape a response, they can also degrade other performance metrics if not placed carefully [@problem_id:2754707].

#### Specifications for Discrete-Time Systems

In [digital control](@entry_id:275588), signals are sequences defined at [discrete time](@entry_id:637509) intervals $t = k T_s$, where $k$ is the sample index and $T_s$ is the sampling period. The definitions of time-domain specifications must be adapted accordingly.

*   **Rise Time ($t_r$):** The first-passage times are defined by the earliest sample indices that meet the criteria. The 10%-90% rise time is $t_r = (k_{90} - k_{10})T_s$, where:
    $$
    k_{10} = \min\{k \ge 0 : y[k] \ge 0.1 y_{\infty}\}, \quad k_{90} = \min\{k \ge 0 : y[k] \ge 0.9 y_{\infty}\}
    $$
*   **Settling Time ($t_s$):** The "enter-and-stay" criterion is captured using a [universal quantifier](@entry_id:145989) over future sample indices. The [settling time](@entry_id:273984) is $t_s = k_s T_s$, where:
    $$
    k_s = \min\{k \ge 0 : |y[\ell] - y_{\infty}| \le \delta|y_{\infty}| \text{ for all } \ell \ge k\}
    $$
*   **Peak Time ($t_p$) and Overshoot ($M_p$):** The [peak time](@entry_id:262671) corresponds to the first sample index achieving the maximum value: $t_p = k_p T_s$ where $k_p = \min \arg\max_{k \ge 0} y[k]$. The [percent overshoot](@entry_id:261908) is defined analogously: $M_p = \max\{0, (y[k_p] - y_{\infty}) / |y_{\infty}|\}$ [@problem_id:2754668].

To see these principles in action, consider a simple discrete-time system with a single pole at $z = -r$, where $0  r  1$, and unit DC gain. Its [step response](@entry_id:148543), assuming a zero initial condition, can be derived as $y[k] = 1 - (-r)^k$ for $k \ge 0$. The steady-state value is $y_{\infty}=1$. The error term, $-(-r)^k$, alternates in sign at each sample while its magnitude decreases. This is a **monotone alternating** response, a behavior unique to [discrete-time systems](@entry_id:263935). The peak value occurs at the sample k=1, where `y[1] = 1+r`. The relative overshoot is therefore $M_p = (y[1]-y_{\infty})/y_{\infty} = r$. This simple example shows that even a single real pole can cause overshoot if it is on the negative real axis, a stark contrast to continuous-time [first-order systems](@entry_id:147467) [@problem_id:2754667].

#### Specifications for MIMO Systems

In multiple-input, multiple-output (MIMO) systems, interactions between channels complicate the definition and measurement of specifications. The response at one output, $y_i(t)$, is a superposition of responses due to all inputs, $u_j(t)$.

A meaningful **channel-wise specification** for the channel $u_j \to y_i$ must be defined by isolating that channel's response. The standard procedure, both analytically and experimentally, is to apply a step input to $u_j$ while holding all other inputs at zero. The specifications can then be computed from the resulting $y_i(t)$ [@problem_id:2754696].

When multiple inputs are active simultaneously, this isolation is lost. Consider a 2x2 system where both inputs receive a unit step. The response of the first output is $Y_1(s) = G_{11}(s)U_1(s) + G_{12}(s)U_2(s)$. The observed response $y_1(t)$ is the sum of the decoupled response from $u_1$ and a cross-coupling response from $u_2$. This coupling term acts as a disturbance that corrupts the "true" specifications of the $u_1 \to y_1$ channel. For instance, if the decoupled response $y_{1,d}(t)$ has a peak at $t_{p,d}$, its derivative is zero at that instant. However, if the coupling response $y_{1,c}(t)$ has a positive slope at $t_{p,d}$, the [total derivative](@entry_id:137587) $\dot{y}_1(t_{p,d}) = \dot{y}_{1,d}(t_{p,d}) + \dot{y}_{1,c}(t_{p,d})$ will be positive. This means the combined response is still rising, and its peak will be delayed to a time $t_p > t_{p,d}$. This demonstrates that time-domain specifications measured during simultaneous excitation are not characteristic of the individual channels but of the combined system and specific input vector [@problem_id:2754696]. Sound experimental practice for characterizing MIMO plants therefore relies on one-at-a-time input excitation or the use of pre-compensating decouplers.