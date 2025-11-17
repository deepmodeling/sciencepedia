## Introduction
When analyzing a probability distribution, we often seek a "typical" value or [summary statistics](@entry_id:196779) to understand its core characteristics. While the mean provides a measure of the center, it can be misleading for distributions that are skewed or contain extreme [outliers](@entry_id:172866). This raises a crucial question: how can we describe the location and spread of a distribution in a way that is robust, comprehensive, and applicable to any data, from financial returns to biological measurements?

This article addresses this gap by providing a thorough exploration of [percentiles](@entry_id:271763), [quartiles](@entry_id:167370), and the median—fundamental concepts in probability theory that offer a richer understanding of a distribution's structure. By the end of this exploration, you will have a solid grasp of not just what these measures are, but why they are indispensable tools for modern quantitative analysis.

We will begin in the "Principles and Mechanisms" chapter by establishing the formal mathematical definitions of [quantiles](@entry_id:178417) and detailing their calculation for continuous, discrete, and mixed distributions. Next, "Applications and Interdisciplinary Connections" will demonstrate how these theoretical concepts are applied to solve real-world problems in fields ranging from engineering and finance to systems biology. Finally, the "Hands-On Practices" section will allow you to solidify your understanding by tackling practical problems, from analyzing sensor data to exploring geometric probabilities.

## Principles and Mechanisms

While the concept of a "center" or a "typical value" of a distribution is intuitively understood, its formalization requires precise mathematical definitions. This chapter delves into the principles and mechanisms governing [percentiles](@entry_id:271763), [quartiles](@entry_id:167370), and the median—fundamental tools for summarizing and interpreting probability distributions. We will explore their formal definitions, methods of calculation for different types of random variables, and their crucial properties, such as robustness and their role in [optimization problems](@entry_id:142739).

### Formal Definition of Quantiles, Percentiles, and Median

The most general way to describe the location and spread of a random variable $X$ is through its **Cumulative Distribution Function (CDF)**, denoted $F_X(x) = P(X \le x)$. Quantiles are points taken at regular intervals from the CDF of a random variable.

For any probability $p \in (0, 1)$, the **$p$-th quantile**, denoted $q_p$, is a value that partitions the distribution such that the probability of the random variable being less than or equal to $q_p$ is at least $p$, and the probability of it being greater than or equal to $q_p$ is at least $1-p$. Formally, a value $q_p$ is a $p$-th quantile if it satisfies both of the following conditions:

1.  $P(X \le q_p) \ge p$
2.  $P(X \ge q_p) \ge 1-p$

This two-sided definition is robust and applies to all types of random variables—continuous, discrete, and mixed. While it may seem complex, its necessity will become apparent when we consider [discrete distributions](@entry_id:193344) where the CDF is not continuous. In many practical scenarios, especially with continuous variables, this definition simplifies considerably.

Certain [quantiles](@entry_id:178417) are so commonly used that they have their own names:

*   **Percentiles**: The $100p$-th percentile is simply the $p$-th quantile. For example, the 90th percentile corresponds to the $0.9$-quantile.
*   **Median ($m$ or $Q_2$)**: This is the 50th percentile, or the $0.5$-quantile. It is the central value that divides the probability distribution into two equal halves: $P(X \le m) \ge 0.5$ and $P(X \ge m) \ge 0.5$.
*   **Quartiles**: These [quantiles](@entry_id:178417) divide the distribution into four equal parts.
    *   The **first quartile ($Q_1$)** is the 25th percentile ($0.25$-quantile).
    *   The **second quartile ($Q_2$)** is the median.
    *   The **third quartile ($Q_3$)** is the 75th percentile ($0.75$-quantile).
*   **Interquartile Range (IQR)**: The distance between the third and first [quartiles](@entry_id:167370), defined as $\text{IQR} = Q_3 - Q_1$. The IQR measures the spread of the central 50% of the distribution and is a robust measure of statistical dispersion.

### Calculation for Continuous Distributions

