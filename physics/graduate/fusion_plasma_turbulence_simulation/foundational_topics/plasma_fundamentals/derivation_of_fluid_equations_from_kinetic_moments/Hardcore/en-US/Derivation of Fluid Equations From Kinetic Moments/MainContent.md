## Introduction
The behavior of a fusion plasma, a complex system of charged particles governed by [electromagnetic forces](@entry_id:196024), is completely described by kinetic theory. This microscopic description, encapsulated in the [phase-space distribution](@entry_id:151304) function, offers a fundamental understanding but comes at an immense computational cost, making it impractical for simulating the vast range of scales involved in plasma turbulence. To bridge this gap, physicists employ fluid models, which describe the plasma using macroscopic quantities like density, velocity, and pressure. This article provides a comprehensive guide to the systematic derivation of these fluid equations from first principles, addressing the critical challenges that arise in the process.

The article is structured to build a robust understanding from theory to application. The first chapter, "Principles and Mechanisms," lays out the formal procedure of taking [velocity moments](@entry_id:1133763) of the kinetic equation to generate a hierarchy of fluid equations and introduces the fundamental closure problem. The second chapter, "Applications and Interdisciplinary Connections," demonstrates how different closure choices create a spectrum of physical models—from MHD to two-fluid theory—with applications in fusion, astrophysics, and beyond. Finally, the "Hands-On Practices" section offers concrete problems to reinforce these theoretical concepts. We begin by examining the core principles of the moment method, which transforms the microscopic particle distribution into a set of macroscopic fluid fields.

## Principles and Mechanisms

The behavior of a fusion plasma is fundamentally governed by the kinetic theory of its constituent particles—ions and electrons—interacting through long-range [electromagnetic forces](@entry_id:196024). The complete description of this system is contained within the [phase-space distribution](@entry_id:151304) function, $f_s(\mathbf{x}, \mathbf{v}, t)$, for each species $s$. This function represents the [number density](@entry_id:268986) of particles in the six-dimensional phase space of position $\mathbf{x}$ and velocity $\mathbf{v}$. However, solving the kinetic equation (such as the Vlasov or Vlasov-Fokker-Planck equation) for $f_s$ is computationally prohibitive for the vast range of spatial and temporal scales relevant to plasma turbulence. Fluid models offer a computationally tractable alternative by describing the plasma in terms of macroscopic quantities that vary only in space and time. This chapter details the principles and mechanisms by which these fluid equations are systematically derived from the underlying kinetic description through the method of [velocity moments](@entry_id:1133763).

### From Microscopic to Macroscopic: The Concept of Velocity Moments

The transition from a microscopic kinetic description to a macroscopic fluid one is achieved by taking velocity moments of the distribution function $f_s$. This procedure effectively averages over the velocity-space information at each spatial point, yielding fluid fields that represent collective properties of the particles.

The fundamental fields are defined as integrals of $f_s$ over all of velocity space . The first three moments are the most crucial:

*   **Zeroth Moment: Number Density**
    The number of particles per unit volume, or **[number density](@entry_id:268986)**, $n_s(\mathbf{x}, t)$, is the zeroth velocity moment of the distribution function:
    $$
    n_s(\mathbf{x}, t) = \int f_s(\mathbf{x}, \mathbf{v}, t) \, d^3v
    $$

*   **First Moment: Bulk Velocity**
    The first raw moment gives the particle flux density, from which we define the mean or **bulk velocity**, $\mathbf{u}_s(\mathbf{x}, t)$, of the fluid:
    $$
    \mathbf{u}_s(\mathbf{x}, t) = \frac{1}{n_s(\mathbf{x}, t)} \int \mathbf{v} f_s(\mathbf{x}, \mathbf{v}, t) \, d^3v
    $$
    The product $n_s m_s \mathbf{u}_s$ represents the [momentum density](@entry_id:271360) of species $s$.

