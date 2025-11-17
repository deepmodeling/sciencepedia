## Introduction
The Riemann integral is a cornerstone of mathematical analysis, providing the first rigorous definition for the intuitive concept of the area under a curve. However, this definition does not apply to all functions; a function must be sufficiently "well-behaved" to be integrable. The central problem, then, is to establish a clear and precise test to determine which functions possess a well-defined Riemann integral. This article addresses this knowledge gap by providing a comprehensive exploration of the Riemann criterion for [integrability](@entry_id:142415).

Across the following chapters, you will build a solid understanding of this fundamental concept. We will begin in "Principles and Mechanisms" by constructing the integral from the ground up, starting with partitions and Darboux sums and culminating in the formal statement of the Riemann criterion and its modern interpretation via Lebesgue's work on discontinuities. Next, "Applications and Interdisciplinary Connections" will demonstrate the power of this criterion by using it to prove the [integrability](@entry_id:142415) of broad classes of functions and to explore the algebraic structure of the space of [integrable functions](@entry_id:191199). Finally, the "Hands-On Practices" section offers a chance to apply these theoretical tools to concrete examples, solidifying your grasp of both the mechanics and the limitations of Riemann integration.

## Principles and Mechanisms

In the preceding chapter, we introduced the Riemann integral as a means of rigorously defining the area under a curve. This concept, while intuitive, rests on a precise and intricate foundation. For a function to be "integrable" in the sense of Riemann, it must satisfy certain conditions of regularity or "well-behavedness." This chapter delves into the principles and mechanisms that govern Riemann integrability, establishing the criteria that separate [integrable functions](@entry_id:191199) from those that are not. We will move from the foundational building blocks of partitions and sums to a powerful, modern criterion that provides a definitive test for [integrability](@entry_id:142415).

### From Partitions to Upper and Lower Sums

The journey to define the integral begins with partitioning the [domain of a function](@entry_id:162002). For a closed interval $[a, b]$, a **partition** $P$ is a finite set of points $\{x_0, x_1, \ldots, x_n\}$ such that $a = x_0  x_1  \ldots  x_n = b$. This partition divides $[a, b]$ into $n$ subintervals of the form $[x_{i-1}, x_i]$, each with a length $\Delta x_i = x_i - x_{i-1}$.

Our goal is to approximate the area under the curve of a function $f(x)$ on $[a, b]$. To do this without ambiguity, we must first require that the function be **bounded** on the interval. That is, there must exist some number $M$ such that $|f(x)| \le M$ for all $x \in [a, b]$. This prevents the "area" from becoming infinite on even the smallest of subintervals.

With a bounded function $f$ and a partition $P$, we can define two fundamental quantities for each subinterval $[x_{i-1}, x_i]$: the **infimum** ([greatest lower bound](@entry_id:142178)) of the function's values, denoted $m_i = \inf_{x \in [x_{i-1}, x_i]} f(x)$, and the **[supremum](@entry_id:140512)** ([least upper bound](@entry_id:142911)), denoted $M_i = \sup_{x \in [x_{i-1}, x_i]} f(x)$.

These values allow us to construct two approximations for the area. The **lower Darboux sum** of $f$ with respect to $P$ is the sum of the areas of rectangles that lie entirely beneath the curve:
$$
L(P, f) = \sum_{i=1}^{n} m_i \Delta x_i
$$
Conversely, the **upper Darboux sum** of $f$ with respect to $P$ is the sum of the areas of rectangles that entirely contain the curve on each subinterval:
$$
U(P, f) = \sum_{i=1}^{n} M_i \Delta x_i
$$
By their very definition, for any given partition $P$, it is always true that $L(P, f) \le U(P, f)$.

To make these definitions concrete, let us consider an example. Suppose we wish to analyze the function $f(x) = 4x - x^2$ on the interval $[0, 4]$ using the partition $P = \{0, 1, 3, 4\}$. This partition creates three subintervals: $[0, 1]$, $[1, 3]$, and $[3, 4]$. We first find the [infimum and supremum](@entry_id:137411) of $f(x)$ on each subinterval. The function is a downward-opening parabola with its maximum at $x=2$.
- On $[0, 1]$, $f(x)$ is increasing, so $m_1 = f(0) = 0$ and $M_1 = f(1) = 3$.
- On $[1, 3]$, the maximum occurs at $x=2$, giving $M_2 = f(2) = 4$. The minimum occurs at the endpoints, $f(1)=3$ and $f(3)=3$, so $m_2=3$.
- On $[3, 4]$, $f(x)$ is decreasing, so $m_3 = f(4) = 0$ and $M_3 = f(3) = 3$.
The lengths of the subintervals are $\Delta x_1 = 1$, $\Delta x_2 = 2$, and $\Delta x_3 = 1$. We can now compute the sums [@problem_id:2328172]:
$$
L(P, f) = (0)(1) + (3)(2) + (0)(1) = 6
$$
$$
U(P, f) = (3)(1) + (4)(2) + (3)(1) = 14
$$
These sums provide a lower and an upper bound for the "true" area under the curve. To get a better estimate, we would need to refine the partition.

