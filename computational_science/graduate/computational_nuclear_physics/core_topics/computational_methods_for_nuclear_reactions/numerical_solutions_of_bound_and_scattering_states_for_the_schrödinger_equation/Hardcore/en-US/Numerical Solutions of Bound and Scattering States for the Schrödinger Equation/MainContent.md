## Introduction
The time-independent Schrödinger equation is the master equation of non-[relativistic quantum mechanics](@entry_id:148643), and the ability to solve it is fundamental to predicting the structure and dynamics of quantum systems. In [nuclear physics](@entry_id:136661), this equation provides the crucial link between the theoretical models of the forces between nucleons and the rich spectrum of experimental observables, from the energies of stable nuclei to the cross sections of [nuclear reactions](@entry_id:159441). However, for realistic interaction potentials, analytical solutions are rarely available, making robust numerical methods indispensable tools for the theoretical physicist. This article addresses the central challenge of numerically solving the Schrödinger equation for the two most important classes of problems: bound states and scattering states.

Across the following chapters, you will gain a comprehensive understanding of the principles, applications, and practical implementation of these numerical solutions. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, dissecting the radial Schrödinger equation, establishing the critical boundary conditions that define physical solutions, and exploring the numerical challenges associated with different potential types. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how these numerical methods are applied to predict experimental [observables](@entry_id:267133) like scattering cross sections, model the complexities of the nuclear tensor force through [coupled channels](@entry_id:204758), and even extend quantum mechanics to describe unstable resonant states. Finally, the "Hands-On Practices" section provides targeted exercises to solidify your understanding of core computational techniques. We begin by examining the foundational principles that govern the behavior of quantum particles in a central potential.

## Principles and Mechanisms

The theoretical and computational investigation of [nuclear structure](@entry_id:161466) and reactions hinges upon our ability to solve the time-independent Schrödinger equation. This chapter delves into the fundamental principles that govern the solutions for single-particle [motion in a central potential](@entry_id:203461), laying the groundwork for the numerical methods used to compute bound-state energies and [scattering phase shifts](@entry_id:138129). We will dissect the equation, examine the behavior of its solutions at physical boundaries, and explore the implications of different potential types, from short-ranged [nuclear forces](@entry_id:143248) to the long-range Coulomb interaction.

### The Radial Schrödinger Equation

The starting point for describing a nucleon of [reduced mass](@entry_id:152420) $\mu$ moving in a spherically [symmetric potential](@entry_id:148561) $V(r)$ is the three-dimensional time-independent Schrödinger equation:
$$
\left[-\frac{\hbar^{2}}{2\mu}\nabla^{2}+V(r)\right]\psi(\mathbf{r})=E\,\psi(\mathbf{r})
$$
Given the spherical symmetry of the potential, the problem is most naturally approached in spherical coordinates $(r, \theta, \phi)$. The [rotational invariance](@entry_id:137644) of the Hamiltonian implies that its [eigenstates](@entry_id:149904) can be chosen to be [simultaneous eigenstates](@entry_id:149152) of the squared orbital [angular momentum operator](@entry_id:155961), $\hat{L}^2$, and its projection, $\hat{L}_z$. This allows for a separation of variables, where the wavefunction $\psi(\mathbf{r})$ is expressed as a product of a radial function $R_{l}(r)$ and a spherical harmonic $Y_{lm}(\theta, \phi)$:
$$
\psi(\mathbf{r}) = R_{l}(r)Y_{lm}(\theta,\phi)
$$
The [spherical harmonics](@entry_id:156424) are the [eigenfunctions](@entry_id:154705) of the angular part of the Laplacian, satisfying $\hat{L}^2 Y_{lm} = \hbar^2 l(l+1) Y_{lm}$, where $l$ is the orbital angular momentum quantum number. Substituting this form into the Schrödinger equation and separating the angular and radial dependencies yields an ordinary differential equation for the radial part, $R_l(r)$.

For both theoretical analysis and numerical computation, it is convenient to work with the **reduced [radial wavefunction](@entry_id:151047)**, defined as $u_l(r) \equiv r R_l(r)$. This substitution simplifies the radial [kinetic energy operator](@entry_id:265633). The equation for $u_l(r)$, known as the **radial Schrödinger equation**, is :
$$
-\frac{\hbar^{2}}{2\mu}\frac{d^{2}u_{l}(r)}{dr^{2}}+\left[V(r)+\frac{\hbar^{2}l(l+1)}{2\mu r^{2}}\right]u_{l}(r)=E u_{l}(r)
$$
This equation is the cornerstone of our analysis. It resembles a one-dimensional Schrödinger equation for a particle moving in an **[effective potential](@entry_id:142581)**, $V_{\text{eff}}(r) = V(r) + \frac{\hbar^{2}l(l+1)}{2\mu r^{2}}$. The second term, known as the **centrifugal barrier**, is a [repulsive potential](@entry_id:185622) that arises from the conservation of angular momentum and pushes the particle away from the origin for any non-zero angular momentum ($l > 0$).

