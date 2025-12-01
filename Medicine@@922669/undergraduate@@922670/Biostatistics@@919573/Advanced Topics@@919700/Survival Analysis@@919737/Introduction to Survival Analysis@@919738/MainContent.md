## Introduction
How long until a patient's cancer recurs? When will a mechanical component fail? How long will a user remain subscribed to a service? These are questions not just about *if* an event will happen, but *when*. The statistical field dedicated to answering them is survival analysis. Its significance lies in its ability to model time-to-event data, a unique data type prevalent in fields from medicine to engineering. However, the primary challenge in analyzing this data is that we often have incomplete information; subjects may leave a study or the study may end before the event of interest occurs, a phenomenon known as censoring. This article provides a comprehensive introduction to the core concepts and methods of survival analysis. In the first chapter, 'Principles and Mechanisms,' we will lay the theoretical groundwork, defining censored data and the key functions used to describe risk over time. The second chapter, 'Applications and Interdisciplinary Connections,' will explore the broad utility of these methods in diverse fields. Finally, 'Hands-On Practices' will offer opportunities to apply these concepts. We begin by establishing the fundamental principles that make the analysis of time-to-event data possible.

## Principles and Mechanisms

Survival analysis is a collection of statistical procedures for which the outcome variable of interest is the time until an event occurs. This chapter introduces the foundational principles that govern the description and analysis of such time-to-event data. We will begin by defining the unique structure of this data, particularly the challenge of censoring. We will then develop the core mathematical functions used to characterize time-to-event distributions—the survival and hazard functions. Finally, we will explore the mechanisms for estimating these functions from data and for modeling the influence of covariates, culminating in an introduction to the widely used [proportional hazards model](@entry_id:171806).

### The Nature of Time-to-Event Data

The primary quantity of interest in survival analysis is the **time-to-event**, a non-negative random variable, denoted by $T$, representing the duration from a defined starting point to the occurrence of a specific event. This event could be death, disease recurrence, equipment failure, or any other well-defined endpoint.

A defining feature of survival data is that we often have incomplete information about $T$. Subjects may leave a study, the study may end before all subjects have experienced the event, or they may experience a different, competing event. This phenomenon is known as **censoring**.

#### Types of Censoring

There are several types of censoring, each corresponding to a different form of incomplete information about the true event time $T$ [@problem_id:4920657].

*   **Right Censoring**: This is the most common form of censoring in survival studies. It occurs when we observe a subject for a certain amount of time, but the event has not occurred by the end of the observation period. All we know is that the true event time $T$ is *greater than* the censoring time. For an observation right-censored at time $C$, the information we have is $T > C$.

*   **Left Censoring**: This occurs when the event is known to have happened *before* a certain time, but we do not know exactly when. For example, if a patient is tested for a chronic disease at a clinic visit at time $L$ and is found to be positive, we only know that the time of onset $T$ is less than or equal to the visit time, i.e., $T \le L$.

*   **Interval Censoring**: This form of censoring occurs when a subject's event time is only known to fall within an interval. This typically arises from periodic follow-up. If a subject is known to be event-free at an assessment at time $L$ but has experienced the event by the next assessment at time $R$, we know only that the event time $T$ falls within the interval $(L, R]$, or $L  T \le R$.

#### Formalizing Right-Censored Data

To handle right-censored data mathematically, we conceptualize two latent, or underlying, random variables for each subject $i$:
1.  The true time-to-event, $T_i \ge 0$.
2.  A potential censoring time, $C_i \ge 0$.

In a study, we can only follow a subject up to the point that either the event occurs or the subject is censored, whichever comes first. Therefore, the actual observed time for subject $i$ is the minimum of these two latent times:

$X_i = \min(T_i, C_i)$

This observed time $X_i$ alone is insufficient; we must also record whether the event occurred or if the observation was censored. This is captured by an **event indicator**, $\delta_i$. The standard convention is to set $\delta_i = 1$ if the event was observed and $\delta_i = 0$ if the observation was censored. An event is considered observed if the event time is less than *or equal to* the censoring time. This is a crucial detail; if a study ends on a specific day and a patient dies on that same day, their death is an observed event, not a censored data point. Thus, the event indicator is formally defined as:

$\delta_i = \mathbf{1}\{T_i \le C_i\}$

where $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167). The data we actually work with in a survival analysis are the pairs $(X_i, \delta_i)$ for each subject [@problem_id:4920605].

