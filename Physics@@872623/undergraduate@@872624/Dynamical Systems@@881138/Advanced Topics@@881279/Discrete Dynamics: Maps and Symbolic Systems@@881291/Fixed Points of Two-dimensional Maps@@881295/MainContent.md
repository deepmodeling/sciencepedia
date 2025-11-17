## Introduction
In the study of how systems evolve over time, points of equilibrium—states that do not change—are of paramount importance. For discrete [two-dimensional systems](@entry_id:274086), or "maps," these are known as fixed points. While a system at a fixed point is stationary, the behavior of nearby states reveals the system's fundamental dynamic character, determining whether it will return to equilibrium, be repelled from it, or spiral into complex oscillations. This article addresses the essential challenge of how to find these fixed points, determine their stability, and understand their profound impact on the system's overall structure and behavior.

By delving into this topic, you will gain a foundational toolkit for analyzing a vast range of dynamic phenomena. The first chapter, **"Principles and Mechanisms,"** lays out the core mathematical framework, showing how to locate fixed points and use the Jacobian matrix and its eigenvalues to classify them as stable nodes, unstable spirals, saddles, and more. Next, **"Applications and Interdisciplinary Connections"** bridges theory and practice, demonstrating how [fixed point analysis](@entry_id:267530) provides critical insights into real-world systems, from competing species in ecology to feedback controllers in engineering. Finally, the **"Hands-On Practices"** section will challenge you to apply these concepts, solidifying your understanding through targeted exercises.

## Principles and Mechanisms

In the study of two-dimensional [discrete dynamical systems](@entry_id:154936), or maps, the concept of a **fixed point** is of fundamental importance. These are the states of a system that remain unchanged under its evolution rule, representing points of equilibrium. While a system at a fixed point is stationary, the behavior of trajectories in its vicinity reveals the essential character of the local dynamics. This chapter will delineate the principles for finding and classifying these fixed points and explore the rich geometric structures they organize in the system's phase space.

### Finding Fixed Points and Periodic Orbits

A two-dimensional map is a function $\mathbf{F}: \mathbb{R}^2 \to \mathbb{R}^2$ that takes a point $\mathbf{x}_n = (x_n, y_n)$ to the next point in a sequence, $\mathbf{x}_{n+1} = \mathbf{F}(\mathbf{x}_n)$. A point $\mathbf{x}^* = (x^*, y^*)$ is a **fixed point** of the map if it is mapped to itself, that is:

$$\mathbf{x}^* = \mathbf{F}(\mathbf{x}^*)$$

In terms of components, if $\mathbf{F}(x, y) = (f(x, y), g(x, y))$, then the fixed points are the solutions to the system of algebraic equations:

$$x^* = f(x^*, y^*)$$
$$y^* = g(x^*, y^*)$$

The complexity of solving this system depends entirely on the nature of the functions $f$ and $g$. A particularly straightforward case arises when the two components evolve independently of each other, a situation known as a **decoupled system**.

Consider a model for two non-interacting species where the population of the "Sun-dusted Moth", $x$, and the "Veridian Beetle", $y$, are governed by the decoupled map $x_{k+1} = \mu x_k(2 - x_k)$ and $y_{k+1} = \lambda y_k^2$ [@problem_id:1676569]. A fixed point $(x^*, y^*)$ must satisfy $x^* = \mu x^*(2 - x^*)$ and $y^* = \lambda (y^*)^2$. Notice that the equation for $x^*$ does not involve $y^*$, and vice versa. We can therefore solve for the fixed-point values of each component separately. For $\mu=1.5$, the solutions for $x^*$ are $x^*=0$ and $x^*=2-1/\mu = 4/3$. For $\lambda=4$, the solutions for $y^*$ are $y^*=0$ and $y^*=1/\lambda = 1/4$. The fixed points of the two-dimensional system are then all possible combinations of these individual solutions: $(0, 0)$, $(4/3, 0)$, $(0, 1/4)$, and $(4/3, 1/4)$. This illustrates a general principle: for a decoupled map $(x, y) \mapsto (f(x), g(y))$, the set of fixed points is the Cartesian product of the sets of fixed points for the one-dimensional maps $x \mapsto f(x)$ and $y \mapsto g(y)$.

