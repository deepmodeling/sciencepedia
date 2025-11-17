## Introduction
The electromagnetic response of a superconductor is its most defining feature, elevating it from a mere "perfect conductor" to a distinct thermodynamic phase of matter. While zero DC resistance was the first discovered property, it is the expulsion of magnetic fields—the Meissner-Ochsenfeld effect—that reveals the profound quantum mechanical nature of the superconducting state. Understanding this response is key to unlocking the physics of superconductivity itself and harnessing its potential. This article provides a graduate-level exploration of this topic, bridging the gap between macroscopic phenomena and their microscopic and phenomenological underpinnings.

Over the next chapters, you will embark on a systematic journey through the theoretical and practical aspects of superconducting electrodynamics. The "Principles and Mechanisms" chapter lays the theoretical groundwork, progressing from the macroscopic London equations to the powerful Ginzburg-Landau theory, and finally exploring the dynamic world of vortices and non-[equilibrium states](@entry_id:168134). Subsequently, the "Applications and Interdisciplinary Connections" chapter showcases how these principles translate into revolutionary technologies—from ultra-sensitive SQUID magnetometers to the building blocks of quantum computers—and reveals deep connections to fields like particle physics and cosmology. Finally, the "Hands-On Practices" section will allow you to apply these concepts to solve concrete physical problems, solidifying your understanding of this fascinating subject.

## Principles and Mechanisms

The electromagnetic response of a superconductor is perhaps its most defining characteristic. Following the discovery of zero DC resistance, the subsequent observation of [perfect diamagnetism](@entry_id:203008)—the Meissner-Ochsenfeld effect—revealed that superconductivity is a distinct thermodynamic phase of matter, not merely an instance of perfect conductivity. Understanding the mechanisms behind this response provides a deep insight into the nature of the superconducting state itself. This chapter will systematically develop the theoretical framework used to describe the electromagnetic properties of superconductors, progressing from the macroscopic phenomenological laws to the microscopic underpinnings and [non-equilibrium dynamics](@entry_id:160262).

### Macroscopic Electrodynamics: The London Equations

The electromagnetic behavior of superconductors can be remarkably well described by a set of simple, yet profound, phenomenological equations developed by brothers Fritz and Heinz London in 1935. The London theory is built upon the **two-fluid model**, which posits that the conduction electrons in a superconductor are divided into two interpenetrating components: normal electrons and superconducting electrons. The normal electrons behave as they do in a normal metal, experiencing scattering and contributing to resistance. The superconducting electrons, with density $n_s$, are condensed into a [macroscopic quantum state](@entry_id:192759) and move without dissipation. As temperature decreases below the critical temperature $T_c$, the [superfluid density](@entry_id:142018) $n_s$ grows from zero to encompass the total electron density at $T=0$.

The first key insight comes from considering the acceleration of these dissipation-free superconducting electrons, or "superelectrons," under an electric field $\mathbf{E}$. Assuming they have mass $m$ and charge $q=-e$, Newton's second law gives $m \frac{d\mathbf{v}_s}{dt} = q\mathbf{E}$. The supercurrent density is $\mathbf{j}_s = n_s q \mathbf{v}_s$. Differentiating with respect to time yields $\frac{\partial \mathbf{j}_s}{\partial t} = n_s q \frac{d\mathbf{v}_s}{dt}$. Combining these leads to the **first London equation**:

$$
\frac{\partial \mathbf{j}_s}{\partial t} = \frac{n_s e^2}{m} \mathbf{E}
$$

This equation correctly predicts infinite DC conductivity: a static electric field would lead to a current that increases linearly in time, an unphysical result implying that static electric fields cannot be sustained within a superconductor.

However, the first London equation alone is insufficient as it does not explain the Meissner effect—the expulsion of magnetic fields. To account for this, the Londons proposed the **second London equation**, which postulates a direct, local relationship between the supercurrent and the magnetic field $\mathbf{B}$:

