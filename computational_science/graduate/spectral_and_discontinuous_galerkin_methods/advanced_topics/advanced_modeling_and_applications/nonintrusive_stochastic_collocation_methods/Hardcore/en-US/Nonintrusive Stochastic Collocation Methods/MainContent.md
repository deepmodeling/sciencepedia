## Introduction
Computational models are indispensable tools in modern science and engineering, yet their predictive power is often limited by uncertainty in input parameters, boundary conditions, and model forms. Quantifying the impact of these uncertainties—a field known as Uncertainty Quantification (UQ)—is critical for creating reliable and robust simulations. However, applying UQ to complex, large-scale legacy codes presents a major challenge, as traditional intrusive methods require deep and often impractical modifications to the solver's source code. Nonintrusive [stochastic collocation](@entry_id:174778) (NISC) methods emerge as a powerful and flexible solution to this problem, offering a "black-box" approach that decouples the UQ framework from the deterministic solver.

This article provides a thorough exploration of NISC, designed to guide the reader from fundamental concepts to advanced applications. We will begin in the first chapter, **Principles and Mechanisms**, by dissecting the nonintrusive paradigm, contrasting it with intrusive approaches, and detailing the theoretical machinery of generalized Polynomial Chaos expansions and their numerical construction. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the method's versatility by exploring its use in [computational physics](@entry_id:146048), fluid dynamics, and its integration with adaptive solvers and optimization frameworks. Finally, the **Hands-On Practices** chapter will offer a set of guided problems to reinforce theoretical understanding and bridge the gap to practical implementation, enabling you to apply these powerful techniques in your own work.

## Principles and Mechanisms

Nonintrusive [stochastic collocation](@entry_id:174778) (NISC) methods represent a powerful and flexible paradigm for propagating uncertainty through complex computational models. Having introduced the general context of uncertainty quantification, this chapter delves into the foundational principles and operative mechanisms of NISC. We will explore how these methods construct accurate approximations of a system's response to random inputs without requiring modification of the underlying deterministic solver, a feature that makes them exceptionally versatile in scientific and engineering practice.

### The Nonintrusive Paradigm: A Black-Box Approach

At the heart of nonintrusive methods is the treatment of the deterministic solver—the complex code that computes the system's response for a fixed set of input parameters—as a "black box." The method only requires the ability to execute the solver for chosen input parameter values and retrieve the corresponding output. This stands in stark contrast to **intrusive** methods, such as the intrusive stochastic Galerkin method.

To formalize this distinction, consider a parametric model where a scalar quantity of interest (QoI), denoted $Q(\boldsymbol{\xi})$, depends on the solution of a deterministic partial differential equation (PDE) that has been discretized by a method such as the Finite Element (FE) method or Discontinuous Galerkin (DG). The vector $\boldsymbol{\xi} \in \mathbb{R}^d$ represents the random inputs.

A **[nonintrusive stochastic collocation](@entry_id:752627)** method approximates the map $\boldsymbol{\xi} \mapsto Q(\boldsymbol{\xi})$ as follows:
1.  A [finite set](@entry_id:152247) of $N$ specific points in the [parameter space](@entry_id:178581), called **collocation nodes** $\{\boldsymbol{\xi}^{(k)}\}_{k=1}^N$, are selected.
2.  The original, unmodified deterministic solver is executed $N$ times, once for each node $\boldsymbol{\xi}^{(k)}$, to produce $N$ corresponding output values, $\{Q(\boldsymbol{\xi}^{(k)})\}_{k=1}^N$.
3.  These input-output pairs are used to construct a functional approximation, or **surrogate model**, $\widehat{Q}(\boldsymbol{\xi})$, typically a multivariate polynomial, that interpolates the computed data.

Crucially, each of the $N$ solver runs is completely independent of the others. The algebraic systems solved at each node are decoupled, making the process "[embarrassingly parallel](@entry_id:146258)." No modification to the deterministic solver's source code is necessary.

Conversely, an **intrusive stochastic Galerkin** method reformulates the governing PDE itself to account for the randomness *before* [discretization](@entry_id:145012). This typically involves expanding the solution in a basis of functions of the random variables (e.g., a Polynomial Chaos Expansion). Applying a Galerkin projection in the stochastic space transforms the single stochastic PDE into a large, coupled system of deterministic PDEs for the expansion coefficients. Discretizing this coupled system results in a single, monolithic block algebraic system. Solving this system requires significant modification of the original deterministic solver to assemble and handle the global coupling between stochastic modes .

