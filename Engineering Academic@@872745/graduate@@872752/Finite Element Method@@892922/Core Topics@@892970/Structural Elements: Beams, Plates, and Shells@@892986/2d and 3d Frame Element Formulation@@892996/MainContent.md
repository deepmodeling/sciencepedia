## Introduction
The frame element is a cornerstone of computational structural mechanics, providing an efficient and powerful means to model skeletal structures like buildings, bridges, and trusses within the finite element method. While introductory texts cover its basic application, a deeper, more robust understanding requires a rigorous examination of its underlying theoretical formulation, its inherent limitations, and its extensibility to complex, real-world phenomena. This article bridges that gap, moving from fundamental principles to advanced applications and practical implementation.

Over the next chapters, you will gain a comprehensive understanding of [frame element formulation](@entry_id:170837). The "Principles and Mechanisms" chapter will deconstruct the element from the ground up, deriving its stiffness properties from both Euler-Bernoulli and Timoshenko beam theories and exploring the critical process of transforming and assembling local contributions into a global system. Next, "Applications and Interdisciplinary Connections" will demonstrate the versatility of the core formulation, showing how it can be extended to model buckling, [material nonlinearity](@entry_id:162855), dynamics, and [soil-structure interaction](@entry_id:755022), while also revealing surprising connections to other scientific fields. Finally, "Hands-On Practices" will provide guided exercises to solidify these concepts, tackling challenges from implementing nonlinear solvers to correctly modeling structural details like hinges.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanical formulations that underpin two- and three-dimensional frame elements in the [finite element method](@entry_id:136884). We will begin by establishing the kinematic degrees of freedom that define the element's state, proceed to the formulation of stiffness and mass properties based on classical and shear-deformable beam theories, explore the procedures for assembling element contributions into a global structural model, and conclude with an introduction to advanced formulations for [geometric nonlinearity](@entry_id:169896).

### Nodal Degrees of Freedom: From 2D to 3D

The formulation of a frame element begins with a precise definition of its **degrees of freedom (DOFs)**. In the context of beam and frame elements, we make a crucial idealization: the cross-section of the member is assumed to be rigid. This means that at any point along the member's axis, the cross-section can translate and rotate as a rigid body, but it does not deform in its own plane. Consequently, the DOFs at a node of a frame element are precisely the parameters required to describe the [rigid body motion](@entry_id:144691) of the cross-section at that nodal point [@problem_id:2538957].

For a **planar frame element**, where all motion is confined to a two-dimensional plane (e.g., the local $x$-$y$ plane), a rigid body has three degrees of freedom. These correspond to:
- **Two translational DOFs**: These are the displacements of the cross-section's [centroid](@entry_id:265015) along the two coordinate axes. In a local coordinate system where the $x$-axis aligns with the element, these are $u_x$ (axial translation) and $u_y$ (transverse translation).
- **One rotational DOF**: This is the rotation of the cross-section within the plane of motion. For motion in the $x$-$y$ plane, this is a rotation about the axis perpendicular to the plane, the $z$-axis, denoted as $\theta_z$. This rotation is directly associated with in-plane bending.

Therefore, each node of a 2D frame element possesses three DOFs: $\{u_x, u_y, \theta_z\}$.

For a **spatial (3D) frame element**, which can deform and move in three-dimensional space, the [kinematics](@entry_id:173318) of a rigid body require six degrees of freedom. These are partitioned into three translations and three rotations:
- **Three translational DOFs**: These are the displacements of the centroid along the three global or local axes, typically denoted $u_x$, $u_y$, and $u_z$. In a local frame, $u_x$ represents axial displacement, while $u_y$ and $u_z$ represent transverse displacements in two orthogonal planes.
- **Three rotational DOFs**: These are the rotations of the cross-section about the three axes, denoted $\theta_x$, $\theta_y$, and $\theta_z$. These rotations have distinct physical meanings:
    - $\theta_x$: Rotation about the member's own longitudinal axis, representing **torsion** or twist.
    - $\theta_y$: Rotation about the local $y$-axis, representing **bending** in the $x$-$z$ plane.
    - $\theta_z$: Rotation about the local $z$-axis, representing **bending** in the $x$-$y$ plane.

