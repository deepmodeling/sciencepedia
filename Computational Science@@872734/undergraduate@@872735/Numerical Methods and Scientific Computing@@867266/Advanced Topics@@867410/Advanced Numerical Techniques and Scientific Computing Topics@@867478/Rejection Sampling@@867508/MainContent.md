## Introduction
Rejection sampling, also known as the acceptance-rejection algorithm, is a fundamental Monte Carlo method used to generate random numbers from a probability distribution. In the landscape of [scientific computing](@entry_id:143987) and statistics, we often encounter complex distributions that cannot be sampled directly using simpler techniques like [inverse transform sampling](@entry_id:139050), which requires a readily invertible cumulative distribution function (CDF). Rejection sampling provides a powerful and general solution to this problem, enabling us to draw samples from nearly any target distribution, provided we can evaluate its probability density function.

This article provides a comprehensive exploration of rejection sampling, from its theoretical underpinnings to its practical implementation. Across three chapters, you will gain a robust understanding of this versatile algorithm. The first chapter, **Principles and Mechanisms**, demystifies the method by starting with a simple geometric intuition, then builds up to the formal algorithm, its mathematical justification, and key considerations for optimizing its efficiency. Next, **Applications and Interdisciplinary Connections** showcases the method's utility in the real world, exploring its role in statistical modeling, the simulation of [stochastic processes](@entry_id:141566), and solving problems in fields as diverse as [computational physics](@entry_id:146048) and finance. Finally, **Hands-On Practices** will allow you to solidify your knowledge through targeted exercises that test your understanding of the algorithm's mechanics and critical assumptions.

## Principles and Mechanisms

The fundamental challenge of generating random variates from a specified probability distribution is a cornerstone of scientific computing, simulation, and statistical inference. While methods like [inverse transform sampling](@entry_id:139050) are elegant and efficient, they require an analytically invertible cumulative distribution function (CDF), a condition not always met by the distributions encountered in practice. Rejection sampling provides a powerful and general alternative, allowing us to draw samples from a complex **[target distribution](@entry_id:634522)**, denoted by its probability density function (PDF) $f(x)$, by using a simpler **proposal distribution**, with PDF $g(x)$, from which we can already sample.

### The Geometric Intuition: Sampling as Area

The core principle of rejection sampling is best understood through a simple geometric analogy. Imagine we wish to generate points $(X, Y)$ that are uniformly distributed within a circle of radius $R$. A direct method to do this might be complex, but sampling from a square that circumscribes the circle is trivial. We can generate a candidate point by drawing its coordinates, $U$ and $V$, independently from a [uniform distribution](@entry_id:261734) on $[-R, R]$. This corresponds to picking a point uniformly at random from a square of side length $2R$.

Some of these points will fall inside the target circle, and some will fall outside. The rejection sampling strategy is to simply discard, or **reject**, the points that fall outside our desired region. We continue generating candidate points from the square until one lands inside the circle; this point is then **accepted** as a valid sample.

The probability of any single candidate point being accepted is straightforward to calculate. Since the points are chosen uniformly from the square, the probability of a point landing within the circle is the ratio of the circle's area to the square's area [@problem_id:1387095].

$$
\mathbb{P}(\text{Accept}) = \frac{\text{Area of Circle}}{\text{Area of Square}} = \frac{\pi R^2}{(2R)^2} = \frac{\pi R^2}{4 R^2} = \frac{\pi}{4}
$$

This simple example reveals the essence of the method: we define a simple-to-sample "bounding" region that contains our target region, sample from the larger region, and reject any samples that are not in the target. The accepted samples will, by construction, be uniformly distributed within the target region.

### The General Acceptance-Rejection Algorithm

We can generalize this geometric idea to sampling from any one-dimensional target PDF, $f(x)$. The "area" we are interested in is now the area under the curve of $f(x)$. The challenge is that this area is not a simple geometric shape. However, we can construct an "envelope" for this area using a proposal distribution $g(x)$ and a constant $M$.

The fundamental requirement is to find a constant $M$ such that the curve of $f(x)$ is always at or below a scaled version of the proposal PDF, $g(x)$. This is the **envelope condition**:

$$
f(x) \le M g(x) \quad \text{for all } x
$$

The function $M g(x)$ serves as an "envelope" that uniformly covers the target density $f(x)$. The algorithm then proceeds by sampling from the area under this envelope and accepting only those points that also lie under the target density's curve.

The **acceptance-rejection algorithm** is as follows:
1.  Draw a candidate sample $Y$ from the [proposal distribution](@entry_id:144814), $Y \sim g$.
2.  Draw a random number $U$ from the standard [uniform distribution](@entry_id:261734), $U \sim \text{Uniform}(0, 1)$.
3.  The candidate $Y$ is accepted if the following condition holds:
    $$
    U \le \frac{f(Y)}{M g(Y)}
    $$
    Otherwise, the candidate is rejected.
