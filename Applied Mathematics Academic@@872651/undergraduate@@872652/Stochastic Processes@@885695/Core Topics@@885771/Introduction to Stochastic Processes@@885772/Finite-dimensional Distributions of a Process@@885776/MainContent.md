## Introduction
Stochastic processes, which model systems evolving randomly over time, are fundamental tools in science and engineering. But how can we move beyond an intuitive idea to a precise mathematical description of such a process? The answer lies in a powerful and unifying concept that forms the bedrock of the entire theory. This article addresses the core problem of rigorously defining a [stochastic process](@entry_id:159502). It demonstrates that the complete probabilistic identity of any process, no matter how complex, is captured by its collection of **[finite-dimensional distributions](@entry_id:197042) (fidis)**.

Throughout the following chapters, you will gain a comprehensive understanding of this foundational concept. The first chapter, **"Principles and Mechanisms"**, will formally introduce fidis and the crucial [consistency conditions](@entry_id:637057) they must satisfy, as established by the Kolmogorov Extension Theorem. Building on this theoretical base, the second chapter, **"Applications and Interdisciplinary Connections"**, will showcase how these principles are used to model real-world phenomena in fields ranging from finance to [population genetics](@entry_id:146344). Finally, **"Hands-On Practices"** will provide targeted exercises to solidify your ability to work with and derive these distributions. We begin by delving into the core principles that govern the construction and validity of these essential distributional building blocks.

## Principles and Mechanisms

A stochastic process, denoted $\{X_t\}_{t \in T}$, is a family of random variables indexed by a set $T$, which typically represents time. While the introduction has provided a general overview, this chapter delves into the fundamental question of how one can mathematically define and specify a stochastic process. The complete probabilistic description of a process is contained within its collection of **[finite-dimensional distributions](@entry_id:197042)**, often abbreviated as **fidis**.

The [finite-dimensional distributions](@entry_id:197042) of a process are the set of all possible [joint probability](@entry_id:266356) distributions for the random variables $X_t$ evaluated at any finite collection of time points. That is, for any integer $n \ge 1$ and any choice of time points $t_1, t_2, \dots, t_n$ from the [index set](@entry_id:268489) $T$, the fidis include the [joint distribution](@entry_id:204390) of the random vector $(X_{t_1}, X_{t_2}, \dots, X_{t_n})$. This [joint distribution](@entry_id:204390) can be specified by a [joint cumulative distribution function](@entry_id:262093) (CDF), a [joint probability mass function](@entry_id:184238) (PMF) in the discrete case, or a [joint probability density function](@entry_id:177840) (PDF) in the continuous case. The collection of these distributions for all possible [finite sets](@entry_id:145527) of time points constitutes the complete probabilistic blueprint of the process.

### The Consistency Conditions

A natural question arises: can any arbitrary collection of joint distributions be designated as the fidis of a stochastic process? The answer is no. For a family of distributions to be valid, they must satisfy certain [self-consistency](@entry_id:160889) requirements. These are formalized by the **Kolmogorov Extension Theorem**, which guarantees the existence of a [stochastic process](@entry_id:159502) with a given family of fidis, provided two conditions are met:

1.  **Permutation Invariance**: The [joint distribution](@entry_id:204390) must be invariant under reordering of the time points. For any permutation $\pi$ of $\{1, 2, \dots, n\}$, the distribution of $(X_{t_1}, \dots, X_{t_n})$ must be the same as the distribution of $(X_{t_{\pi(1)}}, \dots, X_{t_{\pi(n)}})$. This is a natural property of any multivariate random variable.

2.  **Projection Consistency (or Marginalization Consistency)**: The distributions for different sets of time points must be compatible with each other. Specifically, if we have the joint distribution for $(X_{t_1}, \dots, X_{t_n})$, and we marginalize out the last $n-m$ variables (where $m  n$), the resulting [marginal distribution](@entry_id:264862) for $(X_{t_1}, \dots, X_{t_m})$ must be precisely the one specified in our family of fidis for this smaller set of time points.

