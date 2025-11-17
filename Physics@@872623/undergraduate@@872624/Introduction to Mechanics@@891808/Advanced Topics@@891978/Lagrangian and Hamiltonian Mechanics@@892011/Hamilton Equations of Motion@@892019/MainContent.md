## Introduction
While the Lagrangian formulation offers a powerful perspective on classical mechanics, the work of William Rowan Hamilton provides an alternative and equally profound framework. Hamiltonian mechanics shifts the focus from [generalized velocities](@entry_id:178456) to [generalized momenta](@entry_id:166813), placing position and momentum on an equal footing. This approach doesn't just rephrase old laws; it introduces a new mathematical structure and a powerful geometric interpretation of a system's evolution within a construct called phase space. This article bridges the gap between Lagrangian and Hamiltonian dynamics, guiding you through this elegant reformulation. In the "Principles and Mechanisms" chapter, we will derive the Hamiltonian, master Hamilton's equations, and uncover the deep connections between [symmetry and conservation laws](@entry_id:160300). Following this, "Applications and Interdisciplinary Connections" will demonstrate the formalism's power in diverse fields, from celestial mechanics to the foundations of quantum theory. Finally, "Hands-On Practices" will give you the chance to solidify your understanding by solving practical problems.

## Principles and Mechanisms

In our exploration of classical mechanics, the Lagrangian formulation provided a powerful and elegant framework based on the [principle of stationary action](@entry_id:151723). However, an alternative perspective, developed by William Rowan Hamilton, offers new insights and a different, often more convenient, mathematical structure. This Hamiltonian formulation places position and momentum on an equal footing, describing the evolution of a system in a geometric space known as phase space. The equations of motion become a set of [first-order differential equations](@entry_id:173139), which often simplifies both theoretical analysis and numerical solution.

### From Lagrangian to Hamiltonian: The Legendre Transformation

The transition from the Lagrangian to the Hamiltonian framework is accomplished through a mathematical procedure known as the **Legendre transformation**. The Lagrangian, $L(q_i, \dot{q}_i, t)$, is a function of [generalized coordinates](@entry_id:156576), [generalized velocities](@entry_id:178456), and time. The goal is to create a new function, the Hamiltonian, that depends on [generalized coordinates](@entry_id:156576) and their corresponding **conjugate momenta**, rather than velocities.

The [conjugate momentum](@entry_id:172203) $p_i$ corresponding to a generalized coordinate $q_i$ is defined as:
$$
p_i = \frac{\partial L}{\partial \dot{q}_i}
$$
The Hamiltonian $H(q_i, p_i, t)$ is then defined as:
$$
H(q_i, p_i, t) = \sum_{i=1}^{N} p_i \dot{q}_i - L(q_i, \dot{q}_i, t)
$$
To express $H$ solely in terms of $q_i$, $p_i$, and $t$, one must first use the definition of $p_i$ to solve for each generalized velocity $\dot{q}_i$ as a function of coordinates, momenta, and time. These expressions are then substituted into the definition of $H$.

Let us construct the Hamiltonian for a concrete physical system: a simple pendulum of mass $m$ and length $l$. To make the system more general, let the pendulum bob carry a charge $q$ and be subject to both a uniform downward gravitational field $g$ and a uniform horizontal electric field $E$ [@problem_id:2195255]. We choose the angle $\theta$ from the downward vertical as our single generalized coordinate. The position of the bob in a Cartesian system with the origin at the pivot is $x = l \sin\theta$ and $y = -l \cos\theta$ (with y-axis pointing up).

