## Introduction
In the field of [structural mechanics](@entry_id:276699), the analysis of plates—flat structural elements with a small thickness compared to their other dimensions—is fundamental. While Classical Plate Theory (CPT) provides an elegant model for thin, homogeneous plates, its core assumption—that lines normal to the mid-surface remain normal after deformation—breaks down for the thick, laminated composite, and sandwich structures that define modern high-[performance engineering](@entry_id:270797). This limitation creates a critical knowledge gap, as neglecting [transverse shear deformation](@entry_id:176673) can lead to non-conservative designs and inaccurate predictions of structural behavior.

This article provides a comprehensive exploration of First-Order Shear Deformation Theory (FSDT), also known as Reissner-Mindlin theory, a powerful framework that resolves this deficiency. Across three interconnected chapters, you will gain a graduate-level understanding of this essential model. We will begin by exploring its **Principles and Mechanisms**, dissecting the kinematic hypotheses that set it apart from CPT, deriving the governing equations, and examining its inherent limitations, such as the need for a [shear correction factor](@entry_id:164451) and the numerical issue of [shear locking](@entry_id:164115). Next, in **Applications and Interdisciplinary Connections**, we will demonstrate the theory's versatility by applying it to the analysis of [composite laminates](@entry_id:187061), [buckling](@entry_id:162815), and vibration, and exploring its role in aerospace, [thermo-mechanics](@entry_id:172368), and computational analysis. Finally, **Hands-On Practices** will offer a series of guided problems to reinforce these concepts, allowing you to apply FSDT to practical engineering scenarios. We will begin by establishing the theoretical foundations of the model.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanical formulations of the First-Order Shear Deformation Theory (FSDT) for plates, commonly known as Reissner-Mindlin theory. Building upon the introductory concepts, we will systematically construct the theory from its kinematic assumptions, through the derivation of [strain measures](@entry_id:755495) and [stress resultants](@entry_id:180269), to the formulation of the governing [equilibrium equations](@entry_id:172166). Finally, we will critically examine the theory's inherent limitations and key distinguishing features, such as the [shear correction factor](@entry_id:164451) and the numerical pathology of [shear locking](@entry_id:164115).

### Kinematic Hypotheses and the Displacement Field

The fundamental departure of First-Order Shear Deformation Theory from Classical Plate Theory (CPT), or Kirchhoff-Love theory, lies in its kinematic assumptions. CPT rigidly enforces the **normality constraint**: straight lines initially normal to the plate's mid-surface must remain straight and normal to the deformed mid-surface. FSDT relaxes this stringent condition.

The core kinematic hypotheses of FSDT are [@problem_id:2641452] [@problem_id:2641448]:
1.  Straight lines initially normal to the undeformed mid-surface (often called **directors**) remain straight after deformation.
2.  These directors do not change in length during deformation (i.e., they are inextensible).
3.  The directors are **not** required to remain normal to the deformed mid-surface.

This third hypothesis is the defining feature of the theory. It allows for a rotation of the director that is independent of the rotation of the mid-surface itself, which physically corresponds to accommodating **[transverse shear deformation](@entry_id:176673)**.

To translate these hypotheses into a mathematical form, let us consider a plate with its mid-surface in the $x-y$ plane and the thickness coordinate $z$ measured from this surface, such that $z \in [-h/2, h/2]$. The displacement of any point $(x,y,z)$ in the plate can be expressed in terms of five independent kinematic fields defined on the mid-surface $(z=0)$. Let $(u_0(x,y), v_0(x,y), w_0(x,y))$ be the displacements of a point on the mid-surface in the $x, y, z$ directions, respectively. Let $\phi_x(x,y)$ and $\phi_y(x,y)$ represent the rotations of the director about the $y$-axis and the $-x$-axis, respectively.

