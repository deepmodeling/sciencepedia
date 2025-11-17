## Introduction
In the study of [general topology](@entry_id:152375), once we have defined the basic structure of a [topological space](@entry_id:149165), the next step is to develop tools to classify and compare them. One of the most fruitful approaches is to ask: how well can the open sets of a topology distinguish between different points or between points and sets? This question gives rise to a hierarchy of conditions known as the **[separation axioms](@entry_id:154482)**, which provide a scale for measuring the "separateness" of a space. The first and most fundamental of these is the T1 axiom. This article addresses the need for a precise way to classify spaces beyond their basic definition, introducing the T1 property as a foundational concept.

Across the following chapters, you will build a complete understanding of this essential axiom.
- **Principles and Mechanisms** will introduce the formal definition of a T1 space and immediately prove its most powerful and elegant characterization—that singletons are closed sets—exploring the profound consequences of this equivalence.
- **Applications and Interdisciplinary Connections** will demonstrate the axiom's utility in practice, showing how it behaves in various topological constructions and revealing its surprising and deep connections to other fields, particularly [commutative algebra](@entry_id:149047) and the theory of [topological groups](@entry_id:155664).
- **Hands-On Practices** will offer a curated set of problems designed to solidify your intuition and test your mastery of the concepts, from basic counterexamples to short proofs.

We begin our exploration by delving into the core principles and mechanisms that define a T1 space and set it apart from other topological structures.

## Principles and Mechanisms

Following our general introduction to [topological spaces](@entry_id:155056), we now delve into a more refined classification system based on the so-called **[separation axioms](@entry_id:154482)**. These axioms provide a hierarchy for measuring the degree to which points and [closed sets](@entry_id:137168) within a space can be distinguished from one another using the open sets of the topology. The first and most fundamental of these is the T1 axiom.

### The Definition and Immediate Context of T1 Spaces

A topological space $(X, \mathcal{T})$ is called a **T1 space** if for every pair of distinct points $x, y \in X$, there exists an open set containing $x$ but not $y$, and there exists another open set containing $y$ but not $x$.

Formally, for any $x, y \in X$ with $x \neq y$, there exist $U, V \in \mathcal{T}$ such that:
1.  $x \in U$ and $y \notin U$
2.  $y \in V$ and $x \notin V$

This axiom is sometimes called the Fréchet [separation axiom](@entry_id:155057). At first glance, it appears to be a natural and minimal requirement for points to be topologically distinguishable. It strengthens the slightly weaker T0 (or Kolmogorov) axiom, which only requires that for any distinct pair of points, there is *an* open set containing one point but not the other, without specifying which.

The distinction is crucial. To illustrate, consider a set $X = \{a, b, c\}$ with the topology $\mathcal{T} = \{\emptyset, \{a\}, \{a, b\}, X\}$. Let's examine the pairs of distinct points:
- For the pair $(a, b)$, the open set $\{a\}$ contains $a$ but not $b$.
- For the pair $(a, c)$, the open set $\{a\}$ contains $a$ but not $c$.
- For the pair $(b, c)$, the open set $\{a, b\}$ contains $b$ but not $c$.
In each case, we can find an open set containing one point but not the other, so this space is T0. However, is it T1? For the pair $(a, b)$, while we have an open set $\{a\}$ separating $a$ from $b$, we must also find an open set containing $b$ but not $a$. The open sets containing $b$ are $\{a, b\}$ and $X$, both of which also contain $a$. Since no such set exists, the T1 condition fails [@problem_id:1556900]. This simple example demonstrates that the T1 axiom is strictly stronger than the T0 axiom.

### The Fundamental Characterization: Singletons are Closed

While the definition of a T1 space is given in terms of separating points with open sets, its most powerful and frequently used characterization relates to the nature of singleton sets.

**Theorem:** A topological space $(X, \mathcal{T})$ is a T1 space if and only if every singleton set $\{x\}$ is a closed set for all $x \in X$.

**Proof:**
($\Rightarrow$) Assume $(X, \mathcal{T})$ is a T1 space. To show that a set $\{x\}$ is closed, we must show that its complement, $X \setminus \{x\}$, is open. Let $y$ be an arbitrary point in $X \setminus \{x\}$. This means $y \neq x$. By the T1 definition, there exists an open set $U_y \in \mathcal{T}$ such that $y \in U_y$ and $x \notin U_y$. This implies that $U_y \subseteq X \setminus \{x\}$. Since we can find such an [open neighborhood](@entry_id:268496) for every point $y$ in $X \setminus \{x\}$, we can express this complement as the union of all such neighborhoods:
$$X \setminus \{x\} = \bigcup_{y \in X \setminus \{x\}} U_y$$
As the union of open sets is always open, $X \setminus \{x\}$ is an open set. Therefore, its complement, $\{x\}$, is closed.

