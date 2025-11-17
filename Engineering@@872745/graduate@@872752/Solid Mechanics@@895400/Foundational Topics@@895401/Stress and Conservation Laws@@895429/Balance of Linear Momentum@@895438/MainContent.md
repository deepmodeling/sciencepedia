## Introduction
The motion of any continuous body, from a steel beam to the Earth's mantle, is dictated by a set of fundamental physical laws. At the heart of these laws lies the principle of the balance of linear momentum, which serves as the generalization of Newton's second law to deformable media. This principle provides the crucial link between the forces acting on a body and the resulting motion, forming a cornerstone of solid and fluid mechanics. However, moving from Newton's discrete particle mechanics to the complex, continuous world requires a rigorous framework to describe [internal forces](@entry_id:167605) and their relationship to acceleration. This article addresses this challenge by systematically developing the theory of momentum balance in a continuum.

The reader will embark on a comprehensive journey through this fundamental principle, structured across three distinct chapters. The first chapter, **Principles and Mechanisms**, establishes the theoretical foundation, deriving the local equations of motion from first principles and introducing the essential concept of the Cauchy stress tensor. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the immense power of this principle by exploring its use in solving problems ranging from static equilibrium in civil engineering to dynamic [wave propagation](@entry_id:144063) in [seismology](@entry_id:203510) and advanced [multiphysics](@entry_id:164478) models. Finally, the third chapter, **Hands-On Practices**, provides practical problems that allow the reader to apply these concepts to tangible engineering and physics scenarios, solidifying their understanding. By progressing through these sections, the reader will gain a deep and functional mastery of the balance of [linear momentum](@entry_id:174467) and its central role in modern mechanics.

## Principles and Mechanisms

The motion of a continuous body is governed by fundamental physical laws, which, when expressed mathematically, form the basis of [continuum mechanics](@entry_id:155125). Having established the necessary kinematic framework, we now turn to the principles of kinetics, which relate the motion of a body to the forces that cause it. The primary law governing this relationship is the balance of linear momentum, a generalization of Newton's second law to [deformable bodies](@entry_id:201887). This chapter will systematically develop this principle from its foundational postulates to its various mathematical formulations.

### Forces in a Continuum and the Traction Vector

Forces acting on a continuum body are classified into two types: **[body forces](@entry_id:174230)** and **contact forces**. Body forces, such as gravity or electromagnetic forces, act on the material particles throughout the volume of the body without any physical contact. We represent these forces by a vector field $\mathbf{b}(\mathbf{x}, t)$, defined as the force per unit mass. The total [body force](@entry_id:184443) on a volume $V$ is thus $\int_V \rho \mathbf{b} \, dV$, where $\rho$ is the mass density.

Contact forces, in contrast, are transmitted across surfaces, either external boundaries of the body or internal, fictitious surfaces. These forces represent the short-range [molecular interactions](@entry_id:263767) between adjacent parts of the material. The central postulate of continuum mechanics, attributed to Augustin-Louis Cauchy, is that these complex interactions can be described by a continuously distributed vector field known as the **[traction vector](@entry_id:189429)**.

Consider an arbitrary point $\mathbf{x}$ within a continuum. Imagine a small, flat surface element $\Delta S$ containing $\mathbf{x}$, with a defined orientation given by its [unit normal vector](@entry_id:178851) $\mathbf{n}$. This surface divides the material into a "positive" side (the one $\mathbf{n}$ points into) and a "negative" side. The material on the negative side exerts a resultant contact force $\Delta\mathbf{F}_c$ on the material on the positive side across $\Delta S$. The traction vector $\mathbf{t}(\mathbf{x}, \mathbf{n}, t)$ at point $\mathbf{x}$ on a surface with normal $\mathbf{n}$ is defined as the limit of the force per unit area as the area of the surface element shrinks to zero around the point [@problem_id:2616721]:

$$
\mathbf{t}(\mathbf{x}, \mathbf{n}, t) = \lim_{\Delta A \to 0} \frac{\Delta\mathbf{F}_c}{\Delta A}
$$

where $\Delta A$ is the area of the surface element $\Delta S$. The traction vector has units of force per area, which are the units of stress. It represents the local intensity and direction of the [contact force](@entry_id:165079) at a point for a specific surface orientation. It is crucial to recognize that the traction vector $\mathbf{t}$ depends not only on the position $\mathbf{x}$ and time $t$ but fundamentally on the orientation of the surface, $\mathbf{n}$. By Newton's third law of action and reaction, the force exerted by the positive side on the negative side is $-\Delta\mathbf{F}_c$. This implies a fundamental property of the [traction vector](@entry_id:189429) known as **Cauchy's lemma**:

