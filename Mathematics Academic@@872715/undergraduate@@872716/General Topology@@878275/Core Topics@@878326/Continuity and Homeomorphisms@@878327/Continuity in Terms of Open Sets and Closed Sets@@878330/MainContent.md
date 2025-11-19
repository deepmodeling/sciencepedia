## Introduction
In mathematics, and particularly in topology, the idea of a continuous function is fundamental. It formalizes the intuitive notion of a mapping that preserves nearness, allowing us to compare and classify different topological spaces. While students of analysis are familiar with the $\epsilon$-$\delta$ definition of continuity, this framework is tied to the concept of distance and is not general enough for the broader world of [topological spaces](@entry_id:155056). The challenge, therefore, is to formulate a definition of continuity that relies only on the most basic structure of a [topological space](@entry_id:149165): its collection of open sets.

This article rigorously develops this modern, [topological definition of continuity](@entry_id:148722). Across three chapters, you will master the core concepts and their applications. In "Principles and Mechanisms," we will establish the open-set definition, explore equivalent criteria using closed sets and closures, and examine how continuity interacts with [function composition](@entry_id:144881) and restriction. In "Applications and Interdisciplinary Connections," we will witness the power of this definition as we apply it to problems in [functional analysis](@entry_id:146220), abstract algebra, and measure theory. Finally, "Hands-On Practices" will provide opportunities to solidify your understanding through guided exercises.

## Principles and Mechanisms

In our study of topology, the concept of a **continuous function** is of central importance. It is the primary tool for comparing and relating different topological spaces. While the familiar $\epsilon$-$\delta$ definition from [real analysis](@entry_id:145919) provides a metrical foundation for continuity, [general topology](@entry_id:152375) requires a more fundamental definition, one that relies solely on the [structure of open sets](@entry_id:159409). This chapter will rigorously establish this [topological definition of continuity](@entry_id:148722) and explore its immediate and profound consequences. We will dissect the definition through foundational examples, explore equivalent characterizations that offer different perspectives, and examine how continuous functions behave under standard constructions.

### The Topological Definition of Continuity

The transition from a metric space to a general [topological space](@entry_id:149165) necessitates a re-evaluation of continuity. The essence of continuity is that "nearby" points in the domain are mapped to "nearby" points in the [codomain](@entry_id:139336). In a [topological space](@entry_id:149165), the notion of "nearness" is encoded by open sets. This leads to a powerful and elegant generalization.

Let $(X, \mathcal{T}_X)$ and $(Y, \mathcal{T}_Y)$ be two [topological spaces](@entry_id:155056). A function $f: X \to Y$ is said to be **continuous** if for every open set $V$ in the codomain $Y$ (i.e., $V \in \mathcal{T}_Y$), its [preimage](@entry_id:150899), $f^{-1}(V)$, is an open set in the domain $X$ (i.e., $f^{-1}(V) \in \mathcal{T}_X$). The [preimage](@entry_id:150899) is defined as the set of all points in the domain that map into the set $V$:
$$
f^{-1}(V) = \{x \in X \mid f(x) \in V\}
$$
It is crucial to note the directionality of this definition. Continuity is not about the function mapping open sets to open sets (a property known as being an **[open map](@entry_id:155659)**). Instead, it demands that open sets in the [codomain](@entry_id:139336) are "pulled back" to open sets in the domain. A function can be continuous without being an [open map](@entry_id:155659), and vice-versa.

### Foundational Examples and Counterexamples

To build intuition for this abstract definition, we begin with several illustrative examples that explore the interplay between functions and the underlying topologies of their domains and codomains.

#### Constant Functions

Consider the simplest non-trivial function: the constant function. Let $f: X \to Y$ be defined by $f(x) = y_0$ for some fixed $y_0 \in Y$ and for all $x \in X$. Is this function always continuous, regardless of the topologies on $X$ and $Y$?

To answer this, we must examine the [preimage](@entry_id:150899) of an arbitrary open set $V$ in $Y$. There are two possibilities for the relationship between $V$ and the point $y_0$:
1.  If $y_0 \in V$, then for every $x \in X$, $f(x) = y_0 \in V$. This means every point in $X$ belongs to the [preimage](@entry_id:150899). Therefore, $f^{-1}(V) = X$.
2.  If $y_0 \notin V$, then for every $x \in X$, $f(x) = y_0 \notin V$. This means no point in $X$ belongs to the [preimage](@entry_id:150899). Therefore, $f^{-1}(V) = \emptyset$.

