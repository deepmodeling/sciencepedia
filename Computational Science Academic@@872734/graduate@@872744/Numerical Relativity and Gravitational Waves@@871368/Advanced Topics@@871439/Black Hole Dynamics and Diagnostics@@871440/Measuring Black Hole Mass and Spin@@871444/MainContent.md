## Introduction
The measurement of mass and spin—the two parameters that, according to the [no-hair theorem](@entry_id:201738), fully characterize a stationary black hole—is a foundational task in [numerical relativity](@entry_id:140327) and [gravitational wave astronomy](@entry_id:144334). While these properties are clearly defined for an isolated black hole, their measurement in the dynamic environment of a binary merger presents significant theoretical and computational challenges. This article addresses this knowledge gap by providing a comprehensive guide to defining and measuring [black hole mass and spin](@entry_id:746860), from first principles to practical application.

You will begin in "Principles and Mechanisms" by exploring the fundamental properties of Kerr black holes and the laws that govern them, before confronting the complexities of dynamical spacetimes and the quasi-local frameworks required to track evolving black holes. Next, "Applications and Interdisciplinary Connections" will demonstrate how these measurements are used to decode gravitational wave signals, test the foundations of General Relativity, and forge connections with astrophysics and cosmology. Finally, "Hands-On Practices" will provide practical exercises to solidify your understanding and apply these advanced concepts.

## Principles and Mechanisms

The measurement of mass and angular momentum—the two parameters that, according to the [no-hair theorem](@entry_id:201738), uniquely define a stationary, vacuum black hole—is a cornerstone of numerical relativity and gravitational wave astrophysics. While these properties are unambiguously defined for an isolated, stationary Kerr black hole, their characterization in the dynamical context of a binary coalescence presents profound theoretical and practical challenges. This chapter elucidates the fundamental principles and mechanisms for defining and measuring [black hole mass and spin](@entry_id:746860), progressing from the idealized stationary case to the complexities of dynamical spacetimes and their observational signatures.

### Characterizing the Final State: Mass and Spin of a Kerr Black Hole

The endpoint of a [binary black hole merger](@entry_id:159223), after all [gravitational radiation](@entry_id:266024) has propagated to infinity, is expected to be a stationary, axisymmetric Kerr black hole. This final state is described by two parameters: the total mass, $M$, and the [total angular momentum](@entry_id:155748), $J$. From these, a dimensionless spin parameter, $\chi$, is defined in geometric units ($G=c=1$) as:

$$ \chi = \frac{J}{M^2} $$

The value of $\chi$ is constrained to the range $[0, 1]$, where $\chi=0$ corresponds to a non-rotating Schwarzschild black hole and $\chi=1$ represents a maximally rotating Kerr black hole. As a dimensionless ratio, $\chi$ is invariant under a global rescaling of units. For instance, if all length and time scales are rescaled by a factor $\lambda$, mass ($[M] = [L]$) scales as $M \to \lambda M$ and angular momentum ($[J] = [L]^2$) scales as $J \to \lambda^2 J$, leaving $\chi$ unchanged. This makes it a universal descriptor of a black hole's rotational state [@problem_id:3479628].

A black hole's total mass-energy $M$ can be conceptually decomposed. A fundamental component is the **[irreducible mass](@entry_id:160861)**, $M_{\text{irr}}$, which is related to the surface area $A$ of the event horizon by the simple relation:

$$ M_{\text{irr}} = \sqrt{\frac{A}{16\pi}} $$

The [irreducible mass](@entry_id:160861) represents the portion of the black hole's energy that cannot be extracted, even in principle, by processes like the Penrose process. The remaining energy is stored as [rotational energy](@entry_id:160662). To see this connection, one can derive the horizon area directly from the Kerr metric. The event horizon is located at the [radial coordinate](@entry_id:165186) $r_+ = M + \sqrt{M^2 - a^2}$, where $a = J/M$ is the specific angular momentum. The area of this surface is found to be $A = 4\pi(r_+^2 + a^2)$. By substituting the expression for $r_+$ and using the definition $\chi = a/M$, the [irreducible mass](@entry_id:160861) can be expressed directly in terms of $M$ and $\chi$ [@problem_id:3479607]:

$$ M_{\text{irr}} = M \sqrt{\frac{1+\sqrt{1-\chi^{2}}}{2}} $$

