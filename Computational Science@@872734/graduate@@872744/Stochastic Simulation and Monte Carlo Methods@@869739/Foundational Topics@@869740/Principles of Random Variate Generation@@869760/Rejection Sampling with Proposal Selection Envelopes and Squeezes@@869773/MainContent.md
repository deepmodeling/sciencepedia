## Introduction
Rejection sampling is a foundational Monte Carlo method for generating random samples from a target probability distribution that may be too complex to sample from directly. Its elegance lies in leveraging a simpler, easy-to-sample [proposal distribution](@entry_id:144814) to achieve this goal. However, the naive application of this technique can be prohibitively inefficient, particularly when the target density is computationally expensive to evaluate or defined over a high-dimensional space. The central challenge, which this article addresses, is how to design and implement rejection samplers that are not only correct but also computationally efficient.

This article provides a comprehensive journey into the theory and practice of [rejection sampling](@entry_id:142084), moving from core principles to advanced, state-of-the-art techniques. Across three chapters, you will gain a deep, graduate-level understanding of this powerful method. In "Principles and Mechanisms," we will derive the algorithm from first principles, analyze its efficiency, and introduce powerful enhancements like squeeze functions and adaptive envelopes. Following this, "Applications and Interdisciplinary Connections" will broaden our perspective, showcasing how these principles are applied to solve complex, high-dimensional problems and how they connect to diverse fields like optimization, machine learning, and stochastic process simulation. Finally, "Hands-On Practices" will provide a set of practical problems designed to solidify your understanding of the theoretical concepts and their real-world implications.

## Principles and Mechanisms

The previous chapter introduced the conceptual foundation of [rejection sampling](@entry_id:142084). We now undertake a rigorous examination of the principles that ensure its correctness and the mechanisms that govern its performance. This chapter will derive the method from first principles, analyze its [computational efficiency](@entry_id:270255), and explore advanced techniques such as squeeze functions, adaptive envelopes, and regional proposals that are critical for practical applications.

### The Fundamental Rejection Sampling Algorithm

The core challenge that [rejection sampling](@entry_id:142084) addresses is generating random samples from a target probability density function (PDF) $f(x)$ that is difficult to sample from directly. The method leverages our ability to sample from a simpler, more accessible **proposal density** $g(x)$. The fundamental prerequisite for this method is the existence of a constant $M \geq 1$ that establishes an **envelope** relationship between the two densities.

Specifically, for the method to be valid, the proposal $g(x)$ must be chosen such that for some finite constant $M$, the inequality $f(x) \leq M g(x)$ holds for all $x$ in the domain. This is the **envelope condition**. It ensures that the scaled proposal density $M g(x)$ serves as an upper bound, or envelope, for the target density.

The standard acceptance–rejection algorithm proceeds as follows [@problem_id:3335735]:

1.  Draw a candidate sample $X$ from the proposal distribution, $X \sim g$.

2.  Draw an auxiliary random number $U$ from the standard uniform distribution, $U \sim \mathrm{Uniform}(0,1)$. The draws of $X$ and $U$ must be independent.

3.  Accept the candidate sample $X$ if the following condition is met:
    $$
    U \leq \frac{f(X)}{M g(X)}
    $$

4.  If the condition is not met, reject the sample $X$ and return to step 1, repeating the process until a sample is accepted.

To understand why this procedure generates samples from the target density $f(x)$, we analyze the probability distribution of the accepted samples. Let the event of acceptance be denoted by $\mathcal{A}$. The joint PDF of the independently drawn pair $(X, U)$ is $p(x,u) = g(x) \cdot 1 = g(x)$ for $x$ in the domain and $u \in (0,1)$.

The probability of accepting a candidate, conditional on its value being $X=x$, is:
$$
P(\mathcal{A} | X=x) = P\left(U \leq \frac{f(x)}{M g(x)}\right)
$$
Since $U$ is uniform on $(0,1)$ and the envelope condition $f(x) \leq M g(x)$ ensures that $\frac{f(x)}{M g(x)} \in [0, 1]$, this conditional probability is simply:
$$
P(\mathcal{A} | X=x) = \frac{f(x)}{M g(x)}
$$
The [joint probability](@entry_id:266356) of drawing a candidate $x$ *and* it being accepted is the product of the probability of proposing $x$ and the [conditional probability](@entry_id:151013) of accepting it:
$$
P(X \in dx \text{ and } \mathcal{A}) = g(x) \cdot P(\mathcal{A} | X=x) \,dx = g(x) \left(\frac{f(x)}{M g(x)}\right) \,dx = \frac{f(x)}{M} \,dx
$$
This expression gives the [unnormalized density](@entry_id:633966) of the accepted samples. Observe that the proposal density $g(x)$ has cancelled out, leaving a distribution proportional to the target $f(x)$, which is precisely what we require. The constant of proportionality is $1/M$. To find the normalized density of an accepted sample, we must divide by the total probability of acceptance, which we explore next.

