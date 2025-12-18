## Introduction
Modern science and engineering rely heavily on complex computational models to predict the behavior of physical systems. However, a deterministic prediction is often insufficient; a credible analysis must also account for uncertainty in model inputs, parameters, and even the model structure itself. Propagating these uncertainties to quantify their effect on the output—a process known as Uncertainty Quantification (UQ)—is computationally challenging. Traditional methods like Monte Carlo simulation require thousands or millions of model evaluations, which becomes prohibitive when a single run of the high-fidelity simulator takes hours or days.

This article addresses the critical challenge of performing UQ for computationally expensive models through the powerful framework of [surrogate modeling](@entry_id:145866). Surrogate models, also known as metamodels or emulators, are inexpensive mathematical approximations of the complex input-output relationship of a simulator. By replacing the costly simulator with a fast surrogate, we can perform comprehensive UQ analyses that would otherwise be intractable. This guide focuses on two of the most prominent and effective surrogate modeling techniques: Polynomial Chaos Expansions (PCE) and Gaussian Process (GP) regression.

Over the next three chapters, you will gain a deep, practical understanding of these methods. The "Principles and Mechanisms" chapter will lay the theoretical groundwork, exploring how PCE and GP are constructed and what assumptions they entail. Following this, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these surrogates are applied to solve real-world problems in fields from materials science to biomedical engineering. Finally, the "Hands-On Practices" chapter provides interactive exercises to build and apply these models, solidifying your knowledge and skills. We will begin by delving into the fundamental principles that allow these methods to effectively represent and propagate uncertainty.

## Principles and Mechanisms

This chapter delineates the foundational principles and operative mechanisms of [surrogate modeling](@entry_id:145866) for [uncertainty quantification](@entry_id:138597) (UQ). Having established the motivation for surrogate modeling in the previous chapter—namely, the often-prohibitive computational cost of propagating uncertainties through complex, high-fidelity simulators—we now turn to the theoretical and practical underpinnings of two dominant surrogate paradigms: Polynomial Chaos Expansions (PCE) and Gaussian Process (GP) regression. We will explore how these methods are constructed, what assumptions they entail, and how they respectively address the different facets of uncertainty.

### The Landscape of Uncertainty and Surrogates

At its core, surrogate modeling in UQ involves replacing a computationally expensive model, which we may denote as a map $Q(\boldsymbol{X})$ from random inputs $\boldsymbol{X}$ to a quantity of interest $Q$, with a computationally inexpensive approximation, $\hat{Q}(\boldsymbol{X})$. The goal is to construct $\hat{Q}$ such that it is faithful enough to the original model $Q$ that statistics of the output (e.g., mean, variance, probabilities of failure) can be accurately and efficiently estimated.

It is crucial to distinguish these methods from direct simulation techniques like **Monte Carlo (MC) simulation**. An MC approach directly queries the full model $Q$ for a large number of random input samples to build empirical estimates of output statistics. While robust, its slow convergence rate (the [standard error of the mean](@entry_id:136886) estimate scales as $1/\sqrt{N}$ for $N$ samples) makes it impractical for expensive models. Surrogates circumvent this by creating a fast proxy model first, which can then be evaluated millions of times if needed.

Furthermore, it is instructive to differentiate UQ-oriented surrogates from traditional **deterministic response surface modeling**. While both fit a function to data, UQ surrogates are constructed within a probabilistic framework that explicitly accounts for the randomness of the inputs. This allows for a principled quantification of uncertainty. Central to this is the distinction between two types of uncertainty :

*   **Aleatory uncertainty** refers to the inherent, irreducible randomness in a system, such as the natural variability of material properties or environmental conditions. In our framework, this is represented by the probability distribution of the input vector $\boldsymbol{X}$.

*   **Epistemic uncertainty** arises from a lack of knowledge. This includes uncertainty about the correct form or parameters of the physics-based model $Q$ itself, and, critically for [surrogate modeling](@entry_id:145866), uncertainty in the approximation $\hat{Q}$ due to having only a finite number of evaluations of the true model $Q$.

As we will see, PCE is primarily designed to propagate [aleatory uncertainty](@entry_id:154011) through a [spectral representation](@entry_id:153219), while GP regression offers a powerful, built-in mechanism for quantifying the epistemic uncertainty of the surrogate itself .

