## Introduction
How can we measure the causal impact of a policy, program, or intervention when a randomized controlled trial is not feasible? Many real-world programs assign treatment based on whether an individual falls above or below a specific threshold—be it a test score, age, or income level. The Regression Discontinuity (RD) design is a powerful quasi-experimental method that leverages these assignment rules to provide credible causal estimates. By comparing individuals just on either side of the cutoff, RD creates a local experiment, isolating the effect of the treatment from other confounding factors.

This article provides a thorough introduction to the theory and practice of RD designs. It bridges the gap between the intuitive concept of a "jump" at a cutoff and the rigorous statistical framework required to validate and estimate it. Over the course of three chapters, you will gain a deep understanding of this essential tool for [causal inference](@entry_id:146069).

The journey begins in the "Principles and Mechanisms" chapter, where we will unpack the theoretical foundation of RD, including the crucial continuity assumption within the [potential outcomes framework](@entry_id:636884), and explore the statistical mechanics of local [polynomial regression](@entry_id:176102) used to estimate the effect. Next, "Applications and Interdisciplinary Connections" will demonstrate the remarkable versatility of RD, showcasing its use in fields from public policy and medicine to ecology, and situating it within the broader landscape of causal methods like Mendelian Randomization. Finally, "Hands-On Practices" will allow you to apply your knowledge to solve practical challenges, from dealing with data limitations to optimizing your estimation strategy.

## Principles and Mechanisms

The Regression Discontinuity (RD) design is a quasi-experimental method for estimating causal effects in settings where a treatment is assigned based on whether an observed variable, the **running variable**, exceeds a specific cutoff. This chapter delineates the fundamental principles that grant the RD design its causal interpretation and the statistical mechanisms through which these effects are estimated and validated.

### The Core Idea: Identification Through Discontinuity

At its heart, the RD design leverages a discontinuity in treatment assignment to identify a causal effect. Consider a running variable $X$ and a known cutoff value $c$. In the simplest version, the **sharp Regression Discontinuity design**, treatment status $D$ is a deterministic function of whether $X$ is at or above the cutoff:

$D = \mathbf{1}\{X \ge c\}$

Here, $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167). Every unit with a score of at least $c$ receives the treatment, and every unit with a score below $c$ does not. The core intuition is that units with scores just below the cutoff ($X = c - \epsilon$) are likely very similar to units with scores just above the cutoff ($X = c + \epsilon$) for some small $\epsilon > 0$. The only systematic difference between these two groups is that one received the treatment and the other did not. This creates a "local experiment" right at the threshold.

The parameter of interest, or **estimand**, in the RD design is the jump in the conditional expectation of the outcome variable $Y$ at the cutoff $c$. Formally, this is the difference between the right-hand and left-hand limits of the regression function $\mathbb{E}[Y | X=x]$ at the point $c$:

$\tau_{RD} = \lim_{x \downarrow c} \mathbb{E}[Y | X = x] - \lim_{x \uparrow c} \mathbb{E}[Y | X = x]$

If the units on either side of the cutoff are indeed comparable, this jump can be interpreted as the causal effect of the treatment. The next section formalizes this critical assumption.

### The Causal Interpretation: The Potential Outcomes Framework

To formally establish a causal interpretation, we turn to the **[potential outcomes framework](@entry_id:636884)**. For each unit, we conceive of two [potential outcomes](@entry_id:753644): $Y(1)$, the outcome that would be realized if the unit received the treatment, and $Y(0)$, the outcome that would be realized if the unit did not. The observed outcome is $Y = D \cdot Y(1) + (1-D) \cdot Y(0)$. The causal effect of the treatment for a given unit is the difference $Y(1) - Y(0)$.

The specific causal parameter that the RD design aims to identify is the **Average Treatment Effect at the Cutoff**, defined as:

$\tau_{ATE(c)} = \mathbb{E}[Y(1) - Y(0) | X = c]$

This is the average [treatment effect](@entry_id:636010) for the specific subpopulation of individuals whose running variable is exactly equal to the cutoff value.

