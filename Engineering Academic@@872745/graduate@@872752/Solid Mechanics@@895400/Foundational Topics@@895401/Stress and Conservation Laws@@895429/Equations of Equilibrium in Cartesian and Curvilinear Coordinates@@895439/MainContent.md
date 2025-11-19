## Introduction
In the study of solid mechanics, the concept of equilibrium is paramount. It represents the state of balance where all forces and moments acting on a body or any part of it sum to zero, ensuring it remains at rest or in uniform motion. While this principle is intuitive, expressing it in a mathematically rigorous form that is applicable to deformable [continuous bodies](@entry_id:168586) with complex geometries presents a significant challenge. How do we translate the global balance of forces on a body into a set of local equations valid at every single point within it? And how do these equations adapt when we move from a simple rectangular block to a curved pressure vessel or a rotating turbine blade?

This article provides a comprehensive exploration of the [equations of equilibrium](@entry_id:193797), forming a foundational pillar of [continuum mechanics](@entry_id:155125). We will embark on a journey from first principles to advanced applications, designed to build a deep and flexible understanding of this critical topic. In the first chapter, **Principles and Mechanisms**, we will derive the [equilibrium equations](@entry_id:172166) from the fundamental laws of momentum balance, first in the familiar Cartesian coordinate system and then generalizing to any curvilinear system using the powerful tools of [tensor calculus](@entry_id:161423). Next, in **Applications and Interdisciplinary Connections**, we will witness the remarkable versatility of these equations, seeing how they are applied to solve problems in engineering, geophysics, computational methods, and even quantum chemistry. Finally, the **Hands-On Practices** chapter will provide a series of guided problems that allow you to actively apply these concepts, cementing your knowledge from the algebraic to the abstract. By the end, you will not only understand the equations but also appreciate their role as a unifying language across science and engineering.

## Principles and Mechanisms

The state of stress within a continuum body is governed by fundamental physical laws of balance. While the introductory chapter has established the concept of stress, this chapter delves into the mathematical formulation of the equilibrium conditions that arise from these laws. We will begin by deriving the [equations of equilibrium](@entry_id:193797) from first principles in the familiar setting of Cartesian coordinates. Subsequently, we will generalize this framework to arbitrary [curvilinear coordinate systems](@entry_id:172561), a necessary step for analyzing problems with geometric complexities. This generalization will require us to introduce the powerful machinery of [tensor calculus](@entry_id:161423), clarifying the profound difference between a physical law and its particular representation in a coordinate system.

### The Foundation: Balance of Linear Momentum

The cornerstone of [static analysis](@entry_id:755368) in [continuum mechanics](@entry_id:155125) is the principle of **[balance of linear momentum](@entry_id:193575)**. In its integral form, this principle, which is a direct application of Newton's laws to a continuous body, states that for any arbitrary portion of the body (a sub-volume $V$ enclosed by a surface $S$), the sum of all external forces acting upon it must be zero. These forces are of two types: **[surface forces](@entry_id:188034)**, which act on the boundary $S$ of the volume, and **body forces**, which act on the material within the volume $V$.

Surface forces are represented by the **[traction vector](@entry_id:189429)**, $\boldsymbol{t}$, which is the force per unit area acting at a point on the surface. Body forces, such as gravity or electromagnetic forces, are represented by a force density field. This density can be expressed per unit mass, $\boldsymbol{b}$, or per unit volume, $\boldsymbol{f}$. The two are related by the mass density $\rho$ of the material, such that $\boldsymbol{f} = \rho \boldsymbol{b}$.

The integral form of the [balance of linear momentum](@entry_id:193575) for a body in static equilibrium is therefore:

$$
\int_S \boldsymbol{t} \, dS + \int_V \rho \boldsymbol{b} \, dV = \boldsymbol{0}
$$

This equation represents a global balance over a [finite volume](@entry_id:749401). It is important to note what is being omitted to arrive at this static form. The general principle of linear momentum equates the sum of forces to the time rate of change of the body's total momentum. The total momentum is given by $\int_V \rho \boldsymbol{v} \, dV$, where $\boldsymbol{v}$ is the [velocity field](@entry_id:271461). Its [material time derivative](@entry_id:190892) results in an inertial term, $\int_V \rho \boldsymbol{a} \, dV$, where $\boldsymbol{a}$ is the [material acceleration](@entry_id:270992) field. The static [equilibrium equation](@entry_id:749057) is thus a specialization of the more general dynamic [equation of motion](@entry_id:264286), $\int_S \boldsymbol{t} \, dS + \int_V \rho \boldsymbol{b} \, dV = \int_V \rho \boldsymbol{a} \, dV$, under the fundamental assumption that the [acceleration field](@entry_id:266595) is zero, $\boldsymbol{a} = \boldsymbol{0}$ [@problem_id:2636667] [@problem_id:2636641].