### The Squeeze: Upper and Lower Integrals

Intuitively, as we add more points to a partition, our approximations should improve. Let $P'$ be a **refinement** of $P$, meaning $P \subseteq P'$. A key property of Darboux sums is that refining a partition causes the lower sum to increase (or stay the same) and the upper sum to decrease (or stay the same):
$$
L(P, f) \le L(P', f) \le U(P', f) \le U(P, f)
$$
This creates a "squeezing" effect. The set of all possible lower sums, $\{L(P,f)\}$, is bounded above by any upper sum. Similarly, the set of all upper sums, $\{U(P,f)\}$, is bounded below by any lower sum. This allows us to define two critical values:

The **lower Riemann integral** of $f$ is the supremum of all possible lower sums:
$$
\underline{\int_a^b} f(x) \,dx = \sup_{P} L(P, f)
$$
The **upper Riemann integral** of $f$ is the infimum of all possible upper sums:
$$
\overline{\int_a^b} f(x) \,dx = \inf_{P} U(P, f)
$$
It follows directly from the properties of sums that for any bounded function $f$, we have $\underline{\int_a^b} f(x) \,dx \le \overline{\int_a^b} f(x) \,dx$.

For "well-behaved" functions, we expect this inequality to be an equality—that the squeeze closes completely. But this is not always the case. Consider a function defined on $[0, \pi]$ as follows [@problem_id:1450121]:
$$
f(x) = \begin{cases} 5  \text{if } x \in \mathbb{Q} \\ 2  \text{if } x \notin \mathbb{Q} \end{cases}
$$
Because the rational numbers ($\mathbb{Q}$) and [irrational numbers](@entry_id:158320) are both dense in the real line, every subinterval $[x_{i-1}, x_i]$ with positive length will contain both rational and [irrational numbers](@entry_id:158320). Consequently, for any partition $P$ of $[0, \pi]$, the [infimum and supremum](@entry_id:137411) on any subinterval are constant: $m_i = 2$ and $M_i = 5$.
The [lower and upper sums](@entry_id:147709) for *any* partition are therefore:
$$
L(P, f) = \sum_{i=1}^{n} 2 \Delta x_i = 2 \sum_{i=1}^{n} \Delta x_i = 2(\pi - 0) = 2\pi
$$
$$
U(P, f) = \sum_{i=1}^{n} 5 \Delta x_i = 5 \sum_{i=1}^{n} \Delta x_i = 5(\pi - 0) = 5\pi
$$
Since these values are constant for all partitions, the [supremum](@entry_id:140512) of the lower sums is $2\pi$ and the [infimum](@entry_id:140118) of the upper sums is $5\pi$. Thus:
$$
\underline{\int_{0}^{\pi}} f(x) \,dx = 2\pi \quad \text{and} \quad \overline{\int_{0}^{\pi}} f(x) \,dx = 5\pi
$$
In this case, the lower and upper integrals are not equal. The gap between them is $3\pi$, and it cannot be closed, no matter how fine the partition. This leads us to the formal definition of [integrability](@entry_id:142415).

### The Riemann Criterion for Integrability

A bounded function $f$ on a closed interval $[a, b]$ is said to be **Riemann integrable** if its lower and upper Riemann integrals are equal. Their common value is defined as the **Riemann integral** of $f$ from $a$ to $b$, denoted by $\int_a^b f(x) \,dx$.
$$
f \text{ is Riemann integrable on } [a, b] \iff \underline{\int_a^b} f(x) \,dx = \overline{\int_a^b} f(x) \,dx
$$
This definition, while precise, is often impractical to work with directly. A more useful formulation is the **Riemann-Darboux Criterion**:

A bounded function $f$ on $[a, b]$ is Riemann integrable if and only if for every $\epsilon > 0$, there exists a partition $P$ of $[a, b]$ such that:
$$
U(P, f) - L(P, f)  \epsilon
$$
This criterion states that we can make the difference between the [upper and lower sums](@entry_id:146229) arbitrarily small by choosing a sufficiently fine partition. This is equivalent to saying that the gap between the [upper and lower integrals](@entry_id:196080) is zero.

