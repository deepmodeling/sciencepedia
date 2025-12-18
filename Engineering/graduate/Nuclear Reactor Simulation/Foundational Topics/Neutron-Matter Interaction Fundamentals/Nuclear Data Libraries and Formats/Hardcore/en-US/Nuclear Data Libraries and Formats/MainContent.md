## Introduction
Accurate and predictive simulation of nuclear systems, from commercial power reactors to advanced fusion concepts, is fundamentally reliant on a vast repository of high-fidelity nuclear data. This data, which details the probabilities and outcomes of every possible neutron-nucleus interaction, forms the bedrock of modern [computational reactor physics](@entry_id:1122805). However, the sheer volume and complexity of this information present a significant challenge: how is this fundamental physical data organized, processed into a usable state, and applied to solve real-world engineering problems? This article bridges the gap between raw experimental data and practical simulation by providing a comprehensive overview of [nuclear data libraries](@entry_id:1128922) and formats.

This article is structured to guide you from foundational principles to practical application. The first chapter, **Principles and Mechanisms**, will dissect the structure of evaluated nuclear data files like ENDF-6, explaining the physical basis for [data representation](@entry_id:636977), including the sophisticated models for resonances, thermal motion, and fission. Next, the **Applications and Interdisciplinary Connections** chapter will demonstrate the complete workflow for processing this data into simulation-ready libraries for both continuous-energy and multigroup codes, highlighting its crucial role in reactor analysis, safety calculations, and coupled multi-physics problems. Finally, the **Hands-On Practices** section provides interactive problems that allow you to engage directly with the core concepts of data retrieval, validation, and unit handling, solidifying your understanding of these essential tools of nuclear engineering.

## Principles and Mechanisms

The accurate simulation of nuclear reactor behavior hinges on a vast and meticulously organized repository of fundamental physics data. These data, encompassing reaction probabilities (cross sections), energy and angular distributions of secondary particles, and fission characteristics, are the empirical and theoretical foundation upon which transport codes are built. After their introduction, we now delve into the core principles governing the structure, content, and processing of modern [nuclear data libraries](@entry_id:1128922). We will explore the mechanisms by which these libraries represent complex nuclear phenomena and how they are transformed into formats usable by state-of-the-art simulation tools.

### The Hierarchical Structure of Nuclear Data

To be useful for a computational code, nuclear data must be organized in a standardized, hierarchical, and unambiguous manner. A simulation must be able to retrieve a specific piece of information—for example, the elastic [scattering cross section](@entry_id:150101) for Uranium-235 at an incident neutron energy of $1\,\text{MeV}$—through a well-defined query. The **Evaluated Nuclear Data File (ENDF)** format, now in its sixth major version (ENDF-6), provides the internationally accepted standard for this organization.

The ENDF-6 format employs a three-tiered indexing system to uniquely identify any dataset. This hierarchy consists of the Material (MAT), the File (MF), and the Reaction Type (MT) identifiers .

*   **MAT (Material Number):** This is the highest-level identifier. Each MAT number corresponds to a complete set of evaluated data for a specific material. Most commonly, this material is a single nuclide (e.g., $^{235}\text{U}$ or $^{56}\text{Fe}$), but it can also represent a natural element with its isotopic composition or a specific material for [thermal scattering law](@entry_id:1133026) data (e.g., hydrogen bound in water).

*   **MF (File Number):** Within each MAT, data are partitioned into different "Files" according to the category of [physical information](@entry_id:152556). The MF number specifies the type of data being presented. For instance, MF=2 contains resonance parameters, MF=3 contains energy-dependent reaction cross sections, MF=4 contains angular distributions of secondary particles, and MF=6 contains combined energy-angle distributions.

*   **MT (Reaction Type Number):** Within a given (MAT, MF) pair, the data are further subdivided into "Sections" based on the specific reaction channel, identified by the MT number. The MT number specifies the physical process, such as MT=2 for [elastic scattering](@entry_id:152152), MT=18 for fission, or MT=102 for radiative capture.

The triplet $(\text{MAT}, \text{MF}, \text{MT})$ thus forms a unique key to a specific dataset. For example, the data for the angular distribution of elastically scattered neutrons from $^{235}\text{U}$ would be located by its unique $(\text{MAT}, \text{MF}, \text{MT})$ identifier. Within that section, the physical quantities are then tabulated as a function of incident neutron energy, $E$. Energy is treated as the [independent variable](@entry_id:146806) within a dataset, not as part of its identifying key .