*   **Second Moment: Pressure Tensor**
    The second moment describes the transport of momentum. It is most physically meaningful when calculated with respect to the bulk velocity. We define the **[peculiar velocity](@entry_id:157964)** as the random velocity of a particle relative to the local fluid flow, $\mathbf{c} = \mathbf{v} - \mathbf{u}_s$. The [second central moment](@entry_id:200758), weighted by mass, defines the **pressure tensor**, $\mathbf{P}_s(\mathbf{x}, t)$:
    $$
    \mathbf{P}_s(\mathbf{x}, t) = m_s \int (\mathbf{v} - \mathbf{u}_s)(\mathbf{v} - \mathbf{u}_s) f_s(\mathbf{x}, \mathbf{v}, t) \, d^3v = m_s \int \mathbf{c}\mathbf{c} f_s(\mathbf{x}, \mathbf{v}, t) \, d^3v
    $$
    The [pressure tensor](@entry_id:147910) represents the flux of momentum due to the random thermal motion of particles in the co-[moving frame](@entry_id:274518) of the fluid. Its diagonal components correspond to the conventional pressures in each direction, while its off-diagonal components represent viscous stresses.

These moments map the intricate dynamics of the six-dimensional phase space onto a set of three-dimensional fluid fields. The evolution of these fields is found by taking moments of the governing kinetic equation itself.

### The Moment Hierarchy: Deriving the Fluid Equations

Let us consider the collisionless Vlasov equation for a species $s$ with mass $m_s$ and charge $q_s$:
$$
\frac{\partial f_s}{\partial t} + \mathbf{v} \cdot \nabla_{\mathbf{x}} f_s + \frac{q_s}{m_s}(\mathbf{E} + \mathbf{v} \times \mathbf{B}) \cdot \nabla_{\mathbf{v}} f_s = 0
$$
An evolution equation for the moment of any quantity $\psi(\mathbf{v})$ is obtained by multiplying the Vlasov equation by $\psi(\mathbf{v})$ and integrating over velocity space. A key mathematical step in this process involves the acceleration term. Let the acceleration be $\mathbf{a}_s = \frac{q_s}{m_s}(\mathbf{E} + \mathbf{v} \times \mathbf{B})$. The integral of the acceleration term is $\int \psi (\mathbf{a}_s \cdot \nabla_{\mathbf{v}} f_s) d^3v$. Using integration by parts (the [divergence theorem](@entry_id:145271) in velocity space), this becomes:
$$
\int \psi (\mathbf{a}_s \cdot \nabla_{\mathbf{v}} f_s) d^3v = \oint_{S_\infty} \psi f_s \mathbf{a}_s \cdot d\mathbf{S}_v - \int f_s \nabla_{\mathbf{v}} \cdot (\psi \mathbf{a}_s) d^3v
$$
where $S_\infty$ is the spherical surface at infinite velocity. For this procedure to be valid, the distribution function $f_s$ must decay sufficiently rapidly as $|\mathbf{v}| \to \infty$ such that the [surface integral](@entry_id:275394), or **boundary term**, vanishes. A [sufficient condition](@entry_id:276242) is that $f_s$ decays faster than $|\mathbf{v}|^{-2}$ . If $f_s$ has non-decaying "tails," as in the case of runaway electrons, this boundary term can be non-zero, representing an unphysical source or sink of particles in the fluid model unless additional physics (like [relativistic effects](@entry_id:150245) or [radiation drag](@entry_id:187967)) is included to suppress these tails .

Assuming the boundary term vanishes, and noting that the [acceleration field](@entry_id:266595) $\mathbf{a}_s$ is divergence-free in velocity space ($\nabla_{\mathbf{v}} \cdot \mathbf{a}_s = 0$), the integral simplifies to a source term for the moment of $\psi$:
$$
\text{Source}_\psi = -\int f_s (\mathbf{a}_s \cdot \nabla_{\mathbf{v}} \psi) d^3v
$$
This general result explains why the [electromagnetic force](@entry_id:276833) has different effects on different moments .

