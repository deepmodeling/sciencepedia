## Introduction
Laminated composites are foundational materials in modern engineering, prized for their high strength-to-weight ratio and design flexibility. To harness their full potential, engineers rely on accurate analytical models to predict their behavior under various loads. While Classical Lamination Theory (CLT) provides a robust framework for thin plates, its core assumptions break down as plate thickness increases, leading to inaccurate predictions. The primary knowledge gap it leaves is the neglect of [transverse shear deformation](@entry_id:176673), a critical effect in moderately thick [composites](@entry_id:150827).

This article introduces First-Order Shear Deformation Theory (FSDT), a powerful extension that directly addresses this deficiency. By incorporating shear effects, FSDT offers a more realistic and reliable model for a wider range of structural applications. Across the following chapters, you will gain a deep, practical understanding of this essential theory.

The journey begins with **Principles and Mechanisms**, where we will dissect the fundamental kinematic assumptions that separate FSDT from CLT. You will learn how these assumptions lead to the inclusion of transverse shear strains, the formulation of the laminate's [constitutive equations](@entry_id:138559) via the ABD matrix, and the critical concept of the [shear correction factor](@entry_id:164451). Next, the article explores **Applications and Interdisciplinary Connections**, demonstrating how FSDT is applied to practical engineering challenges. We will examine its role in laminate design, the analysis of sandwich panels, the prediction of [buckling](@entry_id:162815) and vibration, and its function as the backbone for modern computational tools. Finally, **Hands-On Practices** will provide you with opportunities to apply these concepts, solidifying your understanding by working through targeted problems that highlight the theory's core principles and practical implications.

## Principles and Mechanisms

First-Order Shear Deformation Theory (FSDT), often referred to as Reissner-Mindlin [plate theory](@entry_id:171507), represents a significant refinement of Classical Lamination Theory (CLT). While CLT provides accurate predictions for the behavior of thin laminated plates, its foundational assumptions become untenable as the plate thickness increases relative to its in-plane dimensions. FSDT extends the kinematic model to account for [transverse shear deformation](@entry_id:176673), a critical mechanism in moderately thick laminates. This chapter elucidates the core principles and mechanical consequences of the FSDT framework.

### Fundamental Kinematic Assumptions

The primary distinction between CLT and FSDT lies in their treatment of the material lines that are initially normal to the plate's mid-surface. CLT is built upon the **Kirchhoff-Love hypothesis**, which posits that these normals remain straight and perpendicular to the deformed mid-surface. A direct consequence of this strict normality constraint is the mathematical enforcement of zero transverse shear strains throughout the plate, i.e., $\gamma_{xz} = 0$ and $\gamma_{yz} = 0$ [@problem_id:2887315]. This simplification is justified for very thin plates where transverse shear strain energy is negligible compared to bending and membrane energies.

For moderately thick plates, however, neglecting [transverse shear deformation](@entry_id:176673) leads to an overly stiff structural model and inaccurate predictions of deflections and stresses. FSDT addresses this deficiency by relaxing the Kirchhoff-Love hypothesis. The core kinematic assumption of FSDT is that **material normals to the mid-surface remain straight and inextensible, but not necessarily perpendicular to the deformed mid-surface** [@problem_id:2887315] [@problem_id:2642022].

This relaxation is mathematically formulated through a specific displacement field. For a plate with its mid-surface defined on the $z=0$ plane, the displacement components $(u, v, w)$ at a point $(x, y, z)$ are expressed in terms of five generalized mid-surface variables:

$$ u(x,y,z) = u_0(x,y) + z \phi_x(x,y) $$
$$ v(x,y,z) = v_0(x,y) + z \phi_y(x,y) $$
$$ w(x,y,z) = w_0(x,y) $$

Here, the five generalized displacements, which are functions of the in-plane coordinates $(x,y)$ only, have distinct physical interpretations [@problem_id:2887260]:
-   $u_0(x,y)$ and $v_0(x,y)$ are the **in-plane displacements** of the mid-surface along the $x$ and $y$ axes.
-   $w_0(x,y)$ is the **transverse displacement** (or deflection) of the mid-surface.
-   $\phi_x(x,y)$ and $\phi_y(x,y)$ are the **rotations** of the initially [normal line](@entry_id:167651) segment about the $y$ and $x$ axes, respectively.

Crucially, in FSDT, $\phi_x$ and $\phi_y$ are independent kinematic variables, distinct from the slopes of the mid-surface, $-\partial w_0 / \partial x$ and $-\partial w_0 / \partial y$. This independence is what permits [transverse shear deformation](@entry_id:176673). The CLT [displacement field](@entry_id:141476) is recovered as a special case where the rotations are constrained to be equal to these slopes.

