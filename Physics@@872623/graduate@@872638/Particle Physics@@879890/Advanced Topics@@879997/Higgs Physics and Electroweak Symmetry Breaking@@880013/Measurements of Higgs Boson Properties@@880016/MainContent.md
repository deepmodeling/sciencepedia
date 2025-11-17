## Introduction
The 2012 discovery of the Higgs boson marked the completion of the Standard Model's particle roster and the beginning of a new era in particle physics. With the existence of the particle confirmed, the central question has shifted from "Does it exist?" to "What is it?" Determining whether this new boson is the precise particle predicted by the Standard Model or the first glimpse into a more complex reality requires a comprehensive program of precision measurements. This endeavor probes the fundamental nature of [electroweak symmetry breaking](@entry_id:161363) and serves as a powerful tool in the search for new physics.

This article provides a graduate-level overview of the key methods and theoretical frameworks used to measure and interpret the properties of the Higgs boson. It addresses the knowledge gap between the discovery of the particle and the sophisticated techniques used to characterize it. The reader will embark on a journey through the core aspects of this research program. The first chapter, **Principles and Mechanisms**, details the foundational techniques for measuring the Higgs boson's mass, couplings, and CP nature, and for probing its [self-interaction](@entry_id:201333). Following this, **Applications and Interdisciplinary Connections** explores how these measurements are used to search for new phenomena and reveals the profound connections between Higgs physics, cosmology, and low-energy precision experiments. Finally, **Hands-On Practices** will offer a chance to apply these concepts to practical physics problems, cementing the theoretical understanding. We begin by examining the core principles that enable these remarkable measurements.

## Principles and Mechanisms

The discovery of the Higgs boson completed the particle content of the Standard Model (SM), but it also initiated a new era of inquiry. Is this new particle truly the Higgs boson predicted by the SM, or is it the first manifestation of a more complex [electroweak symmetry breaking](@entry_id:161363) sector? Answering this question requires a comprehensive program of measurements to determine its properties—mass, spin, CP [quantum numbers](@entry_id:145558), and couplings to other particles—with the highest possible precision. This chapter details the fundamental principles and experimental mechanisms through which these properties are measured and interpreted.

### Precision Measurements and Data Combination

The most fundamental property of any particle is its mass. For the Higgs boson, precision mass measurements are performed in channels with excellent final-state momentum resolution, primarily the decay to two photons, $H \to \gamma\gamma$, and the decay to four leptons via two Z bosons, $H \to ZZ^* \to 4\ell$ (where $\ell = e, \mu$). Each measurement in each channel yields a central value with an associated uncertainty, which is a composite of statistical and systematic components. To achieve the best possible precision, results from different channels and experiments must be combined.

This combination procedure must properly account for all sources of uncertainty, particularly **[systematic uncertainties](@entry_id:755766)** that are correlated between measurements. For instance, the uncertainty on the accelerator's beam energy calibration or the modeling of the underlying event can introduce a systematic shift that affects the reconstructed mass in both the $H \to \gamma\gamma$ and $H \to 4\ell$ channels in a similar way. Ignoring such correlations would lead to an incorrect, typically underestimated, final uncertainty.

The statistically rigorous method for combining measurements is to construct and minimize a $\chi^2$ function. Consider two measurements of the Higgs mass, $m_1$ and $m_2$, with total uncertainties $\delta_1$ and $\delta_2$, respectively. If these measurements have a correlation coefficient $\rho$, their relationship is described by a covariance matrix $V$:

$$
V = \begin{pmatrix} \delta_1^2 & \rho \delta_1 \delta_2 \\ \rho \delta_1 \delta_2 & \delta_2^2 \end{pmatrix}
$$

The $\chi^2$ function for a hypothesized true mass $m_H$ is given by:

$$
\chi^2(m_H) = (\mathbf{m} - \mathbf{1}m_H)^T V^{-1} (\mathbf{m} - \mathbf{1}m_H)
$$

where $\mathbf{m} = \begin{pmatrix} m_1 \\ m_2 \end{pmatrix}$ is the vector of measurements and $\mathbf{1} = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$. Minimizing this $\chi^2$ with respect to $m_H$ yields the best-fit combined value, often called the Best Linear Unbiased Estimate (BLUE). The result of this minimization is a weighted average, where the weights are determined by the elements of the [inverse covariance matrix](@entry_id:138450) $V^{-1}$.

