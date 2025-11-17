## Introduction
Understanding how a solid material deforms under a concentrated load is a fundamental problem in mechanics, with implications ranging from geotechnical engineering to nanoscale material design. While the elastic field due to a point force in an infinite medium—the Kelvin solution—provides a theoretical starting point, real-world applications almost always involve bodies with boundaries, such as the ground beneath a foundation or the surface of a machine component. The presence of a free surface dramatically alters the stress and displacement fields, creating a more complex and practical problem.

This article bridges the gap between the idealized infinite-space solution and its application to the canonical bounded domain: the [elastic half-space](@entry_id:194631). We will explore how to correctly account for a traction-free surface using the powerful [method of images](@entry_id:136235), revealing why a simple analogy to electrostatics is insufficient and what system of singularities is required instead.

Across the following chapters, you will build a comprehensive understanding of this cornerstone topic. The "Principles and Mechanisms" chapter will derive the governing equations and guide you from the Kelvin solution for an infinite body to the Mindlin and Boussinesq solutions for a half-space. In "Applications and Interdisciplinary Connections," we will explore how these theoretical results are applied to solve practical problems in [contact mechanics](@entry_id:177379), materials science, and biophysics. Finally, "Hands-On Practices" will offer concrete exercises to reinforce these concepts and develop your analytical skills.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mathematical mechanisms that govern the elastic response of a solid to a concentrated point force. We begin by establishing the foundational equations of linear [elastostatics](@entry_id:198298). We then develop the solution for a point force within an infinite medium—the celebrated Kelvin solution. Building upon this, we introduce the complexities of a bounded domain by considering an [elastic half-space](@entry_id:194631) with a traction-free surface. The core of our analysis will be the [method of images](@entry_id:136235), a powerful superposition technique. We will demonstrate why a simple image construction fails in elasticity and detail the more sophisticated system of image singularities required to correctly solve the problem, leading to the Mindlin solution. Finally, we will connect this solution for an internal force to the classical Boussinesq problem of a force applied directly to the surface.

### Governing Equations of Linear Elastostatics

The behavior of a static, homogeneous, and isotropic linear elastic material is described by a set of three fundamental physical principles, expressed mathematically.

First, the **[kinematics](@entry_id:173318)** of deformation are described by the relationship between the [displacement vector field](@entry_id:196067), $u_i(\mathbf{x})$, and the [small-strain tensor](@entry_id:754968), $\varepsilon_{ij}(\mathbf{x})$. The strain tensor captures the local deformation (stretching and shearing) and is defined as the symmetric part of the [displacement gradient](@entry_id:165352):
$$
\varepsilon_{ij} = \frac{1}{2} (u_{i,j} + u_{j,i})
$$
where the notation $u_{i,j}$ denotes the partial derivative $\partial u_i / \partial x_j$.

Second, the **constitutive law** relates the internal forces, represented by the Cauchy stress tensor $\sigma_{ij}$, to the deformation. For an isotropic linear elastic material, this relationship is given by Hooke's Law:
$$
\sigma_{ij} = \lambda \varepsilon_{kk} \delta_{ij} + 2\mu \varepsilon_{ij}
$$
Here, $\lambda$ and $\mu$ are the Lamé parameters, which characterize the material's elastic properties. $\mu$ is the shear modulus, and $\delta_{ij}$ is the Kronecker delta. The term $\varepsilon_{kk} = \nabla \cdot \mathbf{u}$ represents the [volumetric strain](@entry_id:267252) (dilatation).

Third, the principle of **[static equilibrium](@entry_id:163498)** requires that the [net force](@entry_id:163825) on any portion of the body is zero. In the absence of acceleration, this leads to the [balance of linear momentum](@entry_id:193575), which in differential form is:
$$
\sigma_{ij,j} + f_i = 0
$$
where $f_i(\mathbf{x})$ is the [body force](@entry_id:184443) density, representing forces like gravity or, as we will see, concentrated loads [@problem_id:2652598].

By substituting the kinematic and [constitutive relations](@entry_id:186508) into the [equilibrium equation](@entry_id:749057), we can express the governing equations entirely in terms of the displacement field $\mathbf{u}$. This yields the **Navier-Cauchy equations of [elastostatics](@entry_id:198298)**:
$$
\mu u_{i,jj} + (\lambda+\mu) u_{j,ij} + f_i = 0
$$
In vector notation, this is $\mu \nabla^2 \mathbf{u} + (\lambda+\mu) \nabla(\nabla \cdot \mathbf{u}) + \mathbf{f} = \mathbf{0}$. These three coupled, second-order partial differential equations form the mathematical foundation for the problems discussed in this chapter.

