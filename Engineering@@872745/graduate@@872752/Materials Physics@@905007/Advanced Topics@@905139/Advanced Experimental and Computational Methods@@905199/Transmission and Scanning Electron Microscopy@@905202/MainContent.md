## Introduction
Transmission Electron Microscopy (TEM) and Scanning Electron Microscopy (SEM) are cornerstones of modern research, providing unparalleled insights into the structure and properties of matter from the micrometer to the atomic scale. The power of these techniques, however, is matched by their complexity; generating and correctly interpreting high-quality data requires a deep understanding of the underlying physics. This article addresses this need by providing a comprehensive overview for graduate-level researchers. We will bridge the gap between abstract theory and practical application, equipping you with the knowledge to select the right technique, optimize experimental conditions, and avoid common pitfalls in data interpretation.

You will first explore the foundational **Principles and Mechanisms**, from the electron optics that guide the beam to the intricate electron-specimen interactions that generate contrast. Next, we will survey the diverse **Applications and Interdisciplinary Connections**, demonstrating how these principles are leveraged to solve real-world problems in materials science, biology, and beyond. Finally, a series of **Hands-On Practices** will allow you to apply these concepts to quantitative problems, solidifying your understanding of these transformative research tools.

## Principles and Mechanisms

This chapter delves into the fundamental principles and mechanisms that govern the operation of transmission and scanning electron microscopes. We will begin by exploring the principles of electron optics, which describe how electron beams are formed and guided. We will then examine the rich variety of interactions that occur when a high-energy electron beam strikes a specimen, as these interactions are the ultimate source of all signals and contrast. Finally, we will synthesize these concepts to understand the primary mechanisms of [image formation](@entry_id:168534) in both scanning and [transmission electron microscopy](@entry_id:161658), from diffraction and [phase contrast](@entry_id:157707) to modern [incoherent imaging](@entry_id:178214) techniques.

### Electron Optics: Guiding the Beam

The ability to form a finely focused probe or a highly magnified image with electrons hinges on the use of electron lenses. Unlike photons, charged electrons can be deflected by electric and magnetic fields. In modern electron microscopes, magnetic lenses are favored for high-energy electrons due to their superior optical properties and robustness.

#### Focusing with Magnetic Lenses

An axially symmetric [magnetic lens](@entry_id:185485) generates a static magnetic field $\mathbf{B}$ that is strongest near the lens center and decays to zero far from it. The motion of an electron with charge $q=-e$ and velocity $\mathbf{v}$ is dictated by the Lorentz force, $\mathbf{F} = q(\mathbf{v} \times \mathbf{B})$. A key consequence of this force law is that the magnetic field does no work on the electron, so the electron's kinetic energy and the magnitude of its momentum, $p$, remain constant.

To understand the focusing action, we can derive the trajectory of an electron traveling near the optical axis (the $z$-axis). In the **[paraxial approximation](@entry_id:177930)**, the electron's radial and azimuthal velocity components are much smaller than its axial velocity, which is approximately constant ($v_z \approx v$). Maxwell's equations constrain the magnetic field components near the axis. For a rotationally symmetric field, the radial component $B_r$ is related to the derivative of the axial component $B_z(z)$ by $B_r(r,z) \approx -\frac{r}{2}\frac{dB_z}{dz}$.

A fundamental result, known as **Busch's theorem**, can be derived from the azimuthal component of the [equation of motion](@entry_id:264286). It shows that for an electron entering the lens from a field-free region parallel to the axis, the induced angular velocity is $\dot{\phi} = -\frac{q B_z(z)}{2 \gamma m}$, where $\gamma m$ is the relativistic mass. This shows that the electron trajectory spirals through the lens.

Substituting this induced rotation into the radial [equation of motion](@entry_id:264286) and changing the independent variable from time $t$ to axial position $z$ (using $dt = dz/v$), we arrive at the **paraxial electron ray equation** [@problem_id:2867998]:
$$
r''(z) + \frac{e^2 B_z^2(z)}{4 p^2} r(z) = 0
$$
where $r(z)$ is the electron's radial position, primes denote differentiation with respect to $z$, and $p = \gamma m v$ is the constant [relativistic momentum](@entry_id:159500) of the electron. This equation is of the form $r''(z) + K(z)r(z) = 0$. The focusing strength, $K(z) = \frac{e^2 B_z^2(z)}{4 p^2}$, is proportional to the square of the axial magnetic field. Since $K(z)$ is always non-negative, the [radial acceleration](@entry_id:173091) is always directed towards the axis. This proves that a rotationally symmetric [magnetic lens](@entry_id:185485) is always a **converging lens** for charged particles.

