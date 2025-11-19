## Introduction
Modeling the intricate paths of propagating cracks presents a significant challenge in [computational fracture mechanics](@entry_id:203605). Traditional methods that explicitly track crack boundaries struggle with complex [topological changes](@entry_id:136654) such as branching, merging, and coalescence. This article introduces the [level set method](@entry_id:137913), a powerful implicit technique that overcomes these limitations by representing crack geometry not as a discrete mesh but as the zero level set of a continuous [scalar field](@entry_id:154310) defined over the entire domain. By studying this approach, you will gain a deep understanding of a modern and versatile tool for simulating material failure. The following chapters will guide you from fundamental theory to practical application. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, defining the [signed distance function](@entry_id:144900) and the Hamilton-Jacobi evolution equation that governs crack motion. The second chapter, "Applications and Interdisciplinary Connections," will explore its use in advanced scenarios like [fatigue analysis](@entry_id:191624), [multiphysics coupling](@entry_id:171389) for problems like [hydraulic fracturing](@entry_id:750442), and integration with experimental data. Finally, "Hands-On Practices" will provide guided exercises to apply these concepts to concrete computational problems, bridging theory with implementation.

## Principles and Mechanisms

Having established the context and motivation for using implicit methods in [fracture mechanics](@entry_id:141480), this chapter delves into the fundamental principles and mechanisms that underpin the [level set method](@entry_id:137913) for crack representation and propagation. We will begin by defining the [implicit representation](@entry_id:195378) of a crack and the special properties of the [signed distance function](@entry_id:144900). We will then explore the kinematic and physical laws governing crack evolution, and conclude with discussions on advanced representations and the integration of these concepts into numerical frameworks.

### The Implicit Representation of Crack Geometry

The foundational principle of the [level set method](@entry_id:137913) is the representation of a geometric object—in our case, a crack surface—not through an explicit parameterization of its boundary, but as the zero isocontour of a higher-dimensional scalar function.

Consider a crack surface $\Gamma$ residing within a solid body that occupies a domain $\Omega \subset \mathbb{R}^d$ (where $d=2$ or $3$). Instead of describing the points on $\Gamma$ directly, we define a continuous [scalar field](@entry_id:154310), the **[level set](@entry_id:637056) function** $\phi: \Omega \to \mathbb{R}$, such that the crack surface is implicitly defined as its zero [level set](@entry_id:637056):

$$
\Gamma = \{ \mathbf{x} \in \Omega \mid \phi(\mathbf{x}) = 0 \}
$$

This seemingly simple definition carries profound implications. One of the most significant is the natural partitioning of the domain. The sign of the [level set](@entry_id:637056) function provides a clear and unambiguous way to distinguish between the two faces of the crack. The regions on either side of the crack can be defined as the open subdomains $\Omega^+ = \{ \mathbf{x} \in \Omega \mid \phi(\mathbf{x}) > 0 \}$ and $\Omega^- = \{ \mathbf{x} \in \Omega \mid \phi(\mathbf{x})  0 \}$. The boundaries of these subdomains as they approach $\Gamma$ constitute the two crack faces. This property is crucial for formulating boundary conditions on the distinct faces and for methods like the eXtended Finite Element Method (XFEM), which require knowledge of which side of the crack an element or node lies on [@problem_id:3577098].

A key geometric property that can be extracted from the [level set](@entry_id:637056) function is the normal vector to the crack surface. For any differentiable [scalar field](@entry_id:154310), its gradient, $\nabla \phi$, is a vector that points in the direction of the steepest ascent and is orthogonal to the [level sets](@entry_id:151155) of the function. Therefore, at any point $\mathbf{x} \in \Gamma$ where the gradient is non-zero ($\nabla \phi(\mathbf{x}) \neq \mathbf{0}$), the gradient vector is normal to the crack surface. The **[unit normal vector](@entry_id:178851)** $\mathbf{n}$, typically defined to point into the $\Omega^+$ region, is given by:

$$
\mathbf{n}(\mathbf{x}) = \frac{\nabla \phi(\mathbf{x})}{\| \nabla \phi(\mathbf{x}) \|}
$$

