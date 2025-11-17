## Introduction
The theory of integration lies at the heart of mathematical analysis, but the familiar Riemann integral has significant limitations, especially when dealing with [limits of functions](@entry_id:159448) and highly [discontinuous functions](@entry_id:139518). To overcome these challenges, [measure theory](@entry_id:139744) introduces the Lebesgue integral, a more powerful and general framework. This article focuses on the first crucial step in this development: constructing the integral and exploring its properties for the class of [non-negative measurable functions](@entry_id:192146). This foundational stage is essential, as the entire theory of integration for more complex functions is built upon it.

This article is structured to provide a comprehensive understanding of this core topic.
*   In **Principles and Mechanisms**, we will construct the Lebesgue integral from the ground up, starting with simple functions and extending to all [non-negative measurable functions](@entry_id:192146). We will explore its fundamental properties and the celebrated convergence theorems that make it so powerful.
*   Next, in **Applications and Interdisciplinary Connections**, we will see how this abstract theory provides the foundational language for diverse fields, from probability theory and [functional analysis](@entry_id:146220) to quantum physics and geometry.
*   Finally, **Hands-On Practices** will offer you the opportunity to apply these concepts to challenging problems, solidifying your understanding of the integral's properties and its superiority over the Riemann integral.

## Principles and Mechanisms

Having established the foundational concepts of [measure spaces](@entry_id:191702) and measurable functions, we now turn to one of the central objectives of measure theory: the development of a robust theory of integration. The Lebesgue integral, which we shall construct, extends the familiar Riemann integral to a much larger class of functions and domains. It also possesses superior convergence properties that make it an indispensable tool in modern analysis, probability theory, and [mathematical physics](@entry_id:265403). This chapter is dedicated to constructing the integral for the class of [non-negative measurable functions](@entry_id:192146) and exploring its fundamental properties and key convergence theorems.

### The Integral of Simple Non-negative Functions

Our construction begins with the most elementary class of [measurable functions](@entry_id:159040): the **simple functions**. Recall that a [simple function](@entry_id:161332) $\phi$ is a measurable function that takes on only a finite number of non-negative values. Any such function can be written in its **[canonical representation](@entry_id:146693)** as a finite [linear combination](@entry_id:155091) of [characteristic functions](@entry_id:261577) of disjoint [measurable sets](@entry_id:159173):
$$ \phi(x) = \sum_{i=1}^{n} a_i \chi_{A_i}(x) $$
where $a_i \ge 0$ are distinct values taken by $\phi$, and $A_i = \{x \mid \phi(x) = a_i\}$ are disjoint [measurable sets](@entry_id:159173) whose union is the domain of $\phi$.

The [integral of a simple function](@entry_id:183337) is defined in the most intuitive way possible: as a weighted sum of its values, where each value is weighted by the measure of the set on which it is constant.

**Definition:** The **Lebesgue integral** of a [non-negative simple function](@entry_id:183498) $\phi = \sum_{i=1}^{n} a_i \chi_{A_i}$ with respect to the measure $\mu$ is defined as:
$$ \int \phi \, d\mu = \sum_{i=1}^{n} a_i \mu(A_i) $$
By convention, if $a_i = 0$ and $\mu(A_i) = \infty$, the product $a_i \mu(A_i)$ is taken to be $0$. The integral is taken over the entire space $X$, but we often restrict the integration to a measurable subset $E \subseteq X$ by defining $\int_E \phi \, d\mu = \int \phi \cdot \chi_E \, d\mu$.

This definition aligns perfectly with our intuitive notion of an integral as a measure of "total value." Consider a function defined on a finite set. Such a function is inherently simple. For instance, let our space be $X = \{v_1, v_2, v_3, v_4, v_5\}$ with a measure $\mu$ assigned to each point. A function $f: X \to [0, \infty)$ can be seen as a simple function where each set $A_i$ is a singleton $\{v_i\}$ and the corresponding value is $a_i = f(v_i)$. Its integral is simply the sum of each function value multiplied by the measure of the corresponding point, fully illustrating the definition [@problem_id:1439558].

For example, if $f(v_1)=9$ and $\mu(\{v_1\}) = 1/3$, the contribution to the total integral from the point $v_1$ is $9 \times \frac{1}{3} = 3$. Summing these products over all points in the space yields the total integral $\int_X f \, d\mu = \sum_{i=1}^{5} f(v_i) \mu(\{v_i\})$ [@problem_id:1439558].

### The Integral of General Non-negative Functions

Most functions of interest are not simple; they may take on a continuum of values. To extend our definition of the integral to any [non-negative measurable function](@entry_id:184645) $f$, we employ an approximation technique that is central to the power of Lebesgue theory. The core idea is to approximate $f$ from below by a sequence of [simple functions](@entry_id:137521).

