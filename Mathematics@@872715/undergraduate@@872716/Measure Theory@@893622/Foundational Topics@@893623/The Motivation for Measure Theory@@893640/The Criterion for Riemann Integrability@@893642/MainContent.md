## Introduction
The concept of finding the area under a curve is a cornerstone of calculus and analysis, yet formalizing this intuitive idea requires a rigorous mathematical framework. The theory of Riemann integration provides just that, offering a method to approximate this area with increasing precision. But this process raises a critical question: under what exact conditions does this approximation converge to a single, well-defined value? In other words, which functions are "integrable" in the Riemann sense?

This article delves into the precise criteria that answer this question, charting a course from fundamental principles to a profound and complete characterization of Riemann integrability. We will explore how the behavior of a function—specifically, the nature of its discontinuities—ultimately determines whether it can be integrated.

The journey is structured across three key sections. In **Principles and Mechanisms**, we will construct the theory from the ground up, starting with the necessity of boundedness, defining lower and upper Darboux sums, and establishing the Riemann and Lebesgue criteria for [integrability](@entry_id:142415). Following this, **Applications and Interdisciplinary Connections** will demonstrate the power of these criteria by testing a diverse gallery of functions and revealing deep connections to topology, [functional analysis](@entry_id:146220), and the practical challenges of computational science. Finally, **Hands-On Practices** will offer a set of curated problems designed to solidify your understanding of these essential concepts through direct application.

## Principles and Mechanisms

In the study of integration, our primary objective is to formalize the intuitive concept of the "area under a curve." This requires a rigorous method for approximating this area and defining the conditions under which this approximation converges to a unique, well-defined value. This section delineates the principles and mechanisms that underpin the theory of Riemann integration, establishing a precise criterion for when a function is considered "integrable."

### The Foundational Requirement: Boundedness

Before we can even begin to speak of approximating the area under a function's graph, we must impose a fundamental constraint: the function must be **bounded** on the interval of integration. A function $f$ is bounded on $[a, b]$ if there exists a real number $M \gt 0$ such that $|f(x)| \le M$ for all $x \in [a, b]$.

To understand why this is a non-negotiable prerequisite, consider the function $f(x) = \frac{1}{x}$ on the interval $(0, 1]$, and let us assign some finite value for the function at $x=0$, say $f(0) = c$. If we attempt to apply the standard method of approximating area using rectangles over a partition of $[0, 1]$, we immediately encounter a problem. Any partition $P = \{x_0, x_1, \dots, x_n\}$ of $[0, 1]$ will have $x_0 = 0$. The first subinterval is $[0, x_1]$. On this subinterval, the function $f$ is unbounded above. As $x$ approaches $0$ from the right, $f(x)$ grows without limit. Consequently, the supremum (least upper bound) of $f(x)$ on $[0, x_1]$ is infinite. Any attempt to calculate an "upper" approximating area will involve a rectangle of infinite height, rendering the entire procedure meaningless within the standard framework of Riemann sums [@problem_id:1450092]. Therefore, the theory of Riemann integration that we develop henceforth is exclusively concerned with bounded functions. The integration of certain unbounded functions is treated separately under the topic of [improper integrals](@entry_id:138794).

### Approximating Area: Lower and Upper Darboux Sums

With the assurance of [boundedness](@entry_id:746948), we can proceed. The core strategy, conceived by Bernhard Riemann, is to trap the true area between two approximations: an underestimation and an overestimation.

Let $f$ be a bounded function on a closed interval $[a, b]$. A **partition** $P$ of $[a, b]$ is a finite, ordered set of points $P = \{x_0, x_1, \dots, x_n\}$ such that $a = x_0 \lt x_1 \lt \dots \lt x_n = b$. This partition divides $[a, b]$ into $n$ subintervals $[x_{i-1}, x_i]$, each with length $\Delta x_i = x_i - x_{i-1}$.

Since $f$ is bounded, it has a finite infimum ([greatest lower bound](@entry_id:142178)) and supremum (least upper bound) on each subinterval. We define:
$m_i = \inf\{f(x) \mid x \in [x_{i-1}, x_i]\}$
$M_i = \sup\{f(x) \mid x \in [x_{i-1}, x_i]\}$

Using these values, we construct two sums:
The **lower Darboux sum** of $f$ with respect to $P$ is the sum of the areas of the inscribed rectangles:
$L(P, f) = \sum_{i=1}^{n} m_i \Delta x_i$

