## Introduction
The challenge of traversing every path in a network exactly once, famously born from the Seven Bridges of Königsberg puzzle, remains a fundamental problem in graph theory with profound practical implications. While Leonhard Euler provided the elegant conditions to determine *if* such a journey, known as an Eulerian tour, is possible, the question of *how* to systematically construct one requires a robust algorithm. This article bridges that gap by providing a comprehensive guide to Hierholzer's algorithm, a remarkably efficient method for finding Eulerian circuits and paths. Across the following chapters, you will gain a deep, practical understanding of this topic. The first chapter, **Principles and Mechanisms**, will dissect the algorithm's core logic, explaining why it is guaranteed to work. Next, **Applications and Interdisciplinary Connections** will showcase its real-world utility in fields from logistics and network design to modern [bioinformatics](@entry_id:146759). Finally, **Hands-On Practices** will offer a series of problems to solidify your learning and test your implementation skills.

## Principles and Mechanisms

This chapter transitions from the question of *whether* an Eulerian tour exists to the more practical questions of *how* to find one and *why* the methods for doing so are guaranteed to work. The central focus will be on a remarkably elegant and efficient procedure known as **Hierholzer's algorithm**. We will dissect this algorithm, not merely as a set of instructions, but as a [constructive proof](@entry_id:157587) of the existence of Eulerian circuits. By understanding its mechanics, we gain a deeper appreciation for the fundamental graph properties that underpin it.

### The Foundational Conditions for Eulerian Tours

Before embarking on a search for an Eulerian tour—a trail that traverses every edge of a graph exactly once—it is imperative to determine if such a tour is even possible. Attempting to run a complex algorithm on a graph that cannot support such a tour is computationally wasteful. Fortunately, a simple set of conditions, first articulated by Leonhard Euler, provides a definitive test.

An **Eulerian circuit** is a closed tour, starting and ending at the same vertex, that uses every edge exactly once. Consider an automated street-sweeping vehicle that must cover every road segment in a district and return to its depot [@problem_id:1512156]. For any intermediate intersection (vertex) on its route, the vehicle must enter it via one road (edge) and leave via a different road. This natural pairing of "in" and "out" edges at every vertex visited implies that the total number of edges connected to any such vertex must be a multiple of two. Even the start/end vertex follows this rule, as every departure is eventually matched by a return, with the final return completing the last pair. This leads to our first critical property:

**For a graph to possess an Eulerian circuit, every vertex must have an even degree.**

However, this condition alone is insufficient. Imagine a city with two separate, unconnected neighborhood grids. Even if every intersection in both grids has an even number of roads, a single vehicle cannot sweep all the roads, as it cannot travel between the disconnected neighborhoods. This illustrates the second condition: connectivity. The graph must not consist of separate, unreachable parts. As illustrated in the case of a graph composed of two disconnected triangles, every vertex has a degree of $2$, but no single tour can cover all six edges. The algorithm would trace one triangle and then halt, as no vertex on that tour has an edge leading to the other component [@problem_id:1512144].

Combining these observations gives us Euler's celebrated theorem for Eulerian circuits:

> A finite, [undirected graph](@entry_id:263035) $G$ has an Eulerian circuit if and only if it is connected (ignoring any [isolated vertices](@entry_id:269995)) and every vertex in $G$ has an even degree.

What if we relax the requirement that the tour must start and end at the same vertex? Such a tour is called an **Eulerian path**. In this case, there will be exactly one starting vertex and one ending vertex. At the starting vertex, the first edge is an "out" edge with no corresponding "in" edge. At the ending vertex, the final edge is an "in" edge with no corresponding "out" edge. These two special vertices will therefore have an odd degree. Every intermediate vertex, however, is both entered and exited, and thus must still have an even degree.

This leads to the generalized conditions for the existence of either an Eulerian path or an Eulerian circuit [@problem_id:1512105]:

> A finite, [undirected graph](@entry_id:263035) $G$ contains an Eulerian tour (either a path or a circuit) if and only if it is connected (ignoring [isolated vertices](@entry_id:269995)) and it has either zero or exactly two vertices of odd degree.

