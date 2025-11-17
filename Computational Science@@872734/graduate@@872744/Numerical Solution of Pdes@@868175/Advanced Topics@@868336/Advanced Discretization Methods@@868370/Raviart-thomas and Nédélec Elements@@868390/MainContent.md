## Introduction
The numerical solution of [partial differential equations](@entry_id:143134) (PDEs) involving vector fields, such as those in electromagnetism and fluid dynamics, presents unique challenges. Unlike scalar problems, vector unknowns like electric fields or fluid velocities have intrinsic physical and geometric structures—a well-defined curl or divergence—that must be preserved in the discretization to avoid instability and non-physical results. Standard [finite element methods](@entry_id:749389) often fail to respect these properties, creating a critical gap in computational modeling.

This article introduces Raviart-Thomas and Nédélec elements, two foundational families of "structure-preserving" [finite element methods](@entry_id:749389) designed to bridge this gap. These methods embed the fundamental properties of [differential operators](@entry_id:275037) directly into the finite element spaces, ensuring stable and physically meaningful simulations. Across three chapters, you will gain a comprehensive understanding of these powerful tools. The first chapter, "Principles and Mechanisms," delves into their theoretical construction, exploring the H(curl) and H(div) spaces, the guiding role of the de Rham complex, and the mechanics of basis functions and mappings. The second chapter, "Applications and Interdisciplinary Connections," demonstrates their crucial role in solving real-world problems, from Maxwell's equations in electromagnetism to Darcy's law in [porous media flow](@entry_id:146440). Finally, the "Hands-On Practices" section provides guided exercises to solidify your understanding of their implementation and behavior.

## Principles and Mechanisms

The numerical solution of many [partial differential equations](@entry_id:143134), particularly those arising in electromagnetics and fluid dynamics, requires a more nuanced approach than standard scalar field problems. Vector-valued unknowns such as electric fields, magnetic fluxes, or fluid velocities possess intrinsic geometric and physical properties—such as a well-defined curl or divergence—that must be respected by the discretization scheme to ensure stable and physically meaningful results. The Raviart-Thomas and Nédélec finite element families are seminal examples of "structure-preserving" or "compatible" [discretization methods](@entry_id:272547), designed from first principles to embed the fundamental structure of the underlying differential operators into the finite element spaces themselves. This chapter elucidates the principles and mechanisms that govern their construction and application.

### The Functional-Analytic Setting: The Spaces $H(\mathrm{curl})$ and $H(\mathrm{div})$

Standard [finite element methods](@entry_id:749389) for second-order elliptic equations, such as the Poisson equation, seek solutions in the Sobolev space $H^1(\Omega)$, which consists of functions that are square-integrable and have square-integrable weak first derivatives. This space is suitable for scalar potentials, but it proves inadequate or overly restrictive for many vector field problems. For instance, the electric field at the interface between two different [dielectric materials](@entry_id:147163) can have a discontinuous normal component, precluding it from being in $(H^1(\Omega))^3$, which would require continuity of all components.

To address this, we introduce two fundamental Hilbert spaces tailored for vector fields. The space $H(\mathrm{curl};\Omega)$ is the natural setting for vector fields whose curl is physically significant and well-behaved, while $H(\mathrm{div};\Omega)$ is the corresponding space for fields with a significant divergence.

For a domain $\Omega \subset \mathbb{R}^d$ (where $d=2$ or $d=3$), these spaces are formally defined as:
$$
H(\mathrm{curl};\Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^d : \nabla \times \boldsymbol{v} \in (L^2(\Omega))^d \}
$$
$$
H(\mathrm{div};\Omega) = \{ \boldsymbol{v} \in (L^2(\Omega))^d : \nabla \cdot \boldsymbol{v} \in L^2(\Omega) \}
$$
Here, $L^2(\Omega)$ is the space of square-[integrable functions](@entry_id:191199), and the derivatives are understood in the weak (or distributional) sense. These spaces are equipped with graph norms:
$$
\|\boldsymbol{v}\|_{H(\mathrm{curl})}^2 = \|\boldsymbol{v}\|_{L^2}^2 + \|\nabla \times \boldsymbol{v}\|_{L^2}^2
$$
$$
\|\boldsymbol{v}\|_{H(\mathrm{div})}^2 = \|\boldsymbol{v}\|_{L^2}^2 + \|\nabla \cdot \boldsymbol{v}\|_{L^2}^2
$$
The physical relevance of these spaces is direct [@problem_id:3313859]. In electromagnetics, Faraday's law of induction ($\nabla \times \boldsymbol{E} = -\partial_t \boldsymbol{B}$) and Ampère's law ($\nabla \times \boldsymbol{H} = \boldsymbol{J} + \partial_t \boldsymbol{D}$) place the electric field $\boldsymbol{E}$ and magnetic field $\boldsymbol{H}$ naturally in $H(\mathrm{curl};\Omega)$. Similarly, Gauss's laws for electricity ($\nabla \cdot \boldsymbol{D} = \rho$) and magnetism ($\nabla \cdot \boldsymbol{B} = 0$) position the electric displacement $\boldsymbol{D}$ and magnetic induction $\boldsymbol{B}$ within $H(\mathrm{div};\Omega)$.

