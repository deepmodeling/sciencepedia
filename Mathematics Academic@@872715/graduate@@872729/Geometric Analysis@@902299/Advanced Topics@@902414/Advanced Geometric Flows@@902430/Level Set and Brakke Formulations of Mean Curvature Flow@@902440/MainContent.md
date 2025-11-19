## Introduction
Mean curvature flow, the process by which a surface evolves to minimize its area, is a fundamental concept in [geometric analysis](@entry_id:157700) with deep connections to physics and materials science. However, the classical description of this flow often breaks down in finite time as surfaces develop singularities, points where curvature blows up and smoothness is lost. To study the evolution through and beyond these critical moments, mathematicians have developed powerful "weak" formulations that generalize the classical notion of flow. This article delves into the two most influential of these frameworks: the measure-theoretic Brakke formulation and the PDE-based [level-set method](@entry_id:165633).

The first chapter, "Principles and Mechanisms," lays the theoretical foundation, introducing the concept of [varifolds](@entry_id:199701) in Brakke's approach and the theory of [viscosity solutions](@entry_id:177596) for the [level-set](@entry_id:751248) equation. It explains how each framework rigorously defines a flow that can handle singularities. The second chapter, "Applications and Interdisciplinary Connections," explores the far-reaching impact of these ideas, showing how [mean curvature flow](@entry_id:184231) emerges in [reaction-diffusion systems](@entry_id:136900) and how the [level-set method](@entry_id:165633) has revolutionized computational modeling of [moving interfaces](@entry_id:141467) in science and engineering. Finally, the "Hands-On Practices" section provides concrete problems to solidify understanding, from analyzing the basic shrinking sphere to exploring the properties of singularity models. This structured journey will equip you with a comprehensive understanding of how these advanced formulations extend the study of [geometric flows](@entry_id:198994) into the realm of non-smooth and topologically complex evolutions.

## Principles and Mechanisms

The evolution of a surface by its mean curvature, while simple to state, leads to the formation of singularities in finite time. These singularities, where curvature blows up and the classical geometric [partial differential equation](@entry_id:141332) (PDE) breaks down, necessitate the development of "weak" formulations of the flow that can be meaningfully continued through and beyond these events. This chapter introduces the two most prominent and powerful weak formulations: the measure-theoretic approach of Kenneth Brakke and the [viscosity solution](@entry_id:198358) framework for the [level-set](@entry_id:751248) equation. We will explore the foundational principles of each and the key analytic tools used to study them.

### The Measure-Theoretic Formulation: Brakke Flow

The Brakke formulation recasts [mean curvature flow](@entry_id:184231) as an evolution of measures. This approach, rooted in [geometric measure theory](@entry_id:187987) (GMT), is capable of describing surfaces with very low regularity, including those with evolving singularities and [topological changes](@entry_id:136654). The central objects in this framework are [varifolds](@entry_id:199701).

#### Varifolds as Generalized Surfaces

To describe a generalized, unoriented $n$-dimensional surface in $\mathbb{R}^{n+1}$, we need a structure that encodes not just the location of the surface but also the direction of its tangent plane at each point. A simple measure on $\mathbb{R}^{n+1}$ is insufficient as it loses all directional information. The appropriate geometric object is a **[varifold](@entry_id:194011)**.

A **[varifold](@entry_id:194011)** $V$ is a Radon measure on the [product space](@entry_id:151533) $\mathbb{R}^{n+1} \times G(n+1, n)$, where $G(n+1, n)$ is the Grassmannian of unoriented $n$-dimensional planes in $\mathbb{R}^{n+1}$. For any [test function](@entry_id:178872) $\phi \in C_c(\mathbb{R}^{n+1} \times G(n+1, n))$, the [varifold](@entry_id:194011) gives a value $V(\phi) = \int \phi(x, S) \, dV(x, S)$. Intuitively, a [varifold](@entry_id:194011) is a distribution of tangent planes over space.

From a [varifold](@entry_id:194011) $V$, we can recover the spatial mass distribution by "forgetting" the plane information. This gives the **weight measure** $\mu_V$, a Radon measure on $\mathbb{R}^{n+1}$, defined as the pushforward of $V$ under the projection $\pi: \mathbb{R}^{n+1} \times G(n+1, n) \to \mathbb{R}^{n+1}$. For any Borel set $A \subset \mathbb{R}^{n+1}$, its mass is given by $\mu_V(A) = V(A \times G(n+1, n))$.

