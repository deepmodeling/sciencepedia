## Introduction
The emergence of superconductivity, characterized by the complete disappearance of [electrical resistance](@entry_id:138948) below a critical temperature, represents a macroscopic quantum phenomenon with profound technological implications. However, the electrodynamic response of a superconductor is far richer than mere perfect conductivity. The key to understanding this unique state lies in the Meissner effect—the active expulsion of magnetic flux—which simple classical models fail to explain. This article provides a comprehensive exploration of London electrodynamics, the first successful phenomenological theory to account for this behavior.

This article is structured to build a robust understanding from first principles to modern applications.
*   The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork. We will derive the two London equations, define the crucial concept of the London [penetration depth](@entry_id:136478), and explore the limits of this local model, introducing the concepts of [coherence length](@entry_id:140689) and nonlocal electrodynamics.
*   The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the theory's power. We will see how the penetration depth is used to characterize materials, probe the symmetry of the superconducting gap, and understand the physics of [quantum vortices](@entry_id:147375) in Type-II superconductors, drawing connections to other fields like AMO physics.
*   Finally, the **Hands-On Practices** section provides opportunities to apply these concepts to solve concrete problems involving field screening, critical currents, and anisotropy.

We begin our exploration by examining the experimental evidence that necessitated a departure from [classical electrodynamics](@entry_id:270496) and paved the way for the elegant framework proposed by Fritz and Heinz London.

## Principles and Mechanisms

The electromagnetic properties of superconductors are profoundly different from those of ordinary metals. The vanishing of direct-current electrical resistance is but one aspect of a richer phenomenology. The defining characteristic of the superconducting state is, in fact, an active and history-independent expulsion of magnetic flux—the Meissner-Ochsenfeld effect. This chapter develops the foundational principles and mechanisms governing this behavior, beginning with the failure of classical models and culminating in the elegant phenomenological framework of London [electrodynamics](@entry_id:158759). We will explore the consequences of this theory, its applications, and its ultimate limitations, which point the way toward a more complete microscopic understanding.

### The Meissner Effect and the Inadequacy of Perfect Conductivity

A natural first step in modeling a material with [zero resistance](@entry_id:145222) is to consider the limit of a "perfect conductor," a hypothetical material with infinite [electrical conductivity](@entry_id:147828), $\sigma \to \infty$. In such a material, Ohm's law, $\mathbf{J} = \sigma \mathbf{E}$, dictates that any finite current density $\mathbf{J}$ must be sustained by a vanishingly small electric field, $\mathbf{E} = \mathbf{0}$. The implications of this are revealed by Faraday's law of induction, $\nabla \times \mathbf{E} = -\partial \mathbf{B} / \partial t$. If $\mathbf{E}$ is zero throughout the material, it follows that:

$$
\frac{\partial \mathbf{B}}{\partial t} = \mathbf{0}
$$

This equation implies that the magnetic induction $\mathbf{B}$ inside a [perfect conductor](@entry_id:273420) can never change. The magnetic flux is "frozen" in time. This prediction can be tested with a thought experiment known as a **field-cooling** protocol [@problem_id:3009512] [@problem_id:2840809]. Imagine a sample is placed in a static, uniform magnetic field $H_0$ at a temperature $T$ above its transition temperature $T_c$. The field penetrates the material. If the sample is then cooled to a temperature below $T_c$ where it becomes a perfect conductor, the condition $\partial \mathbf{B} / \partial t = \mathbf{0}$ means the pre-existing flux remains trapped inside the material.

The Meissner-Ochsenfeld experiment, however, reveals a starkly different reality. When a real superconductor is cooled below $T_c$ in a magnetic field, the magnetic flux is actively expelled from its interior. The final state is one where $\mathbf{B} \approx \mathbf{0}$ in the bulk of the material, regardless of whether the field was applied before or after cooling. This history-independence signifies that the superconducting state is a true **thermodynamic equilibrium state**, not merely a dynamical state of perfect conductivity [@problem_id:3001691]. A new [constitutive relation](@entry_id:268485) is required—one that describes the [equilibrium state](@entry_id:270364) itself by directly linking the persistent screening currents to the magnetic field they are canceling.

