## Introduction
Vortex flows are among the most captivating and fundamental patterns in nature, visible in the graceful spiral of a galaxy and the turbulent swirl of water down a drain. These rotational motions are not just visual curiosities; they are a cornerstone of fluid dynamics, governing the behavior of everything from [weather systems](@entry_id:203348) to aircraft wings. However, their complexity can be daunting. This article aims to demystify vortex flows by breaking them down into their elementary components, providing a clear and structured path to understanding their behavior and significance.

This guide will systematically build your knowledge of elementary plane vortices across three distinct chapters. In **Principles and Mechanisms**, you will learn the essential physics of the two ideal building blocks—the [forced vortex](@entry_id:260585) and the [free vortex](@entry_id:261574)—and see how they are combined into the more realistic Rankine vortex model. In **Applications and Interdisciplinary Connections**, you will discover how these simple models are applied to explain a vast array of real-world phenomena, from the lift on an airplane and the paradox of tea leaves to the exotic world of quantum superfluids. Finally, **Hands-On Practices** will provide you with opportunities to apply these concepts to solve practical problems, solidifying your grasp of the core principles.

## Principles and Mechanisms

Vortex flows are a ubiquitous and fundamental feature of fluid dynamics, appearing in phenomena ranging from the swirl of water down a drain to the vast rotating structures of cyclones and galaxies. In this chapter, we will dissect the underlying principles of elementary plane vortices by examining two idealized building blocks: the **[forced vortex](@entry_id:260585)** and the **[free vortex](@entry_id:261574)**. By understanding their distinct kinematic and dynamic properties, we can then construct a more realistic composite model, the **Rankine vortex**, which provides a powerful framework for analyzing many real-world rotational flows.

### The Forced Vortex: A Model of Solid-Body Rotation

The most straightforward type of [vortex flow](@entry_id:271366) is one that mimics the motion of a rotating solid object. This is known as a **[forced vortex](@entry_id:260585)**. Imagine a cylindrical container of fluid rotating at a constant [angular velocity](@entry_id:192539), $\omega$, about its central axis. After transient effects have dissipated, every fluid particle moves in a circular path with the same angular velocity as the container. This state is called **[solid-body rotation](@entry_id:191086)**.

In a [cylindrical coordinate system](@entry_id:266798) $(r, \theta, z)$ with the origin at the center of rotation, the velocity field for a [forced vortex](@entry_id:260585) is purely tangential. The [radial velocity](@entry_id:159824) $v_r$ and axial velocity $v_z$ are both zero. The tangential velocity, $v_\theta$, of any fluid particle at a radial distance $r$ from the axis is given by the simple [linear relationship](@entry_id:267880):

$v_\theta = \omega r$

A direct consequence of this [velocity profile](@entry_id:266404) is that the angular velocity of any fluid particle, $\Omega = v_\theta / r$, is constant and equal to $\omega$ throughout the flow. This means that every particle, regardless of its radial position, completes a full revolution in the same amount of time, $T = 2\pi / \omega$.

A more profound property of a [forced vortex](@entry_id:260585) is its **vorticity**. Vorticity, denoted by the vector $\vec{\zeta} = \nabla \times \vec{v}$, measures the local angular velocity of a fluid element. For a [two-dimensional flow](@entry_id:266853) in the $r$-$\theta$ plane with velocity $\vec{v} = v_\theta(r) \hat{e}_\theta$, the [vorticity](@entry_id:142747) simplifies to a single component in the $z$-direction:

$\zeta = \frac{1}{r} \frac{d(r v_\theta)}{dr}$

Substituting the velocity profile for a [forced vortex](@entry_id:260585), $v_\theta = \omega r$, we find:

$\zeta = \frac{1}{r} \frac{d(r (\omega r))}{dr} = \frac{1}{r} \frac{d(\omega r^2)}{dr} = \frac{1}{r} (2 \omega r) = 2\omega$

The [vorticity](@entry_id:142747) of a [forced vortex](@entry_id:260585) is a constant value equal to twice the angular velocity. A non-zero vorticity signifies that the flow is **rotational**. Conceptually, if one were to place a tiny paddlewheel into the flow, it would not only be carried around the vortex center but would also spin about its own axis [@problem_id:1752711]. This local spinning is the essence of a [rotational flow](@entry_id:276737).

Another key property is **circulation**, $\Gamma$, defined as the [line integral](@entry_id:138107) of the velocity vector around a closed path $C$: $\Gamma = \oint_C \vec{v} \cdot d\vec{l}$. For a circular path of radius $r$ in a [forced vortex](@entry_id:260585), this becomes:

$\Gamma(r) = \int_0^{2\pi} (\omega r) (r d\theta) = 2\pi \omega r^2$

Unlike the vorticity, the circulation in a [forced vortex](@entry_id:260585) is not constant but increases with the square of the radial distance of the integration path [@problem_id:1752730].