This kinematic field has several immediate consequences [@problem_id:2641975]:
1.  **Straight Normals, No Warping:** Because the in-plane displacements $u$ and $v$ are linear functions of the thickness coordinate $z$, any initially straight [normal line](@entry_id:167651) remains straight after deformation. Furthermore, any initially plane cross-section remains plane; there is no **cross-sectional warping**.
2.  **No Thickness Stretching:** The transverse displacement $w$ is assumed to be uniform through the thickness. This implies that the transverse [normal strain](@entry_id:204633) is identically zero: $\epsilon_{zz} = \frac{\partial w}{\partial z} = 0$.

### Strain Fields and Their Consequences

Applying the linearized three-dimensional [strain-displacement relations](@entry_id:173321) to the FSDT displacement field reveals the structure of deformation within the laminate.

#### In-plane Strains
The in-plane engineering strains ($\epsilon_x, \epsilon_y, \gamma_{xy}$) are found to vary linearly through the thickness:
$$ \boldsymbol{\epsilon}(z) = \begin{pmatrix} \epsilon_x \\ \epsilon_y \\ \gamma_{xy} \end{pmatrix} = \begin{pmatrix} \frac{\partial u_0}{\partial x} \\ \frac{\partial v_0}{\partial y} \\ \frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x} \end{pmatrix} + z \begin{pmatrix} \frac{\partial \phi_x}{\partial x} \\ \frac{\partial \phi_y}{\partial y} \\ \frac{\partial \phi_x}{\partial y} + \frac{\partial \phi_y}{\partial x} \end{pmatrix} $$
This expression is conventionally written as $\boldsymbol{\epsilon}(z) = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}$, where:
-   $\boldsymbol{\epsilon}_0$ is the **mid-surface strain vector**, representing the membrane deformation of the $z=0$ plane.
-   $\boldsymbol{\kappa}$ is the **curvature vector**, representing the bending and twisting of the plate.
These generalized strains are defined entirely by the mid-surface variables [@problem_id:2887241] [@problem_id:2641963].

#### Transverse Shear Strains
The transverse shear strains ($\gamma_{xz}, \gamma_{yz}$) are derived as:
$$ \gamma_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = \phi_x(x,y) + \frac{\partial w_0(x,y)}{\partial x} $$
$$ \gamma_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = \phi_y(x,y) + \frac{\partial w_0(x,y)}{\partial y} $$
A critical and defining feature of FSDT emerges from this derivation: the transverse shear strains, which we can denote as the vector $\boldsymbol{\gamma}_0$, are **constant** with respect to the thickness coordinate $z$ [@problem_id:2641975]. They are non-zero whenever the rotation of the normal ($\phi_x, \phi_y$) differs from the slope of the mid-surface ($-\partial w_0/\partial x, -\partial w_0/\partial y$). While this allows for the inclusion of shear deformation energy, the assumption of a constant strain profile through the thickness is a kinematic simplification with profound consequences, as we shall see.

### Constitutive Relations of the Laminate

To relate the generalized strains to forces and moments, we must integrate the stress-strain behavior of individual plies through the laminate thickness.

#### The Orthotropic Lamina
The building block of a laminate is a single orthotropic ply. Under a state of **[plane stress](@entry_id:172193)** (where $\sigma_z=0$), the relationship between in-plane stresses and strains in the material's principal axes (1, 2) is given by $\boldsymbol{\sigma} = \mathbf{Q} \boldsymbol{\epsilon}$, where $\boldsymbol{\sigma} = [\sigma_{11} \ \sigma_{22} \ \tau_{12}]^T$ and $\boldsymbol{\epsilon} = [\epsilon_{11} \ \epsilon_{22} \ \gamma_{12}]^T$. The **reduced stiffness matrix** $\mathbf{Q}$ for an [orthotropic material](@entry_id:191640) is symmetric and its components are defined in terms of the [engineering constants](@entry_id:199413): longitudinal modulus $E_1$, [transverse modulus](@entry_id:191863) $E_2$, major Poisson's ratio $\nu_{12}$, and in-plane shear modulus $G_{12}$ [@problem_id:2641953].
$$ \mathbf{Q} = \begin{pmatrix} Q_{11} & Q_{12} & 0 \\ Q_{12} & Q_{22} & 0 \\ 0 & 0 & Q_{66} \end{pmatrix} $$
with components $Q_{11} = \frac{E_1}{1-\nu_{12}\nu_{21}}$, $Q_{22} = \frac{E_2}{1-\nu_{12}\nu_{21}}$, $Q_{12} = \frac{\nu_{12}E_2}{1-\nu_{12}\nu_{21}}$, and $Q_{66} = G_{12}$. Thermodynamic consistency requires the symmetry of the stiffness and compliance matrices, which leads to the reciprocal relation $\nu_{21} = (\frac{E_2}{E_1})\nu_{12}$. For use in laminate analysis, this matrix $\mathbf{Q}$ must be transformed into the global laminate coordinate system $(x,y)$ to yield the **transformed reduced [stiffness matrix](@entry_id:178659)** $\bar{\mathbf{Q}}$.

