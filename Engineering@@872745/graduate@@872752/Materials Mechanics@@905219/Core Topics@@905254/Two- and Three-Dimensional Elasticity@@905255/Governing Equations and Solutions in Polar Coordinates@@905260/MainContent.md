## Introduction
The analysis of [stress and strain](@entry_id:137374) within components featuring curved boundaries—such as pressure vessels, plates with holes, or rotating disks—presents a challenge for standard Cartesian coordinates. To accurately model the mechanical behavior of these common engineering structures, it is essential to adopt a coordinate system that aligns with their geometry. The [polar coordinate system](@entry_id:174894) provides the natural framework for such two-dimensional problems, but this requires a complete reformulation of the fundamental principles of continuum mechanics. The familiar equations for strain, equilibrium, and stress must be re-derived to account for the curvature and position-dependent nature of the polar basis.

This article provides a comprehensive guide to mastering elasticity in polar coordinates. We will bridge the gap between abstract principles and practical application by methodically deriving the governing equations and demonstrating their power in solving real-world problems. Across the following chapters, you will gain a deep, analytical understanding of this critical topic in [materials mechanics](@entry_id:189503). The journey begins in **Principles and Mechanisms**, where we will derive the strain-displacement, equilibrium, and [constitutive equations](@entry_id:138559) from first principles, leading to the elegant Airy stress function formulation and the general Michell solution. Next, **Applications and Interdisciplinary Connections** will showcase how this framework is used to solve canonical problems in structural engineering and fracture mechanics, while also highlighting its connections to [thermoelasticity](@entry_id:158447), heat transfer, and fluid dynamics. Finally, **Hands-On Practices** will offer a set of guided problems to reinforce these concepts and build your analytical problem-solving skills.

## Principles and Mechanisms

The analysis of [stress and strain](@entry_id:137374) in bodies with curved geometries, such as plates with holes, curved beams, or pressure vessels, is most naturally undertaken using a coordinate system that aligns with the geometry. The [polar coordinate system](@entry_id:174894) provides the canonical framework for such two-dimensional problems. While the fundamental principles of continuum mechanics—[kinematics](@entry_id:173318), equilibrium, and constitutive behavior—remain invariant, their mathematical expression changes significantly when moving from a Cartesian to a polar framework. This chapter elucidates these governing equations and lays out the systematic analytical methodology for solving plane elasticity problems in [polar coordinates](@entry_id:159425).

### The Geometric Foundation of Polar Coordinates

In contrast to the fixed, globally constant basis vectors of a Cartesian system, the [polar coordinate system](@entry_id:174894) is founded upon a **local and position-dependent basis**. This distinction is the ultimate source of the additional terms that appear in the governing equations of elasticity. Let the position of a point in a plane be described by the Cartesian coordinates $(x, y)$ or the [polar coordinates](@entry_id:159425) $(r, \theta)$, related by the transformation $x = r\cos\theta$ and $y = r\sin\theta$. The [position vector](@entry_id:168381) is $\mathbf{r} = x\mathbf{i} + y\mathbf{j} = r\cos\theta\,\mathbf{i} + r\sin\theta\,\mathbf{j}$.

The [local basis vectors](@entry_id:163370) in a curvilinear system are defined by the [partial derivatives](@entry_id:146280) of the position vector with respect to the coordinates. In our case, these are the **[covariant basis](@entry_id:198968) vectors**, $\mathbf{a}_r$ and $\mathbf{a}_\theta$.

$\mathbf{a}_r = \dfrac{\partial \mathbf{r}}{\partial r} = \cos\theta\,\mathbf{i} + \sin\theta\,\mathbf{j}$

$\mathbf{a}_\theta = \dfrac{\partial \mathbf{r}}{\partial \theta} = -r\sin\theta\,\mathbf{i} + r\cos\theta\,\mathbf{j}$

For formulating physical laws, it is more convenient to work with a set of orthonormal (unit and mutually perpendicular) basis vectors. These are obtained by normalizing the [covariant basis](@entry_id:198968) vectors. The lengths of the [covariant vectors](@entry_id:263917), known as **[scale factors](@entry_id:266678)** $h_i$, are found from the diagonal components of the **metric tensor**, $g_{ij} = \mathbf{a}_i \cdot \mathbf{a}_j$.

$g_{rr} = \mathbf{a}_r \cdot \mathbf{a}_r = \cos^2\theta + \sin^2\theta = 1 \implies h_r = \sqrt{g_{rr}} = 1$

$g_{\theta\theta} = \mathbf{a}_\theta \cdot \mathbf{a}_\theta = r^2\sin^2\theta + r^2\cos^2\theta = r^2 \implies h_\theta = \sqrt{g_{\theta\theta}} = r$

