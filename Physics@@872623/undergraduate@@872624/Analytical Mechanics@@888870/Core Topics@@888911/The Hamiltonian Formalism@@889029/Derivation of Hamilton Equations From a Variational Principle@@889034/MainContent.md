## Introduction
In the study of [analytical mechanics](@entry_id:166738), the Lagrangian formulation provides a powerful framework for describing physical systems. However, an even more profound and symmetric perspective is offered by Hamiltonian mechanics. This approach shifts the description from configuration space to a higher-dimensional state space known as phase space, recasting the second-order Lagrange equations into a more elegant set of [first-order differential equations](@entry_id:173139). This article addresses the fundamental question: how are these new equations of motion derived? We will show that they originate from a variational principle analogous to, yet distinct from, the one used in Lagrangian mechanics.

This exploration is structured to build a comprehensive understanding from the ground up. In the first chapter, **Principles and Mechanisms**, we will rigorously derive Hamilton's equations from a variational principle in phase space, introduce the Hamiltonian function through the Legendre transform, and establish its crucial connection to energy conservation. Following this, the chapter on **Applications and Interdisciplinary Connections** will showcase the remarkable versatility of the Hamiltonian formalism, applying it to problems in electromagnetism, celestial mechanics, and the transition to continuous field theories. Finally, the **Hands-On Practices** section will offer a series of targeted problems designed to reinforce these concepts and develop practical skills. We begin our journey by examining the core [variational principle](@entry_id:145218) that underpins this entire elegant structure.

## Principles and Mechanisms

In the preceding discussions of Lagrangian mechanics, we described the state of a mechanical system using a set of [generalized coordinates](@entry_id:156576) $q_i$ and their corresponding velocities $\dot{q}_i$. The equations of motion, derived from a single scalar function—the Lagrangian—were [second-order differential equations](@entry_id:269365) in time. We now transition to an alternative, yet profoundly equivalent, formulation known as Hamiltonian mechanics. This framework offers a different perspective by describing the system's state in a new space, known as **phase space**, and recasting the dynamics as a set of [first-order differential equations](@entry_id:173139). This change not only provides a powerful new tool for solving complex problems but also reveals deeper symmetries and structural properties of physical laws, forming the bedrock for statistical mechanics and quantum mechanics.

### The Variational Principle in Phase Space

The foundation of Hamiltonian dynamics is a variational principle, analogous to Hamilton's principle in Lagrangian mechanics. However, instead of considering paths in [configuration space](@entry_id:149531) $(q)$, we consider paths in a $2n$-dimensional state space called **phase space**, whose coordinates are the [generalized coordinates](@entry_id:156576) $q_i$ and their corresponding **[canonical momenta](@entry_id:150209)** $p_i$. A key conceptual shift in this formalism is that the coordinates $q(t)$ and momenta $p(t)$ are treated as independent functions to be varied.

The dynamics of the system are governed by the [principle of stationary action](@entry_id:151723) applied to the **phase space [action functional](@entry_id:169216)**, defined as:
$$S[q, p] = \int_{t_1}^{t_2} \left[ \sum_{i=1}^n p_i(t) \dot{q}_i(t) - H(q(t), p(t), t) \right] dt$$
Here, the function $H(q, p, t)$ is the **Hamiltonian** of the system, which we will define more formally in the next section. For now, we take it as a given function of the coordinates, momenta, and time. The physical trajectory that a system follows through phase space is the one that renders this action $S$ stationary, i.e., $\delta S = 0$.

To derive the [equations of motion](@entry_id:170720) from this principle, we compute the variation of the action, $\delta S$, resulting from arbitrary, independent variations of the paths, $\delta q_i(t)$ and $\delta p_i(t)$, which are required to vanish at the time boundaries: $\delta q_i(t_1) = \delta q_i(t_2) = 0$. The variation of the integrand, which we denote as $\mathcal{L}_H = \sum_i p_i \dot{q}_i - H$, is:
$$\delta \mathcal{L}_H = \sum_{i=1}^n \left( \delta p_i \dot{q}_i + p_i \delta \dot{q}_i - \frac{\partial H}{\partial q_i} \delta q_i - \frac{\partial H}{\partial p_i} \delta p_i \right)$$
The variation of the action is the integral of this expression [@problem_id:404156]:
$$\delta S = \int_{t_1}^{t_2} \sum_{i=1}^n \left( \dot{q}_i \delta p_i + p_i \frac{d}{dt}(\delta q_i) - \frac{\partial H}{\partial q_i} \delta q_i - \frac{\partial H}{\partial p_i} \delta p_i \right) dt$$
We can integrate the term involving $\frac{d}{dt}(\delta q_i)$ by parts:
$$\int_{t_1}^{t_2} p_i \frac{d}{dt}(\delta q_i) dt = [p_i \delta q_i]_{t_1}^{t_2} - \int_{t_1}^{t_2} \dot{p}_i \delta q_i dt$$
The boundary term $[p_i \delta q_i]_{t_1}^{t_2}$ vanishes because $\delta q_i$ is zero at the endpoints. Substituting this back into the expression for $\delta S$ and regrouping terms based on the independent variations $\delta q_i$ and $\delta p_i$:
$$\delta S = \int_{t_1}^{t_2} \sum_{i=1}^n \left[ \left( \dot{q}_i - \frac{\partial H}{\partial p_i} \right) \delta p_i - \left( \dot{p}_i + \frac{\partial H}{\partial q_i} \right) \delta q_i \right] dt = 0$$
According to the fundamental lemma of the calculus of variations, if this integral is to be zero for all arbitrary and independent variations $\delta q_i(t)$ and $\delta p_i(t)$, the coefficients of each variation within the integrand must be identically zero. This gives us two sets of [first-order differential equations](@entry_id:173139):
$$\dot{q}_i = \frac{\partial H}{\partial p_i}$$
$$\dot{p}_i = - \frac{\partial H}{\partial q_i}$$
These are **Hamilton's equations of motion**. They form a system of $2n$ [first-order ordinary differential equations](@entry_id:264241) that completely describe the evolution of the system's state $(q, p)$ in phase space.

