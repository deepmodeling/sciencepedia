## Introduction
Ordinary Least Squares (OLS) is a fundamental and widely used estimator in [computational economics](@entry_id:140923), finance, and the broader quantitative sciences. Its appeal lies in its computational simplicity and, under specific conditions, its powerful statistical properties that allow researchers to move beyond mere correlation to make credible causal claims. However, the validity, efficiency, and [interpretability](@entry_id:637759) of OLS results are not guaranteed. They hinge on a set of core assumptions about the underlying data generating process. Ignoring or misunderstanding these assumptions can lead to biased coefficients, incorrect standard errors, and ultimately, flawed conclusions.

This article provides a comprehensive guide to these foundational principles. We will begin in the "Principles and Mechanisms" chapter by systematically dissecting the theoretical meaning of each OLS assumption, from the crucial concept of [exogeneity](@entry_id:146270) to the properties of spherical errors. Next, the "Applications and Interdisciplinary Connections" chapter will demonstrate the real-world relevance of these assumptions, showing how violations like [omitted variable bias](@entry_id:139684) and [heteroskedasticity](@entry_id:136378) manifest in fields ranging from health economics to evolutionary biology. Finally, the "Hands-On Practices" section will offer interactive exercises to solidify these concepts, allowing you to experience the consequences of assumption violations firsthand. By progressing through these chapters, you will gain the essential knowledge to critically evaluate and construct robust [linear regression](@entry_id:142318) models.

## Principles and Mechanisms

The Ordinary Least Squares (OLS) estimator is a cornerstone of [computational economics](@entry_id:140923) and finance, prized for its computational simplicity and, under specific conditions, its desirable statistical properties. The validity and interpretation of OLS results, however, depend critically on a set of assumptions regarding the underlying data-generating process. This chapter systematically dissects these foundational assumptions. For each, we will explore its theoretical meaning, its importance for the properties of the OLS estimator, and the practical consequences of its violation through real-world and hypothetical scenarios. Understanding these principles is paramount for any practitioner seeking to move from mere correlation to credible causal inference.

The [linear regression](@entry_id:142318) model is specified as:
$$
Y_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + \dots + \beta_k X_{ik} + u_i
$$
or in matrix notation, $\mathbf{y} = \mathbf{X}\boldsymbol{\beta} + \mathbf{u}$. The OLS estimator, $\hat{\boldsymbol{\beta}}$, is the vector of coefficients that minimizes the [sum of squared residuals](@entry_id:174395). The celebrated Gauss-Markov theorem states that under a set of assumptions—linearity, [exogeneity](@entry_id:146270), spherical errors, and no perfect multicollinearity—OLS is the **Best Linear Unbiased Estimator (BLUE)**. We will now investigate these assumptions in detail.

### The Crucial Assumption: Exogeneity

Perhaps the most important and most frequently violated assumption is that of **[exogeneity](@entry_id:146270)**, formally expressed as the **zero conditional mean** of the error term:
$$
\mathbb{E}[u_i \mid X_{i1}, X_{i2}, \dots, X_{ik}] = 0
$$
This assumption states that the unobserved factors and errors collected in the term $u_i$ are, on average, unrelated to the values of the explanatory variables $X_{ij}$. It implies that the regressors are not correlated with the error term, a condition known as **[endogeneity](@entry_id:142125)** when violated. The [exogeneity](@entry_id:146270) assumption is the mathematical foundation for establishing that OLS estimators are **unbiased** and **consistent**. An [unbiased estimator](@entry_id:166722) has an expected value equal to the true population parameter, while a [consistent estimator](@entry_id:266642) converges in probability to the true parameter as the sample size grows infinitely large. When [exogeneity](@entry_id:146270) is violated, OLS may misattribute the effects of unobserved factors to the included regressors, leading to biased and misleading conclusions. There are several primary mechanisms through which this violation occurs.

#### Omitted Variable Bias

The most common source of [endogeneity](@entry_id:142125) is **[omitted variable bias](@entry_id:139684) (OVB)**. This occurs when a variable that both influences the [dependent variable](@entry_id:143677) $Y$ and is correlated with at least one of the included independent variables $X$ is omitted from the regression. The effect of this omitted variable becomes part of the error term, causing the error term to be correlated with the included regressor(s).

