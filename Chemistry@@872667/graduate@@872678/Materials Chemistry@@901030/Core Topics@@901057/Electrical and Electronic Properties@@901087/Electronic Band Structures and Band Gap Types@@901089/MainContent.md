## Introduction
The electronic properties of materials, from insulators to semiconductors and metals, are fundamentally dictated by their electronic band structure. Understanding how electron energies are organized within a crystalline solid is the cornerstone of modern materials science and condensed matter physics, enabling the design and engineering of all electronic and optoelectronic devices. However, bridging the gap from abstract quantum mechanical principles to the tangible properties of real-world materials and advanced systems can be challenging. This article aims to provide a comprehensive and cohesive journey through the world of [electronic bands](@entry_id:175335), addressing the 'why' and 'how' behind material behavior.

The reader will embark on a structured exploration beginning with the core theory. In **Principles and Mechanisms**, we will delve into the quantum mechanical origins of energy bands using Bloch's theorem, explore the models that describe their formation, and define the critical features like direct and indirect [band gaps](@entry_id:191975) that govern material properties. Building on this foundation, **Applications and Interdisciplinary Connections** will demonstrate how these principles are applied to engineer materials for [optoelectronics](@entry_id:144180), create transparent conductors, and understand the crucial role of defects and disorder. Finally, **Hands-On Practices** will offer a chance to engage with these concepts through guided computational exercises, translating theoretical knowledge into practical skills for analyzing and predicting material properties. This progression from first principles to practical application provides a robust framework for mastering the theory of electronic band structures.

## Principles and Mechanisms

The electronic properties of [crystalline solids](@entry_id:140223), which underpin modern electronics and [optoelectronics](@entry_id:144180), are governed by the behavior of electrons moving in a [periodic potential](@entry_id:140652) established by the atomic nuclei and core electrons. Unlike in isolated atoms with discrete energy levels, in a crystal, the electronic states group into continuous energy ranges known as **[energy bands](@entry_id:146576)**, separated by forbidden regions called **[band gaps](@entry_id:191975)**. This chapter elucidates the fundamental principles governing the formation of these bands, the mechanisms that dictate their structure, and the consequences for material properties.

### The Quantum Mechanical Origin of Electronic Bands

The defining characteristic of a crystalline solid is its translational symmetry. The crystal potential, $V(\mathbf{r})$, is periodic with respect to the set of Bravais [lattice vectors](@entry_id:161583) $\{\mathbf{R}\}$, such that $V(\mathbf{r} + \mathbf{R}) = V(\mathbf{r})$. This periodicity imposes a powerful constraint on the form of the electronic wavefunctions.

#### Bloch's Theorem and Crystal Momentum

The consequences of [translational symmetry](@entry_id:171614) are encapsulated in **Bloch's Theorem**. It states that the energy [eigenfunctions](@entry_id:154705) for an electron in a periodic potential can be chosen to have the form of a plane wave modulated by a function that has the same [periodicity](@entry_id:152486) as the crystal lattice. Mathematically, these **Bloch functions** are expressed as:

$$
\psi_{n\mathbf{k}}(\mathbf{r}) = e^{i\mathbf{k}\cdot\mathbf{r}} u_{n\mathbf{k}}(\mathbf{r})
$$

where $u_{n\mathbf{k}}(\mathbf{r})$ is the periodic part, satisfying $u_{n\mathbf{k}}(\mathbf{r} + \mathbf{R}) = u_{n\mathbf{k}}(\mathbf{r})$. The vector $\mathbf{k}$ is the **crystal momentum**, a [quantum number](@entry_id:148529) that arises directly from translational symmetry, analogous to how linear momentum arises from [translational symmetry](@entry_id:171614) in free space. The index $n$ is the **band index**, which labels the different energy bands.

An equivalent statement of Bloch's theorem is that an eigenstate, when translated by a lattice vector $\mathbf{R}$, acquires a phase factor determined by its [crystal momentum](@entry_id:136369) $\mathbf{k}$:

$$
\psi_{n\mathbf{k}}(\mathbf{r} + \mathbf{R}) = e^{i\mathbf{k}\cdot\mathbf{R}} \psi_{n\mathbf{k}}(\mathbf{r})
$$