This equation quantifies the relationship between total mass, [irreducible mass](@entry_id:160861), and rotational energy. For a non-rotating black hole ($\chi=0$), $M_{\text{irr}} = M$. For a maximally [rotating black hole](@entry_id:261667) ($\chi=1$), $M_{\text{irr}} = M/\sqrt{2}$, meaning up to $(1 - 1/\sqrt{2}) \approx 29\%$ of the total mass-energy is stored in its rotation and is, in principle, extractable.

The interplay between mass, spin, and area is elegantly encapsulated in the **first law of [black hole mechanics](@entry_id:264759)**:

$$ dM = \frac{\kappa}{8\pi} dA + \Omega_H dJ $$

Here, $dM$, $dA$, and $dJ$ are the infinitesimal changes in mass, area, and angular momentum, respectively; $\kappa$ is the surface gravity (which is constant over the horizon); and $\Omega_H$ is the angular velocity of the horizon. This law is analogous to the first law of thermodynamics, with $M$ playing the role of energy, $A/(8\pi)$ playing the role of entropy (up to a factor), and $\kappa$ playing the role of temperature. The term $\Omega_H dJ$ represents the work done on the black hole by [adding angular momentum](@entry_id:181987).

We can apply this law to understand how a black hole's spin evolves when it accretes matter. Consider a small particle with energy $E$ and angular momentum $L$ being captured by the black hole, such that we can identify $dM=E$ and $dJ=L$. The change in spin, $d\chi$, is found by differentiating its definition: $d\chi = dJ/M^2 - (2J/M^3)dM$. Substituting the particle's properties, we get $d\chi = L/M^2 - (2\chi/M)E$. In the special case of a **reversible capture**, where the process is infinitely slow and adds no entropy, the horizon area does not change ($dA=0$). The first law then implies a strict relation between the absorbed energy and angular momentum: $E = \Omega_H L$. By expressing the Kerr horizon's angular velocity $\Omega_H = a / (r_+^2 + a^2)$ in terms of $M$ and $\chi$, we can solve for the change in spin, which simplifies to a remarkably elegant form [@problem_id:3479578]:

$$ d\chi = \frac{L}{M^2} \sqrt{1-\chi^2} $$

This result demonstrates that for a given amount of absorbed angular momentum $L$, the spin-up effect is greatest for a non-[rotating black hole](@entry_id:261667) ($\chi=0$) and vanishes for a maximally rotating one ($\chi \to 1$), making it increasingly difficult to spin a black hole up to its limit.

### Measuring the Remnant's Properties

In a numerical simulation, the parameters $M$ and $J$ of the final remnant black hole are not directly accessible. Instead, they must be inferred from observable geometric or [radiative properties](@entry_id:150127).

One primary method involves measuring geometric properties of the final, stationary horizon. The horizon area $A$ and [angular velocity](@entry_id:192539) $\Omega_H$ can be computed from the metric components on the horizon surface. These two [observables](@entry_id:267133) are sufficient to determine the two underlying parameters, $M$ and $\chi$. A careful derivation starting from the standard Kerr relations for $A$ and $\Omega_H$ yields a [closed-form expression](@entry_id:267458) for the dimensionless spin purely in terms of these measurable quantities [@problem_id:3479548]:

$$ \chi = \sqrt{\frac{A\,\Omega_H^{2}}{\pi}-\left(\frac{A\,\Omega_H^{2}}{2\pi}\right)^{2}} $$

This formula provides a powerful, direct way to compute the spin of the remnant black hole from the geometric data produced at the end of a simulation.

A second, independent method relies on analyzing the [gravitational radiation](@entry_id:266024) emitted during the final "ringdown" phase. The remnant black hole, having settled to a Kerr state, oscillates in a characteristic way, emitting a signal that is a superposition of **[quasinormal modes](@entry_id:264538) (QNMs)**. The frequencies of these modes, $\omega_{lmn}$, are complex numbers where the real part gives the oscillation frequency and the imaginary part gives the damping time. Crucially, these frequencies are determined solely by the mass $M$ and spin $\chi$ of the final Kerr black hole. They are coordinate-invariant features of the [spacetime geometry](@entry_id:139497). By fitting the late-time gravitational waveform to a sum of damped sinusoids, one can extract these QNM frequencies and thereby infer $M$ and $\chi$. Because the QNM frequencies are fundamental properties of the final geometry, their values are invariant under the gauge freedoms present at [null infinity](@entry_id:159987), such as BMS [supertranslations](@entry_id:755663), making this a robust measurement technique [@problem_id:3479535].

### The Challenge of Dynamics: Quasi-Local Horizons

The clean, stationary picture breaks down during the inspiral and merger phases. The spacetime is highly dynamic, and the individual black holes are distorted. To track the properties of the black holes during this evolution, we must move from global concepts to quasi-local ones.

