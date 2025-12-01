## Introduction
In the quantitative health sciences, one of the most fundamental tasks is to measure how often new cases of a disease or health event arise in a population. This measure, known as incidence, is the bedrock upon which epidemiology is built. The most direct and intuitive way to quantify incidence is through the **incidence proportion**, a measure commonly referred to as **risk**. Understanding risk allows us to move from simply observing disease to quantifying its likelihood, comparing its occurrence between groups, and evaluating the effectiveness of interventions aimed at preventing it.

However, accurately measuring risk is more complex than it first appears. The simple formula of 'new cases divided by population size' quickly breaks down when faced with the realities of research: participants drop out, some are immune, and people can experience competing events like death from other causes. This article addresses this knowledge gap by systematically building the concept of risk from the ground up.

First, in **Principles and Mechanisms**, we will establish the rigorous definition of incidence proportion, explore its probabilistic foundations, and detail the necessary adjustments for real-world complexities like incomplete follow-up and competing risks. Next, **Applications and Interdisciplinary Connections** will demonstrate how this measure is used across clinical medicine and public health to compare risks, evaluate treatments, and inform causal reasoning. Finally, **Hands-On Practices** will provide opportunities to apply these concepts, solidifying your understanding through practical problem-solving. By navigating these chapters, you will gain a robust and applicable understanding of one of epidemiology's most vital tools.

## Principles and Mechanisms

This chapter delves into the principles and mechanisms that govern the measurement of disease occurrence, focusing on the concept of **incidence proportion** as a direct measure of **risk**. We will begin by establishing a rigorous definition under idealized conditions and progressively introduce the complexities encountered in real-world epidemiological studies, such as incomplete follow-up and competing events, detailing the theoretical and practical adjustments required to maintain conceptual and statistical validity.

### Defining Incidence Proportion as a Measure of Risk

In epidemiology, one of our primary goals is to quantify the occurrence of new health-related events in a population over a specified period. The most direct measure of the average individual probability of an event is the **incidence proportion ($IP$)**, also commonly referred to as **cumulative incidence** or simply **risk**.

Under a set of ideal conditions, the incidence proportion is straightforwardly defined. Consider a fixed group of individuals, known as a **closed cohort**, assembled at a baseline time, $t=0$. The fundamental definition of the incidence proportion over a follow-up period of duration $t$ is the ratio of new cases of the event that develop during this period to the number of individuals who were initially susceptible to the event at the beginning of the period. Formally, we write this as:

$IP(t) = \frac{\text{Number of new cases of the event in the interval } [0, t]}{\text{Number of individuals at risk at baseline } (t=0)}$

For this seemingly simple ratio to be a well-defined probability representing the risk of the event, several strict conditions must be met [@problem_id:4599567]. These are:
1.  **A Closed Cohort**: The group under study must be fixed. No new individuals may enter the cohort after the baseline time $t=0$.
2.  **A Well-Defined Population at Risk**: Every individual included in the denominator must be susceptible to developing the event of interest at the start of the study. This means individuals who already have the disease (prevalent cases) or who are immune must be excluded.
3.  **A Fixed Time Horizon**: The follow-up period, $t$, must be fixed and uniform for all individuals for the risk to be clearly interpretable over that specific duration.
4.  **Complete Ascertainment of Outcomes**: To accurately count the number of new cases in the numerator, the outcome status of every single member of the initial cohort must be known at the end of the follow-up period $t$. This implies no loss to follow-up or other forms of data censoring before the end of the specified interval.

When these conditions hold, $IP(t)$ is a dimensionless quantity ranging from $0$ to $1$, and it can be directly interpreted as the average probability that a member of that cohort will develop the outcome by time $t$.

### The Probabilistic Foundation and Properties of Risk

The epidemiological definition of incidence proportion has a rigorous foundation in probability theory. We can conceptualize the time to the occurrence of a health event for an individual as a non-negative random variable, which we denote as $T$. In this framework, the incidence proportion, $IP(t)$, is precisely the **[cumulative distribution function](@entry_id:143135) (CDF)** of this event-time random variable, evaluated at time $t$ [@problem_id:4599612].

$IP(t) = \mathbb{P}(T \le t)$

