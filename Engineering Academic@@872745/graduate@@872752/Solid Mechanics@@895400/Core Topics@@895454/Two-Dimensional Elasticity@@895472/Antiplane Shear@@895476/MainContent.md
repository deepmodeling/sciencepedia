## Introduction
Antiplane shear represents one of the most powerful idealizations in [solid mechanics](@entry_id:164042), offering a way to simplify complex three-dimensional problems into a more tractable two-dimensional framework. It addresses the challenge of analyzing deformations where a body is sheared longitudinally, such as in the tearing of a plate or the twisting of a shaft, by reducing the governing physics to a single scalar equation. This simplification makes it an invaluable tool for both pedagogical purposes and for solving practical problems in engineering and materials science.

This article provides a comprehensive exploration of antiplane shear. The first chapter, **Principles and Mechanisms**, establishes the foundational theory, deriving the kinematic constraints, stress-strain relations, and governing equations from first principles. The second chapter, **Applications and Interdisciplinary Connections**, showcases the theory's broad impact, from the torsion of bars and the mechanics of [screw dislocations](@entry_id:182908) to its pivotal role in [linear elastic fracture mechanics](@entry_id:172400). Finally, **Hands-On Practices** will guide you through solving classic problems to solidify your understanding of these powerful concepts.

## Principles and Mechanisms

The state of antiplane shear represents one of the most elegant and instructive idealizations in the [theory of elasticity](@entry_id:184142). It reduces a three-dimensional problem to a two-dimensional one governed by a single scalar potential function, yet it retains rich physical content, finding applications in the analysis of longitudinally sheared members, [screw dislocations](@entry_id:182908), and Mode III [fracture mechanics](@entry_id:141480). This chapter elucidates the fundamental principles and mechanisms of antiplane shear, proceeding from its kinematic definition to its governing equations, boundary conditions, and its place within the broader framework of solid mechanics.

### Kinematic Definition and Consequences

Antiplane [shear deformation](@entry_id:170920) is defined by a specific kinematic assumption about the displacement field. Consider a body described by a Cartesian coordinate system $(x, y, z)$. The displacement vector at any point is denoted by $\boldsymbol{u} = (u_x, u_y, u_z)$. The **antiplane shear** state is defined by the following kinematic constraints: the in-plane displacement components are identically zero, and the single out-of-plane displacement component, $u_z$, is a function of the in-plane coordinates only. Mathematically, this is expressed as:

$u_x = 0$
$u_y = 0$
$u_z = w(x, y)$

This displacement field describes a motion where each plane originally parallel to the $xy$-plane translates rigidly in the $z$-direction, with the amount of translation, $w$, varying from point to point within the plane. This can be visualized as the shearing of a deck of cards, where the cards slide relative to one another.

The state of strain is derived directly from this kinematic assumption. Within the theory of infinitesimal deformations, the strain tensor components $\varepsilon_{ij}$ are given by $\varepsilon_{ij} = \frac{1}{2}(u_{i,j} + u_{j,i})$, where the comma denotes [partial differentiation](@entry_id:194612). Applying this to the antiplane [displacement field](@entry_id:141476) reveals a remarkably simple strain state [@problem_id:2615407].

The [normal strain](@entry_id:204633) components are:
$\varepsilon_{xx} = \frac{\partial u_x}{\partial x} = 0$
$\varepsilon_{yy} = \frac{\partial u_y}{\partial y} = 0$
$\varepsilon_{zz} = \frac{\partial u_z}{\partial z} = \frac{\partial w(x,y)}{\partial z} = 0$

The in-plane [shear strain](@entry_id:175241) component is also zero:
$\varepsilon_{xy} = \frac{1}{2}\left(\frac{\partial u_x}{\partial y} + \frac{\partial u_y}{\partial x}\right) = 0$

The only non-vanishing strain components are the out-of-plane shear strains:
$\varepsilon_{xz} = \varepsilon_{zx} = \frac{1}{2}\left(\frac{\partial u_x}{\partial z} + \frac{\partial u_z}{\partial x}\right) = \frac{1}{2}\left(0 + \frac{\partial w}{\partial x}\right) = \frac{1}{2}\frac{\partial w}{\partial x}$
$\varepsilon_{yz} = \varepsilon_{zy} = \frac{1}{2}\left(\frac{\partial u_y}{\partial z} + \frac{\partial u_z}{\partial y}\right) = \frac{1}{2}\left(0 + \frac{\partial w}{\partial y}\right) = \frac{1}{2}\frac{\partial w}{\partial y}$

