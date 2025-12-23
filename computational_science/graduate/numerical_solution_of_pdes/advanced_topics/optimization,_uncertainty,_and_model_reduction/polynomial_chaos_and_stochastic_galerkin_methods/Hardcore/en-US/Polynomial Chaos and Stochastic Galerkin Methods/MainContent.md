## Introduction
In the world of computational science and engineering, models are often plagued by uncertainty. From material properties and environmental conditions to geometric imperfections, many parameters in systems governed by partial differential equations (PDEs) are not known with certainty. Ignoring this uncertainty can lead to unreliable predictions and flawed designs. The Polynomial Chaos (PC) expansion and the associated Stochastic Galerkin (SG) method provide a powerful and rigorous mathematical framework for propagating these input uncertainties through a model to quantify their impact on the system's response. This approach moves beyond simple Monte Carlo sampling by treating randomness as a fundamental dimension of the problem, enabling a more detailed and efficient analysis.

This article provides a comprehensive overview of PC and SG methods for graduate-level students and researchers. In the following chapters, you will embark on a journey from foundational theory to practical application. The first chapter, **"Principles and Mechanisms,"** delves into the core of the methodology, explaining how to represent random variables using orthogonal polynomial expansions and how to apply a Galerkin projection to transform a stochastic PDE into a solvable, [deterministic system](@entry_id:174558). The second chapter, **"Applications and Interdisciplinary Connections,"** showcases the versatility of these methods by exploring their use in diverse fields such as solid mechanics, [geosciences](@entry_id:749876), and fluid dynamics, highlighting their ability to tackle complex, real-world problems. Finally, the **"Hands-On Practices"** chapter provides a set of guided problems to bridge theory and implementation, allowing you to build and analyze your own stochastic solvers. By the end, you will have a solid understanding of how to use these advanced spectral techniques to bring a new level of statistical rigor to your computational models.

## Principles and Mechanisms

The conceptual foundation of Polynomial Chaos (PC) and Stochastic Galerkin (SG) methods lies in the application of [spectral theory](@entry_id:275351) to problems involving uncertainty. Where classical [spectral methods](@entry_id:141737) decompose a deterministic function into a basis of [orthogonal functions](@entry_id:160936) (e.g., a Fourier series), PC methods extend this paradigm to the space of random variables. This chapter delineates the foundational principles of this extension, from the representation of random quantities to the formulation and solution of [stochastic partial differential equations](@entry_id:188292) (PDEs).

### Representing Randomness: The Polynomial Chaos Expansion

At the heart of [uncertainty quantification](@entry_id:138597) is the need to represent [functions of random variables](@entry_id:271583), or [stochastic processes](@entry_id:141566), in a computationally tractable manner. The natural mathematical setting for this is a probability space $(\Omega, \mathcal{F}, \mathbb{P})$, and we focus on the Hilbert space $L^2(\Omega)$ of real-valued random variables $X$ with [finite variance](@entry_id:269687), i.e., for which the second moment is finite: $\mathbb{E}[X^2]  \infty$. This space is endowed with an inner product defined by the expectation of the product of two random variables:
$$
\langle X, Y \rangle_{L^2(\Omega)} = \mathbb{E}[X Y] = \int_{\Omega} X(\omega) Y(\omega) \, d\mathbb{P}(\omega)
$$

The central idea of Polynomial Chaos is to represent a random variable of interest, say $u(\boldsymbol{\xi})$, which depends on a vector of underlying random parameters $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$, as an infinite [series expansion](@entry_id:142878) in a [basis of polynomials](@entry_id:148579) that are orthogonal with respect to the probability measure of $\boldsymbol{\xi}$. This is the **Polynomial Chaos Expansion (PCE)**:
$$
u(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} u_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
Here, $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ is a multi-index, $\{\Psi_{\boldsymbol{\alpha}}\}_{\boldsymbol{\alpha} \in \mathbb{N}_0^d}$ is a basis of multivariate polynomials, and $\{u_{\boldsymbol{\alpha}}\}$ are deterministic coefficients. The key property is that the basis polynomials are chosen to be **orthonormal** with respect to the inner product induced by the probability measure of $\boldsymbol{\xi}$. Let $\rho(\boldsymbol{\xi})$ be the [joint probability density function](@entry_id:177840) (PDF) of $\boldsymbol{\xi}$. The [orthonormality](@entry_id:267887) condition is:
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \int_{\mathbb{R}^d} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
where $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the multidimensional Kronecker delta.

