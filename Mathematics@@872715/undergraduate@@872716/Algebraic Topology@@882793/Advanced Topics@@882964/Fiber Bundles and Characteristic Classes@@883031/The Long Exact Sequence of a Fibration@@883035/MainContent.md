## Introduction
In the study of [topological spaces](@entry_id:155056), it is often fruitful to decompose a complex space into simpler, constituent parts. A fibration provides just such a structure, presenting a 'total space' as a family of 'fibers' parameterized by a 'base space'. The fundamental question then arises: how are the topological properties of these three spaces related? The [long exact sequence of a fibration](@entry_id:161359) offers a deep and comprehensive answer, establishing a powerful algebraic link between their respective homotopy groups. It is one of the most versatile computational tools in modern algebraic topology, capable of turning sparse information about some of the spaces into concrete knowledge about others.

This article provides a comprehensive introduction to this essential sequence. The following chapters will guide you from its foundational principles to its most significant applications. Chapter one, "Principles and Mechanisms," will formally introduce the sequence, explain the crucial property of [exactness](@entry_id:268999), and demystify the [connecting homomorphism](@entry_id:160713). Chapter two, "Applications and Interdisciplinary Connections," will showcase the sequence in action, from computing the homotopy groups of spheres and Lie groups to its role in geometry and [classifying space](@entry_id:151621) theory. Finally, chapter three, "Hands-On Practices," will offer practical exercises to solidify your understanding of this indispensable topological tool.

## Principles and Mechanisms

A [fibration](@entry_id:162085), represented by a [continuous map](@entry_id:153772) $p: E \to B$, provides a way to structure a topological space $E$, known as the **total space**, as a family of spaces, called **fibers**, parameterized by another space $B$, the **base space**. For any point $b \in B$, the fiber over $b$ is the subspace $F_b = p^{-1}(b)$. A key property of a fibration is that all its fibers are homotopy equivalent. We can therefore speak of *the* fiber $F$ of the [fibration](@entry_id:162085). Given basepoints $e_0 \in E$, $b_0 = p(e_0) \in B$, and assuming $e_0$ lies in the fiber $F = p^{-1}(b_0)$, the inclusion map of the fiber is denoted by $i: F \to E$.

The profound connection between the topologies of these three spaces is captured by one of the most powerful tools in algebraic topology: the **[long exact sequence of a fibration](@entry_id:161359)**. This sequence establishes an algebraic relationship between the homotopy groups of the fiber, total space, and base space.

For any [fibration](@entry_id:162085) $F \xrightarrow{i} E \xrightarrow{p} B$, there exists a sequence of homotopy groups and homomorphisms:

$$ \cdots \to \pi_n(F) \xrightarrow{i_*} \pi_n(E) \xrightarrow{p_*} \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(F) \to \cdots \to \pi_1(B) \xrightarrow{\partial_1} \pi_0(F) \to \pi_0(E) \to \pi_0(B) $$

Here, $\pi_n(X)$ denotes the $n$-th homotopy group of a space $X$ (for $n \ge 1$) or the set of [path-components](@entry_id:145705) (for $n=0$). The maps $i_*$ and $p_*$ are the group homomorphisms induced by the inclusion $i$ and projection $p$, respectively. The most remarkable feature of this sequence is the **[connecting homomorphism](@entry_id:160713)**, $\partial_n$, which "connects" the sequence by mapping from the $n$-th homotopy group of the base to the $(n-1)$-th homotopy group of the fiber. The entire sequence is **exact**, a property that encodes a wealth of information.

### The Property of Exactness

A sequence of groups and homomorphisms is said to be exact at a particular group if the image of the incoming homomorphism is precisely equal to the kernel of the outgoing homomorphism. The [long exact sequence of a fibration](@entry_id:161359) is exact at every position. This single property has immediate and far-reaching consequences.

The most direct consequence of exactness is that the composition of any two consecutive maps in the sequence is the trivial homomorphism (the map sending every element to the identity). This is because the image of the first map is contained within the kernel of the second. Let's examine the three fundamental compositions in the sequence [@problem_id:1687054]:

1.  **$p_* \circ i_*: \pi_n(F) \to \pi_n(B)$**: This map is induced by the composite function $p \circ i: F \to B$. By definition, the inclusion map $i$ sends the fiber $F$ into the total space $E$ such that every point in the image $i(F)$ is mapped by $p$ to the single basepoint $b_0 \in B$. Thus, $p \circ i$ is a constant map. A constant map induces the trivial homomorphism on all homotopy groups. Therefore, $p_* \circ i_*$ is always the zero map.