### The Point Force as a Distributional Body Force

A central concept in this topic is the idealization of a **concentrated point force**. Physically, any applied load is distributed over a small area or volume. However, when the dimensions of this loaded region are negligible compared to the dimensions of the body, it is mathematically convenient to model the load as acting at a single point. This is achieved by representing the [body force](@entry_id:184443) density, $f_i(\mathbf{x})$, using the Dirac delta distribution. A point force with components $F_i$ applied at a location $\mathbf{x}_0$ is described by the [body force](@entry_id:184443) density:
$$
f_i(\mathbf{x}) = F_i \delta(\mathbf{x} - \mathbf{x}_0)
$$
The delta distribution $\delta(\mathbf{x} - \mathbf{x}_0)$ is zero everywhere except at $\mathbf{x}=\mathbf{x}_0$, and its integral over any volume containing $\mathbf{x}_0$ is unity. This representation correctly ensures that the total force applied to the body is $\int_\Omega f_i(\mathbf{x}) dV = F_i$.

The use of distributions is made rigorous through the **[weak formulation](@entry_id:142897)** of the [equilibrium equations](@entry_id:172166), also known as the [principle of virtual work](@entry_id:138749). By multiplying the [equilibrium equation](@entry_id:749057) $\sigma_{ij,j} + f_i = 0$ by an arbitrary, smooth "test" [displacement field](@entry_id:141476) $\phi_i(\mathbf{x})$ and integrating over the domain $\Omega$, we obtain:
$$
\int_\Omega \sigma_{ij,j} \phi_i dV + \int_\Omega f_i \phi_i dV = 0
$$
Applying the [divergence theorem](@entry_id:145271) and integration by parts to the first term yields the general weak form:
$$
\int_\Omega \sigma_{ij} \phi_{i,j} dV = \int_{\partial\Omega} t_i \phi_i dS + \int_\Omega f_i \phi_i dV
$$
where $t_i = \sigma_{ij}n_j$ is the [traction vector](@entry_id:189429) on the boundary $\partial\Omega$. In the case of a point force at an interior point $\mathbf{x}_0$, the [body force](@entry_id:184443) integral becomes, by the definition of the delta distribution, $F_i \phi_i(\mathbf{x}_0)$. For a [traction-free boundary](@entry_id:197683), $t_i = 0$, and the boundary integral vanishes, leading to the specific weak form [@problem_id:2652625]:
$$
\int_\Omega \sigma_{ij}(\mathbf{x}) \phi_{i,j}(\mathbf{x}) dV = F_i \phi_i(\mathbf{x}_0)
$$
This formulation is fundamental to both the theoretical analysis and numerical solution of elasticity problems involving concentrated loads.

### The Kelvin Solution: A Point Force in an Unbounded Medium

The most fundamental problem is to find the elastic field created by a single point force in an infinite, or unbounded, medium. The solution to this problem is known as the **Kelvin solution**, and it serves as the Green's function for the Navier-Cauchy equations. The displacement $u_i(\mathbf{x})$ due to a force $F_j$ at the origin is given by $u_i(\mathbf{x}) = U_{ij}(\mathbf{x}) F_j$, where $U_{ij}(\mathbf{x})$ is the Kelvin displacement tensor. It is the solution to
$$
\mu U_{ij,kk} + (\lambda+\mu) U_{kj,ki} + \delta_{ij} \delta(\mathbf{x}) = 0
$$
that vanishes as $|\mathbf{x}| \to \infty$.

A powerful method for solving the homogeneous Navier equations is the **Papkovich-Neuber (PN) representation**, which states that any sufficiently smooth displacement field can be expressed in terms of a harmonic [vector potential](@entry_id:153642) $\mathbf{\Phi}$ and a harmonic scalar potential $\chi$ (i.e., $\nabla^2\mathbf{\Phi}=\mathbf{0}$ and $\nabla^2\chi=\mathbf{0}$). The general form is:
$$
\mathbf{u} = \frac{1}{2\mu} \left\{ 4(1-\nu)\mathbf{\Phi} - \nabla(\mathbf{x} \cdot \mathbf{\Phi} + \chi) \right\}
$$
where $\nu$ is the Poisson's ratio. The great utility of this representation is that it automatically satisfies the governing Navier equations. By selecting appropriate singular harmonic potentials, one can construct solutions to problems involving point forces [@problem_id:2652638].

