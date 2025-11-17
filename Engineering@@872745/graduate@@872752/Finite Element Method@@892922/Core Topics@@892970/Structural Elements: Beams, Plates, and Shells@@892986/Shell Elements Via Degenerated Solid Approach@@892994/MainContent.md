## Introduction
The degenerated solid approach (DSA) represents a pivotal development in computational structural mechanics, offering a powerful and versatile method for analyzing shell structures. Pioneered by Ahmad, Irons, and Zienkiewicz, this technique departs from classical 2D shell theories by starting with a full 3D continuum and imposing kinematic constraints to replicate shell behavior. This "solid-to-shell" philosophy resolves many of the challenges associated with modeling arbitrarily curved geometries, [transverse shear deformation](@entry_id:176673), and complex three-dimensional material responses, which often limit traditional formulations. The result is a unified framework capable of handling a vast range of problems from thin plates to moderately thick, laminated [composite shells](@entry_id:204473).

This article provides a comprehensive exploration of the DSA, guiding you from its theoretical underpinnings to its practical implementation and advanced applications.
*   **Chapter 1: Principles and Mechanisms** will dissect the core of the method, including its kinematic foundation, the treatment of degrees of freedom, the enforcement of the [plane stress condition](@entry_id:168184), and the numerical pathologies like [shear locking](@entry_id:164115) that must be addressed.
*   **Chapter 2: Applications and Interdisciplinary Connections** will showcase the versatility of DSA elements in modeling [composite laminates](@entry_id:187061), performing geometrically nonlinear and dynamic analyses, and serving as a bridge to other fields like [fracture mechanics](@entry_id:141480) and computational biology.
*   **Chapter 3: Hands-On Practices** will offer a set of targeted problems designed to solidify your understanding of key concepts, such as the origin of bending strains, the Poisson's effect in plates, and the mitigation of [shear locking](@entry_id:164115).

## Principles and Mechanisms

The formulation of [shell elements](@entry_id:176094) via the degenerated solid approach (DSA) represents a significant milestone in computational [structural mechanics](@entry_id:276699). Pioneered by Ahmad, Irons, and Zienkiewicz, this method departs from classical shell theories, which are inherently two-dimensional. Instead, it begins with the full [kinematics](@entry_id:173318) and constitutive framework of a three-dimensional solid continuum and imposes specific kinematic constraints to model the behavior of thin, shell-like structures. This "solid-to-shell" philosophy provides remarkable generality, allowing for the straightforward modeling of curved geometries and the use of complex three-dimensional material laws. This chapter elucidates the fundamental principles and mechanisms underpinning this powerful approach.

### The Kinematic Foundation of the Degenerated Solid Approach

The central tenet of the degenerated solid approach is the specific set of kinematic assumptions used to describe the motion of the shell. Unlike classical theories built upon a two-dimensional surface, the DSA begins with a three-dimensional **parent element**, typically a bi-unit cube defined by the dimensionless coordinates $(\xi, \eta, \zeta)$ where each coordinate ranges from $-1$ to $1$. The coordinates $(\xi, \eta)$ parameterize the mid-surface of the shell, while $\zeta$ represents the through-thickness direction.

The [position vector](@entry_id:168381) $\mathbf{x}$ of any material point within the shell is then mapped from this [parent domain](@entry_id:169388) to the physical three-dimensional space using the following fundamental relationship:

$$
\mathbf{x}(\xi, \eta, \zeta) = \mathbf{x}_0(\xi, \eta) + \frac{t(\xi, \eta)}{2} \zeta \mathbf{d}(\xi, \eta)
$$

