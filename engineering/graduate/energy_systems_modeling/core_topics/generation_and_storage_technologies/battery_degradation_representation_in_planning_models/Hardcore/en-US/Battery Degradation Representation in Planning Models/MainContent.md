## Introduction
The increasing reliance on battery energy storage systems for [grid stability](@entry_id:1125804), [renewable energy integration](@entry_id:1130862), and economic arbitrage has made their long-term performance and economic viability a critical concern. A battery is not a static asset; it degrades with time and use, leading to a decline in capacity and efficiency. The central challenge for planners and operators is to translate the complex electrochemical and physical processes of degradation into models that are both accurate enough to be meaningful and simple enough to be used within [large-scale optimization](@entry_id:168142) and control frameworks. This article addresses this knowledge gap by providing a comprehensive overview of how battery degradation is represented in modern energy system planning models.

This guide is structured to build your understanding progressively. The first chapter, **"Principles and Mechanisms,"** lays the groundwork by explaining the fundamental phenomena of capacity fade and resistance growth, defining key metrics like State-of-Health (SOH), and describing the core mathematical models for calendar and cycling aging. The second chapter, **"Applications and Interdisciplinary Connections,"** demonstrates how these models are deployed in the real world to solve problems in economic optimization, strategic asset management, and decision-making under uncertainty, highlighting connections to fields like control theory and AI. Finally, the **"Hands-On Practices"** section provides practical exercises to apply these concepts, from building a simple two-factor degradation model to developing a convex surrogate for a complex non-linear cost function.

## Principles and Mechanisms

The accurate representation of battery degradation is a cornerstone of effective energy system planning and operation. While the underlying electrochemical processes are complex, they manifest as macroscopic changes in battery performance that can be observed, quantified, and modeled. This chapter delineates the fundamental principles governing [battery degradation](@entry_id:264757) and describes the primary mechanisms through which these principles are translated into mathematical formulations suitable for planning models.

### Fundamental Degradation Phenomena

At the macroscopic level, the cumulative effects of electrochemical aging in [lithium-ion batteries](@entry_id:150991) are primarily observed as two distinct but interrelated phenomena: **[capacity fade](@entry_id:1122046)** and **internal resistance growth**. Understanding these two effects is the first step in constructing a robust degradation model. 

**Capacity fade** is the irreversible loss of the battery's ability to store and deliver charge. It is a direct consequence of physical and chemical changes within the cell, such as the loss of active electrode material, structural disordering of the electrodes, or the loss of mobile lithium ions to parasitic side reactions. In a planning model, this phenomenon is captured by a time-dependent usable capacity function, denoted as $Q(t)$. This function represents the maximum amount of charge (or energy, assuming a nominal voltage) that a battery can deliver when discharged from a fully charged state. Capacity fade is experimentally quantified by performing a full discharge test at a controlled reference current and temperature. The total charge delivered before the terminal voltage reaches its lower cutoff limit, $V_{\min}$, is measured. A decrease in this value over time signifies [capacity fade](@entry_id:1122046). In a planning context, a shrinking $Q(t)$ directly reduces the total energy a battery can provide, shortening its discharge duration at a given power level.

**Internal resistance growth**, conversely, refers to the increase in the battery's opposition to the flow of electric current. This increased resistance arises from phenomena such as the growth of resistive films on electrode surfaces (most notably the Solid-Electrolyte Interphase, or SEI), degradation of the electrolyte, or loss of electrical contact between active material particles. This is represented by a time-dependent internal resistance function, $R(t)$. The primary consequence of increased resistance is a larger voltage drop (or overpotential) during operation, governed by Ohm's Law. The terminal voltage $V(t)$ of a simplified battery model is given by $V(t) = V_{\mathrm{OC}}(\mathrm{SOC}(t)) - I(t) R(t)$, where $V_{\mathrm{OC}}$ is the open-circuit voltage and $I(t)$ is the current. Internal resistance is quantified by measuring this voltage drop. A common method is a current-step test, where a sudden current pulse $I_{\mathrm{pulse}}$ is applied, and the instantaneous voltage change $\Delta V$ is measured. The resistance is then calculated as $R(t) = \Delta V / I_{\mathrm{pulse}}$.

