## Introduction
Modeling turbulence remains one of the central challenges in [computational fluid dynamics](@entry_id:142614) (CFD). The [time-averaging](@entry_id:267915) process used to derive the Reynolds-Averaged Navier-Stokes (RANS) equations introduces unknown terms, the Reynolds stresses, creating a [closure problem](@entry_id:160656) that must be solved to make the equations predictive. This article explores the foundational approach to this problem: zero-equation mixing-length models. While often superseded by more complex methods in modern industrial practice, these models are indispensable for building a fundamental understanding of the physical reasoning and mathematical structure that underpin all [turbulence modeling](@entry_id:151192). They address the knowledge gap of how to algebraically link the unknown turbulent stresses to the known mean flow quantities in the simplest possible way.

This article is structured to guide you from core concepts to practical application. First, we will delve into the **Principles and Mechanisms**, exploring the Boussinesq hypothesis, Prandtl's [mixing-length theory](@entry_id:752030), and the fundamental physical and mathematical constraints that govern these models. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the model's versatility, showing how it is adapted for complex scenarios in aerodynamics, environmental science, and beyond. Finally, a series of **Hands-On Practices** will provide opportunities to apply these concepts and solidify your understanding through practical problem-solving.

## Principles and Mechanisms

The closure of the Reynolds-Averaged Navier-Stokes (RANS) equations is a central challenge in the simulation of turbulent flows. The process of [time-averaging](@entry_id:267915) the nonlinear Navier-Stokes equations introduces new terms—the Reynolds stresses—which represent the transport of momentum by turbulent fluctuations. To solve the averaged equations, these unknown stresses must be related to the known mean flow quantities. This chapter explores the simplest class of [closures](@entry_id:747387) for this purpose: the zero-equation mixing-length models. These models, while foundational and largely superseded in modern practice by more advanced methods, provide an indispensable pedagogical tool for understanding the core physical principles and mathematical constraints that govern all [turbulence modeling](@entry_id:151192).

### The Boussinesq Hypothesis and the Concept of Eddy Viscosity

The RANS equations for an [incompressible fluid](@entry_id:262924) of constant density $\rho$ contain the Reynolds stress tensor, $-\rho \overline{u'_i u'_j}$, which is symmetric and thus introduces six additional unknown fields to the system of four equations (one continuity, three momentum) . The Boussinesq hypothesis, proposed in 1877 by Joseph Boussinesq, provides the crucial simplifying step for a vast class of turbulence models. It posits that the turbulent stresses, much like viscous stresses in a Newtonian fluid, are linearly proportional to the mean [rate of strain](@entry_id:267998).

This relationship introduces a scalar quantity known as the **turbulent viscosity** or **[eddy viscosity](@entry_id:155814)**, $\mu_t$. The complete hypothesis for the modeled turbulent stress tensor, $\tau_{ij}^t \approx \rho \overline{u'_i u'_j}$, is given by :

$$
\tau_{ij}^t = -2 \mu_t S_{ij} + \frac{2}{3} \rho k \delta_{ij}
$$

Here, $S_{ij} = \frac{1}{2}(\partial_j U_i + \partial_i U_j)$ is the mean [rate-of-strain tensor](@entry_id:260652), $\delta_{ij}$ is the Kronecker delta, and $k = \frac{1}{2}\overline{u'_\ell u'_\ell}$ is the turbulent kinetic energy (TKE) per unit mass. The term $-2\mu_t S_{ij}$ models the anisotropic part of the Reynolds stress, which is responsible for shear production of turbulence. The term $\frac{2}{3}\rho k \delta_{ij}$ represents the isotropic part of the stress, ensuring that the trace of the modeled tensor correctly equals $2\rho k$.

For incompressible flows, where the [continuity equation](@entry_id:145242) is $\partial_i U_i = 0$, the divergence of the isotropic part of the stress tensor becomes the gradient of a scalar: $-\partial_j(\frac{2}{3}\rho k \delta_{ij}) = -\partial_i(\frac{2}{3}\rho k)$. This gradient term can be absorbed into the mean pressure gradient term in the RANS momentum equation by defining a modified or effective pressure, $P^* = P + \frac{2}{3}\rho k$. This is a powerful simplification, as the role of pressure in an incompressible flow is kinematic—its gradient adjusts to enforce the solenoidal velocity constraint—allowing such redefinitions without altering the [velocity field](@entry_id:271461) solution. Consequently, the primary challenge of the Boussinesq hypothesis reduces to finding a model for the kinematic [eddy viscosity](@entry_id:155814), $\nu_t = \mu_t / \rho$ .

