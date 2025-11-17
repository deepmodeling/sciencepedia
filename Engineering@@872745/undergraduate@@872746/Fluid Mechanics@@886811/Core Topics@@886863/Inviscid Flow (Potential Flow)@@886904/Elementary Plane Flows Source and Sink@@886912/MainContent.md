## Introduction
Analyzing fluid flow, especially around complex geometries, presents a significant mathematical challenge. The theory of potential flow offers an elegant solution by simplifying the problem into manageable, fundamental components. This article delves into two of the most essential building blocks: the elementary [source and sink](@entry_id:265703) flows. By treating fluid as ideal, incompressible, and irrotational, we can define these simple patterns and combine them to construct surprisingly accurate models of real-world scenarios. This approach bypasses the complexity of direct simulation, providing powerful insights into flow behavior.

This article is structured to build your understanding progressively. The first chapter, **Principles and Mechanisms**, lays the mathematical groundwork, defining [sources and sinks](@entry_id:263105) and introducing the powerful frameworks of velocity potential, [stream function](@entry_id:266505), and complex potential. Next, in **Applications and Interdisciplinary Connections**, we will leverage the principle of superposition to model practical problems, from flow around solid bodies to groundwater management, and explore fascinating analogies in other scientific disciplines. Finally, the **Hands-On Practices** section will offer a chance to apply these concepts through guided problems, solidifying your grasp of this fundamental topic in [fluid mechanics](@entry_id:152498).

## Principles and Mechanisms

Having established the foundational assumptions of ideal, incompressible, and irrotational plane flows, we now turn to the elementary building blocks used to construct and analyze them. The core idea is to define mathematically simple [flow patterns](@entry_id:153478), known as **elementary flows**, which can be combined through superposition to model more complex and physically relevant scenarios. The most fundamental of these are the [point source](@entry_id:196698) and its counterpart, the point sink.

### The Point Source and Sink: Fundamental Singularities

A **[point source](@entry_id:196698)** is an idealized point in a [two-dimensional flow](@entry_id:266853) field from which fluid emerges uniformly in all radial directions. Conversely, a **point sink** is a point into which fluid flows radially inward. These are not physical objects but rather mathematical constructs—singularities in the flow field—that serve as powerful tools for modeling phenomena such as fluid injection from a pipe, withdrawal from a well, or the [flow patterns](@entry_id:153478) around solid bodies.

The defining characteristic of a source or sink is its **strength**, denoted by $m$. This parameter quantifies the rate at which fluid is introduced into or removed from the flow field. Specifically, the strength $m$ is related to the total [volume flow rate](@entry_id:272850) per unit depth, $Q$, that passes through any closed curve encircling the singularity. For a source, the fluid flows outward. If we consider a circle of radius $r$ centered on the source, the [radial velocity](@entry_id:159824) $v_r$ must be constant along its circumference due to symmetry. The total outward flux $Q$ is then the velocity multiplied by the circumference ($2\pi r$), giving $Q = 2\pi r v_r$.

To standardize the definition, the strength $m$ for a 2D source is typically defined as $m = Q / (2\pi)$. This leads to a simple and fundamental relationship for the [radial velocity](@entry_id:159824) at a distance $r$ from the source:

$$
v_r(r) = \frac{m}{r}
$$

Since the flow is purely radial, the tangential velocity component $v_\theta$ is zero. The velocity field vector $\mathbf{v}$ for a source at the origin can thus be expressed in polar coordinates as $\mathbf{v}(r, \theta) = (m/r) \hat{\mathbf{r}}$ or in Cartesian coordinates as [@problem_id:1752124]:

$$
\mathbf{v}(x,y) = \frac{m}{x^2+y^2} (x\hat{\mathbf{i}} + y\hat{\mathbf{j}}) = \frac{m}{r^2} \mathbf{r}
$$

where $\mathbf{r} = x\hat{\mathbf{i}} + y\hat{\mathbf{j}}$ is the position vector. A sink of strength $m$ is simply represented as a source of strength $-m$, resulting in an inward flow with velocity $v_r = -m/r$.

#### The Physical Nature of a Source: A Point of Non-Zero Divergence

