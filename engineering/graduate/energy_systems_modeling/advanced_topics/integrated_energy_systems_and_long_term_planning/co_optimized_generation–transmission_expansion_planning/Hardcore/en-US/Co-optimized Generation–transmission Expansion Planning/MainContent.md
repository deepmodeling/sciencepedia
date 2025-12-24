## Introduction
The global energy system is undergoing a profound transformation, driven by the need to decarbonize while maintaining reliability and affordability. This transition necessitates massive investments in new infrastructure, particularly [variable renewable energy](@entry_id:1133712) (VRE) sources like wind and solar. However, traditional planning methods, which often treat generation and transmission investments in separate silos, are ill-equipped to handle the complex interdependencies of a modern, renewables-rich grid. This siloed approach frequently leads to inefficient outcomes, stranded assets, and unnecessarily high system costs.

Co-optimized generation-[transmission expansion planning](@entry_id:1133366) provides a holistic and powerful alternative. By considering investments in both generation and the transmission network simultaneously within a single optimization framework, this method identifies the truly least-cost pathway to a reliable and sustainable energy future. It moves beyond simplistic metrics to capture the complex spatial and temporal value of different energy resources, ensuring that the right assets are built in the right places at the right time.

The following sections will guide you through this essential topic. In "Principles and Mechanisms," we will build the mathematical and economic foundation of co-optimization models from the ground up. "Applications and Interdisciplinary Connections" will explore how these models are used to solve real-world challenges, from VRE integration to gas-electric coordination. Finally, "Hands-On Practices" will offer practical exercises to solidify your understanding and build skills in applying these powerful concepts.

## Principles and Mechanisms

Co-optimized generation and [transmission expansion planning](@entry_id:1133366) represents a paradigm shift from traditional, siloed approaches to a holistic, system-level perspective. The core principle is that investment decisions in generation assets and transmission infrastructure are deeply intertwined; optimizing them jointly is essential to achieving a least-cost, reliable, and efficient energy future. This chapter delves into the fundamental principles and mathematical mechanisms that form the foundation of modern co-optimization models. We will construct these models from first principles, explore their economic interpretations, and address the practical challenges of their implementation.

### The Rationale for Co-optimization: Beyond Levelized Cost

A common starting point for comparing electricity generation technologies is the **Levelized Cost of Energy (LCOE)**. LCOE is an average cost metric, typically defined as the total discounted lifetime cost of a technology divided by its total discounted lifetime energy output. While useful for a first-order comparison, relying solely on LCOE for capacity expansion decisions can be profoundly misleading and lead to sub-optimal, high-cost system designs .

The fundamental limitation of LCOE is that it ignores the *system value* of energy. In a real power system, the value of one megawatt-hour is not constant; it varies dramatically depending on *when* and *where* it is produced. A megawatt-hour generated during a system peak when demand is high and reserves are scarce is far more valuable than one generated in the middle of the night when demand is low and there is a surplus of cheap generation. This time-varying value is formally captured in optimization models by the **[shadow price](@entry_id:137037)** (or Lagrange multiplier), often denoted as $\lambda_{n,t}$, on the power balance constraint at each node $n$ and time $t$. This shadow price represents the marginal cost of supplying one more unit of energy at that specific location and time.

Optimal investment decisions are driven not by minimizing average cost, but by equating the *marginal cost* of an investment with its *marginal value* to the system. The marginal value of a new generator or transmission line is determined by how its output profile aligns with the system's needs, as reflected in the pattern of shadow prices. For example, a solar farm may have a very low LCOE, but if its output is concentrated during midday hours when energy is already abundant (and $\lambda_{n,t}$ is low), its marginal value to the system can be small. Conversely, a flexible generator or a storage device that can provide energy during high-priced peak hours may be a superior investment despite a higher LCOE, because its marginal value is significantly greater .

Furthermore, LCOE calculations typically assume an exogenous capacity factor, but in reality, a technology's annual energy output, $E_y$, is endogenous to the system. It depends on the entire generation mix, network congestion, and operational constraints like curtailment. Co-optimization models endogenously determine the dispatch and, therefore, the true operational profile and value of each potential investment, providing a rigorous foundation for planning that LCOE cannot offer.

