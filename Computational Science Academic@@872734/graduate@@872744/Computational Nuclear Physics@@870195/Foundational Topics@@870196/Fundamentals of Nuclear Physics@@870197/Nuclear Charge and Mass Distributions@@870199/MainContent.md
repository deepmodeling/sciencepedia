## Introduction
The spatial arrangement of protons and neutrons within an atomic nucleus, described by its charge and mass distributions, is one of its most fundamental properties. A precise understanding of these distributions is essential for deciphering the complex [nuclear many-body problem](@entry_id:161400), constraining the nature of the nuclear force, and modeling astrophysical objects like neutron stars. However, describing these distributions requires moving beyond simple classical pictures and bridging the gap between the microscopic quantum world of nucleons and the macroscopic quantities measured in the laboratory. This article addresses this challenge by providing a comprehensive theoretical and practical framework for understanding nuclear densities.

This article will guide you through a multi-faceted exploration of this topic. The first chapter, **"Principles and Mechanisms,"** establishes the fundamental formalism, starting from the quantum mechanical definition of one-body density operators and progressing to the physical charge and mass distributions probed by experiments. It details how to characterize these distributions and the crucial corrections needed for accurate theoretical modeling. The second chapter, **"Applications and Interdisciplinary Connections,"** explores how these concepts are realized in practice, detailing the experimental techniques used to measure densities and showing how this data provides stringent tests of [nuclear theory](@entry_id:752748) and connects to [atomic physics](@entry_id:140823) and astrophysics. Finally, the **"Hands-On Practices"** section offers opportunities to apply these principles through computational exercises, solidifying your understanding of how to model and interpret nuclear distributions.

## Principles and Mechanisms

This chapter delves into the fundamental principles that govern the spatial distribution of nucleons within a nucleus. We will formally define the concepts of nuclear charge and mass densities, explore their mathematical properties, and establish the connection between these theoretical constructs and experimentally observable quantities. Furthermore, we will examine the key mechanisms—including the finite size of nucleons, [relativistic effects](@entry_id:150245), and internucleon correlations—that shape these distributions and reveal the rich inner structure of the atomic nucleus.

### Defining Nuclear Densities

The starting point for any discussion of [nuclear structure](@entry_id:161466) is a precise definition of how protons and neutrons are distributed in space. These distributions, or densities, are the primary outputs of many theoretical models and the primary inputs for calculating a wide range of nuclear properties and reaction [observables](@entry_id:267133).

#### One-Body Density Operators

In non-relativistic quantum mechanics, a nucleus containing $A$ nucleons is described by a many-body wave function, $|\Psi\rangle$. The **one-body [number density](@entry_id:268986)**, often called the [matter density](@entry_id:263043), reflects the probability of finding any nucleon at a specific point in space, $\mathbf{r}$. It is formally defined as the expectation value of the one-body [density operator](@entry_id:138151), $\hat{\rho}(\mathbf{r})$:

$$
\rho(\mathbf{r}) = \langle\Psi|\hat{\rho}(\mathbf{r})|\Psi\rangle = \left\langle\Psi\left| \sum_{i=1}^{A} \delta(\mathbf{r}-\hat{\mathbf{r}}_i) \right|\Psi\right\rangle
$$

where $\hat{\mathbf{r}}_i$ is the position operator for the $i$-th nucleon and the sum runs over all $A$ nucleons. Due to the indistinguishability of identical nucleons, this expression can be simplified. For an [antisymmetric wave function](@entry_id:153884) $\Psi(\mathbf{x}_1, \dots, \mathbf{x}_A)$, where $\mathbf{x}_i = (\mathbf{r}_i, s_i, t_i)$ includes spatial, spin, and isospin coordinates, the one-body density can be expressed by integrating out all but one coordinate:

$$
\rho(\mathbf{r}) = A \int d\mathbf{x}_2 \cdots d\mathbf{x}_A |\Psi(\mathbf{r}, s_1, t_1, \mathbf{x}_2, \dots, \mathbf{x}_A)|^2
$$

