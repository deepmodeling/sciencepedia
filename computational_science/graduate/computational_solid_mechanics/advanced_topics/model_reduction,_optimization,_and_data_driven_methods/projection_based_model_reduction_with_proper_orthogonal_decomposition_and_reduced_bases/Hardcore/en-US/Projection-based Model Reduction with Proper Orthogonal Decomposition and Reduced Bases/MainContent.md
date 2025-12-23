## Introduction
High-fidelity simulations in [computational solid mechanics](@entry_id:169583), often based on the [finite element method](@entry_id:136884), provide unparalleled accuracy but come at a steep computational cost. This expense can render them impractical for many-query applications like design optimization, uncertainty quantification, and [real-time control](@entry_id:754131). A significant knowledge gap exists in how to bridge the divide between high-fidelity accuracy and real-time performance. Projection-based [model reduction](@entry_id:171175) offers a powerful solution by creating computationally inexpensive, yet physically faithful, [reduced-order models](@entry_id:754172) (ROMs) that serve as efficient surrogates for the full-order system. This article provides a graduate-level guide to the theory and application of these powerful methods.

The following chapters will guide you through this complex topic. First, **"Principles and Mechanisms"** delves into the mathematical foundations, explaining the Galerkin projection framework, the construction of an [optimal basis](@entry_id:752971) using Proper Orthogonal Decomposition (POD), and the offline-online strategy that enables dramatic computational speedups. Next, **"Applications and Interdisciplinary Connections"** explores the versatility of ROMs in solving practical engineering problems, from parametric design to simulating advanced nonlinear phenomena like plasticity and fracture, and highlights its connections to control theory and data science. Finally, **"Hands-On Practices"** presents a set of guided problems to translate theory into practice, tackling challenges in [hyperelasticity](@entry_id:168357), [error estimation](@entry_id:141578), and constrained multiphysics systems.

## Principles and Mechanisms

This chapter delves into the foundational principles and operative mechanisms of [projection-based model reduction](@entry_id:753807). We transition from the conceptual motivation provided in the introduction to a rigorous examination of how these [reduced-order models](@entry_id:754172) (ROMs) are constructed, what properties they possess, and how their computational efficiency is realized. Our primary focus will be on the widely used Proper Orthogonal Decomposition (POD) for basis construction, situated within a Galerkin projection framework. We will use linear [elastostatics](@entry_id:198298) and [elastodynamics](@entry_id:175818) as our principal examples to develop the core concepts, progressively extending them to address the challenges posed by nonlinearity.

### The Galerkin Projection Framework

The starting point for [projection-based model reduction](@entry_id:753807) is a high-fidelity model, typically a system of ordinary differential equations or algebraic equations resulting from a Finite Element (FE) discretization. For a static problem in linear elasticity, this system takes the form:

$
\mathbf{K}(\mu) \mathbf{u}(\mu) = \mathbf{f}(\mu)
$

Here, $\mathbf{u}(\mu) \in \mathbb{R}^n$ is the vector of nodal displacements for a given parameter $\mu$, $\mathbf{K}(\mu) \in \mathbb{R}^{n \times n}$ is the [symmetric positive definite](@entry_id:139466) (SPD) stiffness matrix, and $\mathbf{f}(\mu) \in \mathbb{R}^n$ is the nodal force vector. The dimension $n$ of this [full-order model](@entry_id:171001) (FOM) can be very large, making repeated solutions for different parameters $\mu$ computationally prohibitive.

The central idea of [projection-based model reduction](@entry_id:753807) is to seek an approximate solution that lies within a low-dimensional subspace of the full-order space $\mathbb{R}^n$. We postulate the existence of a **reduced basis**, represented by the columns of a matrix $\mathbf{V} \in \mathbb{R}^{n \times r}$ with $r \ll n$. The columns of $\mathbf{V}$ are linearly independent vectors, called modes or basis vectors, that span an $r$-dimensional trial subspace. The reduced-order approximation $\mathbf{u}_r(\mu)$ is then expressed as a linear combination of these basis vectors:

$
\mathbf{u}(\mu) \approx \mathbf{u}_r(\mu) = \mathbf{V} \mathbf{a}(\mu)
$

where $\mathbf{a}(\mu) \in \mathbb{R}^r$ is the vector of unknown reduced coordinates. By substituting this ansatz into the original governing equation, we obtain a residual $\mathbf{R}(\mu)$:

$
\mathbf{R}(\mu) = \mathbf{f}(\mu) - \mathbf{K}(\mu) \mathbf{V} \mathbf{a}(\mu)
$

Since $\mathbf{u}_r(\mu)$ is an approximation, the residual will not be zero in general. The **Galerkin projection** principle provides a systematic way to determine the "best" coefficients $\mathbf{a}(\mu)$. It enforces that the residual must be orthogonal to a chosen test subspace. In the standard Galerkin method, the test subspace is chosen to be the same as the trial subspace, i.e., the space spanned by the columns of $\mathbf{V}$. This [orthogonality condition](@entry_id:168905) is expressed as:

$
\mathbf{V}^{\top} \mathbf{R}(\mu) = \mathbf{0}
$

Substituting the expression for the residual yields:

$
\mathbf{V}^{\top} (\mathbf{f}(\mu) - \mathbf{K}(\mu) \mathbf{V} \mathbf{a}(\mu)) = \mathbf{0}
$

Rearranging this gives the **[reduced-order model](@entry_id:634428) (ROM)**, which is a small linear system of size $r \times r$:

$
\mathbf{K}_r(\mu) \mathbf{a}(\mu) = \mathbf{f}_r(\mu)
$

where:
$
\mathbf{K}_r(\mu) = \mathbf{V}^{\top} \mathbf{K}(\mu) \mathbf{V} \in \mathbb{R}^{r \times r} \quad (\text{Reduced Stiffness Matrix})
$
$
\mathbf{f}_r(\mu) = \mathbf{V}^{\top} \mathbf{f}(\mu) \in \mathbb{R}^r \quad (\text{Reduced Force Vector})
$

Once this small system is solved for $\mathbf{a}(\mu)$, the full-dimensional approximate solution is recovered through the reconstruction step $\mathbf{u}_r(\mu) = \mathbf{V} \mathbf{a}(\mu)$. The computational savings arise from the fact that solving an $r \times r$ system is vastly cheaper than solving the original $n \times n$ system. This framework, however, leaves two critical questions unanswered: how to handle boundary conditions, and how to construct a "good" reduced basis $\mathbf{V}$.

### Handling Non-Homogeneous Boundary Conditions

The simple derivation above implicitly assumes [homogeneous boundary conditions](@entry_id:750371) (e.g., zero prescribed displacements). In practice, non-homogeneous essential (Dirichlet) boundary conditions are common and require careful treatment. Let the discrete form of these conditions be expressed as $Q \mathbf{u} = \mathbf{g}$, where $Q$ is a selector matrix identifying the constrained degrees of freedom and $\mathbf{g}$ contains the prescribed values. Several strategies exist, but the **[lifting function method](@entry_id:751272)** is particularly effective and elegant as it preserves the desirable properties of the Galerkin system .

The method decomposes the solution $\mathbf{u}(\mu)$ into two parts:

$
\mathbf{u}(\mu) = \mathbf{w}(\mu) + \mathbf{u}_L(\mu)
$

Here, $\mathbf{u}_L(\mu)$ is a **[lifting function](@entry_id:175709)** (or lifting vector), which is any vector that satisfies the [non-homogeneous boundary conditions](@entry_id:166003), i.e., $Q \mathbf{u}_L(\mu) = \mathbf{g}(\mu)$. The remaining part of the solution, $\mathbf{w}(\mu)$, is the unknown homogeneous component, which must therefore satisfy [homogeneous boundary conditions](@entry_id:750371), $Q \mathbf{w}(\mu) = \mathbf{0}$.

The reduced basis $\mathbf{V}$ is now constructed to approximate only the homogeneous part of the solution space. This means every column of $\mathbf{V}$ must satisfy the homogeneous boundary condition, a property expressed algebraically as $Q \mathbf{V} = \mathbf{0}$. The [ansatz](@entry_id:184384) for the ROM becomes:

$
\mathbf{u}(\mu) \approx \mathbf{u}_r(\mu) = \mathbf{V} \mathbf{a}(\mu) + \mathbf{u}_L(\mu)
$

By construction, this approximation exactly satisfies the prescribed boundary conditions for any choice of reduced coordinates $\mathbf{a}(\mu)$, since $Q \mathbf{u}_r = Q(\mathbf{V}\mathbf{a}) + Q \mathbf{u}_L = \mathbf{0} + \mathbf{g}(\mu) = \mathbf{g}(\mu)$.

