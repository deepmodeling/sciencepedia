## Introduction
In the vast landscape of dynamics and mechanics, the quest to find the "best" path—one that minimizes time, energy, or some other cost—is a fundamental challenge. Geometric [optimal control](@entry_id:138479) offers a profoundly elegant and powerful framework to tackle this problem, recasting it in the language of differential geometry and Hamiltonian systems. At the heart of this approach lies the control Hamiltonian, a function that encodes the system's dynamics, cost, and controls into a single, unifying object. This article addresses the core principles of this theory, bridging the gap between abstract mathematical structure and concrete, solvable problems.

This article will guide you through the theory and application of the control Hamiltonian and the [extremal curves](@entry_id:1124800) it generates. We will begin in the first chapter, **Principles and Mechanisms**, by introducing the Pontryagin Maximum Principle and establishing how [extremal curves](@entry_id:1124800) emerge as the flow of a Hamiltonian vector field. We then move to **Applications and Interdisciplinary Connections**, where we will witness the theory's power in action, solving problems in [time-optimal control](@entry_id:167123), uncovering deep links to sub-Riemannian geometry, and leveraging symmetries to simplify complex systems. Finally, in **Hands-On Practices**, you will have the opportunity to apply these concepts to challenging problems, solidifying your understanding and developing practical skills in geometric control.

## Principles and Mechanisms

This chapter delves into the core principles of [geometric optimal control](@entry_id:1125608), focusing on the central role of the control Hamiltonian. We will develop the necessary conditions for optimality as articulated by the Pontryagin Maximum Principle (PMP) and explore how these conditions give rise to [extremal curves](@entry_id:1124800). These curves are not arbitrary paths but are endowed with a rich geometric structure, as they represent the flow of a specific Hamiltonian vector field on [the cotangent bundle](@entry_id:185138) of the system's configuration manifold. We will dissect the structure of these extremal trajectories, from smooth solutions to more complex bang-bang and [singular arcs](@entry_id:264308), and establish the crucial role of [transversality conditions](@entry_id:176091) in selecting the physically relevant solution. Finally, we will venture into advanced topics, including [state constraints](@entry_id:271616) and [second-order conditions](@entry_id:635610) for optimality, which connect the theory to the frontiers of Poisson geometry and Riemannian geometry.

### The Control Hamiltonian and Pontryagin's Principle

An [optimal control](@entry_id:138479) problem is fundamentally concerned with steering a dynamical system to achieve a certain objective while minimizing a specified cost. In the language of [geometric mechanics](@entry_id:169959), a control system is defined on a configuration manifold $Q$ of dimension $n$. Its state is a point $q \in Q$, and its evolution is governed by a first-order differential equation:
$$
\dot{q}(t) = f(q(t), u(t))
$$
where $u(t)$ is the control input, taking values in a control set $U \subseteq \mathbb{R}^m$. The objective is to minimize a [cost functional](@entry_id:268062), typically of the Bolza form:
$$
J(u) = \Phi(q(T)) + \int_{0}^{T} L(q(t), u(t)) dt
$$
Here, $L: TQ \times U \to \mathbb{R}$ is the **running cost** or Lagrangian, $\Phi: Q \to \mathbb{R}$ is the **terminal cost**, and $[0, T]$ is the time horizon.

The cornerstone of modern [optimal control](@entry_id:138479) theory is the **Pontryagin Maximum Principle (PMP)**. This principle reframes the variational problem in a Hamiltonian setting. We introduce **[costate variables](@entry_id:636897)** (or adjoint variables) $p(t)$, which are [covectors](@entry_id:157727) residing in the [cotangent space](@entry_id:270516) $T^*_{q(t)}Q$. The pair $(q(t), p(t))$ defines a curve in the cotangent bundle $T^*Q$. The central object of the PMP is the **control Hamiltonian**, $H_u$, defined on the Pontryagin bundle $T^*Q \times U$:
$$
H_u(q, p) = \langle p, f(q, u) \rangle - p_0 L(q, u)
$$
where $\langle p, v \rangle$ denotes the natural pairing between a [covector](@entry_id:150263) $p \in T^*_qQ$ and a [tangent vector](@entry_id:264836) $v \in T_qQ$. The constant $p_0$ is a scalar that is either $0$ or $-1$.