### Behavior of Solutions at Physical Boundaries

Solving the radial Schrödinger equation requires specifying boundary conditions at the limits of the domain $r \in [0, \infty)$. The physical nature of the wavefunction imposes stringent constraints on its behavior at both the origin ($r \to 0$) and at large distances ($r \to \infty$).

#### Regularity at the Origin

The original radial function, $R_l(r)$, must remain finite at the origin to ensure the probability density $|\psi(\mathbf{r})|^2$ is well-behaved. Since $u_l(r) = r R_l(r)$, this immediately implies the boundary condition:
$$
u_l(r) \to 0 \quad \text{as} \quad r \to 0
$$
To understand this behavior more precisely, we can analyze the [radial equation](@entry_id:138211) for small $r$. Assuming the potential $V(r)$ is regular at the origin and can be expanded in a Taylor series, such as $V(r) = V(0) + V_2 r^2 + \mathcal{O}(r^4)$, the [dominant term](@entry_id:167418) in the [effective potential](@entry_id:142581) for $l>0$ is the [centrifugal barrier](@entry_id:147153), which diverges as $1/r^2$. A Frobenius analysis of the differential equation shows that there are two possible behaviors for $u_l(r)$ near the origin: $u_l(r) \sim r^{l+1}$ (the [regular solution](@entry_id:156590)) and $u_l(r) \sim r^{-l}$ (the irregular solution). Only the [regular solution](@entry_id:156590) satisfies the physical boundary condition $u_l(0)=0$. Therefore, for any physically acceptable wavefunction, we must have:
$$
u_l(r) \propto r^{l+1} \quad \text{as} \quad r \to 0
$$
This leading-order behavior is the starting point for any numerical outward integration of the equation. Higher-order corrections depend on the potential and energy. For instance, the next term in the [series expansion](@entry_id:142878) is of the form $u_l(r) = r^{l+1}(a_0 + a_2 r^2 + \dots)$, where the coefficient $a_2$ is related to $a_0$ by :
$$
a_2 = \frac{\mu(V(0)-E)}{\hbar^{2}(2l+3)}a_{0}
$$
This more detailed form is crucial for initializing high-order numerical solvers. A key quantity used for matching solutions is the **logarithmic derivative**, $L(r) \equiv u_l'(r)/u_l(r)$. Using the series expansion, its behavior at a small matching radius $a$ can be determined to be:
$$
L(a) \approx \frac{l+1}{a} + \frac{2\mu(V(0)-E)}{\hbar^{2}(2l+3)}a
$$
This expression provides a precise condition to initialize an integration algorithm slightly away from the singular point at $r=0$.

#### Asymptotic Behavior for Short-Range Potentials

At large distances ($r \to \infty$), for a potential $V(r)$ that vanishes faster than $1/r$ (a so-called **short-range potential**), both the [nuclear potential](@entry_id:752727) and the centrifugal barrier become negligible. The [radial equation](@entry_id:138211) simplifies to:
$$
\frac{d^{2}u_{l}(r)}{dr^{2}} \approx -\frac{2\mu E}{\hbar^{2}}u_{l}(r)
$$
The character of the solution in this asymptotic region depends entirely on the sign of the energy $E$  .

**1. Bound States ($E  0$)**

For a bound state, the particle is confined within the [potential well](@entry_id:152140), and its total energy is negative. Let $E = -|E|$. We define a real, positive wave number $\kappa = \sqrt{2\mu|E|/\hbar^2}$. The asymptotic equation becomes $\frac{d^2u_l}{dr^2} \approx \kappa^2 u_l(r)$. The general solution is a [linear combination](@entry_id:155091) of a growing exponential, $e^{\kappa r}$, and a decaying exponential, $e^{-\kappa r}$. For the total probability of finding the particle in all of space to be finite (i.e., for the wavefunction to be normalizable), the wavefunction must vanish at infinity. This requires that we discard the unphysical growing solution. The asymptotic form of the reduced [radial wavefunction](@entry_id:151047) for a [bound state](@entry_id:136872) is therefore:
$$
u_l(r) \sim A e^{-\kappa r} \quad (r \to \infty, E  0)
$$
where $A$ is a normalization constant. When accounting for the sub-leading effects of the centrifugal barrier, the exact asymptotic form involves modified spherical Bessel functions, but the dominant behavior is this exponential decay.