Thus, the antiplane shear state is one of pure shear on planes parallel to the $z$-axis. It is often convenient to work with **engineering shear strains**, denoted by $\gamma_{ij}$, which are defined as $\gamma_{ij} = 2\varepsilon_{ij}$ for $i \neq j$. In antiplane shear, the only non-zero engineering strains are:
$\gamma_{xz} = \frac{\partial w}{\partial x}$
$\gamma_{yz} = \frac{\partial w}{\partial y}$
The vector of these engineering shear strains is simply the two-dimensional gradient of the out-of-plane displacement, $\boldsymbol{\gamma} = (\gamma_{xz}, \gamma_{yz}) = \nabla w$.

A crucial concept in elasticity is **kinematic compatibility**, which ensures that a strain field can be integrated to produce a single-valued, continuous displacement field. When we begin, as we have here, with a well-defined and single-valued displacement potential $w(x,y)$, the resulting strain field is compatible by construction. All Saint-Venant [compatibility conditions](@entry_id:201103) are identically satisfied, provided $w(x,y)$ is sufficiently smooth [@problem_id:2615438].

If, however, one starts by prescribing a strain field with only $\gamma_{xz}(x,y)$ and $\gamma_{yz}(x,y)$ being non-zero, compatibility is not automatic. In a [simply connected domain](@entry_id:197423), the necessary and [sufficient condition](@entry_id:276242) for the existence of a displacement potential $w$ is that the strain field must be irrotational. This reduces to the single scalar equation:
$\frac{\partial \gamma_{xz}}{\partial y} - \frac{\partial \gamma_{yz}}{\partial x} = 0$
Substituting $\gamma_{xz} = \partial w / \partial x$ and $\gamma_{yz} = \partial w / \partial y$, this condition becomes $\frac{\partial^2 w}{\partial y \partial x} = \frac{\partial^2 w}{\partial x \partial y}$, which is an identity for any twice continuously [differentiable function](@entry_id:144590) $w$. The existence of the potential $w$ is the embodiment of compatibility for this state of strain [@problem_id:2615438].

### Stress State and Governing Equations

The stress state in antiplane shear is found by applying the material's [constitutive law](@entry_id:167255) to the derived strain field. For a linear, **isotropic** elastic material, the stress-strain relationship (Hooke's law) is given by:
$\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}$
where $\lambda$ and $\mu$ are the Lamé parameters, $\delta_{ij}$ is the Kronecker delta, and $\varepsilon_{kk}$ is the trace of the strain tensor (volumetric strain).

In antiplane shear, we established that all normal strains are zero, so the volumetric strain $\varepsilon_{kk} = \varepsilon_{xx} + \varepsilon_{yy} + \varepsilon_{zz} = 0$. The [constitutive law](@entry_id:167255) simplifies considerably. The normal stresses vanish:
$\sigma_{xx} = \sigma_{yy} = \sigma_{zz} = 0$
The in-plane shear stress also vanishes:
$\sigma_{xy} = 2\mu \varepsilon_{xy} = 0$

The only non-zero stress components are the out-of-plane shear stresses, which are directly proportional to the out-of-plane displacement gradients via the **shear modulus** $\mu$ (also denoted $G$):
$\sigma_{xz} \equiv \tau_{xz} = 2\mu \varepsilon_{xz} = \mu \frac{\partial w}{\partial x}$
$\sigma_{yz} \equiv \tau_{yz} = 2\mu \varepsilon_{yz} = \mu \frac{\partial w}{\partial y}$

These relations highlight the central physical role of the shear modulus $\mu$: it is the material property that quantifies resistance to [shear deformation](@entry_id:170920) in this mode [@problem_id:2615448]. In vector form, the shear stress vector is $\boldsymbol{\tau} = (\tau_{xz}, \tau_{yz}) = \mu \nabla w$.

