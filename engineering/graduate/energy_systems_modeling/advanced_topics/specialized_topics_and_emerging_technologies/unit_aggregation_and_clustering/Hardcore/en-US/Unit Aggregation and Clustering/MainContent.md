## Introduction
Modeling large-scale energy systems presents a fundamental challenge: the sheer number of individual components—from generators to transmission lines—creates [optimization problems](@entry_id:142739) of intractable size. To make these models computationally manageable, practitioners rely on powerful simplification techniques, with **unit aggregation** and **clustering** chief among them. These methods reduce model complexity by grouping similar physical assets or time periods, but this simplification is not without its risks. The core problem addressed in this article is how to perform this reduction in a principled way, balancing computational efficiency against the loss of fidelity that can lead to inaccurate or physically infeasible results.

This article provides a comprehensive guide to mastering these techniques. The first chapter, **"Principles and Mechanisms,"** will delve into the formal mathematical objectives of aggregation, explaining concepts like relaxation, the Minkowski sum, and the specific challenges of aggregating non-convex constraints. The second chapter, **"Applications and Interdisciplinary Connections,"** will demonstrate how these principles are applied in real-world contexts, from [capacity expansion planning](@entry_id:1122043) and market operations to network reduction, and explore their parallels in other scientific fields. Finally, the **"Hands-On Practices"** section offers practical exercises to solidify your understanding of these core concepts. By progressing through these chapters, you will gain the theoretical foundation and practical insight needed to build robust and reliable energy system models.

## Principles and Mechanisms

In the modeling of large-scale energy systems, a direct representation of every individual component—every generator, transmission line, and load—can lead to optimization problems of intractable size. To manage this complexity, modelers employ reduction techniques, among which **unit aggregation** and **clustering** are paramount. These methods simplify the system representation by grouping similar components or time periods, thereby reducing the number of variables and constraints in the optimization model. This chapter elucidates the fundamental principles governing these techniques, from their formal mathematical underpinnings to the practical consequences of their application. We will explore how aggregation is defined, how it interacts with different types of constraints, and where the simplifications it introduces can lead to modeling errors if not handled with care.

### The Formal Objective of Aggregation

Before delving into specific mechanisms, it is essential to establish the ideal goal of aggregation. At its core, aggregation is a form of **[model reduction](@entry_id:171175)**, where a detailed *original model* is replaced by a simpler *surrogate model*. The ultimate objective is to construct a surrogate that is computationally efficient yet remains a [faithful representation](@entry_id:144577) of the original system.

Let us formalize this objective in the context of a generic Linear Programming (LP) problem, which is a common foundation for many energy system models. The original problem can be stated as:
$$
\min_{x \in \mathbb{R}^{n}} \; c^{\top} x \quad \text{subject to} \quad A x \ge d, \; x \ge 0
$$
Here, $x$ is a high-dimensional vector of decision variables (e.g., the power output of $N$ units over $T$ time periods, so $n=NT$), $c$ is the vector of costs, and the constraints $A x \ge d$ represent physical and operational limits like power balance and capacity.

An aggregation scheme maps the detailed variables $x$ to a lower-dimensional vector of aggregated variables $y \in \mathbb{R}^{k}$ (where $k \lt n$) via a [linear map](@entry_id:201112) $y = M x$. The corresponding surrogate model takes the form:
$$
\min_{y \in \mathbb{R}^{k}} \; c'^{\top} y \quad \text{subject to} \quad B y \ge d, \; y \ge 0
$$
The challenge lies in choosing the aggregated constraint matrix $B$ and cost vector $c'$ such that this surrogate model is "exact."

**Exact aggregation**, in a formal sense, requires the preservation of both feasibility and optimality for any valid input data $(A, d, c)$. This imposes two stringent conditions on the surrogate model's construction :

1.  **Feasibility Preservation:** The feasible set of the surrogate model, $Y(d) = \{ y \in \mathbb{R}^{k}_{+} : B y \ge d \}$, must be the exact image of the original feasible set, $X(d) = \{ x \in \mathbb{R}^{n}_{+} : A x \ge d \}$, under the aggregation map $M$. That is, for all valid demands $d$, it must hold that $Y(d) = M(X(d))$. This ensures a perfect one-to-one correspondence between the sets of feasible solutions in both models.

