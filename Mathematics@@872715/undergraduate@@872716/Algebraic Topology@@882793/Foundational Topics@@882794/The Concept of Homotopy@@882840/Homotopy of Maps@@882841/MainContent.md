## Introduction
In the landscape of algebraic topology, we seek to understand the essential nature of shapes by studying the maps between them. However, the sheer number of [continuous maps](@entry_id:153855) can be overwhelming. The theory of homotopy provides a revolutionary solution by asking a simple yet profound question: when can one map be continuously deformed into another? This concept of "sameness up to deformation" is the cornerstone of homotopy theory, allowing us to simplify complex problems by grouping maps into [equivalence classes](@entry_id:156032).

This article unpacks the theory of homotopy, moving from its formal definition to its far-reaching applications. In "Principles and Mechanisms," you will learn the formal definition of a homotopy, see how it forms an [equivalence relation](@entry_id:144135), and explore foundational concepts like contractible spaces and homotopy equivalence. The journey continues in "Applications and Interdisciplinary Connections," where we reveal how homotopy is used to create powerful algebraic invariants like the fundamental group and to classify complex geometric objects. Finally, "Hands-On Practices" will challenge you to apply these concepts to solve concrete topological problems. By the end, you will understand how this abstract idea of continuous deformation becomes a powerful tool for classifying and understanding [topological spaces](@entry_id:155056).

## Principles and Mechanisms

In the study of topology, we are often interested not just in the properties of spaces themselves, but also in the relationships between them as revealed by [continuous maps](@entry_id:153855). However, the set of all [continuous maps](@entry_id:153855) between two spaces can be vast and complex. Algebraic topology provides a powerful tool for simplifying this picture by grouping maps that are "equivalent" in a specific sense: those that can be continuously deformed into one another. This notion of [continuous deformation](@entry_id:151691) is formalized by the concept of **homotopy**.

### The Formal Definition of Homotopy

Let $X$ and $Y$ be [topological spaces](@entry_id:155056), and let $f: X \to Y$ and $g: X \to Y$ be two [continuous maps](@entry_id:153855). We say that $f$ is **homotopic** to $g$, written $f \simeq g$, if there exists a continuous map $H: X \times [0,1] \to Y$ that satisfies two conditions:
1.  For all $x \in X$, $H(x, 0) = f(x)$.
2.  For all $x \in X$, $H(x, 1) = g(x)$.

The map $H$ is called a **homotopy** between $f$ and $g$. The parameter $t \in [0,1]$ can be intuitively thought of as "time." At time $t=0$, the map is $f$. As $t$ progresses from $0$ to $1$, the map continuously transforms, arriving at $g$ at time $t=1$. For each fixed $t$, the map $H_t: X \to Y$ defined by $H_t(x) = H(x, t)$ is a [continuous map](@entry_id:153772) from $X$ to $Y$.

An alternative and highly insightful perspective is to view a homotopy as a path within a function space [@problem_id:1657320]. Let $Y^X$ denote the set of all continuous functions from $X$ to $Y$, endowed with a suitable topology (such as the [compact-open topology](@entry_id:153876)). A homotopy $H$ from $f$ to $g$ can be seen as defining a continuous path $\hat{H}: [0,1] \to Y^X$, where $\hat{H}(t)$ is the function $H_t$. The starting point of this path, $\hat{H}(0)$, is the function $f$, and the ending point, $\hat{H}(1)$, is the function $g$. Thus, two maps are homotopic if and only if they belong to the same path-component of the function space $Y^X$.

### Fundamental Examples: Contractible Spaces

A particularly important special case of homotopy arises when a map is homotopic to a constant map. A map $f: X \to Y$ is said to be **[null-homotopic](@entry_id:153762)** if it is homotopic to a constant map $c_p: X \to Y$, defined by $c_p(x) = p$ for some fixed point $p \in Y$.

