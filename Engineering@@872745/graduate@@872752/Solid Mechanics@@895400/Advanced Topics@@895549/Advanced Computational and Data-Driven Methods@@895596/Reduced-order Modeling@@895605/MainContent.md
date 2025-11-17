## Introduction
In modern science and engineering, high-fidelity computational models provide unprecedented insight into complex physical phenomena. However, their immense computational cost often renders them impractical for many-query tasks such as design optimization, [uncertainty quantification](@entry_id:138597), and [real-time control](@entry_id:754131). This creates a critical need for methods that can generate fast, accurate, and reliable approximations of these [large-scale systems](@entry_id:166848). Reduced-order modeling (ROM) provides a powerful mathematical and computational framework to address this challenge by systematically extracting the dominant features of a system's behavior and embedding them within a model of drastically smaller size.

This article offers a comprehensive exploration of projection-based reduced-order modeling, guiding you from fundamental principles to advanced applications. It bridges the gap between the theoretical underpinnings of [model reduction](@entry_id:171175) and its practical implementation for solving real-world problems. Across the following chapters, you will gain a deep understanding of how to construct, deploy, and critically evaluate [reduced-order models](@entry_id:754172).

The journey begins in the "Principles and Mechanisms" chapter, where we will dissect the core machinery of ROM, including the foundational principle of projection, the data-driven basis construction technique of Proper Orthogonal Decomposition (POD), and crucial methods like [hyper-reduction](@entry_id:163369) for overcoming computational bottlenecks in nonlinear systems. Next, the "Applications and Interdisciplinary Connections" chapter will broaden our perspective, showcasing how ROM is not only an enabling technology in [solid mechanics](@entry_id:164042) and [structural dynamics](@entry_id:172684) but also shares deep connections with systems and control theory and serves as a general-purpose tool for pattern extraction in data science. Finally, the "Hands-On Practices" chapter will challenge you to apply these concepts, tackling key issues such as energy-[optimal basis](@entry_id:752971) generation, the potential for [model instability](@entry_id:141491), and the implementation of [hyper-reduction](@entry_id:163369). We will start by examining the fundamental principle of projection, which forms the heart of most model reduction strategies.

## Principles and Mechanisms

This chapter delineates the foundational principles and core mechanisms that underpin the field of reduced-order modeling. We will move from the fundamental concept of projection, which lies at the heart of many model reduction techniques, to the practical methods for constructing effective low-dimensional spaces. Subsequently, we will address the critical computational challenges posed by nonlinearities and parametric dependencies, and explore the advanced techniques developed to overcome them.

### The Principle of Projection: Reducing the Governing Equations

The central premise of projection-based [model order reduction](@entry_id:167302) is to constrain the dynamics of a high-dimensional system to a low-dimensional subspace. Consider a general semi-discrete system of equations arising from the [finite element analysis](@entry_id:138109) of a continuum mechanics problem, which can be written in the form:
$$
\boldsymbol{M} \ddot{\boldsymbol{u}}(t) + \boldsymbol{C} \dot{\boldsymbol{u}}(t) + \boldsymbol{K} \boldsymbol{u}(t) = \boldsymbol{f}(t)
$$
Here, $\boldsymbol{u}(t) \in \mathbb{R}^{n}$ is the vector of nodal degrees of freedom (e.g., displacements), where $n$ can be very large. $\boldsymbol{M}$, $\boldsymbol{C}$, and $\boldsymbol{K}$ are the $n \times n$ mass, damping, and stiffness matrices, respectively, and $\boldsymbol{f}(t)$ is the external force vector.

The core of the reduction strategy is to posit an approximation, or **ansatz**, that the state vector $\boldsymbol{u}(t)$ can be well-represented as a linear combination of a small number of pre-selected basis vectors. These basis vectors, $\boldsymbol{v}_1, \dots, \boldsymbol{v}_r$ with $r \ll n$, form the columns of a [basis matrix](@entry_id:637164) $\boldsymbol{V} \in \mathbb{R}^{n \times r}$. The approximation is thus:
$$
\boldsymbol{u}(t) \approx \boldsymbol{V} \boldsymbol{q}(t)
$$
where $\boldsymbol{q}(t) \in \mathbb{R}^{r}$ is the vector of time-dependent generalized or reduced coordinates. The task now shifts from solving for the $n$ components of $\boldsymbol{u}(t)$ to solving for the $r$ components of $\boldsymbol{q}(t)$.

