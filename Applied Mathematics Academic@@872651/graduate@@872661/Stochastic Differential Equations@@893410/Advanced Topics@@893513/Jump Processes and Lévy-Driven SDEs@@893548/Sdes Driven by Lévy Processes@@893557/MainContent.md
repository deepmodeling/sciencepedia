## Introduction
Classical [stochastic differential equations](@entry_id:146618) driven by Brownian motion have been immensely successful in modeling systems subject to continuous, random fluctuations. However, many phenomena in finance, physics, and insurance are characterized by sudden, sharp movements—market crashes, physical impacts, or large insurance claims—that continuous models cannot capture. This gap is filled by extending the framework to SDEs driven by Lévy processes, which naturally incorporate discontinuous jumps. Understanding these advanced models is crucial for creating more realistic and robust descriptions of complex systems.

This article provides a comprehensive theoretical and practical guide to SDEs driven by Lévy processes. It bridges the gap between foundational probability theory and advanced applications by systematically building up the necessary mathematical machinery. Over the course of three chapters, you will gain a deep understanding of this powerful modeling tool.

The journey begins with **Principles and Mechanisms**, where we will formally define jump-diffusion SDEs and dissect their structure. We will explore the crucial Lévy-Itô decomposition, the construction of stochastic integrals with respect to [jump processes](@entry_id:180953), and the key theoretical results, such as well-posedness and the Girsanov theorem, that form the bedrock of the subject.

Next, in **Applications and Interdisciplinary Connections**, we will see this theory in action. We will investigate how introducing jumps into classical models like the Ornstein-Uhlenbeck process transforms their behavior and expands their applicability. This chapter highlights the deep connections between Lévy processes and fields as diverse as [mathematical finance](@entry_id:187074), [actuarial science](@entry_id:275028), [ergodic theory](@entry_id:158596), and the analysis of partial differential equations.

Finally, the **Hands-On Practices** section provides an opportunity to solidify your understanding through a series of guided problems. By working through these exercises, you will develop practical skills in applying the core concepts, from deriving characteristic triplets to using the [infinitesimal generator](@entry_id:270424), preparing you to use these models in your own research.

## Principles and Mechanisms

The extension of [stochastic differential equations](@entry_id:146618) from continuous diffusions to processes incorporating jumps represents a significant leap in modeling capabilities, allowing for the representation of sudden, discontinuous events. This chapter delves into the fundamental principles and mathematical mechanisms that govern [stochastic differential equations](@entry_id:146618) driven by Lévy processes. We will formally define these equations, explore their construction from constituent stochastic integrals, examine key theoretical results such as well-posedness and [change of measure](@entry_id:157887), and investigate important classes of processes that provide both theoretical insight and practical tractability.

### The Structure of Jump-Diffusion SDEs

A general [stochastic differential equation](@entry_id:140379) (SDE) in $\mathbb{R}^n$ that incorporates both continuous and discontinuous sources of randomness is often referred to as a **jump-diffusion**. Its dynamics are driven by a combination of a deterministic drift, a Brownian motion, and a pure-[jump process](@entry_id:201473). The standard representation of such an SDE is given in differential form as:

$$
dX_t = b(X_{t-}) \, dt + \sigma(X_{t-}) \, dW_t + \int_{\mathbb{R}^d} \gamma(X_{t-}, z) \, \tilde{N}(dt, dz)
$$

Here, $X_t$ is the state process in $\mathbb{R}^n$, $W_t$ is a standard $m$-dimensional Brownian motion, and $\tilde{N}(dt, dz)$ is a compensated Poisson random measure on $\mathbb{R}_+ \times \mathbb{R}^d$. This measure is defined as $\tilde{N}(dt, dz) = N(dt, dz) - \nu(dz) \, dt$, where $N(dt, dz)$ is a Poisson random measure that counts the number of jumps occurring at time $t$ with a size in the set $dz$, and $\nu(dz)$ is a **Lévy measure** on $\mathbb{R}^d$. The Lévy measure governs the expected rate and size distribution of the jumps. The functions $b: \mathbb{R}^n \to \mathbb{R}^n$, $\sigma: \mathbb{R}^n \to \mathbb{R}^{n \times m}$, and $\gamma: \mathbb{R}^n \times \mathbb{R}^d \to \mathbb{R}^n$ are the drift vector, [diffusion matrix](@entry_id:182965), and jump coefficient, respectively.

While the [differential form](@entry_id:174025) is a convenient shorthand, the rigorous definition is given by the corresponding stochastic integral equation [@problem_id:2981529]:

