## Introduction
While the intuitive concept of an integral as the "area under a curve" is useful, a rigorous mathematical framework is necessary to handle the vast landscape of functions encountered in analysis. The central challenge, addressed by Bernhard Riemann, was to formalize this concept in a way that precisely defines which functions are "integrable," especially those that are not perfectly continuous. This article delves into the criterion for Riemann [integrability](@entry_id:142415), providing the definitive answer to this foundational question of calculus.

This article will guide you through the essential theory and applications of Riemann integrability. The first chapter, **Principles and Mechanisms**, builds the concept from the ground up, introducing partitions, Darboux sums, and the formal Riemann criterion, and using it to prove the [integrability](@entry_id:142415) of continuous and [monotonic functions](@entry_id:145115). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the criterion's power by applying it to functions with complex discontinuities and exploring its deep connections to other analytical theorems and fields like computational science. Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding by tackling concrete problems that test the limits of the theory.

## Principles and Mechanisms

Having established an intuitive understanding of the [definite integral](@entry_id:142493) as the area under a curve, we now turn to the rigorous construction of this concept, as developed by Bernhard Riemann. The central challenge is to create a definition that is precise enough to handle a wide variety of functions, including those that are not everywhere continuous. This chapter introduces the foundational machinery of partitions, Darboux sums, and the crucial criterion that determines whether a function is, in the formal sense, integrable.

### Upper and Lower Sums: Bounding the Area

The core idea behind the Riemann integral is to approximate the area under the [graph of a function](@entry_id:159270) $f(x)$ on a closed interval $[a, b]$ from both above and below. This is achieved by dividing the interval into smaller pieces and constructing rectangles on each piece.

Let $f: [a, b] \to \mathbb{R}$ be a **bounded function**. A **partition** $P$ of the interval $[a, b]$ is a finite, ordered set of points $P = \{x_0, x_1, \ldots, x_n\}$ such that $a = x_0  x_1  \dots  x_n = b$. This partition divides $[a, b]$ into $n$ subintervals, with the $i$-th subinterval being $I_i = [x_{i-1}, x_i]$. The length of this subinterval is denoted by $\Delta x_i = x_i - x_{i-1}$.

Since $f$ is bounded, it has a finite [infimum and supremum](@entry_id:137411) on each subinterval. We define:
- $m_i = \inf_{x \in I_i} f(x)$ (the [greatest lower bound](@entry_id:142178) of $f$ on $I_i$)
- $M_i = \sup_{x \in I_i} f(x)$ (the [least upper bound](@entry_id:142911) of $f$ on $I_i$)

Using these values, we can define two kinds of sums for the partition $P$:

1.  The **Lower Darboux Sum**, denoted $L(P, f)$, is the sum of the areas of the "inscribed" rectangles:
    $$L(P, f) = \sum_{i=1}^{n} m_i \Delta x_i$$
    This sum represents an underestimation of the true area under the curve.

2.  The **Upper Darboux Sum**, denoted $U(P, f)$, is the sum of the areas of the "circumscribed" rectangles:
    $$U(P, f) = \sum_{i=1}^{n} M_i \Delta x_i$$
    This sum represents an overestimation of the true area under the curve.

For any given partition $P$, it is clear that $L(P, f) \le U(P, f)$. To move from these approximations to a precise definition of the integral, we consider all possible partitions of $[a, b]$.

The **Lower Riemann Integral** of $f$ is defined as the [supremum](@entry_id:140512) over all possible lower sums:
$$\underline{\int_a^b} f(x) \,dx = \sup_{P} \{L(P, f)\}$$

The **Upper Riemann Integral** of $f$ is defined as the infimum over all possible upper sums:
$$\overline{\int_a^b} f(x) \,dx = \inf_{P} \{U(P, f)\}$$

It can be shown that for any bounded function $f$, the lower integral is always less than or equal to the upper integral: $\underline{\int_a^b} f(x) \,dx \le \overline{\int_a^b} f(x) \,dx$.

