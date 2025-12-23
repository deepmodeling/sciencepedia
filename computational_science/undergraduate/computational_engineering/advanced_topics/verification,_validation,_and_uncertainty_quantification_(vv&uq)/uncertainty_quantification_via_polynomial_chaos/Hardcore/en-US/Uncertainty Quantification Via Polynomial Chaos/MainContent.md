## Introduction
In modern computational engineering and science, accurately predicting the behavior of complex systems is paramount. However, our models are inevitably subject to uncertainty, stemming from variable material properties, imprecise measurements, or unknown environmental conditions. Ignoring this uncertainty can lead to unreliable predictions and flawed designs. Uncertainty Quantification (UQ) provides the mathematical and computational tools to manage this challenge. This article introduces a cornerstone of modern UQ: **Polynomial Chaos Expansion (PCE)**. While brute-force methods like Monte Carlo simulation can quantify uncertainty, they often require thousands or millions of model evaluations, rendering them impractical for expensive computational models. PCE addresses this knowledge gap by offering an elegant and highly efficient alternative. It constructs a compact, analytical [surrogate model](@entry_id:146376) of the complex system, capturing the full impact of input uncertainties.

Across the following chapters, you will gain a comprehensive understanding of this powerful technique. **Principles and Mechanisms** will demystify the theory, from the [spectral representation](@entry_id:153219) of random variables to the practical computation of PCE coefficients. **Applications and Interdisciplinary Connections** will showcase the versatility of PCE, demonstrating its use in solving real-world problems in fields from structural mechanics and robotics to [climate science](@entry_id:161057) and machine learning. Finally, **Hands-On Practices** will provide opportunities to apply these concepts to concrete examples, solidifying your understanding. By the end, you will be equipped with the foundational knowledge to leverage Polynomial Chaos for robust analysis and design in the face of uncertainty.

## Principles and Mechanisms

This chapter delves into the foundational principles and core mechanisms of Polynomial Chaos Expansion (PCE), a powerful framework for propagating uncertainty through computational models. We will construct the methodology from first principles, explore its practical implementation, and demonstrate its utility for extracting valuable [statistical information](@entry_id:173092).

### Spectral Representation of Uncertainty

The central premise of Polynomial Chaos is to represent a model's output quantity of interest, which is a random variable due to its dependence on random inputs, not as a collection of sample points, but as a spectral expansion. Let $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$ be a vector of [independent random variables](@entry_id:273896) that parameterize the uncertainty in a model, and let $Y(\boldsymbol{\xi})$ be a scalar output of interest. The PCE method approximates $Y(\boldsymbol{\xi})$ as a series of prescribed polynomial basis functions $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$:

$$
Y(\boldsymbol{\xi}) \approx Y_P(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$

Here, $\mathcal{A}$ is a [finite set](@entry_id:152247) of multi-indices $\boldsymbol{\alpha} = (\alpha_1, \dots, \alpha_d)$, the $c_{\boldsymbol{\alpha}}$ are deterministic coefficients to be determined, and the $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ are multivariate polynomials. This expansion effectively separates the stochasticity, which is captured by the basis functions $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$, from the model's specific response, which is encoded in the deterministic coefficients $c_{\boldsymbol{\alpha}}$. The power of this approach hinges on a specific, crucial property of the basis functions: [orthonormality](@entry_id:267887).

### The Foundation: Orthonormal Polynomials and Galerkin Projection

To make the computation of the coefficients $c_{\boldsymbol{\alpha}}$ efficient and the resulting expansion meaningful, the polynomial basis must be chosen carefully. We define an inner product between two real-valued functions, $f(\boldsymbol{\xi})$ and $g(\boldsymbol{\xi})$, with respect to the probability measure of $\boldsymbol{\xi}$. If $\rho(\boldsymbol{\xi})$ is the [joint probability density function](@entry_id:177840) (PDF) of $\boldsymbol{\xi}$, this inner product is defined as the expectation of their product:

$$
\langle f, g \rangle = \mathbb{E}[f(\boldsymbol{\xi})g(\boldsymbol{\xi})] = \int_{\mathcal{S}_{\boldsymbol{\xi}}} f(\boldsymbol{\xi}) g(\boldsymbol{\xi}) \rho(\boldsymbol{\xi}) d\boldsymbol{\xi}
$$

where $\mathcal{S}_{\boldsymbol{\xi}}$ is the support of the random vector $\boldsymbol{\xi}$. A set of polynomials $\{\Psi_{\boldsymbol{\alpha}}\}$ is said to be **orthonormal** with respect to this inner product if it satisfies the following condition for any two multi-indices $\boldsymbol{\alpha}$ and $\boldsymbol{\beta}$:

$$
\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}
$$

