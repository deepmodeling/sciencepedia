## Introduction
In [mathematical analysis](@entry_id:139664), extending concepts from simple cases to more general settings is a common and powerful theme. One of the most significant leaps in [measure theory](@entry_id:139744) is the generalization of the integral from non-negative functions to any real-valued function. This raises a fundamental question: how can we rigorously define an integral for a function that takes on both positive and negative values? The answer lies in a simple yet elegant technique: decomposing the function into two non-negative components. This article provides a comprehensive exploration of this method.

The first chapter, **Principles and Mechanisms**, will introduce the formal definitions of the positive and negative parts of a function, explore their fundamental algebraic properties, and prove their crucial role in preserving [measurability](@entry_id:199191). Next, **Applications and Interdisciplinary Connections** will demonstrate how this decomposition serves as the bedrock for defining the Lebesgue integral and provides structural insights into fields like functional analysis, measure theory, and probability. Finally, **Hands-On Practices** will guide you through practical exercises to solidify your understanding and apply these concepts to concrete problems. By the end, you will have a thorough grasp of this indispensable tool in modern analysis.

## Principles and Mechanisms

In the study of measure and integration theory, a pivotal step is the extension of the concept of an integral from non-negative functions to general real-valued functions. The primary mechanism for achieving this generalization is the decomposition of any real-valued function into two non-negative components. This chapter elucidates the principles behind this decomposition, explores its fundamental properties, and establishes its indispensable role in the construction of the Lebesgue integral.

### The Canonical Decomposition: Defining Positive and Negative Parts

For any real-valued function $f: X \to \mathbb{R}$, we can define two associated non-negative functions: its **positive part** and its **negative part**.

The **positive part** of $f$, denoted by $f^+$, is defined pointwise for each $x \in X$ as:
$$
f^+(x) = \max\{f(x), 0\}
$$
This function captures the magnitude of $f$ wherever $f$ is positive and is zero elsewhere.

The **negative part** of $f$, denoted by $f^-$, is defined pointwise as:
$$
f^-(x) = \max\{-f(x), 0\} = -\min\{f(x), 0\}
$$
It is crucial to observe that, despite its name, the negative part $f^-(x)$ is always non-negative. The name reflects its purpose: to capture the magnitude of $f$ wherever $f$ is negative. If $f(x) = -5$, then $f^+(x) = 0$ and $f^-(x) = \max\{5, 0\} = 5$.

From these definitions, a key property emerges: for any given $x \in X$, at least one of $f^+(x)$ or $f^-(x)$ must be zero. If $f(x) > 0$, then $f^-(x) = 0$. If $f(x) \le 0$, then $f^+(x) = 0$. This implies that the product of the positive and negative parts is always zero:
$$
f^+(x)f^-(x) = 0 \quad \text{for all } x \in X
$$

These two functions allow us to reconstruct the original function $f$ and its absolute value $|f|$ through simple algebraic relationships. Consider the value of $f(x)$ at any point $x$.
- If $f(x) \ge 0$, then $f^+(x) = f(x)$ and $f^-(x) = 0$. Thus, $f(x) = f^+(x) - f^-(x)$ and $|f(x)| = f(x) = f^+(x) + f^-(x)$.
- If $f(x)  0$, then $f^+(x) = 0$ and $f^-(x) = -f(x)$. Thus, $f(x) = -f^-(x) = f^+(x) - f^-(x)$ and $|f(x)| = -f(x) = f^-(x) = f^+(x) + f^-(x)$.

In both cases, we arrive at the same two fundamental identities, which hold for all $x \in X$:
$$
f(x) = f^+(x) - f^-(x)
$$
$$
|f(x)| = f^+(x) + f^-(x)
$$

These two equations form a linear system for $f^+$ and $f^-$. By adding the two equations, we can solve for $f^+(x)$, and by subtracting the first from the second, we can solve for $f^-(x)$. This yields alternative expressions for the positive and negative parts directly in terms of $f$ and its absolute value [@problem_id:1435922]:
$$
f^+(x) = \frac{1}{2}\big(|f(x)| + f(x)\big)
$$
$$
f^-(x) = \frac{1}{2}\big(|f(x)| - f(x)\big)
$$
These algebraic forms are exceptionally useful in theoretical proofs, particularly when dealing with [properties of measurable functions](@entry_id:198711).

### Preservation of Measurability

A central question in measure theory is whether operations on functions preserve measurability. The decomposition into positive and negative parts behaves very well in this regard. A cornerstone theorem states that a function $f$ is measurable if and only if its positive part $f^+$ and negative part $f^-$ are both measurable.

Let's examine both directions of this statement.