The first hypothesis (straight directors) implies that the in-plane displacements, $u(x,y,z)$ and $v(x,y,z)$, vary linearly with the thickness coordinate $z$. The second hypothesis (inextensible directors) implies that the transverse [normal strain](@entry_id:204633) $\epsilon_{zz} = \partial w / \partial z$ is zero, meaning the transverse displacement $w$ must be independent of $z$. Combining these leads to the FSDT displacement field:
$$
u(x,y,z) = u_0(x,y) + z \phi_x(x,y)
$$
$$
v(x,y,z) = v_0(x,y) + z \phi_y(x,y)
$$
$$
w(x,y,z) = w_0(x,y)
$$
Here, the fields $\phi_x$ and $\phi_y$ are treated as independent kinematic variables, distinct from the slopes of the mid-surface deflection, $\partial w_0 / \partial x$ and $\partial w_0 / \partial y$. It is precisely this independence that allows the theory to model transverse shear effects, which are significant in thick or [composite plates](@entry_id:181791). If we were to enforce the CPT constraint, we would set $\phi_x = -\partial w_0 / \partial x$ and $\phi_y = -\partial w_0 / \partial y$, thereby reducing the number of independent kinematic variables. [@problem_id:2641448]

### Generalized Strains: A 2D Representation of Deformation

From the assumed [displacement field](@entry_id:141476), we can derive the strain components using the linearized [strain-displacement relations](@entry_id:173321) of small-deformation elasticity. This process reveals how the 3D strain field is parameterized by 2D generalized [strain measures](@entry_id:755495) defined on the mid-surface.

The in-plane strain components $(\epsilon_{xx}, \epsilon_{yy}, \gamma_{xy})$ are found to vary linearly through the thickness:
$$
\epsilon_{xx} = \frac{\partial u}{\partial x} = \frac{\partial u_0}{\partial x} + z \frac{\partial \phi_x}{\partial x}
$$
$$
\epsilon_{yy} = \frac{\partial v}{\partial y} = \frac{\partial v_0}{\partial y} + z \frac{\partial \phi_y}{\partial y}
$$
$$
\gamma_{xy} = \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} = \left(\frac{\partial u_0}{\partial y} + \frac{\partial v_0}{\partial x}\right) + z \left(\frac{\partial \phi_x}{\partial y} + \frac{\partial \phi_y}{\partial x}\right)
$$
This structure can be concisely written as $\boldsymbol{\epsilon}(z) = \boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa}$, where $\boldsymbol{\epsilon}_0$ is the **mid-surface strain vector** (representing membrane stretching) and $\boldsymbol{\kappa}$ is the **curvature vector** (representing bending and twisting):
$$
\boldsymbol{\epsilon}_0 = \begin{pmatrix} \partial u_0 / \partial x \\ \partial v_0 / \partial y \\ \partial u_0 / \partial y + \partial v_0 / \partial x \end{pmatrix}
\quad , \quad
\boldsymbol{\kappa} = \begin{pmatrix} \partial \phi_x / \partial x \\ \partial \phi_y / \partial y \\ \partial \phi_x / \partial y + \partial \phi_y / \partial x \end{pmatrix}
$$

The transverse shear strains $(\gamma_{xz}, \gamma_{yz})$ are derived as:
$$
\gamma_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = \phi_x + \frac{\partial w_0}{\partial x}
$$
$$
\gamma_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = \phi_y + \frac{\partial w_0}{\partial y}
$$
A crucial consequence of the first-order kinematic assumption is that these transverse shear strains, which we denote as the vector $\boldsymbol{\gamma}_0$, are **constant through the plate thickness** [@problem_id:2641459]. This is a significant simplification. Physically, for a plate with traction-free top and bottom surfaces, the shear stresses (and thus strains) must be zero at $z = \pm h/2$. The FSDT kinematics cannot capture this variation, an inconsistency that must be addressed, as we will see later. [@problem_id:2887234]

### Stress Resultants: From 3D Continuum to 2D Plate

Plate theory achieves its [dimensional reduction](@entry_id:197644) by working with [stress resultants](@entry_id:180269)—forces and moments per unit length of the mid-surface—instead of the full 3D stress tensor. These resultants are obtained by integrating the 3D Cauchy stress components through the plate thickness. [@problem_id:2641522]

