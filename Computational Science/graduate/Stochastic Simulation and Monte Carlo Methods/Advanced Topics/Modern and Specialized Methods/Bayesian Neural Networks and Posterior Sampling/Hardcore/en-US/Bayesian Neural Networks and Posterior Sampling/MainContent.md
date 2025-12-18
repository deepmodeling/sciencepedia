## Introduction

While [deep neural networks](@entry_id:636170) have achieved state-of-the-art performance in numerous fields, standard models typically provide only [point estimates](@entry_id:753543), failing to capture the uncertainty inherent in their predictions. Bayesian Neural Networks (BNNs) address this limitation by treating model parameters not as fixed values but as probability distributions. This Bayesian approach provides a principled framework for quantifying uncertainty, which is critical for trustworthy decision-making, especially in high-stakes domains.

The primary challenge and the central focus of this article is the problem of inference. The posterior distribution over the high-dimensional [weight space](@entry_id:195741) of a neural network is analytically intractable, meaning we cannot compute it directly. This knowledge gap necessitates the use of sophisticated approximation techniques to unlock the practical benefits of BNNs.

This article provides a comprehensive guide to the core methods for performing inference in BNNs. In "Principles and Mechanisms," we will dissect the two dominant paradigms: [posterior sampling](@entry_id:753636) via Markov Chain Monte Carlo (MCMC) and [posterior approximation](@entry_id:753628) via Variational Inference (VI). In "Applications and Interdisciplinary Connections," we will explore how these probabilistic models enable advanced applications in active learning, [model assessment](@entry_id:177911), and scientific inquiry. Finally, the "Hands-On Practices" section will provide concrete exercises to solidify your understanding of these powerful techniques. We begin by delving into the foundational principles and mechanisms that make inference in these complex models possible.

## Principles and Mechanisms

Having established the foundational motivation for the Bayesian treatment of neural networks, we now turn to the principles and mechanisms that enable inference in these complex models. The posterior distribution over the high-dimensional [weight space](@entry_id:195741), $p(\theta | \mathcal{D})$, is the central object of our inquiry. However, its form is almost always analytically intractable, defined only up to a [normalization constant](@entry_id:190182). Computing this distribution, or even just expectations under it, requires sophisticated approximation techniques. This chapter dissects the two dominant paradigms for this task—[posterior sampling](@entry_id:753636) via Markov Chain Monte Carlo (MCMC) and [posterior approximation](@entry_id:753628) via Variational Inference (VI)—and explores the crucial role of prior specification and its deep connections to the underlying geometry of the model.

### MCMC Methods for Bayesian Neural Networks

MCMC methods aim to generate samples $\{\theta^{(t)}\}_{t=1}^T$ that, in the limit, are drawn from the true posterior distribution $p(\theta | \mathcal{D})$. From this collection of samples, we can approximate any expectation of interest, such as the predictive distribution. Given the high dimensionality and [complex geometry](@entry_id:159080) of BNN posteriors, gradient-based MCMC methods are indispensable.

#### Stochastic Gradient Langevin Dynamics (SGLD)

The theoretical foundation for many modern BNN samplers is the overdamped Langevin diffusion, a [stochastic differential equation](@entry_id:140379) (SDE) whose [stationary distribution](@entry_id:142542) is our target posterior $\pi(\theta) \equiv p(\theta | \mathcal{D})$. The SDE is given by:

$d\theta_t = \frac{1}{2} \nabla_{\theta} \ln \pi(\theta_t) dt + d\mathcal{W}_t$

where $\mathcal{W}_t$ is a standard $d$-dimensional Wiener process (Brownian motion). This equation describes the motion of a particle in a potential field defined by $U(\theta) = -\ln \pi(\theta)$, subjected to random Gaussian fluctuations. The first term is a drift term that pushes the particle towards regions of high probability (low potential energy), while the second is a diffusion term that ensures the entire space is explored.

A straightforward numerical simulation of this SDE can be achieved through the Euler-Maruyama [discretization](@entry_id:145012), which yields the Langevin Dynamics (LD) update rule:

$\theta_{t+1} = \theta_t + \frac{\eta_t}{2} \nabla_{\theta} \ln \pi(\theta_t) + \sqrt{\eta_t} \xi_t$

Here, $\eta_t$ is the step size (or learning rate) at iteration $t$, and $\xi_t \sim \mathcal{N}(0, I_d)$ is a vector of independent standard Gaussian noise. The gradient of the log-posterior, $\nabla_{\theta} \ln \pi(\theta)$, is often called the **score**.

