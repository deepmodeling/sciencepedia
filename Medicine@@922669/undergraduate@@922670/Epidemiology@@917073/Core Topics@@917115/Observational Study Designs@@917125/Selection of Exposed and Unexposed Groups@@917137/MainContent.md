## Introduction
In epidemiology, the ability to draw valid causal conclusions from observational data is a cornerstone of public health research. Unlike randomized controlled trials where random allocation creates comparable groups, observational studies face the inherent challenge that exposed and unexposed individuals often differ systematically. This fundamental difference can lead to confounding and biased results, undermining the validity of a study's findings. This article addresses this critical knowledge gap by providing a comprehensive guide to the principles and practices for selecting appropriate exposed and unexposed groups. Over the next three chapters, you will build a robust understanding of this crucial process. The journey begins with "Principles and Mechanisms," which lays out the theoretical foundations of causal inference, including the concepts of exchangeability, the potential outcomes framework, and the use of Directed Acyclic Graphs (DAGs) to manage confounding. Next, "Applications and Interdisciplinary Connections" translates theory into practice, exploring advanced study designs like the active-comparator, new-user design and methods for handling complex biases in real-world settings. Finally, "Hands-On Practices" will allow you to apply and test your knowledge through targeted exercises. We begin by exploring the core principles that form the bedrock of all valid observational research.

## Principles and Mechanisms

The validity of a causal conclusion from an observational study rests critically on the selection of the exposed and unexposed groups. Whereas a randomized controlled trial creates comparable groups through the act of randomization, an observational study must attempt to approximate this comparability through careful design and analysis. The central goal is to select or construct a comparison group of unexposed individuals who are a valid proxy for what would have happened to the exposed individuals had they not been exposed. This chapter elucidates the core principles and mechanisms that guide this selection process, outlining the theoretical foundations, practical strategies, and common biases that researchers must navigate.

### The Foundational Goal: Achieving Exchangeability

The ultimate aim in selecting a comparison group is to achieve **exchangeability**. In an ideal scenario, the exposed and unexposed groups would be so similar in their baseline risk for the outcome that the choice of which group an individual belongs to is irrelevant to their outcome, were they to have the same exposure. We formalize this concept using the **potential outcomes framework**. For each individual, let $Y^1$ be their potential outcome if they were exposed ($X=1$) and $Y^0$ be their potential outcome if they were unexposed ($X=0$).

In a perfect randomized experiment, the groups are **marginally exchangeable**, meaning the distribution of potential outcomes is the same across exposure groups, formally stated as $(Y^1, Y^0) \perp X$. This implies that the unexposed group's average outcome, $E[Y^0 \mid X=0]$, is a direct and unbiased estimate of the counterfactual average outcome for the exposed group, $E[Y^0 \mid X=1]$.

In observational research, this ideal is rarely met. Individuals who are exposed often differ systematically from those who are not. For example, patients who receive a new vaccine may be older or have more comorbidities than those who do not. Consequently, we aim for a more realistic goal: **conditional exchangeability**. This principle states that, within strata of a set of measured pre-exposure covariates $Z$, exposure assignment is independent of the potential outcomes. Formally, this is written as:

$$
(Y^1, Y^0) \perp X \mid Z
$$

This is the cornerstone assumption of "no unmeasured confounding." It posits that if we compare an exposed person to an unexposed person with the exact same set of characteristics $Z$, any difference in their outcomes can be attributed to the exposure. The challenge, therefore, becomes identifying and measuring a sufficiently rich set of covariates $Z$ to make this assumption plausible [@problem_id:4635160].

### The Three Pillars of Causal Identification

For an [observational study](@entry_id:174507) to yield a valid causal estimate, three fundamental assumptions, or pillars of identifiability, must be met. The selection and construction of study groups are deeply intertwined with satisfying these conditions.

1.  **Consistency**: This assumption provides the crucial link between the potential outcomes we wish to know and the observed outcomes we can measure. It states that an individual's observed outcome is the same as their potential outcome under the exposure they actually received. If an individual has exposure status $X$, their observed outcome $Y$ is equal to $Y^X$. This may seem trivial, but it can be violated if the "exposure" is ill-defined. For instance, if "vaccination" in one clinic also involves comprehensive follow-up care, while in another it does not, there are multiple versions of the treatment $X=1$. This violates the **Stable Unit Treatment Value Assumption (SUTVA)**, which posits no interference between units and no multiple versions of treatment. To ensure consistency, the exposure must be clearly and unambiguously defined. A valid strategy in such cases is to redefine the exposure as a joint regimen (e.g., "vaccination with comprehensive care" vs. "vaccination without") or restrict the analysis to a population where the exposure definition is uniform [@problem_id:4635175].

