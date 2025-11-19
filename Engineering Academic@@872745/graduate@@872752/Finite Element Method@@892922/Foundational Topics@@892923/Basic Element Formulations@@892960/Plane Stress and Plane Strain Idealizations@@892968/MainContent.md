## Introduction
The analysis of deformable solids is fundamentally a three-dimensional problem, but solving the full 3D equations of elasticity can be computationally prohibitive and often unnecessary. Many engineering structures, by virtue of their geometry, exhibit mechanical behavior that can be accurately captured with simpler, two-dimensional models. The key to effective analysis lies in understanding which simplification is appropriate and what its underlying assumptions and consequences are. This is the central challenge addressed by the [plane stress and plane strain](@entry_id:172357) idealizations—two cornerstone concepts in [solid mechanics](@entry_id:164042) that provide a crucial bridge between complex 3D reality and tractable 2D analysis.

This article provides a graduate-level exploration of these powerful idealizations. It moves beyond simple definitions to uncover the rigorous physical justifications and mathematical derivations that underpin each model. By understanding their distinct origins—one based on stress assumptions and the other on kinematic constraints—you will learn to confidently select the appropriate model for a given engineering problem. We will dissect the profound implications of this choice across various disciplines, from the stability of a dam to the [fracture resistance](@entry_id:197108) of a thin metal sheet.

Over the next three sections, you will gain a comprehensive understanding of these 2D models. In **Principles and Mechanisms**, we will establish the theoretical foundations, deriving the constitutive laws for [plane stress and plane strain](@entry_id:172357) from first principles and contrasting them with the axisymmetric case. Following this, **Applications and Interdisciplinary Connections** will demonstrate the practical utility of these models through case studies in [structural engineering](@entry_id:152273), fracture mechanics, and [computational plasticity](@entry_id:171377), revealing how the choice of idealization directly impacts predicted outcomes. Finally, **Hands-On Practices** will provide a set of targeted problems to reinforce your theoretical knowledge and build practical skills in applying these concepts.

## Principles and Mechanisms

The analysis of deformable solids under external loads is fundamentally a three-dimensional problem. However, many engineering structures possess geometric and loading characteristics that allow for significant simplification. By exploiting these features, we can reduce the governing three-dimensional equations of elasticity to more tractable two-dimensional idealizations. These models, while approximate, provide remarkably accurate results for the dominant physical responses and are computationally far more efficient. This chapter elucidates the principles and mechanisms of the two most fundamental [dimensional reduction](@entry_id:197644) techniques in [solid mechanics](@entry_id:164042): **plane stress** and **plane strain**. We will also contrast these with the **axisymmetric** idealization to provide a broader context for two-dimensional modeling.

### The Plane Stress Idealization

The plane stress model is suited for bodies that are thin in one dimension relative to the other two, such as plates, membranes, and shells. The core idea is to assume a simplified state of stress based on the geometry and boundary conditions.

#### Conceptual Basis: A Traction-Based Constraint

The [plane stress](@entry_id:172193) idealization is fundamentally a **traction-based** or **stress-based** assumption [@problem_id:2588310]. It begins by postulating that the stress components acting perpendicular to the plane of the thin body are negligible. For a body lying in the $x$-$y$ plane with a small thickness in the $z$-direction, this assumption is stated as:
$$
\sigma_{zz} = 0, \quad \tau_{xz} = 0, \quad \tau_{yz} = 0
$$
These conditions are assumed to hold throughout the entire body, not just on its surfaces. The validity of this assumption rests on a rigorous justification rooted in the body's geometry and the nature of the applied loads.

#### Physical Justification and First-Principles Derivation

Consider a thin plate of thickness $h$ occupying the region defined by $(x,y) \in \Omega$ and $z \in [-h/2, h/2]$. A key characteristic of such a body is that the thickness is much smaller than any characteristic in-plane length scale, $L$, over which the geometry or loading varies. This geometric condition is expressed as a [scale separation](@entry_id:152215): $h/L \ll 1$ [@problem_id:2588311].

The physical justification for the plane stress state arises from the boundary conditions on the plate's major faces at $z = \pm h/2$. In a typical scenario, these faces are free of any applied forces, or **traction-free**. The relationship between [internal stress](@entry_id:190887) and [surface traction](@entry_id:198058) $\mathbf{t}$ is given by Cauchy's traction formula, $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma}\mathbf{n}$, where $\mathbf{n}$ is the outward [unit normal vector](@entry_id:178851) to the surface.

