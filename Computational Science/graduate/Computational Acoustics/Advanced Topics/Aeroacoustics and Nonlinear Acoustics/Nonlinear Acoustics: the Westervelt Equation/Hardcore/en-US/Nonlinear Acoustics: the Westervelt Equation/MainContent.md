## Introduction
Classical [linear acoustics](@entry_id:1127264), while powerful, fails to describe the behavior of high-intensity sound waves, where phenomena such as waveform distortion, harmonic generation, and shock formation become prominent. The Westervelt equation emerges as a cornerstone of [nonlinear acoustics](@entry_id:200235), providing a single, comprehensive partial differential equation that elegantly captures these effects. It addresses the knowledge gap left by linear theory by unifying the fundamental physics of wave propagation, thermoviscous energy loss, and [quadratic nonlinearity](@entry_id:753902) into one tractable model.

This article provides a thorough exploration of the Westervelt equation, designed to build a deep theoretical and practical understanding. In the first chapter, **Principles and Mechanisms**, we will dissect the equation's mathematical form, investigate the physical origins of its dissipation and nonlinearity terms, and understand its foundational assumptions. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the equation's real-world impact, showcasing its crucial role in medical technologies like Tissue Harmonic Imaging (THI) and computational modeling. Finally, the **Hands-On Practices** section will solidify these concepts through targeted problems, tackling practical calculations and numerical considerations essential for any practitioner in the field.

## Principles and Mechanisms

The Westervelt equation provides a powerful mathematical framework for modeling the propagation of finite-amplitude sound in thermoviscous fluids. It synthesizes three fundamental physical processes—linear wave propagation, thermoviscous dissipation, and [quadratic nonlinearity](@entry_id:753902)—into a single scalar partial differential equation for the acoustic pressure. A common form of this equation, derived under the assumption of a quasi-plane, [traveling wave](@entry_id:1133416), is given by :

$$
\nabla^2 p - \frac{1}{c_0^2} \frac{\partial^2 p}{\partial t^2} + \frac{\delta}{c_0^4} \frac{\partial^3 p}{\partial t^3} = - \frac{\beta}{\rho_0 c_0^4} \frac{\partial^2 (p^2)}{\partial t^2}
$$

Here, $p(\mathbf{x}, t)$ is the acoustic pressure, $c_0$ is the small-signal sound speed, $\rho_0$ is the ambient mass density, $\delta$ is the diffusivity of sound, and $\beta$ is the [coefficient of nonlinearity](@entry_id:1122598). Each term in this equation represents a distinct physical mechanism, and understanding their individual roles and interplay is crucial to comprehending the rich phenomena of [nonlinear acoustics](@entry_id:200235).

### Foundational Assumptions

The derivation of the Westervelt equation from the fundamental conservation laws of fluid dynamics (mass, momentum, and energy) relies on a specific set of simplifying assumptions. These approximations restrict the model's validity to a well-defined physical regime, but are essential for reducing the complexity of the full fluid dynamics equations to a single, more tractable scalar equation .

The primary assumptions are:

1.  **Irrotational Flow**: The acoustic velocity field is assumed to be curl-free ($\nabla \times \mathbf{u} = 0$). This is a valid approximation for sound generated in the bulk of a fluid, away from boundaries where vorticity can be generated. This allows the velocity field to be described by a [scalar potential](@entry_id:276177), greatly simplifying the mathematics.

2.  **Weak Nonlinearity**: The acoustic perturbations are assumed to be small but finite. Formally, the acoustic Mach number, $\varepsilon = U/c_0$ (where $U$ is a characteristic particle velocity), is assumed to be much less than unity ($\varepsilon \ll 1$). The derivation systematically retains terms up to the second order in perturbation amplitude, $\mathcal{O}(\varepsilon^2)$, while discarding higher-order terms. This captures the leading-order nonlinear effects without embracing the full complexity of strong shock dynamics.

3.  **Thermoviscous Dissipation**: Energy loss from the acoustic wave is assumed to arise from classical Stokes-Kirchhoff mechanisms: shear viscosity, [bulk viscosity](@entry_id:187773), and thermal conduction. These effects are modeled as being linearly proportional to the acoustic field variables.

4.  **Quiescent and Homogeneous Medium**: The background medium is assumed to be at rest (no mean flow) and to have uniform properties ($\rho_0$ and $c_0$ are constants). As we will see later, this assumption can be relaxed to study propagation in inhomogeneous media .

