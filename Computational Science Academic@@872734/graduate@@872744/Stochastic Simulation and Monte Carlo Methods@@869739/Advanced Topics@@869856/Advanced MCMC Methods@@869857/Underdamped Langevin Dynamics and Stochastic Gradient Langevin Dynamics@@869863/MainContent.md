## Introduction
In fields ranging from statistical physics to machine learning, a fundamental challenge is to explore and sample from complex, high-dimensional probability distributions. Traditional methods can be slow or become trapped, especially when dealing with massive datasets or intricate energy landscapes. Underdamped Langevin dynamics, which model the motion of a particle with inertia, offer a powerful and physically-grounded alternative for more efficient exploration. However, harnessing their full potential requires a deep understanding of their unique mathematical properties and a careful adaptation to the realities of modern computation, where exact information is often unavailable. This article bridges this gap by providing a comprehensive overview of underdamped Langevin dynamics and their stochastic gradient extensions, offering a graduate-level understanding of both the theory and its practical implementation.

In **Principles and Mechanisms**, we will derive the governing equations from first principles, unraveling the crucial concepts of [hypoellipticity](@entry_id:185488) and [hypocoercivity](@entry_id:193689), and see how these dynamics are adapted for stochastic gradients in algorithms like SGHMC. Next, **Applications and Interdisciplinary Connections** will showcase the versatility of these methods in [molecular dynamics](@entry_id:147283) and machine learning, discussing numerical integrators, advanced modeling techniques, and [variance reduction](@entry_id:145496). Finally, **Hands-On Practices** will solidify your understanding through guided problems that connect the theory to computational practice, focusing on equilibrium properties, [numerical stability](@entry_id:146550), and sampler optimization.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms governing underdamped Langevin dynamics and their application in stochastic gradient methods. We will begin by formally deriving the governing stochastic differential equation (SDE) from physical first principles. Subsequently, we will explore the intricate mathematical properties of these dynamics, including the concepts of [hypoellipticity](@entry_id:185488) and [hypocoercivity](@entry_id:193689), which are essential for understanding their behavior and convergence. Finally, we will extend these principles to the practical realm of large-scale computation, where exact gradients are replaced by stochastic estimates, leading to the development of algorithms like Stochastic Gradient Hamiltonian Monte Carlo (SGHMC).

### The Underdamped Langevin Stochastic Differential Equation

The underdamped Langevin equation describes the motion of a particle with inertia within a potential field, while it is in contact with a [heat bath](@entry_id:137040). This contact gives rise to two competing effects: a dissipative **friction** force that slows the particle down and a **stochastic force** from random thermal fluctuations that energizes it. The balance between these two forces is what allows the system to eventually reach thermal equilibrium.

Let the state of a particle of mass $m$ be described by its position $x_t \in \mathbb{R}^d$ and velocity $v_t \in \mathbb{R}^d$. The evolution of its state is governed by a system of two coupled SDEs. The first is the simple kinematic relation:
$$
\mathrm{d}x_t = v_t\,\mathrm{d}t
$$
The second equation comes from Newton's second law, $m\,\mathrm{d}v_t = F_{\text{total}}\,\mathrm{d}t$, where the total force is the sum of three components:
1.  A **conservative force** derived from a smooth [potential energy function](@entry_id:166231) $U(x)$, given by $F_{\text{cons}} = -\nabla U(x_t)$.
2.  A linear **viscous friction** or drag force, which opposes the particle's motion, $F_{\text{fric}} = -\gamma v_t$, where $\gamma > 0$ is the friction coefficient.
3.  A **stochastic force**, $F_{\text{rand}}$, representing the random collisions with the particles of the [heat bath](@entry_id:137040). This is modeled as Gaussian [white noise](@entry_id:145248).

Combining these forces, we get the equation for the change in velocity. The crucial insight is that the friction and the stochastic force are not independent. They are two manifestations of the same underlying physical interaction with the heat bath. The **Fluctuation-Dissipation Theorem** provides the precise mathematical relationship between them. This theorem ensures that for any initial condition, the long-term statistical properties of the particle's state will converge to the correct thermal [equilibrium distribution](@entry_id:263943), known as the **Gibbs-Boltzmann distribution**. For a system at inverse temperature $\beta = (k_B T)^{-1}$, where $k_B$ is the Boltzmann constant and $T$ is the absolute temperature, the [equilibrium probability](@entry_id:187870) density is proportional to $\exp(-\beta H(x,v))$, where $H(x,v) = U(x) + \frac{1}{2}m\|v\|^2$ is the system's Hamiltonian (total energy).

