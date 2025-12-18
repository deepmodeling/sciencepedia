## Introduction
The stable confinement of a high-temperature plasma is the central challenge of magnetic fusion energy research. Achieving this requires a precise balance where the plasma's [internal pressure](@entry_id:153696) is contained by carefully shaped magnetic fields. While simple models often assume a predefined plasma shape, a realistic plasma's boundary is not fixed; it is a dynamic entity determined by a complex, self-consistent interplay with the external magnetic coils that generate and control it. This article addresses the critical task of modeling this interaction using free-boundary equilibrium solvers, which are foundational tools in modern [computational fusion science](@entry_id:1122784). By working through this material, you will gain a comprehensive understanding of how [plasma equilibrium](@entry_id:184963) is calculated when the boundary is unknown. The following chapters will first deconstruct the core **Principles and Mechanisms**, from the governing Grad-Shafranov equation to the numerical strategies that capture [plasma-coil coupling](@entry_id:1129761). Next, we will explore the pivotal **Applications and Interdisciplinary Connections**, showing how these solvers are used for [plasma control](@entry_id:753487), stability analysis, and advanced device design. Finally, the **Hands-On Practices** section will introduce exercises designed to build practical skills in implementing and analyzing these essential computational models.

## Principles and Mechanisms

This chapter elucidates the fundamental principles governing magnetohydrodynamic (MHD) equilibrium in toroidal fusion devices and the computational mechanisms used to model them. We will begin by establishing the foundational concepts of flux surfaces and the Grad-Shafranov equation, then differentiate between idealized fixed-boundary problems and realistic free-boundary problems, and finally, delve into the critical mechanism of plasma–coil coupling and the computational strategies employed in modern free-boundary solvers.

### The Foundation of Magnetohydrodynamic Equilibrium

The state of a static, ideally conducting plasma is described by the balance of forces, where the [plasma pressure gradient](@entry_id:1129798) is counteracted by the Lorentz force exerted by the magnetic field. This is encapsulated in the ideal MHD force balance equation:
$$
\nabla p = \mathbf{J} \times \mathbf{B}
$$
Here, $p$ is the scalar plasma pressure, $\mathbf{J}$ is the electric current density, and $\mathbf{B}$ is the magnetic field. This equation is solved in conjunction with the magnetostatic Maxwell's equations: Ampère's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}$, and the [solenoidal constraint](@entry_id:755035), $\nabla \cdot \mathbf{B} = 0$, where $\mu_0$ is the [vacuum permeability](@entry_id:186031).

A direct and crucial consequence of the [force balance](@entry_id:267186) equation is that pressure must be constant along magnetic field lines. This can be seen by taking the dot product of the equation with $\mathbf{B}$:
$$
\mathbf{B} \cdot \nabla p = \mathbf{B} \cdot (\mathbf{J} \times \mathbf{B}) = 0
$$
The right-hand side vanishes because the vector $\mathbf{J} \times \mathbf{B}$ is, by definition, orthogonal to $\mathbf{B}$. The result, $\mathbf{B} \cdot \nabla p = 0$, implies that the pressure gradient is everywhere perpendicular to the magnetic field. In magnetically [confined plasmas](@entry_id:1122875), the field lines are assumed to trace out nested surfaces, known as **[magnetic flux surfaces](@entry_id:751623)**. Because pressure is constant along every field line on such a surface, it must be constant over the entire surface. If we label these surfaces with a coordinate $\psi$, then pressure can be expressed as a single-variable function, $p = p(\psi)$. This is the **flux function** property of pressure, a cornerstone of equilibrium theory  .

In systems with continuous toroidal symmetry (axisymmetry), such as an ideal tokamak, we can derive a similar property for the toroidal magnetic field. In a [cylindrical coordinate system](@entry_id:266798) $(R, \phi, Z)$, axisymmetry implies that $\partial/\partial\phi = 0$ for all scalar quantities. The toroidal component of the [force balance](@entry_id:267186) equation is $(\mathbf{J} \times \mathbf{B})_\phi = J_R B_Z - J_Z B_R = 0$. This shows that the poloidal current $\mathbf{J}_p$ is parallel to the [poloidal magnetic field](@entry_id:753563) $\mathbf{B}_p$. Combining this with the poloidal components of Ampère's law leads to the conclusion that the quantity $F \equiv R B_\phi$ is also constant along magnetic field lines: $\mathbf{B} \cdot \nabla F = 0$. Consequently, like pressure, $F$ is also a flux function, $F = F(\psi)$ .

### The Grad-Shafranov Equation: A Framework for Axisymmetric Equilibrium