In the **thin-lens approximation**, where the lens field is assumed to be highly localized, we can integrate the ray equation to find the change in the ray's slope. By doing so, we can derive the [focal length](@entry_id:164489) $f$ of the lens. For a ray entering parallel to the axis, the [focal length](@entry_id:164489) is the distance from the lens at which the ray crosses the axis. The result is [@problem_id:2867998]:
$$
\frac{1}{f} = \frac{e^2}{4 p^2} \int_{-\infty}^{\infty} B_z^2(z) dz
$$
This expression demonstrates that a stronger magnetic field (larger integral of $B_z^2$) or lower electron momentum (lower energy) results in a shorter [focal length](@entry_id:164489) and a more powerful lens.

#### The Fundamental Limit of Round Lenses: Spherical Aberration

While the paraxial ray equation describes the first-order focusing properties of a lens, real lenses suffer from geometric and chromatic **aberrations**. These are deviations from ideal focusing that ultimately limit the resolution of the microscope. The most significant geometric aberration for on-axis imaging is **[spherical aberration](@entry_id:174580)**. It arises because rays traveling at larger angles to the optical axis are focused more strongly than paraxial rays. This causes a point object to be imaged as a blurred disk. The effect is quantified by the [spherical aberration](@entry_id:174580) coefficient, $C_s$.

A landmark result in electron optics is **Scherzer's theorem**, which states that for any lens that is **static**, **rotationally symmetric**, **free of charge or current sources in the beam path**, and **focusing** (positive refractive), the [spherical aberration](@entry_id:174580) coefficient $C_s$ is necessarily positive [@problem_id:2867958]. The [mathematical proof](@entry_id:137161) involves calculating the third-order terms in the electron's trajectory. The final expression for $C_s$ takes the form of an integral along the optic axis of a sum of squared terms involving the electric or magnetic fields and their derivatives. Because all terms in the integrand are non-negative, the integral itself must be positive. This theorem represented a formidable barrier, suggesting that the resolution of conventional electron microscopes was fundamentally limited.

#### Evading Scherzer's Theorem: Aberration Correction

To overcome the limit imposed by Scherzer's theorem, one or more of its core assumptions must be violated. This is the principle behind modern **aberration correctors**, which have revolutionized [electron microscopy](@entry_id:146863) by enabling routine atomic-resolution imaging.

The most common strategy is to violate the assumption of **[rotational symmetry](@entry_id:137077)**. This is achieved by introducing non-round multipole elements, such as quadrupoles, hexapoles, or octupoles, into the electron column. A typical corrector uses a system of two hexapoles separated by transfer lenses [@problem_id:2867958]. While a single hexapole introduces a strong third-order aberration (three-fold [astigmatism](@entry_id:174378)), a carefully designed pair can be used to produce a net *negative* [spherical aberration](@entry_id:174580), which cancels the inherent positive $C_s$ of the round objective lens. This allows the total [spherical aberration](@entry_id:174580) of the system to be tuned to zero or even slightly negative.

An alternative, though less common, approach is to violate the assumption of **static fields**. By incorporating time-dependent radio-frequency (RF) fields, one can create an optical element whose focusing properties depend on the arrival time of the electron. With proper phasing, such an element can impart a negative spherical aberration to the beam, providing another path to correction [@problem_id:2867958].

### Electron-Specimen Interactions: The Source of Contrast

When the high-energy electron beam passes through a thin specimen, a multitude of interactions occur. These interactions modify the direction, phase, and energy of the electrons. By collecting and analyzing these scattered electrons, we can form images and spectra that reveal the structure, composition, and electronic properties of the material. The interactions can be broadly classified as elastic or inelastic.

#### Elastic Scattering

In an [elastic scattering](@entry_id:152152) event, the electron's kinetic energy is conserved (or the [energy transfer](@entry_id:174809) is negligibly small), but its direction of travel changes.

##### Coherent Scattering: The Basis of Diffraction

For a crystalline specimen, the periodic arrangement of atoms acts as a [diffraction grating](@entry_id:178037) for the electron wave. Incident electrons are coherently scattered by the lattice planes, leading to [constructive interference](@entry_id:276464) in specific directions defined by **Bragg's law**: $2d \sin\theta_B = n\lambda$, where $d$ is the spacing of the lattice planes, $\theta_B$ is the Bragg angle, $n$ is an integer, and $\lambda$ is the electron's de Broglie wavelength.