$g_{r\theta} = \mathbf{a}_r \cdot \mathbf{a}_\theta = -r\cos\theta\sin\theta + r\sin\theta\cos\theta = 0$

The vanishing of the off-diagonal component $g_{r\theta}$ confirms that the [polar coordinate system](@entry_id:174894) is orthogonal. The [orthonormal basis](@entry_id:147779) vectors, denoted $\mathbf{e}_r$ and $\mathbf{e}_\theta$, are then given by $\mathbf{e}_i = \mathbf{a}_i / h_i$. [@problem_id:2889560]

$\mathbf{e}_r = \dfrac{\mathbf{a}_r}{h_r} = \cos\theta\,\mathbf{i} + \sin\theta\,\mathbf{j}$

$\mathbf{e}_\theta = \dfrac{\mathbf{a}_\theta}{h_\theta} = -\sin\theta\,\mathbf{i} + \cos\theta\,\mathbf{j}$

Crucially, both $\mathbf{e}_r$ and $\mathbf{e}_\theta$ are functions of the [angular position](@entry_id:174053) $\theta$. As one moves around a circle of constant radius, the directions of "radially outward" and "tangential" continuously change. This spatial variation is captured by the derivatives of the basis vectors:

$\dfrac{\partial \mathbf{e}_r}{\partial \theta} = -\sin\theta\,\mathbf{i} + \cos\theta\,\mathbf{j} = \mathbf{e}_\theta$

$\dfrac{\partial \mathbf{e}_\theta}{\partial \theta} = -\cos\theta\,\mathbf{i} - \sin\theta\,\mathbf{j} = -\mathbf{e}_r$

The derivatives with respect to $r$ are zero. These non-vanishing derivatives are the geometric source of the "extra" terms in the polar coordinate expressions for strain and equilibrium. They are a manifestation of the **curvature** of the coordinate lines and are formally quantified by **Christoffel symbols**, which represent the components of the derivatives of basis vectors in terms of the basis itself. For instance, $\Gamma^r_{\theta\theta} = -r$ and $\Gamma^\theta_{r\theta} = 1/r$. In Cartesian coordinates, all Christoffel symbols vanish because the basis is constant. [@problem_id:2889560]

### Governing Equations in Polar Coordinates

The three pillars of [linear elasticity](@entry_id:166983) theory—kinematics, equilibrium, and [constitutive relations](@entry_id:186508)—are now formulated in this curvilinear framework.

#### Kinematics: The Strain-Displacement Relations

The **[small-strain tensor](@entry_id:754968)**, $\boldsymbol{\varepsilon}$, is the symmetric part of the [displacement gradient](@entry_id:165352), $\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla\mathbf{u} + (\nabla\mathbf{u})^T)$. To find its components in [polar coordinates](@entry_id:159425), we must correctly compute the gradient of the displacement field $\mathbf{u} = u_r(r,\theta)\mathbf{e}_r + u_\theta(r,\theta)\mathbf{e}_\theta$. The [gradient operator](@entry_id:275922) in [polar coordinates](@entry_id:159425) is $\nabla = \mathbf{e}_r \frac{\partial}{\partial r} + \mathbf{e}_\theta \frac{1}{r} \frac{\partial}{\partial \theta}$.

When applying this operator to $\mathbf{u}$, the product rule must be used, and the derivatives of the basis vectors must be included:
$\nabla\mathbf{u} = \left(\mathbf{e}_r \frac{\partial}{\partial r} + \mathbf{e}_\theta \frac{1}{r} \frac{\partial}{\partial \theta}\right) \otimes (u_r\mathbf{e}_r + u_\theta\mathbf{e}_\theta)$

Expanding this expression and collecting terms reveals the components of the [displacement gradient tensor](@entry_id:748571), from which the strain components are derived. A key calculation involves the derivative with respect to $\theta$:
$\dfrac{1}{r} \dfrac{\partial \mathbf{u}}{\partial \theta} = \dfrac{1}{r} \left( \dfrac{\partial u_r}{\partial \theta}\mathbf{e}_r + u_r \dfrac{\partial \mathbf{e}_r}{\partial \theta} + \dfrac{\partial u_\theta}{\partial \theta}\mathbf{e}_\theta + u_\theta \dfrac{\partial \mathbf{e}_\theta}{\partial \theta} \right) = \dfrac{1}{r} \left( \dfrac{\partial u_r}{\partial \theta}\mathbf{e}_r + u_r\mathbf{e}_\theta + \dfrac{\partial u_\theta}{\partial \theta}\mathbf{e}_\theta - u_\theta\mathbf{e}_r \right)$

