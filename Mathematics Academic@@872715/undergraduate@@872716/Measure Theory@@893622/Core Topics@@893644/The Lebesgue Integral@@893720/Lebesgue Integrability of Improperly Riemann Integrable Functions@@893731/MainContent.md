## Introduction
The Lebesgue integral represents a significant advancement over the Riemann integral, offering a more powerful and general framework for the theory of integration. However, this advancement raises a critical question for students of analysis: what is the precise relationship between the familiar improper Riemann integral and the Lebesgue integral, especially over unbounded domains? While the two integrals coincide for well-behaved functions on closed, bounded intervals, their connection becomes far more complex in the context of [improper integrals](@entry_id:138794). This article addresses this knowledge gap by providing a definitive exploration of their relationship.

Across three chapters, this article will guide you through a comprehensive understanding of this topic. The first chapter, "Principles and Mechanisms," will dissect the theoretical underpinnings of the relationship, establishing [absolute convergence](@entry_id:146726) as the fundamental criterion that determines Lebesgue [integrability](@entry_id:142415) for an improperly Riemann integrable function. The second chapter, "Applications and Interdisciplinary Connections," will demonstrate the real-world significance of this distinction, showing how concepts like [conditional convergence](@entry_id:147507) have profound implications in physics, signal processing, and probability theory. Finally, "Hands-On Practices" will allow you to apply these concepts through a series of guided problems, solidifying your ability to analyze the [integrability](@entry_id:142415) of complex functions. We begin by exploring the core principles that govern when these two powerful integration methods align and when they diverge.

## Principles and Mechanisms

As discussed in the introduction, the Lebesgue integral is a powerful extension of the Riemann integral, capable of handling a broader class of functions and exhibiting more robust convergence properties. A natural and pressing question arises: what is the precise relationship between a function being improperly Riemann integrable and it being Lebesgue integrable, particularly over unbounded intervals like $[a, \infty)$? While it is true that any function that is Riemann integrable on a compact interval $[a, b]$ is also Lebesgue integrable on $[a, b]$ with the same integral value, the situation becomes far more nuanced for [improper integrals](@entry_id:138794). This chapter delves into the principles and mechanisms governing this relationship, revealing that the critical distinction lies in the concept of **[absolute convergence](@entry_id:146726)**.

### The Fundamental Equivalence: Absolute Convergence

Let us consider a function $f: [0, \infty) \to \mathbb{R}$ that is Riemann integrable on every compact interval $[0, b]$ for $b \gt 0$. We say $f$ is **improperly Riemann integrable** if the limit $\lim_{b \to \infty} \int_0^b f(x) dx$ exists and is finite. On the other hand, $f$ is **Lebesgue integrable** on $[0, \infty)$ if it is measurable and the Lebesgue integral of its absolute value is finite, i.e., $\int_{[0, \infty)} |f| d\mu \lt \infty$.

The central theorem connecting these two notions provides a clear and decisive criterion. A function $f$ that is Riemann integrable on every compact subinterval of $[0, \infty)$ is Lebesgue integrable on $[0, \infty)$ if and only if its improper Riemann integral is **absolutely convergent**. That is, the improper Riemann integral of its absolute value must be finite:
$$ \int_0^\infty |f(x)| dx = \lim_{b \to \infty} \int_0^b |f(x)| dx \lt \infty $$
When this condition holds, the Lebesgue integral of $f$ exists and is equal to its improper Riemann integral. This statement establishes that the [absolute integrability](@entry_id:146520) of the Riemann integral is the necessary and [sufficient condition](@entry_id:276242) for Lebesgue integrability under these circumstances [@problem_id:1426424].

### The Anatomy of Integrability: Positive and Negative Parts

To understand why [absolute convergence](@entry_id:146726) is the key, we must decompose the function $f$ into its **positive part**, $f^+(x) = \max(f(x), 0)$, and its **negative part**, $f^-(x) = \max(-f(x), 0)$. These are non-negative functions that satisfy two fundamental identities:
$$ f(x) = f^+(x) - f^-(x) $$
$$ |f(x)| = f^+(x) + f^-(x) $$

