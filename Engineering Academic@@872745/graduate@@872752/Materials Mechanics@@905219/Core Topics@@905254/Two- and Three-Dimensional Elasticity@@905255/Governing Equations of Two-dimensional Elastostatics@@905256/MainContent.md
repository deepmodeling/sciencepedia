## Introduction
The [theory of elasticity](@entry_id:184142) provides the fundamental framework for analyzing how solid objects deform and carry loads. For a vast range of engineering structures—from thin plates to long dams—the mechanical behavior can be accurately captured by simplifying the full three-dimensional problem into a more tractable two-dimensional model. However, to apply this powerful simplification effectively, one must first master its theoretical underpinnings. This article addresses the need for a systematic development of the governing equations of two-dimensional [elastostatics](@entry_id:198298), which form the bedrock of [stress analysis](@entry_id:168804) in solid mechanics.

This article is structured to build your expertise from the ground up. In the "Principles and Mechanisms" chapter, we will rigorously derive the core equations of 2D elasticity, including the kinematic, kinetic, and constitutive laws, and introduce the primary solution methodologies. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how this theory is applied to solve critical real-world problems, from stress concentrations in engineering components to modeling in biomechanics and materials science. Finally, the "Hands-On Practices" section provides a set of targeted problems to solidify your understanding and test your practical application of these concepts. We begin by establishing the foundational principles and mechanisms that govern the static response of elastic materials.

## Principles and Mechanisms

The formulation of any problem in [elastostatics](@entry_id:198298) rests upon three foundational pillars: the [kinematic equations](@entry_id:173032) relating strain to displacement, the kinetic [equations of equilibrium](@entry_id:193797) relating stress variations to [body forces](@entry_id:174230), and the [constitutive law](@entry_id:167255) relating stress to strain. In this chapter, we systematically develop these governing equations for the case of two-dimensional (2D) linear elasticity, which serves as a powerful model for a wide range of engineering applications. We will then explore the primary analytical and [variational methods](@entry_id:163656) used to solve the resulting [boundary value problems](@entry_id:137204).

### Kinematics: The Geometry of Deformation

The first step in describing the mechanical state of a continuum is to characterize its deformation. We describe the motion of material points from an undeformed reference configuration to a deformed current configuration by a [displacement vector field](@entry_id:196067), which in a 2D Cartesian plane is denoted by $\mathbf{u}(x,y) = u(x,y)\mathbf{e}_x + v(x,y)\mathbf{e}_y$.

Deformation, or **strain**, is the local measure of how lengths and angles change. The full, geometrically exact measure is given by the nonlinear Green-Lagrange strain tensor. However, the theory of [linear elasticity](@entry_id:166983) is predicated on the assumption of **small deformations**. More precisely, this theory is valid under the **small [displacement gradient](@entry_id:165352) assumption**, which posits that all components of the [displacement gradient tensor](@entry_id:748571), $\nabla\mathbf{u}$, are much less than unity, i.e., $|\partial u_i / \partial x_j| \ll 1$. This condition implies that both local strains and local rigid-body rotations are small. Under this assumption, the nonlinear terms in the Green-Lagrange tensor, which are quadratic in the displacement gradients, become negligible compared to the linear terms.

This [linearization](@entry_id:267670) yields the **[infinitesimal strain tensor](@entry_id:167211)**, denoted $\boldsymbol{\varepsilon}$, which is defined as the symmetric part of the [displacement gradient tensor](@entry_id:748571) [@problem_id:2889757].

$$
\boldsymbol{\varepsilon} = \frac{1}{2} \left( \nabla\mathbf{u} + (\nabla\mathbf{u})^{\mathsf{T}} \right)
$$

This definition ensures that $\boldsymbol{\varepsilon}$ is a proper tensor quantity that is zero for any [rigid-body motion](@entry_id:265795) (translation or small rotation), correctly capturing only the shape and volume changes. In terms of the 2D displacement components $(u, v)$, the components of the [strain tensor](@entry_id:193332) are given by:

$$
\varepsilon_{xx} = \frac{\partial u}{\partial x}
$$

$$
\varepsilon_{yy} = \frac{\partial v}{\partial y}
$$

$$
\varepsilon_{xy} = \varepsilon_{yx} = \frac{1}{2} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right)
$$

