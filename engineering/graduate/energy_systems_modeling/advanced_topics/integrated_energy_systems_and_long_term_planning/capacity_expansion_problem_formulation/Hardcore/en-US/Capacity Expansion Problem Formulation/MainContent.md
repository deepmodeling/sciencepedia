## Introduction
Capacity expansion modeling stands as a cornerstone of modern energy [system analysis](@entry_id:263805), providing a structured framework to navigate the complex, multi-decade challenge of planning future infrastructure. At its heart, it addresses a critical question: how can we determine the most cost-effective portfolio of power plants, transmission lines, and storage assets to build and operate in order to reliably meet future energy demands while adhering to environmental and policy goals? This task requires translating intricate physical, economic, and regulatory realities into a coherent mathematical optimization problem. This article demystifies this process, guiding you through the formulation of [capacity expansion models](@entry_id:1122042) from first principles to advanced applications.

Across the following chapters, you will gain a comprehensive understanding of this powerful analytical tool. The journey begins in **Principles and Mechanisms**, where we will deconstruct the model into its fundamental components: the mathematical sets, variables, objective function, and constraints that define the decision space and physical laws of the system. Next, in **Applications and Interdisciplinary Connections**, we will explore how this foundational framework is extended to represent sophisticated technologies, analyze complex policy scenarios, and grapple with the inherent uncertainties of the future. Finally, the **Hands-On Practices** section provides an opportunity to apply these concepts through targeted coding exercises, solidifying your ability to build and interpret these models. By proceeding through this structured path, you will learn not just the theory but also the practical art of formulating capacity expansion problems for real-world energy planning.

## Principles and Mechanisms

Capacity expansion models are sophisticated analytical tools that formalize the long-term planning problem of an energy system. At their core, these models are large-scale optimization problems designed to determine the least-cost portfolio of investments and operational strategies required to meet future energy demands reliably. This chapter delves into the fundamental principles and mechanisms that constitute the architecture of these models. We will construct the essential components of a capacity expansion model from first principles, examining the formulation of its mathematical structure, economic objective, and physical constraints.

### Foundational Structure: Defining the Decision Space

Every optimization model is constructed upon a scaffold of sets, parameters, and variables. This formal structure defines the scope of the problem—what is being decided, over what dimensions, and subject to what data.

#### Index Sets as the Model's Skeleton

Index sets provide the fundamental dimensions over which decisions are made and data are defined. They are the coordinates of our planning problem, allowing for a precise and granular representation of the energy system. Common and essential index sets include:

*   **Technologies ($k \in \mathcal{K}$ or $i \in \mathcal{I}$):** This set encompasses all technology options available for investment and operation, such as natural gas [combined cycle](@entry_id:189658) plants, solar photovoltaic arrays, wind turbines, battery storage systems, and transmission lines.

*   **Time Periods ($p \in \mathcal{P}$ or $y \in \mathcal{Y}$):** These represent the discrete investment periods over the planning horizon. A period is typically one or more years (e.g., 2025, 2030, 2035), and decisions to build new capacity are made for each of these periods.

*   **Spatial Nodes ($n \in \mathcal{N}$):** To capture the geographic aspects of an energy system, the model domain is divided into a set of nodes or regions. This allows for modeling of region-specific resource availability (e.g., higher solar [irradiance](@entry_id:176465) in one region), demand centers, and the network of transmission lines that connect them. Capturing spatial heterogeneity via the node index $n$ is critical for realistic planning .

*   **Intra-Period Time Slices ($t \in \mathcal{T}$ or $h \in \mathcal{H}$):** Within each investment period (e.g., the year 2030), operational conditions like demand and renewable energy availability can vary significantly. To capture this, each period is subdivided into a set of operational time slices, which can represent seasons, days, or even hours. Decisions about how to operate, or **dispatch**, the system are made for each of these slices.

*   **Vintages ($v \in \mathcal{V}$):** A power plant's performance, such as its efficiency and reliability, often depends on when it was built. A plant commissioned in 2040 will likely be more efficient than one from 2020. To capture these age-dependent characteristics, we use a **vintage** index, which denotes the commissioning period of a specific cohort of capacity. This allows the model to distinguish between old and new assets, a crucial feature for accurately modeling an evolving capital stock .

#### Core Decision Variables

With the model's structure defined by index sets, we can specify the decision variables, which represent the choices the model must make. The two primary categories of decisions are investment and operation.