2.  **$\partial_n \circ p_*: \pi_n(E) \to \pi_{n-1}(F)$**: The [connecting homomorphism](@entry_id:160713) $\partial_n$ intuitively measures the "obstruction" to lifting a map from the base space $B$ to the total space $E$. An element in the image of $p_*$, say $[\beta] \in \pi_n(B)$, has the form $[\beta] = p_*([\alpha])$ for some $[\alpha] \in \pi_n(E)$. This means that the map representing $[\beta]$ already has a lift to $E$—namely, the map representing $[\alpha]$. Consequently, there is no obstruction to lifting, and the [connecting homomorphism](@entry_id:160713) must map $[\beta]$ to the identity element. Thus, the composition $\partial_n \circ p_*$ is the zero map.

3.  **$i_* \circ \partial_n: \pi_n(B) \to \pi_{n-1}(E)$**: The construction of $\partial_n$ involves taking a representative map $g: S^n \to B$ and lifting it, using the homotopy [lifting property](@entry_id:156717), to a map on a hemisphere $D^n \to E$. The boundary of this lift, which lies in the fiber $F$, represents the element $\partial_n[g] \in \pi_{n-1}(F)$. By its very construction, this boundary map (from $S^{n-1}$ to $F$) is [null-homotopic](@entry_id:153762) *within the total space $E$*, as it bounds the lifted hemisphere $D^n$. Therefore, when this boundary map is included into $E$ via $i$, it represents the trivial element in $\pi_{n-1}(E)$. Hence, $i_* \circ \partial_n$ is the zero map.

Beyond this immediate consequence, exactness provides a powerful dictionary for translating properties of one map into properties of its neighbors. For any three consecutive terms $A \xrightarrow{f} B \xrightarrow{g} C$ in an exact sequence, we have $\text{Im}(f) = \text{Ker}(g)$. This implies:
*   The map $g$ is injective if and only if its kernel is trivial. This means $\text{Im}(f)$ must be the trivial group, which occurs if and only if $f$ is the zero map.
*   The map $f$ is surjective if and only if its image is all of $B$. This means $\text{Ker}(g)$ must be all of $B$, which occurs if and only if $g$ is the zero map.

As a direct application, consider the segment $\pi_k(F) \xrightarrow{i_*} \pi_k(E) \xrightarrow{p_*} \pi_k(B)$. If we are given that the map $p_*$ is injective for some $k$, its kernel must be trivial. By [exactness](@entry_id:268999), this forces the image of $i_*$ to be trivial, meaning that $i_*: \pi_k(F) \to \pi_k(E)$ is the trivial map [@problem_id:1687047]. This simple example illustrates how the rigid algebraic structure of exactness allows for precise topological deductions.

### The Connecting Homomorphism and the Path Space Fibration

The [connecting homomorphism](@entry_id:160713) $\partial_n$ is the heart of the [long exact sequence](@entry_id:153438), weaving together the homotopy groups of different dimensions. Its abstract definition via the homotopy [lifting property](@entry_id:156717) can be made exceptionally clear by studying a canonical example: the **[path space fibration](@entry_id:161224)**.

For any pointed, [path-connected space](@entry_id:156428) $(B, b_0)$, its **path space** $PB$ is the space of all paths starting at $b_0$. The map $p: PB \to B$ that evaluates a path at its endpoint, $p(\gamma) = \gamma(1)$, is a fibration. The fiber over the basepoint $b_0$ is the space of all paths that start and end at $b_0$—this is precisely the **[loop space](@entry_id:160867)** $\Omega B$. This gives the fundamentally important [fibration](@entry_id:162085):

$$ \Omega B \longrightarrow PB \longrightarrow B $$

The total space $PB$ has a remarkable property: it is always contractible. This is because any path $\gamma$ can be continuously shrunk to the constant path $c_{b_0}$ by "reeling it in" (e.g., via the homotopy $H(\gamma, t)(s) = \gamma(ts)$). A contractible space has trivial homotopy groups, so $\pi_n(PB) = 0$ for all $n \ge 0$.

Inserting this fact into the [long exact sequence](@entry_id:153438) for the [path space fibration](@entry_id:161224) gives segments of the form:
$$ \dots \to \pi_n(PB) \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to \pi_{n-1}(PB) \to \dots $$
$$ \dots \to 0 \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to 0 \to \dots $$

