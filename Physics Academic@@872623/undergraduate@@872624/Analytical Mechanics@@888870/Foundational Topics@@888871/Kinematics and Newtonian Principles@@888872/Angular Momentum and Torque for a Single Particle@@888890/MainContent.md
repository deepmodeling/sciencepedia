## Introduction
In the study of dynamics, the principles of [linear momentum](@entry_id:174467) and force provide a complete description of [translational motion](@entry_id:187700). However, to understand the universe of rotating, orbiting, and spinning objects, we must extend this framework to describe rotational motion. This requires the introduction of two new fundamental concepts: **angular momentum**, the rotational analog of linear momentum, and **torque**, the rotational analog of force. This article provides a comprehensive introduction to these quantities for a single particle, addressing the knowledge gap between translational and [rotational dynamics](@entry_id:267911).

The journey begins in the "Principles and Mechanisms" chapter, where we will rigorously define angular momentum and torque. We will derive the fundamental law connecting them—the rotational equivalent of Newton's second law—and explore its profound implication: the principle of [conservation of angular momentum](@entry_id:153076). Building on this foundation, the "Applications and Interdisciplinary Connections" chapter will demonstrate the remarkable power and reach of these concepts, showing how they provide crucial insights into everything from the [orbital mechanics](@entry_id:147860) of planets and black holes to the quantum behavior of elementary particles. Finally, the "Hands-On Practices" section will solidify your understanding by guiding you through practical problems that apply these theoretical principles to concrete physical scenarios. Together, these sections will equip you with a robust understanding of the building blocks of [rotational dynamics](@entry_id:267911).

## Principles and Mechanisms

In our study of [translational motion](@entry_id:187700), the concept of [linear momentum](@entry_id:174467), $\mathbf{p}$, and its relationship to force, $\mathbf{F} = \dot{\mathbf{p}}$, provides the fundamental framework for dynamics. We now turn our attention to [rotational motion](@entry_id:172639), for which we must develop an analogous set of principles. The central quantities in this new framework will be **angular momentum** and **torque**. This chapter will define these vector quantities for a single particle and derive the fundamental law that governs their relationship, leading to one of the most powerful conservation principles in physics.

### Defining Angular Momentum

Consider a single particle of mass $m$ moving through space. At a given instant, its position relative to a chosen fixed origin $O$ is described by the position vector $\mathbf{r}$, and it moves with velocity $\mathbf{v}$, giving it a [linear momentum](@entry_id:174467) $\mathbf{p} = m\mathbf{v}$.

The **angular momentum** $\mathbf{L}$ of the particle about the origin $O$ is defined as the [vector cross product](@entry_id:156484) of its position vector and its linear momentum vector:

$$
\mathbf{L} = \mathbf{r} \times \mathbf{p}
$$

Like linear momentum, angular momentum is a vector quantity, possessing both magnitude and direction. Its magnitude is given by $|\mathbf{L}| = |\mathbf{r}| |\mathbf{p}| \sin\phi = rp\sin\phi$, where $\phi$ is the angle between the vectors $\mathbf{r}$ and $\mathbf{p}$. This can be interpreted in two ways: as the product of the particle's linear momentum and the perpendicular distance from the origin to the line of motion ($r_{\perp} = r \sin\phi$), or as the product of the particle's distance from the origin and the component of its momentum perpendicular to the [position vector](@entry_id:168381) ($p_{\perp} = p \sin\phi$). The direction of $\mathbf{L}$ is perpendicular to the plane formed by $\mathbf{r}$ and $\mathbf{p}$, determined by the right-hand rule. This direction represents the axis about which the particle is instantaneously rotating relative to the origin.

It is instructive to relate the physical quantity of angular momentum to the geometry of the particle's motion. We can define an [instantaneous angular velocity](@entry_id:171936) of the particle's [position vector](@entry_id:168381), $\boldsymbol{\omega}$, as $\boldsymbol{\omega} = (\mathbf{r} \times \mathbf{v}) / r^2$. Substituting the definition of linear momentum, $\mathbf{p} = m\mathbf{v}$, into the definition of angular momentum, we find a direct relationship:

$$
\mathbf{L} = \mathbf{r} \times (m\mathbf{v}) = m(\mathbf{r} \times \mathbf{v}) = m r^2 \left( \frac{\mathbf{r} \times \mathbf{v}}{r^2} \right) = (mr^2)\boldsymbol{\omega}
$$

This equation reveals that the angular momentum $\mathbf{L}$ is always parallel to this [instantaneous angular velocity](@entry_id:171936) vector $\boldsymbol{\omega}$, regardless of the particle's trajectory [@problem_id:2031848]. The scalar proportionality factor, $I = mr^2$, is known as the **moment of inertia** of the particle about the origin. This establishes a powerful analogy with linear motion: just as linear momentum is mass times linear velocity ($\mathbf{p} = m\mathbf{v}$), angular momentum is moment of inertia times angular velocity ($\mathbf{L} = I\boldsymbol{\omega}$). However, it is crucial to remember that for a single particle, $I$ is not generally constant, as it depends on the particle's distance $r$ from the origin.

