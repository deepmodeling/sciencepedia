## Introduction
Many real-world systems, from stock prices to biological populations, do not evolve smoothly but are punctuated by sudden, significant shocks. Classical stochastic calculus, built upon the [continuous paths](@entry_id:187361) of Brownian motion, is insufficient to capture these discontinuous dynamics. This limitation creates a critical knowledge gap, demanding a more robust mathematical framework to model and analyze phenomena characterized by abrupt jumps.

This article provides a comprehensive exploration of [stochastic integration](@entry_id:198356) with respect to jump measures, the definitive tool for handling such processes. By mastering this theory, you will gain the ability to construct and interpret sophisticated models that reflect the discontinuous nature of reality. The journey is structured into three progressive chapters. First, **"Principles and Mechanisms"** will lay the theoretical groundwork, introducing the Poisson random measure, the concept of compensation, the construction of the stochastic integral, and its fundamental properties. Next, **"Applications and Interdisciplinary Connections"** will demonstrate the power of this framework by exploring its use in [mathematical finance](@entry_id:187074), [population ecology](@entry_id:142920), and [statistical physics](@entry_id:142945), highlighting its role in solving real-world problems. Finally, **"Hands-On Practices"** will provide practical exercises to solidify your understanding of these core concepts, allowing you to apply the theory directly.

## Principles and Mechanisms

This chapter delineates the foundational principles and mechanisms of [stochastic integration](@entry_id:198356) with respect to jump measures. We begin by formally defining the Poisson random measure, which serves as the fundamental building block for modeling discontinuous processes. Subsequently, we introduce the concept of compensation, a crucial technique for constructing martingale measures from these processes. With these tools in place, we will systematically build the theory of [stochastic integration](@entry_id:198356), defining the integral for a broad class of processes and exploring its most important properties, including the Itô isometry and quadratic variation. Finally, we will apply this framework to the [canonical decomposition](@entry_id:634116) of general [jump processes](@entry_id:180953), elucidating the critical role of truncation in handling processes with infinite activity.

### The Poisson Random Measure

The mathematical object at the heart of pure-[jump processes](@entry_id:180953) is the **Poisson random measure (PRM)**, also known as a Poisson point process. It provides a rigorous way to model the occurrence of random events scattered across time and some abstract space of "marks" or "characteristics".

Let $(E, \mathcal{E})$ be a [measurable space](@entry_id:147379), which we will call the **mark space**. The marks can represent various features of a jump, such as its size, direction, or type. The state space for our random measure will be the product space $(0, \infty) \times E$, representing time and mark respectively.

A random measure $N$ on $(0, \infty) \times E$ is defined as a **Poisson random measure** with **intensity measure** $\mu$ if it satisfies two fundamental properties:

1.  **Poisson Distribution**: For any measurable set $A \subset (0, \infty) \times E$ with finite intensity $\mu(A)  \infty$, the random variable $N(A)$, which counts the number of points in $A$, follows a Poisson distribution with mean $\mu(A)$. That is,
    $P(N(A) = k) = \exp(-\mu(A)) \frac{(\mu(A))^k}{k!}$ for $k = 0, 1, 2, \dots$.

2.  **Independent Increments**: For any finite collection of disjoint [measurable sets](@entry_id:159173) $A_1, A_2, \dots, A_n$ in $(0, \infty) \times E$, the random variables $N(A_1), N(A_2), \dots, N(A_n)$ are mutually independent. [@problem_id:2997828]

The intensity measure $\mu$ governs the expected density of points. A particularly important and common case is when the intensity measure is a [product measure](@entry_id:136592). In the **time-homogeneous case**, the intensity is given by $\mu(dt, dx) = dt \otimes \nu(dx)$, where $dt$ denotes the Lebesgue measure on $(0, \infty)$ and $\nu$ is a $\sigma$-[finite measure](@entry_id:204764) on the mark space $(E, \mathcal{E})$. The measure $\nu$ is often called the **Lévy measure** of the process, and it controls the intensity of jumps with different marks.

