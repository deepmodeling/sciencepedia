## Introduction
Markov Chain Monte Carlo (MCMC) methods are foundational to modern statistical computation, but standard algorithms are designed for simple Euclidean spaces. When a model's parameters are constrained to a [curved space](@entry_id:158033)—such as the sphere in [directional statistics](@entry_id:748454) or the space of [positive-definite matrices](@entry_id:275498) in machine learning—these methods become inefficient or ill-defined. This creates a critical gap for Bayesian inference in a wide range of scientific applications. Geometric MCMC provides a principled solution by reformulating sampling algorithms in the native language of the underlying space: Riemannian geometry.

This article serves as a comprehensive guide to this advanced class of samplers. We will begin by establishing the foundational **Principles and Mechanisms**, replacing Euclidean concepts with the Riemannian toolkit and constructing robust algorithms like the Manifold Metropolis-Adjusted Langevin Algorithm (MMALA) and geometric Hamiltonian Monte Carlo (HMC). Next, we will explore the **Applications and Interdisciplinary Connections**, demonstrating how these methods solve practical problems on topologically [complex manifolds](@entry_id:159076) and accelerate inference in computationally intensive models. Finally, the **Hands-On Practices** will offer concrete exercises to solidify the theoretical concepts. By navigating these chapters, you will gain the knowledge to harness the power of geometry for more efficient and accurate [statistical inference](@entry_id:172747).

## Principles and Mechanisms

Standard Markov Chain Monte Carlo (MCMC) algorithms, such as the Random-Walk Metropolis and the Metropolis-Adjusted Langevin Algorithm (MALA), are intrinsically designed for [sampling from probability distributions](@entry_id:754497) defined on Euclidean spaces, $\mathbb{R}^n$. Their proposal mechanisms rely on concepts native to this setting: straight-line movements for generating proposals and a constant, position-independent notion of distance. When the state space of a statistical model is not a simple Euclidean space but a curved manifold—such as the space of rotation matrices, spheres, or [positive-definite matrices](@entry_id:275498)—these algorithms can be inefficient or mathematically ill-defined. Geometric MCMC methods address this challenge by reformulating sampling algorithms within the natural language of the underlying space: the language of Riemannian geometry. This chapter elucidates the core principles and mechanisms that underpin these advanced sampling techniques.

### The Riemannian Toolkit for MCMC

The transition from Euclidean to Riemannian MCMC requires replacing familiar geometric concepts with their generalized counterparts. The foundational element of this new toolkit is the **Riemannian metric**, which equips a manifold with a notion of local geometry.

At each point $x$ on a manifold $M$, there exists a [tangent space](@entry_id:141028) $T_x M$, which is a vector space that can be thought of as the [best linear approximation](@entry_id:164642) of the manifold at that point. A Riemannian metric, denoted $g_x$, is a collection of inner products, one for each [tangent space](@entry_id:141028). For any two tangent vectors $u, v \in T_x M$, the metric $g_x(u, v)$ defines their inner product, which in turn allows us to define the length of vectors ($\|v\|_x = \sqrt{g_x(v, v)}$) and the angle between them. The metric can vary smoothly from point to point, which gives rise to the curvature of the manifold.

With the metric defined, we can introduce the Riemannian equivalent of a straight line: the **geodesic**. A geodesic is a curve on the manifold that is locally the shortest path between points. More formally, geodesics are curves $\gamma(t)$ that [parallel transport](@entry_id:160671) their own tangent vectors, satisfying the [geodesic equation](@entry_id:136555), a second-order ordinary differential equation. They can also be defined as the stationary curves of the [energy functional](@entry_id:170311) $E[\gamma] = \frac{1}{2} \int g_{\gamma(t)}(\dot{\gamma}(t), \dot{\gamma}(t)) dt$.

To construct algorithms, we need practical ways to move along geodesics. This is accomplished by two fundamental maps:

1.  The **Riemannian exponential map**, $\operatorname{Exp}_x : T_x M \to M$, generalizes the idea of moving from a point in a given direction. It takes a [tangent vector](@entry_id:264836) $v \in T_x M$ and maps it to the point $y \in M$ reached by following the unique geodesic starting at $x$ with [initial velocity](@entry_id:171759) $v$ for one unit of time. That is, if $\gamma(t)$ is the geodesic with $\gamma(0)=x$ and $\dot{\gamma}(0)=v$, then $\operatorname{Exp}_x(v) = \gamma(1)$.

2.  The **Riemannian logarithm map**, $\operatorname{Log}_x : M \to T_x M$, is the inverse of the exponential map (where defined). It takes a point $y \in M$ and returns the initial velocity vector $v \in T_x M$ required for a geodesic to travel from $x$ to $y$ in one unit of time. Thus, $v = \operatorname{Log}_x(y)$. The magnitude of this vector, $\| \operatorname{Log}_x(y) \|_x$, gives the [geodesic distance](@entry_id:159682) between $x$ and $y$.

A powerful example that illustrates these concepts is the manifold of [symmetric positive-definite](@entry_id:145886) (SPD) matrices, $\mathcal{S}_{++}^n$, a space that appears frequently in statistics, machine learning, and medical imaging. A common and useful metric on this space is the **affine-invariant Riemannian metric** . For a point $X \in \mathcal{S}_{++}^n$ and tangent vectors $U, V$ in the tangent space $T_X\mathcal{S}_{++}^n$ (which is simply the space of [symmetric matrices](@entry_id:156259)), the metric is defined as:
$$
g_X(U,V) = \operatorname{tr}(X^{-1} U X^{-1} V)
$$
Deriving the geometric toolkit for this metric is greatly simplified by exploiting its symmetries. The [congruence transformation](@entry_id:154837) $\phi_A(X) = AXA^\top$ for an invertible matrix $A$ is an isometry of this metric, meaning it preserves distances and angles. This allows us to perform calculations at the simplest point on the manifold, the identity matrix $I$, and then transform the results to any other point $X$.

At the identity $I$, the metric becomes the standard Euclidean inner product on matrices, $g_I(U,V) = \operatorname{tr}(UV)$. The geodesics starting at $I$ with velocity $V' \in T_I\mathcal{S}_{++}^n$ are simple matrix exponentials: $\gamma_I(t) = \exp(tV')$. Using the isometry $\phi_{X^{1/2}}(Z) = X^{1/2}ZX^{1/2}$ which maps $I$ to $X$, we can find the geodesic starting at any $X$ with velocity $V \in T_X\mathcal{S}_{++}^n$:
$$
\gamma(t) = X^{1/2} \exp\left(t X^{-1/2} V X^{-1/2}\right) X^{1/2}
$$
From this, the exponential and logarithm maps follow directly :
$$
\operatorname{Exp}_X(V) = X^{1/2} \exp\left(X^{-1/2} V X^{-1/2}\right) X^{1/2}
$$
$$
\operatorname{Log}_X(Y) = X^{1/2} \log\left(X^{-1/2} Y X^{-1/2}\right) X^{1/2}
$$
where $\log(\cdot)$ denotes the principal [matrix logarithm](@entry_id:169041). The [geodesic distance](@entry_id:159682) $d(X,Y)$ is the norm of the [tangent vector](@entry_id:264836) that connects the points, $d(X,Y) = \| \operatorname{Log}_X(Y) \|_X$. This leads to a remarkably elegant formula expressed in terms of the eigenvalues $\lambda_i$ of the matrix product $X^{-1}Y$:
$$
d(X,Y) = \sqrt{\sum_{i=1}^n (\ln(\lambda_i))^2}
$$
For instance, the [geodesic distance](@entry_id:159682) between the [diagonal matrices](@entry_id:149228) $X = \begin{pmatrix} 9  0 \\ 0  4 \end{pmatrix}$ and $Y = \begin{pmatrix} 18  0 \\ 0  4/5 \end{pmatrix}$ on $\mathcal{S}_{++}^2$ can be found by first computing the eigenvalues of $X^{-1}Y = \begin{pmatrix} 2  0 \\ 0  1/5 \end{pmatrix}$, which are $\lambda_1 = 2$ and $\lambda_2 = 1/5$. The distance is then $d(X,Y) = \sqrt{(\ln 2)^2 + (\ln(1/5))^2} = \sqrt{(\ln 2)^2 + (\ln 5)^2}$ .

