## Introduction
In the pursuit of understanding and predicting complex systems, from Earth's climate to economic markets, computational models are indispensable tools. However, every model is an approximation of reality, and its predictions are inevitably subject to uncertainty. While uncertainty from data inputs and model parameters is widely studied, a more profound and challenging source lies in the very structure of the model itself—the choice of equations, processes, and their interactions. This is known as [model structural uncertainty](@entry_id:1128051), and failing to account for it can lead to overconfident and unreliable predictions.

This article addresses this critical knowledge gap by providing a comprehensive guide to the analysis of [model structural uncertainty](@entry_id:1128051). We will equip you with the theoretical and practical tools to diagnose, quantify, and manage this pervasive form of uncertainty. First, in **Principles and Mechanisms**, we will establish a rigorous foundation by defining structural uncertainty, exploring its origins, and introducing formal frameworks like Bayesian Model Averaging. Next, in **Applications and Interdisciplinary Connections**, we will demonstrate how these principles are applied to create robust forecasts and guide decision-making in fields from hydrology to public health. Finally, the **Hands-On Practices** section provides concrete exercises to solidify your understanding of key analytical methods. By navigating these chapters, you will gain the expertise to move beyond single-model thinking and embrace a more robust, uncertainty-aware approach to modeling.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing the analysis of [model structural uncertainty](@entry_id:1128051). Building upon the introductory concepts, we will systematically dissect the nature of structural uncertainty, explore its origins in the modeling process, present formal frameworks for its quantification, and discuss practical methods for [model comparison](@entry_id:266577) and selection. Our objective is to provide a rigorous conceptual foundation for diagnosing, representing, and managing this critical component of predictive uncertainty in environmental and Earth system models.

### A Taxonomy of Model Uncertainty

In any modeling endeavor, the discrepancy between model predictions and real-world observations arises from multiple sources. A clear taxonomy is essential for diagnosing and treating these sources appropriately. Total predictive uncertainty is commonly decomposed into three principal categories: **input uncertainty**, **[parametric uncertainty](@entry_id:264387)**, and **[structural uncertainty](@entry_id:1132557)**.

**Input uncertainty** arises from imperfect knowledge of the data used to force or initialize a model. This includes errors in measurements of boundary conditions (e.g., sea surface temperature), initial conditions (e.g., the initial state of the atmosphere), or external forcings (e.g., aerosol emissions or land-use change scenarios). These errors propagate through the model's dynamics, contributing to uncertainty in the final output.

**Parametric uncertainty** refers to the uncertainty in the values of the parameters within a *given* model structure. Parameters are the coefficients and constants embedded in the model's equations that are not known from first principles and must be estimated or "tuned" based on observational data. Since this estimation is never perfect, the parameter values are uncertain. A standard method for exploring this uncertainty is the **Perturbed Physics Ensemble (PPE)**, where a single model is run many times with different plausible values for its parameters. Calibration against observations can constrain the plausible range of these parameters, thereby reducing [parametric uncertainty](@entry_id:264387).

**Structural uncertainty**, the focus of this chapter, is arguably the most challenging category. It arises because any model is, by necessity, a simplification and abstraction of the complex reality it seeks to represent. The choice of which physical processes to include, how to represent them mathematically, and how to couple them constitutes the model's **structure**. Different valid scientific hypotheses about these processes lead to different model structures. Structural uncertainty is the uncertainty that stems from this choice of model formulation itself. For instance, consider the representation of cloud [autoconversion](@entry_id:1121257) (the process by which cloud droplets coalesce into raindrops). One model structure, $\mathcal{S}_1$, might use a power-law formulation, while an alternative, $\mathcal{S}_2$, might use a different functional form, such as a threshold-based activation. The differences in predictions between $\mathcal{S}_1$ and $\mathcal{S}_2$, even if both are meticulously calibrated (i.e., their respective parameters are optimally tuned), represent structural uncertainty . This uncertainty reflects our incomplete knowledge of the fundamental physics and cannot be eliminated merely by tuning. A **Multi-Model Ensemble (MME)**, which collects results from different models (e.g., $\mathcal{S}_1, \mathcal{S}_2, \dots$), is a primary tool for sampling and assessing structural uncertainty.

