## Introduction
Many real-world systems, from financial markets to biological populations, exhibit sudden, unpredictable changes that cannot be captured by continuous models like Brownian motion. The theory of Poisson random measures provides the essential mathematical framework for describing and analyzing these discontinuous "jump" phenomena. Classical stochastic calculus, built upon continuous martingales, is insufficient for handling such processes, creating a knowledge gap for modeling a wide range of important dynamics.

This article bridges that gap by systematically developing a rigorous calculus for [jump processes](@entry_id:180953). Across three chapters, you will embark on a structured journey from fundamental theory to practical application. The first chapter, **Principles and Mechanisms**, lays the groundwork by defining Poisson random measures and introducing the critical concept of compensation, which is the key to constructing a martingale-based calculus. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates how these theoretical tools are deployed to build and analyze sophisticated models in diverse fields like finance, physics, and insurance. Finally, **Hands-On Practices** offers a set of targeted problems to solidify your understanding and build practical skills. This comprehensive exploration will equip you with the theoretical knowledge and practical insight needed to master the stochastic calculus of jumps.

## Principles and Mechanisms

In the study of [stochastic processes](@entry_id:141566), Brownian motion provides a [canonical model](@entry_id:148621) for continuous random evolution. However, many systems in finance, physics, and biology exhibit abrupt, discontinuous changes or "jumps." To model such phenomena, we must extend our mathematical toolkit beyond the calculus of continuous [martingales](@entry_id:267779). The theory of Poisson random measures and their compensation provides the foundational framework for constructing a rigorous calculus for [jump processes](@entry_id:180953). This chapter will develop this theory, starting from the basic definition of a random measure and culminating in its application to the decomposition of general [jump processes](@entry_id:180953).

### From Random Measures to Poisson Random Measures

A natural way to describe random jumps is to count the number of events occurring in different regions of a space. This concept is formalized by the idea of a **random measure**.

Let $(\Omega, \mathcal{F}, \mathbb{P})$ be a probability space, representing the underlying source of randomness, and let $(E, \mathcal{E})$ be a [measurable space](@entry_id:147379), which we will call the **state space** or **mark space**. A **random measure** $N$ is a mapping $N: \Omega \times \mathcal{E} \to \mathbb{N}_0 \cup \{\infty\}$ that satisfies two key properties [@problem_id:3070063]:

1.  **Measure Property**: For each fixed outcome $\omega \in \Omega$, the function $A \mapsto N(\omega, A)$ is a measure on the state space $(E, \mathcal{E})$. This means it is countably additive: for any sequence of pairwise [disjoint sets](@entry_id:154341) $A_1, A_2, \dots$ in $\mathcal{E}$, we have $N(\omega, \bigcup_{i=1}^\infty A_i) = \sum_{i=1}^\infty N(\omega, A_i)$. It also implies $N(\omega, \emptyset) = 0$. In essence, for a given realization of the world, the counts of random points behave like a standard measure.

2.  **Measurability Property**: For each fixed set $A \in \mathcal{E}$, the function $\omega \mapsto N(\omega, A)$ is a random variable. That is, it is a [measurable function](@entry_id:141135) from $(\Omega, \mathcal{F})$ to $(\mathbb{N}_0 \cup \{\infty\}, 2^{\mathbb{N}_0 \cup \{\infty\}})$. This ensures that we can make probabilistic statements about the number of points in any given set $A$, for instance, by calculating probabilities like $\mathbb{P}(\{\omega \in \Omega : N(\omega, A) = k\})$ for $k \in \mathbb{N}_0 \cup \{\infty\}$.

While this definition is general, it lacks specific distributional structure. The most fundamental and widely used random measure is the **Poisson random measure (PRM)**. A PRM is uniquely defined by its **intensity measure**, a deterministic measure $\nu$ on the state space $(E, \mathcal{E})$.

A random measure $N$ is a Poisson random measure with intensity measure $\nu$ if it satisfies two additional statistical properties [@problem_id:3070065]:

1.  **Poisson Counts**: For any measurable set $A \in \mathcal{E}$ with finite intensity $\nu(A)  \infty$, the random variable $N(A)$ follows a Poisson distribution with parameter $\nu(A)$. That is,
    $$ \mathbb{P}(N(A) = k) = \frac{e^{-\nu(A)}(\nu(A))^k}{k!} $$
    for $k = 0, 1, 2, \dots$. If $\nu(A) = \infty$, we define $N(A) = \infty$ [almost surely](@entry_id:262518).

