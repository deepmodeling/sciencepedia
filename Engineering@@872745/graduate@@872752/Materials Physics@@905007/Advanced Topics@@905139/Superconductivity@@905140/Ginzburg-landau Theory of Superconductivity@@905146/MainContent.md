## Introduction
The discovery of superconductivity presented a profound puzzle: how could a material exhibit [zero electrical resistance](@entry_id:151583) and expel magnetic fields? While the microscopic Bardeen-Cooper-Schrieffer (BCS) theory provided a quantum mechanical answer, a bridge was needed to connect this microscopic world to the macroscopic, measurable phenomena observed in the lab. The Ginzburg-Landau (GL) theory masterfully fills this gap. It is a powerful phenomenological framework that describes the superconducting state not through the complex interactions of individual electrons, but through a macroscopic complex order parameter and the universal principles of phase transitions. This approach provides not only a deep conceptual understanding but also a versatile computational tool for predicting the behavior of real-world superconducting materials.

This article provides a comprehensive exploration of the Ginzburg-Landau theory, structured to build from fundamental concepts to practical applications. The first chapter, **"Principles and Mechanisms"**, will introduce the core ideas: the complex order parameter, the construction of the [free energy functional](@entry_id:184428) based on symmetry, and the derivation of the theory's two fundamental length scales. We will also explore profound consequences like the Anderson-Higgs mechanism. The second chapter, **"Applications and Interdisciplinary Connections"**, demonstrates the theory's predictive power by applying it to calculate thermodynamic properties, describe the intricate [vortex state](@entry_id:204018) in Type II superconductors, and analyze nanoscale systems. We will also see how the theory is adapted for real materials with anisotropy and impurities, and explore its connections to other fields of physics. Finally, **"Hands-On Practices"** will offer a set of guided problems, allowing you to apply the theoretical principles to derive key results, such as the [critical fields](@entry_id:272263) and the conditions that distinguish superconductor types, solidifying your understanding of this essential theory.

## Principles and Mechanisms

### The Superconducting Order Parameter

The Ginzburg-Landau (GL) theory is a phenomenological framework that describes the superconducting state without delving into the microscopic pairing mechanism of electrons. Its central concept is the introduction of a complex **order parameter**, a macroscopic wave function denoted by $\psi(\mathbf{r})$. This function is not the [wave function](@entry_id:148272) of a single particle but rather a coarse-grained field whose value at a point $\mathbf{r}$ represents the collective state of a vast number of superconducting charge carriers—Cooper pairs—in a small volume around that point.

The order parameter can be expressed in terms of its magnitude and phase:
$$
\psi(\mathbf{r}) = |\psi(\mathbf{r})| e^{i\theta(\mathbf{r})}
$$
Each part of this complex function has a profound physical meaning. The magnitude squared, $|\psi(\mathbf{r})|^2$, is interpreted as being proportional to the local density of superconducting carriers, $n_s(\mathbf{r})$. In the normal state, there are no Cooper pairs, so $\psi = 0$. In the superconducting state, a condensate forms, and $\psi$ acquires a non-zero value, signifying the onset of order. The phase, $\theta(\mathbf{r})$, is uniform in the ground state of a simple superconductor, but its spatial variations give rise to supercurrents. The existence of a single, well-defined phase across the entire macroscopic sample is the hallmark of **macroscopic [quantum coherence](@entry_id:143031)**.

It is crucial to distinguish the phenomenological GL order parameter $\psi(\mathbf{r})$ from the microscopic pair amplitude found in the Bardeen-Cooper-Schrieffer (BCS) theory, $\langle \hat{\psi}_\downarrow(\mathbf{r})\hat{\psi}_\uparrow(\mathbf{r})\rangle$. While the former is a macroscopic, coarse-grained field, the latter is a quantum mechanical [expectation value](@entry_id:150961) at a specific point. The connection, established by Lev Gor'kov, shows that near the critical temperature, the GL order parameter is *proportional* to the spatially averaged BCS pair amplitude, not identical to it. The GL theory is thus a long-wavelength, low-energy effective theory built upon the microscopic foundation of Cooper pairing [@problem_id:2826158].