$$
\nabla \times \mathbf{j}_s = - \frac{n_s e^2}{m} \mathbf{B}
$$

This [constitutive relation](@entry_id:268485) is the essence of the superconducting electromagnetic response. By combining it with the static form of Ampere's law, $\nabla \times \mathbf{B} = \mu_0 \mathbf{j}_s$ (assuming the supercurrent dominates), we can derive the governing equation for the magnetic field inside a superconductor. Taking the curl of Ampere's law gives $\nabla \times (\nabla \times \mathbf{B}) = \mu_0 (\nabla \times \mathbf{j}_s)$. Using a standard vector identity, $\nabla \times (\nabla \times \mathbf{B}) = \nabla(\nabla \cdot \mathbf{B}) - \nabla^2 \mathbf{B}$, and knowing that $\nabla \cdot \mathbf{B} = 0$, we find:

$$
\nabla^2 \mathbf{B} = \frac{\mu_0 n_s e^2}{m} \mathbf{B} = \frac{1}{\lambda_L^2} \mathbf{B}
$$

This equation demonstrates that a static magnetic field cannot exist uniformly within a superconductor. Instead, it must decay spatially. The [characteristic length](@entry_id:265857) scale of this decay is the **London penetration depth**, $\lambda_L$, defined as:

$$
\lambda_L = \sqrt{\frac{m}{\mu_0 n_s e^2}}
$$

For a semi-infinite superconductor occupying the space $x>0$ with an external field $B_0$ parallel to the surface, the solution to the screening equation is $B(x) = B_0 \exp(-x/\lambda_L)$. The field is not expelled abruptly but penetrates a thin layer near the surface, typically on the order of tens to hundreds of nanometers.

For a sample of finite size, the Meissner effect is incomplete, and the degree of field expulsion depends on the ratio of the sample size to the [penetration depth](@entry_id:136478) [@problem_id:1131154]. Consider a long superconducting rod of radius $R$ in a parallel magnetic field $H_{app}$. The field inside the rod, $B_z(r)$, is governed by the London screening equation in cylindrical coordinates. The solution that is regular at the origin is $B_z(r) = A I_0(r/\lambda_L)$, where $I_0$ is the modified Bessel function of the first kind. Applying the boundary condition $B_z(R) = \mu_0 H_{app}$, we find the field profile. The volume-averaged magnetization $\langle M \rangle$ can then be calculated, leading to an effective magnetic susceptibility $\chi = \langle M \rangle / H_{app}$ given by:

$$
\chi = \frac{2 I_1(R/\lambda_L)}{(R/\lambda_L) I_0(R/\lambda_L)} - 1
$$

In the limit of a very thick rod ($R \gg \lambda_L$), the ratio of Bessel functions approaches zero, and $\chi \to -1$, corresponding to [perfect diamagnetism](@entry_id:203008). Conversely, for a very thin wire ($R \ll \lambda_L$), the field penetrates almost uniformly, and the susceptibility approaches zero.

This expulsion of the magnetic field has energetic consequences. The transition to the superconducting state in a magnetic field lowers the total free energy of the system. A portion of this is due to the reduction in [magnetic field energy](@entry_id:268850) stored within the sample volume [@problem_id:1131187]. For the same cylindrical rod, the [magnetic energy](@entry_id:265074) per unit length in the normal state (with uniform field $B_n = \mu_0 H_0$) is $E_n = \frac{1}{2}\pi \mu_0 H_0^2 R^2$. In the superconducting state, the field is confined near the surface, and the stored energy $E_{sc}$ is significantly less. The reduction in magnetic energy, $\Delta E = E_n - E_{sc}$, quantifies the work done by the superconductor to expel the field. In the limit of a large radius ($R \gg \lambda_L$), this energy reduction is approximately $\frac{1}{2}\pi \mu_0 H_0^2 (R^2 - 2R\lambda_L)$, which is nearly the total energy of the field that was initially in the sample volume.