By exactness, the maps on either side of $\pi_n(B)$ and $\pi_{n-1}(\Omega B)$ are zero maps. This forces the [connecting homomorphism](@entry_id:160713) $\partial_n$ to be an isomorphism for all $n \ge 1$ [@problem_id:1687043]:
$$ \pi_n(B) \cong \pi_{n-1}(\Omega B) $$

This result, often called the **adjunction isomorphism**, is a cornerstone of homotopy theory. It allows us to trade dimensions, relating the homotopy of a space to that of its [loop space](@entry_id:160867). For instance, by repeated application, we find $\pi_k(\Omega^m B) \cong \pi_{k+m}(B)$. To compute the first homotopy group of the double [loop space](@entry_id:160867) of the 3-sphere, $\pi_1(\Omega^2 S^3)$, we simply apply the [isomorphism](@entry_id:137127) twice: $\pi_1(\Omega^2 S^3) \cong \pi_2(\Omega S^3) \cong \pi_3(S^3)$. Since we know $\pi_3(S^3) \cong \mathbb{Z}$, we conclude that $\pi_1(\Omega^2 S^3) \cong \mathbb{Z}$ [@problem_id:1687043].

Moreover, in this specific context, the [connecting homomorphism](@entry_id:160713) can be described very explicitly. A representative map $\alpha: I^n \to B$ for a class in $\pi_n(B)$ can be viewed as a family of paths parameterized by $I^{n-1}$. This correspondence gives rise to the image class in $\pi_{n-1}(\Omega B)$. Under the standard identification of a map into a [loop space](@entry_id:160867) with its adjoint, the map $\hat{\beta}: I^{n-1} \times I \to B$ representing the class $\partial_n[\alpha]$ is simply given by $\hat{\beta}(v,s) = \alpha(v,s)$, where $(v,s) \in I^{n-1} \times I \cong I^n$ [@problem_id:1687061]. This concrete description demystifies the [connecting homomorphism](@entry_id:160713), revealing it as a natural re-interpretation of a map.

### Key Applications and Structural Consequences

The true utility of the long exact sequence is revealed when applied to specific scenarios. By leveraging information about some of the spaces or maps, we can deduce profound properties of others.

#### The Trivial Fibration: A Baseline Case

The simplest type of fibration is the trivial (or product) fibration $p: F \times B \to B$, given by the projection $p(f,b) = b$. This [fibration](@entry_id:162085) admits a **section**, which is a map $s: B \to F \times B$ such that $p \circ s$ is the identity on $B$. For instance, we can choose a basepoint $f_0 \in F$ and define $s(b) = (f_0, b)$.

The existence of a section has a dramatic effect on the [long exact sequence](@entry_id:153438). On the level of homotopy groups, we have $p_* \circ s_* = \text{id}_{\pi_n(B)}$, which means $p_*$ is surjective and has a right-inverse, $s_*$. By exactness at $\pi_n(B)$, we have $\text{Im}(p_*) = \text{Ker}(\partial_n)$. Since $p_*$ is surjective, its image is the entire group $\pi_n(B)$. Therefore, the kernel of $\partial_n$ is $\pi_n(B)$, which implies that the [connecting homomorphism](@entry_id:160713) $\partial_n$ is the zero map for all $n \ge 1$.

When all connecting homomorphisms are trivial, the long exact sequence shatters into a collection of short [exact sequences](@entry_id:151503):
$$ 0 \to \pi_n(F) \xrightarrow{i_*} \pi_n(F \times B) \xrightarrow{p_*} \pi_n(B) \to 0 $$
Furthermore, the map $s_*$ provides a right-splitting for this sequence, which implies that it splits. Consequently, we recover the familiar [isomorphism](@entry_id:137127) for the homotopy groups of a [product space](@entry_id:151533): $\pi_n(F \times B) \cong \pi_n(F) \oplus \pi_n(B)$ [@problem_id:1687073]. This result serves as an important sanity check, confirming that the [long exact sequence](@entry_id:153438) behaves as expected in the simplest case.

#### The Role of Connectivity

The long exact sequence is particularly effective when some of the spaces involved have trivial low-dimensional homotopy groups (i.e., are highly connected).

