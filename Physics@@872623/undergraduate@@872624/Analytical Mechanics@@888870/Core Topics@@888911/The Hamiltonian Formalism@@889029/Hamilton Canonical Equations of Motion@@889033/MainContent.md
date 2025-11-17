## Introduction
Classical mechanics offers several powerful formalisms for describing the motion of physical systems. While the Lagrangian approach simplifies dynamics using [generalized coordinates](@entry_id:156576) and [second-order differential equations](@entry_id:269365), the Hamiltonian formulation, developed by William Rowan Hamilton, provides an equally potent, alternative perspective. It recasts dynamics into a symmetric set of first-order equations that treat [generalized coordinates](@entry_id:156576) and their conjugate momenta on an equal footing. This shift not only presents a new toolkit for solving problems but also uncovers the deep geometric structure of motion in phase space and lays the mathematical groundwork for statistical and quantum mechanics. This article addresses the need for a unified understanding of this pivotal theory, from its foundational principles to its far-reaching applications.

Across the following chapters, you will gain a thorough understanding of Hamiltonian mechanics. The first chapter, **Principles and Mechanisms**, will guide you through the transition from the Lagrangian to the Hamiltonian via the Legendre transformation, introduce Hamilton's canonical equations, and explore the concepts of phase space, Poisson brackets, and the profound link between [symmetries and conservation laws](@entry_id:168267). The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate the formalism's power in solving advanced problems in classical mechanics and reveal its unifying role in diverse fields such as electromagnetism, optics, and condensed matter physics, showing how it serves as a gateway to modern physical theories. Finally, the **Hands-On Practices** chapter will offer targeted exercises to help you apply these concepts and solidify your mastery of the Hamiltonian method.

## Principles and Mechanisms

The Lagrangian formulation of mechanics, centered on the [principle of stationary action](@entry_id:151723), provides a powerful and elegant framework for deriving the [equations of motion](@entry_id:170720). However, it describes the dynamics of a system with $N$ degrees of freedom through $N$ [second-order differential equations](@entry_id:269365). An alternative, yet equally powerful, formulation was developed by William Rowan Hamilton. The Hamiltonian approach recasts the dynamics in terms of $2N$ [first-order differential equations](@entry_id:173139), treating [generalized coordinates](@entry_id:156576) and [generalized momenta](@entry_id:166813) on an equal footing. This shift in perspective not only offers a different method for solving mechanical problems but also unveils deeper structural symmetries of physical laws and provides the mathematical foundation for statistical mechanics and quantum mechanics.

### From Lagrangian to Hamiltonian: The Legendre Transformation

The transition from the Lagrangian to the Hamiltonian framework is accomplished through a mathematical procedure known as the **Legendre transformation**. The starting point is the Lagrangian, $L(q_i, \dot{q}_i, t)$, which is a function of the [generalized coordinates](@entry_id:156576) $q_i$, [generalized velocities](@entry_id:178456) $\dot{q}_i$, and time $t$. The first step is to define the **[canonical momentum](@entry_id:155151)**, $p_i$, conjugate to the coordinate $q_i$:

$$
p_i \equiv \frac{\partial L}{\partial \dot{q}_i}
$$

This definition establishes a relationship between the [generalized velocities](@entry_id:178456) and the newly defined [canonical momenta](@entry_id:150209). In many standard systems, this relationship can be inverted to express the velocities $\dot{q}_i$ as functions of the coordinates $q_i$, momenta $p_i$, and time $t$.

With the [canonical momenta](@entry_id:150209) defined, the **Hamiltonian**, $H$, is constructed as follows:

$$
H(q_i, p_i, t) = \sum_{i} p_i \dot{q}_i - L(q_i, \dot{q}_i, t)
$$

It is crucial to ensure that after the transformation, the Hamiltonian is expressed solely as a function of the coordinates $q_i$, the [canonical momenta](@entry_id:150209) $p_i$, and time $t$. Any residual dependence on the [generalized velocities](@entry_id:178456) $\dot{q}_i$ must be eliminated by substituting their expressions in terms of the momenta.

