## Introduction
Energy system planning spans vastly different timescales, from multi-decade infrastructure investments to sub-second operational adjustments. This multi-horizon nature presents a central modeling challenge: how to make strategic long-term decisions that are operationally feasible in the short term without creating models of intractable complexity. A single, monolithic model that captures every detail over decades is computationally impossible. This article addresses this critical knowledge gap by providing a structured guide to designing and linking long-term and short-term energy system models.

In the following chapters, you will first explore the foundational "Principles and Mechanisms" that distinguish long-term investment from [short-term operational models](@entry_id:1131591) and the techniques used to couple them. Next, "Applications and Interdisciplinary Connections" will demonstrate how these principles are applied to real-world problems like resource adequacy and storage valuation, drawing parallels to similar challenges in other scientific fields. Finally, the "Hands-On Practices" chapter will offer opportunities to apply these concepts, solidifying your understanding of how to build and analyze multi-horizon energy models.

## Principles and Mechanisms

Energy system planning is fundamentally a multi-scale endeavor. Decisions range from billion-dollar investments in power plants with 50-year lifetimes to sub-second adjustments in generator output to maintain [grid stability](@entry_id:1125804). A central challenge in energy systems modeling is to coherently represent and link these disparate temporal scales. A single monolithic model that captures every operational detail over a multi-decade horizon is computationally intractable. Therefore, the art and science of this field lie in the principled design of distinct but interconnected models for different planning horizons. This chapter elucidates the core principles and mechanisms governing the design and linkage of long-term and short-term models.

### The Dichotomy of Planning Horizons: Investment versus Operation

The first and most crucial step in modeling is to recognize the fundamental dichotomy between long-term investment planning and short-term operational scheduling. The **planning horizon**, defined as the temporal domain over which a model optimizes decisions, must be tailored to the nature of the questions being asked and the decisions being made .

#### Long-Term Horizons: Strategic Investment and Capacity Expansion

Long-term models address strategic questions over horizons spanning years to decades. Their primary purpose is to guide **structural decisions**—high-cost, long-lead-time choices that shape the physical infrastructure of the energy system for years to come.

*   **Decision Variables**: The key decisions in these models are investments ($y$) and retirements of major assets. This includes the capacity, technology type, and location of new power plants, large-scale energy storage facilities, and high-voltage transmission lines. These are often termed "here-and-now" decisions because, despite their long-term consequences, the commitment to invest is made at the beginning of the planning period under uncertainty about the future.  

*   **Constraints and Objectives**: The focus is on ensuring long-run system viability. Constraints enforce aggregate energy balances over coarse time slices (e.g., monthly or annual), meet projected peak demand with a certain reliability margin (**capacity adequacy**), respect overall resource potentials (e.g., total available land for solar farms), and adhere to cumulative policy targets, such as caps on greenhouse gas emissions. The objective is typically to minimize total discounted system cost, comprising capital expenditures on new assets and aggregate operational costs.

*   **Representation of Uncertainty**: Uncertainty in the long term is structural and macroeconomic. Key drivers include future demand growth, long-term trajectories of fuel prices, the rate of technological progress and cost reduction ([learning curves](@entry_id:636273)), and the evolution of energy and [climate policy](@entry_id:1122477). This uncertainty is commonly represented using a [discrete set](@entry_id:146023) of divergent, multi-stage scenarios. The objective function may incorporate risk measures like Conditional Value-at-Risk (CVaR) to hedge against particularly adverse long-term outcomes. 

#### Short-Term Horizons: Operational Feasibility and Real-Time Dispatch

Short-term models address tactical questions over horizons of minutes to days. Their purpose is to determine the most cost-effective and physically feasible way to operate the existing energy infrastructure to meet demand in real-time.

*   **Decision Variables**: The key decisions are **operational** or **recourse** actions ($x_t$) that are made on a continuous, rolling basis as new information becomes available. These include **Unit Commitment (UC)** (which generators to turn on or off), **Economic Dispatch (ED)** (the power output of each online generator), the charging and discharging of energy storage, and the procurement of [ancillary services](@entry_id:1121004) like [operating reserves](@entry_id:1129146).  

