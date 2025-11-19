## Introduction
In the realm of condensed matter physics, our understanding of conventional metals is built upon the elegant and powerful framework of Landau's Fermi liquid theory. This theory successfully describes a vast range of materials by positing that interacting electrons behave as weakly-interacting "quasiparticles." However, a growing class of [strongly correlated materials](@entry_id:198946), including the high-temperature [cuprate superconductors](@entry_id:146531) in their "[strange metal](@entry_id:138796)" phase, exhibit anomalous properties that starkly defy this paradigm. Their resistivity is linear with temperature, not quadratic, and spectroscopic probes reveal [electronic excitations](@entry_id:190531) that are not long-lived. These materials exemplify non-Fermi-liquid behavior, presenting a fundamental challenge to [condensed matter theory](@entry_id:141958).

This article addresses this knowledge gap by providing a systematic exploration of non-Fermi liquids, with a focus on the influential marginal Fermi liquid (MFL) model. It aims to equip you with the theoretical tools to understand why the quasiparticle concept fails and what new physics emerges in its absence. Across three chapters, you will gain a comprehensive understanding of this frontier of physics.

The first chapter, "Principles and Mechanisms," establishes the theoretical baseline by reviewing Landau Fermi liquid theory, developing a general criterion for the quasiparticle's demise, and dissecting the MFL model and its hallmark concept of Planckian dissipation. The second chapter, "Applications and Interdisciplinary Connections," bridges theory with experiment, detailing the spectroscopic and transport signatures of non-Fermi liquids and their microscopic origins in [quantum criticality](@entry_id:143927) and electronic fractionalization. Finally, the "Hands-On Practices" section provides targeted problems to solidify your grasp of these advanced concepts. We begin our investigation by examining the foundational principles of the state from which non-Fermi liquids so radically depart: the Landau Fermi liquid.

## Principles and Mechanisms

Having introduced the broad landscape of non-Fermi-liquid behavior, we now turn to a detailed examination of the principles and mechanisms that govern these exotic metallic states. Our inquiry will begin by firmly establishing the theoretical baseline: Landau's Fermi liquid theory. By understanding the precise nature of a Landau quasiparticle, we can then appreciate the profound consequences of its demise. We will develop a general criterion for the breakdown of the quasiparticle concept and explore in detail the properties of a paradigmatic example, the marginal Fermi liquid. This will lead us to the phenomenological hallmarks of such systems, including the concept of Planckian dissipation. Finally, we will investigate the underlying physical mechanisms, such as [quantum criticality](@entry_id:143927), and the sophisticated theoretical frameworks required to describe phenomena like transport and conservation laws in a world without well-defined quasiparticles.

### The Landau Fermi Liquid Paradigm: Quasiparticles and Their Properties

The foundation of our understanding of conventional metals is Landau's Fermi liquid theory. This remarkably successful theory posits that even in the presence of strong [electron-electron interactions](@entry_id:139900), the low-energy elementary excitations of the system behave like particles. These are not the original, "bare" electrons, but rather **Landau quasiparticles**: dressed entities whose properties are renormalized by the surrounding cloud of interactions.

The modern language for describing these excitations is that of many-body Green's functions. The single-particle retarded Green's function, $G^{\mathrm{R}}(\mathbf{k}, \omega)$, describes the propagation of a particle with momentum $\mathbf{k}$ and energy $\omega$. It obeys Dyson's equation:
$$
G^{\mathrm{R}}(\mathbf{k}, \omega) = \left[\omega - \xi_{\mathbf{k}} - \Sigma^{\mathrm{R}}(\mathbf{k}, \omega)\right]^{-1}
$$
where $\xi_{\mathbf{k}} = \varepsilon_{\mathbf{k}} - \mu$ is the bare electron dispersion relative to the chemical potential $\mu$, and $\Sigma^{\mathrm{R}}(\mathbf{k}, \omega)$ is the **[self-energy](@entry_id:145608)**, which encapsulates all the effects of interactions.

