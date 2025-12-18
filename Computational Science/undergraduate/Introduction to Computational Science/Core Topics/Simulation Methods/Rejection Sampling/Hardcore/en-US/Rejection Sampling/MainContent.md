## Introduction
In the landscape of computational science, the ability to generate random numbers from specific probability distributions is fundamental. While [standard distributions](@entry_id:190144) are easily accessible, many real-world problems in physics, statistics, and machine learning involve complex or custom distributions for which direct [sampling methods](@entry_id:141232) are unavailable. This creates a significant challenge for simulation and Monte Carlo-based inference. Rejection sampling emerges as an elegant and powerful solution to this problem, offering a general framework to sample from any target distribution, provided we can draw from a simpler, related one.

This article serves as a comprehensive guide to mastering rejection sampling. We will begin in the first chapter, **Principles and Mechanisms**, by uncovering the core of the method through intuitive geometric examples before formalizing the general algorithm, proving its correctness, and analyzing its efficiency. Next, in **Applications and Interdisciplinary Connections**, we will explore the remarkable versatility of rejection sampling, examining its role in Monte Carlo estimation, Bayesian inference, and the simulation of complex physical and [stochastic processes](@entry_id:141566). Finally, the **Hands-On Practices** chapter will provide an opportunity to solidify your understanding by tackling practical problems, from calculating efficiency to designing custom samplers for challenging targets.

## Principles and Mechanisms

The generation of random numbers from specified probability distributions is a cornerstone of computational science, enabling the simulation of complex systems and the application of Monte Carlo methods. While some distributions, like the uniform or normal, are readily available in standard software libraries, many scientific models require sampling from more complex or non-standard target distributions. Rejection sampling provides a powerful and general framework for this task, relying on a simple yet profound principle: it is possible to sample from a complex distribution by using a simpler one, provided we introduce a corrective "acceptance-rejection" step. This chapter details the foundational principles and mechanisms of this technique.

### The Geometric Intuition: Sampling by Rejection

The core concept of rejection sampling is most easily grasped through a geometric analogy. Imagine the task of generating points that are uniformly distributed within a complex shape, for which a direct sampling method is not obvious. Rejection sampling solves this by first defining a simpler, larger shape that completely encloses the target shape and from which we can easily sample points uniformly.

A classic illustration is sampling a point $(X, Y)$ uniformly from a circle of radius $R$ centered at the origin. While one might be tempted to sample a radius and an angle, this approach requires careful transformation to ensure uniformity. A more direct method is rejection sampling. We can circumscribe the circle with a square of side length $2R$, defined by the region $[-R, R] \times [-R, R]$. It is trivial to sample a point $(U, V)$ uniformly from this square by independently drawing two coordinates from a uniform distribution on $[-R, R]$.

The procedure is as follows:
1.  Generate a candidate point $(U, V)$ uniformly from the square $[-R, R] \times [-R, R]$.
2.  Check if this point lies within the target region, the circle. This is true if the condition $U^2 + V^2 \le R^2$ is met.
3.  If the condition is met, the point is **accepted**. If not, it is **rejected**, and the process repeats from step 1 until a point is accepted.

The profound result of this procedure is that any accepted point is guaranteed to be uniformly distributed within the circle. But what is the efficiency of this method? The probability that any single candidate point is accepted is simply the ratio of the area of the target region to the area of the proposal region. In this case, the area of the circle is $\pi R^2$ and the area of the square is $(2R)^2 = 4R^2$. Therefore, the [acceptance probability](@entry_id:138494) is $\frac{\pi R^2}{4R^2} = \frac{\pi}{4} \approx 0.7854$ . This means, on average, we expect to generate $1 / (\pi/4) = 4/\pi \approx 1.27$ candidate points to obtain one valid sample inside the circle.

This geometric principle is general. For instance, to generate points uniformly from the region $\mathcal{R}$ enclosed by the parabola $y = x^2$ and the line $y = 1$, we can use a rectangular proposal region $\mathcal{S}$ defined by $-1 \le x \le 1$ and $0 \le y \le 1$. The area of this proposal rectangle is $2$. The area of the target region $\mathcal{R}$ is given by the integral $\int_{-1}^{1} (1 - x^2) \, dx = \frac{4}{3}$. The probability of accepting a candidate point drawn uniformly from the rectangle is the ratio of these areas: $\frac{\text{Area}(\mathcal{R})}{\text{Area}(\mathcal{S})} = \frac{4/3}{2} = \frac{2}{3}$ .

