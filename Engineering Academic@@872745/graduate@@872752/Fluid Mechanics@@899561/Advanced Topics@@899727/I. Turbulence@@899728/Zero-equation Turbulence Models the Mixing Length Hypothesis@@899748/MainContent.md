## Introduction
The closure of the Reynolds-Averaged Navier-Stokes (RANS) equations is a central challenge in computational fluid dynamics, requiring models to represent the effects of turbulent fluctuations on the mean flow. Among the various strategies developed, zero-equation models stand out as the simplest and most computationally efficient class. They address the [closure problem](@entry_id:160656) by providing a direct algebraic link between the unknown Reynolds stresses and the known mean flow properties, avoiding the need for additional [transport equations](@entry_id:756133). This approach, while foundational, introduces critical concepts like [eddy viscosity](@entry_id:155814) and the mixing length, which form the bedrock of modern [turbulence modeling](@entry_id:151192).

This article offers a comprehensive exploration of these foundational models, focusing on the seminal [mixing length hypothesis](@entry_id:202055). The first chapter, **"Principles and Mechanisms,"** will dissect the Boussinesq hypothesis and Prandtl's [mixing length theory](@entry_id:161086), explaining how they reduce the complex Reynolds stress tensor to a solvable algebraic problem. The second chapter, **"Applications and Interdisciplinary Connections,"** will demonstrate the remarkable versatility of the mixing length concept, showcasing its application in advanced engineering flows and its adaptation in fields from astrophysics to combustion. Finally, the **"Hands-On Practices"** section provides a set of problems designed to reinforce these theoretical concepts through practical application. We begin our journey by examining the core principles that enable this algebraic approach to modeling turbulence.

## Principles and Mechanisms

The closure of the Reynolds-Averaged Navier-Stokes (RANS) equations represents one of the central challenges in fluid mechanics. The [time-averaging](@entry_id:267915) process introduces the Reynolds stress tensor, $-\rho \overline{u'_i u'_j}$, which must be modeled in terms of known or solvable quantities. The simplest and historically most significant class of closures are the zero-equation models, which achieve this through purely algebraic relations. This chapter elucidates the principles and mechanisms underpinning these models, focusing on the cornerstone concept of the [mixing length hypothesis](@entry_id:202055).

### The Boussinesq Hypothesis and the Concept of Eddy Viscosity

The foundation for most RANS closures is the **Boussinesq hypothesis**, proposed by Joseph Boussinesq in 1877. This hypothesis establishes a powerful analogy between the action of turbulent eddies and the action of molecules in a gas. Just as [molecular collisions](@entry_id:137334) give rise to viscous stresses that resist [fluid deformation](@entry_id:271538), the chaotic motion of [turbulent eddies](@entry_id:266898) results in a macroscopic transfer of momentum that can be modeled as an augmented stress.

Mathematically, the Boussinesq hypothesis relates the anisotropic part of the Reynolds stress tensor to the mean [strain-rate tensor](@entry_id:266108), $S_{ij}$, in a linear fashion:

$$
-\rho \overline{u'_i u'_j} + \frac{1}{3} \delta_{ij} \rho \overline{u'_k u'_k} = 2 \mu_t S_{ij}
$$

where $\mu_t$ is the **turbulent viscosity** or **[eddy viscosity](@entry_id:155814)**, and $S_{ij} = \frac{1}{2} (\frac{\partial \bar{u}_i}{\partial x_j} + \frac{\partial \bar{u}_j}{\partial x_i})$ is the mean [strain-rate tensor](@entry_id:266108). The term $\frac{1}{3} \delta_{ij} \rho \overline{u'_k u'_k}$ is subtracted to ensure the relation is consistent for the trace of the tensor. Recognizing that the [turbulent kinetic energy](@entry_id:262712) is $k = \frac{1}{2} \overline{u'_k u'_k}$, the model is commonly written as:

$$
-\rho \overline{u'_i u'_j} = 2 \mu_t S_{ij} - \frac{2}{3} \rho k \delta_{ij}
$$

The total shear stress in a turbulent flow is thus the sum of the molecular (viscous) component and the turbulent (Reynolds) component. For a [simple shear](@entry_id:180497) flow with [mean velocity](@entry_id:150038) $\bar{u}(y)$, the total shear stress $\tau_{\text{total}}$ is:

$$
\tau_{\text{total}} = \mu \frac{d\bar{u}}{dy} - \rho \overline{u'v'} = (\mu + \mu_t) \frac{d\bar{u}}{dy} = \rho (\nu + \nu_t) \frac{d\bar{u}}{dy}
$$

Here, $\nu = \mu/\rho$ is the [kinematic viscosity](@entry_id:261275) and $\nu_t = \mu_t/\rho$ is the **eddy kinematic viscosity**. Unlike $\nu$, which is a physical property of the fluid, $\nu_t$ is a property of the flow itself—it varies in space and depends on the state of the turbulence. The Boussinesq hypothesis elegantly reduces the complex problem of modeling six independent components of the Reynolds stress tensor to the simpler problem of modeling the scalar [eddy viscosity](@entry_id:155814), $\nu_t$.

Turbulence models are often classified by the number of additional [transport equations](@entry_id:756133) they solve to determine $\nu_t$ [@problem_id:1766432]. **Zero-equation models** use purely algebraic formulas for $\nu_t$ based on local mean flow properties. **One-equation models** solve one transport equation, typically for [turbulent kinetic energy](@entry_id:262712), to find a velocity scale for turbulence. **Two-equation models** (e.g., $k$-$\epsilon$, $k$-$\omega$) solve two [transport equations](@entry_id:756133) to determine both a velocity scale and a length scale for turbulence. This chapter is devoted to the first and simplest class: zero-equation models.

### Prandtl's Mixing Length Hypothesis

In 1925, Ludwig Prandtl introduced the **[mixing length hypothesis](@entry_id:202055)**, a seminal concept that provided a physical basis for an algebraic expression for the [eddy viscosity](@entry_id:155814). Prandtl envisioned [turbulent flow](@entry_id:151300) not as a continuum of interacting eddies, but as discrete fluid parcels that are displaced by the turbulent motion before mixing with the surrounding fluid.

The core assumption is that a fluid parcel displaced over a characteristic transverse distance $l_m$, the **[mixing length](@entry_id:199968)**, conserves its mean momentum during this short transit [@problem_id:1812861]. Consider a mean shear flow $\bar{u}(y)$. A fluid parcel originating at $y - l_m$ has a [mean velocity](@entry_id:150038) $\bar{u}(y - l_m)$. If it is displaced to position $y$, it arrives carrying its original momentum. The velocity difference between this parcel and the local mean flow creates a streamwise velocity fluctuation $u'$:

$$
u' \approx \bar{u}(y - l_m) - \bar{u}(y) \approx -l_m \frac{d\bar{u}}{dy}
$$

Prandtl further argued that the transverse velocity fluctuation, $v'$, which is responsible for displacing the parcel, should be of the same [order of magnitude](@entry_id:264888) as $u'$. Thus, $|v'| \sim |u'| \sim l_m |\frac{d\bar{u}}{dy}|$. The time-averaged Reynolds shear stress, $-\rho \overline{u'v'}$, can then be modeled as being proportional to the product of these fluctuation scales:

$$
-\rho \overline{u'v'} \propto \rho (l_m \frac{d\bar{u}}{dy}) (l_m \frac{d\bar{u}}{dy})
$$

This leads to the famous [mixing length model](@entry_id:752031) for the Reynolds shear stress:

$$
-\rho \overline{u'v'} = \rho l_m^2 \left| \frac{d\bar{u}}{dy} \right| \frac{d\bar{u}}{dy}
$$

Comparing this with the Boussinesq relation, $-\rho \overline{u'v'} = \rho \nu_t \frac{d\bar{u}}{dy}$, immediately yields an algebraic expression for the [eddy viscosity](@entry_id:155814):

$$
\nu_t = l_m^2 \left| \frac{d\bar{u}}{dy} \right|
$$

It is noteworthy that Prandtl's physical argument relies on the conservation of momentum. G.I. Taylor later proposed an alternative theory based on the conservation of **[vorticity](@entry_id:142747)**, arguing that vorticity is a more fundamental conserved property in [inviscid fluid](@entry_id:198262) motion [@problem_id:1812861]. While Taylor's [vorticity](@entry_id:142747) [transport theory](@entry_id:143989) provided important physical insights, Prandtl's momentum-based [mixing length model](@entry_id:752031) proved more adaptable and remains a cornerstone of elementary [turbulence modeling](@entry_id:151192).

### Models for the Mixing Length

