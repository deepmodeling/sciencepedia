## Introduction
In the field of [computational electromagnetics](@entry_id:269494), approximating continuous physical quantities is a central challenge. Sub-domain basis functions provide a foundational framework for this task, and among the most elementary of these are **pulse basis functions**. Valued for their simplicity and intuitive piecewise-constant nature, they serve as a crucial first step in discretizing complex integral equations that model electromagnetic phenomena.

However, this apparent simplicity belies significant mathematical and physical limitations. The direct application of pulse functions can lead to non-physical results and [numerical instability](@entry_id:137058), a critical knowledge gap for practitioners aiming to build robust and accurate simulation tools. Understanding not only *how* to use these functions but also *when* and *why* they fail is paramount for advanced modeling.

This article provides a comprehensive exploration of pulse basis functions. The **"Principles and Mechanisms"** chapter will dissect their mathematical definition, properties, and critical non-conforming nature, revealing their failure to conserve charge. The **"Applications and Interdisciplinary Connections"** chapter will demonstrate their practical utility in surface and volume [integral equations](@entry_id:138643), numerical analysis, multiphysics, and inverse problems. Finally, the **"Hands-On Practices"** section will offer guided exercises to translate theoretical knowledge into practical skill. We begin by examining the core principles that govern the behavior and implementation of these fundamental building blocks.

## Principles and Mechanisms

In the numerical solution of integral equations, a core task is the approximation of a continuous unknown function—such as a current or [polarization field](@entry_id:197617)—by a [finite set](@entry_id:152247) of basis functions. The choice of these functions is paramount, influencing the accuracy, stability, and computational cost of the entire simulation. Among the simplest and most intuitive choices are **sub-domain basis functions**, particularly **pulse basis functions**, which are piecewise-constant over a partition of the problem domain. While their simplicity is attractive, their mathematical properties reveal profound implications for their use in computational electromagnetics. This chapter will elucidate the fundamental principles of pulse basis functions, from their definition and mathematical properties to their practical application and inherent limitations.

### Definition and Fundamental Properties

Let us consider a domain of interest, $\Omega \subset \mathbb{R}^3$, which may be a volume or a surface. This domain is partitioned into a set of $N$ non-overlapping sub-domains, or elements, denoted by $\{D_i\}_{i=1}^N$. The union of these elements reconstructs the original domain, i.e., $\bigcup_{i=1}^N \overline{D_i} = \overline{\Omega}$.

The **scalar pulse basis function**, $p_i(\mathbf{r})$, associated with sub-domain $D_i$ is defined using the [characteristic function](@entry_id:141714) $\chi_{D_i}(\mathbf{r})$:
$$
p_i(\mathbf{r}) = \chi_{D_i}(\mathbf{r}) = \begin{cases} 1  \text{if } \mathbf{r} \in D_i \\ 0  \text{if } \mathbf{r} \notin D_i \end{cases}
$$
An unknown [scalar field](@entry_id:154310), say $\psi(\mathbf{r})$, can be approximated as a linear combination of these basis functions, creating a piecewise-constant representation:
$$
\psi(\mathbf{r}) \approx \psi_h(\mathbf{r}) = \sum_{i=1}^N c_i p_i(\mathbf{r})
$$
where $\{c_i\}$ are the unknown coefficients to be determined.

For [vector fields](@entry_id:161384), such as an electric field $\mathbf{E}(\mathbf{r})$ or a [current density](@entry_id:190690) $\mathbf{J}(\mathbf{r})$, the concept is extended naturally. A **vector pulse [basis function](@entry_id:170178)** is defined by multiplying a scalar pulse by a constant vector. In a Cartesian coordinate system, a complete [vector basis](@entry_id:191419) within sub-domain $D_i$ is formed by three mutually [orthogonal functions](@entry_id:160936):
$$
\boldsymbol{\phi}_{i,x}(\mathbf{r}) = p_i(\mathbf{r})\hat{\mathbf{x}}, \quad \boldsymbol{\phi}_{i,y}(\mathbf{r}) = p_i(\mathbf{r})\hat{\mathbf{y}}, \quad \boldsymbol{\phi}_{i,z}(\mathbf{r}) = p_i(\mathbf{r})\hat{\mathbf{z}}
$$
An unknown vector field is then approximated as:
$$
\mathbf{F}(\mathbf{r}) \approx \mathbf{F}_h(\mathbf{r}) = \sum_{i=1}^N \left( C_{i,x} \boldsymbol{\phi}_{i,x}(\mathbf{r}) + C_{i,y} \boldsymbol{\phi}_{i,y}(\mathbf{r}) + C_{i,z} \boldsymbol{\phi}_{i,z}(\mathbf{r}) \right)
$$
This construction creates an approximation that is a constant vector within each sub-domain $D_i$. [@problem_id:3351534]

