## Introduction
The search for Hamiltonian cycles—paths that visit every vertex in a graph exactly once before returning to the start—is a classic and notoriously difficult problem in graph theory. While determining their existence is often computationally intensive, the Bondy-Chvátal theorem provides an elegant theoretical framework to simplify this challenge. It achieves this by introducing the concept of a graph's closure, a denser supergraph that preserves the original graph's Hamiltonicity. This article delves into this powerful theorem and its applications. In the following chapters, you will first master the foundational concepts in "Principles and Mechanisms," where we define the graph [closure operation](@entry_id:747392) and its properties. Next, "Applications and Interdisciplinary Connections" will demonstrate the theorem's utility in solving problems and its relationship with other graph-theoretic concepts. Finally, "Hands-On Practices" will offer opportunities to solidify your understanding by applying these techniques to concrete examples.

## Principles and Mechanisms

The study of Hamiltonian cycles, a cornerstone of graph theory, often involves navigating problems of immense computational complexity. The Bondy-Chvátal theorem offers a powerful theoretical lens through which to simplify these problems. It achieves this by introducing the concept of a graph's **closure**, a related but structurally denser graph. This chapter will rigorously define the [closure operation](@entry_id:747392), explore its fundamental properties and limitations, and detail its application via the Bondy-Chvátal theorem to determine the existence of Hamiltonian cycles.

### The Graph Closure Operation

The central mechanism of the Bondy-Chvátal theorem is the [graph closure](@entry_id:275076). For a [simple graph](@entry_id:275276) $G$ with $n$ vertices, its **closure**, denoted $cl(G)$, is a supergraph of $G$ constructed through an iterative process of edge addition.

**Definition: Graph Closure.** Let $G$ be a simple graph with $n$ vertices. The closure $cl(G)$ is the graph obtained by repeatedly adding an edge between any pair of non-adjacent vertices $u$ and $v$ for which the sum of their degrees is at least $n$. That is, if $\{u, v\}$ is not an edge in the current graph and $\deg(u) + \deg(v) \ge n$, the edge $\{u, v\}$ is added. This process continues until no more edges can be added.

The process is inherently iterative. The addition of one edge increases the degrees of two vertices, which may in turn cause other pairs of vertices to satisfy the degree-sum condition. Let us illustrate this with a concrete example.

Consider a graph $G$ with $n=5$ vertices, $V = \{v_1, v_2, v_3, v_4, v_5\}$, whose edge set consists of a path $(v_1, v_2, v_3, v_4, v_5)$ plus an additional edge $(v_1, v_4)$ [@problem_id:1484531]. The initial degrees are:
$\deg(v_1) = 2$, $\deg(v_2) = 2$, $\deg(v_3) = 2$, $\deg(v_4) = 3$, and $\deg(v_5) = 1$.

The condition for adding an edge is $\deg(u) + \deg(v) \ge 5$. We examine the non-adjacent pairs:
- $(v_1, v_3)$: $\deg(v_1) + \deg(v_3) = 2 + 2 = 4  5$. No edge is added.
- $(v_1, v_5)$: $\deg(v_1) + \deg(v_5) = 2 + 1 = 3  5$. No edge is added.
- $(v_2, v_4)$: $\deg(v_2) + \deg(v_4) = 2 + 3 = 5 \ge 5$. We must add the edge $(v_2, v_4)$.
- $(v_2, v_5)$: $\deg(v_2) + \deg(v_5) = 2 + 1 = 3  5$. No edge is added.
- $(v_3, v_5)$: $\deg(v_3) + \deg(v_5) = 2 + 1 = 3  5$. No edge is added.

After this first step, we have a new graph, let's call it $G_1$, which includes the new edge $(v_2, v_4)$. The degrees of $v_2$ and $v_4$ are now updated: $\deg_{G_1}(v_2) = 3$ and $\deg_{G_1}(v_4) = 4$. The other degrees remain unchanged. We must now repeat the process on $G_1$. The remaining non-adjacent pairs are $(v_1, v_3)$, $(v_1, v_5)$, $(v_2, v_5)$, and $(v_3, v_5)$. Let's re-check their degree sums in $G_1$:
- $(v_1, v_3)$: $\deg_{G_1}(v_1) + \deg_{G_1}(v_3) = 2 + 2 = 4  5$.
- $(v_1, v_5)$: $\deg_{G_1}(v_1) + \deg_{G_1}(v_5) = 2 + 1 = 3  5$.
- $(v_2, v_5)$: $\deg_{G_1}(v_2) + \deg_{G_1}(v_5) = 3 + 1 = 4  5$.
- $(v_3, v_5)$: $\deg_{G_1}(v_3) + \deg_{G_1}(v_5) = 2 + 1 = 3  5$.

