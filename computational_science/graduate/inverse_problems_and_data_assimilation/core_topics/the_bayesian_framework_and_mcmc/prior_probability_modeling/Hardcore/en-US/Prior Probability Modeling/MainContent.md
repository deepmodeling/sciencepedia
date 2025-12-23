## Introduction
In the realm of [inverse problems](@entry_id:143129) and data assimilation, inferring unknown parameters from indirect and noisy observations is a central challenge. Many of these problems are inherently ill-posed, meaning that a unique, stable solution does not exist based on the data alone. The Bayesian framework provides a powerful and principled approach to overcome this challenge by systematically integrating prior knowledge with observed data. At the heart of this framework lies the [prior probability](@entry_id:275634) distribution, a crucial component that encodes our beliefs about the unknown parameters before any data is considered. The art and science of constructing this prior are what we call "[prior probability](@entry_id:275634) modeling."

However, selecting and formulating an appropriate prior is far from trivial. A naive choice can lead to misleading inferences, while a well-constructed prior can transform an intractable problem into a well-posed one, yielding physically meaningful and robust solutions. This article addresses the fundamental question: How do we construct priors that effectively encode physical constraints, structural assumptions like smoothness or sparsity, and learn from the data itself?

To guide you through this complex landscape, this article is structured into three comprehensive chapters. We will begin in "Principles and Mechanisms" by exploring the theoretical foundations of prior modeling, from the workhorse Gaussian priors in [infinite-dimensional spaces](@entry_id:141268) to non-Gaussian models for handling discontinuities. Next, in "Applications and Interdisciplinary Connections," we will see these principles in action, demonstrating how priors are applied across diverse fields like fluid dynamics, [medical imaging](@entry_id:269649), and genomics to solve real-world problems. Finally, "Hands-On Practices" will offer concrete exercises to bridge theory and practice, allowing you to implement and explore these powerful techniques yourself.

## Principles and Mechanisms

In the Bayesian formulation of inverse problems, the prior probability distribution represents our state of knowledge about the unknown parameter before observing any data. It is a critical component that serves not only to encode this knowledge but also to regularize the ill-posed nature of many [inverse problems](@entry_id:143129) by restricting the space of plausible solutions. This chapter delves into the principles and mechanisms of constructing and applying these priors, ranging from foundational Gaussian models in [infinite-dimensional spaces](@entry_id:141268) to advanced hierarchical and non-Gaussian structures.

### The Foundational Role of the Prior in Bayesian Inversion

The Bayesian framework synthesizes information from three key components: the **prior distribution** $p(u)$, the **likelihood function** $p(y \mid u)$, and the **[posterior distribution](@entry_id:145605)** $p(u \mid y)$. Let us consider a general [inverse problem](@entry_id:634767) where we seek to determine an unknown parameter $u$ from a set of observations $y$. The observation model is typically expressed as:

$y = \mathcal{G}(u) + \eta$

Here, $\mathcal{G}$ is the **forward operator** that maps the parameter space to the data space, and $\eta$ represents measurement noise.

The **[likelihood function](@entry_id:141927)**, denoted $p(y \mid u)$, is the probability density of the observed data $y$ for a given parameter value $u$. It is entirely determined by the statistical properties of the noise $\eta$. For example, if the noise is assumed to be a centered Gaussian random vector with covariance matrix $\Gamma$, $\eta \sim \mathcal{N}(0, \Gamma)$, then the likelihood is given by:

$p(y \mid u) \propto \exp(-\Phi(u;y))$

where $\Phi(u;y) = \frac{1}{2}\|y - \mathcal{G}(u)\|_{\Gamma}^{2} = \frac{1}{2}(y - \mathcal{G}(u))^{\top} \Gamma^{-1} (y - \mathcal{G}(u))$ is the [negative log-likelihood](@entry_id:637801). It is crucial to understand that for a fixed observation $y$, the likelihood, when viewed as a function of $u$, is not a probability distribution for $u$ and its integral over the parameter space need not equal one .

The **[prior distribution](@entry_id:141376)**, denoted $p(u)$ or by a measure $\mu_0$, encapsulates our beliefs about $u$ *before* considering the data $y$. This knowledge may come from physical principles, previous experiments, or assumptions about the expected structure of the solution (e.g., smoothness). The prior is independent of the current observations $y$. Its essential role is to provide regularization by assigning higher probability to "plausible" solutions and lower probability to "implausible" ones, which is critical for stabilizing the inversion of [ill-posed problems](@entry_id:182873) .

