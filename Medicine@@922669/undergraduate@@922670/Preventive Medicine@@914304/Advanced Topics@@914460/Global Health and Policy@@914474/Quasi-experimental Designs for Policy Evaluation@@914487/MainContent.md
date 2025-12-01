## Introduction
Evaluating the impact of public health policies is a critical but complex task. How do we know if a new law, regulation, or program truly improved health outcomes, or if the changes we observe would have happened anyway? This fundamental question of causality—comparing the world as it is with a world that could have been—sits at the heart of evidence-based policymaking. While randomized controlled trials (RCTs) are often considered the gold standard for establishing causality, they are frequently impractical, unethical, or politically impossible to implement for large-scale social policies. This creates a significant knowledge gap, leaving policymakers without the rigorous evidence needed to make informed decisions.

This article bridges that gap by providing a comprehensive introduction to quasi-experimental designs, a powerful toolkit for conducting rigorous causal inference using observational data. You will learn to move beyond simple before-and-after comparisons to construct credible counterfactuals and isolate the true impact of public health interventions. The content is structured to guide you from foundational theory to practical application across three distinct chapters.

First, **"Principles and Mechanisms"** will introduce the Potential Outcomes Framework, the conceptual bedrock of modern causal inference. We will dissect the core assumptions that make causal claims possible and provide a systematic overview of the primary designs, including Difference-in-Differences, Interrupted Time Series, and Regression Discontinuity. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how these methods are applied to solve real-world problems in public health, from evaluating staggered policy rollouts to assessing health equity and informing economic analyses. Finally, **"Hands-On Practices"** will solidify your understanding through practical exercises that challenge you to apply these techniques to realistic scenarios. By the end of this article, you will have a robust understanding of how to use [quasi-experimental methods](@entry_id:636714) to generate credible evidence on the effects of policies that shape the health of populations.

## Principles and Mechanisms

The evaluation of public health policy presents a formidable challenge rooted in a fundamental question of causality: what would have happened in the absence of the policy? Answering this requires comparing the observed reality with an unobserved counterfactual. This chapter introduces the core principles and theoretical frameworks that allow researchers to construct credible counterfactuals using quasi-experimental data, thereby enabling rigorous causal inference. We will dissect the foundational concepts of potential outcomes, explore the critical assumptions that make causal claims possible, and provide a systematic overview of the primary quasi-experimental designs used in [policy evaluation](@entry_id:136637).

### The Potential Outcomes Framework

At the heart of modern causal inference lies the **Potential Outcomes Framework**, also known as the Rubin Causal Model. This framework formalizes the "what if" question by positing that for any unit of analysis—be it an individual, a community, or a state—there exists a potential outcome for each possible treatment or exposure status.

Let us consider a policy or treatment, denoted by a binary indicator $D$, where $D=1$ if a unit is treated (e.g., exposed to a new policy) and $D=0$ if it is not (the control condition). For each unit $i$, we can define two potential outcomes:

*   $Y_i(1)$: The outcome that would be observed for unit $i$ if it were treated ($D_i=1$).
*   $Y_i(0)$: The outcome that would be observed for the *same* unit $i$ if it were not treated ($D_i=0$).

The **individual-level causal effect** for unit $i$ is the difference between these two potential outcomes: $\tau_i = Y_i(1) - Y_i(0)$. The fundamental problem of causal inference is that we can only ever observe one of these potential outcomes for any given unit. The observed outcome, $Y_i$, can be expressed as $Y_i = D_i Y_i(1) + (1-D_i)Y_i(0)$. The potential outcome that is not observed is the counterfactual.

While individual-level effects are unobservable, we can estimate average causal effects across a population. The most common of these is the **Population Average Treatment Effect (ATE)**, which is the expected value of the individual-level effect over the entire population of interest [@problem_id:4566457]. It is defined as:

$\tau_{ATE} = E[Y(1) - Y(0)]$

Here, $Y(1)$ represents the health outcome that would be observed for an individual if a policy were in place, and $Y(0)$ is the outcome for the same individual if the policy were not in place. For instance, in evaluating a statewide mandate for no-cost influenza vaccination, $\tau_{ATE}$ would represent the average difference in an outcome like influenza-related hospitalizations across all individuals in the state, comparing the hypothetical scenario where the mandate is universally in effect to one where it is not [@problem_id:4566457].

