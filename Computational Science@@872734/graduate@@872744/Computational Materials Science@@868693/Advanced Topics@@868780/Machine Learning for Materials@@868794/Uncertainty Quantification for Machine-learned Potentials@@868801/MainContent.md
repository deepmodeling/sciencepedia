## Introduction
Machine-learned potentials (MLPs) are revolutionizing [computational materials science](@entry_id:145245), offering the accuracy of [first-principles calculations](@entry_id:749419) at a fraction of the computational cost. This breakthrough enables simulations of unprecedented scale and complexity. However, the predictive power of MLPs comes with a critical challenge: reliability. As interpolative models, MLPs can produce unpredictable and unphysical results when applied to atomic configurations outside their training domain. The knowledge gap, therefore, is not just about making predictions, but about knowing how much to trust those predictions. Without a rigorous measure of confidence, MLPs remain powerful but potentially fragile tools.

This article addresses this challenge head-on by providing a comprehensive guide to uncertainty quantification (UQ) for MLPs. By learning to quantify predictive uncertainty, you will gain the ability to transform MLPs into robust and trustworthy scientific instruments. The following chapters will guide you through this essential topic. In "Principles and Mechanisms," you will explore the fundamental concepts of uncertainty, dissecting it into its core components and examining the primary statistical methods for its estimation, from model ensembles to Bayesian frameworks. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these UQ techniques are applied to solve tangible scientific problems, such as calculating reliable material properties, guiding simulations, and accelerating [materials discovery](@entry_id:159066) through [active learning](@entry_id:157812). Finally, "Hands-On Practices" will provide you with the opportunity to apply these concepts, solidifying your understanding by tackling practical challenges in [model validation](@entry_id:141140) and analysis.

## Principles and Mechanisms

The reliability of a [machine-learned potential](@entry_id:169760) (MLP) is paramount for its use in predictive [materials simulation](@entry_id:176516). While the previous chapter introduced the motivation for adopting MLPs, this chapter delves into the fundamental principles and mechanisms for quantifying their predictive uncertainty. A robust understanding of uncertainty is not merely an academic exercise; it is the foundation for building trustworthy models, guiding efficient [data acquisition](@entry_id:273490) through active learning, and propagating errors to make meaningful predictions about macroscopic material properties. We will dissect the nature of uncertainty, explore the primary methodologies for its quantification, and discuss the rigorous evaluation of the resulting probabilistic predictions.

### The Two Faces of Uncertainty: Epistemic and Aleatoric

In the context of statistical modeling, predictive uncertainty is not a monolithic concept. It is essential to distinguish between two fundamental types: **epistemic uncertainty** and **[aleatoric uncertainty](@entry_id:634772)**. Their origins, characteristics, and remedies are distinct, and treating them as such is crucial for developing and interpreting MLPs.

**Aleatoric uncertainty** (from the Latin *alea*, meaning "dice") refers to the inherent randomness or noise in the data-generating process. In the context of MLPs trained on data from Density Functional Theory (DFT), [aleatoric uncertainty](@entry_id:634772) arises from the numerical approximations and tolerances inherent in the DFT calculations themselves. For instance, the use of finite $k$-point meshes for Brillouin zone integration, incomplete [basis sets](@entry_id:164015), convergence thresholds for the [self-consistent field](@entry_id:136549) (SCF) cycle, and choices of electronic smearing for metals all introduce a level of irreducible noise into the computed energy and force labels [@problem_id:3500243]. This uncertainty is a property of the data source, not the MLP. Even with an infinitely flexible model and an infinite amount of training data generated under the *same* DFT protocol, this noise floor would remain. Aleatoric uncertainty can also be **heteroscedastic**, meaning its magnitude can vary depending on the atomic configuration; for example, DFT calculations for metallic systems or configurations near a phase transition may be less precise than for simple insulators.