Consider a researcher studying the factors that determine student test scores (). A simple model might regress a student's score ($S_i$) on the number of hours they studied ($H_i$):
$$
S_i = \alpha_0 + \alpha_1 H_i + e_i
$$
However, a more complete structural model would likely include the student's "innate interest" in the subject ($I_i$):
$$
S_i = \beta_0 + \beta_1 H_i + \beta_2 I_i + u_i
$$
Here, $\beta_1$ represents the true causal effect of an additional hour of study, holding interest constant. Innate interest likely has a direct positive effect on scores, so $\beta_2 > 0$. Furthermore, students with greater interest are likely to study more, implying $\operatorname{Cov}(H_i, I_i) > 0$.

When the researcher estimates the simpler model, the unobserved interest $I_i$ is absorbed into the error term, $e_i = \beta_2 I_i + u_i$. Because $H_i$ is correlated with $I_i$, it is now correlated with the new error term $e_i$, violating the zero conditional mean assumption. In this case, the OLS estimator $\hat{\alpha}_1$ will converge not to the true parameter $\beta_1$, but to:
$$
\operatorname{plim}(\hat{\alpha}_1) = \beta_1 + \beta_2 \frac{\operatorname{Cov}(H_i, I_i)}{\operatorname{Var}(H_i)}
$$
The second term is the **[omitted variable bias](@entry_id:139684)**. Given our assumptions ($\beta_2 > 0$ and $\operatorname{Cov}(H_i, I_i) > 0$), the bias term is positive. The OLS estimate will systematically overestimate the true effect of study hours, because it mistakenly attributes part of the high performance of interested students to their study habits, when in fact it stems from their underlying interest.

This same logic applies in many financial and economic contexts. For example, in a regression of CEO compensation on firm performance, unobserved "CEO talent" is a likely omitted variable. More talented CEOs may improve firm performance and also command higher salaries, leading to an upward bias in the estimated return to performance (). Similarly, in a Capital Asset Pricing Model (CAPM) regression of a stock's excess return on the market's excess return, an unanticipated [monetary policy](@entry_id:143839) shock could affect both the overall market and a specific sector (like banking stocks) through an interest rate channel not captured by the model. This shock acts as an omitted variable correlated with the market return, violating the [exogeneity](@entry_id:146270) assumption ().

#### Simultaneity Bias

Endogeneity also arises when explanatory variables are not truly "independent," but are jointly determined with the [dependent variable](@entry_id:143677) in a system of equations. This is known as **simultaneity bias**.

Consider a simple macroeconomic model where an econometrician wishes to estimate the effect of money supply growth ($\Delta m_t$) on inflation ($\pi_t$) ():
$$
\pi_t = \beta_0 + \beta_1 \Delta m_t + \varepsilon_t
$$
This equation posits that money growth causes inflation. However, central banks actively conduct [monetary policy](@entry_id:143839). They observe inflationary pressures and react by adjusting the money supply. This behavior can be described by a policy reaction function:
$$
\Delta m_t = \gamma_0 - \gamma_1 \pi_t + v_t
$$
where $\gamma_1 > 0$ indicates that the central bank "tightens" policy (reduces money growth) in response to higher inflation. Because $\pi_t$ affects $\Delta m_t$ and $\Delta m_t$ affects $\pi_t$, they are determined simultaneously. By solving this system of equations, one can show that the regressor $\Delta m_t$ is a function of the structural error from the first equation, $\varepsilon_t$. Specifically, we find $\operatorname{Cov}(\Delta m_t, \varepsilon_t) \neq 0$. An unexpected shock $\varepsilon_t$ that increases inflation will, through the central bank's reaction, cause a contemporaneous decrease in $\Delta m_t$. This induces a [negative correlation](@entry_id:637494) between the regressor and the error term, leading OLS to produce a downwardly biased estimate of $\beta_1$.

#### Selection Bias

A third common source of [endogeneity](@entry_id:142125) is **[selection bias](@entry_id:172119)**. This occurs when the process of selecting observations into the sample is not random but is instead correlated with the unobserved factors in the error term.

Imagine a firm offers an optional advanced training course to its portfolio managers and wants to estimate the course's effect on subsequent performance ($y_i$) (). A regression of performance on a dummy variable for course participation ($D_i$) is proposed:
$$
y_i = \beta_0 + \beta_1 D_i + u_i
$$
The problem is that participation is voluntary. Managers who are more motivated, skilled, or ambitious (unobserved factors we can denote $\eta_i$) are more likely to enroll. These same traits also directly contribute to better performance. The error term $u_i$ contains these unobserved factors ($\eta_i$), while the regressor $D_i$ is also a function of them. This creates a correlation between $D_i$ and $u_i$. More motivated managers are both more likely to take the course and to perform well regardless. OLS cannot distinguish the effect of the course from the pre-existing high motivation of those who selected into it, leading to a positively biased estimate of the course's effect, $\beta_1$.

