## Introduction
Reduced Order Models (ROMs) offer a transformative promise for science and engineering: the ability to simulate complex, large-scale dynamical systems in near real-time. By projecting the governing equations onto a low-dimensional subspace, ROMs can capture the dominant behavior of a system at a fraction of the computational cost. However, this promise is often broken by the presence of nonlinearity. When a system's evolution depends on nonlinear operators, a standard Galerkin projection fails to produce a truly efficient ROM, as the evaluation of the nonlinear term remains tethered to the massive dimension of the original high-fidelity model. This computational bottleneck severely limits the practical utility of ROMs for a vast range of real-world problems.

This article addresses this critical knowledge gap by providing a comprehensive guide to the Empirical Interpolation Method (EIM) and its variants—a class of powerful [hyper-reduction](@entry_id:163369) techniques designed specifically to sever this dependency on the [full-order model](@entry_id:171001) size. By learning and applying these methods, you can unlock the full potential of model reduction for general nonlinear systems.

Across the following chapters, you will embark on a journey from fundamental principles to state-of-the-art applications. The "Principles and Mechanisms" chapter will first dissect the computational bottleneck in detail and then systematically derive the EIM and Discrete Empirical Interpolation Method (DEIM), explaining how they construct an efficient approximation from data. Next, the "Applications and Interdisciplinary Connections" chapter will explore how EIM is adapted for sophisticated [numerical schemes](@entry_id:752822) like Discontinuous Galerkin and [spectral methods](@entry_id:141737), and showcase its impact on complex problems in fluid dynamics, solid mechanics, and beyond. Finally, the "Hands-On Practices" section will transition from theory to practice, guiding you through concrete exercises to build, test, and refine your own EIM implementations. We begin by examining the core challenge that motivates this entire field: the persistent computational cost of nonlinearity in [reduced-order modeling](@entry_id:177038).

## Principles and Mechanisms

The central promise of projection-based Reduced Order Models (ROMs) is to replace large-scale dynamical systems with computationally inexpensive surrogates. This is achieved by projecting the governing equations onto a low-dimensional subspace that captures the dominant system behavior. However, the presence of nonlinear operators in the governing equations presents a formidable challenge to this paradigm. A naive application of Galerkin projection to a nonlinear system fails to yield a computationally efficient ROM, as the evaluation of the nonlinear term remains dependent on the dimension of the original high-fidelity model. This chapter elucidates the nature of this computational bottleneck and details the principles and mechanisms of the Empirical Interpolation Method (EIM) and its variants, which are a class of [hyper-reduction](@entry_id:163369) techniques designed to overcome this obstacle.

### The Computational Bottleneck in Nonlinear Reduced-Order Models

Consider a large-scale system of ordinary differential equations (ODEs) arising from the [semi-discretization](@entry_id:163562) of a nonlinear partial differential equation (PDE), written in the general form:
$$
\frac{d\mathbf{u}}{dt} = \mathbf{f}(\mathbf{u})
$$
where $\mathbf{u}(t) \in \mathbb{R}^{N}$ is the state vector of dimension $N \gg 1$, and $\mathbf{f}: \mathbb{R}^{N} \to \mathbb{R}^{N}$ is a nonlinear operator representing the discretized spatial derivatives and source terms.