For the top face at $z=+h/2$, the normal is $\mathbf{n} = \mathbf{e}_z$. The traction-free condition $\mathbf{t}(\mathbf{e}_z) = \mathbf{0}$ implies:
$$
\begin{pmatrix} \sigma_{xz} \\ \sigma_{yz} \\ \sigma_{zz} \end{pmatrix}_{z=h/2} = \boldsymbol{\sigma} \mathbf{e}_z = \mathbf{0}
$$
This requires that $\sigma_{xz}$, $\sigma_{yz}$, and $\sigma_{zz}$ are all zero on the top surface. A similar argument for the bottom surface ($z=-h/2$, $\mathbf{n}=-\mathbf{e}_z$) yields the same result.

These are exact conditions on the boundary. To justify that these stresses are negligible throughout the plate's *interior*, we must invoke the [equations of equilibrium](@entry_id:193797), $\nabla \cdot \boldsymbol{\sigma} = \mathbf{0}$ (assuming no [body forces](@entry_id:174230)). An [order-of-magnitude analysis](@entry_id:184866) based on the [scale separation](@entry_id:152215) $h/L \ll 1$ reveals that if the in-plane stresses ($\sigma_{xx}, \sigma_{yy}, \tau_{xy}$) are of a characteristic magnitude $\sigma_{in}$, then the transverse shear stresses $\tau_{xz}$ and $\tau_{yz}$ are of order $\sigma_{in}(h/L)$, and the transverse [normal stress](@entry_id:184326) $\sigma_{zz}$ is of order $\sigma_{in}(h/L)^2$. For a thin body, these out-of-plane stress components are asymptotically small compared to the in-plane components. The plane stress idealization therefore consists in setting these small components to zero as a leading-order approximation [@problem_id:2588315].

#### Consequences for Strain: The Poisson Effect

A common misconception is that if the stress in a direction is zero, the strain in that direction must also be zero. This is incorrect for materials with a non-zero Poisson's ratio. The coupling between [normal stresses](@entry_id:260622) and strains in different directions, known as the **Poisson effect**, is central here. The full three-dimensional [constitutive law](@entry_id:167255) for an isotropic material relates the strain component $\epsilon_{zz}$ to the stress components:
$$
\epsilon_{zz} = \frac{1}{E} \left[ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) \right]
$$
where $E$ is the Young's modulus and $\nu$ is the Poisson's ratio. Under the [plane stress condition](@entry_id:168184) $\sigma_{zz} = 0$, this equation becomes:
$$
\epsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})
$$
Since the in-plane stresses $\sigma_{xx}$ and $\sigma_{yy}$ are generally non-zero, the out-of-plane strain $\epsilon_{zz}$ is also generally non-zero. This strain represents the physical thinning or thickening of the plate as it is stretched or compressed in its plane. Therefore, [plane stress](@entry_id:172193) does not imply plane strain [@problem_id:2588352].

#### The Reduced Constitutive Law

To formulate a two-dimensional problem, we need a [constitutive law](@entry_id:167255) relating only the in-plane stresses and strains. This is derived by systematically eliminating the out-of-plane components from the 3D equations. The process, known as [static condensation](@entry_id:176722), correctly embodies the Poisson coupling [@problem_id:2588352].

We start with the 3D strain-stress relations and impose the plane stress conditions $\sigma_{zz}=\tau_{xz}=\tau_{yz}=0$ [@problem_id:2588399]:
$$
\epsilon_{xx} = \frac{1}{E}(\sigma_{xx} - \nu\sigma_{yy})
$$
$$
\epsilon_{yy} = \frac{1}{E}(\sigma_{yy} - \nu\sigma_{xx})
$$
$$
\gamma_{xy} = \frac{1}{G}\tau_{xy} = \frac{2(1+\nu)}{E}\tau_{xy}
$$
Solving the first two equations for $\sigma_{xx}$ and $\sigma_{yy}$ in terms of $\epsilon_{xx}$ and $\epsilon_{yy}$, and rearranging the third for $\tau_{xy}$, we obtain the plane stress [constitutive relations](@entry_id:186508). In matrix form, this is:
$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \tau_{xy} \end{pmatrix} = \mathbf{D}^{ps} \begin{pmatrix} \epsilon_{xx} \\ \epsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$
where $\mathbf{D}^{ps}$ is the **[plane stress constitutive matrix](@entry_id:172920)** [@problem_id:2588325]:
$$
\mathbf{D}^{ps} = \frac{E}{1-\nu^2} \begin{pmatrix} 1  \nu  0 \\ \nu  1  0 \\ 0  0  \frac{1-\nu}{2} \end{pmatrix}
$$

