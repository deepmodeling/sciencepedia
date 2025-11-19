## Introduction
Classical [continuum mechanics](@entry_id:155125), built upon differential equations, has been the cornerstone of [solid mechanics](@entry_id:164042) for centuries. However, its foundation crumbles when faced with discontinuities, such as the cracks that initiate and propagate during [material failure](@entry_id:160997). The spatial derivatives central to classical theory become undefined at a crack, necessitating complex, often ad-hoc, extensions like fracture mechanics to predict failure. Peridynamics offers a radical and elegant solution by reformulating the fundamental laws of mechanics. It abandons spatial derivatives in favor of integral equations, describing forces as long-range interactions between points in a material. This conceptual shift provides a unified framework where continuous deformation and fracture are two facets of the same underlying theory.

This article will guide you through the world of [peridynamics](@entry_id:191791) and other non-local continuum theories, from first principles to advanced applications. We begin in the **Principles and Mechanisms** chapter by deriving the peridynamic equation of motion, examining its conservation laws, and tracing the evolution of its [constitutive models](@entry_id:174726) from simple bond-based approaches to the powerful state-based framework. Next, in **Applications and Interdisciplinary Connections**, we will explore the theory's remarkable versatility in modeling complex phenomena, including plasticity, viscoelasticity, and [multiphysics](@entry_id:164478) couplings with thermal, chemical, and electrical fields. Finally, the **Hands-On Practices** chapter provides an opportunity to solidify your understanding by tackling concrete problems in [wave dispersion](@entry_id:180230), parameter calibration, and numerical implementation, bridging the gap between theory and computation.

## Principles and Mechanisms

The transition from classical, local continuum mechanics to a nonlocal framework such as [peridynamics](@entry_id:191791) necessitates a reformulation of the fundamental principles of motion and material response. The core idea is to replace the spatial derivatives that underpin classical theories with [integral operators](@entry_id:187690) that describe interactions over finite distances. This conceptual shift not only allows for the modeling of phenomena involving discontinuities, such as fracture, but also introduces a new set of principles and challenges related to [constitutive modeling](@entry_id:183370), conservation laws, and numerical implementation. This chapter elucidates these core principles and mechanisms.

### The Peridynamic Equation of Motion

In classical continuum mechanics, the internal force density at a material point is given by the divergence of a local stress tensor. This formulation inherently requires that the [displacement field](@entry_id:141476) be differentiable, a condition that is violated at cracks or other sharp discontinuities. Peridynamics reformulates the [balance of linear momentum](@entry_id:193575) by postulating that internal forces arise from the sum of direct, long-range interactions between a material point and all other points within its vicinity.

Consider a material point located at position $\boldsymbol{x}$ in the reference configuration. This point interacts with other points $\boldsymbol{x}'$ that lie within a finite region called the **horizon**, denoted as $\mathcal{H}_{\boldsymbol{x}}$. The horizon is typically defined as a ball of radius $\delta$ centered at $\boldsymbol{x}$, such that $\mathcal{H}_{\boldsymbol{x}} = \{\boldsymbol{x}' \in \Omega : \|\boldsymbol{x}' - \boldsymbol{x}\| \le \delta\}$, where $\Omega$ is the domain occupied by the body and $\delta$ is the **horizon radius**, an [intrinsic length scale](@entry_id:750789) of the material.

The interaction between $\boldsymbol{x}$ and $\boldsymbol{x}'$ is described by a **pairwise force density** function, $\boldsymbol{f}$, which represents the force per unit volume squared that the point at $\boldsymbol{x}'$ exerts on the point at $\boldsymbol{x}$. The total internal force density at $\boldsymbol{x}$, denoted $\boldsymbol{L}(\boldsymbol{x}, t)$, is obtained by integrating these pairwise contributions over the horizon. Applying Newton's second law, the peridynamic [equation of motion](@entry_id:264286) is stated as an integro-differential equation:

$$
\rho(\boldsymbol{x}) \ddot{\boldsymbol{u}}(\boldsymbol{x}, t) = \int_{\mathcal{H}_{\boldsymbol{x}}} \boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x}', t) - \boldsymbol{u}(\boldsymbol{x}, t), \boldsymbol{x}', \boldsymbol{x}) \, \mathrm{d}V_{\boldsymbol{x}'} + \boldsymbol{b}(\boldsymbol{x}, t)
$$

Here, $\rho(\boldsymbol{x})$ is the mass density, $\boldsymbol{u}(\boldsymbol{x}, t)$ is the displacement field, $\ddot{\boldsymbol{u}}$ is the acceleration, and $\boldsymbol{b}(\boldsymbol{x}, t)$ is a prescribed external [body force](@entry_id:184443) density. The pairwise force function $\boldsymbol{f}$ depends on the relative displacement of the two points, $\boldsymbol{\eta} = \boldsymbol{u}(\boldsymbol{x}', t) - \boldsymbol{u}(\boldsymbol{x}, t)$, and their initial positions, captured by the **bond** vector $\boldsymbol{\xi} = \boldsymbol{x}' - \boldsymbol{x}$.

The most profound consequence of this integral formulation is its ability to naturally handle discontinuities. The equation does not involve spatial derivatives of the displacement field, $\nabla \boldsymbol{u}$. Instead, it relies on finite differences of $\boldsymbol{u}$ across bonds. For the integral to be well-defined, the [displacement field](@entry_id:141476) $\boldsymbol{u}$ only needs to satisfy weaker regularity conditions (e.g., being in a Lebesgue space) than the differentiability required by classical theory. A crack, which is a surface of displacement discontinuity, corresponds to a set of points of [measure zero](@entry_id:137864) within the three-dimensional volume of integration $\mathcal{H}_{\boldsymbol{x}}$. Therefore, the integral remains well-defined "almost everywhere" without producing the non-[integrable singularities](@entry_id:634345) (like Dirac delta functions) that arise from taking derivatives of a [discontinuous function](@entry_id:143848). This allows [peridynamics](@entry_id:191791) to model crack initiation and propagation without any special numerical treatment or ad-hoc criteria.

### Fundamental Conservation Laws and Objectivity

For the peridynamic model to be physically valid, it must adhere to the fundamental principles of mechanics, including the conservation of linear and angular momentum, and the [principle of material frame-indifference](@entry_id:188488) (objectivity).

The **[balance of linear momentum](@entry_id:193575)** requires that for any isolated part of the body, the net internal force must be zero. This is guaranteed if the pairwise forces obey Newton's third law of action and reaction. In the peridynamic framework, this translates to an antisymmetry condition on the pairwise force density function:

$$
\boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x}', t) - \boldsymbol{u}(\boldsymbol{x}, t), \boldsymbol{x}', \boldsymbol{x}) = -\boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x}, t) - \boldsymbol{u}(\boldsymbol{x}', t), \boldsymbol{x}, \boldsymbol{x}')
$$