A particularly important manifestation of the projection consistency condition is the **Chapman-Kolmogorov equation**, which is fundamental to the theory of Markov processes. Consider a time-homogeneous process where the [transition probabilities](@entry_id:158294) $p_{ij}(\tau) = P(X_{t+\tau}=j | X_t=i)$ depend only on the [time lag](@entry_id:267112) $\tau$. To get from state $i$ to state $k$ in time $s+t$, the process must pass through some intermediate state $j$ at time $s$. Summing over all possible intermediate states yields the Chapman-Kolmogorov equation. In matrix form, if $P(\tau)$ is the matrix of transition probabilities $p_{ij}(\tau)$, the equation states:

$P(s+t) = P(s)P(t)$ for all $s, t > 0$.

This shows that the transition matrices must form a semigroup under [matrix multiplication](@entry_id:156035). Let's examine this condition with a concrete model [@problem_id:1302847]. Suppose a [bistable memory](@entry_id:178344) cell has two states, $\{0, 1\}$, and the probability of flipping state in a time interval $\tau$ is the same for both states: $p_{01}(\tau) = p_{10}(\tau) = g(\tau)$. Consequently, the probability of not flipping is $p_{00}(\tau) = p_{11}(\tau) = 1 - g(\tau)$. The transition matrix is:
$$
P(\tau) = \begin{pmatrix} 1-g(\tau)  g(\tau) \\ g(\tau)  1-g(\tau) \end{pmatrix}
$$
For this to define a valid process, $P(\tau)$ must satisfy the Chapman-Kolmogorov equation. Let's test the product $P(s)P(t)$:
$$
P(s)P(t) = \begin{pmatrix} 1-g(s)  g(s) \\ g(s)  1-g(s) \end{pmatrix} \begin{pmatrix} 1-g(t)  g(t) \\ g(t)  1-g(t) \end{pmatrix}
$$
$$
= \begin{pmatrix} (1-g(s))(1-g(t)) + g(s)g(t)  (1-g(s))g(t) + g(s)(1-g(t)) \\ g(s)(1-g(t)) + (1-g(s))g(t)  g(s)g(t) + (1-g(s))(1-g(t)) \end{pmatrix}
$$
Simplifying the entries gives:
$$
P(s)P(t) = \begin{pmatrix} 1 - g(s) - g(t) + 2g(s)g(t)  g(s)+g(t)-2g(s)g(t) \\ g(s)+g(t)-2g(s)g(t)  1 - g(s) - g(t) + 2g(s)g(t) \end{pmatrix}
$$
For this matrix to equal $P(s+t)$, we must have $g(s+t) = g(s) + g(t) - 2g(s)g(t)$. This is a [functional equation](@entry_id:176587) that $g(\tau)$ must satisfy. If we define a helper function $h(\tau) = 1 - 2g(\tau)$, the equation simplifies to the multiplicative Cauchy functional equation: $h(s+t) = h(s)h(t)$. The only continuous, non-trivial solution to this is an exponential function, $h(\tau) = \exp(-\lambda \tau)$ for some constant $\lambda$. This implies $1 - 2g(\tau) = \exp(-\lambda \tau)$, which gives $g(\tau) = \frac{1}{2}(1 - \exp(-\lambda \tau))$. Other functional forms, such as $g(\tau) = \frac{1}{2}(1 - \exp(-\lambda \tau^2))$ or $g(\tau) = \sin^2(\omega \tau)$, fail this consistency test. This example powerfully illustrates that the fidis cannot be chosen arbitrarily; they must adhere to strict mathematical constraints.

### Constructing and Characterizing Processes

The remainder of this chapter explores how [finite-dimensional distributions](@entry_id:197042) are defined and derived for several major classes of stochastic processes. We will see that the structure of the process dictates the method for finding its fidis.