Let us illustrate this procedure with a concrete example. Consider a particle of mass $m$ attached to a vertical spring of constant $k$ in a uniform gravitational field $g$ [@problem_id:2055738]. Let the coordinate $z$ be the downward displacement from the spring's natural length. The kinetic energy is $T = \frac{1}{2}m\dot{z}^2$ and the potential energy, comprising both elastic and gravitational contributions, is $V(z) = \frac{1}{2}kz^2 - mgz$. The Lagrangian is thus:

$$
L(z, \dot{z}) = T - V = \frac{1}{2}m\dot{z}^2 - \frac{1}{2}kz^2 + mgz
$$

The [canonical momentum](@entry_id:155151) conjugate to $z$ is:

$$
p_z = \frac{\partial L}{\partial \dot{z}} = m\dot{z}
$$

From this, we can express the velocity as $\dot{z} = p_z / m$. Now, we construct the Hamiltonian:

$$
H(z, p_z) = p_z \dot{z} - L = p_z\left(\frac{p_z}{m}\right) - \left( \frac{1}{2}m\left(\frac{p_z}{m}\right)^2 - \frac{1}{2}kz^2 + mgz \right)
$$

Simplifying this expression yields:

$$
H(z, p_z) = \frac{p_z^2}{m} - \frac{p_z^2}{2m} + \frac{1}{2}kz^2 - mgz = \frac{p_z^2}{2m} + \frac{1}{2}kz^2 - mgz
$$

This is the Hamiltonian for the system, expressed correctly in terms of the coordinate $z$ and its [conjugate momentum](@entry_id:172203) $p_z$.

### Hamilton's Canonical Equations of Motion

The Hamiltonian serves as the [generator of time evolution](@entry_id:166044) for the system's state in **phase space**, a $2N$-dimensional space whose axes correspond to the [generalized coordinates](@entry_id:156576) $q_i$ and [canonical momenta](@entry_id:150209) $p_i$. The equations governing this evolution are known as **Hamilton's canonical equations**. They can be derived by considering the total differential of the Hamiltonian $H(q_i, p_i, t)$:

$$
dH = \sum_i \left( \frac{\partial H}{\partial q_i} dq_i + \frac{\partial H}{\partial p_i} dp_i \right) + \frac{\partial H}{\partial t} dt
$$

Comparing this with the differential of the defining relation $H = \sum_i p_i \dot{q}_i - L$ and using the Euler-Lagrange equations, we arrive at the elegant and symmetric set of equations:

$$
\dot{q}_i = \frac{\partial H}{\partial p_i} \quad \text{and} \quad \dot{p}_i = -\frac{\partial H}{\partial q_i}
$$

These are the canonical [equations of motion](@entry_id:170720). They form a system of $2N$ [first-order ordinary differential equations](@entry_id:264241), in contrast to the $N$ second-order equations of the Lagrangian formalism. Additionally, the time evolution of the Hamiltonian itself is given by:

$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$

This last relation immediately implies that if the Hamiltonian has no explicit time dependence ($\partial H / \partial t = 0$), then it is a constant of the motion, i.e., $H$ is conserved.

For a particle with a time-varying mass $m(t)$ moving in a [one-dimensional potential](@entry_id:146615) $U(x)$ [@problem_id:2055700], the Lagrangian is $L = \frac{1}{2}m(t)\dot{x}^2 - U(x)$. The [canonical momentum](@entry_id:155151) is $p = m(t)\dot{x}$, and the Hamiltonian is $H(x, p, t) = \frac{p^2}{2m(t)} + U(x)$. Applying Hamilton's equations gives:

$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{p}{m(t)}
$$

$$
\dot{p} = -\frac{\partial H}{\partial x} = -\frac{dU}{dx}
$$

