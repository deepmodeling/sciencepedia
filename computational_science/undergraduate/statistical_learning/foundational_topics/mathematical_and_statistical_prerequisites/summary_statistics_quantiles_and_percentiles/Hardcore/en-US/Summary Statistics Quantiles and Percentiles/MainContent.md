## Introduction
Quantiles and percentiles are fundamental tools in statistics, providing a far richer description of a dataset than simple measures of central tendency like the mean. By dividing a distribution into intervals, they allow us to understand its shape, spread, and tails. While the concept of a median (the 50th percentile) is widely understood, the theoretical underpinnings and practical power of the full spectrum of quantiles are often underappreciated. The seemingly trivial task of calculating a quantile from a sample of data hides a surprising amount of nuance, and different statistical software packages can yield different answers from the same data. Understanding these nuances, along with the profound statistical properties of quantiles, is essential for robust data analysis and modeling.

This article delves into the world of quantiles, bridging theory and application to provide a comprehensive understanding. We will unpack the principles that make quantiles so powerful, explore their diverse applications, and offer hands-on practice to solidify these concepts. In the chapters that follow, you will gain a deep appreciation for this versatile statistical tool. **Principles and Mechanisms** will lay the theoretical groundwork, from the various definitions of sample quantiles to their fundamental properties of robustness and their modern interpretation through optimization. **Applications and Interdisciplinary Connections** will showcase how quantiles are used to solve real-world problems in fields ranging from finance and engineering to biology and machine learning. Finally, **Hands-On Practices** will provide concrete coding exercises to translate theory into practical skills, demonstrating the impact of methodological choices and the utility of quantiles in model evaluation.

## Principles and Mechanisms

### Defining Sample Quantiles: From Inversion to Interpolation

At its core, a **quantile** is a point that partitions the range of a probability distribution into continuous intervals with equal probabilities. For a given probability $p \in (0,1)$, the $p$-quantile, denoted $q_p$, is the value below which a proportion $p$ of the observations in a population falls. This is formally defined for a random variable $X$ with a continuous and strictly increasing cumulative distribution function (CDF), $F(x) = \mathbb{P}(X \le x)$, as the unique value $q_p$ such that $F(q_p) = p$.

In practice, we rarely have access to the true CDF $F$. Instead, we work with a finite sample of observations $X_1, X_2, \dots, X_n$. The natural empirical counterpart to the CDF is the **empirical cumulative distribution function (ECDF)**, defined as:

$$ \hat{F}_n(x) = \frac{1}{n} \sum_{i=1}^{n} \mathbf{1}\{X_i \le x\} $$

where $\mathbf{1}\{\cdot\}$ is the indicator function. The ECDF is a step function that increases by $\frac{1}{n}$ at each observed data point. A natural way to define the sample $p$-quantile, $\hat{q}_p$, is to invert the ECDF in the same way we invert the true CDF. This leads to the definition of the quantile as the generalized inverse of the ECDF:

$$ \hat{q}_p = \inf\{x : \hat{F}_n(x) \ge p\} $$

This definition is fundamental and mathematically clean. If we have the ordered sample, or **order statistics**, denoted $x_{(1)} \le x_{(2)} \le \dots \le x_{(n)}$, this definition is equivalent to selecting a specific order statistic. For a given $p \in (0, 1]$, the smallest $x$ for which $\hat{F}_n(x) \ge p$ corresponds to the order statistic $x_{(k)}$ where $k$ is the smallest integer such that $\frac{k}{n} \ge p$. This integer is $k = \lceil np \rceil$. Thus, this "inverse ECDF" method defines the sample quantile as $\hat{q}_p = x_{(\lceil np \rceil)}$ [@problem_id:3177989].

While this definition is simple, it has a drawback: the resulting quantile function $p \mapsto \hat{q}_p$ is a step function, jumping only at values of $p$ where $np$ crosses an integer. This can feel unnatural, and it has led to the development of numerous alternative definitions that use **linear interpolation** between adjacent order statistics to create a smoother quantile function.

A widely used interpolation scheme calculates a real-valued index and interpolates between the order statistics. For a sample of size $n$, one such method defines the index as $h = (n-1)p + 1$. The quantile is then computed by interpolating between $x_{(\lfloor h \rfloor)}$ and $x_{(\lfloor h \rfloor+1)}$ [@problem_id:3177989]. Specifically, with $j = \lfloor h \rfloor$ and $g = h - j$, the quantile is given by:

$$ \hat{q}_p = x_{(j)} + g(x_{(j+1)} - x_{(j)}) $$

This linear interpolation method is just one of many. In a seminal paper, Hyndman and Fan catalogued nine different quantile definitions used across various statistical software packages. For example, the method above corresponds to "Type 7," which is the default in the R programming language. Another method, "Type 8," uses a different index calculation: $i = (n + \frac{1}{3})p + \frac{1}{3}$.

These different definitions can produce materially different results, especially for small sample sizes. Consider a small dataset of 5 sorted observations: $x_{(1)}=3, x_{(2)}=5, x_{(3)}=7, x_{(4)}=10, x_{(5)}=15$. Calculating the 75th percentile ($p=0.75$) using the two methods mentioned gives different answers. The Type 7 method yields $\hat{q}_{0.75} = 10$, while the Type 8 method yields $\hat{q}_{0.75} = \frac{35}{3} \approx 11.67$ [@problem_id:3177908]. This discrepancy highlights a critical issue in data analysis: for results to be reproducible, it is imperative that the specific method used to calculate sample quantiles is reported, as different analysts using different software defaults may arrive at different conclusions from the same data.

Furthermore, it is important to understand the relationship between a set of quantiles and the underlying ECDF. Knowing a few quantiles, such as the quartiles, does not allow for a unique reconstruction of the ECDF, regardless of the definition used. For instance, knowing that the first, second, and third quartiles of a sample of size 8 are 3, 11, and 17 (corresponding to $x_{(2)}$, $x_{(4)}$, and $x_{(6)}$) only fixes those three order statistics. The other data points are only constrained by them (e.g., $x_{(3)}$ must be between 3 and 11), leaving the exact jump locations of the ECDF undetermined. However, if the entire quantile function $p \mapsto \hat{q}_p = x_{(\lceil np \rceil)}$ is known for all $p \in (0,1]$, one can recover all the order statistics by evaluating the function at $p = k/n$ for $k=1, \dots, n$. Knowing all order statistics uniquely determines the ECDF [@problem_id:3177989].

### The Defining Properties of Quantiles: Equivariance and Robustness

Beyond their definitional nuances, quantiles possess fundamental properties that make them powerful tools for data analysis. Two of the most important are equivariance under monotone transformations and robustness to outliers.

#### Equivariance to Monotone Transformations

A key property that distinguishes quantiles from other summary statistics like the mean is their **equivariance under monotone transformations**. If we apply a strictly increasing function $g(x)$ to our data, such as a logarithm or square root, the quantiles of the transformed data are simply the transformed quantiles of the original data. That is, if $Y = g(X)$, then the $p$-quantile of $Y$ is given by:

$$ q_Y(p) = g(q_X(p)) $$

This property holds because a strictly increasing function preserves order. The observation that was the $k$-th smallest in the original dataset will be the $k$-th smallest in the transformed dataset. Consequently, an anomaly detection threshold defined as a high percentile (e.g., the 80th percentile) will flag the exact same observations whether the threshold is applied on the original scale ($X \ge q_X(0.8)$) or on a transformed scale ($Y \ge q_Y(0.8)$) [@problem_id:3177900].

The sample mean does not share this property. In general, $\mathbb{E}[g(X)] \neq g(\mathbb{E}[X])$. For instance, for a log transformation, the exponential of the mean of the logs is the geometric mean, not the arithmetic mean. This equivariance makes quantiles a more stable and interpretable summary for data that may be analyzed on different scales.

#### Robustness to Outliers

Perhaps the most celebrated property of quantiles, and especially the median ($q_{0.5}$), is their **robustness** to outliers. A single extreme observation can pull the sample mean to an arbitrarily large or small value, while the sample median remains largely unaffected.

This concept can be formalized using the **influence function** (IF), a central tool in robust statistics. The influence function, $\mathrm{IF}(x; T, F)$, measures the effect of an infinitesimal contamination at a point $x$ on a statistical functional $T$ (like the mean or median) computed on a distribution $F$. It is defined as the Gâteaux derivative:

$$ \mathrm{IF}(x; T, F) \equiv \lim_{\varepsilon \to 0^{+}} \frac{T((1-\varepsilon)F + \varepsilon \Delta_{x}) - T(F)}{\varepsilon} $$

where $\Delta_x$ is a point mass at $x$.

For the mean functional, $\mu(F) = \int y \, dF(y)$, the influence function can be derived as $\mathrm{IF}(x; \mu, F) = x - \mu(F)$. This function is unbounded in $x$, meaning a contamination far from the mean has a proportionally large influence. For the median functional, $\theta(F)$, assuming a continuous density $f$ that is positive at the median, the influence function is $\mathrm{IF}(x; \theta, F) = \frac{\mathrm{sgn}(x-\theta(F))}{2f(\theta(F))}$. This function is bounded; its value does not grow with the magnitude of the outlier $x$, but depends only on whether the outlier is above or below the median [@problem_id:3177954]. The bounded influence function is the mathematical signature of a robust statistic.

The practical impact of this robustness is profound. In regression analysis, for example, the ordinary least squares (OLS) slope is highly sensitive to outliers because it is based on minimizing squared errors, a concept related to the mean. In contrast, the **Theil-Sen estimator**, which is the median of all pairwise slopes between data points, is a robust alternative. In a simple regression task, the addition of a single high-leverage outlier can catastrophically corrupt the OLS slope, while the Theil-Sen slope remains stable, demonstrating the tangible benefit of median-based methods in the presence of data contamination [@problem_id:3177954].

### A Modern Framework: Quantiles as Minimizers of Loss

A powerful and modern perspective defines quantiles not through distribution functions, but through an optimization problem. This view is the foundation of quantile regression and provides deep insights into the nature of quantiles.

Consider the **asymmetric absolute loss function**, also known as the **check function** or **pinball loss**:

$$ \rho_p(u) = \begin{cases} p u,  u \ge 0 \\ (p-1) u,  u  0 \end{cases} $$

This function is a tilted absolute value function, where the two linear pieces have slopes $p$ and $p-1$. For a random variable $X$, the population $p$-quantile, $q_p$, is the value $\theta$ that minimizes the expected loss, $L_p(\theta) = \mathbb{E}[\rho_p(X-\theta)]$.

This objective function $L_p(\theta)$ is convex. The first-order condition for a minimizer $\theta^*$ can be found using subgradient calculus, which generalizes the derivative for non-differentiable functions. The condition is that zero must be contained in the subgradient of $L_p(\theta)$ at $\theta^*$. The subgradient can be shown to be the interval $\partial L_p(\theta) = [F(\theta^-)-p, F(\theta)-p]$, where $F(\theta^-)$ is the left-hand limit of the CDF at $\theta$. The optimality condition $0 \in [F(\theta^{*-})-p, F(\theta^*)-p]$ translates to:

$$ F(\theta^{*-}) \le p \le F(\theta^*) $$

This elegant result recovers the classic CDF-based definition of a quantile from an optimization perspective [@problem_id:3177894]. It shows that any value in the interval where the CDF is flat at height $p$, or any value where the CDF jumps over $p$, is a valid $p$-quantile and a minimizer of the expected check loss.

This optimization framework is incredibly fruitful. It allows us to seamlessly integrate quantiles into regression models. **Quantile regression** seeks a function $f(x)$ that models the $p$-quantile of the conditional distribution of $Y$ given $X=x$. For a linear model, we find the coefficient vector $\beta$ that minimizes the sum of check losses over the data:

$$ \min_{\beta} \sum_{i=1}^n \rho_p(y_i - x_i^T \beta) $$

This framework can also incorporate regularization. For instance, adding an $L_1$ penalty (as in the LASSO) leads to the objective function $F(\beta) = \sum \rho_p(y_i - x_i^T \beta) + \lambda \|\beta\|_1$. This model encourages sparse solutions, where some coefficients are exactly zero. The subgradient optimality conditions can be used to determine the exact amount of regularization $\lambda$ needed to force a coefficient to be zero, providing a deep connection between the geometry of the check loss, the data, and model sparsity [@problem_id:3177990].

### The Uncertainty of Sample Quantiles: Inference and Asymptotics

A sample quantile $\hat{q}_p$ is an estimate of the true population quantile $q_p$. Like any statistical estimate, it is subject to sampling variability. Quantifying this uncertainty is a central task of statistical inference.

