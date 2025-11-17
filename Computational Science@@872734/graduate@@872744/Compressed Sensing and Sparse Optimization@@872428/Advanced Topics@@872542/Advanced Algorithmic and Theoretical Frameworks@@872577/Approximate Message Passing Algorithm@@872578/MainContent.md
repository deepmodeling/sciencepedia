## Introduction
The Approximate Message Passing (AMP) algorithm represents a significant breakthrough in high-dimensional signal processing and statistical inference. Emerging from the principles of [statistical physics](@entry_id:142945), it provides not only a computationally efficient method for solving [large-scale inverse problems](@entry_id:751147) like [compressed sensing](@entry_id:150278) but also an exceptionally precise theoretical framework for predicting its own performance. The central challenge AMP addresses is how to design an iterative algorithm that is both fast and analytically tractable, a combination that eludes many other methods. This article offers a comprehensive exploration of the AMP framework, bridging theory and practice to provide a graduate-level understanding of this powerful tool.

The journey through this material is structured into three main chapters. First, in **Principles and Mechanisms**, we will dissect the algorithm's iterative structure, focusing on the critical role of the Onsager reaction term and the statistical physics concepts from which it derives. We will uncover the "decoupling principle" and introduce State Evolution, the elegant theory that allows for exact macroscopic predictions of the algorithm's behavior. Next, **Applications and Interdisciplinary Connections** will demonstrate the versatility of the AMP framework, showing how it serves as a precise analytical tool for characterizing mainstream methods like LASSO, adapts to complex [generalized linear models](@entry_id:171019), and connects to frontiers in machine learning and deep learning. Finally, **Hands-On Practices** will provide a series of guided problems to solidify your understanding, taking you from deriving the Onsager term to stabilizing the algorithm for practical use.

## Principles and Mechanisms

This chapter delves into the theoretical underpinnings of the Approximate Message Passing (AMP) algorithm. We will dissect its core iterative structure, uncover the statistical mechanics principles that grant it extraordinary analytical tractability, and formalize the mechanism—State Evolution—that allows for a precise, macroscopic prediction of its performance. We will explore the conditions under which this theory holds, its limitations, and the conceptual extensions that broaden its applicability.

### The AMP Iteration and the Onsager Correction

The Approximate Message Passing algorithm is designed to solve [linear inverse problems](@entry_id:751313) of the form $y = Ax_0 + w$, where $y \in \mathbb{R}^m$ is a vector of measurements, $A \in \mathbb{R}^{m \times n}$ is a known sensing matrix, $x_0 \in \mathbb{R}^n$ is the unknown signal to be recovered, and $w \in \mathbb{R}^m$ represents measurement noise. The canonical setting for AMP assumes a large, random sensing matrix $A$ with independent and identically distributed (i.i.d.) entries, typically drawn from a Gaussian distribution $\mathcal{N}(0, 1/m)$. [@problem_id:3432098]

The AMP algorithm is an iterative procedure that refines an estimate of the signal, $x^t$, at each iteration $t$. A typical form of the algorithm is given by the following two updates:

1.  **Signal Estimate Update:** The new signal estimate, $x^{t+1}$, is obtained by applying a component-wise **[denoising](@entry_id:165626) function** $\eta_t : \mathbb{R}^n \to \mathbb{R}^n$ to an effective observation vector $r^t$:
    $$
    x^{t+1} = \eta_t(r^t) \quad \text{where} \quad r^t = x^t + A^\top z^t
    $$
    Here, $z^t$ is a "working residual" vector from the previous iteration.

2.  **Residual Update:** The residual for the next iteration, $z^{t+1}$, is formed by subtracting the effect of the new estimate from the measurements, with a crucial additional term:
    $$
    z^{t+1} = y - Ax^{t+1} + b_t z^t
    $$

The term $b_t z^t$ is the celebrated **Onsager reaction term**, and it is the key feature that distinguishes AMP from simpler [iterative methods](@entry_id:139472) like the Iterative Soft-Thresholding Algorithm (ISTA). The coefficient $b_t$ is not an arbitrary damping factor; it is a precisely defined quantity that depends on the average derivative of the [denoising](@entry_id:165626) function $\eta_t$ used to compute $x^{t+1}$. This term acts as a memory, carrying forward a scaled version of the previous residual.

The profound role of the Onsager term is to cancel statistical correlations that inevitably build up between the iterates and the matrix $A$. In a [dense graph](@entry_id:634853) where every component of the estimate influences every component of the residual, and vice-versa through the action of $A$ and $A^\top$, feedback loops are ubiquitous. The Onsager term functions as a sophisticated bias correction, removing the "self-interaction" effect that would otherwise contaminate the statistics of the algorithm and hinder its convergence. This correction is not a minor tweak; it fundamentally alters the dynamics of the iteration, leading to a remarkable simplification of its behavior in the high-dimensional limit. [@problem_id:3432160]

