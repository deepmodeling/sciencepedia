## Introduction
In functional analysis, the study of [linear operators](@entry_id:149003) often revolves around the crucial property of continuity, also known as [boundedness](@entry_id:746948). While proving continuity directly by finding a bound can be challenging, a profound result known as the Closed Graph Theorem offers a powerful alternative. This theorem forges a deep link between the continuity of an operator and a more accessible [topological property](@entry_id:141605): the closedness of its graph. This article addresses the central question: under what conditions does having a [closed graph](@entry_id:154162) guarantee that an operator is continuous?

To explore this question, this article is structured to build your understanding from the ground up. The first chapter, **Principles and Mechanisms**, will introduce the foundational concepts, including the [graph of an operator](@entry_id:271574), the definition of a [closed operator](@entry_id:274252), and the pivotal role of Banach spaces, culminating in the formal statement and proof of the theorem. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the theorem's immense utility by applying it to [integral operators](@entry_id:187690), [spectral theory](@entry_id:275351), and even foundational principles in quantum mechanics. Finally, the **Hands-On Practices** chapter provides an opportunity to solidify these concepts through guided problems. We begin by laying the necessary groundwork for understanding this cornerstone of analysis.

## Principles and Mechanisms

In the study of linear operators between [normed spaces](@entry_id:137032), a central theme is the distinction between algebraic and topological properties. While linearity is a purely algebraic concept, properties like continuity (or boundedness) are topological. The Closed Graph Theorem provides a profound bridge between a topological property of an operator's graph and the operator's continuity. To understand this theorem, we must first systematically build the requisite concepts, starting with the graph itself.

### The Graph of a Linear Operator

Let $X$ and $Y$ be [normed vector spaces](@entry_id:274725) over the same field (typically $\mathbb{R}$ or $\mathbb{C}$). The Cartesian product $X \times Y$ is the set of all [ordered pairs](@entry_id:269702) $(x, y)$ where $x \in X$ and $y \in Y$. This product set can be endowed with a vector space structure through component-wise addition and scalar multiplication. Furthermore, we can define a norm on $X \times Y$ that makes it a [normed space](@entry_id:157907). While several [equivalent norms](@entry_id:268877) exist, a common choice is a product norm, such as the sum norm $\|(x,y)\| = \|x\|_X + \|y\|_Y$ or the Euclidean-like norm $\|(x,y)\| = \sqrt{\|x\|_X^2 + \|y\|_Y^2}$. Convergence of a sequence $(x_n, y_n)$ to $(x,y)$ in the [product space](@entry_id:151533) is equivalent to the [component-wise convergence](@entry_id:158444): $x_n \to x$ in $X$ and $y_n \to y$ in $Y$.

For instance, consider the space $Z = X \times Y$ where $X = C([0, 1])$ is the [space of continuous functions](@entry_id:150395) on $[0,1]$ with the [supremum norm](@entry_id:145717) $\|f\|_\infty$, and $Y = \ell^2$ is the space of square-summable sequences with the norm $\|a\|_2$. The norm of an element $(f, a) \in Z$ under the Euclidean-like product norm would be $\|(f, a)\|_Z = \sqrt{\|f\|_\infty^2 + \|a\|_2^2}$. If we take the specific function $f(t) = 4t^2 - 4t + 2$ and the sequence $a_n = (1/\sqrt{2})^n$, we can compute the norms of the components. The maximum of $f(t)$ on $[0,1]$ is $2$, so $\|f\|_\infty = 2$. The [sum of squares](@entry_id:161049) for the sequence is a geometric series: $\sum_{n=1}^\infty ( (1/\sqrt{2})^n )^2 = \sum_{n=1}^\infty (1/2)^n = 1$, so $\|a\|_2 = 1$. The norm of the pair in the product space is therefore $\|(f, a)\|_Z = \sqrt{2^2 + 1^2} = \sqrt{5}$ [@problem_id:2321457]. This construction of a normed [product space](@entry_id:151533) is the essential setting for defining the graph.

The **graph** of a [linear operator](@entry_id:136520) $T: D(T) \subseteq X \to Y$ is the subset of the [product space](@entry_id:151533) $X \times Y$ defined as:
$$
G(T) = \{ (x, Tx) \in X \times Y \mid x \in D(T) \}
$$
A crucial preliminary observation is that if $T$ is a **linear** operator, its graph $G(T)$ is a **linear subspace** of the [product space](@entry_id:151533) $X \times Y$. To verify this, one must check the three conditions for a subspace:
1.  The [zero vector](@entry_id:156189) $(0_X, 0_Y)$ is in $G(T)$, which is true since $T(0_X) = 0_Y$ for any [linear operator](@entry_id:136520).
2.  It is closed under addition: For any $(x_1, Tx_1)$ and $(x_2, Tx_2)$ in $G(T)$, their sum is $(x_1+x_2, Tx_1+Tx_2)$. By linearity, this is equal to $(x_1+x_2, T(x_1+x_2))$, which is also in $G(T)$.
3.  It is closed under scalar multiplication: For any $(x, Tx) \in G(T)$ and any scalar $c$, the multiple $c(x, Tx) = (cx, cTx)$ is equal to $(cx, T(cx))$ by linearity, and thus belongs to $G(T)$ [@problem_id:2321461].