The Pontryagin Maximum Principle provides a set of necessary conditions for a control $u^*(t)$ and its corresponding state trajectory $q^*(t)$ to be optimal. It asserts that if $(q^*(t), u^*(t))$ is an optimal pair, then there exists a non-zero [costate](@entry_id:276264) curve $p(t)$ and a constant $p_0 \in \{0, -1\}$ such that:

1.  **Maximization Condition:** For almost all $t \in [0, T]$, the [optimal control](@entry_id:138479) $u^*(t)$ maximizes the Hamiltonian:
    $$
    H_{u^*(t)}(q^*(t), p(t)) = \max_{v \in U} H_v(q^*(t), p(t))
    $$

2.  **Hamiltonian Dynamics:** The state and [costate variables](@entry_id:636897) evolve according to a set of differential equations governed by this Hamiltonian, which we will detail in the next section.

The case $p_0 = -1$ is known as the **normal case**, and the resulting trajectories are called **normal extremals**. Most problems of physical interest fall into this category. The case $p_0 = 0$ is the **abnormal case**, leading to **abnormal extremals**. These are often associated with pathological situations or underlying geometric constraints in the system dynamics. Unless stated otherwise, we will assume the normal case, setting $p_0=-1$, so the Hamiltonian is $H_u(q, p) = \langle p, f(q, u) \rangle - L(q, u)$.

### Extremals as Hamiltonian Flow

The maximization condition of the PMP implicitly defines the optimal control $u^*(t)$ at each instant as a function of the state $q^*(t)$ and [costate](@entry_id:276264) $p(t)$. By substituting this maximizing control back into the control Hamiltonian, we obtain the **maximized Hamiltonian** (or true Hamiltonian), a function solely on [the cotangent bundle](@entry_id:185138) $T^*Q$:
$$
H(q, p) = \max_{v \in U} \left( \langle p, f(q, v) \rangle - L(q, v) \right)
$$
The profound insight of the geometric formulation is that the optimal trajectories $(q^*(t), p(t))$, known as **[extremal curves](@entry_id:1124800)** or **extremals**, are precisely the [integral curves](@entry_id:161858) of the Hamiltonian vector field $X_H$ generated by this maximized Hamiltonian $H$ on the symplectic manifold $(T^*Q, \omega)$, where $\omega$ is the canonical symplectic two-form.

In [canonical coordinates](@entry_id:175654) $(q_1, \dots, q_n, p_1, \dots, p_n)$ on $T^*Q$, the symplectic form is $\omega = \sum_{i=1}^n dq_i \wedge dp_i$. The Hamiltonian vector field $X_H$ is uniquely defined by the relation $\iota_{X_H}\omega = dH$, where $\iota$ is the [interior product](@entry_id:158127) and $d$ is the exterior derivative. This compact geometric statement unpacks into the familiar **Hamilton's equations**:
$$
\dot{q}_i = \frac{\partial H}{\partial p_i}, \qquad \dot{p}_i = - \frac{\partial H}{\partial q_i}
$$
The first set of equations, $\dot{q} = \partial H / \partial p$, reproduces the system dynamics with the optimal control inserted. The second set, $\dot{p} = -\partial H / \partial q$, governs the evolution of the costate, often called the adjoint dynamics.

A clear illustration of this framework is provided by the [time-optimal control](@entry_id:167123) of a double integrator system . The [system dynamics](@entry_id:136288) are $\dot{q} = v$ and $\dot{v}=u$, where $q$ is position, $v$ is velocity, and $u$ is a bounded control $|u| \le U$. The goal is to minimize time, so the running cost is $L=1$. The normal control Hamiltonian on $T^*\mathbb{R}^2$ with coordinates $(q,v,p_q,p_v)$ is $H_u = p_q v + p_v u - 1$. The maximization of $H_u$ with respect to $u$ depends only on the term $p_v u$, yielding the optimal control $u^* = U \cdot \text{sgn}(p_v)$. Substituting this back gives the maximized Hamiltonian $H = p_q v + U|p_v| - 1$. The extremal dynamics are then given by Hamilton's equations for this $H$. The resulting trajectories for $(q,v)$ are piecewise parabolic arcs, corresponding to periods of maximum acceleration or deceleration.

