## Introduction
Propagating uncertainty through complex computational models is a fundamental challenge across science and engineering. When model inputs are not perfectly known but are instead described by probability distributions, how can we efficiently characterize the resulting uncertainty in the model's output? Traditional methods like Monte Carlo simulation can be prohibitively expensive, requiring thousands or millions of model runs. Polynomial Chaos Expansions (PCE) offer a powerful and elegant alternative, providing a functional representation of the model's response to stochastic inputs. This framework transforms the problem of [uncertainty propagation](@entry_id:146574) into one of spectral expansion, enabling rapid statistical analysis and deep insights into the model's behavior.

This article serves as a comprehensive guide to the theory and application of PCE. We will bridge the gap between abstract mathematics and practical implementation, equipping you with the knowledge to leverage PCE in your own work. The journey begins in the **Principles and Mechanisms** chapter, where we will delve into the mathematical foundations of PCE, learn how to construct the crucial orthonormal polynomial bases, and explore robust computational methods for determining the expansion coefficients. Next, in **Applications and Interdisciplinary Connections**, we will showcase the versatility of PCE, demonstrating its use for sensitivity analysis, inverse problems, and robust design, and revealing its powerful synergy with data science and machine learning. Finally, the **Hands-On Practices** section provides concrete problems to help you master the key computational techniques and solidify your understanding. By the end, you will have a thorough grasp of how PCE can transform intractable stochastic problems into manageable, insightful analyses.

## Principles and Mechanisms

The representation of uncertainty in computational models is a central challenge in [inverse problems](@entry_id:143129), [data assimilation](@entry_id:153547), and [scientific computing](@entry_id:143987) at large. As introduced in the previous chapter, Polynomial Chaos Expansions (PCE) provide a powerful functional representation for a model's response to uncertain inputs. This chapter delves into the fundamental principles and mechanisms that underpin PCE, establishing its mathematical foundation, exploring methods for its practical construction, and detailing the theoretical properties that make it such an effective tool for uncertainty quantification.

### The Mathematical Foundation of Polynomial Chaos Expansions

At its core, a Polynomial Chaos Expansion is a representation of a random variable within a Hilbert space framework. Consider a computational model whose output, a quantity of interest $Y$, is determined by a vector of $d$ random inputs, $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$. We assume these inputs are characterized by a known joint probability measure $\mu$ on $\mathbb{R}^d$. The output $Y$ is thus a random variable that is a function of $\boldsymbol{\xi}$, i.e., $Y = f(\boldsymbol{\xi})$.

The theoretical underpinning of PCE lies in the Hilbert space of square-integrable functions with respect to the measure $\mu$, denoted $L^2(\mu)$. This space consists of all functions $g: \mathbb{R}^d \to \mathbb{R}$ for which the variance is finite. More formally, $g \in L^2(\mu)$ if its squared value is integrable against the measure $\mu$:
$$
\int_{\mathbb{R}^d} |g(\boldsymbol{\xi})|^2 \mathrm{d}\mu(\boldsymbol{\xi})  \infty
$$
This space is equipped with an inner product defined by the expectation operator:
$$
\langle g, h \rangle = \mathbb{E}[gh] = \int_{\mathbb{R}^d} g(\boldsymbol{\xi}) h(\boldsymbol{\xi}) \mathrm{d}\mu(\boldsymbol{\xi})
$$

Within this Hilbert space, a PCE is a [spectral representation](@entry_id:153219) of the function $Y$ in terms of a basis of multivariate polynomials $\{\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\}_{\boldsymbol{\alpha} \in \mathbb{N}_0^d}$ that are orthonormal with respect to this inner product [@problem_id:3411038]. The [orthonormality](@entry_id:267887) condition is expressed as:
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
where $\boldsymbol{\alpha}$ and $\boldsymbol{\beta}$ are multi-indices and $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the Kronecker delta, which is $1$ if $\boldsymbol{\alpha} = \boldsymbol{\beta}$ and $0$ otherwise. The expansion takes the form of a generalized Fourier series:
$$
Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$
The uniqueness of the coefficients $c_{\boldsymbol{\alpha}}$ is a direct and powerful consequence of the [orthonormality](@entry_id:267887) of the basis. By taking the inner product of the entire expansion with a basis function $\Psi_{\boldsymbol{\beta}}$, all terms in the infinite sum vanish except for the one where $\boldsymbol{\alpha} = \boldsymbol{\beta}$, yielding a simple [projection formula](@entry_id:152164) for the coefficients:
$$
c_{\boldsymbol{\beta}} = \langle Y, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi}) \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})]
$$
By convention, the zeroth-order polynomial $\Psi_{\mathbf{0}}$ is the constant function $\Psi_{\mathbf{0}}(\boldsymbol{\xi}) \equiv 1$. Its coefficient, $c_{\mathbf{0}} = \mathbb{E}[Y \cdot 1] = \mathbb{E}[Y]$, is simply the mean of the quantity of interest. All higher-order basis polynomials ($\boldsymbol{\alpha} \neq \mathbf{0}$) are constructed to have [zero mean](@entry_id:271600), i.e., $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = \langle \Psi_{\boldsymbol{\alpha}}, 1 \rangle = \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\mathbf{0}} \rangle = 0$.

