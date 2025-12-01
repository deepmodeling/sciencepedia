## Introduction
In many scientific disciplines, raw quantitative data, while complete, is often too voluminous and complex to yield immediate insight. A list of thousands of blood pressure readings or gene expression values is just a sea of numbers without structure or meaning. The fundamental challenge, and the first step in any data analysis, is to distill this raw information into a few concise, interpretable, and meaningful summaries. This process of summarization allows us to grasp the essential features of our data, compare different groups, and communicate findings effectively. However, choosing and interpreting these summaries is a nuanced task; a poorly chosen statistic can be as misleading as no summary at all.

This article provides a comprehensive guide to summarizing quantitative data, bridging theoretical principles with practical applications. It is designed to equip you with the knowledge to not only calculate [summary statistics](@entry_id:196779) but to understand their properties, limitations, and appropriate use in scientific inquiry.

Across three chapters, you will build a robust understanding of data summarization. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, introducing core concepts like the [empirical distribution function](@entry_id:178599), the [plug-in principle](@entry_id:276689), and the mathematical properties of measures of center, spread, and association. It will also address the critical concepts of robustness and the effect of data transformations. The second chapter, **"Applications and Interdisciplinary Connections,"** moves from theory to practice, showcasing how these summaries are used to solve real-world problems in clinical trials, epidemiology, and diagnostics, from standardizing treatment effects to detecting drug safety signals. Finally, **"Hands-On Practices"** offers targeted problems that allow you to apply these concepts, solidifying your understanding of how to handle common challenges like skewed data and outliers.

## Principles and Mechanisms

The primary objective of quantitative data summarization is to distill the essential features of a dataset into a set of interpretable numerical and graphical forms. While a raw dataset contains all available information, it is often too voluminous to yield immediate insight. The goal of a summary is to capture key aspects of the data's underlying probability distribution—such as its central tendency, dispersion, and shape—without loss of critical information. This chapter outlines the fundamental principles and mechanisms by which we construct, interpret, and critically evaluate these summaries.

### The Empirical Distribution Function: A Complete Nonparametric Summary

The most fundamental summary of a quantitative sample, $X_1, \dots, X_n$, is the **Empirical Cumulative Distribution Function (ECDF)**. The ECDF, denoted $\hat F_n(x)$, is a function that, for any value $x$, reports the proportion of sample observations less than or equal to $x$.

Formally, the ECDF is defined as:
$$
\hat F_n(x) = \frac{1}{n} \sum_{i=1}^n \mathbf{1}\{X_i \le x\}
$$
where $\mathbf{1}\{A\}$ is the [indicator function](@entry_id:154167), which equals $1$ if the condition $A$ is true and $0$ otherwise [@problem_id:4955565].

The ECDF has several key properties. It is a [step function](@entry_id:158924) that is non-decreasing and right-continuous, with its value jumping by at least $1/n$ at each unique observed data point. It ranges from $0$ for values of $x$ smaller than the sample minimum to $1$ for values of $x$ greater than or equal to the sample maximum.

The power of the ECDF lies in its role as a **nonparametric summary**. It makes no assumptions about the underlying distribution from which the data were sampled. Remarkably, the Glivenko-Cantelli theorem guarantees that as the sample size $n$ increases, the ECDF $\hat F_n(x)$ converges to the true population [cumulative distribution function](@entry_id:143135) (CDF), $F(x)$. In this sense, the ECDF is a complete summary of the data, and as we will see, nearly all other numerical summaries can be viewed as specific features derived from it.

### Statistical Functionals and the Plug-in Principle

A powerful way to formalize the process of data summarization is through the concept of a **statistical functional**. A statistical functional, $T(F)$, is any mapping from a distribution (represented by its CDF, $F$) to a real-valued summary of that distribution. For example, the [population mean](@entry_id:175446) is a functional of $F$, as is the population median or variance.