To derive the governing equations for $\boldsymbol{q}(t)$, we substitute the [ansatz](@entry_id:184384) into the original system. This substitution will not, in general, satisfy the equation exactly, leaving a **residual** vector $\boldsymbol{R}(t) \in \mathbb{R}^{n}$:
$$
\boldsymbol{R}(t) = \boldsymbol{M}(\boldsymbol{V}\ddot{\boldsymbol{q}}) + \boldsymbol{C}(\boldsymbol{V}\dot{\boldsymbol{q}}) + \boldsymbol{K}(\boldsymbol{V}\boldsymbol{q}) - \boldsymbol{f}(t) \neq \boldsymbol{0}
$$
The principle of projection provides a systematic way to determine the evolution of $\boldsymbol{q}(t)$ by enforcing a condition of optimality on this residual. We demand that the residual be **orthogonal** to a chosen **test subspace**, typically of the same dimension $r$ as the trial subspace. Let this test subspace be spanned by the columns of a matrix $\boldsymbol{W} \in \mathbb{R}^{n \times r}$. The [orthogonality condition](@entry_id:168905), with respect to the standard Euclidean inner product, is expressed as $\boldsymbol{W}^T \boldsymbol{R}(t) = \boldsymbol{0}$.

#### Galerkin Projection

The most common and intuitive choice is to set the test subspace to be identical to the trial subspace, i.e., $\boldsymbol{W} = \boldsymbol{V}$. This is known as a **(Bubnov-)Galerkin projection**. Applying this condition, $\boldsymbol{V}^T \boldsymbol{R}(t) = \boldsymbol{0}$, to the residual yields:
$$
\boldsymbol{V}^T (\boldsymbol{M}\boldsymbol{V}\ddot{\boldsymbol{q}} + \boldsymbol{C}\boldsymbol{V}\dot{\boldsymbol{q}} + \boldsymbol{K}\boldsymbol{V}\boldsymbol{q} - \boldsymbol{f}) = \boldsymbol{0}
$$
By linearity, we arrive at the [reduced-order model](@entry_id:634428) (ROM):
$$
\boldsymbol{M}_r \ddot{\boldsymbol{q}}(t) + \boldsymbol{C}_r \dot{\boldsymbol{q}}(t) + \boldsymbol{K}_r \boldsymbol{q}(t) = \boldsymbol{f}_r(t)
$$
where the reduced operators are defined by the projection [@problem_id:2679849]:
$$
\boldsymbol{M}_r = \boldsymbol{V}^T \boldsymbol{M} \boldsymbol{V}, \quad \boldsymbol{C}_r = \boldsymbol{V}^T \boldsymbol{C} \boldsymbol{V}, \quad \boldsymbol{K}_r = \boldsymbol{V}^T \boldsymbol{K} \boldsymbol{V}, \quad \boldsymbol{f}_r(t) = \boldsymbol{V}^T \boldsymbol{f}(t)
$$
This is a system of $r$ second-order [ordinary differential equations](@entry_id:147024), which is computationally far cheaper to solve than the original system of size $n$.

A crucial feature of Galerkin projection is its structure-preserving nature for certain operators. If the full-order matrices $\boldsymbol{M}$ and $\boldsymbol{K}$ are symmetric and [positive definite](@entry_id:149459) (SPD), as is typical for [mass and stiffness matrices](@entry_id:751703) in structural mechanics, and the [basis matrix](@entry_id:637164) $\boldsymbol{V}$ has full column rank, then the reduced matrices $\boldsymbol{M}_r$ and $\boldsymbol{K}_r$ are also guaranteed to be symmetric and positive definite. This is because they are formed by a congruent transformation, which preserves these properties. This ensures that the resulting ROM is well-behaved and retains the physical characteristics of the original system, such as positive definite energy norms [@problem_id:2679849].

#### Petrov-Galerkin Projection