### Torque: The Cause of Change in Angular Momentum

Having defined angular momentum, we must ask what causes it to change. For [linear momentum](@entry_id:174467), the agent of change is force, as described by Newton's second law, $\dot{\mathbf{p}} = \mathbf{F}$. We seek a similar relationship for [rotational dynamics](@entry_id:267911). Let us investigate the time rate of change of the angular momentum vector:

$$
\frac{d\mathbf{L}}{dt} = \frac{d}{dt}(\mathbf{r} \times \mathbf{p})
$$

Using the product rule for derivatives of a cross product, we get:

$$
\frac{d\mathbf{L}}{dt} = \left(\frac{d\mathbf{r}}{dt} \times \mathbf{p}\right) + \left(\mathbf{r} \times \frac{d\mathbf{p}}{dt}\right)
$$

The first term involves $\frac{d\mathbf{r}}{dt} = \mathbf{v}$ and $\mathbf{p} = m\mathbf{v}$. Thus, this term is $\mathbf{v} \times (m\mathbf{v}) = m(\mathbf{v} \times \mathbf{v})$. Since the [cross product](@entry_id:156749) of any vector with itself is zero, this term vanishes entirely. This is a remarkable and crucial simplification.

The second term involves $\frac{d\mathbf{p}}{dt}$, which by Newton's second law is simply the [net force](@entry_id:163825) $\mathbf{F}$ acting on the particle. So, the second term becomes $\mathbf{r} \times \mathbf{F}$.

This leads us to the fundamental equation of [rotational dynamics](@entry_id:267911) for a single particle. We define the **torque** $\boldsymbol{\tau}$ (also called the moment of the force) about the origin $O$ as:

$$
\boldsymbol{\tau} = \mathbf{r} \times \mathbf{F}
$$

The time derivative of the angular momentum is therefore equal to the net external torque:

$$
\frac{d\mathbf{L}}{dt} = \boldsymbol{\tau}
$$

This equation is the rotational analogue of $\dot{\mathbf{p}} = \mathbf{F}$. It states that the rate of change of a particle's angular momentum about a point is equal to the [net torque](@entry_id:166772) applied to it about that same point. If there is a [net torque](@entry_id:166772), the angular momentum vector will change over time; if there is no [net torque](@entry_id:166772), the angular momentum vector will remain constant.

Calculating the torque is a straightforward application of the [cross product](@entry_id:156749). For instance, if a particle's motion is governed by a potential energy field $V(\mathbf{r})$, the [conservative force](@entry_id:261070) is $\mathbf{F} = -\nabla V$. The torque is then $\boldsymbol{\tau} = \mathbf{r} \times (-\nabla V)$. Consider a particle moving in the $xy$-plane under a potential $V(x, y) = Cxy$. The force is $\mathbf{F} = -\nabla V = -Cy\hat{\mathbf{i}} - Cx\hat{\mathbf{j}}$. The torque about the origin is then calculated as $\boldsymbol{\tau} = \mathbf{r} \times \mathbf{F} = (x\hat{\mathbf{i}} + y\hat{\mathbf{j}}) \times (-Cy\hat{\mathbf{i}} - Cx\hat{\mathbf{j}})$. The resulting torque vector is $\boldsymbol{\tau} = C(y^2 - x^2)\hat{\mathbf{k}}$ [@problem_id:2031837]. Notice that the torque is perpendicular to the plane of motion.

Alternatively, if the trajectory $\mathbf{r}(t)$ of a particle is known, we can deduce the [net torque](@entry_id:166772) acting on it by first calculating its acceleration, $\mathbf{a}(t) = \ddot{\mathbf{r}}(t)$. From Newton's second law, $\mathbf{F} = m\mathbf{a}$, so the torque is given by $\boldsymbol{\tau}(t) = \mathbf{r}(t) \times (m\mathbf{a}(t))$. For example, an ion trapped in an electromagnetic field might follow a helical path such as $\mathbf{r}(t) = A\cos(\omega t)\hat{\mathbf{i}} + B\sin(\omega t)\hat{\mathbf{j}} + Ct\hat{\mathbf{k}}$. By twice differentiating this position vector to find the acceleration $\mathbf{a}(t)$ and then computing the cross product $\mathbf{r} \times \mathbf{a}$, one can determine the time-varying torque required to maintain this specific trajectory [@problem_id:2031857].

### The Principle of Conservation of Angular Momentum

The relationship $\dot{\mathbf{L}} = \boldsymbol{\tau}$ immediately leads to one of the most fundamental [conservation laws in physics](@entry_id:266475).

