## Introduction
In the study of complex dynamical systems, from energy grids to global climate, time series data provides a window into their underlying behavior. However, classical models that assume stable, stationary processes often fall short, as real-world systems are subject to abrupt shifts, policy changes, and evolving dynamics. This gap necessitates a more advanced toolkit capable of identifying and modeling these "regime changes." This article provides a comprehensive exploration of advanced time series modeling and regime change detection, designed to equip graduate-level researchers and practitioners with the necessary theoretical and practical knowledge.

The journey begins in the **Principles and Mechanisms** chapter, where we will build a solid foundation, starting with concepts like stationarity and cointegration before delving into the workhorse models for conditional mean (ARMA) and variance (GARCH). We will then formalize the concept of a regime change and introduce the key modeling frameworks, from Threshold Autoregressive (TAR) models to latent-state Hidden Markov Models (HMMs). Following this, the **Applications and Interdisciplinary Connections** chapter demonstrates how these models are deployed to solve critical problems in energy forecasting, climate science, and policy evaluation, highlighting the powerful insights gained by moving beyond simple linear assumptions. Finally, the **Hands-On Practices** section bridges theory and practice, offering guided exercises that apply these sophisticated techniques to concrete problems, solidifying your understanding and building practical skills.

## Principles and Mechanisms

This chapter delineates the fundamental principles and mechanisms that underpin advanced time series modeling and regime change detection. We will begin by establishing the foundational concepts of stochastic processes, including stationarity and integration, which are prerequisites for understanding temporal dynamics. Subsequently, we will introduce the canonical models for capturing both the conditional mean and conditional variance of a time series. Building on this foundation, we will formally define what constitutes a regime change and explore the primary modeling frameworks designed to capture such shifts, distinguishing between processes driven by observable and latent state variables. Finally, we will address critical aspects of inference and practice, including the nuanced concept of causality in dynamic systems, principles of model selection, and the challenges posed by incomplete data.

### Foundational Concepts of Time Series Processes

The analysis of any time series begins with characterizing its underlying stochastic properties. The most crucial property is stationarity, which describes whether the statistical characteristics of the process are invariant over time.

#### Stationarity, Unit Roots, and Cointegration

A stochastic process is said to be **strictly stationary** if its joint probability distribution is invariant under time shifts. Formally, for a process $\{X_t\}$, for any collection of time indices $t_1, t_2, \dots, t_k$ and any time shift $s$, the joint distribution of $(X_{t_1}, \dots, X_{t_k})$ is identical to that of $(X_{t_1+s}, \dots, X_{t_k+s})$. This is a very strong condition that is often difficult to verify and may not hold for many real-world series, such as those from energy systems which are subject to trends and structural evolution.

A more lenient and practically useful condition is **weak stationarity** (or covariance stationarity). A process $\{X_t\}$ is weakly stationary if its first two moments are time-invariant. Specifically, three conditions must be met:
1.  The mean is constant: $\mathbb{E}[X_t] = \mu$ for all $t$.
2.  The variance is finite and constant: $\operatorname{Var}(X_t) = \sigma^2  \infty$ for all $t$.
3.  The autocovariance between any two points depends only on their temporal separation (the lag $h$), not on their absolute position in time: $\operatorname{Cov}(X_t, X_{t+h}) = \gamma(h)$ for all $t$ and any lag $h$.

A strictly stationary process with a finite second moment is always weakly stationary. The converse is not generally true, with a notable exception being the Gaussian process, where weak stationarity implies strict stationarity because the entire distribution is defined by its first two moments [@problem_id:4068738]. In practice, a key step in time series modeling, such as for hourly electricity demand, involves transforming the raw data—by removing deterministic components like seasonality and trends—to achieve a residual process that can be reasonably approximated as stationary [@problem_id:4068738].

Many economic and energy-related time series, such as fuel prices, are not stationary. They often exhibit **stochastic trends**, where shocks have a permanent effect on the level of the series. Such a non-stationary process is known as a **unit root process**. A process is said to be **integrated of order $d$**, denoted $I(d)$, if it must be differenced $d$ times to become a stationary process, denoted $I(0)$. A classic example is a random walk, $S_t = S_{t-1} + v_t$, where $v_t$ is a stationary innovation (e.g., white noise). The first difference, $\Delta S_t = S_t - S_{t-1} = v_t$, is stationary, so the random walk $S_t$ is an $I(1)$ process. In contrast, a stable autoregressive process like $c_t = \phi c_{t-1} + u_t$ with $|\phi|  1$ is already stationary and thus is an $I(0)$ process [@problem_id:4068773].