Let us dissect this crucial equation [@problem_id:2596011]:
*   $\mathbf{x}_0(\xi, \eta)$ is the [position vector](@entry_id:168381) of a point on the shell's **mid-surface**.
*   $t(\xi, \eta)$ is the shell thickness at that point.
*   $\zeta$ is the normalized through-thickness coordinate, with $\zeta=-1$ corresponding to the bottom surface and $\zeta=+1$ to the top surface of the shell.
*   $\mathbf{d}(\xi, \eta)$ is the **director vector**. This is a vector field defined over the mid-surface that describes the orientation of the through-thickness "fiber" at each point.

This kinematic description enforces the **straight-fiber assumption**: a line of material points that is initially straight and normal to the undeformed mid-surface remains straight during deformation. This is evident from the [linear dependence](@entry_id:149638) of the [position vector](@entry_id:168381) $\mathbf{x}$ on the coordinate $\zeta$.

Following the **isoparametric concept**, the geometry of the mid-surface and the director field are interpolated from their values at the element's nodes using the same set of shape functions, $N_i(\xi, \eta)$. For an element with $n$ nodes on its mid-surface, the interpolations are:

$$
\mathbf{x}_0(\xi, \eta) = \sum_{i=1}^{n} N_i(\xi, \eta) \mathbf{x}_i
$$

$$
\mathbf{d}(\xi, \eta) = \sum_{i=1}^{n} N_i(\xi, \eta) \mathbf{d}_i
$$

Here, $\mathbf{x}_i$ are the nodal coordinate vectors on the mid-surface, and $\mathbf{d}_i$ are the nodal director vectors. Substituting these into the main kinematic equation gives the complete mapping for the element [@problem_id:2596095]:

$$
\mathbf{x}(\xi, \eta, \zeta) = \sum_{i=1}^{n} N_i(\xi, \eta) \left( \mathbf{x}_i + \frac{t_i}{2} \zeta \mathbf{d}_i \right)
$$
where $t_i$ is the thickness at node $i$, and for convenience, the magnitude of the director $\mathbf{d}_i$ is often normalized to unity while the thickness term is handled explicitly, or the magnitude of $\mathbf{d}_i$ is set to $t_i/2$.

The most significant aspect of this formulation is that the director $\mathbf{d}$ is treated as an independent field. It is not constrained to remain normal to the deformed mid-surface. This is the hallmark of **Reissner-Mindlin [kinematics](@entry_id:173318)**. The ability of the director to rotate relative to the surface normal allows the element to represent **[transverse shear deformation](@entry_id:176673)**, a phenomenon neglected in classical Kirchhoff-Love [shell theory](@entry_id:186302). This makes the degenerated solid shell element particularly suitable for moderately thick shells where shear effects are non-negligible.

### Degrees of Freedom and Constitutive Modeling

Translating the DSA [kinematics](@entry_id:173318) into a functional finite element requires careful consideration of the nodal degrees of freedom (DOFs) and the material [constitutive model](@entry_id:747751).

#### Nodal Degrees of Freedom and the Director Update

For each node $i$, the [position vector](@entry_id:168381) $\mathbf{x}_i$ introduces three [translational degrees of freedom](@entry_id:140257), which can be represented by a [displacement vector](@entry_id:262782) $\mathbf{u}_i$. The director $\mathbf{d}_i$, being a vector in $\mathbb{R}^3$, also seems to introduce three additional degrees of freedom. However, a naive treatment of the three components of $\mathbf{d}_i$ as independent unknowns is problematic. The length of the director is related to the shell thickness, which should not change arbitrarily.

A more robust and elegant approach is to define the nodal director in the current configuration, $\mathbf{d}_I$, by rotating a reference director, $\mathbf{D}_I$, from a known configuration [@problem_id:2596083]. This update is performed using a finite rotation formalism:

$$
\mathbf{d}_I = \mathbf{R}(\Delta \boldsymbol{\theta}_I) \mathbf{D}_I
$$

Here, $\Delta \boldsymbol{\theta}_I$ is a three-component incremental rotation vector that serves as the set of [rotational degrees of freedom](@entry_id:141502) at the node, and $\mathbf{R}(\Delta \boldsymbol{\theta}_I)$ is the corresponding orthogonal [rotation tensor](@entry_id:191990). This formulation has two profound advantages:

1.  **Automatic Thickness Control:** Since $\mathbf{R}$ is an orthogonal tensor, it preserves [vector norms](@entry_id:140649). Therefore, if the reference director is defined such that its length is half the initial thickness, $\|\mathbf{D}_I\| = t_I/2$, the updated director automatically satisfies $\|\mathbf{d}_I\| = t_I/2$. This kinematically enforces the condition of no thickness change, which is a common assumption in many shell theories.

2.  **Intrinsic Avoidance of the Drilling Degree of Freedom:** The so-called **drilling degree of freedom** corresponds to a rotation about the director axis itself. In this formulation, a component of the rotation vector $\Delta \boldsymbol{\theta}_I$ aligned with $\mathbf{d}_I$ results in a spin about the director. Such a spin leaves the director itself invariant: $\mathbf{R}(\alpha \mathbf{d}_I) \mathbf{d}_I = \mathbf{d}_I$. Since the element's [kinematics](@entry_id:173318) depend only on the director vector $\mathbf{d}_I$ (and its gradient), this spin produces no strain and thus no strain energy. The drilling rotation is not an independent generalized coordinate and does not require a spurious stiffness to be controlled, a common issue in other shell formulations.

Thus, a typical DSA shell element node possesses three translational DOFs and three rotational parameters, for a total of six DOFs per node.

#### The 3D Stress/Strain Framework and Plane Stress Enforcement

One of the most powerful features of the DSA is its natural compatibility with general three-dimensional [constitutive models](@entry_id:174726). The formulation does not require an a-priori reduction of the material law to a two-dimensional shell-specific form. The procedure for calculating [internal forces](@entry_id:167605) and stiffness is as follows:

1.  From the element's kinematic field, compute the full three-dimensional [strain tensor](@entry_id:193332) (e.g., the Green-Lagrange strain tensor $\mathbf{E}$ in a Total Lagrangian formulation) at each integration point (Gauss point) throughout the element's volume.

2.  Feed this 3D [strain tensor](@entry_id:193332) into a full 3D constitutive law, $\mathbf{S} = \mathbf{S}(\mathbf{E})$, to obtain the corresponding 3D stress tensor (e.g., the second Piola-Kirchhoff stress tensor $\mathbf{S}$).

This process, however, presents a subtle but critical challenge. For a thin structure, the stress normal to the shell surface is physically negligible. This is the **[plane stress condition](@entry_id:168184)**, which for a [local coordinate system](@entry_id:751394) with the '3' direction normal to the mid-surface, implies $\sigma_{33} = 0$ (or $S_{33} = 0$). The DSA kinematics and a standard 3D material law do not automatically satisfy this condition. For instance, in-plane strains $\varepsilon_{11}$ and $\varepsilon_{22}$ will induce a thickness-[normal stress](@entry_id:184326) $\sigma_{33}$ via Poisson's effect, even if the through-thickness strain $\varepsilon_{33}$ is zero [@problem_id:2596075].

To resolve this, the [plane stress condition](@entry_id:168184) must be explicitly enforced at each integration point during the material state update [@problem_id:2595970]. This is typically achieved by treating the through-thickness strain component, $E_{33}$, as an internal variable rather than a kinematically-driven one. For a given set of five kinematically determined strain components ($E_{11}, E_{22}, E_{12}, E_{13}, E_{23}$), we must find the value of $E_{33}$ that satisfies the scalar nonlinear equation:

$$
r(E_{33}) = S_{33}(E_{11}, E_{22}, E_{12}, E_{13}, E_{23}, E_{33}) = 0
$$

This scalar root-finding problem is solved locally at each Gauss point using a **Newton-Raphson iteration**. At iteration $k$, the update $\Delta E_{33}$ is found by solving:

$$
r(E_{33}^{(k)}) + K \Delta E_{33} = 0 \implies \Delta E_{33} = -K^{-1} r(E_{33}^{(k)})
$$

The residual $r$ is simply the current value of the stress $S_{33}$. The Jacobian $K$ is the partial derivative of the residual with respect to the unknown, which, by definition of the material tangent modulus $C_{ijkl} = \partial S_{ij} / \partial E_{kl}$, is simply $K = C_{3333}$.

Once this local iteration converges, we have the correct material state (stresses and strains) that satisfies the [plane stress condition](@entry_id:168184). A crucial byproduct of this procedure is the **consistent condensed [tangent stiffness](@entry_id:166213)**. To obtain the correct tangent for the [element stiffness matrix](@entry_id:139369), the full 3D tangent $C_{ijkl}$ must be "condensed" by eliminating the row and column corresponding to the $33$-components, using a [static condensation](@entry_id:176722) (Schur complement) procedure [@problem_id:2595970]. This ensures that the global Newton-Raphson method for the full structural problem maintains a quadratic [rate of convergence](@entry_id:146534).

### Strain Fields and Element Formulation

The connection between the global kinematic assumptions and the local stress-strain state is forged through the [strain tensor](@entry_id:193332). The specific structure of the DSA strain field is fundamental to its behavior.

#### Decomposition of the Strain Tensor

Let us examine the structure of the [small-strain tensor](@entry_id:754968) $\boldsymbol{\varepsilon}$ resulting from the DSA kinematic assumption. Using a local coordinate system where $(x_1, x_2)$ are in-plane and $x_3 = (t/2)\zeta$ is the thickness coordinate, the [displacement field](@entry_id:141476) can be written as:
$u_{\alpha}(x_1, x_2, \zeta) = \bar{u}_{\alpha}(x_1, x_2) + x_3 \varphi_{\alpha}(x_1, x_2)$ for $\alpha=1,2$, and $u_3(x_1, x_2) = \bar{w}(x_1, x_2)$, where $\bar{u}_{\alpha}, \bar{w}$ are mid-surface displacements and $\varphi_{\alpha}$ are director rotations.

By applying the strain definition $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$, we can derive the through-thickness distribution of each strain component [@problem_id:2596031]:

*   **In-plane Strains ($\varepsilon_{\alpha\beta}$):** These strains vary linearly through the thickness. They can be decomposed into a constant part (membrane strain) and a part that is linear in $\zeta$ (bending strain):
    $$
    \varepsilon_{\alpha\beta}(\zeta) = \varepsilon_{\alpha\beta}^{m} + \frac{t}{2}\zeta \kappa_{\alpha\beta}
    $$
    where $\varepsilon_{\alpha\beta}^{m} = \frac{1}{2}(\bar{u}_{\alpha,\beta} + \bar{u}_{\beta,\alpha})$ are the **membrane strains** and $\kappa_{\alpha\beta} = \frac{1}{2}(\varphi_{\alpha,\beta} + \varphi_{\beta,\alpha})$ are the **curvatures**.

*   **Transverse Shear Strains ($\gamma_{\alpha 3}$):** A key consequence of the linear kinematic assumption is that the transverse shear strains are constant through the thickness:
    $$
    \gamma_{\alpha 3} = \bar{w}_{,\alpha} + \varphi_{\alpha} = \gamma_{\alpha 3}^0
    $$
    This simplicity is the source of a significant numerical issue known as [shear locking](@entry_id:164115), which we will discuss shortly.

*   **Transverse Normal Strain ($\varepsilon_{33}$):** The kinematic assumption implies that $\varepsilon_{33} = u_{3,3} = \partial \bar{w} / \partial x_3 = 0$. This kinematic constraint of zero thickness change is what necessitates the explicit enforcement of the [plane stress condition](@entry_id:168184) discussed previously.

