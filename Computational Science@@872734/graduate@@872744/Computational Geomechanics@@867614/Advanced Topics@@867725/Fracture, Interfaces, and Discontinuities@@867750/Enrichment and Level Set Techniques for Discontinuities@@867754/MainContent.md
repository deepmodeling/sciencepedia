## Introduction
Modeling discontinuities such as faults, fractures, and [shear bands](@entry_id:183352) is a central challenge in [computational geomechanics](@entry_id:747617). Traditional numerical methods, like the standard Finite Element Method (FEM), struggle with these features because their underlying mathematical framework assumes material continuity. Representing a growing crack or a slipping fault typically requires complex and error-prone mesh regeneration procedures that can dominate the computational cost and compromise solution accuracy. This article addresses this knowledge gap by providing a comprehensive overview of a powerful alternative: the synergistic use of enrichment and level set techniques.

By combining the geometric flexibility of the Level Set Method (LSM) for tracking interfaces with the approximation power of the eXtended Finite Element Method (XFEM), we can model complex, evolving discontinuities on a fixed mesh. This guide is structured to build a thorough understanding, from theory to practice. The first chapter, "Principles and Mechanisms," will delve into the mathematical foundations, explaining how the Partition of Unity allows for specialized [enrichment functions](@entry_id:163895) to capture displacement jumps, kinks, and singularities. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the versatility of these methods by exploring their use in modeling cohesive fracture, [strain localization](@entry_id:176973), and coupled hydro-mechanical and thermo-mechanical phenomena. Finally, the "Hands-On Practices" section provides targeted problems to solidify the core concepts and implementation details. This structured approach will equip you with the knowledge to leverage these advanced techniques for realistic simulations in geomechanics.

## Principles and Mechanisms

The modeling of discontinuities in [geomechanics](@entry_id:175967) requires specialized numerical techniques that can represent complex, evolving geometries and the associated non-smooth field variables without the need for continuous remeshing. This chapter elucidates the fundamental principles and mechanisms underpinning two powerful and synergistic technologies: the Level Set Method (LSM) for geometric representation and the Partition of Unity Method (PUM), particularly in the form of the eXtended Finite Element Method (XFEM), for approximating discontinuous fields. We will explore the theoretical basis of these methods, the specific enrichment strategies for various types of discontinuities, and the key implementation challenges that must be addressed for a robust computational framework.

### Characterizing and Representing Discontinuities

Before a discontinuity can be modeled, it must be precisely characterized both kinematically and geometrically. The former dictates the type of mathematical function needed to describe the field behavior, while the latter provides the spatial map of where this behavior occurs.

#### Kinematic Classification: Strong and Weak Discontinuities

In [continuum mechanics](@entry_id:155125), the nature of a discontinuity is classified by the regularity of the [displacement field](@entry_id:141476), $\boldsymbol{u}$, across an interface, $\Gamma$. We define the jump of a field $f$ across $\Gamma$ at a point $\boldsymbol{x}_\Gamma$ as $[\![f]\!](\boldsymbol{x}_\Gamma) = f^+(\boldsymbol{x}_\Gamma) - f^-(\boldsymbol{x}_\Gamma)$, where $f^+$ and $f^-$ are the limits of the field as $\boldsymbol{x}_\Gamma$ is approached from the positive and negative sides of the interface, respectively.

A **[strong discontinuity](@entry_id:166883)** is characterized by a jump in the displacement field itself. This represents a physical separation or slip, such as occurs across the faces of a crack or a fault.
$$
[\![\boldsymbol{u}]\!] \neq \boldsymbol{0}
$$
In this case, the displacement field is discontinuous. From the perspective of distributional calculus, the gradient of such a field, $\nabla \boldsymbol{u}$, contains a singularity. Specifically, the distributional gradient includes a singular part concentrated on the [surface of discontinuity](@entry_id:180188), given by the term $[\![\boldsymbol{u}]\!] \otimes \boldsymbol{n} \, \delta_\Gamma$, where $\boldsymbol{n}$ is the unit normal to the interface and $\delta_\Gamma$ is the Dirac delta measure supported on $\Gamma$. This term represents an infinite strain localized on a surface of zero thickness.

