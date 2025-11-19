## Introduction
Superconductivity represents a profound state of matter where quantum mechanics manifests on a macroscopic scale, leading to remarkable properties like [zero electrical resistance](@entry_id:151583) and the expulsion of magnetic fields. While the microscopic Bardeen-Cooper-Schrieffer (BCS) theory provides a fundamental explanation based on the pairing of electrons, a vast range of behaviors can be described with incredible accuracy using phenomenological frameworks. This article bridges the gap between abstract quantum theory and observable phenomena, providing a graduate-level guide to the phenomenology of superconductivity. By focusing on these powerful descriptive models, we can understand and engineer the properties of superconductors without delving into the full complexity of the many-body problem.

The reader will embark on a structured journey through the core concepts. The "Principles and Mechanisms" chapter lays the groundwork, starting with the defining Meissner effect and progressing to the elegant London [electrodynamics](@entry_id:158759) and the unifying Ginzburg-Landau theory, which introduces the critical concepts of [coherence length](@entry_id:140689), penetration depth, and vortex physics. Building upon this foundation, the "Applications and Interdisciplinary Connections" chapter demonstrates the practical utility of these principles, exploring their role in advanced experimental probes, cutting-edge electronic devices, and the ongoing quest to understand [unconventional superconductors](@entry_id:141195). Finally, the "Hands-On Practices" section provides an opportunity to apply this knowledge through targeted problems, cementing the connection between theoretical formalism and practical analysis.

## Principles and Mechanisms

The superconducting state is a distinct phase of matter characterized by remarkable [macroscopic quantum phenomena](@entry_id:144018). While a microscopic understanding requires the quantum theory of [many-body systems](@entry_id:144006), the defining properties and behaviors of superconductors can be described with extraordinary success using a set of phenomenological theories. This chapter elucidates the core principles and mechanisms of superconductivity, progressing from its foundational electrodynamic and thermodynamic properties to the elegant Ginzburg-Landau framework that unifies them.

### Perfect Diamagnetism: The Meissner-Ochsenfeld Effect

The transition into the superconducting state at a critical temperature, $T_c$, is marked by two independent, cardinal properties. The first is the complete disappearance of [electrical resistance](@entry_id:138948). While profound, this property of "perfect conductivity" is, by itself, insufficient to define superconductivity. An idealized "[perfect conductor](@entry_id:273420)"—a hypothetical material with infinite conductivity ($\sigma \to \infty$) but otherwise normal electronic properties—would behave differently from a true superconductor. The crucial distinguishing feature is the second property: active expulsion of magnetic fields, a phenomenon known as the **Meissner-Ochsenfeld effect**.

A perfect conductor is governed by Ohm's law, $\mathbf{J} = \sigma \mathbf{E}$, and Faraday's law of induction, $\nabla \times \mathbf{E} = -\partial \mathbf{B}/\partial t$. For a finite current density $\mathbf{J}$, the infinite conductivity implies that the electric field $\mathbf{E}$ inside the material must be zero. Consequently, Faraday's law dictates that $\partial \mathbf{B}/\partial t = 0$. This means the magnetic induction $\mathbf{B}$ inside a perfect conductor can never change. It is "frozen" in time.

Consider a thought experiment comparing a [perfect conductor](@entry_id:273420) and a superconductor using a **field-cooling (FC)** protocol. [@problem_id:3009512] In this procedure, the material is first placed in a static, uniform magnetic field $\mathbf{H}_0$ at a temperature $T > T_c$. The field penetrates the sample. The sample is then cooled to a final temperature $T  T_c$.
- For the **perfect conductor**, as it cools and its conductivity becomes infinite, the external conditions are static. Since $\partial \mathbf{B}/\partial t = 0$ is trivially satisfied, no currents are induced. The magnetic flux that was present in the normal state remains trapped within the material. The final state is characterized by a non-zero bulk magnetic induction, $B_{\text{bulk}} \approx \mu_0 H_0$, and negligible magnetization, $M_{\text{bulk}} \approx 0$.
- For the **superconductor**, the situation is entirely different. Upon cooling through $T_c$, the material undergoes a thermodynamic phase transition into the Meissner state. This new equilibrium state is one of [perfect diamagnetism](@entry_id:203008). Spontaneous, persistent screening currents appear on the surface of the material, generating a magnetic field that precisely cancels the external field in the superconductor's interior. The result is that the magnetic induction is actively expelled from the bulk, leading to $B_{\text{bulk}} \approx 0$.