*   **Investment and Capacity Variables:** These variables represent the long-term decision of *what, where, and when to build*. A continuous variable, such as $a_{t,n,p} \in \mathbb{R}_{+}$ from , can represent the amount of new capacity (in megawatts, MW) of technology $t$ to be added at node $n$ in investment period $p$. These are often called **stock** variables, as they add to the capital stock of the system. For lumpy investments where technologies come in discrete unit sizes, a **binary [indicator variable](@entry_id:204387)**, such as $y_{t,n,p} \in \{0,1\}$, might be used to represent the choice of whether or not to build a unit, often in conjunction with a continuous variable to specify its size.

*   **Operational and Dispatch Variables:** These variables represent the short-term decision of *how to operate the available assets* to meet demand in each time slice. A dispatch variable, such as $g_{t,n,p,h} \in \mathbb{R}_{+}$ from , represents the power output (in MW) from technology $t$ at node $n$ during time slice $h$ of investment period $p$. These are **flow** variables, representing the flow of energy through the system. The indexing is critical: operational decisions must be made at the finest temporal and spatial resolution of the model (i.e., for each node $n$ and time slice $h$) to ensure that local energy balance is met at all times.

### The Objective Function: Quantifying Economic Rationality

The objective function provides the model with a singular goal. For a social planner, this goal is typically to minimize the total system cost over the entire planning horizon, while ensuring demand is met reliably. This requires aggregating all costs—capital, operational, fuel, and policy-related—and expressing them in a common metric.

#### Discounting and Net Present Value (NPV)

A dollar today is worth more than a dollar in the future due to investment opportunities and other factors. This principle, known as the **time value of money**, is incorporated into [capacity expansion models](@entry_id:1122042) through **discounting**. All future costs are converted to their equivalent value in a base year (e.g., the present) using a **discount rate** $r$. A cost $C_t$ incurred in a future year $t$ is discounted to its **Net Present Value (NPV)** by multiplying it by a **discount factor** $d_t = \frac{1}{(1+r)^t}$. The total system cost is then the sum of the NPV of costs from all years in the planning horizon. The discount factor itself is dimensionless, ensuring that it simply scales the currency value without altering its units .

#### Anatomy of System Costs

The total system cost is the sum of several distinct components, each with a specific physical basis and mathematical representation. A comprehensive objective function must correctly account for all of them.

*   **Capital Expenditures (CAPEX):** This is the one-time, upfront cost of building new capacity. If $\Delta K_{g,y}$ is the new capacity (MW) of technology $g$ built in year $y$, and $c^{\mathrm{capex}}_g$ is its capital cost in dollars per MW, the total CAPEX for that year is $\sum_g c^{\mathrm{capex}}_g \Delta K_{g,y}$. This cost is applied only to newly built capacity, not the entire stock .

*   **Fixed Operation and Maintenance (FOM):** These are annual costs incurred for keeping capacity operational, regardless of how much it is used. They include costs like salaries, security, and land leases. If $K_{g,y}$ is the total installed capacity (MW) of technology $g$ in service during year $y$, and $c^{\mathrm{fom}}_g$ is its fixed cost in dollars per MW-year, the total FOM for that year is $\sum_g c^{\mathrm{fom}}_g K_{g,y}$. Unlike CAPEX, FOM applies to the entire active capacity stock.

*   **Variable Operation and Maintenance (VOM):** These costs are directly proportional to the amount of energy produced. They include costs for consumables and component wear-and-tear. If $g_{i,t}$ is the energy generation (in MWh) from technology $i$ in a given period $t$, and $c^{\mathrm{var}}_i$ is its variable cost in dollars per MWh, the total VOM cost is $\sum_i c^{\mathrm{var}}_i g_{i,t}$.

*   **Fuel Costs:** For technologies that consume fuel (e.g., natural gas, coal), this is often the largest variable cost component. If $c^{\mathrm{fuel}}_{i,t}$ is the fuel cost in dollars per MWh of generation, the total fuel cost is $\sum_i c^{\mathrm{fuel}}_{i,t} g_{i,t}$.

*   **Policy Costs:** These are costs arising from government policies, most commonly a price on carbon emissions. If $\pi_t$ is the carbon price in dollars per ton of CO2, and $\eta_i$ is the emissions factor of technology $i$ in tons of CO2 per MWh, the total emissions cost is $\sum_i (\pi_t \eta_i) g_{i,t}$.

The complete objective function for a social planner is the minimization of the sum of the discounted value of all these costs over the entire planning horizon . For a planning horizon $\mathcal{Y}$, the objective is:
$$ \min \sum_{y \in \mathcal{Y}} d_y \left[ \text{CAPEX}_y + \text{FOM}_y + \text{VOM}_y + \text{FuelCost}_y + \text{PolicyCost}_y \right] $$
Substituting the detailed expressions for each cost component gives a comprehensive formulation as demonstrated in .