#### Processes from Underlying Independent Variables

The simplest processes are built from a sequence of independent and identically distributed (i.i.d.) random variables. However, more complex processes with dependent structures can also be constructed from such sequences.

Consider a process $\{X_n\}_{n=1}^{\infty}$ where each $X_n$ is a function of an underlying sequence of i.i.d. variables $\{Z_n\}_{n=1}^{\infty}$. For instance, let each $Z_i$ be drawn from a Uniform$[0,1]$ distribution, and define the process as the running maximum of a scaled sequence [@problem_id:1302878]:
$$
X_n = \max\left(\frac{Z_1}{1}, \frac{Z_2}{2}, \frac{Z_3}{3}, \dots, \frac{Z_n}{n}\right)
$$
To find the one-dimensional CDF, $F_{X_n}(x) = P(X_n \le x)$, we use a key property of the maximum function. The maximum of a set of numbers is less than or equal to $x$ if and only if every number in the set is less than or equal to $x$. Because the $Z_i$ are independent, so are the scaled variables $Y_i = Z_i/i$. Therefore,
$$
F_{X_n}(x) = P\left(\max_{1 \le i \le n} Y_i \le x\right) = P(Y_1 \le x, Y_2 \le x, \dots, Y_n \le x) = \prod_{i=1}^{n} P(Y_i \le x)
$$
We can find each individual probability: $P(Y_i \le x) = P(Z_i/i \le x) = P(Z_i \le ix)$. Since $Z_i$ is Uniform$[0,1]$, its CDF is $F_Z(t) = 0$ for $t \le 0$, $t$ for $0  t  1$, and $1$ for $t \ge 1$. This can be written compactly as $F_Z(t) = \min(1, \max(0, t))$. Substituting this, we get the one-dimensional CDF of our process:
$$
F_{X_n}(x) = \prod_{i=1}^{n} \min(1, \max(0, ix))
$$
This expression fully defines the distribution of $X_n$ for any $n$. Although the underlying components are independent, the process $\{X_n\}$ itself exhibits dependence; for example, $X_{n+1}$ is guaranteed to be greater than or equal to $X_n$.

In a more profound example, an entire infinite sequence of [i.i.d. random variables](@entry_id:263216) can be generated from just a single source of randomness. Consider a random variable $U$ drawn uniformly from $[0,1]$ and its binary expansion, $U = 0.B_1B_2B_3\dots = \sum_{n=1}^\infty B_n 2^{-n}$, where each $B_n$ is a binary digit (0 or 1). We can define a [stochastic process](@entry_id:159502) by setting $X_n = B_n$ [@problem_id:1302865]. What is the joint distribution of $(X_1, X_2, X_3)$? The event $\{X_1=i, X_2=j, X_3=k\}$ corresponds to the set of numbers $U$ whose binary expansion begins with $0.ijk\dots$. These numbers fall into the interval $[\frac{i}{2} + \frac{j}{4} + \frac{k}{8}, \frac{i}{2} + \frac{j}{4} + \frac{k}{8} + \frac{1}{8})$. Since $U$ is uniform on $[0,1]$, the probability of this event is simply the length of this interval, which is $1/8$. This holds for any of the $2^3=8$ possible combinations of $(i,j,k) \in \{0,1\}^3$. Therefore, the joint PMF is $p(i,j,k) = 1/8$. This means $X_1, X_2, X_3$ are independent Bernoulli random variables with success probability $1/2$. By extension, the entire sequence $\{X_n\}$ consists of i.i.d. Bernoulli(1/2) variables, all encoded within a single uniform random number.

#### Gaussian Processes

A particularly important class of processes is the **Gaussian process**. A process $\{X_t\}$ is called Gaussian if for any finite set of time points $(t_1, \dots, t_n)$, the random vector $(X_{t_1}, \dots, X_{t_n})$ has a multivariate normal (Gaussian) distribution. This definition has a powerful consequence: the entire family of fidis is completely determined by two functions:
1.  The **mean function**: $\mu(t) = E[X_t]$
2.  The **[autocovariance function](@entry_id:262114)**: $C(s, t) = \text{Cov}(X_s, X_t)$

