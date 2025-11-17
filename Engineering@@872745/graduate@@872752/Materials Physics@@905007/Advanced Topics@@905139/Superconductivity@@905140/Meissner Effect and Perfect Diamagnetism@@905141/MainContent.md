## Introduction
While the discovery of [zero electrical resistance](@entry_id:151583) heralded the dawn of superconductivity, the phenomenon's true defining characteristic is the active expulsion of magnetic fields—the Meissner-Ochsenfeld effect. This property elevates superconductivity from a mere transport curiosity to a distinct thermodynamic phase of matter. A simple perfect conductor, governed by Lenz's law, would trap any magnetic field present during its transition. A superconductor, however, actively ejects the field, achieving a state of [perfect diamagnetism](@entry_id:203008) regardless of its history. This raises a fundamental question: what physical principles drive this active expulsion and distinguish a superconductor from a perfect conductor?

This article provides a comprehensive exploration of the Meissner effect and [perfect diamagnetism](@entry_id:203008). Across the following chapters, you will gain a deep understanding of this macroscopic quantum phenomenon.

*   The first chapter, **Principles and Mechanisms**, dissects the thermodynamic and electrodynamic foundations of the Meissner effect. It contrasts a superconductor with a perfect conductor, introduces the pivotal London and Ginzburg-Landau phenomenological theories, and explains the crucial classification of superconductors into Type I and Type II.

*   Following this theoretical foundation, **Applications and Interdisciplinary Connections** explores the far-reaching consequences of flux expulsion. We will examine applications ranging from magnetic levitation and advanced [materials characterization](@entry_id:161346) techniques to profound analogies with particle physics, including the Anderson-Higgs mechanism.

*   Finally, **Hands-On Practices** offers a set of guided problems designed to solidify your understanding. You will have the opportunity to apply core concepts, such as calculating the London [penetration depth](@entry_id:136478) and classifying materials using the Ginzburg-Landau parameter, bridging the gap between theory and practical analysis.

## Principles and Mechanisms

The discovery of superconductivity was initially marked by the observation of [zero electrical resistance](@entry_id:151583). However, the defining characteristic that elevates superconductivity from a mere curiosity of [transport phenomena](@entry_id:147655) to a distinct thermodynamic phase of matter is the **Meissner-Ochsenfeld effect**, or simply the **Meissner effect**. This chapter delves into the fundamental principles and mechanisms that govern this phenomenon, distinguishing it from perfect conductivity and exploring the theoretical frameworks developed to describe it.

### The Meissner Effect: Beyond Perfect Conductivity

A hypothetical material with infinite electrical conductivity, $\sigma \to \infty$, is termed a **perfect conductor**. Its behavior is dictated by Ohm's law, $\mathbf{J} = \sigma \mathbf{E}$, and Maxwell's equations. For any finite [current density](@entry_id:190690) $\mathbf{J}$, the electric field $\mathbf{E}$ within the bulk of a [perfect conductor](@entry_id:273420) must be zero. Faraday's law of induction, $\nabla \times \mathbf{E} = - \frac{\partial \mathbf{B}}{\partial t}$, then imposes a crucial constraint on the magnetic induction $\mathbf{B}$ inside the material:
$$
\frac{\partial \mathbf{B}}{\partial t} = 0
$$
This equation implies that the magnetic field within a perfect conductor is "frozen" in time; it cannot change from the value it possessed at the moment the material became perfectly conducting. The state of a [perfect conductor](@entry_id:273420) is therefore path-dependent and determined by its history.

This [path dependence](@entry_id:138606) allows for a thought experiment that critically distinguishes a [perfect conductor](@entry_id:273420) from a true superconductor [@problem_id:2840823] [@problem_id:3009512]. Consider two protocols for cooling a sample below its critical temperature $T_c$ in the presence of a static, uniform external magnetic field $\mathbf{H}_0$:

1.  **Zero-Field-Cooled (ZFC):** The sample is first cooled below $T_c$ in zero field, resulting in an internal state with $\mathbf{B}=0$. Subsequently, the external field $\mathbf{H}_0$ is applied. To maintain the condition $\partial \mathbf{B} / \partial t = 0$, the [perfect conductor](@entry_id:273420) must generate persistent surface currents that screen the applied field, keeping the bulk induction at $\mathbf{B}=0$.

