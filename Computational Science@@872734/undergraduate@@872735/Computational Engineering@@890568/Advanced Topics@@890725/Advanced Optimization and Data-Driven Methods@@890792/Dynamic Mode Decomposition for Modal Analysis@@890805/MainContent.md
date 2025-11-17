## Introduction
In an age where vast amounts of data are generated from simulations and experiments, the challenge lies in extracting simple, [interpretable models](@entry_id:637962) that describe the underlying dynamics of complex systems. From the [turbulent flow](@entry_id:151300) of a fluid to the firing of neurons in the brain, understanding the essential patterns of behavior is key to prediction, analysis, and control. Dynamic Mode Decomposition (DMD) has emerged as a powerful, equation-free technique that rises to this challenge. It provides a systematic way to decompose a complex, high-dimensional time series into a set of coherent spatiotemporal structures, each with a distinct frequency and growth or decay rate.

This article provides a comprehensive overview of Dynamic Mode Decomposition, designed to build your understanding from the ground up. We will explore how DMD bridges the gap between raw data and physical insight. The journey is structured into three main parts:
*   **Principles and Mechanisms:** We will first delve into the mathematical foundations of DMD, exploring how it finds the best-fit linear system for your data and how to interpret the resulting modes and eigenvalues.
*   **Applications and Interdisciplinary Connections:** Next, we will showcase the remarkable versatility of DMD by examining its use across a wide array of fields, including engineering, physics, life sciences, and even socio-economic systems.
*   **Hands-On Practices:** Finally, we will solidify your knowledge through a series of conceptual exercises that highlight key practical aspects, such as parameter selection and the critical interpretation of results.

We begin by deconstructing the core principles of the method, establishing the firm theoretical footing upon which all its powerful applications are built.

## Principles and Mechanisms

This chapter delineates the foundational principles and core mechanisms of Dynamic Mode Decomposition (DMD). We will deconstruct the method from its conceptual origins as a linear system approximation to its practical implementation via spectral analysis of a data-driven operator. The objective is to provide a rigorous understanding of what DMD modes and eigenvalues represent, how they connect to the underlying continuous-time physics of a system, and what fundamental limitations and interpretational challenges must be considered in its application.

### The Best-Fit Linear Dynamical System

At its core, Dynamic Mode Decomposition is a data-driven method for finding a linear dynamical system that best approximates an observed process. Consider a system whose state is described by a vector $\boldsymbol{x}(t) \in \mathbb{R}^n$ evolving in continuous time. If we collect a sequence of measurements, or **snapshots**, of this state at discrete, uniformly spaced time intervals $t_k = k\Delta t$, we obtain a time series $\boldsymbol{x}_0, \boldsymbol{x}_1, \boldsymbol{x}_2, \dots, \boldsymbol{x}_m$.

The central hypothesis of DMD is that there exists a constant matrix $\boldsymbol{A} \in \mathbb{C}^{n \times n}$ that approximately propagates the state vector from one snapshot to the next:
$$
\boldsymbol{x}_{k+1} \approx \boldsymbol{A} \boldsymbol{x}_k
$$
This assumes that the dynamics, which may be nonlinear and complex, can be reasonably modeled by a linear evolution over the time step $\Delta t$. The matrix $\boldsymbol{A}$ is often referred to as the **[propagator](@entry_id:139558)** or **Koopman operator** approximation.

