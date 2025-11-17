## Introduction
Peridynamic solid mechanics represents a paradigm shift from classical theories, offering a powerful framework to analyze [material deformation](@entry_id:169356) and, most significantly, failure. Classical [continuum mechanics](@entry_id:155125), with its reliance on spatial derivatives, fundamentally breaks down at discontinuities like cracks, requiring complex and often ad-hoc criteria to model fracture. Peridynamics overcomes this limitation by reformulating the principles of mechanics using [integral equations](@entry_id:138643), which remain valid even in the presence of evolving discontinuities. This article provides a comprehensive exploration of this [nonlocal theory](@entry_id:752667) for graduate-level students and researchers.

Across the following chapters, you will build a robust understanding of this field. The "Principles and Mechanisms" chapter will lay the theoretical groundwork, detailing the unique [kinematics](@entry_id:173318), equation of motion, and [constitutive models](@entry_id:174726) that define [peridynamics](@entry_id:191791). Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate the theory's practical power, covering its use in fracture mechanics, plasticity, and [coupled multiphysics](@entry_id:747969) problems. Finally, the "Hands-On Practices" section will bridge theory and application through targeted exercises, solidifying your grasp of the core concepts.

## Principles and Mechanisms

This chapter elucidates the foundational principles and mechanical formulations that underpin peridynamic theory. We will transition from the conceptual introduction to a rigorous examination of the mathematical and physical constructs of [peridynamics](@entry_id:191791). Our inquiry begins with the fundamental kinematic quantities that distinguish [peridynamics](@entry_id:191791) from classical continuum mechanics. We will then formulate the equation of motion and explore a hierarchy of [constitutive models](@entry_id:174726), from the simple bond-based framework to the more general state-based correspondence models. Finally, we will investigate how [peridynamics](@entry_id:191791) provides a natural and powerful framework for modeling [material failure](@entry_id:160997) and fracture.

### Fundamental Kinematics: Bonds, Stretch, and the Horizon

Classical continuum mechanics describes deformation locally, through quantities such as the [deformation gradient tensor](@entry_id:150370), which is defined at a point. Peridynamics adopts a fundamentally different, nonlocal perspective. The kinematic description is not based on infinitesimal neighborhoods, but on finite-distance interactions between material points.

#### The Bond and Bond Stretch: A Nonlocal Measure of Deformation

In [peridynamics](@entry_id:191791), the primary kinematic object is the **bond**. For any two material points at reference positions $\mathbf{x}$ and $\mathbf{x}'$, the reference bond is the vector $\boldsymbol{\xi} = \mathbf{x}' - \mathbf{x}$. After deformation, these points move to new positions $\mathbf{y}(\mathbf{x}, t)$ and $\mathbf{y}(\mathbf{x}', t)$, and the deformed bond is the vector $\mathbf{y}(\mathbf{x}', t) - \mathbf{y}(\mathbf{x}, t)$. The change in length of this bond provides the fundamental measure of strain.

