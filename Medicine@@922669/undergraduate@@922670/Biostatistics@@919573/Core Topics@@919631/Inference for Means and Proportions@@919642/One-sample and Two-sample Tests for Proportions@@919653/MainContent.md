## Introduction
Tests for proportions are a cornerstone of biostatistical analysis, providing the framework for drawing conclusions from [binary outcome](@entry_id:191030) data, such as treatment success or disease presence. While the concept of comparing percentages seems intuitive, the rigorous application of these tests is filled with critical nuances that can profoundly impact research findings. A common challenge for students and researchers lies in navigating the choices between different test procedures and understanding the crucial assumptions that underpin their validity. This article addresses this gap by providing a comprehensive guide to one- and two-[sample proportion](@entry_id:264484) tests. We will begin in "Principles and Mechanisms" by building the theoretical foundation from the Bernoulli and Binomial distributions and detailing the mechanics of key procedures like the [z-test](@entry_id:169390) and Fisher's exact test. Subsequently, the "Applications and Interdisciplinary Connections" chapter will demonstrate how these fundamental tools are adapted for sophisticated real-world scenarios, including noninferiority trials, stratified analysis to control for confounding, and analysis of clustered data. Finally, "Hands-On Practices" will provide opportunities to apply these concepts to practical problems, reinforcing the skills needed for robust study design and data analysis.

## Principles and Mechanisms

### The Foundational Models for Proportions: Bernoulli and Binomial

Statistical inference for proportions begins with the simplest case of a [binary outcome](@entry_id:191030). For each subject or experimental unit, we observe one of two mutually exclusive results, which are generically labeled "success" and "failure." In a clinical context, a success could be a patient's positive response to treatment, [seroconversion](@entry_id:195698) after vaccination, or remission from a disease. We model the outcome for a single subject, $Y_i$, as a **Bernoulli random variable**. If $Y_i=1$ denotes a success and $Y_i=0$ a failure, the probability mass function (PMF) is given by:
$$ \Pr(Y_i=y) = p^y(1-p)^{1-y} \quad \text{for } y \in \{0, 1\} $$
The parameter $p = \Pr(Y_i=1)$ is the population proportion or probability of success. It is the central quantity we wish to estimate or test hypotheses about.

When we have a sample of $n$ subjects, we typically assume their outcomes are **[independent and identically distributed](@entry_id:169067) (i.i.d.)**. This means that each subject's outcome is drawn from the same Bernoulli distribution with parameter $p$, and the outcome for one subject does not influence the outcome for another. Under this i.i.d. assumption, the total number of successes in the sample, $X = \sum_{i=1}^n Y_i$, follows a **Binomial distribution**, denoted $X \sim \mathrm{Bin}(n,p)$. Its PMF is:
$$ \Pr(X=k) = \binom{n}{k} p^k (1-p)^{n-k} \quad \text{for } k \in \{0, 1, \dots, n\} $$

A fundamental concept in [statistical inference](@entry_id:172747) is that of a **sufficient statistic**, which is a function of the data that captures all the information relevant to the parameter of interest. For the [binomial model](@entry_id:275034), the count of successes, $X$, is a sufficient statistic for the proportion $p$. To see this, we can examine the joint probability of observing a specific sequence of outcomes $(y_1, y_2, \dots, y_n)$. By the i.i.d. assumption:
$$ \Pr(Y_1=y_1, \dots, Y_n=y_n) = \prod_{i=1}^n p^{y_i}(1-p)^{1-y_i} = p^{\sum y_i} (1-p)^{n - \sum y_i} = p^k (1-p)^{n-k} $$
where $k = \sum y_i$ is the observed total number of successes. This [joint probability](@entry_id:266356) depends on the data only through the total count $k$. According to the **Fisher-Neyman [factorization theorem](@entry_id:749213)**, this implies that the statistic $X = \sum Y_i$ is sufficient for $p$. Knowing the total count of successes tells us everything the sample can about $p$; the specific order in which the successes and failures occurred provides no additional information [@problem_id:4934177].

This leads to another key property: **[identifiability](@entry_id:194150)**. A parameter is identifiable if different values of the parameter lead to different probability distributions for the observable data. For the binomial model with a known sample size $n$, the parameter $p$ is identifiable because for any two distinct proportions $p_1 \neq p_2$, the resulting binomial distributions $\mathrm{Bin}(n, p_1)$ and $\mathrm{Bin}(n, p_2)$ are also distinct. This property is essential, as it ensures that we can, in principle, learn the true value of $p$ from the data [@problem_id:4934204].

### Hypothesis Testing for a Single Proportion