In any [topological space](@entry_id:149165) $(X, \mathcal{T}_X)$, the entire space $X$ and the empty set $\emptyset$ are required to be open by the axioms of a topology. Since the preimage of any open set in $Y$ is either $X$ or $\emptyset$, the [preimage](@entry_id:150899) is always open in $X$. Consequently, any [constant function](@entry_id:152060) between two topological spaces is always continuous [@problem_id:1544619].

#### Functions and Extreme Topologies

The nature of the topologies on the domain and [codomain](@entry_id:139336) can have a dramatic effect on continuity. Consider the two "extreme" topologies that can be placed on a set. The **[discrete topology](@entry_id:152622)** is the collection of all subsets, meaning every set is open. The **[indiscrete topology](@entry_id:149604)** (or [trivial topology](@entry_id:154009)) contains only the [empty set](@entry_id:261946) and the entire space.

What happens if the domain has the discrete topology? Let $f: X \to Y$ be any function, where $X$ is endowed with the [discrete topology](@entry_id:152622). For any open set $V \subseteq Y$, its preimage $f^{-1}(V)$ is some subset of $X$. In the discrete topology, *every* subset of $X$ is open. Therefore, $f^{-1}(V)$ is guaranteed to be open in $X$. This establishes a general principle: **any function from a discrete topological space is continuous** [@problem_id:1544638].

Now, consider the opposite scenario: what if the codomain has the [indiscrete topology](@entry_id:149604)? Let $f: X \to Y$ be any function, where $Y$ is endowed with the [indiscrete topology](@entry_id:149604), $\mathcal{T}_Y = \{\emptyset, Y\}$. To check for continuity, we only need to find the preimages of the open sets in $Y$:
-   $f^{-1}(\emptyset) = \emptyset$
-   $f^{-1}(Y) = X$

As established before, $\emptyset$ and $X$ are always open sets in any topology $\mathcal{T}_X$ on the domain $X$. Thus, the condition for continuity is always satisfied. This gives us another general principle: **any function to an indiscrete topological space is continuous** [@problem_id:1544624].

#### Demonstrating Discontinuity

Proving a function is continuous requires showing that the preimage of *every* open set is open. Conversely, to prove a function is **discontinuous**, one only needs to find a *single* open set in the [codomain](@entry_id:139336) whose [preimage](@entry_id:150899) is not open in the domain.

A canonical example is the [step function](@entry_id:158924) on the real line. Let $X = Y = \mathbb{R}$, both with the standard (usual) topology. Consider the function:
$$
f(x) = \begin{cases} 10  &\text{if } x \ge 0 \\ -10 &\text{if } x  0 \end{cases}
$$
Intuitively, we know this function has a discontinuity at $x=0$. We can prove this rigorously using the topological definition. Let's choose an open set in the codomain $Y$ that contains the point $10$ but not $-10$. A simple choice is the open interval $V = (5, 15)$. Now we compute its [preimage](@entry_id:150899):
$$
f^{-1}((5, 15)) = \{x \in \mathbb{R} \mid f(x) \in (5, 15)\}
$$
The only value the function takes within this interval is $10$. This occurs for all $x \ge 0$. Thus, the preimage is the set $[0, \infty)$. The set $[0, \infty)$ is not an open set in the [standard topology](@entry_id:152252) on $\mathbb{R}$. For instance, any open interval containing the point $0$, such as $(-\epsilon, \epsilon)$ for $\epsilon  0$, contains points not in $[0, \infty)$. Therefore, no open neighborhood of $0$ is contained within the set, proving it is not open. Since we have found an open set $V$ whose preimage $f^{-1}(V)$ is not open, the function $f$ is discontinuous [@problem_id:1544667]. It is worth noting that for other choices of open sets, the [preimage](@entry_id:150899) might be open. For example, the [preimage](@entry_id:150899) of $U = (-15, -5)$ is $(-\infty, 0)$, which is open. Continuity requires the condition to hold for all open sets, without exception.

### Equivalent Formulations of Continuity

The open set definition of continuity is foundational, but several other equivalent characterizations exist. These alternatives can be more convenient in certain proofs and provide deeper insight into the topological nature of continuity.

#### The Closed Set Criterion

A set is closed if and only if its complement is open. This duality between [open and closed sets](@entry_id:140356) suggests an alternative definition for continuity. A function $f: X \to Y$ is continuous if and only if **for every closed set $C$ in $Y$, its preimage $f^{-1}(C)$ is a closed set in $X$**.

