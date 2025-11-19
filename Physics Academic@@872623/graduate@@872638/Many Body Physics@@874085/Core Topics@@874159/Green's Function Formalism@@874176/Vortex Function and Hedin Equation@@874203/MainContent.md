## Introduction
The behavior of electrons in solids, molecules, and other forms of condensed matter is governed by the complex and inseparable effects of their mutual Coulomb repulsion. While single-particle theories like Density Functional Theory (DFT) provide a remarkable starting point, they are fundamentally limited in describing [excited states](@entry_id:273472) and the detailed dynamics of electron correlations. To bridge this gap, a more rigorous framework is required that can systematically account for the full complexity of the many-body problem. This article introduces Hedin's equations, a formally exact and powerful theoretical structure that serves as the foundation for modern [many-body perturbation theory](@entry_id:168555).

This article will guide you through this sophisticated framework in three progressive chapters. In **Principles and Mechanisms**, we will dissect Hedin's pentagon of equations, defining the physical meaning of the [self-energy](@entry_id:145608), [screened interaction](@entry_id:136395), and the crucial [vertex function](@entry_id:145137). We will then explore the derivation and physical interpretation of the celebrated **GW approximation**, the most widely used method stemming from this formalism. Following this, the **Applications and Interdisciplinary Connections** chapter will demonstrate the practical power of these concepts, showing how the GW method corrects the [band gap problem](@entry_id:143831) in materials and how the Bethe-Salpeter equation is used to calculate [optical spectra](@entry_id:185632) and describe [excitons](@entry_id:147299). We will also explore the surprising reach of this formalism into other disciplines, including superconductivity and [quantum transport](@entry_id:138932). Finally, the **Hands-On Practices** section provides a set of conceptual problems designed to solidify your understanding of key derivations, such as the Galitskii-Migdal-Koltun sum rule and the physics of Thomas-Fermi screening.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the behavior of interacting many-electron systems. We will build upon the introductory concepts by presenting a formally exact framework, known as Hedin's equations. From this exact starting point, we will derive and analyze the widely used **GW approximation**, explore its physical content, and discuss its various implementations. Subsequently, we will examine the crucial role of conservation laws and [vertex corrections](@entry_id:146982), culminating in an introduction to the Bethe-Salpeter equation for describing excitonic effects.

### The Formalism of Hedin's Equations

The [complex dynamics](@entry_id:171192) of interacting electrons can be captured by a set of coupled, self-consistent integral equations, first formulated by Lars Hedin in 1965. This framework, now known as **Hedin's equations**, provides a formally exact description of the system in terms of five key quantities: the one-particle Green's function ($G$), the self-energy ($\Sigma$), the screened Coulomb interaction ($W$), the irreducible polarizability ($P$), and the [vertex function](@entry_id:145137) ($\Gamma$).

These quantities have profound physical meanings [@problem_id:2983417]:
*   The **one-particle Green's function**, $G(1,2)$, is the central object, describing the propagation of an electron or a hole between two space-time points, $1 \equiv (\mathbf{r}_1, t_1, \sigma_1)$ and $2 \equiv (\mathbf{r}_2, t_2, \sigma_2)$. Its poles correspond to the [quasiparticle energies](@entry_id:173936), which are the electron addition and removal energies measured in photoemission experiments.
*   The **[self-energy](@entry_id:145608)**, $\Sigma(1,2)$, is a non-local and dynamic [effective potential](@entry_id:142581) that encapsulates all exchange and correlation effects experienced by a propagating particle. It acts as a correction to the single-particle picture, renormalizing energies and introducing finite lifetimes.
*   The **screened Coulomb interaction**, $W(1,2)$, represents the effective interaction between two charges within the material. It is the bare Coulomb interaction, $v$, "dressed" or weakened by the [dynamic polarization](@entry_id:153626) of the surrounding electron cloud. It is the interaction responsible for mediating energy loss processes and collective excitations like [plasmons](@entry_id:146184).
*   The **irreducible polarizability**, $P(1,2)$, is a response function that describes how the electron density responds to a change in the *total* [effective potential](@entry_id:142581) (external plus induced). It is deemed "irreducible" because, in a [diagrammatic expansion](@entry_id:139147), it cannot be split into two separate polarization parts by cutting a single bare interaction line, $v$.
*   The **[vertex function](@entry_id:145137)**, $\Gamma(1,2;3)$, represents the correction to the interaction vertex due to many-body effects. It describes how the coupling of a particle to an external potential at point $3$ is modified by the surrounding [correlated electrons](@entry_id:138307).

