## Introduction
Survival analysis, also known as [time-to-event analysis](@entry_id:163785), is a powerful statistical framework that moves beyond asking *if* an event will occur to asking *when*. From predicting patient survival in a clinical trial to determining the failure time of an engineering component, its applications are vast and critical. The central challenge in this field is dealing with incomplete data. Often, we do not observe the event for every subject in a study; instead, we only know that they survived up to a certain point before being lost to follow-up. This phenomenon, called [censoring](@entry_id:164473), would bias traditional statistical methods, but it is a core feature that [survival analysis](@entry_id:264012) is designed to handle correctly.

This article provides a comprehensive introduction to the fundamentals of [survival analysis](@entry_id:264012). The first chapter, **Principles and Mechanisms**, will build your understanding from the ground up, defining core concepts like the survival and hazard functions, introducing the Kaplan-Meier estimator for non-[parametric analysis](@entry_id:634671), and detailing the widely used Cox [proportional hazards model](@entry_id:171806). Next, in **Applications and Interdisciplinary Connections**, we will explore how these powerful methods are applied to solve real-world problems in diverse fields such as biomedical research, [engineering reliability](@entry_id:192742), and business analytics. Finally, the **Hands-On Practices** chapter will allow you to solidify your knowledge by tackling practical problems and interpreting the results of survival models.

## Principles and Mechanisms

Survival analysis, or [time-to-event analysis](@entry_id:163785), is a collection of statistical procedures for which the outcome variable of interest is the time until an event occurs. This chapter elucidates the core principles and statistical machinery that form the foundation of this field. We will begin by defining the fundamental quantities used to characterize time-to-event data, then explore the essential challenge of incomplete observations, and finally develop the key non-parametric and [semi-parametric models](@entry_id:200031) used for estimation and inference.

### Fundamental Quantities of Survival Analysis

At the heart of [survival analysis](@entry_id:264012) are several interrelated functions that together provide a complete characterization of the distribution of event times. Let $T$ be a non-negative random variable representing the time until an event of interest.

The most intuitive of these functions is the **[survival function](@entry_id:267383)**, denoted by $S(t)$. It is defined as the probability that the event time $T$ is greater than some specified time $t$:

$S(t) = \mathbb{P}(T > t)$

The [survival function](@entry_id:267383) starts at $S(0) = 1$ (assuming no events occur at the exact beginning) and is a non-increasing function of $t$, approaching $0$ as $t \to \infty$. Its complement, $F(t) = 1 - S(t) = \mathbb{P}(T \le t)$, is the [cumulative distribution function](@entry_id:143135) (CDF).

From the CDF, we can define the **probability density function** (PDF), $f(t)$, which describes the probability of the event occurring in an infinitesimal interval around $t$. For continuous event times, the relationship is:

$f(t) = \frac{d}{dt} F(t) = -S'(t)$

While the [survival function](@entry_id:267383) describes the cumulative probability of surviving past time $t$, the **[hazard function](@entry_id:177479)**, $\lambda(t)$, describes the [instantaneous potential](@entry_id:264520) for the event to occur at time $t$, given that it has not already occurred. It is formally defined as the limit of the probability of an event in a small interval $[t, t+\Delta t)$, divided by the length of the interval $\Delta t$, conditional on survival up to time $t$:

$\lambda(t) = \lim_{\Delta t \to 0^+} \frac{\mathbb{P}(t \le T  t + \Delta t \mid T \ge t)}{\Delta t}$

The [hazard function](@entry_id:177479) is a rate, not a probability, and its value can range from $0$ to $\infty$. Using the definition of conditional probability, we can see the direct relationship between the three functions:

$\lambda(t) = \frac{\lim_{\Delta t \to 0^+} \frac{\mathbb{P}(t \le T  t + \Delta t)}{\Delta t}}{\mathbb{P}(T \ge t)} = \frac{f(t)}{S(t)}$

This relationship allows us to express the [survival function](@entry_id:267383) in terms of the [hazard function](@entry_id:177479). By integrating $\lambda(t) = -S'(t)/S(t)$, we obtain the **[cumulative hazard function](@entry_id:169734)**, $\Lambda(t) = \int_0^t \lambda(u)du$, which leads to the fundamental identity:

$S(t) = \exp(-\Lambda(t)) = \exp\left(-\int_0^t \lambda(u)du\right)$

This equation demonstrates that knowing the [hazard function](@entry_id:177479) completely determines the [survival function](@entry_id:267383), and vice versa.

### The Challenge of Incomplete Data: Censoring and Truncation

