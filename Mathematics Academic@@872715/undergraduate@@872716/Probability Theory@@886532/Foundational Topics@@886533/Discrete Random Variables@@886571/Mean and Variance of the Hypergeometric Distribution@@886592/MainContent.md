## Introduction
The [hypergeometric distribution](@entry_id:193745) is the cornerstone statistical model for scenarios involving [sampling without replacement](@entry_id:276879) from a finite population. Whether drawing cards from a deck, inspecting a batch of products, or sampling genes from a genome, this distribution accurately describes the probability of obtaining a certain number of successes. While knowing the probability [mass function](@entry_id:158970) is fundamental, a deeper understanding requires quantifying the distribution's central tendency and spread. This article addresses that need by providing a clear, step-by-step derivation and analysis of the mean and variance of the [hypergeometric distribution](@entry_id:193745).

This guide is structured to build your understanding from the ground up. In "Principles and Mechanisms," we will use elegant tools like [indicator variables](@entry_id:266428) and the [linearity of expectation](@entry_id:273513) to derive the formulas for the mean and variance, interpreting key concepts like the [finite population correction factor](@entry_id:262046) along the way. Next, "Applications and Interdisciplinary Connections" will demonstrate how these statistical moments are pivotal for solving real-world problems in fields ranging from industrial quality control and ecology to bioinformatics and finance. Finally, "Hands-On Practices" will give you the opportunity to apply these concepts to concrete problems, solidifying your knowledge and building practical analytical skills. By the end, you will not only know the formulas but also understand the logic behind them and how to use them for meaningful analysis.

## Principles and Mechanisms

Having introduced the [hypergeometric distribution](@entry_id:193745) as the fundamental model for [sampling without replacement](@entry_id:276879) from a finite population, we now turn to a detailed examination of its core properties. This section will derive and interpret the distribution's mean and variance. These two measures are paramount; the mean describes the central tendency or the "expected" outcome of our sampling experiment, while the variance quantifies the spread or uncertainty around this expectation. We will begin with an elegant and intuitive derivation of the mean, followed by a more involved, yet insightful, analysis of the variance, culminating in an exploration of advanced concepts and generalizations.

### The Expected Value: A Simple Result from a Powerful Idea

Let us consider a population of size $N$ containing $K$ items classified as "successes" and $N-K$ items classified as "failures." We draw a sample of size $n$ without replacement. The random variable $X$ represents the number of successes in our sample. A natural first question is: what is the expected number of successes we should find?

One might initially think this calculation is complex because the probability of success changes with each draw. If the first item drawn is a success, the probability of the second item being a success decreases, and vice versa. While this is true, the **linearity of expectation**, a cornerstone of probability theory, allows us to circumvent this complexity with remarkable ease.

The key is to represent the total number of successes, $X$, as a sum of simpler random variables. Let us define a set of **[indicator variables](@entry_id:266428)** $X_1, X_2, \dots, X_n$, where $X_i = 1$ if the $i$-th item drawn is a success, and $X_i = 0$ otherwise. By definition, the total number of successes in the sample is the sum of these indicators:

$$
X = \sum_{i=1}^{n} X_i
$$

The power of [linearity of expectation](@entry_id:273513) is that the expectation of a sum is always the sum of the expectations, regardless of whether the variables are independent:

$$
\mathbb{E}[X] = \mathbb{E}\left[\sum_{i=1}^{n} X_i\right] = \sum_{i=1}^{n} \mathbb{E}[X_i]
$$

Now, we only need to find the expectation of a single [indicator variable](@entry_id:204387), $\mathbb{E}[X_i]$. For an [indicator variable](@entry_id:204387), the expectation is simply the probability that the event it indicates occurs: $\mathbb{E}[X_i] = \mathbb{P}(X_i = 1)$.

What is the probability that the $i$-th draw results in a success? Due to the **symmetry** of random [sampling without replacement](@entry_id:276879), any item in the population is equally likely to be in any position in the sample. Therefore, the probability that the $i$-th draw is a success is identical to the probability that the first draw is a success. This probability is simply the initial proportion of successes in the population.

$$
\mathbb{E}[X_i] = \mathbb{P}(X_i = 1) = \frac{K}{N}
$$

This holds for every $i$ from $1$ to $n$. Substituting this back into our sum, we arrive at the formula for the mean of the [hypergeometric distribution](@entry_id:193745):

$$
\mathbb{E}[X] = \sum_{i=1}^{n} \frac{K}{N} = n \frac{K}{N}
$$

