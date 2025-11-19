## Introduction
Scanning Probe Microscopy (SPM) represents a paradigm shift in our ability to see and manipulate the world at the nanoscale. These powerful techniques, which include Scanning Tunneling Microscopy (STM) and Atomic Force Microscopy (AFM), have become indispensable tools across science and engineering. However, truly harnessing their potential requires moving beyond a black-box appreciation to a deep understanding of the intricate physics that governs their operation. This article addresses the gap between casual use and expert interpretation by building a robust conceptual foundation from first principles. Over the next three chapters, you will gain a comprehensive understanding of SPM. The journey begins with **Principles and Mechanisms**, where we will explore the fundamental probe-sample interactions and instrumental components that are the bedrock of all SPM methods. We will then see these principles in action in **Applications and Interdisciplinary Connections**, demonstrating how SPM is used to solve real-world problems in materials science, physics, and biology. Finally, the **Hands-On Practices** chapter will challenge you to apply this knowledge to interpret data and diagnose common experimental issues, solidifying your expertise.

## Principles and Mechanisms

Scanning Probe Microscopy (SPM) constitutes a family of advanced surface analysis techniques that achieve nanoscale and often [atomic resolution](@entry_id:188409) by mechanically scanning a sharp probe in close proximity to a sample. The operational principle common to all SPM variants is the [transduction](@entry_id:139819) of a highly localized probe-sample interaction into a measurable signal. This signal is typically used in a feedback loop to maintain a constant [interaction strength](@entry_id:192243) by adjusting the vertical separation between the tip and sample. By raster scanning the probe across the surface and recording the feedback response (e.g., the vertical position of the probe) or the interaction signal itself at each lateral coordinate, a three-dimensional map of a specific surface property is constructed. This chapter elucidates the fundamental physical principles and mechanisms that govern the operation of the most prominent SPM techniques. [@problem_id:2519920]

### Fundamental Probe-Sample Interactions

The versatility of SPM stems from the diverse range of physical interactions that can be harnessed as the probing mechanism. Each distinct interaction gives rise to a unique SPM modality with its own specific contrast mechanism and application domain. The three primary modalities discussed here are Scanning Tunneling Microscopy (STM), Atomic Force Microscopy (AFM), and scattering-type Scanning Near-field Optical Microscopy (s-SNOM).

**Scanning Tunneling Microscopy (STM)** is predicated on the quantum mechanical phenomenon of [electron tunneling](@entry_id:272729). When a sharp, electrically conductive tip is positioned within a few angstroms of a conductive or semiconductive sample, and a bias voltage $V$ is applied, electrons can tunnel through the classically forbidden vacuum [potential barrier](@entry_id:147595) separating the tip and sample. This flow of electrons constitutes the **tunneling current** $I$, which serves as the primary observable. The dominant interaction is therefore the [quantum mechanical tunneling](@entry_id:149523) of electrons, driven by the overlap of electronic wavefunctions under an applied electric field. In its spectroscopic mode, the voltage derivative of the current, $\mathrm{d}I/\mathrm{d}V$, is measured to probe the local density of electronic states (LDOS). [@problem_id:2519920]

**Atomic Force Microscopy (AFM)** operates by measuring forces between the probe and the sample. The probe consists of a sharp tip mounted on a flexible micro-cantilever, which acts as a sensitive force transducer. The dominant interaction is the **total tip-sample force** $F_{\mathrm{ts}}$, which is a sum of various contributions, including short-range Pauli repulsion, long-range van der Waals forces, electrostatic forces, and, in ambient conditions, capillary forces. The primary observable is the mechanical response of the cantilever. In static or "contact" mode, the [cantilever](@entry_id:273660)'s static deflection is measured. In dynamic modes, the [cantilever](@entry_id:273660) is oscillated, and changes in its oscillation amplitude, phase, or resonance frequency shift $\Delta f$—caused by the tip-sample [force gradient](@entry_id:190895) $\partial F_{\mathrm{ts}} / \partial z$—are recorded. [@problem_id:2519920]

