## Introduction
Energy systems are in constant flux, driven by weather, human behavior, and policy changes. The time series data they generate—from building consumption to grid frequency—hold the key to understanding and optimizing their performance. However, these data are often non-stationary, punctuated by abrupt, hidden shifts in their underlying dynamics. Identifying these **structural changes**, or change points, is a critical challenge. Mistaking a true regime shift for random noise, or vice-versa, can lead to flawed forecasts, inefficient operations, and incorrect policy assessments. This article provides a comprehensive guide to the statistical methods designed to meet this challenge.

Over the next three chapters, you will build a robust understanding of [change point detection](@entry_id:1122256) from the ground up. In **Principles and Mechanisms**, we will explore the core statistical theory, distinguishing [structural breaks](@entry_id:636506) from anomalies and detailing the key algorithms for both online and offline detection. Next, in **Applications and Interdisciplinary Connections**, we will see these methods in action, solving real-world problems in building energy management, [renewable energy integration](@entry_id:1130862), and even fields like climate science. Finally, **Hands-On Practices** will offer you the chance to implement and experiment with these powerful techniques through guided coding exercises. We begin by laying the theoretical groundwork: defining what constitutes a structural change and exploring the fundamental principles that govern its detection.

## Principles and Mechanisms

### Defining Structural Change in Time Series

The analysis of energy time series is fundamentally concerned with understanding and predicting system behavior. A critical aspect of this is the detection of **structural changes**, which are persistent shifts in the underlying dynamics of the system. Formally, a **change point** is a time $\tau$ at which the parameters $\theta$ governing the data-generating process, $p_{\theta}(y_t | \mathcal{F}_{t-1})$, change their values. Here, $y_t$ represents the observation at time $t$ (e.g., electricity demand), and $\mathcal{F}_{t-1}$ represents the history of the process up to that point. This framework gives rise to **piecewise-stationary models**, where the parameters $\theta$ are assumed to be constant within distinct, contiguous segments of time, but may change abruptly at the boundaries between segments.

It is crucial to distinguish these structural changes from **transient anomalies** or outliers. A structural change implies a lasting alteration of the system's "rules," whereas an anomaly is a short-lived deviation from which the system quickly recovers. For example, consider an hourly electricity demand series modeled by an [autoregressive process](@entry_id:264527) with an exogenous temperature input (ARX model). The widespread adoption of residential heat pumps over several months would increase the sensitivity of electricity demand to outdoor temperature. This manifests as a persistent change in the [regression coefficient](@entry_id:635881) associated with temperature, marking a true structural change point . In contrast, a multi-hour power outage during a storm causes a temporary drop in measured demand, but the underlying relationship between demand and temperature reverts to its previous state once service is restored. This outage is a transient anomaly, not a structural change. Mistaking an anomaly for a change point would lead to erroneous models with excessively short and meaningless "regimes," highlighting the importance of this conceptual distinction in robust system modeling.

For a change point model to be statistically meaningful, it must be **identifiable**. A model is identifiable if distinct parameter values lead to distinct probability distributions of the observed data. Consider a simple model for a building's electrical load, pre-processed to remove daily cycles, which is assumed to have a single abrupt shift in its mean level at time $\tau$:
$$
y_t = \begin{cases}
    \mu_1 + \varepsilon_t  &\text{for } t \le \tau \\
    \mu_2 + \varepsilon_t  &\text{for } t > \tau
\end{cases}
$$
where $\varepsilon_t$ are independent noise terms with zero mean. The parameters of this model are the triplet $(\mu_1, \mu_2, \tau)$. For this model to be identifiable, several conditions must be met. Most importantly, there must be an actual change in the mean, i.e., $\mu_1 \neq \mu_2$. If $\mu_1 = \mu_2$, the data-generating process is identical for all $t$, and the "change point" $\tau$ has no effect on the data distribution, making its value impossible to determine from the data. Furthermore, the chronological order of the observations must be known; without it, the concept of a change at a specific time index is meaningless. Under these conditions—a genuine parameter shift and known data ordering—the change point model is identifiable, allowing for principled statistical inference .

