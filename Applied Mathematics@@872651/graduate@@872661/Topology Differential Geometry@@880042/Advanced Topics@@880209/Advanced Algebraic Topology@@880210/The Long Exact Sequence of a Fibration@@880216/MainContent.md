## Introduction
The [long exact sequence](@entry_id:153438) of a [fibration](@entry_id:162085) stands as one of the most powerful and versatile instruments in algebraic topology. It serves as a crucial bridge, translating complex geometric relationships between spaces into the structured, computable language of algebra. At its core, the sequence addresses a fundamental problem: given a [fibration](@entry_id:162085)—a map $p: E \to B$ where the space $E$ is "fibered" over the base $B$ with fibers $F$—how can we relate the [topological invariants](@entry_id:138526), specifically the homotopy groups, of these three spaces? The answer lies in an elegant algebraic structure that connects them in a precise, predictable way.

This article will guide you through this cornerstone of topology. In "Principles and Mechanisms," we will introduce the [long exact sequence](@entry_id:153438) itself, delving into the geometric intuition behind its maps and the central role of the [connecting homomorphism](@entry_id:160713). Next, "Applications and Interdisciplinary Connections" will showcase the sequence in action, demonstrating its power to compute the notoriously difficult homotopy groups of spheres, unravel the structure of Lie groups, and forge links to theoretical physics. Finally, "Hands-On Practices" will provide you with the opportunity to apply these concepts to concrete problems, solidifying your understanding of this essential tool.

## Principles and Mechanisms

The [long exact sequence](@entry_id:153438) of a fibration is one of the most powerful and fundamental tools in algebraic topology. It provides a computable, algebraic link between the homotopy groups of the three spaces involved in a [fibration](@entry_id:162085): the total space, the base space, and the fiber. This sequence allows us to deduce information about one space from knowledge of the other two, turning topological problems into algebraic ones. In this chapter, we will establish the sequence, explore the geometric origins of its constituent maps, and demonstrate its utility through a series of foundational applications and computations.

### The Long Exact Sequence in Homotopy

Let $p: E \to B$ be a Serre [fibration](@entry_id:162085) with total space $E$, base space $B$, and fiber $F$. After choosing a basepoint $b_0 \in B$ and a basepoint $e_0$ in the fiber $F = p^{-1}(b_0)$, which also serves as a basepoint for $E$, we have a sequence of inclusions and projections: $F \xrightarrow{i} E \xrightarrow{p} B$. These maps induce homomorphisms on the corresponding homotopy groups. The central theorem states that these are linked by a third map, the **[connecting homomorphism](@entry_id:160713)**, into a long exact sequence.

**Theorem (Long Exact Sequence of a Fibration):** For a [fibration](@entry_id:162085) $F \xrightarrow{i} E \xrightarrow{p} B$ with chosen basepoints, there is a [long exact sequence of homotopy groups](@entry_id:273540) (for $n \ge 1$) and pointed sets (for $n=0$):
$$
\dots \to \pi_n(F) \xrightarrow{i_*} \pi_n(E) \xrightarrow{p_*} \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(F) \to \dots \to \pi_0(F) \to \pi_0(E) \to \pi_0(B)
$$
The maps $i_*$ and $p_*$ are the homomorphisms induced by the [continuous maps](@entry_id:153855) $i: F \to E$ (inclusion) and $p: E \to B$ (projection), respectively. The map $\partial_n$ is the [connecting homomorphism](@entry_id:160713). The sequence is **exact**, which means that at each stage, the image of the incoming map is precisely the kernel of the outgoing map.

A direct and crucial consequence of [exactness](@entry_id:268999) is that the composition of any two consecutive maps in the sequence is the trivial homomorphism. Let's examine why this holds from a geometric perspective, which provides our first insights into the nature of these maps [@problem_id:1687054].

*   **The composition $p_* \circ i_*$:** This map is induced by the composite map $p \circ i: F \to B$. By definition of the fiber, the inclusion $i$ maps $F$ into $p^{-1}(b_0)$. Thus, for any point $x \in F$, $p(i(x)) = b_0$. The map $p \circ i$ is the constant map to the basepoint $b_0$. A constant map induces the trivial homomorphism on all positive-dimensional homotopy groups. Therefore, $p_* \circ i_* = (p \circ i)_*$ is the zero map.

