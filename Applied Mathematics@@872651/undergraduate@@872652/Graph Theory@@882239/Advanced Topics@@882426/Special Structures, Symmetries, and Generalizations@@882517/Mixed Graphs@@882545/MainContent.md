## Introduction
In the study of networks and systems, we often encounter relationships that are not purely symmetric or asymmetric. While traditional graph theory provides powerful tools in the form of undirected and [directed graphs](@entry_id:272310), many real-world scenarios—from one-way streets in a city grid to enzymatic reactions in a protein network—demand a more flexible model. This limitation creates a gap where complex systems with hybrid interactions cannot be faithfully represented. Mixed graphs emerge as the solution, providing a unified framework that incorporates both undirected edges and directed arcs within a single structure. This article provides a comprehensive introduction to mixed graphs, designed to equip you with the theoretical knowledge and practical skills to leverage this powerful model. We will begin in the first chapter, "Principles and Mechanisms", by establishing the formal definitions, [matrix representations](@entry_id:146025), and fundamental properties of mixed graphs, including connectivity and coloring. Subsequently, "Applications and Interdisciplinary Connections" will showcase the versatility of these concepts by exploring their use in diverse fields like urban planning, computer science, and [systems biology](@entry_id:148549). Finally, the "Hands-On Practices" section will solidify your understanding by guiding you through a series of problems designed to apply these theoretical principles to concrete examples.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of mixed graphs as a generalization that incorporates both symmetric (undirected) and asymmetric (directed) relationships within a single structure. This flexibility makes them powerful tools for modeling a wide range of real-world systems, from communication networks and logistical chains to computational dependencies. This chapter delves into the fundamental principles and mechanisms that govern the structure and behavior of mixed graphs. We will explore how to represent them formally, analyze their elementary properties, and investigate more complex structural characteristics such as connectivity, colorability, and the existence of special traversals.

### Formal Definition and Matrix Representations

A **mixed graph** $G$ is formally defined as an ordered triple $G = (V, E, A)$, where $V$ is a [finite set](@entry_id:152247) of **vertices**, $E$ is a set of **undirected edges**, and $A$ is a set of **directed edges**, also known as **arcs**. An undirected edge is an unordered pair of vertices $\{u, v\}$, representing a symmetric link. An arc is an [ordered pair](@entry_id:148349) of vertices $(u, v)$, representing an asymmetric link from $u$ (the tail) to $v$ (the head).

For computational analysis, it is essential to translate this abstract structure into a concrete mathematical object, most commonly an adjacency matrix. A natural first step is to represent the undirected and directed components separately. For a graph with $n = |V|$ vertices, ordered as $(v_1, v_2, \dots, v_n)$, we can define:

1.  The **undirected adjacency matrix**, $U$, an $n \times n$ matrix where $U_{ij} = 1$ if $\{v_i, v_j\} \in E$, and $U_{ij} = 0$ otherwise. By definition, $U$ is a symmetric matrix, i.e., $U_{ij} = U_{ji}$.

2.  The **directed [adjacency matrix](@entry_id:151010)**, $A$, an $n \times n$ matrix where $A_{ij} = 1$ if $(v_i, v_j) \in A$, and $A_{ij} = 0$ otherwise. This matrix is not necessarily symmetric.

Consider a communication network with four data centers, $v_1, v_2, v_3, v_4$. One-way channels form a directed cycle $v_1 \to v_2 \to v_3 \to v_4 \to v_1$, and two-way channels connect $\{v_1, v_3\}$ and $\{v_2, v_4\}$. The corresponding matrices would be:
$$
A = \begin{pmatrix} 0  & 1  & 0  & 0 \\ 0  & 0  & 1  & 0 \\ 0  & 0  & 0  & 1 \\ 1  & 0  & 0  & 0 \end{pmatrix}, \quad U = \begin{pmatrix} 0  & 0  & 1  & 0 \\ 0  & 0  & 0  & 1 \\ 1  & 0  & 0  & 0 \\ 0  & 1  & 0  & 0 \end{pmatrix}
$$
While representing a mixed graph with a pair of matrices $(U, A)$ is unambiguous, it is often desirable to use a single matrix. A simple approach is to sum the two matrices, $M = U + A$. For the network above, this yields:
$$
M = U + A = \begin{pmatrix} 0  & 1  & 1  & 0 \\ 0  & 0  & 1  & 1 \\ 1  & 0  & 0  & 1 \\ 1  & 1  & 0  & 0 \end{pmatrix}
$$
This matrix, which we will call the **walk adjacency matrix**, proves useful for certain applications, as we will see later. However, as a general-purpose representation, it suffers from a critical flaw: ambiguity [@problem_id:1522692]. Consider two distinct vertices $v_i$ and $v_j$. If there is an undirected edge $\{v_i, v_j\}$ and no arcs between them, then $M_{ij} = 1$ and $M_{ji} = 1$. However, if there are no undirected edges but there are two opposing arcs, $(v_i, v_j)$ and $(v_j, v_i)$, we also get $M_{ij} = 1$ and $M_{ji} = 1$. The matrix $M=U+A$ cannot distinguish between these two fundamentally different network structures.

