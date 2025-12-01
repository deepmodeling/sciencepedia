## Introduction
In fields ranging from clinical medicine to evolutionary biology, understanding *when* an event occurs is as critical as knowing *if* it occurs. This is the domain of survival analysis, a powerful set of statistical tools designed to analyze time-to-event data. However, real-world data is rarely complete; studies end, and participants are lost to follow-up, creating a challenge known as censoring. Without the proper methods, researchers risk drawing biased and incorrect conclusions. This article provides a comprehensive guide to mastering two of the foundational tools in survival analysis: the Kaplan-Meier curve and the hazard function.

This journey is structured into three parts. First, the **Principles and Mechanisms** chapter will lay the theoretical groundwork, demystifying core concepts like survival functions, hazard rates, and the critical assumption of [non-informative censoring](@entry_id:170081). Next, the **Applications and Interdisciplinary Connections** chapter will showcase how these methods are applied in the real world, from interpreting clinical trial results and building prognostic models in radiomics to navigating complex pitfalls like competing risks and immortal time bias. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by working through practical examples. We begin by exploring the fundamental concepts that form the bedrock of all [time-to-event analysis](@entry_id:163785).

## Principles and Mechanisms

### Fundamental Concepts: Survival, Hazard, and Censoring

Survival analysis is the branch of statistics dedicated to analyzing the expected duration until one or more events happen. In radiomics, this typically involves modeling the time from a baseline imaging scan or the start of therapy to an outcome such as disease progression, recurrence, or death. Central to this field are three interconnected concepts: the survival function, the [hazard function](@entry_id:177479), and the handling of incomplete data through censoring.

#### The Survival Function: Quantifying the Probability of Being Event-Free

The primary object of interest in survival analysis is the **time-to-event**, a non-negative random variable denoted by $T$. The statistical properties of $T$ are described by several related functions. The **[cumulative distribution function](@entry_id:143135) (CDF)**, $F(t) = \mathbb{P}(T \le t)$, gives the probability that the event has occurred by time $t$. The corresponding **probability density function (PDF)** for a continuous time variable is $f(t) = \frac{d}{dt}F(t)$, representing the density of events at time $t$.

However, in survival analysis, it is often more intuitive to focus on the probability of *not* experiencing the event. This leads to the **[survival function](@entry_id:267383)**, denoted $S(t)$, which is defined as the probability that the time to event is greater than some time $t$:

$$ S(t) = \mathbb{P}(T > t) = 1 - F(t) $$

The survival function begins at $S(0) = 1$ (assuming no one has experienced the event at time zero) and is a non-increasing function that approaches $0$ as $t \to \infty$. It provides a complete characterization of the event time distribution.

#### The Hazard Function: Modeling Instantaneous Risk

While the survival function describes the cumulative probability of remaining event-free, the **[hazard function](@entry_id:177479)**, $h(t)$, provides a more dynamic view of risk. It quantifies the [instantaneous potential](@entry_id:264520) for an event to occur at time $t$, given that the individual has survived up to that moment. It can be thought of as the instantaneous event rate for an individual who is still at risk at time $t$.

To formalize this, consider the probability of an event occurring in a small interval $[t, t+\Delta t)$, conditional on survival up to time $t$. This is $\mathbb{P}(t \le T < t+\Delta t \mid T \ge t)$. To convert this probability into a rate, we divide by the interval width $\Delta t$. The instantaneous hazard is the limit of this rate as the interval becomes infinitesimally small [@problem_id:4805985]:

$$ h(t) = \lim_{\Delta t \to 0^+} \frac{\mathbb{P}(t \le T < t+\Delta t \mid T \ge t)}{\Delta t} $$

Using the definition of conditional probability, we can derive a fundamental relationship between the hazard, the PDF, and the [survival function](@entry_id:267383). The numerator $\mathbb{P}(t \le T < t+\Delta t)$ is approximately $f(t)\Delta t$ for small $\Delta t$, and the conditioning event $\mathbb{P}(T \ge t)$ is simply $S(t)$. This leads to the identity:

$$ h(t) = \frac{f(t)}{S(t)} $$