### The Statistical Physics Connection: From Belief Propagation to AMP

The structure of the AMP algorithm, and particularly the Onsager term, did not arise in a vacuum. It can be rigorously derived from the principles of **loopy [belief propagation](@entry_id:138888) (BP)** applied to the graphical model representing the inference problem. [@problem_id:3432160] In this graphical model, variable nodes correspond to the signal components $\{x_i\}$ and factor nodes correspond to the measurement constraints $\{y_a\}$. When the matrix $A$ is dense, this graph is densely connected, and BP messages circulate in many short loops.

The derivation of AMP from BP relies on a crucial approximation valid in the large-system limit ($m, n \to \infty$ with $m/n \to \delta$). The message passed from a factor node to a variable node involves a sum over many other variables, weighted by the random matrix entries $A_{ai}$. By an appeal to the **Central Limit Theorem (CLT)**, the distribution of this sum is approximated as a Gaussian. This simplifies the [message-passing](@entry_id:751915) updates, reducing them from manipulations of entire distributions to calculations involving only the first two moments (mean and variance). The higher-order [cumulants](@entry_id:152982) of the messages are among the terms discarded in this heuristic derivation. [@problem_id:3432160]

This mean-field-like approximation, however, is subtly inaccurate. The Onsager term emerges precisely as the correction needed to account for the response of the system to a local perturbation. A naive mean-field treatment would neglect terms of order $\mathcal{O}(1/n)$ that describe how a variable $x_i$ influences itself through the network. In the [dense graph](@entry_id:634853) of AMP, a variable is connected to $\mathcal{O}(m)$ factor nodes. The aggregation of these $\mathcal{O}(m) = \mathcal{O}(n)$ small feedback terms results in a macroscopic effect of order $\mathcal{O}(1)$, which cannot be ignored. The Onsager term is exactly this aggregate correction. [@problem_id:3432160]

This concept has a deep parallel in statistical physics, specifically in the study of spin glasses. The **Thouless-Anderson-Palmer (TAP) equations** provide a more accurate mean-field description of the Sherrington-Kirkpatrick model than a naive approach. They include a "reaction term" that corrects for a spin's influence on its own local field. The AMP Onsager term is the direct analogue of the TAP reaction term, both serving to correct for self-interaction in a dense, random system. [@problem_id:3432107]

### The Decoupling Principle and Denoising-based AMP (D-AMP)

The true power of the Onsager correction is revealed in its consequences. By meticulously canceling the problematic correlations, it causes the algorithm's behavior to decouple. In the high-dimensional limit, the complex $n$-dimensional vector $r^t = x^t + A^\top z^t$ that serves as the input to the denoiser behaves statistically as if it were generated by a simple, scalar Additive White Gaussian Noise (AWGN) channel:
$$
r^t_i \approx x_{0,i} + \mathcal{N}(0, \tau_t^2)
$$
for each component $i=1, \dots, n$. Here, $x_{0,i}$ is the true signal component, and $\tau_t^2$ is the variance of an effective Gaussian noise that is statistically independent of the signal $x_0$. [@problem_id:3432122]

This **[decoupling](@entry_id:160890) principle** is a cornerstone of modern AMP theory. It implies that at each iteration, the sophisticated high-dimensional estimation problem is transformed into $n$ parallel, independent scalar denoising problems. The goal of the function $\eta_t$ is simply to estimate a signal component $x_{0,i}$ from its noisy observation $r^t_i$.

This insight gives rise to the **Denoising-based AMP (D-AMP)** framework. Since the effective channel is always AWGN, one can use *any* effective AWGN denoiser for the function $\eta_t$. This "plug-and-play" capability is a major advantage. Instead of being restricted to denoisers derived from a specific, assumed signal prior, one can employ powerful, state-of-the-art denoisers developed for [image processing](@entry_id:276975) or other domains (e.g., BM3D), without even needing an explicit probabilistic model for the signal $x_0$. The only information the denoiser needs is the effective noise level $\tau_t$ at the current iteration. [@problem_id:3432122]

It is crucial to recognize that this effective Gaussian noise is not merely an inheritance of the [measurement noise](@entry_id:275238) $w$. It is a dynamic quantity arising from the complex interplay of the signal, the random matrix $A$, and the iterates. The Gaussianity is a consequence of a CLT-like effect on large sums involving the random entries of $A$, an effect that is made precise and tractable only by the presence of the Onsager term. The decoupling holds even in the noiseless measurement case ($w=0$). [@problem_id:3432122]