### The Plane Strain Idealization

The plane strain model is applicable to bodies that are very long in one dimension and whose geometry and loading do not vary along that length.

#### Conceptual Basis: A Kinematic Constraint

In direct contrast to [plane stress](@entry_id:172193), the [plane strain](@entry_id:167046) idealization is fundamentally a **kinematic** or **displacement-based** assumption [@problem_id:2588310]. It postulates a specific form for the deformation, from which the state of strain is derived. For a long prismatic body aligned with the $z$-axis, we assume that there is no deformation in the axial direction and that the cross-sectional deformation is the same at every point along the length. This is expressed by a [displacement field](@entry_id:141476) of the form:
$$
u = u(x,y), \quad v = v(x,y), \quad w = \text{constant}
$$
Using the [strain-displacement relations](@entry_id:173321), $\epsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$, this kinematic assumption immediately leads to the **[plane strain](@entry_id:167046) conditions**:
$$
\epsilon_{zz} = \frac{\partial w}{\partial z} = 0, \quad \gamma_{xz} = \frac{\partial u}{\partial z} + \frac{\partial w}{\partial x} = 0, \quad \gamma_{yz} = \frac{\partial v}{\partial z} + \frac{\partial w}{\partial y} = 0
$$

#### Physical Justification and First-Principles Derivation

This idealization is appropriate for structures such as long dams, tunnels, or retaining walls, where the length $L_z$ is much greater than the characteristic in-plane dimensions $L$ (i.e., $L/L_z \ll 1$) [@problem_id:2588311]. If the geometry and loading are independent of the $z$-coordinate, **Saint-Venant's principle** suggests that the state of [stress and strain](@entry_id:137374) will also be independent of $z$ in regions far from the ends. Furthermore, for the [total potential energy](@entry_id:185512) of the body to be minimized under these conditions, any deformation that increases [strain energy](@entry_id:162699) without corresponding external work (such as out-of-plane warping) will be suppressed. The minimum energy state is one of pure two-dimensional deformation in the $x$-$y$ plane, justifying the kinematic assumption of plane strain [@problem_id:2588408].

#### Consequences for Stress: The Reaction Stress

Just as [plane stress](@entry_id:172193) does not imply [plane strain](@entry_id:167046), plane strain does not imply plane stress. To enforce the kinematic constraint $\epsilon_{zz}=0$, a stress must develop in the $z$-direction to prevent the material from deforming due to the Poisson effect. From the 3D constitutive law for $\sigma_{zz}$:
$$
\sigma_{zz} = \lambda(\epsilon_{xx} + \epsilon_{yy} + \epsilon_{zz}) + 2\mu\epsilon_{zz}
$$
where $\lambda$ and $\mu$ are the Lamé parameters. Imposing the plane strain condition $\epsilon_{zz}=0$ yields:
$$
\sigma_{zz} = \lambda(\epsilon_{xx} + \epsilon_{yy})
$$
In terms of Young's modulus and Poisson's ratio, this can be written as $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$. This generally non-zero stress is a **reaction stress** that acts to maintain the [plane strain](@entry_id:167046) state [@problem_id:2588352].

#### The Reduced Constitutive Law

The derivation of the [plane strain constitutive matrix](@entry_id:176145) is more direct than for [plane stress](@entry_id:172193). We start with the 3D stress-strain relations and simply set all out-of-plane strain components to zero [@problem_id:2588318]. For the in-plane components, this gives:
$$
\sigma_{xx} = (\lambda+2\mu)\epsilon_{xx} + \lambda\epsilon_{yy}
$$
$$
\sigma_{yy} = \lambda\epsilon_{xx} + (\lambda+2\mu)\epsilon_{yy}
$$
$$
\tau_{xy} = \mu\gamma_{xy}
$$
Assembling these into matrix form gives $\mathbf{\sigma} = \mathbf{D}^{pe}\mathbf{\epsilon}$, where $\mathbf{D}^{pe}$ is the **[plane strain constitutive matrix](@entry_id:176145)** [@problem_id:2588325]:
$$
\mathbf{D}^{pe} = \frac{E}{(1+\nu)(1-2\nu)} \begin{pmatrix} 1-\nu  \nu  0 \\ \nu  1-\nu  0 \\ 0  0  \frac{1-2\nu}{2} \end{pmatrix}
$$

### A Comparative Framework: Plane Stress, Plane Strain, and Axisymmetry

The distinct origins and applicability of these models can be summarized in a side-by-side comparison [@problem_id:2588334].