**If the net external torque on a particle about a fixed origin is zero, then the angular momentum of the particle about that origin is conserved.**

That is, if $\boldsymbol{\tau} = \mathbf{0}$, then $\frac{d\mathbf{L}}{dt} = \mathbf{0}$, which implies $\mathbf{L} = \text{constant}$.

This conservation of a vector quantity implies that both its magnitude and its direction are constant. The condition for zero torque, $\boldsymbol{\tau} = \mathbf{r} \times \mathbf{F} = \mathbf{0}$, occurs under two primary circumstances:
1.  The net force on the particle is zero ($\mathbf{F} = \mathbf{0}$).
2.  The [net force](@entry_id:163825) vector $\mathbf{F}$ is parallel (or anti-parallel) to the position vector $\mathbf{r}$.

The first case is straightforward. A particle moving freely in space with constant velocity $\mathbf{v}$ experiences no force. Its angular momentum $\mathbf{L} = m(\mathbf{r} \times \mathbf{v})$ is constant. Even though its [position vector](@entry_id:168381) $\mathbf{r}(t) = \mathbf{r}_0 + \mathbf{v}t$ is changing with time, a direct calculation shows that the time-dependent terms cancel, leaving a constant angular momentum vector whose magnitude depends on the initial position and velocity [@problem_id:2031844].

The second case, where $\mathbf{F}$ is always parallel to $\mathbf{r}$, is of profound importance. A force with this property is called a **[central force](@entry_id:160395)**. A central force can be written in the form $\mathbf{F} = f(r, \theta, \phi)\hat{\mathbf{r}}$, where $\hat{\mathbf{r}}$ is the radial unit vector. The torque is then $\boldsymbol{\tau} = \mathbf{r} \times \mathbf{F} = (r\hat{\mathbf{r}}) \times (f\hat{\mathbf{r}}) = \mathbf{0}$. Therefore, **the [angular momentum of a particle](@entry_id:178745) is always conserved under the action of a [central force](@entry_id:160395).** The gravitational force and the electrostatic Coulomb force are two paramount examples of [central forces](@entry_id:267832).

In general, for any force field expressed in polar coordinates as $\mathbf{F} = F_r \hat{\mathbf{r}} + F_\theta \hat{\mathbf{\theta}}$, the torque about the origin is $\boldsymbol{\tau} = \mathbf{r} \times \mathbf{F} = (r\hat{\mathbf{r}}) \times (F_r \hat{\mathbf{r}} + F_\theta \hat{\mathbf{\theta}}) = r F_\theta (\hat{\mathbf{r}} \times \hat{\mathbf{\theta}}) = r F_\theta \hat{\mathbf{k}}$. Thus, the torque depends exclusively on the azimuthal component of the force, $F_\theta$. Angular momentum is conserved if and only if this component is zero for all possible particle positions [@problem_id:2031851].

#### Consequences of Angular Momentum Conservation

The conservation of the angular momentum vector $\mathbf{L}$ has two powerful geometric consequences for the particle's trajectory.

First, since the vector $\mathbf{L} = \mathbf{r} \times \mathbf{p}$ is constant, the position vector $\mathbf{r}$ must always be perpendicular to this fixed direction in space. This means that **motion under a [central force](@entry_id:160395) is confined to a plane** that passes through the origin and is perpendicular to the constant angular momentum vector $\mathbf{L}$.

Second, the constant magnitude of $\mathbf{L}$ has a direct link to the area swept out by the position vector. In an infinitesimal time interval $dt$, the particle moves by $d\mathbf{r} = \mathbf{v} dt$. The small triangular area $dA$ swept by the [position vector](@entry_id:168381) $\mathbf{r}$ is half the area of the parallelogram formed by $\mathbf{r}$ and $d\mathbf{r}$:

$$
dA = \frac{1}{2} |\mathbf{r} \times d\mathbf{r}| = \frac{1}{2} |\mathbf{r} \times \mathbf{v} dt| = \frac{1}{2m} |\mathbf{r} \times m\mathbf{v}| dt = \frac{|\mathbf{L}|}{2m} dt
$$

The rate at which area is swept out, known as the **areal velocity**, is therefore:

$$
\frac{dA}{dt} = \frac{L}{2m}
$$

where $L = |\mathbf{L}|$. If angular momentum is conserved, $L$ is constant, and thus the areal velocity is also constant [@problem_id:2031831]. This is famously known as **Kepler's Second Law of Planetary Motion**: a line joining a planet and the Sun sweeps out equal areas during equal intervals of time. We now see this is not just a law for planets but a general consequence of motion under any [central force](@entry_id:160395).

### Advanced Topics and Applications

#### Impulsive Torque and Angular Impulse

