## Introduction
Analyzing the time until an event occurs is a fundamental task in many scientific fields, from medicine and public health to engineering and economics. This type of data, known as time-to-event or survival data, is crucial for answering questions about prognosis, treatment efficacy, and reliability. However, analyzing this data presents a unique statistical challenge: observations are often incomplete. For many subjects, the study ends before the event of interest has happened, a phenomenon called censoring. This incomplete information makes standard analytical methods like linear regression inappropriate and biased, creating a significant knowledge gap for researchers who need to draw valid conclusions from longitudinal studies.

This article provides a comprehensive guide to understanding and analyzing time-to-event data. In the first chapter, "Principles and Mechanisms," we will establish the theoretical foundation, defining the structure of [censored data](@entry_id:173222) and introducing the core mathematical concepts of survival and hazard functions. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the broad utility of these methods across various disciplines and explore advanced models for handling complex scenarios like competing risks and recurrent events. Finally, the "Hands-On Practices" chapter will offer practical exercises to reinforce these concepts, equipping you with the tools to confidently tackle [time-to-event analysis](@entry_id:163785) in your own work.

## Principles and Mechanisms

In the analysis of time-to-event data, our primary objective is to understand the distribution of time until a specific event occurs. However, a unique challenge arises because we often cannot observe the event for every subject in our study. Instead, our observations are frequently incomplete. This chapter delineates the fundamental principles and mechanisms that govern the analysis of such data, providing a rigorous foundation for the statistical models that will be discussed subsequently.

### The Structure of Time-to-Event Data

Let $T$ be a non-negative random variable representing the true time from a defined origin until the occurrence of an event of interest. In an ideal scenario, we would observe $T_i$ for every subject $i$ in a study. In practice, follow-up may be terminated before the event is observed. This phenomenon is known as **right-censoring**.

Let $C_i$ be the time of censoring for subject $i$. We only observe the event if it occurs before or at the censoring time, i.e., if $T_i \le C_i$. If censoring occurs first, $C_i  T_i$, we only know that the event had not yet happened by the time the subject was lost to follow-up.

This observational mechanism yields a pair of variables for each subject: the observed follow-up time, $Y_i$, and an event indicator, $\Delta_i$. These are defined as:
- $Y_i = \min(T_i, C_i)$: The observed time, which is either the event time or the censoring time, whichever comes first.
- $\Delta_i = \mathbf{1}\{T_i \le C_i\}$: The event indicator, where $\Delta_i=1$ signifies that an event was observed at time $Y_i$, and $\Delta_i=0$ signifies that the observation was right-censored at time $Y_i$.

The full data for a subject $i$ in a typical study is therefore the triplet $(Y_i, \Delta_i, \mathbf{Z}_i)$, where $\mathbf{Z}_i$ is a vector of baseline covariates measured at the start of follow-up [@problem_id:4962156]. A valid statistical analysis must utilize the information contained in both the observed time $Y_i$ and the event indicator $\Delta_i$.

### A Taxonomy of Incomplete Data Mechanisms

While right-censoring is the most common form of incomplete data in survival analysis, it is essential to distinguish it from other mechanisms, as each implies a different kind of information about the unobserved event time $T$ [@problem_id:4962274].

- **Right-Censoring**: As described, an individual is observed to be event-free until a time $C$. The information we have is that the true event time is greater than or equal to the censoring time: $T \ge C$.

- **Left-Censoring**: This occurs when an individual is assessed at a time $L$ and is found to have already experienced the event. The exact event time is unknown, but we know it occurred before the assessment. The information we have is: $T \le L$.

- **Interval-Censoring**: This arises from periodic follow-up. If an individual is known to be event-free at an assessment at time $L$ but is found to have experienced the event by the next assessment at time $R$, the event time is known only to lie within that interval. A negative test at time $L$ implies $T  L$, and a positive test at time $R$ implies $T \le R$. The combined information is: $T \in (L, R]$.

These forms of censoring must be conceptually distinguished from **truncation**, which is a condition of the study sampling design itself.

- **Truncation**: This occurs when subjects are only included in the study if their event time falls within a specific window. For example, in a study with a sampling window of $(a, b]$, individuals are only enrolled if their event time $T$ falls in this interval. Any individual observed in the study is known to have $T \in (a, b]$, while individuals with event times outside this window are never part of the dataset. This differs from censoring, which applies to individuals who have already been enrolled in the study.