$$
\mathbf{t}(\mathbf{x}, -\mathbf{n}, t) = -\mathbf{t}(\mathbf{x}, \mathbf{n}, t)
$$

### The Global Balance of Linear Momentum

With the concepts of body and contact forces established, we can now state the principle of balance of linear momentum, also known as **Cauchy's first law of motion**. This principle is a direct application of Newton's second law to a continuous body. For any arbitrary **material volume** $B(t)$—a volume composed of the same material particles at all times—the principle states that the time rate of change of the [total linear momentum](@entry_id:173071) of the body is equal to the resultant of all external forces acting on it.

Mathematically, this is expressed in integral form as follows [@problem_id:2616735]:

$$
\frac{d}{dt} \int_{B(t)} \rho(\mathbf{x}, t) \mathbf{v}(\mathbf{x}, t) \, dV = \int_{B(t)} \rho(\mathbf{x}, t) \mathbf{b}(\mathbf{x}, t) \, dV + \oint_{\partial B(t)} \mathbf{t}(\mathbf{x}, \mathbf{n}, t) \, dA
$$

Let us dissect each term in this fundamental equation:

*   The term on the left, $\frac{d}{dt} \int_{B(t)} \rho \mathbf{v} \, dV$, represents the **rate of change of the [total linear momentum](@entry_id:173071)** of the material body. The integral sums the [momentum density](@entry_id:271360) $\rho \mathbf{v}$ over the entire material volume. The time derivative is a [material derivative](@entry_id:266939) because it follows the deforming material volume $B(t)$.

*   The first term on the right, $\int_{B(t)} \rho \mathbf{b} \, dV$, is the **resultant [body force](@entry_id:184443)** acting on the volume.

*   The second term on the right, $\oint_{\partial B(t)} \mathbf{t} \, dA$, is the **resultant [contact force](@entry_id:165079)** acting on the boundary $\partial B(t)$ of the body. It is the sum of all traction vectors over the entire surface.

This integral equation holds for any sub-volume of the continuum and forms the foundation for deriving the differential equations of motion.

### The Cauchy Stress Tensor

The dependence of the traction vector $\mathbf{t}$ on the normal vector $\mathbf{n}$ is not arbitrary. A remarkable result, also due to Cauchy, demonstrates that this dependence is linear. This can be proven by applying the integral balance of linear momentum to an infinitesimal tetrahedron at a point $\mathbf{x}_0$ [@problem_id:2616731].

Consider a small tetrahedron with three faces aligned with the coordinate planes and one oblique face with outward normal $\mathbf{n}$. Let the characteristic size of the tetrahedron be $\ell$. The areas of its faces scale as $O(\ell^2)$, while its volume scales as $O(\ell^3)$. The integral momentum balance equation applied to this tetrahedron involves [surface integrals](@entry_id:144805) over the four faces and [volume integrals](@entry_id:183482) for body force and inertia. As we shrink the tetrahedron to the point $\mathbf{x}_0$ by letting $\ell \to 0$, the [volume integrals](@entry_id:183482) (scaling as $O(\ell^3)$) vanish much faster than the [surface integrals](@entry_id:144805) (scaling as $O(\ell^2)$). In the limit, the momentum balance equation reduces to a simple equilibrium of forces exerted by the tractions on the four faces.

This analysis reveals that the [traction vector](@entry_id:189429) $\mathbf{t}$ on the oblique face is a linear combination of the traction vectors on the three coordinate faces, with the coefficients being the components of the [normal vector](@entry_id:264185) $\mathbf{n}$. This linear relationship implies the existence of a second-order tensor, the **Cauchy stress tensor** $\boldsymbol{\sigma}(\mathbf{x}, t)$, that maps the [normal vector](@entry_id:264185) to the traction vector:

$$
\mathbf{t}(\mathbf{x}, \mathbf{n}, t) = \boldsymbol{\sigma}(\mathbf{x}, t) \mathbf{n}
$$

