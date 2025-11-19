## Introduction
The structure of a network is often understood by examining its components, and the most fundamental local property of a node is its degree—the number of connections it has. This raises a foundational question in graph theory: given a list of integers, can it represent the degree sequence of a simple graph? This inquiry into "graphic sequences" forms a bridge between local vertex properties and the global structure of a graph, addressing the knowledge gap between a list of numbers and a tangible network. This article provides a thorough exploration of this concept.

In the following chapters, you will delve into the core principles that govern graphic sequences. The "Principles and Mechanisms" chapter will introduce the necessary conditions that any [graphic sequence](@entry_id:274330) must satisfy, such as the Handshaking Lemma, and present the two cornerstone theorems for verification: the recursive Havel-Hakimi algorithm and the global Erdős-Gallai theorem. Building on this theoretical foundation, the "Applications and Interdisciplinary Connections" chapter will demonstrate how degree sequences are used to constrain and predict graph properties like connectivity and planarity, and their vital role in modern [network science](@entry_id:139925) for statistical analysis. Finally, "Hands-On Practices" will offer opportunities to apply these concepts to solve practical problems, solidifying your understanding of how to test, analyze, and interpret graphic sequences.

## Principles and Mechanisms

In the study of graphs, we often seek to understand the relationship between local properties of vertices and the global structure of the network. Perhaps the most fundamental local property of a vertex is its **degree**, the number of edges incident to it. This naturally leads to a foundational question: if we only know the list of degrees of all vertices in a graph, what can we deduce about the graph itself? Can any arbitrary list of integers even represent the degrees of a valid graph? This inquiry brings us to the concept of graphic sequences.

A finite sequence of non-negative integers $S = (d_1, d_2, \ldots, d_n)$ is defined as a **[graphic sequence](@entry_id:274330)** if it is the [degree sequence](@entry_id:267850) of some **simple graph** on $n$ vertices. A [simple graph](@entry_id:275276) is an [undirected graph](@entry_id:263035) with no loops (edges connecting a vertex to itself) and no multiple edges between the same pair of vertices. The graph that has a given [graphic sequence](@entry_id:274330) is called a **realization** of that sequence.

### Fundamental Necessary Conditions

Before employing more advanced techniques, we can often disqualify a sequence from being graphic by checking two straightforward but powerful necessary conditions. These conditions arise directly from the definition of a simple graph.

The first and most crucial condition is a consequence of how edges are counted. Every edge in a graph connects exactly two vertices, contributing one to the degree of each. If we sum the degrees of all vertices in a graph, we are effectively counting each edge twice. This simple observation is formalized in the **Handshaking Lemma**. For any graph $G=(V, E)$, the sum of its vertex degrees is equal to twice the number of its edges:

$$ \sum_{v \in V} \deg(v) = 2|E| $$

From this lemma, it immediately follows that the sum of the degrees in any graph must be an even number. Therefore, a primary test for any potential degree sequence $S = (d_1, d_2, \ldots, d_n)$ is to calculate its sum, $\sum_{i=1}^{n} d_i$. If this sum is odd, the sequence cannot be graphic. For instance, the sequence $(4, 3, 3, 2, 1)$ has a sum of 13, which is odd. Consequently, it is impossible to construct a simple graph with these degrees, and the sequence is not graphic [@problem_id:1509392]. Conversely, if a sequence is known to be graphic, the Handshaking Lemma allows us to precisely determine the number of edges in any of its realizations. A network with a degree sequence of $(7, 7, 6, 5, 4, 4, 3, 2, 1, 1)$ must have a total degree sum of 40, implying that any corresponding graph has exactly $40/2 = 20$ edges [@problem_id:1509378].

The second necessary condition stems from the "simple" nature of the graph. In a simple graph with $n$ vertices, any single vertex can be connected to at most all of the other $n-1$ vertices. This imposes an upper bound on any single degree in the sequence: for all $i$, the degree $d_i$ must satisfy $0 \le d_i \le n-1$. A sequence containing a degree $d_i \ge n$ is therefore not graphic. For example, in a sequence for a 6-vertex graph like $(6, 5, 4, 3, 2, 2)$, the presence of a degree of 6 is an immediate disqualification, as a vertex in a 6-vertex graph can have a maximum degree of only 5 [@problem_id:1509392].

