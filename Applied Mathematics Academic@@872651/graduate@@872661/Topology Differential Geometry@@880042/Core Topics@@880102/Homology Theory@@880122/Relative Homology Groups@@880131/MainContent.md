## Introduction
In algebraic topology, [singular homology](@entry_id:158380) offers a powerful lens for understanding the structure of a space, such as its "holes." But what happens when we want to understand the structure of a space *in relation to* one of its subspaces? How do we precisely measure the topological features that a space $X$ has which are not already part of a subspace $A$? This fundamental question motivates the development of [relative homology](@entry_id:159348) groups.

Relative homology provides the rigorous algebraic framework to answer this question. It allows us to isolate and analyze the topological structure that is "added" when we move from a subspace to a larger ambient space. This article provides a comprehensive exploration of this essential tool.

We will begin in the first chapter, **Principles and Mechanisms**, by defining the relative [chain complex](@entry_id:150246) and introducing the theory's most powerful computational engine: the [long exact sequence of a pair](@entry_id:158857). Next, in **Applications and Interdisciplinary Connections**, we will see this theory in action, exploring how it underpins [cellular homology](@entry_id:157864), clarifies the structure of manifolds with boundaries, and forges connections to fields like [knot theory](@entry_id:141161) and algebraic geometry. Finally, **Hands-On Practices** will offer a series of guided problems to help you master the computational and conceptual aspects of [relative homology](@entry_id:159348), transforming abstract theory into practical skill.

## Principles and Mechanisms

In the study of [topological spaces](@entry_id:155056), [singular homology](@entry_id:158380) provides a powerful algebraic invariant, $H_n(X)$, which counts the $n$-dimensional "holes" of a space $X$. However, we often wish to understand the relationship between a space and one of its subspaces. For instance, how does the topology of a space $X$ change when considered *relative* to a subspace $A$? What new topological features arise in $X$ that are not already present in $A$? To answer these questions, we introduce the concept of **[relative homology](@entry_id:159348) groups**, denoted $H_n(X, A)$. These algebraic tools form a cornerstone of modern algebraic topology, providing a precise way to analyze the topological structure that $X$ possesses beyond what is contained in $A$.

### The Relative Chain Complex

The foundation of [relative homology](@entry_id:159348) lies in a modification of the singular [chain complex](@entry_id:150246). Let $(X, A)$ be a pair of topological spaces, where $A$ is a subspace of $X$. For each non-negative integer $n$, the group of singular $n$-chains of $X$, denoted $C_n(X)$, is the free abelian group on the set of all [continuous maps](@entry_id:153855) $\sigma: \Delta^n \to X$, where $\Delta^n$ is the standard $n$-simplex. Since $A$ is a subspace of $X$, the chain group $C_n(A)$ is naturally a subgroup of $C_n(X)$.

We define the **group of relative $n$-chains** of the pair $(X, A)$ as the [quotient group](@entry_id:142790):
$$
C_n(X, A) := \frac{C_n(X)}{C_n(A)}
$$
An element of $C_n(X, A)$ is an [equivalence class](@entry_id:140585) of chains in $X$, where two chains are considered equivalent if their difference is a chain contained entirely within $A$. Intuitively, this construction "forgets" any part of a chain that lies in $A$. The standard [boundary operator](@entry_id:160216) $\partial: C_n(X) \to C_{n-1}(X)$ descends to a well-defined homomorphism $\partial: C_n(X, A) \to C_{n-1}(X, A)$ because if $c \in C_n(A)$, then $\partial c \in C_{n-1}(A)$. This makes the sequence of relative chain groups $(C_\bullet(X, A), \partial)$ a [chain complex](@entry_id:150246).

The homology of this [chain complex](@entry_id:150246) defines the **[relative homology](@entry_id:159348) groups** of the pair $(X, A)$:
$$
H_n(X, A) := H_n(C_\bullet(X, A)) = \frac{\ker(\partial: C_n(X, A) \to C_{n-1}(X, A))}{\text{im}(\partial: C_{n+1}(X, A) \to C_n(X, A))}
$$
An element of $H_n(X, A)$ is represented by a **relative $n$-cycle**, which is a chain $c \in C_n(X)$ whose boundary lies entirely in $A$, i.e., $\partial c \in C_{n-1}(A)$. Such a relative cycle is a **relative $n$-boundary** if it is homologous, modulo chains in $A$, to the boundary of an $(n+1)$-chain in $X$.

### The Long Exact Sequence of a Pair