After performing the full derivation and taking the symmetric part, we arrive at the [strain-displacement relations](@entry_id:173321): [@problem_id:2889564]

The **radial [normal strain](@entry_id:204633)**, $\varepsilon_{rr}$, measures the stretching of a line element in the radial direction:
$\varepsilon_{rr} = \dfrac{\partial u_r}{\partial r}$

The **hoop (or tangential) [normal strain](@entry_id:204633)**, $\varepsilon_{\theta\theta}$, measures the stretching of a circumferential line element. It has two contributions: one from the change in the tangential displacement $u_\theta$ along the circumference, and another from radial displacement $u_r$, which increases the circumference of a circle:
$\varepsilon_{\theta\theta} = \dfrac{1}{r}\dfrac{\partial u_\theta}{\partial \theta} + \dfrac{u_r}{r}$

The **shear strain**, $\varepsilon_{r\theta}$, measures the change in angle between initially orthogonal radial and tangential lines. The term $-\frac{u_\theta}{r}$ arises directly from the change in the basis vectors:
$\varepsilon_{r\theta} = \dfrac{1}{2}\left( \dfrac{1}{r}\dfrac{\partial u_r}{\partial \theta} + \dfrac{\partial u_\theta}{\partial r} - \dfrac{u_\theta}{r} \right)$

#### Kinetics: The Static Equilibrium Equations

The local [balance of linear momentum](@entry_id:193575), $\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}$, expresses that the [net force](@entry_id:163825) on any infinitesimal volume of material must be zero in a static state. Here, $\boldsymbol{\sigma}$ is the Cauchy stress tensor and $\mathbf{b}$ is the [body force](@entry_id:184443) per unit volume.

Deriving the component form of this equation in [polar coordinates](@entry_id:159425) is most intuitively done by considering force balance on a differential element bounded by $r$, $r+dr$, $\theta$, and $\theta+d\theta$. The curvature of this element is responsible for the additional terms. Summing the forces from tractions on each face and the [body force](@entry_id:184443), and then projecting the sum onto the local $\mathbf{e}_r$ and $\mathbf{e}_\theta$ directions, yields two scalar equations. [@problem_id:2889545]

The [equilibrium equation](@entry_id:749057) in the **radial direction** is:
$\dfrac{\partial \sigma_{rr}}{\partial r} + \dfrac{1}{r}\dfrac{\partial \sigma_{r\theta}}{\partial \theta} + \dfrac{\sigma_{rr}-\sigma_{\theta\theta}}{r} + b_r = 0$
The term $\frac{\sigma_{rr}-\sigma_{\theta\theta}}{r}$ arises because the radial directions on the two tangential faces of the element are not parallel; their slight angle means that the [hoop stress](@entry_id:190931) $\sigma_{\theta\theta}$ contributes a [net force](@entry_id:163825) component in the radial direction.

The [equilibrium equation](@entry_id:749057) in the **tangential direction** is:
$\dfrac{\partial \sigma_{r\theta}}{\partial r} + \dfrac{1}{r}\dfrac{\partial \sigma_{\theta\theta}}{\partial \theta} + \dfrac{2\sigma_{r\theta}}{r} + b_\theta = 0$
The term $\frac{2\sigma_{r\theta}}{r}$ has two origins: one from the radial variation of [shear force](@entry_id:172634) on a larger area at larger $r$, and another from the projection of the [radial stress](@entry_id:197086) $\sigma_{r\theta}$ onto the local tangential direction, which changes with $\theta$.

#### Constitutive Law for Isotropic Materials

For a homogeneous, isotropic, linearly elastic material, the stress-strain relationship is given by Hooke's Law. In its general tensor form, $\boldsymbol{\sigma} = \lambda(\text{tr}\,\boldsymbol{\varepsilon})\mathbf{I} + 2\mu\boldsymbol{\varepsilon}$, where $\lambda$ and $\mu$ are the **Lamé constants**. A fundamental property of [isotropic tensors](@entry_id:195105) is that their component form is identical in any orthonormal basis. Therefore, this relationship holds directly for the physical components in the polar basis $\{ \mathbf{e}_r, \mathbf{e}_\theta, \mathbf{e}_z \}$.

For the important case of **[plane strain](@entry_id:167046)**, we impose the kinematic constraint that all strain components involving the $z$-direction are zero: $\varepsilon_{zz} = \varepsilon_{rz} = \varepsilon_{\theta z} = 0$. The trace of the [strain tensor](@entry_id:193332) (volumetric strain) simplifies to $\text{tr}\,\boldsymbol{\varepsilon} = \varepsilon_{rr} + \varepsilon_{\theta\theta}$. Substituting this into Hooke's Law gives the in-plane [constitutive relations](@entry_id:186508): [@problem_id:2889573]