A **[weak discontinuity](@entry_id:164525)**, by contrast, describes a situation where the material remains macroscopically connected, but its deformation is sharply localized. This manifests as a continuous displacement field, but a discontinuous [displacement gradient](@entry_id:165352) (and thus, discontinuous strain and stress). This is characteristic of phenomena such as [shear bands](@entry_id:183352) in soils and rocks.
$$
[\![\boldsymbol{u}]\!] = \boldsymbol{0}, \quad \text{but} \quad [\![\nabla \boldsymbol{u}]\!] \neq \boldsymbol{0}
$$
Since the [displacement field](@entry_id:141476) is continuous, its distributional gradient does not contain a Dirac-delta-type singularity. The [gradient field](@entry_id:275893) $\nabla \boldsymbol{u}$ is a function that is itself discontinuous across $\Gamma$, representing a "kink" in the displacement field. These distinct kinematic classifications demand different modeling strategies, as we will see in the discussion of [enrichment functions](@entry_id:163895) [@problem_id:3523064].

#### Geometric Representation: The Level Set Method

The Level Set Method (LSM) provides a powerful and flexible framework for implicitly representing and evolving complex interfaces. Instead of explicitly tracking points on the discontinuity $\Gamma$, we represent it as the zero contour of a higher-dimensional scalar function, $\phi(\boldsymbol{x}, t)$, called the **level set function**.
$$
\Gamma(t) = \{\boldsymbol{x} \in \Omega \mid \phi(\boldsymbol{x},t)=0\}
$$
Typically, $\phi$ is defined as the signed distance to the interface, where the sign distinguishes the two sides: $\phi(\boldsymbol{x},t) \gt 0$ on one side and $\phi(\boldsymbol{x},t) \lt 0$ on the other. This representation has several advantages. First, [topological changes](@entry_id:136654) like the merging of two cracks or the [nucleation](@entry_id:140577) of a new one are handled naturally. Second, important geometric properties are readily computed from $\phi$. The [unit normal vector](@entry_id:178851) $\boldsymbol{n}$ to the interface, crucial for defining orientations, is given by the normalized gradient of the [level set](@entry_id:637056) function:
$$
\boldsymbol{n} = \frac{\nabla \phi}{|\nabla \phi|}
$$
Within a finite element context, the level set field is discretized using the same shape functions as other fields. For instance, in an [isoparametric element](@entry_id:750861), $\phi_h(\boldsymbol{x}) = \sum_i N_i(\boldsymbol{x}) \phi_i$. The gradient $\nabla \phi$ at any point inside the element, such as a quadrature point, is then computed using the [chain rule](@entry_id:147422), involving the Jacobian of the mapping from the parent element to the physical element. This allows for the precise calculation of the interface normal at any location required by the formulation [@problem_id:3523096].

The evolution of the interface is governed by advecting the level set function with a velocity field $\boldsymbol{v}(\boldsymbol{x}, t)$. The principle that points on a given level set contour remain on that contour as they move leads to the **Level Set Equation**, a first-order hyperbolic partial differential equation:
$$
\frac{\partial \phi}{\partial t} + \boldsymbol{v} \cdot \nabla \phi = 0
$$
This equation describes the evolution of the entire field $\phi$ in an Eulerian frame. The motion of the interface depends only on the normal component of the velocity, $v_n = \boldsymbol{v} \cdot \boldsymbol{n}$. Substituting $\boldsymbol{n} = \nabla\phi / |\nabla\phi|$ yields the Hamilton-Jacobi form of the equation, which is often used in practice:
$$
\frac{\partial \phi}{\partial t} + v_n |\nabla \phi| = 0
$$
When this equation is discretized in time with an explicit scheme, numerical stability must be ensured. For a first-order upwind finite difference scheme on a Cartesian grid with spacing $\Delta x_i$ in each direction, the Courant-Friedrichs-Lewy (CFL) condition imposes a limit on the time step $\Delta t$. For an unsplit scheme in $d$ dimensions, this condition is:
$$
\Delta t \left( \sum_{i=1}^d \frac{|v_i|}{\Delta x_i} \right) \le 1
$$
where $v_i$ are the components of the velocity vector $\boldsymbol{v}$. This ensures that information does not propagate more than one grid cell per time step, which is necessary for the stability of the numerical scheme [@problem_id:3523070].

### The Principle of Partition of Unity Enrichment

