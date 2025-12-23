## Introduction
Modeling [material failure](@entry_id:160997), particularly the initiation and propagation of discontinuities like cracks, has long been a central challenge in [computational solid mechanics](@entry_id:169583). Classical [continuum mechanics](@entry_id:155125), which relies on spatial derivatives of displacement fields, requires special numerical techniques and ad-hoc criteria to handle these singularities. Peridynamics offers a paradigm shift by reformulating the fundamental [equations of motion](@entry_id:170720) into a nonlocal, integral form. This elegant approach inherently accommodates discontinuities, allowing for the simulation of complex fracture and fragmentation processes within a single, unified framework. This article provides a graduate-level exploration of peridynamic theory, designed to build a deep understanding from first principles to advanced applications.

The journey begins in the "Principles and Mechanisms" chapter, where we will dissect the mathematical foundations of [peridynamics](@entry_id:191791), contrasting bond-based and state-based models and elucidating the core mechanism of [emergent fracture](@entry_id:748952) through bond breaking. Next, the "Applications and Interdisciplinary Connections" chapter will showcase the theory's power by exploring its use in diverse and complex scenarios, from modeling [ductile fracture](@entry_id:161045) and [composite delamination](@entry_id:196694) to simulating large-scale geophysical events like earthquakes and sea ice fracture. Finally, a series of "Hands-On Practices" will provide the opportunity to engage directly with key computational aspects of [peridynamics](@entry_id:191791), such as ensuring [numerical stability](@entry_id:146550) and performing [energy balance](@entry_id:150831) checks in dynamic fracture simulations. By the end, you will have a robust conceptual grasp of how [peridynamics](@entry_id:191791) provides a powerful and versatile tool for understanding and predicting material failure.

## Principles and Mechanisms

This chapter delves into the foundational principles and operative mechanisms of peridynamic theory. Building upon the introductory concepts, we will dissect the mathematical structure of peridynamic models, explore their relationship with classical continuum mechanics, and elucidate the elegant manner in which they describe the initiation and propagation of discontinuities such as cracks.

### The Governing Equation: An Integral Formulation

The cornerstone of [peridynamics](@entry_id:191791) is its reformulation of the [balance of linear momentum](@entry_id:193575). Whereas classical [continuum mechanics](@entry_id:155125) describes [internal forces](@entry_id:167605) through the spatial derivatives of a stress tensor, [peridynamics](@entry_id:191791) employs a nonlocal integral representation. For a material point at position $\boldsymbol{x}$ with mass density $\rho(\boldsymbol{x})$, the [equation of motion](@entry_id:264286) is expressed as an integro-differential equation:

$$
\rho(\boldsymbol{x})\ddot{\boldsymbol{u}}(\boldsymbol{x},t) = \int_{\mathcal{H}_{\boldsymbol{x}}} \boldsymbol{f}(\boldsymbol{u}(\boldsymbol{x}',t)-\boldsymbol{u}(\boldsymbol{x},t), \boldsymbol{x}, \boldsymbol{x}')\,\mathrm{d}V_{\boldsymbol{x}'} + \boldsymbol{b}(\boldsymbol{x},t)
$$

Here, $\boldsymbol{u}(\boldsymbol{x},t)$ is the displacement field, $\ddot{\boldsymbol{u}}$ is its second [material time derivative](@entry_id:190892) (acceleration), and $\boldsymbol{b}(\boldsymbol{x},t)$ is the external [body force](@entry_id:184443) density. The integral represents the net internal force density at $\boldsymbol{x}$, which is the sum of all **pairwise force densities**, $\boldsymbol{f}$, exerted by material points $\boldsymbol{x}'$ within a finite neighborhood of $\boldsymbol{x}$ known as the **horizon**, $\mathcal{H}_{\boldsymbol{x}}$. The horizon is typically a sphere of radius $\delta$, which serves as a fundamental [material length scale](@entry_id:197771).

The critical feature of this equation is that the pairwise force function $\boldsymbol{f}$ depends on the relative displacement, $\boldsymbol{u}(\boldsymbol{x}',t)-\boldsymbol{u}(\boldsymbol{x},t)$, rather than on spatial derivatives of the displacement field. This seemingly simple change has profound implications. The integral operator requires significantly less regularity from the displacement field $\boldsymbol{u}$ than a [differential operator](@entry_id:202628) does. For the integral to be well-defined, it is generally sufficient for $\boldsymbol{u}$ to be measurable, a condition that permits jump discontinuities. From a measure-theoretic standpoint, a discontinuity surface (like a crack) in a three-dimensional body is a two-dimensional manifold, which has zero Lebesgue measure with respect to the volume integral $\mathrm{d}V_{\boldsymbol{x}'}$. This means the integrand remains well-defined almost everywhere, and the integral itself does not produce the non-[integrable singularities](@entry_id:634345) that would arise from applying a [gradient operator](@entry_id:275922) ($\nabla \boldsymbol{u}$) to a discontinuous field. This [intrinsic property](@entry_id:273674) allows [peridynamics](@entry_id:191791) to model the formation and evolution of cracks without requiring special numerical techniques or ad-hoc [failure criteria](@entry_id:195168) applied at a crack tip .

### Bond-Based Peridynamics: A Foundational Model

The simplest and most intuitive peridynamic formulation is the **bond-based** model. In this framework, the interaction between any two material points is governed by a "bond" connecting them, and the force in this bond is independent of all other bonds.

Let the [relative position](@entry_id:274838) vector in the reference configuration be $\boldsymbol{\xi} = \boldsymbol{x}' - \boldsymbol{x}$. The pairwise force density is assumed to be **central**, meaning it acts along the direction of the bond:

$$
\boldsymbol{f}(\boldsymbol{x},\boldsymbol{x}',t) = c(|\boldsymbol{\xi}|) s(\boldsymbol{x},\boldsymbol{x}',t) \frac{\boldsymbol{\xi}}{|\boldsymbol{\xi}|}
$$

Here, $c(|\boldsymbol{\xi}|)$ is a non-negative scalar function called the **micromodulus**, which defines the stiffness of the bond and vanishes for $|\boldsymbol{\xi}| > \delta$. The term $s$ is the **bond stretch**, a scalar measure of the bond's elongation. For small deformations, it is defined as the projection of the relative displacement onto the bond direction, normalized by the initial [bond length](@entry_id:144592):

$$
s(\boldsymbol{x},\boldsymbol{x}',t) = \frac{(\boldsymbol{u}(\boldsymbol{x}',t) - \boldsymbol{u}(\boldsymbol{x},t)) \cdot \boldsymbol{\xi}}{|\boldsymbol{\xi}|^2}
$$

A key property of this formulation is that the pairwise forces are antisymmetric, $\boldsymbol{f}(\boldsymbol{x},\boldsymbol{x}',t) = -\boldsymbol{f}(\boldsymbol{x}',\boldsymbol{x},t)$, which is a direct expression of Newton's third law. This [antisymmetry](@entry_id:261893) ensures that the net internal force on any isolated body is zero, thus satisfying the global [balance of linear momentum](@entry_id:193575). Furthermore, because the forces are central, the net internal torque on any body is also identically zero. This means that the [balance of angular momentum](@entry_id:181848) is automatically satisfied without any additional constitutive constraints .

If the material is **microelastic**, the pairwise force can be derived from a scalar bond potential. For the linear model above, the [strain energy density](@entry_id:200085) $W$ at a point $\boldsymbol{x}$ can be expressed as:

$$
W(\boldsymbol{x},t) = \frac{1}{2} \int_{\mathcal{H}_{\boldsymbol{x}}} \frac{1}{2} c(|\boldsymbol{\xi}|) s(\boldsymbol{x},\boldsymbol{x}',t)^2 |\boldsymbol{\xi}|^2 \,\mathrm{d}V_{\boldsymbol{x}'}
$$

The factor of $1/2$ inside the integral accounts for the energy stored per bond, and the leading factor of $1/2$ outside accounts for the fact that each bond is shared by two points, preventing double-counting when integrating over the entire body .

