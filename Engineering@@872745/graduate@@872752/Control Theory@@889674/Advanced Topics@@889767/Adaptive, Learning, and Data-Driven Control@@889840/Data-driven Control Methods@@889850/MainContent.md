## Introduction
In the landscape of modern engineering and science, the deluge of data has catalyzed a paradigm shift in how we analyze, predict, and control complex systems. Traditional control theory has long relied on a "model-first" approach, where a precise mathematical model of a system is identified before a controller is designed. However, for many complex, high-dimensional, or poorly understood systems, deriving an accurate first-principles model is a formidable, if not impossible, task. This article addresses this challenge by exploring the powerful and increasingly vital field of [data-driven control](@entry_id:178277), which offers methods to synthesize controllers directly from measurement data, bypassing the intermediate step of explicit [system identification](@entry_id:201290).

This article will guide you from the theoretical underpinnings to practical applications and hands-on implementation. In the first chapter, **Principles and Mechanisms**, we will establish the theoretical cornerstone of the field—Willems' Fundamental Lemma—and explore how it enables a direct, non-parametric approach to control. We will also confront the real-world challenges of noise and uncertainty, developing robust methods for reliable performance. Next, in **Applications and Interdisciplinary Connections**, we will see these principles in action, demonstrating their utility in system identification, direct [controller synthesis](@entry_id:261816), safe learning, and their transformative impact on fields from manufacturing to materials science. Finally, the **Hands-On Practices** chapter provides concrete computational exercises to solidify your understanding of key concepts like data informativity and [robust control](@entry_id:260994) design. We begin by delving into the foundational principles that make this direct data-driven approach possible.

## Principles and Mechanisms

This chapter delves into the foundational principles that enable [data-driven control](@entry_id:178277). We move from the classical paradigm of "identify-then-control" to a more direct approach where control laws are synthesized from raw data. We will establish the theoretical cornerstone for this shift—Willems' Fundamental Lemma—and explore its profound implications for prediction, control, and [system analysis](@entry_id:263805). Furthermore, we will confront the practical challenges of noise and uncertainty, developing rigorous methods to ensure reliability and quantify performance in real-world scenarios.

### The Behavioral Approach and Willems' Fundamental Lemma

The classical approach to control is rooted in a parametric description of a system, typically a state-space model or a transfer function. Data-driven methods, in contrast, often begin from a non-parametric perspective known as the **behavioral approach**. In this framework, a dynamical system is not defined by its internal equations, but by its **behavior**, which is the set of all input-output trajectories that the system can produce. For a discrete-time system, the behavior $\mathfrak{B}$ is a subset of all possible time series of inputs and outputs, $\mathfrak{B} \subset \{(u, y) | u_k \in \mathbb{R}^m, y_k \in \mathbb{R}^p, k \in \mathbb{Z}\}$.

A revolutionary insight in this field is that for Linear Time-Invariant (LTI) systems, this potentially infinite-dimensional set of trajectories can be fully characterized by a *single*, sufficiently long and informative experiment. This insight is formalized in what is known as **Willems' Fundamental Lemma**.

To formalize this, we must first structure the experimental data. Given a measured trajectory of length $T$, $\{(u_k, y_k)\}_{k=0}^{T-1}$, we can organize it using **block Hankel matrices**. A Hankel matrix is a matrix where the anti-diagonals are constant. For a time series $z = \{z_k\}_{k=0}^{T-1}$ where $z_k \in \mathbb{R}^r$, the block Hankel matrix of depth $L$ is defined as:
$$
H_L(z) \triangleq 
\begin{bmatrix}
z_0 & z_1 & \cdots & z_{T-L} \\
z_1 & z_2 & \cdots & z_{T-L+1} \\
\vdots & \vdots & \ddots & \vdots \\
z_{L-1} & z_{L} & \cdots & z_{T-1}
\end{bmatrix} \in \mathbb{R}^{rL \times (T-L+1)}.
$$
Each column of this matrix is a time-shifted "snapshot" or sub-trajectory of the original data, of length $L$. By stacking the Hankel matrices of the input and output data, we form a comprehensive data matrix whose columns represent input-output trajectories observed during the experiment.

