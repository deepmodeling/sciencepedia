## Introduction
Magnetism, a fundamentally quantum mechanical phenomenon, underpins a vast array of physical properties and technological applications, from data storage to quantum computing. However, the microscopic arrangement of [atomic magnetic moments](@entry_id:173739)—the magnetic structure—is often hidden from conventional laboratory probes. While bulk measurements can detect a net magnetic moment, they are blind to complex arrangements like [antiferromagnetism](@entry_id:145031), where local moments cancel each other out. To truly understand and engineer magnetic materials, a technique is needed that can directly map the orientation and magnitude of spins at the atomic level.

This is the unique and indispensable role of [neutron scattering](@entry_id:142835). Because the neutron possesses an intrinsic magnetic dipole moment, it interacts directly with the local magnetic fields produced by electrons in a material. This allows it to serve as a premier probe for magnetic crystallography. This article provides a graduate-level guide to the theory and practice of [magnetic structure determination](@entry_id:144402) using neutron scattering. It addresses the key challenge of translating raw diffraction data into a quantitative model of a material's magnetic ground state.

The article is structured to build expertise progressively. Chapter 1, **"Principles and Mechanisms,"** lays the theoretical groundwork, detailing the neutron's magnetic interaction, the derivation of the [scattering cross-section](@entry_id:140322), and the powerful symmetry principles of [magnetic space groups](@entry_id:201553) and representation analysis. Chapter 2, **"Applications and Interdisciplinary Connections,"** demonstrates how these principles are put into practice to solve real-world problems, from characterizing phase transitions and complex spin textures to probing the interplay of magnetism with superconductivity. Finally, Chapter 3, **"Hands-On Practices,"** offers a set of focused problems designed to solidify understanding of key concepts like the [magnetic form factor](@entry_id:136670) and symmetry-based [selection rules](@entry_id:140784).

## Principles and Mechanisms

### The Fundamental Interaction: The Neutron's Magnetic Moment

The capacity of the neutron, an electrically neutral particle, to serve as a premier probe of magnetic structures in [condensed matter](@entry_id:747660) stems from its intrinsic [magnetic dipole moment](@entry_id:149826). This quantum mechanical property is inextricably linked to the neutron's spin. The magnetic moment is an operator, $\boldsymbol{\mu}_n$, that is directly proportional to the neutron's [spin operator](@entry_id:149715), $\mathbf{S}$:

$$
\boldsymbol{\mu}_n = \gamma_n \mathbf{S}
$$

Here, $\gamma_n$ is the **[gyromagnetic ratio](@entry_id:149290)** of the neutron, a fundamental constant. A crucial feature of the neutron is that its [gyromagnetic ratio](@entry_id:149290) is negative ($\gamma_n \approx -1.832 \times 10^8 \, \text{rad} \cdot \text{s}^{-1} \cdot \text{T}^{-1}$). This negative sign imparts a profound physical property: the neutron's magnetic moment vector, $\boldsymbol{\mu}_n$, is always oriented **antiparallel** to its spin vector, $\mathbf{S}$. [@problem_id:3007083]

For convenience in nuclear and particle physics, the [gyromagnetic ratio](@entry_id:149290) is often expressed in terms of the dimensionless neutron **[g-factor](@entry_id:153442)**, $g_n$, and the **nuclear magneton**, $\mu_{\mathrm{N}}$. The nuclear magneton is defined as $\mu_{\mathrm{N}} = \frac{e\hbar}{2m_p}$, where $e$ is the elementary charge, $\hbar$ is the reduced Planck constant, and $m_p$ is the proton mass. The relationship is given by:

$$
\boldsymbol{\mu}_n = g_n \frac{\mu_{\mathrm{N}}}{\hbar} \mathbf{S}
$$

Comparing this with the previous equation, we see that $\gamma_n = g_n \mu_{\mathrm{N}} / \hbar$. The experimentally determined value for the neutron g-factor is $g_n \approx -3.826$. For a spin-$\frac{1}{2}$ particle like the neutron, the magnitude of the magnetic moment is conventionally quoted as the maximum expectation value of its projection along an axis, which corresponds to $|g_n| \mu_{\mathrm{N}} / 2$. This gives a value of approximately $1.913 \, \mu_{\mathrm{N}}$.

