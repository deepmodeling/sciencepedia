## Introduction
Global routing is a cornerstone of modern integrated circuit (IC) [physical design](@entry_id:1129644), responsible for planning the wire paths that connect millions of components on a chip. As chip complexity skyrockets, the sheer density of interconnections creates an immense challenge: how to route all signals without creating "traffic jams" of wires that exceed the physical capacity of the available routing channels. Addressing this congestion problem is the primary task of the global router, which serves as a critical bridge between logic placement and the final, exact wiring performed by the detailed router.

This article provides a comprehensive exploration of the fundamental algorithms that solve this challenge. In "Principles and Mechanisms," you will learn about the [grid graph](@entry_id:275536) abstraction used to model the chip and the core mechanics of the exhaustive maze routing and the heuristic line-probe algorithms. Following this, "Applications and Interdisciplinary Connections" will demonstrate how these pathfinders are adapted for real-world complexities, including timing-driven routing, multi-pin nets, and iterative congestion negotiation, with connections to formal optimization theory. Finally, "Hands-On Practices" will allow you to apply these concepts to concrete problems, solidifying your understanding of how routing decisions are made.

## Principles and Mechanisms

In the physical design of modern integrated circuits, routing is the process of defining the precise metal paths that connect the terminals of all signal nets on a chip. Given its immense complexity, this process is conventionally divided into two stages: global routing and detailed routing. This chapter delves into the fundamental principles and core algorithmic mechanisms of global routing, focusing on the foundational maze and line-probe algorithms. We will establish the abstract model used by global routers, explore its physical and geometric underpinnings, and analyze the algorithms that navigate this model to produce a routable design.

### The Global Routing Problem: Abstraction and Objectives

Global routing operates on a simplified, abstract representation of the chip's layout. The primary goal is to determine the general pathways for all nets while managing the overall distribution of wiring to avoid regions that lack sufficient physical resources. This process serves to guide the subsequent, much more detailed, phase of routing.

#### The Grid Graph Abstraction

The continuous and complex physical space of a chip is discretized into a **[grid graph](@entry_id:275536)**, $G=(V, E)$. The vertices $V$ of this graph do not represent individual atomic locations but rather coarse regions of the chip, typically called **Global Cells (GCells)**. An edge $e \in E$ exists between two vertices if their corresponding GCells are adjacent and share a routable boundary. This graph provides a topological map of the available routing channels.

A **netlist**, $\mathcal{N}=\{N_1, \ldots, N_m\}$, specifies the required connections. Each net $N_k$ is defined by a set of terminals, $T_k$, which are the pins of logic gates that must be electrically connected. These physical pin locations are mapped to their corresponding vertices in the [grid graph](@entry_id:275536). The task is to find a routing solution for each net on this graph. For a two-pin net, this solution is a path; for a multi-pin net, it is a tree connecting all terminals in $T_k$ .

#### Edge Capacity: The Physical Basis of Routing Resources

A critical attribute of the [grid graph](@entry_id:275536) model is the **edge capacity**, $c(e)$, associated with each edge $e \in E$. This integer value represents the maximum number of individual wires that can cross the boundary between the two adjacent GCells represented by the edge. The concept of capacity is not arbitrary; it is derived directly from the physical constraints of the manufacturing process .

On each metal layer of the chip, design rules dictate a minimum wire width and minimum spacing between wires. This defines a **track pitch**, which is the center-to-center distance between parallel wires. The total number of available tracks across a GCell boundary of length $L_e$ on a given layer $\ell$ with pitch $p_\ell$ is approximately $\lfloor L_e / p_\ell \rfloor$.

However, the true capacity is a more nuanced calculation. The total capacity of a GCell edge $e$ is the sum of capacities from all metal layers that can be used to cross that boundary. Typically, layers have a **preferred routing direction** (e.g., horizontal or vertical). For a horizontal edge, only layers with a horizontal preference would primarily contribute to its capacity. Furthermore, several factors reduce the theoretical maximum:

*   **Blockages**: Large macros or IP blocks on the chip may partially or fully obstruct routing channels, reducing the effective boundary length. This is often modeled by a blockage factor, $\alpha_e \in [0, 1]$.
*   **Reserved Tracks**: A certain number of tracks, $r_\ell$, are often reserved for non-signal purposes, such as power delivery (power rails) or clock distribution networks. These must be subtracted from the total available tracks.
*   **Utilization Factors**: A general utilization factor, $\eta_e \le 1$, is often applied to account for a variety of second-order effects like via blockages, local routing complexity, and manufacturing variability that make it impossible to use 100% of the calculated tracks.

Combining these factors, the capacity contribution from a single layer $\ell$ with preferred direction aligned with edge $e$ can be formulated as $c_\ell(e) = \lfloor \eta_e (\lfloor \alpha_e L_e / p_\ell \rfloor - r_\ell) \rfloor$. The total edge capacity $c(e)$ is then the sum of these contributions over all relevant layers, $c(e) = \sum_{\ell} c_\ell(e)$. This capacity model is the primary mechanism by which global routing constrains itself to physically realizable solutions .

#### Formal Objectives and the Distinction from Detailed Routing

The primary goal of global routing is to find a path or tree for each net such that the resource constraints are satisfied. Let $u(e)$ be the **demand** or usage of an edge $e$, defined as the total number of nets whose routes pass through that edge. The fundamental feasibility constraint is that for all edges in the graph, demand must not exceed capacity:
$$ \forall e \in E, \quad u(e) \le c(e) $$

In many dense designs, finding a solution that satisfies all capacity constraints is impossible. The problem then becomes an optimization task to minimize the extent of the violations. A standard objective is to minimize the total **overflow**, which is the sum of all capacity violations across the chip:
$$ \text{Minimize} \sum_{e \in E} \max\{0, u(e) - c(e)\} $$

Secondary objectives, such as minimizing the total estimated wirelength and the number of vias (layer changes), are also crucial for performance and power consumption. The problem can be framed as a complex integer **Multi-Commodity Flow (MCF)** problem, where each net is a commodity to be routed subject to shared capacity constraints .

The output of a global router is not a set of precise, manufacturable wire geometries. Instead, it produces a **routing guide** for each net—a sequence of GCells or grid edges that the net should traverse. This guide serves as the primary input for the **detailed router**. Detailed routing takes these guides and performs the final, exact placement of wires onto specific tracks and metal layers. It is at the detailed routing stage that all manufacturing **Design Rule Checks (DRCs)**—such as precise wire widths, spacing rules, and via enclosure rules—are rigorously enforced to produce a DRC-clean layout. Global routing operates at a coarse level of abstraction, focusing on congestion, while detailed routing operates at the exact geometric level, focusing on DRCs .

### Geometric and Cost Foundations of Rectilinear Routing

The vast majority of digital [integrated circuits](@entry_id:265543) employ a **[rectilinear routing](@entry_id:1130733)** style, where all wire segments are constrained to be either horizontal or vertical. This is a direct consequence of both manufacturing processes and the use of orthogonal preferred-direction metal layers to simplify the routing problem. This constraint has a profound impact on the geometry of shortest paths.

In an obstacle-free grid with uniform costs, any path between two points $p=(x_p, y_p)$ and $q=(x_q, y_q)$ composed of axis-parallel segments must have a length of at least $|x_p - x_q| + |y_p - y_q|$. This value is the **Manhattan distance**, also known as the **$L_1$ distance**, $d_1(p,q)$. Because it is always possible to construct a rectilinear path with exactly this length (e.g., by moving horizontally by $\Delta x$ and then vertically by $\Delta y$), the Manhattan distance is the canonical metric for shortest-path length in unweighted rectilinear grids. Search algorithms, such as [breadth-first search](@entry_id:156630), will expand their wavefronts in diamond-shaped patterns corresponding to $L_1$ distance balls .