### Paradigms of Change Point Detection: Online and Offline

The practical application of [change point detection](@entry_id:1122256) can be broadly divided into two paradigms, distinguished by data availability and operational goals: online detection and offline detection.

**Online detection**, also known as sequential or real-time detection, is used for continuous monitoring. Data arrives one observation at a time, and the goal is to raise an alarm as quickly as possible after a change occurs. A key application is monitoring grid frequency for contingency events .

**Offline detection**, or retrospective segmentation, is applied to a fixed, historical batch of data. The goal is to identify all change points within the dataset to partition it into homogeneous segments for further analysis. This is common in post-event analysis or when building models from historical energy consumption records.

These two paradigms involve different algorithms and present a fundamental trade-off between detection timeliness and accuracy.

#### Online Detection and the CUSUM Procedure

The theoretical foundation of many online detection methods is the **[likelihood ratio](@entry_id:170863)**. For a simple case where data shifts from a pre-change distribution $f_0(y)$ to a post-change distribution $f_1(y)$, the evidence provided by a single data point $y_t$ is captured by the **[log-likelihood ratio](@entry_id:274622)**:
$$
\ell(y_t) = \ln\left(\frac{f_1(y_t)}{f_0(y_t)}\right)
$$
For instance, if we are monitoring for a positive shift in the mean of a Gaussian process from $0$ to $\delta$ with known variance $\sigma^2$, the [log-likelihood ratio](@entry_id:274622) simplifies to a linear function of the observation :
$$
\ell(y_t) = \frac{\delta}{\sigma^2}y_t - \frac{\delta^2}{2\sigma^2}
$$
The **Cumulative Sum (CUSUM)** procedure, developed by E. S. Page, is a powerful online detection algorithm that works by accumulating this evidence over time. The CUSUM statistic $S_t$ is updated recursively:
$$
S_t = \max\{0, S_{t-1} + \ell(y_t)\}, \quad \text{with } S_0 = 0
$$
The statistic $S_t$ represents the maximum accumulated evidence for a change having occurred up to the present time $t$. An alarm is triggered when $S_t$ exceeds a pre-defined threshold $h$.

The choice of $h$ dictates the trade-off between two key performance metrics:
1.  **False Alarm Rate**: The frequency of raising an alarm when no change has occurred. This is related to the average run length (ARL) before a false alarm.
2.  **Detection Delay**: The time elapsed between the true change point $\tau$ and the detection time.

Increasing the threshold $h$ makes the test more conservative, increasing the average time to a false alarm but also increasing the expected detection delay. Conversely, a lower $h$ provides faster detection at the cost of more frequent false alarms .

For a finite monitoring horizon of $N$ hours, the threshold $h$ can be calibrated to ensure the probability of at least one false alarm is no more than a target level $\alpha$. Using properties of likelihood ratios as [martingales](@entry_id:267779), one can derive a bound on this probability, which leads to a simple and elegant rule for setting the threshold :
$$
h \approx \ln\left(\frac{N}{\alpha}\right)
$$
This allows operators to systematically balance detection sensitivity against the tolerance for false alarms in critical monitoring applications.

### Methods for Offline Segmentation

In the offline setting, we are given a complete time series $\{y_t\}_{t=1}^n$ and aim to find the optimal set of change points that partition the data. This is typically formulated as an optimization problem.

#### The Penalized Likelihood Framework

The standard approach is to find a segmentation that minimizes a total cost, which balances goodness-of-fit within segments against a penalty for [model complexity](@entry_id:145563) (i.e., the number of change points). The objective function is:
$$
J(t_1, \dots, t_{K-1}) = \sum_{k=1}^{K} \left( C(y_{t_{k-1}+1:t_k}) \right) + \beta K
$$
where $\{t_k\}_{k=1}^{K-1}$ are the change points (defining $K$ segments), $C(\cdot)$ is the cost of fitting a model to a segment, and $\beta > 0$ is a penalty for each segment.