### Phenomenological Description: The Ginzburg-Landau Theory

The London theory provides an excellent macroscopic description but lacks a connection to the underlying quantum nature of superconductivity and cannot describe situations where the superconducting properties vary in space, such as at a [normal-superconductor interface](@entry_id:140314) or in the core of a vortex. The Ginzburg-Landau (GL) theory, developed in 1950, fills this gap by introducing a complex **order parameter**, $\psi(\mathbf{r})$, which can be interpreted as a macroscopic [wave function](@entry_id:148272) for the superconducting electrons. The local density of superelectrons is given by $n_s^*(\mathbf{r}) = |\psi(\mathbf{r})|^2$.

The GL theory is based on a phenomenological [free energy functional](@entry_id:184428), $F_s$, expanded in powers of the order parameter and its gradient near the critical temperature $T_c$:

$$
F_s = F_n + \int d^3r \left[ \alpha(T) |\psi|^2 + \frac{\beta}{2} |\psi|^4 + \frac{1}{2m^*} |(-i\hbar\nabla - q^*\mathbf{A})\psi|^2 + \frac{\mathbf{B}^2}{2\mu_0} \right]
$$

Here, $F_n$ is the free energy of the normal state. The term with coefficient $\alpha(T)$ drives the transition; near $T_c$, $\alpha(T) = \alpha_0(T-T_c)$ with $\alpha_0 > 0$. Below $T_c$, $\alpha$ is negative, favoring a non-zero $\psi$. The $\beta |\psi|^4$ term (with $\beta > 0$) ensures stability. The gradient term represents the kinetic energy of the superelectrons (with effective mass $m^*$ and charge $q^* = 2e$) and includes their coupling to the [magnetic vector potential](@entry_id:141246) $\mathbf{A}$. The final term is the energy of the magnetic field itself.

From this framework, two fundamental length scales emerge naturally. The **coherence length**, $\xi$, describes the characteristic distance over which the order parameter $\psi$ can vary without a significant energy penalty. It is defined as:

$$
\xi(T) = \frac{\hbar}{\sqrt{2m^*|\alpha(T)|}}
$$

The **penetration depth**, $\lambda$, which is equivalent to the London penetration depth, is the scale over which magnetic fields are screened. In GL theory, it is given by:

$$
\lambda(T) = \sqrt{\frac{m^*\beta}{\mu_0 (q^*)^2 |\alpha(T)|}}
$$

The ratio of these two length scales defines the dimensionless **Ginzburg-Landau parameter**, $\kappa$:

$$
\kappa = \frac{\lambda}{\xi}
$$

This parameter is of paramount importance as it distinguishes two fundamentally different types of superconductors. The distinction is based on the energy of the interface between a normal and a superconducting region. This [surface energy](@entry_id:161228) is positive if $\xi > \lambda$ (i.e., $\kappa  1/\sqrt{2}$), and negative if $\lambda > \xi$ (i.e., $\kappa > 1/\sqrt{2}$).

*   **Type-I Superconductors ($\kappa  1/\sqrt{2}$):** The positive [surface energy](@entry_id:161228) makes the formation of many small normal-state regions energetically unfavorable. These materials exhibit a complete Meissner effect up to a single **thermodynamic critical field**, $H_c$, at which superconductivity is abruptly destroyed in a [first-order phase transition](@entry_id:144521).

*   **Type-II Superconductors ($\kappa > 1/\sqrt{2}$):** The negative [surface energy](@entry_id:161228) makes it favorable for magnetic flux to penetrate the material in the form of [quantized flux](@entry_id:157931) tubes, or vortices, while the bulk remains superconducting. These materials are characterized by two [critical fields](@entry_id:272263): a [lower critical field](@entry_id:144776) $H_{c1}$, where flux begins to penetrate, and a much higher **[upper critical field](@entry_id:139431)**, $H_{c2}$, where bulk superconductivity is finally suppressed in a [second-order phase transition](@entry_id:136930).

