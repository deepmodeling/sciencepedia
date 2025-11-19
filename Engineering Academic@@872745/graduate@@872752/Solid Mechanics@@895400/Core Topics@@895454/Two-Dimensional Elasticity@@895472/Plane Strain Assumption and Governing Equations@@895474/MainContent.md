## Introduction
In solid mechanics, the analysis of three-dimensional bodies often leads to complex systems of partial differential equations that are difficult to solve. A cornerstone of engineering analysis is the simplification of these problems through [dimensional reduction](@entry_id:197644). The [plane strain assumption](@entry_id:186003) represents one of the most powerful idealizations, allowing a vast range of 3D physical systems—from deep underground tunnels to microelectronic components—to be modeled accurately within a more tractable 2D framework. This article addresses the fundamental theory and application of plane strain, bridging the gap between abstract principles and practical engineering consequences.

This article is structured to build a comprehensive understanding of the topic. The first chapter, **"Principles and Mechanisms,"** establishes the formal definition of [plane strain](@entry_id:167046), derives the out-of-plane constraint stress, and formulates the governing equations, including the [biharmonic equation](@entry_id:165706) for the Airy stress function. The second chapter, **"Applications and Interdisciplinary Connections,"** explores the crucial role of the [plane strain assumption](@entry_id:186003) in diverse fields such as geomechanics, fracture mechanics, and [thermoelasticity](@entry_id:158447), demonstrating its practical impact. Finally, **"Hands-On Practices"** provides a set of targeted problems to solidify theoretical concepts and connect them to computational implementation. We begin by establishing the fundamental principles and mechanisms that define the [plane strain](@entry_id:167046) state.

## Principles and Mechanisms

In the analysis of three-dimensional solids, the governing equations of elasticity often present formidable mathematical challenges. A powerful strategy in engineering and physics is to reduce the dimensionality of a problem by leveraging geometric symmetries and loading conditions. Two such idealizations, **[plane strain](@entry_id:167046)** and **plane stress**, are cornerstones of [solid mechanics](@entry_id:164042), allowing a wide range of three-dimensional problems to be modeled and solved in a two-dimensional framework. This chapter elucidates the principles and mechanisms underpinning the [plane strain assumption](@entry_id:186003), from its fundamental definition to its consequences in advanced applications.

### Defining Two-Dimensional States: Plane Strain and Plane Stress

At the heart of any [dimensional reduction](@entry_id:197644) is a set of simplifying assumptions about the state of deformation (strain) or the state of stress. The choice between [plane strain](@entry_id:167046) and [plane stress](@entry_id:172193) hinges on the geometry of the body and the nature of the constraints imposed upon it.

**Plane strain** is a state of deformation. It is defined by the kinematic constraint that all out-of-plane strain components vanish. For a coordinate system where the problem of interest lies in the $x-y$ plane, this means:
$$ \epsilon_{zz} = 0, \quad \epsilon_{xz} = 0, \quad \epsilon_{yz} = 0 $$
The conditions on the shear strains, $\epsilon_{xz}$ and $\epsilon_{yz}$, imply that cross-sections originally perpendicular to the $z$-axis remain plane and do not distort relative to each other in shear. The condition $\epsilon_{zz}=0$ means there is no extension or contraction in the out-of-plane direction. Physically, the [plane strain assumption](@entry_id:186003) is appropriate for bodies that are very long in one direction (say, the $z$-direction) compared to their in-plane dimensions, and whose geometry and loading are uniform along this long axis. Examples include long dams, retaining walls under uniform pressure, and pipelines. The immense length and end constraints effectively prevent the material from deforming axially, especially in regions far from the ends, a concept rigorously justified by Saint-Venant's principle. [@problem_id:2669582] [@problem_id:2669573]