To find the optimal operator $\boldsymbol{A}$ from the data, we arrange the snapshots into two matrices:
$$
\boldsymbol{X} = \begin{bmatrix} |  |   | \\ \boldsymbol{x}_0  \boldsymbol{x}_1  \cdots  \boldsymbol{x}_{m-1} \\ |  |   | \end{bmatrix}
$$
$$
\boldsymbol{X}' = \begin{bmatrix} |  |   | \\ \boldsymbol{x}_1  \boldsymbol{x}_2  \cdots  \boldsymbol{x}_{m} \\ |  |   | \end{bmatrix}
$$
The relationship $\boldsymbol{x}_{k+1} \approx \boldsymbol{A} \boldsymbol{x}_k$ can then be written for the entire dataset as $\boldsymbol{X}' \approx \boldsymbol{A} \boldsymbol{X}$. DMD seeks the operator $\boldsymbol{A}$ that minimizes the Frobenius norm of the residual, $\| \boldsymbol{X}' - \boldsymbol{A} \boldsymbol{X} \|_F$. The solution to this linear [least-squares problem](@entry_id:164198) is given by:
$$
\boldsymbol{A} = \boldsymbol{X}' \boldsymbol{X}^{\dagger}
$$
where $\boldsymbol{X}^{\dagger}$ is the Moore-Penrose pseudoinverse of $\boldsymbol{X}$. While this provides a formal definition, direct computation of the (potentially very large) matrix $\boldsymbol{A}$ is rarely performed in practice, as we will discuss later. The true power of the method lies not in the matrix $\boldsymbol{A}$ itself, but in its spectral properties.

### Spectral Decomposition: DMD Modes and Eigenvalues

The linear system defined by $\boldsymbol{A}$ can be fully understood by examining its eigenvalues and eigenvectors (its spectrum). The eigenvectors of $\boldsymbol{A}$ are known as the **DMD modes**, denoted by $\boldsymbol{\phi}_i$, and the corresponding eigenvalues are the **DMD eigenvalues**, denoted by $\lambda_i$. These quantities satisfy the [characteristic equation](@entry_id:149057):
$$
\boldsymbol{A} \boldsymbol{\phi}_i = \lambda_i \boldsymbol{\phi}_i
$$
Any [state vector](@entry_id:154607) $\boldsymbol{x}_k$ can be expressed as a [linear combination](@entry_id:155091) of these DMD modes. The evolution of the system is then described by the evolution of the mode amplitudes. If the initial state $\boldsymbol{x}_0$ is decomposed as $\boldsymbol{x}_0 = \sum_{i} b_i \boldsymbol{\phi}_i$, where $b_i$ are the mode amplitudes, then the state at a future time step $k$ is given by:
$$
\boldsymbol{x}_k = \boldsymbol{A}^k \boldsymbol{x}_0 = \boldsymbol{A}^k \sum_{i} b_i \boldsymbol{\phi}_i = \sum_{i} b_i (\boldsymbol{A}^k \boldsymbol{\phi}_i) = \sum_{i} b_i \lambda_i^k \boldsymbol{\phi}_i
$$
This equation is the cornerstone of DMD. It reveals that the dynamics are decomposed into a set of coherent spatial structures (the DMD modes $\boldsymbol{\phi}_i$) each evolving with simple, uncoupled temporal dynamics (the powers of the DMD eigenvalues $\lambda_i^k$).

#### Interpreting DMD Eigenvalues: Temporal Dynamics

The value of a complex eigenvalue $\lambda_i$ directly encodes the temporal behavior of its corresponding mode $\boldsymbol{\phi}_i$. An eigenvalue $\lambda_i$ can be expressed in [polar form](@entry_id:168412) as $\lambda_i = |\lambda_i| e^{i\theta_i}$, where $|\lambda_i|$ is its magnitude and $\theta_i = \arg(\lambda_i)$ is its argument (angle). The term $\lambda_i^k$ becomes $|\lambda_i|^k e^{ik\theta_i}$.

The **magnitude $|\lambda_i|$** determines the growth or decay rate of the mode's amplitude over time.
- If **$|\lambda_i|  1$**, the mode is **stable** and decays exponentially. The term $|\lambda_i|^k \to 0$ as $k \to \infty$.
- If **$|\lambda_i| = 1$**, the mode is **persistent** or **neutrally stable**. Its amplitude neither grows nor decays.
- If **$|\lambda_i| > 1$**, the mode is **unstable** and grows exponentially. The term $|\lambda_i|^k \to \infty$ as $k \to \infty$.