Beyond fixed points, dynamical systems can exhibit **[periodic orbits](@entry_id:275117)** or **cycles**, which are sequences of points that repeat. A point $\mathbf{x}_0$ is part of a **period-k orbit** (or [k-cycle](@entry_id:181391)) if $\mathbf{F}^k(\mathbf{x}_0) = \mathbf{x}_0$ and $\mathbf{F}^j(\mathbf{x}_0) \neq \mathbf{x}_0$ for $1 \le j  k$, where $\mathbf{F}^k$ denotes applying the map $k$ times. An essential insight is that any point in a [k-cycle](@entry_id:181391) of a map $\mathbf{F}$ is, by definition, a fixed point of the iterated map $\mathbf{F}^k$. For instance, if a point $P_0$ is part of a 2-cycle such that $F(P_0) = P_1$ and $F(P_1) = P_0$ with $P_0 \neq P_1$, applying the map twice to $P_0$ yields $F^2(P_0) = F(F(P_0)) = F(P_1) = P_0$ [@problem_id:1676559]. Thus, finding periodic orbits of a map is equivalent to finding fixed points of its iterates.

### Linearization and The Jacobian Matrix

Once a fixed point $\mathbf{x}^*$ is located, the next crucial step is to understand its **stability**. Does a trajectory starting near $\mathbf{x}^*$ move toward it, away from it, or simply orbit it? For most fixed points, this question can be answered by **linearization**: approximating the nonlinear map $\mathbf{F}$ near $\mathbf{x}^*$ by a linear map that captures the local dynamics.

Let $\mathbf{x}_n = \mathbf{x}^* + \delta\mathbf{x}_n$, where $\delta\mathbf{x}_n$ is a small deviation from the fixed point. Then,
$$\mathbf{x}_{n+1} = \mathbf{x}^* + \delta\mathbf{x}_{n+1} = \mathbf{F}(\mathbf{x}^* + \delta\mathbf{x}_n)$$
Using a first-order Taylor expansion of $\mathbf{F}$ around $\mathbf{x}^*$, we get:
$$\mathbf{F}(\mathbf{x}^* + \delta\mathbf{x}_n) \approx \mathbf{F}(\mathbf{x}^*) + D\mathbf{F}(\mathbf{x}^*) \delta\mathbf{x}_n$$
where $D\mathbf{F}(\mathbf{x}^*)$ is the matrix of [partial derivatives](@entry_id:146280) of $\mathbf{F}$ evaluated at $\mathbf{x}^*$. This matrix is known as the **Jacobian matrix**, denoted by $J$.

Since $\mathbf{F}(\mathbf{x}^*) = \mathbf{x}^*$, the relation simplifies to $\mathbf{x}^* + \delta\mathbf{x}_{n+1} \approx \mathbf{x}^* + J \delta\mathbf{x}_n$, which gives the linearized dynamics:
$$\delta\mathbf{x}_{n+1} \approx J \delta\mathbf{x}_n$$

The Jacobian matrix for a map $\mathbf{F}(x,y) = (f(x,y), g(x,y))$ is:
$$J(x,y) = D\mathbf{F}(x,y) = \begin{pmatrix} \frac{\partial f}{\partial x}  \frac{\partial f}{\partial y} \\ \frac{\partial g}{\partial x}  \frac{\partial g}{\partial y} \end{pmatrix}$$

