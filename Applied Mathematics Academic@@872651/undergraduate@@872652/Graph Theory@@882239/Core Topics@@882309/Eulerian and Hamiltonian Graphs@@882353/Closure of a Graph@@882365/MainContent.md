## Introduction
In the vast landscape of graph theory, understanding the existence of long paths and cycles within a network is a fundamental challenge. The concept of a Hamiltonian cycle—a path that visits every vertex exactly once before returning to the start—is particularly important but notoriously difficult to identify. The **closure of a graph** emerges as a powerful and elegant theoretical tool designed to simplify this problem by systematically adding edges to reveal a graph's latent structural potential.

This article addresses the knowledge gap between a graph's initial state and its potential for Hamiltonicity. It demystifies the [closure operation](@entry_id:747392), providing a clear framework for its use. You will learn the principles that govern how a graph's closure is constructed, explore its most significant application in proving the existence of Hamiltonian cycles via the Bondy-Chvátal theorem, and see how it connects to other core graph properties.

The following chapters will guide you through this concept. First, **"Principles and Mechanisms"** will formally define the [closure operation](@entry_id:747392) and establish its core properties, such as well-definedness and its effect on connectivity. Next, **"Applications and Interdisciplinary Connections"** will demonstrate its practical utility in solving problems related to Hamiltonicity and its relationship with other [graph invariants](@entry_id:262729). Finally, **"Hands-On Practices"** will offer concrete exercises to solidify your understanding of how the [closure operation](@entry_id:747392) behaves in different scenarios.

## Principles and Mechanisms

In the study of graph theory, particularly concerning long paths and cycles, certain operations allow us to augment a graph's structure to reveal its latent properties. One of the most powerful and elegant of these is the concept of a graph's **closure**. This chapter delineates the principles governing the [closure operation](@entry_id:747392), explores its fundamental mechanisms, and establishes its key properties.

### The Closure Operation: Definition and Process

The [closure operation](@entry_id:747392) is an iterative process of edge addition. For a simple graph $G$ with $n$ vertices, we systematically scan for pairs of non-adjacent vertices whose degrees are sufficiently high.

**Definition:** Let $G$ be a [simple graph](@entry_id:275276) on $n$ vertices. The **closure** of $G$, denoted $cl(G)$, is the graph obtained by repeatedly applying the following rule: if $u$ and $v$ are two non-adjacent vertices in the current graph such that the sum of their degrees is at least $n$, add the edge $\{u, v\}$. This process is continued until no more edges can be added.

The condition for adding an edge between non-adjacent vertices $u$ and $v$ is formally expressed as:
$$ \deg(u) + \deg(v) \ge n $$

To fully grasp this iterative procedure, let us consider a concrete example. Suppose we have a graph $G$ on $n=5$ vertices, $V = \{v_1, v_2, v_3, v_4, v_5\}$. The graph's edges are those of a path $P_5$, which are $(v_1, v_2), (v_2, v_3), (v_3, v_4), (v_4, v_5)$, plus an additional edge $(v_1, v_4)$ [@problem_id:1484531].

First, we calculate the initial degrees of all vertices in $G$:
- $\deg(v_1) = 2$ (connected to $v_2, v_4$)
- $\deg(v_2) = 2$ (connected to $v_1, v_3$)
- $\deg(v_3) = 2$ (connected to $v_2, v_4$)
- $\deg(v_4) = 3$ (connected to $v_1, v_3, v_5$)
- $\deg(v_5) = 1$ (connected to $v_4$)

The condition for adding an edge is $\deg(u) + \deg(v) \ge 5$. We check this for all non-adjacent pairs. The non-adjacent pairs are $(v_1,v_3), (v_1,v_5), (v_2,v_4), (v_2,v_5), (v_3,v_5)$.
- $\deg(v_1)+\deg(v_3) = 2+2=4 \lt 5$.
- $\deg(v_1)+\deg(v_5) = 2+1=3 \lt 5$.
- $\deg(v_2)+\deg(v_4) = 2+3=5 \ge 5$. We **add the edge $(v_2, v_4)$**.
- $\deg(v_2)+\deg(v_5) = 2+1=3 \lt 5$.
- $\deg(v_3)+\deg(v_5) = 2+1=3 \lt 5$.

After this first step, we have a new graph, let's call it $G_1$, which is $G$ plus the edge $(v_2, v_4)$. The degrees are updated: $\deg_{G_1}(v_2)$ is now $3$ and $\deg_{G_1}(v_4)$ is now $4$.
- $\deg_{G_1}(v_1) = 2$
- $\deg_{G_1}(v_2) = 3$
- $\deg_{G_1}(v_3) = 2$
- $\deg_{G_1}(v_4) = 4$
- $\deg_{G_1}(v_5) = 1$