($\Leftarrow$) Assume every singleton set $\{x\}$ in $X$ is closed. Let $x, y$ be distinct points in $X$. Since $\{y\}$ is closed, its complement $U = X \setminus \{y\}$ is an open set. By construction, $x \in U$ and $y \notin U$. Similarly, since $\{x\}$ is closed, its complement $V = X \setminus \{x\}$ is an open set. By construction, $y \in V$ and $x \notin V$. This satisfies the definition of a T1 space.

This equivalence is profound. It reframes the separation property in terms of the topological structure of the simplest non-empty sets. A direct corollary, stemming from the fact that a finite union of closed sets is closed, is an equally useful characterization:

**Corollary:** A space is T1 if and only if every finite subset is closed [@problem_id:1588677].

This characterization illuminates what goes "wrong" in a space that is not T1. If a space is not T1, at least one singleton set $\{x\}$ is not closed. This means its closure, $\overline{\{x\}}$, must contain more than just the point $x$. The [closure of a set](@entry_id:143367) is the smallest closed set containing it. Consider the non-T1 space from before, $X = \{p, q, r\}$ with topology $\mathcal{T} = \{\emptyset, \{p\}, \{p, q\}, X\}$. The closed sets are the complements of these: $X$, $\{q, r\}$, $\{r\}$, and $\emptyset$. Let's examine the closures of the singletons:
- $\overline{\{p\}}$: The smallest closed set containing $p$ is $X = \{p, q, r\}$.
- $\overline{\{q\}}$: The smallest closed set containing $q$ is $\{q, r\}$.
- $\overline{\{r\}}$: The smallest closed set containing $r$ is $\{r\}$.
Here, the points $p$ and $q$ are not closed, and their closures "absorb" other points. The point $q$ is in the closure of $\{p\}$, meaning every open set containing $q$ must also contain $p$. Topologically, $p$ and $q$ are "stuck together" in a way that the T1 axiom forbids [@problem_id:1536288].

### Consequences of the T1 Property

The fact that points are [closed sets](@entry_id:137168) in T1 spaces has several important consequences that ripple through other areas of topology.

#### Limit Points and Density

The T1 axiom has a strong implication for the concept of limit points. Recall that a point $p$ is a **limit point** of a set $A$ if every open neighborhood of $p$ contains a point of $A$ other than $p$. The set of all [limit points](@entry_id:140908) of $A$ is its **derived set**, $A'$. In a T1 space, a point cannot be a limit point of a set consisting of only another single point.

Specifically, for any point $x$ in a T1 space $X$, the derived set of the singleton $\{x\}$ is always the empty set, i.e., $(\{x\})' = \emptyset$ [@problem_id:1580307]. To see why, let $y$ be any other point in $X$ ($y \neq x$). Since the space is T1, there exists an open set $V$ containing $y$ but not $x$. This open neighborhood $V$ of $y$ fails to contain any point of $\{x\}$, so by definition, $y$ cannot be a [limit point](@entry_id:136272) of $\{x\}$. The point $x$ itself also cannot be a [limit point](@entry_id:136272) of $\{x\}$, as any neighborhood of $x$ contains no point of $\{x\}$ *other than* $x$. Thus, no point in $X$ is a limit point of $\{x\}$.

This connects to properties like density. A point $x_0$ is an **[isolated point](@entry_id:146695)** if $\{x_0\}$ is an open set. If a T1 space has no isolated points, then every singleton $\{x_0\}$ is a **nowhere dense** set. A set is nowhere dense if the interior of its closure is empty. Since the space is T1, $\{x_0\}$ is closed, so its closure is just $\{x_0\}$. Since $x_0$ is not an [isolated point](@entry_id:146695), $\{x_0\}$ is not open, meaning its interior must be empty. Thus, $\text{int}(\overline{\{x_0\}}) = \text{int}(\{x_0\}) = \emptyset$ [@problem_id:1571738]. This illustrates how the T1 axiom provides a crucial ingredient (closed singletons) for proving more intricate structural properties.

#### T1 Spaces and Cardinality

A fascinating interaction occurs between the T1 axiom and the size of the underlying set. In a finite [topological space](@entry_id:149165), the T1 property is surprisingly restrictive. If a finite space $X$ is T1, every singleton $\{x\}$ is closed. Since any subset of $X$ is a finite union of singletons, and a finite union of [closed sets](@entry_id:137168) is closed, every subset of $X$ must be closed. If every subset is closed, then every subset is also open (since the complement of a [closed set](@entry_id:136446) is open). This is the definition of the **[discrete topology](@entry_id:152622)**. Therefore, any finite T1 space must have the [discrete topology](@entry_id:152622) [@problem_id:1588670].