The resulting best-fit mass, $\hat{m}_H$, is given by the expression [@problem_id:187990]:

$$
\hat{m}_H = \frac{ \sum_{i,j} (V^{-1})_{ij} m_j }{ \sum_{i,j} (V^{-1})_{ij} } = \frac{m_1(\delta_2^2 - \rho \delta_1 \delta_2) + m_2(\delta_1^2 - \rho \delta_1 \delta_2)}{\delta_1^2 + \delta_2^2 - 2\rho \delta_1 \delta_2}
$$

This formula reveals the crucial role of the correlation. For uncorrelated measurements ($\rho=0$), it reduces to the familiar inverse-variance weighted mean. For positive correlation ($\rho > 0$), which is common for shared [systematic uncertainties](@entry_id:755766), the denominator decreases, leading to a larger uncertainty on the combined value than if the correlation were ignored. Conversely, anti-correlation ($\rho  0$) can lead to a significant reduction in the final uncertainty. This formalism is central to nearly all summary results in experimental particle physics.

### The Kappa Framework: A Universal Language for Deviations

Beyond the mass, the defining characteristic of the Higgs boson is its pattern of couplings to other SM particles. The SM makes precise predictions for these couplings, which are determined by the particles' masses. Testing these predictions is a primary objective of the LHC physics program. The **kappa framework** offers a simplified, model-independent approach to parameterize potential deviations.

In this framework, each coupling of the Higgs boson to a particle $j$ is modified by a factor $\kappa_j$, such that $g_j = \kappa_j g_j^{\text{SM}}$. A value of $\kappa_j=1$ signifies agreement with the SM prediction. For instance, $\kappa_W$ and $\kappa_Z$ modify the couplings to vector bosons, while $\kappa_t$, $\kappa_b$, and $\kappa_\tau$ modify the Yukawa couplings to top quarks, bottom quarks, and tau leptons, respectively.

These modifiers directly impact observable quantities. Production cross-sections, $\sigma$, and partial decay widths, $\Gamma$, involving a single type of vertex generally scale as $\kappa_j^2$. For example, the [partial width](@entry_id:156471) for the tree-level decay $H \to b\bar{b}$ is $\Gamma(H \to b\bar{b}) = \kappa_b^2 \Gamma_{\text{SM}}(H \to b\bar{b})$. Loop-induced processes are more complex, as they can involve multiple particles in the loop. The $ggH$ vertex, for instance, is dominated by the top quark loop but also has a non-negligible bottom quark loop contribution. Its modifier, $\kappa_g$, is therefore a function of $\kappa_t$ and $\kappa_b$.

A critical subtlety is the effect on **branching ratios (BR)**. Since the total decay width, $\Gamma_H = \sum_f \Gamma(H \to f)$, also depends on the various $\kappa$ values, every [branching ratio](@entry_id:157912) is affected by all coupling modifications:

$$
\text{BR}(H \to f) = \frac{\Gamma(H \to f)}{\Gamma_H} = \frac{\kappa_f^2 \Gamma_{\text{SM}}(H \to f)}{\sum_j \kappa_j^2 \Gamma_{\text{SM}}(H \to j)}
$$

Experimental measurements are typically quoted in terms of **signal strengths**, $\mu$, defined for a production mode $i$ and final state $f$ as the ratio of the observed rate to the SM prediction:

$$
\mu_{if} = \frac{\sigma(i) \times \text{BR}(H \to f)}{\sigma_{\text{SM}}(i) \times \text{BR}_{\text{SM}}(H \to f)}
$$

By expressing $\sigma(i)$ and $\text{BR}(H \to f)$ in terms of the kappa modifiers, measurements of $\mu$ can be translated into constraints on the $\kappa_j$ parameters. As a hypothetical example, consider constraining $\kappa_b$ using a measurement of the ratio of signal strengths $\mathcal{R} = \mu(VH, H \to b\bar{b}) / \mu(ggF, H \to \gamma\gamma)$, assuming all other couplings are SM-like ($\kappa_j=1$ for $j \neq b$). The numerator and denominator of this ratio depend on $\kappa_b$ in distinct ways [@problem_id:188077]. The $VH$ production [cross section](@entry_id:143872) is unchanged ($\kappa_V=1$), but the $H \to b\bar{b}$ [branching ratio](@entry_id:157912) changes due to both $\kappa_b^2$ in the [partial width](@entry_id:156471) and its effect on the total width. The $ggF$ production cross section also acquires a $\kappa_b$ dependence from the bottom-quark loop interfering with the top-quark loop. Such a measurement can thus be used to solve for $\kappa_b$, providing a powerful test of the SM's predictions for the Yukawa sector.

