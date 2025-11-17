## Introduction
In the study of networks, we often encounter systems that are built by combining or overlaying simpler structures. From merging transportation routes to integrating layers of a communication network, the need to synthesize complex graphs from basic components is a fundamental challenge. The **[union of graphs](@entry_id:267788)** provides the formal mathematical tool to address this, allowing us to merge two or more graphs into a single, unified entity. But how does this seemingly simple operation affect the underlying structure and properties of the resulting network? How can combining two simple, [disconnected graphs](@entry_id:275570) create a robust, connected system?

This article delves into the theory and application of the graph union. The first chapter, **Principles and Mechanisms**, will lay the groundwork by formally defining the union operation and exploring its algebraic representation. We will investigate its impact on key graph properties such as vertex degrees, connectivity, and cycles, and identify important characteristics that are not preserved. Next, in **Applications and Interdisciplinary Connections**, we will see the union operation in action, exploring how it is used to construct well-known graph families, model [emergent phenomena](@entry_id:145138) in network science, and solve problems in fields like control theory. Finally, the **Hands-On Practices** section will provide you with the opportunity to solidify your understanding by tackling concrete problems that highlight the core concepts discussed.

## Principles and Mechanisms

In our study of graphs, we often need to construct more [complex networks](@entry_id:261695) from simpler ones. One of the most fundamental methods for combining graphs is the **graph union**. This operation, analogous to the union of sets, allows us to merge the structures of two or more graphs into a single, unified entity. Understanding the principles and mechanisms of the graph union is essential, as it provides a basis for modeling systems that evolve or are formed by the aggregation of different components, such as merging transportation networks, combining communication layers, or analyzing the combined strengths of structural supports.

### Defining the Graph Union

Formally, the union of two graphs, $G_1 = (V_1, E_1)$ and $G_2 = (V_2, E_2)$, is a new graph $G = G_1 \cup G_2$ whose vertex set is the union of the individual vertex sets, $V = V_1 \cup V_2$, and whose edge set is the union of the individual edge sets, $E = E_1 \cup E_2$.

A particularly important and common case is when two graphs are defined on the same set of vertices. If $G_1 = (V, E_1)$ and $G_2 = (V, E_2)$, their union is the graph $G = (V, E_1 \cup E_2)$. In this scenario, the set of vertices remains unchanged, and the new edge set simply contains all edges that were present in either of the original graphs. An edge $\{u, v\}$ exists in $G_1 \cup G_2$ if and only if $\{u, v\}$ is an edge in $G_1$ or $\{u, v\}$ is an edge in $G_2$ (or both).

Imagine, for instance, a metropolitan area with two competing bus companies, "CityHopper" ($G_1$) and "RegionalExpress" ($G_2$), serving the same set of hubs ($V$). To create a unified public transportation map, the city authority would form the union of the two route networks. The resulting graph, $G_1 \cup G_2$, would represent all available direct routes, where a connection exists between two hubs if at least one of the companies provides that service [@problem_id:1547927].

### Algebraic and Computational Representations of the Union

The abstract definition of the union naturally translates into operations on common graph [data structures](@entry_id:262134). Considering graphs on the same ordered vertex set $V = \{v_1, v_2, \dots, v_n\}$ is particularly insightful.

#### Adjacency Matrices

Let $A_1$ and $A_2$ be the $n \times n$ adjacency matrices for [simple graphs](@entry_id:274882) $G_1$ and $G_2$, respectively. The entry $(A_k)_{ij}$ is $1$ if an edge exists between $v_i$ and $v_j$ in $G_k$, and $0$ otherwise. We seek the [adjacency matrix](@entry_id:151010) $A$ of the union graph $G = G_1 \cup G_2$.

An edge $\{v_i, v_j\}$ is in the union graph $G$ if and only if it is in $G_1$ **or** it is in $G_2$. This logical structure maps directly onto the entries of the adjacency matrices. The entry $A_{ij}$ should be $1$ if $(A_1)_{ij} = 1$ or $(A_2)_{ij} = 1$. This is precisely the definition of the **logical OR** operation ($\lor$). Therefore, the adjacency matrix of the union is found by applying the element-wise logical OR to the original matrices:

$A_{ij} = (A_1)_{ij} \lor (A_2)_{ij}$

This formulation is elegant and computationally efficient. It is crucial to distinguish this from other operators. For example, the logical AND ($\land$) would correspond to the *intersection* of the graphs (edges present in both), while arithmetic addition, $A_{ij} = (A_1)_{ij} + (A_2)_{ij}$, is not suitable for [simple graphs](@entry_id:274882) as it would result in entries of $2$ for edges present in both graphs, which is characteristic of a [multigraph](@entry_id:261576) representation [@problem_id:1547948].

#### Adjacency Lists

When graphs are represented by adjacency lists, the union operation is just as intuitive. The neighborhood of a vertex $v$ in the union graph $G_1 \cup G_2$, denoted $N_{G_1 \cup G_2}(v)$, is the set of all vertices adjacent to $v$ in either $G_1$ or $G_2$. This corresponds to the union of the individual neighborhood sets:

$N_{G_1 \cup G_2}(v) = N_{G_1}(v) \cup N_{G_2}(v)$

To construct the [adjacency list](@entry_id:266874) for the union graph, one simply merges the adjacency lists for each vertex from the original graphs and removes any duplicate entries. For example, if in the transportation network scenario, hub C is connected to hubs {A, D} in the CityHopper network and to hubs {B, F} in the RegionalExpress network, its neighbors in the unified map would be $\{A, D\} \cup \{B, F\} = \{A, B, D, F\}$ [@problem_id:1547927].

### Structural Properties of the Union

The true power and complexity of the union operation become apparent when we examine its effect on fundamental graph properties. The union does not merely sum the properties of its constituents; it can create entirely new and emergent structures.

#### Vertex Degrees

From the [adjacency list](@entry_id:266874) representation, we can immediately state the [degree of a vertex](@entry_id:261115) $v$ in the union graph $G = G_1 \cup G_2$:

$\deg_G(v) = |N_{G_1}(v) \cup N_{G_2}(v)|$

Using the [principle of inclusion-exclusion](@entry_id:276055) for sets, we can express this as:

$\deg_G(v) = |N_{G_1}(v)| + |N_{G_2}(v)| - |N_{G_1}(v) \cap N_{G_2}(v)| = \deg_{G_1}(v) + \deg_{G_2}(v) - |N_{G_1}(v) \cap N_{G_2}(v)|$

The final term represents the number of neighbors that $v$ has in common in both graphs. This shows that the [degree of a vertex](@entry_id:261115) in the union is the sum of its degrees in the component graphs only if its neighborhoods are disjoint.

This relationship allows us to bound the maximum degree, $\Delta(G)$, of the union graph. For any vertex $v$, we have $\deg_G(v) \le \deg_{G_1}(v) + \deg_{G_2}(v)$. This implies that the maximum degree of the union cannot exceed the sum of the maximum degrees of the components:

$\Delta(G_1 \cup G_2) \le \Delta(G_1) + \Delta(G_2)$

In some cases, this inequality can be an equality. Consider a graph on vertices labeled by the integers modulo 12, $V = \{0, 1, \dots, 11\}$. Let $G_1$ connect vertices whose labels differ by $\pm 2$, and $G_2$ connect vertices whose labels differ by $\pm 3$. In $G_1$, every vertex has degree 2. In $G_2$, every vertex also has degree 2. In the union $G = G_1 \cup G_2$, the neighbors of any vertex $v$ are $\{v+2, v-2, v+3, v-3\}$, all modulo 12. Since these four neighbors are distinct for any $v$, the degree of every vertex in $G$ is exactly $4$. Thus, $\Delta(G) = 4$, which equals $\Delta(G_1) + \Delta(G_2) = 2+2$. This is because for every vertex, the set of neighbors from $G_1$ is disjoint from the set of neighbors from $G_2$ [@problem_id:1547904].