### The Hamiltonian and its Physical Meaning

We have derived Hamilton's equations from a variational principle, but what is the function $H(q, p, t)$? The Hamiltonian is not independent of the Lagrangian formalism; rather, it is constructed from it via a mathematical procedure known as the **Legendre transform**.

Given a Lagrangian $L(q, \dot{q}, t)$, we first define the [canonical momentum](@entry_id:155151) conjugate to the coordinate $q_i$ as:
$$p_i = \frac{\partial L}{\partial \dot{q}_i}$$
The Hamiltonian is then defined as:
$$H(q, p, t) = \sum_{i=1}^n p_i \dot{q}_i - L(q, \dot{q}, t)$$
Crucially, to express $H$ as a function of $(q, p, t)$, one must invert the definition of momentum to express the velocities $\dot{q}_i$ in terms of the momenta $p_i$ and coordinates $q_i$. This inversion is possible if the Lagrangian is regular, meaning the matrix of second derivatives $\frac{\partial^2 L}{\partial \dot{q}_i \partial \dot{q}_j}$ is invertible.

For a simple mechanical system where the kinetic energy is a quadratic form of [generalized velocities](@entry_id:178456), $T = \frac{1}{2} \sum_{jk} g_{jk}(q) \dot{q}_j \dot{q}_k$, and the potential energy $V(q)$ is independent of velocity, the Lagrangian is $L = T - V$. If, additionally, the [coordinate transformations](@entry_id:172727) are time-independent, the Hamiltonian becomes:
$$H = T + V$$
In this common and important case, the Hamiltonian is simply the total mechanical energy of the system. The equivalence between the second-order Euler-Lagrange equations and the first-order Hamiltonian system can be verified directly for any given system [@problem_id:2691439].

The [total time derivative](@entry_id:172646) of the Hamiltonian along a physical trajectory of the system provides profound insight into [energy conservation](@entry_id:146975). Using the chain rule and substituting Hamilton's equations:
$$\frac{dH}{dt} = \frac{\partial H}{\partial t} + \sum_{i=1}^n \left( \frac{\partial H}{\partial q_i} \dot{q}_i + \frac{\partial H}{\partial p_i} \dot{p}_i \right)$$
$$\frac{dH}{dt} = \frac{\partial H}{\partial t} + \sum_{i=1}^n \left( \frac{\partial H}{\partial q_i} \left(\frac{\partial H}{\partial p_i}\right) + \frac{\partial H}{\partial p_i} \left(-\frac{\partial H}{\partial q_i}\right) \right)$$
The terms in the summation cancel exactly, leaving a remarkably simple result [@problem_id:404156]:
$$\frac{dH}{dt} = \frac{\partial H}{\partial t}$$
This equation states that the total change in the Hamiltonian over time is equal to its explicit partial derivative with respect to time. This has a powerful consequence: **If the Hamiltonian does not explicitly depend on time ($\frac{\partial H}{\partial t} = 0$), then the Hamiltonian is a constant of motion ($H = \text{constant}$).** If $H$ also represents the total energy, this corresponds to the principle of conservation of energy.

For systems where parameters change in time, the Hamiltonian will have explicit time dependence, and energy will not be conserved. A clear example is a parametric oscillator with a time-varying frequency, $\omega(t) = \omega_0 \exp(-\gamma t)$, whose Hamiltonian is $H = \frac{p^2}{2m} + \frac{1}{2}m\omega(t)^2q^2$. In this case, energy is continuously lost from the system, and its rate of change is given by $\frac{dH}{dt} = \frac{\partial H}{\partial t} = m\omega(t)\frac{d\omega}{dt}q^2 = -m\gamma\omega_0^2 q^2 \exp(-2\gamma t)$ [@problem_id:2045101].

### Applications and Generalizations

