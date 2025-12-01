## Introduction
Estimating the causal effect of treatments that change over time from observational data is a central task in fields like medicine and public health. Standard statistical methods often fail in this setting due to a complex bias known as time-varying confounding. Marginal Structural Models (MSMs) provide a powerful framework to overcome this challenge and obtain valid causal estimates of treatment strategies from longitudinal data. This article addresses the key problem where a time-varying factor (e.g., a patient's health status) is both influenced by past treatment and influences future treatment, making it both a mediator and a confounder. Adjusting for such a variable in standard regression models leads to biased results.

This article will guide you through the theory and application of MSMs. The **Principles and Mechanisms** chapter will detail the core theory of MSMs, explaining the causal estimand, the [problem of time](@entry_id:202825)-varying confounding, and the mechanics of Inverse Probability of Treatment Weighting (IPTW). Next, the **Applications and Interdisciplinary Connections** chapter will showcase how MSMs are used to answer critical questions in pharmacoepidemiology, [environmental science](@entry_id:187998), and beyond, adapting to complex outcomes like survival data. Finally, the **Hands-On Practices** section will allow you to solidify your understanding of key practical steps, such as calculating weights and diagnosing their performance. By navigating these sections, you will gain a comprehensive understanding of why, how, and when to use Marginal Structural Models to draw robust causal conclusions from complex longitudinal data.

## Principles and Mechanisms

In the analysis of longitudinal data, particularly from observational studies, our objective is often to understand the causal consequences of a sequence of treatments or exposures over time. This chapter delves into the principles and mechanisms of Marginal Structural Models (MSMs), a powerful class of methods designed to estimate the causal effects of time-varying treatments, especially in the presence of confounding that is itself affected by past treatment.

### The Causal Estimand: Marginal Effects of Treatment Histories

To formalize causal questions in a longitudinal setting, we use the [potential outcomes framework](@entry_id:636884). Let us consider a study where individuals are followed over a series of discrete time points $t \in \{0, 1, \dots, T\}$. At each time $t$, a treatment $A_t$ is administered, and a set of covariates $L_t$ are measured. The outcome of interest, $Y$, is measured at the end of the follow-up period. A complete treatment history for an individual is denoted by the vector $\bar{A}_T = (A_0, A_1, \dots, A_T)$.

We define a **potential outcome**, denoted as $Y^{\bar{a}}$, as the outcome that *would have been observed* had an individual, possibly contrary to fact, followed a specific, deterministic treatment history $\bar{a} = (a_0, a_1, \dots, a_T)$ [@problem_id:4581096]. This definition relies on the **Stable Unit Treatment Value Assumption (SUTVA)**, which posits that the potential outcome for one individual is unaffected by the treatment of others (no interference) and that there are no hidden variations of the treatment.

With this framework, we can define our causal estimand. Marginal Structural Models are primarily concerned with the **marginal mean of the potential outcome**, $\mathbb{E}[Y^{\bar{a}}]$ [@problem_id:4581139]. This quantity represents the average outcome we would expect to see in the entire population if every individual had been assigned the treatment regimen $\bar{a}$. It is "marginal" because the expectation is taken over the entire population's distribution of covariates, both baseline and time-varying.

This marginal estimand contrasts with a **conditional estimand**, such as $\mathbb{E}[Y^{\bar{a}} \mid L_0 = \ell_0]$, which represents the average outcome under regimen $\bar{a}$ for the specific subpopulation of individuals who share the same baseline characteristics $L_0 = \ell_0$ [@problem_id:4581096]. While conditional effects are valuable for understanding effect heterogeneity, the marginal effect provides a single, population-level summary that is often the primary interest for public health or policy decisions. These two quantities are related through the law of total expectation:
$$
\mathbb{E}[Y^{\bar{a}}] = \mathbb{E}_{L_0} \left[ \mathbb{E}[Y^{\bar{a}} \mid L_0] \right]
$$
where the outer expectation averages the stratum-specific means over the population distribution of baseline covariates $L_0$.

A Marginal Structural Model (MSM) posits a parametric or [semi-parametric model](@entry_id:634042) directly for this marginal estimand. For example, a simple linear MSM might take the form:
$$
\mathbb{E}[Y^{\bar{a}}] = \beta_0 + \beta_1 \sum_{t=0}^{T} a_t
$$
Here, the parameter $\beta_1$ represents the marginal causal effect of a one-unit increase in the cumulative treatment dose on the final outcome. The challenge, which we address next, is how to estimate parameters like $\beta_0$ and $\beta_1$ using data from an observational study where treatment is not assigned at random.

### The Central Challenge: Time-Varying Confounding

In longitudinal studies, treatment decisions are rarely made in a vacuum. Clinicians often adjust a patient's therapy based on their evolving clinical state. This dynamic gives rise to a particularly challenging form of bias known as **time-varying confounding** or, more specifically, **treatment-confounder feedback**.

Let's consider a common scenario in medicine [@problem_id:4581117]. A patient's current health status, measured by a biomarker $L_t$, influences the doctor's decision to prescribe a treatment $A_t$. This same treatment $A_t$, in turn, affects the patient's future health status, measured by the biomarker at the next visit, $L_{t+1}$. This feedback loop, where $A_{t-1} \to L_t \to A_t$, places the time-varying covariate $L_t$ in a dual causal role:

1.  **$L_t$ as a Confounder**: Because $L_t$ affects both the subsequent treatment $A_t$ and is a predictor of the final outcome $Y$ (i.e., there is a backdoor path $A_t \leftarrow L_t \to Y$), it is a confounder for the effect of $A_t$ on $Y$. Standard epidemiological practice dictates that we must adjust for confounders to obtain an unbiased effect estimate.

2.  **$L_t$ as a Mediator**: Because $L_t$ is affected by past treatment $A_{t-1}$ (i.e., $A_{t-1} \to L_t$) and also affects the outcome $Y$, it lies on a causal pathway from past treatment to the outcome: $A_{t-1} \to L_t \to Y$. The total causal effect of $A_{t-1}$ on $Y$ includes this mediated effect.

This dual role creates a dilemma for standard statistical methods like multivariable regression. If we fit a [regression model](@entry_id:163386) that conditions on the full history of covariates, such as modeling $\mathbb{E}[Y \mid \bar{A}_T, \bar{L}_T]$, we are conditioning on all $L_t$. While this attempts to control for the confounding role of $L_t$, it simultaneously and incorrectly blocks the mediating causal pathway from $A_{t-1}$ through $L_t$ to $Y$. The resulting coefficient for $A_{t-1}$ would represent a *controlled direct effect*, not the *total causal effect* we seek to estimate with our marginal model.

Furthermore, this conditioning can induce a more subtle form of bias known as **collider-stratification bias** [@problem_id:4581149]. Suppose there is an unmeasured factor $U$ (e.g., genetic predisposition, patient adherence) that affects both the biomarker $L_t$ and the outcome $Y$. The causal structure would then include $A_{t-1} \to L_t \leftarrow U \to Y$. In this structure, $L_t$ is a "collider". Conditioning on a collider opens the non-causal path between its parents, creating a spurious association between $A_{t-1}$ and $U$. Since $U$ also affects $Y$, this results in a biased estimate of the effect of $A_{t-1}$.

Therefore, standard regression adjustment fails because one cannot simultaneously adjust for $L_t$ to block confounding and not adjust for it to allow for mediation. Any attempt to do so through simple conditioning leads to bias. MSMs overcome this dilemma by separating the handling of confounding from the modeling of the outcome.

### The Mechanism of Estimation: Inverse Probability of Treatment Weighting

The estimation of Marginal Structural Models is typically accomplished via **Inverse Probability of Treatment Weighting (IPTW)**. The intuition behind IPTW is to create a new, weighted dataset—a pseudo-population—in which the link between the time-varying confounders and treatment assignment is broken. In this pseudo-population, treatment assignment at each time point is independent of the measured past confounder history, mimicking the conditions of a sequential randomized trial.

The core idea of IPTW can be understood as a form of **importance sampling** [@problem_id:4581076]. We have data from an "observed" probability distribution, where treatment depends on covariates. We want to estimate an expectation in a "target" hypothetical distribution, where treatment is independent of those covariates. Importance sampling tells us we can estimate the target expectation by taking a weighted average of our observed data. The weight for each individual is the ratio of the probability of their observed treatment history under the [target distribution](@entry_id:634522) to the probability under the observed distribution.

For an MSM, the weight for an individual $i$ is constructed as the inverse of the [conditional probability](@entry_id:151013) of receiving the treatment history they actually received, given their measured time-varying covariate history. The **unstabilized weight** is defined as:
$$
W_i^{(u)} = \prod_{t=0}^{T} \frac{1}{P(A_{it}=a_{it} \mid \bar{A}_{i,t-1}=\bar{a}_{i,t-1}, \bar{L}_{it}=\bar{\ell}_{it})}
$$
where the denominator is the [conditional probability](@entry_id:151013) of receiving the observed treatment $a_{it}$ at time $t$, given the observed past treatment and covariate histories. These conditional probabilities are often called **propensity scores**. In practice, they are unknown and must be estimated from the data, typically by fitting a pooled [logistic regression model](@entry_id:637047) for treatment at each time point as a function of past covariates and treatment.

Once these weights are calculated for each subject, the parameters $\beta$ of the marginal model $\mathbb{E}[Y^{\bar{a}}] = m(\bar{a}; \beta)$ are estimated by fitting a weighted regression model of the observed outcome $Y$ on the observed treatment history $\bar{A}$, using the weights $W_i$. Because the weighting creates a pseudo-population where there is no confounding by the measured covariates $\bar{L}$, we can fit a marginal model that correctly excludes $\bar{L}_t$ from the regressors, thereby avoiding the biases of standard adjustment methods.

### Foundational Theory: The Identification of Causal Effects

The validity of the IPTW procedure rests on three key **identification assumptions** that connect the unobservable potential outcomes to the observed data. These assumptions, when met, guarantee that we can consistently estimate the parameters of our causal model [@problem_id:4581156].

1.  **Consistency**: For any individual, if their observed treatment history is $\bar{A}$, then their observed outcome $Y$ is equal to their potential outcome under that history, $Y^{\bar{A}}$. This assumption links the potential outcomes world to the real world we observe. It is a statement that the interventions are well-defined.

2.  **Sequential Exchangeability (or No Unmeasured Confounding)**: At every time point $t$, the treatment assigned, $A_t$, is independent of the set of all potential outcomes $\{Y^{\bar{a}}\}$ conditional on the observed past treatment and covariate history $(\bar{A}_{t-1}, \bar{L}_t)$. Formally, $Y^{\bar{a}} \perp A_t \mid \bar{A}_{t-1}, \bar{L}_t$ for all $t$ and all regimens $\bar{a}$. This is the crucial assumption that we have measured and adjusted for all relevant common causes of treatment and outcome at each point in time. It is untestable and its plausibility must be argued from subject-matter knowledge.

3.  **Positivity**: For any combination of past treatment and covariate history that occurs in the population, the probability of receiving any given treatment level at time $t$ is greater than zero. That is, $P(A_t = a_t \mid \bar{A}_{t-1}, \bar{L}_t) > 0$ for all $t$ and all treatment levels $a_t$. This ensures that for every type of subject, there is at least a possibility of them receiving any of the treatments of interest. If this were not true (e.g., if patients with a certain biomarker value are *never* given a particular drug), it would be impossible to estimate the causal effect of that drug for that subgroup from the data.

Under these three assumptions, it can be formally shown that the marginal mean potential outcome is identified by an expression involving the observed data and the propensity scores. The **g-formula identification theorem** for IPTW states:
$$
\mathbb{E}[Y^{\bar{a}}] = \mathbb{E}\left[ Y \cdot \frac{I(\bar{A} = \bar{a})}{P(\bar{A}=\bar{a} \mid \bar{L})} \right]
$$
where $I(\cdot)$ is the indicator function, and the denominator is the conditional probability of the entire treatment regimen $\bar{a}$ given the entire covariate history $\bar{L}$, which can be factorized as the product of the time-specific propensity scores. The sample analogue of this expression is the IPTW estimator, which averages the weighted outcomes for all subjects who followed the regimen $\bar{a}$. This provides the rigorous justification for using IPTW to estimate the parameters of an MSM.

### Practical Refinements and Challenges

#### Stabilized Weights

While the unstabilized weights $W^{(u)}$ provide a [consistent estimator](@entry_id:266642), they can have high variance, especially if some of the [propensity score](@entry_id:635864) denominators are very small. This leads to a few individuals having extremely large weights, making the final estimate unstable. To mitigate this, **stabilized weights** are almost always used in practice [@problem_id:4971112].

A stabilized weight, $W^{(s)}$, is defined as:
$$
W_i^{(s)} = \prod_{t=0}^{T} \frac{P(A_{it}=a_{it} \mid \bar{A}_{i,t-1}=\bar{a}_{i,t-1}, V_i)}{P(A_{it}=a_{it} \mid \bar{A}_{i,t-1}=\bar{a}_{i,t-1}, \bar{L}_{it}=\bar{\ell}_{it})}
$$
where the numerator models the probability of treatment conditional on a reduced set of covariates $V_i$ that are not affected by prior treatment (e.g., baseline covariates only). The denominator remains the same.

Under correct model specification, estimators based on both $W^{(u)}$ and $W^{(s)}$ are consistent for the same causal parameter $\beta$ [@problem_id:4971112]. The purpose of the numerator is to reduce the variability of the weights. Because the numerator term is a probability (between 0 and 1) and is typically "smoother" (less variable) than the denominator, the stabilized weights tend to be smaller and less variable than unstabilized weights. This leads to more precise and stable causal effect estimates. Furthermore, it can be shown that if the denominator model is correctly specified, the estimator remains consistent even if the numerator model is misspecified, although efficiency may be lost [@problem_id:4971112]. The key effect of the stabilized weights is to create a pseudo-population where treatment is independent of the time-varying confounders *conditional on the variables in the numerator* [@problem_id:4971096]. It can also be shown that under correct specification, the expectation of the stabilized weights in the population is one, a useful diagnostic property.

#### Near-Positivity Violations

The practical utility of IPTW is highly dependent on the positivity assumption. In real-world data, we often encounter **near-positivity violations**, where for certain covariate strata, the probability of receiving a specific treatment is not zero, but is extremely small [@problem_id:4581157]. For example, in a precision oncology study, a patient with a specific genomic biomarker $l^{\star}$ might have a very low, but non-zero, probability of receiving a targeted therapy, say $P(A_t=1 | L_t=l^{\star}) \approx 0.01$.

If a patient in this stratum is, by chance, observed to receive the therapy, their IPTW weight will contain a term that is the inverse of this small probability (e.g., $1/0.01 = 100$). Because the total weight is a product over time, a few such instances can cause an individual's weight to become astronomically large, leading to unstable and high-variance estimates.

Stabilization helps by dampening these extremes. The stabilized weight would have a numerator that is the [marginal probability](@entry_id:201078) of treatment, which is much larger than $0.01$. The resulting ratio would be smaller (e.g., $0.4/0.01 = 40$). However, this is still a large weight. Thus, stabilization *reduces* the problem of extreme weights but does not *eliminate* it [@problem_id:4581157]. In practice, analysts often resort to additional techniques such as weight truncation or trimming to manage the influence of these extreme weights, though these methods can introduce their own bias.

### Advanced Topic: Doubly Robust Estimation

A key limitation of standard IPTW is its reliance on the correct specification of the treatment assignment model (the [propensity score](@entry_id:635864)). If this model is misspecified, the resulting causal effect estimate will be biased. An alternative approach, g-computation, relies on correctly specified outcome regression models. **Augmented Inverse Probability Weighting (AIPW)** estimators combine features of both methods to achieve a desirable property called **double robustness** [@problem_id:4971183].

An AIPW estimator for the parameters of an MSM is consistent if *either* the model for the treatment assignment mechanism is correctly specified, *or* a series of models for the outcome regression is correctly specified. One does not need both to be correct. This "doubly robust" property provides two opportunities to obtain a valid estimate.

The AIPW estimator augments the standard IPW estimating equation with a term that is constructed to have an expectation of zero if the outcome model is correct. The structure of this augmentation ensures that if the treatment model is wrong but the outcome model is right, the bias from the misspecified weights is cancelled out. Conversely, if the outcome model is wrong but the treatment model is right, the augmentation term has an expectation of zero, and the estimator effectively reduces to the standard IPW estimator, which is consistent.

This property is particularly valuable in high-dimensional settings where correct specification of any single model is challenging. To be clear, double robustness in a longitudinal setting requires that the *entire sequence* of treatment models is correct, or the *entire sequence* of outcome regression models is correct. It is not sufficient for "mixing and matching" correctly specified models at different time points [@problem_id:4971183]. If both sets of models are correctly specified, the AIPW estimator has the additional benefit of being semiparametrically efficient, meaning it achieves the lowest possible variance among a large class of similar estimators.