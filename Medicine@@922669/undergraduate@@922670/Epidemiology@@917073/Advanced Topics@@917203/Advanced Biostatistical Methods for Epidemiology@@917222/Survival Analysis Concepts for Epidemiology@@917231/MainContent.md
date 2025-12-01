## Introduction
In the field of epidemiology, many of the most critical questions revolve around time: How long until a disease develops after exposure? How long does a patient survive after diagnosis? What is the duration of recovery following an intervention? Answering these questions requires a specialized set of statistical tools known as survival analysis, or [time-to-event analysis](@entry_id:163785). Traditional statistical methods are ill-equipped to handle the unique challenges of this data, most notably the problem of incomplete observations, where we do not know the exact event time for every subject in a study. This article provides a comprehensive guide to understanding and applying the core concepts of survival analysis.

This article is structured to build your expertise progressively. In the first chapter, **"Principles and Mechanisms,"** we will lay the theoretical groundwork. You will learn about the fundamental nature of time-to-event data, including the crucial concepts of censoring and truncation, and become familiar with the key mathematical functions that describe survival. We will then explore the core methods for estimating survival from data, from the non-parametric Kaplan-Meier estimator to the powerful semi-parametric Cox proportional hazards model.

Next, in **"Applications and Interdisciplinary Connections,"** we will bridge the gap between theory and practice. This chapter demonstrates how survival analysis is used to answer real-world questions in clinical research and public health. You will learn to translate statistical outputs like hazard ratios into clinically meaningful measures of absolute risk, navigate complex scenarios involving time-varying exposures and [competing risks](@entry_id:173277), and recognize critical pitfalls like immortal time bias.

Finally, the **"Hands-On Practices"** section offers a chance to apply your knowledge through guided exercises, solidifying your understanding of key techniques like calculating survival curves and validating model assumptions. By the end of this journey, you will be equipped with the foundational knowledge to critically interpret and conduct survival analyses in epidemiological research.

## Principles and Mechanisms

Survival analysis, or [time-to-event analysis](@entry_id:163785), comprises a set of statistical methods for analyzing data where the outcome variable is the time until the occurrence of an event of interest. This field is indispensable in epidemiology, where research questions often concern the duration until disease onset, recovery, or death. Unlike other statistical domains, survival analysis is uniquely defined by its explicit handling of incomplete observations, a ubiquitous feature of longitudinal studies. This chapter delineates the foundational principles and core mechanisms of survival analysis, from fundamental quantities to the sophisticated models used in contemporary epidemiological research.

### The Nature of Time-to-Event Data: Censoring and Truncation

The primary variable in survival analysis is the event time, a non-negative random variable $T$ representing the duration from a well-defined time origin to the occurrence of a specific event. However, in most epidemiological studies, we cannot observe $T$ for all individuals. This incomplete observation arises primarily from two phenomena: censoring and truncation.

**Censoring** refers to a situation where the event time $T$ is only partially known for an individual who is part of the study sample. The information about their event time is limited to an interval. The most common form is **[right censoring](@entry_id:634946)**, which occurs when a subject's follow-up ends before the event has occurred. This may happen because the study concludes at a predetermined administrative end date, or because the subject is lost to follow-up for reasons unrelated to the event. If a subject's follow-up ends at time $C$, we only know that their true event time is greater than $C$, i.e., $T > C$. The subject still provides valuable information: they survived, event-free, for at least time $C$.

Other forms of censoring are also encountered. **Left censoring** occurs when the event is known to have occurred *before* a certain time, but the exact time is unknown. For instance, if a subject is first examined at time $L$ and found to already have a chronic condition, their time to onset $T$ is only known to be less than or equal to $L$, i.e., $T \le L$. **Interval censoring** occurs when an event is known to have happened within a specific time interval, but not precisely when. This is common in studies with periodic follow-up. If a subject is known to be event-free at an examination at time $L$ but has experienced the event by the next examination at time $R$, the information on their event time is restricted to the interval $(L, R]$, i.e., $L  T \le R$.

