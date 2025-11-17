## Introduction
In modern finance, risk models like Value-at-Risk (VaR) and Expected Shortfall (ES) are indispensable tools for quantifying potential losses. However, a model's forecast is meaningless without a rigorous process of verification. This is the critical role of [backtesting](@entry_id:137884): the statistical procedure of comparing a model's risk predictions against actual outcomes to determine its accuracy and reliability. This article addresses the fundamental challenge of how to properly validate these risk models, moving from established techniques for VaR to the more complex and evolving methods required for ES.

This guide will provide a structured journey through the theory and practice of [backtesting](@entry_id:137884). In the first chapter, **Principles and Mechanisms**, we will dissect the statistical foundations, starting with the classic coverage and independence tests for VaR and progressing to the theoretical hurdles and advanced solutions for [backtesting](@entry_id:137884) ES. Next, **Applications and Interdisciplinary Connections** will contextualize these methods, exploring their use in regulatory frameworks, their power in diagnosing model failures during market crises, and their adaptation to complex financial instruments. Finally, **Hands-On Practices** will offer the opportunity to solidify these concepts by working through practical simulations that highlight common pitfalls and advanced techniques. By the end, you will not only understand the mechanics of [backtesting](@entry_id:137884) but also appreciate its role as a cornerstone of robust [financial risk management](@entry_id:138248).

## Principles and Mechanisms

### Foundational Concepts: VaR, ES, and Coherence

Before delving into the mechanisms of [backtesting](@entry_id:137884), it is crucial to solidify our understanding of the risk measures themselves: Value-at-Risk (VaR) and Expected Shortfall (ES). While the previous chapter introduced these concepts, a focused review of their properties reveals why the financial and regulatory communities have increasingly favored ES.

**Value-at-Risk (VaR)** at a [confidence level](@entry_id:168001) $c$ (e.g., $0.99$) is the maximum loss that is not expected to be exceeded over a given horizon with that level of confidence. If we denote the loss random variable as $L$ and its [cumulative distribution function](@entry_id:143135) as $F_L(l) = P(L \le l)$, then the VaR is the $c$-quantile of the loss distribution. Letting $\alpha = 1-c$ be the [tail probability](@entry_id:266795) (e.g., $0.01$), we can define VaR as:
$$
\mathrm{VaR}_{c}(L) = \inf \{l \in \mathbb{R} : P(L > l) \le \alpha \}
$$
In essence, VaR provides a single threshold. It answers the question: "How bad can things get with probability $\alpha$?" However, it provides no information about the severity of losses *when* that threshold is breached.

**Expected Shortfall (ES)**, also known as Conditional Value-at-Risk (CVaR), directly addresses this shortcoming. ES at [confidence level](@entry_id:168001) $c$ is the expected value of the loss, conditional on the loss exceeding the VaR at that same level. Formally:
$$
\mathrm{ES}_{c}(L) = E[L \mid L > \mathrm{VaR}_{c}(L)]
$$
ES answers a different, often more relevant, question: "If things do get bad, what is our expected loss?" By averaging over all losses in the tail, ES provides a more complete picture of the [tail risk](@entry_id:141564) than VaR.

The theoretical superiority of ES stems from its properties as a **[coherent risk measure](@entry_id:137862)**. A risk measure $\rho(\cdot)$ is deemed coherent if it satisfies four axioms: [translation invariance](@entry_id:146173), [positive homogeneity](@entry_id:262235), monotonicity, and, most critically, **[subadditivity](@entry_id:137224)**. The [subadditivity](@entry_id:137224) axiom states that for any two portfolios with losses $L_1$ and $L_2$:
$$
\rho(L_1 + L_2) \le \rho(L_1) + \rho(L_2)
$$
This axiom is the mathematical embodiment of the principle of diversification: the risk of a combined portfolio should be no greater than the sum of the risks of its components. ES is a [coherent risk measure](@entry_id:137862), satisfying [subadditivity](@entry_id:137224) for all loss distributions. In contrast, VaR is famously **not coherent** because it can violate [subadditivity](@entry_id:137224), particularly for portfolios with non-elliptical or skewed loss distributions (such as those containing options). This failure means that under a VaR framework, merging two business units could paradoxically appear to increase total risk, creating perverse incentives against diversification. This fundamental theoretical weakness is a primary driver for the regulatory shift toward ES [@problem_id:2447012].

### Backtesting Value-at-Risk (VaR): From Coverage to Independence

