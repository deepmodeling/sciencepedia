## Introduction
In an interconnected world, from social networks to the intricate wiring of the brain, we are surrounded by complex systems defined by their relationships. To move beyond mere observation and begin a rigorous analysis of these systems, we require a formal language—and that language is graph theory. It provides the mathematical toolkit to abstract entities and their connections into a structure we can measure, manipulate, and reason about. This article bridges the gap between the conceptual idea of a 'network' and its precise mathematical and computational representation.

Over the next three chapters, you will build a comprehensive understanding of this powerful field. The first chapter, **Principles and Mechanisms**, establishes the foundational vocabulary, defining graphs from first principles and exploring their various types and [matrix representations](@entry_id:146025). Following this, **Applications and Interdisciplinary Connections** will demonstrate how these abstract concepts are applied to solve real-world problems in biology, AI, and engineering. Finally, **Hands-On Practices** will solidify your knowledge with practical exercises that reinforce key theoretical concepts. We begin by laying the formal groundwork that makes all subsequent analysis possible.

## Principles and Mechanisms

This chapter delineates the fundamental principles of graph theory, establishing a formal vocabulary for describing networks. We move from the foundational set-theoretic definitions of nodes and edges to a [taxonomy](@entry_id:172984) of graph types, their [matrix representations](@entry_id:146025), and key structural properties. Our objective is to build a rigorous and systematic understanding of the mathematical objects used to model complex systems.

### The Formal Definition of a Graph

At its core, a graph, or network, is a mathematical abstraction used to represent relationships between objects. Formally, a graph is an [ordered pair](@entry_id:148349) $G=(V, E)$, where $V$ is a finite set of elements called **vertices** or **nodes**, and $E$ is a set representing the connections between them, called **edges** or **links**. The specific nature of $E$ determines the most fundamental properties of the graph.

#### Undirected Graphs: The Primacy of Unordered Pairs

In the simplest and most common type of graph, a **simple [undirected graph](@entry_id:263035)**, the relationships are symmetric. If vertex $u$ is connected to vertex $v$, then $v$ is equivalently connected to $u$. This symmetry is captured by defining an edge as an unordered pair of distinct vertices. Formally, the edge set $E$ is a subset of $\binom{V}{2}$, where $\binom{V}{2}$ denotes the set of all 2-element subsets of $V$:
$$E \subseteq \binom{V}{2} = \{\{u, v\} : u, v \in V, u \neq v\}$$
This elegant set-theoretic definition inherently imposes two crucial constraints that characterize a [simple graph](@entry_id:275276) . First, since the elements of $E$ are sets of size two, an edge must connect two *distinct* vertices, which forbids **loops** (edges connecting a vertex to itself). Second, because $E$ is a *set*, it cannot contain duplicate elements. This forbids **parallel edges** (multiple edges connecting the same pair of vertices).

An equivalent formalization, often used in [algebraic graph theory](@entry_id:274338), defines an undirected edge as a symmetric, irreflexive [binary relation](@entry_id:260596) on $V$. In this view, the edge set is a subset of the Cartesian product $V \times V$ that satisfies two conditions: symmetry (if $(u, v) \in E$, then $(v, u) \in E$) and irreflexivity (for all $v \in V$, $(v, v) \notin E$). This perspective directly corresponds to representing the graph with a symmetric adjacency matrix with a zero diagonal, a concept we will explore later.

#### Directed Graphs: Capturing Asymmetry

Many real-world systems, from [food webs](@entry_id:140980) to the World Wide Web, are characterized by asymmetric relationships. To model such systems, we use **[directed graphs](@entry_id:272310)**, or **[digraphs](@entry_id:269385)**. In a [digraph](@entry_id:276959), connections have a specific orientation. This is formalized by defining edges, now called **arcs**, as *[ordered pairs](@entry_id:269702)* of vertices. The arc set $A$ is a subset of the Cartesian product $V \times V$:
$$A \subseteq V \times V = \{(u, v) : u, v \in V\}$$
Here, an arc $(u,v)$ represents a connection *from* $u$ (the tail) *to* $v$ (the head). Crucially, the existence of $(u,v)$ does not imply the existence of $(v,u)$ . Since $A$ is a set, this definition naturally permits at most one arc between any [ordered pair](@entry_id:148349) of vertices.

