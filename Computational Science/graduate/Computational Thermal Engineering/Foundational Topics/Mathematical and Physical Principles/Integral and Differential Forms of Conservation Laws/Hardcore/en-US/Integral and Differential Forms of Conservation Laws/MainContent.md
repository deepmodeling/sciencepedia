## Introduction
The conservation of mass, momentum, and energy constitutes the foundational pillar of computational thermal engineering and continuum mechanics. While the physical principles themselves are intuitive, their mathematical expression takes two distinct but deeply connected forms: the integral and the differential. A thorough understanding of this duality is not just a theoretical exercise; it is essential for developing computational methods that can accurately and robustly simulate complex physical phenomena. The primary challenge addressed in this article is bridging the gap between the global, physically intuitive integral balance and the local, point-wise differential equation, particularly in scenarios where [fluid properties](@entry_id:200256) change abruptly across discontinuities like shock waves.

This article will guide you through the core concepts governing conservation laws. In the **Principles and Mechanisms** section, we will dissect the integral and differential formulations, explore the mathematical link between them via the Divergence Theorem, and establish why the integral form holds primacy for handling discontinuous solutions. We will also examine the necessary [constitutive relations](@entry_id:186508) and the entropy condition required for physical realism. Following this, the **Applications and Interdisciplinary Connections** section will demonstrate the far-reaching impact of these concepts, from classical [gas dynamics](@entry_id:147692) and computational fluid dynamics to surprising applications in traffic flow and [systems biology](@entry_id:148549). Finally, the **Hands-On Practices** section provides exercises to solidify your understanding by applying these principles to practical [numerical verification](@entry_id:156090) and implementation tasks.

## Principles and Mechanisms

The formulation of physical conservation laws is the bedrock of computational [thermal engineering](@entry_id:139895). While the previous chapter introduced the fundamental quantities to be conserved—mass, momentum, and energy—this chapter delves into the mathematical architecture used to express these principles. We will establish the relationship between the macroscopic, **integral form** of conservation laws and their localized, **differential form**. Understanding this relationship is not merely an academic exercise; it is fundamental to constructing numerical methods that are robust, accurate, and physically consistent, especially in the presence of complex phenomena such as shock waves and steep thermal gradients.

### The Integral Form: A Foundation for Conservation

The most fundamental statement of a conservation principle is an integral balance over a finite region of space. This region, known as a **control volume (CV)**, is a conceptually defined volume through which a continuum (a fluid or solid) may flow. The boundary of this volume is its **control surface (CS)**. A control volume, denoted as $V(t)$, is an arbitrary subset of three-dimensional space, and its boundary is $S(t) = \partial V(t)$. The geometry and motion of the control volume are defined by the velocity field of its boundary, $\boldsymbol{u}_{s}(\boldsymbol{x},t)$. We can classify control volumes based on the nature of $\boldsymbol{u}_{s}$:

*   A **fixed control volume** is stationary in the chosen [inertial frame of reference](@entry_id:188136), so $\boldsymbol{u}_{s}(\boldsymbol{x},t) = \boldsymbol{0}$. This is the simplest and most common choice for many analyses.
*   A **[moving control volume](@entry_id:265261)** translates and/or rotates as a rigid body. Its boundary velocity takes the form $\boldsymbol{u}_{s}(\boldsymbol{x},t)=\boldsymbol{U}(t)+\boldsymbol{\Omega}(t)\times\left(\boldsymbol{x}-\boldsymbol{x}_{c}(t)\right)$, where $\boldsymbol{U}(t)$ and $\boldsymbol{\Omega}(t)$ are the translational and angular velocities. The shape of the CV remains constant.
*   A **deforming control volume** changes shape over time, and its boundary velocity $\boldsymbol{u}_{s}(\boldsymbol{x},t)$ does not correspond to simple [rigid-body motion](@entry_id:265795). This is essential for methods like Arbitrary Lagrangian-Eulerian (ALE) simulations.

