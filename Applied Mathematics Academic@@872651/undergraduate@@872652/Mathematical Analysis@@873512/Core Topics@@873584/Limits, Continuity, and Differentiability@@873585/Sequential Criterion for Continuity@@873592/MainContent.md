## Introduction
In the rigorous landscape of real analysis, continuity stands as a foundational concept, traditionally defined using the precise but often unwieldy epsilon-delta ($\varepsilon-\delta$) formulation. While essential, this definition can make proving the continuity or discontinuity of complex functions a challenging task. The **Sequential Criterion for Continuity** offers a powerful and frequently more intuitive alternative, reframing the abstract notion of a limit in the more concrete language of sequences. It addresses the need for a more versatile tool to dissect function behavior, especially at points of discontinuity or for functions with unusual definitions.

This article will guide you through this essential theorem. You will begin by exploring its formal statement and the core mechanisms for its application in the first chapter, **Principles and Mechanisms**. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate its utility in proving major theorems and reveal its connections to fields like topology and numerical analysis. Finally, the **Hands-On Practices** chapter will provide opportunities to apply these concepts and solidify your understanding. By working through these sections, you will gain a deep appreciation for why the [sequential criterion](@entry_id:158961) is an indispensable part of an analyst's toolkit.

## Principles and Mechanisms

In the study of real analysis, the concept of continuity is central. While the epsilon-delta ($\varepsilon-\delta$) definition provides a rigorous foundation, its application can sometimes be cumbersome. An alternative yet entirely equivalent perspective is offered by the **Sequential Criterion for Continuity**. This powerful tool reframes continuity in the language of sequences and their limits. It often provides more intuitive pathways for proofs and is particularly adept at dissecting the behavior of complex or unusually-defined functions. This chapter will explore the principles of this criterion and the mechanisms by which it is applied to establish continuity, prove discontinuity, and derive fundamental theorems about continuous functions.

### The Sequential Formulation of Continuity

The link between the [continuity of a function](@entry_id:147842) at a point and the behavior of sequences converging to that point is profound. The [sequential criterion](@entry_id:158961) formalizes this connection.

**Theorem (Sequential Criterion for Continuity):** A function $f: D \to \mathbb{R}$ is continuous at a point $c \in D$ if and only if for **every** sequence $(x_n)$ of points in its domain $D$ that converges to $c$, the corresponding sequence of function values $(f(x_n))$ converges to $f(c)$. Symbolically:
$$
\lim_{n \to \infty} x_n = c \implies \lim_{n \to \infty} f(x_n) = f(c)
$$

The "if and only if" nature of this theorem means it is not merely a consequence of continuity but a full-fledged alternative definition. The most critical component of this definition is the [universal quantifier](@entry_id:145989) "for every." The condition must hold for all sequences converging to $c$, not just some of them.

To appreciate the importance of this, consider a function that is deliberately constructed to be discontinuous at $c=0$, yet satisfies the condition for a single, specific sequence. For example, let the sequence be $(x_n)$ with $x_n = 1/n$. We can define a function [@problem_id:1322066]:
$$
f(x) = \begin{cases} 0 & \text{if } x=0 \text{ or } x=1/k \text{ for some integer } k \neq 0 \\ 1 & \text{otherwise} \end{cases}
$$
Here, $f(0) = 0$. For the sequence $x_n=1/n$, we have $f(x_n) = 0$ for all $n$, so $\lim_{n \to \infty} f(x_n) = 0 = f(0)$. This single sequence behaves as expected. However, the function is not continuous at $0$. To see this, we can choose another sequence that also converges to $0$, such as $y_n = \frac{1}{n+1/2} = \frac{2}{2n+1}$. None of these terms are of the form $1/k$ for an integer $k$. Thus, $f(y_n) = 1$ for all $n$. This sequence of function values converges to $1$, which is not equal to $f(0)$. Because we have found a sequence $(y_n)$ converging to $0$ for which $(f(y_n))$ does not converge to $f(0)$, the function is discontinuous at $0$. This illustrates that continuity requires a robust connection that holds universally for all paths of approach.

### Applying Continuity: The Limit Interchange Rule

The "forward" implication of the [sequential criterion](@entry_id:158961) is a highly practical tool: if a function is known to be continuous at a point, it preserves [limits of sequences](@entry_id:159667) converging to that point. This effectively allows for an interchange of the function and limit operations:
$$
\lim_{n \to \infty} f(x_n) = f \left( \lim_{n \to \infty} x_n \right)
$$