### Sources and Manifestations of Structural Uncertainty

Structural uncertainty is not an abstract concept; it originates from concrete decisions made during model construction. Understanding these sources is key to appreciating its pervasive influence.

#### Alternative Functional Forms: The Simplest Case

The most direct source of structural uncertainty is the choice of mathematical equations to represent a physical process. A simple but illuminating example can be found in zero-dimensional Energy Balance Models (EBMs) of the Earth's climate . In such a model, the equilibrium temperature $T$ is determined by the balance between absorbed solar radiation and outgoing longwave radiation (OLR), denoted $L(T)$. The functional form of $L(T)$ must be specified.

One physically-grounded choice ($\mathcal{M}_1$) is to use the Stefan-Boltzmann law for a gray body: $L(T) = \varepsilon\sigma T^4$, where $\varepsilon$ is an effective emissivity and $\sigma$ is the Stefan-Boltzmann constant. This form captures the fundamental nonlinearity of thermal radiation.

An alternative choice ($\mathcal{M}_2$), often used for its simplicity, is a linear approximation around a reference temperature $T_0$: $L(T) = A + B(T - T_0)$. Here, the parameters $A$ and $B$ are typically chosen to match the value and slope of the nonlinear form at $T_0$.

Suppose both models are calibrated to produce the same equilibrium temperature ($T_0=288\,\mathrm{K}$) for present-day conditions ($\Delta F = 0$). While they agree at this single point, their response to a forcing (e.g., an increase in greenhouse gases, represented by $\Delta F > 0$) will differ. A forcing of $\Delta F = 4\,\mathrm{W\,m^{-2}}$ might yield a temperature increase of $1.20\,\mathrm{K}$ in the nonlinear model versus $1.25\,\mathrm{K}$ in the linear one—a small difference. However, for a larger forcing of $\Delta F = 20\,\mathrm{W\,m^{-2}}$, the predictions diverge more significantly: a $5.75\,\mathrm{K}$ warming in the nonlinear model versus a $6.25\,\mathrm{K}$ warming in the linear one. This divergence is a direct consequence of their different structures (nonlinearity versus linearity) and persists no matter how well the models are tuned at the reference state. It exemplifies a core principle: **calibration reduces parametric uncertainty but does not eliminate [structural uncertainty](@entry_id:1132557)**.

#### The Aggregation Problem: Parameterization and Closures

In complex Earth system models, a major source of [structural uncertainty](@entry_id:1132557) arises from the need to represent processes that occur at scales smaller than the model's grid resolution. This is known as the **parameterization** or **closure** problem. For example, cloud formation and precipitation involve microphysical interactions at the scale of micrometers, while a global model's grid cell may be 100 kilometers wide. The model must have an equation—a parameterization—that determines the grid-cell average effect of these subgrid processes based on grid-cell average [state variables](@entry_id:138790).

Consider the [autoconversion](@entry_id:1121257) rate, $P$, which depends nonlinearly on the subgrid cloud liquid water [mixing ratio](@entry_id:1127970), $q_c$. A common parameterization might take the form $P(q_c) = k q_c^n$ with $n > 1$. Within a grid cell, $q_c$ is not uniform but has a subgrid probability distribution. The true grid-mean tendency is the expectation over this distribution, $\mathbb{E}[P(q_c)]$. However, many models make a homogeneity assumption, calculating the tendency based on the grid-mean state: $P(\bar{q}_c)$, where $\bar{q}_c = \mathbb{E}[q_c]$.

Because the function $P(q_c)$ is convex (its second derivative is positive), **Jensen's inequality** dictates that $\mathbb{E}[P(q_c)] \ge P(\mathbb{E}[q_c]) = P(\bar{q}_c)$. This means the homogeneous-state closure systematically underestimates the true grid-mean autoconversion rate whenever there is any subgrid variability in $q_c$ . Different assumptions about the subgrid probability distribution of $q_c$ (e.g., assuming a uniform, lognormal, or [gamma distribution](@entry_id:138695)) lead to different "scale-aware" parameterizations, each constituting a distinct model structure. The choice among these closure assumptions is a profound source of structural uncertainty in atmospheric, oceanic, and [land surface models](@entry_id:1127054). The problem is compounded when processes depend on multiple, covarying subgrid variables (e.g., both liquid water and droplet number), as the bias then depends on the full joint subgrid distribution.

