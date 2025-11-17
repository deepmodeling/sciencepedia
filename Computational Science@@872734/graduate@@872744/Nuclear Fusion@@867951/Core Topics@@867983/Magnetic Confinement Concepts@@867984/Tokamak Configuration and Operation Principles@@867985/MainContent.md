## Introduction
The tokamak stands as the most advanced and promising concept for achieving [controlled thermonuclear fusion](@entry_id:197369), offering a potential path to a clean, safe, and virtually limitless energy source. The central challenge of [fusion energy](@entry_id:160137) lies in confining a plasma of deuterium and tritium at temperatures exceeding 100 million degrees Celsius—hotter than the core of the sun. The tokamak addresses this by using a powerful and complex magnetic field to insulate the hot plasma from the surrounding material walls. A deep understanding of the principles governing this [magnetic confinement](@entry_id:161852) is therefore essential for designing, operating, and optimizing these remarkable machines.

This article provides a comprehensive exploration of the [tokamak](@entry_id:160432)'s configuration and operational principles, bridging the gap between fundamental plasma theory and its application in real-world fusion experiments. We will dissect the intricate physics that allows a [tokamak](@entry_id:160432) to function, from the basic [force balance](@entry_id:267186) that holds the plasma in place to the sophisticated control schemes required for high performance. The journey begins in the **Principles and Mechanisms** chapter, which establishes the theoretical bedrock of magnetohydrodynamic (MHD) equilibrium, details the construction of the toroidal and poloidal magnetic fields, and explains how this configuration confines individual particles and dictates collective [plasma stability](@entry_id:197168). Building on this foundation, the **Applications and Interdisciplinary Connections** chapter demonstrates how these principles are applied to solve practical challenges, such as initiating and heating the plasma, pushing operational limits, controlling instabilities, and designing integrated systems for a steady-state reactor. Finally, the **Hands-On Practices** section provides an opportunity to actively engage with the material, reinforcing key theoretical concepts through guided problem-solving.

## Principles and Mechanisms

### The Foundation: Magnetohydrodynamic Equilibrium

The fundamental principle underlying the confinement of a hot, quasi-neutral plasma in a tokamak is the concept of **magnetohydrodynamic (MHD) equilibrium**. In a static state, where plasma flow is negligible, the outward-pushing force of the plasma's kinetic pressure must be precisely balanced by an inward-acting [electromagnetic force](@entry_id:276833). This equilibrium is described by the deceptively simple vector equation:

$$ \nabla p = \mathbf{J} \times \mathbf{B} $$

Here, $p$ represents the scalar [plasma pressure](@entry_id:753503), $\mathbf{J}$ is the electric current density within the plasma, and $\mathbf{B}$ is the magnetic field. This equation states that the [pressure gradient force](@entry_id:262279), which drives the plasma to expand, is counteracted by the Lorentz force exerted by the plasma's own currents interacting with the magnetic field.

This equilibrium condition has profound consequences for the topology of the confining magnetic field. By taking the dot product of the [equilibrium equation](@entry_id:749057) with $\mathbf{B}$ and $\mathbf{J}$ respectively, we find that $\mathbf{B} \cdot \nabla p = 0$ and $\mathbf{J} \cdot \nabla p = 0$. These results signify that both the magnetic field lines and the current density vectors must lie on surfaces of constant pressure. In an axisymmetric toroidal system like a tokamak, these surfaces form a set of nested tori known as **[magnetic flux surfaces](@entry_id:751623)**. Each surface can be labeled by a coordinate, the **poloidal magnetic flux** $\psi$, which is constant on that surface. Consequently, pressure becomes a function of this coordinate alone, $p = p(\psi)$, and the current density is constrained to flow within these surfaces, satisfying $\mathbf{J} \cdot \nabla \psi = 0$ [@problem_id:3722805]. The equilibrium [force balance](@entry_id:267186) is therefore a balance across flux surfaces, where the pressure gradient $\nabla p = (dp/d\psi)\nabla\psi$ is oriented normal to the surfaces and is balanced by the Lorentz force, which must also be normal to the surfaces [@problem_id:3722805].

