## Introduction
In the study of complex systems, understanding the organization of networks beyond individual nodes and edges is paramount. A recurring and fundamental pattern is the [core-periphery structure](@entry_id:1123066), where a dense, well-connected core is surrounded by a sparser, loosely attached periphery. Identifying this mesoscale architecture is crucial for understanding a system's resilience, function, and dynamics. However, pinpointing this structure requires specialized methods that go beyond simple local metrics like degree. This article addresses this need by providing a comprehensive guide to two powerful and computationally efficient techniques: [k-core](@entry_id:1126853) decomposition and its refinement, [onion decomposition](@entry_id:1129131). The following chapters will first delve into the theoretical **Principles and Mechanisms** behind these algorithms, establishing how they reveal a network's nested hierarchy. We will then explore their diverse **Applications and Interdisciplinary Connections**, demonstrating their utility in fields from [systems biology](@entry_id:148549) to infrastructure security. Finally, a series of **Hands-On Practices** will offer the opportunity to apply these concepts and solidify your understanding of how to analyze and interpret [core-periphery structure](@entry_id:1123066) in real-world contexts.

## Principles and Mechanisms

The analysis of [complex networks](@entry_id:261695) often begins with simple, node-level metrics but quickly advances toward understanding larger, collective patterns of organization known as mesoscale structures. Among the most fundamental of these is the concept of a nested hierarchy, where a central, densely connected **core** of nodes is surrounded by successive layers of less central, more sparsely connected nodes forming the **periphery**. This chapter details the principles and mechanisms of two powerful algorithmic techniques for revealing this structure: **k-core decomposition** and its refinement, **[onion decomposition](@entry_id:1129131)**. These methods provide a computationally efficient way to dissect a network into a hierarchy of subgraphs based on their internal connectivity and resilience.

### The [k-core](@entry_id:1126853) Decomposition: A Hierarchy of Resilience

The primary tool for identifying nested structure is the **[k-core](@entry_id:1126853) decomposition**. This method partitions a network into a set of nested subgraphs of increasing connectivity and stability.

#### Formal Definition: Coreness, Cores, and Shells

For a given simple, undirected graph $G = (V, E)$, the **[k-core](@entry_id:1126853)** is defined as the unique maximal [induced subgraph](@entry_id:270312) in which every vertex has a degree of at least $k$ *within that [subgraph](@entry_id:273342)*. The properties of maximality and uniqueness are critical and mathematically guaranteed .

*   **Maximality**: The term "maximal" is used in the context of set inclusion. If $G[S]$ is the vertex set of the $k$-core, it means there is no strict superset $T \supset S$ for which the [induced subgraph](@entry_id:270312) $G[T]$ also satisfies the [minimum degree](@entry_id:273557) condition. It is not maximal in terms of vertex or edge count in an absolute sense, but rather that it cannot be grown any further by adding vertices without violating the [minimum degree](@entry_id:273557) property.

*   **Uniqueness**: The $k$-core is unique for any given $k$ and graph $G$. This can be formally proven by noting that the collection of all vertex sets that induce a [subgraph](@entry_id:273342) with [minimum degree](@entry_id:273557) at least $k$ is closed under the operation of set union. If $S_1$ and $S_2$ both induce subgraphs with [minimum degree](@entry_id:273557) at least $k$, their union $S_1 \cup S_2$ will as well. Consequently, the union of *all* such vertex sets is the single largest set satisfying the property, making it the unique [maximal element](@entry_id:274677) .

This decomposition gives rise to two important node-level attributes:

1.  The **core number**, or **[coreness](@entry_id:1123067)**, $c(v)$ of a vertex $v$ is the highest integer $k$ such that $v$ is a member of the $k$-core. If a vertex has [coreness](@entry_id:1123067) $k$, it belongs to the $1$-core, $2$-core, ..., up to the $k$-core, but is not part of the $(k+1)$-core.

2.  The **k-shell** is the set of all vertices whose [coreness](@entry_id:1123067) is exactly $k$. The shells partition the vertices of the graph, $V = \bigcup_k S_k$.

The set of all $k$-cores forms a nested sequence: $... \subseteq C_{k+1} \subseteq C_k \subseteq ... \subseteq C_1 \subseteq G$. The core with the highest index is often called the **main core** or **innermost core** of the network.

