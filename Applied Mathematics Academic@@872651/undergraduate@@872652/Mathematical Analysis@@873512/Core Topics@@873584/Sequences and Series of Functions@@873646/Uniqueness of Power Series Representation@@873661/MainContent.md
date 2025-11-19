## Introduction
Representing functions as [power series](@entry_id:146836) is a foundational concept in [mathematical analysis](@entry_id:139664), allowing us to approximate complex functions with infinite polynomials and understand their local behavior. But when we find such a series—whether through Taylor's formula, solving a differential equation, or algebraic manipulation—a critical question arises: is this representation the only one possible? This article addresses this fundamental knowledge gap by exploring the **[uniqueness of power series](@entry_id:139951) representation**. The certainty that a function's [power series](@entry_id:146836) is one-of-a-kind is not just a theoretical footnote; it is a powerful tool that underpins vast areas of mathematics and science.

Across the following chapters, you will gain a comprehensive understanding of this vital principle.
*   In **Principles and Mechanisms**, we will rigorously prove the Identity Theorem, the cornerstone of [power series](@entry_id:146836) uniqueness, and explore its profound theoretical consequences, including the link to Taylor coefficients and the powerful concept of analytic continuation.
*   **Applications and Interdisciplinary Connections** will showcase the theorem's utility as a problem-solving technique, demonstrating how equating coefficients is used to prove [combinatorial identities](@entry_id:272246), solve [recurrence relations](@entry_id:276612), and tackle problems in physics and number theory.
*   Finally, **Hands-On Practices** will provide you with the opportunity to apply these concepts to concrete problems, solidifying your understanding through guided exercises.

This journey will reveal how a single, elegant theorem provides the logical foundation for some of the most powerful methods in [modern analysis](@entry_id:146248).

## Principles and Mechanisms

The concept of representing functions as [power series](@entry_id:146836) is a cornerstone of mathematical analysis, providing a powerful bridge between the local behavior of a function at a single point and its global properties over an interval or domain. Central to this entire framework is the principle of uniqueness: if a function can be represented by a [power series](@entry_id:146836), that representation is one of a kind. This chapter will rigorously establish this principle and explore its profound consequences.

### The Identity Theorem for Power Series

The fundamental statement of uniqueness, often called the **Identity Theorem for Power series**, asserts that a function's power [series representation](@entry_id:175860) is uniquely determined.

**Theorem (Identity Theorem for Power Series):** Suppose two [power series](@entry_id:146836), $f(x) = \sum_{n=0}^{\infty} a_n (x-c)^n$ and $g(x) = \sum_{n=0}^{\infty} b_n (x-c)^n$, both converge on an [open interval](@entry_id:144029) $I$ containing the point $c$. If $f(x) = g(x)$ for all $x \in I$, then their coefficients must be identical, i.e., $a_n = b_n$ for all non-negative integers $n$.

The proof of this theorem is not only elegant but also reveals the mechanism by which the coefficients are tethered to the function itself. Let us consider the function $h(x) = f(x) - g(x) = \sum_{n=0}^{\infty} (a_n - b_n)(x-c)^n$. Our premise is that $h(x) = 0$ for all $x$ in the interval $I$.

To prove the theorem, we can determine the coefficients sequentially [@problem_id:2197437].
First, evaluate $h(x)$ at the center of the expansion, $x=c$:
$h(c) = (a_0 - b_0) + (a_1 - b_1)(c-c) + (a_2 - b_2)(c-c)^2 + \dots = a_0 - b_0$.
Since $h(x)=0$ on the interval, and [power series](@entry_id:146836) are continuous functions, $h(c)=0$. Thus, we must have $a_0 = b_0$.