For a [continuous random variable](@entry_id:261218) $X$ with a strictly increasing CDF $F_X(x)$, the quantile $q_p$ is the unique value that satisfies the simpler equation:

$F_X(q_p) = p$

This is because for a continuous variable, $P(X \ge x) = 1 - P(X  x) = 1 - P(X \le x) = 1 - F_X(x)$, so the two conditions of the general definition become equivalent. This equation states that the area under the probability density function (PDF) to the left of $q_p$ is exactly $p$.

This relationship leads to the concept of the **[quantile function](@entry_id:271351)**, $Q(p)$, which is the inverse of the CDF:

$Q(p) = F_X^{-1}(p)$

The [quantile function](@entry_id:271351) directly provides the value of the random variable for any given cumulative probability $p$. Thus, finding the $p$-th quantile is equivalent to evaluating the [quantile function](@entry_id:271351) at $p$, i.e., $q_p = Q(p)$.

For instance, in a communication system where the [signal-to-noise ratio](@entry_id:271196) $X$ has a [quantile function](@entry_id:271351) given by $Q(p) = \sqrt{-\ln(1-p)}$, finding the median is a straightforward application of this principle [@problem_id:1378632]. The median $m$ corresponds to $p=0.5$:

$m = Q(0.5) = \sqrt{-\ln(1 - 0.5)} = \sqrt{-\ln(0.5)} = \sqrt{\ln(2)}$

More commonly, we start with a probability density function (PDF), $f_X(x)$, and must first derive the CDF. Consider the decoherence time $T$ of a qubit, which follows an [exponential distribution](@entry_id:273894) with rate $\lambda$, having a PDF $f(t) = \lambda \exp(-\lambda t)$ for $t \ge 0$ [@problem_id:1378635]. To find the median decoherence time $t_m$, we first calculate the CDF:

$F(t) = \int_{0}^{t} \lambda \exp(-\lambda s) \,ds = 1 - \exp(-\lambda t)$ for $t \ge 0$

Next, we solve $F(t_m) = 0.5$:

$1 - \exp(-\lambda t_m) = 0.5 \implies \exp(-\lambda t_m) = 0.5 \implies -\lambda t_m = \ln(0.5) = -\ln(2)$

This gives the median time $t_m = \frac{\ln(2)}{\lambda}$.

This process applies to any percentile and any distribution, even those with more complex, piecewise definitions. Imagine a climatological model where daily rainfall $X$ follows a triangular distribution [@problem_id:1378627]. To determine the threshold for an "extreme rainfall event," defined as the 90th percentile ($p_{90}$), one must undertake a complete analysis:
1.  First, the PDF must be normalized by finding the constant $C$ such that its total integral is 1.
2.  Second, the PDF is integrated to find the piecewise CDF, $F_X(x)$. This involves calculating the function for each segment of the domain.
3.  Finally, one solves the equation $F_X(p_{90}) = 0.9$. This may require checking the value of the CDF at the boundaries of the pieces to determine which formula for $F_X(x)$ to use. For the given triangular distribution, this involves solving a quadratic equation to find the final expression for $p_{90}$.

### Calculation for Discrete Distributions

When a random variable $X$ is discrete, its CDF, $F_X(x)$, is a [step function](@entry_id:158924). It is constant between the possible values of $X$ and jumps at each of these values. Consequently, for a given probability $p$, there may be no value $x$ for which $F_X(x)$ is exactly equal to $p$. This is where the general two-sided definition of a quantile becomes essential.

A common convention, which is consistent with the general definition, is to define the $p$-th quantile as the smallest value $x_k$ in the support of $X$ for which the CDF meets or exceeds $p$:

$q_p = \min \{x_k \mid F_X(x_k) \ge p\}$

Consider a model for daily defective microchips, a [discrete random variable](@entry_id:263460) $X$ with values in $\{10, 20, 30\}$ and probabilities $P(X=10)=0.45$, $P(X=20)=0.10$, and $P(X=30)=0.45$ [@problem_id:1378602]. To find the median, we first construct the CDF:
*   $F_X(10) = P(X \le 10) = 0.45$
*   $F_X(20) = P(X \le 20) = 0.45 + 0.10 = 0.55$
*   $F_X(30) = P(X \le 30) = 0.45 + 0.10 + 0.45 = 1.00$

