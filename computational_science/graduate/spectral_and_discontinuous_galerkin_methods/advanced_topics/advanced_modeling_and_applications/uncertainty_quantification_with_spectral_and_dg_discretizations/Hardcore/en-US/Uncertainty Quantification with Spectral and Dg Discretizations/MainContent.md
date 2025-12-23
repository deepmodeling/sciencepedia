## Introduction
Partial differential equations (PDEs) are the mathematical backbone of modern science and engineering, but their real-world predictive power is often limited by uncertainties in model parameters, boundary conditions, or even the geometry of the domain. Uncertainty Quantification (UQ) provides a rigorous mathematical and computational framework to propagate these input uncertainties through the model and quantify their impact on the solution. However, integrating UQ with sophisticated numerical discretizations like spectral and Discontinuous Galerkin (DG) methods presents a unique challenge, requiring a unified approach that respects both the [high-order accuracy](@entry_id:163460) of the spatial scheme and the probabilistic nature of the inputs. This article addresses this knowledge gap by providing a comprehensive guide to the theory and practice of UQ for PDEs solved with spectral and DG methods.

The journey begins in the **Principles and Mechanisms** chapter, where we will build the foundational framework from the ground up. You will learn how to represent random inputs using the Karhunen-Loève expansion and approximate stochastic solutions with Generalized Polynomial Chaos (gPC). We will then derive and contrast the two dominant computational strategies: the intrusive stochastic Galerkin method and the non-intrusive [stochastic collocation](@entry_id:174778) approach. Next, the **Applications and Interdisciplinary Connections** chapter demonstrates the power of this framework by exploring its use in solid mechanics, fluid dynamics, and wave physics, while also delving into the computational cost, stability analysis, and frontiers of UQ methodology. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding of assembling the core components of these [stochastic systems](@entry_id:187663). By the end of this article, you will have a deep understanding of how to combine these powerful numerical tools to perform robust [uncertainty analysis](@entry_id:149482) for complex physical systems.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms that underpin [uncertainty quantification](@entry_id:138597) for [partial differential equations](@entry_id:143134) (PDEs) discretized with spectral and Discontinuous Galerkin (DG) methods. We will systematically build the framework, starting from the representation of random inputs, proceeding to the spectral approximation of stochastic solutions, and culminating in the formulation and analysis of both intrusive and non-intrusive computational strategies.

### Modeling Parametric Uncertainty: The Karhunen-Loève Expansion

A primary challenge in uncertainty quantification (UQ) is the mathematical representation of [random fields](@entry_id:177952), such as a spatially varying diffusion coefficient $a(x, \omega)$ in an elliptic PDE . While the [random field](@entry_id:268702) may be infinite-dimensional in principle, for computational purposes it is essential to approximate it using a finite number of random variables. The **Karhunen-Loève (KL) expansion** provides a systematic and optimal means of achieving this [dimensionality reduction](@entry_id:142982) for any second-order [random field](@entry_id:268702)—that is, a field with [finite variance](@entry_id:269687).

Consider a [random field](@entry_id:268702) $g(x, \omega)$ defined on a spatial domain $D$ with mean $\bar{g}(x) = \mathbb{E}[g(x, \cdot)]$ and a continuous, symmetric [covariance kernel](@entry_id:266561) $C(x, y) = \mathbb{E}[(g(x, \cdot) - \bar{g}(x))(g(y, \cdot) - \bar{g}(y))]$. The KL expansion represents the centered field, $g'(x, \omega) = g(x, \omega) - \bar{g}(x)$, as an [infinite series](@entry_id:143366):

$$
g(x, \omega) = \bar{g}(x) + \sum_{n=1}^{\infty} \sqrt{\lambda_n} \phi_n(x) \xi_n(\omega)
$$