The **upper Darboux sum** of $f$ with respect to $P$ is the sum of the areas of the circumscribed rectangles:
$U(P, f) = \sum_{i=1}^{n} M_i \Delta x_i$

Geometrically, $L(P, f)$ represents an area that is guaranteed to be less than or equal to the true area under the curve, while $U(P, f)$ represents an area that is greater than or equal to it.

Let's consider a practical calculation for the continuous function $f(x) = 4x - x^2$ on the interval $[0, 4]$, using the partition $P = \{0, 1, 3, 4\}$ [@problem_id:2328172]. The subintervals are $[0, 1]$, $[1, 3]$, and $[3, 4]$. The function is a downward-opening parabola with its maximum at $x=2$.
*   On $[0, 1]$, $f$ is increasing, so $m_1 = f(0) = 0$ and $M_1 = f(1) = 3$. $\Delta x_1 = 1$.
*   On $[1, 3]$, the maximum is $M_2 = f(2) = 4$. The minimum occurs at the endpoints, $m_2 = f(1) = f(3) = 3$. $\Delta x_2 = 2$.
*   On $[3, 4]$, $f$ is decreasing, so $m_3 = f(4) = 0$ and $M_3 = f(3) = 3$. $\Delta x_3 = 1$.

The sums are:
$L(P, f) = (0)(1) + (3)(2) + (0)(1) = 6$
$U(P, f) = (3)(1) + (4)(2) + (3)(1) = 14$

For this partition, the true area is trapped between $6$ and $14$.

Discontinuities can significantly influence these sums. Consider a function on $[0, 2]$ defined as $f(x) = x^2$ for $x \neq 1$, but with a single point discontinuity where $f(1)=5$. With the coarse partition $P=\{0, 1, 2\}$, the subintervals are $[0, 1]$ and $[1, 2]$ [@problem_id:1450097].
*   On $[0, 1]$, the [infimum](@entry_id:140118) is $m_1 = 0$ (from $x=0$), but the supremum is $M_1 = 5$, the value at the single discontinuous point.
*   On $[1, 2]$, the infimum is $m_2 = \inf\{5, (1, 2]^2\} = 1$, but the [supremum](@entry_id:140512) is $M_2 = \sup\{5, (1, 2]^2\} = 5$.
This leads to $L(P, f) = 0(1) + 1(1) = 1$ and $U(P, f) = 5(1) + 5(1) = 10$. The single point of discontinuity, coinciding with a partition point, has dramatically widened the gap between the [lower and upper sums](@entry_id:147709).

### The Definition of the Riemann Integral

The intuition is that if we add more points to a partition (refining it), our approximation should improve. Indeed, if $P'$ is a refinement of $P$ (i.e., $P \subseteq P'$), one can prove the following crucial relationship:
$L(P, f) \le L(P', f) \le U(P', f) \le U(P, f)$

This shows that as we refine partitions, the set of lower sums is non-decreasing and the set of upper sums is non-increasing. Since $f$ is bounded, these sets of sums are also bounded. The [completeness axiom](@entry_id:141596) of real numbers then guarantees that their [supremum and infimum](@entry_id:146074) exist. We define:

The **lower Riemann integral** of $f$ on $[a, b]$ is $\underline{\int_a^b} f(x) \,dx = \sup_P \{L(P, f)\}$.
The **upper Riemann integral** of $f$ on $[a, b]$ is $\overline{\int_a^b} f(x) \,dx = \inf_P \{U(P, f)\}$.

For any function, the lower integral is always less than or equal to the upper integral. The function is said to be **Riemann integrable** if these two values coincide.

**Definition:** A bounded function $f$ is **Riemann integrable** on $[a, b]$ if $\underline{\int_a^b} f(x) \,dx = \overline{\int_a^b} f(x) \,dx$. The common value is called the **Riemann integral** of $f$ and is denoted by $\int_a^b f(x) \,dx$.

What kind of function would fail this condition? Consider the classic **Dirichlet function** on $[0, 2]$, defined as $f(x) = 7$ if $x$ is rational and $f(x) = 3$ if $x$ is irrational [@problem_id:1450110] [@problem_id:1450121]. Both rational and irrational numbers are dense in the real line, meaning any subinterval $[x_{i-1}, x_i]$ with positive length will contain both types of numbers.
Therefore, for any partition $P$:
$m_i = \inf_{x \in [x_{i-1}, x_i]} f(x) = 3$
$M_i = \sup_{x \in [x_{i-1}, x_i]} f(x) = 7$

