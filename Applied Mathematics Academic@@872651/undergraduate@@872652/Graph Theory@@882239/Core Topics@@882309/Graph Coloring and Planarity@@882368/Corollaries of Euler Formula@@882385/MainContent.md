## Introduction
Euler's formula, $v - e + f = 2$, is a landmark result in graph theory, establishing a fundamental relationship for any connected planar graph. However, the formula's true practical power is realized through its corollaries, which translate this abstract topological property into concrete, measurable constraints on a graph's structure. These derived principles address the crucial question of how dense a [planar graph](@entry_id:269637) can be, providing essential tools for proving non-planarity and understanding the inherent limitations of networks drawn on a two-dimensional plane. This article delves into these powerful consequences, revealing the deep structural rules that govern [planar graphs](@entry_id:268910).

The following chapters will guide you from theoretical derivation to real-world application. In **Principles and Mechanisms**, we will explore how combining Euler's formula with basic graph properties leads to powerful inequalities bounding edge density and vertex degrees. Next, **Applications and Interdisciplinary Connections** will showcase how these mathematical constraints are applied to solve problems in fields ranging from circuit design and molecular chemistry to classical geometry. Finally, **Hands-On Practices** will offer guided problems to solidify your understanding and apply these corollaries to tangible analytical tasks.

## Principles and Mechanisms

While Euler's formula provides a fundamental [topological invariant](@entry_id:142028) for [planar graphs](@entry_id:268910), its true power in combinatorial and geometric applications is unlocked through its corollaries. These corollaries establish profound constraints on the structure of [planar graphs](@entry_id:268910), particularly on their density of edges and the degrees of their vertices. By leveraging the relationship $v - e + f = 2$, we can derive a series of powerful inequalities that serve as essential tools for proving non-planarity, analyzing network properties, and understanding the inherent "sparseness" of any graph that can be drawn on a plane.

### The Fundamental Link Between Faces and Edges

The key to deriving these corollaries lies in establishing a second relationship between the number of edges, $e$, and the number of faces, $f$. This relationship stems from a simple observation about the boundaries of faces in a [planar embedding](@entry_id:263159). Let us consider a simple, connected planar graph $G$ with at least three vertices. Since the graph is simple (no loops or multiple edges), the boundary of any face must consist of at least three edges. This is because a cycle of length 1 (a loop) or 2 (a pair of multiple edges) would be required to form a face with fewer than three boundary edges, both of which are disallowed in a simple graph.

Let us denote the degree of a face, $\deg(f_i)$, as the number of edges on its boundary. The minimum face degree is therefore 3, i.e., $\deg(f_i) \ge 3$ for all faces $f_i$. If we sum the degrees of all faces in the graph, we are counting the boundary edges. Since each edge in a connected [planar graph](@entry_id:269637) serves as a boundary for exactly two faces (or is counted twice for the outer face boundary in some configurations, like a tree), this sum is precisely twice the total number of edges. This is a "[handshaking lemma](@entry_id:261183)" for faces:

$$ \sum_{i=1}^{f} \deg(f_i) = 2e $$

Combining this with the observation that $\deg(f_i) \ge 3$ for all $i$, we can establish an inequality:

$$ 2e = \sum_{i=1}^{f} \deg(f_i) \ge \sum_{i=1}^{f} 3 = 3f $$

This gives us the crucial inequality $2e \ge 3f$, which holds for any simple planar graph with $v \ge 3$.

### Maximum Edge Density in Planar Graphs

We now have two relationships for a simple, connected [planar graph](@entry_id:269637) with $v \ge 3$:
1. Euler's Formula: $v - e + f = 2$, which can be rearranged to $f = 2 - v + e$.
2. The Face-Edge Inequality: $3f \le 2e$.

By substituting the expression for $f$ from Euler's formula into the inequality, we can eliminate the number of faces and derive a direct relationship between the number of vertices and edges.

$$ 3(2 - v + e) \le 2e $$
$$ 6 - 3v + 3e \le 2e $$
$$ 6 - 3v \le -e $$
$$ e \le 3v - 6 $$

This inequality, $e \le 3v - 6$, is a cornerstone result for planar graphs. It states that for a given number of vertices, a simple [planar graph](@entry_id:269637) cannot have an arbitrarily large number of edges. Planar graphs are inherently **sparse**.