In a projection-based ROM, we seek an approximation to the solution that lies in a low-dimensional subspace. This subspace is spanned by the columns of a [basis matrix](@entry_id:637164) $\mathbf{V} \in \mathbb{R}^{N \times r}$, where $r \ll N$. The state is thus approximated as $\mathbf{u}(t) \approx \mathbf{V}\mathbf{a}(t)$, where $\mathbf{a}(t) \in \mathbb{R}^{r}$ is the vector of reduced coordinates. Applying a Galerkin projection—substituting the approximation into the ODE system and projecting the residual onto the same subspace (i.e., requiring the residual to be orthogonal to the columns of $\mathbf{V}$)—yields the reduced dynamical system:
$$
\dot{\mathbf{a}} = \mathbf{V}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a})
$$
While this system is of small dimension $r$, a direct evaluation of its right-hand side for a given reduced state $\mathbf{a}$ reveals a persistent computational dependency on the large dimension $N$. The evaluation proceeds in three steps:
1.  **Lifting (or Reconstruction):** The reduced state $\mathbf{a} \in \mathbb{R}^{r}$ is mapped to the [high-dimensional approximation](@entry_id:750276) $\mathbf{u}_{\text{approx}} = \mathbf{V}\mathbf{a}$. This matrix-vector product has a computational cost of $\mathcal{O}(Nr)$.
2.  **Nonlinear Evaluation:** The full nonlinear operator $\mathbf{f}$ is evaluated on the high-dimensional state, $\mathbf{f}(\mathbf{u}_{\text{approx}})$. The cost of this step depends on the complexity of $\mathbf{f}$, but for typical operators arising from PDE discretizations (e.g., evaluating fluxes at all grid points or quadrature nodes), the cost scales at least linearly with the size of its input, i.e., $\mathcal{O}(N)$.
3.  **Projection:** The resulting high-dimensional vector is projected back onto the reduced subspace via the matrix-vector product $\mathbf{V}^{\top}\mathbf{f}(\mathbf{u}_{\text{approx}})$. This has a cost of $\mathcal{O}(Nr)$.

The total online cost is dominated by these $N$-dependent operations. This **computational bottleneck** renders the reduced model inefficient, as its simulation cost per time step still scales with the size of the original [full-order model](@entry_id:171001) (FOM), defeating the purpose of model reduction . To achieve a true reduction in computational complexity, the evaluation of the reduced nonlinear term $\mathbf{V}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a})$ must be accomplished with a cost that is independent of $N$. Techniques that achieve this are known as **[hyper-reduction](@entry_id:163369)** methods.

### The Special Case of Polynomial Nonlinearities: Tensor Contraction

For a specific class of nonlinearities—those that are polynomial in the components of $\mathbf{u}$—it is possible to achieve an $N$-independent evaluation exactly, without approximation, through an offline/online decomposition.

Consider a [quadratic nonlinearity](@entry_id:753902), which can be expressed in a general form using a bilinear operator $B$ such that $\mathbf{f}(\mathbf{u}) = B(\mathbf{u}, \mathbf{u})$. In component form, this might look like $f_k(\mathbf{u}) = \sum_{i,j} \mathcal{T}_{ijk} u_i u_j$, where $\mathcal{T}$ is a third-order tensor. The $m$-th component of the reduced nonlinear term is:
$$
(\dot{\mathbf{a}})_m = (\mathbf{V}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}))_m = \sum_{k=1}^{N} V_{mk} f_k(\mathbf{V}\mathbf{a})
$$
Substituting the approximation $u_i = \sum_{q=1}^{r} V_{iq} a_q$ yields:
$$
(\dot{\mathbf{a}})_m = \sum_{k=1}^{N} V_{mk} \left( \sum_{i,j=1}^{N} \mathcal{T}_{ijk} \left(\sum_{q=1}^{r} V_{iq} a_q\right) \left(\sum_{s=1}^{r} V_{js} a_s\right) \right)
$$
By rearranging the order of summation, we can isolate the operations that depend on the large dimension $N$:
$$
(\dot{\mathbf{a}})_m = \sum_{q,s=1}^{r} \left( \sum_{k,i,j=1}^{N} V_{mk} \mathcal{T}_{ijk} V_{iq} V_{js} \right) a_q a_s
$$
The term in the parenthesis, $\mathcal{C}_{mqs} = \sum_{k,i,j} V_{mk} \mathcal{T}_{ijk} V_{iq} V_{js}$, forms a reduced third-order tensor of size $r \times r \times r$. This tensor depends only on the fixed operator $\mathcal{T}$ and the basis $\mathbf{V}$, and can therefore be computed once in a computationally intensive **offline** stage. The **online** evaluation for any given $\mathbf{a}$ then becomes a simple [tensor contraction](@entry_id:193373):
$$
(\dot{\mathbf{a}})_m = \sum_{q,s=1}^{r} \mathcal{C}_{mqs} a_q a_s
$$
The cost to evaluate all $r$ components of $\dot{\mathbf{a}}$ is $\mathcal{O}(r^3)$, which is independent of $N$. This principle generalizes: for a polynomial nonlinearity of degree $p$, the online cost becomes $\mathcal{O}(r^{p+1})$ .

