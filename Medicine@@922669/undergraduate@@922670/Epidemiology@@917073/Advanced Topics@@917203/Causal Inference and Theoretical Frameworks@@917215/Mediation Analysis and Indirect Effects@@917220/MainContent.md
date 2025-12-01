## Introduction
In the pursuit of scientific knowledge, we often begin by asking *if* an exposure causes an outcome. Does a new drug improve patient survival? Does a public policy reduce health disparities? While answering these questions is critical, a deeper understanding requires us to ask a more nuanced question: *how* and *why* does the effect occur? Causal mediation analysis provides a formal framework to answer this question by dissecting the causal pathways that link an exposure to an outcome. It moves beyond a "black box" view of causality to illuminate the underlying mechanisms, offering invaluable insights for refining interventions, targeting policies, and advancing theoretical knowledge.

This article provides a comprehensive introduction to the principles and practice of mediation analysis. It addresses the fundamental challenge of decomposing a total effect into its constituent parts—the portion that acts directly on the outcome and the portion that is channeled through an intermediate variable, or mediator. By mastering this framework, you will gain the tools to investigate the intricate processes that drive causal relationships.

Across three chapters, we will build your understanding from the ground up. The first chapter, **"Principles and Mechanisms,"** establishes the theoretical foundation using the [potential outcomes framework](@entry_id:636884), formally defining direct and indirect effects and exploring methods for their estimation. It will also confront key complications, including exposure-mediator interaction and the biases that arise in observational data. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates the power of these concepts by exploring their use in public health, epidemiology, health equity research, and the emerging field of explainable AI. Finally, the **"Hands-On Practices"** section provides an opportunity to apply these principles, tackling core challenges like identifiability, estimation with interaction, and sensitivity analysis. We begin by establishing the core principles that make this powerful analysis possible.

## Principles and Mechanisms

### A Framework for Causal Mediation: Potential Outcomes

While the total effect of an exposure on an outcome quantifies *if* and *how much* an exposure causes a change, mediation analysis aims to illuminate *how* this change occurs by investigating the causal pathways that link them. To formalize this inquiry, we rely on the **potential outcomes** framework, which provides a grammar for asking counterfactual questions.

Let us consider a binary exposure $A \in \{0,1\}$, a mediator $M$, and an outcome $Y$. The total effect of $A$ on $Y$ can be defined by comparing the potential outcomes $Y^1$ and $Y^0$, which represent the outcomes that would be observed for an individual if they were exposed ($A=1$) versus unexposed ($A=0$), respectively. To investigate mediation, we must expand this notation. Let $M^a$ be the potential value of the mediator if an individual were to receive exposure level $a$. Furthermore, let $Y^{a,m}$ denote the potential outcome if, possibly contrary to fact, an individual’s exposure were set to level $a$ and their mediator were set to level $m$.

To connect these abstract potential outcomes to observable data from a study, we must invoke a set of fundamental assumptions [@problem_id:4611460]:

1.  **Consistency**: The potential outcomes must be consistent with the observed data. This means that for an individual who is observed to have exposure $A=a$ and mediator $M=m$, their observed outcome $Y$ is equal to their potential outcome $Y^{a,m}$. Similarly, their observed mediator value is equal to their potential mediator value $M^a$. This assumption links the theoretical counterfactual world to the real, observed world.

2.  **No Interference**: A component of the **Stable Unit Treatment Value Assumption (SUTVA)**, this assumes that the potential outcomes for one individual do not depend on the exposure status of other individuals. In a study of a health outreach program, for instance, this means that one person receiving the outreach does not affect their neighbor's engagement or health outcome. This allows us to write potential outcomes like $Y_i(a,m)$ for individual $i$ without needing to specify the exposure status of all other individuals in the population [@problem_id:4611460].

3.  **Positivity**: For any combination of baseline covariates $L$, there must be a non-zero probability of being assigned to each exposure level. Furthermore, for any given exposure level and set of covariates, any relevant value of the mediator must have a non-zero probability of occurring. This ensures that we have data across all necessary strata to make comparisons and that our estimates are not based on [extrapolation](@entry_id:175955) to groups with no representation in the data [@problem_id:4611460].

Together, these assumptions form the logical foundation upon which we can define and, under further assumptions about confounding, identify direct and indirect effects from observed data.

### Decomposing Effects: Natural vs. Controlled Pathways

