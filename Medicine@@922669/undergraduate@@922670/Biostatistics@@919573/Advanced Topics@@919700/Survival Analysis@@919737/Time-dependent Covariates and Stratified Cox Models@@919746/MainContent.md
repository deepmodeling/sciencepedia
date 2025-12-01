## Introduction
The Cox [proportional hazards model](@entry_id:171806) is a cornerstone of survival analysis, offering a flexible method for examining the relationship between predictors and time-to-event outcomes. However, its standard form relies on two critical assumptions that are often violated in real-world research: that all covariates are fixed over time and that their effects on the hazard are constant. These limitations can lead to inaccurate conclusions when analyzing dynamic processes, such as changing clinical states or accumulating environmental exposures.

This article provides a comprehensive guide to two powerful extensions that overcome these challenges: time-dependent covariates and the stratified Cox model. By incorporating these advanced techniques, researchers can build models that more accurately reflect the complexities of longitudinal data.

Throughout this guide, you will gain a robust understanding of these methods across three focused chapters. The first chapter, **Principles and Mechanisms**, will break down the theoretical foundations, explaining how to incorporate time-varying predictors and how stratification resolves non-proportionality. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the practical use of these models in biostatistics, epidemiology, and even fields like evolutionary biology, highlighting their versatility in solving real scientific problems. Finally, the **Hands-On Practices** section will provide targeted exercises to solidify your ability to implement and interpret these advanced models, bridging the gap between theory and application.

## Principles and Mechanisms

The standard Cox [proportional hazards model](@entry_id:171806) provides a powerful and flexible framework for analyzing time-to-event data. Its central assumption of proportional hazards, however, may not always be met in practice, and its requirement for time-fixed covariates can be a significant limitation. Real-world clinical and epidemiological studies often involve characteristics that change over time, such as evolving disease states, fluctuating biomarker levels, or changes in treatment regimens. Furthermore, the effect of certain factors may not be constant throughout the duration of follow-up. This chapter delves into two fundamental extensions of the Cox model designed to address these complexities: **time-dependent covariates** and **stratification**. By mastering these principles, analysts can build more realistic models that better reflect the dynamic nature of biological and clinical processes.

### Incorporating Time-Dependent Covariates

The basic Cox model assumes that an individual's covariate vector $X$ is measured at baseline and remains constant over time. This is often an oversimplification. Consider a study where a patient's blood pressure is measured at each follow-up visit, or where a subject's medication status changes during the observation period. To accommodate such scenarios, we extend the model to allow for a covariate vector, denoted $X(t)$, whose values can change over time.

#### Defining the Model with Time-Dependent Covariates

The hazard function for an individual at time $t$ is now conditioned on the value of their covariate vector at that same instant, $X(t)$. The model is expressed as:

$$
h(t | X(t)) = h_0(t) \exp(\beta^\top X(t))
$$

Here, $h_0(t)$ remains the unspecified baseline [hazard function](@entry_id:177479), representing the hazard when $X(t)=0$. The vector $\beta$ contains the log-hazard ratios, which are still assumed to be constant over time. The crucial difference is that the linear predictor, $\beta^\top X(t)$, is now a function of time, reflecting the evolving status of the individual.

#### The Meaning of Proportional Hazards Revisited

The inclusion of time-dependent covariates necessitates a more nuanced understanding of the proportional hazards (PH) assumption [@problem_id:4961530]. The term "[proportional hazards](@entry_id:166780)" refers to the model's fundamental structure, which dictates that the ratio of hazards for any two individuals at the *same point in time* depends only on their covariate values at that time, not on time itself via the baseline hazard.

Let's consider two individuals, A and B, with covariate histories $X_A(t)$ and $X_B(t)$. Their hazard ratio at time $t$ is:

$$
\frac{h_A(t)}{h_B(t)} = \frac{h_0(t) \exp(\beta^\top X_A(t))}{h_0(t) \exp(\beta^\top X_B(t))} = \exp(\beta^\top [X_A(t) - X_B(t)])
$$

