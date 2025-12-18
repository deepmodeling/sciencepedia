## Introduction
Mathematical models are indispensable tools in science and engineering, but their predictive power hinges on the reliability of their parameters. Simply fitting a model to data is not enough; we must ask a more fundamental question: can the parameters be uniquely and precisely determined from the available measurements? This is the central challenge of **[identifiability analysis](@entry_id:182774)**, a critical step that validates the relationship between a model, an experiment, and the parameters we seek to uncover. Without it, we risk building models on shaky foundations, leading to flawed conclusions and unreliable designs.

This article provides a comprehensive guide to understanding and applying [identifiability analysis](@entry_id:182774). The first chapter, **Principles and Mechanisms**, establishes the theoretical groundwork, distinguishing between ideal structural identifiability and data-driven [practical identifiability](@entry_id:190721). The second chapter, **Applications and Interdisciplinary Connections**, explores how these principles are used to guide optimal experimental design, inform model selection, and solve real-world problems in fields ranging from battery engineering to pharmacology. Finally, the **Hands-On Practices** chapter provides concrete computational exercises to solidify your understanding of these essential techniques. By navigating these concepts, you will gain the skills to build more robust, reliable, and insightful models.

## Principles and Mechanisms

The process of calibrating a battery model involves inferring the values of its parameters from experimental data. A fundamental question precedes any attempt at estimation: can the parameters be uniquely determined from the available measurements? This question lies at the heart of **[identifiability analysis](@entry_id:182774)**, a critical discipline that assesses the relationship between a model's structure, the experimental design, and the uniqueness of its parameters. This chapter establishes the principles of [parameter identifiability](@entry_id:197485), distinguishes between its various forms, and explores the mechanisms through which [identifiability](@entry_id:194150) issues manifest and can be mitigated in the context of electrochemical battery models.

### Structural Identifiability: The Theoretical Ideal

The first and most fundamental concept is **structural identifiability**. This is a purely theoretical property of the model equations themselves, considered under idealized conditions: perfect, noise-free, continuous-time measurements, and sufficiently informative experimental inputs. Structural identifiability addresses whether it is theoretically possible to uniquely determine the parameter vector, $\theta$, from the model's input-output behavior.

Mathematically, if we define the parameter-to-output map $\mathcal{H}_u(\theta)$ as the noise-free model output trajectory $y(t; \theta, u)$ for a given input $u(t)$, a parameter vector $\theta$ is structurally identifiable if this map is injective. That is, for any two distinct parameter vectors $\theta_1$ and $\theta_2$ in the admissible parameter space, their corresponding outputs must also be distinct.

We distinguish between two levels of structural identifiability :
- **Global [structural identifiability](@entry_id:182904)**: The map $\mathcal{H}_u$ is injective over the entire parameter space. If $\mathcal{H}_u(\theta_1) = \mathcal{H}_u(\theta_2)$, it must imply that $\theta_1 = \theta_2$. This is the strongest form of identifiability.
- **Local structural identifiability**: The map $\mathcal{H}_u$ is injective only within a local neighborhood of a given parameter vector $\theta^*$. This means that in the vicinity of $\theta^*$, no other parameter vector produces the identical output. It allows for the possibility that a finite number of distinct, distant parameter vectors could yield the same output. For instance, if a model's output depends on a parameter $\beta$ only through its square, $\beta^2$, then the parameter values $\beta^*$ and $-\beta^*$ would produce identical outputs. In this case, $\beta$ would be locally, but not globally, structurally identifiable .

Structural [non-identifiability](@entry_id:1128800) is an intrinsic flaw in the model formulation relative to the chosen outputs. It typically arises from symmetries or algebraic redundancies in the model equations. For example, consider a two-time-constant equivalent circuit model (ECM) where a manufacturing [constraint forces](@entry_id:170257) the two RC time constants to be equal: $\tau = R_1 C_1 = R_2 C_2$. The system's dynamic impedance, which would normally be a second-order function of the Laplace variable $s$, collapses into a [first-order system](@entry_id:274311):
$$
Z(s) = R_s + \frac{R_1}{\tau s + 1} + \frac{R_2}{\tau s + 1} = R_s + \frac{R_1 + R_2}{\tau s + 1}
$$
From input-output data, one can only identify the sum of the polarization resistances, $R_p = R_1 + R_2$, but not the individual values of $R_1$ and $R_2$. The model is structurally non-identifiable for these individual parameters because of the algebraic constraint that makes their dynamic signatures indistinguishable .