### Foundational Building Blocks of Expansion Models

To move beyond simple metrics and capture these systemic interactions, we construct optimization models based on the physical laws and economic realities of the power grid. These models are built upon a set of core mathematical components.

#### The Nodal Power Balance Constraint

The most fundamental constraint in any network model is the principle of energy conservation, an application of **Kirchhoff's Current Law (KCL)**. At every node (or bus) $i$ in the network and for every time period $t$, the total power injected into the node must equal the total power withdrawn from it. This ensures that supply meets demand at all locations and times. A comprehensive [nodal power balance](@entry_id:1128739) equation includes all possible sources and sinks of power :

$$
g_{i,t} + dis_{i,t} + \sum_{j \in \mathcal{N}, j \neq i} (1-\ell_{j\to i}) f_{j\to i,t} + m_{i,t} \;=\; d_{i,t} + ch_{i,t} + \sum_{k \in \mathcal{N}, k \neq i} f_{i\to k,t} + l_{i,t}
$$

On the left-hand side are the **injections**:
- $g_{i,t}$: Power generated by dispatchable units at node $i$.
- $dis_{i,t}$: Power discharged from energy storage devices at node $i$.
- $\sum_{j \in \mathcal{N}, j \neq i} (1-\ell_{j\to i}) f_{j\to i,t}$: Power received at node $i$ from transmission flows originating at other nodes $j$. This term critically accounts for resistive losses, where $f_{j\to i,t}$ is the power *sent* from $j$ and $\ell_{j\to i}$ is the fractional loss on the line.
- $m_{i,t}$: Net power imports from adjacent systems connected to node $i$.

On the right-hand side are the **withdrawals**:
- $d_{i,t}$: Inelastic electrical demand (load) at node $i$.
- $ch_{i,t}$: Power drawn from the grid to charge energy storage devices at node $i$.
- $\sum_{k \in \mathcal{N}, k \neq i} f_{i\to k,t}$: Power *sent* from node $i$ to other nodes $k$.
- $l_{i,t}$: Other local losses, such as in the distribution network.

This equation is the bedrock of the model, ensuring physical feasibility in every time slice and at every location.

#### Modeling the Network: The DC Power Flow Approximation

To model the transmission flows $f_{i \to j, t}$, we require a representation of the network physics. For large-scale planning studies, the **Direct Current Optimal Power Flow (DC-OPF)** approximation is the industry and academic standard. It provides a linear model of power flows that is computationally tractable while capturing the essential effects of network topology and constraints. The DC approximation relies on three key assumptions: (1) all bus voltage magnitudes are approximately $1.0$ per unit; (2) the angular difference between connected buses is small; and (3) line resistances are negligible compared to reactances.

Under these assumptions, the real power flow $f_{l,t}$ on a line $l$ connecting bus $i$ to bus $j$ is a linear function of the difference in their voltage phase angles, $\theta_{i,t}$ and $\theta_{j,t}$ :

$$
f_{l,t} = b_l (\theta_{i,t} - \theta_{j,t})
$$

Here, $b_l$ is the **susceptance** of the line, which is the reciprocal of its reactance ($b_l = 1/x_l$). The voltage angles $\theta$ become decision variables in the optimization. To ensure a unique solution, the angle at one bus is typically fixed to zero, creating a **reference bus** (or slack bus).

#### Modeling Investment and Costs

The objective of an expansion planning model is to minimize total system cost, which is the sum of investment and operational costs.
- **Investment Costs**: These are the capital expenditures (CAPEX) for building new assets. For a new generator with capacity $K_g$ and unit investment cost $c^{I,G}$, the cost is $c^{I,G} K_g$. For transmission, the cost of expanding a line's capacity by $\Delta F$ is $c^{I,F} \Delta F$. These costs are typically annualized over the asset's lifetime.
- **Operating Costs**: These are the variable costs (OPEX) of running the system. For a thermal generator, this is primarily its fuel cost, often modeled with a linear marginal cost $c_g$ (in \$/MWh), leading to an operating cost of $c_g \cdot g_t$. More detailed models can use convex quadratic functions, such as $C(g_t) = \alpha g_t^2 + \beta g_t$, to represent increasing marginal costs with output .