In a perfect, infinite, and static crystal, the Hamiltonian commutes with all translation operators. As a result, the [crystal momentum](@entry_id:136369) $\mathbf{k}$ is a conserved quantity for an electron evolving under the influence of the crystal potential alone [@problem_id:2484948]. However, interactions that break this perfect [translational symmetry](@entry_id:171614), such as scattering with lattice vibrations (phonons) or impurities, can cause the electron's [crystal momentum](@entry_id:136369) to change. For example, in [electron-phonon scattering](@entry_id:138098), the total [crystal momentum](@entry_id:136369) of the electron-phonon system is conserved, but momentum is exchanged between the electron and the lattice [@problem_id:2484948].

#### Reciprocal Space and the Brillouin Zone

The crystal momentum $\mathbf{k}$ is not a conventional momentum; it is defined within a special vector space known as **[reciprocal space](@entry_id:139921)**. For a [direct lattice](@entry_id:748468) defined by a set of [primitive vectors](@entry_id:142930) $\{\mathbf{a}_1, \mathbf{a}_2, \mathbf{a}_3\}$, the corresponding reciprocal lattice is spanned by [primitive vectors](@entry_id:142930) $\{\mathbf{b}_1, \mathbf{b}_2, \mathbf{b}_3\}$ defined by the relationship:

$$
\mathbf{a}_i \cdot \mathbf{b}_j = 2\pi\delta_{ij}
$$

where $\delta_{ij}$ is the Kronecker delta. This condition ensures that for any [reciprocal lattice vector](@entry_id:276906) $\mathbf{G} = n_1\mathbf{b}_1 + n_2\mathbf{b}_2 + n_3\mathbf{b}_3$ (with integers $n_i$) and any [direct lattice](@entry_id:748468) vector $\mathbf{R} = m_1\mathbf{a}_1 + m_2\mathbf{a}_2 + m_3\mathbf{a}_3$ (with integers $m_i$), the dot product $\mathbf{G} \cdot \mathbf{R}$ is an integer multiple of $2\pi$. Consequently, $e^{i\mathbf{G}\cdot\mathbf{R}} = 1$.

This property reveals a redundancy in the [crystal momentum](@entry_id:136369) label. A Bloch state with [crystal momentum](@entry_id:136369) $\mathbf{k}+\mathbf{G}$ has the same translational property as one with $\mathbf{k}$, since $e^{i(\mathbf{k}+\mathbf{G})\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}} e^{i\mathbf{G}\cdot\mathbf{R}} = e^{i\mathbf{k}\cdot\mathbf{R}}$. Therefore, all physically distinct electronic states can be described by restricting $\mathbf{k}$ to a single primitive cell of the [reciprocal lattice](@entry_id:136718). By convention, this cell is chosen as the **first Brillouin zone (BZ)**.

The first Brillouin zone is formally constructed as the **Wigner-Seitz cell** of the reciprocal lattice centered at the origin ($\mathbf{k}=\mathbf{0}$). It is the set of all points in [reciprocal space](@entry_id:139921) that are closer to the origin than to any other reciprocal lattice point $\mathbf{G}$. Geometrically, it is the volume enclosed by the planes that are the [perpendicular bisectors](@entry_id:163148) of the vectors connecting the origin to all other [reciprocal lattice](@entry_id:136718) points. The physical significance of the BZ boundary is profound: it is the locus of points in $\mathbf{k}$-space where an electron wave is subject to Bragg reflection from the lattice planes [@problem_id:2484944].

#### Models of Band Formation

The emergence of [energy bands](@entry_id:146576) can be understood from two complementary perspectives.

The **nearly-free electron (NFE) model** starts with free electrons, whose wavefunctions are simple [plane waves](@entry_id:189798) $\psi_{\mathbf{k}}(\mathbf{r}) \propto e^{i\mathbf{k}\cdot\mathbf{r}}$ and whose energy dispersion is a simple parabola, $E(\mathbf{k}) = \frac{\hbar^2 |\mathbf{k}|^2}{2m_0}$. When a weak periodic potential $V(\mathbf{r})$ is introduced, it acts as a perturbation. This perturbation has little effect on the electron energies, except for wavevectors $\mathbf{k}$ near the Brillouin zone boundaries. At these boundaries, the Bragg condition $2\mathbf{k}\cdot\mathbf{G} + |\mathbf{G}|^2 = 0$ is satisfied, leading to strong scattering. The potential mixes states $\mathbf{k}$ and $\mathbf{k}-\mathbf{G}$, lifting the degeneracy and opening an energy gap. In this view, band gaps are a direct consequence of [electron diffraction](@entry_id:141284) by the periodic lattice [@problem_id:2484948].

