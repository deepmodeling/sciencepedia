## Introduction
In experimental research, particularly in fields like biostatistics and psychology, it is common to measure a single subject under multiple conditions or over several time points. This repeated-measures design is powerful because it controls for the inherent variability between subjects, making it easier to detect true treatment effects. However, a significant challenge arises when the collected data do not meet the strict assumptions, such as normality, required by traditional parametric tests like the repeated-measures Analysis of Variance (ANOVA). This knowledge gap necessitates a robust, assumption-free method for analyzing such dependent data.

This article introduces the Friedman test, a cornerstone of [non-parametric statistics](@entry_id:174843) designed specifically for this purpose. We will explore how this [rank-based test](@entry_id:178051) provides a powerful alternative to ANOVA for randomized complete block designs. The following chapters will guide you from theory to practice. In "Principles and Mechanisms," we will dissect the test's core logic, including its ranking procedure and statistical underpinnings. "Applications and Interdisciplinary Connections" will demonstrate how to apply the test in real-world scenarios, interpret its results, and situate it among other statistical methods. Finally, "Hands-On Practices" will solidify your understanding through guided computational exercises.

## Principles and Mechanisms

The Friedman test is a non-parametric statistical test developed by the economist Milton Friedman. It is designed to detect differences between several related treatments or conditions. Conceptually, it is an extension of the [sign test](@entry_id:170622) or the Wilcoxon signed-[rank test](@entry_id:163928) to more than two conditions, and it serves as a non-parametric alternative to the one-way repeated measures [analysis of variance](@entry_id:178748) (ANOVA). The power of the Friedman test lies in its ability to analyze data from a **randomized complete block design** without making strong distributional assumptions, such as normality.

### The Logic of Blocking and Repeated Measures

In many experimental settings, particularly in biostatistics and medicine, we aim to compare the effects of $k$ different treatments. A significant source of variability that can obscure true treatment effects is the inherent heterogeneity between experimental subjects. For example, in a clinical trial, patients may have different baseline health, genetic predispositions, or lifestyle factors. A **completely randomized design**, where subjects are randomly assigned to one of the $k$ treatment groups, must rely on randomization to balance these subject-specific characteristics on average. However, the residual between-subject variability can be large, potentially reducing the statistical power to detect treatment differences.

An elegant solution to this problem is the **randomized complete block design**. In this design, subjects are grouped into homogeneous **blocks**, and within each block, all $k$ treatments are administered. The most common and powerful form of blocking is to use each subject as their own block. This is known as a **repeated-measures design**. Each of the $n$ subjects receives all $k$ treatments, often in a randomized order to prevent time- or order-based confounding. By comparing the treatments *within* each subject, we effectively use each subject as their own control. This design isolates and removes the between-subject variability from the analysis, allowing for a more sensitive comparison of the treatments. [@problem_id:4946243]

To formalize this, we can consider a simple additive model for the response $Y_{ij}$ of subject $i$ to treatment $j$:

$Y_{ij} = \mu + b_i + \tau_j + \varepsilon_{ij}$

Here, $\mu$ represents a grand mean, $b_i$ is a subject-specific effect representing the baseline for subject $i$, $\tau_j$ is the effect of treatment $j$, and $\varepsilon_{ij}$ is the random error. The primary goal is to test the null hypothesis that all treatment effects are equal (i.e., $H_0: \tau_1 = \tau_2 = \dots = \tau_k$). The block effects, $b_i$, are considered **[nuisance parameters](@entry_id:171802)**—sources of variability that we want to control for but are not of primary interest. The Friedman test provides a method to test for treatment effects that is robust to the values of these unknown block effects.

It is crucial to distinguish this structure from that of independent groups. If we had $k$ separate groups of subjects, each receiving a single treatment, the appropriate non-parametric test would be the Kruskal-Wallis test. The Friedman test is specifically designed for dependent samples, where measurements are linked by a blocking factor, such as the same subject being measured multiple times. [@problem_id:4797204]

### The Ranking Procedure: The Core Mechanism

The Friedman test ingeniously controls for the block effects by transforming the data. Instead of analyzing the raw response values $Y_{ij}$, the test operates on their **ranks**. The core mechanism is to rank the $k$ treatment responses *within each block* from $1$ (smallest) to $k$ (largest). Let $r_{ij}$ denote the rank of treatment $j$ within block $i$.

Consider the additive model again: $Y_{ij} = b_i + \tau_j + \varepsilon_{ij}$ (ignoring the constant $\mu$). For a given subject $i$, the term $b_i$ is a constant added to all $k$ observations. Since adding a constant to a set of values does not change their relative order, the ranks $r_{ij}$ are completely unaffected by the subject-specific effect $b_i$. The ranking procedure effectively purges the analysis of this between-subject heterogeneity. [@problem_id:4946243]

More generally, the ranks are invariant to any strictly increasing monotonic transformation applied to the data within a block. This means the test is robust not only to additive subject effects but also to multiplicative or other non-linear subject-specific distortions of the response scale. [@problem_id:4946243]

