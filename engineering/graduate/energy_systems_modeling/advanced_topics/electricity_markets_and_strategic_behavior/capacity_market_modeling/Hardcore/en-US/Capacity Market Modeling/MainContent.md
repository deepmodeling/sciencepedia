## Introduction
Ensuring a reliable supply of electricity is paramount for a modern economy, but guaranteeing long-term grid stability presents a significant economic challenge. In many restructured power systems, traditional energy-only markets have proven insufficient to incentivize the necessary investment in generation capacity, leading to a phenomenon known as the "missing money" problem. Capacity markets have emerged as a primary solution, creating a formal mechanism to procure and pay for the resource adequacy needed to keep the lights on years into the future. This article provides a comprehensive guide to the theory and practice of modeling these critical markets.

Across the following chapters, you will gain a deep, model-based understanding of how capacity markets function. The journey begins in **Principles and Mechanisms**, where we will establish the foundational concepts of resource adequacy, from quantifying reliability with metrics like LOLE to understanding the economic drivers and auction mechanics that define the market. Next, in **Applications and Interdisciplinary Connections**, we will apply these principles to real-world challenges, such as valuing variable resources like wind and solar, analyzing market power, and integrating grid constraints. Finally, the **Hands-On Practices** chapter will allow you to solidify your knowledge by building and analyzing capacity market models yourself, connecting abstract theory to practical implementation.

## Principles and Mechanisms

This chapter delves into the core principles and mechanisms that underpin the modeling of capacity markets. We will begin by establishing the foundational concepts of [power system reliability](@entry_id:1130080), focusing on how adequacy is measured and assessed. Subsequently, we will explore the economic rationale for capacity markets, examining why they are considered a necessary component of modern [electricity market design](@entry_id:1124242). Finally, we will analyze the structure of these markets, from the construction of demand curves to the mechanics of centralized clearing.

### Foundations of Resource Adequacy Assessment

The primary function of a capacity market is to ensure **resource adequacy**, which is the ability of the electric power system to supply the aggregate electrical demand at all times. To manage and procure adequacy, we must first be able to measure it. This section introduces the key metrics and computational methods used for this purpose.

#### Quantifying System Reliability: The Loss of Load Expectation (LOLE)

The most widely accepted metric for resource adequacy is the **Loss of Load Expectation (LOLE)**. Intuitively, LOLE represents the expected number of hours or days over a given period (typically a year) during which the available generating capacity is insufficient to meet system demand. To formalize this, we turn to probability theory.

Consider a single-area power system over a planning horizon of $H$ hours. In any given hour $h$, both the system load, $L_h$, and the available generating capacity, $A_h$, are uncertain. We can model them as random variables with a [joint probability density function](@entry_id:177840) $f_{L_h, A_h}(l, a)$. A **loss-of-load event** occurs in hour $h$ if the realization of load is greater than the realization of available capacity, i.e., $L_h > A_h$.

The probability of this event in hour $h$ is known as the **Loss of Load Probability (LOLP)**. It is found by integrating the [joint density function](@entry_id:263624) over the region where load exceeds capacity:
$$
\text{LOLP}_h = P(L_h > A_h) = \int_{0}^{\infty} \int_{0}^{l} f_{L_h, A_h}(l, a) \, da \, dl
$$
The LOLE for the entire horizon is defined as the expected total number of hours of load loss. By the [linearity of expectation](@entry_id:273513), this is simply the sum of the hourly LOLPs:
$$
\text{LOLE} = \sum_{h=1}^{H} \text{LOLP}_h = \sum_{h=1}^{H} P(L_h > A_h)
$$
This formulation, typically expressed in units of hours/year or days/year (e.g., the common "1 day in 10 years" standard corresponds to an LOLE of 0.1 days/year), provides a rigorous, probabilistic foundation for resource adequacy targets. The core of adequacy modeling, therefore, lies in accurately characterizing the probability distributions of load and available capacity.

#### Modeling Aggregate Supply: The Capacity Outage Probability Table (COPT)

While the load distribution can be derived from historical data and forecasts, determining the distribution of total available capacity, $A_h$, is more complex. A power system comprises hundreds or thousands of individual generating units, each subject to unpredictable forced outages. The total available capacity is the sum of the capacities of all units that are operational at a given time.