This concept leads to a classification of spaces that are, from the perspective of homotopy, trivial. A topological space $X$ is said to be **contractible** if its identity map, $\text{id}_X: X \to X$, is homotopic to a constant map $c_p: X \to X$ for some point $p \in X$. Intuitively, a contractible space is one that can be continuously shrunk to a single point within itself.

A large and important class of contractible spaces are the convex subsets of Euclidean space $\mathbb{R}^n$. For instance, consider the closed unit disk $D^2 = \{ \mathbf{v} \in \mathbb{R}^2 : \|\mathbf{v}\| \le 1 \}$. We can show it is contractible to the origin $\mathbf{0}=(0,0)$ [@problem_id:1557542]. The identity map is $\text{id}_{D^2}(\mathbf{v}) = \mathbf{v}$, and the constant map is $c_\mathbf{0}(\mathbf{v}) = \mathbf{0}$. A homotopy between them is given by the "straight-line homotopy":

$$H(\mathbf{v}, t) = (1-t)\mathbf{v}$$

Let's verify this. The map $H: D^2 \times [0,1] \to \mathbb{R}^2$ is continuous. At $t=0$, we have $H(\mathbf{v}, 0) = (1-0)\mathbf{v} = \mathbf{v} = \text{id}_{D^2}(\mathbf{v})$. At $t=1$, we have $H(\mathbf{v}, 1) = (1-1)\mathbf{v} = \mathbf{0} = c_\mathbf{0}(\mathbf{v})$. Crucially, for any $t \in [0,1]$ and any $\mathbf{v} \in D^2$, the point $H(\mathbf{v}, t)$ remains within $D^2$, since $\|H(\mathbf{v}, t)\| = \|(1-t)\mathbf{v}\| = (1-t)\|\mathbf{v}\| \le 1-t \le 1$. The entire deformation takes place inside $D^2$. This same construction shows that any convex set in $\mathbb{R}^n$ is contractible.

### The Structure of Homotopy: An Equivalence Relation

The homotopy relation $\simeq$ is not just a definition; it imposes a fundamental structure on the set of [continuous maps](@entry_id:153855) $C(X, Y)$ between two spaces. Specifically, it is an **[equivalence relation](@entry_id:144135)**, meaning it satisfies reflexivity, symmetry, and transitivity.

*   **Reflexivity**: For any map $f: X \to Y$, we have $f \simeq f$. This is demonstrated by the "stationary" homotopy $H(x, t) = f(x)$ for all $t \in [0,1]$.

*   **Symmetry**: If $f \simeq g$, then $g \simeq f$. This property is established by simply "reversing the movie." If $F: X \times [0,1] \to Y$ is a homotopy from $f$ to $g$, we can define an "inverse" homotopy $G: X \times [0,1] \to Y$ from $g$ to $f$ by setting $G(x, t) = F(x, 1-t)$ [@problem_id:1657340]. At $t=0$, $G(x, 0) = F(x, 1) = g(x)$, and at $t=1$, $G(x, 1) = F(x, 0) = f(x)$. Since $F$ is continuous, $G$ is also continuous.

*   **Transitivity**: If $f \simeq g$ and $g \simeq h$, then $f \simeq h$. This is proven by concatenating the two given homotopies. Let $F: X \times [0,1] \to Y$ be a homotopy from $f$ to $g$, and let $G: X \times [0,1] \to Y$ be a homotopy from $g$ to $h$. We construct a new homotopy $K: X \times [0,1] \to Y$ from $f$ to $h$ by performing the deformation $F$ on the time interval $[0, 1/2]$ and the deformation $G$ on the time interval $[1/2, 1]$. To do this, we must re-scale the time parameter for each part [@problem_id:1657319]:

    $$K(x, t) = \begin{cases} F(x, 2t)  \text{if } 0 \le t \le 1/2 \\ G(x, 2t - 1)  \text{if } 1/2 \le t \le 1 \end{cases}$$

    We can check that $K(x, 0) = F(x, 0) = f(x)$ and $K(x, 1) = G(x, 1) = h(x)$. The map $K$ is continuous by the pasting lemma, because at $t=1/2$, both definitions agree: $F(x, 2 \cdot 1/2) = F(x, 1) = g(x)$ and $G(x, 2 \cdot 1/2 - 1) = G(x, 0) = g(x)$ [@problem_id:1557532].