This leads to a related and powerful result concerning sequences of partitions. If we have a sequence of partitions $\{P_n\}$ such that their mesh (the length of the longest subinterval) approaches zero, and we find that $\lim_{n \to \infty} [U(P_n, f) - L(P_n, f)] = 0$, then the function $f$ is necessarily Riemann integrable on $[a, b]$ [@problem_id:1450083].

Let's apply this criterion to another function that challenges integrability. Consider $f(x)$ on $[0, 2]$ defined by [@problem_id:1338647]:
$$
f(x) = \begin{cases} x  \text{if } x \in \mathbb{Q} \\ 0  \text{if } x \in \text{irrational} \end{cases}
$$
Let's use a uniform partition $P_n$ with $n$ subintervals, each of length $\Delta x = 2/n$. The partition points are $x_k = 2k/n$. On any subinterval $[x_{k-1}, x_k]$, the presence of irrational numbers means the [infimum](@entry_id:140118) is always $m_k = 0$. The presence of rational numbers and the fact that $f(x)=x$ is increasing for them means the supremum is the right endpoint, $M_k = x_k = 2k/n$.
The [lower and upper sums](@entry_id:147709) are:
$$
L(P_n, f) = \sum_{k=1}^{n} m_k \Delta x = \sum_{k=1}^{n} 0 \cdot \frac{2}{n} = 0
$$
$$
U(P_n, f) = \sum_{k=1}^{n} M_k \Delta x = \sum_{k=1}^{n} \frac{2k}{n} \cdot \frac{2}{n} = \frac{4}{n^2} \sum_{k=1}^{n} k = \frac{4}{n^2} \frac{n(n+1)}{2} = 2 + \frac{2}{n}
$$
As $n \to \infty$, the mesh of $P_n$ goes to zero, but the difference between the sums approaches a non-zero limit:
$$
\lim_{n \to \infty} [U(P_n, f) - L(P_n, f)] = \lim_{n \to \infty} \left(2 + \frac{2}{n} - 0\right) = 2
$$
Since this limit is not 0, the function is not Riemann integrable. The gap between the upper and lower approximations persists, preventing a single value for the integral from being defined.

### A Modern Perspective: The Role of Discontinuities

The Riemann criterion provides a test for [integrability](@entry_id:142415), but it doesn't always give a clear picture of *which kinds* of functions are integrable. The modern understanding of this question, due to the work of Henri Lebesgue, connects [integrability](@entry_id:142415) directly to the set of points where the function is discontinuous.

First, we must re-emphasize a crucial prerequisite: **boundedness**. The entire framework of Darboux sums and Riemann [integrability](@entry_id:142415) is built upon the assumption that the function is bounded on the interval. Consider the function $f(x) = 1/x$ on $(0, 1]$, with $f(0)$ assigned some finite value. This function is not bounded on $[0, 1]$. For any partition $P$, the first subinterval will be $[0, x_1]$. The supremum of $f(x)$ on this subinterval is infinite. Consequently, the upper sum $U(P, f)$ is infinite for every possible partition, making it impossible to satisfy the Riemann criterion. The failure of $f(x)=1/x$ to be Riemann integrable on $[0,1]$ is fundamentally because it is not bounded [@problem_id:1450092].

For bounded functions, the decisive factor is the "size" of the [set of discontinuities](@entry_id:160308). The key result is **Lebesgue's Criterion for Riemann Integrability**:

A bounded function $f$ on a closed interval $[a, b]$ is Riemann integrable if and only if the set of its points of discontinuity has **Lebesgue [measure zero](@entry_id:137864)**.

A set has Lebesgue measure zero if it can be covered by a countable collection of [open intervals](@entry_id:157577) whose total length is arbitrarily small. Intuitively, this means the set is "negligibly small." Importantly, any finite set and any [countable set](@entry_id:140218) (like the set of rational numbers, $\mathbb{Q}$) has [measure zero](@entry_id:137864).

