## Introduction
Understanding the forces between nucleons is a cornerstone of nuclear physics. These forces, described by nuclear potentials, are not directly observable. Instead, their nature must be inferred from the outcomes of scattering experiments, where particles are deflected by their interactions. The central challenge, and the focus of this article, is bridging the gap between raw experimental data—such as scattering cross sections—and the abstract theoretical construct of a potential. This process, known as potential fitting, is a complex blend of quantum theory, statistical analysis, and computational science.

This article provides a comprehensive guide to fitting nuclear potentials to scattering data. We will begin in the first chapter, **Principles and Mechanisms**, by establishing the fundamental connection between scattering [observables](@entry_id:267133) and the underlying potential, exploring the statistical machinery of chi-squared fitting, and delving into advanced concepts like Chiral Effective Field Theory. The second chapter, **Applications and Interdisciplinary Connections**, will demonstrate how these methods are used to dissect the [nuclear force](@entry_id:154226), enhance the physical realism of models, and guide the design of future experiments. Finally, the **Hands-On Practices** chapter offers a series of practical exercises to solidify these concepts, allowing you to apply what you've learned to concrete problems in [computational nuclear physics](@entry_id:747629).

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the process of fitting nuclear potentials to scattering data. We will begin by establishing the theoretical language of scattering theory, connecting abstract mathematical constructs like the S-matrix to concrete experimental observables. Subsequently, we will explore the structure of the nuclear potentials themselves, understanding how different components of the interaction manifest in scattering phenomena. We will then bridge theory and experiment by examining the statistical methods used in the fitting process. Finally, we will address the advanced topics and theoretical frameworks, such as the inclusion of Coulomb and inelastic effects, the ambiguity of phase equivalence, and the modern paradigms of Effective Field Theory and dispersive models, that are essential for constructing high-fidelity nuclear interactions.

### From Scattering Amplitudes to Observables

The primary goal of a scattering experiment is to infer the nature of an interaction, encapsulated in a potential $V$, by observing how it deflects an incident particle. In [nonrelativistic quantum mechanics](@entry_id:752670), this process is described by the asymptotic form of the stationary scattering [wave function](@entry_id:148272), which at large distances consists of an incident plane wave and an [outgoing spherical wave](@entry_id:201591):
$$
\psi(\mathbf{r}) \sim e^{ikz} + f(\theta)\,\frac{e^{ikr}}{r}
$$
Here, $k$ is the [center-of-mass momentum](@entry_id:171180), and $f(\theta)$ is the **[scattering amplitude](@entry_id:146099)**, a complex function that encodes the entire outcome of the elastic scattering process at a given energy.

The most direct experimental observable is the **[differential cross section](@entry_id:159876)**, $d\sigma/d\Omega$, which measures the probability of scattering into a particular direction. It is related to the [scattering amplitude](@entry_id:146099) by a simple and fundamental relation derived from the analysis of probability flux:
$$
\frac{d\sigma}{d\Omega} = |f(\theta)|^2
$$
Integrating the [differential cross section](@entry_id:159876) over all solid angles yields the **total elastic [cross section](@entry_id:143872)**, $\sigma_{\text{el}} = \int |f(\theta)|^2 d\Omega$.

A central principle connecting these [observables](@entry_id:267133) is the **[optical theorem](@entry_id:140058)**. This theorem, a direct consequence of [probability conservation](@entry_id:149166) ([unitarity](@entry_id:138773)), provides a powerful link between the total cross section (representing the total loss of flux from the incident beam due to all interactions) and the [scattering amplitude](@entry_id:146099) in the exact forward direction ($\theta=0$):
$$
\sigma_{\text{tot}} = \frac{4\pi}{k}\,\mathrm{Im}\,f(0)
$$
In the context of fitting a potential, the [optical theorem](@entry_id:140058) serves as a crucial consistency check. Any candidate potential must not only reproduce the angular shape of the [differential cross section](@entry_id:159876) across various angles but must also yield a forward amplitude whose imaginary part is consistent with the measured total [cross section](@entry_id:143872) . A model that fails this test is physically inconsistent.

### The Formalism of Scattering Matrices

To connect the potential to the [scattering amplitude](@entry_id:146099), it is practical to work in a partial-wave basis, where the interaction is analyzed independently for each value of orbital angular momentum $l$. In this basis, the information is encoded in a set of scattering matrices. For single-channel [elastic scattering](@entry_id:152152) (e.g., neutron-proton scattering at low energy), the key quantities are the **S-matrix**, **T-matrix**, and **K-matrix** elements for a given partial wave $l$.