**Epistemic uncertainty** (from the Greek *episteme*, meaning "knowledge") reflects the model's own lack of knowledge. This can be due to two primary sources: insufficient training data or limitations in the model architecture ([model misspecification](@entry_id:170325)). When an MLP is asked to predict the energy of an atomic configuration far from any it has seen during training, its [epistemic uncertainty](@entry_id:149866) will be high. This type of uncertainty is, in principle, reducible. By providing more training data in the regions of high uncertainty or by increasing the [expressive power](@entry_id:149863) of the model, we can reduce our "ignorance" and constrain the model's predictions.

A formal framework for separating these uncertainties is provided by Bayesian probability theory and the **law of total variance**. Consider a model with parameters $\boldsymbol{\theta}$ that makes a prediction for the energy $E$ of a configuration $\mathbf{R}$. Given a training dataset $\mathcal{D}$, the total predictive variance can be decomposed as follows [@problem_id:3500243] [@problem_id:3500252]:
$$
\operatorname{Var}(E \mid \mathbf{R}, \mathcal{D}) = \mathbb{E}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left[ \operatorname{Var}(E \mid \mathbf{R}, \boldsymbol{\theta}) \right] + \operatorname{Var}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left( \mathbb{E}[E \mid \mathbf{R}, \boldsymbol{\theta}] \right)
$$
In this decomposition, the first term, $\mathbb{E}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left[ \operatorname{Var}(E \mid \mathbf{R}, \boldsymbol{\theta}) \right]$, represents the **[aleatoric uncertainty](@entry_id:634772)**. It is the expected value of the data noise variance, averaged over the [posterior distribution](@entry_id:145605) of the model parameters $p(\boldsymbol{\theta} \mid \mathcal{D})$. The second term, $\operatorname{Var}_{\boldsymbol{\theta} \mid \mathcal{D}}\! \left( \mathbb{E}[E \mid \mathbf{R}, \boldsymbol{\theta}] \right)$, represents the **[epistemic uncertainty](@entry_id:149866)**. It is the variance of the model's mean prediction as the parameters $\boldsymbol{\theta}$ vary according to their posterior distribution. This term directly captures our uncertainty about which set of parameters is correct.

The scaling of these uncertainties with system size is also a critical consideration. Modern MLPs are often designed to be **extensive**, with the total energy being a sum of local atomic contributions. In such models, the [epistemic uncertainty](@entry_id:149866) on a per-atom basis can remain bounded even for large systems, provided the training set adequately covers the space of local chemical environments. In contrast, certain sources of [aleatoric uncertainty](@entry_id:634772), such as $k$-point [sampling error](@entry_id:182646) in DFT, can lead to total energy errors that grow with system size. In such cases, the total [aleatoric uncertainty](@entry_id:634772) may increase, while the per-atom [aleatoric uncertainty](@entry_id:634772) remains approximately constant [@problem_id:3500243].

### Methods for Quantifying Epistemic Uncertainty

A variety of methods have been developed to estimate the [epistemic uncertainty](@entry_id:149866) of MLPs. These can be broadly categorized into ensemble-based approaches and Bayesian methods.

#### Ensemble-Based Methods

The conceptually simplest and often the most effective method for estimating [epistemic uncertainty](@entry_id:149866) is to use an **ensemble** or **committee** of models. The core idea is to train multiple ($M$) independent models and use the variance in their predictions as a proxy for [epistemic uncertainty](@entry_id:149866). The independence of the models is typically encouraged by using different random weight initializations and training each model on a different bootstrap resample of the training data [@problem_id:3500187].

