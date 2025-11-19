## Introduction
In modern engineering and computational science, accurately accounting for uncertainty is no longer a luxury but a necessity for robust design and reliable prediction. Material properties, geometric tolerances, and environmental loads are seldom perfectly known, and their variability can have a profound impact on system performance. While methods like Monte Carlo simulation provide a direct approach to propagating uncertainty, their computational cost can be prohibitive for the complex, high-fidelity models prevalent in fields like [solid mechanics](@entry_id:164042). This creates a critical knowledge gap: how can we efficiently quantify the impact of uncertainty in computationally demanding systems?

Polynomial Chaos Expansion (PCE) emerges as a powerful and elegant solution to this challenge. It is a non-sampling-based method that represents a model's response to random inputs as a spectral expansion in a basis of [orthogonal polynomials](@entry_id:146918). This transformation from a complex, often implicit, stochastic model into an explicit polynomial surrogate unlocks remarkable efficiencies in analysis. This article provides a graduate-level guide to the theory and application of PCE.

To achieve a comprehensive understanding, we will first delve into the theoretical foundations in **Principles and Mechanisms**, exploring the Hilbert space framework, the role of [orthogonal polynomials](@entry_id:146918), and the mechanics of constructing the expansion. Following this, **Applications and Interdisciplinary Connections** will demonstrate the method's practical power, showcasing its use in forward [uncertainty propagation](@entry_id:146574), the Stochastic Finite Element Method (SFEM), [reliability analysis](@entry_id:192790), and its connections to fields beyond [structural mechanics](@entry_id:276699). Finally, **Hands-On Practices** will ground the theory by guiding you through key derivations and problem setups, solidifying your ability to implement and utilize PCE for advanced analysis.

## Principles and Mechanisms

This chapter delves into the fundamental principles and operational mechanisms of the Polynomial Chaos Expansion (PCE) method. We will establish the theoretical framework that positions PCE as a powerful tool for [uncertainty quantification](@entry_id:138597), explore the construction of the expansion, and analyze its properties, including the extraction of [statistical information](@entry_id:173092), convergence behavior, and its limitations.

### Foundations: Uncertainty Representation in Hilbert Space

The theoretical underpinning of Polynomial Chaos Expansion is rooted in functional analysis, specifically the theory of Hilbert spaces. A random quantity of interest, such as the displacement or stress in a mechanical system with uncertain parameters, can be viewed as a function defined on a probability space. Let $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ be a vector of $d$ random variables representing the sources of uncertainty in a model. Let the [joint probability distribution](@entry_id:264835) of $\boldsymbol{\xi}$ be denoted by $\mathbb{P}_{\boldsymbol{\xi}}$. A scalar response quantity of the system, $Y$, can then be written as a function $Y(\boldsymbol{\xi})$.

For PCE to be applicable, this response function must be **square-integrable** with respect to the probability measure $\mathbb{P}_{\boldsymbol{\xi}}$. This means its second moment, or mean-square value, must be finite:
$$
\mathbb{E}[Y(\boldsymbol{\xi})^2] = \int Y(\boldsymbol{\xi})^2 \, d\mathbb{P}_{\boldsymbol{\xi}}  \infty
$$
The set of all such square-[integrable functions](@entry_id:191199) forms a Hilbert space, denoted $L^2(\mathbb{P}_{\boldsymbol{\xi}})$. This space is equipped with an inner product defined by the expectation of the product of two functions:
$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int f(\boldsymbol{\xi})g(\boldsymbol{\xi}) \, d\mathbb{P}_{\boldsymbol{\xi}}
$$

