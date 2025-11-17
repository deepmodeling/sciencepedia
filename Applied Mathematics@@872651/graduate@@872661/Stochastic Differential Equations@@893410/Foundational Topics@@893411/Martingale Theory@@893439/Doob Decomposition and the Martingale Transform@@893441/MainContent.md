## Introduction
The Doob decomposition and the [martingale transform](@entry_id:182444) are cornerstones of modern probability theory and [stochastic calculus](@entry_id:143864). They provide a powerful lens through which to analyze the intricate structure of stochastic processes. At its heart, this framework addresses a fundamental question: how can we separate the predictable, trending behavior of a process from its purely random, unpredictable innovations? The ability to perform this separation is not just a theoretical elegance; it is the key to building realistic models and solving practical problems in fields ranging from [quantitative finance](@entry_id:139120) to control theory. This article unpacks this foundational theory, showing how any [submartingale](@entry_id:263978)—a process that tends to drift upwards—can be uniquely split into a '[fair game](@entry_id:261127)' (a [martingale](@entry_id:146036)) and a predictable trend (a compensator).

This article is structured to guide you from foundational principles to practical applications. The first chapter, **Principles and Mechanisms**, lays the theoretical groundwork, progressing from the intuitive discrete-time case to the more sophisticated continuous-time Doob-Meyer decomposition, highlighting crucial concepts like predictability and the 'class D' condition. The second chapter, **Applications and Interdisciplinary Connections**, explores the profound impact of this theory, showing how it underpins [asset pricing](@entry_id:144427) in finance, intensity modeling in point process theory, and [state estimation](@entry_id:169668) in filtering. Finally, the **Hands-On Practices** chapter offers a series of targeted problems to solidify your understanding and connect the abstract theory to concrete calculations. We begin by establishing the formal language of information and time needed to define these processes.

## Principles and Mechanisms

This chapter delves into the structural properties of martingales and related processes. We will explore one of the most profound results in the theory of stochastic processes: the decomposition of submartingales into a "pure" [martingale](@entry_id:146036) component and a predictable, trending component. This decomposition, known as the Doob-Meyer decomposition, not only provides deep insight into the structure of these processes but also serves as the foundation for the theory of [stochastic integration](@entry_id:198356) with respect to [semimartingales](@entry_id:184490). We will begin by establishing the fundamental concepts and then build progressively from the discrete-time case to the more general and powerful continuous-time theory.

### Information and Processes in Time

The [mathematical modeling](@entry_id:262517) of information evolving over time is formalized by a **[filtration](@entry_id:162013)**. Given a probability space $(\Omega, \mathcal{F}, \mathbb{P})$, a filtration is a family of sub-$\sigma$-algebras $(\mathcal{F}_t)_{t \ge 0}$ of $\mathcal{F}$ that is non-decreasing: for any $0 \le s \le t$, it must hold that $\mathcal{F}_s \subseteq \mathcal{F}_t$. Intuitively, $\mathcal{F}_t$ represents all the information available up to time $t$. A [stochastic process](@entry_id:159502) $(X_t)_{t \ge 0}$ is said to be **adapted** to this [filtration](@entry_id:162013) if, for every $t \ge 0$, the random variable $X_t$ is $\mathcal{F}_t$-measurable. This means the value of the process at time $t$ is "known" given the information available at time $t$.

For the powerful theorems of continuous-time [stochastic analysis](@entry_id:188809) to hold, it is standard to impose two technical regularity conditions on the filtration, collectively known as the **usual conditions** or **usual hypotheses**. These are:

1.  **Completeness**: The probability space $(\Omega, \mathcal{F}, \mathbb{P})$ is complete (i.e., every subset of a [null set](@entry_id:145219) is measurable), and the initial $\sigma$-algebra $\mathcal{F}_0$ contains all $\mathbb{P}$-[null sets](@entry_id:203073) of $\mathcal{F}$. By the non-decreasing property, this ensures every $\mathcal{F}_t$ contains all [null sets](@entry_id:203073). This condition prevents pathological behaviors related to [sets of measure zero](@entry_id:157694).