Once $\mu(t)$ and $C(s,t)$ are specified, the PDF for any $(X_{t_1}, \dots, X_{t_n})$ is given by the multivariate normal PDF with [mean vector](@entry_id:266544) $\boldsymbol{\mu} = (\mu(t_1), \dots, \mu(t_n))^\top$ and covariance matrix $\boldsymbol{\Sigma}$ with entries $\Sigma_{ij} = C(t_i, t_j)$.

For example, consider a stationary Gaussian process with mean zero, $\mu(t)=0$, and an [autocovariance function](@entry_id:262114) that depends only on the time lag $\tau = |s-t|$, given by $C(\tau) = \max(0, 1 - |\tau|)$ [@problem_id:1302864]. To find the joint PDF of $(X_1, X_2)$ representing the process at times $t=2.0$ and $t=2.5$, we first determine the parameters of the [bivariate normal distribution](@entry_id:165129). The [mean vector](@entry_id:266544) is $(0,0)^\top$. The time lag is $\tau = |2.5 - 2.0| = 0.5$. The covariance matrix is:
$$
\boldsymbol{\Sigma} = \begin{pmatrix} C(0)  C(0.5) \\ C(0.5)  C(0) \end{pmatrix} = \begin{pmatrix} 1  1/2 \\ 1/2  1 \end{pmatrix}
$$
The determinant is $\det(\boldsymbol{\Sigma}) = 1 - (1/2)^2 = 3/4$, and the inverse is $\boldsymbol{\Sigma}^{-1} = \frac{4}{3}\begin{pmatrix} 1  -1/2 \\ -1/2  1 \end{pmatrix}$. The joint PDF $f(x_1, x_2)$ is then given by the standard formula:
$$
f(x_1, x_2) = \frac{1}{2\pi\sqrt{\det(\boldsymbol{\Sigma})}} \exp\left(-\frac{1}{2}\mathbf{x}^\top \boldsymbol{\Sigma}^{-1} \mathbf{x}\right) = \frac{1}{\pi\sqrt{3}} \exp\left(-\frac{2}{3}(x_1^2 - x_1 x_2 + x_2^2)\right)
$$
This demonstrates how the abstract mean and covariance functions directly yield concrete joint distributions.

Gaussian processes can also arise constructively. A fundamental property is that any [linear transformation](@entry_id:143080) of Gaussian random variables results in another Gaussian random variable. For instance, consider a random signal modeled by $X_t = A \cos(t) + B \sin(t)$, where $A$ and $B$ are i.i.d. standard normal random variables, $A, B \sim \mathcal{N}(0, 1)$ [@problem_id:1302900]. For any set of times $(t_1, \dots, t_n)$, the vector $(X_{t_1}, \dots, X_{t_n})$ is a [linear transformation](@entry_id:143080) of the Gaussian vector $(A, B)^\top$. Thus, $\{X_t\}$ is a Gaussian process. Let's find its mean and covariance functions. The mean is $E[X_t] = E[A]\cos(t) + E[B]\sin(t) = 0$. The [autocovariance](@entry_id:270483) is:
$$
C(t_1, t_2) = E[X_{t_1} X_{t_2}] = E[(A\cos(t_1) + B\sin(t_1))(A\cos(t_2) + B\sin(t_2))]
$$
Expanding this and using $E[A^2]=1$, $E[B^2]=1$, and $E[AB]=0$ (due to independence) gives:
$$
C(t_1, t_2) = \cos(t_1)\cos(t_2) + \sin(t_1)\sin(t_2) = \cos(t_1 - t_2)
$$
The covariance depends only on the [time lag](@entry_id:267112) $t_1 - t_2$, so the process is (wide-sense) stationary. The joint PDF of $(X_{t_1}, X_{t_2})$ is that of a bivariate normal with mean zero and covariance matrix $\boldsymbol{\Sigma} = \begin{pmatrix} 1  \cos(t_1-t_2) \\ \cos(t_1-t_2)  1 \end{pmatrix}$.

