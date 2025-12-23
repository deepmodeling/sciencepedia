## Introduction
Analyzing the complex, evolving patterns within thermal flow fields presents a significant challenge for engineers and scientists. The vast datasets from high-fidelity simulations and experiments often hide the underlying physical mechanisms within a sea of information. Dynamic Mode Decomposition (DMD) has emerged as a transformative, data-driven technique to address this challenge. It provides a systematic framework for extracting coherent spatiotemporal structures, each evolving with a distinct frequency and growth rate, thereby linking complex data directly to the underlying dynamics.

Unlike traditional analysis methods that may focus solely on spatial correlations or energy content, DMD is uniquely tailored to identify dynamically relevant patterns. This article bridges the gap between raw data and physical insight by providing a comprehensive exploration of the DMD framework.

This exploration begins in **Principles and Mechanisms**, where we will dissect the algorithm's theoretical underpinnings in Koopman [operator theory](@entry_id:139990) and explain how to interpret its outputs. We will then transition to **Applications and Interdisciplinary Connections**, showcasing how DMD is used for [reduced-order modeling](@entry_id:177038), system control, and analysis across various scientific fields. Finally, **Hands-On Practices** will solidify these concepts through practical implementation challenges, building your skills from the ground up. Let us begin by delving into the core principles that make Dynamic Mode Decomposition such a powerful tool.

## Principles and Mechanisms

Dynamic Mode Decomposition (DMD) provides a powerful, data-driven framework for analyzing complex thermal flow fields. It extracts coherent spatiotemporal structures from time-resolved data, such as that obtained from experiments or high-fidelity simulations. Unlike methods based purely on spatial correlations, DMD identifies modes that each possess a single characteristic frequency of oscillation and rate of exponential growth or decay. This chapter elucidates the fundamental principles underpinning DMD, its connection to the operator-theoretic view of dynamical systems, and the mechanisms by which it reveals the physics of thermal transport.

### The Koopman Operator Framework and the Role of Observables

The theoretical foundation of DMD is best understood through the lens of Koopman [operator theory](@entry_id:139990). Consider a thermal flow system whose state at any time $t$ is described by a state vector $\mathbf{z}(t)$ in a high-dimensional state space $\mathbb{R}^n$. This vector typically comprises the discretized velocity and temperature fields. For an [autonomous system](@entry_id:175329), the evolution of the state is governed by a (generally nonlinear) function $\mathbf{f}$:
$$
\frac{d\mathbf{z}}{dt} = \mathbf{f}(\mathbf{z}(t))
$$
The solution to this equation can be expressed using a flow map $F^t$, such that $\mathbf{z}(t) = F^t(\mathbf{z}(0))$. While the evolution of the state $\mathbf{z}$ is nonlinear, we can study the system from a different perspective by considering the evolution of functions of the state. These functions are known as **observables**, which are scalar-valued functions $g: \mathbb{R}^n \to \mathbb{C}$ that "observe" or measure some property of the system.

The **Koopman operator**, denoted $\mathcal{K}^t$, is a [linear operator](@entry_id:136520) that describes the evolution of these observables. Its action is defined by composition with the [flow map](@entry_id:276199):
$$
(\mathcal{K}^t g)(\mathbf{z}) = g(F^t(\mathbf{z}))
$$
This equation states that the value of the evolved observable $\mathcal{K}^t g$ at state $\mathbf{z}$ is found by first evolving the state forward by time $t$ to $F^t(\mathbf{z})$ and then evaluating the original observable $g$ at this new state. The remarkable property of the Koopman operator is that it is linear, even when the underlying dynamical system $\mathbf{f}$ is nonlinear. This recasts the study of [nonlinear dynamics](@entry_id:140844) into the well-developed framework of linear [spectral analysis](@entry_id:143718), albeit in an infinite-dimensional function space.

Dynamic Mode Decomposition provides a data-driven, finite-dimensional approximation of the Koopman operator. Given a sequence of snapshots of the system state, sampled at a uniform interval $\Delta t$, DMD seeks a linear operator that best approximates the action of the discrete-time Koopman operator $U_{\Delta t} = \mathcal{K}^{\Delta t}$ .

The choice of [observables](@entry_id:267133) is critical for the success of this approximation. In principle, one could choose any set of functions of the state. However, a particularly convenient and often effective choice for thermal flow analysis is the set of raw [state variables](@entry_id:138790) themselves—pointwise measurements of the temperature and velocity components across the spatial grid . This choice is justified in many physically relevant scenarios. For instance, in systems near a stable equilibrium (like pure conduction) or a periodic state, the dynamics of small perturbations are governed by a set of linearized equations. In such cases, the space of linear observables—functions of the form $g(\mathbf{z}) = \mathbf{w}^{\top}\mathbf{z}$—is approximately invariant under the Koopman operator. This means that the evolution of a linear measurement of the state remains a linear measurement. Applying DMD directly to the state vectors is thus equivalent to approximating the Koopman operator's action on this approximately [invariant subspace](@entry_id:137024) of linear observables. For example, in analyzing the onset of Rayleigh-Bénard convection, the dynamics of small perturbations about the static, conductive base state are linear. DMD applied to snapshots of the temperature and velocity fields can therefore consistently approximate the dominant Koopman modes, which correspond to the leading eigenmodes of the linearized thermal-hydrodynamic system .