The impacts of a growing $R(t)$ are twofold. First, it reduces **[round-trip efficiency](@entry_id:1131124)**, as a greater amount of energy is dissipated as heat, given by the Joule heating loss term $P_{\mathrm{loss}}(t) = I(t)^2 R(t)$. Second, it constrains the battery's **power capability**. Because the battery's operating voltage must remain within a specified window $[V_{\min}, V_{\max}]$, a higher internal resistance means that the voltage limits are reached at a lower current. Since power is a function of current, this effectively reduces the maximum charge and discharge power the battery can sustain.

### Quantifying Battery State and Degradation

To build mathematical models of degradation, we must first define precise metrics for the battery's state and its usage.

#### State-of-Health and State-of-Charge

Two fundamental quantities describe the battery's condition at any given time: **State-of-Health (SOH)** and **State-of-Charge (SOC)**.

The **State-of-Health (SOH)** is a normalized measure of the battery's current condition relative to its fresh state. While SOH can be a composite metric, in the context of capacity-centric planning models, it is most commonly defined as the ratio of the current usable capacity $Q_t$ to the initial (or nominal) capacity $Q_0$:
$$SOH_t = \frac{Q_t}{Q_0}$$
An SOH of $1$ represents a new battery, while a lower value indicates degradation. For example, a battery is often considered to be at its end-of-life for grid applications when its SOH reaches $0.8$. 

The **State-of-Charge (SOC)** represents the current level of charge in the battery. Critically, it is defined as the ratio of the stored energy $e_t$ to the *current* usable capacity $Q_t$:
$$SOC_t = \frac{e_t}{Q_t}$$
This distinction is crucial. As the battery degrades and $Q_t$ decreases, the absolute amount of energy corresponding to a given SOC level also decreases. For instance, an SOC of $0.9$ in a degraded battery represents less stored energy than an SOC of $0.9$ in a new battery. Operational constraints are typically specified in terms of an admissible SOC window, such as $SOC_{\min} \le SOC_t \le SOC_{\max}$. This directly translates to state-dependent bounds on the stored energy: $SOC_{\min} Q_t \le e_t \le SOC_{\max} Q_t$. As $Q_t$ shrinks, this feasible energy window also tightens. 

#### Quantifying Usage: Throughput and Equivalent Full Cycles

To model degradation caused by usage (cycling), we must quantify that usage. The two most common metrics are cumulative throughput and Equivalent Full Cycles.

**Cumulative throughput**, denoted here by $z$, measures the total amount of energy processed by the battery. For a discrete-time model with power dispatch $P_t$ over time steps of length $\Delta t$, the one-way throughput is the sum of the absolute energy charged or discharged. Assuming perfect efficiency for simplicity, the change in SOC is $\Delta s_t = -P_t \Delta t / Q_0$. The normalized throughput in that step is $|\Delta s_t| = |P_t| \Delta t / Q_0$. The cumulative throughput over a horizon is the sum of these incremental changes:
$$z = \sum_{t} \frac{|P_t| \Delta t}{Q_0} = \sum_{t} |s_{t+1} - s_t|$$
This metric represents the total "path length" traveled by the SOC. 

**Equivalent Full Cycles (EFC)** is a more nuanced metric derived from cycle counting. It recognizes that a single deep cycle is more damaging than many shallow cycles that process the same total energy. A formal cycle counting algorithm, such as the Rainflow method, decomposes the SOC trajectory into a set of individual cycles, each with a specific depth $d_i$. The EFC is then defined as the sum of these cycle depths:
$$\mathrm{EFC} = \sum_i d_i$$
Under the idealizing assumptions of perfect efficiency and a trajectory that starts and ends at the same SOC, there is a direct relationship between these two metrics. The total charge throughput $z$ accounts for both charging and discharging flows. For a closed trajectory, the total energy charged must equal the total energy discharged. The EFC, which is equivalent to the sum of all charge events (the total "rise" of the SOC), represents one-way throughput. Therefore, the total two-way throughput is exactly twice the EFC:
$$z = 2 \cdot \mathrm{EFC}$$
This simple identity is foundational for relating throughput-based degradation models to cycle-based models. 