For any extensive property $\Phi$ whose density is $\phi$ (e.g., for mass, $\phi=\rho$; for momentum, $\phi=\rho\boldsymbol{u}$), the general [integral conservation law](@entry_id:175062) states that the time rate of change of the total amount of the property inside the control volume is equal to the net rate of inflow across the control surface plus the rate of generation within the volume. Mathematically, this is expressed as:
$$
\frac{d}{dt}\int_{V(t)} \phi \,dV = - \oint_{S(t)} \boldsymbol{J} \cdot \boldsymbol{n} \, dS + \int_{V(t)} \Sigma \, dV
$$
Here, $\boldsymbol{J}$ is the flux of $\phi$ across the boundary, $\boldsymbol{n}$ is the outward-pointing [unit normal vector](@entry_id:178851) on the control surface $S(t)$, and $\Sigma$ represents any sources or sinks of the property per unit volume. The flux $\boldsymbol{J}$ typically includes two parts: a convective component due to the bulk motion of the continuum, $\phi\boldsymbol{v}$, and a diffusive component, $\boldsymbol{J}_{d}$, arising from molecular-level transport (e.g., viscous stresses or heat conduction).

The validity of this [integral equation](@entry_id:165305), and our ability to manipulate it, depends on certain mathematical regularity conditions. The formulation implicitly assumes that the control volume's evolution is well-behaved; for instance, it can be described by a sufficiently smooth mapping from a fixed reference domain. Furthermore, the property density $\phi$ and velocity field $\boldsymbol{v}$ must be locally integrable for the integrals to be well-defined. These conditions are formalized in the **Reynolds Transport Theorem**, which provides the rigorous mathematical link between the Lagrangian (following a material particle) and Eulerian (in a fixed or [moving control volume](@entry_id:265261)) descriptions of continuum mechanics. Justifying the differentiation of an integral over a time-dependent domain requires careful assumptions about the smoothness of the domain mapping and the [integrability](@entry_id:142415) of the fields, as explored in  and .

### From Integral to Differential Form: The Localization Process

While the integral form provides a global balance, it is often more convenient to work with a local statement of conservation that applies at every point in the domain. This **[differential form](@entry_id:174025)** is derived from the integral form through a process called localization.