The Lorentz force itself can be decomposed into two distinct components by substituting Ampère's law, $\mu_0 \mathbf{J} = \nabla \times \mathbf{B}$:

$$ \mathbf{J} \times \mathbf{B} = -\nabla\left(\frac{B^2}{2\mu_0}\right) + \frac{(\mathbf{B} \cdot \nabla)\mathbf{B}}{\mu_0} $$

The first term, $-\nabla(B^2/2\mu_0)$, is the **[magnetic pressure](@entry_id:272413)** force, which acts from regions of high magnetic field strength to low magnetic field strength. The second term, $(\mathbf{B} \cdot \nabla)\mathbf{B}/\mu_0$, is the **magnetic tension** force, which acts to straighten bent magnetic field lines. In a [tokamak](@entry_id:160432), the [toroidal geometry](@entry_id:756056) means the magnetic field lines are curved. This curvature, particularly of the strong [toroidal field](@entry_id:194478) component $B_\phi$, gives rise to a tension force of magnitude $\sim B_\phi^2/(\mu_0 R)$ (where $R$ is the major radius), which is directed radially *inward* toward the major axis of the torus. This inward "hoop force" is a crucial component of the overall [force balance](@entry_id:267186), helping to confine the plasma against its own pressure [@problem_id:3722805].

### Constructing the Tokamak Magnetic Field

To create the [nested flux surfaces](@entry_id:752411) required for equilibrium, a [tokamak](@entry_id:160432) employs a carefully designed set of magnetic fields with two primary components: a strong **[toroidal field](@entry_id:194478)** and a weaker **[poloidal field](@entry_id:188655)**. The toroidal direction, denoted by the angle $\phi$, is the long way around the torus, while the poloidal direction, denoted by the angle $\theta$, is the short way around the plasma cross-section [@problem_id:3722751]. The combination of these fields results in helical magnetic field lines that trace out the flux surfaces.

#### The Toroidal Field System

The dominant magnetic field component, the **[toroidal field](@entry_id:194478)** $B_\phi$, is generated by a set of large, discrete coils arranged symmetrically around the vacuum vessel. These **Toroidal Field (TF) coils** effectively form a toroidal solenoid. Applying Ampère's law to a circular path concentric with the machine's major axis reveals that the magnitude of the vacuum [toroidal field](@entry_id:194478) scales inversely with the major radius, $R$:

$$ B_\phi(R) \approx \frac{\mu_0 N I_{\text{coil}}}{2\pi R} $$

where $N$ is the number of TF coils and $I_{\text{coil}}$ is the current in each coil [@problem_id:3722723]. This $1/R$ dependence means the field is stronger on the inboard side (small $R$) and weaker on the outboard side (large $R$) of the plasma.

#### The Poloidal Field System

A purely [toroidal magnetic field](@entry_id:756057) cannot by itself confine a plasma in equilibrium. The pressure gradient and [field curvature](@entry_id:162957) would cause the plasma to drift vertically and hit the vessel walls. To create the necessary [nested flux surfaces](@entry_id:752411) and achieve force balance, a **[poloidal magnetic field](@entry_id:753563)** ($B_\theta$) is required. In a tokamak, this crucial field is primarily generated by a large toroidal current, $I_\phi$, flowing within the plasma itself. By Ampère's law, this toroidal current induces a [poloidal magnetic field](@entry_id:753563) that encircles the plasma cross-section, with a magnitude approximately given by $B_\theta(r) \approx \mu_0 I_\phi(r)/(2\pi r)$ for a circular cross-section of minor radius $r$ [@problem_id:3722751].