The nonintrusive nature of [collocation methods](@entry_id:142690) is their defining advantage, allowing them to be wrapped around existing, highly complex, and validated legacy codes with minimal effort. The remainder of this chapter focuses exclusively on the principles of this nonintrusive approach.

### Surrogate Modeling with Generalized Polynomial Chaos

The primary goal of NISC is to construct a surrogate model $\widehat{Q}(\boldsymbol{\xi})$ that accurately and efficiently approximates the true QoI map $Q(\boldsymbol{\xi})$. While various types of surrogates exist, the most common in this context are based on polynomials, leading to what is known as a **generalized Polynomial Chaos (gPC)** expansion.

#### The Role of Orthogonality: The Wiener-Askey Scheme

To build an efficient polynomial representation, we choose a [basis of polynomials](@entry_id:148579) that are orthogonal with respect to the probability measure of the random inputs. Let $\boldsymbol{\xi}$ be a random vector with [joint probability density function](@entry_id:177840) (PDF) $\rho(\boldsymbol{\xi})$ defined on a domain $\Gamma \subset \mathbb{R}^d$. We define a weighted [inner product for functions](@entry_id:176307) in the space $L^2_\rho(\Gamma)$ as:
$$
\langle f, g \rangle_\rho \equiv \int_\Gamma f(\boldsymbol{\xi})\, g(\boldsymbol{\xi})\, \rho(\boldsymbol{\xi})\, \mathrm{d}\boldsymbol{\xi} = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})]
$$
where $\mathbb{E}[\cdot]$ denotes the expectation operator.

A set of polynomials $\{\psi_\alpha(\boldsymbol{\xi})\}$ is orthogonal with respect to this inner product if $\langle \psi_\alpha, \psi_\beta \rangle_\rho = C_\alpha \delta_{\alpha\beta}$ for some normalization constants $C_\alpha$, where $\delta_{\alpha\beta}$ is the Kronecker delta. If $C_\alpha=1$ for all $\alpha$, the basis is **orthonormal**.

The choice of the orthogonal polynomial family is dictated by the distribution of the random inputs. This correspondence, known as the **Wiener-Askey scheme**, provides a blueprint for selecting the [optimal basis](@entry_id:752971) for several common distributions. For independent random variables, the multivariate basis is formed by tensor products of univariate [orthogonal polynomials](@entry_id:146918). The fundamental pairings are :

-   **Uniform Distribution:** For a random variable $\xi \sim U[-1,1]$, the PDF is $\rho(\xi) = 1/2$. The corresponding orthogonal polynomials are the **Legendre polynomials** $P_n(\xi)$.
-   **Gaussian Distribution:** For a standard normal variable $\xi \sim \mathcal{N}(0,1)$, the PDF is $\rho(\xi) = (2\pi)^{-1/2}\exp(-\xi^2/2)$. The corresponding orthogonal polynomials are the **probabilists' Hermite polynomials** $\text{He}_n(\xi)$.
-   **Gamma Distribution:** For a variable $\xi \sim \mathrm{Gamma}(k, \theta)$, with shape $k$ and scale $\theta$, the PDF is $\rho(\xi) = (\Gamma(k)\theta^k)^{-1}\xi^{k-1}\exp(-\xi/\theta)$ on $[0, \infty)$. The associated orthogonal polynomials are the **generalized Laguerre polynomials**, with the specific form $L_n^{(k-1)}(\xi/\theta)$.

#### The gPC Expansion and Its Coefficients

