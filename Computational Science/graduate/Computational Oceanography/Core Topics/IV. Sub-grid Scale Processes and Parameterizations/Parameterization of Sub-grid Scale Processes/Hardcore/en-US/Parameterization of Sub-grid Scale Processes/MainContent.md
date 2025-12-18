## Introduction
The predictive power of modern computational oceanography hinges on a single, fundamental challenge: how to account for physical processes that are too small or too fast to be explicitly resolved by a numerical model. These sub-grid scale (SGS) processes, from turbulent eddies to convective plumes, exert a crucial influence on the large-scale ocean circulation, water mass properties, and the global climate system. Failure to represent their effects leads to models that are not only inaccurate but physically inconsistent. The core difficulty lies in the "closure problem"—the fact that filtering the governing equations of fluid motion introduces new, unknown terms representing the impact of these unresolved scales. The science of parameterization is dedicated to closing this gap by positing physically-grounded relationships between the unknown sub-grid effects and the known, resolved state of the fluid.

This article provides a comprehensive overview of the theory and practice of SGS parameterization. Across three chapters, you will build a foundational understanding of this [critical field](@entry_id:143575). First, **Principles and Mechanisms** will delve into the mathematical origins of the closure problem, introduce foundational concepts like the [eddy viscosity hypothesis](@entry_id:1124144), and discuss the fundamental physical constraints, such as energy conservation, that any valid parameterization must obey. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles are put into practice, exploring core parameterization schemes used in ocean modeling (like GM/Redi and KPP) and examining advanced stochastic and machine learning methods. Finally, **Hands-On Practices** will offer a set of practical exercises to solidify your understanding of [model resolution](@entry_id:752082), the pitfalls of numerical mixing, and the challenges of implementing data-driven [closures](@entry_id:747387).

## Principles and Mechanisms

The equations governing fluid motion, such as the Navier-Stokes equations, are valid at all scales, from the vast oceanic gyres down to the smallest turbulent whorls where energy is dissipated into heat. However, computational models of the ocean, by their very nature, can only represent phenomena occurring on scales larger than their grid resolution. This fundamental limitation necessitates a strategy for accounting for the influence of the unresolved, or **sub-grid scale (SGS)**, processes on the resolved, large-scale flow. This chapter delineates the fundamental principles and mechanisms underlying the parameterization of these [sub-grid scale processes](@entry_id:1132579).

### The Emergence of the Closure Problem

To understand the origin of parameterization, we must first examine how the act of discretization alters the governing equations. Consider the continuous velocity field, $\boldsymbol{u}(\boldsymbol{x},t)$. An ocean model does not solve for this field directly. Instead, it solves for a filtered or averaged representation of it, which we denote with an overbar, $\overline{\boldsymbol{u}}$. This resolved field can be conceptualized as the result of applying a low-pass [spatial filter](@entry_id:1132038) $\mathcal{G}_{\Delta}$ of characteristic width $\Delta$ (the grid spacing) to the true field: $\overline{\boldsymbol{u}} = \mathcal{G}_{\Delta}[\boldsymbol{u}]$ . The residual, $\boldsymbol{u}' = \boldsymbol{u} - \overline{\boldsymbol{u}}$, contains all the information about motions with length scales $L$ smaller than the grid resolution, i.e., $L \lesssim \Delta$. These are the sub-grid scale motions.