2.  **Right-continuity**: The [filtration](@entry_id:162013) is continuous from the right, meaning that for every $t \ge 0$, we have $\mathcal{F}_t = \bigcap_{s>t} \mathcal{F}_s$. This condition essentially states that no new information arrives in an infinitesimally small instant *after* time $t$.

Under these usual conditions, the theoretical framework becomes much more robust. For instance, key processes admit **càdlàg** (right-continuous with left limits) versions, [stopping times](@entry_id:261799) have well-behaved properties, and, most importantly for our purposes, the Doob-Meyer decomposition and the theory of the [martingale transform](@entry_id:182444) are well-defined and powerful [@problem_id:2973593]. Throughout this chapter, we will assume the [filtration](@entry_id:162013) satisfies the usual conditions unless stated otherwise.

### Martingales, Submartingales, and Supermartingales

With the concept of a [filtration](@entry_id:162013) in place, we can define the central objects of our study. A stochastic process $(X_t)_{t \in T}$ (where the time [index set](@entry_id:268489) $T$ can be discrete, like $\mathbb{N}_0$, or continuous, like $\mathbb{R}_+$) is a **[martingale](@entry_id:146036)** with respect to a [filtration](@entry_id:162013) $(\mathcal{F}_t)$ if it satisfies three conditions:

1.  **Adaptedness**: $(X_t)$ is adapted to $(\mathcal{F}_t)$.
2.  **Integrability**: For each $t \in T$, $X_t$ is integrable, i.e., $\mathbb{E}[|X_t|]  \infty$.
3.  **Martingale Property**: For all $s \le t$ in $T$, $\mathbb{E}[X_t \mid \mathcal{F}_s] = X_s$ almost surely.

A [martingale](@entry_id:146036) models a "fair game": the best prediction of its [future value](@entry_id:141018), given the information up to the present, is simply its [present value](@entry_id:141163).

By relaxing the equality in the third condition, we define two related classes of processes. A process $(X_t)$ is a **[submartingale](@entry_id:263978)** if it satisfies the adaptedness and [integrability conditions](@entry_id:158502), but the [martingale property](@entry_id:261270) is replaced by:
$$ \mathbb{E}[X_t \mid \mathcal{F}_s] \ge X_s \quad \text{almost surely, for all } s \le t. $$
A [submartingale](@entry_id:263978) models a "favorable game," where the process is expected to increase or stay the same on average.

Conversely, a process $(X_t)$ is a **[supermartingale](@entry_id:271504)** if it satisfies the adaptedness and [integrability conditions](@entry_id:158502), but the [martingale property](@entry_id:261270) is replaced by:
$$ \mathbb{E}[X_t \mid \mathcal{F}_s] \le X_s \quad \text{almost surely, for all } s \le t. $$
A [supermartingale](@entry_id:271504) models an "unfavorable game," where the process is expected to decrease or stay the same on average. Note that $(X_t)$ is a [supermartingale](@entry_id:271504) if and only if $(-X_t)$ is a [submartingale](@entry_id:263978). Because of this symmetry, we will often focus our theoretical development on submartingales, as the results for supermartingales follow directly [@problem_id:2973603].

A simple consequence of the [submartingale](@entry_id:263978) property is that the expectation of the process is non-decreasing. Taking the expectation of the [submartingale](@entry_id:263978) inequality yields $\mathbb{E}[\mathbb{E}[X_t \mid \mathcal{F}_s]] \ge \mathbb{E}[X_s]$, which by the law of total expectation simplifies to $\mathbb{E}[X_t] \ge \mathbb{E}[X_s]$ for $s \le t$. However, this is only a necessary condition, not a sufficient one for a process to be a [submartingale](@entry_id:263978) [@problem_id:2973603].

