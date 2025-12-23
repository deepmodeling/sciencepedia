## Introduction
Simulating the dynamics of multiphase fluids—from the coalescence of raindrops to the intricate patterns formed during [alloy solidification](@entry_id:148532)—presents a formidable challenge in computational science. These systems are characterized by evolving, deforming interfaces whose behavior is governed by a delicate interplay of thermodynamics and fluid mechanics. A central problem is establishing a unified mathematical framework that can consistently capture complex [topological changes](@entry_id:136654) like droplet breakup and merger while remaining true to the fundamental laws of energy conservation and dissipation.

This article addresses this gap by detailing one of the most powerful and elegant approaches: the coupling of phase-field models with the Navier-Stokes equations. This diffuse-interface method avoids the complexities of explicitly tracking sharp boundaries by describing the entire system with a continuous order parameter field. You will learn how this single conceptual shift allows for the derivation of a comprehensive model from first principles.

The following chapters will guide you through this powerful framework. In **Principles and Mechanisms**, we will construct the model from the ground up, starting with the Ginzburg-Landau free energy, deriving the Cahn-Hilliard and Navier-Stokes equations, and establishing the system's thermodynamic consistency. Next, **Applications and Interdisciplinary Connections** will showcase the model's remarkable versatility, demonstrating how it explains phenomena from static [wetting](@entry_id:147044) and [capillarity](@entry_id:144455) to dynamic [pattern formation](@entry_id:139998) in materials science, [geophysics](@entry_id:147342), and chemical engineering. Finally, **Hands-On Practices** will bridge theory and application, presenting computational exercises that tackle key numerical challenges, such as non-dimensionalization and force balance, essential for building a robust multiphase flow solver.

## Principles and Mechanisms

The coupling of [phase-field models](@entry_id:202885) with the Navier-Stokes equations provides a powerful and thermodynamically consistent framework for simulating multiphase flows. This approach, often referred to as a diffuse-interface method, treats the boundary between different fluid phases not as an infinitesimally thin line, but as a continuous, albeit narrow, region where physical properties transition smoothly. The dynamics of this interface and the bulk fluids are governed by a set of coupled partial differential equations derived from the fundamental principles of continuum mechanics and non-equilibrium thermodynamics. This chapter elucidates these core principles and the mechanisms by which they are mathematically formulated.

### Thermodynamic Foundation: The Ginzburg-Landau Free Energy

The cornerstone of the [phase-field method](@entry_id:191689) is the postulation of a total system free energy, typically a **Ginzburg-Landau functional**, which depends on a [scalar field](@entry_id:154310) variable known as the **order parameter**, denoted by $\phi(\mathbf{x}, t)$. For a [binary fluid mixture](@entry_id:1121573), this order parameter serves to distinguish the two components. The total free energy $\mathcal{F}$ of the system in a volume $\Omega$ is expressed as an integral of a free energy density over this volume. This density is composed of two primary contributions: a local bulk energy density and a [gradient energy](@entry_id:1125718) density.

$$
\mathcal{F}[\phi] = \int_{\Omega} \left( W(\phi) + \frac{\kappa}{2} |\nabla \phi|^2 \right) \, \mathrm{d}V
$$

Here, $W(\phi)$ is the **bulk free energy potential**, which describes the thermodynamic preference of the system in a homogeneous state (i.e., where $\phi$ is spatially uniform). The second term, $\frac{\kappa}{2} |\nabla \phi|^2$, is the **[gradient energy](@entry_id:1125718)**, which penalizes spatial variations in the order parameter. The coefficient $\kappa$ is a positive constant related to the interfacial energy.

For a system to exhibit [phase separation](@entry_id:143918), representing two distinct, stable, and coexisting fluid phases, the bulk potential $W(\phi)$ must have a specific form. It must be a **double-well potential** . This means that $W(\phi)$ possesses two local minima at distinct values of the order parameter, say $\phi_a$ and $\phi_b$. Mathematically, for these states to be stable, the first derivative of the potential must vanish, and the second derivative must be positive:

$$
W'(\phi_a) = 0, \quad W''(\phi_a) > 0
$$
$$
W'(\phi_b) = 0, \quad W''(\phi_b) > 0
$$

The condition that the two phases can coexist in equilibrium (i.e., they are equally stable) further requires that their free energy densities be equal: $W(\phi_a) = W(\phi_b)$. A common and analytically convenient choice for such a potential, which we will use for illustrative purposes, is the symmetric quartic potential:

$$
W(\phi) = \frac{\beta}{4} (\phi^2 - 1)^2
$$

In this form, the material parameter $\beta > 0$ controls the height of the energy barrier between the wells. The minima are located at $\phi = -1$ and $\phi = +1$, corresponding to the two pure bulk phases.

The [gradient energy](@entry_id:1125718) term, $\frac{\kappa}{2} |\nabla \phi|^2$, is crucial for establishing a diffuse interface. By assigning an energetic penalty to gradients in $\phi$, the system avoids infinitely sharp transitions between phases. The positive coefficient, $\kappa > 0$, ensures that creating an interface incurs an energy cost, which is the physical origin of **surface tension**. A negative $\kappa$ would lead to an ill-posed model where the system would favor infinitely rapid oscillations in $\phi$ to unboundedly lower its energy . The interplay between the bulk potential, which drives the system towards the pure phase values of $\phi = \pm 1$, and the [gradient energy](@entry_id:1125718), which penalizes the gradients required to transition between these values, results in an equilibrium interface profile with a finite thickness and energy.

### The Order Parameter and Chemical Potential

For a [binary fluid mixture](@entry_id:1121573) of components A and B, the order parameter $\phi$ is typically defined as a normalized difference in their concentrations or volume fractions. If $c_A$ and $c_B$ are the local volume fractions, subject to the incompressibility constraint $c_A + c_B = 1$, a standard definition for $\phi$ is:

$$
\phi = c_A - c_B = 2c_A - 1
$$

With this definition, a state of pure component A ($c_A=1, c_B=0$) corresponds to $\phi = +1$, and a state of pure component B ($c_A=0, c_B=1$) corresponds to $\phi = -1$. The value $\phi=0$ represents a 50/50 mixture. The order parameter is thus a compositional field, not a mechanical one like pressure or a purely geometric one like a [signed-distance function](@entry_id:754834) .

The evolution of the system towards a state of [minimum free energy](@entry_id:169060) is driven by [thermodynamic forces](@entry_id:161907). The primary driving force for mass diffusion is the gradient of the **chemical potential**, $\mu$. The chemical potential is formally defined as the variational (or functional) derivative of the total free energy functional $\mathcal{F}$ with respect to the order parameter $\phi$:

$$
\mu = \frac{\delta \mathcal{F}}{\delta \phi}
$$

This derivative represents the change in the total free energy of the system upon an infinitesimal, local addition of one component at the expense of the other. By applying the [calculus of variations](@entry_id:142234) to the Ginzburg-Landau functional, we can derive an explicit expression for $\mu$ . The procedure, which involves [integration by parts](@entry_id:136350) and assumes that boundary terms vanish (e.g., on a periodic domain), yields:

$$
\mu = \frac{\partial W}{\partial \phi} - \kappa \nabla^2 \phi
$$

This fundamental result reveals that the chemical potential has two components: a local part, $\frac{\partial W}{\partial \phi}$, which depends on the bulk free energy, and a non-local part, $-\kappa \nabla^2 \phi$, which arises from the [gradient energy](@entry_id:1125718) penalty. For the specific quartic potential $W(\phi) = \frac{\beta}{4}(\phi^2-1)^2$, the derivative is $W'(\phi) = \beta(\phi^3-\phi)$, leading to the explicit expression:

$$
\mu = \beta(\phi^3 - \phi) - \kappa \nabla^2 \phi
$$