**Truncation**, in contrast, is a condition on sample selection itself, meaning that certain individuals are systematically excluded from the study based on their event time. Observers are effectively blind to truncated individuals. **Left truncation**, also known as delayed entry, is the most common form in cohort studies. It occurs when individuals can only be enrolled into the study at some time $E$ after the time origin, provided they are still event-free. For example, a study of mortality after age 65 can only include individuals who survive to age 65. Consequently, the entire sample is conditional on the fact that the event time $T$ is greater than or equal to the entry time $E$, i.e., $T \ge E$. **Right truncation** is less common but can occur in retrospective designs, such as disease registries. If a study includes only individuals whose event occurred before a specific landmark time $U$, then any individual for whom $T > U$ is systematically excluded, and the sample is restricted to those with $T \le U$.

It is crucial to distinguish these concepts: censoring pertains to the loss of information for individuals *included* in the study, while truncation pertains to a sampling mechanism that restricts who is *eligible* to be included in the first place [@problem_id:4640248].

### Key Functions for Describing Survival

To describe the distribution of event times, survival analysis utilizes three interrelated functions.

The **Survival Function**, $S(t)$, is the probability that an individual survives (i.e., remains event-free) beyond time $t$:
$$S(t) = \Pr(T > t)$$
By definition, $S(0) = 1$, and $S(t)$ is a non-increasing function of $t$. It provides a complete summary of the survival experience of a population.

The **Probability Density Function (PDF)**, $f(t)$, represents the unconditional probability of the event occurring per unit time at time $t$. It is the derivative of the cumulative distribution function $F(t) = 1 - S(t)$:
$$f(t) = \frac{d}{dt}F(t) = -S'(t)$$

The **Hazard Function**, $h(t)$, also known as the hazard rate or [instantaneous failure rate](@entry_id:171877), is the central quantity in much of survival modeling. It represents the [instantaneous potential](@entry_id:264520) for the event to occur at time $t$, conditional on survival up to that time:
$$h(t) = \lim_{\Delta t \to 0^+} \frac{\Pr(t \le T  t + \Delta t \mid T \ge t)}{\Delta t}$$
The [hazard function](@entry_id:177479) can be expressed in terms of the survival and density functions:
$$h(t) = \frac{f(t)}{S(t)}$$
Unlike a probability, the hazard is a rate and can take any non-negative value. It describes the dynamics of risk over time. Integrating the hazard function gives the **Cumulative Hazard Function**, $\Lambda(t) = \int_0^t h(u)du$, which represents the accumulated risk up to time $t$. The [survival function](@entry_id:267383) can be directly recovered from the cumulative hazard:
$$S(t) = \exp\big(-\Lambda(t)\big) = \exp\left(-\int_0^t h(u)du\right)$$
This relationship forms the basis of many modeling techniques.

### Estimating Survival from Data

#### The Risk Set

Before we can estimate survival functions, we must first identify who is eligible to experience an event at any given time. The **risk set** at time $t$, denoted $R(t)$, is the set of all individuals in the cohort who are under observation and have not yet experienced the event or been censored just prior to time $t$. In the presence of delayed entry (left truncation) with entry time $a_i$ and an observed follow-up time $y_i$ (which is either an event or censoring time), an individual $i$ is in the risk set $R(t)$ if and only if their entry time has passed and their follow-up time has not: $a_i \le t$ and $y_i \ge t$.

Consider a hypothetical cohort of 8 individuals with specified entry, event, and censoring times. At an event time of $t=4$ months, the risk set $R(4)$ would include an individual who entered at $t=0$ and had an event at $t=4$, another who entered at $t=2$ and was censored at $t=10$, and another who entered at $t=1$ and had an event at $t=6$. However, it would exclude an individual who entered at $t=5$, as they were not yet under observation [@problem_id:4640284]. The size of the risk set, $n_j = |R(t_j)|$, at each distinct event time $t_j$ is a fundamental component of both non-parametric and semi-parametric survival estimators.