The proof of this equivalence is a direct application of [set theory](@entry_id:137783) and definitions. It hinges on the fundamental identity relating preimages and complements: for any subset $S \subseteq Y$, we have $f^{-1}(Y \setminus S) = X \setminus f^{-1}(S)$.

-   ($\Rightarrow$) Assume $f$ is continuous (in terms of open sets). Let $C$ be any closed set in $Y$. By definition, its complement $Y \setminus C$ is an open set in $Y$. Since $f$ is continuous, the [preimage](@entry_id:150899) $f^{-1}(Y \setminus C)$ must be an open set in $X$. Using the identity, this means $X \setminus f^{-1}(C)$ is open in $X$. By definition, the complement of this open set, which is precisely $f^{-1}(C)$, must be a closed set in $X$.

-   ($\Leftarrow$) Assume the preimage of every [closed set](@entry_id:136446) is closed. Let $V$ be any open set in $Y$. Its complement $Y \setminus V$ is a closed set in $Y$. By our assumption, the [preimage](@entry_id:150899) $f^{-1}(Y \setminus V)$ is a [closed set](@entry_id:136446) in $X$. Using the identity again, this means $X \setminus f^{-1}(V)$ is closed in $X$. Therefore, its complement, $f^{-1}(V)$, must be an open set in $X$. This satisfies the open set definition of continuity.

This equivalence is not merely a technical curiosity; it is a powerful tool. For instance, it provides a very elegant way to prove the [continuity of functions](@entry_id:193744) constructed by "pasting" other functions together, as we will see later [@problem_id:1544663].

#### The Closure Criterion

Continuity can also be characterized by its interaction with the **closure** of a set. Recall that the [closure of a set](@entry_id:143367) $A$, denoted $\text{cl}(A)$, is the intersection of all [closed sets](@entry_id:137168) containing $A$. It represents the set $A$ along with all its "limit points". The following three statements are equivalent to the [continuity of a function](@entry_id:147842) $f: X \to Y$:

1.  For every subset $A \subseteq X$, $f(\text{cl}(A)) \subseteq \text{cl}(f(A))$.
2.  For every subset $A \subseteq X$, $\text{cl}(f(\text{cl}(A))) = \text{cl}(f(A))$.
3.  For every subset $B \subseteq Y$, $\text{cl}(f^{-1}(B)) \subseteq f^{-1}(\text{cl}(B))$.

Let's focus on the first statement, which is perhaps the most intuitive. The condition $f(\text{cl}(A)) \subseteq \text{cl}(f(A))$ means that the function maps points adherent to $A$ to points adherent to the image of $A$. A continuous function cannot map a point "close" to a set $A$ to a point that is "far" from the set $f(A)$.

Let's prove the equivalence between continuity and statement 1 [@problem_id:1544658].
-   ($\text{Continuity} \Rightarrow \text{Statement 1}$): Assume $f$ is continuous. For any $A \subseteq X$, the set $\text{cl}(f(A))$ is closed in $Y$. By the closed set criterion, its [preimage](@entry_id:150899), $f^{-1}(\text{cl}(f(A)))$, is a [closed set](@entry_id:136446) in $X$. Since $f(A) \subseteq \text{cl}(f(A))$, it follows that $A \subseteq f^{-1}(f(A)) \subseteq f^{-1}(\text{cl}(f(A)))$. We have found a [closed set](@entry_id:136446), $f^{-1}(\text{cl}(f(A)))$, that contains $A$. Since $\text{cl}(A)$ is the *smallest* [closed set](@entry_id:136446) containing $A$, we must have $\text{cl}(A) \subseteq f^{-1}(\text{cl}(f(A)))$. Applying $f$ to both sides gives $f(\text{cl}(A)) \subseteq f(f^{-1}(\text{cl}(f(A)))) \subseteq \text{cl}(f(A))$, which is the desired inclusion.