The most familiar definition of a black hole boundary is the **event horizon (EH)**, defined as the boundary of the causal past of [future null infinity](@entry_id:261525), $\mathcal{H}^+ = \partial J^-(\mathscr{I}^+)$. This definition is *teleological*: to know whether a point in spacetime lies on the event horizon, one must know the entire future evolution of the spacetime to determine which [light rays](@entry_id:171107) ultimately escape to infinity. In a [numerical simulation](@entry_id:137087) that proceeds step-by-step in time, the future is unknown. Thus, the event horizon cannot be located during the evolution; it can only be constructed in post-processing after the simulation is complete. This makes it impractical for real-time diagnostics [@problem_id:3479565].

For this reason, [numerical relativity](@entry_id:140327) relies on the concept of **apparent horizons (AHs)**. An AH is a *quasi-local* concept, defined on a single spacelike slice $\Sigma_t$. It is the outermost surface for which outgoing light rays are momentarily not expanding. More formally, it is a [marginally outer trapped surface](@entry_id:751673) (MOTS), where the expansion of the outgoing null [congruence](@entry_id:194418), $\theta_{(\ell)}$, vanishes. The condition $\theta_{(\ell)}=0$ translates into a differential equation on the slice $\Sigma_t$ that can be solved at each time step to find the AH's location.

The price for this practical [computability](@entry_id:276011) is **slicing dependence**. In the [3+1 decomposition](@entry_id:140329) of spacetime, the condition for an AH can be written in terms of the geometry of the slice $\Sigma_t$. The expansion $\theta_{(\ell)}$ is given by:

$$ \theta_{(\ell)} \propto D_i s^i - K + K_{ij}s^i s^j $$

where $s^i$ is the outward normal to the AH within the slice, $D_i$ is the [covariant derivative](@entry_id:152476) compatible with the slice's metric, and $K_{ij}$ is the **[extrinsic curvature](@entry_id:160405)** of the slice, with $K$ being its trace. The extrinsic curvature measures how the slice $\Sigma_t$ is embedded within the full four-dimensional spacetime. Since different choices of slicing (i.e., different coordinate gauges) lead to different extrinsic curvatures, a surface that is an AH on one slice may not be on another. Consequently, the location, area, and other properties of the [apparent horizon](@entry_id:746488) are gauge-dependent quantities [@problem_id:3479544]. This slice-dependence means that quantities like the [irreducible mass](@entry_id:160861) computed from the AH area, $M_{\text{irr}}(t) = \sqrt{A(t)/16\pi}$, will exhibit gauge-driven fluctuations during a simulation.

### A Rigorous Framework: Dynamical and Isolated Horizons

The gauge-dependence of apparent horizons necessitates a more rigorous framework to extract [physical information](@entry_id:152556). The concepts of **isolated horizons (IH)** and **[dynamical horizons](@entry_id:748719) (DH)** provide this foundation.

An **isolated horizon** is a null hypersurface foliated by apparent horizons. It represents a black hole in equilibrium—no matter or radiation is falling across it. Its geometry is time-independent. The final remnant black hole in a simulation is modeled as an IH.

A **dynamical horizon**, in contrast, is a *spacelike* hypersurface foliated by apparent horizons. This structure models a black hole that is growing, for instance by accreting matter or absorbing gravitational waves. The spacelike nature of a DH is equivalent to its area being strictly increasing. The growth of area on a DH is governed by a flux-balance law derived from the Einstein field equations [@problem_id:3479523]:

$$ \frac{dA}{dv} = \int_{S_v} N \left[ 8\pi \, T_{ab}\ell^a n^b + \sigma_{ab}\sigma^{ab} + 2\zeta_a \zeta^a \right] d^2 S $$

Here, the rate of area change is sourced by the flux of matter-energy ($T_{ab}\ell^a n^b$) and a non-negative contribution from the gravitational field itself, given by the shear $\sigma_{ab}$ of the outgoing null rays and a rotational term $\zeta_a$. The term $\sigma_{ab}\sigma^{ab}$ represents the flux of [gravitational wave energy](@entry_id:267025) being absorbed by the horizon. This equation is a local, dynamical version of the second law of [black hole mechanics](@entry_id:264759): the area of a black hole can only increase.

Within the IH/DH framework, one can define a quasi-local angular momentum on each AH slice. This typically involves identifying an approximate [axial symmetry](@entry_id:173333) on the (generally distorted) horizon surface and using the corresponding approximate Killing vector in a Komar-like integral. While the resulting spin magnitude can be defined as an intrinsic geometric invariant of the horizon slice, its direction as a vector embedded in the 3D simulation grid remains dependent on the coordinate gauge [@problem_id:3479535].