2.  **Field-Cooled (FC):** The external field $\mathbf{H}_0$ is first applied to the sample in its normal state ($T > T_c$), causing the field to penetrate, such that $\mathbf{B} \approx \mu_0 \mathbf{H}_0$. The sample is then cooled below $T_c$. At the moment of transition, the internal field is non-zero. The law $\partial \mathbf{B} / \partial t = 0$ dictates that this field must remain trapped within the material indefinitely.

A superconductor behaves differently. It is defined by the Meissner effect: the active expulsion of magnetic flux from its interior when it transitions into the superconducting state. This is not a dynamic effect but a defining property of the [thermodynamic equilibrium](@entry_id:141660) state. Regardless of the path taken, a superconductor in a sufficiently weak magnetic field will always seek its equilibrium state, which is characterized by $\mathbf{B}=0$ in the bulk.

Therefore, under the ZFC protocol, both a [perfect conductor](@entry_id:273420) and a superconductor will exhibit $\mathbf{B}=0$ in their interiors. However, under the FC protocol, the perfect conductor traps the field ($\mathbf{B} \approx \mu_0 \mathbf{H}_0$), whereas the superconductor actively expels it, achieving the same final state as in the ZFC case: $\mathbf{B}=0$. This history-independent final state is the hallmark of a true thermodynamic phase transition and the essence of the Meissner effect. The superconductor is not just a [perfect conductor](@entry_id:273420); it is a **perfect diamagnet**.

### The Thermodynamics of Flux Expulsion

The active expulsion of magnetic flux, a process that requires $\partial \mathbf{B} / \partial t \neq 0$, seemingly violates the electrodynamic rules of a [perfect conductor](@entry_id:273420). This indicates that the Meissner effect is not a purely electrodynamic phenomenon but is driven by thermodynamics. The superconducting state is a distinct phase of matter with a lower free energy than the normal state under appropriate conditions [@problem_id:2840873].

For a system at constant temperature $T$ and constant applied magnetic field $\mathbf{H}_a$, the stable equilibrium state is the one that minimizes the **Gibbs free energy density**, $g$. The change in $g$ upon applying a magnetic field is given by $dg = -\mu_0 M \, dH_a$, where $M$ is the magnetization.

Let's compare the Gibbs free energy densities of the normal ($n$) and superconducting ($s$) states. We take the superconducting state at zero field as our reference energy, $g_s(0, T)$. The normal state at zero field is higher in energy by the **condensation energy density**, a purely electronic energy gain from forming Cooper pairs. In the framework of Bardeen-Cooper-Schrieffer (BCS) theory, this energy density at zero temperature is $U_0 = \frac{1}{2}N(0)\Delta_0^2$, where $N(0)$ is the single-spin [electronic density of states](@entry_id:182354) at the Fermi level and $\Delta_0$ is the zero-temperature energy gap [@problem_id:2840878]. So, $g_n(0,T) = g_s(0,T) + U_0(T)$.

-   **Normal State:** For a normal non-magnetic metal, $M_n \approx 0$. Integrating $dg_n$ from $0$ to $H_a$ gives $g_n(H_a, T) \approx g_n(0, T)$.

