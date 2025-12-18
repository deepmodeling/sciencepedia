## Introduction
The ocean is a fluid in constant motion, characterized by phenomena spanning a vast range of spatial and temporal scales. While [numerical ocean models](@entry_id:1128988) can resolve large-scale currents, they cannot explicitly simulate the small-scale turbulent eddies that are critical for vertical transport of heat, salt, and momentum. The effect of this unresolved turbulence must be represented through approximation, a process known as parameterization. This presents one of the greatest challenges in computational oceanography, as the accuracy of these parameterizations directly governs a model's ability to simulate the ocean's vertical structure, its interaction with the atmosphere, and its role in biogeochemical cycles and the climate system.

This article addresses the fundamental knowledge gap between resolved large-scale dynamics and unresolved turbulent mixing. It provides a comprehensive guide to the theory and practice of vertical mixing parameterization, equipping you with the knowledge to understand, implement, and critically evaluate these crucial model components.

First, the "Principles and Mechanisms" chapter will lay the theoretical groundwork, introducing the turbulence closure problem and the flux-gradient hypothesis. It will explore the core physics governing mixing intensity—the interplay between stabilizing stratification and destabilizing shear—and introduce two canonical parameterization schemes: the K-Profile Parameterization (KPP) and the Mellor-Yamada (MY2.5) closure. Next, in "Applications and Interdisciplinary Connections," we will see how these schemes are applied in practice, influencing everything from boundary layer dynamics to the global Meridional Overturning Circulation, and examine their vital connections to marine biogeochemistry and [climate prediction](@entry_id:184747). Finally, the "Hands-On Practices" section will provide an opportunity to solidify your understanding by tackling practical exercises related to the derivation and implementation of these schemes.

## Principles and Mechanisms

In the preceding chapter, we established that oceanic motions span a vast range of scales, from millimeters to global basins. Numerical ocean models, by necessity, resolve only the larger scales of motion, leaving the effects of smaller-scale processes, particularly turbulent mixing, unresolved. The accurate representation of this sub-grid-scale mixing is one of the most critical challenges in computational oceanography. This chapter delves into the fundamental principles and mechanisms governing the parameterization of vertical turbulent mixing, which profoundly influences the vertical structure of temperature, salinity, and momentum, and thereby regulates ocean-atmosphere exchange, biogeochemical cycles, and large-scale circulation.

### The Closure Problem in Vertical Mixing

The starting point for any numerical ocean model is the set of governing equations for fluid motion (the Navier-Stokes equations) and tracer conservation. To isolate the effects of turbulence, we apply a conceptual decomposition, typically **Reynolds averaging**, to every variable. A variable, such as the horizontal velocity $u$, is split into a slowly varying mean component, $\overline{u}$, and a rapidly fluctuating turbulent component, $u'$. The mean component is what the ocean model resolves, while the turbulent component represents the unresolved motions.

When this averaging is applied to the [nonlinear advection](@entry_id:1128854) terms in the governing equations, new terms arise that represent the net transport by turbulent fluctuations. For a horizontally homogeneous ocean column, the Reynolds-averaged equation for the mean horizontal velocity $\overline{u}(z,t)$ takes the form:

$$
\frac{\partial \overline{u}}{\partial t} - f\overline{v} = -\frac{1}{\rho_0} \frac{\partial \overline{p}}{\partial x} + \frac{\partial}{\partial z} \left( \nu \frac{\partial \overline{u}}{\partial z} - \overline{u'w'} \right)
$$

where $f$ is the Coriolis parameter, $\rho_0$ is a reference density, $\overline{p}$ is the mean pressure, and $\nu$ is the molecular viscosity. The critical new term is $\overline{u'w'}$, known as the **kinematic Reynolds stress**. This term represents the vertical flux of horizontal momentum due to turbulent eddies. Similarly, the equation for a mean passive tracer $\overline{\chi}$ contains a turbulent tracer flux term, $\overline{w'\chi'}$:

$$
\frac{\partial \overline{\chi}}{\partial t} = \frac{\partial}{\partial z} \left( \kappa_\chi \frac{\partial \overline{\chi}}{\partial z} - \overline{w'\chi'} \right)
$$

where $\kappa_\chi$ is the molecular diffusivity of the tracer. 

The appearance of these [second-order correlation](@entry_id:190427) terms, such as $\overline{u'w'}$ and $\overline{w'\chi'}$, in the equations for the mean fields presents a fundamental dilemma. We have more unknown variables than we have equations. The system is not mathematically closed. This is the celebrated **closure problem** of turbulence. To make the system of equations solvable, we must introduce additional assumptions, or a **[turbulence closure](@entry_id:1133490) model**, to parameterize the unknown turbulent fluxes in terms of the known, resolved mean fields. 

