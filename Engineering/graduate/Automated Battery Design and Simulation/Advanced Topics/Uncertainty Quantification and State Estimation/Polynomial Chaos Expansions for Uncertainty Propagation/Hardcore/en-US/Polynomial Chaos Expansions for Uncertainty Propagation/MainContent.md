## Introduction
In the world of scientific and engineering simulation, from designing next-generation batteries to assessing [cardiovascular risk](@entry_id:912616), deterministic predictions are often insufficient. Real-world systems are governed by parameters—material properties, operating conditions, manufacturing tolerances—that are inherently uncertain. Understanding how this input uncertainty propagates through a complex model to affect its output is the central challenge of Uncertainty Quantification (UQ). Traditional methods like Monte Carlo simulation can be prohibitively expensive, requiring thousands of runs of computationally intensive models. Polynomial Chaos Expansions (PCE) offer a powerful and efficient alternative, transforming the problem of uncertainty propagation into the construction of an elegant, analytical surrogate model.

This article provides a comprehensive exploration of the PCE methodology, designed to equip you with the theoretical knowledge and practical understanding to apply it effectively. We will embark on a structured journey across three key chapters. First, in **"Principles and Mechanisms,"** we will delve into the mathematical foundations of PCE, exploring how randomness is represented, how appropriate polynomial bases are chosen via the Wiener-Askey scheme, and how the expansion coefficients are computed. Next, **"Applications and Interdisciplinary Connections"** will showcase the versatility of PCE in practice, demonstrating its use for global sensitivity analysis, reliability assessment, and robust design in fields ranging from battery engineering to biomechanics. Finally, **"Hands-On Practices"** will present targeted exercises to solidify your understanding of key implementation details and challenges. We begin by laying the theoretical groundwork that makes these powerful applications possible.

## Principles and Mechanisms

This chapter delineates the fundamental principles and operational mechanisms of Polynomial Chaos Expansions (PCE) as a rigorous framework for [uncertainty propagation](@entry_id:146574) in scientific and engineering models. We transition from the abstract representation of uncertainty to the construction of concrete, computable surrogate models, focusing on the mathematical underpinnings, practical implementation strategies, and the analytical power that PCE affords.

### Representing Randomness: From Variables to Functions

In the context of battery design and simulation, a quantity of interest, such as cell capacity or terminal voltage, is rarely a deterministic value. It is the output of a complex physical system, $Y = g(\boldsymbol{\xi})$, whose behavior is governed by a set of input parameters, $\boldsymbol{\xi} = (\xi_1, \dots, \xi_d)$, that are themselves uncertain. These parameters—representing manufacturing tolerances, material properties, or operating conditions—are best described as random variables. Consequently, the output $Y$ is also a random variable. The central task of [uncertainty propagation](@entry_id:146574) is to characterize the probability distribution of $Y$ given the distributions of the inputs $\boldsymbol{\xi}$.

Polynomial Chaos Expansion offers a powerful approach to this problem by reframing it. Instead of propagating statistical moments or sampling the distribution of $Y$, PCE seeks to construct an analytical representation of the random variable $Y$ itself. This is achieved by expanding $Y$ in a series of basis functions that are dependent on the underlying random inputs $\boldsymbol{\xi}$. The concept is analogous to how a deterministic function can be represented by a Fourier series, which is an infinite sum of simple sinusoidal basis functions. In PCE, we represent a random function in an infinite series of polynomials that are tailored to the probabilistic nature of the inputs.

Formally, we operate within the **Hilbert space of square-integrable random variables**, denoted $L^2(\Omega)$. This space consists of all random variables $Y$ defined on a probability space $(\Omega, \mathcal{F}, \mathbb{P})$ that have a finite second moment, i.e., $\mathbb{E}[Y^2] \lt \infty$. This space is equipped with an inner product defined by the expectation of the product of two random variables: $\langle U, V \rangle = \mathbb{E}[UV]$. The central theorem of Hilbert space theory states that any element can be represented as a generalized Fourier series with respect to any complete [orthonormal basis](@entry_id:147779) of the space.