The **bond stretch**, denoted by $s$, is the fractional change in the bond's length:
$$
s = \frac{\|\mathbf{y}(\mathbf{x}',t) - \mathbf{y}(\mathbf{x},t)\| - \|\mathbf{x}' - \mathbf{x}\|}{\|\mathbf{x}' - \mathbf{x}\|}
$$
If we define the relative displacement as $\boldsymbol{\eta} = \mathbf{u}(\mathbf{x}',t) - \mathbf{u}(\mathbf{x},t)$, where $\mathbf{u}$ is the displacement field, the stretch can be written as:
$$
s = \frac{\|\boldsymbol{\xi} + \boldsymbol{\eta}\| - \|\boldsymbol{\xi}\|}{\|\boldsymbol{\xi}\|}
$$
This scalar quantity replaces the role of the strain tensor in classical mechanics. It is crucial to understand the conceptual differences between the bond stretch $s$ and the classical small strain tensor $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathsf{T}})$ [@problem_id:2667612].

*   **Objectivity and Frame Indifference**: The bond stretch $s$ is computed from the lengths of vectors, which are invariant under rigid-body rotations. Therefore, $s$ is an objective quantity, meaning it is automatically invariant under any superposed [rigid-body motion](@entry_id:265795), including finite rotations. In contrast, the classical small strain tensor $\boldsymbol{\varepsilon}$ is only invariant under *infinitesimal* rigid motions. For a finite rigid rotation, $\boldsymbol{\varepsilon}$ can be nonzero even though the body is unstrained and every bond stretch $s$ is zero. This makes the bond stretch a more robust measure for problems involving [large rotations](@entry_id:751151).

*   **Nonlocality**: The bond stretch $s$ intrinsically depends on the state of two distinct points, $\mathbf{x}$ and $\mathbf{x}'$, separated by a finite distance $\|\boldsymbol{\xi}\| > 0$. It is therefore a **nonlocal** measure. Conversely, $\boldsymbol{\varepsilon}$ is a **local** quantity, defined at a single point $\mathbf{x}$ via the [gradient operator](@entry_id:275922), which involves a limiting process as the neighborhood shrinks to zero.

*   **Large Deformations**: The definition of $s$ involves no linearization or assumption of small deformation. It is a purely geometric measure that remains valid for arbitrarily [large strains](@entry_id:751152) and rotations. The small strain tensor $\boldsymbol{\varepsilon}$, by its very definition, is a linearized measure valid only when the displacement gradients are much smaller than unity.

*   **Correspondence with Classical Strain**: Despite their differences, a correspondence exists in the limit of small deformations. For a smooth displacement field $\mathbf{u}$, a Taylor series expansion reveals that to a leading order, the bond stretch is related to the classical strain tensor by:
    $$
    s \approx \mathbf{n} \cdot \boldsymbol{\varepsilon}(\mathbf{x},t) \mathbf{n}
    $$
    where $\mathbf{n} = \boldsymbol{\xi}/\|\boldsymbol{\xi}\|$ is the unit vector in the direction of the reference bond. This shows that for small strains, the bond stretch approximates the normal component of the classical strain tensor along the bond's direction [@problem_id:2667612]. This relationship is a crucial "[correspondence principle](@entry_id:148030)" that allows peridynamic material parameters to be related to classical [elastic moduli](@entry_id:171361). An important consequence of this relationship is that, to first order, the stretch $s$ is insensitive to relative displacements perpendicular to the bond. A small tangential relative displacement changes the [bond length](@entry_id:144592) only at second order, a feature that has profound implications for the constitutive behavior of simple peridynamic models.

#### The Peridynamic Horizon: Defining the Scale of Nonlocality

In peridynamic theory, a material point at $\mathbf{x}$ does not interact with all other points in the body. Instead, interactions are confined to a neighborhood called the **peridynamic family** or **horizon**, typically a ball of radius $\delta$ centered at $\mathbf{x}$:
$$
\mathcal{H}_{\mathbf{x}} = \{ \mathbf{x}' \in \text{Body} : \|\mathbf{x}' - \mathbf{x}\| \le \delta \}
$$
The radius $\delta$ is a fundamental material parameter known as the **horizon**. It defines the length scale of nonlocality. The force at a point $\mathbf{x}$ depends on the collective motion of all points within its horizon.

The horizon is not a numerical artifact; it is an [intrinsic length scale](@entry_id:750789) of the material model itself [@problem_id:2667647]. This has several important consequences:
1.  **Spatial Filtering**: The integral formulation of [peridynamics](@entry_id:191791) (discussed below) effectively acts as a spatial [low-pass filter](@entry_id:145200). It averages information over the volume of the horizon. As a result, deformation fields with characteristic wavelengths significantly smaller than $\delta$ are naturally smoothed out or attenuated. This phenomenon, known as **dispersion**, is a physical characteristic of nonlocal media and is absent in classical local elasticity.
2.  **Model vs. Discretization**: One must distinguish the physical model parameter $\delta$ from the [numerical discretization](@entry_id:752782) parameter, such as the nodal spacing $h$ in a meshfree implementation. Refining the [discretization](@entry_id:145012) (making $h \to 0$) leads to a more accurate numerical solution of the peridynamic integral equation for a *fixed* $\delta$. However, it cannot remove the intrinsic nonlocal averaging effect over the scale $\delta$. Features smaller than the horizon cannot be resolved, regardless of how fine the [numerical discretization](@entry_id:752782) is.
3.  **Local Limit**: Classical local elasticity can be recovered as a special case. If the peridynamic constitutive parameters are scaled appropriately with $\delta$, the governing [integral equation](@entry_id:165305) converges to the classical partial differential equation of elasticity in the limit as $\delta \to 0$ for sufficiently smooth deformation fields. This confirms that [peridynamics](@entry_id:191791) is a generalization of, and consistent with, classical theory.

#### Kinematics at Discontinuities: A Departure from Classical Theory

A principal advantage of the peridynamic formulation is its ability to handle discontinuities, such as cracks, without mathematical difficulty. In classical mechanics, the deformation gradient $\nabla\mathbf{y}$ is undefined at a surface where the [displacement field](@entry_id:141476) has a [jump discontinuity](@entry_id:139886). The local theory fundamentally breaks down at a crack tip or a crack face.

Peridynamics, however, remains robust [@problem_id:2667608]. Consider a bond $\boldsymbol{\xi}$ that connects two points $\mathbf{x}$ and $\mathbf{x}'$ on opposite sides of a crack. Even though the [displacement field](@entry_id:141476) is discontinuous, the displacements $\mathbf{u}(\mathbf{x})$ and $\mathbf{u}(\mathbf{x}')$ are themselves well-defined finite values. Consequently, the relative displacement $\boldsymbol{\eta}$ and the bond stretch $s$ can be computed directly and remain finite. The nonlocal kinematic description does not require spatial [differentiability](@entry_id:140863) of the [displacement field](@entry_id:141476).