In summary, the full 3D strain vector $\mathbf{E}$ can be written in Voigt notation as:
$$
\mathbf{E}(\zeta) = \begin{pmatrix} \varepsilon_{11}^{m} + \frac{t}{2}\zeta \kappa_{11} \\ \varepsilon_{22}^{m} + \frac{t}{2}\zeta \kappa_{22} \\ \gamma_{12}^{m} + t\zeta \kappa_{12} \\ \gamma_{13}^{0} \\ \gamma_{23}^{0} \\ 0 \end{pmatrix}
$$

#### The Strain-Displacement Matrix

The [finite element formulation](@entry_id:164720) relies on the discrete [strain-displacement matrix](@entry_id:163451), $\mathbf{B}$, which relates the strain at any point to the vector of nodal degrees of freedom, $\mathbf{d}$: $\boldsymbol{\varepsilon} = \mathbf{B} \mathbf{d}$. The [element stiffness matrix](@entry_id:139369) is then computed as $\mathbf{K} = \int_{V} \mathbf{B}^T \mathbf{D} \mathbf{B} \, dV$.

The construction of the $\mathbf{B}$ matrix involves differentiating the shape functions. For instance, to find the component relating the strain $\varepsilon_{xx}$ to the nodal displacements, we use the [chain rule](@entry_id:147422). For a simple rectangular element mapped from the parent square, where $x = a\xi$ and $y=b\eta$, the Jacobian is a simple diagonal matrix. The strain is then:
$$
\varepsilon_{xx} = \frac{\partial u}{\partial x} = \frac{\partial u}{\partial \xi} \frac{\partial \xi}{\partial x} = \frac{1}{a} \frac{\partial}{\partial \xi} \left( \sum_{I=1}^{n} N_I(\xi, \eta) u_I(\zeta) \right) = \frac{1}{a} \sum_{I=1}^{n} \frac{\partial N_I}{\partial \xi} u_I(\zeta)
$$
where $u_I(\zeta)$ includes contributions from both translational and rotational DOFs. Evaluating the derivatives of the shape functions allows for the explicit population of the $\mathbf{B}$ matrix. For example, for a 4-node bilinear element, the contribution of the nodal displacement $u_1$ to the membrane part of $\varepsilon_{xx}$ at the element center $(\xi, \eta) = (0,0)$ is found to be $-\frac{1}{4a} u_1$ [@problem_id:2596019]. This systematic procedure connects the abstract kinematic theory to the concrete numerical objects required for computation.

### Numerical Implementation and Pathologies

While elegant in theory, the practical implementation of low-order DSA elements (e.g., 4-node quadrilaterals or 8-node hexahedra degenerated to shells) is plagued by numerical "locking" phenomena. These are non-physical stiffening effects that arise from the inability of the simple polynomial interpolation to represent complex deformation states.

#### Shear Locking and Reduced Integration

The most notorious [pathology](@entry_id:193640) is **[shear locking](@entry_id:164115)**. As discussed, the Reissner-Mindlin [kinematics](@entry_id:173318) of the DSA element result in a transverse shear strain field that is constant through the thickness. For low-order elements, this field is also of very low order in the in-plane directions. When a thin shell undergoes [pure bending](@entry_id:202969), the exact shear strain should be nearly zero everywhere. However, the low-order interpolated shear field is overconstrained and cannot reproduce this near-zero state. When the stiffness matrix is computed with full numerical integration (e.g., a $2 \times 2$ Gauss quadrature for a bilinear quad), the element is forced into a state with spurious, non-zero shear energy, making it act artificially stiff in bending [@problem_id:2596046]. This effect worsens as the shell thickness decreases, and can completely dominate the solution.

A simple and effective remedy is **reduced integration**. By evaluating the transverse shear contribution to the [stiffness matrix](@entry_id:178659) at a reduced number of integration points (e.g., a single $1 \times 1$ Gauss point at the element center), we are placing fewer constraints on the shear field. The element is now better able to approximate the zero-shear state required for bending, and locking is significantly alleviated.