2.  **Independent Increments**: For any finite collection of pairwise [disjoint sets](@entry_id:154341) $A_1, A_2, \dots, A_k$ in $\mathcal{E}$, the random variables $N(A_1), N(A_2), \dots, N(A_k)$ are mutually independent.

The intensity measure $\nu(A)$ can be intuitively understood as the expected number of points falling into the set $A$. Indeed, the expectation of a Poisson random variable with parameter $\mu$ is $\mu$, so $\mathbb{E}[N(A)] = \nu(A)$.

A crucial technical condition for the existence of a well-behaved PRM is that the intensity measure $\nu$ must be **$\sigma$-finite**. A measure $\nu$ on $(E, \mathcal{E})$ is $\sigma$-finite if the entire space $E$ can be covered by a countable collection of sets $\{E_n\}_{n \in \mathbb{N}}$, each having finite intensity, i.e., $E = \bigcup_{n=1}^\infty E_n$ with $\nu(E_n)  \infty$ for all $n$ [@problem_id:3070104]. This condition ensures that the total number of points in the support of the random measure is [almost surely](@entry_id:262518) countable. On each set $E_n$, the number of points $N(E_n)$ is a Poisson random variable with a finite parameter, and is thus finite [almost surely](@entry_id:262518). The total set of random points is a countable union of these [finite sets](@entry_id:145527), and is therefore itself countable. This [countability](@entry_id:148500) is essential for representing the jumps of a [stochastic process](@entry_id:159502) as a discrete sequence [@problem_id:3070104]. A common example is the standard Poisson process on $\mathbb{R}_+$, which is a PRM whose intensity measure is the Lebesgue measure. The Lebesgue measure is not finite on $\mathbb{R}_+$, but it is $\sigma$-finite, as $\mathbb{R}_+ = \bigcup_{n=1}^\infty [n-1, n)$.

### The Principle of Compensation

The PRM provides a powerful tool for modeling jumps, but it has a non-[zero mean](@entry_id:271600), $\mathbb{E}[N(A)] = \nu(A)$. In the context of [stochastic calculus](@entry_id:143864), we are often interested in constructing martingales, which are processes with zero expected drift. To build a martingale-based theory for [jump processes](@entry_id:180953), analogous to Itô calculus for Brownian motion, we must first remove the inherent "drift" from the PRM. This is achieved through **compensation**.

Given a PRM $N$ with intensity measure $\nu$, we define the **compensated Poisson random measure**, denoted $\tilde{N}$, by formally subtracting the intensity:
$$ \tilde{N}(A) := N(A) - \nu(A) $$
This definition applies to any set $A \in \mathcal{E}$ for which $\nu(A)  \infty$. The measure $\nu$ is called the **compensator** of $N$.

The effect of compensation is immediately apparent when we examine the first and second moments of $\tilde{N}(A)$ for a set $A$ with $\nu(A)  \infty$ [@problem_id:3070078]. Let $\mu = \nu(A)$.

The expectation of the compensated count is:
$$ \mathbb{E}[\tilde{N}(A)] = \mathbb{E}[N(A) - \mu] = \mathbb{E}[N(A)] - \mu = \mu - \mu = 0 $$
By subtracting the mean, we have created a random variable with an expectation of zero.

The second moment of the compensated count is equal to its variance, since its mean is zero:
$$ \mathbb{E}[\tilde{N}(A)^2] = \text{Var}(\tilde{N}(A)) = \text{Var}(N(A) - \mu) $$
Since $\mu$ is a deterministic constant, it does not affect the variance. The variance of a Poisson($\mu$) random variable is $\mu$. Therefore:
$$ \mathbb{E}[\tilde{N}(A)^2] = \text{Var}(N(A)) = \mu = \nu(A) $$
This remarkable property, where the second moment of the compensated measure equals the intensity of the original measure, is the foundation for the Itô [isometry](@entry_id:150881) for [jump process](@entry_id:201473) integrals.

For processes evolving in time, we typically consider a PRM on the product space $\mathbb{R}_+ \times E$, with a deterministic intensity measure of the form $\nu(dt, dx) = dt \otimes \lambda(dx)$, where $dt$ is the Lebesgue measure on time and $\lambda$ is a $\sigma$-[finite measure](@entry_id:204764) on the mark space $E$. In this setting, the compensation is written as $\tilde{N}(dt, dx) = N(dt, dx) - dt\,\lambda(dx)$.