### The Ginzburg-Landau Free Energy Functional

The power of the GL theory lies in its construction of a [free energy functional](@entry_id:184428), $\mathcal{F}[\psi]$, based on general principles of symmetry and [analyticity](@entry_id:140716), as pioneered by Landau for second-order phase transitions. The system's equilibrium state is the one that minimizes this free energy. For a homogeneous superconductor near the critical temperature $T_c$, the free energy density $f$ is expanded as a power series in $\psi$ and its gradients.

**Potential Energy Terms:**
The simplest terms involving only $\psi$ must be invariant under a global U(1) [gauge transformation](@entry_id:141321) ($\psi \to \psi e^{i\phi}$), which reflects the [conservation of charge](@entry_id:264158). This dictates that the expansion must be in powers of $|\psi|^2$. Truncating the series at the fourth order, we obtain the potential energy density:
$$
f_{pot} = \alpha(T) |\psi|^2 + \frac{\beta}{2} |\psi|^4
$$
The coefficients $\alpha(T)$ and $\beta$ are phenomenological parameters [@problem_id:2826163].

*   The coefficient $\alpha(T)$ governs the onset of superconductivity. To model the transition, it is assumed to change sign at $T_c$. For $T > T_c$, the normal state ($\psi=0$) must be the stable minimum, requiring $\alpha(T) > 0$. For $T  T_c$, a superconducting state ($\psi \neq 0$) must be favored, requiring $\alpha(T)  0$. The simplest analytic form satisfying this is a [linear dependence](@entry_id:149638) near $T_c$: $\alpha(T) = \alpha_0(T - T_c)$, where $\alpha_0$ is a positive constant [@problem_id:2826137].

*   The coefficient $\beta$ must be positive ($\beta > 0$). When $T  T_c$, the $\alpha|\psi|^2$ term is negative and would drive $|\psi|$ to infinity. The positive $\beta|\psi|^4$ term ensures the stability of the free energy by penalizing large values of the order parameter, creating a minimum at a finite value. This condition is necessary for a continuous (second-order) phase transition [@problem_id:2826137, @problem_id:2826163].

Minimizing this potential energy for $T  T_c$ yields the equilibrium magnitude of the order parameter in the uniform superconducting state:
$$
|\psi_0|^2 = -\frac{\alpha(T)}{\beta} = \frac{\alpha_0}{\beta}(T_c - T)
$$
This result shows that the condensate density grows continuously from zero as the temperature is lowered below $T_c$, a key feature of a [second-order transition](@entry_id:154877).

**Kinetic and Magnetic Energy Terms:**
Spatial variations of the order parameter, such as those near an interface or in the presence of a supercurrent, increase the free energy. The lowest-order term involving gradients of $\psi$ that is consistent with the system's symmetries (e.g., [inversion symmetry](@entry_id:269948), which forbids terms linear in $\nabla$ [@problem_id:2826163]) is proportional to $|\nabla\psi|^2$.

To incorporate the electromagnetic field, we invoke the principle of **[local gauge invariance](@entry_id:154219)**. This requires replacing the ordinary gradient $\nabla$ with the gauge-covariant derivative, $\mathbf{D}$. For charge carriers of charge $e^*$ and mass $m^*$, this operator and the corresponding kinetic energy density term are:
$$
\mathbf{D}\psi = (-i\hbar\nabla - e^*\mathbf{A})\psi
$$
$$
f_{kin} = \frac{1}{2m^*} |\mathbf{D}\psi|^2 = \frac{1}{2m^*} |(-i\hbar\nabla - e^*\mathbf{A})\psi|^2
$$
Experimental evidence, such as [flux quantization](@entry_id:144492), confirms that the superconducting charge carriers are Cooper pairs, so we must use the pair charge $e^* = 2e$ and effective mass $m^*=2m_e$ [@problem_id:2826163].

