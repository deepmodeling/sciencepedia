## Introduction
In the age of big data, extracting meaningful patterns from complex, high-dimensional measurements is a central challenge across science and engineering. Many systems, from turbulent fluid flows to the fluctuating activity of the human brain, are governed by intricate [nonlinear dynamics](@entry_id:140844) that are difficult to model from first principles. Dynamic Mode Decomposition (DMD) emerges as a powerful, data-driven framework to address this challenge. It provides a way to decompose complex [time-series data](@entry_id:262935) into a set of [coherent structures](@entry_id:182915), or modes, each evolving with a simple, linear temporal behavior. This approach bridges the gap between purely statistical methods and physics-based modeling, offering a global, dynamic perspective that is both interpretable and predictive.

This article provides a comprehensive introduction to Dynamic Mode Decomposition, designed to equip you with both the theoretical understanding and practical skills to apply this versatile method.
First, in **Principles and Mechanisms**, we will explore the elegant mathematical foundations of DMD, connecting it to the Koopman [operator theory](@entry_id:139990) of dynamical systems and detailing the core computational algorithm. You will learn how to interpret the resulting modes and eigenvalues to diagnose stability and oscillatory behavior.
Next, in **Applications and Interdisciplinary Connections**, we will journey through a diverse landscape of real-world problems where DMD has provided critical insights, from fluid dynamics and [structural engineering](@entry_id:152273) to neuroscience and [epidemiology](@entry_id:141409).
Finally, **Hands-On Practices** will guide you through practical coding exercises, reinforcing key concepts such as dealing with measurement artifacts and ensuring the [numerical stability](@entry_id:146550) of your analysis. By the end, you will have a solid grasp of how to leverage DMD to uncover the hidden dynamics in your own data.

## Principles and Mechanisms

This chapter delves into the theoretical principles and computational mechanisms of Dynamic Mode Decomposition (DMD). We will begin by situating DMD within the broader framework of dynamical systems, connecting it to the elegant theory of the Koopman operator. Subsequently, we will detail the core DMD algorithm, explain how to interpret its output, and contrast it with related data analysis techniques.

### The Koopman Operator: A Linear Perspective on Nonlinear Dynamics

Many phenomena in science and engineering are described by nonlinear autonomous dynamical systems, which can be expressed as a set of ordinary differential equations:
$$
\frac{d\mathbf{x}}{dt} = \mathbf{f}(\mathbf{x})
$$
where $\mathbf{x}(t) \in \mathbb{R}^n$ is the state of the system at time $t$ and $\mathbf{f}$ is a generally nonlinear function. The evolution of the state from an initial condition $\mathbf{x}_0$ is described by the [flow map](@entry_id:276199) $\phi^t$, such that $\mathbf{x}(t) = \phi^t(\mathbf{x}_0)$. While the evolution of the state $\mathbf{x}$ is nonlinear, a powerful alternative perspective emerges when we shift our focus from the state itself to functions of the state, known as **[observables](@entry_id:267133)**.

An observable is any scalar- or vector-valued function $g(\mathbf{x})$ that we can measure from the system. The **Koopman operator**, denoted $\mathcal{K}^t$, describes how the values of these observables evolve in time. The action of the Koopman operator is defined by composition with the [flow map](@entry_id:276199) :
$$
(\mathcal{K}^t g)(\mathbf{x}) = g(\phi^t(\mathbf{x}))
$$
This definition means that to find the value of the evolved observable $\mathcal{K}^t g$ at a point $\mathbf{x}$, one first evolves the point $\mathbf{x}$ for a time $t$ using the nonlinear [flow map](@entry_id:276199) to get $\phi^t(\mathbf{x})$, and then evaluates the original observable $g$ at this new point.

Remarkably, the Koopman operator $\mathcal{K}^t$ is a [linear operator](@entry_id:136520), regardless of whether the underlying dynamics $\mathbf{f}(\mathbf{x})$ are linear or nonlinear. It operates on a space of functions (the space of all possible observables), which is typically infinite-dimensional. The central promise of this framework is that if we can understand the spectral properties of the linear Koopman operator, we can decompose the complex nonlinear dynamics into a superposition of simpler, exponentially evolving components.

