## Introduction
In fields from clinical research to public health, understanding the time until an event occurs—be it recovery from illness, equipment failure, or disease recurrence—is a fundamental goal. However, analyzing this "time-to-event" data presents a unique challenge: we often do not observe the event for every subject in our study. Participants may drop out, or the study may end before the event happens, leaving us with incomplete information known as censored data. Standard statistical methods are ill-equipped to handle this complexity, creating a knowledge gap that requires specialized techniques.

This article introduces the Kaplan-Meier estimator, a cornerstone of modern survival analysis, providing the tools to correctly interpret time-to-event data. Across three chapters, you will gain a robust understanding of this powerful method. First, "Principles and Mechanisms" will deconstruct the statistical theory behind the estimator, explaining how it handles censoring and its critical assumptions. Next, "Applications and Interdisciplinary Connections" will showcase the versatility of survival analysis through real-world examples in epidemiology, clinical trials, and even the social sciences. Finally, "Hands-On Practices" will allow you to apply your knowledge through guided exercises, solidifying your ability to calculate and interpret survival curves. We begin by exploring the foundational principles that make this method so essential.

## Principles and Mechanisms

This chapter delves into the foundational principles and statistical machinery of Kaplan-Meier estimation. We will deconstruct how time-to-event data are handled, build the Kaplan-Meier estimator from first principles, scrutinize its critical assumptions, and explore the interpretation of the resulting survival curves.

### The Challenge of Incomplete Data: Censoring and Truncation

In an ideal study, we would observe the exact time-to-event, $T$, for every participant. However, in practice, our observation of $T$ is often incomplete. This incompleteness arises primarily from two distinct phenomena: **censoring** and **truncation**. Understanding the difference is critical for the correct application and interpretation of survival analysis.

#### Censoring: Incomplete Observation of Follow-up

Censoring occurs when we have some information about an individual's event time, but we do not know it precisely. It is an issue of incomplete observation for individuals who are already part of the study cohort. There are three main types of censoring [@problem_id:4605640]:

*   **Right Censoring**: This is the most common form of censoring in prospective studies. It occurs when a participant's follow-up ends before the event of interest has been observed. We only know that their true event time $T$ is greater than their last observed time, or censoring time, $C$. So, we know $T > C$. This can happen for several reasons: the study concludes while the participant is still event-free (administrative censoring), the participant withdraws consent, or they are lost to follow-up for reasons unrelated to the outcome, such as moving away. For example, in a 24-month study of tuberculosis incidence, a participant who remains disease-free at the 24-month final visit is right-censored at 24 months.

*   **Left Censoring**: This occurs when the event is known to have happened *before* a certain observation time, but the exact time is unknown. We only know that $T \le C$. For instance, in a study measuring the age of varicella (chickenpox) infection, if a child's first assessment is at 18 months of age and they already have antibodies for the virus, their infection time is left-censored at 18 months. We know the infection occurred sometime between birth (time 0) and the 18-month visit.

*   **Interval Censoring**: This occurs when an event is known to have happened within a specific time interval, but the exact time is unknown. We know that the event time $T$ falls between two observation points, $a$ and $b$, such that $a  T \le b$. This is common in studies with periodic follow-up examinations. For example, in an HIV study with quarterly testing, if a participant tests negative at their 6-month visit but positive at their 12-month visit, their [seroconversion](@entry_id:195698) time is interval-censored in the window $(6, 12]$ months.

The Kaplan-Meier estimator is designed specifically to handle right-censored data. Methods for left- and interval-censored data are more complex and are beyond the scope of this chapter.

#### Truncation: A Condition for Study Inclusion

Truncation is fundamentally different from censoring. It is not an issue of incomplete observation for a participant already in the study; rather, it is a feature of the study design that dictates which individuals from a target population are included in the sample in the first place.