This [orthonormality](@entry_id:267887) provides an elegant and efficient way to determine the expansion coefficients $u_{\boldsymbol{\alpha}}$. By taking the inner product of the PCE with a basis function $\Psi_{\boldsymbol{\beta}}$, we exploit the orthogonality to isolate the coefficient $u_{\boldsymbol{\beta}}$:
$$
\langle u, \Psi_{\boldsymbol{\beta}} \rangle = \left\langle \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} u_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \right\rangle = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} u_{\boldsymbol{\alpha}} \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} u_{\boldsymbol{\alpha}} \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} = u_{\boldsymbol{\beta}}
$$
Thus, each coefficient is simply the projection of the function $u$ onto the corresponding basis polynomial:
$$
u_{\boldsymbol{\alpha}} = \mathbb{E}[u(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$

For numerical computation, the [infinite series](@entry_id:143366) must be truncated. A common strategy is **total-degree truncation**, where the expansion is limited to polynomials whose multi-indices $\boldsymbol{\alpha}$ have a total degree $|\boldsymbol{\alpha}| = \sum_{i=1}^d \alpha_i$ no greater than a chosen integer $p$. The finite approximation becomes $u_p(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} u_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$, where the [index set](@entry_id:268489) is $\mathcal{A} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : |\boldsymbol{\alpha}| \le p \}$. As a concrete example, consider the function $u(\boldsymbol{\xi}) = \exp(\lambda \xi_1 + \mu \xi_2)$ where $\xi_1, \xi_2$ are independent standard normal variables. Using a basis of orthonormal Hermite polynomials and a total degree of $p=3$, one can compute coefficients such as $u_{(2,1)}$ directly via the projection integral .

A fundamental requirement for this [spectral representation](@entry_id:153219) to be valid is that the chosen polynomial basis must be **complete** in the [function space](@entry_id:136890) of interest, which is the space of all square-[integrable functions](@entry_id:191199) of $\boldsymbol{\xi}$, denoted $L^2(\sigma(\boldsymbol{\xi}))$. Completeness ensures that any such function can be approximated to arbitrary accuracy by a finite polynomial expansion. Fortunately, for many probability measures encountered in practice, this condition holds. For measures with [compact support](@entry_id:276214) (e.g., the Uniform distribution), completeness is guaranteed by the Stone-Weierstrass theorem. For certain measures on non-compact domains, such as the Gaussian measure, completeness of the corresponding classical polynomials (Hermite polynomials) is a cornerstone of functional analysis. The completeness also extends to tensor products for independent variables and to [discrete measures](@entry_id:183686) on a finite number of points .

### Constructing Orthonormal Polynomial Bases

The choice of the basis $\{\Psi_{\boldsymbol{\alpha}}\}$ is not arbitrary; it must be tailored to the probability distribution of the random inputs $\boldsymbol{\xi}$ to ensure orthogonality. The construction strategy depends critically on the [statistical dependence](@entry_id:267552) between the components of $\boldsymbol{\xi}$.

#### The Independent Case: Tensor Products and the Wiener-Askey Scheme

The simplest and most common scenario is when the random inputs $\xi_1, \dots, \xi_d$ are mutually **statistically independent**. In this case, their joint PDF factors into the product of the marginal PDFs: $\rho(\boldsymbol{\xi}) = \prod_{i=1}^d \rho_i(\xi_i)$. This [statistical independence](@entry_id:150300) has a profound consequence: it allows the multivariate inner product to be factorized into a product of one-dimensional integrals.

This separability enables the construction of the multivariate orthonormal basis $\{\Psi_{\boldsymbol{\alpha}}\}$ as a simple tensor product of univariate orthonormal polynomials $\{\psi_k^{(i)}\}$, where each univariate family is orthogonal with respect to its corresponding marginal measure $\rho_i(\xi_i)$:
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i), \quad \text{where } \mathbb{E}[\psi_k^{(i)}(\xi_i) \psi_j^{(i)}(\xi_i)] = \int_{\mathbb{R}} \psi_k^{(i)}(t) \psi_j^{(i)}(t) \rho_i(t) \, dt = \delta_{kj}
$$
The [orthonormality](@entry_id:267887) of this tensor-product basis with respect to the joint measure is a direct consequence of this factorization :
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}\left[\prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i) \psi_{\beta_i}^{(i)}(\xi_i)\right] = \prod_{i=1}^d \mathbb{E}[\psi_{\alpha_i}^{(i)}(\xi_i) \psi_{\beta_i}^{(i)}(\xi_i)] = \prod_{i=1}^d \delta_{\alpha_i \beta_i} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$

