## Introduction
Solving inverse problems—recovering an unknown signal from indirect and noisy measurements—is a fundamental task across science and engineering. However, these problems are often ill-posed, meaning a unique, stable solution does not exist without additional information. This is where prior knowledge becomes essential, traditionally incorporated through simple mathematical regularizers. The central challenge this article addresses is the limitation of these classical priors in capturing the complex, high-dimensional structures inherent in real-world data. The emergence of [deep learning](@entry_id:142022) offers a transformative solution: using deep neural networks (DNNs) to learn expressive, data-driven priors that encode sophisticated knowledge about the expected solution.

This article provides a comprehensive exploration of deep neural network priors. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, detailing how DNNs are formulated as priors within the Bayesian framework and their impact on regularization. The second chapter, **Applications and Interdisciplinary Connections**, will showcase how these priors are applied to solve challenging problems in fields ranging from [medical imaging](@entry_id:269649) to fluid dynamics, creating powerful synergies between machine learning and the sciences. Finally, the **Hands-On Practices** section offers a set of targeted problems designed to build practical intuition for the core concepts. We will begin our journey by examining the foundational principles and diverse mechanisms that define the modern landscape of deep priors.

## Principles and Mechanisms

Having established the foundational role of prior distributions in rendering [ill-posed inverse problems](@entry_id:274739) tractable, we now delve into the principles and mechanisms that underpin the use of [deep neural networks](@entry_id:636170) (DNNs) to construct these priors. This chapter will move from the formal definition of DNN priors within a Bayesian framework to the specific mechanics of different model classes, and finally to an analysis of their impact on regularization and [uncertainty quantification](@entry_id:138597).

### Foundational Formulations of Deep Priors

In the Bayesian paradigm, the [posterior distribution](@entry_id:145605) over an unknown state $x$ given observations $y$ is given by Bayes' rule:
$$
\pi(x \mid y) \propto p(y \mid x) \mu(x)
$$
where $p(y \mid x)$ is the [likelihood function](@entry_id:141927) derived from the observation model and $\mu(x)$ is the prior distribution embodying our knowledge about $x$ before observing $y$. The central innovation of deep priors is the use of a neural network, trained on a large corpus of representative data, to define $\mu(x)$. This can be achieved through two principal strategies: explicit and implicit modeling.

**Explicit priors** directly define a probability measure or a corresponding energy function for $x$. These models learn a function that can assign a probability (or a related score) to any candidate solution $x$. As detailed in , this category can be further divided:

1.  **Generative Models**: These models define a mapping from a simple [latent space](@entry_id:171820) to the complex space of the signal. A random variable $z$ is drawn from a simple base distribution (e.g., a [standard normal distribution](@entry_id:184509), $z \sim \mathcal{N}(0, I_k)$), and the signal $x$ is produced by a generator network $G_\theta$, such that $x = G_\theta(z)$. The prior on $x$, denoted $p_\theta(x)$, is the [pushforward measure](@entry_id:201640) of the latent distribution through the generator.

2.  **Energy-Based Models (EBMs)**: These models, also known as analysis models, define a scalar-valued energy function $E_\theta(x)$ using a neural network. The [prior probability](@entry_id:275634) density is then given by the Boltzmann distribution, $p_\theta(x) = \frac{1}{Z_\theta} \exp(-E_\theta(x))$, where $Z_\theta$ is an intractable [normalizing constant](@entry_id:752675) (the partition function). Such models learn to assign low energy to plausible signals and high energy to implausible ones.

**Implicit priors**, in contrast, do not provide an explicit formula for the prior density. Instead, they define a procedure or operator, typically a denoiser, that implicitly imposes regularization when embedded within an [iterative optimization](@entry_id:178942) algorithm. This approach, often called "plug-and-play" (PnP), has proven remarkably effective in practice.

A critical distinction in all these formulations is that a true Bayesian prior, $p(x)$, must be defined independently of the specific measurement $y$ for which inference is being performed. Formulations where the "prior" is a direct function of $y$ are not Bayesian in the strict sense but rather describe direct inference or amortized inference methods .

### Explicit Priors I: Generative Models of Synthesis

Generative models that synthesize the signal $x$ from a latent code $z$ via a mapping $x=G_\theta(z)$ are a cornerstone of [modern machine learning](@entry_id:637169). The properties of the resulting prior on $x$ depend critically on the properties of the generator $G_\theta$, particularly its dimensionality and invertibility.

#### The Invertible Case: Normalizing Flows