While this definition is very general, to model surfaces, we are primarily interested in **[rectifiable varifolds](@entry_id:634475)**. An $n$-dimensional [varifold](@entry_id:194011) $V$ is rectifiable if there exists a countably $n$-rectifiable set $M \subset \mathbb{R}^{n+1}$ (a set that can be covered, up to a set of Hausdorff $n$-measure zero, by countably many Lipschitz images of subsets of $\mathbb{R}^n$) and a locally $\mathcal{H}^n$-integrable [multiplicity](@entry_id:136466) function $\theta: M \to [0, \infty)$ such that $V$ is concentrated on the graph of the approximate tangent plane map. That is, for $\mathcal{H}^n$-almost every $x \in M$, there exists an approximate tangent plane $T_x M \in G(n+1, n)$, and for any [test function](@entry_id:178872) $\phi$, the [varifold](@entry_id:194011) is given by integration over $M$:
$$
V(\phi) = \int_M \phi(x, T_x M) \, \theta(x) \, d\mathcal{H}^n(x)
$$
In this case, the weight measure is simply $\mu_V = \theta \, \mathcal{H}^n \llcorner M$. A further restriction leads to **integral [varifolds](@entry_id:199701)**, where the multiplicity function $\theta(x)$ is required to be integer-valued ($\theta(x) \in \mathbb{N}$) for $\mu_V$-almost every $x$. This is the class of [varifolds](@entry_id:199701) that arise as limits of smooth surfaces and possess strong compactness properties [@problem_id:3031789] [@problem_id:3031784].

#### First Variation and Generalized Mean Curvature

For a smooth $n$-manifold $M \subset \mathbb{R}^{n+1}$, the [first variation](@entry_id:174697) of its area under a deformation by a vector field $X \in C_c^1(\mathbb{R}^{n+1}; \mathbb{R}^{n+1})$ is given by $\int_M \operatorname{div}_M X \, d\mathcal{H}^n$, where $\operatorname{div}_M X$ is the tangential divergence of $X$ on $M$. This motivates the definition of the **[first variation](@entry_id:174697)** of a [varifold](@entry_id:194011) $V$ as the distribution
$$
\delta V(X) = \int_{\mathbb{R}^{n+1} \times G(n+1, n)} \operatorname{div}_S X(x) \, dV(x, S)
$$
where $\operatorname{div}_S X(x)$ is the trace of the projection of the gradient of $X$ onto the plane $S$.

For a smooth manifold, the divergence theorem gives $\int_M \operatorname{div}_M X \, d\mathcal{H}^n = -\int_M X \cdot H_{\text{class}} \, d\mathcal{H}^n$, where $H_{\text{class}}$ is the classical [mean curvature vector](@entry_id:199617). This suggests that the [mean curvature](@entry_id:162147) of a [varifold](@entry_id:194011) should be related to its [first variation](@entry_id:174697). We say a [varifold](@entry_id:194011) $V$ has a **[generalized mean curvature](@entry_id:199614) vector** if its [first variation](@entry_id:174697) $\delta V$, which is a priori a distribution, is representable as an integral against its weight measure $\mu_V$. This requires the vector-valued measure associated with $\delta V$ to be absolutely continuous with respect to the scalar measure $\mu_V$. If this condition holds, the Radon-Nikodym theorem guarantees the existence of a unique (up to a set of $\mu_V$-[measure zero](@entry_id:137864)) vector field $H \in L^1_{\text{loc}}(\mu_V; \mathbb{R}^{n+1})$ such that for all $X \in C_c^1(\mathbb{R}^{n+1}; \mathbb{R}^{n+1})$,
$$
\delta V(X) = - \int_{\mathbb{R}^{n+1}} X \cdot H \, d\mu_V.
$$
This vector field $H$ is defined as the [generalized mean curvature](@entry_id:199614) of $V$. A key property is that for $\mu_V$-almost every $x$, $H(x)$ is orthogonal to the approximate tangent plane $T_x M$.

