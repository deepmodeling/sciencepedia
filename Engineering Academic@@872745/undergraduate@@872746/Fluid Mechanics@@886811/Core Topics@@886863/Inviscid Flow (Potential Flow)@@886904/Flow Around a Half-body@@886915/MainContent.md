## Introduction
In the realm of fluid dynamics, understanding how fluids interact with solid objects is a central challenge. For many scenarios, complex flows can be simplified and understood through the powerful **principle of superposition**, especially within the framework of ideal potential flow. This principle allows us to build intricate [flow patterns](@entry_id:153478) by combining simple, well-understood elementary flows. A classic and highly instructive application of this method is the creation of the **Rankine half-body**, a model representing the flow around the leading edge of a blunt, semi-infinite object. This model, despite its idealizations, provides crucial insights into the kinematics and pressure dynamics at the forefront of streamlined bodies, addressing the fundamental problem of predicting flow behavior around non-trivial geometries.

This article will guide you through the theory and application of the Rankine half-body. In **Principles and Mechanisms**, you will learn how to construct the flow field by superposing a uniform stream and a source, derive the body's shape, and analyze its velocity and pressure distributions. The **Applications and Interdisciplinary Connections** chapter will then showcase the model's surprising versatility, from aerodynamic design to environmental science. Finally, **Hands-On Practices** will allow you to solidify your understanding through targeted problems. We begin by exploring the fundamental principles that govern the creation of this elegant flow model.

## Principles and Mechanisms

In our study of ideal fluid dynamics, we are governed by Laplace's equation, a linear partial differential equation. A profound consequence of this linearity is the **principle of superposition**: if we have two or more valid [potential flow](@entry_id:159985) solutions, their sum is also a valid solution. This elegant principle allows us to construct complex and physically meaningful [flow patterns](@entry_id:153478) by combining simple, elementary flows. One of the most illustrative examples of this method is the generation of flow around a semi-infinite body, known as the **Rankine half-body**. This model provides a foundational understanding of flow around the leading edge of blunt objects and has surprisingly versatile applications, from [aerospace engineering](@entry_id:268503) to environmental science.

### Constructing the Flow Field by Superposition

The flow around a Rankine half-body is synthesized by the superposition of two fundamental potential flows: a **uniform stream** and a **line source** [@problem_id:1809653]. Let us define these components and their corresponding mathematical representations.

1.  **Uniform Stream**: This is the simplest flow, representing a fluid moving with a constant velocity, which we denote as $U_\infty$, directed along the positive $x$-axis. In a Cartesian coordinate system $(x, y)$, the velocity components are $(u, v) = (U_\infty, 0)$. The velocity potential, $\phi_U$, and stream function, $\psi_U$, are given by:
    $$ \phi_U(x, y) = U_\infty x $$
    $$ \psi_U(x, y) = U_\infty y $$
    In polar coordinates $(r, \theta)$, where $x = r \cos\theta$ and $y = r \sin\theta$, these become:
    $$ \phi_U(r, \theta) = U_\infty r \cos\theta $$
    $$ \psi_U(r, \theta) = U_\infty r \sin\theta $$

2.  **Line Source**: This flow represents fluid emanating radially outward from a single point (the origin). We define the **source strength**, denoted by $m$, as the total [volume flow rate](@entry_id:272850) per unit depth emerging from the source. For a source at the origin, the velocity is purely radial, $v_r = m / (2\pi r)$, and the tangential velocity is zero, $v_\theta = 0$. Its velocity potential, $\phi_s$, and stream function, $\psi_s$, are:
    $$ \phi_s(r) = \frac{m}{2\pi} \ln r $$
    $$ \psi_s(\theta) = \frac{m}{2\pi} \theta $$
    Note that the potential and stream functions are singular at the origin ($r=0$), which is a non-physical point for the combined flow model, as we shall see.

By the principle of superposition, the combined [velocity potential](@entry_id:262992) $\phi$ and stream function $\psi$ for the Rankine half-body are the sums of their elementary components:
$$ \phi(r, \theta) = \phi_U + \phi_s = U_\infty r \cos\theta + \frac{m}{2\pi} \ln r $$
$$ \psi(r, \theta) = \psi_U + \psi_s = U_\infty r \sin\theta + \frac{m}{2\pi} \theta $$

