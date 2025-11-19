## Introduction
How do we design experiments that are maximally informative? In any scientific or engineering endeavor, from placing sensors to monitor a geological field to designing a clinical trial, the choice of experimental setup is critical. A poorly designed experiment can waste resources and yield ambiguous results, while a well-designed one can accelerate discovery. The central challenge is to quantify the value of a potential experiment *before* it is conducted, allowing for a rational and optimal choice among alternatives.

This article explores the Expected Information Gain (EIG), a rigorous and principled framework rooted in Bayesian inference and information theory that directly addresses this challenge. EIG provides a universal currency for measuring the anticipated reduction in uncertainty an experiment will provide about unknown parameters or competing models. By moving beyond [heuristics](@entry_id:261307), EIG enables a systematic approach to designing experiments that are provably optimal from an informational perspective.

The following chapters will guide you through this powerful framework. The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, defining EIG and deriving its key formulations for both simple and complex models. The second chapter, **Applications and Interdisciplinary Connections**, will showcase its remarkable versatility across diverse scientific domains, from geophysics to astronomy. Finally, the **Hands-On Practices** chapter will allow you to apply these concepts to concrete problems, solidifying your understanding of how to leverage EIG for rational scientific inquiry.

## Principles and Mechanisms

The primary goal of experimental design is to conduct experiments that are maximally informative for a given scientific question. The Expected Information Gain (EIG) provides a rigorous and principled framework, rooted in Bayesian inference and information theory, for quantifying the value of a proposed experiment before it is performed. This chapter elucidates the fundamental principles of EIG, derives its formulations for [canonical models](@entry_id:198268), and explores its application in more complex and realistic scenarios.

### Defining Expected Information Gain

At its core, EIG measures the amount of information an experiment is expected to yield about a set of unknown parameters, denoted by the vector $\theta$. Formally, the EIG for a given experimental design $d$ is defined as the **[mutual information](@entry_id:138718)** between the parameter vector $\theta$ and the future observation vector $Y$, written as $I(\theta; Y \mid d)$.

Mutual information can be understood through two equivalent perspectives. The first defines it as the expected reduction in the uncertainty of the parameters upon receiving data. In information theory, uncertainty is quantified by **[differential entropy](@entry_id:264893)**, denoted by $H(\cdot)$. The EIG is thus the difference between the prior entropy of the parameters and the expected posterior entropy after the data are observed:

$$
I(\theta; Y \mid d) = H(\theta) - H(\theta \mid Y, d)
$$

Here, $H(\theta)$ is the entropy of the prior distribution $p(\theta)$, representing our state of knowledge before the experiment. The term $H(\theta \mid Y, d)$ is the conditional entropy of $\theta$ given the data $Y$, which is the average entropy of the posterior distribution $p(\theta \mid y, d)$ over all possible data outcomes $y$. This formulation directly captures the intuitive goal of experimental design: to reduce our uncertainty about $\theta$.

This perspective allows us to distinguish between two types of uncertainty [@problem_id:3380352]. **Epistemic uncertainty** is our lack of knowledge about the true value of the parameter $\theta$. **Aleatoric uncertainty** is the inherent, irreducible randomness in the measurement process, often modeled by an [additive noise](@entry_id:194447) term. The EIG quantifies the expected reduction in *epistemic* uncertainty. The [aleatoric uncertainty](@entry_id:634772), which represents the fundamental limits of the measurement device, cannot be reduced by a single observation, but a well-designed experiment minimizes its negative impact on our ability to learn about $\theta$.

The second, equivalent perspective defines mutual information as the information that the data provides about the parameters. This is expressed as the difference between the entropy of the data itself and the entropy of the data when the parameter is known:

$$
I(\theta; Y \mid d) = H(Y \mid d) - H(Y \mid \theta, d)
$$

Here, $H(Y \mid d)$ is the entropy of the marginal (or prior predictive) distribution of the data, $p(y \mid d) = \int p(y \mid \theta, d) p(\theta) d\theta$. It represents the total variability of the data, arising from both the uncertainty in the parameters and the noise in the measurement. The term $H(Y \mid \theta, d)$ is the entropy of the data conditional on the parameter, which quantifies the variability due solely to measurement noise. This formulation views EIG as the fraction of the total data uncertainty that is explained by the uncertainty in the parameters.

Finally, EIG can also be expressed as the expected **Kullback-Leibler (KL) divergence** from the [prior distribution](@entry_id:141376) to the posterior distribution:

$$
I(\theta; Y \mid d) = \mathbb{E}_{p(y|d)} \left[ D_{\text{KL}}(p(\theta|y,d) \,\|\, p(\theta)) \right]
$$