This elegant approach can also handle parameter dependence, provided the dependence is **affine**. If the operator can be written as $\mathbf{f}(\mathbf{u}, \boldsymbol{\mu}) = \sum_{q=1}^Q \theta_q(\boldsymbol{\mu}) \mathbf{f}_q(\mathbf{u})$, where each $\mathbf{f}_q$ is a polynomial and the $\theta_q(\boldsymbol{\mu})$ are scalar functions of the parameters $\boldsymbol{\mu}$, then one can precompute a reduced tensor for each $\mathbf{f}_q$. The online evaluation involves computing the $Q$ scalar coefficients $\theta_q(\boldsymbol{\mu})$ and performing a weighted sum of the $Q$ tensor contractions. If $Q$ is small, this remains $N$-independent and computationally efficient .

However, this tensor-based approach has two critical limitations:
1.  **Generality:** It is only applicable to polynomial nonlinearities. Many physical models and numerical schemes, such as those involving [trigonometric functions](@entry_id:178918), square roots (e.g., in Riemann solvers for [gas dynamics](@entry_id:147692)), or conditional logic, are non-polynomial. For these general cases, no exact algebraic rearrangement can remove the $N$-dependence .
2.  **Scalability:** The online cost of $\mathcal{O}(r^{p+1})$ can become prohibitive for even moderately large $r$ or for higher-degree polynomials (e.g., cubic terms with $p=3$ lead to $\mathcal{O}(r^4)$ cost). This "curse of dimensionality" in $r$ can render the ROM slower than the FOM if $r$ is not kept very small .

When faced with non-polynomial nonlinearities or non-affine parameter dependence, an alternative, approximate strategy is required. This is the primary motivation for the Empirical Interpolation Method.

### Approximation of General Nonlinearities: The Empirical Interpolation Method

The core idea of EIM and its discrete variant, the Discrete Empirical Interpolation Method (DEIM), is to abandon the goal of evaluating the projected nonlinearity exactly. Instead, we first approximate the high-dimensional nonlinear term $\mathbf{f}(\mathbf{u})$ itself with a surrogate that is computationally cheap to evaluate, and then project this surrogate onto the trial subspace.

The DEIM approximation posits that the output of the nonlinear function, $\mathbf{f}(\mathbf{u})$, lies close to a low-dimensional subspace. This subspace, termed the **collateral subspace**, is spanned by the columns of a [basis matrix](@entry_id:637164) $\mathbf{U} \in \mathbb{R}^{N \times m}$, where $m \ll N$ and typically $m \ge r$. The approximation takes the form:
$$
\mathbf{f}(\mathbf{u}) \approx \mathbf{U} \mathbf{c}(\mathbf{u})
$$
where $\mathbf{c}(\mathbf{u}) \in \mathbb{R}^{m}$ is a vector of coefficients that depends on the input state $\mathbf{u}$.

#### The DEIM Algorithm: Mechanism and Derivation

To determine the unknown coefficients $\mathbf{c}(\mathbf{u})$ efficiently, DEIM imposes an interpolation condition. It requires the approximation $\mathbf{U}\mathbf{c}$ to match the true function $\mathbf{f}(\mathbf{u})$ at a small number of $m$ carefully selected component indices, known as **interpolation points** or **magic points**. Let these indices be $\rho_1, \rho_2, \dots, \rho_m$. We can represent this selection with a **selection matrix** $\mathbf{P} \in \mathbb{R}^{N \times m}$, whose columns are the canonical basis vectors $\mathbf{e}_{\rho_i} \in \mathbb{R}^N$. Applying this matrix as $\mathbf{P}^{\top}$ to a vector simply extracts the components at the selected indices.

