## Introduction
In the study of networks and discrete structures, a graph offers a powerful abstract model. However, to compare, classify, and analyze these structures, we need more than just a list of vertices and edges. The challenge lies in distilling a graph's complex topology into a simpler, quantitative form. This is where [graph invariants](@entry_id:262729)—properties that remain unchanged under [graph isomorphism](@entry_id:143072)—become essential. Among the most fundamental and accessible of these is the degree sequence, a simple list of numbers that captures the connectivity of each vertex. This article addresses the core question: what can this sequence tell us about the graph as a whole?

This exploration is structured into three parts. First, in **"Principles and Mechanisms,"** we will define the [degree sequence](@entry_id:267850), outline methods for its calculation, and uncover the foundational rules it must obey, such as the famous Handshaking Lemma. Next, **"Applications and Interdisciplinary Connections"** will demonstrate how to use the degree sequence as an analytical tool to infer properties like the number of edges and the existence of Hamiltonian cycles, while also confronting its limitations by examining non-[isomorphic graphs](@entry_id:271870) that share the same sequence. Finally, **"Hands-On Practices"** will provide concrete exercises to solidify your understanding of these concepts and their practical application. We begin by establishing the principles that make the degree sequence such a cornerstone of graph theory.

## Principles and Mechanisms

While a graph is fundamentally a set of vertices and edges, this abstract definition can be unwieldy. To understand and classify graphs, we seek to distill their complex structure into simpler, numerical descriptors. Among the most fundamental of these is the **degree sequence**. This chapter explores the principles governing degree sequences, the mechanisms for their calculation, and the profound, though sometimes limited, insights they provide into a graph's structure.

### Defining and Calculating the Degree Sequence

For any vertex $v$ in an [undirected graph](@entry_id:263035) $G$, its **degree**, denoted $\deg(v)$, is the number of edges incident to it. In the context of [simple graphs](@entry_id:274882), where loops are forbidden and no two vertices share more than one edge, the [degree of a vertex](@entry_id:261115) is equivalent to the number of its neighbors.

The **degree sequence** of a graph $G$ with $n$ vertices is the sequence of its vertex degrees. By convention, this sequence is listed in non-increasing order, $(d_1, d_2, \dots, d_n)$, where $d_1 \ge d_2 \ge \dots \ge d_n$.

The degree sequence can be determined directly from any standard representation of the graph. For instance, consider a simple graph with $n$ vertices represented by its $n \times n$ **adjacency matrix** $A$, where the entry $A_{ij}$ is $1$ if vertices $v_i$ and $v_j$ are adjacent and $0$ otherwise. Since each '1' in the $i$-th row corresponds to an edge connected to vertex $v_i$, the degree of $v_i$ is simply the sum of the entries in that row.

**Example: Degree Sequence of a Network** [@problem_id:1495673]

Consider a network of six servers, modeled as a simple graph with vertices $V = \{v_1, \dots, v_6\}$ and an [adjacency matrix](@entry_id:151010) $A$:
$$
A = \begin{pmatrix}
0  1  0  1  0  0 \\
1  0  1  0  1  0 \\
0  1  0  0  1  1 \\
1  0  0  0  0  0 \\
0  1  1  0  0  1 \\
0  0  1  0  1  0
\end{pmatrix}
$$
The degree of each vertex is the sum of its corresponding row:
- $\deg(v_1) = 0+1+0+1+0+0 = 2$
- $\deg(v_2) = 1+0+1+0+1+0 = 3$
- $\deg(v_3) = 0+1+0+0+1+1 = 3$
- $\deg(v_4) = 1+0+0+0+0+0 = 1$
- $\deg(v_5) = 0+1+1+0+0+1 = 3$
- $\deg(v_6) = 0+0+1+0+1+0 = 2$

The multiset of degrees is $\{1, 2, 2, 3, 3, 3\}$. Arranging these in non-increasing order gives the [degree sequence](@entry_id:267850) $(3, 3, 3, 2, 2, 1)$.

### Fundamental Properties and Constraints

Not every sequence of non-negative integers can be the [degree sequence](@entry_id:267850) of a [simple graph](@entry_id:275276). A sequence that can be realized by a simple graph is called a **[graphical sequence](@entry_id:268488)**. Several fundamental theorems provide necessary conditions that any [graphical sequence](@entry_id:268488) must satisfy.

#### The Handshaking Lemma

