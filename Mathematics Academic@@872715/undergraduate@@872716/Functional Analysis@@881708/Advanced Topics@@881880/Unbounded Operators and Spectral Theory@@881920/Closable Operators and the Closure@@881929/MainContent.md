## Introduction
In functional analysis, many of the most significant operators, particularly those arising from differential equations and quantum mechanics, are unbounded. While the property of continuity is too restrictive for these operators, we need a different notion of "well-behavedness" to ensure they are mathematically tractable. This leads to the indispensable concepts of closed and closable operators, which provide a robust framework for handling operators that are not necessarily continuous.

This article addresses a fundamental problem: How do we rigorously define and work with operators like differentiation, which are not continuous and are typically defined on only a small, [dense subset](@entry_id:150508) of a [function space](@entry_id:136890)? The theory of closable operators provides the answer by allowing us to extend these operators to larger, more natural domains in a controlled and consistent manner, preserving essential properties along the way.

This article will guide you through this essential theory. In "Principles and Mechanisms," we will define closed and closable operators using the geometric concept of the operator's graph and explore the key criteria for identifying them. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these abstract ideas provide the rigorous foundation for partial differential equations, quantum mechanics, and [stochastic analysis](@entry_id:188809). Finally, "Hands-On Practices" will challenge you to apply these concepts to concrete examples, solidifying your understanding. The journey begins with the fundamental building block: the [graph of an operator](@entry_id:271574).

## Principles and Mechanisms

In the study of [functional analysis](@entry_id:146220), particularly when dealing with operators that are not necessarily bounded, the concepts of closed and closable operators are of paramount importance. These properties serve as a substitute for continuity, ensuring that the operators are "well-behaved" enough to permit the application of powerful theoretical tools, such as the Closed Graph Theorem. This chapter elucidates the principles underlying these concepts, starting from the geometric notion of an operator's graph to the sequential criteria that make these ideas computationally and theoretically tractable.

### The Graph of an Operator and Closed Operators

Let $X$ and $Y$ be [normed vector spaces](@entry_id:274725) over the same [scalar field](@entry_id:154310). For a linear operator $T: D(T) \to Y$ with domain $D(T) \subseteq X$, its **graph**, denoted $G(T)$, is the set of all [ordered pairs](@entry_id:269702) $(x, Tx)$ for $x$ in its domain. Formally,
$$
G(T) = \{ (x, Tx) \mid x \in D(T) \}
$$
The graph $G(T)$ is a linear subspace of the product space $X \times Y$. The [product space](@entry_id:151533) itself is a [normed space](@entry_id:157907), typically endowed with a norm such as $\|(x,y)\|_{X \times Y} = \|x\|_X + \|y\|_Y$. Convergence in this [product space](@entry_id:151533) is equivalent to [component-wise convergence](@entry_id:158444).

This geometric representation of an operator leads to a natural [topological property](@entry_id:141605). An operator $T$ is said to be a **[closed operator](@entry_id:274252)** if its graph $G(T)$ is a closed subset of the product space $X \times Y$.

This topological definition has a direct and highly useful sequential characterization. An operator $T$ is closed if and only if for every sequence $(x_n)_{n=1}^\infty$ in its domain $D(T)$ that converges to some element $x \in X$, the corresponding sequence of images $(Tx_n)_{n=1}^\infty$ converging to some $y \in Y$ implies that the limit point $x$ must belong to the domain $D(T)$ and its image must be $y$. That is:
If $(x_n) \subset D(T)$, $x_n \to x$ in $X$, and $Tx_n \to y$ in $Y$, then $x \in D(T)$ and $Tx = y$.

This condition should not be confused with continuity. A continuous (i.e., bounded) operator requires that for *every* convergent sequence $x_n \to x$ in its domain, the sequence of images $Tx_n$ must also converge (specifically, to $Tx$). In contrast, the definition of a [closed operator](@entry_id:274252) does not require $(Tx_n)$ to converge. It merely states that *if* it happens to converge, its limit is constrained in a specific way.

However, a fundamental connection exists: any [bounded linear operator](@entry_id:139516) $T: D(T) \to Y$ whose domain $D(T)$ is a [closed subspace](@entry_id:267213) of a Banach space $X$ is a [closed operator](@entry_id:274252) [@problem_id:1848496]. For instance, a [bounded operator](@entry_id:140184) defined on the entirety of a Banach space is always closed. This is because if $x_n \to x$, the closedness of $D(T)$ ensures $x \in D(T)$. The continuity of $T$ then ensures $Tx_n \to Tx$. If we are also given that $Tx_n \to y$, the [uniqueness of limits](@entry_id:142343) in $Y$ implies $y = Tx$.