A fundamental theorem in Hilbert space theory states that any function within the space can be represented as an infinite series of basis functions. The **Generalized Polynomial Chaos Expansion (gPC)** is precisely such a representation, where the basis functions are multivariate polynomials $\{\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\}_{\boldsymbol{\alpha} \in \mathbb{N}_0^d}$ that are complete and orthonormal with respect to the inner product defined above. For any response $Y \in L^2(\mathbb{P}_{\boldsymbol{\xi}})$, there exist unique, deterministic coefficients $\{c_{\boldsymbol{\alpha}}\}$ such that:
$$
Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
where $\boldsymbol{\alpha}$ is a multi-index representing the degrees of the multivariate polynomial. The equality here is not necessarily pointwise, but is understood in the sense of convergence in the Hilbert space norm. This is known as **[mean-square convergence](@entry_id:137545)**. It means that as we include more terms in a truncated version of the series, denoted $Y_p(\boldsymbol{\xi}) = \sum_{|\boldsymbol{\alpha}| \le p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$, the [mean-square error](@entry_id:194940) approaches zero [@problem_id:2671647]:
$$
\lim_{p \to \infty} \|Y - Y_p\|_{L^2}^2 = \lim_{p \to \infty} \mathbb{E}\left[ \left( Y(\boldsymbol{\xi}) - \sum_{|\boldsymbol{\alpha}| \le p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \right)^2 \right] = 0
$$

This expansion transforms the complex, often implicit, relationship between the random inputs $\boldsymbol{\xi}$ and the response $Y$ into a standardized [series representation](@entry_id:175860), which proves to be remarkably convenient for analysis.

### The Building Blocks: Orthonormal Polynomials

The power and efficiency of PCE hinge on the property of **[orthonormality](@entry_id:267887)** of the basis polynomials, $\{\Psi_{\boldsymbol{\alpha}}\}$. A set of polynomials is orthonormal with respect to the probability measure of $\boldsymbol{\xi}$ if the inner product of any two distinct basis functions is zero (orthogonality) and the inner product of any [basis function](@entry_id:170178) with itself is one (normality). This is concisely expressed using the Kronecker delta, $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$:
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
If the random vector $\boldsymbol{\xi}$ has a [joint probability density function](@entry_id:177840) (PDF) $\rho(\boldsymbol{\xi})$, this condition can be written explicitly as an integral [@problem_id:2671685]:
$$
\int \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) \, d\boldsymbol{\xi} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$

A pivotal insight, formalized in the **Wiener-Askey scheme**, is that for many [common probability distributions](@entry_id:171827), families of [classical orthogonal polynomials](@entry_id:192726) naturally satisfy this condition. The PDF of the random variable acts as the weight function for which the polynomial family is orthogonal. The choice of basis is therefore not arbitrary; it must be matched to the distribution of the random inputs to achieve orthogonality. The most common pairings in this scheme are [@problem_id:2671718]:

-   **Gaussian (Normal) Distribution**: The corresponding [orthogonal polynomials](@entry_id:146918) are **Hermite polynomials**.
-   **Uniform Distribution**: On the interval $[-1, 1]$, the corresponding family is the **Legendre polynomials**.
-   **Gamma Distribution**: The corresponding family is the **Laguerre polynomials**.
-   **Beta Distribution**: The corresponding family is the **Jacobi polynomials**.

For a random input that is uniformly distributed on a general interval $[a, b]$, a simple affine transformation can map it to the canonical interval $[-1, 1]$, allowing for the use of Legendre polynomials [@problem_id:2671718].

When the input vector $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ consists of **independent** random variables, the joint PDF is a product of the marginal PDFs, $\rho(\boldsymbol{\xi}) = \prod_{k=1}^d \rho_k(\xi_k)$. In this crucial case, a multivariate [orthonormal basis](@entry_id:147779) can be constructed by the **[tensor product](@entry_id:140694)** of the univariate orthonormal polynomials $\{\psi_n^{(k)}\}$ corresponding to each component $\xi_k$:
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{k=1}^d \psi_{\alpha_k}^{(k)}(\xi_k), \quad \text{where } \boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)
$$
If the input variables are **correlated**, this [simple tensor](@entry_id:201624)-product construction is no longer valid. One must first apply an isoprobabilistic transformation (such as a Nataf or Rosenblatt transform) to map the correlated physical variables into a set of independent standardized variables, upon which the tensor-product basis can be built [@problem_id:2671718].

Some distributions do not have a corresponding classical polynomial family. A [lognormal distribution](@entry_id:261888) is a prominent example. However, if a variable $E$ is lognormal, its logarithm $G = \ln E$ is Gaussian. The standard procedure is to perform this transformation and build the PCE using Hermite polynomials of the underlying Gaussian variable $G$ [@problem_id:2671718].

### Constructing the Expansion: Coefficients and Truncation

Once an appropriate orthonormal basis is chosen, the next step is to determine the deterministic coefficients $c_{\boldsymbol{\alpha}}$ that define the expansion.

#### Calculating PCE Coefficients