#### Observational Equivalence and Underdetermination

In some cases, structural uncertainty cannot be resolved even with infinite data, a fundamental problem known as **underdetermination** or **[structural unidentifiability](@entry_id:1132558)**. This occurs when two or more distinct model structures are **observationally equivalent**, meaning they produce identical probability distributions for the observable data.

Consider two different [multi-compartment models](@entry_id:926863), $M_1$ and $M_2$, representing soil carbon dynamics . Each model has an internal state vector $x_t$ evolving according to its own transition matrix $A_i$: $x_{t+1} = A_i x_t + B u_t$. However, we do not observe the full state vector $x_t$. Instead, we observe only a scalar aggregate, such as the total respiration, given by $y_t = c^\top x_t + v_t$, where $v_t$ is measurement noise.

It is possible to construct a scenario where $A_1 \neq A_2$ but their effect on the observable is identical. This happens if the observation operator $c^\top$ is a left eigenvector of both $A_1$ and $A_2$ with the same eigenvalue. In this special case, the dynamics of the observable quantity $y_t$ will be described by the exact same statistical model (an ARMA process) for both $M_1$ and $M_2$. Consequently, the likelihood of any observed data sequence $\{y_t\}$ is identical for both models. No statistical method based on this data, including Bayesian model selection or cross-validation, can ever distinguish between them. The Kullback-Leibler divergence between their [predictive distributions](@entry_id:165741) is zero.

This illustrates a critical limitation: **more data does not resolve structural uncertainty if the observations themselves do not contain the necessary information to distinguish between structures**. The only remedy is to enrich the observation system—for instance, by measuring more components of the internal state, effectively changing the observation operator $c^\top$ to a higher-rank matrix $C$ that can "see" the internal differences between the models.

### Formal Approaches to Quantifying Structural Uncertainty

Given its existence and importance, how do we formally account for structural uncertainty in our analyses? Two major frameworks have emerged: the single-model discrepancy approach and the [multi-model ensemble](@entry_id:1128268) approach.

#### The Model Discrepancy Framework

This framework, pioneered by Kennedy and O'Hagan, acknowledges the fallibility of a single model from the outset. Instead of assuming the model is perfect, it posits that the relationship between reality and the model includes a discrepancy term, $\delta(x)$ . The observation model is written as:

$y(x) = f(x, \theta) + \delta(x) + \epsilon$

Here, $y(x)$ is the observed data, $f(x, \theta)$ is the output of our deterministic computer model with parameters $\theta$, $\epsilon$ is the aleatory observation error, and $\delta(x)$ is the **model discrepancy** or **structural error term**. This term represents the systematic, [state-dependent error](@entry_id:755360) of the model structure itself: $\delta(x) = \eta(x) - f(x, \theta_{true})$, where $\eta(x)$ is the true underlying process and $\theta_{true}$ represents the "true" physical parameters the model aims to capture.

The introduction of $\delta(x)$ is a formal admission of **epistemic uncertainty** (lack of knowledge) about the model's form. If we omit $\delta(x)$ and attempt to calibrate the model $f(x, \theta)$ directly to the data $y(x)$, the statistical procedure will force the parameters $\theta$ to adopt "unphysical" values to compensate for the model's systematic biases. This contaminates the parameters' interpretation and, critically, leads to underestimated predictive uncertainty, as the [systematic error](@entry_id:142393) is mistaken for simple random noise.

In practice, $\delta(x)$ is treated as an unknown function and is often modeled non-parametrically using a **Gaussian Process (GP)** prior. This allows the framework to learn the form of the [systematic error](@entry_id:142393) from the data. The combined "supermodel" $f(x, \theta) + \delta(x)$ can, in principle, represent the true process $\eta(x)$ far more accurately. The posterior predictive uncertainty then correctly decomposes into contributions from observation noise ($\epsilon$), parameter uncertainty ($\theta$), and structural uncertainty (the posterior uncertainty in $\delta(x)$)  . A significant practical challenge, however, is the potential for **confounding** between the parametric model $f(x,\theta)$ and the flexible discrepancy term $\delta(x)$, which can make the parameters $\theta$ difficult to identify without strong prior information.