The interpolation condition is then written as:
$$
\mathbf{P}^{\top}\mathbf{f}(\mathbf{u}) = \mathbf{P}^{\top}(\mathbf{U}\mathbf{c})
$$
This is a square linear system for the unknown coefficients $\mathbf{c}$:
$$
(\mathbf{P}^{\top}\mathbf{U}) \mathbf{c} = \mathbf{P}^{\top}\mathbf{f}(\mathbf{u})
$$
Provided the matrix $\mathbf{P}^{\top}\mathbf{U} \in \mathbb{R}^{m \times m}$ is invertible (which is a key consideration in selecting the interpolation points), we can solve for $\mathbf{c}$:
$$
\mathbf{c}(\mathbf{u}) = (\mathbf{P}^{\top}\mathbf{U})^{-1} \mathbf{P}^{\top}\mathbf{f}(\mathbf{u})
$$
Substituting this back into the approximation for $\mathbf{f}(\mathbf{u})$ and then into the reduced system provides the DEIM approximation of the reduced nonlinear term :
$$
\dot{\mathbf{a}} = \mathbf{V}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}) \approx \mathbf{V}^{\top} \left( \mathbf{U} (\mathbf{P}^{\top}\mathbf{U})^{-1} \mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}) \right)
$$
This expression can be rearranged for an efficient offline/online decomposition:
$$
\dot{\mathbf{a}} \approx \left( \mathbf{V}^{\top}\mathbf{U} (\mathbf{P}^{\top}\mathbf{U})^{-1} \right) \left( \mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}) \right)
$$
In the offline stage, we compute and store the reduced matrix $\mathbf{A}_{\text{DEIM}} = \mathbf{V}^{\top}\mathbf{U} (\mathbf{P}^{\top}\mathbf{U})^{-1} \in \mathbb{R}^{r \times m}$. The online evaluation for a given $\mathbf{a}$ then involves:
1.  **Lifting to interpolation points:** Reconstruct the state approximation $\mathbf{u}_{\text{approx}} = \mathbf{V}\mathbf{a}$ only at the $m$ rows corresponding to the interpolation points. This is equivalent to computing $\mathbf{P}^{\top}\mathbf{V}\mathbf{a}$, an operation of cost $\mathcal{O}(mr)$.
2.  **Sparse Nonlinear Evaluation:** Evaluate the nonlinear function $f_i$ only for the $m$ selected indices $i \in \{\rho_1, \dots, \rho_m\}$. This gives the vector $\mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a})$ at a cost of $\mathcal{O}(m)$.
3.  **Linear Combination:** Multiply by the precomputed matrix: $\dot{\mathbf{a}} \approx \mathbf{A}_{\text{DEIM}} (\mathbf{P}^{\top}\mathbf{f}(\mathbf{V}\mathbf{a}))$. This has a cost of $\mathcal{O}(rm)$.

The total online cost is dominated by terms proportional to $m$ and $r$, and is completely independent of the FOM dimension $N$. This restores the computational efficiency of the ROM, albeit at the cost of introducing an additional layer of approximation.

#### Constructing the Empirical Basis: Snapshots and POD

The quality of the DEIM approximation hinges on the collateral basis $\mathbf{U}$. A good basis must provide a low-error representation for any vector $\mathbf{f}(\mathbf{u})$ that might be encountered during the system's evolution. The standard method for constructing such a basis is to use Proper Orthogonal Decomposition (POD), which is equivalent to Singular Value Decomposition (SVD), on a collection of sample outputs of the nonlinearity.

