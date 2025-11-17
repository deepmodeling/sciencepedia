## Introduction
While [simple graphs](@entry_id:274882) provide a powerful foundation for network analysis, they often fall short in representing the true complexity of real-world systems. How do we model a transit system with multiple bus routes between the same two stops, or a computer network where a server communicates with itself? This gap is bridged by extending graph theory to include **loops** and **multiple edges**. This article provides a comprehensive introduction to these crucial concepts. In the **Principles and Mechanisms** section, we will formalize the definitions of multigraphs and pseudographs, redefining core properties like [vertex degree](@entry_id:264944) and re-examining the Handshaking Lemma. The **Applications and Interdisciplinary Connections** section will demonstrate how these structures are essential for accurately modeling systems in fields from ecology to network engineering. Finally, the **Hands-On Practices** section will solidify your understanding with targeted exercises on analyzing and constructing graphs with loops and multiple edges.

## Principles and Mechanisms

In the study of graphs, our initial focus is often on **[simple graphs](@entry_id:274882)**, where any two vertices are connected by at most one edge, and no edge connects a vertex to itself. This foundational model is powerful, yet many real-world systems exhibit complexities that [simple graphs](@entry_id:274882) cannot capture. Consider a transit map with multiple bus routes between the same two junctions, a social network where individuals can have multiple types of relationships, or a computer network where a server runs internal diagnostics by communicating with itself. To model such phenomena, we must extend our framework to include **multiple edges** and **loops**. This section will formalize these concepts and explore how their inclusion reshapes fundamental graph properties and enables more sophisticated analysis.

### From Simple Graphs to Pseudographs

The world of graphs can be seen as a hierarchy of increasing structural freedom. At the base lies the [simple graph](@entry_id:275276). When we relax the restriction that there can be at most one edge between any two vertices, we enter the realm of **multigraphs**.

A **[multigraph](@entry_id:261576)** consists of a set of vertices $V$ and a multiset of edges $E$. The use of a multiset for $E$ formally allows for multiple, distinct edges to connect the same pair of vertices, $\{u, v\}$. These are often called **parallel edges** or **multiple edges**.

The final relaxation is to allow edges that connect a vertex to itself. An edge of the form $\{v, v\}$ is called a **loop**. A graph that permits both multiple edges and loops is known as a **[pseudograph](@entry_id:273987)**. In the context of this text, we will adhere to a common convention that distinguishes these types:
-   **Simple Graph**: No loops, no multiple edges.
-   **Multigraph**: Multiple edges are allowed, but loops are not.
-   **Pseudograph**: Both multiple edges and loops are allowed.

This hierarchy implies that every [simple graph](@entry_id:275276) is a [multigraph](@entry_id:261576), and every [multigraph](@entry_id:261576) is a [pseudograph](@entry_id:273987). The most fundamental feature that separates these broader classes from [simple graphs](@entry_id:274882) is the presence of either a loop or a parallel edge. In fact, the structurally simplest graph that is *not* simple is a [pseudograph](@entry_id:273987) consisting of a single vertex and a single loop attached to it [@problem_id:1400588]. If we were to design a [cost function](@entry_id:138681) for a graph, say $S = 5|V| + 2|E|$, the minimal cost for a non-simple graph is achieved by this very structure: a single vertex ($|V|=1$) with one loop ($|E|=1$), yielding a cost of $S = 5(1) + 2(1) = 7$. Any non-[simple graph](@entry_id:275276) based on multiple edges would require at least two vertices and two edges, resulting in a higher cost [@problem_id:1519596].

### Redefining Fundamental Properties

The introduction of loops and multiple edges requires us to revisit one of the most basic properties of a vertex: its degree.

#### Vertex Degree in Pseudographs

The **degree** of a vertex $v$, denoted $\deg(v)$, is defined as the number of edge-ends incident to it. This definition remains consistent, but its application to loops warrants careful consideration.
-   An edge connecting two distinct vertices, $u$ and $v$, has two ends: one incident to $u$ and one to $v$. It therefore contributes 1 to $\deg(u)$ and 1 to $\deg(v)$.
-   A **loop** at a vertex $v$ is an edge with both of its ends incident to $v$. Consequently, a loop contributes 2 to the degree of its vertex.

This convention is not arbitrary; it is essential for preserving the logical consistency of core graph theorems. For instance, consider a network of researchers where edges represent collaborations and loops represent solo-authored papers with heavy self-citation. If a researcher at vertex $v_3$ has one collaborative paper with $v_2$, one with $v_4$, and has published one solo paper (a loop), their degree is not 3, but $1 + 1 + 2 = 4$ [@problem_id:1519568].