### Stochastic Integration with Respect to Random Measures

The true power of the PRM framework is realized when we move from counting points in fixed sets to integrating functions against the random measure. Let $H(\omega, t, x)$ be a suitable [random process](@entry_id:269605) defined on $\Omega \times \mathbb{R}_+ \times E$. The [stochastic integral](@entry_id:195087) $\int_0^T \int_E H(s,x) N(ds,dx)$ can be thought of as a sum of the values of $H$ evaluated at the time and location of each jump of the process $N$.

A cornerstone result for integrals with respect to a PRM is **Campbell's Theorem**, which gives the expectation of the integral. For a suitable integrand $H$, we have [@problem_id:3070065, @problem_id:3070107]:
$$ \mathbb{E}\left[\int_0^T \int_E H(s,x) N(ds,dx)\right] = \mathbb{E}\left[\int_0^T \int_E H(s,x) ds\,\lambda(dx)\right] $$
This formula shows that the expectation of the [stochastic integral](@entry_id:195087) with respect to $N$ is equal to the expectation of its integral with respect to the deterministic intensity measure.

Using this result, we can immediately find the expectation of an integral with respect to the compensated measure $\tilde{N}$:
$$ \mathbb{E}\left[\int_0^T \int_E H(s,x) \tilde{N}(ds,dx)\right] = \mathbb{E}\left[\int_0^T \int_E H(s,x) (N(ds,dx) - ds\,\lambda(dx))\right] $$
$$ = \mathbb{E}\left[\int_0^T \int_E H(s,x) N(ds,dx)\right] - \mathbb{E}\left[\int_0^T \int_E H(s,x) ds\,\lambda(dx)\right] = 0 $$
This confirms that stochastic integrals with respect to a compensated PRM are zero-mean random variables, a key characteristic of [martingales](@entry_id:267779).

Furthermore, we can establish an isometry for these integrals, which is the analogue of the Itô isometry for Brownian motion. For a suitable integrand $H$, the second moment of the integral with respect to $\tilde{N}$ is given by [@problem_id:3070065]:
$$ \mathbb{E}\left[ \left( \int_0^T \int_E H(s,x) \tilde{N}(ds,dx) \right)^2 \right] = \mathbb{E}\left[ \int_0^T \int_E H(s,x)^2 ds\,\lambda(dx) \right] $$
This **Itô [isometry](@entry_id:150881) for Poisson integrals** is the central tool for constructing the theory of [stochastic integration](@entry_id:198356) for [jump processes](@entry_id:180953). It provides a way to define the integral for a wide class of integrands by starting with [simple functions](@entry_id:137521) and using a completion argument, similar to the construction of the Lebesgue integral [@problem_id:3070082].

### Predictability and the Martingale Property

We have seen that integrals with respect to $\tilde{N}$ have [zero mean](@entry_id:271600). The deeper and more useful property is that, under appropriate conditions, the process defined by such an integral, $M_t = \int_0^t \int_E H(s,x) \tilde{N}(ds,dx)$, is a **martingale** with respect to the underlying filtration $(\mathcal{F}_t)$. This property, however, hinges on a crucial condition on the integrand $H$: it must be **predictable**.

To understand predictability, consider the information available to an observer. At time $t$, the [filtration](@entry_id:162013) $\mathcal{F}_t$ represents all information available up to and including time $t$. A process is **adapted** if $H_t$ is known at time $t$. However, this means $H_t$ could depend on whether a jump of $N$ occurred *at the exact moment* $t$. If we were allowed to use such an integrand in our stochastic integral, we could construct a "trading strategy" that foresees a jump an instant before it happens, leading to unbounded profits and breaking the [martingale property](@entry_id:261270).

To prevent this, we require that the value of the integrand $H$ at time $t$ be determined by information available strictly *before* time $t$. This is the intuitive meaning of predictability. Formally, the **predictable $\sigma$-algebra** $\mathcal{P}$ on $\Omega \times \mathbb{R}_+$ is the smallest $\sigma$-algebra that makes all left-continuous [adapted processes](@entry_id:187710) measurable. A process $H(\omega, t)$ is predictable if it is measurable with respect to $\mathcal{P}$. Requiring our integrand $H(\omega, t, x)$ to be $\mathcal{P} \otimes \mathcal{E}$-measurable ensures that $H_t$ is determined by the filtration $\mathcal{F}_{t-}$, the information just before time $t$ [@problem_id:3070055].