Similar to [simple graphs](@entry_id:274882), a **loopless [directed graph](@entry_id:265535)** is one that forbids arcs of the form $(v,v)$. This is achieved by restricting the arc set to be a subset of $(V \times V) \setminus \Delta$, where $\Delta = \{(v,v) : v \in V\}$ is the set of all possible loops .

### A Taxonomy of Graph Types

The universe of graphs extends beyond the simple and loopless directed variants. By relaxing the constraints on loops and parallel edges, we arrive at a broader taxonomy of graph structures essential for modeling diverse phenomena.

#### Loops and Parallel Edges

The key features that distinguish graph types are the permissions for loops and parallel edges. Based on these, we can classify [undirected graphs](@entry_id:270905) into three primary categories :

1.  **Simple Graph**: Disallows both loops and parallel edges. As defined previously, the edge set $E$ is a simple set of 2-element subsets of $V$.

2.  **Multigraph**: Allows parallel edges but disallows loops. The connections between any two vertices are no longer a binary "yes/no" but can have a [multiplicity](@entry_id:136466) greater than one.

3.  **Pseudograph**: Allows both parallel edges and loops. This is the most general form of an [undirected graph](@entry_id:263035).

These distinctions are not merely pedantic; they are critical for accurately modeling systems. For example, a transportation network might have multiple distinct roads (parallel edges) between two cities, and a [protein-protein interaction network](@entry_id:264501) might include proteins that interact with themselves (loops).

#### Formalizing Multiplicity

To accommodate parallel edges in multigraphs and pseudographs, we must refine our formal definition of the edge set. Two standard and equivalent approaches exist :

1.  **Multiplicity Function**: One method is to define the graph as a pair $(V, m)$, where $m$ is a function that maps each possible unordered pair of vertices to a non-negative integer representing the number of edges between them. For a [multigraph](@entry_id:261576) (no loops), the function is $m: \binom{V}{2} \to \mathbb{N}_0$, where $\mathbb{N}_0 = \{0, 1, 2, \dots\}$. The value $m(\{u,v\})$ gives the multiplicity of the edge connecting $u$ and $v$. This is a compact and powerful representation.

2.  **Incidence Map**: An alternative is to define a graph as a triple $(V, E, \psi)$, where $E$ is an abstract set of edge identifiers, and $\psi$ is an incidence map. For a [multigraph](@entry_id:261576), $\psi: E \to \binom{V}{2}$ maps each edge identifier to the pair of vertices it connects. In this model, parallel edges are distinct elements of $E$ that map to the same vertex pair under $\psi$. The multiplicity of the edge $\{u,v\}$ is then unambiguously given by the size of the [preimage](@entry_id:150899), $|\psi^{-1}(\{u,v\})|$. This formulation is useful as it grants a unique identity to each edge, which can be critical for certain algorithms and models.

### Representing Graphs as Matrices

While set-theoretic definitions provide formal rigor, algebraic representations are essential for computational analysis. The two most fundamental [matrix representations](@entry_id:146025) are the [adjacency matrix](@entry_id:151010) and the [incidence matrix](@entry_id:263683).

#### The Adjacency Matrix

The **[adjacency matrix](@entry_id:151010)** $A$ of a graph with $n = |V|$ vertices is an $n \times n$ matrix that encodes direct connections between vertices. For a simple undirected graph, its entries are defined as:
$$
A_{ij} = \begin{cases} 1  \text{if } \{i,j\} \in E \\ 0  \text{otherwise} \end{cases}
$$
By this definition, $A$ for an [undirected graph](@entry_id:263035) is always **symmetric** ($A_{ij} = A_{ji}$) and, for a [simple graph](@entry_id:275276), has a **zero diagonal** ($A_{ii} = 0$) because loops are forbidden . For a [directed graph](@entry_id:265535), $A_{ij}=1$ if $(i,j)$ is an arc, so the matrix is not necessarily symmetric. For [weighted graphs](@entry_id:274716), the entry $A_{ij}$ is often set to the weight of the edge between $i$ and $j$.

