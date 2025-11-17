## Introduction
Mantel's Theorem is a cornerstone of [extremal graph theory](@entry_id:275134), providing a precise and elegant answer to a fundamental question: what is the maximum number of edges a graph can have before it is forced to contain a specific substructure? This article focuses on the simplest and most foundational case—forbidding a triangle ($K_3$). This problem is not merely a theoretical puzzle; it models critical constraints in diverse fields, from preventing feedback loops in network design to understanding the limits of collaboration in social systems. By addressing the knowledge gap between a graph's overall edge density and the emergence of local structures, Mantel's theorem offers a powerful quantitative tool.

This article will guide you through a complete exploration of this classic result. The first chapter, **Principles and Mechanisms**, will introduce the theorem's formal statement, detail its elegant proof, and characterize the unique graphs that achieve the maximum edge limit. Subsequently, **Applications and Interdisciplinary Connections** will broaden our perspective, showcasing the theorem's utility in real-world modeling and its relationship to more advanced structural results. Finally, **Hands-On Practices** will provide opportunities to apply these concepts and solve concrete problems. We begin our journey by delving into the core principles that make Mantel's Theorem so powerful.

## Principles and Mechanisms

Having established the foundational concepts of graph theory in the preceding chapter, we now delve into one of the seminal results in [extremal graph theory](@entry_id:275134): Mantel's Theorem. This theorem addresses a question of fundamental importance: what is the maximum number of edges a simple graph on a given number of vertices can have while avoiding a particular substructure? Specifically, we will focus on the simplest non-trivial [forbidden subgraph](@entry_id:261803), the triangle ($K_3$). This inquiry is not merely an academic puzzle; it models real-world constraints in network design, social structures, and information flow. For instance, one might ask how many pairwise collaborations can be established among a group of $n$ scientists before it becomes inevitable that a "research triad"—a group of three mutually collaborating scientists—must exist [@problem_id:1551509]. Mantel's theorem provides a precise and elegant answer to this question.

### The Quantitative Bound: Mantel's Theorem

At its core, Mantel's theorem provides a [sharp threshold](@entry_id:260915) for the number of edges that forces the existence of a triangle. It makes a powerful statement about the relationship between the global property of edge density and the local property of containing a triangle.

**Mantel's Theorem (1907):** A simple graph $G$ on $n$ vertices with more than $\lfloor \frac{n^2}{4} \rfloor$ edges must contain a triangle.

Equivalently, the theorem states that the maximum number of edges in a [triangle-free graph](@entry_id:276046) on $n$ vertices is exactly $\lfloor \frac{n^2}{4} \rfloor$. This maximum is denoted by $\text{ex}(n, K_3)$, the **extremal number** for the triangle $K_3$.

This theorem allows us to solve a variety of problems with remarkable ease. For example, if a computing architecture with $n=51$ processors must avoid any three mutually connected units due to a "triadic incompatibility" rule, Mantel's theorem immediately tells us that the maximum number of connections is $\text{ex}(51, K_3) = \lfloor \frac{51^2}{4} \rfloor = \lfloor \frac{2601}{4} \rfloor = 650$ [@problem_id:1552014]. Similarly, for a consortium of $n=21$ companies, the maximum number of collaboration links in a triangle-free network is $\lfloor \frac{21^2}{4} \rfloor = \lfloor \frac{441}{4} \rfloor = 110$ [@problem_id:1519829] [@problem_id:1505586]. The number of edges required to *guarantee* a triangle is therefore one more than this maximum, or $\lfloor \frac{n^2}{4} \rfloor + 1$ [@problem_id:1551509].

### The Extremal Structure: Complete Bipartite Graphs

The power of Mantel's theorem lies not just in the numerical bound but also in its characterization of the graphs that achieve this maximum. A graph on $n$ vertices with exactly $\text{ex}(n, K_3)$ edges that is triangle-free is called an **extremal graph**. What do these graphs look like?

The canonical example of a [triangle-free graph](@entry_id:276046) is a **bipartite graph**. In such a graph, the vertex set $V$ can be partitioned into two disjoint [independent sets](@entry_id:270749), $A$ and $B$, such that every edge connects a vertex in $A$ to one in $B$. Since there are no edges *within* $A$ or *within* $B$, no triangle can possibly be formed.