Finally, the energy stored in the magnetic field itself must be included. In SI units, this is $f_{mag} = \frac{|\mathbf{B}|^2}{2\mu_0}$, where $\mathbf{B}$ is the local magnetic induction and $\mu_0$ is the [vacuum permeability](@entry_id:186031) [@problem_id:2826163].

Combining these pieces, the full Ginzburg-Landau [free energy functional](@entry_id:184428) is:
$$
\mathcal{F}[\psi, \mathbf{A}] = \int \left( \alpha |\psi|^2 + \frac{\beta}{2} |\psi|^4 + \frac{1}{2m^*}|(-i\hbar\nabla - e^*\mathbf{A})\psi|^2 + \frac{|\mathbf{B}|^2}{2\mu_0} \right) d^3r
$$
This functional is the cornerstone of the theory, from which all macroscopic electromagnetic properties of a superconductor can be derived.

### Supercurrent and Superfluid Density

The supercurrent is the dissipationless flow of Cooper pairs, and it arises naturally from the kinetic energy term in the GL functional. The supercurrent density $\mathbf{j}_s$ is defined as the response of the free energy to a change in the [vector potential](@entry_id:153642) $\mathbf{A}$. By taking the functional derivative of $\mathcal{F}$ with respect to $\mathbf{A}$, we obtain:
$$
\mathbf{j}_s = -\frac{\delta \mathcal{F}}{\delta \mathbf{A}} = \frac{e^*}{m^*} \text{Re}[\psi^*(-i\hbar\nabla - e^*\mathbf{A})\psi]
$$
Substituting $\psi = |\psi|e^{i\theta}$, this expression simplifies to:
$$
\mathbf{j}_s = \frac{e^*|\psi|^2}{m^*} (\hbar\nabla\theta - e^*\mathbf{A})
$$
This fundamental result reveals several key insights. The current is driven by the gauge-invariant gradient of the phase. This expression is precisely the form of the London equation. By comparing it to the standard hydrodynamic expression for a superfluid, $\mathbf{j}_s = n_s e^* \mathbf{v}_s$, where the superfluid velocity is given by the canonical relation $m^*\mathbf{v}_s = \hbar\nabla\theta - e^*\mathbf{A}$, we can make a direct identification. With the kinetic term normalized as $\frac{1}{2m^*}|\dots|^2$, the superfluid [number density](@entry_id:268986) $n_s$ (counting Cooper pairs) is simply the magnitude squared of the order parameter [@problem_id:2826193, @problem_id:2826206]:
$$
n_s = |\psi|^2
$$
This provides a concrete physical interpretation for the order parameter's magnitude and a direct link between the GL phenomenology and the London model. The energy associated with a phase twist, known as the **phase stiffness** or [superfluid stiffness](@entry_id:147718), is given by $\rho_s = \frac{\hbar^2 n_s}{m^*}$, which controls the energy cost of supercurrents.

### Characteristic Length Scales

The GL functional naturally gives rise to two fundamental length scales that govern the behavior of superconductors.

#### The Coherence Length $\xi(T)$

The **coherence length**, $\xi(T)$, is the characteristic length scale over which the superconducting order parameter $\psi$ can vary without a significant energy cost. It can be thought of as the minimum size of a "superconducting droplet". We can deduce this length by considering a small perturbation to the uniform superconducting state. By minimizing the [free energy functional](@entry_id:184428), one obtains the GL differential equations. Linearizing these equations for a small deviation $\delta\psi$ from the equilibrium value $\psi_0$ reveals that the perturbation heals, or decays, exponentially back to the bulk value. For $T  T_c$, this decay length is proportional to the coherence length [@problem_id:2826135].

From the GL coefficients, the coherence length is defined as:
$$
\xi(T) = \sqrt{\frac{\hbar^2}{2m^*|\alpha(T)|}}
$$
Since $\alpha(T) \propto (T_c - T)$, the [coherence length](@entry_id:140689) diverges near the critical temperature as $\xi(T) \propto (T_c - T)^{-1/2}$.

#### The Magnetic Penetration Depth $\lambda(T)$

