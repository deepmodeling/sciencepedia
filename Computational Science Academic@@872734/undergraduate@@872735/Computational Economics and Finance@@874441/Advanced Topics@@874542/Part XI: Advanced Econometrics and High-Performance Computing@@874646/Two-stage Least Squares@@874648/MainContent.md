## Introduction
In empirical research, establishing a clear causal relationship between variables is the ultimate goal. However, standard methods like Ordinary Least Squares (OLS) can produce misleading results when a variable of interest is endogenous—correlated with unobserved factors that also affect the outcome. This [endogeneity](@entry_id:142125) problem is a pervasive challenge across economics, finance, and the social sciences, clouding our understanding of cause and effect. This article delves into Two-Stage Least Squares (2SLS), a cornerstone of modern econometrics designed specifically to overcome [endogeneity](@entry_id:142125). As a powerful [instrumental variables](@entry_id:142324) (IV) technique, 2SLS provides a framework for obtaining consistent estimates of causal effects by leveraging an external source of variation that is "as good as random."

This article is structured to guide you from theory to practice. In the first chapter, **Principles and Mechanisms**, we will dissect the statistical foundation of 2SLS, from its intuitive two-stage procedure to the critical conditions required for its validity. The second chapter, **Applications and Interdisciplinary Connections**, will showcase the versatility of 2SLS through a journey across diverse fields, illustrating how researchers creatively find and apply instruments to answer fundamental questions. Finally, **Hands-On Practices** will allow you to solidify your understanding by applying the 2SLS estimator to solve real-world econometric problems. By navigating these sections, you will gain a deep and practical understanding of one of the most important tools for causal inference.

## Principles and Mechanisms

The method of Ordinary Least Squares (OLS) yields consistent and unbiased estimates of causal effects only when its core assumption of [exogeneity](@entry_id:146270)—that the regressors are uncorrelated with the error term—is met. When this assumption is violated, a condition known as **[endogeneity](@entry_id:142125)**, OLS estimates are biased and inconsistent. The Two-Stage Least Squares (2SLS) estimator is a principal technique within the broader class of Instrumental Variables (IV) methods designed to overcome [endogeneity](@entry_id:142125) and produce consistent estimates of causal parameters. This chapter details the principles and mechanisms of 2SLS, moving from its intuitive construction to the formal conditions required for its validity and the practical considerations for its application.

### The Mechanics of Two-Stage Least Squares

The name "Two-Stage Least Squares" arises from a highly intuitive interpretation of its procedure. It can be understood as a two-step process of purging an endogenous regressor of its problematic correlation with the structural error term, and then using only the "clean" part of its variation to estimate the causal effect of interest.

Consider the structural model with a single endogenous regressor $x$ and a set of exogenous covariates $W$:
$$ y_i = \beta_1 x_i + W_i'\gamma + u_i $$
Here, $\operatorname{Cov}(x_i, u_i) \neq 0$, but $\operatorname{Cov}(W_i, u_i) = 0$. Suppose we have a set of [instrumental variables](@entry_id:142324), $Z$, which are correlated with $x$ but are exogenous, meaning $\operatorname{Cov}(Z_i, u_i) = 0$. The full set of exogenous variables available is $[W \;\; Z]$. The 2SLS procedure can be described as follows:

**Stage 1: Purging the Endogenous Variation**

The first stage isolates the portion of the variation in the endogenous regressor $x$ that is explained by *all* the exogenous variables in the model. This is achieved by running an OLS regression of the endogenous regressor $x$ on the instruments $Z$ and the exogenous covariates $W$.
$$ x_i = \pi_0 + Z_i'\pi_1 + W_i'\pi_2 + v_i $$
From this regression, we obtain the predicted values of $x_i$, denoted $\hat{x}_i$:
$$ \hat{x}_i = \hat{\pi}_0 + Z_i'\hat{\pi}_1 + W_i'\hat{\pi}_2 $$
By construction, $\hat{x}_i$ is a linear combination of the exogenous variables $Z_i$ and $W_i$. Since both $Z_i$ and $W_i$ are uncorrelated with the structural error $u_i$, their [linear combination](@entry_id:155091) $\hat{x}_i$ will also be asymptotically uncorrelated with $u_i$. The first stage has therefore "purged" $x_i$ of the endogenous component (the part correlated with $u_i$), which is captured in the first-stage residual, $v_i$. The predicted value $\hat{x}_i$ represents the "clean" variation in $x_i$ that we can use for estimation.