The [mixing length hypothesis](@entry_id:202055) does not close the problem entirely; it shifts the burden from modeling $\nu_t$ to modeling the [mixing length](@entry_id:199968), $l_m$. The central task of a zero-equation model is to provide an algebraic prescription for $l_m$ based on the flow geometry and local conditions.

#### The von Kármán Similarity Hypothesis

One of the most elegant approaches for determining $l_m$ was proposed by Theodore von Kármán. His **hypothesis of local kinematic similarity** posits that the turbulent structure, and thus its characteristic length scale $l_m$, should be determined entirely by the local properties of the mean [velocity profile](@entry_id:266404) [@problem_id:683466]. For a one-dimensional mean profile $\bar{u}(y)$, the only local properties available are its derivatives, $\frac{d\bar{u}}{dy}$ and $\frac{d^2\bar{u}}{dy^2}$.

Using [dimensional analysis](@entry_id:140259), we can find the unique combination of these two quantities that yields a unit of length. The dimension of $\frac{d\bar{u}}{dy}$ is $[T^{-1}]$, and the dimension of $\frac{d^2\bar{u}}{dy^2}$ is $[L^{-1}T^{-1}]$. The only ratio that produces a dimension of length $[L]$ is:

$$
l_m \propto \left| \frac{d\bar{u}/dy}{d^2\bar{u}/dy^2} \right|
$$

Introducing a dimensionless constant of proportionality, $\kappa$, known as the **von Kármán constant**, we arrive at the expression:

$$
l_m = \kappa \left| \frac{d\bar{u}/dy}{d^2\bar{u}/dy^2} \right|
$$

This formulation is powerful in theory, as it allows $l_m$ to be determined directly from the mean velocity profile itself. However, its practical application is limited by the numerical difficulty and sensitivity associated with calculating the second derivative of velocity from experimental or computational data.

#### Empirical Models for Wall-Bounded and Free-Shear Flows

The most common approach in practice is to prescribe $l_m$ using simple, empirically derived [algebraic functions](@entry_id:187534) that are tailored to the specific type of flow.

For **wall-bounded flows** like boundary layers and channel flows, the turbulence structure changes significantly with distance from the wall. This necessitates a composite model for $l_m$:

*   **Inner Region (near the wall):** In the region close to the wall but outside the viscous sublayer, the dominant length scale is the distance from the wall itself, $y$. The eddies are constrained by the presence of the surface, so it is natural to assume their size is proportional to $y$. This gives the widely used linear model:
    $$
    l_m = \kappa y
    $$
    where $\kappa \approx 0.41$ is the von Kármán constant. This simple assumption, when combined with the [mixing length](@entry_id:199968) formula, is sufficient to derive the celebrated [logarithmic law of the wall](@entry_id:262057).

*   **Outer Region:** Farther from the wall, eddies are no longer constrained by $y$ but by the overall thickness of the [shear layer](@entry_id:274623), $\delta$. The assumption $l_m = \kappa y$ becomes physically unrealistic, as it would predict mixing lengths that grow indefinitely, eventually exceeding the [boundary layer thickness](@entry_id:269100) [@problem_id:1812881]. Therefore, in the outer region, the [mixing length](@entry_id:199968) is typically modeled as being proportional to the [boundary layer thickness](@entry_id:269100):
    $$
    l_m = \lambda \delta
    $$
    where $\lambda \approx 0.085 - 0.09$ is an empirical constant [@problem_id:1812853].

Practical zero-equation models, such as the **Cebeci-Smith model**, combine these two formulations, using $l_m = \kappa y$ near the wall and switching to $l_m = \lambda \delta$ in the outer region, with a continuity condition at the crossover point. A quantitative comparison at a point $y=0.65\delta$ in the outer region, for instance, shows that Prandtl's unbounded model would predict a mixing length $l_m = 0.41 \times 0.65 \delta = 0.267\delta$, whereas the Cebeci-Smith model gives $l_m = 0.085\delta$. The ratio of these predictions is about $0.319$, highlighting the significant over-prediction of the simpler model in the outer layer [@problem_id:1812881].

For **free-shear flows**, such as jets, wakes, and mixing layers, there is no wall to provide a reference length scale. In these flows, the turbulence scales with the local width of the [shear layer](@entry_id:274623), $b(x)$. A simple and effective model is to assume the mixing length is proportional to this width [@problem_id:1812835]:

$$
l_m(x) = C_m b(x)
$$