$$
X_t = X_0 + \int_0^t b(X_{s-}) \, ds + \int_0^t \sigma(X_{s-}) \, dW_s + \int_0^t \int_{\mathbb{R}^d} \gamma(X_{s-}, z) \, \tilde{N}(ds, dz)
$$

Several features of this definition are crucial. First, the [sample paths](@entry_id:184367) of the solution process $X_t$ are not continuous. The presence of the jump term implies that $X_t$ will be a **càdlàg** process, meaning its paths are right-continuous with left limits existing everywhere. The natural space for such paths is the space $D([0,T]; \mathbb{R}^n)$ of càdlàg functions, in contrast to the space $C([0,T]; \mathbb{R}^n)$ of continuous functions which serves as the path space for standard diffusions driven only by Brownian motion [@problem_id:2994516]. The space $D$ is typically endowed with the **Skorokhod $J_1$ topology**, which is weaker than the uniform topology and gracefully handles [sequences of functions](@entry_id:145607) with jumps at slightly varying times.

Second, the coefficients of the integrands, $b$, $\sigma$, and $\gamma$, are evaluated at $X_{s-}$, which denotes the left-limit of the process, $X_{s-} = \lim_{u \uparrow s} X_u$. This is not a trivial notational choice. Stochastic integrals are defined for integrands that are **[predictable processes](@entry_id:262945)**. A process is predictable if its value at time $t$ is determined by information available strictly before time $t$. While a general càdlàg process is merely adapted, its left-limit process $X_{t-}$ is left-continuous and therefore predictable. Using $X_{s-}$ ensures that the integrands are predictable, making the stochastic integrals well-defined. It reflects the intuitive notion that the state of the system just before a potential jump determines the dynamics at that instant.

A solution $X_t$ to this SDE is a **[semimartingale](@entry_id:188438)**, which admits a [canonical decomposition](@entry_id:634116). The term $\int_0^t b(X_{s-}) \, ds$ constitutes a process of finite variation. The remaining two integral terms together form a [local martingale](@entry_id:203733), which can be further decomposed into its continuous and purely discontinuous parts:
*   **Continuous [local martingale](@entry_id:203733) part**: $M_t^c = \int_0^t \sigma(X_{s-}) \, dW_s$.
*   **Purely discontinuous [local martingale](@entry_id:203733) part**: $M_t^d = \int_0^t \int_{\mathbb{R}^d} \gamma(X_{s-}, z) \, \tilde{N}(ds, dz)$.

The compensation term $-\nu(dz)dt$ in the definition of $\tilde{N}$ is what ensures that the jump integral, under suitable [integrability conditions](@entry_id:158502) on $\gamma$, is a [local martingale](@entry_id:203733) rather than a process with a systematic drift from the jumps.

### Construction of Stochastic Integrals with Respect to Lévy Processes

The SDE is fundamentally a statement about sums of infinitesimal increments, which are defined via stochastic integrals. To understand the SDE, one must first understand how to integrate a [predictable process](@entry_id:274260) with respect to a general Lévy process. Let $L_t$ be a Lévy process with [characteristic triplet](@entry_id:635937) $(b, c, \nu)$ relative to a truncation function, for instance $h(x) = x \mathbf{1}_{|x|\le 1}$. Its Lévy-Itô decomposition is [@problem_id:2995475]:

$$
L_t = bt + \sqrt{c} W_t + \int_0^t \int_{|x| \le 1} x \, \tilde{N}(ds, dx) + \int_0^t \int_{|x| > 1} x \, N(ds, dx)
$$

The stochastic integral of a [predictable process](@entry_id:274260) $\sigma_t$ with respect to $L_t$ is defined by linearity, integrating $\sigma_t$ with respect to each component of the decomposition:

$$
\int_0^t \sigma_s \, dL_s = \int_0^t \sigma_s b \, ds + \int_0^t \sigma_s \sqrt{c} \, dW_s + \int_0^t \int_{|x| \le 1} \sigma_s x \, \tilde{N}(ds, dx) + \int_0^t \int_{|x| > 1} \sigma_s x \, N(ds, dx)
$$

Each integral in this decomposition must be well-defined. This requires specific [integrability conditions](@entry_id:158502) on $\sigma_t$ for any finite time horizon $T>0$:

1.  **Drift Part**: $\int_0^t \sigma_s b \, ds$. This is a standard Lebesgue integral. For it to define a process of finite variation, $\sigma_t$ must be locally integrable: $\int_0^T |\sigma_s| \, ds  \infty$ almost surely.

