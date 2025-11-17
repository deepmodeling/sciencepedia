## Introduction
In the realm of graph theory, a tournament represents a simple yet powerful abstraction: a model of a round-robin competition where every participant faces every other, and one must emerge as the victor. While seemingly straightforward, these [directed graphs](@entry_id:272310) possess a rich and often counterintuitive structure that has fascinated mathematicians for decades. Their study offers profound insights into ranking, dominance, and hierarchy, not only in sports but in fields as diverse as computer science, social choice theory, and [network analysis](@entry_id:139553). This article addresses the fundamental question: How can we rigorously analyze the outcomes of such competitions to uncover underlying patterns, identify dominant players, and understand their structural properties, even in the presence of paradoxical cycles?

This article provides a structured journey through the core concepts of tournament theory. In the first chapter, **Principles and Mechanisms**, we will establish the formal definitions and explore the foundational theorems governing scores, paths, and connectivity. Next, **Applications and Interdisciplinary Connections** will demonstrate how this theoretical framework is applied to solve real-world problems in ranking, scheduling, and network design. Finally, **Hands-On Practices** will offer a set of guided problems to solidify your understanding and apply these concepts directly. We begin by delving into the fundamental principles that form the bedrock of this fascinating topic.

## Principles and Mechanisms

In this chapter, we delve into the fundamental principles and structural mechanisms that govern tournaments. Building upon the introductory concepts, we will formalize the definition of a tournament, explore its elementary properties related to scores, investigate the existence of paths and cycles, and culminate in a discussion of the deep structural properties related to connectivity and dominance.

### Formal Definition and Basic Properties

A **tournament** is a directed graph that models the outcomes of a round-robin competition where every participant plays every other participant exactly once, and no draws are permitted. Formally, a tournament $T = (V, E)$ is a directed graph where for any two distinct vertices $u, v \in V$, exactly one of the directed edges $(u, v)$ or $(v, u)$ is in the edge set $E$. The existence of an edge $(u,v)$ can be interpreted as "$u$ defeats $v$".

This definition implies that a tournament is an orientation of an undirected complete graph $K_n$. A natural first question concerns the sheer number of possible tournaments on a set of $n$ labeled vertices. The number of pairs of vertices in a set of size $n$ is given by the binomial coefficient $\binom{n}{2}$. For each of these pairs, there are two possible directions for the edge between them. Since the choice for each pair is independent, the [multiplication principle](@entry_id:273377) gives the total number of distinct tournaments on $n$ labeled vertices [@problem_id:1550197].

Total number of tournaments on $n$ vertices = $2^{\binom{n}{2}}$

For example, for $n=3$ vertices, there are $\binom{3}{2}=3$ pairs, so there are $2^3 = 8$ possible tournaments. For $n=4$, this number grows to $2^6 = 64$.

A central concept for analyzing tournaments is the **score** of a vertex. The score of a vertex $v$, denoted $s(v)$ or $d^+(v)$, is its [out-degree](@entry_id:263181)—the number of other vertices it defeats. The list of the scores of all vertices in a tournament, typically sorted in non-decreasing order, is called the **[score sequence](@entry_id:272688)**.

A simple yet powerful identity relates the scores of all vertices. In any tournament, every directed edge contributes exactly 1 to the score of its origin vertex and 0 to the score of its destination vertex. Therefore, the sum of all scores in the tournament must equal the total number of edges. This provides a fundamental constraint on any possible [score sequence](@entry_id:272688).

Sum of scores: $\sum_{v \in V} d^+(v) = |E| = \binom{n}{2}$

This identity can be established via a **[double counting](@entry_id:260790) argument**: we count the total number of edges in two ways. First, by definition, it is $\binom{n}{2}$. Second, it is the sum of out-degrees over all vertices. Equating the two gives the result [@problem_id:1550199]. This property is a necessary condition for a sequence of integers to be the [score sequence](@entry_id:272688) of a tournament. For instance, in a tournament with $n=16$ players, the total sum of scores must be $\binom{16}{2} = \frac{16 \times 15}{2} = 120$ [@problem_id:1550199].