This relation is known as **Cauchy's stress theorem**. It is a cornerstone of [continuum mechanics](@entry_id:155125), as it fully characterizes the state of stress at a point. Instead of needing to know the traction for every possible surface orientation, we only need to know the nine components of the tensor $\boldsymbol{\sigma}$. In a Cartesian coordinate system with basis vectors $\{\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3\}$, the components of the stress tensor have a direct physical interpretation. The component $\sigma_{ij}$ represents the $i$-th component of the traction vector acting on a surface whose normal is in the $j$-th direction. Consequently, the columns of the matrix representation of $\boldsymbol{\sigma}$ are simply the traction vectors on the coordinate planes [@problem_id:2616722]:

$$
[\boldsymbol{\sigma}] = \begin{pmatrix} |  |  | \\ \mathbf{t}(\mathbf{e}_1)  \mathbf{t}(\mathbf{e}_2)  \mathbf{t}(\mathbf{e}_3) \\ |  |  | \end{pmatrix} = \begin{pmatrix} \sigma_{11}  \sigma_{12}  \sigma_{13} \\ \sigma_{21}  \sigma_{22}  \sigma_{23} \\ \sigma_{31}  \sigma_{32}  \sigma_{33} \end{pmatrix}
$$

For instance, if the tractions on the coordinate planes at a point are given by $\mathbf{t}(\mathbf{e}_1) = \begin{pmatrix} 2  -1  4 \end{pmatrix}^T$, $\mathbf{t}(\mathbf{e}_2) = \begin{pmatrix} 0  3  5 \end{pmatrix}^T$, and $\mathbf{t}(\mathbf{e}_3) = \begin{pmatrix} 4  1  0 \end{pmatrix}^T$, the stress tensor at that point is $\boldsymbol{\sigma} = \begin{pmatrix} 2  0  4 \\ -1  3  1 \\ 4  5  0 \end{pmatrix}$. We can then find the traction on any other plane, such as one with normal $\mathbf{n}$, by the simple matrix-vector product $\mathbf{t}(\mathbf{n}) = \boldsymbol{\sigma} \mathbf{n}$.

### The Local Balance of Linear Momentum: Eulerian Description

The integral form of the momentum balance is valid for a body of any size. To obtain a local description of motion at a point, we convert the integral equation into a differential equation. This is achieved by applying two key mathematical theorems.

First, using Cauchy's stress theorem $\mathbf{t} = \boldsymbol{\sigma} \mathbf{n}$, the surface integral of contact forces can be transformed into a [volume integral](@entry_id:265381) using the **Divergence Theorem**:
$$
\oint_{\partial B(t)} \mathbf{t} \, dA = \oint_{\partial B(t)} \boldsymbol{\sigma} \mathbf{n} \, dA = \int_{B(t)} (\nabla \cdot \boldsymbol{\sigma}) \, dV
$$
Here, $\nabla \cdot \boldsymbol{\sigma}$ is the **divergence of the stress tensor**.

Second, the time derivative of the momentum integral can be moved inside the integral using the **Reynolds Transport Theorem**, which for a material volume yields:
$$
\frac{d}{dt} \int_{B(t)} \rho \mathbf{v} \, dV = \int_{B(t)} \rho \frac{D\mathbf{v}}{Dt} \, dV = \int_{B(t)} \rho \mathbf{a} \, dV
$$
where $\mathbf{a} = D\mathbf{v}/Dt = \dot{\mathbf{v}}$ is the [material acceleration](@entry_id:270992).

Substituting these back into the integral balance equation gives:
$$
\int_{B(t)} \rho \mathbf{a} \, dV = \int_{B(t)} \rho \mathbf{b} \, dV + \int_{B(t)} (\nabla \cdot \boldsymbol{\sigma}) \, dV
$$
Since this equation must hold for any arbitrary material volume $B(t)$, the integrands must be equal. This **localization argument** yields the local, differential form of the balance of [linear momentum](@entry_id:174467), also known as **Cauchy's equation of motion**:

$$
\nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b} = \rho \mathbf{a}
$$

This vector equation represents three scalar equations. Using [index notation](@entry_id:191923) in a Cartesian coordinate system, where a comma denotes [partial differentiation](@entry_id:194612) (e.g., $\sigma_{ij,j} \equiv \frac{\partial \sigma_{ij}}{\partial x_j}$), the equation is written as [@problem_id:2616702]:

$$
\sigma_{ij,j} + \rho b_i = \rho \dot{v}_i
$$

