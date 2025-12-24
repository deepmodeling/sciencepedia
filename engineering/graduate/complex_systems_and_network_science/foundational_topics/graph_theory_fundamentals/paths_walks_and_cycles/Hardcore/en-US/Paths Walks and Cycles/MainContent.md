## Introduction
While a graph's vertices and edges provide the static skeleton of a complex system, the true dynamics and processes unfold through movement across this structure. The concepts of paths, walks, and cycles are the fundamental language used to describe these movements and their structural implications. Understanding this language is essential for analyzing everything from information flow in social networks and [signal propagation](@entry_id:165148) in biological systems to the robustness of critical infrastructure. This article addresses the need for a rigorous framework to define, count, and analyze these network traversals, bridging the gap between abstract definitions and their powerful real-world applications.

Over the next three chapters, you will build a comprehensive understanding of this core topic. In **Principles and Mechanisms**, we will establish a formal [taxonomy](@entry_id:172984) of traversal—from walks to simple cycles—and explore the elegant algebraic methods for their enumeration. We will then delve into the profound consequences of these concepts by examining classic problems like Eulerian and Hamiltonian paths. Next, in **Applications and Interdisciplinary Connections**, we will see how these theoretical tools are applied across physics, biology, and economics to characterize network topology, predict system dynamics, and optimize [network flows](@entry_id:268800). Finally, **Hands-On Practices** will provide opportunities to apply these principles directly, solidifying your grasp of path-based analysis through targeted computational problems.

## Principles and Mechanisms

The abstract concept of a graph, consisting of vertices and edges, provides a static skeleton for a complex system. To understand the dynamics and processes that unfold upon these networks, we must study the ways in which one can move from vertex to vertex. This chapter delves into the fundamental principles and mechanisms of movement on graphs, establishing a rigorous [taxonomy](@entry_id:172984) of paths, walks, and cycles, and exploring their profound implications for network structure, function, and [algorithmic analysis](@entry_id:634228).

### A Taxonomy of Traversal

The most general notion of traversal on a graph is a **walk**. A walk is a sequence of vertices, $W = (v_0, v_1, \dots, v_k)$, where for each step from $v_{i-1}$ to $v_i$, the edge $\{v_{i-1}, v_i\}$ exists in the graph's edge set $E$. In a simple walk, there are no constraints on repeating vertices or edges; any sequence of adjacent vertices constitutes a valid walk. The **length** of a walk is the number of edges it contains, which is $k$ for the sequence above.

While the walk is a foundational concept, more constrained forms of traversal are often more relevant for modeling realistic processes. These constraints typically involve forbidding repetition. By systematically applying such constraints, we can build a precise hierarchy of traversal types .

A **trail** is a walk in which no edge is traversed more than once. Vertices, however, may be revisited. For example, consider a graph with vertices $\{a, b, c, d, e\}$ and edges allowing the sequence $W_2 = (a, b, e, d, b, c)$. The vertex $b$ is visited twice. However, if the edges traversed, namely $\{a,b\}, \{b,e\}, \{e,d\}, \{d,b\},$ and $\{b,c\}$, are all distinct, then $W_2$ is a valid trail. If any edge were repeated, for instance in a sequence like $(a, b, c, b, c)$ where the edge $\{b,c\}$ is used twice, the sequence would be a walk but not a trail.

A stricter constraint leads to the concept of a **simple path**, or often just a **path**. A simple path is a walk in which no vertices are repeated. This condition immediately implies that no edges can be repeated either, so every simple path is also a trail. A sequence like $W_1 = (a, b, c, d, e)$ where all vertices are distinct is a simple path.

Traversal does not always have distinct start and end points. A **closed walk** is a walk that begins and ends at the same vertex, i.e., $v_0 = v_k$. Within this category, the most important structure is the **simple cycle**, or simply a **cycle**. A simple cycle is a closed walk of length $k \ge 3$ (in a [simple graph](@entry_id:275276)) where the only repeated vertex is the start/end vertex; that is, $v_0 = v_k$, and the vertices $v_0, v_1, \dots, v_{k-1}$ are all distinct. A sequence such as $W_3 = (a, b, c, d, e, a)$ constitutes a simple cycle of length $5$.

This [taxonomy](@entry_id:172984)—from the general walk to the specific simple cycle—provides the fundamental vocabulary for describing movement and structure in networks.

### Algebraic Enumeration of Walks

While the combinatorial definitions of walks and cycles are intuitive, an algebraic approach using the **[adjacency matrix](@entry_id:151010)** of a graph provides powerful computational tools for their enumeration, particularly in [directed graphs](@entry_id:272310) .