### State Evolution: A Predictive Theory of Performance

If the algorithm's behavior simplifies to a scalar AWGN channel at each step, can we predict the evolution of the effective noise level $\tau_t$? The answer is yes, and the predictive tool is called **State Evolution (SE)**.

State Evolution is a set of deterministic, scalar recursions that precisely track the macroscopic properties of the AMP iterates in the high-dimensional limit. The most important of these is the [recursion](@entry_id:264696) for the effective noise variance, $\tau_t^2$. For the model $y = Ax_0+w$ with i.i.d. $A_{ij} \sim \mathcal{N}(0, 1/m)$ and i.i.d. signal components $X_0$, the SE [recursion](@entry_id:264696) is:
$$
\tau_{t+1}^2 = \sigma_w^2 + \frac{1}{\delta} \mathbb{E} \left[ (\eta_t(X_0 + \tau_t Z) - X_0)^2 \right]
$$
where $\sigma_w^2$ is the variance of the measurement noise, $\delta=m/n$ is the measurement ratio, $Z \sim \mathcal{N}(0,1)$ is a standard normal variable independent of $X_0$, and the expectation is taken over the distributions of the signal $X_0$ and the noise $Z$. The term inside the expectation is simply the [mean squared error](@entry_id:276542) (MSE) of the chosen denoiser $\eta_t$ when applied to the effective scalar channel with noise variance $\tau_t^2$. Thus, SE provides a deterministic map from the MSE at one iteration to the effective noise variance of the next. The predicted MSE itself is given by this scalar expectation.

State Evolution is a powerful analytical tool. It allows us to:

*   **Predict Performance:** Before running a single simulation, we can iterate the scalar SE equations to predict the final MSE that AMP will achieve for a given problem setup (signal prior, noise level, measurement rate). [@problem_id:3432119]

*   **Analyze Phase Transitions:** We can treat the SE [recursion](@entry_id:264696) as a one-dimensional discrete dynamical system and study its fixed points. The stability of these fixed points determines the algorithm's behavior. For instance, in noiseless [compressed sensing](@entry_id:150278) of a sparse signal with sparsity $\rho$, one can analyze the stability of the zero-error fixed point. The critical measurement rate $\delta_c$ at which this fixed point becomes unstable corresponds to a phase transition in [signal recovery](@entry_id:185977). A calculation shows this transition occurs precisely at $\delta_c = \rho$, a fundamental result in [compressed sensing](@entry_id:150278) theory. [@problem_id:3432143]

*   **Quantify Model Mismatch:** SE can be used to analyze the effect of using an incorrect assumption about the signal or noise. For example, if the true signal components are Gaussian, $X \sim \mathcal{N}(0,1)$, but the algorithm uses a mismatched linear denoiser $\eta(u)=u$, SE can calculate the resulting fixed-point MSE. By comparing this to the MSE of the Bayes-optimal denoiser, one can precisely quantify the performance degradation due to the model mismatch. [@problem_id:3432155]

When the denoiser $\eta_t$ is chosen to be the Bayes-optimal one for the true signal prior (i.e., the [posterior mean](@entry_id:173826) estimator), the analysis is particularly elegant. In this case, the system is said to satisfy the **Nishimori condition**, and the State Evolution predictions become exact in the high-dimensional limit. [@problem_id:3432107]

### The Denoiser: Properties and Requirements

The denoising function $\eta$ is a critical component of the AMP algorithm. As established by the D-AMP framework, its primary role is to perform estimation in a scalar AWGN channel. The choice of denoiser encodes our prior knowledge about the signal's structure. For a sparse signal, a common choice is the **[soft-thresholding](@entry_id:635249)** function, $\eta(u; \theta) = \operatorname{sgn}(u) \max(|u|-\theta, 0)$, which promotes sparsity by setting small values to zero.

The Onsager correction term $b_t z^t$ depends on the coefficient $b_t$, which is related to the average derivative of the denoiser. For a general, non-separable denoiser, this would involve the trace of its Jacobian matrix. For a separable denoiser $\eta(r) = (\eta_1(r_1), \dots, \eta_n(r_n))$, the Jacobian is diagonal, and the relevant quantity simplifies to the normalized trace, which is called the **divergence**:
$$
\operatorname{div}(\eta)(r) = \frac{1}{n} \operatorname{tr}(J_\eta(r)) = \frac{1}{n} \sum_{i=1}^n \frac{d\eta_i}{dr_i}(r_i)
$$
The Onsager coefficient is then $b_t = \frac{1}{\delta} \operatorname{div}(\eta_t)$, where $\delta = m/n$ is the measurement ratio. [@problem_id:3432094]

