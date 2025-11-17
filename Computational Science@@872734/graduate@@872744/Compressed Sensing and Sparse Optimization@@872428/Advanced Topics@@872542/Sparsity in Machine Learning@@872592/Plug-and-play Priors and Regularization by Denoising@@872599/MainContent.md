## Introduction
Solving [inverse problems](@entry_id:143129), such as reconstructing a clear image from noisy or incomplete data, is a fundamental challenge across science and engineering. Classical approaches rely on regularization, where a mathematical penalty term representing prior knowledge about the signal (e.g., sparsity) is added to an optimization objective. However, hand-crafting these regularizers is often difficult, and simple models fail to capture the rich structure of real-world data. This article introduces a transformative paradigm: Plug-and-Play (PnP) priors and Regularization by Denoising (RED), which bridge this gap by replacing explicit mathematical priors with powerful, often pre-trained, denoising algorithms.

This article will guide you through the core concepts, applications, and practical considerations of this flexible framework. In "Principles and Mechanisms," we will uncover the theoretical underpinnings of PnP/RED, tracing their origins from Bayesian inference to [operator splitting methods](@entry_id:752962) and exploring the crucial questions of convergence and interpretation. In "Applications and Interdisciplinary Connections," we will survey the broad impact of these methods in fields like [medical imaging](@entry_id:269649), graph analytics, and [scientific computing](@entry_id:143987), demonstrating their versatility. Finally, "Hands-On Practices" will offer concrete exercises to solidify your understanding of key challenges, from ensuring [algorithmic stability](@entry_id:147637) to mitigating artifacts in reconstructions. By the end, you will have a comprehensive understanding of how to leverage state-of-the-art denoisers as sophisticated priors for solving complex [inverse problems](@entry_id:143129).

## Principles and Mechanisms

This chapter delves into the principles and mechanisms that underpin Plug-and-Play (PnP) priors and Regularization by Denoising (RED). We begin by establishing the connection between classical Bayesian inference and regularized optimization. We then explore how this connection motivates the replacement of explicit regularizers with powerful denoising algorithms. This exploration will lead us to the core theoretical questions of [interpretability](@entry_id:637759) and convergence, which we will address using tools from convex analysis and [operator theory](@entry_id:139990). Finally, we will examine the practical implications of these theories for designing stable and effective algorithms, particularly those employing modern [deep neural networks](@entry_id:636170).

### From Bayesian Inference to Regularized Optimization

Many problems in signal and [image processing](@entry_id:276975) fall into the category of [linear inverse problems](@entry_id:751313). The goal is to recover an unknown signal $x \in \mathbb{R}^n$ from a set of measurements $y \in \mathbb{R}^m$, which are related through a linear model corrupted by noise:

$y = Ax + w$

Here, $A \in \mathbb{R}^{m \times n}$ is the sensing matrix, representing the physics of the measurement process, and $w \in \mathbb{R}^m$ is an [additive noise](@entry_id:194447) vector. A common and mathematically tractable assumption is that the noise is additive white Gaussian noise (AWGN), meaning each component of $w$ is an independent and identically distributed sample from a Gaussian distribution with [zero mean](@entry_id:271600) and variance $\sigma_w^2$. We can write this compactly as $w \sim \mathcal{N}(0, \sigma_w^2 I)$.

A powerful framework for solving such problems is Bayesian inference. Instead of seeking a single "correct" $x$, we model our uncertainty and knowledge through probability distributions. We specify a **likelihood function** $p(y|x)$, which describes the probability of observing the measurements $y$ given a signal $x$, and a **prior distribution** $p(x)$, which encodes our a priori beliefs about the properties of the true signal (e.g., that it is sparse or piecewise-smooth).

The goal is to compute the **[posterior distribution](@entry_id:145605)** $p(x|y)$ using Bayes' rule:

$$p(x|y) = \frac{p(y|x)p(x)}{p(y)}$$

The posterior combines the information from the measurements with our prior knowledge. A common way to obtain a [point estimate](@entry_id:176325) for $x$ from the posterior is to find the signal that maximizes its probability density. This is known as the **Maximum A Posteriori (MAP)** estimator:

$$\hat{x}_{\text{MAP}} = \arg \max_{x \in \mathbb{R}^n} p(x|y)$$

Since the denominator $p(y)$ is constant with respect to $x$, this is equivalent to maximizing the numerator $p(y|x)p(x)$. It is often more convenient to work with logarithms, turning the product into a sum and yielding an equivalent minimization problem:

$$\hat{x}_{\text{MAP}} = \arg \min_{x \in \mathbb{R}^n} \{-\log p(y|x) - \log p(x)\}$$

Let's make this more concrete using our assumptions [@problem_id:3466501]. The AWGN model implies that the likelihood function is:

$$p(y|x) = \frac{1}{(2\pi \sigma_w^2)^{m/2}} \exp\left(-\frac{1}{2\sigma_w^2} \|y - Ax\|_2^2\right)$$

The [negative log-likelihood](@entry_id:637801), up to constants independent of $x$, is $\frac{1}{2\sigma_w^2} \|y - Ax\|_2^2$. This term is often called the **data-fidelity** or **data-consistency** term, as it penalizes solutions that do not fit the observed data.

For the prior, a flexible and widely used model is the Gibbs distribution, which takes the form $p(x) \propto \exp(-\lambda \phi(x))$. Here, $\phi(x)$ is a function, often called a potential or energy function, that assigns lower energy (and thus higher probability) to signals with desirable properties. The parameter $\lambda > 0$ controls the strength of the prior. The negative log-prior is then $\lambda \phi(x)$ (plus a constant). This term is known as the **regularization term**.

Combining these, the MAP estimation problem becomes:

$$\hat{x}_{\text{MAP}} = \arg \min_{x \in \mathbb{R}^n} \left\{ \frac{1}{2\sigma_w^2} \|y - Ax\|_2^2 + \lambda \phi(x) \right\}$$

This formulation bridges the probabilistic world of Bayesian inference with the deterministic world of optimization. It reveals that MAP estimation is equivalent to solving a regularized optimization problem. The solution is a trade-off between fidelity to the data and conformity to the prior, with the balance controlled by the noise variance $\sigma_w^2$ and the prior strength $\lambda$. Note that multiplying the entire objective by a positive constant ($2\sigma_w^2$) does not change the minimizer. The equivalent problem is $\arg \min_x (\|y - Ax\|_2^2 + (2\lambda\sigma_w^2) \phi(x))$, which shows that the solution depends on the product $\lambda\sigma_w^2$. Higher noise or a stronger belief in the prior both lead to heavier regularization [@problem_id:3466501].

### Plug-and-Play Priors via Operator Splitting

Solving the MAP optimization problem can be challenging, especially when the regularizer $\phi(x)$ is non-differentiable (e.g., the $\ell_1$-norm promoting sparsity). Operator splitting methods, such as the **Alternating Direction Method of Multipliers (ADMM)**, are exceptionally well-suited for such problems.

Let's rephrase the problem as $\min_x f(x) + g(x)$, where $f(x) = \frac{1}{2}\|y - Ax\|_2^2$ is the data-fidelity term and $g(x)$ is the regularization term (we absorb scaling constants into its definition). ADMM introduces a splitting variable $v$ and an equality constraint:

$$\min_{x,v} f(x) + g(v) \quad \text{subject to} \quad x = v$$

This constraint is enforced by minimizing the augmented Lagrangian, which, in its scaled dual form, is:

$$\mathcal{L}_{\rho}(x,v,u) = f(x) + g(v) + \frac{\rho}{2}\|x - v + u\|_2^2 - \frac{\rho}{2}\|u\|_2^2$$

Here, $\rho > 0$ is a [penalty parameter](@entry_id:753318) and $u$ is the scaled dual variable. ADMM proceeds by iteratively minimizing $\mathcal{L}_{\rho}$ with respect to $x$ and $v$, followed by an update of $u$:

1.  **$x$-update:** $x^{k+1} = \arg\min_x \left( f(x) + \frac{\rho}{2}\|x - v^k + u^k\|_2^2 \right)$
2.  **$v$-update:** $v^{k+1} = \arg\min_v \left( g(v) + \frac{\rho}{2}\|x^{k+1} - v + u^k\|_2^2 \right)$
3.  **$u$-update:** $u^{k+1} = u^k + x^{k+1} - v^{k+1}$

For our specific data-fidelity term $f(x) = \frac{1}{2}\|y - Ax\|_2^2$, the $x$-update subproblem is quadratic and has a [closed-form solution](@entry_id:270799) obtained by setting its gradient to zero. This yields [@problem_id:3466547]:

$$x^{k+1} = (A^\top A + \rho I)^{-1} (A^\top y + \rho(v^k - u^k))$$