Another crucial estimand is the **Average Treatment Effect on the Treated (ATT)**. This measures the average causal effect specifically for the subpopulation that was actually exposed to the treatment or policy:

$\tau_{ATT} = E[Y(1) - Y(0) \mid D=1]$

The distinction between ATE and ATT is not merely academic; it is of profound policy relevance, especially when treatment effects are **heterogeneous** (differing across subgroups) and when there is **selection into treatment** (the characteristics of those who get treated differ from the general population).

Consider an evaluation of a voluntary smoke-free workplace policy [@problem_id:4566518]. Suppose the policy is more effective for high-exposure workers (e.g., those in smoky environments) than for low-exposure workers. If firms with high-exposure workforces are more likely to adopt the policy, the group of "treated" workers will be disproportionately composed of those who stand to benefit most. In this scenario, the ATT—the observed effect among adopting firms—will be larger than the ATE, which is the effect one would expect if the policy were mandated for all firms. A hypothetical example illustrates this clearly:
*   High-exposure workers see a reduction of $3$ sick days per year ($\tau_H = -3$).
*   Low-exposure workers see a reduction of $0.5$ sick days per year ($\tau_L = -0.5$).
*   If adopters are $60\%$ high-exposure and the general workforce is $30\%$ high-exposure, we would calculate $\tau_{ATT} = 0.60(-3) + 0.40(-0.5) = -2.0$ sick days.
*   The ATE, however, would be $\tau_{ATE} = 0.30(-3) + 0.70(-0.5) = -1.25$ sick days.
Extrapolating the success observed among voluntary adopters (the ATT) to predict the outcome of a universal mandate (the ATE) would lead to a significant overestimation of the policy's average benefit [@problem_id:4566518].

### Core Assumptions for Causal Inference

The ability to move from observed data to causal estimands like ATE or ATT rests on a set of critical, untestable assumptions. The most foundational of these is the **Stable Unit Treatment Value Assumption (SUTVA)**. SUTVA is a compound assumption comprising two distinct components:

1.  **No Interference**: This component asserts that the potential outcomes for any given unit depend only on that unit's own treatment assignment. The treatment status of one unit does not affect the outcome of another unit.

2.  **Consistency**: This component requires that the treatment is well-defined, meaning there are no hidden variations of the treatment that would lead to different outcomes. The observed outcome for a treated unit is indeed its potential outcome under that specific treatment.

Violations of the no-interference component are common in public health and are often referred to as **spillover effects** or **contagion**. Consider a [policy evaluation](@entry_id:136637) comparing obesity trends in city zip codes that implemented a nutrition labeling ordinance to suburban zip codes that did not [@problem_id:4566435]. If residents of the "untreated" suburban zip codes frequently commute into the city to dine, they are exposed to the calorie labels. This exposure can influence their health outcomes. Consequently, the outcome in the untreated zip code is affected by the treatment status of its neighbor. This violates the no-interference assumption because the potential outcomes of a "control" unit are not independent of the treatment assignment of other units.

Such spillovers are a primary reason why quasi-experimental designs are often preferred over large-scale randomized trials for [policy evaluation](@entry_id:136637). Randomly assigning half of the states to adopt a vaccination mandate and half to serve as controls is not only politically infeasible and ethically problematic, but it is also statistically compromised by spillovers [@problem_id:4566430]. Disease transmission and media influence do not respect state borders, violating SUTVA and biasing simple comparisons between the randomized groups.

### Threats to Internal Validity in Naive Designs

Before delving into specific quasi-experimental designs, it is instructive to understand why simpler approaches, such as a basic pre-post comparison, are often inadequate. The goal of a study is to achieve high **internal validity**, meaning that the observed association between the policy and the outcome can be confidently attributed to a causal relationship. Naive designs are vulnerable to numerous threats to internal validity, which represent plausible alternative explanations for an observed change.

Imagine a public health department launches a vaccination outreach campaign in neighborhoods with low baseline coverage and measures coverage again after the campaign [@problem_id:4566493]. An increase in coverage might not be due to the campaign, but rather to:

*   **History**: An external event occurs at the same time as the intervention. For example, a national media campaign about a measles outbreak could increase vaccination demand everywhere, confounding the effect of the local outreach.
*   **Maturation**: Natural trends or processes that occur over time. Children continuously age into vaccine eligibility, and seasonal patterns (like back-to-school rushes) can influence vaccination rates independently of the campaign.
*   **Instrumentation**: A change in the way the outcome is measured. If the immunization registry updates its software to be better at deduplicating records, this could cause an apparent (but artificial) change in the calculated coverage rate.
*   **Regression to the Mean**: A statistical artifact that occurs when units are selected for treatment based on extreme scores. Neighborhoods were chosen because their coverage was unusually low. Due to random fluctuation, a subsequent measurement is likely to be closer to the average, creating the illusion of improvement even without any intervention.

Quasi-experimental designs are structured to mitigate these and other threats, allowing for more credible causal claims.

### A Taxonomy of Quasi-Experimental Designs

Quasi-experimental designs use observational data but leverage specific features of the policy implementation or [data structure](@entry_id:634264) to mimic the counterfactual logic of a randomized experiment. The choice of design depends on the nature of the policy and the available data. Below is a survey of the most prominent methods. [@problem_id:4566462]

#### Difference-in-Differences (DiD)

The **Difference-in-Differences (DiD)** design is one of the most widely used and intuitive [quasi-experimental methods](@entry_id:636714). It is applicable when outcome data are available for a group exposed to a policy (the treated group) and a group not exposed (the comparison group), both before and after the policy's implementation.

The core idea is to "difference out" unobserved confounding factors. First, one calculates the change in the outcome from the pre-period to the post-period for the treated group. This change reflects both the policy's effect and any general time trends. Second, one calculates the pre-post change for the comparison group, which is assumed to capture only the general time trend. The difference between these two differences is the DiD estimator of the policy's effect.

The canonical two-group, two-period DiD estimator is:
$\hat{\tau}_{DID} = (\bar{Y}_{1,post} - \bar{Y}_{1,pre}) - (\bar{Y}_{0,post} - \bar{Y}_{0,pre})$
where $\bar{Y}_{g,t}$ is the mean outcome for group $g \in \{1,0\}$ in period $t \in \{\text{pre}, \text{post}\}$.

For example, to evaluate a statewide smoke-free policy on acute myocardial infarction (AMI) rates, we can compare the change in AMI rates in the state that adopted the policy (State S) to the change in a neighboring state that did not (State C) [@problem_id:4566478]. If AMI rates in State S fell from 210 to 180 (a change of -30), while rates in State C fell from 205 to 195 (a change of -10), the DiD estimate of the policy's effect would be $(-30) - (-10) = -20$ AMI hospitalizations per 100,000.

The critical identifying assumption of DiD is the **[parallel trends assumption](@entry_id:633981)**. This assumption states that, in the absence of the policy, the average outcome in the treated group would have followed the same trend as the average outcome in the comparison group. Formally, $E[Y_{post}(0) - Y_{pre}(0) \mid D=1] = E[Y_{post}(0) - Y_{pre}(0) \mid D=0]$. This assumption is fundamentally untestable because it involves the counterfactual trend of the treated group. However, its plausibility can be strongly supported by examining pre-intervention data. If the two groups exhibited parallel trends in the outcome for multiple periods before the intervention, it lends credibility to the assumption that they would have continued to do so in its absence [@problem_id:4566501]. For instance, if pre-policy tuberculosis testing rates in two states showed a constant difference over several months, this would support the [parallel trends assumption](@entry_id:633981) for evaluating a policy implemented in one of the states.

#### Interrupted Time Series (ITS)

The **Interrupted Time Series (ITS)** design is powerful when a long time series of an outcome is available for a single population that experiences an intervention at a known point in time. The design uses the pre-intervention trend to establish a counterfactual for the post-intervention period.

ITS is often implemented using a **segmented linear regression model**. For an intervention at time $t=0$, the model can be specified as:
$Y_t = \beta_0 + \beta_1 t + \beta_2 I_t + \beta_3 (t \times I_t) + \varepsilon_t$
where $Y_t$ is the outcome at time $t$, $I_t$ is an indicator equal to 1 for periods post-intervention ($t \ge 0$) and 0 otherwise, and $(t \times I_t)$ is an interaction term.

The coefficients have precise and powerful interpretations [@problem_id:4566428]:
*   $\beta_1$ is the slope of the pre-intervention trend.
*   $\beta_2$ represents the **immediate change in the level** of the outcome at the moment of intervention.
*   $\beta_3$ represents the **change in the slope** of the trend from the pre- to the post-intervention period.