To derive the reduced system, we substitute this new [ansatz](@entry_id:184384) into the full-order governing equation, $\mathbf{K}(\mu) \mathbf{u}(\mu) = \mathbf{f}(\mu)$:

$
\mathbf{K}(\mu) (\mathbf{V} \mathbf{a}(\mu) + \mathbf{u}_L(\mu)) = \mathbf{f}(\mu)
$

The Galerkin projection again demands that the residual be orthogonal to the [test space](@entry_id:755876) spanned by $\mathbf{V}$:

$
\mathbf{V}^{\top} [\mathbf{f}(\mu) - \mathbf{K}(\mu)(\mathbf{V} \mathbf{a}(\mu) + \mathbf{u}_L(\mu))] = \mathbf{0}
$

Rearranging this equation yields the final form of the reduced system :

$
(\mathbf{V}^{\top} \mathbf{K}(\mu) \mathbf{V}) \mathbf{a}(\mu) = \mathbf{V}^{\top} (\mathbf{f}(\mu) - \mathbf{K}(\mu) \mathbf{u}_L(\mu))
$

Comparing this to the homogeneous case, we see that the non-homogeneous boundary condition introduces an additional term, $-\mathbf{V}^{\top} \mathbf{K}(\mu) \mathbf{u}_L(\mu)$, on the right-hand side. This term can be interpreted as the reduced forces induced by the prescribed boundary displacements. A crucial property of this formulation is that if the original [stiffness matrix](@entry_id:178659) $\mathbf{K}(\mu)$ is SPD on the space of homogeneous solutions, the reduced [stiffness matrix](@entry_id:178659) $\mathbf{K}_r(\mu) = \mathbf{V}^{\top} \mathbf{K}(\mu) \mathbf{V}$ remains SPD, thus guaranteeing that the reduced system is well-posed and has a unique solution .

It is vital to maintain consistency in this approach. A common pitfall is to naively combine a [lifting function](@entry_id:175709) with a reduced basis $\mathbf{V}$ whose columns do not satisfy the [homogeneous boundary conditions](@entry_id:750371) (i.e., $Q \mathbf{V} \neq \mathbf{0}$). In such a case, the [ansatz](@entry_id:184384) $\mathbf{u}_L + \mathbf{V} \mathbf{a}$ will generally violate the boundary conditions, as the term $(Q\mathbf{V})\mathbf{a}$ will be non-zero .

### Constructing the Reduced Basis: Proper Orthogonal Decomposition

With a robust projection framework established, we turn to the pivotal task of constructing an effective reduced basis $\mathbf{V}$. While many choices are possible (e.g., analytical functions, vibration modes), a powerful and versatile data-driven approach is **Proper Orthogonal Decomposition (POD)**, also known as Principal Component Analysis (PCA) in other fields. The philosophy of POD is to find a low-dimensional basis that optimally captures the characteristics of a pre-computed set of solutions to the FOM.

#### The POD Optimization Problem

The process begins by running the FOM for a representative set of training parameters $\{\mu_i\}_{i=1}^m$ to generate a collection of high-fidelity solutions, or **snapshots**, $\{\mathbf{u}(\mu_i)\}_{i=1}^m$. These are typically arranged as columns of a snapshot matrix $\mathbf{S} \in \mathbb{R}^{n \times m}$. For problems involving non-homogeneous BCs, these snapshots should be of the homogeneous solution component, $\mathbf{w}(\mu_i)$.

POD seeks an orthonormal basis $\mathbf{V}$ of size $r$ that minimizes the average squared error of projecting the snapshots onto the subspace spanned by $\mathbf{V}$. This error is measured in a norm induced by a chosen [symmetric positive definite](@entry_id:139466) weighting matrix $\mathbf{W}$. The POD problem is formally stated as:

$
\min_{\mathbf{V} \in \mathbb{R}^{n \times r}, \mathbf{V}^{\top}\mathbf{W}\mathbf{V}=\mathbf{I}_r} \frac{1}{m} \sum_{i=1}^{m} \|\mathbf{u}(\mu_i) - \mathbf{V}\mathbf{V}^{\top}\mathbf{W}\mathbf{u}(\mu_i)\|_{\mathbf{W}}^2
$

where $\|\mathbf{x}\|_{\mathbf{W}} = \sqrt{\mathbf{x}^{\top}\mathbf{W}\mathbf{x}}$ is the $\mathbf{W}$-[induced norm](@entry_id:148919). The choice of $\mathbf{W}$ is a critical modeling decision, as it defines the quantity in which the error is being minimized. For mechanical systems, physically meaningful choices are often preferred over the standard Euclidean inner product ($\mathbf{W} = \mathbf{I}$) :