These two conditions serve as an efficient initial screening tool. When faced with determining the possible values for an unknown degree $x$ in a sequence like $\{6, 3, 3, 2, 2, 1, x\}$ for a 7-vertex graph, we can first apply these rules. The maximum degree must be at most $n-1=6$, which is satisfied for any $x \le 6$. The sum of degrees is $17+x$. For this sum to be even, $x$ must be odd. This narrows the possibilities for $x$ from all non-negative integers down to a small set, such as $\{1, 3, 5\}$ [@problem_id:1509406]. However, these conditions are necessary but not sufficient; satisfying them does not guarantee a sequence is graphic.

### Algorithmic Verification: The Havel-Hakimi Theorem

To definitively determine if a sequence is graphic, we need a more robust method. The **Havel-Hakimi theorem** provides a [recursive algorithm](@entry_id:633952) for this purpose. The theorem establishes a powerful equivalence that allows us to reduce the problem to a smaller, simpler one.

The theorem states that a non-increasing sequence of non-negative integers $S = (d_1, d_2, \ldots, d_n)$ (where $d_1 \ge d_2 \ge \ldots \ge d_n$) is graphic if and only if the sequence $S'$ is also graphic. The new sequence $S'$ is of length $n-1$ and is constructed by removing the largest element, $d_1$, and subtracting 1 from the next $d_1$ largest elements. That is:

$S' = (d_2-1, d_3-1, \ldots, d_{d_1+1}-1, d_{d_1+2}, \ldots, d_n)$

After its construction, $S'$ must be re-sorted into non-increasing order before the next step of the algorithm is applied. The process is repeated until the sequence is either trivially graphic (e.g., all zeros) or fails a condition (e.g., contains a negative number).

The intuition behind this algorithm is constructive. If a graph realizing $S$ exists, there must be one where the vertex $v_1$ (with highest degree $d_1$) is connected to the vertices with the next $d_1$ highest degrees. We can then remove $v_1$ and its incident edges. The remaining graph has $n-1$ vertices, and its degree sequence is precisely $S'$. The "if and only if" nature of the theorem is its core strength: if the reduced sequence $S'$ is proven to be non-graphic at any step, we can definitively conclude that the original sequence $S$ was also not graphic [@problem_id:1509427].

Let's apply this to determine if the sequence $S = (3, 3, 2, 2, 1, 1)$ is graphic.
1. The sequence is already sorted. We take the first element, $d_1=3$. We remove it and subtract 1 from the next 3 elements: $(3-1, 2-1, 2-1, 1, 1)$. This gives the new sequence $(2, 1, 1, 1, 1)$.
2. The sequence is sorted. We take $d_1=2$. We remove it and subtract 1 from the next 2 elements: $(1-1, 1-1, 1, 1)$. This gives $(0, 0, 1, 1)$. Re-sorting yields $(1, 1, 0, 0)$.
3. The sequence is sorted. We take $d_1=1$. We remove it and subtract 1 from the next element: $(1-1, 0, 0)$. This gives $(0, 0, 0)$.
Since we have successfully reduced the sequence to all zeros, which is trivially graphic (a graph with no edges), the original sequence $(3, 3, 2, 2, 1, 1)$ is graphic.

Interestingly, each step of the Havel-Hakimi process preserves the parity of the sum of degrees. The sum of the new sequence, $\Sigma(S')$, relates to the sum of the old sequence, $\Sigma(S)$, by the formula $\Sigma(S') = \Sigma(S) - 2d_1$ [@problem_id:1509420]. This makes sense: we remove the contribution of $d_1$ from the sum once by removing the vertex, and a second time by subtracting 1 from $d_1$ other vertices, corresponding to the other ends of the removed edges.

### A Global Condition: The Erdős-Gallai Theorem

While the Havel-Hakimi algorithm provides a procedural test, the **Erdős-Gallai theorem** offers a set of declarative conditions. It provides a global check on the distribution of degrees rather than a recursive reduction.

The theorem states that a non-increasing sequence of non-negative integers $d_1 \ge d_2 \ge \ldots \ge d_n$ is graphic if and only if the sum of the degrees is even, and for every integer $k$ from $1$ to $n$, the following inequality holds:

$$ \sum_{i=1}^{k} d_i \le k(k-1) + \sum_{i=k+1}^{n} \min(k, d_i) $$