### Structure of Extremal Controls

The nature of the [optimal control](@entry_id:138479) law $u^*(q,p)$ depends critically on how the control variable $u$ enters the Hamiltonian. This leads to a classification of extremal structures.

#### Smooth Controls from Concave Hamiltonians

Consider a system where the control $u$ is unconstrained ($U = \mathbb{R}^m$) and the Hamiltonian $H_u$ is a strictly [concave function](@entry_id:144403) of $u$. A common example is the Linear-Quadratic Regulator (LQR), where the dynamics are linear, $\dot{x} = Ax+Bu$, and the cost is quadratic, $L(x,u) = \frac{1}{2}x^\top Q x + \frac{1}{2}u^\top R u$, with $R$ positive definite. The Hamiltonian is:
$$
H_u(x,p,u) = p^\top(Ax+Bu) - \frac{1}{2}x^\top Q x - \frac{1}{2}u^\top R u
$$
Since $H_u$ is strictly concave in $u$, the unique maximizing control is found by the first-order [stationarity condition](@entry_id:191085) $\partial H_u / \partial u = 0$. This yields:
$$
B^\top p - Ru = 0 \implies u^*(p) = R^{-1}B^\top p
$$
The [optimal control](@entry_id:138479) is a smooth, linear function of the [costate](@entry_id:276264). From a more abstract geometric perspective , the [stationarity condition](@entry_id:191085) $\partial H_u / \partial u = 0$ defines a **primary constraint [submanifold](@entry_id:262388)** within the Pontryagin bundle $T^*Q \times U$. The **presymplectic constraint algorithm** then ensures that the Hamiltonian flow is tangent to this [submanifold](@entry_id:262388), effectively reducing the dynamics to the symplectic manifold $T^*Q$ with a reduced Hamiltonian obtained by substituting $u^*(p)$. For the LQR problem, this yields a linear Hamiltonian system for $(x,p)$, whose solution provides the optimal state and [costate](@entry_id:276264) trajectories.

#### Bang-Bang and Singular Controls

For many systems, particularly in time-optimal or fuel-optimal problems, the control enters the Hamiltonian linearly. Such systems are called **control-affine**, with dynamics $\dot{q} = f_0(q) + \sum_{j=1}^m u_j f_j(q)$. If the control is subject to bounds, for instance $|u_j| \le 1$, the Hamiltonian takes the form:
$$
H_u(q, p) = \langle p, f_0(q) \rangle - L(q) + \sum_{j=1}^m u_j \langle p, f_j(q) \rangle
$$
The maximization over $u_j$ only involves the term $u_j \langle p, f_j(q) \rangle$. The coefficient of the control, $\sigma_j(q,p) = \langle p, f_j(q) \rangle$, is known as the **switching function**. The maximizing control law is determined by the sign of this function:
$$
u_j^*(t) = \text{sgn}(\sigma_j(q(t), p(t)))
$$
This type of control, which discontinuously switches between the boundaries of the control set (e.g., $+1$ and $-1$), is called **[bang-bang control](@entry_id:261047)**. As seen in the double integrator problem , this leads to trajectories that are pieced together from segments corresponding to constant control values.

A more complex situation arises if a switching function vanishes identically over a finite time interval, $\sigma_j(t) \equiv 0$. In this case, the PMP provides no information about the [optimal control](@entry_id:138479) from the maximization condition alone. Such a trajectory segment is called a **[singular arc](@entry_id:167371)**. To determine the control on a [singular arc](@entry_id:167371), one must compute successive time derivatives of the switching function, $\dot{\sigma}_j, \ddot{\sigma}_j, \dots$, along the extremal trajectory until the control $u$ appears explicitly. The condition that the derivative must also be zero, $\frac{d^k \sigma_j}{dt^k} \equiv 0$, is then used to solve for the **[singular control](@entry_id:166459)**, $u_s$.

