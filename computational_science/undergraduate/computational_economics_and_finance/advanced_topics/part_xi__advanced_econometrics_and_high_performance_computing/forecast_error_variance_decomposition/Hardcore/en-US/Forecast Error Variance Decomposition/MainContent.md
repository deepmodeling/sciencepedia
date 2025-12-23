## Introduction
Forecast Error Variance Decomposition (FEVD) is a cornerstone technique in [time-series analysis](@entry_id:178930), designed specifically to dissect and quantify the sources of uncertainty in dynamic systems. While a forecast provides a single-[point estimate](@entry_id:176325) of the future, the FEVD offers a richer story, attributing the variance of forecast errors to the fundamental, unpredictable shocks that drive the system. This moves the analysis from mere prediction to structured explanation, answering the critical question: "What factors are responsible for the uncertainty in my forecast?" Understanding these drivers is essential for building coherent economic narratives, managing risk, and making informed policy decisions.

This article provides a comprehensive guide to understanding and applying FEVD. In the first chapter, **Principles and Mechanisms**, we will unpack the mathematical foundations of the decomposition, exploring how correlated forecast innovations are transformed into economically meaningful [structural shocks](@entry_id:136585). The second chapter, **Applications and Interdisciplinary Connections**, demonstrates the technique's versatility by showcasing its use in fields ranging from macroeconomic policy and [financial risk management](@entry_id:138248) to [epidemiology](@entry_id:141409) and [climate science](@entry_id:161057). Finally, the **Hands-On Practices** chapter provides concrete exercises to solidify these concepts, allowing you to apply the theory and interpret the results in practical scenarios.

## Principles and Mechanisms

In the study of dynamic systems, a central goal is to understand not just how to forecast future outcomes, but also to attribute the uncertainty surrounding those forecasts to its various sources. Within the framework of Vector Autoregressions (VARs), the Forecast Error Variance Decomposition (FEVD) is the principal tool for this purpose. It provides a quantitative breakdown of the uncertainty in each variable's forecast, apportioning it to the fundamental, unpredictable "shocks" that drive the system's evolution. This chapter delves into the principles and mechanisms that underpin the construction and interpretation of the FEVD.

### From Forecast Error to Variance Decomposition