2.  **Brownian Part**: $\int_0^t \sigma_s \sqrt{c} \, dW_s$. This is an Itô integral. For it to define a [continuous local martingale](@entry_id:188921), $\sigma_t$ must be locally square-integrable with respect to time: $\int_0^T \sigma_s^2 \, ds  \infty$ [almost surely](@entry_id:262518).

3.  **Small-Jump Part**: $\int_0^t \int_{|x| \le 1} \sigma_s x \, \tilde{N}(ds, dx)$. This is an integral with respect to a compensated random measure. For it to be a square-integrable martingale, the integrand $\sigma_s x$ must be locally square-integrable with respect to the intensity measure $\nu(dx)ds$: $\int_0^T \int_{|x| \le 1} (\sigma_s x)^2 \, \nu(dx) \, ds  \infty$ almost surely.

4.  **Large-Jump Part**: $\int_0^t \int_{|x|  1} \sigma_s x \, N(ds, dx)$. Since the Lévy measure satisfies $\nu(\{x: |x|1\})  \infty$, this is an integral with respect to a finite-activity [jump process](@entry_id:201473) (a compound Poisson process). For this sum of jumps to result in a process of finite variation, we require the integrand to be locally integrable with respect to the intensity measure: $\int_0^T \int_{|x|  1} |\sigma_s x| \, \nu(dx) \, ds  \infty$ almost surely.

These conditions highlight a fundamental dichotomy: martingale components (Brownian, compensated small jumps) typically require $L^2$ conditions, while finite variation components (drift, large jumps) typically require $L^1$ conditions.

### Canonical Representation of SDEs with Jumps

SDEs driven by Lévy processes are often written in a compact form, such as $dX_t = f(X_{t-}) dt + G(X_{t-}) dL_t$. To analyze or simulate such an equation, one must expand it into its canonical form, making the different sources of randomness explicit. This involves substituting the Lévy-Itô decomposition of $L_t$. A subtlety arises because the decomposition of jumps into "small" and "large" may be defined on the jumps of the driving process $L_t$, but for analysis, it is often more natural to define it on the jumps of the state process $X_t$ itself, which are given by $\Delta X_t = G(X_{t-}) \Delta L_t$.

Let's consider such a transformation [@problem_id:2995477]. Suppose we have the SDE $dX_t = f(X_{t-}) dt + G(X_{t-}) dL_t$, where $L_t$ has [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ with $Q=\Sigma \Sigma^\top$. If we choose to decompose the jumps of $X_t$ based on a truncation function $h(y) = y \mathbf{1}_{|y|\le 1}$ acting on the state jump sizes $y=G(X_{t-})z$, the SDE can be rewritten as:

$$
\begin{aligned}
dX_t = \Bigg[f(X_{t-}) + G(X_{t-}) b + \int_{\mathbb{R}^m} \big(G(X_{t-})z - h(G(X_{t-})z)\big) \, \nu(dz)\Bigg] dt \\
\quad + G(X_{t-}) \Sigma \, dW_t \\
\quad + \int_{\mathbb{R}^m} h(G(X_{t-})z) \, \tilde{N}(dt, dz) \\
\quad + \int_{\mathbb{R}^m} \big(G(X_{t-})z - h(G(X_{t-})z)\big) \, N(dt, dz)
\end{aligned}
$$

Notice the crucial **drift adjustment term**: $\int (G(X_{t-})z - h(G(X_{t-})z)) \, \nu(dz)$. This term appears because we have represented the compensated small jumps and uncompensated large jumps according to the [state-space](@entry_id:177074) truncation $h$. The term $G(X_{t-})b$ is the drift inherited from the driving process $L_t$. The adjustment term represents the mean of the "large" state-space jumps, which must be added to the drift to maintain the same overall dynamics. This canonical form is the starting point for many theoretical analyses and [numerical schemes](@entry_id:752822).

### A Concrete Example: Symmetric $\alpha$-Stable Processes

To make these ideas tangible, it is instructive to study a specific, important class of Lévy processes. A **rotationally symmetric $\alpha$-stable Lévy process** in $\mathbb{R}^d$ with index $\alpha \in (0, 2)$ is a pure-[jump process](@entry_id:201473) whose properties of symmetry and self-similarity impose strong constraints on its [characteristic triplet](@entry_id:635937) $(b, Q, \nu)$ [@problem_id:2995471].

*   **Symmetry** ($X_t \overset{d}{=} -X_t$) implies that the drift vector $b$ must be zero and the Lévy measure $\nu$ must be symmetric ($\nu(A) = \nu(-A)$).
*   **Strict stability** ($X_t \overset{d}{=} t^{1/\alpha} X_1$) implies that the [characteristic exponent](@entry_id:188977) must be homogeneous of degree $\alpha$. For $\alpha \in (0,2)$, this forces the Gaussian variance $Q$ to be zero.