| Feature                | Plane Stress                                                                  | Plane Strain                                                                         |
| ---------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **Primary Assumption** | Stress-based: $\sigma_{zz} = \tau_{xz} = \tau_{yz} = 0$                         | Kinematic: $\epsilon_{zz} = \gamma_{xz} = \gamma_{yz} = 0$                             |
| **Geometry**           | "Thin" bodies: thickness $h \ll$ in-plane length $L$                          | "Long" bodies: in-plane length $L \ll$ length $L_z$                                  |
| **Boundary Conditions**| Faces normal to $z$ are traction-free.                                        | Ends normal to $z$ are kinematically constrained.                                    |
| **Out-of-Plane Response**| $\epsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy}) \neq 0$             | $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy}) \neq 0$                                  |
| **Constitutive Matrix**| $\mathbf{D}^{ps} = \frac{E}{1-\nu^2} \begin{pmatrix} 1  \nu  \dots \end{pmatrix}$ | $\mathbf{D}^{pe} = \frac{E}{(1+\nu)(1-2\nu)} \begin{pmatrix} 1-\nu  \nu  \dots \end{pmatrix}$ |

Another powerful two-dimensional idealization is the **axisymmetric model**. This applies to bodies of revolution whose geometry, material properties, and loading are all independent of the circumferential angle $\theta$. The kinematic assumption is that displacements occur only in the radial ($r$) and axial ($z$) directions, i.e., $u_r = u_r(r,z)$ and $u_z = u_z(r,z)$, while the hoop displacement $u_\theta=0$.

A key feature of the axisymmetric model is the presence of a **[hoop strain](@entry_id:174548)**, $\epsilon_{\theta} = u_r/r$, which arises from the change in circumference as a point moves radially. This means that even though the problem is modeled in a 2D ($r-z$) plane, it implicitly accounts for a third dimension of deformation. The resulting formulation involves four stress components ($\sigma_r, \sigma_z, \sigma_\theta, \tau_{rz}$) and four strain components ($\epsilon_r, \epsilon_z, \epsilon_\theta, \gamma_{rz}$). The [constitutive matrix](@entry_id:164908) is a $4 \times 4$ matrix derived directly from the full 3D law [@problem_id:2588325].

### Computational Implications: Incompressibility and Volumetric Locking

The differences between the [plane stress and plane strain](@entry_id:172357) [constitutive models](@entry_id:174726) become stark when considering materials that are nearly incompressible, i.e., materials whose Poisson's ratio $\nu$ approaches $0.5$.

In the limit $\nu \to 0.5$, the denominator term $(1-2\nu)$ in the plane strain matrix $\mathbf{D}^{pe}$ approaches zero. Consequently, the coefficients of the matrix related to volumetric deformation diverge to infinity. An analysis of the matrix's eigenvalues shows that the eigenvalue corresponding to in-plane volumetric strain ($k_{vol} = 2\lambda + 2\mu$) tends to infinity, while eigenvalues for deviatoric (shear) strain remain bounded [@problem_id:2588362]. This signifies an infinitely stiff response to any change in volume, which is physically correct for an [incompressible material](@entry_id:159741).

However, this property causes a severe numerical artifact in low-order displacement-based finite elements known as **volumetric locking**. The polynomial displacement fields of these elements are too simple to satisfy the incompressibility constraint ($\operatorname{tr}(\boldsymbol{\varepsilon}) = \epsilon_{xx} + \epsilon_{yy} \approx 0$) at all points within the element without becoming overly constrained. The element becomes artificially rigid and unable to represent valid deformation modes like bending, leading to grossly inaccurate results.

In contrast, the [plane stress](@entry_id:172193) matrix $\mathbf{D}^{ps}$ has a denominator of $(1-\nu^2)$, which remains bounded and well-behaved as $\nu \to 0.5$. A thin plate can always satisfy the incompressibility constraint by deforming in the out-of-plane ($z$) direction. Consequently, plane stress formulations do not suffer from [volumetric locking](@entry_id:172606).

This pathology in plane strain analysis is well-known, and several effective remedies have been developed. These include **[selective reduced integration](@entry_id:168281)**, where the stiff volumetric part of the element's [stiffness matrix](@entry_id:178659) is integrated with a lower-order [quadrature rule](@entry_id:175061), and **[mixed formulations](@entry_id:167436)** (e.g., u-p elements), which treat pressure as an independent field to enforce the incompressibility constraint in a weaker, more stable manner [@problem_id:2588362]. Understanding the fundamental principles of these idealizations is therefore not just a theoretical exercise; it is essential for the correct and effective application of computational simulation tools.