Assuming that unit outages are [independent events](@entry_id:275822), we can construct the probability distribution for the total system capacity using a [recursive algorithm](@entry_id:633952). The resulting distribution is known as the **Capacity Outage Probability Table (COPT)**, which is a probability [mass function](@entry_id:158970) listing all possible levels of available capacity and their associated probabilities.

Let us consider a system with $n$ generating units. Unit $i$ has a capacity of $c_i$ and a forced outage probability of $p_i$. This means it is available with probability $1-p_i$ and unavailable with probability $p_i$. The COPT is built by adding one unit at a time.

The process begins with a system of zero units, which has 0 MW of capacity with a probability of 1. Now, assume we have the COPT for a system of $k-1$ units. When we add unit $k$, with capacity $c_k$ and outage probability $p_k$, the new distribution is formed by considering two possibilities for every existing capacity state. For each state in the $(k-1)$-unit COPT with capacity $C$ and probability $P$:
1.  If unit $k$ is on outage (with probability $p_k$), the total capacity remains $C$. This adds a probability mass of $P \cdot p_k$ to the state $C$ in the new COPT.
2.  If unit $k$ is available (with probability $1-p_k$), the total capacity becomes $C + c_k$. This adds a probability mass of $P \cdot (1-p_k)$ to the state $C+c_k$ in the new COPT.

This convolution process is repeated for all $n$ units. The final table gives the probability distribution of the total available capacity for the entire fleet, correctly accounting for scenarios where different combinations of unit outages result in the same total capacity level.

#### Integrating Supply and Demand to Calculate LOLE

With the COPT representing the supply-side uncertainty and a load forecast representing the demand-side uncertainty, we can perform a practical calculation of the system LOLE. A common simplification is to use a **Load Duration Curve (LDC)**, which is a sorted list of all hourly loads over the horizon, from highest to lowest.

For each hour $h$ on the LDC, with its corresponding load $L_h$, the LOLP for that hour is the probability that the total available capacity (from the COPT) is strictly less than $L_h$. This is calculated by summing the probabilities of all capacity states in the COPT that are smaller than $L_h$:
$$
\text{LOLP}_h = P(A  L_h) = \sum_{C_j  L_h} P(A = C_j)
$$
where the sum is over all capacity states $C_j$ in the COPT.

The system's total LOLE is then the sum of these hourly LOLPs over all $H$ hours of the LDC. This method, which convolves individual generator outage probabilities into a system supply curve and then compares it against a load distribution, is the workhorse of modern [resource adequacy](@entry_id:1130949) studies.

### Accreditation and Valuation of Capacity Resources

System-level metrics like LOLE are essential, but a capacity market must also value the contribution of individual resources. This process, known as **capacity accreditation**, determines the quantity of capacity a resource is credited with providing, which in turn determines its payment.

#### From Installed to Unforced Capacity: Measuring Contribution to Reliability

A generator's nameplate or maximum rated output is its **Installed Capacity (ICAP)**. However, because generators are not perfectly reliable, crediting them for their full ICAP would overstate their contribution to [resource adequacy](@entry_id:1130949). Instead, capacity markets use a derated value that accounts for the probability of forced outages.

The key metric for generator unreliability is the **Equivalent Forced Outage Rate on demand (EFORd)**. It is defined as the conditional probability that a unit will be unavailable due to a forced outage during periods when it is needed by the system.

Using this metric, we can define the **Unforced Capacity (UCAP)** of a generator. UCAP represents the expected deliverable capacity from the unit, conditioned on it being needed by the system. In a simple two-state model where a unit is either fully available (at its ICAP level) or fully unavailable (0 MW), the relationship between these quantities can be derived from first principles. Let $S$ be a random variable that is 1 if the unit is available and 0 if it is on a forced outage. The deliverable capacity is $ICAP \cdot S$. The UCAP is the expected value of this quantity, conditioned on a demand event $D$:
$$
UCAP = E[ICAP \cdot S | D] = ICAP \cdot E[S | D]
$$
The expected value of the state variable $S$ is simply the probability that it is equal to 1.
$$
E[S | D] = 1 \cdot P(S=1|D) + 0 \cdot P(S=0|D) = P(S=1|D)
$$
By definition, $EFORd = P(S=0|D)$. Since the unit must be in one of the two states, $P(S=1|D) = 1 - P(S=0|D) = 1 - EFORd$. Substituting this back gives the fundamental formula for unforced capacity:
$$
UCAP = ICAP \cdot (1 - EFORd)
$$
This UCAP value, not the ICAP, is typically the product that is bought and sold in a capacity market, as it better reflects a resource's true contribution to [system reliability](@entry_id:274890).