The kinetic energy $T$ is given by:
$$
T = \frac{1}{2} m ( \dot{x}^2 + \dot{y}^2 ) = \frac{1}{2} m ( (l \dot{\theta} \cos\theta)^2 + (l \dot{\theta} \sin\theta)^2 ) = \frac{1}{2} m l^2 \dot{\theta}^2
$$
The potential energy $V$ has contributions from both gravity ($V_g = mgy$) and the electric field ($V_e = -qEx$). We set the potential energy to be zero at the pivot ($x=0, y=0$).
$$
V(\theta) = -mgl\cos\theta - qEl\sin\theta
$$
The Lagrangian $L = T - V$ is:
$$
L(\theta, \dot{\theta}) = \frac{1}{2} m l^2 \dot{\theta}^2 + mgl\cos\theta + qEl\sin\theta
$$
Next, we find the [conjugate momentum](@entry_id:172203) $p_\theta$:
$$
p_\theta = \frac{\partial L}{\partial \dot{\theta}} = m l^2 \dot{\theta}
$$
We invert this relation to express the generalized velocity in terms of the momentum:
$$
\dot{\theta} = \frac{p_\theta}{m l^2}
$$
Finally, we construct the Hamiltonian using the Legendre transformation:
$$
H(\theta, p_\theta) = p_\theta \dot{\theta} - L(\theta, \dot{\theta}) = p_\theta \left(\frac{p_\theta}{m l^2}\right) - \left[ \frac{1}{2} m l^2 \left(\frac{p_\theta}{m l^2}\right)^2 + mgl\cos\theta + qEl\sin\theta \right]
$$
Simplifying this expression yields the Hamiltonian:
$$
H(\theta, p_\theta) = \frac{p_\theta^2}{ml^2} - \left( \frac{p_\theta^2}{2 m l^2} + mgl\cos\theta + qEl\sin\theta \right) = \frac{p_\theta^2}{2 m l^2} - mgl\cos\theta - qEl\sin\theta
$$
Notice that for many common systems where the kinetic energy is a quadratic function of the [generalized velocities](@entry_id:178456) and the potential energy depends only on coordinates, the Hamiltonian takes the familiar form $H = T + V$. Here, the term $\frac{p_\theta^2}{2 m l^2}$ is the kinetic energy expressed in terms of momentum, and the remaining terms constitute the potential energy.

### Hamilton's Equations of Motion

Once the Hamiltonian is constructed, the dynamics of the system are governed by a set of $2N$ [first-order differential equations](@entry_id:173139) known as **Hamilton's equations**:
$$
\dot{q}_i = \frac{\partial H}{\partial p_i}
$$
$$
\dot{p}_i = - \frac{\partial H}{\partial q_i}
$$
These equations form the core of Hamiltonian dynamics. They describe how a point representing the state of the system, $(q_1, ..., q_N, p_1, ..., p_N)$, moves through a $2N$-dimensional space called **phase space**. The elegant symmetry of these equations, where the time derivative of one variable is related to the other variable's partial derivative of $H$, is a hallmark of the formalism.

Let's apply these equations to a particle of mass $m$ in a one-dimensional [anharmonic potential](@entry_id:141227), such as that used to model an [optical tweezer](@entry_id:168262), $V(x) = \alpha x^4$ [@problem_id:2195217]. The Hamiltonian is $H = T + V$:
$$
H(x, p) = \frac{p^2}{2m} + \alpha x^4
$$
Now, we apply Hamilton's equations to find the time evolution of the phase space coordinates $(x, p)$:
$$
\dot{x} = \frac{\partial H}{\partial p} = \frac{\partial}{\partial p} \left( \frac{p^2}{2m} + \alpha x^4 \right) = \frac{p}{m}
$$
This first equation is a restatement of the standard definition of momentum, $p=m\dot{x}$. The second equation gives the dynamics of the momentum:
$$
\dot{p} = - \frac{\partial H}{\partial x} = - \frac{\partial}{\partial x} \left( \frac{p^2}{2m} + \alpha x^4 \right) = -4 \alpha x^3
$$
This result is equivalent to Newton's second law, $F = \dot{p}$, where the force is derived from the potential energy, $F = -\frac{dV}{dx} = -4\alpha x^3$. Hamilton's equations thus correctly reproduce the Newtonian dynamics but within a new, powerful structure.

### Conservation Laws and Symmetries

One of the most profound aspects of both Lagrangian and Hamiltonian mechanics is the deep connection between [symmetries and conservation laws](@entry_id:168267). In the Hamiltonian framework, this connection is particularly transparent.

#### Conservation of Energy