This result is beautifully intuitive. The expected number of successes in the sample is the sample size multiplied by the initial proportion of successes in the population.

Consider a practical scenario from quality control [@problem_id:1373487]. A shipment of $N=50$ transistors contains $K=7$ defective ones. An inspector draws a sample of $n=10$. The expected number of defective transistors in the sample is simply $\mathbb{E}[X] = 10 \times \frac{7}{50} = \frac{7}{5} = 1.4$. This calculation, made simple by [indicator variables](@entry_id:266428), confirms our intuition. Similarly, if a batch of 500 gene-synthesis kits contains an average of 60 with a faulty enzyme ($N=500, K=60$), the expected number of faulty kits in a sample of 25 is $\mathbb{E}[X] = 25 \times \frac{60}{500} = 3$ [@problem_id:1373510].

### The Variance: Quantifying Uncertainty in Dependent Draws

Calculating the variance of $X$ is more involved. Unlike expectation, variance is not linear in general. The [variance of a sum of random variables](@entry_id:272198) depends on their covariances:

$$
\operatorname{Var}(X) = \operatorname{Var}\left(\sum_{i=1}^{n} X_i\right) = \sum_{i=1}^{n} \operatorname{Var}(X_i) + \sum_{i \neq j} \operatorname{Cov}(X_i, X_j)
$$

Because we are sampling *without* replacement, the outcomes of the draws are not independent, which means the covariance terms are non-zero. Let's derive each component systematically, using the same [indicator variable](@entry_id:204387) framework [@problem_id:1373495].

Let $p = K/N$ be the initial proportion of successes.

1.  **Variance of an [indicator variable](@entry_id:204387), $\operatorname{Var}(X_i)$**:
    Since $X_i$ is a Bernoulli random variable with success probability $p$, its variance is a standard result:
    $$
    \operatorname{Var}(X_i) = p(1-p) = \frac{K}{N} \left(1 - \frac{K}{N}\right)
    $$

2.  **Covariance of two distinct [indicator variables](@entry_id:266428), $\operatorname{Cov}(X_i, X_j)$ for $i \neq j$**:
    The covariance is defined as $\operatorname{Cov}(X_i, X_j) = \mathbb{E}[X_i X_j] - \mathbb{E}[X_i]\mathbb{E}[X_j]$. The term $\mathbb{E}[X_i X_j]$ is the probability that both the $i$-th and $j$-th draws are successes, $\mathbb{P}(X_i=1, X_j=1)$. By symmetry, this is the same as the probability that the first two draws are successes:
    $$
    \mathbb{E}[X_i X_j] = \mathbb{P}(X_1=1, X_2=1) = \mathbb{P}(X_1=1) \cdot \mathbb{P}(X_2=1 | X_1=1) = \frac{K}{N} \cdot \frac{K-1}{N-1}
    $$
    Now we can compute the covariance:
    $$
    \operatorname{Cov}(X_i, X_j) = \frac{K(K-1)}{N(N-1)} - \left(\frac{K}{N}\right)^2 = \frac{K}{N} \left( \frac{K-1}{N-1} - \frac{K}{N} \right)
    $$
    $$
    = \frac{K}{N} \left( \frac{N(K-1) - K(N-1)}{N(N-1)} \right) = \frac{K}{N} \left( \frac{NK - N - NK + K}{N(N-1)} \right) = \frac{K}{N} \left( \frac{K-N}{N(N-1)} \right)
    $$
    $$
    = -\frac{K(N-K)}{N^2(N-1)} = -\frac{p(1-p)}{N-1}
    $$
    The covariance is negative. This confirms our intuition: knowing that one draw was a success (e.g., $X_i=1$) removes a success from the pool, thus slightly decreasing the probability of another draw being a success.

Now, we assemble the variance of $X$. There are $n$ variance terms and $n(n-1)$ [ordered pairs](@entry_id:269702) for the covariance calculation (which can also be written as $2 \binom{n}{2}$ terms):

$$
\operatorname{Var}(X) = n \cdot \operatorname{Var}(X_i) + n(n-1) \cdot \operatorname{Cov}(X_i, X_j)
$$