To satisfy this condition, the magnitude of the stochastic force must be precisely calibrated against the friction coefficient $\gamma$ and the temperature $\beta^{-1}$. This leads to the canonical form of the underdamped Langevin SDE [@problem_id:3359208]:
$$
\begin{aligned}
\mathrm{d}x_t = v_t\,\mathrm{d}t \\
m\,\mathrm{d}v_t = -\nabla U(x_t)\,\mathrm{d}t - \gamma v_t\,\mathrm{d}t + \sqrt{2\gamma m \beta^{-1}}\,\mathrm{d}W_t
\end{aligned}
$$
where $W_t$ is a $d$-dimensional standard Wiener process. Note the presence of the mass $m$ in the friction and noise terms, which is often how it is expressed in physics. However, in many applications, particularly in sampling, it is convenient to work with a "unit mass" formulation. This can be achieved by a simple [change of variables](@entry_id:141386). By defining a rescaled velocity variable $u_t = \sqrt{m} v_t$, the kinetic energy term becomes $\frac{1}{2}\|u_t\|^2$, and the SDE system transforms into a form where the mass no longer explicitly appears in the [invariant density](@entry_id:203392) [@problem_id:3359268]. Dividing the velocity equation by $m$ then yields the commonly used form (often with redefined parameters):
$$
\begin{aligned}
\mathrm{d}x_t = v_t\,\mathrm{d}t \\
\mathrm{d}v_t = -\nabla U(x_t)\,\mathrm{d}t - \gamma v_t\,\mathrm{d}t + \sqrt{2\gamma \beta^{-1}}\,\mathrm{d}W_t
\end{aligned}
$$
Henceforth, we will adopt this unit-mass convention, where the potential $U(x)$ and inverse temperature $\beta$ are understood to have absorbed the [mass scaling](@entry_id:177780). In this framework, the [invariant density](@entry_id:203392) for the pair $(x_t, v_t)$ is $\pi(x,v) \propto \exp(-\beta(U(x) + \frac{1}{2}\|v\|^2))$.

### The Geometry of Dynamics: Degeneracy and Hypoellipticity

A careful inspection of the underdamped Langevin SDE reveals a critical structural feature: the stochastic driving term $\mathrm{d}W_t$ only appears in the equation for the velocity $v_t$. The position $x_t$ is not directly subjected to noise; its evolution is determined entirely by the (now stochastic) velocity. This means the diffusion is **degenerate** [@problem_id:3359213]. If we write the SDE for the full [state vector](@entry_id:154607) $Z_t = (x_t, v_t)$ in the form $\mathrm{d}Z_t = b(Z_t)\,\mathrm{d}t + \sigma\,\mathrm{d}W_t$, the [diffusion matrix](@entry_id:182965) $\sigma$ will have a block of zeros corresponding to the position components, making the covariance matrix $\sigma\sigma^\top$ singular.

This degeneracy has profound consequences for the qualitative behavior of the trajectories. Since $\mathrm{d}x_t = v_t\,\mathrm{d}t$, the position path $x_t$ is the time integral of the velocity path $v_t$. While $v_t$ is a rough, non-differentiable Itô process, its integral $x_t$ is smoother—it is continuously differentiable (its derivative being $v_t$). This contrasts sharply with the **overdamped Langevin dynamics**, obtained in the high-friction limit where inertia is negligible, described by $\mathrm{d}x_t = -\nabla U(x_t)\,\mathrm{d}t + \sqrt{2\beta^{-1}}\,\mathrm{d}W_t$. In the [overdamped](@entry_id:267343) case, the noise acts directly on position, and the resulting paths are rough and non-differentiable. The short-time behavior reflects this difference: for underdamped dynamics, [mean-squared displacement](@entry_id:159665) scales like $\mathbb{E}[\|x_t - x_0\|^2] \propto t^2$ (ballistic motion), whereas for [overdamped](@entry_id:267343) dynamics, it scales like $\mathbb{E}[\|x_t - x_0\|^2] \propto t$ (diffusive motion) [@problem_id:3359213].