Let us consider a fixed control volume $V$ for simplicity ($\boldsymbol{u}_s = \boldsymbol{0}$). The integral law becomes:
$$
\frac{d}{dt}\int_{V} \phi \,dV = - \oint_{S} (\phi\boldsymbol{v} + \boldsymbol{J}_d) \cdot \boldsymbol{n} \, dS + \int_{V} \Sigma \, dV
$$
Assuming the fields are sufficiently smooth, we can apply two key mathematical theorems. First, the Leibniz integral rule allows us to move the time derivative inside the integral for a fixed volume:
$$
\frac{d}{dt}\int_{V} \phi \,dV = \int_{V} \frac{\partial \phi}{\partial t} \,dV
$$
Second, the **Divergence Theorem** (or Gauss's theorem) allows us to convert the [surface integral](@entry_id:275394) of the flux into a [volume integral](@entry_id:265381) of its divergence:
$$
- \oint_{S} (\phi\boldsymbol{v} + \boldsymbol{J}_d) \cdot \boldsymbol{n} \, dS = - \int_{V} \nabla \cdot (\phi\boldsymbol{v} + \boldsymbol{J}_d) \,dV
$$
Substituting these back into the integral law, we can collect all terms under a single [volume integral](@entry_id:265381):
$$
\int_{V} \left( \frac{\partial \phi}{\partial t} + \nabla \cdot (\phi\boldsymbol{v}) + \nabla \cdot \boldsymbol{J}_d - \Sigma \right) dV = 0
$$
Since this equation must hold for *any* arbitrary control volume $V$, and assuming the integrand is a continuous function, the integrand itself must be identically zero at every point. This yields the general [differential conservation law](@entry_id:166470):
$$
\frac{\partial \phi}{\partial t} + \nabla \cdot (\phi\boldsymbol{v} + \boldsymbol{J}_d) = \Sigma
$$
This is a partial differential equation (PDE) that describes the local balance of the quantity $\phi$.

### The Primacy of the Integral Form: Discontinuities and Weak Solutions

The derivation of the [differential form](@entry_id:174025) relied on the assumption of smoothness, allowing the application of the [divergence theorem](@entry_id:145271) and the localization argument. However, many [critical phenomena](@entry_id:144727) in thermal engineering, such as shock waves in compressible flow or phase-change fronts, involve sharp **discontinuities** where properties like density, pressure, and velocity are not differentiable. At such a discontinuity, the [differential form](@entry_id:174025) of the conservation law is formally invalid and meaningless.

In contrast, the integral form remains valid even when the solution is discontinuous. A function that satisfies the [integral conservation law](@entry_id:175062) across a domain containing discontinuities is known as a **[weak solution](@entry_id:146017)**. The correct physical behavior at a discontinuity, such as the propagation speed of a shock wave (governed by the Rankine-Hugoniot conditions), is a direct consequence of the integral balance.

This distinction is of paramount importance for numerical methods. Consider the 1D compressible Euler equations discretized on a uniform grid. A **conservative finite volume scheme** is formulated by applying the integral law to each grid cell (control volume) :
$$
\frac{\mathrm{d}\bar U_{i}}{\mathrm{d}t} = -\frac{1}{\Delta x}\left(\hat F_{i+\frac{1}{2}} - \hat F_{i-\frac{1}{2}}\right)
$$
where $\bar U_i$ is the average of the [conserved variables](@entry_id:747720) (e.g., density, momentum, total energy) in cell $i$, and $\hat F_{i\pm1/2}$ are the [numerical fluxes](@entry_id:752791) at the cell interfaces. When these equations are summed over a block of cells, the internal fluxes cancel out in a **[telescoping sum](@entry_id:262349)**. This guarantees that the total amount of the conserved quantity in the block changes only due to the fluxes at the outer boundaries, perfectly mimicking the physical integral law. The Lax-Wendroff theorem states that if such a conservative scheme converges as the mesh is refined, it converges to a [weak solution](@entry_id:146017) of the conservation law, thereby capturing discontinuities with the correct physical properties.

Conversely, one could attempt to discretize a non-conservative, or quasilinear, form of the equations, often written in terms of primitive variables like velocity $u$ and pressure $p$. Such forms are derived from the conservative PDE using the chain rule (e.g., $\frac{\partial F}{\partial x} = \frac{\partial F}{\partial W}\frac{\partial W}{\partial x}$). This manipulation is invalid across a discontinuity. A numerical scheme based on this [non-conservative form](@entry_id:752551) will not have the telescoping flux property and will generally converge to a solution with incorrect shock speeds, as it does not enforce the fundamental integral balance . Therefore, for problems involving shocks or other discontinuities, it is essential to use numerical methods founded on the integral conservative form of the governing equations.

### Closing the System: Constitutive Relations

The conservation laws for mass, momentum, and energy form an incomplete system of equations; they contain more unknowns than equations. To achieve closure, we must introduce **[constitutive relations](@entry_id:186508)**, which are empirically or theoretically derived models that describe the material's response to thermodynamic and mechanical stimuli. These relations connect quantities like stress and heat flux to the primary field variables.

#### Viscous Stress in a Newtonian Fluid

The momentum equation involves the divergence of the Cauchy stress tensor, $\boldsymbol{\sigma}$. For a fluid, this tensor is commonly decomposed into an [isotropic pressure](@entry_id:269937) part and a [viscous stress](@entry_id:261328) part, $\boldsymbol{\tau}$:
$$
\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}
$$
For a **Newtonian fluid**, the [viscous stress](@entry_id:261328) is assumed to be a linear, isotropic function of the rate-of-deformation tensor, $\mathbf{D} = \frac{1}{2}\left(\nabla\mathbf{u}+(\nabla\mathbf{u})^{T}\right)$. The most general such relation introduces two viscosity coefficients, the shear viscosity $\mu$ and the [second viscosity](@entry_id:189253) coefficient $\lambda$:
$$
\boldsymbol{\tau} = \lambda (\nabla \cdot \boldsymbol{u}) \mathbf{I} + 2\mu \mathbf{D}
$$
A common simplification is the **Stokes hypothesis**, which posits that the **[bulk viscosity](@entry_id:187773)**, $\zeta = \lambda + \frac{2}{3}\mu$, is zero. This implies $\lambda = -\frac{2}{3}\mu$. Under this assumption, the [constitutive relation](@entry_id:268485) becomes:
$$
\boldsymbol{\tau} = \mu\left(\nabla\mathbf{u}+(\nabla\mathbf{u})^{T}\right) - \frac{2}{3}\mu(\nabla\cdot\mathbf{u})\mathbf{I}
$$
It is crucial to recognize the limits of this hypothesis . The bulk viscosity relates to dissipative mechanisms that occur during rapid volume changes, often due to finite relaxation times of internal [molecular energy](@entry_id:190933) modes (rotation, vibration). The Stokes hypothesis ($\zeta=0$) is an excellent approximation for monatomic gases (like argon or helium), which lack these internal modes. However, it is generally invalid for polyatomic gases (like air or carbon dioxide), most liquids (where $\zeta$ can be several times larger than $\mu$), and in any flow with very high-frequency oscillations or strong compression, such as within a shock wave.