The [orthonormality](@entry_id:267887) of the basis provides a straightforward method for calculating the coefficients via orthogonal projection. By taking the inner product of the full expansion with a [basis function](@entry_id:170178) $\Psi_{\boldsymbol{\beta}}$, we find:
$$
\langle Y, \Psi_{\boldsymbol{\beta}} \rangle = \left\langle \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \right\rangle = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}} = c_{\boldsymbol{\beta}}
$$
Thus, each coefficient is simply the projection of the [response function](@entry_id:138845) $Y$ onto the corresponding basis polynomial [@problem_id:2671647] [@problem_id:2671724]:
$$
c_{\boldsymbol{\alpha}} = \langle Y, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$
It is important to distinguish between an **orthogonal** basis and an **orthonormal** one. An [orthogonal basis](@entry_id:264024) $\{\tilde{\Psi}_{\boldsymbol{\alpha}}\}$ satisfies $\mathbb{E}[\tilde{\Psi}_{\boldsymbol{\alpha}} \tilde{\Psi}_{\boldsymbol{\beta}}] = \gamma_{\boldsymbol{\alpha}} \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, where $\gamma_{\boldsymbol{\alpha}} = \mathbb{E}[\tilde{\Psi}_{\boldsymbol{\alpha}}^2]$ are normalization constants not necessarily equal to one. The corresponding coefficients are then $\tilde{c}_{\boldsymbol{\alpha}} = \mathbb{E}[Y \tilde{\Psi}_{\boldsymbol{\alpha}}] / \gamma_{\boldsymbol{\alpha}}$. The two sets of coefficients are related by $c_{\boldsymbol{\alpha}} = \tilde{c}_{\boldsymbol{\alpha}} \sqrt{\gamma_{\boldsymbol{\alpha}}}$. The orthonormal formulation is often mathematically cleaner.

#### Truncation and the Curse of Dimensionality

In practice, the infinite series must be truncated to a finite number of terms for computation. A common and effective approach is the **total-degree truncation scheme**. For a chosen maximum polynomial degree $p$, this scheme retains all basis polynomials $\Psi_{\boldsymbol{\alpha}}$ for which the sum of the degrees in each variable does not exceed $p$. The corresponding multi-[index set](@entry_id:268489) is:
$$
\mathcal{A}_p = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \|\boldsymbol{\alpha}\|_1 = \sum_{i=1}^d \alpha_i \le p \right\}
$$
The total number of coefficients (and thus basis functions) in this set, denoted $|\mathcal{A}_p|$, can be determined by a [combinatorial argument](@entry_id:266316). This is equivalent to finding the number of ways to distribute $p$ items into $d+1$ bins (the $d$ variables plus one "slack" variable), a classic "[stars and bars](@entry_id:153651)" problem. The result is given by the [binomial coefficient](@entry_id:156066) [@problem_id:2671734]:
$$
|\mathcal{A}_p| = \binom{d+p}{d} = \frac{(d+p)!}{d! p!}
$$
This formula reveals a significant practical challenge: the number of terms grows polynomially with the degree $p$, but it grows much more rapidly with the number of random dimensions $d$. This rapid growth is a manifestation of the **[curse of dimensionality](@entry_id:143920)**, which can make PCE computationally expensive for problems with many uncertain parameters.

#### Numerical Calculation of Coefficients

The theoretical formula for the coefficients, $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$, involves a multi-dimensional integral over the [parameter space](@entry_id:178581). For all but the simplest cases, this integral cannot be solved analytically. **Non-intrusive** PCE methods treat the computational model of $Y(\boldsymbol{\xi})$ as a black box and approximate these integrals using [numerical quadrature](@entry_id:136578).

For independent input variables, a **tensor-product Gaussian quadrature** rule is highly effective. Given a set of $m_k$ quadrature nodes $\xi_{k,j}$ and weights $w_{k,j}$ for each dimension $k$, the $d$-dimensional integral is approximated by a weighted sum of model evaluations at the tensor-product grid of quadrature points. The approximation for a coefficient $c_{\boldsymbol{\alpha}}$ is [@problem_id:2671643]:
$$
c_{\boldsymbol{\alpha}} \approx \sum_{j_1=1}^{m_1} \cdots \sum_{j_d=1}^{m_d} Y(\xi_{1,j_1}, \dots, \xi_{d,j_d}) \prod_{k=1}^{d} \left( w_{k,j_k} \psi^{(k)}_{\alpha_k}(\xi_{k,j_k}) \right)
$$
The nodes and weights for Gaussian quadrature are specifically chosen to exactly integrate polynomials up to a high degree, making this a very efficient method for computing the PCE coefficients when $Y$ is a smooth function of $\boldsymbol{\xi}$.