A cornerstone theorem of [measure theory](@entry_id:139744) states that for any [non-negative measurable function](@entry_id:184645) $f: X \to [0, \infty]$, there exists a sequence of non-negative [simple functions](@entry_id:137521) $(\phi_n)_{n=1}^\infty$ such that:
1.  The sequence is non-decreasing: $0 \le \phi_1(x) \le \phi_2(x) \le \dots$ for all $x \in X$.
2.  The sequence converges pointwise to $f$: $\lim_{n \to \infty} \phi_n(x) = f(x)$ for all $x \in X$.

With this approximation in hand, we can define the integral of $f$. Since each $\phi_n$ is a better approximation to $f$ than its predecessors, the sequence of their integrals, $\int \phi_n \, d\mu$, should approach the value we wish to assign to $\int f \, d\mu$. This motivates the following definition.

**Definition:** Let $f$ be a [non-negative measurable function](@entry_id:184645). The **Lebesgue integral** of $f$ with respect to the measure $\mu$ is defined as:
$$ \int f \, d\mu = \sup \left\{ \int \phi \, d\mu \mid 0 \le \phi \le f, \phi \text{ is simple} \right\} $$
It follows from this definition and the existence of a non-decreasing approximating sequence $(\phi_n)$ converging to $f$ that $\int f \, d\mu = \lim_{n \to \infty} \int \phi_n \, d\mu$.

This definition is powerful because it does not depend on the specific choice of the approximating sequence. Any [non-decreasing sequence](@entry_id:139501) of [simple functions](@entry_id:137521) converging to $f$ will yield the same value for the limit of their integrals.

To make this construction concrete, consider the function $f(x) = \sqrt{x}$ on the interval $[0, 1]$ with the standard Lebesgue measure. We can construct an explicit sequence of [simple functions](@entry_id:137521) $(s_n)$ that approximate $f$. For each integer $n \ge 1$, we partition the range $[0, 1]$ into $2^n$ subintervals of the form $[\frac{k}{2^n}, \frac{k+1}{2^n})$. We then define $s_n(x)$ to be the constant value $\frac{k}{2^n}$ on the set where $f(x)$ is in this range, i.e., where $\sqrt{x} \approx \frac{k}{2^n}$. This corresponds to setting $s_n(x) = \frac{k}{2^n}$ for $x \in [(\frac{k}{2^n})^2, (\frac{k+1}{2^n})^2)$. As $n$ increases, this approximation becomes finer, and the sequence $(s_n)$ converges monotonically up to $\sqrt{x}$. By calculating the integral of each $s_n$ and taking the limit, we find that $\lim_{n \to \infty} \int_0^1 s_n(x) \, dx = \frac{2}{3}$, which is precisely the value of the familiar Riemann integral $\int_0^1 \sqrt{x} \, dx$. This example beautifully illustrates how the abstract definition of the Lebesgue integral is realized through concrete approximation [@problem_id:1439547].

### Fundamental Properties of the Integral

The Lebesgue integral for non-negative functions possesses several essential properties that are direct consequences of its construction. These properties are fundamental to its use in analysis. Let $f$ and $g$ be [non-negative measurable functions](@entry_id:192146), and let $c \ge 0$ be a constant.

1.  **Linearity:** The integral is a [linear operator](@entry_id:136520).
    *   **Homogeneity:** $\int c f \, d\mu = c \int f \, d\mu$.
    *   **Additivity:** $\int (f+g) \, d\mu = \int f \, d\mu + \int g \, d\mu$.

2.  **Monotonicity:** If $0 \le f(x) \le g(x)$ for all $x$, then $\int f \, d\mu \le \int g \, d\mu$. This follows immediately from the [supremum](@entry_id:140512) definition, as any [simple function](@entry_id:161332) $\phi \le f$ is also less than or equal to $g$.

3.  **Additivity over Domains:** The integral is additive over disjoint domains of integration. If $\{E_n\}_{n=1}^\infty$ is a sequence of pairwise disjoint [measurable sets](@entry_id:159173) and $E = \bigcup_{n=1}^\infty E_n$, then:
    $$ \int_E f \, d\mu = \sum_{n=1}^\infty \int_{E_n} f \, d\mu $$
    This property is known as **[countable additivity](@entry_id:141665)**. For a finite union of two [disjoint sets](@entry_id:154341) $A$ and $B$, this simplifies to $\int_{A \cup B} f \, d\mu = \int_A f \, d\mu + \int_B f \, d\mu$ [@problem_id:1439554]. As a more advanced application, one might need to calculate an integral over a set $S$ which can be partitioned into a countable collection of [disjoint sets](@entry_id:154341) $E_n$. By applying [countable additivity](@entry_id:141665), the total integral can be computed by summing the integrals over each piece: $\int_S f \, dm = \sum_{n=1}^\infty \int_{S \cap E_n} f \, dm$. This technique is particularly effective when the function $f$ has a simple constant form on each $E_n$ [@problem_id:1439550].