**scattering-type Scanning Near-field Optical Microscopy (s-SNOM)** extends [microscopy](@entry_id:146696) into the optical domain with sub-diffraction-limit resolution. It combines the principles of AFM with optical scattering. Here, a laser illuminates the sharp, often metallic, AFM tip, which acts as an optical antenna to create a strongly enhanced and confined electromagnetic near-field at its apex. The dominant interaction is the **optical near-field coupling** between the illuminated tip and the sample. This interaction is highly sensitive to the local dielectric properties of the material beneath the tip. The primary observable is the far-field scattered light from the tip-sample junction. To isolate the weak [near-field](@entry_id:269780) signal from the large, dominant background of far-field scattering, the tip is oscillated vertically, and the detected optical signal is demodulated at higher harmonics of the tip's [oscillation frequency](@entry_id:269468). The amplitude and phase of this demodulated optical signal provide nanoscale maps of the sample's complex [optical constants](@entry_id:186307). [@problem_id:2519920]

### The Physics of Scanning Tunneling Microscopy (STM)

The theoretical foundation of STM lies in the quantum mechanical description of electron transport across a potential barrier. Within the Wentzel–Kramers–Brillouin (WKB) approximation for a one-dimensional barrier, the tunneling probability, and thus the tunneling current $I$, depends exponentially on the tip-sample separation $z$ and the square root of the apparent barrier height $\phi$. For small bias voltages, the current $I$ can be expressed as:

$I \propto V \exp\left(-\frac{2\sqrt{2 m \phi}}{\hbar} z\right)$

Here, $m$ is the electron mass, $\hbar$ is the reduced Planck constant, and $\phi$ is the apparent barrier height, which is related to the work functions of the tip and sample materials. This exponential relationship is the key to STM's exquisite vertical sensitivity. The [logarithmic derivative](@entry_id:169238) of the current with respect to distance, often called the inverse decay length, is directly proportional to the square root of the barrier height:

$S \equiv \frac{\mathrm{d}(\ln I)}{\mathrm{d}z} = -\frac{2\sqrt{2 m \phi}}{\hbar}$

This relationship shows that a typical change in current of an [order of magnitude](@entry_id:264888) can result from a change in distance of only one angstrom, and that the apparent barrier height can be experimentally determined by modulating the tip-sample separation and measuring the corresponding change in current. It is important to note that the apparent barrier height is not an intrinsic property of the sample alone, but is influenced by the tip material, the applied electric field, and image potential effects. [@problem_id:2519889]

The presence of adsorbates on the surface can modify this simple picture. If a molecular layer of thickness $a$ and barrier height $\phi_{\mathrm{ad}}$ is present, the tunneling barrier becomes a composite of the adsorbate and the vacuum gap. The WKB approximation can be extended to this case, with the total decay being the sum of decays through each segment. If the adsorbate possesses a molecular orbital that lies within the energy window of the applied bias, **[resonant tunneling](@entry_id:146897)** can occur, significantly increasing the transmission probability and weakening the effective distance decay of the current. [@problem_id:2519889]

While the WKB model provides a good qualitative understanding, a more rigorous interpretation of STM images requires a more sophisticated theoretical framework. The most general approach is **Bardeen’s tunneling formalism**, derived from [first-order perturbation theory](@entry_id:153242). It expresses the tunneling matrix element $M_{\mu\nu}$ between a tip state $\psi_\nu$ and a sample state $\psi_\mu$ as a [surface integral](@entry_id:275394) of their wavefunctions and gradients in the vacuum gap. This formalism is powerful as it makes no assumptions about the orbital character of the tip or sample wavefunctions. [@problem_id:2519950]

However, Bardeen's formalism is computationally demanding. The **Tersoff–Hamann approximation** provides a more intuitive and widely used interpretation by introducing several key simplifications. It models the tip as a locally spherical potential, with the apex atom having a spherically symmetric **$s$-wave orbital** wavefunction. In the limit of low temperature and small bias voltage ($|eV| \to 0$), and assuming an energy-independent tip density of states, this model yields a remarkably simple and powerful result: the differential conductance is directly proportional to the sample's **[local density of states](@entry_id:136852) (LDOS)** at the position of the tip apex $\mathbf{r}_0$ and at the Fermi energy $E_F$.

$\frac{\mathrm{d}I}{\mathrm{d}V} \propto \rho_{s}(\mathbf{r}_{0}, E_{F})$

This approximation transforms STM from a simple topographic tool into a powerful spectroscopic probe of [surface electronic structure](@entry_id:201446). A constant-current topographic image, in this limit, corresponds to a contour map of constant Fermi-level LDOS. For finite bias, the image represents a contour of the LDOS integrated over the energy window from $E_F$ to $E_F + eV$. It is the simplification of the tip to an $s$-wave probe that enables this direct link between the tunneling current and the sample's LDOS. [@problem_id:2519950]

### The Physics of Atomic Force Microscopy (AFM)

#### The Cantilever as a Mechanical Transducer