In many engineering scenarios, a system is not perfectly static, but the accelerations are small enough that the inertial term $\rho \boldsymbol{a}$ is negligible compared to the stress divergence and body force terms. This is the **[quasi-static approximation](@entry_id:167818)**. A useful criterion for its validity is when the [characteristic time scale](@entry_id:274321) of loading, $T_c$, is much larger than the time it takes for a mechanical wave to travel across the body's characteristic length $L$. This is expressed as $T_c \gg L/c$, where $c$ is the relevant [wave speed](@entry_id:186208) in the material [@problem_id:2636641]. It is also noteworthy that this static framework can be adapted to analyze bodies in steady motion within [non-inertial reference frames](@entry_id:169712), such as a turbine blade rotating at a constant [angular velocity](@entry_id:192539). In such cases, the [fictitious forces](@entry_id:165088) (e.g., centrifugal force) are incorporated into an effective [body force](@entry_id:184443) term, and "static" then refers to the absence of acceleration relative to the moving frame [@problem_id:2636641].

### From Integral to Local Form: The Equation of Equilibrium

The integral form of equilibrium is powerful, but for solving [boundary value problems](@entry_id:137204), a local, [differential form](@entry_id:174025) is indispensable. To transition from the global statement to a local one, we require two key theoretical tools: Cauchy's stress theorem and the [divergence theorem](@entry_id:145271).

In the 19th century, Augustin-Louis Cauchy postulated that the [traction vector](@entry_id:189429) $\boldsymbol{t}$ at a point on a surface depends linearly on the orientation of that surface, as defined by its [unit normal vector](@entry_id:178851) $\boldsymbol{n}$. This [linear relationship](@entry_id:267880) is embodied by a second-order tensor field, $\boldsymbol{\sigma}$, known as the **Cauchy stress tensor**. The relationship, or traction law, is expressed as:

$$
\boldsymbol{t}(\boldsymbol{n}) = \boldsymbol{\sigma}^T \cdot \boldsymbol{n} \quad \text{or, in index notation,} \quad t_i = \sigma_{ji} n_j
$$

Here, $\sigma_{ij}$ represents the $i$-th component of the force acting on a surface whose normal is oriented in the $j$-th direction. The existence of this tensor is a fundamental tenet of [continuum mechanics](@entry_id:155125), valid for any continuum material, not just isotropic ones [@problem_id:2636626] [@problem_id:2636667].

Substituting this traction law into the integral balance equation gives:

$$
\int_S \sigma_{ji} n_j \, dS + \int_V \rho b_i \, dV = 0
$$

This equation must hold for each component $i=1,2,3$. The next step is to apply the **divergence theorem** (also known as Gauss's theorem), which relates the integral of a vector field's flux over a closed surface to the volume integral of its divergence. Applying it to the stress term for each fixed component $i$:

$$
\int_S \sigma_{ji} n_j \, dS = \int_V \frac{\partial \sigma_{ji}}{\partial x_j} \, dV
$$

Substituting this back into the balance equation allows us to combine both terms under a single volume integral:

$$
\int_V \left( \frac{\partial \sigma_{ji}}{\partial x_j} + \rho b_i \right) \, dV = 0
$$

The final step is the **localization principle**. Since this integral must vanish for *any* arbitrary sub-volume $V$ we choose within the body, the integrand itself must be zero at every point (assuming continuity). This yields the local, [differential form](@entry_id:174025) of the static [equilibrium equations](@entry_id:172166):

$$
\frac{\partial \sigma_{ji}}{\partial x_j} + \rho b_i = 0
$$

We are not quite finished. As we will rigorously prove in the next section, the [balance of angular momentum](@entry_id:181848) requires the Cauchy stress tensor to be symmetric, i.e., $\sigma_{ij} = \sigma_{ji}$. Applying this property, we can write the equation in its most common form. Using comma notation to denote [partial differentiation](@entry_id:194612) ($\partial f / \partial x_j \equiv f_{,j}$), the [equations of equilibrium](@entry_id:193797) in Cartesian coordinates are:

$$
\sigma_{ij,j} + \rho b_i = 0 \quad \text{for } i=1,2,3
$$

This is a system of three scalar partial differential equations. Written out explicitly, they are:
$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{yx}}{\partial y} + \frac{\partial \sigma_{zx}}{\partial z} + \rho b_x = 0
$$
$$
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{zy}}{\partial z} + \rho b_y = 0
$$
$$
\frac{\partial \sigma_{xz}}{\partial x} + \frac{\partial \sigma_{yz}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} + \rho b_z = 0
$$