The GL theory provides a precise relationship between these [critical fields](@entry_id:272263) and the parameter $\kappa$ [@problem_id:1131196]. The thermodynamic critical field $H_c$ is related to the condensation energy density (the energy gained by entering the superconducting state): $\frac{1}{2}\mu_0 H_c^2 = \frac{\alpha^2}{2\beta}$. The [upper critical field](@entry_id:139431) $H_{c2}$ is the maximum field in which an infinitesimal superconducting order parameter can nucleate. This is found by solving the linearized GL equation, which has the form of a Schrödinger equation for a charged particle in a magnetic field. The condition for a solution to exist leads to an expression for $H_{c2}$. Combining these results with the definitions of $\lambda$ and $\xi$, one arrives at the celebrated relation:

$$
H_{c2} = \sqrt{2} \kappa H_c
$$

This elegantly shows that for Type-II superconductors ($\kappa > 1/\sqrt{2}$), the [upper critical field](@entry_id:139431) is always larger than the thermodynamic [critical field](@entry_id:143575), allowing for the existence of the [mixed state](@entry_id:147011) between $H_{c1}$ and $H_{c2}$.

### The Vortex State in Type-II Superconductors

In a Type-II superconductor placed in a magnetic field $H$ such that $H_{c1}  H  H_{c2}$, the system enters a [mixed state](@entry_id:147011), also known as the Shubnikov phase. In this state, the magnetic flux penetrates the material in a lattice of discrete fluxoids called **Abrikosov vortices**.

Each vortex consists of a normal-conducting core of radius $\sim\xi$, where the order parameter $\psi$ is suppressed to zero. This core is surrounded by circulating supercurrents in a region of radius $\sim\lambda$. These currents screen the magnetic field, confining it to the [vortex core](@entry_id:159858). A key feature of these vortices is that the total magnetic flux contained within each is quantized in units of the **[magnetic flux quantum](@entry_id:136429)**, $\Phi_0 = h/2e$. The charge $2e$ is a direct manifestation of the fact that the superconducting charge carriers are Cooper pairs of two electrons.

The magnetic field of an isolated vortex line along the $z$-axis can be found by solving the London equation with a source term representing the [quantized flux](@entry_id:157931) at the origin [@problem_id:1131156]. The solution for the field magnitude $B(r)$ at a radial distance $r$ is given by $B(r) = \frac{\Phi_0}{2\pi\lambda^2} K_0(r/\lambda)$, where $K_0$ is the modified Bessel function of the second kind. Far from the core ($r \gg \lambda$), the field has a characteristic asymptotic decay, $B(r) \propto r^{-1/2} \exp(-r/\lambda)$, which is a power law modulated by the exponential screening. The circulating supercurrents also endow the vortex with a magnetic moment. The magnetic dipole moment per unit length of a single vortex line is a universal quantity, given by $\mathcal{M}_z = \Phi_0 / \mu_0$, independent of material parameters [@problem_id:1131155].

Vortices within a superconductor interact with one another. The overlapping fields and currents of two parallel vortices lead to a repulsive force between them. For a separation $d$ that is small compared to the [penetration depth](@entry_id:136478) ($\xi \ll d \ll \lambda$), the repulsive force per unit length is found to be $f(d) \approx \frac{\Phi_0^2}{2\pi\mu_0\lambda^2 d}$ [@problem_id:1203]. This $1/d$ repulsion causes the vortices to arrange themselves into a stable, ordered configuration, typically a triangular Abrikosov lattice, to minimize the total interaction energy.