The theory of [orthogonal polynomials](@entry_id:146918) provides a canonical mapping between [common probability distributions](@entry_id:171827) and families of [classical orthogonal polynomials](@entry_id:192726). This correspondence is known as the **Wiener-Askey scheme** for generalized Polynomial Chaos (gPC). The scheme is based on matching the support and weight function of a classical polynomial family with the support and PDF of the random variable. Key pairings include :
- **Gaussian Distribution** ($\mathcal{N}(0,1)$): The PDF is proportional to the weight function $w(\xi) = \exp(-\xi^2/2)$ on $(-\infty, \infty)$, which corresponds to the **probabilists' Hermite polynomials** $He_n(\xi)$.
- **Uniform Distribution** ($\mathcal{U}(-1,1)$): The PDF is constant on $[-1,1]$, matching the weight $w(\xi)=1$ for **Legendre polynomials** $P_n(\xi)$.
- **Gamma Distribution** ($\Gamma(k, \theta)$): The PDF is proportional to $\xi^{k-1}\exp(-\xi/\theta)$ on $[0, \infty)$, matching the weight for **generalized Laguerre polynomials** $L_n^{(k-1)}(\xi/\theta)$.

#### The Dependent Case: Custom Basis Construction

When the random inputs are **statistically dependent**, the joint PDF $\rho(\boldsymbol{\xi})$ does not factorize. Consequently, the multivariate inner product is no longer separable, and the tensor-product basis constructed from marginal-based polynomials is **not** orthogonal with respect to the joint measure  . For example, the inner product of two different tensor-product basis functions, such as $\psi_{(1,0)}(\boldsymbol{\xi})$ and $\psi_{(0,1)}(\boldsymbol{\xi})$, may be non-zero as it equates to a covariance term that reflects the dependence between the variables.

In this more general case, a valid [orthonormal basis](@entry_id:147779) must be constructed directly for the joint measure $\rho(\boldsymbol{\xi})$. The standard method is to apply the **Gram-Schmidt [orthogonalization](@entry_id:149208) process** to a basis of simple multivariate polynomials, typically the monomials $m_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \xi_i^{\alpha_i}$. The steps are as follows :
1.  Choose an ordered sequence of [linearly independent](@entry_id:148207) monomials (e.g., ordered by total degree, then lexicographically).
2.  Iteratively construct the [orthonormal basis](@entry_id:147779) $\{\Psi_{\boldsymbol{\alpha}}\}$ by orthogonalizing each monomial against the previously constructed basis functions and then normalizing the result.

This process is algorithmically straightforward but has a critical prerequisite: it requires the ability to compute inner products of arbitrary polynomials with respect to the joint measure $\rho$. This ultimately reduces to needing the values of all **mixed moments** of the random vector $\boldsymbol{\xi}$ up to a certain order:
$$
\mathbb{E}[\xi_1^{i_1} \xi_2^{i_2} \dots \xi_d^{i_d}] = \int_{\mathbb{R}^d} \xi_1^{i_1} \dots \xi_d^{i_d} \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi}
$$
In matrix terms, the Gram-Schmidt process is equivalent to performing a Cholesky factorization $G = LL^\top$ of the Gram matrix $G$ whose entries are the inner products of the monomials, $G_{\boldsymbol{\alpha}\boldsymbol{\beta}} = \langle m_{\boldsymbol{\alpha}}, m_{\boldsymbol{\beta}} \rangle_\rho = \mathbb{E}[m_{\boldsymbol{\alpha}} m_{\boldsymbol{\beta}}]$. The coefficients that transform the monomial basis to the [orthonormal basis](@entry_id:147779) are then found from the inverse of the Cholesky factor $L$ .

### The Stochastic Galerkin Method for PDEs

The true power of PCE is realized when it is used as a basis for a Galerkin method to solve stochastic PDEs. This "intrusive" approach transforms a PDE with random inputs into a coupled system of deterministic PDEs for the chaos coefficients.