The $v$-update can be rewritten as:

$$v^{k+1} = \arg\min_v \left( g(v) + \frac{\rho}{2}\|v - (x^{k+1} + u^k)\|_2^2 \right)$$

This is the definition of the **proximal operator** of the function $g$ with parameter $1/\rho$, evaluated at the point $x^{k+1} + u^k$. We denote this as $v^{k+1} = \operatorname{prox}_{g/\rho}(x^{k+1} + u^k)$. The [proximal operator](@entry_id:169061) can be viewed as a generalized projection that performs denoising; it finds a point $v$ that is close to the "noisy" input $x^{k+1} + u^k$ while also having a small value of the regularizer $g(v)$.

This observation is the gateway to the **Plug-and-Play (PnP)** framework. The core idea is to replace the specific, model-based proximal step with a call to a general-purpose, high-performance [denoising](@entry_id:165626) algorithm $D_\sigma(\cdot)$, where $\sigma$ is a parameter controlling the denoising strength. This leads to the **PnP-ADMM** algorithm [@problem_id:3466547]:

1.  $x^{k+1} = (A^\top A + \rho I)^{-1} (A^\top y + \rho(v^k - u^k))$
2.  $v^{k+1} = D_\sigma(x^{k+1} + u^k)$
3.  $u^{k+1} = u^k + x^{k+1} - v^{k+1}$

This framework is exceptionally powerful because it decouples the data-fidelity term (handled in the $x$-update) from the regularization (handled by the denoiser). One can "plug in" any off-the-shelf denoiser, including state-of-the-art methods based on deep neural networks, without needing to know its explicit mathematical form.

### The MAP Interpretation of PnP: The Role of Proximal Maps

A crucial theoretical question arises: when we run a PnP algorithm, what problem are we actually solving? Does the algorithm still correspond to a MAP estimator for some implicit prior? The answer hinges on whether the denoiser $D_\sigma$ used in the PnP scheme can be identified with the [proximal operator](@entry_id:169061) of some function.

The **proximal map** of a proper, lower semicontinuous (lsc), convex function $\phi: \mathbb{R}^n \to (-\infty, +\infty]$ is formally defined as [@problem_id:3466541]:

$$\operatorname{prox}_{\phi}(z) \triangleq \arg\min_{x \in \mathbb{R}^n} \left\{ \phi(x) + \frac{1}{2}\|x-z\|_2^2 \right\}$$

If the denoiser $D_\sigma$ happens to be exactly the [proximal operator](@entry_id:169061) of some proper, lsc, convex function $\phi$ (i.e., $D_\sigma(\cdot) = \operatorname{prox}_{\phi/\rho}(\cdot)$), then the PnP-ADMM algorithm is mathematically identical to the standard ADMM algorithm applied to the convex MAP objective $\min_x f(x) + \phi(x)$ [@problem_id:3466501]. In this case, the PnP algorithm has a clear interpretation as a MAP estimator.

This raises the next question: what properties must a denoiser possess to be the [proximal operator](@entry_id:169061) of a convex function? The answer comes from fundamental results in convex analysis. A necessary and sufficient condition is that the operator must be **firmly nonexpansive** and satisfy a **cyclic monotonicity** condition [@problem_id:3466541]. For a linear denoiser $D(x) = Kx$, these conditions simplify significantly: the matrix $K$ must be **symmetric** ($K=K^\top$) and its eigenvalues must all lie in the interval $[0, 1]$.

Many practical denoisers, however, do not satisfy these conditions. Consider a simple linear denoiser defined by a one-sided [circular convolution](@entry_id:147898): $y[i] = \frac{2}{3}x[i] + \frac{1}{3}x[i-1]$ [@problem_id:3466510]. This corresponds to a linear operator $D(x)=Kx$. The [circulant matrix](@entry_id:143620) $K$ for this operation is not symmetric. Therefore, this denoiser is *not* the proximal operator of any convex function. Consequently, running PnP-ADMM with this denoiser does not correspond to minimizing a convex MAP objective.

When the denoiser is not a proximal map, the fixed points of the PnP algorithm are best understood as solutions to a **consensus equilibrium**, where the solution simultaneously satisfies the constraints imposed by the data-fidelity term and the implicit regularizing behavior of the denoiser, without necessarily minimizing a single global objective function [@problem_id:3466510].

### Regularization by Denoising (RED): Constructing Explicit Priors