For a given input configuration $x$ (which could represent a full [atomic structure](@entry_id:137190) or a local environment), each model $m$ in the committee produces a prediction $y_m(x)$ (e.g., an energy or a force component). Assuming the predictions $\{y_m(x)\}_{m=1}^M$ can be treated as independent and identically distributed samples from the model's predictive distribution, we can estimate the moments of this distribution. The ensemble predictive mean, $\bar{y}(x)$, is simply the sample mean:
$$
\bar{y}(x) = \frac{1}{M} \sum_{m=1}^{M} y_m(x)
$$
The epistemic variance is estimated by the unbiased sample variance of the predictions, which includes Bessel's correction:
$$
s^2(x) = \frac{1}{M-1} \sum_{m=1}^{M} \left( y_m(x) - \bar{y}(x) \right)^2
$$
This approach is powerful due to its simplicity and parallelizability. The same statistical logic applies whether the quantity being predicted is energy or a force component, as long as the models in the committee are trained independently [@problem_id:3500187].

#### Bayesian Methods

Bayesian methods provide a more deeply principled but often more computationally intensive framework for uncertainty quantification. The central idea is to treat the model parameters $\mathbf{w}$ not as single [point estimates](@entry_id:753543) but as random variables, described by a probability distribution.

##### Gaussian Processes