The **S-matrix** element, $S_l$, relates the [outgoing spherical wave](@entry_id:201591) to the incoming one. For elastic scattering from a real potential, [probability conservation](@entry_id:149166) dictates that the S-matrix must be unitary. In a single channel, this simplifies to the condition that $S_l$ is a complex number of unit modulus, which is conventionally parameterized by a real phase shift $\delta_l$:
$$
S_l = e^{2i\delta_l}
$$
The condition $|S_l|=1$ is the partial-wave expression of unitarity.

The on-shell **T-matrix** element, $T_l$, is directly proportional to the partial-wave component of the [scattering amplitude](@entry_id:146099) and is defined in terms of the S-matrix:
$$
T_l = \frac{S_l - 1}{2ik} = \frac{e^{2i\delta_l} - 1}{2ik} = \frac{1}{k}e^{i\delta_l}\sin\delta_l
$$
From the [unitarity](@entry_id:138773) of $S_l$, one can derive the partial-wave [optical theorem](@entry_id:140058), $\operatorname{Im} T_l = k|T_l|^2$, which explicitly shows that for scattering to occur ($\delta_l \neq 0$), the T-matrix must have a non-zero imaginary part, even for a real potential .

The **K-matrix**, or [reactance](@entry_id:275161) matrix, is defined via the tangent of the phase shift:
$$
K_l = \tan\delta_l
$$
For a real potential yielding a real phase shift, the K-matrix is a real quantity. The T-matrix and K-matrix are related through the Heitler equation:
$$
T_l = \frac{K_l}{1-ikK_l}
$$
These matrices have distinct and important analytic properties. The S-matrix (and thus the T-matrix) is analytic in the upper half of the complex $k$-plane. Poles on the positive [imaginary axis](@entry_id:262618) (e.g., at $k=i\kappa$ with $\kappa > 0$) correspond to **[bound states](@entry_id:136502)**, which have normalizable wavefunctions. **Resonances**, or quasi-stable states, correspond to poles in the lower half of the complex $k$-plane on a second, "unphysical" Riemann sheet reached by analytic continuation across the positive real axis . In contrast, a pole of the real K-matrix occurs when the phase shift passes through $\pi/2$ (modulo $\pi$). This condition, $\delta_l = \pi/2$, defines a resonance and leads to a *finite peak* in the partial-wave [cross section](@entry_id:143872) at the [unitarity limit](@entry_id:197354), $\sigma_l = \frac{4\pi}{k^2}(2l+1)$, not a divergence. A pole in the K-matrix does not correspond to a pole in the T-matrix on the real axis.

### The Operator Structure of the Nucleon-Nucleon Interaction

To perform a fit, one must first define a model for the potential $V$. For the nucleon-nucleon (NN) interaction, symmetry principles—invariance under rotations, parity, [time reversal](@entry_id:159918), and [isospin](@entry_id:156514) exchange—severely constrain its general form. A minimal, local potential is typically written as a sum of terms, each consisting of a radial function multiplied by a [spin-orbital](@entry_id:274032) operator: $V(\mathbf{r}) = \sum_i V_i(r) \mathcal{O}_i$. The goal of a fit is to determine the shape of the radial functions $V_i(r)$.

A standard operator basis for the NN interaction includes four main components :
1.  **Central Potential ($V_C(r)\mathbf{1}$):** This is a spin-independent term that depends only on the distance between the two nucleons. It provides the bulk of the interaction strength and is the dominant force determining low-energy S-wave ($l=0$) phase shifts and scattering lengths.

2.  **Spin-Spin Potential ($V_\sigma(r)(\boldsymbol{\sigma}_1 \cdot \boldsymbol{\sigma}_2)$):** This term depends on the relative orientation of the two nucleon spins. Its eigenvalue is different for spin-singlet ($S=0$) and spin-triplet ($S=1$) states, making it directly responsible for the observed splitting between singlet and triplet channels with the same $l$, such as the significant difference between the $^{1}S_0$ and $^{3}S_1$ scattering lengths.

3.  **Spin-Orbit Potential ($V_{LS}(r)(\mathbf{L} \cdot \mathbf{S})$):** This term couples the [total spin](@entry_id:153335) of the pair, $\mathbf{S}$, to their relative orbital angular momentum, $\mathbf{L}$. It is zero for S-waves ($l=0$) but is crucial for $l>0$. It splits the phase shifts for states with the same $l$ and $S$ but different total angular momentum $J$. Its most prominent effect is the splitting among the three triplet P-wave phase shifts ($^{3}P_0, ^{3}P_1, ^{3}P_2$). This interaction is also essential for describing polarization [observables](@entry_id:267133), such as the analyzing power $A_y$.