The interaction of the neutron with a magnetic material is governed by the **Zeeman interaction** between the neutron's magnetic moment and the local magnetic induction, $\mathbf{B}(\mathbf{r})$, produced by the electrons in the material. The interaction potential is:

$$
V(\mathbf{r}) = -\boldsymbol{\mu}_n \cdot \mathbf{B}(\mathbf{r}) = -\gamma_n \mathbf{S} \cdot \mathbf{B}(\mathbf{r})
$$

This potential is the origin of magnetic neutron scattering. In a uniform magnetic field $\mathbf{B} = B\hat{\mathbf{z}}$, the [energy eigenvalues](@entry_id:144381) are $E = - \gamma_n B m_s \hbar$, where $m_s = \pm \frac{1}{2}$. Since $\gamma_n$ is negative, the lowest energy state ($E  0$) corresponds to $m_s = -\frac{1}{2}$, where the neutron's spin is anti-aligned with the field. This occurs because the antiparallel magnetic moment aligns with the field to minimize the energy. [@problem_id:3007083]

### The Scattering Cross-Section: From Potential to Intensity

Within the first Born approximation, the neutron [scattering cross-section](@entry_id:140322) is proportional to the squared magnitude of the [matrix element](@entry_id:136260) of the scattering potential between the initial and final states of the neutron-plus-sample system. This [matrix element](@entry_id:136260) is effectively the Fourier transform of the interaction potential. In a crystal, two primary interactions contribute to the [total scattering](@entry_id:159222): the nuclear strong force and the magnetic [dipole interaction](@entry_id:193339).

#### Nuclear versus Magnetic Scattering

The **nuclear interaction** is a short-range, strong-force interaction between the neutron and the atomic nuclei. It is effectively a point-like interaction on the length scale of thermal neutron wavelengths. This interaction is modeled by the **Fermi pseudopotential**, which is independent of the neutron's spin. Consequently, the nuclear [coherent scattering](@entry_id:267724) operator in the neutron's spin space is a scalar proportional to the [identity operator](@entry_id:204623), $\mathbb{1}$. The resulting [scattering amplitude](@entry_id:146099) is independent of the [momentum transfer](@entry_id:147714), $Q = |\mathbf{Q}|$, apart from [the structure factor](@entry_id:158623) which depends on the atomic arrangement. [@problem_id:3007130] [@problem_id:3007084]

In contrast, the **magnetic interaction**, as defined by $V(\mathbf{r}) = -\gamma_n \mathbf{S} \cdot \mathbf{B}(\mathbf{r})$, is explicitly dependent on the neutron's [spin operator](@entry_id:149715) $\mathbf{S}$. This fundamental difference has profound consequences, allowing the separation of nuclear and magnetic signals.

#### The Projection Rule

To derive the form of the magnetic [scattering amplitude](@entry_id:146099), we must consider the nature of the magnetic induction field $\mathbf{B}(\mathbf{r})$ generated by a magnetization density $\mathbf{M}(\mathbf{r})$. In [magnetostatics](@entry_id:140120), the Fourier components of these fields are related. The key relations $\nabla \cdot \mathbf{B} = 0$ and $\nabla \times \mathbf{H} = \mathbf{0}$ (for no [free currents](@entry_id:191634)) imply that in reciprocal space, $\mathbf{Q} \cdot \mathbf{B}(\mathbf{Q}) = 0$ and $\mathbf{Q} \times \mathbf{H}(\mathbf{Q}) = \mathbf{0}$. These conditions mean that $\mathbf{B}(\mathbf{Q})$ is perpendicular to $\mathbf{Q}$, while $\mathbf{H}(\mathbf{Q})$ is parallel to $\mathbf{Q}$. Using the [constitutive relation](@entry_id:268485) $\mathbf{B}(\mathbf{Q}) \propto \mathbf{H}(\mathbf{Q}) + \mathbf{M}(\mathbf{Q})$, it can be rigorously shown that the magnetic induction component that scatters neutrons is proportional to the component of the magnetization Fourier transform that is perpendicular to the [scattering vector](@entry_id:262662) $\mathbf{Q}$. [@problem_id:3007099] Let us denote this perpendicular component of the [magnetization vector](@entry_id:180304) as $\mathbf{M}_{\perp}(\mathbf{Q})$:

$$
\mathbf{M}_{\perp}(\mathbf{Q}) = \mathbf{M}(\mathbf{Q}) - \hat{\mathbf{Q}}(\hat{\mathbf{Q}} \cdot \mathbf{M}(\mathbf{Q}))
$$

where $\hat{\mathbf{Q}}$ is the unit vector in the direction of $\mathbf{Q}$. This can also be written compactly using a [vector triple product](@entry_id:162942) as $\hat{\mathbf{Q}} \times (\mathbf{M}(\mathbf{Q}) \times \hat{\mathbf{Q}})$.

The scattering amplitude operator for [magnetic scattering](@entry_id:147236), which we will denote $F_M(\mathbf{Q})$, is thus proportional to the dot product of the neutron [spin operator](@entry_id:149715) and this perpendicular magnetization component:

$$
F_M(\mathbf{Q}) \propto \boldsymbol{\sigma} \cdot \mathbf{M}_{\perp}(\mathbf{Q})
$$

where $\boldsymbol{\sigma}$ is the vector of Pauli matrices, which is proportional to the [spin operator](@entry_id:149715) $\mathbf{S}$. This result is the cornerstone of magnetic neutron scattering: **neutrons only scatter from the component of the sample magnetization perpendicular to the [scattering vector](@entry_id:262662)**. This is often called the **projection rule**. [@problem_id:3007130]

#### The Magnetic Structure Factor and Intensity

The total magnetization density in a crystal can be modeled as a superposition of contributions from individual magnetic ions. The Fourier transform of this density defines the **[magnetic structure](@entry_id:201216) factor**, $\mathbf{F}_M(\mathbf{Q})$, which is a vector quantity:

$$
\mathbf{F}_M(\mathbf{Q}) = \sum_j \mathbf{m}_j f_j(Q) \exp(i\mathbf{Q} \cdot \mathbf{r}_j) \exp(-W_j)
$$

Here, the sum is over the magnetic atoms $j$ in the unit cell at positions $\mathbf{r}_j$. $\mathbf{m}_j$ is the vector magnetic moment of the atom, $f_j(Q)$ is the **[magnetic form factor](@entry_id:136670)** accounting for the [spatial distribution](@entry_id:188271) of its magnetic electrons, and $\exp(-W_j)$ is the Debye-Waller factor accounting for thermal vibrations. [@problem_id:3007099]

For an unpolarized neutron beam, the measured intensity of a magnetic Bragg peak is proportional to the squared magnitude of the perpendicular component of this vector structure factor:

$$
I_M(\mathbf{Q}) \propto |\mathbf{F}_{M\perp}(\mathbf{Q})|^2 = |\mathbf{F}_M(\mathbf{Q})|^2 - |\hat{\mathbf{Q}} \cdot \mathbf{F}_M(\mathbf{Q})|^2
$$

This formulation of the intensity explicitly incorporates the projection rule. The [magnetic form factor](@entry_id:136670), $f(Q)$, is the Fourier transform of the normalized [spin density](@entry_id:267742) of a single atom. As it arises from a spatially extended object (the electron cloud), it decreases with increasing $Q$. Consequently, the magnetic [scattering intensity](@entry_id:202196), which is proportional to $[f(Q)]^2$, falls off rapidly with $Q$. This is in sharp contrast to the nuclear intensity, which is intrinsically $Q$-independent. This difference is a key experimental signature: magnetic Bragg peaks are typically most prominent at low scattering angles (low $Q$), while nuclear peaks persist to high angles. [@problem_id:3007084]

### Symmetry in Magnetic Structures

The arrangement of magnetic moments in a crystal is not arbitrary; it must be compatible with the underlying [crystal symmetry](@entry_id:138731). The mathematical framework for describing these symmetries is the theory of [magnetic groups](@entry_id:191510).

#### Magnetic Periodicity and the Propagation Vector

In many magnetic materials, the periodicity of the [magnetic structure](@entry_id:201216) does not coincide with the [periodicity](@entry_id:152486) of the chemical lattice. Such structures are called **modulated magnetic structures**. The [periodicity](@entry_id:152486) is described by a **[magnetic propagation vector](@entry_id:136919)**, $\mathbf{k}$, which is a vector in reciprocal space. This vector is formally defined by the transformation property of the magnetic moments $\mathbf{m}_{\mathbf{R}}$ on lattice sites separated by a nuclear lattice vector $\mathbf{R}$. For a simple single-$\mathbf{k}$ structure, this relation is:

$$
\mathbf{m}_{\mathbf{R}} = \mathbf{m}_{\mathbf{0}} \exp(i 2\pi \mathbf{k} \cdot \mathbf{R})
$$

where $\mathbf{m}_{\mathbf{0}}$ is the moment in the reference unit cell. [@problem_id:3007117]

This periodic [modulation](@entry_id:260640) in real space has a direct consequence in reciprocal space. Magnetic Bragg scattering will appear at positions $\mathbf{Q}$ given by:

$$
\mathbf{Q} = \boldsymbol{\tau} \pm \mathbf{k}
$$

where $\boldsymbol{\tau}$ is a [reciprocal lattice vector](@entry_id:276906) of the chemical lattice. These peaks are known as **magnetic satellites**. The case $\mathbf{k}=\mathbf{0}$ corresponds to a magnetic structure with the same translational periodicity as the chemical lattice (e.g., a simple ferromagnet or a simple antiferromagnet where the magnetic unit cell is the same size as the chemical one). A non-zero $\mathbf{k}$ signifies a different periodicity. If the components of $\mathbf{k}$ (in units of the [reciprocal lattice vectors](@entry_id:263351)) are rational numbers, e.g., $\mathbf{k} = (\frac{1}{3}, 0, \frac{1}{2})$, the structure is **commensurate**, forming a magnetic supercell. For the given example, the magnetic unit cell would be three times larger along the $\mathbf{a}$ direction and two times larger along the $\mathbf{c}$ direction. If any component is irrational, the structure is **incommensurate**. [@problem_id:3007117]

#### Magnetic Space Groups

To fully classify magnetic structures, we must consider not only spatial symmetries but also **[time-reversal symmetry](@entry_id:138094)**. The time-reversal operator, $\Theta$, is an **antiunitary operator** that leaves position invariant but reverses momentum and spin. Crucially for magnetism, it reverses a magnetic moment: $\Theta \mathbf{M} = -\mathbf{M}$. [@problem_id:3007053]

The full symmetry group of a magnetic crystal is a **magnetic [space group](@entry_id:140010)**, also known as a **Shubnikov group**. These groups consist of unitary spatial operations $g = (R|\mathbf{t})$ (where $R$ is a rotation and $\mathbf{t}$ is a translation) and/or antiunitary operations of the form $\Theta g$. An operation $x$ from the magnetic group leaves the magnetization density $\mathbf{M}(\mathbf{r})$ invariant, according to the rule:

$$
\mathbf{M}(\mathbf{r}) = \epsilon(x) R_x \mathbf{M}(R_x^{-1}(\mathbf{r}-\mathbf{t}_x))
$$

where $\epsilon(x)=+1$ for a unitary operation $x$ and $\epsilon(x)=-1$ for an antiunitary operation.

There are three types of [magnetic space groups](@entry_id:201553):
1.  **Type I (Unitary groups):** These are the 230 standard crystallographic [space groups](@entry_id:143034). They contain no time-reversal operator. They can describe ferromagnetic structures where the magnetic order does not break any spatial symmetries.
2.  **Type II (Gray groups):** These are formed by taking a standard [space group](@entry_id:140010) $G$ and adding the product of every element with $\Theta$. They are written as $G + \Theta G$. Since $\Theta$ itself is a member of the group, any static magnetic moment must be zero ($\langle \mathbf{M} \rangle = \Theta \langle \mathbf{M} \rangle = -\langle \mathbf{M} \rangle \implies \langle \mathbf{M} \rangle = 0$). These groups describe paramagnetic or [diamagnetic materials](@entry_id:264470), which exhibit no magnetic Bragg scattering.
3.  **Type III (Black-and-White groups):** These groups contain antiunitary elements, but not $\Theta$ itself. They are essential for describing antiferromagnetic and other complex magnetic arrangements. For instance, an anti-translation symmetry $\Theta \boldsymbol{\tau}$ implies that $\mathbf{M}(\mathbf{r}+\boldsymbol{\tau}) = -\mathbf{M}(\mathbf{r})$, which is the defining property of a simple [antiferromagnet](@entry_id:137114). [@problem_id:3007053]

#### Representation Analysis

