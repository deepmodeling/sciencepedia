## Introduction
Standard [least squares](@entry_id:154899) is a cornerstone of scientific computation, but its effectiveness breaks down when faced with real-world data imperfections like outliers or when solutions are required to possess specific structures, such as sparsity. This knowledge gap—the failure of least squares to handle non-Gaussian errors and enforce structural priors—necessitates more advanced techniques. Iteratively Reweighted Least Squares (IRLS) emerges as a powerful and unifying framework to address these exact limitations. It generalizes the [least squares](@entry_id:154899) objective, enabling robust [parameter estimation](@entry_id:139349) and the recovery of structured models by intelligently re-evaluating the importance of data and model parameters throughout the optimization process. This article provides a comprehensive exploration of IRLS. In "Principles and Mechanisms," we will deconstruct the algorithm, tracing its origins from M-estimators and revealing its deep connections to Bayesian inference. Subsequently, "Applications and Interdisciplinary Connections" will showcase its practical power in diverse fields from geophysical tomography to machine learning. Finally, "Hands-On Practices" will solidify your understanding through targeted computational exercises, equipping you with the skills to apply this versatile method to your own work.

## Principles and Mechanisms

The method of least squares, while foundational to computational science and engineering, rests on the assumption that errors in data are well-behaved—typically, that they follow a Gaussian distribution. This assumption, however, is often violated in practice. Geophysical data, for instance, are frequently contaminated by [outliers](@entry_id:172866) arising from instrument malfunctions, environmental noise, or unmodeled physical phenomena. In such cases, the [quadratic penalty](@entry_id:637777) of [least squares](@entry_id:154899), which heavily penalizes large errors, allows these outliers to exert an undue influence on the solution, leading to biased and unreliable model estimates. Furthermore, many inverse problems are ill-posed, and we seek solutions that are not just plausible but also possess certain desirable structures, such as sparsity. Standard least squares provides no mechanism for promoting such structures.

Iteratively Reweighted Least Squares (IRLS) is a powerful and versatile algorithmic framework designed to overcome these limitations. It generalizes the [least squares principle](@entry_id:637217) to a much broader class of [optimization problems](@entry_id:142739), enabling [robust estimation](@entry_id:261282) in the presence of outliers and the promotion of structured solutions like sparse models. At its core, IRLS reframes a complex, non-[quadratic optimization](@entry_id:138210) problem as a sequence of tractable [weighted least squares](@entry_id:177517) (WLS) problems, where the weights are intelligently updated at each iteration. This chapter elucidates the fundamental principles of IRLS, from its theoretical origins in M-estimation to its elegant interpretation as a Bayesian inference algorithm.

### From Weighted Least Squares to Adaptive Weighting

To understand the innovation of IRLS, we first revisit the standard [weighted least squares](@entry_id:177517) (WLS) problem. Given a linear model $Gm \approx d$, where $G \in \mathbb{R}^{n_d \times n_m}$ is a forward operator (or Jacobian matrix), $m \in \mathbb{R}^{n_m}$ is the model to be estimated, and $d \in \mathbb{R}^{n_d}$ is the observed data, the WLS objective function is:

$J(m) = \frac{1}{2} \| W_d(Gm - d) \|_2^2 = \frac{1}{2} (Gm - d)^{\top} W_d^{\top} W_d (Gm - d)$

Here, $W_d$ is a fixed, or static, weighting matrix. In a statistical context, if the data errors are assumed to be zero-mean Gaussian with covariance $C_d$, setting $W_d^{\top}W_d = C_d^{-1}$ yields the maximum likelihood estimate of $m$. The matrix $W_d$ "whitens" the residuals, giving less influence to noisier data points and accounting for correlations.

To find the minimizer, we set the gradient of $J(m)$ with respect to $m$ to zero. Applying the [chain rule](@entry_id:147422) for gradients of [quadratic forms](@entry_id:154578) yields the [stationarity condition](@entry_id:191085):

$\nabla_m J(m) = G^{\top} W_d^{\top} W_d (Gm - d) = 0$

This rearranges into the familiar **normal equations** for the WLS problem [@problem_id:3605207]:

$(G^{\top} W_d^{\top} W_d G) m = G^{\top} W_d^{\top} W_d d$