It is a crucial and sometimes subtle point that the existence of a [generalized mean curvature](@entry_id:199614) vector is not guaranteed for all [varifolds](@entry_id:199701). Even for an integral [varifold](@entry_id:194011), the [first variation](@entry_id:174697) $\delta V$ may have a part that is singular with respect to $\mu_V$ (e.g., concentrated on a "boundary"), in which case $H$ is not well-defined as an $L^1_{\text{loc}}$ function. The [absolute continuity](@entry_id:144513) condition $\delta V \ll \mu_V$ is a genuine structural assumption on the [varifold](@entry_id:194011) [@problem_id:3031794] [@problem_id:3031784].

#### The Brakke Inequality

With these definitions in hand, we can define a Brakke flow. A smooth [mean curvature flow](@entry_id:184231) satisfies the evolution equation for its area element $d\mu_t$: $\frac{d}{dt} d\mu_t = -|H|^2 d\mu_t$. To generalize this, Brakke proposed an inequality to account for the possibility of sudden mass loss at singularities.

A **Brakke flow** is a one-parameter family of $n$-dimensional integral [varifolds](@entry_id:199701) $(V_t)_{t \ge 0}$ with corresponding weight measures $\mu_t$, satisfying two conditions for almost every $t \ge 0$:
1.  The [varifold](@entry_id:194011) $V_t$ has a [generalized mean curvature](@entry_id:199614) vector $H(\cdot, t)$ that is square-integrable, i.e., $H(\cdot, t) \in L^2_{\text{loc}}(\mu_t; \mathbb{R}^{n+1})$.
2.  For every non-negative, compactly supported [test function](@entry_id:178872) $\phi \in C_c^1(\mathbb{R}^{n+1})$, the rate of change of the weighted mass $\mu_t(\phi) = \int \phi \, d\mu_t$ satisfies the **Brakke inequality**:
    $$
    D^+ \mu_t(\phi) \le \int_{\mathbb{R}^{n+1}} \left( - \phi |H|^2 + \nabla \phi \cdot H \right) d\mu_t.
    $$
Here, $D^+$ denotes the upper-right Dini derivative, a weak form of the time derivative necessary because $t \mapsto \mu_t(\phi)$ may not be differentiable. The term $-\int \phi |H|^2 \, d\mu_t$ represents the local dissipation of area due to the flow, while the term $\int \nabla \phi \cdot H \, d\mu_t = -\delta V_t(\nabla \phi)$ accounts for the transport of the surface. The inequality $(\le)$ and the restriction to $\phi \ge 0$ are the key features that allow the formulation to model the sudden disappearance of mass at a singularity, a phenomenon where equality would fail [@problem_id:3031795].

### The PDE Formulation: Level-Set Flow

An alternative approach to defining [weak solutions](@entry_id:161732) is to represent the evolving surface $\Gamma_t$ as the zero level set of a higher-dimensional function $u(x, t)$. The evolution of $\Gamma_t$ by [mean curvature](@entry_id:162147) is then translated into a PDE for $u$.

#### The Level-Set Equation

If an $n$-dimensional surface $\Gamma_t$ is the zero [level set](@entry_id:637056) of a [smooth function](@entry_id:158037) $u: \mathbb{R}^{n+1} \times [0, \infty) \to \mathbb{R}$, its unit normal is given by $N = Du/|Du|$ and its [mean curvature](@entry_id:162147) is $H = -\operatorname{div}(Du/|Du|)$. The condition that the normal velocity of the surface equals its [mean curvature vector](@entry_id:199617) translates into the following nonlinear, degenerate parabolic PDE for $u$:
$$
u_t - |Du| \operatorname{div}\left(\frac{Du}{|Du|}\right) = 0.
$$
This is the **[level-set](@entry_id:751248) equation** for [mean curvature flow](@entry_id:184231). Its great advantage is that the level sets of $u$ can merge, split, and change topology without the function $u$ itself becoming singular. However, the solutions to this equation can develop sharp corners in their gradients even from smooth initial data, meaning classical ($C^2$) solutions generally do not exist for all time.

#### Viscosity Solutions

The appropriate notion of a [weak solution](@entry_id:146017) for the [level-set](@entry_id:751248) equation is that of a **[viscosity solution](@entry_id:198358)**. This concept, developed by Crandall, Evans, and Lions, defines a solution not by requiring it to satisfy the PDE directly, but by requiring it to satisfy a [comparison principle](@entry_id:165563) against smooth test functions that touch it from above or below.

