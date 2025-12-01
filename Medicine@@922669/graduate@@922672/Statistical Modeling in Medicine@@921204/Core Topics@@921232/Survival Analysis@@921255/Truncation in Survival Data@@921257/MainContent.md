## Introduction
In the analysis of time-to-event data, the challenge of incomplete information is pervasive. While many researchers are familiar with censoring, a less understood but equally critical issue is **truncation**—a condition inherent in the study design that determines which subjects are eligible to be observed. Unlike censoring, where we have partial information about a sampled individual, truncation systematically excludes individuals from the sample altogether based on when their event occurs. Ignoring this selection mechanism can introduce profound bias, leading to incorrect conclusions about survival patterns and treatment effects.

This article provides a comprehensive guide to understanding and correctly handling truncation in survival data. It bridges the gap between the theoretical underpinnings of truncation and its practical consequences in research. By working through the material, you will gain the skills to identify, analyze, and interpret data subject to this common but complex form of incomplete observation.

The article is structured to build your expertise systematically. In the **"Principles and Mechanisms"** chapter, you will learn the fundamental distinction between truncation and censoring, the statistical theory for correcting truncation bias, and how standard methods like the Kaplan-Meier estimator and Cox model are adapted. You will also explore how mishandling truncation leads to critical errors like survivor bias and immortal time bias. The **"Applications and Interdisciplinary Connections"** chapter demonstrates how these principles are applied in epidemiology, causal inference, and other fields, highlighting the importance of study design and advanced modeling. Finally, the **"Hands-On Practices"** section will allow you to solidify your understanding by working through practical problems involving the construction of risk sets and the application of statistical tests to [truncated data](@entry_id:163004).

## Principles and Mechanisms

In the analysis of time-to-event data, our observations are often incomplete. While the previous chapter introduced [right censoring](@entry_id:634946) as a common form of incomplete observation, this chapter delves into a more fundamental data-generating mechanism known as **truncation**. Unlike censoring, which pertains to the partial observation of subjects already included in a study, truncation is a condition of the sampling design itself, determining which subjects are eligible for inclusion in the first place. Understanding truncation is critical, as failure to account for it leads to selection bias and incorrect inferences.

### The Fundamental Distinction: Truncation versus Censoring

To build a rigorous understanding, we must first clearly distinguish truncation from various forms of censoring. Censoring occurs when we have partial information about an individual's event time, but the individual is nonetheless part of our study sample. Truncation, in contrast, means that certain individuals are systematically excluded from the sample based on their event time, rendering them entirely unobserved. [@problem_id:4920645]

Let $T$ be the true time from a well-defined origin (e.g., disease diagnosis) to an event of interest.

**Censoring** refers to situations where the exact value of $T$ is unknown for an individual who has been sampled. Common types include:
- **Right Censoring**: The most frequent type, where observation of a subject ends at a time $C$ before the event has occurred. We only know that the true event time is greater than the censoring time, i.e., $T > C$. The observed data for such a subject are the follow-up time $C$ and an indicator that the event was not seen. Crucially, subjects with $T > C$ are represented in the sample and contribute information up to time $C$. [@problem_id:4858822]
- **Left Censoring**: The event is known to have occurred *before* a certain observation time $E$, but the exact time is unknown. All that is known is $T \le E$. This might occur, for example, if a patient's first diagnostic test for a chronic condition is positive, but the onset was at some unknown point in the past. [@problem_id:4858822]
- **Interval Censoring**: The event is known to have occurred within an interval $(L, R]$, but the exact time is not observed. This is common in studies with periodic assessments, where a subject might test negative at time $L$ and positive at a subsequent visit at time $R$. [@problem_id:4858822]

**Truncation**, on the other hand, is a condition on the sampling frame. It means that the sample is drawn not from the entire target population, but from a sub-population defined by the event time $T$ itself.

- **Left Truncation (Delayed Entry)**: A subject is included in the sample only if their event time occurs *at or after* a specific entry time, $L$. That is, the condition for observation is $T \ge L$. Individuals for whom $T  L$ are never observed and are absent from the dataset. This is a common feature of observational studies. For instance, in a hospital registry study where the time origin is disease onset, patients are enrolled upon their first visit to a specialty clinic. If a patient's entry time (time from onset to first visit) is $L_i$, they can only be enrolled if they are still event-free at that time. Patients who experienced the event before their first potential clinic visit are systematically excluded. [@problem_id:4578311] [@problem_id:4858822]