4.  Repeat steps 1-3 until a sample is accepted. The accepted sample is a draw from the [target distribution](@entry_id:634522) $f(x)$.

The inequality in step 3 is the probabilistic mechanism for checking if a point sampled uniformly from under the envelope $M g(x)$ is also under $f(x)$. A candidate $Y=y$ defines a vertical slice at that position. The height of the envelope is $M g(y)$ and the height of the target is $f(y)$. By comparing a uniform draw $U$ to the ratio $\frac{f(y)}{M g(y)}$, we are effectively selecting a random height along this slice and accepting the candidate if this height falls below the target curve.

### Formal Justification of the Method

The remarkable result of this procedure is that the distribution of the accepted samples is exactly the target distribution $f(x)$. We can prove this by deriving the conditional PDF of a candidate sample, given that it is accepted [@problem_id:1906135].

Let $A$ be the event that a candidate sample $Y \sim g$ is accepted. The probability of acceptance, given a specific value $Y=y$, is precisely the threshold used in the algorithm:
$$
\mathbb{P}(A | Y=y) = \frac{f(y)}{M g(y)}
$$

The [joint probability](@entry_id:266356) of drawing a value in an infinitesimal interval $[y, y+dy)$ and accepting it is:
$$
\mathbb{P}(Y \in [y, y+dy) \text{ and } A) = \mathbb{P}(A | Y=y) \times \mathbb{P}(Y \in [y, y+dy)) = \left(\frac{f(y)}{M g(y)}\right) (g(y) dy) = \frac{f(y)}{M} dy
$$

The total probability of accepting a candidate, $\mathbb{P}(A)$, is found by integrating this joint probability over all possible values of $y$:
$$
\mathbb{P}(A) = \int_{-\infty}^{\infty} \frac{f(y)}{M} dy = \frac{1}{M} \int_{-\infty}^{\infty} f(y) dy
$$

Since $f(y)$ is a valid PDF, its integral over its entire domain is 1. Therefore, the overall probability of accepting a single candidate is:
$$
\mathbb{P}(A) = \frac{1}{M}
$$

Now, we can find the PDF of an accepted sample, which we will call $p_{\text{acc}}(x)$. This is the conditional density of $Y$ given event $A$. Using the definition of conditional probability:
$$
p_{\text{acc}}(x) = \frac{\mathbb{P}(Y \in [x, x+dx) \text{ and } A)/dx}{\mathbb{P}(A)} = \frac{f(x)/M}{1/M} = f(x)
$$
This confirms that the samples produced by the acceptance-rejection algorithm are indeed distributed according to the target PDF, $f(x)$.

### Efficiency and Optimization

The justification above also reveals a crucial aspect of the algorithm's performance: its **efficiency**. The probability of accepting any given candidate is $p = 1/M$. This means, on average, we will need to draw $M$ candidates from the proposal distribution $g(x)$ to obtain one accepted sample from the target distribution $f(x)$. The number of trials, $K$, needed to obtain the first success (an accepted sample) follows a **Geometric distribution** with success parameter $p = 1/M$ [@problem_id:1387125].

To make the sampler as efficient as possible, we must choose the smallest possible value of $M$ that still satisfies the envelope condition $f(x) \le M g(x)$. This optimal value, denoted $M^\star$, is defined by the [supremum](@entry_id:140512) of the ratio of the two densities:
$$
M^\star = \sup_{x} \frac{f(x)}{g(x)}
$$

For instance, to sample from a target PDF $f(x) = 6(x-x^2)$ on $[0,1]$ using a uniform proposal $g(x)=1$ on the same interval, the ratio is simply $f(x)/g(x) = f(x)$. Finding the optimal $M$ reduces to finding the maximum value of $f(x)$ on $[0,1]$. A standard calculus exercise shows the maximum occurs at $x=1/2$, yielding $f(1/2) = 3/2$. Thus, the optimal choice is $M^\star = 3/2$ [@problem_id:1387123]. The [acceptance probability](@entry_id:138494) for this optimally configured sampler would be $1/M^\star = 2/3$. In another case with $f(x)=2x$ and $g(x)=1$ on $[0,1]$, $M^\star = \sup_{x \in [0,1]} 2x = 2$, making the acceptance probability $1/2$ [@problem_id:1387108].

