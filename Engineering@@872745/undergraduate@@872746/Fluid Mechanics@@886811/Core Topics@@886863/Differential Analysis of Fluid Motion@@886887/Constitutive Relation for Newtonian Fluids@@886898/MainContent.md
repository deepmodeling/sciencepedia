## Introduction
To fully predict and understand fluid motion, we need more than just the universal laws of mass and momentum conservation. We must also describe how a specific fluid internally responds to forces—a connection provided by a [constitutive relation](@entry_id:268485). The Cauchy momentum equation relates fluid acceleration to internal stresses, but it leaves a critical question unanswered: what determines these stresses? Without a model linking stress to the fluid's deformation and motion, our system of equations remains incomplete. This article focuses on the most fundamental and widely applicable of these models: the [constitutive relation](@entry_id:268485) for Newtonian fluids, which include common substances like water and air.

We will begin in **"Principles and Mechanisms"** by exploring the foundational distinction between fluids and solids, leading to the development of Newton's law of viscosity. We will then generalize this concept into a complete three-dimensional tensor equation, revealing how viscosity generates both shear and [normal stresses](@entry_id:260622) and culminating in the derivation of the celebrated Navier-Stokes equations. The journey continues in **"Applications and Interdisciplinary Connections,"** where we will witness the remarkable power of this single law to explain and predict phenomena across a vast range of fields, from the [lubrication](@entry_id:272901) of engineering components and the flow of magma in geophysics to the propulsion of [microorganisms](@entry_id:164403) in biology. Finally, **"Hands-On Practices"** will challenge you to apply these principles to solve practical problems, solidifying your understanding of how [viscous forces](@entry_id:263294) govern fluid behavior in both simple and complex scenarios.

## Principles and Mechanisms

The behavior of a fluid in motion is fundamentally governed by the interplay of forces acting upon it. While the previous chapter discussed the conservation laws of mass and momentum, these laws alone are insufficient to predict [fluid motion](@entry_id:182721). The Cauchy momentum equation relates the acceleration of a fluid element to the divergence of the stress tensor, but it does not specify what the stress is. To close the system of equations, we require a **[constitutive relation](@entry_id:268485)**—a mathematical model that connects the internal stresses within a material to its motion and deformation. This chapter explores the principles and mechanisms underlying the [constitutive relation](@entry_id:268485) for the most commonly studied class of fluids: Newtonian fluids.

### The Defining Response of a Fluid to Stress

The essential difference between an elastic solid and a fluid lies in their response to an applied shear stress. An ideal elastic solid, when subjected to a shear stress, deforms until the internal elastic restoring force balances the external load, reaching a [static equilibrium](@entry_id:163498) with a [finite strain](@entry_id:749398). In contrast, a fluid continuously deforms, or flows, as long as a shear stress is applied. The fluid's resistance is not to the deformation itself, but to the *rate* of deformation.

Consider a thin layer of material placed between two [parallel plates](@entry_id:269827), where a constant shear stress $\tau_0$ is applied to the top plate.
If the material is a **Hookean elastic solid** with shear modulus $G$, its response is described by Hooke's Law, $\tau = G\gamma$, where $\gamma$ is the shear strain. Under the stress $\tau_0$, the material deforms by a fixed amount, resulting in a finite displacement $\delta_s$ of the top plate, where $\delta_s/h = \gamma = \tau_0/G$. The deformation ceases once this equilibrium is reached.

Now, if the material is a **Newtonian fluid** with [dynamic viscosity](@entry_id:268228) $\mu$, its response is fundamentally different. Instead of a fixed deformation, the fluid undergoes a continuous shearing motion. The applied stress is proportional to the [rate of shear strain](@entry_id:270048), $\dot{\gamma}$. For a simple shear flow, this rate is equal to the [velocity gradient](@entry_id:261686), $du/dy$. Therefore, $\tau_0 = \mu (du/dy)$. This constant stress induces a [constant velocity](@entry_id:170682) $U$ of the top plate, where $U/h = du/dy = \tau_0/\mu$. The displacement of the plate, $\delta_f$, increases linearly with time, $\delta_f = U T$, and will grow indefinitely as long as the stress is applied. The ratio of these displacements, $\delta_f/\delta_s = (GT)/\mu$, highlights that the fluid's deformation over time $T$ depends on the ratio of the solid's elastic stiffness $G$ to the fluid's viscous resistance $\mu$ [@problem_id:1795077]. This distinction is paramount: solids resist strain, while fluids resist the [rate of strain](@entry_id:267998).