The true power of [relative homology](@entry_id:159348) is unlocked by its connection to the absolute homology groups of $X$ and $A$. This relationship is captured in a fundamental algebraic structure known as the **[long exact sequence of a pair](@entry_id:158857)**. For any pair $(X, A)$, there exists a sequence of homology groups connected by natural homomorphisms:
$$
\dots \to H_n(A) \xrightarrow{i_*} H_n(X) \xrightarrow{j_*} H_n(X, A) \xrightarrow{\partial_*} H_{n-1}(A) \to \dots
$$
This sequence extends infinitely in both directions and is **exact**. Exactness at a group means that the image of the incoming homomorphism is precisely equal to the kernel of the outgoing homomorphism. This single property provides a remarkably powerful computational and theoretical engine.

Let us examine the homomorphisms in this sequence:
1.  **$i_*: H_n(A) \to H_n(X)$**: This map is induced by the inclusion map $i: A \hookrightarrow X$. It takes a homology class in $A$ and treats it as a homology class in the larger space $X$. Its image, $\text{im}(i_*)$, consists of the $n$-dimensional holes of $X$ that were already present in $A$.

2.  **$j_*: H_n(X) \to H_n(X, A)$**: This map is induced by the [quotient map](@entry_id:140877) from chains $C_n(X)$ to relative chains $C_n(X,A)$. It takes a cycle in $X$ and considers it as a relative cycle.

3.  **$\partial_*: H_n(X, A) \to H_{n-1}(A)$**: This is the **[connecting homomorphism](@entry_id:160713)**, a crucial and non-obvious map that bridges dimensions.

By the definition of exactness at $H_n(X)$, we have the fundamental relationship $\text{im}(i_*) = \ker(j_*)$ [@problem_id:1670808]. This algebraic statement has a clear topological meaning: the $n$-cycles in $X$ that become trivial in [relative homology](@entry_id:159348) (i.e., belong to $\ker(j_*)$) are precisely those that are homologous to a cycle coming from the subspace $A$ (i.e., belong to $\text{im}(i_*)$).

### The Connecting Homomorphism: A Geometric Bridge

The [connecting homomorphism](@entry_id:160713) $\partial_*$ is the key to the [long exact sequence](@entry_id:153438). Its geometric definition is quite natural. Let $[\alpha] \in H_n(X, A)$ be a [relative homology](@entry_id:159348) class represented by a relative cycle $\alpha \in C_n(X)$. By definition, $\partial \alpha$ is an $(n-1)$-chain in $A$. Since the [boundary of a boundary is zero](@entry_id:269907), we have $\partial(\partial \alpha) = 0$, which means that $\partial \alpha$ is itself a cycle in $A$. The [connecting homomorphism](@entry_id:160713) is defined by mapping the relative class of $\alpha$ to the absolute class of its boundary:
$$
\partial_*([\alpha]) = [\partial \alpha] \in H_{n-1}(A)
$$
A classic example illustrates this perfectly. Let $X$ be the closed 2-disk $D^2$ and $A$ be its boundary circle $S^1$. The disk itself, viewed as a 2-chain $\iota_{D^2}$, is not a cycle in $X$ because its boundary, the circle $S^1$, is non-zero. However, since its boundary lies entirely in the subspace $A=S^1$, $\iota_{D^2}$ represents a relative 2-cycle of the pair $(D^2, S^1)$. Applying the [connecting homomorphism](@entry_id:160713) $\partial_*: H_2(D^2, S^1) \to H_1(S^1)$ to the class $[\iota_{D^2}]$ means we take its boundary, which is the 1-chain for $S^1$. This 1-chain represents the non-trivial generator of $H_1(S^1) \cong \mathbb{Z}$ [@problem_id:1670811]. In fact, the [long exact sequence](@entry_id:153438) shows that this map is an isomorphism, providing a concrete link between a relative 2-dimensional feature (the disk "relative to its boundary") and an absolute 1-dimensional feature (the boundary circle itself).

### Computational Applications of the Long Exact Sequence

The exactness of the sequence allows us to compute unknown homology groups from known ones. If several groups in the sequence are trivial, the maps between the remaining groups are often forced to be isomorphisms or zero maps.

