## Introduction
While graphs provide an intuitive visual way to understand relationships, their true analytical power is realized when we represent their structure algebraically. This article introduces the two cornerstone methods for this translation: the adjacency matrix and the [incidence matrix](@entry_id:263683). By encoding connectivity into these matrix forms, we move beyond simple diagrams and unlock the vast analytical toolkit of linear algebra, enabling us to solve complex network problems that are intractable by visual inspection alone. The reader will gain a comprehensive understanding of how to represent graphs mathematically and leverage these representations for powerful analysis. The journey begins in "Principles and Mechanisms," where we define adjacency and incidence matrices and explore their fundamental properties, such as the profound link between [matrix powers](@entry_id:264766) and path counting. Next, "Applications and Interdisciplinary Connections" will demonstrate how these concepts are applied across diverse fields, from [computational biology](@entry_id:146988) to quantum mechanics. Finally, "Hands-On Practices" will offer exercises to solidify these theoretical concepts through practical application.

## Principles and Mechanisms

While visual representations of graphs are intuitive, their true power in systematic analysis is unlocked when we translate their structure into the language of linear algebra. By encoding a graph's connectivity into matrices, we can leverage the vast toolkit of [matrix theory](@entry_id:184978) to uncover deep and often non-obvious properties of the network. This chapter explores the two most fundamental [matrix representations](@entry_id:146025) of a graph: the adjacency matrix and the [incidence matrix](@entry_id:263683). We will define these matrices, investigate their properties, and reveal the profound connection between matrix operations and graph-theoretic concepts like paths, degrees, and structural classifications.

### The Adjacency Matrix: Encoding Connectivity

The most common algebraic representation of a graph is its **[adjacency matrix](@entry_id:151010)**. This square matrix acts as a direct lookup table for connections between pairs of vertices. Its definition, however, must be adapted to the type of graph being studied.

#### Simple Undirected Graphs

Let $G = (V, E)$ be a simple [undirected graph](@entry_id:263035) with $n$ vertices, labeled $v_1, v_2, \dots, v_n$. The **adjacency matrix** $A$ of $G$ is an $n \times n$ matrix whose entries $A_{ij}$ are defined as:

$$
A_{ij} = \begin{cases} 1  \text{if } \{v_i, v_j\} \in E \\ 0  \text{otherwise} \end{cases}
$$

By this definition, the matrix $A$ has several immediate and important properties. First, since [simple graphs](@entry_id:274882) do not have loops (edges from a vertex to itself), the diagonal entries are always zero: $A_{ii} = 0$ for all $i$. Second, the nature of an undirected edge is inherently reciprocal: if $v_i$ is connected to $v_j$, then $v_j$ is connected to $v_i$. This physical property of the graph imposes a strict mathematical constraint on its [adjacency matrix](@entry_id:151010). For any pair of indices $i$ and $j$, $A_{ij} = 1$ if and only if $A_{ji} = 1$. This means the matrix is always equal to its transpose, i.e., $A = A^T$. Any [adjacency matrix](@entry_id:151010) of a simple [undirected graph](@entry_id:263035) must be **symmetric**. This symmetry is a guaranteed consequence of the reciprocal nature of connections, a principle seen in many real-world networks like mutual social connections or bidirectional data links [@problem_id:1478859].

#### Directed Graphs

For a directed graph, or **[digraph](@entry_id:276959)**, where edges have a specific orientation, the [adjacency matrix](@entry_id:151010) definition is slightly modified to capture this directionality. For a [digraph](@entry_id:276959) $G = (V, E)$ with $n$ vertices, the entry $A_{ij}$ is defined as:

$$
A_{ij} = \begin{cases} 1  \text{if } (v_i, v_j) \in E \\ 0  \text{otherwise} \end{cases}
$$

Here, an entry $A_{ij} = 1$ signifies an edge *from* $v_i$ *to* $v_j$. Unlike the undirected case, the existence of an edge $(v_i, v_j)$ does not imply the existence of an edge $(v_j, v_i)$. Consequently, the adjacency matrix of a directed graph is **not generally symmetric**.

This matrix representation provides a straightforward way to calculate two crucial properties of a vertex in a [digraph](@entry_id:276959): its [in-degree and out-degree](@entry_id:273421). In a social network context, for instance, where an edge $(v_i, v_j)$ means user $v_i$ follows user $v_j$, the out-degree and in-degree correspond to the number of users one follows and the number of followers one has, respectively [@problem_id:1478854].

The **[out-degree](@entry_id:263181)** of a vertex $v_i$, denoted $d_{\text{out}}(v_i)$, is the number of edges originating from it. This corresponds to summing the entries across the $i$-th row of the adjacency matrix:
$$
d_{\text{out}}(v_i) = \sum_{j=1}^{n} A_{ij}
$$

The **in-degree** of a vertex $v_j$, denoted $d_{\text{in}}(v_j)$, is the number of edges terminating at it. This is found by summing the entries down the $j$-th column:
$$
d_{\text{in}}(v_j) = \sum_{i=1}^{n} A_{ij}
$$

