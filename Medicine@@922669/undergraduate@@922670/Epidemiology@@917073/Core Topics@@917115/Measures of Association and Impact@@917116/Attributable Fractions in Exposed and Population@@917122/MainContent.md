## Introduction
In epidemiology, identifying a link between an exposure and a disease is only the first step. For public health officials, clinicians, and policymakers, the more pressing question is one of impact: what proportion of disease in a population is actually *caused* by a given risk factor? Answering this question is crucial for prioritizing interventions, allocating resources, and communicating public health risks. This article addresses this knowledge gap by providing a comprehensive guide to attributable fractions, the primary epidemiological tools for quantifying the burden of disease attributable to an exposure.

This guide is structured to build your understanding from foundational theory to practical application. The first section, "Principles and Mechanisms," will introduce the causal framework for attributable risk, defining and deriving the formulas for the Attributable Fraction among the Exposed (AF_e) and the Population Attributable Fraction (PAF). The second section, "Applications and Interdisciplinary Connections," will explore how these measures are used in real-world public health scenarios, from environmental health to [policy evaluation](@entry_id:136637), and discusses extensions for complex situations. Finally, the "Hands-On Practices" section provides targeted exercises to solidify your ability to calculate and apply these vital metrics. By the end, you will be equipped to move beyond measures of association to measures of impact, a critical skill for any epidemiologist.

## Principles and Mechanisms

In epidemiology, quantifying the association between an exposure and a disease, often through measures like the risk ratio or odds ratio, is a fundamental first step. However, for public health planning, policy-making, and clinical decision-making, it is often more critical to understand the *impact* of the exposure on the burden of disease. We need to answer questions such as, "What proportion of lung cancer cases are actually caused by smoking?" or "By how much would we reduce the incidence of heart disease if we could eliminate a specific dietary risk factor?" Answering these questions requires moving beyond measures of association to measures of attributable risk.

This chapter elucidates the principles and mechanisms behind two central concepts in this domain: the **Attributable Fraction among the Exposed** and the **Population Attributable Fraction**. We will ground these measures in the rigorous language of causal inference, demonstrate their calculation, and explore their interpretation and practical application. Crucially, we will distinguish between what can be calculated from observed data (associational measures) and what we truly wish to estimate (causal estimands), clarifying the assumptions necessary to bridge this gap.

### The Causal Framework for Attributable Risk

The very notion of a disease case being "attributable to" an exposure is inherently causal. It implies a comparison between the observed reality and a **counterfactual** reality where the exposure was absent. To formalize this, we employ the potential outcomes framework. For any individual, let $Y$ be the observed disease outcome ($Y=1$ for disease, $Y=0$ for no disease) and $A$ be the observed exposure status ($A=1$ for exposed, $A=0$ for unexposed). We can then define two potential outcomes for each individual:

-   $Y^1$: The outcome that *would have been* observed if the individual had been exposed ($A=1$).
-   $Y^0$: The outcome that *would have been* observed if the individual had been unexposed ($A=0$).

For any given individual, we can only observe one of these potential outcomes—the one corresponding to their actual exposure status. This is a statement of the **consistency** assumption, where the observed outcome $Y$ is equal to $Y^A$. The challenge of causal inference is to make valid inferences about the unobserved potential outcomes [@problem_id:4572124].

The attributable fractions are defined through comparisons of risks within this framework. They seek to quantify the proportion of disease that would be prevented under a hypothetical **intervention** that removes the exposure.

### Attributable Fraction among the Exposed ($AF_e$)

The first question we can ask pertains to the burden of disease specifically within the group of people who were exposed. Of the cases observed in this group, what fraction was due to the exposure itself, rather than to other background causes? This is the **Attributable Fraction among the Exposed ($AF_e$)**.

#### Causal Definition and Identification

