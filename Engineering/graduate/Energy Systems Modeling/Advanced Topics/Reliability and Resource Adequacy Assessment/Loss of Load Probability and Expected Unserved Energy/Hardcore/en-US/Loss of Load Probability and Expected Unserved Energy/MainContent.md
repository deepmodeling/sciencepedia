## Introduction
Ensuring a reliable supply of electricity is a fundamental objective for modern society, yet it is a task fraught with uncertainty. The unpredictable nature of customer demand, the stochastic output of renewable energy sources, and the potential for unexpected generator failures create a complex probabilistic environment for system planners. To navigate this uncertainty and make sound investment and operational decisions, a rigorous quantitative framework is essential. This article addresses this need by providing a comprehensive exploration of the core metrics used to assess power system resource adequacy: Loss of Load Probability (LOLP) and Expected Unserved Energy (EUE).

This article is structured to build your expertise from the ground up. In the "Principles and Mechanisms" chapter, we will lay the theoretical foundation, formally defining LOLP, LOLE, and EUE, and exploring the probabilistic models required for their calculation, such as the Capacity Outage Probability Table (COPT). Next, the "Applications and Interdisciplinary Connections" chapter will bridge theory and practice, demonstrating how these metrics are applied in [resource adequacy](@entry_id:1130949) planning, economic analysis, market design, and in conjunction with fields like climate science. Finally, the "Hands-On Practices" section will allow you to solidify your understanding through guided computational exercises. We begin by delving into the principles and mechanisms that underpin these crucial reliability metrics.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of [resource adequacy](@entry_id:1130949) as a cornerstone of [power system reliability](@entry_id:1130080). We established that ensuring sufficient generation capacity to meet electricity demand is a fundamentally probabilistic challenge, owing to uncertainties in both load and supply. This chapter delves into the principles and mechanisms that form the quantitative foundation of modern adequacy assessment. We will formally define the key metrics used by system planners, explore the probabilistic models required for their calculation, and analyze the nuanced interpretations of the results.

### Fundamental Adequacy Metrics

To quantify the risk of supply shortfalls, we rely on a set of standardized, mathematically precise metrics. These metrics are derived from a probabilistic comparison of available supply capacity, denoted by the random variable $C_t$, and system load, denoted by the random variable $L_t$, for each period $t$ within a given planning horizon. A **loss-of-load event** is defined to occur in period $t$ if and only if demand exceeds supply, i.e., $L_t > C_t$.

#### Loss of Load Probability (LOLP)

The most fundamental metric is the **Loss of Load Probability (LOLP)**, which quantifies the likelihood of a shortfall in a single, specific time interval. For a period $t$, it is defined as the probability of the loss-of-load event:

$$
\mathrm{LOLP}_t = \mathbb{P}(L_t > C_t)
$$

This is a dimensionless value between $0$ and $1$ that represents the risk of encountering a deficit in that particular period. Alternatively, using an [indicator function](@entry_id:154167) $\mathbf{1}\{\cdot\}$, which is $1$ if its argument is true and $0$ otherwise, the LOLP for period $t$ can be expressed as the expectation of a Bernoulli random variable corresponding to the shortfall event :

$$
\mathrm{LOLP}_t = \mathbb{E}[\mathbf{1}\{L_t > C_t\}]
$$

#### Loss of Load Expectation (LOLE)

While LOLP provides a snapshot of risk for a single period, planners are typically concerned with the cumulative risk over a longer horizon, such as a year. The **Loss of Load Expectation (LOLE)** aggregates this risk across all periods. It is crucial to distinguish between two common formulations of LOLE. Formally, LOLE is the expected *count* of periods in which a loss-of-load event occurs. Over a horizon of $T$ periods, this is given by:

$$
\mathrm{LOLE}_{\text{count}} = \mathbb{E}\left[\sum_{t=1}^{T} \mathbf{1}\{L_t > C_t\}\right] = \sum_{t=1}^{T} \mathbb{E}[\mathbf{1}\{L_t > C_t\}] = \sum_{t=1}^{T} \mathrm{LOLP}_t
$$

This quantity is a dimensionless number representing the expected number of shortfall intervals. However, in industry practice, LOLE is almost universally reported as an expected *duration*, typically in units of hours per year or days per year. If each period $t$ has a duration of $\Delta t$ (e.g., $1$ hour), the **Loss of Load Duration**, which we will refer to as LOLE for consistency with common usage, is:

$$
\mathrm{LOLE} = \sum_{t=1}^{T} \mathrm{LOLP}_t \cdot \Delta t
$$

This metric answers the question: "For how many hours per year do we expect demand to exceed supply?" For example, an LOLE of $2.4$ hours/year corresponds to the widely discussed "1 day in 10 years" reliability standard ($0.1$ days/year $\times$ $24$ hours/day). It measures the expected *frequency* and *duration* of reliability events but provides no information about their magnitude .

#### Expected Unserved Energy (EUE)

To capture the magnitude, or **severity**, of shortfalls, we use the metric of **Expected Unserved Energy (EUE)**. In any period $t$ where a shortfall occurs ($L_t > C_t$), the amount of power that cannot be supplied is the difference $L_t - C_t$. If there is no shortfall ($L_t \le C_t$), the unserved power is zero. This logic is captured perfectly by the **positive-part operator**, $(x)_+ = \max\{x, 0\}$. The unserved power in period $t$ is the random variable $(L_t - C_t)_+$.

The EUE is the total expected energy not served over the planning horizon. For each period $t$, the [expected unserved energy](@entry_id:1124756) is the expected unserved power multiplied by the period's duration, $\mathbb{E}[(L_t - C_t)_+] \cdot \Delta t$. Summing over the entire horizon gives the total EUE:

$$
\mathrm{EUE} = \sum_{t=1}^{T} \mathbb{E}[(L_t - C_t)_+] \cdot \Delta t
$$

EUE is measured in energy units (e.g., megawatt-hours, MWh) and provides a comprehensive measure of reliability that accounts for both the frequency and the magnitude of supply deficits .

### Probabilistic Modeling of System Components

The definitions of LOLP, LOLE, and EUE depend on the random variables for load ($L_t$) and capacity ($C_t$). To compute these metrics in practice, we must first construct probabilistic models for these system components.

#### Modeling Available Generation Capacity

The total available capacity $C_t$ is the sum of the available capacities of all individual generating units in the system. Since individual units can fail unexpectedly (a **forced outage**), the available capacity of each unit is a random variable, making the total system capacity a random variable as well.

A common approach for modeling a fleet of thermal generators is to construct a **Capacity Outage Probability Table (COPT)**. This table is the probability [mass function](@entry_id:158970) (PMF) of the total available conventional capacity, enumerating all possible capacity levels and their associated probabilities.

Consider a system of $n$ independent two-state generating units, where unit $i$ has capacity $s_i$ and a [forced outage rate](@entry_id:1125211) $q_i$. The available capacity of unit $i$, $X_i$, is $s_i$ with probability $a_i = 1-q_i$ and $0$ with probability $q_i$. The total capacity is $C = \sum_{i=1}^n X_i$. The PMF of $C$ can be built recursively. Let $p_{k-1}$ be the PMF for the first $k-1$ units. To add unit $k$, we "convolve" its distribution with $p_{k-1}$. For each existing capacity state $c'$ with probability $p_{k-1}(c')$, adding unit $k$ creates two new possibilities: the system has capacity $c'$ with probability $p_{k-1}(c') \cdot q_k$ (unit $k$ is out), or it has capacity $c' + s_k$ with probability $p_{k-1}(c') \cdot a_k$ (unit $k$ is in).