With the [kinematics](@entry_id:173318) and [constitutive relations](@entry_id:186508) established, the final piece is the equation of equilibrium. In the absence of inertial effects, the [balance of linear momentum](@entry_id:193575) requires that $\nabla \cdot \boldsymbol{\sigma} + \boldsymbol{b} = \mathbf{0}$, where $\boldsymbol{b}$ is the [body force](@entry_id:184443) vector per unit volume. Given the antiplane shear stress state, the [equilibrium equations](@entry_id:172166) for the $x$ and $y$ directions are trivially satisfied (assuming $b_x=b_y=0$). The only potentially non-trivial equation is for the $z$-direction:
$\frac{\partial \sigma_{zx}}{\partial x} + \frac{\partial \sigma_{zy}}{\partial y} + \frac{\partial \sigma_{zz}}{\partial z} + b_z = 0$

Substituting the [constitutive relations](@entry_id:186508) and noting that $\sigma_{zz}=0$ and $\sigma_{zx}=\sigma_{xz}$, we arrive at the governing partial differential equation for the displacement field $w(x,y)$:
$\frac{\partial}{\partial x}\left(\mu \frac{\partial w}{\partial x}\right) + \frac{\partial}{\partial y}\left(\mu \frac{\partial w}{\partial y}\right) + b_z(x,y) = 0$
This can be written compactly as $\nabla \cdot (\mu \nabla w) + b_z = 0$.

It is a common misconception that antiplane shear is always governed by the Laplace equation. This is only true under two further simplifying assumptions:
1. The material is **homogeneous**, meaning the shear modulus $\mu$ is constant.
2. There are no out-of-plane [body forces](@entry_id:174230), i.e., $b_z = 0$.

Under these conditions, $\mu$ can be factored out of the derivatives, and the governing equation reduces to the celebrated **Laplace equation**:
$\nabla^2 w = \frac{\partial^2 w}{\partial x^2} + \frac{\partial^2 w}{\partial y^2} = 0$

It must be emphasized that this equation arises from equilibrium and the constitutive law, not from kinematic compatibility alone [@problem_id:2615438]. For a heterogeneous material where $\mu = \mu(x,y)$, the full equation $\nabla \cdot (\mu \nabla w) = 0$ must be solved [@problem_id:2615448].

### Context, Validity, and Comparison to Other Models

The antiplane shear idealization is powerful but applies only under specific circumstances [@problem_id:2615451]. The primary requirements are:
1.  **Geometry**: The body must be a **prismatic cylinder**, meaning it has a constant cross-section $\Omega$ along its length (the $z$-axis).
2.  **Loading**: All applied body forces and [surface tractions](@entry_id:169207) must act purely in the out-of-plane ($z$) direction and must not vary along the length of the cylinder.
3.  **Material Symmetry**: The material's constitutive law must not couple the out-of-plane shear strains ($\varepsilon_{xz}, \varepsilon_{yz}$) to in-plane stresses ($\sigma_{xx}, \sigma_{yy}, \sigma_{xy}$). This condition is met by **isotropic** materials and, more generally, by **transversely isotropic** materials whose plane of [isotropy](@entry_id:159159) is the $xy$-plane. For a general anisotropic material, the problem would not decouple, and an antiplane shear state would not be an exact solution.

For a finite-length bar, these conditions are rarely met exactly, especially at the ends where tractions are applied. However, by **Saint-Venant's principle**, if a sufficiently long bar is subjected to the specified lateral loads, the antiplane shear solution is an excellent approximation of the true 3D stress and displacement state in regions far from the ends [@problem_id:2615451].

To better understand antiplane shear, it is useful to contrast it with the other two common 2D idealizations: [plane strain](@entry_id:167046) and [plane stress](@entry_id:172193) [@problem_id:2615403].

*   **Antiplane Shear**: This is a purely **kinematic assumption**. Displacement is constrained: $u_x=0$, $u_y=0$, and $w=w(x,y)$. This implies that the only non-zero strains are the out-of-plane shears $\gamma_{xz}$ and $\gamma_{yz}$. The resulting non-zero stresses are the corresponding shear stresses $\tau_{xz}$ and $\tau_{yz}$.

*   **Plane Strain**: This is also a **kinematic assumption**, typically used for long prismatic bodies with uniform loading. Displacement is constrained: $w=0$, and $u=u(x,y)$, $v=v(x,y)$. This implies that all out-of-[plane strain](@entry_id:167046) components are zero: $\varepsilon_{zz}=0$, $\gamma_{xz}=0$, $\gamma_{yz}=0$. However, to enforce the $\varepsilon_{zz}=0$ constraint, a non-zero out-of-plane [normal stress](@entry_id:184326), $\sigma_{zz} = \lambda(\varepsilon_{xx}+\varepsilon_{yy})$, generally develops.