*   **Left Truncation (or Delayed Entry)**: This occurs in studies where individuals are not observed from a common time zero, but instead become eligible for recruitment at varying times after the process has started. An individual with an entry time $L_i$ is only included in the study if they are event-free at that time. Anyone who experienced the event before their potential entry time $L_i$ is simply not in the study sample. This means the sample is "truncated" on the left; it is conditional on survival up to the entry time. For example, a study of mortality after diagnosis that recruits patients from a hospital registry will only include patients who survived long enough to be diagnosed and entered into the registry. An individual who dies before diagnosis is not part of the sample. In this scenario, an individual who enters the study at time $L_i$ only begins to contribute to the at-risk population for times $t > L_i$ [@problem_id:4605673].

*   **Right Truncation**: This is less common but occurs in retrospective study designs where individuals are only included if their event has already occurred by a certain time. For example, if a study of a [genetic disease](@entry_id:273195) is based on a death registry compiled up to the year 2020, the study will only include individuals who died before 2020. Individuals who have the disease but are still alive in 2020 (i.e., their event time $T$ is after 2020) are "truncated" from the sample. This creates a sample that is conditioned on the event having occurred by the truncation time [@problem_id:4605673].

Censoring and truncation affect the analysis differently. A right-censored individual contributes information up to their censoring time. A left-truncated individual contributes no information before their entry time. A right-truncated individual is entirely absent from the dataset if their event time is too large. The standard Kaplan-Meier estimator can be adapted to correctly handle left truncation, as we will see.

### The Kaplan-Meier Estimator: A Product-Limit Formulation

The survival function $S(t) = \mathbb{P}(T > t)$ can be expressed as a product of conditional probabilities over a sequence of time points. For two time points $t_1  t_2$, the law of [conditional probability](@entry_id:151013) states:
$$ \mathbb{P}(T > t_2) = \mathbb{P}(T > t_2 | T > t_1) \times \mathbb{P}(T > t_1) $$
Extending this over all the distinct event times observed in a study, $t_{(1)}  t_{(2)}  \dots  t_{(m)}$, we can write the [survival function](@entry_id:267383) at time $t$ as:
$$ S(t) = \prod_{j: t_{(j)} \le t} \mathbb{P}(T > t_{(j)} | T > t_{(j-1)}) $$
Since no events are observed between event times, the probability of surviving through such an interval, given survival to its start, is 1. Therefore, the survival function is a step function that only changes value at the times when events occur.

The task of the Kaplan-Meier estimator is to provide a non-parametric estimate for each of these conditional probabilities using the observed data. The estimate for the probability of surviving past an event time $t_{(j)}$, given survival up to that point, is simply the proportion of those at risk who did not experience the event at that time. This requires a precise definition of the set of individuals "at risk."

### The Risk Set: The Foundation of Estimation

The **risk set** at time $t$, denoted $R(t)$, is the set of all individuals in the study who are under active follow-up and have not yet experienced the event just prior to time $t$. These are the individuals who are "at risk" of having the event at time $t$.

To be included in the risk set $R(t)$, an individual $j$ must satisfy two conditions, which elegantly incorporate both left truncation and [right censoring](@entry_id:634946). Let $L_j$ be the entry time (left-truncation time, where $L_j=0$ if entry is at baseline) and $X_j = \min(T_j, C_j)$ be the observed follow-up time (either event or censoring). An individual $j$ is in the risk set at time $t$ if and only if they have already entered the study and are still under follow-up [@problem_id:4605676]:
$$ R(t) = \{j : L_j \le t \text{ and } X_j \ge t\} $$
The number of individuals in the risk set at an event time $t_{(j)}$ is denoted $n_j = |R(t_{(j)})|$. The number of individuals who experience the event at time $t_{(j)}$ is denoted $d_j$.

The empirical estimate of the conditional probability of surviving past $t_{(j)}$ is then $(n_j - d_j) / n_j$. This brings us to the **Kaplan-Meier product-limit formula**:
$$ \hat{S}(t) = \prod_{j: t_{(j)} \le t} \left(1 - \frac{d_j}{n_j}\right) $$
By convention, $\hat{S}(0)=1$. The resulting function, $\hat{S}(t)$, is a right-continuous step function. At each event time $t_{(j)}$, the curve drops. Between event times, it remains flat. At a censoring time, no event occurs, so the survival estimate does not change; however, the censored individual is removed from the risk set for all subsequent time points, affecting the denominator $n_k$ for all $k > j$.

