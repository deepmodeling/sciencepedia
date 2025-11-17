## Introduction
While continuous models like geometric Brownian motion have been revolutionary, they fall short in capturing the sudden, dramatic shifts that define many real-world systems, from stock market crashes to unexpected social trends. These events are not gradual fluctuations but instantaneous jumps, representing a fundamental gap in the toolkit of standard stochastic calculus. This article bridges that gap by introducing jump-diffusion [stochastic differential equations](@entry_id:146618) (SDEs), a powerful framework that marries the continuous evolution of [diffusion processes](@entry_id:170696) with the discrete shocks of [jump processes](@entry_id:180953).

This guide is structured to build your understanding from the ground up. You will learn:
- In **Principles and Mechanisms**, we will construct the theoretical foundation of jump-diffusions, starting with the Poisson random measure, defining the SDE, and deriving essential analytical tools like the Itô-Lévy formula.
- In **Applications and Interdisciplinary Connections**, we will see these theories in action, exploring their profound impact on [quantitative finance](@entry_id:139120), [credit risk](@entry_id:146012), [economic modeling](@entry_id:144051), and their connection to advanced [stochastic analysis](@entry_id:188809).
- Finally, **Hands-On Practices** will provide you with concrete exercises to solidify your command of the mathematical techniques discussed, transforming abstract concepts into practical skills.

## Principles and Mechanisms

While continuous-path models driven by Brownian motion provide a powerful framework for many systems, they are unable to capture the sudden, discontinuous shifts observed in numerous real-world phenomena, such as financial market crashes, insurance claim arrivals, or [neuronal firing](@entry_id:184180). To model such events, we must extend our toolkit to include processes that can jump. This chapter introduces the principles and mechanisms of jump-diffusion [stochastic differential equations](@entry_id:146618) (SDEs), which elegantly combine the continuous fluctuations of a diffusion with the discrete shocks of a [jump process](@entry_id:201473).

### The Poisson Random Measure: The Building Block of Jumps

The fundamental component for modeling discontinuous events is the **Poisson random measure (PRM)**, denoted $N(dt, dz)$. Conceptually, a PRM can be thought of as a random counting device that tracks the occurrence of jumps over time and their corresponding characteristics. It operates on a product space $(0, \infty) \times E$, where the first component represents time and the second, $(E, \mathcal{E})$, is a [measurable space](@entry_id:147379) called the **mark space**, which describes the properties of the jumps (e.g., their size).

The behavior of a PRM is governed by a deterministic measure called the **intensity measure**, commonly denoted $\mu(dt, dz)$. In many applications, this intensity is separable and has the form $\mu(dt, dz) = \nu(dz)dt$. Here, $dt$ represents the uniform intensity over time, while $\nu(dz)$ is a measure on the mark space $E$ known as the **Lévy measure**. The Lévy measure is central as it quantifies the expected rate at which jumps with marks in a given set $B \subset E$ occur. Specifically, $\nu(B)$ is the expected number of jumps with marks in $B$ per unit of time.

Two defining properties characterize the Poisson random measure [@problem_id:3062588]:

1.  **Poisson Counts**: For any [measurable set](@entry_id:263324) $A \subset (0, \infty) \times E$ with finite intensity $\mu(A) = \int_A \nu(dz)dt  \infty$, the random variable $N(A)$, which counts the number of jumps whose time-mark pairs fall in $A$, follows a Poisson distribution with parameter $\mu(A)$. That is, $\mathbb{P}(N(A)=k) = \frac{\exp(-\mu(A))\mu(A)^k}{k!}$. A direct consequence is that the expected number of counts is equal to the intensity: $\mathbb{E}[N(A)] = \mu(A)$. For example, the expected number of jumps with marks in a set $B \subset E$ occurring during the time interval $(s, t]$ is given by $\mathbb{E}[N((s,t] \times B)] = (t-s)\nu(B)$, provided $\nu(B)  \infty$.

2.  **Independence**: For any finite collection of pairwise disjoint measurable sets $A_1, A_2, \dots, A_n$, the random variables $N(A_1), N(A_2), \dots, N(A_n)$ are mutually independent. This property means that the number of jumps occurring in one region of the time-mark space provides no information about the number of jumps in any other non-overlapping region.

### Stochastic Integration and the Role of Compensation

With the PRM defined, we can construct the jump part of our process by summing jump contributions over time. A simple [jump process](@entry_id:201473) might be formed by the [stochastic integral](@entry_id:195087) $J_t = \int_0^t \int_E z \, N(ds, dz)$, which represents a process whose value at time $t$ is the sum of the marks (sizes) of all jumps that have occurred up to that time.