Since homotopy is an equivalence relation, it partitions the set $C(X, Y)$ into disjoint [equivalence classes](@entry_id:156032), called **homotopy classes**. The set of all homotopy classes of maps from $X$ to $Y$ is denoted by $[X, Y]$. Much of algebraic topology is concerned with studying these sets $[X, Y]$ rather than the sets $C(X, Y)$ themselves.

### Compatibility with Map Composition

The power of homotopy as a classification tool stems from its well-behaved interaction with the [composition of functions](@entry_id:148459).

Suppose we have two homotopic maps, $f_0, f_1: X \to Y$, and we pre-compose them with another [continuous map](@entry_id:153772) $g: Z \to X$. The resulting maps are $f_0 \circ g$ and $f_1 \circ g$, both from $Z$ to $Y$. It turns out that these composite maps are also homotopic. If $H: X \times [0,1] \to Y$ is the homotopy between $f_0$ and $f_1$, then a homotopy $K: Z \times [0,1] \to Y$ between $f_0 \circ g$ and $f_1 \circ g$ is given by [@problem_id:1557543]:

$$K(z, t) = H(g(z), t)$$

This construction is continuous because it is a composition of [continuous maps](@entry_id:153855). At $t=0$, $K(z, 0) = H(g(z), 0) = f_0(g(z)) = (f_0 \circ g)(z)$. At $t=1$, $K(z, 1) = H(g(z), 1) = f_1(g(z)) = (f_1 \circ g)(z)$.

Similarly, if we have homotopic maps $g_0, g_1: Y \to Z$ and we post-compose them with a map $f: X \to Y$, the resulting maps $g_0 \circ f$ and $g_1 \circ f$ are also homotopic. The homotopy is given by $L(x, t) = K(f(x), t)$, where $K$ is the homotopy between $g_0$ and $g_1$.

These compatibility properties are crucial. They imply that map composition induces a well-defined operation on homotopy classes. If $[f] \in [X,Y]$ and $[g] \in [Y,Z]$, we can define a composition of classes:
$$[g] \circ [f] = [g \circ f] \in [X,Z]$$
This operation is well-defined because if we choose different representatives $f' \in [f]$ and $g' \in [g]$, the resulting composition $g' \circ f'$ will be homotopic to $g \circ f$, and thus $[g' \circ f'] = [g \circ f]$.

### Refinements: Relative and Path Homotopy

For many applications, particularly in the definition of the fundamental group, we need a more constrained version of homotopy where the deformation leaves a part of the domain fixed.

Let $A$ be a subspace of $X$. Two maps $f, g: X \to Y$ that agree on $A$ (i.e., $f(a) = g(a)$ for all $a \in A$) are **homotopic relative to $A$** if there exists a homotopy $H: X \times [0,1] \to Y$ between them that also satisfies the additional condition:

$H(a, t) = f(a)$ for all $a \in A$ and all $t \in [0,1]$.

This means that for points in the subspace $A$, the map does not change throughout the deformation. For example, one could deform a map on a disk while keeping its values on the boundary circle fixed [@problem_id:1557531].