Not every sequence of integers summing to $\binom{n}{2}$ is a valid [score sequence](@entry_id:272688). **Landau's Theorem** (1953) provides a complete characterization. A sequence of integers $s_1 \le s_2 \le \dots \le s_n$ is the [score sequence](@entry_id:272688) of a tournament if and only if for every $k \in \{1, \dots, n\}$, the following inequality holds:

$\sum_{i=1}^{k} s_i \ge \binom{k}{2}$

with equality holding for $k=n$.

Let's examine the case for $n=3$. The sum of scores must be $\binom{3}{2}=3$. The possible non-decreasing integer sequences that sum to 3 are $(1, 1, 1)$ and $(0, 1, 2)$. Both satisfy Landau's conditions and correspond to the only two non-isomorphic tournaments on 3 vertices [@problem_id:1550239]:
1.  **The Cyclic Tournament ($C_3$)**: Has [score sequence](@entry_id:272688) $(1, 1, 1)$. Here, $v_1 \to v_2 \to v_3 \to v_1$. No single vertex dominates.
2.  **The Transitive Tournament ($Tr_3$)**: Has [score sequence](@entry_id:272688) $(0, 1, 2)$. Here, $v_3 \to v_2 \to v_1$, and also $v_3 \to v_1$. This represents a clear linear ranking.

### Paths, Cycles, and Dominance

The arrangement of edges in a tournament gives rise to interesting path structures. A simple but elegant result connects the local information of scores to a global count of a specific structure: directed paths of length 2. A directed path of length 2 is an ordered triple of vertices $(u, v, w)$ such that $(u, v)$ and $(v, w)$ are edges. Such a path can be thought of as an instance of indirect influence: $u$ defeats $v$, who in turn defeats $w$.

The total number of such paths can be calculated by summing over all possible middle vertices. For each vertex $v$, the number of paths of the form $(u, v, w)$ is the product of its in-degree, $d^-(v)$, and its out-degree, $d^+(v)$. The in-degree $d^-(v)$ counts the number of choices for the first vertex $u$, and the out-degree $d^+(v)$ counts the number of choices for the third vertex $w$. Therefore, the total number of 2-paths is:

Total 2-paths = $\sum_{v \in V} d^-(v) d^+(v)$

Since in any $n$-vertex tournament, $d^+(v) + d^-(v) = n-1$ for every vertex $v$, we can express this purely in terms of the [score sequence](@entry_id:272688):

Total 2-paths = $\sum_{v \in V} (n-1 - d^+(v)) d^+(v) = (n-1)\sum_{v \in V} d^+(v) - \sum_{v \in V} (d^+(v))^2 = (n-1)\binom{n}{2} - \sum_{i=1}^{n} s_i^2$

This formula demonstrates that the number of 2-paths is determined entirely by the [score sequence](@entry_id:272688) [@problem_id:1550213]. For a tournament with a [score sequence](@entry_id:272688) $\{0, 1, 2, 3, 4, 5, 6\}$ on $n=7$ vertices, the total number of 2-paths is $\sum_{k=0}^{6} k(6-k) = 35$.

One of the most celebrated results in tournament theory concerns **Hamiltonian paths**. A Hamiltonian path is a directed path that visits every vertex exactly once. It may seem that a tournament could be structured in such a complex way as to avoid such a path. However, **Redei's Theorem** (1934) states that every tournament has a Hamiltonian path.

