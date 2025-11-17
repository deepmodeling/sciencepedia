## Introduction
The behavior of individual charged particles within the complex magnetic fields of a toroidal fusion device is a cornerstone of [fusion science](@entry_id:182346), dictating [plasma confinement](@entry_id:203546), stability, and overall performance. While the instantaneous motion is described by the simple Lorentz force, understanding the long-term trajectory reveals a crucial dichotomy in particle behavior. This distinction, which separates particles into "trapped" and "passing" populations, addresses the fundamental problem of how [toroidal geometry](@entry_id:756056) transforms microscopic motion into macroscopic transport and stability phenomena. This article provides a comprehensive exploration of this topic. The first chapter, "Principles and Mechanisms," will lay the theoretical groundwork, explaining how [conserved quantities](@entry_id:148503) like the magnetic moment lead to [magnetic mirroring](@entry_id:202456) and the classification of orbits. The second chapter, "Applications and Interdisciplinary Connections," will explore the profound consequences of these orbit types on [neoclassical transport](@entry_id:188243), MHD instabilities, and [fusion reactor design](@entry_id:159959). Finally, "Hands-On Practices" will offer practical exercises to solidify your understanding. We begin by examining the physical principles that govern this fundamental division in particle dynamics.

## Principles and Mechanisms

The behavior of individual charged particles within the complex magnetic fields of a toroidal confinement device is foundational to understanding [plasma transport](@entry_id:181619), stability, and heating. While the Lorentz force dictates the instantaneous trajectory, a more insightful picture emerges from the **[guiding-center approximation](@entry_id:750090)**, which averages over the rapid [gyromotion](@entry_id:204632) to describe the slower drift of the particle's center of gyration. In this framework, the dynamics are elegantly captured by a set of conserved quantities, or **[adiabatic invariants](@entry_id:195383)**, which govern the particle's long-term motion. The existence and properties of these invariants give rise to a fundamental distinction between two classes of particle orbits: **trapped** and **passing**. This chapter elucidates the principles governing this classification and explores the mechanisms that define the structure and dynamics of these orbits.

### The Adiabatic Invariance of the Magnetic Moment

The motion of a charged particle in a magnetic field that varies slowly in space and time is characterized by the conservation of certain quantities. In a static magnetic field, where the Lorentz force $\mathbf{F} = q(\mathbf{v} \times \mathbf{B})$ is always perpendicular to the velocity $\mathbf{v}$, the magnetic field does no work. Consequently, the particle's kinetic energy, $E = \frac{1}{2}mv^2$, is an exact constant of the motion.

A second, more profound invariant arises when the magnetic field changes slowly compared to the particle's [gyromotion](@entry_id:204632). This is the **[first adiabatic invariant](@entry_id:184749)**, or **magnetic moment**, defined as:

$$
\mu = \frac{\frac{1}{2} m v_{\perp}^{2}}{B} = \frac{\text{Perpendicular Kinetic Energy}}{\text{Magnetic Field Strength}}
$$

Here, $v_{\perp}$ is the component of the particle's velocity perpendicular to the magnetic field line, and $B$ is the local magnetic field magnitude. The term "adiabatic" signifies that $\mu$ is not an exact constant of motion like energy but is conserved to a very high degree provided the changes in the magnetic field are "slow." The condition for this invariance can be rigorously derived. For a magnetic field that is uniform in space but varies slowly in time, the Maxwell-Faraday law, $\nabla \times \mathbf{E} = -\partial\mathbf{B}/\partial t$, implies the existence of an [induced electric field](@entry_id:267314) that can do work on the particle. However, when averaged over a single gyration, the net change in $\mu$ is found to be zero to the leading order [@problem_id:3723619]. The conservation of $\mu$ holds true so long as the [characteristic time scale](@entry_id:274321) for the field variation is much longer than the gyroperiod, $T = 2\pi/\Omega$, where $\Omega = |q|B/m$ is the **cyclotron frequency**. This leads to the fundamental criterion for the [adiabatic invariance](@entry_id:173254) of $\mu$:

$$
\frac{1}{B} \left| \frac{dB}{dt} \right| \ll \Omega
$$

This condition is exceptionally well satisfied in typical fusion plasmas, allowing us to treat both $E$ and $\mu$ as conserved quantities along a particle's [guiding-center](@entry_id:200181) trajectory.