The KL divergence $D_{\text{KL}}(p_1 \,\|\, p_0)$ measures the "distance" or dissimilarity from a prior distribution $p_0$ to a [posterior distribution](@entry_id:145605) $p_1$. The EIG is thus the average dissimilarity we expect to see between our posterior and prior beliefs as a result of the experiment. These three definitions are mathematically equivalent and provide complementary insights into the nature of [information gain](@entry_id:262008).

### The Linear-Gaussian Case: An Exact Solution

The most foundational application of EIG is in the linear-Gaussian inverse problem, where all distributions are normal and all relationships are linear. This model, while simple, provides a [closed-form solution](@entry_id:270799) for the EIG that serves as a building block for more complex scenarios [@problem_id:3380334].

Consider a parameter vector $\theta \in \mathbb{R}^n$ with a Gaussian [prior distribution](@entry_id:141376) $\theta \sim \mathcal{N}(\mu_0, C_0)$. The data $Y \in \mathbb{R}^m$ are generated by a linear forward model with additive Gaussian noise:
$$
Y = H\theta + \varepsilon, \quad \text{where } \varepsilon \sim \mathcal{N}(0, R)
$$
Here, $H \in \mathbb{R}^{m \times n}$ is the forward operator or design matrix, and $R$ is the covariance of the observation noise.

To derive the EIG, we use the formulation $I(\theta; Y|d) = H(Y|d) - H(Y|\theta, d)$. For a $k$-dimensional Gaussian variable with covariance $\Sigma$, the [differential entropy](@entry_id:264893) is $\frac{1}{2} \ln \det(2\pi e \Sigma)$.

First, we find the [marginal distribution](@entry_id:264862) of the data, $p(y|d)$. As a [linear transformation](@entry_id:143080) of a Gaussian variable ($\theta$) plus an independent Gaussian variable ($\varepsilon$), $Y$ is also Gaussian. Its mean and covariance are:
$$
\mathbb{E}[Y] = \mathbb{E}[H\theta + \varepsilon] = H\mathbb{E}[\theta] + \mathbb{E}[\varepsilon] = H\mu_0
$$
$$
\text{Cov}(Y) = \text{Cov}(H\theta + \varepsilon) = H \text{Cov}(\theta) H^T + \text{Cov}(\varepsilon) = H C_0 H^T + R
$$
The marginal entropy is therefore $H(Y|d) = \frac{1}{2} \ln \det(2\pi e (H C_0 H^T + R))$.

Next, we find the [conditional distribution](@entry_id:138367) of the data given the parameter, $p(y|\theta, d)$. If $\theta$ is known, $Y$ is simply a shifted version of the noise: $Y|\theta \sim \mathcal{N}(H\theta, R)$. The entropy of this distribution is $H(Y|\theta, d) = \frac{1}{2} \ln \det(2\pi e R)$. Crucially, this entropy does not depend on the specific value of $\theta$.

Subtracting the two entropies yields the EIG:
$$
I(\theta; Y|d) = \frac{1}{2} \left[ \ln \det(2\pi e (H C_0 H^T + R)) - \ln \det(2\pi e R) \right]
$$
$$
I(\theta; Y|d) = \frac{1}{2} \left[ \ln \det(H C_0 H^T + R) - \ln \det(R) \right]
$$
This is the celebrated [closed-form expression](@entry_id:267458) for EIG in the linear-Gaussian case. Several important properties are immediately apparent:
- The EIG is independent of the prior mean $\mu_0$. It only depends on the prior uncertainty, $C_0$, the [experimental design](@entry_id:142447), $H$, and the noise characteristics, $R$ [@problem_id:3380352].
- If the design provides no information (i.e., $H=0$), then EIG is $\frac{1}{2} (\ln \det(R) - \ln \det(R)) = 0$. No information can be gained.
- If there is no prior uncertainty (i.e., $C_0=0$, a degenerate case), then EIG is also zero. If we already know $\theta$, no experiment can be informative about it [@problem_id:3380352].
- As the observation noise increases (i.e., the eigenvalues of $R$ increase), the EIG decreases, reflecting the fact that noisier measurements are less informative.

### Alternative Formulations and Computational Aspects

The EIG formula can be rewritten in several ways that offer different computational advantages and insights. By using the property $\ln(\det(A)) - \ln(\det(B)) = \ln(\det(AB^{-1}))$, the EIG expression can be written as:
$$
I(\theta; Y|d) = \frac{1}{2} \ln \det(I_m + H C_0 H^T R^{-1})
$$
This is known as the **observation-space formulation** because the [matrix determinant](@entry_id:194066) is computed in the $m$-dimensional space of the data.