The conventional Finite Element Method (FEM) struggles to model discontinuities because its polynomial basis functions are inherently smooth within elements. The eXtended Finite Element Method (XFEM) overcomes this by enriching the standard approximation space with additional functions that are tailored to the behavior near the discontinuity. This is built upon the **Partition of Unity (POU)** property of standard FE shape functions, $\{N_i(\boldsymbol{x})\}$. This property states that at any point $\boldsymbol{x}$ in the domain, the sum of all shape functions with support over that point is equal to one.
$$
\sum_{i=1}^{n_{\text{nodes}}} N_i(\boldsymbol{x}) = 1 \quad \forall \boldsymbol{x} \in \Omega
$$
The enriched approximation for a field $u(\boldsymbol{x})$ is then constructed as:
$$
u_h(\boldsymbol{x}) = \underbrace{\sum_{i \in \mathcal{I}} N_i(\boldsymbol{x}) u_i}_{\text{Standard FE Part}} + \underbrace{\sum_{j \in \mathcal{J}} N_j(\boldsymbol{x}) \Psi(\boldsymbol{x}) a_j}_{\text{Enrichment Part}}
$$
Here, $\mathcal{I}$ is the set of all nodes, and $\mathcal{J} \subseteq \mathcal{I}$ is the subset of nodes whose shape function supports are intersected by the discontinuity. The function $\Psi(\boldsymbol{x})$ is the **enrichment function**, and $a_j$ are the additional degrees of freedom associated with the enrichment.

The POU property is what makes this framework powerful. It guarantees that the approximation space can reproduce not only linear fields (if the shape functions are linear) but also the enrichment function $\Psi(\boldsymbol{x})$ itself. This is because any function $\Psi(\boldsymbol{x})$ can be written as $\Psi(\boldsymbol{x}) \cdot 1 = \Psi(\boldsymbol{x}) \sum_i N_i(\boldsymbol{x}) = \sum_i N_i(\boldsymbol{x}) \Psi(\boldsymbol{x})$. By selecting the appropriate nodal coefficients, the enriched basis can thus represent $\Psi(\boldsymbol{x})$ exactly. Consequently, adding the enrichment term $N_j(\boldsymbol{x}) \Psi(\boldsymbol{x})$ expands the approximation space without sacrificing the original **completeness** of the standard FE space. If the standard space can reproduce polynomials up to degree $m$, the enriched space retains this ability because the standard approximation is a subset of the enriched one (obtained by setting all $a_j=0$) [@problem_id:3523069].

### Enrichment Strategies

The choice of the enrichment function $\Psi(\boldsymbol{x})$ is dictated by the physics of the discontinuity being modeled.

#### Strong Discontinuities: Heaviside Enrichment

To model a [strong discontinuity](@entry_id:166883), or displacement jump, we need an enrichment function that is itself discontinuous. The natural choice, built from the level set function $\phi(\boldsymbol{x})$, is the generalized **Heaviside function**, often defined as $\text{sign}(\phi(\boldsymbol{x}))$:
$$
H_\Gamma(\boldsymbol{x}) = \text{sign}(\phi(\boldsymbol{x})) = \begin{cases} +1  \text{if } \phi(\boldsymbol{x}) \gt 0 \\ -1  \text{if } \phi(\boldsymbol{x}) \lt 0 \end{cases}
$$
The enriched displacement approximation directly incorporates this jump. The magnitude of the displacement jump across the interface, $\llbracket \boldsymbol{u}_h \rrbracket$, is then directly controlled by the enriched nodal degrees of freedom $\boldsymbol{a}_j$. A common practical modification is to use a shifted Heaviside function, such as $\Psi(\boldsymbol{x}) = H_\Gamma(\boldsymbol{x}) - H_\Gamma(\boldsymbol{x}_j)$, which ensures that the standard nodal parameter $\boldsymbol{u}_j$ retains its meaning as the physical displacement at node $\boldsymbol{x}_j$.

When this enriched approximation is used in the Principle of Virtual Work, the [distributional derivative](@entry_id:271061) of the Heaviside function, which is a Dirac [delta function](@entry_id:273429) on the interface $\Gamma$, gives rise to an explicit interface integral. This allows for the direct incorporation of interface laws, such as cohesive traction-separation models or contact conditions, into the [weak form](@entry_id:137295) of the [equilibrium equations](@entry_id:172166) [@problem_id:3523109].

#### Weak Discontinuities: Ramp Enrichment

