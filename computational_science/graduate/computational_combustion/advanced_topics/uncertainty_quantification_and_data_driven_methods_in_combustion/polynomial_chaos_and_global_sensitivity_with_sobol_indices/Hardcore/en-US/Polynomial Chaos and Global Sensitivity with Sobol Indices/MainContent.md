## Introduction
Complex computational models, prevalent in fields like computational combustion, are indispensable for modern science and engineering. However, their predictive power is often limited by inherent uncertainties in their input parameters—from physical constants to operational conditions. Understanding how these uncertainties propagate and which inputs contribute most to output variability is a critical task known as Global Sensitivity Analysis (GSA). Traditional methods like Monte Carlo simulation can provide robust answers but often at a prohibitive computational cost, requiring thousands or millions of model evaluations.

This article introduces Polynomial Chaos Expansions (PCE) as a highly efficient and elegant framework to overcome this challenge. PCE provides a method to construct a computationally cheap 'surrogate model' that mimics the original complex system. This surrogate not only accelerates predictions but also holds the key to unlocking a deep understanding of parameter sensitivities. By leveraging the mathematical properties of orthogonal polynomials, we can decompose the output variance and calculate comprehensive sensitivity metrics, such as Sobol indices, with remarkable ease.

Across the following chapters, you will embark on a comprehensive journey into this powerful technique. **Principles and Mechanisms** will lay the theoretical groundwork, explaining how a PCE is constructed and how it directly leads to the calculation of Sobol indices. **Applications and Interdisciplinary Connections** will showcase how PCE-GSA is applied to real-world problems in combustion and beyond, guiding [model refinement](@entry_id:163834) and engineering design. Finally, **Hands-On Practices** will provide practical exercises to solidify your understanding of the method's core computational steps. By the end, you will grasp both the theory and practice of using Polynomial Chaos to quantify uncertainty and sensitivity in complex models.

## Principles and Mechanisms

This chapter delves into the theoretical foundations and practical mechanics of Polynomial Chaos Expansions (PCE) as a powerful tool for [uncertainty quantification](@entry_id:138597) and [global sensitivity analysis](@entry_id:171355) (GSA) in complex models, such as those encountered in computational combustion. We will build the framework from first principles, demonstrating how a random model output can be represented by a spectral expansion, and how this representation directly facilitates the efficient computation of Sobol sensitivity indices.

### The Polynomial Chaos Expansion Framework

At its core, a **Polynomial Chaos Expansion (PCE)** is a [spectral representation](@entry_id:153219) of a second-order random variable, which is a function with [finite variance](@entry_id:269687). Consider a computational model, such as a reacting flow solver, that produces a scalar output of interest, $Y$. This output depends on a vector of $d$ uncertain input parameters, which we represent as a random vector $\boldsymbol{\xi} = (\xi_1, \xi_2, \dots, \xi_d)$ defined on a suitable probability space. The model can be viewed as a function $Y = f(\boldsymbol{\xi})$.

The central idea of PCE is to expand the random output $Y$ in a basis of multivariate polynomials, $\{\Psi_{\boldsymbol{\alpha}}\}_{\boldsymbol{\alpha} \in \mathbb{N}_0^d}$, that are orthonormal with respect to the probability measure of the inputs $\boldsymbol{\xi}$. The expansion takes the form:

$Y(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathbb{N}_0^d} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$

In this expression:
- $\boldsymbol{\alpha} = (\alpha_1, \alpha_2, \dots, \alpha_d)$ is a **multi-index** where each component $\alpha_i$ is a non-negative integer. It specifies the degree of the polynomials for each input variable.
- $\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$ are the multivariate orthonormal basis polynomials.
- $c_{\boldsymbol{\alpha}}$ are the deterministic **PCE coefficients** that uniquely define the expansion.

For this expansion to be computationally useful, it must be truncated to a finite number of terms. This is achieved by restricting the multi-indices $\boldsymbol{\alpha}$ to a [finite set](@entry_id:152247) $\mathcal{A} \subset \mathbb{N}_0^d$:

$Y(\boldsymbol{\xi}) \approx Y_{\text{PCE}}(\boldsymbol{\xi}) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})$

