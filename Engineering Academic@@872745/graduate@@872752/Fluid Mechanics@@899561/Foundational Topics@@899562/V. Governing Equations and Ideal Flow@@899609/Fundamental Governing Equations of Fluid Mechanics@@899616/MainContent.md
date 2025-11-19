## Introduction
The motion of fluids, from the air flowing over an aircraft wing to the dynamics of stars and galaxies, is one of the most complex and ubiquitous phenomena in the physical world. To understand and predict this behavior, scientists and engineers rely on a robust mathematical framework known as the fundamental governing equations. The primary challenge lies in translating universal physical laws—the [conservation of mass](@entry_id:268004), momentum, and energy—into a set of equations that can describe a continuously deforming medium observed from a fixed point in space.

This article provides a graduate-level exposition of this foundational framework. First, in "Principles and Mechanisms," we will rigorously derive the governing equations from first principles, introducing essential concepts like the material derivative, stress tensor, and [constitutive relations](@entry_id:186508) for different fluid types. Next, in "Applications and Interdisciplinary Connections," we explore how these equations are simplified and adapted to model a vast array of phenomena, from geophysical flows and [aeroacoustics](@entry_id:266763) to surprising analogies in quantum mechanics and general relativity. Finally, "Hands-On Practices" will offer opportunities to apply these theoretical concepts to concrete problems, solidifying your understanding. We begin by establishing the language needed to describe fluid motion before systematically building the mathematical expressions of the core conservation laws.

## Principles and Mechanisms

The dynamics of a fluid are governed by a set of fundamental physical laws expressing the conservation of mass, momentum, and energy. While the underlying physics is universal, its mathematical formulation in the context of a deformable, flowing continuum presents unique challenges. This chapter develops the core equations of [fluid mechanics](@entry_id:152498) from first principles, establishing the mathematical framework used throughout the field. We will begin by defining the appropriate kinematic language to describe fluid motion and then systematically derive the [differential forms](@entry_id:146747) of the governing equations.

### The Lagrangian and Eulerian Viewpoints: The Material Derivative

To describe [fluid motion](@entry_id:182721), two primary perspectives can be adopted: the **Lagrangian description** and the **Eulerian description**. In the Lagrangian approach, one follows the trajectory and property changes of individual fluid parcels, much like tracking a single car in traffic. The position of a particle is a function of its initial position $\mathbf{X}$ and time $t$, denoted as $\mathbf{x}(\mathbf{X}, t)$. In contrast, the Eulerian approach observes the flow from fixed points in space. Here, [fluid properties](@entry_id:200256) such as velocity $\mathbf{v}$, pressure $p$, and density $\rho$ are described as fields, i.e., functions of a fixed position $\mathbf{x}$ and time $t$, as in $\mathbf{v}(\mathbf{x}, t)$. While the Lagrangian view is conceptually direct, the Eulerian framework is almost always more practical for formulating and solving fluid dynamics problems.

A crucial link between these two viewpoints is the **[material derivative](@entry_id:266939)**, denoted as $\frac{D}{Dt}$. It represents the total rate of change of a property experienced by a fluid parcel as it moves through the Eulerian field. Consider a scalar property $\phi(\mathbf{x}, t)$. The change in $\phi$ for a specific fluid parcel over an infinitesimal time interval $dt$ is given by the chain rule of calculus:

$d\phi = \frac{\partial \phi}{\partial t} dt + \frac{\partial \phi}{\partial x} dx + \frac{\partial \phi}{\partial y} dy + \frac{\partial \phi}{\partial z} dz$

Dividing by $dt$ gives the rate of change for that parcel:

$\frac{d\phi}{dt} = \frac{\partial \phi}{\partial t} + \frac{\partial \phi}{\partial x} \frac{dx}{dt} + \frac{\partial \phi}{\partial y} \frac{dy}{dt} + \frac{\partial \phi}{\partial z} \frac{dz}{dt}$

Recognizing that the velocity components of the fluid parcel are $v_x = \frac{dx}{dt}$, $v_y = \frac{dy}{dt}$, and $v_z = \frac{dz}{dt}$, we can write this expression in vector notation. The resulting operator is the [material derivative](@entry_id:266939):

$\frac{D}{Dt} \equiv \frac{\partial}{\partial t} + \mathbf{v} \cdot \nabla$

