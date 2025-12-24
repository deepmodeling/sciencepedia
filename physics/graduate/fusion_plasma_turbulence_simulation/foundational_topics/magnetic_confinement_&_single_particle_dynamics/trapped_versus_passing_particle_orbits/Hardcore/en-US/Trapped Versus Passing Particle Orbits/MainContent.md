## Introduction
The behavior of a magnetically confined fusion plasma is ultimately determined by the intricate motion of billions of individual charged particles. Understanding this motion in the complex magnetic geometry of a toroidal device like a tokamak is a foundational challenge in fusion science. While the full trajectory of any single particle is complex, a powerful organizing principle emerges from a fundamental dichotomy in orbit topology: particles can be classified as either "trapped" or "passing." This distinction is not merely a geometric curiosity; it is the key to unlocking a deeper understanding of [plasma transport](@entry_id:181619), stability, and confinement. This article addresses the knowledge gap between simple particle motion and complex macroscopic phenomena by systematically exploring the origins and consequences of these two orbit types.

This article will guide you through the physics of trapped and passing particles in three chapters. First, the **Principles and Mechanisms** chapter will lay the theoretical groundwork, introducing the adiabatic invariants and the [magnetic mirror effect](@entry_id:171262) that give rise to the orbit classification, and describing the characteristic "banana" shape of trapped particle orbits. Next, the **Applications and Interdisciplinary Connections** chapter will explore the profound and wide-ranging impact of this distinction, showing how it governs [neoclassical transport](@entry_id:188243), drives macroscopic instabilities, shapes [microturbulence](@entry_id:1127893), and creates fundamental design differences between tokamaks and stellarators. Finally, the **Hands-On Practices** section will provide opportunities to solidify this knowledge through targeted analytical and computational problems, connecting theory directly to practical application. We begin by examining the fundamental principles that govern a particle's journey through a toroidal magnetic field.

## Principles and Mechanisms

The motion of individual charged particles within the complex magnetic field geometry of a toroidal confinement device is the foundation upon which macroscopic plasma behavior is built. While the full particle trajectory, governed by the Lorentz force, is intricate, a powerful simplification arises from the [separation of timescales](@entry_id:191220). In a typical fusion plasma, the particle's gyration around a magnetic field line is much faster than its motion along the field line, which in turn is often faster than any cross-field drifts. This hierarchy allows for the application of [guiding-center theory](@entry_id:1125840), which averages over the fast gyromotion and reveals a set of approximately conserved quantities, or **[adiabatic invariants](@entry_id:195383)**. These invariants are the keys to understanding and classifying particle orbits.

### Fundamental Invariants of Guiding-Center Motion

For a particle of mass $m$ and charge $q$ moving in a static, or slowly varying, electromagnetic field, three quantities are of paramount importance.

First is the **total energy**, $\mathcal{E}$. In the absence of [non-conservative forces](@entry_id:164833) or time-varying electric fields, the particle's total energy, which is the sum of its kinetic and electrostatic potential energy, is conserved.
$$
\mathcal{E} = \frac{1}{2}mv^2 + q\Phi = \text{constant}
$$
Here, $v$ is the particle's speed and $\Phi$ is the electrostatic potential.

The second invariant is the **magnetic moment**, $\mu$. This quantity is related to the magnetic flux enclosed by the particle's fast gyromotion. It is defined as the kinetic energy associated with the perpendicular motion divided by the magnetic field strength:
$$
\mu = \frac{\frac{1}{2}mv_{\perp}^2}{B}
$$
where $v_{\perp}$ is the component of the particle's velocity perpendicular to the magnetic field line. Unlike the total energy in a static field, $\mu$ is not an exact constant of motion but rather an **adiabatic invariant**. Its conservation relies on the magnetic field varying slowly in space and time relative to the particle's gyromotion. Specifically, for $\mu$ to be approximately conserved, the [characteristic frequencies](@entry_id:1122277) of the fields, $\omega$, must be much smaller than the cyclotron frequency, $\Omega = |q|B/m$, and the spatial scale lengths of the field, $L$, must be much larger than the particle's gyroradius, $\rho = v_{\perp}/\Omega$. This is the standard **[gyrokinetic ordering](@entry_id:1125860)** assumption, often expressed as $\omega/\Omega \sim \rho/L \ll 1$.