It is important to recognize that the choice of $\phi$ for a given crack geometry $\Gamma$ is not unique. If $\phi(\mathbf{x})$ is a valid level set function for $\Gamma$, then any function $\tilde{\phi}(\mathbf{x}) = f(\phi(\mathbf{x}))$ will represent the same crack geometry, provided that $f$ is a function with the property that $f(z)=0$ if and only if $z=0$. If we also wish to preserve the identity of the crack faces, the function $f$ must be strictly increasing. For example, if $f$ is a strictly increasing differentiable function with $f(0)=0$ and $f'(0)0$, then not only is the zero level set preserved, but the regions $\Omega^+$ and $\Omega^-$ also remain unchanged, and the direction of the [unit normal vector](@entry_id:178851) is preserved [@problem_id:3577098]. This flexibility is a powerful feature, but it also suggests that for practical and computational reasons, it is often desirable to choose a level set function with special properties.

### The Signed Distance Function and its Geometric Significance

Among the infinite choices for a [level set](@entry_id:637056) function, the **Signed Distance Function (SDF)** is of paramount importance due to its elegant geometric properties and the simplifications it affords in numerical computations. For a given surface $\Gamma$, the [signed distance function](@entry_id:144900) $\phi(\mathbf{x})$ is defined such that its absolute value at any point $\mathbf{x}$ is the shortest Euclidean distance to the surface, and its sign indicates which side of the surface the point lies on:

$$
\phi(\mathbf{x}) = \pm \text{dist}(\mathbf{x}, \Gamma) = \pm \inf_{\mathbf{y} \in \Gamma} \| \mathbf{x} - \mathbf{y} \|
$$

The sign convention is typically established with respect to a predefined normal field on the crack surface [@problem_id:3577126]. This specific choice of $\phi$ is not just a convenient convention; it possesses a fundamental metric property, expressed by the **Eikonal equation**:

$$
\| \nabla \phi(\mathbf{x}) \| = 1
$$

This equation holds everywhere $\phi$ is differentiable. This property is a direct consequence of the function measuring true distance; the rate of change of distance with respect to spatial position is, by definition, unity. The fact that the gradient has a unit magnitude immediately simplifies the expression for the [normal vector](@entry_id:264185) to $\mathbf{n} = \nabla \phi$, a considerable advantage in computations [@problem_id:3577059].

The geometric information encoded in an SDF extends beyond the [normal vector](@entry_id:264185). The curvature of the level sets can also be extracted. The divergence of the normal field, $\nabla \cdot \mathbf{n}$, gives the mean curvature of the level sets. For an SDF, where $\mathbf{n} = \nabla \phi$, this becomes $\nabla \cdot (\nabla \phi) = \Delta \phi$, the Laplacian of the level set function. A crucial result is that for points $\mathbf{x}$ on the zero [level set](@entry_id:637056) $\Gamma$ itself, the Laplacian of the [signed distance function](@entry_id:144900) is equal to the mean curvature $\kappa$ of the surface at that point [@problem_id:3577059]:

$$
\Delta \phi(\mathbf{x}) = \kappa(\mathbf{x}), \quad \text{for } \mathbf{x} \in \Gamma
$$

This relationship is particularly useful. For instance, it immediately shows that a [level set](@entry_id:637056) function representing a curved crack (where $\kappa \neq 0$) cannot be a harmonic function (for which $\Delta \phi = 0$).

It is critical to distinguish the SDF from a generic implicit function, which lacks the metric property $\| \nabla \phi \| = 1$. Consider a simple rescaling, $g(\mathbf{x}) = \alpha \phi(\mathbf{x})$, where $\phi$ is an SDF and $\alpha$ is a non-zero constant. While $g(\mathbf{x})$ represents the same crack surface, its gradient magnitude is $\| \nabla g \| = \| \alpha \nabla \phi \| = |\alpha| \| \nabla \phi \| = |\alpha|$, which is not unity unless $|\alpha|=1$ [@problem_id:3577126]. The use of a function that is at least approximately an SDF is often a primary goal of numerical [level set](@entry_id:637056) algorithms.

### Crack Kinematics: The Hamilton-Jacobi Evolution Equation