### Traces, Continuity, and Conforming Approximations

The central idea of a conforming finite element method is that the global finite element space must be a subspace of the corresponding continuous [solution space](@entry_id:200470). For [piecewise polynomial](@entry_id:144637) functions, this condition translates into specific continuity requirements across the boundaries (faces or edges) of the mesh elements. For a function in $H^1(\Omega)$, this requires the function itself to be continuous across element interfaces. The continuity conditions for $H(\mathrm{curl};\Omega)$ and $H(\mathrm{div};\Omega)$ are different and are revealed by their respective [trace theorems](@entry_id:203967).

A **[trace operator](@entry_id:183665)** maps a function defined on a domain $\Omega$ to its values on the boundary $\partial\Omega$. For functions in $H(\mathrm{curl};\Omega)$ or $H(\mathrm{div};\Omega)$, which may not be continuous, these traces cannot be defined by simple restriction and must be understood in a weak sense through integration by parts. For sufficiently smooth vector fields $\boldsymbol{v}$ and scalar fields $q$, Green's identities provide the starting point [@problem_id:3334033]:
$$
\int_{\Omega} (\nabla \cdot \boldsymbol{v}) q \, dx + \int_{\Omega} \boldsymbol{v} \cdot \nabla q \, dx = \int_{\partial\Omega} (\boldsymbol{v} \cdot \boldsymbol{n}) q \, dS
$$
$$
\int_{\Omega} (\nabla \times \boldsymbol{v}) \cdot \boldsymbol{w} \, dx - \int_{\Omega} \boldsymbol{v} \cdot (\nabla \times \boldsymbol{w}) \, dx = \int_{\partial\Omega} (\boldsymbol{n} \times \boldsymbol{v}) \cdot \boldsymbol{w} \, dS
$$
These identities allow us to define trace operators for functions that are not smooth enough for the classical theorems to apply.

For a vector field $\boldsymbol{v} \in H(\mathrm{div};\Omega)$, the first identity motivates the definition of the **normal trace**, $\gamma_n(\boldsymbol{v})$. This trace is a [continuous linear operator](@entry_id:269916) mapping from $H(\mathrm{div};\Omega)$ to the dual space $H^{-1/2}(\partial\Omega)$ [@problem_id:3438126]. Consequently, for a [piecewise polynomial](@entry_id:144637) vector field to be in $H(\mathrm{div};\Omega)$, its **normal component must be continuous** across all interior element faces.

For a vector field $\boldsymbol{v} \in H(\mathrm{curl};\Omega)$, the second identity motivates the definition of the **tangential trace**, $\gamma_t(\boldsymbol{v})$. In three dimensions, this trace is often defined as $\gamma_t(\boldsymbol{v}) = \boldsymbol{n} \times \boldsymbol{v}|_{\partial\Omega}$. In two dimensions, it is the scalar tangential component $\boldsymbol{v} \cdot \boldsymbol{t}$. The [trace theorem](@entry_id:136726) for $H(\mathrm{curl})$ states that $\gamma_t$ is a [continuous linear operator](@entry_id:269916) mapping into an appropriate fractional Sobolev space on the boundary (e.g., $H^{-1/2}(\partial\Omega)$ in 2D) [@problem_id:3438126] [@problem_id:3334033]. Therefore, for a [piecewise polynomial](@entry_id:144637) vector field to be in $H(\mathrm{curl};\Omega)$, its **tangential components must be continuous** across all interior element faces.

These two distinct continuity requirements—normal continuity for $H(\mathrm{div})$ and tangential continuity for $H(\mathrm{curl})$—are the fundamental principles guiding the design of Raviart-Thomas and Nédélec elements, respectively.

