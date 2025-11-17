## Introduction
From the intricate patterns on a seashell to the organized structures of immune cells, nature abounds with examples of complex order emerging from simple, local interactions. Many of these phenomena can be described by [reaction-diffusion systems](@entry_id:136900), where local chemical reactions compete with the spatial transport of molecules. A central question in this field is one of stability: when does a simple, uniform state persist, and under what conditions does it spontaneously break symmetry to form a complex, stable pattern? This article addresses this question by developing a rigorous framework for the [linear stability analysis](@entry_id:154985) of such systems, focusing on the celebrated concept of [diffusion-driven instability](@entry_id:158636), first proposed by Alan Turing.

This guide will navigate you through the theoretical underpinnings and practical applications of this powerful concept. The journey begins in the **Principles and Mechanisms** chapter, where we will establish the mathematical foundation of [reaction-diffusion equations](@entry_id:170319) and [linear stability analysis](@entry_id:154985), dissecting how diffusion can surprisingly act as a destabilizing force. Next, in **Applications and Interdisciplinary Connections**, we will see this theory in action, exploring how it explains pattern formation in fields ranging from developmental biology and [network science](@entry_id:139925) to its use as a design principle in synthetic biology. Finally, the **Hands-On Practices** section will provide opportunities to apply these concepts directly, guiding you through the analysis of classic pattern-forming models. We begin by laying the theoretical groundwork for understanding how order arises from uniformity.

## Principles and Mechanisms

This chapter delves into the fundamental principles governing the stability of states in [reaction-diffusion systems](@entry_id:136900). We will establish the mathematical framework for [linear stability analysis](@entry_id:154985), explore the mechanism of [diffusion-driven pattern formation](@entry_id:188821), and examine more nuanced aspects of stability, including transient dynamics and the influence of advection.

### The Mathematical Framework of Reaction-Diffusion Systems

The dynamics of a system of $n$ interacting and diffusing chemical species within a spatial domain are often modeled by a system of [partial differential equations](@entry_id:143134) (PDEs). Let the concentrations of the species at position $\boldsymbol{x}$ and time $t$ be represented by a vector $\boldsymbol{u}(\boldsymbol{x},t) \in \mathbb{R}^n$. The evolution of this concentration field is governed by two principal processes: local chemical reactions and spatial diffusion. Combining the rate of change from [reaction kinetics](@entry_id:150220), described by a vector field $\boldsymbol{f}(\boldsymbol{u})$, with Fick's law of diffusion, we arrive at the general [reaction-diffusion equation](@entry_id:275361):

$$
\partial_t \boldsymbol{u}(\boldsymbol{x},t) = \boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x},t)) + \boldsymbol{D} \Delta \boldsymbol{u}(\boldsymbol{x},t)
$$

Here, $\Delta$ is the Laplacian operator, which acts component-wise on the vector $\boldsymbol{u}$, and $\boldsymbol{D}$ is the $n \times n$ matrix of diffusion coefficients. For simplicity, we typically assume that there is no cross-diffusion between species, meaning $\boldsymbol{D}$ is a [diagonal matrix](@entry_id:637782), $\boldsymbol{D} = \mathrm{diag}(d_1, d_2, \dots, d_n)$, with positive diffusion constants $d_i > 0$. The term $\boldsymbol{f}(\boldsymbol{u})$ represents the local, well-mixed [reaction kinetics](@entry_id:150220). For a [chemical reaction network](@entry_id:152742) governed by the law of mass action, this term takes the specific form $\boldsymbol{f}(\boldsymbol{u}) = \boldsymbol{S}\boldsymbol{R}(\boldsymbol{u})$, where $\boldsymbol{S}$ is the [stoichiometric matrix](@entry_id:155160) and $\boldsymbol{R}(\boldsymbol{u})$ is the vector of reaction rate functions [@problem_id:2652923].

To complete the model, we must specify the spatial domain $\Omega$ and the boundary conditions. A common and physically relevant scenario is a closed, impermeable vessel. This corresponds to a bounded domain $\Omega \subset \mathbb{R}^d$ with **homogeneous Neumann boundary conditions**, which state that there is zero flux across the boundary $\partial\Omega$. Mathematically, this is expressed as $\partial_{\boldsymbol{n}} \boldsymbol{u}(\boldsymbol{x},t) = \boldsymbol{0}$ for all $\boldsymbol{x} \in \partial\Omega$, where $\partial_{\boldsymbol{n}}$ denotes the derivative in the direction of the outward unit normal to the boundary [@problem_id:2652838].