The **argument $\arg(\lambda_i)$** determines the oscillatory frequency of the mode. The term $e^{ik\theta_i}$ represents a rotation in the complex plane at each time step, corresponding to an oscillation with a discrete [angular frequency](@entry_id:274516) of $\theta_i$ radians per time step.

A canonical example is the analysis of a pure rotation ([@problem_id:2387354]). For a point rotating in a plane with a constant angular velocity, the DMD operator is exactly a [rotation matrix](@entry_id:140302). The eigenvalues of this matrix are a complex-conjugate pair, $\lambda_{1,2} = e^{\pm i\theta}$, where $\theta$ is the angle of rotation per time step. The magnitude is $|\lambda| = |e^{\pm i\theta}| = 1$, correctly identifying the motion as persistent (norm-conserving). The argument $\pm\theta$ directly gives the frequency of oscillation. Because real-valued data (such as physical positions) must be represented, the dynamics are formed by a superposition of this conjugate pair of modes, ensuring the result is real.

This framework allows for the stability analysis of a fixed point. If DMD is applied to small perturbations around a fixed point, the resulting eigenvalues determine its stability ([@problem_id:2387419]). The presence of any eigenvalue with magnitude greater than one, $|\lambda_i| > 1$, signifies that the fixed point is unstable, as at least one mode will grow over time. Asymptotic stability requires all eigenvalues to lie strictly inside the unit circle, $|\lambda_i|  1$.

#### Interpreting DMD Modes: Spatial Structures

Each DMD mode $\boldsymbol{\phi}_i$ is a vector in the state space that represents a coherent spatial pattern. This pattern oscillates and grows or decays according to its associated eigenvalue $\lambda_i$. For spatially [distributed systems](@entry_id:268208), such as fluid flows or wave phenomena, the DMD modes often correspond to recognizable physical structures.

For instance, when analyzing a traveling wave of the form $u(x,t) = \exp(i(kx - \omega t))$, DMD correctly identifies the underlying structure ([@problem_id:2387345]). The analysis yields a single dominant eigenvalue $\lambda = \exp(-i\omega\Delta t)$, which captures the temporal oscillation. The corresponding DMD mode $\boldsymbol{\phi}$ is a vector whose elements are samples of the spatial part of the wave, $\exp(ikx)$. By performing a Fourier Transform on this DMD mode, one can extract the spatial wavenumber $k$. This demonstrates how DMD cleanly separates the temporal evolution (in the eigenvalue) from the spatial structure (in the mode).

### From Discrete to Continuous-Time Eigenvalues

While DMD directly computes discrete-time eigenvalues $\lambda_i$ associated with the sampling interval $\Delta t$, many physical systems are governed by continuous-time differential equations. We can relate the discrete-time operator $\boldsymbol{A}$ to an underlying continuous-time operator $\boldsymbol{L}$ via the matrix exponential: $\boldsymbol{A} = \exp(\boldsymbol{L}\Delta t)$. The eigenvalues are similarly related:
$$
\lambda_i = e^{\mu_i \Delta t}
$$
where $\mu_i$ is the continuous-time eigenvalue associated with the $i$-th mode. We can solve for $\mu_i$:
$$
\mu_i = \frac{1}{\Delta t} \ln(\lambda_i)
$$
The complex value $\mu_i$ provides a direct link to the parameters of the governing physical equations. Writing $\mu_i$ in Cartesian form, $\mu_i = \sigma_i + i\omega_i$, we can interpret its components:
-   **$\sigma_i = \text{Re}(\mu_i) = \frac{\ln|\lambda_i|}{\Delta t}$** is the continuous-time **growth/decay rate**. If $\sigma_i  0$, the mode decays; if $\sigma_i > 0$, it grows.
-   **$\omega_i = \text{Im}(\mu_i) = \frac{\arg(\lambda_i)}{\Delta t}$** is the continuous-time **angular frequency**.