The components of this expansion are derived from the spectral decomposition of the covariance [integral operator](@entry_id:147512) $T_C$, defined by $(T_C \varphi)(x) = \int_D C(x, y) \varphi(y) \, dy$ . Specifically:
-   $\{\lambda_n\}_{n \ge 1}$ are the non-negative eigenvalues of $T_C$, ordered non-increasingly.
-   $\{\phi_n(x)\}_{n \ge 1}$ are the corresponding eigenfunctions, which form an orthonormal basis in $L^2(D)$. They are solutions to the integral eigenproblem $\int_D C(x, y) \phi_n(y) \, dy = \lambda_n \phi_n(x)$.
-   $\{\xi_n(\omega)\}_{n \ge 1}$ are scalar random variables with [zero mean](@entry_id:271600) and unit variance. They are also **uncorrelated**, i.e., $\mathbb{E}[\xi_n \xi_m] = \delta_{nm}$.

A crucial property of the KL expansion is its optimality in the mean-square sense. Truncating the series after $N$ terms provides the best $N$-term [linear approximation](@entry_id:146101) of the field. The [mean-square error](@entry_id:194940) of this truncation is simply the sum of the neglected eigenvalues :

$$
\mathbb{E}\left[ \left\| g(\cdot, \omega) - \left(\bar{g}(\cdot) + \sum_{n=1}^{N} \sqrt{\lambda_n} \phi_n(\cdot) \xi_n(\omega) \right) \right\|_{L^2(D)}^2 \right] = \sum_{n=N+1}^{\infty} \lambda_n
$$

This remarkable result implies that to minimize the error, one should retain the terms corresponding to the largest eigenvalues. The decay rate of the eigenvalues $\lambda_n$ is linked to the smoothness of the [covariance kernel](@entry_id:266561) $C(x, y)$, with smoother kernels leading to faster decay and more efficient truncation.

A key distinction arises from the statistical properties of the underlying field. The KL coefficients $\{\xi_n\}$ are always uncorrelated by construction. However, they are **statistically independent if and only if the original random field $g(x, \omega)$ is a Gaussian field**  . This is a profound result: for a Gaussian field, the KL expansion decomposes it into a series of independent standard Gaussian random variables modulating deterministic spatial functions. For non-Gaussian fields, the coefficients, while uncorrelated, may retain higher-order statistical dependencies. In many applications, the field is either assumed to be Gaussian or the KL coefficients are approximated as being independent, which simplifies subsequent analysis.

### Generalized Polynomial Chaos: A Spectral Basis for Randomness

The KL expansion reduces an infinite-dimensional [random field](@entry_id:268702) to a dependence on a vector of scalar random variables $\boldsymbol{\xi} = (\xi_1, \xi_2, \dots)$. The solution to a PDE with such a coefficient, $u(x, \boldsymbol{\xi})$, is itself a [random field](@entry_id:268702). The **Generalized Polynomial Chaos (gPC)** framework provides a powerful tool for representing this solution, or any other quantity of interest, as a spectral expansion in the random variables $\boldsymbol{\xi}$.

The core idea of gPC is to represent a random function $q(\boldsymbol{\xi})$ as a series of polynomials that are orthogonal with respect to the probability measure of $\boldsymbol{\xi}$. If $\boldsymbol{\xi}$ has a [joint probability density function](@entry_id:177840) (PDF) $\rho(\boldsymbol{\xi})$, we seek a [basis of polynomials](@entry_id:148579) $\{\Psi_{\alpha}(\boldsymbol{\xi})\}$ such that:

$$
\mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi})] = \int_{\Gamma} \Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi} = \delta_{\alpha\beta}
$$

Here, $\Gamma$ is the support of $\boldsymbol{\xi}$, and $\alpha$ and $\beta$ are multi-indices. The choice of the optimal polynomial family is dictated by the distribution of the input random variables, a correspondence classified by the **Wiener-Askey scheme** . The most common pairings include:

-   **Gaussian variables** ($\mathcal{N}(0,1)$): **Hermite polynomials**, orthogonal with respect to the weight $w(x) = (2\pi)^{-1/2} \exp(-x^2/2)$.
-   **Uniform variables** ($U[-1,1]$): **Legendre polynomials**, orthogonal with respect to the weight $w(x) = 1/2$.
-   **Gamma variables** ($\mathrm{Gamma}(k,\theta)$): **Generalized Laguerre polynomials**, with appropriate scaling and shifting, orthogonal with respect to the weight $w(x) \propto x^{k-1}\exp(-x/\theta)$.

This direct link between the distribution of the inputs and the choice of an [orthogonal basis](@entry_id:264024) is fundamental to the efficiency of [spectral methods](@entry_id:141737) in UQ.

#### Handling Correlated Inputs

The standard gPC construction assumes that the components of $\boldsymbol{\xi}$ are independent, allowing for the construction of a multivariate basis via tensor products of univariate orthogonal polynomials. When the inputs are correlated, this tensor-product construction no longer yields an [orthogonal basis](@entry_id:264024).

Consider a random vector $\boldsymbol{\xi}$ that is jointly Gaussian with a mean of zero and a non-diagonal covariance matrix $\Sigma$. Attempting to use a tensor-product Hermite basis in these correlated variables would violate the [orthogonality condition](@entry_id:168905). A standard and effective remedy is to first apply a decorrelating [linear transformation](@entry_id:143080). Since $\Sigma$ is symmetric and [positive definite](@entry_id:149459), it admits a factorization, for instance, a Cholesky decomposition $\Sigma = LL^\top$. A new random vector $\boldsymbol{\eta}$ can be defined as $\boldsymbol{\eta} = L^{-1}\boldsymbol{\xi}$. The covariance of $\boldsymbol{\eta}$ is the identity matrix, meaning its components are uncorrelated standard Gaussian variables, and thus independent. One can then build a standard tensor-product Hermite gPC basis in the coordinates of $\boldsymbol{\eta}$ and proceed with the spectral expansion. This restores orthogonality and enables the use of the standard machinery .

### The Combined Approximation Space and Extraction of Moments

To numerically solve a random PDE, we must discretize in both physical space and random space. Combining a spatial [finite element method](@entry_id:136884), such as a Discontinuous Galerkin (DG) method, with a stochastic gPC expansion leads to a tensor-product approximation.

#### Tensor-Product Spaces and Indexing

Let $V_h$ be a finite-dimensional spatial approximation space (e.g., a DG space of broken polynomials) with basis $\{\phi_i(x)\}_{i=1}^{N_s}$. Let $S_p$ be a gPC space of multivariate polynomials in $\boldsymbol{\xi} \in \mathbb{R}^{d_\xi}$ of total degree at most $p$, with basis $\{\Psi_{\alpha}(\boldsymbol{\xi})\}_{\alpha \in \mathcal{A}_p}$. The combined tensor-product space $V_h \otimes S_p$ is the space of functions spanned by all products of the basis functions:

$$
V_h \otimes S_p = \mathrm{span} \{\phi_i(x) \Psi_{\alpha}(\boldsymbol{\xi}) : i \in \{1, \dots, N_s\}, \alpha \in \mathcal{A}_p \}
$$

An approximate solution $u_{h,p}(x, \boldsymbol{\xi})$ is sought in this space:

$$
u_{h,p}(x, \boldsymbol{\xi}) = \sum_{i=1}^{N_s} \sum_{\alpha \in \mathcal{A}_p} u_{i,\alpha} \phi_i(x) \Psi_{\alpha}(\boldsymbol{\xi}) = \sum_{\alpha \in \mathcal{A}_p} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi})
$$

