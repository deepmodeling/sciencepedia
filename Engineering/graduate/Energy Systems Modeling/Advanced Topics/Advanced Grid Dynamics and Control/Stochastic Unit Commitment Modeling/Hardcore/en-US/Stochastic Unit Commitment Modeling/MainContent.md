## Introduction
The increasing integration of [variable renewable energy](@entry_id:1133712) sources like wind and solar power introduces significant uncertainty into power system operations, challenging traditional planning methods. Deterministic unit commitment, which relies on a single forecast, is often insufficient to guarantee reliable and cost-effective grid management in this new paradigm. Stochastic Unit Commitment (SUC) modeling emerges as a powerful solution, offering a robust framework for making operational decisions under uncertainty. This article provides a comprehensive exploration of SUC, designed to equip you with both theoretical knowledge and practical skills.

The following chapters will guide you through this advanced topic. In "Principles and Mechanisms," you will learn the foundational [two-stage stochastic programming](@entry_id:635828) structure, the mathematical formulation of SUC, and how uncertainty is formally represented. Next, "Applications and Interdisciplinary Connections" will broaden this perspective, exploring how SUC is used to manage system flexibility, integrate energy storage and [demand response](@entry_id:1123537), and connect with fields like economics and finance. Finally, the "Hands-On Practices" section will allow you to apply these concepts, solidifying your understanding by building and analyzing SUC models to solve practical operational problems.

## Principles and Mechanisms

The transition from deterministic to stochastic unit commitment represents a fundamental shift in power system operational planning, moving from optimization against a single, assumed-certain future to a more robust paradigm of [optimization under uncertainty](@entry_id:637387). This chapter elucidates the core principles and mechanisms underpinning Stochastic Unit Commitment (SUC), providing a formal basis for its formulation, interpretation, and application. We will begin with the foundational two-stage model, explore the representation of uncertainty and information, assess the economic value of the stochastic approach, and conclude with advanced modeling features and computational considerations.

### The Two-Stage Stochastic Programming Framework

At its heart, the SUC problem is an application of **[two-stage stochastic programming](@entry_id:635828)**. This framework is designed for situations where decisions must be made in stages, with uncertainty being resolved between them. It elegantly captures the temporal reality of power system operations: certain binding decisions must be made in advance (e.g., day-ahead), while other operational adjustments can be made in real-time as conditions become known.

The decisions are partitioned into two categories:

1.  **First-Stage Decisions**: These are the **here-and-now** decisions made *before* the uncertainty is realized. They are fixed and binding across all possible future outcomes. In the context of unit commitment, the primary first-stage decisions are the binary variables that determine the commitment status of thermal generating units—whether a unit is turned on or off, and consequently, if it is starting up or shutting down. These decisions must be **nonanticipative**, meaning they cannot depend on future information that is not yet available. Mathematically, this is enforced by defining these variables to be identical across all scenarios .

2.  **Second-Stage Decisions**: These are the **recourse** or **wait-and-see** decisions made *after* a specific outcome of the uncertain variables (a "scenario") is realized. These decisions are adaptive and can differ from one scenario to another. For SUC, the principal recourse decisions are the continuous power dispatch levels of the committed generators. The system operator adjusts these dispatch levels in real-time to balance supply and demand for the specific conditions that have materialized.

The objective of the SUC model is to select the first-stage commitment decisions that minimize the total expected cost. This cost comprises the certain first-stage commitment costs (e.g., start-up and no-load costs) plus the probability-weighted average of the second-stage operational costs (e.g., fuel and variable O&M costs) across all considered scenarios.

#### Formalizing the Two-Stage SUC Model

Let us formalize a canonical two-stage SUC model. We consider a set of thermal generating units $\mathcal{I}$, a set of time periods $\mathcal{T}$, and a finite set of scenarios $\mathcal{S}$. Each scenario $s \in \mathcal{S}$ has an associated probability $\pi_s$, where $\sum_{s \in \mathcal{S}} \pi_s = 1$.

**Decision Variables:**
-   First-stage (nonanticipative):
    -   $x_{it} \in \{0,1\}$: Commitment status of unit $i$ in period $t$ (1 if on, 0 if off).
    -   $u_{it} \in \{0,1\}$: Start-up decision for unit $i$ in period $t$.
    -   $v_{it} \in \{0,1\}$: Shut-down decision for unit $i$ in period $t$.
-   Second-stage (recourse):
    -   $p_{it}^s \ge 0$: Power dispatch of unit $i$ in period $t$ under scenario $s$.

