## Introduction
In the landscape of statistical analysis, parametric tests like the $t$-test are powerful but rest on strong assumptions, such as the normality of data. When these assumptions are questionable, nonparametric rank-based methods provide robust and reliable alternatives. This article addresses the common challenge of assessing central tendency in one-sample or paired-data settings without relying on distributional assumptions. It offers a deep dive into two cornerstone nonparametric procedures: the Sign Test and the Wilcoxon Signed-Rank Test.

This article will guide you from foundational theory to practical application across three focused chapters.
- In **Principles and Mechanisms**, we will establish a unified framework for one-sample and paired data, dissect the core logic and assumptions of both the Sign Test and the Wilcoxon Signed-Rank Test, and detail practical procedures for handling data complexities like ties and zeros.
- **Applications and Interdisciplinary Connections** will explore the real-world utility of these tests in fields ranging from clinical trials and environmental science to computational biology and engineering. We will also examine deeper theoretical concepts, including the duality between testing and estimation, statistical power, and the robustness that makes these tests so valuable.
- Finally, **Hands-On Practices** will provide targeted exercises to solidify your understanding of calculating test statistics, deriving nonparametric estimators, and critically interpreting the results of your analyses.

## Principles and Mechanisms

This chapter delves into the foundational principles and operational mechanisms of one-sample and paired rank tests. Moving beyond the introductory concepts, we will construct a rigorous understanding of the Sign Test and the Wilcoxon Signed-Rank Test. Our focus will be on the statistical logic that underpins these methods, the assumptions that grant them validity, and the practical procedures for their application, including the handling of common data complexities such as ties and zero values.

### A Unified Framework for One-Sample and Paired-Data Problems

At first glance, a one-sample problem and a paired-data problem appear distinct. The former involves a single set of measurements to be compared against a hypothesized population value, while the latter involves two sets of related measurements (e.g., pre- and post-intervention) to assess a change. However, non-parametric rank tests offer an elegant unification of these two scenarios by transforming them into a single, common inferential problem.

Consider a **one-sample problem** where we have [independent and identically distributed](@entry_id:169067) (i.i.d.) observations $X_1, \dots, X_n$ from a continuous distribution. Our goal is to test a hypothesis about a [location parameter](@entry_id:176482), for instance, whether the population median is equal to a specific value $\theta_0$. We can define a set of differences $d_i = X_i - \theta_0$. The original hypothesis, $H_0: \text{median}(X) = \theta_0$, is then perfectly equivalent to the hypothesis that the median of the distribution of these differences is zero, i.e., $H_0: \text{median}(D) = 0$.

Now, consider a **paired-data problem** with pairs of observations $(X_i^{\text{pre}}, X_i^{\text{post}})$ for $i = 1, \dots, n$. The objective is to test if an intervention has caused a shift in the central tendency. We compute the within-subject differences $d_i = X_i^{\text{post}} - X_i^{\text{pre}}$. The research question, "Is there a treatment effect?", is naturally framed as testing whether the median of these differences is zero: $H_0: \text{median}(D) = 0$.

In both cases, the inferential task is reduced to a one-sample test on a set of derived differences $\{d_i\}$, with the null hypothesis centered on zero [@problem_id:4933923]. This reduction allows us to develop a single set of tools applicable to both experimental designs.

To formalize this, we conceptualize the data-generating process. For a paired study, we assume that the pairs $(Y_{i,1}, Y_{i,0})$ are [independent and identically distributed](@entry_id:169067) draws from some bivariate population distribution, $G$. This setup respects the matching by allowing for arbitrary dependence *within* a pair, while ensuring independence *between* pairs. The differences $D_i = Y_{i,1} - Y_{i,0}$ are therefore also independent and identically distributed random variables, drawn from some univariate distribution $F_D$. The validity of the rank tests we will discuss rests on this foundation of i.i.d. differences [@problem_id:4933887].

### The Sign Test: Inference from Direction Alone

The **[sign test](@entry_id:170622)** is the most straightforward of the rank-based procedures. It is exceptionally robust because it discards all information about the magnitude of the differences, relying solely on their direction (i.e., their sign).

#### Core Principles and Assumptions

The [sign test](@entry_id:170622) is designed to test hypotheses about the **population median**. It does not, in general, test the population mean. This distinction is crucial, especially for skewed distributions where the mean and median diverge. The null hypothesis for the [sign test](@entry_id:170622) is $H_0: \text{median}(D) = 0$ [@problem_id:4933936].

