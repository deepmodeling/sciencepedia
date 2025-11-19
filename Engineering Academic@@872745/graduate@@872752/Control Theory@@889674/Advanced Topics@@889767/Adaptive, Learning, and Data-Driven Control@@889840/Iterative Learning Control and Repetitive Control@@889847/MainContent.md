## Introduction
Iterative Learning Control (ILC) and Repetitive Control (RC) represent a class of advanced control strategies designed to achieve exceptional performance in systems that execute the same task over and over. While conventional feedback controllers treat each moment in time as a new event, ILC and RC exploit the repetitive nature of a task to learn from past errors and progressively refine the control action, ultimately attaining a level of precision that is often unattainable by other means. This article addresses the fundamental knowledge gap between standard control theory and the specialized techniques required for these learning-based systems. It provides a comprehensive framework for understanding, analyzing, and applying ILC and RC.

This article is structured to build your expertise systematically. In the **Principles and Mechanisms** chapter, we will dissect the core concepts, starting with the unique two-dimensional (time and trial) nature of learning control. You will learn the mathematical tools for modeling repetitive tasks, including the powerful lifted system representation, and master the rigorous convergence analysis that forms the theoretical bedrock of ILC. Following this, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice. We will explore how these methods solve critical engineering problems in robotics and manufacturing, discuss practical challenges like robustness and constraints, and uncover fascinating parallels between ILC and iterative processes found in biology and computational science. Finally, the **Hands-On Practices** section will provide you with opportunities to apply these concepts to solve concrete design and analysis problems.

## Principles and Mechanisms

Iterative Learning Control (ILC) and Repetitive Control (RC) are powerful control methodologies designed for systems that perform the same task repeatedly. While both exploit repetition to enhance performance, they are founded on distinct principles and operate under different assumptions. This chapter elucidates the fundamental mechanisms of ILC and RC, starting from their conceptual basis and progressing to the mathematical tools required for their analysis and design.

### The Two-Dimensional Nature of Learning Control

The defining characteristic of a learning control problem is its two-dimensional structure, indexed by both time and trial. Consider a task that is executed repeatedly. We denote the **trial index** by $k \in \{1, 2, 3, \dots\}$ and the **within-trial time index** by $t \in \{0, 1, \dots, N-1\}$, where $N$ is the duration of the task. Consequently, a signal such as the system output is denoted $y_k(t)$, representing the output at time $t$ during the $k$-th execution of the task. Similarly, the control input is denoted $u_k(t)$.

This two-dimensional framework introduces a unique perspective on **causality**. Causality dictates that an effect cannot precede its cause. We must analyze this principle with respect to both indices:

*   **Causality in Trial Index $k$**: The progression from trial $k$ to trial $k+1$ represents the physical passage of time in the learning process. Trial $k$ must be fully completed before the system can even begin trial $k+1$. Therefore, any computation for trial $k+1$, such as determining the input signal $u_{k+1}(t)$, can depend on data from trial $k$ and previous trials, but it is physically impossible for it to depend on data from future trials (e.g., $y_{k+1}(t)$ or $y_{k+2}(t)$). Causality with respect to the trial index $k$ is absolute and cannot be relaxed.

*   **Causality in Time Index $t$**: The situation for the time index $t$ is more nuanced and is central to the power of ILC. Within the real-time execution of any single trial $k$, physical causality must be respected. The control input $u_k(t)$ can only depend on past and present measurements from that same trial, i.e., $\{y_k(\tau) | \tau \le t\}$. However, the core ILC update happens *between* trials. After trial $k$ is finished, the entire data record for that trial, specifically the error trajectory $\{e_k(t)\}_{t=0}^{N-1}$, is available for offline processing. When computing the control input for the next trial, $u_{k+1}(t)$, the algorithm has access to the *entire* history of the previous trial. This means the calculation of $u_{k+1}(t)$ can use error information from "future" time steps of the previous trial, such as $e_k(t+1), e_k(t+2)$, etc. This allows the learning update law to be **noncausal** with respect to the time index $t$. This ability to use noncausal filters is a key advantage of ILC, enabling it to overcome limitations faced by traditional real-time controllers [@problem_id:2714825].

### Mathematical Formulation of Repetitive Tasks

For a learning algorithm to be effective, the task it is trying to learn must be repeatable. The way this repetition is defined mathematically distinguishes the two main paradigms of learning control: finite-horizon ILC and continuous-operation RC.

#### The Finite-Horizon ILC Setting

