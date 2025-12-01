## Introduction
In many real-world studies, from clinical trials to public health research, individuals are followed over time and can experience one of several different outcomes. The occurrence of one event, such as death from a heart attack, can prevent another, like death from cancer, from ever being observed. This scenario, known as [competing risks](@entry_id:173277), poses a significant analytical challenge. A common but critical error is to treat these competing events as simple censored data, leading to biased and overestimated risk predictions. This article provides a comprehensive guide to correctly analyzing data in the presence of competing risks. The first chapter, **Principles and Mechanisms**, will lay the statistical foundation, defining key concepts like the cause-specific hazard and the cumulative incidence function (CIF), and explaining why the latter is crucial for accurate risk assessment. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the practical importance of these methods in diverse fields such as oncology, [policy evaluation](@entry_id:136637), and even algorithmic fairness. Finally, the **Hands-On Practices** section will offer practical problems to reinforce these concepts, ensuring you can confidently apply them in your own work.

## Principles and Mechanisms

In the study of time-to-event data, we are often confronted with situations where individuals can experience one of several distinct types of events. For instance, in a clinical trial for a new [cancer therapy](@entry_id:139037), a patient might die from the cancer under study, die from an unrelated cause such as a heart attack, or experience a non-fatal but significant side effect. The occurrence of any one of these events may preclude the observation of the others. This scenario, where multiple, [mutually exclusive events](@entry_id:265118) are in "competition" to be the first to occur, is the domain of **[competing risks analysis](@entry_id:634319)**. This chapter will elucidate the fundamental principles and statistical machinery required to correctly analyze and interpret data in the presence of such competing events.

### The Conceptual Foundation of Competing Risks

To formalize the [competing risks](@entry_id:173277) framework, it is useful to employ the **latent failure time model**. Imagine that for each individual, there is a set of hypothetical or latent failure times, $\{T_1, T_2, \dots, T_K\}$, one for each of the $K$ possible event types. Each $T_j$ represents the time at which an event of cause $j$ would occur if it were the only type of event possible. In reality, we do not observe this full set of latent times. Instead, we only observe the time of the *first* event that occurs and its specific cause.

Therefore, the observed time to event, denoted by $T$, is the minimum of these latent times:
$$T = \min\{T_1, T_2, \dots, T_K\}$$
The observed cause of the event, denoted by $J$, is the index of the latent time that was the minimum:
$$J = \arg\min_{j \in \{1, \dots, K\}} T_j$$
This pair of observable random variables, $(T, J)$, forms the basis of our data [@problem_id:4579861].

This model provides a clear epidemiological interpretation of what it means for events to be "competing." The various causes are in a race to be the first to occur. When one event, say cause $j$, occurs at time $T$, the follow-up for that individual concludes. As a consequence, that individual is permanently removed from the set of individuals "at risk" for any other event type $k \ne j$ at all subsequent times. This removal from the risk set due to a competing event is a fundamental feature of the data-generating process and must be handled differently from conventional [right-censoring](@entry_id:164686) (e.g., administrative end of study or loss to follow-up), where removal is assumed to be for reasons independent of the failure processes [@problem_id:4579861] [@problem_id:4579894].

### Quantifying Risk: Fundamental Quantities

To analyze competing risks data, we must define two primary quantities: the cause-specific hazard, which describes the instantaneous event rate, and the cumulative incidence function, which describes the cumulative probability of an event.

#### The Cause-Specific Hazard

The **cause-specific hazard (CSH)** for cause $k$, denoted $\lambda_k(t)$, is the instantaneous rate at which individuals who are currently event-free at time $t$ experience an event of cause $k$. More formally, it is defined as the limit of the probability of experiencing event $k$ in a small interval of time, given survival up to that time, scaled by the length of the interval:
$$ \lambda_k(t) = \lim_{\Delta t \to 0} \frac{P(t \le T \lt t+\Delta t, J=k \mid T \ge t)}{\Delta t} $$
The key component of this definition is the conditioning event, $\{T \ge t\}$. This means the risk set for the cause-specific hazard at time $t$ comprises all individuals who have not yet experienced an event of *any* cause. It is the rate of cause $k$ among those who are, at that moment, still "in the competition" [@problem_id:4579836]. In practice, this rate can be estimated over a short interval by dividing the number of observed events of cause $k$ by the total person-time contributed by the at-risk individuals during that interval.

#### The Cumulative Incidence Function