4.  **Tensor Potential ($V_T(r)S_{12}$):** This is a non-central force that couples the spins to the spatial orientation of the nucleon pair. The tensor operator is defined as $S_{12} = 3(\boldsymbol{\sigma}_1 \cdot \hat{\mathbf{r}})(\boldsymbol{\sigma}_2 \cdot \hat{\mathbf{r}}) - \boldsymbol{\sigma}_1 \cdot \boldsymbol{\sigma}_2$. The defining characteristic of the tensor force is that it does not conserve orbital angular momentum. It has non-zero matrix elements between states with the same $J$ and parity but with $l$ differing by two units ($\Delta l = 2$).

The most important consequence of the tensor force is the coupling of channels. For example, in the $J=1$ triplet channel, the tensor force mixes the $^{3}S_1$ ($l=0$) and $^{3}D_1$ ($l=2$) states, as both have the same [total angular momentum](@entry_id:155748) and parity. This mixing gives the [deuteron](@entry_id:161402) its non-zero [electric quadrupole moment](@entry_id:157483) and requires a more complex scattering description. For such **[coupled channels](@entry_id:204758)**, the S-matrix becomes a matrix in the channel space. For the ${}^3S_1$–${}^3D_1$ system, it is a $2 \times 2$ unitary, symmetric matrix parameterized by two phase shifts, $\delta_{S}$ and $\delta_{D}$, and a **mixing angle** $\varepsilon_1$ . A standard parameterization is:
$$
S^{(J=1)} = \begin{pmatrix} \cos 2\varepsilon_1\, e^{2 i \delta_S}  i \sin 2\varepsilon_1\, e^{i(\delta_S+\delta_D)} \\ i \sin 2\varepsilon_1\, e^{i(\delta_S+\delta_D)}  \cos 2\varepsilon_1\, e^{2 i \delta_D} \end{pmatrix}
$$
The mixing angle $\varepsilon_1$ is a direct measure of the strength of the [tensor force](@entry_id:161961) in this channel.

### The Statistical Framework of Fitting

Having defined the theoretical model and its connection to observables, the fitting process aims to find the set of potential parameters $\mathbf{p}$ that best reproduces a set of experimental data $\mathbf{d}$. Assuming the experimental errors follow a Gaussian distribution, the optimal parameters are found by minimizing a **generalized chi-squared function**, $\chi^2$.

In a realistic analysis, data from multiple experiments are combined. These datasets may have different [systematic uncertainties](@entry_id:755766), including overall normalization factors. Furthermore, uncertainties within a single dataset are often correlated. A robust $\chi^2$ must account for these features. For a data vector $\mathbf{d}$ and a model prediction vector $\mathbf{m}(\mathbf{p})$, the generalized $\chi^2$ is a [quadratic form](@entry_id:153497) involving the inverse of the **covariance matrix** $\mathbf{C}$:
$$
\chi^2(\mathbf{p}) = \left(\mathbf{d} - \mathbf{m}(\mathbf{p})\right)^T \mathbf{C}^{-1} \left(\mathbf{d} - \mathbf{m}(\mathbf{p})\right)
$$
The covariance matrix $\mathbf{C}$ contains the variances of the data points on its diagonal and the covariances between data points on its off-diagonals. For independent experiments, $\mathbf{C}$ takes a block-[diagonal form](@entry_id:264850).

Often, an experiment has an overall normalization uncertainty, which can be modeled by introducing a floating normalization parameter $\nu_j$ that multiplies the theoretical prediction for that dataset. These parameters are treated as additional fit parameters, but they are constrained by a **penalty term** in the $\chi^2$ function. This term corresponds to a Bayesian prior, typically a Gaussian centered at 1 with a standard deviation given by the experimental normalization uncertainty $\sigma_{\nu_j}$. The full [objective function](@entry_id:267263) to be minimized with respect to both $\mathbf{p}$ and the normalization parameters $\boldsymbol{\nu}$ becomes :
$$
\chi^2(\mathbf{p},\boldsymbol{\nu}) = \sum_{j=1}^{J} \left[ \left(\mathbf{d}_j - \nu_j\mathbf{m}_j(\mathbf{p})\right)^T \mathbf{C}_j^{-1} \left(\mathbf{d}_j - \nu_j\mathbf{m}_j(\mathbf{p})\right) + \left(\frac{\nu_j-1}{\sigma_{\nu_j}}\right)^2 \right]
$$
where the sum is over the $J$ experiments. For a fixed set of potential parameters $\mathbf{p}$, this expression is a simple quadratic in each $\nu_j$, allowing for an analytic solution for the optimal normalization parameter $\hat{\nu}_j(\mathbf{p})$. Substituting this solution back into the $\chi^2$ yields a profiled $\chi^2$ that depends only on $\mathbf{p}$, which can then be minimized numerically.