-   **Superconducting (Meissner) State:** In this state, $\mathbf{B}=0$. From the relation $\mathbf{B} = \mu_0(\mathbf{H}+\mathbf{M})$ and assuming negligible demagnetizing effects ($H_{internal} \approx H_a$), we find $M_s = -H_a$. The material is a perfect diamagnet. Integrating $dg_s$ gives:
    $$
    g_s(H_a, T) = g_s(0, T) - \int_0^{H_a} \mu_0 (-H_a') \, dH_a' = g_s(0, T) + \frac{1}{2}\mu_0 H_a^2
    $$
    The term $\frac{1}{2}\mu_0 H_a^2$ represents the magnetic energy cost to expel the field from the sample volume.

The superconducting state is stable as long as $g_s(H_a, T)  g_n(H_a, T)$. The difference is:
$$
\Delta g = g_s(H_a, T) - g_n(H_a, T) = \left(g_s(0, T) - g_n(0, T)\right) + \frac{1}{2}\mu_0 H_a^2 = -U_0(T) + \frac{1}{2}\mu_0 H_a^2
$$
This difference becomes zero at the **thermodynamic [critical field](@entry_id:143575)**, $H_c(T)$, where the energy cost of field expulsion exactly balances the [condensation energy](@entry_id:195476) gain. Setting $\Delta g = 0$ gives the fundamental relation:
$$
U_0(T) = \frac{1}{2}\mu_0 H_c(T)^2
$$
The Meissner state is stable for $H_a  H_c(T)$. This thermodynamic analysis reveals that [perfect diamagnetism](@entry_id:203008) is an equilibrium property driven by the competition between electronic condensation energy and [magnetic field energy](@entry_id:268850). A [perfect conductor](@entry_id:273420), lacking any [condensation energy](@entry_id:195476), would always find flux expulsion to be energetically costly and would not exhibit the Meissner effect [@problem_id:2840873].

At zero temperature, this allows us to directly connect the microscopic BCS parameters to the macroscopic [critical field](@entry_id:143575) [@problem_id:2840878]:
$$
\frac{1}{2}N(0)\Delta_0^2 = \frac{1}{2}\mu_0 H_c(0)^2 \implies B_c(0) \equiv \mu_0 H_c(0) = \Delta_0 \sqrt{\mu_0 N(0)}
$$
For typical values like $N(0) \approx 1.50 \times 10^{47} \text{ J}^{-1}\text{m}^{-3}$ and $\Delta_0 \approx 1.80 \text{ meV}$, this relation predicts a critical induction $B_c(0)$ on the order of $0.125$ Tesla, consistent with experimental values for many elemental superconductors.

### Phenomenological Description I: The London Equations

While thermodynamics explains *why* flux is expelled, it does not describe *how* the fields and currents are spatially distributed. The first successful phenomenological theory was proposed by Fritz and Heinz London. It posits a [constitutive relation](@entry_id:268485) for the supercurrent density $\mathbf{J}_s$. In its modern form, the theory is encapsulated in two equations. The second London equation, for static fields, relates the supercurrent to the local [magnetic vector potential](@entry_id:141246) $\mathbf{A}$:
$$
\mathbf{J}_s = -\frac{n_s e^2}{m} \mathbf{A} = -\frac{1}{\mu_0 \lambda_L^2} \mathbf{A}
$$
Here, $n_s$ is the density of superconducting charge carriers (with charge $e$ and mass $m$), and we have defined the **London [penetration depth](@entry_id:136478)** $\lambda_L$:
$$
\lambda_L = \sqrt{\frac{m}{\mu_0 n_s e^2}}
$$
Combining this with Ampere's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{J}_s$, and using $\mathbf{B} = \nabla \times \mathbf{A}$, we arrive at a governing equation for the magnetic field inside the superconductor [@problem_id:2840850]:
$$
\nabla^2 \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}
$$
This equation predicts that a magnetic field cannot exist uniformly inside a superconductor. For a semi-infinite superconductor occupying the space $x>0$ with a magnetic field $B_0 \hat{\mathbf{y}}$ applied parallel to the surface, the solution to this equation that vanishes deep inside the material ($x \to \infty$) is a simple exponential decay [@problem_id:2840850]:
$$
B(x) = B_0 \exp\left(-\frac{x}{\lambda_L}\right)
$$
This result beautifully captures the Meissner effect: the magnetic field is expelled from the bulk but penetrates a thin surface layer of characteristic thickness $\lambda_L$.

The [penetration depth](@entry_id:136478) is not a constant but depends on temperature, primarily through the temperature dependence of the [superfluid density](@entry_id:142018) $n_s(T)$. A simple and historically important description is the **Gorter-Casimir two-fluid model**, which posits a temperature dependence $n_s(T) = n(1 - (T/T_c)^4)$, where $n$ is the total electron density. Since $\lambda_L^2 \propto 1/n_s$, this leads to a characteristic divergence of the [penetration depth](@entry_id:136478) as the temperature approaches $T_c$ [@problem_id:233458]:
$$
\frac{\lambda_L(T)}{\lambda_L(0)} = \frac{1}{\sqrt{1 - (T/T_c)^4}}
$$