Let the operator be $F(p, X) = |p| \operatorname{div}(p/|p|)$, which for $p \neq 0$ can be written as $F(p, X) = \operatorname{tr}\left( \left(I - \frac{p \otimes p}{|p|^2}\right) X \right)$, where $p = Du$ and $X = D^2u$. A continuous function $u$ is a [viscosity solution](@entry_id:198358) of $u_t = F(Du, D^2u)$ if it is both a subsolution and a supersolution.

-   A **viscosity subsolution** requires that for any smooth test function $\phi$ such that $u-\phi$ has a local maximum at $(x_0, t_0)$, the inequality $\phi_t(x_0, t_0) \le F^*(D\phi, D^2\phi)$ holds at that point.
-   A **viscosity supersolution** requires that for any smooth [test function](@entry_id:178872) $\phi$ such that $u-\phi$ has a local minimum at $(x_0, t_0)$, the inequality $\phi_t(x_0, t_0) \ge F_*(D\phi, D^2\phi)$ holds at that point.

Here, $F^*$ and $F_*$ are the upper and lower semicontinuous envelopes of $F$, which handle the singularity at $p=0$. A direct calculation yields:
-   If $D\phi \neq 0$, then $F^* = F_* = F(D\phi, D^2\phi)$.
-   If $D\phi = 0$, the envelopes are determined by the extremal eigenvalues of the Hessian:
    $$
    F^*(0, D^2\phi) = \operatorname{tr}(D^2\phi) - \lambda_{\min}(D^2\phi)
    $$
    $$
    F_*(0, D^2\phi) = \operatorname{tr}(D^2\phi) - \lambda_{\max}(D^2\phi)
    $$
This precise characterization at points of [vanishing gradient](@entry_id:636599) is what allows the theory to uniquely handle the creation (or "fattening") and [annihilation](@entry_id:159364) of [level sets](@entry_id:151155) [@problem_id:3031791].

### Fundamental Properties and Analytic Tools

Both weak formulations admit powerful analytical tools, often generalizations from the smooth setting, which are essential for understanding the behavior of flows near singularities.

#### Huisken's Monotonicity Formula in Weak Settings

One of the most important tools in the study of [mean curvature flow](@entry_id:184231) is **Huisken's [monotonicity formula](@entry_id:203421)**. In the smooth setting, it states that for a flow of [hypersurfaces](@entry_id:159491) $M_t$, the integral of the [backward heat kernel](@entry_id:193390) $\rho_{x_0, t_0}(x, t) = (4\pi(t_0 - t))^{-n/2} \exp(-|x-x_0|^2 / 4(t_0-t))$ over $M_t$ is non-increasing for $t  t_0$:
$$
\frac{d}{dt} \int_{M_t} \rho_{x_0, t_0}(x, t) \, d\mathcal{H}^n(x) \le 0.
$$
This quantity, the **Gaussian density**, measures the area of the surface at a given scale around the space-time point $(x_0, t_0)$. Its monotonicity provides crucial control over the geometry of the flow as it approaches a singularity.

This formula remarkably extends to weak flows:
-   For a **Brakke flow** $\{\mu_t\}$, one can show that the function $t \mapsto \int \rho_{x_0, t_0}(x, t) \, d\mu_t(x)$ is non-increasing. The proof involves a careful approximation argument, since the [heat kernel](@entry_id:172041) itself is not a compactly supported test function admissible in the Brakke inequality. One approximates the kernel with suitable cutoff functions, applies the inequality, and then passes to the limit using tools like the Monotone Convergence Theorem.
-   For a **[level-set](@entry_id:751248) flow**, the connection is made via T. Ilmanen's theory of elliptic regularization. This theory shows how to associate a well-behaved Brakke flow to a [level-set](@entry_id:751248) flow. The [monotonicity](@entry_id:143760) property, being valid for the associated Brakke flow, can then be used to deduce properties of the original [level-set](@entry_id:751248) flow [@problem_id:2979813].

#### The Avoidance Principle

A fundamental property of [mean curvature flow](@entry_id:184231), stemming from the parabolic nature of the governing equation, is the **avoidance principle** (or [comparison principle](@entry_id:165563)): two initially disjoint compact surfaces evolving by mean curvature remain disjoint. This principle can be proven in the weak setting of Brakke flows using the [monotonicity formula](@entry_id:203421).