-   ($\text{Statement 1} \Rightarrow \text{Continuity}$): Assume $f(\text{cl}(A)) \subseteq \text{cl}(f(A))$ for all $A \subseteq X$. To prove continuity, we use the closed set criterion. Let $C$ be a [closed set](@entry_id:136446) in $Y$. Let $A = f^{-1}(C)$. We want to show $A$ is closed, which is equivalent to showing $\text{cl}(A) = A$. By our assumption, $f(\text{cl}(A)) \subseteq \text{cl}(f(A))$. Substituting $A = f^{-1}(C)$, we get $f(\text{cl}(f^{-1}(C))) \subseteq \text{cl}(f(f^{-1}(C)))$. Since $f(f^{-1}(C)) \subseteq C$ and $C$ is closed (so $\text{cl}(C)=C$), we have $\text{cl}(f(f^{-1}(C))) \subseteq \text{cl}(C) = C$. This chain implies $f(\text{cl}(f^{-1}(C))) \subseteq C$. Applying $f^{-1}$ to this inclusion gives $\text{cl}(f^{-1}(C)) \subseteq f^{-1}(C)$. Since a set is always a subset of its closure, we have equality, proving that $f^{-1}(C)$ is closed.

Similar proofs establish the equivalence for statements 2 and 3, providing a rich toolkit for analyzing continuous functions.

#### Checking Continuity using a Basis

Checking the [preimage](@entry_id:150899) of *every* open set can be tedious. Fortunately, it is sufficient to check only the sets in a **basis** for the [codomain](@entry_id:139336)'s topology. A function $f: X \to Y$ is continuous if and only if for every basis element $B$ of the topology on $Y$, the [preimage](@entry_id:150899) $f^{-1}(B)$ is open in $X$.

This simplification works because every open set $V$ in $Y$ can be expressed as a union of basis elements, say $V = \bigcup_{i \in I} B_i$. The preimage operator commutes with unions, so $f^{-1}(V) = f^{-1}(\bigcup_{i \in I} B_i) = \bigcup_{i \in I} f^{-1}(B_i)$. If the [preimage](@entry_id:150899) of each basis element $f^{-1}(B_i)$ is open in $X$, then their union, $f^{-1}(V)$, is also open (since an arbitrary union of open sets is open).

This criterion is particularly useful when working with standard topologies that are defined by a basis, such as the standard topology on $\mathbb{R}$ (basis of open intervals) or the **[lower limit topology](@entry_id:152239)** on $\mathbb{R}$, $\mathcal{T}_\ell$ (basis of half-[open intervals](@entry_id:157577) $[a,b)$).

Consider the identity map $f(x)=x$ from $(\mathbb{R}, \mathcal{T}_\ell)$ to $(\mathbb{R}, \mathcal{T}_s)$, where $\mathcal{T}_s$ is the standard topology. To check if $f$ is continuous, we only need to check the preimages of the basis elements of $\mathcal{T}_s$, which are open intervals $(a,b)$. The [preimage](@entry_id:150899) is $f^{-1}((a,b)) = (a,b)$. Is $(a,b)$ an open set in the [lower limit topology](@entry_id:152239)? Yes, because any [open interval](@entry_id:144029) can be written as a union of basis elements of $\mathcal{T}_\ell$, for example, $(a,b) = \bigcup_{x \in (a,b)} [x, b)$. Since the preimage of every basis element of the codomain's topology is open in the domain, the function is continuous [@problem_id:1544651].

### Properties and Constructions of Continuous Functions

Just as with other mathematical structures, it is important to understand how continuity behaves under common operations like restriction and composition.

#### Restriction of a Function

If a function is continuous on its entire domain, is it also continuous if we restrict its domain to a smaller subspace? Let $f: X \to Y$ be a continuous function, and let $A$ be a subset of $X$, equipped with the **subspace topology**. The restriction of $f$ to $A$ is the function $f|_A: A \to Y$ defined by $(f|_A)(x) = f(x)$ for all $x \in A$.

The function $f|_A$ is always continuous. To prove this, let $V$ be any open set in $Y$. We need to show that $(f|_A)^{-1}(V)$ is open in the subspace topology on $A$. By definition:
$$
(f|_A)^{-1}(V) = \{x \in A \mid (f|_A)(x) \in V\} = \{x \in A \mid f(x) \in V\} = A \cap f^{-1}(V)
$$
Since $f$ is continuous, $f^{-1}(V)$ is an open set in $X$. By the definition of the subspace topology on $A$, the intersection of any open set in $X$ with $A$ is an open set in $A$. Thus, $A \cap f^{-1}(V)$ is open in $A$. This proves that the restriction of any continuous function to a subspace is continuous [@problem_id:1544653].

#### The Pasting Lemma

A powerful tool for constructing continuous functions is the **Pasting Lemma**. It allows us to "glue" two continuous functions together to create a new continuous function on a larger domain.

