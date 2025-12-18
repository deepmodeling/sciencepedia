## Introduction
Connectivity is the cornerstone of network science, but in systems that evolve, the simple existence of a connection is not enough—its timing is everything. While static networks offer a snapshot of potential interactions, [temporal networks](@entry_id:269883) capture the dynamic reality where paths are governed by the relentless [arrow of time](@entry_id:143779). This article delves into the critical concepts of [temporal paths](@entry_id:1132930) and [reachability](@entry_id:271693), exploring how the dimension of time fundamentally reshapes our understanding of connectivity. The core problem this article addresses is the insufficiency of [static analysis](@entry_id:755368), which often leads to incorrect conclusions about causality and influence by ignoring the sequence and timing of events. By navigating this material, you will gain a deep understanding of the formal principles that govern time-respecting connectivity.

This exploration is structured across three key chapters. The first, "Principles and Mechanisms," lays the theoretical foundation, defining what constitutes a valid temporal path and introducing the models and algorithms used to analyze them. The second chapter, "Applications and Interdisciplinary Connections," demonstrates the power of these concepts by applying them to real-world phenomena, from the spread of diseases to the flow of information in biological and social systems. Finally, "Hands-On Practices" provides an opportunity to solidify your understanding through practical exercises that highlight the nuances of temporal pathfinding. We begin by establishing the fundamental principles of causality that distinguish [temporal paths](@entry_id:1132930) from their static counterparts.

## Principles and Mechanisms

The analysis of paths and [reachability](@entry_id:271693) forms the bedrock of network science. In static networks, this analysis is straightforward: if a sequence of edges connects two nodes, a path exists. Temporal networks, however, introduce the critical dimension of time, fundamentally reshaping our understanding of connectivity. The mere existence of connections is no longer sufficient; their timing is paramount. This chapter delves into the core principles governing [temporal paths](@entry_id:1132930) and the mechanisms by which we can model and analyze them. We will move from foundational definitions of causality to richer models incorporating real-world complexities, explore algorithmic representations, and dissect the nuanced criteria for what constitutes an "optimal" temporal path.

### Defining Temporal Paths: The Primacy of Causality

The most fundamental distinction between static and [temporal networks](@entry_id:269883) lies in the concept of a **path**. In a static graph, a path is a sequence of adjacent nodes. In a temporal network, a path is a sequence of interactions, or **contacts**, that are causally connected. A contact can be represented as a tuple $(u, v, t)$, signifying an opportunity for transmission from node $u$ to node $v$ at a specific instant $t$.

A sequence of contacts constitutes a **time-respecting path** (or causal path) only if the time of each contact is greater than or equal to the time of the preceding contact. This non-decreasing time sequence is the mathematical embodiment of causality: information or a process cannot travel backward in time.

This temporal ordering constraint has a profound consequence: the existence of a path in a network's static representation does not guarantee reachability in the temporal domain. Consider a network where the static projection—the graph formed by aggregating all contacts over time—contains the path $s \to a \to b \to t$. If the contact $(a,b)$ occurs at time $t=5$ and the contact $(s,a)$ occurs at time $t=10$, no information can flow from $s$ to $b$ via $a$, because one would arrive at $a$ at time $10$ only to find that the "connecting flight" to $b$ departed five time units earlier . Similarly, if we wish to travel from $A$ to $D$ via a static path $A-B-C-D$, but the contacts are $(B,C)$ at $t=1$ and $(A,B)$ at $t=2$, we arrive at $B$ at time $t=2$, having missed the connection to $C$ at $t=1$. In this case, node $D$ is unreachable from $A$, despite their connection in the static view .

The causality constraint can be defined in two primary ways, a distinction that becomes crucial when multiple contacts occur simultaneously .

A **non-strict [time-respecting path](@entry_id:273041)** is a sequence of contacts $((v_0, v_1, t_1), (v_1, v_2, t_2), \dots, (v_{k-1}, v_k, t_k))$ where the contact times are non-decreasing, i.e., $t_{i+1} \ge t_i$ for all $i$. This definition allows for "instantaneous" travel across multiple nodes if contacts are available at the same time. For example, given contacts $(a,b,1)$ and $(b,c,1)$, a non-strict path from $a$ to $c$ exists, arriving at time $1$.