- **Right Truncation**: A subject is included in the sample only if their event time occurs *at or before* a specific time, $R$. The condition for observation is $T \le R$. This can occur in retrospective studies. For example, if researchers construct a cohort by reviewing records at a fixed date to identify all individuals who have experienced an event, subjects whose event times would have occurred after that date are systematically excluded. [@problem_id:4920645]

The critical difference is that censoring leads to ambiguity in the event time for an observed subject, whereas truncation leads to the complete absence of subjects who do not meet the sampling criteria.

### The Statistical Correction: Conditioning on Inclusion

Because truncation restricts the sample to a sub-population, all [statistical inference](@entry_id:172747) must account for this selection mechanism to avoid bias. The universal principle for correcting for truncation is to **condition the analysis on the event of being included in the sample**. This is achieved by adjusting the likelihood contribution of each subject. [@problem_id:4992402]

Let the event time $T$ follow a distribution with probability density function (PDF) $f(t|\theta)$ and survival function $S(t|\theta)$. The likelihood contribution for an individual is the [conditional probability](@entry_id:151013) of their observed outcome, given that they were eligible for inclusion.

For **left truncation** at time $L_i$ and potential **[right censoring](@entry_id:634946)** at time $C_i$, the observed data are the follow-up time $x_i = \min(T_i, C_i)$ and the event indicator $\Delta_i = \mathbf{1}\{T_i \le C_i\}$. A subject is included only if $T_i \ge L_i$. The probability of this inclusion event is $\mathbb{P}(T_i \ge L_i) = S(L_i|\theta)$. The likelihood contribution for subject $i$ is:

$$
L_i(\theta) = \mathbb{P}(\text{observation } i \mid T_i \ge L_i) = \frac{\mathbb{P}(\text{observation } i \text{ and } T_i \ge L_i)}{\mathbb{P}(T_i \ge L_i)}
$$

Since the observed time $x_i$ must be greater than or equal to $L_i$, the condition $T_i \ge L_i$ is implicit in the observation. The numerator is therefore the standard likelihood contribution for a right-censored observation, $f(x_i|\theta)^{\Delta_i}S(x_i|\theta)^{1-\Delta_i}$. The final likelihood contribution is thus:

$$
L_i(\theta) = \frac{f(x_i|\theta)^{\Delta_i}S(x_i|\theta)^{1-\Delta_i}}{S(L_i|\theta)}
$$

Notice that the denominator is the [survival function](@entry_id:267383) evaluated at the subject-specific entry time. This denominator corrects for the fact that subjects with earlier event times were less likely to be included.

For **right truncation** at time $R_i$, an event at time $t_i$ is observed only if $T_i \le R_i$. The probability of inclusion is $\mathbb{P}(T_i \le R_i) = F(R_i|\theta) = 1 - S(R_i|\theta)$, where $F$ is the cumulative distribution function. The likelihood contribution for an observed event at $t_i$ is:

$$
L_i(\theta) = \frac{f(t_i|\theta)}{F(R_i|\theta)}
$$

### Analysis of Left-Truncated Data: The Modified Risk Set

While the conditional likelihood provides the formal basis for [parametric modeling](@entry_id:192148), a more intuitive and broadly applicable adjustment is used in non-parametric and semi-parametric methods. This adjustment centers on the concept of the **risk set**.

In standard survival analysis, the risk set at time $t$, denoted $R(t)$, consists of all individuals who are under observation and have not yet experienced the event or been censored. For data with delayed entry (left truncation), this definition must be modified. An individual can only be at risk of an event at time $t$ if they have (1) already entered the study *before* time $t$, and (2) not yet experienced the event or censoring. [@problem_id:4576967]

Let $L_i$ be the entry time and $X_i$ be the observed event or censoring time for subject $i$. The correct definition of the at-risk indicator $Y_i(t)$ is $Y_i(t) = \mathbf{1}\{L_i  t \le X_i\}$. The risk set at time $t$ is therefore:

$$
R(t) = \{i : L_i  t \le X_i\}
$$

This modified definition of the risk set is the fundamental mechanism for handling left-[truncated data](@entry_id:163004) in most standard survival analysis procedures. [@problem_id:4989540]

#### The Kaplan-Meier Estimator with Delayed Entry

The Kaplan-Meier (or product-limit) estimator for the survival function, $\hat{S}(t)$, is calculated as a product of conditional survival probabilities at each event time. Its form remains unchanged, but the components are calculated using the modified risk set.

$$
\hat{S}(t) = \prod_{j: t_{(j)} \le t} \left(1 - \frac{d_j}{n_j}\right)
$$