### The General Algorithm for Probability Distributions

The geometric intuition extends directly to sampling from one-dimensional (or higher-dimensional) probability density functions (PDFs). Suppose we wish to sample from a [target distribution](@entry_id:634522) with a complex PDF, denoted $f(x)$, from which direct sampling is difficult. The [acceptance-rejection method](@entry_id:263903) allows us to use a simpler **proposal distribution**, with PDF $g(x)$, from which we can easily draw samples.

For the method to be valid, we must find a constant $M > 0$ such that the function $M g(x)$ serves as an "envelope" for $f(x)$. That is, the fundamental condition must be met:
$$ f(x) \le M g(x) \quad \text{for all } x $$
The function $M g(x)$ is often called the **[envelope function](@entry_id:749028)**. Conceptually, this inequality ensures that the scaled-up proposal density "covers" the target density at every point.

The algorithm then proceeds as follows:
1.  Draw a candidate sample $X$ from the proposal distribution $g(x)$.
2.  Draw a random number $U$ from the uniform distribution $\text{Uniform}(0, 1)$.
3.  **Accept** the candidate $X$ if it satisfies the condition:
    $$ U \le \frac{f(X)}{M g(X)} $$
    Otherwise, **reject** $X$ and return to step 1.

The collection of accepted samples will be independent draws from the target distribution $f(x)$.

Let's consider a concrete example. Suppose our target PDF is $f(x) = 2x$ for $x \in [0, 1]$. We choose a simple proposal distribution: the [uniform distribution](@entry_id:261734) on $[0, 1]$, whose PDF is $g(x) = 1$ for $x \in [0, 1]$. To find the smallest possible constant $M$, we must find the [supremum](@entry_id:140512) of the ratio $f(x)/g(x)$:
$$ M = \sup_{x \in [0, 1]} \frac{f(x)}{g(x)} = \sup_{x \in [0, 1]} \frac{2x}{1} = 2 $$
So we set $M=2$. The acceptance condition for a candidate $X$ becomes $U \le \frac{2X}{2 \cdot 1} = X$. The procedure is: draw $X \sim \text{Uniform}(0, 1)$ and $U \sim \text{Uniform}(0, 1)$, and accept $X$ if $U \le X$.

### Formal Justification and Key Properties

To understand why this method works, we must derive the probability distribution of the accepted samples. Let $X$ be a candidate drawn from $g(x)$ and $A$ be the event that $X$ is accepted. We seek the PDF of the random variable $Y$ representing an accepted sample, which is the conditional PDF of $X$ given $A$, denoted $f_Y(y)$.

Using the definition of [conditional probability](@entry_id:151013), the cumulative distribution function (CDF) of an accepted sample is:
$$ P(Y \le y) = P(X \le y | A) = \frac{P(X \le y \text{ and } A)}{P(A)} $$
The numerator is the probability that a draw is both accepted and has a value less than or equal to $y$. This is found by integrating the probability of acceptance for each value, weighted by the proposal density $g(x)$:
$$ P(X \le y \text{ and } A) = \int_{-\infty}^{y} P(\text{Accept } | X=x) g(x) \, dx = \int_{-\infty}^{y} \frac{f(x)}{M g(x)} g(x) \, dx = \frac{1}{M} \int_{-\infty}^{y} f(x) \, dx $$
The denominator, $P(A)$, is the overall probability of accepting any candidate. This is obtained by integrating over all possible values of $x$:
$$ P(A) = \int_{-\infty}^{\infty} P(\text{Accept } | X=x) g(x) \, dx = \frac{1}{M} \int_{-\infty}^{\infty} f(x) \, dx $$
Since $f(x)$ is a valid PDF, its integral over its entire domain is 1. Thus, the unconditional **acceptance probability** is simply $p = P(A) = \frac{1}{M}$.

Substituting these results back into the expression for the CDF of an accepted sample:
$$ P(Y \le y) = \frac{\frac{1}{M} \int_{-\infty}^{y} f(x) \, dx}{\frac{1}{M}} = \int_{-\infty}^{y} f(x) \, dx $$
This is precisely the CDF of the [target distribution](@entry_id:634522) $f(x)$. Differentiating with respect to $y$ gives the PDF of the accepted samples, $f_Y(y) = f(y)$, confirming that the algorithm is correct.