### Probing New Physics with Kinematic Distributions

While measurements of rates (cross-sections and branching ratios) are powerful, they are not the only tools at our disposal. The kinematic distributions of the Higgs boson and its decay products carry a wealth of information, particularly about the spin and CP properties of its interactions. New physics can manifest not just as a change in the overall number of events, but as a subtle or dramatic alteration of event shapes.

#### CP Properties from Vector Boson Fusion

The interaction of the Higgs boson with vector bosons ($HVV$ coupling) has a specific Lorentz structure in the SM, described by the metric tensor $g^{\mu\nu}$. This corresponds to a pure CP-even (scalar) state. However, an alternative, CP-odd ([pseudoscalar](@entry_id:196696)) coupling is also possible, described by the Levi-Civita tensor $\epsilon^{\mu\nu\rho\sigma}$. The kinematic signatures of these two possibilities are starkly different.

**Vector Boson Fusion (VBF)** is a production process that is exceptionally sensitive to the $HVV$ coupling structure. In VBF, two quarks in the initial protons radiate vector bosons ($W$ or $Z$), which then fuse to produce a Higgs boson. The two quarks are deflected and manifest as energetic jets in the forward and backward regions of the detector. The azimuthal angle separation between these two jets, $\Delta\phi_{jj}$, is a powerful observable for probing the CP nature of the $HVV$ vertex.

Within a simplified model, one can demonstrate how this works [@problem_id:182522]. The amplitude for the CP-even interaction, $\mathcal{V}_h^{\mu\nu} \propto g^{\mu\nu}$, is proportional to the dot product of the incoming quark momenta, which is independent of the transverse [kinematics](@entry_id:173318) of the final state jets. In contrast, the amplitude for the CP-odd interaction, $\mathcal{V}_A^{\mu\nu} \propto \epsilon^{\mu\nu\rho\sigma} k_{1\rho} k_{2\sigma}$, involves the momenta $k_1$ and $k_2$ of the exchanged vector bosons. This term is proportional to the determinant of the four momentum vectors of the process, which evaluates to a term proportional to $p_T^2 \sin\Delta\phi_{jj}$, where $p_T$ is the transverse momentum of the jets. Consequently, the ratio of the squared [matrix elements](@entry_id:186505) behaves as:

$$
\frac{|\mathcal{M}_{A}|^2}{|\mathcal{M}_{h}|^2} \propto p_T^4 \sin^2\Delta\phi_{jj}
$$

This implies that a CP-even Higgs tends to be produced with a relatively flat distribution in $\Delta\phi_{jj}$, whereas a CP-odd Higgs would lead to a distribution that vanishes at $\Delta\phi_{jj}=0$ and $\pi$, and peaks at $\Delta\phi_{jj}=\pi/2$. Experimental measurements of this distribution at the LHC have shown it to be consistent with the CP-even hypothesis, strongly disfavoring a pure CP-odd nature for the observed Higgs boson.

#### CP Properties in Fermionic Decays

The CP nature of the Higgs can also be tested in its couplings to fermions (Yukawa couplings). A general Higgs-fermion interaction can contain both a scalar (CP-even) part and a [pseudoscalar](@entry_id:196696) (CP-odd) part, often parameterized by a CP-mixing angle $\alpha_{CP}$:

$$
\mathcal{L}_{Hff} \propto -H \bar{\psi}_f (\cos\alpha_{CP} + i\sin\alpha_{CP}\gamma_5)\psi_f
$$

where $\alpha_{CP}=0$ is pure scalar and $\alpha_{CP}=\pi/2$ is pure [pseudoscalar](@entry_id:196696). These two terms lead to different spin configurations for the final-state fermions. In the decay $H \to f\bar{f}$, the scalar interaction forces the outgoing fermions to have opposite helicities, a consequence of chirality conservation for a Lorentz scalar interaction. The [pseudoscalar](@entry_id:196696) interaction, however, flips [chirality](@entry_id:144105) and results in the fermions having the same [helicity](@entry_id:157633).