The heart of an AFM is the [cantilever](@entry_id:273660), a micro-machined beam that acts as a spring. For a standard rectangular cantilever of length $L$, width $b$, and thickness $t$, made from a material with Young's modulus $E$ and density $\rho$, its [mechanical properties](@entry_id:201145) can be described by the Euler–Bernoulli [beam theory](@entry_id:176426). The key parameters are:

*   **Static Spring Constant ($k$)**: This relates the force $F$ applied at the free end to the resulting static deflection $\delta$. For an end-loaded rectangular beam, it is given by $k = \frac{3EI}{L^3}$, where $I = \frac{bt^3}{12}$ is the area moment of inertia. This parameter determines the [cantilever](@entry_id:273660)'s sensitivity to static forces.

*   **Effective Mass ($m_{\mathrm{eff}}$)**: For dynamic modes, the continuously distributed mass of the [cantilever](@entry_id:273660) can be treated as a single effective mass concentrated at the tip. For the fundamental flexural mode, this mass is approximately $m_{\mathrm{eff}} \approx 0.2427 \rho Lbt$.

*   **Resonance Frequency ($f_0$)**: The [cantilever](@entry_id:273660)'s natural frequency of oscillation is determined by its stiffness and effective mass, analogous to a simple harmonic oscillator: $f_0 = \frac{1}{2\pi}\sqrt{\frac{k}{m_{\mathrm{eff}}}}$. Substituting the expressions for $k$ and $m_{\mathrm{eff}}$ reveals its strong dependence on geometry and material properties.

*   **Quality Factor ($Q$)**: The $Q$-factor is a dimensionless measure of the damping in the oscillator. It is defined as $2\pi$ times the ratio of the total energy stored to the energy dissipated per oscillation cycle. For a cantilever with an effective viscous [damping coefficient](@entry_id:163719) $c$, $Q = \frac{m_{\mathrm{eff}}\omega_0}{c}$, where $\omega_0 = 2\pi f_0$. A high $Q$-factor implies low damping and a sharp resonance peak, leading to high sensitivity in dynamic AFM modes. [@problem_id:2519930]

#### The Landscape of Tip-Sample Forces

The contrast in AFM arises from the rich variety of forces that can act between the tip and sample. Understanding their relative strengths and ranges is crucial for interpreting images. Let us consider the typical forces encountered in an ambient environment, which can be quantitatively compared using standard physical models. [@problem_id:2519953]

*   **Van der Waals Force**: Arising from fluctuating induced dipoles, this is a ubiquitous attractive force. For a tip of radius $R$ at a distance $z$ from a surface, it scales as $F_{\mathrm{vdW}} \propto R/z^2$. It is a relatively short-range interaction, dominant at nanometer-scale separations. For a $20\,\mathrm{nm}$ tip at $1\,\mathrm{nm}$ separation, its magnitude is typically on the order of tenths of a nanonewton ($0.1-1\,\mathrm{nN}$).

*   **Electrostatic Force**: This force arises from contact potential differences or trapped charges. For a conductive tip and sample, it scales as $F_{\mathrm{elec}} \propto R V^2/z$, where $V$ is the potential difference. As it decays more slowly with distance ($1/z$) than the van der Waals force, it is longer-ranged. Its magnitude is highly dependent on $V$ but can be on the order of tens of piconewtons ($10-100\,\mathrm{pN}$) for typical potentials.

*   **Capillary Force**: In ambient air, a meniscus of water can condense in the tip-sample junction. The surface tension of this liquid bridge creates a strong attractive force, $F_{\mathrm{cap}} \propto R$. This force is largely independent of tip-sample separation until the meniscus ruptures. It is often the strongest force in ambient AFM, with typical magnitudes of tens of nanonewtons ($10-100\,\mathrm{nN}$). Its range is determined by the meniscus stability, typically up to tens of nanometers.

*   **Short-Range Chemical Force**: At very close separations (a few angstroms), direct orbital overlap leads to the formation of chemical bonds or strong Pauli repulsion. These forces are responsible for [atomic resolution](@entry_id:188409). They are the shortest-ranged of all interactions, decaying exponentially over a few tenths of a nanometer. However, their peak strength can be substantial, on the order of nanonewtons ($1-10\,\mathrm{nN}$).

*   **Magnetic Force**: In Magnetic Force Microscopy (MFM), a specialized AFM mode, a magnetized tip is used to probe stray magnetic fields from the sample. The force depends on the tip's magnetic moment and the sample's magnetic field gradient, typically decaying as $1/z^n$ where $n \ge 3$. It is a long-range force, but usually the weakest of the set, with magnitudes in the piconewton range ($1-100\,\mathrm{pN}$).

