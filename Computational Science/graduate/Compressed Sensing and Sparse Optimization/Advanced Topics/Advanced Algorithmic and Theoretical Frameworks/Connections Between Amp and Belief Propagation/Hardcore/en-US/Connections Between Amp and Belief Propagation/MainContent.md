## Introduction
In the realm of [high-dimensional statistics](@entry_id:173687) and signal processing, recovering a signal from a limited number of noisy measurements presents a formidable challenge. While Bayesian methods offer a powerful framework for this task, the underlying inference algorithms, like Belief Propagation (BP), are often computationally intractable for the dense, large-scale problems common in modern applications. This intractability represents a significant knowledge gap, hindering the practical application of principled probabilistic inference. This article bridges that gap by providing a comprehensive exploration of Approximate Message Passing (AMP), an algorithm that emerges as a computationally efficient and analytically precise approximation of BP.

Over the next three chapters, you will embark on a journey from first principles to practical application. The first chapter, **Principles and Mechanisms**, will dissect the theoretical derivation of AMP from BP, revealing how Gaussian approximations and a critical correction term—the Onsager reaction term—transform an intractable problem into an efficient algorithm whose performance is perfectly predictable via State Evolution. Following this, the **Applications and Interdisciplinary Connections** chapter will showcase the framework's versatility, demonstrating how AMP can be adapted for advanced [image processing](@entry_id:276975), incorporate complex signal priors, learn parameters from data, and connect to deep concepts in statistical physics. Finally, the **Hands-On Practices** section will solidify your understanding through guided exercises, allowing you to implement and analyze the core concepts of AMP in canonical [sparse recovery](@entry_id:199430) scenarios.

## Principles and Mechanisms

The Approximate Message Passing (AMP) algorithm represents a significant theoretical and practical breakthrough in high-dimensional statistical inference. Its remarkable performance and precise analytical characterization stem from a deep connection to the principles of [message passing](@entry_id:276725) on graphical models, specifically Belief Propagation (BP). This chapter elucidates the principles and mechanisms that bridge the gap between the general but often intractable BP framework and the efficient, specialized AMP algorithm. We will explore how the computational challenges of BP on dense graphs are surmounted through principled approximations, leading to the structure of AMP, its corrective terms, and its remarkably accurate performance analysis via State Evolution.

### Belief Propagation on Dense Factor Graphs

Let us begin with the canonical linear [inverse problem](@entry_id:634767), where we aim to recover an unknown signal $\mathbf{x}_0 \in \mathbb{R}^n$ from a set of linear measurements $\mathbf{y} \in \mathbb{R}^m$ given by:

$$ \mathbf{y} = \mathbf{A}\mathbf{x}_0 + \mathbf{w} $$

Here, $\mathbf{A} \in \mathbb{R}^{m \times n}$ is a known sensing matrix, and $\mathbf{w} \in \mathbb{R}^m$ is a vector of [additive noise](@entry_id:194447). From a Bayesian perspective, we are interested in the posterior probability distribution $p(\mathbf{x} | \mathbf{y})$. Assuming the signal components $x_i$ are drawn independently from a [prior distribution](@entry_id:141376) $p_X$ and the noise components $w_a$ are independent and Gaussian with variance $\sigma_w^2$, the posterior is given by Bayes' rule:

$$ p(\mathbf{x} | \mathbf{y}) \propto p(\mathbf{y} | \mathbf{x}) p(\mathbf{x}) = \left( \prod_{a=1}^m p(y_a | \mathbf{x}) \right) \left( \prod_{i=1}^n p_X(x_i) \right) $$

where the likelihood term for each measurement is $p(y_a | \mathbf{x}) = \mathcal{N}(y_a; (\mathbf{A}\mathbf{x})_a, \sigma_w^2)$. This probabilistic structure can be visualized as a bipartite **factor graph**. The graph consists of $n$ **variable nodes**, representing the signal components $\{x_i\}$, and $m$ **factor nodes**, representing the measurement constraints $\{y_a\}$. An edge connects variable node $x_i$ to factor node $y_a$ if the matrix entry $A_{ai}$ is non-zero. For a [dense matrix](@entry_id:174457) $\mathbf{A}$, this graph is densely connected.