A function $f$ is said to be **Riemann integrable** on $[a, b]$ if and only if its lower and upper integrals are equal. The common value is then defined as the **Riemann Integral** of $f$, denoted by $\int_a^b f(x) \,dx$.
$$\int_a^b f(x) \,dx = \underline{\int_a^b} f(x) \,dx = \overline{\int_a^b} f(x) \,dx$$

Consider the classic example of a function that fails this condition, a variation of the Dirichlet function defined on $[0, \pi]$ as $f(x) = 5$ for rational $x$ and $f(x) = 2$ for irrational $x$ [@problem_id:1450121]. Since both rational and [irrational numbers](@entry_id:158320) are dense in $\mathbb{R}$, any subinterval $[x_{i-1}, x_i]$ will contain both. Thus, for any partition $P$, we have $m_i = 2$ and $M_i = 5$ for all $i$. The [lower and upper sums](@entry_id:147709) become:
$$L(P, f) = \sum_{i=1}^{n} 2 \Delta x_i = 2(b-a) = 2\pi$$
$$U(P, f) = \sum_{i=1}^{n} 5 \Delta x_i = 5(b-a) = 5\pi$$
Since these values are constant for any partition, the lower integral is $2\pi$ and the upper integral is $5\pi$. Because they are not equal, the function is not Riemann integrable. A similar conclusion arises for the function $f(x)=x$ for rational $x$ and $f(x)=0$ for irrational $x$ on $[0,2]$ [@problem_id:1338647]. For a uniform partition into $n$ subintervals, the lower sum is always $0$, while the upper sum is $2 + 2/n$. In the limit as $n \to \infty$, the lower integral is $0$ and the upper integral is $2$, again demonstrating non-integrability.

### The Riemann-Darboux Integrability Criterion

The definition of [integrability](@entry_id:142415), while precise, can be cumbersome to work with directly. A more practical tool is the **Riemann-Darboux Criterion**, which provides an equivalent condition for integrability.

**Theorem (Riemann-Darboux Criterion):** A bounded function $f$ on $[a, b]$ is Riemann integrable if and only if for every $\epsilon > 0$, there exists a partition $P$ of $[a, b]$ such that:
$$U(P, f) - L(P, f)  \epsilon$$

The expression $U(P, f) - L(P, f)$ represents the total area of the "regions of uncertainty"—the difference between the upper and lower approximating rectangles. The criterion states that a function is integrable if we can make this total uncertain area arbitrarily small by choosing a sufficiently fine partition. If this condition holds, it forces the gap between the [upper and lower integrals](@entry_id:196080) to be zero, ensuring they are equal.

A powerful consequence of this criterion is that if we can find just one sequence of partitions $\{P_n\}$ whose mesh (the length of the longest subinterval) approaches zero, and for which the difference $U(P_n, f) - L(P_n, f)$ approaches zero, then the function is guaranteed to be Riemann integrable [@problem_id:1450083].

### Important Classes of Integrable Functions

The Riemann-Darboux criterion allows us to prove that large and important classes of functions are integrable.

#### Continuous Functions

**Theorem:** If a function $f$ is continuous on a closed interval $[a, b]$, then it is Riemann integrable on $[a, b]$.

The proof relies on the property of **uniform continuity**. A function that is continuous on a closed, bounded interval is necessarily uniformly continuous. This means that for any desired vertical tolerance $\epsilon' > 0$, we can find a horizontal distance $\delta > 0$ such that if two points are closer than $\delta$, their function values are closer than $\epsilon'$. By choosing a partition $P$ with a mesh smaller than this $\delta$, we can ensure that the oscillation $M_i - m_i$ on every subinterval is less than $\epsilon'$. Summing over all subintervals, we get:
$$U(P, f) - L(P, f) = \sum_{i=1}^n (M_i - m_i)\Delta x_i \le \epsilon' \sum_{i=1}^n \Delta x_i = \epsilon' (b-a)$$
By choosing $\epsilon' = \epsilon / (b-a)$, we can make the total difference less than any given $\epsilon$, satisfying the criterion.