The rotation in a [forced vortex](@entry_id:260585) induces a radial pressure gradient. For a steady, [inviscid flow](@entry_id:273124), the inward-acting pressure force must balance the outward-acting centrifugal effect. This balance is expressed by the radial component of the Euler equation:

$\frac{dp}{dr} = \rho \frac{v_\theta^2}{r}$

For a [forced vortex](@entry_id:260585), this becomes $\frac{dp}{dr} = \rho \frac{(\omega r)^2}{r} = \rho \omega^2 r$. This shows that pressure increases with radius. Integrating this equation from a central pressure $P_0$ at $r=0$ to a pressure $P(r)$ at radius $r$ gives the pressure distribution:

$P(r) - P_0 = \int_0^r \rho \omega^2 r' dr' = \frac{1}{2} \rho \omega^2 r^2$

The pressure is lowest at the center and increases parabolically with radius. This principle has a remarkable practical application in the manufacturing of large astronomical mirrors. By rotating a vat of molten glass at a constant [angular velocity](@entry_id:192539) $\omega$, the free surface, which must be a surface of constant pressure, assumes a parabolic shape [@problem_id:1752699]. The slope of this free surface, $z(r)$, can be found by considering that the total differential of pressure, $dp = \frac{\partial p}{\partial r}dr + \frac{\partial p}{\partial z}dz$, must be zero along the surface. With $\frac{\partial p}{\partial r} = \rho \omega^2 r$ and the hydrostatic relation $\frac{\partial p}{\partial z} = -\rho g$, we find the slope to be:

$\frac{dz}{dr} = \frac{\omega^2 r}{g}$

Integrating this result confirms the parabolic shape of the surface: $z(r) = \frac{\omega^2 r^2}{2g} + \text{constant}$.

### The Free Vortex: An Irrotational Ideal

In contrast to the [forced vortex](@entry_id:260585), the **[free vortex](@entry_id:261574)** describes a flow where motion is induced not by an external torque but by, for instance, the [conservation of angular momentum](@entry_id:153076). A common example is the swirl of water draining from a bathtub far from the drain itself.

The defining characteristic of an ideal [free vortex](@entry_id:261574) is that its circulation, $\Gamma$, is constant for any closed path that encloses the origin. For a circular path of radius $r$, $\Gamma = 2\pi r v_\theta$. Since $\Gamma$ is constant, the tangential velocity must vary inversely with the radius:

$v_\theta = \frac{\Gamma}{2\pi r}$

This relationship implies that fluid particles move faster as they approach the center. This is a direct consequence of the [conservation of angular momentum](@entry_id:153076) for fluid particles in the absence of torque (viscosity). If one has velocity measurements at two points in a vortex, one can distinguish it from a [forced vortex](@entry_id:260585). If the product $r v_\theta$ is constant, the flow is a [free vortex](@entry_id:261574); if the ratio $v_\theta / r$ is constant, it is a [forced vortex](@entry_id:260585) [@problem_id:1752722].

Perhaps the most striking and counter-intuitive property of a [free vortex](@entry_id:261574) is its [vorticity](@entry_id:142747). Applying the vorticity formula to the [free vortex](@entry_id:261574) velocity profile for any $r > 0$:

$\zeta = \frac{1}{r} \frac{d(r v_\theta)}{dr} = \frac{1}{r} \frac{d(r \frac{\Gamma}{2\pi r})}{dr} = \frac{1}{r} \frac{d(\frac{\Gamma}{2\pi})}{dr} = 0$

Despite the obvious circular motion of the fluid, the [vorticity](@entry_id:142747) is zero everywhere except at the origin. Such a flow is termed **irrotational**. This means that although fluid particles *revolve* around the vortex center, they do not *rotate* about their own axes. A small paddlewheel placed in a [free vortex](@entry_id:261574) would orbit the center but its orientation would remain fixed, much like a compass needle on a spinning carousel [@problem_id:1752711]. The flow is irrotational.

The concept of the stream function, $\psi$, provides another way to describe this flow. In [polar coordinates](@entry_id:159425), the velocity components are related to $\psi$ by $v_r = \frac{1}{r}\frac{\partial \psi}{\partial \theta}$ and $v_\theta = -\frac{\partial \psi}{\partial r}$. For a [free vortex](@entry_id:261574), $v_r=0$, so $\psi$ is a function of $r$ only. Integrating the expression for $v_\theta$ gives the stream function [@problem_id:1752681]:

$\frac{d\psi}{dr} = -v_\theta = -\frac{\Gamma}{2\pi r} \implies \psi(r) = -\frac{\Gamma}{2\pi} \ln(r) + C$

The [streamlines](@entry_id:266815), which are lines of constant $\psi$, are therefore concentric circles.