Combining these, the process is uniquely characterized by its Lévy measure. Rotational symmetry requires the measure to be uniform on spheres, and the stability property dictates its radial decay. The resulting Lévy measure has a simple density with respect to the Lebesgue measure [@problem_id:2995458]:

$$
\nu(dx) = c_{d,\alpha} |x|^{-d-\alpha} \, dx
$$

for some positive constant $c_{d,\alpha}$. This leads to a characteristic function $\mathbb{E}[\exp(i\langle \xi, X_t \rangle)] = \exp(-t c |\xi|^\alpha)$ for some scale constant $c0$.

The parameter $\alpha$ directly controls the "activity" of the jumps. For any $\alpha \in (0,2)$, the integral $\int_{|x|\le 1} \nu(dx) = \infty$, meaning the process has infinitely many small jumps in any time interval; it is a process of **infinite activity**. Furthermore, one can show that the [sample paths](@entry_id:184367) have **finite variation** if and only if $\alpha \in (0,1)$ [@problem_id:2995471]. When $\alpha \in [1,2)$, the paths have infinite variation.

### Quantifying Jump Activity: The Blumenthal-Getoor Index

The distinction between finite and infinite activity, or finite and infinite variation, can be refined. The **Blumenthal-Getoor (BG) index**, denoted $\beta$, provides a more nuanced measure of the intensity of small jumps of a Lévy process [@problem_id:2995453]. It is defined as:

$$
\beta = \inf \left\{ r  0 : \int_{|x| \le 1} |x|^r \, \nu(dx)  \infty \right\}
$$

The BG index is the [critical exponent](@entry_id:748054) for the [integrability](@entry_id:142415) of moments of small jumps against the Lévy measure. It has a direct interpretation in terms of the path properties:

*   It governs the convergence of the [sum of powers](@entry_id:634106) of small jumps. For a given $p0$, the sum over a finite time interval, $S_p(t) = \sum_{0  s \le t, |\Delta X_s| \le 1} |\Delta X_s|^p$, converges [almost surely](@entry_id:262518) if $p  \beta$ and diverges if $p  \beta$.
*   If the process has no Gaussian component, its paths are of finite variation if and only if $\beta \in [0,1)$. If $\beta \in [1,2)$, the paths are of infinite variation.
*   The BG index provides a sharp classification: $\beta = 0$ corresponds to finite activity (e.g., compound Poisson process); $\beta \in (0, 2)$ corresponds to infinite activity. For a symmetric $\alpha$-[stable process](@entry_id:183611), the BG index is precisely its stability index, $\beta = \alpha$.

### Fundamental Theoretical Results

With the structure of the SDE established, we turn to two cornerstone theoretical results that are indispensable for working with these models.

#### Well-Posedness: Existence and Uniqueness

A primary question for any SDE is whether a solution exists, is unique, and does not "explode" to infinity in finite time. For jump-diffusion SDEs, the classical conditions for diffusions are extended to include the jump term. A standard set of [sufficient conditions](@entry_id:269617) for the existence of a unique, non-exploding [strong solution](@entry_id:198344) involves global Lipschitz and linear growth constraints on the coefficients [@problem_id:2995473]:

There exist constants $L0$ and $K0$ such that for all $x, y \in \mathbb{R}^d$:
1.  **Lipschitz Condition**:
    *   $|b(x) - b(y)| \le L |x-y|$
    *   $\|\Sigma(x) - \Sigma(y)\|_{\mathrm{F}}^2 \le L^2 |x-y|^2$
    *   $\int_Z |\Gamma(x,z) - \Gamma(y,z)|^2 \, \nu(dz) \le L^2 |x-y|^2$

2.  **Linear Growth Condition**:
    *   $|b(x)|^2 \le K(1 + |x|^2)$
    *   $\|\Sigma(x)\|_{\mathrm{F}}^2 \le K(1 + |x|^2)$
    *   $\int_Z |\Gamma(x,z)|^2 \, \nu(dz) \le K(1 + |x|^2)$

These conditions, combined with a square-integrable initial condition, are sufficient to establish global [well-posedness](@entry_id:148590) using an $L^2$ theory based on Itô's formula and Gronwall's inequality. The Lipschitz condition controls the difference between two potential solutions, ensuring uniqueness, while the [linear growth condition](@entry_id:201501) bounds the growth of the process's second moment, preventing explosion.