The structure of a PRM can be better understood through its properties as a marked point process [@problem_id:2997790]. Consider a PRM with a homogeneous intensity measure $dt \otimes \nu(dx)$.

-   If the total mass of the mark space is finite, i.e., $0  \nu(E)  \infty$, the structure is particularly simple. The projection of the random points onto the time axis, defined by the process $N_t(E) = N((0, t] \times E)$, forms a standard homogeneous Poisson process with rate $\nu(E)$. The times of the jumps $T_1, T_2, \dots$ occur with this rate. Conditional on these jump times, the corresponding marks $X_1, X_2, \dots$ are [independent and identically distributed](@entry_id:169067) (i.i.d.) random variables drawn from the probability measure $\nu(\cdot)/\nu(E)$. Furthermore, the sequence of marks is independent of the sequence of jump times.

-   A powerful property known as "thinning" allows us to analyze subsets of jumps. For any [measurable set](@entry_id:263324) of marks $B \in \mathcal{E}$ with $0  \nu(B)  \infty$, the process that counts only the jumps whose marks fall in $B$, given by $N_t(B) = N((0, t] \times B)$, is itself a homogeneous Poisson process with rate $\nu(B)$. [@problem_id:2997790]

-   Another fundamental result concerns the [conditional distribution](@entry_id:138367) of points. If we know that exactly $n$ jumps have occurred in the time interval $(0, t]$, i.e., $N((0, t] \times E) = n$, then the unordered locations of these $n$ jumps are distributed as $n$ [i.i.d. random variables](@entry_id:263216) on the set $(0, t] \times E$. The distribution of each point is the normalized intensity measure $\mu(\cdot)/\mu((0, t] \times E)$. In the homogeneous case, this means the $n$ jump times are i.i.d. and uniformly distributed on $(0, t]$, while the $n$ marks are i.i.d. with distribution $\nu(\cdot)/\nu(E)$, and the times are independent of the marks. [@problem_id:2997790]

-   In the **non-homogeneous case**, the intensity may depend on time, $\mu(dt, dx) = \lambda(t, x) \,dx\,dt$. The counting process $N_t(B) = N((0, t] \times B)$ for a mark set $B$ will have [independent increments](@entry_id:262163), but these increments are no longer stationary, as their distribution depends on the specific time interval. Such a process is a non-homogeneous Poisson process. A remarkable result, the **[time-change theorem](@entry_id:261062)**, states that any such non-homogeneous process can be transformed into a standard (unit rate) homogeneous Poisson process by rescaling time according to its cumulative intensity function. [@problem_id:2997828]

### The Compensated Poisson Random Measure

A PRM $N$ has a non-zero expectation, $\mathbb{E}[N(A)] = \mu(A)$, which reflects a systematic trend or drift. For the purposes of constructing [martingales](@entry_id:267779)—processes with no predictable trend—it is essential to remove this drift. This is achieved through compensation.

Given a PRM $N$ with intensity measure $\mu$, its **compensated Poisson random measure**, denoted $\tilde{N}$, is defined as:
$$
\tilde{N}(dt, dx) := N(dt, dx) - \mu(dt, dx)
$$
This should be understood as a [signed measure](@entry_id:160822)-valued object. For any set $A$ where $\mu(A)  \infty$, the random variable $\tilde{N}(A) = N(A) - \mu(A)$ has an expectation of zero. More profoundly, $\tilde{N}$ represents the "surprise" or innovation in the process: it is the actual number of jumps minus their expected number. The process of integrating against $\tilde{N}$ will, as we will see, yield martingales.

### Construction of the Stochastic Integral

Stochastic integration with respect to a jump measure allows us to construct new processes by summing the effects of jumps, where the contribution of each jump is determined by an **integrand** process. The construction proceeds in stages, starting with the simplest integrands and extending to a general class.

#### Predictability: The Right Class of Integrands