### Physical Content and Reaction Channel Representation

The partitioning of reactions into distinct MT numbers is not merely a bookkeeping convention; it is a direct reflection of fundamental physical principles. In a neutron-nucleus interaction, the possible outcomes—[elastic scattering](@entry_id:152152), [inelastic scattering](@entry_id:138624), capture, fission, etc.—are **mutually exclusive**. A single interaction event results in one and only one of these final states. In the language of quantum mechanics, these distinct final states are represented by [orthogonal vectors](@entry_id:142226) in the Hilbert space of the system. A consequence of this orthogonality is that the total probability of an interaction is the sum of the probabilities of all possible exclusive outcomes, with no interference terms between them .

Since the microscopic cross section, $\sigma_r(E)$, for a reaction channel $r$ is proportional to its probability, the **total cross section**, $\sigma_{\text{tot}}(E)$, must be the sum of all partial cross sections for every open channel at that energy:

$$
\sigma_{\text{tot}}(E) = \sum_{r} \sigma_{r}(E)
$$

The ENDF format is structured to uphold this principle. Each exclusive channel is assigned its own MT number .

*   **MT=1 (Total Cross Section):** This represents $\sigma_{\text{tot}}(E)$ and, in a consistent evaluation, must equal the sum of all other partial reaction cross sections provided in the file, such as [elastic scattering](@entry_id:152152), all forms of [inelastic scattering](@entry_id:138624), capture, fission, and charged-particle emission reactions, within processing tolerances.

*   **MT=2 (Elastic Scattering):** This refers to the process $(n,n)$ where the neutron scatters from the target nucleus, conserving kinetic energy in the [center-of-mass frame](@entry_id:158134), and leaving the nucleus in its ground state. This standard representation models the target as a free particle, an assumption that breaks down at low energies, as we will see later.