**2. Scattering States ($E > 0$)**

For a scattering state, the particle has positive energy and is not confined. It can propagate to and from infinity. We define a real, positive wave number $k = \sqrt{2\mu E/\hbar^2}$. The asymptotic equation is now that of a simple harmonic oscillator, $\frac{d^2u_l}{dr^2} \approx -k^2 u_l(r)$, with oscillatory solutions. In the absence of any potential ($V(r)=0$), the solution that is regular at the origin is proportional to a spherical Bessel function, which asymptotically behaves as $\sin(kr - l\pi/2)$. The effect of the short-range potential is to introduce a shift in the phase of this oscillation. The asymptotic form of the reduced [radial wavefunction](@entry_id:151047) for a scattering state is:
$$
u_l(r) \sim B \sin\left(kr - \frac{l\pi}{2} + \delta_{l}\right) \quad (r \to \infty, E > 0)
$$
The quantity $\delta_l$ is the **phase shift** for the $l$-th partial wave. It encodes all the information about the scattering process and is the primary observable quantity sought in calculations of low-energy [nuclear reactions](@entry_id:159441). A positive phase shift corresponds to an attractive potential, which "pulls in" the wavefunction, while a negative phase shift corresponds to a [repulsive potential](@entry_id:185622).

### Numerical Integration Strategies and Challenges

The boundary conditions at $r=0$ and $r\to\infty$ frame the numerical problem.

For **scattering states**, the energy $E$ is given. The typical strategy is to integrate the [radial equation](@entry_id:138211) outwards. One starts at a very small radius $r_{min}$ (or uses the analytical series from the previous section) with the regular boundary condition $u_l(r) \propto r^{l+1}$ and integrates out to a large **matching radius** $r_m$, chosen to be well beyond the range of the [nuclear potential](@entry_id:752727). At $r_m$, the numerical solution (specifically its logarithmic derivative) is matched to the known analytic solution in the free-particle region, which is a combination of spherical Bessel and Neumann functions, $j_l(kr)$ and $n_l(kr)$. This matching procedure directly determines the value of the phase shift $\delta_l$ . An equivalent and often used formulation expresses the solution in the outer region as $u_l(r) \propto \cos(\delta_l)j_l(kr) - \sin(\delta_l)n_l(kr)$ .

For **[bound states](@entry_id:136502)**, the situation is an [eigenvalue problem](@entry_id:143898): the energy $E$ is not known *a priori*. One must find the specific negative energies for which a solution exists that is regular at the origin *and* decays exponentially at infinity. A common numerical technique is the **shooting method**. One guesses an energy $E$, integrates outwards from the origin, and examines the solution at large $r$. If the solution diverges towards $+\infty$ or $-\infty$, the energy is incorrect. One then adjusts the energy and repeats the process, "shooting" again until an energy is found where the solution "hits the target" of decaying to zero.

However, this outward integration for [bound states](@entry_id:136502) is notoriously **numerically unstable** . Any tiny numerical [round-off error](@entry_id:143577) during the integration will inevitably introduce a small component of the unphysical, exponentially growing solution $e^{\kappa r}$. As the integration proceeds to large $r$, this growing component will quickly swamp the desired decaying solution, leading to numerical overflow and a failure to find the correct eigenvalue. To circumvent this, more stable methods are employed. One common strategy is to integrate inwards from a large radius (initialized with the decaying exponential form) and outwards from the origin, requiring that the two solutions and their derivatives match smoothly at an intermediate point. Another powerful approach is to solve for the [logarithmic derivative](@entry_id:169238) of the wavefunction, which transforms the second-order linear equation for $u_l$ into a first-order non-linear Riccati equation for $L(r)$, a method that is inherently more stable against such issues.

### Extension to Long-Range Coulomb Potentials

When describing the scattering of charged particles, such as proton-proton or nucleus-nucleus scattering, the short-range [nuclear potential](@entry_id:752727) $V_N(r)$ is accompanied by the long-range Coulomb potential, $V_C(r) = \frac{Z_1 Z_2 e^2}{r}$. Because the Coulomb potential falls off very slowly (as $1/r$), it distorts the wavefunction even at arbitrarily large distances. The asymptotic solutions are no longer simple sinusoids.

