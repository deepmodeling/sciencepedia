## Introduction
The reliable and economic operation of modern power grids hinges on a complex optimization problem known as Unit Commitment (UC). At its core, UC determines which power plants to run, and at what level, to meet electricity demand at every moment. While the concept is straightforward, the underlying mathematical formulation is intricate, blending discrete on/off decisions with continuous power levels, physical limitations, and economic objectives. This article demystifies the UC problem by breaking down its formulation from first principles, addressing the gap between high-level understanding and practical modeling expertise.

Over the next three chapters, you will embark on a structured journey through the world of unit commitment. The first chapter, **Principles and Mechanisms**, lays the groundwork by constructing a canonical Mixed-Integer Linear Program (MILP) from scratch, defining its variables, objective function, and critical constraints. The second chapter, **Applications and Interdisciplinary Connections**, expands on this foundation to show how the model is adapted to handle real-world complexities like network constraints, energy storage, and uncertainty from renewable sources. Finally, the **Hands-On Practices** chapter provides targeted exercises to reinforce your understanding of the core concepts. This comprehensive exploration will equip you with the knowledge to formulate, interpret, and extend UC models for advanced energy [system analysis](@entry_id:263805).

## Principles and Mechanisms

The Unit Commitment (UC) problem addresses the challenge of scheduling power generation units to meet system-wide electricity demand at the minimum possible cost, while respecting a complex set of physical and operational constraints. Unlike the simpler **Economic Dispatch** (ED) problem, which assumes the on/off status of generators is predetermined and only optimizes their continuous power output, Unit Commitment must decide which units to turn on or off in each time period. This introduction of discrete on/off decisions, coupled with time-linking constraints, transforms the problem into a large-scale, non-convex, Mixed-Integer Linear Program (MILP), which is the focus of this chapter. 

This chapter deconstructs the canonical thermal [unit commitment formulation](@entry_id:1133607), examining its core components—decision variables, objective function, and constraints—from first principles. We will build the model piece by piece, clarifying the physical or economic rationale behind each mathematical statement.

### The Building Blocks: Decision Variables

To construct a mathematical model of the UC problem, we first need to define a set of variables that capture the decisions to be made. For a system with $N$ generating units, indexed by $i \in \{1, \dots, N\}$, over a planning horizon of $T$ discrete time periods, indexed by $t \in \{1, \dots, T\}$, the primary decisions are:

1.  **Commitment Status ($u_{i,t}$):** A binary variable representing the on/off state of unit $i$ in period $t$.
    $$ u_{i,t} = \begin{cases} 1,  \text{if unit } i \text{ is online in period } t \\ 0,  \text{if unit } i \text{ is offline in period } t \end{cases} $$

2.  **Power Generation ($p_{i,t}$):** A continuous, non-negative variable representing the amount of electrical power produced by unit $i$ in period $t$.

To model the costs and physical limitations associated with state transitions, we introduce two auxiliary [binary variables](@entry_id:162761):

3.  **Startup Indicator ($y_{i,t}$):** A binary variable indicating that unit $i$ transitions from offline to online at the beginning of period $t$.
    $$ y_{i,t} = \begin{cases} 1,  \text{if unit } i \text{ starts up at period } t \\ 0,  \text{otherwise} \end{cases} $$

4.  **Shutdown Indicator ($z_{i,t}$):** A binary variable indicating that unit $i$ transitions from online to offline at the beginning of period $t$.
    $$ z_{i,t} = \begin{cases} 1,  \text{if unit } i \text{ shuts down at period } t \\ 0,  \text{otherwise} \end{cases} $$

The presence of both [binary variables](@entry_id:162761) ($u_{i,t}, y_{i,t}, z_{i,t}$) and continuous variables ($p_{i,t}$) is what makes the UC problem a "mixed-integer" program. 

### The Objective Function: Quantifying Operating Costs

The goal of the UC problem is typically to minimize the total operating cost over the entire planning horizon. This cost is composed of several distinct components that are directly tied to the decision variables we have just defined. 

*   **Variable Production Cost:** This is the cost of the fuel consumed to produce electricity. While the true fuel cost curve is often a non-linear (convex quadratic) function of power output, for the purposes of a linear program it is typically approximated by a [piecewise linear function](@entry_id:634251). In its simplest [linear form](@entry_id:751308), it is the product of a constant variable cost rate, $\beta_i$ (in $/MWh$), and the energy produced, $p_{i,t} \Delta t$, where $\Delta t$ is the duration of the time period.

*   **No-Load Cost:** This is a fixed cost incurred for every period a thermal unit is online ($u_{i,t}=1$), regardless of its power output. It represents the fuel required to maintain operating temperature and pressure and other fixed operational expenses. It is calculated as the product of a no-load cost rate, $\alpha_i$ (in $/h$), and the commitment status, $u_{i,t}$, multiplied by the period duration $\Delta t$.