#### The Handshaking Lemma Revisited

One of the cornerstones of graph theory is the **Handshaking Lemma**, which states that the sum of the degrees of all vertices in a graph is equal to twice the number of edges:
$$ \sum_{v \in V} \deg(v) = 2|E| $$
This theorem holds for [simple graphs](@entry_id:274882), multigraphs, and pseudographs without any modification, provided we use the degree definition where loops contribute 2. The proof remains elegant and intuitive: every edge, whether it connects two different vertices or a single vertex to itself, has exactly two ends. The sum of degrees, $\sum \deg(v)$, is simply a way of counting all edge-ends in the graph, one vertex at a time. Since each of the $|E|$ edges contributes exactly two such ends, the total count must be $2|E|$.

This relationship is remarkably useful. Imagine a research institute where the sum of degrees across all 20 researchers is found to be 118. If we know that 23 loops exist (representing solo papers with self-citation), we can deduce the total number of edges in the network is $|E| = 118/2 = 59$. Subtracting the 23 loops reveals that there must have been $59 - 23 = 36$ distinct collaborative publications between pairs of researchers [@problem_id:1519593] [@problem_id:1519616].

### Representing Multigraphs and Pseudographs

To work with these more general graphs computationally, we must adapt our standard [matrix representations](@entry_id:146025).

#### The Adjacency Matrix

For a [simple graph](@entry_id:275276), the [adjacency matrix](@entry_id:151010) $A$ is a binary matrix where $A_{ij}=1$ if an edge connects vertices $v_i$ and $v_j$, and 0 otherwise. For multigraphs and pseudographs, this representation naturally extends by allowing entries to be non-negative integers.

The entry $A_{ij}$ of the **adjacency matrix** of a [pseudograph](@entry_id:273987) is defined as the number of edges connecting vertices $v_i$ and $v_j$.
-   If $i \neq j$, $A_{ij}$ is the number of parallel edges between $v_i$ and $v_j$.
-   The diagonal entry $A_{ii}$ is the number of loops at vertex $v_i$.

This representation is simple yet powerful. For example, a key diagnostic feature becomes immediately apparent. A network, such as a data center where servers can send diagnostic data to themselves, contains a loop if and only if at least one server $v_i$ has a self-connection. This corresponds directly to the matrix entry $A_{ii}$ being greater than 0. Consequently, we can determine if a graph has any loops at all by examining the sum of its diagonal entries, known as the **trace** of the matrix. A [pseudograph](@entry_id:273987) has at least one loop if and only if $\text{Tr}(A) > 0$ [@problem_id:1519564].

The [adjacency matrix](@entry_id:151010) also provides a profound tool for analyzing connectivity. A celebrated result in [algebraic graph theory](@entry_id:274338) states that the $(i, j)$-th entry of the $k$-th power of the [adjacency matrix](@entry_id:151010), $(A^k)_{ij}$, gives the number of distinct **walks of length $k$** from vertex $v_i$ to vertex $v_j$. This property holds perfectly for pseudographs.

Consider a communication network with three nodes (N1, N2, N3) and various connections, including a loop at N1, two links between N1 and N2, one between N1 and N3, and three between N2 and N3. Its adjacency matrix would be:
$$ A = \begin{pmatrix} 1 & 2 & 1 \\ 2 & 0 & 3 \\ 1 & 3 & 0 \end{pmatrix} $$
To find the number of paths of length 4 that start and end at N1, we need only compute the matrix $A^4$ and look at the entry $(A^4)_{11}$. This calculation, though tedious by hand, is straightforward for a computer and reveals the answer to be 110, a result that would be extremely difficult to obtain by manual enumeration [@problem_id:1519604].

#### The Incidence Matrix

An alternative representation is the **[incidence matrix](@entry_id:263683)** $M$, whose rows are indexed by vertices and columns by edges. For a simple graph, $M_{ie} = 1$ if vertex $v_i$ is an endpoint of edge $e$, and 0 otherwise. Each column for a non-loop edge has exactly two 1s.