Here, $\frac{\partial}{\partial t}$ is the **local derivative**, representing the rate of change at a fixed point in space. The term $\mathbf{v} \cdot \nabla$ is the **[convective derivative](@entry_id:262900)** (or advective derivative), which accounts for the change in the property due to the fluid parcel moving to a new location where the property has a different value.

For example, imagine standing by a river and measuring its temperature. The temperature you measure might change because the entire river is cooling down (local change) or because a warmer patch of water from upstream has just floated to your location (convective change). The material derivative accounts for both effects simultaneously.

To solidify this concept, let us consider a hypothetical unsteady, non-uniform [velocity field](@entry_id:271461) $\mathbf{v}(\mathbf{x}, t) = A y \, \mathbf{i} + B x t \, \mathbf{j} + C z^2 \, \mathbf{k}$ and a scalar field $\phi(\mathbf{x}, t) = D x^2 y - E z t^2$ [@problem_id:525299]. The rate of change of $\phi$ for a fluid parcel is found by applying the material derivative operator:

$\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + \mathbf{v} \cdot \nabla \phi$

First, the local derivative captures the explicit time dependence of $\phi$:
$\frac{\partial \phi}{\partial t} = \frac{\partial}{\partial t} (D x^2 y - E z t^2) = -2 E z t$

Next, the [convective derivative](@entry_id:262900) requires the gradient of $\phi$ and the velocity $\mathbf{v}$:
$\nabla \phi = (2 D x y) \mathbf{i} + (D x^2) \mathbf{j} - (E t^2) \mathbf{k}$
$\mathbf{v} \cdot \nabla \phi = (A y)(2 D x y) + (B x t)(D x^2) + (C z^2)(-E t^2) = 2 A D x y^2 + B D x^3 t - C E z^2 t^2$

Combining these terms gives the total rate of change experienced by the fluid parcel:
$\frac{D\phi}{Dt} = -2 E z t + 2 A D x y^2 + B D x^3 t - C E z^2 t^2$

This expression gives the rate of change of $\phi$ for the particle currently at position $(x, y, z)$ at time $t$. The [material derivative](@entry_id:266939) can be applied to any scalar, vector, or [tensor field](@entry_id:266532), providing the essential tool to express physical laws in the convenient Eulerian framework.

### The Fundamental Conservation Laws

The [governing equations of fluid mechanics](@entry_id:186548) are mathematical statements of three fundamental conservation principles: [conservation of mass](@entry_id:268004), momentum, and energy. We derive their [differential forms](@entry_id:146747) by first considering an arbitrary, fixed region of space known as a **[control volume](@entry_id:143882)** ($V$) enclosed by a surface $S$. The **Reynolds Transport Theorem** provides a general formula for relating the rate of change of a total quantity within a moving fluid system to integrals over a fixed [control volume](@entry_id:143882). Applying this theorem to the conservation laws and then shrinking the [control volume](@entry_id:143882) to an infinitesimal size allows us to derive the governing partial differential equations.

#### Conservation of Mass: The Continuity Equation

The principle of [mass conservation](@entry_id:204015) states that the rate of increase of mass within a control volume must equal the net rate at which mass flows into the volume, plus the rate at which mass is created within the volume (by a [source term](@entry_id:269111) $Q$). In integral form, this is:

$\frac{d}{dt} \int_V \rho \, dV = -\oint_S \rho (\mathbf{v} \cdot \mathbf{n}) \, dS + \int_V Q \, dV$

where $\mathbf{n}$ is the outward-pointing unit normal to the surface $S$. Using the Reynolds Transport Theorem and the Divergence Theorem ($\oint_S \mathbf{F} \cdot \mathbf{n} \, dS = \int_V (\nabla \cdot \mathbf{F}) \, dV$), this integral equation can be converted into its [differential form](@entry_id:174025):

$\frac{\partial \rho}{\partial t} + \nabla \cdot (\rho \mathbf{v}) = Q$

This is the **[continuity equation](@entry_id:145242)**. It is a statement of mass conservation at every point in the fluid. The term $\nabla \cdot (\rho \mathbf{v})$ represents the net mass outflow per unit volume. For many flows, there are no mass sources or sinks ($Q=0$).