### The RANS Model Hierarchy and Zero-Equation Closures

The method used to determine $\nu_t$ defines the complexity and classification of the turbulence model. From [dimensional analysis](@entry_id:140259), $\nu_t$ has units of $[L^2 T^{-1}]$, and must therefore be constructed from a characteristic velocity scale, $V_{turb}$, and a characteristic length scale, $L_{turb}$, of the turbulent eddies: $\nu_t \propto V_{turb} L_{turb}$. The RANS model hierarchy is organized by the number of additional transport partial differential equations (PDEs) solved to determine these scales .

*   **Zero-Equation Models**: These models solve no additional transport PDEs. Both $V_{turb}$ and $L_{turb}$ are determined by purely algebraic expressions based on the local mean flow properties.
*   **One-Equation Models**: These solve one transport PDE for a single turbulence quantity (e.g., TKE, $k$), which provides one scale (typically $V_{turb} \propto \sqrt{k}$), while the other scale ($L_{turb}$) is specified algebraically.
*   **Two-Equation Models**: These solve two transport PDEs for two independent turbulence quantities (e.g., TKE $k$ and its [dissipation rate](@entry_id:748577) $\varepsilon$, or [specific dissipation rate](@entry_id:755157) $\omega$), allowing both the velocity and length scales to be determined dynamically throughout the flow.

Mixing-length models are the canonical example of zero-equation [closures](@entry_id:747387). They provide a closed-form algebraic equation for $\nu_t$, thereby closing the RANS system without increasing the number of PDEs to be solved .

### Prandtl's Mixing-Length Hypothesis

In 1925, Ludwig Prandtl proposed a simple yet powerful physical analogy to model the eddy viscosity. He drew a parallel between the [momentum transport](@entry_id:139628) by [turbulent eddies](@entry_id:266898) and the [momentum transport](@entry_id:139628) by molecules in the [kinetic theory of gases](@entry_id:140543). He introduced the concept of a **[mixing length](@entry_id:199968)**, $l_m$, defined as the characteristic transverse distance a "fluid parcel" or eddy travels before it mixes with its new surroundings and loses its momentum identity .

Consider a [simple shear](@entry_id:180497) flow with [mean velocity](@entry_id:150038) $U(y)$. An eddy displaced from layer $y$ to $y+l_m$ carries with it the [mean velocity](@entry_id:150038) $U(y)$, creating a streamwise velocity fluctuation $u'$ proportional to the velocity difference between the layers, $u' \propto U(y+l_m) - U(y) \approx l_m |\frac{dU}{dy}|$. Prandtl argued that the transverse velocity fluctuation, $v'$, is of the same [order of magnitude](@entry_id:264888). The Reynolds shear stress, $-\rho\overline{u'v'}$, would then be proportional to $\rho (l_m \frac{dU}{dy})^2$. Equating this to the Boussinesq form, $\rho\nu_t \frac{dU}{dy}$, yields the classic mixing-length model for [eddy viscosity](@entry_id:155814):

$$
\nu_t = l_m^2 \left| \frac{dU}{dy} \right|
$$

More generally, for a [three-dimensional flow](@entry_id:265265), the local shear rate is represented by the magnitude of the [strain-rate tensor](@entry_id:266108), $|S| = \sqrt{2 S_{ij} S_{ij}}$. The generalized formula becomes:

$$
\nu_t = l_m^2 |S| = l_m^2 \sqrt{2 S_{ij} S_{ij}}
$$

This formulation is crucial. If the mixing length $l_m$ is prescribed as a known function of position, $l_m(\mathbf{x})$, typically based on geometry (e.g., distance from a wall), then $\nu_t$ becomes an algebraic function of the local [mean velocity](@entry_id:150038) gradients. This closes the RANS equations without any additional [transport equations](@entry_id:756133), fulfilling the definition of a zero-equation model .