The **[tight-binding](@entry_id:142573) (TB) model** provides an alternative, chemically intuitive picture. It starts from the opposite limit: electrons tightly bound to individual atoms with discrete atomic [orbital energies](@entry_id:182840). As atoms are brought together to form a crystal, their wavefunctions overlap. This overlap allows electrons to "hop" from one atom to a neighbor. According to quantum mechanics, this hopping lifts the degeneracy of the [atomic energy levels](@entry_id:148255), broadening them into continuous bands.

For a simple one-dimensional chain of identical atoms with lattice constant $a$, a single orbital per site with on-site energy $\epsilon_0$, and a nearest-neighbor [hopping integral](@entry_id:147296) $-t$ (where $t>0$), the resulting energy dispersion is given by:

$$
E(k) = \epsilon_0 - 2t \cos(ka)
$$

The width of this energy band, known as the **bandwidth** $W$, is the difference between the maximum and minimum energies. For this simple cosine band, $W = E_{\max} - E_{\min} = (\epsilon_0 + 2t) - (\epsilon_0 - 2t) = 4t$. The bandwidth is directly proportional to the [hopping integral](@entry_id:147296) $t$, which itself is a measure of the orbital overlap between neighboring atoms. Stronger interaction leads to wider bands [@problem_id:2484949].

### Characterizing Band Structures

The detailed shape of the energy bands, $E_n(\mathbf{k})$, is the electronic fingerprint of a material. Key features of the [band structure](@entry_id:139379), particularly near the fundamental band gap, dictate its electronic and optical properties.

#### Direct and Indirect Band Gaps

For a semiconductor or insulator, the highest occupied energy band at absolute zero temperature is the **[valence band](@entry_id:158227)**, and the lowest unoccupied band is the **conduction band**. The energy difference between them is the fundamental band gap. The [electronic states](@entry_id:171776) are filled up to the top of the [valence band](@entry_id:158227), the **valence band maximum (VBM)**, and the conduction band is empty. The bottom of the conduction band is the **conduction band minimum (CBM)**.

The character of the band gap depends critically on the relative positions of the VBM and CBM in $\mathbf{k}$-space [@problem_id:2484959]:

*   A material has a **[direct band gap](@entry_id:147887)** if the VBM and CBM occur at the same crystal momentum $\mathbf{k}$.
*   A material has an **[indirect band gap](@entry_id:143735)** if the VBM and CBM occur at different crystal momenta.

This distinction is of paramount importance for optoelectronic applications. As we will see, materials with direct [band gaps](@entry_id:191975) are generally efficient light emitters and absorbers, whereas those with indirect band gaps are not.

To illustrate this, consider the canonical examples of silicon (Si) and gallium arsenide (GaAs) [@problem_id:2484913]. Both are tetrahedrally coordinated semiconductors.
*   **Silicon (Si)** has the diamond crystal structure. Its VBM is at the center of the Brillouin zone, the $\Gamma$ point ($\mathbf{k}=\mathbf{0}$). However, its CBM is located along the line connecting $\Gamma$ to the $X$ point (a face center of the BZ), specifically at $\mathbf{k} \approx 0.85 \times (2\pi/a)(1,0,0)$. Because the VBM and CBM are at different $\mathbf{k}$-points, **Si has an [indirect band gap](@entry_id:143735)** of approximately $1.12$ eV.
*   **Gallium Arsenide (GaAs)** has the [zinc blende structure](@entry_id:149991). Its VBM is also at the $\Gamma$ point. Crucially, its CBM is also located at the $\Gamma$ point. Because the VBM and CBM coincide in $\mathbf{k}$-space, **GaAs has a [direct band gap](@entry_id:147887)** of approximately $1.42$ eV.

The origin of this difference lies in the interplay between [crystal symmetry](@entry_id:138731) and chemical composition. Si, with its [covalent bonding](@entry_id:141465) and [inversion symmetry](@entry_id:269948), exhibits strong repulsion between the $p$-like valence bands and the $s$-like conduction band at the $\Gamma$ point, pushing the $\Gamma$ conduction state to a very high energy. In contrast, GaAs lacks inversion symmetry due to the chemical difference between the Ga (cation) and As (anion) sites. This asymmetry reduces the repulsion, lowering the energy of the $s$-like conduction state at $\Gamma$ relative to other valleys, thereby making the gap direct [@problem_id:2484913].

