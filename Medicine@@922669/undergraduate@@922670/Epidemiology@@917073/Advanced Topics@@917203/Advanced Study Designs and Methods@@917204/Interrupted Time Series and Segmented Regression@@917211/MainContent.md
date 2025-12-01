## Introduction
When randomized controlled trials are not feasible for evaluating large-scale policies, how can we rigorously measure their impact? Interrupted Time Series (ITS) analysis, implemented through segmented regression, offers a powerful quasi-experimental solution. This method is crucial in fields like public health for assessing the effects of new laws or health initiatives on population-level outcomes. The primary challenge it addresses is the inadequacy of simple pre-post comparisons, which often fail to account for pre-existing trends, leading to flawed conclusions. By modeling the outcome's trajectory before an intervention, ITS creates a robust counterfactual—what would have happened without the intervention—allowing for a more accurate estimation of causal effects.

This article will guide you through the theory and practice of ITS analysis. In the first chapter, **Principles and Mechanisms**, you will learn the fundamental logic of ITS and the statistical mechanics of segmented regression, including how to interpret its key parameters. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the method's real-world utility in public health and clinical research, showcasing how to adapt the model for complex data challenges like seasonality and confounding. Finally, the **Hands-On Practices** section will provide foundational exercises to solidify your understanding of the statistical concepts that underpin this powerful analytical tool.

## Principles and Mechanisms

In the evaluation of public health interventions, policies, and large-scale programs, randomized controlled trials are often infeasible or unethical. In their absence, quasi-experimental designs provide a rigorous framework for estimating causal effects. Among the strongest of these designs is the **Interrupted Time Series (ITS)** analysis. This chapter delineates the principles and statistical mechanisms underpinning the ITS method, focusing on its most common implementation: **segmented [regression analysis](@entry_id:165476)**.

### The Logic of Interrupted Time Series

The Interrupted Time Series design leverages longitudinal data to assess the impact of an intervention that is introduced at a specific, known point in time. At its core, ITS is a sophisticated extension of a simple pre-post analysis. Whereas a simple pre-post comparison examines the average outcome level before and after an intervention, it remains vulnerable to confounding by pre-existing trends. For instance, if injury rates were already declining, a simple pre-post comparison might wrongly attribute the entire post-intervention drop to a new safety law, when much of it was part of an ongoing trend.

ITS overcomes this limitation by utilizing a series of observations over time—a **time series**—both before and after the intervention. By modeling the trend in the pre-intervention period, the design establishes a trajectory for the outcome of interest. The fundamental logic of ITS is to project this pre-intervention trend into the post-intervention period. This projection serves as the **counterfactual**: an estimate of what would have happened to the outcome had the intervention *not* occurred. The causal effect of the intervention is then estimated by comparing the observed post-intervention data to this counterfactual projection.

### Modeling the Interruption: Segmented Regression Analysis

The standard statistical method for implementing an ITS analysis is **segmented regression**. This approach fits a [regression model](@entry_id:163386) to the time series data, with the model being "segmented" or allowed to change at the point of the intervention. Let us consider a typical public health scenario: evaluating a new city ordinance intended to reduce a specific type of injury. We have monthly counts of this injury, denoted as $Y_t$, for a series of months $t=1, \dots, T$. The ordinance was enacted at a known time, which we will call $T_0$.

To model the effect of this ordinance, we construct a [linear regression](@entry_id:142318) model that can capture two primary types of effects: an immediate change in the level of the outcome, and a change in its long-term trend. The model is specified as follows:

$$E[Y_t] = \beta_0 + \beta_1 t + \beta_2 A_t + \beta_3 P_t$$

Let us define each component of this model:
*   $Y_t$ is the outcome of interest at time $t$.
*   $t$ is a continuous variable representing time from the start of the observation period (e.g., month 1, 2, 3, ...).
*   $A_t$ is an indicator variable, or dummy variable, that represents the intervention period. It takes the value $0$ for all time points before the intervention ($t  T_0$) and the value $1$ for all time points during and after the intervention ($t \ge T_0$).
*   $P_t$ is a continuous variable that tracks the time elapsed *since* the intervention. It is coded as $0$ for the pre-intervention period ($t  T_0$) and as $t - T_0$ for the post-intervention period ($t \ge T_0$). This variable is effectively an interaction between time and the intervention.

To understand how this model works, we can examine the expected value of $Y_t$ in each segment.

**Before the Intervention ($t  T_0$):**
In this period, both $A_t$ and $P_t$ are equal to zero. The model simplifies to:
$$E[Y_t] = \beta_0 + \beta_1 t$$
This is a simple linear model where $\beta_0$ is the intercept at time $t=0$ and $\beta_1$ is the slope, representing the baseline trend of the outcome before the ordinance was introduced.