A stable, well-defined quasiparticle corresponds to a [simple pole](@entry_id:164416) in the Green's function. Near the Fermi surface, where low-energy physics unfolds, we can expand the inverse Green's function for small $\omega$ and for $\mathbf{k}$ near the Fermi momentum $\mathbf{k}_{\mathrm{F}}$. A quasiparticle pole exists at an energy $E_{\mathbf{k}}$ that satisfies $E_{\mathbf{k}} - \xi_{\mathbf{k}} - \mathrm{Re}\,\Sigma^{\mathrm{R}}(\mathbf{k}, E_{\mathbf{k}}) = 0$. Close to this pole, the Green's function takes the approximate form:
$$
G^{\mathrm{R}}(\mathbf{k}, \omega) \approx \frac{Z(\mathbf{k})}{\omega - E_{\mathbf{k}} + i\Gamma_{\mathbf{k}}}
$$
The quantity $Z(\mathbf{k})$ is the **quasiparticle residue** or weight. It represents the overlap between the physical quasiparticle state and a bare electron state. It is given by [@problem_id:3007625]:
$$
Z(\mathbf{k}_{\mathrm{F}}) = \left[1 - \left.\frac{\partial \mathrm{Re}\,\Sigma^{\mathrm{R}}(\mathbf{k}_{\mathrm{F}}, \omega)}{\partial\omega}\right|_{\omega=0}\right]^{-1}
$$
In a Fermi liquid, interactions ensure that $0  Z  1$. The remaining [spectral weight](@entry_id:144751), $1-Z$, is transferred to an incoherent background of multi-particle excitations. The physical meaning of $Z$ is profound: at zero temperature, the momentum distribution function $n(\mathbf{k}) = \langle c_{\mathbf{k}}^{\dagger}c_{\mathbf{k}}\rangle$ exhibits a discontinuous jump of magnitude $Z$ at the Fermi surface. This jump is the definitive signature of a Fermi liquid ground state [@problem_id:3007625].

The [quasiparticle lifetime](@entry_id:145453), $\tau$, is given by the inverse of its decay rate, $\Gamma_{\mathbf{k}}$. For a Fermi liquid, the decay rate is severely restricted by energy conservation and the Pauli exclusion principle, which limits the available phase space for scattering processes. A hallmark calculation using Fermi's Golden Rule for [two-body scattering](@entry_id:144358) reveals that for a quasiparticle of energy $\omega$ above the Fermi level at temperature $T$, the inverse lifetime has a characteristic quadratic dependence [@problem_id:3007677]:
$$
\tau^{-1}(\omega, T) \propto \omega^2 + (\pi T)^2
$$
This result is of paramount importance. It shows that as a quasiparticle's energy $\omega$ and the temperature $T$ approach zero, its lifetime becomes arbitrarily long ($\tau \to \infty$). The ratio of the decay rate to the energy, $\tau^{-1}/\omega \propto \omega$, vanishes, confirming that the quasiparticle is a well-defined, coherent excitation near the Fermi surface. This stability is the essence of the Landau Fermi liquid.

### The Breakdown of the Quasiparticle: A General Criterion

The concept of a non-Fermi liquid emerges when the Landau quasiparticle ceases to be a valid low-energy excitation. This occurs when the scattering rate becomes comparable to the excitation energy, causing the quasiparticle pole to blur and merge with the incoherent continuum. The key to understanding this breakdown lies in the low-frequency behavior of the self-energy, $\Sigma^{\mathrm{R}}(\omega)$.