**Belief Propagation (BP)** is an iterative algorithm designed to compute approximate marginal posterior distributions $p(x_i | \mathbf{y})$ by passing messages along the edges of this graph. In its sum-product form, two types of messages are computed:
1.  A message $\mu_{i \to a}(x_i)$ from a variable node $i$ to a factor node $a$.
2.  A message $\nu_{a \to i}(x_i)$ from a factor node $a$ to a variable node $i$.

The update rules involve integrating over all variables except the one being passed. For instance, the factor-to-variable message is:

$$ \nu_{a \to i}(x_i) \propto \int \left( \prod_{j \neq i} d x_j \right) p(y_a | \{\mathbf{x}_k\}) \prod_{j \neq i} \mu_{j \to a}(x_j) $$

While exact on tree-structured graphs, BP on dense, loopy graphs like the one here faces a fundamental obstacle: computational intractability . The calculation of each message $\nu_{a \to i}(x_i)$ requires performing an $(n-1)$-dimensional integral. For a generic, non-Gaussian prior $p_X$, the incoming messages $\mu_{j \to a}(x_j)$ are complex functions, not simple scalars. Evaluating this high-dimensional convolution numerically is computationally infeasible, as its cost grows exponentially with the dimension $n$. This "[curse of dimensionality](@entry_id:143920)" renders exact BP impractical for the high-dimensional problems we wish to solve.

### The Central Limit Theorem and Gaussian Message Approximation

The path to a tractable algorithm begins in the large-system limit, where $m, n \to \infty$ with their ratio $m/n \to \delta \in (0, \infty)$. In this regime, the sums of many weakly [correlated random variables](@entry_id:200386) that appear in the BP updates can be approximated as Gaussian, a consequence of the **Central Limit Theorem (CLT)**. This approximation is the conceptual core of AMP.

Let's re-examine the integral for the message $\nu_{a \to i}(x_i)$. The likelihood $p(y_a | \mathbf{x})$ depends on the term $(\mathbf{A}\mathbf{x})_a = A_{ai}x_i + \sum_{j \neq i} A_{aj}x_j$. The second part, $\sum_{j \neq i} A_{aj}x_j$, is a sum over a large number of variables, where each $x_j$ can be viewed as a random variable drawn from the belief represented by the message $\mu_{j \to a}(x_j)$. If the matrix entries $A_{aj}$ are [independent and identically distributed](@entry_id:169067) with [zero mean](@entry_id:271600) and variance $1/m$, the CLT suggests that this sum will be approximately Gaussian. This dramatically simplifies the [high-dimensional integration](@entry_id:143557) into a convolution with a Gaussian kernel.

A similar simplification occurs when aggregating messages at a variable node. The total belief update for a variable $x_i$ involves a term like $\sum_{a=1}^m A_{ai} r_{a \to i}$, where $r_{a \to i}$ is a "residual" message from factor node $a$. This too is a sum of many weakly correlated terms. Provided certain conditions on the matrix $\mathbf{A}$ hold—such as having i.i.d. sub-Gaussian entries with bounded moments or satisfying the Lindeberg condition—this sum also converges to a Gaussian distribution  .

The consequence of these repeated Gaussian approximations is profound. The complex, functional [message-passing algorithm](@entry_id:262248) of BP simplifies into an algorithm that only needs to track the mean and variance of these effective Gaussian messages. The entire [network inference](@entry_id:262164) problem "decouples" into a set of parallel, scalar estimation problems. At each iteration, the estimation of each signal component $x_i$ becomes equivalent to recovering a signal from an observation through a simple scalar Additive White Gaussian Noise (AWGN) channel of the form:

$$ r_i = x_i + \xi_i, \quad \text{with} \quad \xi_i \sim \mathcal{N}(0, \sigma_t^2) $$

Here, $r_i$ is an effective observation and $\sigma_t^2$ is an effective noise variance that is the same for all components at a given iteration $t$. The estimation of $x_i$ thus reduces to computing a posterior expectation or mode based on its prior $p_X(x_i)$ and this simple Gaussian likelihood, an operation often called **denoising**.

### The Extrinsic Principle and the Onsager Correction

The Gaussian approximation, while powerful, relies on an implicit assumption of [statistical independence](@entry_id:150300) that is violated in dense, loopy graphs. The **extrinsic information principle** is a core tenet of BP: the message sent from a node $U$ to a node $V$ must exclude the information that $U$ just received from $V$ . This prevents immediate [feedback loops](@entry_id:265284) ($U \to V \to U$) and mitigates the "[double counting](@entry_id:260790)" of evidence that plagues loopy BP.