*   **Kinetic Energy Norm:** By choosing $\mathbf{W} = \mathbf{M}$, the [mass matrix](@entry_id:177093), and using velocity snapshots, POD finds a basis that minimizes the error in representing the kinetic energy of the system. The kinetic energy of a state with velocity $\dot{\mathbf{u}}$ is $T = \frac{1}{2}\dot{\mathbf{u}}^{\top}\mathbf{M}\dot{\mathbf{u}} = \frac{1}{2}\|\dot{\mathbf{u}}\|_{\mathbf{M}}^2$.
*   **Strain Energy Norm:** By choosing $\mathbf{W} = \mathbf{K}_0$, a reference stiffness matrix (e.g., for a mean parameter value $\mu_0$), and using displacement snapshots, POD minimizes the error in representing the [strain energy](@entry_id:162699). The [strain energy](@entry_id:162699) is $U = \frac{1}{2}\mathbf{u}^{\top}\mathbf{K}_0\mathbf{u} = \frac{1}{2}\|\mathbf{u}\|_{\mathbf{K}_0}^2$. This choice is often highly effective for structural problems as it prioritizes capturing the modes that store the most elastic energy.

When working with problems constrained by pure Neumann boundary conditions, the [stiffness matrix](@entry_id:178659) $\mathbf{K}$ is singular due to rigid-body motions. In this case, $\mathbf{K}$ is not [positive definite](@entry_id:149459) and cannot be used as a weighting matrix. Any energy-norm based procedure must first be restricted to the subspace of elastic deformations, orthogonal to the rigid-body modes .

#### The Method of Snapshots

Solving the POD optimization problem directly via an $n \times n$ [eigenvalue problem](@entry_id:143898) is computationally infeasible for large $n$. The **[method of snapshots](@entry_id:168045)** provides an efficient alternative when the number of snapshots $m$ is much smaller than the dimension $n$. This method relies on the fact that the [optimal basis](@entry_id:752971) vectors must lie in the span of the snapshots themselves.

The procedure to compute a $\mathbf{W}$-orthonormal POD basis is as follows :
1.  Assemble the snapshot matrix $\mathbf{S} \in \mathbb{R}^{n \times m}$ from the training data.
2.  Form the small $m \times m$ [correlation matrix](@entry_id:262631) $\mathbf{C} = \mathbf{S}^{\top} \mathbf{W} \mathbf{S}$. This matrix is symmetric and positive semidefinite.
3.  Solve the eigenvalue problem for the correlation matrix: $\mathbf{C} \mathbf{A} = \mathbf{A} \mathbf{\Lambda}$, where $\mathbf{\Lambda}$ is a [diagonal matrix](@entry_id:637782) of eigenvalues $\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_m \ge 0$ and the columns of $\mathbf{A}$ are the corresponding orthonormal eigenvectors. The magnitude of each eigenvalue $\lambda_i$ represents the "energy" (in the $\mathbf{W}$-norm) captured by the corresponding mode.
4.  Select the first $r$ eigenvectors corresponding to the largest $r$ eigenvalues. Let this be $\mathbf{A}_r \in \mathbb{R}^{m \times r}$ and the corresponding eigenvalue matrix be $\mathbf{\Lambda}_r \in \mathbb{R}^{r \times r}$.
5.  Construct the final reduced [basis matrix](@entry_id:637164) $\mathbf{V} \in \mathbb{R}^{n \times r}$ via the transformation:

    $
    \mathbf{V} = \mathbf{S} \mathbf{A}_r \mathbf{\Lambda}_r^{-1/2}
    $

The resulting basis vectors in $\mathbf{V}$ are guaranteed to be orthonormal with respect to the $\mathbf{W}$ inner product, i.e., $\mathbf{V}^{\top}\mathbf{W}\mathbf{V} = \mathbf{I}_r$.

### Properties and Interpretations of Reduced Models

Having established how to construct a ROM, we now consider its properties and what it truly represents.

#### Optimality, Certification, and Comparison to Other Methods

By its very definition, a POD basis is optimal in an average sense for representing the specific data it was trained on. This means that for a given basis size $r$, no other linear basis can represent the snapshot set with a smaller [mean-squared error](@entry_id:175403). A practical consequence is that a POD basis is generally far more efficient at representing a particular system's behavior than a generic, problem-independent basis. For instance, in [elastodynamics](@entry_id:175818), a one-dimensional POD basis derived from solution snapshots will typically capture more energy from that specific dataset than the lowest-frequency linear vibration mode, unless the dynamics are perfectly described by that single mode .

