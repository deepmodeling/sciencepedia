## Introduction
As the demand for high-performance and reliable batteries grows, moving beyond deterministic models to account for real-world variability has become essential. Single-point predictions from traditional models can be misleading, as they fail to capture uncertainties arising from manufacturing tolerances, operational variations, and the inherent approximations in the models themselves. This gap between idealized models and physical reality undermines our ability to guarantee [battery safety](@entry_id:160758), predict lifetime accurately, and optimize performance. This article provides a comprehensive guide to Uncertainty Quantification (UQ), a rigorous framework for managing this challenge. In the following chapters, you will learn the fundamental concepts underpinning UQ, starting with the principles and mechanisms for classifying and propagating uncertainty. We will then explore the broad applications of these techniques in robust design, real-time control, and lifetime prediction, highlighting interdisciplinary connections. Finally, a series of hands-on practices will allow you to implement key UQ methods yourself. We begin by establishing a systematic methodology for characterizing, propagating, and analyzing the uncertainties that define modern [battery modeling](@entry_id:746700).

## Principles and Mechanisms

Having established the importance of uncertainty quantification (UQ) in the design and operation of battery systems, this chapter delves into the fundamental principles and mechanisms that govern the practice. We will move from a qualitative understanding of uncertainty to a rigorous, quantitative framework. Our objective is to build a systematic methodology for characterizing, propagating, and analyzing the various uncertainties that arise in [physics-based battery models](@entry_id:1129654). We will explore the mathematical tools that allow us to make probabilistic statements about model predictions, assess the relative importance of different uncertain parameters, and address the challenges posed by computationally expensive simulations and imperfect model physics.

### A Taxonomy of Uncertainty in Battery Models

The first step in any rigorous UQ endeavor is to identify and classify the sources of uncertainty. A deterministic model, such as the Doyle-Fuller-Newman (DFN) model, provides a single output for a given set of inputs. However, in reality, both the model and the physical system it represents are subject to various forms of uncertainty. We can categorize these into five primary classes, using the DFN model as a concrete example.

1.  **Parameter Uncertainty**: This refers to the lack of exact knowledge of the physical, chemical, and geometric constants required by the model. For a DFN model, this includes parameters like the [solid-phase diffusion](@entry_id:1131915) coefficient ($D_s$), the interfacial reaction rate constant ($k_0$), electrode porosity ($\epsilon$), and [specific surface area](@entry_id:158570) ($a_s$). This uncertainty arises from limitations in characterization experiments and inherent variability from manufacturing tolerances.

2.  **Model-Form Uncertainty**: Also known as structural uncertainty, this arises because any mathematical model is an idealized approximation of reality. The DFN model, despite its fidelity, typically neglects phenomena such as thermal effects, mechanical stress, and degradation mechanisms like Solid Electrolyte Interphase (SEI) growth. An even simpler Equivalent Circuit Model (ECM) possesses greater [model-form uncertainty](@entry_id:752061), as it omits the spatially distributed physics of diffusion and reaction kinetics that the DFN model captures.

3.  **Numerical Uncertainty**: This is the error introduced by solving the continuous mathematical equations of the model (e.g., partial differential equations) using numerical methods on a computer. It includes [truncation errors](@entry_id:1133459) from discretizing space and time, and convergence errors from [iterative solvers](@entry_id:136910). This uncertainty is a feature of the simulation tool, not the physical battery.

4.  **Initial-Condition Uncertainty**: This refers to the lack of precise knowledge of the battery's state at the beginning of a simulation or experiment ($t=0$). This includes the [spatial distribution](@entry_id:188271) of lithium concentration in the electrodes, $c_s(r, 0)$, or the salt concentration in the electrolyte.

5.  **Measurement Uncertainty**: This is the error associated with the experimental data used for model calibration or validation. It includes random noise from sensors and potential [systematic errors](@entry_id:755765) or biases due to miscalibration. In a measurement model like $y(t) = V_{\text{model}}(t) + \eta_m(t)$, this is represented by the error term $\eta_m(t)$.

A deeper distinction, crucial for the proper treatment of these uncertainties, is between **aleatory** and **epistemic** uncertainty.

-   **Aleatory uncertainty** is the inherent, irreducible randomness or variability in a system. It is a property of the system itself.
-   **Epistemic uncertainty** stems from a lack of knowledge. In principle, it is reducible by gathering more data or improving our models.

The classification of the five uncertainty types can sometimes depend on the context of the study. In typical practice for battery design studies:

-   **Parameter, model-form, and numerical uncertainties** are fundamentally **epistemic**. We could, in principle, reduce our uncertainty in a parameter's value with more experiments, build a more complete model to reduce structural error, or use a finer mesh to reduce numerical error.
-   **Initial-condition and measurement uncertainties** are often treated as **aleatory**. While the initial state of a single cell is a fixed (but unknown) quantity and thus its uncertainty is epistemic, the variability in initial states across a population of cells or over repeated cycles is practically irreducible and best modeled as a random variable. Similarly, the high-frequency, random component of sensor noise is treated as aleatory.