2.  **Optimality Preservation:** The aggregated cost for a given aggregate decision $y$ must represent the true minimum cost to produce that output. This is defined by the *[value function](@entry_id:144750)* of a disaggregation subproblem: $c'^{\top} y = \inf \{ c^{\top} x : x \in \mathbb{R}^{n}_{+}, \; M x = y \}$. This condition ensures that the cost landscape of the surrogate model accurately reflects the economics of the underlying detailed system.

While achieving perfect exact aggregation is rare in complex, non-linear, and non-convex energy system models, these conditions provide a crucial theoretical benchmark against which we can measure the quality and understand the compromises of practical aggregation methods.

### Fundamental Mechanisms of Aggregation

With the theoretical objective established, we now turn to the mechanisms by which aggregation is performed. A primary source of confusion is the conflation of two distinct processes: the aggregation of physical units and the clustering of operating states or time periods.

#### Distinguishing Unit Aggregation and State Clustering

From a formal perspective, these two techniques operate on different mathematical sets .

**Unit Aggregation** involves grouping physical components. Let $U$ be the set of individual generating units. Unit aggregation is defined by a [surjective function](@entry_id:147405) $f: U \to G$ that maps each unit $i \in U$ to a group identifier $g \in G$, where $|G| \lt |U|$. The set of units belonging to group $g$ is the [preimage](@entry_id:150899) $f^{-1}(g)$. The purpose is to reduce the spatial or technological dimension of the model by treating a group of units as a single entity.

**Operating-State Clustering**, by contrast, involves grouping temporal instances or system states. Let $T$ be the set of time indices in a model horizon. Clustering may be defined by a map $h: T \to K$ that assigns each time index $t \in T$ to a representative "typical period" $k \in K$, where $|K| \lt |T|$. Alternatively, the domain of the map could be a set of observed data vectors (e.g., demand and renewable generation profiles). The goal is to reduce the temporal or scenario dimension of the model by replacing a long time series with a smaller set of weighted, [representative periods](@entry_id:1130881).

This textbook chapter focuses primarily on **unit aggregation**, the process of grouping physical assets.

#### The Principle of Summation for Additive Quantities

The simplest and most fundamental mechanism of unit aggregation relies on the principle of summation. For any physical quantities that are **additive** and whose constraints are **separable** across units, the aggregated parameter is simply the sum of the individual parameters.

Consider a set of $n$ generating units, where each unit $i$ has a commitment decision $y_i \in \{0,1\}$ and a power output $p_i$ constrained by $y_i \underline{p}_i \le p_i \le y_i \overline{p}_i$. The total power output from this set of units is $P = \sum_{i=1}^{n} p_i$. For a fixed set of online units (a fixed commitment vector $y$), the feasible range of operation for each unit $i$ is the interval $[y_i \underline{p}_i, y_i \overline{p}_i]$. The set of all achievable values for the total output $P$ is the **Minkowski sum** of these individual intervals. The Minkowski sum of intervals is itself an interval whose bounds are the sums of the corresponding individual bounds .

The feasible range for the aggregate power $P$ is therefore:
$$
\mathcal{P}_y = \left[ \sum_{i=1}^{n} y_i \underline{p}_i, \sum_{i=1}^{n} y_i \overline{p}_i \right]
$$
This demonstrates the core principle: for separable [linear constraints](@entry_id:636966), the feasible set of the aggregate variable is obtained by summing the bounds of the individual variables.

**Example:** Consider a system with six units, where units 1, 3, 4, and 5 are committed to be online ($y_1=y_3=y_4=y_5=1$) and units 2 and 6 are offline ($y_2=y_6=0$). The individual operating ranges $(\underline{p}_i, \overline{p}_i)$ in MW are: U1:(40, 140), U2:(55, 155), U3:(10, 95), U4:(35, 82), U5:(70, 205), U6:(45, 113).