A **Polynomial Chaos Expansion** is precisely such a series, where the chosen basis, $\{\Psi_{\boldsymbol{\alpha}}\}_{\boldsymbol{\alpha}\in\mathbb{N}_0^d}$, consists of multivariate polynomials in the random vector $\boldsymbol{\xi}$. The expansion takes the form:

$$
Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})
$$

Here, $\boldsymbol{\alpha}$ is a multi-index, a vector of non-negative integers $(\alpha_1, \dots, \alpha_d)$, that identifies each polynomial in the basis. The coefficients $c_{\boldsymbol{\alpha}}$ are real-valued scalars. For this representation to be mathematically sound and for the series to converge to $Y$ in the mean-square sense (i.e., $\lim_{P\to\infty} \mathbb{E}[(Y - Y_P)^2] = 0$, where $Y_P$ is a truncated sum), two conditions are essential :
1. The model output must have [finite variance](@entry_id:269687), i.e., $Y \in L^2(\Omega)$.
2. The polynomial basis $\{\Psi_{\boldsymbol{\alpha}}\}$ must be **orthonormal** with respect to the probability measure of $\boldsymbol{\xi}$ and **complete** in $L^2(\Omega)$.

Orthonormality means that $\mathbb{E}[\Psi_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, where $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the Kronecker delta. Completeness ensures that any function in $L^2(\Omega)$ can be approximated to arbitrary precision by a linear combination of the basis functions. Under these conditions, the coefficients $c_{\boldsymbol{\alpha}}$ are uniquely determined by the [orthogonal projection](@entry_id:144168) of $Y$ onto each [basis function](@entry_id:170178):

$$
c_{\boldsymbol{\alpha}} = \langle Y, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[Y \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]
$$

This formula is the cornerstone of PCE, providing the theoretical means to determine the expansion coefficients.

### The Wiener-Askey Scheme: Matching Polynomials to Distributions

The critical choice in constructing a PCE is the selection of an appropriate orthogonal polynomial basis. This choice is not arbitrary; it is dictated by the probability distribution of the input random variables $\boldsymbol{\xi}$. The orthogonality of the basis polynomials is defined with respect to an inner product weighted by the probability density function (PDF), $\rho(\boldsymbol{\xi})$, of the inputs. For a univariate input $\xi$ with PDF $\rho(\xi)$, a polynomial family $\{P_n(\xi)\}$ is orthogonal if:

$$
\int_S P_m(\xi) P_n(\xi) \rho(\xi) d\xi = h_n \delta_{mn}
$$

where $h_n > 0$ is a [normalization constant](@entry_id:190182) and $S$ is the support of the distribution. The family of [classical orthogonal polynomials](@entry_id:192726) that correspond to [common probability distributions](@entry_id:171827) is cataloged by the **Wiener-Askey scheme**. This scheme provides a direct mapping from the type of input uncertainty to the correct polynomial family, ensuring the crucial [orthonormality](@entry_id:267887) condition is met . For independent inputs, the multivariate basis is simply the [tensor product](@entry_id:140694) of the appropriate univariate polynomials.

Key correspondences relevant to battery modeling include:
- **Gaussian Distribution:** For an input $\xi \sim \mathcal{N}(\mu, \sigma^2)$, after standardizing to $Z = (\xi-\mu)/\sigma \sim \mathcal{N}(0,1)$, the corresponding [orthogonal polynomials](@entry_id:146918) are the **Hermite polynomials**, which are orthogonal with respect to the weight function $w(z) \propto \exp(-z^2/2)$.
- **Uniform Distribution:** For an input $\xi \sim \mathcal{U}(a, b)$, after standardizing to $Z = (2\xi - (a+b))/(b-a) \sim \mathcal{U}(-1,1)$, the appropriate basis is the **Legendre polynomials**, orthogonal with respect to the constant weight $w(z)=1$ on $[-1,1]$.
- **Gamma Distribution:** For a Gamma-distributed input, the **Laguerre polynomials** form the [orthogonal basis](@entry_id:264024).
- **Beta Distribution:** For an input on a bounded interval, typically modeled as a Beta distribution, the **Jacobi polynomials** are the correct choice. A variable $U \sim \text{Beta}(a,b)$ on $[0,1]$ requires an affine map $Z = 2U-1$ to the canonical Jacobi support of $[-1,1]$.

This selection process is a foundational step in applying PCE. For instance, in modeling a lithium-ion cell, uncertain parameters might be assigned distributions based on physical reasoning and empirical data . A reaction rate constant $k$, which must be positive and often exhibits multiplicative scatter, is well-modeled by a **Lognormal distribution**. Since $\ln(k)$ is normally distributed, the PCE for $k$ would be built using **Hermite polynomials** of the underlying standard normal variable. A parameter like porosity $\varepsilon$, which is physically constrained to the interval $(0,1)$, is naturally modeled by a **Beta distribution**, necessitating the use of **Jacobi polynomials** for its expansion.

All [classical orthogonal polynomials](@entry_id:192726) share a fundamental property: they satisfy a **[three-term recurrence relation](@entry_id:176845)**. This relation allows for the stable and efficient computation of the polynomial sequence. For example, the orthonormal Legendre polynomials on $[-1,1]$ can be generated via such a recurrence, starting from $P_0(x)$ .

### Handling General Input Dependencies: The Nataf Transform

The Wiener-Askey scheme is most straightforwardly applied when the input variables are independent and follow one of the [standard distributions](@entry_id:190144). Real-world engineering problems, however, often feature inputs that are both correlated and have marginal distributions not found in the classical scheme. The **Nataf transform** provides a rigorous framework to handle this complexity by mapping a general random vector $X$ into a vector of independent standard normal variables $\tilde{Z}$, upon which a standard Hermite [polynomial chaos expansion](@entry_id:174535) can be constructed .

This transformation proceeds in two stages:
1.  **Isoprobabilistic Transformation:** Each component $X_i$ of the input vector is transformed to a standard normal variable $Z_i$ using its marginal [cumulative distribution function](@entry_id:143135) (CDF), $F_i$, and the inverse standard normal CDF, $\Phi^{-1}$. The transformation is $Z_i = \Phi^{-1}(F_i(X_i))$. This step preserves the probability measure of each marginal but transforms its distribution to a standard normal. The resulting vector $Z$ has standard normal marginals, but it inherits a correlation structure from $X$, described by a [correlation matrix](@entry_id:262631) $R_Z$.
2.  **Decorrelation:** The correlated normal vector $Z \sim \mathcal{N}(0, R_Z)$ is then decorrelated into a vector of independent standard normal variables $\tilde{Z}$ using a linear transformation. This is typically achieved using the Cholesky decomposition of the [correlation matrix](@entry_id:262631), $R_Z = LL^\top$. The final transformation is $\tilde{Z} = L^{-1}Z$. The resulting vector $\tilde{Z}$ has an identity covariance matrix, meaning its components are independent and standard normal.

The composite mapping $X \mapsto \tilde{Z}$ is a differentiable transformation whose Jacobian determinant can be calculated, enabling a formal change of variables between the physical space and the independent standard [normal space](@entry_id:154487) . PCE can then be readily applied in the space of $\tilde{Z}$ using Hermite polynomials.

### The Challenge of Dimensionality in Practice

The theoretical PCE involves an [infinite series](@entry_id:143366). For any practical application, this series must be truncated to a finite number of terms. This is achieved by selecting a [finite set](@entry_id:152247) of multi-indices, $\mathcal{A}$. The choice of this [index set](@entry_id:268489) has profound implications for the accuracy and computational cost of the PCE.

A common and systematic approach is **total-degree truncation**, where the basis includes all polynomials for which the sum of the degrees in each variable does not exceed a certain integer $p$. The [index set](@entry_id:268489) is $\mathcal{A} = \{\boldsymbol{\alpha} \in \mathbb{N}_0^d \mid \sum_{i=1}^d \alpha_i \le p\}$. The number of terms in such an expansion, $P = |\mathcal{A}|$, is given by the combinatorial formula :

$$
P = \binom{d+p}{d} = \frac{(d+p)!}{d!p!}
$$

While elegant, this formula reveals a severe practical limitation of PCE: the **curse of dimensionality**. The number of basis functions $P$ grows polynomially with the number of uncertain dimensions $d$ (for a fixed degree $p$) and polynomially with the degree $p$ (for a fixed dimension $d$). For high-dimensional battery models with tens of uncertain parameters ($d \ge 10$), even a modest degree ($p=3$ or $4$) can lead to an intractably large number of basis functions, often in the thousands or millions.

To mitigate this, alternative truncation strategies have been developed .
- **Tensor-product truncation** includes all polynomials where the maximum degree in any single dimension is at most $p$. The number of terms is $(p+1)^d$, which grows exponentially and is almost always computationally infeasible for $d > 3$.
- **Hyperbolic cross truncation** provides a more efficient alternative by retaining polynomials that are considered more important—namely, those with low total degree and low-order interactions. This strategy often results in a much smaller basis set than total-order truncation for the same level of accuracy, especially when the model output is dominated by the effects of a few variables and their interactions.

For a 10-dimensional problem ($d=10$) with maximum degree $p=3$, the number of basis functions vividly illustrates the differences:
- Total-order: $\binom{10+3}{3} = 286$ terms.
- Tensor-product: $(3+1)^{10} = 1,048,576$ terms.
- Hyperbolic cross (with parameter $q=0.75$): $76$ terms.

This comparison underscores why advanced truncation strategies or sparsity-promoting techniques are essential for applying PCE to complex, [high-dimensional systems](@entry_id:750282) like [battery models](@entry_id:1121428) .

### Computing the PCE Coefficients

With a truncated basis $\{\Psi_j\}_{j=1}^P$ selected, the next step is to compute the unknown coefficients $\{c_j\}_{j=1}^P$. Two main families of methods exist: intrusive and non-intrusive.

#### Intrusive Methods: Stochastic Galerkin

The **Stochastic Galerkin** method is an "intrusive" approach, so-named because it requires modification of the governing equations of the physical model. The method involves substituting the PCE representations for both the uncertain inputs and the [state variables](@entry_id:138790) directly into the model equations (e.g., PDEs or ODEs). Then, a Galerkin projection is performed: the resulting equation is projected onto each [basis function](@entry_id:170178) $\Psi_k$ in the stochastic basis.

This procedure eliminates the stochastic dependency and results in a large, coupled system of deterministic equations for the PCE coefficients of the [state variables](@entry_id:138790). For a time-dependent PDE model of a battery electrode, for instance, this process transforms a single stochastic PDE into a large system of coupled deterministic PDEs for the coefficient fields $c_j(x,t)$ . The coupling between these equations arises from integrals of triple products of the basis functions, e.g., $\mathbb{E}[\Psi_i \Psi_j \Psi_k]$. While powerful and often very accurate, the implementation complexity of reformulating and solving these coupled systems limits the widespread use of intrusive methods.

#### Non-Intrusive Methods: Projection and Regression

Non-intrusive methods treat the original computational model as a "black box" that can be evaluated for given input values, but whose internal equations are not modified. These methods compute the coefficients based on a set of well-chosen model evaluations.

**1. Stochastic Projection (Quadrature):**
This approach directly approximates the integral in the coefficient formula $c_{\boldsymbol{\alpha}} = \mathbb{E}[Y \Psi_{\boldsymbol{\alpha}}]$. Since this expectation is an integral over the high-dimensional input space, it is computed via [numerical quadrature](@entry_id:136578). For independent inputs, a **tensor-product Gaussian quadrature** rule is constructed from one-dimensional rules. The 1D nodes and weights are chosen to be optimal for the specific input distribution (e.g., Gauss-Legendre quadrature for uniform inputs, Gauss-Hermite for Gaussian inputs) . The PCE coefficient is then approximated by a weighted sum of the model output evaluated at the quadrature nodes:

$$
c_{\boldsymbol{\alpha}} \approx \sum_{i=1}^{N_q} Y(\boldsymbol{\xi}^{(i)}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}^{(i)}) w_i
$$

