## Introduction
The world is filled with phenomena that occur in discrete, sudden bursts—a stock price jumping after an announcement, a cell releasing a burst of viral particles, or a customer arriving at a a service counter. While continuous processes like Brownian motion effectively model gradual, random drift, they cannot capture these instantaneous events. The key to modeling such "jump" phenomena lies in the theory of [discrete probability distributions](@entry_id:166565). These mathematical constructs provide the language to quantify uncertainty in countable outcomes, forming the bedrock of stochastic processes that evolve discontinuously.

This article delves into the classical [discrete distributions](@entry_id:193344) that are most fundamental to the study of [stochastic differential equations](@entry_id:146618) (SDEs) with jumps. We will bridge the gap between elementary probability theory and advanced [stochastic calculus](@entry_id:143864) by showing how simple counting distributions evolve into dynamic processes.

The first section, **Principles and Mechanisms**, lays the theoretical groundwork. It begins with the Binomial and Poisson distributions, deriving their properties from first principles and exploring the profound connection between them through the Poisson limit theorem. This section builds progressively towards the concept of the Poisson process and its crucial [martingale](@entry_id:146036) structure, which is essential for its use in SDEs. In the second section, **Applications and Interdisciplinary Connections**, we will see these theories in action, exploring how they are used to model jump-diffusion in finance, analyze [equilibrium states](@entry_id:168134) in queueing theory, conduct [statistical inference](@entry_id:172747) in biology, and compare models using information theory. Finally, the **Hands-On Practices** section will offer concrete exercises to solidify your understanding, guiding you through simulating Poisson-distributed events and estimating their parameters from data. By the end, you will have a robust understanding of how these [discrete distributions](@entry_id:193344) serve as the fundamental building blocks for modeling a wide range of dynamic, real-world systems.

## Principles and Mechanisms

This chapter elucidates the fundamental principles and mechanisms of the classical [discrete distributions](@entry_id:193344) that form the foundation for modeling jump phenomena in [stochastic processes](@entry_id:141566). We begin with the most basic building blocks—the Binomial and Poisson distributions—and progressively construct the more sophisticated concepts essential for stochastic differential equations, including the Poisson process, its [martingale](@entry_id:146036) properties, and the Poisson random measure.

### The Binomial Distribution: Counting Successes in Discrete Trials

The most elementary model of a random event is a trial with only two possible outcomes, conventionally labeled "success" and "failure". Such a trial is modeled by the **Bernoulli distribution**. A random variable $Y$ follows a Bernoulli distribution with parameter $p$, denoted $Y \sim \mathrm{Bernoulli}(p)$, if it takes the value 1 (success) with probability $p$ and the value 0 (failure) with probability $1-p$. From first principles, its [expectation and variance](@entry_id:199481) are readily derived:
$ \mathbb{E}[Y] = 1 \cdot p + 0 \cdot (1-p) = p $
$ \mathrm{Var}(Y) = \mathbb{E}[Y^2] - (\mathbb{E}[Y])^2 = (1^2 \cdot p + 0^2 \cdot (1-p)) - p^2 = p - p^2 = p(1-p) $.

While a single Bernoulli trial is simple, a sequence of such trials provides a rich framework for modeling cumulative events. Consider a sequence of $n$ **independent and identically distributed (i.i.d.)** Bernoulli trials, $Y_1, Y_2, \dots, Y_n$, each with success probability $p$. The total number of successes in this sequence is given by the random variable $X = \sum_{i=1}^n Y_i$. This random variable $X$ is said to follow a **Binomial distribution** with parameters $n$ and $p$, denoted $X \sim \mathrm{Bin}(n,p)$.

The properties of the Binomial distribution can be derived directly from its construction as a sum of Bernoulli trials [@problem_id:3044299]. By the **[linearity of expectation](@entry_id:273513)**, the mean of $X$ is the sum of the individual means:
$$ \mathbb{E}[X] = \mathbb{E}\left[\sum_{i=1}^n Y_i\right] = \sum_{i=1}^n \mathbb{E}[Y_i] = \sum_{i=1}^n p = np $$

Because the trials are independent, the variance of the sum is the sum of the variances:
$$ \mathrm{Var}(X) = \mathrm{Var}\left(\sum_{i=1}^n Y_i\right) = \sum_{i=1}^n \mathrm{Var}(Y_i) = \sum_{i=1}^n p(1-p) = np(1-p) $$
These derivations highlight a powerful principle: decomposing a complex random variable into a sum of simpler, independent components often dramatically simplifies the calculation of its moments.