#### Ranking Without Ties

Let's illustrate with an example. A nutrition researcher conducts a crossover study where $n=6$ patients each try $k=4$ diets. A lower glycemic variability score indicates better control. The raw scores for three of the subjects are recorded: [@problem_id:4946292]

| Subject | Diet A | Diet B | Diet C | Diet D |
|---|---|---|---|---|
| $1$ | $12$ | $10$ | $5$ | $7$ |
| $2$ | $8$ | $14$ | $6$ | $11$ |
| $3$ | $13$ | $9$ | $4$ | $6$ |

For Subject 1, the scores are $(12, 10, 5, 7)$. Ranking from lowest to highest gives: C ($5$) gets rank 1, D ($7$) gets rank 2, B ($10$) gets rank 3, and A ($12$) gets rank 4. The ranks are $(4, 3, 1, 2)$.

For Subject 2, the scores are $(8, 14, 6, 11)$. The ranks are: C ($6$) gets rank 1, A ($8$) gets rank 2, D ($11$) gets rank 3, and B ($14$) gets rank 4. The ranks are $(2, 4, 1, 3)$.

This process is repeated for all $n$ subjects, creating a new table of ranks.

#### Handling Tied Observations

In practice, it is possible for two or more treatments to yield the exact same response value within a block. These are called **ties**. The standard procedure for handling ties is to assign each tied observation the average of the ranks they would have occupied. This is known as the **midrank**.

For instance, suppose for a subject in a $k=4$ experiment, the responses for treatments A, B, C, and D are $(7.1, 6.8, 7.1, 5.9)$. [@problem_id:4946272]
1.  Order the responses: $5.9, 6.8, 7.1, 7.1$.
2.  The response $5.9$ (Treatment D) is the smallest and receives rank $1$.
3.  The response $6.8$ (Treatment B) is second and receives rank $2$.
4.  The responses for A and C are tied. They would have occupied ranks $3$ and $4$.
5.  The midrank is the average of these ranks: $\frac{3+4}{2} = 3.5$.
6.  Both Treatment A and Treatment C are assigned the rank $3.5$.

The vector of ranks for this subject is $(3.5, 2.0, 3.5, 1.0)$. Notice that the sum of ranks within the block remains $1+2+3.5+3.5 = 10$, which is the same as the sum of ranks in a no-tie case ($1+2+3+4=10$). This property of midranks is crucial.

### Hypotheses and Core Assumptions

Before applying the test, it is essential to understand its formal hypotheses and the assumptions that underpin its validity.

#### Null and Alternative Hypotheses

The Friedman test evaluates the following hypotheses:
-   **Null Hypothesis ($H_0$)**: Within each block, the probability distributions of the responses for the $k$ treatments are identical.
-   **Alternative Hypothesis ($H_1$)**: At least one of the treatment distributions differs from the others.

The test is fundamentally about distributional equality. [@problem_id:4946270] A common misconception is that the Friedman test is solely a test of medians. While a difference in medians (a location shift) is a primary type of alternative that the test has high power to detect, it is not the only one. Since the test is based on ranks, any systematic difference in distributions that consistently affects the rank ordering of treatments within subjects can lead to a rejection of $H_0$. For example, the test can detect differences in [skewness](@entry_id:178163) even if medians are equal. Conversely, the test has low power to detect some distributional differences, such as a difference in spread (variance) for symmetric distributions with a common median. [@problem_id:4946304]

Therefore, a statistically significant result from a Friedman test should be interpreted as evidence of a **distributional difference** among treatments, not necessarily just a difference in medians. [@problem_id:4946304]

#### Core Assumptions

The validity of the Friedman test rests on a minimal set of assumptions: [@problem_id:4946264]
1.  **Independent Blocks**: The subjects (or blocks) are a random sample from the population of interest. The observations and rank orderings in one block are statistically independent of those in another.
2.  **Exchangeability within Blocks under $H_0$**: The null hypothesis implies that if there is no treatment effect, the treatment labels assigned to the set of $k$ observations within a block are arbitrary. Any permutation of the labels is equally likely. This is the theoretical basis for the test's null distribution.
3.  **No Treatment-by-Block Interaction**: The test assumes that while the block effect ($b_i$) can vary, the treatment effect ($\tau_j$) is consistent across blocks. For instance, it assumes that if Treatment A is better than Treatment B, it is consistently better for all subjects, even if the magnitude of the difference varies. A [strong interaction](@entry_id:158112) (e.g., Treatment A is best for half the subjects, while Treatment B is best for the other half) can violate this assumption and reduce the test's power.
4.  **Ordinal or Continuous Data**: The outcome variable must be at least ordinal, so that a meaningful ranking can be performed within each block.

The test notably does *not* assume that the data are drawn from a normal distribution or that variances are equal across treatments (homoscedasticity), which are requirements for its parametric counterpart, the repeated measures ANOVA.

### The Friedman Test Statistic