### The Global Picture: Conserved Charges at Infinity

To establish a firm physical grounding, we must connect our quasi-local measurements to conserved quantities defined at the boundaries of spacetime. General relativity provides two distinct sets of such charges.

At **spatial infinity ($i^0$)**, for an [asymptotically flat spacetime](@entry_id:192015), the asymptotic symmetry group is the Poincaré group. The [conserved charges](@entry_id:145660) associated with these symmetries are the **Arnowitt-Deser-Misner (ADM) mass and angular momentum** ($M_{\text{ADM}}$, $J_{\text{ADM}}$). These are defined by [surface integrals](@entry_id:144805) over a sphere at infinite spatial radius on an initial spacelike slice. They represent the total mass-energy and angular momentum of the entire spacetime, are constant throughout the evolution, and are free from the ambiguities that affect radiative charges [@problem_id:3479571].

At **[future null infinity](@entry_id:261525) ($\mathscr{I}^+$)**, where gravitational waves propagate, the asymptotic [symmetry group](@entry_id:138562) is the infinite-dimensional Bondi-Metzner-Sachs (BMS) group. This group includes not only the Poincaré transformations but also an infinite number of **[supertranslations](@entry_id:755663)**, which are angle-dependent time shifts, $u \to u + \alpha(\theta, \phi)$. The charges associated with BMS symmetries are the **Bondi-Sachs mass and angular momentum** ($M_{\text{B}}(u)$, $J_{\text{B}}(u)$). Unlike the ADM charges, these are not constant; their rate of change with retarded time $u$ gives the flux of energy and angular momentum carried away by gravitational waves. The presence of [supertranslations](@entry_id:755663) introduces a fundamental ambiguity: the value of the Bondi mass itself depends on the choice of supertranslation frame. This can bias the inference of physical parameters like inspiral spin from the waveform's phase evolution if not carefully handled, as a supertranslation mixes the different spherical harmonic modes of the radiation field [@problem_id:3479535].

### Reconciliation: The Global Angular Momentum Balance

The different definitions of mass and spin—initial ADM charges, quasi-local horizon values, and final remnant parameters—are not independent. They are connected by the fundamental principle of conservation of angular momentum. This leads to a powerful consistency check for any numerical relativity simulation, often called the **reconciliation procedure**.

The [total angular momentum](@entry_id:155748) of the system is given by the initial ADM value, $J_{\text{ADM}}$. As the binary evolves and merges, it radiates a total angular momentum $J_{\text{rad}}$ via gravitational waves. The system settles to a final black hole with spin $S_f$. The global balance law requires:

$$ J_{\text{ADM}} \approx S_f + J_{\text{rad}} $$

In a practical simulation, this balance is explicitly checked [@problem_id:3479518]:
1.  $J_{\text{ADM}}$ is computed from the initial data on the first slice.
2.  The final remnant spin $S_f$ is computed from the properties of the final [apparent horizon](@entry_id:746488) (e.g., using its area and [angular velocity](@entry_id:192539)) or from the ringdown QNM spectrum.
3.  The radiated angular momentum, $J_{\text{rad}}$, is computed from the gravitational waveform $h(t, r, \theta, \phi)$ extracted on spheres of finite coordinate radius $r$. The flux of the $z$-component of angular momentum is given by an expression involving the strain multipoles $h_{\ell m}$:
    $$ \frac{dJ_{z}}{dt} = \frac{r^{2}}{16\pi} \sum_{\ell,m} m \,\mathrm{Im}\left(\dot{h}_{\ell m}(t; r)\, h_{\ell m}^{*}(t; r)\right) $$
    This flux is integrated over the duration of the simulation to get the total radiated angular momentum at that radius, $J^{\text{rad}}(r)$.
4.  Since data at finite radius is contaminated by near-field effects, the result must be extrapolated to [null infinity](@entry_id:159987) ($r \to \infty$). This is often done by performing extractions at multiple radii and fitting to a model, such as a linear function of $1/r$, to find $J_{\text{rad}}(\infty)$.

The agreement between $J_{\text{ADM}}$ and the sum $S_f + J_{\text{rad}}(\infty)$, typically quantified by a normalized mismatch, serves as a crucial validation of the simulation's physical accuracy. It confirms that the initial state, the dynamics of radiation, and the final state are all consistent with the global conservation laws of General Relativity [@problem_id:3479571].