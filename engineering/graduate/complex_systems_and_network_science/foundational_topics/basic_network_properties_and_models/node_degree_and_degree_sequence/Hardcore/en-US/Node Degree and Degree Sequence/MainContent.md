## Introduction
In the study of [complex networks](@entry_id:261695), understanding the connectivity of individual components is the first step toward deciphering the architecture of the entire system. At the most fundamental level, this connectivity is captured by the [node degree](@entry_id:1128744)—a simple count of a node's connections. While a local property, the collection of all node degrees, known as the [degree sequence](@entry_id:267850), holds surprisingly rich information and imposes powerful constraints on the network's global structure. However, a critical gap exists between this list of numbers and a fully realized network. This raises foundational questions: What global properties can be deduced from local degrees alone? Under what conditions can a given sequence of degrees even form a coherent network? And how can we use this sequence to build realistic network models?

This article addresses these questions by exploring the theory and application of [node degree](@entry_id:1128744) and degree sequences. The first chapter, **"Principles and Mechanisms,"** lays the theoretical groundwork, defining degree, introducing key constraints like the [handshaking lemma](@entry_id:261183), and presenting classic theorems that determine whether a sequence is realizable as a graph. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates how these principles are applied to analyze higher-order network structures, predict dynamic processes like disease spread, and provide methodological rigor in fields like biomedicine and neuroscience. Finally, **"Hands-On Practices"** offers practical exercises to solidify these concepts, from verifying fundamental lemmas to implementing [graph realization](@entry_id:270634) algorithms.

## Principles and Mechanisms

The degree of a node is arguably the most fundamental local property in network science, quantifying the number of connections a node maintains. While simple in concept, the collection of all node degrees—the [degree sequence](@entry_id:267850)—imposes strong constraints on the global structure of a network and serves as a cornerstone for both network analysis and modeling. This chapter delves into the principles governing node degrees and their sequences, exploring their definitions, the constraints they impose, the conditions under which a sequence can be realized as a graph, and their central role in generative models.

### Defining Node Degree: A Local Measure of Connectivity

The precise definition of [node degree](@entry_id:1128744) depends on the class of graph under consideration. We begin with the simplest cases and progressively generalize.

#### Undirected Graphs

In a **simple [undirected graph](@entry_id:263035)**—one with no self-loops and no parallel edges—the **degree** of a node $i$, denoted $k_i$ or $d_i$, is the number of edges incident to it. This is equivalent to the number of its distinct neighbors . For a labeled graph with $n$ nodes, the **[degree sequence](@entry_id:267850)** is the ordered $n$-tuple $(d_1, d_2, \dots, d_n)$ where $d_i$ is the degree of the $i$-th node. Since a node cannot be connected to itself and can be connected to each of the other $n-1$ nodes at most once, the degree of any node $i$ in a simple graph is bounded: $0 \le d_i \le n-1$. A degree of $0$ corresponds to an isolated node, while a degree of $n-1$ corresponds to a node connected to all other nodes in the network.

This definition must be refined for **multigraphs**, which permit self-loops (edges connecting a node to itself) and parallel edges (multiple edges between the same pair of nodes). A more robust and general definition of degree is the number of edge endpoints, or **stubs** (half-edges), incident to a node . Following this definition:
*   An edge between two distinct nodes $i$ and $j$ contributes $1$ to $d_i$ and $1$ to $d_j$. If there are $m_{ij}$ parallel edges between $i$ and $j$, they contribute $m_{ij}$ to both $d_i$ and $d_j$.
*   A **[self-loop](@entry_id:274670)** at node $i$ is an edge where both endpoints are incident to node $i$. Therefore, each [self-loop](@entry_id:274670) contributes $2$ to the degree $d_i$.

For instance, consider a [multigraph](@entry_id:261576) on four vertices $\{1,2,3,4\}$ with two parallel edges between nodes 1 and 2, one edge between 2 and 3, one [self-loop](@entry_id:274670) at node 1, and three self-loops at node 4. The degrees would be calculated as follows :
*   $d_1 = 2 \text{ (from parallel edges to 2)} + 2 \text{ (from self-loop)} = 4$.
*   $d_2 = 2 \text{ (from parallel edges to 1)} + 1 \text{ (from edge to 3)} = 3$.
*   $d_3 = 1 \text{ (from edge to 2)} = 1$.
*   $d_4 = 3 \times 2 \text{ (from self-loops)} = 6$.
The resulting degree sequence is $(4, 3, 1, 6)$.

#### Directed Graphs