#### Carrier Dynamics and the Effective Mass

The dispersion relation $E(\mathbf{k})$ not only defines the band structure but also governs how charge carriers ([electrons and holes](@entry_id:274534)) respond to external forces. In the semiclassical picture, the [group velocity](@entry_id:147686) of an electron in a Bloch state is given by:

$$
\mathbf{v}(\mathbf{k}) = \frac{1}{\hbar} \nabla_{\mathbf{k}} E(\mathbf{k})
$$

When an external electric or magnetic field is applied, the acceleration of the electron is not determined by its free-space mass $m_0$, but by the curvature of its energy band. This leads to the concept of **effective mass**. Near a band extremum (CBM or VBM), where the dispersion can be approximated by a parabolic function, the response of an electron to a force $\mathbf{F}$ is $\dot{\mathbf{v}} = \mathbf{m}^{*-1} \mathbf{F}$, where $\mathbf{m}^{*-1}$ is the **inverse [effective mass tensor](@entry_id:147018)**, defined as:

$$
[m^{*-1}]_{ij} = \frac{1}{\hbar^2} \frac{\partial^2 E(\mathbf{k})}{\partial k_i \partial k_j}
$$

*   At a **conduction band minimum**, the energy surface curves upwards ($E(\mathbf{k})$ is a minimum). The second derivatives are positive, resulting in a **positive effective mass**.
*   At a **[valence band](@entry_id:158227) maximum**, the energy surface curves downwards ($E(\mathbf{k})$ is a maximum). The second derivatives are negative, yielding a [negative effective mass](@entry_id:272042) for an electron. This counter-intuitive behavior is resolved by introducing the concept of a **hole**: a quasiparticle representing the absence of an electron. A hole has a positive charge ($+e$) and a **positive effective mass**, allowing it to be treated as a conventional particle [@problem_id:2484987].

In many crystals, the band curvature is not the same in all directions, making the effective mass **anisotropic**. For instance, in an ellipsoidal valley, the mass will be different along the principal axes. This anisotropy has profound consequences for transport properties, as the [carrier mobility](@entry_id:268762) and conductivity become tensorial quantities directly related to the inverse [effective mass tensor](@entry_id:147018). It also affects phenomena like [cyclotron resonance](@entry_id:139685), where the measured [resonance frequency](@entry_id:267512) for a magnetic field applied along a specific direction depends on a combination of the principal masses in the plane perpendicular to the field [@problem_id:2484987].

### Interaction with Light and Selection Rules

The interaction of photons with the electronic states of a crystal governs its optical properties, such as absorption and emission. This interaction is governed by strict conservation laws and quantum mechanical [selection rules](@entry_id:140784).

#### Optical Transitions: Energy and Momentum Conservation

For an electron to be excited from a [valence band](@entry_id:158227) state $|v, \mathbf{k}_i\rangle$ to a conduction band state $|c, \mathbf{k}_f\rangle$ by absorbing a photon, both energy and momentum must be conserved.

1.  **Energy Conservation**: The final energy must equal the initial energy plus the [photon energy](@entry_id:139314): $E_c(\mathbf{k}_f) = E_v(\mathbf{k}_i) + \hbar\omega$.
2.  **Crystal Momentum Conservation**: The final [crystal momentum](@entry_id:136369) must equal the initial crystal momentum plus the photon's momentum: $\mathbf{k}_f = \mathbf{k}_i + \mathbf{q}_{\text{photon}}$.

A crucial simplification arises from the vast difference in scale between the wavelength of visible light (hundreds of nanometers) and the crystal [lattice constant](@entry_id:158935) (sub-nanometer). This implies that the photon's momentum $\mathbf{q}_{\text{photon}}$ is negligible compared to the size of the Brillouin zone. Thus, the momentum conservation rule effectively becomes $\mathbf{k}_f \approx \mathbf{k}_i$. This is known as the **vertical transition** rule: in an $E$-vs-$\mathbf{k}$ diagram, allowed [optical transitions](@entry_id:160047) are represented by vertical lines [@problem_id:2484959].