### Newton's Law of Viscosity and Dynamic Viscosity

The relationship for the [simple shear](@entry_id:180497) flow described above is the historical basis for **Newton's law of viscosity**. For a one-dimensional shear flow, where the velocity $u$ in the $x$-direction varies only with the transverse coordinate $y$, the shear stress $\tau_{yx}$ (the stress acting on a plane with its normal in the $y$-direction, in the $x$-direction) is given by:
$$
\tau_{yx} = \mu \frac{du}{dy}
$$
The constant of proportionality, $\mu$, is called the **coefficient of dynamic viscosity**, or simply the **dynamic viscosity**. It is a property of the fluid that measures its [intrinsic resistance](@entry_id:166682) to shear flow. Fluids with high viscosity, like honey, resist motion strongly, while fluids with low viscosity, like air, offer much less resistance. The term $\frac{du}{dy}$ is the **[velocity gradient](@entry_id:261686)**, also known as the **[rate of shear strain](@entry_id:270048)** or **shear rate**.

This simple relationship forms the basis for measuring viscosity. In a typical parallel-plate viscometer, a fluid layer of thickness $h$ is sheared between a stationary plate and a moving plate. If a force $F$ is applied over an area $A$ to move the top plate at a constant velocity $v$, the shear stress is $\tau = F/A$. Assuming a linear velocity profile, the shear rate is constant and equals $v/h$. By rearranging Newton's law of viscosity, we can determine the fluid's viscosity from these measurable quantities [@problem_id:1775537]:
$$
\mu = \frac{\tau}{du/dy} = \frac{F/A}{v/h}
$$
From this equation, the SI units of [dynamic viscosity](@entry_id:268228) can be deduced. With force in Newtons (N), area in square meters ($m^2$), velocity in meters per second (m/s), and distance in meters (m), the unit for $\mu$ is $(\text{N}/\text{m}^2) \cdot (\text{m}/(\text{m}/\text{s})) = \text{Pa} \cdot \text{s}$. Given that $1 \text{ N} = 1 \text{ kg} \cdot \text{m}/\text{s}^2$, this is equivalent to $(\text{kg} \cdot \text{m}^{-1} \cdot \text{s}^{-2}) \cdot \text{s} = \text{kg} \cdot \text{m}^{-1} \cdot \text{s}^{-1}$.

### The General Constitutive Relation for a Newtonian Fluid

Real fluid flows are rarely one-dimensional. Fluid elements can be stretched, compressed, and sheared simultaneously in all three dimensions. To describe such complex motions, we must generalize Newton's law of viscosity using the language of tensors.

The state of stress at any point in a continuum is completely described by the second-order **Cauchy stress tensor**, denoted $\boldsymbol{\sigma}$ or $\sigma_{ij}$. The component $\sigma_{ij}$ represents the force per unit area on a surface with its normal in the $i$-direction, acting in the $j$-direction. The diagonal components ($\sigma_{xx}, \sigma_{yy}, \sigma_{zz}$) are **[normal stresses](@entry_id:260622)**, which act perpendicularly to the surface (positive for tension, negative for compression). The off-diagonal components ($\sigma_{xy}, \sigma_{yx}$, etc.) are **shear stresses**, which act tangentially to the surface. For non-polar fluids, the stress tensor is symmetric, $\sigma_{ij} = \sigma_{ji}$.

The motion and deformation of a fluid element are described by the **[rate-of-strain tensor](@entry_id:260652)**, $\mathbf{E}$ (also denoted $\boldsymbol{\varepsilon}$), whose components are given by:
$$
\varepsilon_{ij} = \frac{1}{2} \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right)
$$
where $\mathbf{u} = (u_1, u_2, u_3)$ is the velocity vector and $\mathbf{x} = (x_1, x_2, x_3)$ are the coordinates. The diagonal components, like $\varepsilon_{xx} = \partial u_x / \partial x$, represent the rate of [extensional strain](@entry_id:183817) (stretching or compression) of the fluid element along the axes. The off-diagonal components, like $\varepsilon_{xy} = \frac{1}{2}(\partial u_x / \partial y + \partial u_y / \partial x)$, represent half the [rate of shear strain](@entry_id:270048) (the rate of change of the angle between line segments initially parallel to the axes).