where $C_m$ is an empirical constant specific to the type of flow (e.g., for a planar jet, $C_m \approx 0.075$). This demonstrates the adaptability of the [mixing length](@entry_id:199968) concept, provided that an appropriate characteristic length scale for the flow can be identified.

### Illustrative Applications of the Mixing Length Model

To solidify these concepts, let's consider their application to canonical turbulent flow problems.

#### Total Shear Stress Profile near a Wall

Consider a turbulent flow over a flat plate where the mean velocity profile is approximated by the function $\bar{u}(y) = U_{\infty} [1 - \exp(-y/L)]$. The total shear stress is the sum of the viscous and turbulent contributions, $\tau_{\text{total}} = \rho(\nu + \nu_t) \frac{d\bar{u}}{dy}$. First, we find the [velocity gradient](@entry_id:261686):

$$
\frac{d\bar{u}}{dy} = \frac{U_{\infty}}{L} \exp(-y/L)
$$

Using the near-wall [mixing length model](@entry_id:752031), $l_m = \kappa y$, the eddy viscosity is:

$$
\nu_t = l_m^2 \left| \frac{d\bar{u}}{dy} \right| = (\kappa y)^2 \frac{U_{\infty}}{L} \exp(-y/L)
$$

Substituting these into the total stress equation provides a complete expression for the shear stress profile as a function of distance from the wall [@problem_id:1812831]:

$$
\tau_{\text{total}}(y) = \rho \left[ \nu + (\kappa y)^2 \frac{U_{\infty}}{L} \exp(-y/L) \right] \frac{U_{\infty}}{L} \exp(-y/L)
$$

This expression clearly shows how the stress transitions from being viscously dominated very close to the wall (where $y \to 0$ and the $\nu_t$ term vanishes) to being turbulence-dominated further away.

#### The Velocity Defect Law in the Outer Layer

In the outer region of a turbulent boundary layer, the [mixing length model](@entry_id:752031) $l_m = \lambda \delta$ can be used to derive the well-known [velocity defect law](@entry_id:195348). If we approximate the shear stress profile in this region as a linear function, $\tau_t(y) \approx \tau_w (1 - y/\delta)$, where $\tau_w = \rho u_\tau^2$ is the [wall shear stress](@entry_id:263108), we can equate this with the [mixing length model](@entry_id:752031) for stress [@problem_id:1812853]:

$$
\rho l_m^2 \left( \frac{d\bar{u}}{dy} \right)^2 = \rho u_\tau^2 (1 - y/\delta)
$$

Substituting $l_m = \lambda \delta$ and solving for the velocity gradient gives:

$$
\frac{d\bar{u}}{dy} = \frac{u_\tau}{\lambda \delta} (1 - y/\delta)^{1/2}
$$

Integrating this expression from an arbitrary position $y$ to the edge of the boundary layer $\delta$ (where $\bar{u}(\delta) = U_\infty$) yields the velocity defect:

$$
\int_{\bar{u}}^{U_\infty} d\bar{u}' = \int_{y}^{\delta} \frac{u_\tau}{\lambda \delta} (1 - y'/\delta)^{1/2} dy' \implies U_\infty - \bar{u}(y) = \frac{2u_\tau}{3\lambda} (1 - y/\delta)^{3/2}
$$

Dividing by the [friction velocity](@entry_id:267882) $u_\tau$ gives the classic [velocity defect law](@entry_id:195348) form, $\frac{U_\infty - \bar{u}}{u_\tau} = f(y/\delta)$, and shows that the simple [mixing length model](@entry_id:752031) predicts a specific functional form for this law, with the coefficient $K = \frac{2}{3\lambda}$ [@problem_id:1812853]. This demonstrates the power of the model to capture fundamental scaling laws of turbulent flows.

### Fundamental Limitations of Zero-Equation Models

Despite their elegance and utility, zero-equation models based on the [mixing length hypothesis](@entry_id:202055) suffer from fundamental limitations that restrict their applicability, particularly for complex flows. Understanding these limitations is crucial, as they motivate the development of more advanced turbulence models.

#### The Locality Problem: Failure in Non-Equilibrium Flows

The most significant flaw of zero-equation models is their **locality**. The eddy viscosity and turbulent stress at a point are determined solely by the local mean [velocity gradient](@entry_id:261686) at that same point. This implicitly assumes that the turbulence is in a state of **[local equilibrium](@entry_id:156295)**, where the rates of [turbulence production](@entry_id:189980) and dissipation are approximately equal at every point.