### Mechanistic Models of Capacity Fade

With quantitative metrics established, we can formulate models that describe how capacity $Q_t$ evolves in response to time and usage. A standard and powerful approach is to decompose degradation into two primary components: calendar aging and cycling aging. 

#### Decomposing Degradation: Calendar vs. Cycling Aging

**Calendar aging** encompasses all degradation mechanisms that occur over time, regardless of whether the battery is being used. It is primarily driven by temperature and, to a lesser extent, state of charge. The dominant mechanism is the slow growth of the SEI layer on the negative electrode, which consumes lithium ions and increases impedance. In planning models, this is often represented as a capacity loss rate that depends on time. A common, mechanistically-grounded model for diffusion-limited SEI growth posits that capacity loss is proportional to the square root of time, $\sqrt{t}$. 

**Cycling aging** refers to degradation induced by the charging and discharging processes themselves. These mechanisms include mechanical stress from the expansion and contraction of electrode materials, [lithium plating](@entry_id:1127358) at high charge rates, and other potential-dependent side reactions. This component is modeled as a function of usage, typically quantified by the number and depth of cycles.

Assuming these two sets of mechanisms are quasi-independent, a common approach is to model the total [capacity fade](@entry_id:1122046) as the sum of the calendar and cycling components. For a given time horizon $t$ and a sequence of cycles with depths $\{d_i\}$, the capacity can be written as:
$$Q(t) = Q_0 - g_{\mathrm{cal}}(t, T) - g_{\mathrm{cyc}}(\{d_i\})$$
where $g_{\mathrm{cal}}$ is the calendar aging loss function and $g_{\mathrm{cyc}}$ is the cycling aging loss function. 

#### Temperature Dependence: The Arrhenius Law

Electrochemical reaction rates, including those responsible for degradation, are highly sensitive to temperature. This dependence is captured by the **Arrhenius law**, which states that the rate constant $k$ of a [thermally activated process](@entry_id:274558) varies with [absolute temperature](@entry_id:144687) $T$ (in Kelvin) as:
$$k(T) = k_0 \exp\left(-\frac{E_a}{R T}\right)$$
Here, $E_a$ is the activation energy of the process, $R$ is the universal gas constant, and $k_0$ is a pre-exponential factor. Since $E_a > 0$, the rate $k(T)$ increases with temperature.

This principle is applied to both aging components, although they may have distinct activation energies. For a discrete planning period $p$ with duration $\Delta t_p$ and temperature $T_p$, the fractional capacity loss from calendar aging, $\Delta\phi_{p, \mathrm{cal}}$, can be modeled as proportional to time, with an Arrhenius rate:
$$\Delta\phi_{p, \mathrm{cal}} = k_{0,\mathrm{cal}} \exp\left(-\frac{E_{a,\mathrm{cal}}}{R T_p}\right) \Delta t_p$$
Similarly, the loss from cycling, $\Delta\phi_{p, \mathrm{cyc}}$, can be modeled as proportional to the number of equivalent full cycles $N_p$, with its own temperature dependence:
$$\Delta\phi_{p, \mathrm{cyc}} = k_{0,\mathrm{cyc}} \exp\left(-\frac{E_{a,\mathrm{cyc}}}{R T_p}\right) N_p$$
The total fractional loss in the period is the sum: $\Delta \phi_p = \Delta \phi_{p, \mathrm{cal}} + \Delta \phi_{p, \mathrm{cyc}}$. This formulation provides a dimensionally consistent and physically grounded way to incorporate temperature effects into a planning model. 

#### Stress Factors in Cycling Aging

Cycling aging is not merely a function of the number of cycles; it is strongly influenced by how those cycles are performed. The two most critical stress factors are cycle depth and C-rate.

