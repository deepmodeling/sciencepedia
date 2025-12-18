## Introduction
The unit commitment (UC) problem is a cornerstone of reliable and economic power system operation, tasked with determining which power plants to turn on, when to turn them on, and how much electricity each should produce to meet demand at the lowest cost. Given the immense scale and complexity of modern grids, this challenge is addressed using powerful [mathematical optimization](@entry_id:165540) techniques, chief among them being Mixed-Integer Linear Programming (MILP). The MILP framework provides a structured way to translate the non-convex, discrete decisions of power plant operation and the continuous physics of power flow into a solvable model. However, creating an effective formulation is an art, requiring a deep understanding of both the physical system and the mathematical tools.

This article systematically deconstructs the MILP formulation for unit commitment, bridging the gap between foundational theory and advanced, real-world application. It aims to equip readers with the knowledge to build, interpret, and extend UC models. We will navigate from the basic building blocks of the problem to the sophisticated extensions needed to manage today's complex energy landscape.

You will first learn the core **Principles and Mechanisms**, where we will construct the fundamental MILP model from the ground up, defining the decision variables, cost components, and crucial temporal constraints like ramping and minimum up/down times. Next, in **Applications and Interdisciplinary Connections**, we will explore how this basic framework is augmented to model complex technologies like [combined-cycle](@entry_id:185995) plants and energy storage, integrate network constraints for grid security, and manage uncertainty from renewable energy sources. Finally, **Hands-On Practices** will provide opportunities to apply these concepts, guiding you through the practical implementation of key aspects of the UC problem.

## Principles and Mechanisms

The formulation of the unit commitment (UC) problem as a Mixed-Integer Linear Program (MILP) is a cornerstone of modern power system operations. This approach translates the complex physical and economic characteristics of [power generation](@entry_id:146388) into a structured mathematical model that can be solved to find a cost-optimal, physically feasible generation schedule. This chapter deconstructs the UC-MILP, systematically building it from its fundamental variables and constraints to its more sophisticated components. We will explore not only *what* these components are but also *why* they are formulated in specific ways, emphasizing the principles that ensure the model is both computationally tractable and a [faithful representation](@entry_id:144577) of reality.

### Core Variables: The Discreteness of Commitment

At the heart of the unit commitment problem lies a fundamental duality: the continuous nature of power generation versus the discrete nature of a generator's operational status. To capture this, we introduce two primary types of decision variables for each generating unit $i$ over a series of discrete time periods $t$:

1.  A continuous variable, $p_{i,t} \ge 0$, representing the amount of electrical power the unit generates.
2.  A binary variable, $u_{i,t} \in \{0, 1\}$, representing the unit's commitment status. If $u_{i,t} = 1$, the unit is "on" (synchronized to the grid and available to produce power). If $u_{i,t} = 0$, the unit is "off".

The necessity of the binary variable $u_{i,t}$ stems directly from the physical constraints of thermal power plants. A unit cannot operate at any arbitrary power level between zero and its maximum capacity. It has a **minimum stable generation level**, denoted as $P_i^{\min} > 0$. Therefore, for any given period, the unit has only two physically admissible states: it is off and producing zero power, or it is on and producing power $p_{i,t}$ in the range $[P_i^{\min}, P_i^{\max}]$.

This creates a non-convex feasible region for the pair of variables $(u_{i,t}, p_{i,t})$, which consists of the single point $(0,0)$ and the continuous line segment $\{(1, p) \mid P_i^{\min} \le p \le P_i^{\max}\}$. A purely linear program cannot model such a disjoint, non-[convex set](@entry_id:268368). If we were to relax the commitment variable to be continuous, $u_{i,t} \in [0, 1]$, the model could produce physically meaningless solutions. For instance, to meet a small demand of $20$ MW with a unit whose [minimum stable output](@entry_id:1127943) is $P_i^{\min} = 50$ MW, the relaxed model might select a fractional commitment like $u_{i,t}=0.4$ to produce $p_{i,t}=20$ MW. This "partially committed" state has no physical counterpart and leads to a gross miscalculation of operational costs, particularly startup costs .