The term $\nabla \cdot \boldsymbol{\sigma}$ represents the net contact force per unit volume arising from the spatial variation of the stress field. If stresses are uniform throughout a region ($\boldsymbol{\sigma} = \text{const.}$), their divergence is zero, and they contribute no [net force](@entry_id:163825) to accelerate the material within that region. Only a stress *gradient* can produce a net internal force. For example, given a specific stress field, one can compute its divergence to find the internal force density field it generates, which must be balanced by [body forces](@entry_id:174230) and inertia [@problem_id:2616742].

### Balance of Angular Momentum and Symmetry of Stress

In addition to [linear momentum](@entry_id:174467), the balance of **angular momentum** must also be satisfied. This principle states that the time rate of change of the total angular momentum of a body equals the sum of the moments of all external forces. A derivation similar to the one for [linear momentum](@entry_id:174467), but starting with the moment of forces (e.g., $\mathbf{x} \times \mathbf{t}$), leads to a profound conclusion regarding the stress tensor. Assuming there are no distributed body couples acting on the material, the local [balance of angular momentum](@entry_id:181848) requires that the Cauchy stress tensor be symmetric [@problem_id:2616733]:

$$
\boldsymbol{\sigma} = \boldsymbol{\sigma}^T \quad \text{or} \quad \sigma_{ij} = \sigma_{ji}
$$

This is **Cauchy's second law of motion**. This symmetry is of paramount importance, as it reduces the number of independent components of the stress tensor at a point from nine to six. This property will be assumed to hold for the remainder of our studies unless explicitly stated otherwise.

### The Lagrangian Description and Referential Stresses

The formulation $\nabla \cdot \boldsymbol{\sigma} + \rho \mathbf{b} = \rho \mathbf{a}$ is an **Eulerian** description, as all quantities are expressed in terms of the current spatial coordinates $\mathbf{x}$. In solid mechanics, it is often more convenient to use a **Lagrangian** description, where the governing equations are formulated in terms of the material coordinates $\mathbf{X}$ in a fixed reference configuration $\mathcal{B}_0$.

To achieve this, we map the integral balance of momentum back to the reference configuration. This process naturally introduces new [stress measures](@entry_id:198799) that relate forces in the current configuration to areas in the reference configuration.

The first such measure is the **First Piola-Kirchhoff (PK1) stress tensor**, denoted by $\mathbf{P}$. It is defined such that the force element $d\mathbf{f} = \mathbf{t} \, da$ on a current surface element is related to the reference normal $\mathbf{N}$ and reference area element $dA$ by $d\mathbf{f} = \mathbf{P} \mathbf{N} \, dA$. The PK1 tensor is related to the Cauchy stress by [@problem_id:2616703]:

$$
\mathbf{P} = J \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

where $\mathbf{F}$ is the [deformation gradient](@entry_id:163749) and $J = \det \mathbf{F}$. $\mathbf{P}$ is a "two-point" tensor as it maps a vector in the reference configuration (the normal $\mathbf{N}$) to a vector in the current configuration (the force $d\mathbf{f}$). Using this definition and mapping all integrals to the reference domain, the local balance of linear momentum in the material description becomes:

$$
\mathrm{Div}(\mathbf{P}) + \rho_0 \mathbf{b} = \rho_0 \mathbf{a}
$$

Here, $\mathrm{Div}(\cdot)$ is the [divergence operator](@entry_id:265975) with respect to the material coordinates $\mathbf{X}$, and $\rho_0$ is the density in the reference configuration. Despite the symmetry of $\boldsymbol{\sigma}$, the PK1 stress tensor $\mathbf{P}$ is generally **non-symmetric**. [@problem_id:2616708]

Another important referential stress measure is the **Second Piola-Kirchhoff (PK2) stress tensor**, $\mathbf{S}$. It is obtained by pulling the force vector itself back to the reference configuration. Its definition and relation to other measures are:

$$
\mathbf{S} = \mathbf{F}^{-1} \mathbf{P} = J \mathbf{F}^{-1} \boldsymbol{\sigma} \mathbf{F}^{-T}
$$

A key property of the PK2 stress tensor is that it is **symmetric** as a direct consequence of the symmetry of the Cauchy stress. While $\mathbf{S}$ does not appear directly in a simple [divergence form](@entry_id:748608) in the momentum balance equation, its symmetry and the fact that it is defined purely on the reference configuration make it extremely useful for formulating [constitutive equations](@entry_id:138559) (material models). Specifically, $\mathbf{S}$ is energetically conjugate to the Green-Lagrange [strain tensor](@entry_id:193332) $\mathbf{E}$, meaning the [stress power](@entry_id:182907) per unit reference volume is given by $\mathbf{S}:\dot{\mathbf{E}}$ [@problem_id:2616703].