The segment cost $C(\cdot)$ is often derived from the **[log-likelihood](@entry_id:273783)**. For a segment of data assumed to be Gaussian with a constant but unknown mean, the **Maximum Likelihood Estimator (MLE)** for the mean is simply the [sample mean](@entry_id:169249) of the data in that segment. The corresponding minimum cost ([negative log-likelihood](@entry_id:637801)) for the segment is proportional to the [residual sum of squares](@entry_id:637159) around that [sample mean](@entry_id:169249) . Thus, the optimization problem becomes a search for the segmentation that minimizes the total [sum of squared errors](@entry_id:149299) plus a penalty for the number of segments.

#### Optimal Segmentation via Dynamic Programming

This optimization problem can be solved exactly using **[dynamic programming](@entry_id:141107) (DP)**, a method often called **Optimal Partitioning**. Let $F(t)$ be the minimum cost for an optimal segmentation of the first $t$ data points. The solution is built upon the **[principle of optimality](@entry_id:147533)**: an optimal segmentation of $\{y_s\}_{s=1}^t$ must consist of an optimal segmentation of a prefix $\{y_s\}_{s=1}^\tau$ followed by a final segment from $\tau+1$ to $t$. By minimizing over all possible last change points $\tau$, we arrive at the DP recursion :
$$
F(t) = \min_{0 \le \tau < t} \left\{ F(\tau) + C(y_{\tau+1:t}) + \beta' \right\}
$$
where $\beta'$ is the penalty for introducing a new segment. The [base case](@entry_id:146682) is $F(0)=0$ (or $-\beta'$ depending on the exact penalty formulation). This recursion is solved for $t=1, \dots, n$. Since for each $t$, we must check all $t$ previous candidates for $\tau$, the total number of segment cost evaluations is $\sum_{t=1}^n t = \frac{n(n+1)}{2}$. This gives the algorithm a [time complexity](@entry_id:145062) of $O(n^2)$.

#### Accelerating Optimal Segmentation: The PELT Algorithm

While the $O(n^2)$ complexity of standard DP is often acceptable for small datasets, it can be prohibitive for the long time series common in energy systems. The **Pruned Exact Linear Time (PELT)** algorithm is a significant advancement that reduces the expected complexity to $O(n)$ without sacrificing [exactness](@entry_id:268999) .

PELT is based on the same DP [recursion](@entry_id:264696) but incorporates an efficient pruning step. The key insight is that if a potential last change point $\tau$ is suboptimal at the current time $t$, it may be possible to prove it will also be suboptimal for all future times $u > t$. This is possible if the cost function satisfies a specific inequality: for any $s < t < u$, there must exist a constant $K$ such that
$$
C(y_{s+1:u}) \ge C(y_{s+1:t}) + C(y_{t+1:u}) + K
$$
For many common costs, including the sum-of-squares cost for a Gaussian mean shift, this holds with $K=0$.

The PELT pruning condition is: if at time $t$, a candidate last change point $\tau$ satisfies
$$
F(\tau) + C(y_{\tau+1:t}) + K \ge F(t)
$$
then $\tau$ can be permanently removed from the set of candidates for all future steps. When the true change points occur with a roughly constant probability (a reasonable assumption in many systems), this pruning is so effective that the number of active candidates at each step remains small on average, leading to an expected linear [time complexity](@entry_id:145062).

#### Heuristic Methods: Binary Segmentation

Before the development of efficient exact methods like PELT, heuristic approaches were common. **Binary Segmentation** is a widely used greedy algorithm for multiple [change point detection](@entry_id:1122256). It works as follows :
1. Apply a single-change-point test to the entire dataset. If a significant change point is found, split the data at that location.
2. Recursively apply step 1 to the two new sub-segments.
3. Stop when no more significant change points are found in any segment.