This is a remarkable result. The equation for $\dot{p}$ shows that the rate of change of the *canonical momentum* is equal to the applied force $F = -dU/dx$. This is not the same as the full time derivative of the physical momentum, which would be $\frac{d}{dt}(m\dot{x}) = \dot{m}\dot{x} + m\ddot{x}$. The Hamiltonian formalism elegantly separates the change in momentum due to external forces from effects related to changing mass.

### The Physical Interpretation of the Hamiltonian

A central question is the physical meaning of the Hamiltonian. For many systems, it corresponds to the total mechanical energy, $E = T + V$. This is true if the transformations defining the [generalized coordinates](@entry_id:156576) from a Cartesian system do not explicitly depend on time. In such cases, the Hamiltonian can be shown to be $H = T + V$. Our vertical spring example [@problem_id:2055738] illustrates this; the resulting Hamiltonian, $H = \frac{p_z^2}{2m} + \frac{1}{2}kz^2 - mgz$, is precisely the kinetic energy plus the potential energy.

However, when the relationship between Cartesian and [generalized coordinates](@entry_id:156576) is explicitly time-dependent, the Hamiltonian is generally **not** the total energy. Consider a [simple pendulum](@entry_id:276671) whose length is forced to change over time as $l(t) = l_0 + v_0 t$ [@problem_id:2055718]. The kinetic energy is $T = \frac{1}{2}m(v_0^2 + l(t)^2 \dot{\theta}^2)$ and the potential energy is $V = -mg l(t) \cos(\theta)$. The canonical momentum is $p_\theta = m l(t)^2 \dot{\theta}$. A careful Legendre transformation reveals the Hamiltonian to be:

$$
H(\theta, p_\theta, t) = \frac{p_\theta^2}{2m(l_0+v_0t)^2} - mg(l_0+v_0t)\cos\theta - \frac{1}{2}m v_0^2
$$

In this case, the total energy is $E = T+V = \frac{p_\theta^2}{2m l(t)^2} + \frac{1}{2}mv_0^2 - mg l(t) \cos(\theta)$. We can clearly see that $H = E - mv_0^2$. The Hamiltonian is not the total energy. Furthermore, because $H$ explicitly depends on time through the $l(t)$ terms, it is not a conserved quantity. Energy is not conserved because the external agent changing the pendulum's length is doing work on the system.

### Dynamics in Phase Space

The Hamiltonian framework provides a powerful geometric interpretation of a system's dynamics. The state of a system at any instant is represented by a single point in phase space. As time progresses, this point traces out a path known as a **[phase space trajectory](@entry_id:152031)**.

A classic example is the one-dimensional simple harmonic oscillator (SHO) [@problem_id:2055720]. Its Hamiltonian is:

$$
H(q, p) = \frac{p^2}{2m} + \frac{1}{2}kq^2
$$

Since this Hamiltonian has no explicit time dependence, it is conserved. Let's set its value to a constant, the total energy $E$. The trajectory in phase space is defined by the equation $H(q, p) = E$:

$$
\frac{p^2}{2m} + \frac{1}{2}kq^2 = E
$$

Rearranging this equation into standard form gives:

$$
\frac{q^2}{(\sqrt{2E/k})^2} + \frac{p^2}{(\sqrt{2mE})^2} = 1
$$

This is the equation of an **ellipse** centered at the origin of the phase space. The semi-axes of the ellipse are $\sqrt{2E/k}$ along the position axis and $\sqrt{2mE}$ along the momentum axis. Different values of the energy $E$ correspond to a family of nested ellipses. This geometric picture provides a complete and intuitive overview of all possible motions of the oscillator.

The time evolution of any dynamical quantity $A(q, p, t)$ can also be found using the Hamiltonian. The [total time derivative](@entry_id:172646) is:

$$
\frac{dA}{dt} = \frac{\partial A}{\partial t} + \sum_i \left( \frac{\partial A}{\partial q_i}\dot{q}_i + \frac{\partial A}{\partial p_i}\dot{p}_i \right)
$$

