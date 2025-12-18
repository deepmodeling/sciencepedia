## Introduction
Stratified sampling is a cornerstone of statistical methodology, renowned for its power to enhance the precision of estimates by partitioning a population into homogeneous subgroups, or strata. A fundamental question in its application is how to distribute a fixed number of samples among these strata to achieve the greatest efficiency. Proportional allocation offers an intuitive and widely adopted answer to this problem, suggesting that the sample size in each stratum should be directly proportional to its relative size in the population. While simple, this method has profound implications for [variance reduction](@entry_id:145496) and is a critical tool in fields ranging from survey design to computational science. This article delves into the theory, application, and practical considerations of [proportional allocation](@entry_id:634725).

Across the following chapters, we will systematically unpack this powerful technique. In "Principles and Mechanisms," we will derive the stratified estimator, analyze its variance, and reveal how [proportional allocation](@entry_id:634725) eliminates between-stratum variance. We will also investigate the conditions under which it is optimal and explore its limitations. Following this theoretical foundation, "Applications and Interdisciplinary Connections" will showcase its utility in real-world scenarios, from ecological surveillance and public health to advanced Monte Carlo simulations in finance and physics. Finally, "Hands-On Practices" will provide guided exercises to solidify your understanding and allow you to apply these concepts to concrete problems.

## Principles and Mechanisms

This chapter delineates the foundational principles of [stratified sampling](@entry_id:138654), with a particular focus on [proportional allocation](@entry_id:634725). We will construct the stratified estimator from first principles, analyze its variance, and elucidate the mechanism by which it achieves [variance reduction](@entry_id:145496). Subsequently, we will explore the conditions under which [proportional allocation](@entry_id:634725) is optimal and investigate its performance, especially in scenarios involving cost heterogeneity and [high-dimensional integration](@entry_id:143557).

### The Stratified Estimator: Construction and Unbiasedness

Stratified sampling begins with a partition of the population of interest. In [survey sampling](@entry_id:755685), a finite population $U$ of size $N$ is divided into $H$ disjoint strata $U_1, U_2, \dots, U_H$ of sizes $N_1, N_2, \dots, N_H$. The **stratum weights** are defined by the population proportions $W_h = N_h / N$. In the context of Monte Carlo integration, we estimate an integral $I = \int_{\mathcal{X}} f(x) p(x) dx = \mathbb{E}_p[f(X)]$. The domain $\mathcal{X}$ is partitioned into $H$ disjoint strata $\mathcal{S}_1, \mathcal{S}_2, \dots, \mathcal{S}_H$, and the stratum weights are the probability masses $W_h = \mathbb{P}(X \in \mathcal{S}_h)$.

The overall [population mean](@entry_id:175446) $\mu$ (or integral $I$) can be expressed as a weighted average of the individual stratum means $\mu_h$:
$$
\mu = \sum_{h=1}^{H} W_h \mu_h
$$
where $\mu_h$ is the true mean of the variable of interest within stratum $h$. This identity is a direct consequence of the law of total expectation.

A natural way to construct an estimator for $\mu$ is to replace each unknown stratum mean $\mu_h$ with a sample-based estimate. For each stratum $h$, we draw a sample of size $n_h$ and compute the sample mean $\bar{Y}_h$. By substituting these sample means into the population identity, we form the **stratified estimator** $\hat{\mu}_{\text{str}}$:
$$
\hat{\mu}_{\text{str}} = \sum_{h=1}^{H} W_h \bar{Y}_h
$$
A crucial property of this estimator is that it is **design-unbiased**, provided that the sample mean $\bar{Y}_h$ is an unbiased estimator of the true stratum mean $\mu_h$. This is typically ensured by using [simple random sampling](@entry_id:754862) within each stratum. By the linearity of expectation:
$$
\mathbb{E}[\hat{\mu}_{\text{str}}] = \mathbb{E}\left[\sum_{h=1}^{H} W_h \bar{Y}_h\right] = \sum_{h=1}^{H} W_h \mathbb{E}[\bar{Y}_h] = \sum_{h=1}^{H} W_h \mu_h = \mu
$$
This unbiasedness holds for *any* choice of positive sample sizes $n_1, n_2, \dots, n_H$. The weights $W_h$ in the estimator are determined by the population structure itself, not by the sample allocation. This "plug-in" construction ensures that the estimator correctly reflects the composition of the underlying population .

### Variance Analysis and Proportional Allocation