To accommodate pseudographs, this definition is typically modified for loops. If an edge $e_j$ is a loop at vertex $v_i$, its corresponding column in the [incidence matrix](@entry_id:263683) will have a single non-zero entry: a 2 in the row for $v_i$. An entry of 1 is used for non-loop edges. Formally:
$$ M_{ij} = \begin{cases} 2 & \text{if edge } e_j \text{ is a loop at vertex } v_i \\ 1 & \text{if edge } e_j \text{ is not a loop and is incident on } v_i \\ 0 & \text{otherwise} \end{cases} $$
With this convention, the sum of the entries in any row of the [incidence matrix](@entry_id:263683) is equal to the degree of the corresponding vertex [@problem_id:1519568]. This provides a beautiful consistency between the geometric concept of degree and the algebraic properties of the matrix representation.

### Impact on Advanced Graph Properties

The inclusion of loops and multiple edges has significant implications for more advanced graph-theoretic concepts. Some properties extend gracefully, while others break down or require careful re-evaluation.

#### Eulerian Circuits

An **Eulerian circuit** is a trail in a graph that visits every edge exactly once and starts and ends at the same vertex. A cornerstone theorem states that a connected graph has an Eulerian circuit if and only if every vertex has an even degree. This theorem extends seamlessly to connected pseudographs. The reasoning is identical: to traverse the graph, every time we enter a vertex through an edge, we must be able to leave it through a different, unused edge. This pairs up the edge-ends at each vertex. A loop represents a self-contained trip from a vertex and back, adding 2 to the degree and thus preserving its parity.

This principle is of great practical importance. For a transit authority designing a bus network, an Eulerian circuit corresponds to a "comprehensive tour" that covers every route segment exactly once. To ensure such a tour is possible, the network designers must ensure that the degree of every junction is an even number [@problem_id:1519551].

#### Bipartite Graphs

In contrast to Eulerian circuits, the concept of a **[bipartite graph](@entry_id:153947)** is fundamentally incompatible with loops. A graph is bipartite if its vertices can be partitioned into two [disjoint sets](@entry_id:154341), $U$ and $V$, such that every edge connects a vertex in $U$ to one in $V$.

A graph containing a loop cannot be bipartite. The most [direct proof](@entry_id:141172) relies solely on this definition. Let $v$ be a vertex with a loop. In any potential bipartition $(U, V)$, the vertex $v$ must belong to either $U$ or $V$.
-   If $v \in U$, the loop $(v, v)$ is an edge with both endpoints in $U$.
-   If $v \in V$, the loop $(v, v)$ is an edge with both endpoints in $V$.
In either case, the condition that every edge must connect a vertex in $U$ to one in $V$ is violated. Therefore, no such bipartition is possible [@problem_id:1519613]. An alternative perspective is that a loop is a cycle of length 1. Since a graph is bipartite if and only if it contains no odd-length cycles, and 1 is an odd number, the presence of a loop immediately disqualifies the graph.

#### The Challenge of Graph Complements

Finally, extending operations from [simple graphs](@entry_id:274882) to multigraphs is not always straightforward. Consider the **complement** of a simple graph $G$, denoted $\bar{G}$, where an edge exists in $\bar{G}$ if and only if it does not exist in $G$. This operation is an **involution**, meaning that the complement of the complement is the original graph: $\overline{\bar{G}} = G$.

How could we define a complement for a [multigraph](@entry_id:261576)? The simple binary logic of an edge's existence or non-existence is replaced by a [multiplicity](@entry_id:136466), $\mu(u, v) \in \{0, 1, 2, ...\}$. What does it mean to "complement" a [multiplicity](@entry_id:136466) of 5? A desirable property for any new definition is that it remains an [involution](@entry_id:203735).

Let's examine a few possibilities for defining the multiplicity of the complement, $\mu_{M^c}(u, v)$, based on the original multiplicity $\mu_M(u, v)$ [@problem_id:1519548].
-   One idea is to define the complement relative to the maximum [multiplicity](@entry_id:136466) $k_{max}$ in the graph: $\mu_{M^c}(u, v) = k_{max} - \mu_M(u, v)$. However, this fails the [involution](@entry_id:203735) test. The maximum [multiplicity](@entry_id:136466) of $M^c$ might be different from $k_{max}$, leading to $(M^c)^c \neq M$.
-   A more robust definition requires fixing an absolute upper bound $K$ for all multiplicities in the universe of graphs being considered. We can then define the complement relative to this fixed value: $\mu_{M^c}(u, v) = K - \mu_M(u, v)$. Applying the operation twice yields $\mu_{(M^c)^c}(u, v) = K - (K - \mu_M(u, v)) = \mu_M(u, v)$. This definition works perfectly.

This exploration shows that while loops and multiple edges enrich the modeling capabilities of graph theory, they also compel us to think more deeply about the fundamental assumptions underlying its definitions and theorems.