#### A Deeper Look at Outage Rates: Continuous-Time Markov Models

To better understand the probabilistic nature of EFORd, we can model the behavior of a generating unit using a continuous-time Markov process. Consider a unit that transitions between an available state ($U$) and a forced-outage state ($D$). Let the constant rate of failure (transition from $U$ to $D$) be $\lambda$, and the constant rate of repair (transition from $D$ to $U$) be $\mu$.

In the long run, the system reaches a steady state where the probability of being in the outage state, known as the **Forced Outage Rate (FOR)**, is given by the balance of flows between states:
$$
\text{FOR} = \frac{\lambda}{\lambda + \mu}
$$
The EFORd metric is more nuanced because it considers not just the instantaneous probability of being on outage, but the ability to serve a load for a specific duration, $\tau$. If a demand for the unit's service begins at a random time, the EFORd is the probability that the unit cannot remain continuously available for the entire duration $\tau$.

This can be calculated by considering two scenarios. First, if the demand arrives when the unit is already in state $D$ (which occurs with [steady-state probability](@entry_id:276958) $\pi_D = \text{FOR}$), failure is certain. Second, if the demand arrives when the unit is in state $U$ (with probability $\pi_U = 1 - \text{FOR}$), failure occurs if the unit transitions to state $D$ before time $\tau$ has elapsed. Due to the [memoryless property](@entry_id:267849) of the Markov process, the time until failure from state $U$ is exponentially distributed with rate $\lambda$. The probability of remaining in state $U$ for duration $\tau$ is $\exp(-\lambda\tau)$.

Combining these elements yields the expression for EFORd:
$$
\text{EFORd} = \pi_D \cdot (1) + \pi_U \cdot (1 - \exp(-\lambda\tau)) = 1 - \frac{\mu}{\lambda + \mu}\exp(-\lambda\tau)
$$
This derivation shows how the EFORd, a crucial parameter in capacity accreditation, is fundamentally linked to the physical reliability characteristics ($\lambda$ and $\mu$) of the generator and the operational requirements of the system ($\tau$).

### The Economic Rationale for Capacity Markets

Having established the physical and probabilistic basis for measuring reliability, we now turn to the economic question: why are capacity markets necessary? In theory, a well-designed **energy-only market** (where generators are paid only for the energy they produce) should provide sufficient revenue for investment. In practice, this often fails, leading to the "missing money" problem.

#### The "Missing Money" Problem in Energy-Only Markets

In an energy-only market, wholesale electricity prices can, in principle, rise to very high levels during periods of scarcity to reflect the high value of avoiding blackouts. These scarcity rents are supposed to provide the revenue that incentivizes investment in new generation, particularly for "peaking" units that run infrequently but are critical for reliability.

However, a combination of [market power](@entry_id:1127631) mitigation rules, regulatory price caps ($\bar{p}$), and operator caution often prevents prices from reaching the true **Value of Lost Load (VOLL)**, which can be an [order of magnitude](@entry_id:264888) higher than typical price caps. This artificially suppressed scarcity revenue creates a shortfall for investors, known as the **missing money**.

We can formalize this by considering a peaker plant whose profitability depends on scarcity revenues. Many systems implement an **Operating Reserve Demand Curve (ORDC)**, which adds a scarcity price to the energy price based on the level of available reserves. The expected annual revenue for a peaker is the integral of this scarcity price over the distribution of reserve levels during scarce hours. A detailed analysis shows that even with an ORDC, if the price is capped at $\bar{p} \ll VOLL$, the expected revenue can fall significantly short of the amount needed to justify a new investment. This revenue shortfall between what is needed and what an energy-only market provides is the "missing money" that capacity markets are designed to fill.

#### Defining the Target: Cost of New Entry (CONE) and Net CONE

To solve the missing money problem, a capacity market must provide a revenue stream that makes a new, efficient generator economically viable. The benchmark for this is the **Cost of New Entry (CONE)**, sometimes called the gross CONE. CONE represents the full annualized cost of a new generating unit (typically a peaker, which is often the marginal resource for capacity). It includes the annuitized capital cost plus annual fixed operation and maintenance (OM) costs.