Willems' Fundamental Lemma establishes a precise equivalence between the column span of this data matrix and the system's behavior restricted to trajectories of length $L$, denoted $\mathfrak{B}_L$.

**Willems' Fundamental Lemma:** Consider a controllable discrete-time LTI system of minimal order $n$. Let a single input-output trajectory $\{(u_k,y_k)\}_{k=0}^{T-1}$ be given. Let $L \ge 1$ be a desired trajectory length. The set of all input-output trajectories of length $L$ that the system can produce, $\mathfrak{B}_L$, is identical to the column space of the stacked data Hankel matrix $\begin{pmatrix} H_L(u) \\ H_L(y) \end{pmatrix}$ if and only if the input sequence $\{u_k\}_{k=0}^{T-1}$ is **persistently exciting (PE) of order $L+n$**. [@problem_id:2698755]

This lemma is the bedrock of many [data-driven control](@entry_id:178277) methods. It asserts that any valid system trajectory $(u_d, y_d)$ of length $L$ can be represented as a [linear combination](@entry_id:155091) of the observed sub-trajectories. That is, there exists a coefficient vector $g \in \mathbb{R}^{T-L+1}$ such that:
$$
\begin{pmatrix} u_d \\ y_d \end{pmatrix} = \begin{pmatrix} H_L(u) \\ H_L(y) \end{pmatrix} g.
$$
This provides a direct, data-based parameterization of all possible system behaviors without ever needing to compute the [state-space](@entry_id:177074) matrices $(A,B,C,D)$. This ability to bypass explicit system identification is the central advantage of this approach. [@problem_id:2698779]

The critical condition for this powerful result is the **[persistence of excitation](@entry_id:163238)** of the input. An input sequence $\{u_k\}_{k=0}^{T-1}$ with $u_k \in \mathbb{R}^m$ is defined as persistently exciting of order $s$ if its corresponding Hankel matrix $H_s(u) \in \mathbb{R}^{ms \times (T-s+1)}$ has full row rank, i.e., $\operatorname{rank}(H_s(u)) = ms$. Intuitively, this means the input is sufficiently "rich" or "complex" that its time-shifted versions are [linearly independent](@entry_id:148207). The required order for the lemma, $L+n$, arises from two needs: the input must be rich enough to generate any desired input sequence of length $L$ and also to manipulate the $n$-dimensional internal state of the system into any required configuration. [@problem_id:2698753] [@problem_id:2698779]

A practical consequence of the PE rank condition is a necessary constraint on the length of the data experiment, $T$. For the matrix $H_{L+n}(u)$, which has $m(L+n)$ rows and $T-(L+n)+1$ columns, to have full row rank, the number of columns must be at least the number of rows. This yields a minimal data length requirement:
$$
T - (L+n) + 1 \ge m(L+n) \implies T \ge m(L+n) + L+n - 1 = (m+1)(L+n) - 1.
$$
This inequality provides a concrete, checkable condition on the amount of data needed to apply methods based on the fundamental lemma. [@problem_id:2698822] [@problem_id:2698753]

### From Theory to Practice: Data-Enabled Predictive Control (DeePC)

One of the most direct applications of Willems' Fundamental Lemma is in **Data-enabled Predictive Control (DeePC)**. DeePC reformulates the standard Model Predictive Control (MPC) problem in a purely data-driven way.

In a typical [predictive control](@entry_id:265552) setup, we are given a past trajectory of length $L_p$ (the "initial condition") and we want to compute an optimal future control sequence of length $L_f$ that minimizes a certain cost function. Let the total trajectory length be $L = L_p + L_f$. The core idea of DeePC is to search for a future trajectory that is consistent with the system's behavior, as captured by the data Hankel matrices.

