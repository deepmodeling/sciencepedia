## Introduction
Survival analysis is a vital branch of statistics, offering powerful tools to analyze the duration until an event of interest occurs. In disciplines ranging from clinical medicine to engineering, understanding 'time-to-event' data is crucial for assessing prognosis, evaluating treatments, and predicting reliability. However, the unique nature of this data presents a significant analytical challenge: observations are often incomplete. Studies conclude, participants withdraw, or are lost to follow-up, resulting in 'censored' data where the true event time is unknown. Ignoring or mishandling censoring leads to biased results and incorrect conclusions.

This article provides a comprehensive guide to the foundational structures of survival data, demystifying the concepts of event times and censoring.
-   In the first chapter, **Principles and Mechanisms**, we will dissect the core [data structures](@entry_id:262134), explore the different types of censoring and truncation, and construct the statistical likelihood that forms the basis of all survival models.
-   Next, in **Applications and Interdisciplinary Connections**, we will see how these principles are applied to solve real-world problems in medicine, public health, and data science, extending to advanced topics like competing risks and multi-state models.
-   Finally, **Hands-On Practices** will offer practical exercises to build and test your skills in analyzing time-to-event data.

We begin by exploring the fundamental principles and mechanisms that govern the structure of all survival data.

## Principles and Mechanisms

Survival analysis is a collection of statistical procedures for which the outcome variable of interest is the time until an event occurs. Having introduced the fundamental motivations for this field, we now turn to the principles and mechanisms that govern the structure of survival data. Understanding these [data structures](@entry_id:262134) is a prerequisite for the valid application of survival models, as the unique characteristics of time-to-event data—chiefly the presence of incomplete observations—demand specialized analytical techniques.

### The Fundamental Data Structure of Time-to-Event Observations

At the heart of survival analysis lies a distinction between the quantity we wish to study and the quantity we are able to observe. For each individual $i$ in a study, there exists a **latent event time**, denoted as $T_i$, which is a non-negative random variable representing the duration from a well-defined time origin (e.g., diagnosis, enrollment, or birth) to the occurrence of a specific event of interest (e.g., death, disease relapse, or recovery).

In an ideal world, we would observe $T_i$ for every individual. In practice, our observation is often cut short. This may happen because a participant withdraws from the study, is lost to follow-up, or because the study concludes before the event has occurred for them. This phenomenon is known as **censoring**. We can conceptualize a second latent random variable for each individual, the **censoring time** $C_i$, which represents the time from the same origin until the individual is censored.

For any given individual, we can only observe one of these two outcomes: either the event occurs while they are under observation, or they are censored first. Consequently, the actual recorded time for individual $i$, which we will denote as $Y_i$, is the minimum of the true event time and the censoring time. This relationship is fundamental to all survival data [@problem_id:4551017]:

$Y_i = \min(T_i, C_i)$

This observed time $Y_i$ alone is insufficient for analysis. We must also know *why* the observation ended. Did the event occur, or was the individual censored? This is captured by a binary **event indicator**, $\delta_i$. The indicator takes the value $1$ if the event was observed and $0$ if the observation was censored. Formally, it is defined as:

$\delta_i = \mathbb{I}(T_i \le C_i)$

where $\mathbb{I}(\cdot)$ is the indicator function. If $\delta_i=1$, the event occurred and $Y_i = T_i$. If $\delta_i=0$, the observation was censored and $Y_i = C_i$; in this case, we only know that the true event time $T_i$ is some value greater than $Y_i$.

Together, the triplet of the observed time $Y_i$, the event indicator $\delta_i$, and a vector of baseline covariates $X_i$ (such as demographic information or clinical measurements) form the basic unit of data, $(Y_i, \delta_i, X_i)$, for each individual in a survival study [@problem_id:4550963].

### A Taxonomy of Incomplete Observations

The formulation $Y_i = \min(T_i, C_i)$ describes what is known as **[right censoring](@entry_id:634946)**. It is the most common form of incomplete data in medical research, where we know that an individual's true event time is "to the right of" their last follow-up time on a timeline. However, other mechanisms of incomplete observation exist and are crucial to recognize.