With the potential outcomes framework established, we can define distinct types of direct and indirect effects. The primary distinction is between *controlled* and *natural* effects.

The **Controlled Direct Effect (CDE)** quantifies the effect of the exposure on the outcome while the mediator is held constant at a specific level $m$ for everyone in the population. On the mean difference scale, it is defined as:
$$
\text{CDE}(m) = \mathbb{E}[Y^{1,m}] - \mathbb{E}[Y^{0,m}]
$$
The CDE answers the question: "What is the effect of the exposure if we could intervene and fix the mediator to level $m$ for all individuals?" While conceptually clear, its practical relevance can be limited, as it may not be feasible to set a mediator to a uniform value. Identification of the CDE requires controlling for confounding of the exposure-outcome and mediator-outcome pathways, but it does not involve the complex counterfactuals needed for natural effects [@problem_id:4611435].

More commonly, we are interested in decomposing the total effect as it occurs in the real world. This leads to the concepts of **Natural Direct Effect (NDE)** and **Natural Indirect Effect (NIE)**. These effects are based on "cross-world" counterfactuals, where the exposure and mediator are set to values they would have taken under different exposure scenarios.

The **Natural Direct Effect (NDE)** is the effect of the exposure on the outcome if the mediator were kept at the level it would have *naturally* taken in the absence of the exposure ($A=0$). It is defined as:
$$
\text{NDE} = \mathbb{E}[Y^{1, M^0}] - \mathbb{E}[Y^{0, M^0}]
$$
This represents the portion of the effect that does not operate through the mediator pathway influenced by the exposure.

The **Natural Indirect Effect (NIE)** is the effect of changing the mediator from the level it would naturally take under no exposure ($M^0$) to the level it would take under exposure ($M^1$), while holding the exposure itself constant. A standard definition fixes the exposure at the treatment level $A=1$:
$$
\text{NIE} = \mathbb{E}[Y^{1, M^1}] - \mathbb{E}[Y^{1, M^0}]
$$
This contrast isolates the effect transmitted through the mediator, representing the change in outcome that occurs because the exposure has changed the mediator's value [@problem_id:4611435].

A key property of these definitions is that on an additive scale, such as the risk difference, they provide a perfect decomposition of the total effect ($TE$). The total effect is $TE = \mathbb{E}[Y^1] - \mathbb{E}[Y^0] = \mathbb{E}[Y^{1,M^1}] - \mathbb{E}[Y^{0,M^0}]$. By adding and subtracting the term $\mathbb{E}[Y^{1,M^0}]$, we can show:
$$
TE = (\mathbb{E}[Y^{1,M^1}] - \mathbb{E}[Y^{1,M^0}]) + (\mathbb{E}[Y^{1,M^0}] - \mathbb{E}[Y^{0,M^0}]) = \text{NIE} + \text{NDE}
$$
This elegant decomposition is a cornerstone of mediation analysis, but as we will see, it relies on the choice of an additive scale and the absence of certain complexities [@problem_id:4611435]. The identification of NDE and NIE from observational data is more demanding than for CDE, typically requiring an additional "cross-world" independence assumption, such as the absence of any unmeasured factor that would confound the relationship between the potential mediator $M^0$ and the potential outcome $Y^{1,m}$.

### Estimation in Linear Systems: The Product of Coefficients

While the potential outcome definitions are foundational, they are abstract. In practice, we often estimate these effects using [parametric models](@entry_id:170911). The simplest and most illustrative case arises from a system of [linear models](@entry_id:178302) with no exposure-mediator interaction.

Consider a scenario where an exposure $X$ affects a continuous mediator $M$, which in turn affects a continuous or binary outcome $Y$. Suppose we can model these relationships as follows, after adjusting for any necessary confounders [@problem_id:4611430]:
1.  Mediator Model: $M = \alpha_0 + \alpha_1 X + \varepsilon_M$
2.  Outcome Model: $\mathbb{E}[Y \mid X, M] = \beta_0 + \beta_X X + \beta_M M$

Here, $\alpha_1$ represents the effect of a one-unit change in $X$ on the mean of $M$. The coefficient $\beta_M$ represents the effect of a one-unit change in $M$ on the mean of $Y$, holding $X$ constant. Under the necessary identification assumptions, we can show that the NIE is simply the product of these two coefficients.

