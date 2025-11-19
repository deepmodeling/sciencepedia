## Introduction
In the study of networks, closed pathways or cycles represent everything from feedback loops in systems to redundancies in infrastructure. Understanding the nature of these cycles is fundamental to analyzing a graph's structure. However, simply knowing that cycles exist is not enough; we need precise tools to quantify their characteristics. This article addresses this need by focusing on two key metrics that define the extremes of a graph's cyclic nature: girth and circumference. In the following chapters, you will gain a comprehensive understanding of these concepts. "Principles and Mechanisms" will establish the formal definitions of girth and circumference, explore their relationship with core graph properties like bipartiteness and [vertex degree](@entry_id:264944), and analyze how they change under [graph operations](@entry_id:263840). "Applications and Interdisciplinary Connections" will demonstrate their significance in [extremal graph theory](@entry_id:275134), network design, and the analysis of specialized graph families. Finally, "Hands-On Practices" will allow you to apply your knowledge to solve concrete problems on well-known graph structures. Let's begin by delving into the principles that govern these fundamental cycle parameters.

## Principles and Mechanisms

While the previous chapter introduced the fundamental concepts of graph theory, we now turn our attention to one of the most elementary yet profound structural features of a graph: the cycle. Cycles represent feedback loops, redundancies, and closed pathways within a network structure. Quantifying their presence and nature is crucial for understanding graph properties. This chapter introduces two key parameters that capture the extremes of a graph's [cycle structure](@entry_id:147026): the **girth** and the **circumference**.

### Defining the Extremes of Cycle Length

A **cycle** in a [simple graph](@entry_id:275276) is a path that begins and ends at the same vertex, containing at least three vertices, and which does not repeat any other vertices or edges. The **length** of a a cycle is the number of edges it comprises. The set of all cycles within a graph $G$ provides a signature of its connectivity. We are often interested in the shortest and longest possible cycles a graph can support.

The **girth** of a graph $G$, denoted $g(G)$, is the length of a [shortest cycle](@entry_id:276378) contained in $G$. Formally, if $\mathcal{C}(G)$ is the set of all cycles in $G$, then:
$$
g(G) = \min \{ \text{length}(C) \mid C \in \mathcal{C}(G) \}
$$
In a simple graph, a cycle requires at least three vertices and three edges to form (e.g., a triangle), so for any graph containing a cycle, $g(G) \ge 3$.

What if a graph has no cycles? Such a graph is called **acyclic**. Common examples include trees (if connected) and forests (if disconnected). In this case, the set $\mathcal{C}(G)$ is empty, and the minimum is taken over an [empty set](@entry_id:261946). By convention in mathematics, the minimum of an empty set of real numbers is defined as positive infinity. Therefore, the [girth](@entry_id:263239) of any [acyclic graph](@entry_id:272495) is taken to be infinity [@problem_id:1506869]. This convention is useful because it cleanly separates graphs with cycles (finite girth) from those without (infinite [girth](@entry_id:263239)).

On the other end of the spectrum lies the **circumference**. The circumference of a graph $G$, denoted $c(G)$, is the length of a longest simple cycle in $G$.
$$
c(G) = \max \{ \text{length}(C) \mid C \in \mathcal{C}(G) \}
$$
By a similar but distinct convention, if a graph is acyclic, its circumference is defined to be 0 [@problem_id:1506847]. This reflects the absence of any cyclic structure to measure.

### Calculating Girth and Circumference: First Examples

To solidify these definitions, let us consider a few illustrative examples.

Imagine a graph $G$ that is not connected and is composed of several distinct components. The set of all cycles in $G$ is simply the union of the sets of cycles from each component. Consequently, the [girth](@entry_id:263239) of $G$ is the minimum of the girths of its components, and its circumference is the maximum of their circumferences. For instance, consider a graph with 11 vertices where every vertex has degree 2, and the graph consists of two [connected components](@entry_id:141881), one with 4 vertices and one with 7. A connected graph where every vertex has degree 2 must be a cycle. Thus, the graph is the disjoint union of a 4-cycle ($C_4$) and a 7-cycle ($C_7$). The only cycles present are of length 4 and 7. The shortest is the $C_4$ and the longest is the $C_7$. Therefore, $g(G) = 4$ and $c(G) = 7$ [@problem_id:1506861].

In some graphs, the girth and circumference can coincide. A simple yet important case is the **cycle graph**, $C_n$, which consists of a single cycle passing through $n$ vertices. By its very structure, the only cycle in $C_n$ has length $n$. Therefore, for this graph, $g(C_n) = c(C_n) = n$. This property is so distinctive that it uniquely identifies the graph: any [simple graph](@entry_id:275276) on $n$ vertices whose girth is $n$ must be the [cycle graph](@entry_id:273723) $C_n$ [@problem_id:1506849]. Any additional edge (a "chord") would necessarily create a shorter cycle, reducing the [girth](@entry_id:263239).