A natural first question is: under what conditions is the Hamiltonian itself a conserved quantity? To find out, we calculate its [total time derivative](@entry_id:172646), $\frac{dH}{dt}$. Using the [chain rule](@entry_id:147422) for a Hamiltonian $H(q_i, p_i, t)$:
$$
\frac{dH}{dt} = \sum_{i} \left( \frac{\partial H}{\partial q_i} \dot{q}_i + \frac{\partial H}{\partial p_i} \dot{p}_i \right) + \frac{\partial H}{\partial t}
$$
Substituting Hamilton's equations, $\dot{q}_i = \partial H / \partial p_i$ and $\dot{p}_i = - \partial H / \partial q_i$, into this expression:
$$
\frac{dH}{dt} = \sum_{i} \left( \frac{\partial H}{\partial q_i} \frac{\partial H}{\partial p_i} - \frac{\partial H}{\partial p_i} \frac{\partial H}{\partial q_i} \right) + \frac{\partial H}{\partial t}
$$
The terms inside the summation cancel perfectly, leaving a remarkably simple result:
$$
\frac{dH}{dt} = \frac{\partial H}{\partial t}
$$
This equation reveals that the Hamiltonian is a constant of motion if and only if it does not explicitly depend on time. For many physical systems, the coordinate system is chosen such that the kinetic and potential energies do not have explicit time dependence, leading to a time-independent Hamiltonian. In such cases, $H$ is conserved, and it usually corresponds to the total energy of the system. This directly relates to the condition on the Lagrangian, as a more detailed derivation shows that $\frac{dH}{dt} = -\frac{\partial L}{\partial t}$ [@problem_id:2195201]. Therefore, the Hamiltonian is conserved if the Lagrangian has no explicit time dependence.

If, however, the system parameters change with time, the Hamiltonian will not be conserved. Consider a harmonic oscillator whose spring "constant" varies with time, described by a time-dependent [angular frequency](@entry_id:274516) $\omega(t)$ [@problem_id:1247199]. The Hamiltonian is:
$$
H(q, p, t) = \frac{p^2}{2m} + \frac{1}{2}m\omega(t)^2 q^2
$$
The rate of change of the system's energy is given directly by the partial derivative with respect to time:
$$
\frac{dH}{dt} = \frac{\partial H}{\partial t} = \frac{\partial}{\partial t} \left( \frac{1}{2}m\omega(t)^2 q^2 \right) = \frac{1}{2}mq^2 \cdot 2\omega(t)\frac{d\omega}{dt} = m q^2 \omega(t) \dot{\omega}(t)
$$
Energy is pumped into or extracted from the system depending on the sign of $\dot{\omega}(t)$ and the particle's position $q$.

#### Cyclic Coordinates and Conserved Momenta

Symmetries in the spatial coordinates also lead to conservation laws. If the Hamiltonian does not depend on a particular generalized coordinate $q_k$, i.e., $\frac{\partial H}{\partial q_k} = 0$, that coordinate is called **cyclic** or **ignorable**. From Hamilton's second equation, we immediately see the consequence:
$$
\dot{p}_k = - \frac{\partial H}{\partial q_k} = 0
$$
This implies that the [conjugate momentum](@entry_id:172203) $p_k$ is a constant of motion. This is a powerful tool for identifying conserved quantities. For instance, in the case of a projectile moving in a uniform gravitational field [@problem_id:2195203], the Hamiltonian is:
$$
H(x, y, p_x, p_y) = \frac{p_x^2 + p_y^2}{2m} + mgy
$$
The Hamiltonian is independent of the horizontal coordinate $x$, making $x$ a cyclic coordinate. Therefore, its [conjugate momentum](@entry_id:172203), $p_x$, must be conserved:
$$
\dot{p}_x = - \frac{\partial H}{\partial x} = 0
$$
This confirms the conservation of horizontal momentum for [projectile motion](@entry_id:174344). In contrast, $y$ is not cyclic, and we find $\dot{p}_y = - \frac{\partial H}{\partial y} = -mg$, which is the [gravitational force](@entry_id:175476).

### Phase Space and Liouville's Theorem

The concept of **phase space** is central to Hamiltonian mechanics. For a system with $N$ degrees of freedom, the phase space is a $2N$-dimensional space whose axes are the [generalized coordinates](@entry_id:156576) $q_i$ and conjugate momenta $p_i$. At any instant, the complete state of the system is represented by a single point in this space. As the system evolves in time according to Hamilton's equations, this point traces out a trajectory.