#### Multi-Model Ensembles and Their Pitfalls

The most common approach in fields like climate science is to work with a collection of different models developed by different research groups. Such a collection, often termed an **ensemble of opportunity**, is a convenience sample rather than a statistically designed experiment . While the spread of predictions from such an ensemble is often used as a proxy for total uncertainty, this practice is fraught with peril.

Models in an ensemble of opportunity are not independent. They often share [common ancestry](@entry_id:176322), including similar numerical schemes, parameterizations inherited from previous model generations, and calibration against the same observational datasets. This interdependence leads to shared errors and biases. We can formalize this by modeling the prediction of model $i$, $Y_i$, as $Y_i = \tau + S + I_i$, where $\tau$ is the true value, $S$ is a shared error component common to all models in the ensemble (with variance $\sigma_S^2$), and $I_i$ is an idiosyncratic error specific to model $i$ (with variance $\sigma_I^2$). The lack of independence is captured by a positive correlation $\rho$ between the idiosyncratic errors $I_i$ and $I_j$ for different models $i \neq j$.

The true structural variance of any single model is $\sigma_S^2 + \sigma_I^2$. However, the expected value of the ensemble [sample variance](@entry_id:164454), $s^2$, can be shown to be:

$\mathbb{E}[s^2] = \sigma_I^2 (1 - \rho)$

This result reveals two critical problems. First, the ensemble spread **completely fails to account for the shared [error variance](@entry_id:636041)** $\sigma_S^2$, because a bias common to all models shifts the entire ensemble together and is cancelled out when computing deviations from the ensemble mean. Second, the **positive correlation between models actively deflates the spread**, reducing the captured portion of the idiosyncratic variance. Both effects cause the naive ensemble spread to be a systematic and often severe underestimate of the true structural uncertainty.

### Bayesian Model Selection and Averaging

A more principled way to handle a [multi-model ensemble](@entry_id:1128268) is through a Bayesian framework, which provides formal rules for comparing models and combining their predictions.

#### The Marginal Likelihood and the Bayesian Occam's Razor

In the Bayesian paradigm, [model selection](@entry_id:155601) is treated as a problem of inference. Given a set of candidate models $\{\mathcal{M}_k\}$ and data $D$, we can calculate the posterior probability of each model using Bayes' theorem:

$p(\mathcal{M}_k \mid D) \propto p(D \mid \mathcal{M}_k) p(\mathcal{M}_k)$

Here, $p(\mathcal{M}_k)$ is the [prior probability](@entry_id:275634) of the model. The crucial term is $p(D \mid \mathcal{M}_k)$, known as the **marginal likelihood** or **model evidence**. It is the probability of having observed the data $D$ given the model structure $\mathcal{M}_k$, and is calculated by integrating over the entire parameter space of that model:

$p(D \mid \mathcal{M}_k) = \int p(D \mid \theta_k, \mathcal{M}_k) p(\theta_k \mid \mathcal{M}_k) \mathrm{d}\theta_k$

where $p(D \mid \theta_k, \mathcal{M}_k)$ is the likelihood and $p(\theta_k \mid \mathcal{M}_k)$ is the parameter prior for model $\mathcal{M}_k$ .

The [marginal likelihood](@entry_id:191889) embodies an automatic **Occam's razor** that penalizes unnecessary complexity . A simple model makes specific, sharp predictions, concentrating its predictive probability over a small range of possible data outcomes. If the observed data fall in this range, the average likelihood will be high. A complex, highly flexible model can fit a much wider range of data, but must spread its predictive probability thinly over all these possibilities. While it might achieve a very high likelihood for a specific, fine-tuned set of parameters, this region of high performance is "diluted" by the vast area of its parameter space where it fits the data poorly. The integral over the entire parameter space averages this out, penalizing the complex model for its wasted flexibility. The [marginal likelihood](@entry_id:191889) naturally favors simpler models that provide an adequate explanation for the data.

#### Bayesian Model Averaging