#### Conductive Heat Flux and Fourier's Law

The [energy equation](@entry_id:156281) contains the heat [flux vector](@entry_id:273577), $\mathbf{q}$. The most widely used [constitutive relation](@entry_id:268485) for heat conduction is **Fourier's law**:
$$
\mathbf{q} = -k \nabla T
$$
where $k$ is the thermal conductivity and $T$ is the temperature. While seemingly simple, the validity of this law rests on several profound physical assumptions :

1.  **Local Thermodynamic Equilibrium (LTE)**: This assumes that at a small enough scale (a "point" in the continuum sense), a unique, well-defined temperature $T(\boldsymbol{x}, t)$ exists, and all other thermodynamic properties (like internal energy $u$) are unique functions of this local state. This allows us to write the energy storage term as $\rho c \frac{\partial T}{\partial t}$.

2.  **Spatial Scale Separation**: Fourier's law is a continuum concept. It is valid only when the characteristic length scale of the temperature gradient, $L_T$, is much larger than the mean free path, $\lambda$, of the [energy carriers](@entry_id:1124453) (e.g., molecules, phonons, electrons). This condition, often expressed via the Knudsen number, $\text{Kn} = \lambda/L_T \ll 1$, ensures that transport is diffusive. When this assumption fails (e.g., in [nanomaterials](@entry_id:150391) or rarefied gases), Fourier's law is invalid, and more fundamental models like the Boltzmann transport equation are required.

3.  **Temporal Scale Separation**: Fourier's law implies an instantaneous response of the heat flux to a temperature gradient. In reality, there is a finite relaxation time, $\tau_q$, for the heat carriers to adjust. The law is only valid when the macroscopic timescale of the thermal problem, $t_{\text{macro}}$, is much longer than this relaxation time ($\tau_q \ll t_{\text{macro}}$). For extremely fast thermal transients (e.g., pulsed laser heating), this assumption can break down, leading to wave-like (hyperbolic) heat propagation rather than the standard diffusive (parabolic) behavior.

### Energy Equation Dynamics: Viscous Work versus Viscous Dissipation

A subtle but important aspect of the energy conservation law is the role of viscous forces. Two distinct but related terms arise in the analysis: the divergence of the viscous work flux, $\nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u})$, and the viscous dissipation function, $\boldsymbol{\tau}:\nabla\mathbf{u}$.

In the **conservative [total energy equation](@entry_id:1133263)**, derived directly from the [first law of thermodynamics](@entry_id:146485), the effect of viscous stresses appears as a source term representing the rate of work done by [viscous forces](@entry_id:263294) on the fluid, $\nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u})$. This term is the divergence of the viscous work flux vector, $\boldsymbol{\tau}\cdot\mathbf{u}$ .
$$
\frac{\partial (\rho E)}{\partial t} + \nabla\cdot(\rho E \mathbf{u}) = - \nabla\cdot(p\mathbf{u}) - \nabla\cdot\mathbf{q} + \nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u}) + \rho\mathbf{f}\cdot\mathbf{u}
$$
This equation governs the total energy $E = e + \frac{1}{2}|\mathbf{u}|^2$, which includes both internal and kinetic energy.

