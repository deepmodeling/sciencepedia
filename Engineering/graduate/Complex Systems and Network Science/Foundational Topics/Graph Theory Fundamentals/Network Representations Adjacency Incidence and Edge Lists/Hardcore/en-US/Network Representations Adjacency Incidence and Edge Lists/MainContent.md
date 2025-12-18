## Introduction
Representing the intricate web of connections in a complex system is the first and most crucial step in network science. Whether mapping social ties, [gene interactions](@entry_id:275726), or transportation routes, the abstract structure of a graph must be translated into a concrete, computational format before any analysis can begin. However, this translation is not a neutral act; the choice of data structure—the language used to describe the network—profoundly influences analytical power, storage costs, and algorithmic efficiency. This article addresses the fundamental challenge of selecting the right representation by providing a detailed guide to the core methods used in network science.

Over the following chapters, you will gain a comprehensive understanding of these foundational tools. The journey begins in **Principles and Mechanisms**, where we formally define the [adjacency matrix](@entry_id:151010), incidence matrix, and edge list, exploring their mathematical properties and the trade-offs they entail. Next, **Applications and Interdisciplinary Connections** demonstrates how these representations are deployed to solve real-world problems in computer science, biology, and machine learning, highlighting the link between representation choice and scientific insight. Finally, **Hands-On Practices** will provide opportunities to implement these concepts, solidifying your ability to work with network data effectively.

## Principles and Mechanisms

To analyze and model complex systems as networks, we must first translate the abstract structure of a graph into a concrete, computationally tractable format. A graph, formally a pair $G=(V, E)$ consisting of a set of vertices $V$ and a collection of edges $E$ that connect them, can be represented in several ways. The choice of representation is not merely a matter of convention; it has profound implications for algorithmic efficiency, storage requirements, and the types of questions that can be answered easily. This chapter details the principles and mechanisms of the most fundamental network representations: the [adjacency matrix](@entry_id:151010), the incidence matrix, and the edge list. We will explore their formal definitions, their relationships to one another, and the practical trade-offs they entail.

A critical preliminary concept is the distinction between a vertex's intrinsic identity (its **label**, e.g., "Server A," a person's name, a specific protein) and the index it is assigned in a [data structure](@entry_id:634264). Matrix representations, for instance, rely on integer indices for their rows and columns. Therefore, to reconstruct a labeled graph from such a representation, one needs not only the matrix itself but also a mapping that connects these indices back to the meaningful vertex labels. As we will see, this mapping, a [bijection](@entry_id:138092) $\ell: V \to \{1, \dots, |V|\}$, is the essential link between the abstract graph and its concrete encoding . Changing this labeling function alters the representation, and understanding how these representations transform is key to identifying true [graph invariants](@entry_id:262729).

### The Adjacency Matrix: A Vertex-Centric View

The **[adjacency matrix](@entry_id:151010)** is arguably the most common [matrix representation](@entry_id:143451) of a graph. For a graph with $n = |V|$ vertices, the [adjacency matrix](@entry_id:151010) $A$ is an $n \times n$ square matrix where the entry $A_{ij}$ encodes the relationship between the vertex with index $i$ and the vertex with index $j$. The precise nature of this encoding depends on the type of graph being represented .

#### Formal Definitions for Graph Variants

Let us systematically define the [adjacency matrix](@entry_id:151010) for various graph types.

For a **simple undirected graph** (no self-loops, no parallel edges), the adjacency matrix $A$ is a binary matrix where $A_{ij} = 1$ if an edge exists between vertices $i$ and $j$, and $A_{ij} = 0$ otherwise. By this definition, the matrix must be **symmetric** (i.e., $A_{ij} = A_{ji}$ for all $i,j$, so $A = A^{\top}$) because an undirected edge between $i$ and $j$ is the same as an edge between $j$ and $i$. Furthermore, the absence of self-loops means all diagonal entries are zero ($A_{ii} = 0$). These properties correspond directly to the formal definition of the edge set $E$ as an irreflexive, symmetric relation on the vertex set $V$ .

For a **simple [directed graph](@entry_id:265535)**, or **[digraph](@entry_id:276959)**, where edges have orientation (e.g., $i \to j$), the entry $A_{ij}$ is $1$ if a directed edge exists from $i$ to $j$, and $0$ otherwise. An edge from $i$ to $j$ does not imply an edge from $j$ to $i$, so the matrix $A$ is **not necessarily symmetric**. The absence of self-loops still implies a zero diagonal ($A_{ii}=0$). The underlying edge set $E \subseteq V \times V$ is simply an irreflexive relation .