The third important conserved quantity exists in systems with a symmetric geometry. In an axisymmetric device like an ideal tokamak, the system is invariant under rotations in the toroidal direction. The toroidal angle, $\phi$, is therefore an "ignorable coordinate" in the Lagrangian description of the particle's motion. By Noether's theorem, this symmetry implies the conservation of the conjugate canonical momentum, known as the **toroidal canonical momentum**, $P_{\phi}$. It is given by:
$$
P_{\phi} = mR v_{\phi} + q\psi = \text{constant}
$$
where $R$ is the major radius, $v_{\phi}$ is the toroidal component of the velocity, and $\psi$ is the [poloidal magnetic flux](@entry_id:1129914) function (proportional to $R$ times the toroidal component of the vector potential, $A_{\phi}$). Because its conservation stems from a fundamental [geometric symmetry](@entry_id:189059), $P_{\phi}$ is an exact invariant of the motion for any particle orbit—trapped or passing—as long as the system remains perfectly axisymmetric and free of non-Hamiltonian forces like collisions. This conservation is broken by any non-axisymmetric perturbation, such as magnetic field ripple from discrete toroidal field coils, or by turbulent electromagnetic fields.  

### The Magnetic Mirror Effect and Orbit Classification

The conservation of energy $\mathcal{E}$ and magnetic moment $\mu$ provides a powerful constraint on the particle's motion along a magnetic field line. By combining the definitions of these two invariants, we can derive an expression for the particle's velocity component parallel to the magnetic field, $v_{\parallel}$.

The total kinetic energy is $E_{kin} = \mathcal{E} - q\Phi = \frac{1}{2}m(v_{\parallel}^2 + v_{\perp}^2)$. Substituting $v_{\perp}^2$ from the definition of $\mu$, we have:
$$
\mathcal{E} - q\Phi = \frac{1}{2}mv_{\parallel}^2 + \mu B(s)
$$
where $s$ is the coordinate along the magnetic field line. Solving for the parallel kinetic energy gives:
$$
\frac{1}{2}mv_{\parallel}^2 = \mathcal{E} - q\Phi - \mu B(s)
$$
This equation reveals a profound principle: a charged particle moving along a varying magnetic field line acts as if it is moving in a one-dimensional [effective potential](@entry_id:142581), $U_{eff}(s) = \mu B(s) + q\Phi(s)$. The particle's parallel kinetic energy decreases as it moves into regions of stronger magnetic field.

For simplicity, let us first consider the case with no parallel electric field ($\Phi = \text{constant}$). The equation simplifies to $v_{\parallel}^2 = \frac{2}{m}(\mathcal{E} - \mu B(s))$. Since $v_{\parallel}^2$ must be non-negative, a particle can only access regions where its perpendicular energy, $\mu B(s)$, does not exceed its total energy, $\mathcal{E}$. This fundamental constraint is the **accessibility condition**:
$$
B(s) \le \frac{\mathcal{E}}{\mu}
$$
The ratio of the two conserved quantities, $\lambda \equiv \mu/\mathcal{E}$, is a constant for any given particle that encapsulates its pitch angle. This **pitch-angle parameter** is central to classifying orbits. The accessibility condition becomes simply $B(s) \le 1/\lambda$.

A **mirror point** (or turning point) is a location $s_m$ where the particle's parallel motion halts and reverses, i.e., $v_{\parallel}(s_m) = 0$. This occurs precisely where the particle encounters a magnetic field strength $B(s_m) = 1/\lambda$. The force responsible for this reflection is the **[magnetic mirror](@entry_id:204158) force**, $F_{\parallel} = -\mu \nabla_{\parallel}B$, which pushes particles away from regions of high magnetic field. At a mirror point, all the particle's kinetic energy is converted into perpendicular motion, meaning the local pitch angle $\alpha = \arctan(v_{\perp}/v_{\parallel})$ becomes $\pi/2$. This can be expressed elegantly as $\sin^2\alpha = \lambda B(s)$, which equals 1 at the mirror point. 

In a toroidal device, the magnetic field strength is non-uniform, varying along any given field line. It typically has a minimum value, $B_{\min}$, and a maximum value, $B_{\max}$, on a flux surface. This variation allows us to classify all particle orbits into two fundamental types based on their pitch-angle parameter $\lambda$:
1.  **Passing Particles**: If a particle's pitch-angle parameter is small enough that $1/\lambda > B_{\max}$ (or $\lambda  1/B_{\max}$), it will never encounter a magnetic field strong enough to reflect it. Its parallel velocity never reaches zero, and it is free to circulate continuously around the torus in one direction. These are **passing** or **circulating** particles.

2.  **Trapped Particles**: If a particle's pitch-angle parameter falls in the range $1/B_{\max} \le \lambda \le 1/B_{\min}$, then the value $1/\lambda$ corresponds to a magnetic field strength that exists on the flux surface. The particle will travel along the field line until it reaches a mirror point, where it is reflected. It then travels in the opposite direction until it hits a second, symmetric mirror point. The particle is thus confined, or **trapped**, in a subsection of the field line, bouncing between two mirror points. The boundary between these two classes, $\lambda = 1/B_{\max}$, is known as the **trapped-passing [separatrix](@entry_id:175112)**. 