The **posterior distribution**, $p(u \mid y)$ or $\mu^y$, represents our updated knowledge about $u$ *after* observing $y$. It is derived by combining the prior and the likelihood via Bayes' theorem. In [finite-dimensional spaces](@entry_id:151571), this theorem is famously written as:

$p(u \mid y) = \frac{p(y \mid u) p(u)}{p(y)}$

where $p(y) = \int p(y \mid u)p(u) \, du$ is the [marginal likelihood](@entry_id:191889), a [normalizing constant](@entry_id:752675).

For inverse problems set in infinite-dimensional function spaces, such as a separable Hilbert space $X$, the concept of a probability density with respect to a Lebesgue measure is ill-defined. Instead, we work with probability measures. The prior is a measure $\mu_0$ on $X$. The posterior $\mu^y$ is then defined in relation to the prior via the Radon-Nikodym derivative. Bayes' theorem takes the form:

$\frac{d\mu^y}{d\mu_0}(u) = \frac{1}{Z(y)} \exp(-\Phi(u;y))$

where $Z(y) = \int_X \exp(-\Phi(u;y)) \, d\mu_0(u)$ is the [normalization constant](@entry_id:190182). This formulation elegantly states that the posterior measure is absolutely continuous with respect to the prior measure, with a density given by the [likelihood function](@entry_id:141927). This implies that any set of parameters assigned zero probability by the prior will also have zero probability under the posterior .

### Gaussian Priors: The Workhorse of Inverse Problems

Gaussian priors are ubiquitous in [data assimilation](@entry_id:153547) and inverse problems due to their analytical tractability and their deep connections to quadratic regularization and [statistical physics](@entry_id:142945). However, their proper definition and interpretation in [infinite-dimensional spaces](@entry_id:141268) require care.

#### Gaussian Measures in Infinite-Dimensional Spaces

A Gaussian measure $\mu_0 = \mathcal{N}(m_0, \mathcal{C}_0)$ on a separable Hilbert space $\mathcal{H}$ is defined by its mean element $m_0 \in \mathcal{H}$ and its covariance operator $\mathcal{C}_0: \mathcal{H} \to \mathcal{H}$. For a well-defined measure to exist, $\mathcal{C}_0$ must be a symmetric, non-negative, and, crucially, **trace-class** operator. This means that if $\{\lambda_n\}_{n\ge 1}$ are the eigenvalues of $\mathcal{C}_0$, we must have $\sum_{n=1}^\infty \lambda_n  \infty$.

A draw $u$ from a centered Gaussian measure $\mathcal{N}(0, \mathcal{C}_0)$ can be represented by the **Karhunen-Loève expansion**:

$u = \sum_{n=1}^\infty \sqrt{\lambda_n} \xi_n e_n$

where $\{e_n\}$ is an [orthonormal basis of eigenvectors](@entry_id:180262) of $\mathcal{C}_0$ and $\{\xi_n\}$ is a sequence of [independent and identically distributed](@entry_id:169067) standard normal random variables, $\xi_n \sim \mathcal{N}(0,1)$. The trace-class condition ensures that the sum converges and the resulting $u$ is an element of $\mathcal{H}$ with probability one.

A central concept associated with a Gaussian measure is the **Cameron-Martin space**, $\mathcal{H}_{\mathcal{C}_0}$. It is a subspace of $\mathcal{H}$ consisting of "admissible" directions of translation. A vector $h \in \mathcal{H}$ is in the Cameron-Martin space if the translated measure (shifted by $h$) is absolutely continuous with respect to the original measure. Mathematically, it is the range of the square-root of the covariance operator, $\mathcal{H}_{\mathcal{C}_0} = \operatorname{Range}(\mathcal{C}_0^{1/2})$, and can be characterized as:

$\mathcal{H}_{\mathcal{C}_0} = \left\{ u = \sum_{n=1}^\infty u_n e_n \in \mathcal{H} : \|u\|_{\mathcal{H}_{\mathcal{C}_0}}^2 = \sum_{n=1}^\infty \frac{u_n^2}{\lambda_n}  \infty \right\}$