The true power of the [level set method](@entry_id:137913) in [fracture mechanics](@entry_id:141480) lies in its ability to model a *moving* interface. If a crack propagates, its corresponding level set function $\phi$ must evolve in time. This evolution is governed by a [partial differential equation](@entry_id:141332) derived from the kinematics of the moving front.

Let the normal speed of the crack front at a point $\mathbf{x}$ be denoted by $F$. This speed is defined to be positive for an advancing crack. For the zero level set to move correctly, the value of $\phi$ at any point must change according to the speed of the interface passing through it. This kinematic relationship gives rise to the **Hamilton-Jacobi (HJ) evolution equation**:

$$
\frac{\partial \phi}{\partial t} + F \| \nabla \phi \| = 0
$$

Here, $\frac{\partial \phi}{\partial t}$ is the [material time derivative](@entry_id:190892) of $\phi$ at a fixed point in space. The term $F \| \nabla \phi \|$ can be interpreted as $F$ multiplied by a conversion factor that relates the change in $\phi$ to physical motion. If $\phi$ is an SDF, the equation simplifies to $\frac{\partial \phi}{\partial t} + F = 0$, meaning the function value at a fixed point decreases at a rate equal to the speed of the advancing front.

A subtle but critical issue arises from the fact that the physical propagation speed $F$ is only defined on the crack front itself (the zero level set). However, the HJ equation must be solved for $\phi(\mathbf{x}, t)$ throughout the computational domain. This necessitates an **extension of the [velocity field](@entry_id:271461)** $F$ from the crack front to a neighborhood around it. While many extension methods exist, a common and physically motivated choice is to extend $F$ such that it is constant along the normal trajectories to the crack front. This is expressed by the condition $\nabla F \cdot \mathbf{n} = 0$, where $\mathbf{n}$ is the normal to the level set.

As a concrete example, consider a 2D circular crack front of radius $r(t)$ represented by the SDF $\phi(x, y, t) = \sqrt{x^2+y^2} - r(t)$. If the propagation speed on the front is given by $F(\theta)$, where $\theta$ is the polar angle, the velocity extension would make $F$ a function of $\theta$ throughout the domain. The HJ equation describes how the radius evolves: $r'(t) = F(\theta)$. The exact solution after a time $T$ is simply $\phi(x,y,T) = \sqrt{x^2+y^2} - r_0 - F(\theta)T$, demonstrating how the entire field is advected outward along radial lines [@problem_id:3577067]. This simple case illustrates the fundamental mechanism: the evolution of the whole scalar field $\phi$ results in the motion of its zero isocontour.

### The Physics of Propagation: Coupling with Fracture Mechanics

The kinematic description provided by the HJ equation is incomplete without a physical model for the crack speed $F$. In Linear Elastic Fracture Mechanics (LEFM), the driving force for crack growth is the **energy release rate** $G$, which represents the amount of stored elastic energy that becomes available per unit area of crack extension.

According to the classic **Griffith [energy criterion](@entry_id:748980)**, a crack will advance only if this [energy release rate](@entry_id:158357) reaches a critical material property known as the **fracture toughness** or critical [energy release rate](@entry_id:158357), $G_c$. A common way to model the kinetics of crack growth is to define the crack speed $F$ as a function of the ratio $G/G_c$. A simple yet powerful **crack growth law** is given by:

$$
F = v_0 \left( \frac{G}{G_c} - 1 \right)_+ = v_0 \max\left(0, \frac{G}{G_c} - 1\right)
$$

where $v_0$ is a material parameter with units of velocity. This law elegantly captures the threshold nature of fracture: if $G  G_c$, the speed is zero and the crack is arrested; if $G \ge G_c$, the crack advances with a speed proportional to the excess driving force [@problem_id:3577092].

To use this law, one must compute the energy release rate $G$. In many LEFM scenarios, $G$ is related to the **Stress Intensity Factor (SIF)**, $K$. For a Mode I (opening) crack, this relationship is $G = K_I^2/E'$ where $E'$ is the effective Young's modulus ($E'$ is $E$ for plane stress and $E/(1-\nu^2)$ for [plane strain](@entry_id:167046)). The SIF itself depends on the applied loading $\sigma$, the crack length $a$, and the geometry of the component, often expressed via a dimensionless factor $Y$: $K_I = \sigma \sqrt{\pi a} Y(a/W)$, where $W$ is a characteristic length like the specimen width [@problem_id:3577092].