A key assumption for ITS is the absence of other simultaneous events, or **concurrent shocks**, that could have affected the outcome at the same time as the policy. For example, ITS is well-suited for evaluating a national [folic acid](@entry_id:274376) fortification policy by examining monthly neural tube defect rates over many years, provided no other major related policy was enacted at the same time [@problem_id:4566462].

#### Regression Discontinuity Design (RDD)

The **Regression Discontinuity Design (RDD)** is one of the most credible [quasi-experimental methods](@entry_id:636714). It can be used when assignment to a treatment is determined, either deterministically or probabilistically, by whether an observed continuous variable (the **running variable**) is above or below a specific **cutoff**. The key insight is that individuals just on either side of the cutoff are likely to be very similar in all other respects, creating a local randomized experiment. The identifying assumption is the continuity of potential outcomes at the cutoff.

There are two forms of RDD [@problem_id:4566496]:

*   **Sharp RDD**: Treatment assignment is a deterministic function of the running variable. For a running variable $X_i$ and cutoff $c$, everyone with $X_i \ge c$ is treated and everyone with $X_i  c$ is not. The causal effect at the cutoff is simply the difference in the average outcome for units just above and just below the cutoff: $\tau_{SRD} = \lim_{x \downarrow c} E[Y_i \mid X_i = x] - \lim_{x \uparrow c} E[Y_i \mid X_i = x]$.

*   **Fuzzy RDD**: Crossing the cutoff changes the probability of receiving treatment but does not determine it perfectly. For example, an age-based eligibility for a screening program may see some eligible individuals refuse screening and some ineligible individuals get screened for other reasons. In this case, the design becomes an [instrumental variable analysis](@entry_id:166043) (see below), where eligibility at the cutoff is the instrument for treatment. The effect is estimated by the **Wald ratio**: the jump in the outcome at the cutoff divided by the jump in the probability of treatment at the cutoff. This identifies a **Local Average Treatment Effect (LATE)** for the subpopulation of "compliers" whose treatment status was changed by crossing the threshold.

#### Other Key Designs

Several other designs are essential components of the policy evaluator's toolkit:

*   **Instrumental Variables (IV)**: This method is used to address unobserved confounding. It requires an **instrument**—a variable that is correlated with the treatment ($D_i$) but is not correlated with any unobserved confounders and affects the outcome ($Y_i$) only through its effect on the treatment. A valid instrument provides a source of "as-if random" variation in treatment assignment. [@problem_id:4566462]

*   **Propensity Score (PS) Methods**: When selection into treatment is based on a rich set of observable characteristics, PS methods can create comparable treatment and control groups. The [propensity score](@entry_id:635864) is the conditional probability of receiving treatment given these characteristics. By matching, stratifying, or weighting units based on their propensity score, one can adjust for observed confounding under the assumption of **conditional exchangeability** (no unmeasured confounders). [@problem_id:4566462]

*   **Synthetic Control (SC)**: This method is tailored for comparative case studies, often when only a single unit (e.g., a city or state) receives a treatment. It constructs a counterfactual for the treated unit by creating a data-driven weighted average of untreated "donor" units. The weights are chosen such that the resulting "[synthetic control](@entry_id:635599)" best reproduces the pre-intervention outcome trajectory of the treated unit. [@problem_id:4566462]

*   **Event Study (ES)**: This design is a generalization of DiD used for settings with **[staggered adoption](@entry_id:636813)**, where different units implement a policy at different times. By aligning units relative to their "event date" (when they adopted the policy), one can estimate dynamic treatment effects and explicitly test for pre-intervention parallel trends and treatment anticipation effects. [@problem_id:4566462]

### Conclusion: Choosing the Right Design

The principles and mechanisms discussed in this chapter form the bedrock of modern [policy evaluation](@entry_id:136637). The journey begins with the conceptual clarity of the [potential outcomes framework](@entry_id:636884), which forces us to define the precise causal question we seek to answer. Understanding the key assumptions, like SUTVA, and the common threats to internal validity, like history and maturation, allows us to recognize the limitations of naive comparisons.

Ultimately, the choice of a specific quasi-experimental design is not arbitrary. It is dictated by the realities of the policy implementation—when it occurred, who it affected, how assignment was determined—and the structure of the available data. When a randomized experiment is not a viable option, this rigorous toolkit provides a path forward, allowing researchers and policymakers to generate credible evidence on the causal effects of interventions that shape public health.