#### Confidence Intervals via Order Statistics

A non-parametric confidence interval for a population quantile can be constructed directly from the order statistics of a sample. Let $\eta$ be the population median ($p=0.5$) of a continuous distribution. For any observation $X_i$, the probability that it falls below $\eta$ is exactly $0.5$. Thus, if we count the number of observations $K$ in a sample of size $n$ that are less than $\eta$, this count follows a binomial distribution, $K \sim \mathrm{Binomial}(n, 0.5)$.

An interval of the form $(X_{(i)}, X_{(j)})$ contains the true median $\eta$ if and only if the number of observations below $\eta$ is between $i$ and $j-1$, i.e., $i \le K \le j-1$. We can therefore use the cumulative distribution function of the binomial distribution to find indices $i$ and $j$ such that the probability $P(i \le K \le j-1)$ is at least a desired confidence level (e.g., $0.95$). For a sample of size $n=11$, an exact confidence interval for the median with at least $95\%$ coverage is found to be $(X_{(2)}, X_{(10)})$ [@problem_id:3177931]. For larger samples, the binomial count can be approximated by a normal distribution, leading to a simpler, though approximate, method for finding the indices.

#### Asymptotic Distribution

For large samples, a more general and powerful result describes the distribution of the sample quantile. Under regularity conditions (specifically, that the PDF $f$ is continuous and positive at $q_p$), the sample quantile $\hat{q}_p$ is asymptotically normally distributed around the true quantile $q_p$. A linearization argument, related to the **Bahadur representation**, shows that:

$$ \sqrt{n}(\hat{q}_p - q_p) \xrightarrow{d} N\left(0, \frac{p(1-p)}{[f(q_p)]^2}\right) $$

where $\xrightarrow{d}$ denotes convergence in distribution [@problem_id:3177998]. This fundamental result provides several key insights. First, the variance of the sample quantile decreases at the standard rate of $\frac{1}{n}$. Second, the variance depends on the probability level $p$, being largest for the median ($p=0.5$) and smaller for tail quantiles. Third, and most importantly, the variance is inversely proportional to the square of the density at the quantile, $f(q_p)^2$. This is intuitive: where the data are denser ($f(q_p)$ is large), the quantile is more precisely determined.

This asymptotic result can be extended to a vector of quantiles. For instance, the vector of sample quartiles $(\hat{q}_{0.25}, \hat{q}_{0.50}, \hat{q}_{0.75})$ is jointly asymptotically normal. Their asymptotic covariance matrix, $\Sigma_Q$, has entries given by:

$$ (\Sigma_Q)_{ij} = \frac{\min(p_i, p_j) - p_i p_j}{n f(q_{p_i}) f(q_{p_j})} $$

This joint distribution is the key to performing inference on statistics that are functions of multiple quantiles, such as the interquartile range (IQR) or robust measures of skewness. Using the **multivariate delta method**, we can derive the asymptotic variance of such statistics [@problem_id:3178001].

#### Finite-Sample Bounds and Sample Complexity

While asymptotic theory is powerful, it is also useful to have guarantees that hold for any finite sample size $n$. Concentration inequalities provide such bounds. The **Dvoretzky–Kiefer–Wolfowitz (DKW) inequality** provides a uniform bound on the maximum deviation between the ECDF and the true CDF:

$$ \mathbb{P}\left(\sup_{x \in \mathbb{R}} |\hat{F}_n(x) - F(x)| > \epsilon\right) \le 2 \exp(-2n\epsilon^2) $$

This powerful result can be used to derive a non-asymptotic, high-probability bound on the error of the sample quantile, $|\hat{q}_p - q_p|$. If we assume the density $f(x)$ is bounded below by some $m > 0$ in a neighborhood of the true quantile $q_p$, we can relate the quantile error to the uniform CDF error. This leads to a bound of the form:

$$ \mathbb{P}(|\hat{q}_p - q_p| > \tau) \le 2 \exp(-2nm^2\tau^2) $$

This type of bound is central to statistical learning theory. It can be inverted to solve for the **sample complexity**: the minimum sample size $n$ required to guarantee that our sample quantile is within a distance $\tau$ of the true quantile with a specified high probability, $1-\delta$. This provides a practical, theory-grounded recipe for planning experiments and data collection [@problem_id:3177997].