The minimum aggregate output is the sum of the minimum outputs of the online units:
$P_{\min} = 1 \cdot 40 + 0 \cdot 55 + 1 \cdot 10 + 1 \cdot 35 + 1 \cdot 70 + 0 \cdot 45 = 155 \text{ MW}$.

The maximum aggregate output is the sum of the maximum outputs of the online units:
$P_{\max} = 1 \cdot 140 + 0 \cdot 155 + 1 \cdot 95 + 1 \cdot 82 + 1 \cdot 205 + 0 \cdot 113 = 522 \text{ MW}$.

The total flexible operating range (the Lebesgue length of the feasible interval) for the aggregated system is the sum of the individual operating ranges of the online units: $L = P_{\max} - P_{\min} = (140-40) + (95-10) + (82-35) + (205-70) = 100 + 85 + 47 + 135 = 367 \text{ MW}$ .

#### Hierarchical Aggregation with Linear Algebra

This principle of summation can be elegantly formalized and generalized using linear algebra, especially for hierarchical aggregation structures (e.g., individual units grouped into technology classes, which are then grouped into regional fleets). Such a hierarchy can be represented as a tree structure .

Let $p^U$ be the vector of power outputs for all individual units. We can define a binary **[incidence matrix](@entry_id:263683)** $M^{U \to C}$ where the element $(c, i)$ is 1 if unit $i$ belongs to class $c$, and 0 otherwise. If each unit belongs to exactly one class, each column of this matrix sums to 1. The vector of class-level power outputs, $p^C$, is then a linear [pushforward](@entry_id:158718) of the unit-level outputs:
$$
p^C = M^{U \to C} p^U
$$
This [matrix-vector product](@entry_id:151002) is simply a concise way of writing the summation for each class: $(p^C)_c = \sum_{i} (M^{U \to C})_{c,i} p_i = \sum_{i \in \text{class } c} p_i$. This same [linear operator](@entry_id:136520) applies to any other additive quantity, such as capacity, fuel use, or emissions. This process can be repeated up the hierarchy:
$$
p^F = M^{C \to F} p^C \quad \text{and} \quad p^P = M^{F \to P} p^F
$$
The composition of these mappings, $M^{F \to P} M^{C \to F} M^{U \to C}$, provides a direct [linear transformation](@entry_id:143080) from the most detailed unit level to the highest portfolio level. This formulation is fundamental to systematic accounting in multi-level energy models.

### Aggregation as Relaxation: The Loss of Fidelity

The principle of summing parameters seems straightforward, but it relies on a crucial assumption: that the constraints are truly separable and that summing them does not discard important information. In practice, this is often not the case. Most aggregation schemes are not exact but are instead **relaxations** of the original problem. A relaxation produces a surrogate feasible set that is an *outer approximation* of the true feasible set.

Let $\mathcal{F}$ be the true feasible set of an aggregate variable (e.g., the Minkowski sum). A common aggregation method constructs a surrogate set $\tilde{\mathcal{F}}$ by simply summing the individual parameters in the constraint definitions. As a general rule, this process results in a relaxed feasible set, meaning $\mathcal{F} \subseteq \tilde{\mathcal{F}}$ .

This happens because the interactions between constraints at the individual unit level are lost. Summing parameters is mathematically equivalent to relaxing the problem, as properties like $\sum \min(x_i, y_i) \le \min(\sum x_i, \sum y_i)$ and $\sum \max(x_i, y_i) \ge \max(\sum x_i, \sum y_i)$ show that the sum of minimums is less than the minimum of sums, and the sum of maximums is greater than the maximum of sums.

Optimizing over this enlarged set $\tilde{\mathcal{F}}$ has a critical consequence:
1.  **Overly Optimistic Solutions:** An [optimal solution](@entry_id:171456) found in the relaxed surrogate model may lie in the region $\tilde{\mathcal{F}} \setminus \mathcal{F}$, meaning it is not actually achievable by any valid dispatch of the individual units.
2.  **Lower Bounds on Cost:** When minimizing a cost function, optimizing over a larger feasible set can only result in an objective value that is less than or equal to the true optimum. Therefore, the optimal cost from a relaxed aggregate model provides a **lower bound** on the true system cost. The difference between the true optimal cost and this lower bound is known as the **relaxation gap** .