Let us apply this filtering operation to the incompressible Navier-Stokes equations. The momentum equation, written in [divergence form](@entry_id:748608), is:
$$
\partial_{t} u_{i} + \partial_{j} (u_{i} u_{j}) = - \frac{1}{\rho} \partial_{i} p + \nu \partial_{j} \partial_{j} u_{i}
$$
Applying the filter, which we assume commutes with differentiation, yields:
$$
\partial_{t} \overline{u_{i}} + \partial_{j} \overline{(u_{i} u_{j})} = - \frac{1}{\rho} \partial_{i} \overline{p} + \nu \partial_{j} \partial_{j} \overline{u_{i}}
$$
The critical issue arises in the [nonlinear advection](@entry_id:1128854) term, $\overline{u_{i} u_{j}}$. The filter of a product is not equal to the product of the filtered quantities: $\overline{u_{i} u_{j}} \neq \overline{u_{i}} \overline{u_{j}}$. This inequality is the heart of the problem. To proceed, we decompose the filtered product:
$$
\overline{u_i u_j} = \overline{(\overline{u_i} + u_i')(\overline{u_j} + u_j')} = \overline{\overline{u_i}\overline{u_j} + \overline{u_i}u_j' + u_i'\overline{u_j} + u_i'u_j'}
$$
This expression is often simplified by defining the **sub-grid scale (SGS) stress tensor**, $\tau_{ij}$, which represents the total effect of the unresolved scales:
$$
\tau_{ij} \equiv \overline{u_{i} u_{j}} - \overline{u_{i}} \overline{u_{j}}
$$
With this definition, we can rewrite the filtered product as $\overline{u_{i} u_{j}} = \overline{u_{i}} \overline{u_{j}} + \tau_{ij}$. Substituting this back into the filtered momentum equation gives the governing equation for the resolved velocity $\overline{u_i}$ :
$$
\partial_{t} \overline{u_{i}} + \partial_{j} (\overline{u_{i}} \overline{u_{j}}) = - \frac{1}{\rho} \partial_{i} \overline{p} + \nu \partial_{j} \partial_{j} \overline{u_{i}} - \partial_{j} \tau_{ij}
$$
This equation reveals the **closure problem**: it is an equation for the resolved variable $\overline{\boldsymbol{u}}$, but it contains a new unknown, $\tau_{ij}$, which is defined in terms of both the resolved and the unknown unresolved velocity fields. To solve the system, we must find a way to "close" it by positing a relationship—a **parameterization**—that expresses the unknown SGS stress $\tau_{ij}$ in terms of the known resolved variables.

It is crucial to distinguish this filtering approach, characteristic of **Large Eddy Simulation (LES)**, from the ensemble-averaging approach of **Reynolds-Averaged Navier-Stokes (RANS)** models. In RANS, the overbar represents an ensemble average, $\overline{u} = \mathbb{E}[u]$, over many realizations of a statistically stationary flow. The deviation $u'$ is then a random fluctuation with zero mean, $\overline{u'} = 0$. In LES, the filter is a deterministic spatial operator, and the residual $u' = u - \overline{u}$ does not generally have a zero filtered value . While mathematically distinct, both approaches lead to an analogous closure problem involving an unclosed stress tensor.

### Local Closures and the Eddy Viscosity Hypothesis

The simplest path to closing the equations is to invoke the **scale separation assumption**. This hypothesis posits that the unresolved SGS motions have [characteristic length scales](@entry_id:266383) $L_{SGS}$ and time scales $\tau_{SGS}$ that are much smaller than those of the resolved motions, $L_{res}$ and $\tau_{res}$. That is, $\varepsilon_{L} = L_{SGS}/L_{res} \ll 1$ and $\varepsilon_{\tau} = \tau_{SGS}/\tau_{res} \ll 1$ . The temporal separation implies that the fast, small-scale eddies adjust almost instantaneously to the slowly varying, large-scale flow. This justifies seeking a closure that is **local** in both space and time, meaning the SGS stress $\tau_{ij}$ at a point $\boldsymbol{x}$ and time $t$ can be modeled using only the resolved field gradients at that same point and time.

The most widespread local closure is the **[eddy viscosity hypothesis](@entry_id:1124144)**, which draws an analogy between the effect of turbulent eddies and the action of molecular viscosity. It assumes that SGS motions act to dissipate resolved-scale kinetic energy by mixing momentum down the mean [velocity gradient](@entry_id:261686). This leads to a model for the deviatoric (traceless) part of the SGS stress tensor, $\tau_{ij}^d = \tau_{ij} - \frac{1}{3}\delta_{ij}\tau_{kk}$, that is linearly proportional to the resolved-scale [strain rate tensor](@entry_id:198281), $\overline{S}_{ij} = \frac{1}{2}(\partial_j \overline{u_i} + \partial_i \overline{u_j})$:
$$
\tau_{ij}^d = -2\nu_t \overline{S}_{ij}
$$
Here, $\nu_t$ is the **eddy viscosity**, which is not a fluid property but a characteristic of the unresolved turbulence itself. A similar assumption for a passive scalar $\phi$ leads to the **eddy diffusivity hypothesis**, where the SGS flux is parameterized as a down-gradient transport :
$$
\boldsymbol{F}_{\phi} = \overline{\boldsymbol{u}' \phi'} = -K_\phi \nabla \overline{\phi}
$$
where $K_\phi$ is the **eddy diffusivity**. This simple form of parameterization is often called **K-theory**. It is most valid where turbulence is in [local equilibrium](@entry_id:156295) (production balances dissipation) and transport is dominated by small, disorganized eddies .