More commonly, a graph will contain cycles of various lengths, leading to a gap between its girth and circumference. For example, can a graph have a girth of 4 while also containing a 5-cycle? A [girth](@entry_id:263239) of 4 means the graph contains at least one 4-cycle and, crucially, no 3-cycles (triangles). If we attempt to construct such a graph on 5 vertices, the presence of a 5-cycle (which would be a Hamiltonian cycle) means any additional edge would create a cycle of length 3 or 4. To create a 4-cycle without creating a 3-cycle, we find that 5 vertices are insufficient. However, a graph with 6 vertices can satisfy these conditions. For example, take a 5-cycle $v_1-v_2-v_3-v_4-v_5-v_1$ and add a new vertex $u$ connected to $v_1$ and $v_3$. This introduces the 4-cycle $u-v_1-v_2-v_3-u$. Since $v_1$ and $v_3$ are not adjacent, no triangle is formed, and the girth is indeed 4. This construction confirms that the minimum number of vertices for such a graph is 6 [@problem_id:1506854].

### Structural Properties and Their Influence on Cycles

The [cycle structure](@entry_id:147026) of a graph is not arbitrary; it is deeply tied to other fundamental properties like vertex degrees and bipartiteness.

#### Minimum Degree and Cycle Existence

A foundational question is: what is the simplest condition that guarantees a graph must contain a cycle? The answer lies in the [minimum degree](@entry_id:273557) of the graph, $\delta(G)$. If $\delta(G) \ge 2$, meaning every vertex is connected to at least two other vertices, a cycle is guaranteed to exist.

We can prove this with an elegant argument involving a longest path in the graph. Let $P = (v_0, v_1, \ldots, v_L)$ be a path of maximum possible length in $G$. Consider one of its endpoints, say $v_L$. All neighbors of $v_L$ must lie on the path $P$. If $v_L$ had a neighbor $w$ not on $P$, then the path $(v_0, \ldots, v_L, w)$ would be longer than $P$, contradicting our assumption that $P$ is a longest path. Since $\deg(v_L) \ge \delta(G) \ge 2$, $v_L$ has at least two neighbors. All of these neighbors are in $\{v_0, v_1, \ldots, v_L\}$. One of these neighbors is $v_{L-1}$, its predecessor on the path. Therefore, $v_L$ must have at least $\delta(G) - 1$ other neighbors on the path. For $\delta(G) \ge 2$, this means there is at least one neighbor $v_i$ where $i  L-1$. The edge $(v_L, v_i)$ closes a cycle: $v_i - v_{i+1} - \ldots - v_L - v_i$. The existence of this cycle ensures the graph has a finite [girth](@entry_id:263239) [@problem_id:1506856].

#### Bipartiteness and Even Cycles

Another profound connection exists between a graph's [cycle structure](@entry_id:147026) and its ability to be partitioned. A graph is **bipartite** if its vertex set $V$ can be partitioned into two [disjoint sets](@entry_id:154341), say $V_1$ and $V_2$, such that every edge in the graph connects a vertex in $V_1$ to one in $V_2$. A key theorem in graph theory states that **a graph is bipartite if and only if it contains no odd-length cycles**.

This property has a direct implication for the girth of a [bipartite graph](@entry_id:153947). If a bipartite graph contains any cycle, that cycle must have an even length. Therefore, the girth of any non-acyclic bipartite graph must be an even number, with the smallest possibility being 4.

Consider a graph on vertices $\{1, 2, \ldots, 12\}$ where an edge $(u,v)$ exists if their sum $u+v$ is odd and their difference $|u-v| > 2$. The condition that $u+v$ is odd means that one vertex must be even and the other odd. This structure inherently defines a [bipartite graph](@entry_id:153947) with partitions being the set of even-labeled vertices and the set of odd-labeled vertices. Since the graph is bipartite, it cannot contain any 3-cycles. Its girth must be at least 4. We can then search for a 4-cycle. The vertices $1, 6, 3, 8$ form such a cycle:
- $(1,6)$: $1+6=7$ (odd), $|1-6|=5 > 2$.
- $(6,3)$: $6+3=9$ (odd), $|6-3|=3 > 2$.
- $(3,8)$: $3+8=11$ (odd), $|3-8|=5 > 2$.
- $(8,1)$: $8+1=9$ (odd), $|8-1|=7 > 2$.
Since we have found a 4-cycle, and we know no 3-cycles can exist, the girth of this graph is exactly 4 [@problem_id:1506844].

### The Impact of Graph Operations on Girth and Circumference

Understanding how graph modifications affect [girth](@entry_id:263239) and circumference is essential for applications in network design and robustness analysis.

#### Edge Removal