Investment decisions themselves can be modeled in two primary ways:
1.  **Continuous Investment**: Capacity can be added in any non-negative amount ($K \ge 0$). This is mathematically convenient and often used when assets are highly divisible or for high-level planning studies .
2.  **Discrete (Integer) Investment**: Capacity can only be added in predefined "lumps" or modules. This is often represented with binary variables ($x \in \{0, 1\}$ to represent a build/no-build decision) or integer variables ($y \in \{0, 1, 2, \dots\}$ to represent the number of modules built). This is more realistic for large, indivisible assets like power plants or major transmission lines .

### The Core Optimization Problem: A Static Expansion Formulation

By combining these building blocks, we can formulate the canonical static (single-period) co-optimized expansion planning problem.

#### Formulation as a Mixed-Integer Linear Program (MILP)

When investment decisions are discrete, the problem naturally becomes a **Mixed-Integer Linear Program (MILP)**. Let's consider a simple yet powerful two-node example to illustrate the full formulation . Imagine a system with a low-cost generation site (Node 1) and a load center (Node 2) with expensive local generation. The planner must decide whether to build a new generator at Node 1 (binary decision $x \in \{0,1\}$) and whether to upgrade the transmission line between them (binary decision $y \in \{0,1\}$).

The objective is to minimize the sum of annualized investment costs and total hourly operating costs:

$$
\text{Minimize} \quad (F_g \cdot x + F_{\ell} \cdot y) + (c_1 \cdot g_1 + c_2 \cdot g_2)
$$

This objective is minimized subject to a set of constraints:
- **Power Balance**: $g_1 = p_{12}$ (at Node 1) and $g_2 + p_{12} = d_2$ (at Node 2), where $p_{12}$ is the flow from 1 to 2.
- **DC Power Flow**: $p_{12} = b(\theta_1 - \theta_2)$, with $\theta_2=0$ as the reference.
- **Generation Capacity**: The new generator's output $g_1$ is linked to the investment decision: $0 \le g_1 \le \overline{G}_1 \cdot x$. If $x=0$, $g_1$ must be zero. If $x=1$, $g_1$ is limited by its capacity $\overline{G}_1$.
- **Transmission Capacity**: The flow limit is also linked to the investment decision: $|p_{12}| \le \overline{F}^{\text{base}} + \Delta\overline{F} \cdot y$. This constraint creates a non-convex feasible region, which is the hallmark of integer programming.

The presence of the binary variables $x$ and $y$ fundamentally changes the problem's nature. A standard operational OPF with fixed assets is a Linear Program (LP), which can be solved efficiently. The introduction of integer decisions makes the problem **NP-hard**. This means the computational time required to find a guaranteed optimal solution can grow exponentially with the number of integer variables, necessitating sophisticated solvers and algorithms like branch-and-cut. This is a crucial distinction between operational (LP) and investment (MILP) models .

#### Economic Interpretation of Optimal Expansion

To gain deeper economic insight, it is useful to consider a case with continuous investment variables . In such a formulation, the Karush-Kuhn-Tucker (KKT) optimality conditions reveal a powerful economic principle. At the optimal level of investment, the **marginal cost of adding capacity must equal the marginal benefit it provides**.

The marginal benefit of transmission capacity is the reduction in total system operating cost it enables. This reduction comes from displacing expensive local generation with cheaper remote generation. Consider a line connecting a low-cost region (marginal cost $c_1$) to a high-cost region (marginal cost $c_2$). Without the line, the price difference is $c_2 - c_1$. A transmission line with capacity $K$ allows for a flow that reduces this price gap. The marginal value of an additional unit of capacity, $\Delta K$, is precisely the reduction in the total cost of generation, which is related to the difference in nodal prices.