The validity of the [sign test](@entry_id:170622) rests on minimal assumptions:
1.  The differences $D_1, \dots, D_n$ are mutually independent.
2.  The underlying distribution $F_D$ from which the differences are drawn is continuous.

The continuity assumption implies that the probability of any specific value is zero, so under $H_0$, $\mathbb{P}(D_i = 0) = 0$. By definition of the median, $H_0: \text{median}(D) = 0$ means that $\mathbb{P}(D_i \le 0) = 0.5$. Combining these, we find that under the null hypothesis, an observation is equally likely to be positive or negative: $\mathbb{P}(D_i \gt 0) = \mathbb{P}(D_i \lt 0) = 0.5$. Notably, the [sign test](@entry_id:170622) does **not** require the distribution of differences to be symmetric [@problem_id:4933923].

#### The Test Statistic and Its Null Distribution

The test statistic for the [sign test](@entry_id:170622) is simply the number of positive differences, denoted **$S^+$**.
$$S^+ = \sum_{i=1}^{n} \mathbf{1}\{D_i \gt 0\}$$
where $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167).

Under the null hypothesis, each difference $D_i$ constitutes an independent Bernoulli trial with a probability of being "successful" (i.e., positive) of $p=0.5$. Therefore, the test statistic $S^+$ follows a **Binomial distribution** with parameters $n$ and $p=0.5$.

#### Handling Zero Differences

In practical applications, observed differences of exactly zero can occur due to [measurement precision](@entry_id:271560) or rounding, despite the theoretical assumption of continuity. A value of $D_i = 0$ is neither positive nor negative and thus carries no information about the direction of change. The standard and most principled procedure is to **discard all zero differences** from the analysis before computing the test statistic [@problem_id:4933903].

This has a direct consequence: the sample size for the test is reduced. If we start with $n$ observations and find $n_0$ zeros, the **effective sample size** becomes $n^{\star} = n - n_0$. The test statistic $S^+$ is then the count of positive signs among these $n^{\star}$ non-zero observations. Its null distribution is accordingly $\text{Binomial}(n^{\star}, 0.5)$ [@problem_id:4933890].

For example, given the differences $\{1.2, -0.4, 0.0, 0.0, 2.1, -1.5, 0.0, 0.8, -0.1, 0.0, 1.0, -2.2\}$, we have $n=12$ and $n_0=4$ zeros. We discard the zeros, leaving an [effective sample size](@entry_id:271661) of $n^{\star}=8$. Among these 8 non-zero differences, there are 4 positive values ($1.2, 2.1, 0.8, 1.0$), so the observed statistic is $S^+ = 4$. The null distribution for this test is $\text{Binomial}(8, 0.5)$ [@problem_id:4933903].

#### Calculating Exact P-values

Because the null distribution of $S^+$ is a well-defined [discrete distribution](@entry_id:274643), we can calculate exact p-values. For a two-sided test, the p-value is the probability of observing a result as extreme as, or more extreme than, the observed statistic in either tail of the distribution.

The Binomial distribution with $p=0.5$ is symmetric. If our observed statistic is $S^+_{\text{obs}}$, the p-value is the sum of probabilities in the observed tail and the corresponding opposite tail. For an observed $S^+_{\text{obs}} = k$, the two-sided p-value is $P(S^+ \le k) + P(S^+ \ge n^{\star} - k)$. Due to symmetry, this simplifies to $2 \times P(S^+ \le k)$ if $k \lt n^{\star}/2$.

As an illustration [@problem_id:4933888], consider a study with 20 patients that yields 17 non-zero differences, of which $S^+ = 4$ are positive. The effective sample size is $n^{\star}=17$. The null distribution is $B(17, 0.5)$. The expected value is $17 \times 0.5 = 8.5$. Our observed value of 4 is in the lower tail. The probability of a result this extreme or more extreme in the lower tail is $P(S^+ \le 4)$. The corresponding upper tail is defined by values as far or farther from the mean, which are $S^+ \ge 17-4 = 13$.
The two-sided exact p-value is therefore:
$$ p = P(S^+ \le 4) + P(S^+ \ge 13) = \sum_{k=0}^{4} \binom{17}{k}(0.5)^{17} + \sum_{k=13}^{17} \binom{17}{k}(0.5)^{17} $$
Due to symmetry, this is equal to $2 \times P(S^+ \le 4)$.
$$ p = 2 \times (0.5)^{17} \sum_{k=0}^{4} \binom{17}{k} = 2 \times (0.5)^{17} \left(\binom{17}{0} + \binom{17}{1} + \binom{17}{2} + \binom{17}{3} + \binom{17}{4}\right) $$
$$ p = 2 \times \frac{1+17+136+680+2380}{2^{17}} = \frac{2 \times 3214}{131072} \approx 0.04904 $$