For an **isotropic Newtonian fluid** (one whose properties are independent of direction), the [constitutive relation](@entry_id:268485) posits a linear relationship between the stress and rate-of-strain tensors. For an incompressible fluid, this relationship takes the form:
$$
\sigma_{ij} = -p\delta_{ij} + 2\mu\varepsilon_{ij}
$$
Here, $p$ is the **thermodynamic pressure**, a [scalar field](@entry_id:154310) representing the isotropic part of the stress that exists even in a fluid at rest. The term $\delta_{ij}$ is the **Kronecker delta** ($\delta_{ij} = 1$ if $i=j$ and $0$ if $i \neq j$). The term $\tau_{ij} = 2\mu\varepsilon_{ij}$ is the **viscous stress tensor** (or [deviatoric stress tensor](@entry_id:267642)), representing the part of the stress that arises purely from the fluid's motion.

Let's verify this general law for the [simple shear](@entry_id:180497) flow $u(y) = (U/h)y$, with $v=w=0$ [@problem_id:1795116]. The only non-zero velocity gradient is $\partial u / \partial y = U/h$. The components of the [rate-of-strain tensor](@entry_id:260652) are:
$$
\varepsilon_{xy} = \varepsilon_{yx} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right) = \frac{1}{2} \left( \frac{U}{h} + 0 \right) = \frac{U}{2h}
$$
All other components, including the diagonal ones like $\varepsilon_{xx} = \partial u / \partial x = 0$, are zero. The [viscous stress](@entry_id:261328) components are then:
$$
\tau_{xy} = \tau_{yx} = 2\mu\varepsilon_{xy} = 2\mu \left( \frac{U}{2h} \right) = \mu \frac{U}{h}
$$
All other [viscous stress](@entry_id:261328) components are zero. The total stress component $\sigma_{xy}$ is simply $\tau_{xy}$ because the pressure term vanishes ($\delta_{xy} = 0$). This result perfectly matches the one-dimensional form of Newton's law. This exercise confirms the consistency of the general tensor formulation.

The power dissipated by viscous forces per unit volume is given by the product of the viscous stress and the [rate of strain](@entry_id:267998). In the [simple shear](@entry_id:180497) flow example, the only contribution comes from the $\tau_{xy}$ component. The total power required to move the top plate is the drag force times the plate velocity. The drag force is the shear stress multiplied by the plate area, $F_{drag} = \tau_{xy} A$. Thus, the power is $P = F_{drag} U = (\mu \frac{U}{h} A) U = \mu \frac{A}{h} U^2$ [@problem_id:1803032]. This power is converted into internal energy within the fluid, manifesting as heat.

### Viscous Normal Stresses in Extensional Flows

A common misconception is that viscosity only generates shear stresses. However, the general [constitutive relation](@entry_id:268485) $\tau_{ij} = 2\mu\varepsilon_{ij}$ reveals that viscous stresses can also be normal to a surface. This occurs in flows where fluid elements are being stretched or compressed.

Consider a two-dimensional **stagnation-point flow**, described by the [velocity field](@entry_id:271461) $\mathbf{v} = (kx, -ky, 0)$, where $k$ is a positive constant [@problem_id:1794848]. This flow models the fluid motion near a point where the flow impinges on a surface. The components of the [rate-of-strain tensor](@entry_id:260652) are:
$$
\varepsilon_{xx} = \frac{\partial u}{\partial x} = k
$$
$$
\varepsilon_{yy} = \frac{\partial v}{\partial y} = -k
$$
$$
\varepsilon_{xy} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right) = \frac{1}{2} (0 + 0) = 0
$$
The viscous stress components are therefore:
$$
\tau_{xx} = 2\mu\varepsilon_{xx} = 2\mu k
$$
$$
\tau_{yy} = 2\mu\varepsilon_{yy} = -2\mu k
$$
$$
\tau_{xy} = 0
$$
Here, we see non-zero **viscous [normal stresses](@entry_id:260622)**. The term $\tau_{xx} = 2\mu k$ represents a tensile stress in the $x$-direction due to the fluid being stretched along that axis. Similarly, $\tau_{yy} = -2\mu k$ is a compressive stress in the $y$-direction as the fluid is squeezed. These stresses are purely viscous in origin and exist in addition to the thermodynamic pressure $p$. The total normal stress in the x-direction, for instance, is $\sigma_{xx} = -p + 2\mu k$. The pressure field $p(x,y)$ itself is affected by the flow's inertia and can be found by solving the [momentum equation](@entry_id:197225) [@problem_id:1744156].