For the observed jump $\tau_{RD}$ to equal this causal parameter $\tau_{ATE(c)}$, a crucial identifying assumption must hold: the conditional expectation functions of the [potential outcomes](@entry_id:753644), $\mathbb{E}[Y(1)|X=x]$ and $\mathbb{E}[Y(0)|X=x]$, must be continuous in $x$ at the cutoff $c$ . This is the **continuity assumption**.

Let's see how this assumption enables identification. The [right-hand limit](@entry_id:140515) of the observed regression function involves only treated units ($D=1$), for whom $Y=Y(1)$:

$\lim_{x \downarrow c} \mathbb{E}[Y | X = x] = \lim_{x \downarrow c} \mathbb{E}[Y(1) | X = x]$

By the continuity of $\mathbb{E}[Y(1)|X=x]$, this limit equals the value at the point $c$:

$\lim_{x \downarrow c} \mathbb{E}[Y(1) | X = x] = \mathbb{E}[Y(1) | X = c]$

Similarly, the [left-hand limit](@entry_id:139055) involves only untreated units ($D=0$), for whom $Y=Y(0)$:

$\lim_{x \uparrow c} \mathbb{E}[Y | X = x] = \lim_{x \uparrow c} \mathbb{E}[Y(0) | X = x] = \mathbb{E}[Y(0) | X = c]$

The difference between these two identified quantities is precisely the causal effect of interest:

$\tau_{RD} = \mathbb{E}[Y(1) | X = c] - \mathbb{E}[Y(0) | X = c] = \tau_{ATE(c)}$

The continuity assumption is the theoretical cornerstone of the RD design. It formalizes the intuition that nothing else of consequence changes abruptly at the cutoff except for the treatment itself. This assumption is more plausible than the global "unconfoundedness" assumptions required by methods like matching, which posit that treatment is random conditional on covariates across the entire data range. RDD only requires this conditional randomness to hold locally at the cutoff .

The gravity of this assumption can be illustrated with a thought experiment. Suppose the assumption is violated because the potential outcome without treatment, $Y_0(x)$, itself has a jump of size $\delta$ at the cutoff, such that $Y_0(x) = g(x) + \delta \cdot \mathbf{1}\{x \ge c\}$ for some [smooth function](@entry_id:158037) $g(x)$. The observed outcome for untreated units (left of $c$) would be $g(x)$, while for treated units (right of $c$) it would be $Y_1(x) = g(x) + \tau + \delta$. The estimated jump would be $(\tau + \delta)$, not $\tau$. The estimator is therefore biased by the exact amount of the continuity violation, $\delta$ .

### Estimation: Local Polynomial Regression

To estimate the discontinuity $\tau_{RD}$, one must approximate the regression functions on both sides of the cutoff. A naive approach might be to fit a single, flexible [regression model](@entry_id:163386) (a "global smoother") to the data and inspect it for a jump. However, this is fundamentally flawed. Most standard smoothers, such as Locally Weighted Scatterplot Smoothing (LOESS), are designed to produce a *continuous* fitted curve. By their very nature, they will smooth over the discontinuity of interest, leading to a severe downward bias in the estimate of $\tau_{RD}$ . For instance, a simulation where the true jump is $\tau=1$ can show that a global LOESS smoother estimates a jump near zero, effectively hiding the true effect.

The standard and principled approach is **local [polynomial regression](@entry_id:176102)**. This method honors the potential discontinuity by fitting separate models to the data on the left and right sides of the cutoff. The most common variant is **[local linear regression](@entry_id:635822)** ($p=1$), which fits a separate straight line to the data within a specified **bandwidth** $h$ on each side of $c$.

The procedure is as follows:
1.  Select a bandwidth $h > 0$. This defines a window $[c-h, c+h]$ around the cutoff.
2.  For the data on the right side, $X_i \in [c, c+h]$, fit a weighted [linear regression](@entry_id:142318) of $Y_i$ on $(X_i-c)$. The weights are typically assigned by a **kernel function**, such as the triangular kernel $K(u)=(1-|u|)\mathbf{1}\{|u|\le 1\}$, which gives more weight to points closer to $c$. The estimated intercept, $\hat{\beta}_{0, \text{right}}$, is the predicted value $\hat{\mathbb{E}}[Y|X=c^+]$.
3.  Similarly, for the data on the left side, $X_i \in [c-h, c)$, fit a weighted linear regression to obtain the predicted value $\hat{\mathbb{E}}[Y|X=c^-] = \hat{\beta}_{0, \text{left}}$.
4.  The RD estimate is the difference in these predictions: $\hat{\tau}_{RD} = \hat{\beta}_{0, \text{right}} - \hat{\beta}_{0, \text{left}}$.