#### Connectivity and Cycles

The union operation can fundamentally alter the connectivity of a graph. A striking example is that the **union of two [disconnected graphs](@entry_id:275570) can be connected**. Consider a set of six nodes, $V = \{v_1, \dots, v_6\}$. Let $G_1$ be a graph consisting of three separate edges, $E_1 = \{\{v_1, v_2\}, \{v_3, v_4\}, \{v_5, v_6\}\}$, which is clearly disconnected. Let $G_2$ be another [disconnected graph](@entry_id:266696) with two edges, $E_2 = \{\{v_2, v_3\}, \{v_4, v_5\}\}$. The union $G_1 \cup G_2$ has the edge set $E = \{\{v_1, v_2\}, \{v_2, v_3\}, \{v_3, v_4\}, \{v_4, v_5\}, \{v_5, v_6\}\}$. This union graph is the path graph $P_6$, which connects all vertices and is therefore a [connected graph](@entry_id:261731) [@problem_id:1547951].

Just as unions can create paths that connect components, they can also introduce cycles. A powerful illustration of this is the union of two distinct spanning trees. A **spanning tree** on $n$ vertices is a connected [subgraph](@entry_id:273342) with no cycles, which necessarily has exactly $n-1$ edges. Let $T_1$ and $T_2$ be two distinct spanning trees on the same set of $n \ge 3$ vertices. Since they are distinct, there is at least one edge in $T_1$ that is not in $T_2$. Let's say they share $k$ edges, where $k  n-1$.

The number of edges in the union graph $T_1 \cup T_2$ is given by the [inclusion-exclusion principle](@entry_id:264065):
$|E(T_1 \cup T_2)| = |E(T_1)| + |E(T_2)| - |E(T_1) \cap E(T_2)| = (n-1) + (n-1) - k = 2n-2-k$.

Since both $T_1$ and $T_2$ are connected and span all $n$ vertices, their union is also connected. A fundamental theorem of graph theory states that a connected graph with $n$ vertices and $m$ edges has a [cyclomatic number](@entry_id:267135) (the minimum number of edges to remove to make it acyclic) of $m-n+1$. For the graph $T_1 \cup T_2$, this number is:
$(2n-2-k) - n + 1 = n-1-k$.

Since $k  n-1$, the value $n-1-k$ is at least 1. This proves that the union $T_1 \cup T_2$ must contain at least one cycle. Furthermore, it tells us exactly how many "redundant" edges have been created in terms of cycles [@problem_id:1547936].

### Properties Not Preserved by Union

While the union operation can build connectivity and create cycles, it is important to recognize that it does not preserve all desirable graph properties. The union of two graphs from a specific class is not guaranteed to remain in that class.

*   **Bipartiteness**: A graph is bipartite if its vertices can be partitioned into two sets such that no edge connects two vertices within the same set. This property is equivalent to having no odd-length cycles. The union of two bipartite graphs is **not** necessarily bipartite. A minimal counterexample can be constructed on just three vertices, $V = \{1, 2, 3\}$. Let $G_1$ be the path graph with edges $\{\{1,2\}, \{2,3\}\}$, which is bipartite (partition $\{2\}$ and $\{1,3\}$). Let $G_2$ be the graph with the single edge $\{\{1,3\}\}$, which is also bipartite. Their union, $G_1 \cup G_2$, has the edges $\{\{1,2\}, \{2,3\}, \{1,3\}\}$, forming a 3-cycle ($K_3$). Since this union contains an odd cycle, it is not bipartite [@problem_id:1547919].

