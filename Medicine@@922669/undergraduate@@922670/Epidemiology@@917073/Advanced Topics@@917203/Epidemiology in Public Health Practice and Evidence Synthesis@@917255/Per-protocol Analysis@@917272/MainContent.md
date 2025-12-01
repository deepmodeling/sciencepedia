## Introduction
In randomized clinical trials, the gold standard for analysis is the intention-to-treat (ITT) principle, which evaluates the effect of a treatment *assignment* on all participants as randomized. While robust and essential for policy decisions, ITT analysis does not directly answer a different, yet crucial, question for scientists and clinicians: What is the biological effect of a treatment when it is taken exactly as prescribed? This knowledge gap—the difference between the effect of a treatment policy versus the effect of treatment adherence—is the central focus of this article on per-protocol analysis.

This article will guide you through the complexities of estimating the per-protocol effect. In "Principles and Mechanisms," we will formally define this causal question using the potential outcomes framework and dissect the severe biases, such as selection bias and collider-stratification bias, that plague simplistic analyses. Next, "Applications and Interdisciplinary Connections" explores the real-world impact of this analysis, from its critical role in regulatory decisions for [non-inferiority trials](@entry_id:176667) to its interpretation in pharmacology and public health ethics. Finally, "Hands-On Practices" provides an opportunity to apply these concepts through guided exercises in estimating per-protocol effects using methods like inverse probability weighting. By navigating these chapters, you will gain a principled understanding of how to validly estimate the effect of treatment adherence, moving beyond naive comparisons to robust causal inference.

## Principles and Mechanisms

In the analysis of clinical trials, the primary result is typically derived from an **intention-to-treat (ITT)** analysis. As established in the "Introduction," this approach adheres to the principle of comparing participants based solely on their initial random assignment, regardless of the treatment they actually receive or whether they adhere to the protocol. While the ITT analysis provides an unbiased estimate of the causal effect of *assignment* to a treatment strategy, it does not directly answer a different, but equally important, question: What is the effect of *adhering* to the treatment protocol itself? This chapter delves into the principles and mechanisms underlying the estimation of this **per-protocol effect**. We will explore how this causal question is formally defined, the significant biases that invalidate naive analytical approaches, and the principled statistical methods developed to provide valid answers.

### Formulating the Causal Question: Beyond Intention-to-Treat

To appreciate the complexities of per-protocol analysis, one must first clearly distinguish the causal question it seeks to answer from those addressed by other common analyses in clinical trials.

#### The Triad of Estimands: ITT, Per-Protocol, and As-Treated

In a trial where non-adherence occurs, we can conceptualize three distinct research questions, each corresponding to a different estimand [@problem_id:4618664]:

1.  **The Intention-to-Treat (ITT) Estimand**: This targets the causal effect of treatment *assignment*. If $Z$ is the binary indicator for randomization ($Z=1$ for the active treatment group, $Z=0$ for the control group) and $Y$ is the outcome, the ITT effect is the contrast in average outcomes, $E[Y \mid Z=1] - E[Y \mid Z=0]$. Because randomization ensures that the groups defined by $Z$ are, on average, identical with respect to all pre-randomization factors (both measured and unmeasured), this comparison provides an unbiased estimate of the effect of being assigned to one treatment strategy versus the other. However, when non-adherence is present (e.g., some in the $Z=1$ group do not take the treatment, and some in the $Z=0$ group do), the biological effect of the treatment is diluted. The ITT effect thus reflects the reality of treatment effectiveness in a pragmatic setting but may understate the physiological effect of the treatment itself.

2.  **The As-Treated Estimand**: This associational measure compares participants based on the treatment they *actually received*, irrespective of their initial randomization. If $A$ indicates the treatment received, this estimand is $E[Y \mid A=1] - E[Y \mid A=0]$. This approach completely discards the benefit of randomization. Since the actual treatment received is a post-randomization choice, the groups being compared are self-selected and are likely not comparable. For example, patients who feel sicker might be more inclined to seek out active treatment, while those experiencing side effects might discontinue it. This creates **confounding by indication**, a severe form of bias that makes the as-treated analysis an unreliable measure of causal effect, unless sophisticated adjustments for all confounders are made [@problem_id:4618664] [@problem_id:4618681].

