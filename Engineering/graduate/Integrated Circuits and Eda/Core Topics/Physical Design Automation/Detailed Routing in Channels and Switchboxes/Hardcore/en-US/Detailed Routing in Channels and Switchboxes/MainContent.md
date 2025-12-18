## Introduction
Detailed routing represents a crucial final stage in the [physical design](@entry_id:1129644) of integrated circuits, where the abstract connectivity of a netlist is transformed into a precise, manufacturable geometric layout. Following the global routing phase which defines coarse pathways, detailed routing tackles the intricate challenge of assigning exact wire paths within confined regions like channels and switchboxes. This process is far from a simple connect-the-dots exercise; it is a complex optimization problem governed by a dense web of physical, electrical, and manufacturing constraints. The knowledge gap this article addresses is the bridge between the theoretical models of routing and their practical application in creating high-performance, reliable, and manufacturable microchips.

This article will guide you through the multifaceted world of detailed routing in three parts. In the **Principles and Mechanisms** chapter, we will establish the foundational models of the routing environment, formalize the key constraints that govern any valid solution, and explore the core algorithms developed to solve the [channel routing](@entry_id:1122264) problem. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate how these fundamental techniques are extended to address real-world challenges, including timing optimization, signal integrity, and Design for Manufacturability (DFM). Finally, the **Hands-On Practices** section provides concrete exercises to apply these concepts, from constructing [constraint graphs](@entry_id:267131) to performing design rule checks, solidifying your understanding of this critical EDA domain.

## Principles and Mechanisms

This chapter delves into the foundational principles and mechanisms of detailed routing, a critical stage in the physical design of [integrated circuits](@entry_id:265543). Following the global routing phase, which allocates coarse pathways for interconnects, detailed routing determines the exact geometric paths for each net within confined regions such as channels and switchboxes. We will begin by constructing a precise model of the routing environment, then formalize the constraints that govern any valid solution, and finally explore the core algorithms developed to navigate these constraints and achieve a manufacturable layout.

### The Routing Environment: Physical and Mathematical Models

Successful detailed routing begins with a precise understanding of the physical space where wires will be placed. This space is not a continuous void but a highly structured and constrained environment defined by the manufacturing process.

#### Physical Resources: Tracks, Layers, and Vias

In modern Very Large-Scale Integration (VLSI) design, routing is performed on multiple layers of metal, separated by dielectric insulators. A common and effective model is the **Manhattan routing** scheme, where wires on a given layer are restricted to run in a single **preferred direction**, either horizontal or vertical. For instance, a typical three-layer stack might use the first metal layer ($\text{M}_1$) for horizontal routing, the second ($\text{M}_2$) for vertical, and the third ($\text{M}_3$) for horizontal again .

Within each layer, wires are placed on a grid of virtual lines known as **routing tracks**. These tracks represent valid centerlines for wires. The center-to-center distance between adjacent tracks is called the **track pitch**. The pitch is not an arbitrary value; it is carefully determined by the process **design rules** to prevent electrical shorts and other manufacturing defects between adjacent wires. As a first-order approximation, the pitch $p$ is the sum of the minimum wire width $w$ and the minimum wire spacing $s$, i.e., $p = w + s$.

However, a more rigorous derivation of track pitch must account for various manufacturing constraints . The effective width of a wire on a track, $W_{\text{eff}}$, is not just the minimum width $w_{\min}$, but the maximum of all width-related constraints. These include:
1.  The fundamental **minimum wire width**, $w_{\min}$.
2.  The width required for **via enclosure**. A **via** is a connection between two different metal layers. The metal on each layer must extend beyond the via's boundary by a minimum enclosure distance, $e_{\min}$. For a square via of side length $a_v$, the metal pad surrounding it must have a width of at least $W_{\text{via}} = a_v + 2e_{\min}$.
3.  The width dictated by the **minimum area rule**. To ensure that small metal features are not etched away during manufacturing, any isolated piece of metal must have a minimum area, $A_{\min}$. For a short wire stub of length $L_{\min}$, its width must be at least $W_{\text{area}} = A_{\min} / L_{\min}$.

The effective track width is therefore $W_{\text{eff}} = \max(w_{\min}, W_{\text{via}}, W_{\text{area}})$. The minimum track pitch is then $P = W_{\text{eff}} + s_{\min}$, often rounded up to the nearest multiple of the layout grid for quantization. For example, given rules $w_{\min} = 0.06\,\mu\mathrm{m}$, $s_{\min} = 0.06\,\mu\mathrm{m}$, $e_{\min} = 0.01\,\mu\mathrm{m}$, $a_v = 0.05\,\mu\mathrm{m}$, and $A_{\min} = 0.012\,\mu\mathrm{m}^2$ with $L_{\min} = 0.20\,\mu\mathrm{m}$, the governing width is from via enclosure ($W_{\text{via}} = 0.05 + 2 \times 0.01 = 0.07\,\mu\mathrm{m}$). The pitch is thus at least $0.07\,\mu\mathrm{m} + 0.06\,\mu\mathrm{m} = 0.13\,\mu\mathrm{m}$ .

