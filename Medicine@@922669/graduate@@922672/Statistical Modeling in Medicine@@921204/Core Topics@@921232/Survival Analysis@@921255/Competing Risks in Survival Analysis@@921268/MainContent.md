## Introduction
In many time-to-event studies, particularly in medical research, individuals are at risk of experiencing several different types of events. When the occurrence of one event precludes the occurrence of another, these are known as competing risks. The presence of such events presents a significant analytical challenge, as standard survival analysis techniques, like the Kaplan-Meier method, can produce misleading results by failing to properly account for the different event types. This article provides a comprehensive guide to understanding and correctly analyzing data in the presence of [competing risks](@entry_id:173277). The journey begins in the **Principles and Mechanisms** chapter, where we will establish the formal framework, define the crucial quantities of cause-specific hazards and cumulative incidence functions, and detail the two primary regression strategies: cause-specific and subdistribution hazard models. Next, the **Applications and Interdisciplinary Connections** chapter will bridge theory and practice by exploring how these methods are applied to solve substantive problems in oncology, epidemiology, public health, and even finance. Finally, the **Hands-On Practices** chapter offers a series of targeted exercises designed to reinforce these concepts and build practical skills in applying them. By navigating these chapters, you will gain the theoretical knowledge and practical insight needed to confidently tackle competing risks in your own research.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of competing risks as a common challenge in medical research, where individuals are subject to multiple, mutually exclusive types of events. Understanding the principles that govern the analysis of such data is paramount for drawing valid scientific conclusions. This chapter delves into the fundamental framework for competing risks, defining the key metrics for quantifying risk, and elucidating the two major approaches to regression modeling: cause-specific and subdistribution hazard models.

### The Formal Framework of Competing Risks

To analyze competing risks rigorously, we must first establish a formal mathematical framework. Consider a study where an individual can experience one of $K$ distinct and [mutually exclusive events](@entry_id:265118). From a conceptual standpoint, we can imagine that for each individual, there exists a set of unobservable, or **latent**, failure times, $(T_1, T_2, \dots, T_K)$, where $T_k$ represents the hypothetical time at which the event of type $k$ would occur if all other events were impossible. In addition, an individual's follow-up may be terminated by a **[right-censoring](@entry_id:164686)** event at time $C$, for reasons such as loss to follow-up or the administrative end of the study.

In practice, we do not observe the full set of latent failure times. Instead, we only observe the time of the *first* event that occurs. This leads to the observable data for each individual, which consists of a pair $(T, \Delta)$. Here, $T$ is the observed event or censoring time, defined as:

$$T = \min(T_1, T_2, \dots, T_K, C)$$

The variable $\Delta$ is an event indicator that tells us the cause of the event at time $T$. By convention, we set $\Delta = k$ if the observed event was a failure of type $k$ (i.e., $T_k = T$), and $\Delta = 0$ if the observation was right-censored (i.e., $C = T$) [@problem_id:4956480].

A critical assumption for most standard analyses is that of **[non-informative censoring](@entry_id:170081)**. This assumption posits that, at any given time, individuals who are censored are not systematically different in their future risk of failure compared to those who remain under observation. Formally, we assume that the censoring time $C$ is independent of the vector of latent failure times $(T_1, \dots, T_K)$, potentially conditional on a set of baseline covariates $X$. This is expressed as:

$$C \perp (T_1, T_2, \dots, T_K) \mid X$$

This assumption ensures that censoring does not introduce bias into our estimates of risk [@problem_id:4956514]. It is of profound importance to recognize what this framework does *not* assume. The validity of this observable data framework does not require the latent failure times $T_k$ to be independent of each other. In fact, a foundational result in competing risks theory is that the dependence structure among the latent failure times is **non-identifiable** from the observable data $(T, \Delta)$ alone. Multiple, contradictory assumptions about the dependence between latent events can lead to the exact same distribution of observable data. Consequently, without imposing strong, untestable assumptions, we cannot make statistical inferences about this latent dependence structure. This principle guides the entire field toward focusing on quantities that are directly estimable from the data we can actually see [@problem_id:4956519].

### Quantifying Risk: Cause-Specific Hazards and Cumulative Incidence

Given that our analysis must be grounded in observable quantities, we require metrics that can be defined solely in terms of the distribution of $(T, \Delta)$. The two principal measures for quantifying risk in this setting are the cause-specific hazard and the cumulative incidence function.

#### The Cause-Specific Hazard

The **cause-specific hazard (CSH)**, denoted $\lambda_k(t)$, measures the instantaneous rate of failure due to cause $k$ at time $t$, given that an individual has not experienced any event of any type prior to time $t$. Mathematically, it is defined as:

$$\lambda_k(t) = \lim_{h\to 0} \frac{\mathbb{P}(T \in [t, t+h), \Delta=k \mid T \ge t)}{h}$$