At this stage, no pair of non-adjacent vertices satisfies the condition. The process terminates. The final graph, $cl(G)$, is $G_1$, which has one more edge than the original graph $G$.

### Fundamental Properties of Closure

For the [closure operation](@entry_id:747392) to be a reliable analytical tool, it must possess certain fundamental properties. We will now establish its uniqueness, explore its dynamic nature, and identify conditions under which the operation results in no change.

#### Well-Definedness

A potential concern with the iterative definition is whether the final graph depends on the order in which we choose to add eligible edges. If multiple pairs satisfy the degree-sum condition simultaneously, does our choice affect the outcome? The answer is no; the [closure of a graph](@entry_id:269136) is unique.

The reason for this is the **[monotonicity](@entry_id:143760)** of the degree-sum condition [@problem_id:1484559]. Adding an edge to a graph can never decrease the degree of any vertex. Therefore, if the condition $\deg(u) + \deg(v) \ge n$ is met for a non-adjacent pair $\{u, v\}$, it will continue to be met in any supergraph formed by adding other edges.

To formalize this, let $S_1$ and $S_2$ be two different maximal sequences of edge additions starting from graph $G$, resulting in final graphs $cl_1(G)$ and $cl_2(G)$. Consider any edge $e = \{u, v\}$ that was added in sequence $S_1$. This means that at some point during that sequence, in a graph $G'$, the condition $\deg_{G'}(u) + \deg_{G'}(v) \ge n$ was met. Since $cl_2(G)$ is a supergraph of $G'$, the degrees in $cl_2(G)$ are at least as high as in $G'$. Thus, $\deg_{cl_2(G)}(u) + \deg_{cl_2(G)}(v) \ge n$. If $e$ were not in $cl_2(G)$, it would be an eligible edge to add, which contradicts the fact that $S_2$ was a maximal sequence. Therefore, $e$ must be in $cl_2(G)$. This shows that every edge added in $S_1$ must also be in $cl_2(G)$, so $cl_1(G)$ is a [subgraph](@entry_id:273342) of $cl_2(G)$. By a symmetric argument, $cl_2(G)$ is a [subgraph](@entry_id:273342) of $cl_1(G)$. Consequently, the two graphs must be identical. The closure $cl(G)$ is well-defined.

#### The Iterative Dynamic and Self-Closed Graphs

The iterative nature of the closure process is central to its power. An edge that does not initially qualify for inclusion may do so later as other edges are added and degrees increase. Consider a graph on $n=10$ vertices with two non-adjacent vertices $u$ and $v$ having initial degrees $\deg(u)=4$ and $\deg(v)=5$ [@problem_id:1484560]. Their initial degree sum is $4+5=9$, which is less than $10$, so the edge $\{u, v\}$ is not added at the outset. However, suppose there exists another vertex $z$, not adjacent to $u$, with $\deg(z) \ge 6$. Then $\deg(u) + \deg(z) \ge 4+6 = 10$, so the edge $\{u, z\}$ is added. This action increases the degree of $u$ to $\deg'(u)=5$. Now, re-evaluating the pair $\{u,v\}$, we find their new degree sum is $\deg'(u) + \deg(v) = 5+5=10$. The condition is now met, and the edge $\{u, v\}$ is added to the closure. The final state of a pair of vertices can depend on the global structure of the graph.

Conversely, it is possible for the closure process to terminate immediately. This occurs if, in the original graph $G$, no pair of non-adjacent vertices satisfies the degree-sum condition. In such a case, the closure of $G$ is simply $G$ itself, i.e., $cl(G) = G$. A graph with this property is called **self-closed**. For instance, if a graph on $n=10$ vertices is constructed such that for every pair of non-adjacent vertices $u$ and $v$, their degree sum is exactly $n-1=9$, then no edge can ever be added [@problem_id:1484515]. The [closure operation](@entry_id:747392) terminates at the start, and $cl(G)=G$.

### The Bondy-Chvátal Theorem and Hamiltonicity

The primary motivation for defining the [graph closure](@entry_id:275076) is its profound connection to Hamiltonian cycles, articulated by the Bondy-Chvátal theorem.

**Theorem (Bondy-Chvátal, 1976):** A simple graph $G$ with $n \ge 3$ vertices has a Hamiltonian cycle if and only if its closure, $cl(G)$, has a Hamiltonian cycle.

This theorem is remarkable because it allows us to transfer a difficult question about a graph $G$ to what is often an easier question about a denser, more structured graph $cl(G)$. The most powerful and direct application of this theorem arises when the closure is a complete graph. A **complete graph**, denoted $K_n$, is a graph where every pair of distinct vertices is connected by an edge. For any $n \ge 3$, the graph $K_n$ is trivially Hamiltonian. This leads to a powerful corollary.

**Corollary:** If the [closure of a graph](@entry_id:269136) $G$ with $n \ge 3$ vertices is the complete graph $K_n$, then $G$ is Hamiltonian.

Let's see this principle in action. Consider a graph $G$ on $n=6$ vertices with edges $E = \{(v_1, v_2), (v_1, v_5), (v_1, v_6), (v_2, v_5), (v_2, v_6), (v_3, v_4), (v_3, v_5), (v_3, v_6), (v_4, v_5), (v_4, v_6)\}$ [@problem_id:1457307]. The degrees are $\deg(v_1) = \deg(v_2) = \deg(v_3) = \deg(v_4) = 3$ and $\deg(v_5) = \deg(v_6) = 4$. The condition for edge addition is $\deg(u) + \deg(v) \ge 6$. The non-adjacent pairs are $\{v_1, v_3\}$, $\{v_1, v_4\}$, $\{v_2, v_3\}$, $\{v_2, v_4\}$, and $\{v_5, v_6\}$. Their degree sums are:
- $\deg(v_1) + \deg(v_3) = 3 + 3 = 6$
- $\deg(v_1) + \deg(v_4) = 3 + 3 = 6$
- $\deg(v_2) + \deg(v_3) = 3 + 3 = 6$
- $\deg(v_2) + \deg(v_4) = 3 + 3 = 6$
- $\deg(v_5) + \deg(v_6) = 4 + 4 = 8$

All these sums are at least $6$. Therefore, all five missing edges are added in the first step of the closure process. The resulting graph contains every possible edge, so $cl(G) = K_6$. Since $K_6$ is Hamiltonian, we can definitively conclude that the original graph $G$ is also Hamiltonian.

#### The Inconclusive Case

A common misconception is that the converse of the corollary holds: that if $G$ is Hamiltonian, its closure must be complete. This is false. If we compute the [closure of a graph](@entry_id:269136) $G$ and find that $cl(G)$ is *not* a complete graph, we cannot conclude that $G$ is non-Hamiltonian [@problem_id:1484519]. The Bondy-Chvátal theorem simply states that $G$ is Hamiltonian if and only if $cl(G)$ is Hamiltonian. Determining whether a non-complete graph $cl(G)$ is Hamiltonian can still be a difficult problem.

For example, consider the cycle graph $C_{10}$ on $n=10$ vertices. This graph is, by definition, Hamiltonian. Every vertex in $C_{10}$ has degree 2. For any pair of non-adjacent vertices $u$ and $v$, their degree sum is $\deg(u) + \deg(v) = 2+2=4$. Since $4  10$, the condition for adding an edge is never met. Thus, $cl(C_{10}) = C_{10}$. The closure is not $K_{10}$, yet the original graph is Hamiltonian.

This leads to an important point about the theorem's utility. When a graph is its own closure ($cl(G)=G$) but is not complete, the Bondy-Chvátal theorem becomes a [tautology](@entry_id:143929): "$G$ is Hamiltonian if and only if $G$ is Hamiltonian" [@problem_id:1484536]. This provides no new information and the theorem is, in this sense, inconclusive for proving or disproving Hamiltonicity. Both Hamiltonian graphs (like $C_n$ for $n \ge 5$) and non-Hamiltonian graphs (like a [star graph](@entry_id:271558) $K_{1, n-1}$ for $n \ge 4$) can be self-closed without being complete.

### Structural Obstructions to Complete Closures

The closure process, while powerful, is constrained by the initial structure of the graph. Certain structural features can act as permanent barriers, preventing the closure from ever becoming complete.

#### Connectivity

The most fundamental obstruction is a lack of connectivity. The [closure operation](@entry_id:747392) can never connect a [disconnected graph](@entry_id:266696). To see why, let $G$ be a [disconnected graph](@entry_id:266696) on $n$ vertices. Let $u$ and $v$ be two vertices from different connected components, say $C_u$ and $C_v$. Any neighbor of $u$ must lie within $C_u$, and any neighbor of $v$ must lie within $C_v$. Therefore, the maximum possible degree of $u$ is $|V(C_u)| - 1$, and the maximum degree of $v$ is $|V(C_v)| - 1$. This property is maintained throughout the closure process, as edges are only added within existing components, never between them. The sum of their degrees at any stage will thus be bounded:
$\deg(u) + \deg(v) \le (|V(C_u)| - 1) + (|V(C_v)| - 1) = |V(C_u)| + |V(C_v)| - 2$.

Since $C_u$ and $C_v$ are distinct components, $|V(C_u)| + |V(C_v)| \le n$. This gives $\deg(u) + \deg(v) \le n-2$, which is strictly less than $n$. The condition to add an edge between $u$ and $v$ is never met [@problem_id:1484545]. Consequently, if a graph is disconnected, its closure remains disconnected and can never be $K_n$.

#### Cut-Vertices

A more subtle obstruction is the presence of a **[cut-vertex](@entry_id:260941)**—a vertex whose removal increases the number of connected components. If a [connected graph](@entry_id:261731) $G$ on $n \ge 3$ vertices has a [cut-vertex](@entry_id:260941), its closure can never be the complete graph $K_n$ [@problem_id:1484561].

The reasoning is a refinement of the connectivity argument. Let $v$ be a [cut-vertex](@entry_id:260941) in $G$. The graph $G-v$ (the graph with $v$ removed) has at least two [connected components](@entry_id:141881). Let $u$ and $w$ be vertices from two different components of $G-v$, say $C_u$ and $C_w$. In the original graph $G$, $u$ and $w$ are non-adjacent (otherwise $G-v$ would not be disconnected). Any neighbor of $u$ in $G$ must either be in $C_u$ or be the vertex $v$ itself. Similarly, any neighbor of $w$ is in $C_w$ or is $v$. The closure process cannot create an edge between a vertex in $C_u$ and a vertex in $C_w$ for the same reason it cannot bridge disconnected components. The maximum degree of $u$ is bounded by the number of other vertices in its "region": $\deg(u) \le |V(C_u)|$. Likewise, $\deg(w) \le |V(C_w)|$. The sum of their degrees is thus bounded:
$\deg(u) + \deg(w) \le |V(C_u)| + |V(C_w)|$.

Since $C_u$ and $C_w$ are disjoint components in the graph $G-v$, the total number of vertices they contain is at most $n-1$. So, $|V(C_u)| + |V(C_w)| \le n-1$. This means $\deg(u) + \deg(w) \le n-1$, and the edge $\{u, w\}$ can never be added. Therefore, $cl(G)$ cannot be $K_n$.

### A Sufficient Condition from Degree Sequences

While computing the closure can be laborious, a related theorem by Václav Chvátal provides a sufficient condition for Hamiltonicity based solely on a graph's degree sequence. This condition is, in fact, sufficient to guarantee that the graph's closure is complete.

**Theorem (Chvátal, 1972):** Let $G$ be a simple graph with $n \ge 3$ vertices and a degree sequence $d_1 \le d_2 \le \dots \le d_n$. If for every integer $k$ with $1 \le k  n/2$, the implication $d_k \le k \implies d_{n-k} \ge n-k$ holds, then $G$ is Hamiltonian.

If a graph's degree sequence satisfies this condition, it can be proven that its closure is $K_n$. By the Bondy-Chvátal theorem, this implies the graph is Hamiltonian. This provides a powerful shortcut, bypassing the need to construct the closure explicitly.

However, it is crucial to remember this is a *sufficient* condition, not a necessary one. If the condition fails for some $k$, the test is inconclusive. The graph might still be Hamiltonian.

Consider a graph on $n=6$ vertices with the [degree sequence](@entry_id:267850) $(2, 2, 3, 3, 4, 4)$ [@problem_id:1484549]. We must check the condition for $k  n/2$, so for $k=1$ and $k=2$.
- For $k=1$: We check if $d_1 \le 1 \implies d_5 \ge 5$. The degree is $d_1=2$, so the antecedent $2 \le 1$ is false. The implication is therefore true.
- For $k=2$: We check if $d_2 \le 2 \implies d_4 \ge 4$. The degree is $d_2=2$, so the antecedent $2 \le 2$ is true. We must therefore check the consequent. The degree is $d_4=3$. The consequent $3 \ge 4$ is false.

Since the implication fails for $k=2$, Chvátal's condition is not met. This does not mean the graph is non-Hamiltonian. It only means this particular test fails to prove it. The question of its Hamiltonicity remains open without further analysis, such as explicitly computing its closure.