A **strict time-respecting path** imposes a more stringent condition: $t_{i+1} > t_i$ for all $i$. This model assumes that even instantaneous travel requires some infinitesimal, unmodeled time, or it simply prohibits the chaining of simultaneous events. In the previous example, the path from $a$ to $c$ via $b$ would be invalid under the strict definition, as it would require $1 > 1$, which is false.

The set of nodes reachable under strict admissibility is always a subset of those reachable under non-strict admissibility. The two definitions of reachability become equivalent if and only if all contacts in the network occur at unique times, as this scenario makes it impossible to form a path where $t_{i+1} = t_i$. The choice between these models depends on the nature of the system being studied: non-strict models may be suitable for information diffusion in digital systems, while strict models might better represent physical transport.

Finally, any analysis of [reachability](@entry_id:271693) must consider a starting condition, typically a source node $s$ and a start time $\tau$. A path can only begin with a contact $(u_0, u_1, t_1)$ where $u_0=s$ and its departure time $t_1$ is at or after the start time, $t_1 \ge \tau$.

### Richer Models: Incorporating Durations, Delays, and Policies

The simple model of instantaneous contacts can be extended to capture more realistic features of real-world systems. These include the duration of travel, policies on waiting, and the nature of the time domain itself.

#### Latency and Availability

A more descriptive model represents a contact as a tuple $(u, v, t, \lambda)$, where $t$ is the **departure time** from $u$ and $\lambda > 0$ is the **traversal time** or **latency**. An agent departing $u$ at time $t$ arrives at $v$ at time $t + \lambda$. This introduces a duration to each traversal, a feature present in nearly all transportation and [communication systems](@entry_id:275191)  .

#### Waiting Policies

The ability to wait at a node is a critical factor in [temporal reachability](@entry_id:1132932). If an agent arrives at node $v_i$ at time $t_{arr,i}$ and the next desired contact $(v_i, v_{i+1}, t_{i+1}, \lambda_{i+1})$ departs at $t_{i+1} > t_{arr,i}$, the agent must wait. This leads to two primary waiting policies :

1.  **Waiting Allowed**: The departure time for the next leg of the journey, $t_{i+1}$, must simply be after the arrival from the previous leg. The timing constraint for a path is $t_{i+1} \ge t_i + \lambda_i$. This flexibility can be crucial for connecting contacts whose availability windows are misaligned.
2.  **Waiting Disallowed**: The connection must be immediate. The constraint becomes $t_{i+1} = t_i + \lambda_i$. This models "just-in-time" systems.

The set of reachable nodes when waiting is disallowed is a subset of those reachable when waiting is allowed. For many networks, this inclusion is strict; there exist paths that are only possible because of the ability to wait at an intermediate node for a later connection.

#### Discrete versus Continuous Time

The nature of the time domain, $\mathcal{T}$, also has subtle but important implications .
In a **discrete-time model**, where $\mathcal{T} = \{0, 1, \dots, T\}$, time progresses in integer steps. An inequality like $t_{i+1} > t_i + 1$ is equivalent to $t_{i+1} \ge t_i + 2$, a distinction that can dramatically alter [reachability](@entry_id:271693).

In a **continuous-time model**, where $\mathcal{T} = [0, T]$, edge availability might be defined over intervals. A common modeling convention for a traversal with latency $\lambda_i > 0$ starting at time $t_i$ is that the edge must be available for the entire duration $[t_i, t_i + \lambda_i]$. This gives rise to topological subtleties. For example, changing an availability interval from closed, $[a,b]$, to half-open, $(a,b]$, removes the single point $a$. While this change is on a set of Lebesgue [measure zero](@entry_id:137864), it can completely break reachability if a path relies on a seamless connection at the precise instant $a$  .

#### Advanced Node Constraints