### The Graph Norm

The structure of a [closed operator](@entry_id:274252) can be elegantly captured using a special norm on its domain. For an operator $T: D(T) \to Y$, we define the **[graph norm](@entry_id:274478)** $\|\cdot\|_G$ on $D(T)$ by:
$$
\|x\|_G = \|x\|_X + \|Tx\|_Y
$$
This norm effectively combines the norm of an element in the domain with the norm of its image, directly reflecting the topology of the graph in the product space. A sequence $(x_n)$ in $D(T)$ is a Cauchy sequence with respect to the [graph norm](@entry_id:274478) if and only if both $(x_n)$ is a Cauchy sequence in $X$ and $(Tx_n)$ is a Cauchy sequence in $Y$ [@problem_id:1848461].

This equivalence is straightforward to establish. If $(x_n)$ is Cauchy with respect to $\|\cdot\|_G$, then for any $\epsilon > 0$, $\|x_m - x_n\|_G = \|x_m - x_n\|_X + \|T(x_m - x_n)\|_Y  \epsilon$ for large $m, n$. Since norms are non-negative, this implies both $\|x_m - x_n\|_X  \epsilon$ and $\|Tx_m - Tx_n\|_Y  \epsilon$. Conversely, if $(x_n)$ and $(Tx_n)$ are both Cauchy, one can choose $N$ such that for $m,n > N$, $\|x_m - x_n\|_X  \epsilon/2$ and $\|Tx_m - Tx_n\|_Y  \epsilon/2$, which implies $\|x_m - x_n\|_G  \epsilon$.

The [graph norm](@entry_id:274478) provides a powerful characterization of closed operators when the spaces are complete. If $X$ and $Y$ are Banach spaces, an operator $T$ is closed if and only if its domain $D(T)$, when equipped with the [graph norm](@entry_id:274478), is a complete [normed space](@entry_id:157907) (i.e., a Banach space).

### Closable Operators and the Concept of Closure

Many important operators in [mathematical physics](@entry_id:265403) and analysis, especially differential operators, are not closed on their natural "initial" domains (e.g., spaces of infinitely differentiable functions). For example, the [differentiation operator](@entry_id:140145) defined on the space of [smooth functions](@entry_id:138942) with [compact support](@entry_id:276214) within an interval is not a [closed operator](@entry_id:274252) because the domain is not a [closed subspace](@entry_id:267213) in the $L^2$ norm [@problem_id:1848482].

This presents a challenge. We wish to work with closed operators, but many practical operators are not. The solution is to see if we can "extend" such an operator to a closed one in a minimal and natural way. This leads to the idea of closability.

We can attempt to create a [closed operator](@entry_id:274252) from $T$ by taking the closure of its graph, $\overline{G(T)}$, in the [product space](@entry_id:151533) $X \times Y$. However, there is a potential problem: the resulting set $\overline{G(T)}$ might not be the graph of any function. It could contain two distinct pairs $(x, y_1)$ and $(x, y_2)$ with $y_1 \neq y_2$. This would violate the single-valued property of a function.

An operator $T$ is said to be **closable** if the closure of its graph, $\overline{G(T)}$, is indeed the graph of a linear operator. This is equivalent to the condition that $\overline{G(T)}$ does not contain any "vertical lines," except at the origin. That is, if $(0, y) \in \overline{G(T)}$, then it must be that $y=0$.

This leads to the most practical, [sequential criterion](@entry_id:158961) for closability [@problem_id:1848496]:
A linear operator $T$ is closable if and only if for every sequence $(x_n)_{n=1}^\infty$ in $D(T)$ such that $x_n \to 0$ in $X$ and $Tx_n \to y$ in $Y$, it necessarily follows that $y=0$.

Not all operators are closable. Consider the Hilbert space $H = L^2[0,1]$ and the domain $D = C^1[0,1]$. Let $T: D \to \mathbb{C}$ be the functional $Tf = f'(1/2)$. One can construct a sequence of functions $(f_n)$ in $D$ such that $\|f_n\|_{L^2} \to 0$, but $Tf_n = f_n'(1/2) = 1$ for all $n$. Here, $x_n \to 0$ and $Tx_n \to 1$. Since the limit is not zero, the operator $T$ is not closable [@problem_id:1848510]. Such operators are generally considered pathological, and the theory focuses on the well-behaved class of closable operators.

### The Closure Operator

If an operator $T$ is closable, we can define a new operator, called the **closure** of $T$ and denoted $\bar{T}$. By the very definition of closability, the closure of the graph of $T$, $\overline{G(T)}$, is the graph of some operator. We define $\bar{T}$ to be this operator. Therefore, the fundamental relationship is an equality [@problem_id:1848441]:
$$
G(\bar{T}) = \overline{G(T)}
$$
From this definition, the properties of the closure operator $\bar{T}$ follow directly:

1.  **Domain of the Closure**: An element $x \in X$ belongs to the domain of the closure, $D(\bar{T})$, if and only if there exists a sequence $(x_n)$ in $D(T)$ such that $x_n \to x$ and the sequence of images $(Tx_n)$ converges to some element in $Y$ [@problem_id:1848506].

2.  **Action of the Closure**: For an $x \in D(\bar{T})$, the action of the closure is defined as the limit of the corresponding image sequence: $\bar{T}x = \lim_{n\to\infty} Tx_n$. The closability condition ensures that this limit is unique and does not depend on the choice of the sequence $(x_n)$ converging to $x$.

The process of taking the closure achieves its intended goal: **the closure $\bar{T}$ of a [closable operator](@entry_id:271727) $T$ is always a [closed operator](@entry_id:274252)** [@problem_id:1848496]. This is because its graph, $G(\bar{T})$, is a closed set by construction ($\overline{G(T)}$). Furthermore, $\bar{T}$ is an extension of $T$ (i.e., $D(T) \subseteq D(\bar{T})$ and $\bar{T}x = Tx$ for all $x \in D(T)$), and it is the *smallest* closed extension of $T$. If an operator $T$ is already closed to begin with, it is trivially closable, and its closure is simply itself: $\bar{T} = T$ [@problem_id:1848496].

### Sufficient Conditions for Closability

Determining whether an operator is closable directly from the sequential definition can be complex. Fortunately, several powerful theorems provide [sufficient conditions](@entry_id:269617) for closability.

**1. Existence of a Closed Extension:** An operator is closable if and only if it has at least one closed extension. As a particularly useful case, any operator that is the restriction of a bounded (and thus closed) [linear operator](@entry_id:136520) is closable [@problem_id:1848465]. For instance, if $T_{full}: X \to Y$ is a [bounded operator](@entry_id:140184) on a Banach space $X$, and we define an operator $A$ by restricting $T_{full}$ to a non-closed [dense subspace](@entry_id:261392) $D(A) \subset X$, then $A$ is closable, and its closure $\bar{A}$ will be the original operator $T_{full}$ [@problem_id:1848482].

**2. Symmetric Operators in Hilbert Spaces:** In the context of a complex Hilbert space $\mathcal{H}$, symmetry provides a powerful guarantee of closability. A [densely defined operator](@entry_id:264952) $T$ is **symmetric** if $\langle Tx, y \rangle = \langle x, Ty \rangle$ for all $x, y \in D(T)$. **Every densely defined [symmetric operator](@entry_id:275833) is closable** [@problem_id:1848494]. The proof is elegant: suppose $x_n \to 0$ and $Tx_n \to y$. For any $z \in D(T)$, the symmetry and the continuity of the inner product imply:
$$
\langle y, z \rangle = \lim_{n \to \infty} \langle Tx_n, z \rangle = \lim_{n \to \infty} \langle x_n, Tz \rangle = \langle 0, Tz \rangle = 0
$$
Since $D(T)$ is dense in $\mathcal{H}$, this implies $y$ is orthogonal to a [dense subset](@entry_id:150508) of $\mathcal{H}$, which forces $y=0$. This result is foundational in quantum mechanics, as it ensures that operators corresponding to [physical observables](@entry_id:154692) (which are required to be symmetric) are well-behaved.

**3. The Adjoint Operator in Hilbert Spaces:** The concept of closability is deeply connected to the properties of the [adjoint operator](@entry_id:147736). For a [densely defined operator](@entry_id:264952) $T$ on a Hilbert space, its adjoint $T^*$ is well-defined. A fundamental theorem states that **$T$ is closable if and only if the domain of its adjoint, $D(T^*)$, is a [dense subspace](@entry_id:261392) of the Hilbert space** [@problem_id:1848468].

For example, the operator $Tf = i \frac{df}{dx}$ on the domain $D(T) = C_c^1(0,1)$ (continuously differentiable functions with [compact support](@entry_id:276214) in $(0,1)$) is densely defined in $L^2[0,1]$. A calculation shows that its adjoint $T^*$ has the domain $D(T^*) = H^1(0,1)$, the Sobolev space of functions in $L^2$ with a [weak derivative](@entry_id:138481) in $L^2$. Since $H^1(0,1)$ is a [dense subspace](@entry_id:261392) of $L^2[0,1]$, the theorem confirms that $T$ is closable. This connection between the closability of an operator and the denseness of its adjoint's domain is a cornerstone of the advanced theory of [unbounded operators](@entry_id:144655).