With this condition, the integral against the compensated measure $\tilde{N}$ becomes a [local martingale](@entry_id:203733). In general, for any integer-valued random measure $N$, its compensator $\nu$ is its **dual predictable projection**. This is the unique predictable random measure such that for any suitable non-negative [predictable process](@entry_id:274260) $H$, the process $\int H dN - \int H d\nu$ is a [local martingale](@entry_id:203733) [@problem_id:3070040]. For a PRM with a deterministic intensity measure $dt\,\lambda(dx)$, this compensator is simply $dt\,\lambda(dx)$ itself.

The local [martingale property](@entry_id:261270) can be strengthened under stronger [integrability conditions](@entry_id:158502) on the integrand $H$ [@problem_id:3070056]:
*   If $H$ is a [predictable process](@entry_id:274260) that satisfies the square-[integrability condition](@entry_id:160334) $\mathbb{E}\left[\int_0^T \int_E H(s,x)^2 ds\,\lambda(dx)\right]  \infty$, then the integral process $M_t = \int_0^t \int_E H(s,x) \tilde{N}(ds,dx)$ is a **square-integrable [martingale](@entry_id:146036)**. Its predictable [quadratic variation](@entry_id:140680) is given by $\langle M \rangle_t = \int_0^t \int_E H(s,x)^2 ds\,\lambda(dx)$.
*   If $H$ is a bounded [predictable process](@entry_id:274260), the integral process $M_t$ is a true **[martingale](@entry_id:146036)**.

### Application: The Lévy-Itô Decomposition

The machinery of Poisson random measures and their compensation culminates in one of the most profound results in the theory of stochastic processes: the **Lévy-Itô decomposition**. This theorem states that any Lévy process—a process with stationary and [independent increments](@entry_id:262163)—can be decomposed into three independent parts: a linear drift, a Brownian motion, and a pure [jump process](@entry_id:201473) built from a Poisson random measure.

Let $X_t$ be a Lévy process with [characteristic triplet](@entry_id:635937) $(b, \sigma^2, \nu)$, where $b$ is a drift constant, $\sigma^2$ is the variance of the continuous Gaussian part, and $\nu$ is the Lévy measure governing the intensity and size of the jumps. The Lévy-Itô decomposition theorem gives a pathwise representation of $X_t$ as [@problem_id:3070074]:
$$ X_t = bt + \sigma W_t + \int_0^t \int_{|x|1} x \, \tilde{N}(ds, dx) + \int_0^t \int_{|x|\ge 1} x \, N(ds, dx) $$
Here, $W_t$ is a standard Brownian motion and $N$ is a PRM on $\mathbb{R}_+ \times (\mathbb{R} \setminus \{0\})$ with intensity measure $ds\,\nu(dx)$. $\tilde{N}$ is its compensated version.

This decomposition is remarkably insightful:
1.  **Drift and Diffusion**: The terms $bt + \sigma W_t$ represent the continuous part of the process, familiar from Brownian motion with drift.
2.  **Large Jumps**: The integral $\int_0^t \int_{|x|\ge 1} x \, N(ds, dx)$ is a sum over the "large" jumps (those with absolute value $\ge 1$). The condition on a Lévy measure ensures that $\nu(\{x : |x| \ge 1\})  \infty$, meaning large jumps occur at a finite rate. Their sum forms a compound Poisson process, which converges without needing compensation.
3.  **Small Jumps**: The integral $\int_0^t \int_{|x|1} x \, \tilde{N}(ds, dx)$ represents the contribution from "small" jumps. The rate of small jumps can be infinite, but the condition $\int_{|x|1} x^2 \nu(dx)  \infty$ ensures that their sum converges after compensation. This integral is a pure-jump martingale.

The Lévy-Itô decomposition reveals that the complex behavior of any process with [stationary independent increments](@entry_id:635556) can be constructed from just three fundamental building blocks: a deterministic drift, a [continuous martingale](@entry_id:185466) (Brownian motion), and a discontinuous martingale built from a compensated Poisson random measure. This powerful result underscores the central importance of PRMs and the principle of compensation in modern [stochastic analysis](@entry_id:188809).