In contrast, **[plane stress](@entry_id:172193)** is a state of stress. It is defined by the assumption that all out-of-plane stress components are zero:
$$ \sigma_{zz} = 0, \quad \sigma_{xz} = 0, \quad \sigma_{yz} = 0 $$
This assumption is physically justified for bodies that are very thin in one direction. Consider a thin plate loaded only in its plane, with its major faces (e.g., at $z = \pm t/2$) free of traction. The out-of-[plane stress](@entry_id:172193) components are zero on these free surfaces. If the thickness $t$ is small compared to the in-plane dimensions, it is reasonable to assume these stresses remain negligible throughout the entire thickness. Under these conditions, the out-of-plane strain is generally non-zero, governed by the Poisson effect: $\epsilon_{zz} = -\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})$. [@problem_id:2669582]

It is a common error to confuse the conditions defining these two states. The next section will explore a crucial consequence of this distinction: the development of a non-zero out-of-plane stress required to enforce the [plane strain](@entry_id:167046) condition.

### The Constraint Stress: A Consequence of Plane Strain Kinematics

A key feature of plane strain in an isotropic elastic material is the presence of an out-of-plane normal stress, $\sigma_{zz}$, even in the absence of any out-of-plane loading. This stress arises as a mechanical necessity to enforce the kinematic constraint $\epsilon_{zz}=0$.

To understand this mechanism, we turn to the three-dimensional [constitutive law](@entry_id:167255) for a homogeneous, isotropic, linear elastic material (Hooke's Law). The strain-stress relation for the out-of-plane [normal strain](@entry_id:204633) is:
$$ \epsilon_{zz} = \frac{1}{E} [ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) ] $$
where $E$ is the Young’s modulus and $\nu$ is the Poisson’s ratio. The term $-\frac{\nu}{E}(\sigma_{xx} + \sigma_{yy})$ represents the strain that would occur in the $z$-direction due to the **Poisson effect** if the body were free to deform. In a [plane strain](@entry_id:167046) scenario, this deformation is prevented, meaning $\epsilon_{zz}$ must be zero. Enforcing this constraint in the [constitutive equation](@entry_id:267976) gives:
$$ 0 = \frac{1}{E} [ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) ] $$
Solving for $\sigma_{zz}$ reveals the out-of-[plane stress](@entry_id:172193) required to maintain the plane strain state:
$$ \sigma_{zz} = \nu (\sigma_{xx} + \sigma_{yy}) $$
This equation is central to the theory of plane strain. It shows that $\sigma_{zz}$ is a "reaction" or **constraint stress** that develops to counteract the Poisson effect. Unless the material has a zero Poisson's ratio ($\nu=0$) or the in-plane stresses happen to satisfy $\sigma_{xx} + \sigma_{yy} = 0$, a non-zero $\sigma_{zz}$ will always be present. Since $\sigma_{xx}$ and $\sigma_{yy}$ are generally functions of position $(x,y)$, $\sigma_{zz}$ will also vary across the cross-section. [@problem_id:2669597] [@problem_id:2669582]

This out-of-plane stress contributes to the overall state of stress and, consequently, to the **[hydrostatic pressure](@entry_id:141627)**, defined as $p = - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \sigma_{zz})$. Substituting the expression for $\sigma_{zz}$ gives:
$$ p = - \frac{1}{3}(\sigma_{xx} + \sigma_{yy} + \nu(\sigma_{xx} + \sigma_{yy})) = -\frac{1+\nu}{3}(\sigma_{xx} + \sigma_{yy}) $$
This demonstrates that the hydrostatic stress state in a [plane strain](@entry_id:167046) problem is directly dependent on Poisson's ratio, a key consideration in fields like plasticity and geomechanics where material failure is often governed by hydrostatic pressure. For instance, consider a prescribed in-plane stress field $\sigma_{xx} = 2ax^2$, $\sigma_{yy} = 2ay^2$, and $\sigma_{xy} = -4axy$. The resulting [hydrostatic pressure](@entry_id:141627) is $p(x,y) = -\frac{2a(1+\nu)}{3}(x^2+y^2)$, clearly showing its dependence on $\nu$ but not on $E$. [@problem_id:2669550]