Consider a generic linear elliptic PDE with a random diffusion coefficient $a(x, \boldsymbol{\xi})$:
$$
-\nabla \cdot (a(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi})) = f(x)
$$
The first step is to formulate the stochastic [weak form](@entry_id:137295) by multiplying by a [test function](@entry_id:178872) $v(x, \boldsymbol{\xi})$ and taking the expectation:
$$
\mathbb{E} \left[ \int_D a(x, \boldsymbol{\xi}) \nabla u(x, \boldsymbol{\xi}) \cdot \nabla v(x, \boldsymbol{\xi}) \, dx \right] = \mathbb{E} \left[ \int_D f(x) v(x, \boldsymbol{\xi}) \, dx \right]
$$
The **Stochastic Galerkin method** seeks an approximate solution $u_P = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} u_{\boldsymbol{\alpha}}(x) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ within the truncated [polynomial chaos](@entry_id:196964) subspace. This is achieved by testing the weak form against each basis function in that subspace, i.e., using test functions of the form $v(x, \boldsymbol{\xi}) = w(x) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})$ for each $\boldsymbol{\beta} \in \mathcal{A}$, where $w(x)$ is an arbitrary deterministic spatial test function.

Substituting the PCE for $u$ and the test function form for $v$, and also expanding the random coefficient $a(x, \boldsymbol{\xi})$ in a suitable polynomial basis $\{ \psi_k \}$, i.e., $a(x, \boldsymbol{\xi}) = \sum_k a_k(x) \psi_k(\boldsymbol{\xi})$, we arrive at a system of coupled deterministic PDEs for the coefficient functions $u_{\boldsymbol{\alpha}}(x)$ . For each $\boldsymbol{\beta} \in \mathcal{A}$, we have:
$$
\sum_k \sum_{\boldsymbol{\alpha} \in \mathcal{A}} \mathbb{E}[\psi_k(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] \int_D a_k(x) \nabla u_{\boldsymbol{\alpha}}(x) \cdot \nabla w(x) \, dx = \mathbb{E}[\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] \int_D f(x) w(x) \, dx
$$
The key observation is the emergence of the deterministic coefficients $C_{k\boldsymbol{\alpha}\boldsymbol{\beta}} = \mathbb{E}[\psi_k \Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}]$. These quantities are known as **triple products**. They are pure numbers that dictate the coupling between the different modes of the solution. The $\boldsymbol{\beta}$-th equation in the system depends on the unknown coefficient functions $u_{\boldsymbol{\alpha}}$ for all $\boldsymbol{\alpha}$ such that $C_{k\boldsymbol{\alpha}\boldsymbol{\beta}}$ is non-zero for some $k$.

The structure of this coupling is determined entirely by these triple products. For classical polynomial families associated with independent inputs, the triple products are very sparse. This is because these polynomials obey a [three-term recurrence relation](@entry_id:176845). This property can be used to derive **selection rules** that determine when a [triple product](@entry_id:195882) is non-zero. For example, for the orthonormal Hermite polynomials, the [triple product](@entry_id:195882) $\mathbb{E}[\Psi_m \Psi_n \Psi_p]$ is non-zero only if the sum of the indices $m+n+p$ is even and the indices satisfy the triangle inequalities ($m+n \ge p$, etc.). This can be elegantly derived using the generating function for the polynomials . This inherent sparsity is crucial, as it leads to a sparse or block-structured deterministic Galerkin system, which is computationally advantageous.

### Advanced Topics and Extensions

#### Handling Nonlinearities

When the PDE contains a nonlinear term, for instance a polynomial reaction term $r(u, \boldsymbol{\xi}) = \sum_q c_q(\boldsymbol{\xi}) u^q$, the Stochastic Galerkin projection leads to a more complex coupling. Projecting this term onto a [basis function](@entry_id:170178) $\Psi_m$ involves computing the expectation $\mathbb{E}[r(u, \boldsymbol{\xi}) \Psi_m(\boldsymbol{\xi})]$.

Substituting the PCE for both $u$ and the random coefficients $c_q$, the term $u^q$ becomes a product of $q$ polynomial series. When the expectation is taken, this results in a high-order tensor of expected values of products of basis polynomials, e.g., $\mathbb{E}[\psi_p \psi_{i_1} \dots \psi_{i_q} \psi_m]$. The projected nonlinear term for mode $m$ becomes a multi-dimensional [discrete convolution](@entry_id:160939) of the solution's chaos coefficients $\{u_i\}$ . This operation densely couples the modes, which is a primary source of computational complexity for nonlinear stochastic problems.

#### Numerical Implementation and Aliasing

In practice, the [multidimensional integrals](@entry_id:184252) required for the Galerkin projections (such as the triple products) are computed via [numerical quadrature](@entry_id:136578), typically Gauss quadrature. When dealing with nonlinear terms, this introduces a subtle but significant source of error known as **aliasing**.