where the integral implies summation over all spin and [isospin](@entry_id:156514) variables. By integrating the density over all space, we recover the total number of nucleons, which serves as its [normalization condition](@entry_id:156486):

$$
\int \rho(\mathbf{r}) \,d^3r = \left\langle\Psi\left| \sum_{i=1}^{A} \int \delta(\mathbf{r}-\hat{\mathbf{r}}_i) \,d^3r \right|\Psi\right\rangle = \langle\Psi|A|\Psi\rangle = A
$$

This formulation treats nucleons as point-like particles. This **point-nucleon density** is a crucial theoretical construct that we will build upon. [@problem_id:3573930]

#### Formalism in First and Second Quantization

To distinguish between protons and neutrons, we employ the **isospin** formalism. The third component of the isospin operator, $\hat{\tau}_3$, has an eigenvalue of $+1$ for protons and $-1$ for neutrons. We can thus define [projection operators](@entry_id:154142) for protons, $\hat{P}_p = (1+\hat{\tau}_3)/2$, and for neutrons, $\hat{P}_n = (1-\hat{\tau}_3)/2$. Applying these projectors within the density operator allows us to define the **point-proton density** $\rho_p(\mathbf{r})$ and **point-neutron density** $\rho_n(\mathbf{r})$:

$$
\rho_p(\mathbf{r}) = \left\langle\Psi\left| \sum_{i=1}^{A} \frac{1+\hat{\tau}_{3,i}}{2} \delta(\mathbf{r}-\hat{\mathbf{r}}_i) \right|\Psi\right\rangle
$$

$$
\rho_n(\mathbf{r}) = \left\langle\Psi\left| \sum_{i=1}^{A} \frac{1-\hat{\tau}_{3,i}}{2} \delta(\mathbf{r}-\hat{\mathbf{r}}_i) \right|\Psi\right\rangle
$$

These densities are normalized to the proton number $Z$ and neutron number $N$, respectively, i.e., $\int \rho_p(\mathbf{r}) d^3r = Z$ and $\int \rho_n(\mathbf{r}) d^3r = N$. The total number density is simply their sum: $\rho(\mathbf{r}) = \rho_p(\mathbf{r}) + \rho_n(\mathbf{r})$. [@problem_id:3573925] [@problem_id:3573930]

While the first-quantization picture is intuitive, modern [many-body theory](@entry_id:169452) is predominantly formulated in the language of **[second quantization](@entry_id:137766)**. Here, the fundamental objects are [field operators](@entry_id:140269) $\psi_{s,t}(\mathbf{r})$ that annihilate a nucleon with [spin projection](@entry_id:184359) $s$ and isospin projection $t$ at position $\mathbf{r}$. The total number [density operator](@entry_id:138151) is expressed as a bilinear product of these fields, summed over all internal degrees of freedom:

$$
\hat{\rho}(\mathbf{r}) = \sum_{s,t} \psi^\dagger_{s,t}(\mathbf{r}) \psi_{s,t}(\mathbf{r}) \equiv \psi^\dagger(\mathbf{r})\psi(\mathbf{r})
$$

The proton and neutron density operators are constructed by inserting the isospin projectors between the [field operators](@entry_id:140269):

$$
\hat{\rho}_p(\mathbf{r}) = \psi^\dagger(\mathbf{r}) \frac{1+\tau_3}{2} \psi(\mathbf{r})
$$

$$
\hat{\rho}_n(\mathbf{r}) = \psi^\dagger(\mathbf{r}) \frac{1-\tau_3}{2} \psi(\mathbf{r})
$$

The spatial densities are the [expectation values](@entry_id:153208) of these operators in the many-body ground state, $\rho_{p/n}(\mathbf{r}) = \langle\Psi|\hat{\rho}_{p/n}(\mathbf{r})|\Psi\rangle$. This formalism is particularly powerful for theoretical developments and is the standard in advanced computational methods. [@problem_id:3573935]