Note that the Cameron-Martin norm $\| \cdot \|_{\mathcal{H}_{\mathcal{C}_0}}$ is stronger than the original Hilbert space norm $\| \cdot \|_{\mathcal{H}}$. A key, and perhaps counter-intuitive, result is that the Cameron-Martin space and the **support** of the measure are fundamentally different. The support, $\operatorname{supp}(\mu_0)$, is the smallest closed set in $\mathcal{H}$ with probability one. For a centered Gaussian, it is the closure of the range of the covariance operator, $\operatorname{supp}(\mu_0) = \overline{\operatorname{Range}(\mathcal{C}_0)}$. In an infinite-dimensional setting, a random draw $u$ from $\mu_0$ lies in the Cameron-Martin space $\mathcal{H}_{\mathcal{C}_0}$ with probability zero. This is because the sum $\sum_n \xi_n^2$ required for the Cameron-Martin norm [almost surely](@entry_id:262518) diverges. The measure "lives" on a much larger set than the space of admissible shifts .

#### Maximum A Posteriori (MAP) Estimation and Variational Regularization

A common goal in Bayesian inference is to find a point estimate that summarizes the [posterior distribution](@entry_id:145605). One such estimate is the **Maximum A Posteriori (MAP)** estimate, which corresponds to the mode of the posterior distribution. In finite dimensions, this is found by maximizing the posterior density $p(u|y)$, which is equivalent to minimizing the negative log-posterior.

In infinite dimensions, individual points have zero probability, so a mode is not well-defined in the same way. The MAP estimator is instead defined by analyzing the [posterior probability](@entry_id:153467) of small balls centered at a point $u$. A MAP estimator $u_{\mathrm{MAP}}$ is a point that maximizes the posterior mass in its immediate neighborhood, formalized by the limit of small-ball probabilities :

$\lim_{\epsilon \to 0} \frac{\mu^{y}(B_{\epsilon}(u))}{\mu^{y}(B_{\epsilon}(v))} = \exp\bigl(-I(u)+I(v)\bigr)$

Maximizing this ratio for $u$ is equivalent to minimizing the functional $I(u)$, known as the **Onsager-Machlup functional**. For a Gaussian prior $\mu_0 = \mathcal{N}(0, \mathcal{C}_0)$, this functional takes a beautifully familiar form:

$I(u) = \frac{1}{2}\|y - \mathcal{G}(u)\|_{\Gamma}^{2} + \frac{1}{2}\|u\|_{\mathcal{H}_{\mathcal{C}_0}}^{2}$

This holds for $u$ in the Cameron-Martin space $\mathcal{H}_{\mathcal{C}_0}$, while $I(u) = +\infty$ for $u \notin \mathcal{H}_{\mathcal{C}_0}$. This profound result establishes a rigorous link between Bayesian MAP estimation and classical [variational regularization](@entry_id:756446). The MAP estimate is precisely the function that minimizes a Tikhonov-type functional, which is a weighted sum of the [data misfit](@entry_id:748209) and a regularization penalty. Crucially, the penalty term is not the norm in the [ambient space](@entry_id:184743) $\mathcal{H}$, but the squared norm in the Cameron-Martin space, $\|u\|_{\mathcal{H}_{\mathcal{C}_0}}^{2} = \| \mathcal{C}_0^{-1/2} u \|_{\mathcal{H}}^2$. This restricts the set of potential solutions to the smoother functions that populate the Cameron-Martin space. In the common linear-Gaussian case, the MAP estimator $\hat{u}$ is the solution to a linear system that balances the influence of the data and the prior .

#### Priors from Differential Operators

A powerful and physically motivated method for constructing Gaussian priors is to define their precision operator—the inverse of the covariance operator—in terms of a differential operator. Let $\mathcal{L}$ be a linear partial differential operator (e.g., the gradient, curl, or Laplacian) defined on a domain $\Omega$ with appropriate boundary conditions specified in its domain $\mathcal{D}(\mathcal{L})$. We can construct a centered Gaussian prior $\mu_0$ with precision operator $\mathcal{Q} = \mathcal{L}^*\mathcal{L}$, where $\mathcal{L}^*$ is the adjoint of $\mathcal{L}$ .

The negative log-prior, which serves as the regularization penalty in the MAP estimation framework, is then given by the quadratic form:

$\Phi_{\text{prior}}(u) = \frac{1}{2}\langle u, \mathcal{Q} u \rangle_{\mathcal{H}} = \frac{1}{2}\langle u, \mathcal{L}^*\mathcal{L} u \rangle_{\mathcal{H}} = \frac{1}{2}\|\mathcal{L}u\|_{\mathcal{H}}^2$

for all $u \in \mathcal{D}(\mathcal{L})$. This construction has two profound implications:
1.  **Smoothness Control:** The prior penalizes functions for which $\mathcal{L}u$ is large in norm. If $\mathcal{L}$ involves derivatives, this favors smoother functions. The eigenfunctions of $\mathcal{L}^*\mathcal{L}$ corresponding to large eigenvalues typically represent high-frequency oscillations. By penalizing components along these [eigenfunctions](@entry_id:154705), the prior effectively acts as a low-pass filter.
2.  **Boundary Condition Enforcement:** The penalty is finite only for functions $u$ in the domain of the operator, $\mathcal{D}(\mathcal{L})$. Since this domain encodes the boundary conditions, the MAP estimator is forced to satisfy these same physical constraints. For instance, if $\mathcal{D}(\mathcal{L})$ includes functions that are zero on the boundary (Dirichlet conditions), the resulting MAP estimate will also be zero on the boundary.

This method allows us to inject physical laws and constraints directly into the statistical formulation of the inverse problem.

#### Discretization and Mesh Invariance

When implementing models defined on continuous [function spaces](@entry_id:143478), we must discretize them onto a finite grid or mesh. A critical question is whether the statistical properties of our prior are robust to changes in this [discretization](@entry_id:145012). A prior is considered **regridding-robust** or **mesh-invariant** if its discrete representations are consistent across different mesh resolutions .

Operator-defined priors, constructed as described above, exhibit this desirable property. We start with a single, mesh-independent measure $\mu = \mathcal{N}(0, \mathcal{C})$ on a Hilbert space $H$. A discretization is then obtained by projecting samples from this measure onto a finite-dimensional subspace $V_h$ (e.g., a finite element space). The resulting family of [discrete measures](@entry_id:183686), when viewed back in the parent space $H$, converges weakly to the original measure $\mu$ as the mesh is refined ($h \to 0$). This is a form of **[projective consistency](@entry_id:199671)**: all discrete priors are simply marginals, or different views, of a single underlying mesh-independent measure.

In contrast, a "coordinate-wise" prior, where one defines a prior on the coefficients of a mesh-dependent basis (e.g., assuming independent Gaussian coefficients for each node in a [finite element mesh](@entry_id:174862)), generally lacks this robustness. As the mesh is refined, such a prior does not converge to a well-defined measure on the original function space $H$. Instead, its limit is often a more singular object, like a spatial [white noise process](@entry_id:146877), which lives in a larger space of distributions (a negative-order Sobolev space). For the prior to be meaningful and stable across different discretizations, it should be defined first in the continuous domain and then consistently discretized [@problem_id:3414113, @problem_id:3414093].

#### Gaussian Markov Random Fields (GMRFs)

While operator-defined priors are a "continuous-first" approach, **Gaussian Markov Random Fields (GMRFs)** provide a powerful "discrete-first" framework for defining priors on gridded data. A GMRF is a multivariate Gaussian distribution whose statistical dependencies are specified by a graph. The key insight is that the **[precision matrix](@entry_id:264481)** $Q$ (the inverse of the covariance matrix) encodes [conditional independence](@entry_id:262650) relationships .

Specifically, for any two nodes $i$ and $j$ in the graph, the corresponding variables $x_i$ and $x_j$ are conditionally independent given all other variables if and only if the entry $Q_{ij}$ in the [precision matrix](@entry_id:264481) is zero. This has a profound implication: a sparse [precision matrix](@entry_id:264481) corresponds to a model with only local dependencies. The [conditional distribution](@entry_id:138367) of a variable $x_i$ given all others depends only on its immediate neighbors in the graph.

This property is widely exploited to model spatial smoothness. For a field defined on a grid, we can define a graph where nodes are grid points and edges connect adjacent points. A GMRF prior that encourages smoothness can be constructed by setting its [quadratic form](@entry_id:153497) $x^\top Q x$ to penalize differences between neighboring values:

$x^\top Q x = \kappa^2 \sum_{i} x_i^2 + \sum_{(i,j) \in E} w_{ij} (x_i - x_j)^2$