This confirms that the graph of a [linear operator](@entry_id:136520) is not merely a set but carries the algebraic structure of a [vector subspace](@entry_id:151815). The central questions of this chapter, however, concern its topological properties.

### Closed Operators and the Sequential Criterion

In a [metric space](@entry_id:145912), a set is defined as **closed** if it contains all of its [limit points](@entry_id:140908). Since the [product space](@entry_id:151533) $X \times Y$ is a normed (and thus metric) space, we can apply this definition to the graph $G(T)$. An operator $T$ is called a **[closed operator](@entry_id:274252)** if its graph $G(T)$ is a closed subset of $X \times Y$.

Translating the general definition of a [closed set](@entry_id:136446) into the language of sequences provides a more practical criterion. A set is closed if and only if for every convergent sequence of points within the set, the [limit point](@entry_id:136272) also belongs to the set. Applying this to the graph $G(T)$, and recalling that convergence in $X \times Y$ is component-wise, we arrive at the fundamental sequential characterization of a [closed operator](@entry_id:274252) [@problem_id:2321471] [@problem_id:1896778]:

A [linear operator](@entry_id:136520) $T: D(T) \subseteq X \to Y$ is **closed** if, for any sequence $(x_n)$ of elements in its domain $D(T)$ that satisfies two conditions:
1.  $x_n \to x$ for some $x \in X$,
2.  $Tx_n \to y$ for some $y \in Y$,
it necessarily follows that $x \in D(T)$ and $y = Tx$.

It is vital to distinguish this property from continuity. An operator $T$ is continuous if for any convergent sequence $x_n \to x$ in its domain, the image sequence $Tx_n$ is guaranteed to converge to $Tx$. The definition of a [closed operator](@entry_id:274252) is weaker. It does not demand that $Tx_n$ converges whenever $x_n$ does. Instead, it imposes a consistency condition: *if* the sequence of images $Tx_n$ happens to converge to some limit $y$, then that limit must be the "correct" one, namely $Tx$.

### The Link Between Boundedness and Closed Graphs

We can now explore the relationship between the familiar concept of a bounded (continuous) linear operator and the new concept of a [closed operator](@entry_id:274252).

#### Boundedness Implies a Closed Graph

There is a straightforward implication that holds in any [normed space](@entry_id:157907) setting: every [bounded linear operator](@entry_id:139516) with a domain that is all of $X$ has a [closed graph](@entry_id:154162). The proof relies directly on the definition of continuity.

Let $T: X \to Y$ be a [bounded linear operator](@entry_id:139516). To show its graph $G(T)$ is closed, we take a sequence $(x_n)$ in $X$ such that $x_n \to x$ and $Tx_n \to y$. Because $T$ is bounded, it is continuous. Therefore, the convergence $x_n \to x$ implies that $Tx_n \to Tx$. In a [normed space](@entry_id:157907), limits are unique. Since the sequence $Tx_n$ converges to both $y$ and $Tx$, we must have $y = Tx$. This shows that the limit point $(x,y)$ is in fact $(x, Tx)$, which belongs to $G(T)$. Thus, the graph is closed [@problem_id:1887480].

#### Does a Closed Graph Imply Boundedness?

The converse of this statement—whether a [closed graph](@entry_id:154162) implies [boundedness](@entry_id:746948)—is far more subtle and constitutes the heart of the Closed Graph Theorem. In general, the answer is **no**. An operator can have a [closed graph](@entry_id:154162) yet be unbounded if the underlying spaces lack the crucial property of completeness.