### The de Rham Complex: A Blueprint for Finite Element Design

The gradient, curl, and divergence operators are not independent; they are linked by the fundamental [vector calculus identities](@entry_id:161863) $\nabla \times (\nabla \phi) = \boldsymbol{0}$ and $\nabla \cdot (\nabla \times \boldsymbol{A}) = 0$. These identities state that the image of the [gradient operator](@entry_id:275922) is contained in the kernel of the [curl operator](@entry_id:184984), and the image of the curl operator is contained in the kernel of the [divergence operator](@entry_id:265975). This structure can be represented as a sequence of spaces and [differential operators](@entry_id:275037), known as the **de Rham complex**:

$$
0 \to \mathbb{R} \xrightarrow{\subset} H^1(\Omega) \xrightarrow{\nabla} H(\mathrm{curl};\Omega) \xrightarrow{\nabla\times} H(\mathrm{div};\Omega) \xrightarrow{\nabla\cdot} L^2(\Omega) \to 0
$$

A sequence is said to be **exact** if, at each stage, the image of the incoming map is exactly equal to the kernel of the outgoing map. For contractible domains (informally, domains without holes), the de Rham complex is exact [@problem_id:3313859]. This [exactness](@entry_id:268999) property is not merely a mathematical curiosity; it is a deep statement about the structure of [vector fields](@entry_id:161384) and potentials. For example, $\ker(\nabla \times) = \mathrm{im}(\nabla)$ means that any curl-free vector field can be expressed as the gradient of a [scalar potential](@entry_id:276177).

In numerical computations, particularly for eigenvalue problems like the Maxwell cavity problem [@problem_id:3350344], a naive [discretization](@entry_id:145012) can fail to respect this structure. If the discrete kernel of the [curl operator](@entry_id:184984) is larger than the discrete image of the [gradient operator](@entry_id:275922), the numerical scheme will admit non-physical, or **spurious**, solutions. The primary goal of compatible [finite element methods](@entry_id:749389) is to construct discrete finite element spaces ($S_h \subset H^1, N_h \subset H(\mathrm{curl}), \dots$) that form a discrete de Rham complex which is also exact. This ensures that the fundamental properties of the continuous operators are inherited by the discrete approximation, thereby eliminating [spurious modes](@entry_id:163321) by design.

### Constructing Conforming Elements: Nédélec and Raviart-Thomas Families

With the continuity requirements and the de Rham complex as our blueprint, we can now systematically construct the finite element spaces.

#### Nédélec Elements for $H(\mathrm{curl})$

To construct an $H(\mathrm{curl})$-conforming space, we must enforce tangential continuity. Nédélec (or "edge") elements achieve this by defining degrees of freedom (DoFs) that uniquely determine and enforce the behavior of the tangential component on element boundaries.

For a tetrahedral mesh in $\mathbb{R}^3$, the DoFs for the lowest-order Nédélec space are associated with the **edges** of the mesh. Specifically, for each edge $e$, a DoF is defined as the line integral of the vector field's tangential component along that edge:
$$
\text{DoF}_e(\boldsymbol{v}) = \int_e \boldsymbol{v} \cdot \boldsymbol{t} \, ds
$$
where $\boldsymbol{t}$ is a [unit tangent vector](@entry_id:262985) along the edge [@problem_id:3329984]. By assigning a single global DoF to each edge in the mesh, we ensure that any two elements sharing that edge will have the same value for this integral. This is sufficient to guarantee the continuity of the tangential component not just along the edge, but across the entire shared face, thus ensuring $N_h \subset H(\mathrm{curl};\Omega)$.

#### Raviart-Thomas Elements for $H(\mathrm{div})$

Analogously, to build an $H(\mathrm{div})$-conforming space, we need to enforce normal continuity. Raviart-Thomas elements accomplish this by associating degrees of freedom with mesh **faces** (in $\mathbb{R}^3$) or **edges** (in $\mathbb{R}^2$).

For a tetrahedral mesh in $\mathbb{R}^3$, the DoFs for the lowest-order Raviart-Thomas space are the fluxes across each of the four faces. For each face $f$, a DoF is defined as:
$$
\text{DoF}_f(\boldsymbol{v}) = \int_f \boldsymbol{v} \cdot \boldsymbol{n} \, dS
$$
where $\boldsymbol{n}$ is a [unit normal vector](@entry_id:178851) to the face [@problem_id:3329984]. When assembling the global system, two adjacent tetrahedra share a face. By associating a single DoF with this shared face, we enforce that the flux out of one element is equal to the flux into the other, guaranteeing continuity of the normal component and ensuring that the global space $RT_h \subset H(\mathrm{div};\Omega)$.