A crucial requirement for the integrand process is that it must be **predictable**. Intuitively, this means that the value of the integrand just before a jump at time $t$ must be known based on information available strictly before $t$. This property prevents one from "seeing into the future" and ensures that the resulting [compensated integral](@entry_id:181695) has the desired [martingale property](@entry_id:261270).

Formally, consider a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \ge 0}, \mathbb{P})$. The **predictable $\sigma$-algebra** $\mathcal{P}$ on $\Omega \times (0, \infty)$ is the $\sigma$-algebra generated by all [adapted processes](@entry_id:187710) with left-continuous [sample paths](@entry_id:184367). Equivalently, it is generated by sets of the form $A \times (s, t]$ where $0 \le s  t$ and $A \in \mathcal{F}_s$. An integrand process $H(\omega, t, x)$ defined on $\Omega \times (0, \infty) \times E$ is called predictable if it is measurable with respect to the product $\sigma$-algebra $\mathcal{P} \otimes \mathcal{E}$. [@problem_id:2997806]

It is important to distinguish $\mathcal{P}$ from the **optional $\sigma$-algebra** $\mathcal{O}$, which is generated by all [adapted processes](@entry_id:187710) with right-[continuous paths](@entry_id:187361). In general, $\mathcal{P} \subset \mathcal{O}$. While optional integrands are sufficient to define an integral with respect to the raw measure $N$ that yields an [adapted process](@entry_id:196563), the stronger condition of predictability is required to ensure that integration against the compensated measure $\tilde{N}$ yields a [local martingale](@entry_id:203733). [@problem_id:2997806]

#### Integration of Simple Predictable Processes

The construction begins with **simple [predictable processes](@entry_id:262945)**, which are finite [linear combinations](@entry_id:154743) of elementary [predictable processes](@entry_id:262945). An elementary [predictable process](@entry_id:274260) has the form
$H(\omega, t, x) = \xi(\omega) \mathbf{1}_{(s, u]}(t) \mathbf{1}_{B}(x)$, where $\xi$ is an $\mathcal{F}_s$-measurable random variable, $(s, u]$ is a time interval, and $B$ is a set of marks.

For such a simple process $H$, the stochastic integrals are defined by linearity as the natural weighted sum of the measures of the corresponding sets [@problem_id:2997789]:
$$
\int_0^T \int_E H \, dN := \sum_{k=1}^n \xi_k N((s_k, u_k] \times B_k)
$$
$$
\int_0^T \int_E H \, d\tilde{N} := \sum_{k=1}^n \xi_k \tilde{N}((s_k, u_k] \times B_k) = \sum_{k=1}^n \xi_k \left( N((s_k, u_k] \times B_k) - \mu((s_k, u_k] \times B_k) \right)
$$
These definitions are the foundation upon which the entire theory is built.

#### Extension to General Processes and the Itô Isometry

The definition of the integral is extended from simple processes to a much larger class of general [predictable processes](@entry_id:262945) using an approximation procedure. This extension is most naturally carried out in an $L^2$ framework, which relies on the **Itô isometry**.

The Itô [isometry](@entry_id:150881) establishes a fundamental relationship between the second moment of a [stochastic integral](@entry_id:195087) and the norm of its integrand. For a predictable integrand $H$ and a fixed time horizon $T$, the [isometry](@entry_id:150881) states:
$$
\mathbb{E}\left[ \left| \int_0^T \int_E H(s,x) \, d\tilde{N}(s,x) \right|^2 \right] = \mathbb{E}\left[ \int_0^T \int_E |H(s,x)|^2 \, d\mu(s,x) \right]
$$
This identity is a cornerstone of the theory. It implies that the [stochastic integral](@entry_id:195087) map is an [isometry](@entry_id:150881) from the space of predictable integrands, equipped with the norm $\|H\|^2_{L^2(\mu)} = \mathbb{E}[\int |H|^2 d\mu]$, to the space of square-integrable random variables $L^2(\mathbb{P})$.

