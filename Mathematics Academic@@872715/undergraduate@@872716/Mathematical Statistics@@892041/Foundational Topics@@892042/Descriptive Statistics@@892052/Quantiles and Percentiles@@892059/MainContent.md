## Introduction
In the study of data, [measures of central tendency](@entry_id:168414) like the mean offer a snapshot of a dataset's center, but they tell only part of the story. To truly understand a distribution's shape, spread, and the relative standing of individual data points, we must turn to a more powerful set of tools: [quantiles](@entry_id:178417) and their popular expression, [percentiles](@entry_id:271763). While seemingly simple, these measures address a crucial gap in statistical analysis by providing a detailed map of a distribution's landscape, from its center to its most extreme tails.

This article provides a comprehensive exploration of [quantiles](@entry_id:178417), designed to take you from foundational theory to advanced application. In the **Principles and Mechanisms** section, we will establish the formal definition of [quantiles](@entry_id:178417), explore their calculation for both continuous and [discrete distributions](@entry_id:193344), and untangle the complexities of estimating them from sample data. The **Applications and Interdisciplinary Connections** section will showcase the versatility of [quantiles](@entry_id:178417) in fields ranging from reliability engineering and finance to machine learning and biology. Finally, the **Hands-On Practices** section will allow you to solidify your understanding by tackling practical problems. By the end, you will have a robust framework for using [quantiles](@entry_id:178417) to describe, analyze, and model data with greater precision and insight.

## Principles and Mechanisms

In statistical analysis, it is often insufficient to describe a dataset or a probability distribution using only [measures of central tendency](@entry_id:168414) like the mean. To gain a deeper understanding of the distribution's shape, spread, and tail behavior, we turn to measures of position known as **[quantiles](@entry_id:178417)**. Quantiles are points taken at regular intervals from the [cumulative distribution function](@entry_id:143135) (CDF) of a random variable, effectively partitioning the distribution into continuous intervals with equal probabilities.

This chapter delineates the principles governing [quantiles](@entry_id:178417), covering their formal definition, methods for their calculation in both theoretical and empirical contexts, and their fundamental properties and applications.

### The Formal Definition of a Quantile

For a random variable $X$ and a probability $q \in (0, 1)$, a **$q$-quantile** is a value $x_q$ that partitions the distribution such that the probability of observing a value less than or equal to $x_q$ is at least $q$, and the probability of observing a value greater than or equal to $x_q$ is at least $1-q$. More formally, $x_q$ is any number satisfying the two inequalities:

$$
P(X \le x_q) \ge q \quad \text{and} \quad P(X \ge x_q) \ge 1-q
$$

While this definition may seem complex, it is robustly applicable to all types of distributions, including continuous, discrete, and mixed distributions. Common names are given to specific [quantiles](@entry_id:178417):

*   **Median**: The $0.5$-quantile, which splits the distribution into two halves.
*   **Quartiles**: The $0.25$, $0.5$, and $0.75$-[quantiles](@entry_id:178417). The first quartile ($Q_1$) is the $0.25$-quantile, the second quartile ($Q_2$) is the median, and the third quartile ($Q_3$) is the $0.75$-quantile.
*   **Percentiles**: Quantiles where the probability $q$ is expressed as a percentage. For example, the 90th percentile is the $0.9$-quantile.

### Quantiles of Continuous Random Variables

For a [continuous random variable](@entry_id:261218) $X$ with a strictly increasing [cumulative distribution function](@entry_id:143135) (CDF), denoted $F_X(x)$, the definition of a quantile simplifies considerably. The $q$-quantile, $x_q$, is the unique value that satisfies the equation:

$$
F_X(x_q) = q
$$

This implies that the [quantile function](@entry_id:271351) is the inverse of the CDF, i.e., $x_q = F_X^{-1}(q)$. This provides a direct method for calculating theoretical [quantiles](@entry_id:178417) when the CDF is known.

Consider, for instance, a model in [reliability engineering](@entry_id:271311) where a component's lifetime $T$ is described by the CDF $F_T(t) = \frac{t^2}{t^2 + \alpha^2}$ for $t \ge 0$, where $\alpha$ is a positive parameter [@problem_id:1329216]. A metric of interest might be the "B15 life," which is the time by which 15% of components are expected to have failed. This is simply the $0.15$-quantile, $t_{0.15}$. To find it, we solve the equation $F_T(t_{0.15}) = 0.15$:

$$
\frac{t_{0.15}^2}{t_{0.15}^2 + \alpha^2} = 0.15
$$