Here, $\varepsilon_{xx}$ and $\varepsilon_{yy}$ are the **normal strains**, representing the fractional change in length of line elements originally oriented along the $x$ and $y$ axes, respectively. The component $\varepsilon_{xy}$ is the **tensorial [shear strain](@entry_id:175241)**, which quantifies half the change in the angle between two line elements originally oriented along the $x$ and $y$ axes. It is common in engineering practice to use the **engineering shear strain**, $\gamma_{xy}$, defined as $\gamma_{xy} = 2\varepsilon_{xy} = (\partial u/\partial y + \partial v/\partial x)$.

### Kinetics: The Balance of Forces

The second pillar concerns the forces acting on and within the body. Internal forces are described by the **Cauchy stress tensor**, $\boldsymbol{\sigma}$. The component $\sigma_{ij}$ represents the $i$-th component of the force acting on a surface with a normal oriented in the $j$-th direction, per unit area. On any arbitrary internal or external surface with an outward [unit normal vector](@entry_id:178851) $\mathbf{n}$, the force per unit area is given by the **traction vector** $\mathbf{t}$. Cauchy's fundamental theorem establishes the linear relationship between traction and stress [@problem_id:2889739]:

$$
\mathbf{t} = \boldsymbol{\sigma}\mathbf{n} \quad \text{or in components,} \quad t_i = \sigma_{ij}n_j
$$

For a body to be in [static equilibrium](@entry_id:163498), the [net force](@entry_id:163825) and net moment acting on any arbitrary portion of it must be zero. Applying the principle of [balance of linear momentum](@entry_id:193575) to an infinitesimal [control volume](@entry_id:143882), and using the [divergence theorem](@entry_id:145271), yields the **local [equilibrium equations](@entry_id:172166)**:

$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{b} = \mathbf{0}
$$

where $\mathbf{b}$ is the body force vector per unit volume (e.g., gravity). In 2D Cartesian coordinates, this vector equation expands into two scalar partial differential equations:

$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{yx}}{\partial y} + b_x = 0
$$

$$
\frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + b_y = 0
$$

Furthermore, applying the principle of [balance of angular momentum](@entry_id:181848) to an infinitesimal element, in the absence of distributed body couples, reveals a crucial property of the stress tensor: it must be symmetric.

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^{\mathsf{T}} \quad \text{or in components,} \quad \sigma_{ij} = \sigma_{ji}
$$

In two dimensions, this means $\sigma_{xy} = \sigma_{yx}$. This symmetry reduces the number of independent stress components in 2D from four to three: $\sigma_{xx}$, $\sigma_{yy}$, and $\sigma_{xy}$. Consequently, we can write the first [equilibrium equation](@entry_id:749057) using $\sigma_{xy}$ instead of $\sigma_{yx}$.

### Constitutive Law: The Material Response

The kinematic and kinetic equations are universal, applying to any continuum. The third pillar, the **[constitutive law](@entry_id:167255)** or **Hooke's Law**, introduces the material-specific behavior by relating stress to strain. For a homogeneous, isotropic, linearly elastic material, the most general linear relationship between the symmetric [stress and strain](@entry_id:137374) tensors is given by two material constants, the **Lamé parameters** $\lambda$ and $\mu$ [@problem_id:2889796]:

$$
\boldsymbol{\sigma} = \lambda \, \mathrm{tr}(\boldsymbol{\varepsilon}) \mathbf{I} + 2\mu \boldsymbol{\varepsilon}
$$

Here, $\mathbf{I}$ is the identity tensor and $\mathrm{tr}(\boldsymbol{\varepsilon}) = \varepsilon_{kk}$ is the trace of the strain tensor, representing the [volumetric strain](@entry_id:267252). The parameter $\mu$ is the shear modulus, also denoted by $G$, which governs the material's resistance to [shear deformation](@entry_id:170920).

While the Lamé parameters provide a compact mathematical representation, it is often more convenient to use the [engineering constants](@entry_id:199413): **Young's modulus ($E$)** and **Poisson's ratio ($\nu$)**. These are determined from a simple [uniaxial tension test](@entry_id:195375). By analyzing the stress-strain state in such a test, we can derive the relationships between the two sets of constants:

$$
\mu = \frac{E}{2(1+\nu)}
$$

$$
\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}
$$

These relations allow us to express the [constitutive law](@entry_id:167255) in the familiar form involving $E$ and $\nu$.

### Two-Dimensional Idealizations

Many three-dimensional elasticity problems can be reasonably approximated by 2D models under specific geometric and loading conditions. The two primary idealizations are [plane stress and plane strain](@entry_id:172357).