The intuition behind the test statistic is straightforward. First, we compute the ranks $r_{ij}$ for each observation. Then, we sum the ranks for each treatment across all $n$ blocks to get the treatment rank sums:

$R_j = \sum_{i=1}^n r_{ij}$

If the null hypothesis is true, we expect the treatments to receive a similar mix of high and low ranks. Consequently, the rank sums $R_j$ for each treatment should be roughly equal. The Friedman statistic, denoted $\chi^2_F$, quantifies the extent to which the observed rank sums deviate from this expectation.

Under $H_0$, the expected rank for any observation is the average of the possible ranks, $\frac{k+1}{2}$. Thus, the expected rank sum for any treatment is:

$E[R_j] = n \times \frac{k+1}{2}$

The [test statistic](@entry_id:167372) measures the squared deviation of each $R_j$ from its expected value, sums these deviations, and scales the result. The most intuitive form of the statistic is: [@problem_id:4946245]

$\chi^2_F = \frac{12}{nk(k+1)} \sum_{j=1}^k \left(R_j - \frac{n(k+1)}{2}\right)^2$

An algebraically equivalent and more common computational formula (for the no-tie case) is: [@problem_id:4946245]

$\chi^2_F = \frac{12}{nk(k+1)} \sum_{j=1}^k R_j^2 - 3n(k+1)$

The term $\sum R_j^2$ captures the variability between the treatment rank sums. The scaling constant $\frac{12}{nk(k+1)}$ and the subtraction term $-3n(k+1)$ work together to standardize the statistic. They ensure that, under the null hypothesis, the expected value of $\chi^2_F$ is $k-1$, which matches the degrees of freedom of its reference distribution. [@problem_id:4946245]

#### Tie Correction

When ties are present within blocks, the variability of the ranks is reduced. This causes the uncorrected Friedman statistic to be slightly smaller than it should be, making the test conservative (i.e., less likely to find a significant result). A correction factor can be applied to account for this. While the formula for the tie-corrected statistic is complex, conceptually it adjusts the denominator of the statistic to reflect the reduced total variance caused by the ties. For most practical purposes, if the number of ties is small, the uncorrected statistic provides a reasonable approximation.

### The Null Distribution and Statistical Decision

Once the [test statistic](@entry_id:167372) $\chi^2_F$ is calculated, we must compare it to its null distribution to obtain a p-value and make a decision.

#### Large-Sample Chi-Square Approximation

For moderately large sample sizes (e.g., when $n$ or $k$ is large enough), the Friedman statistic $\chi^2_F$ can be shown to approximately follow a **chi-square ($\chi^2$) distribution with $k-1$ degrees of freedom**. The degrees of freedom are $k-1$ because there are $k$ rank sums ($R_j$), but they are not fully independent; they must sum to a fixed total, $n \frac{k(k+1)}{2}$, which imposes one constraint.

To make a statistical decision, we compare the calculated $\chi^2_F$ value to the critical value from the $\chi^2_{k-1}$ distribution at a chosen [significance level](@entry_id:170793) $\alpha$ (e.g., $\alpha = 0.05$). If our calculated statistic exceeds the critical value, we reject the null hypothesis. Equivalently, we calculate the p-value, which is the probability $P(\chi^2_{k-1} \ge \chi^2_F)$. If the p-value is less than $\alpha$, we reject $H_0$.

For example, in the nutrition study with $n=6$ subjects and $k=4$ diets, suppose the rank sums are $R_A=22$, $R_B=17$, $R_C=9$, and $R_D=12$. The Friedman statistic is calculated as $\chi^2_F = 9.80$. We compare this to a $\chi^2$ distribution with $df = k-1 = 3$ degrees of freedom. The p-value is $P(\chi^2_3 \ge 9.80) \approx 0.020$. Since this is less than $0.05$, we reject $H_0$ and conclude that there is a statistically significant difference in the glycemic variability distributions among the four diets. [@problem_id:4946292]

#### The Exact Permutation Distribution

When sample sizes are small (e.g., $n \le 10$ and $k \le 5$), the chi-square approximation may not be accurate. In these cases, it is possible to calculate the **exact null distribution** of the Friedman statistic. This method relies on the permutation principle. [@problem_id:4946282]

Under $H_0$, any of the $k!$ permutations of ranks within a block is equally likely. Since there are $n$ independent blocks, the total number of possible rank-assignment arrays for the entire experiment is $(k!)^n$. For example, with $n=3$ subjects and $k=3$ treatments, there are $(3!)^3 = 6^3 = 216$ equally likely rank configurations. [@problem_id:4946282]

To find the exact distribution, one would (in principle):
1.  Enumerate all $(k!)^n$ possible rank configurations.
2.  Calculate the value of the Friedman statistic, $\chi^2_F$, for each configuration.
3.  The collection of these statistic values forms the exact null distribution.

The exact p-value is then the proportion of these statistic values that are greater than or equal to the statistic calculated from the observed data. Modern statistical software can perform these exact calculations when sample sizes are small enough to make enumeration computationally feasible.