The choice of treating an uncertainty as aleatory or epistemic is a critical modeling decision. Consider the manufacturing variability in electrode porosity, $\epsilon$. If we are analyzing a large population of cells from a stable, well-characterized manufacturing process, we might treat the [cell-to-cell variability](@entry_id:261841) in $\epsilon$ as purely **aleatory**, represented by a single probability distribution. This assumes the cells are **exchangeable** and the process is **stationary**. However, if we have data from only a few batches, or if there is evidence of lot-to-lot drift, our lack of knowledge about the specific parameters of the distribution for each batch introduces a significant **epistemic** component. In this case, a hierarchical model would be needed to capture both the aleatory variability within a batch and the epistemic uncertainty about the batch-level properties.

### The Probabilistic Framework for Uncertainty Propagation

To quantify the impact of these uncertainties, we must represent them mathematically and propagate them through the battery model. This process, known as **[forward uncertainty propagation](@entry_id:1125265)**, involves treating the model inputs as random variables and analyzing the resulting distribution of the model output.

#### Representing Input Uncertainty: Prior Distributions
The uncertainty in model parameters is formally represented by **[prior probability](@entry_id:275634) distributions**. The choice of these distributions should be guided by physical principles and any available domain knowledge.

-   For strictly positive parameters that may span several orders of magnitude, such as the diffusion coefficient $D_s$ or the [reaction rate constant](@entry_id:156163) $k$, the **Log-normal distribution** is appropriate. A standard Normal (Gaussian) distribution is physically inadmissible because its support includes negative values. The Log-normal distribution, with support on $(0, \infty)$, naturally models multiplicative variability and is defined on a scale where orders of magnitude are represented linearly.

-   For parameters that represent fractions or proportions and are thus bounded on the interval $(0, 1)$, such as porosity $\epsilon$, the **Beta distribution** is the natural choice. Its support is inherently $(0, 1)$, and by adjusting its [shape parameters](@entry_id:270600) ($\alpha, \beta$), it can represent a wide range of beliefs about the parameter's distribution, from uniform to highly peaked. For example, a prior for porosity $\epsilon \sim \operatorname{Beta}(14, 26)$ correctly reflects expert knowledge that the value typically lies between $0.2$ and $0.5$ with a mean of $0.35$.

#### Connecting Model to Data: The Likelihood Function
The link between the deterministic model output and noisy experimental data is the **[likelihood function](@entry_id:141927)**. It quantifies how probable the observed data are for a given set of model parameters. Assuming the measurement errors $\varepsilon_t$ are [independent and identically distributed](@entry_id:169067) (i.i.d.) from a zero-mean Gaussian distribution with variance $\sigma^2$, the measurement model is $y_t = V_t(\boldsymbol{\theta}) + \varepsilon_t$, where $V_t(\boldsymbol{\theta})$ is the model's voltage prediction at time $t$ for parameters $\boldsymbol{\theta}$.

The probability density of observing a single data point $y_t$ is given by the Gaussian PDF:
$$
p(y_t | \boldsymbol{\theta}, \sigma^2) = \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(y_t - V_t(\boldsymbol{\theta}))^2}{2\sigma^2} \right)
$$
Due to the independence assumption, the [joint likelihood](@entry_id:750952) for the entire time series of measurements $\mathbf{y} = (y_1, \dots, y_T)$ is the product of the individual densities:
$$
p(\mathbf{y} | \boldsymbol{\theta}, \sigma^2) = \prod_{t=1}^{T} p(y_t | \boldsymbol{\theta}, \sigma^2) = (2\pi\sigma^2)^{-\frac{T}{2}} \exp\left( -\frac{1}{2\sigma^2} \sum_{t=1}^{T} (y_t - V_t(\boldsymbol{\theta}))^2 \right)
$$
This function is the cornerstone of both frequentist (e.g., maximum likelihood estimation) and Bayesian inference. However, its validity rests on the strong assumptions of **independence** and **homoscedasticity** (constant variance) of the errors. These assumptions may be violated in practice. For instance, if the model fails to capture slow dynamics, the residuals $y_t - V_t(\boldsymbol{\theta})$ will be temporally correlated, violating independence. If the measurement noise or model discrepancy is larger at certain states of charge, the error variance will not be constant, violating homoscedasticity. Careful [residual analysis](@entry_id:191495) is required to validate these assumptions.

### Analyzing Parametric Uncertainty: Sensitivity Analysis

With a probabilistic framework in place, we can ask: which uncertain parameters have the greatest influence on the model's output variability? Sensitivity analysis provides the tools to answer this question.

#### Global Sensitivity Analysis (GSA)

GSA evaluates the influence of parameters across their entire range of uncertainty. Variance-based methods, such as Sobol's method, are particularly powerful as they can capture nonlinear and interactive effects.