The routing space is partitioned into specific region types. A **channel** is a rectangular routing region typically bounded by two rows of pins on opposite sides (e.g., top and bottom). A **switchbox** is a more complex region, usually square or rectangular, with pins on all four sides. The total number of available routing tracks and potential via sites within these regions constitutes the available routing resources. These resources are often reduced by **keep-out zones** adjacent to the pin rows to ensure proper pin access and avoid design rule violations . For instance, in a channel of height $H=10$ grid units with a 1-track keep-out at the top and bottom, the number of available horizontal tracks becomes $10 - 2 = 8$. The number of via sites between two consecutive layers is the product of the available horizontal and vertical tracks in their respective preferred directions.

#### The Grid Graph Model

To reason about routing algorithmically, we abstract this physical environment into a mathematical structure known as a **[grid graph](@entry_id:275536)** . In this model, the routing domain is represented as a three-dimensional grid of points $(x,y,\ell)$, where $(x,y)$ are integer coordinates in the plane and $\ell$ is the layer index.
- **Vertices** of the graph correspond to these grid points.
- **Edges** represent potential wire segments and vias.
    - **Wire edges** connect adjacent vertices on the same layer, e.g., $((x,y,\ell), (x+1,y,\ell))$. These correspond to rectilinear wire segments.
    - **Via edges** connect vertices at the same $(x,y)$ location but on adjacent layers, e.g., $((x,y,\ell), (x,y,\ell+1))$.

A **net** is defined by a set of **terminal vertices**, $T_i \subseteq V$, which are fixed points on the grid corresponding to component pins. The detailed routing problem is then to find, for each net $i$, a [subgraph](@entry_id:273342) $S_i$ of the [grid graph](@entry_id:275536) that connects all terminals in $T_i$. To minimize wire length and delay, this subgraph is typically a tree, known as a **Steiner tree**. The crucial constraint is that the edge sets of the subgraphs for any two different nets, $i$ and $j$, must be disjoint: $E_i \cap E_j = \emptyset$. This condition ensures that no two nets are shorted together.

### The Channel Routing Problem: Constraints and Objectives

While the [grid graph](@entry_id:275536) provides a general framework, [channel routing](@entry_id:1122264) has a more specialized and well-studied structure. The primary objective is to route all nets using the minimum number of horizontal tracks, which translates to minimizing the channel's height. This optimization is governed by two fundamental sets of constraints: horizontal and vertical.

#### Horizontal Constraints and Channel Density

A net that must be connected within the channel has a **horizontal span**, defined by the interval $[l_j, r_j]$ from its leftmost pin column $l_j$ to its rightmost pin column $r_j$. In a simple dogleg-free routing, this net requires a single continuous horizontal wire segment covering this entire interval. Since two different nets cannot occupy the same track at the same column, any two nets whose horizontal spans overlap must be assigned to different tracks.

This observation gives rise to the concept of **[channel density](@entry_id:1122260)**. The density at a specific column $i$, denoted $D(i)$, is the number of nets whose horizontal spans cover that column. The **maximum density**, $D_{\max} = \max_i D(i)$, represents the most congested column in the channel. At this column, $D_{\max}$ distinct nets must be routed in parallel. By [the pigeonhole principle](@entry_id:268698), this requires at least $D_{\max}$ separate tracks. Therefore, the maximum density establishes a fundamental lower bound on the channel width: $T_{\min} \ge D_{\max}$ .

This problem can be formally modeled using a **Horizontal Constraint Graph (HCG)**. The vertices of the HCG are the nets, and an undirected edge connects two nets if their horizontal spans overlap. The problem of assigning nets to tracks to avoid horizontal conflicts is then equivalent to the [graph coloring problem](@entry_id:263322) on the HCG, where tracks are colors. The set of nets active at the column with maximum density forms a **clique** (a fully connected [subgraph](@entry_id:273342)) in the HCG. Since the [chromatic number](@entry_id:274073) of any graph is at least its [clique number](@entry_id:272714), this graph-theoretic view provides a more formal justification for the lower bound: $T_{\min} = \chi(HCG) \ge \omega(HCG) = D_{\max}$  .

#### Vertical Constraints

Horizontal constraints arise from nets competing for space along the channel's length. **Vertical constraints**, in contrast, arise from the pin configuration at a single column. If a column contains a pin for net $u$ on the top boundary and a pin for net $v$ on the bottom boundary, the vertical wire segment connecting to net $u$'s horizontal track must not cross the vertical segment for net $v$. In a standard two-layer model, this is only possible if the horizontal track for net $u$ is physically placed above the horizontal track for net $v$.

These ordering constraints are captured in a directed graph called the **Vertical Constraint Graph (VCG)** . The vertices of the VCG are the nets. A directed edge $u \to v$ is added for every column where net $u$ has a top pin and net $v$ has a bottom pin. This edge signifies the constraint that $\text{track}(u)$ must be above $\text{track}(v)$. A path in the VCG, such as $n_1 \to n_2 \to \dots \to n_k$, implies a chain of ordering constraints requiring $k$ distinct tracks. Therefore, the length of the longest path in the VCG, $L_{\max}$, provides another lower bound on the required number of tracks: $T_{\min} \ge L_{\max}$.