This assumption fails dramatically in flows that are far from equilibrium, such as those involving strong pressure gradients, curvature, or separation [@problem_id:1812818]. Consider a flow approaching a separation point due to a strong [adverse pressure gradient](@entry_id:276169). The mean [velocity profile](@entry_id:266404) flattens, and the gradient $\frac{d\bar{u}}{dy}$ becomes zero at some point. The [mixing length model](@entry_id:752031) predicts that where $\frac{d\bar{u}}{dy} = 0$, the eddy viscosity $\nu_t$ and the turbulent stress $\tau_t$ must also be zero.

Physically, this is incorrect. Turbulence has a "memory" and is subject to transport effects like convection and diffusion. Turbulent energy generated upstream can be carried downstream into the region of low [velocity gradient](@entry_id:261686), maintaining a significant level of turbulent stress. By failing to account for this transport, zero-equation models incorrectly predict a collapse of turbulence near separation, leading to poor predictions of the separation point and the size of any resulting recirculation zones. This failure highlights the need for models that solve [transport equations](@entry_id:756133) for turbulence quantities, such as $k$.

#### The Isotropy Problem: Failure to Predict Anisotropic Normal Stresses

A second fundamental limitation stems directly from the linear, scalar form of the Boussinesq hypothesis itself. While it provides a model for the shear stresses, it fails to correctly predict the **Reynolds normal stresses** ($\tau_{xx}, \tau_{yy}, \tau_{zz}$ or $-\rho \overline{u'^2}, -\rho \overline{v'^2}, -\rho \overline{w'^2}$).

Let's examine the modeled [normal stress](@entry_id:184326) components from the Boussinesq relation in an incompressible flow where $\nabla \cdot \bar{\mathbf{u}} = 0$ [@problem_id:1812828]:

$$
-\rho \overline{u'_i u'_i} = 2 \mu_t S_{ii} - \frac{2}{3} \rho k
$$

(no summation on $i$). For an incompressible flow, the diagonal components of the mean [strain-rate tensor](@entry_id:266108) are $S_{11} = \frac{\partial \bar{u}}{\partial x}$, $S_{22} = \frac{\partial \bar{v}}{\partial y}$, and so on. For a [simple shear](@entry_id:180497) flow like that in a channel, where $\bar{u} = \bar{u}(y)$ and $\bar{v} = \bar{w} = 0$, the [continuity equation](@entry_id:145242) $\frac{\partial \bar{u}}{\partial x} + \frac{\partial \bar{v}}{\partial y} + \frac{\partial \bar{w}}{\partial z} = 0$ is automatically satisfied. The diagonal components of the [strain-rate tensor](@entry_id:266108) are all zero: $S_{11} = S_{22} = S_{33} = 0$.

The Boussinesq model therefore predicts:

$$
-\rho \overline{u'^2} = -\frac{2}{3} \rho k \implies \overline{u'^2} = \frac{2}{3} k
$$
$$
-\rho \overline{v'^2} = -\frac{2}{3} \rho k \implies \overline{v'^2} = \frac{2}{3} k
$$
$$
-\rho \overline{w'^2} = -\frac{2}{3} \rho k \implies \overline{w'^2} = \frac{2}{3} k
$$

The model intrinsically predicts that the turbulent kinetic energy is partitioned equally among the three [normal stress](@entry_id:184326) components, a condition known as **isotropy**. However, experimental measurements in virtually all shear flows show a strong **anisotropy**, with the streamwise fluctuations being the largest (i.e., $\overline{u'^2} > \overline{v'^2} \approx \overline{w'^2}$). This discrepancy is a direct consequence of modeling the complex, tensor-valued Reynolds stresses with a simple scalar [eddy viscosity](@entry_id:155814). Capturing this anisotropy requires more sophisticated approaches, such as non-linear [eddy viscosity](@entry_id:155814) models or full Reynolds Stress Models (RSM) that solve [transport equations](@entry_id:756133) for each component of the stress tensor.

Despite these limitations, the [mixing length hypothesis](@entry_id:202055) and the zero-equation models built upon it remain invaluable, both as a pedagogical tool for introducing the concepts of [turbulence modeling](@entry_id:151192) and as a computationally inexpensive method for simulating simple, equilibrium turbulent flows. Their principles form the foundation upon which more advanced and accurate [turbulence models](@entry_id:190404) are built.