The most elementary relationship between degrees and edges is captured by the **Handshaking Lemma**, so named for its analogy to the total number of hands shaken at a party. It states that for any graph $G$ with vertex set $V$ and edge set $E$:
$$
\sum_{v \in V} \deg(v) = 2|E|
$$
The intuition is straightforward: every edge has two endpoints, so when we sum the degrees of all vertices, we count each edge exactly twice. A direct consequence is that the sum of the degrees in any graph must be an even number. This simple test can immediately disqualify many sequences. For example, the sequence $(3, 2, 1, 1)$ cannot be graphical for any graph, as its sum is $7$, an odd number [@problem_id:1495698].

This lemma also allows us to determine the number of edges in a graph directly from its degree sequence. For a graph with [degree sequence](@entry_id:267850) $(4, 4, 3, 3, 2, 1, 1)$, the sum of degrees is $18$. By the Handshaking Lemma, $2|E| = 18$, which implies the graph has $|E|=9$ edges [@problem_id:1495676].

#### The Parity of Odd-Degree Vertices

A powerful corollary of the Handshaking Lemma concerns vertices of odd degree. Since the total sum of degrees must be even, the number of terms in the sum that are odd must itself be even. If there were an odd number of odd-degree vertices, their sum would be odd. The sum of the remaining even-degree vertices would be even, and the total sum (odd + even) would be odd, contradicting the lemma. Therefore, **in any graph, the number of vertices with odd degree must be even**.

This principle reveals why certain network configurations are impossible. Imagine a scenario where a systems engineer is asked to design a network of 11 drones, where each drone must connect to exactly 3 others [@problem_id:1495710]. This would correspond to a graph on 11 vertices where every vertex has a degree of 3. This design specifies 11 vertices of odd degree. Since 11 is an odd number, such a graph cannot exist. The sum of degrees would be $11 \times 3 = 33$, an odd number, violating the Handshaking Lemma.

#### Degree Bounds in Simple Graphs

The definition of a simple graph imposes a hard constraint on the maximum degree a vertex can have. In a simple graph with $n$ vertices, a given vertex $v$ can be connected to at most the other $n-1$ vertices. Therefore, for any vertex $v$ in a simple graph on $n$ vertices, its degree must satisfy $0 \le \deg(v) \le n-1$.

This provides another immediate test for graphical sequences. For instance, the sequence $S_2 = (8, 4, 3, 3, 2, 2, 1, 1)$ cannot be the [degree sequence](@entry_id:267850) of a [simple graph](@entry_id:275276) on $n=8$ vertices [@problem_id:1542629]. The presence of the term '8' violates the condition that any degree $d_i$ must be less than or equal to $n-1 = 7$. No algorithm is needed to determine this; it is a failure to meet a fundamental definitional requirement.

It is crucial to note that this constraint applies only to **[simple graphs](@entry_id:274882)**. If we relax the condition and allow **multigraphs** (which permit multiple edges between two vertices but no loops), a vertex's degree can exceed $n-1$. For example, the sequence $(6, 2, 2, 2)$ is not graphical for a simple graph on $n=4$ vertices, as $6 > 4-1=3$. However, it can be realized by a [multigraph](@entry_id:261576) where one central vertex is connected to the other three vertices by two parallel edges each [@problem_id:1495698].

### Degree Sequences of Common Graph Families

Applying these principles to standard classes of graphs helps build intuition.

- **Empty Graphs:** The [empty graph](@entry_id:262462) on $n$ vertices, $E_n$, has no edges. Consequently, every vertex has a degree of 0. Its [degree sequence](@entry_id:267850) is $(0, 0, \dots, 0)$. This sequence uniquely identifies the graph as the [empty graph](@entry_id:262462), which consists of $n$ [isolated vertices](@entry_id:269995) and therefore has $n$ [connected components](@entry_id:141881) [@problem_id:1501297].

- **Complete Graphs:** The complete graph on $n$ vertices, $K_n$, contains an edge between every pair of distinct vertices. Each vertex is connected to the other $n-1$ vertices, so every vertex has a degree of $n-1$. The degree sequence is $(n-1, n-1, \dots, n-1)$. Such graphs, where every vertex has the same degree, are called **regular graphs**. The sequence $(7, 7, 7, 7, 7, 7, 7, 7)$ is the [degree sequence](@entry_id:267850) for the complete graph on 8 vertices, $K_8$ [@problem_id:1542629]. Knowing this allows for simple calculations, such as finding the average of the squared degrees: for $K_n$, this value is $\frac{1}{n}\sum_{i=1}^n (n-1)^2 = (n-1)^2$ [@problem_id:1495707].