To add further realism, we can introduce node-specific constraints on waiting . Upon arriving at a node $x$ at time $t_{arr}$, an agent might be required to stay for a **minimal dwell time** $\sigma(x)$ (e.g., for servicing) and might be prohibited from waiting longer than a **maximal waiting time** $W(x)$. In this case, the departure time $t_{dep}$ for the next contact must fall within the window $[t_{arr} + \sigma(x), t_{arr} + W(x)]$. These constraints add another layer of complexity to pathfinding, restricting the set of valid [temporal paths](@entry_id:1132930).

### Algorithmic Representations of Temporal Networks

To apply computational algorithms for finding and analyzing [temporal paths](@entry_id:1132930), we must first map the temporal network onto a static graph structure. Two primary representations serve this purpose: the time-unfolded graph and the [event graph](@entry_id:1124707).

#### The Time-Unfolded Graph

The **time-unfolded graph**, or [time-expanded graph](@entry_id:274763), is an intuitive way to represent a discrete-time temporal network as a static, [directed acyclic graph](@entry_id:155158) (DAG) . The construction is as follows:
- For each node $v$ in the original network and each time step $\tau$ in the horizon $\{0, 1, \dots, T\}$, we create a node-time pair $(v, \tau)$ in the unfolded graph.
- Two types of edges are created:
    1.  **Waiting Edges**: For each node $v$ and time $\tau  T$, a directed edge is drawn from $(v, \tau)$ to $(v, \tau+1)$. This represents waiting at node $v$ for one time step. Its weight is the duration of waiting, typically $1$.
    2.  **Temporal Edges**: For each contact $(u, v, t, \lambda)$ in the original network, a directed edge is drawn from the node-time pair $(u, t)$ to $(v, t+\lambda)$. This represents traversing the contact. Its weight is the latency $\lambda$.

In this unfolded DAG, any directed path from a source $(s, \tau_0)$ to a destination $(d, \tau_{final})$ corresponds to a valid time-respecting path in the original network. The total weight of the path in the unfolded graph is $\tau_{final} - \tau_0$, the total elapsed time. This construction brilliantly transforms the problem of finding the earliest arrival time into a standard [single-source shortest path](@entry_id:633889) (SSSP) problem on a DAG, which can be solved efficiently by processing nodes in their natural [topological order](@entry_id:147345) (i.e., by increasing time).

For example, to find the earliest arrival at node $E$ from $(A,0)$ in a given network, we can explore reachable node-time pairs chronologically . If from $(A,0)$ we can take a contact $(A,C,0,1)$, we reach state $(C,1)$. From $(C,1)$, a contact $(C,B,1,1)$ leads to $(B,2)$. From $(B,2)$, a contact $(B,E,2,1)$ leads to $(E,3)$. Since this is the first time we have reached a state involving node $E$, and our search proceeds chronologically, we can conclude that the earliest arrival time at $E$ is $3$.

#### The Event Graph

An alternative, often more compact, representation is the **[event graph](@entry_id:1124707)** (or [line graph](@entry_id:275299) of the temporal network) . In this construction, the nodes of the new graph are the *events* (contacts) of the original temporal network. A directed edge is drawn from event $e_i = (u_i, v_i, t_i, \lambda_i)$ to event $e_j = (u_j, v_j, t_j, \lambda_j)$ if and only if $e_j$ can causally follow $e_i$. This requires two conditions:
1.  **Spatial Contiguity**: The end node of $e_i$ must be the start node of $e_j$, i.e., $v_i = u_j$.
2.  **Temporal Feasibility**: The departure time of $e_j$ must be valid given the arrival from $e_i$. The arrival at node $v_i$ occurs at time $t_i + \lambda_i$. The departure time $t_j$ must respect this arrival time, plus any node-specific waiting constraints. For example, with minimal dwell time $\sigma(v_i)$ and maximal wait time $W(v_i)$, the condition becomes $t_i + \lambda_i + \sigma(v_i) \le t_j \le t_i + \lambda_i + W(v_i)$.

A [time-respecting path](@entry_id:273041) in the original network corresponds to a path in this [event graph](@entry_id:1124707). This representation is particularly powerful for analyzing sequences of events and can be more memory-efficient than the time-unfolded graph if the number of contacts is much smaller than the number of nodes multiplied by the number of time steps.

### Characterizing and Optimizing Temporal Paths

