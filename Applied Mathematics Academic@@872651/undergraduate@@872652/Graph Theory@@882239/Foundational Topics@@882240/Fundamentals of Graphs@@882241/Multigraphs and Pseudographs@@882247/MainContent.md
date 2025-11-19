## Introduction
While [simple graphs](@entry_id:274882) provide a powerful foundation for modeling relationships, many real-world networks exhibit a complexity that surpasses their limitations. Transportation systems feature multiple routes between the same two hubs, computer programs contain functions that call themselves, and communication networks rely on redundant links for reliability. These scenarios cannot be accurately captured by a model that forbids multiple connections and self-references. This gap necessitates more expressive tools: **multigraphs** and **pseudographs**.

This article provides a comprehensive introduction to these essential graph structures. We will bridge the knowledge gap between [simple graphs](@entry_id:274882) and the complex networks they fail to represent. First, the **Principles and Mechanisms** chapter will formally define multigraphs and pseudographs, exploring how fundamental concepts like [vertex degree](@entry_id:264944) and the Handshaking Lemma are adapted. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate their indispensable role in modeling everything from transit systems to software architecture. Finally, the **Hands-On Practices** section offers practical problems to solidify your understanding of these versatile models. We begin by establishing the formal definitions and core properties that distinguish these graphs from their simpler counterparts.

## Principles and Mechanisms

As we move beyond the foundational concepts of [simple graphs](@entry_id:274882), we encounter systems and problems that require a more expressive graphical language. Real-world networks frequently feature multiple distinct relationships between the same two entities or entities that interact with themselves. A transportation map might show several different train lines connecting the same two stations. A computer network may have redundant data links between two critical servers. A function in a computer program might call itself recursively. To model such scenarios accurately, we must generalize the concept of a graph to include multiple edges and self-loops. This leads us to the study of **multigraphs** and **pseudographs**.

### A Hierarchy of Graphs: Expanding the Definitions

The fundamental distinction between different types of graphs lies in the rules they impose on their edge sets. A **simple graph**, as previously discussed, is the most restrictive. It is formally a pair $G=(V, E)$ where $V$ is a set of vertices and $E$ is a set of two-element subsets of $V$. This definition inherently forbids two types of connections:
1.  **Multiple Edges**: More than one edge connecting the same pair of vertices.
2.  **Loops**: An edge connecting a vertex to itself.

To model more complex systems, we selectively relax these restrictions.

A **[multigraph](@entry_id:261576)** is a graph that allows multiple edges between two distinct vertices but still forbids loops. Formally, we can define a [multigraph](@entry_id:261576) as an ordered triple $G=(V, E, \phi)$ where $V$ is a set of vertices, $E$ is a multiset of edges, and $\phi$ is an incidence function that maps each edge in $E$ to an unordered pair of *distinct* vertices from $V$. The existence of multiple edges connecting the same two vertices, say $u$ and $v$, means that the multiset $E$ can contain several distinct edge elements, $e_1, e_2, \ldots, e_k$, such that $\phi(e_1) = \phi(e_2) = \cdots = \phi(e_k) = \{u, v\}$. These edges are often called **parallel edges**.

A **[pseudograph](@entry_id:273987)** is the most general type of [undirected graph](@entry_id:263035), allowing both multiple edges and loops. In a [pseudograph](@entry_id:273987), the incidence function $\phi$ can map an edge to an unordered pair of vertices that are not necessarily distinct. An edge $e$ for which $\phi(e) = \{v, v\}$ for some vertex $v \in V$ is called a **loop**.

This creates a clear hierarchy based on set inclusion. The set of all [simple graphs](@entry_id:274882) is a [proper subset](@entry_id:152276) of the set of all multigraphs, which in turn is a [proper subset](@entry_id:152276) of the set of all pseudographs. Any graph that adheres to a stricter set of rules is, by definition, compliant with a more permissive set. For example, any simple graph can be considered a [multigraph](@entry_id:261576) (where all edge multiplicities are 1) and a [pseudograph](@entry_id:273987) (with no loops). Similarly, any [multigraph](@entry_id:261576) is also a [pseudograph](@entry_id:273987) (one that happens to have no loops) [@problem_id:1400562].

