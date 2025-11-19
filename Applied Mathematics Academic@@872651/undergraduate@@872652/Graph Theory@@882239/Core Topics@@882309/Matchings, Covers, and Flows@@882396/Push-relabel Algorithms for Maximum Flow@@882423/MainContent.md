## Introduction
The maximum flow problem is a cornerstone of [network optimization](@entry_id:266615), modeling everything from logistics and telecommunications to resource allocation. While traditional algorithms solve this problem by finding and augmenting paths from a source to a sink, the push-relabel method offers a distinct and highly efficient alternative. This approach breaks from the convention of maintaining a valid flow at every step, instead operating on a more flexible "preflow" structure. This conceptual shift can be initially counterintuitive but unlocks significant performance gains and a deeper understanding of [network dynamics](@entry_id:268320).

This article provides a complete guide to the push-relabel paradigm. The first chapter, "Principles and Mechanisms," will deconstruct the algorithm into its core components, explaining the roles of preflow, [height functions](@entry_id:181180), and the fundamental `push` and `relabel` operations. Next, "Applications and Interdisciplinary Connections" will broaden the perspective, showcasing how this method solves practical problems like [bipartite matching](@entry_id:274152) and connects to fields like [linear programming](@entry_id:138188) and parallel computing. Finally, "Hands-On Practices" will allow you to solidify your understanding by tackling targeted exercises. We begin by exploring the foundational principles that set the push-relabel method apart from its predecessors.

## Principles and Mechanisms

The push-relabel method represents a significant departure from traditional augmenting-path algorithms for solving the maximum flow problem. Whereas algorithms like Ford-Fulkerson or Edmonds-Karp incrementally augment flow along paths while maintaining the flow conservation property at every step, the push-relabel approach operates on a more relaxed structure called a **preflow**. This chapter will elucidate the foundational principles of this paradigm, detail the core mechanisms of **push** and **relabel** operations, and establish the algorithm's correctness and termination.

### From Valid Flows to Preflows

At the heart of the [push-relabel algorithm](@entry_id:263106) is the concept of a **preflow**. A preflow is a function $f: V \times V \to \mathbb{R}$ that satisfies the capacity constraint, $0 \le f(u,v) \le c(u,v)$ for all vertices $u, v \in V$, and the skew symmetry property, $f(u,v) = -f(v,u)$. However, it relaxes the flow conservation constraint. For a valid flow, the total flow entering a vertex (other than the source $s$ or sink $t$) must equal the total flow leaving it. In a preflow, the inflow can exceed the outflow.

This potential surplus is quantified by the **excess flow** at a vertex $v$, denoted $e(v)$, which is defined as the net flow entering the vertex:
$e(v) = \sum_{u \in V} f(u,v)$.

For a valid flow, $e(v) = 0$ for all $v \in V \setminus \{s, t\}$. For a preflow, we only require that $e(v) \ge 0$ for all $v \in V \setminus \{s, t\}$. A vertex $v \in V \setminus \{s, t\}$ with a strictly positive excess, $e(v) > 0$, is called an **active** vertex. Intuitively, an active vertex has accumulated a surplus of flow that it must eventually send "downstream" towards the sink or "upstream" back to the source. The fundamental goal of the [push-relabel algorithm](@entry_id:263106) is to systematically eliminate all excess at intermediate vertices, thereby transforming an initial preflow into a valid maximum flow.

To illustrate, consider a network with vertices $\{s, a, b, c, t\}$ and a preflow $f$ given. Let's compute the excess for the intermediate vertices. The excess at node $a$, for instance, is the sum of incoming flows minus the sum of outgoing flows. Suppose the only incoming flow is $f(s,a) = 7$, and outgoing flows are $f(a,b)=3$ and $f(a,c)=2$. The excess would be $e(a) = f(s,a) - (f(a,b) + f(a,c)) = 7 - (3+2) = 2$. Since $e(a) > 0$, node $a$ is active. If for another node $c$, the incoming flow is $f(a,c)=2$ and outgoing flows are $f(c,b)=1$ and $f(c,t)=1$, then its excess is $e(c) = 2 - (1+1) = 0$, so it is not active. [@problem_id:1529556] The algorithm will terminate only when no such active vertices remain.

### The Height Function: A Gravitational Analogy

To guide the movement of excess flow, the [push-relabel algorithm](@entry_id:263106) introduces a **height function**, $h: V \to \mathbb{N}$. This function assigns a non-negative integer label to each vertex. The height function can be thought of as creating a gravitational potential field over the network. The source $s$ is placed at the highest level, and the sink $t$ is fixed at the lowest level (height 0). The central idea is to push excess flow "downhill" from a vertex $u$ to a vertex $v$ only if $v$ is at a lower height.

