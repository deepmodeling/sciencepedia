## Introduction
The direct simulation of complete, full-scale combustion systems remains a grand challenge in computational science due to prohibitive computational costs. To overcome this hurdle, engineers and scientists often exploit inherent geometric and physical regularities within a system. Symmetry and [periodic boundary conditions](@entry_id:147809) are powerful mathematical tools that allow the computational domain to be reduced to a fundamental repeating unit, dramatically decreasing simulation time and memory requirements while preserving the essential physics. This article addresses the critical need for a comprehensive understanding of how to correctly formulate and apply these boundary conditions in the context of complex, [reacting flows](@entry_id:1130631).

This article will guide you through the theoretical underpinnings, practical applications, and numerical implementation of these essential techniques. In "Principles and Mechanisms," we will derive the boundary conditions from fundamental physical properties and explore their impact on conservation laws. The "Applications and Interdisciplinary Connections" chapter will demonstrate how these concepts are leveraged to study everything from idealized flames to full gas turbine combustors, and we will see how the same principles apply across diverse scientific fields. Finally, "Hands-On Practices" will provide concrete problems to solidify your understanding and bridge the gap between theory and implementation.

## Principles and Mechanisms

In the computational analysis of combustion and other [reactive flows](@entry_id:190684), the direct simulation of complete, full-scale engineering systems is often prohibitively expensive. A powerful strategy to render such problems tractable is to exploit symmetries and periodicities within the system. By identifying a fundamental repeating unit or a plane of reflection, the computational domain can be reduced to a fraction of its physical size, dramatically decreasing the required computational resources without sacrificing fidelity. This chapter elucidates the fundamental principles governing symmetry and periodic boundary conditions, their mathematical formulation, and their practical implementation within the framework of computational fluid dynamics for [reacting flows](@entry_id:1130631).

### The Principle of Mirror Symmetry

Many physical systems, from canonical flames to complex combustors, exhibit a degree of [mirror symmetry](@entry_id:158730). A flow is considered mirror-symmetric with respect to a plane if the physical state at any point on one side of the plane is a mirror image of the state at the corresponding point on the other side. Exploiting this property allows a simulation to be performed on only half of the domain, with a special set of boundary conditions applied at the [symmetry plane](@entry_id:1132744). The derivation of these conditions stems directly from the transformation properties of physical quantities under reflection.

Let us consider a smooth [plane of symmetry](@entry_id:198308), $\Sigma$, defined by a [unit normal vector](@entry_id:178851) $\hat{\boldsymbol{n}}$. A reflection, $R$, is a geometric operation that maps a point $\boldsymbol{x}$ to its mirror image $\boldsymbol{x}' = R(\boldsymbol{x})$ across the plane. Physical fields transform under this operation according to their tensorial nature.

**Scalar fields**, such as pressure $p$, temperature $T$, density $\rho$, and species mass fractions $Y_k$, are invariant under reflection. This means their value at a point is identical to their value at the reflected point. If we establish a [local coordinate system](@entry_id:751394) where $n$ is the distance along the normal $\hat{\boldsymbol{n}}$ from the plane, this invariance implies that a [scalar field](@entry_id:154310) $\phi$ is an **[even function](@entry_id:164802)** of the normal coordinate:
$$ \phi(\boldsymbol{x}_t, -n) = \phi(\boldsymbol{x}_t, n) $$
where $\boldsymbol{x}_t$ represents the coordinates tangential to the plane. For a sufficiently smooth field, a fundamental property of [even functions](@entry_id:163605) is that their derivative with respect to the symmetric coordinate must be zero at the [plane of symmetry](@entry_id:198308) ($n=0$). Consequently, the normal derivative of any scalar field must vanish at the symmetry plane :
$$ \frac{\partial \phi}{\partial n} \equiv \hat{\boldsymbol{n}} \cdot \nabla \phi = 0 \quad \text{at } \Sigma $$
This condition has a profound physical meaning. For temperature and species, it implies that the diffusive fluxes normal to the plane are zero. For instance, if the heat flux is governed by Fourier's law, $\boldsymbol{q} = -\lambda \nabla T$, then the zero-normal-gradient condition on temperature ensures that the normal component of the heat flux, $\boldsymbol{q} \cdot \hat{\boldsymbol{n}}$, is zero. Similarly, for species fluxes governed by Fick's law, $\boldsymbol{J}_k = -\rho D_k \nabla Y_k$, the condition $\partial Y_k / \partial n = 0$ ensures zero normal diffusive mass flux for each species . In more complex transport models with cross-effects (e.g., Soret and Dufour effects), the fundamental conditions are the vanishing of the total normal fluxes, $\mathbf{n}\cdot \mathbf{q}=0$ and $\mathbf{n}\cdot \mathbf{J}_k=0$, which are typically satisfied when the primary gradients vanish .