Next, we leverage a key property of [power series](@entry_id:146836): they can be differentiated term-by-term within their [interval of convergence](@entry_id:146678). The derivative of $h(x)$ is:
$h'(x) = \sum_{n=1}^{\infty} n(a_n - b_n)(x-c)^{n-1} = (a_1 - b_1) + 2(a_2 - b_2)(x-c) + \dots$
Since $h(x)$ is the zero function on $I$, its derivative $h'(x)$ must also be zero everywhere on $I$. Evaluating at $x=c$:
$h'(c) = a_1 - b_1 = 0$, which implies $a_1 = b_1$.

This process can be repeated. By differentiating $k$ times and evaluating at $x=c$, we isolate the $k$-th coefficient. The $k$-th derivative of $h(x)$ at $x=c$ is given by:
$h^{(k)}(c) = k!(a_k - b_k)$.
Since $h^{(k)}(c)=0$ for all $k$, we must have $k!(a_k - b_k) = 0$. As $k! \neq 0$, it follows that $a_k = b_k$ for all $k \ge 0$.

This demonstrates not only that the coefficients are unique but also reveals the explicit formula for them. If a function $f(x)$ is represented by a power series $\sum a_n (x-c)^n$, then its coefficients *must* be its **Taylor coefficients**:
$$a_n = \frac{f^{(n)}(c)}{n!}$$
This means that if a function has a power [series representation](@entry_id:175860) around a point $c$, that series is necessarily its Taylor series. This direct link between coefficients and derivatives is a powerful computational tool. For instance, if a function $y(x) = 3\exp(x^2)$ is the solution to a differential equation, its Maclaurin series is $y(x) = 3 \sum_{n=0}^{\infty} \frac{x^{2n}}{n!}$. By comparing this to the general form $\sum_{k=0}^{\infty} \frac{y^{(k)}(0)}{k!} x^k$, we can directly read off the values of its derivatives at the origin without computing them directly. The coefficient of $x^8$ is $\frac{y^{(8)}(0)}{8!}$, which in this case corresponds to the $n=4$ term of the first series, $\frac{3}{4!}$. Equating these, we find $y^{(8)}(0) = \frac{3 \cdot 8!}{4!} = 5040$ [@problem_id:2333577].

### Algebraic Applications of Uniqueness

The [identity theorem](@entry_id:139624) is far more than a theoretical curiosity; it is a fundamental tool for solving equations and establishing relationships between functions. The principle is simple: if two [analytic functions](@entry_id:139584) are proven to be equal, their [power series](@entry_id:146836) coefficients must be identical. This transforms a functional equality into an infinite sequence of algebraic equations for the coefficients.

A straightforward application arises in modeling physical systems. Suppose a system's response $R(p)$ to a stimulus $p$ is described by a [power series](@entry_id:146836) $R(p) = \sum a_n (p-p_0)^n$. If the system exhibits [homeostasis](@entry_id:142720), meaning $R(p)=K$ for all $p$ in an interval around $p_0$, we have an equality between two [power series](@entry_id:146836):
$\sum_{n=0}^{\infty} a_n (p-p_0)^n = K + 0 \cdot (p-p_0) + 0 \cdot (p-p_0)^2 + \dots$
By the [identity theorem](@entry_id:139624), we can immediately conclude that $a_0 = K$ and $a_n = 0$ for all $n \ge 1$ [@problem_id:2333553].

This method is particularly effective for handling functional and differential equations. Consider a function $f(z)$ satisfying the equation $f(z) = \sin(z) + f(z^2/4)$. If we represent $f(z)$ by its Maclaurin series $\sum a_n z^n$ and substitute this along with the known series for $\sin(z)$ into the equation, we obtain:
$\sum_{n=0}^{\infty}a_{n}z^{n} = \left(z - \frac{z^3}{3!} + \dots\right) + \sum_{n=0}^{\infty}a_{n}\left(\frac{z^2}{4}\right)^n = \sum_{j=0}^{\infty}\frac{(-1)^{j}}{(2j+1)!}z^{2j+1} + \sum_{n=0}^{\infty}\frac{a_n}{4^n} z^{2n}$
By equating the coefficients of like powers of $z$ on both sides, we can derive recurrence relations for the coefficients. For odd powers $n=2j+1$, we find $a_{2j+1} = \frac{(-1)^j}{(2j+1)!}$. For even powers $n=2m$, we find $a_{2m} = a_m/4^m$. This allows for the systematic computation of all coefficients [@problem_id:2285880].