Consider the [identity operator](@entry_id:204623) $T: X \to Y$ where $X = (C[0,1], \|\cdot\|_1)$ and $Y = (C[0,1], \|\cdot\|_\infty)$. Here, $T(f)=f$.
-   **$T$ is unbounded**: We can find a [sequence of functions](@entry_id:144875), such as tall, narrow spikes, for which the $L^1$-norm (area) is constant but the supremum norm (height) grows indefinitely. For example, the function $f_n(x)$ which is a triangle of height $n$ and base $2/n$ has $\|f_n\|_1 = 1$ but $\|f_n\|_\infty = n$. The ratio $\|Tf_n\|_\infty / \|f_n\|_1 = n$ can be arbitrarily large.
-   **$G(T)$ is closed**: Suppose a sequence $f_n \in C[0,1]$ converges such that $f_n \to f$ in the $L^1$-norm and $Tf_n = f_n \to g$ in the [supremum norm](@entry_id:145717). Convergence in the [supremum norm](@entry_id:145717) is stronger than and implies convergence in the $L^1$-norm. So, $f_n \to g$ in the $L^1$-norm as well. By the [uniqueness of limits](@entry_id:142343) in $(C[0,1], \|\cdot\|_1)$, we must have $f=g$. Thus, the limit point $(f,g)$ is $(f,f)$, which is in the graph of $T$.

Here we have an [unbounded operator](@entry_id:146570) with a [closed graph](@entry_id:154162). This does not violate any theorem because the domain space $X = (C[0,1], \|\cdot\|_1)$ is not a [complete space](@entry_id:159932) (i.e., not a Banach space) [@problem_id:2321453]. A similar conclusion can be drawn from the operator $T((x_n)) = (nx_n)$ on the space $c_{00}$ of finitely non-zero sequences; the operator is unbounded, its graph is closed, but the space $c_{00}$ with the [supremum norm](@entry_id:145717) is not complete [@problem_id:2321475]. These examples highlight the necessity of completeness in the domain. Likewise, one can construct examples showing that the completeness of the codomain is also necessary [@problem_id:1887459].

### The Closed Graph Theorem

The examples above demonstrate that the implication "[closed graph](@entry_id:154162) $\implies$ bounded" requires additional hypotheses on the spaces $X$ and $Y$. The missing ingredient is completeness. This leads us to the statement of the theorem itself.

**The Closed Graph Theorem**: Let $X$ and $Y$ be **Banach spaces** and let $T: X \to Y$ be a linear operator defined on all of $X$. Then $T$ is bounded if and only if its graph $G(T)$ is a closed subset of $X \times Y$.

As we have seen, the implication from [boundedness](@entry_id:746948) to a [closed graph](@entry_id:154162) is always true. The power of the theorem lies in the converse: for linear operators defined everywhere between two Banach spaces, the seemingly weaker condition of having a [closed graph](@entry_id:154162) is sufficient to guarantee [boundedness](@entry_id:746948).

The proof of this non-trivial direction relies on another major result in functional analysis, the Bounded Inverse Theorem. A sketch of the argument is as follows [@problem_id:2321487]:
1.  If $X$ and $Y$ are Banach spaces, their product $X \times Y$ is also a Banach space.
2.  If $G(T)$ is a closed subset of the Banach space $X \times Y$, it is a closed linear subspace and is therefore itself a Banach space.
3.  Consider the projection map $\pi_X: G(T) \to X$ defined by $\pi_X(x, Tx) = x$. This map is linear, bounded, and bijective.
4.  Since both $G(T)$ and $X$ are Banach spaces, the Bounded Inverse Theorem applies to $\pi_X$, ensuring that its inverse $\pi_X^{-1}: X \to G(T)$ is also bounded.
5.  The [boundedness](@entry_id:746948) of $\pi_X^{-1}(x) = (x, Tx)$ means there exists a constant $C$ such that $\|(x, Tx)\|_{X \times Y} \le C\|x\|_X$. This expands to $\|x\|_X + \|Tx\|_Y \le C\|x\|_X$, which directly implies $\|Tx\|_Y \le (C-1)\|x\|_X$. Thus, $T$ is bounded.

The practical utility of this theorem is immense. In many situations, verifying that an operator's graph is closed using the [sequential criterion](@entry_id:158961) is more direct than proving [boundedness](@entry_id:746948) from the definition $\|Tx\| \le C\|x\|$, which may require finding an explicit and often non-obvious constant $C$ [@problem_id:2321444]. For example, if it is given that an operator like $Tf(x) = f(\sqrt{x})$ on the Banach space $L^2[0,1]$ has a [closed graph](@entry_id:154162), the theorem immediately assures us that $T$ is bounded, and we can then proceed to calculate its norm, which turns out to be $\sqrt{2}$ [@problem_id:2321448].

### Consequences and Related Concepts

The Closed Graph Theorem and the properties of closed operators have several important consequences.

#### Properties of Closed Operators