#### Physical Admissibility of Density Functions

Any physically realistic nuclear density function $\rho(r)$, particularly those given by analytical parametrizations, must satisfy several fundamental mathematical requirements. For a spherically symmetric nucleus with proton number $Z$, a [charge density](@entry_id:144672) $\rho_c(r)$ must be:
1.  **Non-negative**: $\rho_c(r) \ge 0$ for all $r \ge 0$, as probability density cannot be negative.
2.  **Normalizable**: The total charge must be finite and equal to $Ze$. This means the integral $4\pi \int_0^\infty r^2 \rho_c(r) dr$ must converge to $Ze$.
3.  **Asymptotically Vanishing**: The density must decay to zero at large distances, $\rho_c(r \to \infty) \to 0$. However, this condition alone is not sufficient for normalizability; the density must decay fast enough. For instance, a decay slower than $1/r^3$ would lead to a divergent integral for the total charge.
4.  **Finite Moments**: Key physical observables, like the root-mean-square (RMS) radius, depend on moments of the distribution. For the RMS radius to be finite, the integral $\int_0^\infty r^4 \rho_c(r) dr$ must converge. This imposes an even stricter condition on the asymptotic decay of the density (faster than $1/r^5$).

These constraints are crucial for validating theoretical models and fitting parametrizations to experimental data. For example, a parametrized function like $\rho(r) = \rho_0(1+\alpha r^2)^p \exp[-(r/R)^q]$ is physically admissible only in specific regimes of its parameters $(\alpha, p, q)$ that ensure all these conditions are met. The presence of a decaying exponential term (for $q > 0$) guarantees convergence for any polynomial part, while a purely [power-law decay](@entry_id:262227) (for $q \le 0$) imposes strong constraints on the exponent $p$. [@problem_id:3573953]

### From Point-Nucleon Distributions to Physical Observables

The point-nucleon densities $\rho_p(\mathbf{r})$ and $\rho_n(\mathbf{r})$ are theoretical abstractions. The actual distributions of charge and mass that are probed experimentally are "smeared out" by the fact that nucleons themselves are not point particles.

#### The Role of Finite Nucleon Size

The physical **nuclear [charge density](@entry_id:144672)**, $\rho_c(\mathbf{r})$, is the quantity that acts as the source for the electric field of the nucleus. It is not identical to the point-proton density $\rho_p(\mathbf{r})$. To obtain the physical charge density, one must fold, or convolute, the point-nucleon distributions with the intrinsic charge distributions of the proton and neutron themselves. Let these intrinsic profiles be $G_p(\mathbf{s})$ and $G_n(\mathbf{s})$. The total [charge density](@entry_id:144672) is then given by:

$$
\rho_c(\mathbf{r}) = \int d^3s \left[ G_p(\mathbf{s}) \rho_p(\mathbf{r}-\mathbf{s}) + G_n(\mathbf{s}) \rho_n(\mathbf{r}-\mathbf{s}) \right]
$$

The intrinsic profiles are normalized to the total charge of the nucleon: $\int G_p(\mathbf{s}) d^3s = e$ and $\int G_n(\mathbf{s}) d^3s = 0$. While the neutron has zero net charge, its intrinsic [charge distribution](@entry_id:144400) $G_n(\mathbf{s})$ is not identically zero. Due to its quark substructure, the neutron possesses a complex internal landscape of positive and negative charge regions. Therefore, the convolution with the point-neutron density $\rho_n(\mathbf{r})$ yields a non-zero contribution to the local shape of the nuclear [charge density](@entry_id:144672) $\rho_c(\mathbf{r})$. Neglecting this neutron contribution is an approximation that is often not justified. [@problem_id:3573925]

Similarly, the physical **nuclear mass density** $\rho_M(\mathbf{r})$ can be defined. To a good approximation, one can neglect the small proton-neutron mass difference and the internal [mass distribution](@entry_id:158451) of the nucleons. In this case, the mass density is directly proportional to the total number density: $\rho_M(\mathbf{r}) \approx m_N \rho(\mathbf{r})$, where $m_N$ is the average nucleon mass. A more precise treatment involves a convolution similar to that for the charge density, using intrinsic mass profiles for the proton and neutron. [@problem_id:3573930]