An alternative approach using the stiffness form of the [constitutive law](@entry_id:167255), $\sigma_{ij} = \lambda \epsilon_{kk} \delta_{ij} + 2\mu \epsilon_{ij}$, provides the same result. Here, $\lambda$ and $\mu$ are the Lamé parameters. Under plane strain, $\epsilon_{zz}=0$, so the [volumetric strain](@entry_id:267252) is $\epsilon_{kk} = \epsilon_{xx} + \epsilon_{yy}$. The out-of-plane stress is then:
$$ \sigma_{zz} = \lambda(\epsilon_{xx} + \epsilon_{yy}) + 2\mu \epsilon_{zz} = \lambda(\epsilon_{xx} + \epsilon_{yy}) $$
Substituting the relation $\lambda = \frac{E\nu}{(1+\nu)(1-2\nu)}$ yields the expression for $\sigma_{zz}$ in terms of the measured in-plane strains:
$$ \sigma_{zz}(x,y) = \frac{E\nu}{(1+\nu)(1-2\nu)} (\epsilon_{xx}(x,y) + \epsilon_{yy}(x,y)) $$
This expression is particularly useful in experimental mechanics, where in-plane strains can be measured using techniques like [digital image correlation](@entry_id:199778), allowing for the indirect determination of the out-of-[plane stress](@entry_id:172193). [@problem_id:2669553]

### Governing Equations and Solution Methods

With the plane strain kinematics established, we can formulate the governing equations for a two-dimensional boundary value problem.

#### Equilibrium and Boundary Conditions

The three-dimensional equations of static equilibrium are $\sigma_{ij,j} + b_i = 0$. For a [plane strain](@entry_id:167046) problem, we assume all field variables are independent of the $z$-coordinate, so $\partial(\cdot)/\partial z = 0$. Furthermore, the out-of-plane shear strains $\epsilon_{xz}$ and $\epsilon_{yz}$ are zero, which for an isotropic material implies the shear stresses $\sigma_{xz}$ and $\sigma_{yz}$ are also zero. Applying these conditions to the 3D [equilibrium equations](@entry_id:172166) yields:
1.  **x-direction:** $\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + \frac{\partial \sigma_{xz}}{\partial z} + b_x = 0 \quad \implies \quad \frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \sigma_{xy}}{\partial y} + b_x = 0$
2.  **y-direction:** $\frac{\partial \sigma_{yx}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \sigma_{yz}}{\partial z} + b_y = 0 \quad \implies \quad \frac{\partial \sigma_{xy}}{\partial x} + \frac{\partial \sigma_{yy}}{\partial y} + b_y = 0$
3.  **z-direction:** $\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} + b_z = 0 \quad \implies \quad 0 + 0 + 0 + b_z = 0$

The first two equations are the familiar 2D [equilibrium equations](@entry_id:172166) that govern the in-plane stresses. The third equation reduces to $b_z = 0$, indicating that the plane strain formulation is only consistent if there is no out-of-plane [body force](@entry_id:184443). [@problem_id:2669582]

To solve these equations for a specific body occupying a domain $\Omega$, we must specify boundary conditions on its boundary $\partial\Omega$. A [well-posed problem](@entry_id:268832) requires partitioning the boundary into a part $\Gamma_u$ where displacements $\boldsymbol{u}=\bar{\boldsymbol{u}}$ are prescribed (a **Dirichlet condition**) and a part $\Gamma_t$ where tractions $\boldsymbol{t}=\bar{\boldsymbol{t}}$ are prescribed (a **Neumann condition**). The traction vector is related to the stress tensor by **Cauchy's formula**, $t_i = \sigma_{ij}n_j$, where $n_j$ are the components of the outward unit normal to the boundary. [@problem_id:2669574]

#### The Airy Stress Function

For problems without [body forces](@entry_id:174230) ($b_x=b_y=0$), the 2D [equilibrium equations](@entry_id:172166) can be automatically satisfied by introducing a [scalar potential](@entry_id:276177) known as the **Airy stress function**, $\phi(x,y)$. The stress components are defined as second derivatives of this function:
$$ \sigma_{xx} = \frac{\partial^2 \phi}{\partial y^2}, \qquad \sigma_{yy} = \frac{\partial^2 \phi}{\partial x^2}, \qquad \sigma_{xy} = -\frac{\partial^2 \phi}{\partial x \partial y} $$
Substituting these definitions into the [equilibrium equations](@entry_id:172166) results in identities, confirming that any stress field derived from a sufficiently smooth function $\phi$ is in equilibrium.