The primary obstacle to applying LD to large-scale BNNs is the computational cost of the full score. The log-posterior is the sum of the log-prior and the log-likelihood, $\ln \pi(\theta) = \ln p(\theta) + \sum_{i=1}^N \ln p(y_i | x_i, \theta)$. Evaluating the sum over the entire dataset of size $N$ at every iteration is prohibitive.

**Stochastic Gradient Langevin Dynamics (SGLD)** overcomes this by replacing the full gradient with a noisy but unbiased estimator computed on a mini-batch of data. At each iteration $t$, we sample a mini-batch $B_t \subset \{1, \dots, N\}$ of size $m$. The stochastic estimate of the log-posterior gradient is:

$\widehat{\nabla_{\theta} \ln \pi(\theta_t)} = \nabla_{\theta} \ln p(\theta_t) + \frac{N}{m} \sum_{i \in B_t} \nabla_{\theta} \ln p(y_i | x_i, \theta_t)$

Substituting this into the LD update gives the SGLD algorithm. As a concrete example, consider a BNN with weights $w$ under a Gaussian prior $p(w) = \mathcal{N}(0, \sigma_p^2 I)$ and a Gaussian likelihood $p(y_i|x_i, w) = \mathcal{N}(f_w(x_i), \sigma_y^2)$, where $f_w(x)$ is the network output. The gradient of the log-posterior is $\nabla_w \ln p(w|\mathcal{D}) = -\frac{1}{\sigma_p^2}w + \frac{1}{\sigma_y^2} \sum_{i=1}^N (y_i - f_w(x_i))\nabla_w f_w(x_i)$. The SGLD update becomes:

$w_{t+1} = w_t + \frac{\eta_t}{2} \left[ -\frac{1}{\sigma_p^2} w_t + \frac{N}{m\sigma_y^2} \sum_{i \in B_t} (y_i - f_{w_t}(x_i)) \nabla_w f_{w_t}(x_i) \right] + \sqrt{\eta_t}\xi_t$

The genius of SGLD is that the noise from mini-batch subsampling is absorbed into the intentionally injected Langevin noise. For the distribution of samples $w_t$ to converge to the true posterior, the [step-size schedule](@entry_id:636095) must satisfy the standard Robbins-Monro conditions, which ensure that the sampler can explore the space but eventually settles:
1. $\sum_{t=1}^{\infty} \eta_t = \infty$ (ensures the sampler can reach any part of the space)
2. $\sum_{t=1}^{\infty} \eta_t^2  \infty$ (ensures the injected noise variance diminishes, allowing convergence)


#### Improving Sampler Efficiency

While SGLD is a foundational scalable sampler, its random-walk nature can lead to slow exploration of the posterior. More advanced methods improve efficiency by incorporating richer geometric information.

**Hamiltonian Monte Carlo (HMC)** introduces an auxiliary momentum variable $p$ and defines a Hamiltonian $H(\theta, p) = U(\theta) + K(p)$, where $U(\theta) = -\ln \pi(\theta)$ is the potential energy and $K(p) = \frac{1}{2} p^T M^{-1} p$ is the kinetic energy, with $M$ being a mass matrix (often diagonal). Instead of a random walk, HMC proposes new states by simulating Hamiltonian dynamics, which trace out contours of constant energy. This allows for large, efficient moves across the [parameter space](@entry_id:178581). However, standard HMC requires manual tuning of two hyperparameters: the step size $\epsilon$ for the numerical integrator (e.g., leapfrog) and the number of integration steps $L$.

The **No-U-Turn Sampler (NUTS)** is an extension of HMC that automates this tuning. To adaptively set the trajectory length, NUTS builds a [binary tree](@entry_id:263879) of states by running the dynamics forwards and backwards in time. It stops the expansion of the trajectory when it detects a "U-turn," which indicates the path is beginning to curve back on itself. This is detected by monitoring the inner product between the vector connecting the endpoints of the trajectory, $\theta^+ - \theta^-$, and the momentum vectors at these endpoints, $p^-$ and $p^+$. The expansion is halted if either $\langle \theta^+ - \theta^-, p^- \rangle  0$ or $\langle \theta^+ - \theta^-, p^+ \rangle  0$. This robust criterion prevents wasted computation on inefficient trajectories. To tune the step size $\epsilon$, NUTS employs a **dual-averaging** [stochastic optimization](@entry_id:178938) scheme during the warm-up phase, which adjusts $\log(\epsilon)$ to steer the average Metropolis-Hastings [acceptance probability](@entry_id:138494) towards a predefined target, typically around $0.8$. 