The presence of mobile vortices has profound consequences for the transport properties of Type-II superconductors. When a transport current density $\mathbf{J}$ is passed through the material in the presence of vortices, it exerts a Lorentz-like force per unit length, $\mathbf{F}_L = \mathbf{J} \times \mathbf{\Phi}_0$, on each vortex (where $\mathbf{\Phi}_0$ is a vector of magnitude $\Phi_0$ aligned with the vortex). If the vortices are free to move, they will be set into motion, opposed by a [viscous drag](@entry_id:271349) force $\mathbf{F}_D = -\eta \mathbf{v}$. In steady state, these forces balance, leading to a constant vortex velocity $\mathbf{v}$. Crucially, the motion of the magnetic flux lines induces a [macroscopic electric field](@entry_id:196409) according to the Josephson relation, $\mathbf{E} = \mathbf{B} \times \mathbf{v}$. Since this electric field is parallel to the current flow, it gives rise to a finite resistance. This process is known as **[flux flow](@entry_id:184417)**. The resulting **flux-flow [resistivity](@entry_id:266481)**, $\rho_f$, can be derived by combining these principles and is given by [@problem_id:1206]:

$$
\rho_f = \frac{B \Phi_0}{\eta}
$$

This dissipation is a major limitation for practical applications of Type-II superconductors in magnets. To achieve [zero resistance](@entry_id:145222), the vortices must be held in place by **pinning** them at defects, grain boundaries, or impurities within the material, which provide energetically favorable sites.

### Frequency-Dependent and Non-Equilibrium Response

The electromagnetic response of a superconductor is not only a function of static fields but also depends critically on the frequency of the applied fields. This is best described using a frequency-dependent complex conductivity, $\sigma(\omega) = \sigma_1(\omega) + i\sigma_2(\omega)$.

The imaginary part, $\sigma_2$, represents the inductive response of the superfluid. In the ideal London model, the superfluid accelerates freely, leading to $\sigma_2 = \frac{n_s e^2}{m\omega} = \frac{1}{\mu_0 \lambda_L^2 \omega}$. This $1/\omega$ dependence is a hallmark of an ideal inductor.

The real part, $\sigma_1$, represents energy absorption or dissipation. At any finite temperature, the [normal fluid](@entry_id:183299) component provides a dissipative channel. In the [two-fluid model](@entry_id:139846), this leads to a finite **[surface resistance](@entry_id:149810)**, $R_s = \text{Re}(Z_s)$, where $Z_s$ is the [surface impedance](@entry_id:194306). For low frequencies ($\omega\tau \ll 1$, where $\tau$ is the normal electron scattering time), the normal fluid behaves like a simple resistor, and its presence allows an AC electric field to penetrate into the superconductor alongside the magnetic field, driving dissipative currents. The resulting [surface resistance](@entry_id:149810) scales as $\omega^2$ and is proportional to the density of normal carriers [@problem_id:1131190]. This finite AC loss is a critical consideration in high-frequency applications like superconducting resonant cavities.

The microscopic BCS theory provides a more detailed picture of $\sigma(\omega)$. At $T=0$, there are no normal electrons (quasiparticles). Energy absorption can only occur if a photon has enough energy to break a Cooper pair, creating two [quasiparticle excitations](@entry_id:138475). This requires a minimum [photon energy](@entry_id:139314) equal to the superconducting energy gap, $\hbar\omega \ge 2\Delta$. Therefore, at $T=0$, $\sigma_1(\omega) = 0$ for $\hbar\omega  2\Delta$. At the [absorption edge](@entry_id:274704), $\hbar\omega \to (2\Delta)^+$, the Mattis-Bardeen formulas predict that the conductivity jumps to a finite value. Specifically, the ratio to the normal state conductivity is [@problem_id:1131163]:

$$
\lim_{\hbar\omega \to 2\Delta^+} \frac{\sigma_1(\omega)}{\sigma_n} = \frac{\pi}{2}
$$

This sharp onset of absorption is a direct consequence of the BCS density of states, which has a singularity at the gap edge.