The existence of such a convergent expansion is guaranteed under three minimal conditions [@problem_id:3523156]:
1.  **Measurability**: The output $Y$ must be fully determined by the inputs $\boldsymbol{\xi}$, meaning it is measurable with respect to the [sigma-algebra](@entry_id:137915) generated by $\boldsymbol{\xi}$. This ensures that $Y$ can indeed be written as a function of $\boldsymbol{\xi}$.
2.  **Finite Variance**: The output $Y$ must have a finite second moment, i.e., $\mathbb{E}[|Y|^2]  \infty$. This ensures that $Y$ is an element of the Hilbert space $L^2(\mu)$.
3.  **Completeness**: The polynomial basis $\{\Psi_{\boldsymbol{\alpha}}\}$ must be complete in $L^2(\mu)$, meaning it can represent any function in the space.

Under these conditions, the series converges in the norm of the space, which is **[mean-square convergence](@entry_id:137545)**: the [mean-squared error](@entry_id:175403) of a truncated expansion $Y_P = \sum_{|\boldsymbol{\alpha}| \le P} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}$ approaches zero as the truncation limit $P$ goes to infinity, i.e., $\mathbb{E}[|Y - Y_P|^2] \to 0$. It is crucial to note that [mean-square convergence](@entry_id:137545) does not, in general, imply the stronger condition of almost-sure (pointwise) convergence, which may require additional regularity of the function $Y$.

### Constructing Orthonormal Polynomial Bases

The "generalized" aspect of gPCE refers to the principle of selecting a polynomial basis that is tailored to the probability measure $\mu$ of the input variables. This idea, formalized in the **Wiener-Askey scheme**, is the key to computational efficiency. Each classical continuous probability distribution is associated with a family of orthogonal polynomials. The choice of a basis that is orthogonal with respect to the input measure is paramount [@problem_id:3341875].

For instance, if an input variable $\xi$ follows a **[standard normal distribution](@entry_id:184509)**, $\xi \sim \mathcal{N}(0,1)$, with probability density function (PDF) $\rho_{\mathrm{G}}(x) = \frac{1}{\sqrt{2\pi}} \exp(-x^2/2)$, the corresponding orthogonal polynomials are the **probabilists' Hermite polynomials**, $\{\mathrm{He}_n(x)\}$. Their orthogonality relation, expressed in terms of the PCE inner product, is:
$$
\mathbb{E}[\mathrm{He}_m(\xi)\mathrm{He}_n(\xi)] = \int_{-\infty}^{\infty} \mathrm{He}_m(x)\mathrm{He}_n(x) \rho_{\mathrm{G}}(x) \mathrm{d}x = n! \delta_{mn}
$$
If an input variable $\xi$ follows a **uniform distribution** on $[-1, 1]$, $\xi \sim \mathcal{U}[-1,1]$, with PDF $\rho_{\mathrm{U}}(x) = 1/2$ on the interval, the corresponding [orthogonal polynomials](@entry_id:146918) are the **Legendre polynomials**, $\{P_n(x)\}$. Their orthogonality relation is:
$$
\mathbb{E}[P_m(\xi)P_n(\xi)] = \int_{-1}^{1} P_m(x)P_n(x) \rho_{\mathrm{U}}(x) \mathrm{d}x = \frac{1}{2n+1} \delta_{mn}
$$
Other correspondences exist, such as Laguerre polynomials for Gamma/Exponential distributions and Jacobi polynomials for Beta distributions.

The practical significance of this correspondence is profound. In intrusive methods like the Stochastic Galerkin method, the [system matrix](@entry_id:172230) for the unknown coefficients $c_{\boldsymbol{\alpha}}$ involves terms of the form $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}]$. By choosing the basis to be orthogonal with respect to the input measure, this "[mass matrix](@entry_id:177093)" becomes diagonal, [decoupling](@entry_id:160890) the equations and drastically simplifying the problem [@problem_id:3341875].