A crucial property of any stochastic integral is its expectation. Using a fundamental result known as Campbell's theorem, the expectation of an integral with respect to a PRM is the integral with respect to its intensity measure. For the process $J_t$, this yields [@problem_id:3062575]:
$$
\mathbb{E}[J_t] = \mathbb{E}\left[\int_0^t \int_E z \, N(ds, dz)\right] = \int_0^t \int_E z \, \nu(dz)ds = t \int_E z \, \nu(dz)
$$
This calculation assumes the integral $\int_E |z| \, \nu(dz)$ is finite. The result shows that $J_t$ is generally not a [martingale](@entry_id:146036), as its expectation drifts over time. In constructing SDEs, it is often mathematically convenient to work with [martingale](@entry_id:146036) components, as they have zero expected change. This motivates the concept of compensation.

We define the **compensated Poisson random measure**, $\tilde{N}(dt, dz)$, by subtracting the deterministic intensity from the random measure:
$$
\tilde{N}(dt, dz) = N(dt, dz) - \nu(dz)dt
$$
By construction, the integral of a suitable function with respect to $\tilde{N}$ has an expectation of zero. For instance, the compensated [jump process](@entry_id:201473) $\tilde{J}_t = \int_0^t \int_E z \, \tilde{N}(ds, dz)$ has expectation [@problem_id:3062575]:
$$
\mathbb{E}[\tilde{J}_t] = \mathbb{E}\left[\int_0^t \int_E z \, N(ds, dz) - \int_0^t \int_E z \, \nu(dz)ds\right] = \mathbb{E}[J_t] - t \int_E z \, \nu(dz) = 0
$$
This demonstrates that $\tilde{J}_t$ is a [martingale](@entry_id:146036). The act of compensation effectively centers the [random process](@entry_id:269605) by removing its predictable drift.

### The Jump-Diffusion Stochastic Differential Equation

We are now equipped to define a full [jump-diffusion process](@entry_id:147901), $X_t$. Such a process evolves according to a [stochastic differential equation](@entry_id:140379) that incorporates a drift term, a continuous diffusion term driven by a Brownian motion $W_t$, and a discontinuous jump term driven by a Poisson random measure. A [canonical representation](@entry_id:146693) uses the compensated PRM, as this separates the martingale components from the drift [@problem_id:3062587]:

$$
dX_t = b(X_{t-}) dt + \sigma(X_{t-}) dW_t + \int_E \gamma(X_{t-}, z) \tilde{N}(dt, dz)
$$

Let us deconstruct this fundamental equation. All processes are defined on a **filtered probability space** $(\Omega, \mathcal{F}, (\mathcal{F}_t)_{t \ge 0}, \mathbb{P})$ that satisfies the "usual conditions," a technical requirement ensuring the filtration is well-behaved. The components are:
- $b(X_{t-})$: The **drift coefficient**, determining the predictable trend of the process.
- $\sigma(X_{t-})$: The **diffusion coefficient**, scaling the magnitude of continuous, random fluctuations driven by the standard Brownian motion $W_t$.
- $\gamma(X_{t-}, z)$: The **jump coefficient**, determining the size of a jump given the state of the process just before the jump and the jump's mark $z$.
- $\tilde{N}(dt, dz)$: The compensated Poisson random measure, driving the discontinuous evolution. A standard assumption is that the Brownian motion $W_t$ and the PRM $N(dt, dz)$ are independent processes.

A subtle but critical element is the use of the **left-limit process**, $X_{t-} = \lim_{s \uparrow t} X_s$. The solution $X_t$ to a jump-diffusion SDE is inherently discontinuous. The value of the process at the exact moment of a jump, $X_t$, includes the jump itself. In contrast, $X_{t-}$ represents the state of the process an instant *before* the jump at time $t$. The theory of [stochastic integration](@entry_id:198356) requires that the integrands—in this case, the coefficients $b$, $\sigma$, and $\gamma$—be **predictable**. A process is predictable if its value at time $t$ is determined by information available strictly before time $t$. Left-continuous processes are predictable. By evaluating the coefficients at $X_{t-}$, we ensure this non-anticipating condition is met, making the stochastic integrals well-defined [@problem_id:3062584] [@problem_id:3062587].