This rule is invaluable for evaluating the limits of complex sequences. If we can express a sequence $(y_n)$ as the composition $y_n = f(x_n)$ where $f$ is a continuous function and the limit of $(x_n)$ is known, the problem is greatly simplified.

For instance, consider the task of finding the limit of the sequence $y_n = f(x_n)$ where $f(x) = \frac{2x+1}{x-3}$ and $x_n = \frac{4n+1}{n}$ [@problem_id:2315299]. Instead of substituting the expression for $x_n$ into $f(x)$ and dealing with a complex fraction, we can proceed in two steps. First, find the limit of $(x_n)$:
$$
\lim_{n \to \infty} x_n = \lim_{n \to \infty} \left(4 + \frac{1}{n}\right) = 4
$$
Second, we recognize that $f(x)$ is a rational function and is therefore continuous at every point where its denominator is non-zero. At $x=4$, the denominator is $4-3=1 \neq 0$, so $f$ is continuous at $4$. We can now apply the limit interchange rule:
$$
\lim_{n \to \infty} y_n = \lim_{n \to \infty} f(x_n) = f \left( \lim_{n \to \infty} x_n \right) = f(4) = \frac{2(4)+1}{4-3} = 9
$$
This principle extends to any combination of continuous functions, such as sums, products, and compositions, which are themselves continuous (a topic we will prove later in this chapter). For example, to find the limit of $S(x_n)$ where $S(x) = \exp(2x) + \cos(\pi x)$ and $x_n = \frac{n^2 - n \sin(n)}{2n^2 + 1}$, we first determine that $\lim_{n \to \infty} x_n = 1/2$. Since $S(x)$ is a sum of continuous functions, it is continuous everywhere. Therefore, the limit is simply $S(1/2) = \exp(1) + \cos(\pi/2) = \exp(1)$ [@problem_id:1322046].

### Proving Continuity with Sequences

The "backward" implication of the criterion provides a template for proving that a function is continuous. To establish [continuity at a point](@entry_id:148440) $c$, we assume we have an arbitrary sequence $(x_n)$ converging to $c$ and then demonstrate, using the properties of $f$, that the sequence $(f(x_n))$ must converge to $f(c)$.

A fundamental example is proving the continuity of the [absolute value function](@entry_id:160606), $f(x)=|x|$, at an arbitrary point $c \in \mathbb{R}$ [@problem_id:1322067]. Let $(x_n)$ be any sequence such that $\lim_{n \to \infty} x_n = c$. Our goal is to show that $\lim_{n \to \infty} |x_n| = |c|$. This is equivalent to showing that $\lim_{n \to \infty} ||x_n| - |c|| = 0$. The key is to employ the **Reverse Triangle Inequality**, which states that for any real numbers $a$ and $b$, $||a| - |b|| \le |a-b|$. Applying this, we have:
$$
0 \le ||x_n| - |c|| \le |x_n - c|
$$
Since we assumed $x_n \to c$, we know that $\lim_{n \to \infty} |x_n - c| = 0$. By the Squeeze Theorem, the term in the middle, $||x_n| - |c||$, must also converge to $0$. This implies $\lim_{n \to \infty} |x_n| = |c|$, which proves that $f(x)=|x|$ is continuous.

This method is particularly effective for functions that satisfy a **Lipschitz condition**. A function $f$ is Lipschitz continuous if there exists a constant $K > 0$ such that for all $x, y$ in the domain, $|f(x) - f(y)| \le K|x - y|$. Let's prove that any such function is continuous everywhere [@problem_id:2315308]. Let $c$ be an arbitrary point, and let $(x_n)$ be any sequence converging to $c$. We have:
$$
0 \le |f(x_n) - f(c)| \le K|x_n - c|
$$
As $n \to \infty$, we have $|x_n - c| \to 0$. Since $K$ is a fixed constant, $K|x_n - c| \to 0$. Once again, by the Squeeze Theorem, we conclude that $|f(x_n) - f(c)| \to 0$, which is the definition of $f(x_n) \to f(c)$. Thus, Lipschitz continuity implies continuity.

### Proving Discontinuity: The Power of a Single Counterexample

The [sequential criterion](@entry_id:158961) is an especially potent tool for proving a function is *discontinuous*. According to the logic of the criterion (its contrapositive form), to show that $f$ is not continuous at $c$, one only needs to find a *single* sequence $(x_n)$ in the domain such that $x_n \to c$, but the sequence of function values $(f(x_n))$ fails to converge to $f(c)$.

This failure can manifest in several ways:

**1. Convergence to the Wrong Limit:** The sequence $(f(x_n))$ converges, but its limit is not $f(c)$. This typically occurs in functions with **jump discontinuities**. For example, consider the function [@problem_id:1292116]:
$$
f(x) = \begin{cases} \cos(\pi x) & \text{if } x \le 1/2 \\ 2x - 2 & \text{if } x > 1/2 \end{cases}
$$
At the point $c=1/2$, the function value is $f(1/2) = \cos(\pi/2) = 0$. To show discontinuity, we can choose a sequence that approaches $1/2$ from the right, for instance, $x_n = 1/2 + 1/n$. Clearly, $x_n \to 1/2$. For this sequence, all terms are greater than $1/2$, so we use the second piece of the function's definition:
$$
f(x_n) = 2(1/2 + 1/n) - 2 = 1 + 2/n - 2 = -1 + 2/n
$$
As $n \to \infty$, we have $\lim_{n \to \infty} f(x_n) = -1$. Since this limit, $-1$, is not equal to $f(1/2) = 0$, the function is discontinuous at $c=1/2$.

**2. Divergence by Oscillation:** The sequence $(f(x_n))$ may fail to converge altogether, for instance, by oscillating between two or more values. A classic example is the [signum function](@entry_id:167507) at $c=0$ [@problem_id:2315327]. A clever choice of sequence is $x_n = \frac{(-1)^n}{n}$. This sequence converges to $0$. However, the function values $f(x_n)$ alternate:
- For even $n$, $x_n = 1/n > 0$, so $f(x_n) = 1$.
- For odd $n$, $x_n = -1/n  0$, so $f(x_n) = -1$.
The resulting sequence of function values is $( -1, 1, -1, 1, \dots )$, which is divergent. Since $(f(x_n))$ does not converge, it certainly cannot converge to $f(0)=0$, proving discontinuity. A similar phenomenon occurs with the [ceiling function](@entry_id:262460) $f(x) = \lceil x \rceil$ at any integer point, such as $c=1$. A sequence like $a_n = 1 + \frac{(-1)^n}{n+1}$ approaches $1$ from both above (for even $n$) and below (for odd $n$), causing the values $f(a_n)$ to oscillate between $2$ and $1$, thus diverging [@problem_id:1322059].

**3. Divergence to Infinity:** The sequence $(f(x_n))$ may be unbounded. Consider the function $f(x) = \frac{1}{\sin^2(x)}$ near $c=0$ [@problem_id:2315307]. The function is not defined at $0$, so continuity is not in question, but we can analyze the limit. Let's choose the sequence $x_n = 1/n$, which converges to $0$. As $n \to \infty$, $x_n \to 0$, and $\sin^2(x_n)$ approaches $0$ through positive values. Consequently, the reciprocal $f(x_n) = \frac{1}{\sin^2(1/n)}$ diverges to $+\infty$. This demonstrates a failure of the limit to exist as a finite number.

### Continuity for Functions on Dense Sets

The [sequential criterion](@entry_id:158961) is particularly revealing when analyzing functions with complex definitions, especially those defined differently for rational and [irrational numbers](@entry_id:158320). The key insight stems from the fact that both the set of rational numbers, $\mathbb{Q}$, and the set of irrational numbers, $\mathbb{R} \setminus \mathbb{Q}$, are **dense** in $\mathbb{R}$. This means that for any real number $c$, we can find a sequence of rational numbers that converges to $c$, and we can also find a sequence of [irrational numbers](@entry_id:158320) that converges to $c$. For a function to be continuous at $c$, the limit of the image sequences must be the same, regardless of which type of sequence we choose.

A famous example is the **Dirichlet function** [@problem_id:2315319]:
$$
f(x) = \begin{cases} 1  \text{if } x \in \mathbb{Q} \\ 0  \text{if } x \notin \mathbb{Q} \end{cases}
$$
This function is discontinuous everywhere. To prove this, let $c$ be any real number.
- If $c$ is rational, $f(c)=1$. We can choose a sequence of irrational numbers $(r_n)$ such that $r_n \to c$. Then $f(r_n) = 0$ for all $n$, so $\lim f(r_n) = 0$. Since $0 \neq f(c)$, $f$ is discontinuous at $c$.
- If $c$ is irrational, $f(c)=0$. We can choose a sequence of rational numbers $(q_n)$ such that $q_n \to c$. Then $f(q_n) = 1$ for all $n$, so $\lim f(q_n) = 1$. Since $1 \neq f(c)$, $f$ is discontinuous at $c$.
Since $c$ was arbitrary, the function is nowhere continuous.