#### The Search for Causal Inference: Identification Strategies

The prevalence of [endogeneity](@entry_id:142125) means that running OLS on observational data rarely yields a causal estimate of a parameter. The creative and rigorous search for a solution to an [endogeneity](@entry_id:142125) problem is known as an **identification strategy**. The goal is to find a source of variation in the endogenous regressor $X$ that is "as-if random" and thus uncorrelated with the error term $u$.

A primary identification strategy is the use of **Instrumental Variables (IV)**. A valid instrument, $Z$, is a variable that is correlated with the endogenous regressor $X$ (relevance), but affects the outcome $Y$ only through its effect on $X$ and is otherwise uncorrelated with the error $u$ ([exogeneity](@entry_id:146270) and exclusion). Another strategy involves finding a **natural experiment**, where a real-world event or policy rule creates "as-if random" assignment to treatment, which can be used as an instrument. Even a **Randomized Controlled Trial (RCT)**, the gold standard for causal inference, can suffer from [endogeneity](@entry_id:142125) if there is imperfect compliance. In such cases, the initial random assignment to treatment can be used as an instrument for the treatment actually received to estimate a **Local Average Treatment Effect (LATE)** ().

### Assumption II: Spherical Errors

The second major set of assumptions concerns the variance-covariance structure of the error terms. The errors are assumed to be **spherical**, which encompasses two distinct conditions: homoskedasticity and no autocorrelation.

#### Homoskedasticity

The assumption of **homoskedasticity** requires that the variance of the error term is constant for all values of the explanatory variables:
$$
\operatorname{Var}(u_i \mid X) = \sigma^2
$$
This means that the scatter of the unobserved factors around the regression line is the same across all observations. When this assumption is violated, we have **[heteroskedasticity](@entry_id:136378)**, where the variance of the error depends on the regressors, $\operatorname{Var}(u_i \mid X) = \sigma_i^2$.

A classic example arises when modeling household electricity consumption as a function of income (). While there is a general trend that higher income leads to higher consumption, the variability in consumption also tends to increase with income. Low-income households have limited discretionary use, so their consumption is relatively stable. High-income households, however, own more devices and have greater discretion over their usage (e.g., heating a large pool, running multiple air conditioners). This leads to a wider range of possible consumption levels, meaning the variance of the unobserved [determinants](@entry_id:276593) of consumption, $u_i$, increases with income.

Crucially, [heteroskedasticity](@entry_id:136378) does not, by itself, cause bias or inconsistency in the OLS coefficient estimators, provided the [exogeneity](@entry_id:146270) assumption still holds. However, it has two important consequences:
1.  The OLS estimator is no longer the "Best" (most efficient) linear unbiased estimator. Other estimators, such as Weighted Least Squares (WLS), can achieve lower variance.
2.  The standard formulas for the variance of the OLS estimators are incorrect, rendering hypothesis tests (t-tests, F-tests) and [confidence intervals](@entry_id:142297) invalid.

The practical solution for inference in the presence of [heteroskedasticity](@entry_id:136378) is to use **Heteroskedasticity-Consistent (HC) standard errors**, often called [robust standard errors](@entry_id:146925), which provide a consistent estimate of the true standard errors even when the form of [heteroskedasticity](@entry_id:136378) is unknown.

#### No Autocorrelation

The second component of spherical errors is the assumption of **no autocorrelation** (or no serial correlation), which states that the error terms for any two different observations are uncorrelated:
$$
\operatorname{Cov}(u_i, u_j \mid X) = 0 \quad \text{for } i \neq j
$$
This assumption is often plausible in random cross-sectional data but is frequently violated in [time-series data](@entry_id:262935) (where shocks can persist over time) or in data with a clustered structure.

Consider a study of intergenerational income mobility that regresses an individual's income on their parents' income, where the dataset includes multiple siblings from the same family (). The error term, $u_{if}$ for individual $i$ in family $f$, captures unobserved factors like genetic endowments, family environment, social networks, and parental encouragement not captured by income. Since siblings share these family-level factors, their error terms will contain a common component. This induces a positive correlation between the errors of siblings from the same family: $\operatorname{Cov}(u_{if}, u_{jf}) > 0$ for $i \neq j$.