3.  **The Per-Protocol Estimand**: This estimand targets the causal effect that would have been observed had all participants adhered perfectly to the protocol to which they were assigned. It seeks to answer a counterfactual question: "What would the difference in outcomes have been if everyone in the treatment group had followed the treatment protocol and everyone in the control group had followed the control protocol?" This estimand is of great interest for understanding the biological or physiological efficacy of a treatment under ideal conditions. However, as we will see, its estimation is far from straightforward.

#### Defining the Per-Protocol Estimand with Potential Outcomes

To formalize the per-protocol question, we must use the framework of **potential outcomes**. Let us consider a longitudinal study where participants are supposed to follow a treatment strategy over time. We can define a specific, sustained treatment strategy $\bar a$ as a sequence of treatment actions over the study period (e.g., "take one pill daily for 90 days"). Similarly, let $\bar a'$ be the comparator strategy (e.g., "take one placebo pill daily for 90 days").

For each participant, we can imagine a potential outcome $Y^{\bar a}$, which is the outcome that *would have been observed* for that person had they followed strategy $\bar a$. Likewise, $Y^{\bar a'}$ is the outcome that would have been observed under strategy $\bar a'$. These potential outcomes exist for every participant, regardless of the treatment they were actually assigned or the one they actually followed [@problem_id:4618659].

Using this notation, the **per-protocol causal estimand** is formally defined as the contrast between the average potential outcomes under these two ideal strategies:

$E[Y^{\bar a}] - E[Y^{\bar a'}]$

This definition clarifies the causal goal. It is not an associational comparison of observed outcomes in self-selected groups of adherers, such as $E[Y \mid \text{adhered to } \bar a] - E[Y \mid \text{adhered to } \bar a']$. Instead, it is a causal contrast defined for the entire study population, asking what would happen under two hypothetical, counterfactual scenarios of perfect adherence.

#### Specifying the Protocol: From Rules to a Formal Strategy

The concept of a strategy $\bar a$ requires precise definition. A study protocol is a set of rules for allowable actions over time. For a per-protocol analysis, these rules must be translated into a formal, time-dependent definition of adherence.

Consider a protocol that requires a daily dose, but allows a certain grace period. For a dose scheduled at time $s_k$, the protocol might define adherence as taking the dose within a **grace window**, for instance, $[s_k - g, s_k + g]$ for some window length $g$. A participant's adherence status at any time $t$ should be determined only by actions whose compliance window has fully closed by that time [@problem_id:4618627].

Formally, we can define a time-varying adherence indicator $D_t$, where $D_t=1$ means the participant has been adherent up to time $t$. A protocol deviation occurs at time $t$ if, for any scheduled dose $k$ whose grace window has closed (i.e., $s_k + g \le t$), the participant failed to take a dose within that window. The adherence indicator can thus be defined as:

$D_t = \prod_{k: s_k + g \le t} \mathbf{1}(\exists m \text{ with } r_m \in [s_k - g, s_k + g])$

where $\{r_m\}$ are the observed administration times and $\mathbf{1}(\cdot)$ is the indicator function. This formulation ensures that adherence is a predictable, non-increasing process over time ($D_t$ can switch from 1 to 0, but not back), based only on information available up to time $t$. Such precision is essential for the advanced statistical methods used to estimate per-protocol effects.

### Sources of Bias in Naive Per-Protocol Analyses

Having formally defined the per-protocol estimand, we now turn to the central challenge: its estimation. Naive attempts to estimate this quantity are fraught with biases that can lead to profoundly incorrect conclusions.

#### Confounding and Selection Bias: Breaking the Randomization

The most common mistake in per-protocol analysis is to simply analyze only the participants who adhered to their assigned protocol. For instance, one might compare the outcomes of adherers in the treatment arm with adherers in the control arm.

This approach is fundamentally flawed because it breaks the protection afforded by randomization. While the full groups defined by $Z=1$ and $Z=0$ are comparable at baseline, the subgroups of *adherers* within these arms are not. Adherence is a post-randomization behavior. The factors that predict whether a person adheres to treatment—such as their underlying health status, their motivation, or their experience of side effects—are often also predictors of the outcome.

For example, participants in the active treatment arm who experience mild side effects may be more likely to stop taking the drug. At the same time, those experiencing side effects may have a different prognosis than those who do not. Comparing the remaining adherers (who did not experience side effects) in the treatment arm to the adherers in the placebo arm (who could not have experienced drug-related side effects) is no longer a fair comparison. This is a form of **selection bias**. The analysis ceases to be a randomized comparison and becomes an observational one, vulnerable to confounding [@problem_id:4618721].

#### The Mechanism of Collider-Stratification Bias

The mechanism underlying this selection bias can be elegantly explained using causal diagrams, or **Directed Acyclic Graphs (DAGs)**. Let us consider a simplified structure where randomization $Z$ influences adherence $D$, and an unmeasured prognostic factor $U$ (e.g., latent health status) also influences both adherence $D$ and the outcome $Y$. This can be represented as:

$Z \rightarrow D \leftarrow U \rightarrow Y$

In this diagram, adherence $D$ is a **collider**, as it has two arrows pointing into it. By the rules of [d-separation](@entry_id:748152) in DAGs, the path between $Z$ and $U$ is blocked by this collider, reflecting the fact that randomization makes $Z$ and $U$ independent in the full population.

However, a naive per-protocol analysis conditions on adherence (e.g., by restricting the analysis to the $D=1$ stratum). Conditioning on a collider (or a descendant of a [collider](@entry_id:192770)) *opens* the path between its parents. This induces a spurious, non-causal association between $Z$ and $U$ within the selected subgroup of adherers. Because $U$ is a cause of the outcome $Y$, this induced association between $Z$ and $U$ creates confounding that was not present in the full, randomized sample. This phenomenon is known as **[collider](@entry_id:192770)-stratification bias** and is the formal reason why randomization is "broken" by conditioning on post-randomization variables like adherence [@problem_id:4618721] [@problem_id:4618681] [@problem_id:4618716].

#### Immortal Time Bias: A Pitfall in Survival Analysis

When the outcome is a time-to-event measure (e.g., time to hospitalization), another insidious bias can arise from the improper definition of adherence. This is known as **immortal time bias** [@problem_id:4618694].

Suppose an investigator defines "adherers" as those who successfully completed the first four weeks of a treatment protocol. By this very definition, to be classified as an "adherer," a participant must have survived without an event for at least four weeks. The person-time contributed by this group during the first four weeks is "immortal"—it is guaranteed to be event-free by the flawed study design.

When calculating the event rate (events per person-time), the denominator for the adherer group includes this immortal person-time, while the numerator for that period is artificially forced to be zero. This systematically deflates the calculated [hazard rate](@entry_id:266388) for the adherer group, creating a spurious appearance of a protective treatment effect.

The correct way to handle such data is to treat adherence as a **time-varying exposure**. A participant's person-time should be classified as "adherent" or "non-adherent" dynamically, based only on information known up to each point in time. For example, in any given week, a participant's person-time is classified based on whether they took the dose in that week. This avoids using future information to classify past exposure, thereby eliminating immortal time bias.

### Principled Estimation of Per-Protocol Effects

Given the biases that plague naive analyses, estimating the per-protocol effect requires advanced statistical methods grounded in the principles of causal inference. These methods treat the per-protocol analysis as an observational study nested within the trial and aim to reconstruct the effect that would have been observed in an ideal (but unrealized) randomized trial with perfect adherence.

#### The Three Pillars of Identification: Consistency, Exchangeability, and Positivity

The validity of these methods rests on three key, untestable assumptions about the relationship between measured data and the counterfactual world:

1.  **Consistency**: This assumption links the potential outcomes to the observed data. It states that an individual's observed outcome is the potential outcome corresponding to the treatment history they actually experienced.

2.  **Exchangeability (or No Unmeasured Confounding)**: This assumption states that the treatment received at any point in time is independent of the potential outcomes, conditional on the observed past. In longitudinal studies, this requires a stronger condition known as **sequential exchangeability**. For a time-varying covariate $L_t$ that is affected by past treatment $A_{t-1}$ and also predicts future treatment $A_t$ and the outcome $Y$ (a structure known as **time-varying confounding**), we must assume that treatment at time $t$ is conditionally independent of the potential outcomes given the entire history of past treatments and covariates, $\bar{A}_{t-1}$ and $\bar{L}_t$. Baseline exchangeability alone is insufficient in this common scenario [@problem_id:4618688] [@problem_id:4618714].

3.  **Positivity**: This assumption requires that for every time point $t$, within every stratum of observed history, the probability of receiving a given treatment and of remaining uncensored (adherent) is strictly greater than zero. If for a certain type of patient it is impossible to receive a particular treatment or to adhere to the protocol, then we have no data to inform us about the counterfactual outcome under that scenario, and the causal effect is not identifiable [@problem_id:4618683].

#### Correcting for Bias with Inverse Probability Weighting

One of the most common methods for per-protocol analysis under these assumptions is **Inverse Probability Weighting (IPW)**. When non-adherence is treated as a form of censoring, the method is often called **Inverse Probability of Censoring Weighting (IPCW)** [@problem_id:4618714].

The intuition behind IPCW is to correct for the selection bias introduced by informative censoring (i.e., when adherence is related to prognostic factors). The method involves two steps:
1.  Model the probability of remaining adherent and uncensored at each time point, conditional on the observed history of covariates and past treatment.
2.  Assign a weight to each individual who remains adherent at the end of the study. This weight is the inverse of their estimated probability of having remained adherent throughout the study.

Individuals who had a high probability of dropping out (e.g., those who became sicker) but who managed to remain adherent are given a larger weight. This up-weighting creates a **pseudo-population** in which the characteristics of the adherers are, in expectation, the same as those of the original full study population. In this pseudo-population, the link between the prognostic factors and adherence is broken, and a simple comparison of outcomes between treatment groups becomes unbiased for the per-protocol effect.

To improve the statistical stability of the estimates, **stabilized weights** are often used. The stabilized weight for an individual $i$ up to time $t$ is given by:

$w_i = \prod_{k=0}^{t} \frac{P(C_i(k)=0 \mid \bar{L}_i(0))}{P(C_i(k)=0 \mid \bar{A}_i(k-1), \bar{L}_i(k))}$

Here, $C_i(k)=1$ denotes censoring (non-adherence) at time $k$. The denominator is the probability of remaining adherent conditional on the full history of covariates $\bar L$ and treatments $\bar A$. The numerator is the probability of remaining adherent conditional on a reduced set of covariates (often just baseline covariates or a subset of the history that does not include past treatment). This stabilization reduces the variance of the estimator without introducing bias, provided the models are correctly specified [@problem_id:4618703].

#### Practical Challenges: Model Specification and Positivity Violations

While powerful, IPW-based methods come with their own challenges [@problem_id:4618714] [@problem_id:4618683]:

*   **Model Misspecification**: The validity of IPW hinges on the correct specification of the models used to estimate the probabilities of adherence/censoring. If these models are incorrect, the weights will be wrong, and the resulting estimate of the per-protocol effect will be biased.
*   **Positivity Violations**: The method can become highly unstable if there are individuals with very low probabilities of remaining adherent (a "practical" positivity violation). This leads to extremely large inverse probability weights, which can cause the variance of the estimator to explode, making the results unreliable. While techniques like weight truncation can mitigate this variance, they may do so at the cost of introducing bias.

In conclusion, per-protocol analysis answers a critical scientific question about the effects of treatment under ideal adherence. However, moving beyond the safe harbor of intention-to-treat analysis requires a deep understanding of causal principles to navigate the treacherous waters of selection bias, confounding, and other methodological pitfalls. Principled methods like [inverse probability](@entry_id:196307) weighting provide a formal framework for this task, but their application requires careful consideration of their underlying assumptions and practical limitations.