ILC is typically formulated for tasks of a fixed, finite duration. A discrete-time linear time-invariant (LTI) plant is described by [state-space equations](@entry_id:266994) for each trial $k$:
$$
x_{k}(t+1) = A x_k(t) + B u_k(t), \quad y_k(t) = C x_k(t), \quad t=0,\dots,N-1
$$
where $x_k(t)$ is the state, $u_k(t)$ is the input, and $y_k(t)$ is the output. The matrices $A$, $B$, and $C$ are constant. Note: to avoid notational confusion, state space variables are written as $x_k(t)$ instead of $x_t^k$.

The fundamental premise of ILC is that the system's response to a given input sequence is identical from trial to trial. This requires two critical assumptions:
1.  **Repeatable Reference**: The desired reference trajectory $\{r(t)\}_{t=0}^{N-1}$ is the same for every trial $k$.
2.  **Repeatable Initial State**: The system is reset to the same initial state at the beginning of every trial, i.e., $x_k(0) = \bar{x}_0$ for all $k$.

These two conditions ensure that the underlying dynamics relating the control input to the [tracking error](@entry_id:273267) are invariant across trials. If the reference or the initial state were to change randomly from one trial to the next, the task itself would be different each time, and learning from past errors would be confounded. It is important to note that while the initial state $\bar{x}_0$ must be repeatable, its specific value need not be known to the control designer. The effect of a constant, non-zero $\bar{x}_0$ manifests as a repeatable component of the error, which the ILC algorithm can learn to counteract implicitly [@problem_id:2714777].

To facilitate analysis, it is standard practice to re-write the trial dynamics in a **lifted system representation**. By unrolling the state-space recursion over the horizon $t=1, \dots, N$, we can express the entire sequence of outputs for a trial as a single linear equation. Let the stacked output vector be $y \triangleq [y(1)^\top, y(2)^\top, \dots, y(N)^\top]^\top$ and the stacked input vector be $u \triangleq [u(0)^\top, u(1)^\top, \dots, u(N-1)^\top]^\top$. The relationship is given by:
$$
y = G u + H x_0
$$
The matrix $H$ maps the initial state to the output sequence and has the structure:
$$
H = \begin{pmatrix} CA \\ CA^2 \\ \vdots \\ CA^N \end{pmatrix}
$$
The matrix $G$ maps the input sequence to the output sequence and is a block lower-triangular Toeplitz matrix:
$$
G = \begin{pmatrix}
CB & 0 & \cdots & 0 \\
CAB & CB & \cdots & 0 \\
\vdots & \vdots & \ddots & \vdots \\
CA^{N-1}B & CA^{N-2}B & \cdots & CB
\end{pmatrix}
$$
The block lower-triangular structure of $G$ is a manifestation of causality within a trial: the output at time $t$ depends only on inputs up to time $t-1$. This lifted representation transforms the two-dimensional problem ($k, t$) into a one-dimensional problem in the trial index $k$, where signals are large vectors and systems are large matrices [@problem_id:2714782].

#### The Continuous-Operation RC Setting

In contrast to ILC, Repetitive Control (RC) is designed for systems that operate continuously and must track or reject an exogenous signal that is periodic with a known period $N$. Here, the repetition is not between discrete, reset trials, but is inherent in the time axis itself, captured by the condition $r(t+N) = r(t)$ for all $t$.

In this setting, there is no reset. The state at the beginning of one period is simply the state at the end of the previous period. This leads to a different boundary condition: $x_k(0) = x_{k-1}(N)$, where $k$ now indexes periods within a single, unending run. This "wrap-around" or [cyclic boundary condition](@entry_id:262709) is fundamentally different from the fixed-reset condition of ILC. Conceptually, RC controllers operate by embedding an **internal model** of the [periodic signal](@entry_id:261016) generator. For a [discrete-time signal](@entry_id:275390) of period $N$, this model often takes the form of a positive feedback loop with a delay of $N$ time steps, which can be represented by the [transfer function pole](@entry_id:267284) structure of $1/(1-z^{-N})$. This delay line provides memory of the previous cycle's error, which is used to correct the current cycle's control action in real time [@problem_id:2714773].

### Convergence Analysis of ILC

The central question in ILC is whether the trial-to-trial learning process converges, causing the tracking error to approach zero.

#### The Error Propagation Dynamics