#### Sampling from Unnormalized Densities

A particularly powerful feature of rejection sampling is its ability to draw samples from a target density that is only known up to a constant of proportionality . This situation is common in Bayesian statistics and statistical physics, where the target density $f(x)$ is expressed as $f(x) = \frac{h(x)}{Z}$, with $h(x)$ being a known, non-negative function and $Z = \int h(x) dx$ being an unknown (and often intractable) [normalizing constant](@entry_id:752675).

The [rejection sampling algorithm](@entry_id:260966) can be adapted to this scenario without needing to compute $Z$. We find a constant $M'$ such that $h(x) \le M' g(x)$ for all $x$. The acceptance rule becomes:
$$ U \le \frac{h(X)}{M' g(X)} $$
where $X \sim g(x)$ and $U \sim \text{Uniform}(0,1)$.

Let's verify that this works. The [acceptance probability](@entry_id:138494), conditional on $X=x$, is $\alpha(x) = \frac{h(x)}{M' g(x)}$. Following the same derivation as before, the PDF of the accepted samples is:
$$ f_{acc}(x) = \frac{\alpha(x) g(x)}{\int \alpha(t) g(t) \, dt} = \frac{\frac{h(x)}{M' g(x)} g(x)}{\int \frac{h(t)}{M' g(t)} g(t) \, dt} = \frac{\frac{1}{M'} h(x)}{\frac{1}{M'} \int h(t) \, dt} = \frac{h(x)}{\int h(t) \, dt} = \frac{h(x)}{Z} = f(x) $$
The unknown constant $Z$ does not appear in the acceptance rule, demonstrating the method's utility for unnormalized densities. The overall [acceptance probability](@entry_id:138494) in this case is $p = P(A) = \frac{\int h(x) dx}{M'} = \frac{Z}{M'}$.

#### Efficiency of the Algorithm

The efficiency of rejection sampling is determined entirely by the [acceptance probability](@entry_id:138494) $p$. Since each proposal is an independent Bernoulli trial with a "success" probability of $p$, the number of trials $K$ required to obtain the first acceptance follows a **Geometric distribution** with parameter $p$ . The probability [mass function](@entry_id:158970) is $P(K=k) = (1-p)^{k-1}p$ for $k=1, 2, \dots$.

The expected number of candidates we must generate to get one accepted sample is $\mathbb{E}[K] = \frac{1}{p}$. For normalized densities $f$ and $g$, this is $\mathbb{E}[K] = M$. This highlights the central challenge in applying rejection sampling: to make the algorithm efficient, one must find a proposal distribution $g(x)$ and a constant $M$ such that $M$ is as close to 1 as possible. A large $M$ implies a low [acceptance rate](@entry_id:636682) and, consequently, a high computational cost. For example, if $f(x) = 12x(1-x)^2$ and we use a uniform proposal $g(x)=1$ on $[0,1]$, the optimal $M$ is $\sup_x f(x) = \frac{16}{9}$. The [acceptance probability](@entry_id:138494) is $p = 1/M = \frac{9}{16}$ .

### Designing an Optimal Proposal Distribution

The choice of the [proposal distribution](@entry_id:144814) $g(x)$ is the most critical factor for the efficiency of a rejection sampler. The goal is to find a $g(x)$ that "matches" the shape of $f(x)$ as closely as possible, which minimizes the necessary envelope constant $M$ and maximizes the acceptance probability $p = 1/M$.

Often, we choose a parametric family of proposal distributions $g_a(x)$ and then optimize the parameter $a$ to find the best possible proposal from that family. This involves finding the value of $a$ that minimizes the envelope constant $M(a) = \sup_x \frac{f(x)}{g_a(x)}$.

As an example, consider sampling from a normal target PDF, $p(x) = \frac{1}{\sqrt{\pi}} \exp(-x^2)$, using a Laplace proposal distribution, $q_b(x) = \frac{1}{2b} \exp(-|x|/b)$, with a tunable [scale parameter](@entry_id:268705) $b > 0$. The envelope constant $M(b)$ is the [supremum](@entry_id:140512) of the ratio:
$$ M(b) = \sup_x \frac{p(x)}{q_b(x)} = \sup_x \left[ \frac{2b}{\sqrt{\pi}} \exp\left(-x^2 + \frac{|x|}{b}\right) \right] $$
By finding the maximum of the exponent, we find that the optimal $x$ occurs at $|x| = \frac{1}{2b}$, yielding $M(b) = \frac{2b}{\sqrt{\pi}} \exp(\frac{1}{4b^2})$. To find the best proposal, we now minimize $M(b)$ with respect to $b$. Calculus reveals that the minimum occurs at $b = 1/\sqrt{2}$. The minimal possible envelope constant for this setup is $M_{min} = \sqrt{\frac{2e}{\pi}}$ . This process demonstrates how a careful analytical choice of the proposal can significantly improve algorithmic performance. A similar optimization can be performed for other target-proposal pairs, such as using an exponential proposal for a target with cubic decay .

### Critical Assumptions and Common Pitfalls

While powerful, the [rejection sampling algorithm](@entry_id:260966) relies on several critical assumptions. Violating these assumptions can lead to incorrect results or complete failure of the method.

#### Pitfall 1: Mismatched Supports
A fundamental requirement is that the **support** of the [proposal distribution](@entry_id:144814) must encompass the support of the target distribution. In other words, if $f(x) > 0$, then we must have $g(x) > 0$. If the proposal density $g(x)$ is zero in a region where the target density $f(x)$ is non-zero, the algorithm will never propose candidates from that region. The resulting samples will be drawn from a truncated version of the target, leading to a systematically **biased** result.

For example, consider a target $f(x)$ that is positive on $[0,2]$ but a proposal $g(x)$ that is only positive on $[1,2]$. The algorithm will never generate a value in $[0,1)$, no matter how many samples are drawn. If the quantity of interest depends on the values in $[0,1)$, the resulting Monte Carlo estimate will be incorrect. This is not a matter of inefficiency; it is a fundamental flaw that produces a wrong answer .

#### Pitfall 2: Heavy Tails
The condition $f(x) \le M g(x)$ for some finite $M$ implies that the ratio $f(x)/g(x)$ must be bounded. This is often violated if the tails of the [proposal distribution](@entry_id:144814) $g(x)$ decay faster than the tails of the target distribution $f(x)$. A classic example is attempting to sample from a standard **Cauchy distribution**, $f(x) \propto 1/(1+x^2)$, using a **normal distribution** $g(x) \propto \exp(-x^2/2\sigma^2)$ as the proposal . The tails of the Cauchy distribution decay polynomially ($x^{-2}$), while the tails of the [normal distribution](@entry_id:137477) decay exponentially.

The ratio $f(x)/g(x)$ will behave like $\exp(x^2/2\sigma^2)/(1+x^2)$ for large $|x|$. This ratio grows without bound as $|x| \to \infty$. Consequently, no finite constant $M$ exists that can satisfy the envelope condition. The [rejection sampling algorithm](@entry_id:260966) is not applicable in this case. The proposal must have tails that are at least as "heavy" as the target's tails.

#### Pitfall 3: Insufficient Envelope Constant
The envelope condition $f(x) \le M g(x)$ must hold for **all** values of $x$. If an analyst mistakenly chooses a constant $M$ that is too small, the condition will be violated in some regions. This means that for some candidates $X$, the acceptance ratio $\frac{f(X)}{M g(X)}$ will be greater than 1.

The effective [acceptance probability](@entry_id:138494) for a given candidate $X$ is $\min\left(1, \frac{f(X)}{M g(X)}\right)$. If $M$ is too small, this probability will be "clipped" at 1 for any $x$ where $f(x) > M g(x)$. This distorts the sampling process. Instead of producing samples from $f(x)$, the algorithm will produce samples from a different, distorted PDF. For instance, if attempting to sample from $f(x)=2x$ on $[0,1]$ with a uniform proposal $g(x)=1$, the correct $M$ is $2$. If one mistakenly uses $M=1$, the acceptance probability is $\min(1, 2x)$. This results in samples being drawn from a completely different, piecewise distribution, not the intended target $f(x)=2x$ . Correctly identifying the global supremum of $f(x)/g(x)$ is therefore essential for the validity of the algorithm.