A critical flaw of the ideal [free vortex](@entry_id:261574) model is the **singularity at the origin** ($r=0$). As $r \to 0$, the velocity $v_\theta$ approaches infinity, which is physically impossible. This suggests that the [free vortex](@entry_id:261574) model cannot be valid near the center of a real vortex.

The pressure field in a [free vortex](@entry_id:261574) can be found using the same radial [equilibrium equation](@entry_id:749057), $\frac{dp}{dr} = \rho \frac{v_\theta^2}{r}$. Substituting the [free vortex](@entry_id:261574) velocity profile:

$\frac{dp}{dr} = \rho \frac{(\Gamma/2\pi r)^2}{r} = \frac{\rho \Gamma^2}{4\pi^2 r^3}$

Integrating this from a radius $r$ to the [far-field](@entry_id:269288) (where $P \to P_\infty$ as $r \to \infty$) shows that the pressure decreases as one approaches the center.

### The Rankine Vortex: A Realistic Synthesis

Real-world vortices, such as tornadoes and whirlpools, do not possess an infinite velocity at their centers. Instead, viscous effects near the center cause the core of the vortex to rotate more like a solid body. The **Rankine vortex** is a brilliant and simple composite model that captures this behavior by combining the two ideal vortices we have discussed [@problem_id:1752727].

The Rankine vortex model consists of:
1.  An **inner core** ($r \le R$) that behaves as a [forced vortex](@entry_id:260585): $v_\theta = \omega r$.
2.  An **outer region** ($r > R$) that behaves as a [free vortex](@entry_id:261574): $v_\theta = \frac{\Gamma}{2\pi r}$.

A crucial physical requirement is that the velocity must be continuous at the interface radius $R$. This allows us to relate the properties of the two regions:

$v_{\theta, \text{inner}}(R) = v_{\theta, \text{outer}}(R) \implies \omega R = \frac{\Gamma}{2\pi R}$

This yields a fundamental relationship: $\Gamma = 2\pi \omega R^2$. This continuity condition is essential for solving problems involving Rankine vortices [@problem_id:1752698] [@problem_id:1752670].

The vorticity profile of the Rankine vortex is particularly illuminating. All the vorticity of the flow is confined within the core, where $\zeta = 2\omega$. Outside the core, the flow is irrotational, with $\zeta = 0$ [@problem_id:1752670]. The Rankine model thus resolves the singularity of the [free vortex](@entry_id:261574) by replacing the point singularity with a finite region of constant [vorticity](@entry_id:142747).

The pressure distribution in a Rankine vortex can be calculated by integrating the radial pressure gradient equation, $\frac{dp}{dr} = \rho \frac{v_\theta^2}{r}$, across both regions. Let's find the total pressure drop from the far-field ($P_\infty$) to the center ($P_0$). The calculation proceeds in two steps [@problem_id:1752689] [@problem_id:1752727]:
1.  **Outer Region ($R$ to $\infty$)**: The pressure increase from $P(R)$ to $P_\infty$ is $\Delta P_{\text{out}} = \int_R^\infty \rho \frac{(\Gamma/2\pi r)^2}{r} dr = \frac{1}{2} \rho (\omega R)^2$.
2.  **Inner Region ($0$ to $R$)**: The pressure increase from $P_0$ to $P(R)$ is $\Delta P_{\text{in}} = \int_0^R \rho (\omega^2 r) dr = \frac{1}{2} \rho \omega^2 R^2$.

The total [pressure drop](@entry_id:151380) is the sum of these two, $P_\infty - P_0 = \Delta P_{\text{in}} + \Delta P_{\text{out}}$. If we denote the velocity at the interface as $V = \omega R$, the total [pressure drop](@entry_id:151380) simplifies to a remarkably elegant result:

$P_\infty - P_0 = \frac{1}{2} \rho V^2 + \frac{1}{2} \rho V^2 = \rho V^2$

Finally, an analysis of the smoothness of the functions at the interface $r=R$ reveals important mathematical properties of the model [@problem_id:1752666].
*   The velocity $v_\theta(r)$ is continuous by construction.
*   The pressure $p(r)$ must also be continuous, as a discontinuity would imply an infinite force.
*   The radial pressure gradient, $\frac{dp}{dr} = \rho \frac{v_\theta^2}{r}$, is continuous because $v_\theta$ is continuous.
*   However, the derivative of the velocity, $\frac{dv_\theta}{dr}$, is discontinuous. For $r  R$, the derivative is $\omega$. For $r > R$, the derivative is $-\omega R^2/r^2$, which equals $-\omega$ at $r=R$. Thus, the derivative jumps from $\omega$ to $-\omega$ across the interface. The curvature of the velocity profile, $\frac{d^2v_\theta}{dr^2}$, is also discontinuous. For $r  R$, the second derivative is zero. For $r > R$, the second derivative is $2\omega R^2/r^3$. Thus, the curvature is also discontinuous at $r=R$.