First, consider a [fibration](@entry_id:162085) $F \to E \to B$ where the **fiber $F$ is $(k-1)$-connected**, meaning $\pi_i(F)=0$ for $1 \le i \le k-1$. Examining the relevant portion of the [long exact sequence](@entry_id:153438):
$$ \dots \to \pi_i(F) \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to \pi_{i-1}(F) \to \dots $$
For $1 \le i \le k-1$, both $\pi_i(F)$ and $\pi_{i-1}(F)$ are trivial. The sequence becomes $0 \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to 0$. Exactness at $\pi_i(E)$ implies $p_*$ is injective, and [exactness](@entry_id:268999) at $\pi_i(B)$ implies $p_*$ is surjective. Thus, $p_*$ is an [isomorphism](@entry_id:137127) for $1 \le i \le k-1$.
For the boundary case $i=k$, the sequence is $\dots \to \pi_k(F) \to \pi_k(E) \xrightarrow{p_*} \pi_k(B) \to \pi_{k-1}(F) = 0$. Exactness at $\pi_k(B)$ implies that $p_*$ is surjective. We cannot conclude [injectivity](@entry_id:147722), as $\pi_k(F)$ may be non-trivial.
In summary, if the fiber is $(k-1)$-connected, the projection map $p_*$ induces isomorphisms on homotopy groups up to dimension $k-1$ and a [surjection](@entry_id:634659) in dimension $k$ [@problem_id:1687078].

Conversely, suppose the **base space $B$ is $k$-connected**, meaning $\pi_i(B)=0$ for $1 \le i \le k$. The relevant sequence is:
$$ \dots \to \pi_i(B) \to \pi_{i-1}(F) \xrightarrow{i_*} \pi_{i-1}(E) \to \pi_{i-1}(B) \to \dots $$
For $1 \le i \le k$, both $\pi_i(B)$ and $\pi_{i-1}(B)$ are trivial. For an index $j$ such that $1 \le j \le k-1$, we look at the segment involving $\pi_j(F)$ and $\pi_j(E)$: $\pi_{j+1}(B) \to \pi_j(F) \xrightarrow{i_*} \pi_j(E) \to \pi_j(B)$. This becomes $0 \to \pi_j(F) \xrightarrow{i_*} \pi_j(E) \to 0$. This implies that $i_*$ is an isomorphism for $1 \le j \le k-1$.
For the boundary case $j=k$, the sequence is $\pi_{k+1}(B) \to \pi_k(F) \xrightarrow{i_*} \pi_k(E) \to \pi_k(B) = 0$. Exactness at $\pi_k(E)$ implies $i_*$ is surjective.
In summary, if the base space is $k$-connected, the fiber inclusion map $i_*$ induces isomorphisms on homotopy groups up to dimension $k-1$ and a [surjection](@entry_id:634659) in dimension $k$ [@problem_id:1687058].

#### Covering Spaces and Monodromy

An important special case of a [fibration](@entry_id:162085) is a **covering space projection** $p: E \to B$, provided $B$ is locally nice. In this case, the fiber $F$ is a discrete set of points. This has two major consequences for the long exact sequence.

First, for a discrete space $F$, the [higher homotopy groups](@entry_id:159688) are all trivial: $\pi_n(F) = 0$ for all $n \ge 1$. This immediately implies that any [connecting homomorphism](@entry_id:160713) $\partial_n: \pi_n(B) \to \pi_{n-1}(F)$ must be the zero map for all $n \ge 2$, since its [codomain](@entry_id:139336) is the [trivial group](@entry_id:151996) [@problem_id:1687031].

Second, the low-dimensional part of the sequence reveals a deep connection. Consider the segment:
$$ \pi_1(E) \to \pi_1(B) \xrightarrow{\partial_1} \pi_0(F) \to \pi_0(E) $$
The map of pointed sets $\partial_1: \pi_1(B) \to \pi_0(F)$ has a beautiful geometric interpretation: it is the **[monodromy action](@entry_id:154516)**. An element of $\pi_1(B)$ is a loop in the base space. Lifting this loop to a path in the total space starting at a point in the fiber, the endpoint of the lifted path will be another point in the fiber (possibly the same one). This action of loops in the base permuting the points of the fiber is precisely what is captured by $\partial_1$. For example, for the universal cover $p: S^2 \to \mathbb{RP}^2$, the fiber is a two-point space. The [non-trivial loop](@entry_id:267469) in $\pi_1(\mathbb{RP}^2) \cong \mathbb{Z}_2$ lifts to a path connecting the two [antipodal points](@entry_id:151589) in the fiber, so the [monodromy action](@entry_id:154516) is non-trivial [@problem_id:1687031].

Furthermore, if the total space $E$ is path-connected, then $\pi_0(E)$ is a single point. By [exactness](@entry_id:268999) at $\pi_0(F)$, the image of $\partial_1$ must equal the kernel of the map $\pi_0(F) \to \pi_0(E)$. Since the target is a single point, this kernel is all of $\pi_0(F)$. Therefore, the connecting map $\partial_1: \pi_1(B) \to \pi_0(F)$ is always surjective when $E$ is path-connected [@problem_id:1687081]. This holds for any [fibration](@entry_id:162085), not just [covering spaces](@entry_id:152318).