#### The Incidence Matrix

The **incidence matrix** $B$ encodes the relationship between vertices and edges. For a graph with $n$ vertices and $m$ edges, $B$ is an $n \times m$ matrix. For a simple [undirected graph](@entry_id:263035), its entries can be defined as $B_{ve} = 1$ if vertex $v$ is an endpoint of edge $e$, and $0$ otherwise.

A more powerful variant for theoretical purposes is the **signed incidence matrix**. For an undirected graph, we can impose an arbitrary orientation on each edge, designating one endpoint as the "tail" and the other as the "head." The entries of the signed incidence matrix $B$ are then defined for a vertex $v$ and an edge $e$ as:
$$
B_{ve} = \begin{cases} -1  \text{if } v \text{ is the tail of } e \\ +1  \text{if } v \text{ is the head of } e \\ 0  \text{if } v \text{ is not an endpoint of } e \end{cases}
$$
The choice of which sign corresponds to tail versus head is a convention, but consistency is key. A remarkable result connects these [matrix representations](@entry_id:146025). The product $BB^\top$ yields an $n \times n$ matrix known as the **graph Laplacian**, $L$. Its entries are given by $(BB^\top)_{ij} = \sum_{e \in E} B_{ie}B_{je}$. A careful derivation reveals :
*   **Diagonal entries ($i=j$):** $(BB^\top)_{ii} = \sum_{e \in E} (B_{ie})^2$, which sums to 1 for every edge incident to vertex $i$. This is exactly the **degree** of vertex $i$, denoted $\deg(i)$.
*   **Off-diagonal entries ($i \neq j$):** $(BB^\top)_{ij}$ is $-1$ if an edge exists between $i$ and $j$, and $0$ otherwise. This is exactly $-A_{ij}$.

This gives the fundamental identity $BB^\top = D - A$, where $D$ is the [diagonal matrix](@entry_id:637782) of vertex degrees. This relationship bridges the vertex-edge incidence structure and the vertex-vertex adjacency structure, and the Laplacian matrix $L = D-A$ is a cornerstone of spectral graph theory.

### Attributes and Generalizations

To capture the rich complexity of real-world systems, the basic graph structure is often augmented with additional data or generalized to represent [higher-order interactions](@entry_id:263120).

#### Weighted Graphs

In many networks, connections are not all equal. They may represent capacities, distances, probabilities, or interaction strengths. A **[weighted graph](@entry_id:269416)** formalizes this by augmenting the graph structure with a weight function $w: E \to \mathbb{R}$ that assigns a real-valued weight to each edge .

It is crucial to distinguish **edge weights** from **node attributes**. A node attribute is a property intrinsic to a vertex, modeled as a function $a: V \to \mathcal{A}$ for some attribute space $\mathcal{A}$. While one can *derive* an edge weight from the attributes of its incident nodes (e.g., $\tilde{w}(\{u,v\}) = \phi(a(u), a(v))$ for some function $\phi$), the resulting object is formally a [weighted graph](@entry_id:269416). This distinction is not merely semantic; mathematical operators like the graph Laplacian are defined in terms of edge weights, regardless of their origin. Modeling a system with derived edge weights versus a system with the underlying node attributes are formally distinct choices with significant implications, especially when considering dynamic processes or interventions on the network . For instance, in a disease spreading model where [transmission probability](@entry_id:137943) $p_{uv}$ depends on node susceptibilities $s(u), s(v)$ and a contact intensity $\lambda(\{u,v\})$, storing only the final probability $p_{uv}$ as an edge weight loses the information required to predict the effect of an intervention that changes a node's susceptibility.

#### Hypergraphs: Beyond Pairwise Interactions