*   **The composition $\partial_n \circ p_*$:** The [connecting homomorphism](@entry_id:160713) $\partial_n$ is constructed via a lifting process. An element in $\mathrm{Im}(p_*)$ is of the form $[p \circ \alpha]$ for some map $\alpha: S^n \to E$. The very existence of the map $\alpha$ serves as a "lift" of the map $p \circ \alpha$ to the space $E$. As we will see, the [connecting homomorphism](@entry_id:160713) measures the obstruction to lifting a map from the base space to the total space; if a lift already exists, the obstruction is trivial. Hence, any element in the image of $p_*$ is sent to the [identity element](@entry_id:139321) by $\partial_n$, meaning $\partial_n \circ p_* = 0$.

*   **The composition $i_* \circ \partial_n$:** An element $[f] = \partial_n([\alpha])$ in $\pi_{n-1}(F)$ is constructed by restricting a certain lift of $\alpha$ to a boundary sphere. This map $f: S^{n-1} \to F$ is, by its very construction, [null-homotopic](@entry_id:153762) in the larger space $E$. That is, the map $i \circ f: S^{n-1} \to E$ can be extended to a map from the disk $D^n$ into $E$. This implies that its homotopy class, $i_*([f])$, is the identity in $\pi_{n-1}(E)$. Thus, $i_* \circ \partial_n = 0$.

### The Connecting Homomorphism: The Geometric Bridge

The maps $i_*$ and $p_*$ are straightforward, but the [connecting homomorphism](@entry_id:160713) $\partial_n$ is the heart of the long exact sequence. It arises directly from the **homotopy [lifting property](@entry_id:156717)** that defines a [fibration](@entry_id:162085).

Let $[\alpha] \in \pi_n(B)$ be a homotopy class represented by a map $\alpha: (I^n, \partial I^n) \to (B, b_0)$, where $I^n$ is the $n$-cube. The [connecting homomorphism](@entry_id:160713) $\partial_n([\alpha])$ is constructed as follows:
1.  Since $\alpha$ sends the boundary $\partial I^n$ to the basepoint $b_0$, we can think of the pair $(I^n, \partial I^n)$ as a relative CW complex.
2.  We seek to lift $\alpha$ to a map $\tilde{\alpha}: I^n \to E$ such that $p \circ \tilde{\alpha} = \alpha$. The [fibration](@entry_id:162085) property guarantees that such a lift exists relative to a given lift on the boundary. We choose a trivial lift on *part* of the boundary: let the basepoint $e_0 \in F$ be the lift of $b_0$.
3.  The map $\alpha$ restricted to the "top" face of the cube, $I^{n-1} \times \{1\}$, is a map to $b_0$. The lift $\tilde{\alpha}$ on this face is not constrained to be constant. Instead, its image must lie entirely within the fiber $F = p^{-1}(b_0)$.
4.  This restriction, $\tilde{\alpha}|_{I^{n-1} \times \{1\}}$, gives a map from an $(n-1)$-cube into $F$ that sends the boundary to $e_0$. This map represents a class in $\pi_{n-1}(F)$, which we define as $\partial_n([\alpha])$.

This construction can be made very explicit in the case of the **[path space fibration](@entry_id:161224)**, a canonical example. For any [pointed space](@entry_id:265918) $(B, b_0)$, let $PB$ be the space of all paths in $B$ starting at $b_0$. The map $p: PB \to B$ sending a path $\gamma$ to its endpoint $\gamma(1)$ is a [fibration](@entry_id:162085). The fiber over $b_0$ is the space of all paths starting and ending at $b_0$—the **[loop space](@entry_id:160867)** $\Omega B$. Consider a class $[\alpha] \in \pi_n(B)$, represented by $\alpha: I^n \to B$. We can identify $I^n$ with $I^{n-1} \times I$. The map $\alpha$ can be viewed as a family of paths in $t \in I$, parameterized by $v \in I^{n-1}$. This defines a lift $\tilde{\alpha}: I^n \to PB$. The [connecting homomorphism](@entry_id:160713) $\partial_n([\alpha])$ is represented by the map into the fiber $\Omega B$ obtained at the endpoint $t=1$. Under the standard adjoint relation between maps into a [loop space](@entry_id:160867), $I^{n-1} \to \Omega B$, and maps from a product space, $I^{n-1} \times I \to B$, the representative map $\hat{\beta}$ for the class $\partial_n([\alpha])$ is simply the original map $\alpha$ itself, when viewing $I^n$ as $I^{n-1} \times I$ [@problem_id:1687061].