### Steady States: Homogeneous and Heterogeneous

A central goal in the study of [reaction-diffusion systems](@entry_id:136900) is to identify and characterize their **steady states**, which are time-independent solutions, $\partial_t \boldsymbol{u} = \boldsymbol{0}$. These states represent the long-term equilibrium or patterned configurations of the system. A steady state solution $\boldsymbol{u}_{\text{ss}}(\boldsymbol{x})$ must therefore satisfy the elliptic PDE:

$$
\boldsymbol{D} \Delta \boldsymbol{u}_{\text{ss}}(\boldsymbol{x}) + \boldsymbol{f}(\boldsymbol{u}_{\text{ss}}(\boldsymbol{x})) = \boldsymbol{0}
$$

subject to the given boundary conditions. Steady states can be classified into two primary types [@problem_id:2652903]:

1.  **Spatially Homogeneous Steady State**: This is a steady state that is constant throughout the spatial domain, i.e., $\boldsymbol{u}_{\text{ss}}(\boldsymbol{x}) \equiv \boldsymbol{u}^*$ for some constant vector $\boldsymbol{u}^* \in \mathbb{R}^n$. For such a state, the Laplacian term vanishes, $\Delta \boldsymbol{u}^* = \boldsymbol{0}$. The governing PDE thus simplifies to a purely algebraic equation:
    $$
    \boldsymbol{f}(\boldsymbol{u}^*) = \boldsymbol{0}
    $$
    This demonstrates a critical principle: the *existence* of a homogeneous steady state is determined solely by the reaction kinetics and is independent of the diffusion coefficients. Questions of existence and uniqueness of such states are the domain of Chemical Reaction Network Theory (CRNT), which provides powerful tools like the Deficiency Zero Theorem to guarantee the existence of positive steady states for certain classes of networks [@problem_id:2652923].

2.  **Spatially Heterogeneous Steady State**: This is any non-constant [steady-state solution](@entry_id:276115), $\bar{\boldsymbol{u}}(\boldsymbol{x})$, often referred to as a **stationary pattern**. Such states are solutions to the full elliptic PDE and represent stable, spatially organized structures that can emerge from an initially uniform concentration field.

While both types of steady states are important, the analysis of homogeneous states provides the crucial foundation for understanding how patterns emerge in the first place.

### Linear Stability Analysis of Homogeneous States

Once a homogeneous steady state $\boldsymbol{u}^*$ is found, the next question is whether it is stable. Will small perturbations decay, returning the system to the uniform state, or will they grow, potentially leading to a new, patterned state? This question is answered through **[linear stability analysis](@entry_id:154985)**.

#### Linearization

We consider a small, space- and time-dependent perturbation $\boldsymbol{v}(\boldsymbol{x},t)$ around the steady state: $\boldsymbol{u}(\boldsymbol{x},t) = \boldsymbol{u}^* + \boldsymbol{v}(\boldsymbol{x},t)$. Substituting this into the [reaction-diffusion equation](@entry_id:275361) and performing a Taylor expansion of $\boldsymbol{f}(\boldsymbol{u})$ around $\boldsymbol{u}^*$ gives:
$$
\partial_t (\boldsymbol{u}^* + \boldsymbol{v}) = \boldsymbol{f}(\boldsymbol{u}^* + \boldsymbol{v}) + \boldsymbol{D} \Delta (\boldsymbol{u}^* + \boldsymbol{v})
$$
$$
\partial_t \boldsymbol{v} = \left( \boldsymbol{f}(\boldsymbol{u}^*) + \boldsymbol{J}\boldsymbol{v} + \mathcal{O}(\|\boldsymbol{v}\|^2) \right) + \boldsymbol{D} \Delta \boldsymbol{v}
$$
where $\boldsymbol{J} = \mathrm{D}\boldsymbol{f}(\boldsymbol{u}^*)$ is the Jacobian matrix of the reaction kinetics evaluated at the steady state. Since $\boldsymbol{f}(\boldsymbol{u}^*) = \boldsymbol{0}$, and for infinitesimal perturbations we can neglect the higher-order terms, we obtain the linearized PDE governing the evolution of the perturbation:

$$
\partial_t \boldsymbol{v}(\boldsymbol{x},t) = \boldsymbol{J}\boldsymbol{v}(\boldsymbol{x},t) + \boldsymbol{D} \Delta \boldsymbol{v}(\boldsymbol{x},t)
$$

The stability of the original steady state $\boldsymbol{u}^*$ is now determined by the behavior of solutions to this linear PDE.

#### Modal Decomposition and the Role of Laplacian Eigenfunctions

The linearized PDE is a linear equation with constant-coefficient matrices $\boldsymbol{J}$ and $\boldsymbol{D}$. This structure is key, as it implies the [linear operator](@entry_id:136520) $\mathcal{L}\boldsymbol{v} = \boldsymbol{J}\boldsymbol{v} + \boldsymbol{D}\Delta\boldsymbol{v}$ commutes with the Laplacian operator $\Delta$. This property allows for a powerful solution technique: [separation of variables](@entry_id:148716) via an [eigenfunction expansion](@entry_id:151460) [@problem_id:2652903].

We expand the perturbation $\boldsymbol{v}(\boldsymbol{x},t)$ in the basis of [eigenfunctions](@entry_id:154705) $\phi_k(\boldsymbol{x})$ of the negative Laplacian on the domain $\Omega$ with homogeneous Neumann boundary conditions. These eigenfunctions are the solutions to the eigenproblem [@problem_id:2652917]:
$$
-\Delta \phi_k = \lambda_k \phi_k \quad \text{in } \Omega, \qquad \partial_{\boldsymbol{n}} \phi_k = 0 \quad \text{on } \partial\Omega
$$
From [spectral theory](@entry_id:275351), we know that for a connected, bounded domain, the eigenvalues $\lambda_k$ are real, non-negative, and form a discrete sequence $0 = \lambda_0 \le \lambda_1 \le \lambda_2 \le \dots \to \infty$. The corresponding [eigenfunctions](@entry_id:154705) $\{\phi_k\}_{k=0}^\infty$ form a complete [orthonormal basis](@entry_id:147779) for the space of square-integrable functions $L^2(\Omega)$ [@problem_id:2652917].

The non-negativity of the eigenvalues can be understood physically. By forming the Rayleigh quotient, we see that $\lambda_k = \frac{\int_\Omega |\nabla \phi_k|^2 d\boldsymbol{x}}{\int_\Omega |\phi_k|^2 d\boldsymbol{x}} \ge 0$. Thus, the eigenvalue $\lambda_k$ is a measure of the "[spatial curvature](@entry_id:755140)" or "waviness" of the mode $\phi_k$. The mode with the lowest eigenvalue, $\lambda_0=0$, corresponds to a constant [eigenfunction](@entry_id:149030) $\phi_0(\boldsymbol{x})$, representing a spatially uniform perturbation [@problem_id:2652917].

By expanding the vector perturbation $\boldsymbol{v}(\boldsymbol{x},t)$ as a series $\boldsymbol{v}(\boldsymbol{x},t) = \sum_{k=0}^\infty \boldsymbol{\hat{v}}_k(t) \phi_k(\boldsymbol{x})$, where $\boldsymbol{\hat{v}}_k(t) \in \mathbb{R}^n$ are time-dependent vector amplitudes, the PDE is transformed into an infinite set of decoupled [ordinary differential equations](@entry_id:147024) (ODEs), one for each spatial mode $k$:

$$
\frac{d\boldsymbol{\hat{v}}_k}{dt} = (\boldsymbol{J} - \lambda_k \boldsymbol{D}) \boldsymbol{\hat{v}}_k(t)
$$

This crucial step reduces the infinite-dimensional PDE problem to an infinite collection of finite-dimensional linear algebra problems [@problem_id:2652838] [@problem_id:2652917]. This decomposition works even if the [diffusion matrix](@entry_id:182965) $\boldsymbol{D}$ is not diagonal, as long as it is constant [@problem_id:2652917].

### The Dispersion Relation and Stability Criteria

The stability of the steady state $\boldsymbol{u}^*$ requires that any small perturbation $\boldsymbol{v}(\boldsymbol{x},t)$ must decay to zero. Since any perturbation can be decomposed into spatial modes, this means the amplitude $\boldsymbol{\hat{v}}_k(t)$ of *every* mode must decay to zero as $t \to \infty$.