When the generator $G_\theta: \mathbb{R}^n \to \mathbb{R}^n$ is an invertible and differentiable function (a diffeomorphism) and the [latent space](@entry_id:171820) has the same dimension as the signal space, the model is known as a **Normalizing Flow (NF)**. The chief advantage of this construction is that the prior density $p_\theta(x)$ is analytically tractable. By the **[change of variables](@entry_id:141386) formula**, the density of $x$ can be related to the density of the base variable $z = G_\theta^{-1}(x)$  :

$$
p_\theta(x) = p_Z(G_\theta^{-1}(x)) \left| \det(J_{G_\theta^{-1}}(x)) \right|
$$

where $p_Z$ is the density of the latent variable (e.g., standard normal) and $J_{G_\theta^{-1}}(x)$ is the Jacobian matrix of the inverse mapping $G_\theta^{-1}$ evaluated at $x$. Using the property that the Jacobian of an [inverse function](@entry_id:152416) is the inverse of the forward function's Jacobian, this can be expressed in terms of the forward mapping $G_\theta$ evaluated at $z=G_\theta^{-1}(x)$:

$$
\log p_\theta(x) = \log p_Z(z) - \log |\det(J_{G_\theta}(z))|
$$

For a network composed of multiple invertible layers, $G_\theta = f_k \circ \dots \circ f_1$, the [chain rule](@entry_id:147422) implies that the [log-determinant](@entry_id:751430) of the full Jacobian is the sum of the log-determinants of the Jacobians of each layer, evaluated at the appropriate intermediate activation :
$$
\log |\det(J_{G_\theta}(z))| = \sum_{i=1}^{k} \log|\det(J_{f_i}(z_{i-1}))|
$$
where $z_0=z$ and $z_i = f_i(z_{i-1})$. This decomposition is crucial for designing efficient NF architectures where these [determinants](@entry_id:276593) are cheap to compute (e.g., using triangular or affine [coupling layers](@entry_id:637015)). A concrete application of this formula for a simple invertible network can be seen in .

When using an NF prior for Maximum a Posteriori (MAP) estimation in a linear [inverse problem](@entry_id:634767) with Gaussian noise ($y = Ax + \epsilon$, $\epsilon \sim \mathcal{N}(0, \sigma^2 I)$), the goal is to find the latent variable $z$ that minimizes the negative log-posterior. The resulting objective function is :

$$
\Phi(z) = \underbrace{\frac{1}{2\sigma^2} \|y - A G_\theta(z)\|_2^2}_{\text{Data Misfit}} + \underbrace{\frac{1}{2}\|z\|_2^2}_{\text{Latent Prior}} + \underbrace{\sum_{i=1}^{k} \log|\det(J_{f_i}(z_{i-1}))|}_{\text{Volume Correction}}
$$

While NFs provide a tractable density, this tractability comes at a cost. The generator $G_\theta$ is a highly nonlinear function, making the [data misfit](@entry_id:748209) term non-convex. Furthermore, the [log-determinant](@entry_id:751430) term adds another layer of non-convexity. Consequently, the MAP optimization problem is typically non-convex, possessing multiple local minima and requiring careful optimization strategies .

#### The Non-Invertible Case: Latent Variable Models

A more common architecture for generative models, found in Variational Autoencoders (VAEs) and Generative Adversarial Networks (GANs), involves a non-invertible generator $G_\theta$ that maps from a low-dimensional [latent space](@entry_id:171820) to a high-dimensional signal space ($d_z  d_n$).

The primary consequence of this dimensionality reduction is that the [prior distribution](@entry_id:141376) on $x$ becomes **singular**. The support of the distribution is confined to an underlying manifold of dimension $d_z$ embedded within the [ambient space](@entry_id:184743) $\mathbb{R}^n$. This manifold has zero Lebesgue measure in $\mathbb{R}^n$, which means the prior does not admit a density function in the conventional sense  . This presents a significant challenge for MAP estimation, as the log-prior term $-\log p_\theta(x)$ would be infinite for any $x$ not exactly on the manifold.

A principled and practical solution is to regularize the model by assuming the generator's output is corrupted by a small amount of noise, for example, assuming a decoder model $p_\theta(x|z) = \mathcal{N}(x; G_\theta(z), \sigma_d^2 I)$ for some small variance $\sigma_d^2$. The prior on $x$ is then the marginal $p_\theta(x) = \int p_\theta(x|z) p(z) dz$. While this integral is intractable, we can form a powerful approximation for the negative log-prior regularizer using an argument related to the Laplace approximation . The regularizer becomes an energy function that seeks the optimal latent code $z^*$ that best reconstructs a given $x$:

$$
-\log p_\theta(x) \approx \min_{z} \left( \frac{1}{2\sigma_d^2} \|x - G_\theta(z)\|^2_2 + \frac{1}{2}\|z\|_2^2 \right)
$$

This approach replaces the problematic singular prior with a well-defined penalty that encourages solutions to lie near the manifold of "plausible" signals generated by $G_\theta$.

However, the non-invertibility of $G_\theta$ introduces another profound challenge: **multimodality**. A single signal $x$ may have multiple, distinct latent codes $z$ that can generate it. Even more commonly, the combination of the non-invertible generator and the likelihood can create a posterior distribution with multiple, well-separated modes. A simple but powerful example is a generator $G(z) = |z|$ with a latent prior $z \sim \mathcal{N}(0, \sigma_z^2)$ . For an observation $y0$, the posterior over $z$ becomes bimodal, with two symmetric peaks.

This multimodality has severe practical consequences:
*   **Optimization**: Gradient-based MAP estimation becomes highly dependent on initialization. Starting on one side of a barrier can lead to one mode, while a different initialization leads to another . Standard optimization is not guaranteed to find the global MAP estimate.
*   **Uncertainty Quantification**: Methods that assume a unimodal posterior, such as simple Variational Inference (VI) with a single Gaussian or the Ensemble Kalman Filter (EnKF), will fail. They will either capture only one mode, severely underestimating the true uncertainty, or average across modes in a way that produces a nonsensical result . To address this, one must employ more sophisticated techniques like MCMC samplers designed for multimodality (e.g., Parallel Tempering) or run optimizers from multiple independent starting points.

### Explicit Priors II: Energy-Based Models of Analysis

A different approach to explicit prior modeling is to define an energy function $E_\theta(x)$ directly with a neural network. The prior density is then $p_\theta(x) \propto \exp(-E_\theta(x))$ . These models are trained to assign low energy to structured, realistic signals and high energy to noisy or unrealistic ones.

The posterior for a linear Gaussian [inverse problem](@entry_id:634767) then becomes:
$$
p_\theta(x \mid y) \propto \exp\left(-\frac{1}{2\sigma^2} \|y-Ax\|_2^2 - E_\theta(x)\right)
$$
The MAP estimation problem is to minimize the negative log-posterior, $J(x) = \frac{1}{2\sigma^2} \|y-Ax\|_2^2 + E_\theta(x)$. The energy function $E_\theta(x)$ acts as the regularization term.

The main advantage of EBMs is their flexibility; they do not require a restricted (invertible) architecture or a low-dimensional latent space. However, their primary drawback is the intractable partition function $Z_\theta = \int \exp(-E_\theta(u)) du$, which makes direct evaluation of probabilities and likelihood-based training challenging. Nevertheless, for MAP estimation or MCMC-based sampling, where only the unnormalized posterior is needed, EBMs provide a powerful framework for defining complex regularizers.

### Implicit Priors: Regularization by Denoising

The "plug-and-play" (PnP) framework offers a radically different way to leverage the power of DNNs as priors. Instead of explicitly defining a prior density $p_\theta(x)$, this approach uses a pre-trained image **denoiser** network, $D_\sigma$, within the iterative steps of an [optimization algorithm](@entry_id:142787) like the Alternating Direction Method of Multipliers (ADMM) .

For an objective function of the form $\min_x f(x) + g(x)$, where $f(x)$ is the data-fidelity term (e.g., $\frac{1}{2\sigma^2}\|Ax-y\|_2^2$) and $g(x)$ is the regularization term, ADMM solves the problem by splitting the variable and iterating:
1.  **Data-Fidelity Update ($x$-update)**: A step involving the likelihood, e.g., $x^{k+1} = \text{prox}_{f/\rho}(\cdot)$.
2.  **Prior Update ($v$-update)**: A step involving the prior, $v^{k+1} = \text{prox}_{g/\rho}(\cdot)$.
3.  **Dual Update ($u$-update)**.

The key insight of PnP is to replace the prior's [proximal operator](@entry_id:169061) step, $\text{prox}_{g/\rho}$, with the application of a denoiser $D_\sigma$. The algorithm becomes a sequence of a data-fidelity step, which enforces consistency with the measurements $y$ and forward model $A$, and a [denoising](@entry_id:165626) step, which projects the current estimate onto the manifold of plausible solutions learned by the denoiser .