The **[plug-in principle](@entry_id:276689)** provides a systematic method for estimating a functional $T(F)$ from a sample. It states that we can obtain an estimator for $T(F)$ by applying the functional to the [empirical distribution function](@entry_id:178599) $\hat F_n$. This estimator is called the plug-in estimator, $T(\hat F_n)$ [@problem_id:4955540]. This principle unifies the derivation of many common [sample statistics](@entry_id:203951), grounding them in their population-level definitions.

### Measures of Central Tendency

Measures of central tendency aim to identify a "typical" or "central" value of the distribution.

#### The Mean

The [population mean](@entry_id:175446), or expected value, is defined by the functional $T(F) = \mathbb{E}_F[X] = \int x \, dF(x)$. Applying the [plug-in principle](@entry_id:276689), we replace the distribution $F$ with the [empirical distribution](@entry_id:267085) $\hat F_n$, which places a probability mass of $1/n$ on each observation $X_i$. The integral becomes a sum:
$$
T(\hat F_n) = \int x \, d\hat F_n(x) = \sum_{i=1}^n X_i \left(\frac{1}{n}\right) = \frac{1}{n} \sum_{i=1}^n X_i = \bar{X}
$$
Thus, the familiar sample mean, $\bar{X}$, is the plug-in estimator of the [population mean](@entry_id:175446) functional [@problem_id:4955540].

#### Quantiles and the Median

Quantiles are values that partition the distribution into continuous intervals with equal probabilities. The $p$-th population quantile is the value $x_p$ such that $F(x_p) = p$. Because a CDF may be discontinuous or have flat regions, a more rigorous definition is required. The quantile functional is the [generalized inverse](@entry_id:749785) of the CDF:
$$
Q_p(F) = \inf\{x : F(x) \ge p\}
$$
This gives the smallest value $x$ for which the cumulative probability is at least $p$ [@problem_id:4955552].

The plug-in estimator for the $p$-th quantile is obtained by applying this functional to the ECDF:
$$
\hat{Q}_n(p) = \inf\{x : \hat F_n(x) \ge p\}
$$
This is the smallest observed value $X_i$ for which the proportion of data at or below it is at least $p$. For example, consider a sorted sample of $n=12$ values where the ECDF first exceeds $0.25$ at the data point $2.3$. The sample $25$-th percentile, $\hat{Q}_{12}(0.25)$, would be $2.3$ [@problem_id:4955552].

The **median** is a special case of a quantile, corresponding to $p=0.5$. The median functional is $T(F) = Q_{0.5}(F)$, and its plug-in estimator is the [sample median](@entry_id:267994) [@problem_id:4955540].

### Measures of Dispersion

Measures of dispersion, or spread, quantify the variability of the data around the center.

#### Variance and Standard Deviation

The population variance is the [second central moment](@entry_id:200758), defined by the functional $T(F) = \mathbb{E}_F[(X-\mu_F)^2] = \int (x - \mu_F)^2 \, dF(x)$, where $\mu_F$ is the population mean. Applying the [plug-in principle](@entry_id:276689) requires replacing both $F$ and $\mu_F$ with their empirical counterparts, $\hat F_n$ and $\mu_{\hat F_n} = \bar{X}$. This yields:
$$
T(\hat F_n) = \int (x - \bar{X})^2 \, d\hat F_n(x) = \frac{1}{n} \sum_{i=1}^n (X_i - \bar{X})^2
$$
This is the **biased [sample variance](@entry_id:164454)**. Note that the commonly used **unbiased sample variance**, $S^2 = \frac{1}{n-1}\sum(X_i - \bar{X})^2$, which includes Bessel's correction, is not the direct plug-in estimator but is a modification designed to have the property that $\mathbb{E}[S^2] = \operatorname{Var}(X)$ [@problem_id:4955540]. The **standard deviation**, $\sigma$, is simply the square root of the variance.