### The Dynamic Mode Decomposition Algorithm

The standard DMD algorithm operates on a sequence of snapshot data. Let us organize our data into two matrices:
$$
X = [\mathbf{z}_0, \mathbf{z}_1, \dots, \mathbf{z}_{m-1}] \in \mathbb{R}^{n \times m}
$$
$$
Y = [\mathbf{z}_1, \mathbf{z}_2, \dots, \mathbf{z}_{m}] \in \mathbb{R}^{n \times m}
$$
Here, $\mathbf{z}_k$ is the state vector at time $t_k = k\Delta t$. The matrix $Y$ is simply the time-shifted version of the matrix $X$. DMD assumes that there exists a single [linear operator](@entry_id:136520) $A$ that approximately advances the state from one snapshot to the next:
$$
\mathbf{z}_{k+1} \approx A \mathbf{z}_k
$$
In matrix form, this relation is $Y \approx AX$. The core of the DMD algorithm is to find the operator $A$ that best fits this relationship in a least-squares sense, by solving the minimization problem:
$$
\min_{A} \|Y - AX\|_{F}^2
$$
where $\|\cdot\|_{F}$ is the Frobenius norm. The solution to this problem is given by:
$$
A = Y X^{+}
$$
where $X^{+}$ is the Moore-Penrose [pseudoinverse](@entry_id:140762) of $X$. In practice, for [high-dimensional systems](@entry_id:750282) where $n \gg m$, the matrix $A$ is not computed explicitly. Instead, a reduced-order version of $A$ is constructed by projecting the data onto a low-rank basis, typically obtained via Singular Value Decomposition (SVD).

The spectral properties of this finite-dimensional operator $A$ are then used to characterize the dynamics. The eigen-decomposition of $A$ yields a set of eigenvalues $\lambda_j$ and corresponding eigenvectors $\boldsymbol{\phi}_j$, which are the **DMD eigenvalues** and **DMD modes**, respectively. Each pair $(\lambda_j, \boldsymbol{\phi}_j)$ represents a coherent structure $\boldsymbol{\phi}_j$ whose amplitude evolves according to the discrete-time multiplier $\lambda_j$.

The fundamental assumption underlying this procedure is that the dynamics can be decomposed into a sum of modes that each evolve exponentially in time. The full state can be reconstructed as:
$$
\mathbf{z}(t) \approx \sum_{j=1}^{r} \boldsymbol{\phi}_j b_j e^{\omega_j t}
$$
where $r$ is the rank of the decomposition, $b_j$ are the initial amplitudes of each mode, and $\omega_j$ are the continuous-time eigenvalues related to the discrete-time DMD eigenvalues $\lambda_j$ by $\lambda_j = e^{\omega_j \Delta t}$. The justification for this [exponential ansatz](@entry_id:176399) comes from the theory of [linear dynamical systems](@entry_id:150282). When the nonlinear governing equations of a thermal flow are linearized about a steady equilibrium state, the resulting dynamics are governed by a linear time-invariant (LTI) operator, whose solutions are precisely sums of exponential functions. Similarly, for dynamics near a periodic attractor (a limit cycle), Floquet theory shows that solutions can also be expressed as a sum of modes with [exponential time](@entry_id:142418) dependence . DMD is therefore a data-driven method for finding the [spectral decomposition](@entry_id:148809) of the best-fit [linear operator](@entry_id:136520) that governs the evolution of the observed data.

### Interpreting DMD Outputs: Eigenvalues and Modes

The output of a DMD analysis is a set of eigenvalue-eigenvector pairs, which contain rich information about the underlying physical mechanisms of the thermal flow.

#### Physical Meaning of the Eigenvalues

Each DMD eigenvalue $\lambda_j$ is a complex number that characterizes the temporal behavior of its corresponding mode $\boldsymbol{\phi}_j$. By converting to the continuous-time eigenvalue $\omega_j = \frac{\ln(\lambda_j)}{\Delta t}$, we can directly interpret its real and imaginary parts:
$$
\omega_j = \sigma_j + i f_j
$$
-   **$\sigma_j = \Re(\omega_j)$** is the **growth/decay rate**. If $\sigma_j > 0$, the amplitude of the mode grows exponentially, indicating an instability. If $\sigma_j  0$, the mode decays exponentially, indicating a stable, dissipative process. If $\sigma_j = 0$, the mode has a sustained, constant amplitude.
-   **$f_j = \Im(\omega_j)$** is the **[angular frequency](@entry_id:274516)** of oscillation. A non-zero $f_j$ signifies that the mode oscillates in time with a period of $2\pi / |f_j|$.