This rule immediately explains the differing optical behaviors of direct and indirect gap materials.
*   In a **direct gap material**, the VBM and CBM are at the same $\mathbf{k}$. A photon with energy equal to the band gap can directly excite an electron from the VBM to the CBM, satisfying both energy and momentum conservation. This is an efficient, first-order process, leading to strong light absorption and emission.
*   In an **indirect gap material**, the VBM and CBM are at different $\mathbf{k}$-points. A vertical transition from the VBM cannot reach the CBM. To bridge the momentum gap $\Delta\mathbf{k} = \mathbf{k}_c - \mathbf{k}_v$, the electron must simultaneously interact with another particle that can provide the necessary momentum. This role is played by a **phonon**, a quantum of lattice vibration. The absorption of a photon becomes a second-order process involving both an electron-photon and an [electron-phonon interaction](@entry_id:140708). Such processes are far less probable, making indirect gap materials poor light emitters and absorbers near their fundamental gap [@problem_id:2484959].

The experimental absorption spectrum reflects this difference. Direct gap materials exhibit a sharp absorption onset, while indirect gap materials show a much weaker, gradual onset featuring "shoulders" or "knees" corresponding to the energies required for transitions involving the absorption or emission of different types of phonons [@problem_id:2484959].

#### Formalism of Optical Absorption

The strength of absorption is quantified by the absorption coefficient, $\alpha(\omega)$. Using Fermi's golden rule, it can be shown that $\alpha(\omega)$ for direct transitions is given by:

$$
\alpha(\omega) = \frac{2\pi e^2}{n_r c \varepsilon_0 m_0^2 \omega} \frac{1}{V} \sum_{\mathbf{k}} \left| \langle c\mathbf{k} | \hat{\mathbf{p}}\cdot\mathbf{e} | v\mathbf{k} \rangle \right|^2 [f_v(\mathbf{k}) - f_c(\mathbf{k})] \delta(E_c(\mathbf{k}) - E_v(\mathbf{k}) - \hbar\omega)
$$

where $n_r$ is the refractive index, $\mathbf{e}$ is the light [polarization vector](@entry_id:269389), $\hat{\mathbf{p}}$ is the momentum operator, and the sum is over all $\mathbf{k}$-states in the first Brillouin zone. The expression highlights two critical factors:

1.  The **momentum [matrix element](@entry_id:136260)**, $\langle c\mathbf{k} | \hat{\mathbf{p}}\cdot\mathbf{e} | v\mathbf{k} \rangle$, which quantifies the quantum mechanical probability of a transition between the initial and final states. Its value is determined by the symmetry and orbital character of the wavefunctions.
2.  The **[joint density of states](@entry_id:143002) (JDOS)**, represented by the sum over the [delta function](@entry_id:273429), which counts the number of pairs of initial and final states separated by the photon energy $\hbar\omega$.

Transitions are governed by **selection rules**. In addition to the $\Delta\mathbf{k}=\mathbf{0}$ rule for direct transitions, the electric-[dipole interaction](@entry_id:193339) (proportional to $\hat{\mathbf{p}}$) imposes others. Since $\hat{\mathbf{p}}$ does not act on spin, spin is conserved ($\Delta s=0$). In crystals with [inversion symmetry](@entry_id:269948) (centrosymmetric), the wavefunctions have definite parity (even or odd). The momentum operator $\hat{\mathbf{p}}$ is odd under inversion. For the matrix element to be non-zero, the overall integrand must be even. This requires the initial and final states to have **opposite parity** (gerade $\leftrightarrow$ [ungerade](@entry_id:147965)) [@problem_id:2484954].

### Beyond Ideal Bulk Crystals

While the preceding principles describe the intrinsic properties of perfect, infinite crystals, real-world materials and devices involve interfaces, computational approximations, and [many-body interactions](@entry_id:751663) that modify this idealized picture.

#### Heterojunctions and Band Alignment

When two different semiconductors are joined to form a **[heterojunction](@entry_id:196407)**, their band structures must align relative to each other. A first-order estimate of this alignment is given by **Anderson's rule**. This rule assumes that when the materials are brought into contact, their vacuum levels align. The **electron affinity** $\chi$ (energy from CBM to vacuum) and **ionization potential** $I$ (energy from VBM to vacuum) are intrinsic bulk properties. Aligning the vacuum levels determines the band offsets: the conduction [band offset](@entry_id:142791) is $\Delta E_c = \chi_1 - \chi_2$ and the valence band offset is $\Delta E_v = (\chi_1 + E_{g1}) - (\chi_2 + E_{g2})$.