### Efficiency and the Cost of Rejection

The constant $M$ is not merely a mathematical construct; it is the single most important factor determining the computational efficiency of the rejection sampler. A larger value of $M$ implies a "looser" envelope, which leads to a lower probability of accepting a candidate sample.

Let's derive the unconditional probability of acceptance for a single trial, $P(\mathcal{A})$. By the law of total probability, we integrate the conditional acceptance probability over all possible values of $X$:
$$
P(\mathcal{A}) = \int P(\mathcal{A} | X=x) g(x) \,dx = \int \left(\frac{f(x)}{M g(x)}\right) g(x) \,dx = \frac{1}{M} \int f(x) \,dx
$$
If the target $f(x)$ is a normalized PDF, then $\int f(x) \,dx = 1$, and the [acceptance probability](@entry_id:138494) simplifies to a remarkably simple expression [@problem_id:3335741]:
$$
P(\mathcal{A}) = \frac{1}{M}
$$
This result reveals that the efficiency of the sampler is inversely proportional to the envelope constant $M$. To maximize efficiency, one must find a proposal $g(x)$ that minimizes $M$. The smallest admissible value for $M$ is the one that makes the envelope as tight as possible [@problem_id:3335735]:
$$
M^{\star} = \sup_{x} \frac{f(x)}{g(x)}
$$
The number of trials, $N$, required to obtain a single accepted sample follows a **geometric distribution** with success probability $p = 1/M$. The expected number of proposals needed is therefore $E[N] = 1/p = M$, and the variance is $\text{Var}(N) = (1-p)/p^2 = M(M-1)$ [@problem_id:3335772]. This makes the interpretation clear: on average, we must generate $M$ candidates from $g(x)$ to obtain one sample from $f(x)$.

In many practical scenarios, the target density is known only up to a [normalizing constant](@entry_id:752675), say $\tilde{f}(x)$, where the true density is $f(x) = \tilde{f}(x)/Z$ and $Z = \int \tilde{f}(x) \,dx$ is unknown. The envelope condition becomes $\tilde{f}(x) \leq M g(x)$. The derivation for the acceptance probability proceeds as before, yielding [@problem_id:3335793]:
$$
P(\mathcal{A}) = \frac{1}{M} \int \tilde{f}(x) \,dx = \frac{Z}{M}
$$
This important result forms the basis for using [rejection sampling](@entry_id:142084) to estimate unknown normalizing constants, a topic we will return to later.

### Enhancing Efficiency: Squeeze Functions

The cost of [rejection sampling](@entry_id:142084) is not just in the number of rejected samples, but also in the computational effort per sample. In many applications, the proposal $g(x)$ is cheap to evaluate, but the target $f(x)$ is computationally expensive. In such cases, we can improve efficiency by reducing the number of times $f(x)$ must be evaluated. This is achieved using a **squeeze function**.

A squeeze function, $s(x)$, is a non-negative function that provides a "cheap" lower bound for the target, satisfying $0 \leq s(x) \leq f(x)$ for all $x$. The chain of inequalities is now $0 \leq s(x) \leq f(x) \leq M g(x)$. The algorithm is modified to a two-stage acceptance test [@problem_id:3335788]:

1.  Draw $X \sim g$ and $U \sim \mathrm{Uniform}(0,1)$.
2.  **Squeeze Test (cheap):** If $U \leq \frac{s(X)}{M g(X)}$, accept $X$ immediately. The evaluation of $f(X)$ is avoided.
3.  **Envelope Test (expensive):** If the squeeze test fails, then evaluate $f(X)$ and accept $X$ if $U \leq \frac{f(X)}{M g(X)}$.
4.  If both tests fail, reject $X$.