A natural question arises from this degeneracy: if noise only directly "kicks" the velocity, how can the system explore the entire position space to reach the target equilibrium? The answer lies in the concept of **[hypoellipticity](@entry_id:185488)**. The randomness injected into the velocity is transferred to the position through the deterministic drift coupling $\mathrm{d}x_t = v_t\,\mathrm{d}t$. Even though the noise is degenerate, it eventually propagates throughout the entire state space.

This mechanism can be made precise through **Hörmander's bracket condition** [@problem_id:3359214]. The dynamics can be represented by a set of vector fields: a drift field $X_0$ and a set of diffusion fields $\{X_i\}$ corresponding to the directions of the noise. For underdamped Langevin dynamics, the drift field is $X_0 = v \cdot \nabla_x - (\gamma v + \nabla U(x)) \cdot \nabla_v$, and the diffusion fields are simply the basis vectors of the [velocity space](@entry_id:181216), $X_i = \partial_{v_i}$. These diffusion fields initially only span the velocity subspace. However, by computing the **Lie bracket** $[X_0, X_i] = X_0 X_i - X_i X_0$, we generate new [vector fields](@entry_id:161384). A direct calculation reveals that $[X_0, X_i] = \gamma\partial_{v_i} - \partial_{x_i}$. This new vector field has a component in the position direction, $\partial_{x_i}$. By taking linear combinations of the original diffusion fields $\{\partial_{v_i}\}$ and these new bracket-generated fields $\{\gamma\partial_{v_i} - \partial_{x_i}\}$, we can construct a basis for the entire position-velocity [tangent space](@entry_id:141028). Since this can be done at every point in the state space (provided $U$ is sufficiently smooth, e.g., $C^2$), Hörmander's condition is satisfied. The primary consequence of this [hypoellipticity](@entry_id:185488) is that the process admits a smooth transition probability density for any positive time $t>0$. That is, even starting from a fixed point, the probability distribution of the particle's state spreads out smoothly across the entire phase space.

### The Evolution of Probability: Fokker-Planck Equation and Invariant Measures

While the SDE describes the evolution of individual particle trajectories, the **Kramers-Fokker-Planck equation** describes the evolution of the probability density $p(x, v, t)$ of an ensemble of such particles. It is the forward Kolmogorov equation for the process and can be derived directly from the SDE [@problem_id:3359248]. For the unit-mass underdamped Langevin SDE, the equation is:
$$
\frac{\partial p}{\partial t} = -\nabla_x \cdot (v p) + \nabla_v \cdot \Big( (\gamma v + \nabla U(x)) p \Big) + \gamma\beta^{-1} \Delta_v p
$$
Each term in this partial differential equation has a clear physical interpretation.
-   The term $-\nabla_x \cdot (v p)$ represents the transport of probability in [position space](@entry_id:148397) due to velocity. It is a pure advection or drift term.
-   The term $\nabla_v \cdot ((\gamma v + \nabla U(x)) p)$ represents the transport of probability in [velocity space](@entry_id:181216) due to the deterministic forces of friction and the [potential gradient](@entry_id:261486).
-   The term $\gamma\beta^{-1} \Delta_v p$ represents the diffusion of probability in [velocity space](@entry_id:181216) due to the random thermal force. The operator $\Delta_v$ is the Laplacian with respect to the velocity coordinates.

The degeneracy of the noise is again apparent here: there is no diffusion term involving the position Laplacian $\Delta_x$.

The **[invariant measure](@entry_id:158370)** $\pi(x,v)$ is a probability density that is a stationary solution to the Fokker-Planck equation, i.e., $\partial \pi / \partial t = 0$. As stated earlier, the physics of the system dictates that this must be the Gibbs-Boltzmann distribution:
$$
\pi(x,v) = Z^{-1} \exp\left(-\beta\left(U(x) + \frac{1}{2}\|v\|^2\right)\right)
$$
where $Z$ is a normalization constant ensuring the total probability is one. One can verify by direct substitution that this density indeed makes the right-hand side of the Fokker-Planck equation zero, confirming that the [fluctuation-dissipation relation](@entry_id:142742) embedded in the SDE's noise coefficient correctly balances the system.

