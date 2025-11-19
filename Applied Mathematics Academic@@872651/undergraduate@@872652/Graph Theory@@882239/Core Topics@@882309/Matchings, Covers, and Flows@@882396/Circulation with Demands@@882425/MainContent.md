## Introduction
In countless real-world systems, from global supply chains to power grids, success hinges on managing the flow of resources across a complex network. It's not enough to simply move items from a single source to a destination; we must balance a distributed web of supplies and demands. The **circulation with demands** model provides a powerful graph-theoretic framework to formally analyze and solve these intricate balancing acts. However, faced with numerous capacity constraints and node requirements, how can we determine if a feasible plan even exists?

This article provides a comprehensive introduction to this fundamental problem in [network optimization](@entry_id:266615). The first chapter, **Principles and Mechanisms**, will delve into the formal definition of circulation, explore the elegant reduction to the maximum flow problem for determining feasibility, and extend the model to handle more complex constraints like minimum flow requirements. Next, the **Applications and Interdisciplinary Connections** chapter will showcase the model's versatility, demonstrating how it can be applied to solve practical problems in logistics, engineering, and even [ecological modeling](@entry_id:193614). Finally, the **Hands-On Practices** section will offer opportunities to apply these concepts to concrete scenarios.

We begin by establishing the core mathematical principles and mechanisms that govern circulations, laying the groundwork for understanding how to find a feasible flow in any given network.

## Principles and Mechanisms

### The Formal Definition of Circulation with Demands

In many real-world network systems, from logistics and transportation to finance and communication, we are concerned not just with moving a commodity from a single origin to a single destination, but with balancing a complex web of supplies and demands distributed throughout the network. The **circulation with demands** problem provides a powerful mathematical framework for modeling and analyzing such systems.

Formally, we begin with a directed graph $G = (V, E)$, where $V$ is a set of vertices (e.g., cities, warehouses, servers) and $E$ is a set of directed edges (e.g., roads, pipelines, data links). Each edge $(u,v) \in E$ is associated with a **capacity** $u(u,v) \ge 0$, representing the maximum amount of flow it can carry.

The key feature that distinguishes this problem is the assignment of a **demand** value $d(v)$ to each vertex $v \in V$. The demand specifies the net flow required at that vertex. By convention:
- If $d(v) > 0$, vertex $v$ is a **sink** or **demand node**, requiring a net inflow of $d(v)$ units.
- If $d(v) < 0$, vertex $v$ is a **source** or **supply node**, providing a net outflow of $-d(v)$ units.
- If $d(v) = 0$, vertex $v$ is a **transshipment node**, where the total flow in must equal the total flow out.

A **[feasible circulation](@entry_id:271969)** is a function $f: E \to \mathbb{R}_{\ge 0}$, which we call a **flow**, that satisfies two fundamental conditions:

1.  **Capacity Constraints:** For every edge $(u,v) \in E$, the flow must not exceed the edge's capacity.
    $$0 \le f(u,v) \le u(u,v)$$

2.  **Demand Constraints:** For every vertex $v \in V$, the net flow at the vertex must equal its demand. The net flow is defined as the total flow entering the vertex minus the total flow leaving it.
    $$\sum_{w \in V \text{ s.t. } (w,v) \in E} f(w,v) - \sum_{w \in V \text{ s.t. } (v,w) \in E} f(v,w) = d(v)$$

For any [feasible circulation](@entry_id:271969) to exist, a simple but critical global condition must be met: the total supply must equal the total demand. In other words, flow cannot be created or destroyed within the system as a whole. This leads to the **Global Balance Condition**:
$$ \sum_{v \in V} d(v) = 0 $$