### A Fundamental Property: The Symmetry of the Cauchy Stress Tensor

The derivation of the [equilibrium equations](@entry_id:172166) relied on the symmetry of the stress tensor, $\sigma_{ij} = \sigma_{ji}$. This property is not an ad-hoc assumption but a direct consequence of another fundamental law: the **[balance of angular momentum](@entry_id:181848)**. In a classical continuum theory that does not account for distributed body couples or couple stresses (so-called non-polar media), the time rate of change of angular momentum of a body about a fixed point is equal to the sum of the moments of all external forces [@problem_id:2636648].

For a static body, the integral form of this balance is:
$$
\int_S \boldsymbol{x} \times \boldsymbol{t} \, dS + \int_V \boldsymbol{x} \times (\rho \boldsymbol{b}) \, dV = \boldsymbol{0}
$$
where $\boldsymbol{x}$ is the [position vector](@entry_id:168381). Following a localization procedure similar to the one used for linear momentum, which involves substituting Cauchy's traction law, applying the [divergence theorem](@entry_id:145271), and crucially, substituting the already-derived local equation for [linear momentum](@entry_id:174467) balance ($\nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0}$), one finds that the integral relation simplifies remarkably. It reduces to a purely local, algebraic condition on the stress tensor itself:
$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T \quad \text{or, in index notation,} \quad \sigma_{ij} = \sigma_{ji}
$$
In component form, this can be expressed as $\varepsilon_{ijk}\sigma_{kj} = 0$, where $\varepsilon_{ijk}$ is the Levi-Civita [permutation symbol](@entry_id:193594). This result is profound. It demonstrates that the stress tensor in a classical continuum must be symmetric for angular momentum to be conserved. This is a fundamental law of mechanics, not a constitutive property dependent on the material (like elasticity or isotropy) [@problem_id:2636648]. This symmetry reduces the number of independent stress components at a point from nine to six.

### Generalization to Curvilinear Coordinates: The Principle of Covariance

Physical reality does not depend on the coordinate system we use to describe it. The [balance of linear momentum](@entry_id:193575), expressed abstractly as $\nabla \cdot \boldsymbol{\sigma} + \rho \boldsymbol{b} = \boldsymbol{0}$, is a **tensor equation**. A defining characteristic of a tensor equation is that its form is invariant under [coordinate transformations](@entry_id:172727); it is **coordinate-invariant** or **covariant** [@problem_id:2636613] [@problem_id:2636661].

This principle has a critical consequence: while the equation's abstract form is unchanged, its representation in terms of components will generally look different in different coordinate systems. The simple form $\sigma_{ij,j} + \rho b_i = 0$ is valid only for Cartesian coordinates, where the basis vectors ($\boldsymbol{e}_x, \boldsymbol{e}_y, \boldsymbol{e}_z$) are constant in both magnitude and direction throughout space.

In a general curvilinear coordinate system, such as cylindrical $(r, \theta, z)$ or spherical $(\rho, \theta, \phi)$ coordinates, the basis vectors are not constant. For example, in a cylindrical system, the radial basis vector $\boldsymbol{e}_r$ points in different directions at different values of $\theta$. The derivative of a [tensor field](@entry_id:266532), such as stress, must account for the change in the components *and* the change in the basis vectors. The simple partial derivative of the components, $\partial \sigma^{ij}/\partial q^j$, is insufficient because it does not transform as a tensor and fails to capture the full geometric picture.

### The Mechanism of Covariance: The Covariant Derivative

To properly handle differentiation in [curvilinear coordinates](@entry_id:178535), we must introduce the concept of the **[covariant derivative](@entry_id:152476)**. Let's consider a general curvilinear coordinate system $q^i$ with [position vector](@entry_id:168381) $\boldsymbol{x}(q^1, q^2, q^3)$. The local **[covariant basis](@entry_id:198968) vectors** are defined as the [tangent vectors](@entry_id:265494) to the coordinate curves: $\boldsymbol{g}_i = \partial\boldsymbol{x}/\partial q^i$ [@problem_id:2636606].

The change in a basis vector $\boldsymbol{g}_j$ as we move along a coordinate curve $q^k$ is given by the partial derivative $\partial \boldsymbol{g}_j / \partial q^k$. Since this derivative is itself a vector, it can be expressed as a linear combination of the basis vectors at that point:

$$
\frac{\partial \boldsymbol{g}_j}{\partial q^k} = \Gamma^l_{kj} \boldsymbol{g}_l
$$