### The London Equations: A Phenomenological Framework

Fritz and Heinz London proposed a phenomenological theory in 1935 that successfully describes the Meissner effect. Their framework is encapsulated in two equations that govern the behavior of the "superfluid" of condensed charge carriers (Cooper pairs).

#### The First London Equation: Dissipationless Acceleration

The first equation describes the dynamics of the superconducting charge carriers. In an idealized model where these carriers (charge $q$, effective mass $m$) experience no scattering or dissipation, their velocity $\mathbf{v}_s$ under the influence of an electric field $\mathbf{E}$ is governed by Newton's second law, $m d\mathbf{v}_s/dt = q\mathbf{E}$. The supercurrent density is given by $\mathbf{J}_s = n_s q \mathbf{v}_s$, where $n_s$ is the number density of superconducting carriers. Taking the time derivative of $\mathbf{J}_s$ yields the **first London equation**:

$$
\frac{\partial \mathbf{J}_s}{\partial t} = \frac{n_s q^2}{m} \mathbf{E}
$$

This equation states that the supercurrent accelerates in the presence of an electric field, rather than reaching a steady velocity as in a normal conductor with resistance. If a constant DC electric field is applied, the current grows linearly with time, $\mathbf{J}_s(t) \propto t$, implying an infinite DC conductivity [@problem_id:3001720]. While this describes perfect conductivity, it is not, by itself, sufficient to explain the Meissner effect.

#### The Second London Equation: The Essence of Meissner Screening

The first London equation, when combined with Maxwell's equations, leads to the relation $\frac{\partial}{\partial t} ( \nabla \times \mathbf{J}_s + \frac{n_s q^2}{m} \mathbf{B} ) = \mathbf{0}$ [@problem_id:2840809]. This means the quantity in the parenthesis is a constant of motion, determined by the initial conditions of the system—precisely the history dependence that fails to describe the Meissner effect.

The crucial insight of the London theory is to postulate that in thermodynamic equilibrium, this constant must always be zero. This postulate gives the **second London equation**:

$$
\nabla \times \mathbf{J}_s = -\frac{n_s q^2}{m} \mathbf{B}
$$

This equation provides the missing [constitutive relation](@entry_id:268485) for the [equilibrium state](@entry_id:270364). A more profound justification for this equation arises from considering the macroscopic quantum nature of the superconducting condensate [@problem_id:2837249]. The [canonical momentum](@entry_id:155151) of a Cooper pair is $\mathbf{p}_{\text{can}} = m\mathbf{v}_s + q\mathbf{A}$, where $\mathbf{A}$ is the [magnetic vector potential](@entry_id:141246). The phase rigidity of the [macroscopic wavefunction](@entry_id:143853) requires that in a simply connected superconductor, this momentum field must be curl-free, $\nabla \times \mathbf{p}_{\text{can}} = \mathbf{0}$. Expanding this gives $m(\nabla \times \mathbf{v}_s) + q(\nabla \times \mathbf{A}) = \mathbf{0}$. Since $\mathbf{B} = \nabla \times \mathbf{A}$ and $\mathbf{J}_s$ is proportional to $\mathbf{v}_s$, this quantum mechanical constraint leads directly to the second London equation. The negative sign is essential; a positive sign would lead to unphysical solutions where the field grows into the superconductor instead of being expelled.

### Magnetic Field Penetration and Screening

The second London equation, when combined with the static Ampère's law ($\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$), fully determines the magnetostatic response of a superconductor. Taking the curl of Ampère's law and substituting the second London equation, we arrive at the fundamental differential equation for the magnetic field inside a superconductor [@problem_id:2837249]:

$$
\nabla^2 \mathbf{B} = \frac{\mu_0 n_s q^2}{m} \mathbf{B}
$$

This is conventionally written as:

$$
\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}
$$

Here, we have defined a [characteristic length](@entry_id:265857) scale, the **London [penetration depth](@entry_id:136478)**, $\lambda_L$:

$$
\lambda_L = \sqrt{\frac{m}{\mu_0 n_s q^2}}
$$