The geometry of diffraction is elegantly visualized in **[reciprocal space](@entry_id:139921)** using the **Ewald sphere construction**. In this construction, the incident electron beam is represented by a wavevector $\mathbf{k}$ of length $k = 1/\lambda$ (in the crystallographic convention). The Ewald sphere is a sphere of radius $k$ centered such that its surface passes through the origin of the reciprocal lattice. A diffracted beam is formed for every [reciprocal lattice](@entry_id:136718) point $\mathbf{g}$ that lies exactly on the surface of the sphere, satisfying the condition $\mathbf{k'} = \mathbf{k} + \mathbf{g}$, where $|\mathbf{k'}| = |\mathbf{k}|$.

In [electron microscopy](@entry_id:146863), the accelerating voltages are high (e.g., 100-300 keV), resulting in very short wavelengths. For a 200 keV electron, the relativistic de Broglie wavelength is $\lambda \approx 2.51$ pm [@problem_id:2867971]. This corresponds to a very large Ewald sphere radius of $k = 1/\lambda \approx 39.9 \, \text{\AA}^{-1}$. Because the sphere is so large compared to the spacing of reciprocal lattice points (typically $ \sim 1 \, \text{\AA}^{-1}$), it is nearly flat over a significant area. Furthermore, the finite thickness $t$ of the specimen causes the reciprocal lattice "points" to be elongated into rods of length $\sim 1/t$ along the beam direction. The "flat" Ewald sphere can therefore intersect many of these [reciprocal lattice](@entry_id:136718) rods simultaneously, especially when the beam is aligned along a major crystal axis (a zone axis). For instance, for a reflection with a spacing of $d=2.0 \, \text{\AA}$ ($g=0.5 \, \text{\AA}^{-1}$), the deviation of the reciprocal lattice point from the perfectly flat condition is $s \approx g^2/(2k) \approx 3.1 \times 10^{-3} \, \text{\AA}^{-1}$. For a specimen thickness of $t=30$ nm, the length of the reciprocal lattice rod is on the order of $1/t \approx 3.3 \times 10^{-3} \, \text{\AA}^{-1}$. Since the deviation $s$ is comparable to the rod length, the diffraction condition is strongly satisfied [@problem_id:2867971]. This simultaneous excitation of many reflections is known as a **multi-beam condition** and is the foundation of high-resolution TEM imaging.

##### Diffraction Contrast in TEM

The principles of diffraction give rise to a powerful imaging mode known as **[diffraction contrast](@entry_id:158591)**. By placing an objective [aperture](@entry_id:172936) in the [back focal plane](@entry_id:164391) of the [objective lens](@entry_id:167334), we can select either the unscattered, transmitted beam (to form a **Bright-Field (BF) image**) or one of the diffracted beams (to form a **Dark-Field (DF) image**). The intensity at any point in the image then depends on how strongly the corresponding point in the specimen is diffracting electrons into or out of the aperture.

Any local deviation from a perfect crystal lattice—such as a dislocation, a grain boundary, or local strain—will alter the diffraction conditions and produce contrast. A classic example is the formation of **bend contours** in a bent crystalline foil [@problem_id:2868017]. As the foil is bent, the orientation of the crystal lattice planes with respect to the incident beam changes continuously across the specimen. This creates dark bands in the BF image at locations where the lattice is oriented to satisfy a Bragg condition, strongly scattering electrons out of the objective aperture. The position of the central, darkest fringe corresponds to the exact Bragg condition ($s_g=0$). In a DF image formed with that diffracted beam, the contrast is complementary: the bend contour appears as a bright band against a dark background, because intensity removed from the BF image appears in the DF image.

##### High-Angle Elastic Scattering

As the [scattering angle](@entry_id:171822) increases, the probability of coherent Bragg diffraction decreases, and [elastic scattering](@entry_id:152152) becomes dominated by close, unscreened encounters between the incident electron and the atomic nuclei. This high-angle scattering process is well-approximated by the **Rutherford scattering** model, where the scattering cross-section is proportional to the square of the atomic number ($Z^2$). Because thermal vibrations of the atoms on the lattice are random, this high-angle scattering is largely an **incoherent** process—the total scattered intensity is simply the sum of the intensities scattered by individual atoms, with no persistent phase relationships. This strong dependence on atomic number is the basis for Z-contrast imaging, as we will see later.

#### Inelastic Scattering