### Convergence to Equilibrium: The Role of Hypocoercivity

Knowing that the system has a unique [stationary distribution](@entry_id:142542) is one thing; understanding how fast it converges to it is another. This is crucial for practical sampling applications. The [rate of convergence](@entry_id:146534) is governed by the spectral properties of the process's **infinitesimal generator**, $L$ [@problem_id:3359258]. For a test function $f(x,v)$, the generator is given by:
$$
L f(x,v) = v\cdot \nabla_{x} f - \big(\nabla U(x)+\gamma v\big)\cdot \nabla_{v} f + \gamma \beta^{-1}\Delta_{v} f
$$
The generator can be decomposed into a symmetric (dissipative) part $\mathcal{S}$ and an antisymmetric (conservative) part $\mathcal{A}$. The symmetric part $\mathcal{S} = \gamma\beta^{-1}\Delta_{v} f - \gamma v\cdot \nabla_{v} f$ is an Ornstein-Uhlenbeck generator that acts only on the velocity variables. The antisymmetric part $\mathcal{A} = v\cdot \nabla_{x} f - \nabla U(x)\cdot \nabla_{v} f$ corresponds to the deterministic Hamiltonian flow.

Exponential convergence to the invariant measure $\pi$ is typically guaranteed if the generator has a **spectral gap**, a condition known as coercivity. This means that the dissipation rate, measured by $-\int (Lf)f \, \mathrm{d}\pi$, is strictly positive for all non-constant functions $f$. However, for the underdamped Langevin generator, the dissipation comes entirely from the symmetric part $\mathcal{S}$. If we take any function $f(x)$ that depends only on position, then $\nabla_v f=0$, and the dissipation is zero. This means the operator is not coercive; it fails to dissipate functions that lie in the kernel of the velocity derivative operator.

Despite this lack of coercivity, the system does converge exponentially to equilibrium (under suitable conditions on the potential $U$, such as [strong convexity](@entry_id:637898)). This phenomenon is known as **[hypocoercivity](@entry_id:193689)** [@problem_id:3359267]. The mechanism is precisely the interaction between the non-dissipative transport part $\mathcal{A}$ and the dissipative part $\mathcal{S}$. The Hamiltonian flow $\mathcal{A}$ constantly mixes position and velocity coordinates. Any purely position-dependent fluctuation is quickly turned by the transport term $v \cdot \nabla_x$ into one that also has velocity dependence, at which point the [dissipative operator](@entry_id:262598) $\mathcal{S}$ can act on it and damp it out. The non-commutativity of $\mathcal{A}$ and $\mathcal{S}$ is the mathematical signature of this coupling, which effectively spreads the dissipation from the velocity subspace to the entire phase space. Proofs of [hypocoercivity](@entry_id:193689) often involve constructing a modified Lyapunov functional that includes cross-terms between position and velocity, which can be shown to decay exponentially, thereby proving [exponential convergence](@entry_id:142080) in an equivalent norm.

### Stochastic Gradient Dynamics

In many modern applications, particularly in machine learning and Bayesian inference with large datasets, the [potential function](@entry_id:268662) $U(\theta)$ (where the parameters $\theta$ take the role of position $x$) is a sum over a vast number of data points, $U(\theta) = \sum_{i=1}^N U_i(\theta)$. Computing the full gradient $\nabla U(\theta)$ at each step of a simulation becomes prohibitively expensive. This motivates the use of **stochastic gradients**, where the gradient is estimated using only a small, random subset (a minibatch) of the data.

#### Overdamped Case: SGLD