The lowest-dimensional connecting map, $\partial_1: \pi_1(B) \to \pi_0(F)$, has a particularly intuitive interpretation. An element of $\pi_1(B, b_0)$ is a loop $\gamma: [0,1] \to B$. By the homotopy [lifting property](@entry_id:156717), we can lift this to a path $\tilde{\gamma}: [0,1] \to E$ starting at our basepoint $e_0 \in F$. Since $p(\tilde{\gamma}(1)) = \gamma(1) = b_0$, the endpoint $\tilde{\gamma}(1)$ must lie in the fiber $F$. The map $\partial_1$ sends the class $[\gamma]$ to the path-component of $F$ containing the point $\tilde{\gamma}(1)$. This mapping is precisely the **[monodromy action](@entry_id:154516)** of the fundamental group of the base on the fiber. For example, in the universal covering [fibration](@entry_id:162085) $p: S^2 \to \mathbb{RP}^2$, the fiber $F$ is a discrete two-point space. The [non-trivial loop](@entry_id:267469) in $\pi_1(\mathbb{RP}^2) \cong \mathbb{Z}_2$ lifts to a path in $S^2$ connecting one point in the fiber to its antipode, the other point in the fiber. Thus, $\partial_1$ maps the non-trivial element of $\pi_1(\mathbb{RP}^2)$ to the non-basepoint element of $\pi_0(F)$ [@problem_id:1687031].

### Fundamental Applications and Consequences

The power of the long exact sequence lies in its ability to translate topological conditions into algebraic constraints. By assuming one of the spaces in a [fibration](@entry_id:162085) is homotopically simple, we can deduce profound relationships between the other two.

#### Homotopy Groups of Loop Spaces

The [path space fibration](@entry_id:161224) $\Omega B \to PB \to B$ is a cornerstone example. The total space $PB$ is always contractible, meaning all its homotopy groups are trivial: $\pi_n(PB) = 0$ for all $n \ge 0$. Inserting this into the [long exact sequence](@entry_id:153438) gives, for each $n \ge 1$, a segment:
$$
\dots \to \pi_n(PB) \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to \pi_{n-1}(PB) \to \dots
$$
Substituting $\pi_n(PB) = 0$ and $\pi_{n-1}(PB) = 0$, we get:
$$
\dots \to 0 \to \pi_n(B) \xrightarrow{\partial_n} \pi_{n-1}(\Omega B) \to 0 \to \dots
$$
For this sequence to be exact, the map $\partial_n$ must be injective (its kernel is the image of the zero map) and surjective (its image is the kernel of the zero map). Therefore, $\partial_n$ is an [isomorphism](@entry_id:137127). This establishes a fundamental relationship:
$$
\pi_n(B) \cong \pi_{n-1}(\Omega B) \quad \text{for all } n \ge 1.
$$
This result allows us to trade dimensions for loops. For instance, to compute the fundamental group of the double [loop space](@entry_id:160867) of the 3-sphere, $\pi_1(\Omega^2 S^3)$, we can apply this [isomorphism](@entry_id:137127) twice:
$$
\pi_1(\Omega^2 S^3) \cong \pi_2(\Omega S^3) \cong \pi_3(S^3)
$$
Given the classical result $\pi_3(S^3) \cong \mathbb{Z}$, we immediately find that $\pi_1(\Omega^2 S^3) \cong \mathbb{Z}$ [@problem_id:1687043]. This same principle is a special case of a more general result: if the total space $E$ of a [fibration](@entry_id:162085) is contractible, the long exact sequence implies $\pi_n(F) \cong \pi_{n+1}(B)$ for all $n \ge 1$ [@problem_id:1687029].

#### Relating Spaces via Fibrations

The long exact sequence serves as a sensitive instrument for comparing the homotopy of spaces linked by a [fibration](@entry_id:162085).

*   **Weakly Contractible Base Space:** If the base space $B$ is weakly contractible (i.e., $\pi_k(B)=0$ for all $k \ge 0$), the long exact sequence breaks into a series of short [exact sequences](@entry_id:151503):
    $$
    \dots \to \pi_k(B)=0 \to \pi_{k-1}(F) \xrightarrow{i_*} \pi_{k-1}(E) \to \pi_{k-1}(B)=0 \to \dots
    $$
    Exactness immediately implies that each $i_*: \pi_k(F) \to \pi_k(E)$ is an [isomorphism](@entry_id:137127) for all $k \ge 0$. This means that if the base of a [fibration](@entry_id:162085) is homotopically trivial, the fiber and the total space are weakly homotopy equivalent [@problem_id:1687070].