In an inelastic scattering event, the incident electron transfers some of its energy to the specimen, leading to various [electronic excitations](@entry_id:190531).

##### Valence Electron Excitations and Secondary Electrons

A common inelastic process involves the transfer of a small amount of energy (typically 5-50 eV) to the specimen's valence or conduction electrons. This can excite an electron to a higher energy state or excite [collective oscillations](@entry_id:158973) of the [electron gas](@entry_id:140692), known as **plasmons**. Another outcome of this energy transfer is the ejection of a loosely bound valence electron from the atom. If this ejected electron has enough energy to overcome the surface work function and escape the specimen, it is termed a **secondary electron (SE)**.

Because [secondary electrons](@entry_id:161135) have very low energies (typically $ 50$ eV), their [mean free path](@entry_id:139563) within the solid is very short (a few nanometers). Consequently, only SEs generated very close to the surface can escape to be detected. The **secondary electron yield**, $\delta$, is defined as the average number of SEs emitted per incident primary electron [@problem_id:2867944]. The dependence of $\delta$ on the primary beam energy $E_0$ is non-monotonic. At very low $E_0$, there is insufficient energy to generate many SEs. As $E_0$ increases, more energy is deposited near the surface, and $\delta$ rises. However, as $E_0$ increases further (into the typical SEM range of 5-30 keV), the primary electrons penetrate deeper into the specimen. Most of the energy is deposited at depths far greater than the SE escape depth. As a result, fewer of the generated SEs can escape, and the yield $\delta$ decreases.

##### Core-Shell Excitations and Electron Energy-Loss Spectroscopy (EELS)

If the incident electron transfers sufficient energy to an atom, it can eject a tightly bound inner-shell (core) electron. This process is characteristic of the specific element and the particular electron shell involved. By using a magnetic [spectrometer](@entry_id:193181) to measure the energy distribution of the transmitted electrons, we create an **Electron Energy-Loss Spectrum (EELS)**.

A typical EELS spectrum consists of several key features [@problem_id:2867934]:
-   The **Zero-Loss Peak (ZLP)**: This is the most intense feature, comprising electrons that have not undergone any [inelastic scattering](@entry_id:138624) (unscattered and elastically scattered electrons). Its width determines the [energy resolution](@entry_id:180330) of the experiment and is primarily governed by the energy spread of the electron source. The relative intensity of the ZLP decreases exponentially with increasing specimen thickness.
-   The **Low-Loss Region** (up to ~50 eV): This region is dominated by [plasmon](@entry_id:138021) peaks and valence electron excitations, providing information about the specimen's dielectric properties.
-   **Core-Loss Edges**: At higher energy losses, sharp onsets or "edges" appear, corresponding to the binding energy of a specific core shell of an element in the sample (e.g., the Carbon K-edge at ~284 eV, the Iron L-edge at ~708 eV). The presence of these edges provides unambiguous elemental identification.

An electron may undergo multiple [inelastic scattering](@entry_id:138624) events, a phenomenon known as **plural scattering**. This results in a measured spectrum that is a convolution of the single-scattering distribution with itself. For quantitative analysis, especially of core-loss edges, this plural scattering must be mathematically removed through a [deconvolution](@entry_id:141233) process.

The shape of the core-loss edge contains a wealth of information. The **Electron Energy-Loss Near-Edge Structure (ELNES)** is sensitive to the unoccupied [electronic density of states](@entry_id:182354), providing information on the local bonding, coordination, and valence state of the element. The **Extended Energy-Loss Fine Structure (EXELFS)**, oscillations further past the edge, arises from interference effects involving the ejected core electron and its neighboring atoms, providing information on bond lengths and coordination numbers.

#### Specimen Damage

Electron-specimen interactions are not always benign; they can irreversibly alter or destroy the specimen, a phenomenon known as **beam damage**. Understanding the mechanisms of beam damage is crucial for studying sensitive materials like polymers, biological samples, and some 2D materials. There are two primary mechanisms [@problem_id:2867982]:

1.  **Radiolysis**: This is a chemically-mediated process driven by [inelastic scattering](@entry_id:138624). The incident electron causes [ionization](@entry_id:136315) or [electronic excitation](@entry_id:183394). The relaxation of these excited states can break chemical bonds, leading to atomic rearrangement, mass loss, or structural changes. Radiolysis does not have a sharp energy threshold and can occur at any beam energy, although its cross-section varies with energy.

