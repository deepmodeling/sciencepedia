## Introduction
In medical and public health research, analyzing the time until an event occurs is a fundamental task. However, this analysis is often complicated by the presence of [competing risks](@entry_id:173277)—events that preclude the occurrence of the primary event of interest. For example, when studying death from cancer, death from cardiovascular disease is a competing risk. Standard survival analysis methods, such as the Cox proportional hazards model, can produce misleading results in this setting, as they fail to properly account for how competing events impact the absolute probability of the main outcome. This creates a critical knowledge gap: how do we accurately model the risk of a specific event when multiple outcomes are possible?

This article provides a detailed exploration of the Fine-Gray model, a powerful statistical tool designed specifically to address the challenge of competing risks. It resolves the ambiguity between etiologic and predictive questions by providing a direct framework for modeling the cumulative incidence function (CIF), or the absolute risk of an event. Across three chapters, you will gain a comprehensive understanding of this essential method. The first chapter, "Principles and Mechanisms," will unpack the core theory, contrasting the cause-specific hazard with the subdistribution hazard and explaining the model's unique construction. Following this, "Applications and Interdisciplinary Connections" will demonstrate the model's practical utility in clinical trials, prognostic modeling, and health [policy evaluation](@entry_id:136637). Finally, "Hands-On Practices" will provide concrete exercises to solidify your ability to apply and interpret the model's results, ensuring you can confidently leverage this technique in your own research.

## Principles and Mechanisms

In the analysis of time-to-event data with [competing risks](@entry_id:173277), a primary objective is often to understand and predict the occurrence of a specific type of event. Two distinct, yet related, quantities are central to this endeavor: the cause-specific hazard and the cumulative incidence function. The choice between these two quantities as the primary target of inference depends fundamentally on the scientific question being asked, leading to different modeling strategies with distinct principles and mechanisms.

### The Divergent Paths of Etiology and Prediction

The first approach focuses on the **cause-specific hazard (CSH)**, denoted $h_k(t)$. For a specific event of interest, cause $k$, the CSH is defined as the instantaneous rate of occurrence of this event at time $t$, conditional on the subject being event-free up to that point. Formally, for an event time $T$ and cause indicator $\Delta$,

$h_k(t) = \lim_{\Delta t \to 0} \frac{\mathbb{P}(t \le T < t+\Delta t, \Delta = k \mid T \ge t)}{\Delta t}$

The conditioning set, $\{T \ge t\}$, defines the **risk set** for the CSH. This set includes only those individuals who have not yet experienced an event of *any* kind. Subjects who experience a competing event are treated as censored at their event time and are removed from this risk set. Consequently, the CSH is ideal for addressing **etiologic** questions about the underlying biological or mechanical process of a specific failure type. It quantifies the instantaneous risk among a "pure" population of susceptible individuals, isolating the rate of the event of interest from the influence of other events [@problem_id:4975246] [@problem_id:4975279].

The second quantity is the **cumulative incidence function (CIF)**, denoted $F_k(t)$, which is the probability that an event of cause $k$ occurs by time $t$.

$F_k(t) = \mathbb{P}(T \le t, \Delta = k)$

Unlike the CSH, the CIF provides a measure of **absolute risk**. It answers a fundamentally **predictive** question: "What is the probability that a subject like this will experience event $k$ by a certain time?", fully accounting for the fact that some individuals will be removed from risk by competing events [@problem_id:4975246]. When a clinician wishes to prognosticate for a patient, the CIF is the relevant quantity [@problem_id:4975246] [@problem_id:4975257].

These two quantities are linked by a crucial relationship. The instantaneous change in the CIF is the product of the CSH and the overall survival probability, $S(t) = \mathbb{P}(T > t)$:

$\frac{d}{dt}F_k(t) = h_k(t) S(t)$

Integrating this relationship reveals the formula for the CIF:

$F_k(t) = \int_0^t h_k(u) S(u) du = \int_0^t h_k(u) \exp\left(-\sum_{j=1}^{K} \int_0^u h_j(v) dv\right) du$