#### Inner Products and Normalization

The properties of these basis functions are best understood within the framework of Hilbert spaces, typically the space of square-[integrable functions](@entry_id:191199), $L^2(\Omega)$. The standard $L^2$ inner product for scalar functions is $\langle f, g \rangle = \int_{\Omega} f(\mathbf{r}) g^*(\mathbf{r}) \, dV$, where $g^*$ denotes the complex conjugate of $g$. For real functions, this simplifies to $\int_{\Omega} f(\mathbf{r}) g(\mathbf{r}) \, dV$.

A defining characteristic of pulse bases on disjoint sub-domains is their inherent **orthogonality**. The inner product of two distinct scalar pulse basis functions $p_i$ and $p_j$ (for $i \neq j$) is:
$$
\langle p_i, p_j \rangle = \int_{\Omega} p_i(\mathbf{r}) p_j(\mathbf{r}) \, dV = \int_{\Omega} \chi_{D_i}(\mathbf{r}) \chi_{D_j}(\mathbf{r}) \, dV = \int_{D_i \cap D_j} 1 \, dV = 0
$$
since the sub-domains are disjoint. The inner product of a [basis function](@entry_id:170178) with itself is its squared norm:
$$
\langle p_i, p_i \rangle = \|p_i\|^2_{L^2} = \int_{D_i} 1^2 \, dV = |D_i|
$$
where $|D_i|$ is the measure (volume or area) of the sub-domain.

This orthogonality is extremely useful, as it simplifies the **Gram matrix** (or [mass matrix](@entry_id:177093)), whose entries are $G_{ij} = \langle p_i, p_j \rangle$. For unnormalized pulse bases, the Gram matrix is a [diagonal matrix](@entry_id:637782) with entries $G_{ii} = |D_i|$. [@problem_id:3351571]

It is often advantageous to normalize the basis functions. A general pulse [basis function](@entry_id:170178) can be written as $\phi_i(\mathbf{r}) = \alpha_i p_i(\mathbf{r})$, where $\alpha_i$ is a normalization constant. The choice of $\alpha_i$ has significant practical consequences. Consider two common choices:
1.  **Unnormalized Basis**: $\alpha_i = 1$. As shown, $\|\phi_i\|^2 = |D_i|$. If the mesh contains elements with widely varying sizes, the diagonal entries of the Gram matrix will span several orders of magnitude. This leads to a **poorly conditioned** matrix, which can cause numerical instability and degrade the accuracy of the solution.
2.  **Measure-Normalized Basis**: $\alpha_i = 1/\sqrt{|D_i|}$. With this choice, the norm of each [basis function](@entry_id:170178) becomes:
    $$
    \|\phi_i\|^2 = \left\langle \frac{p_i}{\sqrt{|D_i|}}, \frac{p_i}{\sqrt{|D_i|}} \right\rangle = \frac{1}{|D_i|} \langle p_i, p_i \rangle = \frac{|D_i|}{|D_i|} = 1
    $$
    Since the basis functions are already orthogonal and now have unit norm, they form an **orthonormal** set. The Gram matrix becomes the identity matrix, $G_{ij} = \delta_{ij}$, which is perfectly conditioned ($\kappa(G)=1$). This normalization is therefore highly recommended for numerical stability. [@problem_id:3351571]

### Regularity and Function Space Conformance

While simple and orthogonal, pulse basis functions possess limited mathematical smoothness. This lack of smoothness is their most critical theoretical failing when applied to problems derived from Maxwell's equations. To formalize this, we must classify them according to the Sobolev spaces relevant to electromagnetics.

