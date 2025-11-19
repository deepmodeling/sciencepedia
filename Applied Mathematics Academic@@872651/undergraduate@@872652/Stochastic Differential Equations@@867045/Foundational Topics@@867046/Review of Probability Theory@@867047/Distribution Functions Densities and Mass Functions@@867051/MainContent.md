## Introduction
The solution to a stochastic differential equation (SDE) is not a single number but a random path—a stochastic process whose behavior must be described in the language of probability. A fundamental challenge, therefore, is to characterize the distribution of the process's state at any given moment in time. This article provides the essential toolkit for this task by exploring the foundational concepts of distribution functions, densities, and mass functions.

We will embark on a structured journey to master these tools. The first chapter, "Principles and Mechanisms," lays the theoretical groundwork, introducing the cumulative distribution function (CDF) as a universal descriptor, dissecting its structure through Lebesgue's decomposition theorem, and examining the dynamics of distributions via the powerful Kolmogorov equations. Following this, "Applications and Interdisciplinary Connections" will showcase how these concepts are applied to model real-world phenomena in physics, finance, and ecology, and how they serve as the backbone for statistical inference. Finally, "Hands-On Practices" will provide an opportunity to solidify these concepts through guided problems, connecting theory to practical calculation. By the end, you will have a robust understanding of how to describe and analyze the probabilistic nature of solutions to stochastic differential equations.

## Principles and Mechanisms

The solution to a [stochastic differential equation](@entry_id:140379) (SDE) is a stochastic process, a path-valued random object. To analyze such processes, we must be able to characterize the probability distributions of the solution at various points in time. This chapter lays the groundwork for this analysis by introducing the fundamental tools used to describe probability distributions: distribution functions, densities, and mass functions. We will explore their formal properties, their interrelationships through the lens of Lebesgue's decomposition theorem, and the dynamical equations that govern their evolution in time.

### The Cumulative Distribution Function: A Universal Descriptor

The most fundamental object describing the distribution of a real-valued random variable $X$ is its **[cumulative distribution function](@entry_id:143135) (CDF)**. For a random variable $X_t$ representing the state of a [stochastic process](@entry_id:159502) at a fixed time $t$, its CDF, denoted $F_{X_t}(x)$, is defined as the probability that the variable takes on a value less than or equal to $x$:

$$
F_{X_t}(x) = \mathbb{P}(X_t \le x), \quad \text{for } x \in \mathbb{R}
$$

Regardless of how the random variable is generated—whether as the solution to an SDE or through some other random mechanism—its CDF must satisfy a [universal set](@entry_id:264200) of properties that derive directly from the [axioms of probability](@entry_id:173939). These properties make the CDF a cornerstone of probability theory. Let's consider a generic real-valued random variable $X$ and its CDF $F_X(x)$.

First, for any two points $x_1 \le x_2$, the event $\{X \le x_1\}$ is a subset of the event $\{X \le x_2\}$. By the [monotonicity](@entry_id:143760) of probability measures, this implies $\mathbb{P}(X \le x_1) \le \mathbb{P}(X \le x_2)$, which means $F_X(x_1) \le F_X(x_2)$. Therefore, **a CDF is always a [non-decreasing function](@entry_id:202520)**.

Second, a real-valued random variable must take on a value in $\mathbb{R}$. As $x$ approaches infinity, the event $\{X \le x\}$ expands to include the entire sample space, so its probability approaches 1. Conversely, as $x$ approaches negative infinity, the event $\{X \le x\}$ shrinks to the [empty set](@entry_id:261946), and its probability approaches 0. Formally, we have the limit properties:

$$
\lim_{x \to -\infty} F_X(x) = 0 \quad \text{and} \quad \lim_{x \to +\infty} F_X(x) = 1
$$

Third, a defining convention in modern probability theory is that the CDF is **right-continuous**. This means that for any point $x$, the limit of $F_X(y)$ as $y$ approaches $x$ from the right is equal to $F_X(x)$ itself: $\lim_{y \downarrow x} F_X(y) = F_X(x)$. This property is a direct consequence of the continuity of probability measures for decreasing sequences of sets.