#### A Note on Dimensional Homogeneity

A critical step in model formulation is ensuring **[dimensional homogeneity](@entry_id:143574)**, or unit consistency. Every term being added together in the objective function must have the same units—in this case, currency (e.g., USD). Similarly, both sides of an equality constraint must have identical units. For example, the emissions cost term $p^{\mathrm{CO2}}_y \cdot \varepsilon_i \cdot g_{i,t,y}$ is dimensionally consistent because the units multiply and cancel out: $(\mathrm{USD}/\mathrm{ton}) \times (\mathrm{ton}/\mathrm{MWh}) \times \mathrm{MWh} = \mathrm{USD}$ . Verifying unit consistency is a fundamental practice for preventing formulation errors and ensuring the model's physical and economic coherence.

### Core Constraints: Defining Physical and Operational Feasibility

Constraints are the mathematical statements that define the "rules of the game" for the energy system. They ensure that the model's solution is physically possible, operationally viable, and meets all service requirements.

#### The Power Balance Constraint

The most fundamental constraint in any power system model is the **power balance** (or energy balance), which enforces the principle of conservation of energy at every node and in every time slice. It stipulates that total power injections must equal total power withdrawals.

In a multi-node system with transmission, storage, and other complexities, this balance becomes more elaborate. For any given node $i$ and time slice $t$, the equation takes the form:
$$ \text{Injections} = \text{Withdrawals} $$
A comprehensive formulation, as explored in , itemizes these components:
$$ g_{i,t} + dis_{i,t} + \sum_{j \neq i} (1-\ell_{j\to i}) f_{j\to i,t} + m_{i,t} = d_{i,t} + ch_{i,t} + \sum_{k \neq i} f_{i\to k,t} + l_{i,t} $$

Here, the terms on the left side are injections: local generation ($g_{i,t}$), storage discharging ($dis_{i,t}$), transmission inflows from other nodes ($f_{j\to i,t}$, adjusted for line losses $\ell_{j\to i}$), and net imports ($m_{i,t}$). The terms on the right side are withdrawals: local demand ($d_{i,t}$), storage charging ($ch_{i,t}$), transmission outflows to other nodes ($f_{i\to k,t}$), and other local losses ($l_{i,t}$). This constraint must hold for all nodes and all time slices, ensuring the system is feasible everywhere and at all times.

#### Capacity and Dispatch Constraints

These constraints link investment decisions (capacity) to operational decisions (dispatch). The core principle is simple: a technology cannot generate more power than its available capacity allows.

However, the "available" capacity is not merely the **nameplate capacity** installed. It must be derated to account for various real-world limitations. Two primary sources of unavailability are:

1.  **Systematic Availability ($a_{k,t}$):** This dimensionless factor ($[0,1]$) represents predictable or systematic limitations. For renewable technologies like wind and solar, it represents the availability of the resource (i.e., the capacity factor). For dispatchable plants, it can represent scheduled maintenance periods.

2.  **Forced Outage Rate (FOR, $f_k$):** This factor ($[0,1]$) represents the probability that a unit is unavailable due to an unscheduled or forced outage (e.g., equipment failure). The probability that a unit is *not* on a forced outage is therefore $(1-f_k)$.

Assuming these two sources of unavailability are independent, the expected fraction of nameplate capacity that is truly available for dispatch is their product, $a_{k,t} \times (1-f_k)$. The maximum dispatch constraint for technology $k$ in time slice $t$ is then:
$$ g_{k,t} \le a_{k,t}(1 - f_k)K_k $$
where $K_k$ is the total installed nameplate capacity. For example, consider a 700 MW gas plant with perfect systematic availability ($a_{\text{g},t}=1$) but a [forced outage rate](@entry_id:1125211) of 8% ($f_{\text{g}}=0.08$). Its expected available capacity for dispatch is not 700 MW, but rather $1 \times (1-0.08) \times 700~\text{MW} = 644~\text{MW}$. Similarly, a 500 MW wind farm with a capacity factor of 50% ($a_{\text{w},t}=0.5$) and a [forced outage rate](@entry_id:1125211) of 2% ($f_{\text{w}}=0.02$) would have an [expected maximum](@entry_id:265227) output of $0.5 \times (1-0.02) \times 500~\text{MW} = 245~\text{MW}$ .

### Advanced Mechanisms for Long-Term Dynamics