By coupling these LEFM principles with the HJ evolution, we create a complete model:
1.  From the current crack geometry (the zero set of $\phi$), compute the [energy release rate](@entry_id:158357) $G$ at the crack front.
2.  Use the crack growth law to determine the normal speed $F$.
3.  Extend the velocity $F$ off the crack front.
4.  Solve the HJ equation for a small time step to update the [level set](@entry_id:637056) function $\phi$, thereby advancing the crack.
5.  Repeat the process.

### Advanced Mechanisms and Representations

#### Computing Driving Forces via Domain Integrals

For complex geometries and loading conditions, simple analytical formulas for SIFs are unavailable. A more general and powerful method for computing the energy release rate is the **J-integral**, which can be converted into a domain integral for robust numerical evaluation. The J-integral is the first component of the Eshelby [energy-momentum tensor](@entry_id:150076) integrated around a path enclosing the crack tip. Using the [divergence theorem](@entry_id:145271) and a smooth weighting function $q(\mathbf{x})$ (which is 1 at the tip and 0 on the domain boundary), the line integral can be converted into an area or volume integral.

For a crack advancing in the $x_1$ direction, the [energy release rate](@entry_id:158357) $G$ can be expressed as:

$$
G = - \int_A \left( \Sigma_{1j} \frac{\partial q}{\partial x_j} \right) dA
$$

where $\Sigma_{ij} = W \delta_{ij} - \sigma_{kj} u_{k,i}$ is the Eshelby [energy-momentum tensor](@entry_id:150076), with $W$ being the [strain energy density](@entry_id:200085). This form is ideal for finite element computations, as it involves integrating well-behaved quantities over a domain away from the crack-tip singularity. For example, in the case of anti-plane shear (Mode III), this general expression simplifies to an integral involving only the [shear modulus](@entry_id:167228) $\mu$, displacement gradients, and the gradient of the weight function $q$ [@problem_id:3577073].

#### Representing Three-Dimensional Cracks

In three dimensions, a crack front is a curve. Representing its complex evolution requires a more sophisticated approach. The **dual [level-set method](@entry_id:165633)** employs two [scalar fields](@entry_id:151443), $\phi$ and $\psi$, to achieve this.
- The first function, $\phi(\mathbf{x})$, represents the crack surface as its zero level set, as before: $\Gamma = \{ \mathbf{x} \mid \phi(\mathbf{x})=0 \}$.
- The second function, $\psi(\mathbf{x})$, is constructed such that its zero level set intersects the crack surface orthogonally, defining the crack front curve $\mathcal{F}$: $\mathcal{F} = \{ \mathbf{x} \mid \phi(\mathbf{x})=0 \text{ and } \psi(\mathbf{x})=0 \}$.

At any point on the crack front $\mathcal{F}$, the gradients of these two functions, $\nabla \phi$ and $\nabla \psi$, are orthogonal to their respective zero-[level surfaces](@entry_id:196027). This setup provides a complete local coordinate system for describing the crack front's geometry and motion [@problem_id:3577061]:
-   **Crack Surface Normal**: The normal to the crack surface is given by $\mathbf{n} = \nabla\phi / \|\nabla\phi\|$.
-   **Crack Front Tangent**: The tangent to the crack front curve $\mathcal{F}$ is orthogonal to both $\nabla\phi$ and $\nabla\psi$, and is thus found via their cross product: $\mathbf{t} = (\nabla\phi \times \nabla\psi) / \|\nabla\phi \times \nabla\psi\|$.
-   **Propagation Direction**: The direction of [crack propagation](@entry_id:160116) *within the crack plane* is orthogonal to both $\mathbf{n}$ and $\mathbf{t}$. It is often taken as the projection of $\nabla \psi$ onto the crack's tangent plane.

This [dual representation](@entry_id:146263) provides the necessary geometric information to apply the HJ evolution equation along the entire 3D crack front.