This finite sum serves as a **surrogate model** or **meta-model** for the original, often computationally expensive, model $f(\boldsymbol{\xi})$. The power of this approach, as we will see, lies in the properties of the basis functions and the information encoded in the coefficients.

### The Role of Independence and Orthogonality

The entire PCE and variance-based sensitivity framework is built upon the twin pillars of statistical independence and functional orthogonality.

A set of random variables $\xi_1, \dots, \xi_d$ are formally defined as **independent** if, for any collection of well-behaved sets (Borel sets) $B_1, \dots, B_d \subset \mathbb{R}$, the probability of the joint event is the product of the probabilities of the individual events:

$\mathbb{P}\left(\bigcap_{i=1}^d \{\xi_i \in B_i\}\right) = \prod_{i=1}^d \mathbb{P}\left(\{\xi_i \in B_i\}\right)$

This is equivalent to stating that the [joint probability](@entry_id:266356) measure $\mu_{\boldsymbol{\xi}}$ on $\mathbb{R}^d$ factorizes into the [tensor product](@entry_id:140694) of the marginal measures $\mu_{\xi_i}$ of each input: $\mu_{\boldsymbol{\xi}} = \bigotimes_{i=1}^d \mu_{\xi_i}$ . It is crucial to distinguish independence from [uncorrelatedness](@entry_id:917675). While [independent variables](@entry_id:267118) are always uncorrelated (assuming finite second moments), the converse is not true; zero covariance only captures the absence of [linear dependence](@entry_id:149638), not all forms of [statistical dependence](@entry_id:267552).

The PCE framework operates within the Hilbert space of square-[integrable functions](@entry_id:191199), $L^2$, where the inner product between two functions $g(\boldsymbol{\xi})$ and $h(\boldsymbol{\xi})$ is defined by the expectation of their product:

$\langle g, h \rangle = \mathbb{E}[g(\boldsymbol{\xi})h(\boldsymbol{\xi})] = \int_{\mathbb{R}^d} g(\boldsymbol{x}) h(\boldsymbol{x}) \, d\mu_{\boldsymbol{\xi}}(\boldsymbol{x})$

The basis polynomials $\Psi_{\boldsymbol{\alpha}}$ are chosen to be **orthonormal** with respect to this inner product, meaning $\langle \Psi_{\boldsymbol{\alpha}}, \Psi_{\boldsymbol{\beta}} \rangle = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, where $\delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$ is the Kronecker delta.

The assumption of input independence is what makes the construction of this orthonormal basis tractable. When the joint measure factorizes, the high-dimensional inner product integral also factorizes. This allows us to construct the multivariate basis functions $\Psi_{\boldsymbol{\alpha}}$ as [simple tensor](@entry_id:201624) products of univariate orthonormal polynomials $\psi_{\alpha_i}$:

$\Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi}) = \prod_{i=1}^d \psi_{\alpha_i}(\xi_i)$

Each family of univariate polynomials $\{\psi_k(\xi_i)\}_{k=0}^\infty$ is chosen to be orthonormal with respect to the corresponding marginal measure $\mu_{\xi_i}$. The [orthonormality](@entry_id:267887) of the multivariate basis is then guaranteed by the factorization of the integral . This elegant structure underpins both the construction of PCE and the Analysis of Variance (ANOVA) decomposition used for Sobol indices.

### Constructing the PCE Basis

Constructing a valid and efficient PCE surrogate requires three key steps: selecting an appropriate polynomial basis for each input, transforming inputs if necessary, and truncating the infinite expansion.

#### Matching Polynomials to Distributions: The Askey Scheme

The cornerstone of an effective PCE is selecting a univariate polynomial family that is orthogonal with respect to the probability distribution of its corresponding input variable. This relationship is codified in the **Wiener-Askey scheme** of [orthogonal polynomials](@entry_id:146918). For a given input $\xi_i$ with probability density function (PDF) $p_i(\xi_i)$, the polynomials $\{\psi_k(\xi_i)\}$ must satisfy the [orthogonality condition](@entry_id:168905) $\mathbb{E}[\psi_k \psi_j] = \delta_{kj}$. Two of the most common pairings are  :