A unique solution to this system exists if the Hessian matrix, $H = G^{\top} W_d^{\top} W_d G$, is [positive definite](@entry_id:149459). Given that $W_d$ is typically chosen such that $W_d^{\top}W_d$ is positive definite, this condition simplifies to requiring that the matrix $G$ has full column rank (i.e., its columns are linearly independent) [@problem_id:3393244].

The critical limitation of this approach is the static nature of $W_d$. It can effectively handle noise whose statistical properties (like variance) are known beforehand. However, it is powerless against [outliers](@entry_id:172866) whose identity as "outliers" is state-dependent—that is, dependent on the model $m$ itself. For example, in [seismic tomography](@entry_id:754649), a travel-time pick might seem perfectly reasonable for one velocity model but become a significant outlier (e.g., a cycle-skip) for another. A fixed weighting scheme cannot adapt to this change. This necessitates a move from static weights to dynamic, model-dependent weights, which lies at the heart of IRLS [@problem_id:3605207].

### The M-Estimator Framework and the IRLS Algorithm

IRLS is most naturally understood as a method for solving problems in the general class of **M-estimators** (Maximum likelihood-type estimators). Instead of minimizing the [sum of squared residuals](@entry_id:174395), M-estimation seeks to minimize a sum of a less rapidly increasing function of the residuals:

$J(m) = \sum_{i=1}^{n_d} \rho(r_i(m))$

where $r(m) = Gm - d$ and $\rho: \mathbb{R} \to \mathbb{R}_{\ge 0}$ is a convex [penalty function](@entry_id:638029). The standard least squares objective is a special case where $\rho(r) = \frac{1}{2}r^2$. By choosing other penalty functions, we can fundamentally change the properties of the estimator.

The [first-order optimality condition](@entry_id:634945) for minimizing $J(m)$ is found by setting its gradient to zero. Using the [chain rule](@entry_id:147422):

$\nabla_m J(m) = \sum_{i=1}^{n_d} \frac{d\rho}{dr}(r_i(m)) \nabla_m r_i(m) = G^{\top}\Psi(r(m)) = 0$

Here, $\psi(r) = \rho'(r)$ is the derivative of the [penalty function](@entry_id:638029), known as the **[influence function](@entry_id:168646)**. The vector $\Psi(r(m))$ contains the element-wise application of $\psi$ to the residual vector $r(m)$ [@problem_id:3605180]. The [influence function](@entry_id:168646) measures the influence of a single data point on the solution. The optimality condition $G^{\top}\Psi(r(m))=0$ is a system of nonlinear equations in $m$, which is generally difficult to solve directly.

The genius of IRLS is to find a clever way to solve this nonlinear system using a sequence of linear ones. This is achieved by defining a **weight function**, $w(r)$, such that the [influence function](@entry_id:168646) can be written as $\psi(r) = w(r) \cdot r$. The weight function is therefore [@problem_id:3605196]:

$w(r) = \frac{\psi(r)}{r}$