A primary application of this idea is **[path homotopy](@entry_id:149610)**. A **path** in a space $Z$ is a continuous map $\gamma: [0,1] \to Z$. Two paths, $\gamma_0$ and $\gamma_1$, with the same starting point $p = \gamma_0(0) = \gamma_1(0)$ and the same ending point $q = \gamma_0(1) = \gamma_1(1)$ are **path-homotopic** if they are homotopic relative to the boundary of the interval, $\{0, 1\}$. Explicitly, this means there is a [continuous map](@entry_id:153772) $F: [0,1] \times [0,1] \to Z$ such that:
*   $F(s, 0) = \gamma_0(s)$ (the homotopy starts at $\gamma_0$)
*   $F(s, 1) = \gamma_1(s)$ (the homotopy ends at $\gamma_1$)
*   $F(0, t) = p$ (the starting point is fixed)
*   $F(1, t) = q$ (the ending point is fixed)

This shows that [path homotopy](@entry_id:149610) is a direct specialization of the concept of homotopy relative to a subspace, where $X=[0,1]$, $Y=Z$, and the subspace is $A=\{0,1\}$ [@problem_id:1657330].

### Homotopy Equivalence and Topological Invariants

The concept of homotopy allows us to define a notion of "sameness" for [topological spaces](@entry_id:155056) that is weaker than homeomorphism but incredibly useful. A [continuous map](@entry_id:153772) $f: X \to Y$ is a **homotopy equivalence** if there exists a map $g: Y \to X$, called a **homotopy inverse**, such that:
$g \circ f \simeq \text{id}_X$ and $f \circ g \simeq \text{id}_Y$.

If such a pair of maps exists, we say that $X$ and $Y$ are **homotopy equivalent** or have the same **homotopy type**, written $X \simeq Y$.

For example, a contractible space $X$ is homotopy equivalent to a single point space $\{p\}$. As seen before, if $p_0 \in X$, the maps are $c: X \to \{p\}$ and $i: \{p\} \to X$ with $i(p) = p_0$. Then $c \circ i = \text{id}_{\{p\}}$, and $i \circ c$ is the constant map $c_{p_0}: X \to X$, which is homotopic to $\text{id}_X$ by definition of contractibility. A more profound example is the homotopy equivalence between the punctured plane $\mathbb{R}^2 \setminus \{\mathbf{0}\}$ and the circle $S^1$.

The main purpose of this definition is to identify properties that are preserved under homotopy equivalence. Such a property is called a **homotopy invariant**. The central mechanism for discovering and using these invariants involves the sets of homotopy classes $[X, Y]$. A homotopy equivalence $f: X \to Y$ induces a bijection of sets:
$f^*: [Y, Z] \to [X, Z]$ for any space $Z$, defined by $f^*([h]) = [h \circ f]$.

The map $f^*$ is a [bijection](@entry_id:138092) because it has an inverse $(g^*)$ induced by the homotopy inverse $g: Y \to X$. This means that from the point of view of maps into a space $Z$, the homotopy-equivalent spaces $X$ and $Y$ are indistinguishable. This powerful idea allows us to replace a complicated space with a simpler, homotopy-equivalent one for the purpose of calculations. For example, to study maps from the [punctured plane](@entry_id:150262) into the circle, $[(\mathbb{R}^2 \setminus \{\mathbf{0}\}), S^1]$, we can instead study the much simpler set $[S^1, S^1]$, which is known to be in bijection with the integers $\mathbb{Z}$ (the "degree" of the map) [@problem_id:1657304].

Finally, a technical but important related concept is the **Homotopy Extension Property (HEP)**. A pair of spaces $(X, A)$ with $A \subset X$ has the HEP if for any space $Y$, any initial map $f: X \to Y$, and any homotopy $h: A \times [0,1] \to Y$ of the restriction $f|_A$ (i.e., $h(a,0)=f(a)$), one can always extend this to a homotopy of the full map $f$. That is, there exists a homotopy $H: X \times [0,1] \to Y$ which restricts to $h$ on $A \times [0,1]$ and starts at $f$ on $X \times \{0\}$ [@problem_id:1657310]. This property ensures that certain "well-behaved" subspaces (such as subcomplexes of CW-complexes) allow for the extension of deformations, a fact that is critical for many foundational proofs in the subject.