## Introduction
Many real-world phenomena, from stock market crashes to evolutionary leaps, are not smooth and continuous but are characterized by sudden, sharp movements. Traditional stochastic models based on Brownian motion fall short in capturing these discontinuous jumps, creating a significant knowledge gap in the modeling of complex systems. This article provides a rigorous framework for understanding and applying processes with jump structures.

This comprehensive exploration is structured into three chapters. The first, **Principles and Mechanisms**, builds the mathematical foundation, defining compound Poisson processes from Poisson random measures and developing the specialized stochastic calculus required to analyze them. The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the power of these models in diverse fields, including [quantitative finance](@entry_id:139120), [actuarial science](@entry_id:275028), and evolutionary biology. Finally, **Hands-On Practices** provides a series of problems to solidify your understanding of the theoretical concepts and their implementation. By navigating these sections, you will gain a deep, functional knowledge of [jump processes](@entry_id:180953) and their critical role in modern [stochastic modeling](@entry_id:261612).

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that govern the behavior of processes with discontinuous, jump-like movements. We will begin by constructing the mathematical object that models these random events—the Poisson random measure—and use it to define the compound Poisson process. We will then explore its rich structural properties, from its [characteristic function](@entry_id:141714) to its [path regularity](@entry_id:203771). Subsequently, we will develop the essential tools of stochastic calculus for these processes, including [stochastic integration](@entry_id:198356) and a generalized Itô's formula. Finally, we will extend our analysis to more general [jump processes](@entry_id:180953) and the stochastic differential equations they drive.

### The Poisson Random Measure: A Foundation for Jumps

The simplest model for events occurring randomly in time is the Poisson process, which counts arrivals. However, in many physical, biological, and economic systems, the events themselves possess intrinsic characteristics. An earthquake has a magnitude, an insurance claim has a monetary value, and a stock price jump has a size. To model both the timing and the characteristics of these events, we generalize the Poisson process to the **Poisson Random Measure (PRM)**, also known as a Poisson point process.

A PRM, denoted $N(dt, dx)$, can be visualized as a random scattering of points on a time-space domain, which we take to be $(0, \infty) \times E$, where $E$ is the "mark space" containing all possible jump characteristics. The measure $N(A)$ for a given set $A \subset (0, \infty) \times E$ simply counts the number of random points that have fallen within $A$. The defining property of a PRM is that for any [measurable set](@entry_id:263324) $A$, the random variable $N(A)$ follows a Poisson distribution with a mean given by the **intensity measure** of the set, denoted $\hat{\nu}(A)$. For the processes we consider, this intensity measure takes the form $\hat{\nu}(dt, dx) = dt \, \nu(dx)$, where $\nu$ is a measure on the mark space $E$. This structure reflects the assumption of [stationary increments](@entry_id:263290); the expected number of points in a time interval of length $dt$ with marks in a set $B \subset E$ is given by $dt \cdot \nu(B)$. The measure $\nu$ is called the **Lévy measure** of the process, and it governs the frequency and size distribution of jumps.

A crucial property of a PRM is that the number of points in any two [disjoint sets](@entry_id:154341) are independent random variables. This property is fundamental to many decomposition arguments.

The intensity measure $\nu(dx)dt$ is also known as the **compensator** of the PRM $N(dt, dx)$. In an intuitive sense, it represents the predictable or expected behavior of the random measure. The difference, $\tilde{N}(dt, dx) = N(dt, dx) - \nu(dx)dt$, is the **compensated Poisson random measure**, which we will see is a martingale-valued measure that captures the pure "surprise" or innovation of the process.

To make this concrete, consider a marked point process where jumps occur at the arrival times $\{T_k\}$ of a Poisson process with rate $\lambda > 0$, and each jump has a random size (mark) $\{J_k\}$ drawn independently from a distribution $F$ on $E$. The associated PRM is $N(dt, dx) = \sum_{k \ge 1} \delta_{(T_k, J_k)}(dt, dx)$. The expected number of jumps arriving in a small time interval $[t, t+dt)$ with a mark in a set $B \subset E$ is the probability of a jump occurring, $\lambda dt$, multiplied by the probability that its mark is in $B$, which is $F(B)$. Thus, the intensity is $\lambda F(B) dt$. This implies that the Lévy measure for this process is $\nu(dx) = \lambda F(dx)$. The total expected rate of jumps of any size is $\nu(E) = \lambda F(E) = \lambda$, as expected.

