## Introduction
In biostatistics and epidemiology, isolating the true relationship between an exposure and an outcome is a paramount challenge. Often, this relationship is distorted by [confounding variables](@entry_id:199777), which can lead to incorrect or even dangerously misleading conclusions. Mantel-Haenszel stratified analysis provides a powerful and intuitive suite of statistical methods designed to address this very problem, allowing researchers to control for confounding and obtain a more accurate estimate of the true effect.

This article serves as a comprehensive guide to this essential technique. The first chapter, "Principles and Mechanisms," will unpack the statistical theory behind stratification, explaining how the Mantel-Haenszel methods work to test for association and estimate a common effect. Next, "Applications and Interdisciplinary Connections" will explore the method's real-world utility in cohort studies, case-control studies, clinical trials, and even [genetic epidemiology](@entry_id:171643). Finally, "Hands-On Practices" will provide practical exercises to solidify your understanding and build your skills in applying these methods to data. By moving from theory to application, you will gain a deep appreciation for Mantel-Haenszel analysis as a cornerstone of modern biomedical research.

## Principles and Mechanisms

Stratified analysis is a cornerstone of modern biostatistics and epidemiology, providing a robust framework for assessing the association between an exposure and an outcome while controlling for the influence of extraneous variables. The Mantel-Haenszel methods, in particular, offer a suite of powerful and intuitive tools for analyzing data from stratified studies. This chapter delineates the fundamental principles that motivate stratified analysis and the statistical mechanisms that underpin the Mantel-Haenszel procedures for testing and estimation.

### The Rationale for Stratified Analysis: Controlling Confounding

In observational studies, a primary challenge is to isolate the true association between an exposure of interest, $E$, and an outcome, $D$, from distortions caused by other factors. A **confounder** is a third variable, $Z$, that is associated with both the exposure $E$ and the outcome $D$ and is not on the causal pathway between them. This dual association creates a non-causal "backdoor" path of association, $E \leftarrow Z \rightarrow D$, which can bias the observed relationship between $E$ and $D$.

The purpose of stratified analysis is to "break" the influence of the confounder by examining the $E$-$D$ association separately within each level, or **stratum**, of the variable $Z$. By conditioning on the confounder, we effectively block the backdoor path. If the null hypothesis of no causal effect of $E$ on $D$ is true, then after conditioning on all confounders, $E$ and $D$ should be statistically independent. This [conditional independence](@entry_id:262650) is denoted as $E \perp D \mid Z$ [@problem_id:4808923].

The necessity of this approach can be dramatically illustrated. Consider a hypothetical study where the crude, unadjusted analysis suggests a protective effect, but a stratified analysis reveals a harmful effect in every stratum. This phenomenon, a severe form of confounding known as **Simpson's Paradox**, highlights the potential for unadjusted analyses to be dangerously misleading.

For instance, imagine a study yielding the following data, stratified by a binary variable $Z$ [@problem_id:4924622]:

-   **Stratum $Z=0$**: Odds Ratio ($OR_0$) = $\frac{6 \times 20}{3 \times 20} = 2.0$
-   **Stratum $Z=1$**: Odds Ratio ($OR_1$) = $\frac{20 \times 95}{190 \times 5} = 2.0$

Within each stratum, the odds of the outcome are twice as high for the exposed group as for the unexposed group. However, if we naively combine, or "collapse," the tables, the marginal data yield a crude odds ratio of:
$$ OR_{crude} = \frac{(6+20) \times (20+95)}{(3+190) \times (20+5)} = \frac{26 \times 115}{193 \times 25} \approx 0.62 $$

The crude analysis incorrectly suggests that the exposure is strongly protective, reducing the odds of the outcome by nearly $40\%$. The stratified analysis, by contrast, correctly reveals a consistent, harmful association in every subgroup defined by $Z$. The discrepancy arises because the stratifying variable $Z$ is associated with both exposure status and the baseline risk of the outcome, thus meeting the criteria for a confounder. Stratification effectively controls for this confounding, allowing for a valid assessment of the $E$-$D$ relationship.

### The Mantel-Haenszel Principle: Conditional Inference

The Mantel-Haenszel procedures are built upon the principle of **conditional inference**. This approach focuses on the structure of the data within each stratum's $2 \times 2$ table. For a given stratum $i$, we denote the cell counts as follows:

| | Outcome ($D=1$) | No Outcome ($D=0$) | Total |
| :--- | :---: | :---: | :---: |
| Exposed ($E=1$) | $a_i$ | $b_i$ | $n_{1i}$ |
| Unexposed ($E=0$) | $c_i$ | $d_i$ | $n_{0i}$ |
| Total | $m_{1i}$ | $m_{0i}$ | $n_i$ |