#### Non-Parametric Estimation: The Kaplan-Meier Estimator

When we do not wish to make strong assumptions about the shape of the hazard or survival function, we can use a non-parametric approach. The most widely used method is the **Kaplan-Meier (KM) estimator**, also known as the [product-limit estimator](@entry_id:171437). The intuition behind the KM estimator is to break down survival over a long period into a series of conditional probabilities of surviving shorter intervals.

Let the distinct, ordered event times in the data be $t_1  t_2  \dots  t_D$. At each event time $t_j$, let $d_j$ be the number of individuals who experience the event and let $n_j$ be the size of the risk set just prior to $t_j$. The conditional probability of *failing* at time $t_j$, given survival up to that point, is estimated as $d_j/n_j$. The [conditional probability](@entry_id:151013) of *surviving* past $t_j$ is therefore estimated as $(1 - d_j/n_j)$. The Kaplan-Meier estimate of the [survival function](@entry_id:267383) at any time $t$ is the product of these conditional survival probabilities for all event times up to and including $t$:
$$\widehat{S}(t) = \prod_{j: t_j \le t} \left(1 - \frac{d_j}{n_j}\right)$$
The resulting survival curve is a step function that starts at 1 and drops only at the observed event times. For example, with a risk set of $n_1=20$ at the first event time $t_1=2$, where $d_1=3$ events occur, the survival estimate drops to $\widehat{S}(2) = 1 - 3/20 = 0.85$. If at the next event time $t_2=5$, the risk set size is $n_2=15$ and $d_2=4$ events occur, the survival estimate drops further to $\widehat{S}(5) = \widehat{S}(2) \times (1 - 4/15) = 0.85 \times (11/15) \approx 0.623$ [@problem_id:4640262].

To quantify the uncertainty of the KM estimate, we use **Greenwood's formula** for the variance, which is derived using the [delta method](@entry_id:276272):
$$\operatorname{Var}\{\widehat{S}(t)\} = [\widehat{S}(t)]^2 \sum_{j: t_j \le t} \frac{d_j}{n_j(n_j - d_j)}$$
This formula allows for the construction of pointwise confidence intervals for the survival curve.

#### Parametric Models

In some situations, it is advantageous to assume that the hazard function follows a specific mathematical form, defined by a small number of parameters. This is the basis of **parametric survival modeling**. Such models can be more efficient than [non-parametric methods](@entry_id:138925) if the assumed distribution is correct, and they allow for smooth estimates of the hazard and survival functions. A variety of parametric families are used in epidemiology, distinguished by the shapes of their hazard functions [@problem_id:4640235].

*   **Exponential Model**: Assumes a [constant hazard rate](@entry_id:271158), $h(t) = \lambda$. This "memoryless" property implies that the risk of the event is the same regardless of how long an individual has been event-free. Its survival function is $S(t) = \exp(-\lambda t)$.
*   **Weibull Model**: A flexible generalization of the exponential model with hazard function $h(t) = \lambda k t^{k-1}$. The shape parameter $k$ allows the hazard to be constant ($k=1$, reducing to exponential), decreasing ($0  k  1$, e.g., representing early failures or a "[burn-in](@entry_id:198459)" period), or increasing ($k > 1$, e.g., representing aging or wear-out).
*   **Gompertz Model**: Often used in demography, this model has an exponentially increasing or decreasing hazard, $h(t) = \lambda \exp(\gamma t)$. It is suitable for modeling phenomena where risk accelerates rapidly with age ($\gamma > 0$).
*   **Log-normal and Log-logistic Models**: These models exhibit non-monotonic hazard functions. The log-normal hazard starts at 0, increases to a peak, and then declines towards 0. The log-logistic hazard can be monotone decreasing or, for shape parameter $\alpha > 1$, can also be non-monotonic (increasing then decreasing). These are useful for modeling processes where risk first rises and then falls, such as mortality following a surgical procedure.