*   **Planarity**: A graph is planar if it can be drawn in the plane with no edges crossing. This property is also not closed under union. One of the classic [non-planar graphs](@entry_id:268333) is the complete graph on five vertices, $K_5$. We can construct $K_5$ as the union of two planar graphs. On a vertex set $V=\{v_1, \dots, v_5\}$, let $G_1$ be the 5-cycle graph $C_5$, with edges connecting adjacent vertices (e.g., $\{v_1,v_2\}, \{v_2,v_3\}, \dots, \{v_5,v_1\}$). This is clearly planar. Now, let $G_2$ be the "star" cycle, with edges connecting vertices at distance 2 (e.g., $\{v_1,v_3\}, \{v_3,v_5\}, \dots, \{v_4,v_1\}$). This is also a 5-cycle and is planar. The union $G_1 \cup G_2$ contains all 10 possible edges on 5 vertices, forming the [non-planar graph](@entry_id:261758) $K_5$ [@problem_id:1547918].

### Advanced Applications and Duality

The union operation also features in more abstract structural results, particularly in its relationship with graph complementation.

#### Union with the Complement

The **complement** of a [simple graph](@entry_id:275276) $G=(V, E)$, denoted $\bar{G}$, is a graph on the same vertex set $V$ with an edge set $\bar{E}$ containing precisely those edges that are *not* in $E$. For any pair of distinct vertices $\{u, v\}$, the edge connecting them exists in either $G$ or $\bar{G}$, but never both.

This exclusive relationship leads to a profound and simple result for their union: the union of any simple graph with its complement is the **complete graph** $K_n$.

$G \cup \bar{G} = K_n$

This is because the edge set $E \cup \bar{E}$ contains every possible edge between any two distinct vertices in $V$. This shows how a graph and its "negative" perfectly combine to form a structure of maximum density [@problem_id:1547934]. This concept extends to a form of De Morgan's Law for graphs: the complement of an intersection is the union of the complements, $\overline{G_1 \cap G_2} = \overline{G_1} \cup \overline{G_2}$. This can be used to re-frame complex questions. For instance, a graph of "non-redundant" connections, defined as edges that do not appear in both $G_1$ and $G_2$, is precisely the graph $\overline{G_1 \cap G_2}$, which can be analyzed as the union of the complements $\overline{G_1} \cup \overline{G_2}$ [@problem_id:1547944].

#### Behavior of Graph Parameters

Finally, we can characterize the behavior of certain graph parameters under the union. A parameter $\pi$ is **subadditive** if $\pi(G_1 \cup G_2) \le \pi(G_1) + \pi(G_2)$. The **[vertex cover number](@entry_id:276590)**, $\tau(G)$, which is the size of the smallest set of vertices that "touches" every edge, is one such parameter.

Let $S_1$ and $S_2$ be minimum vertex covers for $G_1$ and $G_2$, respectively. The set $S_1 \cup S_2$ is a valid [vertex cover](@entry_id:260607) for $G_1 \cup G_2$, because any edge in the union must come from either $G_1$ (and is thus covered by $S_1$) or $G_2$ (and is covered by $S_2$). Therefore, the size of the [minimum vertex cover](@entry_id:265319) of the union is at most the size of this constructed cover:
$\tau(G_1 \cup G_2) \le |S_1 \cup S_2| \le |S_1| + |S_2| = \tau(G_1) + \tau(G_2)$.

This establishes the [subadditivity](@entry_id:137224) of the [vertex cover number](@entry_id:276590). It is important to investigate whether this inequality can be strict or must be an equality. In fact, both are possible [@problem_id:1547953].
*   **Equality holds** if $G_1$ and $G_2$ are vertex-disjoint. In this case, their vertex covers do not interact, and the minimal cover for the union is simply the union of the minimal covers of the components.
*   **Strict inequality can hold** if the graphs share structure. For example, if we take the union of a graph with itself, $G_1 \cup G_1 = G_1$, we have $\tau(G_1)  \tau(G_1) + \tau(G_1)$ for any non-[empty graph](@entry_id:262462). The overlap in structure leads to a more efficient covering.

In summary, the graph union is a foundational operation for building and analyzing [complex networks](@entry_id:261695). While its definition is simple, its effects are rich and varied. It can increase connectivity and create new cyclic structures, but it does not universally preserve properties like bipartiteness or [planarity](@entry_id:274781). By understanding these principles, we gain a deeper appreciation for how local connections aggregate to form global graph structures.