-   **$L^2(\Omega)$**: The space of square-[integrable functions](@entry_id:191199). As shown above, $\|p_i\|_{L^2}^2 = |D_i|$, which is finite for any finite-sized element. Thus, pulse bases are elements of $L^2(\Omega)$ and are said to be **$L^2$-conforming**. [@problem_id:3351544]

-   **$H^1(\Omega)$**: The space of $L^2$ functions whose weak (distributional) gradient is also in $L^2$. A pulse function $p_i$ has a [jump discontinuity](@entry_id:139886) from 1 to 0 at its boundary $\partial D_i$. Its [weak gradient](@entry_id:756667) is not a function but a Dirac delta distribution supported on the surface $\partial D_i$. A distribution supported on a lower-dimensional manifold is not an $L^2$ function. Therefore, pulse functions are **not** in $H^1(\Omega)$.

-   **$H(\mathrm{curl}, \Omega)$**: The space of $L^2$ [vector fields](@entry_id:161384) whose weak curl is also in $L^2$. This space is natural for electric fields, as it corresponds to the requirement that $\nabla \times \mathbf{E}$ be square-integrable (related to finite magnetic flux). Membership in $H(\mathrm{curl})$ implies that the tangential component of the vector field is continuous across element interfaces. A vector pulse basis function is discontinuous across its boundary, so its tangential component necessarily jumps. The weak curl is a surface distribution on the element boundary, not an $L^2$ function. Therefore, vector pulse bases are **not** in $H(\mathrm{curl}, \Omega)$. [@problem_id:3351574] [@problem_id:3351496]

-   **$H(\mathrm{div}, \Omega)$**: The space of $L^2$ vector fields whose weak divergence is also in $L^2$. This space is natural for flux density fields ($\mathbf{D}, \mathbf{B}$), as it relates to finite charge or the absence of [magnetic monopoles](@entry_id:142817). Membership in $H(\mathrm{div})$ implies that the normal component of the vector field is continuous across element interfaces. Again, a vector pulse is discontinuous and violates this condition. Its weak divergence is a surface distribution. Therefore, vector pulse bases are **not** in $H(\mathrm{div}, \Omega)$. [@problem_id:3351574] [@problem_id:3351496]

In summary, pulse basis functions are **$L^2$-conforming but are non-conforming for $H^1$, $H(\mathrm{curl})$, and $H(\mathrm{div})$**. They are properly said to belong to "broken" Sobolev spaces, where differentiability is only considered within each element, but not across them. This non-conformity means they violate the continuity conditions inherent in Maxwell's equations. [@problem_id:3351544]

### Application to Integral Equations and the Problem of Charge Conservation

The use of [non-conforming basis](@entry_id:752548) functions is known as a "[variational crime](@entry_id:178318)" in finite element theory. While often acceptable for [integral equations](@entry_id:138643) due to the smoothing nature of the Green's function, it has a particularly pernicious consequence related to charge conservation.

Consider the surface continuity equation, which links [surface current density](@entry_id:274967) $\mathbf{J}_s$ to [surface charge density](@entry_id:272693) $\rho_s$:
$$
\nabla_s \cdot \mathbf{J}_s = -j\omega \rho_s
$$
This equation is a local statement of [charge conservation](@entry_id:151839). Now, suppose we approximate the surface current $\mathbf{J}_s$ with vector pulse basis functions on a triangular surface mesh. The approximate current is piecewise-constant.
Inside any triangle, the current is a constant vector, so its divergence is zero. This would seem to imply that the [charge density](@entry_id:144672) is zero everywhere. However, the current is discontinuous across the edges separating the triangles. The normal component of the current does not flow continuously from one element to the next.

This discontinuity gives rise to a **distributional surface divergence**. The divergence of the piecewise-constant current is actually a series of Dirac delta functions supported on the edges of the mesh. Via the [continuity equation](@entry_id:145242), this non-physical, singular divergence implies a **non-physical line charge** concentrated along the artificial boundaries of the mesh elements. [@problem_id:3351568]

This is a catastrophic failure of the model. A basis of piecewise-constant functions for the [charge density](@entry_id:144672), $\rho_s(\mathbf{r}) \approx \sum_i q_i p_i(\mathbf{r})$, can only represent charge that is constant over a triangle's area. It cannot represent the line charges produced by the divergence of the pulse-based current. There is a fundamental mismatch between the space containing $\nabla_s \cdot \mathbf{J}_s$ and the space used to represent $\rho_s$. The discrete system is therefore unable to satisfy charge conservation. [@problem_id:3351524]