-   **Gaussian Inputs:** If an input $\xi_i$ follows a [standard normal distribution](@entry_id:184509), $\xi_i \sim \mathcal{N}(0,1)$, the corresponding orthogonal polynomials are the **probabilists' Hermite polynomials**, $\text{He}_k(\xi_i)$.
-   **Uniform Inputs:** If an input $\xi_i$ follows a uniform distribution on $[-1,1]$, $\xi_i \sim \mathcal{U}(-1,1)$, the corresponding orthogonal polynomials are the **Legendre polynomials**, $P_k(\xi_i)$.

The choice is critical. For instance, in modeling combustion, the uncertainty in an Arrhenius activation energy, $E_a$, might be modeled as a Gaussian random variable due to the central limit theorem acting on many small, uncharacterized error sources. A Hermite polynomial basis would then be the appropriate choice. In contrast, the mixture fraction, $Z$, in a nonpremixed flame is physically bounded between 0 and 1. If its uncertainty is modeled as uniform over this range (after an affine map to $[-1,1]$), a Legendre basis would be required. Using a mismatched basis (e.g., Legendre polynomials for a Gaussian input) breaks the [orthogonality property](@entry_id:268007) and invalidates the simple formulas for variance and sensitivity that we will derive later  .

#### Handling General Input Distributions: The Isoprobabilistic Transform

Physical parameters are rarely distributed as standard normal or uniform variables. A powerful technique to handle inputs with arbitrary distributions is the **isoprobabilistic transform**. This method maps a physical variable $X$ with a known [cumulative distribution function](@entry_id:143135) (CDF), $F_X(x)$, to a standardized variable $\xi$ with a target CDF, $F_\xi(\zeta)$, for which a polynomial basis is known (e.g., standard normal). The transform is defined by equating the CDFs:

$F_X(X) = F_\xi(\xi) \implies \xi = F_\xi^{-1}(F_X(X))$

This ensures that the probability measure is preserved. For example, consider a pre-exponential factor $A$ in an Arrhenius [rate law](@entry_id:141492) that is modeled as a lognormal random variable, such that $\ln(A) \sim \mathcal{N}(m, s^2)$ . To use a Hermite PCE, we need to map $A$ to a standard normal variable $\xi \sim \mathcal{N}(0,1)$. The CDF of $A$ is $F_A(a) = \Phi((\ln(a) - m)/s)$, where $\Phi$ is the standard normal CDF. The transform is:

$\xi = \Phi^{-1}(F_A(A)) = \Phi^{-1}\left(\Phi\left(\frac{\ln(A) - m}{s}\right)\right) = \frac{\ln(A) - m}{s}$

By performing this transformation, we can conduct the entire PCE analysis in the standardized space of $\xi$ and later map results back to the physical space if needed.

#### Truncation and the Curse of Dimensionality

In practice, the infinite PCE series must be truncated to a finite number of terms. The choice of the truncation set $\mathcal{A}$ involves a trade-off between accuracy and computational cost. The two most common strategies are defined by the **input dimension** $d$ and the maximum **polynomial degree** $p$ :

1.  **Full-Tensor (FT) Truncation:** This scheme includes all basis polynomials where the degree in each variable, $\alpha_i$, is at most $p$. The [index set](@entry_id:268489) is $\mathcal{A}_{\text{FT}} = \{ \boldsymbol{\alpha} \in \mathbb{N}_0^d \mid \max_i \alpha_i \le p \}$. The number of terms, $N_{\text{FT}}$, is given by:
    $N_{\text{FT}} = (p+1)^d$

2.  **Total-Degree (TD) Truncation:** This more economical scheme includes all basis polynomials where the sum of the degrees, $|\boldsymbol{\alpha}| = \sum_i \alpha_i$, is at most $p$. The [index set](@entry_id:268489) is $\mathcal{A}_{\text{TD}} = \{ \boldsymbol{\alpha} \in \mathbb{N}_0^d \mid |\boldsymbol{\alpha}| \le p \}$. The number of terms, $N_{\text{TD}}$, is given by the combinatorial formula:
    $N_{\text{TD}} = \binom{p+d}{d} = \frac{(p+d)!}{p! d!}$