Substituting Hamilton's canonical equations yields:

$$
\frac{dA}{dt} = \frac{\partial A}{\partial t} + \sum_i \left( \frac{\partial A}{\partial q_i}\frac{\partial H}{\partial p_i} - \frac{\partial A}{\partial p_i}\frac{\partial H}{\partial q_i} \right) = \frac{\partial A}{\partial t} + \{A, H\}
$$

The term $\{A, H\}$ is the **Poisson bracket** of $A$ and $H$. For a quantity $A$ that does not explicitly depend on time, its rate of change is simply given by its Poisson bracket with the Hamiltonian. For instance, for a particle in a quartic potential $U(x) = \frac{1}{4}\beta x^4$ [@problem_id:2055701], the Hamiltonian is $H = \frac{p^2}{2m} + \frac{1}{4}\beta x^4$. If we consider the quantity $Q = px$, its time derivative is:

$$
\dot{Q} = \frac{d}{dt}(px) = \dot{p}x + p\dot{x} = \left(-\frac{\partial H}{\partial x}\right)x + p\left(\frac{\partial H}{\partial p}\right) = (-\beta x^3)x + p\left(\frac{p}{m}\right) = \frac{p^2}{m} - \beta x^4
$$

### Symmetries and Conservation Laws

One of the most profound aspects of the Hamiltonian formalism is its direct link between [symmetries and conservation laws](@entry_id:168267). A symmetry implies that the Hamiltonian is invariant under some change of coordinates.

If the Hamiltonian does not depend on a particular generalized coordinate $q_k$, i.e., $\frac{\partial H}{\partial q_k} = 0$, then that coordinate is called **cyclic** or **ignorable**. From Hamilton's second equation, we immediately see the consequence:

$$
\dot{p}_k = -\frac{\partial H}{\partial q_k} = 0
$$

This implies that the canonical momentum $p_k$ conjugate to the cyclic coordinate $q_k$ is a **conserved quantity**.

This principle provides a systematic way to identify [constants of motion](@entry_id:150267). For a particle moving on the surface of a cone [@problem_id:2055761], described by coordinates $(r, \phi)$, the Hamiltonian is found to be:

$$
H = \frac{p_r^2}{2m} + \frac{p_\phi^2}{2m r^2 \sin^2\alpha} + mgr\cos\alpha
$$

By inspection, the coordinate $\phi$ does not appear in the Hamiltonian. Therefore, $\phi$ is a cyclic coordinate, and its [conjugate momentum](@entry_id:172203), $p_\phi = m r^2 \sin^2\alpha \dot{\phi}$ (which represents the angular momentum about the vertical axis), is conserved.

Similarly, for a [free particle in spherical coordinates](@entry_id:148180) $(r, \theta, \phi)$ [@problem_id:2055746], the Hamiltonian is $H = \frac{p_r^2}{2m} + \frac{p_\theta^2}{2mr^2} + \frac{p_\phi^2}{2mr^2\sin^2\theta}$. The azimuthal angle $\phi$ is cyclic, so $p_\phi$ is conserved. However, the Hamiltonian explicitly depends on $\theta$, so $p_\theta$ is not conserved. Its time evolution is given by Hamilton's equation:

$$
\dot{p}_\theta = -\frac{\partial H}{\partial \theta} = -\frac{\partial}{\partial \theta}\left(\frac{p_\phi^2}{2mr^2\sin^2\theta}\right) = \frac{p_\phi^2 \cos\theta}{mr^2 \sin^3\theta}
$$

This equation describes the rate of change of the polar momentum, which arises because the motion in $\phi$ exerts a "centrifugal" effect related to the $\theta$ coordinate.

### Extensions of the Hamiltonian Formalism

The Hamiltonian framework is robust and can be extended to describe more complex physical situations.

#### Position-Dependent Mass