The derivation using PN potentials or other methods like Fourier transforms yields the celebrated Kelvin tensor. For a force at point $\mathbf{x}_0$, the displacement at point $\mathbf{x}$ is described by the tensor $U_{ij}(\mathbf{x}, \mathbf{x}_0)$. Letting $\mathbf{R} = \mathbf{x} - \mathbf{x}_0$, $R_i = x_i - x_{0,i}$, and $r = |\mathbf{R}|$, the Kelvin solution is [@problem_id:2652624]:
$$
U_{ij}(\mathbf{x}, \mathbf{x}_0) = \frac{1}{16\pi \mu (1-\nu)} \left[ (3-4\nu) \frac{\delta_{ij}}{r} + \frac{R_i R_j}{r^3} \right]
$$
This solution has two distinct parts. The first term, proportional to $\delta_{ij}/r$, represents an isotropic decay of displacement from the source, analogous to the potential in other physical field theories. Its magnitude is influenced by the material's [compressibility](@entry_id:144559) via Poisson's ratio $\nu$. The second term, proportional to $R_i R_j / r^3$, is anisotropic and directional, projecting the response along the line connecting the source and field points [@problem_id:2652601]. Both terms decay as $1/r$, ensuring the displacement vanishes at infinity.

### The Method of Images for the Elastic Half-Space

Real-world problems rarely involve infinite media. A more practical and canonical geometry is the **[elastic half-space](@entry_id:194631)**, a body occupying the region $z > 0$. We now consider the problem of a point force applied at an interior point $\mathbf{x}_0 = (0,0,h)$ with $h > 0$, where the boundary plane at $z=0$ is **traction-free**. This means the stress components $\sigma_{xz}$, $\sigma_{yz}$, and $\sigma_{zz}$ must all be zero everywhere on the plane $z=0$.

The Kelvin solution, by itself, does not satisfy this boundary condition; a point force at $(0,0,h)$ in an infinite medium will induce non-zero tractions on the plane $z=0$. To solve the half-space problem, we use the **method of images**. The principle of superposition allows us to construct the solution as the sum of two fields:
1.  The primary field, which is the Kelvin solution for the original force at $\mathbf{x}_0$ in an infinite medium.
2.  A correction, or image, field, generated by a system of fictitious singularities placed at the mirror-image point $\mathbf{x}_0^* = (0,0,-h)$.

The image singularities must be chosen such that their elastic field, when added to the primary field, exactly cancels the tractions on the plane $z=0$.

#### The Failure of a Simple Image Force

Drawing an analogy from electrostatics, where a point charge near a grounded conducting plane is handled with a single opposite image charge, one might attempt to solve the elasticity problem with a single image point force at $\mathbf{x}_0^*$. However, this simple approach fails.

Let's explore why. The traction vector on the surface $z=0$ has three components: two shear tractions ($\sigma_{xz}, \sigma_{yz}$) and one normal traction ($\sigma_{zz}$). A single [image force](@entry_id:272147) vector $\mathbf{F}'$ at $\mathbf{x}_0^*$ also has three components, which seem to provide enough degrees of freedom. The problem lies in the functional form of the induced tractions. A rigorous analysis shows that the requirements to cancel the shear tractions and the normal traction are contradictory. For a general force $\mathbf{F} = (F_x, F_y, F_z)$ at $(0,0,h)$, canceling the shear tractions on $z=0$ requires an [image force](@entry_id:272147) $\mathbf{F}' = (F_x, F_y, -F_z)$, whereas canceling the normal traction requires $\mathbf{F}' = (-F_x, -F_y, F_z)$. These two conditions are mutually exclusive for any non-zero force $\mathbf{F}$ [@problem_id:2652621].