The sums become:
$L(P, f) = \sum_{i=1}^{n} 3 \Delta x_i = 3 \sum_{i=1}^{n} \Delta x_i = 3(2-0) = 6$
$U(P, f) = \sum_{i=1}^{n} 7 \Delta x_i = 7 \sum_{i=1}^{n} \Delta x_i = 7(2-0) = 14$

Since these values are constant for *any* partition, the lower and upper integrals are:
$\underline{\int_0^2} f(x) \,dx = \sup_P \{6\} = 6$
$\overline{\int_0^2} f(x) \,dx = \inf_P \{14\} = 14$

Because $6 \neq 14$, the Dirichlet function is not Riemann integrable. The function is too "jumpy" everywhere for the approximations to converge to a single value.

### The Riemann Criterion: A Practical Test for Integrability

The definition of integrability, while precise, can be cumbersome to apply directly. A more practical tool is the **Riemann Criterion**.

**Theorem (Riemann Criterion):** A bounded function $f: [a, b] \to \mathbb{R}$ is Riemann integrable if and only if for every $\epsilon \gt 0$, there exists a partition $P$ of $[a, b]$ such that:
$U(P, f) - L(P, f) \lt \epsilon$

This criterion states that a function is integrable if and only if we can make the total area of the "uncertainty zones"—the regions between the tops of the inscribed rectangles and the circumscribed rectangles—arbitrarily small. If this condition holds, it forces the gap between the [upper and lower integrals](@entry_id:196080) to be zero. Specifically, for any such partition $P$, we have $0 \le \overline{\int}f - \underline{\int}f \le U(P, f) - L(P, f) \lt \epsilon$. Since this must hold for any $\epsilon \gt 0$, the only possibility is that the difference is zero. This principle is confirmed in [@problem_id:1450083], where the condition $\lim_{n \to \infty} [U(P_n, f) - L(P_n, f)] = 0$ for a sequence of partitions with shrinking mesh implies [integrability](@entry_id:142415).

### Identifying Integrable Functions

The Riemann Criterion allows us to identify broad classes of functions that are guaranteed to be integrable.

**Monotonic Functions:** If $f$ is monotonic (either non-decreasing or non-increasing) on $[a, b]$, it is Riemann integrable. To see why, consider a non-decreasing $f$ and a uniform partition $P_N$ with $N$ subintervals, each of width $\Delta x = (b-a)/N$. On any subinterval $[x_{k-1}, x_k]$, we have $m_k = f(x_{k-1})$ and $M_k = f(x_k)$. The difference between the sums becomes a [telescoping series](@entry_id:161657):
$$U(P_N, f) - L(P_N, f) = \sum_{k=1}^{N} (M_k - m_k) \Delta x = \Delta x \sum_{k=1}^{N} (f(x_k) - f(x_{k-1}))$$
$$= \frac{b-a}{N} (f(x_N) - f(x_0)) = \frac{(b-a)(f(b)-f(a))}{N}$$
As demonstrated for $f(x)=\sqrt{x}$ on $[0,1]$ [@problem_id:1450122], this difference can be made smaller than any $\epsilon$ by choosing $N$ large enough. For $f(x)=\sqrt{x}$, the difference is simply $1/N$, so to get below $\epsilon=0.008$, one needs $N > 1/0.008 = 125$, making $N=126$ the smallest integer.

**Continuous Functions:** If $f$ is continuous on $[a, b]$, it is Riemann integrable. The proof relies on a deeper property of continuous functions on closed, bounded intervals: **uniform continuity**. This guarantees that for a given $\epsilon' = \frac{\epsilon}{b-a}$, we can find a $\delta \gt 0$ such that for any two points $x, y$ in $[a, b]$ with $|x-y| \lt \delta$, we have $|f(x)-f(y)| \lt \epsilon'$. By choosing a partition $P$ with mesh (the length of the longest subinterval) less than $\delta$, we ensure that on every subinterval, $M_i - m_i \lt \epsilon'$. Then,
$U(P, f) - L(P, f) = \sum_{i=1}^{n} (M_i - m_i) \Delta x_i \lt \epsilon' \sum_{i=1}^{n} \Delta x_i = \epsilon'(b-a) = \epsilon$.
The criterion is satisfied.