#### Interquartile Range (IQR)

The **Interquartile Range (IQR)** is defined as the difference between the $75$-th and $25$-th quantiles: $T(F) = Q_{0.75}(F) - Q_{0.25}(F)$. Its plug-in estimator, the sample IQR, is the difference between the sample $75$-th and $25$-th [percentiles](@entry_id:271763) [@problem_id:4955540]. The IQR measures the spread of the middle $50\%$ of the data.

### Robustness: The Impact of Outliers

A critical property of any statistical summary is its **robustness**, which refers to its resistance to being disproportionately affected by a small number of extreme observations (outliers).

Summaries based on moments, such as the mean and variance, are **not robust**. A single extreme outlier can pull the sample mean to an arbitrarily large or small value. Since the variance is computed from squared deviations from the mean, it is even more sensitive to outliers. In contrast, summaries based on ranks or [order statistics](@entry_id:266649), such as the median and the IQR, are **robust**. For example, in a dataset with an outlier like $\{3.5, 4.0, 4.0, 4.1, 4.1, 4.2, 4.3, 20.0\}$, the sample mean is pulled to $6.025$, far from the bulk of the data. The [sample median](@entry_id:267994), however, remains at $4.1$, providing a more representative summary of the central tendency of the majority of the data. Similarly, the sample IQR of $0.2$ is unaffected by the outlier [@problem_id:4955540].

### Properties of Summaries under Data Transformation

In biostatistics, data are often transformed, for instance by taking a logarithm or by changing units of measurement. Understanding how summaries behave under these transformations is crucial for correct interpretation.

#### Affine Transformations

An affine transformation is of the form $Y = aX + b$, where $a$ represents a change in scale (e.g., converting milligrams to grams) and $b$ represents a shift in location or origin. The properties of summaries under such transformations are described by their **[equivariance](@entry_id:636671)** (transforming in the same way as the data) and **invariance** (remaining unchanged).

-   **Mean**: The mean is both **location equivariant** and **scale equivariant**. That is, $\mathbb{E}[aX+b] = a\mathbb{E}[X] + b$.
-   **Variance**: The variance is **location invariant** but **scale equivariant** with a factor of $a^2$. That is, $\operatorname{Var}(aX+b) = a^2 \operatorname{Var}(X)$. Adding a constant shifts the entire distribution but does not change its spread.
-   **Standard Deviation**: The standard deviation is also **location invariant** and is **scale equivariant**: $\sigma(aX+b) = |a|\sigma(X)$.
-   **Coefficient of Variation (CV)**: For strictly positive data, the CV is defined as $\sigma/\mu$. It is a measure of relative dispersion. The CV is **scale invariant** ($\operatorname{CV}(aX) = \operatorname{CV}(X)$ for $a > 0$) but not location invariant. Its [scale invariance](@entry_id:143212) makes it useful for comparing the variability of datasets with different units or magnitudes [@problem_id:4955515].

#### Monotone Transformations

Non-linear but monotone transformations (e.g., $Y = \log(X)$) are common for analyzing skewed data.

-   **Quantiles**: Quantiles (and thus the median) are **equivariant** under monotone transformations. If $g$ is a strictly increasing function, the $p$-th quantile of $Y=g(X)$ is simply $g$ applied to the $p$-th quantile of $X$: $Q_Y(p) = g(Q_X(p))$. If $g$ is strictly decreasing, the relationship flips the probability: $Q_Y(p) = g(Q_X(1-p))$ [@problem_id:4955544].
-   **Mean and Variance**: In contrast to quantiles, the mean is **not** equivariant under [non-linear transformations](@entry_id:636115). In general, $\mathbb{E}[g(X)] \neq g(\mathbb{E}[X])$. This is a consequence of Jensen's inequality. For example, if we log-transform a right-skewed biomarker, the mean of the logs, back-transformed to the original scale, gives the **geometric mean**, $\exp(\mathbb{E}[\log X])$. This is generally not equal to (and is less than) the [arithmetic mean](@entry_id:165355), $\mathbb{E}[X]$. This distinction is critical for interpretation: the mean of the transformed data does not correspond to the transformed mean of the original data [@problem_id:4955544]. Similarly, there is no simple algebraic relationship between $\operatorname{Var}(g(X))$ and $\operatorname{Var}(X)$ for non-linear $g$.