Consider removing an edge $e$ from a graph $G$ to form a new graph $G' = G-e$. How does the [girth](@entry_id:263239) $g'$ of the new graph relate to the original [girth](@entry_id:263239) $g$? Any cycle that exists in $G'$ must also have existed in $G$, as $G'$ has fewer edges. This means the set of cycles in $G'$ is a subset of the cycles in $G$. Therefore, the length of the [shortest cycle](@entry_id:276378) in $G'$ can be no smaller than the length of the [shortest cycle](@entry_id:276378) in $G$. This gives the fundamental inequality:
$$
g(G') \ge g(G)
$$
If the removed edge $e$ was not part of any [shortest cycle](@entry_id:276378) in $G$, then all original shortest cycles remain in $G'$, and $g' = g$. However, if the edge $e$ was part of *every* [shortest cycle](@entry_id:276378) in $G$, its removal destroys all cycles of length $g$. The new girth $g'$ will be the length of the next-[shortest cycle](@entry_id:276378) in the original graph, meaning $g' > g$ [@problem_id:1506843].

#### Vertex Removal

Removing a vertex is a more drastic operation, as it also removes all incident edges. This can radically alter the cycle structure. A fascinating example illustrates this complexity. Consider a graph $G$ built from a $C_{25}$ and a $C_{30}$ by adding two "bridge" edges, $(a_0, b_0)$ and $(a_5, b_6)$, where $a_i$ are vertices of the $C_{25}$ and $b_j$ are vertices of the $C_{30}$. The cycles in this graph are either the original $C_{25}$ and $C_{30}$, or new cycles that traverse both components using the bridge edges. By analyzing the path lengths, we can find that the shortest of these new cycles has length $5+6+2 = 13$, and the longest has length $20+24+2 = 46$. Thus, for the full graph, $g(G) = 13$ and $c(G) = 46$.

Now, let's remove vertex $v=a_0$. This action removes the edges $(a_{24}, a_0)$, $(a_0, a_1)$, and crucially, the bridge edge $(a_0, b_0)$. The new graph, $G-v$, no longer has any cycles that span both original components, as there is only one connecting edge left, $(a_5, b_6)$, which now acts as a bridge. The only cycles remaining in $G-v$ are those entirely within the original $C_{30}$. Consequently, for $G-v$, its [girth](@entry_id:263239) and circumference are both 30.

Comparing the values before and after removal reveals a dramatic shift: the [girth](@entry_id:263239) increased from $g(G)=13$ to $g(G-v)=30$, while the circumference decreased from $c(G)=46$ to $c(G-v)=30$ [@problem_id:1506828]. This case study demonstrates that local modifications can have significant and sometimes counter-intuitive global consequences on a graph's cycle parameters.

### Conditions for Long Cycles: Circumference and Hamiltonicity

Finally, we turn to the circumference and the search for long cycles. A particularly important type of long cycle is a **Hamiltonian cycle**, which is a simple cycle that visits every vertex in the graph. If a graph on $n$ vertices has a Hamiltonian cycle, its length must be $n$, and this is the maximum possible length for any cycle. Thus, for a Hamiltonian graph, the circumference is exactly $n$.

A central question in graph theory is: which conditions guarantee that a graph is Hamiltonian? A landmark result by Gabriel Andrew Dirac provides a powerful [sufficient condition](@entry_id:276242) based on [minimum degree](@entry_id:273557).

**Dirac's Theorem (1952):** Let $G$ be a [simple graph](@entry_id:275276) with $n \ge 3$ vertices. If the [minimum degree](@entry_id:273557) $\delta(G)$ satisfies $\delta(G) \ge n/2$, then $G$ contains a Hamiltonian cycle.

This theorem establishes a beautiful link between a local property (every vertex having high degree) and a global structural property (the existence of a spanning cycle). As a direct consequence, if $\delta(G) \ge n/2$, we are guaranteed that $c(G) = n$. This is a powerful tool for establishing the circumference of dense graphs. For instance, a network of 40 servers where each is connected to at least 25 others satisfies the condition $25 \ge 40/2$. By Dirac's Theorem, this network must have a Hamiltonian cycle, and its circumference is guaranteed to be 40 [@problem_id:1506864].

It is critical to understand the precise statement of such theorems. The converse of Dirac's Theorem is not true; a graph can have a circumference of $n$ without its [minimum degree](@entry_id:273557) being at least $n/2$. The cycle graph $C_n$ for $n \ge 5$ is a prime example: its circumference is $n$, but its [minimum degree](@entry_id:273557) is only 2, which is less than $n/2$ [@problem_id:1506847]. Similarly, one cannot assume that all regular graphs are Hamiltonian. The famous Petersen graph is 3-regular on 10 vertices, but its circumference is 9, not 10. These counterexamples highlight the specific power and limits of results like Dirac's Theorem in the study of graph cycles.