For weak discontinuities, where displacement is continuous but strain is not, a different enrichment is needed. The enrichment function $\Psi(\boldsymbol{x})$ must be continuous but have a discontinuous gradient (a "kink"). A suitable choice is a **[ramp function](@entry_id:273156)** constructed from the [level set](@entry_id:637056), such as $\Psi(\boldsymbol{x}) = |\phi(\boldsymbol{x})|$. The gradient of this function is $\nabla \Psi(\boldsymbol{x}) = \text{sign}(\phi(\boldsymbol{x})) \nabla \phi(\boldsymbol{x})$, which jumps across the interface $\Gamma$ where $\phi=0$.

This approach is essential for modeling [strain localization](@entry_id:176973) bands. In a standard Cauchy continuum, such bands tend to collapse to zero thickness, a behavior that leads to [pathological mesh dependency](@entry_id:184469) in numerical simulations. Modeling them with [weak discontinuity](@entry_id:164525) enrichment within a generalized continuum framework (such as Cosserat or [strain gradient plasticity](@entry_id:189213) theories) provides a regularization. These theories include an **internal length scale** that introduces an energetic penalty for high strain gradients, ensuring the localization band maintains a finite, physically realistic thickness and restoring mesh objectivity to the simulation [@problem_id:3523071].

#### Singularities: Crack-Tip Enrichment

Linear Elastic Fracture Mechanics (LEFM) predicts that the stress field near a crack tip is singular, behaving like $r^{-1/2}$, where $r$ is the distance from the tip. Correspondingly, the [displacement field](@entry_id:141476) behaves like $r^{1/2}$. To capture this non-polynomial behavior, special **crack-tip [enrichment functions](@entry_id:163895)** are used. These are the leading-order terms of the Williams [eigenfunction expansion](@entry_id:151460) for the displacement field around a crack tip. For a 2D crack in an isotropic material, the basis for this enrichment is spanned by four functions:
$$
\left\{ \sqrt{r}\sin\left(\frac{\theta}{2}\right), \sqrt{r}\cos\left(\frac{\theta}{2}\right), \sqrt{r}\sin(\theta)\sin\left(\frac{\theta}{2}\right), \sqrt{r}\sin(\theta)\cos\left(\frac{\theta}{2}\right) \right\}
$$
Here, $(r, \theta)$ are local polar coordinates centered at the [crack tip](@entry_id:182807). In an XFEM implementation, these coordinates can be constructed using two level set functions: one ($\phi$) representing the signed distance to the crack surface and another ($\psi$) representing the signed distance along the crack to its tip. The [polar coordinates](@entry_id:159425) are then computed at each quadrature point as $r=\sqrt{\phi^2+\psi^2}$ and $\theta=\operatorname{atan2}(\phi, \psi)$. This enrichment is typically applied only to nodes of elements that contain the crack tip, while the Heaviside enrichment is used for elements along the crack faces away from the tip [@problem_id:3523075].

### Implementation: Challenges and Solutions

While elegant in theory, the practical implementation of enrichment methods presents several critical challenges that must be addressed to ensure accuracy and robustness.

#### Numerical Integration for Discontinuous Integrands

A major challenge arises in the computation of element stiffness matrices and force vectors. The integrands in these computations involve products of [shape functions](@entry_id:141015), their derivatives, and the [enrichment functions](@entry_id:163895). For an element cut by a discontinuity and enriched with a Heaviside function, the integrand will be [piecewise polynomial](@entry_id:144637), not polynomial over the whole element. Standard **Gaussian quadrature** is designed for smooth, polynomial integrands and will fail to compute these integrals exactly. For example, applying a 2-point Gauss rule to the integral of the simple [discontinuous function](@entry_id:143848) $f(x)=H(x)x$ over $[-1, 1]$ yields $2/\sqrt{3}$, whereas the exact answer is $1$.

The correct procedure is **subcell integration**. The element is first partitioned into subcells that are aligned with the discontinuity. For example, a [quadrilateral element](@entry_id:170172) cut by a line segment is divided into two or more polygons. Within each subcell, the integrand is now a smooth polynomial. Standard Gaussian quadrature can then be applied to each subcell (often by further decomposing it into standard shapes like triangles), and the results are summed to obtain the exact integral over the element [@problem_id:3523144].

#### The Blending Element Problem

A subtle issue with the [partition of unity](@entry_id:141893) arises in elements that are not cut by the discontinuity but are adjacent to enriched elements. These are known as **blending elements**. They contain a mixture of enriched and non-enriched nodes. In these elements, the sum of the shape functions associated with only the *enriched* nodes is no longer equal to one: $\sum_{j \in J_{\text{elem}}} N_j(\boldsymbol{x}) \neq 1$.