### Polynomial Chaos Expansions: A Spectral Approach

Polynomial Chaos Expansion is a method rooted in [functional analysis](@entry_id:146220) that represents the model output as a spectral expansion in terms of polynomials that are orthogonal with respect to the probability measure of the random inputs. This "chaos" refers not to dynamical chaos, but to the random nature of the variables, following the terminology of Norbert Wiener.

#### The PCE Representation and Orthogonal Polynomials

Let the model output be a square-[integrable function](@entry_id:146566) of the random input vector, $Y = g(\boldsymbol{\Xi})$, where $\boldsymbol{\Xi} = (\Xi_1, \dots, \Xi_d)$ is a vector of $d$ [independent random variables](@entry_id:273896). The PCE approximates $Y$ as a truncated series:
$$
Y \approx \hat{Y}(\boldsymbol{\Xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\Xi})
$$
Here, $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$ is a **multi-index** from a finite set $\mathcal{A} \subset \mathbb{N}_0^d$, the $c_{\boldsymbol{\alpha}}$ are the expansion coefficients to be determined, and the $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\Xi})$ are multivariate basis polynomials.

The crucial feature of PCE is the choice of this basis. The polynomials are constructed to be **orthonormal** with respect to the probability measure of the inputs. For a single random variable $\xi$ with probability density function (PDF) $\rho(\xi)$ on a domain $\Gamma$, a family of polynomials $\{P_n(\xi)\}_{n \ge 0}$ is orthonormal if it satisfies:
$$
\langle P_i, P_j \rangle = \int_{\Gamma} P_i(\xi) P_j(\xi) \rho(\xi) d\xi = \delta_{ij}
$$
where $\delta_{ij}$ is the Kronecker delta. This inner product represents the expectation, $\mathbb{E}[P_i(\xi)P_j(\xi)]$. This property is fundamental; it allows for efficient and stable computation of the coefficients and enables a direct decomposition of the output variance.

The choice of polynomial family is dictated by the distribution of the input variable, a relationship established by the Askey scheme of orthogonal polynomials. For instance :
*   If $\xi \sim \mathcal{U}[-1, 1]$, its PDF is $\rho(\xi) = 1/2$. The corresponding orthogonal polynomials are the **Legendre polynomials**, $L_n(\xi)$. To make them orthonormal, they must be normalized: $P_n(\xi) = \sqrt{2n+1} L_n(\xi)$.
*   If $\xi \sim \mathcal{N}(0, 1)$, its PDF is $\rho(\xi) = (1/\sqrt{2\pi})\exp(-\xi^2/2)$. The corresponding orthogonal polynomials are the **probabilists' Hermite polynomials**, $\mathrm{He}_n(\xi)$. The orthonormal versions are $P_n(\xi) = \mathrm{He}_n(\xi) / \sqrt{n!}$.

For a multidimensional input $\boldsymbol{\Xi}$ with independent components, the multivariate basis $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\Xi})$ is typically formed by a [tensor product](@entry_id:140694) of the univariate orthonormal polynomials corresponding to each component.

#### Truncation Schemes

The infinite PCE series must be truncated to a finite number of terms for practical computation. This is achieved by selecting a [finite set](@entry_id:152247) of multi-indices, $\mathcal{A}$. The choice of $\mathcal{A}$ defines the structure of the [polynomial space](@entry_id:269905) and represents a trade-off between accuracy and complexity. Common choices include :

*   **Total-Degree Truncation**: This scheme includes all polynomials where the sum of the degrees in each variable does not exceed a maximum total degree $p$. The [index set](@entry_id:268489) is $\mathcal{A}^{\text{TD}}_{p,d} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \sum_{i=1}^d \alpha_i \le p\}$. This is the most common choice. The number of terms in this basis, which is the number of coefficients to compute, is given by the combinatorial formula $N = \binom{d+p}{p}$. This number grows polynomially with $p$ but factorially with $d$, posing a challenge for high-dimensional problems (the "curse of dimensionality").