A remarkable property of this evolution is described by **Liouville's Theorem**. Consider a "cloud" of initial conditions, represented by a small volume (or area, in 2D) in phase space. As each point in this cloud evolves, the shape of the volume will distort. Liouville's theorem states that the total volume of this region in phase space remains constant over time. The flow of states in phase space is incompressible, much like an incompressible fluid.

We can demonstrate this for a [simple harmonic oscillator](@entry_id:145764) [@problem_id:2195239]. The Hamiltonian is $H = \frac{p^2}{2m} + \frac{1}{2}m\omega^2q^2$. The solutions to Hamilton's equations are:
$$
q(t) = q_0\cos(\omega t) + \frac{p_0}{m\omega}\sin(\omega t)
$$
$$
p(t) = p_0\cos(\omega t) - m\omega q_0\sin(\omega t)
$$
where $(q_0, p_0)$ is the state at $t=0$. This transformation from $(q_0, p_0)$ to $(q(t), p(t))$ describes how phase space points move. To see how an [area element](@entry_id:197167) transforms, we compute the Jacobian determinant of this transformation:
$$
J(t) = \begin{pmatrix} \frac{\partial q(t)}{\partial q_0} & \frac{\partial q(t)}{\partial p_0} \\ \frac{\partial p(t)}{\partial q_0} & \frac{\partial p(t)}{\partial p_0} \end{pmatrix} = \begin{pmatrix} \cos(\omega t) & \frac{1}{m\omega}\sin(\omega t) \\ -m\omega\sin(\omega t) & \cos(\omega t) \end{pmatrix}
$$
The determinant of this matrix is:
$$
\det J(t) = \cos^2(\omega t) - \left(\frac{1}{m\omega}\sin(\omega t)\right)\left(-m\omega\sin(\omega t)\right) = \cos^2(\omega t) + \sin^2(\omega t) = 1
$$
Since the determinant is exactly 1, any initial area in the $(q,p)$ phase space is preserved over time. An initial rectangle of states might be sheared into a parallelogram, but its area remains unchanged. This theorem has profound consequences, forming the foundation of classical statistical mechanics.

### Poisson Brackets

The structure of Hamilton's equations suggests a more general way to express the time evolution of any physical quantity. This is achieved through the **Poisson bracket**. For any two functions $A(q,p)$ and $B(q,p)$ on phase space, their Poisson bracket is defined as:
$$
\{A, B\} = \sum_{i=1}^{N} \left( \frac{\partial A}{\partial q_i} \frac{\partial B}{\partial p_i} - \frac{\partial A}{\partial p_i} \frac{\partial B}{\partial q_i} \right)
$$
With this definition, Hamilton's equations can be written compactly as:
$$
\dot{q}_i = \{q_i, H\}, \qquad \dot{p}_i = \{p_i, H\}
$$
More generally, the [total time derivative](@entry_id:172646) of any observable $A(q_i, p_i, t)$ is given by:
$$
\frac{dA}{dt} = \{A, H\} + \frac{\partial A}{\partial t}
$$
This powerful equation encompasses all of Hamiltonian dynamics. It states that the change in a quantity $A$ has two sources: its explicit time dependence ($\partial A / \partial t$) and its evolution due to the system's dynamics, captured by the Poisson bracket with the Hamiltonian. If a quantity $A$ does not explicitly depend on time, it is conserved if and only if its Poisson bracket with the Hamiltonian is zero: $\{A, H\} = 0$.

