## Introduction
Locked modes, a type of magnetohydrodynamic (MHD) instability, pose a significant threat to the stable, high-performance operation of tokamak fusion devices. These stationary magnetic islands can degrade plasma confinement, reduce fusion power, and ultimately trigger catastrophic disruptions. Addressing this challenge requires a deep understanding of the underlying physics, from the initial formation of a tearing mode to its interaction with external fields and subsequent locking. This article provides a comprehensive overview of [locked mode](@entry_id:1127418) physics and avoidance, bridging the gap between fundamental theory and practical application. In the following chapters, you will first explore the core **Principles and Mechanisms** that govern tearing mode growth and the torque balance that leads to locking. We will then examine the **Applications and Interdisciplinary Connections**, detailing how this knowledge is used to design diagnostic systems, implement control strategies like [error field correction](@entry_id:749081) and active suppression, and build predictive models. Finally, the **Hands-On Practices** section will offer opportunities to apply these concepts to solve concrete problems in locked mode analysis and control.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the physics of tearing modes and their eventual locking to [static magnetic fields](@entry_id:195560). We will begin by defining the magnetic island, the topological structure at the heart of a [tearing mode](@entry_id:182276), and distinguishing it from ideal magnetohydrodynamic (MHD) instabilities. We will then explore the drivers and dynamics of these modes, the physics of their interaction with external fields, the balance of torques that leads to locking, and the unique characteristics of the particularly deleterious Neoclassical Tearing Mode (NTM). Finally, we will discuss the key diagnostic signatures used to identify locked modes in experimental settings.

### The Anatomy of a Tearing Mode: Magnetic Islands

In a tokamak, magnetic field lines are designed to trace out nested toroidal surfaces of constant magnetic flux, known as **flux surfaces**. This topology is essential for confining the hot plasma. However, this ideal configuration can be disrupted by instabilities. A crucial distinction exists between instabilities governed by ideal MHD and those that require non-ideal effects, such as [plasma resistivity](@entry_id:196902).

In **ideal MHD**, the plasma is treated as a perfect conductor, which imposes the **frozen-in law**, $\mathbf{E} + \mathbf{v} \times \mathbf{B} = \mathbf{0}$. A direct consequence of this law is that the topology of the magnetic field is preserved. Field lines are advected with the plasma fluid, meaning that flux surfaces can be distorted or bent, but they cannot be broken and reconnected. An ideal **[kink instability](@entry_id:192309)**, for example, manifests as a large-scale, helical deformation of the plasma column and its [frozen-in flux](@entry_id:275379) surfaces, but it does not create new topological structures like magnetic islands .

The formation of a **[magnetic island](@entry_id:1127585)** is a hallmark of a **resistive MHD** instability known as a **tearing mode**. In resistive MHD, Ohm's law is modified to include a term for finite [plasma resistivity](@entry_id:196902), $\eta$: $\mathbf{E} + \mathbf{v} \times \mathbf{B} = \eta \mathbf{J}$. While seemingly small, this resistive term is critically important at specific locations in the plasma known as **rational surfaces**. A rational surface, located at a minor radius $r_s$, is a surface where the pitch of the magnetic field lines matches the pitch of a potential helical perturbation. This condition is met when the **safety factor**, $q(r)$, which measures the number of toroidal turns a field line makes for each poloidal turn, takes on a rational value, $q(r_s) = m/n$, for integers $m$ and $n$.

At these resonant surfaces, a helical magnetic perturbation with mode numbers $(m,n)$ can drive a localized sheet of parallel current, $j_{\parallel}$. The finite resistivity allows the magnetic field to diffuse through the plasma, breaking the [frozen-in condition](@entry_id:201082) and enabling **magnetic reconnection**. This process fundamentally changes the magnetic topology. The original nested toroidal flux surfaces are torn and reconnected to form a new set of nested helical surfaces. This new topology is organized around a chain of $m$ magnetic islands located at the [rational surface](@entry_id:1130595).

The structure of a magnetic island is characterized by a distinct set of points and lines . At the center of each island is an **O-point**, an elliptic point around which the reconnected field lines form closed helical contours. The islands are separated by **X-points**, which are hyperbolic saddle points in the magnetic field structure. The special magnetic surface that passes through the X-points is called the **[separatrix](@entry_id:175112)**. It separates the closed flux surfaces within the island from the "passing" flux surfaces of the surrounding plasma. This change in [magnetic topology](@entry_id:751637), from toroidally nested surfaces to a chain of helically nested islands, is the defining feature of a [tearing mode](@entry_id:182276).

### The Classical Tearing Mode and the Role of $\Delta'$