*   **Startup and Shutdown Costs:** These are costs associated with the state transitions. **Startup cost** ($s_i$) can be substantial, accounting for the fuel, labor, and material stress required to bring a unit online. **Shutdown cost** ($c_i$) is typically smaller. These costs are incurred only when a startup or shutdown event occurs, as indicated by $y_{i,t}=1$ or $z_{i,t}=1$, respectively.

Combining these components, the total operating cost to be minimized over all units and all time periods is:
$$ \min \sum_{t=1}^T \sum_{i=1}^N \left( \beta_i p_{i,t} \Delta t + \alpha_i u_{i,t} \Delta t + s_i y_{i,t} + c_i z_{i,t} \right) $$
This objective function is linear in all decision variables, a critical requirement for an MILP formulation.

### Constraints: Enforcing Physical and System-Level Rules

The core of the UC formulation lies in its constraints, which ensure that the resulting schedule is physically feasible and reliably serves the electrical load. These can be divided into system-level constraints and unit-level constraints.

#### System-Level Constraints

The most fundamental system-level constraint is the **power balance equation**, which enforces the principle of energy conservation: at every moment, the total power generated must equal the total power consumed. In a simplified "copper plate" model (which assumes no network congestion), this is a single equation for each time period $t$.

Let $D_t$ be the forecasted demand in period $t$. The simplest form of the power balance constraint is:
$$ \sum_{i=1}^N p_{i,t} = D_t \quad \forall t $$
This states that the sum of power produced by all generators must exactly meet the demand in that period.

In more sophisticated models, this equation is augmented to account for other factors.  For instance, if we consider aggregate transmission losses $\ell_t$ (power that is generated but dissipated as heat in the network) and demand response $r_t$ (a reduction from the baseline demand $D_t^{\text{base}}$), the equation becomes:
$$ \sum_{i=1}^N p_{i,t} = (D_t^{\text{base}} - r_t) + \ell_t \quad \forall t $$
Here, total generation must cover both the realized end-user demand and the power lost in transmission.

#### Unit-Level Constraints

These constraints model the physical limitations of individual generating units.

**Logical Constraints on State Transitions**

The commitment status variable ($u_{i,t}$) and the transition variables ($y_{i,t}, z_{i,t}$) are not independent. Their logical relationship must be enforced mathematically. The change in commitment status between two consecutive periods, $u_{i,t} - u_{i,t-1}$, can only be $-1$ (a shutdown), $0$ (no change), or $1$ (a startup). This is precisely captured by the difference between the startup and shutdown indicators. This gives rise to a foundational linking constraint:
$$ u_{i,t} - u_{i,t-1} = y_{i,t} - z_{i,t} \quad \forall i, t $$
Additionally, a unit cannot simultaneously start up and shut down in the same period, which is enforced by:
$$ y_{i,t} + z_{i,t} \le 1 \quad \forall i, t $$
Together, these two [linear constraints](@entry_id:636966) are sufficient to perfectly model the four possible state transitions: staying off, starting up, shutting down, and staying on. 

**Generation Limits**

A thermal unit cannot produce power when it is offline. When online, its output must lie within a stable operating range defined by a minimum stable generation level, $P_i^{\min}$, and a maximum capacity, $P_i^{\max}$. This conditional logic is elegantly captured by the following pair of linear inequalities:
$$ P_i^{\min} u_{i,t} \le p_{i,t} $$
$$ p_{i,t} \le P_i^{\max} u_{i,t} $$
If $u_{i,t}=0$, these constraints combine to force $p_{i,t}=0$. If $u_{i,t}=1$, they enforce $P_i^{\min} \le p_{i,t} \le P_i^{\max}$. These constraints are fundamental as they link the binary commitment variable to the continuous power output variable. The presence of a non-zero $P_i^{\min}$ is a primary source of the problem's non-convexity. 

**Inter-temporal Constraints: Coupling Decisions Across Time**

The most complex constraints are those that link decisions across different time periods, reflecting the slow dynamics of large thermal units.

*   **Ramping Limits:** A generator's power output cannot change instantaneously. Its rate of change is limited by **ramp-up ($RU_i$)** and **ramp-down ($RD_i$)** rates. When a unit is online in two consecutive periods, this is straightforward: $p_{i,t} - p_{i,t-1} \le RU_i$. However, the formulation must also correctly handle startups and shutdowns. A more comprehensive formulation accounts for special start-up ($SU_i$) and shut-down ($SD_i$) ramp capabilities. A standard tight formulation for these limits is:
    $$ p_{i,t} - p_{i,t-1} \le RU_i u_{i,t-1} + SU_i y_{i,t} $$
    $$ p_{i,t-1} - p_{i,t} \le RD_i u_{i,t} + SD_i z_{i,t} $$
    In the ramp-up constraint, for example, if the unit was already on ($u_{i,t-1}=1, y_{i,t}=0$), the limit is $RU_i$. If the unit is starting up ($u_{i,t-1}=0, y_{i,t}=1$), the limit becomes $SU_i$, which is typically the maximum power the unit can reach in its first hour. The formulation correctly deactivates the constraint when the unit is off. 