The **probability [mass function](@entry_id:158970) (PMF)** of the Binomial distribution, which gives the probability of observing exactly $k$ successes, requires a [combinatorial argument](@entry_id:266316) [@problem_id:3044344]. The derivation rests on three pillars:
1.  **Probability of a Single Sequence**: Consider any single sequence of $n$ trials that contains exactly $k$ successes and $n-k$ failures. Because the trials are independent, the probability of this specific sequence occurring is the product of the individual probabilities: $\underbrace{p \cdot p \cdots p}_{k \text{ times}} \cdot \underbrace{(1-p) \cdot (1-p) \cdots (1-p)}_{n-k \text{ times}} = p^k (1-p)^{n-k}$. Critically, because the trials are also identically distributed, every sequence with $k$ successes has this same probability. This property is guaranteed more generally if the sequence of trials is **exchangeable**.

2.  **Counting the Number of Sequences**: The total number of distinct sequences containing exactly $k$ successes is equivalent to the number of ways to choose $k$ positions for the successes out of the $n$ available positions. This is given by the binomial coefficient, $\binom{n}{k} = \frac{n!}{k!(n-k)!}$.

3.  **Total Probability**: Since each of these $\binom{n}{k}$ sequences is a mutually exclusive outcome, the total probability of observing exactly $k$ successes is the sum of their individual probabilities. This simplifies to the product of the number of sequences and the probability of any single sequence.