- **Path Graphs:** The path graph on $n$ vertices, $P_n$ (for $n \ge 2$), consists of vertices $v_1, \dots, v_n$ with edges connecting $v_i$ and $v_{i+1}$. The two endpoints, $v_1$ and $v_n$, have degree 1. The $n-2$ internal vertices each have degree 2. The [degree sequence](@entry_id:267850) is thus $(\underbrace{2, 2, \dots, 2}_{n-2 \text{ times}}, 1, 1)$. This predictable structure allows us to reason about modifications. If a new edge is added to a [path graph](@entry_id:274599) $P_n$, the degrees of the two vertices incident to the new edge each increase by 1. If we observe a new degree sequence of $(3, 2, 2, 2, 2, 1)$ for a modified path graph on $n=6$ vertices, we can deduce its original state. This new sequence has one vertex of degree 3, four of degree 2, and one of degree 1. The only way to get this from a path graph's sequence is if an endpoint (degree 1) was connected to an internal vertex (degree 2). This changes the sequence from having degrees {2,2,2,2,1,1} to {3,2,2,2,2,1}. The resulting sequence has one 3, one 1, and $n-2$ vertices of degree 2. Comparing this to the observed $(3, 2, 2, 2, 2, 1)$, we see there are four vertices of degree 2, so $n-2=4$, which implies the original graph was $P_6$ [@problem_id:1495704].

### Deeper Implications and Limitations

Beyond these foundational rules, degree sequences hint at deeper structural properties and also have important limitations.

#### Duplicate Degrees and the Pigeonhole Principle

A striking property of [simple graphs](@entry_id:274882) is that, provided they have at least two vertices, they cannot have distinct degrees for all of them. That is, **in any simple graph with $n \ge 2$ vertices, there must be at least two vertices with the same degree**.

The proof is an elegant application of [the pigeonhole principle](@entry_id:268698) [@problem_id:1495678]. In a [simple graph](@entry_id:275276) with $n$ vertices, the possible values for any degree are in the set $\{0, 1, \dots, n-1\}$. At first glance, this set contains $n$ distinct values, suggesting it might be possible for all $n$ vertices to have a unique degree. However, a vertex of degree $n-1$ must be connected to all other vertices, while a vertex of degree $0$ must be connected to none. It is impossible for a graph to simultaneously contain a vertex of degree $n-1$ and a vertex of degree $0$.

Therefore, the set of all degrees for any given simple graph must be a subset of either $\{0, 1, \dots, n-2\}$ or $\{1, 2, \dots, n-1\}$. In either case, there are at most $n-1$ distinct possible degree values available for the $n$ vertices. By [the pigeonhole principle](@entry_id:268698), if we are to assign degrees to $n$ vertices (the "pigeons") from a set of at most $n-1$ available values (the "pigeonholes"), at least two vertices must be assigned the same degree.

#### The Limit of Expressiveness: Non-Isomorphic Realizations

The degree sequence is a powerful [graph invariant](@entry_id:274470), meaning that if two graphs are isomorphic, they must have the same degree sequence. However, the converse is not true. A single [degree sequence](@entry_id:267850) can be realized by multiple **non-isomorphic** graphs. This is perhaps the most significant limitation of the degree sequence as a structural descriptor; it does not uniquely determine the graph's topology.

Consider the [degree sequence](@entry_id:267850) $S = (3, 2, 2, 1, 1, 1)$. It is possible to construct at least two different [simple graphs](@entry_id:274882) on six vertices that both have this degree sequence [@problem_id:1495674].

- **Graph $G_1$**: A central vertex connected to three other vertices, two of which are also connected to a final leaf vertex. This graph is a tree and is therefore connected and acyclic.
- **Graph $G_2$**: A triangle (a 3-cycle) on three vertices, with one of these vertices also connected to a fourth vertex. The remaining two vertices form a separate, isolated edge. This graph is disconnected and contains a cycle.

Both $G_1$ and $G_2$ have the [degree sequence](@entry_id:267850) $(3, 2, 2, 1, 1, 1)$. However, they are fundamentally different structures. $G_1$ is connected, while $G_2$ is not. $G_1$ is acyclic, while $G_2$ has a cycle of length 3. Since connectivity and the presence of cycles are [graph invariants](@entry_id:262729), $G_1$ and $G_2$ cannot be isomorphic.

This example illustrates that while the degree sequence provides a valuable first-order summary of a graph's connectivity, it omits crucial information about how that connectivity is arranged. To distinguish between such graphs, one must turn to more sophisticated invariants.