These choices contrast sharply with standard Lagrange elements for $H^1$ (which use nodal values at vertices to ensure function continuity) and discontinuous elements for $L^2$ (which use moments within the element cell and have no inter-[element continuity](@entry_id:165046) requirements). The specific association of DoFs with geometric entities—nodes for $H^1$, edges for $H(\mathrm{curl})$, faces for $H(\mathrm{div})$, and volumes for $L^2$—is the key mechanism for constructing a discrete, exact de Rham sequence.

### Local Shape Functions and Basis Construction

The abstract definition of degrees of freedom must be translated into concrete polynomial basis functions on a [reference element](@entry_id:168425), such as a reference triangle or tetrahedron.

The local [polynomial space](@entry_id:269905) for the Raviart-Thomas elements of order $k$ (denoted $\mathrm{RT}_k$) on a [simplex](@entry_id:270623) $K$ is typically defined as:
$$
\mathrm{RT}_k(K) = (\mathbb{P}_k(K))^d + \boldsymbol{x} \mathbb{P}_k(K)
$$
where $\mathbb{P}_k(K)$ is the space of scalar polynomials of total degree at most $k$, $(\mathbb{P}_k(K))^d$ is the space of vector polynomials with components in $\mathbb{P}_k(K)$, and $\boldsymbol{x}$ is the [position vector](@entry_id:168381). This choice of space ensures that for any $\boldsymbol{v} \in \mathrm{RT}_k(K)$, its divergence $\nabla \cdot \boldsymbol{v}$ is a polynomial in $\mathbb{P}_k(K)$ and its normal trace $\boldsymbol{v} \cdot \boldsymbol{n}$ on any face is a polynomial of degree $k$ in the face coordinates. The dimension of this space can be derived from this definition; for instance, in 2D, $\dim(\mathrm{RT}_k) = (k+1)(k+3)$ [@problem_id:3438155].

To make this tangible, consider the lowest-order Raviart-Thomas space $\mathrm{RT}_0$ on a reference triangle $\widehat{T}$ in 2D. The local space is spanned by vector fields of the form $\boldsymbol{v}(\boldsymbol{x}) = \boldsymbol{a} + b\boldsymbol{x}$ for a constant vector $\boldsymbol{a}$ and scalar $b$. There are three degrees of freedom, corresponding to the constant normal fluxes across the three edges. A basis function $\widehat{\boldsymbol{\phi}}_j$ is defined by the property that its flux across edge $\widehat{e}_i$ is 1 if $i=j$ and 0 otherwise (a Kronecker delta property). For a specific reference triangle, this leads to a system of linear equations for the coefficients of $\widehat{\boldsymbol{\phi}}_j$. Solving this system yields the explicit formula for the basis function, which can then be used in computations, for example to calculate its $L^2$-norm [@problem_id:3438157]. For the standard reference triangle with vertices $(0,0), (1,0), (0,1)$, the [basis function](@entry_id:170178) associated with the edge on the y-axis is $\widehat{\boldsymbol{\phi}}_3(\boldsymbol{x}) = (x-1, y)$.

It is important to note that the RT family is just one of several families of $H(\mathrm{div})$-[conforming elements](@entry_id:178102). Other families, such as the Brezzi–Douglas–Marini (BDM) and Brezzi–Douglas–Fortin–Marini (BDFM) elements, use different local [polynomial spaces](@entry_id:753582) (e.g., $\mathrm{BDM}_k(K) = (\mathbb{P}_k(K))^d$). This results in different properties, such as a different polynomial degree for the divergence, which in turn affects the choice of a stable pressure space in [mixed formulations](@entry_id:167436) (the [inf-sup condition](@entry_id:174538)) [@problem_id:3438139].

### Isoparametric Mappings and the Commuting Diagram

For the finite element method to be truly general, it must be applicable to domains with curved boundaries, which are approximated by meshes with [curved elements](@entry_id:748117). This is achieved via an **[isoparametric mapping](@entry_id:173239)**, a smooth transformation $F: \widehat{K} \to K$ from a simple reference element $\widehat{K}$ (like a cube or tetrahedron) to a physical element $K$ in the mesh. A crucial question arises: how should the vector-valued basis functions be transformed from $\widehat{K}$ to $K$?