The growth of a magnetic island depends on whether the reconnection process is energetically favorable. The source of free energy for a **classical [tearing mode](@entry_id:182276) (CTM)** is the gradient of the equilibrium toroidal current density. The stability of a CTM is quantified by a crucial parameter known as the **[tearing stability index](@entry_id:755828)**, denoted by $\Delta'$.

The calculation of $\Delta'$ is based on an [asymptotic matching](@entry_id:272190) procedure. The plasma is divided into a narrow "inner" resistive layer centered on the rational surface $r_s$, where reconnection occurs, and a broad "outer" region, where ideal MHD is assumed to hold. In the outer region, the linearized ideal MHD equations are solved for the perturbed helical magnetic flux, $\tilde{\psi}(r)$. While $\tilde{\psi}(r)$ is continuous across $r_s$, its radial derivative is generally not. The parameter $\Delta'$ is defined as the normalized jump in the [logarithmic derivative](@entry_id:169238) of this outer-region solution across the inner layer :
$$
\Delta' \equiv \frac{1}{\tilde{\psi}(r_s)}\left( \left.\frac{d\tilde{\psi}}{dr}\right|_{r_s^+} - \left.\frac{d\tilde{\psi}}{dr}\right|_{r_s^-} \right)
$$
Physically, $\Delta'$ represents the magnetic free energy available from the equilibrium current profile to drive reconnection. A positive value, $\Delta' \gt 0$, indicates that the plasma equilibrium is unstable to the formation of a tearing mode. A negative value, $\Delta' \lt 0$, indicates that the equilibrium is stable against spontaneous tearing.

In the nonlinear phase, when a finite-sized island of width $w$ has formed, its growth is described by the **Rutherford equation**. In its simplest form for a classical [tearing mode](@entry_id:182276), this equation relates the rate of change of the island width to $\Delta'$ and the [plasma resistivity](@entry_id:196902) $\eta$:
$$
\frac{dw}{dt} \propto \frac{\eta}{\mu_0} \Delta'
$$
This equation shows that for a classically unstable plasma ($\Delta' \gt 0$), the island width will grow over a resistive timescale. Conversely, for a classically stable plasma ($\Delta' \lt 0$), any small pre-existing island will decay and shrink . The magnitude of the growth or decay rate is proportional to $|\Delta'|$.

### Plasma Rotation and Field Penetration: Screening versus Forcing

Tokamak plasmas are rarely static; they typically exhibit significant toroidal and poloidal rotation. This rotation has a profound effect on how the plasma responds to external, static, non-axisymmetric magnetic fields, such as the **error fields** arising from imperfections in the magnetic field coils.

When a plasma rotates relative to a static, helical error field, the plasma fluid elements experience this field as an oscillating perturbation. The frequency of this oscillation in the plasma's rest frame is the **Doppler-shifted frequency**, $\omega_{\mathrm{pl}} = m\Omega_p - n\Omega_t$, where $\Omega_p$ and $\Omega_t$ are the poloidal and toroidal rotation frequencies of the plasma. If the [plasma rotation](@entry_id:753506) is sufficiently fast, the plasma responds in an almost ideal MHD manner. The frozen-in law dictates that the plasma will generate **screening currents** on the [rational surface](@entry_id:1130595) that oppose the external perturbation, effectively shielding the plasma interior from the error field and preventing reconnection. This phenomenon is known as **magnetic screening** . Screening is effective when the timescale for the perturbation to pass a point in the plasma, $1/|\omega_{\mathrm{pl}}|$, is much shorter than the characteristic [resistive diffusion time](@entry_id:1130912), $\tau_\eta$, across the resistive layer. This condition is expressed as $|\omega_{\mathrm{pl}}|\tau_\eta \gg 1$.

Conversely, if the plasma rotation is slow, or if it slows down, the Doppler-shifted frequency $\omega_{\mathrm{pl}}$ decreases. When $|\omega_{\mathrm{pl}}|\tau_\eta \lesssim 1$, resistivity becomes important. The magnetic field is no longer frozen to the fluid, allowing resistive slippage and enabling the external field to overcome the screening currents. The external field can then drive reconnection and force the formation of a magnetic island at the rational surface. This process is called **field penetration** .

This transition from screening to penetration can be intuitively understood using an L/R circuit analogy . The plasma's response can be modeled as a circuit with an inductance $L$ (representing the inertia of the screening currents) and a resistance $R$ (representing [plasma resistivity](@entry_id:196902)), driven by the external error field.
- **High Rotation (Screening):** At high rotation frequency, the response is inductive. The induced screening currents are strong, and their phase lags the driving field by approximately $90^\circ$. This leads to a small, suppressed magnetic response inside the plasma.
- **Low Rotation (Penetration):** At low rotation frequency, the response is resistive. The screening currents are weak, and the plasma's magnetic response becomes nearly in-phase with the external field. The field penetrates, and a large, locked island forms.