To create an unambiguous single-matrix representation, we must encode the information more carefully. One successful method is to assign different weights to undirected and directed edges. Let's define a new matrix $M'$ as $M' = 2U + A$ [@problem_id:1522689]. Let's analyze the entries $M'_{ij}$ and $M'_{ji}$ for any pair of distinct vertices $v_i, v_j$:
- If there is no connection: $M'_{ij} = 0, M'_{ji} = 0$.
- If there is only an arc $(v_i, v_j)$: $M'_{ij} = 1, M'_{ji} = 0$.
- If there is only an undirected edge $\{v_i, v_j\}$: $M'_{ij} = 2, M'_{ji} = 2$.
- If there is an undirected edge $\{v_i, v_j\}$ and an arc $(v_i, v_j)$: $M'_{ij} = 3, M'_{ji} = 2$.

In general, for any pair of entries $(M'_{ij}, M'_{ji})$, we can uniquely recover the connection state. The presence of an undirected edge is indicated if $\lfloor M'_{ij} / 2 \rfloor = 1$ (which will always equal $\lfloor M'_{ji} / 2 \rfloor$). The presence of an arc $(v_i, v_j)$ is indicated if the remainder $M'_{ij} \pmod 2 = 1$. This weighted scheme provides a robust and complete representation within a single matrix.

### Vertex Degrees and Fundamental Properties

The local structure at each vertex is characterized by its **degrees**. In a mixed graph, we distinguish three types of degrees for a vertex $v \in V$:

-   The **undirected degree**, denoted $deg_E(v)$, is the number of undirected edges incident to $v$.
-   The **in-degree**, denoted $deg_A^-(v)$, is the number of arcs in $A$ for which $v$ is the head.
-   The **out-degree**, denoted $deg_A^+(v)$, is the number of arcs in $A$ for which $v$ is the tail.

These definitions lead to fundamental relationships analogous to the [handshaking lemma](@entry_id:261183) for [simple graphs](@entry_id:274882). Summing the degrees over all vertices reveals properties of the entire graph. Each undirected edge $\{u, v\}$ contributes 1 to $deg_E(u)$ and 1 to $deg_E(v)$. Therefore, the sum of all undirected degrees is twice the number of undirected edges:
$$ \sum_{v \in V} deg_E(v) = 2|E| $$
Similarly, each arc $(u, v)$ contributes 1 to the [out-degree](@entry_id:263181) of its tail, $u$, and 1 to the in-degree of its head, $v$. Summing over all vertices, we find that the total sum of out-degrees must equal the total sum of in-degrees, and both are equal to the total number of arcs:
$$ \sum_{v \in V} deg_A^+(v) = \sum_{v \in V} deg_A^-(v) = |A| $$
This simple but powerful identity is a cornerstone of [directed graph](@entry_id:265535) theory and remains true for the directed part of a mixed graph. It can be used, for example, to determine unknown degree information in a network. If the in-degrees and out-degrees are known for all but one node, the missing degree can be calculated by enforcing this global balance [@problem_id:1522656].

For some analyses, it is useful to combine these measures into a single metric. The **total degree** of a vertex $v$ is defined as the sum of all connections involving it: $tdeg(v) = deg_E(v) + deg_A^-(v) + deg_A^+(v)$ [@problem_id:1522679]. By summing this quantity over all vertices and applying the previous identities, we obtain a [handshaking lemma](@entry_id:261183) for the total degree in a mixed graph:
$$ \sum_{v \in V} tdeg(v) = \sum_{v \in V} deg_E(v) + \sum_{v \in V} deg_A^-(v) + \sum_{v \in V} deg_A^+(v) = 2|E| + |A| + |A| = 2|E| + 2|A| $$
This shows that the sum of total degrees is always an even number, equal to twice the sum of the number of undirected edges and directed arcs.

### Walks, Paths, and Connectivity

Many applications of graph theory involve analyzing paths and connectivity. To extend these concepts to mixed graphs, we must first define how to traverse its edges and arcs.

A **mixed walk** of length $k$ is a sequence of vertices $v_0, v_1, \dots, v_k$ where for each step from $v_i$ to $v_{i+1}$, either $\{v_i, v_{i+1}\} \in E$ or $(v_i, v_{i+1}) \in A$. That is, one can traverse an undirected edge in either direction, but an arc only in its specified direction.

The number of such walks can be counted using [matrix exponentiation](@entry_id:265553). The appropriate matrix is the **walk [adjacency matrix](@entry_id:151010)** $M = U + A$ that we introduced earlier [@problem_id:1522654]. An entry $M_{ij}=1$ signifies that a single step is possible from $v_i$ to $v_j$. It is a well-established result that the entry $(M^k)_{ij}$ of the $k$-th power of this matrix gives the number of distinct mixed walks of length exactly $k$ from $v_i$ to $v_j$. Although this matrix is ambiguous for uniquely representing the graph's structure, it is perfectly suited for enumerating these one-way traversals.