This connection is exceptionally powerful for system identification. Consider the one-dimensional [advection-diffusion equation](@entry_id:144002), $\frac{\partial u}{\partial t} + c \frac{\partial u}{\partial x} = \nu \frac{\partial^2 u}{\partial x^2}$ ([@problem_id:2387344]). For a single Fourier mode initial condition, $u(x,0) = \exp(imx)$, the solution evolves with a continuous-time eigenvalue $\mu = -\nu m^2 - i c m$. The real part, $-\nu m^2$, is governed by diffusion (a dissipative, decaying process), and the imaginary part, $-cm$, is governed by advection (a propagating, oscillatory process). By computing the DMD eigenvalue $\lambda$ from snapshot data of this system and converting it to the continuous-time eigenvalue $\mu = (\ln\lambda)/\Delta t$, we can estimate the physical parameters. The real part of $\mu$ reveals the diffusion coefficient $\nu$, and the imaginary part reveals the advection speed $c$.

### Fundamental Properties and Limitations

#### Connection to Physical Conservation Laws

DMD can reflect fundamental physical principles of the underlying system. For **Hamiltonian systems**, which conserve energy, the dynamics are constrained. For linear Hamiltonian systems, this conservation implies that the [propagator matrix](@entry_id:753816) $\boldsymbol{A}$ is **symplectic**. A key property of [symplectic matrices](@entry_id:193807) is that if $\lambda$ is an eigenvalue, then so are $\lambda^*$, $1/\lambda$, and $1/\lambda^*$. For a stable system where modes do not grow or decay, this forces the eigenvalues to lie on the unit circle in the complex plane, $|\lambda_i| = 1$. When applying DMD to data from an uncoupled, undamped harmonic oscillator (a simple Hamiltonian system), the resulting DMD eigenvalues will lie on the unit circle to within [numerical precision](@entry_id:173145), correctly reflecting the [conservation of energy](@entry_id:140514) ([@problem_id:2387348]).

#### Aliasing and Logarithmic Ambiguity

A critical limitation of DMD, inherited from the nature of discrete sampling, is **[temporal aliasing](@entry_id:272888)**. According to the Nyquist-Shannon [sampling theorem](@entry_id:262499), to unambiguously resolve a frequency $\omega$, one must sample at a rate greater than $2\omega$, or with a time step $\Delta t  \pi/\omega$. The highest frequency that can be resolved is the **Nyquist frequency**, $\omega_{Nyq} = \pi/\Delta t$.

If a system contains a mode with a true frequency $\omega_{true} > \omega_{Nyq}$, DMD will not be able to distinguish it from a lower frequency "alias" within the principal frequency band $(-\omega_{Nyq}, \omega_{Nyq}]$ ([@problem_id:2387412]).

This phenomenon is a direct consequence of the multivalued nature of the [complex logarithm](@entry_id:174857) used to find the continuous-time eigenvalue $\mu = \frac{1}{\Delta t}\ln(\lambda)$ ([@problem_id:2387404]). The logarithm is defined up to an integer multiple of $2\pi i$:
$$
\ln(\lambda) = \ln|\lambda| + i(\arg(\lambda) + 2\pi k), \quad k \in \mathbb{Z}
$$
This means there is an infinite family of possible continuous-time eigenvalues $\mu_k$ that all map to the same discrete-time eigenvalue $\lambda$:
$$
\mu_k = \frac{\ln|\lambda|}{\Delta t} + i \left( \frac{\arg(\lambda)}{\Delta t} + k \frac{2\pi}{\Delta t} \right)
$$
The real part (growth/decay rate) is uniquely determined. However, the imaginary part (frequency) is ambiguous up to integer multiples of $2\pi/\Delta t$. DMD, by convention, returns the [principal value](@entry_id:192761) (corresponding to $k=0$), which is the frequency lying in the Nyquist band. Without prior knowledge of the system, it is impossible to know if this is the true frequency or an alias of a higher one.