*   **MT=102 (Radiative Capture):** This denotes the absorption reaction $(n,\gamma)$, where the incident neutron is absorbed to form a [compound nucleus](@entry_id:159470), which subsequently de-excites by emitting one or more gamma rays. This process is distinct from [inelastic scattering](@entry_id:138624), $(n,n')$, where a neutron is re-emitted and the resulting gamma rays are associated with that specific inelastic channel.

*   **MT=18 (Total Fission Cross Section):** This represents the total probability of fission, $\sigma_{(n,f)}(E)$. At higher incident energies, it includes the sum of all "multi-chance" fission probabilities, such as second-chance fission $(n,nf)$ and third-chance fission $(n,2nf)$. It is important to note that **fissile** nuclides like $^{235}\text{U}$ and $^{239}\text{Pu}$ can be fissioned by neutrons of any energy and have no fission threshold. In contrast, **fissionable** but non-fissile nuclides like $^{238}\text{U}$ have an effective energy threshold for fission, typically in the MeV range .

To ensure physical consistency, the ENDF format incorporates redundancy through **sum rules**. For example, the non-elastic cross section (MT=3) is explicitly defined as the total (MT=1) minus the elastic (MT=2). The total inelastic cross section (MT=4) is defined as the sum of all discrete and continuum inelastic channels (MT=51 through MT=91). Specialized checking codes are used to verify that these identities hold throughout an evaluated data file, ensuring that the library is self-consistent before it is used for further processing .

### Representing Energy Dependence: From Parameters to Pointwise Data

One of the most complex aspects of nuclear data is the representation of cross sections in the **resonance region**. Here, cross sections exhibit sharp, dramatic fluctuations with energy, corresponding to the formation of quasi-stable energy levels in the [compound nucleus](@entry_id:159470). Directly tabulating these rapidly varying functions would require an immense number of data points. Instead, [nuclear data libraries](@entry_id:1128922) leverage the physics of [nuclear reactions](@entry_id:159441), storing [compact sets](@entry_id:147575) of parameters that can be used to reconstruct the cross sections on an arbitrarily fine energy grid.

#### Resonance Reconstruction (Resolved Region)

In the **resolved resonance region (RRR)**, typically at lower neutron energies, individual resonances are sufficiently separated to be experimentally identified. Here, ENDF File 2 (MF=2) does not store cross sections directly but instead provides the parameters of a [nuclear reaction theory](@entry_id:752732) model, most commonly **R-[matrix theory](@entry_id:184978)**. These parameters include resonance energies ($E_{\lambda}$), spins and parities ($J^{\pi}$), and partial decay widths ($\Gamma_{\lambda c}$) or reduced widths ($\gamma_{\lambda c}$) for each resonance level $\lambda$ and each decay channel $c$ (e.g., neutron emission, [gamma emission](@entry_id:158176), fission) .

The process of converting these MF=2 parameters into the pointwise cross sections found in MF=3 is called **resonance reconstruction**. This is a sophisticated computational procedure that unfolds as follows:

1.  For a given incident neutron energy $E$, the code calculates **channel functions**: the **penetrability** $P_l(E)$, which describes the probability of a neutron with [orbital angular momentum](@entry_id:191303) $l$ overcoming the centrifugal (and possibly Coulomb) barrier to reach the nucleus, and the **shift function** $S_l(E)$.
2.  These are used to compute energy-dependent partial widths from the energy-independent reduced widths stored in the library (e.g., $\Gamma_{\lambda c}(E) = 2 P_l(E) \gamma_{\lambda c}^2$).
3.  Using the specified R-matrix formalism (e.g., Single-Level Breit-Wigner, Multi-Level Breit-Wigner, or the more rigorous Reich-Moore), the code assembles a "level matrix" or "collision matrix" that correctly accounts for interference effects between resonances.
4.  From this matrix, the reaction-specific cross sections are calculated using expressions derived from [scattering theory](@entry_id:143476), such as $\sigma_{ab}(E) = \frac{\pi}{k_a^2} g_a |T_{ab}(E)|^2$, where $T_{ab}$ is an element of the transmission matrix.
5.  This process is repeated on a dense, adaptively refined energy grid that places more points around the sharp peaks and deep valleys of resonances to ensure accurate interpolation. The resulting temperature-dependent pointwise cross sections are then stored in MF=3.

This reconstruction process is a powerful example of how data libraries encode fundamental physics in a compact form, which is then computationally "unpacked" into the detailed functions needed for simulation .

#### The Unresolved Resonance Region (URR)

As incident neutron energy increases, the density of nuclear levels grows, and resonances begin to overlap. Eventually, an energy is reached where individual resonances can no longer be experimentally resolved. This is the **[unresolved resonance region](@entry_id:1133614) (URR)**. In this region, the cross section at any specific energy point is effectively a random variable, governed by the statistical properties of the resonance parameters (e.g., average level spacing $\langle D \rangle$ and average widths $\langle \Gamma_x \rangle$) .

Simply using an average cross section over an energy group is insufficient because of the phenomenon of **self-shielding**. Within the URR, the neutron flux $\phi(E)$ is strongly anti-correlated with the total cross section $\sigma_t(E)$; the flux is depleted at energies corresponding to resonance peaks. The effective reaction rate depends on this detailed correlation. In a mixture of materials, the flux shape is approximately given by $\phi(E) \propto [\sigma_t(E) + \sigma_0]^{-1}$, where $\sigma_0$ is the microscopic **background cross section** that accounts for all other non-resonant cross sections in the material mixture.

To correctly model self-shielding in the URR, evaluated data libraries provide **probability tables**. Instead of defining the cross section as a function of energy, these tables define the probability distribution of the cross section values themselves within a given energy range. Crucially, because the partial cross sections for scattering, fission, and capture all arise from the same underlying resonances, they are not independent. Therefore, the library provides a *joint* probability distribution for the tuple $(\sigma_t, \sigma_s, \sigma_a, \nu, ...)$. By sampling from these tables, which are conditioned on the background cross section $\sigma_0$, a simulation code can accurately reproduce the statistical behavior of reaction rates and properly account for self-shielding effects .

#### The Role of Temperature: Doppler Broadening

The resonance parameters and reconstructed cross sections are typically evaluated for a target nucleus at rest (a temperature of $0\,\text{K}$). However, in a reactor operating at a temperature $T$, target nuclei are in constant thermal motion, described by the Maxwell-Boltzmann velocity distribution. This motion "blurs" the sharp resonances seen by an incident neutron, a phenomenon known as **Doppler broadening** .

The physical basis for this effect is that the reaction probability depends on the kinetic energy in the [center-of-mass frame](@entry_id:158134) (the relative energy), not the laboratory energy of the neutron. To find the [effective cross section](@entry_id:1124176) $\sigma_T(E)$ at a given lab energy $E$ and temperature $T$, one must average the $0\,\text{K}$ cross section $\sigma(E')$ over all possible relative energies $E'$ that can result from the thermal motion of the target nuclei.

Mathematically, this averaging process takes the form of a convolution:

$$
\sigma_T(E) = \int_{0}^{\infty} \sigma(E') G(E' \leftarrow E; T) \, dE'
$$

Here, $G(E' \leftarrow E; T)$ is the **broadening kernel**, which represents the probability distribution of relative energies $E'$ for a given lab energy $E$ and temperature $T$. This kernel is derived from the Maxwell-Boltzmann distribution and has several key properties: it is non-negative, normalized to unity, and its shape is approximately Gaussian in the variable $\sqrt{E}$, with a width that scales as $\sqrt{k_{\mathrm{B}} T}$. The process of Doppler broadening is a critical data processing step that must be performed to generate temperature-specific libraries for reactor analysis, as it is a primary mechanism for negative [reactivity feedback](@entry_id:1130661) and is essential for [reactor safety](@entry_id:1130677).

### Advanced Physics Models for Specific Energy Regimes

Beyond the general framework, [nuclear data libraries](@entry_id:1128922) incorporate specialized physics models for particular energy ranges and phenomena.

#### Thermal Scattering Law (TSL)

At very low neutron energies (the thermal range, typically below a few eV), the model of a [neutron scattering](@entry_id:142835) from a free, stationary nucleus (MT=2) breaks down completely. In this regime, the neutron's wavelength becomes comparable to interatomic distances, and its energy is on the order of the vibrational and rotational energies of atoms bound in molecules or a crystal lattice. The scattering interaction is no longer with a single nucleus but with the collective system, involving the exchange of quantized packets of vibrational energy called **phonons**.

To describe this complex interaction, evaluated data libraries include **Thermal Scattering Law (TSL)** data, often stored in MF=7. This information is derived from a theoretical framework developed by Van Hove and is encapsulated in the **[dynamic structure factor](@entry_id:143433)**, or its dimensionless form, the **[thermal scattering law](@entry_id:1133026), $S(\alpha, \beta)$** . The double-[differential cross section](@entry_id:159876), which gives the probability of scattering from energy $E$ to $E'$ into a solid angle element $d\Omega$, is directly proportional to this function:

$$
\frac{d^{2}\sigma}{dE'\,d\Omega} = \frac{\sigma_{b}}{4\pi\,k_{\mathrm{B}} T}\,\sqrt{\frac{E'}{E}}\,S(\alpha,\beta)
$$

Here, $\sigma_b$ is the characteristic bound [scattering cross section](@entry_id:150101) of the nucleus. The variables $\alpha$ and $\beta$ are dimensionless forms of momentum and energy transfer, respectively:

*   $\boldsymbol{\alpha}$ is the recoil energy a free nucleus would have received, normalized by the thermal energy $k_{\mathrm{B}} T$. It represents the squared **momentum transfer**.
*   $\boldsymbol{\beta}$ is the energy transferred to the neutron, $(E'-E)$, normalized by $k_{\mathrm{B}} T$. It represents the **energy transfer**.

The function $S(\alpha, \beta)$ contains all the information about the material's dynamic structure (e.g., its [phonon spectrum](@entry_id:753408)) and must satisfy a fundamental thermodynamic constraint known as the [principle of detailed balance](@entry_id:200508). This specialized data is essential for accurately modeling [neutron moderation](@entry_id:1128702) in materials like water, graphite, and beryllium  .

#### Fission Neutron Emission

The process of fission is unique in that it is a source of new neutrons that sustain the chain reaction. A data library must therefore describe not only the probability of fission ($\sigma_f(E)$, MT=18) but also the characteristics of the neutrons that are produced. Two key quantities are provided :

1.  **Average Neutron Multiplicity, $\bar{\nu}(E)$:** This is the average number of neutrons emitted per fission event induced by a neutron of energy $E$. $\bar{\nu}(E)$ is a crucial factor that determines the multiplication of neutrons in a system. It generally increases slowly with incident energy.

2.  **Prompt Fission Neutron Spectrum (PFNS), $\chi_p(E)$:** This is the probability density function for the energy $E$ of the neutrons emitted promptly during fission. It is normalized such that $\int_0^{\infty} \chi_p(E)\,dE = 1$. The PFNS is typically a broad spectrum with an average energy around $2\,\text{MeV}$. Common [parametric models](@entry_id:170911), such as the Watt spectrum, are used to represent this distribution.

Together, $\bar{\nu}(E)$ and $\chi_p(E)$ define the fission source term in the [neutron transport equation](@entry_id:1128709). The total rate of neutron production scales with $\int \bar{\nu}(E') \Sigma_f(E') \phi(E') dE'$, while the energy distribution of these newborn neutrons is given by $\chi_p(E)$. Both quantities are fundamental to the fission operator and directly determine the reactor's effective multiplication factor, $k_{\text{eff}}$ .

### Data Representation for Simulation: Continuous-Energy vs. Multigroup

Once the comprehensive physical data has been evaluated and stored in the ENDF format, it must be processed into a form usable by a simulation code. There are two primary paradigms for this .

The **continuous-energy (CE)** representation, also known as the pointwise representation, is used primarily by **Monte Carlo transport codes**. In this approach, the detailed, temperature-broadened, pointwise cross sections (reconstructed from MF=2 and tabulated in MF=3) are stored with interpolation rules. A Monte Carlo code tracks individual neutrons, each with a specific energy $E$. To determine the distance to the next collision or the outcome of that collision, the code evaluates the necessary cross sections directly at that precise energy $E$. This method implicitly and exactly (within the fidelity of the underlying data) captures fine-energy details like resonance self-shielding, as the physics emerges naturally from the simulation.

The **multigroup (MG)** representation is the standard for **deterministic transport codes** (e.g., [diffusion theory](@entry_id:1123718) or [discrete ordinates](@entry_id:1123828) methods). In this method, the continuous energy domain is partitioned into a finite number of discrete energy "groups." For each group $g$, a single effective "group constant" $\Sigma_{x,g}$ is generated for each reaction type $x$. This constant is defined by averaging the continuous-energy cross section over the energy group, weighted by an assumed neutron flux spectrum, $W(E)$:

$$
\Sigma_{x,g} \approx \frac{\int_{E_g}^{E_{g-1}} \Sigma_x(E) W(E) dE}{\int_{E_g}^{E_{g-1}} W(E) dE}
$$

A critical consequence is that **[multigroup cross sections](@entry_id:1128302) are not [fundamental physical constants](@entry_id:272808)**. They are problem-dependent quantities whose accuracy is contingent on how well the weighting spectrum $W(E)$ approximates the true flux in the specific problem being solved. Generating accurate group constants for the resonance region requires sophisticated self-shielding models to account for the flux depression effect. The MG method trades the explicit energy detail of the CE approach for computational speed, solving a [matrix equation](@entry_id:204751) for a small number of groups rather than tracking a vast number of particles through a continuous energy landscape .

### Quantifying Uncertainty: Covariance Data

Evaluated nuclear data are the product of measurements and theoretical modeling, both of which are subject to uncertainties. A modern data library is incomplete without a quantitative assessment of these uncertainties. This information is encoded in **covariance matrices**.

The **covariance function**, $C_{ij}(E,E')$, is the fundamental object for describing these uncertainties. It is defined as the [expectation value](@entry_id:150961) of the product of deviations from the mean for two quantities :

$$
C_{ij}(E,E') = \left\langle \left( \sigma_i(E) - \mu_i(E) \right) \left( \sigma_j(E') - \mu_j(E') \right) \right\rangle
$$

where $\mu_i(E) = \langle \sigma_i(E) \rangle$ is the mean (or evaluated) cross section for reaction $i$.

*   The diagonal elements, $C_{ii}(E,E)$, represent the **variance** (the square of the standard deviation) of the cross section $\sigma_i$ at energy $E$.
*   The off-diagonal elements, $C_{ij}(E,E')$, quantify **correlations**. If $i=j$, $C_{ii}(E,E')$ describes how an uncertainty at energy $E$ is correlated with an uncertainty at energy $E'$. If $i \neq j$, $C_{ij}(E,E')$ describes how an uncertainty in reaction $i$ is correlated with an uncertainty in reaction $j$. These correlations arise from shared experimental setups, theoretical models, or fundamental physical constraints.

In ENDF libraries, covariance data for cross sections are primarily stored in MF=33. This information is crucial for **[uncertainty quantification](@entry_id:138597) (UQ)** in reactor analysis. Using a methodology known as the "[sandwich rule](@entry_id:1131198)," the variance of any calculated reactor parameter $S$ that depends linearly on cross sections can be computed. For a response $S = \int \phi(E) \sum_i a_i \sigma_i(E) dE$, its variance is given by the [double integral](@entry_id:146721):

$$
\text{Var}(S) = \sum_{i,j} \iint \phi(E) \phi(E') a_i a_j C_{ij}(E,E') \, dE \, dE'
$$

The inclusion and use of covariance data represent a significant step towards a truly predictive simulation capability, allowing not just for the calculation of a nominal value but also for a rigorous estimate of its confidence interval.