### The Role of Viscosity in the Momentum Equation

The [constitutive relation](@entry_id:268485) is the key that allows us to express the abstract stress tensor in the Cauchy momentum equation in terms of the velocity field, yielding a solvable equation. The [net force](@entry_id:163825) on a fluid element is due to spatial gradients in stress. The [viscous force](@entry_id:264591) per unit volume is the divergence of the viscous stress tensor, $\mathbf{f}_{visc} = \nabla \cdot \boldsymbol{\tau}$.

For an incompressible Newtonian fluid with constant viscosity $\mu$, this term simplifies remarkably:
$$
(\nabla \cdot \boldsymbol{\tau})_i = \frac{\partial \tau_{ij}}{\partial x_j} = \frac{\partial}{\partial x_j} \left[ \mu \left( \frac{\partial u_i}{\partial x_j} + \frac{\partial u_j}{\partial x_i} \right) \right] = \mu \left( \frac{\partial^2 u_i}{\partial x_j \partial x_j} + \frac{\partial}{\partial x_i} \left( \frac{\partial u_j}{\partial x_j} \right) \right)
$$
The first term is the Laplacian of the velocity component, $\nabla^2 u_i$. The second term involves the divergence of the [velocity field](@entry_id:271461), $\nabla \cdot \mathbf{u} = \partial u_j / \partial x_j$. For an **[incompressible fluid](@entry_id:262924)**, the [continuity equation](@entry_id:145242) requires $\nabla \cdot \mathbf{u} = 0$. Consequently, the [viscous force](@entry_id:264591) term simplifies to:
$$
\mathbf{f}_{visc} = \nabla \cdot \boldsymbol{\tau} = \mu \nabla^2 \mathbf{u}
$$
This result is demonstrated in the context of a flow profile such as $\mathbf{u} = (Ay^2, 0, 0)$, where the only non-zero component of the [viscous force](@entry_id:264591) is $(\nabla \cdot \boldsymbol{\tau})_x = \mu \nabla^2 u_x = \mu (d^2/dy^2)(Ay^2) = 2\mu A$ [@problem_id:1746673].

Substituting this into the Cauchy [momentum equation](@entry_id:197225) gives the celebrated **Navier-Stokes equation for an incompressible Newtonian fluid**:
$$
\rho \frac{D\mathbf{u}}{Dt} = -\nabla p + \rho \mathbf{g} + \mu \nabla^2 \mathbf{u}
$$
Here, the term $\mu \nabla^2 \mathbf{u}$ represents the net [viscous force](@entry_id:264591) per unit volume. It acts as a diffusion term, smearing out velocity gradients in the flow. This diffusive nature of viscosity can be seen through its effect on **vorticity**, $\boldsymbol{\omega} = \nabla \times \mathbf{u}$. By taking the curl of the [viscous force](@entry_id:264591) term, one finds that $\nabla \times \mathbf{f}_{visc} = \mu \nabla^2 \boldsymbol{\omega}$ [@problem_id:1744132]. This means that gradients in vorticity are smoothed out by viscosity, a process analogous to the diffusion of heat.

### Extension to Compressible Fluids and Bulk Viscosity

Our discussion has so far been restricted to [incompressible fluids](@entry_id:181066), where the volume of a fluid element is preserved ($\nabla \cdot \mathbf{u} = 0$). When a fluid is compressible, its volume can change, and this introduces an additional mode of viscous resistance. The rate of volumetric strain, or **dilatation rate**, is given by $\nabla \cdot \mathbf{u}$.