#### Coreness versus Degree: A Crucial Distinction

A common misconception is to equate a node's [coreness](@entry_id:1123067) with its degree. While the two are related—a node's [coreness](@entry_id:1123067) can never exceed its degree, $c(v) \le d(v)$—they measure fundamentally different properties. Degree $d(v)$ is a purely local metric, counting a node's immediate neighbors. In contrast, [coreness](@entry_id:1123067) $c(v)$ is a non-local measure of resilience and influence, determined by whether a node is part of a robustly connected collective.

Consider a hypothetical network composed of two disconnected parts: a star graph with a central hub $v_h$ connected to $7$ leaf nodes, and a complete graph (a [clique](@entry_id:275990)) on $4$ nodes $\{v_a, v_b, v_c, v_d\}$ .

*   The hub $v_h$ has a high degree, $d(v_h)=7$. However, all of its neighbors are leaves with degree $1$. In the search for the $2$-core, all leaves are removed. This in turn leaves $v_h$ with a degree of $0$, causing it to be removed as well. Thus, $v_h$ is only part of the $1$-core, and its [coreness](@entry_id:1123067) is $c(v_h)=1$.

*   Node $v_a$ in the clique has a lower degree, $d(v_a)=3$. However, all of its neighbors are also part of the clique and are themselves connected to each other. This clique forms a stable $3$-core; no node will be removed until we search for the $4$-core. Therefore, the [coreness](@entry_id:1123067) of $v_a$ is $c(v_a)=3$.

This example starkly illustrates the principle: $d(v_h) > d(v_a)$ but $c(v_h)  c(v_a)$. A high degree is no guarantee of a high [coreness](@entry_id:1123067). The [coreness](@entry_id:1123067) of a node is determined not by how many neighbors it has, but by how resiliently connected its neighborhood is.

#### Graph Degeneracy

The k-core decomposition is deeply connected to a classic concept in graph theory known as **degeneracy**. The [degeneracy of a graph](@entry_id:261690) $G$, sometimes denoted $d(G)$, is the smallest integer $d$ such that every [induced subgraph](@entry_id:270312) of $G$ has at least one vertex of degree at most $d$.

There is a direct and important equivalence: the [degeneracy of a graph](@entry_id:261690) is equal to the highest index $k$ for which the $k$-core is non-empty . This value, $k_{max} = \max_v c(v)$, is also known as the [coreness](@entry_id:1123067) of the graph. This equivalence grounds the k-core decomposition in the fundamental structural properties of the graph, showing that the innermost core's index reflects a global constraint on the degrees of all possible subgraphs.

### Algorithmic Foundations: The Peeling Algorithm

The definition of the [k-core](@entry_id:1126853) suggests a natural algorithm for finding it: for a given $k$, iteratively remove (or "peel") all vertices with a degree less than $k$ until no such vertices remain. The set of surviving vertices forms the $k$-core.

To compute the [coreness](@entry_id:1123067) for all vertices in a network simultaneously, a more efficient peeling algorithm is used. Instead of fixing $k$, the algorithm processes vertices in increasing order of their *current* degree. The [coreness](@entry_id:1123067) of a vertex is its degree at the moment it is removed from the network.

The most efficient implementation of this peeling algorithm achieves a linear-[time complexity](@entry_id:145062) of $O(n+m)$ for a graph with $n$ vertices and $m$ edges . This remarkable efficiency is made possible by a specialized [data structure](@entry_id:634264) that functions like a **bucket queue** or **[counting sort](@entry_id:634603)**. The procedure is as follows :

1.  **Initialization**: Compute the initial degree of every vertex. Create an array of "buckets," where each bucket corresponds to a degree value from $0$ to $n-1$. Place each vertex into the bucket corresponding to its degree. This initial sorting by degree can be done in $O(n+m)$ time.
2.  **Iterative Peeling**: Process the buckets in increasing order of degree. Starting with the lowest-degree non-empty bucket (say, bucket $k$), select a vertex $v$.
3.  **Assign Coreness**: The [coreness](@entry_id:1123067) of this vertex $v$ is its current degree, so set $c(v)=k$.
4.  **Update Neighbors**: For each neighbor $u$ of the removed vertex $v$, decrement its degree. If the degree of $u$ drops from $d$ to $d-1$, move vertex $u$ from bucket $d$ to bucket $d-1$.
5.  **Repeat**: Continue processing vertices from the lowest-degree bucket. Because neighbor degrees only ever decrease, the process moves monotonically through the vertices.