Specifically, if $\psi_j$ is an eigenfunction of the Koopman operator with corresponding eigenvalue $\mu_j$ for a discrete time step $\Delta t$, then $\mathcal{K}^{\Delta t} \psi_j = \mu_j \psi_j$. The evolution of this special observable over [discrete time](@entry_id:637509) steps is exceptionally simple:
$$
\psi_j(\mathbf{x}_{k+1}) = \psi_j(\phi^{\Delta t}(\mathbf{x}_k)) = (\mathcal{K}^{\Delta t}\psi_j)(\mathbf{x}_k) = \mu_j \psi_j(\mathbf{x}_k)
$$
This implies that $\psi_j(\mathbf{x}_k) = \mu_j^k \psi_j(\mathbf{x}_0)$. Dynamic Mode Decomposition is, at its core, a data-driven method for finding a finite-dimensional approximation to the Koopman operator and its spectral properties.

### The Dynamic Mode Decomposition Algorithm

DMD aims to find a single linear operator that best propagates a sequence of data snapshots forward in time. Assume we have collected $m$ snapshots of our system, $\{\mathbf{x}_1, \mathbf{x}_2, \dots, \mathbf{x}_m\}$, sampled at a constant time interval $\Delta t$. We arrange this data into two matrices:
$$
X = \begin{pmatrix} |  |   | \\ \mathbf{x}_1  \mathbf{x}_2  \dots  \mathbf{x}_{m-1} \\ |  |   | \end{pmatrix}, \quad
Y = \begin{pmatrix} |  |   | \\ \mathbf{x}_2  \mathbf{x}_3  \dots  \mathbf{x}_{m} \\ |  |   | \end{pmatrix}
$$
DMD seeks a linear operator $A$ that approximates the relationship $Y \approx AX$. This operator $A$ is our finite-dimensional approximation of the true, infinite-dimensional Koopman operator $\mathcal{K}^{\Delta t}$.

A critical prerequisite is the temporal integrity of the snapshot pairs. The DMD algorithm is constructed upon the relationship between a state $\mathbf{x}_k$ and its immediate successor $\mathbf{x}_{k+1}$. If the collected snapshots are not in chronological order, they must be sorted by their time indices before forming the $X$ and $Y$ matrices. Failure to do so breaks the fundamental input-output pairing and leads to an incorrect model. For instance, if the columns of $X$ are permuted while $Y$ is left unchanged, the resulting operator will generally be incorrect, even for perfectly linear, noise-free data . Conversely, if both $X$ and $Y$ have their columns permuted in the exact same way, the [least-squares solution](@entry_id:152054) for $A$ remains unchanged, as this merely reorders the terms in the error sum being minimized .

The best-fit operator $A$ is found by solving the least-squares problem:
$$
\min_A \|Y - AX\|_F^2
$$
where $\|\cdot\|_F$ is the Frobenius norm. The solution is given by $A = YX^{\dagger}$, where $X^{\dagger}$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $X$.

For [high-dimensional systems](@entry_id:750282) where the number of [state variables](@entry_id:138790) $n$ is large, forming the $n \times n$ operator $A$ is computationally prohibitive. The standard DMD algorithm cleverly bypasses this by projecting the dynamics onto a low-dimensional subspace identified by the **Singular Value Decomposition (SVD)**. The procedure is as follows :

1.  Compute the truncated SVD of the input matrix $X$, keeping the top $r$ singular values: $X \approx U_r \Sigma_r V_r^T$. The columns of $U_r \in \mathbb{R}^{n \times r}$ are orthogonal modes (often called Proper Orthogonal Decomposition or POD modes) that form an optimal, energy-ranked basis for the data in $X$.

2.  Project the full operator $A$ onto this low-dimensional basis to obtain a reduced-order operator $\tilde{A} \in \mathbb{C}^{r \times r}$. The relationship is $\tilde{A} = U_r^T A U_r$. Substituting $A = Y V_r \Sigma_r^{-1} U_r^T$ (the pseudoinverse expressed via SVD) yields the efficiently computable form:
    $$
    \tilde{A} = U_r^T Y V_r \Sigma_r^{-1}
    $$
    This is the core computational step of DMD .