Given an [orthonormal basis](@entry_id:147779) $\{\psi_\alpha(\boldsymbol{\xi})\}$, any function $Q \in L^2_\rho(\Gamma)$ can be formally represented by its gPC expansion:
$$
Q(\boldsymbol{\xi}) = \sum_{\alpha \in \mathbb{N}_0^d} \hat{q}_\alpha \psi_\alpha(\boldsymbol{\xi})
$$
The coefficients $\hat{q}_\alpha$, often called [modal coefficients](@entry_id:752057), are determined by projecting $Q$ onto the basis functions. Thanks to [orthonormality](@entry_id:267887), this is simply the inner product:
$$
\hat{q}_\alpha = \langle Q, \psi_\alpha \rangle_\rho = \int_\Gamma Q(\boldsymbol{\xi}) \psi_\alpha(\boldsymbol{\xi}) \rho(\boldsymbol{\xi})\, \mathrm{d}\boldsymbol{\xi} = \mathbb{E}[Q(\boldsymbol{\xi})\psi_\alpha(\boldsymbol{\xi})]
$$
In practice, this [infinite series](@entry_id:143366) must be truncated. A common choice is to include all polynomials up to a certain total degree $P$, resulting in a finite approximation:
$$
Q(\boldsymbol{\xi}) \approx Q_P(\boldsymbol{\xi}) = \sum_{|\alpha| \le P} \hat{q}_\alpha \psi_\alpha(\boldsymbol{\xi})
$$
where $|\alpha| = \sum_{i=1}^d \alpha_i$ is the total degree of the multivariate polynomial $\psi_\alpha$.

To make this concrete, let's consider a simple stochastic PDE . Consider the 1D diffusion problem $-(a(\xi)u_x)_x = 1$ on $x \in (0,1)$ with zero Dirichlet boundary conditions. The diffusion coefficient is random, given by $a(\xi) = \exp(\alpha\xi)$, where $\xi \sim \mathcal{N}(0,1)$ is a standard Gaussian random variable. The exact solution for a fixed $\xi$ is $u(x;\xi) = \frac{x-x^2}{2a(\xi)} = \frac{x-x^2}{2}\exp(-\alpha\xi)$. For a fixed spatial location $x_0$, the QoI is $Q(\xi) = u(x_0;\xi)$. Since the input is Gaussian, we use an orthonormal Hermite basis $\{\phi_n(\xi)\}$. The coefficients of the gPC expansion are given by the projection integral $c_n(x_0) = \mathbb{E}[u(x_0;\xi) \phi_n(\xi)]$. By leveraging the generating function for Hermite polynomials, one can derive the exact analytical expression for these coefficients:
$$
c_n(x_0) = \frac{(x_0-x_0^2)(-\alpha)^n}{2\sqrt{n!}}\exp\left(\frac{\alpha^2}{2}\right)
$$
This example illustrates how the coefficients encode the parametric dependence of the solution. In most realistic problems, however, neither the solution $u$ nor the integral for the coefficients can be computed analytically. Nonintrusive methods provide numerical strategies to compute these coefficients.

### Numerical Computation of gPC Coefficients

There are two primary nonintrusive strategies for numerically determining the truncated set of gPC coefficients $\{\hat{q}_\alpha\}_{|\alpha| \le P}$: **pseudo-[spectral projection](@entry_id:265201)** and **interpolation-based collocation**.

#### Pseudo-Spectral Projection via Quadrature

The pseudo-[spectral projection](@entry_id:265201) method directly approximates the integral defining each coefficient $\hat{q}_\alpha$. A [numerical quadrature](@entry_id:136578) rule with nodes $\{\boldsymbol{\xi}^{(j)}\}_{j=1}^{N_q}$ and weights $\{w_j\}_{j=1}^{N_q}$ is used:
$$
\hat{q}_\alpha = \int_\Gamma Q(\boldsymbol{\xi}) \psi_\alpha(\boldsymbol{\xi}) \rho(\boldsymbol{\xi})\, \mathrm{d}\boldsymbol{\xi} \approx \sum_{j=1}^{N_q} Q(\boldsymbol{\xi}^{(j)}) \psi_\alpha(\boldsymbol{\xi}^{(j)}) w_j
$$
This approach requires evaluating the QoI $Q$ and the basis polynomials $\psi_\alpha$ at the quadrature nodes. The key to the efficiency and accuracy of this method lies in using **Gaussian quadrature** rules. A univariate $N$-point Gaussian quadrature rule constructed for the weight function $\rho(\xi)$ is exact for any integrand that is a product of $\rho(\xi)$ and a polynomial of degree up to $2N-1$.

This exactness property is critical for computing gPC coefficients. Suppose the true QoI map $Q(\boldsymbol{\xi})$ is a polynomial of total degree at most $M$. To compute the coefficient $\hat{q}_\alpha$ exactly, the [quadrature rule](@entry_id:175061) must exactly integrate the product $Q(\boldsymbol{\xi})\psi_\alpha(\boldsymbol{\xi})$, which is a polynomial. The degree of this product is at most $M + |\alpha|$. To compute all coefficients up to total degree $P$, the [quadrature rule](@entry_id:175061) must be exact for polynomials of degree up to $M+P$ .