Another common constructive method is through [recurrence relations](@entry_id:276612). Consider the first-order [autoregressive model](@entry_id:270481), AR(1), defined by $X_n = \frac{1}{2}X_{n-1} + Z_n$ for $n \ge 1$, with $X_0=0$ and $\{Z_n\}$ being i.i.d. $\mathcal{N}(0,1)$ noise terms [@problem_id:1302880]. By repeatedly substituting, we can express any $X_n$ as a linear combination of the Gaussian variables $Z_1, \dots, Z_n$. For example:
$$
X_1 = Z_1
$$
$$
X_3 = \frac{1}{2}X_2 + Z_3 = \frac{1}{2}\left(\frac{1}{2}X_1 + Z_2\right) + Z_3 = \frac{1}{4}Z_1 + \frac{1}{2}Z_2 + Z_3
$$
Since $(X_1, X_3)$ are [linear combinations](@entry_id:154743) of $(Z_1, Z_2, Z_3)$, they are jointly Gaussian with mean zero. We can compute their covariance matrix:
$\text{Var}(X_1) = \text{Var}(Z_1) = 1$.
$\text{Var}(X_3) = \text{Var}(\frac{1}{4}Z_1 + \frac{1}{2}Z_2 + Z_3) = (\frac{1}{4})^2\text{Var}(Z_1) + (\frac{1}{2})^2\text{Var}(Z_2) + 1^2\text{Var}(Z_3) = \frac{1}{16} + \frac{4}{16} + \frac{16}{16} = \frac{21}{16}$.
$\text{Cov}(X_1, X_3) = \text{Cov}(Z_1, \frac{1}{4}Z_1 + \frac{1}{2}Z_2 + Z_3) = \frac{1}{4}\text{Var}(Z_1) = \frac{1}{4}$.
The covariance matrix is $\boldsymbol{\Sigma} = \begin{pmatrix} 1  1/4 \\ 1/4  21/16 \end{pmatrix}$. From this, the joint PDF $f(x_1, x_3)$ can be derived just as in the previous example, fully characterizing this particular two-dimensional distribution of the process.

#### Markov Processes

For a Markov process, the future is conditionally independent of the past, given the present state. This property drastically simplifies the structure of its [finite-dimensional distributions](@entry_id:197042). For a discrete-time Markov chain $\{X_n\}$, the joint PMF can be factored into a product of an initial distribution and a series of one-step [transition probabilities](@entry_id:158294):
$$
P(X_0=i_0, X_1=i_1, \dots, X_n=i_n) = P(X_0=i_0) P(X_1=i_1|X_0=i_0) \cdots P(X_n=i_n|X_{n-1}=i_{n-1})
$$
This provides a direct recipe for computing any fidi. For example, let's find a two-dimensional distribution for a non-consecutive pair of times [@problem_id:1302888]. Consider a two-state Markov chain modelling a component as "Operational" (State 1) or "Under Repair" (State 2). Let the [transition probabilities](@entry_id:158294) be $p_{11} = 0.8$ and $p_{21} = 0.6$. The transition matrix is $T = \begin{pmatrix} 0.8  0.2 \\ 0.6  0.4 \end{pmatrix}$. If the process starts at $X_0=1$, what is the joint probability $P(X_1=1, X_3=2)$? We use the definition of conditional probability and the Markov property:
$$
P(X_1=1, X_3=2 | X_0=1) = P(X_1=1|X_0=1) P(X_3=2 | X_1=1, X_0=1) = P(X_1=1|X_0=1) P(X_3=2 | X_1=1)
$$
The first term is simply the [one-step transition probability](@entry_id:272678) $T_{11} = 0.8$. The second term is the two-step [transition probability](@entry_id:271680) from state 1 to state 2, as the process effectively "restarts" at time $n=1$. This is the $(1,2)$ entry of the matrix $T^2$:
$$
T^2 = \begin{pmatrix} 0.8  0.2 \\ 0.6  0.4 \end{pmatrix} \begin{pmatrix} 0.8  0.2 \\ 0.6  0.4 \end{pmatrix} = \begin{pmatrix} 0.76  0.24 \\ 0.72  0.28 \end{pmatrix}
$$
So, $P(X_3=2 | X_1=1) = (T^2)_{12} = 0.24$. The desired joint probability is $0.8 \times 0.24 = 0.192$. This calculation highlights how the Markov property allows us to build joint distributions from simpler, time-homogeneous transition probabilities.