*   **Highly Connected Fibers:** Suppose the fiber $F$ is highly connected. Specifically, let $F$ be $(k-1)$-connected, meaning $\pi_i(F)=0$ for all $1 \le i \le k-1$. Let's examine the relevant portion of the long exact sequence:
    $$
    \dots \to \pi_i(F) \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to \pi_{i-1}(F) \to \dots
    $$
    If $i \le k-1$, then both $\pi_i(F)$ and $\pi_{i-1}(F)$ are trivial. The sequence becomes $0 \to \pi_i(E) \xrightarrow{p_*} \pi_i(B) \to 0$, which implies that $p_*$ is an isomorphism. If $i=k$, then $\pi_{k-1}(F)=0$, but $\pi_k(F)$ may be non-trivial. The sequence $ \pi_k(E) \xrightarrow{p_*} \pi_k(B) \to 0$ implies that $p_*$ is a [surjection](@entry_id:634659). In summary, if the fiber is $(k-1)$-connected, the projection map $p_*$ induces isomorphisms on homotopy groups up to dimension $k-1$ and a [surjection](@entry_id:634659) in dimension $k$ [@problem_id:1687078]. This principle is a key ingredient in constructing spaces with prescribed homotopy groups, such as in the theory of Postnikov towers.

### Structural Insights from the Long Exact Sequence

Beyond direct computation, the [long exact sequence](@entry_id:153438) reveals deep structural properties of [fibrations](@entry_id:156331).

#### The Role of Sections and Splitting

A fibration $p: E \to B$ admits a **section** if there exists a continuous map $s: B \to E$ such that $p \circ s = \mathrm{id}_B$. The existence of a section has a profound impact on the long exact sequence. On the level of homotopy groups, we have $p_* \circ s_* = \mathrm{id}_{\pi_n(B)}$, which means that $p_*: \pi_n(E) \to \pi_n(B)$ must be a surjective map for all $n$.

By exactness at $\pi_n(B)$, we have $\ker(\partial_n) = \mathrm{im}(p_*)$. Since $p_*$ is surjective, its image is the entire group $\pi_n(B)$. This forces the kernel of $\partial_n$ to be its entire domain, which means the [connecting homomorphism](@entry_id:160713) $\partial_n$ must be the zero map for all $n \ge 1$ [@problem_id:1687083].

When all connecting homomorphisms are trivial, the long exact sequence shatters into a collection of short [exact sequences](@entry_id:151503):
$$
0 \to \pi_n(F) \xrightarrow{i_*} \pi_n(E) \xrightarrow{p_*} \pi_n(B) \to 0
$$
For [abelian groups](@entry_id:145145) (i.e., $n \ge 2$), this means that $\pi_n(E)$ is a [group extension](@entry_id:137693) of $\pi_n(B)$ by $\pi_n(F)$. Furthermore, the map $s_*$ provides a splitting for this sequence, implying that $\pi_n(E) \cong \pi_n(F) \oplus \pi_n(B)$. This is exemplified by the trivial product [fibration](@entry_id:162085) $E = B \times F$, where the homotopy groups simply decompose as a direct sum.

#### Low-Dimensional Exactness and Path Connectivity

The tail end of the long exact sequence provides information about the path components of the spaces. The sequence terminates as:
$$
\dots \to \pi_1(B) \xrightarrow{\partial_1} \pi_0(F) \to \pi_0(E) \to \pi_0(B) \to 0
$$
If we assume that the total space $E$ and base space $B$ are path-connected (as is common in many applications), then $\pi_0(E)$ and $\pi_0(B)$ are trivial (single-point) sets. The sequence then simplifies to:
$$
\pi_1(B) \xrightarrow{\partial_1} \pi_0(F) \to 0
$$
Exactness at $\pi_0(F)$ means that the image of $\partial_1$ is the kernel of the map to the trivial set, which is all of $\pi_0(F)$. Therefore, the connecting map $\partial_1: \pi_1(B) \to \pi_0(F)$ is always surjective when $E$ is path-connected [@problem_id:1687081]. This means that every path-component of the fiber can be "reached" by lifting some loop from the base space.

#### Fibrations with Discrete Fibers