In a static graph, the "best" path is often unambiguously the "shortest" path, minimizing either hop count or a sum of static weights. In [temporal networks](@entry_id:269883), the notion of optimality is multifaceted, giving rise to several distinct optimization criteria.

#### Shortest vs. Earliest-Arrival Paths

A path with the minimum number of contacts, or **shortest path**, is not necessarily the path that gets you to your destination at the earliest time. The **earliest-arrival path** is the one that minimizes the final arrival time. A traveler may be faced with a choice: a direct, one-hop flight that leaves in 19 hours, or a two-hop journey with well-timed connections that starts in 3 hours. The direct flight is the shortest path, but the two-hop journey might offer a much earlier arrival. In one such scenario, the direct path arrives at time 20, while the two-hop path arrives at time 7, clearly demonstrating that the shortest path can be temporally suboptimal due to long, unavoidable waiting times .

#### Foremost vs. Fastest Paths

Even when focusing on time, there are two key measures of path quality :
- The **foremost path** (or earliest-arrival path) is the one that minimizes the final arrival time, regardless of when it departs or how long it takes.
- The **fastest path** is the one that minimizes the total travel duration, defined as (arrival time - departure time).

These two are not always the same. Consider two options to travel from $s$ to $z$:
1.  Path A departs at $t=0$ and arrives at $t=4$. (Duration = 4)
2.  Path B departs at $t=5$ and arrives at $t=7$. (Duration = 2)

Here, Path A is the foremost path because it arrives earlier ($4  7$). However, Path B is the fastest path because its duration is shorter ($2  4$). This captures a familiar trade-off: one might choose to wait for a later, but more efficient, mode of transport to minimize time spent "in transit". The choice between optimizing for arrival time versus duration depends entirely on the application's goal.

#### Paths with Deadlines

In many real-world scenarios, the goal is not simply to arrive as early as possible, but to arrive before a specific **deadline** $D_{dead}$. A path is feasible if its final arrival time is less than or equal to the deadline. Analyzing feasibility requires careful accounting of both traversal latencies and waiting times. A common pitfall is to assume that if the sum of a path's latencies is less than the available time slack ($D_{dead} - t_{start}$), the path is feasible. This is incorrect, as it ignores the mandatory waiting time forced by misaligned contact schedules. A path with a low sum of latencies may be temporally infeasible or may accumulate so much waiting time that it misses the deadline .

This challenge highlights the utility of search algorithms (like A*) guided by a heuristic. A good heuristic is a lower bound on the remaining travel time. For example, $L(v)$, the minimum possible cumulative latency from the current node $v$ to the destination, can be pre-calculated on a static projection of the network. During a search, if an agent reaches node $v$ at time $t_{current}$, and $t_{current} + L(v)  D_{dead}$, this entire search branch can be pruned, as no possible completion can meet the deadline.

### Extensions of the Model: Multiplex Temporal Networks

The principles of [temporal paths](@entry_id:1132930) can be extended to more complex network structures, such as **[multiplex networks](@entry_id:270365)**. A multiplex network consists of a single set of nodes connected by contacts that exist on different **layers**. These layers can represent different modes of transportation (bus, subway, taxi), different channels of communication, or different types of social relationships.

A key feature of pathfinding in such networks is the ability to switch between layers at a node. This action is typically not free and incurs an **inter-layer switching delay**, $\sigma \ge 0$ . This delay accounts for the time it takes to, for example, walk from a bus station to a subway station.

The definition of a time-respecting path is elegantly extended to this context. For a sequence of contacts, we track the layer of each contact. When moving from a contact on layer $\ell_{i-1}$ to one on layer $\ell_i$:
- If the layer is the same ($\ell_i = \ell_{i-1}$), the standard causality constraint applies: the departure time $t_i$ must be no earlier than the arrival time $\tau_{i-1}$.
- If the layer changes ($\ell_i \neq \ell_{i-1}$), the switching delay must be paid. The departure time $t_i$ must be no earlier than the arrival time plus the delay: $t_i \ge \tau_{i-1} + \sigma$.

This piecewise timing constraint formally captures the dynamics of navigation through a multi-modal temporal system, demonstrating the flexibility and power of the temporal path framework.