### Phenomenological Description II: The Ginzburg-Landau Theory

The London theory, while successful, is a local theory and cannot describe spatial variations in the superconducting state itself. The **Ginzburg-Landau (GL) theory**, a landmark development, provides a more powerful framework by introducing a complex **order parameter**, $\psi(\mathbf{r}) = |\psi(\mathbf{r})| e^{i\phi(\mathbf{r})}$. Here, $|\psi|^2$ is interpreted as being proportional to the density of superconducting carriers $n_s$, and $\phi(\mathbf{r})$ is the macroscopic quantum phase.

GL theory is an application of Landau's general theory of second-order phase transitions. It constructs a [free energy functional](@entry_id:184428) based on powers of the order parameter and its gradients. Crucially, it incorporates the magnetic field by using the principle of **[minimal coupling](@entry_id:148226)** from gauge theory, replacing the [momentum operator](@entry_id:151743) $-i\hbar\nabla$ with the gauge-invariant form $-i\hbar\nabla - q_s\mathbf{A}$, where $q_s$ is the charge of the superconducting carriers.

The Meissner effect emerges naturally from this formalism. In a uniform superconductor, the supercurrent is given by:
$$
\mathbf{J}_s = \frac{q_s\hbar}{m^*} |\psi|^2 \nabla\phi - \frac{q_s^2}{m^*} |\psi|^2 \mathbf{A}
$$
In a simply connected sample with no transport current, one can choose a gauge where $\nabla\phi=0$, recovering the London equation. The expulsion of the magnetic field is thus seen as a direct consequence of the superconducting state being described by a macroscopic wave function with a well-defined phase, giving rise to what is sometimes called **phase rigidity** or **phase stiffness** [@problem_id:2840849] [@problem_id:2840849]. In this picture, the photon effectively acquires a mass inside the superconductor, leading to its [exponential decay](@entry_id:136762), a phenomenon analogous to the Higgs mechanism in particle physics.

The GL theory introduces a second fundamental length scale: the **coherence length**, $\xi$. This length scale characterizes the distance over which the superconducting order parameter $|\psi|$ can vary without a significant energy cost. It represents the "stiffness" of the order parameter against spatial variations. The competition between the [penetration depth](@entry_id:136478) $\lambda$ and the coherence length $\xi$ is paramount and is quantified by the dimensionless **Ginzburg-Landau parameter** [@problem_id:2840802]:
$$
\kappa = \frac{\lambda}{\xi}
$$
This parameter governs the energy of an interface between a normal and a superconducting region, fundamentally dividing superconductors into two classes.

### Two Classes of Superconductors: Type I and Type II

The distinction between Type I and Type II superconductors is one of the most important consequences of the GL theory. It originates from the sign of the energy of a normal-superconducting (N-S) interface, $\sigma_{ns}$ [@problem_id:2840802].

This interface energy has two main competing contributions:
1.  A positive energy cost associated with the suppression of the order parameter $|\psi|$ over the coherence length $\xi$ near the interface.
2.  A [negative energy](@entry_id:161542) contribution (an energy gain) from the penetration of the magnetic field into the superconducting region over the length scale $\lambda$, which reduces the total volume from which the field must be expelled.

The sign of the net [surface energy](@entry_id:161228) $\sigma_{ns}$ depends on the relative magnitudes of $\xi$ and $\lambda$:
-   If $\xi > \lambda$, the positive energy cost dominates, and $\sigma_{ns} > 0$.
-   If $\lambda > \xi$, the [negative energy](@entry_id:161542) gain can dominate, and $\sigma_{ns}  0$.

A detailed calculation shows that the crossover occurs at $\kappa = 1/\sqrt{2}$.

**Type I Superconductors ($\kappa  1/\sqrt{2}$):**
These materials have a positive interface energy. It is therefore energetically unfavorable to create N-S boundaries. The system seeks to minimize the interface area. As a magnetic field is applied, the material remains in a complete Meissner state ([perfect diamagnetism](@entry_id:203008), $M=-H_a$) until the field reaches the thermodynamic critical field $H_c$. At this point, the entire sample abruptly transitions into the normal state. This is a [first-order phase transition](@entry_id:144521), characterized by a discontinuous jump in magnetization from $M=-H_c$ to $M \approx 0$ [@problem_id:2840895].