### The Compound Poisson Process

With the PRM as our foundation, we can now formally define a **compound Poisson process (CPP)**. A CPP, $X_t$, is the cumulative sum of all jump marks that have occurred up to time $t$. Using the PRM, this is expressed elegantly as a pathwise integral:
$$
X_t = \int_0^t \int_E x \, N(ds, dx) = \sum_{k: T_k \le t} J_k
$$
This process is the [canonical model](@entry_id:148621) for phenomena where change occurs in discrete, sudden bursts. Its structure is entirely determined by the rate of jumps $\lambda$ and the distribution of jump sizes $F$, which together define the Lévy measure $\nu = \lambda F$. Since the total jump rate $\lambda$ is finite, a CPP is said to be a process of **finite activity**. This means that on any finite time interval $[0, T]$, there are [almost surely](@entry_id:262518) a finite number of jumps.

The key properties of a CPP can be derived directly from this construction.

#### Moments and Characteristic Function

The expectation of any function integrated against the PRM can be found using the compensator, a result often known as Campbell's Theorem. For a [measurable function](@entry_id:141135) $g: E \to \mathbb{R}$, the expectation is given by:
$$
\mathbb{E}\left[ \int_0^t \int_E g(x) \, N(ds, dx) \right] = \int_0^t \int_E g(x) \, \nu(dx) ds = t \int_E g(x) \, \nu(dx)
$$
Setting $g(x)=x$, we find the mean of the CPP: $\mathbb{E}[X_t] = t \int_E x \, \nu(dx) = \lambda t \, \mathbb{E}[J_1]$. The variance and higher moments can be computed similarly. This formula is a cornerstone of our analysis.

The most complete statistical description of a process is its characteristic function. For a $d$-dimensional CPP $X_t$, the characteristic function $\phi_{X_t}(u) = \mathbb{E}[e^{i u \cdot X_t}]$ for $u \in \mathbb{R}^d$ can be derived by conditioning on the number of jumps. This yields the celebrated **Lévy-Khintchine formula** for a CPP:
$$
\mathbb{E}[e^{i u \cdot X_t}] = \exp\left( t \int_E (e^{i u \cdot x} - 1) \, \nu(dx) \right) = \exp\left( \lambda t \int_E (e^{i u \cdot x} - 1) \, F(dx) \right)
$$
This formula uniquely identifies the process through its Lévy measure $\nu$ and provides a powerful analytical tool.

#### Infinitesimal Generator

The evolution of a Markov process can be described by its infinitesimal generator, $\mathcal{L}$, which captures the expected rate of change of a function of the process. For a function $\varphi$, it is defined by $\mathcal{L}\varphi(y) = \lim_{t \to 0^+} t^{-1}(\mathbb{E}[\varphi(X_t)|X_0=y] - \varphi(y))$. For a CPP, in a small time interval $dt$, there is a high probability of no jump, and a small probability $\lambda dt$ of one jump of size $J$. This leads to the generator:
$$
(\mathcal{L}\varphi)(y) = \lambda \int_E [\varphi(y+x) - \varphi(y)] \, F(dx) = \int_E [\varphi(y+x) - \varphi(y)] \, \nu(dx)
$$
This operator is an integro-differential operator that elegantly summarizes the jump dynamics. The process moves from state $y$ to state $y+x$ with an intensity given by the Lévy measure $\nu(dx)$.

### Path Structure and Regularity

The [sample paths](@entry_id:184367) of a CPP are fundamentally discontinuous. Between jump times, the path is constant. At a jump time $T_k$, the path jumps by the value $J_k$. This produces a step-function trajectory. Such paths are described as **càdlàg**, a French acronym for "right-continuous with left limits" (*continu à droite, limites à gauche*).