In a [dense graph](@entry_id:634853), the problem is more severe. An estimate of $x_i$ at iteration $t$, let's call it $\hat{x}_i^t$, is formed using information propagated from all measurement nodes. This information is then used to update the messages going back to the measurement nodes. For example, a naive iterative algorithm might compute a residual $\mathbf{r}^t = \mathbf{y} - \mathbf{A}\hat{\mathbf{x}}^t$ and then update the estimate using $\mathbf{A}^T\mathbf{r}^t$. However, because $\hat{\mathbf{x}}^t$ was itself formed using $\mathbf{A}$, the term $\mathbf{A}\hat{\mathbf{x}}^t$ is statistically correlated with $\mathbf{A}$. This creates a self-interaction or "echo" that violates the extrinsic principle at a statistical level, leading to biased estimates and algorithmic divergence.

AMP resolves this issue by introducing a crucial correction term into the residual update, known as the **Onsager reaction term**. This term is designed to precisely cancel the leading-order [statistical bias](@entry_id:275818) arising from self-interaction. The corrected residual update takes the form:

$$ \mathbf{r}^{t} = \mathbf{y} - \mathbf{A}\hat{\mathbf{x}}^{t} + \mathbf{\omega}^{t} $$

where $\mathbf{\omega}^t$ is the Onsager term. This elegant correction can be derived from first principles using the **[cavity method](@entry_id:154304)** from [statistical physics](@entry_id:142945) . By analyzing the system with one measurement ("cavity") temporarily removed and then reintroducing its effect as a small perturbation, one can show that the spurious feedback term is proportional to the previous residual. Its coefficient is precisely related to the average derivative of the denoising function $\eta(\cdot)$ used to compute $\hat{\mathbf{x}}^t$. For a matrix with i.i.d. Gaussian entries, the same result can be derived more formally using Stein's Lemma . The correction term is found to be:

$$ \mathbf{\omega}^t = \frac{1}{\delta} \left( \frac{1}{n}\sum_{j=1}^n \eta'(\cdot) \right) \mathbf{r}^{t-1} $$

This addition restores the statistical properties required for the Gaussian approximation to hold across iterations, ensuring that the effective noise seen by each variable remains approximately white and independent of the signal.

### State Evolution: The Macroscopic View

With the Onsager correction in place, the performance of AMP can be predicted with remarkable accuracy by a simple, scalar, deterministic [recursion](@entry_id:264696) known as **State Evolution (SE)** . SE tracks the evolution of the effective noise variance $\tau_t^2$ of the equivalent scalar channel from one iteration to the next. The [recursion](@entry_id:264696) is given by:

$$ \tau_{t+1}^2 = \sigma_w^2 + \frac{1}{\delta} \mathbb{E}\left[ \left( \eta(X + \tau_t Z; \tau_t^2) - X \right)^2 \right] $$

Let's dissect this fundamental equation:
- $\tau_{t+1}^2$ is the effective noise variance for the next iteration, $t+1$.
- $\sigma_w^2$ is the variance of the physical measurement noise in the original problem.
- $\delta = m/n$ is the measurement rate.
- The expectation $\mathbb{E}[\cdot]$ is taken over the true signal prior $X \sim p_X$ and a standard Gaussian variable $Z \sim \mathcal{N}(0, 1)$.
- The term inside the expectation, $(\eta(X + \tau_t Z; \tau_t^2) - X)^2$, is the squared error of the scalar denoiser $\eta(\cdot)$ when applied to a signal $X$ corrupted by Gaussian noise of variance $\tau_t^2$. The expectation is thus the [mean squared error](@entry_id:276542) (MSE) of the denoiser at iteration $t$.

The SE equation tells a clear story: the noise in the next iteration is composed of two parts: the original [measurement noise](@entry_id:275238) and the [estimation error](@entry_id:263890) from the current iteration, scaled by the [undersampling](@entry_id:272871) factor $1/\delta$.

This SE recursion for AMP is the direct analogue of **Density Evolution (DE)** for BP. Whereas DE tracks the evolution of entire message densities, the Gaussian approximation simplifies this to tracking a single scalar parameter, the variance. The fixed points of the SE recursion characterize the long-term performance of the AMP algorithm and, under Bayes-optimal conditions, correspond to the theoretically minimum possible MSE achievable for the problem, which is also predicted by the [replica method](@entry_id:146718) of [statistical physics](@entry_id:142945) at stationary points of the Bethe free energy .

### A Worked Example: The Bernoulli-Gaussian Prior

To make these principles concrete, let us derive the key components for a signal with a sparsity-inducing **Bernoulli-Gaussian** prior, a common model in compressed sensing :

$$ p_X(x) = (1-\rho)\delta_0(x) + \rho \mathcal{N}(x; 0, \tau_x) $$

Here, $\rho$ is the sparsity rate (the probability of a component being non-zero), $\delta_0(\cdot)$ is the Dirac delta function at zero, and $\tau_x$ is the variance of the non-zero components.

First, we need the Bayes-optimal denoiser $\eta(r; \sigma^2)$ for the scalar channel $R = X + \Xi$, where $\Xi \sim \mathcal{N}(0, \sigma^2)$. The denoiser is the [posterior mean](@entry_id:173826) $\mathbb{E}[X | R=r]$. Using Bayes' rule and the law of total expectation, one can derive this denoiser in [closed form](@entry_id:271343). It balances the possibility of the signal being zero against it being a non-zero Gaussian value. The resulting expression is:

$$ \eta(r; \sigma^2) = \frac{\tau_x r}{\tau_x+\sigma^2} \left( 1 + \frac{1-\rho}{\rho} \sqrt{\frac{\tau_x+\sigma^2}{\sigma^2}} \exp\left(-\frac{r^2 \tau_x}{2\sigma^2(\tau_x+\sigma^2)}\right) \right)^{-1} $$

Next, we insert this specific denoiser $\eta$ into the general State Evolution formula. The SE [recursion](@entry_id:264696) for the Bernoulli-Gaussian AMP is then:

$$ \sigma_{t+1}^2 = \sigma_w^2 + \frac{1}{\delta} \mathbb{E}_{X,Z}\left[ \left(X - \eta\left(X+\sigma_t Z; \sigma_t^2\right)\right)^2 \right] $$

where the expectation is over $X \sim (1-\rho)\delta_0 + \rho\mathcal{N}(0, \tau_x)$ and $Z \sim \mathcal{N}(0,1)$. This equation, though complex-looking, is a deterministic, [one-dimensional map](@entry_id:264951) that fully characterizes the asymptotic performance of the AMP algorithm for this problem.

### Extensions and Generalizations

The powerful connection between BP and AMP extends beyond this canonical setting.
- **Sum-Product vs. Max-Sum:** The sum-product version of BP computes posterior marginals, leading to the MMSE denoiser in AMP. The max-sum version of BP, which seeks the most probable (MAP) configuration, corresponds to an AMP variant where the denoiser is a [proximal operator](@entry_id:169061) associated with the negative log-prior. For certain models, like the Gaussian-Gaussian case, the MMSE and MAP estimators coincide, and so do the corresponding AMP algorithms .
- **Generalized Linear Models (GAMP):** The framework can be extended from the linear model $y=Ax+w$ to Generalized Linear Models (GLMs), where the output $y$ depends on $Ax$ through an arbitrary, separable [likelihood function](@entry_id:141927). The resulting algorithm, GAMP, also has a corresponding State Evolution that precisely tracks its dynamics .
- **Other Matrix Ensembles:** Standard AMP relies on the matrix A having i.i.d. entries. For other matrix classes, such as orthogonally invariant ensembles, different algorithms like Vector AMP (VAMP) are required. These too are derived from BP principles and possess their own predictive State Evolution recursions, demonstrating the versatility of the underlying connection .

In summary, Approximate Message Passing is not an ad-hoc heuristic but a principled, computationally efficient realization of Belief Propagation on dense [random graphs](@entry_id:270323). Its structure is a direct consequence of the Gaussian approximation of messages, and its essential Onsager correction term is a rigorous implementation of the extrinsic information principle. The algorithm's dynamics are perfectly captured by State Evolution, a scalar simplification of Density Evolution, which provides an unprecedentedly precise tool for predicting and understanding the behavior of iterative algorithms in high dimensions.