Let $G=(V,E)$ be a directed graph with $n$ vertices, labeled $\{1, 2, \dots, n\}$. Its adjacency matrix $A$ is an $n \times n$ matrix where the entry $A_{ij}$ is the number of directed edges from vertex $i$ to vertex $j$. The remarkable power of this representation lies in its behavior under matrix multiplication. The $(i,j)$-th entry of the $k$-th power of the adjacency matrix, $(A^k)_{ij}$, gives the exact number of distinct directed walks of length $k$ from vertex $i$ to vertex $j$.

This can be understood through a brief inductive argument. For $k=1$, $(A^1)_{ij} = A_{ij}$ correctly counts the number of walks of length $1$ (i.e., single edges) from $i$ to $j$. Now, assume $(A^m)_{ip}$ counts the walks of length $m$ from $i$ to any vertex $p$. A walk of length $m+1$ from $i$ to $j$ is formed by taking a walk of length $m$ from $i$ to some intermediate vertex $p$, and then traversing an edge from $p$ to $j$. The total number of such walks is obtained by summing over all possible intermediate vertices $p$: $\sum_{p=1}^n (A^m)_{ip} A_{pj}$. This sum is precisely the definition of the $(i,j)$-th entry of the matrix product $A^m A$. Thus, the number of walks of length $m+1$ is given by $(A^{m+1})_{ij}$.

This principle extends to walks of length $0$. A walk of length $0$ from $i$ to $j$ exists only if $i=j$, in which case it is the trivial walk $(i)$. There is exactly one such walk. This corresponds to the identity matrix $I$, where $I_{ij} = 1$ if $i=j$ and $0$ otherwise. It is therefore standard convention to define $A^0 = I$.

Using this framework, we can also count the total number of walks between two vertices up to a certain length. The total number of directed walks from $i$ to $j$ with a length of at most $K$ is given by the $(i,j)$-th entry of the matrix sum $\sum_{\ell=0}^{K} A^\ell$ .

The diagonal entries of the [matrix powers](@entry_id:264766) are particularly significant. The entry $(A^k)_{ii}$ counts the number of **closed walks** of length $k$ that start and end at vertex $i$. Summing these diagonal entries gives the trace of the matrix, $\mathrm{tr}(A^k) = \sum_{i=1}^n (A^k)_{ii}$, which equals the total number of closed walks of length $k$ in the entire graph.

It is critical, however, to distinguish these closed walks from simple cycles. The quantity $\mathrm{tr}(A^k)$ counts *all* closed walks, including those that revisit vertices and edges multiple times. A single simple cycle of length $k$, say $v_1 \to v_2 \to \dots \to v_k \to v_1$, will be counted $k$ times in the trace: once as the walk $(v_1, \dots, v_1)$ contributing to $(A^k)_{v_1v_1}$, once as $(v_2, \dots, v_2)$ contributing to $(A^k)_{v_2v_2}$, and so on. Therefore, $\mathrm{tr}(A^k)$ includes contributions from all simple cycles of length $k$ (each counted $k$ times), but it is also "contaminated" with counts of non-simple closed walks. Isolating the number of simple cycles from the trace requires more sophisticated combinatorial techniques, such as inclusion-exclusion principles .

### Spanning Traversal: Eulerian and Hamiltonian Paths

Some of the most celebrated problems in graph theory concern paths and cycles that are "spanning" in some sense—either visiting every edge or every vertex of a graph. These two types of problems, while superficially similar, are fundamentally different in their nature and [computational complexity](@entry_id:147058).

#### Eulerian Paths and Circuits

An **Eulerian trail** (or Eulerian path) is a trail in a graph that visits every edge exactly once. If this trail is also closed, it is called an **Eulerian circuit**. The question of their existence was one of the first problems in graph theory, famously solved by Leonhard Euler in his analysis of the Seven Bridges of Königsberg.

The existence of an Eulerian circuit or trail depends on simple, local properties of the graph's vertices. For a connected, undirected graph (or [multigraph](@entry_id:261576)), the conditions are as follows :
1.  An **Eulerian circuit** exists if and only if every vertex in the graph has an even degree. (Note that in a [multigraph](@entry_id:261576), a loop at a vertex adds $2$ to its degree).
2.  An **Eulerian trail** exists if and only if the graph has exactly two vertices of odd degree. The trail must begin at one of the odd-degree vertices and end at the other.

This principle extends naturally to [directed graphs](@entry_id:272310). Here, the notion of degree splits into in-degree (number of incoming edges) and [out-degree](@entry_id:263181) (number of outgoing edges). For a [directed graph](@entry_id:265535) to have an Eulerian circuit, it must be **strongly connected** (meaning there is a directed path from every vertex to every other vertex), and for every vertex $v$, its in-degree must equal its [out-degree](@entry_id:263181): $\text{indeg}(v) = \text{outdeg}(v)$ . This "flow conservation" property at each node ensures that any traversal entering a vertex can also leave, allowing a complete tour of all edges. If the graph instead has exactly one vertex $u$ with $\text{outdeg}(u) - \text{indeg}(u) = 1$ and one vertex $v$ with $\text{indeg}(v) - \text{outdeg}(v) = 1$, with all other vertices balanced, then a directed Eulerian trail exists from $u$ to $v$.