A critically important simplification arises for **[incompressible fluids](@entry_id:181066)**, where the density of a fluid parcel is assumed to be constant: $\frac{D\rho}{Dt} = 0$. Expanding this with the material derivative gives $\frac{\partial \rho}{\partial t} + \mathbf{v} \cdot \nabla \rho = 0$. When combined with the continuity equation (for $Q=0$), this leads to a purely kinematic constraint on the velocity field:

$\nabla \cdot \mathbf{v} = 0$

This states that the [velocity field](@entry_id:271461) of an incompressible flow must be [divergence-free](@entry_id:190991).

The general form of the [continuity equation](@entry_id:145242) can be expressed in any coordinate system. In [cylindrical coordinates](@entry_id:271645) $(r, \theta, z)$ with corresponding velocity components $(v_r, v_\theta, v_z)$, the [divergence operator](@entry_id:265975) takes a specific form, and the [continuity equation](@entry_id:145242) becomes [@problem_id:525266]:

$\frac{\partial \rho}{\partial t} + \frac{1}{r} \frac{\partial (r \rho v_r)}{\partial r} + \frac{1}{r} \frac{\partial (\rho v_\theta)}{\partial \theta} + \frac{\partial (\rho v_z)}{\partial z} = Q$

As an application, consider a steady, incompressible, purely radial flow with a volumetric mass source $Q(r) = \alpha r^2$. The continuity equation simplifies to an ordinary differential equation for the [radial velocity](@entry_id:159824) $v_r(r)$, which can be readily solved to determine the flow profile based on the source distribution and a boundary condition [@problem_id:525266].

#### Conservation of Momentum: The Cauchy and Navier-Stokes Equations

Newton's second law, applied to a fluid parcel, states that the rate of change of momentum of the parcel equals the [net force](@entry_id:163825) acting upon it. Using the [material derivative](@entry_id:266939), this can be written as:

$\rho \frac{D\mathbf{v}}{Dt} = \mathbf{F}_{\text{net}}$

The forces are categorized as **body forces** (acting on the volume of the fluid, like gravity) and **[surface forces](@entry_id:188034)** (acting on the surface of the parcel, like pressure and friction). We denote the [body force](@entry_id:184443) per unit volume as $\rho \mathbf{f}$. The net surface force is represented by the divergence of the **Cauchy stress tensor**, $\boldsymbol{\sigma}$. This leads to the **Cauchy [momentum equation](@entry_id:197225)**:

$\rho \frac{D\mathbf{v}}{Dt} = \nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{f}$

This equation is a general statement of [momentum conservation](@entry_id:149964) but is not yet complete, as the stress tensor $\boldsymbol{\sigma}$ is unknown. To close the system, we require a **[constitutive relation](@entry_id:268485)** that connects the stress to the fluid's motion and state. The choice of [constitutive relation](@entry_id:268485) defines the type of fluid model.

**Ideal Fluid: The Euler Equation**
For an **[inviscid fluid](@entry_id:198262)** (an idealization where viscosity is neglected), [surface forces](@entry_id:188034) can only act normal to any surface. This means there are no shear stresses. In this case, the stress tensor is purely isotropic and is determined entirely by the local thermodynamic pressure, $p$. The [constitutive relation](@entry_id:268485) is [@problem_id:1746703]:

$\sigma_{ij} = -p\delta_{ij}$

where $\delta_{ij}$ is the Kronecker delta. The negative sign indicates that pressure exerts a compressive force. Substituting this into the Cauchy equation gives $\nabla \cdot \boldsymbol{\sigma} = -\nabla p$. The resulting [momentum equation](@entry_id:197225) for an [ideal fluid](@entry_id:272764) is the **Euler equation**:

$\rho \frac{D\mathbf{v}}{Dt} = -\nabla p + \rho \mathbf{f}$

**Newtonian Fluid: The Navier-Stokes Equations**
For a real, viscous fluid, both normal and shear stresses exist. For a **Newtonian fluid**, the stress is assumed to be a linear function of the local rates of [fluid deformation](@entry_id:271538). The stress tensor is decomposed into an [isotropic pressure](@entry_id:269937) part and a **[deviatoric stress tensor](@entry_id:267642)**, $\boldsymbol{\tau}$, which represents the viscous stresses:

$\boldsymbol{\sigma} = -p\mathbf{I} + \boldsymbol{\tau}$

The [constitutive relation](@entry_id:268485) for a compressible isotropic Newtonian fluid relates $\boldsymbol{\tau}$ to the [velocity gradient tensor](@entry_id:270928) $\nabla\mathbf{v}$:

$\boldsymbol{\tau} = \mu \left( \nabla\mathbf{v} + (\nabla\mathbf{v})^T - \frac{2}{3} (\nabla \cdot \mathbf{v}) \mathbf{I} \right) + \kappa (\nabla \cdot \mathbf{v}) \mathbf{I}$

Here, $\mu$ is the **dynamic viscosity** (measuring resistance to shear deformation), $\kappa$ is the **[bulk viscosity](@entry_id:187773)** (measuring resistance to [volumetric expansion](@entry_id:144241)/compression), and $\mathbf{I}$ is the identity tensor. Substituting this full [constitutive relation](@entry_id:268485) into the Cauchy momentum equation yields the **Navier-Stokes equations**, the cornerstone of [fluid mechanics](@entry_id:152498). For an [incompressible flow](@entry_id:140301) ($\nabla \cdot \mathbf{v} = 0$), this simplifies to $\boldsymbol{\tau} = \mu(\nabla\mathbf{v} + (\nabla\mathbf{v})^T)$.

It is often useful to write the [momentum equation](@entry_id:197225) in what is known as **conservation form**. By combining the Cauchy [momentum equation](@entry_id:197225) and the [continuity equation](@entry_id:145242), we can rewrite the momentum balance as [@problem_id:629918]:

$\frac{\partial (\rho v_i)}{\partial t} + \frac{\partial \Pi_{ij}}{\partial x_j} = \rho f_i$

Here, the quantity $\rho v_i$ is the momentum density, and $\Pi_{ij}$ is the **[momentum flux](@entry_id:199796) tensor**. The derived expression for this tensor is:

$\Pi_{ij} = \rho v_i v_j - \sigma_{ij} = \rho v_i v_j + p\delta_{ij} - \tau_{ij}$

This form is powerful because it casts the equation as a balance between the local rate of change of momentum density, the divergence of its flux, and a [source term](@entry_id:269111). The flux has two components: $\rho v_i v_j$, the **convective [momentum flux](@entry_id:199796)** (momentum carried by the [fluid motion](@entry_id:182721) itself), and $-\sigma_{ij}$, the momentum flux transmitted by molecular interactions (pressure and viscous stresses).

#### Conservation of Energy and Viscous Dissipation

The [first law of thermodynamics](@entry_id:146485) governs the energy of a fluid. The total energy of a fluid parcel is the sum of its internal energy ($e$) and kinetic energy ($\frac{1}{2}|\mathbf{v}|^2$). An equation for the mechanical energy component can be derived by taking the dot product of the velocity vector $\mathbf{v}$ with the Cauchy momentum equation [@problem_id:525256]. This yields an evolution equation for the kinetic energy density:

$\rho \frac{D}{Dt}\left(\frac{1}{2}|\mathbf{v}|^2\right) = -\mathbf{v} \cdot \nabla p + \mathbf{v} \cdot (\nabla \cdot \boldsymbol{\tau}) + \rho \mathbf{v} \cdot \mathbf{g}$

The terms on the right-hand side represent the rate of work done on the fluid parcel per unit volume by pressure forces, [viscous forces](@entry_id:263294), and [body forces](@entry_id:174230), respectively. The viscous work term can be rewritten using a vector identity: $\mathbf{v} \cdot (\nabla \cdot \boldsymbol{\tau}) = \nabla \cdot (\boldsymbol{\tau} \cdot \mathbf{v}) - \boldsymbol{\tau} : \nabla\mathbf{v}$. The term $\nabla \cdot (\boldsymbol{\tau} \cdot \mathbf{v})$ is the rate of work done by viscous stresses at the boundary of the fluid element, while the second term has a unique physical significance.

The quantity $\Phi = \boldsymbol{\tau} : \nabla\mathbf{v}$ (or $\tau_{ij} \frac{\partial v_i}{\partial x_j}$ in [index notation](@entry_id:191923)) is the **[viscous dissipation](@entry_id:143708) function**. It is always non-negative ($\Phi \ge 0$) and represents the rate at which [mechanical energy](@entry_id:162989) is irreversibly converted into internal energy (heat) due to viscous friction within the fluid. This term is the source of [viscous heating](@entry_id:161646).