We can demonstrate this failure with a concrete calculation. Consider a vertical force $\mathbf{F} = P \mathbf{e}_z$ at $(0,0,h)$. A natural guess for an image system is a single, anti-parallel force $\mathbf{F}' = -P \mathbf{e}_z$ at $(0,0,-h)$. If this were correct, the total [normal stress](@entry_id:184326) $\sigma_{zz}$ should be zero on the plane $z=0$. Let's compute the [residual stress](@entry_id:138788) at the origin $(0,0,0)$ from this superposition. The stress field of a Kelvin solution is known. Using this, the vertical [normal stress](@entry_id:184326) at the origin from the real force is $\sigma_{zz}^{(1)} = \frac{P(2-\nu)}{4\pi(1-\nu)h^2}$. The contribution from the [image force](@entry_id:272147) is identical, $\sigma_{zz}^{(2)} = \frac{P(2-\nu)}{4\pi(1-\nu)h^2}$. The total residual stress is the sum of these two:
$$
\sigma_{zz}(0,0,0) = \sigma_{zz}^{(1)} + \sigma_{zz}^{(2)} = \frac{P(2-\nu)}{2\pi(1-\nu)h^2}
$$
This result is clearly not zero for any physically meaningful material ($\nu \neq 1/2$) [@problem_id:2652587]. This calculation quantitatively confirms that a simple [image force](@entry_id:272147) is insufficient.

The fundamental reason for this failure is that the traction field generated by a point force consists of a combination of functionally distinct spatial distributions (or kernels). A single image point force generates its own traction field with a fixed structure that cannot be arbitrarily tailored to match and cancel the field from the original source. To achieve cancellation over the entire plane, the image system must be able to generate a more general traction field. This requires a basis of different types of singularities, each producing a [linearly independent](@entry_id:148207) traction kernel on the boundary [@problem_id:2652628].

### The Mindlin Solution: The Correct Image System

The correct solution, first derived by R. D. Mindlin, requires augmenting the simple [image force](@entry_id:272147) with higher-order singularities. These include a **force dipole** and a **center of dilatation**, all located at the image point $\mathbf{x}_0^*$. The strengths of these image singularities are uniquely determined by the requirement to cancel all three traction components on the boundary $z=0$.

The resulting Green's function for the half-space is known as the **Mindlin tensor**, $G_{ij}(\mathbf{x}, \mathbf{x}_0)$. It is expressed as the sum of the original Kelvin solution and the fields from the image system. Using the notation from before, where $K_{ij}$ is the Kelvin tensor and $\mathbf{R}^* = \mathbf{x} - \mathbf{x}_0^*$, the full Mindlin solution is given by a superposition of the Kelvin solution and its derivatives evaluated at the image point [@problem_id:2652623]:
$$
G_{ij}(\mathbf{x}, \mathbf{x}_{0}) = K_{ij}(\mathbf{R}) + G_{ij}^{im}(\mathbf{x}, \mathbf{x}_0^*)
$$
The image solution $G_{ij}^{im}$ is composed of a system of singularities that includes:
- An image Kelvin source (a simple point force).
- A force dipole (related to $\partial_3 K_{ij}(\mathbf{R}^*)$).
- Additional terms involving derivatives of the Kelvin tensor and the fundamental solution of the Laplace equation, which depend on Poisson's ratio $\nu$ and the depth $h$ of the original force.

The complete expression is quite complex, but its structure reveals the physics: a simple [image force](@entry_id:272147) is supplemented by singularities whose fields have different spatial variations, providing the necessary flexibility to satisfy the three traction-free conditions simultaneously over the entire boundary plane.

### The Boussinesq Solution as a Limiting Case

A related and equally important classical problem is the **Boussinesq problem**, which deals with the stress and displacement in a half-space due to a point force applied directly *on* its surface. This can be viewed as the limiting case of the Mindlin problem as the depth of the force $h$ approaches zero.

For a vertical point force of magnitude $F$ applied at the origin on the surface of the half-space $z \ge 0$, the resulting vertical displacement on the surface ($z=0$) at a radial distance $r = \sqrt{x^2+y^2}$ is given by:
$$
u_z(r, 0) = \frac{(1-\nu^2)F}{\pi E r}
$$
where $E$ is the Young's modulus [@problem_id:2652633]. This celebrated result is a cornerstone of [contact mechanics](@entry_id:177379). It shows that the surface displacement under a point load is not localized; it creates a depression that decays slowly, as $1/r$, across the entire surface. This formula highlights the direct link between a macroscopic measurement (surface displacement) and the fundamental elastic properties of the material ($E$ and $\nu$).