The choice to use the compensated measure $\tilde{N}$ is one of convention. An equivalent SDE can be written using the uncompensated measure $N$. By substituting $N(dt, dz) = \tilde{N}(dt, dz) + \nu(dz)dt$ into the jump term, we see that:
$$
\int_E \gamma(X_{t-}, z) N(dt, dz) = \int_E \gamma(X_{t-}, z) \tilde{N}(dt, dz) + \left( \int_E \gamma(X_{t-}, z) \nu(dz) \right) dt
$$
This reveals that moving from the compensated to the uncompensated representation simply incorporates the compensator into the drift term. An SDE with drift $b$ and a jump term driven by $\tilde{N}$ is equivalent to one driven by $N$ with a modified drift $\tilde{b} = b - \int_E \gamma(X_{t-}, z)\nu(dz)$. For instance, in a compound Poisson setting where jumps arrive with rate $\lambda$ and have a mean size $\mu_J$, a process with drift $b$ (using the compensated measure) is equivalent to one with drift $\tilde{b} = b - \lambda\mu_J$ (using the uncompensated measure) [@problem_id:3062572].

### Properties of Solutions

#### Path Structure and Jump Dynamics

Unlike solutions to SDEs driven solely by Brownian motion, the [sample paths](@entry_id:184367) of a [jump-diffusion process](@entry_id:147901) are not continuous. They are **càdlàg** processes, a French acronym for *continue à droite, limites à gauche*, meaning they are right-continuous and have left-limits at all points. This structure perfectly captures a system that evolves continuously between jumps and experiences instantaneous shifts at jump times.

The size of a jump at time $t$ is formally defined as the difference between the process value and its left-limit: $\Delta X_t = X_t - X_{t-}$. We can derive an explicit expression for this jump by examining the integral form of the SDE [@problem_id:3062584]:
$$
X_t = X_0 + \int_0^t b(X_{s-}) ds + \int_0^t \sigma(X_{s-}) dW_s + \int_0^t \int_E \gamma(X_{s-}, z) \tilde{N}(ds, dz)
$$
The first two integral terms, the drift and the diffusion (Itô) integral, are both continuous processes in $t$. Therefore, they cannot contribute to any jump; their value at time $t$ is the same as their left-limit. Any discontinuity must arise from the final term, the integral with respect to the Poisson measure. The jump of the process is thus the jump of this integral, which is given by the sum of all jump contributions occurring exactly at time $t$. This can be written compactly as:
$$
\Delta X_t = \int_E \gamma(X_{t-}, z) N(\{t\}, dz)
$$
Here, $N(\{t\}, dz)$ is a random measure that is non-zero only if a jump occurs at time $t$, in which case it identifies the marks of the jump(s). This formula confirms our intuition: the jump size at time $t$ is determined by the state of the system just before the jump, $X_{t-}$, via the function $\gamma$.

#### Existence and Uniqueness of Strong Solutions

To ensure that the SDE has a unique solution that behaves predictably (i.e., does not "explode" to infinity in finite time), we must impose conditions on the coefficients $b$, $\sigma$, and $\gamma$. These are direct extensions of the conditions for SDEs without jumps. The standard [sufficient conditions](@entry_id:269617) are a **global Lipschitz condition** and a **[linear growth condition](@entry_id:201501)** [@problem_id:3062562] [@problem_id:3062548].

For all $x, y \in \mathbb{R}^d$, there must exist constants $L > 0$ and $K > 0$ such that:

1.  **Global Lipschitz Condition**:
    $$
    |b(x) - b(y)|^2 + \|\sigma(x) - \sigma(y)\|_{\mathrm{F}}^2 + \int_E |\gamma(x,z) - \gamma(y,z)|^2\,\nu(dz) \le L^2\,|x - y|^2
    $$
    This condition bounds the change in the coefficients by the change in the state variable. It is essential for proving uniqueness by ensuring that two solutions starting close together cannot diverge too quickly. Note how the jump coefficient $\gamma$ is included through an $L^2(\nu)$ norm.

2.  **Linear Growth Condition**:
    $$
    |b(x)|^2 + \|\sigma(x)\|_{\mathrm{F}}^2 + \int_E |\gamma(x,z)|^2\,\nu(dz) \le K^2\,(1 + |x|^2)
    $$
    This condition restricts the coefficients from growing faster than linearly with the state. It is crucial for proving existence on any finite time horizon by preventing the solution's moments from exploding.

Under these conditions, for any initial value $X_0$ with a finite second moment, there exists a unique, pathwise càdlàg adapted solution to the SDE.

### Fundamental Tools for Analysis

#### Itô's Formula for Jump-Diffusions