Using the [constitutive relation](@entry_id:268485) for a compressible Newtonian fluid, we can derive an explicit expression for the dissipation function in terms of velocity gradients [@problem_id:525256] [@problem_id:525205]. The result is often expressed using the **[strain-rate tensor](@entry_id:266108)**, $\mathbf{S} = \frac{1}{2}(\nabla\mathbf{v} + (\nabla\mathbf{v})^T)$, which describes the rate of deformation of a fluid element. The dissipation function is then [@problem_id:525205]:

$\Phi = 2\mu S_{ij}S_{ij} + \left(\kappa - \frac{2}{3}\mu\right)(S_{kk})^2$

where $S_{kk} = \nabla \cdot \mathbf{v}$ is the trace of the [strain-rate tensor](@entry_id:266108), representing the rate of [volumetric expansion](@entry_id:144241). This expression shows how both shear deformations (the $S_{ij}S_{ij}$ term) and volumetric deformations (the $(S_{kk})^2$ term) contribute to the irreversible loss of [mechanical energy](@entry_id:162989). For an incompressible flow, $S_{kk}=0$, and the dissipation simplifies to $\Phi = 2\mu S_{ij}S_{ij}$.

### Derived Concepts and Dynamical Quantities

From the fundamental governing equations, we can derive equations for other important physical quantities that provide deeper insight into the structure and dynamics of fluid flow.

#### Vorticity and Circulation

**Vorticity**, defined as the curl of the velocity field, $\boldsymbol{\omega} = \nabla \times \mathbf{v}$, is a point-wise measure of the local [angular velocity](@entry_id:192539) of the fluid. A flow with zero [vorticity](@entry_id:142747) is termed **irrotational**. The evolution of [vorticity](@entry_id:142747) is found by taking the curl of the [momentum equation](@entry_id:197225), which yields the **[vorticity transport equation](@entry_id:139098)**. For a compressible, viscous fluid, this equation is complex, but its terms reveal the physical mechanisms that can generate or destroy vorticity [@problem_id:525288]:

$\frac{D\boldsymbol{\omega}}{Dt} = (\boldsymbol{\omega} \cdot \nabla)\mathbf{v} - \boldsymbol{\omega}(\nabla \cdot \mathbf{v}) + \frac{\nabla\rho \times \nabla p}{\rho^2} + \nabla \times \left(\frac{1}{\rho}\nabla \cdot \boldsymbol{\tau}\right) + \nabla \times \mathbf{f}$

The terms on the right-hand side represent:
1.  **Vortex Stretching and Tilting**: $(\boldsymbol{\omega} \cdot \nabla)\mathbf{v}$ describes how vorticity is amplified or reoriented by velocity gradients, a key mechanism in turbulence.
2.  **Dilatation**: $-\boldsymbol{\omega}(\nabla \cdot \mathbf{v})$ accounts for changes in vorticity due to fluid expansion or compression.
3.  **Baroclinic Torque**: $\frac{\nabla\rho \times \nabla p}{\rho^2}$ generates [vorticity](@entry_id:142747) when gradients of density and pressure are misaligned. This is crucial in phenomena like sea breezes and [stellar convection](@entry_id:161265).
4.  **Viscous Torque and Diffusion**: The term involving $\boldsymbol{\tau}$ shows how viscosity can both diffuse [vorticity](@entry_id:142747) and generate it at boundaries.
5.  **Body Force Curl**: $\nabla \times \mathbf{f}$ shows that non-conservative body forces can be a source of vorticity.

A related integral quantity is **circulation**, defined as the [line integral](@entry_id:138107) of the velocity field around a closed curve $C$: $\Gamma = \oint_C \mathbf{v} \cdot d\mathbf{l}$. By Stokes' theorem, circulation is the flux of vorticity through the surface spanning the curve. **Kelvin's Circulation Theorem** states that for an ideal, barotropic fluid with conservative body forces, the circulation around a material curve (a curve that moves with the fluid) is constant in time: $\frac{D\Gamma}{Dt} = 0$.

However, in a viscous fluid, circulation is not conserved. The rate of change of circulation around a material curve is governed by viscous effects. For an incompressible fluid, this is given by [@problem_id:525316]:

$\frac{d\Gamma}{dt} = \nu \oint_C (\nabla \omega_z) \cdot \mathbf{n} \, ds$

This shows that the circulation only changes if there is a gradient of [vorticity](@entry_id:142747) at the boundary of the circuit, leading to a diffusion of vorticity across the boundary. A practical example is the decay of a vortex, where viscous forces cause the circulation to decrease over time [@problem_id:525316].