This result provides a powerful and easily applicable test for **non-planarity**. If a [simple graph](@entry_id:275276) with $v \ge 3$ vertices has more than $3v-6$ edges, it cannot possibly be planar. Consider a network architect designing internal wiring for [data routing](@entry_id:748216) hubs on a single-layer Printed Circuit Board (PCB), a problem where connections cannot cross. If a proposed design has $v=13$ nodes and $e=34$ connections, we can immediately determine its infeasibility. The maximum number of edges a [planar graph](@entry_id:269637) with 13 vertices can have is $3(13) - 6 = 39 - 6 = 33$. Since $34 > 33$, this network configuration is guaranteed to be non-planar and cannot be implemented on a single-layer PCB [@problem_id:1492325].

However, it is critical to recognize that this condition is **necessary, but not sufficient**. If a graph satisfies $e \le 3v - 6$, it is not guaranteed to be planar. The test can only be used to certify non-planarity, never to confirm [planarity](@entry_id:274781). A failure to violate the inequality means the test is inconclusive. For instance, the complete bipartite graph $K_{3,3}$, a classic example in planarity theory, has $v=6$ vertices and $e=9$ edges. The inequality requires $e \le 3(6)-6=12$. Since $9 \le 12$, the condition is met, yet $K_{3,3}$ is famously non-planar. Based solely on this test, our conclusion about $K_{3,3}$ would be inconclusive [@problem_id:1492301]. To prove the non-[planarity](@entry_id:274781) of graphs like $K_{3,3}$, we need a more refined tool.

### A Tighter Bound for Triangle-Free Graphs

The general inequality $e \le 3v-6$ was derived assuming that the smallest face has a boundary of length 3 (a triangle). What if a graph has no triangles? This is the case for all [bipartite graphs](@entry_id:262451), such as the $K_{3,3}$ graph, which models scenarios like connecting three power plants to three industrial zones with dedicated lines [@problem_id:1492363].

If a simple planar graph with $v \ge 3$ is **triangle-free**, then the smallest possible cycle length is 4. Consequently, the boundary of any face must consist of at least four edges, meaning $\deg(f_i) \ge 4$ for all faces $f_i$. The face [handshaking lemma](@entry_id:261183) $\sum \deg(f_i) = 2e$ now leads to a stronger inequality:

$$ 2e = \sum_{i=1}^{f} \deg(f_i) \ge \sum_{i=1}^{f} 4 = 4f $$

This gives us $2e \ge 4f$, or $e \ge 2f$. Again, we substitute $f=2-v+e$ from Euler's formula:

$$ e \ge 2(2-v+e) $$
$$ e \ge 4 - 2v + 2e $$
$$ 2v - 4 \ge e $$

Thus, for any simple, connected, triangle-free planar graph, the number of edges must satisfy $e \le 2v - 4$. This is a significantly tighter bound than the general one. Let's revisit the $K_{3,3}$ graph ($v=6, e=9$). As a bipartite graph, it is triangle-free. Applying the new inequality, the maximum number of edges it could have if it were planar is $2(6) - 4 = 8$. Since $K_{3,3}$ has $e=9$ edges, and $9 > 8$, it violates this condition. We can now definitively conclude that $K_{3,3}$ is non-planar [@problem_id:1492363].

### Constraints on Vertex Degrees

The sparsity of planar graphs, as captured by the edge density inequalities, has direct and profound consequences for the degrees of their vertices.

First, we can establish a hard limit on the **[average degree](@entry_id:261638)** of any simple planar graph. The [average degree](@entry_id:261638), denoted $\bar{d}$, is the sum of all vertex degrees divided by the number of vertices. By the vertex [handshaking lemma](@entry_id:261183), this sum is $2e$. Therefore, $\bar{d} = \frac{2e}{v}$. Using the inequality $e \le 3v - 6$, we find:

$$ \bar{d} = \frac{2e}{v} \le \frac{2(3v-6)}{v} = \frac{6v - 12}{v} = 6 - \frac{12}{v} $$

Since $v \ge 3$, the term $\frac{12}{v}$ is always positive. Therefore, for any simple [planar graph](@entry_id:269637), the [average degree](@entry_id:261638) is strictly less than 6. This is a fundamental property. In the design of on-chip networks, it implies that no matter how large or complex the planar network becomes, the average number of connections per processing node can never reach 6 [@problem_id:1492318].

An even more powerful consequence follows directly from this fact. In any set of numbers, it is impossible for every number to be greater than the average. Similarly, in a graph, it is impossible for every vertex to have a degree strictly greater than the [average degree](@entry_id:261638). Since the [average degree](@entry_id:261638) is strictly less than 6, there must be at least one vertex whose degree is not 6 or higher. In other words, there must be at least one vertex with a degree of 5 or less.

This can be proven by contradiction. Assume every vertex in a simple planar graph $G$ has a degree of at least 6. Then the sum of degrees would be at least $6v$. By the [handshaking lemma](@entry_id:261183), $2e \ge 6v$, which implies $e \ge 3v$. This, however, directly contradicts the planar graph inequality $e \le 3v - 6$, as $3v$ can never be less than or equal to $3v-6$. The contradiction proves that our initial assumption was false.