The median is the smallest value $x$ where $F_X(x) \ge 0.5$. Since $F_X(10) = 0.45  0.5$ and $F_X(20) = 0.55 \ge 0.5$, the median is $20$. We can verify this with the two-sided definition:
*   $P(X \le 20) = 0.55 \ge 0.5$
*   $P(X \ge 20) = P(X=20) + P(X=30) = 0.10 + 0.45 = 0.55 \ge 0.5$
Both conditions are met, confirming that $20$ is the median.

A fascinating consequence of the formal definition is that the median is not always a unique number. For some distributions, an entire interval of values can serve as the median. Consider a [discrete uniform distribution](@entry_id:199268) on the set $\{1, 2, \dots, N\}$ where $N$ is an even integer [@problem_id:1378600]. In this case, any real number $m$ in the closed interval $[N/2, N/2+1]$ satisfies both median conditions: $P(X \le m) \ge 0.5$ and $P(X \ge m) \ge 0.5$. Thus, any value within this interval, including non-integers, formally qualifies as a median.

### Calculation for Mixed Distributions

Mixed random variables combine features of both [discrete and continuous variables](@entry_id:748495). Their CDFs contain both continuously increasing segments and discrete jumps. To find [quantiles](@entry_id:178417) for such distributions, one must return to the fundamental two-sided definition.

Let's analyze a sensor whose voltage output $V$ is modeled by a [mixed distribution](@entry_id:272867): with probability $3/4$, it is uniform on $[-2, 2]$, and with probability $1/4$, it is a fixed value of $5$ [@problem_id:1378616]. To find the median, we first construct the full CDF, $F_V(m) = P(V \le m)$, using the law of total probability:

$F_V(m) = P(V \le m | \text{noisy}) P(\text{noisy}) + P(V \le m | \text{saturated}) P(\text{saturated})$

This results in a piecewise CDF that has a continuous ramp over $[-2, 2)$ and then jumps at $m=5$. To find the median $m$, we must find a value that satisfies both $P(V \le m) \ge 0.5$ and $P(V \ge m) \ge 0.5$. By carefully writing out these inequalities using the derived CDF, we can solve for $m$. In this case, the conditions constrain the median to a single unique point, $m=2/3$, which lies within the continuous part of the distribution. This example highlights the power and necessity of the general quantile definition in handling complex distributional forms.

### Properties and Interpretations of Quantiles

Beyond their role as descriptive statistics, [quantiles](@entry_id:178417) possess deep theoretical properties that make them invaluable in statistical inference and decision-making.

#### Measures of Location and Symmetry

For a random variable with a PDF $f(x)$ that is symmetric about a point $c$ (i.e., $f(c-x) = f(c+x)$ for all $x$), the [point of symmetry](@entry_id:174836) $c$ is the median of the distribution. This is because the symmetry ensures that exactly half of the probability mass lies on either side of $c$. If the mean exists, it will also be equal to $c$.

This property is extremely useful. For instance, if the voltage noise in an amplifier is modeled by a symmetric triangular distribution centered at a DC offset $V_{dc}$, we immediately know the median voltage is $V_{dc}$ without any calculation [@problem_id:1378598]. Furthermore, symmetry simplifies the calculation of other [quantiles](@entry_id:178417). The first and third [quartiles](@entry_id:167370) will be equidistant from the median, so $Q_1 = V_{dc} - q$ and $Q_3 = V_{dc} + q$ for some value $q$. The IQR is then simply $2q$, and finding it reduces to solving for the deviation $q$ that encloses 25% of the probability mass between the center and $Q_3$.

#### Relationship to Skewness

When a distribution is not symmetric, the mean and median will typically diverge. This divergence provides a simple heuristic for characterizing the **skewness** of the distribution.