### The Wilcoxon Signed-Rank Test: Incorporating Magnitudes

While the [sign test](@entry_id:170622) is robust, it can be inefficient as it ignores the magnitudes of the differences. A difference of $+100$ is treated the same as a difference of $+0.1$. The **Wilcoxon Signed-Rank (WSR) test** provides a more powerful alternative by incorporating information about the relative magnitudes of the differences via ranks.

#### Core Principles and Assumptions

The WSR test is based on a stronger set of assumptions than the [sign test](@entry_id:170622). In addition to **independence** and **continuity** of the differences $D_i$, the WSR test requires that, under the null hypothesis, the distribution of differences $F_D$ is **symmetric about 0** [@problem_id:4933887].

This symmetry assumption is the key to the test's construction. It implies not only that the median is 0, but that the entire probability distribution is a mirror image around 0. A crucial consequence is that the sign of a difference is independent of its absolute value. In other words, under $H_0$, a large difference is just as likely to be positive as it is to be negative.

When the symmetry assumption holds, the null hypothesis implies that the mean (if it exists) and median are both zero. More generally, the WSR test is associated with a [location parameter](@entry_id:176482) known as the **Hodges-Lehmann pseudo-median**, defined as $\text{median}((D_i + D_j)/2)$ for all pairs $(i, j)$. Under symmetry, the pseudo-median, median, and mean coincide [@problem_id:4933936].

#### The Permutation Rationale and Exact Null Distribution