The product of two polynomials from the truncated basis, e.g., $\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}$ where $|\boldsymbol{\alpha}|, |\boldsymbol{\beta}| \le p$, is a polynomial of higher degree. If the quadrature rule is not exact for the full integrand (e.g., $\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}\Psi_{\boldsymbol{\gamma}}$), the energy from the unresolvable high-frequency part of the product is "aliased" or incorrectly projected back onto the resolved modes $\{\Psi_{\boldsymbol{\gamma}}\}_{|\boldsymbol{\gamma}| \le p}$. This introduces a spurious transfer of energy that pollutes the computed coefficients.

This error can be eliminated by using a quadrature rule with a sufficiently high [degree of exactness](@entry_id:175703). For a term like $u_p^m$, where $u_p$ has degree $p$, the product $u_p^m \psi_{\ell}$ (for $\ell \le p$) has a maximum degree of $mp+p$. A Gauss-Legendre rule with $N_q$ points is exact for polynomials up to degree $2N_q-1$. To completely avoid [aliasing](@entry_id:146322), one must choose $N_q$ such that $2N_q - 1 \ge mp+p$. This [de-aliasing](@entry_id:748234) strategy, known as over-integration, requires choosing $N_q \ge \lceil(p(m+1)+1)/2\rceil$ points, which can significantly increase computational cost but is necessary for accuracy .

#### Post-processing: Global Sensitivity Analysis

A major benefit of computing a PCE is that it provides a full probabilistic representation of the solution, from which a wealth of [statistical information](@entry_id:173092) can be extracted at negligible cost. A primary application is **Global Sensitivity Analysis (GSA)**, which aims to apportion the output variance to the different input random variables.

The PCE is mathematically equivalent to the **Analysis of Variance (ANOVA)** or **Hoeffding-Sobol decomposition**. The total variance of the quantity of interest $Q(\boldsymbol{\xi})$ can be decomposed into contributions from individual variables and their interactions. For an orthonormal PCE, this decomposition is remarkably simple:
$$
\mathrm{Var}(Q) = \mathbb{E}[Q^2] - (\mathbb{E}[Q])^2 = \left(\sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}^2\right) - c_{\mathbf{0}}^2 = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}}^2
$$
The partial variance $V_u$ attributable to the set of variables $\boldsymbol{\xi}_u = \{\xi_i \mid i \in u\}$ is simply the sum of the squares of the coefficients whose polynomial basis functions depend *only* on that set of variables:
$$
V_u = \mathrm{Var}(\mathbb{E}[Q \mid \boldsymbol{\xi}_u] - \mathbb{E}[Q]) = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}, \, \mathrm{supp}(\boldsymbol{\alpha}) \subseteq u} c_{\boldsymbol{\alpha}}^2 - \sum_{\boldsymbol{\alpha} \neq \mathbf{0}, \, \mathrm{supp}(\boldsymbol{\alpha}) \subset u} c_{\boldsymbol{\alpha}}^2 = \sum_{\boldsymbol{\alpha} : \, \mathrm{supp}(\boldsymbol{\alpha}) = u} c_{\boldsymbol{\alpha}}^2
$$
Here, $\mathrm{supp}(\boldsymbol{\alpha}) = \{i \mid \alpha_i > 0\}$ is the set of indices of variables on which $\Psi_{\boldsymbol{\alpha}}$ depends.

From this decomposition, the **Sobol sensitivity indices** are computed directly. The first-order index $S_i$, which measures the main effect of $\xi_i$, and the total index $T_i$, which measures the main effect plus all interaction effects involving $\xi_i$, are given by :
$$
S_i = \frac{\sum_{\boldsymbol{\alpha}: \mathrm{supp}(\boldsymbol{\alpha}) = \{i\}} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \neq \mathbf{0}} c_{\boldsymbol{\beta}}^2}, \qquad T_i = \frac{\sum_{\boldsymbol{\alpha}: i \in \mathrm{supp}(\boldsymbol{\alpha})} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \neq \mathbf{0}} c_{\boldsymbol{\beta}}^2}
$$
For instance, given a set of computed coefficients, one can calculate that the first-order Sobol index for the first variable, $S_{\{1\}}$, is $\frac{29}{65}$ by summing the squared coefficients of modes depending only on $\xi_1$ and dividing by the total variance . This capability to perform a complete sensitivity analysis as a simple post-processing step is one of the most compelling features of the Polynomial Chaos methodology.