The choice of a parametric model imposes a strong assumption on the data, which should be justified by prior knowledge or assessed using goodness-of-fit diagnostics.

### Modeling Covariate Effects: The Cox Proportional Hazards Model

In epidemiology, a primary goal is often to assess how risk factors or exposures affect survival. The **Cox [proportional hazards model](@entry_id:171806)**, introduced by Sir David Cox in 1972, is the most widely used method for this purpose. It is a **semi-parametric** model, elegantly combining a non-parametric component for the underlying time trend with a parametric component for covariate effects.

The model assumes that the hazard function for an individual with a vector of covariates $X$ is given by:
$$h(t \mid X) = h_0(t) \exp(\beta^\top X)$$
Here, $h_0(t)$ is the **baseline [hazard function](@entry_id:177479)**, an unspecified non-negative function of time that describes the hazard for an individual with all covariates equal to zero ($X=\mathbf{0}$). The term $\exp(\beta^\top X)$ is the parametric part, where $\beta$ is a vector of [regression coefficients](@entry_id:634860). This model assumes **proportional hazards**, meaning that the covariates act multiplicatively on the baseline hazard. A key consequence is that the ratio of the hazards for two individuals, say with covariate vectors $X_1$ and $X_2$, is constant over time:
$$\frac{h(t \mid X_1)}{h(t \mid X_2)} = \frac{h_0(t) \exp(\beta^\top X_1)}{h_0(t) \exp(\beta^\top X_2)} = \exp\big(\beta^\top (X_1 - X_2)\big)$$
This ratio, the **hazard ratio (HR)**, depends only on the difference in covariates, not on time.

#### Estimation: The Partial Likelihood

The remarkable feature of the Cox model is that the coefficients $\beta$ can be estimated without having to specify or estimate the baseline hazard $h_0(t)$. This is achieved through the maximization of a **partial likelihood** function. The intuition is to consider, at each distinct event time $t_i$, the set of individuals at risk, $\mathcal{R}(t_i)$. Given that exactly one event occurred at this time among the individuals in $\mathcal{R}(t_i)$, we can compute the [conditional probability](@entry_id:151013) that the event happened to the specific individual $i$ who was observed to fail. This probability turns out to be independent of the baseline hazard $h_0(t_i)$, as it cancels from the numerator and denominator [@problem_id:4640216]:
$$\Pr(\text{individual } i \text{ fails} \mid \text{one failure in } \mathcal{R}(t_i)) = \frac{\exp(\beta^\top x_i)}{\sum_{j \in \mathcal{R}(t_i)} \exp(\beta^\top x_j)}$$
The partial likelihood is the product of these conditional probabilities over all observed event times. If we use $\delta_i=1$ to indicate that subject $i$ had an event and $\delta_i=0$ if they were censored, the [partial likelihood](@entry_id:165240) can be written as:
$$L(\beta) = \prod_{i=1}^{n} \left[ \frac{\exp(\beta^\top x_i)}{\sum_{j \in \mathcal{R}(t_i)} \exp(\beta^\top x_j)} \right]^{\delta_i}$$
Maximizing this function with respect to $\beta$ yields the maximum partial likelihood estimates, $\widehat{\beta}$.

#### Interpreting Hazard Ratios and the Challenge of Non-Collapsibility

The primary output of a Cox model is the set of estimated coefficients, which are typically exponentiated to yield hazard ratios, $\exp(\widehat{\beta}_k)$. Under ideal conditions (including correct model specification and no unmeasured confounding), the hazard ratio has a causal interpretation as the multiplicative effect of a one-unit change in covariate $X_k$ on the instantaneous event rate at any time $t$, among those still event-free and with identical values for all other covariates in the model [@problem_id:4640225]. It is a ratio of rates, not a ratio of cumulative risks or probabilities.