To illustrate, consider the following data from a cohort study with staggered entry (left truncation) [@problem_id:4605676]:
*   Subject 1: Enters at $L_1=0$, event at $T_1=3.0$.
*   Subject 2: Enters at $L_2=0$, censored at $C_2=2.5$.
*   Subject 3: Enters at $L_3=1.0$, event at $T_3=4.0$.
*   Subject 4: Enters at $L_4=1.5$, event at $T_4=2.0$.
*   Subject 5: Enters at $L_5=0$, censored at $C_5=2.0$.

The ordered distinct event times are $t_{(1)}=2.0$, $t_{(2)}=3.0$, and $t_{(3)}=4.0$.
*   **At $t_{(1)}=2.0$**: The event is for subject 4. To find the risk set $R(2.0)$, we identify subjects with $L_j \le 2.0$ and $X_j \ge 2.0$. These are subjects 1 ($L=0, X=3.0$), 2 ($L=0, X=2.5$), 3 ($L=1.0, X=4.0$), 4 ($L=1.5, X=2.0$), and 5 ($L=0, X=2.0$). Thus, $n_1=5$. Here, we have $d_1=1$. The survival estimate becomes $\hat{S}(2.0) = 1 \times (1 - 1/5) = 0.8$.
*   **At $t_{(2)}=3.0$**: The event is for subject 1. To find $R(3.0)$, we seek subjects with $L_j \le 3.0$ and $X_j \ge 3.0$. Subjects 2, 4, and 5 have been removed from risk (due to censoring or event before 3.0). Subjects 1 and 3 remain at risk. $n_2=2$, $d_2=1$. The survival estimate becomes $\hat{S}(3.0) = \hat{S}(2.0) \times (1 - 1/2) = 0.8 \times 0.5 = 0.4$.

This step-by-step process, which can be fully specified as an algorithm [@problem_id:4605643], allows us to estimate the entire survival curve without making assumptions about its underlying shape.

### The Critical Assumption of Non-Informative Censoring

The validity of the Kaplan-Meier estimator hinges on a crucial assumption: **[non-informative censoring](@entry_id:170081)**. In simple terms, this means that the act of being censored is not related to an individual's prognosis or underlying risk of the event. At any point in time, individuals who are censored should be representative of those who remain at risk, with respect to their future event probability.

When this assumption is violated, censoring is said to be **informative** or **dependent**, and the Kaplan-Meier estimator will be biased [@problem_id:4605658]. Consider a clinical trial for a new cancer therapy. If patients whose health is rapidly declining are withdrawn from the study to receive palliative care, their censoring is informative. They are censored *because* they are at a very high risk of the event (death). Removing these high-risk individuals from the risk set leaves behind a "healthier" group. The estimator, based on this artificially healthy sample, will observe fewer events than would have occurred in the original cohort, leading to an **overestimation of survival**. The estimated KM curve will be biased upwards, lying above the true survival curve [@problem_id:4605658].

Conversely, [non-informative censoring](@entry_id:170081) includes:
*   **Administrative censoring**: The study ends on a predetermined date. This date is external and unrelated to any single participant's health status.
*   **Loss to follow-up for unrelated reasons**: A participant moves to another country for a new job.

Even administrative censoring can be subtly compromised. If patients with a worse prognosis tend to enroll in the study later, their administrative censoring times (time from their enrollment to the fixed study end date) will be shorter. This induces a [statistical dependence](@entry_id:267552) between a short survival time $T$ and a short censoring time $C$, violating the assumption [@problem_id:4605658].

More formally, using the language of [counting processes](@entry_id:260664), the [non-informative censoring](@entry_id:170081) assumption means that the instantaneous hazard of the event, given the entire history of the process up to time $t$, depends only on an individual's baseline characteristics and not on the censoring mechanism. Let $T$ be the event time, $C$ the censoring time, and $Z$ a vector of baseline covariates. The assumption is that $T$ and $C$ are independent, conditional on $Z$. In terms of stochastic processes, the intensity (instantaneous hazard) of the failure process at time $t$, $\lambda_T(t)$, given the history $\mathcal{F}_{t-}$, depends only on information available at baseline, $\mathcal{F}_0 = \sigma(Z)$. The full history of who else was censored or had an event provides no additional information about the individual's risk [@problem_id:4605700].