Here, $n_{1i}$ and $n_{0i}$ are the row totals (margins) for exposure, and $m_{1i}$ and $m_{0i}$ are the column totals (margins) for the outcome [@problem_id:4808962]. The core idea of the MH approach is to condition the analysis on these marginal totals in each stratum. Once the four margins are treated as fixed, the entire table is determined by the value of a single cell, conventionally taken as $a_i$, the count of exposed individuals with the outcome.

Under the null hypothesis of no association ($OR=1$) within a stratum, and conditional on the fixed margins, the [sampling distribution](@entry_id:276447) of the cell count $a_i$ is the **central hypergeometric distribution** [@problem_id:4808962] [@problem_id:4924690]. This can be conceptualized as drawing a sample of size $m_{1i}$ (the total cases) without replacement from a population of $n_i$ individuals, of whom $n_{1i}$ are "exposed." The random variable $a_i$ is the number of exposed individuals in the sample of cases.

The probability [mass function](@entry_id:158970) is given by:
$$ P(A_i = a_i \mid \text{margins}) = \frac{\binom{m_{1i}}{a_i} \binom{m_{0i}}{n_{1i}-a_i}}{\binom{n_i}{n_{1i}}} $$

The moments of this distribution—its [expectation and variance](@entry_id:199481)—are the fundamental building blocks for Mantel-Haenszel methods. Under the null hypothesis, they are determined solely by the fixed margins:
-   **Expectation**: $E[a_i] = \frac{n_{1i} m_{1i}}{n_i}$
-   **Variance**: $Var(a_i) = \frac{n_{1i} n_{0i} m_{1i} m_{0i}}{n_i^2 (n_i - 1)}$

These formulas provide, for each stratum, the expected count in cell $a_i$ if there were no association, and the variance of this count due to random sampling [@problem_id:4809039]. From this framework, it can be shown that the expected value of the cross-product difference, $a_i d_i - b_i c_i$, is zero under the null hypothesis, a property that is central to both testing and estimation [@problem_id:4808923].

### Testing for Association: The Cochran-Mantel-Haenszel (CMH) Test

To test the null hypothesis of no association across all strata (i.e., the common odds ratio is 1), the Cochran-Mantel-Haenszel (CMH) test combines information by summing the observed deviations from the null expectation. The [test statistic](@entry_id:167372) compares the total observed count of exposed cases, $\sum a_i$, to the total expected count, $\sum E[a_i]$.

The CMH test statistic is constructed as the squared sum of deviations, standardized by the sum of the variances:
$$ T_{CMH} = \frac{\left( \sum_{i=1}^{K} (a_i - E[a_i]) \right)^2}{\sum_{i=1}^{K} Var(a_i)} $$

where $E[a_i]$ and $Var(a_i)$ are the hypergeometric [expectation and variance](@entry_id:199481) defined previously [@problem_id:4809039]. By summing the deviations *before* squaring, the test is sensitive to associations that are, on average, in a consistent direction across strata. Assuming the number of strata or the counts within them are sufficiently large, the CMH statistic $T_{CMH}$ follows an asymptotic **chi-square ($\chi^2$) distribution with one degree of freedom** under the null hypothesis. The single degree of freedom reflects that the test is evaluating a single parameter: whether the common association departs from the null. A p-value is obtained by comparing the observed statistic to this $\chi^2_1$ distribution. For discrete data, a [continuity correction](@entry_id:263775) is sometimes applied to the numerator, which becomes $\left( \left| \sum (a_i - E[a_i]) \right| - 0.5 \right)^2$.

### Estimating a Common Effect Measure

When it is reasonable to assume that the strength of association is the same across all strata—an assumption known as **homogeneity of effect**—we can estimate a single, adjusted summary measure. The Mantel-Haenszel method provides estimators for the common odds ratio, risk ratio, and risk difference.

#### The Mantel-Haenszel Odds Ratio (OR)

The classic MH estimator for the common odds ratio, $\theta_{MH}$, is defined as:
$$ \hat{\theta}_{MH} = \frac{\sum_{i=1}^{K} \frac{a_i d_i}{n_i}}{\sum_{i=1}^{K} \frac{b_i c_i}{n_i}} $$
This elegant formula can be interpreted as the ratio of two pooled quantities. The numerator is a weighted sum of the $a_i d_i$ cross-products, and the denominator is a weighted sum of the $b_i c_i$ cross-products. In both cases, the weight for stratum $i$ is the inverse of the total stratum size, $1/n_i$ [@problem_id:4809013].

An algebraically equivalent and highly insightful representation shows that $\hat{\theta}_{MH}$ is a weighted average of the individual stratum-specific odds ratios ($OR_i = \frac{a_i d_i}{b_i c_i}$):
$$ \hat{\theta}_{MH} = \frac{\sum_{i=1}^{K} w_i OR_i}{\sum_{i=1}^{K} w_i} \quad \text{where the weights are} \quad w_i = \frac{b_i c_i}{n_i} $$
This shows that strata with a larger number of [discordant pairs](@entry_id:166371) (unexposed cases $c_i$ and exposed non-cases $b_i$) relative to their size contribute more to the final estimate. This weighting scheme ensures that the MH estimator is generally not equal to a simple, unweighted average of the stratum-specific odds ratios [@problem_id:4924587].