The transition from screening to penetration as plasma rotation slows is marked by a characteristic shift in the phase of the magnetic response from quadrature ($-90^\circ$) toward being in-phase ($0^\circ$), accompanied by a significant increase in the amplitude of the penetrated field. This phase evolution is a key precursor to [mode locking](@entry_id:264311).

### The Balance of Torques: Mechanisms of Mode Locking

A [tearing mode](@entry_id:182276), whether it arises spontaneously or is forced by an error field, will typically rotate with the surrounding plasma. A **[locked mode](@entry_id:1127418)** is a [tearing mode](@entry_id:182276) that has ceased to rotate and has become stationary with respect to the laboratory frame, usually "locked" to a static external error field. The locking process is a dynamic one, governed by a balance of torques acting on the plasma at the [rational surface](@entry_id:1130595).

The evolution of the island's rotation frequency, $\Omega$, can be described by a toroidal [momentum balance](@entry_id:1128118) equation for the tearing layer  . A simplified model for this balance takes the form:
$$
I_s \frac{d\Omega}{dt} = T_{\mathrm{visc}} + T_{\mathrm{EM}}
$$
where $I_s$ is the effective moment of inertia of the rotating layer. The two primary competing torques are:

1.  **Viscous Torque ($T_{\mathrm{visc}}$):** This term represents the net effect of momentum transport that tries to restore the island's rotation to the natural frequency of the background plasma, $\Omega_0$. It includes contributions from standard viscosity ([momentum diffusion](@entry_id:157895)) and, crucially, from **Neoclassical Toroidal Viscosity (NTV)**. NTV is a drag-like torque that arises from the interaction of particles with non-axisymmetric magnetic fields . By breaking the toroidal symmetry of the tokamak, these fields cause the radial drifts of trapped particles to become non-ambipolar. This generates a net radial current, $J_r$, which interacts with the equilibrium poloidal magnetic field, $B_p$, to produce a net toroidal $\mathbf{J} \times \mathbf{B}$ torque that [damps](@entry_id:143944) rotation. NTV acts as a volumetric momentum sink and can cause plasma spin-down even without direct interaction with the wall . The viscous restoring torque can be modeled as $T_{\mathrm{visc}} = -\Gamma (\Omega - \Omega_0)$, where $\Gamma$ represents the total [damping coefficient](@entry_id:163719).

2.  **Electromagnetic Torque ($T_{\mathrm{EM}}$):** This torque arises from the interaction between the helical currents of the rotating tearing mode and the static external error field. This interaction, a form of **Maxwell stress**, produces a braking torque that depends on the [relative phase](@entry_id:148120) angle, $\phi$, between the island and the error field. To leading order, this torque has a sinusoidal dependence, $T_{\mathrm{EM}}(\phi) \approx -T_0 \sin(\phi)$, where the amplitude $T_0$ is proportional to the strength of the error field and the size of the island .

A rotating tearing mode will begin to slow down, or "slip," relative to the bulk plasma when the electromagnetic braking torque becomes significant. The mode is said to lock when its rotation frequency $\Omega$ drops to zero. In a steady, locked state ($\Omega=0, d\Omega/dt=0$), the torque balance equation simplifies to:
$$
\Gamma \Omega_0 = -T_0 \sin(\phi)
$$
This equation states that for a mode to lock, the [electromagnetic torque](@entry_id:197212) must be able to balance the viscous torque that is trying to spin the island up to its natural frequency $\Omega_0$. A solution for the locked phase angle $\phi$ exists only if the magnitude of the viscous restoring torque is less than or equal to the maximum available electromagnetic torque, $|T_0|$. This leads to the **locking threshold condition**:
$$
|T_0| \ge \Gamma |\Omega_0|
$$
Since $T_0$ is proportional to the error field amplitude, this defines a minimum error field strength required to induce [mode locking](@entry_id:264311) .

### The Neoclassical Tearing Mode: A Pressure-Driven Instability

In high-temperature, low-collisionality plasmas typical of modern high-performance tokamaks, a different and often more dangerous type of [tearing mode](@entry_id:182276) can arise: the **Neoclassical Tearing Mode (NTM)**. Unlike a CTM, which is driven by the equilibrium current gradient ($\Delta' \gt 0$), an NTM can grow even when the plasma is classically stable ($\Delta' \lt 0$) .