When edges have **weights**, captured by a function $w: E \to \mathbb{R}$, the adjacency matrix is generalized to store these weights. The entry $A_{ij}$ becomes the weight of the edge $(i, j)$, or zero if no such edge exists.

For **multigraphs**, which permit multiple parallel edges between the same two vertices, the [adjacency matrix](@entry_id:151010) typically stores the *number* of edges. For an unweighted [multigraph](@entry_id:261576), $A_{ij}$ is the integer count of edges between $i$ and $j$. For a weighted [multigraph](@entry_id:261576), $A_{ij}$ is often the *sum* of the weights of all parallel edges between $i$ and $j$. This aggregation is a key feature of the adjacency [matrix representation](@entry_id:143451): it provides a compact summary but loses the individual identities and attributes of parallel edges .

**Self-loops**, edges that connect a vertex to itself, are represented by non-zero diagonal entries. In a [directed graph](@entry_id:265535) with a [self-loop](@entry_id:274670) at vertex $i$, $A_{ii}$ would be 1 (or the loop's weight). In undirected multigraphs, a common convention is to set $A_{ii}$ to be *twice* the number of self-loops at vertex $i$. This convention is mathematically convenient because it preserves a fundamental relationship between the [adjacency matrix](@entry_id:151010) and vertex degrees, as we shall see next.

#### Deriving Properties: Vertex Degrees

The **degree** of a vertex is one of the most basic and important network measures. The [adjacency matrix](@entry_id:151010) provides a straightforward way to compute it. For a [directed graph](@entry_id:265535), we distinguish between [in-degree and out-degree](@entry_id:273421).

The **[out-degree](@entry_id:263181)** of a vertex $i$, $k^{\text{out}}_i$, is the number of edges originating from it. Based on the definition of $A$, each edge $i \to j$ corresponds to a non-zero entry $A_{ij}$. Summing across the $i$-th row of $A$ counts all outgoing edges. Thus, the out-degree is the row sum:
$$k^{\text{out}}_{i} = \sum_{j=1}^{n} A_{ij}$$
The **in-degree** of a vertex $i$, $k^{\text{in}}_i$, is the number of edges terminating at it. Each edge $j \to i$ corresponds to a non-zero entry $A_{ji}$. Summing down the $i$-th column of $A$ counts all incoming edges. Thus, the in-degree is the column sum:
$$k^{\text{in}}_{i} = \sum_{j=1}^{n} A_{ji}$$

These relationships can be derived directly from first principles . Consider a directed graph on vertices $V=\{1,2,3,4,5,6\}$ with edges $E=\{1\to 2, 1\to 3, 2\to 3, 2\to 2, 3\to 1, 3\to 4, 4\to 5, 5\to 4, 5\to 6, 6\to 3\}$. Its [adjacency matrix](@entry_id:151010) is:
$$A = \begin{pmatrix}
0  & 1 & 1 & 0 & 0 & 0 \\
0  & 1 & 1 & 0 & 0 & 0 \\
1  & 0 & 0 & 1 & 0 & 0 \\
0  & 0 & 0 & 0 & 1 & 0 \\
0  & 0 & 0 & 1 & 0 & 1 \\
0  & 0 & 1 & 0 & 0 & 0
\end{pmatrix}$$
The [out-degree](@entry_id:263181) of vertex 1 is the sum of its row, $0+1+1+0+0+0 = 2$. The in-degree of vertex 3 is the sum of its column, $1+1+0+0+0+1 = 3$. This simple algebraic calculation is a powerful feature of the [adjacency matrix](@entry_id:151010). In vector notation, the [out-degree](@entry_id:263181) vector is given by $A \mathbf{1}$ and the in-degree vector by $A^{\top} \mathbf{1}$, where $\mathbf{1}$ is the all-ones vector. For an undirected graph (where $A=A^\top$), the degree vector is simply $A \mathbf{1}$.

#### Special Structures: Bipartite Graphs

The structure of the adjacency matrix elegantly reflects the underlying structure of the graph. A prime example is a **[bipartite graph](@entry_id:153947)**, where the vertex set $V$ can be partitioned into two [disjoint sets](@entry_id:154341), $U$ and $V_p$ (we use $V_p$ to avoid confusion with the main vertex set $V$), such that every edge connects a vertex in $U$ to one in $V_p$. There are no edges *within* $U$ or $V_p$.

If we label the vertices such that all $|U| = m$ vertices of $U$ come first, followed by all $|V_p|=n$ vertices of $V_p$, the adjacency matrix $A$ takes on a specific block structure. The blocks corresponding to intra-set connections must be zero matrices. The connections between $U$ and $V_p$ are captured by an $m \times n$ **[biadjacency matrix](@entry_id:1121539)**, $B$, where $B_{ij}=1$ if an edge exists between the $i$-th vertex of $U$ and the $j$-th vertex of $V_p$. For an [undirected graph](@entry_id:263035), this results in the [adjacency matrix](@entry_id:151010):
$$A = \begin{pmatrix} 0_{m \times m}  & B \\ B^{\top}  & 0_{n \times n} \end{pmatrix}$$
This structure has significant algebraic consequences. For instance, the eigenvalues of $A$ are directly related to the singular values of the much smaller [biadjacency matrix](@entry_id:1121539) $B$, a fact that is computationally very useful .

### The Incidence Matrix: An Edge-Centric View

While the [adjacency matrix](@entry_id:151010) focuses on relationships between vertices, the **[incidence matrix](@entry_id:263683)** describes the graph from the perspective of its edges, specifying which vertices each edge is incident to. For a graph with $n$ vertices and $m$ edges, the incidence matrix is an $n \times m$ matrix. Its properties depend on whether it encodes direction.

The **unsigned [incidence matrix](@entry_id:263683)**, denoted $C$, is typically used for [undirected graphs](@entry_id:270905). Its entries are defined as $C_{ve} = 1$ if vertex $v$ is an endpoint of edge $e$, and $C_{ve} = 0$ otherwise. For any edge $e$ that is not a [self-loop](@entry_id:274670), its corresponding column in $C$ will have exactly two non-zero entries (both 1), identifying its two endpoints. This representation is inherently orientation-agnostic .

The **signed [incidence matrix](@entry_id:263683)**, denoted $B$, is used to encode direction. For each edge $e$, a direction is specified (either intrinsically for a [digraph](@entry_id:276959), or arbitrarily for an [undirected graph](@entry_id:263035)). The entries are then defined as:
$$B_{ve} = \begin{cases} +1  &\text{if } v \text{ is the head of edge } e \\ -1  &\text{if } v \text{ is the tail of edge } e \\ 0  &\text{otherwise} \end{cases}$$
Each column corresponding to a non-loop edge has exactly two non-zero entries, a $+1$ and a $-1$. The locations of these entries identify the endpoints, and their signs uniquely specify the edge's orientation. Reversing the chosen orientation of an edge simply multiplies its corresponding column vector by $-1$, leaving the endpoint information intact .

#### The Special Case of Self-Loops

Self-loops present a unique and important case for the [incidence matrix](@entry_id:263683). Consider a [self-loop](@entry_id:274670) edge $e$ at vertex $v$. For the unsigned matrix $C$, the column for $e$ would have a single non-zero entry, $C_{ve}$, which is often set to 2 to maintain the property that column sums equal 2.

For the signed matrix $B$, vertex $v$ is simultaneously the head and the tail of the [self-loop](@entry_id:274670). Applying the definition, the entry $B_{ve}$ would be the sum of the contributions for being a head $(+1)$ and a tail $(-1)$, resulting in $B_{ve} = 1 - 1 = 0$. All other entries in that column are also zero. Therefore, a [self-loop](@entry_id:274670) corresponds to an **all-zero column** in the signed [incidence matrix](@entry_id:263683). This has a profound consequence: self-loops are "invisible" to any formulation built purely on the signed [incidence matrix](@entry_id:263683), such as the standard graph Laplacian expression $L = B B^{\top}$ .

### The Edge List: A Direct Enumeration

The **edge list** is the most direct and often most flexible [graph representation](@entry_id:274556). It is simply a collection of all the edges in the graph. For a graph with $m$ edges, the list will have $m$ entries. Each entry describes one edge by specifying its endpoints, and optionally, its weight or other attributes.

-   In a **simple undirected graph**, the edge list is a set of unordered pairs $\{u, v\}$.
-   In a **simple [directed graph](@entry_id:265535)**, it is a set of [ordered pairs](@entry_id:269702) $(u, v)$.
-   For **[weighted graphs](@entry_id:274716)**, each entry becomes a triplet, such as $(u, v, w)$, where $w$ is the edge weight.

The primary strength of the edge list becomes apparent with **multigraphs**. An [adjacency matrix](@entry_id:151010) must aggregate parallel edges into a single number, losing information about their individual properties. An edge list, being a list or multiset rather than a set, can simply contain duplicate entries. For example, two parallel directed edges from $u$ to $v$ would appear as two separate $(u, v)$ entries in the list. This makes the edge list a lossless representation. To guarantee that each edge can be uniquely identified and carry its own attributes (like distinct capacities in a [flow network](@entry_id:272730)), the most robust formalization is a list of records, where each record contains a unique edge identifier, its endpoints, and any associated attributes [@problem_id:4291950, @problem_id:4291942]. Self-loops are naturally represented as pairs with identical endpoints, e.g., $(u, u)$.

### Synthesis and Comparison

Each representation has its strengths and weaknesses, making the choice dependent on the specific graph properties and the computational tasks at hand.

#### Information Content and Isomorphism

As mentioned initially, [matrix representations](@entry_id:146025) depend on an arbitrary vertex labeling. If we change the labeling, say from $\ell$ to $\ell'$, the [adjacency matrix](@entry_id:151010) transforms via a **[permutation matrix](@entry_id:136841)** $P$. If $A$ is the matrix under labeling $\ell$, the new matrix $A'$ under $\ell'$ is given by $A' = P A P^{\top}$ (or, equivalently, $A' = P^{-1} A P$, since $P^{-1}=P^\top$ for permutation matrices) . This is a **[similarity transformation](@entry_id:152935)**. A crucial property of similarity transformations is that they preserve the matrix's eigenvalues. This means the spectrum (the multiset of eigenvalues) of the [adjacency matrix](@entry_id:151010) is a **[graph invariant](@entry_id:274470)**—it does not depend on the arbitrary labeling of vertices, but only on the graph's intrinsic structure. This makes spectral graph theory a powerful tool for analyzing networks.

#### Computational Trade-offs

The choice of data structure has significant consequences for the efficiency of common [graph algorithms](@entry_id:148535). Consider a graph with $N$ vertices and $M$ edges .

-   **Finding an edge $(u,v)$:** The [adjacency matrix](@entry_id:151010) excels here, offering $O(1)$ access time. An edge list requires, in the worst case, scanning the entire list, taking $O(M)$ time.
-   **Iterating over neighbors of a vertex $u$:** Using an adjacency matrix, one must scan an entire row, which takes $O(N)$ time, regardless of how many neighbors the vertex actually has. For an edge list, one must again scan the whole list, taking $O(M)$ time. (In practice, edge lists are often converted to **adjacency lists**, which optimize this operation to be proportional to the vertex's degree).
-   **Calculating the degree sequence:** As analyzed in , the complexities differ dramatically.
    -   With a dense **adjacency matrix**, we must sum each of the $N$ rows, each of length $N$, leading to a $\Theta(N^2)$ complexity, regardless of how many edges the graph has.
    -   With an **edge list**, we can initialize an array of degree counters in $\Theta(N)$ time and then iterate through the $M$ edges, incrementing the counters for the two endpoints of each edge. This gives a total complexity of $\Theta(N+M)$.
    -   With a dense **incidence matrix**, one must iterate through all $N \times M$ entries, leading to a $\Theta(NM)$ complexity.

This analysis reveals a fundamental dichotomy. For **dense graphs**, where $M$ is on the order of $N^2$, the $\Theta(N^2)$ complexity of the adjacency matrix is efficient. For **sparse graphs**, which are common in real-world applications and where $M$ is closer to $N$, the $\Theta(N+M)$ complexity of the edge list is vastly superior.

#### The Role of Self-Loops in Network Dynamics

Finally, we return to the subtle role of self-loops. As we saw, a [self-loop](@entry_id:274670) corresponds to a zero column in the signed incidence matrix and its contribution to the [out-degree](@entry_id:263181) and adjacency matrix diagonals cancel out in the directed out-degree Laplacian, $\mathbf{L} = \mathbf{D}_{\mathrm{out}} - \mathbf{A}$ . This means that for static [structural analysis](@entry_id:153861) based on the Laplacian, such as [spectral clustering](@entry_id:155565) or computing the number of [connected components](@entry_id:141881), self-loops are often irrelevant.

However, they are critically important for **dynamic processes** on networks. Consider a random walk on a [directed graph](@entry_id:265535), where the probability of moving from vertex $i$ to vertex $j$ is given by the transition matrix $\mathbf{P} = \mathbf{D}_{\mathrm{out}}^{-1}\mathbf{A}$. A [self-loop](@entry_id:274670) at vertex $i$ of weight $w$ increases both its out-degree $d_{\mathrm{out}}(i)$ and the diagonal entry $A_{ii}$. This directly increases the "holding probability" $P_{ii} = A_{ii} / d_{\mathrm{out}}(i)$, the chance that the walker stays at vertex $i$ in the next step. This change can significantly alter the [stationary distribution](@entry_id:142542) of the walk and its [mixing time](@entry_id:262374), demonstrating that information ignored by one representation or analytical tool can be vital for another . This illustrates a core principle: the best representation depends entirely on the questions being asked of the network.