A general class of linear ILC laws updates the control input for the next trial based on the input and error from the current trial. Using the lifted system representation, this can be written as:
$$
u_{k+1} = \mathcal{Q}(u_k + \mathcal{L}e_k)
$$
where $\mathcal{L}$ is a learning operator (often a filter) and $\mathcal{Q}$ is a filter used for robustness. A simple and common form, known as **P-type ILC**, sets $\mathcal{Q}=I$ and uses a simple gain for learning:
$$
u_{k+1} = u_k + L e_k
$$
Here, $L$ is a matrix representing the learning filter. Let's derive how the error evolves. The error in trial $k+1$ is $e_{k+1} = r - y_{k+1}$. Using the lifted model $y_{k+1} = G u_{k+1} + H x_0$ (assuming a constant initial state $x_0$ and reference $r$):
$$
e_{k+1} = r - (G u_{k+1} + H x_0) = r - G(u_k + L e_k) - H x_0
$$
Rearranging terms yields:
$$
e_{k+1} = (r - G u_k - H x_0) - G L e_k
$$
Recognizing that the term in parentheses is precisely the error from trial $k$, $e_k = r - y_k = r - (G u_k + H x_0)$, we arrive at the fundamental [error propagation](@entry_id:136644) equation:
$$
e_{k+1} = e_k - G L e_k = (I - G L) e_k
$$
This equation shows that the error from one trial to the next is governed by a [linear operator](@entry_id:136520) $A_e \triangleq I - G L$ [@problem_id:2714778].

#### The Fundamental Convergence Condition

The error sequence $\{e_k\}$ converges to zero for any initial error $e_0$ if and only if the discrete-time linear system $e_{k+1} = A_e e_k$ is asymptotically stable. A cornerstone theorem of [linear systems theory](@entry_id:172825) states that this is true if and only if the **[spectral radius](@entry_id:138984)** of the propagation matrix $A_e$ is strictly less than one:
$$
\rho(A_e)  1
$$
The [spectral radius](@entry_id:138984), $\rho(A_e)$, is defined as the largest magnitude among all eigenvalues of the matrix $A_e$. This is the necessary and sufficient condition for ILC convergence.

It is important to distinguish this from conditions based on [matrix norms](@entry_id:139520). A sufficient (but not necessary) condition for convergence is that any [induced norm](@entry_id:148919) of the operator is less than one, e.g., $\|A_e\|_2  1$. However, a system can converge even if its norm is greater than one, as long as its spectral radius is less than one. A key related result states that $\rho(A_e)  1$ if and only if there *exists* some [induced norm](@entry_id:148919) $\|\cdot\|_\star$ such that $\|A_e\|_\star  1$. The existence of such a norm guarantees [exponential convergence](@entry_id:142080) of the error [@problem_id:2714778].

#### Frequency-Domain Interpretation

The [spectral radius](@entry_id:138984) condition provides a powerful analytical tool in the time domain. For LTI systems, it is often intuitive to analyze convergence in the frequency domain. If we assume the task is periodic and approximate the lifted plant matrix $G$ and learning matrix $L$ as [circulant matrices](@entry_id:190979), then convolution in the time domain becomes simple multiplication in the frequency domain. In this case, the matrices $G$ and $L$ are diagonalized by the Discrete Fourier Transform (DFT), and their eigenvalues are the values of their frequency responses $G(e^{j\omega})$ and $L(e^{j\omega})$ at the DFT frequencies $\omega_m = 2\pi m / N$.

The eigenvalues of the [error propagation](@entry_id:136644) operator $A_e = I - G L$ are then simply $1 - G(e^{j\omega_m})L(e^{j\omega_m})$. The spectral radius condition $\rho(I-GL)  1$ thus becomes equivalent to requiring that the maximum magnitude of these eigenvalues is less than one:
$$
\sup_{\omega \in [0, 2\pi)} |1 - G(e^{j\omega})L(e^{j\omega})|  1
$$
This condition must hold for all frequencies excited by the task. It states that at every frequency, the learning process must be a contraction mapping [@problem_id:2714791]. For the simple P-type ILC where $L(e^{j\omega}) = \alpha$ (a constant scalar), the condition simplifies to $\sup_\omega |1 - \alpha G(e^{j\omega})|  1$. This condition provides a clear guideline for choosing the learning gain $\alpha$ based on the plant's [frequency response](@entry_id:183149) [@problem_id:2714795].

### Advanced Topics and Practical Considerations

#### Handling Disturbances and Noise

Real-world systems are subject to disturbances. We can model the measured output as:
$$
y_k = G u_k + d_r + n_k
$$
Here, $d_r$ is a **repeating disturbance** (e.g., due to repeatable mechanical friction or a periodic external force) that is identical for every trial, and $n_k$ is a **non-repeating disturbance** or noise (e.g., sensor noise) that varies randomly from trial to trial.