*   **Plane Stress**: This is a **stress assumption**, typically used for thin plates loaded in their plane. The stress components acting on the faces of the plate are assumed to be zero: $\sigma_{zz}=0$, $\sigma_{xz}=0$, $\sigma_{yz}=0$. The zero shear stress conditions imply that the corresponding shear strains are also zero: $\gamma_{xz}=0$, $\gamma_{yz}=0$. However, due to the Poisson effect, the out-of-plane [normal strain](@entry_id:204633) is generally non-zero: $\varepsilon_{zz} = -\frac{\lambda}{\lambda+2\mu}(\varepsilon_{xx}+\varepsilon_{yy}) \neq 0$.

In summary, antiplane shear, [plane strain](@entry_id:167046), and [plane stress](@entry_id:172193) represent three distinct, mutually exclusive ways of reducing a 3D elasticity problem to a 2D one, each resting on a different set of foundational assumptions.

### Boundary and Interface Conditions

To solve the governing [partial differential equation](@entry_id:141332) for $w(x,y)$, we must specify conditions on the boundary $\partial \Omega$ of the cross-section. There are two primary types of boundary conditions.

#### Neumann (Natural) Boundary Conditions
This condition involves prescribing the tractions on the boundary. On the lateral surface of the prismatic body, the outward [unit normal vector](@entry_id:178851) is purely in-plane, $\mathbf{n} = (n_x, n_y, 0)$. According to **Cauchy's traction formula**, the traction vector $\mathbf{T}$ on this surface is given by $\mathbf{T} = \boldsymbol{\sigma} \mathbf{n}$. For the antiplane shear stress state, this multiplication yields a [traction vector](@entry_id:189429) that points purely in the $z$-direction [@problem_id:2615423]:
$\mathbf{T} = (\sigma_{xz} n_x + \sigma_{yz} n_y) \mathbf{e}_z$
The magnitude of this out-of-plane traction, $t_z$, is therefore:
$t_z = \sigma_{xz} n_x + \sigma_{yz} n_y$
Substituting the [constitutive relations](@entry_id:186508), we obtain the boundary condition in terms of the displacement $w$:
$t_z = \mu \frac{\partial w}{\partial x} n_x + \mu \frac{\partial w}{\partial y} n_y = \mu (\nabla w \cdot \mathbf{n}) = \mu \frac{\partial w}{\partial n}$
Here, $\partial w / \partial n$ is the normal derivative of $w$. A Neumann boundary condition involves prescribing the value of this traction, $\bar{t}_z$, on a portion of the boundary $\Gamma_t$.

#### Dirichlet (Essential) Boundary Conditions
This condition involves prescribing the displacement itself on a portion of the boundary $\Gamma_w$: $w = \bar{w}$. Physically, this models a part of the boundary that is perfectly bonded to a rigid support or actuator that imposes a specific out-of-plane displacement profile $\bar{w}$ [@problem_id:2615447]. When the displacement is prescribed, the corresponding traction $t_z$ on that boundary segment cannot be independently specified. Instead, $t_z$ becomes an unknown **reaction traction** that must be computed from the solution.

#### Interface Conditions
When a body is composed of multiple materials with different shear moduli, we must specify how the fields behave across the internal interfaces. For a **perfectly bonded** interface $\Gamma$ separating two materials with moduli $\mu_1$ and $\mu_2$, two conditions must be met [@problem_id:2615425]:
1.  **Continuity of Displacement**: The bond prevents any separation or slip, so the displacement field must be continuous across the interface. For antiplane shear, this means:
    $[w] \equiv w_2 - w_1 = 0$
2.  **Continuity of Traction**: In the absence of any singular forces applied directly at the interface, the [traction vector](@entry_id:189429) must be continuous to satisfy equilibrium. This is a direct consequence of Newton's third law. For antiplane shear, this means the out-of-plane traction $t_z$ must be continuous:
    $[t_z] \equiv (t_z)_2 - (t_z)_1 = 0$
    Using the expression $t_z = \mu \partial w / \partial n$, this becomes:
    $\left[\mu \frac{\partial w}{\partial n}\right] = 0$