Similarly, we can use this principle to determine unknown parameters in physical models. If one model predicts a function $f(x) = (1+2x)e^{3x}$ and another proposes a series $g(x) = \sum c_n x^n$ whose coefficients satisfy a [recurrence relation](@entry_id:141039) involving a parameter $\lambda$, such as $(n+1)c_{n+1} - (\lambda - 2n)c_n = 6c_{n-1}$, the models are consistent only if the coefficients of $f(x)$ satisfy this same recurrence. By computing the Maclaurin coefficients of $f(x)$ and substituting them into the recurrence, we can solve for the unique value of $\lambda$ that makes the equality hold for all $n$ [@problem_id:2333573].

Algebraic manipulations of [power series](@entry_id:146836) also rely on this principle. For instance, if $f(x) = (1 - \frac{x^2}{2})g(x)$, where $g(x) = \sum b_n x^n$, then the series for $f(x)$ is $f(x) = \sum b_n x^n - \frac{1}{2}\sum b_n x^{n+2}$. By re-indexing and combining terms, we find that the coefficient $a_n$ of $f(x)$ is related to the coefficients of $g(x)$ by the rule $a_n = b_n - \frac{1}{2}b_{n-2}$ (with $b_k$ defined as 0 for $k  0$). The uniqueness of the resulting series guarantees that this relationship is definitive [@problem_id:2333590]. This same principle is implicitly used when we derive the [power series](@entry_id:146836) for a function like $f(z) = \frac{2z-1}{z^2-4z+3}$ by first decomposing it into partial fractions and then summing the geometric series for each term. The resulting series is guaranteed to be *the* unique Maclaurin series for $f(z)$ within its [disk of convergence](@entry_id:177284) [@problem_id:2285901].

### The Principle of Analytic Continuation

The uniqueness theorem has a profound extension for analytic functions, known as the **Principle of Analytic Continuation** or the Identity Theorem for Analytic Functions. It establishes that the local behavior of an [analytic function](@entry_id:143459) on even a very small set can determine its global behavior across its entire domain of [analyticity](@entry_id:140716).

An analytic function is a function that is locally representable by a convergent power series. The theorem states that if two functions, $f(z)$ and $g(z)$, are analytic on a connected open set (a domain) $D$, and if they agree on a set of points that has a limit point within $D$, then they must be identical everywhere in $D$.

Let's explore the two most common scenarios for this principle:

1.  **Agreement on an Open Interval:** If $f(z)$ and $g(z)$ are analytic on a domain $D$ and we know that $f(x) = g(x)$ for all real $x$ in some open interval $(a, b) \subset D$, then we must have $f(z) \equiv g(z)$ throughout $D$. This is a powerful tool for extending results from the real line into the complex plane. For instance, if we solve a real differential equation like $(1+x^2) f'(x) - 2xf(x) = 0$ on an interval and find the solution $f(x) = C(1+x^2)$ [@problem_id:2285917], the [identity theorem](@entry_id:139624) guarantees that the only [analytic function](@entry_id:143459) on a larger complex domain that agrees with this solution on the real axis is $f(z) = C(1+z^2)$. This uniquely determines the function's values at all complex points in its domain of analyticity. The same principle applies when two different series representations, say one centered at $z=0$ and another at $z=1$, are known to represent the same underlying analytic function. Their equality on the overlapping region of convergence is a necessity, allowing us to treat them as different local descriptions of a single global entity [@problem_id:2285934].