A classic example of an [eddy viscosity model](@entry_id:1124145) is the **Smagorinsky model**, where $\nu_t$ is determined from the local grid scale $\Delta$ and the magnitude of the resolved strain rate, $|\overline{S}| = \sqrt{2 \overline{S}_{mn}\overline{S}_{mn}}$ :
$$
\nu_t = (C_s \Delta)^2 |\overline{S}|
$$
where $C_s$ is the dimensionless Smagorinsky coefficient.

To illustrate, consider a resolved [shear flow](@entry_id:266817) given by $\overline{u}(x,y) = A \sin(ky)$ and $\overline{v}(x,y)=0$. The only non-zero component of the [strain-rate tensor](@entry_id:266108) is $\overline{S}_{12} = \frac{1}{2} Ak \cos(ky)$. The magnitude of the tensor is $|\overline{S}| = |Ak \cos(ky)|$. The SGS shear stress component $\tau_{12}$ is then parameterized as:
$$
\tau_{12} = -2\nu_t \overline{S}_{12} = -2 \left( (C_s \Delta)^2 |Ak \cos(ky)| \right) \left( \frac{1}{2} Ak \cos(ky) \right) = -(C_s \Delta)^2 (Ak)^2 |\cos(ky)|\cos(ky)
$$
For a point where $\cos(ky) > 0$, such as $y_0 = \pi/(3k)$, and given parameters $A=0.8 \, \text{m s}^{-1}$, $k=1 \, \text{m}^{-1}$, $\Delta=2 \, \text{m}$, and $C_s=0.17$, the stress is $\tau_{12} = -(0.17 \cdot 2)^2 (0.8 \cdot 1)^2 \cos^2(\pi/3) = -0.01850 \, \text{m}^2\text{s}^{-2}$ . This calculation demonstrates how an abstract concept—the SGS stress—is translated into a concrete, computable quantity based on resolved fields.

### Anisotropy: The Imprint of Rotation and Stratification

The simple isotropic K-theory, where a single scalar value for $\nu_t$ or $K_\phi$ is used, is fundamentally inadequate for large-scale geophysical flows. The ocean is not isotropic; the presence of planetary rotation and stable stratification makes the vertical direction physically distinct from the horizontal.

1.  **Rotation**: For flows with low Rossby number ($Ro \ll 1$), the Taylor-Proudman theorem indicates that fluid columns tend to become stiff in the vertical, inhibiting vertical shear and promoting quasi-two-dimensional motion in the horizontal plane.
2.  **Stratification**: For flows with low Froude number ($Fr \ll 1$), stable stratification provides a strong restoring force against vertical displacement. It is energetically much easier for fluid parcels to move along surfaces of constant [potential density](@entry_id:1129991) (**isopycnal surfaces**) than across them (**diapycnal surfaces**).

These two effects combine to strongly suppress vertical mixing relative to horizontal mixing. A physically plausible parameterization must reflect this **anisotropy**. The simplest way to do so is to replace the scalar coefficients with **anisotropic tensors**. In a geopotential coordinate system, this can be represented by diagonal tensors with distinct horizontal ($A_h, K_h$) and vertical ($A_v, K_v$) components, where observations and theory demand $A_h \gg A_v$ and $K_h \gg K_v$ . A common [scaling argument](@entry_id:271998) suggests that the ratio of the diffusivities scales as $K_v/K_h \sim (f/N)^2$, where $f$ is the Coriolis parameter and $N$ is the Brunt-Väisälä frequency. In much of the ocean, $f \ll N$, reinforcing the extreme anisotropy.

A more sophisticated approach, particularly for tracers, is to align the diffusivity tensor with the geometry of the stratification itself. This leads to **isoneutral diffusion** schemes. The idea is that mixing should be strong along neutral surfaces (a generalization of isopycnal surfaces) and weak across them. The diffusivity tensor $K$ is constructed to have large eigenvalues for directions in the neutral [tangent plane](@entry_id:136914) and a very small eigenvalue for the dianeutral direction. When isopycnals are sloped relative to the model's coordinate grid, this tensor will have non-zero off-diagonal components, which are crucial for correctly representing [tracer transport](@entry_id:1133278) by mesoscale eddies .

### Beyond Locality: Counter-Gradient and Nonlocal Transport