An essential property of this combined flow is that it remains **irrotational** (except at the source singularity). Since both the uniform stream and the source are irrotational flows, their superposition must also be irrotational. We can verify this by calculating the [vorticity](@entry_id:142747), $\omega_z$, in polar coordinates [@problem_id:1756250]. The velocity components for the combined flow are found by differentiating the [stream function](@entry_id:266505):
$$ v_r = \frac{1}{r}\frac{\partial \psi}{\partial \theta} = U_\infty \cos\theta + \frac{m}{2\pi r} $$
$$ v_\theta = -\frac{\partial \psi}{\partial r} = -U_\infty \sin\theta $$
The [vorticity](@entry_id:142747) is given by $\omega_z = \frac{1}{r} [ \frac{\partial (r v_\theta)}{\partial r} - \frac{\partial v_r}{\partial \theta} ]$. Substituting our velocity components:
$$ \frac{\partial (r v_\theta)}{\partial r} = \frac{\partial}{\partial r}(-U_\infty r \sin\theta) = -U_\infty \sin\theta $$
$$ \frac{\partial v_r}{\partial \theta} = \frac{\partial}{\partial \theta}(U_\infty \cos\theta + \frac{m}{2\pi r}) = -U_\infty \sin\theta $$
Thus, the vorticity is:
$$ \omega_z = \frac{1}{r}[(-U_\infty \sin\theta) - (-U_\infty \sin\theta)] = 0 $$
The vorticity is identically zero everywhere except at the singularity $r=0$, confirming the flow is irrotational.

### Kinematics and the Stagnation Point

The interaction between the oncoming uniform stream and the outward-flowing source creates a rich kinematic structure. Upstream of the source, the two flows directly oppose each other. There must exist a point where the velocity of the uniform stream is exactly cancelled by the velocity from the source. This is the **stagnation point**, where the total velocity of the fluid is zero.

To find this point, we set both velocity components to zero: $v_r = 0$ and $v_\theta = 0$.
The condition $v_\theta = -U_\infty \sin\theta = 0$ implies that $\sin\theta = 0$, which occurs at $\theta = 0$ and $\theta = \pi$.
-   At $\theta = 0$ (the positive $x$-axis), $v_r = U_\infty + \frac{m}{2\pi r}$. Since $U_\infty$, $m$, and $r$ are all positive, $v_r$ cannot be zero.
-   At $\theta = \pi$ (the negative $x$-axis), $v_r = U_\infty \cos\pi + \frac{m}{2\pi r} = -U_\infty + \frac{m}{2\pi r}$. Setting this to zero gives the location of the [stagnation point](@entry_id:266621), $r_s$:
    $$ -U_\infty + \frac{m}{2\pi r_s} = 0 \quad \implies \quad r_s = \frac{m}{2\pi U_\infty} $$
This stagnation point lies on the negative $x$-axis at a "standoff" distance of $m/(2\pi U_\infty)$ from the source. This specific distance is a fundamental parameter of the flow, representing the extent of the source's influence directly against the oncoming stream [@problem_id:1756231].

### The Dividing Streamline and the Body Shape

In [steady flow](@entry_id:264570), fluid particles follow streamlines, which are lines of constant [stream function](@entry_id:266505), $\psi$. The stagnation point, being part of the flow, must lie on a [streamline](@entry_id:272773). The specific [streamline](@entry_id:272773) that passes through the [stagnation point](@entry_id:266621) is of paramount importance. It acts as a [natural boundary](@entry_id:168645), separating the fluid that originated from the source from the fluid that came from the far uniform stream.

We can find the constant value of this **[dividing streamline](@entry_id:274075)**, $\psi_{body}$, by evaluating the [stream function](@entry_id:266505) at the [stagnation point](@entry_id:266621) $(r_s, \theta_s) = (\frac{m}{2\pi U_\infty}, \pi)$:
$$ \psi_{body} = U_\infty r_s \sin(\pi) + \frac{m}{2\pi} (\pi) = U_\infty \left(\frac{m}{2\pi U_\infty}\right) (0) + \frac{m\pi}{2\pi} = \frac{m}{2} $$
Therefore, the equation for the [dividing streamline](@entry_id:274075) is simply $\psi(r, \theta) = \frac{m}{2}$. Since no fluid can cross a streamline, we can replace this [dividing streamline](@entry_id:274075) with a solid, impermeable boundary without altering the flow pattern outside of it. This conceptual solid boundary is the Rankine half-body.

The equation of the body's surface is thus:
$$ U_\infty r \sin\theta + \frac{m}{2\pi} \theta = \frac{m}{2} $$
We can explicitly solve for the [radial coordinate](@entry_id:165186) $r$ as a function of the angle $\theta$ to describe the body's shape [@problem_id:1756222]:
$$ r(\theta) = \frac{\frac{m}{2} - \frac{m}{2\pi}\theta}{U_\infty \sin\theta} = \frac{m(\pi - \theta)}{2\pi U_\infty \sin\theta} $$
This equation defines the shape of a blunt-nosed object that extends to infinity in the downstream direction. We can also express this shape in Cartesian coordinates. Using $y = r\sin\theta$ and $\cot\theta = x/y$, the streamline equation becomes $U_\infty y + \frac{m}{2\pi}\theta = \frac{m}{2}$. Solving for $\theta$ gives $\theta = \pi - \frac{2\pi U_\infty y}{m}$. Substituting this into the geometric relation $x = y \cot\theta$ yields the Cartesian form of the surface [@problem_id:1756246]:
$$ x(y) = y \cot\left(\pi - \frac{2\pi U_\infty y}{m}\right) = -y \cot\left(\frac{2\pi U_\infty y}{m}\right) $$