Another common source of [structural non-identifiability](@entry_id:263509) is [scaling symmetry](@entry_id:162020). Consider a simple model for terminal voltage $V(t) = U(z(t))$ where the [open-circuit voltage](@entry_id:270130) (OCV) is a linear function of state-of-charge (SoC), $U(z) = a + bz$, and SoC evolves as $\dot{z} = -I(t)/Q$. The full output equation becomes:
$$
V(t) = a + b \left(z(0) - \frac{1}{Q} \int_0^t I(\tau)d\tau\right) = \left(a + bz(0)\right) - \frac{b}{Q} \int_0^t I(\tau)d\tau
$$
Even with perfect measurements, we can only ever identify the lumped constant term $(a + bz(0))$ and the ratio $b/Q$. The individual parameters $b$ and $Q$ (and $a$ and $z(0)$) are structurally non-identifiable. This is due to a [scaling symmetry](@entry_id:162020): a transformation such as $(b, Q) \to (b/\gamma, Q/\gamma)$ leaves the identifiable ratio $b/Q$ invariant  . This problem is particularly acute when calibrating models over a narrow SoC window where the OCV curve is nearly linear .

It is critical to distinguish structural parameter identifiability from **state observability**. Observability is the property that the internal states of the system (e.g., SoC, polarization voltages) can be uniquely determined from the outputs, for a *fixed* and known parameter vector. A system can be fully state-observable, yet its parameters may be structurally non-identifiable due to the kind of symmetries described above .

### Practical Identifiability and Sensitivity Analysis

While [structural identifiability](@entry_id:182904) provides a theoretical foundation, it operates in an idealized world. **Practical [identifiability](@entry_id:194150)** addresses the more pertinent question: can parameters be estimated with acceptable precision from a real-world experiment, which involves a finite amount of discrete, noisy data? . A parameter may be structurally identifiable, but if the model's output is extremely insensitive to changes in that parameter, the effect will be swamped by measurement noise, rendering it impossible to estimate accurately.

The core tool for assessing [practical identifiability](@entry_id:190721) is **sensitivity analysis**. The sensitivity of the model output $y(t; \theta)$ with respect to a parameter $\theta_j$ is the partial derivative $\frac{\partial y(t; \theta)}{\partial \theta_j}$. This function quantifies how much the output changes for an infinitesimal change in the parameter. If this sensitivity is zero or very small across the entire experiment, the data contain little to no information about that parameter.

A clear example can be constructed using a Thevenin model. The parameters $R_1$ and $C_1$ of an RC circuit are structurally identifiable. However, if an experiment is conducted with a low-amplitude current input, the resulting voltage variation across the RC element can be smaller than the sensor's noise level. For example, if the RC-induced voltage amplitude is $0.35\,\mathrm{mV}$ while the measurement noise standard deviation is $1\,\mathrm{mV}$, the signal containing information about $R_1$ and $C_1$ is effectively "buried" in the noise. Consequently, while structurally sound, these parameters become practically non-identifiable for this specific experimental design .

### The Fisher Information Matrix: A Quantitative Framework

Sensitivity analysis is formalized through the **Fisher Information Matrix (FIM)**, denoted $\mathcal{I}(\theta)$. The FIM quantifies the amount of information that the experimental data provide about the unknown parameter vector $\theta$. For a common measurement model with [independent and identically distributed](@entry_id:169067) (i.i.d.) Gaussian noise with variance $\sigma^2$, the FIM can be derived from the log-likelihood function of the data. The derivation shows that the FIM is directly related to the output sensitivities . For a set of $N$ measurements at times $t_k$, the FIM is given by:

$$
\mathcal{I}(\theta) = \frac{1}{\sigma^2} \sum_{k=1}^{N} \left( \frac{\partial y(t_k; \theta, u)}{\partial \theta} \right) \left( \frac{\partial y(t_k; \theta, u)}{\partial \theta} \right)^\top
$$

where $\frac{\partial y(t_k; \theta, u)}{\partial \theta}$ is the column vector of output sensitivities with respect to each parameter in $\theta$ at time $t_k$. This expression shows that the FIM is a sum of outer products of the sensitivity vectors, scaled by the inverse noise variance.

The FIM is central to identifiability for two reasons:
1.  A singular FIM (i.e., one that is not invertible) indicates that at least one parameter or a combination of parameters is practically non-identifiable. This occurs if the sensitivity vectors are linearly dependent over the course of the experiment.
2.  The inverse of the FIM provides the **Cramér-Rao Lower Bound (CRLB)**, which sets a theoretical minimum on the variance of any [unbiased estimator](@entry_id:166722) for the parameters. A "large" FIM implies that precise estimates (small variance) are possible.