#### Form Factors: The Momentum-Space Perspective

Elastic [electron scattering](@entry_id:159023) is a primary tool for measuring charge distributions. In such experiments, the relevant quantity is the Fourier transform of the [charge density](@entry_id:144672), known as the **charge form factor**, $F_c(\mathbf{q}) = \int e^{i\mathbf{q}\cdot\mathbf{r}} \rho_c(\mathbf{r}) d^3r$, where $\mathbf{q}$ is the [momentum transfer](@entry_id:147714).

The convolution theorem of Fourier analysis states that the Fourier transform of a convolution is the product of the individual Fourier transforms. Applying this to the expression for $\rho_c(\mathbf{r})$ yields a simple multiplicative relation in [momentum space](@entry_id:148936):

$$
F_c(\mathbf{q}) = \mathcal{F}[G_p] \mathcal{F}[\rho_p] + \mathcal{F}[G_n] \mathcal{F}[\rho_n]
$$

The Fourier transforms of the intrinsic nucleon charge distributions are the **nucleon electric form factors**, $G_E^p(q^2)$ and $G_E^n(q^2)$, where $q = |\mathbf{q}|$. The Fourier transforms of the point-nucleon densities are the **point-[nucleon form factors](@entry_id:158723)**, $F_p(\mathbf{q})$ and $F_n(\mathbf{q})$. Thus, the nuclear charge [form factor](@entry_id:146590) is given by:

$$
F_c(\mathbf{q}) = G_E^p(q^2) F_p(\mathbf{q}) + G_E^n(q^2) F_n(\mathbf{q})
$$

This fundamental equation connects the microscopic point-[nucleon structure](@entry_id:160247) computed from a nuclear model ($F_{p,n}$) to the observable [nuclear form factor](@entry_id:158297) ($F_c$) by incorporating the known electromagnetic structure of the nucleons themselves ($G_E^{p,n}$). [@problem_id:3573930] [@problem_id:3573935]

### Characterizing Nuclear Distributions

To compare different nuclei or to test theoretical models, we need quantitative measures to characterize the shape and size of density distributions.

#### Radial Moments and the Mean-Square Radius

For a given distribution $\rho(\mathbf{r})$, its **n-th radial moment** is defined as the expectation value of $r^n$:

$$
\langle r^n \rangle = \frac{\int r^n \rho(\mathbf{r}) d^3r}{\int \rho(\mathbf{r}) d^3r}
$$

The most important of these is the second moment ($n=2$), which defines the **mean-square radius**, $\langle r^2 \rangle$. Its square root, $\sqrt{\langle r^2 \rangle}$, is the **root-mean-square (RMS) radius**, a standard measure of the size of the distribution.

These moments are directly linked to the behavior of the [form factor](@entry_id:146590) at low [momentum transfer](@entry_id:147714). By expanding the Fourier transform for small $q$, one can show a direct relationship between the mean-square charge radius and the slope of the charge [form factor](@entry_id:146590) at the origin:

$$
\langle r^2 \rangle_c = -6 \left. \frac{d F_c(q^2)}{d(q^2)} \right|_{q^2=0}
$$

where it is assumed the [form factor](@entry_id:146590) is normalized such that $F_c(0)=1$. This relation is pivotal, as it allows the experimental determination of the charge radius from the low-$q$ behavior of the elastic electron [scattering cross section](@entry_id:150101). [@problem_id:3573974]

#### Decomposition of the Nuclear Charge Radius

A precise understanding of the [nuclear charge radius](@entry_id:174675) requires accounting for all contributing physical effects. The experimentally measured mean-square charge radius, $\langle r^2 \rangle_c$, can be decomposed into several distinct terms. A widely used formula, particularly at low momentum transfer, is:

$$
\langle r^2 \rangle_c = \langle r^2 \rangle_p + r_p^2 + \frac{N}{Z} r_n^2 + \delta_{\text{rel}} + \delta_{\text{other}}
$$

Let us dissect each term:
-   $\langle r^2 \rangle_p$: This is the mean-square radius of the point-proton distribution, $\rho_p(\mathbf{r})$. It reflects the spatial extent of the protons due to nuclear dynamics alone.
-   $r_p^2$: This is the intrinsic mean-square charge radius of a single proton, accounting for its finite size ($r_p^2 \approx 0.7 \text{ fm}^2$). It is obtained from the slope of the proton's [electric form factor](@entry_id:160163), $r_p^2 = -6 dG_E^p/dq^2|_{q^2=0}$.
-   $\frac{N}{Z} r_n^2$: This is the contribution from the intrinsic structure of the $N$ neutrons. The factor $N/Z$ accounts for the number of neutrons relative to protons. The neutron's intrinsic mean-square charge radius is small and negative ($r_n^2 \approx -0.11 \text{ fm}^2$), reflecting its internal charge configuration.
-   $\delta_{\text{rel}}$: This represents [relativistic corrections](@entry_id:153041). The most significant of these is the **Darwin-Foldy term**, which arises from the [quantum localization](@entry_id:181245) of a relativistic particle and contributes approximately $3\hbar^2/(4M_p^2c^2)$ to the radius, where $M_p$ is the proton mass.
-   $\delta_{\text{other}}$: This term lumps together smaller corrections, such as those from spin-orbit interactions and two-body [meson-exchange currents](@entry_id:158298), which go beyond the simple [impulse approximation](@entry_id:750576).

This decomposition is essential for connecting the results of computational models, which typically calculate $\langle r^2 \rangle_p$, to the experimentally measured $\langle r^2 \rangle_c$. [@problem_id:3573974]

### Corrections and Advanced Models

Accurate computational modeling of nuclear densities requires careful treatment of several subtle but important physical effects.

#### Relativistic Corrections to the Charge Density

In a relativistic description, such as a Relativistic Mean-Field (RMF) model, nucleons are described by four-component Dirac spinors. The spinor has large ("upper") and small ("lower") two-component parts. In the [non-relativistic limit](@entry_id:183353), the lower component vanishes and the upper component becomes the familiar Schrödinger wavefunction. However, for a nucleon moving in the strong fields inside a nucleus, the lower component is small but non-zero.

The nuclear [charge density](@entry_id:144672) in this framework is proportional to the [scalar density](@entry_id:161438) $\psi^\dagger\psi = |G(r)|^2 + |F(r)|^2$, where $G(r)$ and $F(r)$ are the radial parts of the upper and lower components, respectively. The lower component's contribution, $|F(r)|^2$, is a purely [relativistic correction](@entry_id:155248). A non-relativistic reduction shows that, to leading order, the lower component is related to the gradient of the upper component:

$$
F(r) \approx \frac{\hbar c}{2Mc^2} \left[ \frac{dG(r)}{dr} + \frac{\kappa}{r}G(r) \right]
$$

where $\kappa$ is the relativistic [angular momentum quantum number](@entry_id:172069). Because the lower component's contribution is additive and always positive, its inclusion slightly increases the total normalization and typically leads to a small increase in the calculated RMS radius compared to a purely non-relativistic treatment that considers only the upper component. [@problem_id:3573937]

#### Center-of-Mass Corrections in Shell-Model Calculations

Many [nuclear structure models](@entry_id:161085), such as the [nuclear shell model](@entry_id:155646), are formulated in a coordinate system fixed in the laboratory. The wavefunctions produced by such calculations are not translationally invariant and contain a spurious motion of the nucleus's center of mass (CM). This unphysical motion artificially inflates the size of the nucleus.