### Exploiting the Expansion: Post-Processing for Statistical Insights

Once the PCE coefficients $\{c_{\boldsymbol{\alpha}}\}$ for a truncated expansion are computed, a wealth of [statistical information](@entry_id:173092) about the response $Y$ becomes available through simple algebraic manipulations of these coefficients. This is one of the most attractive features of PCE.

Assuming an [orthonormal basis](@entry_id:147779) $\{\Psi_{\boldsymbol{\alpha}}\}$ with the convention that $\Psi_{\boldsymbol{0}} \equiv 1$ is the constant polynomial, we can derive expressions for the primary statistical moments.

The **mean** or expected value of $Y$ is found by taking the expectation of the series. Due to the orthogonality of the basis polynomials, all terms except the first vanish:
$$
\mathbb{E}[Y] = \mathbb{E}\left[\sum_{\boldsymbol{\alpha} \in \mathcal{A}_p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right] = \sum_{\boldsymbol{\alpha} \in \mathcal{A}_p} c_{\boldsymbol{\alpha}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = c_{\boldsymbol{0}} \mathbb{E}[\Psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}
$$
The mean of the response is simply the zeroth-order coefficient [@problem_id:2671650] [@problem_id:2671724].

The **variance**, $\mathrm{Var}[Y] = \mathbb{E}[(Y - \mathbb{E}[Y])^2]$, can also be expressed in terms of the coefficients. Since $Y - \mathbb{E}[Y] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}$, we have:
$$
\mathrm{Var}[Y] = \mathbb{E}\left[\left(\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right) \left(\sum_{\boldsymbol{\beta} \neq \boldsymbol{0}} c_{\boldsymbol{\beta}} \Psi_{\boldsymbol{\beta}}\right)\right] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} \sum_{\boldsymbol{\beta} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} c_{\boldsymbol{\beta}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}]
$$
Using the [orthonormality](@entry_id:267887) condition $\mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, the double sum collapses, yielding:
$$
\mathrm{Var}[Y] = \sum_{\boldsymbol{\alpha} \in \mathcal{A}_p, \boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2
$$
The variance is the sum of the squares of all higher-order coefficients. This result provides a powerful decomposition of the total variance into contributions from different polynomial basis functions [@problem_id:2671650] [@problem_id:2671724]. Similarly, the covariance of two responses, $U$ and $V$, with PCE coefficients $\{c_{\boldsymbol{\alpha}}\}$ and $\{d_{\boldsymbol{\alpha}}\}$ in the same orthonormal basis, is given by [@problem_id:2671724]:
$$
\mathrm{Cov}[U, V] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} d_{\boldsymbol{\alpha}}
$$

**Example:** Consider a PCE for the tip displacement of a bar with coefficients (in an [orthonormal basis](@entry_id:147779)) given as: $c_{\boldsymbol{0}} = 2.50 \times 10^{-3}$, $c_{1} = 1.20 \times 10^{-4}$, $c_{2} = -8.00 \times 10^{-5}$, $c_{3} = 5.00 \times 10^{-5}$, and $c_{4} = 1.50 \times 10^{-5}$.

The mean displacement is immediately identified [@problem_id:2671650]:
$$
\mathbb{E}[Y] = c_{\boldsymbol{0}} = 2.500 \times 10^{-3} \text{ m}
$$
The variance is the sum of the squares of the other coefficients:
$$
\mathrm{Var}[Y] = (1.20 \times 10^{-4})^2 + (-8.00 \times 10^{-5})^2 + (5.00 \times 10^{-5})^2 + (1.50 \times 10^{-5})^2
$$
$$
\mathrm{Var}[Y] = (1.44 + 0.64 + 0.25 + 0.0225) \times 10^{-8} = 2.3525 \times 10^{-8} \approx 2.353 \times 10^{-8} \text{ m}^2
$$
This demonstrates the ease with which key statistical properties can be obtained once the PCE [surrogate model](@entry_id:146376) is built.

### Theoretical Guarantees and Limitations

While PCE is a powerful method, its effectiveness depends on certain properties of the underlying physical model and its mathematical representation.