This seemingly heuristic substitution has a deep theoretical justification. A denoiser $D_\sigma$ trained to minimize the [mean-squared error](@entry_id:175403) for removing Gaussian noise of variance $\sigma^2$ learns to approximate the Minimum Mean-Squared Error (MMSE) estimator, $D_\sigma(z) \approx \mathbb{E}[x \mid z]$, where $z$ is the noisy input. For additive Gaussian noise, **Tweedie's formula** provides a remarkable connection between this MMSE estimator and the **[score function](@entry_id:164520)** (the gradient of the log-density) of the noisy data distribution $p_\sigma(z)$  :

$$
\mathbb{E}[x \mid z] = z + \sigma^2 \nabla_z \log p_\sigma(z)
$$

Rearranging this gives:
$$
\nabla_z \log p_\sigma(z) = \frac{\mathbb{E}[x \mid z] - z}{\sigma^2} \approx \frac{D_\sigma(z) - z}{\sigma^2}
$$

This reveals that the denoiser's residual, $D_\sigma(z)-z$, is an estimator of the scaled [score function](@entry_id:164520). Therefore, the PnP method can be interpreted as an algorithm that implicitly uses the learned score of the [data manifold](@entry_id:636422) to guide the reconstruction, iteratively balancing [data consistency](@entry_id:748190) with prior knowledge.

### The Impact of Deep Priors on Regularization and Uncertainty

The choice of prior fundamentally dictates how an ill-posed [inverse problem](@entry_id:634767) is regularized. For a linear [inverse problem](@entry_id:634767), the MAP objective is $J(x) = \frac{1}{2}\|y-Ax\|_{\Gamma^{-1}}^2 + E_p(x)$, where $E_p(x)=-\log p(x)$. The stability of this optimization problem depends on the curvature of $J(x)$, given by its Hessian matrix:
$$
H_J(x) = \underbrace{A^T \Gamma^{-1} A}_{H_{\text{data}}} + \underbrace{\nabla^2 E_p(x)}_{H_{\text{prior}}(x)}
$$
The data Hessian, $H_{\text{data}}$, is rank-deficient for [ill-posed problems](@entry_id:182873). The prior provides regularization by adding its own curvature, $H_{\text{prior}}$, making the total Hessian better conditioned .

Classical **Tikhonov regularization** corresponds to a Gaussian prior with a quadratic energy function, $E_p(x) \propto \|Lx\|_2^2$. Its Hessian, $H_{\text{prior}} = \alpha L^T L$, is a **constant** matrix. This means it applies the same regularization uniformly across the entire solution space.

In contrast, a **DNN prior**, whether generative or energy-based, defines a complex, non-quadratic energy function $E_\theta(x)$. Its Hessian, $H_{\text{prior}}(x) = \nabla^2 E_\theta(x)$, is **state-dependent**. The prior learns the underlying low-dimensional structure of the data, and its curvature reflects this geometry. The curvature will be large in directions orthogonal to the learned [data manifold](@entry_id:636422), strongly penalizing solutions that deviate from it. Conversely, it will be small in directions tangential to the manifold, allowing for exploration of plausible variations. This results in a powerful, **anisotropic**, and **data-adaptive** form of regularization .

This state-dependent curvature also has profound implications for [uncertainty quantification](@entry_id:138597). Using the Laplace approximation, the [posterior distribution](@entry_id:145605) around a MAP estimate $x^\star$ can be approximated as a Gaussian with covariance $C_{\text{post}} = (H_J(x^\star))^{-1}$. With a DNN prior, the prior's contribution to the Hessian, $H_{\text{prior}}(x^\star)$, depends on the solution $x^\star$ itself. This means the posterior uncertainty is shaped anisotropically, reflecting the learned local geometry of plausible solutions. This is a significant advantage over classical priors, which impose a fixed uncertainty structure regardless of the specific solution found . However, this advanced characterization of uncertainty must always be considered in light of the potential for multimodality, which the simple Laplace approximation cannot capture.

Finally, it is crucial to recognize that all forms of regularization, including those from deep priors, introduce bias in exchange for a reduction in variance—this is the fundamental [bias-variance trade-off](@entry_id:141977). The goal of a sophisticated DNN prior is not to achieve an unbiased estimate, but to introduce a more intelligent bias that pushes the solution towards the manifold of physically realistic signals, rather than merely towards zero or a smoothed version of the signal . The conditions for the mathematical well-posedness of the Bayesian problem, ensuring the posterior is a valid probability measure, rely on properties of the likelihood such as [boundedness](@entry_id:746948) and strict positivity, especially when the prior is a proper probability measure .