Despite its elegance and simplicity, the bond-based model has a significant limitation. The central-force assumption imposes a constraint on the elastic properties of the material it can represent. When the model's response is compared to that of classical [isotropic linear elasticity](@entry_id:185899), the Lamé parameters $\lambda$ and $\mu$ are found to be constrained. This leads to a fixed value for Poisson's ratio, which is $\nu = 1/4$ in three dimensions and $\nu = 1/3$ in two dimensions. The model cannot, therefore, describe materials with other Poisson's ratios  .

### State-Based Peridynamics: A Generalization

To overcome the limitations of the bond-based model, a more general framework known as **state-based** [peridynamics](@entry_id:191791) was developed. In this formulation, the force in a given bond is allowed to depend on the collective deformation of all other bonds connected to the material point.

This is formalized by introducing the concepts of **states**. A **deformation state**, denoted $\mathbf{Y}$, is a function that maps each bond vector $\boldsymbol{\xi}$ in a point's horizon to its deformed counterpart, $\mathbf{Y}\langle\boldsymbol{\xi}\rangle = \boldsymbol{y}(\boldsymbol{x}+\boldsymbol{\xi},t) - \boldsymbol{y}(\boldsymbol{x},t)$, where $\boldsymbol{y}$ is the current position field. A **force state**, $\mathbf{T}$, is a vector-valued function that assigns a force density vector to each bond $\boldsymbol{\xi}$, denoted $\mathbf{T}\langle\boldsymbol{\xi}\rangle$. The [constitutive law](@entry_id:167255) is then a functional relationship between the deformation state and the force state: $\mathbf{T} = \mathcal{F}(\mathbf{Y})$.