The solution to the modal ODE is $\boldsymbol{\hat{v}}_k(t) = \exp(t\boldsymbol{A}_k) \boldsymbol{\hat{v}}_k(0)$, where $\boldsymbol{A}_k = \boldsymbol{J} - \lambda_k \boldsymbol{D}$. The stability of mode $k$ is therefore determined by the eigenvalues of the $n \times n$ matrix $\boldsymbol{A}_k$. Let $\sigma(\boldsymbol{A}_k)$ be the spectrum (set of eigenvalues) of $\boldsymbol{A}_k$. The amplitude $\boldsymbol{\hat{v}}_k(t)$ decays to zero if and only if all eigenvalues in $\sigma(\boldsymbol{A}_k)$ have strictly negative real parts.

This leads to the concept of the **dispersion relation**, which describes how the temporal growth rate of a perturbation depends on its spatial structure (i.e., its mode index $k$ or [wavenumber](@entry_id:172452)). For each mode $k$, we define $\sigma(k) = \sigma(\boldsymbol{J} - \lambda_k \boldsymbol{D})$ as the set of associated growth rates. The stability of that specific mode is governed by the sign of the maximal real part of these growth rates [@problem_id:2652842]:
*   If $\max \operatorname{Re} \sigma(k)  0$, mode $k$ is **linearly stable** and decays.
*   If $\max \operatorname{Re} \sigma(k) > 0$, mode $k$ is **linearly unstable** and grows.
*   If $\max \operatorname{Re} \sigma(k) = 0$, mode $k$ is **neutrally stable** (at the threshold of instability).

For the entire system to be **linearly asymptotically stable**, all modes must be stable. This translates to the condition that the worst-case growth rate over all possible spatial modes must be negative. We define the maximal growth rate of the system as:
$$
\Gamma = \sup_{k \ge 0} \left\{ \max \operatorname{Re} \mu \mid \mu \in \sigma(\boldsymbol{J} - \lambda_k \boldsymbol{D}) \right\}
$$
The steady state $\boldsymbol{u}^*$ is then linearly asymptotically stable if and only if $\Gamma  0$ [@problem_id:2652801]. If $\Gamma \le 0$, with $\Gamma=0$ occurring for some mode(s) whose corresponding eigenvalues are semisimple, the state is said to be linearly stable (but not asymptotically stable) [@problem_id:2652801].

### The Mechanism of Diffusion-Driven Instability

The framework of [linear stability analysis](@entry_id:154985) leads to one of the most profound concepts in pattern formation: **[diffusion-driven instability](@entry_id:158636)**, first predicted by Alan Turing. This phenomenon occurs when a homogeneous steady state that is stable in the absence of spatial effects is driven unstable by the presence of diffusion. This provides a mechanism for **spontaneous pattern formation**, or [morphogenesis](@entry_id:154405).

The stability of the system without diffusion (or, equivalently, to purely homogeneous perturbations) corresponds to the mode $k=0$, for which $\lambda_0 = 0$. The stability matrix is $\boldsymbol{A}_0 = \boldsymbol{J}$. The condition for stability is that all eigenvalues of $\boldsymbol{J}$ must have negative real parts.

A diffusion-driven, or **Turing**, instability arises if:
1.  The homogeneous steady state is stable to homogeneous perturbations (all eigenvalues of $\boldsymbol{J}$ have negative real parts).
2.  The steady state is unstable to at least one non-homogeneous perturbation (for some $k>0$ where $\lambda_k > 0$, the matrix $\boldsymbol{A}_k = \boldsymbol{J} - \lambda_k \boldsymbol{D}$ has at least one eigenvalue with a positive real part).

This contradicts the simple intuition that diffusion, a dissipative process, should always be stabilizing. Diffusion can, under specific circumstances, be the very cause of instability.

#### A Canonical Example: The Two-Species System

The essential mechanism can be fully elucidated by analyzing a two-species system. Let the Jacobian be $\boldsymbol{J} = \begin{pmatrix} f_u  f_v \\ g_u  g_v \end{pmatrix}$ and the [diffusion matrix](@entry_id:182965) be $\boldsymbol{D} = \mathrm{diag}(d_u, d_v)$. Stability for mode $k$ is determined by the eigenvalues of $\boldsymbol{A}_k = \boldsymbol{J} - \lambda_k \boldsymbol{D}$. According to the Routh-Hurwitz stability criterion for a $2 \times 2$ matrix, the eigenvalues have negative real parts if and only if $\mathrm{Tr}(\boldsymbol{A}_k)  0$ and $\det(\boldsymbol{A}_k) > 0$.

