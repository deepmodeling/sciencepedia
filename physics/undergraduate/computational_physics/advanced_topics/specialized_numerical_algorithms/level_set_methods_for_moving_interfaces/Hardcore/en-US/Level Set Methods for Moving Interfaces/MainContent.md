## Introduction
From the coalescence of liquid droplets to the propagation of a crack in a solid, moving and deforming interfaces are at the heart of countless phenomena in science and engineering. Describing and computing the evolution of these boundaries, however, presents a significant challenge, especially when they undergo complex topological changes such as merging, splitting, or forming sharp corners. While explicit tracking methods that represent the interface with a series of connected points can be intuitive, they become algorithmically complex and fragile when topology changes.

The level set method offers an elegant and powerful alternative. Instead of tracking the interface directly, it embeds the boundary as the zero-level set of a higher-dimensional function defined over the entire computational domain. As this function evolves according to a partial differential equation, its zero contour moves and deforms, capable of handling topological changes automatically and robustly. This article provides a foundational guide to this indispensable computational technique.

You will begin by learning the core concepts in **Principles and Mechanisms**, exploring the implicit representation, the signed distance function, and the derivation of the fundamental level set evolution equation. We will then dive into the essential numerical algorithms needed to solve this equation, including discretization schemes, stability conditions, and the critical reinitialization step. In **Applications and Interdisciplinary Connections**, you will see the method's versatility in action as we survey its use in diverse fields such as fluid dynamics, materials science, image processing, and robotics. Finally, the **Hands-On Practices** section provides guided exercises to translate theory into practice by building your own level set solvers to simulate phenomena like cell division and droplet coalescence.

## Principles and Mechanisms

The level set method provides a powerful and versatile framework for computing the motion of interfaces. Its elegance stems from embedding the interface, a geometric object, as a particular feature of a scalar field defined over the entire computational domain. This chapter delves into the foundational principles of this implicit representation, the mathematical equations governing its dynamics, the numerical algorithms required for its solution, and the key mechanisms that ensure accuracy and stability.

### Implicit Representation and the Signed Distance Function

The core principle of the level set method is the representation of an interface $\Gamma(t)$ in a $d$-dimensional domain $\Omega$ as the zero-isocontour of a $(d+1)$-dimensional scalar field, $\phi(\mathbf{x}, t)$. For a two-dimensional domain, the moving curve $\Gamma(t)$ is defined by the set of points where the surface $\phi(x,y,t)$ intersects the zero plane:
$$
\Gamma(t) = \{ \mathbf{x} \in \Omega \mid \phi(\mathbf{x}, t) = 0 \}
$$
By convention, the field $\phi$ is defined to be negative in the region enclosed by the interface ("inside") and positive in the exterior region ("outside"). This implicit representation is the source of the method's greatest strength: the ability to handle complex topological changes. As the field $\phi$ evolves smoothly in time, its zero-isocontour can merge, split, and develop sharp corners without any special algorithmic intervention. For instance, the inward shrinking of a complex, self-intersecting shape like a Lissajous curve can be simulated, where the interface naturally breaks apart and vanishes without the need for explicit tracking of interface connectivity [@problem_id:2408424]. This stands in stark contrast to explicit Lagrangian methods, which represent the interface with a set of marker points and require sophisticated and often fragile remeshing logic to manage topological events [@problem_id:2567745].

While any function whose zero-level set corresponds to the interface can serve as a level set function, the most convenient and numerically advantageous choice is the **signed distance function (SDF)**. A function $\phi$ is a signed distance function if it satisfies two properties:

1.  The value $|\phi(\mathbf{x}, t)|$ is equal to the shortest Euclidean distance from the point $\mathbf{x}$ to the interface $\Gamma(t)$.
2.  The sign of $\phi(\mathbf{x}, t)$ indicates whether $\mathbf{x}$ is inside ($<0$) or outside ($>0$) the interface.

A direct mathematical consequence of the first property is that a signed distance function satisfies the **Eikonal equation**:
$$
|\nabla \phi| = 1
$$
almost everywhere. This property is immensely useful. It implies that the gradient of the level set function, $\nabla \phi$, is a unit vector that points normal to the level sets. Thus, for an interface $\Gamma$, the outward-pointing unit normal vector $\mathbf{n}$ is given simply by:
$$
\mathbf{n} = \frac{\nabla \phi}{|\nabla \phi|} = \nabla \phi \quad (\text{if } |\nabla \phi|=1)
$$
The importance of the *sign* in the signed distance function cannot be overstated. An unsigned distance function, $\psi(\mathbf{x}) = |\phi(\mathbf{x})|$, while correctly identifying the location of the interface (where $\psi=0$), discards the crucial information of "inside" versus "outside." This loss is catastrophic for many applications. For example, in the extended finite element method (XFEM) for fracture mechanics, a displacement jump across a crack is modeled using a Heaviside enrichment function, $H(\phi)$. If an unsigned function $\psi$ were used, $H(\psi)$ would be equal to $1$ on both sides of the crack, making it impossible to represent a displacement jump. Furthermore, the gradient of $\psi$ points away from the interface on both sides, making it impossible to define a consistent normal vector, which is essential for applying physical laws like pressure or traction on the crack faces [@problem_id:2390825].