The **[magnetic penetration depth](@entry_id:140378)**, $\lambda(T)$, is the [characteristic length](@entry_id:265857) scale over which an external magnetic field is screened and decays to zero inside a superconductor. This screening is the essence of the Meissner effect. This length can be derived by combining the GL expression for the supercurrent with Maxwell's equations. This leads to the London equation for the magnetic field, $\nabla^2\mathbf{B} = \mathbf{B}/\lambda^2$, which describes exponential decay.

The penetration depth is given by:
$$
\lambda(T) = \sqrt{\frac{m^*}{\mu_0 e^{*2} |\psi_0|^2}} = \sqrt{\frac{m^*\beta}{\mu_0 e^{*2} |\alpha(T)|}}
$$
Like the [coherence length](@entry_id:140689), the penetration depth also diverges as $\lambda(T) \propto (T_c - T)^{-1/2}$ near $T_c$.

### The Anderson-Higgs Mechanism

In a neutral superfluid, the spontaneous breaking of the global U(1) symmetry would lead to the emergence of a massless collective excitation known as a Goldstone boson, corresponding to long-wavelength fluctuations of the phase $\theta$. However, in a charged superconductor, this does not happen. The coupling between the order parameter and the electromagnetic field via the covariant derivative drastically alters the physics.

The key insight is that the phase of the order parameter, $\theta$, and the vector potential, $\mathbf{A}$, are not independent degrees of freedom. They are coupled through the gauge-invariant kinetic energy term, which depends on the combination $(\hbar\nabla\theta - e^*\mathbf{A})$. Because of the [local gauge symmetry](@entry_id:148072), one can always choose a gauge (the unitary gauge) where the phase fluctuation $\theta(\mathbf{r})$ is absorbed, or "eaten," by a redefinition of the [vector potential](@entry_id:153642). In this gauge, the kinetic term $\frac{1}{2m^*}|e^*\mathbf{A}|^2$ acts as a mass term for the [gauge field](@entry_id:193054) (the photon). The photon becomes massive inside the superconductor.

This phenomenon, where a [gauge boson](@entry_id:274088) acquires mass by absorbing the Goldstone boson of a spontaneously broken local symmetry, is the **Anderson-Higgs mechanism**. A [massive photon](@entry_id:153463) mediates a short-range force, which physically manifests as the screening of magnetic fields. The range of the force is inversely proportional to the photon's mass, and this range is precisely the [magnetic penetration depth](@entry_id:140378) $\lambda$. Thus, the Meissner effect is a direct and profound consequence of the Anderson-Higgs mechanism at play in superconductors [@problem_id:2826154].

### Type I and Type II Superconductivity

The behavior of a superconductor in an external magnetic field is determined by the interplay between the two fundamental length scales, $\xi$ and $\lambda$. Their ratio defines the dimensionless **Ginzburg-Landau parameter**, $\kappa$:
$$
\kappa = \frac{\lambda(T)}{\xi(T)}
$$
Since both $\lambda$ and $\xi$ have the same temperature dependence near $T_c$, $\kappa$ is a temperature-independent material constant within the GL regime.

The value of $\kappa$ determines whether a material is Type I or Type II. The distinction is governed by the sign of the [surface energy](@entry_id:161228), $\sigma$, of an interface between a normal (N) and a superconducting (S) domain. Creating such an interface involves two competing energy contributions:
1.  A positive energy cost, associated with suppressing the order parameter from its bulk value to zero over the coherence length $\xi$. This is a loss of [condensation energy](@entry_id:195476).
2.  A negative energy contribution (a gain), from allowing the magnetic field to penetrate a region of size $\lambda$, thereby reducing the magnetic field expulsion energy.

If $\xi \gg \lambda$ ($\kappa \ll 1$), the energy cost dominates, and the surface energy $\sigma$ is positive. If $\lambda \gg \xi$ ($\kappa \gg 1$), the energy gain dominates, and $\sigma$ is negative. A rigorous calculation minimizing the GL functional shows that the sign of the [surface energy](@entry_id:161228) changes at a critical value of $\kappa$ [@problem_id:2826189, @problem_id:2826201]:
$$
\kappa_{crit} = \frac{1}{\sqrt{2}}
$$