Because these conditions rely on checking vertex degrees and [graph connectivity](@entry_id:266834)—tasks that can be accomplished efficiently in time polynomial in the number of vertices and edges—the problem of deciding whether a graph has an Eulerian path is computationally tractable.

#### Hamiltonian Paths and Cycles

A **Hamiltonian path** is a simple path that visits every vertex in the graph exactly once. A **Hamiltonian cycle** is a simple cycle that does the same. While the definition seems like a simple counterpart to the Eulerian case (visiting vertices instead of edges), the problem of determining their existence is profoundly harder.

Unlike Eulerian paths, there are no simple, local conditions that are both necessary and sufficient for the existence of a Hamiltonian path or cycle. The problem is inherently **global**: one must find a specific permutation of *all* vertices that satisfies the adjacency constraints of the graph. This fundamental difference is reflected in their [computational complexity](@entry_id:147058) .

Deciding whether a graph has a Hamiltonian cycle (the HC problem) is a classic **NP-complete** problem. This means two things :
1.  It is in the [complexity class](@entry_id:265643) **NP** (Nondeterministic Polynomial time): If a graph *does* have a Hamiltonian cycle, a "certificate"—the ordered list of vertices forming the cycle—can be provided. One can easily verify in [polynomial time](@entry_id:137670) that this sequence of vertices visits every vertex once and that all consecutive pairs are connected by an edge.
2.  It is **NP-hard**: It is at least as hard as any other problem in NP. This is formally shown through polynomial-time reductions. For instance, the known NP-complete problem 3-SAT can be reduced to HC. More simply, one can show HC is NP-hard by reducing the (also NP-complete) Hamiltonian Path (HP) problem to it. Given a graph $G$ for which we want to find a Hamiltonian path, we can construct a new graph $G'$ by adding a new universal vertex connected to all original vertices of $G$. The graph $G$ has a Hamiltonian path if and only if the new graph $G'$ has a Hamiltonian cycle. Since this transformation can be done in [polynomial time](@entry_id:137670), it proves that HC is at least as hard as HP .

The chasm in complexity between the Eulerian and Hamiltonian problems is a cornerstone of [computational graph](@entry_id:166548) theory, illustrating how a seemingly small change in a problem's definition—from local edge constraints to global vertex constraints—can lead to an exponential explosion in difficulty.

### Connectivity and Path Disjointness

In many applications, particularly in communication and transportation networks, the existence of a single path is not enough. Network robustness and capacity depend on the existence of multiple, independent routes between a source $s$ and a target $t$. This leads to the study of disjoint paths .

Two simple paths from $s$ to $t$ are **edge-disjoint** if they do not share any edges. They are **node-disjoint** (or, more precisely, **internally vertex-disjoint**) if they do not share any vertices other than the endpoints $s$ and $t$. Node-disjointness is a stronger condition; any set of node-disjoint paths is also edge-disjoint, but the converse is not always true. A set of paths might share an intermediate vertex but use different edges to enter and leave it, making them edge-disjoint but not node-disjoint.

These concepts are formalized by two key graph parameters:
-   The **[vertex-connectivity](@entry_id:267799)**, denoted $\kappa(G)$, is the minimum number of vertices whose removal would disconnect the graph or reduce it to a single vertex.
-   The **[edge-connectivity](@entry_id:272500)**, denoted $\lambda(G)$, is the minimum number of edges whose removal would disconnect the graph.

The profound link between connectivity and disjoint paths is captured by **Menger's Theorem**, a cornerstone of graph theory. In its vertex form, it states that for any two non-adjacent vertices $s$ and $t$, the maximum number of [internally vertex-disjoint paths](@entry_id:270533) between them, $p_v(s, t)$, is equal to the minimum number of vertices in an $s-t$ separator (a set of vertices whose removal disconnects $s$ from $t$). The edge form is analogous: the maximum number of [edge-disjoint paths](@entry_id:271919), $p_e(s, t)$, is equal to the minimum number of edges in an $s-t$ edge-separator.