Like [heteroskedasticity](@entry_id:136378), the presence of autocorrelation does not bias OLS coefficient estimates, but it does render them inefficient and invalidates standard [statistical inference](@entry_id:172747). The solution is to use **clustered standard errors**, which adjust for the intra-group correlation, allowing for valid [hypothesis testing](@entry_id:142556).

### Assumption III: No Perfect Multicollinearity

For OLS to produce a unique set of estimates, we must assume **no perfect multicollinearity**. This means that none of the [independent variables](@entry_id:267118) is an exact linear function of one or more other [independent variables](@entry_id:267118). In matrix terms, the design matrix $\mathbf{X}$ must have full column rank, which ensures that the matrix $\mathbf{X}^{\top}\mathbf{X}$ is invertible.

Perfect multicollinearity is fundamentally an **identification problem**: if two variables are perfectly linearly related, the model cannot distinguish their individual effects on the [dependent variable](@entry_id:143677). Any attempt to estimate their coefficients will fail, as there are infinitely many possible combinations of coefficients that fit the data equally well.

A classic example is the **[dummy variable trap](@entry_id:635707)** (). Suppose a researcher wants to regress stock returns on a set of industry dummies (e.g., Technology, Healthcare, Financials). If the researcher includes a dummy for every single industry *and* an intercept term (a constant), perfect multicollinearity will occur. This is because the sum of all the industry dummies for any observation is always 1, which is identical to the intercept. The OLS estimation cannot be computed because $\mathbf{X}^{\top}\mathbf{X}$ is singular. The solution is to remove one of the redundant variables—either the intercept or one of the [dummy variables](@entry_id:138900). The omitted dummy category then becomes the baseline against which the other coefficients are interpreted.

It is important to distinguish perfect multicollinearity from **imperfect multicollinearity**, where regressors are highly but not perfectly correlated. Imperfect multicollinearity does not prevent OLS estimation but can lead to large standard errors and unstable coefficient estimates, making it difficult to precisely measure the individual effects of the correlated variables.

### Synthesis: The Geometric View of Gauss-Markov

The principles discussed can be unified through a geometric interpretation of the OLS estimator, which helps to clarify the distinct roles of the different assumptions (). In the $n$-dimensional space of observations, the vector of outcomes $\mathbf{y}$ can be viewed as a point. The columns of the regressor matrix $\mathbf{X}$ span a $k$-dimensional subspace. The OLS procedure finds the vector of fitted values, $\hat{\mathbf{y}} = \mathbf{X}\hat{\boldsymbol{\beta}}$, by performing an [orthogonal projection](@entry_id:144168) of $\mathbf{y}$ onto the [column space](@entry_id:150809) of $\mathbf{X}$.

-   The **[exogeneity](@entry_id:146270)** assumption, $\mathbb{E}[\mathbf{u} \mid \mathbf{X}] = \mathbf{0}$, ensures that the true regression line $\mathbf{X}\boldsymbol{\beta}$ is the center of the distribution of $\mathbf{y}$. When this holds, the OLS projection is centered on the true value, making the estimator $\hat{\boldsymbol{\beta}}$ **unbiased**.

-   The **spherical errors** assumption, $\operatorname{Var}(\mathbf{u} \mid \mathbf{X}) = \sigma^2 \mathbf{I}$, is the crucial condition for OLS to be **Best** (efficient). This assumption implies that the cloud of uncertainty around the true regression line is a sphere. In this "standard" Euclidean geometry, the shortest distance from a point to a plane is the perpendicular line, which corresponds to the OLS [orthogonal projection](@entry_id:144168). If errors are not spherical (i.e., heteroskedastic or autocorrelated), the uncertainty cloud is an ellipsoid. The standard OLS projection is no longer the most efficient way to estimate the model; a different projection, defined by the geometry of the [error covariance](@entry_id:194780) (i.e., Generalized Least Squares), would be more efficient.

-   The **no perfect multicollinearity** assumption ensures that the columns of $\mathbf{X}$ are linearly independent and thus form a proper $k$-dimensional basis for the subspace. If this fails, the subspace is of a lower dimension, and the mapping from a point in the subspace back to a unique coefficient vector $\hat{\boldsymbol{\beta}}$ is not possible.

In summary, the OLS assumptions provide a precise framework for understanding when and why [linear regression](@entry_id:142318) provides credible and efficient estimates. Violations of these assumptions are not mere technicalities; they represent fundamental challenges to [causal inference](@entry_id:146069) that require careful diagnosis and sophisticated solutions.