### Parameter Correlation, Sloppiness, and Experimental Design

The inverse of the FIM, which approximates the covariance matrix of the estimated parameters, $\mathbf{\Sigma} \approx \mathcal{I}(\theta)^{-1}$, reveals not only the uncertainty in each parameter (the diagonal elements $\mathbf{\Sigma}_{ii}$) but also the **[parameter correlation](@entry_id:274177)** (the off-diagonal elements $\mathbf{\Sigma}_{ij}$). The **correlation coefficient** between two parameter estimates, $\hat{\theta}_i$ and $\hat{\theta}_j$, is defined as:

$$
\rho_{ij} = \frac{\mathbf{\Sigma}_{ij}}{\sqrt{\mathbf{\Sigma}_{ii}\mathbf{\Sigma}_{jj}}}
$$

A value of $|\rho_{ij}|$ close to $1$ indicates a strong linear relationship between the estimation errors of the two parameters. This high correlation is a direct consequence of the sensitivity vectors for $\theta_i$ and $\theta_j$ being nearly collinear. Geometrically, this means the cost function surface (e.g., sum-of-squared-errors) has a long, narrow "valley" or canyon, and the resulting confidence region for the parameters is a highly elongated ellipsoid. The estimator can determine the combination of parameters that defines the narrow direction of the valley, but it struggles to locate the parameters along the flat, elongated direction .

This phenomenon is common in complex [battery models](@entry_id:1121428):
- In an SPM, the [solid-phase diffusion](@entry_id:1131915) coefficient $D_s$ and the particle radius $R_s$ are often highly correlated because the diffusion dynamics are primarily governed by the characteristic time constant $\tau_s = R_s^2/D_s$. The output is sensitive to this ratio, but much less sensitive to $D_s$ and $R_s$ individually, leading to high correlation along contours where $R_s^2/D_s$ is constant  .
- When calibrating an OCV model over a narrow SoC window, the parameters for the intercept ($a$), slope ($b$), and capacity ($Q$) can become highly correlated as the window shrinks, reflecting the increasing difficulty of distinguishing a constant offset from a shallow slope and a scaled time axis .

In many high-dimensional models, a more general phenomenon known as **sloppiness** occurs. A [sloppy model](@entry_id:1131759) is one where the FIM is technically invertible but severely ill-conditioned, meaning its eigenvalues span many orders of magnitude. A few large eigenvalues correspond to "stiff" parameter combinations that are well-constrained by the data. Many small eigenvalues correspond to "sloppy" combinations that are only weakly constrained, leading to enormous estimation uncertainty in those directions . The **Singular Value Decomposition (SVD)** of the [sensitivity matrix](@entry_id:1131475) $S$ is a powerful tool for diagnosing sloppiness; small singular values directly correspond to these weakly identifiable, sloppy parameter combinations .

Crucially, practical identifiability, correlation, and sloppiness are not just properties of the model, but properties of the *entire experiment*. A poor experimental design will yield poor [identifiability](@entry_id:194150).
- If the input current provides no excitation (e.g., $I(t)=0$), the sensitivity to most dynamic parameters will be zero, making them unidentifiable .
- If the experiment is conducted entirely on an OCV plateau (where $d\text{OCV}/d\text{SoC} \approx 0$), the model output loses its sensitivity to capacity $Q$, making it practically unidentifiable .

Conversely, identifiability can be improved by designing better experiments. The goal of **Optimal Experimental Design (OED)** is to choose an input profile $u(t)$ that maximizes the information content, typically by maximizing some scalar measure of the FIM (e.g., its determinant). Using broadband input signals like pseudo-random binary sequences (PRBS) or multi-sine waves excites the system dynamics across various timescales. This helps to make the sensitivity vectors for different parameters more orthogonal, reducing correlations and improving the conditioning of the FIM . Furthermore, augmenting standard pulse tests with other measurement techniques, such as Electrochemical Impedance Spectroscopy (EIS), can provide complementary information that helps to decouple parameters whose effects are similar in the time domain, thereby reducing sloppiness .

In conclusion, [identifiability analysis](@entry_id:182774) forms a conceptual hierarchy from the theoretical ideal of structural identifiability to the quantitative, data-dependent realities of practical identifiability, correlation, and [sloppiness](@entry_id:195822). It is an indispensable tool in the battery modeling workflow, providing the theoretical basis for selecting appropriate [model complexity](@entry_id:145563) and for designing experiments that yield data rich enough to calibrate those models with confidence.