For instance, consider a graph constructed from two complete graphs on five vertices, $K_5$, which share exactly two vertices, $\{x,y\}$ . Let $s$ be a vertex unique to the first $K_5$ and $t$ be a vertex unique to the second. Any path from $s$ to $t$ must pass through either $x$ or $y$. This means the set $\{x,y\}$ is an $s-t$ [vertex separator](@entry_id:272916) of size $2$. By Menger's theorem, the maximum number of node-disjoint paths between $s$ and $t$ is $p_v(s,t) = 2$. Indeed, one can construct two such paths, e.g., $(s,x,t)$ and $(s,y,t)$. The global [vertex-connectivity](@entry_id:267799) of this graph is also $\kappa(G)=2$. However, because the cliques are highly connected internally, more paths are possible if they are allowed to share nodes. For instance, paths like $(s,a,x,c,t)$ and $(s,b,y,d,t)$ can be constructed in addition to the direct ones, allowing for $p_e(s,t)=4$ [edge-disjoint paths](@entry_id:271919), which is limited by the degree of the source/target nodes. In this case, $\lambda(G) = 4$. This example powerfully illustrates how vertex bottlenecks can be more restrictive than edge bottlenecks.

### Advanced and Generalized Path Concepts

The classical notions of paths and cycles have been extended and adapted to capture the complexities of modern network models, including those with memory, multiple layers, and time-varying topologies.

#### Non-Backtracking Walks

A standard walk has a "memoryless" property at each step. A **non-[backtracking](@entry_id:168557) walk** introduces a minimal memory of one step: it is a walk on the directed edges (arcs) of a graph that is forbidden from immediately reversing its direction . If a walk traverses an arc $u \to v$, the next arc cannot be $v \to u$. Such walks avoid trivial, redundant traversals and have been shown to be fundamental to understanding graph spectra and community structure.

The dynamics of non-[backtracking](@entry_id:168557) walks can be perfectly captured by the **Hashimoto matrix** (or non-[backtracking](@entry_id:168557) operator), $B$. This is a matrix whose rows and columns are indexed by the directed arcs of the graph. For a graph with $|E|$ undirected edges, there are $2|E|$ arcs, so $B$ is a $2|E| \times 2|E|$ matrix. An entry $B_{e_1, e_2}$ is $1$ if arc $e_2$ can follow arc $e_1$ in a non-[backtracking](@entry_id:168557) walk, and $0$ otherwise. That is, if $e_1 = (u \to v)$ and $e_2 = (x \to y)$, then $B_{e_1, e_2}=1$ if and only if $x=v$ (head-to-tail adjacency) and $y \neq u$ (non-reversal). The powers of this matrix, $(B^k)_{e_1, e_2}$, count the number of non-[backtracking](@entry_id:168557) walks of length $k+1$ that start with arc $e_1$ and end with arc $e_2$.

#### Paths in Multilayer Networks

Many real-world systems are best modeled as **[multilayer networks](@entry_id:261728)**, where a common set of nodes participates in different types of relationships, represented as layers. A path in such a network can now move both within a layer (**intralayer** steps) and between layers at the same node (**interlayer** steps) .

The entire system can be represented by a **[supra-adjacency matrix](@entry_id:755671)**, $S$. For a two-layer network with intralayer adjacency matrices $A^{[1]}$ and $A^{[2]}$, and interlayer coupling between node replicas, $S$ takes a [block matrix](@entry_id:148435) form:
$$
S = \begin{pmatrix} A^{[1]} & \omega I \\ \omega I & A^{[2]} \end{pmatrix}
$$
Here, the diagonal blocks $A^{[\alpha]}$ describe intralayer connections, while the off-diagonal blocks $\omega I$ describe the weighted connections between a node in one layer and its counterpart in the other (where $\omega$ is the [coupling strength](@entry_id:275517) and $I$ is the identity matrix). The algebraic counting principle holds: the powers of $S$ count the number of walks in this multilayer system. A notable property is that for a walk to start and end in the same layer, it must make an even number of interlayer transitions .

#### Paths in Temporal Networks

When interactions are not persistent, we enter the realm of **[temporal networks](@entry_id:269883)**, where edges are only active at specific points or intervals in time. A path in such a network must be a **time-respecting path**, meaning it is causally feasible . A sequence of edges $(v_0 \to v_1), (v_1 \to v_2), \dots$ is only valid if the traversal of edge $(v_{i-1} \to v_i)$ begins *after* arriving at $v_{i-1}$ and *after* the edge itself becomes available.

In this context, the familiar notion of a "shortest path" fragments into several distinct concepts of optimality. For instance:
-   The **shortest path** is typically the one with the minimum number of edges (hops).
-   The **fastest path** is the one that minimizes the total travel duration, resulting in the earliest possible arrival time at the destination.

These two are not necessarily the same. Consider a 2-hop path where a long wait is required at the intermediate node for the second edge to become available. A different 3-hop path with no waiting time might yield a much earlier arrival time, thus being faster despite being longer in terms of hops . Understanding these distinctions is paramount for optimizing processes on dynamic networks.