A key theoretical question is what conditions the denoiser must satisfy for the SE theory to hold. Must it be differentiable everywhere? The answer is no. Many useful denoisers, including [soft-thresholding](@entry_id:635249), are not differentiable at all points. The theory requires a weaker condition: that the denoiser components $\eta_i$ be **locally Lipschitz continuous**. By Rademacher's theorem, this guarantees that they are [differentiable almost everywhere](@entry_id:160094), which is sufficient for the divergence to be well-defined and for the high-dimensional limiting arguments to hold. [@problem_id:3432094]

Conversely, if the denoiser is not even Lipschitz, the algorithm can behave erratically and diverge. For instance, if one uses the non-Lipschitz denoiser $\eta(u) = u^2$ to recover a zero signal from zero measurements, the SE [recursion](@entry_id:264696) for the effective noise variance becomes $\tau_{t+1}^2 = (3/\delta) \tau_t^4$. For any non-zero initialization $\tau_0 > 0$, this [recursion](@entry_id:264696) shows that $\tau_t$ grows doubly-exponentially, indicating a catastrophic failure of the algorithm. This provides a clear illustration of the necessity of regularity conditions on the denoiser. [@problem_id:3432142]

### Universality, Limitations, and Extensions

The theoretical framework of AMP and SE is powerful, but it is essential to understand its scope and limitations.

#### Probabilistic vs. Deterministic Guarantees

The guarantees provided by AMP theory are fundamentally different from those associated with methods based on the **Restricted Isometry Property (RIP)**. RIP is a deterministic property of a *fixed* matrix $A$. If a matrix satisfies RIP, it provides a uniform, worst-case guarantee for the recovery of all signals within a certain class (e.g., all $k$-[sparse signals](@entry_id:755125)). In contrast, the AMP framework is probabilistic. It makes predictions about the *average-case* performance for a problem instance drawn randomly from a given [statistical ensemble](@entry_id:145292) (of matrices $A$ and signals $x_0$). The results are asymptotic, holding with high probability for large systems, but they are not uniform guarantees for any finite-dimensional matrix. [@problem_id:3432098]

#### Universality of the Matrix Ensemble

A remarkable property of AMP is its **universality**. The State Evolution predictions are not limited to Gaussian matrices. They hold for a wide class of random matrix ensembles where the entries are i.i.d., have [zero mean](@entry_id:271600), a fixed variance (e.g., $1/m$), and finite higher moments. For example, AMP performs identically, and SE tracks its MSE equally well, whether the matrix entries are Gaussian or Rademacher ($\pm 1/\sqrt{m}$). However, this universality has limits. If the matrix entries are drawn from a [heavy-tailed distribution](@entry_id:145815) with infinite fourth moment (e.g., a Student-t distribution with 3 degrees of freedom), the standard SE predictions fail to track the algorithm's performance. The assumptions underlying the CLT-like arguments break down. Interestingly, practical modifications like normalizing the columns of the matrix can sometimes restore the algorithm's good behavior. [@problem_id:3432119]

#### Limitations for Structured Matrices and Extensions

The classic AMP derivation relies heavily on the i.i.d. structure of the matrix $A$. The algorithm is known to fail for many deterministic or [structured matrices](@entry_id:635736), even those that are good for [compressed sensing](@entry_id:150278), such as subsampled Fourier or Hadamard matrices. The specific correlation structure of these matrices is not canceled by the standard scalar Onsager term, leading to divergence.

This limitation motivated the development of more advanced algorithms. The core issue for non-i.i.d. matrices, such as general **right-rotationally invariant (RRI)** matrices (of the form $A = USV^\top$ with Haar-random $U, V$), is that the linear mixing step involves the matrix $A^\top A$, which has a non-trivial spectral structure. To handle this, the algorithmic structure must be adapted.

*   **Vector AMP (VAMP)** tackles this by splitting the iteration into two distinct modules: a non-linear [denoising](@entry_id:165626) module that only sees a scalar channel, and a linear estimation module that handles the interaction with the matrix $A$ via LMMSE estimation. The "Onsager correction" is implicitly handled by the protocol for exchanging extrinsic information between these modules, and its parameters can be computed from the singular value spectrum of $A$.

*   **Orthogonal AMP (OAMP)** takes a different route, modifying the denoiser to be "divergence-free" or modifying the linear estimation step to be decorrelating. This can cause the explicit Onsager memory term to vanish, while the necessary decorrelation is guaranteed by the orthogonality properties of the RRI matrix ensemble.

These extensions, VAMP and OAMP, generalize the principles of AMP to a much broader class of sensing matrices, significantly expanding the practical reach of [message-passing](@entry_id:751915) algorithms in signal processing and machine learning. [@problem_id:3432133]