For variables that do not follow a standard distribution, a simple affine transformation often suffices. For example, if $\Xi \sim \mathcal{N}(\mu, \sigma^2)$, we can define a standard normal variable $Z = (\Xi - \mu)/\sigma$. A basis for functions of $\Xi$ can be constructed using Hermite polynomials of the standardized variable, $\{\mathrm{He}_n((\Xi - \mu)/\sigma)\}$. This mapped basis remains orthogonal with respect to the measure of $\Xi$ [@problem_id:3341875].

### Handling High-Dimensional Inputs

Most realistic models involve multiple uncertain parameters. Constructing and managing the multivariate polynomial basis is a critical aspect of PCE.

#### Tensor-Product Basis for Independent Inputs

When the input variables $\xi_1, \dots, \xi_d$ are mutually independent, the joint probability measure is a product of the marginal measures, $\mu = \mu_1 \otimes \dots \otimes \mu_d$. In this ubiquitous case, a multivariate [orthonormal basis](@entry_id:147779) can be systematically constructed via the **tensor product** of the corresponding univariate orthonormal polynomials [@problem_id:3411063].

Let $\{\psi_n^{(i)}\}_{n=0}^{\infty}$ be the univariate orthonormal polynomial basis corresponding to the distribution of $\xi_i$. A multivariate basis function $\Psi_{\boldsymbol{\alpha}}$ indexed by the multi-index $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d) \in \mathbb{N}_0^d$ is defined as:
$$
\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}^{(i)}(\xi_i)
$$
Due to the independence of the inputs, the expectation of a product is the product of expectations. This property ensures that the tensor-product basis is also orthonormal with respect to the joint measure:
$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}\left[ \left(\prod_{i=1}^d \psi_{\alpha_i}^{(i)}\right) \left(\prod_{i=1}^d \psi_{\beta_i}^{(i)}\right) \right] = \prod_{i=1}^d \mathbb{E}[\psi_{\alpha_i}^{(i)} \psi_{\beta_i}^{(i)}] = \prod_{i=1}^d \delta_{\alpha_i \beta_i} = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$
This construction provides a systematic way to build high-dimensional bases, but its size grows rapidly, a manifestation of the **[curse of dimensionality](@entry_id:143920)**.

#### Truncation Strategies

In practice, the infinite PCE series must be truncated to a finite number of terms. This is achieved by selecting a finite set of multi-indices, $\mathcal{A} \subset \mathbb{N}_0^d$. The choice of this [index set](@entry_id:268489) has a profound impact on the accuracy and cost of the PCE surrogate. Several standard truncation schemes exist [@problem_id:3411063] [@problem_id:3341902]:

1.  **Total-Degree (TD) Truncation**: This is the most common scheme. It includes all polynomials up to a specified maximum total degree $p$. The [index set](@entry_id:268489) is defined by the $L_1$-norm of the multi-index:
    $$
    \mathcal{A}_p^{\mathrm{TD}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : |\boldsymbol{\alpha}|_1 = \sum_{i=1}^d \alpha_i \le p \right\}
    $$
    The number of terms in this set, which is the number of unknown coefficients to compute, is given by the combinatorial formula:
    $$
    |\mathcal{A}_p^{\mathrm{TD}}| = \binom{d+p}{p}
    $$
    While polynomial in $d$ for a fixed $p$, this number grows very quickly.

2.  **Tensor Product (TP) or Full Tensor (FT) Truncation**: This scheme includes all polynomials where the degree in each dimension is at most $p$. The [index set](@entry_id:268489) is defined by the $L_\infty$-norm:
    $$
    \mathcal{A}_p^{\mathrm{FT}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : |\boldsymbol{\alpha}|_\infty = \max_{1 \le i \le d} \alpha_i \le p \right\}
    $$
    This forms a hyper-cubic [index set](@entry_id:268489) with [cardinality](@entry_id:137773) $(p+1)^d$, which scales exponentially and is rarely feasible in even moderate dimensions.