For example, consider the system $\dot{x}_1 = u$, $\dot{x}_2 = x_1 + u x_2$ with control $u \in [-1,1]$ . The switching function is $\sigma(t) = p_1(t) + p_2(t)x_2(t)$. A [singular arc](@entry_id:167371) requires $\sigma(t) \equiv 0$. Its first time derivative along the extremal flow is found to be $\dot{\sigma}(t) = p_2(t)(x_1(t)-1)$. For a [singular arc](@entry_id:167371), we must also have $\dot{\sigma}(t) \equiv 0$. Assuming a non-trivial costate ($p_2 \not\equiv 0$), this implies the state is constrained to $x_1(t) \equiv 1$ on the [singular arc](@entry_id:167371). The control still does not appear. The second derivative is $\ddot{\sigma}(t) = u(t)p_2(t)(2-x_1(t))$. The condition $\ddot{\sigma}(t) \equiv 0$, combined with $x_1 \equiv 1$, yields $u_s(t)p_2(t)(2-1)=0$, which forces the [singular control](@entry_id:166459) to be $u_s(t)=0$.

### Transversality Conditions at the Boundary

Hamilton's equations generate a family of [extremal curves](@entry_id:1124800) filling the cotangent bundle. To identify the unique optimal trajectory for a specific problem, one must impose boundary conditions. While initial conditions like a fixed starting state $q(0)=q_0$ are straightforward, the conditions at the terminal time $T$ are more subtle and are known as **[transversality conditions](@entry_id:176091)**. They depend on the nature of the terminal cost and constraints.

-   **Fixed Terminal State and Time:** If both $q(T)$ and $T$ are fixed, no additional conditions are needed for the costate $p(T)$.

-   **Free Terminal State:** If the terminal state $q(T)$ is free and there is a terminal cost $\Phi(q(T))$, the [transversality condition](@entry_id:261118) is:
    $$
    p(T) = d\Phi(q(T)) \quad \left(\text{in coordinates, } p_i(T) = \frac{\partial \Phi}{\partial q_i}(q(T))\right)
    $$
    If there is no terminal cost ($\Phi=0$), this simplifies to $p(T)=0$. This condition was used to solve the LQR problem in .

-   **Free Terminal Time:** If the terminal time $T$ is free, the [transversality condition](@entry_id:261118) relates to the value of the maximized Hamiltonian at the end of the trajectory:
    $$
    H(q(T), p(T)) = -\frac{\partial \Phi}{\partial t}(q(T), T)
    $$
    If the terminal cost does not explicitly depend on time, this simplifies to the important condition $H(q(T), p(T)) = 0$. For time-optimal problems where $L=1$ and $\Phi=0$, this means the Hamiltonian is identically zero along the entire extremal.

-   **Terminal State on a Submanifold:** If the terminal state is constrained to lie on a submanifold defined by $g(q(T))=0$, we introduce a Lagrange multiplier vector $\nu$ and form an augmented terminal cost $\tilde{\Phi}(q) = \Phi(q) + \nu^\top g(q)$. The [transversality condition](@entry_id:261118) for the momentum becomes:
    $$
    p(T) = d\tilde{\Phi}(q(T)) = d\Phi(q(T)) + \nu^\top dg(q(T))
    $$
    These conditions are powerful tools. For instance, in a problem with a free final time $T$ and a terminal state constrained to $q(T)-c=0$ , one can combine the time [transversality condition](@entry_id:261118) $H(T)=0$ with the momentum [transversality condition](@entry_id:261118) $p(T)=\alpha q(T) + \nu$ (derived from a cost $\Phi=\frac{\alpha}{2}q^2$) to explicitly solve for the Lagrange multiplier $\nu$. The calculation yields $p(T)=0$ from the Hamiltonian condition, which, when substituted into the momentum condition along with $q(T)=c$, gives $\nu = -\alpha c$.

### Advanced Topics: Constraints and Second-Order Conditions

While the PMP provides powerful necessary conditions for optimality, a deeper understanding requires exploring the geometric structures underlying [state constraints](@entry_id:271616) and investigating [second-order conditions](@entry_id:635610) that distinguish minimizing trajectories from other extremals.

#### State Constraints and Coisotropic Reduction