Finally, we must also distinguish these structured forms of incomplete data from general **missingness**, where a subject is enrolled in the study, but their event time information is simply not recorded for reasons that may or may not be systematic. Unlike censoring, missingness by itself does not necessarily impose a known inequality on the value of $T$.

### Fundamental Mathematical Quantities

To formalize the analysis of time-to-event data, we use several interrelated mathematical functions to characterize the distribution of the event time $T$.

- **Survival Function ($S(t)$)**: This is the probability that an individual survives, or remains event-free, beyond time $t$.
$$ S(t) = \mathbb{P}(T  t) $$
The survival function starts at $S(0) = 1$ and is a non-increasing function of $t$, approaching $0$ as $t \to \infty$.

- **Probability Density Function ($f(t)$)**: For a continuous event time $T$, the PDF represents the density of events at time $t$. It is related to the [survival function](@entry_id:267383) by $f(t) = -\frac{d}{dt} S(t)$.

- **Hazard Function ($\lambda(t)$)**: The hazard function, sometimes denoted $h(t)$, is arguably the most central concept in survival analysis. It represents the [instantaneous potential](@entry_id:264520) for an event to occur at time $t$, given that the individual has survived up to that time. Formally, it is defined as a limit:
$$ \lambda(t) = \lim_{\Delta t \to 0} \frac{\mathbb{P}(t \le T  t+\Delta t \mid T \ge t)}{\Delta t} $$
The [hazard function](@entry_id:177479) describes the evolving risk of the event over time. A rising hazard indicates increasing risk, while a falling hazard indicates decreasing risk.