Solving for $t_{0.15}$ yields $0.85 t_{0.15}^2 = 0.15 \alpha^2$, which simplifies to $t_{0.15} = \alpha \sqrt{\frac{3}{17}}$. This symbolic expression gives the B15 life for any component following this lifetime model, demonstrating the power of theoretical [quantiles](@entry_id:178417) in engineering applications.

Similarly, in a particle physics experiment, the energy $E$ of a particle might be modeled by the CDF $F(E) = \frac{\ln(E)}{\ln(20)}$ for $1 \le E \le 20$ [@problem_id:1943547]. To find the third quartile ($Q_3$) and the 40th percentile ($P_{40}$), we solve $F(Q_3)=0.75$ and $F(P_{40})=0.40$, respectively.

For $Q_3$, we have $\frac{\ln(Q_3)}{\ln(20)} = 0.75$, which gives $Q_3 = \exp(0.75 \ln(20)) = 20^{0.75} \approx 9.46$.
For $P_{40}$, we have $\frac{\ln(P_{40})}{\ln(20)} = 0.40$, which gives $P_{40} = \exp(0.40 \ln(20)) = 20^{0.40} \approx 3.31$.

If only the probability density function (PDF), $f(x)$, is known, one must first derive the CDF by integration, $F(x) = \int_{-\infty}^{x} f(t) dt$, before finding the quantile. This process can be more involved, especially for [piecewise functions](@entry_id:160275) [@problem_id:1949190]. For a distribution with a skewed PDF defined on $[-L, L]$, finding the 75th percentile requires normalizing the PDF to find the constant of integration, then constructing the piecewise CDF, identifying which piece contains the probability $0.75$, and finally solving for the value. Such calculations, while algebraically intensive, are a direct application of the fundamental principle $F(x_q) = q$.

### Quantiles of Discrete Random Variables

For [discrete random variables](@entry_id:163471), the CDF is a [step function](@entry_id:158924), which means a value $x$ satisfying $F(x) = q$ may not exist for every $q \in (0, 1)$. In this case, we must return to the more general definition. The $q$-quantile is often defined as the smallest value $x_q$ such that $F(x_q) \ge q$.

This concept is well-illustrated in quality control [@problem_id:1949186]. Let $X$ be the number of microchip inspections needed to find the first passing chip, where the probability of passing is $p$. $X$ follows a geometric distribution with CDF $P(X \le k) = 1 - (1-p)^k$ for integer $k \ge 1$. Suppose we want to find the minimum number of inspections $k$ to ensure a probability of at least $q$ of finding a passing chip. This is equivalent to finding the $q$-quantile of this distribution. We seek the smallest integer $k$ such that:

$$
P(X \le k) \ge q
$$

Substituting the CDF gives $1 - (1-p)^k \ge q$. After algebraic manipulation, this inequality becomes:

$$
k \ge \frac{\ln(1-q)}{\ln(1-p)}
$$

Since $k$ must be an integer, the smallest value of $k$ satisfying this is $k = \left\lceil \frac{\ln(1-q)}{\ln(1-p)} \right\rceil$. This result provides a practical performance guarantee based on the quantile of a [discrete distribution](@entry_id:274643).

### Sample Quantiles: The Challenge of Estimation

When moving from theoretical distributions to finite datasets, the calculation of [quantiles](@entry_id:178417) becomes surprisingly ambiguous. There is no single, universally accepted definition for a sample quantile, leading to different results from different statistical software packages. This ambiguity arises because we are trying to estimate the [quantiles](@entry_id:178417) of an underlying continuous distribution from a small, [discrete set](@entry_id:146023) of observations.

To illustrate, consider a small dataset of four API response times: $\{10, 20, 40, 50\}$ milliseconds [@problem_id:1949201]. Let's calculate the 75th percentile ($p=0.75$) using two common methods.

*   **Method 1 (Linear Interpolation):** This method, used by many software packages, defines a rank $r = 1 + p(n-1) = 1 + 0.75(4-1) = 3.25$. The percentile is found by interpolating between the 3rd and 4th values. The value is $(1-0.25)x_3 + 0.25x_4 = 0.75(40) + 0.25(50) = 42.5$.

*   **Method 2 (Empirical Distribution):** This method uses the rank $k = \lceil p \cdot n \rceil = \lceil 0.75 \cdot 4 \rceil = 3$. The percentile is simply the 3rd value in the sorted dataset, which is $40$.

The two standard methods yield different results, $42.5$ and $40$. This highlights the importance of understanding the specific definition used by any tool or methodology.