The coefficients $\Gamma^l_{kj}$ are the **Christoffel symbols of the second kind**. They are not components of a tensor but are geometric quantities that encode how the coordinate system's basis vectors change from point to point [@problem_id:2636606]. For a coordinate system derived from a smooth mapping, they are symmetric in their lower indices: $\Gamma^l_{kj} = \Gamma^l_{jk}$.

With this definition, we can define a derivative operator that produces a true tensor. The [covariant derivative](@entry_id:152476) of a vector field $v^i$, for example, is defined as:
$$
\nabla_k v^i \equiv v^i_{;k} = \frac{\partial v^i}{\partial q^k} + \Gamma^i_{lk}v^l
$$
The Christoffel symbol term is precisely the correction needed to account for the changing basis, ensuring that the resulting object, $v^i_{;k}$, transforms as a type-(1,1) tensor.

The same principle applies to the stress tensor. The **[covariant divergence](@entry_id:275039)** of the contravariant stress tensor $\sigma^{ij}$ is the contraction of its [covariant derivative](@entry_id:152476), $(\text{div } \boldsymbol{\sigma})^i = \sigma^{ij}{}_{;j}$. Its full expression is [@problem_id:2636650] [@problem_id:2636661]:

$$
\sigma^{ij}{}_{;j} = \frac{\partial\sigma^{ij}}{\partial q^j} + \Gamma^{i}{}_{kj}\sigma^{kj} + \Gamma^{j}{}_{kj}\sigma^{ik}
$$

The local equation of equilibrium, $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \boldsymbol{0}$, can now be written in its general component form, valid in any coordinate system:

$$
\sigma^{ij}{}_{;j} + b^i = 0
$$

The Christoffel symbols themselves are determined by the geometry of the coordinate system, specifically by the **metric tensor**, $g_{ij} = \boldsymbol{g}_i \cdot \boldsymbol{g}_j$, and its derivatives. The unique, torsion-free, [metric-compatible connection](@entry_id:194538) used in mechanics is the **Levi-Civita connection**, whose Christoffel symbols are given by the metric [@problem_id:2636606]. This deep connection ensures that the entire framework is self-consistent. For instance, a useful identity relates the trace of the Christoffel symbols to the determinant of the metric tensor, $g = \det[g_{ij}]$, as $\Gamma^j_{kj} = (1/\sqrt{g})\partial_k\sqrt{g}$. This allows the [covariant divergence](@entry_id:275039) to be written in alternative compact forms, which are often convenient for calculation [@problem_id:2636629].

### Application: Equilibrium in Cylindrical Coordinates

To make these abstract concepts concrete, let us derive the [equations of equilibrium](@entry_id:193797) in the commonly used orthonormal [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$. The non-constant basis vectors give rise to non-zero Christoffel symbols, which manifest as additional "geometric" terms in the final equations. By performing the full divergence calculation, one obtains the three scalar [equilibrium equations](@entry_id:172166) for the physical stress components [@problem_id:2636643] [@problem_id:2636626]:

**Radial ($r$) direction:**
$$
\frac{\partial \sigma_{rr}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{r\theta}}{\partial\theta} + \frac{\partial \sigma_{rz}}{\partial z} + \frac{\sigma_{rr}-\sigma_{\theta\theta}}{r} + b_r=0
$$

**Circumferential ($\theta$) direction:**
$$
\frac{\partial \sigma_{r\theta}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta\theta}}{\partial\theta} + \frac{\partial \sigma_{\theta z}}{\partial z} + \frac{2\sigma_{r\theta}}{r} + b_{\theta}=0
$$

**Axial ($z$) direction:**
$$
\frac{\partial \sigma_{rz}}{\partial r} + \frac{1}{r}\frac{\partial \sigma_{\theta z}}{\partial\theta} + \frac{\partial \sigma_{zz}}{\partial z} + \frac{\sigma_{rz}}{r} + b_z=0
$$

In these equations, the terms involving division by $r$, such as $(\sigma_{rr}-\sigma_{\theta\theta})/r$ and $2\sigma_{r\theta}/r$, are the direct result of the non-zero Christoffel symbols. They are not arbitrary additions but are the necessary geometric corrections that arise from expressing the invariant physical law of momentum balance in a curved coordinate system. For instance, the term $(\sigma_{rr}-\sigma_{\theta\theta})/r$ arises from the fact that the surfaces on which $\sigma_{rr}$ and $\sigma_{\theta\theta}$ act are not parallel and have areas that scale differently with radius. These equations form the starting point for solving a vast range of problems in engineering and physics, from pressurized pipes to rotating disks. Under simplifying assumptions, such as axisymmetry ($\partial/\partial\theta = 0$), these equations reduce further, facilitating analytical solutions [@problem_id:2636641].