While a CDF is always right-continuous, it is not necessarily left-continuous. The potential discrepancy between the function's value at a point and its [left-hand limit](@entry_id:139055) reveals another crucial feature. The [left-hand limit](@entry_id:139055), $\lim_{y \uparrow x} F_X(y)$, can be shown to equal $\mathbb{P}(X \lt x)$. The difference between the value at $x$ and this limit gives the probability that the random variable is exactly equal to $x$:

$$
F_X(x) - \lim_{y \uparrow x} F_X(y) = \mathbb{P}(X \le x) - \mathbb{P}(X \lt x) = \mathbb{P}(X = x)
$$

This quantity, $\mathbb{P}(X=x)$, is known as a **point mass** or an **atom** of the distribution. A jump discontinuity in the CDF at a point $x$ signals that the random variable can take the value $x$ with non-zero probability [@problem_id:3049555]. If the CDF is continuous at $x$, then $\mathbb{P}(X=x)=0$.

### The Lebesgue Decomposition: Dissecting a Distribution

The properties of the CDF allow us to classify probability distributions. The celebrated **Lebesgue decomposition theorem** states that any CDF, $F_X$, can be uniquely decomposed into a sum of three components:

$$
F_X = F_{\mathrm{ac}} + F_{\mathrm{s}} + F_{\mathrm{d}}
$$

Here, $F_{\mathrm{ac}}$ is an **absolutely continuous** part, $F_{\mathrm{s}}$ is a **singular continuous** part, and $F_{\mathrm{d}}$ is a **discrete** (or jump) part. Understanding these components is key to understanding the rich variety of distributions that can arise from stochastic processes.

#### The Discrete Part and Probability Mass Functions

A distribution is purely discrete if all its probability is concentrated on a countable set of points. In this case, $F_X = F_{\mathrm{d}}$. The distribution is completely described by its **probability [mass function](@entry_id:158970) (PMF)**, $p_X(k) = \mathbb{P}(X=k)$, for each value $k$ in the countable support of $X$. The CDF is then a step function, constant between the points of support and jumping at each of them. The size of the jump at point $k$ is precisely the probability mass $p_X(k)$ [@problem_id:3049604].

A classic example from [stochastic processes](@entry_id:141566) is the number of events in a homogeneous Poisson process $\{N_t\}_{t \ge 0}$ with rate $\lambda$ by a fixed time $T$. The random variable $X = N_T$ follows a Poisson distribution with parameter $\lambda T$. Its support is the set of non-negative integers $\{0, 1, 2, \dots\}$, and its PMF is given by:

$$
p_X(k) = \mathbb{P}(X=k) = e^{-\lambda T} \frac{(\lambda T)^k}{k!}, \quad k=0,1,2,\dots
$$

The CDF, $F_X(x) = \mathbb{P}(X \le x)$, is constant on any interval $[m, m+1)$ for an integer $m \ge 0$, and for any $x$ in this interval, its value is the sum of the masses up to $m$:

$$
F_X(x) = \sum_{k=0}^{m} p_X(k) \quad \text{for } x \in [m, m+1)
$$

This function is a pure [step function](@entry_id:158924), embodying a purely [discrete distribution](@entry_id:274643) [@problem_id:3049604].

#### The Absolutely Continuous Part and Probability Density Functions

A distribution is absolutely continuous if its CDF can be expressed as the integral of a non-negative function, $f_X(x)$, called the **probability density function (PDF)**. In this case, $F_X = F_{\mathrm{ac}}$. The relationship is given by:

$$
F_X(x) = \int_{-\infty}^{x} f_X(u) \, du
$$

This integral representation implies that the CDF of an absolutely [continuous random variable](@entry_id:261218) is, in fact, an [absolutely continuous function](@entry_id:190100) in the sense of [real analysis](@entry_id:145919). By the Fundamental Theorem of Calculus for Lebesgue integrals, the CDF is [differentiable almost everywhere](@entry_id:160094), and its derivative is the PDF: $F_X'(x) = f_X(x)$ at all points where $f_X$ is continuous [@problem_id:3049615].

