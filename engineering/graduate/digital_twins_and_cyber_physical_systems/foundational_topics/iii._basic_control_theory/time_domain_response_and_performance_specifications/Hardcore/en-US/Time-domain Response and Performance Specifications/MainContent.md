## Introduction
Understanding and quantifying the dynamic behavior of physical systems is a cornerstone of modern engineering, particularly in the realm of Digital Twins (DTs) and Cyber-Physical Systems (CPS). A DT's primary role is to accurately predict and optimize its physical counterpart, a task that demands a precise language for performance. While frequency-domain methods offer deep insights into stability, [time-domain specifications](@entry_id:164027) provide a more direct and intuitive measure of how a system behaves moment-to-moment, especially during critical transient phases. This article addresses the need for a rigorous framework to define and analyze transient performance, bridging the gap between theoretical models and real-world system behavior.

This article provides a comprehensive exploration of [time-domain response](@entry_id:271891) analysis. In "Principles and Mechanisms," you will learn the fundamental metrics and mathematical tools, from classical transfer functions to modern [state-space analysis](@entry_id:266177), used to characterize [system dynamics](@entry_id:136288). "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to solve complex problems in robotics, power electronics, and networked control, highlighting the unique challenges of the cyber-physical domain. Finally, "Hands-On Practices" will allow you to apply these concepts through guided problems, solidifying your ability to analyze, predict, and shape system performance.

## Principles and Mechanisms

The primary function of a Digital Twin (DT) within a Cyber-Physical System (CPS) is often to predict, monitor, and optimize the dynamic behavior of its physical counterpart. To achieve this, we must establish a rigorous, quantitative language to describe system performance. While [frequency-domain analysis](@entry_id:1125318) provides profound insights into stability and robustness, [time-domain specifications](@entry_id:164027) offer a more direct and intuitive assessment of a system's transient behavior. These specifications quantify how a system responds to a canonical input, most commonly a step change in its reference or a disturbance. This chapter elucidates the fundamental principles governing [time-domain response](@entry_id:271891) and the mechanisms by which we analyze and specify performance, transitioning from classical transfer function models to modern state-space representations and addressing challenges unique to the cyber-physical context.

### Defining Time-Domain Performance Metrics

The response of a system to a step input, $u(t) = A\,\mathbf{1}(t)$, where $\mathbf{1}(t)$ is the [unit step function](@entry_id:268807), is a rich source of information. The transient portion of this response reveals the system's inherent dynamic character—its speed, oscillatory nature, and damping. To formalize this, we define a set of standard time-domain performance specifications. Let $y(t)$ be the system output, and assume the system is stable, such that its output converges to a finite steady-state value, $y_{\infty} = \lim_{t \to \infty} y(t)$. We also define the [supremum and infimum](@entry_id:146074) of the response as $y_{\max} = \sup_{t \ge 0} y(t)$ and $y_{\min} = \inf_{t \ge 0} y(t)$, respectively.

A robust set of definitions must be precise and handle various scenarios, such as responses that settle to negative values or exhibit both over- and undershooting behavior.

-   **Percent Overshoot ($M_p$) and Undershoot ($M_u$)**: Overshoot quantifies the amount by which the response exceeds its final value. A scientifically rigorous definition must be normalized by the magnitude of the steady-state value to be invariant to the sign of the response. For an excursion *above* the final value (i.e., $y_{\max} > y_{\infty}$), the **[percent overshoot](@entry_id:261908)** is defined as:
    $$
    M_p = \frac{y_{\max} - y_{\infty}}{|y_{\infty}|}
    $$
    If the response never exceeds the final value ($y_{\max} \le y_{\infty}$), the overshoot is zero. Similarly, for an excursion *below* the final value (i.e., $y_{\min}  y_{\infty}$), the **percent undershoot** is defined as:
    $$
    M_u = \frac{y_{\infty} - y_{\min}}{|y_{\infty}|}
    $$
    These separate definitions allow us to distinguish between these two distinct behaviors. Crucially, if a finite steady-state value $y_{\infty}$ does not exist (e.g., for an unstable or marginally stable system), these metrics are undefined. Attempting to approximate a final value or substitute an arbitrary one would be non-rigorous .

-   **Peak Time ($t_p$)**: This is the time at which the first peak of the overshoot occurs, corresponding to the instant $t0$ where $y(t)$ first reaches a [local maximum](@entry_id:137813).