### The Dynamics of an Interface: The Level Set Equation

The evolution of the interface is governed by a velocity field $\mathbf{v}$. A point $\mathbf{x}(t)$ that remains on the interface $\Gamma(t)$ must satisfy $\phi(\mathbf{x}(t), t) = 0$ for all time. Taking the material derivative (the total derivative with respect to time) gives:
$$
\frac{D\phi}{Dt} = \frac{\partial \phi}{\partial t} + \nabla \phi \cdot \frac{d\mathbf{x}}{dt} = 0
$$
Recognizing that $\frac{d\mathbf{x}}{dt} = \mathbf{v}$ is the velocity of the point on the interface, we arrive at the general advection equation for the level set field:
$$
\frac{\partial \phi}{\partial t} + \mathbf{v} \cdot \nabla \phi = 0
$$
This equation states that the level set function is materially transported with the velocity field [@problem_id:2567687].

In many physical problems, the velocity of the interface is prescribed only in its normal direction, $F_n$. The tangential component of the velocity only affects the parameterization of the interface, not its geometric shape. The velocity vector can thus be written as $\mathbf{v} = F_n \mathbf{n}$. Substituting the expression for the normal vector, $\mathbf{n} = \nabla\phi/|\nabla\phi|$, into the advection equation yields:
$$
\frac{\partial \phi}{\partial t} + \left( F_n \frac{\nabla \phi}{|\nabla \phi|} \right) \cdot \nabla \phi = 0
$$
$$
\frac{\partial \phi}{\partial t} + F_n \frac{\nabla \phi \cdot \nabla \phi}{|\nabla \phi|} = \frac{\partial \phi}{\partial t} + F_n \frac{|\nabla \phi|^2}{|\nabla \phi|} = 0
$$
This simplifies to the canonical **Hamilton-Jacobi form of the level set equation**:
$$
\frac{\partial \phi}{\partial t} + F_n |\nabla \phi| = 0
$$
This first-order, non-linear hyperbolic partial differential equation is the fundamental law governing the evolution of the level set function. The normal speed $F_n$ can be a constant, or it can depend on local geometric properties like curvature ($\kappa = \nabla \cdot \mathbf{n}$), or on external physics.

### Numerical Discretization and Solution

Solving the level set equation numerically presents several challenges. The process involves discretizing the domain, representing $\phi$ on a grid, and approximating the time and space derivatives.

#### Interface Localization and Representation

On a discrete grid, such as a triangular mesh used in the finite element method, the interface is not explicitly tracked. Instead, its location is inferred from the values of $\phi$ at the grid nodes. An element is identified as being "cut" by the interface if the nodal values of $\phi$ are not all of the same sign. Within a cut element, the interface can be reconstructed. For a linear triangular element with nodal values $\phi_1, \phi_2, \phi_3$, the function $\phi$ is assumed to vary linearly. This implies the zero-level set within the element is a straight line segment. The endpoints of this segment are found by identifying the edges with a sign change and using linear interpolation to find the exact intersection point. For an edge connecting nodes $i$ and $j$ with values $\phi_i$ and $\phi_j$, the intersection occurs at a fractional distance $t^\star = \phi_i / (\phi_i - \phi_j)$ from node $i$ [@problem_id:2573418]. This "marching triangles" (or "marching squares" for quadrilaterals) approach allows for visualization and is the basis for numerical integration over the distinct material regions.

#### Spatial Discretization and Numerical Diffusion

The spatial derivative term $|\nabla \phi|$ (or $\mathbf{v} \cdot \nabla \phi$) is non-linear and hyperbolic, requiring special care. Simple centered finite difference schemes are unstable for this type of equation. The standard approach is to use an **upwind scheme**, which discretizes the spatial derivatives using a stencil that is biased in the direction from which information is propagating.

A **first-order upwind scheme**, such as the Godunov scheme, provides the necessary stability. It is robust and guarantees that no new oscillations are created. However, its major drawback is a large amount of **numerical diffusion**. This can be understood by examining the scheme's modified equation, which reveals that the scheme is effectively solving the original PDE plus an artificial diffusion term with a coefficient proportional to the grid spacing $\Delta x$ [@problem_id:2408390]. This diffusion has the undesirable effect of smearing sharp features. In the context of level set methods, it causes the profile of $\phi$ to broaden, losing the sharp signed-distance property, and can visibly distort the interface, especially in flows with high curvature or shear, such as the classic test case of a solid body rotating in a swirling vortex [@problem_id:2408390].