To obtain a physically meaningful intrinsic density, this CM motion must be removed. In models based on a Harmonic Oscillator (HO) basis, this correction can be elegantly formulated. The laboratory-frame wavefunction, $|\Psi_{\text{lab}}\rangle$, can be factorized into an intrinsic part, $|\Psi_{\text{int}}\rangle$, and a part describing the CM motion, $|\Phi_{\text{cm}}\rangle$. The lab-frame density is then a convolution of the intrinsic density with the density of the CM. Consequently, the relationship between the form factors is multiplicative:

$$
F_{\text{lab}}(q) = F_{\text{int}}(q) \cdot F_{\text{cm}}(q)
$$

If the CM is in its HO ground state (a common approximation), its [form factor](@entry_id:146590) is a Gaussian, $F_{\text{cm}}(q) = \exp(-q^2b^2/4A)$, where $b$ is the HO length parameter. The intrinsic form factor, which is the physically relevant quantity, is then obtained by "deconvolving" this Gaussian smearing:

$$
F_{\text{int}}(q) = F_{\text{lab}}(q) \exp\left(+\frac{q^2b^2}{4A}\right)
$$

This directly translates to an additive correction for the mean-square radii. The lab-frame radius is the sum of the intrinsic and CM radii: $\langle r^2 \rangle_{\text{lab}} = \langle r^2 \rangle_{\text{int}} + \langle R_{\text{cm}}^2 \rangle$. The intrinsic radius is therefore:

$$
\langle r^2 \rangle_{\text{int}} = \langle r^2 \rangle_{\text{lab}} - \langle R_{\text{cm}}^2 \rangle = \langle r^2 \rangle_{\text{lab}} - \frac{3b^2}{2A}
$$

Neglecting this correction leads to a systematic overestimation of the [nuclear radius](@entry_id:161146). Applying it is a critical step in comparing shell-model calculations with experimental data. [@problem_id:3573982]

### Probing Nuclear Structure and Correlations

The details of charge and mass distributions provide a powerful window into the underlying nuclear dynamics, including the properties of the [nuclear force](@entry_id:154226) and the nature of correlations.

#### The Neutron Skin and the Symmetry Energy

In [neutron-rich nuclei](@entry_id:159170) ($N > Z$), the neutron and proton distributions are not identical. The **[neutron skin thickness](@entry_id:752466)**, $\Delta r_{np}$, is defined as the difference between the RMS radii of the point-neutron and point-proton distributions:

$$
\Delta r_{np} \equiv \sqrt{\langle r^2 \rangle_n} - \sqrt{\langle r^2 \rangle_p}
$$

The formation of a [neutron skin](@entry_id:159530) is a delicate balance of competing effects. The **[nuclear symmetry energy](@entry_id:161344)**, a term in the [nuclear equation of state](@entry_id:159900) that quantifies the energy cost of having an unequal number of protons and neutrons, creates a "symmetry pressure". This pressure pushes the excess neutrons from the high-density interior towards the lower-density surface, favoring the formation of a neutron-rich skin. This outward push is counteracted by surface tension, which favors a compact nucleus.

The magnitude of the symmetry pressure is highly sensitive to the [density dependence](@entry_id:203727) of the symmetry energy. This dependence is characterized by the **slope parameter $L$**. Theoretical models consistently predict a strong positive correlation: a larger value of $L$ implies a steeper rise in symmetry energy with density, leading to a stronger symmetry pressure and, consequently, a thicker [neutron skin](@entry_id:159530). The measurement of $\Delta r_{np}$ in nuclei like $^{208}\text{Pb}$ is therefore a crucial experimental constraint on the [nuclear equation of state](@entry_id:159900), with significant implications for the properties of [neutron stars](@entry_id:139683). [@problem_id:3573975]

#### Distributions in Deformed Nuclei

While many nuclei are spherical or nearly spherical in their ground state, a large number exhibit a permanent non-spherical, or **deformed**, shape. For such nuclei, the charge and mass densities are no longer functions of only the [radial coordinate](@entry_id:165186) $r$, but also depend on the angles $(\theta, \phi)$.