The integrality of $u_{i,t}$ is thus essential. We bridge the discrete status and continuous output using a pair of linear "linking" constraints:

$$
P_i^{\min} u_{i,t} \le p_{i,t} \le P_i^{\max} u_{i,t}
$$

If $u_{i,t} = 1$, these constraints correctly enforce $P_i^{\min} \le p_{i,t} \le P_i^{\max}$. If $u_{i,t} = 0$, they collapse to $0 \le p_{i,t} \le 0$, forcing the output to be zero as required. These constraints are a classic example of a **big-M formulation**, where the parameter $P_i^{\max}$ serves as the coefficient "M". In a single-period context, this formulation is ideal, meaning its [linear programming relaxation](@entry_id:261834) perfectly describes the convex hull of the actual non-convex feasible set .

### The Objective Function: Modeling Operational Costs

The primary goal of unit commitment is to meet electricity demand at the minimum possible operational cost. The objective function aggregates all relevant costs over the scheduling horizon and across all units. A comprehensive formulation includes three main types of costs .

$$
\min \sum_{t=1}^T \sum_{i=1}^N \left( C_i^{\text{prod}}(p_{i,t}) + C_i^{\text{NL}} u_{i,t} + C_i^{\text{SU}} y_{i,t} + C_i^{\text{SD}} z_{i,t} \right)
$$

**Variable Production Cost**: The term $C_i^{\text{prod}}(p_{i,t})$ represents the cost of fuel consumed to generate power $p_{i,t}$. This cost is typically a convex (often quadratic) function of output. For a linear model, it is approximated by a piecewise-linear function. The simplest approximation is a single linear function, adding a term like $c_i p_{i,t}$ to the objective, where $c_i$ is the marginal cost of production.

**No-Load Cost**: The term $C_i^{\text{NL}} u_{i,t}$ represents the **no-load cost**. This is a fixed cost incurred for every hour that unit $i$ is online ($u_{i,t}=1$), regardless of its power output level. Its economic interpretation arises from the physical properties of thermal generators. Even to remain synchronized to the grid at its [minimum stable output](@entry_id:1127943), a unit consumes a significant amount of fuel to maintain temperature and pressure and to power auxiliary systems. The no-load cost corresponds to the intercept of the unit's fuel-cost curve. By separating this fixed component from the variable production cost, the model accurately captures the total cost of operation when a unit is committed .

**Start-up and Shutdown Costs**: Transitioning a unit between off and on states incurs substantial costs. To model these, we introduce two additional binary [indicator variables](@entry_id:266428):
-   $y_{i,t} \in \{0, 1\}$: The **start-up variable**, where $y_{i,t}=1$ if unit $i$ starts up at the beginning of period $t$.
-   $z_{i,t} \in \{0, 1\}$: The **shutdown variable**, where $z_{i,t}=1$ if unit $i$ shuts down at the beginning of period $t$.

The corresponding terms in the objective function are $C_i^{\text{SU}} y_{i,t}$ and $C_i^{\text{SD}} z_{i,t}$. It is crucial to recognize that a single parameter like $C_i^{\text{SU}}$ is a simplification. The physical cost of a startup depends heavily on the unit's thermal state. A **hot start** (after a short shutdown) costs less than a **warm start**, which in turn costs less than a **cold start** (after a long shutdown). A single-parameter model cannot distinguish between these cases and typically uses an average or worst-case value. More advanced UC models incorporate temperature-dependent startup costs, but the term $C_i^{\text{SU}} y_{i,t}$ provides the basic linear structure required for a standard MILP .

### System-Wide Constraints

While many constraints apply to individual units, some must be enforced at the system level to ensure the grid operates as a whole.

**Power Balance**: The most fundamental system constraint is that total generation must meet total demand in every time period. In its simplest "copper plate" form (ignoring the [network topology](@entry_id:141407)), this is:

$$
\sum_{i=1}^N p_{i,t} = D_t
$$