The intuition behind this inequality is to check if the "degree budget" of the $k$ highest-degree vertices is plausible. The left side, $\sum_{i=1}^{k} d_i$, represents the total degree sum demanded by these $k$ vertices. The right side represents the maximum possible degree sum they could collectively have. This maximum consists of two parts:
1.  **Internal Edges:** Edges connecting vertices *within* this group of $k$. At most, they can form a complete graph $K_k$, which has $k(k-1)/2$ edges and thus contributes $k(k-1)$ to their degree sum.
2.  **External Edges:** Edges connecting these $k$ vertices to the *remaining* $n-k$ vertices. Each of the remaining vertices $v_i$ (for $i > k$) can provide at most $d_i$ edges in total, and can connect to at most all $k$ of the high-degree vertices. Therefore, its contribution to their degree sum is capped by $\min(k, d_i)$.

If for even a single value of $k$, the required sum of degrees on the left exceeds the maximum possible sum on the right, the sequence cannot be graphic. For example, consider the sequence $S = (5, 5, 5, 3, 1, 1)$ [@problem_id:1509399]. The sum is 20 (even). Let's test the Erdős-Gallai condition for $k=3$:
- Left-hand side: $\sum_{i=1}^{3} d_i = 5 + 5 + 5 = 15$. (The problem in the original dataset has an arithmetic error, the correct calculation is $5+5+5=15$, not 12. Let's use another example for clarity from `1509392`.)
Let's re-examine sequence $D$ from `1509392`: $S=(4, 4, 4, 1, 1)$ with $n=5$. The sum is 14 (even). Let's test for $k=3$:
- Left-hand side: $\sum_{i=1}^{3} d_i = 4 + 4 + 4 = 12$.
- Right-hand side: $k(k-1) + \sum_{i=4}^{5} \min(k, d_i) = 3(2) + \min(3, 1) + \min(3, 1) = 6 + 1 + 1 = 8$.
Since $12 \not\le 8$, the inequality fails. Therefore, the sequence $(4, 4, 4, 1, 1)$ is not graphic.

### Beyond Existence: Uniqueness and Graph Properties

Knowing a sequence is graphic tells us that at least one corresponding graph exists. A natural follow-up question is: does this sequence specify the graph's structure uniquely? In most cases, the answer is no. A single [graphic sequence](@entry_id:274330) can often be realized by multiple **non-isomorphic** graphs—graphs that have fundamentally different structures.

For example, the sequence $(3, 3, 2, 2, 1, 1)$ is graphic. However, it can be realized by at least two distinct network topologies. One realization could be a graph consisting of a cycle of four vertices where two opposite vertices have an extra edge between them, plus an isolated edge. Another realization might be a path of four vertices where the two central vertices are also connected to two separate "leaf" nodes. These structures are not the same; for instance, one might contain triangles while the other does not, a structural property that distinguishes them as non-isomorphic [@problem_id:1509424].

This lack of uniqueness extends to fundamental graph properties like connectivity. Consider the simple 2-regular sequence $(2, 2, 2, 2, 2, 2)$. This sequence can be realized as a single, connected 6-vertex cycle ($C_6$). Alternatively, it can be realized as two disconnected 3-vertex cycles (two disjoint triangles, $C_3 \sqcup C_3$). The first realization has one connected component, while the second has two. Thus, the [degree sequence](@entry_id:267850) alone does not determine whether the underlying network is connected [@problem_id:1509403].

Finally, it is worth noting the relationship between a graph and its **complement**. For a simple graph $G$ with $n$ vertices and degree sequence $S = (d_1, \ldots, d_n)$, its complement $\bar{G}$ has a [degree sequence](@entry_id:267850) $S^c = (n-1-d_1, \ldots, n-1-d_n)$. A significant theorem in this area states that $S$ is graphic if and only if $S^c$ is also graphic. This provides a powerful connection, allowing us to infer properties about one graph from its counterpart. For instance, if a graph is the disjoint union of two complete graphs, $K_4$ and $K_6$ (on 10 vertices total), its degree sequence consists of four 3s and six 5s. Its complement's [degree sequence](@entry_id:267850) would consist of four instances of $(10-1)-3=6$ and six instances of $(10-1)-5=4$. Using the Handshaking Lemma, we can immediately calculate that this [complement graph](@entry_id:276436) must have $(4 \cdot 6 + 6 \cdot 4)/2 = 24$ edges, without ever needing to visualize its structure [@problem_id:1509411].

In summary, degree sequences provide a vital, if incomplete, lens through which to view graph structure. While powerful theorems allow us to determine if a sequence is realizable, we must remain aware that the sequence alone seldom tells the full story of a graph's topology.