Let's re-derive the [error propagation](@entry_id:136644) dynamics. The error is $e_k = r - y_k = r - (G u_k + d_r + n_k)$. The next error is $e_{k+1} = r - y_{k+1} = r - (G u_{k+1} + d_r + n_{k+1})$. Substituting $u_{k+1} = u_k + L e_k$:
$$
e_{k+1} = r - G u_k - G L e_k - d_r - n_{k+1}
$$
From the definition of $e_k$, we can write $r - G u_k - d_r = e_k + n_k$. Substituting this gives:
$$
e_{k+1} = (e_k + n_k) - G L e_k - n_{k+1} = (I - G L) e_k + n_k - n_{k+1}
$$
This updated dynamic reveals two crucial insights:
1.  The repeating disturbance $d_r$ has completely vanished from the [error propagation](@entry_id:136644) equation. This means that a standard ILC algorithm is inherently capable of learning to reject any and all disturbances that repeat perfectly from trial to trial. The learning process automatically adjusts the control input to counteract their effect.
2.  The non-repeating noise $n_k$ now acts as a driving term in the error dynamics. If we assume $n_k$ is zero-mean [white noise](@entry_id:145248), taking the expectation of the error equation gives $\mathbb{E}[e_{k+1}] = (I - G L)\mathbb{E}[e_k]$. If the convergence condition $\rho(I-GL)  1$ holds, the mean error $\mathbb{E}[e_k]$ will converge to zero. This means ILC achieves zero [tracking error](@entry_id:273267) *on average* in the presence of non-repeating noise, but the noise will cause the error to have a non-zero variance around zero at steady state [@problem_id:2714767].

#### Robustness to Model Uncertainty

The convergence analysis so far has assumed a perfect model $G$ of the plant. In reality, there is always some mismatch. A common way to model this is with **[multiplicative uncertainty](@entry_id:262202)**, where the true plant $G_\Delta$ is related to the nominal model $G$ by $G_\Delta = G(I+\Delta)$, and the uncertainty $\Delta$ is bounded in norm, e.g., $\|\Delta\|_\infty \le \bar{\delta}$.

The [error propagation](@entry_id:136644) for the true system is $e_{k+1} = (I - G_\Delta L) e_k$. For robust convergence, we need $\|I - G_\Delta L\|_\infty  1$ for all possible $\Delta$. Using the triangle inequality, we can derive a sufficient condition for [robust stability](@entry_id:268091):
$$
\|I - G L\|_\infty + \|\Delta G L\|_\infty  1
$$
By bounding the uncertainty term, we arrive at the condition:
$$
\sup_\omega|1-G(j\omega)L(j\omega)| + \bar{\delta} \sup_\omega|G(j\omega)L(j\omega)|  1
$$
This condition shows a fundamental trade-off. The term $|GL|$ represents the "control effort" or [loop gain](@entry_id:268715) of the learning process. A higher gain may speed up nominal convergence but also amplifies the effect of uncertainty (as seen in the term $\bar{\delta} |GL|$), potentially leading to instability. Designing a robust ILC requires balancing nominal performance against stability in the face of [model error](@entry_id:175815) [@problem_id:2714787] [@problem_id:2714795].

#### Inversion and Nonminimum-Phase Systems

Ideally, to achieve perfect tracking in a single step ($e_{k+1} = 0$), the [error propagation](@entry_id:136644) operator $I-GL$ should be the zero operator. This would require the learning filter $L$ to be the inverse of the plant, $L = G^{-1}$. However, this is often impossible in practice.

A critical challenge arises from **nonminimum-phase (NMP)** systems. These are systems that have zeros outside the unit circle in the z-plane. If a plant $G(z)$ has an NMP zero $z_0$ with $|z_0|>1$, its inverse $G(z)^{-1}$ will have a pole at $z_0$. A pole outside the unit circle corresponds to an unstable and unbounded impulse response. Therefore, a causal, stable inverse for an NMP system does not exist. This is a fundamental limitation for any real-time causal controller.

This is where the noncausal nature of the ILC update becomes a decisive advantage. Since the learning filter $L$ is applied offline to the stored data from the previous trial, it does not need to be causal. A stable, noncausal inverse can be constructed by factoring the plant transfer function $G(z)$ into a minimum-phase part $G_{mp}(z)$ and an all-pass nonminimum-phase part $G_{nmp}(z)$. The stable inverse is then formed by:
1.  Inverting the minimum-phase part causally, $L_{mp}(z) = G_{mp}(z)^{-1}$, which is stable.
2.  Inverting the nonminimum-phase part noncausally. This is effectively achieved by time-reversal. For a [nonminimum-phase zero](@entry_id:164181) $z_0$, the noncausal inverse has a stable zero at its "mirrored" location $1/\overline{z_0}$. This corresponds to a filter with time advances (positive powers of $z$), which is only implementable offline.

By combining these, one can construct a stable filter $L$ whose [frequency response](@entry_id:183149) $L(e^{j\omega})$ closely approximates $G(e^{j\omega})^{-1}$, especially by ensuring the product $G(e^{j\omega})L(e^{j\omega})$ is real and positive (zero-phase), thereby avoiding the [phase lag](@entry_id:172443) that plagues causal controllers for NMP systems. This powerful capability allows ILC to achieve performance levels on NMP systems that are unattainable with real-time causal control strategies like RC [@problem_id:2714788].