This leads to specific requirements on the number of quadrature points . For example:
-   **Computing Moments:** To compute the variance $\sigma^2 = \mathbb{E}[Q^2] - (\mathbb{E}[Q])^2$ exactly for a polynomial QoI $Q \in \mathbb{P}_M$, we need to compute two integrals. The integrand for $\mathbb{E}[Q]$ is $Q$ (degree $M$), while the integrand for $\mathbb{E}[Q^2]$ is $Q^2$ (degree $2M$). To get both exact with an $N$-point Gaussian quadrature, the stricter condition must hold: $2N-1 \ge 2M$.
-   **Computing gPC Coefficients:** To compute coefficients $\hat{q}_\alpha$ for $|\alpha| \le P$ for a QoI $Q \in \mathbb{P}_M$, the integrand has maximum degree $M+P$. Thus, we require $2N-1 \ge M+P$. In the univariate case, this implies we need at least $N = \lceil (M+P+1)/2 \rceil$ points. If $Q$ itself is represented by a degree $P$ polynomial, we need $2N-1 \ge 2P$, or $N \ge P+1$ points  .

The choice of [quadrature rule](@entry_id:175061) must match the input probability distribution. For instance, Gauss-Legendre quadrature is used for uniform inputs, and Gauss-Hermite for Gaussian inputs. Using a mismatched rule, such as Gauss-Legendre for an integral over $\mathbb{R}$ with a Gaussian weight, would introduce significant errors (e.g., domain [truncation error](@entry_id:140949)) and would not achieve the rapid convergence of the appropriate rule .

#### Interpolation-based Collocation

An alternative approach is to first construct a polynomial interpolant of $Q(\boldsymbol{\xi})$ and then derive its gPC coefficients. This method is based on the algebra of polynomial interpolation rather than [numerical integration](@entry_id:142553)  .

Let $\mathcal{P}_P^d$ be the space of multivariate polynomials in $d$ variables with total degree at most $P$. The dimension of this space is $N_{dim} = \binom{P+d}{d}$. An **interpolating polynomial** $\widehat{Q}(\boldsymbol{\xi}) \in \mathcal{P}_P^d$ is constructed to match the true QoI at a set of $N_{dim}$ collocation nodes $\{\boldsymbol{\xi}^{(j)}\}_{j=1}^{N_{dim}}$:
$$
\widehat{Q}(\boldsymbol{\xi}^{(j)}) = Q(\boldsymbol{\xi}^{(j)}) \quad \text{for } j=1, \dots, N_{dim}
$$
For this to define a unique polynomial, the node set must be **unisolvent** for the space $\mathcal{P}_P^d$. This means that the generalized Vandermonde matrix associated with the nodes and a basis for $\mathcal{P}_P^d$ is invertible.

Given a unisolvent set, we can define a unique **Lagrange basis** $\{\ell_j(\boldsymbol{\xi})\}_{j=1}^{N_{dim}} \subset \mathcal{P}_P^d$ with the property $\ell_j(\boldsymbol{\xi}^{(k)}) = \delta_{jk}$. The unique [interpolating polynomial](@entry_id:750764) is then given explicitly by:
$$
\widehat{Q}(\boldsymbol{\xi}) = \sum_{j=1}^{N_{dim}} Q(\boldsymbol{\xi}^{(j)}) \ell_j(\boldsymbol{\xi})
$$
A fundamental property of [polynomial interpolation](@entry_id:145762) is its [exactness](@entry_id:268999): if the true function $Q(\boldsymbol{\xi})$ is itself a polynomial in the interpolation space (i.e., $Q \in \mathcal{P}_P^d$), then its unique interpolant is the function itself: $\widehat{Q}(\boldsymbol{\xi}) \equiv Q(\boldsymbol{\xi})$. This follows because $Q$ itself satisfies the interpolation conditions and is in the correct space, and uniqueness allows for no other solution.