The key to the $O(1)$ update time for moving a vertex between buckets is to use auxiliary pointers that track the position of each vertex within the bucket array. This allows for constant-time relocation, avoiding costly searches. Since each vertex is removed once and each edge causes exactly two degree-decrement operations over the entire algorithm, the total [time complexity](@entry_id:145062) is bounded by $O(n+m)$.

### The Onion Decomposition: A Refined View of the Core

The k-core decomposition provides a valuable [first-order approximation](@entry_id:147559) of a network's [core-periphery structure](@entry_id:1123066). However, it treats all nodes within a given k-shell as structurally equivalent. The **[onion decomposition](@entry_id:1129131)** offers a more granular view by stratifying the nodes *within* each shell, revealing a finer hierarchy.

#### Defining Onion Layers

Onion decomposition refines the k-core by assigning each node $v$ a **layer index**, $\ell(v)$, in addition to its shell index ([coreness](@entry_id:1123067)) $s(v)$ . The pair $(s(v), \ell(v))$ provides a more detailed coordinate for a node's position. The layer index measures how deeply embedded a node is within its own shell. A higher layer index signifies greater importance or centrality to the integrity of that shell. It is important to note that several algorithmic variants of [onion decomposition](@entry_id:1129131) exist. The version described here peels layers based on a degree threshold equal to the shell's [coreness](@entry_id:1123067). Other variants, which may be encountered in different contexts or software packages, might use different peeling rules. The hands-on practices in the appendices will provide an opportunity to work with some of these specific implementations to illustrate this point.

#### The Layering Algorithm

The algorithm to compute onion layers is a recursive peeling process conducted within the context of each shell. A common mistake is to perform this peeling only on the [subgraph](@entry_id:273342) induced by the shell itself. A scientifically sound procedure must account for the connections that nodes in a shell have to nodes in deeper (higher-indexed) shells, as these connections contribute to their [coreness](@entry_id:1123067) .

The correct procedure is as follows:
1.  **Compute Coreness**: First, perform the standard k-core decomposition to find the [coreness](@entry_id:1123067) $c_i$ for every node $i$ and thereby identify the shells $S_k$.
2.  **Process Shells**: For each shell $S_k$, perform a sub-peeling process. The crucial step is to work within the graph induced by the entire k-core, $H_k = G[\{j \in V \mid c_j \ge k\}]$. This ensures all connections contributing to a node's membership in the k-core are considered.
3.  **Peel Layers within the Shell**: Initialize a layer counter, $r=1$.
    *   In the current [residual graph](@entry_id:273096) (initially $H_k$), identify all nodes $i \in S_k$ whose degree has dropped to exactly $k$.
    *   Assign these nodes the current layer index, $l_i = r$.
    *   Remove all of these nodes *simultaneously*. This synchronous removal ensures the process is deterministic and independent of tie-breaking.
    *   Increment the layer counter, $r \leftarrow r+1$, and repeat this process on the new, smaller [residual graph](@entry_id:273096) until all nodes from the shell $S_k$ have been removed.

#### A Concrete Example

Consider a simple graph with vertices $V=\{a,b,c,d,e,h\}$ and edges forming a 5-cycle $(a-b-c-d-e-a)$ with an additional node $h$ connected to $a$, $b$, and $c$ .

*   **k-core Analysis**: First, we compute [coreness](@entry_id:1123067). The initial degrees are $d(d)=d(e)=2$ and $d(a)=d(b)=d(c)=d(h)=3$. The entire graph has a [minimum degree](@entry_id:273557) of $2$, so it is a $2$-core. To check for a $3$-core, we peel nodes with degree less than $3$. Nodes $d$ and $e$ are removed. In the remaining graph on $\{a,b,c,h\}$, the degrees of $a$ and $c$ drop to $2$. They are then removed. Finally, $b$ and $h$ are left with degree $1$ and are also removed. The $3$-core is empty. Therefore, all nodes in this graph have a [coreness](@entry_id:1123067) of $2$, and they all belong to the $2$-shell.

