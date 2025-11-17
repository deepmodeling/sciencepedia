## Introduction
Analyzing economies with diverse households and aggregate risk poses a significant challenge due to the "[curse of dimensionality](@entry_id:143920)," as tracking the entire distribution of wealth is computationally intractable. The Krusell-Smith algorithm offers a breakthrough solution by assuming agents have [bounded rationality](@entry_id:139029), using simple, low-dimensional rules to forecast the economy's future path. This article provides a comprehensive guide to this powerful method. The first chapter, **Principles and Mechanisms**, details the algorithm's core iterative process and the economic logic behind approximate aggregation. Next, **Applications and Interdisciplinary Connections** explores how the framework provides crucial insights into the welfare costs of business cycles, [precautionary savings](@entry_id:136240), and even supply chain risk. Finally, **Hands-On Practices** presents practical exercises to solidify your understanding of its implementation.

## Principles and Mechanisms

The analysis of heterogeneous-agent economies with aggregate risk presents a formidable challenge. The state of such an economy is not merely a set of aggregate variables but the entire cross-sectional distribution of households over their individual states, such as wealth and idiosyncratic productivity. As this distribution is an infinite-dimensional object, solving for the economy's equilibrium dynamics via standard recursive methods is generally intractable. The Krusell-Smith algorithm provides a powerful and widely-used method to circumvent this "[curse of dimensionality](@entry_id:143920)" by postulating a form of [bounded rationality](@entry_id:139029) in how agents form expectations. This chapter elucidates the core principles of this method, explores its key economic implications, and details how the framework can be extended to accommodate more complex economic phenomena.

### The Core Mechanism: Approximate Aggregation

The foundational insight of the Krusell-Smith algorithm is that, for many economic questions, the full complexity of the cross-sectional distribution may be superfluous for forecasting future prices. Instead, the evolution of the economy might be well-approximated by the dynamics of a small number of aggregate variables, typically low-order moments of the distribution. The most common application uses only the mean of the asset distribution—the aggregate capital stock, $K_t$—along with the current state of aggregate productivity, $Z_t$.

The algorithm assumes that individual agents do not attempt to track the evolution of the entire distribution. Instead, they form expectations using a simple, low-dimensional forecasting rule for the aggregate capital stock. This is known as the **Perceived Law of Motion (PLM)**. A typical specification for the PLM is a log-linear function:
$$
\log K_{t+1} = \beta_0 + \beta_1 \log K_t + \beta_2 \log Z_t
$$
where the coefficients $(\beta_0, \beta_1, \beta_2)$ are what agents believe govern the economy's aggregate dynamics.

The algorithm then proceeds as a [fixed-point iteration](@entry_id:137769) to ensure these beliefs are consistent with the economy's actual outcomes:

1.  **Assume a PLM:** Begin with an initial guess for the coefficients of the PLM.

2.  **Solve the Household's Problem:** Given the PLM, each household can form expectations about future factor prices (the rental rate of capital and wages), which are functions of the future aggregate state $(K_{t+1}, Z_{t+1})$. With these expectations, the household solves its [dynamic optimization](@entry_id:145322) problem, yielding an individual [policy function](@entry_id:136948) for savings, $a_{i, t+1} = s(a_{i,t}, e_{i,t}; K_t, Z_t)$, where $a_i$ is individual assets and $e_i$ is the idiosyncratic shock.

3.  **Simulate the Economy:** Starting from some initial distribution of households, simulate the economy forward for a large number of periods. In each period, idiosyncratic and aggregate shocks are realized, and households make decisions according to their policy functions. Aggregating these individual savings decisions yields the actual next-period capital stock, $K_{t+1} = \int s(a, e; K_t, Z_t) d\Phi_t(a,e)$, where $\Phi_t$ is the cross-sectional distribution at time $t$. This simulation generates a time series for $(K_t, Z_t)$ that represents the **Actual Law of Motion (ALM)** implied by agents' behavior.