Thus, each node of a 3D frame element possesses six degrees of freedom: $\{u_x, u_y, u_z, \theta_x, \theta_y, \theta_z\}$. Understanding this foundational concept is critical, as these DOFs are the primary variables that the [finite element formulation](@entry_id:164720) seeks to solve for [@problem_id:2538957].

### The Euler-Bernoulli Frame Element: A Classical Approach

The Euler-Bernoulli beam theory provides the classical foundation for modeling slender frame elements where the effects of [transverse shear deformation](@entry_id:176673) are considered negligible.

#### Kinematic Assumptions

The central kinematic hypothesis of Euler-Bernoulli theory is that **plane cross-sections initially normal to the member's centroidal axis remain plane and normal to the deformed centroidal axis** after deformation. This powerful assumption has direct mathematical consequences. Let us consider a 2D element in the $x$-$y$ plane with transverse displacement $v_0(x)$. The "plane" part of the assumption implies that the axial displacement $u_x$ varies linearly over the cross-section. The "normal" part implies that the rotation of the cross-section, $\theta_z(x)$, is not an independent variable but is dictated by the slope of the deformed centroidal axis, $\frac{dv_0}{dx}$.

For small rotations, $\theta_z(x) = \frac{dv_0}{dx}$. This relationship can be understood more fundamentally by examining the transverse shear strain, $\gamma_{xy}$. For a displacement field where $u_x(x,y) = u_0(x) - y\,\theta_z(x)$ and $u_y(x,y) = v_0(x)$, the engineering shear strain is given by:
$$ \gamma_{xy} = \frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x} = -\theta_z(x) + \frac{dv_0}{dx} $$
The Euler-Bernoulli assumption is equivalent to neglecting transverse shear strain, i.e., setting $\gamma_{xy} = 0$. This directly enforces the kinematic constraint $\theta_z(x) = \frac{dv_0}{dx}$ [@problem_id:2538855].

#### Interpolation and Shape Functions

To build a finite element, we must choose appropriate interpolation functions (shape functions) for the displacement fields. The choice is dictated by the physics of the deformation modes.

For **[axial deformation](@entry_id:180213)**, governed by the displacement $u_0(x)$, a key requirement for a valid finite element is its ability to represent a state of constant strain exactly. This is known as the **constant-strain patch test**. For [axial strain](@entry_id:160811), $\varepsilon_x = du_0/dx$. To represent a constant strain, the displacement $u_0(x)$ must be a linear function of $x$. A two-node element must therefore use linear interpolation for the axial [displacement field](@entry_id:141476). Given nodal axial displacements $u_1$ and $u_2$ at $x=0$ and $x=L$, the [displacement field](@entry_id:141476) is:
$$ u_0(x) = \left(1 - \frac{x}{L}\right)u_1 + \left(\frac{x}{L}\right)u_2 = N_1(x)u_1 + N_2(x)u_2 $$
The derivative, $\frac{du_0}{dx} = \frac{u_2-u_1}{L}$, is constant, proving that this simple [linear interpolation](@entry_id:137092) is not only sufficient but also necessary to satisfy this fundamental convergence criterion [@problem_id:2538857].

For **flexural (bending) deformation**, the requirements are more stringent. The governing differential equation for an Euler-Bernoulli beam is a fourth-order equation: $EI \frac{d^4v_0}{dx^4} = q(x)$, where $q(x)$ is the distributed transverse load. To derive the [weak form](@entry_id:137295), we multiply by a [test function](@entry_id:178872) $\eta(x)$ and integrate by parts twice. This leads to a [bilinear form](@entry_id:140194) involving second derivatives of both the [trial function](@entry_id:173682) $v_0$ and the test function $\eta$:
$$ \int_0^L EI v_0''(x) \eta''(x) \,dx = \dots $$
The [strain energy](@entry_id:162699) of the beam, $\frac{1}{2} \int_0^L EI (v_0''(x))^2 dx$, must be finite. This requires that the second derivative $v_0''$ be square-integrable. The function space for which this holds is the Sobolev space $H^2$. For a conforming [finite element method](@entry_id:136884), where the global approximation is formed by [piecewise polynomials](@entry_id:634113), membership in $H^2$ over the entire domain demands that the approximation be **$C^1$-continuous**. This means that both the function itself (the transverse displacement $v_0$) and its first derivative (the slope $\frac{dv_0}{dx}$) must be continuous across element boundaries [@problem_id:2538947]. This requirement is unique to bending in Euler-Bernoulli theory; axial displacement and torsion are governed by second-order equations, whose weak forms only involve first derivatives, thus requiring only $C^0$ continuity (continuity of the function itself).