Notice that the baseline hazard $h_0(t)$ cancels out, which is the essence of proportionality. However, because the covariate vectors $X_A(t)$ and $X_B(t)$ are themselves functions of time, their difference, and thus the entire hazard ratio, can also change over time. For example, if $X(t)$ represents current treatment status, the hazard ratio comparing a treated to an untreated individual will change at the moment one of them alters their treatment. Therefore, in the presence of time-dependent covariates, the PH assumption does not imply that the hazard ratio between two subjects is constant throughout their entire follow-up. Instead, it implies that at any given instant $t$, the hazard is proportional to the baseline hazard, with a proportionality factor determined by the *current* covariate values [@problem_id:4961530].

It is essential to distinguish this from a model with **time-varying coefficients**, which would take the form $h(t|X) = h_0(t)\exp(\beta(t)^\top X)$. This latter model is used when the *effect* of a (typically time-fixed) covariate is thought to change over time, a different source of non-proportionality [@problem_id:4961540].

#### The Counting Process Framework: A Formal Approach

To handle the complexities of time-dependent data, including staggered entry and complex censoring patterns, survival analysis relies on the elegant formalism of counting process theory. For each individual $i$, we define several processes:

*   The **counting process**, $N_i(t)$, which counts the number of observed events for individual $i$ up to time $t$. For a single, non-recurrent event, it is a [step function](@entry_id:158924) that jumps from $0$ to $1$ at the event time.

*   The **at-risk indicator process**, $Y_i(t)$, which takes the value $1$ if individual $i$ is under observation and has not yet experienced the event at time $t$, and $0$ otherwise. This simple indicator elegantly handles both left-truncation (delayed entry, where $Y_i(t)=0$ before the study entry time) and right-censoring.

*   The **covariate process**, $X_i(t)$, which is the history of the individual's time-dependent covariates.

The [instantaneous rate of change](@entry_id:141382) of the counting process is described by its **intensity process**, $\lambda_i(t)$. The intensity is defined such that $\lambda_i(t)dt$ is the probability that individual $i$ experiences an event in the infinitesimal interval $[t, t+dt)$, given all information available up to time $t$. An event can only occur if the individual is at risk, so the intensity must be zero when $Y_i(t)=0$. This links the intensity to the hazard function:

$$
\lambda_i(t) = Y_i(t) h(t | X_i(t))
$$

Substituting the Cox model for the hazard function, the individual intensity process becomes:

$$
\lambda_i(t) = Y_i(t) h_0(t) \exp(\beta^\top X_i(t))
$$

This formulation [@problem_id:4961491] provides the rigorous mathematical foundation for estimating the parameters of the Cox model with time-dependent data.

#### Practical Implementation: The Start-Stop Data Representation

In practice, we must translate an individual's continuous-time history into a format that statistical software can analyze. This is achieved using the **start-stop** or **counting process** [data representation](@entry_id:636977). An individual's entire follow-up period is partitioned into a series of non-overlapping intervals, $(\text{start}, \text{stop}]$, such that their covariate values are constant within each interval. A new interval begins whenever a covariate value changes.

Each interval is represented by a separate row in the dataset, containing the subject's ID, the start time, the stop time, the constant covariate values for that interval, and an event indicator. The event indicator is $0$ for all intervals except the final one for a subject who experiences an event, where it is $1$.

For example, consider a subject who enters a study at time $t=1$ (left-truncated), has a covariate $X$ that changes from $0$ to $1$ at $t=4$ and from $1$ to $2$ at $t=8$, and experiences the event at $t=10$. This single subject's history would be represented by three rows in the dataset [@problem_id:4961476]:
*   Row 1: $(\text{start}=1, \text{stop}=4, X=0, \text{event}=0)$
*   Row 2: $(\text{start}=4, \text{stop}=8, X=1, \text{event}=0)$
*   Row 3: $(\text{start}=8, \text{stop}=10, X=2, \text{event}=1)$