This probabilistic definition reveals fundamental properties of risk. One of the most important is **[monotonicity](@entry_id:143760)**. For an irreversible event, if an individual has experienced the event by an earlier time $t_1$, they have logically also experienced it by any later time $t_2 > t_1$. In set-theoretic terms, the event $\{T \le t_1\}$ is a subset of the event $\{T \le t_2\}$. A basic axiom of probability states that if an event $A$ is a subset of an event $B$, then $\mathbb{P}(A) \le \mathbb{P}(B)$. Consequently, for any two time points $t_1  t_2$, it must be that:

$IP(t_1) \le IP(t_2)$

This means that risk, as measured by incidence proportion for an irreversible event, can only stay the same or increase over time; it cannot decrease. A report claiming, for instance, that the 3-month risk of a chronic disease was $0.18$ and the 6-month risk was $0.14$ in the same closed cohort with complete follow-up would represent a logical impossibility, as it would imply that the event $\{T \le 3 \text{ months}\} \cap \{T > 6 \text{ months}\}$ occurred with positive probability, which is a contradiction [@problem_id:4599550]. An alternative way to see this is by decomposing the risk at time $t_2$:

$IP(t_2) = \mathbb{P}(T \le t_2) = \mathbb{P}(T \le t_1) + \mathbb{P}(t_1  T \le t_2) = IP(t_1) + \mathbb{P}(\text{event occurs between } t_1 \text{ and } t_2)$

Since probabilities cannot be negative, $IP(t_2)$ must be greater than or equal to $IP(t_1)$.

### Constructing the Population at Risk

The denominator of the incidence proportion formula, the **population at risk**, requires careful definition. It is not necessarily the total number of individuals in a workplace or community but specifically those who are biologically susceptible to becoming a new case of the disease. Proper construction of this risk set is critical for an accurate estimation of risk.

Consider a study to determine the 2-year risk of first-ever acute appendicitis in a cohort of $1,200$ employees [@problem_id:4599586]. To define the baseline population at risk, we must systematically exclude individuals who cannot become an *incident case*:
-   **Immune or Not Susceptible Individuals**: Those who have had a prior appendectomy have no appendix and are biologically incapable of developing appendicitis. They must be excluded.
-   **Prevalent Cases**: Individuals who are currently hospitalized with acute appendicitis at baseline ($t=0$) are existing cases, not new ones. They are not at risk of *developing* the condition during follow-up and must be excluded.
-   **Individuals with a Prior History (for first-ever events)**: If the outcome of interest is the *first* occurrence of an event, then individuals with a documented history of that event (e.g., a prior episode of appendicitis treated non-operatively) must also be excluded from the risk set.

In the example from [@problem_id:4599586], if there were $90$ employees with prior appendectomies, $10$ with prevalent appendicitis, and $25$ with a prior history, the correct denominator would be $1,200 - 90 - 10 - 25 = 1,075$. The 2-year risk would then be the number of new cases observed during the 2 years divided by this carefully constructed risk set of $1,075$. A comorbidity, such as Irritable Bowel Syndrome, that does not confer immunity would not be grounds for exclusion.

### Distinguishing Risk from Rate: The Role of Person-Time

A common point of confusion in epidemiology is the distinction between risk (incidence proportion) and rate. The **incidence rate ($IR$)**, also known as incidence density, measures the speed at which new events occur, while risk measures the probability of an event occurring over a defined period.

The crucial difference lies in the denominator and the type of population each measure is suited for [@problem_id:4599580].
-   **Incidence Proportion (Risk)** is calculated with a denominator that is a count of *people* at risk at the start of a period. It is dimensionless, a probability, and ideally suited for a closed cohort with complete follow-up.
-   **Incidence Rate** is calculated with a denominator that is the sum of the time each individual was followed while at risk, a quantity known as **person-time**. It has units of time$^{-1}$ (e.g., cases per person-year), is not a probability, and is not bounded by $1$. It is the natural measure for **dynamic or open populations**, where individuals may enter or leave over time.

For example, in a closed cohort of $1,800$ workers followed for $3$ years, where $162$ develop a disease, the $3$-year risk is $IP(3) = 162/1,800 = 0.09$, or $9\%$. In contrast, in a dynamic city population where $180$ cases occur over $27,000$ person-years of observation, the incidence rate is $IR = 180 / 27,000 = 0.0067 \text{ cases per person-year}$. These two numbers, $0.09$ and $0.0067$, measure different things and are not directly comparable without transformation.

### Addressing Real-World Complexities I: Incomplete Follow-Up and Censoring