A particularly important class of [fibrations](@entry_id:156331) are [covering spaces](@entry_id:152318). For a covering map $p: E \to B$, the fiber $F$ is a discrete space. As a result, its [higher homotopy groups](@entry_id:159688) are all trivial: $\pi_n(F) = 0$ for all $n \ge 1$. The long exact sequence then contains the segment:
$$
\dots \to \pi_n(F)=0 \to \pi_n(E) \xrightarrow{p_*} \pi_n(B) \to \pi_{n-1}(F)=0 \to \dots
$$
For any $n \ge 2$, this reduces to $0 \to \pi_n(E) \xrightarrow{p_*} \pi_n(B) \to 0$. Exactness dictates that $p_*$ is an [isomorphism](@entry_id:137127). This leads to the remarkable conclusion that for $n \ge 2$, $\pi_n(E) \cong \pi_n(B)$. The [higher homotopy groups](@entry_id:159688) are unable to distinguish a space from its covering spaces. For example, for the [universal cover](@entry_id:151142) $p: S^2 \to \mathbb{RP}^2$, we find $\pi_n(\mathbb{RP}^2) \cong \pi_n(S^2)$ for all $n \ge 2$ [@problem_id:1687031]. All the [topological complexity](@entry_id:261170) of the covering is concentrated in the fundamental groups.

### A Computational Example: The Stiefel Manifold

To conclude, we demonstrate the computational power of the [long exact sequence](@entry_id:153438) with a concrete example. Consider the Stiefel manifold $V_2(\mathbb{R}^5)$, the space of all orthonormal 2-frames ([ordered pairs](@entry_id:269702) of [orthonormal vectors](@entry_id:152061)) in $\mathbb{R}^5$. There is a natural fibration $p: V_2(\mathbb{R}^5) \to S^4$ given by sending a frame $(v_1, v_2)$ to its first vector $v_1$. The base space is the sphere $S^4$. The fiber over a point $v_1 \in S^4$ consists of all [unit vectors](@entry_id:165907) $v_2$ orthogonal to $v_1$. This space of vectors is precisely a 3-sphere, $S^3$. This gives the [fibration](@entry_id:162085):
$$
S^3 \to V_2(\mathbb{R}^5) \to S^4
$$
Our goal is to compute $\pi_3(V_2(\mathbb{R}^5))$. We write down the relevant portion of the long exact sequence:
$$
\dots \to \pi_4(S^4) \xrightarrow{\partial_4} \pi_3(S^3) \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \xrightarrow{p_*} \pi_3(S^4) \to \dots
$$
We use the known homotopy groups of spheres: $\pi_4(S^4) \cong \mathbb{Z}$, $\pi_3(S^3) \cong \mathbb{Z}$, and $\pi_3(S^4) = 0$. Substituting these into the sequence yields:
$$
\mathbb{Z} \xrightarrow{\partial_4} \mathbb{Z} \xrightarrow{i_*} \pi_3(V_2(\mathbb{R}^5)) \to 0
$$
Now, we need information about the [connecting homomorphism](@entry_id:160713) $\partial_4$. It is a known, non-trivial result that for this specific fibration, the map $\partial_4: \mathbb{Z} \to \mathbb{Z}$ is multiplication by 2. Let's accept this fact and proceed [@problem_id:1687052].

By exactness at $\pi_3(V_2(\mathbb{R}^5))$, the image of $i_*$ is equal to the kernel of $p_*$. Since $p_*$ maps to the trivial group, its kernel is its entire domain. Thus, $\mathrm{Im}(i_*) = \pi_3(V_2(\mathbb{R}^5))$. This means $i_*$ is surjective.

By exactness at $\pi_3(S^3)$, the kernel of $i_*$ is equal to the image of $\partial_4$. Since $\partial_4$ is multiplication by 2, its image is the subgroup of even integers, $2\mathbb{Z} \subset \mathbb{Z}$. So, $\ker(i_*) = 2\mathbb{Z}$.

By the [first isomorphism theorem](@entry_id:146795) for groups, the image of a homomorphism is isomorphic to the quotient of its domain by its kernel. Therefore,
$$
\mathrm{Im}(i_*) \cong \mathrm{Domain}(i_*) / \ker(i_*) = \pi_3(S^3) / \ker(i_*) = \mathbb{Z} / 2\mathbb{Z}
$$
Since we found that $\mathrm{Im}(i_*) = \pi_3(V_2(\mathbb{R}^5))$, we conclude:
$$
\pi_3(V_2(\mathbb{R}^5)) \cong \mathbb{Z}_2
$$
The third homotopy group of the Stiefel manifold $V_2(\mathbb{R}^5)$ is the [cyclic group](@entry_id:146728) of order 2. This calculation, which would be formidable by other means, becomes a straightforward algebraic exercise once the [long exact sequence](@entry_id:153438) and its properties are in hand.