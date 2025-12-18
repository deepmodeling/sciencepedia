## Introduction
Turbulence remains one of the most significant challenges in computational fluid dynamics (CFD), and the closure problem associated with the Reynolds-Averaged Navier–Stokes (RANS) equations is a central hurdle for engineers and scientists. Algebraic eddy-viscosity models represent the first and most fundamental approach to solving this problem. By postulating a direct algebraic link between the unknown Reynolds stresses and the known mean flow gradients, these models offer a computationally inexpensive and robust method for simulating turbulent flows, forming the bedrock of modern [turbulence modeling](@entry_id:151192). However, their simplicity comes with inherent limitations that are crucial to understand for their responsible application.

This article provides a comprehensive examination of algebraic eddy-viscosity models, designed for the graduate-level student or practicing engineer. We will navigate from their conceptual origins to their practical implementation and critical assessment. Across the following chapters, you will gain a deep understanding of this foundational modeling class.

First, in **Principles and Mechanisms**, we will dissect the core concepts, starting with the Boussinesq hypothesis and the eddy viscosity analogy. We will then build up from Prandtl's [mixing-length theory](@entry_id:752030) to a complete two-layer framework, the Cebeci-Smith model, examining the crucial role of near-wall damping functions. The chapter concludes by exposing the fundamental limitations of these models in complex, non-equilibrium flows.

Next, in **Applications and Interdisciplinary Connections**, we will explore the canonical use of these models for wall-bounded flows, their extension to heat and mass transfer problems relevant to thermal and chemical engineering, and their adaptation for challenging regimes like high-speed and [rotating flows](@entry_id:188796). We will also uncover their conceptual connection to other modeling paradigms, such as [subgrid-scale modeling](@entry_id:154587) in Large Eddy Simulation (LES).

Finally, the **Hands-On Practices** section will challenge you to apply this theoretical knowledge. Through a series of guided problems, you will move from deriving the eddy viscosity from first principles to implementing and refining these models in a practical context, solidifying your understanding of their behavior and numerical considerations.

## Principles and Mechanisms

### The Eddy Viscosity Concept and the Boussinesq Hypothesis

In the study of turbulent flows, a central challenge is the closure problem associated with the Reynolds-Averaged Navier–Stokes (RANS) equations. The time-averaging process introduces the Reynolds stress tensor, $-\rho \overline{u_i' u_j'}$ for incompressible flow or $-\overline{\rho u_i'' u_j''}$ for [compressible flow](@entry_id:156141) using Favre averaging, which represents the transport of mean momentum by turbulent fluctuations. Algebraic eddy-viscosity models provide the simplest framework for closing the RANS equations by postulating a constitutive relationship for these unknown stresses.

The foundational concept of these models is the **eddy viscosity**, a heuristic introduced by Joseph Boussinesq in 1877. This concept draws an analogy between the microscopic, [molecular transport](@entry_id:195239) of momentum that gives rise to fluid viscosity and the macroscopic, [convective transport](@entry_id:149512) of momentum by turbulent eddies. While molecular viscosity, $\nu$, is a thermodynamic property of the fluid itself, originating from momentum exchange over the microscopic mean free path of molecules, the eddy viscosity, $\nu_t$, is a property of the *flow*, not the fluid. It represents an effective increase in diffusivity due to the chaotic swirling motions of turbulence, which mix momentum far more efficiently than molecular diffusion.