At thermodynamic equilibrium, the chemical potential must be spatially uniform throughout the system.

### Evolution of the Phase Field: Conserved vs. Non-Conserved Dynamics

Since the order parameter $\phi$ in a [binary fluid mixture](@entry_id:1121573) is directly related to the local concentration of a chemical species, its total amount, $\int_\Omega \phi \, \mathrm{d}V$, must be conserved over time (in the absence of chemical reactions). The evolution equation for $\phi$ must therefore take the form of a conservation law. This is a crucial distinction that separates the correct model for fluid mixtures from other [phase-field models](@entry_id:202885).

The dynamics of a conserved order parameter are described by the **Cahn-Hilliard equation**. This equation can be derived from the general continuity equation for species concentration, $\partial_t \phi + \nabla \cdot \mathbf{J} = 0$, where $\mathbf{J}$ is the total flux of the order parameter . The flux is composed of two parts: an advective flux, $\phi\mathbf{u}$, due to the bulk motion of the fluid with velocity $\mathbf{u}$, and a [diffusive flux](@entry_id:748422), $\mathbf{j}$. According to linear non-equilibrium thermodynamics, the diffusive flux is proportional to the gradient of the chemical potential, $\mathbf{j} = -M \nabla \mu$, where $M > 0$ is the **mobility**. Combining these elements and using the [incompressibility](@entry_id:274914) condition $\nabla \cdot \mathbf{u} = 0$, we arrive at the advected Cahn-Hilliard equation:

$$
\frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi = \nabla \cdot (M \nabla \mu)
$$

The structure of this equation guarantees conservation. Integrating over a domain with no-flux or [periodic boundary conditions](@entry_id:147809), the right-hand side integrates to zero by the [divergence theorem](@entry_id:145271), and the advection term also integrates to zero for a [divergence-free velocity](@entry_id:192418) field. Thus, $\frac{d}{dt}\int_\Omega \phi \, \mathrm{d}V = 0$ . The Cahn-Hilliard equation is a fourth-order partial differential equation in $\phi$, since $\mu$ contains a $\nabla^2 \phi$ term.

It is instructive to contrast this with the dynamics of a [non-conserved order parameter](@entry_id:1128777), described by the **Allen-Cahn equation** . In this case, the rate of change of $\phi$ is directly proportional to the chemical potential itself, not the divergence of its gradient:

$$
\frac{\partial \phi}{\partial t} + \mathbf{u} \cdot \nabla \phi = -\Gamma \mu
$$

where $\Gamma > 0$ is a relaxation coefficient. The Allen-Cahn equation does not conserve the total integral of $\phi$ and is therefore appropriate for modeling phenomena where the order parameter is not a conserved quantity, such as the orientation of crystal lattices or the magnetization in a ferromagnet, but it is not suitable for describing the [phase separation](@entry_id:143918) of a [binary fluid mixture](@entry_id:1121573).

### Coupling to Fluid Dynamics: The Navier-Stokes Equations

The motion of the fluid mixture is governed by the **incompressible Navier-Stokes equations**, which express the [conservation of linear momentum](@entry_id:165717). The crucial step is to incorporate the effects of the phase field and its interface into the momentum balance. The equation takes the general form:

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = \nabla \cdot \boldsymbol{\sigma} + \mathbf{f}_{\mathrm{ext}}
$$

where $\rho$ is the mass density, $\mathbf{u}$ is the velocity, $p$ is the pressure, and $\boldsymbol{\sigma}$ is the total stress tensor. For a multiphase system, the stress tensor is composed of the [isotropic pressure](@entry_id:269937), the viscous stress, and the capillary stress: $\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\sigma}_{\mathrm{visc}} + \boldsymbol{\sigma}_{\mathrm{cap}}$.

