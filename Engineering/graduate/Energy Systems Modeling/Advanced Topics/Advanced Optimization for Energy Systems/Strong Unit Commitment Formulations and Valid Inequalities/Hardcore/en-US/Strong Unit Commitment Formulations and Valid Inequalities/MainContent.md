## Introduction
The Unit Commitment (UC) problem, which determines the optimal on/off schedule for power generators, is a fundamental and computationally intensive task in energy system operations. As systems grow in complexity, the need for efficient and accurate solutions becomes paramount. A common bottleneck in solving the Mixed-Integer Linear Programs (MILPs) that represent UC is the use of "weak" mathematical formulations, whose continuous relaxations provide poor guidance to optimizers, resulting in long computation times and suboptimal results. This article bridges the gap between basic modeling and high-performance optimization by focusing on the theory and practice of "strong" formulations and [valid inequalities](@entry_id:636383).

In the following sections, you will gain a comprehensive understanding of how to build computationally superior UC models. In **Principles and Mechanisms**, we will explore the mathematical foundations of strength, from the [convex hull](@entry_id:262864) of a single generator's operating region to the powerful inequalities that govern [inter-temporal constraints](@entry_id:1126569) like minimum up/down times and ramp rates. Next, **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied to enhance physical realism, model system-level interactions like network constraints, and enable advanced algorithmic approaches. Finally, **Hands-On Practices** will provide opportunities to apply and reinforce these concepts. By mastering these techniques, you will be equipped to build faster, more robust, and more realistic models for modern energy systems.

## Principles and Mechanisms

The efficacy of a Unit Commitment (UC) model, particularly when formulated as a Mixed-Integer Linear Program (MILP), is profoundly dependent on the mathematical "strength" of its formulation. A **strong formulation** is one whose continuous relaxation—where binary variables are allowed to take fractional values between 0 and 1—provides a feasible region that closely approximates the convex hull of the true, discrete feasible solutions. Tighter relaxations lead to more accurate bounds within the [branch-and-bound](@entry_id:635868) solution process, drastically reducing computation time and improving the quality of solutions for large, complex energy systems. This section elucidates the core principles and mechanisms behind constructing such strong formulations, progressing from fundamental single-period relationships to complex inter-temporal dynamics and advanced mathematical techniques.

### Fundamental Constraints and Their Convex Hulls

The cornerstone of any UC formulation is the set of constraints that model the physical and economic characteristics of a single generating unit within a single time period. The strength of the entire model begins with how accurately and tightly these fundamental relationships are represented.

#### The Production-Commitment Link

The most basic relationship in a UC model is that a generator can produce power if and only if it is committed to be online. Let $u_t \in \{0, 1\}$ be the binary commitment variable for a unit at time period $t$, where $u_t=1$ signifies the unit is on and $u_t=0$ signifies it is off. Let $p_t$ be the continuous variable representing the power output in that period. When online, the unit's output is constrained between a minimum stable generation level, $P^{\min}$, and a maximum capacity, $P^{\max}$. When offline, its output is zero. This physical reality defines a non-convex, disjunctive feasible set for the pair of variables $(u_t, p_t)$:

$$ S = \{(0, 0)\} \cup \{(1, p) \mid P^{\min} \le p \le P^{\max}\} $$

A naive or weak formulation might attempt to model this with separate constraints, but a strong formulation seeks a set of linear inequalities that describe the **[convex hull](@entry_id:262864)** of $S$. The convex hull, denoted $\operatorname{conv}(S)$, is the smallest [convex set](@entry_id:268368) containing all points in $S$. For this disjunction, the [convex hull](@entry_id:262864) is a triangle in the $(u_t, p_t)$ plane defined by the vertices $(0, 0)$, $(1, P^{\min})$, and $(1, P^{\max})$.

The linear inequalities that define this triangle for $u_t \in [0, 1]$ are derived from its bounding edges:

$$ P^{\min} u_t \le p_t $$
$$ p_t \le P^{\max} u_t $$