#### Hourglass Modes

Reduced integration, while solving one problem, introduces another: **[hourglass modes](@entry_id:174855)**, also known as [spurious zero-energy modes](@entry_id:755267) [@problem_id:2596046]. These are non-rigid deformation patterns of the element that produce exactly zero strain at the reduced set of integration points. Consequently, they generate zero [strain energy](@entry_id:162699) and are not resisted by the element's stiffness matrix. The stiffness matrix becomes rank-deficient, and an unconstrained structure can deform in these non-physical patterns without any resistance, corrupting the solution.

For a 4-node [quadrilateral element](@entry_id:170172) with one-point integration, these modes correspond to displacement fields that are proportional to the term $\xi\eta$. For example, an in-plane [displacement field](@entry_id:141476) of $u_x = \delta \xi \eta$ has derivatives $\partial u_x/\partial \xi = \delta\eta$ and $\partial u_x/\partial \eta = \delta\xi$. Both derivatives are zero at the element center $(\xi, \eta) = (0,0)$. The corresponding nodal [displacement vector](@entry_id:262782), which creates this "bow-tie" or "hourglass" shape, is therefore a [zero-energy mode](@entry_id:169976) [@problem_id:2596026] [@problem_id:2596017]. A basis for the two in-plane [hourglass modes](@entry_id:174855) can be expressed as the columns of the following matrix:
$$
\begin{pmatrix}
1  & 0 \\
0  & 1 \\
-1 & 0 \\
0  & -1 \\
1  & 0 \\
0  & 1 \\
-1 & 0 \\
0  & -1
\end{pmatrix}
$$

#### Advanced Stabilization Techniques

Modern [shell elements](@entry_id:176094) employ sophisticated techniques to reap the benefits of reduced integration without suffering from its drawbacks. The goal is to strike a balance between accuracy (no locking) and stability (no [hourglassing](@entry_id:164538)).

*   **Selective Reduced Integration (SRI) with Hourglass Control:** This popular strategy involves integrating different parts of the strain energy with different rules. The membrane and bending terms, which are less prone to locking, are integrated with a full quadrature rule (e.g., $2 \times 2$). The transverse shear terms are evaluated with a reduced rule (e.g., $1 \times 1$). To counteract the resulting instability, a small artificial stiffness, or **[hourglass control](@entry_id:163812)**, is added to the element formulation. This stabilization is carefully designed to only penalize the [hourglass modes](@entry_id:174855), while having no effect on constant strain states, thereby ensuring the element still passes fundamental consistency checks like the patch test [@problem_id:2596046].

*   **Assumed Natural Strain (ANS):** This is a more theoretically grounded approach to combat locking. Instead of using the shear strains derived directly from the finite element displacement interpolation, an independent, lower-order "assumed" strain field is constructed. This is done by sampling the raw FE shear strains at a few specially chosen locations (tying points), such as the midpoints of the element edges, and then interpolating these values to the Gauss points for the stiffness calculation [@problem_id:2595977]. For instance, the [shear strain](@entry_id:175241) $\gamma_{13}^*$ might be assumed to vary linearly in $\xi$ and be constant in $\eta$. This assumed field is too simple to capture the complex strain distribution that causes locking, but it is rich enough to represent a constant shear state exactly. Because any constant strain field is reproduced exactly by the interpolation, the ANS method is guaranteed to pass the **patch test**, a fundamental requirement for convergence. This ensures accuracy while circumventing the locking mechanism.

In conclusion, the degenerated solid approach provides a versatile and powerful framework for shell analysis. Its success hinges not only on its elegant kinematic foundation but also on the careful numerical techniques developed to overcome the inherent challenges of low-order interpolation, resulting in elements that are both robust and accurate across a wide range of applications.