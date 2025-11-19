## Introduction
In the framework of general relativity, spacetime is not a passive backdrop but an active, dynamic entity represented by a mathematical structure known as a manifold. To describe physics within this paradigm, we must understand how objects move from one point to another. The paths of particles and light rays are traced out as curves on this manifold. Understanding these curves is the key to unlocking the principles of motion, causality, and gravity itself.

This article addresses the fundamental question of how to mathematically describe and interpret trajectories in the curved geometry of spacetime. We will build a comprehensive picture of motion, starting from local definitions and extending to the global paths that govern physical phenomena.

You will begin in the "Principles and Mechanisms" chapter by learning the essential tools for describing curves: the tangent vector, which defines a curve's direction at a point, and the metric tensor, which endows spacetime with geometry and [causal structure](@entry_id:159914). You will then discover geodesics, the "straightest possible" paths that particles follow in the absence of external forces. The "Applications and Interdisciplinary Connections" chapter will demonstrate the power of these concepts by applying them to tangible scenarios, from the behavior of light and matter around black holes to the large-scale dynamics of the cosmos. Finally, the "Hands-On Practices" section will provide opportunities to solidify your understanding by working through concrete problems related to these foundational ideas.

## Principles and Mechanisms

In the preceding chapter, we introduced the concept of a manifold as the fundamental mathematical stage for the events of spacetime. We now turn our attention to the actors on this stage: particles and [light rays](@entry_id:171107). Their histories are traced out as paths, or **curves**, on the [spacetime manifold](@entry_id:262092). Understanding the properties of these curves is essential for describing motion, causality, and the very fabric of gravitational physics. This chapter will develop the principles governing these curves, from the local properties defined by [tangent vectors](@entry_id:265494) to the global properties of paths that dictate physical motion.

### Tangent Vectors and the Metric

A curve on a manifold is formally a map from a real interval into the manifold, $x^{\mu}(\lambda)$, where $\lambda$ is a parameter along the curve. The most immediate characterization of a curve at a particular point is its direction and "speed" with respect to the parameter $\lambda$. This information is captured by the **[tangent vector](@entry_id:264836)**, defined as the derivative of the coordinate functions with respect to the parameter:

$$
U^{\mu} = \frac{dx^{\mu}}{d\lambda}
$$

The components $U^{\mu}$ represent the rate of change of each coordinate $x^{\mu}$ as we move along the curve. The collection of all possible [tangent vectors](@entry_id:265494) at a single point on the manifold forms a vector space known as the [tangent space](@entry_id:141028).

While the tangent vector tells us the direction of a curve, it is the **metric tensor**, $g_{\mu\nu}$, that endows the manifold with a notion of distance and geometry. The metric allows us to compute the invariant magnitude, or norm, of a [tangent vector](@entry_id:264836). The squared [norm of a vector](@entry_id:154882) $U^{\mu}$ is given by the [scalar product](@entry_id:175289):

$$
\|U\|^{2} = g_{\mu\nu} U^{\mu} U^{\nu}
$$

This quantity is a scalar, meaning it has the same value for all observers. To build intuition, consider a simple two-dimensional curved manifold: the surface of a sphere of radius $R$. In standard [spherical coordinates](@entry_id:146054) $(\theta, \phi)$, the line element is $ds^2 = R^2(d\theta^2 + \sin^2\theta d\phi^2)$, which tells us the metric components are $g_{\theta\theta} = R^2$ and $g_{\phi\phi} = R^2\sin^2\theta$.

Let us examine a curve of constant latitude, where $\theta = \theta_0$ is fixed. We can naturally parameterize this path by the azimuthal angle, $\lambda = \phi$. The coordinates of the curve are $x^\mu(\phi) = (\theta_0, \phi)$. The [tangent vector](@entry_id:264836) has components $\frac{d\theta}{d\phi} = 0$ and $\frac{d\phi}{d\phi} = 1$. The squared norm of this tangent vector is:

$$
\|T\|^{2} = g_{\theta\theta}\left(\frac{d\theta}{d\phi}\right)^{2} + g_{\phi\phi}\left(\frac{d\phi}{d\phi}\right)^{2} = R^2(0)^2 + R^2\sin^2\theta_0(1)^2 = R^2\sin^2\theta_0
$$