The dimensions of eddy viscosity and molecular [kinematic viscosity](@entry_id:261275) are identical, $[\nu_t] = [\nu] = L^2 T^{-1}$. However, their physical origins and typical magnitudes differ dramatically in high Reynolds number flows. Through dimensional reasoning, the eddy viscosity can be expected to scale with a characteristic turbulent velocity, $u'$, and a characteristic turbulent length scale, $\ell$:
$$
\nu_t \sim u' \ell
$$
In the outer region of a [turbulent boundary layer](@entry_id:267922), the largest eddies have a size comparable to the boundary-layer thickness, $\ell \sim \mathcal{O}(\delta)$, and the velocity fluctuations are a non-negligible fraction of the freestream speed, $u' \sim \mathcal{O}(0.1 U_e)$. For a typical subsonic aerodynamic flow, such as air at $U_e = 50 \, \mathrm{m/s}$ with a boundary layer thickness of $\delta = 0.02 \, \mathrm{m}$, a representative estimate of the eddy viscosity is $\nu_t \sim (0.1 \times 50 \, \mathrm{m/s}) \times (0.02 \, \mathrm{m}) = 0.1 \, \mathrm{m^2/s}$. Comparing this to the molecular kinematic viscosity of air, $\nu \approx 1.5 \times 10^{-5} \, \mathrm{m^2/s}$, we find that the eddy viscosity is several orders of magnitude larger: $\nu_t / \nu \approx 10^4$. This vast difference underscores why turbulent stresses, not viscous stresses, dominate momentum transport in most regions of a high Reynolds number flow .

The formal link between the Reynolds stresses and the mean flow gradients is the **Boussinesq hypothesis**. In its general form for [compressible flow](@entry_id:156141) using mass-weighted (Favre) averaging, the hypothesis relates the turbulent stress tensor, $\tau_{ij} = -\overline{\rho u_i'' u_j''}$, to the mean [rate-of-strain tensor](@entry_id:260652), $S_{ij}$. The full hypothesis states that the *anisotropic* part of the turbulent stress is proportional to the *deviatoric* part of the mean [strain-rate tensor](@entry_id:266108). A widely used, though formally simplified, version of this relationship is:
$$
\tau_{ij} = 2 \mu_t S_{ij} - \frac{2}{3} \overline{\rho} k \delta_{ij}
$$
Here, $\mu_t = \overline{\rho} \nu_t$ is the dynamic eddy viscosity, $\overline{\rho}$ is the mean density, and $\delta_{ij}$ is the Kronecker delta. The term $S_{ij}$ is the mean strain-rate tensor, defined from the gradients of the Favre-averaged velocity field, $\tilde{u}_i$:
$$
S_{ij} = \frac{1}{2} \left( \frac{\partial \tilde{u}_i}{\partial x_j} + \frac{\partial \tilde{u}_j}{\partial x_i} \right)
$$
The quantity $k$ is the turbulent kinetic energy per unit mass, defined in the Favre-averaged context as $k = \frac{1}{2} \widetilde{u_\ell'' u_\ell''} = \frac{\overline{\rho u_\ell'' u_\ell''}}{2\overline{\rho}}$. The term $-\frac{2}{3} \overline{\rho} k \delta_{ij}$ is the isotropic part of the turbulent stress, which acts as a "turbulent pressure." This simplified form is strictly valid only when the mean flow divergence, $\nabla \cdot \tilde{\boldsymbol{u}}$, is zero, but it is frequently employed in CFD codes for its simplicity . The central task of any algebraic model is to provide a formula for the eddy viscosity, $\mu_t$ or $\nu_t$.

### Zero-Equation Models: The Mixing-Length Hypothesis

Algebraic models are often termed "[zero-equation models](@entry_id:1134180)" because they compute the eddy viscosity from the local mean flow quantities without solving any additional transport differential equations for turbulence variables. The first and most influential of these is **Prandtl's [mixing-length hypothesis](@entry_id:1127966)**.

Prandtl postulated that the turbulent shear stress, analogous to kinetic theory, arises from fluid parcels moving a characteristic distance, the **[mixing length](@entry_id:199968)** $\ell_m$, before mixing with their surroundings. The magnitude of the velocity fluctuation is assumed to scale with the mean velocity change over this distance, $|u'| \sim \ell_m |\partial U/\partial y|$. By equating the Boussinesq hypothesis, $-\overline{u'v'} = \nu_t (\partial U/\partial y)$, with the mixing-length model for the stress, $-\overline{u'v'} = \ell_m^2 (\partial U/\partial y) |\partial U/\partial y|$, we can solve for the eddy viscosity :
$$
\nu_t = \ell_m^2 \left| \frac{\partial U}{\partial y} \right|
$$
This expression provides an algebraic formula for $\nu_t$, but it shifts the closure problem to finding an appropriate model for the mixing length, $\ell_m$.

