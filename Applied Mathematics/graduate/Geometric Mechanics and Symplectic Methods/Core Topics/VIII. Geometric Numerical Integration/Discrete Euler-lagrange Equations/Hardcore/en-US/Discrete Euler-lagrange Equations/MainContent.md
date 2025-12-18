## Introduction
In the numerical simulation of physical systems, long-term accuracy and stability are paramount. Standard numerical methods often introduce artificial energy drift, causing simulations to become unphysical over time. The solution lies in a class of algorithms known as variational or [geometric integrators](@entry_id:138085), which are designed to respect the fundamental geometric structure of the underlying physics. At the heart of this modern approach to computational mechanics are the Discrete Euler-Lagrange (DEL) equations, which reformulate dynamics through a discrete version of Hamilton's Principle of Stationary Action. This article addresses the knowledge gap between standard numerical recipes and these powerful [structure-preserving methods](@entry_id:755566).

Across three chapters, this article provides a graduate-level introduction to the theory and application of [discrete variational mechanics](@entry_id:1123832). The first chapter, "Principles and Mechanisms," will guide you through the first-principles derivation of the DEL equations, exploring their profound geometric consequences, including symplecticity and the discrete Noether's theorem for conservation laws. The subsequent chapter, "Applications and Interdisciplinary Connections," will demonstrate how this framework is used to build robust integrators for a vast range of real-world problems in robotics, molecular dynamics, control theory, and even [classical field theory](@entry_id:149475). Finally, in "Hands-On Practices," you will solidify your understanding by tackling practical exercises, from deriving famous integrators like Störmer-Verlet to benchmarking methods on [chaotic systems](@entry_id:139317).

## Principles and Mechanisms

The formulation of mechanics through [variational principles](@entry_id:198028), such as Hamilton's Principle of Stationary Action, offers profound insights into the geometric structure of dynamics. Variational integrators extend this philosophy to the realm of numerical computation by constructing algorithms directly from a discretized version of Hamilton's principle. This approach ensures that the resulting numerical methods inherit fundamental structural properties of the continuous system, such as symplecticity and [momentum conservation](@entry_id:149964), leading to exceptional long-term fidelity and stability. This chapter elucidates the derivation of the core equations of [discrete variational mechanics](@entry_id:1123832)—the Discrete Euler-Lagrange equations—and explores their profound geometric consequences.

### The Principle of Stationary Discrete Action

The foundation of [variational integration](@entry_id:1133722) lies in replacing the continuous [action integral](@entry_id:156763) with a discrete sum. Let the configuration of a mechanical system be described by coordinates $q$ on a smooth, finite-dimensional configuration manifold $Q$. A continuous trajectory is a curve $q: [t_0, t_N] \to Q$. In the discrete setting, we represent this trajectory by a sequence of points $\{q_k\}_{k=0}^N$ in $Q$, where $q_k$ approximates the configuration at time $t_k = t_0 + kh$ for a fixed time step $h > 0$.

The continuous action is the integral of the Lagrangian $L(q, \dot{q})$ along a path. Its discrete counterpart is constructed from a **discrete Lagrangian**, $L_d: Q \times Q \times \mathbb{R}_{>0} \to \mathbb{R}$. This function, $L_d(q_k, q_{k+1}; h)$, is designed to approximate the [action integral](@entry_id:156763) over a single time step from $t_k$ to $t_{k+1}$:
$$
L_d(q_k, q_{k+1}; h) \approx \int_{t_k}^{t_{k+1}} L(q(t), \dot{q}(t)) \, dt
$$
where $q(t)$ is a path segment connecting $q_k$ and $q_{k+1}$. The total **discrete action**, $S_d$, for the path $\{q_k\}_{k=0}^N$ is the sum of these contributions over all segments:
$$
S_d[\{q_k\}_{k=0}^N] = \sum_{k=0}^{N-1} L_d(q_k, q_{k+1}; h)
$$
The dynamics are then determined by the **discrete principle of stationary action**, which posits that the discrete trajectory followed by the system is one that renders the discrete action $S_d$ stationary with respect to variations of the interior points of the path. Consider a variation of the path, $\{\delta q_k\}_{k=0}^N$, where each $\delta q_k$ is a tangent vector in $T_{q_k}Q$. For a fixed-endpoint problem, these variations must vanish at the boundaries: $\delta q_0 = 0$ and $\delta q_N = 0$.