A comparative analysis under typical ambient conditions reveals a force magnitude hierarchy of: **capillary > chemical bonding > van der Waals > electrostatic > magnetic**. The hierarchy of interaction ranges is typically: **electrostatic > magnetic > capillary > van der Waals > chemical bonding**. This underscores why capillary forces dominate ambient AFM, often obscuring the finer details, and why achieving [atomic resolution](@entry_id:188409) requires operating in [ultra-high vacuum](@entry_id:196222) (UHV) to eliminate the meniscus and carefully controlling electrostatic effects. [@problem_id:2519953]

#### The Mechanism of Atomic Resolution

Atomic resolution in non-contact AFM (NC-AFM), particularly in UHV, is a remarkable achievement that relies on the exquisite sensitivity to short-range chemical forces. The key observable in frequency-modulation NC-AFM is the shift in the [cantilever](@entry_id:273660)'s [resonance frequency](@entry_id:267512), $\Delta f$, which is proportional to the tip-sample force *gradient* averaged over the oscillation cycle.

The total [force gradient](@entry_id:190895) is a sum of the long-range van der Waals background and the short-range chemical interaction. While the long-range component, arising from the mesoscopic tip body, provides a significant, slowly varying background gradient, it does not provide atomic contrast. Atomic resolution emerges because the **short-range [force gradient](@entry_id:190895) varies dramatically** as the tip moves laterally from being directly over a surface atom ("atop" site) to a position between atoms ("hollow" or "bridge" site). [@problem_id:2519890]

For instance, consider a tip apex atom at a distance of $0.34\,\mathrm{nm}$ from a surface atom (atop site) and $0.38\,\mathrm{nm}$ at a hollow site. Using a Lennard-Jones potential to model the interaction, the calculated short-range [force gradient](@entry_id:190895) can change by tens of Newtons per meter ($\mathrm{N\,m^{-1}}$) between these two positions. This is a huge variation, often comparable to or even larger than the entire background gradient from the long-range van der Waals force. It is this strong, site-specific modulation of the short-range [force gradient](@entry_id:190895), which decays exponentially, that the FM-AFM system detects as a variation in frequency shift, thereby producing an image of the individual atoms on the surface. This mechanism is effective for both covalent and ionic surfaces, as [short-range interactions](@entry_id:145678) are universally present. [@problem_id:2519890]

### Dynamic Modes of AFM: Signal Interpretation

Dynamic AFM modes, where the cantilever is oscillated, offer significant advantages over static contact mode, including reduced lateral forces and the ability to probe dissipative interactions. The two primary dynamic modes are Amplitude Modulation (AM-AFM) and Frequency Modulation (FM-AFM).

#### Amplitude Modulation (AM-AFM)

In AM-AFM, commonly known as "[tapping mode](@entry_id:263659)," the [cantilever](@entry_id:273660) is driven by a sinusoidal force at a fixed frequency $\omega$, typically slightly below its free resonance frequency $\omega_0$. The [tip-sample interaction](@entry_id:188716) modifies both the effective stiffness and damping of the system. The feedback loop maintains a constant oscillation **amplitude** ($A$) by adjusting the average tip-sample height. Two key signals are recorded: the height, which forms the topographic image, and the **phase lag** ($\phi$) between the drive signal and the [cantilever](@entry_id:273660)'s response.

From the equation of a driven, [damped harmonic oscillator](@entry_id:276848), we can derive the steady-state [energy balance](@entry_id:150831). The energy per cycle supplied by the drive, $E_{\mathrm{drive}} = \pi F_d A \sin\phi$, must equal the total energy dissipated by intrinsic [cantilever](@entry_id:273660) damping and tip-sample dissipative interactions. The energy dissipated by the [tip-sample interaction](@entry_id:188716), $E_{\mathrm{ts}}$, can thus be expressed in terms of measurable quantities:

$E_{\mathrm{ts}} = \pi F_d A \sin\phi - \pi \omega c_0 A^2$

where $F_d$ is the drive force amplitude and $c_0$ is the cantilever's intrinsic [damping coefficient](@entry_id:163719). This equation reveals a crucial insight: with the amplitude $A$ held constant by the feedback loop, any variation in the phase signal $\phi$ is a direct and quantitative measure of changes in tip-sample dissipation ($\gamma_{\mathrm{ts}}$). The height channel, which adjusts the tip-sample separation to keep $A$ constant, primarily responds to changes in the **conservative interaction** ([force gradient](@entry_id:190895) $k_{\mathrm{ts}}$), as this detunes the resonance and has the largest effect on amplitude. [@problem_id:2519971]