In the inner region of a [wall-bounded flow](@entry_id:153603), particularly the inertial sublayer (or logarithmic region), the turbulence scales are dictated by the distance from the wall. Prandtl proposed the simple linear relationship:
$$
\ell_m = \kappa y
$$
where $y$ is the distance from the wall and $\kappa$ is a dimensionless constant. This assumption is remarkably powerful. In the inertial sublayer, viscous stresses are negligible and the total shear stress is approximately constant and equal to the wall shear stress, $\tau \approx \tau_w = \rho u_\tau^2$, where $u_\tau$ is the [friction velocity](@entry_id:267882). Combining this with the mixing-length model gives:
$$
\tau_w \approx \rho \nu_t \frac{\partial U}{\partial y} = \rho \left( (\kappa y)^2 \frac{\partial U}{\partial y} \right) \frac{\partial U}{\partial y} = \rho (\kappa y)^2 \left( \frac{\partial U}{\partial y} \right)^2
$$
Solving for the [velocity gradient](@entry_id:261686) yields $\partial U/\partial y = u_\tau / (\kappa y)$. Integrating this expression in non-dimensional wall coordinates ($U^+ = U/u_\tau$, $y^+ = y u_\tau/\nu$) leads directly to the celebrated **logarithmic law of the wall**:
$$
U^+ = \frac{1}{\kappa} \ln(y^+) + B
$$
where $B$ is an integration constant. This derivation reveals a profound connection: the model parameter $\kappa$ is not arbitrary but is fundamentally constrained by experimental data. The slope of the [logarithmic velocity profile](@entry_id:187082) in semi-log coordinates is $1/\kappa$. Decades of experimental measurements show this slope to be approximately $1/0.41$, which fixes the value of the **von Kármán constant** to $\kappa \approx 0.41$ .

### Refining the Model: Near-Wall Behavior and Damping Functions

While the simple [mixing-length model](@entry_id:1127967) $\ell_m = \kappa y$ successfully recovers the logarithmic law, it fails catastrophically near the wall. In the [viscous sublayer](@entry_id:269337) ($y^+ \lesssim 5$), molecular viscosity dominates, and the velocity profile is linear: $U^+ = y^+$. From this, the mean shear is constant, $\partial U/\partial y = u_\tau^2/\nu$. If we apply the undamped [mixing-length model](@entry_id:1127967) $\nu_t = (\kappa y)^2 |\partial U/\partial y|$ in this region, the eddy viscosity becomes:
$$
\nu_t = (\kappa y)^2 \frac{u_\tau^2}{\nu} = \kappa^2 \left( \frac{y u_\tau}{\nu} \right)^2 \nu = \kappa^2 (y^+)^2 \nu
$$
This predicts that the ratio of eddy to molecular viscosity, $\nu_t/\nu = \kappa^2 (y^+)^2$, grows quadratically away from the wall. At the edge of the sublayer, $y^+=5$, the model predicts $\nu_t/\nu \approx (0.41)^2 \times 5^2 \approx 4.2$. This is a stark contradiction, as the viscous sublayer is defined by the condition $\nu_t \ll \nu$. The model unphysically predicts that turbulent transport is dominant where it should be negligible .

The remedy for this deficiency is to introduce a **damping function**, $f_d$, that suppresses the [mixing length](@entry_id:199968) as the wall is approached. The modified mixing length takes the form $\ell_m = \kappa y f_d(y^+)$. A physically correct damping function must satisfy $f_d \to 0$ as $y^+ \to 0$ and $f_d \to 1$ for large $y^+$ to recover the logarithmic law behavior.