The most common and intuitive approach is the **flux-gradient hypothesis**, which posits that turbulent mixing acts like an enhanced form of [molecular diffusion](@entry_id:154595), transporting properties "down" the mean gradient. This is expressed through a linear relationship:

$$
\overline{u'w'} = -K_m \frac{\partial \overline{u}}{\partial z}
$$
$$
\overline{w'\chi'} = -K_\chi \frac{\partial \overline{\chi}}{\partial z}
$$

Here, $K_m$ is the **eddy viscosity** for momentum and $K_\chi$ is the **eddy diffusivity** for the tracer $\chi$. The negative sign is crucial; it ensures that if the mean velocity increases with depth (a positive gradient), the turbulent flux of momentum is negative (downward), acting to smooth out the gradient. Likewise, if a tracer concentration decreases with height (a negative gradient), the [turbulent flux](@entry_id:1133512) is positive (upward), again acting to reduce the gradient.  

It is imperative to distinguish these eddy coefficients from their molecular counterparts. Molecular diffusivity, $\kappa_m$, is an intrinsic property of the fluid, describing transport by the random motion of molecules. Eddy diffusivity, $K$, is a property of the *flow*, representing the transport by coherent, macroscopic fluid parcels (eddies). In a typical active [oceanic boundary layer](@entry_id:1129039), turbulent transport is vastly more efficient than [molecular transport](@entry_id:195239). An order-of-magnitude estimate can be made by scaling $K$ with a characteristic turbulent velocity scale, $u'$, and length scale, $\ell'$, as $K \sim u' \ell'$. For a moderate wind event where the friction velocity is $u_* \approx 10^{-2}\,\mathrm{m\,s^{-1}}$ and a near-surface mixing length is $\ell \approx 0.5\,\mathrm{m}$, the eddy diffusivity is on the order of $K \sim 5 \times 10^{-3}\,\mathrm{m^2\,s^{-1}}$. This is about four to five orders of magnitude larger than the molecular diffusivity for heat in water ($\kappa_m \approx 1.4 \times 10^{-7}\,\mathrm{m^2\,s^{-1}}$). The entire challenge of vertical mixing parameterization lies in determining the physically correct forms for $K_m$ and $K_\chi$ based on the state of the flow. 

### The Role of Stratification and Shear

The intensity of vertical mixing is fundamentally controlled by a competition between mechanical generation of turbulence by [vertical shear](@entry_id:1133795) and the suppression of vertical motion by density stratification.

#### Static Stability and the Brunt-Väisälä Frequency

An essential concept for quantifying stratification is **static stability**. Consider a fluid parcel at rest in a density-[stratified fluid](@entry_id:201059), $\rho(z)$. If the parcel is displaced vertically by a small distance $\eta$ without exchanging heat with its surroundings, it retains its original density. The ambient fluid at the new location has a different density. This density difference creates a [buoyancy force](@entry_id:154088). For a coordinate system where $z$ is positive upward, the vertical [equation of motion](@entry_id:264286) for the parcel, under the Boussinesq approximation, simplifies to the form of a simple harmonic oscillator:

$$
\frac{d^2\eta}{dt^2} + N^2 \eta = 0
$$

The squared frequency of oscillation, $N^2$, is known as the **Brunt-Väisälä frequency** squared, and is defined as:

$$
N^2 = -\frac{g}{\rho_0} \frac{\partial \overline{\rho}}{\partial z}
$$

If density decreases with height ($\partial \overline{\rho}/\partial z  0$), then $N^2 > 0$. In this case, a displaced parcel experiences a restoring [buoyancy force](@entry_id:154088), causing it to oscillate. This is a **stably stratified** fluid. If density were to increase with height ($\partial \overline{\rho}/\partial z > 0$), then $N^2  0$, and any small displacement would grow exponentially. This is an **unstably stratified** fluid, which leads to spontaneous overturning, or convection. For a typical mid-latitude stratification with $\partial \overline{\rho}/\partial z = -0.010\,\mathrm{kg\,m^{-4}}$, the Brunt-Väisälä frequency is $N \approx 9.8 \times 10^{-3}\,\mathrm{s}^{-1}$, corresponding to an oscillation period of about 10 minutes. 

#### Richardson Numbers and the Turbulent Prandtl Number

The competition between the stabilizing effect of buoyancy and the destabilizing effect of [velocity shear](@entry_id:267235) is quantified by the dimensionless **gradient Richardson number**, $Ri_g$:

$$
Ri_g = \frac{N^2}{S^2}
$$

where $S^2 = (\partial \overline{u}/\partial z)^2 + (\partial \overline{v}/\partial z)^2$ is the squared magnitude of the [vertical shear](@entry_id:1133795). A small $Ri_g$ implies that shear dominates, favoring the growth of turbulence. A large $Ri_g$ implies that stratification dominates, suppressing vertical motions and turbulence. All realistic mixing schemes must represent this suppression by making the eddy coefficients, $K_m$ and $K_\chi$, decreasing functions of $Ri_g$. 