*   **Minimum Up and Down Times:** To avoid excessive [thermal stress](@entry_id:143149) from rapid heating and cooling cycles, operational policies dictate that once a unit is turned on, it must remain on for a **minimum up time ($T_i^{\text{up}}$)**, and once shut down, it must remain off for a **minimum down time ($T_i^{\text{down}}$)**.  This is enforced by "window" constraints. If a unit starts up at time $t$ ($y_{i,t}=1$), it must remain on for the next $T_i^{\text{up}}$ periods. This is modeled by:
    $$ \sum_{\tau=t}^{t+T_i^{\text{up}}-1} u_{i,\tau} \ge T_i^{\text{up}} y_{i,t} $$
    Since each $u_{i,\tau}$ cannot exceed 1, this sum can only be greater than or equal to $T_i^{\text{up}}$ if every $u_{i,\tau}$ in the window is equal to 1. A similar logic applies for the minimum down time:
    $$ \sum_{\tau=t}^{t+T_i^{\text{down}}-1} (1-u_{i,\tau}) \ge T_i^{\text{down}} z_{i,t} $$

### Advanced Formulation Techniques and Best Practices

Formulating a correct MILP is only the first step; formulating a *good* MILP that can be solved efficiently is a more advanced skill. This involves creating a "tight" formulation, meaning its linear programming (LP) relaxation—where binary variables are allowed to take fractional values between 0 and 1—provides a close approximation of the true integer problem.

#### The Role and Perils of Big-M Constraints

Many logical implications in UC are modeled using the "Big-M" technique. This involves adding a large constant, $M$, to a constraint to effectively disable it under certain logical conditions. For example, the ramp-up constraint can be written in a Big-M style:
$$ p_t - p_{t-1} \le R_{\text{up}} + M^{\text{up}} (2 - u_{t-1} - u_t) $$
When the unit is on in both periods, $u_{t-1}=u_t=1$, the term with $M^{\text{up}}$ becomes zero, and the ramp limit is active. In any other case (startup, shutdown, stay off), the term $(2 - u_{t-1} - u_t)$ is at least 1, and if $M^{\text{up}}$ is large enough, the constraint becomes non-binding.

The key challenge is choosing a value for $M$ that is "just big enough." An overly large $M$ weakens the LP relaxation, allowing unrealistic fractional solutions that slow down the solver. It can also cause numerical instability due to the large difference in coefficient magnitudes. The tightest valid $M$ is the smallest value that guarantees the constraint is non-restrictive in all "off" states. For the ramp-up constraint above, the tightest $M^{\text{up}}$ is found by calculating the maximum possible value of $p_t - p_{t-1} - R_{\text{up}}$ during a startup, which is $P_{\max} - R_{\text{up}}$. Using values derived from the physical parameters of the unit is always superior to using arbitrary large numbers. 

#### Strengthening Formulations with Valid Inequalities

The quality of a UC formulation can be significantly improved by adding **[valid inequalities](@entry_id:636383)**. These are constraints that are redundant for the integer problem but cut off fractional solutions in the LP relaxation, thereby "tightening" it.

For instance, the basic generation limit $p_{i,t} \le P_i^{\max} u_{i,t}$ can be strengthened. If we know the unit's maximum output during its startup hour is $\overline{S}_i  P_i^{\max}$, we can add the following [valid inequality](@entry_id:170492):
$$ p_{i,t} \le P_i^{\max} u_{i,t} - (P_i^{\max} - \overline{S}_i) y_{i,t} $$
If $y_{i,t}=1$, this constraint tightens the upper bound on power to $p_{i,t} \le \overline{S}_i$, providing a more accurate representation of the unit's capability in the LP relaxation. 

The ultimate goal of this process is to make the [feasible region](@entry_id:136622) of the LP relaxation as close as possible to the **convex hull** of the true integer feasible set. A convex-hull formulation is ideal because its LP relaxation has no fractional [extreme points](@entry_id:273616) corresponding to that substructure, completely closing the "[integrality gap](@entry_id:635752)" for that part of the problem. While deriving the full [convex hull](@entry_id:262864) for the entire UC problem is intractable, modern research has produced very tight, near-convex-hull formulations for specific substructures like the minimum up/down time constraints, which are critical for building effective, solvable UC models. 