We previously considered mass varying with time. A different scenario involves a mass that depends on position, $m(x)$ [@problem_id:2055713]. For a bead with mass $m(x) = m_0 \exp(\alpha x)$ in a potential $U(x) = \frac{1}{2}kx^2$, the Hamiltonian is $H = \frac{p^2}{2m(x)} + U(x)$. Here, the position $x$ appears in the kinetic energy term as well. Hamilton's equation for the momentum now becomes:

$$
\dot{p} = -\frac{\partial H}{\partial x} = -\left( \frac{\partial}{\partial x}\left(\frac{p^2}{2m(x)}\right) + \frac{dU}{dx} \right) = \frac{p^2}{2} \frac{m'(x)}{m(x)^2} - kx
$$

where $m'(x) = dm/dx$. The term involving $m'(x)$ acts as a "fictitious force" that arises because of the changing inertia of the particle as it moves. By differentiating $\dot{x} = p/m(x)$ and substituting the expression for $\dot{p}$, one can derive the acceleration, which includes a term proportional to $-\dot{x}^2$, a feature characteristic of such systems.

#### Non-Conservative Systems

The standard formalism applies to [conservative systems](@entry_id:167760). However, it can be modified to include [non-conservative forces](@entry_id:164833), such as friction or drag. If a non-conservative [generalized force](@entry_id:175048) $Q_i$ acts on the system, Hamilton's equations are modified as:

$$
\dot{q}_i = \frac{\partial H}{\partial p_i} \quad \text{and} \quad \dot{p}_i = -\frac{\partial H}{\partial q_i} + Q_i
$$

Here, the Hamiltonian $H$ is still constructed from the conservative parts of the system. For a damped harmonic oscillator subject to a drag force $F_{drag} = -\gamma\dot{x}$ [@problem_id:2055727], the [generalized force](@entry_id:175048) is $Q_x = -\gamma\dot{x}$. The rate of change of the Hamiltonian (the [mechanical energy](@entry_id:162989)) is then:

$$
\frac{dH}{dt} = \sum_i \left( \frac{\partial H}{\partial q_i}\dot{q}_i + \frac{\partial H}{\partial p_i}\dot{p}_i \right) = \sum_i \left( \frac{\partial H}{\partial q_i}\frac{\partial H}{\partial p_i} + \frac{\partial H}{\partial p_i}(-\frac{\partial H}{\partial q_i} + Q_i) \right) = \sum_i \frac{\partial H}{\partial p_i} Q_i
$$

For the one-dimensional damped oscillator, this becomes $\frac{dH}{dt} = \frac{\partial H}{\partial p} Q_x = (\frac{p}{m})(-\gamma\dot{x}) = (\frac{p}{m})(-\gamma\frac{p}{m}) = -\frac{\gamma p^2}{m^2}$. Since $\gamma > 0$, the rate of change is always negative or zero, correctly describing the dissipation of [mechanical energy](@entry_id:162989) from the system due to the drag force.

#### Canonical Transformations

Finally, the structure of Hamilton's equations is preserved under a specific class of transformations in phase space known as **[canonical transformations](@entry_id:178165)**. These transformations map one set of [canonical coordinates](@entry_id:175654) and momenta $(q, p)$ to another $(Q, P)$ while leaving the form of the equations of motion invariant. Such transformations are invaluable for simplifying problems, often by making one or more of the new coordinates cyclic. These transformations are defined by **[generating functions](@entry_id:146702)**. For example, the transformation to [action-angle variables](@entry_id:161141) for the [simple harmonic oscillator](@entry_id:145764) [@problem_id:2055763], given by $q = \sqrt{\frac{2P}{m\omega}} \sin Q$ and $p = \sqrt{2m\omega P} \cos Q$, can be shown to be generated by a function of the first type, $F_1(q, Q) = \frac{m\omega}{2}q^2 \cot Q$. The study of these transformations opens the door to more advanced methods in dynamics, such as Hamilton-Jacobi theory.