2.  **Agreement on a Convergent Sequence:** The condition for uniqueness can be made even smaller. It is sufficient for $f(z)$ and $g(z)$ to agree on an infinite sequence of distinct points $\{z_k\}$ that converges to a point $z_0$ inside the domain $D$. The proof is an elegant application of the [power series](@entry_id:146836) [identity theorem](@entry_id:139624). Consider the function $h(z) = f(z) - g(z)$. We have $h(z_k) = 0$ for all $k$. Since [analytic functions](@entry_id:139584) are continuous, $h(z_0) = \lim_{k\to\infty} h(z_k) = 0$. Now, consider the Taylor series of $h(z)$ around $z_0$. If $h(z)$ were not identically zero, its series would have a first non-zero term, say $c_m(z-z_0)^m$. This would mean $h(z) \approx c_m(z-z_0)^m$ near $z_0$, implying that $z_0$ is an *isolated* zero. But this contradicts the fact that $h(z)$ is zero on the sequence $\{z_k\}$ converging to $z_0$. The only escape from this contradiction is that all coefficients of the Taylor series of $h(z)$ at $z_0$ must be zero. This makes $h(z)$ identically zero in a neighborhood of $z_0$, and by the argument in case 1, it must be zero throughout the entire domain $D$.

This powerful result means that if we know, for example, that two entire functions $f(x)$ and $g(x)=\cos(x)$ agree on the points $x_k=1/k$ for $k=1, 2, 3, \dots$, this is sufficient to conclude that $f(x) \equiv g(x)$ for all real (and complex) numbers. From this, we can determine all coefficients of the [power series](@entry_id:146836) for $f(x)$ [@problem_id:2333574] [@problem_id:2333584]. A classic and striking example of this is a function analytic in a disk around the origin which has zeros at every point $z_n = 1/n$. Since this sequence of zeros converges to a point within the disk (the origin), the function must be identically zero [@problem_id:2285946].

A finite version of this principle applies to polynomials. A polynomial of degree at most $N$ is uniquely determined by its values at $N+1$ distinct points. If two such polynomials, $P(z)$ and $Q(z)$, agree at $N+1$ points, their difference $D(z) = P(z) - Q(z)$ is a polynomial of degree at most $N$ with $N+1$ roots. The only such polynomial is the zero polynomial, so $D(z) \equiv 0$, which implies $P(z) \equiv Q(z)$ [@problem_id:2285883].

### Structural Consequences of Uniqueness

The [uniqueness of power series](@entry_id:139951) means that properties of a function must be reflected in the structure of its coefficients.

#### Symmetry: Even and Odd Functions
An [even function](@entry_id:164802) is one for which $f(x) = f(-x)$. If $f(x) = \sum a_n x^n$ is its Maclaurin series, then we must have:
$\sum_{n=0}^{\infty} a_n x^n = f(x) = f(-x) = \sum_{n=0}^{\infty} a_n (-x)^n = \sum_{n=0}^{\infty} a_n (-1)^n x^n$
By the [identity theorem](@entry_id:139624), the coefficients must match, so $a_n = a_n (-1)^n$. If $n$ is odd, this becomes $a_n = -a_n$, which implies $a_n = 0$. Thus, **the [power series](@entry_id:146836) of an even function contains only even powers of $x$**.

Conversely, an [odd function](@entry_id:175940) satisfies $f(x) = -f(-x)$. A similar argument shows that $a_n = -a_n(-1)^n$, which implies $a_n=0$ for all even $n$. Thus, **the power series of an odd function contains only odd powers of $x$**.

This property is extremely useful. For instance, knowing that $\sinh(x)$ is odd and $\cos(x)$ is even, we can immediately conclude that their product $h(x) = \sinh(x)\cos(x)$ is an [odd function](@entry_id:175940). Therefore, without any calculation, we know that all coefficients of even-powered terms in its Maclaurin series must be zero, e.g., $c_6 = 0$ [@problem_id:2333600]. Similarly, when constructing the even part of a function, $g_e(x) = \frac{g(x)+g(-x)}{2}$, we are guaranteed that its resulting power series will only have even-powered terms [@problem_id:2333575].