These samples are called **snapshots**. A snapshot matrix $\mathbf{S}_{\mathbf{f}} = [\mathbf{f}(\mathbf{u}^{(1)}) | \mathbf{f}(\mathbf{u}^{(2)}) | \dots | \mathbf{f}(\mathbf{u}^{(K)})]$ is assembled, where each column is the result of evaluating the nonlinear operator for a representative state $\mathbf{u}^{(k)}$. The truncated SVD of this matrix, $\mathbf{S}_{\mathbf{f}} \approx \mathbf{U} \boldsymbol{\Sigma} \mathbf{W}^{\top}$, provides the orthonormal basis $\mathbf{U} \in \mathbb{R}^{N \times m}$ that is optimal in the sense that it minimizes the projection error over the provided snapshots.

The choice of snapshots is critical for the robustness and accuracy of the resulting ROM. Several principled strategies exist for generating a rich snapshot set :
*   **Trajectory-based Sampling:** The most common approach is to run a full-order simulation for a few representative parameter values and collect snapshots $\mathbf{f}(\mathbf{u}(t_j))$ at various time instances $t_j$.
*   **Parametric Sweeps:** To ensure the ROM is accurate over a range of parameters $\boldsymbol{\mu} \in \mathcal{P}$, snapshots should be collected from FOM simulations at various points in the parameter domain, particularly at the boundaries and in regions of high sensitivity. This ensures the basis $\mathbf{U}$ captures the parametric variability of the nonlinearity manifold.
*   **Random Perturbations:** Augmenting the snapshot set with evaluations at randomly perturbed states, $\mathbf{f}(\mathbf{u}^{(k)} + \epsilon \boldsymbol{\eta})$, is an effective technique. For small perturbations, this is equivalent to sampling the action of the nonlinearity's Jacobian, $\mathbf{J}_{\mathbf{f}}(\mathbf{u}^{(k)})$, on random vectors. This enriches the basis with information about the local [tangent space](@entry_id:141028) of the nonlinearity manifold, improving robustness for states that are near, but not exactly on, the sampled trajectories.
*   **Greedy/Adaptive Sampling:** An advanced approach involves iteratively building the basis. One starts with an initial basis, identifies a state-parameter pair where the current ROM has the largest error (estimated by an [a posteriori error indicator](@entry_id:746618)), runs the FOM at that point to generate a new "most-needed" snapshot, and augments the basis with this new information.

A crucial, non-negotiable principle is that **snapshots must be generated using the identical discrete operators as the FOM** . If the snapshots were computed with, for example, a different quadrature rule or [numerical flux](@entry_id:145174), the basis $\mathbf{U}$ would be optimized to represent a different function manifold, leading to a systematic and potentially destabilizing modeling error in the ROM.

#### Selecting Interpolation Points: The Greedy Algorithm

With a basis $\mathbf{U}$ in hand, the interpolation points must be chosen. A naive choice could lead to an ill-conditioned or even [singular matrix](@entry_id:148101) $\mathbf{P}^{\top}\mathbf{U}$. The standard DEIM algorithm selects these points via a greedy procedure. The first point $\rho_1$ is chosen as the index where the first basis vector, $\mathbf{U}_{:,1}$, has its maximum absolute value. The second [basis vector](@entry_id:199546) is made orthogonal to the first (at the selected row), and the second point $\rho_2$ is chosen to maximize the magnitude of the residual. This process, which can be implemented efficiently using a pivoted QR or LU decomposition, iteratively selects points that are "most informative" given the previously chosen points, thereby promoting a well-conditioned $\mathbf{P}^{\top}\mathbf{U}$ matrix.

### Applications and Advanced Topics

#### Hyper-reduction for Discontinuous Galerkin Methods