As an example, consider the celebrated Hénon map, a paradigm for [chaotic dynamics](@entry_id:142566), given by $x_{n+1} = 1 - ax_n^2 + y_n$ and $y_{n+1} = bx_n$ [@problem_id:1676553]. With parameters $a=2, b=2$, one of the fixed points is found by solving $x = 1 - 2x^2 + y$ and $y = 2x$. Substituting the second equation into the first yields a quadratic equation $2x^2 - x - 1 = 0$, with solutions $x=1$ and $x=-1/2$. The fixed point with the larger x-coordinate is $(1, 2)$. The Jacobian matrix of this map is:
$$J(x,y) = \begin{pmatrix} -2ax  1 \\ b  0 \end{pmatrix}$$
Evaluating this at the fixed point $(1, 2)$ with $a=2, b=2$ gives the constant matrix that governs the local [linear dynamics](@entry_id:177848):
$$J(1,2) = \begin{pmatrix} -4  1 \\ 2  0 \end{pmatrix}$$
The behavior of this linear map determines the stability of the fixed point.

### The Geometry of Linearization: Eigenvalues and Eigendirections

The dynamics of the linear map $\delta\mathbf{x}_{n+1} = J \delta\mathbf{x}_n$ are entirely determined by the **eigenvalues** and **eigenvectors** of the Jacobian matrix $J$. An eigenvector $\mathbf{v}$ of $J$ is a non-[zero vector](@entry_id:156189) that does not change direction when multiplied by $J$; it is only scaled by a factor $\lambda$, its corresponding eigenvalue: $J\mathbf{v} = \lambda\mathbf{v}$.

These eigenvectors define special directions through the fixed point, known as **eigendirections**. If a deviation $\delta\mathbf{x}_0$ from the fixed point lies along an eigendirection $\mathbf{v}$, subsequent deviations will remain along this line: $\delta\mathbf{x}_n = \lambda^n \delta\mathbf{x}_0$. The line passing through the fixed point in the direction of an eigenvector is an **invariant line** of the linearized system [@problem_id:1676538].
*   If $|\lambda|  1$, points on this line are attracted towards the fixed point. This is a **stable eigendirection**.
*   If $|\lambda| > 1$, points on this line are repelled from the fixed point. This is an **unstable eigendirection**.
*   If $|\lambda| = 1$, points on this line maintain their distance from the fixed point in the [linear approximation](@entry_id:146101).

For example, in a population model governed by the [linear map](@entry_id:201112) $\vec{p}_{n+1} = A \vec{p}_n$ with $A = \begin{pmatrix} 2  1 \\ 1  3 \end{pmatrix}$, the eigenvalues are $\lambda_{\pm} = \frac{5 \pm \sqrt{5}}{2}$. The larger eigenvalue, $\lambda_+ \approx 3.618$, corresponds to a faster rate of population growth. The associated eigenvector, which can be found by solving $(A - \lambda_+ I)\mathbf{v} = \mathbf{0}$, defines an invariant line with slope $y/x = \lambda_+ - 2 = \frac{1+\sqrt{5}}{2}$ [@problem_id:1676538]. Any initial population with this ratio will see its population grow by a factor of $\lambda_+$ at each time step, while maintaining the same population ratio.

### Classification of Hyperbolic Fixed Points

A fixed point is called **hyperbolic** if none of the eigenvalues of its Jacobian matrix have a modulus of one (i.e., $|\lambda_i| \neq 1$ for all $i$). For [hyperbolic fixed points](@entry_id:269450), the Hartman-Grobman theorem guarantees that the dynamics of the nonlinear map in a small neighborhood of the fixed point are qualitatively the same as the dynamics of its linearization. This allows us to classify [hyperbolic fixed points](@entry_id:269450) based solely on their eigenvalues.

Let the eigenvalues of the $2 \times 2$ Jacobian be $\lambda_1$ and $\lambda_2$.

**Case 1: Real Eigenvalues ($\lambda_1, \lambda_2 \in \mathbb{R}$)**