The **[balance of angular momentum](@entry_id:181848)**, in the absence of distributed body couples, requires that the net internal torque on any part of the body also vanishes. This imposes a further constraint on the pairwise forces. Specifically, the force vector $\boldsymbol{f}$ between two points must be collinear with the vector connecting their deformed positions, $\boldsymbol{y}(\boldsymbol{x}', t) - \boldsymbol{y}(\boldsymbol{x}, t)$. Such a force is known as a **central force**. This condition ensures that the moment arm and the force vector are parallel, yielding zero torque for each interacting pair. While this is a strict requirement for simple peridynamic models, more advanced formulations relax this constraint, as will be discussed later.

The principle of **[material frame-indifference](@entry_id:178419)**, or **objectivity**, demands that the constitutive response of the material must be independent of the observer. This means the internal forces must transform appropriately under a superposed [rigid body motion](@entry_id:144691) (translation and rotation). If the observer applies a rigid rotation $\boldsymbol{Q}(t)$, the deformed bond vector $\boldsymbol{Y} = \boldsymbol{y}' - \boldsymbol{y}$ transforms to $\boldsymbol{Q}\boldsymbol{Y}$, and the [constitutive law](@entry_id:167255) must predict a force that transforms similarly, i.e., $\boldsymbol{f}^* = \boldsymbol{Q}\boldsymbol{f}$. This is formally expressed as a requirement of [equivariance](@entry_id:636671) on the constitutive function. Furthermore, a pure [rigid body motion](@entry_id:144691) of the material, which involves no deformation, must produce zero internal forces.

### Constitutive Modeling: From Bond-Based to State-Based Peridynamics

The predictive power of [peridynamics](@entry_id:191791) lies in its [constitutive model](@entry_id:747751), which defines the pairwise force function $\boldsymbol{f}$. The theory has evolved from simple models with significant limitations to more general frameworks capable of describing a wide range of material behaviors.

#### Bond-Based Peridynamics and its Limitations

The simplest and original formulation is **[bond-based peridynamics](@entry_id:188457)**. In this model, the interaction between any two points is assumed to be independent of all other interactions. The force is a central force that depends only on the **stretch** of the bond connecting the two points. The stretch, $s$, is the fractional change in the bond's length:

$$
s = \frac{\|\boldsymbol{y}(\boldsymbol{x}', t) - \boldsymbol{y}(\boldsymbol{x}, t)\| - \|\boldsymbol{x}' - \boldsymbol{x}\|}{\|\boldsymbol{x}' - \boldsymbol{x}\|}
$$

For a linear, microelastic material, the magnitude of the pairwise force is proportional to the stretch, modulated by a **micromodulus function** $c(\boldsymbol{\xi})$ that depends on the initial bond vector $\boldsymbol{\xi}$. The micromodulus characterizes the stiffness of the bonds. For an isotropic material, $c$ depends only on the [bond length](@entry_id:144592), $c(\boldsymbol{\xi}) = \tilde{c}(\|\boldsymbol{\xi}\|)$. For [material stability](@entry_id:183933), the [strain energy](@entry_id:162699) must be positive, which requires $\tilde{c}(r) \ge 0$ for all $r \le \delta$.

To connect this micromodel to classical elasticity, one equates the peridynamic [strain energy density](@entry_id:200085) with the classical [strain energy density](@entry_id:200085) under a homogeneous strain field. This calibration procedure reveals a major limitation of the bond-based model. The central, independent force assumption imposes a rigid constraint on the resulting elastic properties. For a 3D isotropic material, this procedure invariably leads to the conclusion that the Lamé parameters must be equal, $\lambda = \mu$. This, in turn, fixes the Poisson's ratio to $\nu = 1/4$, regardless of the choice of micromodulus function $c(r)$ or horizon $\delta$. This severe restriction makes [bond-based peridynamics](@entry_id:188457) unsuitable for accurately modeling many common engineering materials.

#### State-Based Peridynamics: A General Framework

To overcome this limitation, **[state-based peridynamics](@entry_id:190841)** was introduced. This more general framework replaces the scalar-valued bond stretch with vector-valued **states**.

A **deformation state**, denoted $\underline{\boldsymbol{Y}}[\boldsymbol{x}, t]$, is a function that collects all the deformed bond vectors originating from a point $\boldsymbol{x}$:
$$
\underline{\boldsymbol{Y}}[\boldsymbol{x}, t]\langle\boldsymbol{\xi}\rangle = \boldsymbol{y}(\boldsymbol{x}+\boldsymbol{\xi}, t) - \boldsymbol{y}(\boldsymbol{x}, t)
$$
A **force state**, denoted $\underline{\boldsymbol{T}}[\boldsymbol{x}, t]$, is a function that assigns a force vector to each bond originating from $\boldsymbol{x}$:
$$
\underline{\boldsymbol{T}}[\boldsymbol{x}, t]\langle\boldsymbol{\xi}\rangle = \boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x}+\boldsymbol{\xi}, t) - \boldsymbol{u}(\boldsymbol{x}, t), \boldsymbol{x}+\boldsymbol{\xi}, \boldsymbol{x})
$$
The crucial difference is that the force state $\underline{\boldsymbol{T}}$ is a functional of the entire deformation state $\underline{\boldsymbol{Y}}$. This means the force in a particular bond $\boldsymbol{\xi}$ can now depend on the deformation of all other bonds in the neighborhood. This cross-coupling allows for a much richer constitutive response.