The generation of this [poloidal field](@entry_id:188655) by an internal plasma current is the defining characteristic of the [tokamak](@entry_id:160432) concept, distinguishing it from other confinement devices like the [stellarator](@entry_id:160569), which uses complex, three-dimensional external coils to generate the entire confining field without requiring a net [toroidal plasma](@entry_id:202484) current [@problem_id:3722751]. The initial plasma current is typically induced by a [central solenoid](@entry_id:747208), which acts as the primary winding of a transformer, with the plasma ring forming the secondary winding. Additional sets of external **Poloidal Field (PF) coils** are used to shape the plasma cross-section and maintain its position.

### Properties of the Magnetic Configuration

The superposition of the externally generated [toroidal field](@entry_id:194478) and the internally generated [poloidal field](@entry_id:188655) creates a complex [magnetic structure](@entry_id:201216) with several key properties that determine the plasma's confinement and stability.

#### Magnetic Flux Surfaces and Coordinates

As established, in an axisymmetric equilibrium, the magnetic field lines lie on nested toroidal flux surfaces. The magnetic field can be formally expressed in a way that makes this structure explicit, known as the Clebsch representation:

$$ \mathbf{B} = \nabla\phi \times \nabla\psi + I(\psi) \nabla\phi $$

Here, $\nabla\phi = \hat{\mathbf{e}}_\phi/R$ is the gradient of the toroidal angle, $\psi(R,Z)$ is the [poloidal flux](@entry_id:753562) function whose level sets define the flux surfaces, and $I(\psi) = R B_\phi$ is a flux function related to the poloidal current. The first term represents the [poloidal field](@entry_id:188655) $\mathbf{B}_p$, and the second term represents the [toroidal field](@entry_id:194478) $\mathbf{B}_t$ [@problem_id:3722751]. The **magnetic axis** is the center of the [nested flux surfaces](@entry_id:752411), where $\psi$ is extremal and the [poloidal field](@entry_id:188655) is zero.

#### Safety Factor and Magnetic Shear

The helical nature of the magnetic field lines is quantified by the **[safety factor](@entry_id:156168)**, $q$. It represents the number of times a field line winds toroidally for every single poloidal transit. For a large-aspect-ratio circular [tokamak](@entry_id:160432), it is approximately $q(r) \approx (r/R_0)(B_\phi/B_\theta)$. The value of $q$ typically varies with radial position, defining a **[q-profile](@entry_id:180285)**, $q(r)$.

Surfaces where the [safety factor](@entry_id:156168) is a rational number, $q(r_s) = m/n$ for integers $m$ and $n$, are called **rational surfaces**. On these surfaces, a magnetic field line closes back on itself after $m$ toroidal transits and $n$ poloidal transits. As we will see, these surfaces are particularly important for [plasma stability](@entry_id:197168), as they are locations where helical plasma perturbations with the same pitch can resonate with the magnetic field [@problem_id:3722755].

The radial variation of the safety factor is described by the **magnetic shear**, a dimensionless quantity defined as:

$$ s = \frac{r}{q}\frac{dq}{dr} $$

Magnetic shear measures the rate at which the pitch of the field lines changes with radius. A standard [tokamak](@entry_id:160432) has **positive shear** ($s > 0$), where $q$ increases monotonically from the center outwards. Configurations with a non-monotonic [q-profile](@entry_id:180285) can have regions of **negative or reversed shear** ($s  0$) or zero shear ($s=0$) [@problem_id:3722721]. Magnetic shear is a powerful tool for controlling [plasma instabilities](@entry_id:161933).

#### Toroidal Field Ripple

The use of a finite number, $N$, of TF coils breaks the perfect axisymmetry of the [tokamak](@entry_id:160432). This discreteness creates a periodic [modulation](@entry_id:260640) of the [toroidal field](@entry_id:194478) strength in the $\phi$ direction, known as **Toroidal Field (TF) ripple**. The ripple amplitude, $\delta \equiv (B_{\phi,\max} - B_{\phi,\min})/\langle B_\phi \rangle$, is largest between the coils and smallest in the plane of the coils. The magnitude of the ripple decreases strongly as the number of coils $N$ increases. Spatially, ripple is much larger on the outboard side of the torus (where the coils are farther apart) and decreases significantly toward the inboard side [@problem_id:3722723]. This seemingly small deviation from axisymmetry can have significant consequences for the confinement of energetic particles.