where $D_t$ is the forecast demand for period $t$. A more realistic formulation acknowledges that the power system is not perfectly efficient and that demand is not entirely fixed. The balance equation can be extended to include **transmission losses** ($\ell_t$) and **[demand response](@entry_id:1123537)** ($r_t$). Losses represent power that is generated but dissipated as heat in the network, acting as an additional load that must be supplied. Demand response represents a reduction in consumption from a baseline forecast ($D_t^{\text{base}}$). The refined power balance equation becomes:

$$
\sum_{i=1}^N p_{i,t} = (D_t^{\text{base}} - r_t) + \ell_t
$$

This equation correctly states that total generation must cover both the power delivered to end-users and the power lost in transit .

**Operating Reserve**: To ensure grid reliability against unforeseen events like generator failures or demand forecast errors, system operators maintain a buffer of **[operating reserves](@entry_id:1129146)**. This is capacity that is online and can be quickly dispatched. This is modeled with a constraint of the form:

$$
\sum_{i=1}^N r_{i,t}^{\text{res}} \ge R_t
$$

where $r_{i,t}^{\text{res}}$ is the reserve contribution from unit $i$ and $R_t$ is the total system reserve requirement. The reserve provided by a unit is limited by its unused capacity, leading to a coupling with the power output: $p_{i,t} + r_{i,t}^{\text{res}} \le P_i^{\max} u_{i,t}$.

### Unit-Specific Temporal Constraints

The most complex aspects of the UC formulation are the constraints that link a unit's operation across time periods. These constraints model the physical inertia and stresses that limit how quickly a unit can change its state or output level.

**Logical Transition Constraints**: To make startup and shutdown costs meaningful, the [indicator variables](@entry_id:266428) $y_{i,t}$ and $z_{i,t}$ must be logically linked to the commitment status $u_{i,t}$. A startup occurs if and only if a unit was off at $t-1$ and is on at $t$. A shutdown is the reverse. A robust and tight formulation to capture this is a pair of constraints. The first relates the change in state to the [indicator variables](@entry_id:266428):

$$
u_{i,t} - u_{i,t-1} = y_{i,t} - z_{i,t}
$$

For the first period ($t=1$), this is initialized using the known status from the previous day, $\bar{u}_{i,0}$: $u_{i,1} - \bar{u}_{i,0} = y_{i,1} - z_{i,1}$. This single equation is insufficient because if the state does not change ($u_{i,t} = u_{i,t-1}$), it only implies $y_{i,t} = z_{i,t}$, allowing the physically impossible solution $y_{i,t}=1$ and $z_{i,t}=1$. We must therefore add a [mutual exclusivity](@entry_id:893613) constraint:

$$
y_{i,t} + z_{i,t} \le 1
$$

This set of constraints correctly and uniquely identifies startup and shutdown events . An alternative (but equally valid) way to define the startup indicator is through a set of inequalities: $y_{i,t} \ge u_{i,t} - u_{i,t-1}$, $y_{i,t} \le u_{i,t}$, and $y_{i,t} \le 1 - u_{i,t-1}$ .

**Minimum Up and Down Times**: Thermal power plants cannot be cycled on and off too frequently without incurring significant thermal stress and [material fatigue](@entry_id:260667). To prevent this, operational policies mandate a **minimum up time ($T_i^{\text{up}}$)** and a **minimum down time ($T_i^{\text{down}}$)**. Once a unit starts, it must remain on for at least $T_i^{\text{up}}$ consecutive periods. Once it shuts down, it must remain off for at least $T_i^{\text{down}}$ periods. These are enforced with "windowed" sum constraints that are triggered by a startup or shutdown event :

$$
\sum_{\tau=t}^{t + T_i^{\text{up}} - 1} u_{i,\tau} \ge T_i^{\text{up}} \cdot y_{i,t} \quad (\text{Minimum Up Time})
$$
$$
\sum_{\tau=t}^{t + T_i^{\text{down}} - 1} (1 - u_{i,\tau}) \ge T_i^{\text{down}} \cdot z_{i,t} \quad (\text{Minimum Down Time})
$$