A Turing instability requires:
1.  **Reaction-only stability (k=0)**: $\mathrm{Tr}(\boldsymbol{J}) = f_u+g_v  0$ and $\det(\boldsymbol{J}) = f_u g_v - f_v g_u > 0$.
2.  **Diffusion-driven instability (k0)**: For some $\lambda_k > 0$, stability is lost.

Let's examine the trace and determinant of $\boldsymbol{A}_k$:
$$
\mathrm{Tr}(\boldsymbol{A}_k) = \mathrm{Tr}(\boldsymbol{J}) - \lambda_k(d_u+d_v)
$$
$$
\det(\boldsymbol{A}_k) = \det(\boldsymbol{J}) - \lambda_k(f_u d_v + g_v d_u) + \lambda_k^2 d_u d_v
$$

Since $\mathrm{Tr}(\boldsymbol{J})  0$ and $d_u, d_v > 0$, the trace $\mathrm{Tr}(\boldsymbol{A}_k)$ will always be negative for any $\lambda_k > 0$. Therefore, instability can only arise if the determinant condition is violated, i.e., if $\det(\boldsymbol{A}_k)$ becomes negative for some $\lambda_k > 0$.

The function $h(\lambda_k) = \det(\boldsymbol{A}_k)$ is a quadratic in $\lambda_k$. For it to dip below zero, given that $h(0)=\det(\boldsymbol{J}) > 0$ and it opens upwards (since $d_u d_v > 0$), its minimum must occur at a positive $\lambda_k$ and be negative. This leads to two further conditions:
3.  The coefficient of the linear term in $h(\lambda_k)$ must be positive: $f_u d_v + g_v d_u > 0$.
4.  The minimum value of the determinant must be negative, which is equivalent to $(f_u d_v + g_v d_u)^2 > 4 d_u d_v \det(\boldsymbol{J})$.

These four inequalities constitute the classical Turing conditions [@problem_id:2652799]. The instability first emerges at the **critical wavenumber** where the determinant first touches zero. This corresponds to the minimum of the determinant parabola, yielding a critical Laplacian eigenvalue of $\lambda_c = \frac{f_u d_v + g_v d_u}{2 d_u d_v}$. The corresponding spatial pattern will have a characteristic wavelength related to $\lambda_c$ [@problem_id:2652799].

#### The Activator-Inhibitor Logic

The mathematical conditions for Turing instability have a powerful physical interpretation in terms of an **[activator-inhibitor](@entry_id:182190)** mechanism. Consider a feed-forward motif where species $u$ is the activator and $v$ is the inhibitor [@problem_id:2652901]:
*   The activator promotes its own production ($f_u > 0$).
*   The activator promotes the inhibitor's production ($g_u > 0$).
*   The inhibitor suppresses the activator's production ($f_v  0$).
*   The inhibitor decays or suppresses itself ($g_v  0$).

For the reaction-only system to be stable, the inhibitor's self-damping must be strong enough to overcome the activator's self-amplification ($f_u+g_v  0$). The crucial condition for Turing instability becomes $f_u d_v + g_v d_u > 0$. With $f_u > 0$ and $g_v  0$, this can be written as $f_u d_v > |g_v| d_u$. This inequality is most easily satisfied if the diffusion coefficient of the inhibitor is much larger than that of the activator, $d_v \gg d_u$.

This leads to the famous heuristic for Turing patterns: **short-range activation and [long-range inhibition](@entry_id:200556)**. A small local fluctuation in the activator can grow due to autocatalysis. This also produces the inhibitor, but because the inhibitor diffuses much faster, it spreads out, suppressing activator growth in a wide surrounding region while leaving the central peak to continue growing. The result is a stable pattern of isolated peaks, whose spacing is determined by the diffusion length of the inhibitor.

### Advanced Topics and Broader Contexts

While the [modal analysis](@entry_id:163921) of homogeneous states is foundational, a complete understanding of stability requires considering more complex phenomena.

#### Transient Growth and Non-Normality