These interpretations allow us to connect the DMD spectrum directly to physical phenomena. For example, consider a stably [stratified fluid](@entry_id:201059) layer where [thermal fluctuations](@entry_id:143642) are observed . A DMD analysis might reveal two distinct types of modes:
1.  **Diffusion-dominated modes:** These modes are non-oscillatory ($f_j \approx 0$) and have a negative growth rate ($\sigma_j  0$). They represent the pure decay of thermal structures due to molecular diffusion. For a thermal Fourier mode with wavenumber magnitude $k$, the theoretical decay rate is $-\alpha k^2$, where $\alpha$ is the [thermal diffusivity](@entry_id:144337). The real part of the DMD eigenvalue for such a mode will closely match this value.
2.  **Buoyancy-driven modes:** In a stably [stratified fluid](@entry_id:201059), buoyancy provides a restoring force, leading to internal gravity waves. These appear as oscillatory modes ($f_j \neq 0$) in the DMD spectrum. The frequency $f_j$ will be related to the Brunt-Väisälä frequency $N = \sqrt{g\beta (d\bar{T}/dz)}$, which is the characteristic frequency of buoyancy oscillations. These modes will also be damped ($\sigma_j  0$) due to the effects of [thermal diffusion](@entry_id:146479) and viscosity.

Since the input data (e.g., temperature fields) are real-valued, the DMD operator $A$ is a real matrix. Consequently, its non-real eigenvalues must appear in **complex-conjugate pairs**. A single complex mode $\boldsymbol{\phi}_j e^{\omega_j t}$ would result in a complex-valued field. A real-valued physical oscillation is reconstructed by combining a complex-conjugate pair of DMD modes. This combination forms a real, oscillating structure (like a cosine wave with a phase shift) whose amplitude grows or decays according to the shared real part of the eigenvalue, $\sigma_j$, and oscillates at the frequency $f_j$ .

For instance, in the flow past a heated cylinder, periodic shedding of thermal plumes occurs. This is a classic oscillatory phenomenon. A DMD analysis will capture this with a dominant complex-conjugate pair of eigenvalues. The magnitude of the eigenvalues, $|\lambda_j| = e^{\sigma_j \Delta t}$, will be slightly less than 1, reflecting the physical reality that the advected thermal structures are simultaneously dissipated by diffusion. The angle of the eigenvalues, $\arg(\lambda_j) = f_j \Delta t$, will correspond to the shedding frequency  .

### The Nature of DMD Modes

The DMD modes $\boldsymbol{\phi}_j$ are the spatial structures associated with each distinct temporal behavior. A key distinction between DMD and other decomposition techniques like Proper Orthogonal Decomposition (POD) lies in the properties of these modes.

#### Dynamic vs. Energy Optimality: DMD and POD

**Proper Orthogonal Decomposition (POD)** produces a set of orthonormal spatial modes that are optimal for representing the energy (or variance) of the snapshot data. The first POD mode is the single spatial structure that captures the most energy in the dataset, the second captures the most of the remaining energy, and so on. This makes POD an extremely efficient method for [data compression](@entry_id:137700).

**Dynamic Mode Decomposition (DMD)**, by contrast, seeks modes that are dynamically pure. Each DMD mode is associated with a single frequency and growth/decay rate. It is therefore optimized for dynamic modeling and interpretation, not for energy compression .

This distinction is crucial in thermal flow analysis. A phenomenon like a coherent oscillation might not be very energetic compared to the mean flow or large-scale turbulent fluctuations. In POD, such an oscillation could be smeared across many modes, making its dynamics difficult to interpret. DMD, however, is designed to isolate this oscillation into a single mode (or a conjugate pair), clearly separating its frequency and growth rate from other phenomena in the flow .

#### The Physical Significance of Non-Orthogonal Modes

A defining feature of DMD modes is that they are generally **not orthogonal**. While POD modes are orthogonal by construction, DMD modes are the eigenvectors of the generally [non-normal matrix](@entry_id:175080) $A$. This non-orthogonality is not a flaw; it is a fundamental property that reflects the underlying physics of many fluid flows, particularly those dominated by advection.

The governing operators for advection-diffusion problems in open domains (with inflow and outflow boundaries) are typically **non-normal**. A non-[normal operator](@entry_id:270585) is one that does not commute with its adjoint. The eigenvectors of such operators are not orthogonal. The DMD operator $A$, being an approximation of these underlying physics, inherits this [non-normality](@entry_id:752585) .