Beyond equilibrium response, the dynamics of a superconductor returning to equilibrium after a perturbation reveal further collective phenomena. The **Time-Dependent Ginzburg-Landau (TDGL)** theory provides a framework for these processes. Perturbations to the order parameter can be decomposed into changes in its amplitude, $|\psi|$, and its phase, $\phi$.

A small, spatially uniform perturbation of the order parameter *amplitude* will relax back to its equilibrium value exponentially. The relaxation time, $\tau_{amp}$, is governed by the curvature of the GL free energy potential. Near the critical temperature, this [relaxation time](@entry_id:142983) is found to be $\tau_{amp} = \frac{\gamma}{2\alpha_0(T_c-T)}$ [@problem_id:1207]. The divergence of $\tau_{amp}$ as $T \to T_c$ is an example of **[critical slowing down](@entry_id:141034)**, a universal feature of second-order phase transitions.

The dynamics of the order parameter *phase* are even more intricate and are coupled to the dynamics of the quasiparticle population. A spatial gradient in the phase corresponds to a supercurrent ($\mathbf{j}_s \propto \nabla\phi$), while a temporal gradient corresponds to a voltage, or more precisely, a difference in the chemical potential for Cooper pairs ($U = -\hbar \partial\phi/\partial t$). The conversion between the superfluid and normal fluid currents can create a **charge imbalance**, where the quasiparticle distribution is no longer in [local equilibrium](@entry_id:156295). This imbalance relaxes at a characteristic rate. The coupling between these processes gives rise to collective modes. For a one-dimensional wire, this leads to a diffusive-like relaxation of phase perturbations [@problem_id:1131180].

In a two-dimensional film near $T_c$, this coupling manifests as a propagating collective excitation known as the **Carlson-Goldman mode**. This mode can be visualized as a wave of charge imbalance, where oscillations between the superfluid and normal fluid densities propagate through the material. Its existence is a direct consequence of the coupling between the inductive (superfluid) and diffusive (quasiparticle) [charge transport](@entry_id:194535) channels. The mode has a characteristic [dispersion relation](@entry_id:138513), which in certain limits is given by $\text{Re}[\omega(q)] \approx \sqrt{(Dq^2 + \gamma_{in}) / (L_K \sigma_n)}$, where $D$ is the quasiparticle diffusion constant, $\gamma_{in}$ is the charge-imbalance relaxation rate, $L_K$ is the [kinetic inductance](@entry_id:141594), and $\sigma_n$ is the [normal fluid](@entry_id:183299) conductivity [@problem_id:1131170]. The observation of this mode was a significant confirmation of the non-equilibrium dynamic theories of superconductivity.

### Advanced Topics and Probes of Superconductivity

The electromagnetic response serves as a powerful and versatile tool to probe the more subtle and complex properties of superconductors, including the effects of material purity and the nature of the superconducting gap itself.

#### Non-local Electrodynamics and the Clean/Dirty Limits

The London equations assume a local relationship between current and fields. This is an approximation valid only when the length scales over which the fields vary (e.g., $\lambda$) are much larger than the intrinsic size of a Cooper pair, the **BCS [coherence length](@entry_id:140689)** $\xi_0$. When this condition is not met, the response becomes non-local: the current at a point $\mathbf{r}$ depends on the vector potential in a neighborhood around $\mathbf{r}$.

This non-locality is affected by [impurity scattering](@entry_id:267814). We distinguish two regimes based on the [electron mean free path](@entry_id:185806), $\ell$:
*   **Clean limit:** $\ell \gg \xi_0$. The Cooper pair's motion is ballistic over its own size.
*   **Dirty limit:** $\ell \ll \xi_0$. The constituent electrons scatter many times within the extent of a single pair.

The effective coherence length that governs the non-local response, known as the **Pippard [coherence length](@entry_id:140689)** $\xi_{pip}$, accounts for both the intrinsic pair size and scattering. These effects combine like parallel resistors, leading to the relation [@problem_id:1131159]:

$$
\frac{1}{\xi_{pip}} = \frac{1}{\xi_0} + \frac{1}{\ell}
$$

In the dirty limit, $\xi_{pip} \approx \ell$. Since [impurity scattering](@entry_id:267814) reduces the effective [coherence length](@entry_id:140689) while having a smaller effect on the penetration depth, it generally increases the Ginzburg-Landau parameter $\kappa = \lambda/\xi$. Consequently, a material that is a Type-I superconductor in its pure form can become a Type-II superconductor when made sufficiently dirty. This effect is crucial in the engineering of high-field superconducting materials. Similarly, the temperature dependence of quantities like the penetration depth is different in the two limits. For instance, in the dirty limit near $T_c$, the inverse square [penetration depth](@entry_id:136478) depends linearly on temperature, with a slope $\frac{d}{dT}(\lambda^{-2}) \propto -\mu_0 \sigma_n k_B$, where $\sigma_n$ is the normal-state conductivity [@problem_id:1131177].

#### Probing Unconventional Superconductivity

While many superconductors are well-described by the conventional BCS theory with a uniform, isotropic ([s-wave](@entry_id:754474)) energy gap, a large class of materials, including the high-temperature cuprates and [iron-based superconductors](@entry_id:138849), exhibit **[unconventional superconductivity](@entry_id:141315)**. Their properties are often dictated by an anisotropic energy gap that may contain nodes (points or lines on the Fermi surface where the gap vanishes).

The electromagnetic response is a primary tool for distinguishing these states. For instance, in **[multi-band superconductors](@entry_id:198577)** like MgB₂, superconductivity exists simultaneously in different [electronic bands](@entry_id:175335), each with its own energy gap. The total electromagnetic response is a superposition of the contributions from each band. The low-frequency imaginary conductivity, for example, becomes a weighted sum over the bands, with each band contributing a term proportional to $1/\Delta_i$, allowing experimental techniques to probe the different gap values [@problem_id:1131182].

A particularly powerful technique is the measurement of the **nonlinear electromagnetic response**. While the linear response of s-wave and [d-wave superconductors](@entry_id:139318) can be similar, their nonlinear responses differ dramatically. In a [d-wave superconductor](@entry_id:139850), the presence of nodes in the gap allows for the easy creation of low-energy [quasiparticle excitations](@entry_id:138475) by a supercurrent (via the Doppler shift of the quasiparticle spectrum). This leads to a nonlinear current-velocity relationship that, at $T=0$, contains a non-analytic term of the form $\mathbf{J}_s \propto \gamma |\mathbf{v}_s|\mathbf{v}_s$ [@problem_id:1131183]. When such a material is subjected to a strong sinusoidal magnetic field of frequency $\omega$, this nonlinearity generates higher harmonics in the magnetic response. The non-analytic term leads to a distinct scaling of the third-harmonic magnetization with the applied field amplitude, $M_{3\omega} \propto H_0^2$. This contrasts with the $M_{3\omega} \propto H_0^3$ scaling expected from the analytic nonlinearities of a conventional gapped superconductor. The measurement of this nonlinear Meissner effect has become a key experimental signature for identifying nodal superconductivity.

Finally, in a zero magnetic field, the [specific heat jump](@entry_id:141287) at the superconducting transition, $\Delta c$, provides another [thermodynamic signature](@entry_id:185212). For a Type-II superconductor, this jump persists in the presence of a magnetic field, though its magnitude is reduced. GL theory predicts that the jump is proportional to the transition temperature, $\Delta c \propto T_{c2}(H)$. In the specific, theoretical limit where the applied field equals the extrapolated zero-temperature [critical field](@entry_id:143575), $H=H_{c2}(0)$, the transition is pushed to absolute zero, $T_{c2}=0$, and the [specific heat jump](@entry_id:141287) vanishes [@problem_id:1131166]. This illustrates the deep connections between the electromagnetic, thermodynamic, and microscopic properties of the superconducting state.