By the definition of the Lebesgue integral for real-valued functions, $f$ is Lebesgue integrable if and only if both $f^+$ and $f^-$ are Lebesgue integrable. Since $f^+$ and $f^-$ are non-negative, their Lebesgue integrability is equivalent to their Lebesgue integrals being finite. Therefore, $f$ is Lebesgue integrable if and only if:
$$ \int_{[a, \infty)} f^+ d\mu \lt \infty \quad \text{and} \quad \int_{[a, \infty)} f^- d\mu \lt \infty $$
This is, in turn, equivalent to the condition $\int_{[a, \infty)} |f| d\mu = \int_{[a, \infty)} (f^+ + f^-) d\mu \lt \infty$.

Now, let us assume the improper Riemann integral $\int_a^\infty f(x) dx$ converges to a finite value $L$. For any $b > a$, we have $\int_a^b f(x) dx = \int_a^b f^+(x) dx - \int_a^b f^-(x) dx$. As $b \to \infty$, the integrals of the non-negative functions $f^+$ and $f^-$ are non-decreasing and thus approach limits, which may be finite or infinite. Let $P = \int_a^\infty f^+(x) dx$ and $N = \int_a^\infty f^-(x) dx$. For the limit $L = \lim_{b \to \infty} (\int_a^b f^+ - \int_a^b f^-)$ to be finite, we cannot have one of $P$ or $N$ be finite and the other infinite. This leaves only two possibilities:

1.  Both $P$ and $N$ are finite. In this case, $\int_a^\infty |f(x)| dx = P + N$ is also finite. The function is absolutely convergent and therefore Lebesgue integrable [@problem_id:1426428].
2.  Both $P$ and $N$ are infinite. Their difference, $L$, can still converge to a finite value through a delicate cancellation. This leads to the phenomenon of [conditional convergence](@entry_id:147507).

This insight reveals a profound consequence: the improper Riemann [integrability](@entry_id:142415) of $f$ does not guarantee the improper Riemann [integrability](@entry_id:142415) of its positive part, $f^+$. Indeed, $f^+$ is improperly Riemann integrable if and only if $|f|$ is improperly Riemann integrable [@problem_id:1426444]. When an integral converges conditionally, both $\int f^+ dx$ and $\int f^- dx$ must diverge to infinity.

### Conditional Convergence: Where Riemann and Lebesgue Diverge

The most significant divergence between the two integration theories occurs with integrals that are **conditionally convergent**. An improper Riemann integral $\int_a^\infty f(x) dx$ is said to converge conditionally if it converges, but the integral of its absolute value, $\int_a^\infty |f(x)| dx$, diverges.

In such a case, the Riemann integral exists due to cancellations between the positive and negative areas under the curve of $f$. However, the Lebesgue integral, by its very definition, relies on the convergence of the integral of the absolute value. If $\int |f| d\mu = \infty$, the function is not Lebesgue integrable. Therefore, **any function whose improper Riemann integral converges conditionally is not Lebesgue integrable.**

#### The Canonical Example: The Sinc Function

The most famous example illustrating this principle is the **[sinc function](@entry_id:274746)**, $f(x) = \frac{\sin(x)}{x}$ (with $f(0)=1$). The improper Riemann integral converges to a well-known value:
$$ \int_0^\infty \frac{\sin(x)}{x} dx = \frac{\pi}{2} $$
The convergence of this integral can be established using [integration by parts](@entry_id:136350) or, more generally, the Dirichlet test for [improper integrals](@entry_id:138794). The oscillations of $\sin(x)$ provide the necessary cancellations as the magnitude of the function slowly decays like $1/x$.

However, the function is not Lebesgue integrable. To see this, we must examine the integral of its absolute value:
$$ \int_0^\infty \left| \frac{\sin(x)}{x} \right| dx $$
We can lower-bound this integral by summing the contributions over intervals of length $\pi$. For any integer $k \ge 1$, we consider the interval $[k\pi, (k+1)\pi]$. On this interval, $x \le (k+1)\pi$, so $\frac{1}{x} \ge \frac{1}{(k+1)\pi}$. This gives us:
$$ \int_{k\pi}^{(k+1)\pi} \frac{|\sin(x)|}{x} dx \ge \frac{1}{(k+1)\pi} \int_{k\pi}^{(k+1)\pi} |\sin(x)| dx = \frac{2}{(k+1)\pi} $$
Summing over all such intervals from $k=1$ onwards, we find:
$$ \int_\pi^\infty \left| \frac{\sin(x)}{x} \right| dx \ge \sum_{k=1}^\infty \frac{2}{(k+1)\pi} = \frac{2}{\pi} \sum_{j=2}^\infty \frac{1}{j} $$
Since the series on the right is a tail of the divergent [harmonic series](@entry_id:147787), the integral of the absolute value diverges to infinity [@problem_id:1426433] [@problem_id:1426412]. Thus, $f(x) = \frac{\sin(x)}{x}$ is a quintessential example of a function that is improperly Riemann integrable but not Lebesgue integrable.

