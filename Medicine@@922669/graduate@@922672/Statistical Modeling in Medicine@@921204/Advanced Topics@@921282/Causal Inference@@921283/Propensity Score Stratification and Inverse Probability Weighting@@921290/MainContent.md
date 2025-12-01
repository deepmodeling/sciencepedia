## Introduction
In observational medical research, determining the true causal effect of a treatment is a significant challenge. Unlike randomized controlled trials, where treatment allocation is random, observational studies often suffer from [confounding bias](@entry_id:635723): the very factors influencing a treatment decision may also be linked to the patient's outcome. Propensity score methods offer a powerful statistical toolkit to address this issue, allowing researchers to emulate the conditions of a randomized trial using existing data. By adjusting for the probability of receiving a treatment, these techniques can yield more reliable estimates of causal effects, provided certain key assumptions are met.

This article provides a comprehensive guide to two cornerstone propensity score techniques: stratification and inverse probability weighting (IPTW). The first chapter, **Principles and Mechanisms**, will lay the theoretical groundwork, defining causal estimands and the identification assumptions required for causal inference. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the versatility of these methods in complex real-world scenarios, from pharmacoepidemiology to genomics. Finally, the **Hands-On Practices** chapter will offer practical exercises to solidify understanding and build essential analytical skills.

## Principles and Mechanisms

In observational medical research, the primary challenge in estimating the causal effect of a treatment or exposure is confounding. Unlike in a randomized controlled trial (RCT), where treatment assignment is governed by chance and is therefore independent of patient characteristics, in observational studies, the factors that influence a clinician's decision to administer a treatment are often also related to the patient's prognosis. Propensity score methods provide a powerful and principled framework for addressing this confounding, allowing for the estimation of causal effects under a specific set of transparent assumptions. This chapter elucidates the theoretical principles underpinning these methods and the mechanisms through which they operate.

### The Causal Estimands: Defining the Research Question

Before any estimation can occur, it is imperative to precisely define the causal quantity of interest, or **estimand**. The [potential outcomes framework](@entry_id:636884) provides the necessary language. For a binary treatment $A \in \{0,1\}$, let $Y(1)$ be the potential outcome an individual would experience if they received the treatment ($A=1$) and $Y(0)$ be the potential outcome they would experience if they did not ($A=0$). The fundamental problem of causal inference is that for any given individual, we can only observe one of these potential outcomes.

Based on these potential outcomes, we can define several estimands that correspond to different clinical or policy questions [@problem_id:4980951]:

*   The **Average Treatment Effect (ATE)** is defined as $\mathrm{ATE} = \mathbb{E}[Y(1) - Y(0)]$. This measures the average effect of the treatment if it were administered to every individual in the entire population of interest. The ATE is the natural estimand for broad policy decisions, such as whether a public health system should adopt a new therapy for all eligible patients.

*   The **Average Treatment Effect on the Treated (ATT)** is defined as $\mathrm{ATT} = \mathbb{E}[Y(1) - Y(0) \mid A=1]$. This measures the average effect of the treatment specifically for the subpopulation of patients who, in reality, received the treatment. The ATT is often of great clinical relevance as it answers the question, "What was the effect of the treatment for the types of patients who were actually prescribed it?" This is particularly important when a treatment is preferentially given to higher-risk individuals, and the goal is to evaluate its benefit in that specific clinical context [@problem_id:4980949].

*   The **Average Treatment Effect on the Controls (ATC)**, sometimes called the Average Treatment Effect on the Untreated (ATU), is defined as $\mathrm{ATC} = \mathbb{E}[Y(1) - Y(0) \mid A=0]$. This measures the average effect of the treatment had it been given to the subpopulation of patients who, in reality, did not receive it. The ATC is most relevant when considering the expansion of a therapy to patient populations who are not currently receiving it.

These three estimands are not necessarily equal in the presence of treatment effect heterogeneity, where the effect of the treatment, $Y(1)-Y(0)$, varies with patient characteristics. The choice of estimand is a crucial first step that must be driven by the specific scientific question.