#### Case Study: Aggregating Ramp Rate Constraints

The aggregation of dynamic constraints like [ramp rates](@entry_id:1130534) provides a clear illustration of this relaxation phenomenon . For a single unit $i$, the ability to ramp up its power output $\Delta p_i = p_i^{t+1} - p_i^t$ is limited by two factors: its intrinsic ramp-up rate $R_i^\uparrow$ and its available "headroom" to its maximum capacity, $\overline{p}_i - p_i^t$. The true maximum ramp-up for a single unit is therefore:
$$
\Delta p_i^{\max} = \min(R_i^\uparrow, \overline{p}_i - p_i^t)
$$
The true maximum aggregate ramp-up for a cluster of units is the sum of these individual maximums, as each unit's ramp is constrained independently:
$$
\Delta P^{\uparrow, \text{max}}_{\text{true}} = \sum_{i=1}^{N} \min(R_i^\uparrow, \overline{p}_i - p_i^t)
$$
A simple aggregate model might define an aggregate ramp rate as $\tilde{R}^\uparrow = \sum_{i=1}^{N} R_i^\uparrow$. This model implicitly assumes that the total system can ramp up by the sum of all individual [ramp rates](@entry_id:1130534). This is a relaxation because it ignores the state-dependent capacity headroom of each unit. If a unit is already operating near its maximum capacity, its contribution to the aggregate ramp-up is small or zero, regardless of its nominal ramp rate. The simple sum $\sum R_i^\uparrow$ overestimates the true ramping capability whenever at least one unit is capacity-limited rather than ramp-limited. This overestimation of flexibility can lead a model to believe the system can respond to a contingency faster than is physically possible.

### Aggregating Non-Convex and Non-Linear Structures

The challenges of aggregation are magnified when dealing with the non-convexities and non-linearities that are characteristic of real-world energy systems.

#### Non-Convexities in Unit Commitment

Thermal generators are subject to complex operational constraints, such as minimum up-times and down-times, which introduce a combinatorial and non-convex nature to the problem. The feasible operating schedule for a single unit is not a single [convex polyhedron](@entry_id:170947) but rather a **union of disjoint [polyhedra](@entry_id:637910)**, where each polyhedron corresponds to a specific valid on/off pattern over the time horizon . This structure is the domain of **disjunctive programming**.

When aggregating $N$ such identical units, the true aggregate feasible set $\mathcal{A}$ is formed by considering every possible combination of valid schedules for each of the $N$ units. For each combination, the resulting aggregate states form a [convex set](@entry_id:268368) (a Minkowski sum of [polyhedra](@entry_id:637910)). The total aggregate feasible set is the **union of all these Minkowski sums**.
$$
\mathcal{A} = \bigcup_{(\sigma^{(1)}, \dots, \sigma^{(N)}) \in \Sigma^N} \left( \bigoplus_{i=1}^{N} \mathcal{P}(\sigma^{(i)}) \right)
$$
This results in a highly complex and non-[convex set](@entry_id:268368). A standard MILP model for the aggregated system operates on a [convex relaxation](@entry_id:168116) of this set (its convex hull). This relaxation can contain points—for example, a fractional number of committed units like $n_t = 3.5$—that do not exist in the true set $\mathcal{A}$. Such points cannot be disaggregated into valid integer schedules for the individual units, giving rise to a significant relaxation gap. This gap reflects the loss of the detailed combinatorial feasibility information during aggregation.

#### Non-Linearities in Cost Functions

Similarly, aggregating units with non-linear cost functions is not a simple matter of summing parameters. Consider units with piecewise-linear production costs, comprising a fixed start-up or no-load cost (an intercept $b_i$) and a variable marginal cost (a slope $a_i$) .