The true power of the Hamiltonian formalism is revealed when dealing with systems that are more complex than simple point masses in a Cartesian potential.

#### Systems with Non-Standard Kinetic Energy

The clean separation of kinematic and dynamic aspects in Hamilton's equations makes them particularly well-suited for systems where the relationship between momentum and velocity is non-trivial.

Consider a model for a particle whose effective mass depends on its position, $M(q)$. The Hamiltonian might take the form $H = \frac{p^2}{2M(q)} + V(q)$ [@problem_id:2045080]. Hamilton's equations are:
$$\dot{q} = \frac{\partial H}{\partial p} = \frac{p}{M(q)}$$
$$\dot{p} = -\frac{\partial H}{\partial q} = -\left( -\frac{p^2}{2M(q)^2}M'(q) + V'(q) \right) = \frac{p^2 M'(q)}{2M(q)^2} - V'(q)$$
Notice that the equation for $\dot{p}$ contains a term that depends on momentum (or velocity squared, since $p=M(q)\dot{q}$). This term acts as a "[fictitious force](@entry_id:184453)" arising not from a potential, but from the change in inertia of the particle as it moves. The Hamiltonian method derives this term automatically and systematically.

A more profound example is the motion of particles in curved spacetimes, a cornerstone of general relativity. The kinetic energy is defined by the spacetime metric. For instance, for a particle moving in the equatorial plane of a static, spherically symmetric gravitational field, the kinetic energy can be derived from a line element of the form $ds^2 = g_{rr}(r) dr^2 + g_{\phi\phi}(r) d\phi^2$. The corresponding Hamiltonian is $H = \frac{1}{2m}(g^{rr} p_r^2 + g^{\phi\phi} p_\phi^2)$ [@problem_id:2045068]. Hamilton's equations then describe the particle's trajectory, where terms like $\frac{\partial g^{rr}}{\partial r}$ give rise to gravitational forces in the $\dot{p}_r$ equation. Furthermore, if the metric is independent of a coordinate (e.g., $\phi$), the Hamiltonian will also be independent of $\phi$, leading immediately to $\dot{p}_\phi = -\frac{\partial H}{\partial \phi} = 0$. This demonstrates that the momentum conjugate to a cyclic coordinate is conserved, a general and powerful result in Hamiltonian mechanics.

#### Multi-Particle Systems

The Hamiltonian formalism extends seamlessly to systems with many degrees of freedom. For a system of $N$ particles, the phase space is $6N$-dimensional, described by coordinates $(\vec{q}_1, \dots, \vec{q}_N)$ and momenta $(\vec{p}_1, \dots, \vec{p}_N)$. The [action functional](@entry_id:169216) is generalized as seen previously, and the variational principle yields $6N$ first-order [equations of motion](@entry_id:170720), one pair for each coordinate-momentum component.

A significant simplification occurs if the particles are non-interacting. In this case, the total Hamiltonian is simply the sum of the individual Hamiltonians for each particle: $H = \sum_{j=1}^N H_j(\vec{q}_j, \vec{p}_j)$. Because $H_j$ depends only on the coordinates of the $j$-th particle, we find:
$$\dot{\vec{q}}_k = \frac{\partial H}{\partial \vec{p}_k} = \frac{\partial H_k}{\partial \vec{p}_k}$$
$$\dot{\vec{p}}_k = -\frac{\partial H}{\partial \vec{q}_k} = -\frac{\partial H_k}{\partial \vec{q}_k}$$
The equations of motion for each particle are completely independent of all other particles [@problem_id:2045121]. This elegant [decoupling](@entry_id:160890) is a hallmark of the Hamiltonian description of [non-interacting systems](@entry_id:143064).

#### Non-Conservative Systems

While the standard Hamiltonian framework is built for [conservative systems](@entry_id:167760), it can be extended to include certain types of [dissipative forces](@entry_id:166970), such as [linear drag](@entry_id:265409). If a drag force can be derived from a **Rayleigh dissipation function**, $\mathcal{F}(\dot{q})$, the modified Euler-Lagrange equations can be used to find the corresponding modification to Hamilton's equations. The [canonical momentum](@entry_id:155151) $p$ and Hamiltonian $H$ are defined from the conservative part of the Lagrangian as usual. The equations for the [time evolution](@entry_id:153943) become [@problem_id:2045082]:
$$\dot{q} = \frac{\partial H}{\partial p}$$
$$\dot{p} = -\frac{\partial H}{\partial q} - \frac{\partial \mathcal{F}}{\partial \dot{q}}$$
The equation for $\dot{q}$ retains its canonical form, while the equation for the rate of change of momentum, $\dot{p}$, acquires an additional term representing the non-conservative, dissipative force. This demonstrates the modularity and extensibility of the Hamiltonian approach.

In summary, the derivation of Hamilton's equations from a variational principle in phase space provides a robust and versatile framework for classical mechanics. Its elegant structure not only simplifies the analysis of complex systems but also uncovers fundamental conservation laws and provides the essential language for the development of modern physics.