The [stationarity condition](@entry_id:191085) is $\delta S_d = 0$. To derive the consequences of this condition, we compute the [first variation](@entry_id:174697) of the action:
$$
\delta S_d = \delta \sum_{k=0}^{N-1} L_d(q_k, q_{k+1}; h) = \sum_{k=0}^{N-1} \delta L_d(q_k, q_{k+1}; h)
$$
Using the [chain rule](@entry_id:147422), the variation of a single term is:
$$
\delta L_d(q_k, q_{k+1}; h) = \langle D_1 L_d(q_k, q_{k+1}; h), \delta q_k \rangle + \langle D_2 L_d(q_k, q_{k+1}; h), \delta q_{k+1} \rangle
$$
Here, $D_1 L_d$ and $D_2 L_d$ denote the [partial derivatives](@entry_id:146280) of $L_d$ with respect to its first and second arguments on $Q$, respectively. Summing these variations yields:
$$
\delta S_d = \sum_{k=0}^{N-1} \left( \langle D_1 L_d(q_k, q_{k+1}; h), \delta q_k \rangle + \langle D_2 L_d(q_k, q_{k+1}; h), \delta q_{k+1} \rangle \right)
$$
To group terms by the variation $\delta q_k$, we perform a discrete "[summation by parts](@entry_id:139432)" by re-indexing the second part of the sum. Letting $j=k+1$ in the second sum and then renaming the index back to $k$, we find:
$$
\delta S_d = \sum_{k=0}^{N-1} \langle D_1 L_d(q_k, q_{k+1}; h), \delta q_k \rangle + \sum_{k=1}^{N} \langle D_2 L_d(q_{k-1}, q_k; h), \delta q_k \rangle
$$
We now separate the boundary terms ($k=0$ and $k=N$) from the interior terms ($k=1, \dots, N-1$). The fixed-endpoint conditions $\delta q_0 = 0$ and $\delta q_N = 0$ ensure that the boundary terms vanish . This leaves a sum over the interior points:
$$
\delta S_d = \sum_{k=1}^{N-1} \left( \langle D_1 L_d(q_k, q_{k+1}; h) + D_2 L_d(q_{k-1}, q_k; h), \delta q_k \rangle \right)
$$
For the action to be stationary, this expression must be zero for *arbitrary* independent variations $\delta q_k$ at the interior points. By the fundamental lemma of [calculus of variations](@entry_id:142234), this implies that the coefficient of each $\delta q_k$ must be the zero [covector](@entry_id:150263). This yields the **Discrete Euler-Lagrange (DEL) equations**:
$$
D_1 L_d(q_k, q_{k+1}; h) + D_2 L_d(q_{k-1}, q_k; h) = 0, \quad \text{for } k=1, \dots, N-1.
$$
This set of equations provides a rule for determining the evolution of the system from one step to the next. Notice that the equation at index $k$ involves the points $q_{k-1}, q_k,$ and $q_{k+1}$, making it a second-order [difference equation](@entry_id:269892) on the configuration manifold $Q$ .

### Geometric Structure of the DEL Equations

A crucial aspect of this formulation, often missed in a purely coordinate-based derivation, is its intrinsic geometric meaning. The derivatives $D_1 L_d$ and $D_2 L_d$ are not just collections of [partial derivatives](@entry_id:146280); they are [covectors](@entry_id:157727). Specifically:
- $D_1 L_d(q_k, q_{k+1}; h)$ is the partial derivative of $L_d$ with respect to its first argument, which is a point on $Q$. This derivative is a linear map on [tangent vectors](@entry_id:265494) at $q_k$, meaning it is an element of the [cotangent space](@entry_id:270516) $T_{q_k}^*Q$.
- $D_2 L_d(q_{k-1}, q_k; h)$ is the partial derivative of $L_d$ with respect to its second argument. This derivative is evaluated at the pair $(q_{k-1}, q_k)$, but the differentiation is with respect to the second argument, $q_k$. Thus, it is also a [covector](@entry_id:150263) in the [cotangent space](@entry_id:270516) $T_{q_k}^*Q$.

