## Introduction
Geometric Brownian Motion (GBM) stands as a cornerstone model in [quantitative finance](@entry_id:139120) and other [stochastic modeling](@entry_id:261612) disciplines, providing a foundational framework for describing the random evolution of asset prices. Its mathematical elegance and tractability have made it indispensable for the development of seminal theories like the Black-Scholes-Merton [option pricing model](@entry_id:138981). However, moving from theory to practice—valuing complex derivatives, managing [portfolio risk](@entry_id:260956), or modeling commodity prices—requires robust and accurate simulation techniques. The challenge lies not just in generating random paths, but in deeply understanding the properties of the simulation methods themselves, their inherent errors, and the subtle biases that can arise in practical applications.

This article provides a comprehensive guide to the simulation of Geometric Brownian Motion, designed for graduate-level practitioners and researchers. We will bridge the gap between the underlying [stochastic calculus](@entry_id:143864) and its computational implementation. First, in "Principles and Mechanisms," we will dissect the GBM stochastic differential equation, explore its fundamental properties, and compare exact and approximate simulation schemes, paying close attention to [error analysis](@entry_id:142477) and bias correction. Next, "Applications and Interdisciplinary Connections" will demonstrate the power of GBM simulation in solving real-world problems, from pricing [exotic options](@entry_id:137070) and managing [credit risk](@entry_id:146012) to valuing real assets in energy and planning for pension funds. Finally, a series of "Hands-On Practices" will provide opportunities to implement these concepts, offering a practical pathway to mastering the art and science of [stochastic simulation](@entry_id:168869).

## Principles and Mechanisms

This chapter delineates the fundamental mathematical principles and mechanisms that govern Geometric Brownian Motion (GBM). We will begin by formally defining the process through its stochastic differential equation (SDE) and establishing its well-posedness. Subsequently, we will derive its core properties, including the log-normal nature of the process, its strict positivity, and its statistical moments. Building on this theoretical foundation, we will explore various methods for its [numerical simulation](@entry_id:137087), from exact schemes to common approximation methods. The chapter will conclude with a rigorous analysis of the types of errors inherent in these simulations and an examination of the biases that arise, particularly when estimating path-dependent functionals, along with strategies for their correction.

### The Geometric Brownian Motion SDE

Geometric Brownian Motion is a [continuous-time stochastic process](@entry_id:188424) that serves as a cornerstone model in [financial mathematics](@entry_id:143286), most notably in the Black-Scholes-Merton [option pricing](@entry_id:139980) framework. A process $(S_t)_{t \ge 0}$ is said to follow a GBM if it satisfies the following stochastic differential equation:

$$dS_t = \mu S_t \, dt + \sigma S_t \, dW_t$$

Here, $S_t$ represents the state of the process at time $t$ (e.g., an asset price), with a given initial state $S_0 > 0$. The parameter $\mu \in \mathbb{R}$ is the constant **drift rate**, representing the instantaneous expected return of the process per unit time. The parameter $\sigma > 0$ is the constant **volatility**, representing the instantaneous standard deviation of the process's return. The term $(W_t)_{t \ge 0}$ is a standard **Brownian motion** (or Wiener process) defined on a filtered probability space $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \ge 0}, \mathbb{P})$, which provides the source of randomness for the process.

A crucial first step in the analysis of any SDE is to ensure that it is well-posed, meaning a unique solution exists. For the general SDE $dS_t = b(S_t) dt + a(S_t) dW_t$, a standard theorem guarantees the existence of a unique [strong solution](@entry_id:198344) if the drift coefficient $b(x)$ and diffusion coefficient $a(x)$ satisfy two conditions: global Lipschitz continuity and a [linear growth](@entry_id:157553) bound. For GBM, the coefficients are $b(x) = \mu x$ and $a(x) = \sigma x$. These are linear functions and can be shown to satisfy both conditions:

1.  **Global Lipschitz Continuity**: A function $f(x)$ is globally Lipschitz if there exists a constant $L$ such that $|f(x) - f(y)| \le L|x - y|$ for all $x, y$. For our coefficients, we have $|b(x) - b(y)| = |\mu||x-y|$ and $|a(x) - a(y)| = |\sigma||x-y|$. Thus, they are globally Lipschitz with constants $|\mu|$ and $|\sigma|$, respectively.

2.  **Linear Growth Condition**: The coefficients must satisfy $|b(x)| + |a(x)| \le K(1 + |x|)$ for some constant $K$. For GBM, we have $|\mu x| + |\sigma x| = (|\mu| + |\sigma|)|x|$. This is clearly less than or equal to $(|\mu| + |\sigma|)(1 + |x|)$, satisfying the condition.

Since both conditions hold, the GBM SDE admits a unique [strong solution](@entry_id:198344) for any initial condition $S_0$.

### Fundamental Properties