### The Magnetic Mirror Effect

The conservation of energy and magnetic moment provides a powerful constraint on particle motion. The total kinetic energy can be decomposed into parts parallel and perpendicular to the magnetic field:

$$
E = \frac{1}{2}mv_{\parallel}^2 + \frac{1}{2}mv_{\perp}^2
$$

Using the definition of the magnetic moment, we can replace the perpendicular kinetic energy term: $\frac{1}{2}mv_{\perp}^2 = \mu B$. Substituting this into the [energy conservation equation](@entry_id:748978) gives:

$$
E = \frac{1}{2}mv_{\parallel}^2 + \mu B(s)
$$

where $s$ is a coordinate along the magnetic field line. This equation reveals that the parallel motion of the guiding center is analogous to the motion of a particle with energy $E$ in a one-dimensional effective potential $U_{\text{eff}}(s) = \mu B(s)$. As a particle moves into a region of stronger magnetic field, the potential energy $\mu B$ increases. To conserve total energy $E$, the particle's parallel kinetic energy, $\frac{1}{2}mv_{\parallel}^2$, must decrease.

We can solve for the parallel velocity squared:

$$
v_{\parallel}^2 = \frac{2}{m} \left( E - \mu B(s) \right)
$$

For a particle to physically exist at a location $s$, its velocity must be real, which requires $v_{\parallel}^2 \ge 0$. This imposes a strict kinematic constraint: a particle can only access regions where $B(s) \le E/\mu$. If a particle moving along a field line encounters a region where the field strength is increasing, it will slow down. If the field becomes strong enough to satisfy the equality $B(s) = E/\mu$, the parallel velocity $v_{\parallel}$ becomes zero. At this point, the [guiding center](@entry_id:189730) stops its forward motion along the field line and is repelled by a force $F_{\parallel} \approx -\mu \nabla_{\parallel}B$, which accelerates it back toward the region of weaker magnetic field. This phenomenon is known as **[magnetic mirroring](@entry_id:202456)**, and the location where $v_{\parallel}=0$ is called a **mirror point** or **turning point** [@problem_id:3723695].

At a mirror point, all of the particle's kinetic energy is converted into perpendicular motion, meaning $v_{\perp}$ is maximized. This is a direct consequence of the exchange between parallel and perpendicular kinetic energy required to conserve both $E$ and $\mu$.

### Classification of Orbits in a Toroidal Field

In a toroidal confinement device like a [tokamak](@entry_id:160432), the magnetic field is inherently non-uniform. Due to the geometry, the [toroidal magnetic field](@entry_id:756057) coils are spaced more closely on the inboard side (smaller major radius) than on the outboard side (larger major radius). This results in a magnetic field strength that is approximately inversely proportional to the major radius, $R$. On any given [magnetic flux surface](@entry_id:751622), the field is strongest on the **high-field side** (inboard, $\theta=\pi$) and weakest on the **low-field side** (outboard, $\theta=0$). This natural variation in $B$ acts as a [magnetic mirror](@entry_id:204158) system.

Let's consider the widely used model for the magnetic field magnitude on a flux surface in a large-aspect-ratio tokamak [@problem_id:3723553]:

$$
B(\theta) \approx \frac{B_0}{1 + \epsilon \cos\theta}
$$

Here, $\theta$ is the poloidal angle ($\theta=0$ on the outboard midplane), $\epsilon = r/R_0$ is the inverse [aspect ratio](@entry_id:177707) of the flux surface, and $B_0$ is the field strength at the geometric axis ($R=R_0$). The field varies between a minimum $B_{\text{min}} \approx B_0/(1+\epsilon)$ and a maximum $B_{\text{max}} \approx B_0/(1-\epsilon)$.

The fate of a particle depends on its pitch angle, which relates its parallel to perpendicular velocity. A convenient, dimensionless parameter that captures this is the ratio of the two invariants, $\lambda = \mu/E$. Our condition for parallel velocity becomes:

$$
v_{\parallel}^2 = \frac{2E}{m} \left( 1 - \frac{\mu}{E} B(s) \right) = \frac{2E}{m} \left( 1 - \lambda B(s) \right)
$$