#### Reality: The Schwarz Reflection Principle
Consider a function $f(z)$ analytic in a neighborhood of the origin with a Maclaurin series $f(z) = \sum a_n z^n$. What is the consequence if all coefficients $a_n$ are real numbers? Let's compute the conjugate of $f(z)$:
$\overline{f(z)} = \overline{\sum_{n=0}^{\infty} a_n z^n} = \sum_{n=0}^{\infty} \overline{a_n z^n} = \sum_{n=0}^{\infty} \overline{a_n} \overline{z^n}$
Since $a_n$ are real, $\overline{a_n} = a_n$. Also, $\overline{z^n} = (\bar{z})^n$. This gives:
$\overline{f(z)} = \sum_{n=0}^{\infty} a_n (\bar{z})^n = f(\bar{z})$
This important identity, $\overline{f(z)} = f(\bar{z})$, is known as the **Schwarz Reflection Principle**. It states that for an analytic function whose [power series expansion](@entry_id:273325) along the real axis has only real coefficients, its value at a conjugate point $\bar{z}$ is the conjugate of its value at $z$ [@problem_id:2285944]. This principle formalizes the process of extending a real [analytic function](@entry_id:143459) into the complex plane.

### Boundaries and Extensions of the Principle

To fully appreciate the power of the [identity theorem](@entry_id:139624), it is crucial to understand its limitations and the breadth of its applicability.

#### Analytic vs. Infinitely Differentiable ($C^{\infty}$)
The uniqueness theorem applies to **analytic functions**—functions that are, by definition, locally equal to their [power series](@entry_id:146836). This class of functions is a strict subset of the infinitely differentiable functions (class $C^{\infty}$). There exist functions that have derivatives of all orders, yet are not represented by their Taylor series in any neighborhood of a point. The canonical example is [@problem_id:2333570]:
$$ f(x) = \begin{cases} \exp(-1/x^2)  \text{if } x \neq 0 \\ 0  \text{if } x = 0 \end{cases} $$
One can rigorously show that this function is in $C^{\infty}$ for all real $x$, and that all its derivatives at the origin are zero: $f^{(n)}(0) = 0$ for all $n \ge 0$. Consequently, its Maclaurin series is the zero series: $\sum 0 \cdot x^n = 0$. However, the function $f(x)$ is clearly not the zero function. This means $f(x)$ is not equal to its Maclaurin series on any [open interval](@entry_id:144029) containing the origin. This does not contradict the [identity theorem](@entry_id:139624) because the theorem's premise—that the function is represented by its power series—is not met. The existence of such functions highlights the special nature of analyticity.

#### Prerequisites for Representation
For a function to even be a candidate for a power [series representation](@entry_id:175860), it must satisfy strong smoothness conditions. In complex analysis, the condition is [analyticity](@entry_id:140716) ([complex differentiability](@entry_id:140243)), which is shown via the Cauchy-Riemann equations to be a very restrictive condition. For instance, the seemingly [simple function](@entry_id:161332) $f(z) = \text{Re}(z)$ is not analytic anywhere. Its limit definition of a derivative depends on the path of approach to a point. Since it is not analytic, it cannot be represented by a power series around any point [@problem_id:2285903].

#### Extension to Other Fields
The core argument for uniqueness—that the lowest-order non-zero coefficient can be isolated by factoring out a power of $x$ and taking a limit—does not fundamentally depend on the properties of real or complex numbers. It relies on the algebraic structure of power series and the [topological properties](@entry_id:154666) of a complete valued field. This means the Identity Theorem holds in other contexts, such as the field of **$p$-adic numbers**, $\mathbb{Q}_p$. If two [power series](@entry_id:146836) with rational coefficients converge on a $p$-adic disk $|x|_p \lt R$ and agree on a sequence of points $\{x_k\}$ converging to 0 in the $p$-adic metric, the same inductive argument proves that their coefficients must be identical [@problem_id:2333602]. This demonstrates that the [uniqueness of power series](@entry_id:139951) is a deep and fundamental algebraic and topological principle, extending far beyond its initial applications in calculus.