The existence of a PDF has a profound consequence: for any single point $c$, the probability is zero. This is because the probability of an interval is the area under the PDF curve, and the area over a single point is zero:

$$
\mathbb{P}(a \lt X \le b) = F_X(b) - F_X(a) = \int_a^b f_X(u) \, du, \quad \text{so } \mathbb{P}(X=c) = \int_c^c f_X(u) \, du = 0
$$

This means that an absolutely continuous distribution has no point masses. Conversely, if a random variable has a [point mass](@entry_id:186768), $\mathbb{P}(X=c) > 0$, its distribution cannot be described by a PDF alone [@problem_id:3049615]. Furthermore, the PDF is not unique; it can be changed on a set of Lebesgue measure zero (e.g., at a finite number of points) without altering any probability calculations, as such changes do not affect the value of its integral [@problem_id:3049615].

#### The Singular Continuous Part

The most counterintuitive component is the singular continuous distribution. Here, $F_X = F_{\mathrm{s}}$. The CDF is continuous everywhere (so there are no point masses, $\mathbb{P}(X=x)=0$ for all $x$), but the function increases only on a set of Lebesgue measure zero. This means the derivative of the CDF is zero "[almost everywhere](@entry_id:146631)," so it cannot be recovered by integrating its derivative. The canonical example is the **Cantor distribution**, whose CDF (the "[devil's staircase](@entry_id:143016)") is constant on the infinitely many intervals removed to construct the Cantor set, yet rises from 0 to 1 entirely on the Cantor set itself, which has [measure zero](@entry_id:137864). While less common in introductory applications, such distributions can arise in more complex models.

#### Mixed Distributions

Many stochastic processes lead to **mixed distributions**, where two or three components of the Lebesgue decomposition are present. A powerful way to understand this is through a mixture model [@problem_id:3049528]. Imagine a process where, with probability $\beta$, the outcome $X$ is drawn from a Gaussian distribution (absolutely continuous); with probability $\alpha$, from a Cantor distribution (singular continuous); and with probability $\gamma = 1 - \alpha - \beta$, the outcome is deterministically set to 0 (discrete). The resulting CDF is a weighted sum of the three component CDFs: $F_X(x) = \beta F_{\text{Gaussian}}(x) + \alpha F_{\text{Cantor}}(x) + \gamma F_{\text{Discrete}}(x)$. The Lebesgue decomposition of $F_X$ is simply the sum of the corresponding weighted components:
- The absolutely continuous part has the density $f_{\mathrm{ac}}(x) = \beta f_{\text{Gaussian}}(x)$.
- The singular continuous part is $F_{\mathrm{s}}(x) = \alpha F_{\text{Cantor}}(x)$.
- The discrete part consists of a single point mass $p_X(0) = \gamma$ at the origin.

A highly relevant example in SDEs is a [diffusion process](@entry_id:268015) on a domain with an **[absorbing boundary](@entry_id:201489)**. Consider a process $X_t$ on $[a, \infty)$ starting at $X_0 > a$, which is absorbed upon hitting $a$. For any time $t>0$, there is a non-zero probability, $\mathbb{P}(\tau_a \le t)$, that the process has already been absorbed, where $\tau_a$ is the [first hitting time](@entry_id:266306) of $a$. This creates a point mass of size $\mathbb{P}(\tau_a \le t)$ at the point $x=a$. For paths that have not been absorbed, their positions are distributed over $(a, \infty)$ according to a "sub-probability" density $p(t,x)$. The total mass of this density is the [survival probability](@entry_id:137919), $\int_a^\infty p(t,x) \, dx = \mathbb{P}(\tau_a > t)$. The complete law of $X_t$ is therefore a [mixed distribution](@entry_id:272867) with a discrete part (the atom at $a$) and an absolutely continuous part (the density on $(a, \infty)$) [@problem_id:3049541].

### Calculating Expectations