Another major challenge is the **[ill-conditioning](@entry_id:138674)** of the posterior, where the curvature of the landscape varies dramatically in different directions. Standard SGLD or HMC with an identity mass matrix will mix very slowly. **Preconditioning** addresses this by applying a linear transformation to the [parameter space](@entry_id:178581) to make the posterior geometry more isotropic (spherical). For SGLD, this corresponds to using a preconditioning matrix $G$ in the drift term. The preconditioned SDE becomes:

$d\theta_t = \frac{1}{2} G \nabla_{\theta} \ln \pi(\theta_t) dt + \boldsymbol{\sigma} d\mathcal{W}_t$

For $\pi(\theta)$ to remain the [stationary distribution](@entry_id:142542), the Fokker-Planck equation dictates that the [diffusion tensor](@entry_id:748421) $D = \frac{1}{2}\boldsymbol{\sigma} \boldsymbol{\sigma}^T$ must equal $\frac{1}{2}G$. This implies $\boldsymbol{\sigma}\boldsymbol{\sigma}^T = G$. A valid choice for the [diffusion matrix](@entry_id:182965) is $\boldsymbol{\sigma} = G^{1/2}$, the [matrix square root](@entry_id:158930) of $G$. The Euler-Maruyama discretization of this process has a noise term given by $\sqrt{\eta_t} G^{1/2} \xi_t$, where $\xi_t \sim \mathcal{N}(0, I_d)$. Using this preconditioned update is equivalent to performing standard SGLD in a transformed space $\phi = G^{-1/2}\theta$ where the geometry is better behaved, and then mapping back to the original space. 

#### Exploiting Posterior Geometry: Symmetries

Deep neural networks often possess geometric non-identifiabilities, or symmetries, where distinct parameter settings yield identical model outputs. For instance, the neurons in a given layer can be permuted without changing the function. A more subtle example arises in networks with **Batch Normalization (BN)**. For a given hidden unit, the BN operation is invariant to the scaling of its incoming weights and bias, $t_i \mapsto c_i t_i$ for any $c_i > 0$, as the scaling factor $c_i$ is cancelled out by the normalization step. If the prior on the log-scale of these weights is uniform, this invariance in the likelihood creates perfectly flat directions or manifolds in the posterior distribution. 

Standard samplers like SGLD or HMC will diffuse along these flat directions in a slow, random-walk fashion, wasting considerable computation. A more effective strategy is to design **symmetry-aware MCMC proposals**. For the BN [scaling symmetry](@entry_id:162020), we can reparameterize the weights $t_i = \exp(s_i) u_i$, where $u_i$ is a unit vector and $s_i$ is the log-scale. The posterior is flat along the $s_i$ dimensions. A custom Metropolis-Hastings move can propose to update only the $s_i$ parameters, for instance $s_i' = s_i + \delta_i$ with $\delta_i$ from a symmetric distribution. Because the posterior density is identical at the current state and the proposed state (provided it remains within prior bounds), and the proposal is symmetric, the acceptance probability for such a move is exactly 1. This allows the sampler to traverse the non-identifiable manifolds in a single step, dramatically improving [sampling efficiency](@entry_id:754496). 

### Variational Inference for Bayesian Neural Networks

Variational Inference (VI) reframes Bayesian inference as an optimization problem. Instead of sampling from the posterior $p(\theta | \mathcal{D})$, we posit a family of tractable distributions $q_\phi(\theta)$ parameterized by $\phi$, and then find the member of this family that is "closest" to the true posterior.

#### The Variational Principle and The KL Divergence

Closeness is typically measured by the **Kullback-Leibler (KL) divergence**. The standard VI objective is to minimize the forward KL divergence, $\mathrm{KL}(q_\phi(\theta) \| p(\theta | \mathcal{D}))$. This is equivalent to maximizing the **Evidence Lower Bound (ELBO)**, $\mathcal{L}(\phi) = \mathbb{E}_{q_\phi}[\ln p(\mathcal{D}|\theta)] - \mathrm{KL}(q_\phi(\theta) \| p(\theta))$.

The choice of divergence has profound consequences for the behavior of the approximation. The forward KL divergence is defined as:

$\mathrm{KL}(q \| p) = \int q(\theta) \log \frac{q(\theta)}{p(\theta | \mathcal{D})} d\theta$