This result is geometrically intuitive: the circumference of a latitude circle is $2\pi (R\sin\theta_0)$, and our tangent vector's magnitude reflects this effective radius. For a path along the equator ($\theta_0 = \pi/2$), the squared norm is simply $R^2$. If the curve were instead parameterized by $\phi(\lambda) = \omega\lambda$ for some constant $\omega$, the [tangent vector](@entry_id:264836) components would be $\frac{d\theta}{d\lambda} = 0$ and $\frac{d\phi}{d\lambda} = \omega$. The magnitude would then be $\sqrt{R^2\sin^2(\pi/2) \omega^2} = R\omega$, directly proportional to the "[angular velocity](@entry_id:192539)" $\omega$. These examples demonstrate a crucial point: the metric is the essential tool for translating coordinate-dependent velocity components into an invariant geometric length.

### Causal Structure of Spacetime

When we move from a purely spatial manifold like a sphere to a Lorentzian manifold representing spacetime, the concept of a vector's norm acquires a profound physical meaning related to causality. Throughout this text, we will adopt the **spacetime signature** $(-,+,+,+)$. This means that in the flat Minkowski space of special relativity, the line element is $ds^2 = -c^2 dt^2 + dx^2 + dy^2 + dz^2$, and the metric tensor is $\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1)$ in units where $c=1$. Note that the alternative signature $(+,-,-,-)$ is also common in the literature; this choice reverses the sign of all squared norms.

With our chosen signature, the squared norm of a [tangent vector](@entry_id:264836) $V^\mu$ classifies it into one of three categories, determining its causal nature:

*   **Timelike:** $g_{\mu\nu}V^{\mu}V^{\nu}  0$. A tangent vector is timelike if it points within the future or past light cone. Curves whose tangent vectors are everywhere timelike can represent the trajectories of massive particles, which must travel slower than light.

*   **Spacelike:** $g_{\mu\nu}V^{\mu}V^{\nu}  0$. A [tangent vector](@entry_id:264836) is spacelike if it points outside the [light cone](@entry_id:157667). A spacelike curve connects events that are causally disconnected; one cannot be reached from the other without exceeding the speed of light.

*   **Null (or Lightlike):** $g_{\mu\nu}V^{\mu}V^{\nu} = 0$. A [tangent vector](@entry_id:264836) is null if it lies directly on the [light cone](@entry_id:157667). Null curves represent the trajectories of [massless particles](@entry_id:263424), such as photons, which travel at the speed of light.

To illustrate this, consider a hypothetical curve in Minkowski space parameterized by $\lambda$: $x^{\mu}(\lambda) = (a\cosh\lambda, a\sinh\lambda, 0, 0)$. First, we find the [tangent vector](@entry_id:264836) $U^\mu = dx^\mu/d\lambda$:
$$
U^{\mu} = \left(a\sinh\lambda, a\cosh\lambda, 0, 0\right)
$$
Now, we calculate its squared norm using the Minkowski metric $\eta_{\mu\nu} = \text{diag}(-1, 1, 1, 1)$:
$$
\eta_{\mu\nu} U^{\mu} U^{\nu} = -(U^0)^2 + (U^1)^2 + (U^2)^2 + (U^3)^2 = -(a\sinh\lambda)^2 + (a\cosh\lambda)^2
$$
Using the identity $\cosh^2\lambda - \sinh^2\lambda = 1$, we find:
$$
\eta_{\mu\nu} U^{\mu} U^{\nu} = a^2(\cosh^2\lambda - \sinh^2\lambda) = a^2
$$
Since $a$ is a positive constant, $a^2  0$. The tangent vector is therefore **spacelike** for all values of $\lambda$, meaning this curve represents a path of causally disconnected points and cannot be the [worldline](@entry_id:199036) of any physical object.

### Worldlines, Proper Time, and 4-Velocity

The trajectory of a physical object through spacetime is its **[worldline](@entry_id:199036)**. As established, the worldline of a massive particle must be a [timelike curve](@entry_id:637389), while that of a massless particle must be a null curve.

#### Massive Particles and Proper Time

For a massive particle traveling along a timelike worldline, we can define a physically meaningful parameter: the **[proper time](@entry_id:192124)**, $\tau$. This is the time measured by a clock carried along with the particle. The differential interval of proper time, $d\tau$, is related to the invariant line element $ds$ by:

$$
c^2 d\tau^2 = -ds^2 = -g_{\mu\nu} dx^{\mu} dx^{\nu}
$$

The negative sign is necessary because for a timelike path, $ds^2  0$. In a [local inertial frame](@entry_id:275479) (Minkowski coordinates), this becomes $c^2 d\tau^2 = c^2 dt^2 - (dx^2 + dy^2 + dz^2)$. Dividing by $dt^2$, we can relate the [proper time](@entry_id:192124) interval to the [coordinate time](@entry_id:263720) interval $dt$:

$$
c^2 \left(\frac{d\tau}{dt}\right)^2 = c^2 - \left(\frac{dx}{dt}\right)^2 - \left(\frac{dy}{dt}\right)^2 - \left(\frac{dz}{dt}\right)^2 = c^2 - v^2
$$
where $v$ is the instantaneous spatial speed of the particle. This yields the famous **time dilation** formula:

$$
\frac{d\tau}{dt} = \sqrt{1 - \frac{v^2}{c^2}} = \frac{1}{\gamma}
$$

The total proper time elapsed for a particle along a path from event A to event B is found by integrating this expression: $\Delta\tau = \int_A^B d\tau = \int_{t_A}^{t_B} \sqrt{1 - v(t)^2/c^2} \, dt$. For a particle undergoing non-uniform motion, such as [simple harmonic motion](@entry_id:148744) $x(t) = A\sin(\omega t)$, the total [proper time](@entry_id:192124) elapsed during one period $T = 2\pi/\omega$ is less than $T$, as its speed is continuously changing. The calculation involves an integral that evaluates to an elliptic function, demonstrating how time dilation accumulates over a complex trajectory.

When a particle's [worldline](@entry_id:199036) is parameterized by its own [proper time](@entry_id:192124) $\tau$, the resulting tangent vector is called the **[4-velocity](@entry_id:261095)**:

$$
U^{\mu} = \frac{dx^{\mu}}{d\tau}
$$

The [4-velocity](@entry_id:261095) is a central object in [relativistic mechanics](@entry_id:263483). Let's find its norm. From the definition of [proper time](@entry_id:192124), we can write $g_{\mu\nu} \frac{dx^\mu}{d\tau} \frac{dx^\nu}{d\tau} = \frac{ds^2}{d\tau^2} = -c^2$. Thus, the squared norm of the [4-velocity](@entry_id:261095) is a universal constant:

$$
g_{\mu\nu} U^{\mu} U^{\nu} = -c^2
$$

In units where $c=1$, the [4-velocity](@entry_id:261095) is a unit timelike vector with $U_\mu U^\mu = -1$. Furthermore, since [coordinate time](@entry_id:263720) $t$ is generally taken to increase into the future for a physical particle, and $d\tau$ is positive by convention, the time component of the [4-velocity](@entry_id:261095), $U^0 = dt/d\tau = \gamma c$, is always positive. A non-[spacelike vector](@entry_id:636555) with a positive time component is called **future-pointing**. Therefore, the [4-velocity](@entry_id:261095) of any massive particle is a future-pointing, unit timelike vector.

#### Massless Particles and Affine Parameters

The worldlines of massless particles like photons are **null curves**, meaning $ds^2=0$ along their entire trajectory. This immediately implies that proper time cannot be used as a parameter, since $d\tau$ would be zero. Instead, we use a more general **affine parameter**, typically denoted $\lambda$. An affine parameter is one for which the [geodesic equation](@entry_id:136555) (to be discussed shortly) takes its simplest form.

To find the path of a light ray in a given spacetime, we simply set the [line element](@entry_id:196833) to zero, $ds^2=0$. For instance, in a hypothetical spacetime with the metric $ds^2 = -(\alpha \rho)^2 c^2 d\tau^2 + d\rho^2$, a light ray's path is governed by $d\rho/d\tau = \pm \alpha \rho c$. By integrating this equation, one can trace the path of light signals, for example, on a round trip between two points, and ultimately calculate elapsed time for observers.

A simple example of a null curve in flat spacetime is the path of a photon moving in the $xy$-plane, given by $x^\mu(\lambda) = (k\lambda, k\lambda\cos\alpha, k\lambda\sin\alpha, 0)$, where $k$ and $\alpha$ are constants. The [tangent vector](@entry_id:264836) is $U^\mu = (k, k\cos\alpha, k\sin\alpha, 0)$. Its squared norm is:

$$
\eta_{\mu\nu} U^{\mu} U^{\nu} = -(k)^2 + (k\cos\alpha)^2 + (k\sin\alpha)^2 + 0 = -k^2 + k^2(\cos^2\alpha + \sin^2\alpha) = 0
$$
This confirms that the tangent vector is null, as expected for a photon.

### Geodesics: The Straightest Possible Paths