While PnP implicitly regularizes through an algorithmic step, the **Regularization by Denoising (RED)** framework seeks to construct an *explicit* regularization function $R(x)$ from a given denoiser $D(x)$. This allows one to formulate a clear optimization objective and apply any suitable solver, such as [gradient descent](@entry_id:145942).

Two main approaches to defining $R(x)$ exist:

#### Gradient-Based Regularization

This approach postulates that the regularizer $R(x)$ is a function whose gradient is the denoiser residual:

$$\nabla R(x) = x - D(x)$$

For a vector field to be the gradient of a [scalar potential](@entry_id:276177), it must be a **conservative** (or irrotational) field. On a [simply connected domain](@entry_id:197423) like $\mathbb{R}^n$, this is true if and only if its Jacobian matrix is symmetric. The Jacobian of the field $x - D(x)$ is $I - J_D(x)$, where $J_D(x)$ is the Jacobian of the denoiser. The symmetry of $I - J_D(x)$ is equivalent to the symmetry of $J_D(x)$ itself [@problem_id:3466520]. Thus, this approach is valid only for denoisers with a symmetric Jacobian.

A remarkable instance where this condition holds is for **Minimum Mean Squared Error (MMSE)** denoisers. Given a prior $p_X$ and an observation model $Z = X + N$ with Gaussian noise $N \sim \mathcal{N}(0, \sigma^2 I)$, the MMSE denoiser is the conditional mean $D_\sigma(z) = \mathbb{E}[X | Z=z]$. A celebrated result known as **Tweedie's formula** connects this denoiser to the [marginal distribution](@entry_id:264862) of the noisy data, $p_Z(z)$ [@problem_id:3466506]:

$$D_\sigma(z) = z + \sigma^2 \nabla_z \log p_Z(z)$$

Rearranging this gives an explicit expression for the residual:

$$z - D_\sigma(z) = -\sigma^2 \nabla_z \log p_Z(z) = \nabla_z \left( -\sigma^2 \log p_Z(z) \right)$$

This shows that for an MMSE denoiser, the residual field is indeed conservative, and the corresponding regularizer is simply $R_\sigma(z) = -\sigma^2 \log p_Z(z)$ (up to a constant). This provides a deep and elegant link between [statistical estimation](@entry_id:270031) and explicit regularization [@problem_id:3466506].

#### Direct Functional Regularization

An alternative RED approach defines the regularizer directly as a functional:

$$R_{\text{RED}}(x) = \frac{1}{2} x^\top(x - D(x))$$

This form is appealingly simple, but its gradient does not, in general, equal the desired residual $x - D(x)$. By applying the product rule for [vector calculus](@entry_id:146888), one can derive the gradient as [@problem_id:3466523] [@problem_id:3466520]:

$$\nabla R_{\text{RED}}(x) = x - \frac{1}{2} \left( D(x) + J_D(x)^\top x \right)$$

For this gradient to equal $x - D(x)$, it must be that $D(x) = J_D(x)^\top x$. If the denoiser's Jacobian is symmetric, this condition becomes $D(x) = J_D(x)x$, which, by Euler's homogeneous function theorem, implies that the denoiser must be a positive homogeneous function of degree 1 (e.g., $D(cx) = cD(x)$ for $c > 0$). This is a strong requirement not met by many denoisers, including most [proximal operators](@entry_id:635396) [@problem_id:3466520].

### Convergence Guarantees and Operator Theory

Replacing a well-behaved proximal operator with an arbitrary denoiser is a powerful but perilous move; it can easily cause an algorithm to diverge. Ensuring convergence requires analyzing the properties of the denoiser through the lens of [operator theory](@entry_id:139990).

PnP algorithms can be viewed as fixed-point iterations of the form $z^{k+1} = T(z^k)$, where $T$ is an operator representing one full iteration of the algorithm. The convergence of such schemes depends critically on the properties of $T$, which in turn depend on the properties of the denoiser $D$. The key properties are defined by how the operator affects the distance between points [@problem_id:3466548]:

-   **Contractive:** An operator $D$ is a contraction if there exists $q \in [0,1)$ such that $\|D(x) - D(y)\|_2 \le q \|x-y\|_2$ for all $x,y$. If the overall PnP operator $T$ is contractive, the Banach [fixed-point theorem](@entry_id:143811) guarantees [global convergence](@entry_id:635436) to a unique fixed point at a linear rate.