#### Generalization to Multigraphs

The adjacency matrix concept can be extended to **multigraphs**, where multiple edges may exist between the same pair of vertices. For a [multigraph](@entry_id:261576), the entry $A_{ij}$ is defined as the **number of edges** connecting vertices $v_i$ and $v_j$. For an undirected [multigraph](@entry_id:261576), the matrix remains symmetric.

This definition elegantly connects to a foundational result in graph theory: the [handshaking lemma](@entry_id:261183). The [degree of a vertex](@entry_id:261115) $v_i$ in a [multigraph](@entry_id:261576) is the sum of entries in its corresponding row (or column), $d(v_i) = \sum_{j=1}^{n} A_{ij}$. The sum of all entries in the adjacency matrix is therefore the sum of the degrees of all vertices: $\sum_{i=1}^{n} \sum_{j=1}^{n} A_{ij} = \sum_{i=1}^{n} d(v_i)$. The [handshaking lemma](@entry_id:261183) states that this sum is equal to twice the total number of edges, $m$. Thus, the sum of all elements in the adjacency matrix of an undirected [multigraph](@entry_id:261576) is always $2m$ [@problem_id:1478867].

### Uncovering Structure through Matrix Powers: The Algebra of Walks

The true analytical power of the adjacency matrix is revealed when we consider its powers. Matrix multiplication, a simple algebraic operation, corresponds to the intricate graph-theoretic concept of "walks." A **walk** of length $k$ from a vertex $u$ to a vertex $w$ is a sequence of vertices $v_0, v_1, \dots, v_k$ such that $v_0 = u$, $v_k = w$, and $\{v_{i-1}, v_i\}$ is an edge for all $i=1, \dots, k$. Vertices and edges may be revisited.

The central theorem connecting algebra and graph walks is as follows:

For any graph with [adjacency matrix](@entry_id:151010) $A$, the entry $(i, j)$ of the matrix $A^k$ gives the number of distinct walks of length $k$ from vertex $v_i$ to vertex $v_j$.

We can understand this theorem through induction. The base case $k=1$ is true by the definition of $A$. For the [inductive step](@entry_id:144594), assume $(A^k)_{ij}$ counts the walks of length $k$. A walk of length $k+1$ from $v_i$ to $v_j$ consists of a walk of length $k$ from $v_i$ to some intermediate vertex $v_p$, followed by a single step from $v_p$ to $v_j$. To find the total number of such walks, we must sum over all possible penultimate vertices $v_p$:

$$
(\text{Walks of length } k+1 \text{ from } v_i \text{ to } v_j) = \sum_{p=1}^{n} (\text{Walks of length } k \text{ from } v_i \text{ to } v_p) \times (\text{Walks of length } 1 \text{ from } v_p \text{ to } v_j)
$$

This translates directly into the definition of matrix multiplication:
$$
(A^{k+1})_{ij} = (A^k A)_{ij} = \sum_{p=1}^{n} (A^k)_{ip} A_{pj}
$$
This powerful result means that counting complex path combinations in a network, such as multi-hop data packet routes, can be accomplished by simply computing a matrix power [@problem_id:1478868].

#### Interpreting Low-Order Powers

The first few powers of $A$ provide particularly accessible insights.

For $A^2$, the off-diagonal entry $(A^2)_{ij}$ for $i \neq j$ counts the number of walks of length 2 from $v_i$ to $v_j$. Such a walk must be of the form $v_i \to v_p \to v_j$. The number of such walks is precisely the number of vertices $v_p$ that are adjacent to both $v_i$ and $v_j$, i.e., the number of **[common neighbors](@entry_id:264424)**.

The diagonal entry $(A^2)_{ii}$ counts the number of walks of length 2 that start and end at $v_i$. For a [simple graph](@entry_id:275276), such a walk is $v_i \to v_j \to v_i$, where $v_j$ must be a neighbor of $v_i$. The number of choices for $v_j$ is, by definition, the degree of $v_i$. Thus, for a simple graph, the diagonal entries of $A^2$ list the degrees of the vertices: $(A^2)_{ii} = \deg(v_i)$ [@problem_id:1478852].

For $A^3$, the diagonal entry $(A^3)_{ii}$ gives the number of closed walks of length 3 starting and ending at $v_i$. A walk $v_i \to v_j \to v_k \to v_i$ in a [simple graph](@entry_id:275276) requires $v_i, v_j, v_k$ to be distinct, forming a triangle. Each triangle involving $v_i$ gives rise to two such walks ($v_i \to v_j \to v_k \to v_i$ and $v_i \to v_k \to v_j \to v_i$). Therefore, $(A^3)_{ii}$ is equal to twice the number of triangles containing vertex $v_i$. For a complete graph $K_n$, where every vertex is connected to every other vertex, a 3-hop round trip from $v_i$ involves choosing a first hop to any of the $n-1$ other vertices, and a second hop to any of the remaining $n-2$ vertices, after which the return path is fixed. The total number of such walks is $(n-1)(n-2)$, which can be verified by computing $(A^3)_{ii}$ where $A$ is the [adjacency matrix](@entry_id:151010) for $K_n$ [@problem_id:1478851].