This expulsion demonstrates that the Meissner state is a true thermodynamic ground state, not merely a path-dependent consequence of perfect conductivity. The state of [perfect diamagnetism](@entry_id:203008) is achieved regardless of whether the field is applied after cooling (**zero-field-cooling**, ZFC) or before cooling (FC). From the [constitutive relation](@entry_id:268485) $\mathbf{B} = \mu_0(\mathbf{H} + \mathbf{M})$, if the internal field $B_{\text{bulk}} \approx 0$ and demagnetizing effects are negligible ($H_{\text{in}} \approx H_0$), the superconductor must develop a large, uniform diamagnetic magnetization $M_{\text{bulk}} \approx -H_0$. Measurement of this substantial negative magnetization upon field-cooling is the definitive experimental signature that distinguishes a superconductor from a simple [perfect conductor](@entry_id:273420). [@problem_id:3009512]

### The London Electrodynamics

The first successful phenomenological theory to account for the Meissner effect was developed by Fritz and Heinz London. It describes the electrodynamic response of the superconducting charge carriers, or **superfluid**. The theory is encapsulated in two equations that replace Ohm's law for the supercurrent density $\mathbf{J}_s$. Assuming the superfluid consists of charge carriers with charge $q$, mass $m$, and number density $n_s$, the **London equations** are:

1.  **Acceleration Equation**: $\dfrac{\partial \mathbf{J}_s}{\partial t} = \dfrac{n_s q^2}{m} \mathbf{E}$
2.  **Field Equation**: $\nabla \times \mathbf{J}_s = -\dfrac{n_s q^2}{m} \mathbf{B}$

The first equation describes perfect conductivity: any electric field accelerates the superfluid without dissipation. The second equation is the key to the Meissner effect. By combining it with the static form of Ampère's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$, we can derive an equation for the magnetic field itself. Taking the curl of Ampère's law and substituting the second London equation yields:
$$ \nabla \times (\nabla \times \mathbf{B}) = -\nabla^2 \mathbf{B} = \mu_0 (\nabla \times \mathbf{J}_s) = -\mu_0 \frac{n_s q^2}{m} \mathbf{B} $$
This gives the fundamental equation for [magnetostatics](@entry_id:140120) in a superconductor:
$$ \nabla^2 \mathbf{B} = \frac{\mu_0 n_s q^2}{m} \mathbf{B} \equiv \frac{1}{\lambda_L^2} \mathbf{B} $$
Here, we have defined the **London [penetration depth](@entry_id:136478)**, $\lambda_L$:
$$ \lambda_L = \sqrt{\frac{m}{\mu_0 n_s q^2}} $$
This parameter represents the [characteristic length](@entry_id:265857) scale for magnetic field variations inside a superconductor.

For a simple geometry, such as a semi-infinite superconductor occupying the space $x>0$ with an external field $B_0 \hat{\mathbf{z}}$ at the boundary, this differential equation has a decaying solution. [@problem_id:3009520] The magnetic field inside the superconductor is given by:
$$ B(x) = B_0 \exp(-x/\lambda_L) $$
This result quantitatively describes the Meissner effect: the magnetic field is expelled from the bulk, penetrating only a thin surface layer of thickness $\lambda_L$.