*   **Stable Node:** If $0  |\lambda_{1,2}|  1$. All nearby trajectories approach the fixed point tangent to the eigendirection of the eigenvalue with the larger magnitude (slower contracting direction).
*   **Unstable Node:** If $|\lambda_{1,2}| > 1$. All nearby trajectories are repelled from the fixed point.
*   **Saddle Point:** If one eigenvalue has modulus less than 1 and the other greater than 1 (e.g., $|\lambda_1|  1  |\lambda_2|$). This is a fundamentally important type of fixed point. Trajectories are attracted along the stable eigendirection but repelled along the unstable eigendirection. For the system $x_{n+1} = \frac{7}{4}x_n - \frac{1}{2}y_n^2$, $y_{n+1} = \frac{1}{2}y_n + \frac{1}{4}x_n^2$, the Jacobian at the fixed point $(0,0)$ is $J(0,0) = \begin{pmatrix} 7/4  0 \\ 0  1/2 \end{pmatrix}$. The eigenvalues are $\lambda_1 = 7/4$ and $\lambda_2 = 1/2$. Since $|\lambda_1| > 1$ and $|\lambda_2|  1$, the origin is a saddle point [@problem_id:1676565].

**Case 2: Complex Conjugate Eigenvalues ($\lambda_{1,2} = \alpha \pm i\beta$)**

If the eigenvalues are complex, they must occur in a conjugate pair for a real matrix. The dynamics involve rotation. Let $|\lambda| = \sqrt{\alpha^2 + \beta^2}$.

*   **Stable Spiral (or Spiral Sink):** If $|\lambda|  1$. Trajectories spiral inwards towards the fixed point. For instance, in a model of a controlled mechanical system, linearization around the origin might yield eigenvalues $\lambda = 0.9 \pm 0.3i$. Since $|\lambda| = \sqrt{0.9^2 + 0.3^2} = \sqrt{0.9}  1$, the origin is a [stable spiral](@entry_id:269578) [@problem_id:1676535].
*   **Unstable Spiral (or Spiral Source):** If $|\lambda| > 1$. Trajectories spiral outwards, away from the fixed point.
*   **Center:** If $|\lambda| = 1$. In the [linear approximation](@entry_id:146101), trajectories are [closed curves](@entry_id:264519) (ellipses) around the fixed point. This is a non-hyperbolic case, and the true [nonlinear dynamics](@entry_id:140844) may differ.

### Phase Space Structure: Manifolds and Basins

The eigendirections of the Jacobian provide a blueprint for the geometric structures that organize the entire phase space. For a saddle point, the local directions of attraction and repulsion extend globally into curves known as the **[stable and unstable manifolds](@entry_id:261736)**.

*   The **stable manifold**, $W^s(\mathbf{x}^*)$, is the set of all points that are attracted to the fixed point $\mathbf{x}^*$ as time goes to infinity ($n \to \infty$).
*   The **unstable manifold**, $W^u(\mathbf{x}^*)$, is the set of all points that are attracted to the fixed point as time goes to negative infinity ($n \to -\infty$), i.e., points that are repelled from $\mathbf{x}^*$ forward in time.

Crucially, the stable and unstable eigendirections of the Jacobian at the fixed point are tangent to the [stable and unstable manifolds](@entry_id:261736) at that point. We can therefore approximate the manifolds near the fixed point by the straight lines defined by the eigenvectors [@problem_id:1676529]. For the map with Jacobian $J = \begin{pmatrix} 2  1/2 \\ 3  0 \end{pmatrix}$ at the origin, the eigenvalues are $\lambda_s = 1 - \sqrt{10}/2$ (stable) and $\lambda_u = 1 + \sqrt{10}/2$ (unstable). The corresponding eigenvectors give the slopes of the local stable manifold, $m_s = -2-\sqrt{10}$, and local unstable manifold, $m_u = \sqrt{10}-2$.