*   **Onion Decomposition**: Now, we refine the $2$-shell.
    *   **Layer 1**: We start with the full graph and look for nodes in the $2$-shell with degree exactly $2$. These are nodes $d$ and $e$. We remove them and assign them layer index $\ell=1$.
    *   **Layer 2**: After removing $\{d,e\}$, the degrees of their neighbors $a$ and $c$ drop to $2$. Now, in the [residual graph](@entry_id:273096), $a$ and $c$ are the nodes in the $2$-shell with degree $2$. We remove them and assign them layer index $\ell=2$.
    *   **Layer 3**: After removing $\{a,c\}$, only nodes $b$ and $h$ remain. Their degrees in the [residual graph](@entry_id:273096) are now $1$. Since $1  2$, they are removed next. We assign them layer index $\ell=3$.

This simple example clearly demonstrates the power of [onion decomposition](@entry_id:1129131). While all nodes belong to the same $2$-shell, they are clearly stratified into three distinct onion layers: Layer 1 ($\{d,e\}$), Layer 2 ($\{a,c\}$), and Layer 3 ($\{b,h\}$). This reveals a fine-grained hierarchy of centrality that the k-core decomposition alone misses.

### From Decomposition to Structure and Function

The ultimate goal of these [decomposition methods](@entry_id:634578) is to infer principles of network organization and function from the identified structures.

#### Approximating Core-Periphery Structure

Core-periphery structure is often formally defined using a **stochastic [blockmodel](@entry_id:1121715)**, where the network is partitioned into a core block $C$ and a periphery block $P$. In this idealized model, the probability of an edge existing between two nodes depends on their block membership, with the condition that $p_{CC} > p_{CP} > p_{PP}$ . That is, core nodes are densely connected to each other, peripherial nodes are sparsely connected to each other, and core-periphery connections have an intermediate density.

The [k-core](@entry_id:1126853) and onion decompositions provide a powerful, deterministic, and scalable method for approximating such a structure. The innermost, highest-indexed cores and layers correspond to the network's structural core, while the outer, low-indexed shells constitute the periphery. While the integer indices from these decompositions provide a discrete assignment of nodes to layers, they are often used as a basis for inferring continuous **[coreness](@entry_id:1123067) scores**, which assign each node a scalar value quantifying its position along a smooth core-to-periphery gradient .

#### Onion Layers as a Signature of Resilience

The true power of [onion decomposition](@entry_id:1129131) lies in its ability to quantify the resilience of the shells themselves. While two networks might have identical degree sequences and even identical [k-core](@entry_id:1126853) structures, the wiring *within* their shells can be dramatically different. One might be tree-like and fragile, while the other is rich in cycles and robust .

The onion layer index captures this difference. A deeper onion layer (higher $\ell(v)$) is a signature of redundant connectivity. A vertex survives more peeling rounds precisely because its neighbors within the shell are themselves part of a resilient, multiply-connected component, often characterized by cycles. This structural redundancy has direct functional consequences for [network robustness](@entry_id:146798):

*   **Connectivity**: By Menger's theorem, a greater number of redundant paths translates directly to higher **[vertex-connectivity](@entry_id:267799)** ($\kappa$) within the shell. This means more nodes must be removed to fragment the shell.
*   **Percolation**: A network with more resilient, cycle-rich cores will exhibit a slower decay in the size of its [giant connected component](@entry_id:1125630) ($S(p)$) under random node failures. The onion structure can thus predict how gracefully a network will degrade.
*   **Spectral Properties**: The structure of the core is also reflected in the network's spectral properties. Deeper onion layers, by enhancing conductance and removing bottlenecks, tend to be associated with a higher **[algebraic connectivity](@entry_id:152762)** ($\lambda_2$ of the Laplacian matrix), a key indicator of how difficult it is to cut the graph into separate components.

In summary, [k-core](@entry_id:1126853) and [onion decomposition](@entry_id:1129131) are not merely descriptive tools for visualizing network layers. They are analytical engines that provide deep insights into the hierarchical organization of complex systems, revealing a structure that is intimately linked to their stability, resilience, and overall function.