The natural condition for the integral with respect to $\tilde{N}$ to be a well-defined square-integrable [martingale](@entry_id:146036) is therefore that the right-hand side of the isometry is finite [@problem_id:2997823]:
$$
\mathbb{E}\left[ \int_0^T \int_E |H(s,x)|^2 \, \mu(dt, dx) \right]  \infty
$$
By Fubini's theorem, this condition can often be equivalently written as $\int_0^T \int_E \mathbb{E}[|H(t,x)|^2] \, \mu(dt, dx)  \infty$. [@problem_id:2997823] The integral for any $H$ satisfying this condition is then defined as the $L^2(\mathbb{P})$ [limit of integrals](@entry_id:141550) of simple functions that approximate $H$.

### Fundamental Properties of the Compensated Integral

Stochastic integrals with respect to the compensated measure $\tilde{N}$ possess several crucial properties that make them central tools in [stochastic analysis](@entry_id:188809).

#### The Martingale Property

The primary purpose of compensation is to create [martingales](@entry_id:267779). For any [predictable process](@entry_id:274260) $H$ satisfying a minimal [integrability condition](@entry_id:160334), the process $M_t$ defined by the stochastic integral
$$
M_t = \int_0^t \int_E H(s,x) \, d\tilde{N}(s,x)
$$
is a **[local martingale](@entry_id:203733)**. The core reason for this is that the integral has zero expectation. For a suitable integrand $H$, we can show from first principles that
$$
\mathbb{E}\left[ \int_0^t \int_E H(s,x) \, d\tilde{N}(s,x) \right] = 0
$$
This is proven by first establishing the result for simple predictable functions, leveraging the independence of increments of the PRM, and then extending to general integrands via an approximation argument (e.g., using the Monotone Convergence Theorem) [@problem_id:2997791]. The term $\mu(dt,dx)$ in the definition of $\tilde{N}$ is precisely the **compensator** that removes the drift from the raw jump integral, resulting in a [martingale](@entry_id:146036).

#### Quadratic Variation

The **[quadratic variation](@entry_id:140680)** of a martingale measures the cumulative size of its squared movements. For [jump processes](@entry_id:180953), two distinct but related notions of quadratic variation are of paramount importance [@problem_id:2997819]. Let $M_t = \int_0^t \int_E H(s,x) \, d\tilde{N}(s,x)$.

1.  **Optional Quadratic Variation $[M,M]_t$**: This process is defined pathwise by the sum of the squares of the jumps of $M$ up to time $t$:
    $$
    [M,M]_t := \sum_{0  s \le t} (\Delta M_s)^2
    $$
    where $\Delta M_s = M_s - M_{s-}$. For the integral $M_t$, a jump occurs at time $s$ if and only if the PRM $N$ has an atom at time $s$. The jump size is $\Delta M_s = \int_E H(s,x) N(\{s\}, dx)$. A careful calculation reveals that the optional [quadratic variation](@entry_id:140680) can be expressed as a stochastic integral with respect to the *uncompensated* measure $N$:
    $$
    [M,M]_t = \int_0^t \int_E H(s,x)^2 \, N(ds,dx)
    $$
    The process $[M,M]_t$ is itself a pure-jump, increasing process. Its paths are random and jump at the same times as the underlying PRM.

2.  **Predictable Quadratic Variation $\langle M \rangle_t$**: This process, also called the "angle bracket," is the unique predictable, increasing process such that $M_t^2 - \langle M \rangle_t$ is a [local martingale](@entry_id:203733). It can be understood as the compensator of the optional quadratic variation. It is given by the integral of $H^2$ against the *intensity measure* $\mu$:
    $$
    \langle M \rangle_t = \int_0^t \int_E H(s,x)^2 \, \mu(ds,dx)
    $$
    In contrast to $[M,M]_t$, the process $\langle M \rangle_t$ is predictable and, if $\mu$ is non-atomic in time, continuous. It represents the "expected" or "predictable" part of the cumulative squared variation. The relationship $\mathbb{E}[[M,M]_t] = \mathbb{E}[\langle M \rangle_t]$ connects the two concepts via expectation. This distinction is fundamental: $[M,M]_t$ represents the realized, random variation, while $\langle M \rangle_t$ represents its predictable counterpart.