A more nuanced situation arises when the two parts of the function's definition can "meet." Consider the function [@problem_id:1870023]:
$$
f(x) = \begin{cases} x^{2} + 2x  \text{if } x \in \mathbb{Q} \\ 4x - 1  \text{if } x \notin \mathbb{Q} \end{cases}
$$
For $f$ to be continuous at a point $c$, the limit along a rational sequence must equal the limit along an irrational sequence. Assuming the two pieces (a polynomial and a linear function) are themselves continuous, this means we must have:
$$
\lim_{q_n \to c} (q_n^2 + 2q_n) = \lim_{r_n \to c} (4r_n - 1)
$$
$$
c^2 + 2c = 4c - 1
$$
Solving this equation gives $c^2 - 2c + 1 = 0$, or $(c-1)^2 = 0$, which yields $c=1$ as the only *possible* point of continuity. At $c=1$, both rules give the value $1^2+2(1)=3$ and $4(1)-1=3$. Since any sequence $(x_n) \to 1$, whether rational or irrational, results in $f(x_n)$ approaching $3$, the function is indeed continuous at $x=1$ and nowhere else.

This principle reaches its apex with **Thomae's function**, which exhibits a surprising behavior. It is defined as $f(x)=0$ if $x$ is irrational, and $f(x)=1/q$ if $x=p/q$ is a rational number in lowest terms ($q>0$) [@problem_id:2315302]. One can show that for any real number $c$, $\lim_{x \to c} f(x) = 0$.
- If $c$ is irrational, then $f(c)=0$. Since the limit matches the function value, Thomae's function is continuous at every irrational number.
- If $c$ is rational, $c=p/q$, then $f(c)=1/q > 0$. Since the limit is $0$, which does not equal $f(c)$, the function is discontinuous at every rational number. This is a **[removable discontinuity](@entry_id:146730)** [@problem_id:1322061], because redefining $f(c)$ to be $0$ would make the function continuous at that point.

### The Sequential Criterion in Action: Proving Fundamental Theorems

The elegance of the [sequential criterion](@entry_id:158961) is most apparent when proving the fundamental properties of continuous functions. The proofs often become simple applications of the corresponding [limit theorems for sequences](@entry_id:140340).

#### Algebra of Continuous Functions

Let $f$ and $g$ be functions continuous at a point $c$.
- **Sum:** The function $(f+g)(x) = f(x)+g(x)$ is continuous at $c$.
  *Proof:* Let $(x_n)$ be any sequence converging to $c$. By the continuity of $f$ and $g$, we know $f(x_n) \to f(c)$ and $g(x_n) \to g(c)$. By the Algebraic Limit Theorem for sequences, the sum of these sequences converges to the sum of their limits:
  $$ \lim_{n \to \infty} (f+g)(x_n) = \lim_{n \to \infty} (f(x_n) + g(x_n)) = \lim_{n \to \infty} f(x_n) + \lim_{n \to \infty} g(x_n) = f(c) + g(c) = (f+g)(c) $$
  Thus, $f+g$ is continuous at $c$.

- **Quotient:** The function $(f/g)(x) = f(x)/g(x)$ is continuous at $c$, provided $g(c) \neq 0$.
  *Proof:* Let $(x_n)$ be any sequence in the domain of $f/g$ converging to $c$. This means $g(x_n) \neq 0$ for all $n$. As before, $f(x_n) \to f(c)$ and $g(x_n) \to g(c)$. An argument might proceed by directly applying the [quotient rule for limits](@entry_id:157988) of sequences. However, this rule requires that the denominator sequence terms are all non-zero, and the limit of the denominator is non-zero. While we are given $g(c) \neq 0$, it is not guaranteed that $g(x_n) \neq 0$ for every term in *any* sequence converging to $c$. This represents a subtle but crucial gap in a naive proof [@problem_id:2315295].
  The correct justification is as follows: Since $g$ is continuous at $c$ and $g(c) \neq 0$, it can be shown that there exists an $N \in \mathbb{N}$ such that for all $n \ge N$, $g(x_n) \neq 0$. The [quotient rule](@entry_id:143051) for sequence limits can then be applied to the tail of the sequence, which is sufficient to establish the limit.
  $$ \lim_{n \to \infty} \frac{f(x_n)}{g(x_n)} = \frac{\lim_{n \to \infty} f(x_n)}{\lim_{n \to \infty} g(x_n)} = \frac{f(c)}{g(c)} = (f/g)(c) $$

#### Composition of Continuous Functions