In a more realistic model, the cost of traversing the grid is not uniform. As discussed, metal layers have preferred directions. Moving a unit distance horizontally on a horizontal-preference layer might have a low cost, while moving the same distance vertically (a "wrong-way" jog) would incur a higher cost. If the cost per unit step is $p_x$ horizontally and $p_y$ vertically, the obstacle-free shortest path cost becomes a **weighted $L_1$ metric**: $p_x |x_p - x_q| + p_y |y_p - y_q|$. Furthermore, changing layers requires inserting a **via**, which adds its own cost, $c_v$, due to increased resistance and manufacturing challenges. An A-star (A*) [search algorithm](@entry_id:173381), a popular choice for this problem, can use the pure weighted $L_1$ distance as an **admissible heuristic**—a lower-bound estimate of the true remaining cost—because the true cost will include these terms plus any additional costs from detours around obstacles and via insertions .

### Core Algorithms for Two-Pin Nets

We now turn to the two dominant families of algorithms for finding a path between a source and a target pin on the [grid graph](@entry_id:275536).

#### Maze Routing: The Exhaustive Approach

The most fundamental [global routing algorithm](@entry_id:1125679) is **maze routing**, pioneered by C.Y. Lee. In its basic form for an unweighted grid (where every edge has a uniform cost of 1), the **Lee algorithm** is a direct application of **Breadth-First Search (BFS)** .

The algorithm works by propagating a "wave" from the source vertex $s$. It uses a simple First-In-First-Out (FIFO) queue. Initially, only $s$ is in the queue. The algorithm repeatedly dequeues a vertex and "explores" all its unvisited, non-obstacle neighbors, enqueuing them and marking them as visited. The process continues until the target vertex $t$ is dequeued. The path is then recovered by [backtracking](@entry_id:168557) from $t$ to $s$ using predecessor pointers stored during the expansion.

The Lee algorithm provides two powerful guarantees for unweighted grids:
1.  **Completeness**: If a path exists between the source and target, the Lee algorithm is guaranteed to find it. The wavefront will eventually propagate through any traversable channel, however convoluted.
2.  **Optimality**: Because BFS explores the graph in layers of increasing distance from the source, the first time it reaches the target, it is guaranteed to have done so via a path with the minimum possible number of edges. In a unit-cost grid, this is a shortest-path guarantee.

This optimality does not depend on any tie-breaking rules in the queue; any path found will have the minimal length .

To handle the more realistic scenario of weighted edges (due to anisotropic layer costs, congestion penalties, etc.), the Lee algorithm is generalized. This generalization is precisely **Dijkstra's algorithm**. Instead of a FIFO queue, which treats all frontier nodes equally, Dijkstra's algorithm employs a **[priority queue](@entry_id:263183)** keyed by the cumulative path cost from the source. At each step, it extracts the vertex from the [priority queue](@entry_id:263183) with the minimum tentative cost and relaxes its neighbors. The use of a [priority queue](@entry_id:263183) ensures that the [wavefront](@entry_id:197956) expands in order of increasing path cost, not just hop count. This guarantees finding the minimum-cost path, provided all edge weights are non-negative, a condition that holds in routing .

The choice of [data structure](@entry_id:634264) for the [priority queue](@entry_id:263183) is critical for performance. A simple implementation using an unsorted array would require scanning all vertices to find the minimum-cost node at each step, leading to an $O(|V|^2)$ runtime. By using a more efficient data structure like a [binary heap](@entry_id:636601), where `extract-min` and `decrease-key` operations take $O(\log|V|)$ time, the overall complexity of Dijkstra's algorithm is reduced to $O(|E|\log|V|)$. For sparse grid graphs where $|E| \approx |V|$, this is a significant asymptotic improvement, justifying the use of a [priority queue](@entry_id:263183) over a simple array .