The London equations can be understood more deeply as a manifestation of macroscopic quantum mechanics. [@problem_id:3009598] The supercurrent can be expressed in a gauge-invariant form using the phase $\theta$ of the macroscopic condensate wavefunction, $\Psi = \sqrt{n_s} e^{i\theta}$:
$$ \mathbf{J}_s = \frac{n_s q}{m} (\hbar \nabla \theta - q\mathbf{A}) $$
where $\mathbf{A}$ is the [magnetic vector potential](@entry_id:141246). This expression highlights that the supercurrent is driven by gradients in the phase of the order parameter and by the [vector potential](@entry_id:153642). Taking the curl of this equation immediately yields the second London equation, as $\nabla \times (\nabla \theta) = 0$. Taking the time derivative and using the Josephson relation for the phase evolution, $\hbar \partial_t \theta = -q\phi - \mu$ (where $\phi$ is the [scalar potential](@entry_id:276177) and $\mu$ is the chemical potential), yields the first London equation. The local relation $\mathbf{J}_s = -(n_s q^2/m) \mathbf{A}$, from which the Meissner effect is often derived, is therefore not a fundamental law but holds only in a specific gauge choice known as the London gauge, where $\nabla\theta=0$ and $\nabla\cdot\mathbf{A}=0$. [@problem_id:3009520]

### Flux Quantization

The description of the supercurrent in terms of the condensate phase leads to another profound quantum effect: the quantization of magnetic flux. Consider a superconducting ring or any multiply-connected geometry. Deep inside the material, far from any surfaces, the screening currents must vanish, so $\mathbf{J}_s = 0$. From the gauge-invariant expression for the current, this implies:
$$ \hbar \nabla \theta = q\mathbf{A} $$
Now, let us integrate this expression along a closed path $C$ that lies entirely within the bulk of the superconducting ring.
$$ \oint_C \hbar \nabla \theta \cdot d\mathbf{l} = \oint_C q\mathbf{A} \cdot d\mathbf{l} $$
The order parameter $\Psi$ must be single-valued. This means that upon traversing a closed loop, its phase can only change by an integer multiple of $2\pi$. Thus, the integral on the left-hand side is:
$$ \oint_C \nabla \theta \cdot d\mathbf{l} = 2\pi n, \quad \text{where } n \in \mathbb{Z} $$
The integral on the right-hand side is, by Stokes' theorem, equal to $q$ times the magnetic flux $\Phi_B$ passing through the area enclosed by the path $C$:
$$ \oint_C q\mathbf{A} \cdot d\mathbf{l} = q \Phi_B $$
Combining these results gives the condition for [flux quantization](@entry_id:144492):
$$ \hbar(2\pi n) = q\Phi_B \quad \implies \quad \Phi_B = n \frac{2\pi\hbar}{q} = n \frac{h}{q} $$
Experiments have resoundingly confirmed this prediction. Crucially, they found that the charge $q$ is not the elementary charge $e$, but twice its value. The charge carriers are pairs of electrons—**Cooper pairs**—with charge $q=2e$. This leads to the fundamental value of the **[magnetic flux quantum](@entry_id:136429)**, $\Phi_0$:
$$ \Phi_0 = \frac{h}{2e} \approx 2.067 \times 10^{-15} \, \text{Wb} $$
The experimental verification of [flux quantization](@entry_id:144492) with charge $2e$ was a landmark triumph for the microscopic BCS theory of superconductivity, which had predicted the formation of Cooper pairs. [@problem_id:1031]

### Ginzburg-Landau Theory

The London theory is powerful but limited; it assumes the density of superconducting carriers, $n_s$, is constant. Near the critical temperature $T_c$, or in the presence of strong magnetic fields or spatial inhomogeneities, this assumption breaks down. The **Ginzburg-Landau (GL) theory** provides a more general and powerful phenomenological framework.

The GL theory is built upon a complex **order parameter**, $\Psi(\mathbf{r})$, which can be thought of as a macroscopic "wavefunction" for the superconducting condensate. Its local magnitude is related to the [superfluid density](@entry_id:142018), $n_s(\mathbf{r}) \propto |\Psi(\mathbf{r})|^2$. The theory postulates that near $T_c$, the free energy density of the system can be expanded as a [power series](@entry_id:146836) in the order parameter. For a uniform superconductor in zero field, the free energy density difference between the superconducting ($s$) and normal ($n$) states is:
$$ \Delta f = f_s - f_n = a(T) |\Psi|^2 + \frac{b}{2} |\Psi|^4 $$
The coefficients $a(T)$ and $b$ are phenomenological parameters. To ensure a stable superconducting state, $b$ must be positive. The parameter $a(T)$ is assumed to change sign at the critical temperature, with the [linear approximation](@entry_id:146101) $a(T) = a_0(T-T_c)$ where $a_0  0$.