Since both terms in the DEL equation, $D_1 L_d(q_k, q_{k+1}; h)$ and $D_2 L_d(q_{k-1}, q_k; h)$, reside in the *same* vector space $T_{q_k}^*Q$, their sum is a well-defined operation on the manifold, independent of any choice of coordinates. The DEL equation is a statement that a specific sum of two [covectors](@entry_id:157727) at the point $q_k$ equals the zero covector . This coordinate-free perspective is fundamental to understanding the geometric properties of the resulting integrators.

The DEL equation implicitly defines the update map $(q_{k-1}, q_k) \mapsto q_{k+1}$. For this map to be well-defined and unique, we must be able to solve for $q_{k+1}$ given its predecessors. Let us define a function $F(x, y, z) = D_1 L_d(y, z) + D_2 L_d(x, y)$, where $(x, y, z)$ corresponds to $(q_{k-1}, q_k, q_{k+1})$. The DEL equation is $F(q_{k-1}, q_k, q_{k+1}) = 0$. By the **Implicit Function Theorem**, we can locally solve for $q_{k+1}$ as a [smooth function](@entry_id:158037) of $(q_{k-1}, q_k)$ if the Jacobian of $F$ with respect to its third argument, $z=q_{k+1}$, is invertible. In [local coordinates](@entry_id:181200), this Jacobian matrix is precisely the matrix of mixed [second partial derivatives](@entry_id:635213), $D_{12}L_d(q_k, q_{k+1})$. Therefore, the condition for a unique, smooth update map is that the discrete Lagrangian must be **non-degenerate**, meaning the matrix $D_{12}L_d$ is invertible . This is the discrete analogue of the regularity condition for a continuous Lagrangian.

### Symplecticity and the Discrete Legendre Transform

The most celebrated property of [variational integrators](@entry_id:174311) is that they are **symplectic**. This means they exactly preserve the canonical symplectic 2-form on the phase space ([the cotangent bundle](@entry_id:185138) $T^*Q$), which has profound consequences for the qualitative long-term behavior of the numerical solution. To see this, we transition from the Lagrangian picture on $Q \times Q$ to the Hamiltonian picture on $T^*Q$ using the **discrete Legendre transforms**.

For each segment $(q_k, q_{k+1})$, we define two sets of momenta, corresponding to the left and right endpoints of the interval:
$$
p_k^- := -D_1 L_d(q_k, q_{k+1}; h)
$$
$$
p_{k+1}^+ := D_2 L_d(q_k, q_{k+1}; h)
$$
These definitions map a pair of configurations $(q_k, q_{k+1}) \in Q \times Q$ to a pair of phase space points, $(q_k, p_k^-) \in T^*Q$ and $(q_{k+1}, p_{k+1}^+) \in T^*Q$ . The sign convention for $p_k^-$ is chosen to align with the boundary terms that arise in the variation of the continuous action.

With these definitions, the DEL equation, $D_1 L_d(q_k, q_{k+1}; h) + D_2 L_d(q_{k-1}, q_k; h) = 0$, can be rewritten. The term $D_2 L_d(q_{k-1}, q_k; h)$ defines the momentum $p_k^+$ at the end of the $[k-1, k]$ interval. The term $D_1 L_d(q_k, q_{k+1}; h)$ defines the momentum $-p_k^-$ at the start of the $[k, k+1]$ interval. The DEL equation thus becomes:
$$
-p_k^- + p_k^+ = 0 \quad \implies \quad p_k^- = p_k^+
$$
This elegant result, known as **momentum matching**, shows that the DEL equation simply enforces continuity of momentum across the junction at $q_k$ .

The one-step update map on phase space, $\tilde{F}_h: (q_k, p_k) \mapsto (q_{k+1}, p_{k+1})$, is implicitly defined by the pair of Legendre transform equations:
$$
p_k = -D_1 L_d(q_k, q_{k+1}; h)
$$
$$
p_{k+1} = D_2 L_d(q_k, q_{k+1}; h)
$$
The non-degeneracy condition on $L_d$ ensures that the first equation can be inverted to find $q_{k+1}$ given $(q_k, p_k)$, making the map $\tilde{F}_h$ well-defined.