Just as an impulse $\mathbf{J} = \int \mathbf{F} dt$ describes the change in [linear momentum](@entry_id:174467), we can define an **[angular impulse](@entry_id:166396)** as the integral of torque over time. Integrating the rotational law of motion gives:

$$
\Delta \mathbf{L} = \mathbf{L}_f - \mathbf{L}_i = \int_{t_i}^{t_f} \boldsymbol{\tau} dt = \int_{t_i}^{t_f} (\mathbf{r} \times \mathbf{F}) dt
$$

For a "sharp impulse" where the force is applied over a very short time interval, the particle's position vector $\mathbf{r}$ can be treated as constant during the impulse. In this case, the change in angular momentum is simply:

$$
\Delta \mathbf{L} \approx \mathbf{r} \times \left(\int \mathbf{F} dt\right) = \mathbf{r} \times \mathbf{J}
$$

From this, it is clear that if an impulse $\mathbf{J}$ is delivered to a particle at position $\mathbf{r}$, its angular momentum about the origin will remain unchanged ($\Delta \mathbf{L} = \mathbf{0}$) if and only if the impulse vector is parallel to the [position vector](@entry_id:168381) ($\mathbf{J} \parallel \mathbf{r}$), as this makes their [cross product](@entry_id:156749) zero [@problem_id:2031821].

#### Precession of Angular Momentum

What happens if the torque is not zero, but has a specific relationship to the angular momentum? A particularly interesting case is when the torque vector is consistently perpendicular to the angular momentum vector. Such a torque cannot change the magnitude of $\mathbf{L}$ (since $d(L^2)/dt = d(\mathbf{L} \cdot \mathbf{L})/dt = 2\mathbf{L} \cdot \dot{\mathbf{L}} = 2\mathbf{L} \cdot \boldsymbol{\tau} = 0$), but it will change its direction. This causes the angular momentum vector to rotate, a phenomenon known as **precession**.

A beautiful physical example occurs in orbital mechanics when a dominant [central potential](@entry_id:148563) is perturbed by a smaller, non-central term. For a particle in a nearly [circular orbit](@entry_id:173723) under a potential like $U(r, \theta) = U_0(r) + U_1(r, \theta)$, the non-central part $U_1$ can generate a small, persistent torque. If this torque, when averaged over an orbit, is perpendicular to the time-averaged angular momentum vector, it will cause the orbital plane to precess. This is known as nodal precession. The rate of this precession can be calculated from the properties of the perturbing potential and the orbit itself, providing a powerful tool to analyze complex gravitational and electromagnetic systems [@problem_id:2031817].

#### Symmetry and Conservation in Hamiltonian Mechanics

The connection between the absence of torque and the [conservation of angular momentum](@entry_id:153076) is an example of a much deeper principle articulated by Noether's theorem: every [continuous symmetry](@entry_id:137257) of a physical system corresponds to a conserved quantity. For angular momentum, the relevant symmetry is **[rotational invariance](@entry_id:137644)**.

This can be seen clearly in the Hamiltonian formulation of mechanics. The [time evolution](@entry_id:153943) of any quantity $A(q,p)$ is given by $\frac{dA}{dt} = \{A, H\} + \frac{\partial A}{\partial t}$, where $\{A, H\}$ is the Poisson bracket. For the $z$-component of angular momentum, $L_z = xp_y - yp_x$, its time derivative is $\dot{L}_z = \{L_z, H\}$. If the Hamiltonian $H$ is invariant under rotations about the $z$-axis, then $L_z$ will be conserved.

Consider a potential $V(x, y, z) = C(x^2+y^2+z^2) + Kxy$. The term $C(x^2+y^2+z^2) = Cr^2$ is spherically symmetric and thus invariant under any rotation. The term $Kxy$, however, is not invariant under a general rotation about the $z$-axis. A direct calculation using Hamilton's equations or Poisson brackets shows that $\frac{dL_z}{dt} = K(y^2-x^2)$ [@problem_id:2031852]. This rate of change is non-zero, confirming that the lack of [rotational symmetry](@entry_id:137077) about the $z$-axis (due to the $Kxy$ term) leads to the non-conservation of $L_z$. If $K=0$, the potential becomes centrally symmetric, $\dot{L}_z=0$, and the $z$-component of angular momentum is conserved. This framework provides a rigorous and elegant confirmation that conservation laws are fundamentally linked to the symmetries of the system's energy.

Finally, it is worth noting that while these principles are derived in an [inertial frame of reference](@entry_id:188136), the concepts can be extended to [non-inertial frames](@entry_id:168746), such as a rotating turntable. In such frames, one must include [fictitious forces](@entry_id:165088) (like the Coriolis and centrifugal forces) when calculating the torque. These fictitious torques lead to a modified [rotational dynamics](@entry_id:267911) equation, providing a framework to analyze motion from the perspective of a rotating observer [@problem_id:2031838].