The total risk of disease among the exposed is $P(Y=1 \mid A=1)$, which under the consistency assumption is equivalent to $P(Y^1=1 \mid A=1)$. The risk that this same group *would have had* if they had not been exposed is the counterfactual quantity $P(Y^0=1 \mid A=1)$. The excess risk due to the exposure is the difference between these two. The $AF_e$ is this excess risk expressed as a proportion of the total risk among the exposed [@problem_id:4572124]:

$$
AF_{e, \text{causal}} = \frac{P(Y^1=1 \mid A=1) - P(Y^0=1 \mid A=1)}{P(Y^1=1 \mid A=1)}
$$

The primary challenge is that the counterfactual risk, $P(Y^0=1 \mid A=1)$, is unobservable. We cannot simultaneously observe what happens to exposed individuals when they are both exposed and unexposed. To estimate this quantity from data, we must make a critical assumption known as **exchangeability**. This assumption states that the risk of the outcome under the counterfactual condition of no exposure is the same for those who were actually exposed and those who were actually unexposed. Formally, $Y^0 \perp A$, which means $P(Y^0=1 \mid A=1) = P(Y^0=1 \mid A=0)$. This implies that the unexposed group can serve as a valid surrogate for what would have happened to the exposed group in the absence of exposure. In an [observational study](@entry_id:174507), this assumption is often plausible only after conditioning on a sufficient set of common causes (confounders) $L$, written as $Y^0 \perp A \mid L$. In a well-conducted randomized controlled trial, randomization itself tends to ensure exchangeability holds [@problem_id:4572124].

Under exchangeability and consistency, we can identify the unobservable counterfactual risk with the observable risk in the unexposed group:
$$
P(Y^0=1 \mid A=1) \stackrel{\text{exchangeability}}{=} P(Y^0=1 \mid A=0) \stackrel{\text{consistency}}{=} P(Y=1 \mid A=0)
$$

#### Computational Formula and Interpretation

By substituting the observable risk among the unexposed ($R_u = P(Y=1 \mid A=0)$) for the unobservable counterfactual risk, and using $R_e = P(Y=1 \mid A=1)$, we arrive at the standard computational formula for $AF_e$:

$$
AF_e = \frac{R_e - R_u}{R_e} = 1 - \frac{R_u}{R_e}
$$

This can also be expressed in terms of the Risk Ratio ($RR = R_e/R_u$) as:

$$
AF_e = 1 - \frac{1}{RR}
$$

The structure of this formula, $\frac{R_e - R_u}{R_e}$, highlights its meaning as a part-to-whole ratio. The numerator, $R_e - R_u$, is the **Risk Difference ($RD$)**, representing the absolute excess risk among the exposed that is attributable to the exposure. This quantity has units of risk (e.g., cases per 100 person-years). The denominator, $R_e$, is the total risk observed in the exposed group. By dividing the excess risk by the total risk, we create a dimensionless proportion, which is the fraction of the total risk in the exposed group that is in excess of their baseline risk [@problem_id:4572177].

For example, consider a study where the risk of disease among the exposed is $R_e = 0.20$ and among the unexposed is $R_u = 0.05$ [@problem_id:4572152].
The $AF_e$ would be:
$$
AF_e = \frac{0.20 - 0.05}{0.20} = \frac{0.15}{0.20} = 0.75
$$
The causal interpretation is as follows: assuming exchangeability, consistency, and other identifying conditions hold, **75% of the disease cases that occurred among the exposed individuals are attributable to the exposure**. In other words, if we could have intervened to remove the exposure from this group, 75% of their cases would have been prevented.

### Population Attributable Fraction ($PAF$)

While $AF_e$ is informative about the impact on exposed individuals, public health policy is often concerned with the entire population. The **Population Attributable Fraction ($PAF$)** addresses this by quantifying the proportion of all disease cases in the total population (both exposed and unexposed) that are attributable to the presence of the exposure.

#### Causal Definition and Identification

The $PAF$ is defined by comparing the observed overall population risk, $R_p = P(Y=1)$, to the counterfactual population risk that would have been observed had the exposure been eliminated from the entire population. This counterfactual risk is $R_{cf} = P(Y^0=1)$ [@problem_id:4572164]. The causal $PAF$ is therefore:

$$
PAF_{\text{causal}} = \frac{P(Y=1) - P(Y^0=1)}{P(Y=1)} = \frac{R_p - R_{cf}}{R_p}
$$

This definition makes clear that $PAF$ is an inherently causal estimand, as it is defined with respect to a hypothetical, population-wide intervention that sets $A=0$ for everyone [@problem_id:4572088].

To identify the $PAF$ from data, we must identify its components. The observed population risk, $R_p$, can be calculated as a weighted average of the risks in the exposed and unexposed subgroups, where the weights are the prevalence of exposure ($p_e = P(A=1)$) and non-exposure ($1-p_e$):
$$
R_p = R_e \cdot p_e + R_u \cdot (1 - p_e)
$$

The counterfactual population risk, $R_{cf} = P(Y^0=1)$, is the risk that would exist if everyone were unexposed. Under the same assumption of exchangeability used for $AF_e$, this population-wide baseline risk is equal to the observed risk in the unexposed group, $R_u$.

#### Computational Formula and Interpretation

Substituting the observable quantities into the causal definition gives the standard computational formula for $PAF$:

$$
PAF = \frac{R_p - R_u}{R_p}
$$

Let's continue the previous example where $R_e = 0.20$, $R_u = 0.05$, and let the prevalence of exposure in the population be $p_e = 0.40$ [@problem_id:4572152].

First, we calculate the total population risk:
$$
R_p = (0.20 \times 0.40) + (0.05 \times 0.60) = 0.08 + 0.03 = 0.11
$$
Now, we can calculate the $PAF$:
$$
PAF = \frac{0.11 - 0.05}{0.11} = \frac{0.06}{0.11} \approx 0.545
$$
The causal interpretation is: assuming the necessary causal assumptions hold, **approximately 54.5% of all disease cases in the total population are attributable to the exposure**. If we could eliminate the exposure from the entire population, the disease incidence would fall by about 54.5%.

#### The Critical Role of Exposure Prevalence

Unlike the $AF_e$, which depends only on the relative risk, the $PAF$ is critically dependent on both the strength of the association ($RR$) and the **prevalence of the exposure ($p_e$)**. This can be seen by substituting the expressions for $R_p$ and $R_e$ into the $PAF$ formula to derive an alternative expression that depends only on $p_e$ and $RR$:

$$
PAF = \frac{p_e(RR - 1)}{1 + p_e(RR - 1)}
$$

This formula makes it clear that even if an exposure is a very strong risk factor (high $RR$), its impact on the population's health ($PAF$) will be small if the exposure is very rare (low $p_e$). For example, consider an occupational hazard with a strong association with a disease ($RR=8$) but a very low prevalence in the general population ($p_e=0.005$). Despite the high risk for those exposed, the $PAF$ is only about 3.4% [@problem_id:4572176]. Conversely, a weaker risk factor ($RR=1.5$) that is extremely common ($p_e=0.80$) can have a much larger population impact ($PAF \approx 28.6\%$).

### Absolute vs. Relative Impact: PAR and Public Health Planning

The $PAF$ is a relative measure—a proportion. For public health planning, it is often equally important to consider the **absolute impact** of an exposure. This is captured by the **Population Attributable Risk (PAR)**, also known as the population risk difference. The PAR is the absolute difference between the population risk and the counterfactual risk under no exposure [@problem_id:4572131]:

$$
PAR = R_p - R_{cf} = R_p - R_u
$$

In our running example, $PAR = 0.11 - 0.05 = 0.04$. This means there is an excess of 4 cases per 100 people in the total population due to the exposure.

The relationship between the relative and absolute measures is straightforward:
$$
PAF = \frac{PAR}{R_p} \quad \text{or} \quad PAR = PAF \times R_p
$$