This gives rise to a [dynamic programming](@entry_id:141107) algorithm. Starting with a PMF of $1$ at capacity $0$, we iteratively add each generator, updating the PMF at each step. The [computational complexity](@entry_id:147058) of this algorithm is $\mathcal{O}(n \cdot S)$, where $n$ is the number of units and $S$ is the total installed capacity. Once the final PMF, $p(c)$, is computed, adequacy metrics can be calculated directly against any given load level .

The simple two-state model can be readily extended to capture more realistic generator behavior, such as **partial deratings**, where a unit is online but operating at a reduced output level. A unit with a nameplate capacity of $100$ MW might have three states: fully available at $100$ MW (e.g., probability $0.90$), partially derated to $60$ MW (e.g., probability $0.08$), and fully on outage at $0$ MW (e.g., probability $0.02$). These states are incorporated into the COPT as distinct outcomes, and their probabilities must sum to one. When convolving this multi-state unit into the system COPT, each existing capacity state fans out into three new states instead of two .

#### Modeling Load and the Crucial Role of Correlation

The "load" that conventional generators must meet is increasingly defined as the **net load**, $N_t = L_t - R_t$, where $L_t$ is the gross customer demand and $R_t$ is the output from [variable renewable energy](@entry_id:1133712) (VRE) sources like wind and solar. Since both $L_t$ and $R_t$ are stochastic, the [net load](@entry_id:1128559) $N_t$ is also a random variable.

A critical principle in adequacy assessment is that calculating metrics like LOLP and EUE requires knowledge of the **[joint probability distribution](@entry_id:264835)** of [net load](@entry_id:1128559) and available capacity, $f_{N,C}(n,c)$. Knowing only the marginal distributions, $f_N(n)$ and $f_C(c)$, is not sufficient. The dependence structure, or correlation, between net load and capacity availability is crucial . For instance, extreme heat waves can simultaneously drive up air conditioning demand (increasing $N_t$) and increase the failure rate of thermal generators (decreasing $C_t$), a dangerous positive correlation that dramatically increases shortfall risk. In general, LOLP must be computed via an integral over the [joint distribution](@entry_id:204390):

$$
\mathrm{LOLP}_t = \iint_{n > c} f_{N,C}(n,c) \, \mathrm{d}n \, \mathrm{d}c
$$

This principle highlights a major pitfall of simplified, non-chronological modeling methods. A common historical approach is to use a **load-duration curve (LDC)**, which sorts all hourly loads in a year from highest to lowest, thereby discarding all information about when they occur. If one attempts to account for VRE by subtracting an *average* VRE output from this LDC, the temporal correlation between load and VRE is destroyed.

Consider a system where low wind output consistently coincides with high demand periods. A chronological simulation, which evaluates the supply-demand balance hour by hour, would correctly identify these high-risk intervals. The LDC method with averaged wind, however, would effectively "smear" the benefit of high wind during low-demand hours over to the high-demand hours, artificially lowering the peak net load and leading to a gross underestimation of reliability risk. This demonstrates that preserving the chronology of load and VRE is essential for accurate adequacy assessment .

#### Advanced Dependency: Correlated Failures

Just as load and capacity can be correlated, the failures of individual generators can also be correlated. **Common-mode failures** occur when a single external event or stressor increases the likelihood of outages for multiple components simultaneously. Examples include extreme weather, fuel supply disruptions, or cyberattacks.

Modeling such dependencies is complex but essential for capturing certain high-impact risks. One approach is to introduce a latent (unobserved) stress factor, $Z$. For instance, the system could be in a "normal" state ($Z=0$) or a "stressed" state ($Z=1$) with some probability. Conditional on the state of $Z$, generator outages are assumed to be independent, but the outage probabilities themselves depend on $Z$. Under the stressed state, the [forced outage rate](@entry_id:1125211) $q_i$ of each unit could increase. The total LOLP is then calculated using the law of total probability, summing the conditional LOLP in each state weighted by the probability of that state:

$$
\mathrm{LOLP}_{\text{total}} = \mathrm{LOLP}|_{Z=0} \cdot \mathbb{P}(Z=0) + \mathrm{LOLP}|_{Z=1} \cdot \mathbb{P}(Z=1)
$$

This framework allows for the analysis of how sensitive the system's reliability is to the frequency and severity of such common-mode stress events .

### Interpreting Adequacy Metrics: Frequency vs. Severity

System planners use both LOLE and EUE because they measure different dimensions of risk. LOLE measures the *frequency* of shortfalls, while EUE captures both *frequency and severity*. Two systems can have identical LOLE but vastly different EUE, and a policy decision that improves one metric may not improve the other proportionally.

Consider two hypothetical power systems, A and B, that both experience an expected 20 hours of shortfall per year (i.e., $LOLE_A = LOLE_B = 20$ hours/year). In system B, every shortfall is of a moderate size, say $100$ MW. In system A, most shortfalls are small ($50$ MW), but there is a small chance of an extremely large shortfall ($1000$ MW). Because of these rare but severe events, the average shortfall magnitude in system A is much higher than in system B. As a result, even though their shortfall frequency is identical, system A will have a significantly higher EUE. This "severity effect" demonstrates that LOLE alone can obscure critical vulnerabilities to high-impact events .

This distinction is particularly important when the distribution of [net load](@entry_id:1128559) has "heavy tails," meaning that extreme events, while rare, are more likely than they would be under a normal distribution. For a system facing a [heavy-tailed risk](@entry_id:1125992), a capacity addition that successfully halves the LOLE (reduces the frequency of events) will not necessarily halve the EUE. The EUE is driven by the magnitude of the largest, rarest events, and these may be less affected by the capacity addition. In fact, for certain distributions, a $50\%$ reduction in LOLP can lead to a much smaller reduction in EUE. This illustrates that EUE can be a "stickier" risk metric, and focusing solely on an LOLE target may leave the system exposed to significant residual risk in terms of unserved energy .

### Discretization and Model Resolution

Finally, it is important to understand how the choice of temporal resolution in a model affects the calculated metrics. Adequacy models typically discretize a continuous-time reality into a series of time steps, each with duration $\Delta t$ (e.g., one hour). The values of the metrics depend on how they are defined in relation to this discretization.

Consider a fixed planning horizon $T$ that is partitioned into $N = T/\Delta t$ steps. As we refine the model by making $\Delta t$ smaller (and $N$ larger), the behavior of the metrics is as follows :
-   **LOLP** (as a per-step probability, $\mathbb{P}(L_t > C_t)$): This value is approximately *invariant* to $\Delta t$, as it reflects the instantaneous risk at a point in time.
-   **LOLE** (as an expected duration, $\sum \mathrm{LOLP}_t \cdot \Delta t$): This value is also approximately *invariant* to $\Delta t$. The expression is a Riemann sum that approximates the integral of the instantaneous shortfall probability over the horizon. As $\Delta t$ shrinks, the number of terms in the sum increases, but this is offset by the decrease in the $\Delta t$ multiplier, causing the sum to converge to a stable value.
-   **EUE** ($\sum \mathbb{E}[(L_t-C_t)_+]\cdot\Delta t$): This metric is also approximately *invariant* to $\Delta t$ for the same reason as LOLE; it is a Riemann sum that converges to the integral of the expected unserved power.
-   **LOLE** (as an expected count of steps, $\sum \mathrm{LOLP}_t$): This value is *not* invariant. Since each term is approximately constant, the sum scales directly with the number of steps, $N$. Therefore, the expected count of shortfall intervals is proportional to $1/\Delta t$.

Understanding these scaling properties is essential for correctly implementing and interpreting the results of discrete-time adequacy simulations and for ensuring consistency when comparing results from models with different time resolutions.