While individual $I(1)$ series wander without reverting to a mean, a collection of such series may be bound together by a long-run equilibrium relationship. This phenomenon is known as **cointegration**. A set of $I(1)$ time series is said to be cointegrated if a specific linear combination of them is stationary ($I(0)$). This stationary linear combination represents the equilibrium relationship. The vector of coefficients that defines this combination is called the **cointegrating vector**. For example, consider a vector of energy prices $X_t = (p^E_t, p^G_t, c_t)'$, where electricity price $p^E_t$ and gas price $p^G_t$ are both $I(1)$ due to a common stochastic trend, while coal cost $c_t$ is $I(0)$. If a linear combination, such as $p^E_t - \lambda p^G_t$, eliminates the common trend and results in an $I(0)$ process, then $p^E_t$ and $p^G_t$ are cointegrated with the cointegrating vector $(1, -\lambda, 0)'$ [@problem_id:4068773].

#### Autoregressive Moving Average (ARMA) Models

For a stationary time series, the **Autoregressive Moving Average (ARMA)** model provides a parsimonious description of its dynamics. An **ARMA(p,q)** model expresses the current value of the series, $X_t$, as a linear function of its own past values (the autoregressive component) and past innovation terms (the moving average component). Using the backshift operator $B$ (where $B X_t = X_{t-1}$), the model is defined as:
$$ \phi(B) X_t = c + \theta(B) \varepsilon_t $$
Here, $\phi(B) = 1 - \sum_{i=1}^p \phi_i B^i$ is the autoregressive polynomial of order $p$, $\theta(B) = 1 + \sum_{j=1}^q \theta_j B^j$ is the moving average polynomial of order $q$, $c$ is a constant, and $\{\varepsilon_t\}$ is a white noise process of innovations.

For non-stationary $I(d)$ series, the model can be extended to the **Autoregressive Integrated Moving Average (ARIMA)** framework. An **ARIMA(p,d,q)** model specifies that the $d$-th difference of the series, $W_t = (1-B)^d X_t$, follows a stationary ARMA(p,q) process:
$$ \phi(B) (1-B)^d X_t = c + \theta(B) \varepsilon_t $$
This class of models forms the foundation of linear time series forecasting. To incorporate external information, such as the effect of ambient temperature on electricity load, the **ARMAX** model extends the conditional mean of the series with exogenous regressors $Z_t$:
$$ \phi(B) X_t = c + \beta' Z_t + \theta(B) \varepsilon_t $$
In this formulation, variables like temperature and its non-linear transformations (e.g., heating and cooling degree days) enter the model additively through the term $\beta'Z_t$, directly influencing the conditional mean of the electricity load $X_t$ [@problem_id:4068783].

#### Conditional Heteroskedasticity and GARCH Models

While ARMA models describe the conditional mean of a process, they assume the variance of the innovations, $\operatorname{Var}(\varepsilon_t)$, is constant. However, many financial and energy price series exhibit **volatility clustering**, where periods of high volatility are followed by periods of high volatility, and periods of low volatility are followed by periods of low volatility. This implies that the variance, conditional on past information, is time-varying. This phenomenon is known as **conditional heteroskedasticity**.

The **Generalized Autoregressive Conditional Heteroskedasticity (GARCH)** model is the standard tool for capturing such dynamics. A GARCH model specifies a process for the conditional variance. Let $\epsilon_t$ be the mean-adjusted return or innovation, defined by $\epsilon_t = \sigma_t z_t$, where $z_t$ is an i.i.d. process with zero mean and unit variance, and $\sigma_t^2$ is the conditional variance. A **GARCH(p,q)** model specifies the evolution of $\sigma_t^2$ as:
$$ \sigma_t^2 = \omega + \sum_{i=1}^{q} \alpha_i \epsilon_{t-i}^2 + \sum_{j=1}^{p} \beta_j \sigma_{t-j}^2 $$
The parameters must satisfy $\omega > 0$, $\alpha_i \ge 0$, and $\beta_j \ge 0$ to ensure the variance is positive. The term $\sum \alpha_i \epsilon_{t-i}^2$ is the **ARCH component**, capturing the influence of past shocks (large past $|\epsilon_{t-i}|$ lead to high current variance), and the term $\sum \beta_j \sigma_{t-j}^2$ is the **GARCH component**, capturing the persistence in volatility.