It is a fundamental result (often called the [handshaking lemma](@entry_id:261183)) that the number of odd-degree vertices in any graph must be even. Therefore, a connected graph can have 0, 2, 4, 6, ... vertices of odd degree. The conditions above state that only the cases of 0 and 2 permit an Eulerian tour. Checking these degree and connectivity conditions is a fast and efficient prerequisite before deploying a more complex algorithm like Hierholzer's.

### The Mechanism of Hierholzer's Algorithm

Hierholzer's algorithm provides a constructive method to find an Eulerian tour, effectively proving the "sufficiency" part of Euler's theorem (i.e., if the conditions are met, a tour is guaranteed to exist). Its core strategy is remarkably intuitive: find one cycle, and if that doesn't cover the whole graph, find another cycle that shares a vertex with the first and splice them together. This process is repeated until all edges are incorporated.

#### Finding a Sub-Tour Without Getting Stuck

Let us assume we have a [connected graph](@entry_id:261731) where every vertex has an even degree. The algorithm begins by selecting an arbitrary starting vertex, $v_0$, and embarking on a trail, traversing only unused edges. A common concern for any trail-finding procedure is the possibility of getting "stuck" at some vertex $v_k$ before the tour is complete—that is, arriving at $v_k$ and finding no unused edges to leave with.

Hierholzer's algorithm is elegantly immune to this problem for any vertex other than the starting one, $v_0$. The reason lies in the even-degree property [@problem_id:1512128]. Let's consider any intermediate vertex $v_k \neq v_0$. Since $\deg(v_k)$ is even, let's say $\deg(v_k) = 2m$. The first time our trail visits $v_k$, it uses one edge to enter and one to leave, consuming two edges. If the trail visits $v_k$ a second time, it again consumes a pair of edges. Now, suppose our trail has just entered $v_k$ for the $j$-th time, making it the current end of our trail. At this moment, we have used $2(j-1) + 1$ edges connected to $v_k$ (an odd number). The number of remaining, unused edges at $v_k$ is $\deg(v_k) - (2(j-1)+1) = 2m - 2j + 2 - 1 = 2(m-j+1) - 1$, which is also an odd number. Since this number cannot be zero, there must be at least one unused edge available for exiting.

Therefore, a trail starting at $v_0$ can never get stuck at an intermediate vertex. The only vertex at which the trail can terminate is the one where it began, $v_0$. This guarantees that the process of arbitrarily following unused edges will always produce a closed tour (a circuit).

#### The Splicing Procedure: Integrating Sub-Tours

After the algorithm finds its first circuit, say $C_1$, it may be that $C_1$ does not include all edges of the graph. At this point, the genius of Hierholzer's method becomes apparent. Because the original graph $G$ was connected, there must be at least one vertex on the circuit $C_1$ that is connected to the [subgraph](@entry_id:273342) of unused edges. If this were not the case, no path would exist from any vertex in $C_1$ to any vertex not in $C_1$, contradicting the graph's connectivity [@problem_id:1512159].

