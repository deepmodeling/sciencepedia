## Introduction
Finding the shortest path between all pairs of vertices in a graph is a fundamental problem in computer science and [network analysis](@entry_id:139553). While running Dijkstra's algorithm from every vertex is effective for graphs with non-negative weights, this approach fails in the presence of negative-weight edges. This introduces a significant challenge, as many real-world systems, from [financial networks](@entry_id:138916) to project management, involve models with both costs and benefits. Johnson's algorithm provides an elegant and efficient solution to this [all-pairs shortest paths](@entry_id:636377) problem, especially for sparse graphs where it significantly outperforms alternative methods.

This article provides a comprehensive exploration of Johnson's algorithm. The first chapter, **"Principles and Mechanisms"**, deconstructs the core reweighting technique, explaining how vertex potentials are used to eliminate negative weights while preserving shortest paths. Next, **"Applications and Interdisciplinary Connections"** explores its utility in diverse fields like logistics, finance, and reinforcement learning, showcasing how abstract graph problems model real-world challenges. Finally, the **"Hands-On Practices"** section offers practical coding problems to solidify your understanding and translate theory into a functional implementation.

## Principles and Mechanisms

Johnson's algorithm provides an elegant and efficient solution to the [all-pairs shortest paths](@entry_id:636377) (APSP) problem for sparse graphs, particularly those containing negative-weight edges. To fully appreciate its design, we must first understand the limitations of more straightforward approaches and then delve into the central principle of reweighting that makes Johnson's algorithm possible. This chapter will deconstruct the algorithm into its fundamental components, exploring the theoretical underpinnings that guarantee its correctness and performance.

### The Challenge of Negative Weights in All-Pairs Shortest Paths

The APSP problem seeks to find the shortest path distance between every pair of vertices in a weighted, directed graph. A simple strategy is to run a [single-source shortest path](@entry_id:633889) (SSSP) algorithm from each vertex. If all edge weights in the graph are non-negative, this approach is highly effective. We can execute Dijkstra's algorithm from each of the $n$ vertices. Using a [binary heap](@entry_id:636601) implementation, each run takes $O(m + n \log n)$ time, where $n$ is the number of vertices and $m$ is the number of edges. For a sparse graph where $m$ is on the order of $n$, the total time for APSP would be $O(n(n+n\log n)) = O(n^2 \log n)$.

However, the presence of [negative edge weights](@entry_id:264831) invalidates the core assumption of Dijkstra's algorithm. Dijkstra's is a [greedy algorithm](@entry_id:263215) that finalizes the shortest path to a vertex once it is extracted from the priority queue. This greedy choice is only safe if all edge weights are non-negative, which ensures that paths can only get longer as more edges are added. With negative weights, a seemingly longer path could ultimately become shorter, leading to incorrect results.

Consider a [simple graph](@entry_id:275276) structure that illustrates this failure [@problem_id:3242420]. Imagine three vertices $s$, $a$, and $t$, with edges $(s, a)$, $(a, t)$, and a direct edge $(s, t)$. Let the weights be $w(s,t) = 5$, $w(s,a) = 7$, and $w(a,t) = -3$. The true shortest path from $s$ to $t$ is via vertex $a$, with a total weight of $w(s,a) + w(a,t) = 7 - 3 = 4$. However, Dijkstra's algorithm, starting from $s$, would first relax the edge $(s,t)$, setting the distance to $t$ as $5$. Because $5 \lt 7$, the algorithm would greedily select and finalize vertex $t$ before vertex $a$, reporting the incorrect shortest path distance of $5$. The existence of even a single negative-weight edge can thus cause this naive "run Dijkstra from everywhere" approach to fail.

An alternative that correctly handles negative weights is the Bellman-Ford algorithm. Running Bellman-Ford from each of the $n$ vertices would correctly solve the APSP problem, but at a much higher computational cost. Each run of Bellman-Ford takes $O(nm)$ time, leading to a total APSP time of $O(n^2m)$. For sparse graphs, this is $O(n^3)$, which is substantially slower than the Dijkstra-based approach. The central question Johnson's algorithm answers is: can we find a way to use the faster Dijkstra's algorithm even in the presence of negative weights, thereby achieving a better [time complexity](@entry_id:145062) for sparse graphs?

### The Core Principle: Reweighting with Potentials

The ingenious solution at the heart of Johnson's algorithm is to transform the graph's edge weights. The goal is to produce a new set of non-negative weights, $w'$, such that the shortest paths in the reweighted graph are identical to those in the original graph. This transformation is achieved using a technique called **reweighting by potentials**.

We assign a real number, or **potential**, $h(v)$ to every vertex $v \in V$. The original weight $w(u,v)$ of an edge $(u,v)$ is then transformed into a new weight $w_h(u,v)$ according to the following formula:

$$w_h(u,v) = w(u,v) + h(u) - h(v)$$