In our study of [incompressible fluids](@entry_id:181066), a cornerstone is the continuity equation, which simplifies to the statement that the divergence of the velocity field is zero: $\nabla \cdot \mathbf{v} = 0$. This mathematical condition reflects the physical principle that fluid is neither created nor destroyed within the flow. The point [source and sink](@entry_id:265703) are deliberate violations of this rule. At the exact location of the source ($r=0$), the [velocity field](@entry_id:271461) is singular, and its divergence is infinite. This singularity is precisely what models the creation of fluid.

The **Divergence Theorem** provides a more rigorous interpretation. While the concept of plane flow is two-dimensional, it is illuminating to consider a three-dimensional point source as an analogy [@problem_id:1752143]. For a 3D source, the velocity field decays as $1/r^2$, and the [divergence theorem](@entry_id:145271) states that the total volumetric flux out of any closed surface $S$ is equal to the [volume integral](@entry_id:265381) of the divergence:

$$
Q_{out} = \oiint_S \mathbf{v} \cdot \hat{\mathbf{n}} \, dS = \iiint_V (\nabla \cdot \mathbf{v}) \, dV
$$

For a point source, the divergence is zero everywhere except at the origin. The theorem reveals that the integral of this singular divergence over any volume containing the source yields a constant value—the total [volumetric flow rate](@entry_id:265771) $Q$. This is the mathematical essence of a source: it is a concentrated point of positive divergence. In our 2D context, this means the line integral of the normal velocity component over any closed curve enclosing the source yields a constant flux per unit depth, $Q = 2\pi m$.

#### The Irrotational Character of Source Flow

Another crucial property of elementary flows is their rotational character, quantified by the **curl** of the velocity field, also known as **[vorticity](@entry_id:142747)** ($\boldsymbol{\omega} = \nabla \times \mathbf{v}$). For a flow to be described by a [velocity potential](@entry_id:262992), it must be **irrotational**, meaning its curl must be zero.

Let us examine the curl of a 2D source flow. In Cartesian coordinates, with $v_x = \frac{mx}{x^2+y^2}$ and $v_y = \frac{my}{x^2+y^2}$, the z-component of the curl is:

$$
(\nabla \times \mathbf{v})_z = \frac{\partial v_y}{\partial x} - \frac{\partial v_x}{\partial y} = \frac{\partial}{\partial x}\left(\frac{my}{x^2+y^2}\right) - \frac{\partial}{\partial y}\left(\frac{mx}{x^2+y^2}\right) = -\frac{2mxy}{(x^2+y^2)^2} - \left(-\frac{2mxy}{(x^2+y^2)^2}\right) = 0
$$

This calculation shows that the curl is zero everywhere except at the singularity $r=0$ [@problem_id:1752124]. Because the flow is irrotational, **Stokes' Theorem** guarantees that the **circulation**, $\Gamma = \oint_C \mathbf{v} \cdot d\mathbf{l}$, around any [simple closed path](@entry_id:178274) $C$ that does not enclose the origin is zero. This irrotational nature is what qualifies sources and sinks as **potential flows**, allowing us to use the powerful mathematical machinery of [potential theory](@entry_id:141424).

### Mathematical Frameworks for Potential Flow

The irrotational property of source/sink flows enables us to describe them using scalar [potential functions](@entry_id:176105), which are often easier to work with than vector velocity fields, especially when combining multiple flows.

#### The Velocity Potential ($\phi$)

For any [irrotational flow](@entry_id:159258), the [velocity field](@entry_id:271461) can be expressed as the gradient of a scalar function called the **[velocity potential](@entry_id:262992)**, $\phi$:

$$
\mathbf{v} = \nabla\phi
$$

In polar coordinates, this means $v_r = \partial\phi/\partial r$ and $v_\theta = (1/r)\partial\phi/\partial\theta$. For a source flow, we have $v_\theta=0$ and $v_r = m/r$. Integrating the radial component gives:

$$
\frac{\partial\phi}{\partial r} = \frac{m}{r} \quad \implies \quad \phi(r) = m \ln(r) + \text{constant}
$$

By convention, the constant is set to zero. Thus, the velocity potential for a source at the origin is $\phi(r) = m \ln(r)$, and for a sink, $\phi(r) = -m \ln(r)$. The Laplace equation $\nabla^2\phi = 0$ is satisfied for $r \neq 0$, confirming this is a valid potential flow.

