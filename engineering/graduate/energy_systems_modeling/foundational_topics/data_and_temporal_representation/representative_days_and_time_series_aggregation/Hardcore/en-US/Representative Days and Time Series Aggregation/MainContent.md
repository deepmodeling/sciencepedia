## Introduction
Energy system optimization models are crucial for planning our future energy infrastructure, but they face a significant hurdle: time. Modeling a full year at an hourly resolution creates a computational problem so large it is often impossible to solve. This article addresses this challenge by exploring **temporal aggregation**, the set of techniques used to reduce a model's time horizon from 8760 hours to a manageable number of representative periods. The core problem is that this simplification is not free; it introduces a trade-off between computational speed and model accuracy, with the potential for costly errors in investment and operational planning.

This article provides a comprehensive guide to navigating this complex landscape. First, the **"Principles and Mechanisms"** chapter will dissect the fundamental approaches to aggregation, from time slicing to representative days, and explain the critical differences between using centroids and medoids. It will uncover how these choices can lead to systematic biases, such as underestimating the need for peak capacity and long-duration storage. Next, the **"Applications and Interdisciplinary Connections"** chapter will illustrate the real-world consequences of these principles in power system planning, network analysis, and even fields like epidemiology and environmental science. Finally, the **"Hands-On Practices"** section will offer practical exercises to solidify your understanding, allowing you to directly experience the impact of different aggregation strategies. By understanding these concepts, you will be equipped to build models that are both tractable and reliable.

## Principles and Mechanisms

Energy system optimization models are foundational tools for planning future infrastructure investments and understanding operational strategies. A central challenge in their formulation is the representation of time. The dynamics of electricity demand, the variability of renewable energy sources, and the operational constraints of generators and storage devices unfold over thousands of hours in a year. A model that captures every hour of a year—a full chronological time series of $T=8760$ hours—offers the highest temporal fidelity. However, for many planning models, particularly those involving discrete investment and operational decisions formulated as Mixed-Integer Linear Programs (MILPs), solving a problem of this scale is computationally prohibitive. This chapter explores the principles and mechanisms of **temporal aggregation**, a set of indispensable techniques for reducing the temporal complexity of these models while striving to preserve the essential characteristics of the original time series.

### The Rationale for Temporal Aggregation: The Tractability-Fidelity Trade-off

The computational burden of large-scale optimization models, especially MILPs, grows rapidly with the number of variables and constraints. Consider a typical capacity expansion model that makes unit commitment decisions for a set of thermal generators. If there are $N$ generators and $T$ time steps, the model includes at least $N \times T$ binary variables to represent the on/off status of each generator at each hour, along with numerous continuous variables for power output and chronological constraints for ramping and storage.

The complexity of solving an MILP is largely driven by the size of the combinatorial search space, which grows exponentially with the number of integer variables. As a practical example, a model for a system with $N=50$ thermal units over a full year ($T=8760$) would involve $50 \times 8760 = 438,000$ binary commitment variables. Aggregating this time series into $K=12$ representative days of $H=24$ hours each reduces the number of time steps to $K \times H = 288$. The number of binary variables plummets to $50 \times 288 = 14,400$—a reduction of over 96%. The number of time-coupling constraints, which link one hour to the next, is similarly reduced. This dramatic reduction in problem size is often the only way to make long-term planning models computationally tractable [@problem_id:4117318].

This gain in tractability, however, is not free. It comes at the cost of reduced temporal fidelity. The core task of temporal aggregation is to create a reduced representation of time that preserves the statistical and operational characteristics of the original data most relevant to the planning decision. The choices made during aggregation can introduce biases and errors, leading to suboptimal or even physically infeasible investment plans. The remainder of this chapter is dedicated to understanding these choices and their profound consequences.

### Fundamental Approaches to Aggregation

Temporal aggregation methods map the original time index $\{1, \dots, T\}$ to a smaller set of temporal representatives. The two most common families of methods differ fundamentally in how they handle chronology [@problem_id:4117329].