*   **Constraints and Objectives**: The focus is on minute-by-minute physical feasibility and security. Constraints must be chronologically detailed, enforcing power balance at each time step, respecting the technical limits of generators such as **ramping rates** (e.g., $|p_{i,t} - p_{i,t-1}| \le R_{i}$), minimum up-times and down-times, and adhering to the thermal limits of the transmission network, often modeled using approximations like the **Direct Current Optimal Power Flow (DC-OPF)**. The objective is to minimize the operational cost (primarily fuel and startup costs) over the short-term horizon.

*   **Representation of Uncertainty**: Uncertainty is high-frequency and related to forecast errors. The primary sources are deviations in [variable renewable energy](@entry_id:1133712) (VRE) generation (wind and solar) and fluctuations in electricity demand. This is handled within a recourse framework, where decisions can be adjusted as uncertainty unfolds, or through methodologies like robust optimization or [chance constraints](@entry_id:166268) that ensure reliability against a set of possible forecast errors. 

### The Mechanics of Inter-temporal Coupling: State and Dynamics

The long-term and short-term horizons are not independent; they are deeply intertwined. Long-term investment decisions define the physical system within which short-term operations must take place, while the cost and feasibility of short-term operations determine the economic value of long-term investments. This coupling is formally captured by the concept of a **state vector**.

In a discrete-time dynamic system, the **state vector** ($x_t$) is the minimal set of information at a time $t$ that is required to fully determine the system's future evolution, given subsequent decisions and external inputs. Variables that must be carried from one period to the next are called **horizon-coupling states**; they are the glue that binds the timeline together. Variables that can be determined entirely within a single period, based on the current state and inputs, are considered **local** or **control variables** .

The key horizon-coupling state variables in energy systems include:

*   **Physical Stocks**: These represent inventories of conserved quantities. The state-of-charge ($s_t$) of a storage device, the volume of water in a hydropower reservoir, or the amount of fuel in a stockpile all carry over from one period to the next according to physical conservation laws.  

*   **Capital Stocks**: The vector of installed capacities ($k_t$) for generation, storage, and transmission is a fundamental state variable. This stock evolves slowly over the long-term horizon through investment and retirement decisions. It acts as a primary constraint on the feasible set of short-term operational decisions. 

*   **Operational Memory**: The technical limitations of conventional generators create path-dependency. To enforce minimum up-time and down-time constraints, the model must know the unit's on/off status in the previous period ($y_{t-1}$) and how long it has been in that state ($\tau^{\text{on}}_{t-1}, \tau^{\text{off}}_{t-1}$). Similarly, to enforce [ramping constraints](@entry_id:1130532), the power output of the previous period ($g_{t-1}$) must be known. These variables constitute the "memory" of the operational state. 

*   **Cumulative Stocks**: Long-term policies often impose budgets on cumulative quantities. A prime example is a cap on total greenhouse gas emissions over a multi-year period. To ensure compliance, the total emissions accumulated up to period $t$ ($e_t$) must be tracked as a state variable. 

To illustrate how these dynamics are formalized, consider the evolution of the capital stock. If we let $K_{i,t}$ be the new capacity of technology $i$ (with a fixed lifetime of $L_i$ periods) commissioned in period $t$, the total available capacity $C_{i,t}$ is the sum of all vintages that are still operational. This can be expressed in two mathematically equivalent ways :

1.  **Convolution Sum**: This formulation directly sums the capacity investments over a rolling window of the past $L_i$ periods:
    $$ C_{i,t} = \sum_{\tau = t - L_i + 1}^{t} K_{i,\tau} $$

2.  **Recursive Stock-Balance Equation**: This formulation updates the stock from the previous period by adding new investments and subtracting retiring assets:
    $$ C_{i,t} = C_{i,t-1} + K_{i,t} - K_{i,t-L_i} $$
    Here, the term $K_{i,t-L_i}$ represents the capacity vintage that was commissioned $L_i$ periods ago and is now retiring. Both formulations describe the same physical process and are fundamental to long-term [capacity expansion models](@entry_id:1122042).