First, assume $f^+$ and $f^-$ are [measurable functions](@entry_id:159040). Since the set of measurable functions on a given [space forms](@entry_id:186145) a vector space, it is closed under subtraction. Therefore, the function $f = f^+ - f^-$ is also measurable.

Conversely, assume $f$ is a [measurable function](@entry_id:141135). The [absolute value function](@entry_id:160606) $t \mapsto |t|$ is a continuous function. Since the composition of a measurable function and a continuous function is measurable, the function $|f|$ is also measurable. Now, using the algebraic expressions derived previously,
$$
f^+ = \frac{1}{2}(|f| + f) \quad \text{and} \quad f^- = \frac{1}{2}(|f| - f)
$$
we see that $f^+$ and $f^-$ are formed from linear combinations of the measurable functions $f$ and $|f|$. As the class of measurable functions is closed under addition, subtraction, and scalar multiplication, it follows that both $f^+$ and $f^-$ must be measurable.

While the [measurability](@entry_id:199191) of $f$ is a *sufficient* condition for the [measurability](@entry_id:199191) of $f^+$ and $f^-$, it is not strictly necessary for $f^+$ to be measurable. Consider a non-measurable subset $A \subset [0, 1)$ and define a function $f(x) = \chi_A(x) - 1$, where $\chi_A$ is the characteristic function of $A$. This function is non-measurable because the [preimage](@entry_id:150899) of the open set $(-\frac{1}{2}, \frac{1}{2})$ is precisely the [non-measurable set](@entry_id:138132) $A$. However, its positive part is $f^+(x) = \max\{\chi_A(x)-1, 0\}$, which is identically the zero function for all $x \in [0, 1)$, since $\chi_A(x)$ is either $0$ or $1$. The [constant function](@entry_id:152060) $f^+(x)=0$ is certainly measurable [@problem_id:1435916]. This example highlights that the implication ($f$ measurable $\implies$ $f^+, f^-$ measurable) is the workhorse of the theory, while the converse requires both $f^+$ and $f^-$ to be measurable.

### Fundamental Algebraic Properties

The decomposition into positive and negative parts interacts with other algebraic operations in predictable and useful ways.

**Scalar Multiplication:**
Let $c \in \mathbb{R}$ be a constant.
- If $c \ge 0$, it is straightforward to show that $(cf)^+ = cf^+$ and $(cf)^- = cf^-$.
- If $c  0$, the relationship is inverted. Let $k = -c > 0$. Then:
  $$
  (cf)^+(x) = \max\{cf(x), 0\} = \max\{-kf(x), 0\} = k \max\{-f(x), 0\} = k f^-(x) = -c f^-(x)
  $$
  A similar argument shows that $(cf)^-(x) = -c f^+(x)$. This property is useful when evaluating integrals of scaled functions [@problem_id:1435882]. For instance, the integral of the positive part of $g(x) = cf(x)$ where $c  0$ can be computed by finding the integral of the negative part of $f(x)$ and scaling by $-c$.

**Addition and Subadditivity:**
The decomposition does not distribute linearly over addition. Instead, it satisfies an important inequality known as [subadditivity](@entry_id:137224). For any two functions $f$ and $g$ defined on the same domain, we have:
$$
(f+g)^+ \le f^+ + g^+ \quad \text{and} \quad (f+g)^- \le f^- + g^-
$$
To prove the first inequality, we note that $f(x) \le f^+(x)$ and $g(x) \le g^+(x)$ for all $x$. Summing these gives $f(x)+g(x) \le f^+(x)+g^+(x)$. Since the function $t \mapsto \max\{t, 0\}$ is non-decreasing, we can apply it to both sides:
$$
(f+g)^+(x) = \max\{f(x)+g(x), 0\} \le \max\{f^+(x)+g^+(x), 0\}
$$
Because $f^+(x) \ge 0$ and $g^+(x) \ge 0$, their sum is non-negative, so $\max\{f^+(x)+g^+(x), 0\} = f^+(x)+g^+(x)$. This completes the proof [@problem_id:1435908]. The second inequality for the negative parts follows by applying the first result to the functions $-f$ and $-g$.