Following the standard definition $NIE = \mathbb{E}[Y^{1, M^1}] - \mathbb{E}[Y^{1, M^0}]$ for a unit change in $X$ from 0 to 1, we can derive this result. From the models, $\mathbb{E}[M^x] = \alpha_0 + \alpha_1 x$ and $\mathbb{E}[Y^{x,m}] = \beta_0 + \beta_X x + \beta_M m$.
$$
\mathbb{E}[Y^{1, M^1}] = \beta_0 + \beta_X (1) + \beta_M \mathbb{E}[M^1] = \beta_0 + \beta_X + \beta_M (\alpha_0 + \alpha_1)
$$
$$
\mathbb{E}[Y^{1, M^0}] = \beta_0 + \beta_X (1) + \beta_M \mathbb{E}[M^0] = \beta_0 + \beta_X + \beta_M \alpha_0
$$
Subtracting these yields:
$$
NIE = (\beta_0 + \beta_X + \beta_M \alpha_0 + \beta_M \alpha_1) - (\beta_0 + \beta_X + \beta_M \alpha_0) = \alpha_1 \beta_M
$$
This intuitive **product-of-coefficients** method provides a direct way to compute the indirect effect. For example, if a policy increases fine particulate matter ($M$) by $\alpha_1 = 6.3 \, \mu g/m^3$ and each unit increase in $M$ increases asthma risk ($Y$) by $\beta_M = 0.004$, the indirect effect of the policy on asthma risk is simply $NIE = 6.3 \times 0.004 = 0.0252$ [@problem_id:4611430]. Similarly, in this simple model, the NDE corresponds to the coefficient $\beta_X$.

### Complications in Effect Decomposition

#### The Role of Exposure-Mediator Interaction

The simple decomposition and the equivalence of NDE and CDE break down in the presence of **exposure-mediator interaction**. This occurs when the effect of the mediator on the outcome differs by exposure status, or conversely, when the effect of the exposure on the outcome differs depending on the level of the mediator.

Consider an outcome model that includes an interaction term:
$$
Y = \beta_0 + \beta_1 A + \beta_2 M + \beta_3 AM + \varepsilon_Y
$$
In this case, the CDE is no longer constant but depends on the level $m$ at which the mediator is controlled:
$$
CDE(m) = \mathbb{E}[Y^{1,m} - Y^{0,m}] = (\beta_1 + \beta_3 m)
$$
The NDE, which sets the mediator to its value under non-exposure ($M^0$), becomes:
$$
NDE = \mathbb{E}[Y^{1, M^0} - Y^{0, M^0}] = \beta_1 + \beta_3 \mathbb{E}[M^0]
$$
This reveals a crucial distinction: in the presence of interaction ($\beta_3 \neq 0$), the NDE is not equal to the CDE, unless the level $m$ chosen for the CDE happens to equal the average level of the mediator in the unexposed group, $\mathbb{E}[M^0]$ [@problem_id:4611468] [@problem_id:4611435]. For example, if $\beta_3 = -0.1$, the expected mediator level under no exposure is $\mathbb{E}[M^0] = 10$, and we evaluate the CDE at a level of $m=15$, the difference between the two effects is $\Delta = NDE - CDE(15) = \beta_3(\mathbb{E}[M^0] - 15) = -0.1(10 - 15) = 0.5$ [@problem_id:4611468].

When interaction is present, the two-way decomposition ($TE = NDE + NIE$) can be expanded into a **four-way decomposition** to provide a more nuanced understanding of the causal effects. On an additive scale, the total effect can be partitioned into [@problem_id:4611427]:
1.  **Controlled Direct Effect (CDE)**: The effect of the exposure when the mediator is absent (or at its reference level, $m=0$). This corresponds to $\beta_1$ in the interaction model.
2.  **Pure Indirect Effect (PIE)**: The effect of the mediator in the absence of the exposure. This corresponds to $\beta_2 (\mathbb{E}[M^1] - \mathbb{E}[M^0])$.
3.  **Mediated Interaction (INTmed)**: The portion of the interaction effect that is mediated through the exposure's influence on the mediator. This corresponds to $\beta_3 (\mathbb{E}[M^1] - \mathbb{E}[M^0])$.
4.  **Reference Interaction (INTref)**: The portion of the interaction effect that is due to subjects having the mediator at its reference level even without exposure. This corresponds to $\beta_3 \mathbb{E}[M^0]$.

