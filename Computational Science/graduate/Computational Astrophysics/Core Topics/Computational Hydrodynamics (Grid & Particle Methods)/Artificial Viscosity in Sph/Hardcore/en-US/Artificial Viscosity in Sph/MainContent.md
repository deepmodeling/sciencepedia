## Introduction
In many fields of computational science, from engineering to astrophysics, the accurate simulation of fluid dynamics is essential. A central challenge lies in numerically capturing shock waves, where [fluid properties](@entry_id:200256) change discontinuously. Smoothed Particle Hydrodynamics (SPH), a versatile Lagrangian particle-based method, is widely used for such problems but fails in its standard form. This is because its equations are inherently isentropic, contradicting the irreversible, entropy-generating nature of shocks. This failure can lead to unphysical particle interpenetration and simulation instability. This article provides a thorough examination of [artificial viscosity](@entry_id:140376), the standard numerical solution used to resolve this critical issue in SPH.

This article is structured to build your expertise progressively. In the "Principles and Mechanisms" chapter, you will learn why ideal SPH breaks down at shocks and how the Monaghan-Gingold artificial viscosity formulation provides a robust, conservative fix. The "Applications and Interdisciplinary Connections" chapter will then explore the practical use of this method in astrophysics, from gravitational collapse to accretion disks, and discuss its sophisticated extensions to [magnetohydrodynamics](@entry_id:264274) and relativistic regimes, as well as its surprising connections to other scientific fields. Finally, the "Hands-On Practices" section offers concrete problems to solidify your understanding of the method's implementation and its theoretical underpinnings.

## Principles and Mechanisms

The accurate simulation of gas dynamics is a cornerstone of [computational astrophysics](@entry_id:145768), essential for modeling phenomena from [stellar evolution](@entry_id:150430) to the formation of large-scale cosmic structures. A central challenge in this field is the numerical treatment of [shock waves](@entry_id:142404). In Smoothed Particle Hydrodynamics (SPH), a powerful Lagrangian method, the standard formulation derived from the inviscid Euler equations is insufficient to handle the profound physical changes that occur across a shock. This chapter details the fundamental principles necessitating a modification to the ideal SPH equations and elucidates the mechanism of **[artificial viscosity](@entry_id:140376)**, the standard numerical technique employed to resolve this challenge.

### The Challenge of Shocks in Ideal Hydrodynamics

In fluid dynamics, a **shock wave** is an extremely thin region across which fluid properties such as pressure, density, and temperature change abruptly. In the theoretical framework of the inviscid Euler equations, which govern the motion of an ideal, non-viscous, non-conductive fluid, these shocks are modeled as true mathematical discontinuities. The [differential form](@entry_id:174025) of the Euler equations becomes singular and breaks down at such a discontinuity.

However, the underlying physical conservation laws of mass, momentum, and energy remain valid. By applying these laws in their integral form to a small [volume element](@entry_id:267802) that straddles the shock front, one can derive a set of algebraic relations known as the **Rankine–Hugoniot jump conditions**. For a steady, planar shock oriented perpendicular to the $x$-axis, these conditions relate the fluid states upstream (1) and downstream (2) of the shock :

1.  **Mass Conservation:** The mass flux is continuous: $[\rho u] = \rho_2 u_2 - \rho_1 u_1 = 0$.
2.  **Momentum Conservation:** The flux of momentum plus pressure is continuous: $[\rho u^2 + p] = (\rho_2 u_2^2 + p_2) - (\rho_1 u_1^2 + p_1) = 0$.
3.  **Energy Conservation:** The flux of energy is continuous: $[\rho u (e + \frac{1}{2}u^2 + p/\rho)] = 0$, where $e$ is the specific internal energy.

While these equations dictate the conservation of key quantities, they are not sufficient on their own. The mathematics of the Euler equations admits multiple solutions that satisfy the [jump conditions](@entry_id:750965), including unphysical "expansion shocks" where a [rarefaction wave](@entry_id:172838) spontaneously steepens into a discontinuity. Physics provides the crucial selection criterion through the **Second Law of Thermodynamics**. A shock is a fundamentally irreversible process where ordered kinetic energy is dissipated into disordered thermal energy. Consequently, the specific entropy, $s$, of a fluid element must increase as it passes through the shock. This **[entropy condition](@entry_id:166346)**, $s_2 > s_1$, is the definitive characteristic of a physically admissible shock wave and is essential for selecting the unique, correct solution  .