### The Doob Decomposition in Discrete Time

The defining property of a [submartingale](@entry_id:263978) suggests that it contains a "drift" or an expected upward trend. The first fundamental decomposition theorem, due to Joseph Doob, makes this intuition precise for discrete-time processes. It states that any [submartingale](@entry_id:263978) can be uniquely decomposed into a martingale and a predictable, increasing process.

**The Doob Decomposition Theorem (Discrete Time):** Let $(X_n)_{n \in \mathbb{N}_0}$ be an integrable, [adapted process](@entry_id:196563). Then it admits a unique decomposition $X_n = M_n + A_n$, where:
1.  $(M_n)_{n \in \mathbb{N}_0}$ is a [martingale](@entry_id:146036) with respect to $(\mathcal{F}_n)$.
2.  $(A_n)_{n \in \mathbb{N}_0}$ is a **predictable** process, meaning that for each $n \ge 1$, the random variable $A_n$ is $\mathcal{F}_{n-1}$-measurable.
3.  $A_0 = 0$.

Furthermore, if $(X_n)$ is a [submartingale](@entry_id:263978), the [predictable process](@entry_id:274260) $(A_n)$ is non-decreasing (or **increasing**), i.e., $A_{n} \ge A_{n-1}$ almost surely for all $n \ge 1$. If $(X_n)$ is a [supermartingale](@entry_id:271504), $(A_n)$ is non-increasing.

The process $(A_n)$ is called the **compensator** of $(X_n)$. The proof of this theorem is constructive. We define the process $(A_n)$ by its increments:
$$ A_0 = 0, \quad \text{and for } n \ge 1, \quad \Delta A_n := A_n - A_{n-1} = \mathbb{E}[X_n - X_{n-1} \mid \mathcal{F}_{n-1}]. $$
The total process is $A_n = \sum_{k=1}^n \mathbb{E}[X_k - X_{k-1} \mid \mathcal{F}_{k-1}]$. By construction, $A_n$ is $\mathcal{F}_{n-1}$-measurable for $n \ge 1$, so it is predictable. If $(X_n)$ is a [submartingale](@entry_id:263978), $\mathbb{E}[X_n \mid \mathcal{F}_{n-1}] \ge X_{n-1}$, which implies $\Delta A_n \ge 0$, so $(A_n)$ is increasing. We then define the martingale part as $M_n = X_n - A_n$. One can readily verify that $(M_n)$ is indeed a [martingale](@entry_id:146036) [@problem_id:2973603]. This decomposition provides a canonical way to separate the "[fair game](@entry_id:261127)" component from the predictable trend in any [adapted process](@entry_id:196563).

### The Martingale Transform

The Doob decomposition reveals a fundamental structure. The [martingale transform](@entry_id:182444) provides a fundamental tool for constructing new processes from existing ones. In discrete time, the transform represents the gains from a dynamic trading strategy.

Let $(M_n)_{n \in \mathbb{N}_0}$ be a martingale and let $(H_n)_{n \ge 1}$ be a [predictable process](@entry_id:274260), representing a strategy where the amount $H_n$ held during the interval $(n-1, n]$ is decided based on information available at time $n-1$. The **[martingale transform](@entry_id:182444)** process $(Y_n)$ is defined as the cumulative gain:
$$ Y_n = Y_0 + \sum_{k=1}^n H_k (M_k - M_{k-1}). $$
A key result is that if the integrand process $(H_n)$ is predictable and bounded, the resulting transform process $(Y_n)$ is also a martingale. The proof hinges on the predictability of $H_k$:
$$ \mathbb{E}[Y_n - Y_{n-1} \mid \mathcal{F}_{n-1}] = \mathbb{E}[H_n (M_n - M_{n-1}) \mid \mathcal{F}_{n-1}]. $$
Since $H_n$ is $\mathcal{F}_{n-1}$-measurable, it can be pulled out of the [conditional expectation](@entry_id:159140):
$$ \mathbb{E}[Y_n - Y_{n-1} \mid \mathcal{F}_{n-1}] = H_n \mathbb{E}[M_n - M_{n-1} \mid \mathcal{F}_{n-1}] = H_n (M_{n-1} - M_{n-1}) = 0. $$
This shows that $\mathbb{E}[Y_n \mid \mathcal{F}_{n-1}] = Y_{n-1}$, confirming that $(Y_n)$ is a [martingale](@entry_id:146036) [@problem_id:2973603]. This property—that integration with respect to a [martingale](@entry_id:146036) preserves the [martingale property](@entry_id:261270) if the integrand is predictable—is a central theme that extends to continuous time.