Specifically, the algorithm will only permit a push of flow from a vertex $u$ to a vertex $v$ if $h(u) = h(v) + 1$. This strict height difference ensures that flow moves in a controlled, acyclic manner at any given moment, preventing situations where flow is pushed back and forth indefinitely between a pair of vertices. If an active vertex finds itself "stuck," with no lower neighbors to which it can push flow, it must increase its own height—an operation called relabeling—to create a new downhill path.

### Core Mechanisms: Push and Relabel

The algorithm iteratively refines the preflow using two fundamental operations: **push** and **relabel**. These operations are exclusively applied to active vertices.

#### The Push Operation

A **push** operation moves excess flow from an active vertex $u$ to one of its neighbors $v$. A push from $u$ to $v$ is applicable if and only if three conditions are met:
1.  **Active Vertex**: The vertex $u$ must have excess flow, i.e., $e(u) > 0$. [@problem_id:1529569]
2.  **Residual Capacity**: The edge $(u,v)$ must have available capacity in the **[residual graph](@entry_id:273096)** $G_f$. The residual capacity is defined as $c_f(u,v) = c(u,v) - f(u,v)$. Thus, we require $c_f(u,v) > 0$.
3.  **Height Condition**: The push must be "downhill," meaning $h(u) = h(v) + 1$.

An edge $(u,v)$ that satisfies the second and third conditions is called an **admissible edge**. A push operation can only occur along an admissible edge originating from an active vertex.

For example, consider an active node $u$ with $h(u)=2$. Suppose it has two neighbors, $v$ and $w$, with residual capacity on edges $(u,v)$ and $(u,w)$. If $h(v)=1$ and $h(w)=2$, only edge $(u,v)$ is admissible because it satisfies the height condition $h(u) = h(v)+1$. The edge $(u,w)$ is not admissible because $h(u) \neq h(w)+1$. [@problem_id:1529562]

When a push from $u$ to $v$ is performed, the amount of flow pushed is $\delta = \min(e(u), c_f(u,v))$. This is either the entire excess from $u$ or just enough to saturate the edge $(u,v)$. The preflow and excesses are updated as follows:
- $f(u,v)$ is increased by $\delta$.
- $f(v,u)$ is decreased by $\delta$.
- $e(u)$ is decreased by $\delta$.
- $e(v)$ is increased by $\delta$. [@problem_id:1529546]

Notice that a push operation conserves the total excess flow between the participating vertices, merely transferring it from $u$ to $v$.

#### The Relabel Operation

A **relabel** operation is applied to an active vertex $u$ when it has excess flow ($e(u) > 0$) but no admissible edges along which to push it. This implies that for every vertex $v$ for which there is residual capacity on the edge $(u,v)$, the height condition is not met; specifically, $h(u) \le h(v)$. The vertex $u$ is in a "[potential well](@entry_id:152140)" and cannot push its excess downhill.

To resolve this, the relabel operation increases the height of $u$ to the minimum possible level that will allow a future push. The new height is set to:
$h(u) \leftarrow 1 + \min \{ h(v) \mid c_f(u,v) > 0 \}$

This action lifts $u$ just high enough ($1$ unit above its lowest neighbor in the [residual graph](@entry_id:273096)) to enable a push. For example, if an active node $a$ with $h(a)=1$ has residual capacity to neighbors $s$ and $b$ with $h(s)=4$ and $h(b)=1$, it cannot push to either (since $h(a) \neq h(s)+1$ and $h(a) \neq h(b)+1$). Therefore, a relabel is necessary. The new height would be $h(a) \leftarrow 1 + \min(h(s), h(b)) = 1 + \min(4, 1) = 2$. [@problem_id:1529588] [@problem_id:1529526]

### The Generic Algorithm

With the core mechanisms defined, we can outline the structure of the generic [push-relabel algorithm](@entry_id:263106).

#### Initialization

The algorithm begins by establishing an initial preflow and [height function](@entry_id:271993). This setup deliberately violates flow conservation to inject flow into the network, creating the initial set of active vertices.
1.  **Initialize Flow**: Set $f(u,v) = 0$ for all edges.
2.  **Initialize Heights**: Set the source height $h(s) = |V|$ (the number of vertices in the graph) and $h(v) = 0$ for all other vertices $v \in V \setminus \{s\}$. The heights of $s$ and $t$ remain fixed throughout the algorithm.
3.  **Saturate from Source**: For each vertex $u$ adjacent to the source $s$, set the flow $f(s,u) = c(s,u)$. This pushes the maximum possible flow out of the source.
4.  **Calculate Initial Excesses**: Based on the initial flow, the excess at each vertex is calculated. Neighbors $u$ of the source will have an initial excess $e(u) = c(s,u)$, and the source will have a large negative excess $e(s) = -\sum_{(s,u) \in E} c(s,u)$. All other vertices will have zero excess.

For a path graph $s \to u \to v \to t$ with $|V|=4$, the initialization would set $h(s)=4$ and $h(u)=h(v)=h(t)=0$. If $c(s,u)=15$, the flow $f(s,u)$ becomes $15$, while all other flows are $0$. This results in initial excesses $e(u)=15$ and $e(s)=-15$. [@problem_id:1529545]