A common task is to test whether an unknown population proportion $p$ is equal to some pre-specified benchmark value $p_0$. This is formulated as a hypothesis test with the null hypothesis $H_0: p = p_0$.

#### The Exact Binomial Test

Since the exact distribution of the success count $X$ under the null hypothesis is known to be $\mathrm{Bin}(n, p_0)$, we can perform a test without relying on any approximations. This is called the **[exact binomial test](@entry_id:170573)**. The procedure involves calculating the probability of observing a result as extreme or more extreme than the one actually observed, assuming $H_0$ is true. This probability is the **p-value**.

For a one-sided alternative, such as $H_A: p > p_0$, the p-value is the probability of observing the observed count $x$ or anything larger: $p = \Pr(X \ge x | p_0) = \sum_{k=x}^n \binom{n}{k} p_0^k (1-p_0)^{n-k}$.

For a two-sided alternative, $H_A: p \neq p_0$, defining "as or more extreme" is more complex, especially if the binomial distribution is skewed ($p_0 \neq 0.5$). A principled and common approach is the **method of small probabilities**. With this method, we define extremity based on the probability of each outcome under $H_0$. An outcome is considered as or more extreme than the observed count $x$ if its probability under $H_0$ is less than or equal to the probability of $x$. The two-sided p-value is then the sum of probabilities of all such outcomes:
$$ p\text{-value} = \sum_{k \,:\, \Pr(X=k|p_0) \le \Pr(X=x|p_0)} \Pr(X=k|p_0) $$
This method ensures that the rejection region of the test consists of the least likely outcomes under the null hypothesis, providing a valid, albeit sometimes conservative, test [@problem_id:4934203].

#### The Large-Sample z-Test and the Normal Approximation

When the sample size $n$ is large, the binomial distribution can be well-approximated by a normal distribution, a consequence of the **Central Limit Theorem (CLT)**. The sample proportion $\hat{p} = X/n$ has mean $E[\hat{p}] = p$ and variance $\mathrm{Var}(\hat{p}) = \frac{p(1-p)}{n}$. The CLT implies that for large $n$, the distribution of $\hat{p}$ is approximately normal: $\hat{p} \approx N(p, \frac{p(1-p)}{n})$.

This justifies the use of a **[z-test](@entry_id:169390)**. The general form of the z-statistic is:
$$ Z = \frac{\text{Estimate} - \text{Null Value}}{\text{Standard Error under Null}} $$
When testing $H_0: p = p_0$, the null value is $p_0$. The crucial choice is the [standard error](@entry_id:140125). Since the test is conducted under the assumption that $H_0$ is true, the variance of $\hat{p}$ should be calculated using $p_0$. This leads to the **[score test](@entry_id:171353)** statistic:
$$ Z_{\text{score}} = \frac{\hat{p} - p_0}{\sqrt{p_0(1-p_0)/n}} $$
An alternative, the **Wald test** statistic, uses the sample estimate $\hat{p}$ in the standard error: $Z_{\text{Wald}} = \frac{\hat{p} - p_0}{\sqrt{\hat{p}(1-\hat{p})/n}}$. While asymptotically equivalent, the [score test](@entry_id:171353) is generally preferred for [hypothesis testing](@entry_id:142556) as it maintains better control over the **Type I error rate** (the probability of falsely rejecting a true null hypothesis) in finite samples. The Wald standard error is more appropriate for constructing [confidence intervals](@entry_id:142297) around the estimate $\hat{p}$.

For example, consider a scenario testing $H_0: p = 0.5$ with a sample size of $n=40$. The [score test](@entry_id:171353) uses a fixed standard error based on $p_0=0.5$. The Wald test uses a [standard error](@entry_id:140125) that depends on the observed count, $k$. For an observed count of $k=14$ ($\hat{p}=0.35$), the Wald statistic is larger in magnitude than the score statistic. This can lead to different rejection decisions. A careful analysis shows that for this scenario, the Wald test would reject $H_0$ at the $\alpha=0.05$ level, while the better-calibrated [score test](@entry_id:171353) would not. The actual Type I error rate for the Wald test can be significantly inflated above the nominal $\alpha$, whereas the [score test](@entry_id:171353) provides a size closer to $\alpha$ [@problem_id:4934192].

The validity of any [z-test](@entry_id:169390) hinges on the quality of the [normal approximation](@entry_id:261668). A common but misleading rule is to require $n \ge 30$. This is insufficient for proportions. The shape of the binomial distribution depends on both $n$ and $p$. If $p$ is close to 0 or 1, the distribution is highly skewed, and a much larger $n$ is needed for the symmetric normal distribution to be a good fit. A more reliable guideline is to check the expected number of successes and failures under the null hypothesis. The approximation is generally considered adequate if both **$np_0 \ge 10$** and **$n(1-p_0) \ge 10$**. This ensures the distribution is not compressed against its boundaries and has reduced [skewness](@entry_id:178163) [@problem_id:4934213].