The distinction between relative ($PAF$) and absolute ($PAR$) impact is vital for prioritizing interventions. Consider two communities, X and Y, where an exposure has the same relative risk ($RR=2.5$) and prevalence ($p_e=0.10$). Because these two parameters determine the $PAF$, both communities will have the same $PAF \approx 13.0\%$. A naive interpretation might suggest that an intervention to remove the exposure has equal priority in both locations.

However, if the baseline risk in the unexposed is higher in Community X ($R_{0,X} = 0.05$) than in Community Y ($R_{0,Y} = 0.02$), the absolute impact will differ. The Risk Difference ($RD$) is greater in Community X ($RD_X = 0.075$) than in Community Y ($RD_Y = 0.03$). Consequently, the PAR is also greater in Community X. Eliminating the exposure would prevent approximately 75 cases per 10,000 people in Community X, but only 30 cases per 10,000 people in Community Y. Therefore, an intervention in Community X would yield a much greater absolute benefit [@problem_id:4572089]. This illustrates why public health decision-makers must consider both relative and absolute measures of impact.

### Extension to Protective Exposures: The Prevented Fraction

When an exposure is protective ($RR \lt 1$), such as a vaccine or a healthy diet, the concept of an "attributable" fraction is replaced by a **Prevented Fraction**. The logic is analogous but inverted.

The **Prevented Fraction among the Exposed ($PF_e$)** is the proportion of potential cases among the exposed group that were averted *because of* the protective exposure. It is calculated as the risk reduction relative to the risk they would have had without the exposure ($R_u$):

$$
PF_e = \frac{R_u - R_e}{R_u} = 1 - RR
$$

For a vaccine, this quantity is commonly known as **vaccine efficacy**. For example, if the risk of disease is $R_e=0.005$ in the vaccinated and $R_u=0.025$ in the unvaccinated, the $RR=0.2$. The $PF_e = 1 - 0.2 = 0.80$, meaning the vaccine prevented 80% of the cases that would have otherwise occurred in the vaccinated group [@problem_id:4572094].

The **Population Prevented Fraction ($PF_p$)** is the proportion of all potential cases in the total population that were averted due to the presence of the protective exposure. It is calculated as the reduction in population risk relative to the risk that would have existed if no one had been exposed ($R_u$):

$$
PF_p = \frac{R_u - R_p}{R_u}
$$

For protective exposures, there is a simple and intuitive relationship between population impact, individual-level efficacy, and exposure prevalence (or coverage):
$$
PF_p = p_e \times PF_e
$$
This shows that the overall population benefit of a vaccine is a direct product of its efficacy and how many people receive it [@problem_id:4572094].

### Summary: The Rigor of Causal Interpretation

Attributable and prevented fractions are powerful tools for translating research findings into measures of public health impact. However, their interpretation as the outcomes of hypothetical interventions is predicated on a set of strong, untestable assumptions. Moving from a simple associational calculation to a robust causal claim requires a comprehensive and rigorous framework. Any such claim must be supported by a checklist of conditions [@problem_id:4572134] [@problem_id:4572088]:

1.  **A Well-Defined Intervention and Consistency**: The exposure and the intervention to remove it must be clearly specified.
2.  **Exchangeability**: The exposed and unexposed groups must be comparable, either unconditionally (as in a randomized trial) or conditional on a sufficient set of measured confounders. This is the "no unmeasured confounding" assumption.
3.  **Positivity**: There must be both exposed and unexposed individuals at all levels of the confounding variables to allow for meaningful comparison.
4.  **SUTVA (Stable Unit Treatment Value Assumption)**: The outcome of one individual must not be affected by the exposure status of others (no interference), and there are no hidden variations of the exposure.
5.  **No Measurement Error**: The exposure, outcome, and all confounders must be measured accurately.
6.  **No Selection Bias**: The study population must be representative of the target population with respect to the causal question, with no biasing effects from loss to follow-up or self-selection.

Only when these conditions are met, or reasonably approximated, can we confidently state that an attributable fraction represents the "proportion of cases caused by" an exposure.