Under these conditions, the complex system of vector and scalar equations governing the fluid can be collapsed into the single Westervelt equation for the acoustic pressure $p$.

### The Physics of Dissipation: The Diffusivity of Sound

The term that encapsulates the effects of thermoviscous dissipation is $+\frac{\delta}{c_0^4}\frac{\partial^3 p}{\partial t^3}$. The parameter $\delta$, known as the **diffusivity of sound**, is a composite coefficient that combines all relevant material properties responsible for linear acoustic absorption . Its definition is:

$$
\delta = \frac{1}{\rho_0} \left( \frac{4}{3}\mu + \mu_b \right) + \frac{\kappa(\gamma-1)}{\rho_0 C_p}
$$

where $\mu$ is the [shear viscosity](@entry_id:141046), $\mu_b$ is the [bulk viscosity](@entry_id:187773), $\kappa$ is the thermal conductivity, $\gamma$ is the ratio of specific heats, and $C_p$ is the specific heat at constant pressure. This parameter has dimensions of $\mathrm{length}^2/\mathrm{time}$, characteristic of a [diffusion process](@entry_id:268015).

Each component of $\delta$ corresponds to a distinct physical mechanism of energy loss:

*   **Shear Viscosity Contribution ($\frac{4}{3}\mu/\rho_0$)**: Even in a purely longitudinal (compressional) [plane wave](@entry_id:263752), the process of expansion and contraction induces velocity gradients that engage the fluid's resistance to shear. This term quantifies the dissipation arising from the deviatoric part of the [viscous stress](@entry_id:261328) tensor, converting coherent acoustic energy into heat.

*   **Bulk Viscosity Contribution ($\mu_b/\rho_0$)**: Bulk viscosity accounts for dissipative losses during pure volumetric changes. A primary physical origin, especially in polyatomic gases, is **molecular relaxation**. When an acoustic wave compresses a gas, the [translational kinetic energy](@entry_id:174977) of molecules increases almost instantly. However, the transfer of this energy to internal rotational and vibrational modes takes a finite amount of time. This lag between translational and internal energy states is an [irreversible process](@entry_id:144335) that dissipates acoustic energy. At ultrasonic frequencies that are comparable to the inverse of these relaxation times, the effective bulk viscosity can become very large and often dominate all other sources of absorption .

*   **Thermal Conduction Contribution ($\frac{\kappa(\gamma-1)}{\rho_0 C_p}$)**: Acoustic waves create regions of local compression and rarefaction, which, under adiabatic conditions, correspond to regions of slightly higher and lower temperature, respectively. Heat naturally flows from the hot compressed regions to the cold rarefied regions. This flow, driven by the thermal conductivity $\kappa$, is an irreversible, entropy-generating process that drains energy from the wave. Contrary to intuition, a higher thermal conductivity leads to *more* attenuation, not less, because it facilitates this dissipative heat transfer .

For a single-frequency wave of [angular frequency](@entry_id:274516) $\omega$, the dissipative term results in an exponential amplitude decay with a characteristic attenuation coefficient $\alpha$ that scales with the square of the frequency: $\alpha(\omega) \propto \delta \omega^2$. This means the [dissipative operator](@entry_id:262598) acts as a low-pass filter, preferentially damping high-frequency components of the wave. Spatially, this corresponds to the smoothing of sharp gradients in the pressure waveform .

### The Physics of Nonlinearity: Waveform Steepening and Harmonic Generation

The right-hand side of the Westervelt equation, $-\frac{\beta}{\rho_0 c_0^4} \frac{\partial^2 (p^2)}{\partial t^2}$, is the source of all quadratic nonlinear phenomena. Its strength is governed by the dimensionless **[coefficient of nonlinearity](@entry_id:1122598)**, $\beta$, defined as :

$$
\beta = 1 + \frac{B}{2A}
$$

The parameter $B/A$ is the classical parameter of nonlinearity, derived from the second-order term in the Taylor expansion of the fluid's equation of state, $p(\rho)$. The term $\frac{B}{2A}$ thus represents **[material nonlinearity](@entry_id:162855)**. The '1' in the expression for $\beta$ arises from **convective nonlinearity**, which includes terms like $(\mathbf{u} \cdot \nabla)\mathbf{u}$ in the momentum equation that are quadratic in the acoustic field variables. Therefore, $\beta$ elegantly combines nonlinear effects from both the fluid's constitutive law and its convective dynamics.