### Fundamental Constraints on Eddy Viscosity Models

Any physically meaningful [constitutive model](@entry_id:747751) must satisfy certain fundamental principles, including objectivity and [realizability](@entry_id:193701). These constraints dictate the mathematical structure of the model.

#### Objectivity (Frame Invariance)

A physical model for stress should not depend on the observer's frame of reference, particularly if the frame is undergoing [rigid-body motion](@entry_id:265795) (translation or rotation). This principle is known as **[material frame-indifference](@entry_id:178419)** or **objectivity**. The [velocity gradient tensor](@entry_id:270928), $\partial_j U_i$, is not objective, as it changes under a superimposed rotation. However, its symmetric part, the [strain-rate tensor](@entry_id:266108) $S_{ij}$, is objective, while its antisymmetric part, the rotation-rate tensor $R_{ij}$, is not. For a [turbulence model](@entry_id:203176) to be objective, the eddy viscosity $\nu_t$ must be constructed from objective quantities. The scalar magnitude of the [strain-rate tensor](@entry_id:266108), $|S| = \sqrt{2 S_{ij} S_{ij}}$, is a frame-invariant scalar, whereas the magnitude of the rotation-rate tensor or the full [velocity gradient tensor](@entry_id:270928) are not. This provides the fundamental justification for why [eddy viscosity](@entry_id:155814) models are based on the strain rate, ensuring that the model correctly predicts zero turbulent stress for a pure [solid-body rotation](@entry_id:191086), where there is no deformation .

#### Realizability and Physical Consistency

**Realizability** refers to a set of constraints that ensure a turbulence model does not produce unphysical results. A primary [realizability](@entry_id:193701) condition for eddy viscosity models is that the eddy viscosity must be non-negative: $\nu_t \ge 0$.

This constraint arises directly from the second law of thermodynamics. The production of turbulent kinetic energy, $P_k$, represents the drain of energy from the mean flow into the turbulent cascade, an irreversible process that ultimately results in viscous dissipation and an increase in entropy. This production term is modeled as $P_k = 2\nu_t S_{ij}S_{ij}$. Since the squared norm of the [strain-rate tensor](@entry_id:266108), $S_{ij}S_{ij}$, is always non-negative, the requirement that energy flows from the large scales of the mean flow to the small scales of turbulence ($P_k \ge 0$) directly implies $\nu_t \ge 0$. A naive model that, for instance, made $\nu_t$ proportional to the signed shear rate could produce a negative $\nu_t$ in regions of negative shear. This would unphysically predict a "[backscatter](@entry_id:746639)" of energy from turbulent fluctuations to the mean flow, violating the second law .

Furthermore, a negative $\nu_t$ has catastrophic numerical consequences. The RANS momentum equation is a diffusive system, with an effective viscosity of $(\nu + \nu_t)$. If $\nu_t$ becomes sufficiently negative such that $(\nu + \nu_t)  0$, the governing PDE changes character from a forward-parabolic (diffusive) equation to a backward-parabolic (anti-diffusive) one. Such equations are notoriously ill-posed and lead to the unbounded amplification of [numerical errors](@entry_id:635587), causing immediate solver divergence. The squared term $l_m^2$ and the magnitude $|S|$ in the standard mixing-length formulation are therefore essential for both physical [realizability](@entry_id:193701) and [numerical stability](@entry_id:146550) .

### Application in Wall-Bounded Flows and The van Driest Damping

The primary arena for mixing-length models has been wall-bounded flows, such as boundary layers, pipes, and channels. In the region not immediately adjacent to the wall, [dimensional analysis](@entry_id:140259) suggests the only relevant length scale for eddies is the distance from the wall, $y$. This leads to the simplest and most famous prescription for the [mixing length](@entry_id:199968):

$$
l_m = \kappa y
$$

where $\kappa \approx 0.41$ is the empirical von Kármán constant. When this is combined with the assumptions of a constant-stress layer near the wall where turbulent stresses dominate viscous ones ($-\overline{u'v'} \approx u_\tau^2$), the mixing-length model successfully derives the celebrated **[logarithmic law of the wall](@entry_id:262057)** for the mean [velocity profile](@entry_id:266404), $U^+ = \frac{1}{\kappa} \ln(y^+) + B$ .