The sum of these four components recovers the total effect: $TE = CDE + PIE + INTmed + INTref$. This decomposition isolates the effect due purely to mediation (PIE), purely to direct effects (CDE), and the two components of their interaction.

#### The Importance of Scale: Collapsibility and Effect Measures

The elegant additive decomposition of effects is highly dependent on the chosen effect measure. The **risk difference (RD)** is an additive measure, and on this scale, effects are **collapsible**. This means that if a variable (like a mediator) is not a confounder, the marginal (overall) effect will be a weighted average of the stratum-specific effects.

This property does not hold for multiplicative measures like the **risk ratio (RR)** and, most notoriously, the **odds ratio (OR)**. The odds ratio is **non-collapsible**. This means that the marginal OR can differ from the conditional ORs within strata of another variable, even if that variable is not a confounder.

Consider a scenario where an exposure $X$ has no direct effect on an outcome $Y$ within levels of a mediator $M$. This means the conditional risk differences and odds ratios are both null ($0$ and $1$, respectively). If $X$ causes $M$ and $M$ causes $Y$, a total effect will be induced. On the risk difference scale, the total effect is purely an indirect effect. However, on the odds ratio scale, the marginal OR can be substantially different from $1$ due to non-collapsibility, giving the false impression of a direct effect if one were to misinterpret the marginal measure [@problem_id:4611444].

For instance, if the risk of an outcome is $0.09$ for the unexposed and $0.17$ for the exposed, the total effect is a risk difference of $0.08$. If the controlled direct effect is $0$, this $0.08$ is purely mediated. The marginal odds ratio, however, is approximately $2.07$. An analyst seeing a conditional OR of $1$ and a marginal OR of $2.07$ might be confused, but this is a natural mathematical property of the odds ratio, not a sign of confounding. This highlights that a claim like $OR_{TE} = OR_{NDE} \times OR_{NIE}$ is generally false [@problem_id:4611435]. The choice of scale is therefore not arbitrary; it fundamentally shapes the interpretation and decomposition of causal effects.

### Challenges in Observational Data: Bias and Its Remedies

In randomized trials, confounding of the exposure-outcome relationship is controlled by design. However, mediation analysis introduces new challenges, as the mediator is almost always observational. This opens the door to several forms of bias.

#### Confounding and Collider Bias

The most significant challenge in mediation analysis is confounding of the mediator-outcome relationship. To estimate the effect of the mediator on the outcome ($\beta_M$), one must adjust for all common causes of $M$ and $Y$. If there is an unmeasured common cause, say $U$, the estimate of $\beta_M$ and the subsequent indirect effect will be biased.

A more subtle issue is **[collider bias](@entry_id:163186)**. To estimate the direct effect of an exposure $E$ on an outcome $Y$, we must condition on the mediator $M$. However, if an unmeasured confounder $U$ of the $M-Y$ relationship exists, the [causal structure](@entry_id:159914) contains the path $E \to M \leftarrow U \to Y$. In this structure, the mediator $M$ is a **collider**. Conditioning on a collider opens the non-causal path between its parents. Therefore, by conditioning on $M$ to estimate the direct effect, we inadvertently open a spurious pathway between $E$ and $Y$ through $U$, inducing bias in our estimate of the direct effect [@problem_id:4611442]. This is a pernicious problem because the very act of adjusting for the mediator, which is necessary to separate direct from indirect effects, can itself create bias.

Selection bias is another form of [collider bias](@entry_id:163186). If selection into the study sample ($S=1$) is caused by both the mediator and the outcome (i.e., $M \to S \leftarrow Y$), then restricting the analysis to the selected sample is equivalent to conditioning on a [collider](@entry_id:192770), which can distort the true associations [@problem_id:4611442].

#### Quantifying Uncertainty: Sensitivity Analysis for Unmeasured Confounding

Since we can rarely be certain that we have measured all $M-Y$ confounders, it is crucial to assess how sensitive our conclusions are to potential unmeasured confounding. **Sensitivity analysis** provides a quantitative framework for this assessment.