A **Gaussian Process (GP)** is a non-parametric Bayesian model that defines a [prior distribution](@entry_id:141376) directly over functions. An MLP based on a GP models the [potential energy surface](@entry_id:147441) $E(\mathbf{R})$ as a draw from a distribution of functions, specified by a mean function (typically assumed to be zero) and a [covariance function](@entry_id:265031), or **kernel**, $k(\mathbf{R}, \mathbf{R}')$. The kernel encodes our prior assumptions about the function's properties, such as its smoothness. It defines the covariance between the energy values at any two configurations $\mathbf{R}$ and $\mathbf{R}'$.

A powerful feature of GPs is their natural handling of structured inputs and outputs. For instance, if the total energy of a structure $S$ is modeled as a sum of local contributions, $E(S) = \sum_{i=1}^{N(S)} f(a_i)$, where $f(a_i)$ is the energy of the local environment $a_i$ modeled by a GP, then the total energy $E(S)$ is also a GP. The covariance between the total energies of two structures, $S$ and $S'$, is derived by summing the kernel function over all pairs of atomic environments from the two structures [@problem_id:3500242]:
$$
\operatorname{Cov}(E(S), E(S')) = \sum_{i=1}^{N(S)} \sum_{j=1}^{N(S')} \operatorname{Cov}(f(a_i), f(a'_j)) = \sum_{i=1}^{N(S)} \sum_{j=1}^{N(S')} k(a_i, a'_j)
$$
For example, a kernel based on the similarity of Smooth Overlap of Atomic Positions (SOAP) descriptors $\mathbf{s}(a)$ could be $k(a,a') = \sigma_{f}^{2} ( \hat{\mathbf{s}}(a) \cdot \hat{\mathbf{s}}(a') )^{\zeta}$, where $\hat{\mathbf{s}}(a)$ is the normalized descriptor.

A critical aspect of GP potentials is their ability to incorporate **derivative observations**, such as atomic forces. Since the force is the negative gradient of the energy, $\mathbf{F}(\mathbf{R}) = -\nabla_{\mathbf{R}}E(\mathbf{R})$, and differentiation is a [linear operator](@entry_id:136520), the forces are also jointly Gaussian with the energies. The necessary cross-covariances can be derived by applying the differentiation operators to the base energy kernel. For a one-dimensional system, for example, the energy-force and force-force covariances are [@problem_id:3500223]:
$$
k_{E,F}(x, x') = \operatorname{Cov}(E(x), F(x')) = -\frac{\partial k(x, x')}{\partial x'}
$$
$$
k_{F,F}(x, x') = \operatorname{Cov}(F(x), F(x')) = \frac{\partial^2 k(x, x')}{\partial x \partial x'}
$$
Observing a noiseless energy value at a specific configuration $\mathbf{R}^*$ will drive the predictive [energy variance](@entry_id:156656) at that point to zero. However, this does not mean the force uncertainty vanishes. Unless the kernel imposes a deterministic relationship between a function's value and its gradient at a point (which is not true for common kernels like the squared-exponential), observing the energy value only partially constrains the gradient. Thus, it is possible to have zero predictive variance for the energy but non-zero predictive variance for the forces, highlighting that energy and forces provide distinct, albeit correlated, information to the model [@problem_id:3500252].

##### Bayesian Neural Networks

**Bayesian Neural Networks (BNNs)** extend the Bayesian philosophy to [deep learning](@entry_id:142022) by placing a prior distribution over the network's weights, $p(\mathbf{w})$. Given training data $\mathcal{D}$, one computes the posterior distribution $p(\mathbf{w} \mid \mathcal{D})$ via Bayes' rule. Predictions are then made by marginalizing over this posterior.

In practice, the exact posterior is intractable. A common solution is **[variational inference](@entry_id:634275) (VI)**. In VI, we approximate the true posterior with a simpler, parameterized distribution $q(\mathbf{w})$, often a fully-factorized (mean-field) Gaussian [@problem_id:3500173]:
$$
q(\mathbf{w}) = \prod_{j=1}^{D} \mathcal{N}(w_j \mid m_j, s_j^2)
$$
The variational parameters (means $\mathbf{m}$ and variances $\mathbf{s}^2$) are optimized to minimize the Kullback-Leibler (KL) divergence $\mathrm{KL}(q(\mathbf{w}) \,\|\, p(\mathbf{w} \mid \mathcal{D}))$. This is equivalent to maximizing the Evidence Lower Bound (ELBO), which consists of a data likelihood term and a regularization term corresponding to the KL divergence between the variational posterior and the prior, $\mathrm{KL}(q(\mathbf{w}) \,\|\, p(\mathbf{w}))$.

A popular and computationally efficient approximation to BNNs is **Monte Carlo (MC) dropout**. It has been shown that a standard neural network trained with dropout and $\ell_2$ regularization is approximately performing [variational inference](@entry_id:634275) [@problem_id:3500238]. To obtain uncertainty estimates at test time, dropout is kept active, and one performs $K$ stochastic forward passes through the network, each with a different random dropout mask. This process effectively draws $K$ samples of the weights from the approximate variational posterior. For each sample $\mathbf{w}_k$, a force prediction $\mathbf{F}_k$ is computed. The predictive mean and epistemic covariance are then estimated using the [sample mean](@entry_id:169249) and sample covariance of the $\{\mathbf{F}_k\}_{k=1}^K$ predictions. This epistemic uncertainty is distinct from the [aleatoric uncertainty](@entry_id:634772), which would be represented by the variance parameter of the model's [likelihood function](@entry_id:141927) [@problem_id:3500238].

### The Role of Symmetries in Reducing Uncertainty

Physical laws are symmetric under operations like rotation, translation, and permutation of identical atoms. Incorporating these symmetries into an MLP architecture, a property known as **equivariance**, is not only elegant but also a powerful mechanism for reducing uncertainty. An equivariant model understands *a priori* that if a configuration $x$ is rotated to $Rx$, the predicted force vector $f(x)$ must rotate accordingly to $Rf(x)$.

This built-in knowledge acts as a potent prior that allows the model to generalize far more effectively. When an equivariant model is trained on a single data point $(x, y)$, it implicitly learns about the entire **symmetry orbit** of that point, i.e., all pairs $(Rx, Ry)$ for all valid rotations $R$. In a Bayesian framework, this means that an observation at $x$ will reduce the posterior variance not just at $x$, but equally across its entire orbit. In contrast, a generic, non-equivariant model would gain little to no information about the system at $Rx$ from an observation at $x$, and would require explicit training on data from all parts of the orbit to learn the symmetry [@problem_id:3500195]. For finite symmetry groups, such as crystal point groups, this provides an enormous data-efficiency gain, effectively giving the model the benefit of a dataset augmented by all group operations without the computational cost of training on such a large dataset [@problem_id:3500195].

### Distribution-Free Uncertainty and Calibration

The methods discussed so far produce a model-dependent estimate of uncertainty. An alternative and complementary approach is **[conformal prediction](@entry_id:635847)**, a framework that can wrap around any underlying model to produce prediction sets with rigorous, distribution-free coverage guarantees.

The **split [conformal prediction](@entry_id:635847)** algorithm works as follows: the data is split into a proper [training set](@entry_id:636396) and a calibration set. A model is trained on the training set. Then, for each point $(x_i, y_i)$ in the calibration set, a **nonconformity score** $s_i$ is computed, which measures how "strange" the true observation $y_i$ is relative to the model's prediction for $x_i$. The $(1-\alpha)$ quantile of these calibration scores is then used as a threshold to define prediction sets for new inputs. By construction, these sets are guaranteed to contain the true outcome with a probability of at least $1-\alpha$, regardless of the underlying data distribution, as long as the data is exchangeable [@problem_id:3500220].

For vector-valued force predictions, where a model might output a [mean vector](@entry_id:266544) $\mu(x)$ and a covariance matrix $\Sigma(x)$, a sophisticated nonconformity score can be defined using the **Mahalanobis norm** of the residual:
$$
s(x, y) = \sqrt{(y - \mu(x))^{\top} \Sigma(x)^{-1} (y - \mu(x))}
$$
This score intelligently uses the model's own (possibly uncalibrated) uncertainty estimate $\Sigma(x)$ to measure discrepancy. Regions where the model predicts high variance will be down-weighted, leading to adaptively shaped prediction sets (ellipsoids) that are more informative than simple spheres based on Euclidean distance [@problem_id:3500220].

### Evaluating Predictive Uncertainty

Finally, it is not sufficient to simply produce uncertainty estimates; we must rigorously assess their quality. The key concept here is **[probabilistic calibration](@entry_id:636701)**. A model is said to be perfectly calibrated if its [predictive distributions](@entry_id:165741) match the true conditional distributions of the data.

A formal test for calibration is provided by the **probability [integral transform](@entry_id:195422) (PIT)**. For a continuous target variable, if the model is calibrated, the PIT values $U_i = F_i(y_i)$, where $F_i$ is the model's predictive cumulative distribution function (CDF) for observation $y_i$, should be uniformly distributed on the interval $[0,1]$ [@problem_id:3500250]. Visualizing the distribution of PIT values or quantifying its deviation from uniformity provides a direct way to assess calibration.

Several quantitative metrics, known as **proper scoring rules**, are used to evaluate probabilistic forecasts. These rules are designed to be minimized, in expectation, only when the predicted distribution equals the true data-generating distribution.
- **Negative Log-Likelihood (NLL)**, or logarithmic score, is a widely used proper scoring rule. For a Gaussian prediction with mean $\mu_i$ and variance $\sigma_i^2$, it takes the form $\frac{1}{2}\log(2\pi \sigma_i^2) + \frac{(y_i - \mu_i)^2}{2\sigma_i^2}$, which penalizes both inaccurate means and poorly estimated variances [@problem_id:3500250].
- **Continuous Ranked Probability Score (CRPS)** is another strictly proper scoring rule that generalizes the mean absolute error to probabilistic forecasts. It is defined as the integrated squared difference between the forecast CDF $F$ and the empirical CDF of the observation $y$:
$$
\mathrm{CRPS}(F,y) = \int_{-\infty}^{\infty} ( F(z) - \mathbf{1}\{z \ge y\} )^2 \, dz
$$
Lower CRPS values indicate a better combination of accuracy and calibration [@problem_id:3500250].

Direct measures of miscalibration can also be computed. For example, an **Expected Calibration Error (ECE)** can be defined by [binning](@entry_id:264748) the PIT values and measuring the average deviation of their empirical CDF from the ideal uniform CDF. A well-calibrated model will exhibit an ECE close to zero [@problem_id:3500250]. These evaluation tools are indispensable for validating the trustworthiness of an MLP's uncertainty estimates before deploying it in real-world simulations.