**Vector fields**, such as velocity $\boldsymbol{u}$, transform differently. A velocity vector at a reflected point is the reflection of the original vector. This means its component normal to the plane is reversed, while its components tangential to the plane are preserved. Decomposing the velocity into its normal component, $u_n = \boldsymbol{u} \cdot \hat{\boldsymbol{n}}$, and its tangential component, $\boldsymbol{u}_t = \boldsymbol{u} - u_n \hat{\boldsymbol{n}}$, we find their parity behaviors are distinct :
*   The normal velocity component, $u_n$, is an **[odd function](@entry_id:175940)** of the normal coordinate $n$: $u_n(\boldsymbol{x}_t, -n) = -u_n(\boldsymbol{x}_t, n)$.
*   The tangential velocity component, $\boldsymbol{u}_t$, is an **[even function](@entry_id:164802)** of the normal coordinate $n$: $\boldsymbol{u}_t(\boldsymbol{x}_t, -n) = \boldsymbol{u}_t(\boldsymbol{x}_t, n)$.

From these parity properties, we derive the boundary conditions for velocity at the [symmetry plane](@entry_id:1132744) ($n=0$). An [odd function](@entry_id:175940) must be zero at the origin, so:
$$ u_n = 0 \quad \text{at } \Sigma $$
This is the **[no-penetration condition](@entry_id:191795)**, which ensures that no mass flows across the symmetry plane. The tangential velocity, being an [even function](@entry_id:164802), has a zero [normal derivative](@entry_id:169511) at the plane:
$$ \frac{\partial \boldsymbol{u}_t}{\partial n} = \mathbf{0} \quad \text{at } \Sigma $$
This is a **free-[slip condition](@entry_id:1131753)**. It implies that the [symmetry plane](@entry_id:1132744) exerts no tangential shear stress on the fluid. To see this more formally, consider the normal-tangential component of the Newtonian [viscous stress](@entry_id:261328) tensor, $\tau_{nt}$. In Cartesian coordinates with the plane at $x=0$, this would be $\tau_{xy} = \mu (\partial u_x / \partial y + \partial u_y / \partial x)$. The term $\partial u_y / \partial x$ corresponds to $\partial u_t / \partial n$, which we found to be zero. The term $\partial u_x / \partial y$ corresponds to the tangential derivative of the normal velocity, $\partial u_n / \partial y$. Since $u_n$ is an [odd function](@entry_id:175940) of the normal coordinate $x$, its derivative with respect to a tangential coordinate like $y$ remains odd in $x$ and must therefore also be zero at $x=0$. Thus, both terms in the shear stress expression vanish, leading to zero shear stress at the symmetry plane, $\tau_{nt}|_{\Sigma}=0$ .

In summary, for a [reacting flow](@entry_id:754105) problem with a plane of [mirror symmetry](@entry_id:158730), the complete set of boundary conditions to be applied at that plane is:
*   **No penetration:** $u_n = 0$
*   **Zero normal gradient for all scalars:** $\partial p/\partial n = 0$, $\partial T/\partial n = 0$, $\partial Y_k/\partial n = 0$
*   **Zero normal gradient for tangential velocity:** $\partial \boldsymbol{u}_t/\partial n = \mathbf{0}$

These conditions collectively ensure that simulating one half of the domain is an exact representation of the full symmetric problem .

### The Principle of Periodicity

Periodic boundary conditions are employed when a system's properties are statistically homogeneous in one or more directions. This is common in the study of turbulence, where one simulates a representative "box" of fluid that is considered to be part of an infinitely repeating pattern. This concept can be applied to both translational and rotational configurations.

#### Spatial Periodicity in Cartesian Domains

Consider a rectangular domain $\Omega = [0,L_x] \times [0,L_y] \times [0,L_z]$. If the flow is periodic in all three directions, the domain is topologically equivalent to a three-dimensional torus ($\mathbb{T}^3$). This means that the faces of the domain are identified with their opposites; for example, the plane at $x=0$ is physically the same as the plane at $x=L_x$.

For any field variable $\phi$ (scalar or vector component), this physical identification implies a strict mathematical equality at corresponding points on opposite faces. These are the "wrap-around" equalities that define periodicity :
*   **x-periodicity:** $\phi(0,y,z,t) = \phi(L_x,y,z,t)$
*   **y-periodicity:** $\phi(x,0,z,t) = \phi(x,L_y,z,t)$
*   **z-periodicity:** $\phi(x,y,0,t) = \phi(x,y,L_z,t)$

These conditions must hold for all fundamental fields describing the fluid state, including all components of velocity $\boldsymbol{u}$, pressure $p$, temperature $T$, and all species mass fractions $Y_k$. This ensures that the fluid state and all its derivatives are continuous across the periodic boundaries, allowing structures like turbulent eddies to exit one side of the domain and re-enter seamlessly from the other.