The effect of **cycle depth** is captured using the **Palmgren–Miner [linear damage accumulation](@entry_id:195991) rule**, borrowed from materials fatigue science. This rule posits that the total damage is the sum of the damage incurred in each individual cycle. If a battery can withstand $N(d)$ cycles of a constant depth $d$ before failure, the damage per cycle is $1/N(d)$. A cycle stress function, $f(d)$, is defined to be proportional to this damage, $f(d) \propto 1/N(d)$. Since deeper cycles are more damaging, $N(d)$ is a decreasing function of $d$, making $f(d)$ an increasing function. A widely used empirical fit for cycle life is the power law $N(d) \propto d^{-\beta}$, which leads to a convex power-law stress function:
$$f(d) = \alpha d^{\beta}$$
where $\alpha > 0$ and $\beta > 1$ are empirical constants. The total cycling wear is then the sum over all cycles identified in the trajectory: $\sum_i f(d_i)$. 

The **C-rate**, defined as the power normalized by the battery's energy capacity ($C_r = |P_t|/Q_t$), is another critical stress factor. High C-rates induce large reaction overpotentials, which accelerate parasitic side reactions like SEI growth and can trigger [lithium plating](@entry_id:1127358), a particularly damaging mechanism. The relationship between current density (proportional to C-rate) and overpotential is highly nonlinear, as described by the Butler-Volmer equation. This implies that degradation should "accelerate" with C-rate. A degradation stress proxy, $g(C_r)$, should therefore be a monotonically increasing and **convex** function of the C-rate. Linear models like $g(C_r) = \kappa C_r$ fail to capture this acceleration. Physically consistent functional forms include a power law, $g(C_r) = \kappa C_r^b$ with $b>1$, or an [exponential function](@entry_id:161417), $g(C_r) = \kappa (\exp(\beta C_r) - 1)$, which is directly motivated by [electrochemical kinetics](@entry_id:155032). 

### Integrating Degradation into Planning Models

The physical principles and mechanistic models described above must be translated into a form compatible with [mathematical optimization](@entry_id:165540). This is typically achieved in one of two ways: by representing degradation as an economic cost in the objective function, or by modeling it as a dynamic constraint on the battery's state.

#### Formulating Degradation as a Cost

In many planning models, especially those focused on economic dispatch or investment, it is convenient to represent battery wear as a marginal cost of use. This approach linearizes the long-term cost of replacement and appends it to the short-term operational cost objective. The key is to define a **marginal cost-of-use**, $\lambda$.

This parameter can be derived from the battery's total replacement cost, $C^{\mathrm{rep}}$, and its [expected lifetime](@entry_id:274924), quantified either as a total number of Equivalent Full Cycles, $L$, or a total energy throughput, $X^{\mathrm{life}}$. By amortizing the total replacement cost over the total lifetime service, we arrive at the marginal cost. If using EFC accounting, the cost per EFC is:
$$\lambda = \frac{C^{\mathrm{rep}}}{L} \quad (\text{in } \$/\text{EFC})$$
If using throughput accounting, the cost per unit of energy is:
$$\lambda = \frac{C^{\mathrm{rep}}}{X^{\mathrm{life}}} \quad (\text{in } \$/\text{MWh})$$
This marginal cost $\lambda$ is then multiplied by the usage metric in each period, $y_t$, to form an additive wear cost term, $\sum_t \lambda y_t$, in the optimization objective. This technique effectively translates a future, discrete replacement event into a continuous, present-day cost that the model can trade off against other operational costs. 

#### Formulating Degradation as State Dynamics

An alternative and often more physically detailed approach is to model the capacity $Q_t$ as a state variable that evolves over time according to a degradation rule. A common linear formulation for a time step $\Delta t$ is:
$$Q_{t+1} = Q_t - \phi z_t - \psi k(T_t) \Delta t$$
Here, the capacity is reduced by a cycling component proportional to the throughput in the period, $z_t$, and a calendar component proportional to the time duration $\Delta t$, scaled by a temperature factor $k(T_t)$. The parameters $\phi$ and $\psi$ are calibrated from experimental data. 