The essential feature that distinguishes a [pseudograph](@entry_id:273987) from a [multigraph](@entry_id:261576) is the presence of at least one loop. The smallest possible [pseudograph](@entry_id:273987) that is *not* a [multigraph](@entry_id:261576) consists of a single vertex and a single loop on that vertex [@problem_id:1400588]. Formally, this graph is described by $V = \{v_1\}$ and an edge multiset $E = \{\{v_1, v_1\}\}$.

The capacity of these graph types to hold edges differs significantly. Consider a set of $n$ vertices.
- The maximum number of edges in a **[simple graph](@entry_id:275276)** is the number of ways to choose two distinct vertices, which is $E_S = \binom{n}{2}$.
- In a **[multigraph](@entry_id:261576)** where we allow up to $k$ parallel edges between any pair of distinct vertices, the maximum number of edges becomes $E_M = k \binom{n}{2}$.
- In a **[pseudograph](@entry_id:273987)** with the same multiplicity constraint $k$ and an additional allowance of up to $m$ loops at each vertex, the maximum number of edges is the sum of the maximum non-loop edges and the maximum loop edges: $E_P = k \binom{n}{2} + mn$.

For instance, on a set of $n=5$ vertices, a simple graph has at most $\binom{5}{2} = 10$ edges. A [multigraph](@entry_id:261576) allowing up to $k=4$ edges between any pair has at most $4 \times 10 = 40$ edges. A [pseudograph](@entry_id:273987) with these constraints plus a maximum of $m=2$ loops per vertex can have up to $40 + (2 \times 5) = 50$ edges [@problem_id:1400564].

### Redefining Vertex Degree

The concept of a vertex's degree must be carefully defined to be meaningful for multigraphs and pseudographs. The **degree** of a vertex $v$, denoted $\deg(v)$, is the total number of edge ends incident to it. This definition has a critical implication for loops:

**A loop at a vertex $v$ contributes 2 to $\deg(v)$.**

This convention is not arbitrary. A loop is a single edge, but it connects to its vertex at both of its "ends". This definition ensures that the fundamental Handshaking Lemma is preserved across all graph types.

The **Handshaking Lemma** for pseudographs states that the sum of the degrees of all vertices in a finite graph is equal to twice the number of edges:
$$ \sum_{v \in V} \deg(v) = 2|E| $$
This holds because every non-loop edge contributes 1 to the degree of its two distinct endpoints (totaling 2 to the sum), and every loop contributes 2 to the degree of its single vertex. Since every edge in the graph $E$ contributes exactly 2 to the total degree sum, the identity holds. A direct and powerful corollary is that **the number of vertices with an odd degree in any finite [pseudograph](@entry_id:273987) must be even** [@problem_id:1522863]. A proposed graph with a degree sequence of $\{1, 2, 3, 3\}$ cannot exist because it has three odd-degree vertices, and its degree sum is $1+2+3+3=9$, an odd number that cannot equal $2|E|$.

The expanded definition of degree allows for structures not possible in [simple graphs](@entry_id:274882). For example, a vertex $v$ can have $\deg(v)=4$ while being **adjacent** (connected by at least one edge) to only two other vertices, $u$ and $w$. This can be achieved in a [multigraph](@entry_id:261576) by having, for instance, two edges between $v$ and $u$ and two edges between $v$ and $w$. It can also be achieved in a [pseudograph](@entry_id:273987) by having one edge to $u$, one to $w$, and one loop at $v$, giving $\deg(v) = 1 + 1 + 2 = 4$ [@problem_id:1495452]. In a simple graph, however, the [degree of a vertex](@entry_id:261115) is always equal to the number of its adjacent vertices.

### A Note on Definitions: The Impact of Loop Counting

The robustness of graph-theoretic principles often relies on careful and consistent definitions. The standard convention of counting a loop as 2 towards the degree is a prime example. To see why, consider a non-standard definition where a loop contributes only 1 to its vertex's degree.