To prove that this map is symplectic, we consider the total differential of the discrete Lagrangian, viewed as a function of its two arguments, $q_k$ and $q_{k+1}$:
$$
dL_d = \langle D_1 L_d, dq_k \rangle + \langle D_2 L_d, dq_{k+1} \rangle
$$
Substituting the momentum definitions, we find a remarkable relationship:
$$
dL_d = -\langle p_k, dq_k \rangle + \langle p_{k+1}, dq_{k+1} \rangle
$$
This shows that the 1-form $\langle p_{k+1}, dq_{k+1} \rangle - \langle p_k, dq_k \rangle$ is exact; it is the differential of the scalar function $L_d$. In coordinate-free notation, this is $\theta_{k+1} - \theta_k = dL_d$, where $\theta = p_i dq^i$ is the canonical 1-form on $T^*Q$. Taking the exterior derivative of this relation and using the fact that $d(d L_d) = 0$ for any function $L_d$, we get:
$$
d(\theta_{k+1} - \theta_k) = 0 \quad \implies \quad d\theta_{k+1} - d\theta_k = 0
$$
Since the canonical symplectic 2-form is defined as $\omega = -d\theta = dq \wedge dp$, this implies $\omega_{k+1} = \omega_k$. In terms of the map $\tilde{F}_h$, this is $\tilde{F}_h^* \omega = \omega$, which is the definition of a symplectic map. This proof reveals that the discrete Lagrangian acts as a **Type 1 [generating function](@entry_id:152704)** for the symplectic map $\tilde{F}_h$. Crucially, this proof holds for any fixed time step $h>0$; symplecticity is an exact structural property of the integrator, not an approximate one that holds only in the limit $h \to 0$  .

### Accuracy and Consistency

While a variational integrator is exactly symplectic for any time step $h$, its accuracy as a numerical method depends critically on how well the discrete Lagrangian $L_d$ approximates the true physics. The ideal benchmark for this is the **exact discrete Lagrangian**, $L_d^E(q_0, q_1; h)$, defined as the action of the true solution of the Euler-Lagrange equations that connects $q_0$ to $q_1$ in time $h$:
$$
L_d^E(q_0, q_1; h) := \int_0^h L(q_{sol}(t), \dot{q}_{sol}(t)) dt, \quad \text{where } q_{sol}(0)=q_0, q_{sol}(h)=q_1
$$
A key result is that if one could use $L_d^E$, the discrete Legendre transforms would yield momenta that are identical to the continuous momenta of the exact solution at the endpoints of the interval .

In practice, $L_d^E$ is rarely computable in [closed form](@entry_id:271343). Instead, we use an approximation obtained, for instance, by applying a [numerical quadrature](@entry_id:136578) rule to the integral of $L$ along some simple curve (like a straight line) connecting $q_k$ and $q_{k+1}$. A discrete Lagrangian $L_d$ is said to be **consistent of order $r$** if it approximates the exact discrete Lagrangian with an error of $\mathcal{O}(h^{r+1})$. It can be shown that an integrator constructed from an $r$-th order consistent discrete Lagrangian will have a global error of order $\mathcal{O}(h^r)$ in tracking the true solution. For instance, many common second-order methods arise from [quadrature rules](@entry_id:753909) that are themselves second-order accurate .

It is important to reiterate the distinction: accuracy depends on the size of $h$, but symplecticity does not. For any fixed $h>0$, the integrator generates a trajectory on a nearby, exactly preserved symplectic manifold. As $h \to 0$, this nearby manifold converges to the true one. This is in stark contrast to non-symplectic methods (like standard Runge-Kutta schemes), which do not preserve any symplectic structure for finite $h$, leading to secular drifts in conserved quantities like energy over long integrations.

### Example: The Störmer-Verlet Method

To make these ideas concrete, let us derive the well-known Störmer-Verlet method from a [variational principle](@entry_id:145218) . Consider a system on $Q=\mathbb{R}^n$ with a constant mass matrix $M$ and potential energy $V(q)$. The continuous Lagrangian is $L(q, \dot{q}) = \frac{1}{2}\dot{q}^T M \dot{q} - V(q)$.