The decay $H \to \tau^+\tau^-$ is an excellent laboratory for this test, as the tau lepton's short lifetime means its spin information is transferred to the angular distributions of its decay products (e.g., $\tau \to \pi\nu_\tau$). By measuring these angular correlations, one can reconstruct the probability of producing same-helicity versus opposite-helicity tau pairs. The ratio of these probabilities is directly sensitive to the CP-mixing angle [@problem_id:188020]. In the Higgs rest frame, the squared amplitudes for opposite-[helicity](@entry_id:157633) states ($h_1 = -h_2$) are proportional to $\cos^2\alpha_{CP}$, while those for same-helicity states ($h_1 = h_2$) are proportional to $\sin^2\alpha_{CP}$. The ratio of total probabilities is thus:

$$
\mathcal{R} = \frac{P(\text{same helicity})}{P(\text{opposite helicity})} = \frac{\tan^2\alpha_{CP}}{\beta_\tau^2} = \frac{\tan^2\alpha_{CP}}{1 - 4m_\tau^2/m_H^2}
$$

where $\beta_\tau$ is the tau velocity. A measurement of $\mathcal{R}$ provides a direct measurement of $\tan\alpha_{CP}$, constraining any CP-violating component in the tau-Yukawa coupling.

#### Probing BSM Amplitudes via Interference

More generally, kinematic distributions are sensitive to any form of new physics that can interfere with the SM amplitude. Consider the decay $H \to VV \to 4f$. The kinematics are described by several angles, including $\Phi_{dec}$, the angle between the decay planes of the two vector bosons. If a BSM physics process contributes an amplitude $\mathcal{A}_{\text{BSM}}$ in addition to the SM amplitude $\mathcal{A}_{\text{SM}}$, the total differential decay rate will contain a pure SM term $|\mathcal{A}_{\text{SM}}|^2$, a pure BSM term $|\mathcal{A}_{\text{BSM}}|^2$, and an interference term $2\,\text{Re}(\mathcal{A}_{\text{SM}}^* \mathcal{A}_{\text{BSM}})$.

Often, these terms have different dependencies on the kinematic angles. For example, the SM and a hypothetical CP-even BSM contribution might have a $\cos(2\Phi_{dec})$ dependence, while their interference term might be proportional to $\cos(\Phi_{dec})$ [@problem_id:188089]. The expectation value of an observable like $\cos(\Phi_{dec})$ is computed by integrating over the distribution:

$$
\langle \cos(\Phi_{dec}) \rangle = \frac{\int \cos(\Phi_{dec}) \frac{d\Gamma}{d\Phi_{dec}} d\Phi_{dec}}{\int \frac{d\Gamma}{d\Phi_{dec}} d\Phi_{dec}}
$$

Due to the orthogonality of cosine functions, terms like $\int \cos(\Phi_{dec}) d\Phi_{dec}$ and $\int \cos(\Phi_{dec})\cos(2\Phi_{dec}) d\Phi_{dec}$ integrate to zero over the full range $[0, 2\pi]$. The only term that survives in the numerator is the one from the interference, $\int \cos^2(\Phi_{dec}) d\Phi_{dec}$. The resulting expectation value is directly proportional to the product of the SM and BSM couplings, $g_{\text{SM}}g_{\text{BSM}}$. A non-zero measurement of such an observable would be a clear signal of new physics and its interference with the Standard Model.

### Probing the Higgs Potential

The scalar potential responsible for [electroweak symmetry breaking](@entry_id:161363) is predicted in the SM to be $V(h) = \frac{1}{2}m_H^2 h^2 + \lambda_{HHH} h^3 + \lambda_{HHHH} h^4$. The discovery of the Higgs boson only establishes the quadratic term. A complete test of the SM requires measuring the trilinear ($\lambda_{HHH}$) and quartic ($\lambda_{HHHH}$) self-couplings, which dictate the shape of the Higgs potential.

#### Direct Probes: Higgs Pair Production

The most direct method to access the trilinear self-coupling is through the production of Higgs boson pairs ($HH$). The dominant production mode in the SM is gluon-[gluon fusion](@entry_id:158683), $gg \to HH$. At leading order, this process proceeds via two types of top-quark [loop diagrams](@entry_id:149287): "box" diagrams where both Higgs bosons are emitted from the quark loop, and "triangle" diagrams where an intermediate virtual Higgs splits into two, involving the $\lambda_{HHH}$ vertex.