It is important to recognize, however, that the phase signal is not a pure measure of dissipation. The phase lag $\phi$ is mathematically dependent on both the conservative gradient ($k_{\mathrm{ts}}$) and the dissipative damping ($\gamma_{\mathrm{ts}}$), as seen in its governing equation:

$\tan \phi = \frac{\omega(c_0 + \gamma_{\mathrm{ts}})}{k + k_{\mathrm{ts}} - m\omega^2}$

Because a single measurement, $\phi$, depends on two unknowns, the phase image is inherently a convolution of conservative and dissipative effects. Without additional information or assumptions, these contributions cannot be unambiguously separated from the phase channel alone. [@problem_id:2519971]

#### Frequency Modulation (FM-AFM)

In FM-AFM, the [cantilever](@entry_id:273660) is part of a self-oscillating loop, meaning it is always driven at its instantaneous [resonance frequency](@entry_id:267512), $f$. A [phase-locked loop](@entry_id:271717) (PLL) ensures that the drive signal always maintains a constant phase relationship (typically $90^\circ$) with the [cantilever](@entry_id:273660)'s motion, thereby tracking changes in the resonance frequency. The primary observable is the **frequency shift**, $\Delta f = f - f_0$.

For a purely conservative interaction, the frequency shift can be rigorously related to the **virial of the [tip-sample interaction](@entry_id:188716)**, $V_{\mathrm{ts}}$. The virial is defined as the time-average of the dot product of the interaction force and the [position vector](@entry_id:168381) relative to the [center of oscillation](@entry_id:262246), $z_0$. For [one-dimensional motion](@entry_id:190890), this is:

$V_{\mathrm{ts}} = \frac{1}{T} \int_0^T F_{\mathrm{ts}}(z(t)) [z(t) - z_0] \mathrm{d}t$

This quantity represents the cycle-averaged work-like term for the interaction. For sinusoidal motion $z(t) = z_0 + A\cos(\omega t)$ and in the limit of small frequency shifts ($|\Delta f| \ll f_0$), the frequency shift is exactly related to the virial by:

$\Delta f = -\frac{f_0}{k A^2} V_{\mathrm{ts}}$

This fundamental relationship, derived from energy conservation or [harmonic balance](@entry_id:166315), connects the measured frequency shift to a well-defined integral property of the [tip-sample interaction](@entry_id:188716) force over the oscillation cycle. It provides a powerful pathway for [quantitative analysis](@entry_id:149547), allowing for the reconstruction of the interaction force and potential from measurements of $\Delta f$ as a function of distance. [@problem_id:2519978] In the small-amplitude limit, this relation simplifies to the well-known approximation $\Delta f \approx \frac{f_0}{2k} \frac{\mathrm{d}F_{\mathrm{ts}}}{\mathrm{d}z}$.

### Instrumentation and Control

The physical principles of SPM are realized through sophisticated instrumentation, centrally involving piezoelectric scanners for positioning and feedback controllers for regulation.

#### Piezoelectric Scanners

Precise, sub-nanometer positioning in most SPMs is achieved using scanners made of [piezoelectric materials](@entry_id:197563), such as lead zirconate titanate (PZT). A common design is the **piezoelectric tube scanner**. This is a hollow cylinder of PZT with a continuous inner electrode and a segmented outer electrode, typically divided into four quadrants ($+X, -X, +Y, -Y$).

The tube is poled radially, and the material is characterized by a transverse piezoelectric coefficient $d_{31}$, which relates an electric field applied in the radial direction (direction '3') to the strain induced in the axial direction (direction '1'). By applying voltages to the electrodes, controlled motion is produced:

*   **Z-Motion (Extension/Retraction)**: Applying a uniform voltage $V_z$ to all four outer quadrants relative to the grounded inner electrode creates a uniform [axial strain](@entry_id:160811), causing the tube to extend or contract. The change in length $\Delta L$ scales as $\Delta L \propto d_{31} L V_z / t$, where $L$ is the tube length and $t$ is its wall thickness.