**Objective Function:**
The goal is to minimize the sum of fixed commitment costs and the expected value of the variable generation costs:
$$
\min_{x,u,v,p} \sum_{i \in \mathcal{I}} \sum_{t \in \mathcal{T}} \left( c_i^{\text{su}} u_{it} + c_i^{\text{nl}} x_{it} \right) + \sum_{s \in \mathcal{S}} \pi_s \left( \sum_{i \in \mathcal{I}} \sum_{t \in \mathcal{T}} c_i^{\text{var}} p_{it}^s \right)
$$
where $c_i^{\text{su}}$, $c_i^{\text{nl}}$, and $c_i^{\text{var}}$ are the start-up, no-load, and variable costs for unit $i$, respectively.

**Key Constraints:**
The model is subject to several constraints that must hold for each scenario $s \in \mathcal{S}$:
1.  **Power Balance:** The total generation must meet the demand $D_t^s$ in each period $t$ of each scenario $s$.
    $$
    \sum_{i \in \mathcal{I}} p_{it}^s = D_t^s, \quad \forall t \in \mathcal{T}, s \in \mathcal{S}
    $$
2.  **Generation Limits:** The dispatch of each unit must be within its operational limits and can only be non-zero if the unit is committed. These are the crucial **coupling constraints** that link the first and second stages.
    $$
    P_i^{\min} x_{it} \le p_{it}^s \le P_i^{\max} x_{it}, \quad \forall i \in \mathcal{I}, t \in \mathcal{T}, s \in \mathcal{S}
    $$
3.  **Logical and Temporal Constraints:** The relationships between commitment, start-up, and shut-down, as well as [inter-temporal constraints](@entry_id:1126569) like minimum up/down times and [ramping limits](@entry_id:1130533), must be enforced. For instance, the start-up/shut-down logic is scenario-independent:
    $$
    x_{it} - x_{i,t-1} = u_{it} - v_{it}, \quad \forall i \in \mathcal{I}, t \in \mathcal{T}
    $$
    Ramping constraints, however, apply to the scenario-dependent dispatch variables.

This formulation ensures that a single, robust commitment schedule ($x_{it}$) is found, which is feasible and cost-effective on average, while allowing for flexible real-time dispatch ($p_{it}^s$) to handle any of the specific outcomes represented by the scenarios.

To make this concrete, consider a simple one-period problem with three units and two demand scenarios . Suppose we must decide which units to commit ($x_i$) before knowing whether demand will be high ($D^1=120$ MW with probability $0.6$) or low ($D^2=60$ MW with probability $0.4$). One possible commitment strategy is to turn on Units 1 and 2, incurring a fixed start-up cost of $C_1^{\text{SU}} + C_2^{\text{SU}} = \$1600$. If high demand occurs, these units are dispatched to meet the $120$ MW load at a variable cost of $\$2800$. If low demand occurs, they are dispatched to meet the $60$ MW load at a cost of $\$1200$. The total expected cost for this commitment is the fixed cost plus the expected variable cost: $\$1600 + 0.6(\$2800) + 0.4(\$1200) = \$3760$. The SUC model systematically evaluates all feasible commitment combinations to find the one, like this, that yields the lowest total expected cost. In this example, committing Units 1 and 2 is indeed the optimal strategy, superior to committing too little capacity (and facing shortfalls) or too much (and incurring excessive fixed costs).

### Modeling Uncertainty: Scenarios and Information Structure

The effectiveness of SUC hinges on a realistic representation of uncertainty. The model relies on a discrete set of scenarios, $\mathcal{S}$, to approximate the continuous probability distributions of uncertain parameters.

#### Sources of Uncertainty

In modern power systems, several key sources of uncertainty must be considered :
-   **Net Load:** This is the primary source of short-term uncertainty, representing the total system demand minus the output from variable renewable energy (VRE) sources like wind and solar. Forecast errors for both load and VRE contribute to its variability.
-   **Forced Outages:** Conventional generators can fail unexpectedly, leading to a sudden loss of capacity. This is a discrete, high-impact event.
-   **Fuel Prices:** The price of natural gas and other fuels can fluctuate, altering the economic merit order of dispatchable units.

These uncertainties differ in their impact. Net load and fuel price variations primarily require **dispatch recourse**—adjusting the continuous output levels of already committed units to re-balance the system or optimize economic dispatch. In contrast, a major generator outage may remove a significant block of capacity, potentially requiring **commitment recourse**—the rapid start-up of a fast-start unit that was kept offline to restore system feasibility. Advanced SUC models may use a multi-stage structure to capture this possibility.

#### Scenario Generation

A critical practical question is: where do the scenarios come from? Naive sampling can fail to capture essential statistical properties. A scientifically sound methodology is required to generate a set of scenarios that is both representative and computationally tractable.