Once the distribution of a random variable $X$ is known, we can compute the expectation of any well-behaved function $g(X)$. The expectation, $\mathbb{E}[g(X)]$, represents the probability-weighted average of the values of $g(X)$. The formula depends on the type of distribution.

- If $X$ is a [discrete random variable](@entry_id:263460) with PMF $p_X(k)$, the expectation is a sum:
$$ \mathbb{E}[g(X)] = \sum_{k} g(k) p_X(k) $$
- If $X$ is an absolutely [continuous random variable](@entry_id:261218) with PDF $f_X(x)$, the expectation is an integral:
$$ \mathbb{E}[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x) \, dx $$

For a concrete example, let's consider the Ornstein-Uhlenbeck process, which models mean-reverting behavior and is described by the SDE $dX_t = -\theta(X_t - m)dt + \sigma dW_t$ with $X_0=x_0$. The solution at a fixed time $T > 0$ can be found explicitly. It is a random variable $X_T$ that follows a normal (Gaussian) distribution. Its mean $\mu_{X_T}$ and variance $\sigma^2_{X_T}$ are:
$$
\mu_{X_T} = m + (x_0 - m)e^{-\theta T}
$$
$$
\sigma^2_{X_T} = \frac{\sigma^2}{2\theta}(1 - e^{-2\theta T})
$$
Since $X_T$ is a [continuous random variable](@entry_id:261218) with a known PDF—the Gaussian density $f_{X_T}(x) = \frac{1}{\sqrt{2\pi\sigma^2_{X_T}}} \exp(-\frac{(x-\mu_{X_T})^2}{2\sigma^2_{X_T}})$—we can compute the expectation of any function $g(X_T)$ by integration. A particularly important case is the **[moment-generating function](@entry_id:154347)**, which corresponds to $g(x) = e^{\lambda x}$. By computing the integral $\mathbb{E}[e^{\lambda X_T}] = \int_{-\infty}^{\infty} e^{\lambda x} f_{X_T}(x) dx$, one finds the well-known result for a normal distribution [@problem_id:3049560]:
$$
\mathbb{E}[e^{\lambda X_T}] = \exp\left(\lambda \mu_{X_T} + \frac{1}{2}\lambda^2 \sigma^2_{X_T}\right)
$$
This demonstrates the standard workflow: solve the SDE to find the distribution of $X_T$, identify its PDF, and then use the integral definition of expectation.

### The Dynamics of Distributions: Kolmogorov Equations

For a Markovian [stochastic process](@entry_id:159502) $\{X_t\}$, the distribution of $X_t$ evolves over time. This evolution can be described by a **[transition probability](@entry_id:271680) density**, denoted $p(s,x; t,y)$. This function represents the probability density of the process being at state $y$ at time $t$, given that it was at state $x$ at time $s  t$. More formally, if the conditional law of $X_t$ given $X_s=x$, denoted $P_{s,t}(x, \cdot)$, is absolutely continuous with respect to the Lebesgue measure, then the transition density is its Radon-Nikodym derivative [@problem_id:3049586]:
$$
\mathbb{P}(X_t \in A | X_s = x) = \int_A p(s,x; t,y) \, dy
$$
As a density in the variable $y$, it must integrate to 1 over the entire state space: $\int_{\mathbb{R}} p(s,x; t,y) \, dy = 1$.

For [diffusion processes](@entry_id:170696) that are solutions to SDEs, the evolution of this density is governed by a partial differential equation (PDE). The **Kolmogorov Forward Equation**, also known as the **Fokker-Planck Equation**, describes how the probability density $p(t,y)$ of being at state $y$ at time $t$ evolves. For an SDE of the form $dX_t = b(t, X_t) dt + \sigma(t, X_t) dW_t$, the equation is:
$$
\frac{\partial p(t,y)}{\partial t} = -\frac{\partial}{\partial y} \left( b(t,y) p(t,y) \right) + \frac{1}{2} \frac{\partial^2}{\partial y^2} \left( \sigma(t,y)^2 p(t,y) \right)
$$
The first term on the right, involving the drift $b$, describes transport of probability mass, much like a convection term. The second term, involving the diffusion coefficient $\sigma$, describes the spreading of probability, like a diffusion term.