This transformation might seem arbitrary at first, but its effect on the weight of any path is profound. Consider an arbitrary path $p = \langle v_0, v_1, \ldots, v_k \rangle$ from a vertex $u=v_0$ to $v=v_k$. Its original weight is $w(p) = \sum_{i=1}^{k} w(v_{i-1}, v_i)$. The weight of this same path in the reweighted graph is:

$$w_h(p) = \sum_{i=1}^{k} w_h(v_{i-1}, v_i) = \sum_{i=1}^{k} (w(v_{i-1}, v_i) + h(v_{i-1}) - h(v_i))$$

By rearranging the terms, we can see that the potential terms form a [telescoping sum](@entry_id:262349):

$$w_h(p) = \left( \sum_{i=1}^{k} w(v_{i-1}, v_i) \right) + (h(v_0) - h(v_1)) + (h(v_1) - h(v_2)) + \dots + (h(v_{k-1}) - h(v_k))$$

$$w_h(p) = w(p) + h(v_0) - h(v_k) = w(p) + h(u) - h(v)$$

This result is crucial. It shows that for any given pair of vertices $(u,v)$, the reweighting process changes the weight of *every* path between them by the exact same amount, $h(u) - h(v)$. Consequently, if one path was shorter than another in the original graph, it will remain shorter in the reweighted graph. The set of shortest paths is therefore **preserved** under any potential-based reweighting [@problem_id:3242431].

Once we compute shortest path distances $\delta_h(u,v)$ in the reweighted graph, we can recover the original shortest path distances $\delta(u,v)$ by simply reversing the transformation:

$$\delta(u,v) = \delta_h(u,v) - h(u) + h(v)$$

This also means that the reweighting formula itself is invertible. Given a set of reweighted edge weights $w'(u,v)$ and the potentials $h(v)$, one can reconstruct the original edge weights using the relation $w(u,v) = w'(u,v) - h(u) + h(v)$ [@problem_id:3242442].

### The Feasibility Condition and its Construction

For the reweighting strategy to be useful, we must be able to run Dijkstra's algorithm on the reweighted graph. This requires that all reweighted edge weights are non-negative. This leads to the **feasibility condition** for the potential function $h$:

For every edge $(u,v) \in E$, we must have $w_h(u,v) \ge 0$.

Substituting the reweighting formula, this becomes:

$w(u,v) + h(u) - h(v) \ge 0$, which is equivalent to $h(v) \le h(u) + w(u,v)$.

This is the sole formal requirement for a potential function $h$ to be valid for Johnson's algorithm [@problem_id:3242431]. The challenge now becomes finding such a function $h$. This inequality is reminiscent of the **[triangle inequality](@entry_id:143750)** property of shortest paths: for any source $s$, the shortest path distance to a vertex $v$, denoted $\delta(s,v)$, must satisfy $\delta(s,v) \le \delta(s,u) + w(u,v)$ for any edge $(u,v)$.

This observation provides the key to constructing a feasible potential. If we can set $h(v) = \delta(s,v)$ for some source vertex $s$, the feasibility condition is automatically satisfied. However, for this to work, the source $s$ must have a finite-path distance to every other vertex in the graph. A general graph may not contain such a vertex.

To overcome this, Johnson's algorithm employs a clever artifice:
1.  A new, auxiliary source vertex $s'$ is added to the graph.
2.  For every original vertex $v \in V$, a directed edge $(s',v)$ is added with weight $0$.

Let's call this augmented graph $G'$. In $G'$, the new source $s'$ is guaranteed to have a path to every other vertex $v \in V$. Now, we can define our potential function $h(v)$ as the shortest path distance from $s'$ to $v$ in this augmented graph: $h(v) = \delta_{G'}(s',v)$. Since the original graph $G$ (and thus $G'$) may contain negative-weight edges, these shortest path distances must be computed using an algorithm that can handle them, such as Bellman-Ford.

### The Complete Johnson's Algorithm

With these principles in place, we can now outline the complete procedure for Johnson's algorithm:

1.  **Augmentation:** Create a new graph $G'$ by adding a new source vertex $s'$ to $G$. For each vertex $v \in V$, add a new edge $(s', v)$ with weight $w(s',v) = 0$.

2.  **Potential Calculation:** Run the Bellman-Ford algorithm on $G'$ starting from the source $s'$. This has two possible outcomes:
    *   If a negative-weight cycle is detected, the algorithm reports that shortest paths are not well-defined and terminates.
    *   If no [negative-weight cycles](@entry_id:633892) exist, for each vertex $v \in V$, the potential is set to the computed shortest path distance: $h(v) = \delta_{G'}(s',v)$.

3.  **Reweighting:** Compute a new set of non-[negative edge weights](@entry_id:264831) $w_h$ for the original graph $G$. For each edge $(u,v) \in E$, set $w_h(u,v) = w(u,v) + h(u) - h(v)$.