One of the most powerful tools in stochastic calculus is Itô's formula, which acts as a [chain rule](@entry_id:147422) for functions of stochastic processes. For jump-diffusions, this extends to the **Itô-Lévy formula**. For a sufficiently [smooth function](@entry_id:158037) $f \in C^2(\mathbb{R})$, its differential $df(X_t)$ is given by [@problem_id:3062546]:
$$
\begin{aligned}
df(X_t) =  \left[ f'(X_{t-})b(X_{t-}) + \frac{1}{2}f''(X_{t-})\sigma^2(X_{t-}) + \int_E \Big(f(X_{t-}+\gamma(X_{t-},z)) - f(X_{t-}) - f'(X_{t-})\gamma(X_{t-},z)\Big)\nu(dz) \right] dt \\
 + f'(X_{t-})\sigma(X_{t-})dW_t \\
 + \int_E \Big(f(X_{t-}+\gamma(X_{t-},z)) - f(X_{t-})\Big)\tilde{N}(dt,dz)
\end{aligned}
$$
This formula contains three types of terms:
- The **predictable drift part** (the $dt$ term): It includes the classical Itô drift ($f'b + \frac{1}{2}f''\sigma^2$) plus an additional integral term. This new term represents the expected change in $f$ due to jumps, adjusted by a first-order Taylor expansion term, which arises from the compensation.
- The **[continuous martingale](@entry_id:185466) part** (the $dW_t$ term): This is identical to the standard Itô formula.
- The **discontinuous martingale part** (the $\tilde{N}(dt,dz)$ term): This integral captures the actual, random changes in $f$ at jump times. The integrand, $f(X_{t-}+\gamma) - f(X_{t-})$, is simply the change in the function $f$ caused by a jump.

#### The Infinitesimal Generator

The drift part of the Itô-Lévy formula is an object of profound importance: the **[infinitesimal generator](@entry_id:270424)** of the process, denoted $\mathcal{L}$. It is formally defined as the expected instantaneous rate of change of a function of the state:
$$
\mathcal{L}f(x) = \lim_{t \downarrow 0} \frac{\mathbb{E}_x[f(X_t)] - f(x)}{t}
$$
For a [jump-diffusion process](@entry_id:147901), the generator takes the form [@problem_id:3062563]:
$$
\mathcal{L}f(x) = \underbrace{b(x)f'(x) + \frac{1}{2}\sigma^2(x)f''(x)}_{\text{Diffusion Part}} + \underbrace{\int_E \Big[ f(x+\gamma(x,z)) - f(x) - f'(x)\gamma(x,z) \Big] \nu(dz)}_{\text{Jump Part}}
$$
The generator is a powerful analytical tool. It connects the SDE to a family of partial integro-differential equations (the Kolmogorov equations) and establishes a fundamental property: for any suitable function $f$, the process $M_t^f = f(X_t) - f(X_0) - \int_0^t \mathcal{L}f(X_s) ds$ is a [local martingale](@entry_id:203733).

### Decomposing Jumps: The Lévy-Itô Decomposition

The structure of the Lévy measure $\nu$ determines the nature of the jumps. It is often insightful to decompose the [jump process](@entry_id:201473) according to the size of the jumps. This is the essence of the **Lévy-Itô decomposition**. A standard approach is to use a truncation threshold (e.g., at $|z|=1$) to separate "small" jumps from "large" jumps [@problem_id:3062568].

1.  **Large Jumps** ($|z| > 1$): For a process to be well-behaved, it cannot have an infinite number of large jumps in a finite time. This requires that the rate of large jumps be finite: $\int_{|z|>1} \nu(dz)  \infty$. The process of large jumps, $\int_0^t \int_{|z|>1} z N(ds, dz)$, is a **compound Poisson process**. Because it has finite activity (a finite number of jumps on any finite time interval), it is well-defined without compensation.

2.  **Small Jumps** ($|z| \le 1$): The Lévy measure may allow for an infinite rate of small jumps, i.e., $\int_{|z|\le 1} \nu(dz) = \infty$. Such a process has infinite activity. Attempting to sum these jumps directly may fail. However, if the variance of the small jumps is finite, i.e., $\int_{|z|\le 1} |z|^2 \nu(dz)  \infty$, then the [compensated integral](@entry_id:181695) $\int_0^t \int_{|z|\le 1} z \tilde{N}(ds, dz)$ is a well-defined square-integrable [martingale](@entry_id:146036).

The two conditions—finite activity for large jumps and [finite variance](@entry_id:269687) for small jumps—are precisely the defining properties of a Lévy measure. This decomposition allows any [jump process](@entry_id:201473) driven by a Lévy measure to be written as the sum of a finite-activity compound Poisson process (large jumps), a zero-mean [martingale](@entry_id:146036) with potentially infinite activity (compensated small jumps), and a deterministic drift adjustment arising from the compensation [@problem_id:3062568]. This powerful decomposition is central to both the theory and simulation of jump-[diffusion processes](@entry_id:170696).