#### Zeroth Moment: The Continuity Equation
For the zeroth moment, we choose $\psi(\mathbf{v}) = 1$. The gradient is $\nabla_{\mathbf{v}}\psi = \mathbf{0}$. Consequently, the source term from the acceleration vanishes identically. The moment of the Vlasov equation becomes:
$$
\frac{\partial}{\partial t} \int f_s d^3v + \nabla_{\mathbf{x}} \cdot \int \mathbf{v} f_s d^3v = 0
$$
Substituting the definitions of $n_s$ and $\mathbf{u}_s$, we obtain the **continuity equation**, which expresses the conservation of particle number:
$$
\frac{\partial n_s}{\partial t} + \nabla \cdot (n_s \mathbf{u}_s) = 0
$$

#### First Moment: The Momentum Equation
For the first moment, we choose $\psi(\mathbf{v}) = m_s\mathbf{v}$. The gradient is the tensor $\nabla_{\mathbf{v}}(m_s\mathbf{v}) = m_s \mathbf{I}$, where $\mathbf{I}$ is the identity tensor. The source term from the acceleration is:
$$
\text{Source}_{m_s\mathbf{v}} = - \int f_s \left(\frac{q_s}{m_s}(\mathbf{E} + \mathbf{v} \times \mathbf{B}) \cdot (m_s \mathbf{I})\right) d^3v = -q_s \int f_s (\mathbf{E} + \mathbf{v} \times \mathbf{B}) d^3v
$$
Evaluating the integral gives $-q_s(n_s \mathbf{E} + n_s \mathbf{u}_s \times \mathbf{B})$, which is the negative of the Lorentz force density. Applying the moment procedure to the full Vlasov equation yields:
$$
\frac{\partial}{\partial t}(m_s n_s \mathbf{u}_s) + \nabla \cdot (m_s \int \mathbf{v}\mathbf{v} f_s d^3v) = q_s n_s (\mathbf{E} + \mathbf{u}_s \times \mathbf{B})
$$
The second term contains the momentum flux tensor, $\int \mathbf{v}\mathbf{v} f_s d^3v$. By substituting $\mathbf{v} = \mathbf{u}_s + \mathbf{c}$, this can be decomposed into the flux of momentum from the [bulk flow](@entry_id:149773) and the flux from random motion: $m_s \int \mathbf{v}\mathbf{v} f_s d^3v = m_s n_s \mathbf{u}_s\mathbf{u}_s + \mathbf{P}_s$. Using the continuity equation to simplify, we arrive at the **momentum equation** :
$$
m_s n_s \left( \frac{\partial \mathbf{u}_s}{\partial t} + \mathbf{u}_s \cdot \nabla \mathbf{u}_s \right) = q_s n_s (\mathbf{E} + \mathbf{u}_s \times \mathbf{B}) - \nabla \cdot \mathbf{P}_s
$$
This equation states that the inertia of the fluid element is balanced by the Lorentz force and the force due to pressure gradients and viscous stresses.

### The Closure Problem: An Unavoidable Challenge

The derivation of the momentum equation reveals a fundamental difficulty. The evolution equation for the first moment ($\mathbf{u}_s$) depends on the second moment ($\mathbf{P}_s$). This pattern persists throughout the hierarchy of [moment equations](@entry_id:149666). If we derive the evolution equation for the pressure tensor $\mathbf{P}_s$ (the second moment), we find that it depends on the third central moment, known as the **heat flux tensor**, $\mathbf{Q}_s$:
$$
\mathbf{Q}_s(\mathbf{x}, t) = m_s \int \mathbf{c}\mathbf{c}\mathbf{c} f_s(\mathbf{x}, \mathbf{v}, t) \, d^3v
$$
The evolution equation for $\mathbf{P}_s$ takes the form :
$$
\frac{\partial \mathbf{P}_s}{\partial t} + \nabla \cdot (\mathbf{u}_s \mathbf{P}_s) + \left[ (\mathbf{P}_s \cdot \nabla)\mathbf{u}_s + ((\mathbf{P}_s \cdot \nabla)\mathbf{u}_s)^T \right] + \nabla \cdot \mathbf{Q}_s = \text{Lorentz terms}
$$
This equation shows that the pressure tensor changes due to convection, pressure-work terms (compression/expansion), and, critically, the divergence of the heat flux tensor, $\nabla \cdot \mathbf{Q}_s$. The evolution of the $n$-th moment always depends on the $(n+1)$-th moment. This infinite chain is known as the **closure problem**.

