## Introduction
In modern computational science and engineering, accurately predicting the behavior of complex systems is paramount. However, these predictions are often clouded by uncertainty stemming from imprecise measurements, manufacturing tolerances, or inherent [stochasticity](@entry_id:202258) in physical parameters. Quantifying the impact of these uncertainties, a field known as Uncertainty Quantification (UQ), is critical but often computationally prohibitive, with traditional methods like Monte Carlo simulation requiring thousands or millions of model evaluations. This article introduces Polynomial Chaos Expansions (PCE), a powerful spectral method that addresses this challenge by creating an inexpensive and analytical [surrogate model](@entry_id:146376) of the complex system.

This article provides a comprehensive exploration of the PCE framework. You will learn to re-cast problems of [uncertainty propagation](@entry_id:146574) from a stochastic sampling context into a deterministic algebraic one. The chapters will guide you through the theoretical underpinnings, practical applications, and hands-on implementation of this versatile technique.

The journey begins in **Principles and Mechanisms**, where we will dissect the mathematical foundation of PCE, from its basis in Hilbert spaces to the practical methods for constructing the expansion for various types of uncertain inputs. Next, **Applications and Interdisciplinary Connections** will showcase how PCE is leveraged across diverse fields—from electromagnetics and [solid mechanics](@entry_id:164042) to control systems and machine learning—to perform sensitivity analysis, solve inverse problems, and analyze [stochastic dynamics](@entry_id:159438). Finally, **Hands-On Practices** will provide you with the opportunity to solidify your understanding by building and utilizing a PCE for a practical problem, bridging theory with implementation.

## Principles and Mechanisms

The Polynomial Chaos Expansion (PCE) provides a functional representation of a system's response to stochastic inputs, grounded in the principles of [functional analysis](@entry_id:146220) and [approximation theory](@entry_id:138536). It recasts the problem of [uncertainty propagation](@entry_id:146574) into the deterministic problem of finding the coefficients of a spectral expansion. This chapter elucidates the foundational principles of PCE, the mechanisms for its construction, and its powerful applications.

### The Hilbert Space Framework of Randomness

At its core, a Polynomial Chaos Expansion is a representation of a random variable within a specific Hilbert space. Consider a physical system whose behavior can be described by a model output, $Y$. This output depends on a vector of $d$ random input parameters, $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$, which are characterized by a joint probability measure $\mu$. We are interested in quantities $Y$ that possess [finite variance](@entry_id:269687), which mathematically corresponds to the space of square-integrable functions, denoted $L^2(\mu)$. This space consists of all functions $Y(\boldsymbol{\xi})$ for which the second moment is finite:
$$
\mathbb{E}[Y^2] = \int_{\Gamma} Y(\boldsymbol{\xi})^2 \, \mathrm{d}\mu(\boldsymbol{\xi}) \lt \infty
$$
where $\Gamma$ is the support of the random vector $\boldsymbol{\xi}$.

The space $L^2(\mu)$ is a Hilbert space endowed with an inner product defined by the expectation of the product of two of its elements:
$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int_{\Gamma} f(\boldsymbol{\xi})g(\boldsymbol{\xi}) \, \mathrm{d}\mu(\boldsymbol{\xi})
$$
As with any Hilbert space, we can represent any element $Y \in L^2(\mu)$ as a [series expansion](@entry_id:142878) in terms of a complete orthonormal basis. The central idea of generalized Polynomial Chaos (gPC) is to choose this basis as a set of multivariate polynomials, $\{\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\}_{\boldsymbol{\alpha} \in \mathcal{A}}$, where $\mathcal{A}$ is a countable set of multi-indices. The [orthonormality](@entry_id:267887) condition is expressed as:
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
where $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the Kronecker delta.