In **[directed graphs](@entry_id:272310)**, or **[digraphs](@entry_id:269385)**, where edges (called arcs) have an origin and a destination, connectivity is captured by two distinct measures for each node. The **in-degree**, $k_i^{\text{in}}$, is the number of arcs terminating at node $i$, while the **out-degree**, $k_i^{\text{out}}$, is the number of arcs originating from node $i$ .

These quantities are conveniently expressed using the graph's **[adjacency matrix](@entry_id:151010)** $A$, where $A_{ij}$ is the number of arcs from node $i$ to node $j$. The out-degree of node $i$ is the sum of the entries in its corresponding row, and the in-degree is the sum of the entries in its corresponding column:
$$
k_i^{\text{out}} = \sum_{j=1}^{n} A_{ij} \quad \text{and} \quad k_i^{\text{in}} = \sum_{j=1}^{n} A_{ji}
$$
A directed [self-loop](@entry_id:274670) from node $i$ to itself corresponds to a nonzero diagonal entry $A_{ii}$. Such an arc both originates and terminates at $i$, so each [self-loop](@entry_id:274670) at node $i$ contributes $1$ to $k_i^{\text{out}}$ and $1$ to $k_i^{\text{in}}$ . The total number of self-loops in the graph is thus given by the trace of the adjacency matrix, $\mathrm{trace}(A) = \sum_i A_{ii}$. For a simple [digraph](@entry_id:276959) with $n$ nodes, the degrees are bounded by $0 \le k_i^{\text{in}}, k_i^{\text{out}} \le n-1$ .

### Global Constraints from Local Properties: The Handshaking Lemmas

A remarkable feature of graph theory is that purely local information, such as node degrees, can lead to powerful global statements about the entire graph. The most fundamental of these is the [handshaking lemma](@entry_id:261183).

#### The Handshaking Lemma for Undirected Graphs

By summing the degrees of all nodes in an undirected graph, we are counting every edge endpoint. Since each edge, by definition, has exactly two endpoints, this sum must be equal to twice the total number of edges, $|E|$. This gives the **[handshaking lemma](@entry_id:261183)**:
$$
\sum_{i \in V} d_i = 2|E|
$$
This identity holds for any [undirected graph](@entry_id:263035), including multigraphs, provided the degree contribution of a [self-loop](@entry_id:274670) is counted as 2 [@problem_id:4293370, @problem_id:4293345]. A direct and profound consequence of this lemma is that the sum of degrees is always an even number. This, in turn, implies that **the number of vertices with an odd degree must be even**. To see this, one can partition the vertices into those with even degree ($V_{\text{even}}$) and those with odd degree ($V_{\text{odd}}$). The sum of degrees over $V_{\text{even}}$ is even. For the total sum to be even, the sum of degrees over $V_{\text{odd}}$ must also be even. A sum of odd numbers can only be even if there is an even number of terms, meaning $|V_{\text{odd}}|$ must be an even integer .

#### The Handshaking Lemma for Directed Graphs

A similar principle applies to [directed graphs](@entry_id:272310). Summing all out-degrees counts the origin of every arc exactly once. Summing all in-degrees counts the destination of every arc exactly once. Since every arc has exactly one origin and one destination, both sums must equal the total number of arcs, $|E|$:
$$
\sum_{i \in V} k_i^{\text{out}} = \sum_{i \in V} k_i^{\text{in}} = |E|
$$
This is the [handshaking lemma](@entry_id:261183) for [directed graphs](@entry_id:272310) [@problem_id:4293429, @problem_id:4293345]. Unlike the undirected case, the total number of arcs $|E|$ can be any non-negative integer, so the sum of in-degrees (or out-degrees) is not constrained to be even. However, the sum of all in- and out-degrees across the network is always even:
$$
\sum_{i \in V} (k_i^{\text{in}} + k_i^{\text{out}}) = \sum_{i \in V} k_i^{\text{in}} + \sum_{i \in V} k_i^{\text{out}} = |E| + |E| = 2|E|
$$
This leads to a subtler parity constraint: the number of nodes with odd in-degree and the number of nodes with odd [out-degree](@entry_id:263181) must have the same parity (i.e., both are even or both are odd), though they need not be equal .

### From Sequence to Structure: The Question of Graphicality

The degree sequence provides a statistical summary of a network's connectivity. A natural and deep question follows: given a sequence of integers, does there exist a [simple graph](@entry_id:275276) that realizes it? Such a sequence is called **graphical**.

#### The Degree Sequence as an Incomplete Descriptor