where $u_{\alpha}(x) = \sum_{i=1}^{N_s} u_{i,\alpha} \phi_i(x)$ are the deterministic coefficient fields. The dimension of the stochastic space $S_p$ for $d_\xi$ variables and total degree $p$ is given by the combinatorial "[stars and bars](@entry_id:153651)" formula, $N_\xi = |\mathcal{A}_p| = \binom{d_\xi + p}{p}$. The total number of degrees of freedom in the problem is therefore $\dim(V_h \otimes S_p) = N_s \times N_\xi$ . For implementation, these $(i, \alpha)$ pairs of indices must be mapped to a single global index for the vector of unknowns. A common choice is a block ordering where the spatial index $i$ runs fastest, giving the map $k = (I(\alpha)-1)N_s + i$, where $I(\alpha)$ is the position of $\alpha$ in an ordered list of multi-indices.

#### Mean and Variance from gPC Coefficients

A primary advantage of the gPC representation is the ease with which statistical moments of the solution can be computed. The basis is constructed such that the zeroth polynomial, $\Psi_0$, is a constant (typically 1). By [orthonormality](@entry_id:267887), $\mathbb{E}[\Psi_0] = 1$ and $\mathbb{E}[\Psi_\alpha] = \mathbb{E}[\Psi_\alpha \Psi_0] = 0$ for all $\alpha \neq 0$.

Taking the expectation of the gPC expansion for $u(x, \boldsymbol{\xi})$ yields:

$$
\mathbb{E}[u(x, \boldsymbol{\xi})] = \mathbb{E}\left[\sum_{\alpha} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi})\right] = \sum_{\alpha} u_{\alpha}(x) \mathbb{E}[\Psi_{\alpha}(\boldsymbol{\xi})] = u_0(x) \mathbb{E}[\Psi_0] = u_0(x)
$$

The **mean** of the random solution field is simply its zeroth-order gPC coefficient field .

The variance can be computed similarly. The pointwise variance is $\mathrm{Var}[u(x, \boldsymbol{\xi})] = \mathbb{E}[(u(x, \boldsymbol{\xi}) - \mathbb{E}[u(x, \boldsymbol{\xi})])^2]$. Substituting the gPC series:

$$
u(x, \boldsymbol{\xi}) - \mathbb{E}[u(x, \boldsymbol{\xi})] = \sum_{|\alpha|>0} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi})
$$

Squaring this and taking the expectation, the cross-terms vanish due to orthogonality, leaving:

$$
\mathrm{Var}[u(x, \boldsymbol{\xi})] = \mathbb{E}\left[\left(\sum_{|\alpha|>0} u_{\alpha}(x) \Psi_{\alpha}(\boldsymbol{\xi})\right)^2\right] = \sum_{|\alpha|>0} \sum_{|\beta|>0} u_{\alpha}(x) u_{\beta}(x) \mathbb{E}[\Psi_{\alpha}\Psi_{\beta}] = \sum_{|\alpha|>0} u_{\alpha}(x)^2
$$

The pointwise **variance** is the sum of the squares of the higher-order gPC coefficient fields. If we consider a spatially integrated variance, such as $\mathbb{E}[\|u - \mathbb{E}[u]\|_{L^2(D)}^2]$, the same logic applies, yielding the sum of the squared $L^2$-norms of the higher-order coefficients: $\sum_{|\alpha|>0} \|u_\alpha\|_{L^2(D)}^2$ .

### Intrusive Methods: The Stochastic Galerkin Approach

Having established the representation of the solution, we now turn to methods for computing the unknown coefficient fields $u_\alpha(x)$. The **stochastic Galerkin method** is an *intrusive* approach, meaning it requires modification of the original PDE solver to derive and solve a new, large, coupled system for all the coefficients simultaneously.

#### Formulation and Derivation of Coupled Equations

The method is based on a Galerkin projection in the random space. We require the residual of the PDE, when the gPC approximation is substituted, to be orthogonal to the gPC basis itself. For an elliptic problem $-\nabla \cdot (a(x,\boldsymbol{\xi}) \nabla u) = f(x)$, this condition is:

$$
\mathbb{E}\left[\left(-\nabla \cdot (a \nabla u_{h,p}) - f\right) \Psi_{\alpha} \right] = 0, \quad \text{for all } \alpha \in \mathcal{A}_p
$$

Substituting $u_{h,p} = \sum_{\beta} u_{\beta}(x) \Psi_{\beta}(\boldsymbol{\xi})$ and exploiting the linearity of the operators and the fact that $\nabla$ does not act on $\boldsymbol{\xi}$, we arrive at a coupled system of PDEs for the coefficients $u_\beta(x)$ :

$$
-\sum_{\beta \in \mathcal{A}_p} \nabla \cdot \left( \mathbb{E}[a \Psi_{\alpha} \Psi_{\beta}] \nabla u_{\beta}(x) \right) = f(x) \mathbb{E}[\Psi_{\alpha}] = f(x)\delta_{\alpha 0}
$$

The coupling between the equations for different modes is governed by the stochastic stiffness coefficients $\widehat{a}_{\alpha\beta}(x) = \mathbb{E}[a(x,\boldsymbol{\xi}) \Psi_{\alpha}(\boldsymbol{\xi}) \Psi_{\beta}(\boldsymbol{\xi})]$. For an affine dependence of the coefficient, $a(x, \boldsymbol{\xi}) = a_0(x) + \sum_{k=1}^{d} a_k(x) \xi_k$, and a Hermite polynomial basis, these coupling terms can be computed analytically using the [three-term recurrence relation](@entry_id:176845) for the polynomials. This leads to a sparse, structured coupling :

$$
\widehat{a}_{\alpha\beta}(x) = a_{0}(x)\,\delta_{\alpha\beta} + \sum_{k=1}^{d} a_{k}(x) \left( \sqrt{\alpha_k+1}\,\delta_{\beta, \alpha+e_k} + \sqrt{\alpha_k}\,\delta_{\beta, \alpha-e_k} \right)
$$
where $e_k$ is the multi-index with a 1 in the $k$-th position. This shows that the equation for mode $\alpha$ is directly coupled only to its immediate neighbors in the multi-index graph.

#### The Structure of the Fully Discrete System

When this system of PDEs is subsequently discretized in space using a DG method, a large, monolithic linear algebra system results. The weak formulation for the DG method is applied to the coupled system. For a hyperbolic conservation law, for example, this involves integrating by parts on each element and introducing a [numerical flux](@entry_id:145174) at interfaces, a procedure that is then projected onto the stochastic basis .

For an elliptic problem, if we discretize the spatial domain with basis functions $\{\phi_i(x)\}$, the DG [stiffness matrix](@entry_id:178659) for a deterministic coefficient $a_m(x)$ is $(K_m)_{ij} = B_{a_m}(\phi_j, \phi_i)$. The global stiffness matrix for the full stochastic Galerkin system acting on the stacked vector of all unknown coefficients takes a highly structured form expressed via Kronecker products :

$$
\mathcal{A} = \sum_{m=0}^{M} G_m \otimes K_m
$$

Here, $a(x, \boldsymbol{\xi})$ is expanded as $\sum_{m=0}^M a_m(x) \Psi_m(\boldsymbol{\xi})$, $K_m$ is the spatial DG matrix for coefficient $a_m(x)$, and $G_m$ is a matrix of triple-product integrals $(G_m)_{\alpha\beta} = \mathbb{E}[\Psi_\alpha \Psi_\beta \Psi_m]$. This elegant structure reveals how the spatial operators $K_m$ are weighted and coupled by the stochastic interaction matrices $G_m$.

#### Theoretical Guarantees: Well-posedness and Convergence