Given such a basis, any random variable $Y \in L^2(\mu)$ can be represented by the series [@problem_id:3411038]:
$$
Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
The convergence of this series is in the $L^2$ sense. The coefficients $c_{\boldsymbol{\alpha}}$, often called the spectral or Fourier coefficients, are uniquely determined due to the [orthonormality](@entry_id:267887) of the basis. They are found by projecting the function $Y$ onto each basis polynomial:
$$
c_{\boldsymbol{\alpha}} = \langle Y, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$
By convention, the zeroth-order basis polynomial is a constant, $\Psi_{\boldsymbol{0}}(\boldsymbol{\xi}) = C$. The [normalization condition](@entry_id:156486) $\langle \Psi_{\boldsymbol{0}}, \Psi_{\boldsymbol{0}} \rangle = 1$ implies $\mathbb{E}[C^2] = C^2 = 1$, so we choose $\Psi_{\boldsymbol{0}}(\boldsymbol{\xi}) = 1$. Consequently, all higher-order basis polynomials ($\boldsymbol{\alpha} \neq \boldsymbol{0}$) must have [zero mean](@entry_id:271600), as $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{0}} \rangle = \delta_{\boldsymbol{\alpha}\boldsymbol{0}} = 0$. This immediately reveals a remarkable property: the zeroth-order coefficient $c_{\boldsymbol{0}}$ is simply the mean of the quantity of interest:
$$
c_{\boldsymbol{0}} = \langle Y, \Psi_{\boldsymbol{0}} \rangle = \mathbb{E}[Y \cdot 1] = \mathbb{E}[Y]
$$

### The Wiener-Askey Scheme: Matching Polynomials to Distributions

The term "generalized" in gPCE refers to the extension of Norbert Wiener's original theory, which was specific to Gaussian random variables and Hermite polynomials. The gPCE framework leverages the fact that for any of the common continuous or [discrete probability distributions](@entry_id:166565), there exists a corresponding family of [classical orthogonal polynomials](@entry_id:192726). This relationship is known as the **Wiener-Askey scheme**. The key is that the weight function defining the orthogonality of a polynomial family must match the probability density function (PDF) of the random input variable.

For a system with independent random inputs $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$, the joint PDF is the product of the marginal PDFs, $f_{\boldsymbol{\xi}}(\boldsymbol{\xi}) = \prod_{i=1}^d f_i(\xi_i)$, and the multivariate basis functions $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ can be constructed as tensor products of univariate orthogonal polynomials $\psi_{\alpha_i}^{(i)}(\xi_i)$:
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$
The choice for each univariate family $\psi^{(i)}$ depends on the distribution of the corresponding input $\xi_i$. For example, consider a [multiphysics](@entry_id:164478) model with two independent uncertain parameters: one modeled by a standard normal distribution, $\xi_1 \sim \mathcal{N}(0,1)$, and the other by a standard uniform distribution, $\xi_2 \sim \text{Uniform}(-1,1)$ [@problem_id:3523231].

1.  For $\xi_1 \sim \mathcal{N}(0,1)$, the PDF is $w_1(\xi_1) = \frac{1}{\sqrt{2\pi}}\exp(-\xi_1^2/2)$. The family of polynomials orthogonal with respect to this Gaussian weight function is the **probabilists' Hermite polynomials**, $He_k(x)$.

2.  For $\xi_2 \sim \text{Uniform}(-1,1)$, the PDF is $w_2(\xi_2) = \frac{1}{2}$ on the interval $[-1,1]$. The polynomials orthogonal with respect to a constant weight function on $[-1,1]$ are the **Legendre polynomials**, $P_k(x)$.

The appropriate tensor-product basis for this problem would therefore be $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = He_{\alpha_1}(\xi_1) P_{\alpha_2}(\xi_2)$ (after proper normalization). Other important pairings in the Wiener-Askey scheme include Laguerre polynomials for Gamma-distributed inputs and Jacobi polynomials for Beta-distributed inputs.

### Handling Complex and Correlated Inputs

The standard PCE framework assumes that the input random variables are independent. Real-world systems often involve correlated inputs or inputs that are continuous [random fields](@entry_id:177952). PCE can be adapted to these scenarios through preliminary transformations.

#### Correlated Random Variables and the Nataf Transformation