Now we repeat the process on $G_1$. The remaining non-adjacent pairs are $(v_1,v_3), (v_1,v_5), (v_2,v_5), (v_3,v_5)$.
- $(v_1,v_3)$: $\deg_{G_1}(v_1)+\deg_{G_1}(v_3) = 2+2 = 4 \lt 5$.
- $(v_1,v_5)$: $\deg_{G_1}(v_1)+\deg_{G_1}(v_5) = 2+1 = 3 \lt 5$.
- $(v_2,v_5)$: $\deg_{G_1}(v_2)+\deg_{G_1}(v_5) = 3+1 = 4 \lt 5$.
- $(v_3,v_5)$: $\deg_{G_1}(v_3)+\deg_{G_1}(v_5) = 2+1 = 3 \lt 5$.

No other pair satisfies the condition. The process terminates. The final graph, $cl(G)$, contains the original 5 edges plus the newly added edge $(v_2, v_4)$, for a total of 6 edges.

### Fundamental Properties of Closure

The [closure operation](@entry_id:747392) possesses several foundational properties that make it a reliable and powerful tool.

#### Well-Definedness

A crucial question arises from the iterative definition: does the final closure graph depend on the order in which we add the qualifying edges? If multiple pairs satisfy the degree-sum condition simultaneously, which one should we choose first? Fortunately, the result is always the same. The closure of a graph is **well-defined**.

The justification for this uniqueness lies in the **monotonicity of the degree-sum condition** [@problem_id:1484559]. Suppose we have a graph $H$ and two non-adjacent vertices $u, v$ such that $\deg_H(u) + \deg_H(v) \ge n$. If we form a supergraph $H'$ by adding some *other* edge to $H$, the degrees of $u$ and $v$ in $H'$ can only increase or stay the same: $\deg_{H'}(u) \ge \deg_H(u)$ and $\deg_{H'}(v) \ge \deg_H(v)$. Consequently, the degree-sum condition will still hold: $\deg_{H'}(u) + \deg_{H'}(v) \ge n$.

This means that an edge, once it becomes eligible for addition, remains eligible regardless of which other eligible edges are added. Any sequence of additions that continues until no more edges can be added (a maximal sequence) must therefore result in the same final set of edges. Any edge that could have been added in one sequence must eventually have its condition met and be added in any other maximal sequence. This guarantees that $cl(G)$ is a unique graph for any given $G$.

#### Termination and Closed Graphs

The closure process is guaranteed to terminate. A simple graph on $n$ vertices can have at most $\binom{n}{2}$ edges. Each step of the closure process adds at least one edge, so the process must halt in a finite number of steps.

The process stops when the graph is **closed**. A graph $H$ is called closed if $cl(H) = H$. This is equivalent to stating that for every pair of non-adjacent vertices $u, v$ in $H$, their degree sum is strictly less than $n$:
$$ \deg_H(u) + \deg_H(v) \lt n $$

A complete graph $K_n$ is trivially closed because it has no non-adjacent pairs. However, many non-complete graphs are also closed [@problem_id:1484533]. For instance, on $n=8$ vertices:
- The [cycle graph](@entry_id:273723) $C_8$ is closed. Every vertex has degree 2. For any non-adjacent pair $\{u, v\}$, $\deg(u) + \deg(v) = 2+2=4 \lt 8$.
- A graph consisting of two disjoint copies of $K_4$ is also closed. Every vertex has degree 3. The only non-adjacent pairs are vertices from different components. For any such pair, $\deg(u) + \deg(v) = 3+3=6 \lt 8$.

In contrast, the complete bipartite graph $K_{4,4}$ on $n=8$ vertices is *not* closed. Every vertex has degree 4. Any two vertices in the same partition set are non-adjacent, and their degree sum is $4+4=8 \ge 8$. The closure of $K_{4,4}$ would therefore involve adding all edges within each partition, ultimately resulting in the complete graph $K_8$.

### The Dynamics of the Closure Process

The iterative nature of closure can lead to cascading edge additions. The addition of a single edge increases the degrees of its two endpoints, which may, in turn, cause other pairs of vertices to satisfy the degree-sum condition.