2.  **Exchangeability**: As discussed, this is the assumption of no unmeasured confounding conditional on a set of measured covariates $Z$. The primary task in study design is to select comparison groups and measure covariates in a way that makes conditional exchangeability as plausible as possible.

3.  **Positivity** (or Overlap): This assumption requires that within every stratum of the covariates $Z$, there is a non-zero probability of being both exposed and unexposed. Formally, for a binary exposure, this means $0  P(X=1 \mid Z=z)  1$ for all values of $z$ in the target population. If positivity is violated for a particular subgroup (e.g., if a new diet is strictly contraindicated for patients with advanced kidney disease), it becomes a **structural zero**. In this stratum, everyone is unexposed, making it impossible to estimate the effect of the diet. Standard methods like [inverse probability](@entry_id:196307) weighting or standardization fail in this scenario. The primary design-stage solution is to restrict the study population—and thus, the target of inference—to the strata of $Z$ where positivity holds. This involves carefully defining eligibility criteria to exclude individuals for whom exposure is deterministic [@problem_id:4635132].

### Identifying Confounders: The Backdoor Criterion and DAGs

To achieve conditional exchangeability, we must select an appropriate set of covariates $Z$ for adjustment. **Directed Acyclic Graphs (DAGs)** provide a powerful and rigorous framework for this task. DAGs are visual representations of our causal assumptions about the relationships between variables.

A non-causal path between an exposure $X$ and an outcome $Y$ is known as a **backdoor path**. Such a path contains an arrow pointing into $X$ and can create a spurious association, which is the essence of confounding. The **[backdoor criterion](@entry_id:637856)** gives us a rule for selecting an adjustment set $Z$: a set of variables $Z$ is sufficient for confounding control if it blocks every backdoor path between $X$ and $Y$ and no variable in $Z$ is a descendant of the exposure $X$.

Consider a causal model for a vaccination study [@problem_id:4635129]:
-   Let $C$ be age and comorbidity, $L$ be health-seeking behavior, $X$ be vaccination, and $Y$ be hospitalization.
-   If both $C$ and $L$ affect the decision to vaccinate and independently affect the risk of hospitalization, they create backdoor paths: $X \leftarrow C \rightarrow Y$ and $X \leftarrow L \rightarrow Y$. To block these paths and control for confounding, we must include both $C$ and $L$ in our adjustment set $Z$.
-   If vaccination $X$ leads to the production of antibodies $M$, which in turn prevent hospitalization $Y$, this creates a causal path $X \rightarrow M \rightarrow Y$. To estimate the total effect of vaccination, we must *not* adjust for the mediator $M$. Adjusting for a mediator would block a causal pathway, estimating only the direct effect of $X$ not mediated through $M$.
-   Suppose both vaccination ($X$) and health-seeking behavior ($L$) lead to more intense health screening ($S$), creating the structure $X \rightarrow S \leftarrow L$. The variable $S$ is a **collider**. A path containing a collider is naturally blocked. Adjusting for a [collider](@entry_id:192770) (or its descendant) *unblocks* the path, inducing a spurious association known as **[collider](@entry_id:192770)-stratification bias**. Therefore, one must not adjust for $S$.

By applying the [backdoor criterion](@entry_id:637856) to a DAG representing our best subject-matter knowledge, we can systematically identify a valid set $Z$ for ensuring conditional exchangeability.

### Practical Strategies for Constructing Comparison Groups

Moving from theory to practice, several key strategies are employed to select and construct comparable exposed and unexposed groups.

#### Propensity Score Methods

Directly matching or stratifying on a large set of covariates $Z$ can be difficult due to the "[curse of dimensionality](@entry_id:143920)." The **[propensity score](@entry_id:635864)**, defined as the [conditional probability](@entry_id:151013) of receiving the exposure given the set of covariates, $e(Z) = P(X=1 \mid Z)$, provides an elegant solution. It can be shown that if conditional exchangeability holds given $Z$, it also holds given the [propensity score](@entry_id:635864) $e(Z)$. This single score carries all the information in $Z$ relevant for confounding.

A typical workflow using [propensity score matching](@entry_id:166096) involves several steps [@problem_id:4635135]:
1.  **Model the Propensity Score**: Estimate $e(Z)$ for every individual, typically using a logistic regression model with $X$ as the outcome and $Z$ as the predictors.
2.  **Check for Overlap**: Assess the distribution of propensity scores in the exposed and unexposed groups. The analysis must be restricted to the region of common support, where positivity holds.
3.  **Match or Weight**: Use the score to create comparable groups. In **matching**, each exposed individual is matched to one or more unexposed individuals with a similar propensity score. In **weighting**, individuals are weighted by the inverse of their probability of receiving the exposure they received, creating a pseudo-population where confounders are balanced.
4.  **Assess Covariate Balance**: This is a critical diagnostic step. After matching or weighting, the researcher must verify that the distributions of the original covariates $Z$ are indeed balanced between the groups. If not, the [propensity score](@entry_id:635864) model must be refined and the process repeated.