This leads to the classification:

*   **Type I Superconductors ($\kappa  1/\sqrt{2}$):** The surface energy is positive ($\sigma > 0$). The system minimizes the area of N-S interfaces. It exhibits a perfect Meissner effect, completely expelling magnetic fields up to a thermodynamic [critical field](@entry_id:143575) $H_c$, at which it undergoes a [first-order transition](@entry_id:155013) into the fully normal state. Most elemental superconductors are Type I.

*   **Type II Superconductors ($\kappa > 1/\sqrt{2}$):** The surface energy is negative ($\sigma  0$). It is energetically favorable for the system to create N-S interfaces. Above a [lower critical field](@entry_id:144776) $H_{c1}$, the magnetic field penetrates the material in the form of [quantized flux](@entry_id:157931) tubes, known as Abrikosov vortices. Each vortex has a normal core of size $\xi$ where $\psi \approx 0$, surrounded by screening supercurrents that circulate over a distance $\lambda$. The material is in a "[mixed state](@entry_id:147011)" of coexisting normal and superconducting regions. As the field increases, the density of vortices increases until they overlap at the [upper critical field](@entry_id:139431) $H_{c2}$, where the entire material becomes normal. Most alloys and high-temperature superconductors are Type II.

### Validity of Mean-Field Theory: The Ginzburg Criterion

The Ginzburg-Landau theory, as presented so far, is a [mean-field theory](@entry_id:145338); it neglects the effect of [thermal fluctuations](@entry_id:143642) of the order parameter. The validity of this approximation can be assessed by the **Ginzburg criterion**. The criterion compares the available thermal energy, $k_B T_c$, with the condensation energy gained within a characteristic fluctuation volume, which is the coherence volume $\xi^3$. Mean-field theory is valid when the condensation energy significantly exceeds the thermal energy, preventing fluctuations from destroying the superconducting order.

This comparison leads to a condition on the reduced temperature, $t = |T - T_c|/T_c$. The [mean-field approximation](@entry_id:144121) holds when $t$ is sufficiently far from zero, specifically when $t \gg \mathrm{Gi}$, where $\mathrm{Gi}$ is the dimensionless **Ginzburg number** [@problem_id:2826172]. The Ginzburg number can be derived from the GL parameters and is given by:
$$
\mathrm{Gi} = \frac{1}{2} \left( \frac{k_B T_c \mu_0^2 e^{*2}}{2\pi \hbar^2 m^*} \frac{m^*\beta}{\alpha_0 \hbar^2} \right)^2 \propto \left( \frac{k_B T_c}{\Delta C \xi_0^3} \right)^2
$$
where $\Delta C$ is the [specific heat jump](@entry_id:141287) at $T_c$ and $\xi_0$ is the zero-temperature coherence length (or more precisely, the amplitude in $\xi(T) = \xi_0 t^{-1/2}$).

The magnitude of $\mathrm{Gi}$ reveals the importance of fluctuations for a given material:
*   For conventional low-$T_c$ superconductors like niobium ($T_c \approx 9$ K), the [coherence length](@entry_id:140689) is large ($\xi_0 \sim 40$ nm). The Ginzburg number is extremely small, $\mathrm{Gi} \sim 10^{-8}$. The fluctuation regime is confined to an immeasurably tiny temperature window around $T_c$, making the mean-field GL theory exceptionally accurate.
*   For high-$T_c$ [cuprate superconductors](@entry_id:146531) ($T_c \approx 90$ K), the coherence length is very short ($\xi_0 \sim 1.5$ nm) and $T_c$ is high. This leads to a much larger Ginzburg number, with $\mathrm{Gi}$ approaching unity. This implies that [thermal fluctuations](@entry_id:143642) are significant over a wide temperature range (several Kelvin) around $T_c$. In this regime, the simple GL [mean-field theory](@entry_id:145338) breaks down, and more advanced theories that account for fluctuations are necessary to describe phenomena like the broadening of the resistive transition and precursor diamagnetism above $T_c$ [@problem_id:2826172].