### Graphical Summaries

Graphical summaries provide an intuitive, visual representation of the distribution.

#### Histograms

A [histogram](@entry_id:178776) groups data into bins and plots the frequency or proportion of data in each bin as a bar. While intuitive, it is formally a **piecewise-constant density estimator**. To be a valid probability density estimate, the height of each bar must be the proportion of data in that bin divided by the bin width, $h$. The estimator for the density $f(x)$ is:
$$
\hat f(x) = \frac{1}{nh} \sum_{i=1}^n \mathbf{1}\{X_i \in \text{bin}(x)\}
$$
This normalization ensures that the total area under the [histogram](@entry_id:178776) is $1$ [@problem_id:4955528].

A [histogram](@entry_id:178776) is considered a "coarse" summary because its appearance depends heavily on two arbitrary user choices: the bin width $h$ and the bin origin (the starting point of the first bin). A wider $h$ leads to a smoother but more biased estimate (oversmoothing), while a narrower $h$ leads to a less biased but more variable estimate (undersmoothing) [@problem_id:4955528].

#### Boxplots

A **Tukey boxplot** is a concise graphical summary based on robust statistics. It displays five key numbers:
1.  **Median ($Q_2$)**: A line inside the box.
2.  **The Box**: Extends from the first quartile ($Q_1$, the $25$-th percentile) to the third quartile ($Q_3$, the $75$-th percentile). The length of the box is the IQR.
3.  **Whiskers**: Lines extending from the box to the smallest and largest observed values that are not considered outliers. A common rule sets the whisker boundaries at $Q_1 - 1.5 \times \text{IQR}$ and $Q_3 + 1.5 \times \text{IQR}$.
4.  **Outliers**: Any data points that fall beyond the whiskers are plotted individually [@problem_id:4955534].

The boxplot provides a quick visual assessment of the data's center (median), spread (IQR), skewness (asymmetry of the box and whiskers around the median), and presence of potential outliers.

#### Quantile-Quantile (Q-Q) Plots

A **Q-Q plot** is a powerful graphical tool for comparing the distribution of a sample to a theoretical reference distribution (e.g., a normal distribution). It is constructed by plotting the theoretical [quantiles](@entry_id:178417) from the reference distribution against the corresponding [sample quantiles](@entry_id:276360) (the ordered data points, $X_{(i)}$). If the sample data are drawn from the reference distribution, the points on the Q-Q plot will lie approximately on a straight line [@problem_id:4955563].

Systematic deviations from this line are highly informative:
-   An **S-shaped curve** indicates a mismatch in tail weight. If the points are below the line in the left tail and above the line in the right tail, the sample distribution has **heavier tails** than the reference distribution [@problem_id:4955563].
-   A **concave or convex curve** indicates a skewness mismatch.
-   A straight line with a **slope** different from $1$ indicates that the sample has a different scale (dispersion) than the reference distribution.

### Summarizing Bivariate Association

When summarizing the relationship between two quantitative variables, correlation coefficients are commonly used.

-   **Pearson's product-moment correlation ($r$)** measures the strength and direction of a **linear** relationship. It is calculated from the raw data values and is highly sensitive to outliers. It is not suitable for capturing non-linear relationships.
-   **Spearman's [rank correlation](@entry_id:175511) ($\rho$)** and **Kendall's [rank correlation](@entry_id:175511) ($\tau$)** are robust, nonparametric alternatives. They are computed on the ranks of the data, not their actual values. Consequently, they measure the strength of **monotonic** (consistently increasing or decreasing) relationships, whether linear or not. Because they depend only on ordering, they are highly resistant to outliers and are invariant to any strictly monotone transformation of the variables. They are the preferred measures of association when the relationship is nonlinear but monotonic, or when the data contain outliers or come from [heavy-tailed distributions](@entry_id:142737) where moments like variance may not be stable or even exist [@problem_id:4955529].