**After the Intervention ($t \ge T_0$):**
In this period, $A_t=1$ and $P_t = t - T_0$. The model is:
$$E[Y_t] = \beta_0 + \beta_1 t + \beta_2(1) + \beta_3(t - T_0)$$
To better interpret this, we can rearrange the terms by grouping the intercept and the slope components:
$$E[Y_t] = (\beta_0 + \beta_2 - \beta_3 T_0) + (\beta_1 + \beta_3)t$$
This reveals that the post-intervention segment is also a line, but with a new intercept, $(\beta_0 + \beta_2 - \beta_3 T_0)$, and a new slope, $(\beta_1 + \beta_3)$.

### Interpreting Model Parameters as Causal Effects

The power of the segmented regression model lies in the direct interpretation of the coefficients $\beta_2$ and $\beta_3$ as the effects of the intervention.

*   **$\beta_2$: The Immediate Level Change.** The coefficient $\beta_2$ quantifies the immediate impact of the intervention. It represents the abrupt "jump" or "drop" in the outcome level that occurs at the exact time of the intervention, $T_0$. To see this formally, consider the value of the outcome at $t=T_0$. The pre-intervention line, projected to this point, would be $\beta_0 + \beta_1 T_0$. The post-intervention line starts at $t=T_0$. At this point, $P_{T_0} = T_0 - T_0 = 0$, so the model gives $E[Y_{T_0}] = \beta_0 + \beta_1 T_0 + \beta_2$. The difference between these two values is precisely $\beta_2$. In our example, a statistically significant negative $\beta_2$ would suggest the ordinance caused an immediate reduction in injuries.

*   **$\beta_3$: The Change in Trend.** The coefficient $\beta_3$ captures the sustained or long-term impact of the intervention on the outcome's trajectory. It represents the change in the slope of the time series after the intervention, compared to the slope before it. As we derived, the pre-intervention slope is $\beta_1$ and the post-intervention slope is $\beta_1 + \beta_3$. Therefore, $\beta_3$ is the difference between these two slopes. In our injury example, a significant negative $\beta_3$ would imply that, after its introduction, the ordinance caused injuries to decline at a faster rate than they were before (or to increase at a slower rate).

These two parameters, $\beta_2$ and $\beta_3$, thus provide a nuanced picture of the intervention's impact, separating its immediate shock from its effect on the longer-term trend.

### Assumptions for Causal Inference

The ability to interpret $\beta_2$ and $\beta_3$ as **causal effects** is not automatic; it rests on a critical set of assumptions. The central assumption of ITS analysis is that the pre-intervention trend provides a valid representation of the counterfactual trajectory in the post-intervention period [@problem_id:4626179]. Using the potential outcomes framework, let $Y_t(1)$ be the outcome at time $t$ if the intervention occurs, and $Y_t(0)$ be the potential outcome if it does not. We observe $Y_t = Y_t(0)$ for $t  T_0$ and $Y_t = Y_t(1)$ for $t \ge T_0$. The causal inference relies on the assumption that the unobserved counterfactual mean, $E[Y_t(0)]$ for $t \ge T_0$, can be accurately predicted by extrapolating the pre-intervention trend: $E[Y_t(0)] = \beta_0 + \beta_1 t$.

For this central assumption to be plausible, several threats to the validity of the design must be ruled out:

1.  **No Concurrent Interventions:** No other events or interventions that could plausibly affect the outcome $Y_t$ must have occurred at or around the same time $T_0$. If another policy change happened concurrently, it becomes impossible to disentangle its effects from the intervention under study.

2.  **Absence of Anticipatory Effects:** The analysis assumes that the pre-intervention trend is not distorted by anticipation of the intervention. If, for example, news of the impending ordinance caused people to change their behavior before the law was officially enacted, the baseline trend $\beta_1$ would be biased, invalidating the counterfactual projection.

3.  **Stability of the System:** The nature of the outcome measurement and the composition of the population under study must remain stable throughout the observation period, apart from the intervention itself. An abrupt change in how injuries are recorded or a sudden shift in population demographics at time $T_0$ could create an artificial "interruption" in the time series.

4.  **Correct Model Specification:** The model chosen must adequately describe the data. While the linear model presented is common, the true underlying trend may be non-linear. Furthermore, time series data are often characterized by **autocorrelation**, where the observation at time $t$ is correlated with the observation at time $t-1$. Standard regression assumes [independent errors](@entry_id:275689), and violating this assumption can lead to incorrect standard errors and p-values. It is crucial to test for and, if necessary, adjust for autocorrelation using techniques like Autoregressive Integrated Moving Average (ARIMA) models or [generalized least squares](@entry_id:272590). The model should also include terms to control for other patterns, such as **seasonality**, if present.

5.  **Stable Unit Treatment Value Assumption (SUTVA):** As with all causal inference, SUTVA must hold. This implies that the intervention is well-defined and that there is no interference between units. In a single-series ITS, this primarily means the effect of the ordinance on the city is self-contained and consistent.

When these assumptions are reasonably met, the Interrupted Time Series design provides a powerful and transparent method for evaluating the causal impact of interventions in the real world.