## Introduction
In the study of [analytical mechanics](@entry_id:166738), the quest for more fundamental and powerful descriptions of motion leads us beyond the familiar Lagrangian framework. The Hamiltonian formulation represents such an advancement, offering a new perspective on dynamics that is not only elegant but essential for progress into modern physics. This approach addresses the limitations of a purely velocity-based description by introducing a more symmetric and insightful space known as phase space, built from [generalized coordinates](@entry_id:156576) and their conjugate momenta. This article will guide you through the core of Hamiltonian mechanics. In the "Principles and Mechanisms" chapter, you will learn the foundational concepts, from the Legendre transformation to Hamilton's equations. Following this, the "Applications and Interdisciplinary Connections" chapter will showcase the remarkable power of the Hamiltonian in fields ranging from quantum theory to cosmology. Finally, the "Hands-On Practices" section will allow you to apply these concepts to concrete physical problems, solidifying your understanding. Let us begin by delving into the principles that define this transformative approach to mechanics.

## Principles and Mechanisms

Following our introduction to the broad motivations for reformulating classical mechanics, this chapter delves into the principles and mechanisms of the Hamiltonian formulation. Where the Lagrangian approach is built upon the configuration space of a system, described by [generalized coordinates](@entry_id:156576) and velocities $(q, \dot{q})$, the Hamiltonian framework shifts our perspective to **phase space**, a space described by [generalized coordinates](@entry_id:156576) and their corresponding [generalized momenta](@entry_id:166813) $(q, p)$. This transition is not merely a [change of variables](@entry_id:141386); it provides a deeper insight into the structure of dynamics, reveals [fundamental symmetries](@entry_id:161256), and paves the way for advanced topics in statistical mechanics and quantum theory.

### From Lagrangian to Hamiltonian: The Legendre Transformation

The bridge between the Lagrangian and Hamiltonian formalisms is a mathematical procedure known as the **Legendre transformation**. Its purpose is to change the functional dependence of our primary dynamical function from coordinates and velocities to coordinates and momenta.

We begin with the Lagrangian $L(q_i, \dot{q}_i, t)$. The first step is to define the **[generalized momentum](@entry_id:165699)** $p_i$ conjugate to the generalized coordinate $q_i$:

$$
p_i \equiv \frac{\partial L}{\partial \dot{q}_i}
$$

It is crucial to recognize this as a definition. While for simple systems the [generalized momentum](@entry_id:165699) often corresponds to the familiar mechanical momentum (mass times velocity), this is not universally true, especially in the presence of velocity-dependent potentials or when using non-Cartesian coordinates.

With the [generalized momenta](@entry_id:166813) defined, the **Hamiltonian function** $H$ is constructed through the Legendre transformation of the Lagrangian:

$$
H(q_i, p_i, t) = \sum_i p_i \dot{q}_i - L(q_i, \dot{q}_i, t)
$$

To complete this transformation, one must perform a critical algebraic step: the set of equations defining the momenta, $p_i = \partial L / \partial \dot{q}_i$, must be inverted to express the [generalized velocities](@entry_id:178456) $\dot{q}_i$ as functions of the coordinates, momenta, and time, i.e., $\dot{q}_i = \dot{q}_i(q_j, p_j, t)$. These expressions are then substituted into the definition of $H$, ensuring that the final Hamiltonian is a function exclusively of the phase space variables $(q_i, p_i)$ and time $t$.

The procedure can be summarized as follows:
1.  Begin with the Lagrangian $L(q_i, \dot{q}_i, t)$.
2.  Calculate the [generalized momenta](@entry_id:166813) for all degrees of freedom: $p_i = \partial L / \partial \dot{q}_i$.
3.  Algebraically solve these equations to express each $\dot{q}_i$ in terms of $q_j$ and $p_j$.
4.  Substitute these expressions for $\dot{q}_i$ into the defining equation for the Hamiltonian, $H = \sum_i p_i \dot{q}_i - L$, to eliminate all velocity terms.

### Constructing the Hamiltonian in Practice

Let us solidify this abstract procedure with several representative examples that highlight its application across different physical scenarios.

#### Standard Conservative Systems

For many common physical systems, the Lagrangian takes the form $L = T - V$, where the kinetic energy $T$ is a quadratic function of the [generalized velocities](@entry_id:178456) and the potential energy $V$ is a function of the coordinates only. In this "standard" case, the Hamiltonian takes a particularly familiar form.

Consider a particle of mass $m$ moving in a potential $V(q_i)$. The kinetic energy is $T = \frac{1}{2} \sum_i m_i \dot{q}_i^2$. The Lagrangian is $L = \frac{1}{2} \sum_i m_i \dot{q}_i^2 - V(q_i)$. The [generalized momentum](@entry_id:165699) is $p_i = \partial L / \partial \dot{q}_i = m_i \dot{q}_i$. The Hamiltonian is then:

$$
H = \sum_i p_i \dot{q}_i - L = \sum_i (m_i \dot{q}_i)\dot{q}_i - \left( \frac{1}{2} \sum_i m_i \dot{q}_i^2 - V(q_i) \right) = \frac{1}{2} \sum_i m_i \dot{q}_i^2 + V(q_i)
$$

Substituting $\dot{q}_i = p_i / m_i$, we find:

$$
H = \sum_i \frac{p_i^2}{2m_i} + V(q_i) = T + V
$$

Thus, for standard [conservative systems](@entry_id:167760), the Hamiltonian is simply the sum of the kinetic and potential energies—the total energy of the system—expressed in phase space variables.

As a concrete illustration, consider an ion of mass $m$ in a two-dimensional anisotropic harmonic potential $V(x,y) = \frac{1}{2}k_1 x^2 + \frac{1}{2}k_2 y^2$ [@problem_id:2084316]. The Lagrangian is $L = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) - \frac{1}{2}(k_1 x^2 + k_2 y^2)$. The momenta are $p_x = m\dot{x}$ and $p_y = m\dot{y}$. Following the procedure, the Hamiltonian is found to be:

$$
H(x, y, p_x, p_y) = \frac{p_x^2}{2m} + \frac{p_y^2}{2m} + \frac{1}{2}k_1 x^2 + \frac{1}{2}k_2 y^2
$$

This result demonstrates a key property: for a system composed of uncoupled subsystems, the total Hamiltonian is the sum of the Hamiltonians of the individual subsystems. This is evident as $H = H_x + H_y$, where $H_x$ and $H_y$ describe independent harmonic oscillators. This [principle of additivity](@entry_id:189700) applies broadly, for instance, to a system of two distinct, uncoupled harmonic oscillators described by coordinates $q_1$ and $q_2$ [@problem_id:2084287].

#### Non-Cartesian Coordinate Systems

The Hamiltonian formalism is particularly powerful when applied to systems described by non-Cartesian coordinates, such as polar or spherical coordinates. In these cases, the kinetic energy term in the Lagrangian often depends on the [generalized coordinates](@entry_id:156576), not just the velocities.

Let us analyze a particle of mass $m$ moving in a two-dimensional central potential $V(r) = \alpha r^3$, described by [polar coordinates](@entry_id:159425) $(r, \theta)$ [@problem_id:2084346]. The kinetic energy is $T = \frac{1}{2}m(\dot{r}^2 + r^2\dot{\theta}^2)$, so the Lagrangian is $L = \frac{1}{2}m(\dot{r}^2 + r^2\dot{\theta}^2) - \alpha r^3$.

The [generalized momenta](@entry_id:166813) are:
$$
p_r = \frac{\partial L}{\partial \dot{r}} = m\dot{r}
$$
$$
p_\theta = \frac{\partial L}{\partial \dot{\theta}} = mr^2\dot{\theta}
$$

Here, we see that $p_r$ corresponds to the [linear momentum](@entry_id:174467) in the radial direction, while $p_\theta$ is the angular momentum. Inverting for the velocities gives $\dot{r} = p_r/m$ and $\dot{\theta} = p_\theta / (mr^2)$. Substituting these into the definition of $H$ yields:

$$
H = p_r\dot{r} + p_\theta\dot{\theta} - L = \frac{p_r^2}{m} + \frac{p_\theta^2}{mr^2} - \left[ \frac{1}{2}m\left(\frac{p_r^2}{m^2} + r^2\frac{p_\theta^2}{m^2r^4}\right) - \alpha r^3 \right]
$$

Simplifying this expression, we arrive at the Hamiltonian:

$$
H(r, \theta, p_r, p_\theta) = \frac{p_r^2}{2m} + \frac{p_\theta^2}{2mr^2} + \alpha r^3
$$

This form elegantly separates the energy into a radial kinetic term, a rotational kinetic term (often called the centrifugal barrier), and the potential energy. The presence of the coordinate $r$ in the kinetic energy part of the Hamiltonian is a common and important feature when using [curvilinear coordinates](@entry_id:178535).

#### Beyond Standard Systems: Velocity and Position Dependence

The true power and generality of the Hamiltonian method become apparent in "non-standard" systems, where the simple relationship $H=T+V$ may not hold.

A prominent class of such systems involves Lagrangians with terms linear in the velocities. These often arise when describing the [motion of charged particles](@entry_id:265607) in magnetic fields. Consider a particle of mass $m$ with a Lagrangian $L = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2) + k(x\dot{y} - y\dot{x})$ [@problem_id:2084312]. The terms linear in velocity lead to a modified definition of canonical momentum:

$$
p_x = \frac{\partial L}{\partial \dot{x}} = m\dot{x} - ky
$$
$$
p_y = \frac{\partial L}{\partial \dot{y}} = m\dot{y} + kx
$$

Here, the **[canonical momentum](@entry_id:155151)** ($p_x, p_y$) is clearly distinct from the **kinematic momentum** ($m\dot{x}, m\dot{y}$). This is a fundamental concept. Solving for the velocities gives $\dot{x} = (p_x+ky)/m$ and $\dot{y} = (p_y-kx)/m$. The Legendre transformation reveals a striking result:

$$
H = p_x\dot{x} + p_y\dot{y} - L = \frac{1}{2}m(\dot{x}^2 + \dot{y}^2)
$$

Notice that the [velocity-dependent potential](@entry_id:168006) terms have cancelled out. The Hamiltonian is equal to the kinetic energy. However, to express it in the required phase space variables, we must substitute our expressions for $\dot{x}$ and $\dot{y}$:

$$
H(x, y, p_x, p_y) = \frac{1}{2m}\left[ (p_x+ky)^2 + (p_y-kx)^2 \right]
$$

This is a critical example: the Hamiltonian is not simply $T(p) + V(q)$, and its form is not immediately intuitive from the Lagrangian. A similar non-standard relationship between momentum and velocity appears in systems with Lagrangians containing terms like $\alpha x \dot{x}$ [@problem_id:2084317].

Another important non-standard case involves a **position-dependent mass**, $m(q)$. For a [free particle](@entry_id:167619) experiencing no potential, the Lagrangian is $L = \frac{1}{2}m(q)\dot{q}^2$ [@problem_id:2084294]. The [canonical momentum](@entry_id:155151) is $p = m(q)\dot{q}$, so $\dot{q} = p/m(q)$. The Hamiltonian is:

$$
H = p\dot{q} - L = p\left(\frac{p}{m(q)}\right) - \frac{1}{2}m(q)\left(\frac{p}{m(q)}\right)^2 = \frac{p^2}{2m(q)}
$$

If, for example, $m(q) = m_0/(1+\alpha q^2)$, the Hamiltonian becomes $H(q, p) = \frac{(1+\alpha q^2)p^2}{2m_0}$. The kinetic energy term in the Hamiltonian now explicitly depends on the position coordinate $q$, a direct consequence of the position-dependent mass.

### The Dynamics of Phase Space: Hamilton's Equations

Having constructed the Hamiltonian, we now turn to its primary purpose: describing the [time evolution](@entry_id:153943) of the system. The Hamiltonian function acts as the [generator of time evolution](@entry_id:166044) for the phase space coordinates $(q_i, p_i)$. This evolution is governed by a set of elegant, symmetric, [first-order differential equations](@entry_id:173139) known as **Hamilton's [equations of motion](@entry_id:170720)**.

These equations can be derived by considering the total differential of the Hamiltonian, $H(q_i, p_i, t)$. First, from calculus:

$$
dH = \sum_i \left( \frac{\partial H}{\partial q_i}dq_i + \frac{\partial H}{\partial p_i}dp_i \right) + \frac{\partial H}{\partial t}dt
$$

Second, from the definition $H = \sum_i p_i \dot{q}_i - L$:

$$
dH = \sum_i (\dot{q}_i dp_i + p_i d\dot{q}_i) - \sum_i \left( \frac{\partial L}{\partial q_i}dq_i + \frac{\partial L}{\partial \dot{q}_i}d\dot{q}_i \right) - \frac{\partial L}{\partial t}dt
$$

Using the definitions $p_i = \partial L / \partial \dot{q}_i$ and the Euler-Lagrange equation $\dot{p}_i = \partial L / \partial q_i$, and noting that $\partial L/\partial t = -\partial H/\partial t$, this expression simplifies to:

$$
dH = \sum_i (\dot{q}_i dp_i - \dot{p}_i dq_i) + \frac{\partial H}{\partial t}dt
$$

Comparing the coefficients of $dq_i$ and $dp_i$ in our two expressions for $dH$, we arrive at Hamilton's equations:

$$
\dot{q}_i = \frac{\partial H}{\partial p_i} \qquad \text{and} \qquad \dot{p}_i = -\frac{\partial H}{\partial q_i}
$$

These are $2n$ [first-order differential equations](@entry_id:173139) for a system with $n$ degrees of freedom, contrasting with the $n$ second-order equations of the Lagrangian formalism. Their symmetric structure is not only aesthetically pleasing but also provides a powerful framework for theoretical analysis.