These two inequalities constitute the ideal [linear representation](@entry_id:139970) of the production-commitment link . When $u_t$ is forced to be binary, they correctly enforce the original disjunction. If $u_t=0$, both inequalities combine to force $p_t=0$. If $u_t=1$, they correctly enforce $P^{\min} \le p_t \le P^{\max}$. Their power lies in the continuous relaxation. In a simplified scenario where a unit must meet a load $L_t$ (so $p_t = L_t$) and the objective function penalizes commitment (a cost on $u_t$), an optimizer will choose the smallest possible $u_t$. The constraint $p_t \le P^{\max} u_t$ implies $u_t \ge p_t / P^{\max}$. The optimizer will thus set $u_t = L_t / P^{\max}$ . If the load $L_t$ is between $0$ and $P^{\max}$, the optimal relaxed value of $u_t$ will be fractional, and the inequality $p_t = P^{\max} u_t$ will be tight. This provides the solver with a highly accurate local relationship between cost and output, which is crucial for making effective branching decisions.

### Modeling Inter-temporal Dynamics

While single-period constraints form the foundation, the essence of the UC problem lies in its inter-temporal nature. Decisions made in one period have direct consequences for subsequent periods. Modeling these dynamics strongly is critical.

#### Capturing Transitions: Startup and Shutdown Variables

To model transition costs, minimum up/down times, and [ramping limits](@entry_id:1130533), we must explicitly represent the events of a unit starting up or shutting down. We introduce two additional binary variables:
- $v_t \in \{0, 1\}$: The **startup indicator**, where $v_t=1$ if the unit transitions from off at $t-1$ to on at $t$.
- $w_t \in \{0, 1\}$: The **shutdown indicator**, where $w_t=1$ if the unit transitions from on at $t-1$ to off at $t$.

These events are logically tied to the commitment status $u_t$. An analysis of the four possible state transitions ($u_{t-1} \to u_t$) reveals a direct relationship: the change in state, $u_t - u_{t-1}$, is $1$ for a startup, $-1$ for a shutdown, and $0$ otherwise. This perfectly matches the value of $v_t - w_t$. This gives rise to the elegant and fundamental state transition equation:

$$ u_t - u_{t-1} = v_t - w_t $$

This equation must hold for all periods $t \in \{1, \dots, T\}$, with $u_0$ representing the unit's known initial state. However, this single equation is insufficient for a strong formulation . When the state does not change ($u_t - u_{t-1} = 0$), the equation becomes $v_t = w_t$. For binary variables, this permits two solutions: $(v_t, w_t) = (0, 0)$, which is correct, and $(v_t, w_t) = (1, 1)$, which is physically meaningless as a unit cannot simultaneously start and shut down.

To forbid this unphysical state, we must add a **[valid inequality](@entry_id:170492)** that is redundant for the true integer solutions but cuts off fractional solutions that violate the logic. The [mutual exclusivity](@entry_id:893613) of startup and shutdown events is captured by the inequality:

$$ v_t + w_t \le 1 $$

This constraint is valid because the preconditions for $v_t=1$ (requiring $u_{t-1}=0$) and $w_t=1$ (requiring $u_{t-1}=1$) are contradictory . Together, the equality $u_t - u_{t-1} = v_t - w_t$ and the inequality $v_t + w_t \le 1$ form a strong and complete description of the logical relationship between commitment, startup, and shutdown variables. While other formulations exist, such as those using multiple inequalities (e.g., $v_t \ge u_t - u_{t-1}$ and $w_t \ge u_{t-1} - u_t$), this two-constraint set is generally preferred for its tightness and clarity.

### Temporal Constraints and Their Strong Formulations

The most significant [inter-temporal constraints](@entry_id:1126569) in UC are minimum up/down times and ramp rates. Their formulations are canonical examples of strong [valid inequalities](@entry_id:636383).

#### Minimum Up and Down Times

Generating units cannot be cycled on and off arbitrarily. After starting up, a thermal unit must typically run for a minimum number of consecutive periods, its **minimum up time ($T^{\mathrm{up}}$)**, to ensure [thermal stability](@entry_id:157474). Similarly, after shutting down, it must remain off for a **minimum down time ($T^{\mathrm{down}}$)**.