In a formal optimization, the Lagrange multiplier $\lambda$ on the transmission capacity constraint $|f| \le K$ represents the marginal value of that capacity. The optimality condition for the investment variable $K$ becomes:

$$
c^{I,F} = \lambda
$$

where $c^{I,F}$ is the marginal investment cost of transmission. This elegant result states that we should continue investing in transmission capacity until the cost of the next megawatt of capacity is exactly equal to the marginal system value it provides. A similar principle applies to generation investment. The optimal capacity for a new generator is determined where the marginal investment cost equals the marginal value it provides to the system. This value is the total reduction in operating costs (producer surplus) that the new capacity enables over its lifetime, which is a function of how often and how much it can displace more expensive generation .

### Incorporating Modern Energy System Components

The basic framework can be extended to model the key technologies of modern, low-carbon power systems: variable renewables and energy storage.

#### Modeling Energy Storage

Energy storage, such as batteries, offers temporal flexibility. It can absorb cheap energy when it is plentiful and inject it back into the grid when energy is scarce and expensive. In doing so, it can act as a substitute for either transmission capacity or conventional peaking generators . Modeling storage requires introducing new variables and constraints:

- **Decision Variables**: Storage is characterized by its charging power ($p^{ch}_t$), discharging power ($p^{dis}_t$), and its energy state-of-charge ($e_t$). Investment decisions correspond to its power capacity ($P_s$) and energy capacity ($E_s$).
- **State-of-Charge Dynamics**: The core constraint links the energy level between time periods, accounting for losses:
$$
e_t = e_{t-1} + \eta^{ch} p^{ch}_t \cdot \Delta t - \frac{1}{\eta^{dis}} p^{dis}_t \cdot \Delta t
$$
where $\eta^{ch}$ and $\eta^{dis}$ are the charging and discharging efficiencies, respectively, and $\Delta t$ is the duration of the time step.
- **Capacity Limits**: The variables are bounded by the invested capacities: $0 \le p^{ch}_t \le P_s$, $0 \le p^{dis}_t \le P_s$, and $0 \le e_t \le E_s$.
- **Cyclic Constraint**: When modeling a representative period (e.g., a day or week), a cyclic constraint $e_T = e_0$ is often imposed to ensure that the storage device's operation is sustainable over the long term .

#### Modeling Variable Renewable Energy (VRE)

Modeling VRE sources like wind and solar is conceptually straightforward but has profound implications for the system. The key feature is that their output is not fully dispatchable but is limited by the available natural resource. This is captured by a simple capacity constraint that incorporates a time-varying availability factor, $a_t$ :

$$
0 \le g_{vre,t} \le a_t \cdot K_{vre}
$$

Here, $K_{vre}$ is the invested nameplate capacity of the VRE plant, and $a_t \in [0, 1]$ is the capacity factor at time $t$. The time series of availability factors, $\{a_t\}$, is a crucial data input that captures the diurnal, seasonal, and stochastic nature of the renewable resource. The need to balance the system around this variable and partially uncontrollable generation source is a primary driver for investments in transmission, storage, and flexible generation .

### Ensuring Reliability: Security-Constrained Planning

A least-cost system is of little use if it is not reliable. Transmission planning must therefore ensure that the grid can withstand credible disturbances without catastrophic failure. The most common standard for this is the **N-1 security criterion**, which mandates that the system must remain in a secure state following the unexpected loss of any single major component (e.g., a transmission line or generator).

Incorporating this criterion into an expansion model leads to a **Security-Constrained Optimal Power Flow (SCOPF)** formulation. In a **preventive SCOPF**, the pre-contingency dispatch is optimized such that *no corrective action* is needed to alleviate violations after a contingency occurs . This is a conservative but highly robust approach.

Modeling this directly would require re-solving the power flow for every possible line outage, for every time step—a computationally impossible task within a large-scale optimization. Instead, we use pre-computed **sensitivity factors**. A **Line Outage Distribution Factor (LODF)** quantifies how the flow on one line changes in response to an outage of another. The post-contingency flow on line $k$ after an outage of line $m$, $f^{\text{post}}_{k|m}$, can be approximated as a linear function of the pre-contingency flows :

