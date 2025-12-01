## Introduction
Time-to-event analysis is a cornerstone of [statistical modeling](@entry_id:272466), particularly in medicine and public health, where understanding the timing of events like disease progression, recovery, or death is critical for evaluating treatments and quantifying prognosis. This analysis hinges on two fundamental concepts—the [survival function](@entry_id:267383) and the [hazard function](@entry_id:177479). Mastering their definitions, their intricate mathematical relationship, and their application to data with incomplete observations is essential for any researcher or analyst working with longitudinal outcomes.

This article provides a comprehensive exploration of these core concepts, building from first principles to advanced applications. Across three chapters, you will gain a robust understanding of modern survival analysis. The journey begins in **"Principles and Mechanisms"**, where we will formally define the survival and hazard functions, derive their mathematical connection, and introduce foundational methods for estimation in the presence of [censored data](@entry_id:173222), including the non-parametric Kaplan-Meier estimator and the semi-parametric Cox [proportional hazards model](@entry_id:171806). Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these theoretical models are used to solve real-world problems, from comparing clinical trial outcomes to assessing [credit risk](@entry_id:146012) in finance and reliability in engineering, while also touching upon advanced topics like [competing risks](@entry_id:173277) and frailty models. Finally, **"Hands-On Practices"** will offer the opportunity to solidify these concepts through targeted problem-solving. This structured approach will equip you with the knowledge to not only interpret but also effectively apply survival analysis in your own work.

## Principles and Mechanisms

In the analysis of time-to-event data, our primary goal is to characterize the distribution of event times. This chapter transitions from the introductory concepts to the core mathematical machinery used to describe and model these distributions. We will formally define the principal functions of survival analysis—the survival and hazard functions—and explore their intricate relationship. We will then establish how to perform statistical inference in the ubiquitous presence of incomplete data, known as censoring, and conclude by introducing the foundational model for assessing the impact of covariates on event risk.

### Core Quantities: The Survival and Hazard Functions

The cornerstone of survival analysis is the **time-to-event variable**, a non-negative random variable, denoted by $T$, representing the time from a defined starting point to the occurrence of an event of interest. This event could be progression of a disease in an oncology trial, relapse after therapy, or readmission to a hospital.

#### The Survival Function

The most intuitive way to describe the distribution of $T$ is through the **[survival function](@entry_id:267383)**, denoted $S(t)$. It is defined as the probability that the time-to-event is greater than some specified time $t$.

$$S(t) = P(T > t)$$

The survival function is directly related to the more familiar **cumulative distribution function (CDF)**, $F(t)$, which gives the probability that the event has occurred by time $t$, i.e., $F(t) = P(T \le t)$. Since the event has either occurred by time $t$ or it has not, these probabilities must sum to one. Therefore, for any time-to-event variable, the relationship is:

$$S(t) = 1 - F(t)$$

The survival function has several key properties that follow from this definition. In the context of a clinical study where time is a non-negative, continuous variable, we can establish its behavior at the boundaries [@problem_id:4853746].
At the beginning of follow-up ($t=0$), we assume that no subject has yet experienced the event. For a continuous variable $T$, the probability of an event occurring at any single instant, including exactly at $t=0$, is zero. That is, $P(T=0)=0$. Thus, the probability of "surviving" past time zero, $S(0) = P(T > 0)$, is equal to $P(T \ge 0)$, which is 1. We write this as $S(0^+) = 1$, where the notation indicates the limit as $t$ approaches $0$ from the right.

As time progresses, $S(t)$ is a non-increasing function, as the probability of surviving can only decrease or stay the same as the time horizon lengthens. In most clinical and biological contexts, we assume that the event will eventually occur for all subjects if they are followed long enough. This corresponds to a **proper probability distribution**. Under this assumption, the probability of surviving indefinitely is zero, which means:

$$\lim_{t\to\infty} S(t) = 0$$