The total amplitude is a sum of these contributions: $\mathcal{M} = \mathcal{M}_{\text{box}} + \mathcal{M}_{\text{triangle}}$. The triangle amplitude is directly proportional to the trilinear coupling, so deviations are parameterized by $\kappa_\lambda = \lambda_{HHH}/\lambda_{\text{SM}}$. The amplitude becomes $\mathcal{M}(\kappa_\lambda) = \mathcal{M}_{\text{box}} + \kappa_\lambda \mathcal{M}_{\text{triangle,SM}}$. The cross-section is then a quadratic function of $\kappa_\lambda$ [@problem_id:188025]:

$$
\hat{\sigma}(\kappa_\lambda) \propto |\mathcal{M}_{\text{box}} + \kappa_\lambda \mathcal{M}_{\text{triangle,SM}}|^2 = |\mathcal{M}_{\text{box}}|^2 + \kappa_\lambda^2 |\mathcal{M}_{\text{triangle,SM}}|^2 + 2\kappa_\lambda \text{Re}(\mathcal{M}_{\text{box}}^* \mathcal{M}_{\text{triangle,SM}})
$$

A crucial feature of the SM is that the box and triangle amplitudes interfere destructively, significantly suppressing the total $HH$ cross-section. A measurement of the $HH$ production rate, which is extremely challenging due to its small value, provides a handle on $\kappa_\lambda$. A significant enhancement of the rate could indicate a value of $\kappa_\lambda$ far from the SM prediction of one.

#### Indirect Probes: Loop Corrections to Single-Higgs Processes

Given the difficulty of direct $HH$ measurements, it is valuable to search for indirect effects of an anomalous self-coupling. The trilinear coupling can appear in higher-order [loop corrections](@entry_id:150150) to single-Higgs processes. For example, the amplitude for the decay $H \to \gamma\gamma$ receives two-[loop corrections](@entry_id:150150) that involve a $\lambda_{HHH}$ vertex.

While the one-loop amplitude for $H \to \gamma\gamma$ from a [heavy fermion](@entry_id:139422) loop is a constant in the heavy-mass limit, the two-loop correction involving $\kappa_\lambda$ introduces an additional contribution. This correction is calculable and depends on $\kappa_\lambda$. The ratio of the two-loop anomalous contribution to the one-loop SM contribution can be expressed as [@problem_id:188078]:

$$
R = \frac{\delta\mathcal{A}_f^{(\lambda)}}{\mathcal{A}_f^{\text{1L}}} = \kappa_\lambda \frac{3(\pi^2 - 3)\,m_H^2}{64\pi^2\,v^2}
$$

This shows that a precise measurement of the $H \to \gamma\gamma$ rate (and other precision observables) can provide an *indirect* constraint on $\kappa_\lambda$. While these constraints are typically weaker than those from direct searches, they provide complementary information and probe the self-coupling in a completely different regime.

### Theoretical Frameworks and Interpretation

The results of Higgs property measurements must be interpreted within broader theoretical contexts. They provide powerful constraints on new physics scenarios and help us understand the fundamental principles governing the electroweak scale.

#### Unitarity and High-Energy Scattering

One of the most profound theoretical roles of the Higgs boson is to ensure the **[unitarity](@entry_id:138773)** of [scattering amplitudes](@entry_id:155369) at high energies. In a theory without a Higgs boson, the [scattering amplitude](@entry_id:146099) for longitudinally polarized vector bosons, such as $W_L^+ W_L^- \to Z_L Z_L$, grows with the square of the [center-of-mass energy](@entry_id:265852), $\mathcal{A} \sim s/M_W^2$. This unchecked growth eventually violates the unitarity bound on scattering probability.

In the SM, diagrams involving Higgs exchange precisely cancel this bad high-energy behavior, rendering the amplitudes well-behaved. This cancellation requires the Higgs couplings to vector bosons to be exactly as predicted. If the coupling deviates, parameterized by $\kappa_V = g_{hVV}/g_{hVV}^{\text{SM}}$, the cancellation becomes incomplete. In the high-energy limit, the problematic part of the amplitude for $W_L W_L \to Z_L Z_L$ re-emerges, proportional to $(1-\kappa_V^2)s/v^2$ [@problem_id:188050].