For a compressible, isotropic Newtonian fluid, the [constitutive relation](@entry_id:268485) must be modified to account for stresses arising from this dilatation. The most general linear relationship is:
$$
\sigma_{ij} = -p\delta_{ij} + \lambda(\nabla \cdot \mathbf{u})\delta_{ij} + 2\mu\varepsilon_{ij}
$$
This equation introduces a new material property, $\lambda$, known as the **second coefficient of viscosity**. The term $\lambda(\nabla \cdot \mathbf{u})\delta_{ij}$ represents an isotropic viscous stress that resists the rate of change of the fluid element's volume [@problem_id:1526392].

It is often convenient to decompose the [rate-of-strain tensor](@entry_id:260652) into a deviatoric (trace-free) part and a spherical (trace) part. The trace is $\varepsilon_{kk} = \nabla \cdot \mathbf{u}$. The viscous stress can then be written as:
$$
\tau_{ij} = 2\mu \left(\varepsilon_{ij} - \frac{1}{3} (\nabla \cdot \mathbf{u}) \delta_{ij}\right) + K (\nabla \cdot \mathbf{u}) \delta_{ij}
$$
Here, the first term represents resistance to isochoric (volume-preserving) shear deformation, while the second term represents resistance to volumetric deformation. The coefficient $K = \lambda + \frac{2}{3}\mu$ is called the **coefficient of [bulk viscosity](@entry_id:187773)**, or simply **[bulk viscosity](@entry_id:187773)**. It directly quantifies the fluid's resistance to rapid compression or expansion. For many practical applications involving monatomic gases, the **Stokes' hypothesis** is invoked, which assumes $K=0$ (or $\lambda = -2/3 \mu$). However, this is an approximation and does not hold for all fluids, particularly polyatomic gases and liquids.

### Thermodynamic Constraints on Viscosity

The coefficients of viscosity are not arbitrary; they are constrained by the fundamental laws of thermodynamics. The process of viscous deformation is inherently dissipative, meaning it converts ordered [mechanical energy](@entry_id:162989) into disordered internal energy (heat). The rate of this energy conversion per unit volume is the **[viscous dissipation](@entry_id:143708) function**, $\Phi_v$, given by the inner product of the viscous stress and rate-of-strain tensors: $\Phi_v = \tau_{ij}\varepsilon_{ij}$.

The Second Law of Thermodynamics requires that entropy must increase in any [irreversible process](@entry_id:144335). For fluid flow, this implies that [viscous dissipation](@entry_id:143708) must always be non-negative, $\Phi_v \ge 0$. A fluid cannot spontaneously create kinetic energy from its internal heat through viscous action.

By substituting the general compressible [constitutive relation](@entry_id:268485) into the expression for $\Phi_v$, we can derive the constraints on $\mu$ and $K$ [@problem_id:1744157]. The calculation shows that the dissipation function can be elegantly expressed as a sum of two independent terms:
$$
\Phi_v = 2\mu \varepsilon'_{ij}\varepsilon'_{ij} + K (\varepsilon_{kk})^2
$$
where $\varepsilon'_{ij}$ is the trace-free (deviatoric) part of the [rate-of-strain tensor](@entry_id:260652). The term $\varepsilon'_{ij}\varepsilon'_{ij}$ is the sum of the squares of the [deviatoric strain](@entry_id:201263)-rate components and is always non-negative. Similarly, $(\varepsilon_{kk})^2 = (\nabla \cdot \mathbf{u})^2$ is also always non-negative.

For $\Phi_v$ to be non-negative for any arbitrary flow (i.e., for any possible values of $\varepsilon'_{ij}$ and $\varepsilon_{kk}$), the coefficients multiplying these non-negative terms must themselves be non-negative. This leads to the fundamental thermodynamic constraints:
$$
\mu \ge 0 \quad \text{and} \quad K \ge 0
$$
The [dynamic viscosity](@entry_id:268228) and the bulk viscosity must both be non-negative. This rigorous result, grounded in the Second Law of Thermodynamics, confirms our physical intuition that viscosity is a dissipative, or energy-losing, mechanism.