To create a finite set of equations suitable for simulation, this hierarchy must be truncated at some order. This is achieved by positing a **[closure relation](@entry_id:747393)**—an expression for the highest-order moment in the system in terms of lower-order moments. For example, to close the system at the level of the pressure tensor, one must provide a model for $\mathbf{Q}_s$ in terms of $n_s$, $\mathbf{u}_s$, and $\mathbf{P}_s$.

The act of closure inevitably involves a loss of [physical information](@entry_id:152556). The heat flux tensor describes the transport of thermal energy. A key component of this is the **heat [flux vector](@entry_id:273577)**, $\mathbf{q}_s$, which is the contracted trace of $\mathbf{Q}_s$:
$$
\mathbf{q}_s = \frac{m_s}{2} \int |\mathbf{c}|^2 \mathbf{c} f_s \, d^3v
$$
This vector represents the flux of thermal energy relative to the bulk fluid motion . Truncating the hierarchy by simply setting $\mathbf{Q}_s = \mathbf{0}$ is equivalent to neglecting heat flux, which eliminates the primary fluid pathway for representing crucial kinetic phenomena. These include **[collisionless damping](@entry_id:144163)** (like Landau damping), which is a key mechanism for the dissipation of turbulent energy, and **[nonlocal heat transport](@entry_id:1128880)**, where fast particles carry thermal energy over long distances along magnetic field lines. Therefore, the choice of closure is not merely a mathematical convenience; it determines which physical processes the fluid model is capable of describing .

### Approaches to Closure in Magnetized Plasmas

The choice of closure is highly dependent on the physics of interest, particularly the plasma's collisionality and the strength of the magnetic field.

#### Anisotropic Pressure and Gyrotropy

In a strongly magnetized plasma, particle motion is constrained by the magnetic field lines. Gyromotion is fast, while motion along the field is slower. This naturally leads to an [anisotropic pressure](@entry_id:746456). If the distribution function is symmetric with respect to rotations around the magnetic field direction $\hat{\mathbf{b}} = \mathbf{B}/B$ (a property called **gyrotropy**), the [pressure tensor](@entry_id:147910) simplifies significantly. It can be described by two scalar pressures: the pressure parallel to the magnetic field, $p_{\parallel s}$, and the pressure perpendicular to it, $p_{\perp s}$ .
$$
\mathbf{P}_s = p_{\perp s} (\mathbf{I} - \hat{\mathbf{b}}\hat{\mathbf{b}}) + p_{\parallel s} \hat{\mathbf{b}}\hat{\mathbf{b}}
$$
These scalar pressures are defined as velocity-space moments:
$$
p_{\parallel s} = m_s \int c_{\parallel}^2 f_s \, d^3v \quad \text{and} \quad p_{\perp s} = \frac{m_s}{2} \int c_{\perp}^2 f_s \, d^3v
$$
where $c_\parallel = \mathbf{c} \cdot \hat{\mathbf{b}}$ and $c_\perp$ is the magnitude of the [peculiar velocity](@entry_id:157964) perpendicular to $\hat{\mathbf{b}}$. The factor of $1/2$ for $p_{\perp s}$ arises because the perpendicular pressure is isotropic in the 2D plane perpendicular to $\hat{\mathbf{b}}$.

#### Collisionless and Collisional Closures