The FT scheme grows exponentially with dimension $d$, quickly becoming computationally intractable. This is a manifestation of the **curse of dimensionality**. The TD scheme grows polynomially in $d$ (for fixed $p$), offering a significant reduction in the number of basis terms and making PCE feasible for problems with a moderate number of uncertain inputs.

### Computing PCE Coefficients

Once the basis is defined, the final step in constructing the surrogate is to compute the coefficients $c_{\boldsymbol{\alpha}}$.

#### The Projection Formula

Because the basis functions $\Psi_{\boldsymbol{\alpha}}$ are orthonormal, the coefficients $c_{\boldsymbol{\alpha}}$ are found by simply projecting the model output $Y$ onto each basis function. This is done by taking the inner product:

$c_{\boldsymbol{\alpha}} = \langle Y, \Psi_{\boldsymbol{\alpha}} \rangle = \mathbb{E}[Y(\boldsymbol{\xi}) \Psi_{\boldsymbol{\alpha}}(\boldsymbol{\xi})]$

This formula is the theoretical foundation for all methods of coefficient computation. The practical challenge lies in evaluating this expectation, which is a high-dimensional integral. Two major paradigms exist to tackle this problem .

#### Intrusive vs. Non-Intrusive Methods

1.  **Intrusive Methods (Galerkin Projection):** The intrusive approach reformulates the governing equations of the physical model (e.g., the Navier-Stokes equations in a combustion solver). The state variables (velocity, temperature, species concentrations) are themselves expanded in a PCE. Substituting these expansions into the governing equations and projecting the resulting residual onto each basis polynomial yields a new, large, coupled system of deterministic equations for the PCE coefficients of the state variables. Solving this system requires deep modification of the original solver's source code, particularly its residual and Jacobian calculation routines. This "intrusive" nature makes it powerful but difficult to implement in complex legacy codes.

2.  **Non-Intrusive Methods:** These methods treat the original computational model as a "black box" that simply provides an output $Y$ for a given input $\boldsymbol{\xi}$. No code modification is needed. Instead, the projection integral for $c_{\boldsymbol{\alpha}}$ is approximated numerically by cleverly sampling the model. Common techniques include:
    -   **Numerical Quadrature (Stochastic Collocation):** The integral is approximated by a weighted sum of model evaluations at specific points (quadrature nodes).
    -   **Regression:** The model is evaluated at a set of sample points (the "training data"), and the coefficients are found by solving a [least-squares problem](@entry_id:164198) to fit the PCE surrogate to the data.

Non-intrusive methods are far more popular due to their ease of implementation, as they can be wrapped around any existing simulation code.

### From PCE to Global Sensitivity Indices

One of the most significant applications of PCE is the efficient calculation of global sensitivity indices, which quantify the contribution of each input uncertainty to the output uncertainty.

#### Variance Decomposition via PCE

The [orthonormality](@entry_id:267887) of the PCE basis leads to a remarkably elegant decomposition of the model output's variance. The mean of the output is simply the first coefficient, since $\mathbb{E}[Y] = \mathbb{E}[\sum c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}] = \sum c_{\boldsymbol{\alpha}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}] = c_{\boldsymbol{0}}\mathbb{E}[\Psi_{\boldsymbol{0}}] = c_{\boldsymbol{0}}$.

The total variance, $\mathrm{Var}(Y) = \mathbb{E}[(Y - \mathbb{E}[Y])^2]$, becomes:

$\mathrm{Var}(Y) = \mathbb{E}\left[\left(\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}} \Psi_{\boldsymbol{\alpha}}\right)^2\right] = \sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} \sum_{\boldsymbol{\beta} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}c_{\boldsymbol{\beta}} \mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}]$

Due to [orthonormality](@entry_id:267887), $\mathbb{E}[\Psi_{\boldsymbol{\alpha}}\Psi_{\boldsymbol{\beta}}] = \delta_{\boldsymbol{\alpha}\boldsymbol{\beta}}$, and the expression simplifies beautifully to the sum of the squares of the coefficients (excluding the mean):