The behavior of GBM is best understood by transforming the process into a more familiar one. This is achieved through the application of Itô's lemma, a fundamental tool of [stochastic calculus](@entry_id:143864).

#### The Log-Normal Property and Exact Solution

Let us consider the process $X_t = \log S_t$. Applying Itô's lemma for the function $f(s) = \log s$, whose derivatives are $f'(s) = 1/s$ and $f''(s) = -1/s^2$, we obtain the dynamics of $X_t$:

$$dX_t = f'(S_t) dS_t + \frac{1}{2} f''(S_t) d\langle S \rangle_t$$

The quadratic variation term is $d\langle S \rangle_t = (\sigma S_t)^2 dt = \sigma^2 S_t^2 dt$. Substituting this and the SDE for $S_t$ yields:

$$dX_t = \frac{1}{S_t}(\mu S_t \, dt + \sigma S_t \, dW_t) + \frac{1}{2} \left(-\frac{1}{S_t^2}\right)(\sigma^2 S_t^2 dt)$$
$$dX_t = (\mu \, dt + \sigma \, dW_t) - \frac{1}{2}\sigma^2 dt$$
$$dX_t = \left(\mu - \frac{1}{2}\sigma^2\right) dt + \sigma dW_t$$

This remarkable result shows that the logarithm of a GBM process, $\log S_t$, is itself an **arithmetic Brownian motion** (also known as a generalized Wiener process) with a constant drift of $(\mu - \frac{1}{2}\sigma^2)$ and a constant diffusion coefficient of $\sigma$. Since this SDE for $X_t$ has constant coefficients, it can be integrated directly from $0$ to $t$:

$$\log S_t - \log S_0 = \int_0^t \left(\mu - \frac{1}{2}\sigma^2\right) ds + \int_0^t \sigma dW_s$$
$$\log S_t = \log S_0 + \left(\mu - \frac{1}{2}\sigma^2\right)t + \sigma W_t$$

Exponentiating both sides gives the explicit [closed-form solution](@entry_id:270799) for Geometric Brownian Motion:

$$S_t = S_0 \exp\left(\left(\mu - \frac{1}{2}\sigma^2\right)t + \sigma W_t\right)$$

From this solution, we can deduce several key properties. Since $W_t$ is a normally distributed random variable, $W_t \sim \mathcal{N}(0, t)$, the process $\log S_t$ is also normally distributed. Specifically, for any $t>0$, the distribution of $\log S_t$ is Gaussian with mean and variance given by:

$$ \mathbb{E}[\log S_t] = \log S_0 + \left(\mu - \frac{1}{2}\sigma^2\right)t $$
$$ \mathrm{Var}(\log S_t) = \sigma^2 t $$

A random variable whose logarithm is normally distributed is said to follow a **[log-normal distribution](@entry_id:139089)**. Therefore, $S_t$ is log-normally distributed for all $t > 0$.

#### Strict Positivity

A critical feature of GBM, especially in its application to asset prices, is that it remains strictly positive. This can be seen directly from the explicit solution. Given an initial value $S_0 > 0$, the value of $S_t$ is the product of $S_0$ and an exponential term. Since the argument of the exponential function is always a finite real number (as Brownian paths are continuous and finite-valued), the exponential term is always strictly positive. Consequently, $S_t > 0$ for all $t \ge 0$, almost surely.

This property distinguishes GBM from the simpler arithmetic Brownian motion (ABM), $dX_t = \mu dt + \sigma dW_t$, whose solution is $X_t = X_0 + \mu t + \sigma W_t$. An ABM process is normally distributed and its value can become negative with positive probability, regardless of its initial value. The reason for GBM's positivity lies in its **state-dependent diffusion coefficient**, $\sigma S_t$. As $S_t$ approaches zero, the magnitude of the random fluctuations, $\sigma S_t dW_t$, also diminishes, effectively preventing the process from reaching or crossing zero.

#### Moments and Modeling Implications

The explicit solution also allows for the straightforward calculation of the moments of $S_t$. To find the expected value, we use the [moment-generating function](@entry_id:154347) of a normal random variable. Recall that for $Z \sim \mathcal{N}(\nu, \tau^2)$, $\mathbb{E}[e^{kZ}] = \exp(k\nu + \frac{1}{2}k^2\tau^2)$. Applying this to $S_t = S_0 \exp(X_t)$ where $X_t = (\mu - \frac{1}{2}\sigma^2)t + \sigma W_t$:

$$ \mathbb{E}[S_t] = S_0 \mathbb{E}\left[\exp\left(\left(\mu - \frac{1}{2}\sigma^2\right)t + \sigma W_t\right)\right] $$
$$ \mathbb{E}[S_t] = S_0 \exp\left(\left(\mu - \frac{1}{2}\sigma^2\right)t\right) \mathbb{E}[e^{\sigma W_t}] $$