Symmetry provides a powerful and systematic method for determining possible magnetic structures, known as **representation analysis**. The magnetic moments arranged on a crystallographic site must form a basis for an [irreducible representation](@entry_id:142733) (irrep) of the crystal's [space group](@entry_id:140010). By calculating which irreps are present in the magnetic representation and what their basis vectors are, one can enumerate all symmetry-allowed magnetic structures.

This process involves:
1.  Identifying the propagation vector $\mathbf{k}$ and its corresponding **little group** $G_\mathbf{k}$ (the subgroup of [space group](@entry_id:140010) operations that leave $\mathbf{k}$ invariant).
2.  For a magnetic atom at a specific Wyckoff site, determining its [site-symmetry group](@entry_id:146984).
3.  Decomposing the representation of an [axial vector](@entry_id:191829) (a magnetic moment) into the irreps of the [site-symmetry group](@entry_id:146984). This tells us the allowed orientations of a moment on a single site.
4.  Inducing this representation up to the full little group $G_\mathbf{k}$ to find the symmetry-adapted modes for the entire set of magnetic atoms in the crystal.

For example, consider a magnetic ion in the hexagonal space group $P6_3/mmc$ at the Wyckoff site $2a$ with positions $(0,0,0)$ and $(0,0,1/2)$, for a $\mathbf{k}=\mathbf{0}$ magnetic structure. The [site symmetry](@entry_id:183677) is $D_{3d}$. Representation analysis shows that a single moment can be oriented along the c-axis (transforming as the $A_{2g}$ irrep of $D_{3d}$) or within the ab-plane (transforming as the $E_g$ irrep). When considering the two atoms in the unit cell, these modes combine to form ferromagnetic (moments on both sites are parallel) and antiferromagnetic (moments are antiparallel) stacking arrangements along the c-axis. Each of these arrangements is a [basis vector](@entry_id:199546) of a specific irrep of the full [space group](@entry_id:140010). Using the **[projection operator method](@entry_id:265505)**, one can explicitly construct these basis vectors. For the ferromagnetic mode with moments along the c-axis, the unnormalized [basis vector](@entry_id:199546) in the 6D space $(S_{x1},S_{y1},S_{z1},S_{x2},S_{y2},S_{z2})$ is $(0,0,1,0,0,1)$. Normalizing this vector gives the final basis vector: $(\begin{matrix} 0  0  \frac{\sqrt{2}}{2}  0  0  \frac{\sqrt{2}}{2} \end{matrix})$. [@problem_id:3007057] This systematic, group-theory-based approach is indispensable for solving complex magnetic structures.

### Quantitative Analysis and Advanced Topics

Beyond determining the geometry of magnetic order, neutron scattering provides quantitative information about the magnitude of moments and the nature of [magnetic phase transitions](@entry_id:139255).

#### Magnetic Order Parameter

The intensity of a magnetic Bragg peak is not just a marker of [magnetic order](@entry_id:161845); its magnitude is directly related to the size of the ordered magnetic moments. The magnetic intensity $I_M$ is proportional to the square of the magnetic structure factor, which is itself linear in the moment magnitude $\mathbf{m}_j$. For a simple collinear magnetic structure, the integrated intensity of a magnetic Bragg peak is directly proportional to the square of the sublattice magnetization, or the [magnetic order](@entry_id:161845) parameter, $m(T)$:

$$
I_M(T) \propto m(T)^2
$$

This relationship is fundamental. It allows [neutron diffraction](@entry_id:140330) to be a primary experimental technique for studying [magnetic phase transitions](@entry_id:139255). By measuring the intensity of a magnetic peak as a function of temperature, one can directly track the evolution of the order parameter. Near a continuous (second-order) phase transition at the ordering temperature $T_N$ (the Néel temperature for an [antiferromagnet](@entry_id:137114)), the order parameter is expected to follow a power law:

$$
m(T) \propto \left(1 - \frac{T}{T_N}\right)^\beta
$$

where $\beta$ is the critical exponent for the order parameter. From the intensity measurements, one can extract $\beta$ by analyzing the relation $I_M(T) \propto (1 - T/T_N)^{2\beta}$. For example, if intensity measurements at $T_1=180\,$K and $T_2=190\,$K for a material with $T_N=200\,$K yielded a ratio $I(T_1)/I(T_2)=1.58$, one could solve for $\beta$ via $\frac{I_1}{I_2} = (\frac{1-T_1/T_N}{1-T_2/T_N})^{2\beta}$, which gives $\beta \approx 0.330$. [@problem_id:3007090]