### Towards Continuous Time: Predictability and Projections

Extending these ideas to continuous time requires a more sophisticated framework, particularly for the notion of "predictability." A process whose value at time $t$ is determined by information strictly *before* time $t$ should be considered predictable.

On the [product space](@entry_id:151533) $\Omega \times \mathbb{R}_+$, we define the **predictable $\sigma$-algebra**, denoted $\mathcal{P}$, as the $\sigma$-algebra generated by all [adapted processes](@entry_id:187710) with left-continuous [sample paths](@entry_id:184367). Equivalently, it is generated by the collection of "predictable rectangles": sets of the form $A \times (s, t]$ where $A \in \mathcal{F}_s$, along with initial sets $A \times \{0\}$ where $A \in \mathcal{F}_0$ [@problem_id:2973620]. A process is **predictable** if it is measurable with respect to $\mathcal{P}$.

The predictable $\sigma$-algebra must be distinguished from the **optional $\sigma$-algebra**, denoted $\mathcal{O}$. The optional $\sigma$-algebra is generated by all [adapted processes](@entry_id:187710) with càdlàg (right-continuous with left limits) [sample paths](@entry_id:184367). Since any left-continuous [adapted process](@entry_id:196563) is also càdlàg, it follows that $\mathcal{P} \subseteq \mathcal{O}$. This inclusion is generally strict. For instance, the jump of a Poisson process occurs at a totally inaccessible [stopping time](@entry_id:270297) $\tau$. The event of the jump, represented by the graph $[[\tau]] = \{(\omega, t) : t = \tau(\omega)\}$, is an optional set but not a predictable one, as it cannot be "predicted" an instant before it occurs [@problem_id:2973595, @problem_id:2973620].

This distinction is crucial. Just as [conditional expectation](@entry_id:159140) projects a random variable onto a smaller $\sigma$-algebra, we can project entire processes onto the spaces of optional or [predictable processes](@entry_id:262945). For a suitable integrable process $Y$, we can define its **optional projection** ${}^oY$ and **predictable projection** ${}^pY$. These are, respectively, the unique optional and [predictable processes](@entry_id:262945) that satisfy certain averaging properties. Formally, they are characterized by their behavior at [stopping times](@entry_id:261799) [@problem_id:2973591]:
*   The optional projection ${}^oY$ is the unique optional process such that for every stopping time $T$, ${}^oY_T = \mathbb{E}[Y_T \mid \mathcal{F}_T]$ [almost surely](@entry_id:262518) on $\{T  \infty\}$.
*   The predictable projection ${}^pY$ is the unique [predictable process](@entry_id:274260) such that for every **predictable** stopping time $S$, ${}^pY_S = \mathbb{E}[Y_S \mid \mathcal{F}_{S-}]$ almost surely on $\{S  \infty\}$, where $\mathcal{F}_{S-}$ represents the information strictly before time $S$.

These projections are the formal machinery underlying the continuous-time decomposition theorems [@problem_id:2973595, @problem_id:2973591].

### The Doob-Meyer Decomposition in Continuous Time

The central result of this chapter is the continuous-time analogue of the Doob decomposition. The goal is to decompose a continuous-time [submartingale](@entry_id:263978) $X_t$ into a martingale part $M_t$ and an increasing part $A_t$. However, this requires an additional [integrability condition](@entry_id:160334) on the [submartingale](@entry_id:263978).