### Complications and Advanced Concepts

#### Scattering of Charged Particles

When scattering charged particles, such as in proton-proton or proton-nucleus scattering, the long-range Coulomb potential $V_C(r) = \alpha/r$ must be included alongside the short-range [nuclear potential](@entry_id:752727) $V_N(r)$. The long range of the Coulomb force fundamentally alters the [asymptotic behavior](@entry_id:160836) of the wave function; it never becomes a simple sine wave. Instead, the solutions in the region where $V_N(r)$ is negligible are the regular and irregular **Coulomb functions**, $F_l(\eta, kr)$ and $G_l(\eta, kr)$, where $\eta$ is the dimensionless **Sommerfeld parameter**.

To isolate the effects of the short-range [nuclear force](@entry_id:154226), the total phase shift is separated into a known part from the pure Coulomb interaction, $\sigma_l(\eta)$, and an additional shift, $\delta_l^N$, caused by the [nuclear potential](@entry_id:752727). The asymptotic form of the full [radial wave function](@entry_id:156768) is written as a phase-shifted combination of the Coulomb basis functions:
$$
u_l(r) \xrightarrow[r\to\infty]{} A_l\left[F_l(\eta,kr)\cos\delta_l^N+G_l(\eta,kr)\sin\delta_l^N\right]
$$
This leads to a total phase shift that is the sum of the two contributions, $\delta_l^{\text{total}} = \sigma_l(\eta) + \delta_l^N$. The full S-[matrix element](@entry_id:136260) is then given by $S_l = e^{2i(\sigma_l(\eta) + \delta_l^N)}$ . In a fit, one solves the Schrödinger equation with both potentials and extracts $\delta_l^N$ to compare with experimental data.

#### Inelasticity and Optical Potentials

At sufficiently high energies, it becomes possible to excite the target nucleus or produce new particles (like pions). These processes remove flux from the elastic scattering channel. This loss of flux is called **inelasticity** or absorption. The S-matrix element is no longer unitary in the elastic channel alone; its modulus becomes less than one. This is parameterized by introducing a real **inelasticity parameter** $\eta_l$:
$$
S_l = \eta_l e^{2i\delta_l}, \quad \text{with } 0 \le \eta_l \le 1
$$
The quantity $1-\eta_l^2$ represents the probability of reaction for that partial wave. To model such absorption, the potential itself must be made complex. This is the **[optical potential](@entry_id:156352)**, $U(r) = V_R(r) + iV_I(r)$, where the imaginary part $V_I(r)$ (conventionally negative) accounts for the loss of flux.

The presence of inelasticity has profound consequences for the other scattering quantities. The single-channel K-matrix, which was real in the elastic case, now becomes complex. For example, using the measured values $k=1.2\,\mathrm{fm}^{-1}$, $\delta_1=20^\circ$, and $\eta_1=0.85$ for a [p-wave](@entry_id:753062) channel, one can calculate the complex K-matrix to be $K_1 \approx (0.30 + i\,0.077)\,\mathrm{fm}$ . Furthermore, the low-energy [effective range expansion](@entry_id:137491) (ERE) must be generalized. The quantity $k^{2l+1}\cot\delta_l$ is no longer analytic. The proper generalization involves a complex phase shift, $\Delta_l = \delta_l - \frac{i}{2}\ln\eta_l$, and the expansion of $k^{2l+1}\cot\Delta_l$ leads to complex scattering lengths and effective ranges, whose imaginary parts encode the strength of absorption at low energy .

#### Phase Equivalence and Off-Shell Ambiguity

A fundamental challenge in [fitting potentials](@entry_id:749431) is the problem of non-uniqueness. It is possible to construct different potentials that produce the exact same [phase shifts](@entry_id:136717) at all energies and therefore predict identical [two-body scattering](@entry_id:144358) observables. Such potentials are called **phase-equivalent**. This ambiguity arises because two-body [observables](@entry_id:267133) are determined by the [asymptotic behavior](@entry_id:160836) of the [wave function](@entry_id:148272). One can apply a short-range [unitary transformation](@entry_id:152599) to the potential, which alters its form and the [wave function](@entry_id:148272) at short distances but leaves the asymptotic behavior—and thus all [phase shifts](@entry_id:136717)—unchanged .