#### Plasma Shaping

Modern [tokamaks](@entry_id:182005) move beyond simple circular [cross-sections](@entry_id:168295) to achieve higher performance. The shape of the plasma boundary is typically described by two key parameters: **elongation** ($\kappa$) and **[triangularity](@entry_id:756167)** ($\delta$). Elongation refers to the vertical stretching of the plasma ($\kappa = Z_{\max}/a$, where $Z_{\max}$ is the half-height and $a$ is the minor radius), which allows for a higher [plasma current](@entry_id:182365) for a given safety factor. Triangularity describes the "D-shape" of the plasma. A positive [triangularity](@entry_id:756167) points the "tip" of the D-shape away from the major axis. These shapes can be parameterized using a Fourier series for the boundary coordinates $R(\theta)$ and $Z(\theta)$. For a simple, up-down symmetric shape given by $R(\theta) = R_0 + a \cos\theta - a\delta\cos(2\theta)$ and $Z(\theta) = a\kappa\sin\theta$, the parameters $\kappa$ and $\delta$ can be directly related to the coefficients of the series [@problem_id:3722777]. Advanced shaping is critical for accessing high-performance operating regimes.

### Particle Confinement and Transport

The primary function of the magnetic configuration is to confine the energetic plasma particles long enough for [fusion reactions](@entry_id:749665) to occur. In an ideal, perfectly axisymmetric field, this confinement is remarkably effective.

#### Guiding-Center Orbits and Conserved Quantities

The motion of a charged particle in a strong, slowly varying magnetic field can be simplified to the motion of its **[guiding center](@entry_id:189730)**, the point around which the particle executes its rapid [gyromotion](@entry_id:204632). In an axisymmetric [tokamak](@entry_id:160432), the toroidal angle $\phi$ is an ignorable coordinate in the [equations of motion](@entry_id:170720). By Noether's theorem, this symmetry implies the existence of a conserved quantity: the **[canonical toroidal angular momentum](@entry_id:747109)**, $P_\phi$.

$$ P_\phi = m R v_\phi + q_s \psi = \text{constant} $$

Here, $m$ and $q_s$ are the particle's mass and charge, $R$ is its major radial position, $v_\phi$ is its toroidal velocity, and $\psi$ is the [poloidal flux](@entry_id:753562) at its location [@problem_id:3722793]. This conservation law is the bedrock of single-[particle confinement](@entry_id:148454) in a [tokamak](@entry_id:160432). It strictly limits the radial excursion of a particle's guiding center, as any movement across flux surfaces (a change in $\psi$) must be compensated by a corresponding change in its mechanical momentum ($m R v_\phi$).

#### Drift Surfaces and Orbit Widths

Due to the curvature and gradient of the magnetic field, guiding centers do not follow magnetic field lines exactly. They experience slow drifts, primarily the $\nabla B$ and curvature drifts, which are perpendicular to the magnetic field. The path traced by a drifting [guiding center](@entry_id:189730) is called a **drift surface**. Because of the $P_\phi$ conservation, these drift surfaces deviate only slightly from the [magnetic flux surfaces](@entry_id:751623).

Particles can be divided into two classes based on their velocity parallel to the magnetic field. **Passing particles** have sufficient parallel velocity to travel continuously around the torus. Their drift surfaces are radially shifted circles or ovals. **Trapped particles** have low parallel velocity and are magnetically mirrored in the weak-field region on the outboard side of the torus. Their guiding centers trace out a characteristic "banana" shape in the poloidal plane. The width of these [banana orbits](@entry_id:202619) represents the maximum radial deviation of the particle's drift surface from a single flux surface [@problem_id:3722793].