This equation shows that the cumulative incidence of cause $k$ depends not only on its own cause-specific hazard, $h_k(t)$, but also on the cause-specific hazards of all competing events, which are embedded within the overall [survival function](@entry_id:267383) $S(t)$. A covariate's effect on $F_k(t)$ is therefore a complex interplay of its effects on all causes of failure. An intervention might increase the CSH for the event of interest but simultaneously increase the CSH for a competing event even more, thereby reducing the pool of subjects available to experience the event of interest and potentially *decreasing* the overall CIF [@problem_id:4975282]. This complexity motivates a modeling approach that targets the CIF directly.

### The Subdistribution Hazard: A Direct Route to Modeling the CIF

The Fine-Gray model provides a direct path to modeling the CIF by defining a new type of hazard function: the **subdistribution hazard (SDH)**. The goal is to construct a [hazard function](@entry_id:177479), let's call it $\gamma_k(t)$, that relates to the CIF, $F_k(t)$, in the same simple way that a standard hazard relates to a standard [survival function](@entry_id:267383). That is, we desire a relationship of the form:

$F_k(t) = 1 - \exp\left(-\int_0^t \gamma_k(u) du\right)$

From this desired relationship, the subdistribution hazard can be defined as:

$\gamma_k(t) = -\frac{d}{dt}\ln(1 - F_k(t)) = \frac{\frac{d}{dt} F_k(t)}{1 - F_k(t)}$

This definition reveals the essence of the SDH. It is the instantaneous rate of cause $k$ events, but the denominator is $1 - F_k(t)$, which is the probability of *not* having had the event of interest by time $t$. This leads to a profound change in the definition of the risk set [@problem_id:4975296].

The conditioning event "not having had event $k$ by time $t$" is the union of two [disjoint sets](@entry_id:154341): $\{T \ge t\}$ (being event-free) and $\{T < t, \Delta \ne k\}$ (having already experienced a competing event). This defines the **subdistribution risk set**. At any time $t$, this risk set contains all individuals who are still event-free *plus* all individuals who have previously failed from a competing cause. Individuals are only removed from this risk set when they experience the event of interest, cause $k$. This contrasts sharply with the CSH risk set, which removes individuals after any event [@problem_id:4975279] [@problem_id:4975162].

The formal definition of the subdistribution hazard is thus:

$\gamma_k(t) = \lim_{\Delta t \to 0} \frac{\mathbb{P}(T \in [t, t+\Delta t), \Delta = k \mid (T \ge t) \text{ or } (T < t, \Delta \ne k))}{\Delta t}$

In practice, this is operationalized with a modified at-risk indicator for each subject $i$. The indicator, $Y_i^*(t)$, is equal to 1 if subject $i$ is in the subdistribution risk set at time $t$, and 0 otherwise. This can be expressed as:

$Y_i^{*}(t) = I(T_i \ge t) + I(T_i < t, \Delta_i \ne k)$

where $I(\cdot)$ is the [indicator function](@entry_id:154167). This indicator ensures that a subject who experiences a competing event remains "at risk" for the subdistribution hazard of the event of interest, even though they cannot biologically experience it. This statistical device is what allows the model to directly target the population-level quantity $F_k(t)$ [@problem_id:4975221].

### The Fine-Gray Proportional Subdistribution Hazards Model

The Fine-Gray model imposes a [proportional hazards](@entry_id:166780) structure on the subdistribution hazard. For a vector of covariates $Z$, the model is specified as:

$\gamma_k(t \mid Z) = \gamma_{k,0}(t) \exp(\beta_k^T Z)$

Here, $\gamma_{k,0}(t)$ is the **baseline subdistribution hazard**, an unspecified non-negative function of time representing the SDH when $Z=0$. The vector $\beta_k$ contains the [regression coefficients](@entry_id:634860) [@problem_id:4975257].

The exponentiated coefficient, $\exp(\beta_{kj})$, is the **subdistribution hazard ratio (SHR)** associated with a one-unit increase in covariate $Z_j$. It quantifies the multiplicative effect of the covariate on the instantaneous rate of cause $k$ events *among all individuals who have not yet experienced cause k*. This interpretation differs crucially from that of a cause-specific hazard ratio (CSHR) from a standard Cox model. A CSHR quantifies the effect on the rate among only those who are completely event-free [@problem_id:4975162].