Let's analyze a network under this alternative rule [@problem_id:1400587]. Let $M$ be the number of non-loop edges and $N_L$ be the number of loops. Each non-loop edge contributes 2 to the total degree sum, while each loop now contributes 1. The degree sum identity becomes:
$$ \sum_{v \in V} \deg(v) = 2M + N_L $$
In this system, the sum of degrees is no longer guaranteed to be an even number. Its parity is the same as the parity of $N_L$, the number of loops. If we were to design a $k$-regular network on $n$ vertices where both $k$ and $n$ are odd, the sum of degrees would be $nk$, an odd number. For the identity $nk = 2M + N_L$ to hold, $N_L$ must also be an odd number. This demonstrates that changing a fundamental definition can drastically alter a graph's properties. The standard definition ($\text{loop} \to 2$) is preferred in mainstream graph theory precisely because it preserves the elegant and powerful property that the sum of degrees is always even.

### Representing Multigraphs and Pseudographs

Representing these more complex graphs requires [data structures](@entry_id:262134) that can encode information about edge multiplicity and loops.

#### Adjacency Matrix

The [adjacency matrix](@entry_id:151010) $A$ of a [pseudograph](@entry_id:273987) with $n$ vertices is an $n \times n$ matrix where the entries are non-negative integers.
- For $i \neq j$, the entry $A_{ij}$ is the number of edges connecting vertex $v_i$ and vertex $v_j$. Since the graphs are undirected, $A_{ij} = A_{ji}$.
- The diagonal entry $A_{ii}$ is the number of loops at vertex $v_i$.

From this matrix, we can extract key properties. The total number of loops, $L$, is simply the sum of the diagonal entries, which is the trace of the matrix:
$$ L = \sum_{i=1}^{n} A_{ii} = \operatorname{tr}(A) $$
The total number of edges, $|E|$, is the sum of all loops plus the sum of all non-loop edges. To count the non-loop edges without duplication, we sum the entries in the upper (or lower) triangle of the matrix. This gives the formula:
$$ |E| = \sum_{i=1}^{n} A_{ii} + \sum_{1 \le i  j \le n} A_{ij} $$
Alternatively, this can be expressed as $|E| = \frac{1}{2}\left(\sum_{i=1}^{n} \sum_{j=1}^{n} A_{ij} + \sum_{i=1}^{n} A_{ii}\right)$ [@problem_id:1522861].

The powers of the adjacency matrix retain their meaning as counting walks. The entry $(A^k)_{ij}$ gives the number of distinct walks of length $k$ from $v_i$ to $v_j$. For a [pseudograph](@entry_id:273987), this accounts for all possible paths, including those using parallel edges and loops. For example, the diagonal entry $(A^2)_{ii}$ counts the number of walks of length 2 that start and end at vertex $v_i$. Such a walk can be formed by traversing an edge to a neighbor $v_k$ and immediately returning, or by traversing a loop. The formula is $(A^2)_{ii} = \sum_{k=1}^n A_{ik}A_{ki}$. Since $A$ is symmetric, this becomes $(A^2)_{ii} = \sum_{k=1}^n A_{ik}^2$.

Consider a researcher, Dr. Reed, represented by vertex $r$. She has 3 loops (self-review processes), 4 parallel edges to a colleague Dr. Carter (vertex $c$), and 1 edge to a supervisor Dr. Flores (vertex $f$) [@problem_id:1400605]. The relevant matrix entries are $A_{rr}=3$, $A_{rc}=4$, and $A_{rf}=1$. The number of 2-step walks from Dr. Reed back to herself is:
$$ (A^2)_{rr} = A_{rr}^2 + A_{rc}^2 + A_{rf}^2 = 3^2 + 4^2 + 1^2 = 9 + 16 + 1 = 26 $$
These 26 walks consist of: 9 walks using one loop and then another (or the same one again), 16 walks by going to Dr. Carter via one of the 4 channels and returning via any of the 4, and 1 walk by going to Dr. Flores and returning.