The most fundamental example is standard one-dimensional Brownian motion, corresponding to the SDE $dX_t = dW_t$ (so $b=0, \sigma=1$). Its transition density, starting from $x$ at time $0$, is the Gaussian or "heat kernel":
$$
p(t,x,y) = \frac{1}{\sqrt{2\pi t}} \exp\left(-\frac{(y-x)^2}{2t}\right)
$$
A direct calculation shows that this function satisfies the Fokker-Planck equation, which in this case simplifies to the classical **heat equation** [@problem_id:3049607]:
$$
\frac{\partial p}{\partial t} = \frac{1}{2} \frac{\partial^2 p}{\partial y^2}
$$
The initial condition is that at $t=0$, all probability is concentrated at the starting point $x$, i.e., $p(0,x,y) = \delta(y-x)$, where $\delta$ is the Dirac delta distribution.

### Deeper Mechanisms and Applications

#### Stationary Distributions

A natural question is whether a process settles into an equilibrium state. A **stationary distribution** is a probability distribution that does not change over time. If a process $X_t$ has a stationary density $\pi(y)$, then if the initial state $X_0$ is drawn from this distribution, the state $X_t$ will have the same distribution for all $t0$. To find such a density, we seek a time-independent solution to the Fokker-Planck equation, i.e., we set $\partial_t p = 0$:
$$
0 = -\frac{d}{dy} \left( b(y) \pi(y) \right) + \frac{1}{2} \frac{d^2}{dy^2} \left( \sigma(y)^2 \pi(y) \right)
$$
This condition implies that the [probability current](@entry_id:150949) is constant, and with [natural boundary conditions](@entry_id:175664) at infinity, this constant must be zero. This leaves a first-order ODE that can often be solved for $\pi(y)$, which is then normalized to integrate to 1. For many processes, particularly those with a restoring drift that pulls the process back to a central region, a unique [stationary distribution](@entry_id:142542) exists and the process is ergodic, meaning the distribution of $X_t$ will converge to this stationary distribution as $t \to \infty$ regardless of the starting point [@problem_id:3049618].

#### Duality of Forward and Backward Equations

The Fokker-Planck equation describes the evolution of densities. There is a dual equation, the **Kolmogorov Backward Equation**, which describes the evolution of expectations of functions of the process, like $u(s,x) = \mathbb{E}[g(X_t) | X_s=x]$. The backward equation involves an operator $\mathcal{L}$, the [infinitesimal generator](@entry_id:270424) of the process, and is given by $\partial_s u + \mathcal{L}u = 0$. The forward and backward equations are deeply connected through a mathematical property called duality. The operator governing the forward equation, $\mathcal{L}^*$, is the formal adjoint of the generator $\mathcal{L}$. This duality implies that the integral $\int u(t,y) p(t,y) dy$ is constant in time. This conservation law is a powerful theoretical tool, connecting the "forward" picture of evolving densities with the "backward" picture of evolving expectations [@problem_id:3049534].

#### Change of Measure and Girsanov's Theorem

A final, powerful mechanism is the ability to change the probability measure itself. **Girsanov's theorem** provides a formal procedure for changing the drift of a process by defining a new probability measure $\mathbb{Q}$ that is related to the original measure $\mathbb{P}$ via a Radon-Nikodym derivative. On any finite time interval $[0,t]$, this [change of measure](@entry_id:157887) is such that the measures $\mathbb{P}$ and $\mathbb{Q}$ are **equivalent**. This means they are mutually absolutely continuous: an event has probability zero under $\mathbb{P}$ if and only if it has probability zero under $\mathbb{Q}$ [@problem_id:3049582]. This technique is indispensable in [mathematical finance](@entry_id:187074) for moving from the "real-world" measure to a "risk-neutral" measure for pricing financial derivatives, and it serves as a cornerstone of the modern theory of [stochastic integration](@entry_id:198356).