When there are multiple endogenous regressors, say $X_1$ and $X_2$, and multiple instruments $Z_1, Z_2, Z_3$, the first stage becomes a multivariate regression system. Each endogenous variable is regressed on the full set of instruments. In matrix notation, if $X$ is the $n \times k$ matrix of endogenous regressors and $Z$ is the $n \times L$ matrix of all exogenous variables (instruments and included covariates), the first-stage regression system is $X = Z\Pi + V$. The OLS estimate of the [coefficient matrix](@entry_id:151473) $\Pi$ is given by $\hat{\Pi} = (Z'Z)^{-1}Z'X$. The matrix of predicted values is then $\hat{X} = Z\hat{\Pi} = Z(Z'Z)^{-1}Z'X$.

**Stage 2: Estimating the Causal Effect**

The second stage uses the "clean" predicted values $\hat{x}_i$ from the first stage in place of the original endogenous regressor $x_i$ to estimate the structural parameter $\beta_1$. We run an OLS regression of the outcome variable $y_i$ on the predicted endogenous regressor $\hat{x}_i$ and the original exogenous covariates $W_i$:
$$ y_i = \beta_1 \hat{x}_i + W_i'\gamma + \text{error}_i $$
The resulting OLS estimate of $\beta_1$ is the 2SLS estimate, $\hat{\beta}_{1, 2SLS}$. Because $\hat{x}_i$ is now uncorrelated with the structural error $u_i$, this second-stage regression does not suffer from [endogeneity](@entry_id:142125) bias, and $\hat{\beta}_{1, 2SLS}$ is a [consistent estimator](@entry_id:266642) of $\beta_1$.

### Algebraic Formulation and Equivalence

While the two-stage interpretation is pedagogically useful, it is not computationally necessary. The entire procedure can be expressed in a single formula. Let $X$ be the $n \times k$ matrix of all regressors in the structural model (both endogenous and exogenous) and $Z$ be the $n \times L$ matrix of all exogenous variables (the instruments, including any regressors from $X$ that are exogenous). The matrix of predicted values from the first stage is $\hat{X} = Z(Z'Z)^{-1}Z'X = P_Z X$, where $P_Z$ is the [projection matrix](@entry_id:154479) onto the column space of $Z$.

The 2SLS estimator from the second stage is the OLS estimator of regressing $y$ on $\hat{X}$ (when all regressors are treated as potentially endogenous):
$$ \hat{\beta}_{2SLS} = (\hat{X}'\hat{X})^{-1}\hat{X}'y $$
Substituting $\hat{X} = P_Z X$ and using the properties that $P_Z$ is symmetric ($P_Z' = P_Z$) and idempotent ($P_Z P_Z = P_Z$), we get the general formula for the 2SLS estimator:
$$ \hat{\beta}_{2SLS} = (X'P_Z'P_Z X)^{-1} X'P_Z'y = (X'P_Z X)^{-1} X'P_Z y $$
This formula shows that 2SLS can be viewed as an OLS regression of $P_Z y$ on $P_Z X$.

In the special case where the number of instruments equals the number of endogenous regressors (a situation known as **exact identification**), the 2SLS estimator is algebraically identical to the simple [instrumental variables](@entry_id:142324) (IV) estimator. The IV estimator is defined by the sample [moment condition](@entry_id:202521) $Z'(y - X\beta) = 0$, which solves to $\hat{\beta}_{IV} = (Z'X)^{-1}Z'y$. It can be shown analytically and demonstrated computationally that this is equivalent to the two-stage procedure. This equivalence highlights that 2SLS is fundamentally about using the [orthogonality condition](@entry_id:168905) between the instruments and the error to identify the parameters of interest.

### Conditions for Identification

For the 2SLS estimator to be well-defined and consistent, two critical conditions must be met. These are known as the identification conditions.

#### The Order Condition

The **order condition** is a simple counting rule: the number of excluded instruments ($L$) must be at least as great as the number of endogenous regressors ($k$).
- If $L  k$, the model is **underidentified**. There is not enough information to obtain a unique estimate of the parameters.
- If $L = k$, the model is **exactly identified**.
- If $L > k$, the model is **overidentified**. There is more information than is strictly necessary, which can be useful for testing instrument validity.

The order condition is necessary but not sufficient for identification. It is possible for it to hold while the model remains unidentified if the instruments are not actually relevant.

#### The Rank Condition

The **rank condition** is the crucial and [sufficient condition](@entry_id:276242) for identification. It requires that the instruments have a meaningful relationship with the endogenous regressors. Formally, in a model with $k$ endogenous regressors and an $n \times L$ matrix of instruments $Z$, the $L \times k$ matrix of population covariances, $\mathbb{E}[Z'X]$, must have full column rank, i.e., its rank must be equal to $k$.
$$ \operatorname{rank}(\mathbb{E}[Z'X]) = k $$
In a finite sample, we check the sample analog of this condition:
$$ \operatorname{rank}(Z'X) = k $$
This condition ensures that the instruments provide enough independent linear variation to separately identify the effect of each endogenous regressor. A failure of the rank condition means that some linear combination of the instruments is uncorrelated with the endogenous regressors, or that the instruments are collinear. For example, if we have two endogenous regressors ($k=2$) but the matrix $Z'X$ has rank 1, we cannot disentangle the effects of the two regressors, and the model is not identified, even if the order condition holds.

### Practical Challenges: Assessing Instrument Validity

Meeting the formal identification conditions is only the first step. In applied research, the quality of the instruments is paramount. The two foundational assumptions for any instrument $Z_i$ are **relevance** and **[exogeneity](@entry_id:146270)**.

#### Instrument Relevance and the Weak Instrument Problem

Instrument relevance requires that $\operatorname{Cov}(Z_i, x_i) \neq 0$. This is the essence of the rank condition. However, in finite samples, it is not enough for the correlation to be merely non-zero; it must be strong. An instrument that is only weakly correlated with the endogenous regressor is called a **weak instrument**.

When instruments are weak, 2SLS has poor finite-sample properties. The distribution of the 2SLS estimator can be wide, leading to imprecise estimates. More problematically, the 2SLS estimate can be severely biased in small samples, with its mean shifted towards the biased OLS estimate.

A practical rule of thumb for diagnosing [weak instruments](@entry_id:147386) in the case of a single endogenous regressor is to examine the **first-stage F-statistic**. This is the F-statistic from a test of the joint significance of the *excluded* instruments (those not also included as covariates) in the first-stage regression. A widely cited rule of thumb, proposed by Staiger and Stock (1997), suggests that an F-statistic below 10 is a cause for concern, indicating that the instruments are weak. A higher F-statistic provides more confidence that the instruments are relevant and that the 2SLS estimator's asymptotic properties are a reliable guide.

#### Instrument Exogeneity: The Exclusion Restriction

The second, and more challenging, condition for instrument validity is **[exogeneity](@entry_id:146270)**, often called the **[exclusion restriction](@entry_id:142409)**. This condition states that the instrument must be uncorrelated with the structural error term, $\operatorname{Cov}(Z_i, u_i) = 0$. This implies that the instrument affects the outcome variable $y_i$ *only* through its effect on the endogenous regressor $x_i$ and not through any other channel.

Unlike relevance, the [exclusion restriction](@entry_id:142409) is a theoretical assumption that cannot be directly tested from the data (except in the overidentified case, as discussed later). Its justification must come from economic theory, institutional knowledge, and careful reasoning about the data-generating process. A common threat to the [exclusion restriction](@entry_id:142409) arises if the instrument is correlated with some unobserved factor that also influences the outcome.

For example, consider a study estimating the effect of bank credit on firm investment, using a "shift-share" instrument constructed from firm exposure to banks that rely on foreign funding, interacted with a global interest rate shock. An argument against this instrument's validity would be if firms that borrow from such banks are also, for instance, more export-intensive. If the global rate shock also affects exchange rates, it could directly impact the investment of these export-intensive firms, creating a second pathway from the instrument to the outcome that bypasses bank credit. This would violate the [exclusion restriction](@entry_id:142409).

A more technical violation can occur in time-series contexts. Using a lagged [dependent variable](@entry_id:143677), $y_{t-1}$, as an instrument for an endogenous regressor $x_t$ is a common strategy. If the structural errors $u_t$ are not serially correlated, this instrument is valid. However, if the errors follow an [autoregressive process](@entry_id:264527), such as $u_t = \rho u_{t-1} + e_t$, then $u_t$ is correlated with $u_{t-1}$. Since $y_{t-1}$ is a function of $u_{t-1}$, it follows that $\operatorname{Cov}(y_{t-1}, u_t) \neq 0$. The presence of serial correlation in the structural error renders the lagged [dependent variable](@entry_id:143677) an invalid instrument, leading to inconsistent 2SLS estimates.

### Inference with 2SLS

Once the 2SLS coefficients are estimated, the next step is to compute their standard errors to perform hypothesis tests. This stage contains a critical pitfall.

#### The Fallacy of Naive Standard Errors

A common misunderstanding is to believe that one can simply perform the two stages of 2SLS using standard OLS software and then use the standard errors reported by the second-stage regression. This approach is incorrect and yields inconsistent standard errors. The reason is that the second-stage regression uses a **generated regressor**, $\hat{X}$, which was estimated in the first stage. Standard OLS software, when applied to the second stage, treats $\hat{X}$ as if it were a fixed, non-random variable. This ignores the [sampling variability](@entry_id:166518) from the first-stage estimation of $\hat{X}$. The uncertainty from the first stage must be propagated into the calculation of the standard errors for the final coefficients. Failing to do so results in standard errors that are too small, leading to over-rejection of null hypotheses.

#### Correct Standard Errors for 2SLS

The correct formula for the [asymptotic variance](@entry_id:269933)-covariance matrix of the 2SLS estimator must account for the full estimation procedure. Under the simplifying assumption of homoskedastic structural errors ($E[u_i^2|Z_i] = \sigma_u^2$), the [asymptotic variance](@entry_id:269933) of $\hat{\beta}_{2SLS}$ is given by:
$$ \operatorname{Var}(\hat{\beta}_{2SLS}) = \sigma_u^2 (X'P_Z X)^{-1} $$
In practice, the assumption of homoskedasticity is often unrealistic. The **[heteroskedasticity](@entry_id:136378)-robust** (or White) variance-covariance matrix is therefore preferred. This is a "sandwich" estimator that is valid under arbitrary forms of [heteroskedasticity](@entry_id:136378):
$$ \operatorname{Var}_{robust}(\hat{\beta}_{2SLS}) = (X'P_Z X)^{-1} (X'P_Z \hat{\Omega} P_Z X) (X'P_Z X)^{-1} $$
where $\hat{\Omega}$ is a diagonal matrix containing the squared 2SLS residuals, $\hat{u}_i^2 = (y_i - X_i'\hat{\beta}_{2SLS})^2$. Crucially, these residuals must be computed using the original data $X$, not the predicted values $\hat{X}$. Standard errors for each coefficient are the square roots of the diagonal elements of this matrix. Modern statistical software automatically computes these correct standard errors for 2SLS.

#### Testing for Endogeneity: The Durbin-Wu-Hausman Test

Before committing to 2SLS, it is often useful to formally test whether the regressor of interest is indeed endogenous. If it is not, OLS is preferred as it is more efficient (i.e., has lower variance) than 2SLS. The **Durbin-Wu-Hausman (DWH) test** serves this purpose.

The [null hypothesis](@entry_id:265441) of the DWH test is that the regressor is exogenous. The intuition is simple: if the regressor is exogenous, both OLS and 2SLS are consistent estimators, and their estimates should be similar in large samples. If the regressor is endogenous, OLS is inconsistent while 2SLS is consistent, so their estimates should diverge. A statistically significant difference between the OLS and 2SLS estimates is thus taken as evidence of [endogeneity](@entry_id:142125).

A convenient regression-based version of the test can be implemented in two steps:
1. Regress the endogenous regressor(s) $x$ on the instruments $Z$ and obtain the residuals, $\hat{v}$.
2. Regress the outcome $y$ on the original regressors $X$ *and* the first-stage residuals $\hat{v}$. A standard t-test (or F-test for multiple endogenous regressors) on the coefficient(s) of $\hat{v}$ is the DWH test. If the coefficient on $\hat{v}$ is statistically significant, we reject the [null hypothesis](@entry_id:265441) of [exogeneity](@entry_id:146270).

### A Unifying Example: Errors-in-Variables

The problem of classical [measurement error](@entry_id:270998) provides a clear and compelling case for 2SLS. Suppose the true structural model is:
$$ y_i = \beta x_i^* + u_i $$
where $x_i^*$ is the true, unobserved value of a regressor. Instead of $x_i^*$, we observe a noisy measure:
$$ x_i = x_i^* + v_i $$
where $v_i$ is classical measurement error, meaning it is uncorrelated with the true value $x_i^*$ and the structural error $u_i$.

If we naively run OLS of $y_i$ on the observed $x_i$, we are estimating the equation:
$$ y_i = \beta (x_i - v_i) + u_i = \beta x_i + (u_i - \beta v_i) $$
The composite error term is $\epsilon_i = u_i - \beta v_i$. The regressor $x_i = x_i^* + v_i$ is correlated with this error term because both contain $v_i$. Specifically, $\operatorname{Cov}(x_i, \epsilon_i) = \operatorname{Cov}(x_i^* + v_i, u_i - \beta v_i) = -\beta \operatorname{Var}(v_i)$. This correlation induces [endogeneity](@entry_id:142125) bias. The OLS estimator is inconsistent and suffers from **[attenuation bias](@entry_id:746571)**, meaning its probability limit is biased towards zero:
$$ \operatorname{plim} \hat{\beta}_{OLS} = \beta \frac{\operatorname{Var}(x^*)}{\operatorname{Var}(x^*) + \operatorname{Var}(v_i)} $$
Now, suppose we can find an instrument $z_i$ that is correlated with the true value $x_i^*$ but is uncorrelated with both the measurement error $v_i$ and the structural error $u_i$. The 2SLS estimator using $z_i$ as an instrument for $x_i$ will be consistent for $\beta$. In large samples, 2SLS successfully corrects the [attenuation bias](@entry_id:746571) of OLS. This classic example demonstrates the power of the 2SLS framework to overcome a fundamental data problem and recover consistent estimates of causal effects.