Discontinuous Galerkin (DG) methods are a powerful tool for discretizing conservation laws, but their structure makes them a prime candidate for [hyper-reduction](@entry_id:163369). The DG semi-discrete residual for an element $K_e$ can be written as $M_e \dot{\mathbf{u}}_e = \mathbf{f}_e(\mathbf{u})$, where $\mathbf{f}_e$ is the local residual operator. This operator consists of two parts :
$$
\mathbf{f}_e(\mathbf{u}) = \mathbf{f}_e^{\text{vol}}(\mathbf{u}) + \mathbf{f}_e^{\text{surf}}(\mathbf{u})
$$
The **volume term**, $\mathbf{f}_e^{\text{vol}}$, arises from integrals over the element's interior, e.g., $\int_{K_e} \nabla \phi_i \cdot \mathbf{F}(\mathbf{u}_h) \,dx$. These are evaluated using quadrature, requiring the evaluation of the physical flux $\mathbf{F}$ at a potentially large number of quadrature points within each element. The **surface term**, $\mathbf{f}_e^{\text{surf}}$, comes from integrals on the element faces, e.g., $\int_{\partial K_e} \phi_i \hat{\mathbf{F}}(\mathbf{u}_h^-, \mathbf{u}_h^+) \,ds$, where $\hat{\mathbf{F}}$ is a numerical flux.

DEIM is ideally suited to approximate the volume term. The collection of all flux evaluations at all quadrature points across all elements forms the high-dimensional vector to be approximated. However, the surface term can also pose a bottleneck. Many sophisticated numerical fluxes (e.g., for [entropy-stable schemes](@entry_id:749017) or for the Euler equations) are non-polynomial functions of the states on either side of the interface. In such cases, the [tensor contraction](@entry_id:193373) method is inapplicable, and [hyper-reduction](@entry_id:163369) via DEIM becomes essential to approximate the numerical flux evaluations as well . A complete DG [hyper-reduction](@entry_id:163369) scheme often involves assembling a single nonlinear vector $\mathbf{f}(\mathbf{u})$ containing all quadrature-point and face-based nonlinear evaluations, and then applying DEIM to this concatenated vector. The global operator is then assembled from the hyper-reduced element-wise operators .

#### A Variant: The Empirical Quadrature Method (EQM)

A closely related technique is the Empirical Quadrature Method (EQM), which seeks to directly approximate the integral terms in the [weak form](@entry_id:137295). Instead of approximating the integrand function $\mathbf{f}(\mathbf{u})$, EQM constructs a custom, low-cost [quadrature rule](@entry_id:175061). An integral of the form $\int_{\Omega} \phi_i(x) g(u(x)) \,dx$ is approximated by a weighted sum of integrand evaluations at a small set of empirically selected quadrature points $\{x_j\}$:
$$
\int_{\Omega} \phi_i(x) g(u(x)) \,dx \approx \sum_{j=1}^{m_q} w_j \phi_i(x_j) g(u(x_j))
$$
The key idea is that the points $\{x_j\}$ and weights $\{w_j\}$ are not from a standard rule like Gaussian quadrature, but are "learned" from data. Given a set of training snapshots $\{u^{(k)}(x)\}$, the weights can be determined by solving a linear system that enforces the quadrature rule to be exact for each snapshot integral . For instance, given two training snapshots $u^{(1)}$ and $u^{(2)}$ and two selected points $x_1, x_2$, the weights $w_1, w_2$ are found by solving:
$$
\begin{pmatrix}
\phi(x_1) g(u^{(1)}(x_1)) & \phi(x_2) g(u^{(1)}(x_2)) \\
\phi(x_1) g(u^{(2)}(x_1)) & \phi(x_2) g(u^{(2)}(x_2))
\end{pmatrix}
\begin{pmatrix} w_1 \\ w_2 \end{pmatrix}
=
\begin{pmatrix}
\int \phi(x) g(u^{(1)}(x)) dx \\
\int \phi(x) g(u^{(2)}(x)) dx
\end{pmatrix}
$$
This approach provides another avenue for [hyper-reduction](@entry_id:163369), particularly tailored to integral-based weak forms.

#### Practical Considerations and Refinements

**Boundary Conditions:** In many applications, it is crucial that the ROM exactly satisfies the specified boundary conditions. This can be achieved within the DEIM framework by constraining the selection of interpolation points. If the vector $\mathbf{f}(\mathbf{u})$ includes degrees of freedom corresponding to boundary or "ghost" points where boundary conditions are imposed, one can force the DEIM procedure to select these points. The selection matrix $\mathbf{P}$ is constructed to include the canonical basis vectors for all boundary points, with the remaining points chosen greedily from the interior degrees of freedom. This ensures that the DEIM approximation interpolates the boundary data exactly, embedding the boundary condition enforcement directly into the [hyper-reduction](@entry_id:163369) without requiring ad-hoc post-processing .