While the hazard describes an instantaneous rate, a more clinically and epidemiologically intuitive quantity is the probability of an event occurring over a specified period. The **cumulative incidence function (CIF)** for cause $k$, denoted $F_k(t)$, provides exactly this. It is defined as the probability that an event of cause $k$ has occurred by time $t$:
$$ F_k(t) = P(T \le t, J=k) $$
The CIF represents the **crude probability** or **absolute risk** of experiencing event $k$ by a certain time, correctly accounting for the fact that some individuals may be removed from observation by competing events [@problem_id:4579887]. This makes the CIF the preferred estimand for prognostic questions, patient counseling, and public health planning, where the goal is to predict the actual burden of an event in a real-world population [@problem_id:4579879]. For example, when counseling a patient about their 10-year risk of dying from prostate cancer, the CIF provides the most relevant figure, as it properly incorporates the competing risk of death from other causes like heart disease, which is a significant factor in older populations [@problem_id:4579879].

### The Relationship Between Hazards and Cumulative Incidence

The cause-specific hazard and the cumulative incidence function are intimately related. The CIF can be expressed as an integral involving the CSH and the **overall survival function**, $S(t) = P(T > t)$, which is the probability of remaining free of any event up to time $t$.

To fail from cause $k$ in an infinitesimally small interval around time $u$, an individual must first survive all causes up to time $u$ (with probability $S(u)$) and then experience the hazard for cause $k$ (at a rate of $\lambda_k(u)$). Integrating this instantaneous probability from $0$ to $t$ gives the CIF:
$$ F_k(t) = \int_0^t \lambda_k(u) S(u) \,du $$
The overall survival function $S(u)$ itself depends on the **overall hazard**, which is the sum of all cause-specific hazards: $\lambda(u) = \sum_{j=1}^{K} \lambda_j(u)$. The relationship is $S(u) = \exp\left(-\int_0^u \lambda(s) \,ds\right)$.

This integral formulation reveals a crucial insight: the cumulative incidence of cause $k$ depends not only on its own hazard, $\lambda_k(t)$, but also on the hazards of all competing causes, $\{\lambda_j(t)\}_{j \neq k}$, through the $S(u)$ term [@problem_id:4579893]. If the hazard of a competing event increases, more individuals will fail from that competing cause, reducing the proportion of the cohort that survives event-free. This reduces $S(u)$, which in turn shrinks the value of the integral for $F_k(t)$. Consequently, increasing the risk of a competing event can decrease the observed cumulative incidence of the event of interest, even if the latter's own specific hazard remains unchanged [@problem_id:4579893] [@problem_id:4579894].

For very short time horizons, however, the influence of competing events is minimal. A first-order Taylor expansion reveals that as $t \downarrow 0$, the CIF is well-approximated by $F_k(t) \approx \lambda_k t$. In this initial instant, the probability of the event of interest is governed almost entirely by its own hazard, as there has been insufficient time for competing events to significantly deplete the at-risk population [@problem_id:4579893].

### A Common Pitfall: The Naive Kaplan-Meier Approach

A frequent and serious error in analyzing competing risks data is to estimate the risk of cause $k$ by calculating a standard Kaplan-Meier survival curve, where events of type $k$ are treated as "failures" and all competing events are treated as "[non-informative censoring](@entry_id:170081)." The resulting risk estimate, $1 - S_{\text{KM}}(t)$, does not estimate the CIF, $F_k(t)$.

The Kaplan-Meier estimator is designed to estimate survival in a world where censored individuals are assumed to remain at risk beyond their censoring time. By treating competing events as censoring, this approach implicitly analyzes a hypothetical world where those competing events have been eliminated. The quantity it estimates is the **net risk**, defined as the probability of failing from cause $k$ if all other causes were absent [@problem_id:4579888]:
$$ \text{Net Risk}_k(t) = 1 - \exp\left(-\int_0^t \lambda_k(u) \,du\right) $$
Because the net risk calculation does not account for individuals being removed from the risk pool by competing events, it will always be greater than or equal to the crude risk (the CIF). The two quantities are only equal in the trivial case where no [competing risks](@entry_id:173277) exist [@problem_id:4579875]. For instance, in a hypothetical cohort with a constant CSH for disease ($\lambda_D = 0.04$) and a competing event ($\lambda_C = 0.06$), the 5-year net risk of the disease is $1 - \exp(-0.04 \times 5) \approx 0.181$. However, the true 5-year crude risk (CIF) is only $\frac{0.04}{0.04+0.06}(1 - \exp(-(0.04+0.06) \times 5)) \approx 0.157$. The naive Kaplan-Meier approach overestimates the actual probability of the disease by ignoring the depletion of the at-risk population due to the competing event [@problem_id:4579888].

### Estimation in Practice

#### Non-parametric Estimation: The Aalen-Johansen Estimator