The conditioning event, $T \ge t$, is crucial: it defines the **risk set** for the cause-specific hazard as consisting of all individuals who are event-free and uncensored at time $t$. An individual is removed from this risk set at the moment they experience an event of *any* cause or are censored [@problem_id:4956480].

It is essential to distinguish between a competing event and a censoring event in this context. Suppose we are interested in the cause-specific hazard for cause 1, $\lambda_1(t)$. If a patient experiences a competing event of cause 2 at time $u$, they are removed from the risk set for all times $t > u$. This is because they are no longer "at risk" for event 1. Similarly, if a patient is censored at time $u$, they are also removed from the risk set for all $t > u$. The fundamental difference, however, is that the competing event is an observed failure outcome, whereas censoring represents incomplete observation [@problem_id:4956514].

#### The Cumulative Incidence Function

While the cause-specific hazard describes an instantaneous rate, clinical interest often lies in the overall probability of an event occurring over a period of time. This is captured by the **cumulative incidence function (CIF)**, denoted $F_k(t)$. The CIF is defined as the probability that a failure from cause $k$ has occurred by time $t$:

$$F_k(t) = \mathbb{P}(T \le t, \Delta = k)$$

The CIF represents the **absolute risk**, or **crude probability**, of experiencing event $k$ by time $t$ in the real-world setting where all competing risks are simultaneously active [@problem_id:4772062].

These two fundamental quantities, the CSH and the CIF, are intrinsically linked. The probability of experiencing event $k$ in a small interval $[u, u+du)$ is the product of the probability of being at risk at time $u$ (i.e., surviving all causes until $u$), $S(u) = \mathbb{P}(T > u)$, and the instantaneous rate of event $k$ given survival, $\lambda_k(u)du$. Integrating this instantaneous probability from time 0 to $t$ yields the CIF:

$$F_k(t) = \int_0^t S(u) \lambda_k(u) du$$

This relationship highlights a critical feature of [competing risks](@entry_id:173277): the cumulative incidence of a specific cause, $k$, depends not only on its own cause-specific hazard, $\lambda_k(t)$, but also on the hazards of all other competing causes, as they are encapsulated within the overall [survival function](@entry_id:267383) $S(t)$.

### A Common Methodological Pitfall: The 1-Minus-Kaplan-Meier Fallacy

A frequent and serious error in analyzing [competing risks](@entry_id:173277) data is to treat competing events as if they were [non-informative censoring](@entry_id:170081) times and then to apply the standard Kaplan-Meier (KM) method to estimate the probability of the event of interest. The resulting quantity, often denoted $1 - \hat{S}_{KM}(t)$, is then misinterpreted as an estimate of the CIF.

This approach is fundamentally flawed because it attempts to estimate a different quantity, known as the **net risk**. The net risk is the probability of failure in a hypothetical world where all competing risks have been eliminated. In contrast, the CIF represents the **crude risk** in the real world where competing risks are present. Because competing events remove individuals from the at-risk pool, the crude risk (CIF) will always be less than or equal to the net risk (1-KM) [@problem_id:4579888].

For example, consider a simplified scenario with constant cause-specific hazards for a disease of interest, $\lambda_D = 0.04$ per year, and a competing event, $\lambda_C = 0.06$ per year. The 5-year CIF, or crude probability, correctly accounts for both hazards and is calculated as $\frac{\lambda_D}{\lambda_D+\lambda_C}(1 - \exp(-(\lambda_D+\lambda_C) \times 5))$, which is approximately $0.157$. The incorrect 1-KM approach, which treats the competing events as censoring, would estimate the net probability $1 - \exp(-\lambda_D \times 5)$, which is approximately $0.181$. The overestimation is a direct consequence of ignoring the fact that a proportion of the population is no longer at risk for the disease of interest because they have already experienced the competing event [@problem_id:4579888].

The mathematical reason for this overestimation can be seen by examining the infinitesimal increments that each estimator accumulates. A proper estimator for the CIF, $\hat{F}_k(t)$, accumulates increments of the form $\hat{S}(u-) \frac{dN_k(u)}{Y(u)}$, where $dN_k(u)$ is the number of events of cause $k$ at time $u$ and $\hat{S}(u-)$ is the overall event-free survival probability. The incorrect $1 - \hat{S}_{KM}(t)$ approach (where competing events are censored for cause $k$ analysis), however, is fundamentally flawed because its underlying survival estimate is not reduced by competing events. It thus overestimates the proportion of the population truly at risk for event $k$ at later times. This systematically accumulates more probability mass, leading to the inequality $1 - \hat{S}_{KM}(t) \ge \hat{F}_k(t)$ [@problem_id:4956499].

### Regression Modeling Strategies