#### Handling Topological Changes: Merging and Branching

A defining advantage of the implicit level set representation is its inherent ability to handle [topological changes](@entry_id:136654) seamlessly. Explicit methods that track a crack's boundary require complex logic to detect and perform "surgery" when cracks merge or a single crack branches into multiple daughter cracks.

In the level set framework, such events are a natural outcome of the HJ evolution. For example, **[crack branching](@entry_id:193371)** can occur if the physical driving force indicates that propagation is favorable in multiple directions simultaneously. From an LEFM perspective, a criterion for branching can be formulated by examining the directional energy release rate $G(\theta)$ around the [crack tip](@entry_id:182807). If $G(\theta)$ exhibits two or more distinct local maxima at angles $\pm \theta_b$ where the driving force exceeds the [material toughness](@entry_id:197046) ($G(\pm\theta_b) \ge G_c$), it provides a physical trigger for branching. The velocity field $F$ in the HJ equation is then defined to reflect these multiple propagation directions. The subsequent evolution of the single $\phi$ field will naturally develop a forked zero-level set, representing the branched crack, without any special algorithmic intervention [@problem_id:3577115].

### Integration with Numerical Methods and Broader Context

#### The eXtended Finite Element Method (XFEM)

The [level set method](@entry_id:137913) is a geometric tool; to perform a mechanical simulation, it must be coupled with a discretization method like the Finite Element Method (FEM). A standard FEM mesh with continuous basis functions cannot represent the displacement jump that occurs across a crack unless the mesh boundaries are aligned with the crack (a "body-fitted" mesh), which is prohibitively complex for propagating cracks.

The **eXtended Finite Element Method (XFEM)** resolves this by enriching the standard FEM approximation space. The level set function(s) provide the geometric information needed to determine which nodes require enrichment [@problem_id:3577076].
-   **Heaviside Enrichment**: Nodes whose finite element "support" (the patch of elements connected to the node) is completely cut through by the crack are enriched with a discontinuous Heaviside function. This allows the model to capture the displacement jump.
-   **Crack-Tip Enrichment**: Nodes whose support contains a [crack tip](@entry_id:182807) are enriched with special functions that replicate the known asymptotic near-tip fields from LEFM (e.g., functions involving $\sqrt{r}\sin(\theta/2)$). This allows the model to accurately represent the [stress singularity](@entry_id:166362) without extreme [mesh refinement](@entry_id:168565).

The selection is topological: it depends on whether an element is cut by the $\phi=0$ level set or contains the [crack tip](@entry_id:182807), not on simple proximity. This makes the method robust and accurate.

#### Context: Sharp vs. Diffuse Interface Models

It is instructive to place the [level set method](@entry_id:137913) in the broader context of fracture modeling paradigms. The [level set method](@entry_id:137913) is a quintessential **sharp-interface** approach: the crack is a lower-dimensional manifold with zero thickness that sharply divides the domain. The [displacement field](@entry_id:141476) is discontinuous across this interface.

This stands in contrast to **diffuse-interface** or **phase-field** models. In these models, a crack is represented by a continuous scalar field $d(\mathbf{x})$, often called a damage or phase field, where $d \in [0, 1]$. The value $d=0$ represents intact material, while $d=1$ represents fully broken material. The crack is "smeared" over a region with a characteristic thickness $\ell$. Instead of a displacement jump, there is a continuous displacement field with very high strains localized in the damaged band. The traction-free condition is mimicked by degrading the material's elastic stiffness as a function of $d$ [@problem_id:3577120].

While conceptually different, the two approaches are deeply connected. Under appropriate energetic formulations, it can be shown that as the regularization length scale of the [phase-field model](@entry_id:178606) goes to zero ($\ell \to 0$), the solution $\Gamma$-converges to that of the sharp Griffith fracture model [@problem_id:3577120]. Each paradigm has its advantages: [level set](@entry_id:637056)/XFEM models explicitly enforce the sharp discontinuity, while [phase-field models](@entry_id:202885) avoid the need for enrichment and can naturally predict complex crack initiation and branching patterns by solving a standard system of PDEs.