State-based models are further classified:
-   **Ordinary State-Based Peridynamics**: In this class, the force vector in each bond, $\underline{\boldsymbol{T}}[\boldsymbol{x}]\langle\boldsymbol{\xi}\rangle$, is still required to be collinear with the deformed bond vector, $\underline{\boldsymbol{Y}}[\boldsymbol{x}]\langle\boldsymbol{\xi}\rangle$. This preserves the [central force](@entry_id:160395) nature and automatically satisfies the [balance of angular momentum](@entry_id:181848). However, because the magnitude of the force can depend on the collective deformation of the neighborhood, it is possible to construct models that correspond to any physically admissible Poisson's ratio.
-   **Non-Ordinary State-Based Peridynamics**: This is the most general form, where the collinearity constraint is relaxed. The force vector is not necessarily parallel to the deformed bond vector, allowing for non-[central forces](@entry_id:267832). In this case, the [balance of angular momentum](@entry_id:181848) is not automatically satisfied for each bond pair. Instead, it must be enforced through an integral constraint on the [constitutive law](@entry_id:167255), which is equivalent to requiring the symmetry of a nonlocal stress tensor. This framework is powerful enough to subsume classical [continuum mechanics](@entry_id:155125) as a special case and can model a vast range of complex material behaviors, including [thermomechanical coupling](@entry_id:183230) by augmenting the deformation state with thermal effects.

### The Mechanics of Fracture and Regularization

A primary motivation for the development of [peridynamics](@entry_id:191791) is its intrinsic capability to model material failure and fracture.

#### Damage and Emergent Crack Formation

In [bond-based peridynamics](@entry_id:188457), a simple and effective damage model is based on a **[critical stretch](@entry_id:200184) criterion**. Each bond is assumed to have a finite strength, characterized by a [critical stretch](@entry_id:200184) value, $s_c$. If the stretch of a bond exceeds this critical value, the bond is considered broken and can no longer sustain any force. This failure is typically modeled as irreversible.

The process of fracture emerges naturally from this mechanism:
1.  **Initiation**: As a material is loaded, the stretch in the bonds increases. A crack initiates in the region where a bond (or a cluster of bonds) first reaches the [critical stretch](@entry_id:200184) $s_c$.
2.  **Propagation**: Once a bond breaks, the load it was carrying is redistributed to its neighbors. This can cause the stretch in adjacent bonds to increase, potentially leading them to reach $s_c$ and fail as well. This cascade of bond failures constitutes [crack propagation](@entry_id:160116).

Because the governing equation is an integral over interacting particles, a crack is simply represented as a surface across which bonds have been broken. The peridynamic integral for a point near this surface automatically excludes contributions from points on the other side, naturally creating a traction-free crack face. This elegant mechanism avoids the need for supplemental equations to track crack paths or define propagation criteria, which are major challenges in classical [fracture mechanics](@entry_id:141480) methodologies.

#### Nonlocality as a Regularization Method

The use of a [nonlocal theory](@entry_id:752667) provides a crucial mathematical benefit when modeling materials that soften, i.e., lose stiffness as they accumulate damage. In classical *local* models, [strain softening](@entry_id:185019) leads to a loss of [ellipticity](@entry_id:199972) of the governing equations. When solved numerically, this manifests as a **[pathological mesh dependence](@entry_id:183356)**: the deformation localizes into a zone whose width is dictated by the computational mesh size. As the mesh is refined, the width of the damage zone shrinks to zero, and the calculated energy required to form the fracture, $G_f$, also spuriously converges to zero. This is physically incorrect, as fracture energy should be a material property.