For a dogleg-free routing to be possible, the VCG must be a Directed Acyclic Graph (DAG). If the VCG contains a cycle, for example $A \to C \to B \to A$, it implies an impossible ordering requirement: the track for A must be above the track for C, the track for C must be above the track for B, and the track for B must be above the track for A. Such a configuration makes a dogleg-free routing impossible .

### Fundamental Algorithms for Channel Routing

The dual constraints of the HCG and VCG form the basis for channel [routing algorithms](@entry_id:1131127). The complexity and approach of these algorithms depend on the nature of the constraints present in a given problem.

#### The Left-Edge Algorithm for Unconstrained Channels

In the simplest case, where the VCG is empty (no vertical constraints), the problem reduces to satisfying only the horizontal constraints. This is equivalent to coloring the HCG, which is a special type of graph known as an **[interval graph](@entry_id:263655)**. Interval graphs are [perfect graphs](@entry_id:276112), meaning their [chromatic number](@entry_id:274073) equals their [clique number](@entry_id:272714). Consequently, the minimum number of tracks is exactly $D_{\max}$.

A simple and optimal algorithm for this case is the **Left-Edge Algorithm** . It operates as follows:
1. Sort the net intervals by their left endpoints, $l_j$, in increasing order.
2. Process the nets one by one from this sorted list.
3. For each net, assign it to the first available track (i.e., the lowest-indexed track) where its interval does not overlap with any nets already placed on that track.

This greedy strategy is guaranteed to produce a routing with the minimum possible number of tracks, $D_{\max}$.

#### Handling Vertical Constraints and Doglegs

When vertical constraints are present (but the VCG is acyclic), the problem becomes more complex. Both density and vertical ordering must be respected. A lower bound for the required number of tracks in a dogleg-free solution is given by $T_{\min} \ge \max(D_{\max}, L_{\max})$ . The goal of many algorithms is to achieve this bound.

The **Constrained Left-Edge Algorithm** extends the simple left-edge method to handle the VCG . It maintains a set of "eligible" nets, which are those whose VCG predecessors have all been routed (i.e., nets with an in-degree of 0 in the remaining VCG).
1. Initialize the set of eligible nets $\mathcal{E}$ with all nets that are heads in the VCG (in-degree 0).
2. While $\mathcal{E}$ is not empty:
    a. Select the net $i \in \mathcal{E}$ with the smallest left endpoint $l_i$. Ties can be broken by choosing the net with the smaller right endpoint $r_i$.
    b. Find the lowest-indexed track $t$ that satisfies both:
        i. **Horizontal Constraint:** Net $i$ does not overlap with existing nets on track $t$.
        ii. **Vertical Constraint:** Track $t$ is below the tracks of all of net $i$'s VCG predecessors.
    c. Assign net $i$ to track $t$.
    d. Remove $i$ from the set of unplaced nets. Update the in-degrees of its successors in the VCG. Add any successors whose in-degree becomes 0 to the eligible set $\mathcal{E}$.

This algorithm provides a powerful heuristic for the general [channel routing](@entry_id:1122264) problem.

When the VCG contains a cycle, a dogleg-free solution is impossible. To break the cycle, at least one net involved must be split across multiple tracks using a **dogleg**. A dogleg is a via that allows a net to switch from one horizontal track to another, breaking its single horizontal span into multiple segments. This resolves the rigid vertical ordering constraint for that net. The minimum number of nets that must be doglegged to break all cycles is given by the size of the **minimum feedback vertex set** of the VCG. For a simple cycle like $A \to C \to B \to A$, removing any single vertex breaks the cycle, so the minimum feedback vertex set size is 1, implying at least one dogleg is necessary .

### Broader Context and Complexity

Detailed routing is the final step in a hierarchical process. It takes as input the coarse path assignments from an earlier **global routing** stage . The global router operates on a simplified tile-based abstraction of the layout, using estimated channel capacities to guide its decisions. A key challenge is that these capacity estimates often ignore localized congestion caused by via blockages or pin access issues. Consequently, a global routing solution that appears valid (i.e., does not exceed estimated capacities) may still be unroutable at the detailed stage. This highlights the critical importance of robust detailed [routing algorithms](@entry_id:1131127).

The [channel routing](@entry_id:1122264) problem, while seemingly simple in its formulation, is computationally difficult. While the dogleg-free case with an empty VCG is solvable in [polynomial time](@entry_id:137670), the general [channel routing](@entry_id:1122264) problem (allowing doglegs to minimize track count) is **NP-complete** . This means there is no known efficient algorithm to find the optimal solution for all instances. The NP-completeness is typically proven via a complex reduction from a known hard problem like 3-SAT, where logic gates are constructed using intricate channel and VCG configurations. This [computational hardness](@entry_id:272309) is the primary motivation for the development of powerful and effective heuristics, such as the [constrained left-edge algorithm](@entry_id:1122937) and its many variants, which aim to find high-quality, if not always strictly optimal, solutions in a practical amount of time.