*   **X/Y-Motion (Bending)**: To bend the scanner, a differential voltage is applied. For example, applying $+V_x$ to the $+X$ quadrant and $-V_x$ to the $-X$ quadrant causes one side of the tube to extend and the opposite side to contract. This differential strain induces a curvature $\kappa$, causing the free end of the tube to deflect laterally. The resulting tip displacement scales as $x \propto d_{31} (L^2/R) V_x / t$, where $R$ is the tube radius. This quadratic dependence on length makes longer scanners more sensitive for lateral scanning but also mechanically less stable. [@problem_id:2519916]

A critical aspect of [piezoelectric actuators](@entry_id:169515) is their non-ideal behavior, especially in open-loop operation (without position feedback). The three main sources of error are:

*   **Hysteresis**: The relationship between applied voltage and displacement is path-dependent. The displacement for a given voltage is different depending on whether the voltage is increasing or decreasing, forming a characteristic loop. This is an [intrinsic property](@entry_id:273674) of the ferroelectric material, arising from domain wall motion.
*   **Creep**: When a step change in voltage is applied, the actuator does not reach its final position instantaneously. Instead, it continues to drift slowly, typically with a [logarithmic time](@entry_id:636778) dependence, towards a new [equilibrium position](@entry_id:272392).
*   **Nonlinearity**: Even under quasi-static conditions, the displacement is not strictly proportional to the applied voltage. The response can be described by a single-valued but nonlinear curve.

These intrinsic material behaviors mean that in open-loop operation, the scanner's position is not a unique or stable function of the applied voltage, leading to significant [image distortion](@entry_id:171444). This necessitates the use of closed-loop scanners with independent position sensors or, more commonly, robust [feedback control](@entry_id:272052) of the [tip-sample interaction](@entry_id:188716) itself. [@problem_id:2519916]

#### Feedback Control

The feedback loop is the brain of the SPM, responsible for maintaining a constant [tip-sample interaction](@entry_id:188716) and tracking the surface topography. The most common type of controller is the **Proportional-Integral-Derivative (PID)** controller. It calculates an output (the Z-piezo voltage) based on the [error signal](@entry_id:271594) (e.g., the difference between the measured tunneling current and its setpoint).

The transfer function from the true sample height to the recorded piezo height can be shown to be the **[complementary sensitivity function](@entry_id:266294)** $T(s) = L(s)/(1+L(s))$, where $L(s)$ is the [open-loop transfer function](@entry_id:276280) of the entire system (controller and plant). For faithful tracking, we require $T(s) \approx 1$, which is achieved when the loop gain $|L(s)| \gg 1$. The frequency at which the gain drops to unity, the crossover frequency $\omega_c$, defines the **bandwidth** of the feedback loop. To accurately trace a feature of lateral width $w$ scanned at speed $v$, the loop bandwidth must be high enough to respond on the timescale of the feature traversal, $\Delta t \approx w/v$. For example, scanning a $10\,\mathrm{nm}$ feature at $10\,\mu\mathrm{m/s}$ requires a response time of $\approx 1\,\mathrm{ms}$, corresponding to a required bandwidth of $\gtrsim 1\,\mathrm{kHz}$. [@problem_id:2519929]

Each term of the PID controller plays a distinct role:

*   **Proportional (P) Gain**: This provides a corrective action proportional to the current error. Increasing P-gain generally increases the loop bandwidth, allowing for faster scanning. However, excessively high P-gain reduces the system's **phase margin** (a measure of stability), leading to overshoot and oscillations ("ringing") at sharp surface features.

*   **Integral (I) Gain**: This term integrates the error over time. Its primary role is to provide infinite gain at zero frequency (DC), which **eliminates steady-state error**. This ensures that the average [tip-sample interaction](@entry_id:188716) is precisely maintained at the [setpoint](@entry_id:154422), even on tilted or slowly varying surfaces. However, the integrator introduces a $-90^\circ$ phase lag, which reduces the [phase margin](@entry_id:264609) and can destabilize the loop, causing oscillations if the gain is too high.

*   **Derivative (D) Gain**: This term acts on the rate of change of the error. It provides a [phase lead](@entry_id:269084), which can counteract the [phase lag](@entry_id:172443) from the plant and the integrator. This **increases the [phase margin](@entry_id:264609)**, improving stability and damping oscillations. It allows for higher P and I gains to be used, enabling faster and more accurate tracking. The main drawback is that the D-term amplifies high-frequency sensor noise, which can roughen the final image.

Optimizing a PID loop is a crucial experimental skill, involving a trade-off between tracking speed (high bandwidth) and stability (sufficient [phase margin](@entry_id:264609), typically $\gtrsim 45^\circ-60^\circ$ to limit ringing). [@problem_id:2519929]