A subtle but critical property of the hazard ratio is its **non-collapsibility**. A statistical measure is collapsible if its marginal (crude) value in a population is a weighted average of its conditional (stratum-specific) values. The odds ratio and hazard ratio are non-collapsible, while the risk ratio and risk difference are collapsible. This means that even if a covariate $Z$ is a strong prognostic factor but is completely independent of an exposure $E$ (i.e., it is not a confounder), the marginal hazard ratio for $E$ will not be equal to the conditional hazard ratio for $E$ adjusted for $Z$. The marginal HR will typically be attenuated towards the null value of 1.

This phenomenon occurs because the composition of the risk sets changes over time. In a hypothetical scenario where a prognostic factor $Z$ doubles risk and an exposure $E$ triples it, the subgroup with both risk factors ($E=1, Z=1$) will experience events and drop out of the risk set faster than other subgroups. As time progresses, the exposed group ($E=1$) becomes increasingly composed of the more robust individuals (those with $Z=0$), while the unexposed group ($E=0$) retains a higher proportion of its high-risk members (those with $Z=1$). This differential change in the underlying risk profile of the groups being compared causes the marginal hazard ratio to change over time and differ from the constant conditional HR [@problem_id:4640225]. This is not a form of bias; it simply reflects the fact that marginal and conditional hazard ratios are different estimands. Because of this, it is considered good practice in observational studies to report both the conditional HR from a confounder-adjusted model and a complementary, collapsible measure of absolute effect, such as the difference in restricted mean survival time (RMST) [@problem_id:4640225].

#### Estimating Survival Curves from a Cox Model

Although the Cox model estimation procedure bypasses the baseline hazard, we can estimate it after obtaining $\widehat{\beta}$. The most common method is the **Breslow estimator** for the cumulative baseline hazard, $H_0(t) = \int_0^t h_0(u)du$. This estimator is derived by equating the observed number of events at each event time $t_j$ to the expected number predicted by the model [@problem_id:4640279]:
$$\widehat{H}_0(t) = \sum_{j: t_j \le t} \frac{d_j}{\sum_{k \in \mathcal{R}(t_j)} \exp(\widehat{\beta}^\top x_k)}$$
Once $\widehat{H}_0(t)$ is obtained, one can estimate the [survival function](@entry_id:267383) for any individual with a specific covariate profile $X_p$:
$$\widehat{S}(t \mid X_p) = \exp(-\widehat{H}_0(t) \exp(\widehat{\beta}^\top X_p))$$

### Advanced Concepts and Extensions

#### The Counting Process Framework

The theoretical underpinnings of modern survival analysis, especially for models with recurrent events or time-dependent covariates, are formalized using the **counting process framework**. In this approach, for each individual $i$, we define a **counting process** $N_i(t)$, which counts the number of events the individual has experienced by time $t$. For a single event, $N_i(t)$ is either 0 or 1. We also define the **at-risk process** $Y_i(t)$, which is an indicator variable that equals 1 if the individual is at risk at time $t$ (i.e., has entered the study and has not yet been censored or had the event) and 0 otherwise.

The [hazard function](@entry_id:177479) is replaced by the **intensity process**, $\lambda_i(t)$, where $\lambda_i(t)dt$ is the [conditional probability](@entry_id:151013) of an event occurring in the small interval $[t, t+dt)$, given the entire history of the process up to that point. The genius of this formulation is that the Cox model's intensity can be written compactly as:
$$\lambda_i(t) = Y_i(t) h_0(t) \exp\big(\beta^\top X_i(t)\big)$$
The inclusion of the $Y_i(t)$ term elegantly handles all issues of censoring and delayed entry, as the intensity is automatically zero for any individual not in the risk set. This framework provides a rigorous basis for deriving the statistical properties of survival estimators and for extending them to more complex [data structures](@entry_id:262134) [@problem_id:4640299].