#### The Stream Function ($\psi$)

An alternative but equally powerful tool is the **stream function**, $\psi$. In 2D incompressible flow, it is defined such that its derivatives give the velocity components:
*   In Cartesian coordinates: $u = \frac{\partial\psi}{\partial y}, \quad v = -\frac{\partial\psi}{\partial x}$
*   In polar coordinates: $v_r = \frac{1}{r}\frac{\partial\psi}{\partial\theta}, \quad v_\theta = -\frac{\partial\psi}{\partial r}$

The utility of the stream function is twofold. First, lines of constant $\psi$ are **[streamlines](@entry_id:266815)**—curves that are everywhere tangent to the velocity vector. Second, the difference in the value of $\psi$ between two streamlines equals the [volume flow rate](@entry_id:272850) per unit depth between them.

For a source, $v_\theta = 0$, which implies $\partial\psi/\partial r = 0$, so $\psi$ is a function of $\theta$ only. Using the [radial velocity](@entry_id:159824) component [@problem_id:1752164]:

$$
v_r = \frac{1}{r}\frac{d\psi}{d\theta} = \frac{m}{r} \quad \implies \quad \frac{d\psi}{d\theta} = m
$$

Integrating with respect to $\theta$ gives $\psi(\theta) = m\theta + \text{constant}$. Defining $\psi=0$ along the positive x-axis ($\theta=0$), we find the constant is zero. Thus, for a source at the origin, $\psi = m\theta$. For a sink, by the same logic, $\psi = -m\theta$.

#### The Complex Potential ($W(z)$)

For 2D potential flows, complex analysis provides a remarkably elegant framework. We define a complex coordinate $z = x+iy = re^{i\theta}$ and a **complex potential** $W(z) = \phi(x,y) + i\psi(x,y)$. For a source at the origin, we can combine the [velocity potential](@entry_id:262992) and [stream function](@entry_id:266505):

$$
W(z) = \phi + i\psi = m \ln(r) + i(m\theta) = m(\ln(r) + i\theta) = m \ln(re^{i\theta}) = m \ln(z)
$$

This compact expression contains all information about the flow. The velocity field can be found by differentiating $W(z)$. The **[complex velocity](@entry_id:201810)** is defined as:

$$
\frac{dW}{dz} = u - iv
$$

For a source, $\frac{dW}{dz} = \frac{m}{z}$. The fluid speed is the magnitude of this complex number, $|\mathbf{v}| = |u-iv| = |dW/dz|$.

### The Principle of Superposition: Constructing Complex Flows

The true power of elementary flows lies in the **[principle of superposition](@entry_id:148082)**. Since Laplace's equation, which governs both $\phi$ and $\psi$, is linear, the sum of any two solutions is also a solution. This means we can create complex [flow patterns](@entry_id:153478) by simply adding the potentials of elementary flows. The total velocity potential is $\phi_{total} = \sum \phi_i$, the total stream function is $\psi_{total} = \sum \psi_i$, and the total complex potential is $W_{total} = \sum W_i$. The resulting velocity field is the vector sum of the individual velocity fields, $\mathbf{v}_{total} = \sum \mathbf{v}_i$.

#### Example: The Source-Sink Pair

A classic and instructive combination is a source of strength $m$ at $(-a, 0)$ and a sink of equal strength at $(a, 0)$. This arrangement is a fundamental model for flow around a solid body known as a Rankine oval. Let's analyze this flow.

The complex potential is found by superposition [@problem_id:1752173]:
$$
W(z) = W_{source} + W_{sink} = m \ln(z+a) - m \ln(z-a) = m \ln\left(\frac{z+a}{z-a}\right)
$$