The regularity of these paths can be characterized more formally. Because a CPP has a finite number of jumps in any finite time interval, its paths have **finite $p$-variation** for any $p>0$. The $p$-variation, $V_p(X;[0,T]) = \sup_{\Pi} \sum_{i} |X_{t_i} - X_{t_{i-1}}|^p$, simplifies for a pure-[jump process](@entry_id:201473) to the sum of the $p$-th powers of the jump magnitudes: $\sum_{k=1}^{N_T} |J_k|^p$. Since $N_T$ is finite a.s., this sum is also finite a.s. This property distinguishes CPPs sharply from processes like Brownian motion, which has infinite $p$-variation for $p \le 2$.

A more refined measure of jump activity is the **Blumenthal-Getoor index**, $\beta$, defined as:
$$
\beta = \inf\left\{ r \ge 0 : \int_{|x| \le 1} |x|^r \, \nu(dx)  \infty \right\}
$$
This index quantifies the prevalence of small jumps. For a CPP, the Lévy measure $\nu$ has finite total mass, $\nu(\mathbb{R}^d) = \lambda  \infty$. This implies that the integral condition is met even for $r=0$, since $\int_{|x| \le 1} |x|^0 \, \nu(dx) = \nu(\{|x| \le 1\}) \le \lambda  \infty$. Consequently, for any compound Poisson process, the Blumenthal-Getoor index is $\beta = 0$. This signifies the lowest possible level of jump activity and is a hallmark of finite-activity processes.

### Stochastic Calculus for Jump Processes

To analyze systems driven by jumps, we need a corresponding calculus. This involves defining integrals with respect to jump measures and developing a suitable chain rule (Itô's formula).

#### Stochastic Integration and Martingales

While the integral with respect to the PRM, $N(dt, dx)$, is a pathwise sum, the integral with respect to the **compensated PRM**, $\tilde{N}(dt, dx) = N(dt, dx) - \nu(dx)dt$, is a true stochastic integral that defines a [martingale](@entry_id:146036). The construction of this integral, $M_t = \int_0^t \int_E H(s, x) \, \tilde{N}(ds, dx)$, requires careful technical considerations. The integrand $H(\omega, s, x)$ must be **predictable**, meaning its value at time $s$ is determined by information available strictly before $s$. Formally, $H$ must be measurable with respect to the **predictable $\sigma$-field**, $\mathcal{P}$, which is generated by left-continuous [adapted processes](@entry_id:187710).

Under suitable [integrability conditions](@entry_id:158502), the resulting process $M_t$ is a [martingale](@entry_id:146036). For example, if the integrand $g(x)$ depends only on the mark, the process $M_t = \int_0^t \int_E g(x) \, \tilde{N}(ds, dx)$ is a square-integrable martingale provided $\int_E g(x)^2 \nu(dx)  \infty$. Its predictable [quadratic variation](@entry_id:140680), which measures the "accumulated variance" of the martingale, is given by a generalized Itô isometry:
$$
\langle M \rangle_t = \mathbb{E}[M_t^2] = \int_0^t \int_E g(x)^2 \nu(dx) ds = t \int_E g(x)^2 \nu(dx)
$$
This formula is the jump-process analogue of the quadratic variation of an integral with respect to Brownian motion. The most general condition for the integral to be a well-defined [local martingale](@entry_id:203733) is that $\int_0^t\int_E (|H(s,x)|^2 \wedge |H(s,x)|) \nu(dx) ds  \infty$ [almost surely](@entry_id:262518).

#### The Multivariate Itô Formula for Jump Processes

The classical Itô's formula for continuous processes must be extended to account for discontinuous jumps. For a twice continuously [differentiable function](@entry_id:144590) $f$ and a general $d$-dimensional càdlàg [semimartingale](@entry_id:188438) $X_t$, the formula is:
$$
f(X_t) = f(X_0) + \int_0^t \nabla f(X_{s-})^\top dX_s + \frac{1}{2} \int_0^t \sum_{i,j=1}^d \partial_{ij} f(X_{s-}) d[X^i, X^j]^c_s + \sum_{0  s \le t} \left( f(X_s) - f(X_{s-}) - \nabla f(X_{s-})^\top \Delta X_s \right)
$$