The existence of the flux functions $p(\psi)$ and $F(\psi)$ in an axisymmetric system allows for a remarkable simplification of the 3D vector equilibrium problem into a single 2D scalar equation. The [poloidal magnetic field](@entry_id:753563) can be expressed in terms of the [poloidal flux](@entry_id:753562) function $\psi(R,Z)$ as $\mathbf{B}_p = \frac{1}{R} \nabla \psi \times \hat{\mathbf{e}}_\phi$. Substituting this, along with the definitions of the flux functions, into the governing MHD equations yields the celebrated **Grad–Shafranov equation (GSE)**:
$$
\Delta^* \psi = - \mu_0 R^2 \frac{dp}{d\psi} - F \frac{dF}{d\psi}
$$
where $\Delta^* \equiv R \frac{\partial}{\partial R}(\frac{1}{R}\frac{\partial}{\partial R}) + \frac{\partial^2}{\partial Z^2}$ is the Grad-Shafranov operator.

This is a non-linear, second-order, elliptic partial differential equation for the poloidal flux $\psi(R,Z)$. The right-hand side represents the toroidal plasma current density, $J_\phi$, which acts as the source for the poloidal magnetic field. The term involving $p'(\psi) = dp/d\psi$ arises from plasma pressure and is known as the [diamagnetic current](@entry_id:201627) source. The term involving $F'(\psi) = dF/d\psi$ arises from poloidal currents that modify the toroidal field and is known as the paramagnetic or [diamagnetic current](@entry_id:201627) source, depending on its sign. In a vacuum region where $p=0$ and $\mathbf{J}=0$, both $p'(\psi)$ and $F'(\psi)$ are zero, and the toroidal field simply follows the characteristic $B_\phi \propto 1/R$ decay . The reduction of the MHD equilibrium problem to this 2D scalar PDE is a profound simplification compared to non-axisymmetric devices like stellarators, where one must solve the full 3D vector force-balance equations, a problem that scales computationally as $\mathcal{O}(N^3)$ versus $\mathcal{O}(N^2)$ for the 2D GSE, where $N$ is the resolution in each dimension .

### Fixed-Boundary vs. Free-Boundary Equilibria: Defining the Problem

To solve the Grad-Shafranov equation, one must specify boundary conditions. The nature of these conditions gives rise to two fundamentally different classes of equilibrium problems.

A **fixed-boundary equilibrium** problem is one in which the plasma's shape is prescribed beforehand . Computationally, this is achieved by defining a domain $\Omega$ in the $(R,Z)$ plane whose boundary, $\partial\Omega$, corresponds to the desired plasma shape. The GSE is then solved inside this domain subject to a Dirichlet boundary condition, $\psi|_{\partial\Omega} = \psi_b$, which forces the boundary to be a flux surface. This surface is typically designated as the **Last Closed Flux Surface (LCFS)**. In this formulation, the problem is to find the internal plasma state (i.e., the profile of $\psi(R,Z)$ inside $\Omega$) that is consistent with the prescribed shape and the chosen flux functions $p(\psi)$ and $F(\psi)$. This approach is computationally convenient and useful for theoretical studies, but it decouples the plasma from the external coils that are physically responsible for its shaping and positioning.

In contrast, a **free-boundary equilibrium** problem does not prescribe the plasma boundary. Instead, the boundary's shape and location are unknown and must be determined as part of the solution  . The inputs to a [free-boundary problem](@entry_id:636836) are the external coil geometry and the currents they carry, along with the plasma profile functions $p(\psi)$ and $F(\psi)$. The solver must then find a self-consistent solution for the magnetic field and plasma state in a domain that includes both the plasma and the surrounding vacuum region. The plasma boundary emerges naturally from this solution as the LCFS. This formulation is physically realistic and essential for the design and operational analysis of fusion devices, as it directly models the interaction between the plasma and the engineering system that confines it.

### The Mechanism of Plasma-Coil Coupling

The core of the [free-boundary problem](@entry_id:636836) lies in the intricate, non-linear coupling between the plasma and the external magnetic field coils. This coupling arises from the principle of superposition and the enforcement of force balance.

The total magnetic field $\mathbf{B}$, and consequently the total [poloidal flux](@entry_id:753562) $\psi$, can be expressed as a linear superposition of the contribution from the plasma currents, $\mathbf{B}_\text{pl}$ ($\psi_\text{pl}$), and the contribution from the external coils, $\mathbf{B}_\text{coil}$ ($\psi_\text{coil}$ or $\psi_\text{vac}$):
$$
\psi(R,Z) = \psi_\text{pl}(R,Z) + \psi_\text{vac}(R,Z)
$$
This superposition forms a self-consistent feedback loop :
1.  The external coils, with known geometry and currents, produce a vacuum magnetic field described by $\psi_\text{vac}$.
2.  The plasma exists within the *total* field, $\psi$. To maintain equilibrium, its internal currents $\mathbf{J}$ must adjust to satisfy the [force balance](@entry_id:267186) condition $\nabla p = \mathbf{J} \times \mathbf{B}$.
3.  These plasma currents, which depend on the plasma profiles $p(\psi)$ and $F(\psi)$, in turn act as the source for the plasma's self-field, $\psi_\text{pl}$.
4.  The plasma field $\psi_\text{pl}$ modifies the total field $\psi$, which alters the shape of the flux surfaces. This change in shape and position requires a further readjustment of the plasma currents to maintain [force balance](@entry_id:267186).