A widely-used formulation is the **van Driest damping function**, derived from considering the oscillatory motion of a fluid element near a wall. It can be formally derived by solving a simple first-order relaxation model for the damping function, $\frac{df_d}{dy^+} = \frac{1}{A^+}(1 - f_d)$, with the boundary condition $f_d(0)=0$. The solution to this differential equation is:
$$
f_d(y^+) = 1 - \exp\left(-\frac{y^+}{A^+}\right)
$$
where $A^+$ is an empirical constant, typically set to $A^+ \approx 26$, that defines the thickness of the buffer layer. For small $y^+$, this function has the Taylor expansion $f_d(y^+) \approx y^+/A^+$. Substituting this into the near-wall eddy viscosity formula gives a new scaling:
$$
\frac{\nu_t}{\nu} \sim \kappa^2 (y^+)^2 [f_d(y^+)]^2 \sim \kappa^2 (y^+)^2 \left(\frac{y^+}{A^+}\right)^2 = \frac{\kappa^2}{(A^+)^2} (y^+)^4
$$
This $\nu_t \propto (y^+)^4$ scaling ensures that the eddy viscosity is very strongly suppressed near the wall, guaranteeing that $\nu_t/\nu \ll 1$ in the viscous sublayer and correctly capturing the physics of wall-damping .

### A Complete Algebraic Model: The Cebeci-Smith Formulation

The [mixing-length model](@entry_id:1127967), even with van Driest damping, has another flaw: the eddy viscosity $\nu_t = (\kappa y f_d)^2 |\partial U/\partial y|$ continues to grow with distance from the wall throughout the boundary layer. This is unphysical, as turbulence scales in the outer (wake) region are limited by the [boundary layer thickness](@entry_id:269100) $\delta$. To address this, more complete algebraic models, such as the **Cebeci-Smith model**, employ a two-layer formulation.

1.  **Inner-Layer Formulation ($\mu_t^{\mathrm{in}}$)**: For the region close to the wall, the model uses the Prandtl [mixing-length hypothesis](@entry_id:1127966) with van Driest damping, as developed above:
    $$
    \mu_t^{\mathrm{in}}(y) = \rho \left[ \kappa y \left(1 - \exp\left(-\frac{y^+}{A^+}\right)\right) \right]^2 \left| \frac{\partial U}{\partial y} \right|
    $$