#### Adjacency List

Using an [adjacency list](@entry_id:266874) for a [pseudograph](@entry_id:273987) presents a unique challenge: distinguishing between multiple edges connecting the same two vertices. A simple list of neighboring vertex indices, e.g., `adj[v] = [u, u, w]`, is ambiguous. If we wish to delete one of the edges to `u`, which one do we mean?

To uniquely represent any [pseudograph](@entry_id:273987), the data structure must be able to identify each edge individually. Storing aggregated counts, such as `(neighbor, count)`, is also insufficient for this purpose. A robust solution is for the [adjacency list](@entry_id:266874) of a vertex `v`, `adj[v]`, to contain an entry for each *edge* incident to it. Each entry is a pair `(w, edge_id)`, where `w` is the other endpoint of the edge (or `v` itself for a loop), and `edge_id` is a unique identifier for that specific edge instance [@problem_id:1400561].

With such a structure, calculating the [degree of a vertex](@entry_id:261115) `v` requires iterating through its [adjacency list](@entry_id:266874). We would iterate through the list, adding 1 to a running total for each entry `(w, edge_id)` where $w \neq v$, and adding 2 for each entry where $w = v$. This computation correctly determines the degree and takes time proportional to the number of edges incident to $v$.

### Isomorphism in Multigraphs

The concept of **[isomorphism](@entry_id:137127)**—structural equivalence—becomes more nuanced with multigraphs. Two [simple graphs](@entry_id:274882) are isomorphic if there is a vertex [bijection](@entry_id:138092) that preserves adjacency. For multigraphs and pseudographs, this bijection must also preserve the number of edges between corresponding pairs of vertices.

**Two multigraphs $G_1=(V_1, E_1)$ and $G_2=(V_2, E_2)$ are isomorphic** if there exists a [bijection](@entry_id:138092) $f: V_1 \to V_2$ such that the multiplicity of the edge $\{u, v\}$ in $G_1$ is equal to the multiplicity of the edge $\{f(u), f(v)\}$ in $G_2$ for all pairs of vertices $u, v \in V_1$.

This stricter condition reveals an important property: the degree sequence is a weaker invariant for multigraphs than it is for [simple graphs](@entry_id:274882). It is possible for two multigraphs to be non-isomorphic even if they have the same number of vertices, the same number of edges, the same underlying [simple graph](@entry_id:275276), and the exact same degree sequence.

The reason for this is that the *distribution* of edge multiplicities matters. Consider two multigraphs built upon a 4-cycle $v_1-v_2-v_3-v_4-v_1$ [@problem_id:1522848].
- **Graph A:** Multiplicities for edges $(e_{12}, e_{23}, e_{34}, e_{41})$ are $(2, 2, 1, 2)$.
- **Graph B:** Multiplicities are $(3, 1, 2, 1)$.

Let's calculate their degree sequences:
- **Graph A:** $\deg(v_1)=2+2=4$, $\deg(v_2)=2+2=4$, $\deg(v_3)=2+1=3$, $\deg(v_4)=1+2=3$. Sequence: $\{4, 4, 3, 3\}$.
- **Graph B:** $\deg(v_1)=3+1=4$, $\deg(v_2)=3+1=4$, $\deg(v_3)=1+2=3$, $\deg(v_4)=2+1=3$. Sequence: $\{4, 4, 3, 3\}$.

Both graphs have the same underlying simple graph ($C_4$) and the same [degree sequence](@entry_id:267850). However, they cannot be isomorphic. A necessary condition for [isomorphism](@entry_id:137127) is that the multiset of all edge multiplicities must be the same. For Graph A, this multiset is $\{1, 2, 2, 2\}$. For Graph B, it is $\{1, 1, 2, 3\}$. Since these multisets are different, no [isomorphism](@entry_id:137127) can exist. This example powerfully illustrates that to confirm structural equivalence in multigraphs, one must look beyond simple invariants like the [degree sequence](@entry_id:267850) and consider the specific arrangement of edge multiplicities.