For instance, suppose we are given a pair $(X, A)$ where $H_2(X) = 0$, $H_1(A) \cong \mathbb{Z}$, and we are told the [connecting homomorphism](@entry_id:160713) $\partial_*: H_2(X, A) \to H_1(A)$ is surjective. The relevant part of the [long exact sequence](@entry_id:153438) is:
$$
H_2(X) \to H_2(X, A) \xrightarrow{\partial_*} H_1(A)
$$
Since $H_2(X) = 0$, the image of the first map is the trivial group. By [exactness](@entry_id:268999) at $H_2(X, A)$, we must have $\ker(\partial_*) = 0$, meaning $\partial_*$ is injective. As we were given that $\partial_*$ is also surjective, it must be an isomorphism. Therefore, we can deduce that $H_2(X, A) \cong H_1(A) \cong \mathbb{Z}$ without any further geometric information [@problem_id:1670767].

More sophisticated applications involve analyzing the induced maps. Consider the Möbius strip $M$ and its boundary circle $A$. One can show that the inclusion map $i: A \hookrightarrow M$ induces a homomorphism $i_*: H_1(A) \to H_1(M)$ that corresponds to the multiplication-by-2 map from $\mathbb{Z}$ to $\mathbb{Z}$. Let's compute $H_1(M, A)$. The relevant part of the LES is:
$$
H_1(A) \xrightarrow{i_*} H_1(M) \xrightarrow{j_*} H_1(M, A) \to H_0(A)
$$
From the long exact sequence, one can establish the isomorphism $H_1(M, A) \cong H_1(M) / \text{im}(i_*)$. Substituting the known groups and map, we get:
$$
H_1(M, A) \cong \mathbb{Z} / (2\mathbb{Z}) \cong \mathbb{Z}_2
$$
This demonstrates that the [relative homology](@entry_id:159348) can capture torsion information that is not immediately obvious from the absolute homology groups of $X$ and $A$ alone. In this case, the first [relative homology](@entry_id:159348) group being $\mathbb{Z}_2$ reflects the non-orientable nature of the Möbius strip [@problem_id:1691887].

### Geometric Interpretation and Further Theorems

Beyond computation, [relative homology](@entry_id:159348) groups and the [long exact sequence](@entry_id:153438) provide profound geometric insights. For example, what does it mean for a [relative homology](@entry_id:159348) group to be trivial? Consider the implication of $H_1(X, A) = 0$. The LES segment is:
$$
H_1(X) \xrightarrow{j_*} H_1(X, A) \xrightarrow{\partial_*} H_0(A) \xrightarrow{i_*} H_0(X)
$$
If $H_1(X, A) = 0$, [exactness](@entry_id:268999) implies that the map $\partial_*$ is the zero map, and therefore its kernel is all of $H_1(X, A)$. By exactness at $H_0(A)$, this means $\text{im}(\partial_*) = \ker(i_*) = 0$, so $i_*: H_0(A) \to H_0(X)$ is injective. This tells us that any two points in $A$ that can be connected by a path in $X$ can also be connected by a path within $A$. Furthermore, exactness at $H_1(X,A)$ implies that $j_*$ must have image 0, which means $H_1(X)$ maps to 0 in $H_1(X,A)$. The geometric interpretation is subtle but powerful: it can be shown that $H_1(X, A) = 0$ is equivalent to the statement that any path in $X$ with both of its endpoints in $A$ is homologous in $X$ to a path that lies entirely within $A$ [@problem_id:1670828].

Two other fundamental results expand the utility of [relative homology](@entry_id:159348).

#### Excision Theorem
The **Excision Theorem** states that if $Z$ is a subset of $A$ whose closure is contained in the interior of $A$, then the inclusion $(X \setminus Z, A \setminus Z) \hookrightarrow (X, A)$ induces an [isomorphism](@entry_id:137127) on all [relative homology](@entry_id:159348) groups:
$$
H_n(X \setminus Z, A \setminus Z) \cong H_n(X, A)
$$
This theorem formalizes the idea that [relative homology](@entry_id:159348) depends only on the structure of $X$ "near" the boundary of $A$. We can "excise" or cut out parts of $A$ deep in its interior without affecting the result. For a pair $(X, A)$ that is a **good pair** (e.g., $A$ is a closed [subcomplex](@entry_id:264130) of a CW complex $X$), this theorem leads to a crucial isomorphism:
$$
H_n(X, A) \cong \tilde{H}_n(X/A)
$$
where $\tilde{H}_n$ denotes [reduced homology](@entry_id:274187) and $X/A$ is the [quotient space](@entry_id:148218) obtained by collapsing $A$ to a point. This connects [relative homology](@entry_id:159348) to the absolute homology of a related space, which is often easier to visualize. For example, consider the pair $(S^2, S^1)$ where $S^1$ is the equator. The quotient space $S^2/S^1$ is topologically a wedge of two spheres, $S^2 \vee S^2$. The second homology of $S^2 \vee S^2$ is $\mathbb{Z} \oplus \mathbb{Z}$, so we can immediately deduce that $H_2(S^2, S^1) \cong \mathbb{Z} \oplus \mathbb{Z}$ [@problem_id:1670806]. Similarly, for a sphere $S^2$ and a [closed disk](@entry_id:148403) $A \subset S^2$, we can excise the interior of the disk to show $H_n(S^2, A) \cong H_n(S^2 \setminus \text{int}(A), A \setminus \text{int}(A)) \cong H_n(D^2, S^1)$, simplifying the computation [@problem_id:1670788].