### Building MCMC Algorithms on Manifolds

With the Riemannian toolkit established, we can adapt standard MCMC algorithms. A prime example is the generalization of MALA to the **manifold Metropolis-adjusted Langevin algorithm (MMALA)**. The standard Langevin diffusion is driven by the gradient of the log-target density. On a manifold, the target density $\pi(x) \propto \exp(-U(x))$ is defined with respect to the Riemannian volume measure, and its gradient is the Riemannian gradient, $\nabla U$. The corresponding overdamped Langevin diffusion on the manifold $(M,g)$ takes the form
$$
dX_t = -\frac{1}{2} (G(X_t))^{-1} \nabla U(X_t) dt + d\mathcal{B}_t
$$
where $G(X_t)$ is the matrix representation of the metric $g_{X_t}$ in [local coordinates](@entry_id:181200) and $d\mathcal{B}_t$ is Riemannian Brownian motion.

A [numerical discretization](@entry_id:752782) of this diffusion forms the basis for the MMALA proposal. Unlike in Euclidean space, the local "scale" of the space, given by the metric $g(x)$, is position-dependent. This affects both the drift and diffusion components of the proposal. A simplified MMALA proposal at state $x$ for a new state $x'$ can be formulated as a Gaussian distribution on the tangent space, which is then mapped to the manifold. In a one-dimensional setting for clarity, with a metric $g(x)$, a target $\pi(x) \propto \exp(-U(x))$, and a step-size $h$, the proposal might be a Gaussian with a position-dependent mean and variance :
$$
\mu(x) = x - \frac{h^2}{2} g(x)^{-1} U'(x)
$$
$$
\sigma^2(x) = h^2 g(x)^{-1}
$$
The crucial insight is that the proposal density $q(x'|x) = \mathcal{N}(x' ; \mu(x), \sigma^2(x))$ is no longer symmetric. That is, because the variance $\sigma^2$ depends on the position, $q(x'|x)$ is generally not equal to $q(x|x')$. Consequently, a simple Metropolis [acceptance probability](@entry_id:138494), which assumes symmetry, would not yield the correct [stationary distribution](@entry_id:142542). We must use the full **Metropolis-Hastings** acceptance probability, $\alpha(x, x') = \min\left(1, r(x,x')\right)$, where the acceptance ratio $r(x,x')$ includes a correction for the proposal asymmetry:
$$
r(x, x') = \frac{\pi(x') q(x | x')}{\pi(x) q(x' | x)}
$$
Working with the log-acceptance ratio is often more stable:
$$
\ln r(x, x') = \ln(\pi(x')) - \ln(\pi(x)) + \ln(q(x | x')) - \ln(q(x' | x))
$$
Substituting the expressions for the Gaussian proposal density and noting that $\ln(\pi(x)) = -U(x) + \text{const}$, we find that the Hastings correction term $\ln(q(x | x')) - \ln(q(x' | x))$ introduces a term related to the metric itself. Specifically, the log-ratio of the normalization constants of the Gaussian proposals contributes a term $\frac{1}{2}\ln(\sigma^2(x)/\sigma^2(x')) = \frac{1}{2}\ln(g(x')/g(x))$ . This demonstrates a core principle: when designing MCMC on manifolds, the geometry, encoded in the metric, influences not only the proposal's drift and variance but also the very structure of the [acceptance probability](@entry_id:138494).