In the region $r \ge r_m$ where the [nuclear potential](@entry_id:752727) is negligible, the radial Schrödinger equation becomes the **Coulomb wave equation**. Its two [linearly independent solutions](@entry_id:185441) are the regular and irregular **Coulomb functions**, denoted $F_l(\eta, kr)$ and $G_l(\eta, kr)$, respectively . These functions depend on the dimensionless **Sommerfeld parameter**, $\eta$, which quantifies the strength of the Coulomb interaction relative to the kinetic energy:
$$
\eta = \frac{\mu Z_1 Z_2 e^2}{\hbar^2 k}
$$
The presence of the short-range [nuclear potential](@entry_id:752727) means the full solution for $r \ge r_m$ is a linear combination of these two functions. By convention, it is written as:
$$
u_l(r) \propto \cos\delta_l F_l(\eta, kr) + \sin\delta_l G_l(\eta, kr)
$$
Here, $\delta_l$ is now the **nuclear phase shift**, representing the additional phase shift caused by $V_N(r)$ on top of the underlying Coulomb scattering.

The asymptotic forms of the Coulomb functions themselves are revealing :
$$
F_l(\eta, kr) \sim \sin\left(kr - \frac{l\pi}{2} - \eta\ln(2kr) + \sigma_l\right)
$$
$$
G_l(\eta, kr) \sim \cos\left(kr - \frac{l\pi}{2} - \eta\ln(2kr) + \sigma_l\right)
$$
Compared to the free-particle case, two new features appear. First, there is a logarithmic [phase distortion](@entry_id:184482), $-\eta\ln(2kr)$, which is a hallmark of long-range $1/r$ potentials. Second, there is a **Coulomb phase shift**, $\sigma_l = \arg\Gamma(l+1+i\eta)$, which is the phase shift produced by the Coulomb potential alone. The total phase of the asymptotic wavefunction is the sum of these contributions, and the partial-wave [scattering matrix](@entry_id:137017) element becomes $S_l = e^{2i(\sigma_l + \delta_l)}$. Numerical calculations proceed by integrating outward through the combined nuclear and Coulomb potential up to $r_m$ and then matching to the combination of $F_l$ and $G_l$ to extract the nuclear phase shift $\delta_l$.

### Singular Potentials and Self-Adjointness

The discussion so far has assumed that the potential $V(r)$ is regular or, at worst, less singular than the $1/r^2$ [centrifugal barrier](@entry_id:147153) at the origin. However, some theoretical models involve potentials that are as singular as or more singular than the centrifugal term, such as an attractive [inverse-square potential](@entry_id:202452) $V(r) = -\alpha/r^2$ with $\alpha0$. Such cases demand a more careful consideration of the mathematical properties of the Hamiltonian operator itself, specifically its **self-adjointness**. A self-adjoint Hamiltonian guarantees a unique, probability-conserving [time evolution](@entry_id:153943).

The radial Hamiltonian can be written in terms of an effective coupling constant $\gamma = l(l+1) - \frac{2\mu\alpha}{\hbar^2}$. The behavior of the solutions near the origin and the self-adjointness of the Hamiltonian are determined by the value of $\gamma$ . The **Weyl limit-point/limit-[circle criterion](@entry_id:173992)** provides a precise test. For a potential term $q(r) = \gamma/r^2$ at the singular endpoint $r=0$:
*   If $\gamma \ge 3/4$, the endpoint is said to be **limit-point**. In this regime, only one of the two independent solutions of the Schrödinger equation is square-integrable near the origin. The physical requirement of a finite probability is sufficient to uniquely specify the solution. The Hamiltonian is essentially self-adjoint, and no extra boundary condition is needed at $r=0$.
*   If $\gamma  3/4$, the endpoint is **limit-circle**. In this case, *both* independent solutions are square-integrable near the origin. The minimal Hamiltonian is not self-adjoint and has a one-parameter family of [self-adjoint extensions](@entry_id:264525). This means that square-integrability alone is not enough to define the physics. A choice must be made, which takes the form of an additional boundary condition at $r=0$, such as specifying the value of $\lim_{r\to 0}[r\,u'(r)/u(r)]$. This choice is not a mathematical convenience; it is a physical input that determines the properties of the system, such as its bound-state energies and scattering length.

This has a critical consequence for [s-wave](@entry_id:754474) ($\ell=0$) interactions. For [s-wave](@entry_id:754474) interactions ($\ell=0$), the coupling becomes $\gamma = -2\mu\alpha/\hbar^2  0$. This always falls in the limit-circle case ($\gamma  3/4$). Therefore, for an [s-wave](@entry_id:754474) nucleon in such a potential, the physics is not fully specified by the Hamiltonian alone. A boundary condition at the origin, which parameterizes the choice of [self-adjoint extension](@entry_id:151493), must be provided to have a well-defined quantum mechanical problem . This boundary condition effectively models the unknown short-range physics that resolves the singularity.