The greedy nature of this algorithm—committing to the single "best" split at each stage without considering joint effects—makes it fast but suboptimal. It is susceptible to a failure mode known as **masking**. Imagine a scenario with a large, sudden change in net load followed closely by a smaller change of opposite sign (e.g., cloud cover suddenly reduces solar generation, then a [demand response](@entry_id:1123537) event slightly reduces load). Binary segmentation's first pass will be dominated by the large change and will likely place a split near it. In the subsequent recursion, the smaller change will be located very close to the new boundary of its sub-segment. Test statistics for change points are typically less powerful for changes near the edges of a segment. This poor localization, combined with the small magnitude of the change, can cause the test to lack power, and the smaller change is "masked" by the larger one and remains undetected. This illustrates the critical trade-off between computational speed and statistical accuracy in choosing a detection algorithm.

### Practical Considerations in Change Point Modeling

#### Model Selection and Penalty Choice

Offline segmentation methods based on penalized cost require a choice of the [penalty parameter](@entry_id:753318) $\beta$. This is equivalent to the statistical problem of model selection: choosing the number of segments, $m$. Several [information criteria](@entry_id:635818) have been proposed for this task. The goal is to find a criterion that is **consistent**, meaning it selects the true number of change points with probability tending to 1 as the data length $n \to \infty$.

For change point problems, consistency requires the penalty for adding a parameter to grow with $n$, but slower than the likelihood gain from a true change.
- The **Akaike Information Criterion (AIC)** uses a penalty that is constant with respect to $n$. This penalty is not strong enough to overwhelm the likelihood gain from fitting noise, so AIC is inconsistent and tends to overfit, selecting too many change points.
- The **Bayesian Information Criterion (BIC)** and the **Minimum Description Length (MDL)** principle both lead to penalties that are proportional to $\log n$. For example, a proper MDL formulation includes terms for encoding both the continuous parameter values and the discrete locations of the change points, resulting in a penalty that scales with $\log n$. This growth is sufficient to dominate the spurious likelihood gain from overfitting but is small enough relative to $n$ to remain sensitive to true changes. Thus, BIC and MDL are generally consistent for selecting the number of change points in a segmentation model .

#### Handling Seasonality and Autocorrelation

A major challenge in applying [change point detection](@entry_id:1122256) to real-world energy data is that it is rarely a simple sequence of [independent and identically distributed](@entry_id:169067) (i.i.d.) observations. Energy time series typically exhibit strong **seasonality** (e.g., daily and weekly cycles) and **autocorrelation** (short-term memory).

Applying classical tests like CUSUM, which assume i.i.d. data, directly to such series is a grave error. The presence of unmodeled positive autocorrelation dramatically inflates the **[long-run variance](@entry_id:751456)** of the [partial sums](@entry_id:162077) used in [test statistics](@entry_id:897871). The [long-run variance](@entry_id:751456) is approximately $\sigma^2(1 + 2\sum_{h=1}^\infty \rho(h))$, where $\rho(h)$ is the autocorrelation at lag $h$. A standard test that uses the marginal variance $\sigma^2$ will severely underestimate the true variability of its statistic, leading to overly narrow decision boundaries and a highly inflated Type I error rate (i.e., frequent false alarms) .

A rigorous procedure must be followed to account for these features:
1.  **Deseasonalize the Data**: First, remove any deterministic seasonal patterns. This can be done by taking seasonal differences (e.g., $X_t - X_{t-24}$ for hourly data) or by regressing the data on a set of harmonic terms (sines and cosines) at the seasonal frequencies.
2.  **Address Autocorrelation**: After deseasonalization, the remaining series may still be autocorrelated. There are two primary strategies to handle this:
    *   **Prewhitening**: Fit a suitable time series model (e.g., an ARMA or SARIMA model) to the deseasonalized series. The residuals from this model should be approximately uncorrelated (white noise). The [change point detection](@entry_id:1122256) test can then be validly applied to these residuals.
    *   **Test Correction**: Alternatively, apply the test to the autocorrelated (but deseasonalized) series, but adjust the [test statistic](@entry_id:167372) by replacing the standard variance estimate with a **Heteroskedasticity and Autocorrelation Consistent (HAC)** estimator of the [long-run variance](@entry_id:751456), such as the Newey-West estimator.

Failure to perform these adjustments will render the results of any change point analysis unreliable, underscoring the necessity of careful time series diagnostics before applying detection algorithms.