This parameter quantifies the distance over which an external magnetic field can penetrate into the surface of a superconductor before being screened by supercurrents. Note that its dependence is on the [vacuum permeability](@entry_id:186031) $\mu_0$, not the [permittivity](@entry_id:268350) $\varepsilon_0$, reflecting the magnetic nature of the screening phenomenon [@problem_id:2837249].

For a simple geometry, such as a semi-infinite superconductor occupying the half-space $x>0$ with a magnetic field $B_0 \hat{\mathbf{z}}$ applied parallel to the surface, the equation simplifies to $d^2 B_z/dx^2 = B_z/\lambda_L^2$. The physically acceptable solution, which decays into the bulk and matches the external field at the boundary, is:

$$
B_z(x) = B_0 \exp(-x/\lambda_L)
$$

This [exponential decay](@entry_id:136762) is the mathematical signature of the Meissner effect. The field is not zero immediately at the surface but is expelled from the bulk over a finite length scale $\lambda_L$. This screening is the result of a delicate energetic balance [@problem_id:3001691]. Allowing the field to penetrate costs [magnetic energy density](@entry_id:193006) ($B^2/2\mu_0$), while creating the screening currents costs kinetic energy. The exponential profile represents the minimal total free energy configuration.

### Applications and Refinements of the Local Model

#### Field and Current in a Superconducting Film

The power of the London theory can be demonstrated by analyzing a more [complex geometry](@entry_id:159080), such as a superconducting film of thickness $d$ (from $x=0$ to $x=d$) with a field $H_0 \hat{\mathbf{z}}$ applied at $x0$ and zero external field at $x>d$ [@problem_id:2837251]. The governing equation for the magnetic field $H_z(x)$ inside the film remains $\frac{d^2 H_z}{dx^2} = \frac{1}{\lambda_L^2} H_z$. However, the boundary conditions are now $H_z(0) = H_0$ and $H_z(d)=0$. The solution to this [two-point boundary value problem](@entry_id:272616) is:

$$
H_z(x) = H_0 \frac{\sinh\left((d-x)/\lambda_L\right)}{\sinh\left(d/\lambda_L\right)}
$$

From this field profile, the screening current density can be found using Ampère's law, $\mathbf{J} = \nabla \times \mathbf{H} = -\frac{dH_z}{dx}\hat{\mathbf{y}}$. Evaluating this at the surface $x=0$ gives the magnitude of the [surface current density](@entry_id:274967):

$$
J_{\text{surf}} = |J_y(x=0)| = \frac{H_0}{\lambda_L} \coth\left(\frac{d}{\lambda_L}\right)
$$

In the thick-film limit ($d \gg \lambda_L$), $\coth(d/\lambda_L) \to 1$, and we recover the result for a semi-infinite superconductor, $J_{\text{surf}} = H_0/\lambda_L$. In the thin-film limit ($d \ll \lambda_L$), $\coth(u) \approx 1/u$, so $J_{\text{surf}} \approx \frac{H_0}{\lambda_L} (\frac{\lambda_L}{d}) = \frac{H_0}{d}$. This indicates that the current is distributed almost uniformly through the thin film.

#### The London Gauge and Transverse vs. Longitudinal Response

The gauge-invariant second London equation can be expressed in terms of the [vector potential](@entry_id:153642) $\mathbf{A}$. This leads to the relation $\mathbf{J}_s = -(n_s q^2/m)\mathbf{A}$ provided one works in a specific gauge, known as the **London gauge**, which for a bulk superconductor is defined by $\nabla \cdot \mathbf{A} = 0$ and constraints on the scalar potential [@problem_id:1818570]. This choice simplifies the equations and makes the local, proportional relationship between current and [vector potential](@entry_id:153642) explicit.