where $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the multidimensional Kronecker delta, which is $1$ if $\boldsymbol{\alpha} = \boldsymbol{\beta}$ and $0$ otherwise. This single condition implies two properties: **orthogonality** ($\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = 0$ for $\boldsymbol{\alpha} \neq \boldsymbol{\beta}$) and **normalization** ($\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\alpha}} \rangle = 1$).

The utility of an orthonormal basis becomes immediately clear when determining the coefficients $c_{\boldsymbol{\alpha}}$. The coefficients of the PCE are determined by **Galerkin projection**, which seeks the best approximation in a mean-square sense. This is achieved by ensuring that the error of the approximation, $Y(\boldsymbol{\xi}) - Y_P(\boldsymbol{\xi})$, is orthogonal to the space spanned by the basis functions. That is, for every basis function $\Psi_{\boldsymbol{\beta}}$ in our set:

$$
\langle Y(\boldsymbol{\xi}) - \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}), \Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi}) \rangle = 0
$$

By linearity of the inner product, this becomes:

$$
\langle Y, \Psi_{\boldsymbol{\beta}} \rangle - \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = 0
$$

If the basis is orthonormal, $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, the summation collapses to a single term, yielding a remarkably simple formula for the coefficients:

$$
c_{\boldsymbol{\beta}} = \langle Y, \Psi_{\boldsymbol{\beta}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\beta}}(\boldsymbol{\xi})]
$$

This is the cornerstone of PCE. The coefficients are simply the projection of the model output onto each basis function. If the basis were merely orthogonal (i.e., $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\alpha}} \rangle = h_{\boldsymbol{\alpha}} \neq 1$), the formula would be $c_{\boldsymbol{\beta}} = \langle Y, \Psi_{\boldsymbol{\beta}} \rangle / h_{\boldsymbol{\beta}}$. If the basis were not orthogonal at all, one would have to solve a dense linear system of equations (the "normal equations"), which is computationally far more demanding. Thus, the selection of an [orthonormal basis](@entry_id:147779) is paramount for both theoretical elegance and computational efficiency.

### Choosing the Right Basis: The Wiener-Askey Scheme and Isoprobabilistic Transforms

The requirement that the polynomial basis be orthogonal with respect to the input probability measure begs the question: how do we find such polynomials for a given input distribution? The **Wiener-Askey scheme** provides a canonical map between several [common probability distributions](@entry_id:171827) and corresponding families of [classical orthogonal polynomials](@entry_id:192726). Key pairings include:

*   **Gaussian** distribution ($\xi \sim \mathcal{N}(\mu, \sigma^2)$): **Hermite** polynomials.
*   **Uniform** distribution ($\xi \sim \mathcal{U}(a,b)$): **Legendre** polynomials.
*   **Gamma** distribution: **Laguerre** polynomials.
*   **Beta** distribution: **Jacobi** polynomials.

For a problem with multiple independent inputs, the multivariate basis $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ is simply the tensor product of the appropriate univariate polynomials for each input, i.e., $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^{d} \psi_{\alpha_i}^{(i)}(\xi_i)$.

A practical challenge arises when an input variable's distribution is not one of these classical types. A common example in engineering is a Young's modulus that is modeled by a **[lognormal distribution](@entry_id:261888)** to ensure its value is always positive. The [lognormal distribution](@entry_id:261888) does not have a corresponding classical polynomial family. The solution is to use an **isoprobabilistic transform**. By definition, if a variable $E$ is lognormal, then its logarithm $\ln E$ is Gaussian. We can thus define a standard normal variable $\xi \sim \mathcal{N}(0,1)$ and relate it to $E$ via:

$$
\xi = \frac{\ln E - \mu_g}{\sigma_g} \quad \iff \quad E(\xi) = \exp(\mu_g + \sigma_g \xi)
$$

where $\mu_g$ and $\sigma_g$ are the mean and standard deviation of $\ln E$. Instead of trying to build a PCE for the output $Y(E)$ in terms of the lognormal variable $E$, we re-express the output as a function of the standard normal variable, $Y(E(\xi))$, and build the PCE in terms of $\xi$ using the appropriate Hermite polynomials. This technique of transforming the inputs into variables with canonical distributions is fundamental to the practical application of PCE. For correlated non-Gaussian inputs, this idea extends to multivariate transforms like the Nataf transform.

### Practical Implementation: Intrusive vs. Non-Intrusive Methods

With the theoretical framework established, we turn to the practical computation of the coefficients $c_{\boldsymbol{\alpha}}$. There are two main families of methods: intrusive and non-intrusive.

#### Intrusive Methods

An **intrusive** or **Stochastic Galerkin** method takes the governing equations of the model (e.g., a system of PDEs) and reformulates them in the stochastic space. This is done by substituting the PCE for all random [state variables](@entry_id:138790) directly into the equations. A Galerkin projection is then applied in the random dimension, yielding a large, coupled system of deterministic equations for the PCE coefficients of the state variables.