The Galerkin framework can be generalized by allowing the test subspace to differ from the trial subspace, i.e., $\boldsymbol{W} \neq \boldsymbol{V}$. This approach is known as a **Petrov-Galerkin projection**. The resulting reduced equations have a similar structure, but with asymmetric projections [@problem_id:2679836]:
$$
(\boldsymbol{W}^T \boldsymbol{M} \boldsymbol{V}) \ddot{\boldsymbol{q}} + (\boldsymbol{W}^T \boldsymbol{C} \boldsymbol{V}) \dot{\boldsymbol{q}} + (\boldsymbol{W}^T \boldsymbol{K} \boldsymbol{V}) \boldsymbol{q} = \boldsymbol{W}^T \boldsymbol{f}
$$
A primary motivation for employing a Petrov-Galerkin method is to ensure the **stability** of the ROM, especially when dealing with systems governed by [non-normal operators](@entry_id:752588). Non-normal operators, which do not commute with their adjoint (transpose), arise frequently in fluid dynamics ([convection-dominated flows](@entry_id:169432)) or [structural mechanics](@entry_id:276699) with [non-conservative forces](@entry_id:164833). For such systems, a standard Galerkin projection ($\boldsymbol{W}=\boldsymbol{V}$) can yield a reduced model that is unstable, even when the original [full-order model](@entry_id:171001) is stable. By carefully selecting a different test basis $\boldsymbol{W}$, it is possible to enforce stability in the reduced system. For instance, an optimal choice for stability involves choosing $\boldsymbol{W}$ to approximate the dominant left eigenvectors (or [adjoint modes](@entry_id:746298)) of the system operator, leading to a bi-[orthogonal projection](@entry_id:144168) that can diagonalize the reduced system and guarantee stability [@problem_id:2679836].

Furthermore, specific choices of $\boldsymbol{W}$ can endow the projection with desirable properties. For a steady-state problem $\boldsymbol{A}\boldsymbol{u}=\boldsymbol{b}$, for instance, choosing the test basis as $\boldsymbol{W} = \boldsymbol{A}\boldsymbol{V}$ results in a method that minimizes the Euclidean norm of the residual, $\|\boldsymbol{A}\boldsymbol{V}\boldsymbol{q} - \boldsymbol{b}\|_2$. This is known as a least-squares Petrov-Galerkin method [@problem_id:2679836].

### Constructing the Reduction Basis: From Theory to Practice

The effectiveness of a projection-based ROM hinges entirely on the quality of the trial basis $\boldsymbol{V}$. A "good" basis is one that can accurately represent the system's behavior with a very small number of vectors, $r$.

#### Theoretical Underpinnings: The Notion of Approximability

Before constructing a basis, it is useful to ask a more fundamental question: how "reducible" is a given physical problem? The set of all possible solutions to a problem, for instance as a parameter $\boldsymbol{\mu}$ varies, forms a set in the high-dimensional state space known as the **solution manifold**, $\mathcal{M} = \{ \boldsymbol{u}(\boldsymbol{\mu}) \mid \boldsymbol{\mu} \in \mathcal{P} \}$. The theoretical limit on the accuracy of any linear subspace approximation is quantified by the **Kolmogorov $n$-width**, defined as:
$$
d_n(\mathcal{M}) := \inf_{\substack{Y \subset \mathbb{R}^n \\ \dim Y = n}} \; \sup_{\boldsymbol{u} \in \mathcal{M}} \; \inf_{\boldsymbol{y} \in Y} \; \|\boldsymbol{u} - \boldsymbol{y}\|
$$
In essence, $d_n(\mathcal{M})$ measures the [worst-case error](@entry_id:169595) for the best possible $n$-dimensional linear subspace. For reduced-order modeling to be effective, the $n$-width of the solution manifold must decay rapidly as $n$ increases.

The rate of decay is intimately linked to the properties of the underlying governing equations. It is a key theoretical result that if the solution manifold is the image of a compact parameter set under an analytic map, its $n$-width decays exponentially. This occurs in problems where the governing operators depend analytically on the parameters, such as in linear elasticity with parameters defining the Lamé constants [@problem_id:2679864]. Conversely, problems whose solutions are dominated by the transport of localized features (e.g., traveling wave fronts or [shock waves](@entry_id:142404)) often exhibit very slow, algebraic decay of their $n$-width. In such cases, any basis of global functions is inefficient, as many basis vectors are needed to represent the feature at all its possible locations. This indicates that standard linear subspace ROMs may perform poorly for these problems [@problem_id:2679864].

#### Data-Driven Basis Generation: Proper Orthogonal Decomposition (POD)