It is crucial to understand why London theory focuses on the response to magnetic (transverse) fields while seemingly ignoring electric (longitudinal) effects. The reason lies in the vastly different energy scales of the collective modes [@problem_id:3001717]. A combination of the first London equation, the continuity equation, and Gauss's law shows that any longitudinal charge-density fluctuation $\rho$ oscillates at the very high **[plasma frequency](@entry_id:137429)**, $\omega_p = \sqrt{n_s q^2/(m\varepsilon_0)}$. These [plasmons](@entry_id:146184) have a large energy gap, $\hbar\omega_p$, typically in the ultraviolet range. For low-frequency and static phenomena, these modes are not excited, and the system remains charge-neutral ($\rho \approx 0$). The transverse magnetic response, however, is gapless. Magnetic fields can be screened even at zero frequency. This makes magnetic screening the dominant, low-energy electrodynamic feature of a superconductor.

### Breakdown of the Local Approximation: Nonlocal Electrodynamics

The London theory is a **local theory**; it assumes the current at a point $\mathbf{r}$ is determined solely by the fields at that same point. This is a valid approximation only if the electromagnetic fields vary slowly on the [intrinsic length scale](@entry_id:750789) of superconductivity. This intrinsic scale is the **BCS [coherence length](@entry_id:140689)**, $\xi_0 \approx \hbar v_F / (\pi \Delta_0)$, which represents the spatial extent of a Cooper pair ($v_F$ is the Fermi velocity and $\Delta_0$ is the superconducting energy gap).

When the field variation length (set by $\lambda_L$) is no longer much larger than the pair size $\xi_0$, the local approximation breaks down. The current at $\mathbf{r}$ is more accurately described as an average of the [vector potential](@entry_id:153642) over a neighborhood of size $\xi_0$ around $\mathbf{r}$. This is the domain of **nonlocal electrodynamics**, pioneered by Pippard. The response is described by a convolution in real space, or in Fourier space by a wavevector-dependent kernel $K(\mathbf{q})$:

$$
\mathbf{J}(\mathbf{q}) = -K(\mathbf{q}) \mathbf{A}(\mathbf{q})
$$

The local London theory is the limit $q \to 0$, where $K(\mathbf{q})$ approaches a constant. As the field variation becomes more rapid (increasing $q$), the averaging effect of the finite-sized Cooper pairs washes out the response, so $K(q)$ is a decreasing function of $q$ [@problem_id:3023056]. The first nonlocal correction to the penetration depth can be calculated by expanding the Pippard kernel for small $q$, which yields a wavevector-dependent penetration depth [@problem_id:1096857]:

$$
\lambda(q) \approx \lambda_L \left(1+\frac{\xi_0^2 q^2}{20}\right)
$$

The degree of nonlocality is governed by the ratio of the two fundamental length scales, captured by the **Ginzburg-Landau parameter** $\kappa = \lambda/\xi$.
- For **Type II superconductors**, $\kappa \gg 1$, meaning $\lambda \gg \xi$. The fields vary slowly compared to the pair size, and the local London theory is an excellent approximation.
- For **Type I superconductors**, $\kappa \ll 1$, meaning $\lambda \ll \xi$. The response is strongly nonlocal (Pippard limit), and the London theory is insufficient.

The presence of impurities also dramatically affects locality [@problem_id:2837254] [@problem_id:3023056]. In the **dirty limit**, where the [electron mean free path](@entry_id:185806) $l$ is much shorter than the intrinsic [coherence length](@entry_id:140689) ($l \ll \xi_0$), frequent scattering reduces the effective size of a Cooper pair to $\xi \approx l$. This shortening of the [coherence length](@entry_id:140689) tends to restore locality. In this dirty-local limit, the penetration depth increases, following the relation $\lambda \approx \lambda_L \sqrt{\xi_0 / l}$. Furthermore, a remarkable connection emerges: the [superfluid stiffness](@entry_id:147718), which is proportional to $1/\lambda^2$, becomes directly proportional to the product of the normal-state conductivity $\sigma_n$ and the energy gap $\Delta_0$. It is important to note that this discussion applies to nonmagnetic impurities. According to **Anderson's theorem**, nonmagnetic impurities do not break Cooper pairs and have a minor effect on thermodynamic properties like $T_c$. In contrast, magnetic impurities break time-reversal symmetry, are strong pair-breakers, and rapidly destroy superconductivity.