This non-orthogonality is precisely what enables DMD to capture important physical phenomena like **[transient growth](@entry_id:263654)** and convective instabilities. In a heated boundary layer, for example, small disturbances can be amplified significantly as they are advected downstream, even if the flow is asymptotically stable. This transient amplification is a result of the [constructive interference](@entry_id:276464) of non-orthogonal [eigenmodes](@entry_id:174677). A set of decaying, non-orthogonal DMD modes can superpose to create a spatially localized wavepacket that grows in amplitude as it propagates, perfectly capturing the physics of a [convective instability](@entry_id:199544). An [orthogonal basis](@entry_id:264024), like that from POD, is ill-suited to represent this mechanism concisely. The [non-orthogonality](@entry_id:192553) of DMD modes is therefore a feature, not a bug, that allows the decomposition to represent complex wave phenomena in advective thermal flows .

### Advanced Considerations in Applying DMD

While the core principles of DMD are straightforward, its successful application to complex thermal flows requires an awareness of several important theoretical and practical details.

#### Consistency and the Koopman Invariant Subspace

The accuracy of DMD as an approximation of Koopman [spectral theory](@entry_id:275351) hinges on a crucial condition. The DMD eigenvalues will converge to the true Koopman eigenvalues if the chosen observables span a subspace that is **invariant** under the action of the Koopman operator. If this finite-dimensional subspace is closed under the dynamics, DMD can perfectly capture the evolution on that subspace .

In practice, this strict condition is rarely met. However, for many flows of engineering interest, such as those near a steady state or a stable limit cycle, the long-term dynamics are dominated by a small number of Koopman modes. If the chosen observables (e.g., the raw state variables) have a significant projection onto these dominant modes, the subspace is approximately invariant. Under these conditions—along with autonomous dynamics, uniform sampling, and sufficient low-noise data—DMD provides a consistent and highly effective approximation of the most important spectral features of the flow .

#### Handling Non-Stationary and Non-Autonomous Systems

The standard DMD algorithm assumes that the underlying dynamics are autonomous and stationary. However, many thermal systems involve non-[stationary processes](@entry_id:196130), such as a slow ramp-up of heating or cooling. In such cases, the mean state of the system drifts over time. Applying standard DMD to this data is problematic, as the algorithm will attempt to fit a single linear model to a non-autonomous process. This often results in a spurious, [dominant mode](@entry_id:263463) with an eigenvalue near 1 (zero frequency), which represents the mean drift and can mask the true underlying dynamics .

To address this, modified DMD algorithms are required. Two common approaches are:
1.  **DMD with Control (DMDc):** If the cause of the drift is a known external input (like the ramped heat flux), the system can be modeled as $x_{k+1} = Ax_k + Bu_k$, where $u_k$ is the input signal. The DMDc algorithm solves for both the intrinsic dynamics matrix $A$ and the input matrix $B$, thereby separating the [forced response](@entry_id:262169) from the natural dynamics.
2.  **State Augmentation:** For affine systems where the drift can be modeled as a slowly varying bias term $b_k$, one can augment the state vector to $\hat{x}_k = [x_k^T, 1]^T$. A linear model is then fit to this augmented state, which can explicitly capture a constant bias term.

For analyzing fluctuations around a drifting mean, a different preprocessing step is needed for POD and DMD. For POD, one should subtract the time-varying mean from each snapshot to properly isolate the energy of the fluctuations. For DMD, simply subtracting a mean is insufficient; an advanced formulation like DMDc or [state augmentation](@entry_id:140869) is necessary to correctly identify the system's [linear dynamics](@entry_id:177848) in the presence of drift .

#### Uniqueness of the Decomposition

Finally, it is important to consider the uniqueness of the DMD solution. The set of DMD eigenvalues is determined by the data and the chosen rank of the approximation. However, the uniqueness of the DMD modes (the eigenvectors) depends on the properties of the DMD operator $A$.
-   If all eigenvalues of $A$ are distinct (a simple spectrum), then each corresponding eigenvector is unique up to a scalar multiple. The entire set of modes is therefore unique up to individual scaling and permutation .
-   If an eigenvalue is repeated (i.e., it has a [geometric multiplicity](@entry_id:155584) greater than one), the corresponding [eigenspace](@entry_id:150590) is multi-dimensional. In this case, any basis for that [eigenspace](@entry_id:150590) is a valid set of eigenvectors. This choice of basis is not unique. This can occur, for instance, in systems with geometric symmetries.

This is a subtle but important point for the rigorous interpretation of DMD results. In most complex thermal flows without special symmetries, the DMD eigenvalues are typically distinct, leading to a unique set of dynamic modes.