### Hypothesis Testing for Two Proportions

A frequent objective in biostatistics is to compare proportions from two independent groups, such as a treatment group and a control group in a clinical trial. Let the data be $X_1 \sim \mathrm{Bin}(n_1, p_1)$ and $X_2 \sim \mathrm{Bin}(n_2, p_2)$, assumed to be independent. Our goal is to test the null hypothesis $H_0: p_1 = p_2$.

Just as in the one-sample case, the pair of counts $(X_1, X_2)$ is jointly sufficient for the pair of parameters $(p_1, p_2)$ [@problem_id:4934177]. We can compare the proportions using several metrics:
-   **Risk Difference (RD)**: $\Delta = p_1 - p_2$
-   **Risk Ratio (RR)**: $RR = p_1 / p_2$
-   **Odds Ratio (OR)**: $OR = \frac{p_1/(1-p_1)}{p_2/(1-p_2)}$

The null hypothesis of no difference, $p_1 = p_2$, is equivalent to $\Delta=0$, $RR=1$, and $OR=1$. Although the null hypotheses are parametrically identical, the specific tests developed for each metric are not identical in finite samples due to differences in their variance estimations [@problem_id:4934161]. Here, we focus on the most common test, which is for the risk difference.

#### The Pooled Two-Sample z-Test

Under the null hypothesis $H_0: p_1 = p_2$, there is a single, common proportion $p$. This unknown common $p$ is a **nuisance parameter**. The logic of the [score test](@entry_id:171353) dictates that we should estimate this [nuisance parameter](@entry_id:752755) under the null hypothesis to construct our [test statistic](@entry_id:167372). The most [efficient estimator](@entry_id:271983) for the common proportion is the **[pooled proportion](@entry_id:162685)**, which combines data from both groups:
$$ \hat{p}_{\text{pool}} = \frac{X_1 + X_2}{n_1 + n_2} $$
The [standard error](@entry_id:140125) of the difference in sample proportions, $\hat{p}_1 - \hat{p}_2$, is estimated using this pooled value. The resulting **pooled two-sample [z-test](@entry_id:169390)** statistic is:
$$ Z = \frac{(\hat{p}_1 - \hat{p}_2) - 0}{\sqrt{\hat{p}_{\text{pool}}(1-\hat{p}_{\text{pool}})\left(\frac{1}{n_1} + \frac{1}{n_2}\right)}} $$
Under $H_0$, this statistic follows an approximate standard normal distribution for large samples. This test is the [score test](@entry_id:171353) for the two-sample proportion problem and generally has good Type I error control [@problem_id:4934202].

For instance, in a study comparing two vaccines, suppose vaccine A resulted in $X_1=42$ seroconversions out of $n_1=240$ subjects, and vaccine B had $X_2=26$ out of $n_2=260$. We wish to test if vaccine A has a higher [seroconversion](@entry_id:195698) rate ($H_A: p_1 > p_2$) at $\alpha=0.05$.
- Sample proportions: $\hat{p}_1 = 42/240 = 0.175$ and $\hat{p}_2 = 26/260 = 0.1$.
- Pooled proportion: $\hat{p}_{\text{pool}} = (42+26)/(240+260) = 68/500 = 0.136$.
- The [test statistic](@entry_id:167372) is $Z = \frac{0.175 - 0.1}{\sqrt{0.136(1-0.136)\left(\frac{1}{240} + \frac{1}{260}\right)}} \approx 2.44$.
- The one-sided p-value is $\Pr(Z \ge 2.44) \approx 0.007$. Since $0.007  0.05$, we reject $H_0$ and conclude there is significant evidence that vaccine A has a higher [seroconversion](@entry_id:195698) rate [@problem_id:4934219].

The conditions for the validity of this [z-test](@entry_id:169390) are an extension of the one-sample case: all four *expected* cell counts in the $2 \times 2$ table of group vs. outcome must be sufficiently large. We check this using the [pooled proportion](@entry_id:162685): $n_1\hat{p}_{\text{pool}}$, $n_1(1-\hat{p}_{\text{pool}})$, $n_2\hat{p}_{\text{pool}}$, and $n_2(1-\hat{p}_{\text{pool}})$ should all be at least 5, or more conservatively, 10 [@problem_id:4934213].

#### Fisher's Exact Test

