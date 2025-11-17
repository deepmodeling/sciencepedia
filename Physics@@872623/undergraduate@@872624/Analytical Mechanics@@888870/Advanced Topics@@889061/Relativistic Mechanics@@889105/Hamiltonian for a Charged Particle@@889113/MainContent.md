## Introduction
In the study of [analytical mechanics](@entry_id:166738), the Hamiltonian formulation offers a profound perspective on the dynamics of physical systems by shifting the focus from configuration space to the broader realm of phase space. While the Hamiltonian for simple [conservative systems](@entry_id:167760) is often a straightforward sum of kinetic and potential energies, describing a charged particle moving in an electromagnetic field presents a more intricate challenge. The magnetic force, which depends on velocity, does not derive from a simple scalar potential, requiring a more sophisticated approach rooted in the Lagrangian and the principle of [minimal coupling](@entry_id:148226). This article bridges that gap by systematically developing the Hamiltonian for a charged particle.

Over the course of three chapters, you will gain a comprehensive understanding of this fundamental concept. The first chapter, **Principles and Mechanisms**, meticulously derives the Hamiltonian from the Lagrangian, clarifying the crucial distinction between mechanical and canonical momentum and exploring the physical implications of the vector potential and gauge invariance. The second chapter, **Applications and Interdisciplinary Connections**, showcases the immense practical utility of this formalism, applying it to solve problems in [atomic physics](@entry_id:140823), [plasma confinement](@entry_id:203546), and [particle accelerator design](@entry_id:753196), and revealing its role as a bridge to modern physics. Finally, **Hands-On Practices** will allow you to solidify your understanding by tackling concrete problems, from deriving [cyclotron motion](@entry_id:276597) to analyzing particle trajectories in complex fields.

## Principles and Mechanisms

The transition from the Lagrangian to the Hamiltonian formulation of mechanics provides a powerful new perspective on dynamics, shifting the focus from configuration space to phase space. For a charged particle moving in an electromagnetic field, this transition is particularly insightful, revealing deep connections between momentum, energy, and the fundamental nature of [electromagnetic potentials](@entry_id:150802). This chapter will derive the Hamiltonian for a charged particle and explore its structure, physical interpretation, and consequences for the particle's motion.

### The Hamiltonian from Minimal Coupling

The starting point for our derivation is the standard Lagrangian for a non-relativistic particle of mass $m$ and charge $q$ moving in an electromagnetic field described by a [scalar potential](@entry_id:276177) $\phi(\vec{r}, t)$ and a [vector potential](@entry_id:153642) $\vec{A}(\vec{r}, t)$. This Lagrangian is constructed via the principle of **[minimal coupling](@entry_id:148226)**:

$L(\vec{r}, \vec{v}, t) = \frac{1}{2}m\vec{v}^{2} - q\phi(\vec{r}, t) + q\vec{v} \cdot \vec{A}(\vec{r}, t)$

Here, $\frac{1}{2}m\vec{v}^{2}$ is the kinetic energy, while the terms involving $\phi$ and $\vec{A}$ represent the interaction of the charge with the electromagnetic field. To move to the Hamiltonian formalism, we must perform a **Legendre transformation** from [generalized velocities](@entry_id:178456) ($\vec{v}$) to [generalized momenta](@entry_id:166813) ($\vec{p}$).

The first step is to define the **[canonical momentum](@entry_id:155151)** $\vec{p}$ conjugate to the position coordinate $\vec{r}$. It is defined as the partial derivative of the Lagrangian with respect to the velocity $\vec{v}$:

$\vec{p} = \frac{\partial L}{\partial \vec{v}} = \nabla_{\vec{v}} L$

Applying this definition to our Lagrangian yields:

$\vec{p} = \frac{\partial}{\partial \vec{v}} \left( \frac{1}{2}m\vec{v}^{2} - q\phi + q\vec{v} \cdot \vec{A} \right) = m\vec{v} + q\vec{A}$

This equation is of paramount importance. It reveals that for a charged particle in a magnetic field (where $\vec{A}$ is non-zero), the [canonical momentum](@entry_id:155151) $\vec{p}$ is not the same as the familiar **mechanical momentum**, which we will denote as $\vec{\pi} = m\vec{v}$. The [canonical momentum](@entry_id:155151) includes an additional term, $q\vec{A}$, that depends directly on the [vector potential](@entry_id:153642) at the particle's location.

The Hamiltonian $H$ is then defined by the Legendre transformation:

$H = \vec{p} \cdot \vec{v} - L$