*   **Advantage**: This approach is mathematically elegant and often highly accurate, as it finds the solution that is optimal in the mean-square sense for the chosen [polynomial space](@entry_id:269905).
*   **Disadvantage**: It is "intrusive" because it requires extensive, and often prohibitively complex, modifications to the source code of the existing deterministic solver. For large, complex "legacy" codes, this is typically impractical.

#### Non-Intrusive Methods

**Non-intrusive** methods treat the deterministic solver as a "black box" that can be evaluated for given input values, but whose internal workings are not modified. This makes them exceptionally practical. The coefficients $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$ are computed by approximating these projection integrals.

A primary non-intrusive approach is **[stochastic collocation](@entry_id:174778)** using numerical quadrature. The integral is approximated by a weighted sum of function evaluations at specific points (nodes):

$$
c_{\boldsymbol{\alpha}} = \int Y(\boldsymbol{\xi})\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})\rho(\boldsymbol{\xi}) d\boldsymbol{\xi} \approx \sum_{j=1}^{M} w_j Y(\boldsymbol{\xi}_j) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}_j)
$$

Here, $\{(\boldsymbol{\xi}_j, w_j)\}_{j=1}^M$ are the nodes and weights of a suitable [quadrature rule](@entry_id:175061) (e.g., Gauss-Legendre quadrature for uniform inputs). To compute the PCE, one simply runs the deterministic solver $M$ times at the prescribed nodes $\{\boldsymbol{\xi}_j\}$ to obtain the values $\{Y(\boldsymbol{\xi}_j)\}$ and then performs the summation for each coefficient $c_{\boldsymbol{\alpha}}$. Because each of the $M$ solver runs is independent, this process is [embarrassingly parallel](@entry_id:146258), making it highly suitable for modern computing clusters.

Another popular non-intrusive method is based on **regression**. In this approach, one generates a larger number of input samples $N$, runs the solver to obtain the corresponding outputs $\{Y(\boldsymbol{\xi}_i)\}_{i=1}^N$, and then finds the coefficients $c_{\boldsymbol{\alpha}}$ that minimize the least-squares error $\sum_{i=1}^N (Y(\boldsymbol{\xi}_i) - \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}_i))^2$.

The central trade-off is clear: intrusive methods offer optimality but are difficult to implement, while non-intrusive methods are vastly more practical and easier to deploy but introduce an additional layer of approximation error (quadrature or regression error) on top of the PCE truncation error.

### The Payoff I: Computing Statistical Moments

Once the PCE coefficients $\{c_{\boldsymbol{\alpha}}\}$ are computed, they form a highly compact surrogate model from which rich [statistical information](@entry_id:173092) can be extracted analytically, without any further runs of the original expensive model.

The mean (expectation) of the output $Y$ is given directly by the zeroth-order coefficient, as all higher-order orthonormal polynomials have [zero mean](@entry_id:271600):

$$
\mathbb{E}[Y] = \mathbb{E}[\sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\alpha}}] = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}\mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = c_{\boldsymbol{0}} \mathbb{E}[\Psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}
$$

since $\Psi_{\boldsymbol{0}} \equiv 1$.

The variance of $Y$ can also be computed directly from the coefficients. Using the definition $\text{Var}(Y) = \mathbb{E}[Y^2] - (\mathbb{E}[Y])^2$:

$$
\text{Var}(Y) = \mathbb{E}[(\sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\alpha}})^2] - c_{\boldsymbol{0}}^2 = \sum_{\boldsymbol{\alpha}, \boldsymbol{\beta}} c_{\boldsymbol{\alpha}}c_{\boldsymbol{\beta}}\mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}] - c_{\boldsymbol{0}}^2
$$

Due to [orthonormality](@entry_id:267887), $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, so the expression simplifies to:

$$
\text{Var}(Y) = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}}^2 - c_{\boldsymbol{0}}^2 = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}}^2
$$

Thus, the variance is simply the sum of the squares of all coefficients except the zeroth-order one.

For example, consider a degree-2 PCE in one variable with coefficients $c_0=2$, $c_1=-1$, and $c_2=1/2$. The mean and variance are immediately computed as:

$$
\mathbb{E}[Y] = c_0 = 2
$$
$$
\text{Var}(Y) = c_1^2 + c_2^2 = (-1)^2 + (\frac{1}{2})^2 = 1 + \frac{1}{4} = \frac{5}{4}
$$
This ability to derive statistical moments instantly is a significant advantage over traditional Monte Carlo methods, which would require thousands of model evaluations to achieve similar accuracy.

### The Payoff II: Global Sensitivity Analysis