Depending on the relative positions of the band edges, heterojunctions are classified into three types [@problem_id:2484926]:
*   **Type I (straddling)**: The narrower band gap material is nested entirely within the wider band gap material. This confines both [electrons and holes](@entry_id:274534) in the same material.
*   **Type II (staggered)**: The band edges are staggered, such that the CBM and VBM are lowest in different materials. This spatially separates electrons and holes across the interface.
*   **Type III (broken gap)**: The alignment is so staggered that the conduction band of one material lies below the valence band of the other.

These alignments are fundamental to the design of [quantum wells](@entry_id:144116), laser diodes, and high-electron-mobility transistors. It is important to note that Anderson's rule is an idealization; in reality, interface dipoles and chemical bonding can cause significant deviations from this simple picture.

#### The DFT Band Gap Problem and Quasiparticle Energies

Modern materials science relies heavily on **Density Functional Theory (DFT)** for calculating band structures. However, standard approximations to DFT, such as the Local Density Approximation (LDA) and Generalized Gradient Approximation (GGA), are notorious for systematically underestimating the band gaps of semiconductors and insulators.

This is not a numerical error but a fundamental flaw in the approximations. The exact fundamental gap is $E_g = I - A$, which can be shown to equal the difference in the derivative of the total energy $E$ with respect to particle number $N$ as $N$ crosses an integer. For the exact DFT functional, this leads to the relation $E_g = E_g^{\text{KS}} + \Delta_{xc}$, where $E_g^{\text{KS}}$ is the gap between the highest occupied and lowest unoccupied Kohn-Sham eigenvalues, and $\Delta_{xc}$ is a positive correction known as the **derivative discontinuity** of the [exchange-correlation potential](@entry_id:180254). Standard approximations like LDA and GGA lack this discontinuity (i.e., they have $\Delta_{xc}=0$), which is the primary reason they underestimate the gap [@problem_id:2484980].

This highlights a crucial distinction: Kohn-Sham eigenvalues are mathematical energies of an auxiliary non-interacting system, designed to reproduce the ground-state density. They are not, in general, the true electron addition/removal energies. These true energies are called **[quasiparticle energies](@entry_id:173936)** and correspond to poles of the interacting one-electron Green's function. They are what photoemission (measures occupied states) and inverse photoemission (measures unoccupied states) experiments probe. More advanced computational methods, such as the **GW approximation**, are designed to calculate these [quasiparticle energies](@entry_id:173936) and provide much more accurate [band gaps](@entry_id:191975) [@problem_id:2484980].

#### Many-Body Effects: Excitons

Even an accurate quasiparticle band gap does not fully describe [optical absorption](@entry_id:136597). When a photon creates an electron-hole pair, these two particles attract each other via the Coulomb force. This interaction can fundamentally alter the optical spectrum. The bound electron-hole pair is a new quasiparticle called an **[exciton](@entry_id:145621)**.

The consequences of this interaction are twofold [@problem_id:2485014]:
1.  **Bound Excitons**: The attraction can lead to the formation of discrete [bound states](@entry_id:136502) with energies *below* the quasiparticle gap, $E_{\text{QP}}$. These appear as sharp absorption peaks in the optical spectrum. The lowest energy peak defines the **optical gap**, $E_{\text{opt}} = E_{\text{QP}} - E_b$, where $E_b$ is the [exciton binding energy](@entry_id:138355).
2.  **Continuum Enhancement**: Even for photon energies above the quasiparticle gap, the persistent Coulomb attraction enhances the probability of finding the electron and hole near each other. This **Sommerfeld enhancement** modifies the shape of the absorption continuum, often changing the absorption onset in a 3D material from a gradual $\sqrt{\hbar\omega - E_{\text{QP}}}$ dependence to a finite step.

These many-body effects are captured theoretically by solving the **Bethe-Salpeter Equation (BSE)**, an effective two-particle Schrödinger equation for the electron-hole pair. The BSE, typically solved using [quasiparticle energies](@entry_id:173936) and a screened Coulomb interaction from a GW calculation, provides a state-of-the-art description of the [optical properties of materials](@entry_id:141842), including the energies and oscillator strengths of all excitonic states [@problem_id:2485014].