*   **Hyperbolic (or $q$-norm) Truncation**: To mitigate the curse of dimensionality, hyperbolic truncation schemes prioritize low-order interactions. The [index set](@entry_id:268489) is defined as $\mathcal{A}^{\text{HY}}_{p,d,q} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d : \left(\sum_{i=1}^d \alpha_i^q\right)^{1/q} \le p\}$ for a parameter $q \in (0, 1]$. When $q=1$, this reduces to the total-degree scheme. As $q$ decreases towards 0, the scheme more strongly penalizes multi-indices with many non-zero entries (high-order interactions), thus favoring terms that involve fewer input variables. This often leads to sparser, more efficient representations for functions where high-order interactions are less important.

#### Computing the Coefficients

Once a basis and truncation scheme are chosen, the coefficients $c_{\boldsymbol{\alpha}}$ must be determined. This can be done via intrusive or non-intrusive methods.

*   **Intrusive Methods**: An intrusive approach, often based on **Galerkin projection**, reformulates the governing equations of the physical model in the stochastic space. The PCE representation is substituted into the original equations, and the resulting residual is made orthogonal to each basis polynomial. This transforms a stochastic problem into a larger system of coupled, deterministic equations for the PCE coefficients.

    For example, consider a simple system governed by the ODE $\frac{du}{dt} = a(\xi) u(t, \xi)$ . Substituting the PCE ansatz $u(t, \xi) \approx \sum_{m=0}^K u_m(t) \Phi_m(\xi)$ and projecting onto each [basis function](@entry_id:170178) $\Phi_j(\xi)$ yields a system of coupled ODEs for the [time-dependent coefficients](@entry_id:894705) $\mathbf{u}(t) = [u_0(t), \dots, u_K(t)]^T$:
    $$
    \frac{d\mathbf{u}}{dt} = \mathbf{A} \mathbf{u}, \quad \text{where } \mathbf{A}_{jm} = \mathbb{E}[a(\xi) \Phi_j(\xi) \Phi_m(\xi)]
    $$
    This requires modifying the original solver code to implement this new, larger system, hence the term "intrusive." This approach can be highly efficient if feasible but lacks generality as it is tied to the specific governing equations.

*   **Non-Intrusive Methods**: These methods treat the original model $g(\boldsymbol{\Xi})$ as a "black box" and determine the coefficients by running the model at a set of sample points. This makes them applicable to any computational model without modification. The two main non-intrusive approaches are [spectral projection](@entry_id:265201) and regression.

    1.  **Non-Intrusive Spectral Projection**: Leveraging the orthogonality of the basis, the coefficients can be formally expressed as projections: $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\Xi})]$. This expectation is an integral over the input space, which is then approximated numerically using a [quadrature rule](@entry_id:175061):
        $$
        c_{\boldsymbol{\alpha}} \approx \sum_{m=1}^M w^{(m)} g(\boldsymbol{\xi}^{(m)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(m)})
        $$
        where $\{\boldsymbol{\xi}^{(m)}\}$ are quadrature nodes and $\{w^{(m)}\}$ are corresponding weights. To obtain accurate coefficients, the [quadrature rule](@entry_id:175061) must be sufficiently precise. Specifically, if the model output $Y=g(\boldsymbol{\Xi})$ is itself a polynomial of total degree $p$, then to exactly recover the coefficients of its PCE of degree $p$, the integrand $Y \Psi_{\boldsymbol{\alpha}}$ will have a total degree up to $2p$. The [quadrature rule](@entry_id:175061) must therefore be exact for all polynomials of degree up to $2p$ . This often requires using high-order rules like Gaussian quadrature or sparse grids.

    2.  **Least-Squares Regression**: An alternative is to generate a set of $N$ input samples (an experimental design) $\{\boldsymbol{\xi}^{(i)}\}_{i=1}^N$, evaluate the model to get outputs $\{y^{(i)}\}_{i=1}^N$, and then find the coefficients $\mathbf{c}$ that minimize the squared error. This is a linear regression problem. Defining the **design matrix** $\Phi$ with entries $\Phi_{ij} = \psi_j(\boldsymbol{\xi}^{(i)})$ and the observation vector $\mathbf{y}$, the problem is to solve $\mathbf{y} \approx \Phi \mathbf{c}$. The [least-squares solution](@entry_id:152054) is found by solving the **[normal equations](@entry_id:142238)** :
        $$
        (\Phi^T \Phi) \mathbf{c} = \Phi^T \mathbf{y}
        $$
        A unique solution requires at least as many samples as coefficients ($N \ge P+1$) and an invertible Gram matrix $\Phi^T \Phi$. In practice, the matrix can become ill-conditioned if samples are poorly distributed, leading to [numerical instability](@entry_id:137058). This can be mitigated by using [space-filling sampling](@entry_id:1132002) strategies (like Latin Hypercube Sampling), increasing the sample size $N$, or using [regularization techniques](@entry_id:261393) like Tikhonov regularization. In cases of noisy or heteroscedastic data, a **Weighted Least Squares (WLS)** formulation can be employed to give more weight to more reliable data points .