Beyond simple moments, the PCE provides a complete decomposition of the output variance, which enables a comprehensive **Global Sensitivity Analysis (GSA)**. GSA seeks to apportion the uncertainty in the output $Y$ to the uncertainty in the different input variables $\xi_i$. This is contrasted with [local sensitivity analysis](@entry_id:163342), which only examines the effect of small perturbations around a nominal point (i.e., computing derivatives).

The PCE provides a functional **Analysis of Variance (ANOVA)** decomposition. The total variance, $V = \sum_{\boldsymbol{\alpha} \neq \mathbf{0}} c_{\boldsymbol{\alpha}}^2$, can be partitioned into contributions from each input variable and their interactions. This allows for the direct computation of **Sobol' indices**.

Let $\text{supp}(\boldsymbol{\alpha}) := \{j \in \{1,\dots,d\} : \alpha_j > 0\}$ be the set of indices of variables on which the polynomial $\Psi_{\boldsymbol{\alpha}}$ depends.

The **first-order Sobol' index** $S_i$ measures the direct contribution of input $\xi_i$ to the total variance. It is computed by summing the squared coefficients of all basis functions that depend *only* on $\xi_i$:

$$
S_i = \frac{V_i}{V} = \frac{\sum_{\boldsymbol{\alpha}: \text{supp}(\boldsymbol{\alpha})=\{i\}} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \neq \mathbf{0}} c_{\boldsymbol{\beta}}^2}
$$

Similarly, **higher-order indices** $S_{\mathfrak{u}}$ that quantify the variance from the pure interaction of a set of variables $\mathfrak{u}$ are computed by summing over coefficients whose basis functions depend exactly on that set of variables.

The **total-effect Sobol' index** $S_{T_i}$ measures the contribution of $\xi_i$, including its main effect and all interactions with other variables. It is computed by summing the squared coefficients of all basis functions that have *any* dependence on $\xi_i$:

$$
S_{T_i} = \frac{\sum_{\boldsymbol{\alpha}: i \in \text{supp}(\boldsymbol{\alpha})} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \neq \mathbf{0}} c_{\boldsymbol{\beta}}^2} = \frac{\sum_{\boldsymbol{\alpha}: \alpha_i > 0} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\beta} \neq \mathbf{0}} c_{\boldsymbol{\beta}}^2}
$$

Remarkably, all of these sensitivity indices are obtained as a simple post-processing step once the PCE coefficients are known, with no additional evaluations of the computational model required. This makes PCE an exceptionally efficient tool for GSA.

### Challenges and Limitations

Despite its power, PCE is not without its challenges and limitations.

#### The Curse of Dimensionality

The primary challenge for PCE is the **curse of dimensionality**. As the number of random input dimensions, $d$, increases, the number of basis functions required to maintain a given polynomial accuracy grows rapidly. For a total polynomial degree $p$, the number of basis functions is given by a combinatorial term:

$$
|\mathcal{A}| = \binom{p+d}{d} = \frac{(p+d)!}{p! d!} \approx \frac{d^p}{p!} \text{ for large } d
$$

This [polynomial growth](@entry_id:177086) in $d$, while better than exponential, can still become computationally prohibitive for even moderate $d$ and $p$. This combinatorial explosion directly impacts the size of the coupled system in intrusive Galerkin methods. For non-intrusive methods, the curse is often even more severe. A standard [tensor-product quadrature](@entry_id:145940) rule with $q$ points per dimension requires $q^d$ model evaluations, an [exponential growth](@entry_id:141869) that quickly becomes intractable. While advanced techniques like sparse grids can mitigate this, the [curse of dimensionality](@entry_id:143920) remains the central obstacle to applying PCE in very high-dimensional problems.

#### Convergence for Non-Smooth Models

PCE relies on approximating a function with global polynomials. The convergence rate of this approximation depends heavily on the smoothness of the model response $Y(\boldsymbol{\xi})$. If $Y(\boldsymbol{\xi})$ is analytic, the PCE converges exponentially fast. However, many real-world models exhibit non-smooth behavior, such as discontinuities arising from [phase changes](@entry_id:147766) or the activation of [contact constraints](@entry_id:171598).

When a global PCE is used to approximate a function with a jump discontinuity, it suffers from the **Gibbs phenomenon**. The polynomial approximation will exhibit [spurious oscillations](@entry_id:152404) near the discontinuity. While the approximation will converge in the mean-square ($L^2$) sense, the convergence rate slows from exponential to a much slower algebraic rate (e.g., $O(1/p)$). Furthermore, the amplitude of the over- and undershoots near the jump does not decay as the polynomial order $p$ increases, preventing uniform convergence. This behavior is a fundamental property of approximating [discontinuous functions](@entry_id:139518) with global smooth bases and is not resolved by simply changing the polynomial family (e.g., from Legendre to Hermite). This limitation necessitates the use of more advanced techniques, such as multi-element PCE or adaptive methods, for problems with known discontinuities.