The ideal of a closed cohort with complete follow-up is rare. In practice, participants may be lost to follow-up (e.g., move away), withdraw from the study, or the study may end before they have an event. This phenomenon is called **[right censoring](@entry_id:634946)**.

When censoring occurs, the naive incidence proportion formula, $\frac{\text{Number of cases}}{N_0}$, becomes biased. For example, in a study of $12,000$ residents, if $3,000$ move away before the end of the follow-up period, they are no longer observed and cannot contribute to the case count for the full duration. Including them in the denominator $N_0 = 12,000$ as if they were followed for the entire period artificially inflates the denominator and leads to an underestimation of the true risk [@problem_id:4599544].

To handle right-[censored data](@entry_id:173222), epidemiologists employ methods from survival analysis, most notably the **Kaplan-Meier (KM) estimator**. This method does not compute risk directly but instead estimates the **[survival function](@entry_id:267383), $S(t)$**, which is the probability of *not* having the event by time $t$, i.e., $S(t) = \mathbb{P}(T > t)$. The risk is then estimated from its complementary relationship: $\widehat{IP}(t) = 1 - \hat{S}(t)$, where $\hat{S}(t)$ is the KM estimate.

The validity of the Kaplan-Meier method hinges on the crucial **noninformative censoring assumption**. This assumption states that, at any point in time, individuals who are censored must have the same future risk of the event as those who continue to be followed. In other words, the reason for censoring must be unrelated to an individual's prognosis. If, for example, sicker participants are more likely to drop out of a study, the censoring is informative, and the KM estimator will be biased (in this case, overestimating survival and underestimating risk) [@problem_id:4599616].

It is important to recognize that the Kaplan-Meier method is a generalization of the simple incidence proportion. In the ideal scenario of a closed cohort with absolutely no right-censoring before the end of the observation period $t$, the Kaplan-Meier estimate $1 - \hat{S}(t)$ simplifies and becomes mathematically identical to the naive proportion of events, $D(t)/N$ [@problem_id:4599570].

### Addressing Real-World Complexities II: Competing Risks

A further layer of complexity arises when participants are at risk of multiple types of events, and the occurrence of one event type precludes the occurrence of the event of interest. These are known as **competing risks**. A classic example is a study of non-fatal myocardial infarction (MI), where death from any other cause is a competing risk because a person who has died cannot subsequently have an MI.

A common but incorrect approach is to treat competing events as if they were standard noninformative censoring and use the Kaplan-Meier method. This procedure leads to a systematic overestimation of the true risk [@problem_id:4599593]. The reason is that the noninformative censoring assumption is violated: an individual who experiences the competing event of death has a future probability of MI equal to zero, which is fundamentally different from the future MI risk of individuals who remain alive.

The KM-based approach, $1 - \hat{S}(t)$, estimates a counterfactual quantity known as the **net risk**: the risk of the event of interest if all competing risks were hypothetically eliminated. The proper target quantity in the presence of [competing risks](@entry_id:173277) is the **Cumulative Incidence Function (CIF)**, often denoted $F_k(t)$ for cause $k$. The CIF represents the **crude risk**: the actual probability of experiencing event $k$ by time $t$ in the real world, where all causes of failure are active. The net risk, $1 - S_k(t)$, will always be greater than or equal to the crude risk, $F_k(t)$.

To analyze the effect of exposures or interventions on risk in the presence of competing events, advanced regression models are required. The choice of model depends on the research question [@problem_id:4599581]:
-   **Cause-Specific Hazard (CSH) Models**: These models evaluate the effect of an exposure on the instantaneous rate of a specific event *among those who are still event-free*. They are best suited for asking **etiologic questions** about the direct biological or behavioral effect of an exposure on an event's hazard.
-   **Subdistribution Hazard (SDH) Models**: The most common of these is the Fine-Gray model. It models the CIF directly by using a modified risk set that cleverly keeps individuals who have experienced a competing event in the denominator. These models are best suited for **prediction** and for assessing the overall impact of an exposure on the absolute risk of an event in a population, accounting for both direct effects and indirect effects mediated through changes in competing risks.

For instance, a new drug might have no direct effect on cancer incidence (a null finding in a CSH model) but might significantly reduce cardiovascular death (a competing risk). By allowing more people to live longer, the drug could indirectly lead to a higher observed cumulative incidence of cancer in the population, an effect that would be captured by an SDH model but not the CSH model. This highlights the critical importance of selecting an analytical method that aligns with the specific research question being asked about risk.