To express the Hamiltonian as a function of phase space coordinates $(\vec{r}, \vec{p})$, we must eliminate the velocity $\vec{v}$. From the definition of canonical momentum, we can express $\vec{v}$ in terms of $\vec{p}$:

$\vec{v} = \frac{1}{m}(\vec{p} - q\vec{A})$

Substituting this into the definition of $H$ provides a direct, albeit algebraically intensive, path. A more elegant approach is to first simplify $H$ in terms of $\vec{v}$ and then substitute.

$H = \vec{p} \cdot \vec{v} - \left(\frac{1}{2}m\vec{v}^{2} - q\phi + q\vec{v} \cdot \vec{A}\right)$
$H = (\vec{p} - q\vec{A}) \cdot \vec{v} - \frac{1}{2}m\vec{v}^{2} + q\phi$

Using the relation $\vec{p} - q\vec{A} = m\vec{v}$, we get:

$H = (m\vec{v}) \cdot \vec{v} - \frac{1}{2}m\vec{v}^{2} + q\phi = m\vec{v}^{2} - \frac{1}{2}m\vec{v}^{2} + q\phi = \frac{1}{2}m\vec{v}^{2} + q\phi$

This intermediate result is illuminating: the value of the Hamiltonian is precisely the total energy of the particle, the sum of its kinetic energy and its [electric potential energy](@entry_id:260623). Now, to complete the transformation to phase space variables, we substitute $\vec{v} = \frac{1}{m}(\vec{p} - q\vec{A})$:

$H(\vec{r}, \vec{p}, t) = \frac{1}{2}m\left|\frac{1}{m}(\vec{p} - q\vec{A})\right|^2 + q\phi = \frac{1}{2m}|\vec{p} - q\vec{A}|^2 + q\phi$

This is the general Hamiltonian for a non-relativistic charged particle in an electromagnetic field [@problem_id:2056964] [@problem_id:2056984]. It can be written as:

$H(\vec{r}, \vec{p}, t) = \frac{(\vec{p} - q\vec{A}(\vec{r}, t))^2}{2m} + q\phi(\vec{r}, t)$

### Interpreting the Hamiltonian

The structure of this Hamiltonian is rich with physical meaning. The term $q\phi$ is clearly the potential energy due to the electric field. The term $\frac{1}{2m}(\vec{p} - q\vec{A})^2$ is the kinetic part of the Hamiltonian, and as we have seen, it corresponds to the physical kinetic energy $T = \frac{1}{2}m\vec{v}^2$.

Let's examine this kinetic term more closely by expanding the square [@problem_id:2056999]:

$T = \frac{1}{2m}(\vec{p}^2 - 2q\vec{p}\cdot\vec{A} + q^2\vec{A}^2)$

Compared to the Hamiltonian of a free particle, $H_{free} = \frac{\vec{p}^2}{2m}$, we see two new terms introduced by the [vector potential](@entry_id:153642): $-\frac{q}{m}\vec{p}\cdot\vec{A}$ and $\frac{q^2}{2m}\vec{A}^2$. The first term, linear in $\vec{p}$, represents the direct coupling between the particle's canonical momentum and the magnetic field. The second term is quadratic in $\vec{A}$.

The distinction between [canonical momentum](@entry_id:155151) $\vec{p}$ and mechanical momentum $m\vec{v}$ is crucial and can be understood through limiting cases:

1.  **Purely Electrostatic Field:** If the magnetic field is zero, we can choose a gauge where the [vector potential](@entry_id:153642) $\vec{A} = \vec{0}$ everywhere. In this case, the relationship $\vec{p} = m\vec{v} + q\vec{A}$ simplifies to $\vec{p} = m\vec{v}$ [@problem_id:2057027]. The canonical and mechanical momenta are identical. The Hamiltonian becomes $H = \frac{\vec{p}^2}{2m} + q\phi$, which is the familiar form for a particle in a conservative potential field.

2.  **Field-Free Region:** In a region completely free of electromagnetic fields, both $\phi=0$ and $\vec{A}=\vec{0}$. The Hamiltonian then reduces to that of a [free particle](@entry_id:167619), $H = \frac{\vec{p}^2}{2m}$ [@problem_id:2057006].