Nonlocal models, including [peridynamics](@entry_id:191791), regularize this problem by introducing an [intrinsic material length scale](@entry_id:197348), the horizon $\delta$. The averaging nature of the integral operator prevents strain from localizing to a zone smaller than the horizon. The width of the damage process zone is therefore determined by $\delta$, not the mesh size. As a result, the computed fracture energy converges to a finite, non-zero value that is objective with respect to [mesh refinement](@entry_id:168565). The fracture energy can be directly related to the energy required to break all the bonds crossing a unit area, providing a physical link between the micro-scale bond properties and the macro-scale [fracture toughness](@entry_id:157609).

### Implementation and Convergence

While the peridynamic framework offers significant advantages, its nonlocal nature introduces unique challenges in numerical implementation, particularly concerning the application of boundary conditions and ensuring convergence to classical solutions in the appropriate limit.

#### The Challenge of Boundary Conditions

Classical boundary conditions, such as prescribed displacements (Dirichlet) or prescribed tractions (Neumann), are defined on surfaces, which have zero volume. The peridynamic [equation of motion](@entry_id:264286), however, is a volumetric [integral equation](@entry_id:165305). A point near a boundary has a truncated horizon, leading to an artificial mechanical response known as the "surface effect." Directly applying a condition on the boundary surface is ill-posed.

To address this, several remedies have been developed:
-   **Dirichlet Conditions**: One common approach is to enforce the displacement constraint not on the boundary surface itself, but over a volumetric "collar" or "boundary layer" of thickness $\delta$. An alternative and widely used method is to create a **fictitious layer** of "ghost" particles outside the domain. The displacements of these ghost particles are prescribed according to the desired boundary condition, thus providing the "missing" interactions for the real particles near the boundary.
-   **Neumann Conditions**: Applying a [surface traction](@entry_id:198058) $\bar{\boldsymbol{t}}$ is often achieved by converting it into an equivalent [body force](@entry_id:184443) $\boldsymbol{b}$ that acts within a boundary layer of thickness $\delta$. The equivalence is established by ensuring that the virtual work done by the body force matches the [virtual work](@entry_id:176403) of the [surface traction](@entry_id:198058) for any admissible [virtual displacement](@entry_id:168781).

These methods are designed to be consistent with the classical theory, meaning they recover the standard local boundary conditions in the limit as $\delta \to 0$.

#### Asymptotic Compatibility

The connection between the nonlocal peridynamic model and classical continuum mechanics is formalized through the concept of **asymptotic compatibility (AC)**. It refers to the requirement that the discrete peridynamic solution must converge to the solution of the corresponding local partial differential equation as both the mesh size $h$ and the horizon $\delta$ approach zero.

This convergence is not guaranteed under arbitrary limits. It is crucial that the limits are taken in a coupled manner, specifically with the ratio $h/\delta \to 0$. This ensures that as the nonlocality vanishes, the discrete neighborhood of any point remains sufficiently populated for the [numerical quadrature](@entry_id:136578) to remain a consistent approximation of the integral operator. Failure to maintain this ratio can lead to a loss of accuracy or convergence to the wrong solution.

Achieving AC is particularly challenging on bounded domains and in [heterogeneous materials](@entry_id:196262). The aforementioned surface effect due to truncated horizons at boundaries breaks the symmetry of the [integral operator](@entry_id:147512), introducing a bias that prevents convergence unless a suitable boundary correction is applied. Similarly, at interfaces between different materials, standard [quadrature rules](@entry_id:753909) can fail, necessitating corrections that ensure the discrete operator can at least exactly reproduce affine (linear) fields, a fundamental condition for consistency. These numerical considerations are essential for validating peridynamic simulations and establishing their credentials as a robust [multiscale modeling](@entry_id:154964) tool.