### Bridging Horizons: Aggregation, Decomposition, and Valuation

The computational burden of a fully detailed, multi-decade model is prohibitive. This necessitates methods for simplifying the problem and linking specialized models.

#### The Fundamental Trade-off: Resolution versus Tractability

The core challenge stems from the relationship between the planning horizon length ($H$), the [temporal resolution](@entry_id:194281) or time-step size ($\Delta t$), and the total number of time periods in the model ($T$). For a uniform discretization, $T = H / \Delta t$. The model's size—its number of variables and constraints—scales directly with $T$. Finer resolution (smaller $\Delta t$) provides a more accurate numerical approximation of [continuous dynamics](@entry_id:268176) (e.g., storage level integration or generator ramping) but exponentially increases the computational effort, especially for models with integer variables like unit commitment. This forces a trade-off: a long horizon requires a coarse resolution, while a fine resolution necessitates a short horizon .

#### Temporal Aggregation and Its Consequences

To make long-term models computationally tractable, a common technique is **[temporal aggregation](@entry_id:1132908)**, where the full chronological sequence of hours in a year is replaced by a small number of **[representative periods](@entry_id:1130881)** (e.g., a "typical sunny weekday," "typical cloudy weekend," etc.). While this dramatically reduces model size, it comes at the cost of breaking the chronological links between time steps, which can introduce significant biases .

*   **Loss of Serial Correlation and Storage Valuation**: Real-world electricity prices exhibit strong **serial correlation** (autocorrelation), meaning the price in one hour is a good predictor of the price in the next. This creates arbitrage opportunities over multiple hours or days. Representative period models, by decoupling periods, destroy this correlation across period boundaries. For example, a model with separate "representative weekdays" and "representative weekends" cannot capture the value of a long-duration storage device that charges on a low-priced weekend and discharges on a high-priced weekday. This typically leads to a systemic **undervaluation** of energy storage, particularly long-duration technologies. 

*   **Violation of Chronological Constraints**: Inter-temporal constraints that span across the boundaries of [representative periods](@entry_id:1130881) are ignored. For instance, a model might schedule a generator to shut down at the end of one representative day and start up at the beginning of the next. In reality, this could correspond to a downtime of only a few hours, violating a minimum down-time constraint. By ignoring these links, the model overestimates the operational flexibility of the system and may underestimate its total cost. 

#### Valuation and Feedback Mechanisms

A sophisticated modeling framework involves a **bidirectional information flow** between long-term and short-term models, often implemented via decomposition techniques.

*   **Feed-Forward**: The long-term investment model makes strategic decisions (e.g., how much solar capacity to build). These decisions are then passed as fixed parameters (i.e., the available capacity) to the short-term operational model. 

*   **Feedback**: The short-term model is simulated with this fixed capacity under various operating conditions. The results of these simulations provide crucial economic feedback to the investment model. The most important feedback signals are the **[dual variables](@entry_id:151022)** (or shadow prices) of the short-term optimization problem.
    *   The dual variable on the power balance constraint represents the marginal cost of supplying an additional unit of energy at a specific time and location—the **Locational Marginal Price (LMP)**. The expected LMP over time is a primary indicator of operational costs and signals the profitability of building new, cheaper generation.
    *   The dual variable on a generator's capacity constraint represents the marginal value of having an extra unit of that capacity available, often called the **[capacity value](@entry_id:1122050)**.
    *   By iterating between the models, passing capacity decisions down and economic signals up, this decomposition approach seeks a consistent equilibrium between investment and operation. 

### Advanced Topics in Horizon Design

Building robust and unbiased multi-horizon models requires attention to several advanced but critical details related to uncertainty and economic valuation.

#### Long-Term Uncertainty and Non-Anticipativity