#### The ABD Matrix and Extension-Bending Coupling
Laminate theory works with [stress resultants](@entry_id:180269)—forces and moments per unit length—obtained by integrating stresses through the thickness $h$.
-   **Force resultants:** $\mathbf{N} = \int_{-h/2}^{h/2} \boldsymbol{\sigma}(z) \, \mathrm{d}z$
-   **Moment resultants:** $\mathbf{M} = \int_{-h/2}^{h/2} z \boldsymbol{\sigma}(z) \, \mathrm{d}z$

Substituting the FSDT strain distribution and the ply [constitutive law](@entry_id:167255) into these integrals yields the celebrated laminate [constitutive equations](@entry_id:138559) [@problem_id:2887241]:
$$ \begin{pmatrix} \mathbf{N} \\ \mathbf{M} \end{pmatrix} = \begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B} & \mathbf{D} \end{pmatrix} \begin{pmatrix} \boldsymbol{\epsilon}_0 \\ \boldsymbol{\kappa} \end{pmatrix} $$
The $3 \times 3$ submatrices are defined by through-thickness integrals of the transformed ply stiffnesses [@problem_id:2641993]:
-   **Extensional stiffness matrix:** $\mathbf{A} = \sum_{k=1}^{N} \bar{\mathbf{Q}}^{(k)} (z_k - z_{k-1})$
-   **Coupling [stiffness matrix](@entry_id:178659):** $\mathbf{B} = \frac{1}{2} \sum_{k=1}^{N} \bar{\mathbf{Q}}^{(k)} (z_k^2 - z_{k-1}^2)$
-   **Bending [stiffness matrix](@entry_id:178659):** $\mathbf{D} = \frac{1}{3} \sum_{k=1}^{N} \bar{\mathbf{Q}}^{(k)} (z_k^3 - z_{k-1}^3)$

The **[coupling matrix](@entry_id:191757) $\mathbf{B}$** is a unique feature of [composite laminates](@entry_id:187061). A non-zero $\mathbf{B}$ matrix signifies the presence of **extension-bending coupling**. This means that applying a purely in-plane load can cause the laminate to bend or twist, and applying a pure bending moment can cause it to stretch or shear.

Consider a thought experiment on an unsymmetric laminate, for which $\mathbf{B} \neq \mathbf{0}$. If we apply only an in-plane force resultant $\mathbf{N}$ (so that the total moment resultant $\mathbf{M}=\mathbf{0}$), the second [constitutive equation](@entry_id:267976) becomes $\mathbf{0} = \mathbf{B}\boldsymbol{\epsilon}_0 + \mathbf{D}\boldsymbol{\kappa}$. This implies that if the laminate stretches or shears (i.e., $\boldsymbol{\epsilon}_0 \neq \mathbf{0}$), it must develop a non-zero curvature $\boldsymbol{\kappa} = -\mathbf{D}^{-1}\mathbf{B}\boldsymbol{\epsilon}_0$ to maintain [moment equilibrium](@entry_id:752138). Physically, stretching an unsymmetric laminate creates an internal moment due to the unbalanced stiffness distribution about the mid-plane, forcing the laminate to curve [@problem_id:2641982]. For a laminate with a [stacking sequence](@entry_id:197285) that is symmetric in both material and orientation about the geometric mid-plane, the $\mathbf{B}$ matrix is identically zero, and this coupling vanishes [@problem_id:2641982].

### The Challenge of Transverse Shear

While FSDT successfully introduces the *effects* of transverse shear, its simplified [kinematics](@entry_id:173318) create a significant theoretical inconsistency.

#### The Constant Strain Problem and Shear Correction
As established, FSDT kinematics lead to a transverse shear strain field that is constant through the thickness. Hooke's law then implies that the transverse shear stresses ($\tau_{xz}, \tau_{yz}$) are piecewise-constant through the thickness (constant within each layer) [@problem_id:2887280]. This prediction directly contradicts the physical reality that for a plate with traction-free top and bottom surfaces, the transverse shear stresses must be zero at these boundaries, i.e., $\tau_{xz}(z=\pm h/2) = 0$ [@problem_id:2641975]. An exact elasticity solution shows a parabolic-like distribution of shear stress.

This discrepancy means that FSDT overestimates the laminate's transverse shear stiffness. To correct for this, a **[shear correction factor](@entry_id:164451)**, $k$, is introduced. This factor modifies the relationship between the shear force resultants $\mathbf{Q} = \int_{-h/2}^{h/2} \boldsymbol{\tau}(z) \, \mathrm{d}z$ and the shear strains $\boldsymbol{\gamma}_0$. The corrected [constitutive relation](@entry_id:268485) is:
$$ \mathbf{Q} = \mathbf{A}_s \boldsymbol{\gamma}_0 $$
where the **transverse shear [stiffness matrix](@entry_id:178659)** $\mathbf{A}_s$ incorporates the correction factor. For instance, for the $xz$-component in an orthotropic plate, the effective stiffness is $A_{s55} = k_{xz} \int G_{xz}(z) \mathrm{d}z$ [@problem_id:2642018].