We construct a discrete Lagrangian using a simple [finite difference approximation](@entry_id:1124978) for the velocity, $\dot{q} \approx (q_{k+1}-q_k)/h$, and a midpoint-like approximation for the potential energy term:
$$
L_d(q_k, q_{k+1}; h) = \frac{1}{2h}(q_{k+1}-q_k)^T M (q_{k+1}-q_k) - \frac{h}{2}(V(q_k) + V(q_{k+1}))
$$
This corresponds to applying a [trapezoidal rule](@entry_id:145375) to the continuous Lagrangian. We now compute the derivatives needed for the DEL equation:
$$
D_1 L_d(q_k, q_{k+1}) = -\frac{1}{h}M(q_{k+1}-q_k)^T - \frac{h}{2}(\nabla V(q_k))^T
$$
$$
D_2 L_d(q_{k-1}, q_k) = \frac{1}{h}M(q_k - q_{k-1})^T - \frac{h}{2}(\nabla V(q_k))^T
$$
Plugging these into the DEL equation $D_1 L_d(q_k, q_{k+1}) + D_2 L_d(q_{k-1}, q_k) = 0$ (and transposing to get column vectors) gives:
$$
-\frac{1}{h}M(q_{k+1}-q_k) - \frac{h}{2}\nabla V(q_k) + \frac{1}{h}M(q_k - q_{k-1}) - \frac{h}{2}\nabla V(q_k) = 0
$$
Rearranging terms, we obtain:
$$
M \frac{q_{k+1} - 2q_k + q_{k-1}}{h^2} = -\nabla V(q_k)
$$
This is precisely the **Störmer-Verlet method**, revealed here as the [equation of motion](@entry_id:264286) for a specific discrete variational principle. Its excellent long-term energy behavior is a direct consequence of the symplecticity guaranteed by its variational origin.

### Symmetries and Discrete Noether's Theorem

One of the most elegant results in mechanics is Noether's theorem, which links continuous symmetries of the Lagrangian to conserved quantities. This principle has a direct and powerful analogue in the discrete setting.

Suppose a Lie group $G$ acts on the configuration manifold $Q$ and the discrete Lagrangian is invariant under this action, i.e., $L_d(g \cdot q, g \cdot q') = L_d(q, q')$ for all $g \in G$. Differentiating this invariance with respect to the [group action](@entry_id:143336) at the identity gives the infinitesimal invariance condition:
$$
\langle D_1 L_d(q_k, q_{k+1}), \xi_Q(q_k) \rangle + \langle D_2 L_d(q_k, q_{k+1}), \xi_Q(q_{k+1}) \rangle = 0
$$
for any element $\xi$ in the Lie algebra $\mathfrak{g}$ of $G$, where $\xi_Q$ is the [infinitesimal generator](@entry_id:270424) vector field on $Q$.

This identity allows us to define a **[discrete momentum map](@entry_id:1123825)** $J_d: Q \times Q \to \mathfrak{g}^*$, where $\mathfrak{g}^*$ is the dual of the Lie algebra. Its definition is:
$$
\langle J_d(q_k, q_{k+1}), \xi \rangle := \langle D_2 L_d(q_k, q_{k+1}), \xi_Q(q_{k+1}) \rangle
$$
Using the infinitesimal invariance, we immediately have an alternative expression:
$$
\langle J_d(q_k, q_{k+1}), \xi \rangle = -\langle D_1 L_d(q_k, q_{k+1}), \xi_Q(q_k) \rangle
$$
The **discrete Noether's theorem** states that this momentum map is conserved along any trajectory that satisfies the DEL equations . That is,
$$
J_d(q_{k-1}, q_k) = J_d(q_k, q_{k+1}) \quad \text{for all } k.
$$
The proof is a direct application of the definitions. We test equality by pairing with an arbitrary $\xi \in \mathfrak{g}$:
$$
\langle J_d(q_k, q_{k+1}), \xi \rangle = -\langle D_1 L_d(q_k, q_{k+1}), \xi_Q(q_k) \rangle
$$
$$
\langle J_d(q_{k-1}, q_k), \xi \rangle = \langle D_2 L_d(q_{k-1}, q_k), \xi_Q(q_k) \rangle
$$
The equality of these two expressions, $\langle D_2 L_d(q_{k-1}, q_k), \xi_Q(q_k) \rangle = -\langle D_1 L_d(q_k, q_{k+1}), \xi_Q(q_k) \rangle$, is equivalent to $\langle D_1 L_d(q_k, q_{k+1}) + D_2 L_d(q_{k-1}, q_k), \xi_Q(q_k) \rangle = 0$. This is true precisely because the trajectory satisfies the DEL equations. This theorem guarantees that variational integrators derived from symmetric discrete Lagrangians will exactly preserve the corresponding [discrete momentum map](@entry_id:1123825), a feature crucial for simulating systems with conserved quantities like linear or angular momentum.