### Boundary and Initial Conditions

The local form of the momentum balance is a system of partial differential equations. To obtain a unique solution for a specific physical problem, these equations must be supplemented with boundary conditions on the spatial domain $\Omega$ and initial conditions for dynamic problems.

The boundary of the body, $\partial\Omega$, is typically partitioned into two [disjoint sets](@entry_id:154341), $\Gamma_t$ and $\Gamma_u$ [@problem_id:2616727]:

1.  **Traction Boundary Condition**: On the portion of the boundary $\Gamma_t$, the forces are prescribed. This is expressed by specifying the traction vector, $\bar{\mathbf{t}}$. The boundary condition is:
    $$
    \boldsymbol{\sigma} \mathbf{n} = \bar{\mathbf{t}} \quad \text{on } \Gamma_t
    $$
    This is also known as a **Neumann** condition. In the context of [variational principles](@entry_id:198028) (like the [principle of virtual work](@entry_id:138749)), it is termed a **natural** boundary condition because it arises naturally from the boundary term during integration by parts.

2.  **Displacement Boundary Condition**: On the portion of the boundary $\Gamma_u$, the motion is prescribed. This is expressed by specifying the [displacement vector](@entry_id:262782), $\bar{\mathbf{u}}$. The boundary condition is:
    $$
    \mathbf{u} = \bar{\mathbf{u}} \quad \text{on } \Gamma_u
    $$
    This is also known as a **Dirichlet** condition. It is termed an **essential** boundary condition because it must be explicitly enforced on the space of admissible solutions in a [variational formulation](@entry_id:166033).

For a [well-posed problem](@entry_id:268832), conditions must be specified over the entire boundary, such that $\Gamma_t \cup \Gamma_u = \partial\Omega$ and $\Gamma_t \cap \Gamma_u = \emptyset$ (or their intersection is of lower dimension). For dynamic problems (where $\mathbf{a} \neq \mathbf{0}$), one must also specify **initial conditions**, typically the initial displacement field $\mathbf{u}(\mathbf{x}, 0)$ and the [initial velocity](@entry_id:171759) field $\mathbf{v}(\mathbf{x}, 0)$ for all points in the body.

### The Control Volume Formulation

An alternative perspective on the integral balance of momentum is the **control volume** or **Eulerian** formulation, which is particularly prevalent in fluid mechanics. Instead of a material volume that deforms with the flow, we consider a fixed or [moving control volume](@entry_id:265261) $V(t)$ in space. Material can flow across the boundaries of this [control volume](@entry_id:143882).

When applying the balance of linear momentum to such a volume, the Reynolds Transport Theorem introduces an additional term that accounts for the momentum carried by the mass crossing the boundary. The general integral balance for a [control volume](@entry_id:143882) $V(t)$ whose boundary moves with velocity $\mathbf{w}$ is [@problem_id:2616750]:

$$
\frac{d}{dt} \int_{V(t)} \rho\mathbf{v}\,dV + \int_{\partial V(t)} \rho\mathbf{v} \big[(\mathbf{v}-\mathbf{w})\cdot\mathbf{n}\big]\,dA = \int_{V(t)} \rho\mathbf{b}\,dV + \int_{\partial V(t)} \boldsymbol{\sigma}\mathbf{n}\,dA
$$

Here, the new term is the **momentum flux**: $\int_{\partial V(t)} \rho\mathbf{v} \big[(\mathbf{v}-\mathbf{w})\cdot\mathbf{n}\big]\,dA$. It represents the net rate of [convective transport](@entry_id:149512) of [linear momentum](@entry_id:174467) out of the [control volume](@entry_id:143882). The term $(\mathbf{v}-\mathbf{w})\cdot\mathbf{n}$ is the velocity of the material normal to the boundary, relative to the moving boundary itself. This term is zero for a material volume, as $\mathbf{v} = \mathbf{w}$ on the boundary by definition, which recovers the formulation we started with. This more general view highlights the distinction between the Lagrangian (material) and Eulerian (spatial/[control volume](@entry_id:143882)) descriptions of motion and their corresponding balance laws.