#### The Mantel-Haenszel Risk Ratio (RR) and Risk Difference (RD)

The MH principle can be extended to other effect measures, which is particularly relevant in cohort studies.

The **Mantel-Haenszel Risk Ratio** estimator is given by:
$$ \hat{RR}_{MH} = \frac{\sum_{i=1}^{K} \frac{a_i n_{0i}}{n_i}}{\sum_{i=1}^{K} \frac{c_i n_{1i}}{n_i}} $$
This can be understood as a ratio of weighted risks. The numerator is a weighted sum of the risk in the exposed group ($a_i/n_{1i}$), and the denominator is a weighted sum of the risk in the unexposed group ($c_i/n_{0i}$). The implicit weights for the risks are $w_i = \frac{n_{1i} n_{0i}}{n_i}$ [@problem_id:4924662].

The **Mantel-Haenszel Risk Difference** estimator is a weighted average of the stratum-specific risk differences:
$$ \hat{RD}_{MH} = \frac{\sum_{i=1}^{K} w_i \left( \frac{a_i}{n_{1i}} - \frac{c_i}{n_{0i}} \right)}{\sum_{i=1}^{K} w_i} $$
The standard MH weights for the risk difference are derived from inverse-variance principles and are given by $w_i = \frac{n_{1i} n_{0i}}{n_{1i} + n_{0i}}$. These weights give more influence to strata where the risk difference can be estimated with higher precision (i.e., large strata with a balanced allocation of exposed and unexposed subjects) [@problem_id:4924619].

### Effect Modification vs. Confounding: A Critical Distinction

The validity of pooling stratum-specific estimates into a single summary measure hinges on the assumption of homogeneity. When this assumption is violated—that is, when the true effect measure genuinely differs across strata—we have **effect modification** (or interaction).

Effect modification is a biological or social phenomenon, distinct from the statistical artifact of confounding. It implies that the effect of the exposure on the outcome depends on the level of the third variable $Z$. For example, a drug's effect may be stronger in one genetic group than another [@problem_id:4808966].

Consider a study where the stratum-specific odds ratios are markedly different, for instance, $OR_{Z=0} = 4.0$ and $OR_{Z=1} = 2.0$ [@problem_id:4808966]. In this case, reporting a single pooled estimate would be misleading as it would obscure this important finding. The appropriate action is to report the stratum-specific effects separately and conclude that the variable $Z$ modifies the effect of the exposure.

To formally assess the homogeneity assumption, one can use the **Breslow-Day test**. This test evaluates the null hypothesis that the odds ratios are equal across all strata: $H_0: \theta_1 = \theta_2 = \dots = \theta_K$ [@problem_id:4809007]. The test statistic is a sum of squared deviations of the observed counts ($a_k$) from their expected values, where the expectation is calculated under the assumption of a common odds ratio (estimated by $\hat{\theta}_{MH}$):
$$ Q_{BD} = \sum_{k=1}^K \frac{(a_k - E_{\hat{\theta}_{MH}}[a_k])^2}{Var_{\hat{\theta}_{MH}}(a_k)} $$
Under the null hypothesis of homogeneity, $Q_{BD}$ follows an asymptotic $\chi^2$ distribution with $K-1$ degrees of freedom. A small p-value from this test provides evidence against the homogeneity assumption, suggesting the presence of effect modification.

### Advanced Topic: Non-Collapsibility of the Odds Ratio

A final, subtle principle concerns a mathematical property of the odds ratio known as **non-collapsibility**. While a discrepancy between a crude and an adjusted estimate is a necessary sign of confounding, it is not sufficient. The odds ratio can fail to be "collapsible"—meaning the crude OR can differ from the common conditional OR—even in the complete absence of confounding.

This occurs when the stratifying variable $Z$ is associated with the outcome $D$ but is *not* associated with the exposure $E$. In this scenario, $Z$ is not a confounder. However, if the common odds ratio is not equal to $1$, the crude odds ratio will still be attenuated towards the null compared to the common conditional odds ratio [@problem_id:4809042].

This mathematical curiosity arises because the odds ratio is a non-linear function of probabilities. Unlike the risk difference, which is collapsible, the crude odds ratio is not a simple weighted average of the stratum-specific odds ratios. Therefore, observing that a crude OR differs from an MH-adjusted OR does not, on its own, prove the existence of confounding. One must also establish that the stratifying variable is associated with the exposure. This distinction underscores the importance of a careful theoretical framework when interpreting the results of stratified analyses.