#### Time Slicing

**Time slicing** involves partitioning the original set of hours into a smaller number of slices, or operating states, based on the similarity of their characteristics (e.g., load, renewable availability). Crucially, this grouping is performed *without regard to chronological order*. For instance, a sunny, low-demand midday hour in April might be grouped into the same slice as a similar hour in September. Each slice is then represented by a single point, typically the centroid (average) of all hours within it, and is assigned a weight corresponding to the number of hours it represents.

The primary strength of time slicing is that it provides an excellent approximation of the **marginal distribution** of the system's operating conditions. It accurately captures the frequency of high-load hours, high-wind hours, and so on. This is valuable for sizing total capacity. However, by completely discarding the temporal sequence, time slicing makes it impossible to model any process with memory. Chronological constraints, such as generator ramp limits ($|g_{i,t} - g_{i,t-1}| \le R_i$) or the state-of-charge evolution of an energy storage device ($s_{t+1} = s_t + \dots$), become meaningless because the concepts of "previous" ($t-1$) and "next" ($t+1$) are lost.

#### Representative Periods

A more common approach, particularly for models with storage or ramping constraints, is the selection of **representative periods**. This method begins by segmenting the original time series into contiguous periods of a fixed duration, typically 24 hours to form days. These periods (e.g., 365 days of the year) are then clustered based on their similarity. From each cluster, one or more representative periods are chosen.

This approach preserves the **intra-period chronology**. Within each 24-hour representative day, the hour-to-hour sequence is maintained, allowing the model to capture dynamics such as diurnal load cycles, solar generation ramps, and daily cycling of battery storage. However, the standard implementation of this method discards **inter-period chronology**. The model may know that a "sunny, high-load summer day" type occurs 30 times a year, but it does not know the sequence in which these days occur relative to other day types. This fundamental break in the year-long timeline has critical implications, especially for technologies with memory longer than the period duration, such as seasonal storage.

### Methods for Selecting Representative Periods

Choosing representative periods is fundamentally a clustering problem: grouping similar daily profiles and selecting a proxy for each group. The choice of this proxy—the representative itself—is a critical decision with significant trade-offs [@problem_id:4117368] [@problem_id:4117402].

#### Centroids: The Synthetic Average

One common method is to represent each cluster by its **centroid**, which is the component-wise arithmetic mean of all the daily profiles within it. An aggregation based on centroids has one paramount advantage: it perfectly preserves time-additive linear quantities. For an exogenous variable like electricity demand, the total annual demand calculated from the weighted sum of centroid representatives will exactly equal the true total annual demand from the original time series [@problem_id:4117402]. This property is essential for the integrity of models whose objective functions and constraints involve annual totals or averages of energy, costs, or emissions [@problem_id:4117429].

However, the centroid is a synthetic construct—an "average day" that may never have occurred and may not even be physically plausible. The process of averaging smooths the data, which has two detrimental effects:
1.  **Dampening of Extremes**: The peak load of a centroid day will almost always be lower than the true peak load of the most extreme day in its cluster.
2.  **Smoothing of Ramps**: The rate of change (ramp) in a centroid profile is dampened compared to the sharpest ramps in the original data.

As we will see, these properties can lead a model to systematically underestimate the need for both generation capacity and system flexibility.

#### Medoids: The Real Representative

An alternative is to represent each cluster by its **medoid**. The medoid is an actual, historically observed day from the cluster that is most "central," meaning it has the minimum average dissimilarity to all other days in its cluster [@problem_id:4117368].

The definitive advantage of using a medoid is that it guarantees the representative day is a **realistic and feasible profile**. All intra-day characteristics—the precise timing and magnitude of peaks, the steepness of ramps, and the complex correlations between variables (e.g., how wind and solar output co-evolve with demand)—are preserved exactly as they occurred. This is critical for accurately modeling constraints that depend on these joint patterns.