The physical consequence of this term is that the local speed of sound becomes dependent on the instantaneous [acoustic pressure](@entry_id:1120704) :

$$
c(p) \approx c_0 + \frac{\beta p}{\rho_0 c_0}
$$

For most common fluids, $\beta > 0$, meaning that regions of compression ($p>0$) travel faster than the small-signal speed $c_0$, while regions of [rarefaction](@entry_id:201884) ($p0$) travel slower. For an initially sinusoidal wave, this causes the wave crests to progressively catch up to the troughs ahead of them. The front of the waveform becomes steeper, while the back becomes less steep. This process, known as **waveform steepening**, distorts the wave from its original shape.

In the frequency domain, this time-domain distortion manifests as the generation of new frequency components, specifically **harmonics** of the original source frequency $\omega$. The quadratic term $p^2$ is the engine of this process. For a fundamental wave at frequency $\omega$, the term $p^2$ directly generates a static (DC) pressure component and, most importantly, the second harmonic at frequency $2\omega$. Odd harmonics are not generated directly. Instead, they arise from a cascade effect: the newly generated second harmonic at $2\omega$ interacts with the fundamental at $\omega$ through the same [quadratic nonlinearity](@entry_id:753902), producing sum and difference frequencies, including the third harmonic at $3\omega$. This explains why, for a single-frequency source, the second harmonic amplitude initially grows linearly with propagation distance $x$, while the third harmonic amplitude grows as $x^2$ .

### The Central Dynamic: The Competition Between Steepening and Smoothing

The Westervelt equation fundamentally describes a competition: the nonlinear term continuously generates higher harmonics, steepening the waveform toward a shock, while the dissipative term continuously removes energy from these same high frequencies, smoothing the waveform . The ultimate fate of a high-intensity wave depends on which of these two effects is dominant.

This competition can be quantified by comparing two [characteristic length scales](@entry_id:266383):

1.  The **[shock formation distance](@entry_id:1131576)**, $L_s$: The distance over which an initially sinusoidal wave would steepen into a mathematical shock (a vertical [wavefront](@entry_id:197956)) in a lossless $(\delta=0)$ medium. It is given by $L_s = \frac{\rho_0 c_0^3}{\beta \omega_0 p_0}$, where $p_0$ and $\omega_0$ are the source pressure amplitude and frequency.

2.  The **attenuation length**, $L_a$: The distance over which the wave's amplitude is significantly reduced by dissipation. It is defined as the reciprocal of the attenuation coefficient at the [fundamental frequency](@entry_id:268182), $L_a = 1/\alpha(\omega_0) = \frac{2c_0^3}{\delta \omega_0^2}$.

The ratio of these two lengths defines the **Gol'dberg number**, $\Gamma = L_a / L_s$. This dimensionless number is the single most important parameter determining the character of nonlinear propagation :

*   If $\Gamma \gg 1$, then $L_s \ll L_a$. Nonlinear effects dominate. The wave has ample distance to steepen into a shock-like structure before it is significantly attenuated. This is the domain of strong nonlinear distortion and shock formation.

*   If $\Gamma \ll 1$, then $L_s \gg L_a$. Dissipative effects dominate. The wave's amplitude is damped out long before significant [nonlinear steepening](@entry_id:183454) can occur. In this regime, the nonlinear term in the Westervelt equation can be neglected, and the propagation is well-described by the simpler **linear [thermoviscous wave equation](@entry_id:1133089)**.

### Connections to Other Acoustic Models

The Westervelt equation occupies a central place in a hierarchy of acoustic models, and its relationship to simpler or alternative models can be understood by examining its limiting cases.

*   **The Classical Linear Wave Equation**: If we consider the hypothetical limit where both nonlinearity and dissipation are absent ($\beta \to 0$ and $\delta \to 0$), the Westervelt equation simplifies dramatically to :
    $$
    \nabla^2 p - \frac{1}{c_0^2} \frac{\partial^2 p}{\partial t^2} = 0
    $$
    This is the familiar d'Alembertian or classical [linear wave equation](@entry_id:174203), describing the propagation of infinitesimal disturbances in an ideal, lossless fluid.

*   **The Linear Thermoviscous Wave Equation**: As noted above, in the regime where dissipation dominates nonlinearity ($\Gamma \ll 1$), we can set $\beta \to 0$ but retain $\delta$. This yields the linear [thermoviscous wave equation](@entry_id:1133089) (or Stokes wave equation) , which models linear propagation with classical $\omega^2$ attenuation.