**Theorem (The Pasting Lemma):** Let $X$ and $Y$ be topological spaces, and let $A$ and $B$ be two closed subsets of $X$ such that $A \cup B = X$. Let $f: A \to Y$ and $g: B \to Y$ be continuous functions (with respect to the subspace topologies on $A$ and $B$). If $f(x) = g(x)$ for all $x \in A \cap B$, then the function $h: X \to Y$ defined by
$$
h(x) = \begin{cases} f(x)  \text{if } x \in A \\ g(x)  \text{if } x \in B \end{cases}
$$
is continuous.

The proof is most elegantly handled using the [closed set](@entry_id:136446) criterion for continuity. Let $C$ be an arbitrary [closed set](@entry_id:136446) in $Y$. We must show that $h^{-1}(C)$ is a [closed set](@entry_id:136446) in $X$. From the definition of $h$, we have:
$$
h^{-1}(C) = \{x \in X \mid h(x) \in C\} = \{x \in A \mid f(x) \in C\} \cup \{x \in B \mid g(x) \in C\} = f^{-1}(C) \cup g^{-1}(C)
$$
Since $f: A \to Y$ is continuous and $C$ is closed in $Y$, the set $f^{-1}(C)$ is closed *in the subspace A*. This means there exists a closed set $F_1$ in $X$ such that $f^{-1}(C) = A \cap F_1$. Because $A$ is itself a closed set in $X$, the intersection of two closed sets, $A \cap F_1$, is a closed set in $X$. Therefore, $f^{-1}(C)$ is closed in $X$.

By the same argument, since $g$ is continuous and $B$ is a [closed set](@entry_id:136446), $g^{-1}(C)$ is also a closed set in $X$.

Finally, $h^{-1}(C) = f^{-1}(C) \cup g^{-1}(C)$ is the union of two closed sets in $X$. Since the finite union of closed sets is always closed, $h^{-1}(C)$ is a [closed set](@entry_id:136446) in $X$. As this holds for any closed set $C$ in $Y$, the function $h$ is continuous [@problem_id:1544643]. A similar version of the lemma holds if $A$ and $B$ are both open sets.

### Continuity, Bijections, and Homeomorphisms

In topology, we often want to know when two spaces are "topologically equivalent" or "the same" from a topological point of view. This notion is captured by the concept of a [homeomorphism](@entry_id:146933). A **[homeomorphism](@entry_id:146933)** is a function $f: X \to Y$ that is:
1.  A [bijection](@entry_id:138092) (one-to-one and onto).
2.  Continuous.
3.  Has a continuous inverse, $f^{-1}: Y \to X$.

It is a common and critical mistake to assume that any [continuous bijection](@entry_id:198258) is a homeomorphism. The third condition—that the inverse must also be continuous—is not automatic. A [continuous bijection](@entry_id:198258) whose inverse is not continuous provides a "weaker" mapping between spaces.

A simple but illuminating [counterexample](@entry_id:148660) can be constructed using extreme topologies [@problem_id:1544655]. Let $X = \{1, 2\}$ with the discrete topology $\mathcal{T}_X = \{\emptyset, \{1\}, \{2\}, X\}$, and let $Y = \{a, b\}$ with the [indiscrete topology](@entry_id:149604) $\mathcal{T}_Y = \{\emptyset, Y\}$. Define the function $f: X \to Y$ by $f(1) = a$ and $f(2) = b$.

-   **Is $f$ a [continuous bijection](@entry_id:198258)?** The function is clearly a [bijection](@entry_id:138092). To check for continuity, we note that the domain $X$ has the [discrete topology](@entry_id:152622). As we established earlier, any function from a [discrete space](@entry_id:155685) is continuous. So, $f$ is a [continuous bijection](@entry_id:198258).

-   **Is the inverse $f^{-1}$ continuous?** The inverse function is $f^{-1}: Y \to X$, where $f^{-1}(a) = 1$ and $f^{-1}(b) = 2$. To check if $f^{-1}$ is continuous, we must see if the preimage of every open set in its codomain, $X$, is open in its domain, $Y$. Let's pick the open set $U = \{1\}$ in $X$. Its [preimage](@entry_id:150899) under $f^{-1}$ is $(f^{-1})^{-1}(\{1\}) = f(\{1\}) = \{a\}$. The set $\{a\}$ is not an open set in the [indiscrete topology](@entry_id:149604) of $Y$, since the only open sets are $\emptyset$ and $Y=\{a,b\}$. Because we found an open set in the codomain ($X$) whose [preimage](@entry_id:150899) is not open in the domain ($Y$), the function $f^{-1}$ is not continuous.