### Why Ideal SPH Fails at Shocks

The standard formulation of SPH is derived from a discrete Lagrangian, a powerful approach that guarantees the conservation of fundamental quantities. For a system of SPH particles, this formalism naturally conserves total mass, [total linear momentum](@entry_id:173071), [total angular momentum](@entry_id:155748), and, crucially, total energy to machine precision . The evolution of a particle's specific internal energy, $u_i$, is coupled to the work done by pressure forces in a way that the total energy, summed over kinetic and internal components, remains constant.

This elegant conservation property, however, leads to a profound problem. The resulting evolution for each SPH particle is **isentropic**, meaning its specific entropy is conserved: $ds_i/dt = 0$ (up to small numerical integration errors). This creates a direct contradiction with the physics of shocks. The purely isentropic nature of ideal SPH cannot produce the mandatory entropy increase required by the Second Law of Thermodynamics .

The numerical consequences of this failure are catastrophic. When particles representing a fluid in a state of compression approach a shock front, the ideal SPH equations provide no mechanism to dissipate their kinetic energy. Instead of decelerating and heating up, the particles would unphysically interpenetrate or "stream" through each other. This leads to a multi-valued velocity field, which is nonsensical for a fluid description, and generates large, [spurious oscillations](@entry_id:152404) in the post-shock region—a numerical artifact akin to the Gibbs phenomenon. Ultimately, the simulation becomes unstable and breaks down  . To build a robust SPH code, a mechanism for controlled, entropy-generating dissipation must be introduced.

### The Concept of Artificial Viscosity

The solution to the problem of shocks in SPH is the introduction of an **[artificial viscosity](@entry_id:140376)** (AV). This is a carefully designed, non-physical term added to the equations of motion with the specific goal of mimicking the dissipative effects of a real shock front. It is crucial to distinguish this numerical construct from the true physical viscosity present in real fluids.

**Physical viscosity**, described by the Navier–Stokes equations, is an intrinsic transport property of a fluid, quantified by coefficients such as the dynamic viscosity, $\mu$. It arises from the microphysical transport of momentum by molecules or ions and produces a stress that opposes velocity gradients. This process operates on microscopic scales, such as the collisional [mean free path](@entry_id:139563) ($l_{\mathrm{mfp}}$), which also sets the physical thickness of a shock front in a collisional gas.

**Artificial viscosity**, in contrast, is a purely numerical device designed for one purpose: robust shock capturing . Its key characteristics are:

-   It is not a model of any microphysical transport coefficient. In most astrophysical contexts, such as the highly diffuse [intergalactic medium](@entry_id:157642) (IGM), the physical Reynolds number is enormous, and physical viscosity is negligible on the scales resolved by a simulation. The AV term does not attempt to model, for example, the complex Braginskii viscosity of a [magnetized plasma](@entry_id:201225) .
-   It operates on the numerical resolution scale of the simulation, typically on the order of the SPH smoothing length, $h$. In almost all astrophysical simulations, this scale is many orders of magnitude larger than the physical mean free path ($h \gg l_{\mathrm{mfp}}$).
-   Its purpose is not to resolve the microscopic internal structure of the shock, but to provide the correct amount of dissipation to ensure that the macroscopic Rankine–Hugoniot jump conditions are satisfied across the numerically broadened shock front.
-   It acts as a **numerical regularization** technique, preventing the unphysical particle interpenetration that would otherwise destroy the simulation at a discontinuity .

The fundamental requirement for any AV scheme is that it must be thermodynamically consistent. In regions of compression where shocks form ($\nabla \cdot \mathbf{v}  0$), the AV term must produce a non-negative heating rate, $Q_{\mathrm{av}} \ge 0$. As the change in specific entropy is given by $T ds/dt = Q_{\mathrm{av}}$, this condition ensures that $ds/dt \ge 0$, in accordance with the Second Law of Thermodynamics. Any scheme that violates this would permit unphysical "cooling shocks" and would be numerically unstable .

### The Mechanism of Artificial Viscosity: The Monaghan-Gingold Formulation