where $(\boldsymbol{\xi}^{(i)}, w_i)$ are the multi-dimensional quadrature nodes and weights. This method is highly efficient and accurate, provided the model function $Y$ is sufficiently smooth.

**2. Least-Squares Regression:**
An alternative non-intrusive approach is to estimate the coefficients via **[least-squares regression](@entry_id:262382)**. This is particularly useful when the model evaluations are not located at specific quadrature points, such as when using existing experimental data or random samples. Given $N$ model evaluations (samples) $\{(\boldsymbol{\xi}^{(i)}, y^{(i)})\}_{i=1}^N$, we seek the coefficients $\mathbf{c}$ that minimize the squared error between the PCE prediction and the observed data. This is formulated as a linear [least-squares problem](@entry_id:164198) :

$$
\min_{\mathbf{c} \in \mathbb{R}^P} \|\mathbf{\Psi}\mathbf{c} - \mathbf{y}\|_2^2
$$

Here, $\mathbf{y} \in \mathbb{R}^N$ is the vector of model outputs, $\mathbf{c} \in \mathbb{R}^P$ is the vector of unknown coefficients, and $\mathbf{\Psi} \in \mathbb{R}^{N \times P}$ is the design matrix, with entries $\Psi_{ij} = \Psi_j(\boldsymbol{\xi}^{(i)})$. For this problem to be well-posed and have a unique solution, the design matrix $\mathbf{\Psi}$ must have full column rank, which generally requires the number of samples $N$ to be at least as large as the number of basis functions $P$ ($N \ge P$), and the sample points must be chosen such that they do not lead to [linear dependence](@entry_id:149638) among the columns of $\mathbf{\Psi}$. When sampling is non-uniform, a **weighted least-squares** formulation can be employed to improve accuracy .