These are the **transmission conditions** for antiplane shear. Note that while displacement $w$ and the product $\mu \partial w / \partial n$ are continuous, the [displacement gradient](@entry_id:165352) $\nabla w$ (and thus the strain and stress) will generally be discontinuous across the interface if $\mu_1 \neq \mu_2$.

### Variational Formulation and Analogies

The [boundary value problem](@entry_id:138753) for antiplane shear can be elegantly reformulated using [variational principles](@entry_id:198028), which form the foundation for powerful numerical methods like the Finite Element Method. The central concept is the **[total potential energy](@entry_id:185512)** functional, $\Pi[w]$, which for a [conservative system](@entry_id:165522) is the difference between the total internal [strain energy](@entry_id:162699) and the potential of the external loads.

The **[strain energy density](@entry_id:200085)** (energy per unit volume) is $U_0 = \frac{1}{2} \boldsymbol{\sigma} : \boldsymbol{\varepsilon}$. For antiplane shear, this simplifies to [@problem_id:2615448]:
$U_0 = \frac{1}{2} (\tau_{xz} \gamma_{xz} + \tau_{yz} \gamma_{yz}) = \frac{1}{2} \mu \left[ \left(\frac{\partial w}{\partial x}\right)^2 + \left(\frac{\partial w}{\partial y}\right)^2 \right] = \frac{1}{2}\mu |\nabla w|^2$

The [total potential energy](@entry_id:185512) functional $\Pi[w]$ is obtained by integrating the [strain energy density](@entry_id:200085) and subtracting the work done by the body force $b_z$ and the prescribed [surface traction](@entry_id:198058) $\bar{t}$ on $\Gamma_t$ [@problem_id:2615437]:
$$ \Pi[w] = \int_{\Omega} \frac{1}{2}\mu |\nabla w|^2 \,dA - \int_{\Omega} b_z w \,dA - \int_{\Gamma_t} \bar{t} w \,ds $$

The Principle of Minimum Potential Energy states that of all admissible displacement fields, the one that satisfies equilibrium minimizes this functional. An **admissible displacement field** is one that is sufficiently smooth for the [energy functional](@entry_id:170311) to be finite and that satisfies any prescribed kinematic (Dirichlet) boundary conditions. In a modern framework, the appropriate space of functions is the **Sobolev space** $H^1(\Omega)$, which consists of functions that are square-integrable and have square-integrable first derivatives. The set of admissible functions is then:
$W_{\mathrm{ad}} = \{ w \in H^1(\Omega) \,:\, w = \bar{w} \text{ on } \Gamma_w \text{ in the trace sense} \}$
The requirement that displacement is prescribed on a portion of the boundary ($\Gamma_w$ has positive measure) is crucial for ensuring a unique solution.

In the variational setting, the Dirichlet condition $w=\bar{w}$ is called an **essential** boundary condition because it must be explicitly enforced on the space of [trial functions](@entry_id:756165). The Neumann condition is a **natural** boundary condition as it emerges from the minimization process itself. In the **[principle of virtual work](@entry_id:138749)**, any [virtual displacement](@entry_id:168781) $\delta w$ must vanish on the Dirichlet portion of the boundary, $\delta w = 0$ on $\Gamma_w$. This ensures that the work of the unknown reaction forces on $\Gamma_w$ does no virtual work [@problem_id:2615447].

Finally, the mathematical structure of antiplane shear is analogous to several other problems in physics and engineering. A famous example is the **Saint-Venant torsion** of a [prismatic bar](@entry_id:190143) [@problem_id:2615416]. In the torsion problem, the axial displacement is described by a **[warping function](@entry_id:187475)** $\psi(x,y)$, which, for a homogeneous bar, satisfies the Laplace equation: $\nabla^2 \psi = 0$. The traction-free condition on the lateral boundary of the bar imposes a Neumann-type boundary condition on the [warping function](@entry_id:187475):
$\frac{\partial \psi}{\partial n} = y n_x - x n_y$
The governing equation and the type of boundary condition are identical to those for an antiplane shear problem. Specifically, the torsion problem for a bar with cross-section $\Omega$ is mathematically equivalent to an antiplane shear problem on the same domain $\Omega$ with no [body forces](@entry_id:174230) and a prescribed boundary traction $t_z = G(y n_x - x n_y)$, where one identifies the out-of-plane displacement $w$ with the [warping function](@entry_id:187475) $\psi$. This powerful analogy allows solutions and insights from one problem to be transferred directly to the other.