If a startup occurs ($y_{i,t}=1$), the first [constraint forces](@entry_id:170257) all $u_{i,\tau}$ in the subsequent window of length $T_i^{\text{up}}$ to be 1. The logic for the minimum down time constraint is analogous.

**Ramping Constraints**: The power output of a generator cannot change instantaneously. The rate of change is limited by physical and thermal properties. These are known as **[ramping limits](@entry_id:1130533)**. A simple ramp constraint applies only when a unit is on for two consecutive periods: $p_{i,t} - p_{i,t-1} \le RU_i$, where $RU_i$ is the ramp-up limit. However, this does not properly account for the transitions of starting up or shutting down, which have their own specific ramping capabilities ($SU_i$ and $SD_i$). A more sophisticated and tighter formulation incorporates the unit's status:

$$
p_{i,t} - p_{i,t-1} \le RU_i u_{i,t-1} + SU_i y_{i,t}
$$
$$
p_{i,t-1} - p_{i,t} \le RD_i u_{i,t} + SD_i z_{i,t}
$$

Let's analyze the ramp-up constraint. If the unit was on at $t-1$ and stays on ($u_{i,t-1}=1, y_{i,t}=0$), the limit becomes $RU_i$. If the unit starts up at $t$ ($u_{i,t-1}=0, y_{i,t}=1$), the limit becomes $SU_i$ and applies to the output $p_{i,t}$ itself, since $p_{i,t-1}=0$. The ramp-down constraint works symmetrically. This formulation elegantly captures the different ramp limits applicable in different states using the [indicator variables](@entry_id:266428) .

### On Formulation Tightness and the Role of "Big-M"

The quality of an MILP formulation is judged not only by its correctness but also by its **tightness**. A tighter formulation has an LP relaxation (where integer variables are allowed to be continuous) that provides a better bound on the true integer solution, which generally allows the solver to find the optimal solution much faster. Many constraints in the UC model are "big-M" constraints, which use a large constant $M$ to turn a constraint on or off based on a binary variable.

The [ramping constraints](@entry_id:1130532) discussed above are a form of big-M constraint. A more explicit example is a generalized ramp constraint of the form $p_t - p_{t-1} \le R_{\text{up}} + M^{\text{up}} (2 - u_{t-1} - u_t)$. Here, the term $(2 - u_{t-1} - u_t)$ is zero only when the unit is on in both periods, thereby activating the base ramp limit $R_{\text{up}}$. When the constraint is meant to be deactivated (e.g., during a startup), the $M^{\text{up}}$ term must be large enough to not artificially restrict the variables.

Choosing the right value for $M$ is critical. It must be large enough to be valid, but no larger. An unnecessarily large $M$ weakens the LP relaxation and can cause [numerical instability](@entry_id:137058) in the solver. The tightest (smallest) valid value for $M$ is the maximum possible value of the expression it is meant to relax.

For example, consider the up-ramping constraint $p_t - p_{t-1} - R_{\text{up}} \le M^{\text{up}} (2 - u_{t-1} - u_t)$. We need to find the maximum possible value of the left-hand side when the constraint is inactive (i.e., when $(u_{t-1}, u_t) \ne (1,1)$). The worst case is a startup, where $p_{t-1}=0$ and $p_t$ can be as high as $P_{\max}$. The maximum value is thus $P_{\max} - 0 - R_{\text{up}}$. Therefore, the tightest valid value is $M^{\text{up}} = P_{\max} - R_{\text{up}}$. A similar analysis yields $M^{\text{down}} = P_{\max} - R_{\text{down}}$ for the ramp-down constraint .

These principles of creating tight, robust formulations are central to effective energy systems modeling. While the basic constraints define the problem, advanced techniques like deriving tight big-M values, generating [valid inequalities](@entry_id:636383) to strengthen the formulation (e.g., startup-specific ramp limits), and applying reformulations (e.g., perspective reformulation for convex costs) are what distinguish a theoretically correct model from a practically solvable one .