These five quantities are interconnected through a [closed set](@entry_id:136446) of five equations, often depicted as a pentagon [@problem_id:2785443] [@problem_id:2930174] [@problem_id:2983417]. Using a compact notation where repeated numerical indices imply integration over the corresponding space-time and spin variables, the equations are:

1.  **Dyson's Equation for $G$**: The interacting Green's function $G$ is related to a non-interacting reference $G_0$ and the [self-energy](@entry_id:145608) $\Sigma$.
    $$ G(1,2) = G_0(1,2) + G_0(1,3)\Sigma(3,4)G(4,2) $$
    In operator form, this is $G^{-1} = G_0^{-1} - \Sigma$.

2.  **Equation for $\Sigma$**: The self-energy is constructed from the Green's function, the [screened interaction](@entry_id:136395), and the [vertex function](@entry_id:145137).
    $$ \Sigma(1,2) = \mathrm{i} \, G(1,3)W(1^+,4)\Gamma(3,2;4) $$
    The infinitesimal time shift $1^+$ ensures correct time ordering.

3.  **Dyson's Equation for $W$**: The [screened interaction](@entry_id:136395) $W$ is the sum of the bare interaction $v$ and all interactions mediated by the polarizable medium.
    $$ W(1,2) = v(1,2) + v(1,3)P(3,4)W(4,2) $$

4.  **Equation for $P$**: The irreducible polarizability is a bubble of two Green's function lines, with the interaction vertex dressed by $\Gamma$.
    $$ P(1,2) = -\mathrm{i} \, G(1,3)G(4,1^+)\Gamma(3,4;2) $$
    The factor of $-\mathrm{i}$ arises from the fermionic loop in the [diagrammatic expansion](@entry_id:139147).

5.  **Equation for $\Gamma$**: The [vertex function](@entry_id:145137) itself satisfies a complex integral equation.
    $$ \Gamma(1,2;3) = \delta(1,2)\delta(1,3) + \frac{\delta \Sigma(1,2)}{\delta G(4,5)}G(4,6)G(7,5)\Gamma(6,7;3) $$
    The first term, $\delta(1,2)\delta(1,3)$, is the bare vertex, representing a simple point-like interaction. The integral term, whose kernel is the functional derivative $\delta\Sigma/\delta G$, represents all higher-order interaction effects.

The derivation of this system relies on [functional calculus](@entry_id:138358) [@problem_id:2785443]. By introducing a fictitious external potential $\phi$ that couples to the density, one can define $\Gamma$ as the response of the inverse Green's function to this potential, $\Gamma(1,2;3) = -\delta G^{-1}(1,2) / \delta\phi(3)$. Applying the [chain rule](@entry_id:147422), $\delta\Sigma/\delta\phi = (\delta\Sigma/\delta G)(\delta G/\delta\phi)$, leads directly to the integral equation for $\Gamma$. While formally exact, this system of equations is computationally intractable due to the final equation for $\Gamma$, which relates the vertex to a functional derivative of the self-energy that, in turn, depends on $\Gamma$. This creates an infinite hierarchy. To make progress, one must introduce an approximation to "close" the loop, and the most common starting point is to approximate the [vertex function](@entry_id:145137) $\Gamma$ [@problem_id:2785469].

### The GW Approximation

The most fundamental and widely used closure for Hedin's equations is the **GW approximation** (GWA). It is obtained by neglecting all explicit [vertex corrections](@entry_id:146982), which amounts to replacing the full [vertex function](@entry_id:145137) $\Gamma$ with its zeroth-order term, the bare vertex [@problem_id:2930154]:
$$ \Gamma(1,2;3) \approx \Gamma_0(1,2;3) = \delta(1,2)\delta(1,3) $$
This single, powerful approximation simplifies the entire Hedin's pentagon.

#### Structure of the GW Self-Energy and Screening

Substituting $\Gamma=1$ into the equations for $P$ and $\Sigma$ yields their well-known approximate forms [@problem_id:2930154]:

*   The irreducible polarizability $P$ becomes the **bare polarization bubble**, which defines the **Random Phase Approximation (RPA)**.
    $$ P(1,2) \approx -\mathrm{i} \, G(1,3)G(4,1^+)\delta(3,4)\delta(3,2) = -\mathrm{i} \, G(1,2)G(2,1^+) $$
    Diagrammatically, this approximation for the screening corresponds to summing all **ring diagrams** (or bubble diagrams) to infinite order [@problem_id:2785472]. This captures the long-range collective response of the electron gas but neglects [short-range correlations](@entry_id:158693) and attractive electron-hole interactions.

*   The [self-energy](@entry_id:145608) $\Sigma$ simplifies to a [direct product](@entry_id:143046) of the Green's function and the [screened interaction](@entry_id:136395).
    $$ \Sigma(1,2) \approx \mathrm{i} \, G(1,3)W(1^+,4)\delta(3,2)\delta(3,4) = \mathrm{i} \, G(1,2)W(1^+,2) $$
    This expression, $\Sigma = \mathrm{i}GW$, gives the approximation its name.

#### Physical Interpretation of $\Sigma = \mathrm{i}GW$

The structure of the GW self-energy, a product in the [real-space](@entry_id:754128) and time domain, has profound physical implications [@problem_id:2464632]. By the [convolution theorem](@entry_id:143495), a product of two functions in the time domain corresponds to a convolution of their Fourier transforms in the frequency domain. Thus, the frequency-dependent [self-energy](@entry_id:145608) is given by:
$$ \Sigma(\mathbf{k}, \omega) \propto \mathrm{i} \int \frac{d\omega'}{2\pi} \int \frac{d^3\mathbf{q}}{(2\pi)^3} G(\mathbf{k}-\mathbf{q}, \omega-\omega') W(\mathbf{q}, \omega') $$
This expression provides a beautiful physical picture [@problem_id:2930171]: the self-energy of an electron (or hole) with energy $\omega$ and momentum $\mathbf{k}$ is a sum over all possible processes where it emits or absorbs an excitation of the medium (a plasmon or an electron-hole pair, described by $W$) with energy $\omega'$ and momentum $\mathbf{q}$. The particle is "dressed" by a cloud of virtual polarizations.

This dynamical nature contrasts sharply with simpler theories:
*   **Hartree-Fock Theory**: Here, the exchange self-energy is $\Sigma_x = -\mathrm{i}Gv$, involving the *bare*, instantaneous Coulomb interaction $v$. This leads to a real and energy-independent self-energy that cannot describe correlation effects or finite quasiparticle lifetimes.
*   **Static Screening (COHSEX)**: If one approximates the screening as static, using $W(\omega=0)$, the resulting self-energy is also real and energy-independent. It accounts for an average screening effect but misses all [dynamical correlation](@entry_id:171647).

The key feature of the GWA is its use of a **dynamically [screened interaction](@entry_id:136395)** $W(\omega)$. This makes the [self-energy](@entry_id:145608) $\Sigma(\omega)$ both **energy-dependent** and **complex**.
*   The **real part**, $\mathrm{Re}[\Sigma(\omega)]$, describes the energy shift of the single-particle levels, leading to the renormalized [quasiparticle energies](@entry_id:173936).
*   The **imaginary part**, $\mathrm{Im}[\Sigma(\omega)]$, is non-zero for energies away from the Fermi level. It gives the quasiparticle an inverse lifetime ($\tau^{-1} \propto |\mathrm{Im}[\Sigma]|$), representing the possibility of decay into more complex excitations. The rich structure in $W(\omega)$, such as [plasmon](@entry_id:138021) poles, also gives rise to **satellite peaks** in the [spectral function](@entry_id:147628), a hallmark of many-body correlation.

The GWA is most justifiable in systems where screening is effective and correlations are relatively weak, such as in high-density electron gases, simple metals, and sp-bonded semiconductors. It is less reliable in systems with strong localization (d- and f-electron materials), low dimensionality, or strong excitonic effects, where [vertex corrections](@entry_id:146982) become crucial [@problem_id:2930154].

### Flavors of GW: Levels of Self-Consistency

The equations of the GW approximation still form a coupled set ($G$ depends on $\Sigma$, which depends on $G$ and $W$, which in turn depends on $G$). In practice, various computational schemes, or "flavors" of GW, have been developed based on different levels of self-consistency in solving these equations [@problem_id:2785455, 2785447].

*   **$G_0W_0$**: This is a non-self-consistent, "one-shot" approach, most commonly performed on top of a Density Functional Theory (DFT) calculation. One starts with the Kohn-Sham orbitals and eigenvalues to build a non-interacting Green's function $G_0$. This is used to compute the RPA screening $W_0$ once. The [self-energy](@entry_id:145608) is then evaluated as $\Sigma = \mathrm{i}G_0W_0$, and [quasiparticle energies](@entry_id:173936) are obtained as a first-order correction to the initial Kohn-Sham energies. While computationally efficient, this view of $G_0W_0$ as a simple perturbative correction is fraught with limitations [@problem_id:2464575]: the result depends on the starting DFT functional, the "correction" is not guaranteed to be small, and errors in the DFT starting point (like underestimated [band gaps](@entry_id:191975)) can lead to overscreening in $W_0$, which propagates to the final result.

*   **$GW_0$ (Eigenvalue Self-Consistency)**: This scheme introduces partial self-consistency by updating the Green's function $G$ while keeping the [screened interaction](@entry_id:136395) fixed at the $W_0$ level. The [quasiparticle energies](@entry_id:173936) that are poles of $G$ are updated iteratively until they converge. This often improves results over $G_0W_0$ by ensuring internal consistency of the [quasiparticle energies](@entry_id:173936).

*   **Fully Self-Consistent GW (scGW)**: Here, the full set of GW equations for $G$, $P$, $W$, and $\Sigma$ are iterated until all quantities are mutually consistent. While theoretically more rigorous, this approach is computationally demanding and does not always improve upon simpler schemes, partly due to the neglect of [vertex corrections](@entry_id:146982).

*   **Quasiparticle Self-Consistent GW (qsGW)**: This is a popular alternative to scGW. Instead of iterating the fully dynamical quantities, it seeks to find an optimal static, Hermitian effective Hamiltonian $H_{\mathrm{eff}}$ whose single-particle Green's function $G_0$ is the "best" possible starting point for a subsequent $G_0W_0$ calculation. At each step, a dynamical $\Sigma(\omega)$ is calculated and used to construct an updated static $H_{\mathrm{eff}}$, which is then iterated to [self-consistency](@entry_id:160889).

### Conservation Laws, Sum Rules, and the Ward Identity

A crucial test for any [many-body theory](@entry_id:169452) is its adherence to fundamental conservation laws, such as the conservation of charge, momentum, and energy. These laws manifest as **sum rules**, which are exact integral relations that the system's response functions must satisfy.

For example, the **[compressibility sum rule](@entry_id:151722)** relates the static, long-wavelength limit of the reducible polarization to the thermodynamic [compressibility](@entry_id:144559) $\kappa$ of the system [@problem_id:1220221]:
$$ \kappa = \frac{1}{n^2} P(\mathbf{q}\to 0, \omega=0) $$
Another fundamental constraint is the **[f-sum rule](@entry_id:147775)**, which for the charge response is a direct consequence of particle number conservation and the commutation relations of quantum mechanics. It relates the first frequency moment of the imaginary part of the polarizability (or the dynamical structure factor) to the particle density and mass [@problem_id:1220204, 1220180]:
$$ \int_{-\infty}^{\infty} d\omega \, \omega \, \mathrm{Im}[P(\mathbf{q},\omega)] = \pi n \frac{q^2}{m} $$
Approximations that satisfy these sum rules are known as **[conserving approximations](@entry_id:139611)**.

In the language of [many-body theory](@entry_id:169452), local charge conservation is formally guaranteed by the **Ward-Takahashi Identity** (WTI), which connects the [vertex function](@entry_id:145137) $\Gamma$ to the self-energy $\Sigma$. In the limit of long wavelengths ($\mathbf{q}\to 0$) and low frequencies ($\Omega\to 0$), this identity takes the form [@problem_id:2486733, 2930176]:
$$ \Gamma \approx 1 - \frac{\partial \Sigma}{\partial \omega} $$
This identity reveals a critical issue with the standard GW approximation [@problem_id:2930176]. By setting $\Gamma=1$, the approximation is only consistent with the WTI if $\partial\Sigma/\partial\omega = 0$. However, the GW self-energy is inherently frequency-dependent. This inconsistency means that simple GW schemes, particularly non-self-consistent ones like $G_0W_0$, violate the Ward identity and are thus not strictly [conserving approximations](@entry_id:139611).

This apparent paradox is resolved by the concept of **$\Phi$-derivable approximations** [@problem_id:2486733]. Theories where the self-energy is obtained as the functional derivative of a scalar functional $\Phi[G]$ (i.e., $\Sigma = \delta\Phi/\delta G$) are guaranteed to be conserving if solved to full [self-consistency](@entry_id:160889). The fully self-consistent GW (scGW) scheme is $\Phi$-derivable and thus satisfies the sum rules. In contrast, one-shot $G_0W_0$ is not, explaining its potential for unphysical results. The RPA polarization, being the result of a self-consistent summation of ring diagrams, remarkably satisfies the [f-sum rule](@entry_id:147775) on its own [@problem_id:1220180].

### Beyond GW: Introducing the Vertex Correction

The primary limitation of the GW approximation is its neglect of the [vertex function](@entry_id:145137) $\Gamma$. This [vertex correction](@entry_id:137909) accounts for repeated scattering between the electron and the hole, an effect entirely absent in the RPA description of screening. Incorporating the vertex is essential for describing phenomena dominated by strong electron-hole interactions, most notably **[excitons](@entry_id:147299)**—[bound states](@entry_id:136502) of an electron-hole pair.

The theoretical framework for describing [excitons](@entry_id:147299) is the **Bethe-Salpeter Equation** (BSE), an [integral equation](@entry_id:165305) for the two-particle [correlation function](@entry_id:137198). The BSE can be derived directly from Hedin's formalism [@problem_id:1220209]. For the reducible polarizability $\chi$, which describes the response to an external potential, the BSE takes the form:
$$ \chi = \chi_0 + \chi_0 K \chi $$
where $\chi_0 = -iGG$ is the non-interacting response function (a bubble of two full Green's functions) and $K$ is the BSE kernel, representing the effective electron-hole interaction. The kernel is formally related to the bare interaction and the [self-energy](@entry_id:145608) via $K = v + \mathrm{i}(\delta\Sigma/\delta G)$.

For practical calculations, particularly for describing optical excitons in materials, the BSE kernel $K$ is typically approximated by two terms [@problem_id:2985478]:
$$ K \approx K^d + K^x = -W(\omega=0) + v $$
*   $K^d = -W(\omega=0)$ is the **attractive, statically screened direct interaction**. This term describes the Coulomb attraction between the electron and the hole, screened by the other electrons in the system. It is responsible for the binding of the exciton.
*   $K^x = v$ is the **repulsive, bare [exchange interaction](@entry_id:140006)**. This short-range term arises from the Pauli exclusion principle and is responsible for the energy splitting between singlet and triplet excitons. It is unscreened because it involves the virtual [annihilation](@entry_id:159364) and recreation of the [electron-hole pair](@entry_id:142506), a process too fast for the surrounding medium to respond.

This GW-BSE approach, which involves first calculating [quasiparticle energies](@entry_id:173936) using GW and then solving the BSE with the kernel $K = v-W$, has become the state-of-the-art method for computing [optical spectra](@entry_id:185632) of a wide range of materials.

Finally, it is crucial to recognize the interplay between [vertex corrections](@entry_id:146982) to the polarization $P$ and the self-energy $\Sigma$ [@problem_id:2486722].
*   Including the vertex in $P$ (as in the BSE) introduces electron-hole attraction, which reduces screening (i.e., lowers the dielectric constant $\varepsilon$). A less-[screened interaction](@entry_id:136395) $W$ in the GW [self-energy](@entry_id:145608) tends to increase the quasiparticle band gap.
*   Including the vertex in $\Sigma$ itself ($\Sigma = \mathrm{i}GW\Gamma$) tends to have the opposite effect, partially cancelling the gap-opening effect.

A fully conserving theory, which satisfies the Ward identity, must include these corrections consistently in both quantities. The minimal fix to restore conservation in the GW approximation is to use the vertex derived from the Ward identity itself, $\Gamma_{\mathrm{WI}} = 1 - \partial\Sigma/\partial\omega$, in the calculation of response properties [@problem_id:2930176]. This insight paves the way for systematic improvements beyond the standard GW approximation, moving the theory closer to an exact description of the [many-electron problem](@entry_id:165546).