3.  **Hyperbolic Cross (HC) and Anisotropic Truncation**: These schemes aim to reduce the number of terms by exploiting the common observation that the influence of high-order interactions (terms involving many variables simultaneously) is often smaller than that of low-order interactions or high-order effects of single variables. A [hyperbolic cross](@entry_id:750469) set can be defined as:
    $$
    \mathcal{A}_p^{\mathrm{HC}} = \left\{ \boldsymbol{\alpha} \in \mathbb{N}_0^d : \prod_{j=1}^d (\alpha_j + 1) \le p+1 \right\}
    $$
    This set preferentially prunes multi-indices with many non-zero components, leading to a much smaller basis size compared to TD, with an asymptotic cardinality of $O(p (\log p)^{d-1})$. This "sparsity-promoting" structure makes HC and related anisotropic schemes highly effective for high-dimensional problems.

### From Random Fields to Finite Inputs: The Karhunen-Loève Expansion

In many physical problems, uncertainty is not confined to a few scalar parameters but is distributed over space or time, represented by a random field or process. For instance, in computational electromagnetics, the material permittivity $\epsilon(\mathbf{r}, \omega)$ might be a random field over a domain $D \subset \mathbb{R}^3$ [@problem_id:3341904]. Directly applying PCE to such an infinite-dimensional input is not feasible.

The **Karhunen-Loève (KL) expansion** provides a bridge by decomposing a second-order [random process](@entry_id:269605) (one with [finite variance](@entry_id:269687)) into a set of deterministic spatial modes and uncorrelated random variables. This furnishes an optimal, in the mean-square sense, finite-dimensional representation of the field.

Given a [random field](@entry_id:268702) $u(\mathbf{r})$ with mean $m(\mathbf{r}) = \mathbb{E}[u(\mathbf{r})]$ and [covariance kernel](@entry_id:266561) $C(\mathbf{r}, \mathbf{r}') = \mathbb{E}[(u(\mathbf{r}) - m(\mathbf{r}))(u(\mathbf{r}') - m(\mathbf{r}'))]$, the KL expansion is derived from the spectral decomposition of the covariance integral operator, $\mathcal{T}_C$. The spatial modes $\phi_n(\mathbf{r})$ and corresponding eigenvalues $\lambda_n$ are the solutions to the Fredholm [integral equation](@entry_id:165305) of the second kind:
$$
\int_D C(\mathbf{r}, \mathbf{r}') \phi_n(\mathbf{r}') \mathrm{d}\mathbf{r}' = \lambda_n \phi_n(\mathbf{r})
$$
The random field can then be represented as:
$$
u(\mathbf{r}) = m(\mathbf{r}) + \sum_{n=1}^\infty \sqrt{\lambda_n} \phi_n(\mathbf{r}) \xi_n
$$
where $\{\phi_n\}$ is an [orthonormal set](@entry_id:271094) of functions in $L^2(D)$, the eigenvalues $\lambda_n$ represent the variance contribution of each mode, and $\{\xi_n\}$ is a set of uncorrelated, zero-mean, unit-variance random variables. If the original field is Gaussian, the variables $\xi_n$ are independent standard normal variables.

A crucial practical step is to truncate this infinite series to a finite number of modes, $M$, chosen to capture a desired fraction of the total variance (i.e., $\sum_{n=1}^M \lambda_n / \sum_{n=1}^\infty \lambda_n$). This yields a finite-dimensional approximation:
$$
u_M(\mathbf{r}) = m(\mathbf{r}) + \sum_{n=1}^M \sqrt{\lambda_n} \phi_n(\mathbf{r}) \xi_n
$$
Any model output $Y$ that depends on the field $u(\mathbf{r})$ can now be approximated as a function of the finite random vector $\boldsymbol{\xi} = (\xi_1, \dots, \xi_M)$. This vector becomes the input for a standard PCE, typically using Hermite polynomials if the field is Gaussian [@problem_id:3411021]. The error introduced by this truncation can be precisely quantified. For example, for a linear functional $y = L(u)$, the [mean-square error](@entry_id:194940) from KL truncation is $\mathbb{E}[(y - y_M)^2] = \sum_{n=M+1}^\infty \lambda_n (L(\phi_n))^2$ [@problem_id:3411021].

For some covariance kernels, the eigenproblem can be solved analytically. A classic example is a zero-mean Gaussian process on $[0, 1]$ with covariance $C(x, x') = \sigma^2 \min(x, x')$, which corresponds to a Wiener process. The KL eigenpairs are found by converting the [integral equation](@entry_id:165305) into a differential equation, yielding eigenvalues $\lambda_n = \frac{4\sigma^2}{(2n-1)^2\pi^2}$ and [eigenfunctions](@entry_id:154705) $\phi_n(x) = \sqrt{2}\sin((n-\frac{1}{2})\pi x)$ for $n=1, 2, \dots$ [@problem_id:3411021]. This provides a concrete pathway from an infinite-dimensional stochastic problem to a finite-dimensional PCE implementation.

### Computing PCE Coefficients: Non-Intrusive Methods

Once the basis and truncation scheme are defined, the central task is to compute the coefficients $c_{\boldsymbol{\alpha}}$. **Non-intrusive methods** are particularly appealing because they treat the original deterministic model solver as a "black box," requiring only model evaluations at specific points in the parameter space. The two main non-intrusive strategies are projection and regression [@problem_id:3341911].

#### Projection Methods

Projection methods directly approximate the integral in the coefficient formula $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y\Psi_{\boldsymbol{\alpha}}] / \mathbb{E}[\Psi_{\boldsymbol{\alpha}}^2]$ using **numerical quadrature**. For a given [basis function](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}$, we can approximate its coefficient by:
$$
c_{\boldsymbol{\alpha}} \approx \frac{1}{\gamma_{\boldsymbol{\alpha}}} \sum_{k=1}^N w_k Y(\boldsymbol{\xi}^{(k)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(k)})
$$
where $\{\boldsymbol{\xi}^{(k)}\}_{k=1}^N$ are the quadrature nodes, $\{w_k\}_{k=1}^N$ are the corresponding weights, and $\gamma_{\boldsymbol{\alpha}} = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}^2]$ is a normalization constant.