(For $r=0$, the weight is typically defined by the limit $w(0) = \lim_{r\to 0} \psi(r)/r = \psi'(0) = \rho''(0)$).

Substituting this back into the optimality condition gives:

$G^{\top} W(m) r(m) = 0$

where $W(m)$ is a diagonal matrix with entries $w(r_i(m))$. This equation, $G^{\top} W(m) (Gm - d) = 0$, now looks strikingly similar to the WLS normal equations, but with a crucial difference: the weight matrix $W$ depends on the model $m$ itself.

This structure suggests an iterative solution strategy. We start with an initial guess $m^{(0)}$ and, at each iteration $k$, we "freeze" the weights based on the current model's residuals, $r^{(k)} = Gm^{(k)} - d$. We compute the diagonal weight matrix $W^{(k)}$ with entries $w_i^{(k)} = w(r_i^{(k)})$. We then solve the standard WLS problem with these fixed weights to find the next iterate $m^{(k+1)}$ [@problem_id:3605186]:

$m^{(k+1)} = \arg\min_m \sum_{i=1}^{n_d} w_i^{(k)} ( (Gm)_i - d_i )^2$

The solution to this subproblem is given by the linear system:

$(G^{\top} W^{(k)} G) m^{(k+1)} = G^{\top} W^{(k)} d$

This procedure is repeated until the model $m^{(k)}$ converges. This is the Iteratively Reweighted Least Squares algorithm. It transforms a complex nonlinear problem into a sequence of familiar linear (WLS) problems.

### IRLS for Robustness: Taming Outliers

The power of IRLS for [robust estimation](@entry_id:261282) stems directly from the relationship between the [penalty function](@entry_id:638029) $\rho$, the [influence function](@entry_id:168646) $\psi$, and the resulting weights $w$.

For standard least squares, $\rho(r) = \frac{1}{2}r^2$, which gives $\psi(r) = r$. The [influence function](@entry_id:168646) is unbounded; as a residual grows, its influence on the solution grows without limit. The corresponding weight is $w(r) = \psi(r)/r = 1$, confirming that OLS applies a uniform weight to all data points, making it highly sensitive to [outliers](@entry_id:172866) [@problem_id:3605196].

Robust estimators, by contrast, are built from penalty functions that lead to **bounded influence functions**. If $\psi(r)$ is bounded, the influence of any single data point is capped, no matter how large its residual. This automatically leads to weights $w(r) = \psi(r)/r$ that decrease as $|r|$ increases, effectively down-weighting outliers. Let's examine some canonical examples.

#### Huber Loss
The Huber loss provides a [smooth interpolation](@entry_id:142217) between quadratic behavior for small residuals and linear behavior for large ones [@problem_id:3393314]:

$\rho_{\delta}(r) = \begin{cases} \frac{1}{2} r^{2}, & |r| \le \delta \\ \delta |r| - \frac{1}{2} \delta^{2}, & |r| > \delta \end{cases}$

The parameter $\delta$ is a threshold that separates inliers from outliers. The corresponding [influence function](@entry_id:168646) is:

$\psi(r) = \rho'_{\delta}(r) = \begin{cases} r, & |r| \le \delta \\ \delta \cdot \text{sgn}(r), & |r| > \delta \end{cases}$

This function is bounded by $\delta$. The IRLS weights are:

$w(r) = \frac{\psi(r)}{r} = \begin{cases} 1, & |r| \le \delta \\ \frac{\delta}{|r|}, & |r| > \delta \end{cases} = \min\left(1, \frac{\delta}{|r|}\right)$

This beautifully illustrates the mechanism: inliers ($|r| \le \delta$) are treated with standard [least squares](@entry_id:154899) (weight 1), while outliers ($|r| > \delta$) are progressively down-weighted as their magnitude increases. For instance, with $\delta=1$, residuals of $\{0.2, 2, 20\}$ would receive Huber weights of $\{1, 0.5, 0.05\}$, whereas standard least squares would assign weights of $\{1, 1, 1\}$ to all of them [@problem_id:3605196].

#### Heavy-Tailed Distributions: Student's t and Cauchy
In many geophysical applications, noise is better modeled by [heavy-tailed distributions](@entry_id:142737) like the Student's t-distribution, which assigns higher probability to extreme events ([outliers](@entry_id:172866)) than the Gaussian distribution. The [negative log-likelihood](@entry_id:637801) for a Student's [t-distribution](@entry_id:267063) with $\nu$ degrees of freedom and scale $\sigma$ gives rise to the [penalty function](@entry_id:638029) [@problem_id:3605180]:

$\rho(r) = \frac{\nu + 1}{2} \ln\left(1 + \frac{r^2}{\nu \sigma^2}\right)$

The [influence function](@entry_id:168646) and corresponding IRLS weights are:

$\psi(r) = \frac{(\nu + 1) r}{r^2 + \nu \sigma^2} \quad \text{and} \quad w(r) = \frac{\nu + 1}{r^2 + \nu \sigma^2}$

A special case of this for $\nu=1$ is closely related to the **Cauchy penalty**, $\rho(r) = \frac{c^2}{2} \ln(1 + (r/c)^2)$, which yields weights $w(r) = \frac{1}{1+(r/c)^2}$ [@problem_id:3605281]. In both cases, the weight $w(r)$ decreases as $O(1/r^2)$ for large $|r|$, providing very strong down-weighting of outliers.

#### Lp-Norms
The family of Lp-norms, with penalties $\rho(r) \propto |r|^p$, also generates important estimators. For $p=2$, we recover OLS. For $1 \le p  2$, we get robust estimators. The [influence function](@entry_id:168646) is $\psi(r) \propto |r|^{p-1}\text{sgn}(r)$ and the weights are $w(r) \propto |r|^{p-2}$ [@problem_id:3605186]. Since the exponent $p-2$ is negative, the weight decreases as the residual magnitude increases, providing robustness.

### IRLS for Sparsity Promotion

The IRLS framework is not limited to robust [data fitting](@entry_id:149007); it can also be applied to the regularization term of an inverse problem to promote sparsity. A common objective function for finding a sparse model $m$ is:

$F(m) = \frac{1}{2}\|Gm - d\|_2^2 + \lambda \sum_{j=1}^{n_m} \phi(|m_j|)$

where $\phi$ is a sparsity-inducing penalty on the model coefficients. While the L1-norm, $\phi(|m_j|) = |m_j|$, is the most famous convex sparsity promoter, [non-convex penalties](@entry_id:752554) can often achieve better sparsity by more closely approximating the true L0 pseudo-norm (which simply counts non-zero entries).

A powerful example is the logarithmic penalty, $\phi(|m_j|) = \log(|m_j| + \epsilon)$, where $\epsilon > 0$ is a small smoothing parameter. This function is concave and provides a better approximation to the L0 "norm" than the convex L1-norm. Directly minimizing the resulting non-convex objective is hard. However, we can apply an IRLS-like procedure. This approach is an instance of a broader class of algorithms known as **Majorization-Minimization (MM)** [@problem_id:3393260].

In the MM framework, we replace the difficult non-convex penalty $\sum_j \log(|m_j| + \epsilon)$ with a simpler [surrogate function](@entry_id:755683) that is an upper bound (a "majorizer") and is tight at the current iterate $m^{(k)}$. For a [concave function](@entry_id:144403) like log, its first-order Taylor expansion provides such a majorizer. This leads to the surrogate penalty:

$\sum_{j=1}^{n_m} w_j^{(k)} |m_j| \quad \text{where} \quad w_j^{(k)} = \frac{1}{|m_j^{(k)}| + \epsilon}$

The original problem of minimizing the [data misfit](@entry_id:748209) plus a log-penalty is thus replaced by iteratively solving a sequence of **reweighted L1-norm** problems:

$m^{(k+1)} = \arg\min_m \left\{ \frac{1}{2}\|Gm - d\|_2^2 + \lambda \sum_{j=1}^{n_m} w_j^{(k)} |m_j| \right\}$

This reweighted scheme enhances sparsity. If a coefficient $m_j^{(k)}$ is large, its weight $w_j^{(k)}$ becomes small, reducing the penalty and preventing the bias that L1-regularization imposes on large coefficients. Conversely, if $m_j^{(k)}$ is small, its weight becomes large, increasing the shrinkage pressure and encouraging the coefficient to become exactly zero. This adaptive penalization is a highly effective mechanism for recovering [sparse signals](@entry_id:755125).

### A Bayesian Perspective: IRLS as an EM Algorithm

A profoundly insightful perspective on IRLS emerges from Bayesian statistics, where it can often be derived as an Expectation-Maximization (EM) algorithm. This connection reveals that the ad-hoc weighting schemes are, in fact, principled results of probabilistic [hierarchical modeling](@entry_id:272765). The key is the representation of heavy-tailed or sparse-promoting distributions as **Gaussian Scale Mixtures (GSM)**.

A GSM represents a random variable with a non-Gaussian distribution as having a Gaussian distribution conditional on a latent (unobserved) scale (variance or precision) parameter, which itself follows a specific mixing distribution.

#### Robustness from a Gamma-Gaussian Mixture
Consider again the Student's [t-distribution](@entry_id:267063) for residuals. It can be exactly represented as a GSM: a residual $r_i$ follows a Student's [t-distribution](@entry_id:267063) if we model it as being conditionally Gaussian, $r_i | \tau_i \sim \mathcal{N}(0, \sigma^2/\tau_i)$, where the latent precision $\tau_i$ follows a Gamma distribution, $\tau_i \sim \text{Gamma}(\nu/2, \nu/2)$ [@problem_id:3393242].

Within this hierarchical model, finding the maximum likelihood estimate for the model $m$ can be framed as an EM problem, where the $\tau_i$ are [latent variables](@entry_id:143771). The algorithm proceeds in two steps:
1.  **E-Step**: Compute the expectation of the latent precisions given the observed data and the current model estimate $m^{(k)}$. This is the posterior expectation, $\mathbb{E}[\tau_i | r_i^{(k)}]$.
2.  **M-Step**: Maximize the expected complete-data [log-likelihood](@entry_id:273783) with respect to $m$. This maximization step turns out to be precisely a [weighted least squares](@entry_id:177517) problem, where the weights are the expected precisions computed in the E-step.

For the Student-t model, the posterior expectation of the precision is:

$w_i^{(k)} = \mathbb{E}[\tau_i | r_i^{(k)}] = \frac{\nu + 1}{\nu + (r_i^{(k)})^2/\sigma^2}$

This is exactly the same weight we derived earlier from the M-estimator formalism [@problem_id:3393242]. The Bayesian perspective thus provides a deep probabilistic justification for the IRLS algorithm for Student-t regression: the weights are the optimal estimates of the precision for each data point.

#### Sparsity from an Exponential-Gaussian Mixture
A similar connection exists for sparsity. The Laplace distribution, whose negative log-prior corresponds to L1-regularization, can be represented as a GSM. A parameter $m_j$ has a Laplace distribution if we model it as conditionally Gaussian, $m_j | s_j \sim \mathcal{N}(0, s_j)$, where the latent variance $s_j$ follows an Exponential distribution [@problem_id:3393254].

Again, applying the EM algorithm to this hierarchical model to find the MAP estimate for $m$ yields an IRLS algorithm. The M-step is a Tikhonov-[regularized least squares](@entry_id:754212) problem where the regularization weights are the expected latent precisions, $\mathbb{E}[1/s_j | m_j^{(k)}]$. For the Laplace prior with parameter $\lambda$, this expectation is:

$w_j^{(k)} = \mathbb{E}[1/s_j | m_j^{(k)}] = \frac{\lambda}{|m_j^{(k)}|}$

This is precisely the weight used in the reweighted L1 algorithm for approximating L1 or sparser penalties. The EM framework provides a principled derivation for this popular and effective heuristic.

### Convergence and Practical Considerations

The implementation and convergence of IRLS depend on the properties of the objective function and the [forward model](@entry_id:148443).

If the [penalty function](@entry_id:638029) $\rho$ is strictly convex (implying $\rho'' > 0$) and the forward operator $G$ has full column rank, then the overall [objective function](@entry_id:267263) $J(m)$ is strictly convex and has a unique global minimizer. In this setting, the IRLS update direction can be shown to be a descent direction. With a proper [globalization strategy](@entry_id:177837) like a line search, the IRLS algorithm is guaranteed to converge to the unique solution [@problem_id:3605235].

The local convergence rate can be analyzed by viewing IRLS as a [fixed-point iteration](@entry_id:137769), $m^{(k+1)} = T(m^{(k)})$. The [rate of convergence](@entry_id:146534) near a solution $m^\star$ is determined by the [spectral radius](@entry_id:138984) of the Jacobian matrix $T'(m^\star)$. For Lp-norm regression, it can be shown that this Jacobian is $(2-p)I$. The local convergence rate is therefore linear with a factor of $|2-p|$ [@problem_id:3393307]. This indicates that as $p$ approaches 1 (i.e., for nearly L1-regression), the convergence rate slows down significantly.

The situation changes dramatically if $\rho$ is non-convex, as is the case for penalties that generate **redescending influence functions** (e.g., Tukey's biweight, where $\psi(r) \to 0$ as $|r| \to \infty$). Such estimators can completely reject extreme [outliers](@entry_id:172866). However, the non-[convexity](@entry_id:138568) means the objective function $J(m)$ may have multiple local minima. IRLS, being a local optimization method, will converge to a [stationary point](@entry_id:164360) that depends on the initial guess $m^{(0)}$. There are no guarantees of finding the global minimum in this case [@problem_id:3605235].

In summary, Iteratively Reweighted Least Squares is a unifying and powerful algorithmic principle. It provides a bridge from simple least squares to a vast landscape of advanced estimators for robust and structured inversion. By iteratively solving simple [weighted least squares](@entry_id:177517) problems, it can tackle complex non-quadratic objectives, finding its justification in the formalisms of M-estimation, Majorization-Minimization, and hierarchical Bayesian inference.