The [standard solution](@entry_id:183092) to this problem is to abandon pulse bases for currents and instead use a **[divergence-conforming basis](@entry_id:748602)**, such as the **Rao-Wilton-Glisson (RWG) basis functions** (also known as rooftop functions). An RWG basis function is defined on a pair of adjacent triangles and is constructed to guarantee that the current component normal to the shared edge is continuous. This continuity ensures that the divergence of any current expanded in the RWG basis is a regular $L^2$ function (specifically, it is piecewise-constant). This makes it compatible with a piecewise-constant (pulse) basis for the [charge density](@entry_id:144672), forming a **compatible mixed basis** that correctly enforces charge conservation at the discrete level. [@problem_id:3351524] [@problem_id:3351496]

### Discretization Schemes and Convergence

When pulse bases are used in a Method of Moments (MoM) framework, the choice of testing functions is also critical. The two most common choices are Galerkin testing and collocation.

Let's consider the [self-interaction](@entry_id:201333) term in a [volume integral equation](@entry_id:756568), which involves integrating the Green's function over a sub-domain. The 3D Helmholtz Green's function has a $1/R$ singularity. This is a **weakly singular** kernel, meaning it is integrable over a 3D volume. Therefore, a Cauchy Principal Value is not required for these integrals. [@problem_id:3351512]

-   **Galerkin Testing**: The [test functions](@entry_id:166589) are chosen to be the same as the basis functions. The matrix self-term becomes a double [volume integral](@entry_id:265381), $Z_{ii} = \int_{D_i} \int_{D_i} G(\mathbf{r}, \mathbf{r}') \, dV' \, dV$. The resulting matrix is **symmetric** (for a symmetric kernel), and the value of $Z_{ii}$ depends only on the geometry of the element $D_i$.

-   **Collocation (Point-Matching)**: The integral equation is enforced only at a single point $\mathbf{r}_i^c$ within each element. The matrix self-term is a single integral, $Z_{ii} = \int_{D_i} G(\mathbf{r}_i^c, \mathbf{r}') \, dV'$. The resulting matrix is generally **non-symmetric**, and the value of $Z_{ii}$ depends on the arbitrary choice of the collocation point $\mathbf{r}_i^c$.

Galerkin's method is generally preferred for its stability and symmetry properties. [@problem_id:3351512]

Finally, we consider the **convergence rate** of the solution as the mesh size $h$ approaches zero. For a Galerkin method applied to a second-kind integral equation (which is common for VIEs), the error is governed by how well the basis functions can approximate the true solution. Standard [approximation theory](@entry_id:138536) for finite elements shows that for a solution with smoothness $\mathbf{P} \in H^s(\Omega)^3$, the $L^2$ error for piecewise-constant ($p=0$) basis functions behaves as:
$$
\|\mathbf{P} - \mathbf{P}_h\|_{L^2(\Omega)} = O(h^{\min(p+1, s)}) = O(h^{\min(1, s)})
$$
For problems with smooth geometries and material properties, the solution is typically at least in $H^1$, so $s \ge 1$. This means that pulse basis functions generally yield **first-order convergence** ($O(h)$) in the $L^2$ norm. The [weak singularity](@entry_id:756676) of the integral kernel does not degrade this asymptotic [rate of convergence](@entry_id:146534). [@problem_id:3351525] While convergent, this rate is often slower than that achieved by higher-order or conforming basis functions like RWG for relevant engineering quantities. [@problem_id:3351496] The underlying fidelity of any such method, however, relies on a well-constructed mesh of **shape-regular** elements and valid **parametrizations** from a reference element to ensure numerical integrals are uniformly accurate. [@problem_id:3351516]

In conclusion, pulse basis functions offer a simple entry point into the [discretization](@entry_id:145012) of [integral equations](@entry_id:138643). Their orthogonality and simple structure are appealing. However, their non-conforming nature leads to fundamental violations of physical principles like [charge conservation](@entry_id:151839), necessitating the use of more sophisticated, conforming basis functions for robust and accurate solutions in many electromagnetic applications.