A strong way to model the minimum up time requirement is to link a startup event directly to the commitment status of future periods. If a unit starts up at period $t$ ($v_t=1$), it must be on for the $T^{\mathrm{up}}$ periods from $t$ to $t+T^{\mathrm{up}}-1$. In a linear formulation, this is expressed as: If $v_t=1$, then $\sum_{\tau=t}^{t+T^{\mathrm{up}}-1} u_{\tau} = T^{\mathrm{up}}$. If $v_t=0$, no such constraint is imposed. Both cases are captured by the single, powerful inequality:

$$ \sum_{\tau=t}^{t+T^{\mathrm{up}}-1} u_{\tau} \ge T^{\mathrm{up}} v_t $$

This constraint must be formulated for all periods $t$ where the full window of $T^{\mathrm{up}}$ periods falls within the planning horizon, i.e., for $t \in \{1, \dots, T - T^{\mathrm{up}} + 1\}$ . For startup events near the end of the horizon, this inequality must be adjusted.

The minimum down time constraint is modeled symmetrically. A shutdown at period $t$ ($w_t=1$) requires the unit to be off ($u_\tau=0$, or equivalently $1-u_\tau=1$) for the $T^{\mathrm{down}}$ periods from $t$ to $t+T^{\mathrm{down}}-1$. This leads to the symmetric [valid inequality](@entry_id:170492):

$$ \sum_{\tau=t}^{t+T^{\mathrm{down}}-1} (1-u_{\tau}) \ge T^{\mathrm{down}} w_t $$

This inequality is applied for all $t \in \{1, \dots, T - T^{\mathrm{down}} + 1\}$ . These "window-sum" inequalities are exceptionally strong because they directly link a single event variable ($v_t$ or $w_t$) to a set of [state variables](@entry_id:138790) ($u_\tau$), providing the solver with significant logical leverage.

#### Ramp Rate Constraints

The power output of a generator cannot change instantaneously. The rate of change is limited by physical and mechanical constraints. These **ramp rates** are typically different for increasing output (**ramp-up rate, $R^{\mathrm{up}}$**) and decreasing output (**ramp-down rate, $R^{\mathrm{down}}$**). Furthermore, the allowable change in output during a startup or shutdown event is often different from the normal online [ramping limits](@entry_id:1130533), defined by a **startup ramp limit ($SU$)** and a **shutdown ramp limit ($SD$)**.

A strong formulation for these constraints must correctly distinguish between the different transition scenarios. Consider the ramp-up constraint on the change $p_t - p_{t-1}$.
1.  **Online-to-Online**: If the unit is on at both $t-1$ and $t$ ($u_{t-1}=1, u_t=1$), then $p_t - p_{t-1} \le R^{\mathrm{up}}$.
2.  **Off-to-On (Startup)**: If the unit starts up at $t$ ($v_t=1$), then $p_{t-1}=0$, and the limit is $p_t \le SU$.
3.  **Other cases**: In shutdown or off-off cases, the change $p_t - p_{t-1}$ is either negative or zero, so the ramp-up constraint is naturally satisfied.

A single inequality that captures these cases strongly is:

$$ p_t - p_{t-1} \le R^{\mathrm{up}} u_{t-1} + SU v_t $$

Here, the term $R^{\mathrm{up}} u_{t-1}$ activates the normal ramp limit only if the unit was on in the previous period. The term $SU v_t$ activates the startup limit only during a startup event.

Symmetrically, for the ramp-down constraint on the change $p_{t-1} - p_t$:
1.  **Online-to-Online**: $p_{t-1} - p_t \le R^{\mathrm{down}}$.
2.  **On-to-Off (Shutdown)**: $p_t=0$, and the limit is $p_{t-1} \le SD$.
3.  **Other cases**: The ramp-down limit is not restrictive.

The corresponding strong inequality is:

$$ p_{t-1} - p_t \le R^{\mathrm{down}} u_t + SD w_t $$

Here, $R^{\mathrm{down}} u_t$ activates the normal ramp-down limit only if the unit will be on in the current period, and $SD w_t$ activates the shutdown limit during a shutdown event. This pair of inequalities provides a tight and correct representation of ramping physics .

### Advanced Strengthening Techniques