A fascinating question is to characterize graphs for which the [closure operation](@entry_id:747392) adds exactly one edge [@problem_id:1489493]. One might naively assume this happens if and only if exactly one pair of non-adjacent vertices $\{x, y\}$ initially satisfies $\deg_G(x) + \deg_G(y) \ge n$. This condition is necessary, but not sufficient.

Consider what happens after we add the edge $\{x, y\}$. The degrees of $x$ and $y$ each increase by 1. Let the new graph be $G' = G + \{x, y\}$. Now, consider another vertex $z$ that was not adjacent to $x$ in $G$. If it happened that $\deg_G(x) + \deg_G(z) = n-1$, then in $G'$ the new degree sum would be:
$$ \deg_{G'}(x) + \deg_{G'}(z) = (\deg_G(x)+1) + \deg_G(z) = (n-1)+1=n $$
This would trigger the addition of the edge $\{x, z\}$, contradicting the requirement that only one edge is added.

Therefore, for exactly one edge $\{x, y\}$ to be added, two conditions must be met:
1.  There is a unique non-adjacent pair $\{x, y\}$ in $G$ with $\deg_G(x) + \deg_G(y) \ge n$.
2.  For any other vertex $z \notin \{x, y\}$, if $z$ is not adjacent to $x$, then $\deg_G(x) + \deg_G(z) \le n-2$. Similarly, if $z$ is not adjacent to $y$, then $\deg_G(y) + \deg_G(z) \le n-2$.

This more stringent condition ensures that the first and only edge addition does not trigger a cascade of further additions.

### Closure and Structural Graph Properties

The [closure operation](@entry_id:747392) can alter several fundamental properties of a graph. Since it only ever adds edges, it tends to make a graph "more connected."

#### Connectivity

A key structural property is whether a graph is connected. The [closure operation](@entry_id:747392) preserves disconnectedness. If a graph $G$ is disconnected, its closure $cl(G)$ must also be disconnected [@problem_id:1484545].

To see why, let $G$ have at least two [connected components](@entry_id:141881). Let $u$ be a vertex in component $C_1$ and $v$ be a vertex in component $C_2$. The vertices $u$ and $v$ are non-adjacent. The degree of $u$ is at most $|V(C_1)| - 1$, and the degree of $v$ is at most $|V(C_2)| - 1$. The sum of their degrees is therefore:
$$ \deg(u) + \deg(v) \le (|V(C_1)| - 1) + (|V(C_2)| - 1) $$
Since $|V(C_1)| + |V(C_2)| \le n$, the total number of vertices, we have:
$$ \deg(u) + \deg(v) \le n - 2 \lt n $$
The degree-sum condition is never met for any pair of vertices in different components. The closure process can add edges *within* components, but it can never add an edge *between* them. Thus, the components remain separate in $cl(G)$.

#### Diameter

The **diameter** of a graph is the maximum [shortest-path distance](@entry_id:754797) between any pair of vertices. Adding an edge to a graph can never increase the distance between any two vertices; it can only decrease it or keep it the same. Consequently, the [diameter of a graph](@entry_id:271355)'s closure is always less than or equal to the diameter of the original graph: $D(cl(G)) \le D(G)$.

The diameter can, in fact, strictly decrease [@problem_id:1489507]. Consider the cycle graph $C_4$ on $n=4$ vertices. Every vertex has degree 2. The diameter of $C_4$ is 2 (the distance between opposite vertices). For any pair of non-adjacent vertices, their degree sum is $2+2=4 \ge n$. Thus, the [closure operation](@entry_id:747392) adds both diagonals, transforming $C_4$ into the complete graph $K_4$. The diameter of $K_4$ is 1. In this case, $D(cl(C_4)) = 1 \lt 2 = D(C_4)$.

### Monotonicity of the Closure Operator

The closure operator itself exhibits a crucial monotonic property with respect to the graph's edge set. This property is key to understanding its behavior and interaction with other operations.

Let $G_1$ and $G_2$ be two graphs on the same vertex set $V$. If $G_1$ is a subgraph of $G_2$ (i.e., $E(G_1) \subseteq E(G_2)$), then $cl(G_1)$ is a subgraph of $cl(G_2)$ (i.e., $E(cl(G_1)) \subseteq E(cl(G_2))$).

We can demonstrate this by considering the process step-by-step. Any edge added during the closure of $G_1$ is due to a pair $\{u,v\}$ satisfying $\deg_{G_1'}(u) + \deg_{G_1'}(v) \ge n$ for some intermediate graph $G_1'$. Because $G_1$ is a subgraph of $G_2$, any intermediate graph $G_1'$ will be a [subgraph](@entry_id:273342) of the corresponding intermediate graph $G_2'$, and thus the degree-sum condition will also be met for that pair in the context of closing $G_2$. This ensures that every edge added to form $cl(G_1)$ will also be added to form $cl(G_2)$.