This [data structure](@entry_id:634264) allows the [partial likelihood](@entry_id:165240) estimation procedure to correctly identify the risk set and the covariate values for all individuals at risk at the precise moment each event occurs.

### Addressing Non-Proportional Hazards: The Stratified Cox Model

The second major challenge in survival analysis is the potential violation of the [proportional hazards assumption](@entry_id:163597) for a key covariate. For instance, in a multi-center clinical trial, different centers might have fundamentally different patient populations or care protocols, leading their baseline event rates to diverge or converge over time. Forcing a single baseline hazard function $h_0(t)$ on all centers would be a misspecification. Including "center" as a regular covariate would impose the PH assumption, forcing the hazard ratio between any two centers to be constant over time, which is precisely the assumption being violated.

The solution to this problem is **stratification**. Instead of estimating a single baseline hazard function, we estimate a separate, completely unspecified baseline hazard for each level (or **stratum**) of the problematic categorical covariate.

The stratified Cox model is defined as:

$$
h_s(t | X(t)) = h_{0s}(t) \exp(\beta^\top X(t))
$$

Here, $s$ indexes the strata (e.g., $s=1, 2, \dots, K$ for $K$ clinical centers). The model has two key features [@problem_id:4961500, @problem_id:4961542]:
1.  Each stratum $s$ has its own unique baseline hazard function, $h_{0s}(t)$. These functions are not assumed to be related to each other in any way; they can cross, diverge, or converge arbitrarily.
2.  The vector of [regression coefficients](@entry_id:634860), $\beta$, is assumed to be **common** across all strata. This reflects a belief that while the baseline risk may differ between centers, the relative effect of the covariates in $X(t)$ (e.g., the benefit of a treatment) is the same in every center.

By allowing separate baseline hazards, the effect of the stratifying variable is effectively absorbed into them. The hazard ratio comparing two individuals in different strata, $g_i$ and $g_j$, is now a function of time [@problem_id:4961490]:

$$
\mathrm{HR}_{i:j}(t) = \frac{h_{0,g_i}(t)}{h_{0,g_j}(t)} \exp(\beta^\top [X_i(t) - X_j(t)])
$$

Since the ratio of the baseline hazards, $\frac{h_{0,g_i}(t)}{h_{0,g_j}(t)}$, is not necessarily constant, this model explicitly allows for non-[proportional hazards](@entry_id:166780) *between* the strata. In contrast, for two individuals within the *same* stratum ($g_i = g_j = g$), the baseline hazards cancel, and the hazard ratio simplifies to the familiar proportional form:

$$
\mathrm{HR}_{i:j}(t) = \exp(\beta^\top [X_i(t) - X_j(t)])
$$

Thus, stratification elegantly resolves non-proportionality for the stratifying variable while maintaining the familiar structure of the Cox model for the other covariates within each stratum [@problem_id:4961542].

### Estimation: The Stratified Partial Likelihood

Estimation of the common coefficient vector $\beta$ in a stratified model proceeds via maximization of a stratified partial likelihood. The crucial principle is that all comparisons are made only **within strata**.

At each time an event occurs, we construct a risk set. However, this risk set only includes individuals who belong to the same stratum as the person who experienced the event. The contribution to the partial likelihood from an event to subject $i$ in stratum $s$ at time $t_j$ is:

$$
\frac{\exp(\beta^\top X_i(t_j))}{\sum_{k \in R_s(t_j)} \exp(\beta^\top X_k(t_j))}
$$

where $R_s(t_j)$ is the set of individuals at risk in stratum $s$ at time $t_j$. Notice that the stratum-specific baseline hazard $h_{0s}(t_j)$ would appear in both the numerator and denominator, and thus cancels out. The full [partial likelihood](@entry_id:165240) is simply the product of these terms over all events in all strata [@problem_id:4961500].