### Characterizing the Distribution of Event Times

To describe the distribution of the random variable $T$, we use a set of related mathematical functions. While one can be derived from another, each provides a unique and valuable perspective on the nature of the risk over time.

#### The Survival Function

The most intuitive of these is the **survival function**, denoted $S(t)$. It is defined as the probability that the event time $T$ is greater than some specified time $t$.

$S(t) = P(T  t)$

The [survival function](@entry_id:267383) provides a direct answer to the question: "What is the probability of surviving beyond time $t$?" Based on this probabilistic definition, the survival function has several fundamental properties [@problem_id:4920654]:

1.  **Domain and Range**: Since $S(t)$ is a probability, its values are in $[0, 1]$. As time $t$ must be non-negative, the domain of interest is typically $[0, \infty)$.
2.  **Boundary Conditions**: Assuming no events can occur before $t=0$, $S(0) = P(T0)$. If events can't occur exactly at $t=0$, then $P(T=0)=0$ and $S(0)=1$. As time extends to infinity, the probability of survival must approach zero, so $\lim_{t \to \infty} S(t) = 0$.
3.  **Monotonicity**: As time increases, the probability of survival cannot increase. Therefore, $S(t)$ is a **non-increasing** function of $t$. For any $t_1  t_2$, we must have $S(t_1) \ge S(t_2)$.
4.  **Continuity**: For any random variable $T$, its [survival function](@entry_id:267383) $S(t)$ is **right-continuous**. This means that as we approach any time $t$ from the right, the limit of the [survival function](@entry_id:267383) is equal to the value of the function at $t$, i.e., $\lim_{s \downarrow t} S(s) = S(t)$.

The survival function is simply the complement of the [cumulative distribution function](@entry_id:143135) (CDF), $F(t) = P(T \le t)$. Thus, for all $t$:

$S(t) = 1 - F(t)$

If the event time $T$ can take on discrete values, the [survival function](@entry_id:267383) will have downward jumps or discontinuities. The size of the jump at any time $t$ is exactly equal to the probability that the event occurs at that specific time: $S(t^-) - S(t) = P(T=t)$, where $S(t^-)$ is the limit from the left. If $T$ is a [continuous random variable](@entry_id:261218), then $P(T=t)=0$ for all $t$, and the survival function is continuous.

#### The Hazard Function

While the survival function describes the cumulative probability of not failing, the **[hazard function](@entry_id:177479)**, $h(t)$, provides an instantaneous measure of risk. It addresses the question: "Given that an individual has survived up to time $t$, what is the instantaneous rate at which they will experience the event?"

Formally, the [hazard function](@entry_id:177479) is defined as the limit of the probability of experiencing the event in a small interval $[t, t+\Delta t)$, given survival up to time $t$, divided by the width of the interval $\Delta t$:

$h(t) = \lim_{\Delta t \to 0^+} \frac{P(t \le T  t + \Delta t \mid T \ge t)}{\Delta t}$

The hazard is a rate, not a probability, so its value can be greater than 1. Its units are events per unit of time (e.g., deaths per person-year). The term $h(t)\Delta t$ can be interpreted as the approximate probability that an individual who is event-free at time $t$ will experience the event in the next small interval of time $\Delta t$ [@problem_id:4920653].

For a continuous time-to-event variable with probability density function (PDF) $f(t)$ and [survival function](@entry_id:267383) $S(t)$, the definition of [conditional probability](@entry_id:151013) leads to a fundamental relationship:

$h(t) = \frac{f(t)}{S(t)}$

This identity highlights that the hazard rate is the unconditional density of events at time $t$, scaled by the proportion of individuals who are still alive and at risk of the event at that time.

The survival and hazard functions are deterministically linked. Given the hazard function $h(t)$, the survival function can be recovered through the **[cumulative hazard function](@entry_id:169734)**, $H(t) = \int_0^t h(u)du$:

$S(t) = \exp(-H(t)) = \exp\left(-\int_0^t h(u)du\right)$

This relationship is immensely powerful, as it allows us to move between the different characterizations of the event time distribution.

#### Illustrative Example: The Weibull Distribution

To make these concepts concrete, consider a time-to-event variable $T$ that follows a Weibull distribution, a flexible parametric model often used in reliability engineering and survival analysis. Its survival function is given by:

$S(t) = \exp\left(-\left(\frac{t}{\alpha}\right)^\beta\right)$ for $t \ge 0$