Substituting our results:
$$
\operatorname{Var}(X) = n \cdot p(1-p) + n(n-1) \left( -\frac{p(1-p)}{N-1} \right)
$$
Factoring out the common term $n \cdot p(1-p)$:
$$
\operatorname{Var}(X) = n p(1-p) \left( 1 - \frac{n-1}{N-1} \right) = n p(1-p) \left( \frac{(N-1) - (n-1)}{N-1} \right)
$$
This simplifies to the final, canonical formula for the variance of the [hypergeometric distribution](@entry_id:193745):
$$
\operatorname{Var}(X) = n \frac{K}{N} \left(1 - \frac{K}{N}\right) \frac{N-n}{N-1}
$$

For example, in a study of 100 tissue samples of which 30 have a genetic marker ($N=100, K=30$), if a technician selects 12 samples ($n=12$), the variance in the number of marked samples is calculated using this formula [@problem_id:1373498]. The result would be $\operatorname{Var}(X) = 12 \cdot \frac{30}{100} \cdot \frac{70}{100} \cdot \frac{100-12}{100-1} \approx 2.240$. The **standard deviation**, a more interpretable [measure of spread](@entry_id:178320) in the same units as the mean, is simply the square root of the variance, $\sigma_X = \sqrt{\operatorname{Var}(X)}$ [@problem_id:1373489].

### Interpreting the Variance: The Finite Population Correction Factor

The formula for the hypergeometric variance is revealing when compared to its counterpart for the binomial distribution. If we were sampling *with* replacement, the number of successes would follow a [binomial distribution](@entry_id:141181) with variance $n p(1-p)$. Our formula is:

$$
\operatorname{Var}(X) = \underbrace{n p(1-p)}_{\text{Binomial Variance}} \times \underbrace{\frac{N-n}{N-1}}_{\text{Finite Population Correction}}
$$

The term $\frac{N-n}{N-1}$ is known as the **[finite population correction](@entry_id:270862) (FPC)** factor. It precisely captures the reduction in variance due to [sampling without replacement](@entry_id:276879). Let's analyze its behavior:

*   **When $n=1$**, the FPC is 1. The variance of a single draw is $p(1-p)$, which is logical.
*   **As $N \to \infty$ for a fixed $n$**, the FPC approaches 1, since $\frac{N-n}{N-1} \approx \frac{N}{N} = 1$. This mathematically confirms why the [binomial distribution](@entry_id:141181) is an excellent approximation for the [hypergeometric distribution](@entry_id:193745) when the population size $N$ is very large compared to the sample size $n$. In such cases, removing a few items from the population does not significantly alter the probability of success for subsequent draws.
*   **When $n=N$**, the FPC is $\frac{N-N}{N-1} = 0$. The variance is zero. This is perfectly intuitive: if we sample the entire population, there is no uncertainty. We know we will find exactly $K$ successes.

The FPC quantifies how much information is gained from the fact that we do not replace the items. A fascinating question arises from this relationship: for a given population of size $N$, what sample size $n$ would cause the true hypergeometric variance to be exactly half of the variance predicted by the simpler [binomial model](@entry_id:275034) [@problem_id:1373490]? To find this, we set the FPC to $0.5$:

$$
\frac{N-n}{N-1} = \frac{1}{2}
$$
Solving for $n$ gives $2(N-n) = N-1$, which simplifies to $2N - 2n = N-1$, leading to $n = \frac{N+1}{2}$. This surprising result shows that one must sample roughly half of the population for the variance reduction from [sampling without replacement](@entry_id:276879) to be 50%.

### Advanced Principles and Generalizations

The foundational formulas for mean and variance enable a deeper exploration of the [hypergeometric distribution](@entry_id:193745)'s properties and its application to more complex scenarios.

#### Optimizing Sample Design: The Maximization of Variance

In experimental design, we sometimes wish to choose a sample size that maximizes the variability of an outcome, perhaps to enhance the [statistical power](@entry_id:197129) of a test. Let's consider the variance of the [hypergeometric distribution](@entry_id:193745) as a function of the sample size, $n$:

$$ V(n) = \left( \frac{K(N-K)}{N^2(N-1)} \right) \cdot n(N-n) $$

The first part of this expression is a positive constant with respect to $n$. Therefore, to maximize $V(n)$, we need only maximize the quadratic function $g(n) = n(N-n) = Nn - n^2$. This function describes a downward-opening parabola whose vertex (maximum point) occurs at $n = N/2$.

This means that for a fixed population size $N$, the uncertainty about the number of successes in a sample is greatest when the sample size is half the population size [@problem_id:1373512]. Intuitively, if we take a very small sample ($n \approx 1$), we expect a count near zero. If we take a very large sample ($n \approx N$), we expect a count near $K$. In both cases, the outcome is quite predictable. The greatest uncertainty occurs in the middle, when we sample half the population. If $N$ is an even integer, the optimal sample size is exactly $n=N/2$.