Rather than selecting a single "best" model, Bayesian principles advocate for accounting for the uncertainty in model choice itself. **Bayesian Model Averaging (BMA)** accomplishes this by creating a composite predictive distribution that is a weighted average of the individual models' [predictive distributions](@entry_id:165741), with the weights being their posterior probabilities:

$p(y^\star \mid D) = \sum_{k=1}^{K} p(y^\star \mid D, \mathcal{M}_k) p(\mathcal{M}_k \mid D)$

Here, $p(y^\star \mid D)$ is the full BMA predictive distribution for a new observation $y^\star$. This composite distribution reflects the uncertainty from all levels: the inherent randomness within each model, the [parametric uncertainty](@entry_id:264387) within each model (integrated out in $p(y^\star \mid D, \mathcal{M}_k)$), and the structural uncertainty across the models (accounted for by the summation) .

#### A Practical Guide to Information Criteria

Calculating the marginal likelihood integral is often computationally prohibitive. In practice, modelers frequently resort to **information criteria**, which provide approximations or alternative measures for [model comparison](@entry_id:266577). Four common criteria are:

-   **Akaike Information Criterion (AIC):** $AIC = -2\ln(\hat{L}) + 2p$, where $\hat{L}$ is the maximum likelihood and $p$ is the number of parameters. AIC aims to select the model that minimizes the expected out-of-sample prediction error (measured by Kullback-Leibler divergence). It is asymptotically justified for large datasets and is particularly useful when the true data-generating process is likely not among the candidate models (i.e., under **misspecification**).

-   **Bayesian Information Criterion (BIC):** $BIC = -2\ln(\hat{L}) + p\ln(n)$, where $n$ is the number of observations. BIC is derived from a large-sample approximation of the log marginal likelihood. Its goal is **consistency**—as the amount of data grows, it will select the true model with probability approaching 1, provided the true model is in the candidate set. Its stronger penalty for complexity (compared to AIC) makes it favor simpler models.

-   **Deviance Information Criterion (DIC):** A hierarchical modeling generalization, DIC is a Bayesian criterion that estimates a model's predictive accuracy while penalizing for an "effective" number of parameters calculated from the posterior distribution. It is heuristic and performs poorly in models with non-Gaussian posteriors or parameter [non-identifiability](@entry_id:1128800).

-   **Widely Applicable Information Criterion (WAIC):** WAIC is a more modern and robustly Bayesian criterion. Like AIC, its goal is to estimate out-of-sample predictive accuracy. Unlike DIC, it is fully Bayesian (averaging over the posterior rather than using a [point estimate](@entry_id:176325)) and is valid for the singular models (e.g., hierarchical or mixture models) where DIC often fails. WAIC is asymptotically equivalent to [leave-one-out cross-validation](@entry_id:633953) .

The choice of criterion depends on the scientific goal: use BIC if you believe a "true" model exists in your set and you wish to identify it; use AIC or WAIC if your goal is purely predictive performance, especially when you assume all models are imperfect approximations.

### The Epistemic Nature of Structural Uncertainty

Finally, it is crucial to synthesize these concepts by returning to the fundamental nature of uncertainty. Structural uncertainty is quintessentially **epistemic**: it represents a lack of knowledge about the true governing equations of a system. In principle, it is reducible. With better theory, better experiments, and more informative observations, we could discover superior model structures, reducing or eliminating the discrepancy $\delta(x)$ and driving the posterior probability of one model $\mathcal{M}_k$ towards unity.

However, in the practice of prediction, this epistemic uncertainty often behaves like **aleatory** (irreducible) uncertainty from the perspective of an end-user . When we construct a BMA forecast or a [multi-model ensemble](@entry_id:1128268) prediction, the spread in the final predictive distribution arises from all sources of uncertainty combined. The formal decomposition of total predictive variance, via the Law of Total Variance, shows that it is the sum of the average within-model variance and the between-model variance. This latter term, which quantifies the contribution of structural uncertainty, simply adds to the total spread. A user receiving this forecast cannot distinguish the portion of the variance due to lack of knowledge about model form from the portion due to inherent system randomness. This dual character—fundamentally epistemic but operationally behaving like a component of [stochasticity](@entry_id:202258)—is a defining feature of [structural uncertainty](@entry_id:1132557) in modern predictive science.