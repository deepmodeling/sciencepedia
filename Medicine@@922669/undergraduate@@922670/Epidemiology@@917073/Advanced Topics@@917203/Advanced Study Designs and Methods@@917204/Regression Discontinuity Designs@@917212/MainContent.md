## Introduction
Estimating the true causal effect of an intervention—from a new drug to a public health policy—is a central challenge in epidemiology and social sciences. In the absence of a randomized controlled trial, researchers need credible methods to distinguish correlation from causation. The Regression Discontinuity Design (RDD) emerges as one of the most powerful and intuitive [quasi-experimental methods](@entry_id:636714) for this task. It provides a rigorous framework for evaluating programs that use a specific threshold or cutoff to determine eligibility, creating a unique opportunity for causal inference. RDD leverages these real-world rules to mimic a randomized experiment for individuals right at the edge of the cutoff. However, its power comes with a set of critical assumptions and potential pitfalls that must be thoroughly understood and checked. This article provides a comprehensive guide to understanding and applying this elegant design.

Across three chapters, you will gain a robust understanding of RDD. The first chapter, **Principles and Mechanisms**, will dissect the core logic of both Sharp and Fuzzy RDD, explaining the underlying assumptions and key parameters. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the versatility of RDD with real-world examples from public health, policy, [environmental science](@entry_id:187998), and even neuroscience. Finally, the **Hands-On Practices** chapter will offer interactive exercises to solidify your understanding and build practical skills in [data visualization](@entry_id:141766) and estimation for RDD analysis. By navigating these sections, you will learn not only the theory behind RDD but also how to critically apply and interpret it in practice.

## Principles and Mechanisms

### The Core Logic of the Regression Discontinuity Design

The Regression Discontinuity (RD) design is a powerful quasi-experimental method for causal inference that emulates a randomized controlled trial in specific circumstances. Its logic applies when an intervention or treatment is assigned based on whether an individual's observed value on a continuous measure, known as the **running variable**, falls above or below a specific **cutoff** point. For instance, a public health program might offer a free smoking cessation program to patients whose respiratory risk score exceeds a certain threshold, or a preventive therapy might be recommended for patients whose blood pressure is above a specific value [@problem_id:4629832] [@problem_id:4629794].

At its heart, the RD design rests on a simple and compelling intuition: individuals with scores on the running variable that are just barely on either side of the cutoff are likely to be very similar. Consider two individuals whose risk scores are infinitesimally different, one just below the cutoff and one just above. It is reasonable to assume that, on average, these two individuals are comparable in all other respects—both observed and unobserved—that might influence the outcome of interest. The only systematic difference between them is that one is assigned to the treatment group and the other to the control group. Therefore, any abrupt change, or "discontinuity," in the average outcome observed precisely at the cutoff can be attributed to the causal effect of the treatment.

This "as-good-as-randomized" comparison at the threshold is the foundational strength of the RD design. To formalize this, let us define the key components:

*   The **running variable**, denoted by $X_i$ for individual $i$, is the continuous variable used to determine treatment eligibility. It must be a pre-treatment measure that is not itself affected by the treatment.
*   The **cutoff**, denoted by $c$, is the pre-specified threshold value of the running variable that determines assignment.
*   The **treatment indicator**, denoted by $D_i$, is a binary variable equal to $1$ if individual $i$ receives the treatment and $0$ otherwise.

There are two primary forms of the RD design, distinguished by the nature of the assignment rule.

### The Sharp Regression Discontinuity Design

In a **Sharp Regression Discontinuity (SRD)** design, treatment assignment is a deterministic function of the running variable. All individuals at or above the cutoff receive the treatment, and all individuals below the cutoff do not. The assignment rule is given by a simple indicator function:

$D_i = \mathbf{1}\{X_i \ge c\}$

where $\mathbf{1}\{\cdot\}$ is the indicator function, equal to 1 if the condition inside is true and 0 otherwise. This creates a perfect, sharp jump in the probability of treatment at the cutoff, from 0 to 1.

To formally identify the causal effect, we use the **potential outcomes framework**. For each individual $i$, we define two potential outcomes: $Y_i(1)$, the outcome that would be observed if the individual received the treatment, and $Y_i(0)$, the outcome that would be observed if they did not. The individual causal effect is the unobservable difference, $Y_i(1) - Y_i(0)$. The observed outcome is $Y_i = D_i Y_i(1) + (1-D_i) Y_i(0)$.

The parameter of interest in an RD design is the **Average Treatment Effect at the Cutoff**, which is the average effect for the subpopulation of individuals with a running variable value exactly equal to $c$:

$\tau_{SRD} = \mathbb{E}[Y_i(1) - Y_i(0) \mid X_i = c]$

This is a **local average treatment effect** because it pertains only to the individuals "at the margin" of eligibility.

The key assumption that allows us to identify this parameter is the **continuity of conditional potential outcomes**. We must assume that the average potential outcomes, conditional on the running variable, are continuous functions of $x$ at the cutoff $c$. Formally, for $d \in \{0,1\}$:

$\lim_{x \to c} \mathbb{E}[Y_i(d) \mid X_i=x] = \mathbb{E}[Y_i(d) \mid X_i=c]$

This assumption posits that in the absence of the treatment rule, the relationship between the running variable and the average outcomes would be smooth through the cutoff point. Any discontinuity observed in the data must therefore arise from the treatment itself [@problem_id:4629828].

Under this assumption, we can identify $\tau_{SRD}$ using observable data. Consider the [conditional expectation](@entry_id:159140) of the *observed* outcome, $\mathbb{E}[Y_i \mid X_i=x]$.
*   For individuals just above the cutoff ($x \to c^+$), they are all treated, so $\mathbb{E}[Y_i \mid X_i=x] = \mathbb{E}[Y_i(1) \mid X_i=x]$.
*   For individuals just below the cutoff ($x \to c^-$), they are all untreated, so $\mathbb{E}[Y_i \mid X_i=x] = \mathbb{E}[Y_i(0) \mid X_i=x]$.

Taking the limits and applying the continuity assumption:
$\lim_{x \downarrow c} \mathbb{E}[Y_i \mid X_i=x] = \lim_{x \downarrow c} \mathbb{E}[Y_i(1) \mid X_i=x] = \mathbb{E}[Y_i(1) \mid X_i=c]$
$\lim_{x \uparrow c} \mathbb{E}[Y_i \mid X_i=x] = \lim_{x \uparrow c} \mathbb{E}[Y_i(0) \mid X_i=x] = \mathbb{E}[Y_i(0) \mid X_i=c]$

Therefore, the difference in the [one-sided limits](@entry_id:138326) of the observed outcome regression function at the cutoff identifies the causal effect of interest [@problem_id:4629794]:

$\tau_{SRD} = \lim_{x \downarrow c} \mathbb{E}[Y_i \mid X_i=x] - \lim_{x \uparrow c} \mathbb{E}[Y_i \mid X_i=x] = \mathbb{E}[Y_i(1) \mid X_i=c] - \mathbb{E}[Y_i(0) \mid X_i=c]$

It is crucial to understand that this estimand is local. Generalizing the effect found at $c$ to populations with running variable values far from $c$ is not warranted without making strong, additional assumptions, such as the treatment effect being homogeneous across all values of $X_i$ (i.e., $\mathbb{E}[Y_i(1) - Y_i(0) \mid X_i=x]$ is constant for all $x$). In most epidemiological contexts, this is an implausible assumption; the effect of a therapy for individuals at high risk (far above $c$) may be very different from its effect on individuals at marginal risk (near $c$) [@problem_id:4629806].

### The Fuzzy Regression Discontinuity Design

In many real-world settings, the assignment rule is not perfectly deterministic. For example, a guideline may recommend treatment for individuals with a risk score $X_i \ge c$, but some eligible patients may decline the treatment, while some ineligible patients may receive it through clinical discretion or other means [@problem_id:4629774]. This scenario gives rise to the **Fuzzy Regression Discontinuity (FRD)** design.

In an FRD design, crossing the cutoff $c$ does not perfectly determine treatment status but instead induces a discontinuous change in the *probability* of receiving treatment. Formally:

$\lim_{x \downarrow c} \mathbb{P}(D_i=1 \mid X_i=x) \neq \lim_{x \uparrow c} \mathbb{P}(D_i=1 \mid X_i=x)$

However, the jump is not from 0 to 1. The FRD framework can be understood as a special case of an **Instrumental Variable (IV)** analysis, where the eligibility rule, $Z_i = \mathbf{1}\{X_i \ge c\}$, serves as an instrument for the treatment status, $D_i$ [@problem_id:4629774]. For this local IV strategy to be valid, several conditions must hold:

1.  **Instrument Relevance:** The instrument must be correlated with the treatment. In the FRD context, this means the probability of treatment must actually jump at the cutoff. The denominator of the estimand below must be non-zero.
2.  **Exclusion Restriction:** The instrument ($Z_i$) can only affect the outcome ($Y_i$) through its effect on the treatment ($D_i$). This is implicitly satisfied by the same continuity of potential outcomes assumption used in the SRD. It ensures that crossing the cutoff has no direct effect on potential outcomes.
3.  **Monotonicity (No Defiers):** The instrument must affect all individuals in the same direction. Monotonicity assumes that there are no "defiers"—individuals who would receive the treatment if ineligible but refuse it if eligible. In the potential outcomes framework for treatment assignment, where $D_i(z)$ is the treatment status if eligibility is $z$, this means $D_i(1) \ge D_i(0)$ for all individuals [@problem_id:4626151].

Under these assumptions, the causal effect is identified by the **Wald estimator**, which is the ratio of the discontinuity in the outcome to the discontinuity in the treatment probability:

$\tau_{FRD} = \frac{\lim_{x \downarrow c} \mathbb{E}[Y_i \mid X_i=x] - \lim_{x \uparrow c} \mathbb{E}[Y_i \mid X_i=x]}{\lim_{x \downarrow c} \mathbb{E}[D_i \mid X_i=x] - \lim_{x \uparrow c} \mathbb{E}[D_i \mid X_i=x]}$

This ratio corrects for the imperfect compliance by scaling the "reduced-form" effect on the outcome (the numerator) by the size of the "first-stage" effect on treatment take-up (the denominator).

### Interpretation of the FRD Estimand: The Complier Average Causal Effect

The FRD estimand has a specific and important interpretation. The [monotonicity](@entry_id:143760) assumption allows us to classify the population at the cutoff into three groups:

*   **Always-Takers:** Individuals who would take the treatment regardless of eligibility ($D_i(1)=1, D_i(0)=1$).
*   **Never-Takers:** Individuals who would never take the treatment regardless of eligibility ($D_i(1)=0, D_i(0)=0$).
*   **Compliers:** Individuals whose treatment status is determined by the eligibility rule ($D_i(1)=1, D_i(0)=0$). These are the people who are "compliers" with the instrument.

The FRD estimator $\tau_{FRD}$ identifies the average treatment effect *only for the subpopulation of compliers at the cutoff*. The contributions of always-takers and never-takers to the outcome regression cancel out in the numerator's difference, as their treatment status does not change when crossing the cutoff. The denominator can be shown to equal the proportion of compliers at the cutoff. Thus, $\tau_{FRD}$ isolates the **Local Average Treatment Effect (LATE)** for those individuals at the margin whose behavior is actually changed by the eligibility rule [@problem_id:4629835].

### Threats to Validity and Diagnostic Checks

The validity of any RD design hinges on the assumption that individuals on either side of the cutoff are comparable, differing only in their treatment assignment. This can be violated if individuals can precisely manipulate their running variable.

#### Manipulation of the Running Variable

The most significant threat to an RD design is **strategic manipulation**. If patients or clinicians can influence the measured value of the running variable $X_i$ to place an individual on the more desirable side of the cutoff, the "as-if randomized" logic breaks down [@problem_id:4629790]. For instance, if healthier patients who are just below a diagnostic threshold for statin therapy manage to manipulate their LDL cholesterol measurement to be just above the threshold to receive treatment, then the group just above the cutoff will be systematically healthier than the group just below it. This creates a discontinuity in unobserved factors that affect the outcome, violating the continuity of potential outcomes and biasing the estimate [@problem_id:4629790].

A primary diagnostic for this type of sorting is the **McCrary density test**. This test examines whether the probability density function of the running variable, $f_X(x)$, has a discontinuity at the cutoff. A significant jump or drop in the number of observations at $c$ is strong evidence of manipulation. While passing this test (finding no jump) is a necessary check, it is not a definitive proof of validity, as some forms of sorting may not result in a density discontinuity [@problem_id:4629790, @problem_id:4629827].

#### Covariate Balance Tests

A second crucial set of diagnostic checks involves examining **baseline covariates**. Since pre-treatment characteristics $Z_i$ (e.g., age, comorbidities) are determined before the treatment is assigned, their conditional expectations should also be continuous at the cutoff. A discontinuity in a baseline variable is a clear red flag, indicating that the groups on either side of the cutoff are not comparable for reasons other than the treatment itself.

A formal test for covariate balance can be conducted for each baseline variable by running an RD analysis on it, treating it as the outcome. Using a method like [local linear regression](@entry_id:635822), one can estimate the regression function on both sides of the cutoff and test whether the intercepts are significantly different. A statistically significant jump for any pre-treatment covariate casts serious doubt on the validity of the RD design for the main outcome of interest [@problem_id:4629804, @problem_id:4629827]. These validity checks are essential steps in any credible RD analysis, strengthening the claim that the design successfully isolates a causal effect.