The most prominent and powerful method for constructing a problem-specific, data-driven basis is **Proper Orthogonal Decomposition (POD)**, also known as Principal Component Analysis (PCA) in other fields. The procedure begins by collecting data in the form of solution "snapshots," which are state vectors $\boldsymbol{u}(t_k)$ computed from a [high-fidelity simulation](@entry_id:750285) at different points in time or for different parameter values. These snapshots are arranged as columns of a snapshot matrix $\boldsymbol{X} = [\boldsymbol{u}_1, \boldsymbol{u}_2, \dots, \boldsymbol{u}_m] \in \mathbb{R}^{n \times m}$.

POD seeks the $r$-dimensional [orthonormal basis](@entry_id:147779) that is optimal in the sense that it minimizes the average squared Euclidean error between the snapshots and their projections onto the basis. This is equivalent to finding the basis that maximizes the average projected "energy" of the snapshots [@problem_id:2679843]. This optimization problem leads to a profound result from linear algebra: the [optimal basis](@entry_id:752971) vectors are the leading $r$ [left singular vectors](@entry_id:751233) of the snapshot matrix $\boldsymbol{X}$.

Let the Singular Value Decomposition (SVD) of the snapshot matrix be $\boldsymbol{X} = \boldsymbol{U}\boldsymbol{\Sigma}\boldsymbol{V}^T$. The columns of $\boldsymbol{U}$ are the [left singular vectors](@entry_id:751233) (the POD modes), and the diagonal entries of $\boldsymbol{\Sigma}$ are the singular values, $\sigma_i$. The total "energy" of the snapshot set, measured by the squared Frobenius norm, is equal to the sum of the squared singular values: $\|\boldsymbol{X}\|_F^2 = \sum_i \sigma_i^2$. The amount of energy captured by the $i$-th POD mode is $\sigma_i^2$. This provides a rigorous and quantitative criterion for truncating the basis: one retains the first $r$ modes that capture a desired fraction (e.g., 0.9999) of the total energy [@problem_id:2679843].

The standard POD formulation is optimal for the Euclidean norm. If one wishes to optimally represent a different physical quantity, such as kinetic energy ($\frac{1}{2}\boldsymbol{u}^T\boldsymbol{M}\boldsymbol{u}$) or [strain energy](@entry_id:162699) ($\frac{1}{2}\boldsymbol{u}^T\boldsymbol{K}\boldsymbol{u}$), a [weighted inner product](@entry_id:163877) must be used. This is achieved by transforming the snapshot data prior to performing the SVD. For instance, to find a basis optimal for kinetic energy, one would perform POD on the transformed snapshot matrix $\boldsymbol{M}^{1/2}\boldsymbol{X}$, where $\boldsymbol{M}^{1/2}$ is a [matrix square root](@entry_id:158930) of the mass matrix. The resulting POD modes are then mapped back to the original space [@problem_id:2679843].

#### A Comparison: POD versus Linear Modal Analysis

In structural engineering, a traditional approach to [model reduction](@entry_id:171175) is **linear [modal analysis](@entry_id:163921)**. The basis is chosen to be the first few eigenvectors ([normal modes](@entry_id:139640)) of the linearized system at an equilibrium point. While these modes form a complete basis, their effectiveness is limited when dealing with strongly nonlinear systems.

For a geometrically nonlinear structure, the [internal forces](@entry_id:167605) contain quadratic and cubic terms in the displacements. When the system equations are projected onto the linear [modal basis](@entry_id:752055), these nonlinear terms create coupling between the modes. Even if a motion is initiated purely within a subspace of the first few modes, the [nonlinear dynamics](@entry_id:140844) will inevitably excite higher-frequency modes that were truncated from the model. This "energy spillover" means the linear modal subspace is not an [invariant subspace](@entry_id:137024) of the nonlinear flow. In strongly nonlinear regimes, this effect can be severe, leading to large errors and inaccurate predictions [@problem_id:2679802]. This is especially true in the presence of phenomena like [internal resonance](@entry_id:750753) (e.g., a $2:1$ resonance between two modes), where nonlinear coupling is the dominant physical mechanism; a model that truncates one of the participating modes cannot possibly capture the dynamics [@problem_id:2679802].

In contrast, a POD basis is fundamentally different. Because it is extracted from snapshots of the *actual nonlinear simulation*, it is inherently tailored to the solution manifold. The POD modes are not simple sinusoids; they are complex spatial shapes that implicitly contain the effects of [geometric nonlinearity](@entry_id:169896) and modal coupling at the energy level of the snapshots. For this reason, a POD basis of a given size $r$ is almost always far more accurate and efficient than a linear [modal basis](@entry_id:752055) of the same size for representing strongly [nonlinear dynamics](@entry_id:140844) [@problem_id:2679802].