Therefore, **every simple [planar graph](@entry_id:269637) must contain at least one vertex with degree 5 or less** [@problem_id:1492322] [@problem_id:1492349]. This result is remarkably useful. For instance, it is the crucial lemma in the standard proof of the Five-Color Theorem, which states that any map can be colored with at most five colors such that no two adjacent regions have the same color. The existence of a low-degree vertex provides the starting point for an inductive proof of that theorem.

### Advanced Structural Deductions

The algebraic relationships provided by Euler's formula and the handshaking lemmas can be combined to deduce highly specific structural properties of graphs. These methods are particularly powerful in fields like computational chemistry for analyzing molecular structures.

Consider the family of [fullerenes](@entry_id:154486), which are hollow carbon molecules whose structure is a [3-regular graph](@entry_id:261395) (every carbon atom has degree 3) where all faces are pentagons or hexagons. Let's determine the number of pentagonal faces such a molecule must have, given it has $v=20$ atoms [@problem_id:1492348].
1.  **Vertices and Edges:** We are given $v=20$. Since every vertex has degree 3, the vertex [handshaking lemma](@entry_id:261183) gives $2e = 3v = 3(20) = 60$, so $e=30$.
2.  **Euler's Formula:** We can now find the total number of faces: $f = 2 - v + e = 2 - 20 + 30 = 12$.
3.  **Face Properties:** Let $f_5$ be the number of pentagonal faces and $f_6$ be the number of hexagonal faces. We know $f_5 + f_6 = f = 12$.
4.  **Face Handshaking:** The sum of face degrees is $2e = 60$. This sum can also be expressed as $5f_5 + 6f_6$. So, we have the system of equations:
    $$ f_5 + f_6 = 12 $$
    $$ 5f_5 + 6f_6 = 60 $$
    Substituting $f_6 = 12 - f_5$ into the second equation gives $5f_5 + 6(12 - f_5) = 60$, which simplifies to $5f_5 + 72 - 6f_5 = 60$, or $-f_5 = -12$. Thus, $f_5 = 12$.
This remarkable result shows that any fullerene, regardless of its size (number of atoms), must have exactly 12 pentagonal faces.

This algebraic approach can also reveal how "close" a graph is to being a **triangulation** (a [maximal planar graph](@entry_id:266059) where $e=3v-6$). Consider a processing architecture modeled as a simple connected planar graph where the number of links $e$ is constrained to be $e=3v-7$ [@problem_id:1492369]. This is just one edge short of the maximum possible. We can precisely determine the facial structure of any such graph.
1.  **Find Total Faces:** $f = 2 - v + e = 2 - v + (3v - 7) = 2v - 5$.
2.  **Use Face Handshaking:** $\sum_{k \ge 3} k f_k = 2e = 2(3v - 7) = 6v - 14$.
3.  **Combine Formulas:** Consider the quantity $\sum_{k \ge 3} (k-3)f_k$. This sum is non-zero only for non-triangular faces.
    $$ \sum_{k \ge 3} (k-3)f_k = \left(\sum kf_k\right) - 3\left(\sum f_k\right) = (6v-14) - 3(2v-5) = 6v - 14 - 6v + 15 = 1 $$
Since $k$ and $f_k$ must be integers, the only way for the sum $\sum_{k \ge 4} (k-3)f_k$ to equal 1 is if exactly one term is non-zero and equal to 1. This happens if and only if $f_4 = 1$ (making the term $(4-3)f_4 = 1$) and $f_k=0$ for all $k \ge 5$. This proves that any [planar graph](@entry_id:269637) with $e=3v-7$ edges must consist of one quadrilateral face and all other faces must be triangles. This demonstrates the powerful rigidity that Euler's formula and its corollaries impose on planar [embeddings](@entry_id:158103).

### Generalization to Disconnected Graphs

Finally, it is important to note that the classic form of Euler's formula applies only to [connected graphs](@entry_id:264785). For a planar graph with $c$ connected components, the formula generalizes. By considering each component separately and accounting for the merging of their outer faces into a single shared outer face, one can derive the generalized formula [@problem_id:1492300]:

$$ v - e + f = c + 1 $$

This is particularly relevant in applications like urban planning, where a city's transportation map may consist of several disjoint networks. This generalized formula ensures that the fundamental topological relationship holds even when the graph is not connected. The corollaries derived for simple [connected graphs](@entry_id:264785), however, should be applied to each component individually rather than to the [disconnected graph](@entry_id:266696) as a whole.