#### The Bernoulli Equation

For an ideal (inviscid) fluid, the Euler equation can be integrated along a [streamline](@entry_id:272773) under certain conditions to yield the celebrated **Bernoulli equation**. A more general result, the **unsteady Bernoulli equation**, can be derived for an **[irrotational flow](@entry_id:159258)** where $\mathbf{v} = \nabla\phi$ for some [velocity potential](@entry_id:262992) $\phi$. Using the vector identity $(\mathbf{v} \cdot \nabla)\mathbf{v} = \nabla(\frac{1}{2}|\mathbf{v}|^2) - \mathbf{v} \times (\nabla \times \mathbf{v})$, and setting the vorticity $\nabla \times \mathbf{v}$ to zero, the Euler equation becomes:

$\nabla\left(\frac{\partial\phi}{\partial t} + \frac{1}{2}|\mathbf{v}|^2 + h + \Phi_g\right) = \mathbf{f}_{nc}$

Here, we have assumed a barotropic fluid where $\frac{1}{\rho}\nabla p = \nabla h$ and a [body force](@entry_id:184443) decomposed into a conservative part $\mathbf{f}_c = -\nabla \Phi_g$ (e.g., gravity) and a non-conservative part $\mathbf{f}_{nc}$ [@problem_id:525240]. The expression inside the gradient defines the generalized Bernoulli function, $H$. This equation shows that $H$ is constant throughout the fluid domain *only if* the flow is steady ($\frac{\partial}{\partial t}=0$) and all forces are conservative ($\mathbf{f}_{nc}=0$). If [non-conservative forces](@entry_id:164833) are present, the Bernoulli function will vary from point to point, and its change along a path is determined by the work done by those [non-conservative forces](@entry_id:164833) [@problem_id:525240].

#### Introduction to Turbulent Flows: Reynolds Averaging

Most flows encountered in nature and engineering are turbulent, characterized by chaotic, unsteady, and three-dimensional fluctuations. Direct simulation of the Navier-Stokes equations for such flows is often intractable. A common approach is **Reynolds averaging**, where the [instantaneous velocity](@entry_id:167797) $U_i$ and pressure $P$ are decomposed into a mean component ($\overline{U}_i, \overline{P}$) and a fluctuating component ($u'_i, p'$):

$U_i = \overline{U}_i + u'_i, \quad P = \overline{P} + p'$

Substituting this decomposition into the incompressible Navier-Stokes equations and averaging yields the **Reynolds-Averaged Navier-Stokes (RANS) equations**. These equations govern the mean flow but contain a new term, the **Reynolds stress tensor**, $R_{ij} = -\rho\overline{u'_i u'_j}$. This tensor represents the net transport of momentum by the turbulent fluctuations and acts as an additional stress on the mean flow.

The appearance of the Reynolds stresses introduces a [closure problem](@entry_id:160656), as these new unknowns must be modeled. Second-[moment closure](@entry_id:199308) models attempt to solve this by deriving and modeling [transport equations](@entry_id:756133) for the Reynolds stresses themselves. A key term in the [transport equation](@entry_id:174281) for $\overline{u'_i u'_j}$ is the **production tensor**, $P_{ij}$ [@problem_id:525243]:

$P_{ij} = -\left(\overline{u'_i u'_k}\frac{\partial \overline{U}_j}{\partial x_k} + \overline{u'_j u'_k}\frac{\partial \overline{U}_i}{\partial x_k}\right)$

The production tensor describes the rate at which kinetic energy is transferred from the mean flow to the turbulent fluctuations through the action of the Reynolds stresses working against the [mean velocity](@entry_id:150038) gradients. This is the primary mechanism that sustains turbulence. For instance, in a flow with mean shear and rotation, the production of shear stress $\overline{u'_1 u'_2}$ depends directly on the [mean velocity](@entry_id:150038) gradients and the existing [normal stresses](@entry_id:260622), illustrating the complex interplay between the mean flow and the turbulent field [@problem_id:525243].

This chapter has laid out the mathematical foundation of [fluid mechanics](@entry_id:152498). These governing equations—continuity, Navier-Stokes, and energy—form a coupled system of [nonlinear partial differential equations](@entry_id:168847) whose solutions describe the vast and complex world of fluid motion.