Therefore, this function $f$ is a [continuous bijection](@entry_id:198258) but not a [homeomorphism](@entry_id:146933). This demonstrates that continuity of $f$ and $f^{-1}$ are separate conditions.

### An Application: Identifying Closed Sets in Function Spaces

The principles of continuity extend far beyond simple sets into more abstract realms, such as spaces of functions. Consider the space $X = C([0, 1], \mathbb{R})$ of all continuous real-valued functions on the interval $[0,1]$, equipped with the topology induced by the sup-norm metric, $d(f, g) = \sup_{t \in [0,1]} |f(t) - g(t)|$.

Let's investigate the properties of a specific subset of this space:
$$
S = \left\{ f \in C([0, 1], \mathbb{R}) \mid f(0) = \int_0^1 f(t) dt \right\}
$$
Is this set open, closed, or neither in $X$? We can answer this question elegantly by leveraging a general theorem about continuous functions.

**Theorem:** Let $f, g: X \to Y$ be two continuous functions. If the codomain $Y$ is a **Hausdorff space** (a space where any two distinct points have disjoint open neighborhoods), then the set $E = \{x \in X \mid f(x) = g(x)\}$ is a [closed subset](@entry_id:155133) of $X$.

*Proof:* To show $E$ is closed, we will show its complement $X \setminus E$ is open. Let $x_0$ be an arbitrary point in $X \setminus E$. By definition, $f(x_0) \neq g(x_0)$. Since $Y$ is Hausdorff, there exist [disjoint open sets](@entry_id:150704) $U$ and $V$ in $Y$ such that $f(x_0) \in U$ and $g(x_0) \in V$. Because $f$ and $g$ are continuous, their preimages $f^{-1}(U)$ and $g^{-1}(V)$ are both open sets in $X$. Their intersection, $W = f^{-1}(U) \cap g^{-1}(V)$, is also an open set in $X$, and it contains $x_0$. For any point $x \in W$, we have $f(x) \in U$ and $g(x) \in V$. Since $U$ and $V$ are disjoint, we must have $f(x) \neq g(x)$, which means $x \in X \setminus E$. Thus, $W \subseteq X \setminus E$. We have found an open neighborhood of $x_0$ that is entirely contained in $X \setminus E$, proving that $X \setminus E$ is open. Therefore, $E$ is closed.

Now, let's apply this theorem to our set $S$. The [codomain](@entry_id:139336) for our comparisons is $\mathbb{R}$, which is a Hausdorff space. We can define two functions (called functionals) from our space $X=C([0,1])$ to $\mathbb{R}$:
-   The "evaluation at 0" functional: $\phi_1(f) = f(0)$
-   The "integration" functional: $\phi_2(f) = \int_0^1 f(t) dt$

The set $S$ is precisely the set of functions $f$ where $\phi_1(f) = \phi_2(f)$. If we can show that both $\phi_1$ and $\phi_2$ are continuous functions from $(X,d)$ to $\mathbb{R}$, our theorem will immediately tell us that $S$ is a closed set.

Indeed, both are continuous. For $\phi_1$, we have $|\phi_1(f) - \phi_1(g)| = |f(0) - g(0)| \le \sup_{t \in [0,1]} |f(t) - g(t)| = d(f,g)$. For $\phi_2$, we have $|\phi_2(f) - \phi_2(g)| = |\int_0^1 (f(t)-g(t)) dt| \le \int_0^1 |f(t)-g(t)| dt \le \int_0^1 d(f,g) dt = d(f,g)$. Both functionals are Lipschitz continuous with a constant of 1, which implies they are continuous.

A slightly different but equivalent approach is to define a single functional $L: X \to \mathbb{R}$ by $L(f) = \phi_1(f) - \phi_2(f) = f(0) - \int_0^1 f(t) dt$. As the difference of two continuous functions, $L$ is also continuous. The set $S$ is then simply $S = \{f \in X \mid L(f) = 0\}$. This is the preimage of the set $\{0\}$ under the continuous function $L$. Since $\{0\}$ is a [closed set](@entry_id:136446) in $\mathbb{R}$, its [preimage](@entry_id:150899) $S = L^{-1}(\{0\})$ must be a closed set in $X$ [@problem_id:1545165]. This example showcases how the abstract definition of continuity provides powerful tools for analyzing complex mathematical structures.