Poisson brackets provide a direct way to calculate the rate of change of [physical quantities](@entry_id:177395). For instance, the time rate of change of angular momentum is torque. Let's calculate the x-component of the torque, $\tau_x = \dot{L}_x$, for a particle in a potential $V(\mathbf{r})$ [@problem_id:1247242]. Since $L_x = yp_z - zp_y$ has no explicit time dependence, $\dot{L}_x = \{L_x, H\}$. The Hamiltonian is $H = \frac{\mathbf{p}^2}{2m} + V(\mathbf{r})$. A useful property is that the Poisson bracket of angular momentum with any function of $|\mathbf{p}|^2$ is zero, so $\{L_x, T\} = 0$. This leaves:
$$
\dot{L}_x = \{L_x, V\} = \left( \frac{\partial L_x}{\partial y} \frac{\partial V}{\partial p_y} - \frac{\partial L_x}{\partial p_y} \frac{\partial V}{\partial y} \right) + \left( \frac{\partial L_x}{\partial z} \frac{\partial V}{\partial p_z} - \frac{\partial L_x}{\partial p_z} \frac{\partial V}{\partial z} \right)
$$
Since $V$ is a function of coordinates only and $L_x$ is linear in momenta, this simplifies to:
$$
\dot{L}_x = - \frac{\partial L_x}{\partial p_y} \frac{\partial V}{\partial y} - \frac{\partial L_x}{\partial p_z} \frac{\partial V}{\partial z} = -(-z)\frac{\partial V}{\partial y} - (y)\frac{\partial V}{\partial z} = z\frac{\partial V}{\partial y} - y\frac{\partial V}{\partial z}
$$
This expression, $y F_z - z F_y$, is precisely the definition of the x-component of the torque $\mathbf{\tau} = \mathbf{r} \times \mathbf{F}$, where $\mathbf{F} = -\nabla V$. This confirms the consistency and utility of the Poisson bracket formalism. This formalism is especially powerful in complex situations, such as analyzing the [motion of charged particles](@entry_id:265607) in magnetic fields, where the distinction between [canonical momentum](@entry_id:155151) $\mathbf{p}$ and mechanical momentum $\mathbf{\pi} = m\mathbf{v} = \mathbf{p} - q\mathbf{A}$ is crucial [@problem_id:1247102].

### Canonical Transformations

A key advantage of the Hamiltonian framework is the flexibility to change coordinate systems while preserving the structure of the [equations of motion](@entry_id:170720). A transformation from old coordinates $(q,p)$ to new coordinates $(Q,P)$ is called a **[canonical transformation](@entry_id:158330)** if there exists a new Hamiltonian $K(Q,P,t)$ such that the dynamics are still governed by Hamilton's equations:
$$
\dot{Q} = \frac{\partial K}{\partial P}, \qquad \dot{P} = - \frac{\partial K}{\partial Q}
$$
The goal of such a transformation is typically to simplify the form of the Hamiltonian, ideally making one or more of the new coordinates cyclic.

A direct test for whether a transformation $Q(q,p), P(q,p)$ is canonical is to compute the **fundamental Poisson brackets** of the new variables using the old variables. A transformation is canonical if:
$$
\{Q, P\}_{qp} = 1, \quad \{Q, Q\}_{qp} = 0, \quad \{P, P\}_{qp} = 0
$$
Let's verify the transformation given by $Q=q^2$ and $P=\frac{p}{2q}$ [@problem_id:1247111]. We compute the Poisson bracket $\{Q,P\}$ with respect to the original $(q,p)$ variables:
$$
\{Q, P\}_{qp} = \frac{\partial Q}{\partial q}\frac{\partial P}{\partial p} - \frac{\partial Q}{\partial p}\frac{\partial P}{\partial q}
$$
The required partial derivatives are:
$$
\frac{\partial Q}{\partial q} = 2q, \quad \frac{\partial Q}{\partial p} = 0, \quad \frac{\partial P}{\partial q} = -\frac{p}{2q^2}, \quad \frac{\partial P}{\partial p} = \frac{1}{2q}
$$
Substituting these into the Poisson bracket gives:
$$
\{Q, P\}_{qp} = (2q)\left(\frac{1}{2q}\right) - (0)\left(-\frac{p}{2q^2}\right) = 1 - 0 = 1
$$
Since the bracket is equal to 1, the transformation is indeed canonical.

Advanced techniques, such as the **Hamilton-Jacobi theory**, provide systematic methods for finding [canonical transformations](@entry_id:178165) that can solve a given problem completely. For example, one can seek a transformation that makes the new Hamiltonian $K$ identically zero, or dependent only on the new momentum $P$ [@problem_id:1247190]. In such cases, the new coordinates become simple functions of time, and the problem is effectively solved. These powerful methods bridge the gap between classical mechanics and the development of quantum mechanics, where the Hamiltonian and Poisson brackets play foundational roles.