This formulation creates a crucial time-coupling in the planning model. The decision to charge or discharge the battery at time $t$ (which determines $z_t$) directly impacts the available capacity $Q_{t+1}$ in the subsequent period. This, in turn, constrains future operations through two key state-dependent constraints:
1.  **Energy Limit:** The storable energy is bounded by the current capacity: $0 \le E_t \le Q_t$.
2.  **Power Limit:** The maximum power capability scales with capacity: $|P_t| \le \bar{P} \cdot (Q_t / Q_0)$, where $\bar{P}$ is the nameplate power of the new battery.

The joint effect of these constraints is that the [feasible operating region](@entry_id:1124878) for the battery (in terms of power and energy) dynamically shrinks as it degrades. A dispatch schedule that is feasible for a new battery may become infeasible over time as the battery ages. This state-dependent formulation correctly captures the physical reality that a degraded battery is less powerful and stores less energy, ensuring that the model's solutions remain physically viable over the entire planning horizon. The full set of [linear constraints](@entry_id:636966) forms a time-coupled [convex polyhedron](@entry_id:170947). 

### Advanced Topics in Degradation Modeling

While the models discussed provide a robust foundation, several advanced considerations arise when seeking higher fidelity or analyzing the theoretical properties of these models.

#### Cycle Counting and the Challenge of Convexity

The most accurate method for quantifying cycle fatigue is the **Rainflow counting algorithm**. This standardized method (ASTM E1049) processes the time series of SOC [local extrema](@entry_id:144991) (peaks and valleys) and, through a range-ordering rule, pairs them into a set of closed cycles $\{d_i\}$. The total wear is then computed using the Palmgren-Miner rule, $\sum_i f(d_i)$, where $f(d)$ is a convex stress function. 

While physically accurate, embedding the Rainflow algorithm directly into a planning optimization is exceptionally challenging. The algorithm's logic is combinatorial: which peak pairs with which valley depends on the specific sequence and magnitude of all other extrema. A small change in the SOC trajectory can cause a complete re-pairing of cycles, leading to a discontinuous jump in the total degradation cost. Formulating this pairing logic requires integer variables and complex [logical constraints](@entry_id:635151), transforming a potentially simple convex problem into a difficult Mixed-Integer Nonlinear Program (MINLP). The resulting degradation objective function is inherently **non-convex**. 

Due to this computational intractability, practitioners often resort to **[convex surrogate models](@entry_id:1123047)**. Instead of performing explicit cycle counting, these models use a proxy for degradation that is a [convex function](@entry_id:143191) of the decision variables. A common surrogate is to penalize the magnitude of SOC change at each time step:
$$J_{\mathrm{sur}}(x_{1:T}) = \sum_{t=1}^{T-1} \psi(|x_{t+1}-x_t|)$$
where $x_t$ is the SOC and $\psi(\cdot)$ is a calibrated convex function. This formulation preserves the convexity of the optimization problem, allowing for efficient solution, while still approximating the principle that larger SOC swings are more damaging. 

#### Path Dependence and the Markov Property

Cycle-based degradation models are, by their very nature, **path-dependent**. The amount of degradation incurred to reach a certain state $(SOC_t, Q_t)$ depends on the specific history of charging and discharging, not just the current state. For example, a simple half-cycle model might calculate damage upon a reversal of direction (e.g., switching from charging to discharging). The magnitude of this damage would depend on the depth of the just-completed half-cycle, which is determined by the SOC at the last reversal point, $e_t$. 

This [path dependence](@entry_id:138606) has a profound implication for control theory: the battery system is **not Markovian** in the simple state space $(SOC_t, Q_t)$. The Markov property requires that the future evolution of the system depends only on the current state, not the history. In our case, the future degradation (and thus the evolution of $Q_t$) depends on historical information like the last extremum, $e_t$, which is not contained in the state $(SOC_t, Q_t)$ alone. Two identical current states that were reached via different paths will have different future evolutions.

To restore the Markov property, one must augment the state space to include the relevant historical information. For the half-cycle model, the state would need to become $S'_t = (SOC_t, Q_t, e_t, d_t)$, where $d_t$ is the current direction of motion. While this renders the problem theoretically tractable as a Markov Decision Process (MDP), it significantly increases the dimensionality and complexity of the model, presenting a trade-off between modeling accuracy and computational feasibility. 