If the input vector $\boldsymbol{\Xi}$ consists of [correlated random variables](@entry_id:200386), the tensor-product construction of the basis is no longer valid, as the joint PDF is not a product of the marginals. The **Nataf transformation** is a standard procedure to address this. Its goal is to find an invertible transformation $\boldsymbol{\Xi} = T(\mathbf{Z})$ that maps a vector $\mathbf{Z}$ of independent standard random variables to the target correlated vector $\boldsymbol{\Xi}$. The PCE is then constructed for the quantity of interest viewed as a function of the independent variables, $\tilde{Q}(\mathbf{Z}) = Q(T(\mathbf{Z}))$.

For the common case where the input vector $\boldsymbol{\Xi}$ follows a multivariate Gaussian distribution $\mathcal{N}(\boldsymbol{\mu}, \boldsymbol{\Sigma})$, the Nataf transformation simplifies to a linear "whitening" transformation [@problem_id:3341898]. We seek a matrix $\mathbf{A}$ such that if we define the transformed variables as $\mathbf{Z} = \mathbf{A}(\boldsymbol{\Xi} - \boldsymbol{\mu})$, the covariance of $\mathbf{Z}$ is the identity matrix, $\text{Cov}(\mathbf{Z}) = \mathbf{I}$. This condition, $\mathbf{A}\boldsymbol{\Sigma}\mathbf{A}^\top = \mathbf{I}$, can be satisfied in several ways. Two common methods are:
1.  **Cholesky Decomposition**: Since the covariance matrix $\boldsymbol{\Sigma}$ is symmetric and positive-definite, it admits a unique lower-triangular Cholesky decomposition $\boldsymbol{\Sigma} = \mathbf{L}\mathbf{L}^\top$. The [transformation matrix](@entry_id:151616) is then $\mathbf{A} = \mathbf{L}^{-1}$.
2.  **Eigendecomposition**: Using the [spectral decomposition](@entry_id:148809) $\boldsymbol{\Sigma} = \mathbf{V}\boldsymbol{\Lambda}\mathbf{V}^\top$, where $\mathbf{V}$ is the orthogonal matrix of eigenvectors and $\boldsymbol{\Lambda}$ is the diagonal matrix of eigenvalues, a valid transformation is $\mathbf{A} = \boldsymbol{\Lambda}^{-1/2}\mathbf{V}^\top$.

Once this transformation is performed, the model can be expressed in terms of the independent standard normal variables $\mathbf{Z}$, and a standard PCE using Hermite polynomials can be constructed.

#### Random Fields and the Karhunen-Loève Expansion

When a system parameter is a spatially or temporally varying random field, such as a random permittivity $\epsilon(\mathbf{r}, \omega)$ in an electromagnetics problem, we face an input with infinite dimensionality. The **Karhunen-Loève (K-L) expansion** is a fundamental tool for discretizing such fields into a [countable set](@entry_id:140218) of uncorrelated random variables [@problem_id:3341904]. It is the optimal [linear representation](@entry_id:139970) of a [random process](@entry_id:269605) in terms of [mean-square error](@entry_id:194940).