This process continues until a self-consistent state is reached where the plasma shape, position, and internal currents are in equilibrium with the total magnetic field they collectively produce. Any change in the external coil currents alters $\psi_\text{vac}$, which perturbs the equilibrium and causes the plasma boundary and internal structure to readjust, demonstrating the intrinsic coupling between the coil system and the plasma shape.

### Computational Methods for Free-Boundary Problems

Solving the free-boundary Grad-Shafranov problem requires a numerical strategy that can handle the non-linear coupling and the unknown boundary. A common and effective approach involves solving for the plasma's contribution to the flux within a large computational domain that encompasses the vacuum region around the plasma.

#### Formulation for Numerical Solvers

The standard method reformulates the problem to solve specifically for the plasma-generated flux, $\psi_\text{pl}$ . The computational domain $\Omega$ extends from the device's central axis to an outer computational boundary, $\partial\Omega_\text{ext}$, often coinciding with the vacuum vessel wall.

1.  **Decomposition and Pre-calculation:** The total flux is decomposed as $\psi = \psi_\text{pl} + \psi_\text{vac}$. Since the external coil currents and positions are known, the vacuum flux $\psi_\text{vac}$ can be pre-computed throughout the domain $\Omega$ using the Biot-Savart law or by employing a Green's function (or [response matrix](@entry_id:754302)) that provides a linear map from the coil currents to the flux at any point in the domain . Inside $\Omega$, where there are no coil windings, $\psi_\text{vac}$ is source-free and satisfies the [homogeneous equation](@entry_id:171435) $\Delta^* \psi_\text{vac} = 0$.

2.  **Governing Equation and Boundary Condition:** The GSE is written for the total flux $\psi$, but since $\Delta^*$ is a linear operator, we have $\Delta^* \psi = \Delta^* (\psi_\text{pl} + \psi_\text{vac}) = \Delta^* \psi_\text{pl}$. The equation to be solved for $\psi_\text{pl}$ becomes:
    $$
    \Delta^* \psi_\text{pl} = - \mu_0 R^2 \frac{dp(\psi)}{d\psi} - F(\psi) \frac{dF(\psi)}{d\psi}
    $$
    Crucially, the source terms on the right-hand side depend on the *total* flux, $\psi = \psi_\text{pl} + \psi_\text{vac}$, which embeds the [plasma-coil coupling](@entry_id:1129761) directly into the equation. A simple and effective boundary condition is imposed on the outer boundary $\partial\Omega_\text{ext}$: a homogeneous Dirichlet condition for the plasma flux, $\psi_\text{pl}|_{\partial\Omega_\text{ext}} = 0$. This physically represents the assumption that the plasma's self-field decays to zero far from the plasma. The total flux on this boundary is then simply the pre-calculated vacuum flux: $\psi|_{\partial\Omega_\text{ext}} = \psi_\text{vac}|_{\partial\Omega_\text{ext}}$ .

This formulation results in a non-linear boundary-value problem for $\psi_\text{pl}$, which is typically solved iteratively using methods like the Finite Element Method (FEM) for spatial discretization combined with a Newton-Raphson scheme to handle the non-linearity .

#### Identification of the Plasma Boundary

Since the plasma boundary is an output of the calculation, a robust method is needed to identify it from the final solution for $\psi(R,Z)$. The physical boundary is the Last Closed Flux Surface (LCFS), which separates the region of closed, [nested flux surfaces](@entry_id:752411) from the region of open field lines that intersect material surfaces (like the wall or a divertor).

1.  **Locating X-Points:** For diverted or limited plasmas, the LCFS is a **separatrix**—a special flux surface that passes through one or more **X-points**. An X-point is a [stagnation point](@entry_id:266621) of the poloidal magnetic field, corresponding to a saddle point of the flux function $\psi$. Computationally, X-points are found by searching for locations where the gradient of the flux vanishes, $\nabla\psi = \mathbf{0}$. To confirm a [stationary point](@entry_id:164360) is a saddle, one must inspect the Hessian matrix of $\psi$; its eigenvalues must be real and have opposite signs .

2.  **Rigorous Separatrix Tracing:** Once an X-point is located, its corresponding flux value, $\psi_X$, defines the separatrix contour. However, the most rigorous method for identifying the LCFS is to perform magnetic field line tracing. By definition, field lines lie on flux surfaces. One can trace the full 3D trajectory of field lines, $\mathrm{d}\mathbf{x}/\mathrm{d}s = \mathbf{B}(\mathbf{x})$, starting at various points near the candidate [separatrix](@entry_id:175112). Trajectories starting just inside the LCFS will remain confined, returning to their initial poloidal position after one or more toroidal transits. Trajectories starting just outside will be "open," eventually terminating on a material boundary. The LCFS is precisely the surface that separates these two topological behaviors, a definition that can be robustly implemented in modern equilibrium solvers .