#### Well-Posedness of the Underlying Problem

For PCE to be meaningful, the underlying physical problem must be well-posed for (almost) every realization of the random parameters. Consider a linear elastostatic problem where the Young's modulus $E$ is a random variable. The [weak form](@entry_id:137295) of the problem requires the bilinear form $a(u,v)$, which depends on $E$, to be coercive and continuous. This typically requires that the random modulus $E(\omega)$ be bounded away from both zero and infinity, i.e., there exist deterministic constants $0  E_{\min} \le E(\omega) \le E_{\max}  \infty$ for almost every outcome $\omega$. If $E(\omega)$ could be zero, coercivity is lost and the system may not be stable. If $E(\omega)$ could be infinite, continuity is lost. These bounds ensure not only that a unique solution exists for each realization, but also that the solution's norm is sufficiently controlled, which is necessary for the solution to be a member of the Hilbert space $L^2(\mathbb{P}_{\boldsymbol{\xi}}; V)$, where $V$ is the function space for the [displacement field](@entry_id:141476) (e.g., $H_0^1$). This membership is the formal requirement for the existence of a mean-square convergent PCE [@problem_id:2671680].

#### The Promise of Spectral Convergence

The primary theoretical advantage of PCE is its potential for **[spectral convergence](@entry_id:142546)**. This means the error of the truncated approximation decreases exponentially with the polynomial degree $p$, often written as $\|Y - Y_p\| \le C \exp(-\gamma p)$ for some constants $C, \gamma > 0$. This is significantly faster than the algebraic convergence rates (e.g., $O(p^{-k})$) typical of [finite element methods](@entry_id:749389) in space.

This remarkable [rate of convergence](@entry_id:146534) is achieved if the response function $Y(\boldsymbol{\xi})$ is **analytic** with respect to the random parameters $\boldsymbol{\xi}$. More formally, [spectral convergence](@entry_id:142546) is guaranteed if the parameter-to-solution map, $\boldsymbol{\xi} \mapsto Y(\boldsymbol{\xi})$, can be holomorphically extended into a region of the complex plane that contains the real domain of the parameters. For a PDE problem, this requires that the governing operator remains well-posed (e.g., coercive) not just for real values of $\boldsymbol{\xi}$, but also for complex values within that extended region [@problem_id:2671644]. For many linear elliptic problems with smoothly varying coefficients, this condition holds, and PCE delivers exceptionally accurate results with relatively few terms.

#### Limitations: The Challenge of Non-Smoothness

The promise of [spectral convergence](@entry_id:142546) is broken when the [response function](@entry_id:138845) $Y(\boldsymbol{\xi})$ is not smooth. In [solid mechanics](@entry_id:164042), non-smoothness arises frequently from physical phenomena such as:

-   **Unilateral contact:** A component makes or breaks contact with a surface.
-   **Plasticity:** Material behavior changes upon reaching a [yield stress](@entry_id:274513).
-   **Fracture:** A crack initiates or propagates.

These events introduce "kinks" or even discontinuities into the response function. For instance, consider a response representing a [contact force](@entry_id:165079), $R(\xi) = \max(0, \alpha\xi - c)$. This function is continuous but has a discontinuous first derivative at the contact activation point $\xi = c/\alpha$. When we attempt to approximate such a non-analytic function with a global basis of smooth polynomials (like Hermite or Legendre), the convergence rate degrades from exponential to slow algebraic decay. Furthermore, the approximation suffers from [spurious oscillations](@entry_id:152404) near the singularity, a phenomenon analogous to the Gibbs effect in Fourier series [@problem_id:2671655].

A powerful remedy for this limitation is the **multi-element Polynomial Chaos Expansion** (m-PCE), also known as piecewise PCE. The core idea is to partition the random [parameter space](@entry_id:178581) into several "elements", with the boundaries of the elements aligned with the locations of the non-smoothness. Within each element, the [response function](@entry_id:138845) is typically smooth (often analytic). A separate, local PCE is then constructed for each element. Since the function is smooth within each element, [spectral convergence](@entry_id:142546) is recovered locally. Global statistics are then computed by combining the results from each element, weighted by the probability mass of that element, according to the laws of total [expectation and variance](@entry_id:199481) [@problem_id:2671655]. This approach restores the high accuracy of PCE for a much broader class of engineering problems involving non-linear, non-smooth behavior.