This reasoning yields the familiar Binomial PMF:
$$ \mathbb{P}(X=k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad \text{for } k \in \{0, 1, \dots, n\} $$

### The Poisson Distribution: Modeling Rare Events

The Poisson distribution is fundamental for modeling the number of events occurring in a fixed interval of time or space when these events happen with a known average rate and independently of the time since the last event. A random variable $X$ follows a **Poisson distribution** with parameter (or rate) $\lambda > 0$, denoted $X \sim \mathrm{Pois}(\lambda)$, if its PMF is given by:
$$ \mathbb{P}(X=k) = \frac{e^{-\lambda} \lambda^k}{k!}, \quad \text{for } k \in \{0, 1, 2, \dots\} $$
The presence of the [factorial](@entry_id:266637) $k!$ and the power $\lambda^k$ is characteristic, and the term $e^{-\lambda}$ ensures that the probabilities sum to 1, as can be seen from the Taylor series expansion for $e^{\lambda} = \sum_{k=0}^{\infty} \frac{\lambda^k}{k!}$.

The mean and variance of the Poisson distribution can be derived from its PMF [@problem_id:3044275]. A key algebraic trick simplifies the summations. For the mean:
$$ \mathbb{E}[X] = \sum_{k=0}^{\infty} k \cdot \frac{e^{-\lambda} \lambda^k}{k!} = \sum_{k=1}^{\infty} k \cdot \frac{e^{-\lambda} \lambda^k}{k!} = \lambda e^{-\lambda} \sum_{k=1}^{\infty} \frac{\lambda^{k-1}}{(k-1)!} $$
Letting $j = k-1$, the sum becomes $\sum_{j=0}^{\infty} \frac{\lambda^j}{j!} = e^{\lambda}$. Thus,
$$ \mathbb{E}[X] = \lambda e^{-\lambda} e^{\lambda} = \lambda $$

A similar approach, often using **[factorial](@entry_id:266637) moments**, is used for the variance. The second factorial moment is $\mathbb{E}[X(X-1)]$. A calculation analogous to the one above reveals that $\mathbb{E}[X(X-1)] = \lambda^2$. From this, we find the variance:
$$ \mathrm{Var}(X) = \mathbb{E}[X^2] - (\mathbb{E}[X])^2 = (\mathbb{E}[X(X-1)] + \mathbb{E}[X]) - (\mathbb{E}[X])^2 = (\lambda^2 + \lambda) - \lambda^2 = \lambda $$
A defining characteristic of the Poisson distribution is that its **mean and variance are equal**.

A more elegant method for computing moments involves **[generating functions](@entry_id:146702)**. The **probability [generating function](@entry_id:152704) (PGF)** of a [discrete random variable](@entry_id:263460) $X$ is $G_X(s) = \mathbb{E}[s^X]$. For $X \sim \mathrm{Pois}(\lambda)$:
$$ G_X(s) = \sum_{k=0}^{\infty} s^k \frac{e^{-\lambda} \lambda^k}{k!} = e^{-\lambda} \sum_{k=0}^{\infty} \frac{(s\lambda)^k}{k!} = e^{-\lambda} e^{s\lambda} = \exp(\lambda(s-1)) $$
Factorial moments can be found by differentiating the PGF and evaluating at $s=1$. For instance, $\mathbb{E}[X(X-1)] = G_X''(1)$. Differentiating our expression for $G_X(s)$ twice gives $G_X''(s) = \lambda^2 \exp(\lambda(s-1))$, so $G_X''(1) = \lambda^2$, confirming our previous result [@problem_id:3044342].

The **[cumulant generating function](@entry_id:149336) (CGF)**, $K_X(t) = \ln \mathbb{E}[e^{tX}]$, is particularly insightful. For a Poisson variable, it is simply the logarithm of the [moment generating function](@entry_id:152148) $M_X(t) = G_X(e^t)$:
$$ K_X(t) = \ln(\exp(\lambda(e^t - 1))) = \lambda(e^t - 1) $$
The CGF's power lies in its additivity for [sums of independent random variables](@entry_id:276090): if $X$ and $Y$ are independent, then $K_{X+Y}(t) = K_X(t) + K_Y(t)$. The simple, clean form of the Poisson CGF is a primary reason for its ubiquity in the theory of [stochastic processes](@entry_id:141566) [@problem_id:3044301].

### The Bridge Between Binomial and Poisson: The Law of Small Numbers

There is a profound connection between the Binomial and Poisson distributions. The Poisson distribution can be viewed as a limiting case of the Binomial distribution in a regime where the number of trials $n$ is very large and the probability of success $p$ is very small. This is known as the **Poisson limit theorem** or the **law of small numbers**.

Formally, if $X_n \sim \mathrm{Bin}(n, p_n)$ and we consider the limit as $n \to \infty$ and $p_n \to 0$ such that the mean $\lambda = np_n$ remains constant, then the distribution of $X_n$ converges to a Poisson distribution with parameter $\lambda$.

We can investigate the quality of this approximation more rigorously. Let's analyze the error in approximating the Binomial probability $\mathbb{P}(X=0) = (1-p)^n$ by the Poisson probability $\mathbb{P}(Z=0) = e^{-\lambda}$, where $\lambda=np$. In the asymptotic regime where $p = \lambda/n$, we have:
$$ (1-p)^n = \left(1 - \frac{\lambda}{n}\right)^n = \exp\left(n \ln\left(1 - \frac{\lambda}{n}\right)\right) $$
Using the Taylor expansion $\ln(1-x) = -x - \frac{x^2}{2} - O(x^3)$ for small $x$, we find:
$$ n \ln\left(1 - \frac{\lambda}{n}\right) = n\left(-\frac{\lambda}{n} - \frac{\lambda^2}{2n^2} - O\left(\frac{1}{n^3}\right)\right) = -\lambda - \frac{\lambda^2}{2n} - O\left(\frac{1}{n^2}\right) $$
Exponentiating this and using the expansion $e^y \approx 1+y$ for small $y$ gives:
$$ \left(1 - \frac{\lambda}{n}\right)^n = e^{-\lambda} \exp\left(-\frac{\lambda^2}{2n} - O\left(\frac{1}{n^2}\right)\right) \approx e^{-\lambda}\left(1 - \frac{\lambda^2}{2n}\right) $$
The [approximation error](@entry_id:138265) $E(n,p) = (1-p)^n - e^{-np}$ therefore has a leading-order term of $-\frac{\lambda^2 e^{-\lambda}}{2n}$ [@problem_id:3044324]. This shows that the error not only vanishes as $n \to \infty$, but it does so at a rate proportional to $1/n$.

A more powerful and non-asymptotic result for quantifying this approximation is **Le Cam's inequality**. It provides an upper bound on the **[total variation distance](@entry_id:143997)** $d_{\mathrm{TV}}$ between the distributions. For a sum $S$ of $n$ independent Bernoulli trials with potentially different probabilities $p_1, \dots, p_n$, and a Poisson random variable $Z$ with mean $\lambda = \sum p_i$, Le Cam's inequality states:
$$ d_{\mathrm{TV}}(\mathcal{L}(S), \mathcal{L}(Z)) \le \sum_{i=1}^n p_i^2 $$
In the specific case of the Binomial distribution where all $p_i = p$, this simplifies to:
$$ d_{\mathrm{TV}}(\mathrm{Bin}(n,p), \mathrm{Pois}(np)) \le np^2 $$
For example, for a process with $n=800$ trials and a small success probability of $p=0.006$, the upper bound on the error is $800 \times (0.006)^2 = 0.0288$. This provides a concrete, practical guarantee on the quality of the Poisson approximation without resorting to limits [@problem_id:3044300].

### From Static Counts to Dynamic Processes: The Poisson Process

The Poisson distribution describes static counts. To model events unfolding in time, we introduce the **homogeneous Poisson process**, $\{N(t)\}_{t \ge 0}$. This is a counting process defined by the following core properties:
1.  $N(0) = 0$.
2.  **Independent Increments**: The number of events in non-overlapping time intervals are [independent random variables](@entry_id:273896). For any $0 \le t_1  t_2 \le t_3  t_4$, the increment $N(t_4) - N(t_3)$ is independent of the increment $N(t_2) - N(t_1)$.
3.  **Stationary Increments**: The distribution of the number of events in an interval depends only on the length of the interval, not its location. For any $s  t$, the increment $N(t) - N(s)$ has the same distribution as $N(t-s)$.
4.  **Poisson-distributed Increments**: For any $t > s \ge 0$, the number of events in the interval $(s, t]$, $N(t) - N(s)$, follows a Poisson distribution with parameter $\lambda(t-s)$.

The properties of the Poisson process can be elegantly explored using the CGF. Let's find the CGF of an increment $Y = N(t) - N(s)$ for $0 \le s  t$. We can write $N(t) = N(s) + (N(t) - N(s))$. Due to [independent increments](@entry_id:262163), the CGF is additive: $K_{N(t)}(u) = K_{N(s)}(u) + K_{N(t)-N(s)}(u)$. Since $N(\tau) \sim \mathrm{Pois}(\lambda \tau)$, we know from our earlier derivation that $K_{N(\tau)}(u) = \lambda \tau (e^u - 1)$. Therefore:
$$ K_{N(t)-N(s)}(u) = K_{N(t)}(u) - K_{N(s)}(u) = \lambda t (e^u - 1) - \lambda s (e^u - 1) = \lambda(t-s)(e^u - 1) $$
This result confirms that the increment $N(t)-N(s)$ follows a Poisson distribution with parameter $\lambda(t-s)$, consistent with the definition of the process [@problem_id:3044301].

The correlation structure of the process is also revealing. Let's compute the covariance $\mathrm{Cov}(N(s), N(t))$ for $s \le t$. We again use the decomposition $N(t) = N(s) + (N(t) - N(s))$:
$$ \mathrm{Cov}(N(s), N(t)) = \mathrm{Cov}(N(s), N(s) + N(t) - N(s)) $$
Using the [bilinearity of covariance](@entry_id:274105):
$$ \mathrm{Cov}(N(s), N(s)) + \mathrm{Cov}(N(s), N(t) - N(s)) = \mathrm{Var}(N(s)) + \mathrm{Cov}(N(s), N(t) - N(s)) $$
Because the increments $N(s)$ and $N(t)-N(s)$ are independent, their covariance is zero. The variance of $N(s) \sim \mathrm{Pois}(\lambda s)$ is $\lambda s$. Thus, for $s \le t$:
$$ \mathrm{Cov}(N(s), N(t)) = \lambda s $$
This result can be generalized for any $s, t \ge 0$ as $\mathrm{Cov}(N(s), N(t)) = \lambda \min(s, t)$. The covariance depends on the length of the common observation time, a direct consequence of the [independent increments](@entry_id:262163) structure [@problem_id:3044305].

### Martingale Structures and Generalizations for Stochastic Calculus

For the Poisson process to be a useful component in stochastic differential equations, it must be integrated into the framework of [martingale theory](@entry_id:266805). The Poisson process $N(t)$ itself is not a martingale, as its expectation $\mathbb{E}[N(t)] = \lambda t$ is not constant. However, we can construct a [martingale](@entry_id:146036) by subtracting this predictable trend. The **compensated Poisson process** is defined as:
$$ M(t) = N(t) - \lambda t $$
This process $M(t)$ is a fundamental **[martingale](@entry_id:146036)** with respect to the [natural filtration](@entry_id:200612) generated by $N(t)$.

In modern stochastic calculus, a key characteristic of a [martingale](@entry_id:146036) is its **quadratic variation**. For a pure-[jump process](@entry_id:201473) like $M(t)$, the [quadratic variation](@entry_id:140680) $[M](t)$ is the sum of its squared jumps up to time $t$. The jumps of $M(t)$ are identical to the jumps of $N(t)$, which are all of size 1. Therefore, the [quadratic variation](@entry_id:140680) is simply the sum of $1^2$ for every jump that occurs:
$$ [M](t) = \sum_{0  s \le t} (\Delta M(s))^2 = \sum_{0  s \le t} (\Delta N(s))^2 = \sum_{0  s \le t} 1^2 = N(t) $$
The quadratic variation of the compensated Poisson process is the Poisson process itself. Note that $[M](t)$ is a random, discontinuous process. This is distinct from the quadratic variation of Brownian motion, which is the deterministic, continuous process $[W](t) = t$.

The theory of [martingales](@entry_id:267779) also defines the **predictable [quadratic variation](@entry_id:140680)**, denoted $\langle M \rangle(t)$. This is the unique, [predictable process](@entry_id:274260) such that $M(t)^2 - \langle M \rangle(t)$ is a [martingale](@entry_id:146036). It can be thought of as the "expected" [quadratic variation](@entry_id:140680) given the information from the past. For the compensated Poisson process, this compensator is precisely the trend we subtracted to create the martingale in the first place:
$$ \langle M \rangle(t) = \lambda t $$
The pair of results, $[M](t) = N(t)$ and $\langle M \rangle(t) = \lambda t$, is central to developing Itô's formula for processes with jumps [@problem_id:3044323].

Two further generalizations are essential for building realistic SDE models.

First, the **compound Poisson process** models scenarios where jump sizes are also random. It is defined as a sum $S(t) = \sum_{i=1}^{N(t)} Y_i$, where $N(t)$ is a Poisson process and $\{Y_i\}$ is an i.i.d. sequence of jump-size random variables, independent of $N(t)$. The moments of $S(t)$ can be found using the laws of total [expectation and variance](@entry_id:199481), conditioning on the number of jumps $N(t)=n$. Let $\mu = \mathbb{E}[Y_1]$ and $\sigma^2 = \mathrm{Var}(Y_1)$. The mean and variance of $S(t)$ are given by:
$$ \mathbb{E}[S(t)] = \mathbb{E}[\mathbb{E}[S(t)|N(t)]] = \mathbb{E}[N(t)\mu] = \mu \mathbb{E}[N(t)] = \lambda t \mu $$
$$ \mathrm{Var}(S(t)) = \mathbb{E}[\mathrm{Var}(S(t)|N(t))] + \mathrm{Var}(\mathbb{E}[S(t)|N(t)]) = \mathbb{E}[N(t)\sigma^2] + \mathrm{Var}(N(t)\mu) = \lambda t \sigma^2 + \lambda t \mu^2 = \lambda t (\sigma^2 + \mu^2) = \lambda t \mathbb{E}[Y_1^2] $$
These results are known as Wald's identity and the Blackwell-Girshick identity, respectively [@problem_id:3044328].

Second, the most powerful generalization is the **Poisson random measure (PRM)**, which provides a unified framework for describing jumps in both time and some other characteristic space (e.g., jump size). Let $(E, \mathcal{E})$ be a space of possible jump marks. A PRM, denoted $\mu(dt, dz)$, is a random [counting measure](@entry_id:188748) on the product space $\mathbb{R}_+ \times E$. It is defined by two properties:
1.  **Distribution**: For any measurable set $A \subset \mathbb{R}_+ \times E$ with finite intensity $\Lambda(A) = \int_A \nu(dz)dt  \infty$, the random count of points $\mu(A)$ follows a Poisson distribution with parameter $\Lambda(A)$. The measure $\nu(dz)$ is called the **Lévy measure** and describes the intensity of jumps of different marks.
2.  **Independence**: The counts on any collection of pairwise [disjoint sets](@entry_id:154341) are independent random variables.

This abstract object seamlessly unifies all the concepts we have discussed. The standard Poisson process $N(t)$ is simply the count of points in the set $[0,t] \times E$, i.e., $N(t) = \mu([0,t] \times E)$, assuming $\nu(E)=\lambda$. A compound Poisson process is an integral with respect to the PRM: $S(t) = \int_0^t \int_E z \, \mu(ds, dz)$. The PRM is the fundamental building block for constructing general Lévy processes and defining the jump part of [stochastic differential equations](@entry_id:146618) [@problem_id:3044309].