The mirror point condition $B = E/\mu$ is now simply $B = 1/\lambda$. Whether a particle is trapped or not depends on whether the value $1/\lambda$ falls within the range of magnetic field strengths present on the flux surface, $[B_{\text{min}}, B_{\text{max}}]$ [@problem_id:3723695].

1.  **Passing Particles**: If a particle has a small magnetic moment relative to its energy (i.e., it is dominated by parallel motion), its required mirroring field $1/\lambda$ may be greater than any field strength it encounters, $1/\lambda > B_{\text{max}}$. Such a particle never mirrors. It has sufficient parallel kinetic energy to overcome the magnetic "hill" on the high-field side and will continuously circulate around the torus, either in the direction of the toroidal current (co-passing) or opposite to it (counter-passing). The condition for a particle to be passing is therefore $\lambda  1/B_{\text{max}}$.

2.  **Trapped Particles**: If a particle has a larger magnetic moment (i.e., more perpendicular velocity), its mirroring field $1/\lambda$ may fall within the range of field strengths on the surface: $B_{\text{min}} \le 1/\lambda \le B_{\text{max}}$. Such a particle cannot reach the high-field side. It is "trapped" in the magnetic well on the low-field side, bouncing between two mirror points, called **bounce points**, located at the poloidal angles $\pm\theta_b$ where $B(\theta_b) = 1/\lambda$. Using a normalized pitch-angle parameter $\lambda' = \mu B_0/E$, the bounce angles are given by [@problem_id:3723553]:
    $$
    \theta_b = \pm \arccos\left(\frac{\lambda' - 1}{\epsilon}\right)
    $$

The boundary that separates these two populations in phase space is called the **trapped-passing separatrix**. It is defined by particles that are marginally trapped, meaning they turn exactly at the point of maximum magnetic field, $B_{\text{max}} = 1/\lambda$. For the standard field model, this critical value of the normalized pitch parameter $\lambda' = \mu B_0/E$ is found at $\lambda' = 1-\epsilon$ [@problem_id:3723617]. Particles with $\lambda'  1-\epsilon$ are passing, while those with $1-\epsilon \le \lambda' \le 1+\epsilon$ are trapped.

The periodic motion of a [trapped particle](@entry_id:756144) between its bounce points occurs with a characteristic frequency, the **bounce frequency** $\omega_b = 2\pi/T_b$. The bounce time $T_b$ is the time for one full oscillation and can be calculated by integrating the inverse of the parallel velocity along the particle's path between the bounce points, $l_1$ and $l_2$:

$$
T_b = 2 \int_{l_1}^{l_2} \frac{dl}{|v_{\parallel}(l)|} = 2 \sqrt{\frac{m}{2E}} \int_{l_1}^{l_2} \frac{dl}{\sqrt{1 - \lambda B(l)}}
$$

This gives the bounce frequency as [@problem_id:3723649]:
$$
\omega_{b} = \frac{\pi \sqrt{\frac{2E}{m}}}{\int_{l_{1}}^{l_{2}} \frac{dl}{\sqrt{1 - \lambda B(l)}}}
$$

### Orbit Topology and Canonical Momentum

In an axisymmetric system like an ideal [tokamak](@entry_id:160432), there is another exact constant of motion: the **[canonical toroidal angular momentum](@entry_id:747109)**, $P_\phi$. It is composed of a mechanical part and an electromagnetic part:

$$
P_\phi = m R v_\phi + q \psi
$$

where $v_\phi$ is the toroidal velocity component, and $\psi$ is the poloidal magnetic flux function, which serves as a [radial coordinate](@entry_id:165186) (constant $\psi$ defines a flux surface). The conservation of $P_\phi$ has a profound consequence: as a particle moves, if its mechanical momentum $m R v_\phi$ changes, its radial position $\psi$ must also change to keep $P_\phi$ constant.

For a [trapped particle](@entry_id:756144), this effect is dramatic. As it moves from the outboard midplane towards a bounce point, its parallel velocity $v_\parallel$ decreases to zero. Since the toroidal velocity is mostly parallel velocity ($v_\phi \approx v_\parallel B_\phi/B$), $v_\phi$ also approaches zero at the bounce points. This constitutes a significant change in the mechanical momentum term. To conserve $P_\phi$, the [guiding center](@entry_id:189730) must drift radially, tracing a path that deviates from a single flux surface. When the particle reverses direction, it retraces this [radial drift](@entry_id:158246), creating a closed orbit in the poloidal plane. The characteristic shape of this orbit is a crescent or "banana," and its maximum radial width is known as the **banana width**, $\Delta r$.

The tips of this [banana orbit](@entry_id:192144) correspond to the bounce points where $v_\parallel=0$. At these radial turning points, the equation for $P_\phi$ simplifies, showing that the tips of all [banana orbits](@entry_id:202619) for a given particle lie on a single flux surface, $\psi_{\text{turn}} = P_\phi/q$ [@problem_id:3723666]. The radial width of the orbit can be directly related to the change in mechanical momentum over half a bounce. Using the definition of the [safety factor](@entry_id:156168), $q(r) = r B_\phi / (R B_\theta)$, this leads to an expression for the banana width [@problem_id:3723676]:

$$
\Delta r \sim \frac{q}{\sqrt{\epsilon}} \rho
$$

where $\rho$ is the particle's [gyroradius](@entry_id:261534). This width can be significant, especially for energetic particles, and is a primary reason why [trapped particles](@entry_id:756145) dominate [neoclassical transport](@entry_id:188243).

### Precession and the Hierarchy of Frequencies

In addition to bouncing, the guiding centers of [trapped particles](@entry_id:756145) are subject to slow drifts due to the gradient and curvature of the magnetic field. These drifts have a component in the vertical direction, which, when combined with the projection onto the poloidal plane, results in a net precession of the [banana orbit](@entry_id:192144) in the toroidal direction. This slow toroidal drift occurs at the **bounce-averaged precession frequency**, $\omega_d$. For a deeply [trapped particle](@entry_id:756144), this frequency can be calculated as [@problem_id:3723551]:

$$
\omega_d \approx \frac{E}{q R_0 r B_\theta}
$$

The motion of a [trapped particle](@entry_id:756144) is thus characterized by three distinct time scales and their associated frequencies:
1.  **Cyclotron Frequency ($\Omega$)**: The rapid gyration of the particle around a field line.
2.  **Bounce Frequency ($\omega_b$)**: The [periodic motion](@entry_id:172688) of the [guiding center](@entry_id:189730) between mirror points.
3.  **Precession Frequency ($\omega_d$)**: The slow toroidal drift of the entire [banana orbit](@entry_id:192144).

These frequencies are well-separated, obeying the hierarchy $\Omega \gg \omega_b \gg \omega_d$. This ordering is fundamental to the theoretical treatment of plasma behavior, allowing phenomena on different time scales to be analyzed separately.

### Ripple Trapping: A Consequence of Imperfect Axisymmetry

Real [tokamaks](@entry_id:182005) are not perfectly axisymmetric. The [toroidal magnetic field](@entry_id:756057) is generated by a discrete number of coils, typically 16 to 20. This creates a small periodic variation, or **ripple**, in the magnetic field strength as a function of the toroidal angle $\phi$. This can be modeled as:

$$
B(\phi) = B_{\text{avg}}(1 + \delta \cos(N\phi))
$$

where $N$ is the number of coils and $\delta$ is the small ripple amplitude [@problem_id:3723560]. This ripple superimposes small magnetic wells on top of the main [toroidal field](@entry_id:194478) variation. Just as the main [toroidal field](@entry_id:194478) gradient can trap particles, these local wells can also trap particles through the same [magnetic mirror](@entry_id:204158) mechanism. A particle becomes **ripple-trapped** if it has insufficient parallel energy to escape a local ripple well.

Applying the mirror condition $B(\phi) = E/\mu$ to the ripple field, we find that trapping occurs when the particle's pitch-angle parameter $\lambda = \mu B_{\text{avg}} / E$ falls within the range:

$$
\frac{1}{1+\delta} \le \lambda \le \frac{1}{1-\delta}
$$

The onset for ripple trapping occurs at $\lambda_c = 1/(1+\delta)$. Particles in this regime are confined between two ripple crests. Because they cannot complete a full bounce orbit, they are not subject to the same averaging effects that confine toroidally [trapped particles](@entry_id:756145). Instead, their vertical drifts are uncompensated, often leading to their rapid loss from the plasma. Mitigating such ripple-induced losses is a critical aspect of [tokamak](@entry_id:160432) design.