For a second-order [random field](@entry_id:268702) $\epsilon(\mathbf{r}, \omega)$ with mean $m(\mathbf{r}) = \mathbb{E}[\epsilon(\mathbf{r})]$ and [covariance function](@entry_id:265031) $C(\mathbf{r}, \mathbf{r}') = \mathbb{E}[(\epsilon(\mathbf{r})-m(\mathbf{r}))(\epsilon(\mathbf{r}')-m(\mathbf{r}'))]$, the K-L expansion is derived from the spectral decomposition of the covariance integral operator $\mathcal{T}_C$. This involves solving the Fredholm [integral equation](@entry_id:165305) of the second kind:
$$
\int_D C(\mathbf{r}, \mathbf{r}') \phi_n(\mathbf{r}') \, \mathrm{d}\mathbf{r}' = \lambda_n \phi_n(\mathbf{r})
$$
where $\{\lambda_n\}$ are the eigenvalues and $\{\phi_n(\mathbf{r})\}$ are the corresponding orthonormal eigenfunctions. The [random field](@entry_id:268702) can then be represented as:
$$
\epsilon(\mathbf{r}, \omega) = m(\mathbf{r}) + \sum_{n=1}^\infty \sqrt{\lambda_n} \phi_n(\mathbf{r}) \xi_n(\omega)
$$
A crucial result is that the random coefficients $\xi_n(\omega)$ are zero-mean, uncorrelated, and have unit variance, i.e., $\mathbb{E}[\xi_n \xi_m] = \delta_{nm}$. By truncating this series, the random field is approximated using a finite number of uncorrelated random variables $\{\xi_n\}_{n=1}^N$. These variables can then serve as the inputs for a Polynomial Chaos Expansion of the model output.

### Computational Methods for Determining PCE Coefficients

The [projection formula](@entry_id:152164) $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$ defines the PCE coefficients, but computing this expectation is non-trivial when $Y(\boldsymbol{\xi})$ is the output of a complex simulation (e.g., a finite element solver). Broadly, methods to compute the coefficients fall into two categories: intrusive and non-intrusive.

#### Intrusive Methods: Stochastic Galerkin

The **stochastic Galerkin method** is an intrusive approach where the PCE representation is integrated directly into the governing equations of the physical model [@problem_id:3523236]. The solution to the governing equations, say $u(x, \boldsymbol{\xi})$, is itself expressed as a PCE: $u(x, \boldsymbol{\xi}) = \sum_{\boldsymbol{\beta}} u_{\boldsymbol{\beta}}(x) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})$. This expansion is substituted into the PDE. A Galerkin projection is then applied, where the resulting residual equation is made orthogonal to each basis polynomial $\Psi_{\boldsymbol{\alpha}}$. This process transforms the stochastic PDE into a large, coupled system of deterministic PDEs for the coefficients $u_{\boldsymbol{\beta}}(x)$.

For instance, applying this to a nonlinear elliptic problem like $-\nabla \cdot (a(x, \boldsymbol{\xi})\nabla u) + \sigma(u) = f(x)$ results in a [deterministic system](@entry_id:174558) that couples all the [modal coefficients](@entry_id:752057) $u_{\boldsymbol{\beta}}(x)$. Solving this requires specialized solvers and modifications to the original code, making the method "intrusive". Its primary advantage is that, for problems with sufficient regularity, it can achieve high (spectral) accuracy by solving one large coupled system. However, the intrusiveness and the complexity of handling nonlinear terms are significant drawbacks.

#### Non-intrusive Methods: Treating the Solver as a Black Box

Non-intrusive methods are often preferred in practice because they treat the existing deterministic solver as a "black box," requiring no modification to the source code. These methods compute the coefficients by running the solver at a set of sample points and post-processing the results.

**1. Projection via Numerical Quadrature (Stochastic Collocation):**
This method directly approximates the integral in the [projection formula](@entry_id:152164) $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y\Psi_{\boldsymbol{\alpha}}] = \int Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) f(\boldsymbol{\xi}) \, \mathrm{d}\boldsymbol{\xi}$ using numerical quadrature. The solver is evaluated at the chosen quadrature nodes $\{\boldsymbol{\xi}^{(n)}\}$, and the coefficients are computed as a weighted sum:
$$
c_{\boldsymbol{\alpha}} \approx \sum_{n=1}^N w_n Y(\boldsymbol{\xi}^{(n)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(n)})
$$
For high accuracy, specific [quadrature rules](@entry_id:753909) are matched to the input distributions (e.g., Gauss-Hermite for Gaussian inputs, Gauss-Legendre for uniform inputs). A key result is that an $n$-point Gauss quadrature rule can exactly integrate polynomials up to degree $2n-1$. If the model output $Y(\boldsymbol{\xi})$ is itself a polynomial of degree $p$, then the product $Y\Psi_{\boldsymbol{\alpha}}$ can be integrated exactly with a sufficiently high-order rule, leading to exact coefficients [@problem_id:3341911]. For multi-dimensional problems, however, forming a full tensor-product grid of quadrature points leads to [exponential growth](@entry_id:141869) in the number of required simulations, a manifestation of the **[curse of dimensionality](@entry_id:143920)**. For $d$ dimensions, $(p+1)^d$ points are needed to exactly integrate a degree-$p$ polynomial, which quickly becomes infeasible. Sparse grid methods can alleviate this, but the scaling remains challenging.