For long-term planning, it is insufficient to [model capacity](@entry_id:634375) as a simple aggregate stock. We must also capture the processes of aging, performance degradation, and retirement. Furthermore, we must manage the computational burden that arises from modeling many years of detailed operations.

#### Modeling Capital Stock Evolution: Vintages and Retirements

A key mechanism for modeling the evolution of the capital stock is **vintage tracking**. As introduced earlier, this involves indexing capacity not just by technology, but also by its commissioning period, or vintage ($v$). This allows the model to distinguish between assets of different ages.

The dynamics of this vintage-indexed capacity stock are governed by a set of **stock-flow accounting equations**. For a given technology $i$ and vintage $v$, let $B_{i,v}$ be the new capacity built, $A_{i,t,v}$ be the active capacity in period $t$, and $R_{i,t,v}$ be the capacity retired in period $t$. The dynamics can be formulated as follows :

1.  **Initialization:** Capacity of vintage $v$ comes into existence in period $v$. Thus, $A_{i,v,v} = B_{i,v}$. Before this, $A_{i,t,v}=0$ for all $t \lt v$.

2.  **Evolution:** In subsequent periods ($t > v$), the active stock is the previous period's stock minus retirements: $A_{i,t,v} = A_{i,t-1,v} - R_{i,t,v}$.

3.  **Endogenous Retirement:** The retirement variable $R_{i,t,v}$ is a decision variable, allowing the model to choose to retire capacity early if it is economically optimal (e.g., if it becomes too expensive to operate). Retirements are bounded such that $0 \le R_{i,t,v} \le A_{i,t-1,v}$.

4.  **Technical Lifetime:** Every technology has a maximum technical lifetime, $L_i$. All capacity of vintage $v$ must be retired by the end of its life. This is enforced with a hard constraint: $A_{i,t,v} = 0$ for all $t \ge v + L_i$.

This vintage-based framework provides a powerful and accurate way to model the lifecycle of assets within the energy system.

#### Managing Computational Complexity: Representative Time Slices

Modeling every hour of every year in a multi-decade planning horizon is computationally intractable. A standard technique to address this is to approximate the full chronology of operations using a small number of **representative time slices**. The goal is to reduce computational load while preserving the key characteristics of the original chronological data, namely the total energy demand and the peak demand conditions.

This is achieved by partitioning the hours of a year into clusters, or slices ($s \in \mathcal{S}$). Each slice is defined by a single set of representative parameters (e.g., average demand $\bar{d}_s$, average renewable availability $\bar{a}_s$) and a weight ($w_s$) corresponding to the number of hours it represents . To preserve total energy, the representative values are typically the arithmetic mean of the values in that slice, and the weight $w_s$ is the number of hours in the slice.

A critical feature of this method is the treatment of extreme events. If the hour with the highest demand of the year (the **peak hour**) is averaged with many other hours, the resulting representative demand will be much lower than the actual peak. This would cause the model to underestimate the capacity needed for resource adequacy. The [standard solution](@entry_id:183092) is to isolate the peak demand hour(s) into a dedicated **peak slice**. For this singleton slice, the representative demand is exactly the true peak demand, ensuring this critical adequacy signal is not lost in the aggregation process .

### Economic Interpretations: From Planner to Market

The formulation described thus far adopts the perspective of a central **social planner** whose objective is to minimize total system cost. This is a powerful and common framework for long-term policy and infrastructure analysis. However, in many parts of the world, investment decisions are not made by a central planner but by decentralized, profit-seeking firms operating in a competitive market.

There is a deep connection between these two perspectives. A **decentralized competitive equilibrium** can be formulated where each investor in a technology $i$ seeks to maximize their own profit, taking market prices $\{p_t\}$ as given :
$$ \max_{\{K_i, g_{it}\}} \quad \sum_{t \in \mathcal{T}} p_t g_{it} - \sum_{t \in \mathcal{T}} c_i^{\mathrm{var}} g_{it} - c_i^{\mathrm{inv}} K_i $$
subject to their own operational constraints ($0 \le g_{it} \le a_{it}K_i$). In equilibrium, a set of prices $\{p_t\}$ must emerge such that the market clears (i.e., total generation from all profit-maximizing investors equals demand).

Under the assumptions of perfect competition, the First Fundamental Theorem of Welfare Economics implies that the outcome of this decentralized competitive market is equivalent to the solution of the social planner's cost-minimization problem. The wholesale energy prices $p_t$ in the [market equilibrium](@entry_id:138207) are precisely the **shadow prices** (or Lagrange multipliers) on the energy balance constraints in the planner's problem. This profound result provides a strong theoretical foundation for using centralized optimization models to understand and anticipate the behavior of competitive energy markets.