To mitigate numerical diffusion, **high-order schemes** are necessary. A popular class of schemes is the **Weighted Essentially Non-Oscillatory (WENO)** family. A fifth-order WENO scheme, for instance, achieves high accuracy in smooth regions of the flow while adaptively reducing to a lower-order, robust scheme near sharp gradients to avoid spurious oscillations. For a fixed grid, a WENO scheme preserves the sharpness of the interface far more accurately than a first-order upwind scheme, resulting in significantly lower error in the interface position and conservation of geometric properties like area [@problem_id:2408390, @problem_id:2408429].

In a finite element context, the analogue of upwinding is provided by stabilized methods, such as the **Streamline-Upwind/Petrov-Galerkin (SUPG)** method. This method modifies the standard Galerkin formulation by adding a stabilization term that acts along the streamline (velocity) direction. This term also introduces artificial diffusion, which is necessary for stability but can degrade the signed-distance property over time [@problem_id:2567687, @problem_id:2573442].

#### Stability and the Courant-Friedrichs-Lewy (CFL) Condition

When using an explicit time-stepping scheme (e.g., Forward Euler or a Runge-Kutta method), the time step $\Delta t$ is not independent of the grid spacing $\Delta x$. The **Courant-Friedrichs-Lewy (CFL) condition** dictates the maximum allowable time step for stability. For a first-order hyperbolic PDE, this condition requires that the numerical domain of dependence contain the physical domain of dependence. For the level set equation, the characteristic speed of information propagation is related to the interface velocity. For the Hamilton-Jacobi form, the maximum characteristic speed is $\max|F_n|$, and for the advection form, it is $\max|\mathbf{v}|$. The stability condition for a first-order upwind scheme in one dimension is:
$$
\Delta t \le \frac{\Delta x}{\max |F_n|}
$$
In two dimensions on a uniform grid ($\Delta x = \Delta y = h$), the condition becomes more restrictive:
$$
\Delta t \left( \frac{\max|F_n|}{\Delta x} + \frac{\max|F_n|}{\Delta y} \right) \le 1 \quad \implies \quad \Delta t \le \frac{h}{2 \max |F_n|}
$$
This condition depends only on the maximum magnitude of the velocity, not on its sign or its frequency content; high-frequency oscillations in the velocity field do not tighten this bound for a monotone upwind scheme [@problem_id:2408409, @problem_id:2408398]. It is also important to note that using a higher-order time integrator, such as a Strong Stability Preserving (SSP) Runge-Kutta method, does not relax this fundamental CFL limit; SSP methods are designed to preserve the stability of the underlying Forward Euler step, not to extend it [@problem_id:2408398].

### Maintaining the Signed Distance Property: Reinitialization

A critical practical issue in level set methods is that the evolution equation, $\phi_t + F_n|\nabla\phi|=0$, does not preserve the signed-distance property, $|\nabla\phi|=1$. During the evolution, the level set function can become too steep or too flat in the vicinity of the interface, leading to a loss of accuracy in the calculation of the normal and curvature, and potentially impacting stability. This degradation is caused both by non-uniform velocity fields and by the numerical diffusion inherent in the discretization scheme [@problem_id:2606563, @problem_id:2573442].

To remedy this, a **reinitialization** procedure is periodically applied. This process computationally reshapes the $\phi$ field back into a signed distance function without moving the zero-level set. A common and effective method is to solve an auxiliary PDE in a fictitious time $\tau$:
$$
\frac{\partial \phi}{\partial \tau} = S(\phi_0) (1 - |\nabla \phi|)
$$
Here, $\phi_0$ is the level set field at the beginning of the reinitialization step, and $S(\phi_0)$ is a smoothed sign function of that frozen field. Let's analyze the components of this equation [@problem_id:2606563]:

*   **Steady State**: The evolution in $\tau$ stops when $\partial \phi / \partial \tau = 0$. This occurs when $|\nabla \phi| = 1$, which is the Eikonal equation. Thus, the steady-state solution is a signed distance function.
*   **Invariance of the Interface**: The term $S(\phi_0)$ acts as a switch. On the original zero-level set, $\phi_0 = 0$, so $S(\phi_0) = 0$. This forces $\partial \phi / \partial \tau = 0$ on the interface, meaning the interface itself does not move during reinitialization. This is a crucial property; using a time-dependent sign function $S(\phi(\tau))$ instead is unstable and would cause the interface to drift unphysically [@problem_id:2573442].