-   **Rise Time ($t_r$)**: This metric quantifies the speed of the response. It is commonly defined as the time taken for the response to rise from one fraction of its final value to another. The **10-90% [rise time](@entry_id:263755)** ($t_{10-90}$) is the interval $t_{0.9} - t_{0.1}$, where $t_c$ is the time at which the output first reaches the value $c \cdot y_{\infty}$.

-   **Settling Time ($t_s$)**: This is the time required for the response to enter and remain within a specified tolerance band around the final value, typically $\pm 2\%$ or $\pm 5\%$. It measures how long the transient oscillations persist.

### The Canonical Second-Order System

Many complex systems can be effectively modeled or approximated by a second-order linear time-invariant (LTI) system. Its behavior serves as an archetype for understanding [time-domain specifications](@entry_id:164027). The standard form of its governing differential equation is:
$$
\frac{d^2y(t)}{dt^2} + 2\zeta\omega_n\frac{dy(t)}{dt} + \omega_n^2 y(t) = \omega_n^2 u(t)
$$
Here, $\omega_n$ is the **[undamped natural frequency](@entry_id:261839)**, which represents the [oscillation frequency](@entry_id:269468) if there were no damping, and $\zeta$ is the **damping ratio**, a dimensionless quantity that determines the nature of the transient response.

For a system that is **underdamped** ($0  \zeta  1$), the response to a unit step input ($u(t) = \mathbf{1}(t)$ with $y(0)=0, \dot{y}(0)=0$) is a sinusoid whose amplitude decays exponentially:
$$
y(t) = 1 - \frac{\exp(-\zeta \omega_n t)}{\sqrt{1-\zeta^2}} \sin(\omega_d t + \phi)
$$
where $\omega_d = \omega_n \sqrt{1-\zeta^2}$ is the **[damped natural frequency](@entry_id:273436)** and $\phi = \arccos(\zeta)$.

From this analytical solution, we can derive exact expressions for the key performance metrics. The **[peak time](@entry_id:262671)**, $t_p$, is found by setting the first derivative $\dot{y}(t)$ to zero for the first time, which occurs when $\sin(\omega_d t) = 0$ for $t>0$. This yields:
$$
t_p = \frac{\pi}{\omega_d} = \frac{\pi}{\omega_n \sqrt{1-\zeta^2}}
$$
The value of the response at this time is $y(t_p) = 1 + \exp(-\zeta \omega_n t_p)$. This leads directly to the formula for the **[percent overshoot](@entry_id:261908)**, $M_p = y(t_p) - 1$:
$$
M_p = \exp\left(-\frac{\pi\zeta}{\sqrt{1-\zeta^2}}\right)
$$
These two formulae are cornerstones of control theory. The first shows that both $\zeta$ and $\omega_n$ determine the [peak time](@entry_id:262671), while the second reveals a powerful result: the overshoot $M_p$ depends *only* on the [damping ratio](@entry_id:262264) $\zeta$.

In a practical DT context, these relationships are invaluable for [system identification](@entry_id:201290). For instance, if a physical actuator's [step response](@entry_id:148543) is measured, yielding a peak value of $1.200$ times its steady-state value at a time of $t_p = 0.200$ seconds, we can reverse-engineer the parameters of its underlying second-order model. The overshoot $M_p = 0.200$ allows us to solve for $\zeta$. Taking the natural logarithm gives $-\ln(M_p) = \pi\zeta / \sqrt{1-\zeta^2}$, from which $\zeta$ can be isolated. Once $\zeta$ is known, the measured [peak time](@entry_id:262671) $t_p$ allows us to solve for $\omega_n$ using the [peak time](@entry_id:262671) equation. This process provides the essential model parameters needed for the DT to simulate and predict the actuator's behavior .

### Responses of More Complex Systems

While the second-order model is foundational, real-world systems often have more complex dynamics, including additional poles and zeros, which significantly alter the [time-domain response](@entry_id:271891).

#### The Effect of Zeros and Non-Minimum Phase Behavior

Zeros in a system's transfer function, $G(s) = N(s)/D(s)$, introduce derivatives of the input into the response, which can dramatically change its shape. Of particular importance are systems with zeros in the right-half of the complex plane (RHP), known as **[non-minimum phase](@entry_id:267340) (NMP)** systems. These systems are notorious for exhibiting an **[initial inverse response](@entry_id:260690)**, or undershoot, where the output initially moves in the opposite direction to its final value.