The **membrane force resultants**, $\mathbf{N}$, represent the in-plane forces:
$$
N_{xx} = \int_{-h/2}^{h/2} \sigma_{xx} \,dz, \quad N_{yy} = \int_{-h/2}^{h/2} \sigma_{yy} \,dz, \quad N_{xy} = \int_{-h/2}^{h/2} \sigma_{xy} \,dz
$$

The **bending and twisting moment resultants**, $\mathbf{M}$, represent the first moment of the in-plane stresses about the mid-surface:
$$
M_{xx} = \int_{-h/2}^{h/2} z \sigma_{xx} \,dz, \quad M_{yy} = \int_{-h/2}^{h/2} z \sigma_{yy} \,dz, \quad M_{xy} = \int_{-h/2}^{h/2} z \sigma_{xy} \,dz
$$

The **transverse shear force resultants**, $\mathbf{Q}$, represent the integrated transverse shear stresses:
$$
Q_x = \int_{-h/2}^{h/2} \sigma_{xz} \,dz, \quad Q_y = \int_{-h/2}^{h/2} \sigma_{yz} \,dz
$$
These definitions provide the vital link between the 3D stress state within the plate and the 2D quantities used in the plate's governing equations.

### The Constitutive Framework of FSDT Plates

The [constitutive law](@entry_id:167255) of the plate relates the generalized stresses (resultants) to the generalized strains. This is derived by substituting the 3D [constitutive law](@entry_id:167255) (e.g., Hooke's Law for an elastic material) into the integral definitions of the resultants.

For a general **laminated plate** composed of $n$ orthotropic layers, each with its own transformed reduced [stiffness matrix](@entry_id:178659) $\bar{\mathbf{Q}}^{(k)}$ and transverse shear stiffness matrix $\bar{\mathbf{Q}}_s^{(k)}$, the stress in layer $k$ is given by $\boldsymbol{\sigma}^{(k)} = \bar{\mathbf{Q}}^{(k)} \boldsymbol{\epsilon} = \bar{\mathbf{Q}}^{(k)} (\boldsymbol{\epsilon}_0 + z \boldsymbol{\kappa})$. Substituting this into the definitions for $\mathbf{N}$ and $\mathbf{M}$ and integrating layer by layer yields the celebrated **[A, B, D] matrix formulation** [@problem_id:2887241]:
$$
\begin{pmatrix} \mathbf{N} \\ \mathbf{M} \end{pmatrix} = \begin{pmatrix} \mathbf{A} & \mathbf{B} \\ \mathbf{B} & \mathbf{D} \end{pmatrix} \begin{pmatrix} \boldsymbol{\epsilon}_0 \\ \boldsymbol{\kappa} \end{pmatrix}
$$
The submatrices are defined by the following integrals, summing over all layers from $k=1$ to $n$ with layer interfaces at $z_k$:
-   The **[extensional stiffness](@entry_id:193973) matrix**, $\mathbf{A} = \sum_{k=1}^{n} \int_{z_{k-1}}^{z_k} \bar{\mathbf{Q}}^{(k)} \,dz$, relates in-plane forces to mid-surface strains.
-   The **[bending-stretching coupling](@entry_id:195676) matrix**, $\mathbf{B} = \sum_{k=1}^{n} \int_{z_{k-1}}^{z_k} z \bar{\mathbf{Q}}^{(k)} \,dz$, couples membrane forces to curvatures and [bending moments](@entry_id:202968) to membrane strains. This matrix is non-zero for asymmetric laminates.
-   The **[bending stiffness](@entry_id:180453) matrix**, $\mathbf{D} = \sum_{k=1}^{n} \int_{z_{k-1}}^{z_k} z^2 \bar{\mathbf{Q}}^{(k)} \,dz$, relates [bending moments](@entry_id:202968) to curvatures.

Similarly, the transverse shear relationship is given by:
$$
\mathbf{Q} = \mathbf{A}_s \boldsymbol{\gamma}_0
$$
where $\mathbf{A}_s$ is the **transverse shear stiffness matrix**, defined as $\mathbf{A}_s = \sum_{k=1}^{n} \int_{z_{k-1}}^{z_k} \mathbf{k}_s \bar{\mathbf{Q}}_s^{(k)} \,dz$. Note the inclusion of a matrix of **shear correction factors**, $\mathbf{k}_s$, which will be discussed shortly. For a single homogeneous, isotropic layer, these relations simplify considerably.

### Governing Equilibrium Equations

The final piece of the theoretical puzzle is equilibrium. By considering force and moment balance on an infinitesimal plate element, we arrive at five [equilibrium equations](@entry_id:172166). In the absence of in-plane body forces and for a transverse distributed load $p(x,y)$, these are:
1.  $\partial_x N_{xx} + \partial_y N_{xy} = 0$
2.  $\partial_x N_{xy} + \partial_y N_{yy} = 0$
3.  $\partial_x Q_x + \partial_y Q_y + p = 0$
4.  $\partial_x M_{xx} + \partial_y M_{xy} - Q_x = 0$
5.  $\partial_x M_{xy} + \partial_y M_{yy} - Q_y = 0$

By substituting the constitutive and kinematic relations into these [equilibrium equations](@entry_id:172166), we can derive a set of five coupled partial differential equations (PDEs) in terms of the five kinematic unknowns $(u_0, v_0, w_0, \phi_x, \phi_y)$. For a homogeneous, isotropic plate, these equations can be written in a compact operator form [@problem_id:2641506]:
$$
\mathcal{L}\,\begin{pmatrix} u_{0} \\ v_{0} \\ w_{0} \\ \phi_{x} \\ \phi_{y} \end{pmatrix}
=
\begin{pmatrix} 0 \\ 0 \\ -p \\ 0 \\ 0 \end{pmatrix}
$$
where $\mathcal{L}$ is a $5 \times 5$ matrix of differential operators. The structure of $\mathcal{L}$ reveals that the in-plane displacements $(u_0, v_0)$ are uncoupled from the transverse behavior $(w_0, \phi_x, \phi_y)$ in the linear isotropic case. This system of PDEs, along with appropriate boundary conditions, constitutes the complete mathematical model for analyzing the plate's behavior.

### Critical Analysis: Limitations and Key Concepts of FSDT

While powerful, FSDT is built on simplifying assumptions that have important consequences. Understanding these is crucial for its appropriate application.

#### The Inconsistency of Transverse Shear and the Role of the Shear Correction Factor

As established, FSDT [kinematics](@entry_id:173318) lead to a transverse shear strain that is constant through the thickness [@problem_id:2641459]. This directly contradicts the physical requirement that shear stresses (and strains, for a material with finite surface [shear modulus](@entry_id:167228)) must vanish on traction-free surfaces, i.e., $\tau_{xz}(\pm h/2) = \tau_{yz}(\pm h/2) = 0$. If one were to enforce this condition in FSDT, the constant strain must be zero everywhere, leading to zero shear force resultants ($Q_x = Q_y = 0$). This would violate plate equilibrium for any non-zero transverse load [@problem_id:2887234].

FSDT resolves this paradox not by fixing the [kinematics](@entry_id:173318), but by correcting the resulting energy. A **[shear correction factor](@entry_id:164451)**, $\kappa$ (often denoted $k_s$), is introduced into the constitutive law for the shear resultant, e.g., $Q_x = \kappa G h \gamma_{xz}$. The factor $\kappa$ is chosen to make the shear [strain energy](@entry_id:162699) calculated by the simplified FSDT model equal to the "true" shear [strain energy](@entry_id:162699) calculated from 3D [elasticity theory](@entry_id:203053) for a given shear resultant.

The defining principle for $\kappa$ is the equality of [strain energy](@entry_id:162699) per unit area [@problem_id:2887261]:
$$
U_{\text{FSDT}} = \frac{Q_x^2}{2 \kappa G h} = U_{\text{3D}} = \int_{-h/2}^{h/2} \frac{\tau_{xz}(z)^2}{2G} \,dz
$$
Solving for $\kappa$ gives its general definition:
$$
\kappa = \frac{Q_x^2}{h \int_{-h/2}^{h/2} \tau_{xz}(z)^2 \,dz}
$$
For the classic parabolic [shear stress distribution](@entry_id:197453) found in a homogeneous rectangular beam under transverse shear, this calculation yields the well-known value $\kappa = 5/6$. Higher-order theories avoid this artifice by using more complex kinematic assumptions (e.g., cubic or higher-order terms in $z$ for in-plane displacements) that allow the [shear strain](@entry_id:175241) to vary through the thickness and satisfy the [traction-free boundary](@entry_id:197683) conditions exactly [@problem_id:2887234].

#### FSDT as a Generalization of Classical Plate Theory

Classical Plate Theory (CPT) can be viewed as a constrained version of FSDT. The CPT kinematic constraint, $\gamma_{xz} = \gamma_{yz} = 0$, is recovered from FSDT under specific conditions [@problem_id:2641529].
1.  **Statically:** In regions of [pure bending](@entry_id:202969) where the [shear force](@entry_id:172634) resultants $Q_x$ and $Q_y$ are identically zero, the FSDT [constitutive law](@entry_id:167255) ($Q_x = \kappa G h \gamma_{xz}$) dictates that the shear strains must also be zero, making the two theories coincide regardless of thickness.
2.  **Energetically:** If one considers the transverse shear rigidity, $C_s = \kappa G h$, as a parameter, the limit $C_s \to \infty$ acts as a penalty term in the potential energy functional. To maintain finite energy, the shear strains must be driven to zero ($\gamma_{xz} \to 0$, $\gamma_{yz} \to 0$). Thus, Kirchhoff-Love [kinematics](@entry_id:173318) are recovered in the limit of infinite shear rigidity.
3.  **Asymptotically:** For very thin plates ($h/L \to 0$), the solution for deflection from FSDT converges to the CPT solution. However, it is a common misconception that the shear strains themselves vanish in this limit. They do not; rather, the shear term in the [energy functional](@entry_id:170311) becomes negligible compared to the bending term.

#### Shear Locking: A Numerical Anomaly in the Thin Plate Limit

When FSDT is implemented using standard low-order $C^0$ continuous finite elements (e.g., bilinear quadrilaterals with nodes at the corners), a numerical pathology known as **[shear locking](@entry_id:164115)** occurs for thin plates [@problem_id:2641533]. This manifests as an excessively stiff, non-physical response where the plate fails to bend properly.

The origin of [shear locking](@entry_id:164115) is a mismatch between the [finite element approximation](@entry_id:166278) spaces for rotations and transverse displacement. In the thin plate limit ($h \to 0$), the plate's behavior is dominated by the bending energy, and the [total potential energy](@entry_id:185512) is minimized only when the shear strain $\boldsymbol{\gamma} = \boldsymbol{\theta} - \nabla w_0$ is nearly zero. The [finite element formulation](@entry_id:164720) attempts to enforce this constraint, $\boldsymbol{\gamma}_h = \boldsymbol{\theta}_h - \nabla w_h \approx \boldsymbol{0}$.

However, the discrete rotation field $\boldsymbol{\theta}_h$ is typically chosen to be continuous across element boundaries, while the gradient of the discrete displacement, $\nabla w_h$, is discontinuous for standard $C^0$ elements. A continuous field cannot equal a discontinuous field. The formulation can only satisfy the constraint in a trivial, non-bending way. As $h$ decreases, the shear energy term, proportional to $h$, becomes a massive penalty relative to the bending energy term, proportional to $h^3$. This forces the solution to suppress all bending to avoid incurring any parasitic [shear strain](@entry_id:175241), thus "locking" the element.

In the language of numerical analysis, this problem arises because the pair of interpolation spaces for $(\boldsymbol{\theta}_h, w_h)$ violates the Ladyzhenskaya–Babuška–Brezzi (LBB) stability condition for the [mixed formulation](@entry_id:171379). Specialized techniques such as reduced/selective integration, [assumed strain methods](@entry_id:176141) (e.g., MITC elements), or mixed interpolation are required to create stable, locking-free finite element formulations of FSDT.