Strict equality, $(f+g)^+ = f^+ + g^+$, does not hold in general. To see this, consider the functions $f(x) = \sin(x)$ and $g(x) = \cos(x)$ at the point $x_0 = \frac{3\pi}{4}$ [@problem_id:1435892]. Here, $f(x_0) = \frac{\sqrt{2}}{2}$ and $g(x_0) = -\frac{\sqrt{2}}{2}$.
- The sum of the positive parts is $(f^+ + g^+)(x_0) = \max\{\frac{\sqrt{2}}{2}, 0\} + \max\{-\frac{\sqrt{2}}{2}, 0\} = \frac{\sqrt{2}}{2} + 0 = \frac{\sqrt{2}}{2}$.
- The positive part of the sum is $(f+g)^+(x_0) = \max\{\frac{\sqrt{2}}{2} - \frac{\sqrt{2}}{2}, 0\} = \max\{0, 0\} = 0$.
Clearly, $\frac{\sqrt{2}}{2} \ne 0$. Equality holds if and only if $f(x)$ and $g(x)$ have the same sign (or one is zero).

### The Jordan Decomposition and Its Minimality Property

The representation $f = f^+ - f^-$ is often called the **Jordan decomposition** of $f$. This decomposition is not just one of many possibilities; it is canonical and minimal in a very precise sense.

Suppose we have any decomposition of $f$ into the difference of two non-negative functions, say $f = g - h$, where $g(x) \ge 0$ and $h(x) \ge 0$ for all $x$. How does this arbitrary decomposition relate to the Jordan decomposition?

From $f = g - h$, we have $g = f + h$. Since $h \ge 0$, it follows that $g \ge f$. Because $g$ is also non-negative by definition, $g$ must be greater than or equal to both $f$ and $0$. Therefore, it must be greater than or equal to their maximum:
$$
g(x) \ge \max\{f(x), 0\} = f^+(x)
$$
Similarly, from $f = g - h$, we have $h = g - f$. Since $g \ge 0$, it follows that $h \ge -f$. Because $h$ is also non-negative, we can conclude that:
$$
h(x) \ge \max\{-f(x), 0\} = f^-(x)
$$
This demonstrates that the Jordan decomposition is the most "efficient" representation of $f$ as a difference of non-negative functions. Any other such pair of functions, $(g,h)$, must be pointwise at least as large as the canonical pair $(f^+, f^-)$ [@problem_id:1435914].

This minimality property has profound implications for integration. By the [monotonicity](@entry_id:143760) of the integral, if $f = g-h$ is any decomposition into [non-negative measurable functions](@entry_id:192146), then:
$$
\int g \,d\mu \ge \int f^+ \,d\mu \quad \text{and} \quad \int h \,d\mu \ge \int f^- \,d\mu
$$
The value $\int g \,d\mu - \int f^+ \,d\mu = \int (g - f^+) \,d\mu$ quantifies the "excess" of the decomposition $(g,h)$ relative to the minimal Jordan decomposition [@problem_id:1435917].

### The Role in Defining the Lebesgue Integral

The Jordan decomposition provides the very foundation for defining the Lebesgue integral of a general real-valued measurable function. The integral is first defined for non-negative simple functions and then extended to all [non-negative measurable functions](@entry_id:192146) via approximation. The final step is to accommodate functions that take both positive and negative values.

A measurable function $f$ is said to be **Lebesgue integrable** if the integrals of both its positive and negative parts are finite. That is,
$$
\int f^+ \,d\mu  \infty \quad \text{and} \quad \int f^- \,d\mu  \infty
$$
Since $|f| = f^+ + f^-$, this condition is equivalent to requiring that the integral of its absolute value be finite: $\int |f| \,d\mu  \infty$ [@problem_id:1435920].

If a function $f$ is Lebesgue integrable, its Lebesgue integral is **defined** as:
$$
\int f \,d\mu = \int f^+ \,d\mu - \int f^- \,d\mu
$$
The minimality of the Jordan decomposition ensures this definition is robust and avoids issues with [indeterminate forms](@entry_id:144301) like $\infty - \infty$.

In practice, calculating an integral using this definition often involves splitting the domain of integration into regions where the function is non-negative and where it is negative. For instance, to calculate an integral like $I = \int_0^\pi (f^+(x) + 2f^-(x)) dx$ for $f(x) = \cos(2x) - \frac{1}{2}$ [@problem_id:1435929], one must first identify the set $P = \{x \in [0, \pi] \mid f(x) \ge 0\}$ and its complement $N = \{x \in [0, \pi] \mid f(x)  0\}$. The integral then becomes:
$$
I = \int_P f(x) \,dx + \int_N 2(-f(x)) \,dx
$$
This requires solving the inequality $\cos(2x) \ge \frac{1}{2}$ on the interval $[0, \pi]$. Similarly, calculating the measure of sets like $S_1 = \{x \mid f^+(x) > c\}$ for some $c>0$ simply reduces to finding the measure of the set $\{x \mid f(x) > c\}$ [@problem_id:1435921]. This decomposition method proves to be a powerful and versatile tool, essential for both theoretical developments and practical computations in analysis and probability theory.