This integral is large if $q(\theta)$ assigns probability mass where $p(\theta | \mathcal{D})$ is small. To minimize it, $q(\theta)$ is forced to be zero wherever the true posterior is zero. This "zero-forcing" property leads to **[mode-seeking](@entry_id:634010)** behavior. If the true posterior is multimodal (as is common in BNNs due to symmetries) and the variational family $q_\phi$ is unimodal (e.g., a mean-field Gaussian), the optimal $q_\phi$ will collapse to cover only one of the modes, ignoring the others. This results in an approximation that severely underestimates the true posterior uncertainty. 

In contrast, the reverse KL divergence is:

$\mathrm{KL}(p \| q) = \int p(\theta | \mathcal{D}) \log \frac{p(\theta | \mathcal{D})}{q(\theta)} d\theta$

This integral is large if $q(\theta)$ is small in a region where $p(\theta | \mathcal{D})$ has mass. Minimizing it forces $q(\theta)$ to be non-zero wherever the true posterior is non-zero. This "zero-avoiding" property encourages **mass-covering** behavior. For a [multimodal posterior](@entry_id:752296) and a unimodal $q_\phi$, the approximation will spread itself out to cover all modes, often resulting in an overdispersed distribution that places significant probability in the low-density regions between modes.  While standard VI minimizes the forward KL, other algorithms are based on minimizing the reverse KL or other divergences.

#### Expressive Variational Families

The quality of a VI approximation is fundamentally limited by the [expressivity](@entry_id:271569) of the chosen variational family $q_\phi$. The simplest choice, a **mean-field** (fully factorized) Gaussian, assumes independence among all parameters and cannot capture any posterior correlations. This is a strong and often unrealistic assumption.

To build more flexible approximations, we can use **Normalizing Flows**. A [normalizing flow](@entry_id:143359) transforms a simple base distribution (e.g., a standard Gaussian) through a series of invertible, differentiable mappings to produce a complex, multi-modal target distribution. Let the base variable be $z \sim p_z(z)$ and the invertible map be $f_\phi$. The transformed variable is $w = f_\phi(z)$. The density of the resulting variational distribution $q_\phi(w)$ is given by the [change of variables](@entry_id:141386) formula:

$q_\phi(w) = p_z(f_\phi^{-1}(w)) \left| \det J_{f_\phi^{-1}}(w) \right|$

where $J_{f_\phi^{-1}}$ is the Jacobian of the inverse map. The log-density is then $\log q_\phi(w) = \log p_z(f_\phi^{-1}(w)) + \log |\det J_{f_\phi^{-1}}(w)|$.

A popular and effective flow architecture is the **affine coupling layer**. It partitions its input $x$ into two parts, $(x_A, x_B)$. One part is left unchanged, while the other is transformed by an affine transformation whose parameters are a function of the unchanged part: $y_A = x_A$, and $y_B = x_B \odot \exp(s(x_A)) + t(x_A)$. The functions $s(\cdot)$ and $t(\cdot)$ can themselves be neural networks. This construction has a triangular Jacobian, making its determinant (and [log-determinant](@entry_id:751430)) trivial to compute: it is simply the sum of the elements of $s(x_A)$. By composing many such layers, alternating which part is transformed, we can build highly expressive distributions that can model complex dependencies and correlations, far exceeding the capabilities of a mean-field Gaussian. 

### The Critical Role of the Prior

The [prior distribution](@entry_id:141376), $p(\theta)$, is not merely a regularization term but a powerful tool for injecting domain knowledge and controlling model behavior. Moving beyond simple isotropic Gaussian priors is often crucial for building effective BNNs.

#### Hierarchical Priors for Sparsity and Structure

**Hierarchical priors** are a key mechanism for creating adaptive and structured models. In this scheme, a parameter's prior is itself conditioned on a hyperparameter, which is given its own hyperprior.

A classic example is **Automatic Relevance Determination (ARD)**. For a weight vector $w$, instead of a single prior variance, each component $w_j$ is given its own precision $\alpha_j$: $p(w_j|\alpha_j) = \mathcal{N}(0, \alpha_j^{-1})$. Each precision $\alpha_j$ is then given a broad hyperprior, typically a Gamma distribution, $p(\alpha_j) = \mathrm{Gamma}(a, b)$. This structure allows the model to learn the importance of each feature. If a feature is irrelevant, the posterior for its corresponding precision $\alpha_j$ will be concentrated at large values, effectively shrinking the weight $w_j$ to zero and pruning the feature from the model. In a conjugate setting (e.g., [linear regression](@entry_id:142318)), the full conditional posteriors for $w$ and $\alpha$ are [standard distributions](@entry_id:190144) (Gaussian and Gamma, respectively), enabling efficient Gibbs sampling. 