3.  **Purely Magnetic Field:** Consider a particle moving in a uniform magnetic field $\vec{B} = B_0 \hat{z}$ with no electric field ($\phi=0$). A possible choice of [vector potential](@entry_id:153642) is the **Landau gauge**, $\vec{A} = (-B_0 y, 0, 0)$. The [canonical momentum](@entry_id:155151) components are $p_x = mv_x - qB_0y$ and $p_y = mv_y$. The Lagrangian is independent of the coordinate $x$, making $p_x$ a conserved quantity. This conserved [canonical momentum](@entry_id:155151) is not the mechanical momentum $mv_x$, which oscillates as the particle undergoes [circular motion](@entry_id:269135). Instead, the conserved quantity $p_x$ can be shown to be directly related to the $y$-coordinate of the center of the circular orbit (the guiding center), illustrating a profound difference in the physical meaning of the two types of momentum [@problem_id:2056958].

### Equations of Motion and the Lorentz Force

A valid Hamiltonian formulation must reproduce the correct [equations of motion](@entry_id:170720). For a charged particle, this means it must yield the **Lorentz force** law. Let's verify this using Hamilton's equations:

$\dot{\vec{r}} = \frac{\partial H}{\partial \vec{p}}$ and $\dot{\vec{p}} = -\frac{\partial H}{\partial \vec{r}}$

From the first equation, we find the particle's velocity $\vec{v} = \dot{\vec{r}}$:

$\dot{r}_i = \frac{\partial H}{\partial p_i} = \frac{\partial}{\partial p_i}\left[ \frac{1}{2m}\sum_j (p_j - qA_j)^2 + q\phi \right] = \frac{1}{m}(p_i - qA_i)$

This confirms our earlier relation: $m\vec{v} = \vec{p} - q\vec{A}$.

The second equation gives the time evolution of the canonical momentum. Its derivation is more involved as both $\vec{A}$ and $\phi$ depend on $\vec{r}$. Taking the derivative component-wise gives:

$\dot{p}_i = -\frac{\partial H}{\partial r_i} = -\frac{\partial}{\partial r_i}\left[ \frac{1}{2m}\sum_j (p_j - qA_j)^2 + q\phi \right] = \frac{q}{m}\sum_j (p_j - qA_j)\frac{\partial A_j}{\partial r_i} - q\frac{\partial \phi}{\partial r_i}$

Substituting $p_j - qA_j = mv_j$, we get:

$\dot{p}_i = q\sum_j v_j \frac{\partial A_j}{\partial r_i} - q\frac{\partial \phi}{\partial r_i}$

This equation describes the rate of change of the canonical momentum. To find the force, we need the rate of change of the mechanical momentum, $\frac{d}{dt}(m\vec{v})$. Using the chain rule:

$\frac{d}{dt}(mv_i) = \frac{d}{dt}(p_i - qA_i) = \dot{p}_i - q\frac{dA_i}{dt} = \dot{p}_i - q\left(\frac{\partial A_i}{\partial t} + \sum_j \frac{\partial A_i}{\partial r_j}\dot{r}_j\right) = \dot{p}_i - q\frac{\partial A_i}{\partial t} - q\sum_j v_j\frac{\partial A_i}{\partial r_j}$

Substituting our expression for $\dot{p}_i$:

$\frac{d}{dt}(mv_i) = \left(q\sum_j v_j \frac{\partial A_j}{\partial r_i} - q\frac{\partial \phi}{\partial r_i}\right) - q\frac{\partial A_i}{\partial t} - q\sum_j v_j\frac{\partial A_i}{\partial r_j}$

Rearranging terms:

$\frac{d}{dt}(mv_i) = q\left(-\frac{\partial\phi}{\partial r_i} - \frac{\partial A_i}{\partial t}\right) + q\sum_j v_j\left(\frac{\partial A_j}{\partial r_i} - \frac{\partial A_i}{\partial r_j}\right)$

The first term is exactly the $i$-th component of the electric field, $E_i = -\nabla_i\phi - \frac{\partial A_i}{\partial t}$. The second term can be shown to be the $i$-th component of the [magnetic force](@entry_id:185340), $(\vec{v} \times \vec{B})_i$, where $\vec{B} = \nabla \times \vec{A}$. Therefore, we have successfully recovered the Lorentz force law in vector form [@problem_id:2056955]:

$\frac{d}{dt}(m\vec{v}) = q(\vec{E} + \vec{v} \times \vec{B})$

Furthermore, the formalism correctly predicts that [static magnetic fields](@entry_id:195560) do no work. In a static magnetic field with no electric field ($\phi=0$, $\partial \vec{A}/\partial t = 0$), the Hamiltonian is $H = \frac{1}{2m}(\vec{p} - q\vec{A})^2 = T$. Since the Hamiltonian does not explicitly depend on time, it is a conserved quantity, $\frac{dH}{dt}=0$. Therefore, the kinetic energy $T$ is conserved, and $\frac{dT}{dt}=0$ [@problem_id:2057001].