Once the interpolant $\widehat{Q}(\boldsymbol{\xi})$ is constructed, its coefficients in the gPC basis $\{\psi_\alpha\}$ can be found by a simple [change of basis](@entry_id:145142). This involves solving a linear system that maps the nodal values $\{Q(\boldsymbol{\xi}^{(j)})\}$ to the [modal coefficients](@entry_id:752057) $\{\hat{q}_\alpha\}$. Crucially, if $Q \in \mathcal{P}_P^d$, this process recovers the exact gPC coefficients of $Q$ without relying on any quadrature rule exactness . If $Q$ is not a polynomial of degree at most $P$, [aliasing](@entry_id:146322) errors will occur.

### Practical Implementation and Extensions

#### From Surrogate to Statistics

Once the gPC surrogate $\widehat{Q}(\boldsymbol{\xi}) = \sum_{|\alpha| \le P} \hat{q}_\alpha \psi_\alpha(\boldsymbol{\xi})$ is constructed (by either projection or interpolation), it provides a complete, albeit approximate, statistical characterization of the QoI. Moments and other statistical quantities can be computed analytically and cheaply from the gPC coefficients. Due to the [orthonormality](@entry_id:267887) of the basis, the mean and variance are particularly simple:
-   **Mean:** $\mu_Q = \mathbb{E}[Q] \approx \mathbb{E}[\widehat{Q}] = \mathbb{E}\left[\sum \hat{q}_\alpha \psi_\alpha\right] = \sum \hat{q}_\alpha \mathbb{E}[\psi_\alpha] = \hat{q}_0$, since $\psi_0$ is constant and $\mathbb{E}[\psi_\alpha]=0$ for $|\alpha|>0$.
-   **Variance:** $\sigma^2_Q = \mathbb{E}[(Q-\mu_Q)^2] \approx \mathbb{E}[(\widehat{Q}-\hat{q}_0)^2] = \mathbb{E}\left[\left(\sum_{|\alpha|>0} \hat{q}_\alpha \psi_\alpha\right)^2\right] = \sum_{|\alpha|>0} \hat{q}_\alpha^2$.

Similarly, if one has access to samples of the QoI's sensitivity with respect to a deterministic parameter, say $\frac{\partial Q}{\partial a}$, one can construct a gPC surrogate for this quantity as well. Assuming differentiation under the expectation is valid, the sensitivity of the mean can be computed as $\frac{d\mu_Q}{da} = \mathbb{E}\left[\frac{\partial Q}{\partial a}\right]$. This expectation can be approximated using the same quadrature rule applied to the sensitivity samples . For instance, given samples $\{J_k\}$ and $\{\frac{\partial J}{\partial a}|_k\}$ at four tensor-product Gauss-Legendre nodes for a 2D uniform input, the mean, variance, and sensitivity of the mean are approximated as:
$$
\mu \approx \frac{1}{4}\sum_{k=1}^4 J_k, \quad \sigma^2 \approx \left(\frac{1}{4}\sum_{k=1}^4 J_k^2\right) - \mu^2, \quad \frac{d\mu}{da} \approx \frac{1}{4}\sum_{k=1}^4 \frac{\partial J}{\partial a}\bigg|_k
$$

#### The Curse of Dimensionality and Sparse Grids

A major challenge for multivariate approximation is the **[curse of dimensionality](@entry_id:143920)**. The number of nodes required for interpolation or quadrature on a full tensor-product grid grows exponentially with the dimension $d$. Even for the more efficient total-degree [polynomial spaces](@entry_id:753582), the number of nodes required, $\binom{P+d}{d}$, grows polynomially in $d$ with degree $P$, which is often computationally prohibitive.

**Smolyak sparse grids** offer a powerful remedy for moderate dimensions ($d \lesssim 10$). The Smolyak construction method combines tensor products of univariate quadrature or interpolation rules of varying coarseness in a specific way to cancel out the leading error terms. The resulting grid has far fewer points than a full tensor-product grid of comparable accuracy.

A sparse grid at total level $a$ in $d$ dimensions is constructed as a union of smaller tensor-product grids. For instance, using nested univariate rules $\{X_i\}$, the Smolyak node set is $\mathcal{S}(a,d)=\bigcup_{\boldsymbol{i}\in \mathcal{I}(a,d)} ( X_{i_{1}} \times \cdots \times X_{i_{d}} )$, where $\mathcal{I}(a,d)$ is a carefully chosen set of multi-indices. Due to the [nestedness](@entry_id:194755) of the univariate rules ($X_i \subset X_{i+1}$), this union can be simplified, and the total number of distinct nodes can be calculated using the [principle of inclusion-exclusion](@entry_id:276055) . This construction provides a polynomial interpolant that is exact for a specific space of polynomials (the "[look-up table](@entry_id:167824)" space), balancing accuracy and computational cost far more effectively than full tensor grids.