**Type II Superconductors ($\kappa > 1/\sqrt{2}$):**
These materials have a negative interface energy. It is energetically favorable to create N-S interfaces. This allows for a completely new state of matter: the **[mixed state](@entry_id:147011)** or **[vortex state](@entry_id:204018)**.
-   For low applied fields, $H_a  H_{c1}$, the material behaves like a Type I superconductor, exhibiting a complete Meissner effect ($M=-H_a$).
-   At a **[lower critical field](@entry_id:144776)**, $H_{c1}$, it becomes energetically favorable to allow magnetic flux to penetrate the sample. This happens not uniformly, but in the form of [quantized flux](@entry_id:157931) tubes called **vortices** or **fluxons**. Each vortex consists of a normal-state core (of radius $\approx \xi$) surrounded by circulating supercurrents. The field $H_{c1}$ is determined by the balance between the energy cost of creating a vortex line and the magnetic work gained by admitting flux [@problem_id:2840895]. For large $\kappa$, $H_{c1} \approx \frac{\Phi_0}{4\pi\mu_0\lambda^2}\ln\kappa$.
-   The flux contained within each vortex is quantized in units of the [magnetic flux quantum](@entry_id:136429), $\Phi_0 = h/(2e)$. The experimental confirmation of this value was crucial evidence that the superconducting charge carriers ($q_s$) have a charge of $2e$, confirming the microscopic BCS theory of electron pairing (Cooper pairs) [@problem_id:2840849].
-   In the mixed state, for $H_{c1}  H_a  H_{c2}$, the density of vortices increases with the applied field. The magnetization magnitude $|M|$ continuously decreases from its maximum value $|M|=H_{c1}$ at $H_a=H_{c1}$.
-   At the **[upper critical field](@entry_id:139431)**, $H_{c2}$, the normal cores of the vortices overlap, and superconductivity is destroyed throughout the material. The magnetization becomes zero. The transitions at $H_{c1}$ and $H_{c2}$ are second-order phase transitions.

### Refinements: Non-local Electrodynamics

The London and GL theories are **local** theories, meaning the supercurrent $\mathbf{J}_s(\mathbf{r})$ at a point $\mathbf{r}$ is determined by the [vector potential](@entry_id:153642) $\mathbf{A}(\mathbf{r})$ at that same point. This is a good approximation only if the [characteristic length scales](@entry_id:266383) of superconductivity are much smaller than the scale over which the fields vary.

Pippard first recognized that this is not always the case. The Cooper pairs that form the superfluid have a finite size, the BCS [coherence length](@entry_id:140689) $\xi_0$. The current at a point should depend on the vector potential averaged over a volume of this size. This leads to a **non-local** relationship between current and vector potential, which can be expressed in Fourier space as $\mathbf{J}_s(\mathbf{q}) = -Q(q) \mathbf{A}_\perp(\mathbf{q})$, where the response kernel $Q(q)$ is now wavevector-dependent [@problem_id:2840838].

In the clean limit ($\ell \gg \xi_0$, where $\ell$ is the [electron mean free path](@entry_id:185806)), the range of non-locality is set by $\xi_0$. For field variations on length scales shorter than $\xi_0$ (i.e., for large wavevectors $q \gtrsim 1/\xi_0$), the averaging process weakens the current response. This means $Q(q)$ decreases with increasing $q$. Consequently, the Meissner screening becomes less effective for short-wavelength field components. The field decay near the surface is no longer a pure exponential and is instead described by a more complex function that depends on the ratio $\lambda_L/\xi_0$.

Despite these modifications to the surface screening, the long-wavelength ($q \to 0$) response remains the same as in the London theory. Since bulk thermodynamic properties are governed by the response to uniform fields, non-locality does not alter the fundamental [perfect diamagnetism](@entry_id:203008) of the bulk superconducting state. It is a refinement that primarily affects the spatial distribution of fields and currents near surfaces and interfaces [@problem_id:2840838].