### The Payoff: A Powerful Surrogate Model

Once the coefficients $\{c_{\boldsymbol{\alpha}}\}$ are computed, the truncated PCE serves as an analytical and computationally inexpensive **surrogate model** of the original complex simulation. This surrogate can be evaluated instantly for any new input, but its true power lies in the analytical post-processing it enables.

Key statistical properties of the model output $Y$ can be derived directly and analytically from the PCE coefficients, leveraging the [orthonormality](@entry_id:267887) of the basis. Since the constant basis function is $\Psi_{\boldsymbol{0}}=1$, the expectation (mean) is simply the first coefficient :

$$
\mathbb{E}[Y] = \mathbb{E}\left[\sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right] = \sum_{\boldsymbol{\alpha}} c_{\boldsymbol{\alpha}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = c_{\boldsymbol{0}} \mathbb{E}[\Psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}
$$

The variance, which measures the spread of the output, is the sum of the squares of all other coefficients. This follows from Parseval's identity:

$$
\text{Var}[Y] = \mathbb{E}[(Y - \mathbb{E}[Y])^2] = \mathbb{E}\left[\left(\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right)^2\right] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2
$$

Furthermore, if two different outputs, say discharge capacity $Y_Q$ and heat generation $Y_H$, are expanded on the same basis, their covariance can also be computed directly from their respective coefficient vectors $\mathbf{c}^{(Q)}$ and $\mathbf{c}^{(H)}$:

$$
\text{Cov}[Y_Q, Y_H] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^{(Q)} c_{\boldsymbol{\alpha}}^{(H)}
$$

These simple formulas allow for the instantaneous calculation of statistical moments without any further model simulations. From these, other important quantities like the Pearson correlation coefficient can be computed to understand the relationships between different performance metrics . Beyond moments, the PCE surrogate enables efficient global sensitivity analysis (e.g., computing Sobol' indices), [optimization under uncertainty](@entry_id:637387), and [reliability analysis](@entry_id:192790), making it an indispensable tool in modern automated design and simulation workflows.