### Orbit Classification in a Tokamak

Let's apply these principles to the specific case of a large-aspect-ratio tokamak. The magnetic field on a flux surface of minor radius $r$ and major radius $R_0$ can be approximated as:
$$
B(\theta) \approx B_0(1 - \epsilon \cos\theta)
$$
where $\epsilon = r/R_0 \ll 1$ is the inverse aspect ratio, $\theta$ is the poloidal angle with $\theta=0$ corresponding to the outboard midplane (the point of largest major radius), and $B_0$ is the field at the magnetic axis. In this model, the magnetic field is weakest at the outboard side, $B_{\min} = B(\theta=0) = B_0(1-\epsilon)$, and strongest at the inboard side, $B_{\max} = B(\theta=\pi) = B_0(1+\epsilon)$. Another common model, particularly valid for circular flux surfaces, is $B(\theta) = B_{ref} / (1+\epsilon\cos\theta)$, where $\theta=0$ is now on the inboard side; the physical principles remain identical, only the angular convention is shifted.  

Using the $B_0(1-\epsilon\cos\theta)$ model, the trapping condition $1/B_{\max}  \lambda  1/B_{\min}$ translates to:
$$
\frac{1}{B_0(1+\epsilon)} \le \lambda \le \frac{1}{B_0(1-\epsilon)}
$$
This defines the region of phase space occupied by trapped particles. The bounce points $\theta_b$ for a trapped particle are found by solving $B(\theta_b) = 1/\lambda$:
$$
B_0(1 - \epsilon \cos\theta_b) = \frac{1}{\lambda} \implies \cos\theta_b = \frac{1 - 1/(\lambda B_0)}{\epsilon}
$$
This yields two symmetric bounce points, $\theta_b = \pm \arccos\left( \frac{1 - 1/(\lambda B_0)}{\epsilon} \right)$, between which the particle oscillates.

A crucial parameter for understanding transport is the **[trapped particle](@entry_id:756144) fraction**, $f_t$, which is the fraction of particles on a flux surface that are trapped. Assuming an isotropic velocity distribution (e.g., a Maxwellian), we can calculate this fraction. It is convenient to work with the pitch-cosine at the location of minimum magnetic field, $\xi = v_{\parallel}/v$ at $\theta=0$. The trapping condition can be shown to be equivalent to $|\xi|  \sqrt{(B_{\max}-B_{\min})/B_{\max}} \approx \sqrt{2\epsilon}$. Integrating a uniform pitch-cosine distribution over this range gives a remarkably simple and important result for the trapped fraction in a large-aspect-ratio tokamak:
$$
f_t \approx \sqrt{\frac{2\epsilon}{1+\epsilon}} \approx \sqrt{2\epsilon}
$$
This shows that even in a device with a small aspect ratio variation, a significant fraction of particles can be trapped. 

### Orbit Dynamics and Timescales

The motion of trapped and passing particles occurs on distinct timescales. For a passing particle, the time to complete one poloidal circuit is the **transit time**, $T_t = \oint ds/v_{\parallel}$. For a particle with $v_\parallel \approx v$, moving along a field line of length $2\pi q R$, this gives a **transit frequency** $\omega_t = 2\pi/T_t$:
$$
\omega_t \approx \frac{v}{qR}
$$
where $q$ is the safety factor.

For a [trapped particle](@entry_id:756144), the time to complete one full bounce between turning points is the **bounce time**, $T_b$. For a "deeply trapped" particle (one that is confined near the bottom of the magnetic well, $\theta \approx 0$), the bounce frequency $\omega_b = 2\pi/T_b$ can be estimated. The parallel velocity is significantly reduced, $v_\parallel \sim v\sqrt{\epsilon}$, leading to a longer period. A detailed calculation shows:
$$
\omega_b \approx \frac{v\sqrt{\epsilon}}{\sqrt{2} qR}
$$
Comparing the two, we see that the characteristic frequency of trapped particle motion is slower than that of passing particles by a factor of $\sqrt{\epsilon}$. This [timescale separation](@entry_id:149780) is critical for many plasma phenomena. 

The projected path of a passing particle's guiding center onto a poloidal cross-section is a circle shifted slightly from the [magnetic flux surface](@entry_id:751622). For a trapped particle, the picture is more intricate. The conservation of toroidal canonical momentum, $P_{\phi} = mRv_{\phi} + q\psi$, dictates the particle's radial motion (since $\psi$ is a flux surface label, or radial coordinate). As a trapped particle moves poloidally, its toroidal velocity $v_{\phi}$ and major radius $R$ both change. To keep $P_{\phi}$ constant, its radial coordinate $\psi(r)$ must also change. This leads to a poloidal projection that is not a simple arc but a closed, crescent-shaped orbit known as a **banana orbit**. In an ideal axisymmetric, time-independent system, the orbit is perfectly closed. Integrating the radial motion equation over one full bounce period $T_b$ shows that the net change in flux, $\Delta\psi_b$, is exactly zero. This means there is no net radial drift; the banana orbit is radially confined. 