#### The Role of Magnetic Shear in Orbits

Magnetic shear influences orbit topology by changing the field line pitch and thus the characteristic frequencies of particle motion (bounce/transit and precession frequencies). This can affect the width of orbits and, by causing particles that move radially to experience different magnetic structures, can help decorrelate large radial excursions that might otherwise lead to enhanced transport [@problem_id:3722793].

#### Ripple-Induced Transport

The conservation of $P_\phi$ relies on perfect axisymmetry. The small but finite TF ripple breaks this symmetry. In the ripple "wells" between TF coils, local magnetic traps can form. Particles with low parallel velocity, especially high-energy ions from heating systems, can become trapped in these ripple wells. Once trapped, they experience a rapid, uncompensated vertical drift that can quickly carry them out of the plasma. This process, known as **ripple trapping**, is a significant loss mechanism for energetic ions, particularly on the outboard side of the tokamak where ripple is largest [@problem_id:3722723].

### Plasma Stability and Control

A plasma that is in MHD equilibrium is not necessarily stable. It can be susceptible to a variety of collective instabilities that can degrade confinement or even terminate the discharge. Understanding and controlling these instabilities is a central theme of fusion research.

#### MHD Instabilities and Rational Surfaces

Many large-scale MHD instabilities are driven by the plasma current and pressure gradients. These modes tend to be helical in nature, with a specific poloidal mode number $m$ and toroidal mode number $n$. A key insight is that these modes are most easily excited at the rational surfaces where the mode's [helicity](@entry_id:157633) matches that of the equilibrium magnetic field, i.e., where $q = m/n$. At these resonant locations, the restoring force associated with field-line bending is minimized because the perturbation's parallel wavevector, $k_\parallel$, vanishes.

In a real plasma with finite [electrical resistivity](@entry_id:143840), this resonance allows for **[magnetic reconnection](@entry_id:188309)**, where magnetic field lines are cut and re-joined, forming structures called **[magnetic islands](@entry_id:197895)**. This process gives rise to **[tearing modes](@entry_id:194294)**, which can degrade confinement by creating shortcuts for heat and particles to escape across the [nested flux surfaces](@entry_id:752411). A particularly important instability is the $m/n=1/1$ **[internal kink mode](@entry_id:750752)**, which can be triggered if the central [safety factor](@entry_id:156168) $q(0)$ drops below 1. This mode is thought to be the primary driver of **[sawtooth oscillations](@entry_id:754514)**, a periodic crash in the central [plasma temperature](@entry_id:184751) and density [@problem_id:3722755].

#### The Role of Magnetic Shear in Stability

Magnetic shear is one of the most powerful mechanisms for stabilizing MHD modes. For an instability to grow radially, it must extend away from its resonant rational surface. In a sheared magnetic field, moving radially means moving to a region with a different field line pitch. The helical perturbation is then no longer aligned with the [local field](@entry_id:146504), resulting in a large $k_\parallel$ and a strong stabilizing restoring force from field-line bending. This line-bending energy, which scales as $s^2$, is a potent stabilizer of **interchange modes**. Thus, increasing the magnitude of the shear, $|s|$, enhances stability against these modes, regardless of the sign of $s$.

The sign of the shear, however, is critical for **[ballooning modes](@entry_id:195101)**. These pressure-driven modes "balloon" on the outboard side of the torus to take advantage of the unfavorable magnetic curvature there. In a standard positive shear ($s > 0$) configuration, the mode tends to be strongly localized in the bad-curvature region, making it more unstable. In a negative or reversed shear ($s  0$) configuration, the [magnetic topology](@entry_id:751637) enhances the connection between the outboard bad-curvature region and the inboard good-curvature region. This allows the stabilizing effect of good curvature to be more effective, generally making the plasma more stable against [ballooning modes](@entry_id:195101) for a given pressure gradient [@problem_id:3722721].

#### Plasma Current Drive and Profile Control