While the choice of sample sizes $n_h$ does not affect the estimator's unbiasedness, it critically determines its variance and, therefore, its efficiency. Assuming that samples are drawn independently across different strata, the variance of the stratified estimator is:
$$
\operatorname{Var}(\hat{\mu}_{\text{str}}) = \operatorname{Var}\left(\sum_{h=1}^{H} W_h \bar{Y}_h\right) = \sum_{h=1}^{H} W_h^2 \operatorname{Var}(\bar{Y}_h)
$$
If [simple random sampling](@entry_id:754862) is used to draw $n_h$ samples from stratum $h$ (with population variance $\sigma_h^2$), the variance of the sample mean is $\operatorname{Var}(\bar{Y}_h) = \sigma_h^2 / n_h$ (ignoring finite population corrections, which is standard in Monte Carlo contexts or for very large populations). The general variance formula for the stratified estimator is thus:
$$
\operatorname{Var}(\hat{\mu}_{\text{str}}) = \sum_{h=1}^{H} \frac{W_h^2 \sigma_h^2}{n_h}
$$
This formula reveals that the total variance is a sum of contributions from each stratum, with each contribution depending on the stratum's weight ($W_h$), its internal variability ($\sigma_h^2$), and the number of samples allocated to it ($n_h$).

**Proportional allocation** is an intuitive and common method for distributing a total sample size $n$ among the strata. It allocates samples in proportion to the stratum weights:
$$
n_h = n W_h
$$
Under this rule, larger or more probable strata receive more samples. Substituting this allocation into the general variance formula yields the variance for [proportional allocation](@entry_id:634725) :
$$
\operatorname{Var}(\hat{\mu}_{\text{prop}}) = \sum_{h=1}^{H} \frac{W_h^2 \sigma_h^2}{n W_h} = \frac{1}{n} \sum_{h=1}^{H} W_h \sigma_h^2
$$
The variance is simply the weighted average of the within-stratum variances, scaled by the total sample size $n$.

### The Mechanism of Variance Reduction

To understand why stratification is effective, we compare the variance of the proportional stratified estimator to that of a simple (or crude) Monte Carlo (CMC) estimator based on $n$ [independent samples](@entry_id:177139) drawn from the entire population. The variance of the CMC estimator is $\operatorname{Var}(\hat{\mu}_{\text{CMC}}) = \frac{1}{n}\operatorname{Var}(Y)$, where $Y$ is the random variable of interest.

The **Law of Total Variance** provides the key to this comparison. It decomposes the total variance of $Y$ into two components:
$$
\operatorname{Var}(Y) = \mathbb{E}[\operatorname{Var}(Y \mid \text{stratum})] + \operatorname{Var}(\mathbb{E}[Y \mid \text{stratum}])
$$
The first term, $\mathbb{E}[\operatorname{Var}(Y \mid \text{stratum})] = \sum_{h=1}^H W_h \sigma_h^2$, is the average of the variances *within* the strata. The second term, $\operatorname{Var}(\mathbb{E}[Y \mid \text{stratum}]) = \sum_{h=1}^H W_h (\mu_h - \mu)^2$, is the variance *between* the stratum means.

The variance of the CMC estimator is therefore:
$$
\operatorname{Var}(\hat{\mu}_{\text{CMC}}) = \frac{1}{n} \left( \sum_{h=1}^{H} W_h \sigma_h^2 + \sum_{h=1}^{H} W_h (\mu_h - \mu)^2 \right)
$$
Comparing this with the variance under [proportional allocation](@entry_id:634725), $\operatorname{Var}(\hat{\mu}_{\text{prop}}) = \frac{1}{n} \sum_{h=1}^{H} W_h \sigma_h^2$, we see that the entire "between-stratum" variance component has been eliminated .

This is the central mechanism of [variance reduction](@entry_id:145496) in [stratified sampling](@entry_id:138654). In crude Monte Carlo, the number of samples falling into each stratum is random. This randomness contributes to the overall variance through the between-stratum term. By fixing the number of samples per stratum ($n_h$), [stratified sampling](@entry_id:138654) removes this source of randomness entirely. The variance reduction is precisely $\frac{1}{n} \sum W_h (\mu_h - \mu)^2$, which is always non-negative. Therefore, [proportional allocation](@entry_id:634725) never increases variance compared to crude Monte Carlo and will strictly decrease it unless all stratum means $\mu_h$ are identical  .

### The Question of Optimality