For instance, consider a particle moving in the potential $V(x,y) = cxy$ [@problem_id:2084304]. The Hamiltonian is $H = \frac{p_x^2 + p_y^2}{2m} + cxy$. Applying Hamilton's equations gives the system's evolution directly:
$$
\dot{x} = \frac{\partial H}{\partial p_x} = \frac{p_x}{m}
$$
$$
\dot{y} = \frac{\partial H}{\partial p_y} = \frac{p_y}{m}
$$
$$
\dot{p}_x = -\frac{\partial H}{\partial x} = -cy
$$
$$
\dot{p}_y = -\frac{\partial H}{\partial y} = -cx
$$
These four first-order equations completely describe the dynamics in phase space.

### Symmetries and Conservation Laws

One of the most profound aspects of the Hamiltonian formalism is its direct and transparent connection between [symmetries and conservation laws](@entry_id:168267).

#### The Conservation of the Hamiltonian

A central question is: under what conditions is the Hamiltonian $H$ itself a conserved quantity? We can find the [total time derivative](@entry_id:172646) of $H$ along a trajectory of the system:

$$
\frac{dH}{dt} = \frac{d}{dt}H(q(t), p(t), t) = \sum_i \left( \frac{\partial H}{\partial q_i}\dot{q}_i + \frac{\partial H}{\partial p_i}\dot{p}_i \right) + \frac{\partial H}{\partial t}
$$

Substituting Hamilton's equations, $\dot{q}_i = \partial H / \partial p_i$ and $\dot{p}_i = -\partial H / \partial q_i$, into this expression yields:

$$
\frac{dH}{dt} = \sum_i \left( \frac{\partial H}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial H}{\partial p_i}\frac{\partial H}{\partial q_i} \right) + \frac{\partial H}{\partial t} = \frac{\partial H}{\partial t}
$$

This remarkably simple and powerful result states that the [total time derivative](@entry_id:172646) of the Hamiltonian is equal to its partial derivative with respect to time. Consequently, **the Hamiltonian is conserved if and only if it does not explicitly depend on time** ($\partial H / \partial t = 0$).

If the system is standard and conservative, we know $H = T+V$, which is the total energy. If the potential is time-independent, then $H$ is time-independent, and thus total energy is conserved. However, if the potential explicitly depends on time, as in a [harmonic oscillator](@entry_id:155622) with a decaying [spring constant](@entry_id:167197) $V(x,t) = \frac{1}{2}kx^2 \exp(-\gamma t)$, the Hamiltonian will also have explicit time dependence [@problem_id:2084313]. In this case, $H = \frac{p^2}{2m} + \frac{1}{2}kx^2 \exp(-\gamma t)$, and since $\partial H / \partial t \neq 0$, the Hamiltonian (and the energy) is not conserved.

More complex time dependencies can lead to interesting dynamics. For a system with the Lagrangian $L = \frac{1}{2}m\dot{x}^{2} \exp(\gamma t) - V(x)\exp(-\gamma t)$, the resulting Hamiltonian is $H = (\frac{p^2}{2m} + V(x))\exp(-\gamma t)$ [@problem_id:2084298]. Applying our master equation gives:

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t} = -\gamma \left(\frac{p^2}{2m} + V(x)\right)\exp(-\gamma t) = -\gamma H
$$

Here, the Hamiltonian is not conserved but decays exponentially, a non-trivial result that follows directly from the formalism.

#### Cyclic Coordinates and Conserved Momenta

The connection between [symmetry and conservation](@entry_id:154858) is most clearly seen with [cyclic coordinates](@entry_id:166051). A coordinate $q_k$ is said to be **cyclic** if it does not appear explicitly in the Hamiltonian. That is, $\partial H / \partial q_k = 0$.

From Hamilton's equation for the [conjugate momentum](@entry_id:172203) $p_k$, we have:

$$
\dot{p}_k = - \frac{\partial H}{\partial q_k}
$$

If $q_k$ is cyclic, then $\partial H / \partial q_k = 0$, which immediately implies $\dot{p}_k = 0$. This means $p_k$ is a constant of the motion. Therefore, **the [generalized momentum](@entry_id:165699) conjugate to a cyclic coordinate is a conserved quantity**.

This provides a direct link between a system's symmetry and a conserved physical quantity. For instance, if the Hamiltonian is independent of a spatial coordinate like $x$, it implies the system is symmetric under translations in the $x$-direction, and the corresponding momentum $p_x$ is conserved.

Consider a particle moving in a potential that depends only on $x$, such as $V(x,y) = V_0 \sin^2(\beta x)$ [@problem_id:2084290]. The Hamiltonian is $H = \frac{p_x^2+p_y^2}{2m} + V_0 \sin^2(\beta x)$. Since the coordinate $y$ does not appear in $H$, it is a cyclic coordinate. According to our principle, its [conjugate momentum](@entry_id:172203), $p_y$, must be conserved. This makes intuitive sense: with no forces acting in the $y$-direction, the momentum in that direction must remain constant. The Hamiltonian formalism makes this connection immediate and rigorous.