Long-term uncertainties are often represented using a **scenario tree**, where the path from the root to a leaf represents one possible future evolution of uncertain parameters (e.g., fuel prices). When optimizing over such a tree, a critical principle that must be enforced is **non-anticipativity**. This ensures that a decision made at any point in time is based only on information that would have been available at that time, and not on future knowledge.

Mathematically, non-anticipativity is enforced by adding constraints that force the decision variables to be identical for any scenarios that share the same history up to that decision point. For example, consider a scenario tree where two scenarios, $\omega^1$ and $\omega^2$, are indistinguishable at stage $t=2$ (i.e., they pass through the same node). The non-anticipativity constraint for a decision variable $u_2$ would be $u_2(\omega^1) = u_2(\omega^2)$. At the root node ($t=1$), all scenarios are indistinguishable, so the initial investment decision must be a single value across all scenarios. These constraints ensure that the resulting policy is implementable in reality. 

#### Economic Valuation: Discounting and End-of-Horizon Effects

Comparing costs and revenues that occur at different points in time requires a consistent valuation framework. The standard approach is **Net Present Value (NPV)**, where future cash flows are discounted to a common point in time, usually the present. A cash flow $C_t$ occurring in year $t$ is discounted using a discount factor $d_t = (1+r)^{-t}$, where $r$ is the [discount rate](@entry_id:145874). The NPV is then $\sum_{t=0}^{T} d_t C_t$. This framework is essential for making rational trade-offs, such as the decision to invest in a technology now versus waiting for its cost to decline due to [technological learning](@entry_id:1132886) .

When using a finite planning horizon $T$, a significant source of bias arises from the **end-of-horizon effect** or **truncation bias**. An investment model with a horizon ending at year $T$ will not see any of the benefits or costs that occur after $T$. This systematically biases the model against long-lived assets. An asset with a 40-year life built in year $T-5$ would appear to have only a 5-year operational life, making it seem economically unattractive.

To counteract this, a **salvage value** (or terminal value) is added to the objective function. This term represents the residual economic value of assets at the end of the horizon. A common approximation, assuming linear depreciation of value, calculates the salvage capacity $S_i(T)$ of an asset $i$ with lifetime $L_i$ and capacity $K_i$ commissioned at time $t_i$ as:
$$ S_i(T) = \frac{L_i - (T - t_i)}{L_i} K_i $$
This represents the fraction of the asset's useful life that remains beyond the horizon, multiplied by its capacity. Including this term ensures that investment decisions made near the end of the horizon are evaluated more accurately. 

#### Hybrid Risk Preferences Across Horizons

The nature of uncertainty differs across horizons, and so might a decision-maker's attitude towards it. A sophisticated approach may employ different [risk modeling](@entry_id:1131055) paradigms for different time scales.

*   For long-term planning, where uncertainty is represented by probabilistic scenarios, **[stochastic programming](@entry_id:168183)**—which aims to minimize the expected total cost—is a common and suitable choice.

*   For short-term operations, the primary goal is often ensuring reliability against any realization of forecast error within a plausible range. Here, **[robust optimization](@entry_id:163807)** is a powerful alternative. Instead of minimizing expected cost, it minimizes the worst-case cost over a defined uncertainty set $\mathcal{U}$.

These two perspectives can be combined in a hybrid objective function. For a first-stage investment decision $x$, the total cost can be a weighted sum of the capital cost, the worst-case short-term operational cost, and the expected long-term operational cost:
$$ \min_{x} f(x) + \lambda \left( \sup_{\xi_{s} \in \mathcal{U}} \min_{y_{s}} c_{s}(x, y_s; \xi_s) \right) + (1-\lambda) \left( \mathbb{E}_{\omega \sim \mathbb{P}} \left[ \min_{y_{\ell}} c_{\ell}(x, y_{\ell}; \omega) \right] \right) $$
The weighting parameter $\lambda \in [0,1]$ allows the planner to explicitly trade off between prioritizing long-term economic efficiency (low $\lambda$) and guaranteeing short-term operational robustness (high $\lambda$). This hybrid approach provides a richer framework for navigating the complex uncertainties inherent in energy system planning. 