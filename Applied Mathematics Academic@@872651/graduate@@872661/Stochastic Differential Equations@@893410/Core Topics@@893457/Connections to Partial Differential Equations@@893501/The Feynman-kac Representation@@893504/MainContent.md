## Introduction
The worlds of deterministic partial differential equations (PDEs) and random [stochastic processes](@entry_id:141566), though seemingly distinct, are connected by a bridge of remarkable elegance and power: the Feynman-Kac representation. This fundamental theorem asserts that the solution to a broad class of linear PDEs can be found not by classical analytical methods, but by calculating the expected value of a functional over an ensemble of random paths. This probabilistic viewpoint revolutionizes our ability to understand and solve these equations, particularly in high-dimensional settings where traditional numerical methods fail. It resolves the challenge of finding solutions to complex PDEs by reformulating them into more [tractable problems](@entry_id:269211) of averaging over stochastic trajectories.

This article provides a comprehensive exploration of this profound connection, guiding you from first principles to advanced applications.
* In **Principles and Mechanisms**, we will construct the Feynman-Kac formula from the ground up, starting with the infinitesimal generator that links an SDE to a PDE, and rigorously prove the representation using [martingale](@entry_id:146036) calculus.
* In **Applications and Interdisciplinary Connections**, we will witness the formula in action, uncovering its pivotal role in pricing financial derivatives, grounding the [path integrals](@entry_id:142585) of quantum mechanics, and solving problems in [potential theory](@entry_id:141424).
* Finally, **Hands-On Practices** will offer a series of guided problems to solidify your understanding, allowing you to apply the theory to concrete examples from diffusion, [jump processes](@entry_id:180953), and [spectral analysis](@entry_id:143718).

We begin our journey by delving into the core principles that make this powerful representation possible.

## Principles and Mechanisms

The Feynman-Kac representation establishes a profound and powerful link between the world of [partial differential equations](@entry_id:143134) (PDEs) and the realm of [stochastic processes](@entry_id:141566). It asserts that solutions to a large class of linear parabolic and elliptic PDEs can be expressed as expectations of functionals of a corresponding stochastic differential equation (SDE). This bridge is not merely a theoretical curiosity; it provides a vital tool for both analysis and computation. Analytically, it allows methods from probability theory, such as [martingale](@entry_id:146036) techniques, to be applied to the study of PDEs. Computationally, it forms the basis of Monte Carlo methods for solving high-dimensional PDEs, which are often intractable with traditional grid-based numerical schemes. This chapter will build the Feynman-Kac formula from first principles, explore its meaning, and outline its most important extensions and theoretical underpinnings.

### The Infinitesimal Generator: A Bridge Between Dynamics and Operators

The connection between an SDE and a PDE is mediated by a differential operator known as the **infinitesesimal generator**. Consider a time-homogeneous Itô diffusion process $(X_t)_{t \ge 0}$ in $\mathbb{R}^d$ that solves the SDE:

$$dX_t = b(X_t)dt + \sigma(X_t)dW_t, \quad X_0 = x$$

where $W_t$ is a standard $m$-dimensional Brownian motion, and the drift $b: \mathbb{R}^d \to \mathbb{R}^d$ and diffusion coefficient $\sigma: \mathbb{R}^d \to \mathbb{R}^{d \times m}$ satisfy conditions ensuring the existence of a unique, non-explosive solution. This process defines a **Markov semigroup** $(P_t)_{t \ge 0}$, which describes the evolution of observables. For a bounded, measurable function $f: \mathbb{R}^d \to \mathbb{R}$, the action of the semigroup is defined as the expected value of $f$ evaluated at the process's future state:

$$(P_t f)(x) := \mathbb{E}_x[f(X_t)] = \mathbb{E}[f(X_t) | X_0=x]$$

The infinitesimal generator $\mathcal{L}$ of the process (and its semigroup) captures the [instantaneous rate of change](@entry_id:141382) of this expected value. Formally, for a function $f$ in the domain of the generator, $D(\mathcal{L})$, its action is defined by the limit:

$$(\mathcal{L} f)(x) = \lim_{t \downarrow 0} \frac{(P_t f)(x) - f(x)}{t} = \lim_{t \downarrow 0} \frac{\mathbb{E}_x[f(X_t)] - f(x)}{t}$$

While this definition is abstract, for sufficiently smooth functions, we can find a concrete expression for $\mathcal{L}$ using Itô's formula. Let $f \in C_b^2(\mathbb{R}^d)$, the space of twice continuously differentiable functions with bounded derivatives. Applying Itô's formula to $f(X_t)$ gives:

$$f(X_t) - f(x) = \int_0^t \nabla f(X_s) \cdot dX_s + \frac{1}{2} \int_0^t \mathrm{Tr}\left(\sigma(X_s)\sigma(X_s)^\top D^2 f(X_s)\right) ds$$

Substituting the SDE for $dX_s$ and taking the expectation $\mathbb{E}_x[\cdot]$ causes the [stochastic integral](@entry_id:195087) term (which is a martingale) to vanish:

$$\mathbb{E}_x[f(X_t)] - f(x) = \mathbb{E}_x \left[ \int_0^t \left( b(X_s) \cdot \nabla f(X_s) + \frac{1}{2}\mathrm{Tr}\left(a(X_s) D^2 f(X_s)\right) \right) ds \right]$$

where $a(x) = \sigma(x)\sigma(x)^\top$ is the [diffusion matrix](@entry_id:182965). Dividing by $t$ and taking the limit as $t \downarrow 0$, the continuity of the integrand allows us to evaluate it at time $s=0$ and position $x$. This reveals that for any $f \in C_b^2(\mathbb{R}^d)$, the limit defining $(\mathcal{L}f)(x)$ exists and is equal to a second-order partial differential operator [@problem_id:3001175]:

$$(\mathcal{L}f)(x) = b(x) \cdot \nabla f(x) + \frac{1}{2}\mathrm{Tr}\left(a(x) D^2 f(x)\right)$$

This operator is the cornerstone of the Feynman-Kac representation. It is crucial to note that the domain $D(\mathcal{L})$ is a strict subset of all bounded [measurable functions](@entry_id:159040); the limit does not exist for functions lacking sufficient regularity.

It is instructive to contrast the PDE associated with the Feynman-Kac formula, the **Kolmogorov backward equation**, with its dual, the **Fokker-Planck equation** (or Kolmogorov forward equation). The backward equation, which we will study in depth, describes the evolution of an expected value backward in time from a terminal condition. The forward equation describes the evolution of the probability density $\rho(t,x)$ of the process $X_t$ forward in time from an initial density. It is governed by the formal adjoint of the generator, $\mathcal{L}^*$, and takes the form $\partial_t \rho = \mathcal{L}^* \rho$ [@problem_id:3001163]. Our focus remains on the backward equation, as it is the one whose solution is given by the Feynman-Kac formula.

### The Feynman-Kac Representation: Statement and Proof

Let us now consider a general linear parabolic terminal value problem. We seek a function $u(t,x)$ that solves:

$$\partial_t u(t,x) + (\mathcal{L}u)(t,x) - V(t,x)u(t,x) = -f(t,x), \quad (t,x) \in [0,T) \times \mathbb{R}^d$$

with the terminal condition:

$$u(T,x) = g(x), \quad x \in \mathbb{R}^d$$

Here, $\mathcal{L}$ is the [infinitesimal generator](@entry_id:270424) corresponding to the SDE for a process $X_s^{t,x}$ starting at $X_t=x$. The function $V(t,x)$ is a **potential** (or killing rate), $f(t,x)$ is an inhomogeneous **[source term](@entry_id:269111)**, and $g(x)$ is the **terminal payoff**.