A more fundamental notion of connectivity ignores the directionality of arcs. This is captured by the **underlying [undirected graph](@entry_id:263035)**, denoted $G_u$. This graph has the same vertex set $V$ as the mixed graph, but its edge set is formed by taking all of the original undirected edges and adding a new undirected edge for every arc. Formally, the edge set of $G_u$ is $E' = E \cup \{\{u, v\} \mid (u, v) \in A\}$. Care must be taken to treat the new set of edges $E'$ as a set, meaning duplicate edges are not counted [@problem_id:1522657].

Using this construction, we can define a basic level of connectivity. A mixed graph $G$ is said to be **weakly connected** if its underlying [undirected graph](@entry_id:263035) $G_u$ is connected [@problem_id:1522661]. This means that for any two vertices $u, v$ in the graph, there is a path between them in $G_u$, ignoring the original orientations of the arcs. This is often the first and most basic requirement for a network to be considered functional as a whole.

### Advanced Topics in Mixed Graphs

The rich structure of mixed graphs allows for the study of more complex problems that blend concepts from both undirected and directed graph theory.

#### Mixed Graph Coloring

Graph coloring is a classic problem with numerous applications, such as scheduling and resource allocation. For a mixed graph, the standard definition of a **proper $k$-coloring** is a function $c: V \to \{1, 2, \dots, k\}$ that assigns a color to each vertex such that any two adjacent vertices have different colors. Two vertices are considered adjacent if they are connected by an undirected edge or by an arc in either direction [@problem_id:1522691]. This definition effectively means that we are seeking a proper coloring of the underlying [undirected graph](@entry_id:263035) $G_u$. The **[chromatic number](@entry_id:274073)** of the mixed graph, $\chi(G)$, is therefore equal to $\chi(G_u)$.

However, the true modeling power of mixed graphs emerges when the coloring rules differ for edges and arcs. Consider a scheduling problem where vertices represent tasks, colors represent [discrete time](@entry_id:637509) slots, undirected edges represent resource conflicts (tasks cannot run simultaneously), and directed arcs represent dependencies (a task must run no later than another). This can be modeled by a coloring function $c$ with the following constraints [@problem_id:1522676]:
1.  For any undirected edge $\{u, v\} \in E$, we require $c(u) \neq c(v)$.
2.  For any directed arc $(u, v) \in A$, we require $c(u) \leq c(v)$.

If a pair of vertices $(u, v)$ is connected by both an undirected edge and a directed arc, the conditions combine to demand a strict temporal ordering: $c(u)  c(v)$. By tracing chains of such constraints, one can establish a lower bound on the number of required colors (time slots). For example, a sequence of dependencies and conflicts such as $v_1 \to v_2 \to \dots \to v_m$ where each adjacent pair also has a conflict will require at least $m$ distinct colors, as it implies $c(v_1)  c(v_2)  \dots  c(v_m)$. This type of specialized coloring is a powerful tool for solving complex scheduling and sequencing problems.

#### Mixed Eulerian Circuits

An **Eulerian circuit** is a trail that visits every link in a graph exactly once and returns to the starting vertex. This concept is vital in logistics, network diagnostics, and DNA sequencing. For a mixed graph, a **mixed Eulerian circuit** is a circuit that traverses every undirected edge and every directed arc exactly once, respecting the direction of the arcs.

The existence of such a circuit depends on delicate balance conditions at each vertex. A connected mixed graph $G = (V, E, A)$ has a mixed Eulerian circuit if and only if the undirected edges in $E$ can be oriented to form a set of arcs $E'$ such that the resulting fully [directed graph](@entry_id:265535) $(V, A \cup E')$ is Eulerian. This, in turn, requires that every vertex in the new graph is **balanced**, meaning its total in-degree equals its total out-degree.

Let's say for a vertex $v$, we choose to orient $x_v$ of its $d_E(v)$ incident undirected edges as outgoing arcs. The remaining $d_E(v) - x_v$ edges become incoming arcs. The balance condition at vertex $v$ is:
$$ \underbrace{d_A^+(v) + x_v}_{\text{Total out-degree}} = \underbrace{d_A^-(v) + (d_E(v) - x_v)}_{\text{Total in-degree}} $$
Solving for $x_v$ gives the number of undirected edges that *must* be oriented outwards from $v$:
$$ 2x_v = d_A^-(v) - d_A^+(v) + d_E(v) \implies x_v = \frac{d_A^-(v) - d_A^+(v) + d_E(v)}{2} $$
For a mixed Eulerian circuit to exist in a [connected graph](@entry_id:261731), two conditions must be met for every vertex $v \in V$ [@problem_id:1522659]:
1.  The quantity $d_A^-(v) - d_A^+(v) + d_E(v)$ must be an even integer. This ensures that $x_v$ is an integer.
2.  The calculated value of $x_v$ must be feasible, i.e., $0 \leq x_v \leq d_E(v)$.

These vertex-by-vertex conditions, combined with the global requirement that $\sum d_A^+(v) = \sum d_A^-(v)$, provide a complete characterization for the existence of mixed Eulerian circuits and serve as a powerful analytical tool for networks that blend symmetric and asymmetric processes.