$\mathrm{Var}(Y) = \sum_{\boldsymbol{\alpha} \in \mathcal{A}, \boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2$

This fundamental result shows that the total variance is partitioned among the basis functions, with each term $c_{\boldsymbol{\alpha}}^2$ representing the partial variance contributed by the [basis function](@entry_id:170178) $\Psi_{\boldsymbol{\alpha}}$  .

#### First-Order and Total-Effect Sobol Indices

Sobol indices are ratios of these partial variances.

The **first-order Sobol index**, $S_i$, measures the fraction of the total output variance that is due to the main effect of input $\xi_i$ alone, excluding interactions. It is defined as $S_i = \mathrm{Var}(\mathbb{E}[Y|\xi_i]) / \mathrm{Var}(Y)$. Within the PCE framework, the [conditional expectation](@entry_id:159140) $\mathbb{E}[Y|\xi_i]$ isolates all terms that depend only on $\xi_i$. The variance of this quantity corresponds to the sum of squared coefficients for basis functions that depend *only* on $\xi_i$. This leads to the formula  :

$S_i = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_i} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2}$, where $\mathcal{A}_i = \{\boldsymbol{\alpha} \in \mathcal{A} \mid \alpha_i > 0, \text{ and } \alpha_j=0 \text{ for all } j \neq i\}$

The **total-effect Sobol index**, $S_{T_i}$, measures the contribution of input $\xi_i$ including its main effect and all its interactions with other variables. This corresponds to summing the partial variances from all basis functions that involve $\xi_i$ in any way (i.e., where $\alpha_i \ge 1$). The formula is :

$S_{T_i} = \frac{\sum_{\boldsymbol{\alpha} \in \mathcal{A}_{T_i}} c_{\boldsymbol{\alpha}}^2}{\sum_{\boldsymbol{\alpha} \neq \boldsymbol{0}} c_{\boldsymbol{\alpha}}^2}$, where $\mathcal{A}_{T_i} = \{\boldsymbol{\alpha} \in \mathcal{A} \mid \alpha_i \ge 1\}$

Once a PCE is constructed, computing all first-order and total-effect Sobol indices is a matter of simple post-processing—grouping and summing squared coefficients—at virtually no additional computational cost.

#### A Worked Example

Let's illustrate this with a concrete example from a combustion model . Suppose a second-degree PCE for a flame speed $Y$ as a function of three standardized inputs $(X_1, X_2, X_3)$ has been computed, yielding the following non-zero coefficients:

$c_{0}=0, \quad c_{1}=2, \quad c_{2}=1, \quad c_{3}=\frac{1}{2}$
$c_{11}=1, \quad c_{22}=0, \quad c_{33}=\frac{1}{2}$
$c_{12}=\frac{3}{2}, \quad c_{13}=0, \quad c_{23}=1$

(Here, $c_i$ is shorthand for the coefficient of $\psi_1(X_i)$, $c_{ii}$ for $\psi_2(X_i)$, and $c_{ij}$ for $\psi_1(X_i)\psi_1(X_j)$).

1.  **Total Variance:** We sum the squares of all non-constant coefficients:
    $\mathrm{Var}(Y) = 2^2 + 1^2 + (0.5)^2 + 1^2 + 0^2 + (0.5)^2 + (1.5)^2 + 0^2 + 1^2 = 4 + 1 + 0.25 + 1 + 0 + 0.25 + 2.25 + 0 + 1 = 9.75$

2.  **First-Order Indices ($S_i$):** We group coefficients for [main effects](@entry_id:169824).
    -   $V_1 = c_1^2 + c_{11}^2 = 2^2 + 1^2 = 5 \implies S_1 = 5 / 9.75 \approx 0.513$
    -   $V_2 = c_2^2 + c_{22}^2 = 1^2 + 0^2 = 1 \implies S_2 = 1 / 9.75 \approx 0.103$
    -   $V_3 = c_3^2 + c_{33}^2 = (0.5)^2 + (0.5)^2 = 0.5 \implies S_3 = 0.5 / 9.75 \approx 0.051$

3.  **Total-Effect Indices ($S_{T_i}$):** We group all coefficients involving each variable.
    -   $V_{T1} = (c_1^2 + c_{11}^2) + c_{12}^2 + c_{13}^2 = 5 + (1.5)^2 + 0^2 = 7.25 \implies S_{T1} = 7.25 / 9.75 \approx 0.744$
    -   $V_{T2} = (c_2^2 + c_{22}^2) + c_{12}^2 + c_{23}^2 = 1 + (1.5)^2 + 1^2 = 4.25 \implies S_{T2} = 4.25 / 9.75 \approx 0.436$
    -   $V_{T3} = (c_3^2 + c_{33}^2) + c_{13}^2 + c_{23}^2 = 0.5 + 0^2 + 1^2 = 1.5 \implies S_{T3} = 1.5 / 9.75 \approx 0.154$