The disadvantage is that the medoid, being just one sample from the cluster, does not generally preserve the cluster's mean. Consequently, an aggregation based on medoids will typically not preserve annual totals of demand or energy, introducing a bias that may require subsequent correction or rescaling [@problem_id:4117402].

### The Consequences of Aggregation: Errors and Biases

The compromises made during aggregation are not merely academic; they translate directly into biases in the model's outputs, potentially leading to flawed investment decisions.

#### Underestimation of Adequacy and Flexibility Needs

Resource adequacy is the ability of a power system to meet demand at all times. A system's need for firm generation capacity is primarily driven by its **peak net load**—the highest point of demand after subtracting variable renewable generation. Flexibility, or the ability to respond to rapid changes, is driven by the steepest **net load ramps**.

Aggregation methods, especially those based on centroids, systematically smooth out these extreme events [@problem_id:4117284]. A model that is "shown" a smoothed net load profile with a lower peak will logically conclude that less firm capacity is needed. Similarly, a model seeing gentler ramps will underestimate the need for flexible resources like fast-ramping gas turbines or batteries. This can lead to an overly optimistic plan that builds an insufficient amount of capacity and flexibility, compromising the reliability of the future system [@problem_id:4117284] [@problem_id:4117402].

#### Distortion of Chronological Dependencies

Perhaps the most significant bias introduced by standard representative day methods stems from the loss of inter-period chronology. This particularly affects the valuation and sizing of technologies with operational memory, most notably **energy storage**.

In a full chronological model, an energy storage device can carry energy from one day to the next, enabling it to manage multi-day weather events. For example, it can charge during a series of windy days and discharge during a subsequent multi-day "wind drought" (a period of low wind). This ability is determined by its energy capacity ($E_{\max}$) and the **autocorrelation** of the net load time series—the tendency for high- or low-load periods to persist over time [@problem_id:4117339].

An aggregated model with disconnected representative days, where storage is forced to be cyclic within each day (i.e., its end-of-day state must equal its start-of-day state), is blind to these multi-day patterns. It cannot see a wind drought that lasts for three consecutive days. Instead, it might simulate a "low-wind day" type three times, but in each instance, the storage is magically "reset" at the beginning of the day. This makes the storage appear more powerful than it is, breaks the link between its operation and the true duration of scarcity events, and leads the model to systematically underestimate the need for long-duration energy storage [@problem_id:4117318] [@problem_id:4117341]. This same chronological break also prevents the correct modeling of multi-day operational constraints on thermal generators, such as minimum up- and down-times.

### Quantifying and Evaluating Aggregation Error

Given these potential pitfalls, it is crucial to have a formal way to measure the quality of an aggregation. We can evaluate the error from two perspectives: the fidelity of the input data and the accuracy of the final model outputs.

#### Input Fidelity Metrics

Let $\{x_t\}$ be the original time series and $\{\hat{x}_t\}$ be the reconstructed time series from the aggregation. Several metrics can quantify the difference between them [@problem_id:4117311]:
- **Bias ($b$)**: The average signed error. A low bias is important for economic objectives, as it indicates that the total energy represented is accurate.
- **Mean Absolute Error (MAE)**: The average of the absolute differences. This metric is well-aligned with economic objectives where costs are roughly linear with energy, as it reflects the average magnitude of dispatch deviations.
- **Root Mean Square Error (RMSE)**: The square root of the average of squared errors. By squaring errors, RMSE heavily penalizes large deviations. This makes it more sensitive to errors in extreme values than MAE.
- **Supremum Norm ($L_{\infty}$-norm)**: The single largest absolute error across the entire time series, $||\hat{x} - x||_\infty = \max_t |\hat{x}_t - x_t|$.