Here, the first term penalizes the overall magnitude, while the second term, a weighted sum of squared differences across edges $E$, penalizes local roughness. This quadratic form is precisely the discrete analogue of penalties like $\int (\kappa^2 u^2 + |\nabla u|^2) dx$ derived from [differential operators](@entry_id:275037). If $\kappa^2=0$ and the graph is connected, the matrix $Q$ is singular (the constant vector is in its [nullspace](@entry_id:171336)), leading to an improper prior known as an **intrinsic GMRF (IGMRF)**, which is defined only on contrasts between variables.

### Beyond Gaussianity: Advanced Prior Models

While powerful, Gaussian priors are fundamentally unimodal and defined by second-[order statistics](@entry_id:266649) (mean and covariance). Their associated quadratic penalties promote global smoothness, which can be undesirable when the unknown field is expected to contain sharp edges, discontinuities, or other non-smooth features.

#### Enforcing Constraints via Transformations

Many physical parameters are inherently constrained, such as being strictly positive (e.g., diffusion coefficients, concentrations). A flexible way to build priors that respect such constraints is to model an unconstrained latent field with a simple distribution (like a Gaussian) and then transform it into the constrained space .

A common example is enforcing positivity. Instead of modeling the positive field $u(x)$ directly, we model an underlying latent field $v(x)$ as a Gaussian Process, $v \sim \mathcal{GP}(m,k)$, and define the target field as:

$u(x) = \exp(v(x))$

The resulting process for $u(x)$ is a **log-Gaussian Process**. Its properties are derived directly from the transformation.
- **Positivity:** Since the [exponential function](@entry_id:161417) maps any real number to a positive one, the realizations of $u(x)$ are guaranteed to be strictly positive [almost surely](@entry_id:262518).
- **Marginal Distributions:** At any point $x$, $v(x)$ is Gaussian, $v(x) \sim \mathcal{N}(m(x), k(x,x))$. Therefore, $u(x) = \exp(v(x))$ follows a **[log-normal distribution](@entry_id:139089)**. Its mean is $\mathbb{E}[u(x)] = \exp(m(x) + \frac{1}{2}k(x,x))$.
- **Dependence Structure:** The correlation structure of $u$ is inherited from that of $v$. If two points $v(x_1)$ and $v(x_2)$ are independent, then so are $u(x_1)$ and $u(x_2)$.
- **Posterior Complexity:** This transformation results in a non-Gaussian prior on $u$. In a Bayesian analysis, the negative log-prior for a discrete representation $u_{1:n}$ involves terms like $\log(u_i)$, leading to a non-[quadratic penalty](@entry_id:637777) functional and typically requiring numerical methods like MCMC for posterior exploration .

#### Priors for Discontinuities: The Total Variation Prior

For problems where the unknown field is expected to be piecewise-constant or contain sharp discontinuities (e.g., in [medical imaging](@entry_id:269649) or [fault detection](@entry_id:270968)), Gaussian smoothness priors are inappropriate as they excessively penalize the large gradients present at edges, resulting in oversmoothed reconstructions.

The **Total Variation (TV) prior** is a popular alternative designed to preserve such features. It belongs to a class of edge-preserving priors that are often formulated in the Gibbs form, $p(u) \propto \exp(-\lambda R(u))$, where $R(u)$ is a regularization functional. While a Gaussian prior corresponds to a [quadratic penalty](@entry_id:637777) on the gradient, $R(u) = \sum_i \|(Du)_i\|_2^2$, the isotropic TV prior uses an $\ell_1$-type penalty on the gradient magnitudes :

$R_{\text{TV}}(u) = \sum_i \|(Du)_i\|_2$

The crucial difference lies in the growth of the penalty. The [quadratic penalty](@entry_id:637777) of the Gaussian prior grows rapidly with the magnitude of the gradient, severely penalizing any sharp jumps. In contrast, the TV penalty grows only linearly. This relative tolerance for large gradients allows the reconstruction to retain sharp edges. At the same time, the cusp of the $\ell_1$-norm at the origin strongly penalizes small, non-zero gradients, promoting solutions where the gradient is sparse—that is, zero in many locations. A sparse gradient corresponds directly to a piecewise-constant field, which is the desired structure.

### Principled Selection and Learning of Priors

The selection of a prior is a defining feature of Bayesian modeling. This choice can be guided by physical principles, subjective expertise, or formal rules designed for objectivity.