### The Role of Sets of Measure Zero

One of the most significant distinctions between the Lebesgue and Riemann integrals lies in their treatment of [sets of measure zero](@entry_id:157694), also known as **[null sets](@entry_id:203073)**. In Lebesgue theory, such sets are effectively invisible to the integral.

A property is said to hold **almost everywhere** (a.e.) if the set of points where it fails to hold is a [set of measure zero](@entry_id:198215). This concept leads to several profound consequences for integration.

First, if a [non-negative measurable function](@entry_id:184645) $f$ is integrated over a set $E$ with $\mu(E)=0$, the integral is zero. This is clear for [simple functions](@entry_id:137521) and extends to general functions by the supremum definition.

Second, and more importantly, changing a function on a [null set](@entry_id:145219) does not alter its integral. If two [non-negative measurable functions](@entry_id:192146) $f$ and $g$ are equal [almost everywhere](@entry_id:146631) (i.e., $f(x)=g(x)$ for all $x$ outside a [null set](@entry_id:145219) $N$), then $\int f \, d\mu = \int g \, d\mu$. This is because the difference $f-g$ is zero everywhere except on $N$, and the integral of any function over $N$ is zero. This property is immensely useful. For instance, consider a function defined with one rule for rational numbers and another for [irrational numbers](@entry_id:158320) within an interval like $[0, 1]$ [@problem_id:1439535]. Since the set of rational numbers $\mathbb{Q}$ is countable and thus has Lebesgue [measure zero](@entry_id:137864), the function is equal a.e. to the function defined only on the irrationals. Its integral can therefore be computed by ignoring the values on the [rational points](@entry_id:195164) entirely. This principle also applies to functions defined piecewise, where some pieces are defined over [null sets](@entry_id:203073) [@problem_id:1439554].

The converse of this principle is also a cornerstone of the theory:

**Theorem:** Let $f$ be a [non-negative measurable function](@entry_id:184645). Then $\int f \, d\mu = 0$ if and only if $f(x) = 0$ almost everywhere.

The "if" part is a direct consequence of the previous discussion. For the "only if" part, if $f$ were greater than some $\epsilon > 0$ on a set $E$ of positive measure, its integral would be at least $\epsilon \cdot \mu(E) > 0$. Therefore, for the integral to be zero, the set $\{x \mid f(x) > 0\}$ must have [measure zero](@entry_id:137864). This provides a powerful criterion for identifying functions that integrate to zero. Any non-negative function that is non-zero only on a [null set](@entry_id:145219)—such as the set of rational numbers, the Cantor set, or a finite set of points—will have a Lebesgue integral of zero. Conversely, any function that is strictly positive, even by a tiny constant amount, on a set of positive measure will have a positive integral [@problem_id:1439534].

### Convergence Theorems: Interchanging Limits and Integrals

Perhaps the most celebrated feature of the Lebesgue integral is its powerful relationship with limiting operations. A central question in analysis is: under what conditions can we interchange the order of integration and a limit process? That is, when is the following equality true for a [sequence of functions](@entry_id:144875) $(f_n)$?
$$ \lim_{n \to \infty} \int f_n \, d\mu = \int \left( \lim_{n \to \infty} f_n \right) \, d\mu $$
The Riemann integral behaves poorly in this regard, but the Lebesgue integral provides remarkably general and elegant answers, particularly for non-negative functions.

#### The Monotone Convergence Theorem

The first major result is the **Monotone Convergence Theorem (MCT)**, which gives a simple and powerful condition for the interchange of limit and integral.

**Theorem (Monotone Convergence):** Let $(f_n)_{n=1}^\infty$ be a sequence of [non-negative measurable functions](@entry_id:192146). If the sequence is non-decreasing, i.e., $f_n(x) \le f_{n+1}(x)$ for all $n$ and for almost every $x$, and let $f(x) = \lim_{n \to \infty} f_n(x)$. Then:
$$ \lim_{n \to \infty} \int f_n \, d\mu = \int f \, d\mu = \int \left( \lim_{n \to \infty} f_n \right) \, d\mu $$
Note that the limit integral may be infinite. The theorem's power lies in its simplicity: monotonicity is all that is required. The MCT is, in fact, deeply connected to our very definition of the integral for a general non-negative function, which was defined via a [limit of integrals](@entry_id:141550) of an increasing sequence of [simple functions](@entry_id:137521).