The local, down-gradient [closures](@entry_id:747387) of K-theory fail spectacularly in situations where the scale separation assumption breaks down. A prime example is a [convective boundary layer](@entry_id:1123026), where turbulence is organized into large, [coherent structures](@entry_id:182915) (e.g., [buoyant plumes](@entry_id:264967) or [thermals](@entry_id:275374)) that can span the entire layer depth. These large eddies can transport properties over long distances, violating the assumption of locality.

This organized transport can lead to **counter-gradient fluxes**, where the [turbulent flux](@entry_id:1133512) is directed *up* the mean gradient (i.e., from low mean concentration to high mean concentration). For instance, in a convectively mixed layer heated from below, [buoyant plumes](@entry_id:264967) can transport heat upward even in the upper part of the layer where the mean potential temperature might be increasing with height ($\partial \overline{\theta}/\partial z > 0$). A local K-theory model, $F_\theta = -K_\theta \partial \overline{\theta}/\partial z$, would incorrectly predict a downward flux in this region.

To capture such phenomena, more advanced **nonlocal [closures](@entry_id:747387)** are required. These models abandon the strict dependence on the local gradient. A general nonlocal closure can be expressed in two ways :
1.  **Spatially Nonlocal Diffusion**: The flux at a point $\boldsymbol{x}$ is given by an integral of the mean gradient over a neighborhood, weighted by a kernel $\mathbf{K}(\boldsymbol{x}, \boldsymbol{x}')$ that represents the finite "[mixing length](@entry_id:199968)" of large eddies.
2.  **Counter-Gradient Term**: The flux is modeled as the sum of a standard down-gradient diffusive term and an additional "nonlocal" flux term, $\boldsymbol{\Gamma}$, which is not proportional to the local gradient.
$$
\boldsymbol{F}_{\phi} = - \mathbf{K}_{\phi} \nabla \overline{\phi} + \boldsymbol{\Gamma}_{\phi}
$$
This added term $\boldsymbol{\Gamma}_{\phi}$ is designed to represent the advective-like transport by large, coherent eddies. In a [convective boundary layer](@entry_id:1123026), a physically plausible form for the vertical component $\Gamma_\phi$ can be constructed using mixed-layer similarity scales . The characteristic velocity and scalar scales are the convective velocity $w_{\star}$ and the surface flux scale $\phi_{\star}$. The nonlocal flux term can then be written as $\Gamma_\phi = C_\phi w_\star \phi_\star f(z/z_i)$, where $z_i$ is the boundary layer depth, $C_\phi$ is a constant, and $f(z/z_i)$ is a dimensionless shape function that is positive in the interior and vanishes at the boundaries of the layer (e.g., at $z=0$ and $z=z_i$). This formulation allows the model to produce a positive (upward) flux even when the local gradient term is zero or opposing.

### Fundamental Constraints on Parameterizations

Any physically meaningful parameterization, regardless of its complexity, must adhere to certain fundamental principles dictated by physics and mathematics.

#### Energetic Consistency

Sub-grid scale turbulence is the primary pathway through which energy cascades from the large, resolved scales to the small scales where it is ultimately dissipated by molecular viscosity. Therefore, a parameterization of these processes must act as a net energy sink for the resolved flow; it must not spontaneously create energy. This principle is known as **energetic consistency**. For a Boussinesq fluid, the total resolved energy is the sum of Kinetic Energy (KE) and Available Potential Energy (APE). The SGS parameterizations must ensure that the domain-integrated tendency of total energy due to SGS terms is non-positive . A standard [eddy viscosity model](@entry_id:1124145) for the [deviatoric stress](@entry_id:163323), $\boldsymbol{\tau}^d_{\mathrm{sgs}} = -2\nu_t \overline{\boldsymbol{S}}$ with $\nu_t \ge 0$, guarantees that the rate of change of KE is $\frac{dE_k}{dt}|_{sgs} = -\int_V 2\nu_t \overline{\boldsymbol{S}}:\overline{\boldsymbol{S}} \, dV \le 0$. Similarly, a down-gradient buoyancy flux $\boldsymbol{J}_{b,\mathrm{sgs}} = -K_b \nabla b$ with $K_b \ge 0$ ensures the rate of change of APE is non-positive. Parameterizations must be formulated and implemented to satisfy this dissipative constraint.

#### Potential Vorticity Conservation

In a rotating, stratified fluid, **Ertel's Potential Vorticity (PV)**, $q = (\boldsymbol{\omega}_a \cdot \nabla b)$, is a crucial dynamical tracer. For ideal (inviscid and adiabatic) flow, PV is conserved following fluid parcels. Many sub-grid processes, particularly the stirring by mesoscale eddies, are intended to be modeled as ideal processes that merely redistribute tracers without mixing them. Such parameterizations must not act as spurious sources or sinks of PV. This imposes powerful constraints on their formulation . For example:
*   An [eddy-induced velocity](@entry_id:1124135) $\boldsymbol{u}^\star$ (as in the Gent-McWilliams scheme) must be non-divergent and tangent to isopycnals ($\boldsymbol{u}^\star \cdot \nabla b = 0$) to be adiabatic and PV-conserving.
*   An isoneutral diffusion tensor $\mathbf{K}$ must truly mix along neutral surfaces, which for buoyancy implies the diffusive flux of buoyancy itself, $-\mathbf{K}\nabla b$, must be zero.
A profound and elegant way to satisfy this constraint is to formulate the parameterization such that its effect on the PV budget appears in flux-[divergence form](@entry_id:748608), $Dq/Dt = \nabla \cdot \boldsymbol{\Psi}_q$. This ensures that the parameterization only redistributes PV within the domain, rather than creating or destroying it in the interior .

#### Material Constraints: Positivity and Monotonicity

Many tracers in ocean models represent physical quantities that are inherently bounded, most commonly requiring non-negativity (e.g., salinity, biological species concentrations). A numerical scheme, including its parameterization components, is **positivity-preserving** if it guarantees that an initially non-negative tracer field remains non-negative (in the absence of sinks). More generally, a scheme is **monotone** if it does not create new local maxima or minima in the solution. This is a crucial property, as spurious overshoots or undershoots are unphysical and can lead to numerical instability. The physical basis for this constraint is that SGS processes represent mixing, which should smooth out [extrema](@entry_id:271659), not create them . A discrete update for a tracer concentration $c_i$ is monotone if the new value $c_i^{n+1}$ can be written as a convex combination of values at the previous time step, $c_i^{n+1} = \sum_j w_{ij} c_j^n$, where the weights are non-negative ($w_{ij} \ge 0$) and sum to one ($\sum_j w_{ij} = 1$). Ensuring that parameterizations satisfy these constraints, often through techniques like [flux limiting](@entry_id:749486), is essential for robust and physically meaningful simulations .

### The Blurring Line: Numerical versus Physical Mixing

Finally, it is critical to recognize that the explicit parameterization chosen by the modeler is not the only source of mixing in a simulation. The numerical scheme used to discretize the advection operator inherently introduces errors that often manifest as a diffusive process. This is termed **numerical diffusion**.

To see this, consider the [first-order upwind scheme](@entry_id:749417) for advection in the $x$-direction, $\partial_t c + u \partial_x c = 0$. A truncation [error analysis](@entry_id:142477) reveals that this discrete scheme does not solve the original PDE, but rather a "[modified equation](@entry_id:173454)" that includes an additional second-derivative term :
$$
\frac{\partial c}{\partial t} + u \frac{\partial c}{\partial x} = \frac{u \Delta x}{2}(1 - C) \frac{\partial^2 c}{\partial x^2} + \text{higher order terms}
$$
where $C = u\Delta t / \Delta x$ is the Courant number. This shows the scheme behaves as if it has an effective numerical diffusivity of $K_{num} = \frac{u \Delta x}{2}(1 - C)$.

This artifact becomes particularly pernicious in ocean models that use a geopotential coordinate grid. If the flow is directed along isopycnals that are sloped with respect to the grid, the numerical diffusion, which acts along the grid lines, will have a component that projects across the isopycnals. This creates a spurious **numerical [diapycnal mixing](@entry_id:1123661)**, which can be orders of magnitude larger than the true physical diapycnal mixing in the ocean . For a slope $S = \tan\theta$, this numerical diapycnal diffusivity scales as $K_{d,num} \propto u \Delta x S^2$. While refining the grid (reducing $\Delta x$) can decrease this spurious mixing, it remains a persistent challenge. The total effective diapycnal mixing in a model is the sum of the explicitly parameterized physical mixing and the implicit, often unwanted, numerical mixing. A failure to account for or control numerical diffusion can lead to a profound misrepresentation of water mass transformations and the overall ocean state.