For time-series uncertainties like wind power forecast errors, a common approach involves fitting a stochastic process model to historical forecast error data . For example, a Vector AutoRegressive Moving Average (VARMA) model can be used. The procedure is as follows:
1.  **Model Fitting:** An ARMA model is fitted to the historical forecast error residuals for each wind site. This captures the **temporal autocorrelation**—the tendency for errors at one hour to be correlated with errors in previous hours.
2.  **Innovation Covariance:** The correlations of the unpredictable "shocks" or "innovations" ($\boldsymbol{\epsilon}_t$) between different wind sites are calculated and stored in a covariance matrix $\Sigma$. This captures the **spatial cross-correlation**—the tendency for wind speeds at geographically close sites to be related.
3.  **Simulation:** To generate a new scenario, one first samples a sequence of multivariate innovation vectors $\boldsymbol{\epsilon}_t$ from a distribution (e.g., multivariate normal) with a mean of zero and covariance $\Sigma$. This is often done using a Cholesky decomposition of $\Sigma$ applied to a vector of independent random samples.
4.  **Forward Recursion:** These sampled innovations are then fed into the fitted ARMA equations, which are simulated forward in time to produce a complete, dynamically consistent scenario path that respects both the temporal and spatial correlations observed in historical data.

This process generates a large set of high-fidelity scenarios, which can then be reduced to a smaller, computationally manageable set for the SUC model using techniques that preserve key statistical properties.

### The Principle of Nonanticipativity in Multi-Stage Models

The concept of nonanticipativity is the cornerstone of stochastic programming, ensuring that decisions respect the chronological flow of information. While straightforward in the two-stage case, its generalization to multi-stage problems requires the use of a **scenario tree**.

A scenario tree represents the evolution of uncertainty over time. It starts from a single root node at the first stage and branches out at subsequent stages as uncertainty is progressively revealed. Each path from the root to a terminal leaf represents one complete scenario.

In this structure, the nonanticipativity principle states that any two scenarios that are indistinguishable up to a certain stage $t$ must have identical decisions up to that stage. In other words, if two scenario paths pass through the same node $\omega$ at stage $t$, the decisions made at that node must be the same for both paths .

To implement this in a Mixed-Integer Linear Program (MILP), nonanticipativity is enforced via explicit equality constraints. For a given node $\omega$ at stage $t$ through which a set of $k$ scenarios pass, we must ensure the decision variables at that node are equal across all $k$ scenarios. This can be achieved by choosing one scenario as a reference and adding $k-1$ equality constraints that set the variables for the other scenarios equal to the reference.

The total number of nonanticipativity constraints in a multi-stage model is the sum of these constraints over all non-leaf nodes in the tree, for all decision variables, and for all units. For a problem with $I$ units and a decision made at stage $t$ at node $\omega$ through which $|\mathcal{S}_t(\omega)|$ scenarios pass, we require $I \times (|\mathcal{S}_t(\omega)| - 1)$ constraints for that decision at that node .

The calculation of the expected cost objective in a multi-stage model also follows the tree structure. Costs associated with decisions at a particular node are weighted by the probability of reaching that node. The total expected cost is the sum of these probability-weighted costs over all nodes in the tree, or equivalently, the sum of total scenario costs weighted by the probabilities of the terminal leaves .

### Assessing the Value of Stochastic Modeling

Implementing SUC is more complex than traditional deterministic methods. Therefore, it is crucial to quantify its benefits. Decision theory provides two key metrics for this purpose: the Value of the Stochastic Solution (VSS) and the Expected Value of Perfect Information (EVPI).

#### The Value of the Stochastic Solution (VSS)

The VSS measures the economic benefit of using the SUC model compared to a simpler deterministic approach. The most common deterministic baseline is the **Expected Value (EV) problem**, where uncertain parameters are replaced by their expected values, and a deterministic unit commitment is solved. The resulting commitment schedule is then evaluated under the true scenario distribution to find its expected cost, $z^{\text{E}}$. The VSS is the difference between this cost and the optimal cost from the SUC model, $z^{\text{S}}$ .

$$
\text{VSS} = z^{\text{E}} - z^{\text{S}}
$$

A positive VSS represents the savings achieved by explicitly modeling uncertainty. The VSS tends to be large under three conditions:
1.  **High Uncertainty:** When the spread of possible outcomes is wide, the expected value is a poor representation of any single realization. Decisions optimized for the "average" case may perform very poorly in extreme but plausible scenarios.
2.  **Inflexible First-Stage Decisions:** Commitment decisions are costly and often irreversible in the short term. A poor commitment made day-ahead cannot be easily fixed in real-time. The SUC model proactively selects a more robust commitment that provides the necessary flexibility for the recourse stage.
3.  **Highly Nonlinear Recourse Costs:** If the cost of adapting to a scenario is nonlinear, the EV solution will be suboptimal. A prime example is the use of a very high Value of Lost Load (VOLL) to penalize energy shortfalls. The EV solution might not commit enough capacity, leading to frequent and costly load shedding in low-generation scenarios. The SUC solution, by minimizing expected cost, will naturally hedge against these high-cost events by committing more capacity, even if it increases the fixed costs .