Consider a water distribution network for an agricultural region, where pumping stations act as sources and irrigation fields act as sinks [@problem_id:1488578]. Suppose the total supply from all pumps is $430 \text{ m}^3/\text{h}$ (i.e., $\sum d(v)_{\text{sources}} = -430$) and the total demand from all fields is $445 \text{ m}^3/\text{h}$ (i.e., $\sum d(v)_{\text{sinks}} = 445$). The sum of all demands is $\sum d(v) = -430 + 445 = 15$. Because this sum is not zero, there is a net deficit of $15 \text{ m}^3/\text{h}$ in the network. It is physically impossible to satisfy the demands with the given supplies. To make a feasible flow possible, the system must be balanced, for instance by introducing a new reservoir that acts as a source with a demand of $d(\text{Reservoir}) = -15$, thereby restoring the global balance.

### Solving for Feasibility: Reduction to Maximum Flow

Determining whether a [feasible circulation](@entry_id:271969) exists for a given network with demands is a fundamental question. Fortunately, we do not need a new algorithm from scratch. We can cleverly transform the circulation problem into an equivalent **maximum flow problem**, which can then be solved efficiently using standard algorithms like Edmonds-Karp or Dinic's algorithm.

The transformation, or **reduction**, involves constructing a new graph $G' = (V', E')$ from the original network $G = (V,E)$. The procedure is as follows:

1.  Initialize $V' = V$ and $E' = E$. The capacities on all original edges from $E$ are retained.
2.  Add two new special vertices to $V'$: a **super-source** $s'$ and a **super-sink** $t'$.
3.  For each supply node $v \in V$ (where $d(v) < 0$), add a new edge from the super-source to it: $(s', v)$. The capacity of this edge is set to the amount of supply, i.e., $u(s', v) = -d(v)$.
4.  For each demand node $v \in V$ (where $d(v) > 0$), add a new edge from it to the super-sink: $(v, t')$. The capacity of this edge is set to the amount of demand, i.e., $u(v, t') = d(v)$.
5.  Transshipment nodes (where $d(v)=0$) are not connected to $s'$ or $t'$.

The intuition behind this construction is that the super-source $s'$ acts as the ultimate origin for all supply in the network, and the super-sink $t'$ acts as the ultimate destination for all demand. The new edges model the injection of supply into the network and the extraction of demand from it.

A [feasible circulation](@entry_id:271969) exists in the original graph $G$ if and only if the maximum flow from $s'$ to $t'$ in the new graph $G'$ is equal to the total demand (or supply) in the system. Let $D_{total} = \sum_{v: d(v)>0} d(v)$. A [feasible circulation](@entry_id:271969) exists if and only if the value of the maximum $s'$-$t'$ flow in $G'$ is exactly $D_{total}$. This condition means that the maximum flow is large enough to saturate all the new edges connected to the super-sink, thereby satisfying all demands. Because the network is balanced, this will also saturate all edges leaving the super-source.