$\sigma_{rr} = \lambda(\varepsilon_{rr}+\varepsilon_{\theta\theta}) + 2\mu \varepsilon_{rr}$

$\sigma_{\theta\theta} = \lambda(\varepsilon_{rr}+\varepsilon_{\theta\theta}) + 2\mu \varepsilon_{\theta\theta}$

$\sigma_{r\theta} = 2\mu \varepsilon_{r\theta}$

It is essential to note that under plane strain, a non-zero out-of-plane stress $\sigma_{zz}$ is required to maintain the $\varepsilon_{zz}=0$ constraint:
$\sigma_{zz} = \lambda(\varepsilon_{rr}+\varepsilon_{\theta\theta})$

### Formulations and Solution Strategies

Having established the set of governing equations, the next step is to formulate a strategy for solving them. A direct, displacement-based approach is possible, but a stress-based formulation is often more powerful for analytical solutions.

#### Equilibrium and Compatibility

A central challenge in elasticity is that the problem is **statically indeterminate**: the [equilibrium equations](@entry_id:172166) provide only two PDEs for the three unknown stress components ($\sigma_{rr}, \sigma_{\theta\theta}, \sigma_{r\theta}$). Equilibrium alone is insufficient to determine the stress field. [@problem_id:2889580]

The missing piece of the puzzle is **compatibility**. While a [displacement field](@entry_id:141476) always produces a valid (compatible) strain field, the reverse is not true. An arbitrary strain field, satisfying only the [constitutive relations](@entry_id:186508) and equilibrium, might not be integrable to a continuous, single-valued displacement field. It could describe a deformation that involves physically impossible gaps or overlaps. The [compatibility conditions](@entry_id:201103) are a set of differential constraints on the strain components that ensure such a single-valued displacement field exists. For a 2D problem, these reduce to a single equation. In polar coordinates, the **Saint-Venant [compatibility condition](@entry_id:171102)** is: [@problem_id:2889592]
$\dfrac{1}{r^2}\dfrac{\partial^2 \varepsilon_{rr}}{\partial \theta^2} + \dfrac{\partial^2 \varepsilon_{\theta\theta}}{\partial r^2} + \dfrac{2}{r}\dfrac{\partial \varepsilon_{\theta\theta}}{\partial r} - \dfrac{1}{r}\dfrac{\partial \varepsilon_{rr}}{\partial r} = \dfrac{2}{r}\dfrac{\partial^2 \varepsilon_{r\theta}}{\partial r \partial \theta} + \dfrac{2}{r^2}\dfrac{\partial \varepsilon_{r\theta}}{\partial \theta}$

A complete solution to an elasticity problem requires finding a field that simultaneously satisfies equilibrium, compatibility, and the constitutive law, along with the specified boundary conditions. In a displacement-based formulation, compatibility is satisfied automatically by defining strains from a displacement field. In a stress-based formulation, compatibility must be explicitly enforced. [@problem_id:2889580]

#### The Airy Stress Function

For 2D problems with no body forces, the stress-based formulation is greatly simplified by the introduction of the **Airy stress function**, $\Phi(r, \theta)$. This is a [scalar potential](@entry_id:276177) from which the stress components are derived: [@problem_id:2889543]

$\sigma_{rr} = \dfrac{1}{r}\dfrac{\partial \Phi}{\partial r} + \dfrac{1}{r^{2}} \dfrac{\partial^{2} \Phi}{\partial \theta^{2}}$

$\sigma_{\theta \theta} = \dfrac{\partial^{2} \Phi}{\partial r^{2}}$

$\sigma_{r \theta} = - \dfrac{\partial}{\partial r} \left( \dfrac{1}{r} \dfrac{\partial \Phi}{\partial \theta} \right)$

The power of this formulation lies in the fact that for any sufficiently smooth function $\Phi$, the stress field derived from it **identically satisfies the two [equilibrium equations](@entry_id:172166)**. This elegantly resolves the problem of static indeterminacy.

With equilibrium automatically satisfied, the task reduces to enforcing compatibility. By substituting the stress expressions (in terms of $\Phi$) into the compatibility condition (via the [constitutive law](@entry_id:167255)), we find that $\Phi$ must satisfy a single, fourth-order partial differential equation known as the **[biharmonic equation](@entry_id:165706)**:
$\nabla^4 \Phi = \nabla^2(\nabla^2 \Phi) = 0$
where $\nabla^2 = \frac{\partial^2}{\partial r^2} + \frac{1}{r}\frac{\partial}{\partial r} + \frac{1}{r^2}\frac{\partial^2}{\partial \theta^2}$ is the Laplacian in [polar coordinates](@entry_id:159425). Solving plane elasticity problems is thus reduced to finding the appropriate biharmonic function $\Phi$ that also satisfies the boundary conditions. [@problem_id:2889543]