Furthermore, let's consider the subgraph $G'$ formed by the unused edges. Every vertex in $G'$ also has an even degree. This is because the circuit $C_1$ used an even number of edges at every vertex it touched. For any vertex $v$, its degree in $G'$, $\deg_{G'}(v)$, is its original degree $\deg_G(v)$ minus the number of edges used by $C_1$ at $v$. Since both of these numbers are even, their difference is also even.

This means the remaining edges form a collection of (one or more) components, each of which is itself Eulerian.

The algorithm proceeds as follows [@problem_id:1512143] [@problem_id:1512141]:
1.  Scan the vertices of the current main tour, $C_{main}$.
2.  Find the first vertex, let's call it $v_{splice}$, that has an incident unused edge.
3.  Starting from $v_{splice}$, begin a new sub-tour, $C_{sub}$, using only edges from the unused subgraph $G'$. Because all vertices in $G'$ have even degree, this sub-tour is guaranteed to be a circuit, returning to $v_{splice}$.
4.  Splice $C_{sub}$ into $C_{main}$. If $C_{main}$ was the sequence $(\dots, u, v_{splice}, w, \dots)$, the new main tour becomes $(\dots, u, \text{sequence of } C_{sub}, w, \dots)$. Note that $C_{sub}$ starts and ends with $v_{splice}$, so the sequence is seamless.

Let's illustrate with a concrete example. Suppose an algorithm has found an initial tour $T_1 = (\text{A, B, D, C, A})$ in a larger graph. The edges $\{\text{A,B}\}, \{\text{B,D}\}, \{\text{D,C}\}, \{\text{C,A}\}$ are now used. We scan the tour: A has no unused edges. B, however, is found to have unused incident edges. We start a new sub-tour from B, using only remaining edges. Suppose this process, following some deterministic rule (e.g., choosing the alphabetical-first neighbor), yields the sub-tour $T_2 = (\text{B, E, D, F, E, G, B})$ [@problem_id:1512141].

To splice, we replace the vertex B in the original tour with the entire sequence of $T_2$.
Original tour: $(\text{A}, \mathbf{B}, \text{D, C, A})$
Sub-tour: $(\mathbf{B, E, D, F, E, G, B})$
The new, longer tour is: $(\text{A}, \mathbf{B, E, D, F, E, G, B}, \text{D, C, A})$.

This process is repeated until no unused edges remain. Since each step incorporates at least one new edge, the algorithm is guaranteed to terminate, with the final result being a single circuit that includes every edge of the graph.

### Extensions and Advanced Insights

#### Hierholzer's vs. Naive Algorithms

One might wonder why such a seemingly complex [splicing](@entry_id:261283) process is necessary. Why not just use a simple "greedy" algorithm: from the current vertex, always go to the next available, unvisited edge? Such methods are prone to failure. A greedy algorithm can prematurely trace a sub-cycle, returning to a vertex whose edges are all now used, trapping the tour before all edges of the graph have been visited. For example, in the complete graph $K_5$, a greedy traversal starting at A might produce the path $\text{A} \to \text{B} \to \text{C} \to \text{A} \to \dots$, closing the A-B-C triangle early and potentially getting stuck at A later on, leaving other edges untouched [@problem_id:1512140]. Hierholzer's systematic approach of finding and merging complete sub-tours ensures this premature "trapping" does not happen.

#### Application to Eulerian Paths

The logic of Hierholzer's algorithm extends directly to finding Eulerian [paths in graphs](@entry_id:268826) with two odd-degree vertices. The only modification is that the algorithm *must* start at one of the two odd-degree vertices. The initial trail-finding process is no longer guaranteed to return to its start. Instead, because of the parity argument, it is guaranteed to terminate only when it reaches the *other* odd-degree vertex. This initial trail forms the backbone of the final path. After this main trail is found, the splicing procedure remains identical: find vertices along the trail with unused edges and splice in closed sub-tours until all edges are exhausted [@problem_id:1512109].

#### The Deeper Principle of Degree Parity

The reliability of Hierholzer's algorithm is rooted in the interplay between a trail and [vertex degree](@entry_id:264944) parity. Let's analyze this with a thought experiment [@problem_id:1512116]. Imagine a graph where all vertices have even degree. Suppose a single edge $(x, y)$ is removed. Now, vertices $x$ and $y$ have odd degree, and all others remain even. If we start a trail at a third vertex, $v$ (which has even degree), where can this trail possibly end (i.e., get stuck)?

-   For any internal vertex $z$ of the trail ($z \neq v, x, y$), it is entered and exited, so an even number of its edges are used. Since $\deg(z)$ is even, the trail can't get stuck at $z$.
-   The trail can only get stuck at a vertex $u$ if the number of its edges used by the trail equals its total degree.
-   An open trail (starting at $v$ and ending at $u \neq v$) uses an odd number of incident edges at its endpoints $v$ and $u$.
-   Therefore, if the trail gets stuck at $u \neq v$, $\deg(u)$ must be odd. The only such vertices are $x$ and $y$.
-   If the trail gets stuck at its starting point $v$, it must have formed a closed loop. This uses an even number of edges at $v$. Since $\deg(v)$ is even, this is also possible.

This confirms that the walk can only terminate at one of the odd-degree vertices ($x$ or $y$) or by forming a closed loop back at its even-degree starting point ($v$). This fundamental principle governs why walks terminate where they do, and it is the mathematical bedrock upon which Hierholzer's algorithm is built. It is not just a clever procedure; it is a physical manifestation of the properties of degree parity in graphs.