### Identifiability: Conditions for Causal Inference

To estimate these counterfactual quantities from observed data—the vector of covariates $X$, the received treatment $A$, and the observed outcome $Y$—we must make a set of assumptions that allow us to "identify" the estimand. Identification means being able to express the estimand as a function of the distribution of the observed data. The three core identification assumptions are as follows [@problem_id:4980964] [@problem_id:4980908]:

1.  **Stable Unit Treatment Value Assumption (SUTVA)**: This assumption comprises two distinct components.
    *   **No Interference**: The potential outcomes for any given individual are unaffected by the treatment assignment of other individuals. This allows us to write the potential outcome as $Y_i(a)$ for individual $i$, which depends only on their own treatment status $a$, not on the entire vector of treatment assignments across the population.
    *   **Consistency**: An individual's observed outcome is their potential outcome corresponding to the treatment they actually received. Mathematically, if an individual receives treatment $A_i = a$, then their observed outcome is $Y_i = Y_i(a)$. This is the crucial link between the unobserved potential outcomes and the observed data.

2.  **Conditional Exchangeability (Unconfoundedness)**: This assumption states that, conditional on the measured baseline covariates $X$, the treatment assignment is independent of the potential outcomes. Formally, $(Y(0), Y(1)) \perp A \mid X$. This is often referred to as "no unmeasured confounding" or "ignorability". It asserts that while treated and untreated groups may differ systematically overall, within any stratum defined by a specific set of covariates $X=x$, the treatment assignment is effectively random. It is the most critical and untestable assumption in observational research, as it requires that we have measured a sufficient set of covariates to capture all common causes of treatment assignment and the outcome.

3.  **Positivity (or Overlap)**: This assumption requires that for every set of covariate values $x$ present in the population, there is a non-zero probability of receiving either treatment level. Formally, for all $x$ in the support of $X$, $0  \Pr(A=1 \mid X=x)  1$. If for some subgroup of patients (e.g., those with a contraindication), treatment is never assigned, it is impossible to learn what the effect of the treatment would have been in that subgroup. Positivity ensures that a comparison group exists for all types of patients in the study [@problem_id:4980913].

Under these three assumptions, the ATE and other causal estimands are identifiable from the observed data distribution.

### The Propensity Score: A Dimensionality Reduction Tool

Conditioning on a high-dimensional vector of covariates $X$ can be difficult or impossible in practice. The **[propensity score](@entry_id:635864)**, defined as the [conditional probability](@entry_id:151013) of receiving treatment given the baseline covariates, provides a remarkable solution to this problem.

$$e(X) = \Pr(A=1 \mid X)$$

The utility of the [propensity score](@entry_id:635864) stems from its two fundamental properties, first established by Rosenbaum and Rubin (1983) [@problem_id:4980880]:

1.  **The Balancing Property**: The propensity score is a balancing score, meaning that conditional on the propensity score, the treatment assignment $A$ is independent of the full covariate vector $X$. Formally, $X \perp A \mid e(X)$. This implies that within a subpopulation of individuals who share the same [propensity score](@entry_id:635864), the distribution of all measured covariates, $X$, is the same for the treated and untreated groups. In this sense, the [propensity score](@entry_id:635864) acts as a "univariate summary" of the multivariate confounding information contained in $X$.

2.  **Sufficiency for Unconfoundedness**: If conditional exchangeability holds given $X$, i.e., $(Y(0), Y(1)) \perp A \mid X$, then it also holds given the [propensity score](@entry_id:635864) $e(X)$, i.e., $(Y(0), Y(1)) \perp A \mid e(X)$. This theorem is a direct consequence of the balancing property and is the theoretical justification for using the [propensity score](@entry_id:635864) to adjust for confounding. It proves that adjusting for the single scalar variable $e(X)$ is sufficient to remove bias due to all measured covariates in $X$, just as if we had adjusted for the full vector $X$.