The choice of [proposal distribution](@entry_id:144814) $g(x)$ is even more critical than the choice of $M$. A proposal that closely matches the shape of the target $f(x)$ will lead to a ratio $f(x)/g(x)$ that is nearly constant, and thus an $M^\star$ value close to 1, indicating high efficiency. An advanced application of this principle involves not just choosing a proposal family but tuning its parameters for optimal performance. Consider sampling from a standard normal target $p(x) \propto \exp(-x^2)$ using a Laplace [proposal distribution](@entry_id:144814) $q_b(x) \propto \exp(-|x|/b)$ with a tunable scale parameter $b$. One can derive an expression for the optimal envelope constant $M(b)$ as a function of $b$, and then choose the value of $b$ that minimizes $M(b)$, thereby designing the most efficient sampler within that proposal family [@problem_id:3186788]. This demonstrates that designing a good rejection sampler can be an optimization problem in itself.

### Sampling from Unnormalized Densities

One of the most powerful features of rejection sampling is its ability to generate samples from a [target distribution](@entry_id:634522) that is only known up to a constant of proportionality. In many statistical models, the target density is specified as $f(x) = \frac{h(x)}{Z}$, where $h(x)$ is a known, non-negative function, but the [normalizing constant](@entry_id:752675) $Z = \int h(x) dx$ is unknown or computationally intractable.

Rejection sampling elegantly sidesteps the need to compute $Z$. We can define our envelope condition directly in terms of $h(x)$: find a constant $M'$ such that $h(x) \le M' g(x)$ for all $x$. The acceptance condition then becomes:
$$
U \le \frac{h(Y)}{M' g(Y)}
$$
Notice that this check does not involve $Z$. To see why this works, we can follow the formal justification. The PDF of accepted samples will be:
$$
p_{\text{acc}}(x) = \frac{h(x)/M'}{\int (h(y)/M') dy} = \frac{h(x)}{\int h(y) dy} = \frac{h(x)}{Z} = f(x)
$$
The unknown constant $Z$ appears in both the numerator and denominator of the derivation and cancels out, leaving the correct target PDF. This makes rejection sampling an invaluable tool in Bayesian statistics and other fields where unnormalized posterior distributions are common [@problem_id:2403647].

### Critical Assumptions and Failure Modes

The power of rejection sampling is contingent on two critical assumptions. Violating either will not merely reduce efficiency but can render the entire simulation invalid.

#### The Support Condition

The first assumption is that the **support** of the [target distribution](@entry_id:634522) must be contained within the support of the proposal distribution. In other words, if $f(x) \gt 0$, then we must have $g(x) \gt 0$. If the proposal density is zero in a region where the target density is non-zero, the algorithm will never be able to generate samples from that region.

This violation does not increase variance; it introduces **bias**. The resulting samples are not drawn from $f(x)$, but from a truncated version of $f(x)$ restricted to the support of $g(x)$. For example, if one were to erroneously use a Uniform$[1,2]$ proposal to sample from a target that has mass on $[0,2]$, the algorithm would never produce a value less than 1. Any subsequent estimate, such as an expected value, would be systematically incorrect because it completely ignores the behavior of the function on the interval $[0,1)$ [@problem_id:2403695].

#### The Envelope Condition and Tail Behavior

The second, more subtle assumption is the existence of a finite constant $M$ that satisfies $f(x) \le M g(x)$. This is guaranteed if the ratio $f(x)/g(x)$ is bounded over the entire support. A common failure mode occurs when the tails of the [proposal distribution](@entry_id:144814) $g(x)$ decay faster than the tails of the target distribution $f(x)$.

A classic example is attempting to sample from a **Cauchy distribution**, known for its heavy tails, using a **[normal distribution](@entry_id:137477)** as a proposal. The tails of a [normal distribution](@entry_id:137477)'s PDF decay exponentially (as $\exp(-x^2)$), while the tails of a Cauchy PDF decay polynomially (as $x^{-2}$). The ratio of the Cauchy PDF to the normal PDF will grow without bound as $|x| \to \infty$. Consequently, no finite envelope constant $M$ exists, and rejection sampling cannot be applied in this scenario [@problem_id:1387101].

Even if a finite $M^\star$ exists, using a value $M \lt M^\star$ is a critical error. If the bound is underestimated, say $M=(1-\epsilon)M^\star$, there will be a region of $x$ values where $f(x) \gt M g(x)$. In this region, the acceptance ratio $\frac{f(x)}{M g(x)}$ exceeds 1, violating the probabilistic foundation of the method. If the algorithm clips this ratio to 1, it will over-sample from this region, introducing bias into the final set of samples. The probability of encountering such a violation can be explicitly calculated and serves as a measure of the risk of this error [@problem_id:3266307]. Practitioners should implement diagnostics, such as monitoring the maximum observed ratio $f(X)/g(X)$ during a pilot run, to ensure their chosen $M$ is indeed a valid upper bound.

In summary, rejection sampling is a versatile and indispensable method in computational science. Its principles, rooted in a simple geometric intuition, provide a robust framework for sampling from complex distributions, even unnormalized ones. However, its successful application demands a careful choice of proposal distribution and a rigorous verification of its two fundamental assumptions: complete support coverage and the existence of a finite envelope.