For example, in a logistics network with supply nodes $A$ and $D$ ($d(A)=-10, d(D)=-6$) and demand nodes $B, C, E$ ($d(B)=5, d(C)=8, d(E)=3$), the reduction would create edges $(s', A)$ with capacity $10$ and $(s', D)$ with capacity $6$. It would also create edges $(B, t')$, $(C, t')$, and $(E, t')$ with capacities $5$, $8$, and $3$, respectively [@problem_id:1488616]. The total supply is $16$ and the total demand is $16$. A [feasible circulation](@entry_id:271969) exists if and only if we can push $16$ units of flow from $s'$ to $t'$ in the transformed network. The sum of capacities of all new edges in this construction is the total supply plus the total demand, which is $16 + 16 = 32$.

### Incorporating Lower Bounds on Flow

The basic model assumes that the flow on any edge can be zero. However, in many practical applications, there are operational requirements for a minimum non-zero flow. For example, a pipeline might require a minimum flow to prevent [sedimentation](@entry_id:264456), or a shipping route might be contractually obligated to carry a minimum volume. This adds a **lower bound** constraint $l(u,v) \ge 0$ to each edge, so the capacity constraint becomes:

$$l(u,v) \le f(u,v) \le u(u,v)$$

This more complex problem can be elegantly reduced to the standard circulation problem (with zero lower bounds) through a [change of variables](@entry_id:141386). For each edge $(u,v)$, we define a new **excess flow** variable $f'(u,v)$ representing the flow above the required minimum:

$$f'(u,v) = f(u,v) - l(u,v)$$

By substituting $f(u,v) = f'(u,v) + l(u,v)$ into the original constraints, we can derive an equivalent problem in terms of $f'$.

First, the capacity constraints on $f'$ are found by substituting into the original inequality:
$l(u,v) \le f'(u,v) + l(u,v) \le u(u,v)$, which simplifies to
$$0 \le f'(u,v) \le u(u,v) - l(u,v)$$
The new capacity for the excess flow, $u'(u,v)$, is simply the original capacity minus the lower bound.

Second, the demand constraints must be updated. We substitute $f(u,v)$ in the conservation equation for each node $w$:
$$\sum_{v} (f'(v,w) + l(v,w)) - \sum_{v} (f'(w,v) + l(w,v)) = d(w)$$
Rearranging the terms to isolate the $f'$ variables gives:
$$\left( \sum_{v} f'(v,w) - \sum_{v} f'(w,v) \right) = d(w) - \left( \sum_{v} l(v,w) - \sum_{v} l(w,v) \right)$$
The left side is the net flow for $f'$ at node $w$. The right side defines a new, **adjusted demand**, $d'(w)$. The term in the parenthesis on the right represents the net imbalance at node $w$ caused by committing to send the minimum flow $l(u,v)$ on every edge. Thus, the new demand is the original demand adjusted for this built-in flow imbalance.

To illustrate, consider a water distribution system with demands and minimum pipeline flows [@problem_id:1488566]. Let a junction A have an original demand $d(A) = 0$. Suppose water flows into A from S with $l(S,A) = 5$, and flows out of A to C and D with $l(A,C) = 2$ and $l(A,D) = 3$. The net imbalance from lower-bound flows at A is $(\text{inflow}) - (\text{outflow}) = 5 - (2+3) = 0$. So the adjusted demand is $d'(A) = d(A) - 0 = 0$. Now consider the source S, with $d(S)=-20$. It has no incoming lower-bound flows, but has outgoing lower-bound flows $l(S,A)=5$ and $l(S,B)=5$. The imbalance at S is $0 - (5+5) = -10$. The adjusted demand is $d'(S) = -20 - (-10) = -10$.

After computing the adjusted demands $d'(v)$ and adjusted capacities $u'(u,v)$ for all nodes and edges, we have a standard circulation-with-demands problem (with zero lower bounds) for the flow $f'$. We can solve this transformed problem for feasibility, for example by reducing it to a max-flow problem as described previously. Once a feasible excess flow $f'$ is found, the feasible flow for the original problem is simply recovered by $f(u,v) = f'(u,v) + l(u,v)$.

### Conditions for Feasibility: A Deeper Look

The reduction to max-flow provides an algorithmic way to check for feasibility, but it does not give a direct, structural reason for *why* a network might be infeasible. For this, we turn to a powerful result analogous to the [max-flow min-cut theorem](@entry_id:150459), known as **Hoffman's Circulation Theorem**.

The theorem provides a simple "certificate" of infeasibility. Intuitively, a [feasible circulation](@entry_id:271969) cannot exist if there is some subset of nodes $S \subset V$ that collectively demands more flow than can possibly be delivered to it, or generates more supply than can possibly be shipped out of it.

Let's focus on the case with upper capacities but zero lower bounds. A circulation is infeasible if and only if there exists a set of vertices $S \subset V$ that acts as a "bottleneck." For such a set $S$, the total demand originating from within it, $\sum_{v \in S} d(v)$, cannot be satisfied because it exceeds the total capacity of all edges leaving the set, $c(S, V \setminus S) = \sum_{u \in S, v \in V \setminus S} u(u,v)$. This is because the net demand from $S$ must be fulfilled by flow passing through the cut $(S, V \setminus S)$ to the rest of the graph, $V \setminus S$.

We can quantify this by defining an **overload value** for any subset $S$:
$$ \Delta(S) = \sum_{v \in S} d(v) - c(S, V \setminus S) $$
Hoffman's theorem states that a [feasible circulation](@entry_id:271969) exists if and only if $\Delta(S) \le 0$ for all subsets $S \subset V$. If we can find even one set $S$ for which $\Delta(S) > 0$, we have proven that no [feasible circulation](@entry_id:271969) is possible, and the value of $\Delta(S)$ quantifies the severity of this bottleneck.

Consider a data center network where servers have data production/consumption demands and links have capacity limits [@problem_id:1488621]. Suppose we have a set of servers $S=\{A, B, D\}$ with demands $d(A)=10$, $d(B)=-3$, and $d(D)=5$. The total net demand for this set is $\sum_{v \in S} d(v) = 10 - 3 + 5 = 12$ Tbps. This net demand must be shipped out of the set $S$. Suppose the outgoing links are $(A,C)$ and $(B,C)$ with total capacity $c(S, V \setminus S) = c(A,C) + c(B,C) = 4 + 1 = 5$ Tbps. The overload value is $\Delta(S) = 12 - 5 = 7$. Since $\Delta(S) > 0$, this set $S$ collectively generates a net of 12 Tbps but only has paths to export 5 Tbps. It is therefore impossible for the network to balance the flows, and this specific set $S$ serves as a proof of infeasibility. Finding the subset $S$ that maximizes $\Delta(S)$ identifies the most critical bottleneck in the system.

### The Structure of Feasible Solutions

When a [feasible circulation](@entry_id:271969) exists, is the solution unique? Generally, no. The set of all feasible circulations often forms a convex set, meaning there can be infinitely many solutions. Understanding the relationship between these solutions is crucial for optimization and [network control](@entry_id:275222).

Let $f_1$ and $f_2$ be two distinct feasible circulations for the same problem. Their difference, $g = f_1 - f_2$, defines a flow on the edges (where some values may be negative). Let's examine the conservation law for $g$ at any vertex $v$:
$$ \text{net flow of } g \text{ at } v = \text{net flow of } f_1 - \text{net flow of } f_2 = d(v) - d(v) = 0 $$
This shows that the difference between any two feasible circulations is itself a **pure circulation**—a flow that satisfies the conservation law with zero demand at every vertex.

A fundamental theorem by Ford and Fulkerson states that any such pure circulation can be decomposed into a sum of smaller flows, each circulating around a simple directed cycle. This gives us a powerful tool: we can navigate the space of feasible solutions by identifying cycles and modifying the flow along them.

To do this systematically, we use the concept of the **[residual graph](@entry_id:273096)**, $G_f$, associated with a given flow $f$. For each edge $(u,v) \in E$ in the original graph:
- If $f(u,v) < u(u,v)$, we can still send more flow from $u$ to $v$. This is represented by a **forward edge** $(u,v)$ in $G_f$ with residual capacity $u_f(u,v) = u(u,v) - f(u,v)$.
- If $f(u,v) > 0$, we can "cancel" or "push back" some of the existing flow. This is represented by a **backward edge** $(v,u)$ in $G_f$ with residual capacity $u_f(v,u) = f(u,v)$.

A new, distinct [feasible circulation](@entry_id:271969) $f'$ can be generated from an existing one, $f$, by finding a simple directed cycle in the [residual graph](@entry_id:273096) $G_f$ and pushing an additional amount of flow $\delta$ along this cycle. The maximum amount $\delta$ that can be pushed is limited by the minimum residual capacity of any edge on the chosen cycle. Augmenting the flow in this manner preserves the demand constraints at every node while respecting capacity constraints.

For example, given a feasible flow in a small network [@problem_id:1488583], we can construct the [residual graph](@entry_id:273096). If we find a directed cycle, say $A \to C \to B \to A$, with residual capacities of $1$, $5$, and $1$ respectively, we can augment the flow. The bottleneck on this cycle is $\delta = \min\{1, 5, 1\} = 1$. Pushing $\delta=1$ unit of flow along this cycle means we increase the flow on the original edges $(A,C)$, $(C,B)$, and $(B,A)$ by 1. The result is a new flow that is also feasible. This technique allows us to explore the entire [solution space](@entry_id:200470) starting from a single [feasible circulation](@entry_id:271969).

### Advanced Topics and Practical Extensions

The circulation framework is highly versatile and can be extended to model more complex, realistic scenarios.

**Minimum-Cost Circulation**
In most practical problems, satisfying demands is not enough; we want to do so at the lowest possible cost. If each edge $(u,v)$ has an associated cost $p(u,v)$ per unit of flow, the **[minimum-cost circulation](@entry_id:264018) problem** seeks a [feasible circulation](@entry_id:271969) $f$ that minimizes the total cost:
$$ \min \sum_{(u,v) \in E} p(u,v) f(u,v) $$
For instance, a cloud provider connecting data centers in Amsterdam, Berlin, Copenhagen, and Dublin might have different costs for transmitting data over different fiber optic links [@problem_id:1488619]. The goal is to find a [data transfer](@entry_id:748224) plan that balances all surpluses and deficits at the minimum total transmission cost. This problem is a cornerstone of [network optimization](@entry_id:266615) and can be solved with algorithms such as the [cycle-canceling algorithm](@entry_id:637262) or successive [shortest path algorithms](@entry_id:634863). Proving the optimality of a solution often involves using dual variables (or "potentials") associated with the nodes, which provide a lower bound on the optimal cost.

**Sparsest Circulation**
In some applications, the cost is not linear with the amount of flow, but rather there is a fixed cost for using a route at all. In this case, the goal is to find a [feasible circulation](@entry_id:271969) that minimizes the number of edges with non-zero flow, i.e., to find the **sparsest circulation**. This models scenarios where activating a shipping route or a data link incurs a significant operational cost, regardless of the volume it carries. For a small supply chain network, one might find multiple ways to ship containers from plants to distribution centers, but the most efficient plan would be one that uses the minimum number of distinct routes [@problem_id:1488569]. This is a harder, [combinatorial optimization](@entry_id:264983) problem, as its [objective function](@entry_id:267263) is not linear. Solutions often involve characterizing the space of all feasible flows and then searching its boundaries for solutions where some flow variables are zero.

**Minimizing Demand Violations**
What happens if a network is provably infeasible? In the real world, operations do not simply halt. Instead, the goal shifts from perfect satisfaction to minimizing the negative impact. We can model this by seeking a flow that, while adhering to all capacity constraints, minimizes a weighted sum of the demand violations. For each vertex $v$, the violation is the absolute difference between its net flow and its demand, $|(\text{net flow at } v) - d(v)|$. By assigning penalty weights to these violations, we can prioritize satisfying more critical demands. For a logistics network where production exceeds shipping capacity, this approach would find a shipping plan that minimizes the total penalty from product shortages at retail stores and unshipped inventory at the plant [@problem_id:1488584]. This transforms an infeasible problem into a solvable optimization problem.

**Robust Circulation**
Planning often happens under uncertainty. The exact demand at a market or the exact output of a plant may not be known in advance, but can be estimated to lie within a certain interval. The **robust circulation problem** addresses this by seeking a single, static flow plan $f$ that remains feasible for *any* possible realization of demands within their specified intervals, $[d_{\min}(v), d_{\max}(v)]$. For a flow $f$ to be robustly feasible, its resulting net flow at each node $v$, $B_f(v)$, must lie within that node's demand interval: $d_{\min}(v) \le B_f(v) \le d_{\max}(v)$. This condition translates the problem into a system of linear inequalities on the flow variables. For a supply chain with uncertain supply, local warehouse imbalances, and fluctuating market demand, this method can determine a fixed shipping plan that is guaranteed to be feasible no matter how the uncertainties resolve within their given bounds [@problem_id:1488612].