Consider a system with transfer function $G(s) = k(s-z)/((s+p_1)(s+p_2))$ where the zero $z$ is positive ($z > 0$). When subjected to a step input, the initial response is dominated by the high-frequency gain, while the final value is determined by the DC gain $G(0)$. Because of the RHP zero, these can have opposite signs, forcing the response to start in one direction before reversing course to reach its steady state. By deriving the [step response](@entry_id:148543) $y(t)$ via inverse Laplace transform and finding the time $t_{min}$ where $\dot{y}(t)=0$, we can calculate the magnitude of this undershoot. This analysis directly links a feature in the [s-plane](@entry_id:271584) (an RHP zero) to a specific, often undesirable, time-domain characteristic that must be accurately captured by a DT .

#### Higher-Order and Critically Damped Systems

For systems of higher order or those that are not underdamped (i.e., $\zeta \ge 1$), the response is no longer oscillatory but consists of a sum of decaying exponential terms. While seemingly simpler, calculating metrics like rise time can become analytically complex. For example, consider a system with a repeated real pole, such as $G(s) = 1/(1+s\tau)^2$, which corresponds to a **critically damped** ($\zeta=1$) [second-order system](@entry_id:262182). The [step response](@entry_id:148543) is found via [partial fraction expansion](@entry_id:265121) and inverse Laplace transform to be:
$$
y(t) = 1 - \left(1 + \frac{t}{\tau}\right)\exp(-t/\tau)
$$
To find the 10-90% rise time, we must solve the equation $y(t_c) = c$ for $t_{0.1}$ and $t_{0.9}$. This requires solving $1-c = (1+t_c/\tau)\exp(-t_c/\tau)$, a [transcendental equation](@entry_id:276279). The solution can be expressed using the **Lambert W function**, which is defined by the relation $z = W(z)\exp(W(z))$. After algebraic manipulation, one finds that the solution involves the $W_{-1}$ branch of this function. This illustrates that even for seemingly simple LTI systems, precise analytical expressions for performance metrics may require advanced mathematical functions, a capability required for high-fidelity DTs .

### The State-Space Perspective

The transfer function is limited to LTI systems with a single input and single output. The **[state-space representation](@entry_id:147149)** provides a far more powerful and general framework for analyzing complex, multi-input, multi-output (MIMO) systems. The system is described by a pair of equations:
$$
\dot{x}(t) = Ax(t) + Bu(t) \quad \text{(State Equation)}
$$
$$
y(t) = Cx(t) + Du(t) \quad \text{(Output Equation)}
$$
where $x(t)$ is the state vector, $A$ is the state matrix, $B$ is the input matrix, $C$ is the output matrix, and $D$ is the feedthrough matrix.

The solution to the state equation for a given initial state $x(0)$ and input $u(t)$ is given by the [convolution integral](@entry_id:155865):
$$
x(t) = \exp(At)x(0) + \int_{0}^{t} \exp(A(t-\tau))Bu(\tau)d\tau
$$
The term $\exp(At)$, known as the **[state transition matrix](@entry_id:267928)** or **matrix exponential**, is central to the entire [time-domain response](@entry_id:271891). It propagates the state of the system through time. The matrix exponential is formally defined by its Taylor [series expansion](@entry_id:142878):
$$
\exp(At) = I + At + \frac{(At)^2}{2!} + \frac{(At)^3}{3!} + \dots
$$
While this series is the formal definition, it is often computed via other means. If the matrix $A$ is diagonalizable, $A=PDP^{-1}$, then $\exp(At) = P\exp(Dt)P^{-1}$, which is straightforward to calculate. However, if $A$ has [repeated eigenvalues](@entry_id:154579) and is not diagonalizable, it must be brought to its **Jordan [normal form](@entry_id:161181)**. For example, if $A = D+N$, where $D$ is diagonal and $N$ is a [nilpotent matrix](@entry_id:152732) ($N^k=0$ for some integer $k$), and if $D$ and $N$ commute ($DN=ND$), then $\exp(At) = \exp(Dt)\exp(Nt)$. The exponential of the nilpotent part becomes a finite polynomial in $t$, as its [series expansion](@entry_id:142878) truncates .

#### Modal Decomposition

The state-space framework reveals that the system's response is a superposition of **modes**, each corresponding to an eigenvalue of the state matrix $A$. Real eigenvalues correspond to exponentially decaying or growing modes ($e^{\lambda t}$), while complex conjugate pairs of eigenvalues $\lambda = \sigma \pm j\omega_d$ correspond to damped oscillatory modes ($e^{\sigma t}\cos(\omega_d t)$, $e^{\sigma t}\sin(\omega_d t)$).