**Left Censoring:** In some scenarios, the event of interest has already occurred before the first observation. For an individual first assessed at time $C$, a positive finding means we only know that the event time $T$ occurred at some point before $C$. The information we have is that $T \le C$, or that $T$ lies in the interval $(0, C]$. A classic example arises in studies of perinatal HIV infection, where the time origin is birth. If an infant's first test at age $C$ weeks is positive, the infection time $T$ is left-censored, as it could have occurred anytime between birth and the test [@problem_id:4985890].

**Interval Censoring:** This type of censoring occurs when we cannot pinpoint the event time but can only determine that it happened within a specific time interval. This is common in studies with periodic follow-up assessments. For instance, in a study of HIV [seroconversion](@entry_id:195698) with routine testing, a participant might test negative at time $L$ and subsequently test positive at time $R$. We then know that the [seroconversion](@entry_id:195698) event $T$ occurred in the interval $(L, R]$. Similarly, in a study of Human Papillomavirus (HPV) clearance, a positive test at time $L$ followed by a negative test at time $R$ implies that the clearance event occurred between these two assessments [@problem_id:4985890].

Each of these censoring types imparts different information about the latent event time $T$ and requires a specific mathematical formulation to be correctly incorporated into a statistical model.

### The Likelihood Function for Censored Data

The primary tool for incorporating censored data into a statistical model is the likelihood function. The likelihood contribution of each individual is the probability of observing their specific data, given a model for the event time distribution. Let us denote the probability density function (PDF) of the event time $T$ as $f_T(t; \theta)$ and the [survival function](@entry_id:267383) as $S_T(t; \theta) = \mathbb{P}(T > t)$, where $\theta$ is a vector of model parameters.

For an individual $i$ with observed data $(Y_i, \delta_i)$:

*   If the event is observed ($\delta_i=1$), the time $Y_i$ is the exact event time $T_i$. The probability of an event occurring in a small interval around $Y_i$ is proportional to the PDF, so the likelihood contribution is $f_T(Y_i; \theta)$.

*   If the observation is right-censored ($\delta_i=0$), we only know that the event time $T_i$ is greater than the observed time $Y_i$. The probability of this is, by definition, the [survival function](@entry_id:267383) evaluated at $Y_i$. The likelihood contribution is therefore $S_T(Y_i; \theta)$.

We can write a single elegant expression for the likelihood contribution of subject $i$ that covers both cases [@problem_id:4550963]:

$L_i(\theta) = [f_T(Y_i; \theta)]^{\delta_i} [S_T(Y_i; \theta)]^{1-\delta_i}$

The total likelihood for a sample of $n$ independent individuals is the product of their individual contributions, $L(\theta) = \prod_{i=1}^n L_i(\theta)$.

For other censoring types, the likelihood contribution is derived from the probability of the observed interval [@problem_id:4985890]:

*   For a **left-censored** observation $T \le C$, the contribution is $\mathbb{P}(T \le C) = F_T(C; \theta) = 1 - S_T(C; \theta)$.
*   For an **interval-censored** observation $L  T \le R$, the contribution is $\mathbb{P}(L  T \le R) = S_T(L; \theta) - S_T(R; \theta)$.

#### The Crucial Assumption of Non-Informative Censoring

The validity of this likelihood construction hinges on a critical assumption: **[non-informative censoring](@entry_id:170081)**. Intuitively, this means that the mechanism of censoring provides no extra information about an individual's risk of failure, beyond what is already contained in their measured covariates. For example, if patients who are becoming sicker are more likely to drop out of a study, their censoring is "informative" because it is related to their prognosis. This would violate the assumption. In contrast, censoring due to the administrative end of a study is typically non-informative [@problem_id:4985818].

Formally, [non-informative censoring](@entry_id:170081) is defined as the [conditional independence](@entry_id:262650) of the true event time $T$ and the censoring time $C$, given the covariates $X$:

$T \perp C \mid X$

This assumption has a profound theoretical consequence. If the event time process depends on parameters $\theta$ and the censoring process depends on a distinct set of parameters $\psi$, the independence assumption allows the full likelihood to be factorized into two separate parts [@problem_id:4985903]:

$L(\theta, \psi) = \left( \prod_{i=1}^n [f_T(Y_i; \theta)]^{\delta_i} [S_T(Y_i; \theta)]^{1-\delta_i} \right) \times \left( \prod_{i=1}^n [f_C(Y_i; \psi)]^{1-\delta_i} [S_C(Y_i; \psi)]^{\delta_i} \right)$

$L(\theta, \psi) = L_T(\theta) \times L_C(\psi)$

Because the part of the likelihood involving the event parameters, $L_T(\theta)$, is separate from the part involving the censoring parameters, $L_C(\psi)$, we can perform valid [statistical inference](@entry_id:172747) for $\theta$ (e.g., finding the maximum likelihood estimate) using only $L_T(\theta)$ and without needing to specify a model for the censoring process. This powerful result is what allows methods like Cox [proportional hazards](@entry_id:166780) regression to be applied without modeling the distribution of censoring times, provided censoring is non-informative [@problem_id:4551017].

A common and important scenario where [non-informative censoring](@entry_id:170081) is plausible by design is administrative censoring in a study with a fixed end date. Consider a study that ends at a fixed calendar time $\tau$. If participants enter at different calendar times $E_i$, their potential censoring time is $C_i = \tau - E_i$. If the entry time $E_i$ is independent of the underlying event time $T_i$ (e.g., in a randomized trial where enrollment is not related to prognosis), then $C_i$ will also be independent of $T_i$. Even if entry time is correlated with prognosis, conditioning on covariates that capture this relationship (like enrollment year) can often restore the conditional independence required for the assumption to hold [@problem_id:4985816] [@problem_id:4985818].

### Data Structures for Complex Study Designs

#### Left Truncation (Delayed Entry)

It is critical to distinguish censoring from **truncation**. Censoring is a property of an observation on a sampled individual, whereas truncation is a property of the sampling process itself. **Left truncation**, also known as delayed entry, occurs when individuals are only included in the study if they are event-free at their time of entry. For example, a hospital-based registry studying time-to-stroke from symptom onset might only enroll patients who are referred from clinics, meaning they must have survived without a stroke from onset until referral [@problem_id:4985815].

If an individual has an entry time $L_i$, they are only observed if their true event time $T_i$ is greater than $L_i$. This conditioning event, $T_i > L_i$, must be accounted for in the analysis. It changes the support of the observed event times to $(L_i, \infty)$ and modifies the distribution functions. For an observed individual, the conditional survival function for $t > L_i$ becomes:

$S_{T \mid T>L_i}(t) = \mathbb{P}(T_i > t \mid T_i > L_i) = \frac{\mathbb{P}(T_i > t)}{\mathbb{P}(T_i > L_i)} = \frac{S_T(t)}{S_T(L_i)}$

A remarkable consequence is that the conditional hazard function for $t > L_i$ remains unchanged:

$\lambda_{T \mid T>L_i}(t) = \frac{f_{T \mid T>L_i}(t)}{S_{T \mid T>L_i}(t)} = \frac{f_T(t) / S_T(L_i)}{S_T(t) / S_T(L_i)} = \frac{f_T(t)}{S_T(t)} = \lambda_T(t)$

This means that for an individual who has survived to entry time $L_i$, their instantaneous risk of failure thereafter is the same as for an individual from the untruncated population. This property is what allows standard hazard-based models like the Cox model to be adapted for left-[truncated data](@entry_id:163004) [@problem_id:4985815].

#### The Risk Set and Counting Process Notation

Hazard-based models are built upon the concept of the **risk set**. At any point in time $t$, the risk set, denoted $\mathcal{R}(t)$, is the set of all individuals who are currently under observation and "at risk" of experiencing the event. In the counting process formulation of survival analysis, this is formalized using an **at-risk indicator process**, $Y_i(t)$, which is a binary function equal to $1$ if individual $i$ is in the risk set at time $t$, and $0$ otherwise.

The definition of $Y_i(t)$ depends on the study design. For a simple cohort study with entry at time $0$ and observed [exit time](@entry_id:190603) $X_i$ (due to event or [right censoring](@entry_id:634946)), an individual is at risk from the start until their exit. Thus, $Y_i(t) = \mathbb{I}(t \le X_i)$.