These three functions are deterministically related. By expanding the [conditional probability](@entry_id:151013) in the definition of the [hazard function](@entry_id:177479), we can derive a fundamental relationship [@problem_id:4962102]:
$$ \lambda(t) = \frac{\lim_{\Delta t \to 0} \mathbb{P}(t \le T  t+\Delta t) / \Delta t}{\mathbb{P}(T \ge t)} = \frac{f(t)}{S(t)} $$
This shows that the [hazard rate](@entry_id:266388) is the event density at time $t$ scaled by the probability of having survived to be at risk at that time. Another useful relationship can be derived by noting that $f(t) = -S'(t)$:
$$ \lambda(t) = -\frac{S'(t)}{S(t)} = -\frac{d}{dt} \ln S(t) $$

- **Cumulative Hazard Function ($\Lambda(t)$)**: This function represents the total accumulated risk up to time $t$. It is defined as the integral of the [hazard function](@entry_id:177479):
$$ \Lambda(t) = \int_0^t \lambda(u) \, du $$
Integrating the expression $\lambda(t) = -\frac{d}{dt} \ln S(t)$ from $0$ to $t$ reveals a direct and powerful link between the cumulative hazard and survival functions [@problem_id:4962104]:
$$ \Lambda(t) = \int_0^t \left(-\frac{d}{du} \ln S(u)\right) \, du = -[\ln S(u)]_0^t = -(\ln S(t) - \ln S(0)) $$
Since $S(0) = \mathbb{P}(T  0) = 1$, we have $\ln S(0) = 0$. This yields the critical relationship:
$$ \Lambda(t) = -\ln S(t) \quad \text{or equivalently} \quad S(t) = \exp(-\Lambda(t)) $$
This equation demonstrates that knowing the hazard function (and thus the cumulative hazard) is equivalent to knowing the [survival function](@entry_id:267383).

### The Likelihood for Censored Data

A primary reason for the specialized methods of survival analysis is that standard statistical models, such as Gaussian linear regression, are inappropriate for time-to-event data [@problem_id:4962250]. There are three main reasons for this:
1.  **Censoring**: Simply discarding censored observations introduces severe selection bias, as subjects with longer event times are more likely to be censored and would be systematically excluded. Conversely, treating censoring times as event times systematically underestimates the true event times for censored subjects, biasing results.
2.  **Distributional Support**: Event times are non-negative, whereas the Gaussian distribution has support on the entire real line.
3.  **Distributional Shape**: Event time data are often strongly right-skewed, which violates the symmetry assumption of the Gaussian distribution.

The principled approach to inference for censored data is to construct a likelihood function that correctly reflects the information provided by each observation. The contribution of each subject to the total likelihood depends on whether their observation ended in an event or in censoring [@problem_id:4962156].

- For a subject $i$ with an **observed event** ($\Delta_i=1$), we know their event occurred precisely at time $Y_i$. Their contribution to the likelihood is the probability density at that time: $f(Y_i)$.
- For a subject $i$ who was **right-censored** ($\Delta_i=0$), we know their event occurred at some time *after* $Y_i$. Their contribution to the likelihood is the probability of this outcome: $\mathbb{P}(T_i  Y_i) = S(Y_i)$.

Combining these using the event indicator $\Delta_i$, the likelihood contribution for subject $i$ is:
$$ L_i(\theta) = [f(Y_i \mid \mathbf{Z}_i; \theta)]^{\Delta_i} [S(Y_i \mid \mathbf{Z}_i; \theta)]^{1-\Delta_i} $$
where $\theta$ represents the parameters of the model for the event time distribution. The total likelihood is the product of these individual contributions over all subjects. This likelihood function correctly uses the exact times for events and the lower bounds for censored times, providing a valid basis for estimation. An equivalent and often more convenient form can be expressed using the hazard and cumulative hazard functions:
$$ L_i(\theta) = [\lambda(Y_i \mid \mathbf{Z}_i; \theta)]^{\Delta_i} S(Y_i \mid \mathbf{Z}_i; \theta) = [\lambda(Y_i \mid \mathbf{Z}_i; \theta)]^{\Delta_i} \exp(-\Lambda(Y_i \mid \mathbf{Z}_i; \theta)) $$

### The Independent Censoring Assumption

The validity of the censored data likelihood described above hinges on a critical assumption known as **independent censoring** or **[non-informative censoring](@entry_id:170081)**. This assumption does not mean that the event time $T$ and censoring time $C$ are marginally independent. Rather, it states that, conditional on any measured covariates $\mathbf{Z}$, the event time and censoring time are independent [@problem_id:4962247]:
$$ T \perp C \mid \mathbf{Z} $$
Intuitively, this means that for a group of individuals with the same covariate values, the reason for censoring provides no extra information about their prognosis or risk of the event.

Under this assumption, the [joint likelihood](@entry_id:750952) for the parameters of the event distribution ($\theta$) and the censoring distribution ($\phi$) factorizes into two separate parts [@problem_id:4962167]:
$$ L(\theta, \phi) = L_T(\theta) \times L_C(\phi) $$
This factorization is profoundly important because it allows us to perform inference on the parameters of interest, $\theta$, by maximizing only the event-time portion of the likelihood, $L_T(\theta)$, without needing to specify or model the censoring mechanism.

When the independent censoring assumption is violated, censoring is said to be **informative**. This occurs when the reason for censoring is related to the risk of the event, even after accounting for covariates. For example, if a patient is withdrawn from a drug trial because their health is rapidly declining, their censoring is informative of an impending event. In such cases, the likelihood does not factorize, and standard methods will produce biased results. Principled analysis of informatively censored data requires advanced techniques that explicitly model the dependence between the event and censoring processes, such as inverse probability of censoring weighting (IPCW) or joint models [@problem_id:4962167].

### Modeling Time-to-Event Data: The Cox Model

With the principles of [censored data](@entry_id:173222) likelihood and independent censoring established, we can introduce models that relate covariates to event times. A key component of many such models is the **risk set**.

The risk set at time $t$, denoted $\mathcal{R}(t)$, is the set of all individuals who are under observation and have not yet experienced an event just prior to time $t$. For studies where all subjects enter at time 0, this is simply the set of subjects with observed times $Y_i \ge t$. In studies with **delayed entry**, where subject $i$ enters the study at time $L_i  0$, the definition must be more precise. A subject is in the risk set at time $t$ if they entered the study *before* $t$ and remained event-free and uncensored *at least until* $t$ [@problem_id:4962248]. Formally:
$$ \mathcal{R}(t) = \{i : L_i  t \le Y_i \} $$
For example, a subject who enters at $L=5$ is not in the risk set at $t=5$ (or any time prior), but is in the risk set at $t=6$ provided their follow-up extends to 6 or beyond. A subject censored at $Y=5$ is in the risk set just prior to $t=5$ but not at any time after 5.

The most widely used model in survival analysis is the **Cox Proportional Hazards (PH) model**. It is a [semi-parametric model](@entry_id:634042) that specifies the hazard for an individual with covariates $\mathbf{Z}$ as [@problem_id:4962101]:
$$ \lambda(t \mid \mathbf{Z}) = \lambda_0(t) \exp(\boldsymbol{\beta}^\top \mathbf{Z}) $$
The model has two components:
1.  $\lambda_0(t)$: An unspecified, non-parametric **baseline hazard function**. This is the [hazard function](@entry_id:177479) for an individual with covariates $\mathbf{Z} = \mathbf{0}$.
2.  $\exp(\boldsymbol{\beta}^\top \mathbf{Z})$: A parametric component where $\boldsymbol{\beta}$ is a vector of [regression coefficients](@entry_id:634860).

The key feature of the Cox model is the **[proportional hazards assumption](@entry_id:163597)**. The ratio of the hazards for two individuals with different covariate vectors, $\mathbf{Z}_1$ and $\mathbf{Z}_2$, is constant over time:
$$ \frac{\lambda(t \mid \mathbf{Z}_2)}{\lambda(t \mid \mathbf{Z}_1)} = \frac{\lambda_0(t) \exp(\boldsymbol{\beta}^\top \mathbf{Z}_2)}{\lambda_0(t) \exp(\boldsymbol{\beta}^\top \mathbf{Z}_1)} = \exp(\boldsymbol{\beta}^\top (\mathbf{Z}_2 - \mathbf{Z}_1)) $$
The term $\exp(\beta_j)$ for a single covariate $Z_j$ has a direct interpretation as the **hazard ratio (HR)**. It is the multiplicative factor by which the hazard changes for each one-unit increase in $Z_j$, holding all other covariates constant. Estimation of the $\boldsymbol{\beta}$ coefficients is achieved through a technique called partial likelihood, which cleverly uses the risk sets at each observed event time to construct a likelihood that is independent of the unknown baseline hazard $\lambda_0(t)$.

### Extension to Competing Risks

In many studies, subjects are at risk for more than one type of event, and the occurrence of one event type precludes the occurrence of others. This is the **competing risks** setting. For example, in a study of elderly patients, causes of death might include heart disease, cancer, or other causes.

Analyzing competing risks requires a careful distinction between two different modeling targets, which correspond to two different types of hazard functions [@problem_id:4962141]. Let $K$ be the cause of the event.

1.  **Cause-Specific Hazard ($\lambda_k(t)$)**: This is the instantaneous rate of an event of cause $k$ at time $t$, among those who are currently event-free.
    $$ \lambda_k(t) = \lim_{\Delta t \to 0} \frac{\mathbb{P}(t \le T  t+\Delta t, K=k \mid T \ge t)}{\Delta t} $$
    The risk set for $\lambda_k(t)$ consists of all subjects who have not yet experienced an event of *any* cause. Modeling the cause-specific hazard is appropriate for **etiologic questions**, where the goal is to understand the direct effect of a covariate on the rate of a specific disease process. In this analysis, events from competing causes are typically treated as right-censored observations.

2.  **Subdistribution Hazard ($\tilde{\lambda}_k(t)$)**: This hazard is constructed to directly model the **Cumulative Incidence Function (CIF)**, $F_k(t) = \mathbb{P}(T \le t, K=k)$, which represents the absolute risk of experiencing an event of cause $k$ by time $t$ in the presence of competing events. The subdistribution hazard is defined as:
    $$ \tilde{\lambda}_k(t) = \frac{dF_k(t)/dt}{1 - F_k(t)} = \frac{d}{dt} \{-\ln(1 - F_k(t))\} $$
    The "risk set" for this hazard is conceptually different: it includes individuals who are event-free *and* individuals who have already experienced a competing event. This is an artificial construct, but it provides a direct link to the CIF, making it the appropriate tool for **absolute risk prediction**.

The choice between modeling the cause-specific hazard and the subdistribution hazard is not a matter of correctness, but of aligning the statistical tool with the scientific question at hand: etiology versus prediction.