In medical research, a primary goal is often to assess the effect of covariates, such as treatment exposure or patient characteristics, on the risk of an event. In the [competing risks](@entry_id:173277) setting, there are two dominant regression strategies, which model different aspects of risk and thus have different interpretations.

#### Modeling Cause-Specific Hazards

The most direct approach is to model the cause-specific hazard for each event type separately using a standard Cox proportional hazards model. For cause $k$ and a covariate vector $X$, the model is specified as:

$$\lambda_k(t \mid X) = \lambda_{0k}(t) \exp(\beta_k' X)$$

Here, $\lambda_{0k}(t)$ is an unspecified baseline cause-specific hazard, and $\beta_k$ is the vector of [regression coefficients](@entry_id:634860) for cause $k$. The interpretation of a coefficient in this model is straightforward: $\exp(\beta_k)$ is the **cause-specific hazard ratio**. It represents the multiplicative effect of a one-unit increase in the corresponding covariate on the instantaneous rate of cause $k$ events among those who are currently event-free.

A crucial point of interpretation is that the cause-specific hazard ratio, $\exp(\beta_k)$, does **not** generally equal the ratio of cumulative incidences. The effect of a covariate on the CIF is more complex. As we saw, the CIF, $F_k(t \mid X) = \int_0^t S(u \mid X) \lambda_k(u \mid X) du$, depends on the covariate's effect on $\lambda_k$ and its effect on the overall survival function $S(u \mid X)$. The overall survival is determined by the sum of *all* cause-specific hazards. Therefore, if a covariate affects the hazards of competing events, it will alter the at-risk population over time, thereby indirectly influencing the cumulative incidence of cause $k$. For instance, a treatment that strongly reduces the risk of a competing event may increase the size of the population remaining at risk for the event of interest, potentially leading to an increase in its cumulative incidence even if the treatment has no direct effect on its cause-specific hazard [@problem_id:4956462].

#### Modeling the Cumulative Incidence Function: The Fine-Gray Model

If the primary research goal is to evaluate the effect of covariates on the absolute risk or cumulative incidence, an alternative approach is to model the CIF directly. The most common method for this is the **Fine-Gray model**, which models the **subdistribution hazard**.

The ingenuity of this approach lies in the redefinition of the risk set. For a cause-specific hazard analysis of cause 1, an individual who experiences a competing event (cause 2) is removed from the risk set. For a subdistribution hazard analysis of cause 1, that individual is artificially kept in the risk set. The subdistribution risk set at time $t$ for cause 1 comprises all individuals who have not yet experienced an event of cause 1, regardless of whether they have experienced a competing event [@problem_id:4956504].

The subdistribution hazard for cause $k$, denoted $\tilde{\lambda}_k(t)$, is the instantaneous rate of cause $k$ events in this specially defined risk set. Formally:

$$\tilde{\lambda}_k(t) = \lim_{\Delta t \to 0} \frac{\mathbb{P}(t \le T  t+\Delta t, \Delta = k \mid T > t \text{ or } (T \le t, \Delta \ne k))}{\Delta t}$$

The denominator, $\mathbb{P}(T > t \text{ or } (T \le t, \Delta \ne k))$, is simply $1 - \mathbb{P}(T \le t, \Delta = k)$, which is $1 - F_k(t)$. This leads to a beautifully simple relationship between the subdistribution hazard and the CIF:

$$F_k(t) = 1 - \exp\left(-\int_0^t \tilde{\lambda}_k(u) du\right)$$

This relationship is analogous to the standard link between a [hazard function](@entry_id:177479) and a survival function, and it is the foundation of the Fine-Gray model [@problem_id:4956464]. The model specifies a [proportional hazards assumption](@entry_id:163597) on the subdistribution hazard:

$$\tilde{\lambda}_k(t \mid X) = \tilde{\lambda}_{0k}(t) \exp(\gamma_k' X)$$

The interpretation of the coefficient $\gamma_k$ from this model is more complex than that of the cause-specific Cox model. The **subdistribution hazard ratio (SHR)**, $\exp(\gamma_k)$, does not represent a simple ratio of CIFs. Instead, it implies the following relationship between the "subdistribution survivor functions" ($1-F_k(t)$) for two groups (e.g., treated $Z=1$ vs. control $Z=0$):

$$1 - F_k(t \mid Z=1) = \left[1 - F_k(t \mid Z=0)\right]^{\exp(\gamma)}$$

This shows that the covariate has a multiplicative effect on the cumulative subdistribution hazard, which translates to a power relationship for the subdistribution survivor functions. While less intuitive than a simple ratio, this provides a direct link between the covariate and its effect on the ultimate cumulative incidence [@problem_id:4956489].

In summary, cause-specific models are often preferred for etiological questions about the instantaneous biological or mechanical process of failure, while subdistribution hazard models are preferred for prediction and for quantifying the effect of covariates on the overall, absolute risk of an event over time. The choice of model should be driven by the specific research question.