Let us assume that, at zero temperature, the imaginary part of the self-energy on the Fermi surface has a general power-law form for small frequencies:
$$
\mathrm{Im}\,\Sigma^{\mathrm{R}}(\omega) = -C |\omega|^{\alpha} \quad (C > 0, \alpha > 0)
$$
The standard Fermi liquid corresponds to $\alpha=2$. What happens for other values of $\alpha$? The analyticity of the Green's function, rooted in causality, dictates that the real and imaginary parts of the [self-energy](@entry_id:145608) are not independent but are related by the **Kramers-Kronig relations** [@problem_id:3007630]. Using these relations, we can determine the effect of this assumed form of $\mathrm{Im}\,\Sigma^{\mathrm{R}}(\omega)$ on the real part, and specifically on its derivative at $\omega=0$, which determines the quasiparticle residue $Z$.

A detailed analysis [@problem_id:3007652] shows that the derivative $\partial \mathrm{Re}\,\Sigma^{\mathrm{R}}/\partial\omega$ at $\omega=0$ depends crucially on $\alpha$:
- For $\alpha > 1$, the derivative is finite, resulting in a finite, non-zero quasiparticle residue $Z$. The Fermi liquid case ($\alpha=2$) falls into this category.
- For $\alpha \le 1$, the derivative diverges, $\partial \mathrm{Re}\,\Sigma^{\mathrm{R}}/\partial\omega |_{\omega=0} \to \infty$.

Recalling the definition $Z = [1 - \partial_{\omega} \mathrm{Re}\,\Sigma^{\mathrm{R}}]^{-1}$, a diverging derivative immediately implies that the quasiparticle residue vanishes:
$$
Z = 0 \quad \text{for} \quad \alpha \le 1
$$
This is the general criterion for the destruction of the Landau quasiparticle. The physical consequence is drastic: since the jump in the [momentum distribution](@entry_id:162113) $n(\mathbf{k})$ at the Fermi surface is equal to $Z$, a vanishing residue implies that this discontinuity disappears. The momentum distribution becomes a continuous function across the Fermi surface, although its slope may be singular. The sharp distinction between occupied and unoccupied states, which defines the Fermi sea of a conventional metal, is lost. This is the defining characteristic of a non-Fermi-liquid ground state.

### Case Study: The Marginal Fermi Liquid

The case $\alpha=1$ represents a particularly important class of non-Fermi liquids, known as **marginal Fermi liquids (MFLs)**. The term "marginal" signifies that they lie at the boundary of stability for the quasiparticle. This behavior is captured by a phenomenological [self-energy](@entry_id:145608) that has been proposed to describe materials like the high-temperature [cuprate superconductors](@entry_id:146531) in their "[strange metal](@entry_id:138796)" phase. At zero temperature, its form is [@problem_id:3007647] [@problem_id:3007625]:
$$
\Sigma^{\mathrm{R}}(\omega) = \lambda \omega \ln\left(\frac{\omega_c}{|\omega|}\right) - i \lambda \frac{\pi}{2}|\omega|
$$
Here, $\lambda$ is a dimensionless coupling constant and $\omega_c$ is a high-[energy cutoff](@entry_id:177594). The imaginary part is linear in $|\omega|$, corresponding to $\alpha=1$. The real part, with its characteristic $\omega \ln|\omega|$ form, is not arbitrary; it is precisely what is required by the Kramers-Kronig relations for a particle-hole symmetric system with a linear-in-$|\omega|$ imaginary part [@problem_id:3007630].