Consider a stable $n$-variable VAR model of order $p$, or VAR($p$), which describes the evolution of a vector of variables $y_t$:
$$
y_t = c + A_1 y_{t-1} + \dots + A_p y_{t-p} + u_t
$$
Here, $c$ is a vector of intercepts, $A_i$ are $n \times n$ coefficient matrices, and $u_t$ is the vector of one-step-ahead forecast errors, or **innovations**. These innovations are assumed to be serially uncorrelated with a [zero mean](@entry_id:271600) and a constant, symmetric, positive-definite covariance matrix $\Sigma_u = \mathbb{E}[u_t u_t']$.

The optimal $h$-step-ahead forecast of $y_{t+h}$ made at time $t$ is the conditional expectation, $\mathbb{E}_t[y_{t+h}]$. The error associated with this forecast is the difference between the actual outcome and the forecast: $e_{t+h|t} = y_{t+h} - \mathbb{E}_t[y_{t+h}]$. Using the moving-average (MA) representation of the VAR process, $y_t = \sum_{s=0}^\infty \Phi_s u_{t-s}$ (where $\Phi_s$ are the impulse response matrices), this forecast error can be expressed as a [linear combination](@entry_id:155091) of future innovations:
$$
e_{t+h|t} = \sum_{s=0}^{h-1} \Phi_s u_{t+h-s}
$$
The variance of this forecast error is captured by the Mean Squared Error (MSE) matrix, $\Sigma_y(h) = \mathbb{E}[e_{t+h|t} e_{t+h|t}']$, which is given by:
$$
\Sigma_y(h) = \sum_{s=0}^{h-1} \Phi_s \Sigma_u \Phi_s'
$$
The diagonal elements of $\Sigma_y(h)$ represent the forecast [error variance](@entry_id:636041) for each individual variable. However, because the components of the [innovation vector](@entry_id:750666) $u_t$ are typically correlated (i.e., the off-diagonal elements of $\Sigma_u$ are non-zero), the contributions of different innovations to this variance are entangled. To meaningfully decompose the variance, we must first transform the correlated innovations into a set of uncorrelated **[structural shocks](@entry_id:136585)**.

### The Role of Orthogonalization: Identifying Structural Shocks

The goal of [orthogonalization](@entry_id:149208) is to identify a set of underlying, mutually uncorrelated [structural shocks](@entry_id:136585), $\varepsilon_t$, which are assumed to have an identity covariance matrix ($\mathbb{E}[\varepsilon_t \varepsilon_t'] = I$). These shocks are related to the observable reduced-form innovations $u_t$ through an invertible impact matrix $S$:
$$
u_t = S \varepsilon_t
$$
Substituting this into the definition of the covariance matrix $\Sigma_u$ yields $\Sigma_u = \mathbb{E}[(S \varepsilon_t)(S \varepsilon_t)'] = S \mathbb{E}[\varepsilon_t \varepsilon_t'] S' = S S'$. The identification problem is that for any given $\Sigma_u$, there are infinitely many matrices $S$ that satisfy this equation. To proceed, we must impose restrictions on $S$ that are guided by economic theory.

A common and straightforward method for achieving identification is the **Cholesky decomposition**. This method assumes a recursive causal structure among the variables at the moment a shock occurs. By choosing a specific ordering of the variables in the vector $y_t$, we can uniquely define $S$ as the lower-triangular Cholesky factor $P$ of $\Sigma_u$, such that $\Sigma_u = P P'$.

The choice of a [lower-triangular matrix](@entry_id:634254) $P$ imposes a powerful set of zero restrictions on the contemporaneous impact of the shocks. Consider a two-variable system with variables $y_1$ and $y_2$. The relation $u_t = P \varepsilon_t$ becomes :
$$
\begin{pmatrix} u_{1,t} \\ u_{2,t} \end{pmatrix} = \begin{pmatrix} p_{11} & 0 \\ p_{21} & p_{22} \end{pmatrix} \begin{pmatrix} \varepsilon_{1,t} \\ \varepsilon_{2,t} \end{pmatrix}
$$
This expands to:
$$
u_{1,t} = p_{11} \varepsilon_{1,t}
$$
$$
u_{2,t} = p_{21} \varepsilon_{1,t} + p_{22} \varepsilon_{2,t}
$$
This structure implies that a structural shock to the first variable, $\varepsilon_{1,t}$, can contemporaneously affect both $y_{1,t}$ (through $u_{1,t}$) and $y_{2,t}$ (through $u_{2,t}$). However, a structural shock to the second variable, $\varepsilon_{2,t}$, can only affect $y_{2,t}$ contemporaneously; its impact on $y_{1,t}$ is restricted to be zero at horizon $h=0$. The variable ordered first is thus assumed to be the most "exogenous" in a contemporaneous sense.

This highlights that the ordering of variables is not a mere technical choice but a critical economic assumption. For example, consider a VAR model for a small open economy that includes global oil price inflation ($A_t$) and domestic consumer price inflation ($B_t$). With the ordering $(A_t, B_t)$, the Cholesky decomposition implies that a global oil shock can immediately affect domestic inflation, but a domestic inflation shock cannot contemporaneously affect the global oil price. This is an economically plausible assumption. Reversing the order to $(B_t, A_t)$ would imply the opposite, counter-intuitive causal flow . The justification for a particular ordering must come from economic theory or institutional knowledge about the relative speeds of information transmission and response in the system.

### The Anatomy of Forecast Error Variance Decomposition

With a set of orthogonal [structural shocks](@entry_id:136585) $\varepsilon_t$ in hand, we can now derive the FEVD. The forecast error is rewritten in terms of these shocks:
$$
e_{t+h|t} = \sum_{s=0}^{h-1} \Phi_s (P \varepsilon_{t+h-s}) = \sum_{s=0}^{h-1} \Theta_s \varepsilon_{t+h-s}
$$
Here, $\Theta_s = \Phi_s P$ is the matrix of **orthogonalized impulse responses** at horizon $s$. Its element $(\Theta_s)_{ij}$ represents the response of variable $i$ to a one-standard-deviation structural shock in variable $j$ after $s$ periods.

The forecast [error variance](@entry_id:636041) for variable $i$ is the $i$-th diagonal element of the MSE matrix, which now becomes:
$$
\text{Var}(e_{i,t+h|t}) = \mathbb{E}\left[ \left( \sum_{s=0}^{h-1} \sum_{j=1}^{n} (\Theta_s)_{ij} \varepsilon_{j,t+h-s} \right)^2 \right]
$$
Since the [structural shocks](@entry_id:136585) $\varepsilon_j$ are orthogonal and have unit variance, all cross-product terms in the expectation are zero. The variance simplifies to a sum of squared impulse responses:
$$
\text{Var}(e_{i,t+h|t}) = \sum_{s=0}^{h-1} \sum_{j=1}^{n} (\Theta_s)_{ij}^2 = \sum_{j=1}^{n} \left( \sum_{s=0}^{h-1} (\Theta_s)_{ij}^2 \right)
$$
This equation is the heart of the decomposition. It shows that the total forecast [error variance](@entry_id:636041) of variable $i$ is a simple sum of the contributions from each structural shock $j$. The term $\sum_{s=0}^{h-1} (\Theta_s)_{ij}^2$ represents the total variance in variable $i$ over the forecast horizon $h$ that is attributable to shock $j$.

The **Forecast Error Variance Decomposition (FEVD)** share is defined as the proportion of the total forecast [error variance](@entry_id:636041) of variable $i$ at horizon $h$ that is explained by structural shock $j$:
$$
\text{FEVD}_{i \leftarrow j}(h) = \frac{\sum_{s=0}^{h-1} (\Theta_s)_{ij}^2}{\sum_{k=1}^{n} \sum_{s=0}^{h-1} (\Theta_s)_{ik}^2}
$$
By construction, for any given variable $i$ and horizon $h$, the shares from all shocks sum to $1$ ($\sum_{j=1}^n \text{FEVD}_{i \leftarrow j}(h) = 1$).

### Interpreting the Decomposition: Exogeneity, Endogeneity, and Economic Narratives

The FEVD table provides a rich summary of the dynamic interactions within a VAR system. A variable is considered **relatively exogenous** if a large proportion of its forecast [error variance](@entry_id:636041) is explained by its *own* structural shock. In the extreme case, if the FEVD for a variable $y_1$ shows that its own shock accounts for nearly 100% of its forecast [error variance](@entry_id:636041) at all horizons, we can infer that $y_1$ is **block exogenous** with respect to the other variables in the system. This means that shocks originating from other variables have a negligible dynamic impact on $y_1$ . This is often the theoretical expectation for a policy instrument that is set without feedback from other variables. For a truly structurally exogenous policy instrument, its FEVD from its own shock would be exactly 100% at all forecast horizons .

Conversely, a variable is considered **endogenous** if a large share of its forecast [error variance](@entry_id:636041) is explained by shocks to *other* variables in the system. The FEVD thus quantifies the channels and magnitudes of shock transmission over different time horizons.

Consider a three-variable macroeconomic VAR with real output growth ($y_t$), inflation ($\pi_t$), and a short-term policy interest rate ($i_t$). An FEVD analysis might reveal the following patterns :
-   At a **short horizon** ($h=1$), each variable's forecast [error variance](@entry_id:636041) is predominantly explained by its own shock (e.g., 85% for output, 70% for inflation, 80% for the interest rate). This is a common finding, reflecting immediate, own-variable responses.
-   At a **longer horizon** ($h=12$), the picture changes dramatically. The variance of output and inflation might now be largely explained by shocks to the interest rate (e.g., 55% for output, 75% for inflation). This illustrates the delayed transmission of [monetary policy](@entry_id:143839) shocks to the real economy and prices. Simultaneously, the variance of the interest rate itself might now be mostly explained by inflation shocks (e.g., 60%). This suggests the policy rate is behaving endogenously, systematically responding to inflation in a manner consistent with a Taylor-type policy rule. By comparing the FEVD across horizons, we can construct a coherent economic narrative about the system's dynamic structure.

### Advanced Properties and Alternative Decompositions

The FEVD has several important properties and has been extended to address limitations of the standard Cholesky-based approach.

#### The Forecast Horizon and Convergence

The composition of the FEVD changes with the forecast horizon $h$. At $h=1$, the forecast error is just the innovation $u_{t+1}$, so the FEVD depends only on the contemporaneous impact matrix $P$. As $h$ increases, the dynamic propagation of shocks through the system, captured by the $A_k$ matrices, plays an increasingly important role. For a stable VAR, as the horizon $h \to \infty$, the forecast [error variance](@entry_id:636041) converges to the total unconditional variance of the process. The FEVD shares therefore converge to a stable long-run decomposition. This infinite-horizon limit can be computed efficiently by solving a system of discrete-time Lyapunov equations, avoiding the need for infinite summation .

#### The Critical Role of Correlation and Ordering

It is crucial to re-emphasize that the Cholesky-based FEVD is conditional on the chosen causal ordering. This dependence arises entirely from the need to handle the contemporaneous correlation in the reduced-form innovations $u_t$. To see this, consider a special case where the innovations are already uncorrelated, meaning their covariance matrix $\Sigma_u$ is diagonal. In this scenario, the lower-triangular Cholesky factor $P$ is also a diagonal matrix. The "[orthogonalization](@entry_id:149208)" step, $u_t = P \varepsilon_t$, does not mix innovations across variables; it simply scales them. Consequently, the attribution of variance to each shock is unambiguous, and the resulting FEVD is invariant to the ordering of the variables . This highlights that the ordering debate is fundamentally about how to attribute the effects of correlated shocks.

#### Generalized Forecast Error Variance Decomposition (GFEVD)

To address the ordering-dependence of the Cholesky method, Pesaran and Shin (1998) proposed the **Generalized Forecast Error Variance Decomposition (GFEVD)**. The GFEVD provides an order-invariant decomposition by avoiding the explicit [orthogonalization](@entry_id:149208) of shocks. It instead considers the effect of a shock to one variable and allows for its historical correlation with other shocks. A key feature of the GFEVD is that the resulting variance contributions for a given variable do not necessarily sum to one, so they are typically normalized by their sum for ease of interpretation. Numerical comparisons confirm that while Cholesky-based FEVD results can change significantly with the [variable ordering](@entry_id:176502), the GFEVD results remain identical, providing a more robust, though conceptually different, picture of the system's dynamics .

### Practical Considerations in Model Specification

Finally, it is essential to recognize that the FEVD is a product of the entire VAR model specification. Its accuracy and reliability depend on the validity of the underlying model. Two key aspects of specification are particularly important:

-   **Lag Length Selection**: The dynamic properties of the VAR, captured by the impulse response functions $\Phi_s$, depend on the chosen lag order $p$. Including too few lags (under-specification) can lead to biased estimates of the impulse responses and, consequently, a distorted FEVD. For instance, omitting a significant second lag can alter the calculated FEVD shares, especially at longer horizons where dynamic propagation is key .

-   **Structural Stability**: A standard VAR model assumes that its parameters are constant over time. If the true data-generating process undergoes a **structural break** (e.g., a central bank alters its policy rule), estimating a single VAR over the entire sample will produce parameters that are a weighted average of the pre- and post-break regimes. The FEVD computed from this misspecified model will be a distorted hybrid that does not accurately represent the dynamics of either period, potentially leading to flawed economic inferences . It is therefore crucial to test for and account for [structural instability](@entry_id:264972) before conducting FEVD analysis.

In conclusion, the Forecast Error Variance Decomposition is a powerful and versatile tool for exploring the dynamics of multivariate systems. Its proper application requires not only a firm grasp of its mathematical foundations but also a keen awareness of the economic assumptions embedded in its construction and the potential pitfalls related to model specification.