In a nearly [collisionless plasma](@entry_id:191924), the evolution of $p_{\parallel s}$ and $p_{\perp s}$ can be approximated by adiabatic invariants. A classic example is the **Chew-Goldberger-Low (CGL)** or double-adiabatic closure, which provides separate [evolution equations](@entry_id:268137) for $p_{\parallel s}$ and $p_{\perp s}$. Using a simpler, isotropic closure, $p_{\text{iso}} = (p_{\parallel s} + 2p_{\perp s})/3$, in a system where pressure is inherently anisotropic can lead to significant errors. For instance, in a tokamak-like magnetic field with curvature, the radial force balance computed with an isotropic pressure model can incorrectly estimate the forces holding the plasma, leading to an error that scales with the plasma pressure and the torus aspect ratio . This highlights the necessity of using [closures](@entry_id:747387) that respect the underlying physics of the system.

Collisions provide a powerful mechanism for closure by driving the distribution function towards a local Maxwellian, which is isotropic. **Pitch-angle scattering**, in particular, efficiently randomizes particle velocity directions, causing the pressure anisotropy to relax towards zero ($p_{\parallel s} \to p_{\perp s}$) on a collisional timescale . In fluid simulations, this effect is modeled using [collision operators](@entry_id:1122657). Simple models like the **Bhatnagar-Gross-Krook (BGK) operator**, $C[f] = -\nu(f - f_M)$, are often employed. By construction, if the target Maxwellian $f_M$ is built from the moments of $f$, the BGK operator conserves particle number, momentum, and energy exactly, making it suitable for fluid [closures](@entry_id:747387). Other operators, like the constant-coefficient **Lenard-Bernstein (LB) operator**, may not conserve momentum or energy and instead model relaxation to a fixed background state, making them less suitable for models of [isolated systems](@entry_id:159201) .

### Coupling to Electromagnetism and Advanced Topics

A complete fluid model requires not only the fluid equations for each species but also Maxwell's equations for the evolution of the electric ($\mathbf{E}$) and magnetic ($\mathbf{B}$) fields. The system is closed by relating the charge and current densities, which are sources in Maxwell's equations, back to the fluid moments. The total current density is $\mathbf{J} = \sum_s q_s n_s \mathbf{u}_s$.

In the low-frequency regime typical of much of fusion plasma turbulence, the displacement current in Ampère's law can be neglected, giving $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$. This directly links the magnetic field to the fluid currents. The electric field is determined by a **generalized Ohm's law**, which is derived from the electron momentum equation. By neglecting electron inertia (due to the small electron mass) but retaining the electron pressure gradient and resistivity, we obtain an expression for $\mathbf{E}$. Substituting this into Faraday's law, $\partial_t \mathbf{B} = -\nabla \times \mathbf{E}$, yields the induction equation that governs the evolution of the magnetic field :
$$
\partial_t \mathbf{B} = \nabla \times \left(\mathbf{u}_i \times \mathbf{B}\right) - \nabla \times \left(\frac{\mathbf{J} \times \mathbf{B}}{e n}\right) + \nabla \times \left(\frac{\nabla p_e}{e n}\right) - \nabla \times \left(\eta \mathbf{J}\right)
$$
This equation includes ideal magnetohydrodynamic (MHD) convection, the Hall effect, the electron pressure (baroclinic) term, and resistivity. It self-consistently couples the magnetic field evolution to the fluid quantities, thereby closing the full system of equations.

Despite their power, it is crucial to recognize the inherent limitations of fluid models. They are, by nature, approximations of the full kinetic reality. These limitations become severe at short spatial scales. For example, in describing drift waves, fluid models fail when the perpendicular wavelength becomes comparable to the ion Larmor radius ($k_\perp \rho_i \sim 1$). The reason is that low-order fluid closures for **Finite Larmor Radius (FLR)** effects, such as the polarization drift and gyroviscous stress, are effectively low-order Taylor expansions of the true kinetic ion response. They cannot capture the non-local averaging effect of the large ion gyromotion, which is accurately described in **[gyrokinetic theory](@entry_id:186998)** by functions like $\Gamma_0(k_\perp^2 \rho_i^2)$. This failure highlights the frontier where fluid models must give way to more fundamental kinetic or gyrokinetic simulations to faithfully capture the plasma dynamics .