This modification preserves the correctness of the sampler. The overall event for acceptance is the logical OR of the two tests: ($U \le s(X)/(M g(X))$) or ($U > s(X)/(M g(X))$ and $U \le f(X)/(M g(X))$). Since $s(x) \leq f(x)$, this union is equivalent to the single condition $U \leq f(X)/(M g(X))$. Therefore, the distribution of accepted samples and the overall [acceptance probability](@entry_id:138494) $1/M$ (or $Z/M$) remain unchanged [@problem_id:3335788].

The efficiency gain comes from the trials that pass the squeeze test, thereby saving a call to evaluate $f(X)$. The probability of this "early acceptance" is:
$$
P(\text{early accept}) = \int P\left(U \leq \frac{s(x)}{M g(x)}\right) g(x) \,dx = \int \frac{s(x)}{M g(x)} g(x) \,dx = \frac{1}{M} \int s(x) \,dx
$$
The closer the integral of $s(x)$ is to the integral of $f(x)$ (i.e., the "tighter" the squeeze), the greater the computational savings. A common and powerful way to construct squeeze functions is in the context of log-concave densities, which leads to the idea of adaptive envelopes.

### Advanced Envelope and Squeeze Constructions

The simple proposal $g(x)$ and constant $M$ form the basis of [rejection sampling](@entry_id:142084), but practical efficiency often demands more sophisticated constructions for the envelope and squeeze.

#### Adaptive Rejection Sampling (ARS)

For the important class of **log-concave** target densities (where $\log f(x)$ is a [concave function](@entry_id:144403)), a powerful technique known as **Adaptive Rejection Sampling (ARS)** can be employed. ARS dynamically builds an increasingly tight envelope and squeeze function as sampling proceeds.

The core idea is to maintain a set of abscissae (points on the x-axis) where $\log f(x)$ has been evaluated.
-   The **envelope** $u(x)$ is constructed from the exponentials of the [tangent lines](@entry_id:168168) to $\log f(x)$ at these abscissae. Since $\log f(x)$ is concave, the tangent lines lie everywhere above the function, so $\exp(\text{tangents})$ provides a valid upper bound. The log-envelope $\log u(x)$ is the pointwise minimum of these tangent-line functions.
-   The **squeeze** $s(x)$ is constructed from the exponentials of the secant lines connecting the evaluated points $(\{x_i, \log f(x_i)\})$. Concavity ensures these secants lie everywhere below the function.

The acceptance probability for this sampler is given by the ratio of the areas under the target and the envelope, $P(\text{accept}) = \frac{\int f(x)dx}{\int u(x)dx}$ [@problem_id:3335751].

The "adaptive" nature of ARS is its key feature. Whenever a sample is rejected, it is because the envelope $u(x)$ was a poor approximation of $f(x)$ at that point. The ARS algorithm then adds the rejected point to its set of abscissae. This update refines the model: a new tangent is added, creating a new, tighter envelope $u_{k+1}(x)$ such that $u_{k+1}(x) \leq u_k(x)$ for all $x$. Because the original function is strictly concave, the new envelope is *strictly* tighter in a neighborhood of the new point, meaning $\int u_{k+1}(x)dx  \int u_k(x)dx$. This strictly increases the overall [acceptance probability](@entry_id:138494), causing the sampler to become more efficient over time [@problem_id:3335751].

#### Regional Rejection Sampling

Another powerful strategy for creating a tighter envelope is to partition the domain $\mathcal{X}$ into disjoint regions $\{A_i\}$ and define a separate, local envelope constant $M_i = \sup_{x \in A_i} f(x)/g(x)$ for each region. This can produce a much tighter overall fit than a single global constant $M = \sup_i M_i$.

However, implementing this correctly requires care. A naive approach, such as drawing $X \sim g$ and then accepting with probability $f(X)/M_i$ for the region $A_i$ containing $X$, is incorrect. This procedure would produce a biased sample, as the effective re-weighting factor $1/M_i$ varies by region.

The correct approach is to define a new, composite [proposal distribution](@entry_id:144814). This can be viewed as a two-stage process [@problem_id:3335746]:
1.  Select a region $I=i$ with probability $\pi_i$ proportional to $M_i \int_{A_i} g(x) \,dx$.
2.  Draw a sample $X$ from the [proposal distribution](@entry_id:144814) $g(x)$ restricted and renormalized to the chosen region $A_i$.
3.  Accept the sample $X$ with probability $p(x) = f(x)/(M_i g(x))$.