Backtesting is the process of statistically verifying whether a risk model’s forecasts are consistent with subsequent realized outcomes. For a VaR model, the core principle is straightforward. Let $\{v_t\}_{t=1}^T$ be a sequence of one-day-ahead VaR forecasts at level $c$, and let $\{L_t\}_{t=1}^T$ be the corresponding realized losses. We can define a sequence of **exceedance indicators**, or "hits":
$$
I_t = \begin{cases} 1  \text{if } L_t > v_t \\ 0  \text{if } L_t \le v_t \end{cases}
$$
If the VaR model is correctly specified, the exceedance indicator series $\{I_t\}$ should behave as an [independent and identically distributed](@entry_id:169067) (i.i.d.) Bernoulli sequence with parameter $p = 1-c = \alpha$. This implies two distinct, testable properties:
1.  **Unconditional Coverage**: The probability of an exceedance on any given day is $\alpha$.
2.  **Independence**: Exceedances are independent of each other over time. An exceedance today should not provide any information about the likelihood of an exceedance tomorrow.

#### Unconditional Coverage: The Kupiec Test

The most basic backtest, proposed by Kupiec (1995), focuses solely on the unconditional coverage property. The **proportion of failures (POF) test** evaluates the null hypothesis $H_0: p = \alpha$ against the alternative $H_A: p \ne \alpha$. It compares the number of observed exceedances, $x = \sum I_t$, with the number expected, $T\alpha$. The test is based on a [likelihood ratio](@entry_id:170863) statistic:
$$
LR_{uc} = 2 \ln \left( \frac{(1-\hat{p})^{T-x}\hat{p}^x}{(1-\alpha)^{T-x}\alpha^x} \right)
$$
where $\hat{p} = x/T$ is the empirical exceedance rate. Under the null hypothesis, $LR_{uc}$ is asymptotically distributed as a chi-square ($\chi^2$) random variable with one degree of freedom.

While simple and intuitive, the Kupiec test suffers from a critical flaw: it is completely blind to the temporal pattern of exceedances. Consider a bank whose VaR model is evaluated over $T=1000$ days at $\alpha=0.01$. The expected number of exceedances is $10$. If the bank reports exactly $x=10$ exceedances, its empirical rate $\hat{p}$ is $0.01$, perfectly matching $\alpha$. The $LR_{uc}$ statistic will be zero, and the model will pass the Kupiec test with flying colors. However, if all $10$ of these exceedances occurred consecutively during a 10-day period of market crisis, the model is clearly failing precisely when it is most needed. The Kupiec test cannot detect this dangerous clustering of violations, potentially misleading regulators about the true risk exposure [@problem_id:2374183].

#### Conditional Coverage: The Christoffersen Test

To address the weakness of the Kupiec test, Christoffersen (1998) proposed a more powerful framework that jointly tests for both correct unconditional coverage and independence. This **conditional coverage test** consists of three components built on likelihood ratios:
1.  **Unconditional Coverage Test ($LR_{uc}$)**: This is identical to the Kupiec test.
2.  **Independence Test ($LR_{ind}$)**: This test specifically checks for serial dependence. It models the exceedance series $\{I_t\}$ as a first-order Markov chain and tests the null hypothesis that the probability of an exceedance tomorrow is independent of whether an exceedance occurred today. That is, $P(I_t=1 | I_{t-1}=1) = P(I_t=1 | I_{t-1}=0)$. A rejection of this null suggests that exceedances are clustered.
3.  **Conditional Coverage Test ($LR_{cc}$)**: This is the joint test of both properties. A key property of the likelihood ratio framework is that the joint [test statistic](@entry_id:167372) is simply the sum of the individual components: $LR_{cc} = LR_{uc} + LR_{ind}$. Under the joint null hypothesis, $LR_{cc}$ is asymptotically distributed as $\chi^2(2)$.

This framework is far more informative. A model that systematically underestimates risk after large shocks will produce clustered exceedances, causing it to fail the [independence test](@entry_id:750606) and, consequently, the conditional coverage test, even if its long-run average number of exceedances is correct [@problem_id:2374196]. Conversely, an overly conservative model that produces too few, but independent, exceedances might fail the $LR_{uc}$ test but pass the $LR_{ind}$ test [@problem_id:2374196].

#### Backtesting as Statistical Inference: Errors and Power

It is essential to remember that [backtesting](@entry_id:137884) is a form of [statistical hypothesis testing](@entry_id:274987) and is subject to the same limitations and nuances.