The Feynman-Kac formula states that, under suitable regularity conditions on the coefficients and functions, the unique classical solution to this PDE is given by the following [conditional expectation](@entry_id:159140) [@problem_id:3001120]:

$$u(t,x) = \mathbb{E}_{t,x} \left[ \exp\left(-\int_t^T V(s,X_s) ds\right) g(X_T) + \int_t^T \exp\left(-\int_t^s V(r,X_r) dr\right) f(s,X_s) ds \right]$$

This representation is remarkable. It recasts the solution of a deterministic PDE as an average over a vast ensemble of random paths. The solution at $(t,x)$ is a sum of two parts: the expected terminal payoff $g(X_T)$, discounted back to time $t$ along the path, and the sum of all intermediate source contributions $f(s,X_s)$, each discounted from its time of occurrence $s$ back to time $t$.

#### Proof by Martingale Method

The validity of this representation can be rigorously established using Itô calculus. The proof architecture itself provides deep insight into the connection between the PDE and the SDE [@problem_id:3001178]. Assuming a classical solution $u \in C^{1,2}$ exists, we can verify that it must have the probabilistic form above. The core strategy is to construct a process that, by virtue of $u$ solving the PDE, becomes a [martingale](@entry_id:146036).

Let's fix $(t,x)$ and consider the process $X_s = X_s^{t,x}$ for $s \in [t,T]$. We define two auxiliary processes:
1. The discount factor process: $\Gamma_s = \exp\left(-\int_t^s V(r, X_r) dr\right)$
2. The solution evaluated along the path: $U_s = u(s, X_s)$

Now, we construct a new process $Y_s$ for $s \in [t,T]$:

$$Y_s = \Gamma_s U_s + \int_t^s \Gamma_r f(r, X_r) dr = \exp\left(-\int_t^s V(r,X_r)dr\right)u(s,X_s) + \int_t^s \exp\left(-\int_t^r V(\tau,X_\tau)d\tau\right) f(r,X_r) dr$$

The key step is to compute the differential $dY_s$ using Itô's product rule on $\Gamma_s U_s$ and the [fundamental theorem of calculus](@entry_id:147280) on the integral term. The differential of $\Gamma_s$ is $d\Gamma_s = -\Gamma_s V(s,X_s) ds$. The differential of $U_s = u(s,X_s)$ via Itô's formula for time-dependent functions is $dU_s = (\partial_s u + \mathcal{L}u)(s,X_s)ds + \text{martingale term}$.

Applying the product rule $d(\Gamma_s U_s) = \Gamma_s dU_s + U_s d\Gamma_s$, we get:
$d(\Gamma_s U_s) = \Gamma_s \left( (\partial_s u + \mathcal{L}u)(s,X_s) ds + dM_s \right) - \Gamma_s U_s V(s,X_s) ds$
$= \Gamma_s \left( \partial_s u + \mathcal{L}u - V u \right)(s,X_s) ds + \Gamma_s dM_s$
where $dM_s$ represents the stochastic integral (martingale) part.

Since $u$ solves the PDE, we have $\partial_s u + \mathcal{L}u - Vu = -f$. Substituting this into the expression for $d(\Gamma_s U_s)$ yields:
$d(\Gamma_s U_s) = -\Gamma_s f(s,X_s) ds + \Gamma_s dM_s$

Now we can find the differential of our full process $Y_s$:
$dY_s = d(\Gamma_s U_s) + d\left(\int_t^s \Gamma_r f(r,X_r) dr\right) = \left(-\Gamma_s f(s,X_s) ds + \Gamma_s dM_s\right) + \left(\Gamma_s f(s,X_s) ds\right) = \Gamma_s dM_s$

The drift term, composed of contributions from the PDE and the compensating integral, has perfectly cancelled out. The process $Y_s$ is therefore a [local martingale](@entry_id:203733). Under suitable boundedness conditions on the coefficients and the solution $u$, it can be shown to be a true martingale.