The choice of definition can also be affected by the size of the dataset. For instance, one common method computes the rank as $R = \frac{p}{100} \times N$ [@problem_id:1949181]. If $R$ is not an integer, the rank is rounded up. If $R$ is an integer, the percentile is the average of the values at ranks $R$ and $R+1$. For a dataset of $N=19$ scores, the 90th percentile rank is $0.90 \times 19 = 17.1$, which rounds to 18. The percentile is the 18th score. If a 20th student is added, the rank becomes $0.90 \times 20 = 18$. Now, because the rank is an integer, the percentile is the average of the 18th and 19th scores. A single data point can thus not only change the quantile's value but also the very method of its calculation.

### Properties and Applications of the Median

The median, or $0.5$-quantile, holds a special place in statistics due to several desirable properties.

#### Robustness to Outliers

Perhaps the most celebrated property of the median is its **robustness**. A statistic is robust if it is not heavily influenced by outliers or extreme values. The mean, which incorporates the value of every data point, is sensitive to [outliers](@entry_id:172866). The median, being a measure of position, is not.

Consider a corporate division with 10 analysts earning a salary $S$ and 11 managers earning a much higher salary due to a large bonus [@problem_id:1949199]. The total number of employees is 21. The sorted list of salaries would have 10 values of $S$, followed by 11 higher values. The median is the 11th value in this list, which corresponds to a manager's salary. The [arithmetic mean](@entry_id:165355), in contrast, would be an average of all salaries, a value pulled downwards by the 10 lower salaries and upwards by the 11 higher ones, resulting in a number that may not represent any single employee's compensation well. This example shows that while both are measures of center, the median often provides a more representative value of a "typical" individual in skewed distributions.

#### Symmetry

For a [continuous random variable](@entry_id:261218) $X$ with a PDF $f(x)$ that is symmetric about a point $c$ (i.e., $f(c-u) = f(c+u)$ for all $u$), the median is exactly $c$. This is because a symmetric distribution has equal probability mass on either side of the [point of symmetry](@entry_id:174836). Since the median is the point that divides the total probability into two equal halves of $0.5$, it must coincide with the [axis of symmetry](@entry_id:177299). For example, if a PDF on $[0, 6]$ is symmetric about $x=3$, its median is guaranteed to be 3, a fact that can be confirmed through direct integration but is more elegantly established by observing the symmetry [@problem_id:1949162].

#### Minimization of Absolute Deviation

The median possesses an important optimality property that provides a theoretical justification for its use. While the mean is the value $c$ that minimizes the expected squared error $E[(X-c)^2]$, the median is the value $m$ that minimizes the **expected [absolute error](@entry_id:139354)**, $E[|X-m|]$.

This can be proven by defining the cost function $g(m) = E[|X-m|] = \int_{-\infty}^{\infty} |x-m| f(x) dx$. By splitting the integral at $m$ and differentiating with respect to $m$ using the Leibniz rule, we find:

$$
g'(m) = \int_{-\infty}^{m} f(x) dx - \int_{m}^{\infty} f(x) dx = F(m) - (1 - F(m)) = 2F(m) - 1
$$

Setting the derivative to zero to find the minimum gives $2F(m) - 1 = 0$, which implies $F(m) = 0.5$. This is precisely the definition of the median. Therefore, if the cost of an error is proportional to its [absolute magnitude](@entry_id:157959), the median is the optimal choice for a reference point [@problem_id:1949182]. This property is crucial in decision theory and [economic modeling](@entry_id:144051).

### The Sampling Distribution of Quantiles

When we calculate a quantile from a sample drawn from a population, that sample quantile is a statistic. As such, it is a random variable with its own [sampling distribution](@entry_id:276447). If we were to draw multiple random samples from the same population, we would obtain a different [sample median](@entry_id:267994) for each, and these medians would form a distribution.

An interesting and sometimes counter-intuitive result is that the expected value of the [sample median](@entry_id:267994) is not necessarily equal to the true population median. This means the [sample median](@entry_id:267994) can be a biased estimator of the population median, especially in small samples.

Consider a small population of 8 salaries [@problem_id:1949183]. The population median is the average of the 4th and 5th values, which is $(50+60)/2 = 55$ thousand dollars. If we draw random samples of size 3 without replacement, we can calculate the median for each possible sample. By calculating the probability of each salary value becoming the [sample median](@entry_id:267994) and summing them up, we can find the expected value of the [sample median](@entry_id:267994). This calculation reveals an expected value of approximately $55.21$ thousand dollars. This value is close to, but not equal to, the true population median of $55$. This discrepancy illustrates the concept of [statistical bias](@entry_id:275818) and underscores the distinction between a sample statistic and its corresponding population parameter.