-   **Kernel**: If a [linear operator](@entry_id:136520) $T: X \to Y$ between [normed spaces](@entry_id:137032) has a [closed graph](@entry_id:154162), its kernel, $\ker(T) = \{ x \in X \mid Tx=0 \}$, must be a [closed subspace](@entry_id:267213) of $X$. This can be proven by observing that $\ker(T)$ is the [inverse image](@entry_id:154161) of the closed set $G(T)$ under the [continuous map](@entry_id:153772) $i: X \to X \times Y$ given by $i(x) = (x, 0)$ [@problem_id:2321466].
-   **Inverse**: If an injective linear operator $T: X \to Y$ has a [closed graph](@entry_id:154162), then its inverse $T^{-1}: \mathrm{Im}(T) \to X$ also has a [closed graph](@entry_id:154162). This follows from viewing the graph of $T^{-1}$ as the image of the graph of $T$ under the isometric [homeomorphism](@entry_id:146933) $S: X \times Y \to Y \times X$ defined by $S(x,y) = (y,x)$ [@problem_id:2321479].
-   **Linear Functionals**: For a [linear functional](@entry_id:144884) $f: X \to \mathbb{R}$ on a Banach space $X$, having a [closed graph](@entry_id:154162) is equivalent to being continuous, which is also equivalent to having a closed kernel. This provides a particularly sharp criterion for the continuity of functionals [@problem_id:1887481].

#### Applications of the Theorem

The Closed Graph Theorem can be used to deduce properties of operators and spaces.
-   **Sums of Operators**: If $S$ and $T$ are two linear operators from a Banach space $X$ to a Banach space $Y$, and both have closed graphs, then their sum $R = S+T$ also has a [closed graph](@entry_id:154162). This is because, by the Closed Graph Theorem, $S$ and $T$ must be bounded. The sum of two [bounded operators](@entry_id:264879) is bounded, and any [bounded operator](@entry_id:140184) has a [closed graph](@entry_id:154162) [@problem_id:1887458].
-   **Projections**: Consider a Banach space $X$ that is an algebraic direct sum $X = M \oplus N$, where $M$ is a [closed subspace](@entry_id:267213) but $N$ is not. The projection operator $P$ onto $M$ along $N$ has $\ker(P) = N$. Since the kernel is not closed, $P$ cannot be a [continuous operator](@entry_id:143297). By the contrapositive of the Closed Graph Theorem, its graph cannot be closed. This provides a powerful link between the geometric configuration of subspaces and the analytic properties of the associated projection [@problem_id:1887490].

### Closable Operators and Adjoints

Not all useful operators in analysis are closed. A prominent example is the differentiation operator $Tf = f'$ with domain $D(T) = C^1[0,1]$ viewed as a subspace of $L^2[0,1]$. This operator is not closed because one can construct a sequence of $C^1$ functions that converges in the $L^2$-norm to a function that is not continuously differentiable (e.g., a sequence converging to a function with a 'corner') [@problem_id:2321436].

This leads to the idea of a **[closable operator](@entry_id:271727)**. A [densely defined operator](@entry_id:264952) $T$ is closable if the closure of its graph, $\overline{G(T)}$, is the graph of a well-defined operator, which we denote by $\overline{T}$. This is equivalent to the condition that for any sequence $(x_n)$ in $D(T)$ with $x_n \to 0$ and $Tx_n \to y$, it must be that $y=0$. This condition prevents the closure of the graph from assigning multiple values to a single point. The [differentiation operator](@entry_id:140145) on $C^1[0,1]$ is not closed, but it is closable. Its closure, $\overline{T}$, is a new operator defined on a larger domain (the Sobolev space $H^1$).

The concept of a [closed graph](@entry_id:154162) is intimately linked to the **[graph norm](@entry_id:274478)**, defined on $D(T)$ by $\|x\|_G = \|x\|_X + \|Tx\|_Y$. A fundamental result states that if $X$ and $Y$ are Banach spaces, the graph $G(T)$ is closed in $X \times Y$ if and only if the domain $D(T)$, equipped with the [graph norm](@entry_id:274478), is a Banach space [@problem_id:1887510]. This provides an alternative way to think about closedness: it is the property that makes the domain complete under a norm that incorporates information about both the function and its image under the operator.

Finally, a primary source of naturally occurring closed operators is the theory of adjoints in Hilbert spaces. It is a cornerstone theorem of [operator theory](@entry_id:139990) that if $T$ is a densely defined linear operator between two Hilbert spaces, its **adjoint operator** $T^*$ is always a [closed operator](@entry_id:274252) [@problem_id:2321463]. It is important to note that $T^*$ is not necessarily bounded, even if $T$ is. The property of being closed is, however, guaranteed. This fact underscores the importance of closed operators as a broader and more natural class than [bounded operators](@entry_id:264879), especially when dealing with [unbounded operators](@entry_id:144655) like those that arise in quantum mechanics and the theory of [partial differential equations](@entry_id:143134).