This principle has direct consequences:
- **Adding an edge:** If we take a graph $G$ and add an edge $e$ to form $G' = G+e$, then $cl(G)$ must be a subgraph of $cl(G')$ [@problem_id:1489481].
- **Removing an edge:** Conversely, if we take a graph $G$ and remove an edge $e$ to form $G' = G-e$, then $cl(G')$ must be a subgraph of $cl(G)$ [@problem_id:1489496].

This monotonic behavior allows us to establish more complex identities. For instance, consider the interaction between closure and the union of two graphs, $G_1$ and $G_2$, on the same vertex set [@problem_id:1489471]. Because $G_1 \subseteq G_1 \cup G_2$, monotonicity implies $cl(G_1) \subseteq cl(G_1 \cup G_2)$. Similarly, $cl(G_2) \subseteq cl(G_1 \cup G_2)$. Together, this means $cl(G_1) \cup cl(G_2) \subseteq cl(G_1 \cup G_2)$. Applying the closure operator to both sides and using its [idempotence](@entry_id:151470) ($cl(cl(H))=cl(H)$) leads to the elegant identity:
$$ cl(G_1 \cup G_2) = cl(cl(G_1) \cup cl(G_2)) $$
Note that the simpler relation $cl(G_1 \cup G_2) = cl(G_1) \cup cl(G_2)$ is not generally true. The union operation can create new degree synergies that allow for edge additions in $cl(G_1 \cup G_2)$ that would not have occurred in either $cl(G_1)$ or $cl(G_2)$ alone.

### Closure and Graph Complement

Finally, it is instructive to investigate whether the [closure operation](@entry_id:747392) commutes with other common [graph operations](@entry_id:263840), such as the complement. The **complement** of a graph $G$, denoted $\overline{G}$, is the graph on the same vertex set where two vertices are adjacent if and only if they are not adjacent in $G$. Does $cl(\overline{G}) = \overline{cl(G)}$ hold in general?

Let's test this with a small example [@problem_id:1489468]. Let $G$ be a graph on $V=\{v_1, v_2, v_3, v_4, v_5\}$ with edges $(v_1, v_2)$ and $(v_2, v_3)$. Here $n=5$.
-   **To find $\overline{cl(G)}$:**
    -   First, find $cl(G)$. The degrees in $G$ are $\deg(v_1)=1, \deg(v_2)=2, \deg(v_3)=1, \deg(v_4)=0, \deg(v_5)=0$. The maximum degree sum for any non-adjacent pair is $\deg(v_2)+\deg(v_1) = 2+1=3$, which is less than $n=5$. No edges are added. Thus, $cl(G) = G$.
    -   Now, we take the complement: $\overline{cl(G)} = \overline{G}$. This graph contains all edges except $(v_1, v_2)$ and $(v_2, v_3)$.
-   **To find $cl(\overline{G})$:**
    -   First, find $\overline{G}$. The degrees in $\overline{G}$ are given by $\deg_{\overline{G}}(v) = n-1-\deg_G(v)$.
    $\deg_{\overline{G}}(v_1)=4-1=3$, $\deg_{\overline{G}}(v_2)=4-2=2$, $\deg_{\overline{G}}(v_3)=4-1=3$, $\deg_{\overline{G}}(v_4)=4-0=4$, $\deg_{\overline{G}}(v_5)=4-0=4$.
    -   The non-adjacent pairs in $\overline{G}$ are precisely the edges of $G$: $(v_1, v_2)$ and $(v_2, v_3)$.
    -   For $(v_1, v_2)$: $\deg_{\overline{G}}(v_1) + \deg_{\overline{G}}(v_2) = 3+2=5 \ge 5$. We must add this edge.
    -   For $(v_2, v_3)$: $\deg_{\overline{G}}(v_2) + \deg_{\overline{G}}(v_3) = 2+3=5 \ge 5$. We must add this edge.
    -   Adding these two edges makes the graph complete. Thus, $cl(\overline{G}) = K_5$.

In this case, $\overline{cl(G)} = \overline{G}$ (which is not complete), while $cl(\overline{G}) = K_5$. The two are not equal. This demonstrates that the closure and complement operations do not commute. Such investigations are crucial for developing a precise understanding of an operator's scope and limits.