Here, $\alpha  0$ is a **[scale parameter](@entry_id:268705)** that stretches or compresses the time axis, and $\beta  0$ is a **shape parameter** that dictates the pattern of risk over time.

We can derive the corresponding hazard function using the relationship $h(t) = -S'(t)/S(t)$, or by first finding the cumulative hazard $H(t) = -\ln(S(t))$. Using the latter approach:

$H(t) = -\ln\left[\exp\left(-\left(\frac{t}{\alpha}\right)^\beta\right)\right] = \left(\frac{t}{\alpha}\right)^\beta$

The hazard function is the derivative of the cumulative hazard, $h(t) = H'(t)$:

$h(t) = \frac{d}{dt} \left(\frac{t^\beta}{\alpha^\beta}\right) = \frac{\beta t^{\beta-1}}{\alpha^\beta} = \frac{\beta}{\alpha}\left(\frac{t}{\alpha}\right)^{\beta-1}$ [@problem_id:1925083]

The shape parameter $\beta$ determines the nature of the hazard over time:
- If $\beta  1$, the hazard rate $h(t)$ increases with time. This models phenomena where risk increases with age, such as many forms of cancer.
- If $\beta  1$, the hazard rate $h(t)$ decreases with time. This might model recovery after a surgery, where the risk of complication is highest immediately after the procedure.
- If $\beta = 1$, the [hazard rate](@entry_id:266388) is constant, $h(t) = 1/\alpha$. This is the [exponential distribution](@entry_id:273894), which characterizes "memoryless" processes where the risk of failure is constant regardless of how long the unit has survived.

### Estimation from Censored Data

The central challenge of survival analysis is to estimate functions like $S(t)$ and $h(t)$ from data that are subject to censoring. If we were to naively calculate the proportion of subjects surviving past time $t$ while ignoring censored observations or treating them as events, our estimates would be biased.

#### The Independent Censoring Assumption

To proceed with valid estimation, we must make a crucial assumption known as **[non-informative censoring](@entry_id:170081)** or **independent censoring**. In its general form, when covariates $X$ are present, this assumption states that, conditional on the covariates, the true event time $T$ is independent of the censoring time $C$:

$T \perp C \mid X$

This assumption means that, for individuals with the same covariate values, the mechanism that leads to censoring provides no extra information about their prognosis or risk of failure [@problem_id:4920602]. For example, if a clinical trial ends on a planned date, this is typically a [non-informative censoring](@entry_id:170081) mechanism. However, if a patient is withdrawn from a study because their health is deteriorating, this censoring is informative, and standard methods may not apply.

Under independent censoring, the instantaneous rate of observed events among those still at risk is an [unbiased estimator](@entry_id:166722) of the true underlying [hazard rate](@entry_id:266388). This fundamental property allows us to identify the hazard and survival functions from the observable data $(Y, \Delta, X)$. A further practical requirement is the **positivity assumption**, which states that there must be a non-zero probability of remaining uncensored at any time $t$ for which we wish to estimate the hazard, i.e., $P(C \ge t \mid X)  0$ [@problem_id:4920602].

#### The Kaplan-Meier Estimator

The most widely used non-[parametric method](@entry_id:137438) for estimating the [survival function](@entry_id:267383) from right-[censored data](@entry_id:173222) is the **[product-limit estimator](@entry_id:171437)**, more commonly known as the **Kaplan-Meier (KM) estimator**. It builds on the idea that the probability of surviving past time $t$ can be broken down into a product of conditional probabilities of surviving past each distinct event time up to $t$.

Let the ordered, distinct event times in the data be $t_{(1)}  t_{(2)}  \dots  t_{(D)}$. The survival function at a time $t$ can be written as:

$S(t) = P(T > t_{(k)})$ where $t_{(k)} \le t  t_{(k+1)}$
$S(t) = P(T  t_{(1)}) \times P(T  t_{(2)} \mid T  t_{(1)}) \times \dots \times P(T  t_{(k)} \mid T  t_{(k-1)})$

The Kaplan-Meier estimator provides an empirical estimate for each term in this product. For each event time $t_{(i)}$, let $n_i$ be the number of subjects at risk (those who have not yet had an event or been censored), and let $d_i$ be the number of subjects who experience the event at $t_{(i)}$. The empirical estimate for the [conditional probability](@entry_id:151013) of surviving past $t_{(i)}$ is then $(n_i - d_i) / n_i$.