It is crucial to distinguish between the **conditional variance** $\operatorname{Var}(\epsilon_t \mid \mathcal{F}_{t-1}) = \sigma_t^2$, which is time-varying, and the **unconditional variance** $\operatorname{Var}(\epsilon_t)$, which, if the process is stationary, is constant over time. For a GARCH(p,q) process to be covariance-stationary, the sum of its parameters must be less than one: $\sum_{i=1}^q \alpha_i + \sum_{j=1}^p \beta_j  1$. Under this condition, the constant unconditional variance is given by:
$$ \operatorname{Var}(\epsilon_t) = \frac{\omega}{1 - \sum_{i=1}^q \alpha_i - \sum_{j=1}^p \beta_j} $$
For example, for a GARCH(1,1) model with parameters $\omega=0.0004$, $\alpha_1=0.05$, and $\beta_1=0.90$, the stationarity condition $\alpha_1+\beta_1 = 0.95  1$ holds, and the unconditional variance is $\frac{0.0004}{1-0.05-0.90} = 0.008$ [@problem_id:4068772].

### The Concept of Regime Change

A central theme in modern time series analysis is the recognition that the underlying structure of a data-generating process may not be constant over time. Sudden shocks, policy changes, technological innovations, or evolving environmental conditions can induce abrupt or gradual shifts in the statistical properties of a series. These shifts define different **regimes**, and modeling them is critical for accurate forecasting and policy analysis.

#### Change Points: Definition and Detection Modalities

A **change point**, $\tau$, is a point in time at which the data-generating distribution of a time series changes. This can manifest as a shift in the mean, variance, autoregressive parameters, or any other aspect of the model that was previously assumed to be constant [@problem_id:4068760]. For example, in the context of power grid stability, a generator trip or a large load change can induce a change point in the time series of grid frequency deviations, moving the system from one stationary regime to another.

There are two primary modalities for dealing with change points:
1.  **Offline Segmentation**: This is a retrospective analysis performed on a complete, finite block of historical data, $X_{1:T}$. The goal is to partition the entire time series into the most likely set of contiguous segments, each corresponding to a distinct statistical regime. This is typically framed as an optimization problem, where an algorithm seeks the number and locations of change points that best explain the data according to a chosen criterion (e.g., maximizing likelihood while penalizing complexity). Since the full dataset is available, information from the future (relative to any point $t  T$) can be used to make decisions about change points.

2.  **Online Detection**: This is a sequential, real-time procedure designed to detect a change point as quickly as possible after it occurs. At each time step $t$, a decision must be made based only on the information available up to that point, denoted by the filtration $\mathcal{F}_t$. The algorithm cannot use future data. The decision rule is formulated as a **stopping time**, which signals an alarm when there is sufficient evidence of a change. Online detection involves a fundamental trade-off between the **detection delay** (how long it takes to detect a change after it has happened) and the **false alarm rate** (the frequency of raising an alarm when no change has occurred) [@problem_id:4068760].

#### Models with Observable Regime Switching

In some systems, the transition between regimes is governed by an observable variable. This leads to a class of models where the parameters of the time series are explicit functions of this **threshold variable**.

A **Threshold Autoregressive (TAR)** model is a piecewise linear autoregression where the model's parameters switch abruptly when a threshold variable $q_t$ crosses a specific value $c$. A simple two-regime TAR model can be written as:
$$ y_t = \begin{cases} c_1 + \sum_{i=1}^p \phi_{1,i} y_{t-i} + \epsilon_t  \text{if } q_t \le c \\ c_2 + \sum_{i=1}^p \phi_{2,i} y_{t-i} + \epsilon_t  \text{if } q_t > c \end{cases} $$
The threshold variable $q_t$ can be an exogenous variable (e.g., ambient temperature) or an endogenous one, such as a lagged value of the series itself, $y_{t-d}$, which defines a **Self-Exciting TAR (SETAR)** model. The key feature of TAR models is the discontinuous, sharp switch between regimes [@problem_id:4068759].