The sequential proof for the [continuity of composite functions](@entry_id:146868) is particularly clear [@problem_id:2315317].
- **Composition:** If $f$ is continuous at $c$, and $g$ is continuous at $f(c)$, then the [composite function](@entry_id:151451) $(g \circ f)(x) = g(f(x))$ is continuous at $c$.
  *Proof:* Let $(x_n)$ be any sequence converging to $c$.
  1. Since $f$ is continuous at $c$, the sequence of image points $(f(x_n))$ converges to $f(c)$.
  2. Let's call this new sequence $(y_n)$, where $y_n = f(x_n)$. We now have a sequence $(y_n)$ that converges to the point $f(c)$.
  3. Since $g$ is continuous at the point $f(c)$, we can apply the [sequential criterion](@entry_id:158961) to $g$ and the sequence $(y_n)$. This gives us $\lim_{n \to \infty} g(y_n) = g(f(c))$.
  4. Substituting back $y_n = f(x_n)$, we have $\lim_{n \to \infty} g(f(x_n)) = g(f(c))$, which is precisely the statement that $\lim_{n \to \infty} (g \circ f)(x_n) = (g \circ f)(c)$. Thus, $g \circ f$ is continuous at $c$.

#### Preservation of Order and Sign

Continuity also guarantees that inequalities are preserved in the limit.
- **Order Preservation:** If $f$ is continuous at $c$ and there is a sequence $x_n \to c$ such that $f(x_n) \ge M$ for all $n$, then it must be that $f(c) \ge M$. This follows directly from the order limit theorem for sequences: $f(c) = \lim f(x_n)$, and the [limit of a sequence](@entry_id:137523) of numbers greater than or equal to $M$ must also be greater than or equal to $M$. This principle is useful for determining function values when its behavior on a sequence is bounded [@problem_id:2315313].

- **Sign Preservation:** A strictly stronger result is that a continuous function preserves *strict* inequality in a neighborhood. If $f$ is continuous at $c$ and $f(c) > 0$, then there exists a $\delta > 0$ such that $f(x) > 0$ for all $x$ in the domain satisfying $|x-c|  \delta$ [@problem_id:1322039].
  *Proof by Contradiction:* Suppose this is false. Then for any $\delta > 0$, we can find an $x$ with $|x-c|\delta$ and $f(x) \le 0$. We can use this to construct a sequence. For each $n \in \mathbb{N}$, let $\delta_n = 1/n$. There must exist a point $x_n$ such that $|x_n - c|  1/n$ and $f(x_n) \le 0$. The sequence $(x_n)$ constructed this way clearly converges to $c$. Since $f$ is continuous at $c$, we must have $f(x_n) \to f(c)$. But since $f(x_n) \le 0$ for all $n$, the Order Preservation principle implies that its limit must be less than or equal to $0$, so $f(c) \le 0$. This contradicts our initial assumption that $f(c) > 0$. Therefore, the assumption must be false, and there must exist a neighborhood around $c$ where $f(x)$ is strictly positive.

### The Importance of the Domain: Continuity on Discrete Sets

Finally, the [sequential criterion](@entry_id:158961) brilliantly illuminates how the topological nature of the domain influences continuity. Consider a function whose domain is the set of integers, $f: \mathbb{Z} \to \mathbb{R}$ [@problem_id:2315291]. Let's test for continuity at an arbitrary integer $c \in \mathbb{Z}$.

We must consider any sequence $(x_k)$ of integers such that $x_k \to c$. What does it mean for a sequence of integers to converge to an integer? For any $\varepsilon > 0$, there must be an $N$ such that for $k \ge N$, $|x_k - c|  \varepsilon$. If we choose $\varepsilon = 1/2$, the inequality $|x_k - c|  1/2$, where both $x_k$ and $c$ are integers, has only one solution: $x_k = c$.

This means that any sequence of integers that converges to an integer must be **eventually constant**; that is, there exists an $N$ such that $x_k = c$ for all $k \ge N$.
Now consider the sequence of function values, $(f(x_k))$. For all $k \ge N$, we have $f(x_k) = f(c)$. This sequence is also eventually constant, so it trivially converges to $f(c)$.
$$
\lim_{k \to \infty} f(x_k) = f(c)
$$
Since this holds for any sequence $(x_k)$ in $\mathbb{Z}$ converging to $c$, the function $f$ is continuous at $c$. And since $c$ was an arbitrary integer, **every function with the domain $\mathbb{Z}$ is continuous**. The isolated nature of the points in the domain ensures that the condition for [sequential continuity](@entry_id:137310) is always satisfied. This surprising result underscores that continuity is not a property of the function alone, but a property of the function in relation to its domain.