The most widely used implementation of artificial viscosity in SPH is the formulation developed by Monaghan and Gingold. It is constructed as a pairwise interaction that is added to the pressure term in the [momentum equation](@entry_id:197225) and contributes a corresponding heating term in the energy equation.

The core of the method is the pairwise [artificial viscosity](@entry_id:140376) scalar, $\Pi_{ij}$, which acts between particles $i$ and $j$. It is designed to be non-zero only when particles are approaching one another, a condition that serves as a discrete proxy for a compressive flow. This is implemented via the condition $\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$, where $\mathbf{v}_{ij} = \mathbf{v}_i - \mathbf{v}_j$ is the relative velocity and $\mathbf{r}_{ij} = \mathbf{r}_i - \mathbf{r}_j$ is the [separation vector](@entry_id:268468).

The standard form of the Monaghan-Gingold [artificial viscosity](@entry_id:140376) is given by  :
$$
\Pi_{ij} = 
\begin{cases}
\dfrac{-\alpha c_{ij} \mu_{ij} + \beta \mu_{ij}^2}{\rho_{ij}},   \text{if } \mathbf{v}_{ij}\cdot\mathbf{r}_{ij}  0 \\
0,   \text{otherwise}
\end{cases}
$$
Here, the terms are defined as follows:
-   $\mu_{ij} = \dfrac{h_{ij} \mathbf{v}_{ij} \cdot \mathbf{r}_{ij}}{|\mathbf{r}_{ij}|^2 + \eta^2}$ is a dimensionless measure of the compression rate between the particles. Note that for approaching particles, $\mu_{ij}  0$.
-   $\rho_{ij} = \frac{1}{2}(\rho_i + \rho_j)$ is the mean density.
-   $c_{ij} = \frac{1}{2}(c_i + c_j)$ is the mean sound speed.
-   $h_{ij} = \frac{1}{2}(h_i + h_j)$ is the mean smoothing length.
-   $\alpha$ and $\beta$ are [dimensionless parameters](@entry_id:180651), typically of order unity, that control the strength of the viscosity. The linear term, controlled by $\alpha$, acts similarly to a physical [bulk viscosity](@entry_id:187773) and is effective at handling moderate shocks. The quadratic term, controlled by $\beta$, becomes dominant in strong shocks with high Mach numbers and is essential for preventing particle interpenetration .
-   $\eta^2$ is a small regularization parameter (e.g., $\eta^2 \approx 0.01 h_{ij}^2$) that prevents the denominator from becoming zero when particles are very close, ensuring numerical stability .

This viscous term $\Pi_{ij}$ contributes to the [equations of motion](@entry_id:170720) for particle $i$ as follows:

**Momentum Equation:** The contribution to the acceleration is
$$
\left.\dfrac{d\mathbf{v}_i}{dt}\right|_{\mathrm{AV}} = -\sum_j m_j \Pi_{ij} \nabla_i W_{ij}
$$
where $m_j$ is the mass of particle $j$ and $W_{ij}$ is the SPH [smoothing kernel](@entry_id:195877). Since $\Pi_{ij}$ is positive for approaching particles and the kernel gradient $\nabla_i W_{ij}$ points from $i$ to $j$, this term represents a repulsive force that opposes compression, decelerating the particles at the shock front.

**Energy Equation:** The corresponding heating rate for the specific internal energy is
$$
\left.\dfrac{du_i}{dt}\right|_{\mathrm{AV}} = \dfrac{1}{2}\sum_j m_j \Pi_{ij} \mathbf{v}_{ij} \cdot \nabla_i W_{ij}
$$
This term represents the rate of work done by the [viscous force](@entry_id:264591), which correctly converts the dissipated kinetic energy into internal energy (heat). The factor of $\frac{1}{2}$ ensures that the total energy of the interacting pair (and thus the whole system) is conserved. This heating term is what produces the necessary entropy increase across the shock .

This formulation is constructed to be symmetric ($\Pi_{ij} = \Pi_{ji}$), and the resulting pairwise forces are antisymmetric. This symmetry, a discrete analogue of Newton's third law, guarantees that the scheme conserves [total linear momentum](@entry_id:173071) and [total angular momentum](@entry_id:155748), preserving the elegant conservation properties of the underlying SPH method while robustly capturing shocks .

### Advanced Topics and Refinements