A natural extension of the TAR model is the **Smooth Transition Autoregressive (STAR)** model, which allows for a gradual, continuous transition between regimes. Instead of an abrupt switch, a STAR model represents the dynamics as a weighted average of two or more linear AR models, where the weights are determined by a continuous transition function $G(q_t; \gamma, c)$ bounded between 0 and 1. The model takes the form:
$$ y_t = (1 - G(q_t; \gamma, c)) (\text{AR model 1}) + G(q_t; \gamma, c) (\text{AR model 2}) + \epsilon_t $$
Common choices for $G$ include the logistic function (giving an LSTAR model) and the exponential function (giving an ESTAR model). This framework is particularly well-suited for modeling phenomena where the system's response changes smoothly. For example, the relationship between electricity load and ambient temperature is famously non-linear: below a comfort band, load increases as it gets colder (heating); above the band, load increases as it gets hotter (cooling); and within the band, load is relatively insensitive to temperature. This can be elegantly captured by a STAR model with temperature as the transition variable [@problem_id:4068759].

#### Models with Latent Regime Switching: Hidden Markov Models

In many applications, the underlying regime is not directly observable but is instead a **latent state** that must be inferred from the data. **Hidden Markov Models (HMMs)**, also known as Markov-switching models, provide a powerful framework for this task.

An HMM consists of two components:
1.  An unobserved **latent state process** $\{s_t\}$, which is assumed to be a first-order Markov chain. This means the probability of being in a certain state at time $t$ depends only on the state at time $t-1$: $\mathbb{P}(s_t \mid s_{1:t-1}) = \mathbb{P}(s_t \mid s_{t-1})$. The dynamics of this chain are governed by an initial state distribution and a transition probability matrix.
2.  An **observation process**, where the conditional distribution of the observed variable $y_t$ depends on the current latent state $s_t$. For example, in a Markov-switching AR(p) model, the AR parameters, intercept, and innovation variance all depend on the regime $s_t$.

The joint probability of the observations and the latent state path factorizes according to the model's dependency structure:
$$ p(y_{1:T}, s_{1:T}) = p(s_1) \prod_{t=2}^T p(s_t \mid s_{t-1}) \times \prod_{t=1}^T p(y_t \mid y_{t-1:t-p}, s_t) $$
This structure allows for efficient inference using recursive algorithms like the Hamilton filter to compute the likelihood by integrating over all possible state paths [@problem_id:4068723].

A significant challenge in Bayesian estimation of HMMs is the **label switching** problem. Because the labels of the latent states $\{1, \dots, K\}$ are arbitrary, the likelihood function is invariant to any permutation of these labels. If the prior distribution on the parameters is also symmetric (exchangeable), the posterior distribution will have $K!$ identical, symmetric modes. This means that while the overall model fit and predictive distributions are unaffected, the interpretation of a specific "regime $k$" becomes ambiguous across MCMC draws. To achieve interpretable, consistent labeling of regimes, one must either impose identifying constraints (e.g., ordering the regime-specific means or variances) or apply post-processing relabeling algorithms [@problem_id:4068723].

### Inference and Practical Challenges

Building and interpreting advanced time series models involves navigating several complex inferential and practical issues. These include distinguishing causality from correlation, selecting the appropriate model complexity, and handling imperfections in real-world data.

#### Granger Causality and Its Pitfalls

In a multivariate system, understanding the directional influence between variables is paramount. **Granger causality** provides a statistical definition of causality based on predictability. A time series $W_t$ is said to **Granger-cause** another time series $L_t$ if past values of $W_t$ contain information that helps predict future values of $L_t$, above and beyond the information already contained in the past values of $L_t$ and any other relevant variables. In a linear Vector Autoregressive (VAR) framework, this is tested by examining whether the coefficients on the lagged values of $W_t$ are statistically significant in the equation for $L_t$ [@problem_id:4068727].

It is critical to distinguish Granger causality from contemporaneous correlation. Two variables can be highly correlated at time $t$ (e.g., due to a common shock affecting their innovations), yet have no Granger-causal relationship. For instance, in a VAR model for load $L_t$ and wind generation $W_t$, the coefficient on $W_{t-1}$ in the $L_t$ equation might be zero (no Granger causality), while the correlation between their error terms, $\operatorname{Corr}(\varepsilon_t^{(L)}, \varepsilon_t^{(W)})$, is non-zero (contemporaneous correlation) [@problem_id:4068727].