With this construction, the [unnormalized density](@entry_id:633966) of accepted samples becomes $f(x)/C$ for all $x$, where $C = \sum_i M_i \int_{A_i} g(x) \,dx$ is the normalization constant for the region-selection probabilities. Because the density is proportional to $f(x)$ with a uniform constant, the method is correct. The overall [acceptance probability](@entry_id:138494) is $1/C$ (for a normalized $f$). As the partition is refined, the sum $\sum_i |A_i| \sup_{x \in A_i} f(x)$ (for uniform $g$) approaches the integral $\int f(x) dx = 1$, and the [acceptance probability](@entry_id:138494) converges to 1, demonstrating the potential for near-perfect efficiency [@problem_id:3335746]. This same "divide and conquer" logic can be extended to target densities that are themselves mixtures, leading to compositional [rejection sampling](@entry_id:142084) schemes [@problem_id:3335748].

### Applications and Theoretical Connections

Beyond its primary role in generating random variates, [rejection sampling](@entry_id:142084) provides tools for [statistical inference](@entry_id:172747) and possesses deep connections to information theory.

#### Estimating Normalizing Constants

As noted earlier, when sampling from an unnormalized target $\tilde{f}(x) = Z f(x)$, the [acceptance probability](@entry_id:138494) is $\alpha = Z/M$. This relationship can be inverted to estimate the unknown [normalizing constant](@entry_id:752675) $Z$. Suppose we conduct $N$ independent trials and observe $A$ acceptances. The proportion of successes, $A/N$, is an unbiased estimator for the probability $\alpha$. This leads to the following estimator for $Z$ [@problem_id:3335793]:
$$
\hat{Z} = M \left(\frac{A}{N}\right)
$$
This estimator is unbiased, as its expectation is $E[\hat{Z}] = M \cdot E[A/N] = M \alpha = M(Z/M) = Z$. The random variable $A$ follows a [binomial distribution](@entry_id:141181), $A \sim \text{Binomial}(N, \alpha)$. The variance of the estimator is therefore:
$$
\text{Var}(\hat{Z}) = \text{Var}\left(\frac{M A}{N}\right) = \left(\frac{M}{N}\right)^2 \text{Var}(A) = \frac{M^2}{N^2} \left( N \alpha(1-\alpha) \right) = \frac{M^2}{N} \frac{Z}{M}\left(1-\frac{Z}{M}\right) = \frac{MZ - Z^2}{N}
$$
The precision of the estimate improves with the number of trials $N$ and decreases as the envelope $M$ becomes looser relative to $Z$.

#### Practical Envelope Construction

A practical challenge is that the exact value of $M^{\star} = \sup_x f(x)/g(x)$ may be difficult to compute analytically. A common strategy is to approximate it by evaluating $f(x)/g(x)$ over a fine grid of points. This, however, does not guarantee a valid envelope. A rigorous approach involves using properties of the function, such as a Lipschitz constant $L$ for the ratio $r(x)=f(x)/g(x)$. If one computes the maximum on a grid with spacing $h$, $\widehat{M}_{\text{grid}}$, a valid (though possibly suboptimal) envelope constant can be constructed as $\widehat{M} = \widehat{M}_{\text{grid}} + Lh/2$. This provides a rigorous trade-off: a finer grid (smaller $h$) increases the computational cost of finding $\widehat{M}$ but results in a smaller, more efficient $\widehat{M}$, yielding a higher acceptance probability [@problem_id:3335754].

#### Connection to Information Theory

The efficiency of [rejection sampling](@entry_id:142084) has an elegant interpretation in the language of information theory. The optimal envelope constant $M^{\star} = \sup_x f(x)/g(x)$ is directly related to the order-$\infty$ **Rényi divergence**, defined as $D_{\infty}(f\|g) = \ln\left(\sup_x f(x)/g(x)\right)$.

This gives the identity $D_{\infty}(f\|g) = \ln(M^{\star})$. The maximum possible acceptance probability for a given proposal $g$ is therefore:
$$
\alpha^{\star} = \frac{1}{M^{\star}} = \frac{1}{\exp(D_{\infty}(f\|g))} = \exp(-D_{\infty}(f\|g))
$$
This profound connection reframes the problem of designing an efficient proposal distribution $g$ as a problem of minimizing the Rényi divergence between the target and the proposal [@problem_id:3335759]. It formally quantifies the notion that a good proposal must "resemble" the target, not just in its general shape, but specifically in a way that minimizes the maximum ratio of their densities.