A more subtle consequence of stable stratification is its differential impact on the transport of momentum and scalars. Vertical motions ($w'$) are directly suppressed by buoyancy forces. This preferentially [damps](@entry_id:143944) the vertical flux of scalars like buoyancy ($\overline{w'b'}$, where $b$ is buoyancy), which relies entirely on vertical displacements. The vertical flux of horizontal momentum ($\overline{u'w'}$) also depends on $w'$ but is a more complex process. As a result, in stably [stratified flows](@entry_id:265379), turbulence is generally less efficient at transporting scalars vertically than it is at transporting momentum. This implies that the eddy diffusivity for scalars should be smaller than the eddy viscosity for momentum, $K_h  K_m$.

This relationship can be formalized through the Turbulent Kinetic Energy (TKE) budget. The TKE balance includes a production term from shear, $P = K_m S^2$, and a destruction term from buoyancy, $-B = K_h N^2$. The ratio of these terms defines the **flux Richardson number**, $R_f = -B/P$. For turbulence to be sustained, $R_f$ must be below a critical value, typically observed to be $R_f \lesssim 0.2$. From these definitions, we find a direct relationship:

$$
R_f = \frac{K_h N^2}{K_m S^2} = \frac{Ri_g}{Pr_t}
$$

where $Pr_t = K_m/K_h$ is the **turbulent Prandtl number**. The observation that turbulence can persist at gradient Richardson numbers of $Ri_g > 0.25$ (a critical value for [linear instability](@entry_id:1127282)) while requiring $R_f \lesssim 0.2$ provides a powerful argument that $Pr_t$ must be greater than 1 in stable conditions. Both theoretical models and observational data confirm this, showing that $Pr_t$ increases with $Ri_g$. This anisotropic nature of mixing is a key piece of physics that sophisticated parameterizations aim to capture. 

### Key Parameterization Schemes

We now turn to two of the most influential classes of vertical mixing schemes used in ocean models: the K-Profile Parameterization (KPP) and the Mellor-Yamada (MY) [closures](@entry_id:747387). They represent different philosophies for solving the closure problem.

#### The K-Profile Parameterization (KPP): A Boundary Layer Scheme

The K-Profile Parameterization is a **diagnostic** scheme specifically designed to represent the physics of the ocean surface boundary layer. It does not solve [prognostic equations](@entry_id:1130221) for turbulence properties, but rather diagnoses the mixing profile from the mean fields and surface forcing at each time step, making it computationally efficient. Its architecture has several key components. 

First, KPP diagnoses the **boundary layer depth**, $h$. This is accomplished by calculating a **bulk Richardson number**, $Ri_b$, which compares the total buoyancy difference across a layer of depth $d$ relative to the surface with the velocity shear across that same layer. The boundary layer depth $h$ is defined as the depth at which $Ri_b$ first reaches a critical value. This provides a physically-based definition of the extent of the actively mixing surface layer. 

Second, within this boundary layer ($0 \le z \le h$), KPP prescribes a specific shape for the eddy diffusivity profile, $K(z)$. This "K-profile" is a polynomial function of the dimensionless depth $z/h$ that is matched to [surface layer similarity](@entry_id:1132681) theory. The magnitude of the profile is scaled by surface forcing parameters, namely the **[friction velocity](@entry_id:267882)**, $u_* = \sqrt{|\boldsymbol{\tau}|/\rho_0}$, and the **surface buoyancy flux**, $B_0$. The relative importance of wind-forced shear turbulence and buoyancy-driven convective turbulence is determined by the **Monin-Obukhov length**, $L = -u_*^3/(\kappa B_0)$, where $\kappa$ is the von Kármán constant. The K-profile is constructed such that it satisfies the physical constraint $K(0)=0$ and matches smoothly to an interior mixing scheme at the base of the boundary layer, $z=h$.  

Third, and most distinctively, KPP includes a **[nonlocal transport](@entry_id:1128882) term**, $\Gamma(z)$, in its parameterization of scalar fluxes:

$$
\overline{w'\chi'} = -K_\chi(z) \frac{\partial \overline{\chi}}{\partial z} + \Gamma(z)
$$

This term is included only for scalars (like temperature and salinity) and only under unstable, convective conditions ($B_0 > 0$, which corresponds to $L  0$). The justification for this term comes from a fundamental failure of local, flux-gradient models. In a strongly [convective boundary layer](@entry_id:1123026), vigorous mixing by large, coherent plumes can homogenize the interior of the layer, leading to a near-[zero mean](@entry_id:271600) gradient, $\partial \overline{\chi}/\partial z \approx 0$. A purely local model would predict zero flux in this region. However, conservation laws demand a continuous, non-zero flux from the surface to balance the imposed surface forcing. The nonlocal term $\Gamma(z)$ represents the transport by these large plumes, which can carry properties across the boundary layer, sometimes against the local mean gradient (a phenomenon known as **[counter-gradient flux](@entry_id:1123121)**). This term is crucial for accurately simulating the deepening of the mixed layer during surface cooling.  

#### The Mellor-Yamada (MY) Closures: A Local Prognostic Approach

The Mellor-Yamada family of [closures](@entry_id:747387) represents a more general, physics-based approach rooted in simplifications of the full second-[moment equations](@entry_id:149666). We will focus on the widely used Mellor-Yamada Level 2.5 (MY2.5) scheme.

MY2.5 is a **local, prognostic** scheme. It is prognostic because it solves [evolution equations](@entry_id:268137) for two turbulence variables: the [turbulent kinetic energy](@entry_id:262712) (TKE), typically represented by $q^2 = 2 \times \text{TKE}$, and a variable representing the turbulent length scale, $q^2\lambda$, where $\lambda$ is a master mixing length. Solving these additional equations allows the turbulence field to have a "memory" of past forcing, but it also makes the scheme computationally more expensive than diagnostic schemes like KPP.  

The scheme is local because the eddy coefficients at a given depth $z$ are determined by the local values of the prognostic variables ($q, \lambda$) and the local mean gradients ($S, N^2$). The eddy viscosity and diffusivity are given by:

$$
K_m = q \lambda S_m(Ri_g) \quad \text{and} \quad K_h = q \lambda S_h(Ri_g)
$$

The key components here are the **stability functions**, $S_m$ and $S_h$. These are [algebraic functions](@entry_id:187534) of the gradient Richardson number, $Ri_g$, that are derived from the [turbulence closure](@entry_id:1133490) theory. They are designed to encapsulate the physics of [stratified turbulence](@entry_id:1132493), automatically reducing the efficiency of mixing as stability increases (i.e., as $Ri_g$ increases). As discussed previously, the theory also yields $S_m > S_h$ for stable conditions ($Ri_g > 0$), thus correctly producing a turbulent Prandtl number greater than one.  

As a concrete example, to calculate the Reynolds stress $\overline{u'w'}$ at a certain depth using MY2.5, one would perform the following steps :
1.  Obtain the local values of TKE ($k = q^2/2$) and the mixing length $\lambda$ from the prognostic turbulence equations.
2.  Calculate the local mean shear $S$ and [buoyancy frequency](@entry_id:1121933) $N$ from the resolved model fields.
3.  Compute the gradient Richardson number $Ri_g = N^2/S^2$.
4.  Evaluate the [stability function](@entry_id:178107) $S_m(Ri_g)$ using its defined algebraic form.
5.  Calculate the eddy viscosity $K_m = \sqrt{2k} \cdot \lambda \cdot S_m(Ri_g)$.
6.  Finally, compute the stress as $\overline{u'w'} = -K_m (\partial \overline{u}/\partial z)$.

### A Comparative Summary

The KPP and MY2.5 schemes exemplify two distinct and powerful approaches to parameterizing vertical mixing, each with its own philosophy, complexity, and domain of applicability.

| Feature               | K-Profile Parameterization (KPP)                                  | Mellor-Yamada Level 2.5 (MY2.5)                                   |
| --------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Philosophy**        | Boundary Layer Scheme                                             | General Turbulence Closure                                        |
| **Method**            | Diagnostic (algebraic calculation)                                | Prognostic (solves differential equations for TKE, length scale)  |
| **Complexity**        | Computationally cheaper                                           | Computationally more expensive                                    |
| **Locality**          | Hybrid: nonlocal term for scalars in convection, local otherwise  | Purely local                                                      |
| **Key Stability Input** | Bulk Richardson number ($Ri_b$) for boundary layer depth          | Gradient Richardson number ($Ri_g$) for stability functions       |
| **Strengths**         | Accurate simulation of the active surface boundary layer, especially convective deepening and [entrainment](@entry_id:275487). | General applicability, well-suited for stably stratified, shear-driven turbulence in the interior and bottom boundary layers. |
| **Weaknesses**        | Less general; relies on a separate interior mixing scheme.        | Can struggle with strong convection due to the lack of a [nonlocal transport](@entry_id:1128882) mechanism. |

In practice, the choice between these schemes depends on the specific scientific application. KPP's explicit representation of nonlocal transport and its tuning to boundary layer observations often make it the preferred choice for simulating the ocean's response to atmospheric forcing. MY2.5, with its more general formulation based on local TKE budgets, provides a robust framework for a wider range of turbulent regimes, particularly those away from direct surface forcing. Understanding the principles and mechanisms behind both is essential for the modern computational oceanographer. 