The principle of unitarity requires the real part of each partial wave amplitude, $a_J$, to be bounded: $|\text{Re}(a_J)| \leq 1/2$. For the [s-wave](@entry_id:754474) ($J=0$) component of the $W_L W_L$ [scattering amplitude](@entry_id:146099), this leads to an upper bound on the energy scale at which the theory remains perturbative:

$$
s_{\text{max}} = \frac{8\pi v^2}{|1-\kappa_V^2|}
$$

A measurement of $\kappa_V$ close to 1 pushes this "[unitarity](@entry_id:138773) violation scale" $\sqrt{s_{\text{max}}}$ to very high energies. Conversely, any measured deviation $|\kappa_V - 1| > 0$ implies that new physics *must* appear at or below the scale $\sqrt{s_{\text{max}}}$ to restore [unitarity](@entry_id:138773). Precision measurements of Higgs couplings thus provide a powerful, model-independent probe of the energy scale of new phenomena.

#### Effective Field Theory and its Limitations

A systematic way to interpret Higgs measurements is through the lens of **Effective Field Theory (EFT)**. In the SM-EFT framework, the SM Lagrangian is augmented by higher-dimensional operators, suppressed by powers of a new physics scale $\Lambda$. Measurements of Higgs couplings and kinematic distributions can be used to constrain the coefficients of these operators.

However, it is critical to understand the limits of validity of any EFT. An EFT is only valid for processes with characteristic [energy scales](@entry_id:196201) well below the scale of the new physics it parameterizes. For Higgs physics, a common approximation is the **Heavy-Top Effective Field Theory (HEFT)**, where the top quark is assumed to be infinitely massive and is "integrated out," leading to effective local vertices like $ggh$ and $gghh$.

This approximation works well for processes where the energy scale is much less than the [top quark mass](@entry_id:160842), $E \ll m_t$. However, it fails spectacularly at high energies. Consider Higgs production in association with a jet, $gg \to Hg$, at high transverse momentum ($p_T$). In the full theory, the process is mediated by a top quark loop. At high $p_T \gg m_t$, the theory resolves the internal structure of the loop. In HEFT, the interaction is point-like. This leads to different predictions for the high-$p_T$ behavior. For example, at high $p_T$, certain [helicity](@entry_id:157633) amplitudes that are zero in HEFT become non-zero in the full theory [@problem_id:188053]. This leads to a ratio of the full theory cross-section to the HEFT prediction that deviates significantly from unity. Measuring the Higgs $p_T$ spectrum and comparing it to these predictions provides a direct test of the EFT framework and can reveal the scale at which it breaks down.

#### Constraining Specific Beyond-the-SM Scenarios

Ultimately, the goal is to use the pattern of measured Higgs properties to identify the nature of any new physics. Different BSM scenarios predict different patterns of deviations for the $\kappa_j$ modifiers. For example, in **Composite Higgs Models**, the Higgs is a pseudo-Nambu-Goldstone boson arising from the breaking of a larger global symmetry at a scale $f$. All Higgs couplings are suppressed relative to the SM by factors related to the ratio $\xi = v^2/f^2$.

In the minimal SO(5)/SO(4) model, for instance, the coupling modifiers for the single-Higgs and double-Higgs interactions with vector bosons are predicted to be functions of $\xi$ [@problem_id:188003]:

$$
\kappa_V = \sqrt{1-\xi} \qquad \text{and} \qquad \kappa_{2V} = 1-2\xi
$$

This leads to a concrete prediction for the ratio of these modifiers: $\kappa_{2V}/\kappa_V^2 = (1-2\xi)/(1-\xi)$. A precise measurement of $\kappa_V$ implies a value for $\xi$, which in turn predicts the values of all other coupling modifiers, such as $\kappa_f$ (for fermions), $\kappa_\lambda$, and $\kappa_{2V}$. A global fit to all measured Higgs properties can therefore stringently test such a model, and a confirmed pattern of correlated deviations would be a smoking gun for this specific new physics scenario.

In conclusion, the measurement of Higgs boson properties is a multi-faceted endeavor that combines precision experimental data with sophisticated theoretical interpretation. From the careful statistical combination of mass measurements to the use of kinematic distributions to probe CP properties and the search for the Higgs self-coupling, each measurement opens a new window onto the mechanism of [electroweak symmetry breaking](@entry_id:161363). Interpreted through the lenses of unitarity, EFT, and specific BSM models, these measurements are not merely about cataloging the properties of a particle, but are a deep exploration of the fundamental structure of our universe.