The proof is beautifully constructive and demonstrates a powerful general technique. Consider any directed path $P = (v_1, v_2, \dots, v_k)$ that is not Hamiltonian, meaning $k  n$. Let $u$ be any vertex not on the path $P$. We can always extend $P$ to a longer path that includes $u$ [@problem_id:1511613]. There are three cases:
1.  If there is an edge $(u, v_1)$, we can prepend $u$ to form the path $(u, v_1, \dots, v_k)$.
2.  If there is an edge $(v_k, u)$, we can append $u$ to form the path $(v_1, \dots, v_k, u)$.
3.  If neither of the above holds, then by the tournament property, we must have edges $(v_1, u)$ and $(u, v_k)$. Consider the vertices of $P$. Since there is an edge from $v_1$ *to* $u$ but an edge from $u$ *to* $v_k$, there must be a first vertex $v_{i+1}$ along the path that is beaten by $u$. This implies that its predecessor, $v_i$, must beat $u$. So, we have the edges $(v_i, u)$ and $(u, v_{i+1})$. We can then insert $u$ between $v_i$ and $v_{i+1}$ to form the longer path $(v_1, \dots, v_i, u, v_{i+1}, \dots, v_k)$.

Since we can always extend any non-Hamiltonian path, we can start with a path of length 1 (any edge) and repeatedly extend it until it includes all vertices. This guarantees that every tournament contains a Hamiltonian path.

### Transitive Tournaments and Kings

While a Hamiltonian path provides a sequential ordering of vertices, it does not necessarily imply a clear "best-to-worst" ranking. For instance, in a 3-cycle $(v_1, v_2, v_3)$, the path $(v_1, v_2, v_3)$ is Hamiltonian, but $v_3$ defeats $v_1$, disrupting a simple linear hierarchy.

A tournament that does represent a perfect, unambiguous ranking is known as a **[transitive tournament](@entry_id:267486)**. A tournament $T$ is transitive if it contains no cycles. This is equivalent to the "defeats" relation being a transitive relation: if $(u, v) \in E$ and $(v, w) \in E$, then $(u, w) \in E$. In a [transitive tournament](@entry_id:267486), the vertices can be linearly ordered $v_1, v_2, \dots, v_n$ such that an edge $(v_i, v_j)$ exists if and only if $i  j$. This structure defines a [strict total order](@entry_id:270978) on the vertex set [@problem_id:1550507].

A key feature of a [transitive tournament](@entry_id:267486) on $n$ vertices is that its [score sequence](@entry_id:272688) is always $(0, 1, 2, \dots, n-1)$. The vertex with score $n-1$ is the unique winner (defeating all others), the vertex with score $n-2$ is the runner-up, and so on, down to the vertex with score 0. Thus, in a [transitive tournament](@entry_id:267486), the ranking is perfectly determined by the scores.

In most tournaments, however, such a clear winner does not exist. This motivates a more relaxed concept of dominance known as a **king**. A vertex $v$ is called a king if for every other vertex $u \in V$, there is a directed path from $v$ to $u$ of length at most 2. In other words, $v$ either defeats $u$ directly (path of length 1) or defeats some intermediate vertex $w$ who in turn defeats $u$ (path of length 2). The name comes from chess, where a king, despite being vulnerable, can attack any adjacent square.

Surprisingly, every tournament has at least one king. A simple way to find one is given by the following theorem:

**Theorem**: Any vertex with the maximum score in a tournament is a king.

**Proof**: Let $v$ be a vertex with the maximum score, $s(v) = d^+(v)$. Let $u$ be any other vertex. If $(v, u)$ is an edge, the condition is met (path of length 1). If $(u, v)$ is an edge, we need to find a vertex $w$ such that $(v, w)$ and $(w, u)$ are edges. Let $N^+(v)$ be the set of vertices defeated by $v$. If there is any $w \in N^+(v)$ such that $(w, u)$ is an edge, we are done. Suppose for contradiction that for all $w \in N^+(v)$, the edge is $(u, w)$. This means $u$ defeats every vertex in $N^+(v)$. In addition, $u$ defeats $v$. Therefore, the score of $u$ is at least $|N^+(v)| + 1 = d^+(v) + 1$. This contradicts the assumption that $v$ has the maximum score. Thus, such a $w$ must exist, and $v$ is a king [@problem_id:1516477].

It is important to note that a vertex can be a king even if it does not have the maximum score. The set of all kings can include multiple vertices with varying scores.