The most direct application of this idea is to the overdamped Langevin equation, leading to the **Stochastic Gradient Langevin Dynamics (SGLD)** algorithm [@problem_id:3359221]. A discrete-time step of the algorithm takes the form:
$$
\theta_{k+1} = \theta_k - \eta_k \widehat{\nabla U}(\theta_k) + \sqrt{2\eta_k \beta^{-1}}\,\xi_k
$$
where $\eta_k$ is the step size, $\xi_k \sim \mathcal{N}(0, I)$ is standard Gaussian noise, and $\widehat{\nabla U}(\theta_k)$ is the stochastic gradient estimator. For this algorithm to correctly approximate the target distribution $\pi(\theta) \propto \exp(-\beta U(\theta))$, the stochastic gradient must satisfy two key properties:
1.  **Conditional Unbiasedness**: $\mathbb{E}[\widehat{\nabla U}(\theta_k) \,|\, \theta_k] = \nabla U(\theta_k)$. This ensures that, on average, the drift of the algorithm points in the correct direction. Any systematic bias would lead to convergence to the wrong distribution.
2.  **Controlled Variance**: The variance of the gradient estimator, $\mathbb{E}[\|\widehat{\nabla U}(\theta_k) - \nabla U(\theta_k)\|^2 \,|\, \theta_k]$, must be bounded. This ensures that the noise introduced by the [gradient estimation](@entry_id:164549) does not overwhelm the dynamics.

Under these conditions, and with a properly decaying step size schedule (e.g., $\sum \eta_k = \infty$, $\sum \eta_k^2  \infty$), SGLD can be shown to converge to the [target distribution](@entry_id:634522).

#### Underdamped Case: SGHMC

The same principle can be applied to underdamped Langevin dynamics, an approach often called **Stochastic Gradient Hamiltonian Monte Carlo (SGHMC)** [@problem_id:3359216]. The continuous-time dynamics are modified by replacing the true gradient with the stochastic estimator. This introduces an additional source of noise into the velocity equation. The total noise now comprises the intentionally injected thermal noise and the noise from the [gradient estimation](@entry_id:164549).

Let the covariance of the [gradient noise](@entry_id:165895) be $\mathbb{E}[(\widehat{\nabla U} - \nabla U)(\widehat{\nabla U} - \nabla U)^\top] = B(x)$. To preserve the Gibbs-Boltzmann distribution as the [invariant measure](@entry_id:158370) of the [continuous-time process](@entry_id:274437), the fluctuation-dissipation theorem must be upheld for the *total* system, which now includes this extra [gradient noise](@entry_id:165895). This requires a re-calibration [@problem_id:3359233]. Let the underdamped SDE with a user-chosen friction matrix $\Gamma$ and injected noise covariance $\Sigma\Sigma^\top$ be:
$$
\mathrm{d}v_t = -\widehat{\nabla U}(x_t)\,\mathrm{d}t - \Gamma v_t\,\mathrm{d}t + \Sigma\,\mathrm{d}W_t
$$
This is equivalent to a process with drift $-\nabla U(x_t) - \Gamma v_t$ and a total noise process whose [quadratic variation](@entry_id:140680) is $(\Sigma\Sigma^\top + B(x_t)) \mathrm{d}t$. For the system to have the target invariant measure, the [fluctuation-dissipation relation](@entry_id:142742) dictates that the total diffusion must balance the friction term $\Gamma$. Assuming $\Gamma$ is symmetric, the condition is $2\Gamma = \beta(\Sigma\Sigma^\top + B(x_t))$. This leads to the crucial insight for SGHMC: the injected noise must be chosen as
$$
\Sigma\Sigma^\top = \frac{2}{\beta}\Gamma - B(x_t)
$$
This shows that the injected noise $\Sigma$ must be *reduced* to compensate for the noise $B(x_t)$ coming from the stochastic gradients. The friction matrix $\Gamma$ now plays a dual role: it provides physical dissipation and also sets the scale of the total noise that the system can tolerate while remaining at the correct temperature.

This approach contrasts fundamentally with classical Hamiltonian Monte Carlo (HMC). HMC propagates trajectories using deterministic, time-reversible Hamiltonian dynamics and relies on a Metropolis-Hastings acceptance step to correct for [discretization errors](@entry_id:748522) and maintain detailed balance. SGHMC, by introducing friction and noise, creates a non-[reversible process](@entry_id:144176) that does not satisfy detailed balance. Instead of an acceptance test, it relies on the fluctuation-dissipation principle to ensure that the process has the correct stationary distribution in the continuous-time limit [@problem_id:3359216]. While this avoids costly rejections, especially in high dimensions, it introduces its own challenge: the bias from time-discretization, which is typically controlled by using a sufficiently small step size.