**2. Regression via Least-Squares:**
An alternative non-intrusive approach is to frame the problem as one of statistical regression. We postulate the truncated PCE model $Y(\boldsymbol{\xi}) \approx \sum_{\boldsymbol{\alpha} \in \mathcal{A}_p} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ and aim to find the coefficients $\{c_{\boldsymbol{\alpha}}\}$ that best fit a set of model evaluations. Given $N$ sample pairs $\{(\boldsymbol{\xi}^{(n)}, Y(\boldsymbol{\xi}^{(n)}))\}_{n=1}^N$, this leads to a linear system of equations $\mathbf{y} \approx \boldsymbol{\Psi}\mathbf{c}$, where $y_n = Y(\boldsymbol{\xi}^{(n)})$ and $\Psi_{n,\boldsymbol{\alpha}} = \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(n)})$. The coefficients are typically found by solving the linear [least-squares problem](@entry_id:164198):
$$
\min_{\mathbf{c}} \|\boldsymbol{\Psi}\mathbf{c} - \mathbf{y}\|_2^2
$$
To ensure a [well-posed problem](@entry_id:268832), the number of samples $N$ must be at least the number of unknown coefficients $M = |\mathcal{A}_p|$, and for stability, [oversampling](@entry_id:270705) ($N > M$, e.g., $N=2M$) is recommended [@problem_id:3341911]. The sample points $\boldsymbol{\xi}^{(n)}$ are often drawn randomly from the input distribution $\mu$. A major advantage of regression is its flexibility in sampling and its ability to mitigate the [curse of dimensionality](@entry_id:143920). The number of required samples grows with the number of basis functions, $M = \binom{d+p}{p} \sim d^p/p!$, which is polynomial in $d$, a much slower growth than the exponential scaling of [tensor-product quadrature](@entry_id:145940) [@problem_id:3341911].

### Applications of the PCE Surrogate Model

Once the coefficients $\{c_{\boldsymbol{\alpha}}\}$ have been computed, the resulting PCE serves as an inexpensive and analytical surrogate model for the original complex simulation. This enables a range of powerful post-processing analyses.

#### Computation of Statistical Moments

The [orthonormality](@entry_id:267887) of the polynomial basis allows for the direct and exact computation of statistical moments from the PCE coefficients. As already shown, the mean is simply the zeroth coefficient, $\mathbb{E}[Y] = c_{\boldsymbol{0}}$. The variance can be computed with similar ease [@problem_id:2589461]. Using the definition $\mathrm{Var}(Y) = \mathbb{E}[(Y - \mathbb{E}[Y])^2]$:
$$
\mathrm{Var}(Y) = \mathbb{E}\left[ \left(\sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}} - c_{\boldsymbol{0}}\Psi_{\boldsymbol{0}}\right)^2 \right] = \mathbb{E}\left[ \left(\sum_{\boldsymbol{\alpha} \in \mathcal{A}\setminus\{\boldsymbol{0}\}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right)^2 \right]
$$
Expanding the square and using [orthonormality](@entry_id:267887), we find that all cross-terms vanish:
$$
\mathrm{Var}(Y) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}\setminus\{\boldsymbol{0}\}} \sum_{\boldsymbol{\beta} \in \mathcal{A}\setminus\{\boldsymbol{0}\}} c_{\boldsymbol{\alpha}}c_{\boldsymbol{\beta}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}] = \sum_{\boldsymbol{\alpha} \in \mathcal{A}\setminus\{\boldsymbol{0}\}} c_{\boldsymbol{\alpha}}^2
$$
Thus, the total variance of the model output is simply the sum of the squares of all higher-order PCE coefficients. This elegant result allows for instantaneous moment estimation once the expansion is built.

#### Global Sensitivity Analysis

The structure of the PCE is particularly well-suited for **Global Sensitivity Analysis (GSA)**, which aims to apportion the output variance to the different input variables. The most common GSA metrics are the **Sobol' indices**. The first-order Sobol' index, $S_i$, measures the direct contribution of input $\xi_i$ to the output variance. The total-effect index, $T_i$, measures the total contribution of $\xi_i$, including its interactions with all other variables.