For example, consider the function $f(x) = x^2$ on $[0, 1]$ [@problem_id:1338631]. For a uniform partition into $n$ subintervals, the difference between the [upper and lower sums](@entry_id:146229) is precisely $1/n$. To make this difference less than $0.1$, we simply need $1/n  0.1$, which means $n > 10$. The smallest integer value is $n=11$, demonstrating concretely how refining the partition shrinks the area of uncertainty.

#### Monotonic Functions

**Theorem:** If a function $f$ is monotonic (either non-decreasing or non-increasing) on $[a, b]$, then it is Riemann integrable on $[a, b]$.

This remarkable result holds even if the function has jump discontinuities. The proof is surprisingly elegant. Let's consider a [non-decreasing function](@entry_id:202520) $f$ and a uniform partition $P_n$ of $[a, b]$ into $n$ subintervals of length $\Delta x = (b-a)/n$ [@problem_id:1338622]. On any subinterval $I_i = [x_{i-1}, x_i]$, the infimum is $m_i = f(x_{i-1})$ and the [supremum](@entry_id:140512) is $M_i = f(x_i)$. The difference between the [upper and lower sums](@entry_id:146229) is:
$$U(P_n, f) - L(P_n, f) = \sum_{i=1}^n (M_i - m_i) \Delta x = \frac{b-a}{n} \sum_{i=1}^n (f(x_i) - f(x_{i-1}))$$
The sum is a **[telescoping series](@entry_id:161657)**: $(f(x_1) - f(x_0)) + (f(x_2) - f(x_1)) + \dots + (f(x_n) - f(x_{n-1})) = f(x_n) - f(x_0) = f(b) - f(a)$.
Thus, the difference simplifies beautifully to:
$$U(P_n, f) - L(P_n, f) = \frac{(b-a)(f(b)-f(a))}{n}$$
As $n \to \infty$, this quantity clearly approaches zero. Since we have found a sequence of partitions for which the difference tends to zero, the function is Riemann integrable.

#### Lipschitz Continuous Functions

A function $f$ is **Lipschitz continuous** on $[a,b]$ if there exists a constant $K > 0$ such that $|f(x) - f(y)| \le K|x-y|$ for all $x, y \in [a,b]$. This is a stronger condition than uniform continuity. Unsurprisingly, these functions are also Riemann integrable.

Using the Lipschitz condition, we can bound the oscillation on any subinterval $I_i$ by $M_i - m_i \le K \Delta x_i$. For a partition $P_N$ with mesh $|P_N|$, the difference between the sums is:
$$U(P_N, f) - L(P_N, f) = \sum_{i=1}^N (M_i - m_i)\Delta x_i \le \sum_{i=1}^N (K \Delta x_i)\Delta x_i \le K |P_N| \sum_{i=1}^N \Delta x_i = K |P_N| (b-a)$$
As the mesh $|P_N| \to 0$, the difference $U(P_N, f) - L(P_N, f)$ is squeezed to zero, proving integrability. This provides a direct relationship between the mesh size and the approximation error, as seen in the analysis of $f(x)=1/(1+x^2)$ [@problem_id:1338627].

### Properties of Riemann Integrable Functions

The set of Riemann integrable functions on a fixed interval is well-behaved under common algebraic operations.

**Linearity:** If $f$ and $g$ are Riemann integrable on $[a, b]$ and $c$ is a constant, then $f+g$ and $cf$ are also Riemann integrable. The proof for the sum $f+g$ relies on the [triangle inequality](@entry_id:143750) for suprema and infima. On any subinterval $I_i$, we have $M_i(f+g) \le M_i(f) + M_i(g)$ and $m_i(f+g) \ge m_i(f) + m_i(g)$. This leads directly to the inequality for the Darboux sums [@problem_id:1338648]:
$$U(f+g, P) - L(f+g, P) \le [U(f, P) - L(f, P)] + [U(g, P) - L(g, P)]$$
Since $f$ and $g$ are integrable, each term on the right can be made arbitrarily small by choosing a fine enough partition. This forces the term on the left to also become arbitrarily small, proving that $f+g$ is integrable.