The correct non-parametric estimator for the CIF is the **Aalen-Johansen estimator**. It correctly synthesizes information on all event types to estimate the crude risk for a specific cause. Using counting process notation, where $dN_k(u)$ is the number of events of type $k$ at time $u$ and $Y(u)$ is the number of individuals at risk just before $u$, the estimator is given by:
$$ \hat{F}_k(t) = \sum_{u \le t} \hat{S}(u-) \frac{dN_k(u)}{Y(u)} $$
Here, the sum is taken over all observed event times $u$ up to time $t$. Each term in the sum represents the estimated unconditional probability of failing from cause $k$ at time $u$. This is calculated as the product of two components:
1.  $\hat{S}(u-)$: The Kaplan-Meier estimate of the overall probability of being event-free just prior to time $u$.
2.  $\frac{dN_k(u)}{Y(u)}$: The estimated [conditional probability](@entry_id:151013) (or hazard) of failing from cause $k$ at time $u$, given that one was event-free.

This formula beautifully mirrors the continuous-time integral, accumulating the increments of cause-specific risk, each weighted by the probability of surviving long enough to be at risk for that increment [@problem_id:4579881].

#### Regression Modeling: Cause-Specific Cox Models

To investigate how covariates influence the risk of different event types, we can use regression models. The most common approach is to model each cause-specific hazard separately using a **cause-specific Cox [proportional hazards model](@entry_id:171806)**:
$$ \lambda_k(t \mid X) = \lambda_{k0}(t)\exp(\beta_k^\top X) $$
This model allows for a unique baseline [hazard function](@entry_id:177479), $\lambda_{k0}(t)$, and a unique vector of log-hazard ratios, $\beta_k$, for each cause $k$. This flexibility is crucial, as a covariate might increase the risk of one event type while decreasing or having no effect on another.

The fitting procedure is straightforward: for each of the $K$ causes, a separate standard Cox model is fitted. For the model of cause $k$, failures from cause $k$ are coded as events, while failures from all competing causes ($j \ne k$) are treated as right-censored observations at their time of occurrence [@problem_id:4579862]. This correctly removes individuals from the risk set as soon as they experience any event, aligning perfectly with the definition of the cause-specific hazard.

### An Alternative Framework: Modeling the Subdistribution

An alternative to modeling cause-specific hazards is to model the CIF directly. This approach, pioneered by Fine and Gray, is based on the **subdistribution hazard**. The subdistribution hazard for cause $k$, $h_k^{SD}(t)$, is defined as:
$$ h_k^{SD}(t) = \lim_{\Delta t \to 0} \frac{P(t \le T \lt t+\Delta t, J=k \mid T \ge t \text{ or } (T \le t, J \neq k))}{\Delta t} $$
The defining feature of the subdistribution hazard is its conditioning set, or **pseudo-risk set**. Unlike the CSH risk set, which only contains event-free individuals, this pseudo-risk set includes both event-free individuals *and* those who have already experienced a competing event [@problem_id:4579880]. While it may seem paradoxical to keep individuals who can no longer fail in the risk set, this mathematical construction ensures that a [proportional hazards model](@entry_id:171806) based on $h_k^{SD}(t)$ will yield direct predictions of the CIF.

The choice between cause-specific and subdistribution hazard models depends on the research question. Cause-specific models excel at identifying the etiologic effects of covariates on the rate of an event among those who are currently healthy. Subdistribution models are tailored for prediction, as they directly model the absolute risk of an event in the full population.

### Choosing the Right Tool: Interpretation and Application

The choice between the CIF, net risk, and cause-specific hazard is not a matter of statistical correctness but of aligning the estimand with the scientific question.

-   **Cause-Specific Hazards** are the tool of choice for **etiologic and mechanistic research**. They answer questions about the instantaneous rate or intensity of a process. For example, a study investigating how a gene affects the rate of stroke among currently stroke-free individuals would focus on the CSH [@problem_id:4579879].

-   The **Cumulative Incidence Function (CIF)** is indispensable for **prognosis, prediction, and public health**. It answers practical questions about absolute risk in a real-world setting where multiple outcomes are possible. Projecting the number of cancer deaths to allocate resources or informing a patient of their actual chance of an outcome requires the CIF [@problem_id:4579879].

-   **Net Risk** is a hypothetical quantity, useful in some **etiologic contexts** where the goal is to understand the "pure" biological potential of a risk factor by conceptually removing the influence of all other causes. This might be relevant in isolating a carcinogenic process, but its interpretation remains non-obvious as it describes a world that cannot be observed [@problem_id:4579879].

By understanding these distinctions, researchers can select the appropriate analytical tools to draw meaningful and accurate conclusions from time-to-event data with competing risks.