When sample sizes are small or event counts are low (so-called "sparse data"), the [normal approximation](@entry_id:261668) for the [z-test](@entry_id:169390) is unreliable. A clinical study with $n_1=35$ patients in one arm, only $x_1=1$ of whom achieve suppression, is a classic example where the [z-test](@entry_id:169390) is inappropriate [@problem_id:4934212]. In these situations, an exact method is required.

**Fisher's [exact test](@entry_id:178040)** provides a way to compute an exact p-value without relying on large-sample approximations. The key idea is to eliminate the [nuisance parameter](@entry_id:752755) $p$ by **conditioning on the margins** of the $2 \times 2$ contingency table. That is, we consider the row totals ($n_1, n_2$) and column totals ($X_1+X_2, n_1+n_2 - (X_1+X_2)$) to be fixed.

Given these fixed margins, the probability of observing a particular count $x$ in the upper-left cell of the table follows a **[hypergeometric distribution](@entry_id:193745)**. This can be derived from a [combinatorial argument](@entry_id:266316). Imagine an urn containing $N=n_1+n_2$ balls, of which $K=X_1+X_2$ are "successes". If we draw $n=n_1$ balls without replacement (representing the subjects in group 1), the probability of getting exactly $x$ successes is:
$$ \Pr(X_{11}=x | n_1, n_2, K) = \frac{\binom{K}{x} \binom{N-K}{n_1-x}}{\binom{N}{n_1}} $$
This distribution does not depend on the unknown proportion $p$. To get a p-value, we sum these hypergeometric probabilities for all tables that are as extreme or more extreme than the one observed.

Consider a case-control study with the following table of colonization status by hospital ward:
|         | Colonized | Not Colonized | Total |
|---------|-----------|---------------|-------|
| Ward 1  | 7         | 0             | 7     |
| Ward 2  | 2         | 5             | 7     |
| Total   | 9         | 5             | 14    |
Here, $N=14$, $K=9$, and we are looking at the distribution of the count in the top-left cell, which can range from 2 to 7. The probability of the observed table ($x=7$) is $\Pr(X=7) = \frac{\binom{9}{7}\binom{5}{0}}{\binom{14}{7}} = \frac{36 \times 1}{3432} \approx 0.01049$. To get a one-sided p-value, we would sum probabilities for $X \ge 7$, which is just this value. For a two-sided p-value, we would add the probabilities of all tables that are equally or less likely to occur, which in this symmetric case includes the table with $X=2$ in the top-left cell, giving a p-value of approximately $2 \times 0.01049 = 0.02098$ [@problem_id:4934218]. Because it makes no distributional approximations, Fisher's test is "exact." However, due to the discreteness of the [hypergeometric distribution](@entry_id:193745), it can be conservative, meaning its actual Type I error rate is often strictly less than the nominal level $\alpha$.

### The Importance of Underlying Assumptions

The validity of all the tests described above rests on critical assumptions about the data-generating process. Violating these assumptions can severely compromise the conclusions of a study.

1.  **Identical Distribution:** The standard one-sample and two-sample tests assume that the success probability is constant for all individuals within a group. If individuals have heterogeneous probabilities (e.g., some are healthier than others), the variance of the [sample proportion](@entry_id:264484) is actually smaller than the binomial variance suggests. Using a standard [z-test](@entry_id:169390) in this situation would be conservative, leading to a loss of statistical power [@problem_id:4934204].

2.  **Independence:** This is arguably the most critical and most frequently violated assumption in practice. Many studies involve **clustered data**, where subjects are grouped (e.g., patients within hospitals, students within schools). Outcomes for subjects within the same cluster are often correlated. For example, patients at a single clinic might share similar care practices or environmental exposures, inducing a positive correlation in their outcomes. This positive correlation inflates the true variance of the [sample proportion](@entry_id:264484). A standard test that ignores this clustering (i.e., assumes independence) will systematically underestimate the true variance. This leads to a test statistic that is artificially large and a p-value that is artificially small. The test becomes **anticonservative**, meaning its actual Type I error rate can be much higher than the nominal $\alpha$ level, leading to an excess of false-positive findings. It is crucial to use statistical methods that account for clustering, such as generalized estimating equations (GEE) or mixed-effects models, when such [data structures](@entry_id:262134) are present [@problem_id:4934204]. It is a common misconception that conditional tests like Fisher's exact test are immune to this; the assumption of exchangeability underlying the hypergeometric model is also violated by clustering.

In summary, while the mechanics of one- and two-sample proportion tests are straightforward, their correct application requires a careful consideration of the sample size, [data sparsity](@entry_id:136465), and, most importantly, the underlying assumptions of the statistical model.