The Kaplan-Meier estimate of the survival function is the product of these conditional probabilities up to time $t$:

$\hat{S}(t) = \prod_{i: t_{(i)} \le t} \left(1 - \frac{d_i}{n_i}\right)$

The result is a [step function](@entry_id:158924) that drops downwards only at the times when events occur. The size of each drop depends on the number of events relative to the number of individuals at risk at that time. Censored observations do not cause the survival curve to drop, but they do reduce the number of individuals in the risk set for subsequent event times.

**Worked Example: Calculating a Kaplan-Meier Estimate**

Let's apply this method to data from a clinical study with 12 individuals, where we want to estimate the [survival probability](@entry_id:137919) at 10 months [@problem_id:4920591].

The observed data (time in months, outcome) are: 1.5(Event), 2.0(Censored), 2.2(E), 3.0(E), 4.5(C), 5.0(E), 6.0(E), 7.5(C), 8.0(E), 9.0(C), 10.0(E), 12.0(C).

We construct a table to track the estimation process, focusing on the distinct event times:

| Event Time $t_{(i)}$ | At Risk $n_i$ | Events $d_i$ | Censored before next event | Cond. Survival Prob. $\frac{n_i - d_i}{n_i}$ | KM Estimate $\hat{S}(t_{(i)})$ |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **0** | 12 | 0 | 0 | - | 1.0000 |
| **1.5** | 12 | 1 | 1 (at 2.0) | $\frac{11}{12}$ | $1.0 \times \frac{11}{12} = 0.9167$ |
| **2.2** | 10 | 1 | 0 | $\frac{9}{10}$ | $0.9167 \times \frac{9}{10} = 0.8250$ |
| **3.0** | 9 | 1 | 1 (at 4.5) | $\frac{8}{9}$ | $0.8250 \times \frac{8}{9} = 0.7333$ |
| **5.0** | 7 | 1 | 0 | $\frac{6}{7}$ | $0.7333 \times \frac{6}{7} = 0.6286$ |
| **6.0** | 6 | 1 | 1 (at 7.5) | $\frac{5}{6}$ | $0.6286 \times \frac{5}{6} = 0.5238$ |
| **8.0** | 4 | 1 | 1 (at 9.0) | $\frac{3}{4}$ | $0.5238 \times \frac{3}{4} = 0.3929$ |
| **10.0** | 2 | 1 | 1 (at 12.0) | $\frac{1}{2}$ | $0.3929 \times \frac{1}{2} = 0.1964$ |

The estimated [survival probability](@entry_id:137919) at $t=10$ months is $\hat{S}(10)$. Since the KM curve is constant between events, $\hat{S}(10) = \hat{S}(10.0)$. From the table, we see that $\hat{S}(10.0) = 0.1964$. The calculation is:
$\hat{S}(10) = \frac{11}{12} \times \frac{9}{10} \times \frac{8}{9} \times \frac{6}{7} \times \frac{5}{6} \times \frac{3}{4} \times \frac{1}{2} = \frac{11}{56} \approx 0.1964$.

### Modeling the Effect of Covariates

While the Kaplan-Meier estimator is invaluable for describing survival in a single group, we often want to understand how different factors or covariates (e.g., treatment, age, biomarkers) affect survival time. The most popular approach for this is the **Cox proportional hazards model**.

#### The Proportional Hazards Assumption

The core of the Cox model is the **[proportional hazards assumption](@entry_id:163597)**. This assumption states that the ratio of the hazard functions for any two individuals is constant over time. For example, consider two groups, A and B. The [proportional hazards assumption](@entry_id:163597) implies:

$\frac{h_A(t)}{h_B(t)} = \lambda$ (a constant)

The constant $\lambda$ is called the **hazard ratio (HR)**. If $\lambda = 2$, it means individuals in group A have twice the instantaneous risk of failure at any given time $t$ compared to individuals in group B, given that they have survived to time $t$.

Let's consider a food science example modeling strawberry spoilage [@problem_id:1925081]. Suppose the hazard of spoilage for refrigerated strawberries is $h_{ref}(t)$ and for room-temperature strawberries is $h_{room}(t)$. If we assume [proportional hazards](@entry_id:166780) with a hazard ratio $\lambda = 4.0$, then $h_{room}(t) = 4.0 \times h_{ref}(t)$ for all $t$. This means that at any point in time, a room-temperature strawberry has four times the instantaneous risk of spoiling compared to a refrigerated one. This relationship allows us to determine the survival curve for one group if we know the survival curve and the hazard ratio for the other. Specifically, since $S(t) = \exp(-H(t))$, the relationship $h_{room}(t) = \lambda \cdot h_{ref}(t)$ implies $H_{room}(t) = \lambda \cdot H_{ref}(t)$, and thus:

$S_{room}(t) = \exp(-\lambda \cdot H_{ref}(t)) = (\exp(-H_{ref}(t)))^\lambda = [S_{ref}(t)]^\lambda$

#### The Cox Proportional Hazards Model

The Cox model generalizes this idea to a set of $p$ covariates contained in a vector $x = (x_1, \dots, x_p)$. The model specifies the [hazard function](@entry_id:177479) for an individual with covariates $x$ as:

$\lambda(t \mid x) = \lambda_0(t) \exp(\beta_1 x_1 + \beta_2 x_2 + \dots + \beta_p x_p) = \lambda_0(t) \exp(\beta^\top x)$

This model has two components:
1.  $\lambda_0(t)$: The **baseline hazard function**. This is the hazard function for an individual with all covariates equal to zero ($x=0$). The Cox model is called a **semi-parametric** model because it makes no assumptions about the shape of this baseline hazard.
2.  $\exp(\beta^\top x)$: The relative risk component. This part scales the baseline hazard up or down depending on the individual's covariate values.

The key interpretative feature comes from examining the hazard ratio for two individuals, one with covariates $x_A$ and another with covariates $x_B$:

$\frac{\lambda(t \mid x_A)}{\lambda(t \mid x_B)} = \frac{\lambda_0(t) \exp(\beta^\top x_A)}{\lambda_0(t) \exp(\beta^\top x_B)} = \exp(\beta^\top (x_A - x_B))$

Notice that the baseline hazard $\lambda_0(t)$ cancels out, meaning the hazard ratio is constant over time, satisfying the [proportional hazards assumption](@entry_id:163597).

To interpret a single coefficient, say $\beta_j$, consider two individuals with identical covariates except for $x_j$, which is one unit higher for the first individual. The hazard ratio is:

$\frac{\lambda(t \mid x_j+1)}{\lambda(t \mid x_j)} = \exp(\beta_j)$

Thus, $\exp(\beta_j)$ is the hazard ratio associated with a one-unit increase in the covariate $x_j$, holding all other covariates constant [@problem_id:4920590].

### An Extension: Competing Risks

In many real-world scenarios, subjects are at risk of more than one type of event, and the occurrence of one event precludes the occurrence of others. This is the **competing risks** setting. For example, in a study of elderly patients with heart disease, a patient might die from a cardiac event (the event of interest) or from cancer (a competing event).

In this framework, we model the risk of each event type using a **cause-specific [hazard function](@entry_id:177479)**, $h_k(t)$, for each cause $k$. The overall hazard of experiencing *any* event is simply the sum of the cause-specific hazards:

$h_{\text{overall}}(t) = \sum_k h_k(t)$

A key quantity of interest in [competing risks](@entry_id:173277) is the probability that an event, when it occurs, is of a particular type. Given that an event occurs at time $t$, the conditional probability that it is due to cause $j$ is the ratio of the cause-specific hazard for cause $j$ to the overall hazard at that time:

$P(\text{Event type} = j \mid \text{Event at time } t) = \frac{h_j(t)}{h_{\text{overall}}(t)}$

For instance, consider a biologist studying tadpoles that can either metamorphose into frogs (cause M) or be eaten by predators (cause P) [@problem_id:1925099]. Suppose the cause-specific hazards are $h_M(t) = 0.005t$ and $h_P(t) = 0.04$. If we observe an event (either metamorphosis or predation) at day $t_0 = 10.0$, the probability that this event was [metamorphosis](@entry_id:191420) is:

$P(\text{Metamorphosis} \mid \text{Event at } t=10) = \frac{h_M(10)}{h_M(10) + h_P(10)} = \frac{0.005 \times 10}{0.005 \times 10 + 0.04} = \frac{0.05}{0.05 + 0.04} = \frac{0.05}{0.09} \approx 0.556$

At 10 days, there is a 55.6% chance that an observed event is a successful [metamorphosis](@entry_id:191420) rather than a predation event. This highlights how cause-specific hazards allow us to dissect the different risks operating on a population over time.