#### Change of Measure: The Girsanov Theorem

The Girsanov theorem is a powerful tool for changing the probability measure under which a process is considered. This is fundamental in applications like financial [derivative pricing](@entry_id:144008), where one switches from a "real-world" measure to a "risk-neutral" measure. For jump-diffusions, the theorem allows for simultaneous changes to the drift of the Brownian part and the intensity of the jump part [@problem_id:2995451].

Suppose we change the measure from $\mathbb{P}$ to $\mathbb{Q}$ using a [predictable process](@entry_id:274260) $\theta_t$ to shift the Brownian motion and a predictable positive function $\kappa(t,z)$ to tilt the jump measure. The Radon-Nikodym density process $L_t = \frac{d\mathbb{Q}}{d\mathbb{P}}\big|_{\mathcal{F}_t}$ is given by the Doléans-Dade exponential:

$$
L_t = \exp\left(\int_0^t \theta_s \, dW_s - \frac{1}{2}\int_0^t \theta_s^2 \, ds\right) \exp\left(\int_0^t \int_E \ln \kappa(s,z) \, \mu(ds,dz) - \int_0^t \int_E (\kappa(s,z)-1) \, \nu_s(dz)ds\right)
$$

Under the new measure $\mathbb{Q}$:
1.  The process $W_t^{\mathbb{Q}} = W_t - \int_0^t \theta_s \, ds$ is a standard Brownian motion.
2.  The random measure $\mu$ has a new compensator $\nu_t^{\mathbb{Q}}(dz)dt = \kappa(t,z) \nu_t(dz)dt$.

Consequently, the SDE for $X_t$ transforms. The original dynamics under $\mathbb{P}$,
$dX_t = b_t dt + \sigma_t dW_t + \int_E \gamma(t,z) (\mu(dt,dz) - \nu_t(dz)dt)$,
become under $\mathbb{Q}$:
$$
dX_t = \left(b_t + \sigma_t\theta_t + \int_E \gamma(t,z) (\kappa(t,z)-1) \nu_t(dz)\right)dt + \sigma_t dW_t^{\mathbb{Q}} + \int_E \gamma(t,z) (\mu(dt,dz) - \kappa(t,z)\nu_t(dz)dt)
$$
The drift of $X_t$ is altered by two terms: $\sigma_t\theta_t$ from the change in the continuous part, and $\int \gamma(\kappa-1)\nu dt$ from the change in the jump intensity.

### A Tractable Class: Affine Jump-Diffusions

While the general theory provides a solid foundation, practical applications often rely on models that possess enough structure to be analytically tractable. **Affine jump-diffusions** form such a class and are ubiquitous in fields like [mathematical finance](@entry_id:187074) for modeling interest rates and asset prices. A process is affine if its drift, [diffusion matrix](@entry_id:182965), and jump intensity are affine functions of the state [@problem_id:2995462]:

*   Drift: $b(x) = b_0 + Bx$
*   Instantaneous Covariance: $a(x) = \Sigma(x)\Sigma(x)^\top = a_0 + \sum_{i=1}^d x_i a_i$
*   Lévy Measure: $\nu(x, dz) = \nu_0(dz) + \sum_{i=1}^d x_i \nu_i(dz)$

The remarkable property of affine processes lies in their **infinitesimal generator**. The generator $\mathcal{A}$ of a Markov process describes the expected rate of change of functions of the process. For an affine jump-diffusion (possibly with an affine killing rate $k(x) = k_0 + \kappa \cdot x$), when the generator acts on an exponential function $f(x) = e^{u \cdot x}$, the result is again an [exponential function](@entry_id:161417) multiplied by an [affine function](@entry_id:635019) of the state:

$$
\mathcal{A} e^{u \cdot x} = (\phi(u) + x \cdot \psi(u)) e^{u \cdot x}
$$

The functions $\phi(u)$ and $\psi(u)$ are themselves composed of the affine coefficients and are related to the characteristic exponents of the underlying Lévy measures. This affine structure of the generator has profound consequences. It implies that the [characteristic function](@entry_id:141714) of the process, $\mathbb{E}^x[\exp(u \cdot X_t)]$, is also of an exponential-affine form. Specifically, it can be shown to satisfy $\mathbb{E}^x[\exp(u \cdot X_t)] = \exp(\Phi(t,u) + x \cdot \Psi(t,u))$, where the coefficients $\Phi$ and $\Psi$ solve a system of ordinary differential equations (ODEs), known as Riccati equations. The ability to reduce the problem of finding the entire distribution of the process to solving a system of ODEs is what makes affine models exceptionally powerful and widely used.