### Gaussian Process Regression (Kriging): A Probabilistic Approach

Gaussian Process regression, also known in geostatistics as Kriging, offers a fundamentally different, non-parametric approach to [surrogate modeling](@entry_id:145866). Instead of positing a specific functional form like a polynomial, it places a probability distribution over the space of all possible functions.

#### The Gaussian Process Framework

A **Gaussian Process (GP)** is a stochastic process where any finite collection of points has a multivariate Gaussian distribution. A GP is fully specified by a **mean function** $m(x)$ and a **[covariance function](@entry_id:265031)** or **kernel** $k(x, x')$. We write:
$$
f(x) \sim \mathcal{GP}(m(x), k(x, x'))
$$
The mean function represents the prior expected value of the function at any point, while the kernel encodes the correlation between function values at different points. The choice of kernel is paramount as it imparts prior assumptions about the function's properties, such as smoothness and lengthscale.

Given a set of $n$ noise-free training observations $\{(x_i, y_i)\}_{i=1}^n$, the GP framework uses Bayesian conditioning to update the prior distribution into a posterior distribution over functions. The prediction at a new point $x_*$ is not a single value but a full Gaussian distribution, characterized by a [posterior mean](@entry_id:173826) and a posterior variance.

#### The Predictive Equations and Interpolation

For a GP prior with mean $m(x)$ and kernel $k(x,x')$, and noise-free training data $\mathbf{y}$ at inputs $X$, the [posterior predictive distribution](@entry_id:167931) at a test point $x_*$ is $\mathcal{N}(\mu_*(x_*), \sigma^2_*(x_*))$, where :
*   **Posterior Mean**: $\mu_*(x_*) = m(x_*) + \mathbf{k}_*^T \mathbf{K}^{-1} (\mathbf{y} - \mathbf{m})$
*   **Posterior Variance**: $\sigma^2_*(x_*) = k_{**} - \mathbf{k}_*^T \mathbf{K}^{-1} \mathbf{k}_*$

Here, $\mathbf{K}$ is the $n \times n$ covariance matrix of the training inputs with entries $K_{ij} = k(x_i, x_j)$, $\mathbf{k}_*$ is the vector of covariances between the training inputs and the test point, $k_{**} = k(x_*, x_*)$, and $\mathbf{m}$ is the prior mean evaluated at the training inputs.

A remarkable property of GP regression in the noise-free case is that it is an **exact interpolator**. If we evaluate the [posterior mean](@entry_id:173826) at any training input $x_i$, it returns the observed value $y_i$. Furthermore, the posterior variance at any training input $x_i$ is exactly zero . This means the model is perfectly certain about the function's value at the points it has already seen. This property holds regardless of the chosen prior mean function, provided the kernel matrix $\mathbf{K}$ is invertible. The posterior variance $\sigma^2_*(x_*)$ is a powerful feature: it provides a built-in, local measure of the surrogate's **epistemic uncertainty**. The variance is low near training data and grows in regions far from any data, signaling where the surrogate's predictions are less reliable .

#### The Role of the Covariance Kernel

The choice of kernel determines almost all properties of the GP surrogate. A widely used choice is the **squared-exponential (SE) kernel**:
$$
k(x,x') = \sigma^2 \exp\left(-\frac{(x - x')^2}{2\ell^2}\right)
$$
This kernel is defined by two hyperparameters: the signal variance $\sigma^2$ and the characteristic **lengthscale** $\ell$.
*   $\sigma^2$ controls the overall vertical scale of variation of the function.
*   $\ell$ is arguably the more critical parameter. It dictates the distance over which function values are strongly correlated. A large $\ell$ implies that the function is smooth and varies slowly, so data points have a long-range influence. A small $\ell$ implies the function is "wiggly" and decorrelates quickly, so data point influence is highly localized .

The lengthscale $\ell$ profoundly affects the surrogate's behavior. A larger $\ell$ leads to a smoother predictive mean and slower reversion to the prior mean far from data. Conversely, as $\ell \to 0$, the GP becomes a "nugget" model where data points have no influence beyond their immediate vicinity. A key property of the SE kernel is that it is infinitely differentiable, which means that functions drawn from a GP with an SE kernel are [almost surely](@entry_id:262518) infinitely differentiable. This makes it an excellent choice for very smooth functions but, as we will see, a poor choice for non-smooth ones.

### Advanced Topics and Practical Considerations

While powerful, both PCE and GP regression have their limitations, particularly when dealing with the complex, multiscale phenomena often encountered in [scientific computing](@entry_id:143987).

#### Approximating Non-Smooth and Discontinuous Functions

Many physical systems exhibit non-smooth behavior, such as phase transitions or material fracture, which can manifest as kinks or even jump discontinuities in the model output. Approximating such functions presents a significant challenge for standard surrogate models .

*   **Challenges for PCE**: When approximating a [discontinuous function](@entry_id:143848) (e.g., a Heaviside [step function](@entry_id:158924)) with a polynomial series, one loses the desirable **[spectral convergence](@entry_id:142546)** (error decreases exponentially with polynomial degree $p$). Instead, the convergence degrades to an algebraic rate, such as $O(p^{-1})$ for the [mean-square error](@entry_id:194940) of a [step function](@entry_id:158924). Moreover, the PCE approximation will exhibit the **Gibbs phenomenon**: persistent over- and under-shoots near the discontinuity whose magnitude does not vanish as $p \to \infty$. While the approximation still converges in a mean-square sense, the [pointwise convergence](@entry_id:145914) is poor near the jump.

*   **Challenges for GP**: A GP with a smooth kernel, like the SE kernel, assumes the underlying function is smooth. The [posterior mean](@entry_id:173826), being a combination of smooth [kernel functions](@entry_id:1126899), is itself smooth and cannot represent a true discontinuity. When forced to fit discontinuous data, the GP surrogate may exhibit [spurious oscillations](@entry_id:152404) near the jump. The [approximation error](@entry_id:138265) will be limited by the regularity of the true function, leading to slow algebraic convergence rates. While using a "rougher" kernel, such as one from the **Matérn family**, can better align the prior assumptions with a non-smooth reality and improve the approximation of kinks, even these models produce continuous [sample paths](@entry_id:184367) and thus cannot represent a true [jump discontinuity](@entry_id:139886) .

#### Hybrid Models: PC-Kriging

To combine the strengths of both paradigms, hybrid models have been developed. **PC-Kriging** is a prominent example that uses a PCE to model the global trend of a function, while a GP models the localized, correlated residuals . The model structure is:
$$
f(\boldsymbol{\xi}) = \underbrace{\sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})}_{\text{Global PCE Trend}} + \underbrace{Z(\boldsymbol{\xi})}_{\text{Local GP Residual}}
$$
This structure, formally known as Universal Kriging, is highly flexible. The PCE component, using its global [orthogonal basis](@entry_id:264024), efficiently captures the large-scale, smooth behavior of the function. The GP component then acts as a local corrector, modeling the remaining variations that the truncated PCE misses. This leverages the [spectral efficiency](@entry_id:270024) of PCE for global trends and the probabilistic interpolation power of GP for local details.

Training a PC-Kriging model requires the joint estimation of both the PCE coefficients and the GP kernel hyperparameters, typically via a concentrated or profile maximum likelihood approach. This ensures an optimal partitioning of the function's variability between the global trend and the local residual process. The model gracefully reduces to its constituent parts in limiting cases: if the GP residual variance shrinks to zero, it becomes a pure PCE model; if the PCE trend is reduced to a constant, it becomes an Ordinary Kriging model . This hybrid approach often provides more accurate and robust surrogates for complex functions than either method alone.