This violates the POU property for the enrichment basis, meaning the enrichment function $\Psi(\boldsymbol{x})$ cannot be exactly reproduced by the enriched part of the approximation in that element. This can lead to a loss of accuracy and suboptimal convergence rates. For example, in a 1D blending element on $[1, 2]$ with an enriched node at $x=1$ and a standard node at $x=2$, the enriched basis consists only of $N_1(x)\Psi(x)$. It is impossible to find a single nodal coefficient $a_1$ such that $N_1(x)\Psi(x)a_1 = \Psi(x)$ for all $x \in [1,2]$, as this would require $a_1 = 1/N_1(x)$, which is not a constant. This problem requires special correction techniques, such as using ramp functions to smoothly transition the enrichment to zero, to restore the optimal properties of the method [@problem_id:3523061].

#### Conditioning of System Matrices

The introduction of [enrichment functions](@entry_id:163895) can lead to severe [ill-conditioning](@entry_id:138674) of the [global stiffness matrix](@entry_id:138630). This occurs when the enriched basis functions become nearly linearly dependent on the standard basis functions. This is a common problem when a discontinuity passes very close to a node, making the enriched shape function $N_i(\boldsymbol{x})\Psi(\boldsymbol{x})$ very similar to the standard shape function $N_i(\boldsymbol{x})$ over most of its support.

Even without considering the interaction with standard [shape functions](@entry_id:141015), the set of [enrichment functions](@entry_id:163895) themselves might be non-orthogonal and poorly conditioned. For example, a basis for modeling a jump and kink at $x=0$ on $[-1, 1]$ could include $\{1, x, \operatorname{sign}(x), |x|\}$. The **Gram matrix**, whose entries are the inner products $G_{ij} = \langle b_i, b_j \rangle$ of the basis functions, quantifies their correlation. A large condition number for this matrix indicates a poorly conditioned basis. For the example basis, the condition number is $\kappa_2(G) = (29 + 8\sqrt{13})/3 \approx 19.27$, which is far from the ideal value of 1.

One solution to this problem is to perform an **[orthogonalization](@entry_id:149208)** of the enrichment basis at the element level using a procedure like the Gram-Schmidt process. This transforms the original basis into an orthonormal one. The Gram matrix of the new basis is the identity matrix, which has a perfect condition number of 1, thereby eliminating this source of [ill-conditioning](@entry_id:138674) and improving the numerical stability of the formulation [@problem_id:3523110].

### Application: Simulating Crack Propagation

The principles and mechanisms described above can be integrated into a powerful algorithm for simulating [crack propagation](@entry_id:160116). The process is an iterative loop:

1.  **Solve for Deformation:** For the current crack geometry, defined by one or more level set functions, an XFEM analysis is performed. The mesh remains fixed, and elements are enriched with Heaviside functions (for the crack faces) and LEFM branch functions (for the crack tips). Solving the resulting system of linear equations yields the [displacement field](@entry_id:141476).

2.  **Determine Propagation Law:** The computed displacement field is post-processed to evaluate the Stress Intensity Factors ($K_I$ and $K_{II}$) at each crack tip. These values are then used in a fracture criterion. For example, the **Maximum Circumferential Stress (MCS)** criterion states that the crack will propagate in the direction $\theta_c$ that maximizes the hoop stress, which for mixed-mode loading is given by:
    $$
    \theta_c = 2\,\arctan\left[\frac{1}{4}\left(\frac{K_I}{K_{II}} - \sqrt{\left(\frac{K_I}{K_{II}}\right)^2 + 8}\right)\right] \quad (\text{for } K_{II} \neq 0)
    $$
    A kinetic law, such as the Paris law, is then used to determine the speed of [crack propagation](@entry_id:160116), $v_n$, based on the SIFs.

3.  **Update Crack Geometry:** The computed propagation direction and speed define a velocity vector for the [crack tip](@entry_id:182807). The [level set](@entry_id:637056) function(s) describing the crack are then evolved by solving the Hamilton-Jacobi equation, $\partial \phi / \partial t + v_n |\nabla \phi| = 0$, for a small time step.

This cycle of "solve, evaluate, and update" is repeated, allowing the simulation to capture complex, non-planar crack growth through a material without the need for cumbersome and error-prone remeshing procedures [@problem_id:3523063].