The interpretation is clear: Input $X_1$ is the most influential factor, accounting for over 51% of the variance through its main effect alone, and over 74% in total. Input $X_2$ has a modest main effect (10%) but a significant total effect (44%), indicating it is highly interactive, primarily with $X_1$. Input $X_3$ is a minor contributor.

### Advanced Considerations

While powerful, the application of PCE requires careful thought regarding its efficiency and underlying assumptions.

#### Computational Cost and Convergence: PCE vs. Monte Carlo

For GSA, the primary alternative to PCE is direct **Monte Carlo (MC) simulation**. The two approaches have fundamentally different convergence characteristics :

-   **Monte Carlo:** The root-[mean-square error](@entry_id:194940) of MC-based Sobol index estimators converges at a rate of $O(N^{-1/2})$, where $N$ is the number of model simulations. This rate is independent of the input dimension and the smoothness of the model. MC is robust and reliable, especially for models with discontinuities or sharp gradients, such as the abrupt transition in [ignition delay time](@entry_id:1126377) that can occur in [stiff chemical systems](@entry_id:755453).

-   **Polynomial Chaos Expansion:** The error in PCE-based indices has two sources: truncation error (from using a finite-degree expansion) and [sampling error](@entry_id:182646) (if coefficients are found by regression). For models that are analytic or sufficiently smooth in their inputs, the truncation error decays *spectrally* (faster than any polynomial rate) as the degree $p$ increases. This makes PCE incredibly sample-efficient for smooth, low-to-moderate dimensional problems, often requiring orders of magnitude fewer simulations than MC for the same accuracy. However, for non-[smooth functions](@entry_id:138942), this rapid convergence is lost, and MC may be more efficient. Regression-based PCE introduces a bias-variance trade-off: a low-degree PCE might have low variance but high bias, while a high-degree PCE has lower bias but requires more samples to control the variance of its many coefficients.

In summary, PCE is generally preferred for computationally expensive, smooth models where the output variance is driven by a relatively small number of inputs and their interactions (low [effective dimension](@entry_id:146824)). MC remains the method of choice for highly non-smooth models, high-dimensional problems, or when implementation simplicity is paramount.

#### The Critical Assumption of Independence

The entire elegant framework of constructing tensor-product bases and calculating Sobol indices by summing squared coefficients rests critically on the assumption that the input variables are **statistically independent** .

In many real-world scenarios, particularly in [combustion chemistry](@entry_id:202796), this assumption is violated. For example, when fitting a [chemical kinetic mechanism](@entry_id:1122345) to experimental data, the Arrhenius parameters—[pre-exponential factor](@entry_id:145277) $A$ and activation energy $E_a$—often become statistically correlated.

When inputs are dependent:
- The [joint probability](@entry_id:266356) measure no longer factorizes.
- The Hoeffding-Sobol decomposition is no longer orthogonal, and the total variance is not a simple sum of partial variances. Standard Sobol indices lose their clear interpretation, and their sum can be greater than 1.
- A tensor-product basis constructed from marginal distributions is no longer orthogonal with respect to the true joint measure. As a result, the PCE coefficients will misattribute the shared variance from correlated inputs, leading to biased and misleading sensitivity indices.

To rigorously handle correlated inputs, one must either:
1.  **Transform the inputs:** Apply a transformation (e.g., a Rosenblatt or Nataf transform) to map the correlated physical variables into a new set of [independent variables](@entry_id:267118). Standard PCE and Sobol analysis can then be performed in this transformed space.
2.  **Use alternative methods:** Employ sensitivity metrics that are explicitly defined for dependent inputs, such as Shapley effects, which provide a fair and additive allocation of variance even in the presence of correlations.

Understanding this limitation is essential for the responsible application of Polynomial Chaos Expansions in global sensitivity analysis.