The [martingale property](@entry_id:261270) implies that $\mathbb{E}_{t,x}[Y_T] = Y_t$. Let's evaluate $Y$ at the start and end times:
- At time $t$: $\Gamma_t=1$, $U_t=u(t,x)$, and the integral is zero. Thus, $Y_t = u(t,x)$.
- At time $T$: $U_T = u(T,X_T) = g(X_T)$. So, $Y_T = \exp\left(-\int_t^T V(s,X_s)ds\right) g(X_T) + \int_t^T \exp\left(-\int_t^s V(r,X_r)dr\right) f(s,X_s)ds$.

Equating $\mathbb{E}_{t,x}[Y_T] = Y_t$ gives us exactly the Feynman-Kac formula.

### Probabilistic Interpretation and Operator Properties

The Feynman-Kac formula is more than a computational trick; it provides deep insight into the structure of the PDE.

#### The Potential as a Killing Rate

The term $V(t,x)$ in the PDE, which appears as a zero-order operator, has a clear probabilistic meaning. Consider the case where $V \ge 0$. The factor $\exp\left(-\int_t^s V(r,X_r)dr\right)$ can be interpreted as the probability that the path "survives" up to time $s$ without being "killed" by a random mechanism whose instantaneous rate of occurrence at time $r$ is $V(r,X_r)$ [@problem_id:3001147].

For example, if we set $f=0$ and $g=1$, the solution becomes:
$u(t,x) = \mathbb{E}_{t,x}\left[\exp\left(-\int_t^T V(s,X_s)ds\right)\right]$
This is precisely the expected [survival probability](@entry_id:137919) of the process up to time $T$. If $V \equiv c > 0$ is a constant, this simplifies to $u(t,x) = e^{-c(T-t)}$, the solution to $\partial_t u = -cu$. The formula correctly discounts the terminal payoff $g(X_T)$ by the probability that the path survives long enough to receive it. When $V \equiv 0$, the exponential factors become 1, and the representation reduces to the solution of the standard Kolmogorov backward equation without killing [@problem_id:3001147]:
$u(t,x) = \mathbb{E}_{t,x}\left[g(X_T) + \int_t^T f(s,X_s) ds\right]$

#### The Feynman-Kac Semigroup

The Feynman-Kac representation allows us to define a new family of operators, $(T_t)_{t \ge 0}$, known as the **Feynman-Kac [semigroup](@entry_id:153860)**. For a time-[homogeneous system](@entry_id:150411) where $V(x)$ does not depend on time, it acts on bounded measurable functions $g$ as:
$$(T_t g)(x) = \mathbb{E}_x\left[\exp\left(-\int_0^t V(X_s)ds\right) g(X_t)\right]$$
This [semigroup](@entry_id:153860) describes the evolution of an observable $g$ for a process that is subject to killing. It has several important properties that follow directly from the [properties of expectation](@entry_id:170671) [@problem_id:3001106]:
- **Positivity-Preserving**: If $g \ge 0$, then $(T_t g)(x) \ge 0$ for all $t,x$. This is because the exponential term and $g(X_t)$ are both non-negative.
- **Contractivity**: If the potential is non-negative ($V \ge 0$), then the semigroup is a contraction on the space of bounded functions equipped with the supremum norm, i.e., $\|T_t g\|_\infty \le \|g\|_\infty$. This is because the killing mechanism can only reduce the expected value.
- **Growth Bound**: If the potential is bounded from below, $V(x) \ge -K$ for some $K \ge 0$, the [semigroup](@entry_id:153860) norm is bounded by an exponential: $\|T_t g\|_\infty \le e^{Kt} \|g\|_\infty$. A negative potential corresponds to "creation" or "branching," which can cause [exponential growth](@entry_id:141869) in the expected value.