#### Main Loop

After initialization, the algorithm enters its main loop, which continues as long as there is at least one active vertex $u \in V \setminus \{s,t\}$. In each iteration, the algorithm performs the following steps:
1.  Select an active vertex $u$.
2.  Apply an applicable push or relabel operation to $u$.

A common strategy for managing operations is the **Discharge** procedure. `Discharge(u)` is a subroutine that applies push and relabel operations to an active vertex $u$ until its excess $e(u)$ becomes zero. While $e(u) > 0$, the procedure checks for an admissible edge $(u,v)$. If one exists, it performs a push. If not, it relabels $u$. This process is repeated until $u$ is no longer active. The main algorithm then consists of repeatedly selecting an active vertex and calling `Discharge` on it until no active vertices remain. [@problem_id:1529546]

### Analysis of Correctness and Termination

Two critical questions remain: Does this process always terminate? And if it does, is the resulting flow a maximum flow? The answers to both lie in properties of the height function.

#### The Height Invariant

Throughout the execution of the algorithm, a crucial invariant is maintained: for every edge $(u,v)$ in the current [residual graph](@entry_id:273096) $G_f$, the height inequality $h(u) \le h(v) + 1$ holds. A push operation only occurs when $h(u) = h(v)+1$, and since it might create a reverse residual edge $(v,u)$, we must check the invariant for this new edge: $h(v) = h(u)-1 \le h(u)+1$, which is true. A relabel of $u$ increases $h(u)$, which preserves the invariant for all outgoing residual edges $(u,v)$. The new height is chosen specifically to restore the invariant for at least one edge. A state where an edge in the [residual graph](@entry_id:273096) violates this, e.g., $h(u) > h(v) + 1$, could not have been produced by a correct execution of the algorithm. [@problem_id:1529587]

#### Termination

The algorithm is guaranteed to terminate. This can be argued by showing that the total number of push and relabel operations is finite.

The number of **relabel** operations is bounded. Each relabel operation on a vertex $u$ strictly increases its height $h(u)$. A key property is that the height of any vertex $u$ can never exceed $2|V|-1$. This is because any active vertex $u$ must have a path back to the source $s$ in the [residual graph](@entry_id:273096). Applying the height invariant along this path of length at most $|V|-1$ shows that $h(u) \le h(s) + (|V|-1) = |V| + |V|-1 = 2|V|-1$. Since each relabel increases a vertex's height and the height is bounded, any single vertex can only be relabeled a finite number of times (at most $2|V|-1$ times). [@problem_id:1529523]

The number of **push** operations is also finite. Pushes can be categorized as *saturating* (if they exhaust the residual capacity of an edge) or *non-saturating* (if they exhaust the excess of the active vertex). The number of saturating pushes is bounded, as each one can be seen as "using up" an edge in a particular direction, and heights must increase significantly before that same edge can be used again. Bounding non-saturating pushes requires a more complex potential function argument, but they are also finite. Since the total number of operations is bounded, the algorithm must terminate.

#### Correctness

When the algorithm terminates, there are no active vertices in $V \setminus \{s,t\}$. This means $e(u)=0$ for all intermediate vertices, satisfying the flow conservation property. The final preflow is therefore a valid flow.

To prove it is a **maximum** flow, we use the [max-flow min-cut theorem](@entry_id:150459), which states that a flow is maximum if and only if there is no [augmenting path](@entry_id:272478) from $s$ to $t$ in the [residual graph](@entry_id:273096). We can prove that upon termination, no such path exists.

Let $f'$ be the final flow and $h'$ be the final height function. Assume for the sake of contradiction that there is an augmenting path $s=v_0, v_1, \dots, v_k=t$ in the final [residual graph](@entry_id:273096) $G_{f'}$. By the height invariant, for each edge $(v_i, v_{i+1})$ on this path, we must have $h'(v_i) \le h'(v_{i+1}) + 1$. [@problem_id:1529571]
Applying this inequality across the entire path:
$h'(v_0) \le h'(v_1)+1$
$h'(v_1) \le h'(v_2)+1$
...
$h'(v_{k-1}) \le h'(v_k)+1$

Summing these inequalities telescopically gives $h'(v_0) \le h'(v_k) + k$.
We know the fixed heights of the [source and sink](@entry_id:265703) are $h'(s) = h'(v_0) = |V|$ and $h'(t) = h'(v_k) = 0$. Substituting these values gives $|V| \le 0 + k$, so $k \ge |V|$.
However, an augmenting path is a simple path, so its length $k$ (the number of edges) can be at most $|V|-1$. This leads to the contradiction $|V| \le |V|-1$.

The contradiction shows that our initial assumption was false: there can be no [augmenting path](@entry_id:272478) from $s$ to $t$ in the final [residual graph](@entry_id:273096). Therefore, the flow produced by the [push-relabel algorithm](@entry_id:263106) upon termination is a maximum flow.