A deformed density $\rho_c(\mathbf{r})$ is typically analyzed by expanding it in a basis of spherical harmonics $Y_{\lambda\mu}(\theta, \phi)$:

$$
\rho_c(r, \theta, \phi) = \sum_{\lambda=0}^{\infty} \sum_{\mu=-\lambda}^{\lambda} \rho_{\lambda\mu}(r) Y_{\lambda\mu}(\theta, \phi)
$$

The radial functions $\rho_{\lambda\mu}(r)$ are the **multipole components** of the density. Nuclear symmetries impose strong constraints on this expansion. For a nucleus with [axial symmetry](@entry_id:173333) about the $z$-axis, only terms with $\mu=0$ survive. If the nucleus also has reflection symmetry (invariance under spatial inversion $\mathbf{r} \to -\mathbf{r}$), the property $Y_{\lambda\mu}(\pi-\theta, \phi+\pi) = (-1)^\lambda Y_{\lambda\mu}(\theta, \phi)$ dictates that only even values of $\lambda$ are allowed.

The $\lambda=0$ term, $\rho_{00}(r)$, represents the spherically-averaged part of the density. The $\lambda=2$ term, $\rho_{20}(r)$, describes the [quadrupole deformation](@entry_id:753914), which is responsible for the nucleus's electric quadrupole moment, $Q_2$. This moment is proportional to the [quadrupole moment](@entry_id:157717) of the density distribution, which is calculated as follows:
$$ \int r^2 Y_{20}(\theta, \phi) \rho_c(\mathbf{r}) d^3r = \int_0^\infty r^4 \rho_{20}(r) dr $$

This [multipole expansion](@entry_id:144850) provides a systematic framework for quantifying the shape of [deformed nuclei](@entry_id:748278). [@problem_id:3573996]

#### Two-Body Correlations and the Pair Distribution Function

The one-body densities $\rho_p(\mathbf{r})$ and $\rho_n(\mathbf{r})$ describe the average distribution of nucleons and are the central quantities in mean-field theories. However, they do not contain information about how the position of one nucleon affects the probability of finding another nearby. This information is encoded in the **two-body density**, $\rho^{(2)}(\mathbf{r}_1, \mathbf{r}_2)$, which is the joint probability of finding a nucleon at $\mathbf{r}_1$ and another at $\mathbf{r}_2$.

Correlations are quantified by the **[pair distribution function](@entry_id:145441)**, $g(r)$, which compares the true two-body density to that of an uncorrelated system. For a finite nucleus, a suitable definition involves averaging over the center-of-mass of the pair:

$$
g(r) \approx \frac{\langle \rho^{(2)}(\mathbf{R}+\mathbf{r}/2, \mathbf{R}-\mathbf{r}/2) \rangle_{\mathbf{R}}}{\langle \rho(\mathbf{R}+\mathbf{r}/2)\rho(\mathbf{R}-\mathbf{r}/2) \rangle_{\mathbf{R}}}
$$

where $\mathbf{r}$ is the relative separation and $\mathbf{R}$ is the center-of-mass coordinate. In the absence of correlations, $g(r) = 1$. The [nucleon-nucleon interaction](@entry_id:162177) features a strong repulsive core at short distances ($r \lesssim 0.5$ fm). This **short-range correlation (SRC)** makes it highly improbable to find two nucleons very close to each other, creating a "correlation hole" where $g(r) \to 0$ as $r \to 0$.

These strong correlations also have a noticeable effect on the one-body density itself. In [momentum space](@entry_id:148936), SRCs scatter nucleons from low-momentum states (within the Fermi sea) to high-momentum states. Since the low-momentum states are primarily responsible for the density in the nuclear interior, this scattering process leads to a depletion of the central one-body density. To conserve the total number of nucleons, this depletion is compensated by a slight enhancement of the density in the surface region. This redistribution of matter is a direct, observable consequence of the short-range part of the [nuclear force](@entry_id:154226), going beyond the simple mean-field picture. [@problem_id:3573984]