This criterion is incredibly powerful. Let's revisit some functions from this new perspective [@problem_id:1338593].
- A **[monotonic function](@entry_id:140815)** on $[a, b]$ is always Riemann integrable. This is because the [set of discontinuities](@entry_id:160308) of a [monotonic function](@entry_id:140815) is at most countable, and therefore has measure zero. The function $f_B(x) = \sum_{n=1}^{\infty} \frac{1}{n^3} H(x - 1/n)$ is a sum of non-decreasing functions, making it non-decreasing (and bounded). It is therefore Riemann integrable.
- **Thomae's function** (or the "popcorn function") is defined on $[0,1]$ by $f(x) = 1/q$ if $x = p/q$ is a rational number in lowest terms, and $f(x) = 0$ if $x$ is irrational [@problem_id:1409300]. One can show this function is continuous at every irrational number but discontinuous at every rational number. The [set of discontinuities](@entry_id:160308) is $\mathbb{Q} \cap [0, 1]$, which is countable and thus has [measure zero](@entry_id:137864). Since the function is also bounded (by 1), it is Riemann integrable.
- In contrast, a function like $f_A(x) = \cos(x)$ for rational $x$ and $f_A(x) = \sin(x)$ for irrational $x$ is continuous only where $\cos(x) = \sin(x)$ (i.e., at $x=\pi/4$ in $[0,1]$). The [set of discontinuities](@entry_id:160308) is $[0,1] \setminus \{\pi/4\}$, which has measure $1$ (not zero). Therefore, this function is not Riemann integrable.

Lebesgue's criterion also simplifies the evaluation of many integrals. A profound consequence is that changing a function's values on a set of measure zero does not affect its [integrability](@entry_id:142415) or the value of its integral. Consider the function on $[0,1]$ defined as $f(x) = 1/(n^2+1)$ for $x=1/n$ ($n \in \mathbb{N}$) and $f(x) = \cos(\pi x / 2)$ otherwise [@problem_id:1338614]. This function is bounded and differs from the continuous function $g(x) = \cos(\pi x / 2)$ only on the [countable set](@entry_id:140218) $\{1, 1/2, 1/3, \ldots\}$, which has [measure zero](@entry_id:137864). Therefore, $f$ is Riemann integrable, and its integral is the same as that of $g(x)$:
$$
\int_0^1 f(x) \,dx = \int_0^1 \cos\left(\frac{\pi x}{2}\right) \,dx = \left[ \frac{2}{\pi}\sin\left(\frac{\pi x}{2}\right) \right]_0^1 = \frac{2}{\pi}
$$

### Advanced Insights into Integrability

The concept of discontinuity can be quantified using the **oscillation** of a function. The oscillation of $f$ at a point $x$, denoted $\omega_f(x)$, is defined as:
$$
\omega_f(x) = \lim_{\delta \to 0^+} \sup_{s,t \in (x-\delta, x+\delta) \cap [a,b]} |f(s)-f(t)|
$$
The oscillation measures the extent of variation of the function in an arbitrarily small neighborhood of $x$. A function $f$ is continuous at $x$ if and only if $\omega_f(x) = 0$. The [set of discontinuities](@entry_id:160308) is precisely the set where $\omega_f(x) > 0$.

This allows for a deeper formulation of the [integrability condition](@entry_id:160334). For example, a function defined to be $5$ on a special set $K$ and $2$ elsewhere, where $K$ is a "fat Cantor set" with positive measure (e.g., measure $1/2$), will be discontinuous at every point of $K$ [@problem_id:2328140]. On this set $K$, the oscillation $\omega_f(x) = |5-2| = 3$. Since the [set of discontinuities](@entry_id:160308) has positive measure, the function is not Riemann integrable. The integral of the oscillation function, $\int_0^1 \omega_f(x) \,dx = \int_K 3 \,dx = 3 \cdot m(K) = 3/2$, gives a quantitative measure of this failure. It can be shown that a bounded function is Riemann integrable if and only if the integral of its oscillation is zero.

Another advanced criterion for Riemann [integrability](@entry_id:142415), which hints at connections to [functional analysis](@entry_id:146220), involves "continuity in the mean." It states that a bounded function $f$ is Riemann integrable on $[a,b]$ if and only if
$$
\lim_{h \to 0^+} \int_a^{b-h} |f(x+h) - f(x)| \,dx = 0
$$
This condition essentially averages the "local difference" of the function across the interval. For a pathological case like the Dirichlet function $D(x)$, which is everywhere discontinuous, this property fails dramatically. For any irrational $h$, the integrand $|D(x+h) - D(x)|$ is 1 on a [dense set](@entry_id:142889), and its upper integral is $1-h$. This prevents the limit from being zero, providing yet another confirmation of its non-[integrability](@entry_id:142415) [@problem_id:2328187].

In summary, the Riemann criterion for integrability, in its various forms, provides a rigorous framework for understanding which bounded functions possess a well-defined integral. While the original formulation in terms of [upper and lower sums](@entry_id:146229) is fundamental, the modern perspective based on the measure of the [set of discontinuities](@entry_id:160308) offers a more powerful and often more intuitive tool for classifying functions and calculating their integrals.