Let's consider a concrete example . Imagine routing from $S=(0,0)$ to $T=(3,3)$ on a $4 \times 4$ grid with two layers, $L_1$ and $L_2$. Let $L_1$ be a preferred-horizontal layer (horizontal cost 1, vertical cost 2) and $L_2$ be a preferred-vertical layer (horizontal cost 2, vertical cost 1). Let vias cost 2. Suppose a vertical wall of obstacles blocks column 1 on $L_1$. A simple path on $L_1$ might seem appealing, but the high vertical cost on this layer makes it expensive. A weighted maze router (Dijkstra's) would explore multiple options simultaneously. It might expand along $L_1$ vertically, incurring a cost of 2 for each step. At the same time, it could explore taking a via to $L_2$ (cost 2), moving vertically on $L_2$ (cost 1 per step), and then taking another via back to $L_1$. By maintaining the minimum cumulative cost in its [priority queue](@entry_id:263183), the algorithm might discover, for instance, that a path staying entirely on $L_1$ by going around the obstacles is cheaper than one involving multiple layer changes, or vice-versa, depending on the exact costs. For a path from $(0,0,L_1)$ to $(3,3,L_1)$ with obstacles at $\{(0,1,L_1), (1,1,L_1), (2,1,L_1)\}$, a shortest path might be $(0,0,L_1) \to (1,0,L_1) \to (2,0,L_1) \to (3,0,L_1) \to (3,1,L_1) \to (3,2,L_1) \to (3,3,L_1)$. This path involves 3 horizontal steps and 3 vertical steps, all on layer $L_1$. The total cost is $3 \times (\text{horizontal cost on } L_1) + 3 \times (\text{vertical cost on } L_1) = 3 \times 1 + 3 \times 2 = 9$. Dijkstra's algorithm would systematically find this path by correctly evaluating all alternatives .

#### Line-Probe Routing: The Heuristic Approach

While maze routing is robust and optimal, its "blind" expansion can be computationally expensive, often exploring a large area of the grid. **Line-probe algorithms** offer a faster, more directed alternative by using heuristics to guide the search.

A classic and powerful example is **Hadlock's algorithm**, which, like Dijkstra's, is also complete and optimal but employs a more specialized search strategy for rectilinear grids . The core concept is the **detour number**, $k$. A move is considered a "towards" move if it decreases the Manhattan distance to the target $T$, and an "away" move if it increases it. The detour number $k$ of a path is simply the number of "away" moves it contains. The total length $L$ of any path from a source $S$ to $T$ is given by the elegant formula:
$$ L = d_1(S, T) + 2k $$
This formula highlights that finding a shortest-length path is equivalent to finding a path with the minimum possible detour number.

Hadlock's algorithm implements a best-first search on $k$. It explores all possible paths with $k=0$ first. This is done by extending **line probes**—straight line segments—from the source only in "towards" directions. If the target is not found, it then begins generating and exploring paths with $k=1$. This is done by taking a frontier point from the $k=0$ search and making a single "away" move, then continuing from there with "towards" moves. This layered search, managed by a bucketed [priority queue](@entry_id:263183) (one bucket per value of $k$), guarantees that the first path found to the target will have the minimum possible $k$ and thus minimum length.

For example, to route from $S=(0,0)$ to $T=(4,0)$ with an obstacle blocking the direct path at $(1,0), (2,0), (3,0)$, a $k=0$ search would fail immediately as the only "towards" move is into an obstacle. The algorithm would then initiate a $k=1$ search. It could make one "away" move from $S$, say to $(0,1)$. From there, it would proceed with "towards" moves: a line probe rightwards to $(4,1)$, followed by a final "towards" move down to the target $T=(4,0)$. This path has $k=1$ and is the shortest possible detour .

#### Comparative Analysis