A profound consequence of periodicity is its effect on global conservation laws. For any conserved quantity, its governing equation can be integrated over the entire domain $\Omega$. By the Gauss Divergence Theorem, the [volume integral](@entry_id:265381) of the divergence of a flux is equal to the net flux through the boundary $\partial \Omega$. In a periodic domain, the flux out of one face is exactly matched by the flux into the opposite face. Because the outward normal vectors on opposite faces are antiparallel, their contributions to the total [surface integral](@entry_id:275394) cancel perfectly. Thus, the net flux of any quantity across the boundary of a periodic domain is identically zero.

This simplifies the global budget equations for total mass $M$, momentum $\boldsymbol{P}$, energy $E_{\text{tot}}$, and species mass $N_i$ to only include volumetric source terms :
$$ \frac{\mathrm{d}M}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\,\mathrm{d}V = 0 $$
$$ \frac{\mathrm{d}\boldsymbol{P}}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\boldsymbol{u}\,\mathrm{d}V = \int_{\Omega}\rho\boldsymbol{f}\,\mathrm{d}V $$
$$ \frac{\mathrm{d}E_{\text{tot}}}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho E\,\mathrm{d}V = \int_{\Omega}\left(\rho\,\boldsymbol{u}\cdot\boldsymbol{f} + \sum_i h_i \omega_i\right)\,\mathrm{d}V $$
$$ \frac{\mathrm{d}N_i}{\mathrm{d}t} = \frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho Y_i\,\mathrm{d}V = \int_{\Omega}\omega_i\,\mathrm{d}V $$
Here, $\boldsymbol{f}$ is a body force, and $\omega_i$ are chemical source terms. These equations highlight that a periodic domain is a closed system with respect to mass, momentum, and [energy transport](@entry_id:183081) across its boundaries, making it an ideal setting for studying the evolution of a system due to internal processes like chemical reaction and viscous dissipation, or homogeneous forcing.

#### Cyclic Periodicity in Curvilinear Coordinates

Many engineering devices, such as gas turbine combustors, possess rotational or [cyclic symmetry](@entry_id:193404). For an annular combustor with $N$ identical sectors, one can simulate a single sector of angle $\Delta\theta = 2\pi/N$ and apply cyclic [periodic boundary conditions](@entry_id:147809).

The principle is the same as for Cartesian periodicity: the physical state at a point $(r, \theta_0, z)$ on one azimuthal boundary is identical to the state at the corresponding point $(r, \theta_0+\Delta\theta, z)$ on the other. For scalar quantities, this again means simple equality: $\phi(r, \theta_0, z) = \phi(r, \theta_0+\Delta\theta, z)$.

However, for vector quantities, the situation is more complex because the cylindrical [coordinate basis](@entry_id:270149) vectors, $\boldsymbol{e}_r(\theta)$ and $\boldsymbol{e}_\theta(\theta)$, rotate with the angle $\theta$. The physical vector $\boldsymbol{a}$ at the two corresponding points is the same, but its components in the two different local bases are not. To find the mapping between components, we must account for the rotation of the basis. If the basis at $\theta_0+\Delta\theta$ is rotated by an angle $\Delta\theta$ relative to the basis at $\theta_0$, then to keep the physical vector invariant, its components must be counter-rotated by an angle $-\Delta\theta$. This leads to the following transformation for the cylindrical vector components $[a_r, a_\theta, a_z]^\top$ from the boundary at $\theta_0$ (denoted by superscript $-$) to the boundary at $\theta_0+\Delta\theta$ (superscript $+$) :
$$
\begin{pmatrix} a_r \\ a_\theta \\ a_z \end{pmatrix}^{+}
=
\begin{pmatrix}
\cos\Delta\theta  & \sin\Delta\theta  & 0\\
-\sin\Delta\theta & \cos\Delta\theta  & 0\\
0 & 0 & 1
\end{pmatrix}
\begin{pmatrix} a_r \\ a_\theta \\ a_z \end{pmatrix}^{-}
$$
This transformation correctly maps the vector components between the two periodic boundaries, ensuring that the physical vector field is continuous across the periodic interface.

### Numerical Implementation and Advanced Considerations

The translation of these continuous mathematical principles into a discrete numerical algorithm requires careful attention to detail, particularly within a Finite Volume Method (FVM).

#### Discretization of Periodic Boundary Conditions