Here, $t_{(j)}$ are the distinct event times, $d_j$ is the number of events at $t_{(j)}$, and $n_j$ is the size of the risk set at that time, $n_j = |R(t_{(j)})| = \sum_i \mathbf{1}\{L_i  t_{(j)} \le X_i\}$.

To illustrate, consider calculating $\hat{S}(18)$ using the data from a study with delayed entry, as in [@problem_id:4992399]. Let the data for 8 subjects be $(L_i, T_i, \delta_i)$: $(0, 6, 1)$, $(2, 14, 1)$, $(5, 10, 0)$, $(9, 20, 1)$, $(11, 26, 0)$, $(3, 18, 1)$, $(15, 22, 1)$, $(7, 12, 1)$. The event times $\le 18$ are $6, 12, 14, 18$.
- At event time $t=6$: Subjects 1, 2, 3, and 6 are at risk ($L_i  6$ and $T_i \ge 6$). So, $n_1=4, d_1=1$.
- At event time $t=12$: Subjects 2, 4, 5, 6, and 8 are at risk ($L_i  12$ and $T_i \ge 12$). So, $n_2=5, d_2=1$.
- At event time $t=14$: Subjects 2, 4, 5, and 6 are at risk. So, $n_3=4, d_3=1$.
- At event time $t=18$: Subjects 4, 5, 6, and 7 are at risk. So, $n_4=4, d_4=1$.

The estimate is $\hat{S}(18) = (1 - \frac{1}{4}) \times (1 - \frac{1}{5}) \times (1 - \frac{1}{4}) \times (1 - \frac{1}{4}) = \frac{3}{4} \times \frac{4}{5} \times \frac{3}{4} \times \frac{3}{4} = 0.3375$.

The same principle of modifying the risk set applies to non-parametric hypothesis tests like the **[log-rank test](@entry_id:168043)**, where the comparison of observed versus expected events in different groups is based on risk sets correctly defined to account for delayed entry. [@problem_id:4576967]

#### The Cox Proportional Hazards Model with Delayed Entry

The elegance of the risk set modification extends directly to [semi-parametric models](@entry_id:200031). The Cox [proportional hazards model](@entry_id:171806) relies on a **partial likelihood**, which is constructed from a series of probabilities at each event time, conditional on the risk set at that time. By simply using the modified risk set definition, $R(t) = \{i: L_i  t \le X_i\}$, the partial likelihood correctly handles delayed entry without any other change to the estimation procedure. This allows for consistent estimation of the hazard ratios, provided the underlying assumptions are met. [@problem_id:4992402]

### Theoretical Foundations and Key Assumptions

The validity of these methods relies on two crucial theoretical conditions related to the entry process. [@problem_id:4921566]

1.  **Support Condition**: For any time $t$ at which we wish to estimate the survival function or hazard, there must be a non-zero probability that individuals can be observed. This means the support of the distribution of entry times $L$ must overlap with the time interval of interest. Formally, for $S(t)$ to be identifiable, we must have $\mathbb{P}(L \le t)  0$. If all subjects enter after some time $t_0$, we can learn nothing about the survival distribution before $t_0$.

2.  **Independent Truncation**: The entry process must be "independent" of the event process in a specific sense. It is not required that $L$ and $T$ are unconditionally independent. Rather, the assumption is that, conditional on having survived up to a certain time, knowing the specific entry time provides no further information about the future risk of an event. Formally, for any entry time $\ell$ and any time $t \ge \ell$:
    $$ \mathbb{P}(T > t \mid L = \ell, T \ge \ell) = \mathbb{P}(T > t \mid T \ge \ell) $$
    This ensures that the hazard rate observable in the truncated sample is representative of the true population [hazard rate](@entry_id:266388). When this condition is violated (e.g., if sicker patients are referred to a specialty clinic earlier), the truncation is informative, and more advanced methods may be needed.

### Important Manifestations of Truncation in Study Design

The abstract concept of truncation manifests as concrete and critical forms of bias in epidemiological and clinical research.

#### Survivor Bias in Prevalent Cohorts and Length-Biased Sampling

A common source of left truncation is the use of **prevalent cohorts**—groups of individuals assembled based on their existing disease status at a single point in time. This contrasts with **incident (or inception) cohorts**, which enroll individuals at the time of disease onset. By definition, a prevalent cohort can only include individuals who have survived from their disease onset until the date of cohort assembly. This induces a form of selection bias known as **survivor bias**. [@problem_id:4578311]

In a special but important scenario where the disease is in a "steady state" (constant incidence and survival distribution over time), this survivor bias takes a specific form called **[length-biased sampling](@entry_id:264779)**. The probability of an individual being included in a cross-sectional sample of prevalent cases is proportional to their total survival duration, $T$. Individuals with longer survival times have a larger window of opportunity to be observed as a prevalent case. [@problem_id:4633366]