Since $W_t \sim \mathcal{N}(0, t)$, its [moment-generating function](@entry_id:154347) at point $\sigma$ is $\mathbb{E}[e^{\sigma W_t}] = \exp(\frac{1}{2}\sigma^2 t)$. Substituting this back gives:

$$ \mathbb{E}[S_t] = S_0 \exp\left(\mu t - \frac{1}{2}\sigma^2 t\right) \exp\left(\frac{1}{2}\sigma^2 t\right) = S_0 e^{\mu t} $$

This confirms that the drift parameter $\mu$ governs the average growth rate of the process. A similar calculation yields the second moment, $\mathbb{E}[S_t^2] = S_0^2 \exp((2\mu + \sigma^2)t)$, from which the variance is derived:

$$ \mathrm{Var}(S_t) = \mathbb{E}[S_t^2] - (\mathbb{E}[S_t])^2 = S_0^2 e^{2\mu t} (e^{\sigma^2 t} - 1) $$

From a modeling perspective, the structure of GBM implies **scale invariance**; if the price $S_t$ is rescaled by a constant factor (e.g., a change of currency), the new process follows a GBM with the same parameters $\mu$ and $\sigma$. Furthermore, the [log-returns](@entry_id:270840), $\log S_{t+\Delta t} - \log S_t$, are independent and identically distributed normal random variables. This property is known as **homoscedasticity of [log-returns](@entry_id:270840)**.

### Simulation of Geometric Brownian Motion

The analytical tractability of GBM leads to efficient and accurate simulation methods, which are essential for pricing complex derivatives and [risk management](@entry_id:141282).

#### The Exact Simulation Method (Log-Euler)

The fact that the logarithm of GBM is an arithmetic Brownian motion with an exact solution provides a powerful simulation strategy. The exact transition law between two points in time, $t_k$ and $t_{k+1}$, is given by:

$$S_{t_{k+1}} = S_{t_k} \exp\left(\left(\mu - \frac{1}{2}\sigma^2\right)(t_{k+1} - t_k) + \sigma (W_{t_{k+1}} - W_{t_k})\right)$$

Since the Brownian increment $W_{t_{k+1}} - W_{t_k}$ is a Gaussian random variable with mean $0$ and variance $\Delta t = t_{k+1} - t_k$, we can write it as $\sqrt{\Delta t} Z_k$, where $Z_k \sim \mathcal{N}(0,1)$ is a standard normal random variable. This yields the iterative simulation scheme:

$$S_{t_{k+1}} = S_{t_k} \exp\left(\left(\mu - \frac{1}{2}\sigma^2\right)\Delta t + \sigma \sqrt{\Delta t} Z_k\right)$$

This method is often called the **Log-Euler method**. It is an "exact" method in the sense that for any given time grid, the simulated values $(S_{t_0}, S_{t_1}, \dots, S_{t_N})$ have the same joint distribution as the true process sampled at those times. This means the method produces the exact [marginal distribution](@entry_id:264862) of $S_{t_n}$ at each grid point, regardless of the step size $\Delta t$. A crucial advantage of this method is that it inherently preserves the positivity of the process, as the exponential function is always positive. This method can also be extended to handle time-dependent parameters $\mu(t)$ and $\sigma(t)$ by replacing constant terms with integrals over the time step.

#### The Euler-Maruyama Method

A more direct, but naive, approach is to apply the Euler-Maruyama discretization directly to the original SDE for $S_t$. This yields the update rule:

$$\hat{S}_{t_{k+1}} = \hat{S}_{t_k} + \mu \hat{S}_{t_k} \Delta t + \sigma \hat{S}_{t_k} \sqrt{\Delta t} Z_k = \hat{S}_{t_k} (1 + \mu \Delta t + \sigma \sqrt{\Delta t} Z_k)$$

While simple to implement, this method suffers from a significant flaw: it does not guarantee positivity. For any finite step size $\Delta t$, there is a non-zero probability that the normal random variable $Z_k$ takes a large negative value, causing the term in parentheses to become negative and thus yielding a non-physical negative price. Furthermore, this scheme is biased; the expected value of the simulated process, $\mathbb{E}[\hat{S}_T] = S_0(1 + \mu \Delta t)^{T/\Delta t}$, does not equal the true mean $\mathbb{E}[S_T] = S_0 e^{\mu T}$ for finite $\Delta t$. For these reasons, the Log-Euler method is almost always preferred for simulating GBM.

### Error Analysis in Monte Carlo Simulation

When using numerical schemes for Monte Carlo estimation, it is vital to understand the nature and magnitude of the associated errors. Two primary types of error are of interest: strong error and weak error.

#### Strong and Weak Convergence

**Strong error** measures the pathwise closeness between the true process $S_T$ and its [numerical approximation](@entry_id:161970) $\hat{S}_T$. The strong terminal-time error in $L^p$ is defined as:

$$ \text{Strong Error} = \left(\mathbb{E}\left[|S_T - \hat{S}_T|^p\right]\right)^{1/p} $$

A scheme has a strong [order of convergence](@entry_id:146394) $\gamma$ if this error is of order $\mathcal{O}(h^\gamma)$, where $h$ is the step size. Strong convergence is critical when the exact path shape matters, as in the pricing of some [path-dependent options](@entry_id:140114) or in the context of advanced [variance reduction techniques](@entry_id:141433) like Multilevel Monte Carlo (MLMC).

**Weak error**, on the other hand, measures the error in expectations. For a given [test function](@entry_id:178872) $\varphi$ (representing, for example, an option payoff), the weak error is the bias of the estimator:

$$ \text{Weak Error} = \left|\mathbb{E}[\varphi(\hat{S}_T)] - \mathbb{E}[\varphi(S_T)]\right| $$

A scheme has a weak [order of convergence](@entry_id:146394) $\beta$ if this error is $\mathcal{O}(h^\beta)$. Weak error is the primary concern for pricing European-style options, where only the expectation of the final payoff is needed. The total error in a Monte Carlo estimation thus decomposes into a deterministic bias (weak error) and a statistical [sampling error](@entry_id:182646), which decreases at a rate of $\mathcal{O}(N^{-1/2})$ with the number of paths $N$.

For Lipschitz continuous payoffs $\varphi$, strong convergence implies [weak convergence](@entry_id:146650), as the weak error can be bounded by the strong error. However, the converse is not true; a scheme can have a high weak order but a low strong order.

For GBM, the standard Euler-Maruyama scheme has a **strong order of 1/2** and a **weak order of 1**. To improve [strong convergence](@entry_id:139495), one can use [higher-order schemes](@entry_id:150564) like the **Milstein method**, which for GBM achieves a **strong order of 1** while retaining a **weak order of 1**. In standard Monte Carlo, where complexity depends on the weak order, both EM and Milstein have similar performance. However, in MLMC, the higher strong order of the Milstein scheme leads to a significant improvement in computational efficiency.

### Bias in Simulating Path-Dependent Functionals

A subtle but critical issue arises when pricing path-dependent instruments, even when using the "exact" Log-Euler simulation method. While this method generates unbiased samples of the process at discrete grid points, this does not translate to unbiased estimates for functionals that depend on the [continuous path](@entry_id:156599) between these points.

Consider the task of estimating the price of an option whose payoff depends on the continuous-time supremum of the asset price, $M_T = \sup_{0 \le t \le T} S_t$. A naive simulation approach would approximate this with the maximum over the discrete grid points, $\hat{M}_T = \max_{0 \le k \le N} S_{t_k}$. Since the grid is a subset of the continuous time interval, it is always true that $\hat{M}_T \le M_T$. The process can, and almost surely will, attain its maximum between the simulation dates. This leads to a systematic **negative bias**: $\mathbb{E}[\hat{M}_T]  \mathbb{E}[M_T]$.

The consequences of this bias depend on the specific payoff. For a lookback option, whose payoff may be proportional to $M_T$, this leads to underpricing. For an **up-and-out barrier option**, which becomes worthless if $S_t$ ever touches a barrier $B$, the effect is the opposite. The simulation might fail to detect a barrier-crossing event that occurs between grid points. This leads to fewer simulated knock-outs than in reality, resulting in a **positive bias** in the estimated option price. This is a time-discretization bias, and it persists even if the grid points themselves are simulated exactly.

#### Correction via Brownian Bridge

To eliminate this [discretization](@entry_id:145012) bias, one must account for the behavior of the path between the grid points. A principled way to do this is by using properties of the **Brownian bridge**. Since the log-price process $X_t = \log S_t$ is an arithmetic Brownian motion, its path between two simulated points $(t_k, X_{t_k})$ and $(t_{k+1}, X_{t_{k+1}})$ is a Brownian bridge. The distribution of the maximum and minimum of a Brownian bridge is known analytically.

For each simulated interval $[t_k, t_{k+1}]$, one can condition on the start and end values and then use these known formulas to either:
1.  Draw a random sample of the interval's true maximum from its correct [conditional distribution](@entry_id:138367).
2.  Calculate the exact probability that the path crossed a given barrier within that interval.

By aggregating these results across all intervals (e.g., by taking the maximum of all interval maxima or checking for any barrier-crossing event), one can construct an estimator for the path-dependent functional that is free from discretization bias. This method provides an exact statistical treatment of the inter-step behavior, thereby correcting the bias inherent in discrete monitoring. It is important to note that [variance reduction techniques](@entry_id:141433) like [antithetic variates](@entry_id:143282), while useful for reducing [sampling error](@entry_id:182646), do not correct this systematic bias.