To achieve $C^1$ continuity, we use **cubic Hermite polynomials** as shape functions for the transverse displacement $v_0(x)$. A cubic polynomial has four coefficients, which can be uniquely determined by the four nodal DOFs associated with bending: the displacements $v_1, v_2$ and the rotations $\theta_1, \theta_2$ at the two nodes. Since $\theta = dv_0/dx$, these nodal DOFs are precisely the values of the function and its first derivative at the element ends.

#### The Element Stiffness Matrix

With the shape functions defined, we can derive the [element stiffness matrix](@entry_id:139369) from the [strain energy](@entry_id:162699). As axial and bending behaviors are uncoupled in a straight, prismatic element, we can derive their stiffness contributions separately and superimpose them.

The **axial [stiffness matrix](@entry_id:178659)** is derived from the [strain energy](@entry_id:162699) $U_{axial} = \frac{1}{2} \int_0^L EA (\varepsilon_x)^2 dx$. Using the linear shape functions, this yields the familiar $2 \times 2$ matrix relating nodal forces to nodal axial displacements $(u_1, u_2)$.

The **bending stiffness matrix** is derived from the [strain energy](@entry_id:162699) $U_{bending} = \frac{1}{2} \int_0^L EI (\kappa)^2 dx$, where the curvature is $\kappa = \frac{d^2v_0}{dx^2}$. Using the second derivatives of the cubic Hermite [shape functions](@entry_id:141015), this yields a $4 \times 4$ matrix relating nodal shear forces and moments to nodal transverse displacements and rotations $(v_1, \theta_1, v_2, \theta_2)$.

By assembling these contributions according to the full nodal DOF vector for a 2D frame element, $\mathbf{q}_e = \begin{pmatrix}u_1  v_1  \theta_1  u_2  v_2  \theta_2\end{pmatrix}^{\mathsf T}$, we obtain the complete $6 \times 6$ local [stiffness matrix](@entry_id:178659) $\mathbf{k}_e$ [@problem_id:2538922]:
$$
\mathbf{k}_e = \begin{pmatrix}
\frac{EA}{L} & 0 & 0 & -\frac{EA}{L} & 0 & 0 \\
0 & \frac{12EI}{L^3} & \frac{6EI}{L^2} & 0 & -\frac{12EI}{L^3} & \frac{6EI}{L^2} \\
0 & \frac{6EI}{L^2} & \frac{4EI}{L} & 0 & -\frac{6EI}{L^2} & \frac{2EI}{L} \\
-\frac{EA}{L} & 0 & 0 & \frac{EA}{L} & 0 & 0 \\
0 & -\frac{12EI}{L^3} & -\frac{6EI}{L^2} & 0 & \frac{12EI}{L^3} & -\frac{6EI}{L^2} \\
0 & \frac{6EI}{L^2} & \frac{2EI}{L} & 0 & -\frac{6EI}{L^2} & \frac{4EI}{L}
\end{pmatrix}
$$
This matrix exactly represents the stiffness properties of a linear elastic Euler-Bernoulli [beam element](@entry_id:177035).

### The Timoshenko Frame Element: Incorporating Shear Deformation