However, this optimality is limited. POD is a "black box" method that knows nothing about the governing equations or the parameter space. Its quality is entirely dependent on the training snapshots. If the [training set](@entry_id:636396) fails to capture some important behavior of the system, the resulting ROM will perform poorly for parameters that excite that behavior. POD provides no rigorous guarantee on the ROM's accuracy for a new, unseen parameter $\mu$.

This limitation motivates an alternative strategy known as the **Greedy Reduced Basis Method (RBM)**. Instead of starting with a fixed set of snapshots, a greedy algorithm iteratively builds the basis. At each step, it searches the parameter domain for the parameter $\mu^*$ that yields the largest error for the current ROM. This search is guided by a computationally cheap *a posteriori* [error estimator](@entry_id:749080). The snapshot corresponding to $\mu^*$ is then added to the basis, and the process repeats. This procedure is designed to systematically reduce the [worst-case error](@entry_id:169595) across the entire parameter domain  .

The theoretical benchmark for the best possible accuracy of any $r$-dimensional [linear approximation](@entry_id:146101) is the **Kolmogorov $r$-width** of the solution manifold. It has been proven that under certain conditions—most critically, the availability of a reliable [error estimator](@entry_id:749080)—the [greedy algorithm](@entry_id:263215) achieves a near-optimal convergence rate that tracks the Kolmogorov $r$-width. POD does not offer such a strong [worst-case error](@entry_id:169595) guarantee. The success of the greedy approach hinges on the reliability of the error surrogate; if the surrogate fails to accurately identify the location of maximum error, the algorithm's optimality is lost .

#### Interpretation as Approximations to Invariant Manifolds

A deeper interpretation of a projection-based ROM comes from the theory of dynamical systems. The full-order dynamical system evolves in an $n$-dimensional (or $2n$-dimensional phase) space. A ROM constrains the dynamics to an $r$-dimensional affine subspace (a "flat manifold") defined by $\mathbf{u} = \mathbf{u}_L + \mathbf{V}\mathbf{a}$.

A true **invariant manifold** is a subspace of the state space with the property that any trajectory starting on the manifold remains on it for all time. This requires that at every point on the manifold, the vector field of the true dynamics must be tangent to the manifold. For our mechanical system, this means the [acceleration vector](@entry_id:175748) $\ddot{\mathbf{u}}$ computed from the FOM must lie within the reduced basis subspace, $\text{range}(\mathbf{V})$.

A Galerkin ROM does *not* typically describe an invariant manifold of the full system. The Galerkin condition, $\mathbf{V}^{\top}\mathbf{R}=\mathbf{0}$, only forces the residual to be orthogonal to the subspace; it does not force the residual to be zero. Physically, this means the true [acceleration vector](@entry_id:175748) generally points off the reduced subspace, and the Galerkin projection finds the "closest" acceleration vector that lies within the subspace.

In the special case of a linear, undamped, unforced system ($ \mathbf{M}\ddot{\mathbf{u}} + \mathbf{K}\mathbf{u} = \mathbf{0} $), a subspace $\text{range}(\mathbf{V})$ is an invariant manifold if and only if it is spanned by a set of eigenvectors of the [generalized eigenproblem](@entry_id:168055) $\mathbf{K}\phi = \lambda \mathbf{M}\phi$. For general [nonlinear systems](@entry_id:168347), the situation is more complex. The [invariant manifolds](@entry_id:270082) that are tangent to the linear [eigenspaces](@entry_id:147356) at an equilibrium point are typically *curved*. A linear-subspace ROM, therefore, can only be a [first-order approximation](@entry_id:147559) to the true, curved invariant manifold near that equilibrium .

### Achieving Computational Efficiency

The ultimate goal of model reduction is a dramatic reduction in computation time for many-query applications (e.g., optimization, uncertainty quantification). This is achieved through a strict separation of computations into two stages.

#### The Offline-Online Paradigm

*   **Offline Stage:** This is a one-time, computationally expensive phase. It involves all the preparatory work that does not depend on the specific parameter value for which a solution is desired. This includes:
    1.  Generating snapshots by running the FOM (if using POD).
    2.  Constructing the reduced basis $\mathbf{V}$ from the snapshots.
    3.  Pre-computing all parameter-independent components of the reduced system.