An alternative derivation using the definition $I(\theta; Y|d) = H(\theta) - H(\theta|Y,d)$ leads to a **parameter-space formulation** [@problem_id:3380387]. For the linear-Gaussian model, the [posterior distribution](@entry_id:145605) $p(\theta|y)$ is also Gaussian, with a [posterior covariance](@entry_id:753630) $C_{\text{post}}$ that is independent of the data $y$:
$$
C_{\text{post}} = (C_0^{-1} + H^T R^{-1} H)^{-1}
$$
The EIG is then the difference between the prior and posterior entropies:
$$
I(\theta; Y|d) = \frac{1}{2} \left[ \ln \det(C_0) - \ln \det(C_{\text{post}}) \right] = \frac{1}{2} \ln \det(C_0 C_{\text{post}}^{-1}) = \frac{1}{2} \ln \det(I_n + C_0 H^T R^{-1} H)
$$
The equivalence of the observation-space and parameter-space formulations is a direct consequence of the **[matrix determinant lemma](@entry_id:186722)**, which states that $\det(I_k + AB) = \det(I_j + BA)$ for matrices $A \in \mathbb{R}^{k \times j}$ and $B \in \mathbb{R}^{j \times k}$.

The existence of these two forms has significant computational implications. The observation-[space form](@entry_id:203017) requires computing the determinant of an $m \times m$ matrix, while the parameter-[space form](@entry_id:203017) requires an $n \times n$ determinant. In many [inverse problems](@entry_id:143129), the number of parameters $n$ is very large (e.g., a discretized field), while the number of measurements $m$ is relatively small. In such cases ($m \ll n$), the observation-space formulation is vastly more computationally efficient [@problem_id:3380387]. For numerical stability, especially with high-dimensional or poorly conditioned matrices, the [log-determinant](@entry_id:751430) should be computed via Cholesky decomposition rather than by computing the determinant directly [@problem_id:3380334].

### EIG in the Context of Optimal Experimental Design

The EIG criterion is closely related to other classical criteria in Optimal Experimental Design (OED). For the linear-Gaussian model, maximizing the EIG is mathematically equivalent to minimizing the determinant of the [posterior covariance matrix](@entry_id:753631), $\det(C_{\text{post}})$. This is precisely the objective of **Bayesian D-optimality** [@problem_id:3380385].

However, EIG possesses a crucial advantage over many classical criteria: **invariance to [reparameterization](@entry_id:270587)**. If we change our parameter representation via an [invertible linear transformation](@entry_id:149915) $\theta' = T\theta$, the EIG remains unchanged: $I(\theta'; Y \mid d) = I(\theta; Y \mid d)$. This means that the informational value of an experiment does not depend on the arbitrary choice of coordinate system for the parameters. In contrast, other criteria like A-optimality (minimizing $\text{tr}(C_{\text{post}})$) or E-optimality (minimizing the largest eigenvalue of $C_{\text{post}}$) are not invariant under general linear transformations. This invariance establishes EIG as a more fundamental measure of experimental value [@problem_id:3380385].

### Extending Beyond the Linear-Gaussian Model

While the linear-Gaussian model provides essential insights, most real-world scientific models are nonlinear. For a general nonlinear model, $Y = g(\theta) + \varepsilon$, a [closed-form expression](@entry_id:267458) for EIG is typically not available. This is because the posterior distribution $p(\theta|y)$ is non-Gaussian, and its shape and entropy depend on the specific data realization $y$.

A powerful method for handling such cases is the **Laplace approximation** [@problem_id:3380408]. This technique approximates the [posterior distribution](@entry_id:145605) $p(\theta|y)$ with a Gaussian distribution centered at the maximum a posteriori (MAP) estimate, $\theta_{\text{MAP}}(y)$. The covariance of this approximating Gaussian is the inverse of the Hessian of the negative log-posterior evaluated at the MAP point. The resulting approximate EIG becomes an expectation over all possible data outcomes:
$$
I(\theta; Y \mid d) \approx \frac{1}{2} \mathbb{E}_{Y \mid d}\left[\ln \det\left(\Sigma_0 \left(\Sigma_0^{-1} + H_{\mathcal{L}}(\theta_{\text{MAP}}(y))\right)\right)\right] = \frac{1}{2} \mathbb{E}_{Y \mid d}\left[\ln \det\left(I_n + \Sigma_0 H_{\mathcal{L}}(\theta_{\text{MAP}}(y))\right)\right]
$$
Here, $H_{\mathcal{L}}$ is the Hessian of the [negative log-likelihood](@entry_id:637801). Unlike the linear case where the [information matrix](@entry_id:750640) is constant, here it depends on the parameter value and includes contributions from both the model's local slope (Jacobian) and its local curvature (second derivatives of $g(\theta)$). The computation of this expectation is a significant challenge, often requiring Monte Carlo methods.