The Euler-Bernoulli theory is highly accurate for slender beams. However, for deep beams or members made of materials with a low [shear modulus](@entry_id:167228) relative to their [elastic modulus](@entry_id:198862), [transverse shear deformation](@entry_id:176673) can become significant. The **Timoshenko [beam theory](@entry_id:176426)** provides a more general model that accounts for this effect.

#### Kinematic Assumptions

Timoshenko theory relaxes the "normalcy" constraint of Euler-Bernoulli theory. It assumes that **plane sections remain plane, but are not necessarily normal to the deformed centroidal axis**. This seemingly small change has a profound impact on the formulation. The rotation of the cross-section, $\theta(x)$, is no longer tied to the slope of the centerline, $\frac{dv}{dx}$. Instead, $\theta(x)$ and $v(x)$ are treated as two **independent** fields [@problem_id:2538934].

The transverse [shear strain](@entry_id:175241), $\gamma_{xy} = \frac{dv}{dx} - \theta(x)$, is now generally non-zero. The value of $\gamma_{xy}$ represents the difference between the slope of the centerline and the rotation of the cross-section. Because the displacement and rotation fields are independent, the element requires only $C^0$ continuity for both, which simplifies the choice of [shape functions](@entry_id:141015).

#### Interpolation and Shear Locking

Since $v(x)$ and $\theta(x)$ are independent, we must choose separate interpolation functions for each. A natural first choice might be to use simple linear Lagrange polynomials for both fields. However, this leads to a notorious numerical pathology known as **[shear locking](@entry_id:164115)**.