3.  Compute the [eigenvalues and eigenvectors](@entry_id:138808) of the small matrix $\tilde{A}$. The eigenvalues of $\tilde{A}$ are the **DMD eigenvalues**, which we denote as $\lambda_j$. The **DMD modes**, which are approximations to the eigenvectors of the full operator $A$, can be reconstructed from the eigenvectors of $\tilde{A}$.

### Interpreting the DMD Spectrum

The output of DMD—a set of eigenvalues $\lambda_j$ and corresponding modes $\phi_j$—provides a decomposition of the dynamics into components that each evolve with simple linear behavior. The evolution of each mode is given by $\phi_j \lambda_j^k$.

A discrete DMD eigenvalue $\lambda_j$ is a complex number whose properties encode the temporal behavior of its associated mode:

*   The **magnitude**, $|\lambda_j|$, determines the mode's growth or decay rate. If $|\lambda_j| > 1$, the mode is unstable and grows exponentially. If $|\lambda_j|  1$, the mode is stable and decays. If $|\lambda_j| = 1$, the mode persists with constant amplitude, representing a neutrally stable or purely oscillatory component .

*   The **argument** (or angle), $\arg(\lambda_j)$, determines the mode's frequency of oscillation. The phase advances by $\arg(\lambda_j)$ at each time step. A zero argument implies a non-oscillatory mode.

This decomposition is particularly powerful for separating phenomena. For instance, consider a signal composed of a decaying [sinusoid](@entry_id:274998), such as $y_k = e^{-0.2 k \Delta t} \cos(2\pi f k \Delta t)$. Classical Fourier analysis, which uses undamped sinusoids ($e^{i\omega t}$), requires a broad spectrum of frequencies to represent the [exponential decay](@entry_id:136762). In contrast, DMD is ideally suited to capture this behavior with a single pair of complex-conjugate eigenvalues, where $|\lambda|  1$ represents the decay and $\arg(\lambda)$ represents the [oscillation frequency](@entry_id:269468) .

#### From Discrete Eigenvalues to Continuous-Time Dynamics

To connect the discrete DMD eigenvalues to the underlying continuous-time system, we use the relationship $\lambda = e^{\mu \Delta t}$, where $\mu$ is an eigenvalue of the continuous-time Koopman generator $\mathcal{L}$. We can solve for $\mu$:
$$
\mu = \frac{\ln(\lambda)}{\Delta t}
$$
The real and imaginary parts of $\mu$ have direct physical interpretations:
*   **Growth/Decay Rate**: $\text{Re}(\mu) = \frac{\ln|\lambda|}{\Delta t}$. A positive real part indicates an unstable mode, while a negative real part indicates a stable, decaying mode.
*   **Angular Frequency**: $\text{Im}(\mu) = \frac{\arg(\lambda)}{\Delta t}$. This is the [oscillation frequency](@entry_id:269468) of the mode in radians per unit time.

This relationship is crucial for stability analysis. A fixed point of a dynamical system is unstable if DMD identifies any mode with $|\lambda| > 1$, which corresponds to $\text{Re}(\mu) > 0$ .

A subtlety arises because the [complex logarithm](@entry_id:174857) is multi-valued: $\ln(\lambda) = \ln|\lambda| + i(\arg(\lambda) + 2\pi k)$ for any integer $k$. This introduces an ambiguity in the continuous-time frequency:
$$
\text{Im}(\mu_k) = \frac{\arg(\lambda) + 2\pi k}{\Delta t}
$$
The imaginary part is only determined up to integer multiples of $2\pi/\Delta t$, a phenomenon known as **[aliasing](@entry_id:146322)**. The sampling process cannot distinguish between frequencies that differ by a multiple of the [sampling frequency](@entry_id:136613). The real part, however, is uniquely determined because $\ln|\lambda|$ is single-valued .

#### Canonical Example: Pure Rotation