Many interactions in biological, social, and technological systems are not pairwise but involve groups of three or more actors. A **hypergraph** is a powerful generalization of a graph designed to model these [higher-order interactions](@entry_id:263120). Formally, a hypergraph is a pair $H = (V, \mathcal{E})$, where $V$ is a set of vertices and $\mathcal{E}$ is a family of subsets of $V$, called **hyperedges**. Each hyperedge $e \in \mathcal{E}$ can be of any [cardinality](@entry_id:137773), directly representing a group interaction . A [simple graph](@entry_id:275276) is just a special case where all hyperedges have a [cardinality](@entry_id:137773) of 2 (a 2-uniform hypergraph).

A common way to analyze a hypergraph is to project it onto a simple graph. The **2-section** of a hypergraph $H$, denoted $G_2(H)$, is a graph on the same vertex set $V$ where an edge $\{u,v\}$ exists if and only if there is at least one hyperedge in $H$ that contains both $u$ and $v$. This projection is inherently lossy; for example, a hypergraph with a single hyperedge $\{u,v,w\}$ and a hypergraph with three hyperedges $\{u,v\}, \{v,w\}, \{u,w\}$ both project to the same 2-section (a triangle), despite representing fundamentally different interaction structures .

The structure of a hypergraph can be perfectly captured by its **incidence bipartite graph** $B(H)$, whose vertex set is partitioned into $V$ and $\mathcal{E}$, with an edge connecting $v \in V$ and $e \in \mathcal{E}$ if and only if $v \in e$. This construction provides a lossless representation of the hypergraph's structure in the familiar form of a simple graph .

#### Multiplex Networks: Layered Systems

Complex systems are often composed of multiple types of relationships coexisting on the same set of entities. A **multiplex network** is a framework for modeling such layered systems. It is defined as a family of graphs $\{G^{(1)}, G^{(2)}, \dots, G^{(L)}\}$, each representing a different "layer" of interaction, but all sharing the same common vertex set $V$ .