Because the Fine-Gray model is built directly upon the SDH, the estimated coefficients $\beta_k$ have a direct and monotonic impact on the CIF. A positive coefficient (SHR > 1) implies a higher CIF, while a negative coefficient (SHR < 1) implies a lower CIF. This direct link makes the Fine-Gray model an exceptionally powerful tool for prediction and prognostic modeling [@problem_id:4975282].

### Estimation and the Challenge of Censoring

Estimating the parameters of the Fine-Gray model is complicated by the presence of right-censoring, particularly due to the unique structure of the subdistribution risk set. If a subject is censored at time $t_c$, they are removed from follow-up. For a cause-specific model, this is straightforward. For the Fine-Gray model, however, that subject *should* have remained in the risk set for the event of interest if they were destined to experience a competing event at some time $t > t_c$. Since this is unobservable, a naive analysis would be biased.

The [standard solution](@entry_id:183092) is **Inverse Probability of Censoring Weighting (IPCW)**. The intuition is to use the individuals who remain under observation to represent those who were censored. Each subject's contribution to the analysis at time $t$ is up-weighted by the inverse of their probability of remaining uncensored up to that time. The weight for subject $i$ at time $t$ is:

$\hat{W}_i(t) = \frac{I(C_i \ge t)}{\hat{G}(t)}$

where $C_i$ is the censoring time for subject $i$, and $\hat{G}(t)$ is a consistent estimate (e.g., from a Kaplan-Meier estimator) of the censoring survival function $G(t) = P(C \ge t)$ [@problem_id:4975222].

For IPCW to produce consistent estimates, a critical assumption must hold: **conditional independent censoring**. This assumption states that, conditional on the measured covariates $Z$, the censoring time $C$ is independent of the failure time $T$ and cause $\Delta$. Formally:

$C \perp (T, \Delta) \mid Z$

This means that after accounting for the known covariates, the reason a subject is censored provides no additional information about their prognosis. If this assumption is violated (i.e., censoring is informative), for example, if sicker patients (who are at higher risk of an event) are also more likely to drop out of the study for reasons not captured in $Z$, then the weights will be incorrect. This systematically misweights contributions, leading to biased and inconsistent estimates of $\beta_k$ [@problem_id:4975309].

### Model Assumptions and Diagnostics

Like the Cox model, the Fine-Gray model rests on a key assumption: **proportional subdistribution hazards**. This means the SHR for a given covariate is constant over time. It is a crucial theoretical point that the proportional subdistribution hazards assumption and the proportional cause-specific hazards assumption are, for the same covariate and event, **mutually exclusive** except in trivial cases (e.g., no competing risks). Therefore, if a covariate has a proportional effect on the CSH, its effect on the SDH will be time-varying, and vice versa [@problem_id:4975171].

Assessing the proportionality assumption for a Fine-Gray model is therefore essential. Two practical methods are commonly used:

1.  **Graphical Diagnostics**: Under the proportional SDH assumption, the quantity $\log(-\log(1 - F_k(t)))$ should be linearly related to the log-cumulative baseline SDH, with a constant vertical shift between covariate groups. Therefore, plotting $\log(-\log(1 - \widehat{\text{CIF}}_k(t)))$ against time or log-time for each group should yield approximately parallel curves.

2.  **Formal Testing**: A formal test can be conducted by introducing a time-dependent interaction term into the model. For a covariate $Z_j$, one can add the term $Z_j \times g(t)$, where $g(t)$ is a function of time such as $\log(t)$ or $t$. A test of the null hypothesis that the coefficient for this interaction term is zero constitutes a test of the proportionality assumption. A significant result suggests the SHR is not constant over time [@problem_id:4975171].

It is also important not to confuse tests of proportionality with other tests, such as Gray's test for the equality of CIFs. Gray's test assesses the null hypothesis that the CIFs are identical across groups (i.e., $\beta_k=0$), not whether the [proportional hazards assumption](@entry_id:163597) holds when they differ [@problem_id:4975171].