**Products and Compositions:** The class of [integrable functions](@entry_id:191199) is also closed under multiplication and certain compositions.

- If $f$ is integrable, then so is $f^2$. The key insight is to relate the oscillation of $f^2$ to the oscillation of $f$. For any subinterval $I$, we have $\omega(f^2, I) = \sup_{x,y \in I}|f(x)^2 - f(y)^2|$. Using $|f(x)^2 - f(y)^2| = |f(x)-f(y)||f(x)+f(y)|$ and the fact that $f$ is bounded by some constant $M$, we can establish the bound $\omega(f^2, I) \le 2M \cdot \omega(f, I)$ [@problem_id:1338638]. This relationship allows us to translate the integrability of $f$ into the [integrability](@entry_id:142415) of $f^2$.

- More generally, if $f:[a,b] \to [c,d]$ is Riemann integrable and $\phi:[c,d] \to \mathbb{R}$ is continuous, then the composition $\phi \circ f$ is also Riemann integrable. The continuity of $\phi$ ensures that where $f$ behaves well (has small oscillation), $\phi \circ f$ also behaves well. The "bad" regions where $f$ has large oscillation are contained in intervals of small total length, and the effect of these regions on the overall integral can be controlled. This powerful theorem guarantees the integrability of functions like the one in problem [@problem_id:2328185], which is a composition of a step-like function and a simple linear function.

### The Lebesgue Criterion for Riemann Integrability

We have seen that continuous and [monotonic functions](@entry_id:145115) are integrable, while wildly [discontinuous functions](@entry_id:139518) like the Dirichlet function are not. This suggests that the "size" of the [set of discontinuities](@entry_id:160308) is the deciding factor. The ultimate answer to the question of which functions are Riemann integrable is given by a beautiful and profound theorem due to Henri Lebesgue.

First, we need the concept of a **set of measure zero**. A set $S \subset \mathbb{R}$ is said to have [measure zero](@entry_id:137864) if, for any $\epsilon > 0$, it can be covered by a countable collection of open intervals whose total length is less than $\epsilon$. Intuitively, a set of measure zero is negligibly small. All finite and [countable sets](@entry_id:138676) have [measure zero](@entry_id:137864).

**Theorem (Lebesgue's Criterion for Riemann Integrability):** A bounded function $f$ on a closed interval $[a, b]$ is Riemann integrable if and only if its [set of discontinuities](@entry_id:160308) has measure zero.

This theorem provides a complete characterization of Riemann integrable functions and unifies all our previous results:
- **Continuous functions:** The [set of discontinuities](@entry_id:160308) is empty, which has measure zero.
- **Monotonic functions:** The [set of discontinuities](@entry_id:160308) is at most countable, which has [measure zero](@entry_id:137864).
- **Dirichlet function:** The [set of discontinuities](@entry_id:160308) is the entire interval, which does not have [measure zero](@entry_id:137864).

Furthermore, this criterion allows us to handle more intricate functions. Consider the function $f$ on $[0,1]$ which is equal to $\cos(\pi x / 2)$ except at the points $x = 1/n$ for positive integers $n$ [@problem_id:1338614]. The [set of discontinuities](@entry_id:160308) is the countable set $\{1, 1/2, 1/3, \dots\}$. Since this set has [measure zero](@entry_id:137864) and the function is bounded, the Lebesgue criterion immediately tells us that $f$ is Riemann integrable.

A vital corollary of this theorem is that if two functions $f$ and $g$ are equal everywhere except on a [set of measure zero](@entry_id:198215), then their [integrability](@entry_id:142415) is linked: if one is integrable, so is the other, and their integrals are identical. This is why, in problem [@problem_id:1338614], the integral of the modified function is simply the integral of $\cos(\pi x / 2)$, as the values on the [countable set](@entry_id:140218) of points do not affect the final result.