The choice of quadrature rule is critical. For independent inputs, **Gauss quadrature** rules are highly effective. A one-dimensional $n$-point Gauss rule associated with a specific polynomial family (e.g., Gauss-Legendre for uniform inputs, Gauss-Hermite for Gaussian inputs) can exactly integrate any polynomial up to degree $2n-1$. To compute coefficients for a PCE of total degree $p$, the integrand $Y\Psi_{\boldsymbol{\alpha}}$ must be integrated exactly. If $Y$ itself is a polynomial of degree at most $p$, the product $Y\Psi_{\boldsymbol{\alpha}}$ has a degree of at most $2p$. Thus, a univariate Gauss rule with $n=p+1$ points in each dimension is sufficient for exact integration. For a $d$-dimensional problem, a full tensor-product of these rules requires $N=(p+1)^d$ model evaluations. This exponential scaling severely limits the applicability of [tensor-product quadrature](@entry_id:145940) to low-dimensional problems ($d \lesssim 4$). For higher dimensions, **sparse-grid quadrature** methods are used to achieve a similar degree of accuracy with a much more favorable, near-polynomial scaling in the number of points.

#### Regression Methods

Regression methods re-frame the problem as a data-fitting exercise. We generate a set of $N$ input samples (the "experimental design") $\{\boldsymbol{\xi}^{(k)}\}_{k=1}^N$, run the solver to obtain the corresponding outputs $\{y_k = Y(\boldsymbol{\xi}^{(k)})\}_{k=1}^N$, and then find the coefficients $\mathbf{c}$ that minimize the [sum of squared errors](@entry_id:149299):
$$
\min_{\mathbf{c}} \sum_{k=1}^N \left( y_k - \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(k)}) \right)^2
$$
This is a standard **linear least-squares** problem, which can be written in matrix form as $\min_{\mathbf{c}} \|\mathbf{y} - \boldsymbol{\Psi}\mathbf{c}\|_2^2$, where $\boldsymbol{\Psi}$ is the $N \times M$ design matrix with entries $\Psi_{k,\boldsymbol{\alpha}} = \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(k)})$, and $M$ is the number of basis functions.

For a unique and stable solution, the number of samples $N$ must be at least the number of coefficients $M$. In practice, [oversampling](@entry_id:270705) with $N \ge 2M$ is recommended to ensure the system is well-conditioned. The samples are typically drawn randomly from the input probability measure.

Comparing the two methods, [least-squares regression](@entry_id:262382) can be much more efficient for high-dimensional problems. While tensor-product projection suffers from the exponential scaling $N=(p+1)^d$, the sample requirement for regression scales with the basis size, $N \gtrsim M = \binom{d+p}{p}$. For high $d$ and low $p$, this polynomial scaling is vastly superior, making regression a key method for alleviating the [curse of dimensionality](@entry_id:143920) [@problem_id:3341911].

### Advanced Topics and Convergence

#### Spectral Convergence

One of the most attractive properties of PCE is its potential for **[spectral convergence](@entry_id:142546)**. This means that for sufficiently [smooth functions](@entry_id:138942), the [mean-square error](@entry_id:194940) of the truncated expansion decays faster than any algebraic power of the polynomial degree $p$, often exponentially, e.g., $O(\rho^{-p})$ for some $\rho  1$.