Since for a continuous variable $f(t) = -\frac{d}{dt}S(t)$, we can also write $h(t) = \frac{-S'(t)}{S(t)}$. This form reveals another powerful identity involving the natural logarithm [@problem_id:4805985]:

$$ h(t) = -\frac{d}{dt}\ln S(t) $$

This equation highlights that the hazard function describes the relative rate of decrease of the survival curve at time $t$. By integrating the [hazard function](@entry_id:177479), we obtain the **[cumulative hazard function](@entry_id:169734)**, $H(t) = \int_0^t h(u)du$. Rearranging and integrating the previous equation gives the crucial link from hazard back to survival:

$$ S(t) = \exp(-H(t)) $$

This exponential relationship underscores that the survival curve is an integral representation of the entire history of the [hazard function](@entry_id:177479) up to time $t$. As we will see, two populations can have vastly different temporal hazard profiles but, by coincidence, similar survival probabilities at certain time points.

#### The Challenge of Incomplete Data: Censoring and Truncation

A defining feature of survival data is that we rarely observe the event time for every individual in a study. Follow-up is finite. Patients may withdraw, be lost to follow-up, or the study may end before they experience the event. These situations lead to incomplete observations known as **censoring**.

The most common form is **[right censoring](@entry_id:634946)**. For a given subject, we only know that their true event time $T$ is greater than their last observed follow-up time. For instance, in a clinical trial following patients for up to $24$ months, a patient who completes the follow-up without an event is right-censored at $24$ months [@problem_id:4952891]. If another patient withdraws from the study at month $10$, their observation is right-censored at $10$ months. The observed data for each individual $i$ thus consists of a pair: the observed time $X_i = \min(T_i, C_i)$ and an event indicator $\Delta_i = \mathbf{1}\{T_i \le C_i\}$, where $C_i$ is the censoring time.

For survival estimation methods like the Kaplan-Meier estimator to be unbiased, a critical assumption must hold: censoring must be **non-informative** (or independent). This means that, conditional on all information gathered up to a time $t$, an individual being censored at that time provides no information about their risk of having the event in the future [@problem_id:4952891]. Formally, the strongest condition is that the true event time $T$ and the censoring time $C$ are stochastically independent random variables, written as $T \perp C$ [@problem_id:4562423]. A violation of this assumption introduces significant bias. For example, if sicker patients are more likely to be lost to follow-up, the remaining sample becomes progressively healthier. This leads to an artificially low event rate and a survival curve that overestimates the true survival of the original population [@problem_id:4952891].

Distinct from censoring is **left truncation**, or **delayed entry**. This occurs when subjects are not observed from time zero but instead enter the study at a later time $L_i > 0$. For instance, a radiomics study might only include patients after they receive a specific imaging scan, which may occur months after their initial diagnosis (time zero). The crucial feature of left truncation is that individuals who experience the event *before* their potential entry time ($T_i < L_i$) are never included in the study sample [@problem_id:4562399]. The analysis must therefore account for the fact that the observed sample is conditioned on survival up to at least the entry time. In the counting process framework of survival analysis, a subject's at-risk process, $Y_i(t)$, which indicates if they are under observation, is active only during the interval $[L_i, X_i]$. The risk set at any time $t$ correctly includes only those individuals who have already entered the study ($L_i \le t$) and have not yet been censored or experienced the event.

### Non-Parametric Estimation: The Kaplan-Meier Method

When we lack a theoretical basis to assume a specific probability distribution for the event times, we turn to [non-parametric methods](@entry_id:138925). The cornerstone of non-parametric survival estimation is the **Kaplan-Meier (KM) estimator**, also known as the [product-limit estimator](@entry_id:171437).

#### The Product-Limit Formula

The Kaplan-Meier estimator provides an estimate of the survival function $S(t)$ from censored time-to-event data. Its logic is most easily understood in a discrete-time setting, such as a study where patient status is assessed at scheduled follow-up visits [@problem_id:4562441].

Let $t_1, t_2, \dots, t_k$ be the distinct times at which events are observed. The probability of surviving past time $t_j$, given survival up to just before $t_j$, is the complement of the [conditional probability](@entry_id:151013) of experiencing the event at $t_j$. This [conditional probability](@entry_id:151013) is the **discrete hazard**, $p_j = \mathbb{P}(T=t_j \mid T \ge t_j)$. The overall [survival probability](@entry_id:137919) up to any time $t$ is the product of these conditional survival probabilities at all preceding event times.

The discrete hazard $p_j$ is estimated from the data as the number of events at time $t_j$, denoted $d_j$, divided by the number of individuals at risk (alive and under observation) just prior to $t_j$, denoted $n_j$. The Kaplan-Meier estimate of the [survival function](@entry_id:267383) is then:

$$ \hat{S}(t) = \prod_{j: t_j \le t} (1 - \hat{p}_j) = \prod_{j: t_j \le t} \left(1 - \frac{d_j}{n_j}\right) $$

Crucially, censored individuals contribute to the risk set $n_j$ at all event times prior to their censoring time. When a subject is censored, they are simply removed from the risk set for all subsequent time points.

Consider a radiomics study where events (progressions) are assessed at scheduled visits [@problem_id:4562441].
-   At the start, $n_1 = 100$ patients are at risk. At $t_1 = 3$ months, $d_1 = 10$ progressions occur.
-   Between $t_1$ and $t_2 = 6$ months, $5$ patients are censored. Thus, the number at risk for the $t_2$ visit is $n_2 = n_1 - d_1 - (\text{censored}) = 100 - 10 - 5 = 85$. At $t_2$, $d_2 = 12$ progressions occur.
-   Between $t_2$ and $t_3 = 9$ months, $2$ patients are censored. The number at risk for the $t_3$ visit is $n_3 = n_2 - d_2 - (\text{censored}) = 85 - 12 - 2 = 71$. At $t_3$, $d_3 = 8$ progressions occur.

The KM survival estimate at $t=9$ months is calculated as the product of surviving each interval:
$$ \hat{S}(9) = \left(1 - \frac{d_1}{n_1}\right) \times \left(1 - \frac{d_2}{n_2}\right) \times \left(1 - \frac{d_3}{n_3}\right) = \left(1 - \frac{10}{100}\right) \times \left(1 - \frac{12}{85}\right) \times \left(1 - \frac{8}{71}\right) $$
$$ \hat{S}(9) = (0.90) \times (0.8588) \times (0.8873) \approx 0.686 $$
This means the estimated probability of being progression-free at $9$ months is $68.6\%$.

#### Interpreting Kaplan-Meier Curves

The resulting KM estimate, $\hat{S}(t)$, is a right-continuous step function. It is constant between event times and drops vertically at each time an event occurs. The size of the drop at an event time depends on the number of events relative to the number of individuals at risk.

Two practical issues frequently arise in the interpretation of KM curves [@problem_id:4562416]:
1.  **Censoring of the Largest Observation:** If the largest observed time in the dataset, $t_{\max}$, corresponds to a censored observation, the KM curve does not drop at this time. It remains flat at its last computed value. Beyond $t_{\max}$, there are no individuals left in the risk set, so the [survival probability](@entry_id:137919) is not estimable from the data. The curve is conventionally considered undefined for $t > t_{\max}$. It is statistically incorrect to force the curve to drop to zero in this case.

2.  **Estimating Median Survival:** The [median survival time](@entry_id:634182) is the time point at which the [survival probability](@entry_id:137919) reaches $0.5$. It is estimated as the smallest time $\tilde{t}$ for which $\hat{S}(\tilde{t}) \le 0.5$. If the study ends or follow-up is too short, the KM curve may never drop to $0.5$. In this scenario, the median survival is **not reached** or **not estimable**. It is invalid to extrapolate the curve to estimate a median. The correct practice is to report that the median survival exceeds the maximum follow-up time (e.g., "median survival > 24 months") and to supplement the report with other metrics, such as the [survival probability](@entry_id:137919) at a fixed time point (e.g., the 2-year survival rate) or the Restricted Mean Survival Time (RMST).

### Advanced Topics and Complex Scenarios

While the Kaplan-Meier curve is a fundamental tool, a sophisticated analysis requires a deeper understanding of the underlying hazard dynamics, robust methods for comparing groups, and proper handling of complex event structures.

#### Hazard Function Dynamics: A Deeper Look at Risk

The Kaplan-Meier curve, which visualizes $S(t)$, provides an integrated, cumulative view of survival. However, it can sometimes obscure important temporal changes in the underlying risk, which are captured by the [hazard function](@entry_id:177479), $h(t)$.

Since $S(t) = \exp(-H(t))$, the cumulative hazard can be estimated directly from the KM curve as $\hat{H}(t) = -\ln(\hat{S}(t))$. By taking differences of $\hat{H}(t)$ across time intervals, we can approximate the average [hazard rate](@entry_id:266388) within those intervals. This can be critical for clinical decision-making. For example, in a [radiotherapy](@entry_id:150080) response monitoring study, identifying a period of sharply rising hazard could signal the ideal time to schedule adaptive interventions or intensified imaging [@problem_id:4562397]. If survival probabilities are $S(6)=0.88$ and $S(8)=0.80$, the approximate cumulative hazards are $H(6) \approx -\ln(0.88) = 0.128$ and $H(8) \approx -\ln(0.80) = 0.223$. The average hazard in the interval $(6, 8)$ weeks is approximately $\frac{0.223 - 0.128}{8-6} = 0.0475$ per week. Comparing this to other intervals reveals the dynamics of risk over time.

This distinction is especially important in cases of **non-proportional hazards**, where the ratio of hazards between two groups is not constant over time. Consider a radiomics study stratifying patients into a Radiomics-High and a Radiomics-Low group [@problem_id:4562474]. Analysis of piecewise hazard rates might reveal that the High-risk group has a very high initial hazard that then decreases over time (a "front-loaded" risk, perhaps from early aggressive disease). In contrast, the Low-risk group might have a low initial hazard that gradually increases (a "back-loaded" risk, from delayed progression). These two very different biological patterns could, by chance, lead to similar cumulative event counts and overlapping KM curves at a late time point (e.g., $24$ months). Inspecting the KM curves alone would miss this crucial difference in the timing of risk, whereas a direct analysis of the hazard functions reveals the distinct [failure mechanisms](@entry_id:184047).

#### Comparing Survival Distributions

A primary goal in many studies is to compare survival between two or more groups (e.g., treatment arms).

The most common method for this is the **log-rank test**. It is a non-parametric test of the null hypothesis that the survival functions of the groups are identical ($H_0: S_1(t) = S_2(t)$ for all $t$). The test statistic is constructed by comparing the observed number of events in each group at each event time to the number that would be expected under the null hypothesis. While the [log-rank test](@entry_id:168043) is always valid for testing this null hypothesis (assuming [non-informative censoring](@entry_id:170081)), its statistical power is greatest when the hazards are proportional. In the presence of non-[proportional hazards](@entry_id:166780), particularly **crossing hazards**, its power can be severely diminished. For instance, if a new radiomics-guided therapy carries a higher risk of early toxicity (higher initial hazard) but confers a long-term survival benefit (lower later hazard), the negative and positive differences in the log-rank statistic may cancel each other out, leading to a non-significant result even when a clinically meaningful difference exists [@problem_id:4562434].

An alternative, robust measure for comparing survival distributions, especially under non-proportional hazards, is the **Restricted Mean Survival Time (RMST)**. The RMST is defined up to a pre-specified time horizon $\tau$ as the area under the survival curve:

$$ \mu(\tau) = \int_0^\tau S(t) dt $$

It represents the average event-free time experienced by the group over the interval $[0, \tau]$. The comparison between two groups is then based on the difference in their RMST, $\Delta(\tau) = \mu_1(\tau) - \mu_2(\tau)$. This provides a single summary of the treatment effect that is easily interpretable (e.g., "a gain of 2 months in average progression-free survival over 24 months") and does not depend on the [proportional hazards assumption](@entry_id:163597) [@problem_id:4562434].

#### Competing Risks

In many clinical scenarios, subjects are at risk for more than one type of event, and the occurrence of one event type precludes the occurrence of another. This is the problem of **[competing risks](@entry_id:173277)**. For instance, when studying time to local cancer progression, a patient might die from treatment-related toxicity before any progression can be observed. This toxicity-related death is a competing risk for local progression [@problem_id:4562409].

A common but severe methodological error is to treat competing events as standard [right-censoring](@entry_id:164686) in a Kaplan-Meier analysis. This violates the [non-informative censoring](@entry_id:170081) assumption because the competing event (e.g., death) provides definitive information that the primary event (progression) can no longer occur. This practice leads to biased estimates. Specifically, the quantity $1 - \hat{S}_{KM}(t)$ will systematically overestimate the true probability of experiencing the event of interest in the real world [@problem_id:4952891], [@problem_id:4562409].

The correct approach is to estimate the **cause-specific cumulative incidence function (CIF)**, defined as $F_k(t) = \mathbb{P}(T \le t, \text{event type}=k)$. This function gives the probability of experiencing event type $k$ by time $t$ in the presence of all other competing events. It can be estimated non-parametrically using methods like the Aalen-Johansen estimator.

For regression modeling in the presence of [competing risks](@entry_id:173277), two primary strategies exist:
1.  **Cause-Specific Hazard Models:** A standard Cox proportional hazards model can be fit for the cause-specific hazard of the event of interest, treating all competing events as censored. This is valid for asking etiological questions about the direct effect of a covariate on the instantaneous rate of a specific event type.
2.  **Subdistribution Hazard Models:** The Fine-Gray model directly models the effect of covariates on the CIF. This is the preferred approach for building predictive models of an individual's cumulative risk of a specific event.

These concepts can be unified within a **multi-state model** framework, which conceptualizes the patient's journey as transitions between different states (e.g., 'healthy' -> 'progression', 'healthy' -> 'death from other causes'). This provides a coherent and flexible way to represent and analyze complex event histories [@problem_id:4562409].