To maximize the number of edges in a [bipartite graph](@entry_id:153947) on $n$ vertices with partition sizes $|A| = a$ and $|B| = b$ (where $a+b=n$), we should include every possible edge between $A$ and $B$. This forms the **complete [bipartite graph](@entry_id:153947)** $K_{a,b}$, which has $ab$ edges. To maximize this product for a fixed sum $n=a+b$, we must make $a$ and $b$ as close as possible. This is a standard result from arithmetic, formally seen by writing $ab = \frac{(a+b)^2 - (a-b)^2}{4} = \frac{n^2 - (a-b)^2}{4}$. The product is maximized when $|a-b|$ is minimized.
*   If $n$ is even, $n=2k$, we choose $a=b=k$, giving $k^2 = \frac{n^2}{4}$ edges.
*   If $n$ is odd, $n=2k+1$, we choose $a=k$ and $b=k+1$, giving $k(k+1) = \frac{n-1}{2} \frac{n+1}{2} = \frac{n^2-1}{4} = \lfloor \frac{n^2}{4} \rfloor$ edges.

In both cases, the maximum number of edges is $\lfloor \frac{n^2}{4} \rfloor$. The graph that achieves this is the complete bipartite graph $K_{\lfloor n/2 \rfloor, \lceil n/2 \rceil}$. This specific graph is also known as the **Turán graph** $T(n,2)$. Mantel's theorem implies that any graph with the maximum possible number of edges that is still triangle-free *must* be this complete [bipartite graph](@entry_id:153947) [@problem_id:1519846].

It is insightful to consider what happens just below this threshold. The graph $T(10,2) = K_{5,5}$ is triangle-free and has $25$ edges. If we seek a [triangle-free graph](@entry_id:276046) on 10 vertices with 24 edges, we could simply remove an edge from $K_{5,5}$. However, other structures also exist. The graph $K_{4,6}$ also has $4 \times 6 = 24$ edges and is triangle-free. Notably, $K_{4,6}$ cannot be a subgraph of $K_{5,5}$. This demonstrates that while the Turán graph $T(n,2)$ is the unique maximizer, other dense bipartite graphs exist just below the maximum threshold, reinforcing the idea that bipartiteness is the essential structural feature for dense, [triangle-free graphs](@entry_id:267894) [@problem_id:1519835].

### Unveiling the Mechanism: Proofs from Local Properties

To understand *why* the $\lfloor n^2/4 \rfloor$ bound holds, we must examine the local consequences of being triangle-free. These local constraints, when aggregated over the entire graph, yield the global bound.

#### Fundamental Local Constraints in Triangle-Free Graphs

Two properties are particularly fundamental. The first concerns the neighborhood of a single vertex. Consider a "collaboration circle" consisting of all individuals who have directly collaborated with a specific person, say Dr. Sharma. If the overall network is triangle-free, what can we say about the connections *within* this circle? If any two people in the circle had collaborated, they, along with Dr. Sharma, would form a triangle. This is forbidden. Therefore, there can be no collaborations at all within Dr. Sharma's collaboration circle. In graph-theoretic terms:

**Property 1:** In a [triangle-free graph](@entry_id:276046) $G$, the neighborhood $N(v)$ of any vertex $v$ is an **independent set**. [@problem_id:1519854]

The second property concerns a pair of adjacent vertices. Consider a triangle-free network of servers where a link exists between Server U and Server V. If there were a third server, W, connected to both U and V, the set $\{U, V, W\}$ would form a forbidden feedback loop (a triangle). Consequently, the set of servers connected to U (excluding V) and the set of servers connected to V (excluding U) must be completely disjoint. This leads to a powerful inequality on their degrees, $d(u)$ and $d(v)$:

**Property 2:** For any edge $uv$ in a [triangle-free graph](@entry_id:276046) $G$ on $n$ vertices, we have $d(u) + d(v) \le n$. [@problem_id:1519851]

This is because the $|N(u)|-1$ neighbors of $u$ (other than $v$) and the $|N(v)|-1$ neighbors of $v$ (other than $u$) are [disjoint sets](@entry_id:154341) of vertices, and together with $u$ and $v$ themselves, they account for $(d(u)-1) + (d(v)-1) + 2$ distinct vertices. This sum cannot exceed $n$. For instance, in a triangle-free network of $N=117$ servers, if one server $U$ has degree 45, any adjacent server $V$ can have a degree of at most $117 - 45 = 72$ [@problem_id:1519851].

#### A Global Bound from Local Information: Proof of Mantel's Theorem

This second local property provides a direct path to proving Mantel's theorem. The proof is a masterful example of how summing a local inequality over the entire graph structure can lead to a global conclusion.