The condition for [spectral convergence](@entry_id:142546) is rooted in complex analysis: the model output $Y(\boldsymbol{\xi})$ must be **analytic** as a function of the parameters $\boldsymbol{\xi}$, and this [analyticity](@entry_id:140716) must extend to a region in the complex plane $\mathbb{C}^d$ that contains the real support of the random inputs [@problem_id:3341842]. For models described by partial differential equations, like Maxwell's equations, this translates to the requirement that the solution map $\boldsymbol{\xi} \mapsto \boldsymbol{E}(\cdot, \boldsymbol{\xi})$ be holomorphic (analytic for a vector-valued function) into the solution space (e.g., $\boldsymbol{H}(\mathrm{curl})$). This, in turn, depends on the PDE operator remaining well-posed and continuously invertible for complex-valued parameters $\boldsymbol{\zeta}$ within that region.

For example, in the time-harmonic Maxwell equations, if the medium has uniform physical losses ($\mathrm{Im}(\epsilon)  \delta  0$), the operator is coercive and remains invertible for complex parameters near the real axis, guaranteeing [analyticity](@entry_id:140716) and [spectral convergence](@entry_id:142546). In lossless cases, resonances (eigenfrequencies) can occur where the operator is singular. Spectral convergence is achieved only if the parameter-to-output map remains analytic, which requires that these resonances are uniformly avoided for all complex parameters in a neighborhood of the real domain [@problem_id:3341842]. Functions with discontinuities, such as a material property that switches based on a parameter's sign, are not analytic and their PCEs will converge at a much slower algebraic rate.

#### Handling Correlated Inputs

The standard tensor-product construction of a multivariate PCE basis relies on the independence of the input random variables. When inputs are correlated, this construction fails, as the [joint probability](@entry_id:266356) measure is no longer separable. Two main strategies exist to handle dependence [@problem_id:3411039]:

1.  **Direct Dependent-Basis Approach**: One can construct a multivariate polynomial basis $\{\Phi_{\boldsymbol{\alpha}}\}$ that is directly orthogonal with respect to the joint (dependent) probability measure. This can be done numerically, for instance, via a Gram-Schmidt [orthogonalization](@entry_id:149208) process applied to a set of monomial basis functions. While theoretically sound, this approach presents a major computational challenge: calculating the coefficients via projection requires evaluating integrals against the non-separable joint density, for which standard tensor-product or sparse-grid [quadrature rules](@entry_id:753909) are not applicable.

2.  **Transform-to-Independence Approach**: A more common strategy is to first find a **measure-preserving transport** $T$ that maps a vector of independent random variables $\mathbf{U}$ (often standard normal or uniform) to the target correlated variables $\mathbf{X}$, i.e., $\mathbf{X} = T(\mathbf{U})$. Examples of such maps include the **Nataf transform** for Gaussian copulas and the **inverse Rosenblatt transform** for general copulas. One then constructs a PCE for the composite model $g(\mathbf{U}) = Y(T(\mathbf{U}))$. This new function $g$ depends on [independent variables](@entry_id:267118), so a standard tensor-product basis and associated computational tools (quadrature, regression) can be used. This approach effectively transfers the complexity of the dependence from the measure into the function being expanded. The transformation $T$ is generally nonlinear, so the composite model $g(\mathbf{U})$ may be more complex and require a larger PCE than the original model $Y(\mathbf{X})$ might have in its "natural" dependent basis.

It is a common misconception that a tensor product of univariate orthogonal polynomials (e.g., Hermite) remains orthogonal for a correlated measure (e.g., a correlated Gaussian). This is false; for example, the inner product of $\Psi_{(1,0,\dots)}(\mathbf{X}) = X_1$ and $\Psi_{(0,1,\dots)}(\mathbf{X}) = X_2$ is $\mathbb{E}[X_1 X_2] = \mathrm{Cov}(X_1, X_2)$, which is non-zero for correlated variables [@problem_id:3411039].

Ultimately, the choice of basis is a matter of representation. If a [surrogate model](@entry_id:146376), whether constructed via a direct or a transformed approach, represents the true model output exactly (almost surely), then any subsequent inference, such as computing a Bayesian [posterior distribution](@entry_id:145605), will be identical regardless of the chosen representation [@problem_id:3411039]. The challenge lies in finding the most compact and computationally efficient representation for a given problem.