*   **Online Stage:** This is the rapid computation phase performed for each new parameter $\mu$. It must be independent of the full-order dimension $n$. It involves:
    1.  Assembling the small $r \times r$ reduced matrices and vectors using the pre-computed offline data.
    2.  Solving the $r \times r$ ROM system.
    3.  Reconstructing the full-order solution if needed.

The key to enabling this separation is an **affine parameter dependence** of the FOM operators. This means the operators can be expressed as a short linear combination of parameter-dependent scalar functions and parameter-independent matrices. For the stiffness matrix, this would look like:

$
\mathbf{K}(\mu) = \sum_{q=1}^{Q_K} \theta_q(\mu) \mathbf{K}_q
$

where $\theta_q(\mu)$ are scalar functions and $\mathbf{K}_q$ are constant matrices. When this structure exists, the reduced [stiffness matrix](@entry_id:178659) becomes:

$
\mathbf{K}_r(\mu) = \mathbf{V}^{\top} \mathbf{K}(\mu) \mathbf{V} = \mathbf{V}^{\top} \left( \sum_{q=1}^{Q_K} \theta_q(\mu) \mathbf{K}_q \right) \mathbf{V} = \sum_{q=1}^{Q_K} \theta_q(\mu) (\mathbf{V}^{\top} \mathbf{K}_q \mathbf{V})
$

The small $r \times r$ matrices $\mathbf{K}_{r,q} = \mathbf{V}^{\top} \mathbf{K}_q \mathbf{V}$ can be computed once in the offline stage. In the online stage, assembling $\mathbf{K}_r(\mu)$ only requires evaluating the scalar functions $\theta_q(\mu)$ and performing a short weighted sum of small matrices—an operation whose cost is independent of $n$ .

The resulting speedup can be immense. For a typical dynamic structural analysis problem, the online cost of the FOM is dominated by the iterative solution of large [linear systems](@entry_id:147850) at each time step, scaling with $n$ and the number of non-zeros in $\mathbf{K}$. The online cost of the ROM is dominated by the assembly and solution of an $r \times r$ system. A concrete analysis shows that speedup factors of many orders of magnitude are readily achievable .

#### The Challenge of Nonlinearities: Hyper-reduction

For nonlinear problems, a new bottleneck appears. The internal force vector $\mathbf{f}_{\text{int}}(\mathbf{u})$ is a nonlinear function of the displacements. Even with a reduced basis, evaluating the reduced internal force vector for the ROM, $\mathbf{f}_{\text{int},r} = \mathbf{V}^{\top} \mathbf{f}_{\text{int}}(\mathbf{V}\mathbf{a})$, requires first computing the full $n$-dimensional vector $\mathbf{f}_{\text{int}}(\mathbf{V}\mathbf{a})$. This computation typically involves looping over all elements in the FE mesh, making its cost dependent on $n$ and destroying the online efficiency.

**Hyper-reduction** is a class of techniques designed to overcome this bottleneck. The core idea is to approximate the nonlinear function itself. A common approach, known as sampling or gappy POD, is to compute the internal force contributions only for a small subset of "sample" elements and then reconstruct the full projected term using pre-computed weights . The hyper-reduced internal force is approximated as:

$
\mathbf{f}_{\text{int}}^{\text{HR}}(\mathbf{u}) := \sum_{e \in S} w_e \mathbf{f}_{\text{int}}^{(e)}(\mathbf{u})
$

where $S$ is a small subset of elements and $w_e$ are weights. The goal of [hyper-reduction](@entry_id:163369) is to choose the samples and weights such that the projected hyper-reduced force accurately approximates the projected full force:

$
\mathbf{V}^{\top} \mathbf{f}_{\text{int}}^{\text{HR}}(\mathbf{V}\mathbf{a}) \approx \mathbf{V}^{\top} \mathbf{f}_{\text{int}}(\mathbf{V}\mathbf{a})
$

When successful, this allows the online evaluation of the nonlinear term to be independent of $n$. Importantly, if the original material model is hyperelastic (conservative), and if the element tangents are symmetric positive semidefinite, these crucial physical properties can be preserved in the hyper-reduced model by ensuring the weights are non-negative. This helps maintain the stability and physical consistency of the final reduced model . The introduction of [hyper-reduction](@entry_id:163369) constitutes a second layer of approximation, further modifying the underlying dynamics of the system being modeled .