Testing for Granger causality is fraught with pitfalls:
-   **Omitted Variable Bias**: If a third variable, $G_t$, is a common driver of both $W_t$ and $L_t$, but is omitted from the model, a test might find a spurious causal link from $W_t$ to $L_t$. This occurs because the lagged variable $W_{t-1}$ acts as a proxy for the omitted causal variable $G_{t-1}$ [@problem_id:4068727].
-   **Unaccounted Structural Breaks**: Ignoring a regime change and estimating a single, constant-parameter model on pooled data from different regimes can lead to spurious findings of causality. The shifts in the means or other parameters across regimes can induce correlations in the pooled data that are misinterpreted as predictive relationships [@problem_id:4068727]. This highlights the deep connection between regime change detection and valid causal inference. Similarly, a structural break in a cointegrating relationship can lead a test to incorrectly conclude there is no cointegration, when in fact it exists within sub-periods with different cointegrating vectors [@problem_id:4068773].

#### Model Selection Criteria

When faced with a choice between competing models—for instance, an AR(1) vs. an AR(2), or a 2-regime vs. a 3-regime HMM—we need a formal criterion for selection. **Information criteria** provide a principled way to balance model fit (as measured by the maximized log-likelihood, $\ell(\hat{\theta})$) with model complexity (as measured by the number of free parameters, $k$). The goal is to select the model that minimizes the criterion value. The most common criteria are:
-   **Akaike Information Criterion (AIC):** $AIC = -2 \ell(\hat{\theta}) + 2k$
-   **Bayesian Information Criterion (BIC):** $BIC = -2 \ell(\hat{\theta}) + k \ln(n)$
-   **Hannan-Quinn Information Criterion (HQIC):** $HQIC = -2 \ell(\hat{\theta}) + 2k \ln(\ln n)$

where $n$ is the number of observations. BIC imposes a stronger penalty for complexity than AIC, especially for large $n$, and tends to select more parsimonious models. The time-dependent structure of the data is fully captured within the likelihood function $\ell(\hat{\theta})$, so these standard forms apply directly to time series models under typical regularity conditions.

A crucial and often-missed step is correctly counting the number of free parameters, $k$. For a complex model like an $S$-regime, $p$-order Markov-switching autoregression, $k$ must include all freely estimated parameters: $Sp$ AR coefficients, $S$ intercepts, $S$ innovation variances, and the $S(S-1)$ free parameters of the transition probability matrix. Confusing latent variables with parameters is a fundamental error; the latent state path $\{s_t\}$ is integrated out in the likelihood and does not contribute to $k$ [@problem_id:4068787].

#### Missing Data Mechanisms and Their Implications

Real-world data from energy systems are often incomplete due to sensor failures, communication errors, or maintenance. The reason why data are missing—the **missingness mechanism**—has profound implications for the validity of any statistical inference. The mechanisms are classified as follows:
-   **Missing Completely At Random (MCAR):** The probability of a value being missing is independent of all data, both observed and unobserved.
-   **Missing At Random (MAR):** The probability of a value being missing may depend on the *observed* data, but conditional on the observed data, it does not depend on the *unobserved* (missing) values. For a time series, this could mean the probability of $y_t$ being missing depends on the observed past value $y_{t-1}$.
-   **Missing Not At Random (MNAR):** The probability of a value being missing depends on the unobserved value itself, even after accounting for all observed data. An example is a sensor that fails when the quantity it measures (e.g., net load $y_t$) exceeds a certain latent threshold.

The key concept for likelihood-based inference is **ignorability**. If the data are MAR (or MCAR) and the parameters of the data model and the missingness model are distinct, the missingness mechanism is ignorable. This means that valid, consistent estimates of the model parameters can be obtained by maximizing the **observed-data likelihood**, which is the likelihood function after integrating out the missing values. Methods like the Kalman filter combined with the Expectation-Maximization (EM) algorithm are designed to do precisely this for linear Gaussian state-space models and are therefore valid under MAR.

Under MNAR, the missingness mechanism is non-ignorable. Simply ignoring the missingness or using standard methods designed for MAR will generally lead to biased parameter estimates and invalid inference. This can be particularly damaging for regime change detection, as an unmodeled MNAR process can create spurious evidence of a structural break or mask a true one. Valid inference under MNAR requires explicitly modeling the joint distribution of the data and the missingness process, which is a significantly more complex task [@problem_id:4068724].