### Interpreting Kaplan-Meier Curves

Once estimated, the Kaplan-Meier curve is a rich source of information about survival patterns.

#### Median Survival Time

A common summary statistic is the **[median survival time](@entry_id:634182)**: the time point at which the survival probability is 0.5. Since the KM curve is a step function, this is defined precisely as the smallest time $t$ at which the survival curve drops to or below 0.5. Formally, $m = \inf\{t: \hat{S}(t) \le 0.5\}$. The use of the [infimum](@entry_id:140118) (greatest lower bound) ensures that the median is always uniquely defined [@problem_id:4605697].

*   If the curve jumps from above 0.5 to below 0.5 at an event time $t_j$, the [median survival time](@entry_id:634182) is exactly $t_j$.
*   If the curve drops to exactly 0.5 at time $a$ and remains flat for an interval $[a, b)$, the [median survival time](@entry_id:634182) is $a$.
*   If the curve does not drop to 0.5 by the end of the follow-up period (often due to heavy censoring or low event rates), the median is not reached. It is reported as being greater than the longest follow-up time in the study.

#### Comparing Survival Between Groups

A primary use of Kaplan-Meier analysis is to compare survival experiences between two or more groups (e.g., a treatment group and a control group).

Visually, if the curve for group A is consistently above the curve for group B, this suggests that group A has better survival. A formal statistical comparison is performed using the **log-rank test**. The null hypothesis ($H_0$) of the [log-rank test](@entry_id:168043) is that the survival distributions in the populations from which the groups were drawn are identical. That is, $H_0: S_1(t) = S_2(t)$ for all $t \ge 0$. This is mathematically equivalent to stating that their hazard functions are identical: $H_0: h_1(t) = h_2(t)$ for all $t \ge 0$ [@problem_id:2410286].

A crucial concept when comparing curves is the **proportional hazards (PH) assumption**. This assumption states that the hazard ratio between two groups is constant over time: $h_1(t) / h_2(t) = \lambda$. Under this assumption, the survival functions are related by $S_1(t) = [S_2(t)]^\lambda$. A key consequence of this relationship is that if the hazard ratio $\lambda \ne 1$, the survival curves cannot cross. Therefore, observing Kaplan-Meier curves that cross is strong visual evidence of **non-[proportional hazards](@entry_id:166780)** [@problem_id:4605644]. This implies that the relative effect of the group exposure (e.g., treatment benefit or harm) changes over time. When curves cross, the log-rank test can lose statistical power, as a beneficial effect in an early period may be cancelled out by a harmful effect in a later period [@problem_id:4605644]. A useful graphical diagnostic for the PH assumption is a "log-log" plot of $\log(-\log \hat{S}(t))$ versus $\log(t)$, where parallel curves support the assumption.

### Relationship to the Actuarial Method

The Kaplan-Meier estimator is closely related to the older **actuarial life-table estimator**. The actuarial method also estimates survival as a product of conditional probabilities, but it first groups the data into fixed time intervals (e.g., 1-year intervals). It then estimates an average conditional [survival probability](@entry_id:137919) for each interval, typically assuming that censoring occurs uniformly within the interval.

This grouping introduces a classic **bias-variance trade-off** [@problem_id:4605650]. By smoothing over intervals, the actuarial method can produce an estimate with lower variance (a smoother curve) than the Kaplan-Meier estimator. However, this comes at the cost of bias, as the assumption of uniform censoring and event risk within a wide interval may not hold. If censoring is concentrated early in an interval, for example, the actuarial method will tend to overestimate survival for that interval [@problem_id:4605650].

The Kaplan-Meier estimator can be seen as the logical endpoint of the actuarial method. As the width of the time intervals in the actuarial method shrinks towards zero, the estimator converges to the Kaplan-Meier estimator [@problem_id:4605650]. For this reason, when exact event and censoring times are available, the Kaplan-Meier method is preferred as it avoids the grouping bias inherent in the life-table approach.