#### Further Illustrations of Conditional Convergence

The principle of [conditional convergence](@entry_id:147507) is not limited to the [sinc function](@entry_id:274746). Several other functions, some constructed explicitly for pedagogical clarity, demonstrate the same behavior.

1.  **Oscillatory Functions with Slow Decay**: The function $f(x) = \frac{\cos(x)}{\sqrt{x}}$ on $[1, \infty)$ is another such example. The Dirichlet test confirms that its improper Riemann integral converges. However, the integral of its absolute value, $\int_1^\infty \frac{|\cos(x)|}{\sqrt{x}} dx$, can be shown to diverge by comparing it to the divergent [p-series](@entry_id:139707) $\sum \frac{1}{\sqrt{k}}$ [@problem_id:1426431]. The decay rate of $1/\sqrt{x}$ is not fast enough to ensure [absolute convergence](@entry_id:146726).

2.  **Piecewise Constant Functions**: Consider the function defined by a series of characteristic functions [@problem_id:1423438]:
    $$ f(x) = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n} \chi_{[n-1, n)}(x) $$
    This function is a "staircase" function, taking the value $\frac{(-1)^{n+1}}{n}$ on the interval $[n-1, n)$. The improper Riemann integral is simply the sum of the [alternating harmonic series](@entry_id:140965):
    $$ \int_0^\infty f(x) dx = \sum_{n=1}^{\infty} \frac{(-1)^{n+1}}{n} = \ln(2) $$
    This series converges. However, the integral of its absolute value corresponds to the harmonic series:
    $$ \int_0^\infty |f(x)| dx = \sum_{n=1}^{\infty} \int_{n-1}^n \frac{1}{n} dx = \sum_{n=1}^{\infty} \frac{1}{n} = \infty $$
    This makes the function non-Lebesgue integrable. A similar analysis applies to the function $f(x) = \frac{(-1)^{\lfloor x \rfloor}}{x}$, which also has a convergent improper Riemann integral but a divergent absolute integral, since $|f(x)| \approx \frac{1}{x}$ [@problem_id:1409277].

### Absolute Convergence: The Domain of Agreement

When an improper Riemann integral converges absolutely, the distinction between the two integration frameworks vanishes. If $\int_a^\infty |f(x)| dx$ is finite, then as we have established, $f$ is Lebesgue integrable. Furthermore, the Dominated Convergence Theorem can be invoked to show that the value of the Lebesgue integral matches the improper Riemann integral.

A clear example is the function $g(x) = \exp(-x^2)\cos(x)$ [@problem_id:1426412]. Its absolute value is bounded by a function whose integral is known to be finite:
$$ |g(x)| = |\exp(-x^2)\cos(x)| \le \exp(-x^2) $$
The integral of the bounding function is the Gaussian integral: $\int_{-\infty}^\infty \exp(-x^2) dx = \sqrt{\pi}$. By the [comparison test](@entry_id:144078), the improper Riemann integral $\int_{-\infty}^\infty |g(x)| dx$ converges. This [absolute convergence](@entry_id:146726) guarantees that $g(x)$ is Lebesgue integrable on $\mathbb{R}$. Here, the [exponential decay](@entry_id:136762) of $\exp(-x^2)$ is sufficiently rapid to overpower the oscillations of the cosine term, ensuring that the total area of the "lobes" is finite.

### A Crucial Special Case: Non-negative Functions

The discussion of conditional versus [absolute convergence](@entry_id:146726) simplifies dramatically when we restrict our attention to **non-negative functions**. If $f(x) \ge 0$ for all $x$, then $f(x) = |f(x)|$. Consequently, the convergence of the improper Riemann integral $\int_0^\infty f(x) dx$ is, by definition, absolute.