4.  **Update the PLM:** Use statistical methods, typically Ordinary Least Squares (OLS), to fit the PLM functional form to the simulated data. For example, one would regress the simulated $\log K_{t+1}$ on a constant, $\log K_t$, and $\log Z_t$ to obtain a new set of coefficients $(\beta'_0, \beta'_1, \beta'_2)$.

5.  **Iterate to Convergence:** Compare the new coefficients with the initial guess. If they are sufficiently close, a [rational expectations](@entry_id:140553) equilibrium has been found: the beliefs that agents use to make decisions are, on average, consistent with the aggregate outcomes of those decisions. If not, the new coefficients become the PLM for the next iteration, and the process repeats from Step 2.

### The Art and Science of State Variable Selection

The success of the Krusell-Smith algorithm hinges critically on the choices of which aggregate variables to include in the PLM and what functional form to use for the forecasting rule.

#### Informative State Variables

The aggregate variables included in the PLM must be sufficiently informative about the future evolution of the factor prices that determine household income. A variable that does not co-move with the business cycle or that remains constant is useless for forecasting. For example, consider a standard neoclassical model where capital goods can be produced one-for-one from consumption goods without adjustment costs. In such an environment, the equilibrium price of installed capital, $q_t$, must always equal its replacement cost, which is one unit of the consumption good (the numeraire). Therefore, $q_t=1$ for all $t$. If agents were to adopt a PLM for $\log q_{t+1}$, they would be forecasting a constant, $\log(1)=0$. This forecast provides no information about the future aggregate capital stock $K_{t+1}$ or productivity $Z_{t+1}$, making it impossible to form the expectations needed to solve the household's savings problem. This demonstrates that the choice of the forecasting variable is not arbitrary; it must be a variable that genuinely summarizes the state of the aggregate economy relevant to individual agents [@problem_id:2441720].

#### The Power of "Approximate Aggregation"

A remarkable finding in the original work by Krusell and Smith is that a simple PLM conditioning only on aggregate capital $K_t$ and the aggregate shock $Z_t$ provides an extremely accurate approximation of the true dynamics. The forecasting rule has an $R^2$ statistic very close to one. This phenomenon is known as **approximate aggregation**.

The reason for this surprising success lies in the interaction between household preferences and the highly [skewed distribution](@entry_id:175811) of wealth. In these models, a small fraction of wealthy households holds a large majority of the aggregate capital stock. Their savings decisions, therefore, disproportionately drive the evolution of $K_t$. If these wealthy households have preferences that exhibit **Decreasing Absolute Risk Aversion (DARA)**—a standard feature of CRRA utility functions—their precautionary saving motive weakens as they become richer. For very wealthy agents, consumption is high and smooth, and their saving behavior is primarily driven by the intertemporal substitution motive (i.e., reacting to the expected interest rate), much like a representative agent in a complete-markets model. Because the dynamics of aggregate capital are dominated by these "almost representative" agents, the complex, heterogeneous behavior of poorer, constrained households has only a minor impact on the aggregate. Consequently, the mean of the wealth distribution, $K_t$, becomes a sufficient statistic for the aggregate dynamics, justifying the simple, low-dimensional PLM [@problem_id:2441763].

While a log-linear functional form is the standard benchmark, the framework allows for more flexible specifications. Advanced implementations can use [non-parametric methods](@entry_id:138925), such as kernel regression or Gaussian processes, to let the data from the simulation reveal potentially important non-linearities or regime-switching dynamics in the ALM that a linear rule would miss [@problem_id:2441747].

### Key Economic Insights from Heterogeneity

The primary value of the Krusell-Smith framework is not merely as a computational tool, but for the fundamental economic insights it provides by taking heterogeneity and [market incompleteness](@entry_id:145582) seriously.

#### Amplified Welfare Costs of Business Cycles

In a Representative Agent (RA) model, the welfare cost of business cycles is typically found to be very small. This is because the aggregate consumption stream is relatively smooth. The KS framework reveals a starkly different picture. Even if the aggregate consumption path is identical to that in an RA model, the welfare costs of fluctuations are an order of magnitude larger. This is because aggregate statistics mask significant underlying heterogeneity. During a recession (a negative aggregate shock), not only does average consumption fall, but income risk and unemployment risk for individual households rise. Low-asset, borrowing-constrained households are forced to cut consumption sharply. Since their consumption is low, their marginal utility is very high. The total welfare cost, which is the integrated sum of individual welfare losses, is therefore heavily weighted toward these vulnerable households. Incomplete markets prevent them from insuring against these downturns, making recessions far more painful than they appear from an aggregate perspective [@problem_id:2441778].

#### Precautionary Savings and Higher-Order Risk

The model also provides a rich laboratory for studying [precautionary savings](@entry_id:136240). The precautionary motive is governed by the property of **prudence**, defined by a positive third derivative of the utility function, $u'''(c) > 0$. Prudence implies that uncertainty about future income leads agents to save more today as a buffer. CRRA preferences, for instance, exhibit prudence. This framework allows us to go beyond simple variance and analyze the impact of higher-order risk. Consider, for example, a change in the distribution of aggregate shocks from Gaussian to one with "[fat tails](@entry_id:140093)" (higher [kurtosis](@entry_id:269963)), holding mean and variance constant. A [fat-tailed distribution](@entry_id:274134) increases the probability of rare but severe disasters. For a prudent agent, the possibility of a catastrophic drop in future consumption—and thus an astronomically high future marginal utility—provides a powerful incentive to increase savings today. When all agents react this way, the aggregate capital stock in the economy rises. This shows that the threat of rare disasters can have a first-order impact on capital accumulation and macroeconomic aggregates [@problem_id:2441746].

### Extending the State Space: When Simple Aggregation Fails

While approximate aggregation using only $(K_t, Z_t)$ is remarkably effective in the benchmark model, it is an approximation whose validity can break down under alternative assumptions about the economy's structure. In such cases, the algorithm's flexibility allows the researcher to augment the state space of the PLM.

#### Changes in Factor Income Distribution

The simple PLM works well when factor prices can be expressed solely as functions of $(K_t, Z_t)$. This holds if the aggregate production function only depends on the sum of different inputs. Suppose, however, that the technology exhibits **capital-skill complementarity**, meaning capital is more complementary to high-skilled labor than to low-skilled labor. Mathematically, this means the cross-partial derivative of the production function with respect to capital and skilled labor is larger than that with respect to capital and unskilled labor. In this scenario, an increase in the aggregate capital stock will raise the wages of high-skilled workers more than the wages of low-skilled workers, thus widening the skill premium. Now, factor prices depend not just on the total amount of capital, but also on the composition of the labor force. The distribution of wealth across skill groups becomes a relevant aggregate state variable. An accurate PLM would then need to be augmented to include additional moments of the distribution, such as the share of capital held by skilled households, to track the evolution of relative prices [@problem_id:2441755].

#### Path Dependence and Hysteresis

The framework can also be adapted to capture non-Markovian dynamics, such as hysteresis. Suppose the true law of motion depends not just on the current state $K_t$, but also on the historical maximum of the capital stock, $M_t = \max_{s \le t} K_s$. This could arise, for instance, if investment triggers irreversible learning-by-doing effects. To solve such a model, the state space of the PLM is simply augmented to include this new variable:
$$
\log K_{t+1} = \beta_0 + \beta_1 \log K_t + \beta_2 \log Z_t + \beta_3 \log M_t
$$
Furthermore, the simulation step of the algorithm must include the law of motion for the new state variable itself, which in this case is its [recursive definition](@entry_id:265514): $M_{t+1} = \max\{M_t, K_{t+1}\}$. This demonstrates the modularity of the Krusell-Smith approach in accommodating more complex and path-dependent aggregate dynamics [@problem_id:2441759].

### Beliefs, Information, and Expectation Formation

The Krusell-Smith algorithm is fundamentally a model of expectation formation. Its structure can be readily adapted to explore environments with richer informational assumptions.

#### Imperfect Information and Filtering

In the [standard model](@entry_id:137424), the aggregate shock $Z_t$ is perfectly observed by all agents. If, instead, agents observe only a noisy public signal of the shock, the problem becomes one of signal extraction. To maintain a tractable, recursive structure, an agent's state must be augmented with their **belief** about the unobserved shock. In a standard linear-Gaussian setup, this belief is fully summarized by its posterior mean and variance. The evolution of this belief is governed by the laws of Bayesian filtering (e.g., the Kalman filter). Since the signal is public, all agents share the same belief. The aggregate state of the economy thus becomes $(K_t, \hat{Z}_t, P_t^Z)$, where $\hat{Z}_t$ and $P_t^Z$ are the common [posterior mean](@entry_id:173826) and variance of the shock. The PLM must then be modified to condition on these belief states, as they are the variables that agents actually use to form expectations about the future [@problem_id:2441756].

#### Heterogeneous Beliefs

The framework can also incorporate persistent disagreement among agents. Suppose there are different types of agents, each with a different subjective belief about the [transition probabilities](@entry_id:158294) of the aggregate shock. When confronted with a common history of aggregate data, how does the learning procedure evolve? The estimation step of the algorithm is purely statistical. Since all agents observe the same public data $(K_t, Z_t)$ and use the same statistical method (OLS) to estimate the PLM's coefficients, they will all arrive at the **same estimated PLM**. However, their behavior will differ. When solving their optimization problems, each agent type uses its own [subjective probability](@entry_id:271766) matrix to weigh future possibilities, leading to different savings policy functions. The aggregate law of motion is then a mixture of these different behaviors. The resulting equilibrium is a state where all agents agree on the best-fit [statistical forecasting](@entry_id:168738) rule for aggregate capital, yet the data they are fitting is itself generated by their fundamental disagreements about the underlying structure of the economy [@problem_id:2441722]. This principle can be extended to even more complex environments, such as those with local network effects, where agents' forecasts are influenced by the behavior of their peers [@problem_id:2441769].