Eigenvalue analysis determines the asymptotic, long-term fate of a perturbation. However, it does not tell the whole story about the short-term dynamics. For the modal equation $\dot{\boldsymbol{\hat{v}}}_k = \boldsymbol{A}_k \boldsymbol{\hat{v}}_k$, if the matrix $\boldsymbol{A}_k$ is **non-normal**—meaning it does not commute with its [conjugate transpose](@entry_id:147909), $\boldsymbol{A}_k \boldsymbol{A}_k^* \neq \boldsymbol{A}_k^* \boldsymbol{A}_k$—then its eigenvectors are not orthogonal. This [non-orthogonality](@entry_id:192553) can lead to constructive interference between decaying [eigenmodes](@entry_id:174677), resulting in a temporary, sometimes substantial, amplification of the perturbation norm before its eventual decay. This is known as **transient growth**.

The potential for transient growth is quantified by the **numerical abscissa**, $w(\boldsymbol{A}_k)$, which is the maximum real part of the [numerical range](@entry_id:752817) of $\boldsymbol{A}_k$. It governs the maximum possible instantaneous growth rate of the norm: $\frac{d}{dt}\|\boldsymbol{\hat{v}}_k(t)\|_2 \le w(\boldsymbol{A}_k)\|\boldsymbol{\hat{v}}_k(t)\|_2$. For any matrix, $\alpha(\boldsymbol{A}_k) \le w(\boldsymbol{A}_k)$, where $\alpha$ is the spectral abscissa. For [normal matrices](@entry_id:195370), equality holds, and no transient growth is possible in a stable system. For [non-normal matrices](@entry_id:137153), however, it is possible to have $\alpha(\boldsymbol{A}_k)  0$ ([asymptotic stability](@entry_id:149743)) while simultaneously having $w(\boldsymbol{A}_k) > 0$. This is the signature of transient growth: the system is stable in the long run, but certain initial perturbations can experience a short-term burst of amplification [@problem_id:2652806].

#### Convective versus Absolute Instability

When a system includes advection (bulk flow), the concept of instability becomes richer. Consider a one-dimensional system with advection speed $V$: $\partial_t u + V \partial_x u = \dots$. An instability is classified as [@problem_id:2652827]:
*   **Convective**: A localized perturbation grows in amplitude but is simultaneously swept away by the flow, such that at any fixed point in space, the perturbation eventually vanishes.
*   **Absolute**: A localized perturbation grows in place, eventually contaminating the entire domain.

The distinction is crucial for understanding whether an instability will be localized and transient or global and persistent in an open-flow system. The **Briggs-Bers criterion** provides a method to distinguish these cases by analyzing the dispersion relation $\lambda(k)$ in the [complex wavenumber](@entry_id:274896) plane. Absolute instability corresponds to a "pinch point" saddle $k_0$ where two [complex roots](@entry_id:172941) of the [dispersion relation](@entry_id:138513) merge. The condition for the saddle is $\partial\lambda/\partial k = 0$. The absolute growth rate is then $\operatorname{Re}(\lambda(k_0))$. For the simple model $\partial_t \phi + V \partial_x \phi = D \partial_{xx} \phi + a \phi$ with $a>0$, the absolute growth rate is $\lambda_{\text{abs}} = a - V^2/(4D)$. The system transitions from absolute to [convective instability](@entry_id:199544) when $\lambda_{\text{abs}}=0$, which occurs at a critical advection speed of $V_c = 2\sqrt{Da}$ [@problem_id:2652827].

#### Stability of Heterogeneous States

Finally, it is important to recognize the limitations of the analysis presented. The elegant [modal decomposition](@entry_id:637725) is only possible when linearizing around a *homogeneous* steady state. If we wish to analyze the stability of a *heterogeneous* state, or stationary pattern $\bar{\boldsymbol{u}}(\boldsymbol{x})$, the [linearization](@entry_id:267670) yields an operator with spatially varying coefficients: $\partial_t \boldsymbol{v} = \boldsymbol{J}(\bar{\boldsymbol{u}}(\boldsymbol{x}))\boldsymbol{v} + \boldsymbol{D}\Delta\boldsymbol{v}$. In this case, the operator no longer commutes with the Laplacian, and the Laplacian [eigenfunctions](@entry_id:154705) do not decouple the system. The analysis of pattern stability requires significantly more advanced [spectral theory](@entry_id:275351) for variable-coefficient operators and is an active area of research [@problem_id:2652903].