These manifolds are not just local curiosities; they have profound global consequences. For systems with one or more attracting fixed points (or other [attractors](@entry_id:275077)), the phase space is partitioned into **basins of attraction**. The basin of an attractor is the set of all [initial conditions](@entry_id:152863) whose trajectories converge to it. The boundaries of these basins are often formed by the stable manifolds of [saddle points](@entry_id:262327). A trajectory starting infinitesimally on one side of a [stable manifold](@entry_id:266484) will converge to one attractor, while a trajectory on the other side may converge to a different attractor or diverge to infinity. This makes the stable manifolds of saddles the critical "watersheds" of the dynamical landscape [@problem_id:1676575].

### Beyond Linearization: Non-Hyperbolic Points and Bifurcations

When a fixed point is **non-hyperbolic** (i.e., at least one eigenvalue has modulus $|\lambda|=1$), the Hartman-Grobman theorem does not apply. The [linear approximation](@entry_id:146101) is insufficient to determine stability, and the nonlinear terms of the map become decisive.

These non-hyperbolic cases represent the boundaries between different [stability regions](@entry_id:166035). We can visualize these boundaries in the plane of the Jacobian's trace ($\tau = \lambda_1 + \lambda_2$) and determinant ($\Delta = \lambda_1 \lambda_2$). A fixed point is non-hyperbolic if an eigenvalue is $1$, $-1$, or a complex number with modulus $1$. These conditions correspond to specific lines in the $(\tau, \Delta)$ plane [@problem_id:1676557]:
*   $\lambda = 1$ is an eigenvalue $\iff \Delta = \tau - 1$.
*   $\lambda = -1$ is an eigenvalue $\iff \Delta = -\tau - 1$.
*   $\lambda = e^{\pm i\theta}$ are eigenvalues $\iff \Delta = 1$ (and $\tau^2 - 4  0$).

When the parameters of a map are varied, a fixed point's eigenvalues may move in the complex plane. If they cross the unit circle, the fixed point's stability changes, and the system undergoes a **bifurcation**—a qualitative change in the long-term dynamics. The three lines above are the locations of the three generic co-dimension one bifurcations for maps: the saddle-node, period-doubling, and Neimark-Sacker [bifurcations](@entry_id:273973).

The **Neimark-Sacker bifurcation** occurs when a pair of [complex conjugate eigenvalues](@entry_id:152797) cross the unit circle away from the real axis. This typically results in a fixed point changing from a [stable spiral](@entry_id:269578) to an unstable spiral (or vice-versa) and the birth of a small, closed **invariant circle** around the fixed point. For a qubit model with Jacobian $J(0,0) = \begin{pmatrix} r  -b \\ b  r \end{pmatrix}$, the eigenvalues are $\lambda = r \pm ib$ with modulus $|\lambda|=\sqrt{r^2+b^2}$. A Neimark-Sacker bifurcation occurs when $|\lambda|=1$, meaning $r^2+b^2=1$. If $b = \sin(\pi/7)$, this bifurcation happens at the critical parameter value $r_c = \sqrt{1-\sin^2(\pi/7)} = \cos(\pi/7)$ [@problem_id:1676555].

The subtle role of nonlinear terms is starkly illustrated by comparing two maps whose Jacobians at the origin both have eigenvalues $(\lambda_1, \lambda_2) = (1,1)$ [@problem_id:1676567].
1.  For the map $F_A(x, y) = ( x - \alpha x (x^2+y^2), y - \alpha y (x^2+y^2) )$, the Jacobian is the identity matrix. The nonlinear term is a damping force that pulls points toward the origin.
2.  For the map $F_B(x, y) = ( x+y, y+\beta x^2 )$, the Jacobian is a non-diagonalizable Jordan block $\begin{pmatrix} 1  1 \\ 0  1 \end{pmatrix}$. The nonlinear term combines with the linear "shear" to push points away from the origin.
Even with identical eigenvalues from [linearization](@entry_id:267670), the full dynamics are completely different: one system is stable, the other unstable, a distinction entirely determined by the form of the higher-order terms. This serves as a powerful reminder that while linearization is an indispensable tool, its limitations define the frontier where the most interesting and complex dynamical phenomena often emerge.