Shear locking occurs in the thin-beam limit. As a beam becomes very slender, its shear stiffness becomes very large relative to its bending stiffness. In the potential energy expression, the shear [strain energy](@entry_id:162699) term, $\frac{1}{2} \int \kappa_s G A (v' - \theta)^2 dx$, dominates. To keep the energy bounded, the discrete shear strain $v_h' - \theta_h$ must approach zero. If we use [linear interpolation](@entry_id:137092) for both $v_h$ and $\theta_h$, then $v_h'$ is a constant, while $\theta_h$ is linear. The constraint $v_h' = \theta_h$ can only be satisfied if the linear function $\theta_h$ is also a constant, which severely restricts the element's ability to bend. The element becomes artificially "locked" in shear, exhibiting far too much [bending stiffness](@entry_id:180453).

To avoid [shear locking](@entry_id:164115), the interpolation spaces for displacement, $\mathcal{S}_v$, and rotation, $\mathcal{S}_\theta$, must satisfy a compatibility condition. A key insight is that the space of derivatives of the displacement interpolation, $\mathcal{D}\mathcal{S}_v = \{v' | v \in \mathcal{S}_v\}$, must be "rich" enough to represent the rotation interpolation space $\mathcal{S}_\theta$. Using linear functions for both ($P_1$ for $v$ and $P_1$ for $\theta$) fails this, as the space of derivatives is the space of constants ($P_0$), which cannot represent all linear functions in $\mathcal{S}_\theta$.

Several advanced strategies exist to create [locking-free elements](@entry_id:751420) without resorting to numerical fixes like reduced integration. One such method involves choosing a higher-order [polynomial space](@entry_id:269905) for displacement than for rotation (e.g., cubic for $v_h$ and linear for $\theta_h$) and using a modified formulation based on projecting the [shear strain](@entry_id:175241) appropriately. These methods ensure that the element can represent a [pure bending](@entry_id:202969) state without spurious shear strains, even as the beam becomes very thin [@problem_id:2538871].

### Assembling the Global System

Individual element matrices must be transformed into a common global coordinate system and assembled to form the model of the entire structure.

#### Coordinate Transformations: From Local to Global

Each frame element is most easily formulated in a **[local coordinate system](@entry_id:751394)** (e.g., with the $x'$-axis aligned along the member). The full structure, however, exists in a single **global coordinate system** ($X,Y,Z$). We must therefore establish a transformation between these frames.

For a 3D frame element connecting global node coordinates $\mathbf{r}_A$ and $\mathbf{r}_B$, a local right-handed [orthonormal basis](@entry_id:147779) $\{\hat{\boldsymbol{e}}_{x}, \hat{\boldsymbol{e}}_{y}, \hat{\boldsymbol{e}}_{z}\}$ can be constructed.
1. The local axial direction $\hat{\boldsymbol{e}}_{x}$ is defined by the normalized vector from node A to B.
2. An auxiliary direction $\hat{\boldsymbol{e}}_{z}$ is found by taking the [cross product](@entry_id:156749) of $\hat{\boldsymbol{e}}_{x}$ with a non-collinear global reference vector (e.g., the global Z-axis, $\mathbf{V}_{ref}=(0,0,1)$) and normalizing the result.
3. The final direction $\hat{\boldsymbol{e}}_{y}$ is found by the [cross product](@entry_id:156749) $\hat{\boldsymbol{e}}_{z} \times \hat{\boldsymbol{e}}_{x}$ to complete the [right-handed system](@entry_id:166669) [@problem_id:2538863].

The components of these local [unit vectors](@entry_id:165907), expressed in the global coordinate system, form the columns of a $3 \times 3$ **rotation matrix**, $\mathbf{E}$. This matrix rotates vector components from the local frame to the global frame. Because both displacement vectors and (infinitesimal) rotation vectors transform in the same way, the full $12 \times 12$ element transformation matrix $\mathbf{T}$ is constructed as a [block-diagonal matrix](@entry_id:145530):
$$ \mathbf{T} = \begin{pmatrix}
\mathbf{E} & \mathbf{0} & \mathbf{0} & \mathbf{0} \\
\mathbf{0} & \mathbf{E} & \mathbf{0} & \mathbf{0} \\
\mathbf{0} & \mathbf{0} & \mathbf{E} & \mathbf{0} \\
\mathbf{0} & \mathbf{0} & \mathbf{0} & \mathbf{E}
\end{pmatrix} $$
This matrix relates the 12 local DOFs to the 12 global DOFs for the element, i.e., $\mathbf{d}^g = \mathbf{T} \mathbf{d}^l$. Since $\mathbf{T}$ is composed of pure rotation matrices, it is orthogonal and its determinant is always 1 [@problem_id:2538863].

#### Assembling Global Matrices and Load Vectors

The transformation rules for stiffness matrices and force vectors are derived from the principle that energy and work are [scalar invariants](@entry_id:193787), meaning their values must be independent of the coordinate system.

The [strain energy](@entry_id:162699) in an element can be written as $U_e = \frac{1}{2} (\mathbf{d}^l)^T \mathbf{k}_l \mathbf{d}^l$ in [local coordinates](@entry_id:181200) and $U_e = \frac{1}{2} (\mathbf{d}^g)^T \mathbf{k}_g \mathbf{d}^g$ in global coordinates. Substituting $\mathbf{d}^l = \mathbf{T}^{-1} \mathbf{d}^g = \mathbf{T}^T \mathbf{d}^g$ (since $\mathbf{T}$ is orthogonal) into the first expression and equating it with the second reveals the transformation rule for the stiffness matrix:
$$ \mathbf{k}_g = \mathbf{T}^T \mathbf{k}_l \mathbf{T} $$
The same logic applies to the [consistent mass matrix](@entry_id:174630), which is derived from kinetic energy: $\mathbf{m}_g = \mathbf{T}^T \mathbf{m}_l \mathbf{T}$ [@problem_id:2538892].

Loads applied along the element's length must be converted into **[consistent nodal loads](@entry_id:176954)**, which are work-equivalent forces and moments at the nodes. This is achieved by invoking the [principle of virtual work](@entry_id:138749). The [virtual work](@entry_id:176403) done by a distributed load $p(x)$ over a [virtual displacement](@entry_id:168781) field $\delta v(x)$ must equal the [virtual work](@entry_id:176403) done by the [consistent nodal forces](@entry_id:204135) $\mathbf{f}_e$ over the virtual nodal displacements $\delta \mathbf{d}$:
$$ \delta W_{ext} = \int_0^L p(x) \delta v(x) \,dx = (\delta \mathbf{d})^T \mathbf{f}_e $$
By substituting the interpolation $\delta v(x) = \mathbf{N}(x) \delta \mathbf{d}$, we find the general formula for the [consistent load vector](@entry_id:163156): $\mathbf{f}_e = \int_0^L \mathbf{N}(x)^T p(x) \,dx$. For a uniform transverse load $w$ on an Euler-Bernoulli element, this integral yields the well-known fixed-end reactions: transverse forces of $wL/2$ and moments of $\pm wL^2/12$ at the nodes. This approach is energetically consistent and far more accurate than simply "lumping" the total force at the nodes, as it correctly accounts for the work done by the load during rotational virtual displacements [@problem_id:2538811].

The nodal force vector transforms from local to global coordinates via $\mathbf{f}_g = \mathbf{T}^T \mathbf{f}_l$. This again follows from work invariance: $(\mathbf{d}^g)^T \mathbf{f}_g = (\mathbf{d}^l)^T \mathbf{f}_l$.

The final **assembly process** involves iterating through all elements in the model. For each element, the local stiffness, mass, and load vectors are computed and then transformed to the global frame. The entries of these global element matrices and vectors are then added into the correct locations in the overall global system matrices ($\mathbf{K}$, $\mathbf{M}$) and global [load vector](@entry_id:635284) ($\mathbf{F}$), according to the element's connectivity map. This "[scatter-add](@entry_id:145355)" procedure superimposes the contributions of all elements to form the final system of equations to be solved [@problem_id:2538892].

### Introduction to Geometric Nonlinearity

When a structure undergoes large displacements and rotations, the linear assumptions of the preceding sections are no longer valid. The analysis enters the realm of **[geometric nonlinearity](@entry_id:169896)**. A common and important case is that of **[large rotations](@entry_id:751151) and small strains**, typical of flexible, slender structures. Two prominent formulations for this class of problems are the Corotational and Updated Lagrangian methods.

#### Formulations for Large Rotations and Small Strains

The fundamental challenge in large rotation analysis is satisfying the **[principle of objectivity](@entry_id:185412)** (or [material frame-indifference](@entry_id:178419)), which states that the material's constitutive response must be independent of any superimposed [rigid-body motion](@entry_id:265795).

The **Corotational (CR) formulation** addresses this challenge in a physically intuitive way. It decomposes the motion of each element into a large rigid-body part and a small deformational part. This is achieved by defining a **corotating coordinate system** that translates and rotates with the element. The element's deformation is then measured relative to this local, moving frame. Because the [rigid-body rotation](@entry_id:268623) has been "filtered out," the remaining deformation is small, allowing the standard linear, small-strain [element stiffness matrix](@entry_id:139369) to be used to compute local [internal forces](@entry_id:167605). These forces are then transformed back to the global frame to compute the residual for the nonlinear solution process. The CR approach is known for its computational efficiency and relatively straightforward implementation, making it a popular choice for extending [linear codes](@entry_id:261038) to handle [geometric nonlinearity](@entry_id:169896) [@problem_id:2538869].

The **Updated Lagrangian (UL) formulation** is a more general approach derived directly from continuum mechanics. In this formulation, the configuration at the end of the previous successful load step is used as the reference configuration for the current increment. The governing equations are written in rate form. Because the material rotates between increments, standard time derivatives of stress tensors are not objective. Therefore, the UL formulation requires the use of an **[objective stress rate](@entry_id:168809)**, such as the Jaumann or Green-Naghdi rate, in the [constitutive law](@entry_id:167255) to ensure objectivity. While the UL framework is more general and can naturally handle [finite strain plasticity](@entry_id:175182), its application to the specific case of small-strain, large-rotation problems involves greater implementation complexity (e.g., correct implementation of the objective rate and the corresponding consistent tangent) without necessarily offering an accuracy advantage over a well-implemented [corotational formulation](@entry_id:177858) [@problem_id:2538869]. A common misconception is that UL formulations avoid the complexities of handling finite 3D rotations; in fact, both CR and UL methods require a rigorous and explicit procedure for updating nodal orientations at each step, as finite rotations are not vector quantities.