In practice, reinitialization is an additional computational expense. It is not necessary to perform it at every time step. Instead, it can be triggered adaptively, for example, when a metric monitoring the deviation of $|\nabla \phi|$ from $1$ in a narrow band around the interface exceeds a certain tolerance [@problem_id:2606563]. For simple, smooth flows like a uniformly expanding circle, the accuracy of the interface position is remarkably insensitive to the reinitialization frequency, because the reinitialization procedure is explicitly designed not to move the zero contour [@problem_id:2408465]. An alternative to solving the time-dependent reinitialization equation is to directly solve the Eikonal equation $|\nabla\phi|=1$ using a highly efficient algorithm like the Fast Marching Method or Fast Sweeping Method [@problem_id:2573442].

### Applications and Advanced Considerations

The level set framework is versatile and enables the modeling of complex physics at the interface.

#### Two-Fluid Flows and Surface Tension

In simulating flows with two different fluids (e.g., air and water), the interface is sharp, but material properties like density ($\rho$) and viscosity ($\mu$) must be represented on the fixed grid. This is typically done by defining a smooth transition across the interface using a smoothed Heaviside function, $H_\epsilon(\phi)$. For example, the density at any point can be defined as:
$$
\rho(\phi) = \rho_1 + (\rho_2 - \rho_1)(1 - H_\epsilon(\phi))
$$
The parameter $\epsilon$ controls the thickness of this numerical transition layer. Since $\phi$ is an SDF, the physical thickness is approximately $2\epsilon$. The choice of $\epsilon$ involves a critical trade-off. If $\epsilon$ is chosen to be much smaller than the grid spacing $\Delta x$, the discrete gradients of the properties become very large, leading to numerical instabilities and large spurious currents. Conversely, a very large $\epsilon$ smears the interface too much, degrading accuracy and artificially damping physical phenomena like capillary waves. A robust choice, commonly used in practice, is to couple the interface thickness to the grid resolution, e.g., $\epsilon = 1.5 \Delta x$, ensuring the interface is resolved over a few grid cells [@problem_id:2408399].

Surface tension, a force that acts only on the interface, can be modeled as a continuous body force using the **Continuum Surface Force (CSF)** model. The force is distributed within the transition layer using the derivative of the smoothed Heaviside function, which acts as a regularized Dirac delta function, $\delta_\epsilon(\phi) = H'_\epsilon(\phi)$:
$$
\mathbf{f}_\sigma = \sigma \kappa \delta_\epsilon(\phi) \mathbf{n}
$$
Here, $\sigma$ is the surface tension coefficient and $\kappa$ is the local curvature. Provided $\delta_\epsilon(\phi)$ is properly normalized, the total force applied is independent of the thickness parameter $\epsilon$; it is merely distributed over a wider or narrower band [@problem_id:2408399].

#### Boundary Conditions

Properly handling the interaction of an interface with a domain boundary is critical. To model a solid, no-penetration wall, the component of the interface velocity normal to the wall must be zero. In the level set framework, this physical condition is enforced by applying a **homogeneous Neumann boundary condition** on the level set function, $\partial \phi / \partial \mathbf{n}_{\text{wall}} = 0$. This correctly halts the interface upon contact with the boundary. In contrast, a Dirichlet boundary condition, $\phi=0$, is generally incorrect as it artificially pins the interface to the wall for all time, regardless of the physical dynamics [@problem_id:2408443].

#### Conservation Properties

A key consideration in fluid dynamics is the conservation of quantities like mass or volume. For an incompressible flow ($\nabla \cdot \mathbf{v} = 0$), the area (in 2D) or volume (in 3D) enclosed by the interface should be exactly conserved. However, standard numerical schemes for the non-conservative level set equation ($\phi_t + \mathbf{v} \cdot \nabla \phi = 0$) do not guarantee this at the discrete level. Numerical diffusion from schemes like first-order upwind can lead to significant, unphysical area loss. High-order schemes like WENO perform much better, with area error decreasing rapidly with grid refinement, but do not provide exact conservation. For applications where strict mass conservation is paramount, specialized **conservative level set methods** must be employed, which solve a conservative advection equation for a smoothed indicator function [@problem_id:2408429].

#### Multi-Material Systems

The level set method can be extended to handle problems with multiple material interfaces, such as triple junctions where three materials meet. This is typically done by using one level set function for each material or interface. A challenge arises at intersection points, where it may be ambiguous which interface is "active" or closest to a given point. For instance, if two discrete interfaces $\phi_h^{(1)}=0$ and $\phi_h^{(2)}=0$ intersect inside an element, the rule of choosing the interface with the smaller $|\phi_h|$ value breaks down. This ambiguity must be resolved with a deterministic and consistent tie-breaking rule. A robust strategy is to introduce a small, priority-based bias to the selection rule. The magnitude of this bias must be chosen carefully to be on the order of the discretization error of the level set function itself (e.g., $O(h^{p+1})$ for a polynomial approximation of degree $p$), ensuring that the tie-breaking does not degrade the overall geometric accuracy of the method as the mesh is refined [@problem_id:2573444].