#### Variance of Linear Combinations

The standard rules for variances of linear transformations apply directly to hypergeometric random variables. For constants $a$ and $b$, we know that $\operatorname{Var}(aX+b) = a^2 \operatorname{Var}(X)$. This property is useful for analyzing derived quantities.

For instance, in a [population genetics](@entry_id:146344) study, researchers might be interested in the difference, $D$, between the number of carriers ($X_C$) and non-carriers ($X_{NC}$) in a sample of size $n$ [@problem_id:1373499]. Since $X_C + X_{NC} = n$, we can write $X_{NC} = n - X_C$. The difference is:

$$
D = X_C - X_{NC} = X_C - (n - X_C) = 2X_C - n
$$

Here, $X_C$ is our hypergeometric random variable $X$. Using the property of variance, the variance of this difference is:

$$
\operatorname{Var}(D) = \operatorname{Var}(2X - n) = 2^2 \operatorname{Var}(X) = 4 \operatorname{Var}(X)
$$

Thus, the variance of the imbalance between the two groups is simply four times the variance of the number of carriers.

#### The Multivariate Hypergeometric Distribution

The principles we have developed can be extended to populations partitioned into more than two categories. Suppose a population of size $N$ is composed of $m$ different types of items, with $N_k$ items of type $k$ for $k=1, \dots, m$, such that $\sum N_k = N$. If we draw a sample of size $n$, let $X_k$ be the number of items of type $k$ in the sample. The vector $(X_1, \dots, X_m)$ follows a **multivariate [hypergeometric distribution](@entry_id:193745)**.

The mean and variance for each $X_k$ are direct analogues of the two-category case:
$$ \mathbb{E}[X_k] = n \frac{N_k}{N} $$
$$ \operatorname{Var}(X_k) = n \frac{N_k}{N} \left(1 - \frac{N_k}{N}\right) \frac{N-n}{N-1} $$

Crucially, we can also define the covariance between the counts of two different categories, $X_i$ and $X_j$ for $i \neq j$. A similar derivation as before yields:
$$ \operatorname{Cov}(X_i, X_j) = -n \frac{N_i}{N} \frac{N_j}{N} \frac{N-n}{N-1} $$
The covariance is again negative, reflecting the competition for slots in the sample: finding more items of type $i$ leaves less room for items of type $j$.

These moments are essential for analyzing more complex models. For example, if a signal $S$ is a weighted sum of counts from different species in a genomics sample, $S = \sum_{k=1}^m w_k X_k$, its variance can be calculated using the general formula for the variance of a sum [@problem_id:1373496]:

$$
\operatorname{Var}(S) = \sum_{k=1}^{m} w_k^2 \operatorname{Var}(X_k) + \sum_{i \neq j} w_i w_j \operatorname{Cov}(X_i, X_j)
$$
Substituting the expressions for the variance and covariance leads to a [closed-form expression](@entry_id:267458) for the signal's fluctuation, which is critical for assessing the reliability of the measurement protocol.

#### Invariance in Sequential Sampling

A final, elegant principle relates to sequential sampling. Consider a two-stage process where a sample of $n_1$ is drawn, and then a second sample of $n_2$ is drawn from the remaining $N-n_1$ items [@problem_id:1373526]. Let $X_2$ be the number of successes in the second sample. What is its (unconditional) variance?

One might guess the process is more complex, as the parameters for the second draw depend on the outcome of the first. However, the principle of symmetry once again provides a powerful shortcut. From an unconditional standpoint, before any sampling has occurred, any set of $n_2$ items has the same probability of constituting the second sample. Therefore, the unconditional distribution of $X_2$ must be identical to that of a single sample of size $n_2$ drawn directly from the original population.

This implies that the mean and variance of $X_2$ are given by the standard hypergeometric formulas, with sample size $n_2$:

$$ \mathbb{E}[X_2] = n_2 \frac{K}{N} $$
$$ \operatorname{Var}(X_2) = n_2 \frac{K}{N} \left(1 - \frac{K}{N}\right) \frac{N-n_2}{N-1} $$

This non-obvious result can be proven formally using the Law of Total Variance, but its conceptual foundation lies in the [exchangeability](@entry_id:263314) of items in a random sample. It demonstrates that the sequential nature of the sampling does not alter the [marginal distribution](@entry_id:264862) of the count in a subsequent sample, a profound and useful result in the theory of sampling.