#### Polarized Neutron Scattering

Using a beam of neutrons with their spins aligned—a **polarized neutron beam**—unlocks even more detailed information. When a polarized beam with initial polarization $\mathbf{P}_0$ scatters from a magnetic crystal, the cross-section contains additional terms beyond the simple sum of nuclear and magnetic intensities. The full expression for a detector that does not analyze the final polarization is:

$$
\frac{d\sigma}{d\Omega} \propto |N(\mathbf{Q})|^2 + |\mathbf{M}_\perp(\mathbf{Q})|^2 + 2\mathbf{P}_0 \cdot \text{Re}[N(\mathbf{Q})^* \mathbf{M}_\perp(\mathbf{Q})] + \mathbf{P}_0 \cdot i(\mathbf{M}_\perp(\mathbf{Q}) \times \mathbf{M}_\perp(\mathbf{Q})^*)
$$

Here, $N(\mathbf{Q})$ is the [nuclear structure](@entry_id:161466) factor. The third term is the **nuclear-magnetic interference term**. It is linear in the neutron polarization $\mathbf{P}_0$ and the [magnetic structure](@entry_id:201216) factor $\mathbf{M}_\perp$. This term is non-zero only when nuclear and [magnetic scattering](@entry_id:147236) coexist at the same $\mathbf{Q}$, and it depends on the [relative phase](@entry_id:148120) between the nuclear and magnetic structure factors. Crucially, this term is odd under reversal of the magnetization ($\mathbf{M} \to -\mathbf{M}$) and odd under reversal of the neutron polarization ($\mathbf{P}_0 \to -\mathbf{P}_0$). This property makes it invaluable for detecting weak magnetic signals and for determining the absolute orientation of magnetic moments. Because it averages to zero over domains with opposite magnetization, observing it requires a single-domain sample, often achieved by applying a magnetic field. [@problem_id:3007054] The fourth term is a **chiral term**, sensitive to non-coplanar or helical magnetic structures that lack [inversion symmetry](@entry_id:269948) combined with time reversal.

#### Beyond the Dipole Approximation: Multipolar Scattering

The standard scattering formalism assumes the interaction is purely between the neutron's [magnetic dipole moment](@entry_id:149826) and the dipole moment of the magnetic ions (the "[dipole approximation](@entry_id:152759)"). However, in many materials, particularly those with strong spin-orbit coupling like $f$-electron systems, the magnetization density around an ion is not spherical. This asphericity can be described by a multipole expansion, giving rise to [higher-order moments](@entry_id:266936) like magnetic quadrupoles, octupoles, and so on.

These **higher-order magnetic multipoles** can also scatter neutrons, but their contribution to the [scattering amplitude](@entry_id:146099) has a different dependence on the momentum transfer $\mathbf{Q}$. While the dipole contribution $\langle j_0(Q) \rangle$ is largest at $Q=0$, the contribution from a multipole of rank $l$ scales as $Q^l$ at low $Q$. Therefore, multipolar effects become appreciable only at higher momentum transfers, when the condition $|\mathbf{Q}| r_{\mathrm{mag}} \gtrsim 1$ is met, where $r_{\mathrm{mag}}$ is the radius of the magnetic shell. [@problem_id:3007107]

Experimental signatures of multipolar scattering include:
1.  Systematic deviations of the measured [magnetic form factor](@entry_id:136670) from the calculated dipolar [form factor](@entry_id:146590), especially at high $Q$.
2.  The appearance of magnetic intensity at Bragg reflections where the dipolar [magnetic structure](@entry_id:201216) factor is predicted to be zero by symmetry (a "dipole-forbidden" position). This occurs because the selection rules for vector (dipole) and tensor (quadrupole) quantities can be different.
3.  A unique signature in the polarization of the scattered beam. Techniques like **spherical neutron [polarimetry](@entry_id:158036)**, which measures the full change in the neutron polarization vector upon scattering, are exceptionally powerful for identifying and characterizing the nature of multipolar order. [@problem_id:3007107]

The study of such "hidden" multipolar order, which is not visible to conventional bulk magnetization measurements, represents a frontier in the investigation of [quantum materials](@entry_id:136741).