The fundamental difference between maze and line-probe algorithms lies in their search strategy.
*   **Lee's Algorithm (BFS/Dijkstra's)** is an **uninformed** or **best-first search** that expands based on accumulated cost. Its [wavefront](@entry_id:197956) propagates isotropically. To connect points separated by Manhattan distance $D$, it typically explores a diamond-shaped region containing $\Theta(D^2)$ vertices.
*   **Line-Probe Algorithms (A*/Hadlock's)** are **informed** or **heuristic searches**. They use the goal location to direct the search. By prioritizing paths that head towards the target, the search is confined to a narrow corridor around the final route. In sparse obstacle environments, the number of vertices explored is typically only $O(D)$.

In terms of worst-case [time complexity](@entry_id:145062) on an $m \times n$ grid, Lee's algorithm (BFS) is $O(mn)$, while a priority-queue-based line-probe or weighted maze router is $O(mn \log(mn))$. However, the practical performance is dictated by the typical number of visited nodes. The quadratic versus [linear scaling](@entry_id:197235) of visited nodes ($D^2$ vs. $D$) means that for most practical instances, heuristic line-probe methods are significantly faster and more memory-efficient than uninformed maze routers .

### Handling Multi-Pin Nets and Congestion

Real-world designs involve nets with many terminals and intense competition for routing resources. The simple two-pin [routing algorithms](@entry_id:1131127) must be extended to handle these complexities.

#### The Challenge of Multi-Pin Nets

For a net with more than two terminals, the objective is to connect all of them with a tree structure of minimum total wirelength. The [ideal solution](@entry_id:147504) in a rectilinear grid is the **Rectilinear Steiner Minimum Tree (RSMT)**. An RSMT connects all terminals and may introduce new vertices, called **Steiner points**, to reduce the total length .

The RSMT should be distinguished from a **Minimum Spanning Tree (MST)**. An MST is constructed on a graph whose vertices are only the terminals themselves; it does not permit the introduction of Steiner points. Since an MST is a more constrained structure, its length is always greater than or equal to the length of the RSMT:
$$ \text{Length}(\text{RSMT}) \le \text{Length}(\text{MST}) $$
The ability to add Steiner points, for example at the [intersection of lines](@entry_id:153322) forming the bounding box of a set of terminals, can significantly reduce total wirelength. The famous **Hanan Grid Theorem** proves that there always exists an RSMT whose Steiner points lie on the grid formed by passing horizontal and vertical lines through all terminals. While this reduces the search space, the problem of finding the exact RSMT remains **NP-hard**.

Due to this [computational complexity](@entry_id:147058), practical global routers do not compute exact RSMTs for every net. Instead, they rely on efficient **[heuristics](@entry_id:261307)**. A common approach is to first compute an MST on the terminals and then decompose the multi-pin net into a set of two-pin connections, which are then routed sequentially using maze or line-probe algorithms .

#### Managing Congestion: Iterative Routing

The most significant challenge in global routing is managing congestion. Routing each net independently to minimize its own wirelength will inevitably lead to massive overflow in popular channels. To address this, global routers employ an **iterative** approach. The most common scheme is "rip-up and reroute," where nets are routed sequentially. After each net is routed, the demand on the edges it uses is updated.

To guide the routing process, the cost function for the pathfinding algorithm is made congestion-aware. The cost of traversing an edge is no longer just its physical length but also includes a penalty that depends on its current level of congestion. A common formulation for the global objective combines wirelength and overflow via a weighted sum, parameterized by a trade-off parameter $\lambda \ge 0$ :
$$ J_{\lambda} = (\text{Total Wirelength}) + \lambda \cdot (\text{Total Overflow}) $$
This can be written as:
$$ J_{\lambda} = \sum_{e \in E} w(e) u(e) + \lambda \sum_{e \in E} \max\{0, u(e) - c(e)\} $$
where $w(e)$ is the length of edge $e$ and $u(e)$ is its usage.

As $\lambda \to 0$, the objective is simply to minimize wirelength. As $\lambda \to \infty$, the penalty for any overflow becomes immense, forcing the router to prioritize finding a congestion-free solution if one exists. This objective function induces a dynamic, iteration-dependent cost for each edge. When routing a new net, the cost of an edge $e$ with current demand $u(e)$ and capacity $c(e)$ can be set to:
$$ \text{cost}(e) = w(e) + \text{penalty}(u(e), c(e)) $$
A simple penalty might be zero if $u(e)  c(e)$ and a large value (related to $\lambda$) if $u(e) \ge c(e)$. More sophisticated functions use a smooth, nonlinear increase in cost as demand approaches and exceeds capacity.

By iteratively routing nets with these congestion-aware costs, the system naturally balances wirelength and congestion. Nets routed early might take direct paths. As certain regions become congested, the edge costs in those regions increase, steering later nets to find detours through less crowded areas. This iterative feedback mechanism is the cornerstone of modern global routing, enabling maze and line-probe algorithms to collectively produce high-quality, routable solutions for millions of nets.