To motivate this condition, consider the **Optional Sampling Theorem**, which states that for a [submartingale](@entry_id:263978) $X$ and [stopping times](@entry_id:261799) $\sigma \le \tau$, we have $\mathbb{E}[X_\tau] \ge \mathbb{E}[X_\sigma]$ under suitable conditions. Without such conditions, the theorem can fail dramatically. For example, let $(B_t)$ be a standard Brownian motion starting at $B_0=0$. The process $X_t = \exp(-B_t)$ is a [submartingale](@entry_id:263978). Let $\tau_a = \inf\{t \ge 0 : B_t = a\}$ for some $a  0$. We have $\mathbb{E}[X_0] = \exp(0) = 1$. At the stopping time $\tau_a$, we have $X_{\tau_a} = \exp(-a)$, so $\mathbb{E}[X_{\tau_a}] = e^{-a}$. For $a0$, $e^{-a}  1$, so we have $\mathbb{E}[X_{\tau_a}]  \mathbb{E}[X_0]$, a clear violation of the optional sampling inequality. The failure occurs because the [stopping time](@entry_id:270297) $\tau_a$ is unbounded and the process $X_t$ is not sufficiently integrable [@problem_id:2973611].

The correct condition to ensure well-behaved limits and decompositions is the **class D** property. A [submartingale](@entry_id:263978) $(X_t)_{t \ge 0}$ is of class D if the family of random variables $\{X_\tau : \tau \text{ is any bounded stopping time}\}$ is [uniformly integrable](@entry_id:202893). Uniform [integrability](@entry_id:142415) is a strengthening of $L^1$-[boundedness](@entry_id:746948) and is the key to controlling the behavior of the process at [stopping times](@entry_id:261799). It is precisely the condition needed to restore the Optional Sampling Theorem for general [stopping times](@entry_id:261799).

This leads to the celebrated Doob-Meyer Decomposition Theorem.

**The Doob-Meyer Decomposition Theorem (Continuous Time):** Let $(X_t)_{t \ge 0}$ be a càdlàg [submartingale](@entry_id:263978) of class D. Then there exists a unique decomposition
$$ X_t = M_t + A_t, \quad t \ge 0, $$
where:
1.  $(M_t)_{t \ge 0}$ is a [uniformly integrable](@entry_id:202893) càdlàg [martingale](@entry_id:146036).
2.  $(A_t)_{t \ge 0}$ is a **predictable**, càdlàg, increasing process with $A_0 = 0$ and $\mathbb{E}[A_\infty]  \infty$.

The process $A_t$ is the **compensator** of $X_t$. The uniqueness of this decomposition depends crucially on the requirement that $A_t$ be predictable. If we were to only require $A_t$ to be an optional increasing process, the decomposition would not be unique [@problem_id:2973596, @problem_id:2973595]. In the language of projections, $A_t$ is the dual predictable projection of the "raw" increasing part of $X_t$.

The class D condition is not merely a technical convenience; it is necessary. It is possible to construct submartingales that are not of class D and for which the increasing part in their [canonical decomposition](@entry_id:634116) is not predictable. For example, one can define a [local martingale](@entry_id:203733) $M_t = \int_0^t (T-s)^{-1} d\tilde{N}_s$ based on a compensated Poisson process $\tilde{N}$, whose positive part $X_t = M_t^+$ is a [submartingale](@entry_id:263978). The increasing part of $X_t$ can be shown to have jumps at the totally inaccessible jump times of the Poisson process, meaning it cannot be predictable. Therefore, $X_t$ fails to have a Doob-Meyer decomposition, and by the theorem, it cannot be of class D [@problem_id:2973614].