The choice of bandwidth $h$ and polynomial order $p$ is critical and involves a bias-variance trade-off. A larger bandwidth reduces variance (by using more data) but can increase bias if the true regression function is curved, as the local polynomial becomes a poor approximation. This **specification bias** is a primary concern. For a local linear estimator, the leading term of the bias is proportional to $h^2$ and the difference in the *curvature* (second derivatives) of the true regression functions on either side of the cutoff, i.e., $m_+''(c) - m_-''(c)$ .

More flexible estimators, such as penalized [cubic splines](@entry_id:140033) with a knot at the cutoff, can sometimes achieve smaller bias by better capturing the underlying curvature. By using all data points (not just those within a bandwidth) and a penalty on roughness, [splines](@entry_id:143749) can "borrow strength" from data far from the cutoff to obtain a more stable estimate of the function's shape, which is particularly useful in sparse-data regions . However, these methods introduce their own tuning parameters (e.g., the smoothing penalty $\lambda$) and complexities.

### Extensions: The Fuzzy Regression Discontinuity Design

In many real-world scenarios, crossing the cutoff does not deterministically assign treatment but merely influences the probability of receiving it. This is known as the **fuzzy Regression Discontinuity design**. For example, a scholarship program may have an eligibility score cutoff, but not all eligible students take up the scholarship, and some ineligible students may receive it through other means.

In this setting, the sharp jump in treatment is replaced by a jump in the *probability* of treatment. The fuzzy RD design is best understood as a local **Instrumental Variable (IV)** model . The instrument $Z$ is the eligibility indicator, $Z = \mathbf{1}\{X \ge c\}$, which is exogenous by design. The treatment $D$ is now endogenous, as individuals' decisions to take up the treatment may be correlated with their [potential outcomes](@entry_id:753644).

The causal effect is estimated using the **local Wald estimator**, which is the ratio of the jump in the outcome (the reduced-form effect) to the jump in the treatment probability (the first-stage effect):

$\tau_{LATE} = \frac{\lim_{x \to c^+} \mathbb{E}[Y | X=x] - \lim_{x \to c^-} \mathbb{E}[Y | X=x]}{\lim_{x \to c^+} \mathbb{E}[D | X=x] - \lim_{x \to c^-} \mathbb{E}[D | X=x]}$

This estimator requires two key assumptions in addition to the continuity of [potential outcomes](@entry_id:753644). The first is the **[exclusion restriction](@entry_id:142409)**, which states that the instrument $Z$ affects the outcome $Y$ only through its effect on treatment status $D$. The continuity assumption on [potential outcomes](@entry_id:753644) ensures this holds. The second is **[monotonicity](@entry_id:143760)**, which requires that the instrument pushes all individuals' treatment decisions in the same direction. This means there are no **defiers**—individuals who would take the treatment if ineligible ($Z=0$) but refuse it if eligible ($Z=1$).

Under these assumptions, the local Wald estimand identifies the **Local Average Treatment Effect (LATE)** for compliers at the cutoff. **Compliers** are the subpopulation of individuals whose treatment status is changed by the instrument (i.e., they take the treatment if and only if they are eligible). The denominator of the Wald ratio, $\mathbb{E}[D|Z=1] - \mathbb{E}[D|Z=0]$, identifies the proportion of compliers in the population at the cutoff .

The [monotonicity](@entry_id:143760) assumption is crucial and testable. The denominator of the Wald estimator—the first-stage effect—must be non-zero. A positive first stage indicates that compliers outnumber defiers. If, however, the first stage is negative, it implies that defiers outnumber compliers, a direct violation of the [monotonicity](@entry_id:143760) assumption. In this case, the Wald estimator becomes an uninterpretable weighted average of the treatment effects for compliers and defiers, losing its causal meaning as a LATE .