To understand how this work is partitioned between kinetic and internal energy, we must derive the **internal [energy equation](@entry_id:156281)**. This is accomplished by subtracting the mechanical energy equation (found by taking the dot product of the momentum equation with the velocity vector $\mathbf{u}$) from the [total energy equation](@entry_id:1133263). This derivation relies on the vector calculus identity:
$$
\nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u}) = \mathbf{u}\cdot(\nabla\cdot\boldsymbol{\tau}) + \boldsymbol{\tau}:\nabla\mathbf{u}
$$
After algebraic manipulation, the resulting internal [energy equation](@entry_id:156281) contains a new term, the **[viscous dissipation](@entry_id:143708)**, $\Phi_v = \boldsymbol{\tau}:\nabla\mathbf{u}$ :
$$
\rho\frac{De}{Dt} = -p(\nabla\cdot\mathbf{u}) - \nabla\cdot\mathbf{q} + \boldsymbol{\tau}:\nabla\mathbf{u}
$$
The term $\boldsymbol{\tau}:\nabla\mathbf{u}$ represents the rate per unit volume at which mechanical energy is irreversibly converted into internal energy due to viscous action—in essence, heating due to friction. It is a strictly non-negative source term for internal energy. The distinction is critical: $\nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u})$ is the net rate of work done by viscous stresses, which can change both kinetic and internal energy, while $\boldsymbol{\tau}:\nabla\mathbf{u}$ is specifically the portion of that work that is dissipated as heat. For a closed, adiabatic domain with no-slip walls, the net viscous work done on the boundary is zero ($\mathbf{u}=\mathbf{0}$), and the integral of $\nabla\cdot(\boldsymbol{\tau}\cdot\mathbf{u})$ over the volume vanishes. Total energy is conserved, and viscous dissipation merely acts to convert kinetic energy into internal energy within the domain.

### Physical Admissibility and Numerical Stability: The Entropy Condition

For [hyperbolic conservation laws](@entry_id:147752), such as the Euler equations, mathematical solutions to the integral form (weak solutions) are not necessarily unique. For example, a single initial condition can lead to either a shock wave or a non-physical expansion wave. To select the physically correct solution, an additional constraint is needed: the Second Law of Thermodynamics.

This is enforced through a mathematical **[entropy inequality](@entry_id:184404)**. For a convex entropy function $U(\boldsymbol{u})$ with a corresponding entropy flux $\boldsymbol{\Psi}(\boldsymbol{u})$, any physically admissible solution must satisfy:
$$
\frac{\partial U(\boldsymbol{u})}{\partial t} + \nabla \cdot \boldsymbol{\Psi}(\boldsymbol{u}) \le 0
$$
This inequality states that the total entropy in a [closed system](@entry_id:139565) can only increase (or stay constant for [reversible processes](@entry_id:276625)). For the Euler equations, the mathematical [entropy production](@entry_id:141771) must be non-negative at shocks.

This physical principle has profound implications for numerical methods. A conservative scheme that converges to a [weak solution](@entry_id:146017) is not enough; it must converge to the unique, physically correct, entropy-satisfying solution. Modern [numerical schemes](@entry_id:752822) are designed to be **entropy stable**, meaning they contain a discrete mechanism that prevents the violation of the Second Law. This is typically achieved by designing [numerical flux](@entry_id:145174) functions that have the correct dissipative properties . An **entropy-stable flux** is often constructed by adding a carefully calibrated numerical dissipation matrix to an underlying **entropy-conservative flux**. The conservative part ensures entropy is conserved in smooth regions, while the dissipative part guarantees that entropy is correctly produced at discontinuities like shocks. Advanced frameworks, such as those combining [summation-by-parts](@entry_id:755630) (SBP) operators with simultaneous-approximation-term (SAT) penalties, provide a rigorous path to constructing high-order, provably [entropy-stable schemes](@entry_id:749017) for complex systems like the Navier-Stokes equations, ensuring that simulations are not only accurate but also physically and thermodynamically consistent .