When selecting an aggregation, the choice of metric should align with the model's purpose.
- For ensuring **resource adequacy**, which is driven by peak loads, minimizing the $L_{\infty}$-norm is most appropriate as it directly controls the error in the single worst-case hour. Minimizing RMSE is also a good strategy to suppress large errors at the tails of the distribution.
- For evaluating **economic performance**, which depends on the sum of costs over all hours, minimizing MAE and ensuring a low bias ($b$) are more relevant.
- Metrics like the Mean Absolute Percentage Error (MAPE) should be used with caution, as they become unstable and can be misleading when the true values $x_t$ are close to zero, a common occurrence for net load.

#### Output Reliability Metrics

Ultimately, we care about how aggregation errors affect the model's conclusions about system reliability. Key reliability metrics include the **Loss-of-Load Probability (LOLP)**, the probability that demand will exceed available generation, and **Expected Unserved Energy (EUE)**, the total energy shortfall expected over a period.

Aggregation that smooths out the tails of the net load distribution will underestimate the true probability of extreme events. If a capacity expansion model uses this smoothed distribution to meet a specific LOLP target, it will build insufficient capacity. When this under-built system is faced with the true, more volatile net load, it will experience a higher LOLP and greater EUE than the aggregated model predicted [@problem_id:4117341]. This demonstrates a crucial feedback loop: errors in time series representation lead to errors in investment decisions, which in turn lead to real-world performance that fails to meet the planning targets.

### Advanced Mechanisms: Mitigating Aggregation Errors

Recognizing these limitations, researchers have developed more sophisticated techniques to improve the fidelity of aggregated models.

#### Reintroducing Chronology with Transition Matrices

To address the critical issue of lost inter-period chronology, especially for multi-day storage modeling, one can explicitly model the transitions between representative days. This is achieved by constructing a **transition matrix** $T \in \mathbb{R}^{N \times N}$, where $N$ is the number of representative day types [@problem_id:4117399].

The element $T_{ij}$ is defined as the number of times in the original chronological sequence that a day of type $i$ was immediately followed by a day of type $j$. This matrix empirically captures the sequential relationships between day types. It has the property that the sum of its $i$-th row, $\sum_j T_{ij}$, equals the total number of days of type $i$ ($w_i$), and the sum of its $j$-th column, $\sum_i T_{ij}$, equals the total number of days of type $j$ ($w_j$).

This matrix can be used to link the state variables (like storage state-of-charge) across representative periods. Let $s_i^{\mathrm{end}}$ be the storage level at the end of a type-$i$ day and $s_j^{\mathrm{start}}$ be the level at the start of a type-$j$ day. A conservation constraint can be formulated as:
$$ \sum_{i=1}^N T_{ij} s_i^{\mathrm{end}} = w_j s_j^{\mathrm{start}} \quad \text{for each day type } j $$
This equation ensures that the total "flow" of stored energy into all days of type $j$ from their preceding days matches the total energy required at the start of all type-$j$ days. This formulation re-establishes an annual storage balance and allows the model to "see" the impact of multi-day weather patterns, leading to more realistic sizing of long-duration storage.

#### A Principled Approach: Bilevel Optimization

A more fundamental question is how to select the "best" set of representative days in the first place. While clustering based on input data similarity is a common heuristic, the ideal clustering is one that minimizes the error in the final output of the planning model (e.g., total system cost). This can be formalized as a **bilevel optimization problem** [@problem_id:4117426].

-   The **upper-level problem** is a discrete optimization that chooses the set of representative days and the assignment of original days to them. Its objective is to minimize the difference between the final cost from the aggregated model and the (pre-computed) cost from the full chronological model.
-   The **lower-level problem** is the capacity expansion model itself, which is solved for a given set of representative days passed down from the upper level.

This structure perfectly captures the goal of finding a data-reduction scheme that is optimal for the specific decision-making problem at hand. However, this formulation results in a non-convex, mixed-integer bilevel program, which is exceptionally difficult to solve and represents a frontier of research in energy systems modeling. It serves as a theoretical benchmark, reminding us that temporal aggregation is not merely a pre-processing step but an integral and challenging part of the modeling process itself.