A simple, purely [rotational motion](@entry_id:172639) provides a clear illustration of how DMD captures oscillatory behavior. Consider a point rotating in a plane, whose state is given by the vector $\mathbf{s}_k = [x_k, y_k]^T$. This is a linear system where the [evolution operator](@entry_id:182628) is a [rotation matrix](@entry_id:140302). DMD applied to this system will yield a pair of complex-conjugate eigenvalues on the unit circle, $\lambda_{1,2} = e^{\pm i\theta}$, where $\theta$ is the angle of rotation per time step . The magnitude $|\lambda|=1$ correctly identifies the motion as having zero growth or decay. The corresponding DMD modes will also be a complex-conjugate pair. Crucially, a real-valued initial state, such as a point starting on the x-axis, will excite *both* of these complex modes. The real-valued rotational motion observed in the data is the result of the superposition of these two complex-conjugate modes evolving in time .

### DMD in Context: Strengths and Limitations

The utility of DMD is best understood by comparing it to other methods and by recognizing its inherent assumptions.

#### DMD versus Local Linearization

For a [nonlinear system](@entry_id:162704) $\dot{\mathbf{x}} = \mathbf{f}(\mathbf{x})$, a classic analysis technique is [local linearization](@entry_id:169489) around a fixed point or a trajectory point $\mathbf{x}_0$. This involves approximating the dynamics using the Jacobian matrix $J(\mathbf{x}_0) = \partial \mathbf{f}/\partial \mathbf{x}|_{\mathbf{x}_0}$. This model is, by definition, only valid in a small neighborhood of $\mathbf{x}_0$.

DMD, in contrast, computes a *single* [linear operator](@entry_id:136520) from data spanning a large region of the state space. If the data captures a system's long-term behavior on an attractor, such as a limit cycle, DMD can provide a global linear model for that attractor. It can simultaneously identify the persistent oscillatory modes of the cycle (with $|\lambda| \approx 1$) and the transient modes that decay onto it (with $|\lambda|  1$). A Jacobian-based model at a single point on the cycle cannot provide this global picture . However, it is important to note that when DMD is applied to data collected from a very small neighborhood of a point $\mathbf{x}_0$, its result converges to that of [local linearization](@entry_id:169489) .

The global power of DMD for nonlinear systems is best explained by Koopman theory. DMD succeeds when the chosen observables (in standard DMD, the state variables themselves) lie within, or can be well-approximated by, a finite-dimensional subspace that is invariant under the Koopman operator. Under this condition, DMD can provide a globally valid linear model for the evolution of those [observables](@entry_id:267133) .

#### DMD versus Proper Orthogonal Decomposition (POD)

DMD is often compared to POD, especially in fields like fluid dynamics. While the DMD algorithm uses the POD modes (the columns of $U_r$) as its computational basis, the final DMD modes are fundamentally different.

*   **POD** is an energy-based decomposition. Its modes are spatially orthogonal and ranked by how much kinetic energy (or variance) they capture from the data ensemble. The temporal behavior of POD modes is complex and not guaranteed to be single-frequency.
*   **DMD** is a dynamics-based decomposition. Its modes are eigenvectors of the estimated [evolution operator](@entry_id:182628) $A$. They are generally not orthogonal but are associated with a single frequency and growth/decay rate.

This distinction is critical. Because POD prioritizes energy, it may combine distinct dynamical phenomena into a single, high-energy mode. For example, in a simulation of [vortex shedding](@entry_id:138573), a slowly decaying transient and the primary periodic shedding might be mixed within the first few POD modes. DMD is designed to separate these phenomena into distinct modes: a decaying mode with a real eigenvalue and an oscillatory mode with a complex-conjugate eigenvalue pair .

#### The Critical Role of Rank Truncation

The choice of the truncation rank $r$ in the SVD step is a crucial parameter that determines the complexity of the resulting linear model. The rank $r$ must be large enough to capture the dynamic phenomena of interest. If a system has $p$ distinct modes, but the rank is chosen such that $r  p$, DMD will be unable to resolve all $p$ modes. It will instead identify a set of $r$ modes that are often mixtures of the underlying true modes .

Furthermore, since the basis $U_r$ is ordered by energy, low-energy modes may be discarded if the rank $r$ is too small. A dynamically important but low-[amplitude mode](@entry_id:145714) might not be captured if its contribution to the total energy is below the threshold set by the truncation. Similarly, resolving modes with very closely spaced frequencies can be challenging and may require a longer data sequence (more snapshots) to ensure they are distinguishable by the algorithm .