Suppose we have an unmeasured confounder $C$ that affects the mediator $M$ with strength $\gamma_C$ and the outcome $Y$ with strength $\delta_C$. In a naive regression of $Y$ on $X$ and $M$ that omits $C$, the estimated coefficient for the mediator, $\widehat{\beta}_M$, will be biased. It can be shown that the true coefficient, $\beta_M$, is related to the biased estimate by [@problem_id:4611426]:
$$
\beta_M = \widehat{\beta}_M - \frac{\delta_C \gamma_C}{\operatorname{Var}(M \mid X)}
$$
The bias term is a function of the product of the confounding paths ($\delta_C \gamma_C$) and the residual variance of the mediator. An analyst can postulate plausible values for the sensitivity parameters $\gamma_C$ and $\delta_C$ and calculate what the true indirect effect *would be* under that degree of confounding. For example, if a naive analysis yields a mediator coefficient $\widehat{\beta}_M=1.44$, but we believe an unmeasured confounder exists with effects $\gamma_C=0.80$ and $\delta_C=0.50$ and the residual mediator variance is $2.00$, the corrected coefficient would be $\beta_M = 1.44 - \frac{0.80 \times 0.50}{2.00} = 1.24$. The corrected NIE would then be calculated using this adjusted value, leading to a more robust conclusion [@problem_id:4611426].

#### The Impact of Measurement Error

Another practical challenge is **measurement error**. If the mediator $M$ is measured with error, this can also lead to biased estimates. Under a classical measurement error model, the observed mediator $M^*$ is the true mediator plus random noise: $M^* = M + U$, where $U$ is independent of all other variables.

When we naively regress the outcome $Y$ on the exposure $X$ and the error-prone mediator $M^*$, the resulting coefficient for the mediator, $\beta_M^*$, will be biased, typically towards the null. This is known as **attenuation**. The relationship between the true coefficient $\beta_M$ and the biased one $\beta_M^*$ is given by:
$$
\beta_M^* = \beta_M \frac{\operatorname{Var}(M_{\text{true_residual}})}{\operatorname{Var}(M_{\text{true_residual}}) + \operatorname{Var}(U)}
$$
where $\operatorname{Var}(M_{\text{true_residual}})$ is the variance of the true mediator not explained by the exposure, and $\operatorname{Var}(U)$ is the variance of the measurement error. The attenuation factor is always less than 1, meaning $\beta_M^*$ will be smaller in magnitude than $\beta_M$. Consequently, the naive indirect effect, calculated as $\alpha_X \beta_M^*$, will be an underestimate of the true indirect effect $\alpha_X \beta_M$ [@problem_id:4611458]. If the true effect of a mediator is $\beta_M=1.5$ but the measurement error is large, the observed effect might be only $\beta_M^*=0.6$, leading to a significant underestimation of the mediated pathway.

### Extending the Framework: The Case of Multiple Mediators

The principles of mediation analysis can be extended to more complex scenarios involving multiple mediators. These mediators can operate in **parallel** (where the exposure affects multiple mediators independently) or in **series** (where one mediator in turn affects another).

Consider a system with two mediators, $M_1$ and $M_2$, where the exposure $X$ affects both, and $M_1$ also affects $M_2$. The causal pathways can be represented by a series of linear equations [@problem_id:4611436]:
-   $M_1 = a_1 X + \dots$
-   $M_2 = a_2 X + d M_1 + \dots$
-   $Y = c X + b_1 M_1 + b_2 M_2 + \dots$

The total natural indirect effect is the sum of the effects of all pathways that originate at $X$, pass through at least one mediator, and end at $Y$. In this system, there are three such pathways:
1.  The path through $M_1$ alone: $X \to M_1 \to Y$. Its effect is $a_1 b_1$.
2.  The path through $M_2$ alone: $X \to M_2 \to Y$. Its effect is $a_2 b_2$.
3.  The serial path through $M_1$ and then $M_2$: $X \to M_1 \to M_2 \to Y$. Its effect is the product of the coefficients along the path: $a_1 d b_2$.

The total natural indirect effect is the sum of these three path-specific effects:
$$
\text{NIE}_{\text{total}} = a_1 b_1 + a_2 b_2 + a_1 d b_2
$$
For example, if a community intervention ($X$) improves diet ($M_1$, $a_1=0.8$) and fitness ($M_2$, $a_2=0.5$), and better diet also improves fitness ($d=0.4$), with diet and fitness having effects on a health index ($Y$) of $b_1=1.2$ and $b_2=0.9$ respectively, the total indirect effect would be $NIE = (0.8)(1.2) + (0.5)(0.9) + (0.8)(0.4)(0.9) = 1.698$ [@problem_id:4611436]. This path-tracing approach, while powerful, relies on the strong assumptions of linearity and no unmeasured confounding between any two variables in the system.