The validity of the stochastic Galerkin method rests on firm theoretical ground. For the original random PDE to be well-posed, key properties must hold for (almost) every realization of the random parameters. For an elliptic problem, the Lax-Milgram theorem guarantees a unique solution in $H_0^1(D)$ provided the diffusion coefficient $a(x, \omega)$ is uniformly bounded and coercive, i.e., there exist deterministic constants $0  a_{\min} \le a_{\max}  \infty$ such that $a_{\min} \le a(x, \omega) \le a_{\max}$ almost surely. Under these conditions, the solution can also be shown to have finite mean-square energy, i.e., $u \in L^2(\Omega; H_0^1(D))$ .

These conditions are also sufficient for the stability and convergence of the combined intrusive stochastic Galerkin and DG method. The [uniform ellipticity](@entry_id:194714) and boundedness of $a(x, \boldsymbol{\xi})$ ensures that the resulting global [bilinear form](@entry_id:140194) is coercive and continuous, which in turn guarantees that the final linear system is [symmetric positive definite](@entry_id:139466) (for a symmetric DG method) and that the approximation is stable. For convergence, we also require that the [polynomial space](@entry_id:269905) $S_p$ is dense in the space of square-integrable functions of $\boldsymbol{\xi}$, a property guaranteed if the probability measure has finite moments of all orders .

### Non-Intrusive Methods: The Stochastic Collocation Approach

In contrast to the intrusive nature of the stochastic Galerkin method, **non-intrusive methods** treat the deterministic PDE solver as a "black box". They do not require modification of the underlying code. The **[stochastic collocation](@entry_id:174778) method** is a prominent example of this philosophy.

The procedure is conceptually straightforward :
1.  **Sample:** Choose a set of nodes $\{\boldsymbol{\xi}^{(j)}\}_{j=1}^M$ in the random [parameter space](@entry_id:178581) $\Gamma$. The choice of these nodes is critical for accuracy and efficiency, with common choices being roots of orthogonal polynomials (for tensor-product grids) or points from sparse-grid constructions.
2.  **Solve:** For each node $\boldsymbol{\xi}^{(j)}$, solve the deterministic PDE using the existing solver (e.g., a DG code). This yields a set of "snapshot" solutions $u_h(x; \boldsymbol{\xi}^{(j)})$. These solves are completely independent and can be run in parallel.
3.  **Reconstruct:** Use the computed solutions (or quantities of interest derived from them, $q(\boldsymbol{\xi}^{(j)})$) to construct a global [polynomial approximation](@entry_id:137391) $q_{\text{SC}}(\boldsymbol{\xi})$ in the gPC space $\Pi_p$.

The reconstruction step is typically achieved via [polynomial interpolation](@entry_id:145762). If the number of collocation nodes $M$ equals the dimension of the [polynomial space](@entry_id:269905) $N$, and the nodes form a **unisolvent** set (meaning any polynomial in $\Pi_p$ that is zero at all nodes must be the zero polynomial), then there exists a unique interpolant $q_{\text{SC}}(\boldsymbol{\xi}) \in \Pi_p$ that matches the computed values exactly at the nodes. A key property is that this interpolation is exact if the true quantity of interest $q(\boldsymbol{\xi})$ is itself a polynomial in $\Pi_p$ .

Alternatively, the gPC coefficients can be computed via a **pseudospectral approach**, where the integral in the [projection formula](@entry_id:152164) $c_\alpha = \mathbb{E}[q(\boldsymbol{\xi}) \Psi_\alpha(\boldsymbol{\xi})]$ is approximated by a [numerical quadrature](@entry_id:136578) rule whose points are the collocation nodes. If $q \in \Pi_p$, the integrand $q \Psi_\alpha$ is a polynomial of degree at most $2p$. A [quadrature rule](@entry_id:175061) that is exact for such polynomials will compute the gPC coefficients exactly .

The primary advantage of [stochastic collocation](@entry_id:174778) is its ease of implementation, as it leverages existing, highly optimized deterministic solvers. The main distinction from intrusive methods is the complete [decoupling](@entry_id:160890) of the deterministic solves, avoiding the need to formulate and solve a large, monolithic system .