**Functions with Finitely Many Discontinuities:** What if a function is "mostly" continuous? If a bounded function $f$ on $[a, b]$ has a finite number of discontinuities, it is still Riemann integrable. The strategy is to "quarantine" the discontinuities. Suppose there are $N$ points of discontinuity. For any $\epsilon \gt 0$, we can enclose each of these $N$ points within a very small subinterval. Let's say we make each of these $N$ subintervals of width $w$ [@problem_id:1450103]. The maximum possible contribution to $U(P, f) - L(P, f)$ from one such subinterval is $(M_{max} - m_{min})w$. If $|f(x)| \le K$, this contribution is at most $2Kw$. The total contribution from all $N$ "bad" subintervals is at most $2KNw$. We can make this part less than $\epsilon/2$ by choosing $w$ small enough (specifically, $w  \frac{\epsilon}{4KN}$). On the remaining parts of the interval, $f$ is continuous. We can thus choose a further refinement of these parts to make their contribution to the total difference also less than $\epsilon/2$. The total difference $U(P,f) - L(P,f)$ is then less than $\epsilon$.

### The Lebesgue Criterion: A Complete Characterization

The previous examples—the Dirichlet function, [monotonic functions](@entry_id:145115), functions with finite discontinuities—all suggest that the key to Riemann [integrability](@entry_id:142415) lies in the nature and extent of the function's [set of discontinuities](@entry_id:160308). This idea is made precise by a profound result from Henri Lebesgue.

First, we need the concept of a **set of measure zero**. A set $S \subset \mathbb{R}$ has Lebesgue measure zero if, for any $\epsilon \gt 0$, it can be covered by a countable collection of open intervals whose total length is less than $\epsilon$. Intuitively, a measure-zero set is "negligibly small."
*   Any [finite set](@entry_id:152247) has [measure zero](@entry_id:137864).
*   Any [countable set](@entry_id:140218) (like the set of rational numbers $\mathbb{Q}$) has [measure zero](@entry_id:137864).
*   More surprisingly, there exist uncountable [sets of measure zero](@entry_id:157694). The canonical example is the **ternary Cantor set**, which is constructed by iteratively removing the open middle third of intervals. It is uncountable, yet its total length (measure) is zero.

**Theorem (Lebesgue's Criterion for Riemann Integrability):** A bounded function $f: [a, b] \to \mathbb{R}$ is Riemann integrable if and only if the set of points where $f$ is discontinuous has Lebesgue measure zero.

This elegant theorem provides a complete and powerful characterization. It explains all our prior results:
*   A continuous function is integrable because its [set of discontinuities](@entry_id:160308) is empty, and the empty set has measure zero.
*   A [monotonic function](@entry_id:140815) is integrable because its [set of discontinuities](@entry_id:160308) is at most countable, and [countable sets](@entry_id:138676) have [measure zero](@entry_id:137864).
*   A function with finitely many discontinuities is integrable because a [finite set](@entry_id:152247) has [measure zero](@entry_id:137864) [@problem_id:1450103].
*   The Dirichlet function is not integrable because it is discontinuous at every point of its domain; the [set of discontinuities](@entry_id:160308) is the entire interval, which has positive measure.

The Lebesgue criterion also resolves more subtle cases. If a bounded function's discontinuities are all contained within the ternary Cantor set, it must be Riemann integrable, because its discontinuity set is a subset of a measure-zero set and thus also has measure zero [@problem_id:1335078]. The [uncountability](@entry_id:154024) of the Cantor set is irrelevant; its "size" in the sense of measure is what matters.

Conversely, if the [set of discontinuities](@entry_id:160308) has a positive measure, the function cannot be Riemann integrable. Consider a function that is $\gamma$ on a "fat" Cantor-like set $E$ of positive measure $m(E) = 1 - \alpha/2$, and $\delta$ elsewhere [@problem_id:1335055]. This function is discontinuous on the set $E$. Since $m(E) \gt 0$, the function is not Riemann integrable. Furthermore, we can calculate that the gap between the [upper and lower integrals](@entry_id:196080) is precisely $(\gamma - \delta)m(E)$, directly quantifying the failure of integrability by the measure of the discontinuity set.

In summary, the journey from intuitive approximations to a rigorous theory of integration culminates in Lebesgue's criterion. It reveals that the delicate dance between continuity and discontinuity, as measured by the concept of Lebesgue measure, is the ultimate arbiter of Riemann integrability for bounded functions.