#### Processes with Special Structures

For some processes, the most natural characterization is not directly in terms of the fidis of $\{X_t\}$, but in terms of related quantities like inter-arrival times or increments.

The **Poisson process** $\{N(t), t \ge 0\}$ is defined by the property that the number of events in any interval of length $\tau$, $N(t+\tau) - N(t)$, follows a Poisson distribution with mean $\lambda\tau$, and the numbers of events in disjoint intervals are independent. An equivalent characterization is that the inter-arrival times $S_i = T_i - T_{i-1}$ (where $T_n$ is the time of the $n$-th arrival) are i.i.d. exponential random variables with rate $\lambda$. From this, we can derive the fidis of the arrival times themselves [@problem_id:1302881]. Let's find the joint PDF of $(T_1, T_2)$. We have $T_1 = S_1$ and $T_2 = S_1 + S_2$. This is a [linear transformation](@entry_id:143080) from $(S_1, S_2)$ to $(T_1, T_2)$. The joint PDF of the independent exponential variables is $f_{S_1, S_2}(s_1, s_2) = (\lambda \exp(-\lambda s_1))(\lambda \exp(-\lambda s_2)) = \lambda^2 \exp(-\lambda(s_1+s_2))$ for $s_1, s_2 > 0$. Using the [change of variables](@entry_id:141386) formula, with $s_1=t_1$ and $s_2 = t_2 - t_1$, and a Jacobian determinant of 1, we get the joint PDF for the arrival times:
$$
f_{T_1, T_2}(t_1, t_2) = \lambda^2 \exp(-\lambda (t_1 + (t_2 - t_1))) = \lambda^2 \exp(-\lambda t_2)
$$
This density is valid for the region where $s_1>0$ and $s_2>0$, which corresponds to $t_1>0$ and $t_2 - t_1 > 0$, or $0  t_1  t_2$.

Sometimes, we are interested in joint distributions that involve not just the state of the process, but also **functionals of its path**. A classic example is the **[simple symmetric random walk](@entry_id:276749)** $\{S_n\}$ on the integers, starting at $S_0=0$. Let $M_n = \max\{S_0, S_1, \dots, S_n\}$ be the running maximum. What is the [joint probability](@entry_id:266356) $P(S_n=k, M_n=m)$ [@problem_id:1302852]? This requires a more sophisticated combinatorial tool: the **[reflection principle](@entry_id:148504)**. The event $\{S_n=k, M_n=m\}$ is the set of paths that end at $k$ and have a maximum of exactly $m$. This is equivalent to the set of paths that reach level $m$ but never reach level $m+1$. The probability can be calculated as:
$$
P(S_n=k, M_n=m) = P(S_n=k, M_n \ge m) - P(S_n=k, M_n \ge m+1)
$$
For $k \le m$, the [reflection principle](@entry_id:148504) states that the number of paths from $(0,0)$ to $(n,k)$ that touch or cross level $m$ is equal to the number of paths from $(0,0)$ to a reflected endpoint $(n, 2m-k)$. This gives the remarkable identity $P(S_n=k, M_n \ge m) = P(S_n=2m-k)$. Applying this to our formula yields, for $k \le m$:
$$
P(S_n=k, M_n=m) = P(S_n=2m-k) - P(S_n=2(m+1)-k)
$$
For example, to find $P(S_7=1, M_7=3)$, we calculate $P(S_7=2(3)-1) - P(S_7=2(4)-1) = P(S_7=5) - P(S_7=7)$. For a [simple symmetric random walk](@entry_id:276749), $P(S_n=j) = \binom{n}{(n+j)/2} (1/2)^n$. This gives $P(S_7=5) = \binom{7}{6}(1/2)^7 = 7/128$ and $P(S_7=7) = \binom{7}{7}(1/2)^7 = 1/128$. The final probability is $7/128 - 1/128 = 6/128 = 3/64$.