With this form of the self-energy, we can directly compute the quantities that signal the breakdown of Fermi liquid theory. The derivative of the real part is [@problem_id:3007647]:
$$
\frac{\partial \Sigma'(\omega)}{\partial \omega} = \lambda \left[ \ln\left(\frac{\omega_c}{|\omega|}\right) - 1 \right]
$$
As $\omega \to 0$, this derivative diverges logarithmically to $+\infty$. This confirms that at the Fermi energy, the quasiparticle residue is exactly zero, $Z=0$. The quasiparticle is "marginally" stable, with its [spectral weight](@entry_id:144751) vanishing precisely at the Fermi surface. We can also define a frequency-dependent residue $Z(\omega) = [1 - \partial\Sigma'(\omega)/\partial\omega]^{-1}$, which shows how the quasiparticle character is recovered as one moves away from the Fermi level, only to vanish logarithmically upon approach [@problem_id:3007647].

### Phenomenological Hallmarks: Planckian Dissipation and Anomalous Transport

The unique [self-energy](@entry_id:145608) of a marginal Fermi liquid leads to striking phenomenological consequences, particularly in its scattering properties. At finite temperature $T$ and for low frequencies ($\omega \ll T$), the relevant energy scale is set by temperature. The MFL hypothesis, which assumes electrons are coupled to a broad, [scale-invariant spectrum](@entry_id:158962) of fluctuations, leads to an imaginary part of the self-energy that is linear in temperature [@problem_id:3007602]:
$$
\Sigma''(\omega \to 0, T) \propto -\lambda T
$$
The quasiparticle scattering rate is $\tau^{-1} = -2 \Sigma''$. This immediately implies a scattering rate that is linear in temperature:
$$
\frac{1}{\tau} \approx \pi \lambda \frac{k_B T}{\hbar}
$$
where we have restored the physical constants. This linear-in-temperature scattering rate is a hallmark of MFLs and many [strange metals](@entry_id:141452). It stands in stark contrast to the $T^2$ dependence in a Fermi liquid.

This behavior is often referred to as **Planckian dissipation**. The term is motivated by a heuristic argument based on the uncertainty principle, $\Delta E \Delta t \gtrsim \hbar$. If we identify the energy uncertainty $\Delta E$ with the thermal energy $k_B T$ and the time uncertainty $\Delta t$ with the [scattering time](@entry_id:272979) $\tau$, we arrive at an upper bound on the scattering rate: $1/\tau \lesssim k_B T / \hbar$ [@problem_id:3007653]. The linear-in-$T$ scattering rate of an MFL appears to saturate this putative bound, suggesting that the system is dissipating energy as fast as quantum mechanics allows. Whereas the $T^2$ rate of a Fermi liquid is parametrically smaller than this bound at low temperatures, the MFL operates at this limit, signifying a state of maximal incoherence [@problem_id:3007653].

If this [single-particle scattering](@entry_id:136491) time also governs momentum relaxation, it leads directly to a DC electrical resistivity that is linear in temperature, $\rho(T) \propto T$. This anomalous temperature dependence is one of the most famous signatures of strange-metal behavior and is naturally explained within the MFL framework [@problem_id:3007653].

### Mechanisms for Non-Fermi-Liquid Behavior

What physical mechanisms can give rise to a [self-energy](@entry_id:145608) that destroys the quasiparticle? Two major themes in modern [condensed matter](@entry_id:747660) physics provide answers: [quantum criticality](@entry_id:143927) and the existence of novel [phases of matter](@entry_id:196677) with [topological order](@entry_id:147345).

#### Quantum Criticality

A primary mechanism for generating non-Fermi-liquid behavior is a **quantum critical point (QCP)**—a [continuous phase transition](@entry_id:144786) at zero temperature, driven by a non-thermal parameter like pressure or magnetic field. Near a QCP, the system is filled with long-range, low-energy quantum fluctuations of an order parameter (e.g., antiferromagnetic [spin fluctuations](@entry_id:141847)). The coupling of these critical bosonic fluctuations to the electrons on a Fermi surface can mediate an intensely strong and singular interaction.

Consider a model where a metallic Fermi surface is coupled to an overdamped critical boson. The effective interaction mediated by this boson is long-ranged in both space and time. A [renormalization group](@entry_id:147717) analysis of such a system reveals that the dynamics are governed by a **[dynamic critical exponent](@entry_id:137451)** $z$, which relates the scaling of time and space. For a generic metallic QCP in dimensions $d \ge 2$, the strong damping of the bosons by particle-hole pairs in the Fermi sea (Landau damping) leads to $z=3$ [@problem_id:3007651]. This means that frequency scales as momentum cubed, $\omega \sim q^3$, a much slower dynamic than in a vacuum ($z=1$) or at a conventional critical point ($z=2$). This singular dynamic is a direct source of non-Fermi-liquid behavior in the [electron self-energy](@entry_id:148523).

Furthermore, the presence of a Fermi surface introduces a fundamental anisotropy into the scaling. Only momentum components perpendicular to the Fermi surface are strongly affected by the critical scaling. The tangential directions do not participate, leading to a phenomenon known as **[hyperscaling violation](@entry_id:148457)**, characterized by an exponent $\theta = d-1$ [@problem_id:3007651]. This theoretical framework provides a concrete pathway to non-Fermi-liquid states.

#### Conservation Laws and Transport in the Absence of Quasiparticles

The breakdown of the quasiparticle picture poses a fundamental challenge for describing [transport properties](@entry_id:203130). The standard Drude and Boltzmann transport theories are built upon the premise of well-defined quasiparticles with a [mean free path](@entry_id:139563). How can a metal conduct electricity if there are no long-lived charge carriers?

The answer lies in focusing on the true [conserved quantities](@entry_id:148503) of the system. In a translationally invariant system, the total momentum $\mathbf{P}$ is conserved. Even without quasiparticles, $\mathbf{P}$ is a well-defined operator. A finite DC conductivity requires a mechanism for momentum to relax, such as scattering off impurities or Umklapp scattering from the lattice.

The **memory matrix formalism** provides a rigorous framework for calculating transport coefficients in this regime [@problem_id:3007620]. It identifies the slowest decaying variables in the system—in this case, the total momentum $\mathbf{P}$—and projects the dynamics onto this slow subspace. The DC conductivity can then be expressed in terms of two quantities: a static susceptibility $\chi_{JP}$ that measures the overlap between the current operator $\mathbf{J}$ and the [momentum operator](@entry_id:151743) $\mathbf{P}$, and a memory [matrix element](@entry_id:136260) $M_{PP}(0)$ that quantifies the rate at which momentum is relaxed by the symmetry-breaking potential. The resulting expression is [@problem_id:3007620]:
$$
\sigma_{\mathrm{dc}} = \frac{\chi_{JP}^2}{M_{PP}(0)}
$$
This powerful formula demonstrates that conductivity is fundamentally a balance between the system's capacity to carry current via its [conserved momentum](@entry_id:177921) and the rate at which that momentum is degraded. It allows for the calculation of resistivity even in a "bad metal" where the quasiparticle concept has completely failed.

Finally, we must consider the fate of another fundamental organizing principle, **Luttinger's theorem**, which relates the volume of the Fermi surface to the total electron density. Is this theorem also invalidated in a non-Fermi liquid? The answer depends on the nature of the state. For a marginal Fermi liquid, which does not break any symmetries or possess intrinsic [topological order](@entry_id:147345), Luttinger's theorem remains valid [@problem_id:3007617]. The volume enclosed by the surface of singularities in [momentum space](@entry_id:148936) (where the real part of the inverse Green's function vanishes at zero frequency) still correctly counts the total charge density. The theorem can even be generalized to systems with zeros in their Green's function, where the relevant quantity is the volume of [k-space](@entry_id:142033) where $G(\mathbf{k}, 0) > 0$ [@problem_id:3007617].

However, in more exotic states, such as a **fractionalized Fermi liquid (FL\*)**, which possess [emergent gauge fields](@entry_id:146708) and [topological order](@entry_id:147345), the theorem is violated. In an FL\*, the electron fractionalizes into constituent parts, and the Fermi surface is formed by emergent neutral fermions. This Fermi surface encloses a volume that does not correspond to the total electron density, and the discrepancy is a signature of the underlying topological nature of the phase [@problem_id:3007617]. This highlights that "non-Fermi liquid" is not a single category, but a vast territory of new metallic states, each with its own unique principles and governing mechanisms.