#### The Active-Comparator, New-User Design

Often, the most powerful tool is not statistical adjustment but intelligent study design. **Confounding by indication** is a pervasive problem where patients with more severe disease are more likely to be treated, creating a strong association between prognosis and exposure. A specific form, **channeling bias**, occurs when patients with certain prognostic profiles are preferentially channeled to a particular therapy [@problem_id:4635190].

The **active-comparator, new-user design** is a state-of-the-art approach to mitigate these biases.
-   **Active Comparators**: Instead of comparing users of a new drug to non-users, the comparison is made with users of an alternative, established drug for the very same indication. This ensures both groups were deemed to require treatment, making them far more comparable on both measured and unmeasured aspects of disease severity than a non-user group would be [@problem_id:4635201].
-   **New-User Design**: The comparison is restricted to individuals newly initiating their respective therapies. This aligns the start of follow-up (time zero) for everyone, ensuring a comparable baseline state and avoiding biases associated with using prevalent (long-term) users.

This design philosophy aims to make the groups as exchangeable as possible from the outset, reducing the reliance on complex statistical adjustment.

#### The Study Base Principle in Case-Control Studies

In a case-control study, where individuals are selected based on their outcome status (cases vs. controls), the principle of exchangeability manifests as the **study base principle**. The study base is defined as the population experience (e.g., person-time at risk) from which the cases arose. For the estimated association to be unbiased, the selected controls must be representative of the exposure distribution within this same study base. If controls are selected from a different source (e.g., using hospital-based controls for cases that arose from the general community), their probability of being selected may depend on their exposure status, leading to **selection bias** [@problem_id:4635152].

### A Gallery of Common Biases in Group Selection

Even with sound principles, several common pitfalls can invalidate a study. Awareness of these biases is essential for robust design.

#### Immortal Time Bias

This bias is a major pitfall in studies with time-varying exposures. It occurs when a period of follow-up, during which an individual must survive to become exposed, is incorrectly classified as "exposed" person-time. For example, if we classify patients as "exposed" if they ever start a drug during follow-up and compare them to "never-exposed" patients from the start of follow-up ($t=0$), we introduce a bias. The exposed patients were "immortal" during the period before they started the drug—they could not die and still become exposed. Attributing this event-free time to the exposed group artificially lowers its event rate, creating a spurious appearance of a protective effect [@problem_id:4635146].

There are two primary ways to avoid immortal time bias:
1.  **Time-Varying Exposure Analysis**: An individual's person-time is correctly attributed to the unexposed state before they initiate treatment and to the exposed state afterward.
2.  **Risk-Set Sampling**: For each person who initiates exposure at a specific time, a new "time zero" is created. Unexposed comparators are selected from the set of individuals who were also alive and at risk at that same moment, aligning the start of their analytical follow-up.

#### Collider-Stratification Bias

As introduced in the context of DAGs, conditioning on a [collider](@entry_id:192770)—a variable influenced by two other variables—can induce a spurious association between those variables. A classic example arises in hospital-based studies. Suppose a pre-hospital exposure ($X$) attenuates symptoms of a disease, while an unmeasured factor ($U$) worsens the underlying disease and the risk of in-hospital mortality ($Y$). Both $X$ and $U$ influence the presenting severity ($S$), which determines hospital admission ($A$). The structure is $X \rightarrow S \leftarrow U \rightarrow Y$. If an analysis is restricted to admitted patients (i.e., conditioning on $A$, a descendant of the collider $S$), a spurious association between $X$ and $U$ is created within the hospital population. This leads to biased estimates of the effect of $X$ on $Y$. The solution is to use a **population-based design** that samples individuals irrespective of their admission status, thereby avoiding conditioning on the collider [@problem_id:4635194].

#### Choosing Inappropriate Comparators

The choice of comparator group is arguably the single most important design decision. Several common choices are fraught with risk [@problem_id:4635201].
-   **Non-users**: Often differ from users in fundamental ways (health status, health-seeking behaviors), leading to strong confounding by indication.
-   **Historical Controls**: Individuals treated in a prior era before a new drug was available may differ due to changes in standard of care, diagnostic practices, or population risk factors over time (**secular trends**).
-   **Prevalent Users**: Comparing new users of one drug to prevalent (long-term) users of another is biased. Prevalent users are "survivors" of their therapy's early risks and have demonstrated tolerance. This breaks the new-user design principle and leads to a non-comparable start of follow-up.

By understanding these principles and potential pitfalls, researchers can more effectively design observational studies that yield robust and meaningful evidence about causal effects. The thoughtful selection of an unexposed group is not a preliminary step but the very foundation upon which causal inference is built.