Since the [plasma current](@entry_id:182365) profile (and thus the [q-profile](@entry_id:180285) and shear profile) is critical for stability, controlling it is paramount. The total current in a [tokamak](@entry_id:160432) is a sum of several components:

1.  **Ohmic Current ($j_\Omega$)**: This is the current driven by the toroidal electric field induced by the [central solenoid](@entry_id:747208). It follows a form of Ohm's law, $j_\Omega = \sigma E_\phi$, where the Spitzer conductivity $\sigma$ scales strongly with [electron temperature](@entry_id:180280) as $T_e^{3/2}$. Since the plasma core is hottest, the ohmic current profile is typically peaked in the center [@problem_id:3722766].
2.  **Bootstrap Current ($j_{bs}$)**: This is a "self-generated" current arising from neoclassical effects in a [toroidal geometry](@entry_id:756056). The pressure gradient, through its interaction with [trapped particles](@entry_id:756145), drives a parallel current that requires no external driver. This current is particularly strong in regions of high pressure gradient. In modern high-performance (H-mode) plasmas, a steep pressure gradient forms at the plasma edge (the "pedestal"), leading to a large, localized [bootstrap current](@entry_id:182038) in the edge region [@problem_id:3722766].
3.  **External Non-inductive Current Drive ($j_{CD}$)**: To sustain the [plasma current](@entry_id:182365) for long pulses or in steady-state (when the [central solenoid](@entry_id:747208)'s flux is exhausted), external power must be injected. This can be done by launching radio-frequency (RF) waves (e.g., Lower Hybrid Current Drive, Electron Cyclotron Current Drive) that transfer momentum to the electrons, or by injecting high-energy neutral atom beams (Neutral Beam Injection - NBI) that deposit fast ions which then circulate and constitute a current. These methods are not only essential for [steady-state operation](@entry_id:755412) but also provide powerful tools for actively controlling the [current density](@entry_id:190690) profile to optimize stability and performance [@problem_id:3722766].

### The Plasma Boundary and Power Exhaust

The outermost region of the confined plasma plays a critical role in the overall performance and longevity of a fusion device. This region mediates the interaction between the hot core plasma and the material walls of the vacuum vessel.

#### The Separatrix and Scrape-Off Layer (SOL)

In modern [tokamaks](@entry_id:182005), the plasma boundary is not defined by a solid object (a "limiter") but by a [magnetic topology](@entry_id:751637). Poloidal field coils are used to create a magnetic null point in the [poloidal field](@entry_id:188655), known as an **X-point**. The flux surface that passes through this X-point is called the **separatrix** or the **Last Closed Flux Surface (LCFS)**. It separates the inner region of closed, [nested flux surfaces](@entry_id:752411) (the confined plasma) from an outer region where the field lines are "open"—they terminate on material surfaces called **[divertor](@entry_id:748611) targets**.

This outer region of open field lines is called the **Scrape-Off Layer (SOL)**. Plasma and energy that cross the [separatrix](@entry_id:175112) from the core are rapidly transported along the magnetic field lines in the SOL to the [divertor](@entry_id:748611) targets. A **single-null** configuration has one X-point and two [divertor](@entry_id:748611) legs (an inner and outer one), while a **double-null** configuration has two X-points (top and bottom) and four divertor legs [@problem_id:3722801].

#### The Physics of the SOL and Divertor

Transport in the SOL is highly anisotropic. Due to the rapid motion of particles along magnetic field lines, parallel transport dominates over perpendicular (cross-field) transport. Particles and energy are channeled along the SOL to the [divertor](@entry_id:748611) targets on a much faster timescale than they diffuse radially across the SOL. The thickness of the SOL is therefore determined by a balance: it is set by the rate of slow perpendicular transport feeding the layer from the core, balanced against the rate of rapid parallel transport draining the layer to the divertor [@problem_id:3722801].

The narrow [divertor](@entry_id:748611) legs serve to channel the exhausted plasma power to a remote, heavily shielded location, protecting the main chamber walls. However, this concentrates the heat flux onto the divertor targets to extreme levels. A key challenge is to dissipate this power before it strikes the target. This is achieved through a process called **detachment**. By injecting gas into the divertor region, a cold, dense plasma is created in front of the target. In this state, volumetric processes such as ion-neutral [charge exchange](@entry_id:186361) and ion-electron recombination become dominant. These processes dissipate the plasma's momentum and convert its thermal energy into radiated light, which is spread over a large surface area. This causes a dramatic drop in the particle and heat flux reaching the target, effectively "detaching" the hot plasma from the material surface in a fluid sense [@problem_id:3722801].

### Performance Metrics and the Path to Fusion

The ultimate goal of a tokamak is to function as a net energy source. Several key metrics are used to quantify progress toward this goal.

#### Global Power Balance and Energy Confinement

In a steady-state plasma, the total heating power must balance the total power loss. The heating consists of external auxiliary heating ($P_{\text{aux}}$) and self-heating from fusion-produced alpha particles ($P_\alpha$). The power loss ($P_{\text{loss}}$) is due to transport of energy out of the plasma. This balance is characterized by the **global [energy confinement time](@entry_id:161117)**, $\tau_E$:

$$ \tau_E = \frac{W}{P_{\text{loss}}} = \frac{W}{P_{\text{aux}} + P_\alpha} $$

where $W$ is the total thermal energy stored in the plasma. A longer $\tau_E$ signifies better insulation and a more efficient device.

#### Fusion Gain and Ignition

The performance of a fusion plasma is often measured by the **fusion gain**, $Q$, defined as the ratio of the total [fusion power](@entry_id:138601) produced ($P_{\text{fus}}$) to the external heating power required to sustain it:

$$ Q = \frac{P_{\text{fus}}}{P_{\text{aux}}} $$

A value of $Q=1$ represents [scientific breakeven](@entry_id:754572), where the [fusion power](@entry_id:138601) equals the heating power. A power plant will require $Q > 10$. The ultimate goal is **ignition**, a self-sustaining plasma where external heating is no longer needed ($P_{\text{aux}} = 0$), corresponding to $Q \to \infty$. In an ignited plasma, the transport losses are balanced solely by the alpha-particle self-heating ($P_\alpha = P_{\text{loss}}$) [@problem_id:3722745].

#### The Fusion Triple Product

The conditions for achieving a certain level of performance can be encapsulated in a single figure of merit. By analyzing the power balance, one can derive a condition on the product of the plasma density ($n$), temperature ($T$), and [energy confinement time](@entry_id:161117) ($\tau_E$). For a deuterium-tritium plasma with $T_e = T_i = T$ and neglecting radiation losses, the requirement for a given $Q$ is:

$$ n T \tau_E = \frac{12 T^2}{E_{\text{fus}} \langle\sigma v\rangle (f_\alpha + 1/Q)} $$

where $\langle\sigma v\rangle$ is the temperature-dependent fusion reactivity and $f_\alpha \approx 0.2$ is the fraction of fusion energy carried by alpha particles. The condition for ignition ($Q \to \infty$) is known as the **Lawson criterion**. This **[fusion triple product](@entry_id:749673)**, $n T \tau_E$, is a widely used metric for comparing experimental results and gauging progress toward a reactor [@problem_id:3722745].

To bridge the gap between theoretical requirements and experimental reality, performance is often compared against empirical [scaling laws](@entry_id:139947) derived from a database of results from many tokamaks. The **confinement enhancement factor**, $H_{98} = \tau_E / \tau_{98}$, measures how much better (or worse) the experimentally achieved confinement time $\tau_E$ is compared to a standard scaling prediction (e.g., the ITER98y2 scaling, $\tau_{98}$). Achieving $H_{98} \ge 1$ is a common target for reactor designs, indicating that the [plasma confinement](@entry_id:203546) is at least as good as the empirically expected value [@problem_id:3722745].