### Convergence and Advanced Topics

#### Conditions for Rapid Convergence

The remarkable efficiency of spectral and [collocation methods](@entry_id:142690) stems from their potential for **[exponential convergence](@entry_id:142080)**. The convergence rate of the polynomial approximation error with increasing degree $P$ depends critically on the regularity of the QoI map $Q(\boldsymbol{\xi})$.

A cornerstone result of [approximation theory](@entry_id:138536) states that if the map $\boldsymbol{\xi} \mapsto Q(\boldsymbol{\xi})$ is **analytic** on the domain $\Gamma$ and can be extended to a larger region in the complex plane, the error of the gPC approximation (and related collocation schemes) decays exponentially with $P$. In the context of PDEs with random parameters, this analytic regularity of the QoI map is inherited from the problem data. If the PDE coefficients, source terms, and boundary conditions are [analytic functions](@entry_id:139584) of the parameter $\boldsymbol{\xi}$, and the PDE remains uniformly well-posed, then the solution map $\boldsymbol{\xi} \mapsto u(\cdot;\boldsymbol{\xi})$ is also analytic. Consequently, a QoI defined as a [continuous linear functional](@entry_id:136289) of the solution, $Q(\boldsymbol{\xi})=\ell(u(\cdot;\boldsymbol{\xi}))$, will also be analytic, and NISC methods will converge exponentially .

Conversely, if the map $Q(\boldsymbol{\xi})$ has limited smoothness, convergence is only **algebraic**. For instance, if $Q$ is only $r$ times continuously differentiable ($Q \in C^r(\Gamma)$), the error typically decays as $\mathcal{O}(P^{-r})$. A function with a "kink," such as $Q(\xi) = |\xi|$, is [continuous but not differentiable](@entry_id:261860) at $\xi=0$, and a global polynomial approximation will suffer from slow convergence and Gibbs-type oscillations near the singularity .

#### Handling Non-Smoothness: The Case of Hyperbolic PDEs

A significant challenge arises in problems where the solution's character changes discontinuously with the random parameters. A classic example is the solution of a nonlinear hyperbolic PDE, such as the inviscid Burgers' equation, with uncertain initial data.

Consider the Burgers' equation $u_t + (\frac{1}{2}u^2)_x = 0$ with an uncertain initial amplitude $u(x,0;\xi) = \xi f(x)$, where $\xi \sim U[0,1]$. For this equation, shocks (discontinuities in the physical solution $u$) can form in finite time. The [shock formation](@entry_id:194616) time $t_s$ depends inversely on the initial amplitude: $t_s(\xi) \propto 1/\xi$. For any fixed observation time $t > 0$, there exists a critical threshold $\xi^*$ such that for $\xi  \xi^*$, the solution at time $t$ is smooth (pre-shock), while for $\xi > \xi^*$, the solution is discontinuous (post-shock), governed by a different set of physical laws (the Rankine-Hugoniot condition).

This abrupt change in the physics causes the QoI map $Q(\xi) = u(x,t;\xi)$ to be only piecewise smooth in the stochastic variable $\xi$. The map develops a kink or [jump discontinuity](@entry_id:139886) at $\xi = \xi^*$. A global [polynomial approximation](@entry_id:137391) across the entire stochastic domain $[0,1]$ will fail to capture this feature accurately and will converge very slowly.

To overcome this, more advanced **Multi-Element Stochastic Collocation (MESC)** methods are required . The core idea is to partition the stochastic domain $\Gamma$ into sub-domains (elements) based on the locations of non-smoothness. In the Burgers' example, one would partition $[0,1]$ at $\xi^*$. Then, within each element, a separate, local high-order polynomial collocation is performed. By aligning the element boundaries with the physical regime changes, the map $Q(\xi)$ is smooth within each element, and local [exponential convergence](@entry_id:142080) can be restored. The global statistics are then recovered by combining the results from all elements, weighted appropriately by the probability measure of each element. This illustrates how the principles of NISC can be extended to tackle some of the most challenging problems in [uncertainty quantification](@entry_id:138597).