The noiseless DeePC formulation is an optimization problem over the coefficient vector $g$. Given a past input-output trajectory $(u_p, y_p)$, we seek to find a $g$ that satisfies:
$$
\begin{pmatrix} U_p \\ Y_p \end{pmatrix} g = \begin{pmatrix} u_p \\ y_p \end{pmatrix}.
$$
This constraint enforces that the trajectory parameterized by $g$ is consistent with the observed past. Once such a $g$ is found, the corresponding future input-output trajectory is predicted as:
$$
\begin{pmatrix} u_f \\ y_f \end{pmatrix} = \begin{pmatrix} U_f \\ Y_f \end{pmatrix} g.
$$
The optimization problem is then to choose $g$ to minimize a [cost function](@entry_id:138681) $J(u_f, y_f)$ subject to the past consistency constraint and any other operational constraints on the inputs and outputs.

Under ideal, noise-free conditions, this data-driven prediction is equivalent to one made by a traditional model-based predictor. If the data used to construct the Hankel matrices is PE of order $L+n$, and the past window is long enough to uniquely determine the system state (typically $L_p \ge n$ for an observable system), then the feasible set of trajectories defined by the data is precisely the true system behavior. Consequently, the optimal trajectory found by DeePC is identical to the one found by an MPC controller using a perfect model $(A,B,C,D)$. [@problem_id:2698779]

The DeePC framework can be further contextualized by comparing it with another modern control paradigm, **System Level Synthesis (SLS)**. While DeePC is purely data-driven, SLS is a model-based method that re-parameterizes the control problem in terms of achievable closed-loop system responses. It uses the known system matrices $(A,B)$ to define an affine constraint on the space of all possible closed-loop response maps. In a remarkable theoretical convergence, under the same ideal conditions that guarantee the [exactness](@entry_id:268999) of DeePC (noiseless data, full state measurement, sufficient PE, and identical cost functions), the set of feasible trajectories described by SLS and DeePC become identical. This implies that both methods, one starting from a model and the other from data, will compute the exact same [optimal control](@entry_id:138479) sequence. [@problem_id:2698824]

### Managing Uncertainty in Data-Driven Control

The ideal, noiseless world of the fundamental lemma provides the theoretical foundation, but practical success hinges on effectively handling noise and uncertainty. When measurements are corrupted by noise, the linear consistency equations of DeePC no longer hold, as the noisy trajectory does not lie in the [column space](@entry_id:150809) of the (noise-free) data Hankel matrix. This necessitates more robust formulations.

#### Regularization in DeePC: Slack Variables and Tikhonov Terms

A powerful way to adapt DeePC for noisy data is through regularization. Two key techniques are the introduction of **[slack variables](@entry_id:268374)** and **Tikhonov regularization**.

Consider the past output consistency equation in DeePC, which now involves a noisy measurement $y_p^m$: $Y_p g = y_p^m$. To avoid infeasibility due to noise, we introduce a [slack variable](@entry_id:270695) $\sigma_y$:
$$
Y_p g + \sigma_y = y_p^m.
$$
Instead of a hard constraint, we now have a "soft" one, and we penalize the magnitude of the [slack variable](@entry_id:270695) in the [cost function](@entry_id:138681) with a term like $\lambda_\sigma \lVert \sigma_y \rVert_2^2$. This term is equivalent to adding a least-squares penalty $\lambda_\sigma \lVert y_p^m - Y_p g \rVert_2^2$ to the objective, which encourages the solution to be close to the noisy measurement without demanding an exact fit.

Additionally, to prevent [overfitting](@entry_id:139093) to the noise in both the historical data (in the Hankel matrices) and the current measurements, a **Tikhonov regularization** term $\lambda_g \lVert g \rVert_2^2$ is added to the cost. This term penalizes large coefficients in the vector $g$, promoting simpler, smoother solutions. [@problem_id:2698809]