#### Long Exact Sequence of a Triple
The entire framework can be generalized. For a **triple of spaces** $(X, A, B)$ with $B \subset A \subset X$, there is a natural [short exact sequence](@entry_id:137930) of chain complexes:
$$
0 \to C_\bullet(A, B) \to C_\bullet(X, B) \to C_\bullet(X, A) \to 0
$$
This, in turn, induces a [long exact sequence](@entry_id:153438) in homology, relating the [relative homology](@entry_id:159348) groups of the three pairs involved:
$$
\dots \to H_n(A, B) \to H_n(X, B) \to H_n(X, A) \xrightarrow{\partial} H_{n-1}(A, B) \to \dots
$$
This sequence allows for even more intricate analysis, such as breaking down a complex [relative homology](@entry_id:159348) computation into more manageable steps [@problem_id:1670789].

### A Case Study: The Solid Torus

To see these principles in action, let's analyze the pair $(X, A)$ where $X = S^1 \times D^2$ is a solid torus and $A = S^1 \times S^1$ is its boundary torus.
The space $X$ is homotopy equivalent to $S^1$, so its only non-[trivial homology](@entry_id:265875) groups are $H_0(X) \cong \mathbb{Z}$ and $H_1(X) \cong \mathbb{Z}$. The boundary $A$ is a [2-torus](@entry_id:265991), with $H_0(A) \cong \mathbb{Z}$, $H_1(A) \cong \mathbb{Z} \oplus \mathbb{Z}$, and $H_2(A) \cong \mathbb{Z}$. All higher homology groups are trivial.

Let's compute $H_3(X, A)$ and $H_2(X, A)$.
For $n=3$, the LES segment is:
$$
H_3(A) \to H_3(X) \to H_3(X, A) \to H_2(A) \to H_2(X)
$$
Substituting the known groups:
$$
0 \to 0 \to H_3(X, A) \xrightarrow{\partial_*} \mathbb{Z} \to 0
$$
Exactness forces the [connecting homomorphism](@entry_id:160713) $\partial_*$ to be an isomorphism, so $H_3(X, A) \cong \mathbb{Z}$. This reveals a 3-dimensional relative feature, even though neither $X$ nor $A$ has any 3-dimensional homology.

For $n=2$, the LES segment is:
$$
H_2(A) \xrightarrow{i_*} H_2(X) \to H_2(X, A) \to H_1(A) \xrightarrow{i_*} H_1(X)
$$
Substituting the known groups:
$$
\mathbb{Z} \xrightarrow{i_*} 0 \to H_2(X, A) \to \mathbb{Z} \oplus \mathbb{Z} \xrightarrow{i_*} \mathbb{Z}
$$
From the first part of this snippet, $0 \to H_2(X, A) \to H_1(A)$, we see that $H_2(X, A)$ is isomorphic to the kernel of the map $i_*: H_1(A) \to H_1(X)$. The group $H_1(A)$ is generated by the meridian (a circle bounding a disk slice of $X$) and the longitude (a circle running parallel to the core of $X$). Under the inclusion $A \hookrightarrow X$, the meridian becomes the boundary of a disk and is thus null-homologous in $X$. The longitude becomes homologous to the core circle of $X$. Therefore, the map $i_*: \mathbb{Z} \oplus \mathbb{Z} \to \mathbb{Z}$ sends a class $(m, l)$ to $l$. The kernel of this map is the subgroup of meridional loops, which is isomorphic to $\mathbb{Z}$. Thus, $H_2(X, A) \cong \mathbb{Z}$ [@problem_id:1670830].

These computations demonstrate that [relative homology](@entry_id:159348) is not merely an abstract construction; it is a vital tool for revealing the hidden topological structures that emerge when spaces are built upon one another.