The equilibrium state is found by minimizing this free energy.
-   For $T  T_c$, $a(T)  0$. The free energy is minimized when $|\Psi|=0$. The system is in the normal state.
-   For $T  T_c$, $a(T)  0$. The minimum of the free energy occurs at a non-zero value of the order parameter. Differentiating with respect to $|\Psi|^2$ and setting the result to zero gives the equilibrium amplitude: [@problem_id:3009562]
    $$ |\Psi_0|^2 = -\frac{a(T)}{b} = \frac{a_0(T_c - T)}{b} $$
Substituting this back into the free energy expression gives the **condensation energy density**, which is the energy gained by transitioning to the superconducting state:
$$ \Delta f_{\text{eq}} = -\frac{a(T)^2}{2b} = -\frac{a_0^2(T-T_c)^2}{2b} $$
This quadratic dependence on $(T-T_c)$ is characteristic of a [second-order phase transition](@entry_id:136930), consistent with experimental observations in zero field.

#### The Two Fundamental Length Scales

To describe the response to magnetic fields and spatial variations, the GL [free energy functional](@entry_id:184428) must be extended to include gradient and magnetic terms:
$$ \mathcal{F}[\Psi, \mathbf{A}] = \int d^3r \left[ a|\Psi|^2 + \frac{b}{2}|\Psi|^4 + \frac{1}{2m^*}|(-i\hbar\nabla - q\mathbf{A})\Psi|^2 + \frac{|\mathbf{B}|^2}{2\mu_0} \right] $$
From this functional emerge two natural length scales.

1.  The **Ginzburg-Landau [coherence length](@entry_id:140689)**, $\xi$. This is the characteristic length scale over which the order parameter $\Psi$ can vary. It represents the distance over which $\Psi$ "heals" back to its bulk value after being forced to zero, for example, at an interface with a normal metal (the [proximity effect](@entry_id:139932)). [@problem_id:1828381] It is defined as:
    $$ \xi(T) = \sqrt{\frac{\hbar^2}{2m^*|a(T)|}} \propto (T_c - T)^{-1/2} $$
    Suppressing the order parameter costs [condensation energy](@entry_id:195476), an effect governed by $\xi$.

2.  The **[magnetic penetration depth](@entry_id:140378)**, $\lambda$. This is the same length scale introduced in the London theory, now derived from the GL functional. It describes the screening of magnetic fields.
    $$ \lambda(T) = \sqrt{\frac{m^*}{ \mu_0 q^2 |\Psi_0|^2}} \propto (T_c - T)^{-1/2} $$
    Allowing a magnetic field to penetrate the superconductor reduces the magnetic exclusion energy, an effect governed by $\lambda$.

The temperature dependence of these length scales is a crucial probe of the underlying physics. In particular, measurements of $\lambda(T)$ at temperatures far below $T_c$ provide insight into the structure of the microscopic superconducting energy gap. Since $\lambda(T)^{-2} \propto n_s(T)$, the change in penetration depth reflects the depletion of the superfluid due to thermal [quasiparticle excitations](@entry_id:138475). [@problem_id:3009616]
-   For a **fully gapped** superconductor (like conventional [s-wave](@entry_id:754474) materials), there is a finite energy cost $\Delta_0$ to create an excitation. At low temperatures ($k_B T \ll \Delta_0$), the number of excitations is exponentially small, leading to an exponentially flat temperature dependence: $\Delta\lambda(T) = \lambda(T) - \lambda(0) \propto \exp(-\Delta_0/k_B T)$.
-   For a superconductor with **nodes** in its gap (e.g., line nodes in d-wave [cuprates](@entry_id:142665)), excitations can be created with arbitrarily low energy. This leads to a power-law temperature dependence. For clean materials with line nodes, the low-temperature change is linear: $\Delta\lambda(T) \propto T$.

### Type I and Type II Superconductivity