### Extensions to Constrained and Forced Systems

The power of the variational framework extends to more complex systems, including those with nonholonomic constraints or [non-conservative forces](@entry_id:164833).

#### Discrete Lagrange-d'Alembert Principle

Consider a system with nonholonomic constraints, where the admissible velocities are restricted to a subbundle $\mathcal{D} \subset TQ$. The principle of virtual work states that [constraint forces](@entry_id:170257) do no work on virtual displacements. In the discrete setting, this is modeled by restricting the variations in the [action principle](@entry_id:154742) to the constraint distribution: $\delta q_k \in \mathcal{D}(q_k)$. Applying this restriction to the variation of the discrete action, we find that the [stationarity condition](@entry_id:191085) $\delta S_d = 0$ no longer requires the DEL expression to be zero. Instead, it requires it to be orthogonal to all admissible variations:
$$
\langle D_1 L_d(q_k, q_{k+1}) + D_2 L_d(q_{k-1}, q_k), \delta q_k \rangle = 0 \quad \text{for all } \delta q_k \in \mathcal{D}(q_k)
$$
This is the definition of the covector $D_1 L_d(q_k, q_{k+1}) + D_2 L_d(q_{k-1}, q_k)$ belonging to the **[annihilator](@entry_id:155446)** of the constraint space, denoted $\mathcal{D}(q_k)^\circ$. The resulting **discrete Lagrange-d'Alembert equations** are:
$$
D_1 L_d(q_k, q_{k+1}) + D_2 L_d(q_{k-1}, q_k) \in \mathcal{D}(q_k)^\circ
$$
This framework provides a systematic way to construct [structure-preserving integrators](@entry_id:755565) for nonholonomic systems, such as a rolling wheel .

#### Non-Conservative Forcing and Energy

When external [non-conservative forces](@entry_id:164833) are present, the variational principle can be augmented with a discrete [virtual work](@entry_id:176403) term. This leads to the **forced discrete Euler-Lagrange equations**. In general, the presence of [non-conservative forces](@entry_id:164833), especially dissipative ones, breaks the symplecticity of the system .

However, there are important exceptions. If a force can be derived from a "discrete potential" (i.e., the [virtual work](@entry_id:176403) term itself is a variation of some function), it can be absorbed into a modified discrete Lagrangian, and the resulting integrator will be symplectic with respect to a modified symplectic form. This is the case for **magnetic forces**, which can be incorporated into the Lagrangian via a magnetic potential, leading to an integrator that preserves a "twisted" symplectic form .

For general forces, while symplecticity is lost, a crucial energy-tracking property is maintained. A discrete version of the [work-energy theorem](@entry_id:168821) can be derived from a discrete analogue of Noether's theorem for time-translation symmetry. Even though energy is not conserved, its change from one step to the next is precisely equal to the discrete work done by the external forces over that step:
$$
E_d(q_k, q_{k+1}) - E_d(q_{k-1}, q_k) = \mathcal{W}_d
$$
where $E_d$ is a discrete energy function derived from $L_d$, and $\mathcal{W}_d$ is the discrete work. This ensures that the integrator correctly accounts for energy entering or leaving the system, avoiding the unphysical numerical dissipation or energy growth that plagues many standard methods when applied to forced or [dissipative systems](@entry_id:151564) over long times .