A key geometric feature is the ultimate width of the body far downstream. As $x \to \infty$, the influence of the localized source diminishes, and the flow becomes parallel to the $x$-axis. In this limit, $\theta \to 0$ and the stream function approximates to that of the uniform stream, $\psi \approx U_\infty y$. The half-width of the body, $H$, is the asymptotic value of $y$ on the surface. By equating the far-field [stream function](@entry_id:266505) to the constant value on the body streamline, we find this crucial dimension [@problem_id:1756255] [@problem_id:1756233]:
$$ U_\infty H = \psi_{body} = \frac{m}{2} \quad \implies \quad H = \frac{m}{2U_\infty} $$
This result has significant practical utility. For instance, if modeling a pollutant plume from a smokestack (source strength $m$) in a steady wind ($U_\infty$), this equation predicts the ultimate half-width of the plume far downstream. A discharge of $m = 0.200 \text{ m}^2/\text{s}$ into a current of $U_\infty = 0.150 \text{ m/s}$ would result in a plume half-width of $H = 0.200 / (2 \times 0.150) \approx 0.667 \text{ m}$ [@problem_id:1756265]. Notably, the shape and dimensions of the body are determined solely by the ratio $m/U_\infty$ and are independent of [fluid properties](@entry_id:200256) like density or viscosity, a characteristic feature of ideal, incompressible potential flow.

### Pressure Distribution and Bernoulli's Equation

To understand the forces exerted by the fluid on the body, we must analyze the pressure distribution. For steady, incompressible, and [irrotational flow](@entry_id:159258), pressure and velocity are linked by **Bernoulli's equation**:
$$ p + \frac{1}{2}\rho V^2 = p_\infty + \frac{1}{2}\rho U_\infty^2 = \text{constant} $$
where $p$ and $V$ are the local pressure and speed, $p_\infty$ and $U_\infty$ are the values in the freestream, and $\rho$ is the fluid density. It is convenient to express the pressure distribution using the dimensionless **[pressure coefficient](@entry_id:267303)**, $C_p$:
$$ C_p = \frac{p - p_\infty}{\frac{1}{2}\rho U_\infty^2} $$
From Bernoulli's equation, we can write the [pressure coefficient](@entry_id:267303) purely in terms of velocities:
$$ C_p = 1 - \left(\frac{V}{U_\infty}\right)^2 $$
At the stagnation point, $V=0$, so $C_p = 1$, representing the maximum pressure on the body.

Let's calculate the pressure at another point on the body's surface, for example, where the body intersects the positive $y$-axis ($\theta = \pi/2$) [@problem_id:1756261]. First, we find the radial location of this point from the body surface equation:
$$ U_\infty r \sin(\pi/2) + \frac{m}{2\pi}(\pi/2) = \frac{m}{2} \quad \implies \quad U_\infty r + \frac{m}{4} = \frac{m}{2} \quad \implies \quad r = \frac{m}{4U_\infty} $$
Next, we evaluate the velocity components at this point $(r, \theta) = (m/(4U_\infty), \pi/2)$:
$$ v_r = U_\infty \cos(\pi/2) + \frac{m}{2\pi r} = \frac{m}{2\pi (m/4U_\infty)} = \frac{2U_\infty}{\pi} $$
$$ v_\theta = -U_\infty \sin(\pi/2) = -U_\infty $$
The total speed squared at this point is $V^2 = v_r^2 + v_\theta^2 = (\frac{2U_\infty}{\pi})^2 + (-U_\infty)^2 = U_\infty^2 (1 + \frac{4}{\pi^2})$. The [pressure coefficient](@entry_id:267303) is therefore:
$$ C_p = 1 - \frac{V^2}{U_\infty^2} = 1 - \left(1 + \frac{4}{\pi^2}\right) = -\frac{4}{\pi^2} $$
The negative value indicates that the pressure at this point is lower than the freestream pressure, a consequence of the fluid accelerating as it flows around the body's shoulder.

Far downstream ($x \to \infty$), the velocity on the body surface gradually approaches the freestream velocity, $V \to U_\infty$. Consequently, the [pressure coefficient](@entry_id:267303) $C_p$ must approach zero, meaning the pressure on the body recovers to the freestream pressure [@problem_id:1756262]. A more detailed [asymptotic analysis](@entry_id:160416) reveals that the velocity on the surface is slightly greater than freestream, $V \approx U_\infty + \frac{m}{2\pi x}$, leading to a [pressure coefficient](@entry_id:267303) that approaches zero from below:
$$ C_p(x) \approx -\frac{m}{\pi U_\infty x} $$
This slow [pressure recovery](@entry_id:270791) is a hallmark of the source's lingering influence, even at great distances downstream.