In this framework, we distinguish two types of edges:
*   **Intralayer edges**: These are the conventional edges within each layer, described by the edge sets $E^{(\ell)}$ for each layer $\ell$.
*   **Interlayer couplings**: These are edges connecting the representation of the *same* vertex across different layers. For a node-aligned multiplex, these are edges connecting $(v_i, \ell)$ to $(v_i, \ell')$ for different layers $\ell$ and $\ell'$.

The entire system can be represented by a **supra-graph**, a single large graph whose vertices are the node-layer pairs $(v_i, \ell)$. The adjacency matrix of this supra-graph, $\mathcal{A}$, has a block structure where the diagonal blocks are the intralayer adjacency matrices $A^{(\ell)}$, and the off-diagonal blocks encode the interlayer couplings . This structure allows for a holistic analysis of how interactions in one layer influence and are influenced by interactions in others.

### Fundamental Structural Properties and Classes

Certain structural properties and graph classes are so ubiquitous and important that they form a core part of the graph theorist's toolkit.

#### Connectivity

The concept of connectivity describes whether and how vertices in a graph are connected by paths.

In an undirected graph, the concept is straightforward: a graph is **connected** if there is a path between every pair of distinct vertices. If not, it decomposes into several **[connected components](@entry_id:141881)**.

In [directed graphs](@entry_id:272310), the situation is more nuanced. We define two principal types of connectivity :
*   **Weak Connectivity**: A directed graph is weakly connected if its underlying [undirected graph](@entry_id:263035) (formed by ignoring all edge directions) is connected. This means there is a path between any two vertices, but not necessarily one that respects edge directions.
*   **Strong Connectivity**: A [directed graph](@entry_id:265535) is strongly connected if for every [ordered pair](@entry_id:148349) of vertices $(u, v)$, there is a directed path from $u$ to $v$. This is a much stricter condition.

The [mutual reachability](@entry_id:263473) relation ($u \leftrightsquigarrow v$ if $u$ can reach $v$ and $v$ can reach $u$) is an [equivalence relation](@entry_id:144135) on the vertices of a [digraph](@entry_id:276959). The [equivalence classes](@entry_id:156032) of this relation partition the vertex set into **Strongly Connected Components** (SCCs). Within each SCC, every node can reach every other node.

The global structure of a [digraph](@entry_id:276959) can be understood by examining its **[condensation graph](@entry_id:261832)**, which is formed by contracting each SCC into a single supernode. An arc exists between two supernodes if there was an arc in the original graph between any two vertices in the corresponding SCCs. A fundamental result is that the [condensation graph](@entry_id:261832) is always a **Directed Acyclic Graph (DAG)** .

#### Bipartite Graphs

A **[bipartite graph](@entry_id:153947)** is a graph whose vertices can be divided into two disjoint and [independent sets](@entry_id:270749), $U$ and $W$, such that every edge connects a vertex in $U$ to one in $W$. No edge connects two vertices within the same set.

Bipartite graphs have a simple and profound characterization related to their [cycle structure](@entry_id:147026): **a graph is bipartite if and only if it contains no cycles of odd length** . To see why, consider a path in a [bipartite graph](@entry_id:153947) starting in set $U$. Each step moves to the other set. To form a cycle by returning to the starting vertex, one must take an even number of steps. Thus, all cycles are of even length. Conversely, if a graph has no [odd cycles](@entry_id:271287), one can construct a valid bipartition, proving the equivalence. This property makes them central to matching problems and certain types of scheduling.

#### Directed Acyclic Graphs (DAGs)

A **Directed Acyclic Graph (DAG)** is a [directed graph](@entry_id:265535) that contains no directed cycles. DAGs are fundamental for modeling systems with dependencies, causal relationships, or hierarchical structures, such as project task schedules, [citation networks](@entry_id:1122415), or computational workflows.

The absence of cycles endows DAGs with special properties. The [reachability](@entry_id:271693) relation in a DAG forms a **[partial order](@entry_id:145467)** on its vertices . Furthermore, a key operational property of a DAG is that its vertices can be arranged in a **topological ordering**—a linear ordering of vertices such that for every directed edge from $u$ to $v$, vertex $u$ comes before vertex $v$ in the ordering. A [directed graph](@entry_id:265535) admits a topological ordering if and only if it is a DAG . This property stems from another basic fact: every non-empty finite DAG must have at least one vertex with in-degree 0 (a "source") and at least one vertex with out-degree 0 (a "sink").

### Relations Between Graphs: Isomorphism and Homomorphism

When comparing two different graphs, we often need to determine if they are structurally the same or how one can be mapped onto another.

A **[graph isomorphism](@entry_id:143072)** is the most stringent form of structural equivalence. An [isomorphism](@entry_id:137127) between two graphs $G=(V, E)$ and $G'=(V', E')$ is a [bijection](@entry_id:138092) $f: V \to V'$ that preserves adjacency: $\{u, v\} \in E$ if and only if $\{f(u), f(v)\} \in E'$. If such a mapping exists, the graphs are said to be **isomorphic**. Isomorphic graphs are identical from a structural standpoint, merely differing in the labels of their vertices . An isomorphism from a graph to itself is called an **[automorphism](@entry_id:143521)**. The set of all [automorphisms](@entry_id:155390) of a graph forms a group, the **[automorphism group](@entry_id:139672)**, which captures the graph's symmetries.

A more relaxed notion is that of a **[graph homomorphism](@entry_id:272314)**. A homomorphism from a graph $G=(V,E)$ to a graph $H=(W,F)$ is a function $h:V \to W$ that preserves edges, meaning if $\{u,v\} \in E$, then $\{h(u), h(v)\} \in F$. Unlike an isomorphism, a homomorphism need not be bijective, and the adjacency preservation is only required in one direction. A notable application of this concept is in [graph coloring](@entry_id:158061). A proper $k$-coloring of a graph $G$ is equivalent to a homomorphism from $G$ to the complete graph $K_k$ . For instance, a graph is bipartite (2-colorable) if and only if there exists a homomorphism from it to $K_2$.