First, there is the risk of **Type I error**: rejecting a correctly specified model by pure chance. A test with a [significance level](@entry_id:170793) of $0.05$ will, by design, incorrectly reject a valid model approximately $5\%$ of the time in the long run. However, for the finite sample sizes used in practice, the actual Type I error rate may differ from the nominal significance level. This is because the test statistics are based on a discrete number of exceedances, while the critical values are derived from a continuous [asymptotic distribution](@entry_id:272575) (the $\chi^2$ distribution). One can compute the exact finite-sample error rate by summing the binomial probabilities of all outcomes that would lead to a rejection, revealing the true performance of the test for a given sample size [@problem_id:2374164].

Second, and arguably more critical in practice, is the issue of **[statistical power](@entry_id:197129)**. Power is the probability of correctly rejecting a misspecified model (the complement of Type II error). A low-power test is one that is unlikely to detect a bad model. The power of VaR backtests deteriorates dramatically as the [confidence level](@entry_id:168001) $c$ increases. For a VaR at the $c=0.999$ level ($\alpha=0.001$), one expects only one exceedance every 1000 days. With such a small number of expected data points (exceedances), it becomes statistically very difficult to distinguish a model whose true exceedance rate is $0.001$ from one whose rate is, for instance, $0.002$, even though the latter implies double the risk. For a fixed sample size, increasing the VaR [confidence level](@entry_id:168001) severely reduces the power of backtests, posing a significant practical challenge for [model validation](@entry_id:141140) [@problem_id:2374176].

### Beyond Binary Outcomes: Backtesting with Loss Functions

The hit-based tests of Kupiec and Christoffersen are limited because they treat all exceedances equally, regardless of their magnitude. An exceedance of one dollar is counted the same as an exceedance of one million dollars. A more sophisticated approach is to use a **[loss function](@entry_id:136784)** (or **[scoring function](@entry_id:178987)**) that penalizes forecasts based on the size of the error.

For a quantile forecast like VaR, the natural choice is the **quantile [loss function](@entry_id:136784)**, also known as the "check" function. For a VaR forecast $v_t$ for a loss $L_t$ at [tail probability](@entry_id:266795) $\alpha$, the forecast error is $u_t = L_t - v_t$. The quantile loss is:
$$
\ell_{\alpha}(u_t) = (\alpha - \mathbf{1}\{u_t  0\}) u_t
$$
Let's analyze this function's behavior:
-   **When an exceedance occurs ($L_t  v_t \implies u_t  0$):** The indicator $\mathbf{1}\{u_t  0\}$ is $0$, and the loss is $\alpha u_t$. The penalty is proportional to the magnitude of the shortfall, weighted by the small probability $\alpha$.
-   **When no exceedance occurs ($L_t \le v_t \implies u_t \le 0$):** The indicator is $1$ (for $u_t  0$), and the loss is $(\alpha - 1) u_t = (1-\alpha)(-u_t)$. This penalizes overly conservative forecasts where $v_t$ was much larger than the realized loss $L_t$. The penalty is proportional to the size of the over-prediction, weighted by the large probability $1-\alpha$.

A key property of this function is that the true conditional $\alpha$-quantile of the loss distribution is the unique value that minimizes the expected quantile loss. Therefore, by calculating the average quantile loss, $\overline{L}_{\alpha} = \frac{1}{T} \sum_{t=1}^T \ell_{\alpha}(L_t - v_t)$, we obtain a single metric that evaluates the overall quality of the VaR forecasts, accounting for both frequency and magnitude of errors [@problem_id:2446219]. Models with lower average quantile loss are preferred.

### The Challenge of Backtesting Expected Shortfall (ES)

While [backtesting](@entry_id:137884) VaR is relatively straightforward, [backtesting](@entry_id:137884) ES presents significant theoretical and practical challenges.

A common misconception is that a model with accurate ES forecasts should also pass a VaR backtest. This is not necessarily true. It is possible to construct a scenario where a model's ES forecast is highly accurate, yet it systematically fails a VaR backtest. For example, a simulation can be designed where the true frequency of tail losses is double the rate assumed by the model, causing it to fail an unconditional coverage test. However, the distribution of those tail losses can be engineered (e.g., using a Generalized Pareto Distribution) such that their conditional average perfectly matches the model's ES forecast. This demonstrates that correctly modeling the frequency of [tail events](@entry_id:276250) (VaR) and correctly modeling the average magnitude of [tail events](@entry_id:276250) (ES) are two distinct problems [@problem_id:2374170].