Before exploring tests for graphicality, it is crucial to recognize that the [degree sequence](@entry_id:267850) does not uniquely determine a graph's structure. Multiple non-[isomorphic graphs](@entry_id:271870) can share the same [degree sequence](@entry_id:267850). Two graphs are **isomorphic** if they are structurally identical, meaning there exists a [one-to-one mapping](@entry_id:183792) of their vertices that preserves adjacency.

For example, consider the [degree sequence](@entry_id:267850) $d=(3,3,2,2,2,2)$. There are at least two non-isomorphic [simple graphs](@entry_id:274882) that realize this sequence . One such graph, $G_A$, can be formed by two triangles, $\{1,3,4\}$ and $\{2,5,6\}$, connected by the edge $\{1,2\}$. Another, $G_B$, is a 6-cycle $\{1-3-5-2-6-4-1\}$ with an additional edge $\{1,2\}$. Both graphs realize the sequence $d$. However, they are structurally distinct. A simple way to prove this is by comparing a **[graph invariant](@entry_id:274470)**—a property preserved under [isomorphism](@entry_id:137127). The number of triangles (3-cycles) is one such invariant. Graph $G_A$ contains two triangles, whereas graph $G_B$ contains none. Since they have a different number of triangles, they cannot be isomorphic. This simple example demonstrates that the degree sequence is a first-order characterization; higher-order structures like cycles and motifs are not fully determined by it.

#### Characterizing Graphical Sequences

Despite its limitations, determining whether a sequence is graphical is a foundational problem. Two major results provide powerful tools for this task.

##### The Havel-Hakimi Algorithm

The **Havel-Hakimi algorithm** offers a constructive and recursive method to test for graphicality. It is based on a simple, powerful observation: if a sequence $S = (d_1, \dots, d_n)$ is graphical, then there must exist a realization where the vertex $v_1$ with the highest degree $d_1$ is connected to the $d_1$ vertices with the next-highest degrees.

This leads to the following recursive reduction step :
1.  Ensure the sequence $S$ is sorted in nonincreasing order.
2.  Remove the first term, $d_1$.
3.  Subtract 1 from each of the next $d_1$ terms in the sequence.
4.  The original sequence $S$ is graphical if and only if the new, shorter sequence is graphical (after re-sorting).

The process is repeated until the sequence consists entirely of zeros (which is graphical, realized by the [empty graph](@entry_id:262462)) or until a step cannot be completed (e.g., a term becomes negative or $d_1$ exceeds the length of the remaining sequence), in which case the original sequence is not graphical.

For example, applying a single step to the sequence $(7,6,6,5,4,4,3,3,2,2)$: we remove the 7, and subtract 1 from the next seven terms $(6,6,5,4,4,3,3)$. This yields the new sequence $(5,5,4,3,3,2,2,2,2)$, which is already sorted. The graphicality of the original 10-node sequence is now equivalent to the graphicality of this 9-node sequence .

##### The Erdős-Gallai Theorem

While Havel-Hakimi provides a constructive procedure, the **Erdős-Gallai theorem** provides an existential characterization through a set of inequalities. It states that a nonincreasing sequence of non-negative integers $\{d_1 \ge d_2 \ge \dots \ge d_n\}$ is graphical if and only if two conditions are met :
1.  The sum of degrees, $\sum_{i=1}^n d_i$, is an even number.
2.  For every integer $k$ from $1$ to $n$, the following inequality holds:
    $$
    \sum_{i=1}^{k} d_i \le k(k-1) + \sum_{i=k+1}^{n} \min(k, d_i)
    $$
The first condition is the [handshaking lemma](@entry_id:261183). The necessity of the second, more complex condition can be understood by considering the $k$ vertices with the highest degrees. The sum of their degrees, $\sum_{i=1}^{k} d_i$, accounts for edges connecting these $k$ vertices to each other and edges connecting them to the remaining $n-k$ vertices. The term $k(k-1)$ is an upper bound on the contribution from edges *within* the set of $k$ vertices (each of the $\binom{k}{2}$ possible edges is counted twice in the degree sum). The term $\sum_{i=k+1}^{n} \min(k, d_i)$ is an upper bound on the contribution from edges extending *out of* the set; an edge from a vertex $v_i$ (where $i>k$) can connect to at most $k$ vertices in the high-degree set, and is also limited by its own degree $d_i$ . The theorem proves these intuitive bounds are not only necessary but also sufficient.

### Degree Sequences in Network Modeling

In modern network science, degree sequences are not just analytical objects but also fundamental building blocks for creating synthetic networks that mimic real-world systems.