-   **Nonexpansive:** An operator $D$ is nonexpansive if $\|D(x) - D(y)\|_2 \le \|x-y\|_2$ for all $x,y$. This is a weaker condition. If $T$ is nonexpansive, fixed-point theorems (e.g., Krasnosel'skii-Mann) guarantee convergence to a fixed point (if one exists), though the rate is typically sublinear.

-   **Averaged:** An operator $T$ is $\alpha$-averaged if it can be written as $T = (1-\alpha)I + \alpha S$ for some $\alpha \in (0,1)$ and a nonexpansive operator $S$. This is a large and important class of well-behaved nonexpansive operators. Proximal-gradient steps and ADMM iterations are often averaged under suitable assumptions.

-   **Firmly Nonexpansive:** An operator $D$ is firmly nonexpansive if $\|D(x) - D(y)\|_2^2 \le \langle D(x) - D(y), x - y \rangle$. This is a special case of averaged operators ($\alpha=1/2$) and implies [nonexpansiveness](@entry_id:752626). Critically, the proximal map of any proper, lsc, convex function is firmly nonexpansive.

If a denoiser $D$ used in PnP-ADMM is nonexpansive, the resulting ADMM operator is typically averaged, which is sufficient to guarantee convergence to a fixed point [@problem_id:3466531]. This makes [nonexpansiveness](@entry_id:752626) a highly desirable property for PnP denoisers.

Remarkably, this operator property can be connected back to the statistical properties of the prior that an MMSE denoiser implicitly uses. It can be shown that if the [prior distribution](@entry_id:141376) $p_X(x)$ is **log-concave** (i.e., $-\log p_X(x)$ is a [convex function](@entry_id:143191)), then the corresponding MMSE denoiser $D_\sigma$ is **nonexpansive**. Furthermore, if the prior is **strongly log-concave**, the MMSE denoiser is a **contraction** [@problem_id:3466531]. This establishes a profound link: statistically reasonable assumptions about the signal prior translate directly into the mathematically desirable stability properties of the denoiser.

### Practical Implications for Deep Denoisers

Modern PnP and RED methods achieve state-of-the-art results by using powerful denoisers based on deep Convolutional Neural Networks (CNNs). A standard CNN is a composition of layers, and its overall Lipschitz constant is bounded by the product of the Lipschitz constants of its individual layers. A typical layer involves convolution, a normalization step, and a nonlinear activation [@problem_id:3466517].

-   **Convolutional layers** are [linear operators](@entry_id:149003) whose Lipschitz constant is their [spectral norm](@entry_id:143091).
-   **Activation functions** like ReLU and its variants are typically 1-Lipschitz (nonexpansive).
-   **Normalization layers** are problematic. Common techniques like Batch Normalization, Instance Normalization, and Group Normalization are not guaranteed to be nonexpansive and can have very large Lipschitz constants [@problem_id:3466517].

Therefore, a standard off-the-shelf CNN denoiser is generally not nonexpansive, and its use in a PnP framework comes with no formal convergence guarantees. To build provably stable PnP algorithms, one must design the [network architecture](@entry_id:268981) to enforce [nonexpansiveness](@entry_id:752626). This can be achieved by carefully controlling the Lipschitz constant of each layer [@problem_id:3466517]:

1.  **Control Convolutional Layers:** The spectral norm of each convolutional weight matrix must be constrained to be at most 1. This can be done via **[spectral normalization](@entry_id:637347)**, which uses the [power iteration](@entry_id:141327) method to estimate and normalize the largest [singular value](@entry_id:171660) during training. For convolutions with circular padding, the [spectral norm](@entry_id:143091) can be computed exactly and efficiently in the Fourier domain via the FFT [@problem_id:3466517]. Alternatively, one can enforce constraints for the weights to form a **Parseval tight frame** ($W^\top W = I$).

2.  **Use 1-Lipschitz Activations:** This is easily satisfied by most common [activation functions](@entry_id:141784).

3.  **Avoid Problematic Normalization:** Architectures for provably stable PnP should avoid standard [normalization layers](@entry_id:636850) or carefully control their parameters to ensure they do not amplify the Lipschitz constant.

By composing layers that are each guaranteed to be nonexpansive (Lipschitz constant $\le 1$), the entire network becomes nonexpansive, providing a rigorous foundation for the convergence of the PnP algorithm in which it is embedded [@problem_id:3466517]. While many PnP methods perform well empirically even with unconstrained denoisers, this line of research into building provably stable deep priors is crucial for creating reliable and theoretically sound inverse problem solvers.