### The General Solution: The Michell Expansion

The general solution to the [biharmonic equation](@entry_id:165706) in [polar coordinates](@entry_id:159425) can be found using the [method of separation of variables](@entry_id:197320). This leads to an [infinite series](@entry_id:143366) solution known as the **Michell solution**, which provides a powerful toolkit for solving a wide variety of plane elasticity problems.

#### Structure of the General Solution

The Michell solution expresses $\Phi(r, \theta)$ as a Fourier series in $\theta$. The radial dependence of each harmonic term is found by solving an [ordinary differential equation](@entry_id:168621), which reveals four independent solutions for each angular mode $n$. The four characteristic radial exponents are $n$, $-n$, $n+2$, and $-n+2$. [@problem_id:2889579]

A crucial subtlety arises when these exponents are not distinct. This happens for the low-order angular modes $n=0$ and $n=1$. For these special cases, the [repeated roots](@entry_id:151486) in the characteristic equation give rise to logarithmic terms in the solution. [@problem_id:2889555] The complete Michell solution is:

$\Phi(r,\theta) = (A_0 r^2 \ln r + B_0 r^2 + C_0 \ln r + D_0) \\ \quad + (a_1 r^3 + b_1 r \ln r + c_1 r + d_1 r^{-1})\cos\theta + (e_1 r^3 + f_1 r \ln r + g_1 r + h_1 r^{-1})\sin\theta \\ \quad + \sum_{n=2}^{\infty} \left[ (a_n r^n + b_n r^{-n} + c_n r^{n+2} + d_n r^{-n+2})\cos(n\theta) + (e_n r^n + f_n r^{-n} + g_n r^{n+2} + h_n r^{-n+2})\sin(n\theta) \right]$

The coefficients ($A_0, B_0, \dots, h_n$) are constants determined by the boundary conditions of a specific problem.

#### Physical Admissibility and Regularity Conditions

The Michell expansion provides the complete family of mathematical solutions. To find the unique physical solution for a given problem, we must apply boundary conditions and enforce physical regularity. A common scenario is a domain that includes the origin, such as a solid disk. For such a case, the solution must be physically well-behaved at $r=0$. This implies two fundamental requirements: [@problem_id:2889578]

1.  The **stress components must remain bounded** as $r \to 0$. A material cannot sustain infinite stress at a regular interior point.
2.  The **displacement field must be finite and single-valued** as $r \to 0$.

Applying these requirements to the Michell solution allows us to systematically eliminate terms that produce non-physical behavior at the origin.

*   **Negative Power Terms:** Terms with negative powers of $r$ (e.g., $r^{-n}$, $r^{-n+2}$ for $n>2$) lead to stresses that are singular (e.g., $\sigma \propto r^{-k}$ with $k>0$) as $r \to 0$. These terms must be excluded for a solution in a disk.

*   **Logarithmic Terms:** All logarithmic terms (e.g., $\ln r$, $r^2\ln r$, $r\ln r$) are problematic. They not only produce stresses that are logarithmically singular at the origin but also lead to displacements that are multi-valued (i.e., contain a $\theta$ term), which is physically impossible in a simply connected body. Therefore, all logarithmic terms must be suppressed. [@problem_id:2889555]

*   **Permissible Terms:** After excluding singular terms, the general solution for a domain containing the origin simplifies to a series of positive integer powers of $r$. This includes the constant and $r^2$ terms for $n=0$, the $r$ and $r^3$ terms for $n=1$, and the $r^n$ and $r^{n+2}$ terms for $n \ge 2$. Note that the terms $\Phi=D_0$ (constant) and $\Phi \propto r\cos\theta, r\sin\theta$ produce zero stress and correspond to [rigid body motion](@entry_id:144691), which are always admissible. [@problem_id:2889578]

It is critical to understand that the "singular" terms are not incorrect; they are simply inadmissible for problems involving a solid region at the origin. For problems involving domains that *exclude* the origin, such as an annulus (a plate with a hole) or an exterior region, these singular terms are not only permissible but are essential for constructing solutions that can satisfy boundary conditions on the inner and outer surfaces. [@problem_id:2889543] [@problem_id:2889555] For example, the [stress concentration](@entry_id:160987) around a hole is captured precisely by these terms that are singular at $r=0$.