#### The Degree Distribution

For large networks, it is often more practical to work with the **empirical degree distribution**, $p_k$, which represents the fraction of nodes in the network that have degree $k$. It is formally defined as:
$$
p_{k} = \frac{N_k}{n} = \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}\{d_{i} = k\}
$$
where $n$ is the total number of nodes, $N_k$ is the number of nodes with degree $k$, and $\mathbf{1}\{\cdot\}$ is the [indicator function](@entry_id:154167) . The quantity $p_k$ can be interpreted as the probability that a randomly chosen node has degree $k$. This function is a proper probability distribution, as its sum over all possible degrees is necessarily 1:
$$
\sum_{k=0}^{n-1} p_k = \sum_{k=0}^{n-1} \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}\{d_i = k\} = \frac{1}{n} \sum_{i=1}^{n} \sum_{k=0}^{n-1} \mathbf{1}\{d_i = k\} = \frac{1}{n} \sum_{i=1}^{n} 1 = 1
$$
The inner sum evaluates to 1 because for any given node $i$, its degree $d_i$ matches exactly one value of $k$ in the range of possible degrees . The shape of this distribution—be it Poissonian, exponential, or a power law—is a key signature of a network's organizing principles.

#### The Configuration Model

The **configuration model** is a canonical method for generating a random [multigraph](@entry_id:261576) with a predefined [degree sequence](@entry_id:267850) $\{d_i\}$. Its construction is elegant and intuitive :
1.  Start with $n$ disconnected vertices.
2.  To each vertex $i$, attach $d_i$ "stubs" or "half-edges". The total number of stubs in the system is $L = \sum_i d_i$, which must be even.
3.  Create a complete and [perfect matching](@entry_id:273916) on the set of $L$ stubs by pairing them up uniformly at random. Each pair of stubs becomes an edge.

This procedure generates an element from the ensemble of all possible multigraphs with the given [degree sequence](@entry_id:267850), where each element is equally likely. By its nature, the model can produce self-loops (if two stubs from the same vertex are paired) and parallel edges (if multiple pairs of stubs connect the same two vertices). For the generated network to be a simple graph, the random pairing must avoid both of these "bad" events.

The probability of obtaining a [simple graph](@entry_id:275276) depends on the properties of the degree sequence. For sparse networks typical in real-world applications, this probability can be significant. It has been shown that in the limit of large $n$, if the degree sequence satisfies the condition that the second moment is on the order of the first moment (i.e., $\sum_i d_i^2 = O(L)$) and the maximum degree is not too large (e.g., $d_{\max} = o(\sqrt{L})$), the expected number of self-loops and parallel edges converges to a finite constant. Consequently, the probability of generating a simple graph is bounded away from zero . This makes the configuration model a powerful tool for studying the properties of networks beyond just their [degree sequence](@entry_id:267850), by providing a null model against which to compare real-world network structures.

### Extensions to Directed Graphs: Digraphic Sequences

The problem of realizability can be extended to [directed graphs](@entry_id:272310). A pair of sequences, $(\mathbf{k}^{\text{out}}, \mathbf{k}^{\text{in}})$, is called **digraphic** if there exists a simple directed graph realizing them as the [out-degree](@entry_id:263181) and in-degree sequences, respectively.

As established, a primary necessary condition is that the sum of out-degrees must equal the sum of in-degrees. The full set of [necessary and sufficient conditions](@entry_id:635428) is given by the **Fulkerson-Chen-Anstee theorem**, a powerful generalization of the Erdős-Gallai theorem . It states that a pair of sequences is digraphic if and only if $\sum k_i^{\text{out}} = \sum k_i^{\text{in}}$ and for every subset of vertices $X \subseteq V$, the following inequality holds:
$$
\sum_{i \in X} k^{\text{out}}_i \le \sum_{j \notin X} \min(|X|, k^{\text{in}}_j) + \sum_{j \in X} \min(|X|-1, k^{\text{in}}_j)
$$
The logic mirrors the undirected case. The left side is the total number of arcs that must originate from vertices in $X$. The right side is the maximum capacity for these arcs to terminate. The first term on the right bounds the capacity of arcs terminating outside $X$, while the second term bounds the capacity of arcs terminating inside $X$. The crucial $|X|-1$ term appears because arcs from $i \in X$ to $j \in X$ are only possible if $i \neq j$, ruling out self-loops. Just as with the undirected case, a constructive algorithm analogous to Havel-Hakimi also exists, which succeeds if and only if these conditions are met .