#### Plane Stress

The **plane stress** assumption is appropriate for thin, plate-like structures loaded in the plane of the plate, with no forces on their flat faces [@problem_id:2889738]. The defining assumption is that the stress components acting out of the plane are zero throughout the thickness:

$$
\sigma_{zz} = \sigma_{xz} = \sigma_{yz} = 0
$$

This is a kinetic assumption. Under this condition, the out-of-plane [normal strain](@entry_id:204633) $\varepsilon_{zz}$ is generally non-zero due to the Poisson effect. From the 3D Hooke's law, we find $\varepsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})$ [@problem_id:2889774]. By enforcing the [plane stress condition](@entry_id:168184) in the 3D [constitutive equations](@entry_id:138559), we can derive a reduced 2D stress-strain relationship. Expressed in matrix form relating the stress vector $\{\sigma_{xx}, \sigma_{yy}, \sigma_{xy}\}^{\mathsf{T}}$ to the engineering strain vector $\{\varepsilon_{xx}, \varepsilon_{yy}, \gamma_{xy}\}^{\mathsf{T}}$, the plane stress [constitutive law](@entry_id:167255) is [@problem_id:2889781]:

$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix} = \frac{E}{1-\nu^2} \begin{pmatrix} 1 & \nu & 0 \\ \nu & 1 & 0 \\ 0 & 0 & \frac{1-\nu}{2} \end{pmatrix} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$

The inverse of this relation, giving strains from stresses, is given by the [compliance matrix](@entry_id:185679):

$$
\begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix} = \frac{1}{E} \begin{pmatrix} 1 & -\nu & 0 \\ -\nu & 1 & 0 \\ 0 & 0 & 2(1+\nu) \end{pmatrix} \begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix}
$$

#### Plane Strain

The **[plane strain](@entry_id:167046)** assumption is suitable for very long, prismatic bodies (like dams, tunnels, or retaining walls) where the geometry and loading are uniform along the length of the body. Far from the ends, the deformation is confined to the cross-sectional plane. The defining assumption is kinematic: all out-of-plane strain components are zero:

$$
\varepsilon_{zz} = \varepsilon_{xz} = \varepsilon_{yz} = 0
$$

To enforce the zero [axial strain](@entry_id:160811) condition ($\varepsilon_{zz}=0$), an out-of-plane normal stress $\sigma_{zz}$ must develop. From Hooke's Law, this stress is found to be $\sigma_{zz} = \nu(\sigma_{xx} + \sigma_{yy})$ [@problem_id:2889774]. This stress prevents the material from deforming in the $z$-direction as it would under the in-plane stresses.

Substituting this constraint into the 3D [constitutive law](@entry_id:167255) yields the 2D plane strain constitutive relationship. Interestingly, the algebraic form of the [plane strain](@entry_id:167046) equations can be made identical to the [plane stress](@entry_id:172193) equations by defining a set of **effective 2D moduli**, denoted $E'$ and $\nu'$ [@problem_id:2889758]:

$$
E' = \frac{E}{1-\nu^2}, \quad \nu' = \frac{\nu}{1-\nu}
$$

Using these effective moduli, the plane strain stress-strain law is:

$$
\begin{pmatrix} \sigma_{xx} \\ \sigma_{yy} \\ \sigma_{xy} \end{pmatrix} = \frac{E'}{1-(\nu')^2} \begin{pmatrix} 1 & \nu' & 0 \\ \nu' & 1 & 0 \\ 0 & 0 & \frac{1-\nu'}{2} \end{pmatrix} \begin{pmatrix} \varepsilon_{xx} \\ \varepsilon_{yy} \\ \gamma_{xy} \end{pmatrix}
$$

It is important to note that while the normal stress-strain coupling terms differ between [plane stress and plane strain](@entry_id:172357), the in-plane shear response is identical in both cases for an isotropic material. The compliance term relating $\gamma_{xy}$ to $\sigma_{xy}$ is $\frac{1}{G} = \frac{2(1+\nu)}{E}$ in both formulations [@problem_id:2889774].

### Governing Equations and Solution Strategies

Having established the fundamental relations, we can assemble the full set of governing equations. For a 2D problem, we have three independent stress components ($\sigma_{xx}, \sigma_{yy}, \sigma_{xy}$), three independent strain components ($\varepsilon_{xx}, \varepsilon_{yy}, \varepsilon_{xy}$), and two displacement components ($u, v$). These eight unknown functions are governed by:
- Two [equilibrium equations](@entry_id:172166).
- Three [strain-displacement relations](@entry_id:173321).
- Three [constitutive relations](@entry_id:186508).
This gives a complete system of eight equations for eight unknowns, which can be solved subject to appropriate boundary conditions. Various strategies exist to simplify and solve this system.

#### The Compatibility Condition

The three strain components are derived from only two displacement components. This implies that the strain components are not independent of one another. By differentiating the [strain-displacement relations](@entry_id:173321) and combining them to eliminate the displacement functions, we arrive at a constraint equation that any valid strain field must satisfy. This is the **Saint-Venant [compatibility condition](@entry_id:171102)**. In 2D, it takes the form [@problem_id:2889746]:

$$
\frac{\partial^2 \varepsilon_{xx}}{\partial y^2} + \frac{\partial^2 \varepsilon_{yy}}{\partial x^2} = 2\frac{\partial^2 \varepsilon_{xy}}{\partial x \partial y}
$$

This equation is purely kinematic; its derivation relies only on the definition of strain and the assumption of a continuous, single-valued displacement field. It contains no material parameters. It ensures that a given strain field can be integrated to find a valid [displacement field](@entry_id:141476).

#### Stress-Based Formulations and the Airy Stress Function

One powerful solution strategy is to reformulate the problem entirely in terms of stress. The [equilibrium equations](@entry_id:172166) are two equations for three unknown stresses, and the system is statically indeterminate. The compatibility condition provides the necessary additional constraint. By substituting the [constitutive law](@entry_id:167255) into the [strain compatibility](@entry_id:199659) equation, we obtain a set of equations governing the stress field, known as the **Beltrami-Michell compatibility equations**. These equations, unlike their strain counterparts, do involve material constants.

For the common case of 2D problems with no [body forces](@entry_id:174230) ($\mathbf{b}=\mathbf{0}$), the [equilibrium equations](@entry_id:172166) can be identically satisfied by introducing a [scalar potential](@entry_id:276177) known as the **Airy stress function**, $\Phi(x,y)$. The stress components are defined as second derivatives of this function:

$$
\sigma_{xx} = \frac{\partial^2 \Phi}{\partial y^2}, \quad \sigma_{yy} = \frac{\partial^2 \Phi}{\partial x^2}, \quad \sigma_{xy} = -\frac{\partial^2 \Phi}{\partial x \partial y}
$$

With these definitions, the two [equilibrium equations](@entry_id:172166) are automatically satisfied for any sufficiently [smooth function](@entry_id:158037) $\Phi$. The problem is thus reduced to finding a single function $\Phi$ that satisfies the [compatibility condition](@entry_id:171102). For a homogeneous, [isotropic material](@entry_id:204616), substituting these stress definitions into the Beltrami-Michell equations remarkably yields a single governing PDE for $\Phi$ in which the material constants cancel out [@problem_id:2889746]:

$$
\nabla^4 \Phi = \nabla^2(\nabla^2 \Phi) = \frac{\partial^4 \Phi}{\partial x^4} + 2\frac{\partial^4 \Phi}{\partial x^2 \partial y^2} + \frac{\partial^4 \Phi}{\partial y^4} = 0
$$

This is the **[biharmonic equation](@entry_id:165706)**. Solving elasticity problems in this framework involves finding a biharmonic function $\Phi$ that also satisfies the boundary conditions, which must be expressed in terms of stresses.

This method is particularly potent in [coordinate systems](@entry_id:149266) suited to the problem geometry. For instance, in [polar coordinates](@entry_id:159425) $(r, \theta)$, which are natural for problems involving holes or disks, the stress components can be expressed in terms of derivatives of $\Phi(r, \theta)$, and the [biharmonic equation](@entry_id:165706) takes the form $(\nabla^2)^2\Phi = 0$ where $\nabla^2$ is the Laplacian in polar coordinates [@problem_id:2889741]. For example, a stress function of the form $\Phi(r, \theta) = C r^3 \cos\theta$ is biharmonic and generates a valid stress field, with $\sigma_{rr} = 2Cr\cos\theta$.

### Advanced Solution Methodologies

For more complex problems, even more powerful mathematical machinery has been developed. We briefly introduce two cornerstone advanced methods for 2D [elastostatics](@entry_id:198298).

#### Complex Variable Methods

The [biharmonic equation](@entry_id:165706) is intimately connected to the theory of analytic [functions of a complex variable](@entry_id:175282). N.I. Muskhelishvili and G.V. Kolosov pioneered a method that represents the Airy stress function and the [displacement field](@entry_id:141476) in terms of two analytic complex potentials, $\phi(z)$ and $\psi(z)$, where $z = x+iy$. The Goursat [representation theorem](@entry_id:275118) states that any biharmonic function $F(x,y)$ can be written as:

$$
F(x,y) = \Re\left[ \bar{z}\phi(z) + \chi(z) \right]
$$

where $\chi'(z) = \psi(z)$. This elegant formulation allows the powerful tools of complex analysis, such as [conformal mapping](@entry_id:144027) and [contour integration](@entry_id:169446), to be applied to elasticity problems.

From this representation, key combinations of stresses and displacements can be derived directly in terms of the potentials. The two fundamental stress formulas are [@problem_id:2889750]:

$$
\sigma_{xx} + \sigma_{yy} = 4\Re[\phi'(z)]
$$

$$
\sigma_{yy} - \sigma_{xx} + 2i\sigma_{xy} = 2[\bar{z}\phi''(z) + \psi'(z)]
$$

These equations form the basis for solving a vast class of 2D elasticity problems, especially those involving complex geometries like cracks and inclusions, where stress concentrations are of primary interest.

#### Variational Formulations and the Weak Form

An alternative approach, which forms the theoretical foundation for the finite element method (FEM), is to reformulate the governing PDEs into an integral statement known as the **weak or variational form**. This is achieved by multiplying the [equilibrium equation](@entry_id:749057) by an arbitrary "test" or "virtual" displacement field $\mathbf{w}$ and integrating over the domain. Applying integration by parts (Green's theorem) transfers a derivative from the stress tensor to the [test function](@entry_id:178872), yielding the [principle of virtual work](@entry_id:138749) [@problem_id:2889748]:

$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{w}) \, d\Omega = \int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, d\Omega + \int_{\partial\Omega} \mathbf{t} \cdot \mathbf{w} \, d\Gamma
$$

This equation states that for a body in equilibrium, the [internal virtual work](@entry_id:172278) (left side) equals the external virtual work (right side) for any kinematically admissible [virtual displacement](@entry_id:168781). This formulation has several advantages. It requires less smoothness on the solution $\mathbf{u}$ than the original PDE (hence "weak" form) and it naturally incorporates certain types of boundary conditions.

In a [well-posed problem](@entry_id:268832), the boundary $\partial\Omega$ is partitioned into a part $\Gamma_D$ where displacements are prescribed ($\mathbf{u} = \bar{\mathbf{u}}$), and a part $\Gamma_N$ where tractions are prescribed ($\boldsymbol{\sigma}\mathbf{n} = \bar{\mathbf{t}}$). These are handled differently in the weak form:

1.  **Essential Boundary Conditions** (e.g., prescribed displacements on $\Gamma_D$) must be satisfied by the solution space itself. The actual displacement field $\mathbf{u}$ is sought in a **[trial space](@entry_id:756166)** of functions that satisfy $\mathbf{u}=\bar{\mathbf{u}}$ on $\Gamma_D$. The test functions $\mathbf{w}$ are chosen from a corresponding vector space where the homogeneous condition $\mathbf{w}=\mathbf{0}$ on $\Gamma_D$ holds.

2.  **Natural Boundary Conditions** (e.g., prescribed tractions on $\Gamma_N$) are satisfied automatically by the [variational equation](@entry_id:635018). The prescribed traction $\bar{\mathbf{t}}$ is substituted directly into the boundary integral on the right-hand side.

The final weak statement is: Find $\mathbf{u}$ (satisfying essential BCs) such that for all [test functions](@entry_id:166589) $\mathbf{w}$ (satisfying homogeneous essential BCs):

$$
\int_{\Omega} \boldsymbol{\sigma}(\mathbf{u}) : \boldsymbol{\varepsilon}(\mathbf{w}) \, d\Omega = \int_{\Omega} \mathbf{b} \cdot \mathbf{w} \, d\Omega + \int_{\Gamma_{N}} \bar{\mathbf{t}} \cdot \mathbf{w} \, d\Gamma
$$

This variational framework is not only a powerful analytical tool but also the starting point for developing robust [numerical approximation](@entry_id:161970) schemes that have revolutionized engineering analysis.