The competition between the two length scales, $\xi$ and $\lambda$, leads to two distinct classes of superconducting behavior. The classification depends on the dimensionless **Ginzburg-Landau parameter**, $\kappa$:
$$ \kappa = \frac{\lambda}{\xi} $$
The distinction arises from the sign of the surface energy, $\sigma_{NS}$, of an interface between a normal (N) and a superconducting (S) domain. [@problem_id:3009572]
-   The cost to create the interface comes from suppressing the order parameter over the length $\xi$, contributing a positive term to $\sigma_{NS}$ proportional to $\xi$.
-   The gain comes from allowing the magnetic field to penetrate over the length $\lambda$, reducing the total magnetic expulsion energy and contributing a negative term to $\sigma_{NS}$ proportional to $\lambda$.

The net [surface energy](@entry_id:161228) is therefore determined by the balance of $\xi$ and $\lambda$. A rigorous calculation within GL theory shows that the [surface energy](@entry_id:161228) is zero when $\xi = \sqrt{2}\lambda$. This critical condition defines the boundary between the two types of superconductors. In terms of the GL parameter, the critical value is: [@problem_id:1825916]
$$ \kappa_c = \frac{1}{\sqrt{2}} $$

-   **Type I Superconductors** ($\kappa  1/\sqrt{2}$): In these materials, $\xi > \lambda$. The energy cost of suppressing the order parameter dominates, resulting in a **positive [surface energy](@entry_id:161228)** ($\sigma_{NS} > 0$). The system seeks to minimize the area of any N-S interface. These materials exhibit a complete Meissner effect up to a thermodynamic [critical field](@entry_id:143575) $H_c$, at which point the entire sample abruptly transitions to the normal state.

-   **Type II Superconductors** ($\kappa > 1/\sqrt{2}$): In these materials, $\lambda > \xi$. The energy gain from field penetration dominates, resulting in a **negative [surface energy](@entry_id:161228)** ($\sigma_{NS}  0$). It becomes energetically favorable for the system to create N-S interfaces. This leads to a radically different behavior in a magnetic field.

#### The Mixed State and Abrikosov Vortices

For a Type II superconductor, there are two [critical fields](@entry_id:272263), $H_{c1}$ and $H_{c2}$.
-   For $H  H_{c1}$, the material is in a complete Meissner state, just like a Type I superconductor.
-   For $H > H_{c2}$, the material is in the normal state.
-   For $H_{c1}  H  H_{c2}$, the system enters a new thermodynamic phase known as the **[mixed state](@entry_id:147011)**. In this state, magnetic flux penetrates the superconductor not uniformly, but in the form of discrete, quantized fluxoids called **Abrikosov vortices**.

An Abrikosov vortex is a [topological defect](@entry_id:161750) in the superconducting order parameter, representing a tube of magnetic flux surrounded by circulating supercurrents. Its structure is governed by the two length scales, $\xi$ and $\lambda$. [@problem_id:3009470]
-   **Vortex Core**: At the center of the vortex, the order parameter $\Psi$ is driven to zero. This "normal" core has a radius on the order of the coherence length, $\xi$. The order parameter amplitude heals to its bulk value over this distance, behaving as $|\Psi(r)| \propto r$ for small radial distance $r$ from the center (for a singly-[quantized vortex](@entry_id:161003)).
-   **Magnetic Flux**: The normal core allows magnetic flux to thread through the superconductor. The total flux contained within a single vortex is precisely one flux quantum, $\Phi_0 = h/2e$. This is the lowest-energy configuration.
-   **Supercurrents**: Circulating around the core are persistent supercurrents. These currents are responsible for screening the magnetic field of the vortex from the rest of the bulk superconductor. The [current density](@entry_id:190690) vanishes at the very center (since $\Psi=0$), peaks at a radius of order $\xi$, and then decays over the longer length scale of the [penetration depth](@entry_id:136478), $\lambda$. The magnetic field is maximal at the vortex center and also decays over the scale $\lambda$.

As the external field increases above $H_{c1}$, more and more vortices penetrate the sample. These vortices repel each other and, in an ideal sample, arrange themselves into a regular triangular pattern known as the Abrikosov [vortex lattice](@entry_id:140837). This stable, mixed phase of coexisting superconducting regions and normal vortex cores persists until the field reaches $H_{c2}$, where the vortex cores overlap and the entire material becomes normal.