The [shear correction factor](@entry_id:164451) is not an arbitrary parameter; it is derived from the principle of **energetic equivalence**. The factor $k$ is chosen such that the shear strain energy calculated by the simplified FSDT model (with its constant strain) equals the shear [strain energy](@entry_id:162699) calculated from a more accurate 3D elasticity solution for the same resultant shear force. This leads to the following rigorous definition for the [shear correction factor](@entry_id:164451) [@problem_id:2642009]:
$$ k = \frac{\left( \int_{-h/2}^{h/2} \tau_{xz}(z) \, \mathrm{d}z \right)^2}{\left( \int_{-h/2}^{h/2} G_{xz}(z) \, \mathrm{d}z \right) \left( \int_{-h/2}^{h/2} \frac{\tau_{xz}(z)^2}{G_{xz}(z)} \, \mathrm{d}z \right)} $$
Here, $\tau_{xz}(z)$ is the physically realistic, non-uniform stress distribution. For a homogeneous isotropic plate, this procedure yields the well-known value of $k \approx 5/6$. For [composite laminates](@entry_id:187061), the factor depends on the [stacking sequence](@entry_id:197285) and material properties.

#### Recovering Realistic Shear Stresses
It is vital to understand that the [shear correction factor](@entry_id:164451) adjusts the global stiffness and energy; it does not fix the unphysical, constant stress distribution within the FSDT solution itself. To obtain a realistic, point-wise stress profile, a **post-processing** step is necessary. This is achieved by integrating the 3D differential [equations of equilibrium](@entry_id:193797) through the thickness [@problem_id:2887280]:
$$ \frac{\partial \tau_{xz}}{\partial z} = - \left( \frac{\partial \sigma_x}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} \right) $$
Starting from a known boundary condition, e.g., $\tau_{xz}(z=-h/2) = 0$, one can integrate this equation upward. The in-plane stresses ($\sigma_x, \sigma_{xy}$) and their derivatives are taken from the FSDT solution already obtained. Since the in-plane stresses are piecewise-linear in $z$, their gradients are also piecewise-linear, and integrating them with respect to $z$ yields a continuous, piecewise-quadratic distribution for the transverse shear stress that satisfies the boundary conditions and provides a much more accurate picture of the internal stress state.

### Computational Implementation and Shear Locking

The FSDT framework is particularly well-suited for the Finite Element Method (FEM). Because the [strain energy](@entry_id:162699) expression involves only first-order derivatives of the five generalized displacements ($u_0, v_0, w_0, \phi_x, \phi_y$), they can all be interpolated using simple $C^0$-continuous [shape functions](@entry_id:141015). This is a significant advantage over CLT, which requires $C^1$ continuity for the deflection $w_0$, making element formulation more complex [@problem_id:2642022].

However, this simple formulation suffers from a numerical [pathology](@entry_id:193640) known as **[shear locking](@entry_id:164115)**. In the limit of a very thin plate ($h \to 0$), the shear [strain energy](@entry_id:162699), which scales with plate thickness $h$, becomes orders of magnitude larger than the bending energy, which scales with $h^3$. To keep the total energy finite, the shear strains $\boldsymbol{\gamma}_0$ must vanish. This imposes the Kirchhoff constraints ($\phi_x = -\partial w_0/\partial x$, etc.) on the discrete model.

For a standard four-node [quadrilateral element](@entry_id:170172) using equal-order [bilinear interpolation](@entry_id:170280) for all five fields, the discrete system is unable to satisfy this zero-shear constraint at all integration points without forcing the element into a trivial, undeformed state. The element becomes artificially rigid against bending, or "locked" [@problem_id:2641963].

Several techniques have been developed to overcome [shear locking](@entry_id:164115). The most common are:
-   **Selective/Reduced Integration:** The shear stiffness term in the element formulation is integrated using a lower order quadrature rule than the bending term. This effectively weakens the shear constraint and prevents locking.
-   **Assumed/Mixed Strain Formulations:** More advanced methods, such as Mixed Interpolation of Tensorial Components (MITC), construct a separate, lower-order interpolation for the shear strain field that is specifically designed to represent a [pure bending](@entry_id:202969) state with zero shear energy, thereby eliminating the source of locking [@problem_id:2641963].

These remedies are essential for developing robust and accurate finite elements based on First-Order Shear Deformation Theory, enabling its application across the full range of plate thicknesses.