Let $G=(V, E)$ be a [triangle-free graph](@entry_id:276046) with $n$ vertices and $m$ edges. As we established, for every edge $uv \in E$, the inequality $d(u) + d(v) \le n$ holds. Let us sum this inequality over all edges in the graph:
$$ \sum_{uv \in E} (d(u) + d(v)) \le \sum_{uv \in E} n = mn $$
The left-hand side of this inequality can be re-evaluated by considering the contribution of each vertex. A vertex $v$ with degree $d(v)$ is an endpoint of $d(v)$ edges. For each of these edges, its degree $d(v)$ is added to the sum. Thus, the term $d(v)$ appears $d(v)$ times in the sum, contributing $d(v)^2$. Therefore, the sum is equivalent to the sum of the squares of all vertex degrees:
$$ \sum_{v \in V} d(v)^2 = \sum_{uv \in E} (d(u) + d(v)) $$
Combining these gives the inequality $\sum_{v \in V} d(v)^2 \le mn$.

Now, we introduce the **Cauchy-Schwarz inequality**, which provides a fundamental relationship between the [sum of squares](@entry_id:161049) and the square of the sum. For any set of real numbers $x_1, \dots, x_n$, we have $(\sum x_i)^2 \le n (\sum x_i^2)$. Applying this to the vertex degrees $d(v)$:
$$ \left(\sum_{v \in V} d(v)\right)^2 \le n \sum_{v \in V} d(v)^2 $$
From the [handshaking lemma](@entry_id:261183), we know that $\sum_{v \in V} d(v) = 2m$. Substituting this and our previous inequality:
$$ (2m)^2 \le n \left(\sum_{v \in V} d(v)^2\right) \le n (mn) = m n^2 $$
This simplifies to $4m^2 \le mn^2$. If $m>0$, we can divide by $4m$ to get $m \le \frac{n^2}{4}$. Since $m$ must be an integer, we have $m \le \lfloor \frac{n^2}{4} \rfloor$, which completes the proof of Mantel's theorem [@problem_id:1551509] [@problem_id:1552014].

### A Condition on Minimum Degree

Mantel's theorem provides a condition based on the total number of edges. An alternative, and often more practical, condition can be formulated based on the [minimum degree](@entry_id:273557) of the graph, $\delta(G)$.

**Corollary to Mantel's Theorem:** If a simple graph $G$ on $n$ vertices has a [minimum degree](@entry_id:273557) $\delta(G) > \frac{n}{2}$, then $G$ must contain a triangle.

The proof of this corollary is beautifully direct and relies on the first local property we identified. Suppose for contradiction that $\delta(G) > n/2$ and $G$ is triangle-free. Pick an arbitrary vertex $v$. Let $S = N(v)$ be its neighborhood. By definition, $|S| = d(v) \ge \delta(G) > n/2$.

Since $G$ is triangle-free, $S$ must be an independent set. Now consider any vertex $u \in S$. Because $S$ is an [independent set](@entry_id:265066), all of $u$'s neighbors must lie outside of $S$. The vertex $u$ is connected to $v$. The remaining vertices available to be neighbors of $u$ are in the set $V \setminus (S \cup \{v\})$. The size of this set is $n - 1 - |S| = n - 1 - d(v)$. Therefore, the degree of $u$ is at most $1 + (n-1-d(v)) = n-d(v)$. So, we have $d(u) \le n - d(v)$, which implies $d(u) + d(v) \le n$.

However, by our initial assumption, both $d(u)$ and $d(v)$ are greater than $n/2$. Their sum must therefore be strictly greater than $n$. This is a direct contradiction. Thus, our initial assumption that $G$ is triangle-free must be false.

This result allows us to determine minimum connectivity requirements to guarantee certain structures. For instance, in a secure network of 99 researchers, what is the minimum number of connections $k$ each researcher must have to guarantee a "collaboration triangle"? According to the corollary, a triangle is guaranteed if $\delta(G) = k > 99/2 = 49.5$. Since $k$ must be an integer, the smallest value is $k=50$. A [minimum degree](@entry_id:273557) of $k=49$ is insufficient, as demonstrated by the triangle-free complete bipartite graph $K_{49,50}$, whose [minimum degree](@entry_id:273557) is 49 [@problem_id:1519850]. This illustrates the sharpness of the $\delta(G) > n/2$ bound.

In summary, Mantel's theorem and its related results form the bedrock of [extremal graph theory](@entry_id:275134). They demonstrate a profound connection between the local structure of a graph (the absence of triangles) and its global properties (edge density and [minimum degree](@entry_id:273557)), providing precise thresholds that have found applications across science and engineering.