### The Physical Reality of the Vector Potential

The Hamiltonian formalism places the potentials $\phi$ and $\vec{A}$ on center stage, treating them as fundamental fields that define the dynamics. This perspective suggests that the vector potential $\vec{A}$ is not merely a mathematical convenience for calculating $\vec{B}$, but a physical entity in its own right. This idea is strikingly demonstrated by the Aharonov-Bohm effect.

Consider a charged particle moving in a region outside an infinitely long [solenoid](@entry_id:261182) [@problem_id:2057000]. Inside the [solenoid](@entry_id:261182), there is a constant magnetic field $\vec{B}$, but outside, $\vec{B}=\vec{0}$. However, the [vector potential](@entry_id:153642) $\vec{A}$ outside the [solenoid](@entry_id:261182) is non-zero. In cylindrical coordinates $(r, \varphi, z)$, it can be written as $\vec{A} = \frac{\Phi_B}{2\pi r}\hat{\varphi}$, where $\Phi_B$ is the total magnetic flux confined within the solenoid.

A particle moving in this region never experiences a [magnetic force](@entry_id:185340), because $\vec{B}=0$. Yet, its dynamics are affected. The Hamiltonian, with $\phi=0$, is:

$H = \frac{1}{2m}(\vec{p} - q\vec{A})^2$

In [cylindrical coordinates](@entry_id:271645), the [canonical momentum](@entry_id:155151) conjugate to the angle $\varphi$ is $p_\varphi = \frac{\partial L}{\partial \dot{\varphi}} = mr^2\dot{\varphi} + q r A_\varphi = mr^2\dot{\varphi} + \frac{q\Phi_B}{2\pi}$. The kinetic energy is $T = \frac{1}{2m}(p_r^2 + p_z^2 + \frac{(p_\varphi - q r A_\varphi)^2}{r^2})$. Substituting the expressions for the momenta, the Hamiltonian becomes:

$$H = \frac{1}{2m}\left[p_r^2 + p_z^2 + \frac{1}{r^2}\left(p_\varphi - \frac{q\Phi_B}{2\pi}\right)^2\right]$$

Even though the particle is in a field-free region, its Hamiltonian—and thus its dynamics—depends on the magnetic flux $\Phi_B$ trapped inside the [solenoid](@entry_id:261182). This demonstrates that the vector potential has observable physical consequences, a cornerstone of modern gauge theories.

### Gauge Invariance and Canonical Transformations

The electric and magnetic fields $\vec{E}$ and $\vec{B}$ are invariant under a **[gauge transformation](@entry_id:141321)** of the potentials:

$\vec{A}' = \vec{A} + \nabla\chi$
$\phi' = \phi - \frac{\partial\chi}{\partial t}$

where $\chi(\vec{r}, t)$ is an arbitrary scalar function. Since the physics described by the Lorentz force depends only on $\vec{E}$ and $\vec{B}$, the predictions of the theory must be independent of the choice of gauge. How is this reflected in the Hamiltonian formalism?

Under such a transformation, the [canonical momentum](@entry_id:155151) is not invariant. The new canonical momentum $\vec{p}'$ is related to the old one $\vec{p}$ by:

$\vec{p}' = m\vec{v} + q\vec{A}' = m\vec{v} + q(\vec{A} + \nabla\chi) = (m\vec{v} + q\vec{A}) + q\nabla\chi = \vec{p} + q\nabla\chi$

So, a [gauge transformation](@entry_id:141321) on the [vector potential](@entry_id:153642) induces a position-dependent shift in the canonical momentum [@problem_id:2057007]. This transformation, $(\vec{r}, \vec{p}) \to (\vec{r}, \vec{p} + q\nabla\chi)$, is a type of **[canonical transformation](@entry_id:158330)**. While the numerical values of the Hamiltonian and [canonical momentum](@entry_id:155151) change with the gauge, the physical content of Hamilton's equations remains the same. The form of the Hamiltonian itself is preserved, which is a key feature of this coupling. The change in the Hamiltonian is $H'-H = -q \frac{\partial\chi}{\partial t}$, which can be shown to preserve the form of the [equations of motion](@entry_id:170720). This elegant covariance of the Hamiltonian framework under [gauge transformations](@entry_id:176521) is a deep and powerful feature of the theory of electromagnetism.