A defining feature of [survival analysis](@entry_id:264012) is its ability to correctly handle incomplete observations. The most common form of incompleteness is **[right-censoring](@entry_id:164686)**, which occurs when a subject's time-to-event is not fully observed. Instead, we only know that their true event time is greater than a certain observed [censoring](@entry_id:164473) time.

Consider an experiment tracking a cohort of newly generated neurons in the brain [@problem_id:2745909]. An investigator images a fixed [field of view](@entry_id:175690) at discrete time points. The event of interest is neuron death. However, some neurons may migrate out of the imaging field. When a neuron disappears between sessions without evidence of death, its ultimate fate is unknown. We know it was alive up to the last time it was seen, but its true time of death is unobserved. This is a classic example of [right-censoring](@entry_id:164686). If we were to naively exclude these censored observations or treat them as if they had died, our survival estimates would be biased. Survival analysis provides the tools to use the partial information from these subjects correctly.

For standard survival estimators to be valid, the [censoring](@entry_id:164473) mechanism must be **non-informative**. Informally, this means that, conditional on any measured covariates, the act of [censoring](@entry_id:164473) provides no extra information about the subject's prognosis. Violating this assumption leads to **informative [censoring](@entry_id:164473)** and biased results. [@problem_id:3179117] provides several illustrative scenarios:

*   **Administrative Censoring**: A study has a pre-specified end date. All subjects still at risk (event-free) at this date are censored. This is the archetypal [non-informative censoring](@entry_id:170081) mechanism, as the [censoring](@entry_id:164473) is determined by the study's calendar, not by the subjects' health.
*   **Loss to Follow-up (Conditionally Non-Informative)**: Patients may move away and stop attending clinic visits. If the reasons for moving (e.g., age, distance to clinic) are measured as covariates and are not otherwise related to the subject's hidden health status, the [censoring](@entry_id:164473) can be considered non-informative *conditional on the covariates*.
*   **Informative Censoring**: In a study using electronic health records, sicker patients might have more frequent clinical contact and thus are less likely to be censored (i.e., they have longer follow-up times), while healthier patients with sparse records are censored earlier. Here, the [censoring](@entry_id:164473) time is directly related to the underlying prognosis, making the [censoring](@entry_id:164473) informative and invalidating standard methods.

Another form of data incompleteness is **left truncation**, or delayed entry. This occurs when subjects are not observed from the beginning of the time scale (e.g., from birth or diagnosis) but only enter the study at a later time. For an individual to be included in the study, they must have survived up to their entry time. This requires special handling of the risk sets, as we will see later [@problem_id:3179091].

### Non-Parametric Estimation of Survival and Hazard

When we do not wish to make strong assumptions about the underlying distribution of survival times, we can use non-parametric estimators. The two most important are the Kaplan-Meier estimator for the survival function and the Nelson-Aalen estimator for the [cumulative hazard function](@entry_id:169734).

#### The Kaplan-Meier Estimator

The **Kaplan-Meier (KM) estimator**, also known as the [product-limit estimator](@entry_id:171437), is built on a simple, powerful idea: the probability of surviving beyond time $t$ is the product of the conditional probabilities of surviving through each preceding interval that ends in an event.

Let the distinct event times be $t_1  t_2  \dots  t_k$. At each event time $t_i$, let $d_i$ be the number of individuals who experience the event, and let $n_i$ be the number of individuals at risk (alive and under observation) just prior to $t_i$. The conditional probability of surviving past $t_i$, given survival up to $t_i$, is estimated as $(n_i - d_i) / n_i$. The KM estimate of the survival function is then the product of these factors over all event times up to $t$:

$\hat{S}_{KM}(t) = \prod_{i: t_i \le t} \left(1 - \frac{d_i}{n_i}\right)$

Censored observations are crucial in this calculation: they remain in the risk set until their [censoring](@entry_id:164473) time, at which point they are removed from the denominator $n_i$ for all subsequent calculations. They do not contribute to the event counts $d_i$.

Let's construct the KM estimator from first principles using a small dataset [@problem_id:3179090]. Consider a cohort of 7 individuals with the following observed times (in weeks) and outcomes ($\delta=1$ for event, $\delta=0$ for [censoring](@entry_id:164473)): $(1, 1), (3, 1), (4, 0), (5, 1), (7, 0), (8, 1), (10, 1)$.