#### The Elicitability Problem

The fundamental difficulty in [backtesting](@entry_id:137884) ES lies in a theoretical property known as **elicitability**. A risk measure is "elicitable" if it is the unique minimizer of the expectation of some [scoring function](@entry_id:178987). As we saw, VaR is elicitable with respect to the quantile [loss function](@entry_id:136784). However, Gneiting (2011) showed that ES is **not elicitable** on its own. This implies there is no [scoring function](@entry_id:178987) that can be used to directly evaluate and compare competing ES forecasts in the same way we can for VaR.

The crucial breakthrough was the discovery that the pair $(\mathrm{VaR}, \mathrm{ES})$ is **jointly elicitable**. This means we must evaluate forecasts of VaR and ES together. There exists a class of consistent [scoring functions](@entry_id:175243) $S(v, e; y)$ for a VaR forecast $v$, an ES forecast $e$, and a realized loss $y$. One such family of functions, proposed by Fissler and Ziegel (2016), is:
$$
S(v,e;y) = (\mathbf{1}\{y  v\} - (1-\alpha))v - \mathbf{1}\{y  v\}\frac{y}{\alpha}e + \frac{1}{2\alpha}e^2 + \dots
$$
(The full form is more complex). The critical implication of this joint elicitability is that the ranking of competing ES models can be ambiguous. Different choices of a valid [scoring function](@entry_id:178987) can lead to different model rankings. For instance, a simulation comparing a [historical simulation](@entry_id:136441) model with a Normal distribution-based model for the (VaR, ES) pair can show that one model is preferred under one [scoring function](@entry_id:178987), while the other is preferred under a different one [@problem_id:2374159]. This is not a flaw in the theory but a deep truth: evaluating ES requires specifying preferences about the trade-offs between VaR accuracy and ES accuracy.

#### Practical Backtests for ES

Despite the theoretical complexities, several practical methods for [backtesting](@entry_id:137884) ES have been developed.

One major class of tests, such as the **Fissler-Ziegel (FZ) test**, is derived directly from the theory of joint [scoring functions](@entry_id:175243). These functions give rise to "identification functions" or "[moment conditions](@entry_id:136365)"—vectors whose expectation must be zero if the model is correctly specified. For the (VaR, ES) pair, one such vector is:
$$
g_t =\begin{pmatrix} \mathbf{1}\{L_t  v\} - \alpha \\ \mathbf{1}\{L_t  v\} \frac{L_t}{\alpha} - e \end{pmatrix}
$$
A more robust version is also available [@problem_id:2374158]. A backtest can be constructed by forming a Wald statistic based on the sample average of these vectors, $\bar{g} = \frac{1}{T}\sum g_t$, to test if it is statistically different from zero. This provides a formal joint test of the VaR and ES forecasts [@problem_id:2374158].

A second, more intuitive class of tests, pioneered by Acerbi and Szekely, focuses on a direct property of ES. If an ES forecast $\hat{e}_t$ is correct, the average of the "secured positions" ($S_t = L_t - \hat{e}_t$) that fall in the VaR tail should be zero. The **Acerbi-Szekely (AS) [test statistic](@entry_id:167372)** is simply this tail average:
$$
T_{\mathrm{AS}} = \frac{1}{|\mathcal{E}|}\sum_{t \in \mathcal{E}} (L_t - \hat{e}_t)
$$
where $\mathcal{E} = \{t: L_t  v_t\}$ is the set of exceedances. A simple decision rule is to reject the model if $T_{\mathrm{AS}}$ is positive (since for losses $L$, ES is a positive number representing the expected loss amount, a positive statistic implies $L_t  \hat{e}_t$ on average in the tail, meaning risk is underestimated).

This simple rule provides no p-value. To create a formal hypothesis test, one can use **bootstrapping**. This powerful non-parametric technique allows us to simulate the distribution of the $T_{\mathrm{AS}}$ statistic under the null hypothesis. By repeatedly [resampling](@entry_id:142583) from the observed (centered) data and recomputing the statistic, we can build an [empirical distribution](@entry_id:267085) and calculate a p-value for our originally observed statistic. This allows for rigorous statistical inference without relying on complex [asymptotic theory](@entry_id:162631), which is especially useful in the context of rare [tail events](@entry_id:276250) [@problem_id:2374204].