### Critical Considerations in Data Summary

Summarizing data is not a mechanical process. Several critical issues must be considered for summaries to be valid and interpretable.

#### Limits of Standard Deviation

While the standard deviation ($\sigma$) is a ubiquitous [measure of spread](@entry_id:178320), its interpretation is highly dependent on the shape of the distribution. For a normal distribution, the "68-95-99.7" rule provides a useful heuristic for the proportion of data within $1$, $2$, and $3$ standard deviations of the mean. However, for distributions that are skewed or heavy-tailed, this rule does not apply.

The most general statement that can be made about spread using only the mean and standard deviation comes from **Chebyshev's inequality**:
$$
P(|X-\mu| \ge k\sigma) \le \frac{1}{k^2}
$$
This inequality holds for *any* distribution with a finite variance. It states, for example, that the proportion of data lying $2$ standard deviations or more from the mean cannot exceed $1/2^2 = 0.25$. Equivalently, at least $75\%$ of the data must lie within $2\sigma$ of the mean. For $k=3$, at least $8/9$ (approx. $88.9\%$) must lie within $3\sigma$ of the mean. The existence of distributions that approach this bound shows that without stronger assumptions (like normality or unimodality), $\sigma$ provides only a weak, worst-case guarantee on the concentration of data around the mean [@problem_id:4955537] [@problem_id:4955537].

#### Incomplete Data: Missingness, Censoring, and Truncation

In biostatistics, data are rarely complete. Naive summaries on the available data can lead to severe bias.

-   **Missing Data**: The validity of summaries depends on the **[missing data](@entry_id:271026) mechanism**.
    -   **Missing Completely At Random (MCAR)**: Missingness is independent of all study variables, both observed and unobserved ($R \perp (X,Z)$). Under MCAR, the observed data are a simple random subsample of the full sample, and complete-case analyses (using only observed data) are unbiased.
    -   **Missing At Random (MAR)**: Missingness depends only on observed variables, not the unobserved variable itself ($R \perp X \mid Z$). Under MAR, a complete-case analysis is generally biased, as the subsample of observed data is no longer random with respect to the outcome $X$.
    -   **Missing Not At Random (MNAR)**: Missingness depends on the value of the unobserved variable itself ($R \not\perp X \mid Z$). Here, complete-case analysis is biased, and adjustments are difficult without strong, untestable assumptions.
    Therefore, simply computing a sample mean or ECDF on the observed data is only justified under the strong and often unrealistic assumption of MCAR [@problem_id:4955545].

-   **Censoring and Truncation**: In time-to-event studies, observations are often incomplete in specific ways.
    -   **Right-censoring** occurs when a subject's event time $T$ is not observed because the study ends or the subject is lost to follow-up at a censoring time $C  T$. We only know that $T > C$.
    -   **Left-truncation** occurs when subjects are only included in the study if they are event-free at their time of entry $L$, meaning all subjects in the cohort must have $T > L$.
    A naive approach, such as calculating the sample mean of the observed follow-up times, $X = \min(T,C)$, and treating censored times as true event times, leads to a systematic **downward bias**. This is because every censored observation replaces the true, larger event time $T$ with the smaller censoring time $C$, pulling the average down. Formally, $\mathbb{E}[\min(T,C)]  \mathbb{E}[T]$ whenever there is a non-zero probability of censoring. Specialized methods, such as the Kaplan-Meier estimator, are required to correctly summarize such data [@problem_id:4955555].