#### The Principle of Maximum Entropy

When our prior knowledge is limited to a set of testable constraints, such as the known mean and variance of a parameter, the **Principle of Maximum Entropy (MaxEnt)** provides an objective method for selecting a [prior distribution](@entry_id:141376) . It states that we should choose the probability distribution that maximizes the Shannon entropy subject to the given constraints. This ensures that the chosen prior is the "least informative" possible, in the sense that it introduces no additional assumptions beyond what is explicitly known.

For a set of constraints of the form $\mathbb{E}[g_i(\mathbf{x})] = c_i$, the MaxEnt prior is found by solving a constrained variational problem. The solution is always a member of the **[exponential family](@entry_id:173146)** of distributions, with a density of the form:

$p(\mathbf{x}) \propto \exp\left(-\sum_{i=1}^{k} \lambda_i g_i(\mathbf{x})\right)$

where the Lagrange multipliers $\lambda_i$ are chosen to satisfy the constraints. This principle yields familiar results:
-   If only the mean and variance are known for a real-valued variable, the MaxEnt prior is a **Gaussian** distribution.
-   If only the mean is known for a positive variable, the MaxEnt prior is an **exponential** distribution.
-   If only the support is known (and is finite), the MaxEnt prior is a **uniform** distribution.

This approach contrasts with subjective prior elicitation, where an expert's qualitative beliefs about smoothness, sparsity, or correlation are translated into a specific prior form, often through [hierarchical modeling](@entry_id:272765). The MaxEnt approach provides a formal and reproducible procedure when knowledge is limited to simple moments .

#### Hierarchical Models and Hyperparameter Estimation

Often, the form of a prior is chosen (e.g., a Gaussian smoothness prior), but its parameters, such as the regularization strength or a [correlation length](@entry_id:143364)-scale, are unknown. These parameters of the prior are called **hyperparameters**. **Hierarchical Bayesian modeling** provides a framework for learning these hyperparameters from the data itself by assigning them their own prior distributions, known as **[hyperpriors](@entry_id:750480)** .

A two-level hierarchy has the structure:
1.  **Likelihood:** $p(y \mid u)$
2.  **Conditional Prior:** $p(u \mid \theta)$ (where $\theta$ are the hyperparameters)
3.  **Hyperprior:** $p(\theta)$

The joint posterior is then $p(u, \theta \mid y) \propto p(y \mid u) p(u \mid \theta) p(\theta)$. There are three common strategies for inference in this setting:

1.  **Full Bayesian Treatment:** This approach embraces all uncertainty by working with the full marginal posterior for $u$, obtained by integrating out the hyperparameters: $p(u \mid y) = \int p(u, \theta \mid y) \, d\theta$. This is the most complete but often most computationally demanding approach. In the common Gaussian-Gamma hierarchical model, for example, integrating out the precision hyperparameter results in a marginal prior for $u$ that is a heavy-tailed Student's [t-distribution](@entry_id:267063), not a Gaussian .

2.  **Empirical Bayes (or Type-II Maximum Likelihood):** This is a pragmatic two-step approach. First, a [point estimate](@entry_id:176325) for $\theta$ is found by maximizing the **marginal likelihood** $p(y \mid \theta) = \int p(y \mid u) p(u \mid \theta) \, du$. Then, this estimate $\hat{\theta}_{\text{EB}}$ is plugged into the conditional posterior, and inference proceeds using $p(u \mid y, \hat{\theta}_{\text{EB}})$. This approach effectively uses the data to select the prior.

3.  **Type-II Maximum A Posteriori (MAP-II):** This is a variation of empirical Bayes. Instead of maximizing the [marginal likelihood](@entry_id:191889) of the hyperparameter, it finds a MAP estimate for $\theta$ by maximizing its posterior, $p(\theta \mid y) \propto p(y \mid \theta) p(\theta)$. This allows the hyperprior $p(\theta)$ to regularize the estimate of $\theta$. The resulting estimate $\hat{\theta}_{\text{MAP}}$ is then plugged into the conditional posterior for $u$. If the hyperprior $p(\theta)$ is uniform, the EB and MAP-II approaches yield the same estimate for $\theta$ .

Hierarchical modeling provides a powerful and principled framework for adapting the [prior distribution](@entry_id:141376) to the information present in the data, moving beyond fixed priors to models that can learn and self-tune.