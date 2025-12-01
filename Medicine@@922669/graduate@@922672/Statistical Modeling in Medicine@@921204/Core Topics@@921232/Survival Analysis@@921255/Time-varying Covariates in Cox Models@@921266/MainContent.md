## Introduction
The Cox proportional hazards model is a cornerstone of survival analysis, providing a powerful tool for understanding the relationship between covariates and time-to-event outcomes. While the basic model assumes that patient characteristics are fixed at baseline, clinical and epidemiological reality is far more dynamic. Patient exposures, treatments, and biomarkers often change over time, and these changes carry vital information about risk. The failure to properly account for this dynamic nature can lead to missed insights and, more critically, biased conclusions.

This article addresses the crucial extension of the Cox model to incorporate **time-varying covariates**. It bridges the gap between basic survival analysis and the advanced techniques required for longitudinal data. By navigating this topic, you will gain the skills to model dynamic processes, interpret their effects correctly, and avoid pervasive statistical pitfalls. The following chapters are structured to build your expertise comprehensively. "Principles and Mechanisms" will lay the theoretical groundwork, explaining how the model is specified, estimated, and justified. "Applications and Interdisciplinary Connections" will demonstrate the model's power in real-world scenarios, from clinical research to causal inference. Finally, "Hands-On Practices" will provide practical exercises to solidify your understanding and prepare you to apply these methods in your own work.

## Principles and Mechanisms

The Cox [proportional hazards model](@entry_id:171806) provides a robust and flexible framework for analyzing time-to-event data. While its foundational form assumes covariates are fixed at baseline, its true power in clinical and epidemiological research is most evident in its extension to accommodate **time-varying covariates**. These are variables whose values can change over the course of follow-up for an individual. This chapter elucidates the principles and mechanisms governing the use of time-varying covariates in the Cox model, moving from the fundamental model specification to the advanced and subtle issues of interpretation and causality that arise in practice.

### The Extended Cox Model: Incorporating Dynamic Information

In many longitudinal studies, the risk of an event is not solely determined by baseline characteristics. It evolves in response to dynamic physiological states, environmental exposures, or treatments initiated during follow-up. The extended Cox model directly incorporates such information by allowing the covariate vector to be a function of time.

The [hazard function](@entry_id:177479) for subject $i$ at time $t$, conditional on their covariate history, is specified as:

$$
h_i(t \mid \mathbf{X}_i(t)) = h_0(t) \exp(\boldsymbol{\beta}' \mathbf{X}_i(t))
$$

Here, $h_0(t)$ remains the unspecified baseline hazard function, representing the hazard for an individual with a covariate vector of zero at time $t$. The vector of [regression coefficients](@entry_id:634860), $\boldsymbol{\beta}$, is typically assumed to be constant. The crucial extension is that the covariate vector, $\mathbf{X}_i(t)$, is now a function of time $t$. For instance, if we are studying time to myocardial infarction, $\mathbf{X}_i(t)$ might include a patient's current systolic blood pressure $BP_i(t)$ and an indicator for whether they are currently taking a statin $Z_i(t)$ [@problem_id:4991820]. The model thus uses the most current available information to assess an individual's instantaneous risk.

### The Proportional Hazards Assumption in a Time-Varying Context

A common point of confusion is how the proportional hazards (PH) assumption holds when covariates themselves are changing over time. The "proportionality" in the extended Cox model applies in an **instantaneous sense**.

Consider two individuals, $i$ and $j$. At any single point in time $t$, the ratio of their hazards is:

$$
\frac{h_i(t)}{h_j(t)} = \frac{h_0(t) \exp(\boldsymbol{\beta}' \mathbf{X}_i(t))}{h_0(t) \exp(\boldsymbol{\beta}' \mathbf{X}_j(t))} = \exp(\boldsymbol{\beta}' (\mathbf{X}_i(t) - \mathbf{X}_j(t)))
$$

Notice that the baseline hazard $h_0(t)$ cancels out. The hazard ratio at time $t$ depends only on the difference in the covariate vectors of the two individuals *at that specific instant* $t$ [@problem_id:4991901]. The effect of the covariates, as captured by $\boldsymbol{\beta}$, is assumed to be constant over time. However, because the values of $\mathbf{X}_i(t)$ and $\mathbf{X}_j(t)$ can change, the hazard ratio between individuals $i$ and $j$ may also change over time. For example, if individual $i$ starts a medication at time $t_1$, their hazard ratio relative to an untreated individual $j$ will change at $t_1$. Proportionality is maintained in the sense that the multiplicative separation of the baseline hazard from the covariate-dependent relative risk holds at every moment in time. If two individuals happened to have identical covariate trajectories, such that $\mathbf{X}_i(t) = \mathbf{X}_j(t)$ for all $t$, their hazard ratio would be $\exp(\boldsymbol{\beta}' \mathbf{0}) = 1$ for all time [@problem_id:4991820].

This is distinct from a model with **time-varying effects**, which we will discuss later, where the coefficient $\boldsymbol{\beta}$ itself is a function of time, leading to a violation of the [proportional hazards assumption](@entry_id:163597) [@problem_id:4991895].

### Estimation: The Partial Likelihood with Time-Dependent Covariates

The estimation of $\boldsymbol{\beta}$ proceeds via maximization of the **[partial likelihood](@entry_id:165240)**, a construction that elegantly circumvents the need to estimate the baseline hazard $h_0(t)$. The logic extends directly to the time-varying case.

Let the distinct ordered event times in the study be $t_{(1)}  t_{(2)}  \dots  t_{(J)}$. At each event time $t_{(j)}$, we identify the individual who had the event, denoted by index $i(j)$, and the set of all individuals who were at risk of the event just prior to $t_{(j)}$, known as the **risk set** $\mathcal{R}(t_{(j)})$. The contribution to the partial likelihood at $t_{(j)}$ is the conditional probability that, given one event occurred among the risk set, it was subject $i(j)$ who experienced it.

This probability is the ratio of subject $i(j)$'s hazard to the sum of hazards of everyone in the risk set, all evaluated at time $t_{(j)}$:

$$
L_j(\boldsymbol{\beta}) = \frac{h_{i(j)}(t_{(j)})}{\sum_{k \in \mathcal{R}(t_{(j)})} h_k(t_{(j)})} = \frac{h_0(t_{(j)})\exp(\boldsymbol{\beta}' \mathbf{X}_{i(j)}(t_{(j)}))}{\sum_{k \in \mathcal{R}(t_{(j)})} h_0(t_{(j)})\exp(\boldsymbol{\beta}' \mathbf{X}_k(t_{(j)}))}
$$

As before, the baseline hazard $h_0(t_{(j)})$ cancels. The full [partial likelihood](@entry_id:165240) is the product of these terms across all event times:

$$
L(\boldsymbol{\beta}) = \prod_{j=1}^{J} \frac{\exp(\boldsymbol{\beta}' \mathbf{X}_{i(j)}(t_{(j)}))}{\sum_{k \in \mathcal{R}(t_{(j)})} \exp(\boldsymbol{\beta}' \mathbf{X}_k(t_{(j)}))}
$$

The critical operational detail is that for each event time $t_{(j)}$, the model requires the specific values of the covariate vectors $\mathbf{X}_k(t_{(j)})$ for the subject who failed, $i(j)$, and for *every other subject* $k$ who was in the risk set at that exact moment [@problem_id:4991825]. The partial likelihood compares the risk profile of the person who had the event to the risk profiles of all people who could have had the event at that same time.

### A Rigorous Foundation: The Counting Process Formulation

The modern theoretical justification for the Cox model, particularly with time-varying covariates, is rooted in the theory of [counting processes](@entry_id:260664) and [martingales](@entry_id:267779). This formulation provides a rigorous basis for understanding the model's assumptions and properties.

For each individual $i$, we define several processes:
-   **Counting Process** $N_i(t)$: A process that counts the number of observed events for individual $i$ up to time $t$. For time-to-first-event data, $N_i(t)$ is either 0 or 1.
-   **At-Risk Process** $Y_i(t)$: An indicator process that is $1$ if individual $i$ is at risk of an event at time $t$ (i.e., has not yet had the event and has not been censored) and $0$ otherwise.
-   **Filtration** $\mathcal{F}_t$: The history of all events, censoring, and covariate measurements for all individuals up to time $t$. $\mathcal{F}_{t-}$ denotes the history strictly *prior* to time $t$.

The Cox model is a model for the **intensity process**, $\lambda_i(t)$, of the counting process $N_i(t)$. The intensity is defined such that $\lambda_i(t)dt = \mathbb{E}[dN_i(t) \mid \mathcal{F}_{t-}]$, representing the [conditional probability](@entry_id:151013) of an event in an infinitesimal interval $[t, t+dt)$ given the past history. The intensity is related to the hazard by $\lambda_i(t) = Y_i(t) h_i(t)$. Thus, the model is:

$$
\lambda_i(t) = Y_i(t) h_0(t) \exp(\boldsymbol{\beta}' \mathbf{X}_i(t))
$$

The intensity is zero when the subject is not at risk ($Y_i(t)=0$). The integral of the intensity process, $\Lambda_i(t) = \int_0^t \lambda_i(u)du$, is called the **compensator** [@problem_id:4991892]. The process $M_i(t) = N_i(t) - \Lambda_i(t)$ is a martingale, a property that is fundamental to proving the statistical properties of the partial likelihood estimator.

For this elegant mathematical structure to hold, a crucial condition must be placed on the covariate process $\mathbf{X}_i(t)$: it must be **predictable**. A process is predictable if its value at time $t$ is determined by the information available just before time $t$, i.e., it is measurable with respect to the filtration $\mathcal{F}_{t-}$. In practice, this means that the covariate values used to calculate the risk at an event time $t$ must be based on information gathered strictly before $t$ [@problem_id:4991781] [@problem_id:4991820]. This formalizes the intuitive notion that one cannot use information from the future to predict a present risk. For example, a biomarker measured at the time of a heart attack cannot be used as a time-varying covariate to predict that same heart attack, as its value may be a consequence of the event itself. We must use the value measured just prior to the event.

### Practical Implementation: The Start-Stop Data Format

The [partial likelihood](@entry_id:165240) calculation requires knowing the covariate vector for every at-risk subject at every event time. Most statistical software is not designed to work with covariates as continuous functions of time. The practical solution is to restructure the data into the **counting process** or **start-stop** format.

This involves splitting the follow-up period of each individual into a series of intervals. A new interval begins for an individual whenever their status changes for any of the time-varying covariates. For a subject $i$ with entry time $a_i$, final observation time $T_i$, and covariate change times $\tau_{i1}, \tau_{i2}, \dots$, their record is split at each of these time points.

The result is a dataset where each individual is represented by multiple rows. Each row contains:
1.  A subject ID.
2.  A start time, $t^{\text{start}}$.
3.  A stop time, $t^{\text{stop}}$.
4.  An event status indicator (e.g., 1 if an event occurred at $t^{\text{stop}}$, 0 otherwise).
5.  A vector of covariate values, which are constant throughout the interval $[t^{\text{start}}, t^{\text{stop}})$.

With the data in this format, the software can easily construct the risk set at any event time $t_{(j)}$ by simply finding all rows where $t^{\text{start}} \le t_{(j)}  t^{\text{stop}}$. The constant covariate vector on that row provides the required $\mathbf{X}_k(t_{(j)})$ for the partial likelihood calculation. This segmentation is not an approximation but an exact representation of the piecewise-constant covariate history required by the likelihood formula [@problem_id:4991780].

### Important Distinctions: Covariates, Effects, and Interpretation

Applying the extended Cox model effectively requires understanding several critical distinctions.

#### Time-Varying Covariates versus Time-Varying Effects

As established, a model with a time-varying covariate $X(t)$ and a constant coefficient $\beta$ maintains the [proportional hazards assumption](@entry_id:163597) for the *effect* of that covariate. The model form is $h(t) \propto \exp(\beta X(t))$.

This is fundamentally different from a model with a **time-varying effect** (or coefficient), which is a model for non-proportional hazards. Here, the coefficient associated with a covariate is an explicit function of time, $\beta(t)$. This is often used for baseline covariates, say $Z$, whose influence changes over the follow-up period. A common way to model this is by including an interaction term between the covariate and a function of time, $g(t)$:

$$
h(t \mid Z) = h_0(t) \exp(\beta_1 Z + \beta_2 (Z \times g(t))) = h_0(t) \exp((\beta_1 + \beta_2 g(t)) Z)
$$

The log-hazard ratio for a one-unit increase in $Z$ is now $\beta_1 + \beta_2 g(t)$, which depends on time. For example, if we use $g(t) = \log(t)$, the hazard ratio becomes $\exp(\beta_1 + \beta_2 \log(t)) = \exp(\beta_1) t^{\beta_2}$, which clearly varies with $t$ [@problem_id:4991895]. A non-zero trend in the Schoenfeld residuals for a baseline covariate is a key diagnostic indicating the need for such a model.

#### External versus Internal Covariates

Time-varying covariates can be broadly classified as **external** or **internal**, a distinction with profound implications for interpretation [@problem_id:4991893].

An **external covariate** is a process whose path is not influenced by the individuals under study. Examples include fixed subject characteristics like age, or ambient environmental exposures like daily air pollution levels [@problem_id:4991893] or temperature [@problem_id:4991784]. These can generally be included in a Cox model without major conceptual difficulties, although one must be careful about modeling different time scales (e.g., analysis time vs. calendar time) [@problem_id:4991784].

An **internal covariate** is a process generated by the individual, whose existence requires the subject to be alive and uncensored. Most biomarkers, such as serum lactate, blood pressure, or estimated [glomerular filtration rate](@entry_id:164274) (eGFR), fall into this category [@problem_id:4991784] [@problem_id:4991893]. While the Cox model is mathematically valid for estimating the *association* between an internal covariate and the hazard, causal interpretation of the coefficient is fraught with peril. This is because the covariate's path can be influenced by the same underlying disease process that leads to the event, a phenomenon known as **[reverse causation](@entry_id:265624)** or confounding by indication [@problem_id:4991820]. Furthermore, if the timing of biomarker measurements is not fixed but is driven by a patient's clinical status (e.g., sicker patients are measured more often), this creates an **informative observation process**, which can induce bias in standard analyses [@problem_id:4991784].

### A Critical Pitfall: Immortal Time Bias

One of the most common and serious errors in the analysis of observational data is **immortal time bias**. This bias arises when a time-dependent exposure, such as the initiation of a medication after baseline, is improperly coded as a fixed baseline characteristic.

Consider a study where some patients initiate a new drug at some time $T_i^* > 0$ after study entry. A naive analysis might classify patients into two groups based on whether they *ever* start the drug during follow-up. This is incorrect because, for a patient who starts the drug at $T_i^*$, the time period $[0, T_i^*)$ is "immortal" with respect to that exposure. They must, by definition, survive this period to become exposed. Assigning this person-time to the "exposed" group incorrectly credits the drug with the survival that was a prerequisite for its initiation, which artificially lowers the mortality rate in the exposed group and biases the estimated effect in a favorable direction [@problem_id:4991846].

The correct way to handle such an exposure is to treat it as a time-varying covariate, $X_i(t) = \mathbb{I}(t \ge T_i^*)$. Using the start-stop data format, such a patient would contribute person-time to the unexposed group during $[0, T_i^*)$ and to the exposed group from $T_i^*$ onward. This approach correctly attributes person-time and risk, providing a consistent estimate of the association parameter $\beta$, assuming no other biases like confounding are present [@problem_id:4991846].

### Beyond Association: Time-Dependent Confounding and Causal Inference

The most complex challenge arises in observational studies with **time-dependent confounding**. This occurs when a time-varying covariate, such as a biomarker $L(t)$, is both a predictor of future treatment $X(t)$ and a prognostic factor for the outcome, and is also on the causal pathway from past treatment to the outcome. This creates a feedback loop: treatment affects the confounder, which in turn affects future treatment and the outcome [@problem_id:4991887].

In this scenario, standard regression adjustment fails to provide a valid estimate of the causal effect of treatment.
-   Omitting the confounder $L(t)$ from the model leads to classic [confounding bias](@entry_id:635723).
-   Including the confounder $L(t)$ in a standard Cox model also leads to bias, because conditioning on an intermediate variable on the causal pathway can block part of the treatment's effect and induce other biases.

The coefficient $\beta_X$ from a model $h(t) \propto \exp(\beta_X X(t) + \beta_L L(t))$ does not have a causal interpretation in this setting. However, it is crucial to recognize that the model remains a valid **associational model**. It correctly describes the instantaneous risk conditional on the observed history and can be very useful for risk prediction [@problem_id:4991895].

To estimate the causal effect of a time-varying treatment in the presence of time-dependent confounding, specialized methods are required. These methods aim to estimate the outcome in a hypothetical world where treatment is assigned according to a specific rule. The two major classes of methods for this problem are:
1.  **Marginal Structural Models (MSMs)**: These models use [inverse probability](@entry_id:196307) weighting (IPW) to create a pseudo-population in which the confounders no longer predict treatment assignment, breaking the feedback loop. A weighted Cox model can then be fit to this pseudo-population to estimate the marginal causal effect of treatment.
2.  **Structural Nested Models (SNMs)**: These models directly parameterize the causal effect of treatment at each time point and use a procedure called g-estimation to find the parameter values consistent with the data under an assumption of no unmeasured confounding.

Both approaches rely on strong, untestable assumptions but provide a formal framework for moving beyond association to causal inference with time-varying exposures [@problem_id:4991887]. Understanding when a standard extended Cox model is sufficient and when these more advanced methods are necessary is a hallmark of sophisticated practice in survival analysis.