The aggregate cost function $c_{\mathrm{agg}}(P)$ is defined as the minimum total cost to produce a total power level $P$. Constructing this function requires solving an [economic dispatch](@entry_id:143387) subproblem for every level of $P$. This involves two layers of optimization:
1.  **Commitment:** Deciding the optimal subset of units to have online to meet demand $P$. This choice must balance the fixed costs $b_i$ of the committed units against their marginal costs $a_i$.
2.  **Dispatch:** For a given set of active units, allocating the total demand $P$ among them according to **merit order** (i.e., loading the unit with the lowest marginal cost $a_i$ first, up to its capacity, before moving to the next cheapest unit).

The resulting aggregate cost function $c_{\mathrm{agg}}(P)$ is itself a complex, non-convex, piecewise function. Simply creating a single "representative" unit with averaged cost parameters would completely fail to capture this economic structure. This also reinforces a key lesson from hierarchical modeling: for non-linear quantities like fuel consumption (which is directly related to cost), the true aggregate value is the sum of the functions of the individual outputs, $\sum f_i(p_i)$, which is not equal to a representative function of the sum of outputs, $f_{agg}(\sum p_i)$ .

### Practical Implications and Remedies for Aggregation Errors

The loss of fidelity inherent in aggregation is not merely a theoretical concern; it has significant practical consequences. One of the most critical is the failure of spatially blind models to respect local constraints.

#### The Problem of Spatially Blind Aggregation

Consider an environmental constraint, such as a limit on the hourly $NO_x$ emissions from each generator's smokestack. If we aggregate two generators from different airshed zones and replace their individual emission limits ($\alpha_1 P_1 \le L_1$ and $\alpha_2 P_2 \le L_2$) with a single aggregate constraint on total emissions ($\alpha_1 P_1 + \alpha_2 P_2 \le L_1 + L_2$), we fundamentally alter the geometry of the feasible set .

Geometrically, the original pair of constraints defines a rectangular [feasible region](@entry_id:136622) in the $(P_1, P_2)$ plane. The single aggregate constraint defines a triangular region (a simplex). The rectangle is a strict subset of the triangle. An economic dispatch model optimizing over this relaxed triangular set is free to choose a solution on the boundary—for instance, loading one generator heavily while leaving the other idle—that would have been forbidden by the original individual limit. This can lead to a dispatch plan that appears optimal and feasible in the aggregate model but results in a severe violation of local environmental regulations when implemented in the real world.

#### Remedies: Spatially-Aware Aggregation

To mitigate such errors, modelers must incorporate spatial information back into their aggregated models. Two common remedies are:

1.  **Zonal Constraints:** Instead of aggregating all units into a single system-wide cluster, one can perform a more granular aggregation based on location (e.g., airshed, grid zone). By maintaining separate constraints for each zone—for instance, enforcing a total $NO_x$ cap for all units within Zone A and a separate cap for Zone B—the model can prevent the "swapping" of emissions between sensitive regions. This is a direct application of the hierarchical aggregation framework using incidence matrices to [map units](@entry_id:186728) to zones .

2.  **Location-Specific Penalty Functions:** As a complementary approach, one can add penalty terms to the model's objective function. For instance, one could add a cost proportional to the emissions in each zone, e.g., $\sum_{z} \pi_z e_z$, where $e_z$ are the total emissions in zone $z$ and $\pi_z$ is a location-specific penalty price. This creates an economic incentive to reduce emissions, especially in more sensitive zones assigned a higher penalty $\pi_z$. While this "soft" constraint does not offer the absolute guarantee of a hard constraint, it is a powerful tool for guiding the optimization towards more environmentally benign outcomes, especially when used in conjunction with zonal caps .

In conclusion, unit aggregation and clustering are indispensable tools for managing the complexity of modern energy system models. However, they are not a "free lunch." Every act of aggregation involves a trade-off between model simplicity and fidelity. A thorough understanding of the underlying principles—of summation and Minkowski sums, of relaxation and convex hulls, and of the behavior of non-convex and non-[linear constraints](@entry_id:636966)—is essential for any serious modeler. By recognizing aggregation as a form of relaxation and being mindful of the information it discards, practitioners can build models that are not only computationally tractable but also robust and reliable guides for real-world decision-making.