Superimposed on this fast [bounce motion](@entry_id:1121799) are slower cross-field drifts. The most significant for trapped particles is the toroidal precession due to the [magnetic field gradient](@entry_id:924531) and curvature. This causes the banana orbit itself to drift slowly in the toroidal direction. The rate of this precession can be calculated by bounce-averaging the instantaneous drift velocity. This calculation often involves [special functions](@entry_id:143234), like Bessel functions, which arise from integrating sinusoidal functions over a bounce period. 

### Consequences for Plasma Confinement

The distinction between trapped and passing orbits is not merely academic; it has profound consequences for [plasma confinement](@entry_id:203546). A key parameter is the width of the particle orbits. The **gyroradius** scales as $\rho_s \propto \sqrt{m_s}/|q_s|$, meaning for the same temperature, an ion has a much larger gyroradius than an electron ($\rho_i \sim \sqrt{m_i/m_e} \rho_e$). The radial width of a [banana orbit](@entry_id:192144), or **banana width** $\Delta_{b,s}$, is even larger and scales with the gyroradius and geometric factors:
$$
\Delta_{b,s} \sim \frac{q}{\sqrt{\epsilon}}\rho_s
$$
Consequently, ion [banana orbits](@entry_id:202619) are significantly wider than electron [banana orbits](@entry_id:202619) ($\Delta_{b,i} \gg \Delta_{b,e}$). This has two major implications:
1.  **Neoclassical Transport**: Collisions can knock a particle from one [banana orbit](@entry_id:192144) to another, causing a radial step of size $\sim \Delta_{b,s}$. Since ions have much larger banana widths, this collisional transport (neoclassical transport) is typically dominated by ions.
2.  **Turbulent Transport**: Microturbulence creates fluctuating fields with a characteristic perpendicular wavelength. If a particle's orbit width is much larger than this wavelength, it "averages out" the effect of the fluctuations, reducing its response and the associated turbulent transport. Because ion orbits are so large, they experience stronger **orbit averaging** than electrons, which can decouple them from short-wavelength turbulence. 

### Beyond Ideal Axisymmetry

The simple picture of toroidally trapped and passing particles is valid for an ideal, axisymmetric tokamak. Real devices deviate from this ideal.

**Stellarators**, by design, are non-axisymmetric. Their magnetic field has a helical structure, which can be modeled by adding a ripple term to the toroidal field: $B(\theta,\phi) \simeq B_0 [1 - \epsilon \cos\theta + \delta \cos(N\phi - M\theta)]$. This helical ripple creates multiple [local minima and maxima](@entry_id:266772) in the magnetic field along a field line. These local wells can trap particles in a new way, creating a class of **helically-trapped** or **ripple-trapped** particles. These particles are confined to a small segment of the torus and can experience rapid radial drift, often leading to significant particle and energy losses. 

Even in a tokamak, perturbations can alter orbit topology. A **parallel electric field**, $E_{\parallel}$, arising from a potential variation $\phi(s)$ along the field, modifies the effective potential to $U_{eff}(s) = \mu B(s) + q\phi(s)$. This directly changes the mirroring condition. For a positive ion ($q0$), a potential that increases towards the high-field region (an "ambipolar" field) will enhance the mirroring effect, trapping particles that would otherwise be passing. Conversely, a time-dependent fluctuation $\delta E_{\parallel}(s,t)$ can do work on a particle, changing its total energy. If this energy change is comparable to its parallel kinetic energy and occurs coherently over a bounce or transit time, it can cause **transitions between trapped and passing states**. This "detrapping" and "retrapping" is a fundamental mechanism in turbulent transport. 

Finally, the very concept of an [adiabatic invariant](@entry_id:138014), like the bounce action $J_b = \oint v_{\parallel} ds$, relies on a [separation of timescales](@entry_id:191220). Near the trapped-passing [separatrix](@entry_id:175112), the turning points of a barely-trapped particle move close to the magnetic field maximum. The particle spends a very long time near these turning points, causing the bounce period $T_b$ to diverge logarithmically. Consequently, even very slow fluctuations with frequency $\omega$ can violate the adiabatic condition $\omega T_b \ll 1$. This breaks the invariance of $J_b$, leading to chaotic motion in a "boundary layer" of finite width in phase space around the [separatrix](@entry_id:175112). Particles in this layer can readily scatter between trapped and passing states, contributing significantly to transport. 