The [viscous stress](@entry_id:261328) for a Newtonian fluid is given by $\boldsymbol{\sigma}_{\mathrm{visc}} = 2\eta \mathbf{D}(\mathbf{u})$, where $\eta$ is the dynamic viscosity and $\mathbf{D}(\mathbf{u}) = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^\top)$ is the symmetric rate-of-deformation tensor. In a [two-phase flow](@entry_id:153752), the viscosity may vary with composition, $\eta = \eta(\phi)$. In this case, the viscosity cannot be pulled out of the [divergence operator](@entry_id:265975) in the momentum equation, and the [viscous force](@entry_id:264591) term must be written as $\nabla \cdot (2\eta(\phi)\mathbf{D}(\mathbf{u}))$ .

The key coupling between the phase field and fluid momentum arises from the **[capillary force](@entry_id:181817)**. This force is the mechanical manifestation of surface tension and originates from the free energy associated with the interface. In the phase-field framework, this force can be expressed as a body force density, $\mathbf{f}_{\mathrm{cap}}$, that acts throughout the diffuse interfacial region. A thermodynamically consistent formulation for this force is given by  :

$$
\mathbf{f}_{\mathrm{cap}} = -\phi \nabla \mu
$$

This term, also known as the **Korteweg force**, represents the force exerted on the fluid by the non-uniformities in the chemical potential that define the interface. It drives flows that tend to minimize interfacial area, such as the retraction of a liquid ligament or the [coalescence](@entry_id:147963) of droplets.

Assembling all the components, the momentum equation for the coupled Cahn-Hilliard–Navier–Stokes system is:

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = -\nabla p + \nabla \cdot (2\eta\mathbf{D}(\mathbf{u})) - \phi \nabla \mu
$$

This equation, along with the [incompressibility constraint](@entry_id:750592) $\nabla \cdot \mathbf{u} = 0$, governs the fluid velocity field.

### The Complete System and its Properties

We can now assemble the full Cahn-Hilliard–Navier–Stokes (CH-NS) model, also known as "Model H" in the Hohenberg-Halperin classification. It is a set of four coupled equations for the variables $\phi$, $\mathbf{u}$, $p$, and $\mu$ :

1.  **Incompressibility:** $\nabla \cdot \mathbf{u} = 0$
2.  **Momentum Conservation (Navier-Stokes):** $\rho(\partial_t \mathbf{u} + \mathbf{u}\cdot\nabla \mathbf{u}) = -\nabla p + \nabla\cdot(2\eta\mathbf{D}(\mathbf{u})) - \phi\nabla \mu$
3.  **Order Parameter Conservation (Cahn-Hilliard):** $\partial_t \phi + \mathbf{u}\cdot\nabla \phi = \nabla\cdot(M\nabla \mu)$
4.  **Chemical Potential Definition:** $\mu = W'(\phi) - \kappa\nabla^2 \phi$

#### Thermodynamic Consistency and Energy Dissipation

A defining feature of this system is its inherent [thermodynamic consistency](@entry_id:138886). The total energy of the system, $E = K + \mathcal{F}$, is the sum of the kinetic energy $K = \int_\Omega \frac{1}{2}\rho |\mathbf{u}|^2 \, \mathrm{d}V$ and the mixing free energy $\mathcal{F}$. By deriving the evolution equation for $E$, one can show that the system is dissipative . The time derivative of the total energy is:

$$
\frac{\mathrm{d}E}{\mathrm{d}t} = \frac{\mathrm{d}K}{\mathrm{d}t} + \frac{\mathrm{d}\mathcal{F}}{\mathrm{d}t}
$$

A detailed derivation shows that the capillary force term $-\phi \nabla \mu$ in the momentum equation and the advection term $\mathbf{u} \cdot \nabla \phi$ in the Cahn-Hilliard equation represent a reversible transfer of energy between kinetic and free energy forms. When the total energy balance is computed, these transfer terms exactly cancel each other out. The final result for the rate of change of total energy is:

$$
\frac{\mathrm{d}E}{\mathrm{d}t} = - \int_{\Omega} \left( 2\eta |\mathbf{D}(\mathbf{u})|^2 + M |\nabla \mu|^2 \right) \, \mathrm{d}V
$$

Since $\eta>0$ and $M>0$, the integrand is non-negative. Therefore, $\frac{\mathrm{d}E}{\mathrm{d}t} \le 0$, which demonstrates that the total energy of the [isolated system](@entry_id:142067) can only decrease or remain constant. This energy decay is due to two irreversible dissipative processes: **[viscous dissipation](@entry_id:143708)** in the fluid (the $2\eta|\mathbf{D}|^2$ term) and **diffusive dissipation** from species [interdiffusion](@entry_id:186107) (the $M|\nabla\mu|^2$ term).

#### Physical Interpretation of Model Parameters

The abstract parameters $\kappa$ and $\beta$ in the free energy functional can be directly related to measurable physical properties of the interface: its thickness and surface tension. By analyzing a one-dimensional, stationary, planar interface, we can derive these relationships. The equilibrium profile is found by setting the chemical potential to zero everywhere, $\mu=0$, which yields a solvable ordinary differential equation for $\phi(x)$. The solution for the quartic potential is a hyperbolic tangent profile :

$$
\phi(x) = \tanh\left(\frac{x}{\sqrt{2\kappa/\beta}}\right)
$$

From this profile, we can define a characteristic **interfacial thickness**, $\ell$. For instance, defining $\ell$ as the distance over which $\phi$ changes from -0.9 to +0.9 gives $\ell = 2\sqrt{2\kappa/\beta} \text{arctanh}(0.9) = \sqrt{2}\ln(19)\sqrt{\kappa/\beta}$. Regardless of the specific definition, the thickness scales as:

$$
\ell \propto \sqrt{\frac{\kappa}{\beta}}
$$

The **surface tension**, $\sigma$, is defined as the excess free energy per unit area of the interface. It can be calculated by integrating the excess free energy density, $W(\phi) + \frac{\kappa}{2}(\partial_x\phi)^2$, across the equilibrium profile . This calculation yields the classic result:

$$
\sigma = \frac{2\sqrt{2}}{3} \sqrt{\kappa \beta}
$$

These relations are crucial for calibrating the phase-field model parameters to match the properties of a real physical system.

#### Mechanism of Phase Separation: Spinodal Decomposition

The Cahn-Hilliard equation naturally captures the fundamental mechanism of spontaneous [phase separation](@entry_id:143918) known as **spinodal decomposition**. This can be illustrated via a [linear stability analysis](@entry_id:154985) of the quiescent Cahn-Hilliard equation around a homogeneous, unstable state (e.g., $\phi_0 = 0$) . By analyzing the growth of small sinusoidal perturbations of the form $\exp(\sigma t + i\mathbf{k} \cdot \mathbf{x})$, one can derive a dispersion relation for the growth rate $\sigma$ as a function of the wavenumber $k = |\mathbf{k}|$. For the Ginzburg-Landau model with $W(\phi) = \frac{A}{2}\phi^2 + \frac{B}{4}\phi^4$ (where $A  0$ for an unstable base state), this relation is:

$$
\sigma(k) = -M k^2 (A + \kappa k^2)
$$

This relation shows that for a range of wavenumbers $0  k  \sqrt{-A/\kappa}$, the growth rate $\sigma$ is positive. This means that long-wavelength fluctuations will spontaneously grow exponentially in time, leading to the formation of distinct phase domains. Very short-wavelength fluctuations ($k > \sqrt{-A/\kappa}$) are suppressed by the [gradient energy](@entry_id:1125718) penalty ($\kappa k^2$ term), while very long-wavelength fluctuations ($k \to 0$) grow slowly. This process explains the emergence of [characteristic length scales](@entry_id:266383) during the initial stages of [phase separation](@entry_id:143918), a hallmark of complex fluid dynamics that the CH-NS system is adept at modeling.