However, a valid elastic solution must also satisfy kinematic compatibility. For small strains, this is expressed by the [strain compatibility](@entry_id:199659) equation:
$$ \frac{\partial^2 \epsilon_{xx}}{\partial y^2} + \frac{\partial^2 \epsilon_{yy}}{\partial x^2} = 2 \frac{\partial^2 \epsilon_{xy}}{\partial x \partial y} $$
By substituting the plane strain [constitutive relations](@entry_id:186508) into this equation, and then expressing the stresses in terms of the Airy function $\phi$, we arrive at a single governing partial differential equation for $\phi$:
$$ \frac{\partial^4 \phi}{\partial x^4} + 2\frac{\partial^4 \phi}{\partial x^2 \partial y^2} + \frac{\partial^4 \phi}{\partial y^4} = 0 $$
This is the **[biharmonic equation](@entry_id:165706)**, often written compactly as $\nabla^4 \phi = 0$ or $\nabla^2(\nabla^2\phi)=0$. Any biharmonic function $\phi$ represents a valid stress state for a plane strain problem. Notably, the same equation governs plane stress problems, meaning solutions for $\phi$ can often be applied to both cases, though the resulting strain and displacement fields will differ.

For example, consider the cubic polynomial $\phi(x,y) = a x^{3} + b y^{3} + c x y^{2} + d x^{2} y$. The Laplacian is $\nabla^2\phi = (6ax+2dy) + (6by+2cx)$, which is a linear function. The Laplacian of a linear function is zero, so $\nabla^2(\nabla^2\phi) = 0$. This function is biharmonic and thus represents a valid stress field, which can be computed as $\sigma_{xx} = 6by+2cx$, $\sigma_{yy} = 6ax+2dy$, and $\sigma_{xy} = -2cy-2dx$. [@problem_id:2669581]

### Advanced Topics and Extensions

The classical [plane strain](@entry_id:167046) model can be extended and more rigorously justified, and its application has profound consequences in fields such as fracture and computational mechanics.

#### Generalized Plane Strain

The strict assumption $\epsilon_{zz}=0$ is sometimes overly restrictive. A useful extension is **[generalized plane strain](@entry_id:182960)**, which allows for a uniform, non-zero [axial strain](@entry_id:160811):
$$ \epsilon_{zz} = \bar{\epsilon} = \text{constant} $$
The other plane strain kinematic assumptions ($\epsilon_{xz}=0$, $\epsilon_{yz}=0$, and independence of fields from $z$) are retained. This model is appropriate for long prismatic bodies that are free to expand or contract uniformly along their axis. Common applications include a long bar subjected to a net axial force or a uniform change in temperature with unconstrained ends. [@problem_id:2669572]

In this formulation, $\bar{\epsilon}$ is an additional unknown. The problem is closed by imposing a global condition on the axial direction. Most commonly, the net axial force $N_z$ is prescribed. By integrating the axial stress $\sigma_{zz}$ over the cross-sectional area $A$, we obtain a scalar equation that relates $\bar{\epsilon}$ to the average in-plane strains and the prescribed force $N_z$:
$$ N_z = \int_A \sigma_{zz} \, dA $$
For example, for a body with free ends ($N_z=0$) under a uniform temperature change $\Delta T$, $\bar{\epsilon}$ will adjust to the value $\alpha \Delta T$ (where $\alpha$ is the [coefficient of thermal expansion](@entry_id:143640)), allowing the body to expand freely while maintaining zero net axial force. [@problem_id:2669572]