$$
f^{\text{post}}_{k|m} = f^{\text{base}}_{k} + \operatorname{LODF}_{k,m} \cdot f^{\text{base}}_{m}
$$

Using this relationship, we can add a set of linear constraints to our main MILP for each potential contingency $m$ and each monitored line $k$:

$$
|f^{\text{base}}_{k} + \operatorname{LODF}_{k,m} \cdot f^{\text{base}}_{m}| \le \overline{F}_k
$$

These constraints ensure that the chosen pre-contingency dispatch is inherently "N-1 secure." This added security comes at a cost; enforcing these constraints will always result in a total system cost that is greater than or equal to the cost of a model without them. The dual variables on these security constraints provide a direct monetary measure of the marginal cost of ensuring reliability for a specific contingency, offering valuable insight for planners .

### Practical Modeling Considerations

Translating the theoretical models described above into practical, solvable tools requires addressing several important implementation details.

#### Dynamic Planning and Investment Lead Times

Real-world planning is not static; it occurs over a multi-year horizon. A **dynamic planning model** makes investment decisions in multiple stages over time. A critical feature of dynamic models is the inclusion of **investment lead times**. An investment decision made today does not result in available capacity until several years in the future. This is modeled by accumulating capacity over time based on past decisions :

$$
G_{n,t} = G^{0}_n + \sum_{\tau=1}^{t - L^{G}_n} x^{G}_{n,\tau}
$$

Here, the available capacity $G_{n,t}$ at time period $t$ is the initial capacity $G^0_n$ plus the sum of all investment decisions $x^G_{n,\tau}$ made up to period $t - L^G_n$, where $L^G_n$ is the lead time in years. This inter-temporal link makes the problem larger but more accurately reflects the long-term nature of infrastructure planning. Costs incurred in future years are brought to a present value using a **discount factor**, $\delta_t$.

#### Temporal Resolution and Representative Periods

Modeling an entire year at an hourly resolution (8760 time steps) is computationally intensive, especially for dynamic, security-constrained MILPs. To manage this complexity, planners use **temporal aggregation** techniques. A naive approach, such as using monthly average load and VRE availability, will fail spectacularly because it discards the very chronological variations and correlations that drive the need for flexibility and transmission .

A more sophisticated and valid approach is the use of **representative periods** . This method involves:
1.  **Clustering**: Analyzing a full year of chronological data (load, wind, solar profiles) and using clustering algorithms to identify a small set of "typical" or "archetypal" days or weeks that capture the full range of operating conditions (e.g., a sunny winter weekday, a windy summer weekend, a calm, cold peak-demand day).
2.  **Weighting**: Each representative period $t$ is assigned a weight, $h_t$, representing the number of hours in the year that this period represents.
3.  **Optimization**: The expansion planning model is then solved over this reduced set of periods. The total annual operating cost is calculated as the weighted sum of the operating costs from each representative period.

This technique reduces computational burden while preserving the critical chronological dependencies (for ramping and storage) within each period and the statistical diversity of conditions across the year, leading to more robust investment decisions.

#### Data Requirements and Granularity

The principle that "the model is only as good as the data" is paramount. A well-posed co-optimization model requires a rich and granular dataset to avoid structural biases . Essential inputs include:
- **Nodal Load Profiles**: Time series of demand at each major bus in the network.
- **VRE Availability Factors**: Co-located and time-synchronized availability factors for each potential renewable technology at each node.
- **Cost Parameters**: Projections for capital costs, fixed and variable operating costs, and fuel costs for all technologies.
- **Network Parameters**: A complete description of the transmission grid, including line reactances (for DC-OPF), thermal limits, and topology.

The granularity of this data is critical. As discussed, hourly or sub-hourly chronological data is necessary to capture ramping requirements, storage arbitrage opportunities, and the crucial covariance between load and VRE generation. Spatial granularity at the nodal level is required to accurately model congestion and make meaningful decisions about where to site new generation and build new transmission lines. Neglecting either temporal or spatial detail will obscure the very system interactions that co-optimization is designed to resolve.