Thanks to the [orthonormality](@entry_id:267887) of the tensor-product basis, these indices can be computed directly from the PCE coefficients by partitioning the total variance [@problem_id:3341860]. The total variance is $D = \sum_{\boldsymbol{\alpha} \in \mathcal{A}\setminus\{\boldsymbol{0}\}} c_{\boldsymbol{\alpha}}^2$. The partial variance associated only with input $\xi_i$ is the sum of squares of coefficients for basis functions that depend only on $\xi_i$. Let $\mathcal{A}_i$ be the set of multi-indices where only the $i$-th component is non-zero ($\alpha_j = 0$ for all $j \neq i$). Then, the first-order index is:
$$
S_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_i \setminus \{\boldsymbol{0}\}} c_{\boldsymbol{\alpha}}^2}{D}
$$
The total-effect index is computed by summing the squares of all coefficients corresponding to basis functions that have any dependence on $\xi_i$. Let $\mathcal{A}_{\sim i}$ be the set of multi-indices where the $i$-th component is non-zero ($\alpha_i > 0$). The total-effect index is:
$$
T_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_{\sim i}} c_{\boldsymbol{\alpha}}^2}{D}
$$
This "PCE-based Sobol'" analysis provides a complete sensitivity profile of the model with virtually no additional computational cost once the PCE is constructed.

### Advanced Topics and Refinements

#### Truncation Schemes and the Curse of Dimensionality

In practice, the infinite PCE series must be truncated to a finite number of terms. The choice of the multi-[index set](@entry_id:268489) $\mathcal{A}_p$ for a maximum "degree" $p$ is critical, especially in high dimensions.
- **Total-Degree (TD) Truncation:** This is the most common scheme, including all polynomials for which the sum of the univariate degrees is at most $p$:
  $$
  \mathcal{A}_p^{\mathrm{TD}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \sum_{j=1}^d \alpha_j \le p \right\}
  $$
  The number of terms in this set is $|\mathcal{A}_p^{\mathrm{TD}}| = \binom{d+p}{p}$, which grows polynomially in $d$ (for fixed $p$) and can become very large.
- **Hyperbolic-Cross (HC) Truncation:** This scheme is designed to reduce the number of terms by preferentially removing high-order [interaction terms](@entry_id:637283) (where many $\alpha_j$ are simultaneously non-zero), which are often assumed to be less important. A common definition is:
  $$
  \mathcal{A}_p^{\mathrm{HC}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{j=1}^d (\alpha_j + 1) \le p+1 \right\}
  $$
  The number of terms in this set grows much more slowly with dimension than in the TD case, helping to alleviate the [curse of dimensionality](@entry_id:143920) in certain problems [@problem_id:3341902].

#### Multi-Element PCE for Non-Smooth Responses

Standard PCE exhibits [spectral convergence](@entry_id:142546) only if the model response $Y(\boldsymbol{\xi})$ is sufficiently smooth. For many real-world problems, such as an electromagnetic [waveguide](@entry_id:266568) operating near its [cutoff frequency](@entry_id:276383), the response may have kinks or discontinuities [@problem_id:3341868]. In such cases, standard PCE suffers from slow convergence and spurious Gibbs oscillations.

The **Multi-Element Polynomial Chaos Expansion (ME-PCE)** is an advanced technique designed to handle such non-smoothness. The core idea is to partition the input space of the random variables into several disjoint "elements". The partition is specifically designed so that any non-smooth behavior occurs at the boundaries between elements. Within each element, the function is smooth. A separate, local PCE is then constructed on each element, using a [basis of polynomials](@entry_id:148579) that are orthogonal with respect to the *conditional* probability measure on that element [@problem_id:3341868]. The global approximation is the collection of these [piecewise polynomial](@entry_id:144637) representations.

This approach effectively isolates the non-smoothness and restores fast convergence rates within each element, mitigating the Gibbs phenomenon and allowing accurate approximation even with low-order local polynomials [@problem_id:3341868]. For a uniform random input, this might involve using scaled and shifted Legendre polynomials on each sub-interval of the partition [@problem_id:3341868]. ME-PCE is thus a powerful extension of the PCE framework, analogous to the finite element method in physical space, enabling robust uncertainty quantification for a much broader class of complex models.