When left truncation is present, the structure becomes more complex. An individual $i$ with entry time $L_i$ and [exit time](@entry_id:190603) $X_i$ is only at risk during the interval $(L_i, X_i]$. The strict inequality on the left is a standard convention ensuring that individuals are not considered at risk at the exact moment of entry. The corresponding at-risk indicator is [@problem_id:4985887] [@problem_id:4985815]:

$Y_i(t) = \mathbb{I}(L_i  t \le X_i)$

And the risk set is $\mathcal{R}(t) = \{i : Y_i(t) = 1\}$.

To solidify these concepts, let us consider a concrete dataset from a hypothetical study with both left truncation and [right censoring](@entry_id:634946) [@problem_id:4985935]. The data for 8 patients include entry time ($A_i$), [exit time](@entry_id:190603) ($X_i$), and an event indicator ($\Delta_i=1$ for event, $0$ for censored). The distinct event times are $t_{(1)}=3$, $t_{(2)}=6$, and $t_{(3)}=9$. We can construct the number of failures ($d_k$) and the risk set ($R_k$) at each of these times.

*   **At $t_{(1)}=3$:**
    *   Failures: Patient 1 had an event at $X_1=3$. So, $d_1 = 1$.
    *   Risk Set $R_1 = \{i : A_i  3 \text{ and } X_i \ge 3\}$: Patients 1, 2, 3, 4, and 7 satisfy this, so the risk set is $\{1, 2, 3, 4, 7\}$ and its size is $n_1=5$.

*   **At $t_{(2)}=6$:**
    *   Failures: Patients 3 and 4 had events at $X_3=6, X_4=6$. So, $d_2 = 2$.
    *   Risk Set $R_2 = \{i : A_i  6 \text{ and } X_i \ge 6\}$: Patients 3, 4, 5, and 7 satisfy this. Note that patient 2 was censored at $X_2=5$ and is no longer at risk. Patient 6 entered at $A_6=6$, so they are not yet in the risk set. The risk set is $\{3, 4, 5, 7\}$ and its size is $n_2=4$.

*   **At $t_{(3)}=9$:**
    *   Failures: Patients 6 and 8 had events at $X_6=9, X_8=9$. So, $d_3 = 2$.
    *   Risk Set $R_3 = \{i : A_i  9 \text{ and } X_i \ge 9\}$: Patients 6, 7, and 8 satisfy this. The risk set is $\{6, 7, 8\}$ and its size is $n_3=3$.

This careful construction of risk sets, which correctly accounts for who has entered and not yet exited the study, is the foundation for [non-parametric methods](@entry_id:138925) like the Kaplan-Meier estimator and semi-parametric methods like the Cox model when applied to complex observational data.

### A Practical Complication: Tied Event Times

The standard derivation of the Cox [partial likelihood](@entry_id:165240) assumes that event times are continuous, implying that the probability of two individuals experiencing an event at the exact same time is zero. However, in practice, event times are often recorded on a discrete scale (e.g., in days, weeks, or months). For example, in a study tracking postoperative atrial fibrillation with daily assessments, it is common for multiple patients to be recorded as having an event on the same day [@problem_id:4985871].

This phenomenon, known as **tied event times** or simply **ties**, violates the "single failure" assumption underlying the simplest form of the [partial likelihood](@entry_id:165240). When $d_k > 1$ individuals fail at time $t_{(k)}$, the probabilistic question is no longer "which single individual from the risk set failed?" but rather "which specific group of $d_k$ individuals from the risk set failed?".

The mathematical formulation must be adjusted to reflect the [combinatorial probability](@entry_id:166528) of observing that specific set of $d_k$ failures from the $n_k$ individuals at risk. The no-tie likelihood formula is no longer valid, and its naive use can lead to biased results. Several methods, such as the Breslow, Efron, and exact discrete-time likelihoods, have been developed to handle ties. The choice among them depends on the frequency of ties and computational considerations, a topic that will be explored in subsequent chapters. The key principle remains that the presence of ties fundamentally alters the structure of the data and necessitates a modification to the analytical machinery.