An even more powerful sparsity-inducing prior is the **Horseshoe prior**. For a scalar weight $w$, this prior is specified hierarchically as $w \mid \tau \sim \mathcal{N}(0, \tau^2)$, with a scale parameter $\tau$ that follows a half-Cauchy distribution, $\tau \sim \mathrm{HalfCauchy}(\beta)$. The marginal prior $p(w)$ that results from integrating out $\tau$ has remarkable properties. As $|w| \to 0$, the density diverges logarithmically, $p(w) \sim c_1 \log(1/|w|^2)$, creating an infinitely tall spike at zero that provides immense shrinkage for small, noisy coefficients. Simultaneously, as $|w| \to \infty$, the density decays polynomially like a Cauchy distribution, $p(w) \sim c_2/|w|^2$. These heavy tails allow large, true signals to pass through without being over-shrunk. This combination of strong shrinkage and robustness to large signals makes the Horseshoe an excellent prior for sparse high-dimensional problems. A more complex variant, the regularized Horseshoe, uses a double hierarchy $w_j \sim \mathcal{N}(0, \lambda_j^2 \tau^2)$ with $\lambda_j, \tau \sim \mathrm{HalfCauchy}(1)$, which results in even heavier tails of the form $p(w_j) \sim c_3 \ln|w_j|/|w_j|^2$.  

Priors can also encode structural knowledge. For a convolutional filter, an i.i.d. Gaussian prior on its weights is unrealistic, as it assumes adjacent weights are uncorrelated. A better approach is to model the filter as a function over a discrete spatial grid and place a **Gaussian Process (GP)** prior on this function. This is equivalent to a multivariate Gaussian prior on the vectorized filter weights, $\mathbf{w} \sim \mathcal{N}(0, \boldsymbol{\Sigma})$, where the covariance matrix entries are determined by a [kernel function](@entry_id:145324), $\boldsymbol{\Sigma}_{ab} = K(\mathbf{p}_a, \mathbf{p}_b)$, that depends on the spatial locations $\mathbf{p}_a, \mathbf{p}_b$ of the weights. This encodes the assumption that nearby weights should be correlated, promoting spatially smooth filters. In a [convolutional neural network](@entry_id:195435), the posterior over this single shared filter is informed by evidence from all patches in the input data. 

### Connections to Non-Bayesian Deep Learning

The principles of BNNs are deeply connected to the broader theory of deep learning, particularly in the infinite-width limit. This perspective provides a powerful theoretical bridge between the Bayesian and frequentist optimization-based viewpoints.

In the limit as layer widths go to infinity, and under a specific "Neural Tangent" [parameterization](@entry_id:265163), two key phenomena emerge. First, the distribution of the network function $f_\theta(x)$ at initialization, taken over the random draws of $\theta$, converges to a Gaussian Process. The covariance of this GP is given by the **Neural Network Gaussian Process (NNGP) kernel**:

$K_{\mathrm{NNGP}}(x, x') = \lim_{\text{width} \to \infty} \mathbb{E}_\theta[ f_\theta(x) f_\theta(x') ]$

This kernel is determined by the [network architecture](@entry_id:268981) and is fixed at initialization. It represents the prior over functions induced by the prior over weights.

Second, during training with [gradient descent](@entry_id:145942) on a squared error loss, the network's function evolution is governed by another kernel. The change in the function is driven by the dot product of its gradients with respect to the parameters. In the infinite-width limit, this dot product also converges to a deterministic kernel, the **Neural Tangent Kernel (NTK)**:

$\Theta(x, x') = \lim_{\text{width} \to \infty} \nabla_\theta f_\theta(x) \cdot \nabla_\theta f_\theta(x')$

The remarkable result of NTK theory is that for infinitely wide networks, this kernel remains "frozen" at its initial value throughout training. The training dynamics of the neural network become equivalent to performing kernel regression with the fixed NTK. This means that in this specific theoretical regime, a complex, [non-convex optimization](@entry_id:634987) problem on the parameters of a neural network simplifies to a linear update rule on the function's outputs. The NNGP kernel describes the Bayesian prior, while the NTK describes the path taken by [gradient-based optimization](@entry_id:169228), providing a profound link between these two worlds. 