The proof of the Doob-Meyer theorem itself is quite deep, but its strategy is motivated by the discrete case. It involves considering the process on refining discrete-time partitions of the time axis, performing the discrete Doob decomposition on each, and showing that the resulting sequence of discrete compensators converges to the continuous-time [predictable process](@entry_id:274260) $A_t$. The arguments for this convergence rely on compactness properties that are guaranteed by the class D condition and are closely related to the logic underpinning Doob's [submartingale](@entry_id:263978) convergence theorems (which are themselves proven using the upcrossing inequality) [@problem_id:2973609].

### The Martingale Transform in Continuous Time

The final piece of our framework is the [continuous-time martingale](@entry_id:188701) transform, more commonly known as the **[stochastic integral](@entry_id:195087)**. Given a càdlàg [local martingale](@entry_id:203733) $M$ and a suitable integrand process $H$, we define the stochastic integral process $(H \cdot M)_t = \int_0^t H_s dM_s$.

The construction of this integral is a multi-step process [@problem_id:2973594]:
1.  **Simple Predictable Integrands**: The integral is first defined for "simple" [predictable processes](@entry_id:262945) $H$ of the form $H_t = \sum_{i} H_i \mathbf{1}_{(T_{i-1}, T_i]}(t)$, where $H_i$ is $\mathcal{F}_{T_{i-1}}$-measurable. The integral is defined as $\sum_i H_i (M_{T_i \wedge t} - M_{T_{i-1} \wedge t})$, representing gains from a simple buy-and-hold strategy.
2.  **Extension by Approximation**: The definition is extended by approximation to a large class of predictable integrands. A key class is $L^2_{\text{loc}}(M)$, consisting of [predictable processes](@entry_id:262945) $H$ for which $\int_0^t H_s^2 d[M]_s  \infty$ [almost surely](@entry_id:262518), where $[M]$ is the [quadratic variation](@entry_id:140680) of $M$.
3.  **Localization**: The integral is extended to even more general locally bounded predictable integrands via a localization argument using [stopping times](@entry_id:261799).

The crucial requirement throughout this construction is that the integrand $H$ must be **predictable**. This ensures that the resulting process $(H \cdot M)_t$ is a [local martingale](@entry_id:203733). If $H$ were merely optional, the integral would not in general be a [local martingale](@entry_id:203733) [@problem_id:2973595].

The [stochastic integral](@entry_id:195087) interacts elegantly with the Doob-Meyer decomposition. Let $X = M+A$ be the decomposition of a class D [submartingale](@entry_id:263978). Let $H$ be a non-negative, bounded, [predictable process](@entry_id:274260). The integral with respect to the [submartingale](@entry_id:263978) $X$ is defined as:
$$ (H \cdot X)_t = \int_0^t H_s dX_s := \int_0^t H_s dM_s + \int_0^t H_s dA_s. $$
Here, the first term, $(H \cdot M)_t$, is a martingale (and even [uniformly integrable](@entry_id:202893) if $M$ is). The second term, being the integral of a non-negative function with respect to an increasing function, is itself an increasing and [predictable process](@entry_id:274260). The sum of a [martingale](@entry_id:146036) and an increasing process is a [submartingale](@entry_id:263978). Furthermore, one can show that if $X$ is of class D and $H$ is bounded, the resulting [submartingale](@entry_id:263978) $(H \cdot X)_t$ is also of class D, meaning it satisfies the optional [sampling property](@entry_id:276451) [@problem_id:2973611, @problem_id:2973597].

This decomposition of an integral is a foundational principle of stochastic calculus. Any process that can be decomposed into the sum of a [local martingale](@entry_id:203733) and a process of finite variation is called a **[semimartingale](@entry_id:188438)**. The Doob-Meyer theorem shows that submartingales are a special class of [semimartingales](@entry_id:184490) whose finite variation part is increasing and predictable. The theory of [stochastic integration](@entry_id:198356) can be extended to all [semimartingales](@entry_id:184490), which form the largest class of processes for which a reasonable theory of integration can be built.