*   In a **right-skewed** (or positively skewed) distribution, the tail on the right side is longer. Extreme high values pull the mean upwards, while the median remains more centrally located. Thus, we typically find that **mean  median**.
*   In a **left-skewed** (or negatively skewed) distribution, the tail on the left side is longer, and extreme low values pull the mean downwards. Here, we typically find that **mean  median**.

The Chi-squared distribution, common in [goodness-of-fit](@entry_id:176037) tests, provides a clear example. For a Chi-squared distribution with $k$ degrees of freedom, the mean is exactly $k$. The median is approximately $k(1 - 2/(9k))^3$. For $k=11$, the mean is $11$ and the median is approximately $10.35$ [@problem_id:1378590]. The fact that the mean is greater than the median correctly identifies the well-known right-skew of the Chi-squared distribution. The [exponential distribution](@entry_id:273894) [@problem_id:1378635] exhibits the same property, with a mean of $1/\lambda$ and a smaller median of $(\ln 2)/\lambda \approx 0.693/\lambda$.

#### Robustness to Heavy Tails and Outliers

Perhaps the most celebrated property of the median and IQR is their **robustness**. A robust statistic is one that is not unduly affected by outliers or extreme values in a distribution. The mean, which incorporates the magnitude of every single value, is highly sensitive to [outliers](@entry_id:172866). A single extreme data point can dramatically shift the mean.

The median, by contrast, depends only on the rank-ordering of the values. It marks the 50th percentile, regardless of how far the values at the tails extend. This makes it a much more stable measure of central tendency for distributions with "heavy tails"—those where extreme events are relatively likely.

The canonical example is the Cauchy distribution, which is used to model resonance phenomena and appears in signal processing [@problem_id:1378607]. The tails of the Cauchy distribution are so heavy that the integral for its expected value does not converge; its mean is undefined. The same is true for its variance. Yet, its median and [quartiles](@entry_id:167370) are perfectly well-defined. The CDF of a Cauchy distribution is a smooth, [invertible function](@entry_id:144295), allowing for straightforward calculation of its median ($x_0$, the [location parameter](@entry_id:176482)) and its IQR ($2\gamma$, where $\gamma$ is the [scale parameter](@entry_id:268705)). This ability to provide meaningful summaries for distributions where the mean fails demonstrates the profound practical importance of [quantiles](@entry_id:178417).

#### The Median as an Optimal Choice

The choice between the mean and the median as a measure of "center" can be framed as an optimization problem. Suppose we want to choose a single number $c$ to represent a distribution $X$. What is the "best" choice? The answer depends on how we define the cost of an error $(X-c)$.

It is a well-known result that the **mean** is the value of $c$ that minimizes the **expected squared error**, $E[(X-c)^2]$. The squared error heavily penalizes large deviations.

In contrast, the **median** is the value of $c$ that minimizes the **expected [absolute error](@entry_id:139354)**, $E[|X-c|]$. The absolute error penalizes all deviations linearly, making it less sensitive to [outliers](@entry_id:172866). We can prove this by defining the expected [absolute deviation](@entry_id:265592) as a function of $c$, $D(c) = \int_{-\infty}^{\infty} |x-c|f(x)dx$. Differentiating with respect to $c$ using Leibniz's rule yields:

$\frac{dD}{dc} = \int_{-\infty}^{c} f(x)dx - \int_{c}^{\infty} f(x)dx = F(c) - (1 - F(c)) = 2F(c) - 1$

Setting the derivative to zero to find the minimum gives $2F(c) - 1 = 0$, or $F(c) = 0.5$. This is precisely the definition of the median for a continuous variable.

This property has direct practical applications. Consider an operational problem of placing a central data hub along a coastline to collect data from sensors [@problem_id:1378626]. If the energy cost of transmission is directly proportional to the distance between a sensor at position $X$ and the hub at position $c$, the total expected energy cost is proportional to $E[|X-c|]$. To minimize this cost, the hub should be placed not at the mean position of the alerts, but at their **median** position. This insight transforms a seemingly complex optimization problem into a straightforward calculation of a quantile.