2.  **Knock-on Displacement**: This is a ballistic process where an incident electron transfers sufficient momentum and energy in an [elastic collision](@entry_id:170575) to a nucleus to physically eject it from its lattice site. This process has a sharp energy threshold. The maximum kinetic energy $T_{\max}$ that an electron of kinetic energy $E$ can transfer to a nucleus of mass $M$ in a head-on collision is given by [relativistic kinematics](@entry_id:159064):
    $$
    T_{\max}(E) = \frac{2Mc^{2}E(E+2m_{e}c^{2})}{(m_{e}c^{2}+Mc^{2})^{2} + 2Mc^{2}E}
    $$
    where $m_e$ is the electron mass. An atom can only be displaced if $T_{\max}$ exceeds its displacement energy, $E_d$. The minimum beam energy required for this is the **knock-on [threshold energy](@entry_id:271447)**, $E_t$, defined by $T_{\max}(E_t) = E_d$. For example, for carbon in graphene with $E_d \approx 22$ eV, the threshold beam energy is calculated to be $E_t \approx 109$ keV [@problem_id:2867982]. Below this energy, [knock-on damage](@entry_id:193993) is impossible, and any observed damage must be due to [radiolysis](@entry_id:188087). Above this energy, [knock-on damage](@entry_id:193993) becomes an increasingly probable and often dominant damage mechanism.

### Image Formation Mechanisms in SEM and STEM

Scanning electron microscopes (SEM) and scanning transmission electron microscopes (STEM) both operate by rastering a focused electron probe across a specimen. An image is formed by measuring the intensity of a specific signal as a function of the probe position. The key difference lies in the signals detected and the specimen thickness.

#### Scanning Electron Microscopy (SEM) Contrast

SEM is typically used to study the surface of bulk samples. The two primary signals used for imaging are secondary and [backscattered electrons](@entry_id:161669).

##### Topographical Contrast with Secondary Electrons (SEs)

As discussed earlier, low-energy [secondary electrons](@entry_id:161135) can only escape from the top few nanometers of the surface. The SE yield is highly sensitive to the local surface topography. If the surface is tilted with respect to the beam, more SEs can escape from the side of a feature, leading to bright edges. This makes SE imaging an excellent mode for visualizing the three-dimensional morphology of a surface [@problem_id:2867944].

##### Compositional Contrast with Backscattered Electrons (BSEs)

Backscattered electrons (BSEs) are primary electrons that have undergone large-angle elastic scattering and re-emerged from the specimen surface. The **backscattered coefficient**, $\eta$, is the fraction of incident electrons that become BSEs. Because high-angle scattering is a Rutherford-like process, the probability of backscattering increases strongly with the [atomic number](@entry_id:139400) $Z$ of the target material. Therefore, regions with a higher average atomic number will scatter more electrons backward and appear brighter in a BSE image. This provides strong **[compositional contrast](@entry_id:159156)**, allowing for the visualization of different phases or elements in a sample [@problem_id:2867944].

#### Scanning Transmission Electron Microscopy (STEM) Contrast

In STEM, a thin specimen is used, and detectors are placed *below* the specimen to collect the transmitted electrons. By using annular detectors that collect electrons scattered into different angular ranges, a variety of contrast mechanisms can be realized simultaneously.

##### From Bright-Field to Dark-Field

Several detectors can be used to form images [@problem_id:2867942]:
-   A **Bright-Field (BF)** detector on the optical axis collects the unscattered beam and electrons scattered to very small angles.
-   An **Annular Bright-Field (ABF)** detector collects electrons scattered to angles just outside the direct beam, a regime useful for imaging light elements.
-   An **Annular Dark-Field (ADF)** detector collects electrons scattered to intermediate angles. The contrast is a complex mix of coherent Bragg scattering and [incoherent scattering](@entry_id:190180).

##### Incoherent Imaging: HAADF and Z-Contrast

The most powerful and widely used STEM imaging mode is **High-Angle Annular Dark-Field (HAADF)** imaging. The HAADF detector has a large inner angle, designed specifically to collect electrons scattered to high angles (e.g.,  50 mrad) while excluding the intense transmitted and Bragg-diffracted beams. This isolates the incoherent, high-angle [elastic scattering](@entry_id:152152) signal.

Because the scattering is incoherent, the image can be interpreted as a direct map of the scattering power of the specimen, convolution-free from the complex interference effects of [phase contrast](@entry_id:157707). The total intensity collected by the HAADF detector from an atomic column is, to a good approximation, the sum of the intensities scattered by each atom in that column. This makes the interpretation of HAADF images remarkably straightforward.