A naive component-wise transformation is incorrect, as it fails to preserve the essential normal or tangential continuity properties. The correct transformations, known as **Piola transformations**, are derived from geometric principles to ensure the invariance of the degrees of freedom.

For an $H(\mathrm{div})$-conforming Raviart-Thomas element, the degrees of freedom are fluxes. The transformation must preserve the value of the [flux integral](@entry_id:138365). This leads to the **contravariant Piola transform**:
$$
\boldsymbol{v}(\boldsymbol{x}) = \frac{1}{\det(\mathbf{J})} \mathbf{J} \widehat{\boldsymbol{v}}(\widehat{\boldsymbol{x}}), \quad \text{where } \boldsymbol{x}=F(\widehat{\boldsymbol{x}})
$$
Here, $\mathbf{J}$ is the Jacobian of the mapping $F$. This specific form ensures that $\int_f \boldsymbol{v} \cdot \boldsymbol{n} \, dS = \int_{\widehat{f}} \widehat{\boldsymbol{v}} \cdot \widehat{\boldsymbol{n}} \, d\widehat{S}$ for any corresponding faces $f$ and $\widehat{f}$ [@problem_id:3438186].

For an $H(\mathrm{curl})$-conforming Nédélec element, the degrees of freedom are [line integrals](@entry_id:141417) (circulations). The transformation must preserve these integrals. This is achieved by the **covariant Piola transform**:
$$
\boldsymbol{w}(\boldsymbol{x}) = (\mathbf{J}^{-1})^T \widehat{\boldsymbol{w}}(\widehat{\boldsymbol{x}})
$$
This form ensures that $\int_e \boldsymbol{w} \cdot \boldsymbol{t} \, ds = \int_{\widehat{e}} \widehat{\boldsymbol{w}} \cdot \widehat{\boldsymbol{t}} \, d\widehat{s}$ for any corresponding edges $e$ and $\widehat{e}$ [@problem_id:3438186].

These transformations are fundamental to extending compatible [finite element methods](@entry_id:749389) to general meshes. They also form a key part of the **[commuting diagram](@entry_id:261357) property**. This property ensures that the discrete operators and spaces are not just internally consistent ([exact sequence](@entry_id:149883)) but also good approximations of their continuous counterparts. It states that applying a differential operator after projecting onto the finite element space should be the same as projecting after applying the operator. For example, for the divergence:
$$
\nabla \cdot (\Pi_h^{div} \boldsymbol{v}) = \Pi_h^{L^2} (\nabla \cdot \boldsymbol{v})
$$
where $\Pi_h^{div}$ and $\Pi_h^{L^2}$ are the canonical [projection operators](@entry_id:154142) onto the discrete $H(\mathrm{div})$ and $L^2$ spaces, respectively [@problem_id:3438139] [@problem_id:3350344]. The Piola transforms are precisely the mappings required to make these diagrams commute on general elements, solidifying the link between the discrete and continuous de Rham complexes.

### Implementation Aspects: The Role of Orientation

When implementing these elements in a finite element code, a subtle but critical mechanical detail emerges: the handling of **orientation**. To define the DoFs globally, we assign a unique orientation to each edge (a direction) and each face (a normal) in the mesh. However, when we process a single element $K$, its local [vertex ordering](@entry_id:261753) induces its own local orientation for its edges and faces. This local orientation may or may not align with the predefined global one.

For example, for a Nédélec element, the global DoF is $\int_e \boldsymbol{v} \cdot \boldsymbol{t}_e \, ds$, where $\boldsymbol{t}_e$ is the globally chosen tangent. The local basis function on element $K$ is defined with respect to a local tangent $\boldsymbol{t}_{e,K}$. If $\boldsymbol{t}_{e,K} = - \boldsymbol{t}_e$, the locally computed contribution to the global system will have the wrong sign.

The mechanism to correct this is straightforward but essential: during the assembly process, for each edge (or face), the code must compare the local orientation to the global orientation. If they are opposite, the corresponding entry in the local element matrix must be multiplied by -1 before being added to the global matrix [@problem_id:3438136]. This simple sign flip is the mechanism that guarantees that the contributions from adjacent elements correctly enforce continuity rather than erroneously cancelling each other out. This ensures that the final assembled system is independent of the arbitrary local vertex numbering used in the mesh [data structure](@entry_id:634264), leading to a robust and correct implementation.