When the state and [costate](@entry_id:276264) are required to evolve on a specific [submanifold](@entry_id:262388) $C \subset T^*Q$, the dynamics must be compatible with this constraint. A particularly elegant situation occurs when the constraint submanifold is **coisotropic**. A [submanifold](@entry_id:262388) $C$ defined by constraint functions $\phi_a(q,p)=0$ is coisotropic if the ideal of functions vanishing on $C$ is closed under the canonical Poisson bracket. This is equivalent to requiring $\{\phi_a, \phi_b\}|_C = 0$ for all pairs of constraint functions, where $\{\cdot, \cdot\}$ is the Poisson bracket.

If $C$ is coisotropic, the Hamiltonian flow generated by any function that is constant on the characteristic leaves of $C$ will be tangent to $C$. In the context of control, if we can find a reduced Hamiltonian $H_{red}$ on $C$, its flow will automatically respect the constraints. This process is known as **[coisotropic reduction](@entry_id:1122620)**.

A problem might impose such constraints explicitly , for instance, by requiring the extremals of a [harmonic oscillator](@entry_id:155622) system to satisfy $p_2 + \alpha q_1 = 0$ and $p_1 + \alpha q_2 = 0$. One can first verify that this constraint [submanifold](@entry_id:262388) is coisotropic by computing the Poisson bracket of the constraint functions, which vanishes identically. Then, one derives the minimized Hamiltonian $H_{\min}(q,p)$ using the PMP as usual. Finally, this Hamiltonian is restricted to the constraint [submanifold](@entry_id:262388) by substituting the [constraint equations](@entry_id:138140) (e.g., expressing $p$ in terms of $q$), yielding a **reduced Hamiltonian** $H_{red}(q)$ that describes the dynamics on the constrained phase space.

#### Second-Order Optimality and Jacobi Fields

The PMP only provides [first-order necessary conditions](@entry_id:170730). An extremal curve may correspond to a [local minimum](@entry_id:143537), a [local maximum](@entry_id:137813), or a saddle point of the [cost functional](@entry_id:268062). To distinguish a true minimum, one must analyze the second variation of the cost. This connects optimal control to the classical [calculus of variations](@entry_id:142234) and the geometry of the underlying manifold.

Consider the fundamental problem of minimizing kinetic energy, $\mathcal{J} = \frac{1}{2} \int_0^T g(\dot{q}, \dot{q}) dt$, on a Riemannian manifold $(M,g)$ . The PMP extremals for this problem are precisely the **geodesics** of the manifold. A geodesic is a locally shortest path, but only for a limited duration.

The local optimality of a geodesic is determined by the definiteness of the second variation of the energy functional. The key to analyzing this are **Jacobi fields**. A Jacobi field $J(t)$ along a geodesic $\gamma(t)$ can be thought of as a vector field describing the [infinitesimal displacement](@entry_id:202209) between $\gamma(t)$ and a nearby geodesic. It is the solution to the **Jacobi equation**:
$$
\nabla_{\dot{\gamma}}\nabla_{\dot{\gamma}}J + R(J, \dot{\gamma})\dot{\gamma} = 0
$$
where $\nabla$ is the Levi-Civita connection and $R$ is the Riemann [curvature tensor](@entry_id:181383).

A point $\gamma(T)$ is **conjugate** to the starting point $\gamma(0)$ if there exists a non-trivial Jacobi field $J(t)$ along $\gamma$ such that $J(0)=0$ and $J(T)=0$. The fundamental result of Morse theory states that a geodesic segment $\gamma([0,T])$ ceases to be locally minimizing if $T$ is greater than or equal to the first conjugate time. At the first conjugate time, the second variation of the energy becomes singular, losing its [positive definiteness](@entry_id:178536).

For a manifold of constant [positive sectional curvature](@entry_id:193532) $K$, such as a sphere, the Jacobi equation for a normal Jacobi field $J(t)$ simplifies to the harmonic oscillator equation $\ddot{y}(t) + Ky(t)=0$, where $y(t)$ is the magnitude of $J(t)$ in a parallel-transported frame. The condition for a conjugate point, $y(0)=0$ and $y(T)=0$, is satisfied for the first time when $\sqrt{K}T = \pi$. Thus, the first conjugate time is $T_{\text{conj}} = \pi / \sqrt{K}$ . This means that on a sphere of radius $R$ (where $K=1/R^2$), a geodesic (a [great circle](@entry_id:268970) arc) is the shortest path only until it reaches the antipodal point, a distance of $\pi R$.