The MCT is especially useful for dealing with [infinite series](@entry_id:143366) of non-negative functions. Since a series $\sum_{n=0}^{\infty} f_n$ is the limit of its partial sums $S_N = \sum_{n=0}^{N} f_n$, and since the $f_n$ are non-negative, the [sequence of partial sums](@entry_id:161258) $(S_N)$ is non-decreasing. The MCT thus directly justifies interchanging the summation and integration:
$$ \int \left( \sum_{n=0}^{\infty} f_n \right) \, d\mu = \int \left( \lim_{N \to \infty} S_N \right) \, d\mu = \lim_{N \to \infty} \int S_N \, d\mu = \lim_{N \to \infty} \sum_{n=0}^{N} \int f_n \, d\mu = \sum_{n=0}^{\infty} \int f_n \, d\mu $$
This allows for the straightforward evaluation of integrals of functions defined by [infinite series](@entry_id:143366) by instead summing the integrals of the individual terms, a technique that can greatly simplify calculations [@problem_id:1439537].

#### Fatou's Lemma

What happens if the sequence of non-negative functions is not monotone? The equality from MCT may no longer hold. However, we are not left without a tool. **Fatou's Lemma** provides a general inequality that relates the integral of the [limit inferior](@entry_id:145282) to the [limit inferior](@entry_id:145282) of the integrals.

**Theorem (Fatou's Lemma):** For any sequence $(f_n)_{n=1}^\infty$ of [non-negative measurable functions](@entry_id:192146):
$$ \int \left( \liminf_{n \to \infty} f_n \right) \, d\mu \le \liminf_{n \to \infty} \left( \int f_n \, d\mu \right) $$
Fatou's Lemma is a statement of robust optimism: in the limit, no "mass" (the value of the integral) can be created out of nothing, but it can be lost. The strict inequality arises in two typical scenarios.

1.  **Mass Escaping to Infinity:** Consider a sequence of "traveling bump" functions, such as $f_n(x) = \chi_{[n, n+1]}(x)$. For any fixed $x$, $f_n(x) \to 0$, so $\liminf f_n = 0$, and the integral of the limit is $\int 0 \, d\mu = 0$. However, the integral of each function in the sequence is $\int f_n \, d\mu = \mu([n, n+1]) = 1$. The [limit inferior](@entry_id:145282) of these integrals is $\liminf (1) = 1$. Thus, we have $0  1$. The "mass" of the integral of $f_n$ has escaped to infinity and is lost in the pointwise limit [@problem_id:1439543].

2.  **Mass Concentrating on Shrinking Sets:** Consider a sequence of functions that become taller and narrower, like $f_n(x) = n \chi_{(0, 1/n)}(x)$. The pointwise limit is $\lim_{n \to \infty} f_n(x) = 0$ for all $x  0$. The integral of the limit is therefore 0. However, the integral of each $f_n$ is $\int_0^1 n \chi_{(0, 1/n)} \, dx = n \cdot (1/n) = 1$. Again, the limit of the integrals is 1, while the integral of the limit is 0. Here, the mass concentrates onto a set of measure zero [@problem_id:1439541].

3.  **Oscillating Functions:** Even without escaping or concentrating mass, the inequality can be strict. Consider a sequence that alternates between two functions, say $f_n(x) = 6x$ for odd $n$ and $f_n(x) = 12(1-x)$ for even $n$ on $[0, 1]$. The [pointwise limit](@entry_id:193549) inferior is $\liminf f_n(x) = \min\{6x, 12(1-x)\}$. The sequence of integrals alternates between $\int_0^1 6x \, dx = 3$ and $\int_0^1 12(1-x) \, dx = 6$. The [limit inferior](@entry_id:145282) of these integrals is 3. However, the integral of the pointwise limit inferior function is $\int_0^1 \min\{6x, 12(1-x)\} \, dx = 2$. We find that $2  3$, providing another concrete example where the inequality in Fatou's Lemma is strict [@problem_id:1439531].

These examples underscore that without the condition of monotonicity (or another condition like domination, to be studied later), we cannot guarantee the exchange of limit and integral. Fatou's Lemma provides the best possible general statement for non-negative functions, serving as both a cautionary principle and a key technical tool in the proofs of more advanced convergence theorems.

In this chapter, we have built the Lebesgue integral from first principles for all [non-negative measurable functions](@entry_id:192146). We have seen how its definition via approximation by simple functions leads to powerful and intuitive properties, particularly its elegant handling of [null sets](@entry_id:203073) and limiting operations. These principles and mechanisms form the bedrock upon which the entire theory of Lebesgue integration is built.