These two regularization parameters, $\lambda_\sigma$ and $\lambda_g$, introduce a classic **[bias-variance trade-off](@entry_id:141977)**.
-   **Tikhonov Regularization ($\lambda_g$):** Increasing $\lambda_g$ shrinks the solution vector $g$ towards zero. This introduces **bias** (the expected value of the estimate moves away from the true value), but it also reduces the **variance** of the estimate by making it less sensitive to the specific noise realization in the data.
-   **Slack Variable Penalty ($\lambda_\sigma$):** The choice of $\lambda_\sigma$ balances fitting the current measurement against the other objectives. Taking $\lambda_\sigma \to \infty$ forces an exact fit to the noisy data ($y_p^m$), leading to overfitting and high variance in the predictions. Conversely, taking $\lambda_\sigma \to 0$ makes the prediction independent of the past output measurement, reducing variance from that noise source but introducing significant bias by ignoring crucial information about the current state. [@problem_id:2698809]

This regularized formulation can be interpreted from a Bayesian perspective as a **Maximum A Posteriori (MAP)** estimation problem. The Tikhonov term corresponds to a zero-mean Gaussian prior on the coefficients $g$, and the slack penalty corresponds to a Gaussian likelihood model for the [measurement noise](@entry_id:275238). From this viewpoint, the resulting estimator is known to be biased but has a smaller variance than an unregularized [least-squares solution](@entry_id:152054), providing a more robust estimate in the presence of noise. [@problem_id:2698809]

#### Set-Membership Identification with Bounded Noise

An alternative to the [stochastic noise](@entry_id:204235) model is to assume that the disturbances, while unknown, are confined to a known bounded set. This leads to the paradigm of **[set-membership identification](@entry_id:163550)**. Here, the goal is not to find a single "best" model, but to characterize the set of *all* possible models that are consistent with the observed data and the noise bounds.

For a simple ARX model like $y_k = a y_{k-1} + v_k$ with a known disturbance bound $|v_k| \le \varepsilon$, each data point $(y_{k-1}, y_k)$ constrains the unknown parameter $a$ to lie within a specific interval. The relation $v_k = y_k - a y_{k-1}$ combined with the bound gives $|y_k - a y_{k-1}| \le \varepsilon$, which defines an interval for $a$. After collecting multiple data points, the **feasible parameter set** $\mathcal{S}$ is the intersection of all such intervals. This intersection is itself an interval (or an empty set if the data is inconsistent with the assumed noise bound), providing a rigorous characterization of the [parameter uncertainty](@entry_id:753163). [@problem_id:2698786]

#### Certifying Performance: Robust vs. Probabilistic Guarantees

When controlling a system under uncertainty, providing performance guarantees is paramount. A **robust (or worst-case) guarantee** ensures that constraints are satisfied for *all* possible realizations of the uncertainty. However, such a guarantee is often impossible to provide from finite data if the true bounds of the uncertainty (e.g., the maximum possible disturbance magnitude $B^\star$) are unknown. An empirical bound $\widehat{B}_N$ estimated from $N$ samples is always an underestimate of the true bound, so a guarantee based on $\widehat{B}_N$ is not truly robust. [@problem_id:2698768]

A more practical approach is to seek **probabilistic guarantees**. Instead of proving that violations will *never* occur, we aim to prove with high confidence that the *probability* of a violation is small. This is achieved by treating constraint violations as random events and using statistical tools to bound their frequency.

For example, by running $N$ independent closed-loop experiments and observing the number of episodes with constraint violations, we can compute an empirical violation frequency $\widehat{p}_N$. Using [concentration inequalities](@entry_id:263380) like **Hoeffding's inequality**, we can derive a high-confidence upper bound on the true, unknown violation probability $p$. For a desired [confidence level](@entry_id:168001) $1-\delta$, we can state that $p$ is less than or equal to an upper bound $\overline{p}_N(\delta)$ given by:
$$
\overline{p}_N(\delta) = \widehat{p}_N + \sqrt{\frac{\ln(1/\delta)}{2N}}.
$$
This provides a rigorous, data-driven certificate of safety in a statistical sense, quantifying the trade-off between the number of experiments $N$ and the tightness of the guarantee. [@problem_id:2698768]