2.  **Outer-Layer Formulation ($\mu_t^{\mathrm{out}}$)**: In the outer region, the eddy viscosity is assumed to reach a constant "plateau" value that scales with outer variables. A common formulation, based on Clauser's work, is:
    $$
    \mu_t^{\mathrm{out}}(y) = C \rho U_e \delta_k
    $$
    where $U_e$ is the velocity at the edge of the boundary layer, $\delta_k$ is the [displacement thickness](@entry_id:154831), and $C$ is an empirical constant (Clauser's constant, typically $\approx 0.0168$). A more general form includes an intermittency or wake function, $W(y/\delta)$, to account for the variation of turbulence across the outer layer. A dimensionally consistent form is $\mu_t^{\mathrm{out}}(y)=\rho U_e \delta W(y/\delta)$.

3.  **Blending**: The inner and outer formulations are combined by taking the minimum value at each point across the boundary layer:
    $$
    \mu_t(y) = \min\left(\mu_t^{\mathrm{in}}(y), \mu_t^{\mathrm{out}}(y)\right)
    $$
This blending ensures that the model correctly uses the damped mixing-length formulation near the wall and transitions to the physically appropriate, capped outer-layer value, preventing the unphysical growth of eddy viscosity far from the wall .

### Fundamental Limitations of Algebraic and Isotropic Models

Despite their elegance and success in simple attached flows, algebraic eddy-viscosity models possess fundamental limitations that render them inaccurate for more complex flows. These limitations stem from two core properties: their **local nature** and their **isotropic assumption**.

#### Limitation 1: Non-Equilibrium and History Effects

Algebraic models are "local" in nature, meaning the eddy viscosity at a streamwise location $x$ is determined solely by the [mean velocity](@entry_id:150038) profile at that same location. They are effectively "amnesiac," having no memory of the upstream flow history. This becomes a critical failure in **non-equilibrium flows**, such as those experiencing strong adverse pressure gradients (APG) leading to separation.

In an APG flow, energetic turbulent eddies are produced in upstream regions of high shear and are then convected downstream into regions of lower shear near the point of separation. This **history effect** or [non-local transport](@entry_id:1128806) sustains a high level of turbulent stress even where the local mean shear, $\partial U/\partial y$, becomes small. A local algebraic model, where $\nu_t \propto |\partial U/\partial y|$, will incorrectly predict that the eddy viscosity and turbulent stresses collapse to zero as the mean shear vanishes. This under-prediction of turbulent mixing makes the boundary layer appear less resistant to the adverse pressure gradient, leading to a systematic and often significant **delay in the predicted onset of [flow separation](@entry_id:143331)**. Capturing these non-local effects requires models that solve transport equations for turbulence quantities (e.g., $k$ and $\epsilon$), which explicitly account for the convection and diffusion of turbulence energy .

#### Limitation 2: Insensitivity to Body Forces and Streamline Curvature

The Boussinesq hypothesis, in its [linear form](@entry_id:751308), posits that the principal axes of the Reynolds stress tensor are co-aligned with those of the mean strain-rate tensor. This is a reasonable approximation in many [simple shear](@entry_id:180497) flows, but it fails in flows subjected to [body forces](@entry_id:174230), such as the Coriolis force in a [rotating frame](@entry_id:155637), or strong streamline curvature.

Consider a [simple shear flow](@entry_id:1131665) in a [rotating frame](@entry_id:155637). The Coriolis force acts directly on the velocity fluctuations, leading to a redistribution of energy among the Reynolds stress components. This causes the principal axes of the true Reynolds stress tensor to rotate away from those of the mean strain-rate tensor. The linear isotropic model, $\tau_{ij}^{\mathrm{dev}} = 2\mu_t S_{ij}$, is structurally incapable of representing this effect, as it rigidly enforces alignment between the two tensors. Its predictions are entirely insensitive to the rate of system rotation, $\Omega$. A dramatic consequence of this failure is the inability to predict **counter-gradient [momentum transport](@entry_id:139628)**. In strongly stabilized (anti-cyclonic) [rotating flows](@entry_id:188796), experiments and higher-fidelity simulations show that the Reynolds shear stress $\overline{u'v'}$ can become positive even when the mean velocity gradient $\partial U/\partial y$ is positive. The linear model, which predicts $-\overline{u'v'} \propto \nu_t (\partial U/\partial y)$, cannot capture this phenomenon without invoking an unphysical negative eddy viscosity, $\nu_t  0$ .

#### Limitation 3: Failure to Capture Anisotropic Normal Stresses

A third critical flaw of the isotropic eddy-viscosity model is its inability to correctly represent [turbulence anisotropy](@entry_id:756224), particularly differences between the normal Reynolds stresses (e.g., $\overline{u'^2}$ vs. $\overline{v'^2}$). This failure is vividly illustrated in the case of [fully developed flow](@entry_id:151791) through a **non-circular duct**, such as one with a square cross-section.

Experimentally, such flows exhibit a weak secondary motion in the cross-plane, with fluid flowing from the center towards the corners along the wall bisectors and returning to the center along the walls. This phenomenon, known as **Prandtl's [secondary flow](@entry_id:194032) of the second kind**, is driven entirely by turbulence. The source term for the mean streamwise vorticity, $\omega_x$, which characterizes this [secondary flow](@entry_id:194032), can be shown to depend on the cross-plane gradients of the Reynolds stresses, specifically the terms $(\overline{u_y^2} - \overline{u_z^2})$ and $\overline{u_y u_z}$.

A linear isotropic model, when applied to the primary streamwise flow, predicts that the normal stresses in the cross-plane are equal: $\overline{u_y^2} = \overline{u_z^2} = \frac{2}{3}k$. It also predicts $\overline{u_y u_z} = 0$. As a result, the source term for streamwise vorticity is identically zero, and the model fundamentally fails to predict the existence of any secondary flow. The real flow is driven by the anisotropy of the normal stresses, which the isotropic model cannot generate. To capture this physics, one must resort to more advanced [closures](@entry_id:747387), such as **[non-linear eddy-viscosity models](@entry_id:752577) (NLEVMs)** or **algebraic Reynolds-stress models (ARSMs)**, which include additional terms that explicitly model the stress anisotropy . These models represent a step up in complexity from the algebraic models discussed in this chapter and bridge the gap toward full Reynolds-stress transport models.