To make the role of nonlinearity more concrete, consider a simple scalar model $y = a\theta + c\theta^2 + \varepsilon$. A standard [linearization](@entry_id:267670) approach would approximate the model as $y \approx a\theta + \varepsilon$, leading to an EIG that depends only on the linear coefficient $a$. However, a more accurate approximation of the EIG that accounts for the quadratic term reveals an additional positive contribution to the [information gain](@entry_id:262008) that is proportional to $c^2$. This discrepancy highlights that model curvature can be a source of information that is entirely missed by simple linearization [@problem_id:3380420].

### Advanced Topics and Practical Considerations

#### Information Gain for a Quantity of Interest

In many applications, the goal is not to learn the entire parameter vector $\theta$, but rather a specific, often lower-dimensional, **quantity of interest (QoI)**, $Q(\theta)$. The objective then becomes maximizing $I(Q(\theta); Y \mid d)$.

The relationship between the EIG for the parameters and the EIG for the QoI is governed by the **Data Processing Inequality** from information theory. Because $Q(\theta)$ is a function of $\theta$, the variables form a Markov chain $Y - \theta - Q(\theta)$. This implies that any information the data provides about the QoI must be "processed" through the full parameter vector. Consequently, we have the fundamental inequality [@problem_id:3380351]:
$$
I(\theta; Y \mid d) \ge I(Q(\theta); Y \mid d)
$$
One cannot gain more information about a function of a variable than about the variable itself. Equality holds if and only if $Q(\theta)$ is a **sufficient statistic** for $\theta$ with respect to the data $y$, or, as a special case, if $Q$ is a bijective (one-to-one) transformation of $\theta$. In general, an experiment that is optimal for learning $\theta$ is not necessarily optimal for learning $Q(\theta)$, and the design objective must be chosen to align with the scientific goal.

#### Hierarchical Models and Hyperparameters

Scientific models often involve **hierarchical priors**, where parameters of interest $\theta$ have a [prior distribution](@entry_id:141376) $p(\theta|\lambda)$ that depends on hyperparameters $\lambda$, which themselves have a prior $p(\lambda)$. A key design question is whether to focus on learning $\theta$ or to also account for uncertainty in $\lambda$ [@problem_id:3380360].

The [chain rule for mutual information](@entry_id:271702) provides a clear answer:
$$
I((\theta, \lambda); y \mid d) = I(\theta; y \mid d) + I(\lambda; y \mid \theta, d)
$$
The joint EIG for both parameters and hyperparameters is the sum of the marginal EIG for $\theta$ and the EIG for $\lambda$ *given* knowledge of $\theta$.

If the likelihood $p(y|\theta,d)$ does not depend on $\lambda$, then learning $\theta$ perfectly would leave no information to be gained about $\lambda$ from the data, so $I(\lambda; y \mid \theta, d)=0$. In this case, the joint and marginal EIG objectives are identical, $I((\theta, \lambda); y \mid d) = I(\theta; y \mid d)$. If, however, the likelihood depends on $\lambda$ (e.g., $\lambda$ is a parameter of the noise model), then $I(\lambda; y \mid \theta, d) > 0$. An experiment can now be designed to learn about the hyperparameters directly, and the joint EIG will be greater than the marginal EIG.

#### Model Misspecification and Robust Design

The EIG formulations discussed so far assume that the statistical model (prior and likelihood) is a perfect representation of reality. In practice, all models are approximations. **Model misspecification** can lead to a biased assessment of an experiment's value. For example, if a model contains both structured model error and random observation noise, but a practitioner incorrectly lumps them together as a single, independent noise term, the calculated EIG will be incorrect. The true EIG depends on the complete error structure, including any correlations between [model error](@entry_id:175815) and the parameters, and ignoring this structure can lead to suboptimal experimental designs [@problem_id:3380389].

To address this, we can formulate a **distributionally robust** EIG objective. Instead of assuming a single nominal likelihood $p_{\phi}(y|\theta,d)$, we can define an [ambiguity set](@entry_id:637684) $\mathcal{Q}_{\rho}$ of plausible "true" likelihoods that are close to the nominal one (e.g., within a certain KL-divergence radius). The robust design goal is to choose an experiment that performs well even under the worst-case likelihood in this set. The objective becomes [@problem_id:3380353]:
$$
\text{maximize}_d \left( \inf_{q \in \mathcal{Q}_{\rho}(d)} \mathbb{E}_{p(\theta)q(y|\theta,d)} \left[ \log p_{\phi}(\theta|y,d) - \log p(\theta) \right] \right)
$$
This expression seeks to maximize the [information gain](@entry_id:262008) that is guaranteed, even when nature chooses the most adversarial data-generating process $q$ from the [ambiguity set](@entry_id:637684), while our inference remains based on the nominal posterior $p_{\phi}$. This maximin approach provides a path toward designing experiments that are resilient to our own modeling uncertainties, representing a frontier in information-theoretic [experimental design](@entry_id:142447).