The theoretical foundation of the WSR test is a permutation argument. We condition on the observed set of absolute differences, $\{|d_1|, \dots, |d_{n'}|\}$ (after removing $n_0$ zeros for an [effective sample size](@entry_id:271661) of $n'$). This also fixes their ranks, $\{1, \dots, n'\}$.

Under the null hypothesis of symmetry about 0, the sign ($+$ or $-$) attached to each of these ranks is an independent random outcome with probability $0.5$. There are $2^{n'}$ possible ways to assign signs to the $n'$ ranks, and under $H_0$, each of these assignments is equally likely. The exact null distribution of any [test statistic](@entry_id:167372) based on these signed ranks can be found by enumerating the statistic's value across all $2^{n'}$ equally probable outcomes [@problem_id:4933878]. This is the principle that makes the WSR test an exact, distribution-free procedure.

#### The Test Statistic and its Null Distribution

The WSR [test statistic](@entry_id:167372), **$W^+$**, is defined as the sum of the ranks corresponding to the *positive* differences. The procedure is as follows:
1.  Compute the differences $d_i = y_i - x_i$.
2.  Discard any pairs where $d_i = 0$. Let the [effective sample size](@entry_id:271661) be $n'$.
3.  Take the absolute value of the non-zero differences, $|d_i|$.
4.  Assign ranks to these $n'$ absolute values, from 1 (smallest) to $n'$ (largest).
5.  Calculate $W^+$ by summing the ranks of the differences that were originally positive.

Under the null hypothesis, the [expectation and variance](@entry_id:199481) of $W^+$ are given by:
$$ E[W^+] = \frac{n'(n'+1)}{4} $$
$$ \text{Var}(W^+) = \frac{n'(n'+1)(2n'+1)}{24} $$

#### Handling Ties in Magnitudes

The continuity assumption theoretically precludes ties in the absolute magnitudes, $|d_i|$. In practice, however, ties are common. The standard procedure is to assign the **average rank** (or **mid-rank**) to each member of a tied group. For example, if three observations are tied for what would have been ranks 5, 6, and 7, each is assigned the rank $(5+6+7)/3 = 6$.

The presence of ties does not affect the expectation of $W^+$, but it *reduces* the variance. The sum of squared ranks is smaller when average ranks are used compared to a set of distinct integer ranks. The variance formula must be corrected for ties as follows [@problem_id:4933899]:
$$ \text{Var}(W^+) = \frac{n'(n'+1)(2n'+1)}{24} - \frac{\sum_{j=1}^{g} (t_j^3 - t_j)}{48} $$
Here, $g$ is the number of tied groups, and $t_j$ is the number of observations in the $j$-th tied group.

#### A Comprehensive Example

Let's apply the full WSR procedure to a dataset from a clinical study [@problem_id:4933891]. The paired differences are $d = \{ -4, 3, 0, 5, -2, -5, 2, 4, 0, -3, 1, -1 \}$.

1.  **Handle Zeros**: There are 2 zero differences. We discard them. The [effective sample size](@entry_id:271661) is $n' = 12 - 2 = 10$.

2.  **Rank Absolute Magnitudes with Ties**: The non-zero absolute differences are $\{4, 3, 5, 2, 5, 2, 4, 3, 1, 1\}$.
    -   Sorted absolute values: $\{1, 1, 2, 2, 3, 3, 4, 4, 5, 5\}$.
    -   Ranks 1, 2 are tied at value 1: average rank is $(1+2)/2 = 1.5$.
    -   Ranks 3, 4 are tied at value 2: average rank is $(3+4)/2 = 3.5$.
    -   Ranks 5, 6 are tied at value 3: average rank is $(5+6)/2 = 5.5$.
    -   Ranks 7, 8 are tied at value 4: average rank is $(7+8)/2 = 7.5$.
    -   Ranks 9, 10 are tied at value 5: average rank is $(9+10)/2 = 9.5$.

3.  **Calculate $W^+$**: The original positive differences were $\{3, 5, 2, 4, 1\}$. We sum their corresponding ranks:
    $$ W^+ = \text{rank}(|3|) + \text{rank}(|5|) + \text{rank}(|2|) + \text{rank}(|4|) + \text{rank}(|1|) $$
    $$ W^+ = 5.5 + 9.5 + 3.5 + 7.5 + 1.5 = 27.5 $$

4.  **Calculate Null Expectation and Tie-Corrected Variance**:
    $$ E[W^+] = \frac{10(10+1)}{4} = 27.5 $$
    For the variance, we have 5 tied groups, each of size $t_j = 2$.
    $$ \text{Var}(W^+) = \frac{10(11)(21)}{24} - \frac{5 \times (2^3 - 2)}{48} = 96.25 - \frac{5 \times 6}{48} = 96.25 - 0.625 = 95.625 $$

5.  **Hypothesis Test**: The observed statistic $W^+ = 27.5$ is exactly equal to its null expectation. This provides the least possible evidence against the null hypothesis, and the p-value is 1.0. We would fail to reject $H_0$. For larger samples where the statistic is not exactly at the mean, a **[normal approximation](@entry_id:261668)** with [continuity correction](@entry_id:263775) is often used to calculate a Z-score and p-value:
    $$ Z = \frac{W^+ - E[W^+]}{\sqrt{\text{Var}(W^+)}} $$

### The Invariance Principle of Rank Tests

A defining feature of rank-based tests is their **invariance** to certain types of data transformations. This property makes them robust and explains why they are considered "scale-free."

The key principle is that ranks depend only on the relative ordering of values, not on their specific magnitudes. Any **strictly increasing [monotonic function](@entry_id:140815)** applied to a set of values will preserve their order, and therefore leave their ranks unchanged [@problem_id:4933876].

For the WSR test, the statistic $W^+$ is a function of the signs of the differences and the ranks of their absolute magnitudes. If we apply any strictly increasing function $\phi$ to the absolute magnitudes $M_i = |d_i|$, the new values $\phi(M_i)$ will have the exact same ranks as the original $M_i$. The signs are also unaffected. Consequently, the test statistic $W^+$ and its p-value remain identical. A simple example of such a transformation is scaling by a positive constant, $\phi(x) = c \cdot x$ for $c \gt 0$. This demonstrates that the WSR test result is not affected by a change in the units of measurement (e.g., from mg/dL to g/L), a property known as **[scale-invariance](@entry_id:160225)** [@problem_id:4933876].

The [sign test](@entry_id:170622) exhibits a different kind of invariance. It is invariant under any strictly increasing transformation $\psi$ applied to the differences $D_i$ if and only if that transformation preserves the point zero, i.e., $\psi(0)=0$. This ensures that $\text{sign}(\psi(D_i)) = \text{sign}(D_i)$. If $\psi(0) \neq 0$, the signs can change, and the test is not invariant [@problem_id:4933876].

It is important to note that this invariance does not typically extend to arbitrary transformations of the raw data in a paired analysis. Applying a non-linear strictly increasing function $g$ to the pre- and post-measurements, forming new differences $d'_i = g(Y_i) - g(X_i)$, will generally change the ordering of the absolute differences, altering the ranks and the WSR test result [@problem_id:4933876]. This underscores that the assumptions and properties of these tests apply specifically to the distribution of the differences themselves.