### Data-Driven Analysis of System Properties

Beyond [control synthesis](@entry_id:170565), data-driven methods can be used to analyze intrinsic properties of a system, such as stability or passivity, without first identifying a parametric model.

#### Testing Dissipativity from Time-Domain Data

A central concept in [system analysis](@entry_id:263805) is **[dissipativity](@entry_id:162959)**. A system is dissipative with respect to a **supply rate** $w(u,y)$ if there exists a non-negative **storage function** $V(x)$ such that the energy stored in the system does not increase more than the energy supplied to it. For a discrete-time system, this is expressed by the incremental [dissipation inequality](@entry_id:188634):
$$
V(x_{k+1}) - V(x_k) \le w(u_k, y_k).
$$
This inequality must hold for all possible transitions of the system. A powerful data-driven technique is to postulate a class of storage functions, for instance quadratic functions of the form $V(x) = x^T P x$ with $P \succeq 0$, and then use data to check if a valid $P$ exists.

If we assume a quadratic storage candidate $V(x) = p x^2$ for a scalar system where the state is measured ($y_k = x_k$), the [dissipation inequality](@entry_id:188634) becomes a [linear inequality](@entry_id:174297) in the unknown parameter $p$:
$$
p(x_{k+1}^2 - x_k^2) \le w(u_k, x_k).
$$
Each measured state transition $(u_k, x_k, x_{k+1})$ provides one such [linear inequality](@entry_id:174297). A set of these inequalities can be solved to check for the existence of a feasible $p \ge 0$. If a solution exists, the system is certified to be dissipative for that storage function class and supply rate, directly from data. [@problem_id:2698805]

#### From Time Domain to Frequency Domain: The KYP Lemma and Positive Realness

The concept of [dissipativity](@entry_id:162959) is deeply connected to frequency-domain properties via the celebrated **Kalman-Yakubovich-Popov (KYP) lemma**. A particularly important special case is **passivity**, which corresponds to [dissipativity](@entry_id:162959) with respect to the supply rate $w(u,y) = u^T y$. The KYP lemma establishes that a stable LTI system is passive if and only if its transfer matrix $G(s)$ is **positive real (PR)**. A transfer matrix is positive real if $G(j\omega) + G(j\omega)^* \succeq 0$ for all real frequencies $\omega$.

The KYP lemma provides an equivalent condition in the form of a Linear Matrix Inequality (LMI) involving the [state-space](@entry_id:177074) matrices $(A,B,C,D)$ and the storage function matrix $P$. This bridges the time-domain property (existence of a storage function) and the frequency-domain property (positive realness). [@problem_id:2698787]

This connection enables data-driven verification of these properties from frequency-domain measurements. If one has access to [frequency response](@entry_id:183149) data $G(j\omega_k)$ at a set of frequencies $\{\omega_k\}$, one can check the PR condition at these points. If the samples are from a [dense set](@entry_id:142889) on the real axis, the continuity of the rational function $G(j\omega)$ allows one to conclude that if $G(j\omega_k) + G(j\omega_k)^* \succeq 0$ at all sample points, then the property holds for all frequencies, and the system is passive. [@problem_id:2698787]

For practical scenarios with noisy measurements at a finite number of frequencies, more advanced techniques are required. Robust methods, often leveraging the **Generalized KYP (GKYP) lemma** (which extends the result to finite frequency intervals), can provide conservative but rigorous certificates of passivity by verifying the property over an entire [uncertainty set](@entry_id:634564) of models consistent with the noisy data. [@problem_id:2698787]