It is crucial to understand what this dimensionality reduction does and does not accomplish [@problem_id:4980937]. The [propensity score](@entry_id:635864), $e(X)$, summarizes all information in $X$ that is relevant to the **treatment assignment mechanism**. However, it does not necessarily summarize all information in $X$ that is relevant to the **outcome-generating mechanism**. A covariate might be a very strong predictor of the outcome (a prognostic variable) but only weakly associated with treatment assignment. When we reduce $X$ to $e(X)$, the prognostic information from such a variable can be diminished. While adjusting for $e(X)$ is sufficient to obtain an unbiased estimate of the treatment effect, it may not be the most statistically efficient (i.e., lowest variance) approach. Methods that can leverage additional prognostic information from $X$, such as doubly [robust estimation](@entry_id:261282), can often yield more precise estimates.

### Propensity Score Stratification

Propensity score stratification is an intuitive method that directly leverages the balancing property. The procedure involves partitioning the sample into a number of strata (typically $K=5$ or $K=10$) based on quantiles of the estimated propensity score, $\hat{e}(X)$. The treatment effect is then estimated within each stratum and averaged across strata to produce an overall estimate.

The mechanism by which this reduces bias is one of approximation [@problem_id:4980910]. While the balancing property holds when conditioning on the exact value of $e(X)$, stratification approximates this by conditioning on stratum membership. Within each narrow stratum defined by [quantiles](@entry_id:178417) of $\hat{e}(X)$, the propensity scores are not identical but are highly similar. This near-constancy of $e(X)$ within a stratum leads to **approximate balance** of the covariate distributions between treated and untreated subjects. Consequently, a simple comparison of outcomes within a stratum is subject to much less [confounding bias](@entry_id:635723) than a crude comparison in the full sample.

However, for any finite number of strata $K$, there will be some residual variation in $e(X)$ within each stratum, which implies some **residual confounding**. This results in a finite-$K$ bias that decreases as the number of strata increases. In the limit, as $K \to \infty$ (and the sample size grows appropriately), the bias of the stratified estimator converges to zero, and its estimand becomes equivalent to that of IPTW [@problem_id:4980908].

In practice, a common choice is to use $K=5$ strata, i.e., stratifying on quintiles of the propensity score [@problem_id:4980918]. This practice is a heuristic grounded in early work by Cochran and later verified by Rosenbaum and Rubin, who showed that for a single normally distributed confounder, five strata can remove approximately 90% of the bias. This choice represents a pragmatic trade-off: it achieves substantial bias reduction while maintaining a sufficient number of treated and untreated individuals within each stratum to allow for stable estimation, avoiding the high variance that would result from having very small or empty strata.

To target different estimands, the within-stratum effects are combined using different weights [@problem_id:4980951]:
*   For the **ATE**, the stratum-specific effects are averaged, weighting by the proportion of the total sample in each stratum.
*   For the **ATT**, the stratum-specific effects are averaged, weighting by the proportion of the *treated* sample in each stratum.
*   For the **ATC**, the stratum-specific effects are averaged, weighting by the proportion of the *control* sample in each stratum.

### Inverse Probability of Treatment Weighting (IPTW)

Inverse Probability of Treatment Weighting is a powerful alternative that uses the [propensity score](@entry_id:635864) to create a weighted "pseudo-population" in which the covariates are no longer associated with treatment assignment. The fundamental idea is to weight each individual by the inverse of the probability of receiving the treatment they actually received, conditional on their covariates.

For estimating the **ATE**, the unstabilized weights are:

$$
w_i = \frac{A_i}{e(X_i)} + \frac{1-A_i}{1-e(X_i)}
$$

This means a treated subject ($A_i=1$) receives a weight of $1/e(X_i)$, and an untreated subject ($A_i=0$) receives a weight of $1/(1-e(X_i))$. Under the identification assumptions, the weighted mean of the outcome in this pseudo-population consistently estimates the potential outcome means [@problem_id:4980880]:

$$
\mathbb{E}[Y(1)] = \mathbb{E}\left[\frac{A Y}{e(X)}\right] \quad \text{and} \quad \mathbb{E}[Y(0)] = \mathbb{E}\left[\frac{(1-A) Y}{1-e(X)}\right]
$$

The ATE is then identified as the difference of these two expectations.

The weighting scheme can be adapted to target the **ATT** [@problem_id:4980949]. For the ATT, the target population is the treated group. Therefore, the treated subjects are already representative of themselves and are given a weight of $1$. The control subjects are reweighted to match the covariate distribution of the treated group. This results in the following weights:

*   For treated subjects ($A_i=1$): $w_i^{\mathrm{ATT}} = 1$
*   For control subjects ($A_i=0$): $w_i^{\mathrm{ATT}} = \frac{e(X_i)}{1-e(X_i)}$

This set of weights creates a pseudo-population where the weighted control group has the same covariate distribution as the unweighted treated group, allowing for a direct comparison to estimate the ATT. A crucial diagnostic step is to check that this reweighting has indeed achieved balance between the unweighted treated group and the weighted control group.

### Practical Challenges: Positivity and Weight Instability

The validity and performance of [propensity score](@entry_id:635864) methods, particularly IPTW, depend critically on the positivity assumption. Violations of this assumption can be either strict or practical, with different consequences [@problem_id:4980913] [@problem_id:4980945].

**Strict positivity violations** occur when for a certain subpopulation defined by covariates $X=x$, the [propensity score](@entry_id:635864) is exactly 0 or 1. This means treatment is either impossible or guaranteed for this subpopulation. In this case, there is no empirical basis for comparison, and the ATE is fundamentally non-identifiable without making strong, untestable modeling assumptions to extrapolate outcomes. IPTW fails because the weights become infinite, and stratification fails because the corresponding strata will contain only treated or only control subjects.

**Practical positivity violations** are more common and occur when propensity scores are very close to 0 or 1. This indicates poor overlap between the covariate distributions of the treated and control groups. Consider a treated patient ($A=1$) with a very low [propensity score](@entry_id:635864), say $\hat{e}(X) = 0.01$. This patient was very unlikely to receive the treatment but did. Their IPTW weight for the ATE would be $1/0.01 = 100$. This single individual is given enormous influence in the analysis, representing 100 such individuals in the pseudo-population. Such extreme weights lead to IPTW estimators with very high variance, making them unstable and highly sensitive to the exact outcome of a few individuals and to misspecification of the [propensity score](@entry_id:635864) model.

Several strategies exist to mitigate the problem of extreme weights:

*   **Stabilized Weights**: Stabilized weights rescale the standard weights by the [marginal probability](@entry_id:201078) of treatment, e.g., $sw_i^{\mathrm{ATE}} = A_i \frac{\Pr(A=1)}{e(X_i)} + (1-A_i) \frac{\Pr(A=0)}{1-e(X_i)}$. While stabilized weights generally have better statistical properties (e.g., lower variance) than unstabilized weights, they do not solve the core problem. The denominator remains $e(X_i)$ or $1-e(X_i)$, so they still become very large when positivity is practically violated [@problem_id:4980908] [@problem_id:4980945].

*   **Trimming or Weight Capping**: Another approach is to either discard (trim) subjects with extreme propensity scores (e.g., outside the range $[0.05, 0.95]$) or to cap (winsorize) the weights at some maximum value. This directly addresses the source of instability and can dramatically reduce the variance of the estimator. However, this comes at a significant cost: it changes the target estimand. The analysis no longer estimates the ATE for the full population but rather the ATE for a restricted "[overlap population](@entry_id:276854)" where positivity is stronger. This introduces a [bias-variance trade-off](@entry_id:141977), where an analyst accepts some bias with respect to the original question to obtain a more stable and precise answer to a related but different question [@problem_id:4980913] [@problem_id:4980945].