First, we establish the [life table](@entry_id:139699):
*   At $t_1=1$: An event occurs. The risk set contains all 7 individuals. So, $n_1=7, d_1=1$.
*   At $t_2=3$: An event occurs. Subject 1 is no longer at risk. The risk set has 6 individuals. So, $n_2=6, d_2=1$.
*   At $t=4$: A subject is censored. This does not change the survival estimate at this time.
*   At $t_3=5$: An event occurs. Subjects 1 (event), 2 (event), and 3 (censored) are no longer at risk. The risk set has 4 individuals. So, $n_3=4, d_3=1$.

To find the [survival probability](@entry_id:137919) at week 7, $\hat{S}(7)$, we note that the KM estimate is a step function that only changes at event times. Therefore, $\hat{S}(7)$ is the same as the value just after the last event at $t=5$. We compute the product of the conditional survival probabilities:

$\hat{S}(7) = \hat{S}(5) = \left(1 - \frac{d_1}{n_1}\right) \times \left(1 - \frac{d_2}{n_2}\right) \times \left(1 - \frac{d_3}{n_3}\right) = \left(1 - \frac{1}{7}\right) \times \left(1 - \frac{1}{6}\right) \times \left(1 - \frac{1}{4}\right)$

$\hat{S}(7) = \left(\frac{6}{7}\right) \times \left(\frac{5}{6}\right) \times \left(\frac{3}{4}\right) = \frac{15}{28} \approx 0.536$

This step-by-step calculation, which correctly incorporates information from subjects who are censored, is the cornerstone of non-parametric [survival analysis](@entry_id:264012).

#### The Nelson-Aalen Estimator and its Relationship to Kaplan-Meier

While the KM estimator focuses on the survival function, the **Nelson-Aalen (NA) estimator** provides a non-parametric estimate of the [cumulative hazard function](@entry_id:169734), $\Lambda(t)$. Its construction is additive rather than multiplicative. At each event time $t_i$, the term $d_i/n_i$ represents the estimated hazard increment. The NA estimator is simply the sum of these increments up to time $t$:

$\hat{\Lambda}_{NA}(t) = \sum_{i: t_i \le t} \frac{d_i}{n_i}$

There is a deep connection between the KM and NA estimators that mirrors the continuous-time relationship $S(t) = \exp(-\Lambda(t))$. We can see this by taking the logarithm of the KM estimator:

$\ln \hat{S}_{KM}(t) = \sum_{i: t_i \le t} \ln\left(1 - \frac{d_i}{n_i}\right)$

Using the Taylor [series expansion](@entry_id:142878) $\ln(1-x) = -x - x^2/2 - \dots$, we get:

$\ln \hat{S}_{KM}(t) \approx \sum_{i: t_i \le t} \left(-\frac{d_i}{n_i}\right) = -\hat{\Lambda}_{NA}(t)$

This leads to the important approximation $\hat{S}_{KM}(t) \approx \exp(-\hat{\Lambda}_{NA}(t))$. This approximation is most accurate when the individual hazard increments $d_i/n_i$ are small, which is typical in large datasets with few tied event times. In small samples or at the tail of the survival curve where risk sets are small, the approximation can be less precise [@problem_id:3179138].

### Modeling Covariates: The Cox Proportional Hazards Model

Often, our goal is not just to describe the survival experience of a single group but to understand how various factors, or **covariates**, influence the time to event. The **Cox Proportional Hazards (CPH) model**, proposed by Sir David Cox in 1972, is the most widely used method for this purpose.

The model is semi-parametric and assumes that the hazard for an individual with a covariate vector $\mathbf{x}$ is given by:

$h(t \mid \mathbf{x}) = h_0(t) \exp(\mathbf{x}^T \boldsymbol{\beta})$

This model has two key components:
1.  The **baseline [hazard function](@entry_id:177479)**, $h_0(t)$, which is an unknown, non-parametric function of time. It represents the hazard for an individual with all covariates equal to zero ($\mathbf{x}=\mathbf{0}$).
2.  The parametric component, $\exp(\mathbf{x}^T \boldsymbol{\beta})$, which describes how the covariates modify the baseline hazard. $\boldsymbol{\beta}$ is a vector of [regression coefficients](@entry_id:634860) to be estimated. The term $\exp(\mathbf{x}^T \boldsymbol{\beta})$ is the **[hazard ratio](@entry_id:173429) (HR)** relative to baseline.

The central assumption of the model is **[proportional hazards](@entry_id:166780)**: the ratio of the hazards for any two individuals is constant over time. For individuals with covariates $\mathbf{x}_1$ and $\mathbf{x}_2$, the [hazard ratio](@entry_id:173429) is:

$\frac{h(t \mid \mathbf{x}_1)}{h(t \mid \mathbf{x}_2)} = \frac{h_0(t) \exp(\mathbf{x}_1^T \boldsymbol{\beta})}{h_0(t) \exp(\mathbf{x}_2^T \boldsymbol{\beta})} = \exp((\mathbf{x}_1 - \mathbf{x}_2)^T \boldsymbol{\beta})$

Notice that the time-dependent baseline hazard $h_0(t)$ cancels out. This observation is the key to estimating $\boldsymbol{\beta}$.

#### Partial Likelihood Estimation

The genius of the Cox model lies in its method of estimation, the **[partial likelihood](@entry_id:165240)**. It allows us to estimate the [regression coefficients](@entry_id:634860) $\boldsymbol{\beta}$ without needing to know or estimate the baseline hazard $h_0(t)$.

The [partial likelihood](@entry_id:165240) is constructed as a product of conditional probabilities over the observed event times. Consider an event occurring at time $t_j$ for subject $i_j$. Given the risk set $R(t_j)$ (the set of all individuals still at risk just before $t_j$) and the fact that exactly one event occurred, the [conditional probability](@entry_id:151013) that it was subject $i_j$ who had the event is the ratio of their hazard to the sum of the hazards of everyone in the risk set [@problem_id:3179096]:

$P(\text{subject } i_j \text{ fails} \mid \text{one failure from } R(t_j) \text{ at } t_j) = \frac{h(t_j \mid \mathbf{x}_{i_j})}{\sum_{k \in R(t_j)} h(t_j \mid \mathbf{x}_k)} = \frac{h_0(t_j)\exp(\mathbf{x}_{i_j}^T \boldsymbol{\beta})}{\sum_{k \in R(t_j)} h_0(t_j)\exp(\mathbf{x}_k^T \boldsymbol{\beta})} = \frac{\exp(\mathbf{x}_{i_j}^T \boldsymbol{\beta})}{\sum_{k \in R(t_j)} \exp(\mathbf{x}_k^T \boldsymbol{\beta})}$

The baseline hazard $h_0(t_j)$ cancels completely. The [partial likelihood](@entry_id:165240) for the entire dataset is the product of these terms for all observed events:

$L_p(\boldsymbol{\beta}) = \prod_{j: \text{event at } t_j} \frac{\exp(\mathbf{x}_{i_j}^T \boldsymbol{\beta})}{\sum_{k \in R(t_j)} \exp(\mathbf{x}_k^T \boldsymbol{\beta})}$

This function depends only on $\boldsymbol{\beta}$ and the data, and it can be maximized to find the maximum [partial likelihood](@entry_id:165240) estimate, $\hat{\boldsymbol{\beta}}$.

Let's illustrate with a small example [@problem_id:3179095]. A study has 4 subjects, with event times ordered as $t=1$ (Subject 3, $x_3=2$), $t=2$ (Subject 1, $x_1=0$), and $t=4$ (Subject 4, $x_4=1$). Subject 2 ($x_2=1$) is censored at $t=3$.
*   **Event at $t=1$**: The risk set $R(1)$ includes all 4 subjects. The [partial likelihood](@entry_id:165240) term is $\frac{\exp(2\beta)}{\exp(2\beta) + \exp(0\beta) + \exp(1\beta) + \exp(1\beta)}$.
*   **Event at $t=2$**: Subject 3 has exited. The risk set $R(2)$ includes Subjects 1, 2, and 4. The term is $\frac{\exp(0\beta)}{\exp(0\beta) + \exp(1\beta) + \exp(1\beta)}$.
*   **Event at $t=4$**: Subjects 1 (event) and 2 (censored) have exited. The risk set $R(4)$ contains only Subject 4. The term is $\frac{\exp(1\beta)}{\exp(1\beta)} = 1$.
The full [partial likelihood](@entry_id:165240) is the product of these terms. Notice how the censored subject contributes to the denominators of the risk sets for events occurring before its [censoring](@entry_id:164473) time.

#### Prediction with the Cox Model

Once we have the estimate $\hat{\boldsymbol{\beta}}$, we can make predictions. This involves a two-step process [@problem_id:3179096]:
1.  **Estimate the Baseline Cumulative Hazard**: We use the **Breslow estimator**, which extends the logic of the Nelson-Aalen estimator to the regression context:
    $\hat{\Lambda}_0(t) = \sum_{j: t_j \le t} \frac{d_j}{\sum_{k \in R(t_j)} \exp(\mathbf{x}_k^T \hat{\boldsymbol{\beta}})}$
    The denominator is the sum of the estimated relative risks for all individuals in the risk set at each event time.