**Aliasing in Spectral Methods:** When using Fourier [pseudospectral methods](@entry_id:753853), a subtle issue arises during snapshot generation. The pseudospectral evaluation of a product, like $g(u) = u^2$, is performed by pointwise multiplication on the physical grid. This is equivalent to a [circular convolution](@entry_id:147898) in Fourier space, which causes **[aliasing](@entry_id:146322)**: high-frequency modes of the true product are incorrectly "wrapped around" and contaminate the low-frequency modes. Snapshots corrupted by [aliasing](@entry_id:146322) lead to a less efficient collateral basis $\mathbf{U}$, as the SVD must waste capacity representing this spurious energy. This can be avoided by performing a **de-aliased** evaluation using [zero-padding](@entry_id:269987) in Fourier space, a procedure known as the **3/2-rule** for quadratic nonlinearities. By transforming to a finer grid with at least $3/2$ the number of points, performing the product, and then transforming back and truncating, one obtains snapshots free of [aliasing error](@entry_id:637691). This leads to a higher-quality basis $\mathbf{U}$ with faster singular value decay and improved approximation accuracy .

### Theoretical Analysis and Limitations

#### Cost Comparison: Tensor Contraction vs. DEIM

While DEIM is more general than [tensor contraction](@entry_id:193373), it introduces an approximation error. It is instructive to compare their costs in a scenario where both are applicable, such as a cubic nonlinearity. The tensor method has an exact online cost of $\mathcal{O}(r^4)$. The DEIM approximation has an online cost of roughly $\mathcal{O}(rm)$ (plus the cost to evaluate the nonlinear function at $m$ points). To maintain accuracy for complex nonlinearities, the number of interpolation points $m$ may need to grow polynomially with $r$. For instance, if analysis shows that $m$ must scale quadratically with the reduced dimension, i.e., $m \propto r^2$, the DEIM online cost would be $\mathcal{O}(r^3)$ . While asymptotically better than the tensor method's $\mathcal{O}(r^4)$ cost, this "quadratic curse of dimensionality" indicates that for ROMs with larger reduced dimensions $r$, DEIM can become computationally demanding itself, requiring a large number of interpolation points $m$ to maintain accuracy.

#### The Commutator Error and Stability

A deeper theoretical issue with DEIM and other approximate [hyper-reduction](@entry_id:163369) methods is their interaction with the Galerkin projection, which can have profound implications for the stability of the ROM. The order of operations matters: applying the exact nonlinearity and then projecting is not the same as projecting first and then applying an approximate nonlinearity. The difference is the **[commutator error](@entry_id:747515)**:
$$
E(u) = \mathcal{P}_r(\mathcal{N}(u)) - \tilde{\mathcal{N}}(\mathcal{P}_r u)
$$
where $\mathcal{P}_r$ is the [projection operator](@entry_id:143175) and $\tilde{\mathcal{N}}$ is the EIM/DEIM approximation of the nonlinear operator $\mathcal{N}$. This error is generally non-zero .

The significance of this error is that many full-order [numerical schemes](@entry_id:752822) are designed with specific algebraic structures (e.g., skew-symmetry of the convective operator) that guarantee the conservation of quantities like energy or entropy at the discrete level, ensuring stability. Approximate [hyper-reduction](@entry_id:163369) methods like DEIM typically do not preserve these delicate structures. The [commutator error](@entry_id:747515) manifests as a spurious term in the discrete [energy balance](@entry_id:150831) of the ROM, which can act as an artificial source or sink of energy, potentially leading to instabilities and blow-up even when the original FOM and the Galerkin ROM are perfectly stable. This remains an active area of research, with ongoing efforts to develop structure-preserving [hyper-reduction](@entry_id:163369) methods that mitigate these stability issues.