The collection of all bond deformations $\boldsymbol{\eta}(\mathbf{x}, \mathbf{x}')$ for $\mathbf{x}' \in \mathcal{H}_{\mathbf{x}}$ provides a rich, directionally-dependent description of the [kinematics](@entry_id:173318), even at a discontinuity. This description naturally incorporates the displacement jump across the crack. Unlike the classical theory which loses all kinematic information at the discontinuity, the peridynamic description retains a complete picture of the relative motions of neighboring points [@problem_id:2667608] [@problem_id:2667612]. This inherent ability to accommodate discontinuities is what makes [peridynamics](@entry_id:191791) an exceptionally powerful tool for modeling fracture.

### The Peridynamic Equation of Motion

The dynamics of a peridynamic body are governed by an integro-differential equation that represents the [balance of linear momentum](@entry_id:193575). For a material point at position $\mathbf{x}$, Newton's second law is expressed as:
$$
\rho(\mathbf{x}) \ddot{\mathbf{u}}(\mathbf{x}, t) = \int_{\mathcal{H}_{\mathbf{x}}} \mathbf{f}(\mathbf{u}(\mathbf{x}', t) - \mathbf{u}(\mathbf{x},t), \mathbf{x}' - \mathbf{x}) \, dV_{\mathbf{x}'} + \mathbf{b}(\mathbf{x}, t)
$$
Here, $\rho$ is the mass density, $\ddot{\mathbf{u}}$ is the [local acceleration](@entry_id:272847), and $\mathbf{b}$ is an external body force density (like gravity). The integral term represents the net internal force on the point $\mathbf{x}$ resulting from its interactions with all other points $\mathbf{x}'$ within its horizon.

The function $\mathbf{f}$ is the **pairwise force function**. It specifies the force vector that a point at $\mathbf{x}'$ exerts on a point at $\mathbf{x}$ per unit volume squared. This function encapsulates the material's constitutive response. Newton's third law requires that the force be equal and opposite, i.e., $\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = -\mathbf{f}(-\boldsymbol{\eta}, -\boldsymbol{\xi})$. The various peridynamic models are distinguished by their choice for this constitutive function $\mathbf{f}$.

### Constitutive Models: A Hierarchy of Material Response

The predictive power of [peridynamics](@entry_id:191791) lies in its [constitutive models](@entry_id:174726), which relate the forces between particles to their relative deformation. A hierarchy of models exists, ranging from simple central-force laws to general state-based formulations capable of capturing complex material behaviors.

#### Bond-Based Peridynamics: The Central Force Model

The simplest and most intuitive peridynamic model is the **bond-based** microelastic model [@problem_id:2667588]. In this formulation, the interaction between any two points is independent of all other points. The material is envisioned as a lattice of interacting particles. For an [isotropic material](@entry_id:204616), the pairwise interaction must be derivable from a micro-potential $\omega$ that depends only on the scalar bond stretch $s$. This leads to a **[central force](@entry_id:160395)** law: the interaction force must act along the line connecting the two points in their deformed positions.

The pairwise force function takes the form:
$$
\mathbf{f}(\boldsymbol{\eta}, \boldsymbol{\xi}) = c(\|\boldsymbol{\xi}\|) s \, \frac{\boldsymbol{\xi} + \boldsymbol{\eta}}{\|\boldsymbol{\xi} + \boldsymbol{\eta}\|}
$$
Here, $s$ is the bond stretch, the vector fraction is the [unit vector](@entry_id:150575) along the deformed bond, and $c(\|\boldsymbol{\xi}\|)$ is a positive scalar function called the **micromodulus**, which determines the stiffness of the bond. For a homogeneous and [isotropic material](@entry_id:204616), the micromodulus can only depend on the initial bond length $\|\boldsymbol{\xi}\|$.

While simple and computationally efficient, the bond-based model has a significant limitation. The assumption of [central forces](@entry_id:267832), where bonds offer no resistance to relative rotation, severely constrains the elastic properties of the material. For a linear elastic, isotropic, 3D material modeled this way, the Poisson's ratio is fixed at $\nu = 1/4$ (or $\nu = 1/3$ in 2D). This limitation prevents the modeling of many common materials and motivates the development of more general state-based models.

#### State-Based Peridynamics: A More General Framework

To overcome the limitations of the bond-based approach, **state-based** [peridynamics](@entry_id:191791) was developed. In this framework, the force in a bond is allowed to depend on the collective deformation of all bonds within the horizon. This is accomplished by introducing the concept of a **state**. A peridynamic state is a function that operates on the family of bonds within a horizon.

The [equation of motion](@entry_id:264286) is rewritten using force states $\mathbf{T}$:
$$
\rho(\mathbf{x}) \ddot{\mathbf{u}}(\mathbf{x}, t) = \int_{\mathcal{H}_{\mathbf{x}}} (\mathbf{T}(\mathbf{x}, t)\langle\boldsymbol{\xi}\rangle - \mathbf{T}(\mathbf{x}', t)\langle-\boldsymbol{\xi}\rangle) \, dV_{\mathbf{x}'} + \mathbf{b}(\mathbf{x}, t)
$$
Here, $\mathbf{T}(\mathbf{x}, t)\langle\boldsymbol{\xi}\rangle$ is the force state at point $\mathbf{x}$, representing the force density exerted by the bond $\boldsymbol{\xi}$. State-based models are categorized as ordinary or non-ordinary.

##### Ordinary State-Based Models: Independent Control of Bulk and Shear Response

In **ordinary state-based** models, the force state vector $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ is still constrained to be collinear with the bond vector, just as in bond-based models. However, its magnitude can now depend on the collective deformation of the entire neighborhood. This added freedom is sufficient to overcome the fixed Poisson's ratio problem [@problem_id:2667632].

A common approach is to decompose the deformation into volumetric (dilatational) and deviatoric (distortional) parts, analogous to classical elasticity. One defines a scalar measure of local volume change, the **dilatation** $\theta(\mathbf{x})$, as a weighted average of the extensions of all bonds in the horizon. The extension of each bond is then decomposed into a spherical part contributing to this dilatation and a deviatoric part $e^d$ representing shape change [@problem_id:2667635].

The force state can then be constructed as a sum of two contributions, one driven by the collective dilatation $\theta(\mathbf{x})$ and the other by the bond's individual deviatoric extension $e^d$, each scaled by independent [elastic moduli](@entry_id:171361) (e.g., [bulk modulus](@entry_id:160069) $\kappa$ and [shear modulus](@entry_id:167228) $\mu$). A typical form for the force state is:
$$
\mathbf{T}(\mathbf{x})\langle \boldsymbol{\xi} \rangle = \left[ k_{\text{vol}} \kappa \theta(\mathbf{x}) + k_{\text{dev}} \mu e^d(\mathbf{x}, \boldsymbol{\xi}) \right] \frac{\boldsymbol{\xi}}{\|\boldsymbol{\xi}\|}
$$
where $k_{\text{vol}}$ and $k_{\text{dev}}$ are coefficients involving influence functions and bond geometry. Because this model includes two independent moduli, $\kappa$ and $\mu$, it can represent any physically admissible Poisson's ratio, providing a significant improvement in generality over the bond-based formulation [@problem_id:2667632].

##### Non-Ordinary State-Based Models: The Correspondence Principle

The most general formulation is the **non-ordinary state-based** model. This approach abandons the constraint that forces must be collinear with bonds. The force state $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ can now point in any direction, allowing for the modeling of shear forces at the bond level. This is achieved through a **[correspondence principle](@entry_id:148030)**, which directly links the peridynamic formulation to classical continuum mechanics [@problem_id:2667661] [@problem_id:2667635].

The procedure involves three steps:
1.  **Define a Nonlocal Deformation Gradient**: At each point $\mathbf{x}$, a nonlocal [deformation gradient](@entry_id:163749) $\mathbf{F}(\mathbf{x})$ is computed. This tensor is the best [linear map](@entry_id:201112) that transforms reference bonds $\boldsymbol{\xi}$ to deformed bonds $\mathbf{Y}\langle\boldsymbol{\xi}\rangle$ in a weighted, [least-squares](@entry_id:173916) sense over the horizon.
2.  **Apply a Classical Constitutive Law**: With the deformation gradient $\mathbf{F}(\mathbf{x})$ available, *any* standard constitutive law from classical continuum mechanics can be used to compute a corresponding stress tensor, such as the first Piola-Kirchhoff stress $\mathbf{P}(\mathbf{x})$. This is where arbitrary material behavior, including any Poisson's ratio, is introduced.
3.  **Map Stress back to Force State**: The classical stress $\mathbf{P}(\mathbf{x})$ is then mapped back to a peridynamic force state $\mathbf{T}\langle\boldsymbol{\xi}\rangle$. This mapping is constructed to ensure that the peridynamic [equation of motion](@entry_id:264286) converges to the classical one in the appropriate limit.

The resulting force state has the form:
$$
\mathbf{T}(\mathbf{x})\langle \boldsymbol{\xi} \rangle = \omega(\|\boldsymbol{\xi}\|) \, \mathbf{P}(\mathbf{x}) \, \mathbf{K}^{-1}(\mathbf{x}) \, \boldsymbol{\xi}
$$
Here, $\omega$ is an [influence function](@entry_id:168646) and $\mathbf{K}(\mathbf{x})$ is the **shape tensor**, defined as $\mathbf{K}(\mathbf{x}) = \int_{\mathcal{H}_{\mathbf{x}}} \omega(\|\boldsymbol{\xi}\|) \boldsymbol{\xi} \otimes \boldsymbol{\xi} \, dV_{\boldsymbol{\xi}'}$. The shape tensor captures the geometry of the horizon and appropriately weights the contribution of each bond. For a spherical horizon and constant [influence function](@entry_id:168646), this tensor becomes a scalar multiple of the identity, simplifying calculations. For a unit-radius horizon in 3D with $\omega=1$, the shape tensor is $\mathbf{K} = \frac{4\pi}{15}\mathbf{I}$, and its inverse is $\mathbf{K}^{-1} = \frac{15}{4\pi}\mathbf{I}$ [@problem_id:2667621].

This correspondence framework is extremely powerful, as it allows the vast library of existing classical [constitutive models](@entry_id:174726) to be directly incorporated into the nonlocal peridynamic framework, enabling the simulation of complex material responses while retaining the ability to model fracture.

### Modeling Material Failure: The Peridynamic Approach to Fracture

The ability to model fracture initiation and propagation is arguably the most compelling feature of [peridynamics](@entry_id:191791). In this framework, fracture is not a special case requiring extra criteria; it is a natural outcome of the underlying mechanics.

#### Damage as Irreversible Bond Breaking

Damage is modeled through the irreversible breaking of bonds [@problem_id:2667586]. A simple and effective failure criterion is based on a **[critical stretch](@entry_id:200184)**, $s_c$. A bond between points $\mathbf{x}$ and $\mathbf{x}'$ is assumed to break permanently if its stretch $s$ ever exceeds this critical value.

To enforce irreversibility, the failure condition must depend on the entire loading history. A history-dependent bond status variable, $\mu(\mathbf{x}, \mathbf{x}', t)$, is introduced:
$$
\mu(\mathbf{x}, \mathbf{x}', t) = 
\begin{cases}
1  & \text{if } s(\mathbf{x}, \mathbf{x}', \tau) \le s_c \text{ for all } \tau \le t \\
0  & \text{otherwise}
\end{cases}
$$
A bond is intact if $\mu=1$ and broken if $\mu=0$. Once $\mu$ switches to 0, it can never return to 1. The pairwise force function is then modified to reflect this status:
$$
\mathbf{f}_{\text{damage}} = \mu(\mathbf{x}, \mathbf{x}', t) \cdot \mathbf{f}_{\text{intact}}
$$
When a bond breaks, its ability to carry force is eliminated. A crack is simply a surface where a sufficient number of bonds have broken. Local damage at a point $\mathbf{x}$ can be quantified as the weighted fraction of broken bonds within its horizon.

This process is inherently dissipative. When a bond breaks at stretch $s_c$, the elastic energy stored within it is released. This energy release is consistent with the energy required to create new fracture surfaces, as described by [fracture mechanics](@entry_id:141480).

#### Energetic Consistency and the Critical Stretch Criterion

While conceptually simple, choosing the [critical stretch](@entry_id:200184) $s_c$ as a constant material property leads to an issue: the predicted macroscopic [fracture toughness](@entry_id:157609) of the material becomes dependent on the choice of the horizon radius $\delta$ [@problem_id:2667609]. A larger horizon means more bonds cross a potential crack plane, and if each breaks at the same stretch $s_c$, the total energy release (and thus the peak load) will increase with $\delta$. This makes the model physically inconsistent, as [fracture energy](@entry_id:174458) should be an intrinsic material property.

To resolve this, $s_c$ must be related to the macroscopic [fracture energy](@entry_id:174458), $G_c$ (for Mode I fracture), and the horizon $\delta$. The fracture energy $G_c$ is the energy required to create a unit area of new crack surface. In [peridynamics](@entry_id:191791), this corresponds to the total elastic energy stored in all bonds that cross a unit area of the crack plane at the instant of failure.

The energy stored in a bond just before breaking is proportional to $c(\|\boldsymbol{\xi}\|)s_c^2$. Equating the integral of this energy over all breaking bonds to $G_c$ yields a relationship of the form:
$$
G_c = \frac{1}{2} s_c^2 \cdot A(\delta)
$$
where $A(\delta)$ is an integral that depends on the micromodulus $c$ and the geometry of the horizon $\delta$. This allows us to define a horizon-dependent [critical stretch](@entry_id:200184):
$$
s_c(\delta) = \sqrt{\frac{2 G_c}{A(\delta)}}
$$
By using this energy-based criterion, the peridynamic model is calibrated to reproduce a specific, measurable macroscopic fracture property, $G_c$, regardless of the choice of the model parameter $\delta$. This makes the simulation results objective and physically meaningful, providing a robust link between the microscopic parameters of [peridynamics](@entry_id:191791) and the macroscopic principles of fracture mechanics.