Beyond modeling specific physical constraints, several general mathematical techniques can be applied to derive powerful [valid inequalities](@entry_id:636383), further strengthening the MILP formulation.

#### Knapsack-like Constraints and MIR Cuts

Many constraints in UC models take the form of a **knapsack constraint**, where a sum of variables is bounded by a capacity that can be "switched on" by a binary variable. A common example arises when a unit must co-optimize its provision of energy ($p_t$) and [ancillary services](@entry_id:1121004) like spinning reserves ($s_t$). If the total output is limited by capacity $\overline{P}$ ($p_t + s_t \le \overline{P} u_t$) and the unit has minimum obligations $D$ for energy and $S$ for reserves ($p_t \ge D, s_t \ge S$), we can derive a powerful cut.

From the obligations, we know that any [feasible solution](@entry_id:634783) must satisfy $p_t + s_t \ge D+S$. Combining this with the capacity limit gives $D+S \le \overline{P} u_t$, or $u_t \ge (D+S)/\overline{P}$. Since we know $u_t$ must be an integer, we can strengthen this continuous bound by applying a [ceiling function](@entry_id:262460). This is a simple application of the principle behind **Mixed-Integer Rounding (MIR)** cuts:

$$ u_t \ge \left\lceil \frac{D+S}{\overline{P}} \right\rceil $$

For an instance where $(D+S)/\overline{P}$ is fractional, say $0.86$, the LP relaxation allows $u_t=0.86$. However, this MIR inequality forces $u_t \ge \lceil 0.86 \rceil = 1$, thus cutting off the fractional solution and pushing the relaxed solution closer to the true integer optimum .

#### Convex Cost Functions and Perspective Reformulation

The production cost of a generator is typically a non-linear, [convex function](@entry_id:143191) of its output. For MILP, this is often approximated by a convex, [piecewise linear function](@entry_id:634251) $C(p_t)$. A standard but weak method to model this is using "big-M" constraints. A far superior approach is the **perspective reformulation**.

For a [convex function](@entry_id:143191) $C(x)$, its perspective is the function $u \cdot C(x/u)$. The epigraph of the perspective function is convex, and if $C(p_t)$ is piecewise linear, defined as the maximum of several affine functions $C(p_t) = \max_k \{\alpha_k + d_k p_t\}$, its perspective epigraph can be represented by a set of linear inequalities. If $c_t$ is the cost variable, the formulation is:

$$ c_t \ge \alpha_k u_t + d_k p_t \quad \text{for each piece } k $$

This formulation is significantly stronger than big-M methods. To see why, consider a fractional commitment $u_t=0.5$. The perspective cut provides a lower bound on cost $c_t$ that is scaled appropriately. For instance, in a numerical example with a cost function defined by multiple segments, the bound from the perspective formulation can be substantially higher (e.g., $1500$) than the bound one would get by simply evaluating the original cost function at the given power level (e.g., $1000$). This tighter bound on cost for fractional commitment states is invaluable to the MILP solver .

#### A Glimpse into Complete Polyhedral Descriptions

The techniques discussed so far add [valid inequalities](@entry_id:636383) to tighten the formulation for specific substructures of the problem. A more ambitious goal in polyhedral theory is to find a complete description of the [convex hull](@entry_id:262864) of all feasible integer solutions. For the specific combinatorial problem of a single unit's on/off sequence subject to minimum up and down times, such descriptions are known.

It has been shown that the [convex hull](@entry_id:262864) of feasible sequences $(u, v, w)$ is given by the basic transition equations and variable bounds, augmented by a set of "window-sum" inequalities that are different from, but related to, those used to enforce the constraints themselves. These inequalities take the form:

$$ \sum_{k=\max(1,\,t-T^{\mathrm{up}}+1)}^{t} v_k \le u_t $$
$$ \sum_{k=\max(1,\,t-T^{\mathrm{down}}+1)}^{t} w_k \le 1 - u_t $$

These inequalities provide a global perspective, ensuring that the state $u_t$ at any time $t$ is consistent with the history of startups and shutdowns in the relevant preceding windows . While more complex to implement, such formulations represent the frontier of strong modeling, offering the tightest possible continuous relaxations and paving the way for solving ever larger and more complex unit commitment problems.