#### Causal Inference and Time-Varying Covariates

In many epidemiological studies, covariates are not fixed at baseline but change over time. A crucial distinction must be made between **external** and **internal** time-dependent covariates [@problem_id:4640254].
*   An **external covariate** is one whose path over time is not influenced by the individual's unfolding event or treatment history. An example is ambient air pollution, which is determined by weather and emissions, not by an individual's health status. The coefficient for an external covariate in a Cox model can often be interpreted causally, assuming no unmeasured confounding.
*   An **internal covariate** is one whose path is itself part of the [stochastic process](@entry_id:159502) being studied, influenced by prior events or treatments. Examples include a biomarker like lung function, which can decline after a disease exacerbation, or the dose of a medication, which may be adjusted by a physician in response to the patient's condition.

Including internal covariates in a standard Cox model poses significant challenges for causal interpretation. Adjusting for an internal covariate that is a mediator on the causal pathway from an exposure to the event will block that pathway, yielding an estimate of the direct effect, not the total effect. More problematically, it can introduce severe bias. For example, if a treatment is given to sicker patients (confounding by indication), or if an unmeasured factor like frailty influences both the internal biomarker and the risk of the event, adjusting for the treatment or biomarker can induce a spurious association through a mechanism called collider-stratification bias. Estimating causal effects in the presence of time-dependent confounding requires advanced methods such as marginal structural models, which go beyond the scope of a standard Cox model.

#### Competing Risks

A final common complexity is the presence of **competing risks**, where an individual can experience one of several mutually exclusive event types, and the occurrence of one type of event precludes the occurrence of any other. For example, in a study of elderly patients, causes of death might be cardiovascular disease, cancer, or other causes.

In this setting, treating events from competing causes as simple censorings is incorrect and leads to biased results. Instead, we must use methods designed for [competing risks](@entry_id:173277). Two main approaches are used to characterize the risk of a specific cause, say cause $k$ [@problem_id:4640268]:

1.  **Cause-Specific Hazard ($h_k(t)$)**: This is the instantaneous rate of failure from cause $k$ among those who are still alive and at risk of all events.
    $$h_k(t) = \lim_{\Delta t \to 0} \frac{\Pr(t \le T  t + \Delta t, \text{cause}=k \mid T \ge t)}{\Delta t}$$
    Cause-specific hazards can be modeled using a standard Cox model, where events from competing causes are treated as censored. This approach is useful for etiological questions about the direct impact of a risk factor on the rate of a specific event type.

2.  **Cumulative Incidence Function (CIF) ($F_k(t)$)**: This is the [marginal probability](@entry_id:201078) of failing from cause $k$ by time $t$.
    $$F_k(t) = \Pr(T \le t, \text{cause}=k)$$
    The CIF is the most relevant quantity for prediction and assessing the absolute public health burden of a cause. It is crucially related to the cause-specific hazard and the *overall* survival from all causes, $S(t)$, by the integral:
    $$F_k(t) = \int_0^t S(u-) h_k(u) du$$
    This relationship highlights why simply using a Kaplan-Meier estimate for cause $k$ (by censoring other causes) is wrong; the KM method estimates $1 - \exp(-\int_0^t h_k(u)du)$, which ignores the fact that individuals must survive [competing risks](@entry_id:173277) (accounted for by the $S(u-)$ term) to be able to fail from cause $k$. For direct modeling of the CIF, methods based on the **subdistribution hazard** are used. The subdistribution hazard, $\tilde{h}_k(t)$, modifies the risk set by retaining individuals who have already failed from competing causes, allowing for a direct link to the CIF.

Understanding these distinctions is essential for conducting and interpreting survival analyses in the complex settings frequently encountered in epidemiological research.