We have characterized the types of curves that can represent physical objects, but which specific paths do they follow? In the absence of non-gravitational forces, both massive and [massless particles](@entry_id:263424) travel along **geodesics**. A geodesic is the straightest possible path on a manifold.

For massive particles, this corresponds to the path of **maximal proper time** between two spacetime events—a principle known as extremal aging. The path a particle follows can be found by extremizing the [proper time](@entry_id:192124) functional $S = \int d\tau = \int \sqrt{-g_{\mu\nu}\dot{x}^\mu \dot{x}^\nu} \, d\lambda$. A simpler but equivalent approach is to extremize the functional for the squared length, using the Lagrangian $L = g_{\mu\nu}\dot{x}^\mu \dot{x}^\nu$, where dots denote differentiation with respect to an affine parameter $\lambda$. The equations of motion are then given by the Euler-Lagrange equations:

$$
\frac{d}{d\lambda}\left(\frac{\partial L}{\partial \dot{x}^\alpha}\right) - \frac{\partial L}{\partial x^\alpha} = 0
$$

These are the **[geodesic equations](@entry_id:264349)**. They describe how a particle's velocity vector changes as it moves through a curved spacetime, encoding the effects of gravity. For example, in a 'toy universe' with the metric $ds^2 = -(1+ky)^2 c^2 dt^2 + dy^2$, the Lagrangian is $L = -(1+ky)^2 c^2 \dot{t}^2 + \dot{y}^2$. Applying the Euler-Lagrange equation for the $y$ coordinate yields:

$$
\frac{d}{d\lambda}(2\dot{y}) - (-2k(1+ky)c^2\dot{t}^2) = 0 \quad \implies \quad \ddot{y} = -kc^2(1+ky)\dot{t}^2
$$

This result shows a particle experiences an "acceleration" in the $y$-direction that depends on its position $y$ and its velocity in the time direction. This is a manifestation of a fictitious gravitational force in this particular coordinate system, arising entirely from the geometry of the spacetime.

### Symmetries and Conserved Quantities

Solving the full set of [geodesic equations](@entry_id:264349) can be complicated. However, if the spacetime possesses symmetries, our task can be greatly simplified. According to **Noether's theorem**, every [continuous symmetry](@entry_id:137257) of a physical system corresponds to a conserved quantity. In general relativity, a symmetry of the spacetime is represented by a **Killing vector field**.

A Killing vector field $\xi^\mu$ describes a direction along which the metric does not change. In practical terms, if the metric components $g_{\mu\nu}$ in a given coordinate system do not depend on a particular coordinate $x^\alpha$, then the vector field corresponding to translations in that direction, $\partial_\alpha$ (which has components $\xi^\alpha = 1$ and $\xi^\beta = 0$ for $\beta \neq \alpha$), is a Killing vector.

The key result is that for any particle traveling along a geodesic with [4-velocity](@entry_id:261095) $U^\mu$, the quantity formed by projecting the [4-velocity](@entry_id:261095) onto a Killing vector is conserved:

$$
C = g_{\mu\nu} U^{\mu} \xi^{\nu} = \text{constant}
$$

Consider a spacetime used to model rotation, with the line element $ds^2 = -dt^2 + dr^2 + r^2 d\phi^2 + dz^2 + 2\omega r^2 dt d\phi$. The metric components do not depend on the coordinates $t$ or $\phi$. This implies the existence of two Killing vectors, $\xi_{(t)} = \partial_t$ and $\xi_{(\phi)} = \partial_\phi$. These correspond to two [conserved quantities](@entry_id:148503) for a particle on a geodesic:

1.  Conserved energy per unit mass, $E = -g_{\mu\nu}U^\mu \xi_{(t)}^\nu = -g_{t\mu}U^\mu = -(-U^t + \omega r^2 U^\phi) = U^t - \omega r^2 U^\phi$.
2.  Conserved angular momentum per unit mass, $L_z = g_{\mu\nu}U^\mu \xi_{(\phi)}^\nu = g_{\phi\mu}U^\mu = \omega r^2 U^t + r^2 U^\phi$.

These conservation laws provide powerful algebraic constraints on the motion. If we know the particle's [4-velocity](@entry_id:261095) and position at one point on its trajectory, we can compute $E$ and $L_z$. Then, if we later observe the particle at a new position, we can use these conserved values to determine components of its new [4-velocity](@entry_id:261095) without having to integrate the full [equations of motion](@entry_id:170720). This technique is an indispensable tool in the study of particle orbits in symmetric spacetimes, such as those around stars and black holes.