For infinite sets, this is not the case. Consider an infinite set $X$ with the **[cofinite topology](@entry_id:138582)**, where the open sets are the empty set and any subset whose complement is finite. In this topology, any [finite set](@entry_id:152247) is, by definition, closed. This means every singleton is closed, so the space is T1. However, unless $X$ is finite, this is not the [discrete topology](@entry_id:152622). This space provides a crucial example that T1 is strictly weaker than the T2 (Hausdorff) axiom. In a T2 space, any two distinct points have disjoint open neighborhoods. In the [cofinite topology](@entry_id:138582) on an infinite set, any two non-empty open sets have an infinite intersection, and thus the space cannot be T2 [@problem_id:1588692].

### The T1 Property Under Topological Constructions

A central theme in topology is understanding how properties behave when we build new spaces from old ones. The T1 property is well-behaved under most standard constructions.

A property is called a **[topological property](@entry_id:141605)** if it is preserved by homeomorphisms. The T1 axiom is indeed a [topological property](@entry_id:141605). If $f: X \to Y$ is a homeomorphism and $X$ is T1, then for any point $y \in Y$, its preimage $x = f^{-1}(y)$ forms a closed singleton $\{x\}$ in $X$. Since $f$ is a homeomorphism, the map $f$ is continuous, and the image of a closed set under the inverse map $f^{-1}$ is not guaranteed to be closed. However, a [homeomorphism](@entry_id:146933) $f$ is a [closed map](@entry_id:150357), meaning it sends closed sets to [closed sets](@entry_id:137168). Thus $f(\{x\}) = \{y\}$ is a [closed set](@entry_id:136446) in $Y$. Since this holds for all $y \in Y$, the space $Y$ is T1.

More generally, we can analyze its behavior under several key operations:

- **Subspaces:** The T1 property is **hereditary**, meaning any subspace of a T1 space is also a T1 space. If $Y \subseteq X$ and $X$ is T1, then for any $y \in Y$, the set $\{y\}$ is closed in $X$. The [closed sets](@entry_id:137168) of the subspace $Y$ are intersections of closed sets of $X$ with $Y$. Thus, $\{y\} \cap Y = \{y\}$ is closed in $Y$. This makes $Y$ a T1 space [@problem_id:1536272].

- **Products:** The T1 property is **productive**. The product space $X \times Y$ is T1 if and only if both factor spaces $X$ and $Y$ are T1. If $X$ and $Y$ are T1, then for any $(x,y) \in X \times Y$, the sets $\{x\}$ and $\{y\}$ are closed in their respective spaces. The sets $X \times \{y\}$ and $\{x\} \times Y$ are closed in the [product space](@entry_id:151533), and their intersection is the singleton $\{(x,y)\}$, which is therefore closed. Conversely, if the product $X \times Y$ is T1, then its subspaces are T1. Since $X$ is homeomorphic to the subspace $X \times \{y_0\}$ for any fixed $y_0 \in Y$, it must also be T1 [@problem_id:1569189].

- **Disjoint Unions:** The disjoint union of a family of T1 spaces is also a T1 space. To separate two points in the union, if they come from the same original space, we use the T1 property of that space. If they come from different original spaces, say $p \in X$ and $q \in Y$, then the entire set $X$ (as a subset of the disjoint union) is an open set containing $p$ but not $q$, and likewise for $Y$ [@problem_id:1588688].

- **Quotients:** Here we must issue a strong caution. Unlike the previous constructions, the T1 property is **not** preserved under quotient maps. A quotient space can fail to be T1 even if the original space is T1. The key is to examine the equivalence classes. A singleton point in the quotient space, $\{[x]\}$, is closed if and only if its [preimage](@entry_id:150899), the equivalence class $[x]$, is a closed set in the original space. If we can define an equivalence relation where at least one equivalence class is not a closed set, the [quotient space](@entry_id:148218) will not be T1. For example, let $X = \mathbb{Z}$ with the [cofinite topology](@entry_id:138582) (a T1 space). Define an [equivalence relation](@entry_id:144135) where all even integers are equivalent to each other, and all odd integers form their own singleton classes. The [equivalence class](@entry_id:140585) of even numbers, $E$, is an infinite set whose complement (the odd numbers) is also infinite. Therefore, $E$ is not a [finite set](@entry_id:152247) and thus not a [closed set](@entry_id:136446) in the [cofinite topology](@entry_id:138582). The point $\{[E]\}$ in the quotient space $\mathbb{Z}/\sim$ corresponds to a singleton set that is not closed, so the quotient space is not T1 [@problem_id:1588698].

In summary, the T1 axiom provides a foundational step in classifying [topological spaces](@entry_id:155056). Its elegant equivalence to the "singletons are closed" property makes it a powerful and versatile tool for proving other theorems and for understanding the behavior of spaces under common topological constructions.