The argument proceeds by contradiction. Suppose two initially disjoint Brakke flows, $\mu_t^1$ and $\mu_t^2$, first touch at a point $x_0$ at time $\tau$. One considers the superposed flow $\nu_t = \mu_t^1 + \mu_t^2$ and examines the Gaussian density functional $\Phi^{\nu}_{(x_0, \tau)}(t) = \int \rho_{x_0, \tau}(x,t) \, d\nu_t(x)$.
1.  For any time $t  \tau$, because the supports of $\mu_t^1$ and $\mu_t^2$ are disjoint, the value $\Phi^{\nu}_{(x_0, \tau)}(t)$ must be strictly less than 2.
2.  However, at the first contact point $(x_0, \tau)$, the theory of tangent flows implies that the limiting density $\lim_{t \nearrow \tau} \Phi^{\nu}_{(x_0, \tau)}(t)$ must be at least 2 (at least 1 from each flow).
These two facts contradict the non-increasing nature of $t \mapsto \Phi^{\nu}_{(x_0, \tau)}(t)$. Thus, a first contact is impossible. This elegant argument showcases the power of the [monotonicity formula](@entry_id:203421) as a tool for controlling the global behavior of weak flows [@problem_id:3027481].

### Singularities, Fattening, and the Mean-Convexity Condition

The [level-set](@entry_id:751248) formulation, while providing [existence and uniqueness of solutions](@entry_id:177406), can sometimes produce behaviors that are considered unphysical. One such behavior is "fattening".

#### The Phenomenon of Fattening

The evolving front in a [level-set](@entry_id:751248) flow is the zero set $K_t = \{x : u(x,t)=0\}$. **Fattening** is said to occur if, for some $t_0  0$, the set $K_{t_0}$ develops a non-empty interior. This means the "surface" momentarily becomes a region of positive volume where $u$ is identically zero.

A canonical example exhibiting this behavior is the evolution starting from two tangent closed disks in $\mathbb{R}^2$. At the [point of tangency](@entry_id:172885), the notion of a unique evolution breaks down. One can approximate the initial data with two slightly separated disks (leading to a subsolution where they shrink apart) or with a single, smoothly connected "peanut" shape (leading to a supersolution that stays connected). The true [viscosity solution](@entry_id:198358) must lie between these, which forces the zero set to fill the region between the two bracketing evolutions, thereby creating an open set where $u(x,t)=0$ for small $t  0$ [@problem_id:3033521].

#### Non-Fattening of Mean-Convex Flows: A Bridge Between Formulations

Fattening is often undesirable, as we typically want our weak flow to represent a moving hypersurface (a set of codimension one). A large and geometrically important class of surfaces for which fattening is precluded are **[mean-convex](@entry_id:193370)** surfaces—those whose [mean curvature vector](@entry_id:199617) (with respect to the inward normal) is non-negative.

A cornerstone result in the theory, primarily due to T. Ilmanen and G. Huisken, states that the [level-set](@entry_id:751248) flow of a [mean-convex](@entry_id:193370) initial surface does not fatten. This holds even as the flow passes through singularities, such as the neck-pinch of a dumbbell shape. The proof of this theorem provides a beautiful bridge between the [level-set](@entry_id:751248) and Brakke formulations.

The argument, in essence, is that for [mean-convex](@entry_id:193370) initial data, the weak flow is unique across different definitions. One can construct a weak flow using GMT, known as the **flow by minimizing hulls**, which by construction consists of a nested family of sets whose boundaries form a non-fattening Brakke flow. The core of the proof is to show that this GMT-based flow coincides with the one given by the [level-set method](@entry_id:165633). Since the minimizing hull flow does not fatten, the [level-set](@entry_id:751248) flow cannot either. This identification relies on the avoidance principle and sophisticated barrier arguments, showing that the "inner" and "outer" approximations of the [level-set](@entry_id:751248) flow are both trapped by the same unique minimizing hull evolution [@problem_id:3027454] [@problem_id:3033521]. This result not only provides a crucial regularity property for an important class of flows but also demonstrates a deep consistency between the PDE and measure-theoretic viewpoints.