In this case, a function $f \ge 0$ is improperly Riemann integrable if and only if it is Lebesgue integrable. When they exist, the two integrals are equal. This can be proven formally using the **Monotone Convergence Theorem** [@problem_id:1426433]. Let $f_n(x) = f(x) \cdot \chi_{[0, n]}(x)$. The sequence of functions $\{f_n\}$ is non-negative and increases monotonically to $f$. By the Monotone Convergence Theorem, the Lebesgue integral of $f$ is:
$$ \int_{[0, \infty)} f d\mu = \lim_{n \to \infty} \int_{[0, \infty)} f_n d\mu $$
Since $f$ is Riemann integrable on $[0, n]$, its Lebesgue and Riemann integrals on this [compact set](@entry_id:136957) are equal. Thus:
$$ \int_{[0, \infty)} f_n d\mu = \int_0^n f(x) dx $$
Taking the limit as $n \to \infty$, we get:
$$ \int_{[0, \infty)} f d\mu = \lim_{n \to \infty} \int_0^n f(x) dx $$
This shows that the Lebesgue integral equals the improper Riemann integral. If one is finite, so is the other. This formalizes the intuition that for non-negative functions, there can be no cancellation of areas, and thus no possibility of [conditional convergence](@entry_id:147507).

### Extensions and Further Properties

The principles discussed so far can be extended to other scenarios, such as functions that are unbounded on a finite interval, and can be used to analyze the preservation of integrability under certain operations.

#### Unbounded Functions on Finite Intervals

The same dichotomy between absolute and [conditional convergence](@entry_id:147507) appears when dealing with improper Riemann integrals on bounded intervals, such as $(0, 1]$, where the function may be unbounded near an endpoint. Consider a function that is continuous on $(0, 1]$ and whose improper Riemann integral is defined as $\lim_{\epsilon \to 0^+} \int_\epsilon^1 f(x) dx$.

A classic example is $f(x) = \frac{\sin(1/x)}{x}$ on $(0, 1]$ [@problem_id:1426448]. By making the substitution $t=1/x$, the improper Riemann integral becomes:
$$ \lim_{\epsilon \to 0^+} \int_\epsilon^1 \frac{\sin(1/x)}{x} dx = \lim_{T \to \infty} \int_1^T \frac{\sin(t)}{t} dt $$
As we have seen, this integral converges. However, the integral of the absolute value becomes $\int_1^\infty \frac{|\sin(t)|}{t} dt$, which diverges. Thus, $f(x)$ is improperly Riemann integrable on $(0, 1]$ but is not Lebesgue integrable. This demonstrates that the core issue is the nature of convergence, not merely the unboundedness of the domain of integration.

#### Preservation of Integrability under Multiplication

A more subtle question concerns how integrability behaves under multiplication. For instance, if a function $f$ is improperly Riemann integrable on $[0, \infty)$, does multiplying it by a bounded, [monotonic function](@entry_id:140815) preserve this property?

Consider the function $h(x) = f(x) \arctan(x)$ [@problem_id:1426427]. The function $\arctan(x)$ is bounded and monotonic on $[0, \infty)$, approaching $\frac{\pi}{2}$ as $x \to \infty$. We can write $\arctan(x) = \frac{\pi}{2} - g(x)$, where $g(x) = \frac{\pi}{2} - \arctan(x)$ is a positive, [monotonic function](@entry_id:140815) that tends to $0$. The integral of $h(x)$ becomes:
$$ \int_0^b h(x) dx = \frac{\pi}{2} \int_0^b f(x) dx - \int_0^b f(x) g(x) dx $$
The first term converges by hypothesis. The convergence of the second term, $\int_0^\infty f(x)g(x) dx$, can be established by a more general form of the Dirichlet or Abel test for [improper integrals](@entry_id:138794), often proven using [integration by parts](@entry_id:136350). Since $f$ has a bounded primitive $F(x) = \int_0^x f(t) dt$ and $g(x)$ is monotonic and tends to zero, the integral converges. Therefore, if $f$ is improperly Riemann integrable, so is $h(x) = f(x)\arctan(x)$. This result holds even if the integral of $f$ converges only conditionally, highlighting the robust nature of [tests for convergence](@entry_id:144433) that rely on [monotonicity](@entry_id:143760).

In summary, the bridge between the worlds of improper Riemann and Lebesgue integration is built upon the foundation of [absolute convergence](@entry_id:146726). While the Lebesgue integral sacrifices the ability to make sense of conditionally convergent integrals, it gains immense power through its superior convergence theorems and its solid grounding in [measure theory](@entry_id:139744), which treats the integral of any integrable function as an absolutely convergent process.