While [proportional allocation](@entry_id:634725) is simple and guarantees variance reduction over CMC, it is not always the most efficient way to allocate samples. The [optimal allocation](@entry_id:635142) is the one that minimizes the variance $\operatorname{Var}(\hat{\mu}_{\text{str}}) = \sum_{h=1}^{H} \frac{W_h^2 \sigma_h^2}{n_h}$ for a fixed total sample size $n = \sum n_h$. Using the method of Lagrange multipliers, one can show that the [optimal allocation](@entry_id:635142), known as **Neyman allocation**, assigns samples according to the rule :
$$
n_h^{\text{opt}} \propto W_h \sigma_h
$$
This rule dictates that more samples should be allocated to strata that are large (high $W_h$) and/or have high internal variability (high $\sigma_h$).

Proportional allocation ($n_h \propto W_h$) coincides with the optimal Neyman allocation if and only if the within-stratum standard deviations $\sigma_h$ are constant across all strata  . When $\sigma_h$ varies significantly, [proportional allocation](@entry_id:634725) can be highly suboptimal.

Consider a scenario from rare-event simulation, where a small stratum (e.g., $W_2=0.01$) contains most of the variance (e.g., $\sigma_2^2=100$), while a large stratum ($W_1=0.99$) has very low variance ($\sigma_1^2=0.01$). Proportional allocation would assign 99 times more samples to the low-variance stratum, effectively "wasting" them where precision is already high, while severely under-sampling the high-variance region where they are most needed. In this specific case, the variance under [proportional allocation](@entry_id:634725) can be over 25 times larger than the variance under the optimal Neyman allocation, highlighting the potential inefficiency of ignoring stratum-specific variance information .

### Incorporating Heterogeneous Costs

In many practical applications, the cost of obtaining a sample, $c_h$, varies by stratum. The objective then becomes to minimize variance for a fixed total budget $C = \sum c_h n_h$. The optimization problem is modified accordingly, and the resulting **cost-[optimal allocation](@entry_id:635142)** is :
$$
n_h^{\text{opt}} \propto \frac{W_h \sigma_h}{\sqrt{c_h}}
$$
This extended rule provides an intuitive directive: allocate more samples to strata that are large, highly variable, and cheap to sample, while allocating fewer samples to strata that are small, homogeneous, or expensive to sample.

A naive allocation that is merely proportional to stratum weight and inversely proportional to cost (e.g., $n_h \propto W_h / c_h$) fails to account for the crucial roles of $\sigma_h$ and the square root of the cost. In a scenario with varying costs and variances, such a naive rule can be significantly less efficient than the true cost-[optimal allocation](@entry_id:635142). For example, in a hypothetical three-stratum problem, a "cost-proportional" rule could result in a variance nearly twice as large as the minimum achievable variance for the same budget .

### Context, Limitations, and Extensions

**Stratification in High Dimensions:** The effectiveness of stratification can diminish rapidly as the dimension $d$ of the integration domain increases—a manifestation of the **curse of dimensionality**. Stratifying along a single coordinate $X_j$ only removes the variance component associated with the main effect of that coordinate, $\operatorname{Var}(\mathbb{E}[f(X) \mid X_j])$. In many high-dimensional problems, the total variance of $f(X)$ is dominated by interactions between multiple variables, meaning that any single coordinate has a very small main effect. In such cases, single-axis stratification yields negligible [variance reduction](@entry_id:145496). A principled strategy for choosing a stratification axis is to identify the direction $\mathbf{a}$ in the input space along which the function varies the most, i.e., the direction that maximizes $\operatorname{Var}(\mathbb{E}[f(X) \mid \mathbf{a}^\top X])$. This connects stratification to the broader field of [sensitivity analysis](@entry_id:147555) .

**Relation to Other Methods:** It is instructive to contrast [stratified sampling](@entry_id:138654) with other [variance reduction techniques](@entry_id:141433). **Importance sampling** modifies the [sampling distribution](@entry_id:276447) itself and corrects for the change with multiplicative weights. In contrast, [stratified sampling](@entry_id:138654) retains the original conditional distributions but deterministically allocates the number of samples drawn from each. The two are distinct paradigms . However, stratification can be powerfully combined with other methods. For instance, after stratification has eliminated the between-stratum variance, **Quasi-Monte Carlo (QMC)** methods, such as those using scrambled Sobol' sequences, can be applied independently *within* each stratum. This hybrid approach uses QMC to estimate the within-stratum means more efficiently than standard Monte Carlo, thereby tackling the remaining source of error and potentially achieving a much faster overall convergence rate .