The drive for an NTM comes from a perturbation to the **bootstrap current**. The bootstrap current is a self-generated current that arises from trapped particle dynamics in the presence of a [plasma pressure gradient](@entry_id:1129798) ($\nabla p$). When a [magnetic island](@entry_id:1127585) grows to a sufficient width, the rapid transport of particles and heat along the reconnected field lines flattens the pressure profile inside the island. This local flattening of $\nabla p$ eliminates the bootstrap current within the island. The result is a helical "hole" or deficit in the bootstrap current that has the same helical structure as the island itself.

This helical current deficit provides a powerful, positive feedback mechanism. According to Ampère's law, this missing current generates a magnetic perturbation that reinforces the original island, causing it to grow further. This drive is added to the classical Rutherford equation, which becomes the Modified Rutherford Equation (MRE):
$$
\frac{dw}{dt} \propto \eta \left( \Delta' + \Delta'_{bs}(w) \right)
$$
where $\Delta'_{bs}(w)$ is the destabilizing term from the bootstrap current deficit. This term is typically positive and increases with island width. For a classically stable plasma ($\Delta' \lt 0$), an NTM can grow if the bootstrap drive is strong enough to overcome the classical stabilization, i.e., $\Delta'_{bs}(w) > -\Delta'$.

Crucially, the pressure-flattening mechanism is only effective if the island is wider than a certain critical threshold, $w_{\text{crit}}$. This means that NTMs are nonlinearly unstable: they cannot grow from an infinitesimal perturbation. They require a finite-sized **seed island** to be triggered, which can be provided by other MHD events like a [sawtooth crash](@entry_id:754512) or an Edge Localized Mode (ELM) .

### Locking of Neoclassical Tearing Modes

The additional growth drive for NTMs has significant consequences for their locking behavior. Comparing an NTM to a CTM under identical background conditions and error field strengths reveals key differences .

First, due to the additional bootstrap drive, an NTM will typically grow to a much larger saturated island width than a CTM. This has a direct impact on the island's natural rotation frequency, $\Omega_0(w)$. Neoclassical theory and experimental observations show that the magnitude of $\Omega_0(w)$ tends to decrease as the island width $w$ increases. Therefore, the larger NTM island will have a smaller natural frequency.

Recalling the locking threshold, $|T_0| \ge \Gamma |\Omega_0|$, a smaller natural frequency $|\Omega_0|$ means that the viscous restoring torque is weaker. Consequently, a smaller electromagnetic torque $|T_0|$, and thus a smaller external error field, is required to stop the island's rotation. This means that **NTMs generally have a lower locking threshold and are easier to lock than CTMs** .

Furthermore, the strong, nonlinear feedback from the bootstrap [current drive](@entry_id:186346) often leads to **hysteretic behavior**. This means the error field value required to cause locking as the field is increased is higher than the value at which the mode unlocks as the field is subsequently decreased. This [bistability](@entry_id:269593) is a characteristic feature of NTM dynamics that is largely absent for CTMs .

### Experimental Signatures of Locked Modes

The transition from a rotating [tearing mode](@entry_id:182276) to a stationary locked mode is accompanied by clear, observable changes in diagnostic signals. The primary tools for identifying this transition are magnetic pickup coils and soft X-ray detectors .

-   **Magnetic Diagnostics (Mirnov Coils):** Mirnov coils are small coils placed around the plasma edge that measure the time-derivative of the [poloidal magnetic field](@entry_id:753563), $V_{\text{Mirnov}} \propto d B_\theta/dt$. For a rotating [tearing mode](@entry_id:182276) with frequency $\Omega$, these coils detect a sinusoidal signal with frequency $m\Omega$. As the mode slows down and locks, its frequency $\Omega \to 0$. Consequently, the measured voltage signal, being proportional to the time derivative, **decays to near zero**. Simultaneously, analysis of the phase of the magnetic perturbation from an array of toroidally or poloidally separated coils shows that the phase, which had been advancing linearly in time, **stagnates and becomes constant**. This phase stagnation is the definitive signature of locking.

-   **Soft X-Ray (SXR) Diagnostics:** SXR cameras measure the emissivity of the plasma, which is a strong function of electron temperature and density. The flattened pressure profile inside a magnetic island typically corresponds to a region of reduced SXR emissivity. For a rotating [tearing mode](@entry_id:182276), SXR detectors viewing the [rational surface](@entry_id:1130595) observe a **periodic modulation or dip** in the signal as the cooler island sweeps past their line of sight. When the mode locks, this island structure becomes stationary. The periodic modulations cease, and are replaced by a **time-independent, stationary depression** in the SXR emissivity profile at the spatial location of the locked island.

Together, the decay and phase stagnation of the magnetic signals, combined with the cessation of SXR modulations, provide an unambiguous identification of a locked mode event in a tokamak experiment.