The annuitized capital cost is calculated using the **Capital Recovery Factor (CRF)**, which converts the upfront overnight capital cost into a stream of equal annual payments over the asset's [economic life](@entry_id:1124123), given a specific discount rate (the weighted average cost of capital, or WACC).
$$
\text{CONE} = (\text{Overnight Capital Cost}) \cdot \text{CRF} + (\text{Fixed OM Cost})
$$
However, this new generator is still expected to earn some revenue from the energy and [ancillary services](@entry_id:1121004) markets. The capacity market only needs to provide the "missing" portion. This leads to the definition of **Net CONE**, which is the gross CONE minus the expected net revenues from these other markets.
$$
\text{Net CONE} = \text{CONE} - (\text{Expected Energy  Ancillary Service Net Revenues})
$$
Net CONE represents the target annual revenue from the capacity market that would allow a marginal new entrant to break even. It is therefore a critical parameter that anchors the price level in a capacity market auction.

### Designing the Market: Demand Curves and Clearing Mechanisms

A capacity market, like any market, consists of supply and demand. The supply is formed by the offers from existing and new resources, while the demand is determined by the system operator based on reliability targets and economic principles.

#### Constructing the Capacity Demand Curve

A key element in modern capacity market design is a downward-sloping demand curve, which represents the system's [willingness to pay](@entry_id:919482) for incremental capacity. This curve can be derived from a welfare economics framework. A social planner's objective is to choose the level of installed capacity, $K$, that minimizes the total social cost, which is the sum of the cost to build capacity, $C(K)$, and the expected cost of outages, $v \cdot L(K)$, where $v$ is the VOLL and $L(K)$ is the [expected unserved energy](@entry_id:1124756).
$$
\min_{K} S(K) = C(K) + v \cdot L(K)
$$
The optimal level of capacity is found where the marginal cost of adding capacity equals the marginal benefit of that capacity. The marginal benefit is the reduction in expected outage costs. The [first-order condition](@entry_id:140702) for this optimization is:
$$
C'(K) = -v \cdot \frac{dL}{dK}
$$
The term on the right, the marginal reliability benefit, defines the inverse demand curve for capacity, $p(K)$. This marginal benefit is equal to the Value of Lost Load ($v$) multiplied by the resulting Loss of Load Expectation ($\text{LOLE}$), measured in hours/year. The LOLE at a given capacity level $K$ is in turn derived from the probability that [net load](@entry_id:1128559) exceeds capacity, $1-F_N(K)$. Thus, the price on the demand curve is given by:
$$p(K) = v \cdot \text{LOLE}(K)$$
The shape, or **elasticity**, of this demand curve is intimately tied to the physical characteristics of the system. Assuming that LOLE decays exponentially with capacity, $\text{LOLE}(K) = L_0 \exp(-\beta K)$, which is a reasonable approximation for many systems, the own-price elasticity of the capacity demand curve can be shown to be $\varepsilon_D(K) = -\beta K$. This elegant result demonstrates that the responsiveness of the demand curve to price is directly related to how effectively additional capacity reduces reliability risk (as captured by $\beta$).

#### The Clearing Mechanism: A Formal View

The final step is the market clearing. In a centralized [capacity auction](@entry_id:1122039), the system operator procures capacity to meet its target by solving a constrained optimization problem. The objective is to minimize the total procurement cost, subject to meeting a minimum reliability requirement, $R$. The problem can be formally stated as:
$$
\min_{X} \int_{0}^{X} c(u) \, du \quad \text{subject to} \quad X \ge R
$$
where $X$ is the total cleared capacity and $c(u)$ is the marginal cost of procurement (the aggregate supply curve).

The solution to this optimization problem can be analyzed using the Karush-Kuhn-Tucker (KKT) conditions. The dual variable (or Lagrange multiplier) associated with the reliability constraint, $X \ge R$, has a crucial economic interpretation: it is the **shadow price** of the constraint. This shadow price represents the marginal cost of satisfying the reliability requirement, and it becomes the market clearing price for capacity.

For instance, in the simple case where the cost-minimizing procurement level falls exactly at the required level $R$, the KKT conditions show that the market clearing price is equal to the marginal cost of supply at that quantity, $c(R)$. This formal mechanism ensures that the market procures the desired quantity of capacity and that all cleared resources are paid a uniform price that reflects the marginal cost of ensuring [system reliability](@entry_id:274890).