However, the simple $l_m = \kappa y$ model has a critical flaw: it does not account for the kinematic damping of eddies by viscosity as the wall is approached. The model predicts a non-zero [mixing length](@entry_id:199968) and [eddy viscosity](@entry_id:155814) at the wall, which is unphysical. To correct this, **van Driest damping** is introduced. This modification multiplies the mixing length by a damping function that forces it to zero at the wall. The standard form is :

$$
l_m = \kappa y \left( 1 - \exp\left(-\frac{y^+}{A^+}\right) \right)
$$

Here, $y^+ = y u_\tau / \nu$ is the non-dimensional wall distance, $u_\tau = \sqrt{\tau_w/\rho}$ is the [friction velocity](@entry_id:267882), and $A^+$ is an empirical constant (typically $A^+ \approx 26$). This function has the correct asymptotic properties:
*   For large $y^+ \gg A^+$, the exponential term vanishes, and the model recovers the logarithmic-layer behavior, $l_m \to \kappa y$.
*   For small $y^+ \to 0$, the damping term behaves as $y^+/A^+$, causing the eddy viscosity to decay rapidly as $\nu_t/\nu \sim (y^+)^4$. This ensures that molecular viscosity dominates in the viscous sublayer, consistent with physical reality .

### Fundamental Limitations and Predictive Failures

While elegant and instructive, zero-equation models suffer from a fundamental limitation that curtails their use in complex engineering flows: they are based on the **[local equilibrium hypothesis](@entry_id:182180)**. By being purely algebraic, they assume that the rates of [turbulence production](@entry_id:189980) and dissipation are in balance at every point in the flow. This implies that the turbulence has no "memory" and adjusts instantaneously to the local mean flow conditions.

This assumption breaks down severely in **non-equilibrium flows**, which are ubiquitous in practice. A key example is flow over an airfoil with an [adverse pressure gradient](@entry_id:276169) leading to separation. In such a flow, turbulence is generated in the high-shear region upstream and is then convected by the mean flow into the separation bubble, where local [mean velocity](@entry_id:150038) gradients are weak. An algebraic model, seeing only the low local shear, will incorrectly predict a very low [eddy viscosity](@entry_id:155814) inside the bubble. It fails to account for the history of the turbulence and its transport via convection. More advanced [one-equation models](@entry_id:275708), which solve a transport PDE for [turbulent kinetic energy](@entry_id:262712), can capture this non-local effect and are therefore far more suitable for [separated flows](@entry_id:754694) .

Even more fundamentally, the standard mixing-length model is constitutionally incapable of predicting the onset of separation ($\tau_w \to 0$). The model's entire near-wall framework, including the van Driest damping, is built upon inner-layer scaling using the [friction velocity](@entry_id:267882) $u_\tau$ and the [wall coordinate](@entry_id:756609) $y^+$. As the wall shear stress $\tau_w$ approaches zero, the scaling velocity $u_\tau$ also goes to zero. This collapses the entire inner-layer coordinate system, making concepts like $y^+$ and the law-of-the-wall ill-defined. The model cannot self-consistently describe a state of zero wall shear because its own mathematical foundation disintegrates in that limit .

### Extensions for Complex Effects

Despite their limitations, the core ideas of algebraic closures can be extended to account for more complex physics, demonstrating their adaptability. For example, in flows subjected to strong system rotation, turbulence is significantly altered. This effect can be introduced into a mixing-length model by modifying $l_m$ with a correction factor that depends on the **Rossby number**, $Ro = |S|/(2|\mathbf{\Omega}|)$, which compares the local shear timescale to the rotation timescale. A physically consistent correction function, guided by more advanced theories like Rapid Distortion Theory (RDT), can suppress the eddy viscosity in rotation-dominated regimes ($Ro \to 0$) and recover the [standard model](@entry_id:137424) in shear-dominated regimes ($Ro \to \infty$), improving predictions for geophysical or [turbomachinery](@entry_id:276962) flows . Such extensions, however, often require case-by-case tuning and highlight the model's lack of universality.