#### Conditionally Independent and Exchangeable Processes

Finally, we consider processes where the random variables are not independent, but their dependence has a specific symmetric structure. A sequence of random variables $\{X_n\}$ is **exchangeable** if its joint distribution is invariant under any permutation of its indices. For any $n$ and any permutation $\pi$, the vector $(X_1, \dots, X_n)$ has the same distribution as $(X_{\pi(1)}, \dots, X_{\pi(n)})$.

A canonical example is the **beta-Bernoulli process** [@problem_id:1302858]. This is a hierarchical model where first, a global success probability $P$ is drawn from a Beta$(\alpha, \beta)$ distribution. Then, conditional on this value $P=p$, a sequence of Bernoulli trials $\{X_n\}$ is generated, where each $X_n$ is independent with success probability $p$. Unconditionally, these trials are not independent. Knowing that $X_1=1$ makes it more likely that $P$ is large, which in turn increases the probability that $X_2=1$.

Let's derive the joint PMF for $(X_1, \dots, X_k)$. Let $s = \sum_{i=1}^k x_i$ be the number of successes in the sequence $(x_1, \dots, x_k)$. Conditional on $P=p$, the probability is $p^s (1-p)^{k-s}$. To find the unconditional probability, we must average over all possible values of $p$, weighted by its PDF:
$$
P(X_1=x_1, \dots, X_k=x_k) = \int_0^1 P(X_1=x_1, \dots, X_k=x_k | P=p) f_P(p) dp
$$
$$
= \int_0^1 p^s(1-p)^{k-s} \frac{p^{\alpha-1}(1-p)^{\beta-1}}{B(\alpha,\beta)} dp = \frac{1}{B(\alpha,\beta)} \int_0^1 p^{\alpha+s-1}(1-p)^{\beta+k-s-1} dp
$$
The integral is, by definition, the Beta function $B(\alpha+s, \beta+k-s)$. So the joint PMF is:
$$
P(X_1=x_1, \dots, X_k=x_k) = \frac{B(\alpha+\sum x_i, \beta+k-\sum x_i)}{B(\alpha,\beta)}
$$
Crucially, this probability depends only on the number of successes, $s$, and not on their specific positions in the sequence. This is the definition of [exchangeability](@entry_id:263314). De Finetti's theorem provides the deep insight that any infinite exchangeable sequence of binary random variables can be represented in this way, as a mixture of i.i.d. Bernoulli trials. This connects the abstract symmetry of [exchangeability](@entry_id:263314) to the concrete mechanism of [conditional independence](@entry_id:262650).

In summary, the family of [finite-dimensional distributions](@entry_id:197042) provides the complete mathematical description of a [stochastic process](@entry_id:159502). The validity of this family rests on fundamental [consistency conditions](@entry_id:637057). The methods for deriving these distributions vary widely with the nature of the process, from direct construction using underlying variables and [combinatorial principles](@entry_id:174121) to the application of defining properties for classes like Gaussian and Markov processes. Understanding these principles and mechanisms is the key to analyzing and applying stochastic models.