In a system where a deterministic plan results in an expected cost of $\$24.4$ million due to massive load-shedding penalties in low-wind scenarios, an SUC solution might find a commitment that costs only $\$6.47$ million in expectation. The resulting VSS of nearly $\$18$ million highlights the immense value of hedging against low-probability, high-impact events.

#### The Expected Value of Perfect Information (EVPI)

The EVPI quantifies the "cost of uncertainty" itself. It is defined as the difference between the optimal SUC cost ($z^{\text{S}}$) and the expected cost of a hypothetical **wait-and-see (WS)** or clairvoyant solution ($z^{\text{WS}}$). The WS solution is found by calculating the optimal commitment and dispatch for each scenario *as if it were known in advance*, and then taking the probability-weighted average of these perfect-foresight costs.

$$
\text{EVPI} = z^{\text{S}} - z^{\text{WS}}
$$

Operationally, the EVPI represents the maximum amount of money a system operator should be willing to pay for a perfect forecast . For instance, if the SUC cost is $\$13.72$ million and the clairvoyant cost is $\$13.41$ million, the EVPI is $\$0.31$ million. This value serves as an economic upper bound on investments in better forecasting technology or other information-gathering activities. No information, no matter how accurate, can provide more value than the EVPI.

### Advanced Modeling and Computational Complexity

While the two-stage model is foundational, practical SUC formulations often incorporate greater detail and face significant computational challenges.

#### Detailed Decision Hierarchy

In electricity markets, the decision hierarchy is more granular. Day-ahead (first-stage) decisions often include not just unit commitment ($u_{g,t}$) but also a financially binding energy preschedule ($p_{g,t}^{DA}$) and the procurement of ancillary service capacity, such as up- and down-reserves ($R^{\uparrow}_{g,t}, R^{\downarrow}_{g,t}$). The real-time (second-stage) recourse actions then involve not only energy redispatch ($\Delta p_{g,t,s}$) but also the actual deployment of those reserves ($\rho^{\uparrow}_{g,t,s}, \rho^{\downarrow}_{g,t,s}$) to balance the grid .

#### The Curse of Dimensionality

The most significant barrier to the practical application of SUC is its computational complexity. In the standard **scenario-expanded formulation**, a full set of decision variables is created for each scenario. This leads to a dramatic increase in the size of the resulting MILP.

Let's consider the size of a multi-stage SUC model with $|\mathcal{I}|$ units, $|\mathcal{T}|$ time periods, and $|\mathcal{S}|$ scenarios, where all variables are indexed by scenario .
-   **Number of Binary Variables ($N_{\text{bin}}$):** With three binary variables per unit-period ($x, u, v$), the total count is $N_{\text{bin}} = 3 |\mathcal{I}| |\mathcal{T}| |\mathcal{S}|$.
-   **Number of Continuous Variables ($N_{\text{cont}}$):** With three continuous variables ($p, r^+, r^-$), the count is $N_{\text{cont}} = 3 |\mathcal{I}| |\mathcal{T}| |\mathcal{S}|$.
-   **Number of Constraints ($N_{\text{con}}$):** The number of constraints also scales linearly with $|\mathcal{S}|$, for example, $N_{\text{con}} \approx (7 |\mathcal{I}| |\mathcal{T}|) |\mathcal{S}|$ for a typical formulation.

The true challenge lies in the exponential nature of solving MILPs. The complexity of the branch-and-bound algorithm, used by commercial solvers, is, in the worst case, exponential in the number of binary variables. If we model the number of explored nodes as $N_{\text{nodes}} = \beta^{N_{\text{bin}}}$ for some base $\beta > 1$, we see that:
$$
N_{\text{nodes}}(\beta) = \beta^{3 |\mathcal{I}| |\mathcal{T}| |\mathcal{S}|} = (\beta^{3 |\mathcal{I}| |\mathcal{T}|})^{|\mathcal{S}|}
$$
This expression shows that the computational effort grows exponentially with the number of scenarios. This phenomenon, known as the **curse of dimensionality**, is the primary reason that SUC models are often limited to a few dozen or hundred scenarios and why significant research is devoted to decomposition algorithms (e.g., Benders decomposition, Progressive Hedging) that can solve problems with many more scenarios by breaking them into smaller, more manageable pieces.