2.  **Predict Survival**: The baseline [survival function](@entry_id:267383) is estimated as $\hat{S}_0(t) = \exp(-\hat{\Lambda}_0(t))$. For a new individual with covariates $\mathbf{x}^*$, the predicted survival function is derived from the [proportional hazards](@entry_id:166780) structure:
    $\hat{S}(t \mid \mathbf{x}^*) = \hat{S}_0(t)^{\exp(\mathbf{x}^{*T} \hat{\boldsymbol{\beta}})}$
    This powerful formula combines the non-parametric baseline survival curve with the parametric effect of the covariates to generate individualized survival predictions.

### Advanced Topics and Practical Considerations

The framework of [survival analysis](@entry_id:264012) is flexible and can be adapted to handle more complex scenarios.

#### Time-Varying Risk Sets and Covariates

The definition of the risk set is critical and can be adapted to various study designs.
*   **Left Truncation**: When individuals have delayed entry into a study at time $L_i$, they are only eligible to be in the risk set for times $t$ where $L_i \le t$. When constructing the [partial likelihood](@entry_id:165240) for a Cox model, the risk set $R(t)$ correctly includes only those individuals who have entered the study by time $t$ and have not yet experienced an event or been censored [@problem_id:3179091].
*   **Time-Dependent Covariates**: In many real-world scenarios, a subject's exposure status can change over time. For example, a patient may start a new treatment midway through follow-up. A naive analysis that classifies the patient as "treated" from baseline can lead to a severe form of confounding known as **immortal time bias**. This is because the patient had to survive the "immortal" time period before starting treatment, and incorrectly allocating this event-free time to the treated group artificially deflates its risk rate. The correct approach is to model the exposure as a time-dependent covariate, $X(t)$, which switches from $0$ to $1$ at the time treatment begins. By correctly allocating person-time to unexposed and exposed periods, this bias can be eliminated, often reversing the apparent effect of the treatment [@problem_id:3179064].

#### The Choice and Transformation of the Time Axis

The choice of time scale is a crucial modeling decision. Time can be measured as age, calendar time, or time since diagnosis, among others. A key feature of the Cox model is that the estimate of $\boldsymbol{\beta}$ is invariant to any strictly increasing monotonic transformation of time. However, the baseline [hazard function](@entry_id:177479) $h_0(t)$ is not. If we re-scale time according to a smooth, strictly increasing function $s = g(t)$, the baseline hazard on the new time scale, $\lambda_0^{(s)}(s)$, is related to the original baseline hazard $\lambda_0^{(t)}(t)$ by:

$\lambda_0^{(s)}(s) = \lambda_0^{(t)}(g^{-1}(s)) \cdot \frac{d}{ds}g^{-1}(s)$

This transformation rule underscores the interpretation of hazard as a rate (events per unit time) and shows how it must be rescaled when the units of time are changed [@problem_id:3179145]. For instance, switching from age to time-since-diagnosis corresponds to a simple shift of the time axis, which shifts the functional form of the baseline hazard.

#### Competing Risks

In some studies, there may be several distinct types of events, and the occurrence of one type prevents the others from being observed. This is the **[competing risks](@entry_id:173277)** framework. For example, in a study of elderly patients, causes of death could be cancer, heart disease, or other causes.

In this setting, we define a **cause-specific hazard**, $\lambda_k(t)$, for each cause $k$. This is the instantaneous rate of failure from cause $k$, given survival up to time $t$ [@problem_id:3179114]. The overall hazard is the sum of the cause-specific hazards: $\lambda(t) = \sum_k \lambda_k(t)$.

A common goal in [competing risks analysis](@entry_id:634319) is to estimate the probability of experiencing a specific event type by time $t$. One might be tempted to use the Kaplan-Meier method, treating all other event types as censored. However, this estimates a quantity in a hypothetical world where other causes of failure do not exist, and it does not yield the true probability in the presence of [competing risks](@entry_id:173277).

The correct quantity is the **Cumulative Incidence Function (CIF)**, $F_k(t) = \mathbb{P}(T \le t, J=k)$, where $J$ is the event type. The CIF can be directly estimated and has a fundamental relationship with the cause-specific hazard and the overall survival function $S(t)$:

$F_k(t) = \int_0^t \lambda_k(u) S(u-) du$

Here, $S(u-)$ is the [left-hand limit](@entry_id:139055) of the [survival function](@entry_id:267383), representing the probability of being at risk just before time $u$. The use of the left-limit is crucial to correctly account for individuals who fail at exactly time $u$ [@problem_id:3179114]. This integral shows that the probability of failing from cause $k$ depends not only on the rate of cause $k$ events but also on the probability of surviving all other causes long enough for a cause $k$ event to occur.