### Overcoming Computational Bottlenecks

Simply generating a good basis and projecting the governing equations is often not sufficient to achieve the desired computational [speedup](@entry_id:636881), particularly for nonlinear and parametric problems.

#### The Nonlinearity Challenge

When we apply a Galerkin projection to a system with a nonlinear internal force term $\boldsymbol{f}_{\text{int}}(\boldsymbol{u})$, the resulting reduced equation contains the term $\boldsymbol{V}^T \boldsymbol{f}_{\text{int}}(\boldsymbol{V}\boldsymbol{q})$. At each time step of a simulation, evaluating this term presents a major computational bottleneck. The standard ("naive") procedure is:
1. Reconstruct the full-dimensional [state vector](@entry_id:154607) from the reduced coordinates: $\boldsymbol{u} = \boldsymbol{V}\boldsymbol{q}$. This is a matrix-vector product of size $(n \times r) \times (r \times 1)$, with a cost that scales with $n$.
2. Evaluate the nonlinear force function on this full vector: $\boldsymbol{f}_{\text{int}}(\boldsymbol{u})$. The cost of this step depends on the complexity of the nonlinearity but crucially depends on the full dimension $n$ (e.g., it may involve a loop over all elements or nodes in the mesh).
3. Project the resulting force vector back down to the reduced space: $\boldsymbol{V}^T \boldsymbol{f}_{\text{int}}(\boldsymbol{u})$. This is another [matrix-vector product](@entry_id:151002) with a cost scaling with $n$.

Because the evaluation cost remains dependent on the large dimension $n$ of the [full-order model](@entry_id:171001), the goal of creating a truly low-cost ROM has not been achieved. The ROM's state is small, but its evaluation is still large [@problem_id:2679796] [@problem_id:2679802].

#### Hyper-reduction: Decoupling from the Full Model Mesh

To break this dependence on $n$, a second level of approximation is required, collectively known as **[hyper-reduction](@entry_id:163369)**. The goal of [hyper-reduction](@entry_id:163369) is to approximate the nonlinear function evaluation itself.

In a finite element context, where [internal forces](@entry_id:167605) are computed by integrating stresses over the domain via [numerical quadrature](@entry_id:136578), the full computation involves summing contributions from a large number of quadrature points, $M$. The cost is proportional to $M$, and $M$ typically scales with $n$. Hyper-reduction methods approximate this sum by using only a very small subset of $s$ carefully selected quadrature points ($s \ll M$). The resulting computational speedup is directly proportional to the ratio $M/s$, which can be substantial [@problem_id:2679797].

The **Discrete Empirical Interpolation Method (DEIM)** is a widely used and rigorous [hyper-reduction](@entry_id:163369) technique. Instead of approximating the state $\boldsymbol{u}$, DEIM approximates the nonlinear function vector $\boldsymbol{g}(\boldsymbol{u}) = \boldsymbol{f}_{\text{int}}(\boldsymbol{u})$ directly. It constructs a separate basis, $\boldsymbol{U} \in \mathbb{R}^{n \times m}$, for the nonlinear term (typically via POD on snapshots of $\boldsymbol{g}(\boldsymbol{u})$). It then seeks an approximation of the form $\boldsymbol{g}(\boldsymbol{u}) \approx \boldsymbol{U}\boldsymbol{c}$. The key insight of DEIM is to determine the coefficient vector $\boldsymbol{c}$ not by a full projection, but by enforcing that the approximation exactly interpolates the true function $\boldsymbol{g}(\boldsymbol{u})$ at a small set of $m$ judiciously chosen component indices. These indices are encoded in a sampling matrix $\boldsymbol{P}$. This leads to the DEIM approximation [@problem_id:2679793]:
$$
\tilde{\boldsymbol{g}}(\boldsymbol{u}) = \boldsymbol{U} (\boldsymbol{P}^T \boldsymbol{U})^{-1} \boldsymbol{P}^T \boldsymbol{g}(\boldsymbol{u})
$$
The online evaluation of this term only requires evaluating the original function $\boldsymbol{g}(\boldsymbol{u})$ at the $m$ sampled indices, not the full vector. This makes the computational cost of evaluating the reduced nonlinear term independent of $n$ and dependent only on the small dimensions $r$ and $m$.

#### The Parametric Challenge and the Reduced Basis Method (RBM)