### Practical Integration with Retractions and Vector Transports

While the [exponential map](@entry_id:137184) provides a geometrically perfect way to move on a manifold, it is often computationally expensive or may not have a [closed-form expression](@entry_id:267458). This presents a major hurdle for algorithms like Hamiltonian Monte Carlo (HMC), which require simulating trajectories on the manifold. To overcome this, we turn to practical approximations: **retractions** and **vector transports**.

A **retraction** $R_x(v)$ is a smooth mapping from the tangent space $T_x M$ to the manifold $M$ that serves as a computationally cheaper, first-order approximation to the exponential map. It must satisfy two key properties: $R_x(0) = x$, and its differential at the origin of the tangent space is the identity map. A common example is the projection-based retraction on a sphere or circle. For a point $x$ on the unit circle $S^1$ and a tangent vector $v \in T_x S^1$, the retraction can be defined by moving along $v$ in the ambient Euclidean space and then projecting the result back onto the circle :
$$
R_x(v) = \frac{x+v}{\|x+v\|}
$$

Hamiltonian dynamics evolves a system in phase space (position and momentum). As the position $x$ moves to a new point $y$ on the manifold, the associated momentum vector, which lives in $T_x M$, must be moved to the new tangent space $T_y M$. The geometrically correct way to do this is via **parallel transport**, a procedure that moves a tangent vector along a curve (ideally a geodesic) without changing its length or its angle relative to the curve. Like the exponential map, parallel transport can be computationally demanding.

A **vector transport** $\mathcal{T}_{x \to y}(v)$ is a practical approximation of [parallel transport](@entry_id:160671). It provides a rule for mapping a vector $v \in T_x M$ to a vector in $T_y M$. A simple and widely used transport is [orthogonal projection](@entry_id:144168). For example, to transport a vector $w$ (residing in the ambient $\mathbb{R}^2$) to the tangent space at a new point $y \in S^1$, we can project $w$ onto $T_y S^1$: $\Pi_{T_y S^1}(w) = w - (w \cdot y)y$ .

These approximations allow us to construct a tractable "leapfrog" integrator for HMC on a manifold. A single step starting from $(x_0, p_0)$ with step-size $h$ might look like this:
1.  **Momentum Half-Step:** Update momentum based on the [potential gradient](@entry_id:261486): $p_{1/2} = p_0 - \frac{h}{2} \nabla U(x_0)$.
2.  **Position Update:** Update position using the retraction: $x_1 = R_{x_0}(h p_{1/2})$.
3.  **Momentum Transport:** Transport the intermediate momentum vector to the new [tangent space](@entry_id:141028) using a vector transport: $\tilde{p}_{1/2} = \mathcal{T}_{x_0 \to x_1}(p_{1/2})$.
4.  **Momentum Half-Step:** Complete the momentum update at the new position: $p_1 = \tilde{p}_{1/2} - \frac{h}{2} \nabla U(x_1)$.

The price of this computational convenience is that the integrator no longer exactly conserves the Hamiltonian energy. This introduces a numerical error, which is the primary reason HMC algorithms require a final Metropolis-Hastings acceptance step to ensure the correct [stationary distribution](@entry_id:142542) is targeted. By performing an [asymptotic expansion](@entry_id:149302) for small step-sizes $h$, we can analyze the magnitude of this error. For the specific retraction-transport scheme on the circle $S^1$ with initial condition $(\theta_0, p_0)=(0,p)$ , the Hamiltonian error $H(\theta_1, p_1) - H(\theta_0, p_0)$ can be shown to be of order $h^2$, with a leading-order term of $-\frac{1}{2} p^4 h^2$. This non-zero error is a direct consequence of the retraction and vector transport being only first-order approximations to the true [geodesic flow](@entry_id:270369). Understanding these errors is fundamental to designing and tuning efficient geometric MCMC samplers for complex, real-world problems.