The generator of this semigroup, which we can find by taking the derivative at $t=0$, is precisely the Schrödinger-type operator $\mathcal{L} - V$. The function $u(t,x) = (T_t g)(x)$ thus solves the PDE $\partial_t u = (\mathcal{L}-V)u$ with initial condition $u(0,x)=g(x)$ [@problem_id:3001150].

### Extensions and Foundations

The framework presented so far can be extended and requires a rigorous foundation to be complete.

#### Boundary Value Problems

The Feynman-Kac formula can be adapted to solve elliptic and parabolic PDEs on a bounded domain $D \subset \mathbb{R}^d$ with specified boundary conditions. Consider the stationary (elliptic) Dirichlet problem:
$$\mathcal{L}u(x) - c(x)u(x) = -f(x), \quad x \in D$$
$$u(x) = g(x), \quad x \in \partial D$$

To find the solution, we consider the process $X_s$ starting at $x \in D$ and run it until it first hits the boundary $\partial D$. Let this random time be the **[exit time](@entry_id:190603)**, $\tau_D = \inf\{ s \ge 0 : X_s \notin D \}$. The process is "killed" at the boundary. The solution $u(x)$ is then given by a similar representation, but with the fixed time $T$ replaced by the random stopping time $\tau_D$ [@problem_id:3001127]:

$$u(x) = \mathbb{E}_{x} \left[ \exp\left(-\int_{0}^{\tau_D} c(X_s)ds\right) g(X_{\tau_D}) + \int_{0}^{\tau_D} \exp\left(-\int_{0}^{s} c(X_r)dr\right) f(X_s)ds \right]$$

The terminal payoff $g$ is received at the boundary point $X_{\tau_D}$, and all [discounting](@entry_id:139170) and sources are integrated only up to the [exit time](@entry_id:190603) $\tau_D$.

#### Rigorous Foundations and Viscosity Solutions

The derivation and validity of the Feynman-Kac representation rely on a set of technical conditions. For the existence of a unique [strong solution](@entry_id:198344) to the SDE, from which a classical ($C^{1,2}$) solution to the PDE can be derived, standard conditions include local Lipschitz continuity and linear growth bounds on the coefficients $b$ and $\sigma$ [@problem_id:3001156].

However, the theory is far more robust. A cornerstone of modern SDE theory, established by Stroock and Varadhan, shows that a unique [weak solution](@entry_id:146017) ([uniqueness in law](@entry_id:186911)) exists under much weaker assumptions: that the coefficients $b$ and $\sigma$ are merely bounded and measurable, provided the [diffusion matrix](@entry_id:182965) $a(x)=\sigma(x)\sigma(x)^\top$ is uniformly elliptic [@problem_id:3001156].

Under these weak conditions, the PDE coefficients are not continuous, and a classical $C^{1,2}$ solution may not exist. Nonetheless, the probabilistic formula for $u(t,x)$ remains well-defined. The remarkable fact is that this function $u$ is the unique **[viscosity solution](@entry_id:198358)** to the PDE [@problem_id:3001104]. A [viscosity solution](@entry_id:198358) is a continuous function that satisfies the PDE in a weaker sense: wherever a smooth function "touches" it from above or below, that [smooth function](@entry_id:158037) must satisfy a [differential inequality](@entry_id:137452) related to the PDE. Proving this involves a sophisticated three-part argument:
1.  Showing the function $u$ defined by the formula is continuous, which relies on deep regularity results for the SDE's transition density (like Aronson estimates).
2.  Verifying that $u$ satisfies the viscosity sub- and super-solution inequalities via a localized martingale argument with smooth [test functions](@entry_id:166589).
3.  Establishing uniqueness via a [comparison principle](@entry_id:165563) for [viscosity solutions](@entry_id:177596), a hallmark of the Crandall-Ishii-Lions theory.

This modern perspective guarantees that the Feynman-Kac representation provides the unique, physically meaningful solution to the PDE even when the coefficients lack the smoothness required by classical theory, cementing its role as a fundamental tool in the analysis of [stochastic systems](@entry_id:187663) and differential equations.