Many engineering analyses involve understanding system behavior as a function of certain parameters $\boldsymbol{\mu}$ (e.g., material properties, boundary conditions, geometric features). The goal is to build a ROM that is valid and fast to evaluate for *any* value of $\boldsymbol{\mu}$ within a given range. This is the domain of the **Reduced Basis Method (RBM)**.

While the core of RBM is still a Galerkin projection onto a basis of snapshots (now taken at different parameter values), it faces a similar online evaluation bottleneck. For a new parameter $\boldsymbol{\mu}$, the reduced matrices $\boldsymbol{A}_N(\boldsymbol{\mu}) = \boldsymbol{V}^T \boldsymbol{A}(\boldsymbol{\mu}) \boldsymbol{V}$ depend on $\boldsymbol{\mu}$. Assembling the full matrix $\boldsymbol{A}(\boldsymbol{\mu})$ and projecting it for every new query would be prohibitively slow.

RBM overcomes this through an **offline-online computational decomposition**. This strategy is enabled by assuming (or enforcing) that the parameter-dependent operators have an **affine parameter dependence**. This means the operator can be written as a short [linear combination](@entry_id:155091) of parameter-independent operators, multiplied by scalar functions of the parameter [@problem_id:2679819]:
$$
a(w, v ; \boldsymbol{\mu}) = \sum_{q=1}^{Q_{a}} \Theta_{q}^{a}(\boldsymbol{\mu}) a_{q}(w, v)
$$
This affine structure allows the computations to be split:
*   **Offline Stage (expensive, one-time):** The basis $\boldsymbol{V}$ is constructed. Then, the small, parameter-independent reduced matrices corresponding to each term in the affine expansion are computed and stored: $(\boldsymbol{A}_{N,q})_{ij} = a_q(v_j, v_i)$. This stage is slow as it involves the [full-order model](@entry_id:171001).
*   **Online Stage (fast, for each query):** For a new parameter value $\boldsymbol{\mu}$, one simply evaluates the (cheap) scalar functions $\Theta_{q}^{a}(\boldsymbol{\mu})$ and assembles the final reduced matrix through a simple [linear combination](@entry_id:155091) of the pre-computed matrices: $\boldsymbol{A}_{N}(\boldsymbol{\mu}) = \sum_{q=1}^{Q_{a}} \Theta_{q}^{a}(\boldsymbol{\mu}) \boldsymbol{A}_{N,q}$.

This procedure yields a parametric ROM whose online evaluation cost is completely independent of the original high-fidelity model dimension $N_h$, enabling rapid exploration of the parameter space.

### The Broader Landscape: Intrusive versus Non-Intrusive Modeling

It is important to recognize that the projection-based techniques described thus far—Galerkin, POD-Galerkin, RBM, and DEIM—belong to a class of methods known as **intrusive models**. They are "intrusive" because their implementation requires explicit access to and manipulation of the discretized operators ($\boldsymbol{M}, \boldsymbol{C}, \boldsymbol{K}, \boldsymbol{f}_{\text{int}}$) of the [full-order model](@entry_id:171001). One needs to be able to form these matrices and vectors in order to project them [@problem_id:2679811].

An entirely different philosophy gives rise to **non-intrusive [reduced-order models](@entry_id:754172)**, often called **[surrogate models](@entry_id:145436)**. These methods treat the existing [high-fidelity simulation](@entry_id:750285) code as a "black box." The only interaction with the full model is to use it to generate a set of training data, consisting of input-output pairs (e.g., parameter values and their corresponding solutions, $(\boldsymbol{\mu}_i, \boldsymbol{u}_i)$).

The non-intrusive approach then uses techniques from machine learning, [function approximation](@entry_id:141329), and statistics to directly learn the input-to-output map, for instance, the parametric solution map $\mathcal{S}: \boldsymbol{\mu} \mapsto \boldsymbol{u}(\boldsymbol{\mu})$. Instead of approximating the governing equations, these methods approximate the *solution* to the governing equations. They do not involve the projection of a residual. Examples of non-intrusive techniques include those based on neural networks, Gaussian process regression, [polynomial chaos expansions](@entry_id:162793), and radial basis functions. The choice between intrusive and non-intrusive methods depends on factors such as access to the [full-order model](@entry_id:171001) source code, the need for physical interpretability and certification, and the complexity of the problem's solution manifold [@problem_id:2679811].