### Integrals for Lévy Processes and the Role of Truncation

The framework of [stochastic integration](@entry_id:198356) with respect to a PRM is the natural language for describing **Lévy processes**—[stochastic processes](@entry_id:141566) with stationary and [independent increments](@entry_id:262163). A Lévy process's jumps can be described by a PRM on $(0, \infty) \times (\mathbb{R}^d \setminus \{0\})$ with a time-homogeneous intensity measure $dt \otimes \nu(dx)$, where the **Lévy measure** $\nu$ satisfies the condition:
$$
\int_{\mathbb{R}^d \setminus \{0\}} (1 \wedge |x|^2) \, \nu(dx)  \infty
$$
This condition is a cornerstone of the theory [@problem_id:2997825]. It implies that while the rate of very small jumps can be infinite, it cannot be "too infinite." Specifically, it guarantees two things:
1.  The rate of "large" jumps is finite: $\nu(\{x : |x| > 1\})  \infty$.
2.  The second moment of "small" jumps is finite: $\int_{\{x: |x| \le 1\}} |x|^2 \, \nu(dx)  \infty$.

When a Lévy process has **infinite activity**, meaning $\nu(\mathbb{R}^d \setminus \{0\}) = \infty$, there are infinitely many jumps in any finite time interval. This presents a challenge: how can we meaningfully sum the contributions of infinitely many jumps? The answer lies in **truncation** [@problem_id:2997888]. We split the jumps into "large" and "small" ones.

-   **Large Jumps** (e.g., $|x|>1$): Since their rate is finite, the integral representing their contribution, $\int_0^t \int_{|x|>1} x \, N(ds,dx)$, is a well-defined finite sum over any finite time interval. This process is a **compound Poisson process**. No compensation is needed to define it. [@problem_id:2997888]

-   **Small Jumps** (e.g., $|x|\le1$): The infinite number of jumps in this region means we cannot simply sum them. However, the condition $\int_{|x|\le1} |x|^2 \, \nu(dx)  \infty$ is precisely the $L^2$ [integrability condition](@entry_id:160334) required by the Itô isometry to define the [compensated integral](@entry_id:181695) $M_t = \int_0^t \int_{|x|\le1} x \, \tilde{N}(ds,dx)$ as a square-integrable martingale. The compensation subtracts the divergent mean of the small jumps, leaving a well-defined [martingale](@entry_id:146036) process.

This splitting is formalized using a **truncation function**, which is a bounded, measurable function $\chi: \mathbb{R}^d \to \mathbb{R}^d$ that agrees with the identity near the origin (e.g., $\chi(x)=x$ for $|x|\le 1$) [@problem_id:2997807]. Using such a function, any Lévy process $X_t$ can be decomposed (the **Lévy-Itô decomposition**) into a drift, a Brownian motion part, a compensated small-jump martingale, and an uncompensated large-jump compound Poisson process.

The choice of truncation function (e.g., changing the [cutoff radius](@entry_id:136708) from $1$ to some other value $c$) is a matter of representation; it does not change the law of the process. The intrinsic properties, such as the [continuous martingale](@entry_id:185466) part and the Lévy measure, remain invariant. However, changing the truncation function from $\chi$ to $\chi'$ necessitates an adjustment to the drift characteristic $b_t$ to absorb the change in the compensation. The new drift $b'_t$ is related to the old one by:
$$
b'_t = b_t + \int_{\mathbb{R}^d} (\chi'(x) - \chi(x)) \, \nu(dx)
$$
This transformation rule ensures that the overall process $X_t$ remains unchanged, demonstrating that the decomposition is a powerful but non-unique representation of the process's paths. [@problem_id:2997807]