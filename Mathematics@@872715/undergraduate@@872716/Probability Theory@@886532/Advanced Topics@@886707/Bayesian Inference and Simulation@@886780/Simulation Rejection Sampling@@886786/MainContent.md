## Introduction
The challenge of generating random numbers from complex probability distributions is a common hurdle in statistics, physics, and machine learning. While [standard distributions](@entry_id:190144) are easily sampled, many real-world models produce distributions that are too complex for direct methods. Rejection sampling, also known as the [acceptance-rejection method](@entry_id:263903), offers a powerful and conceptually elegant solution to this problem. It provides a general-purpose algorithm for sampling from nearly any target distribution, provided we can evaluate its density function.

This article provides a comprehensive guide to understanding and applying [rejection sampling](@entry_id:142084). The first chapter, **Principles and Mechanisms**, will dissect the core algorithm, explain the critical mathematical conditions for its validity, and analyze its efficiency. The second chapter, **Applications and Interdisciplinary Connections**, will showcase its versatility across various fields, from geometric sampling to Bayesian inference. Finally, the **Hands-On Practices** chapter will offer practical exercises to solidify your understanding and build your skills in implementing and optimizing the method.

## Principles and Mechanisms

In the study of probability and statistics, we are often confronted with the task of generating random variates from a specified probability distribution. While direct methods exist for common distributions like the uniform or normal, many complex distributions, especially those arising in specialized modeling contexts, lack straightforward sampling procedures. Rejection sampling, also known as the [acceptance-rejection method](@entry_id:263903), provides a powerful and general framework for this task. It allows us to sample from a complex **[target distribution](@entry_id:634522)**, described by a probability density function (PDF) $f(x)$, by using a simpler **proposal distribution**, $g(x)$, from which we can readily draw samples.

### The Rejection Sampling Algorithm

The core idea of [rejection sampling](@entry_id:142084) is to generate candidate samples from the [proposal distribution](@entry_id:144814) $g(x)$ and then probabilistically "accept" or "reject" them in such a way that the accepted samples follow the desired target distribution $f(x)$. For this to work, we must first identify a constant $M$ such that the function $M g(x)$ serves as an envelope for $f(x)$.

The algorithm proceeds as follows:

1.  **Setup**: Choose a proposal distribution with PDF $g(x)$ from which it is easy to sample. Find a constant $M$ such that $f(x) \le M g(x)$ for all values of $x$.
2.  **Proposal**: Generate a candidate random variate $Y$ from the [proposal distribution](@entry_id:144814) $g(x)$.
3.  **Acceptance Test**: Generate a random number $U$ from the standard [uniform distribution](@entry_id:261734), $U \sim \text{Uniform}(0, 1)$.
4.  **Decision**: If the condition $U \le \frac{f(Y)}{M g(Y)}$ is satisfied, accept the sample $X = Y$. Otherwise, reject $Y$ and return to step 2.

The process is repeated until a sample is accepted. The collection of accepted samples will form a random sample from the [target distribution](@entry_id:634522) $f(x)$.

A helpful way to visualize this process is to imagine plotting the functions $f(x)$ and $M g(x)$ on a graph. The condition $f(x) \le M g(x)$ ensures that the curve of $f(x)$ lies entirely underneath the curve of $M g(x)$. The algorithm is analogous to throwing darts at the region under the curve $M g(x)$. The horizontal position of the dart corresponds to the sampled value $Y$ from $g(x)$, and the vertical position (scaled to be between 0 and 1) corresponds to $U$. If the dart lands under the target curve $f(x)$, we "accept" it. If it lands between $f(x)$ and the envelope $M g(x)$, we "reject" it. This geometric intuition demonstrates that the probability of accepting a candidate $Y$ is proportional to the height $f(Y)$, which is precisely what is needed to sculpt the [proposal distribution](@entry_id:144814) into the shape of the target distribution.

### Fundamental Conditions for Validity

For the [rejection sampling algorithm](@entry_id:260966) to produce variates from the correct [target distribution](@entry_id:634522) $f(x)$, two fundamental conditions must be met. Violating these conditions can lead to sampling from an entirely different, and incorrect, distribution.

#### The Bounding Condition and the Constant $M$

The first and most critical condition is the existence of a finite constant $M$ such that **$f(x) \le M g(x)$ for all $x$**. This is often called the **bounding condition**. This inequality ensures that the [acceptance probability](@entry_id:138494) in step 4 of the algorithm, $\frac{f(Y)}{M g(Y)}$, is always well-defined and less than or equal to 1.

To make the algorithm as efficient as possible (i.e., to minimize the number of rejections), we should choose the smallest possible value of $M$ that satisfies this condition. This optimal value, $M^*$, is given by:

$$M^* = \sup_{x} \frac{f(x)}{g(x)}$$