While these potentials are indistinguishable in two-body elastic scattering, their predictions for other systems can differ. The differences are captured by the **off-shell** behavior of the T-matrix. The T-[matrix elements](@entry_id:186505) $\langle \mathbf{k}' | T(E) | \mathbf{k} \rangle$ are "on-shell" when the initial and final momenta correspond to the energy $E$ (i.e., $E = k^2/(2\mu) = k'^2/(2\mu)$). Observables in systems with three or more bodies, such as the [triton binding energy](@entry_id:756183) or nucleon-[deuteron](@entry_id:161402) scattering, involve intermediate states where the interacting pair is off-shell. These [observables](@entry_id:267133) are therefore sensitive to the off-shell properties of the T-matrix, which differ among phase-equivalent potentials. Comparing predictions for [few-body systems](@entry_id:749300) to data is therefore a crucial tool for distinguishing between and refining candidate nuclear potentials . In principle, formal [inverse scattering theory](@entry_id:200099) states that a unique local potential can be determined from the complete set of phase shifts and bound-state information, but the practical limitations of finite and imprecise data mean that ambiguity always remains .

### Modern Theoretical Frameworks

#### Chiral Effective Field Theory

Modern nuclear potentials are constructed within the framework of **Chiral Effective Field Theory (EFT)**. This approach builds the interaction systematically as an expansion in powers of $(Q/\Lambda_\chi)$, where $Q$ is a typical low momentum (like the pion mass) and $\Lambda_\chi$ is the "breakdown scale" of the theory. The potential consists of long-range pion exchanges, which are derived from the underlying theory of QCD, and a series of short-range contact terms with unknown coefficients called **Low-Energy Constants (LECs)**, which are fixed by fitting to data.

The pion-exchange potentials can be singular at the origin ($r \to 0$), requiring **regularization**. This is achieved by multiplying the potential by a [regulator function](@entry_id:754216), either in coordinate space (e.g., $f_R(r;R)$ which suppresses the potential for $r  R$) or in [momentum space](@entry_id:148936) (e.g., $f_\Lambda(k;\Lambda)$ which suppresses high-momentum components $k > \Lambda$). The physical results must be independent of this unphysical regulator. This is achieved through **renormalization**: the bare LECs are made to depend on the [cutoff scale](@entry_id:748127) ($\Lambda$ or $R$) in such a way that physical observables (like the [scattering length](@entry_id:142881)) remain constant. For instance, at leading order, the LEC $C_0$ must "run" with the cutoff as $C_0(\Lambda) \propto 1/\Lambda$ to cancel the linear divergence of [loop integrals](@entry_id:194719) .

The choice of regulator scale is not arbitrary. If the cutoff is chosen too low (a "soft" potential), it can interfere with and distort the well-understood long-range pion-exchange physics, biasing the fitted LECs . A key diagnostic is to vary the cutoff over a reasonable range and check that the variation in predicted observables is consistent with the estimated [truncation error](@entry_id:140949) of the EFT expansion. A large, unexpected sensitivity to the cutoff signals a problem with the calculation .

#### Causality and Dispersion Relations

For optical potentials that are energy-dependent, the principle of **causality**—that an effect cannot precede its cause—imposes a powerful constraint. Causality implies that the underlying nucleon self-energy, which the [optical potential](@entry_id:156352) represents, must be an [analytic function](@entry_id:143459) in the upper half of the [complex energy plane](@entry_id:203283). A direct mathematical consequence of this [analyticity](@entry_id:140716) is that the real and imaginary parts of the potential, $V_R(E)$ and $V_I(E)$, are not independent. They are related by [integral transforms](@entry_id:186209) known as **[dispersion relations](@entry_id:140395)** or Kramers-Kronig relations.

For nuclear optical potentials, a **subtracted [dispersion relation](@entry_id:138513)** is typically required for convergence:
$$
V_{R}(E)-V_{R}(E_{0})=\frac{1}{\pi}\,\mathcal{P}\! \int_{-\infty}^{\infty}\mathrm{d}E'\,V_{I}(E')\left(\frac{1}{E'-E}-\frac{1}{E'-E_{0}}\right)
$$
where $\mathcal{P}$ denotes the Cauchy [principal value](@entry_id:192761) and $E_0$ is an arbitrary subtraction energy . This relation links the energy dependence of the real potential to an integral over the imaginary (absorptive) potential at all energies. A **Dispersive Optical Model (DOM)** is a sophisticated fitting approach that enforces this causality constraint. In a DOM fit, one parameterizes the [imaginary potential](@entry_id:186347) $V_I(E)$ and uses the [dispersion relation](@entry_id:138513) to generate the energy-dependent part of the real potential $V_R(E)$. This greatly reduces the model's free parameters and ensures a more physical and predictive description of scattering over a wide energy range .