### Computational Examples: The Stiefel Manifolds

The ultimate test of the [long exact sequence](@entry_id:153438) is its ability to facilitate the computation of previously unknown homotopy groups. A rich source of examples comes from the **Stiefel manifolds**, spaces of orthonormal frames in a vector space.

Consider the [fibration](@entry_id:162085) $S^3 \to V_2(\mathbb{R}^5) \to S^4$, where $V_2(\mathbb{R}^5)$ is the space of 2-frames in $\mathbb{R}^5$. We want to compute $\pi_3(V_2(\mathbb{R}^5))$. The relevant portion of the long exact sequence is:
$$ \dots \to \pi_4(S^4) \xrightarrow{\partial_4} \pi_3(S^3) \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \xrightarrow{p_*} \pi_3(S^4) \to \dots $$
We substitute the known homotopy groups: $\pi_4(S^4) \cong \mathbb{Z}$, $\pi_3(S^3) \cong \mathbb{Z}$, and $\pi_3(S^4) = 0$. The sequence becomes:
$$ \mathbb{Z} \xrightarrow{\partial_4} \mathbb{Z} \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \to 0 $$
A deeper result (from the study of [characteristic classes](@entry_id:160596)) states that the [connecting homomorphism](@entry_id:160713) $\partial_4: \mathbb{Z} \to \mathbb{Z}$ is multiplication by 2. Now we can use exactness to solve for the unknown group.
1.  Exactness at $\pi_3(S^3)$: $\text{Ker}(i_*) = \text{Im}(\partial_4)$. Since $\partial_4$ is multiplication by 2, its image is the subgroup $2\mathbb{Z} \subset \mathbb{Z}$. So, $\text{Ker}(i_*) = 2\mathbb{Z}$.
2.  Exactness at $\pi_3(V_2(\mathbb{R}^5))$: $\text{Im}(i_*) = \text{Ker}(p_*)$. Since $p_*$ maps to the trivial group, its kernel is the entire domain, $\pi_3(V_2(\mathbb{R}^5))$. Thus, $i_*$ is surjective.
3.  By the First Isomorphism Theorem for groups, $\text{Im}(i_*) \cong \pi_3(S^3) / \text{Ker}(i_*)$.
Putting it all together:
$$ \pi_3(V_2(\mathbb{R}^5)) = \text{Im}(i_*) \cong \mathbb{Z} / 2\mathbb{Z} \cong \mathbb{Z}_2 $$
The [long exact sequence](@entry_id:153438) has allowed us to determine that the third homotopy group of this Stiefel manifold is the cyclic group of order 2 [@problem_id:1687052]. This illustrates how the sequence frames the computation as a **[group extension problem](@entry_id:145893)**, where the middle group $\pi_n(E)$ is constrained by a [short exact sequence](@entry_id:137930) involving kernels and cokernels of the connecting homomorphisms.

A similar calculation can be performed for the complex Stiefel manifold in the [fibration](@entry_id:162085) $S^3 \to V_2(\mathbb{C}^3) \to S^5$ to compute $\pi_4(V_2(\mathbb{C}^3))$. The sequence is $\pi_5(S^5) \xrightarrow{\partial_5} \pi_4(S^3) \xrightarrow{i_*} \pi_4(V_2(\mathbb{C}^3)) \xrightarrow{p_*} \pi_4(S^5)$. Knowing $\pi_4(S^5)=0$ and that, in this case, $\partial_5$ is the zero map, [exactness](@entry_id:268999) immediately implies that $i_*: \pi_4(S^3) \to \pi_4(V_2(\mathbb{C}^3))$ is an isomorphism. Since $\pi_4(S^3) \cong \mathbb{Z}_2$, we again find $\pi_4(V_2(\mathbb{C}^3)) \cong \mathbb{Z}_2$ [@problem_id:1687069].

In conclusion, the [long exact sequence of a fibration](@entry_id:161359) is a deep and versatile principle. It provides a rigid algebraic framework that links the homotopy groups of the fiber, total space, and base space. By understanding the property of [exactness](@entry_id:268999) and the nature of the [connecting homomorphism](@entry_id:160713), we gain a powerful mechanism for exploring the structure of [topological spaces](@entry_id:155056) and computing homotopy groups that would otherwise be far beyond our reach.