Similarly, the total [stream function](@entry_id:266505) is the sum of the individual functions [@problem_id:1752136]:
$$
\psi(x,y) = m\left[ \arctan\left(\frac{y}{x+a}\right) - \arctan\left(\frac{y}{x-a}\right) \right]
$$
(Here using the text's definition $m=Q/2\pi$).

Let's examine the velocity along the y-axis ($x=0$). Due to symmetry, we expect the flow to be directed purely along the x-axis. Calculating the velocity components $u = \partial\psi/\partial y$ and $v = -\partial\psi/\partial x$ at $x=0$ confirms that $v=0$. The horizontal velocity $u$ along the y-axis is found to be:

$$
u(0,y) = \frac{2ma}{a^2+y^2}
$$

This velocity is greatest when the denominator is smallest, which occurs at the origin ($y=0$). The maximum speed along this line is therefore $u_{max} = 2ma/a^2 = 2m/a$ [@problem_id:1752136] [@problem_id:1752173].

The superposition principle also provides an elegant way to calculate flow rates. The [volume flow rate](@entry_id:272850) per unit depth across the line segment from the origin to a point $(0, H)$ on the y-axis is given by the difference in the stream function values at the endpoints, $Q_{segment} = \psi(0,H) - \psi(0,0)$. This is often much simpler than directly integrating the [velocity field](@entry_id:271461) [@problem_id:1752166].

#### The Far-Field View and the Dipole

If we observe the source-sink pair from a distance much larger than their separation ($r \gg a$), the flow pattern simplifies. By performing a Taylor expansion on the potential function, we find that the leading-order term for the velocity potential is [@problem_id:1752181]:

$$
\phi(r, \theta) \approx \frac{2ma \cos\theta}{r}
$$

The velocity components in this far-field limit decay as $1/r^2$. This $1/r$ potential dependence and $1/r^2$ velocity decay are characteristic of a **dipole** or **doublet**. A dipole is formally the result of letting a [source and sink](@entry_id:265703) approach each other ($a \to 0$) while their strength increases ($m \to \infty$) such that the product $\mu = 2ma$, known as the **dipole moment**, remains constant. The dipole is the next fundamental building block, crucial for modeling [flow around a cylinder](@entry_id:264296).

### Physical Applications and Advanced Concepts

The abstract framework of sources and sinks finds direct application in modeling real-world problems.

#### Tracking Particle Paths

A [velocity field](@entry_id:271461) is not just a mathematical object; it dictates the motion of [massless particles](@entry_id:263424) suspended in the fluid. The velocity of a particle is simply the velocity of the fluid at the particle's current location, $\mathbf{v}_{particle} = d\mathbf{r}/dt$. This relationship allows us to calculate particle trajectories and transit times.

For instance, consider a ventilation system modeled as a 2D source, where the [radial velocity](@entry_id:159824) is $v_r = m/r$. The time $T$ required for a particle to travel from an initial radius $r_1$ to a final radius $r_2$ can be found by integrating the relation $dt = dr/v_r(r)$ [@problem_id:1752176]:

$$
T = \int_{0}^{T} dt = \int_{r_1}^{r_2} \frac{dr}{v_r(r)} = \int_{r_1}^{r_2} \frac{r}{m} dr = \frac{1}{2m} (r_2^2 - r_1^2)
$$

This direct link between the field description and [particle kinematics](@entry_id:159679) is a powerful tool for analyzing transport and mixing processes.

#### Unsteady Flow and Pressure Dynamics

While many introductory examples are steady, the potential flow framework can be extended to **unsteady flows** where the source strength varies with time, $m(t)$. In such cases, the [velocity potential](@entry_id:262992) also becomes time-dependent, $\phi(r, t)$. The pressure field can no longer be determined by the simple Bernoulli equation. Instead, we must use the **unsteady Bernoulli equation** for [irrotational flow](@entry_id:159258):

$$
\frac{P}{\rho} + \frac{\partial\phi}{\partial t} + \frac{1}{2}|\mathbf{v}|^2 = F(t)
$$

where $\rho$ is the fluid density and $F(t)$ is a function of time determined by boundary conditions. The term $\partial\phi/\partial t$ represents the pressure variation required to accelerate the fluid particles as the flow field changes. For example, if a source is activated and its strength increases linearly with time ($m(t)=kt$), the pressure at any point in the fluid will depend not only on the instantaneous velocity but also on the rate of change of the potential, reflecting the inertia of the entire fluid system [@problem_id:1752121]. This demonstrates the robustness of the potential flow model in handling more complex, time-dependent phenomena.