*   **The Burgers Equation**: The Westervelt equation is a "two-way" equation, admitting solutions that travel in any direction. For many applications involving a directed beam, it is computationally advantageous to use a "one-way" model that describes propagation primarily along a single axis. By introducing a retarded time coordinate $\tau = t - x/c_0$ (for propagation along $x$) and making a [parabolic approximation](@entry_id:140737), the Westervelt equation can be reduced. If we further assume the wave is a [plane wave](@entry_id:263752), thereby **neglecting diffraction**, the result is the one-dimensional Burgers equation for acoustics :
    $$ \frac{\partial p}{\partial x} - \frac{\beta}{\rho_0 c_0^3} p \frac{\partial p}{\partial \tau} - \frac{\delta}{2c_0^3} \frac{\partial^2 p}{\partial \tau^2} = 0 $$
    This famous equation isolates the one-dimensional competition between [quadratic nonlinearity](@entry_id:753902) (the $p \frac{\partial p}{\partial \tau}$ term) and thermoviscous diffusion (the $\frac{\partial^2 p}{\partial \tau^2}$ term).

### Extensions and Limitations

While powerful, the standard Westervelt equation has limitations stemming from its underlying assumptions. Important extensions have been developed to address these.

#### Frequency-Dependent Dissipation and Relaxation

The constant-$\delta$ model is predicated on the classical Stokes-Kirchhoff theory, which yields an [attenuation coefficient](@entry_id:920164) $\alpha \propto \omega^2$. However, in many real media, particularly polyatomic gases like air, molecular relaxation processes introduce additional loss mechanisms that are strongly frequency-dependent. Near a characteristic relaxation frequency, the absorption can deviate significantly from the $\omega^2$ law. Causality, via the Kramers-Kronig relations, dictates that this frequency-dependent absorption must be accompanied by a frequency-dependent phase speed, a phenomenon known as **dispersion**.

A constant-$\delta$ model cannot capture these effects. A more accurate model for such media requires promoting the diffusivity to a complex, frequency-dependent function, $\delta(\omega)$. In the time domain, this corresponds to replacing the simple third-order time derivative with a causal [convolution integral](@entry_id:155865) involving a [memory kernel](@entry_id:155089). This acknowledges that the medium's response at a given time depends on the history of the acoustic field, a direct consequence of the finite time scales of the relaxation processes .

#### Propagation in Inhomogeneous Media

The standard Westervelt equation assumes a homogeneous medium. For applications in biomedical ultrasound or [ocean acoustics](@entry_id:1129046), it is crucial to account for spatial variations in the background sound speed $c(\mathbf{x})$ and density $\rho(\mathbf{x})$. A generalized Westervelt equation can be derived for such media. While various forms exist depending on the approximations made, a rigorous formulation starting from the linear conservation laws for an inhomogeneous fluid modifies the spatial operator :

$$
\rho(\mathbf{x}) \nabla \cdot \left( \frac{1}{\rho(\mathbf{x})} \nabla p \right) - \frac{1}{c^2(\mathbf{x})} \frac{\partial^2 p}{\partial t^2} - \dots = \dots
$$

The presence of spatially varying coefficients has profound consequences for wave propagation:

*   **Refraction and Focusing**: The spatial variation of sound speed, $c(\mathbf{x})$, acts like a refractive index profile for light. In the high-frequency limit of [geometric acoustics](@entry_id:1125600), ray trajectories bend toward regions of lower sound speed. This allows for the natural focusing or defocusing of sound by the medium itself. For instance, a medium where the sound speed is lower along a central axis than in the periphery will act as a focusing lens for an acoustic beam.

*   **Amplitude Modulation and Diffraction**: The variation of density, $\rho(\mathbf{x})$, primarily affects the wave amplitude through changes in [acoustic impedance](@entry_id:267232), $Z(\mathbf{x}) = \rho(\mathbf{x})c(\mathbf{x})$, leading to scattering and reflection. In the [geometric acoustics](@entry_id:1125600) limit, $\rho(\mathbf{x})$ does not determine the ray paths, which are governed by $c(\mathbf{x})$. Both parameters, however, influence the strength of diffraction. These generalized models are essential for accurately simulating acoustic fields in complex environments like biological tissue.