We can formalize the strong dependence of the HAADF signal on [atomic number](@entry_id:139400) $Z$. Modeling the elastic scattering using a screened Coulomb potential (e.g., a Yukawa potential) and the first Born approximation, we can integrate the [differential cross-section](@entry_id:137333) over the detector angles $\theta_{\mathrm{in}}$ to $\theta_{\mathrm{out}}$ [@problem_id:2867963]. The resulting intensity $I$ is found to be proportional to the specimen thickness $t$ and approximately proportional to $Z^n$, where $n$ is the **Z-contrast exponent**. The value of $n$ depends on the [screening effect](@entry_id:143615) of the atomic electrons and the detector collection angles. In the limit of very high angles where screening is negligible, scattering is purely Rutherford-like and $n=2$. For realistic detector angles, screening reduces the exponent. A full derivation shows that $n$ can be expressed as [@problem_id:2867942]:
$$
n(Z) = 2 - \frac{2}{3} A(Z) \left( \frac{1}{k^2\theta_{\mathrm{in}}^2 + A(Z)} + \frac{1}{k^2\theta_{\mathrm{out}}^2 + A(Z)} \right)
$$
where $A(Z) \propto Z^{2/3}$ is a term related to the [screening length](@entry_id:143797), and $k$ is the electron wave number. For typical conditions (e.g., 200 keV, $Z=26$, $\theta_{\mathrm{in}}=60$ mrad), this yields $n \approx 1.89$ [@problem_id:2867942]. The strong, monotonic dependence of HAADF intensity on $Z$ (often approximated as $I \propto Z^{1.7}$) makes it an exceptional technique for atomic-resolution [compositional mapping](@entry_id:198273), often called **Z-contrast imaging**.

#### Coherent Imaging: High-Resolution TEM (HRTEM)

In contrast to the [incoherent imaging](@entry_id:178214) of STEM-HAADF, conventional high-resolution TEM (HRTEM) is a **[coherent imaging](@entry_id:171640)** technique. It is a broad-beam method (not scanned) where an image is formed by the interference of the transmitted beam with multiple Bragg-diffracted beams that are allowed to pass through a large objective [aperture](@entry_id:172936). The resulting image is essentially an interference pattern, or hologram, whose contrast is highly sensitive to the phases of the electron waves. This is known as **[phase contrast](@entry_id:157707)**.

The formation of [phase contrast](@entry_id:157707) images is described by the **Contrast Transfer Function (CTF)**, which modulates the amplitudes and phases of different spatial frequencies (details of the specimen structure) in the image. An ideal microscope would transfer all spatial frequencies with equal fidelity, but real instruments are limited by aberrations and instabilities.

One critical limitation is the **[temporal coherence](@entry_id:177101)** of the electron beam, which is finite due to the energy spread of the source and instabilities in the accelerating voltage. Chromatic aberration ($C_c$) of the [objective lens](@entry_id:167334) converts this energy spread $\delta E$ into a focal spread $\delta f = C_c \delta E / E_0$. This "blurring" of the focus washes out contrast at high spatial frequencies. This effect is described by a [temporal coherence](@entry_id:177101) [envelope function](@entry_id:749028), $E_t(u)$, which multiplies the ideal CTF. For a Gaussian energy spread with standard deviation $\sigma_E$, this envelope is also Gaussian [@problem_id:2867938]:
$$
E_t(u) = \exp\left( -\frac{1}{2} \pi^2 \lambda^2 u^4 \sigma_f^2 \right)
$$
where $\sigma_f = C_c \sigma_E / E_0$. This [envelope function](@entry_id:749028) defines the ultimate **information limit** of the microscope, $u_i$, which is the highest [spatial frequency](@entry_id:270500) that can be meaningfully transferred. This limit is typically defined as the frequency where the envelope falls to $1/e$. From the equation above, we can derive:
$$
u_i = \left(\frac{\sqrt{2} E_0}{\pi \lambda C_c \sigma_E}\right)^{1/2}
$$
For a typical 200 kV microscope with $C_c=2.2$ mm and an energy spread of $\Delta E=0.7$ eV, the information limit is about $u_i \approx 7.41 \, \text{nm}^{-1}$, corresponding to a real-space distance of about $1.35$ Å [@problem_id:2867938]. This demonstrates how the fundamental optical properties of the lens and the characteristics of the electron source combine to set a hard limit on the achievable resolution in HRTEM.