In practice, the numerator and denominator of the Wald ratio are estimated using separate local polynomial regressions. Since the outcome and treatment regressions have different [dependent variables](@entry_id:267817), their functional forms and error variances will generally differ. Therefore, it is statistically appropriate and often necessary to use different, separately optimized bandwidths ($h_Y$ and $h_D$) for the two regressions to minimize the overall [mean squared error](@entry_id:276542) of the LATE estimate .

### Threats to Validity and Specification Checks

The validity of an RD analysis hinges on its core assumptions. Rigorous empirical work therefore requires a battery of tests to probe for potential violations.

#### Strategic Manipulation

The central assumption of continuity rests on the idea that individuals cannot precisely manipulate their running variable score to fall just on one side of the cutoff. If they can, the "as-if random" assignment at the threshold breaks down. For example, if individuals who stand to gain most from a program can strategically boost their score to get just above the cutoff, then the group just above $c$ will systematically differ from the group just below $c$ in their [potential outcomes](@entry_id:753644), violating continuity . This sorting behavior introduces a bias. Formally, if a fraction $q$ of agents in a region $[c-\delta, c)$ can add $\delta$ to their score, this creates a discontinuity in the relationship between the true, pre-manipulation score and the observed score right at the cutoff .

The primary diagnostic for manipulation is the **McCrary density test**, which checks for a discontinuity in the probability density function of the running variable at the cutoff. A suspicious "bunching" of observations just above the cutoff is a telltale sign of manipulation and a serious threat to the design's validity .

#### Continuity and Model Misspecification

Even without manipulation, the continuity assumption can be violated, or the chosen estimation model can be misspecified, leading to biased results. Two key types of specification checks address this.

First, a **covariate balancing check** tests whether pre-treatment covariates are continuous at the cutoff. The logic is that if observable characteristics that should not be affected by the treatment show no jump, it lends credibility to the assumption that unobservable characteristics and [potential outcomes](@entry_id:753644) are also continuous. This is done by running the same RD estimation procedure on a pre-treatment covariate $Z$ instead of the outcome $Y$. The estimated "effect" on $Z$ should be zero. It is critical that this check be performed using the *same bandwidth and polynomial order* as the main outcome analysis. Using a different, larger bandwidth might average over a localized imbalance, masking a problem that is relevant for the main estimate .

Second, **placebo tests** involve re-estimating the RD effect at fake cutoffs where no treatment discontinuity exists. For example, one might test for a jump at $c-2h$ or $c+2h$. If the model is correctly specified, it should find no statistically significant effects at these placebo locations. Finding significant placebo effects is a strong indication that the model (e.g., the bandwidth or polynomial order) is misspecified and is likely fitting a global non-linear trend, creating spurious jumps. This severely undermines the credibility of the estimate at the true cutoff, as it is likely contaminated by the same specification bias .

#### Measurement Error

A final practical threat is **[measurement error](@entry_id:270998)** in the running variable. Suppose treatment is truly assigned based on a latent score $X^*$, but the analyst only observes a noisy version, $W = X^* + U$. When the RD analysis is naively performed using the observed variable $W$, individuals are misclassified. Some with true scores $X^*  c$ will have observed scores $W \ge c$, and vice versa. This blurring of the sharp assignment boundary effectively transforms a sharp design into a fuzzy one. The consequence is an **[attenuation bias](@entry_id:746571)**: the estimated effect will be biased toward zero, as the discontinuity is smeared out across the distribution of the [measurement error](@entry_id:270998) . The magnitude of this bias depends on the variance of the [measurement error](@entry_id:270998) relative to the variation in the running variable itself.

In conclusion, while the Regression Discontinuity design offers a powerful and transparent approach to [causal inference](@entry_id:146069), its validity rests on a set of well-defined assumptions. A credible RD analysis must not only provide an estimate of the effect but also a body of evidence from diagnostic and specification tests that support the integrity of the design and the chosen estimation strategy.