Consider the task of sampling from a [target distribution](@entry_id:634522) with PDF $f(x) = 6(x - x^2)$ for $x \in [0, 1]$, using a uniform proposal distribution $g(x) = 1$ on the same interval [@problem_id:1387123]. To find the optimal $M$, we must find the maximum value of the ratio $\frac{f(x)}{g(x)} = 6(x - x^2)$ on the interval $[0, 1]$. Using basic calculus, we find the derivative is $6(1 - 2x)$, which is zero at $x = \frac{1}{2}$. The second derivative is negative, confirming this is a maximum. The value of the function at this point is $f(\frac{1}{2}) = 6(\frac{1}{2} - \frac{1}{4}) = \frac{3}{2}$. Thus, the optimal choice for the constant is $M = \frac{3}{2}$.

What happens if this condition is violated by choosing $M$ too small? Suppose one attempts to sample from $f(x) = 2x$ on $[0, 1]$ with a proposal $g(x)=1$ but mistakenly sets $M=1$ [@problem_id:1387128]. The correct optimal constant should be $M = \sup_{x \in [0,1]} \frac{2x}{1} = 2$. With the incorrect choice $M=1$, the acceptance probability for a given candidate $x^*$ becomes $\min(1, \frac{f(x^*)}{M g(x^*)}) = \min(1, 2x^*)$. For any $x^* > \frac{1}{2}$, this probability is incorrectly capped at 1, whereas it should be $x^*$. This effectively "shaves off" the top of the target distribution, distorting the final result. The resulting samples will not follow the PDF $f(x)=2x$, but rather a truncated and renormalized version of it.

#### The Support and Tail Conditions

The second crucial condition relates to the **supports** of the two distributions. The support of a PDF is the set of values where the function is non-zero. The condition is that **the support of the [proposal distribution](@entry_id:144814) $g(x)$ must contain the support of the [target distribution](@entry_id:634522) $f(x)$**. In other words, if $f(x) > 0$ for some $x$, then we must have $g(x) > 0$ for that same $x$. If this condition is not met, there will be regions where the target distribution is positive, but the [proposal distribution](@entry_id:144814) will never generate candidates. Consequently, the algorithm will never produce samples from these regions, leading to a fundamentally incorrect result.

For instance, if we try to sample from a target PDF $p(x) = 1 - \frac{x}{2}$ on $[0, 2]$ using a uniform proposal $q(x)$ on $[0, 1.5]$, we violate the support condition [@problem_id:1387084]. The algorithm can never generate a value in the interval $(1.5, 2]$, even though $p(x)$ is non-zero there. The resulting samples will be drawn from a distribution that is a truncated and renormalized version of $p(x)$ over the interval $[0, 1.5]$, not the intended target.

A more subtle implication of the bounding condition $f(x) \le M g(x)$ concerns the **tail behavior** of the distributions. For the supremum $M = \sup_x \frac{f(x)}{g(x)}$ to be finite, the tails of the [proposal distribution](@entry_id:144814) $g(x)$ must decay to zero at least as slowly as the tails of the target distribution $f(x)$. If $g(x)$ has "lighter" tails than $f(x)$, the ratio $\frac{f(x)}{g(x)}$ will grow without bound as $|x| \to \infty$, making it impossible to find a finite $M$.

A classic illustration of this is the attempt to sample from a standard **Cauchy distribution**, $f(x) = \frac{1}{\pi(1+x^2)}$, using a **Normal distribution**, $g(x)$, as the proposal [@problem_id:1387101]. The Cauchy distribution has heavy tails, decaying like $x^{-2}$. The Normal distribution, by contrast, has extremely light tails, decaying exponentially like $\exp(-x^2)$. The ratio $\frac{f(x)}{g(x)}$ is proportional to $\frac{\exp(x^2/2\sigma^2)}{1+x^2}$, which diverges to infinity as $|x|$ increases. No finite constant $M$ can be found, and thus [rejection sampling](@entry_id:142084) is not feasible with this choice of proposal. One must choose a proposal with tails that are at least as heavy as the Cauchy distribution itself.

### Efficiency and Performance Analysis

The practical utility of [rejection sampling](@entry_id:142084) depends on its **efficiency**, which is defined as the probability that a single candidate point drawn from the [proposal distribution](@entry_id:144814) is accepted. An inefficient algorithm may require an enormous number of proposals to generate a single accepted sample, rendering it computationally impractical.

The acceptance probability, let's call it $p_{accept}$, can be derived directly. For a given proposal $Y=y$, the [conditional probability](@entry_id:151013) of acceptance is $\frac{f(y)}{M g(y)}$. To find the unconditional probability of acceptance, we average this over all possible values of $Y$ according to its distribution $g(y)$:

$$p_{accept} = \mathbb{P}(\text{Accept}) = \int_{-\infty}^{\infty} \mathbb{P}(\text{Accept} | Y=y) g(y) dy = \int_{-\infty}^{\infty} \frac{f(y)}{M g(y)} g(y) dy = \frac{1}{M} \int_{-\infty}^{\infty} f(y) dy$$

Since $f(y)$ is a probability density function, its integral over its entire domain is 1. Therefore, we arrive at a remarkably simple and fundamental result:

$$p_{accept} = \frac{1}{M}$$

This result underscores the importance of choosing the smallest possible $M$. The efficiency of the algorithm is inversely proportional to $M$. A smaller $M$ means a higher acceptance rate and a more efficient simulation [@problem_id:1387108] [@problem_id:1387077].

The number of trials, $K$, needed to obtain the first accepted sample is a random variable. Since each trial is an independent Bernoulli experiment with a "success" probability of $p_{accept} = 1/M$, the random variable $K$ follows a **Geometric distribution** with parameter $p = 1/M$ [@problem_id:1387125].

The expected number of trials to get one accepted sample is the mean of this [geometric distribution](@entry_id:154371), which is:

$$E[K] = \frac{1}{p_{accept}} = M$$

This provides a direct, intuitive meaning for the constant $M$: it is the average number of candidates we must generate to obtain one valid sample from the target distribution. For example, if we wish to sample from the PDF $f(\theta) = \frac{1}{2}\sin(\theta)$ on $[0, \pi]$ using a uniform proposal $g(\theta) = \frac{1}{\pi}$ on the same interval, we first find the optimal constant $M = \sup_{\theta \in [0, \pi]} \frac{f(\theta)}{g(\theta)} = \sup_{\theta \in [0, \pi]} \frac{\pi}{2}\sin(\theta) = \frac{\pi}{2}$. The expected number of proposals to get one accepted sample is therefore $M = \frac{\pi}{2} \approx 1.57$ [@problem_id:1387124].

### Geometric Applications and the Curse of Dimensionality

The [rejection sampling](@entry_id:142084) framework has a very direct and intuitive application in geometric problems, such as sampling points uniformly from a complex shape. Suppose we wish to generate a point uniformly from a circle of radius $R$ centered at the origin [@problem_id:1387095]. A simple way to do this is to use a circumscribing square, $[-R, R] \times [-R, R]$, as the proposal region. We generate a point $(U, V)$ uniformly from this square and accept it if it falls within the circle, i.e., if $U^2 + V^2 \le R^2$.

In this context, the target PDF $f(x,y)$ is a constant $\frac{1}{\pi R^2}$ inside the circle and zero outside. The proposal PDF $g(x,y)$ is a constant $\frac{1}{(2R)^2}$ inside the square and zero outside. The [acceptance probability](@entry_id:138494) is simply the ratio of the area of the acceptance region (the circle) to the area of the proposal region (the square):

$$p_{accept} = \frac{\text{Area of Circle}}{\text{Area of Square}} = \frac{\pi R^2}{(2R)^2} = \frac{\pi}{4}$$

This corresponds exactly to the general formula $p_{accept} = 1/M$, where $M = 4/\pi$. The expected number of trials to get one point in the circle is $M = 4/\pi \approx 1.27$.

While elegant in low dimensions, this geometric interpretation reveals a major limitation of [rejection sampling](@entry_id:142084): the **[curse of dimensionality](@entry_id:143920)**. As the number of dimensions, $d$, increases, the efficiency of [rejection sampling](@entry_id:142084) can degrade catastrophically.

Consider the problem of sampling from a $d$-dimensional unit ball using a proposal from the circumscribing unit hypercube $[-1, 1]^d$ [@problem_id:1387132]. The efficiency, or acceptance probability, is the ratio of the volumes:

$$p_d = \frac{\text{Volume of } d\text{-ball}}{\text{Volume of } d\text{-cube}} = \frac{\pi^{d/2} / \Gamma(\frac{d}{2} + 1)}{2^d}$$

The expected number of trials is $E_d = 1/p_d$. As $d$ increases, the volume of the hyperball becomes an infinitesimally small fraction of the volume of the hypercube. For even dimensions $d=2k$, the expected number of trials simplifies to a striking expression:

$$E_{2k} = k! \left(\frac{4}{\pi}\right)^k$$

This value grows astonishingly fast. For $d=2$ ($k=1$), $E_2 \approx 1.27$. For $d=10$ ($k=5$), $E_{10} \approx 320$. For $d=20$ ($k=10$), $E_{20} \approx 4.6 \times 10^8$. To sample a single point from a 20-dimensional sphere would require, on average, hundreds of millions of proposals. This phenomenon makes simple [rejection sampling](@entry_id:142084) completely infeasible for high-dimensional problems, motivating the development of more advanced simulation techniques such as Markov Chain Monte Carlo (MCMC) methods, which are designed to navigate high-dimensional spaces more effectively.