This property holds even for scenarios where we know that all events must occur by some finite maximum time, $\tau$. In such cases of **finite lifetime support**, where $P(T \le \tau) = 1$, it is guaranteed that $S(t) = 0$ for all $t \ge \tau$, and thus the limit is also zero [@problem_id:4853746].

#### The Hazard Function

While the survival function describes the cumulative probability of being event-free, the **[hazard function](@entry_id:177479)**, $h(t)$, provides an instantaneous perspective. It quantifies the risk of experiencing the event at time $t$, conditional on having been event-free up to that very moment. It is an "[instantaneous failure rate](@entry_id:171877)."

To formalize this, we first consider the average [failure rate](@entry_id:264373) over a small time interval $[t, t+\Delta t)$, given survival up to time $t$. This is the conditional probability of the event occurring in the interval, divided by the interval's duration, $\Delta t$ [@problem_id:4991492].

$$ \text{Average Rate} = \frac{P(t \le T  t+\Delta t \mid T \ge t)}{\Delta t} $$

The hazard function is the limit of this average rate as the interval shrinks to an infinitesimal point in time:

$$ h(t) = \lim_{\Delta t \to 0^+} \frac{P(t \le T  t+\Delta t \mid T \ge t)}{\Delta t} $$

The numerator is a dimensionless probability, while the denominator has units of time. Therefore, the hazard function $h(t)$ has units of inverse time (e.g., events per person-year). It is a rate, not a probability, and its value can exceed 1. For instance, a hazard of $h(t) = 0.1$ events/year at a specific time $t$ means that a subject who is event-free just before $t$ has, at that instant, a risk of failure corresponding to a rate of $0.1$ events per year.

### The Interrelationship of Survival and Hazard

The survival and hazard functions are two sides of the same coin; one can always be derived from the other. This fundamental relationship is central to survival modeling. Starting from the definition of the [hazard function](@entry_id:177479) and using the relationship between [conditional probability](@entry_id:151013) and the [survival function](@entry_id:267383), we can derive a differential equation.

The conditional probability in the numerator of the hazard definition is $P(t \le T  t+\Delta t \mid T \ge t) = \frac{P(t \le T  t+\Delta t)}{P(T \ge t)} = \frac{S(t) - S(t+\Delta t)}{S(t)}$. Substituting this gives:

$$ h(t) = \lim_{\Delta t \to 0^+} \frac{S(t) - S(t+\Delta t)}{\Delta t \cdot S(t)} = \frac{1}{S(t)} \left( -\lim_{\Delta t \to 0^+} \frac{S(t+\Delta t) - S(t)}{\Delta t} \right) $$

Recognizing the limit as the definition of the derivative $S'(t)$, we arrive at:

$$ h(t) = -\frac{S'(t)}{S(t)} = -\frac{d}{dt}\ln(S(t)) $$

This differential equation is the mathematical linchpin connecting the two functions [@problem_id:4956177]. To express the [survival function](@entry_id:267383) in terms of the hazard, we can integrate this equation from $0$ to $t$. This leads to the definition of the **[cumulative hazard function](@entry_id:169734)**, $H(t)$:

$$ H(t) = \int_0^t h(u) \, du $$

The cumulative hazard represents the total accumulated risk up to time $t$. Since the [hazard rate](@entry_id:266388) $h(t)$ is always non-negative, $H(t)$ is a non-decreasing function of time [@problem_id:4612114]. It continues to accumulate risk even if the instantaneous hazard $h(t)$ decreases over some periods.

Integrating the differential equation yields $-\ln(S(t)) + \ln(S(0)) = \int_0^t h(u) \, du = H(t)$. Since $S(0)=1$, we have $\ln(S(0))=0$, which simplifies to $H(t) = -\ln(S(t))$. Exponentiating this equation gives the explicit formula for the survival function in terms of the cumulative hazard:

$$ S(t) = \exp(-H(t)) = \exp\left(-\int_0^t h(u) \, du\right) $$

For a survival model to represent a proper probability distribution where the event is certain to eventually occur, the total accumulated risk must be infinite, which means $\lim_{t \to \infty} H(t) = \infty$. This ensures that $\lim_{t \to \infty} S(t) = 0$ [@problem_id:4956177].

To illustrate these concepts, consider a study where the hazard of an adverse event is piecewise-constant. For example, let the hazard be $h(t) = 0.08$ per month for the first 3 months, then decrease to $h(t) = 0.02$ for months 3 to 6, and then rise to $h(t) = 0.05$ for months 6 to 9 [@problem_id:4612114]. The cumulative hazard at $t=9$ months is found by summing the accumulated risk in each interval:
$$ H(9) = \int_0^3 0.08 \,du + \int_3^6 0.02 \,du + \int_6^9 0.05 \,du = (0.08 \times 3) + (0.02 \times 3) + (0.05 \times 3) = 0.24 + 0.06 + 0.15 = 0.45 $$
The [survival probability](@entry_id:137919) at 9 months is then $S(9) = \exp(-H(9)) = \exp(-0.45)$. Notice how $H(t)$ increases at every step, even when the instantaneous hazard $h(t)$ drops from $0.08$ to $0.02$ at the 3-month mark.

### Dealing with Incomplete Data: Censoring and Truncation

A defining feature of survival analysis is that our data are often incomplete. In a typical clinical study, we may not observe the event for every subject due to patients dropping out, the study ending, or other reasons. This incomplete observation is known as **censoring**. It is crucial to distinguish between different types of censoring, as they represent different states of knowledge about the true event time $T$ [@problem_id:4853768].

*   **Right-Censoring**: This is the most common form of censoring. It occurs when a subject's follow-up ends before the event is observed. We only know that the true event time $T$ is greater than the last known event-free time, $C$. The observed data for a subject is a pair: the observed time $Y = \min(T, C)$ and an event indicator $\Delta = \mathbb{I}(T \le C)$, where $\mathbb{I}(\cdot)$ is the indicator function. If $\Delta=1$, the event was observed at time $Y=T$. If $\Delta=0$, the subject was censored at time $Y=C$, and we only know that $T  C$.

*   **Left-Censoring**: This occurs when we know the event happened before a certain observation time $L$, but we do not know exactly when. All we know is $T \le L$. For instance, if a patient is found to have relapsed at their first post-treatment assessment, their relapse time is left-censored.

*   **Interval-Censoring**: This occurs when a subject is monitored periodically. If a subject is event-free at time $L$ but is found to have had the event by the next visit at time $R$, the event time is known only to lie in the interval $(L, R]$. This is common in studies with scheduled check-ups.

It is important to distinguish censoring from **left-truncation** (or late entry). In a truncated dataset, subjects are only included in the study if they are event-free at a certain time $L$. Individuals for whom $T \le L$ are systematically excluded from observation entirely. In a left-censored dataset, the subject is known to be part of the cohort, and the information $T \le L$ is part of the data.

For standard statistical methods to yield valid results, the censoring mechanism must be **non-informative**. The weakest and most common version of this assumption is that, conditional on any measured covariates $X$, the true event time $T$ is independent of the censoring time $C$. This is written as $T \perp C \mid X$ [@problem_id:4853768]. This assumption means that, for individuals with the same covariate profile, the reason for censoring provides no extra information about their future risk of the event.

### The Likelihood Function for Right-Censored Data

The concept of censoring is directly incorporated into the construction of the **likelihood function**, which is the foundation for [parameter estimation](@entry_id:139349) in most survival models. The likelihood of the observed data is the [joint probability](@entry_id:266356) of all observations. Assuming subjects are independent, this is the product of the likelihood contributions from each individual.

Let's derive the contribution for a single subject $i$ with observation $(t_i, \delta_i)$, where $t_i$ is the observed time and $\delta_i$ is the event indicator (1 if event, 0 if right-censored), and covariates $x_i$ [@problem_id:4991471].

1.  **Uncensored Observation ($\delta_i = 1$)**: The event was observed to occur at time $t_i$. For a continuous variable, the probability of an event in an infinitesimal interval $[t_i, t_i+dt)$ is given by the probability density function (PDF), $f(t_i \mid x_i)dt$. The likelihood contribution is therefore the density $f(t_i \mid x_i)$.

2.  **Right-Censored Observation ($\delta_i = 0$)**: The subject was observed to be event-free up to time $t_i$, after which they were lost to follow-up. The information we have is that their true event time is greater than $t_i$. The probability of this is, by definition, the survival function, $S(t_i \mid x_i)$.

We can write a single elegant expression for the likelihood contribution of subject $i$ using the event indicator $\delta_i$:

$$ L_i(\theta) = [f(t_i \mid x_i; \theta)]^{\delta_i} [S(t_i \mid x_i; \theta)]^{1-\delta_i} $$

Here, $\theta$ represents the parameters of the model. The full likelihood for the entire dataset is the product of these individual contributions:

$$ L(\theta) = \prod_i [f(t_i \mid x_i; \theta)]^{\delta_i} [S(t_i \mid x_i; \theta)]^{1-\delta_i} $$

Using the relationship $f(t \mid x) = h(t \mid x)S(t \mid x)$, we can rewrite the full likelihood in a form that is often more convenient, especially for proportional hazards models:

$$ L(\theta) = \prod_i [h(t_i \mid x_i; \theta)S(t_i \mid x_i; \theta)]^{\delta_i} [S(t_i \mid x_i; \theta)]^{1-\delta_i} = \prod_i [h(t_i \mid x_i; \theta)]^{\delta_i} S(t_i \mid x_i; \theta) $$

This formulation shows that every subject contributes their survival probability up to their last observation time $t_i$, and those who experience an event contribute an additional factor of the hazard at that instant.

### Non-parametric Estimation

Often, we do not wish to assume a particular [parametric form](@entry_id:176887) (e.g., Weibull or exponential) for the distribution of event times. Non-parametric methods allow us to estimate the survival and hazard functions directly from the data.

#### The Kaplan-Meier Estimator for Survival

The most widely used non-parametric estimator for the [survival function](@entry_id:267383) is the **Kaplan-Meier (KM) estimator**, also known as the [product-limit estimator](@entry_id:171437). It can be derived from first principles using the [chain rule of probability](@entry_id:268139) [@problem_id:4956179].

Let the distinct, ordered event times in the data be $t_1  t_2  \dots  t_k$. The probability of surviving past some time $t$ can be expressed as a product of conditional probabilities:
$$ S(t) = P(T  t_1) \times P(T  t_2 \mid T  t_1) \times \dots $$
At each event time $t_i$, we estimate the conditional probability of surviving past $t_i$, given survival up to that point. Let $n_i$ be the number of subjects at risk (alive and uncensored) just before time $t_i$, and let $d_i$ be the number of subjects who experience the event at $t_i$. The estimated conditional probability of failing at $t_i$ is $\frac{d_i}{n_i}$. Therefore, the estimated conditional probability of surviving past $t_i$ is $1 - \frac{d_i}{n_i}$.

The Kaplan-Meier estimator for the [survival function](@entry_id:267383) is the product of these estimated conditional survival probabilities for all event times up to time $t$:

$$ \hat{S}(t) = \prod_{t_i \le t} \left(1 - \frac{d_i}{n_i}\right) $$

The resulting estimator is a step function that decreases only at the observed event times.

#### The Nelson-Aalen Estimator for Cumulative Hazard

An alternative non-parametric approach focuses on estimating the [cumulative hazard function](@entry_id:169734), $H(t)$. The **Nelson-Aalen (NA) estimator** is built by summing the estimated hazard increments at each event time [@problem_id:4991508]. The instantaneous hazard is a rate, so the amount of hazard accumulated over a small interval around $t_i$ is $h(t_i)\Delta t$. This is approximately the [conditional probability](@entry_id:151013) of failure at $t_i$, which we estimated as $\frac{d_i}{n_i}$. The NA estimator for the cumulative hazard is therefore the sum of these hazard increments:

$$ \hat{H}(t) = \sum_{t_i \le t} \frac{d_i}{n_i} $$

Using the relationship $S(t) = \exp(-H(t))$, we can obtain a corresponding non-parametric estimator for the survival function, known as the Fleming-Harrington estimator, by plugging in the Nelson-Aalen estimate:

$$ \hat{S}(t) = \exp(-\hat{H}(t)) = \exp\left(-\sum_{t_i \le t} \frac{d_i}{n_i}\right) $$

This provides a smooth alternative to the Kaplan-Meier step function, though they are asymptotically equivalent.

### Modeling Covariate Effects: The Proportional Hazards Model

A primary goal in medical research is to understand how patient characteristics, or covariates, affect the time to an event. The most celebrated tool for this is the **proportional hazards (PH) model**, introduced by Sir David Cox. The model assumes that covariates act multiplicatively on an underlying baseline [hazard function](@entry_id:177479), $h_0(t)$ [@problem_id:4991485].

The hazard for an individual with a vector of covariates $x$ is modeled as:

$$ h(t \mid x) = h_0(t) \exp(\beta^\top x) $$

Here, $h_0(t)$ is the **baseline hazard function**, which is the hazard for an individual with all covariates equal to zero ($x=0$). The term $\exp(\beta^\top x)$ is a time-independent scalar that modifies the baseline hazard. The vector $\beta$ contains the [regression coefficients](@entry_id:634860), which quantify the effect of each covariate on the log-hazard.

The central implication of this model is that the ratio of hazards for any two individuals is constant over time. For two individuals with covariate vectors $x_1$ and $x_2$:

$$ \frac{h(t \mid x_1)}{h(t \mid x_2)} = \frac{h_0(t) \exp(\beta^\top x_1)}{h_0(t) \exp(\beta^\top x_2)} = \exp(\beta^\top(x_1 - x_2)) $$

This constant ratio is the **hazard ratio (HR)**. The baseline hazard $h_0(t)$, which can have any arbitrary shape, cancels out completely. This property gives the model its name and its great flexibility. It's important to note that this proportionality does not extend to survival functions or probability densities; the ratio of survival probabilities, $S(t \mid x_1) / S(t \mid x_2)$, is not constant over time [@problem_id:4991485].

The genius of the Cox model lies in its "semi-parametric" nature. It is possible to estimate the parameter vector $\beta$ without making any assumptions about the form of the baseline hazard $h_0(t)$. This is achieved using a **partial likelihood** function [@problem_id:4956193].

The partial likelihood is constructed as a product of conditional probabilities over the observed event times. At each event time $t_{(k)}$, we consider the set of individuals at risk, $R_k$. The contribution to the partial likelihood is the conditional probability that the specific individual observed to fail, say subject $i$, is the one who fails, given that exactly one failure occurred among the members of $R_k$. This probability is:

$$ P(\text{subject } i \text{ fails} \mid \text{one failure in } R_k) = \frac{\text{Hazard for subject } i}{\sum_{j \in R_k} \text{Hazard for subject } j} = \frac{h(t_{(k)} \mid x_i)}{\sum_{j \in R_k} h(t_{(k)} \mid x_j)} $$

Substituting the PH model form, we find that the baseline hazard cancels out:

$$ \frac{h_0(t_{(k)}) \exp(\beta^\top x_i)}{ \sum_{j \in R_k} h_0(t_{(k)}) \exp(\beta^\top x_j)} = \frac{\exp(\beta^\top x_i)}{\sum_{j \in R_k} \exp(\beta^\top x_j)} $$

The full [partial likelihood](@entry_id:165240) is the product of these terms over all event times. Because $h_0(t)$ vanishes from the expression, we can obtain estimates for $\beta$ by maximizing this function, thereby identifying the hazard ratios without any knowledge of the absolute risk or its evolution over time. This separation of the relative effects ($\beta$) from the baseline risk ($h_0(t)$) is the methodological hallmark of the Cox model.