In a cell-centered FVM, the domain is divided into a finite number of control volumes or cells, and the solution is stored as cell-averaged values. To compute fluxes at the faces of cells near a boundary, information is needed from outside the domain. This is provided by **ghost cells**. For a periodic boundary, the values in the ghost cells are populated by copying from cells on the opposite side of the interior domain. For a 1D domain with cells indexed $i=1, \dots, N_x$, the [ghost cells](@entry_id:634508) at the left boundary (e.g., $i=0, -1, \dots$) are filled from the right side of the interior, and vice versa :
$$ U_{0,j,k} = U_{N_x,j,k} \quad \text{and} \quad U_{N_x+1,j,k} = U_{1,j,k} $$
This wrap-around indexing is applied to the entire vector of [conserved variables](@entry_id:747720) $U = (\rho, \rho\boldsymbol{u}, \rho E, \rho Y_k)^\top$.

This ghost-cell procedure has a critical and elegant consequence for [discrete conservation](@entry_id:1123819). When the numerical flux across a boundary face is computed (e.g., at face $x_{1/2}$ between cells 0 and 1), the stencil uses the wrapped state from the opposite boundary. This automatically ensures that the numerical flux computed at the left boundary face is identical to the flux computed at the right boundary face: $F^x_{1/2,j,k} = F^x_{N_x+1/2,j,k}$. When the flux divergences are summed over all cells in the domain, these boundary fluxes cancel in a telescoping sum, leading to a discretely [conservative scheme](@entry_id:747714) that mirrors the global conservation property of the continuous equations.

#### Periodicity in Low-Mach Number Formulations

In many combustion scenarios, flow speeds are much lower than the speed of sound. In this low-Mach number regime, acoustic waves can be filtered out to allow for larger computational time steps. This is achieved by decomposing the pressure field into a spatially uniform **thermodynamic pressure** $p_0(t)$ and a small, spatially varying **[hydrodynamic pressure](@entry_id:1126255)** $p_h(\boldsymbol{x},t)$:
$$ p(\boldsymbol{x},t) = p_0(t) + p_h(\boldsymbol{x},t) $$
The gradient of the pressure, which drives the flow in the momentum equation, is simply $\nabla p_h$. Taking the divergence of the momentum equation leads to an elliptic (Poisson-type) equation for the hydrodynamic pressure $p_h$.

In a periodic domain, this elliptic equation presents a challenge: its solution is only defined up to an arbitrary additive constant. If $p_h(\boldsymbol{x},t)$ is a solution, so is $p_h(\boldsymbol{x},t)+C(t)$. To obtain a unique solution, a **[gauge condition](@entry_id:749729)** must be imposed. The standard choice is to fix the volume average of the [hydrodynamic pressure](@entry_id:1126255) to zero :
$$ \langle p_h \rangle_V = \frac{1}{V}\int_V p_h(\boldsymbol{x},t)\,\mathrm{d}V = 0 $$
This constraint removes the ambiguity and renders the problem well-posed, allowing for stable and accurate simulation of low-Mach [reacting flows](@entry_id:1130631) in [periodic domains](@entry_id:753347).

#### Symmetries in Turbulent Reacting Flows: A Conceptual Overview

While symmetry and periodicity are powerful idealizations, it is crucial to understand when they are physically justifiable. In turbulent [reacting flows](@entry_id:1130631), the instantaneous fields are chaotic, three-dimensional, and highly asymmetric. Symmetry, in this context, almost always refers to **[statistical symmetry](@entry_id:272586)**.

Physical phenomena intrinsic to combustion often break symmetries . For example:
*   **Heat release and density variation:** In a premixed flame, the transition from cold, dense reactants to hot, light products breaks [translational symmetry](@entry_id:171614) in the direction normal to the flame.
*   **Buoyancy:** The presence of gravity, $\boldsymbol{g}$, defines a preferred direction in space. This breaks general [rotational symmetry](@entry_id:137077), though it may still permit axisymmetry about the gravity vector, as seen in a vertical buoyant flame.

Despite the complexity of the instantaneous fields, [statistical symmetry](@entry_id:272586) can be a valid and powerful modeling assumption. If the geometry, boundary conditions, and governing equations themselves do not have a [preferred orientation](@entry_id:190900) or location, then the averaged statistics of the flow will not either.
*   In a simulation of a statistically planar flame, while symmetry is broken in the normal direction, the statistics can be homogeneous in the tangential directions, justifying the use of [periodic boundary conditions](@entry_id:147809) there.
*   In a [turbulent jet](@entry_id:271164) from an axisymmetric nozzle, even though the instantaneous flow contains non-axisymmetric eddies, the time-averaged flow will be axisymmetric, justifying a 2D RANS simulation or analysis of averaged 3D LES data in [cylindrical coordinates](@entry_id:271645).

The choice to impose a symmetry or [periodic boundary condition](@entry_id:271298) is therefore a profound modeling decision, rooted in an understanding of which symmetries are preserved by the fundamental physics and which are broken, and whether the interest lies in the instantaneous realization of a flow or its long-term statistical behavior.