### The Incidence Matrix: A Vertex-Edge Perspective

An alternative way to represent a graph is through its **[incidence matrix](@entry_id:263683)**, which describes the relationship between vertices and edges. For a graph $G = (V, E)$ with $n$ vertices $\{v_1, \dots, v_n\}$ and $m$ edges $\{e_1, \dots, e_m\}$, the [incidence matrix](@entry_id:263683) $M$ is an $n \times m$ matrix defined as:

$$
M_{ie} = \begin{cases} 1  \text{if vertex } v_i \text{ is an endpoint of edge } e \\ 0  \text{otherwise} \end{cases}
$$

The structure of this matrix is dictated by the fundamental properties of edges.

*   Each edge in a simple graph connects exactly two distinct vertices. Consequently, every column of the [incidence matrix](@entry_id:263683) must contain exactly two non-zero entries (both 1s). A column with one 1 would imply a loop, which is not present in a [simple graph](@entry_id:275276) [@problem_id:1478863].

*   The sum of the entries in a row corresponding to vertex $v_i$ counts the number of edges for which $v_i$ is an endpoint. This is precisely the definition of the **degree** of vertex $v_i$ in an [undirected graph](@entry_id:263035) (without loops) [@problem_id:1478800]. Thus, $\deg(v_i) = \sum_{e \in E} M_{ie}$.

#### Relating Incidence and Adjacency

While the adjacency and incidence matrices offer different perspectives, they are deeply related. This relationship is revealed by the matrix product $P = MM^T$. Let's analyze the entries of this $n \times n$ matrix.

The diagonal entry $P_{ii}$ is given by the dot product of the $i$-th row of $M$ with itself:
$$
P_{ii} = (MM^T)_{ii} = \sum_{e \in E} M_{ie} M_{ie} = \sum_{e \in E} (M_{ie})^2
$$
Since the entries of $M$ are either 0 or 1, this sum is simply the number of 1s in the $i$-th row, which we already established is the degree of vertex $v_i$. So, $(MM^T)_{ii} = \deg(v_i)$.

The off-diagonal entry $P_{ij}$ for $i \neq j$ is given by the dot product of the $i$-th and $j$-th rows of $M$:
$$
P_{ij} = (MM^T)_{ij} = \sum_{e \in E} M_{ie} M_{je}
$$
A term $M_{ie} M_{je}$ in this sum is 1 if and only if both $M_{ie}=1$ and $M_{je}=1$, which means that edge $e$ is incident to both vertex $v_i$ and vertex $v_j$. The sum, therefore, counts the number of edges that directly connect $v_i$ and $v_j$.

Putting these facts together reveals a remarkable identity [@problem_id:1478837]. For a simple graph where there's at most one edge between any two vertices, the matrix product $MM^T$ yields a matrix whose diagonal entries are the vertex degrees and whose off-diagonal entry $(i, j)$ is 1 if an edge exists between $v_i$ and $v_j$, and 0 otherwise. This can be expressed compactly as:

$$
MM^T = D + A
$$

where $D$ is the [diagonal matrix](@entry_id:637782) of vertex degrees and $A$ is the [adjacency matrix](@entry_id:151010). The matrix $D+A$ is known as the **signless Laplacian matrix**, a significant object in [spectral graph theory](@entry_id:150398) that emerges naturally from the [incidence matrix](@entry_id:263683).

### Deeper Connections: Spectral Properties and Graph Structure

The connection between a graph's structure and the algebraic properties of its matrices runs deeper still, extending into the realm of eigenvalues and [spectral analysis](@entry_id:143718). One of the most elegant examples of this connection relates to bipartite graphs.

A graph is **bipartite** if its vertices can be divided into two disjoint and [independent sets](@entry_id:270749), $U$ and $W$, such that every edge connects a vertex in $U$ to one in $W$. A key property of [bipartite graphs](@entry_id:262451) is that they contain no cycles of odd length. This structural property has a direct consequence for walks: any walk in a [bipartite graph](@entry_id:153947) must alternate between vertices in $U$ and vertices in $W$. Therefore, a closed walk, which starts and ends at the same vertex, must take an even number of steps. There are no closed walks of odd length in a bipartite graph.

This brings us back to the powers of the adjacency matrix. The total number of closed walks of length $k$ in a graph is given by the sum of the diagonal entries of $A^k$, known as the **trace** of the matrix, $\text{tr}(A^k)$.

Because a bipartite graph has no closed walks of odd length, it must be that for any odd integer $k > 0$:
$$
\text{tr}(A^k) = 0
$$

This provides a powerful and purely algebraic test for bipartiteness. If the trace of all odd powers of a graph's adjacency matrix is zero, the graph must be bipartite [@problem_id:1478830]. This profound result exemplifies the core theme of this chapter: that [matrix representations](@entry_id:146025) do not merely store graph data, but transform combinatorial problems into algebraic ones, often revealing structure and properties in a surprisingly elegant and powerful fashion.