While the standard Monaghan-Gingold [artificial viscosity](@entry_id:140376) is a cornerstone of SPH, it has known limitations that have motivated several important refinements.

**Shear Viscosity and Switches**
A significant drawback of the simple compression trigger $\mathbf{v}_{ij} \cdot \mathbf{r}_{ij}  0$ is its tendency to activate in flows with pure shear (where $\nabla \cdot \mathbf{v} = 0$ but $\nabla \times \mathbf{v} \neq 0$), such as a Kelvin-Helmholtz instability. This leads to spurious dissipation that can unphysically damp the growth of such instabilities. To mitigate this, **viscosity switches** have been developed. A common example is the Balsara switch, which multiplies the AV term by a factor $f_i = \frac{|\nabla \cdot \mathbf{v}|_i}{|\nabla \cdot \mathbf{v}|_i + |\nabla \times \mathbf{v}|_i}$. This factor approaches unity in regions of pure compression (shocks) and zero in regions of pure shear or rotation, effectively suppressing viscosity where it is not wanted .

**Signal Velocity**
Modern SPH codes often employ a more physically motivated approach to set the magnitude of the viscosity, based on the concept of a **[signal velocity](@entry_id:261601)**. This is an estimate of the maximum speed at which information can propagate between two particles. For approaching particles, a robust [signal velocity](@entry_id:261601) is defined as :
$$
v_{\text{sig}} = c_i + c_j - \beta' (\mathbf{v}_{ij} \cdot \hat{\mathbf{r}}_{ij})
$$
where $\beta'$ is a dimensionless constant. This expression combines the sound speeds of both particles with a term proportional to their closing velocity, providing a more accurate upper bound on the [characteristic speed](@entry_id:173770) of a compressive wave. In [cosmological simulations](@entry_id:747925), it is critical that the relative velocity $\mathbf{v}_{ij}$ used here is the **[peculiar velocity](@entry_id:157964)** (motion relative to the Hubble flow), ensuring that the uniform [expansion of the universe](@entry_id:160481) does not itself trigger spurious dissipation .

**Time-Dependent Viscosity**
A constant, high value for the viscosity parameter (e.g., $\alpha \sim 1$) is necessary to capture strong shocks, but it can be overly dissipative in other regions. In simulations of subsonic turbulence, for example, a constant high viscosity leads to an artificially low effective Reynolds number, excessively damping the turbulent cascade. This has led to the development of **time-dependent viscosity** schemes. In these methods, each particle $i$ has its own viscosity parameter $\alpha_i(t)$ that evolves in time, decaying in quiescent regions and rapidly increasing in response to a shock trigger (e.g., a strong negative velocity divergence). This allows the simulation to maintain high effective Reynolds numbers in turbulent flows while retaining the ability to capture shocks robustly when they appear .

**Limitations: Contact Discontinuities**
Finally, it is essential to recognize that artificial viscosity is a specialized tool for capturing shocks. It is ineffective at handling another type of hydrodynamic feature: the **[contact discontinuity](@entry_id:194702)**. This is an interface where pressure and velocity are continuous, but density and temperature (and thus entropy) jump. Because the flow is not compressive across a stationary [contact discontinuity](@entry_id:194702), the AV term is not triggered. Standard density-based SPH formulations produce a persistent, spurious pressure gradient or "pressure blip" at these interfaces due to the inconsistent mixing of density and entropy, leading to unphysical surface tension-like forces.

Resolving this issue requires different tools :
-   **Artificial Conductivity (AC):** A term that introduces diffusion of thermal energy or entropy, triggered by sharp gradients in temperature or entropy. This smooths the thermal profile across the contact, resolving the pressure inconsistency.
-   **Pressure-Entropy SPH:** Advanced SPH formulations that are derived from a different Lagrangian or use [iterative methods](@entry_id:139472) to enforce pressure continuity by construction, eliminating the root cause of the pressure blip.

In conclusion, artificial viscosity is an indispensable numerical mechanism that allows the Lagrangian SPH method to successfully simulate the non-isentropic, dissipative physics of [shock waves](@entry_id:142404). While the classic formulation provides a robust foundation, ongoing research and refinement continue to produce more sophisticated schemes that improve accuracy by minimizing dissipation away from shocks and addressing other numerical challenges inherent in the simulation of complex [astrophysical fluid dynamics](@entry_id:189496).