The [equation of motion](@entry_id:264286) for [state-based peridynamics](@entry_id:190841) is written as:
$$
\rho(\boldsymbol{x})\ddot{\boldsymbol{u}}(\boldsymbol{x},t) = \int_{\mathcal{H}_{\boldsymbol{x}}} \left[ \mathbf{T}\langle\boldsymbol{\xi}\rangle(\boldsymbol{x},t) - \mathbf{T}\langle-\boldsymbol{\xi}\rangle(\boldsymbol{x}',t) \right] \,\mathrm{d}V_{\boldsymbol{x}'} + \boldsymbol{b}(\boldsymbol{x},t)
$$
The term $\mathbf{T}\langle-\boldsymbol{\xi}\rangle(\boldsymbol{x}',t)$ represents the reaction force exerted by $\boldsymbol{x}$ on $\boldsymbol{x}'$.

The crucial departure from the bond-based model is that the force vector $\mathbf{T}\langle\boldsymbol{\xi}\rangle$ is not required to be collinear with the bond vector $\boldsymbol{\xi}$. This allowance for **non-[central forces](@entry_id:267832)** breaks the geometric constraint that led to a fixed Poisson's ratio. As a result, state-based models can be calibrated to represent general [isotropic materials](@entry_id:170678) with any physically admissible Poisson's ratio, as well as [anisotropic materials](@entry_id:184874). However, this generality comes at a price: the [balance of angular momentum](@entry_id:181848) is no longer automatically satisfied. It must be enforced as an additional constitutive constraint on the force state, typically requiring that the net torque produced by the force state within any horizon is zero .

### Bridging Scales and Connecting to Classical Theory

A central theme in [peridynamics](@entry_id:191791) is the connection between its nonlocal, micro-structured description and the familiar world of macroscopic, classical continuum mechanics.

#### The Correspondence Principle

One powerful method for constructing state-based [constitutive models](@entry_id:174726) is the principle of **constitutive correspondence**. This principle provides a systematic way to use existing classical material models (e.g., from linear or [nonlinear elasticity](@entry_id:185743)) within the peridynamic framework. The core idea is to compute an effective, nonlocal [deformation gradient](@entry_id:163749) $\mathbf{F}$ at each point by finding the tensor that best maps the reference-configuration bonds to their deformed counterparts in a [least-squares](@entry_id:173916) sense .

For a point $\boldsymbol{x}$, this nonlocal deformation gradient $\mathbf{F}(\boldsymbol{x})$ is computed as:
$$
\mathbf{F}(\boldsymbol{x}) = \left( \int_{\mathcal{H}_{\boldsymbol{x}}} \omega(|\boldsymbol{\xi}|) \mathbf{Y}\langle\boldsymbol{\xi}\rangle \otimes \boldsymbol{\xi} \,\mathrm{d}V_{\boldsymbol{\xi}} \right) \mathbf{K}^{-1}(\boldsymbol{x})
$$
where $\omega(|\boldsymbol{\xi}|)$ is an [influence function](@entry_id:168646) weighting the contribution of different bonds, and $\mathbf{K}(\boldsymbol{x})$ is the **shape tensor**:
$$
\mathbf{K}(\boldsymbol{x}) = \int_{\mathcal{H}_{\boldsymbol{x}}} \omega(|\boldsymbol{\xi}|) \boldsymbol{\xi} \otimes \boldsymbol{\xi} \,\mathrm{d}V_{\boldsymbol{\xi}}
$$
Once $\mathbf{F}$ is known, one can compute a strain tensor (e.g., $\boldsymbol{\epsilon} = \frac{1}{2}(\mathbf{F}^T\mathbf{F} - \mathbf{I})$) and then use a classical [constitutive law](@entry_id:167255), such as Hooke's law $\boldsymbol{\sigma} = \mathbf{C} : \boldsymbol{\epsilon}$, to find a stress tensor. This stress is then used to define the peridynamic force state $\mathbf{T}$. This procedure allows the vast library of classical material models to be adapted for nonlocal simulations capable of handling discontinuities .

#### The Local Limit and Model Calibration

In regions where the deformation field is sufficiently smooth, the peridynamic operator should converge to the classical [differential operator](@entry_id:202628) as the horizon radius $\delta$ shrinks to zero. This consistency is crucial for the theory's validity. This convergence can be demonstrated by performing a Taylor [series expansion](@entry_id:142878) of the [displacement field](@entry_id:141476) within the peridynamic integral. For the limit to exist and match the form of the classical elasticity operator, certain conditions on the micromodulus kernel $c(|\boldsymbol{\xi}|)$ are required. Specifically, the kernel must be an even function to ensure that all odd-order terms in the expansion integrate to zero, and it must have a finite second moment to ensure that the leading-order contribution yields a well-defined second-order differential operator  .

This connection also provides a direct path for calibrating peridynamic models. By equating the peridynamic [strain energy density](@entry_id:200085) with the classical [strain energy density](@entry_id:200085) for a known deformation state, one can derive relationships between the microscopic parameters (like the micromodulus $c(r)$) and macroscopic [engineering constants](@entry_id:199413) (like the [bulk modulus](@entry_id:160069) $K$ and [shear modulus](@entry_id:167228) $\mu$). For instance, by considering a uniform hydrostatic expansion $u(\boldsymbol{x}) = \alpha \boldsymbol{x}$, one can derive the following expression for the [bulk modulus](@entry_id:160069) in a 3D bond-based model :

$$
K = \frac{2\pi}{9} \int_{0}^{\delta} c(r) r^4\, \mathrm{d}r
$$
Such relationships are essential for ensuring that a peridynamic simulation reproduces the correct macroscopic elastic behavior of a material.

### The Peridynamic Mechanism of Fracture

The most celebrated feature of [peridynamics](@entry_id:191791) is its ability to simulate complex fracture phenomena, such as crack initiation, branching, and [coalescence](@entry_id:147963), within a single, unified framework.

#### Emergent Cracks and Bond Breaking

In [peridynamics](@entry_id:191791), a crack is not a geometric entity that is explicitly inserted into the model. Instead, it is an **emergent phenomenon** that arises naturally from the evolution of material damage. Fracture is modeled by defining a failure criterion for each individual bond. A common and simple criterion is to assume that a bond breaks irreversibly if its stretch $s$ exceeds a **[critical stretch](@entry_id:200184)** $s_c$ . When a bond breaks, its ability to transmit force is permanently removed (i.e., its micromodulus $c$ is set to zero).

A crack, therefore, corresponds to a region of space where a sufficient number of bonds have broken. As damage accumulates, a path of broken bonds can form, effectively severing the mechanical connection between the two sides of the path. This creates a surface across which forces can no longer be transmitted, resulting in a naturally traction-free crack surface . This process can be visualized using a graph analogy: the material points are vertices, and the intact bonds are edges. Fracture corresponds to the removal of edges from the graph. When a set of edges forming a "cut" is removed, the graph becomes disconnected, just as the material separates to form a crack .

#### The Horizon as a Regularizing Length Scale

In classical Linear Elastic Fracture Mechanics (LEFM), the [stress and strain](@entry_id:137374) fields are singular at a sharp [crack tip](@entry_id:182807). The peridynamic horizon $\delta$ provides a natural length scale that regularizes this singularity. Because forces are computed by averaging interactions over the [finite volume](@entry_id:749401) of the horizon, the fields remain bounded everywhere, including at the tip of a crack. The horizon size $\delta$ is therefore not merely a numerical parameter but a constitutive length scale that characterizes the extent of the material's nonlocal behavior and is related to the size of the fracture **process zone**. A simplified analysis, which models the peridynamic energy at a [crack tip](@entry_id:182807) as an average of the singular LEFM energy over the horizon disk, reveals that the characteristic size of this process zone, $r_p$, is directly proportional to the horizon, with one estimate yielding $r_p = \delta/2$ .

Just as the [elastic moduli](@entry_id:171361) can be related to the micromodulus, the macroscopic fracture toughness of a material can be linked to the microscopic failure criterion. By equating the energy dissipated by breaking all bonds across a unit area with the material's critical energy release rate, or **[fracture energy](@entry_id:174458)** $G_c$, one can derive a relationship between $G_c$ and the [critical stretch](@entry_id:200184) $s_c$. For a 3D bond-based model, this relationship is :

$$
s_c = \sqrt{\frac{2 G_c}{\pi \int_0^\delta c(r) r^4 \mathrm{d}r}}
$$
This expression provides the final, crucial link needed to calibrate a peridynamic model for predictive simulations of [brittle fracture](@entry_id:158949).

### Advanced Topic: Volumetric Locking in Nearly Incompressible Materials

While peridynamic models offer powerful advantages, their numerical implementation can present challenges, particularly for materials that are [nearly incompressible](@entry_id:752387) (i.e., Poisson's ratio $\nu \to 0.5$). In this limit, the [bulk modulus](@entry_id:160069) becomes extremely large, leading to a severe energy penalty for any volumetric deformation. Numerical [discretization](@entry_id:145012), especially with the truncated integration domains near boundaries in correspondence models, can introduce spurious, non-zero volumetric strains even in deformations that should be purely volume-preserving, such as simple shear. This artifact leads to an unphysically stiff response known as **volumetric locking** .

This issue can be diagnosed by comparing the apparent [shear modulus](@entry_id:167228) computed from the strain energy in a [simple shear](@entry_id:180497) simulation to the true material [shear modulus](@entry_id:167228). An unphysically high apparent modulus indicates locking. Several advanced formulations have been developed to mitigate this problem:

*   **Stabilized Correspondence Models**: Inspired by the "B-bar" methods in [finite element analysis](@entry_id:138109), these models replace the problematic local volumetric strain at each point with a smoothed or averaged value over a larger domain. This averaging cancels out much of the spurious numerical noise, relaxing the volumetric constraint and reducing locking.

*   **Non-Ordinary State-Based (NOSB) Models**: A more direct approach is to reformulate the [constitutive law](@entry_id:167255) to be less sensitive to volumetric deformation. For instance, a model can be constructed based on a deviatoric-hydrostatic split of the energy, where the volumetric part is handled separately or, in some cases, ignored entirely for certain deformation modes. A deviatoric-only model, for example, computes [strain energy](@entry_id:162699) based only on the shape-changing part of the strain, making it inherently immune to volumetric locking artifacts .

These advanced techniques demonstrate the ongoing development of the peridynamic framework to address both fundamental physical representation and practical numerical performance.