To make this concrete, let's examine the calculation of the denominator at a specific event time $t$. The risk set $R_s(t)$ contains all individuals in stratum $s$ who have entered the study and are still alive and uncensored just prior to $t$. The covariate vector $X_k(t)$ for each individual $k \in R_s(t)$ is their value at that instant. For example, if an event occurs at $t=7$, we must use the covariate values that are active at $t=7$. If a subject's covariate changed at $t=6.5$, this new value is used. If it changes at the exact moment of the event, say $t=7$, theory dictates that we use the value just before the change (the [left-hand limit](@entry_id:139055)), as the covariate process must be **predictable**—its value at $t$ is determined by information known just before $t$ [@problem_id:4961515].

For the [partial likelihood](@entry_id:165240) estimator $\hat{\beta}$ to be consistent, a few key theoretical conditions must be met [@problem_id:4961537]:
1.  **Predictability of Covariates**: As mentioned, the covariate process $X_i(t)$ must not depend on information from the future.
2.  **Conditional Non-informative Censoring**: The censoring mechanism must not provide information about an individual's risk of failure that is not already captured by the covariate history. This allows censoring to depend on past health status, but not on future prognosis.
3.  **Correct Risk Set Specification**: The risk sets must be correctly constructed at every event time, respecting each individual's entry time, [exit time](@entry_id:190603), and stratum membership.

### A Critical Pitfall: Immortal Time Bias

When working with time-dependent exposures, such as the initiation of a new drug, analysts must be wary of a subtle but devastating error known as **immortal time bias**. This bias arises from the incorrect classification of exposure time.

Consider an observational study where patients may initiate a drug at some point after their initial diagnosis. A naive (and incorrect) analysis might classify any patient who *ever* initiates the drug as "exposed" for their entire follow-up period, from time $t=0$. The period between diagnosis ($t=0$) and drug initiation for these patients is "immortal" with respect to the exposed group's experience: by definition, they had to survive this period to initiate the drug. An event could not have occurred to them *as an exposed person* during this time.

Including this immortal time in the person-time denominator for the exposed group, without any corresponding events, artificially deflates the calculated event rate for this group. This can make a harmful drug appear neutral or even protective [@problem_id:4961522]. For instance, a calculation on a sample dataset showed a naive analysis yielding a [rate ratio](@entry_id:164491) of $0.81$ (suggesting a 19% risk reduction), whereas a correct time-dependent analysis revealed the true [rate ratio](@entry_id:164491) to be $3.27$ (suggesting a more than 3-fold increase in risk). The only way to avoid this bias is to treat exposure as a time-dependent covariate, where individuals contribute person-time to the unexposed group before initiation and to the exposed group only after initiation.

### Summary: Choosing the Right Analytic Tool

This chapter has introduced three powerful ways to extend the Cox model to reflect the complexities of real-world data. It is crucial to understand their distinct purposes to select the appropriate tool for a given analytic challenge [@problem_id:4961540]:

*   **Time-Dependent Covariates ($X(t)$)** are used when the *value* of a characteristic changes over time (e.g., blood pressure, tumor size, current medication). The model form is $h(t|X(t)) = h_0(t)\exp(\beta^\top X(t))$.

*   **Time-Varying Coefficients ($\beta(t)$)** are used when the *effect* (log-hazard ratio) of a covariate is believed to change over time (e.g., the effect of a surgical intervention may be high initially and wane over time). The model form is $h(t|X) = h_0(t)\exp(\beta(t)^\top X)$.

*   **Stratification** is used when a categorical covariate violates the [proportional hazards assumption](@entry_id:163597). Its effect is allowed to be non-proportional by absorbing it into stratum-specific baseline hazard functions. The model form is $h_s(t|X) = h_{0s}(t)\exp(\beta^\top X)$.

These methods are not interchangeable. They address different sources of model misspecification and can even be combined, for example, in a stratified Cox model with time-dependent covariates. A thoughtful application of these principles allows for a more rigorous and valid analysis of complex time-to-event data.