4.  **All-Pairs Computation:** For each vertex $u \in V$:
    *   Run Dijkstra's algorithm with source $u$ on the graph $G$ with the new weights $w_h$. This computes the reweighted shortest path distances $\delta_h(u,v)$ for all $v \in V$.

5.  **Final Distance Recovery:** For each pair of vertices $(u,v)$, compute the true shortest path distance by reversing the potential transformation: $\delta(u,v) = \delta_h(u,v) - h(u) + h(v)$.

The overall [time complexity](@entry_id:145062) is the sum of its parts. The Bellman-Ford step on $G'$ takes $O((n+1)(m+n)) = O(nm)$. The reweighting step takes $O(m)$. The main workload is running Dijkstra $n$ times, which takes $O(n(m+n\log n))$ using a [binary heap](@entry_id:636601). The final recovery takes $O(n^2)$. For sparse graphs where $m = \Theta(n)$, the total [time complexity](@entry_id:145062) is $O(n^2\log n)$, which is a significant improvement over the $O(n^3)$ complexity of running Bellman-Ford from every vertex [@problem_id:3242450].

### Mechanistic Insights and Special Cases

A deeper understanding of Johnson's algorithm emerges from examining its behavior in specific scenarios.

#### The Role of Negative-Weight Cycles

The fundamental limitation for any [shortest path algorithm](@entry_id:273826) on a graph with negative weights is the **negative-weight cycle**. If a path from $u$ to $v$ can reach a cycle of negative total weight and then proceed to $v$, one can traverse the cycle repeatedly to make the path's weight arbitrarily small. In this case, the shortest path distance $d(u,v)$ is $-\infty$ [@problem_id:3242409]. Johnson's algorithm is only applicable to graphs without such cycles.

The Bellman-Ford step (Step 2) serves as the crucial detector for these cycles. The Bellman-Ford algorithm finds [shortest paths in a graph](@entry_id:267725) with $N$ vertices in at most $N-1$ passes of edge relaxation. If, on the $N$-th pass, any distance can still be improved, it is definitive proof of a reachable negative-weight cycle. In our case, this check happens on the graph $G'$ with $n+1$ vertices [@problem_id:3242459]. The formation of such cycles can be straightforward; for example, if an undirected edge $\{u,v\}$ with positive weight $w$ is naively converted to two directed edges $(u,v)$ and $(v,u)$ with weight $-w$, a negative-weight 2-cycle is created, which Bellman-Ford would detect, causing Johnson's algorithm to fail [@problem_id:32564].

#### Behavior on Graphs with Non-Negative Weights

A valuable conceptual test is to consider running Johnson's algorithm on a graph that already has only non-negative weights. In this scenario, when we form the augmented graph $G'$, the shortest path from the new source $s'$ to any vertex $v$ is simply the direct edge $(s',v)$ of weight 0, as any other path from $s'$ would involve edges from the original graph, all of which are non-negative. Therefore, the Bellman-Ford step will compute potentials $h(v) = 0$ for all $v \in V$.

When these potentials are used for reweighting, we get:
$w_h(u,v) = w(u,v) + h(u) - h(v) = w(u,v) + 0 - 0 = w(u,v)$

The reweighted graph is identical to the original graph. Consequently, Johnson's algorithm simply performs $n$ runs of Dijkstra on the original graph. The total number of operations, such as [priority queue](@entry_id:263183) `decrease-key` calls, will be exactly the same as in the naive "run Dijkstra from everywhere" strategy [@problem_id:3242411]. This shows that Johnson's algorithm incurs no unnecessary overhead in this special case, apart from the initial Bellman-Ford pass.

#### Properties of the Potential Space

The design of the algorithm reveals subtle properties about the space of all possible feasible potentials. The use of an auxiliary source vertex $s'$ is a robust way to generate a valid [potential function](@entry_id:268662), but it is not the only way. One could, for instance, try to pick an existing vertex $r \in V$ and set $h(v) = \delta(r,v)$. This modified approach would work if and only if $r$ can reach every other vertex in the graph. If some vertex is unreachable from $r$, its potential would be infinite, and the reweighting arithmetic would fail, demonstrating the elegance of the auxiliary source construction [@problem_id:3242492].

Furthermore, the set of all feasible potentials for a given graph has a specific structure. If a graph is **strongly connected** (i.e., every vertex is reachable from every other vertex), then any two feasible [potential functions](@entry_id:176105), $h_1$ and $h_2$, must differ by a single additive constant across all vertices. That is, there exists a constant $c$ such that $h_2(v) = h_1(v) + c$ for all $v \in V$. If the graph is not strongly connected, more degrees of freedom exist, and this uniqueness property is lost [@problem_id:32510]. This insight connects the algorithmic mechanism of reweighting to the fundamental topological structure of the graph itself.