This leads to a distortion in the observed distribution of survival times. If the true [population density](@entry_id:138897) of survival time $T$ is $f(t)$ with mean $\mu = \mathbb{E}[T]$, the density of survival time among those sampled in the prevalent cohort, $g(t)$, is:
$$
g(t) = \frac{t f(t)}{\mu}
$$
A naive analysis of the total survival times from this prevalent cohort will produce a biased estimate of the mean survival. The expected value of survival time in the length-biased sample is:
$$
\mathbb{E}_g[T] = \frac{\mathbb{E}[T^2]}{\mathbb{E}[T]}
$$
Since $\mathbb{E}[T^2] = \text{Var}(T) + (\mathbb{E}[T])^2$, the biased mean is always greater than or equal to the true mean $\mathbb{E}[T]$. For an exponential survival distribution with rate $\theta$ (and true mean $1/\theta$), the length-biased mean is $2/\theta$, an inflation of 100%. [@problem_id:4633366] The correct analysis of such data requires treating it as left-truncated, using the delayed-entry methods described above.

#### Immortal Time Bias

A particularly pernicious form of bias related to the mishandling of delayed entry is **immortal time bias**. This bias arises in observational studies comparing outcomes for "treated" vs. "untreated" subjects, where treatment is initiated at some time $V  0$ after eligibility. A flawed analysis might classify a subject as "treated" from the time origin ($t=0$) but start counting events only after treatment initiation at $V$. In this setup, the person-time contributed by the subject during the interval $[0, V)$ is misclassified as "treated" person-time. Because the subject must, by definition, survive this period to receive treatment, this interval is "immortal"—no events can be counted for the treated group during this time. This artificially inflates the survival and deflates the hazard of the treated group, often creating a spurious appearance of treatment benefit. [@problem_id:4376903]

Correctly handling this situation requires recognizing that the subject is not yet treated in the interval $[0, V)$. Valid analytical approaches include treating treatment as a time-dependent covariate or using a delayed-entry approach where the treated subject enters the risk set for the treated group only at time $V$. Comparing a delayed-entry treated group to an untreated group with entry at $t=0$, however, introduces its own selection bias. Modern causal inference frameworks, such as marginal structural models or target trial emulation, provide rigorous solutions by ensuring a common time origin for all subjects and correctly accounting for treatment status as it evolves over time. [@problem_id:4376903]

### Model Diagnostics for Truncated Data

Even when left-[truncated data](@entry_id:163004) are modeled correctly, it remains essential to assess the [goodness-of-fit](@entry_id:176037) of the model. The standard suite of diagnostic tools for the Cox model, particularly those based on residuals, can be adapted for use with [truncated data](@entry_id:163004). The key is to consistently apply the principles of the counting process formulation. [@problem_id:4992412]

The **compensator** or cumulative hazard for subject $i$ must be integrated over their actual time at risk, from $L_i$ to $t$. The estimated cumulative hazard for subject $i$ at their observed time $\tilde{T}_i$ is:
$$
\hat{A}_i(\tilde{T}_i) = \left[ \hat{\Lambda}_0(\tilde{T}_i) - \hat{\Lambda}_0(L_i) \right]\exp\{\hat{\beta}^\top Z_i\}
$$
This quantity is the correctly defined **Cox-Snell residual**. If the model is correct, these residuals (paired with their event indicators $\Delta_i$) should behave like a censored sample from a standard [exponential distribution](@entry_id:273894). Plotting their estimated cumulative hazard should yield a straight line with a slope of 1 through the origin. [@problem_id:4992412]

The **martingale residual** is the difference between the observed number of events ($\Delta_i$) and the estimated cumulative hazard:
$$
\hat{M}_i = \Delta_i - \hat{A}_i(\tilde{T}_i) = \Delta_i - \left[ \hat{\Lambda}_0(\tilde{T}_i) - \hat{\Lambda}_0(L_i) \right]\exp\{\hat{\beta}^\top Z_i\}
$$
These residuals should have a mean near zero and can be plotted against covariates to detect model misspecification.

Finally, **Schoenfeld residuals**, which are used to check the [proportional hazards assumption](@entry_id:163597), remain valid as long as they are calculated using the properly defined risk sets $R(t) = \{i: L_i  t \le \tilde{T}_i\}$ at each event time. [@problem_id:4992412] The ability to adapt this full diagnostic toolkit demonstrates the robustness and coherence of the modern counting process approach to survival analysis in the face of complex data structures like truncation.