It is crucial to recognize that even this generalized assumption is not universally applicable for all problems with $z$-invariant geometry and loading. A prominent counterexample is the torsion of a [prismatic bar](@entry_id:190143), where the [cross-sections](@entry_id:168295) rotate relative to one another, inducing in-plane displacements that vary linearly with $z$ (e.g., $u = -\alpha z y$, $v = \alpha z x$). This violates the core assumption that $u$ and $v$ are functions of $x$ and $y$ only. [@problem_id:2669573] A more rigorous justification for when [plane strain](@entry_id:167046) is applicable comes from [asymptotic analysis](@entry_id:160416), which shows that for a long, slender body with a small [aspect ratio](@entry_id:177707) $\varepsilon = L_{xy}/L_z \ll 1$, the plane strain solution emerges as the leading-order approximation in regions far from the ends. [@problem_id:2669551]

#### Consequences in Fracture Mechanics

The [plane strain](@entry_id:167046) constraint has critical practical implications in the field of [fracture mechanics](@entry_id:141480). The constraint against out-of-plane deformation leads to a higher triaxial stress state near the tip of a crack compared to a plane stress state. This makes the material behave in a more brittle manner.

This physical effect is captured quantitatively in the relationship between the **energy release rate** $J$ (a measure of the energy available to drive crack growth) and the **[stress intensity factor](@entry_id:157604)** $K_I$ (a measure of the stress field severity at the [crack tip](@entry_id:182807)). For a linear elastic material, this relationship is:
$$ J = \frac{K_I^2}{E'} $$
where $E'$ is an effective modulus. The value of $E'$ depends on the assumed kinematic state:
-   For **[plane stress](@entry_id:172193)**: $E' = E$
-   For **[plane strain](@entry_id:167046)**: $E' = \frac{E}{1-\nu^2}$

The term $(1-\nu^2)^{-1}$ shows that the effective stiffness is higher in plane strain. For a given stress intensity factor $K_I$, the [energy release rate](@entry_id:158357) $J$ is lower in [plane strain](@entry_id:167046) than in plane stress (since $1-\nu^2  1$). Conversely, for a given energy input $J$, a higher stress intensity can be sustained. The increased stiffness arises directly from the energy stored by the out-of-plane constraint stress $\sigma_{zz}$. This difference is fundamental to understanding why the measured fracture toughness of a material often depends on the thickness of the specimen being tested. [@problem_id:2669561]

#### Consequences in Computational Mechanics: Volumetric Locking

In the limit of incompressibility ($\nu \to 0.5$), the material's [bulk modulus](@entry_id:160069) $\kappa$ approaches infinity. The condition of [incompressibility](@entry_id:274914) is zero volumetric strain, $\epsilon_v = \epsilon_{xx} + \epsilon_{yy} + \epsilon_{zz} = 0$. Under plane strain, this reduces to the in-plane constraint:
$$ \nabla \cdot \boldsymbol{u} = \epsilon_{xx} + \epsilon_{yy} = 0 $$
When solving nearly incompressible plane strain problems using the standard displacement-based Finite Element Method (FEM), this constraint can lead to a numerical [pathology](@entry_id:193640) known as **volumetric locking**. Low-order elements (like bilinear quadrilaterals) have a limited number of kinematic degrees of freedom. Enforcing the [incompressibility constraint](@entry_id:750592) at every integration point imposes too many constraints, artificially "locking" the element and preventing it from deforming. The result is a solution that is spuriously stiff and physically meaningless. [@problem_id:2669596]

The standard remedy for [volumetric locking](@entry_id:172606) is to use a **mixed [finite element formulation](@entry_id:164720)**. In this approach, the hydrostatic pressure $p$ is introduced as an independent field variable that acts as a Lagrange multiplier to enforce the [incompressibility constraint](@entry_id:750592) in a weak, integral sense. The resulting system of equations solves for both displacement $\boldsymbol{u}$ and pressure $p$. For this [mixed formulation](@entry_id:171379) to be stable and produce accurate results, the discrete approximation spaces for $\boldsymbol{u}$ and $p$ must satisfy the **Ladyzhenskaya–Babuška–Brezzi (LBB) stability condition**. This ensures that the pressure field is well-behaved and that the kinematic constraint is not over-enforced, thereby eliminating locking. [@problem_id:2669596]