### Practical Implementation and Interpretation

#### The Role of SVD and Rank Truncation

In practice, the state dimension $n$ can be very large, making the computation of $\boldsymbol{A} = \boldsymbol{X}'\boldsymbol{X}^{\dagger}$ infeasible. The standard DMD algorithm circumvents this by using the **Singular Value Decomposition (SVD)**. The data matrix $\boldsymbol{X}$ is decomposed as $\boldsymbol{X} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^*$, where $\boldsymbol{U}$ and $\boldsymbol{V}$ have orthonormal columns and $\boldsymbol{\Sigma}$ is a [diagonal matrix](@entry_id:637782) of singular values.

The columns of $\boldsymbol{U}$ (the "POD modes") form an optimal low-rank basis for the data. The algorithm projects the full operator $\boldsymbol{A}$ onto this low-rank basis, resulting in a much smaller operator $\tilde{\boldsymbol{A}} \in \mathbb{C}^{r \times r}$, where $r$ is the chosen rank of the approximation:
$$
\tilde{\boldsymbol{A}} = \boldsymbol{U}_r^* \boldsymbol{A} \boldsymbol{U}_r = \boldsymbol{U}_r^* \boldsymbol{X}' \boldsymbol{V}_r \boldsymbol{\Sigma}_r^{-1}
$$
Here, the subscript $r$ denotes truncation to the first $r$ components. The eigenvalues of this small matrix $\tilde{\boldsymbol{A}}$ are the DMD eigenvalues.

The choice of the truncation rank $r$ is a critical user decision ([@problem_id:2387367]). If $r$ is chosen to be too low, distinct physical modes may be merged into a single DMD mode, or low-energy modes may be discarded entirely. This is particularly problematic for systems with closely spaced frequencies, which require a higher rank to resolve. If $r$ is chosen to be too high, the algorithm may fit noise in the data, leading to spurious modes. The optimal choice of $r$ often involves analyzing the decay of the singular values in $\boldsymbol{\Sigma}$ to separate the energy-dominant components from the noise floor.

#### DMD for System Identification

DMD's formulation as a [system identification](@entry_id:201290) tool gives it a key advantage over traditional [spectral analysis](@entry_id:143718) methods like the Fast Fourier Transform (FFT). An FFT decomposes a signal into a fixed basis of orthogonal sinusoids. This is effective if the underlying modes are indeed sinusoidal and orthogonal. However, if the data is a mixture of non-orthogonal, coupled modes, an FFT applied to a single measurement channel may fail to separate them, especially if the time series is short or the frequencies are close ([@problem_id:2387370]).

DMD, by contrast, does not assume a fixed basis. It learns the [optimal basis](@entry_id:752971) (the DMD modes) directly from the data. By analyzing the entire multi-channel state vector simultaneously, DMD can de-mix and correctly identify the frequencies and spatial forms of the underlying modes, even when they are non-orthogonal.

#### A Caution on Interpretation: Stochastic Processes

Finally, a crucial point of caution is required. DMD is fundamentally a [linear regression](@entry_id:142318) algorithm. It will find the best-fit linear model for *any* dataset provided, even one generated by a purely stochastic process with no underlying deterministic dynamics ([@problem_id:2387414]).

If DMD is applied to a random walk, for example, it will produce a set of modes and eigenvalues. The eigenvalues will tend to cluster near $\lambda=1$ on the real axis, correctly identifying the "memory" in the integrated noise process. The DMD modes will tend to align with the directions of highest variance in the data (the principal components of the noise). However, it would be a profound error to interpret these as physically meaningful dynamic modes. They are merely statistical artifacts of the random forcing. This highlights the importance of user expertise: DMD is a powerful tool for analyzing systems believed to contain [coherent structures](@entry_id:182915), but its results must be interpreted with a critical understanding of the underlying physics and the nature of the data.