If the state matrix $A$ is block-diagonal, the system decouples into independent subsystems. This allows for a clear analysis of how each mode contributes to the overall output. For example, a system with a state matrix like $A=\text{diag}(A_1, A_2)$ can be analyzed by solving the simpler dynamics for each block, $\dot{x}_1 = A_1 x_1 + B_1 u$ and $\dot{x}_2 = A_2 x_2 + B_2 u$, and then reconstructing the total output $y(t)$ using the output matrix $C$. This decomposition is a powerful conceptual and computational tool for understanding and predicting the behavior of complex systems by examining their constituent dynamic parts .

### Performance in the Cyber-Physical Domain

In a CPS, the continuous-time dynamics of the physical plant interact with the discrete-time logic of the digital controller and observer. This interface introduces unique challenges that a high-fidelity DT must account for.

#### Sampling and Measurement Discrepancies

A DT or digital controller does not see the continuous output $y(t)$ but rather a sampled version, $y(kT_s)$, where $T_s$ is the [sampling period](@entry_id:265475). This sampling process can lead to significant discrepancies between the true performance of the physical asset and the performance measured by the digital system.

For example, the measured [peak time](@entry_id:262671) will be an integer multiple of the [sampling period](@entry_id:265475), $t_{p, \text{meas}} = n^{\star}T_s$. The sample index $n^{\star}$ is the one that maximizes $y(nT_s)$. This index is not necessarily the one for which $nT_s$ is closest to the true [peak time](@entry_id:262671) $t_p$. One must compare the output values at the sampling instants surrounding the true peak to find the actual measured maximum .

Similarly, the measured overshoot can be substantially lower than the true continuous-time overshoot. A worst-case scenario occurs when the true peak falls exactly halfway between two sampling instants. The measured overshoot, $M_{p,s}$, will be the value of the response at one of these two adjacent samples. Due to the decaying nature of the response envelope, the maximum value will occur at the sample time *after* the true peak, i.e., at $t_p + T_s/2$. The ratio of the sampled to continuous overshoot, $\rho = M_{p,s}/M_p$, can be derived analytically and demonstrates that for a given system, faster sampling (smaller $T_s$) leads to $\rho \to 1$, while slower sampling can cause the DT to significantly underestimate the true physical overshoot, potentially leading to incorrect performance assessments .

#### Model Mismatch and Performance Robustness

A DT is, by definition, a model. All models are imperfect. The discrepancy between the nominal model parameters used for design and analysis and the actual parameters of the physical plant is known as **[model mismatch](@entry_id:1128042)**. A crucial task for a DT is to predict how this mismatch affects system performance.

Consider a PD controller designed to give a nominal system (with mass $m_0$) a desired closed-loop damping ratio $\zeta_0$. If the actual physical plant has a different mass, $m = m_0(1+\delta)$, the fixed controller gains will now be operating on a different system. By substituting the controller into the actual plant dynamics and recasting the resulting closed-loop equation into the standard second-order form, we can derive the *actual* damping ratio of the physical system, $\zeta = \zeta_0 / \sqrt{1+\delta}$. Using this actual $\zeta$ in the overshoot formula reveals precisely how the overshoot will change as a function of the mass uncertainty $\delta$. This type of analysis, central to robust control, is essential for a DT to provide reliable performance guarantees in the face of real-world [parametric uncertainty](@entry_id:264387) .

#### Control Effort as a Performance Metric

Finally, performance is not solely about the output response; it also concerns the resources required to achieve it. In many CPS applications, from robotics to power electronics, minimizing actuator effort or energy consumption is critical. The **actuation energy** can be quantified by the squared $\mathcal{L}^2$ norm of the control input, $E[u] = \int_0^T u(t)^2 dt$.

For an LTI system, a fundamental question is: what is the minimum energy required to drive the output to a specific value $y_T$ at a time $T$? The output at time $T$ is given by the inner product $y_T = \langle g, u \rangle$ in the function space $\mathcal{L}^2[0,T]$, where the kernel $g(\tau) = C\exp(A(T-\tau))B$ encapsulates the system's dynamics. The Cauchy-Schwarz inequality, $|\langle g, u \rangle|^2 \le \|g\|^2 \|u\|^2$, provides a lower bound on the required energy: $\|u\|^2 \ge y_T^2 / \|g\|^2$. The minimum energy is achieved when the input signal $u(t)$ is chosen to be proportional to the kernel function $g(t)$. This establishes a profound link between the system's inherent properties (encoded in $A, B, C$) and the minimum achievable cost to perform a control task, providing another critical dimension of time-domain performance specification .