### Strong Connectivity and Structural Decomposition

The concepts of paths and cycles are intimately related to the connectivity of the tournament. A directed graph is **strongly connected** if for every [ordered pair](@entry_id:148349) of distinct vertices $(u, v)$, there is a directed path from $u$ to $v$. In a tournament setting, this means that despite any local defeats, every player has a path of influence leading to every other player.

What prevents a tournament from being strongly connected? A simple case occurs if there is a "source" vertex—one that defeats all others. Such a vertex has a score of $n-1$ and an in-degree of 0. Since no edges enter this vertex, no other vertex can have a path leading to it, immediately violating the condition for [strong connectivity](@entry_id:272546) [@problem_id:1550175].

This idea can be generalized. A tournament is not strongly connected if and only if there exists a proper non-empty subset of vertices $S \subset V$ such that there are no edges from any vertex in $S$ to any vertex in $V \setminus S$. All edges between $S$ and its complement $V \setminus S$ point *into* $S$. Such a set $S$ is sometimes called an initial set or, in applied contexts, a "Sovereign Bloc" [@problem_id:1550244].

This structural property has a precise algebraic signature related to scores. If all edges from $V \setminus S$ point into $S$, then for any vertex $s \in S$, all of its outgoing edges must terminate at another vertex within $S$. Summing the scores of all vertices in $S$ must therefore exactly account for the total number of edges in the subgraph induced by $S$. Since the [induced subgraph](@entry_id:270312) is itself a tournament on $|S|$ vertices, it has $\binom{|S|}{2}$ edges. This leads to a powerful criterion:

A tournament is not strongly connected if and only if there exists a proper non-empty subset of vertices $S \subset V$ such that $\sum_{s \in S} d^+(s) = \binom{|S|}{2}$.

This condition provides an algorithmic way to test for [strong connectivity](@entry_id:272546) using only the [score sequence](@entry_id:272688), although finding such a set $S$ can be computationally intensive [@problem_id:1550244].

This leads to the most profound structural result about tournaments, due to Moon (1962). Every tournament $T$ has a unique (up to [isomorphism](@entry_id:137127)) decomposition into its **[strong components](@entry_id:265360)**. The vertex set $V$ can be partitioned into $V_1, V_2, \dots, V_m$ such that:
1.  Each [induced subgraph](@entry_id:270312) $T[V_i]$ is a [strongly connected tournament](@entry_id:265092).
2.  The relationship between the components is transitive: for any $i  j$, every vertex in $V_i$ has a directed edge to every vertex in $V_j$.

This means any tournament can be viewed as a "[transitive tournament](@entry_id:267486) of [strong components](@entry_id:265360)." The tournament fails to be strongly connected if and only if it has more than one strong component ($m > 1$). The structure described in [@problem_id:1550210] is a perfect example of this decomposition, where the sets $V_1, V_2, V_3, V_4$ are the vertex sets of the [strong components](@entry_id:265360).

This decomposition provides a complete characterization of kings. A vertex $v \in V_i$ can reach any vertex in a component $V_j$ where $j > i$ via a direct edge (path of length 1). It can also reach any vertex within its own component $V_i$ because $T[V_i]$ is strongly connected. However, a vertex $v \in V_i$ (for $i>1$) can never reach any vertex in a component $V_j$ with $j  i$, because all edges between these components point from $V_j$ to $V_i$.

Therefore, for a vertex to be a king, it must be able to reach every other vertex. This is only possible if the vertex belongs to the very first strong component, $V_1$. Within $V_1$, every vertex can reach every other vertex in $V_1$ (since it's strongly connected) and can reach every vertex in all subsequent components $V_j$ (for $j>1$) by a direct edge. Thus, we have the following elegant result:

**Theorem**: The set of all kings in a tournament is precisely the vertex set of its first strong component, $V_1$.

This final theorem beautifully interlinks the concepts of dominance (kings), connectivity ([strong components](@entry_id:265360)), and the overall hierarchical structure of any tournament [@problem_id:1550210].